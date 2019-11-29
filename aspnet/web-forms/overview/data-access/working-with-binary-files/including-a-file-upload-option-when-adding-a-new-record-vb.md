---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-vb
title: 添加新记录时包括文件上传选项（VB） |Microsoft Docs
author: rick-anderson
description: 本教程演示如何创建允许用户输入文本数据和上传二进制文件的 Web 界面。 要说明可用的选项，请使用 t 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 5776281d-4637-4d1e-a65b-2621d2cade44
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-vb
msc.type: authoredcontent
ms.openlocfilehash: 8edaf1754eddd7b03f1c323d1bee13238582fc99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596921"
---
# <a name="including-a-file-upload-option-when-adding-a-new-record-vb"></a>添加新纪录时增加文件上载选项 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_VB.exe)或[下载 PDF](including-a-file-upload-option-when-adding-a-new-record-vb/_static/datatutorial56vb1.pdf)

> 本教程演示如何创建允许用户输入文本数据和上传二进制文件的 Web 界面。 为了说明可用于存储二进制数据的选项，一个文件将保存在数据库中，而另一个文件存储在文件系统中。

## <a name="introduction"></a>简介

在前两个教程中，我们探讨了用于存储与应用程序数据模型关联的二进制数据的技术，并介绍了如何使用 FileUpload 控件将文件从客户端发送到 web 服务器，以及如何在eb 控件。 但我们尚未讨论如何将上载的数据与数据模型关联。

在本教程中，我们将创建一个网页来添加新类别。 除了类别的 "名称" 和 "说明" 文本框外，此页还需要包含两个 FileUpload 控件：一个用于新的类别的图片，另一个用于小册子。 上载的图片将直接存储在 "新记录" 的 "`Picture`" 列中，而小册子将保存到 `~/Brochures` 文件夹中，该文件夹中的文件的路径保存在新的 "记录" `BrochurePath` 列中。

创建此新网页之前，需要更新体系结构。 `CategoriesTableAdapter` 的主查询不检索 `Picture` 列。 因此，自动生成的 `Insert` 方法仅具有 `CategoryName`、`Description`和 `BrochurePath` 字段的输入。 因此，需要在 TableAdapter 中创建一个提示所有四个 `Categories` 字段的附加方法。 还需要更新业务逻辑层中的 `CategoriesBLL` 类。

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>步骤1：将`InsertWithPicture`方法添加到`CategoriesTableAdapter`

创建[数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中的 `CategoriesTableAdapter` 后，我们将其配置为基于主查询自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句。 此外，我们还指导 TableAdapter 使用 DB 直接方法，该方法创建了方法 `Insert`、`Update`和 `Delete`。 这些方法执行自动生成的 `INSERT`、`UPDATE`和 `DELETE` 语句，因此，根据主查询返回的列接受输入参数。 在 "[上传文件](uploading-files-vb.md)" 教程中，我们扩充了 `CategoriesTableAdapter` 的主查询以使用 `BrochurePath` 列。

由于 `CategoriesTableAdapter` 的主查询不引用 `Picture` 列，因此不能添加新记录，也不能使用 `Picture` 列的值来更新现有记录。 为了捕获此信息，可以在 TableAdapter 中创建一个新方法，该方法专门用于插入包含二进制数据的记录，也可以自定义自动生成的 `INSERT` 语句。 自定义自动生成的 `INSERT` 语句的问题在于，我们可能会在向导覆盖自定义项时出现问题。 例如，假设我们自定义了 `INSERT` 语句以包括使用 `Picture` 列。 这会更新 TableAdapter `Insert` 方法，以便为类别的图片二进制数据包含一个附加输入参数。 然后，可以在业务逻辑层中创建一个方法来使用此 DAL 方法，并通过表示层调用此 BLL 方法，并 wonderfully。 也就是说，下一次通过 TableAdapter 配置向导配置 TableAdapter。 向导完成后，会立即覆盖对 `INSERT` 语句的自定义，`Insert` 方法会恢复为旧格式，并且我们的代码将不再编译！

> [!NOTE]
> 当使用存储过程而不是即席 SQL 语句时，这种干扰是不会出现的问题。 将来的教程将使用存储过程来替代数据访问层中的即席 SQL 语句。

为了避免这种潜在的麻烦，无需自定义自动生成的 SQL 语句，而是创建新的 TableAdapter 方法。 此方法命名为 `InsertWithPicture`，它将接受 `CategoryName`、`Description`、`BrochurePath`和 `Picture` 列的值，并执行 `INSERT` 语句，该语句将所有四个值存储在新记录中。

打开类型化数据集，然后在设计器中右键单击 `CategoriesTableAdapter` 的标头，然后从上下文菜单中选择 "添加查询"。 这将启动 "TableAdapter 查询配置向导"，该向导首先向我们询问 TableAdapter 查询应如何访问数据库。 选择 "使用 SQL 语句"，然后单击 "下一步"。 下一步将提示输入要生成的查询类型。 由于我们要创建一个查询，以便向 `Categories` 表中添加新记录，请选择 "插入"，然后单击 "下一步"。

[![选择插入选项](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image1.png)

**图 1**：选择插入选项（[单击以查看完全大小的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image2.png)）

现在，需要指定 `INSERT` SQL 语句。 向导会自动提出与 TableAdapter s 主查询对应的 `INSERT` 语句。 在这种情况下，它是插入 `CategoryName`、`Description`和 `BrochurePath` 值的 `INSERT` 语句。 更新语句，以便将 `Picture` 列与 `@Picture` 参数一起包含，如下所示：

[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample1.sql)]

向导的最后一个屏幕要求我们命名新的 TableAdapter 方法。 输入 `InsertWithPicture`，然后单击 "完成"。

[![命名新的 TableAdapter 方法 InsertWithPicture](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image3.png)

**图 2**：将新的 TableAdapter 方法命名 `InsertWithPicture` （[单击以查看完全大小的映像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image4.png)）

## <a name="step-2-updating-the-business-logic-layer"></a>步骤2：更新业务逻辑层

由于表示层只应使用业务逻辑层进行交互，而不是将其直接发送到数据访问层，因此，我们需要创建一个用于调用刚才创建的 DAL 方法（`InsertWithPicture`）的 BLL 方法。 对于本教程，请在名为 `InsertWithPicture` 的 `CategoriesBLL` 类中创建一个方法，该方法接受作为输入三 `String` s 和 `Byte` 数组。 `String` 输入参数适用于类别的 "名称"、"说明" 和 "小册子" 文件路径，而 "`Byte`" 数组用于 "类别" 图片的二进制内容。 如下面的代码所示，此 BLL 方法会调用相应的 DAL 方法：

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample2.vb)]

> [!NOTE]
> 在将 `InsertWithPicture` 方法添加到 BLL 之前，请确保已保存类型化数据集。 由于 `CategoriesTableAdapter` 类代码是根据类型化数据集自动生成的，因此，如果你不首先将更改保存到类型化数据集，则 `Adapter` 属性不会知道 `InsertWithPicture` 方法。

## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>步骤3：列出现有类别及其二进制数据

在本教程中，我们将创建一个页面，使最终用户能够向系统添加新类别，并为新类别提供图片和手册。 在[前面的教程](displaying-binary-data-in-the-data-web-controls-vb.md)中，我们使用了一个包含 TemplateField 和 ImageField 的 GridView 来显示每个类别的名称、说明、图片和下载其手册的链接。 在本教程中，让我们复制该功能，同时创建一个页面，其中列出了所有现有类别，并允许创建新的类别。

首先打开 `BinaryData` 文件夹中的 "`DisplayOrDownload.aspx`" 页。 请在 "源" 视图中，复制 GridView 和 ObjectDataSource 声明性语法，并将其粘贴到 `UploadInDetailsView.aspx`中的 `<asp:Content>` 元素内。 此外，别忘了将 `GenerateBrochureLink` 方法从 `DisplayOrDownload.aspx` 的代码隐藏类复制到 `UploadInDetailsView.aspx`中。

[![将声明性语法从 DisplayOrDownload 复制并粘贴到 UploadInDetailsView](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image5.png)

**图 3**：将声明性语法从 `DisplayOrDownload.aspx` 复制并粘贴到 `UploadInDetailsView.aspx` （[单击以查看完全大小的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image6.png)）

将声明性语法和 `GenerateBrochureLink` 方法复制到 "`UploadInDetailsView.aspx`" 页后，请通过浏览器查看该页，以确保已正确复制所有内容。 应该会看到一个 GridView，其中列出了8个类别，其中包含用于下载小册子和类别图片的链接。

[![现在应看到每个类别及其二进制数据](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image7.png)

**图 4**：你现在应看到每个类别及其二进制数据（[单击以查看完全大小的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image8.png)）

## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>步骤4：配置`CategoriesDataSource`以支持插入

`Categories` GridView 使用的 `CategoriesDataSource` ObjectDataSource 当前不提供插入数据的功能。 为了支持通过此数据源控件插入，我们需要将 `Insert` 方法映射到其基础对象中的方法 `CategoriesBLL`。 具体而言，我们想要将它映射到在步骤2中添加的 `CategoriesBLL` 方法，`InsertWithPicture`。

首先，单击 "ObjectDataSource s 智能" 标记中的 "配置数据源" 链接。 第一个屏幕显示数据源配置为使用的对象，`CategoriesBLL`。 将此设置保留原样，并单击 "下一步" 以转到 "定义数据方法" 屏幕。 转到 "插入" 选项卡，然后从下拉列表中选择 `InsertWithPicture` 方法。 单击“完成”按钮以完成向导。

[![将 ObjectDataSource 配置为使用 InsertWithPicture 方法](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image9.png)

**图 5**：将 ObjectDataSource 配置为使用 `InsertWithPicture` 方法（[单击查看完全大小的映像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image10.png)）

> [!NOTE]
> 完成该向导后，Visual Studio 可能会询问你是否要刷新字段和键，这将重新生成数据 Web 控件字段。 选择 "否"，因为选择 "是" 将覆盖你可能已进行的任何字段自定义。

完成向导后，ObjectDataSource 现在将包含其 `InsertMethod` 属性的值以及四个类别列 `InsertParameters`，如以下声明性标记所示：

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>步骤5：创建插入接口

第一次介绍了如何[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)，DetailsView 控件提供内置的插入界面，可在使用支持插入的数据源控件时使用。 让我们将一个 DetailsView 控件添加到此页面上，此页面将永久呈现其插入界面，使用户能够快速添加新类别。 在 DetailsView 中添加新类别时，它下面的 GridView 会自动刷新并显示新类别。

首先，将 DetailsView 从工具箱拖动到 GridView 上方的设计器，将其 `ID` 属性设置为 `NewCategory` 并清除 `Height` 和 `Width` 属性值。 在 "DetailsView s" 智能标记中，将其绑定到现有 `CategoriesDataSource`，然后选中 "启用插入" 复选框。

[![将 DetailsView 绑定到 CategoriesDataSource 并启用插入](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image11.png)

**图 6**：将 DetailsView 绑定到 `CategoriesDataSource` 并启用插入（[单击查看完全尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image12.png)）

若要在插入界面中永久渲染 DetailsView，请将其 `DefaultMode` 属性设置为 `Insert`。

请注意，DetailsView 具有五个 BoundFields `CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`和 `BrochurePath`，尽管 `CategoryID` BoundField 不在插入界面中呈现，因为它的 `InsertVisible` 属性设置为 `False`。 这些 BoundFields 存在，因为它们是 `GetCategories()` 方法返回的列，而 ObjectDataSource 调用此方法来检索其数据。 但对于插入，我们不想让用户指定 `NumberOfProducts`的值。 此外，我们还需要让他们为新类别上传图片，并上传小册子的 PDF。

完全删除 DetailsView 中的 `NumberOfProducts` BoundField，然后分别更新 `CategoryName` 的 `HeaderText` 属性，并将 `BrochurePath` BoundFields 分别更新为类别和小册子。 接下来，将 `BrochurePath` BoundField 转换为 TemplateField 并为该图片添加新的 TemplateField，为此新 TemplateField 提供 `HeaderText` 图片值。 移动 `Picture` TemplateField，使其位于 `BrochurePath` TemplateField 和 CommandField 之间。

![将 DetailsView 绑定到 CategoriesDataSource 并启用插入](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image7.gif)

**图 7**：将 DetailsView 绑定到 `CategoriesDataSource` 并启用插入

如果通过 "编辑字段" 对话框将 `BrochurePath` BoundField 转换为 TemplateField，则 TemplateField 包括 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 但是，只需要 `InsertItemTemplate`，因此可随意删除其他两个模板。 此时，DetailsView 的声明性语法应该如下所示：

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>为小册子和图片字段添加 FileUpload 控件

目前，`BrochurePath` TemplateField s `InsertItemTemplate` 包含一个文本框，而 `Picture` TemplateField 不包含任何模板。 我们需要更新这两个 TemplateField `InsertItemTemplate` s 才能使用 FileUpload 控件。

从 "DetailsView s" 智能标记中，选择 "编辑模板" 选项，然后从下拉列表中选择 `BrochurePath` TemplateField s `InsertItemTemplate`。 删除文本框，然后将 "FileUpload" 控件从 "工具箱" 拖放到模板中。 将 `ID` 的 FileUpload 控件设置为 `BrochureUpload`。 同样，将 FileUpload 控件添加到 `Picture` TemplateField s `InsertItemTemplate`。 将此 FileUpload 控件 `ID` 设置为 `PictureUpload`。

[![将 FileUpload 控件添加到则](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image13.png)

**图 8**：将 FileUpload 控件添加到 `InsertItemTemplate` （[单击以查看完全大小的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image14.png)）

进行这些添加后，这两个 TemplateField 的声明性语法将为：

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample5.aspx)]

当用户添加新类别时，我们希望确保手册和图片的文件类型正确。 对于小册子，用户必须提供 PDF。 对于该图片，我们需要用户上传一个图像文件，但还是允许使用特定类型的*任何*图像文件或仅图像文件（如 Gif 或 JPGs？ 为了允许不同的文件类型，我们需要将 `Categories` 架构扩展为包含一个捕获文件类型的列，以便可以通过 `DisplayCategoryPicture.aspx`中的 `Response.ContentType` 将此类型发送到客户端。 由于我们没有这样一列，因此将用户限制为只能提供特定的图像文件类型是明智的。 `Categories` 表的现有图像是位图，但对于通过 web 提供的图像而言，JPGs 是更合适的文件格式。

如果用户上传的文件类型不正确，则需要取消插入并显示一条指示问题的消息。 在 DetailsView 下添加标签 Web 控件。 将其 `ID` 属性设置为 "`UploadWarning`，清除其 `Text` 属性，将" `CssClass` "属性设置为" Warning "，将" `Visible` "和" `EnableViewState` "属性设置为 `False`。 `Warning` CSS 类在 `Styles.css` 中定义，并以一种较大的红色、斜体、粗体呈现文本。

> [!NOTE]
> 理想情况下，会将 `CategoryName` 和 `Description` BoundFields 转换为 Templatefield，并将其插入接口自定义。 例如，`Description` 插入界面可能更适合通过多行文本框。 由于 `CategoryName` 列不接受 `NULL` 值，因此应添加 RequiredFieldValidator 以确保用户为新类别的名称提供一个值。 这些步骤留给读者演练。 请返回[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)，深入了解如何增强数据修改接口。

## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>步骤6：将上传的手册保存到 Web 服务器的文件系统中

当用户输入新类别的值并单击 "插入" 按钮时，将发生回发和插入工作流将。 首先，将触发 DetailsView s [`ItemInserting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx)。 接下来，将调用 ObjectDataSource `Insert()` 方法，这会导致向 `Categories` 表中添加新的记录。 然后，将触发 DetailsView s 的[`ItemInserted` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx)。

在调用 ObjectDataSource `Insert()` 方法之前，必须首先确保用户上传了相应的文件类型，然后将小册子 PDF 保存到 web 服务器的文件系统。 为 DetailsView s `ItemInserting` 事件创建事件处理程序，并添加以下代码：

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample6.vb)]

事件处理程序通过引用 DetailsView 的模板中的 `BrochureUpload` FileUpload 控件开始。 如果已上传小册子，则会检查上传的文件的扩展名。 如果扩展不是，则为。PDF，则会显示警告，并取消插入操作，并且事件处理程序的执行将结束。

> [!NOTE]
> 依赖于已上传的文件扩展名并不是确保上传的文件是 PDF 文档的 "确认" 方法。 用户可能具有扩展名为 `.Brochure`的有效 PDF 文档，或者可能已使用了非 PDF 文档并向其提供了 `.pdf` 扩展。 为了更最终地验证文件类型，需要以编程方式检查文件 s 的二进制内容。 不过，这种完全方法通常是多余的;检查扩展是否足以应对大多数情况。

如[上传文件](uploading-files-vb.md)教程中所述，将文件保存到文件系统时必须小心，以便一个用户上传不会覆盖另一个。 在本教程中，我们将尝试使用与上传文件相同的名称。 但是，如果 `~/Brochures` 目录中已存在具有相同文件名的文件，则我们会在末尾追加一个数字，直到找到唯一名称。 例如，如果用户上传名为 `Meats.pdf`的小册子文件，但 `~/Brochures` 文件夹中已经有一个名为 `Meats.pdf` 的文件，则将保存的文件名更改为 `Meats-1.pdf`。 如果已存在，则我们会尝试 `Meats-2.pdf`等，直到找到唯一的文件名。

下面的代码使用[`File.Exists(path)` 方法](https://msdn.microsoft.com/library/system.io.file.exists.aspx)来确定是否已存在具有指定文件名的文件。 如果是这样，则会继续为小册子尝试新文件名，直到找不到冲突。

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample7.vb)]

如果找到有效的文件名，则需要将该文件保存到文件系统，并且必须更新 ObjectDataSource `brochurePath``InsertParameter` 值，以便将此文件名写入数据库。 正如我们在*上传文件*教程中看到的那样，可以使用 FileUpload 控件 `SaveAs(path)` 方法保存该文件。 若要更新 ObjectDataSource `brochurePath` 参数，请使用 `e.Values` 集合。

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample8.vb)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>步骤7：将上传的图片保存到数据库

若要将上载的图片存储在新的 `Categories` 记录中，需要将上传的二进制内容分配给 DetailsView s `ItemInserting` 事件中的 ObjectDataSource s `picture` 参数。 但在进行此分配之前，我们需要先确保上传的图片是 JPG，而不是其他图像类型。 如步骤6中所示，让我们使用上传的图片 s 文件扩展名来确定其类型。

虽然 `Categories` 表允许 `Picture` 列的 `NULL` 值，但所有类别当前都有图片。 允许用户在通过此页面添加新类别时提供图片。 以下代码将进行检查，以确保已上传图片，并且它具有适当的扩展名。

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample9.vb)]

此代码应放置在步骤6中的代码*之前*，因此，如果图片上传有问题，则在将小册子文件保存到文件系统之前，事件处理程序将终止。

假设已上传了适当的文件，请使用以下代码行将上传的二进制内容分配给图片参数 s 值：

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample10.vb)]

## <a name="the-completeiteminsertingevent-handler"></a>Complete`ItemInserting`事件处理程序

为完整起见，以下是完整的 `ItemInserting` 事件处理程序：

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample11.vb)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>步骤8：修复`DisplayCategoryPicture.aspx`页面

让我们花点时间来测试在过去几个步骤中创建的插入接口和 `ItemInserting` 事件处理程序。 通过浏览器访问 `UploadInDetailsView.aspx` 页面，尝试添加类别，但要省略照片，或者指定非 JPG 照片或非 PDF 手册。 在任何这些情况下，将显示一条错误消息并取消插入工作流。

[![如果上传了无效的文件类型，将显示一条警告消息](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image15.png)

**图 9**：如果上传了无效的文件类型，将显示一条警告消息（[单击以查看完全大小的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image16.png)）

验证页面是否需要上载图片，并且不接受非 PDF 或非 JPG 文件后，请使用有效的 JPG 图片添加新类别，使小册子字段保持为空。 单击 "插入" 按钮后，页面将回发，并将一个新记录添加到 `Categories` 表中，并将上传的图像 s 二进制内容直接存储在数据库中。 将更新 GridView 并为新添加的类别显示一行，但如图10所示，新的类别的图片不会正确呈现。

[![未显示新的类别的图片](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image17.png)

**图 10**：不显示新的类别图（[单击以查看完全尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image18.png)）

不显示新图片的原因是：返回指定的类别图片的 `DisplayCategoryPicture.aspx` 页面配置为处理具有 OLE 标头的位图。 在将该78字节标头发送回客户端之前，会将其从 `Picture` 列的二进制内容中去除。 但刚刚为新类别上传的 JPG 文件没有此 OLE 标头;因此，从图像的二进制数据中删除了有效的必要字节。

由于现在 `Categories` 表中的两个位图都带有 OLE 标头和 JPGs，我们需要更新 `DisplayCategoryPicture.aspx` 以便对原始八个类别进行 OLE 标头剥离，并跳过对较新类别记录的此项去除。 在下一教程中，我们将介绍如何更新现有的记录图像，并更新所有旧的类别图片，使其 JPGs。 不过，现在，在 `DisplayCategoryPicture.aspx` 中使用下面的代码来仅对那些具有以下八个类别的 OLE 标头进行去掉：

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample12.vb)]

进行此更改后，在 GridView 中，JPG 图像现在会正确呈现。

[已正确呈现新类别 ![JPG 图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image19.png)

**图 11**：已正确呈现新类别的 JPG 图像（[单击以查看完全尺寸的图像](including-a-file-upload-option-when-adding-a-new-record-vb/_static/image20.png)）

## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>步骤9：在出现异常时删除小册子

在 web 服务器的文件系统上存储二进制数据的一个挑战是，它在数据模型与其二进制数据之间引入了断开连接。 因此，在删除记录时，还必须删除文件系统上相应的二进制数据。 插入时也可能会出现这种情况。 请考虑以下方案：用户添加了一个新类别，指定了有效的图片和手册。 单击 "插入" 按钮时，会发生回发并引发 DetailsView s `ItemInserting` 事件，将小册子保存到 web 服务器的文件系统。 接下来，调用 ObjectDataSource s `Insert()` 方法，该方法调用 `CategoriesBLL` 类 s `InsertWithPicture` 方法，该方法调用 `CategoriesTableAdapter` 的 `InsertWithPicture` 方法。

现在，如果数据库处于脱机状态，或者在 `INSERT` SQL 语句中出错，会发生什么情况呢？ 显然，插入将失败，因此不会向数据库添加新的类别行。 但我们仍将上传的小册子文件放在 web 服务器的文件系统上！ 在插入工作流的过程中，需要删除此文件。

如前文所述，在[ASP.NET Page 教程中处理 BLL 和 DAL 级别的异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)中，从体系结构的深度中引发异常时，它通过各个层向上冒泡。 在表示层，我们可以确定 DetailsView s `ItemInserted` 事件是否发生了异常。 此事件处理程序还提供了 ObjectDataSource `InsertParameters`的值。 因此，我们可以为 `ItemInserted` 事件创建事件处理程序，该事件检查是否存在异常，如果是，则删除由 ObjectDataSource s `brochurePath` 参数指定的文件：

[!code-vb[Main](including-a-file-upload-option-when-adding-a-new-record-vb/samples/sample13.vb)]

## <a name="summary"></a>总结

为了提供一个基于 web 的界面来添加包含二进制数据的记录，必须执行许多步骤。 如果二进制数据直接存储在数据库中，则需要更新体系结构，添加特定方法来处理二进制数据的插入事例。 更新体系结构后，下一步就是创建插入界面，该界面可以使用已自定义的 DetailsView 来实现，以包含每个二进制数据字段的 FileUpload 控件。 然后，可以将上传的数据保存到 web 服务器的文件系统中，或将其分配给 DetailsView s `ItemInserting` 事件处理程序中的数据源参数。

将二进制数据保存到文件系统比将数据直接保存到数据库需要更多的计划。 必须选择命名方案才能避免一个用户上传覆盖另一个。 此外，如果数据库插入失败，则必须执行额外的步骤以删除上载的文件。

现在，我们可以使用小册子和图片向系统添加新类别，但我们尚未介绍如何更新现有类别的二进制数据，或者如何正确删除已删除类别的二进制数据。 下一教程将介绍这两个主题。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Dave Gardner、Teresa Murphy 和 Bernadette Leigh。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](displaying-binary-data-in-the-data-web-controls-vb.md)
> [下一页](updating-and-deleting-existing-binary-data-vb.md)
