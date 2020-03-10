---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
title: 更新和删除现有的二进制数据C#（） |Microsoft Docs
author: rick-anderson
description: 在前面的教程中，我们看到了 GridView 控件如何使编辑和删除文本数据变得简单。 在本教程中，我们将了解 GridView 控件如何进行 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 35798f21-1606-434b-83f8-30166906ef49
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e37381ee48fcda8e0e10374aa7a6ae53c3cc77c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78475142"
---
# <a name="updating-and-deleting-existing-binary-data-c"></a>上载和删除现有的二进制数据 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_CS.exe)或[下载 PDF](updating-and-deleting-existing-binary-data-cs/_static/datatutorial57cs1.pdf)

> 在前面的教程中，我们看到了 GridView 控件如何使编辑和删除文本数据变得简单。 在本教程中，我们将了解 GridView 控件如何还可以编辑和删除二进制数据，无论二进制数据是保存在数据库中，还是存储在文件系统中。

## <a name="introduction"></a>简介

过去三个教程中，我们添加了相当多的功能来处理二进制数据。 首先，将 `BrochurePath` 列添加到 `Categories` 表，并相应地更新体系结构。 此外，我们还添加了 "数据访问层" 和 "业务逻辑层" 方法来使用 "类别" 表的 "现有 `Picture`" 列，其中包含图像文件的二进制内容。 我们构建了一个网页，用于在 GridView 中显示二进制数据，其中的 "类别" 图片显示在 "`<img>`" 元素中，并已添加了 DetailsView 以允许用户添加新类别并上传其小册子和图片数据。

仍要实现的所有功能都是编辑和删除现有类别的功能，我们将在本教程中使用 GridView 内置的编辑和删除功能完成这项工作。 编辑类别时，用户可以选择上传新图片，也可以让类别继续使用现有图片。 对于小册子，他们可以选择使用现有小册子、上传新小册子，或指示该类别不再有与之相关联的小册子。 让我们开始吧！

## <a name="step-1-updating-the-data-access-layer"></a>步骤1：更新数据访问层

DAL 具有自动生成的 `Insert`、`Update`和 `Delete` 方法，但这些方法是根据 `CategoriesTableAdapter` 的主查询生成的，该查询不包括 `Picture` 列。 因此，`Insert` 和 `Update` 方法不包含用于指定类别的图片的二进制数据的参数。 正如[前面的教程](including-a-file-upload-option-when-adding-a-new-record-cs.md)中所述，在指定二进制数据时，我们需要创建一个新的 TableAdapter 方法来更新 `Categories` 表。

打开类型化数据集，然后在设计器中右键单击 `CategoriesTableAdapter` 的标头，然后从上下文菜单中选择 "添加查询" 以启动 "TableAdapter 查询配置向导"。 此向导首先向我们询问 TableAdapter 查询应如何访问数据库。 选择 "使用 SQL 语句"，然后单击 "下一步"。 下一步将提示输入要生成的查询类型。 由于我们要创建一个查询以将新记录添加到 `Categories` 表中，因此请选择 "更新"，然后单击 "下一步"。

[![选择更新选项](updating-and-deleting-existing-binary-data-cs/_static/image1.gif)](updating-and-deleting-existing-binary-data-cs/_static/image1.png)

**图 1**：选择更新选项（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image2.png)）

现在，需要指定 `UPDATE` SQL 语句。 向导会自动提出与 TableAdapter s 主查询（更新 `CategoryName`、`Description`和 `BrochurePath` 值）对应的 `UPDATE` 语句。 更改语句，使 `Picture` 列随 `@Picture` 参数一起提供，如下所示：

[!code-sql[Main](updating-and-deleting-existing-binary-data-cs/samples/sample1.sql)]

向导的最后一个屏幕要求我们命名新的 TableAdapter 方法。 输入 `UpdateWithPicture`，然后单击 "完成"。

[![命名新的 TableAdapter 方法 UpdateWithPicture](updating-and-deleting-existing-binary-data-cs/_static/image2.gif)](updating-and-deleting-existing-binary-data-cs/_static/image3.png)

**图 2**：将新的 TableAdapter 方法命名 `UpdateWithPicture` （[单击以查看完全大小的映像](updating-and-deleting-existing-binary-data-cs/_static/image4.png)）

## <a name="step-2-adding-the-business-logic-layer-methods"></a>步骤2：添加业务逻辑层方法

除了更新 DAL 之外，我们还需要更新 BLL，使其包含用于更新和删除类别的方法。 这些是将从表示层调用的方法。

对于删除类别，可以使用 `CategoriesTableAdapter` 自动生成的 `Delete` 方法。 将以下方法添加到 `CategoriesBLL` 类：

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample2.cs)]

对于本教程，我们将创建两种方法用于更新类别-一种方法需要二进制图片数据，并调用我们刚刚添加到 `CategoriesTableAdapter` 中的 `UpdateWithPicture` 方法，另一种方法只接受 `CategoryName`、`Description`和 `BrochurePath` 值，并使用 `CategoriesTableAdapter` 类自动生成的 `Update` 语句。 使用两种方法背后的基本原理是，在某些情况下，用户可能需要更新类别的图片及其其他字段，在这种情况下，用户必须上传新图片。 然后，可以在 `UPDATE` 语句中使用上传的图片的二进制数据。 在其他情况下，用户可能只需要更新名称和说明。 但如果 `UPDATE` 语句也需要 `Picture` 列的二进制数据，则我们还需要提供该信息。 这需要额外的数据库行程才能恢复正在编辑的记录的图片数据。 因此，我们需要两个 `UPDATE` 方法。 业务逻辑层根据更新类别时是否提供图片数据，确定要使用哪一个。

为此，请将两个方法添加到 `CategoriesBLL` 类，这两个方法都命名为 `UpdateCategory`。 第一个应接受三个 `string` s、`byte` 数组和 `int` 作为其输入参数;第二个只是三个 `string` s 和一个 `int`。 `string` 输入参数适用于类别的 "名称"、"说明" 和 "小册子" 文件路径，`byte` 数组适用于类别的图片的二进制内容，`int` 标识要更新的记录的 `CategoryID`。 请注意，如果传入的 `byte` 数组 `null`，则第一个重载将调用第二个：

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample3.cs)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>步骤3：通过插入和查看功能进行复制

在[前面的教程](including-a-file-upload-option-when-adding-a-new-record-cs.md)中，我们创建了一个名为 `UploadInDetailsView.aspx` 的页面，该页面列出了 GridView 中的所有类别，并提供了 DetailsView 来向系统添加新类别。 在本教程中，我们将对 GridView 进行扩展，以包括编辑和删除支持。 请不要从 `UploadInDetailsView.aspx`中继续工作，而是将本教程的更改从同一文件夹 `~/BinaryData`放置在 `UpdatingAndDeleting.aspx` 页中。 将声明性标记和代码从 `UploadInDetailsView.aspx` 复制并粘贴到 `UpdatingAndDeleting.aspx`中。

首先打开 "`UploadInDetailsView.aspx`" 页。 复制 `<asp:Content>` 元素中的所有声明性语法，如图3所示。 接下来，打开 `UpdatingAndDeleting.aspx` 并在其 `<asp:Content>` 元素中粘贴此标记。 同样，将 `UploadInDetailsView.aspx` 页 s 代码隐藏类中的代码复制到 `UpdatingAndDeleting.aspx`。

[![从 UploadInDetailsView 复制声明性标记](updating-and-deleting-existing-binary-data-cs/_static/image3.gif)](updating-and-deleting-existing-binary-data-cs/_static/image5.png)

**图 3**：从 `UploadInDetailsView.aspx` 复制声明性标记（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image6.png)）

复制声明性标记和代码后，请访问 `UpdatingAndDeleting.aspx`。 你应看到相同的输出，并且与上一教程中的 "`UploadInDetailsView.aspx`" 页具有相同的用户体验。

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>步骤4：将删除支持添加到 ObjectDataSource 和 GridView

正如我们在[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中讨论的那样，GridView 提供内置的删除功能，如果网格中的基础数据源支持删除，则可以在 checkbox 的勾选标记中启用这些功能。 当前 GridView 绑定到的 ObjectDataSource （`CategoriesDataSource`）不支持删除。

若要解决此情况，请单击 "ObjectDataSource s 智能" 标记中的 "配置数据源" 选项以启动向导。 第一个屏幕显示 ObjectDataSource 配置为使用 `CategoriesBLL` 类。 单击 "下一步"。 目前仅指定 ObjectDataSource `InsertMethod` 和 `SelectMethod` 属性。 但是，向导将分别自动填充 "更新" 和 "删除" 选项卡中的下拉列表，分别分别为 `UpdateCategory` 和 `DeleteCategory` 方法。 这是因为在 `CategoriesBLL` 类中，我们使用 `DataObjectMethodAttribute` 作为更新和删除的默认方法来标记这些方法。

现在，将 "更新" 选项卡 s 下拉列表设置为 "（无）"，但将 "删除选项卡 s" 下拉列表设置为 "`DeleteCategory`"。 我们将在步骤6中返回到此向导，以添加更新支持。

[![将 ObjectDataSource 配置为使用 DeleteCategory 方法](updating-and-deleting-existing-binary-data-cs/_static/image4.gif)](updating-and-deleting-existing-binary-data-cs/_static/image7.png)

**图 4**：将 ObjectDataSource 配置为使用 `DeleteCategory` 方法（[单击查看完全大小的映像](updating-and-deleting-existing-binary-data-cs/_static/image8.png)）

> [!NOTE]
> 完成该向导后，Visual Studio 可能会询问你是否要刷新字段和键，这将重新生成数据 Web 控件字段。 选择 "否"，因为选择 "是" 将覆盖你可能已进行的任何字段自定义。

ObjectDataSource 现在将为其 `DeleteMethod` 属性和 `DeleteParameter`包含一个值。 请记住，使用该向导指定方法时，Visual Studio 会将 ObjectDataSource `OldValuesParameterFormatString` 属性设置为 `original_{0}`，这将导致更新和删除方法调用出现问题。 因此，请完全清除此属性，或将其重置为默认 `{0}`。 如果需要刷新此 ObjectDataSource 属性的内存，请参阅[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程的概述。

完成向导并修复 `OldValuesParameterFormatString`后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample4.aspx)]

配置 ObjectDataSource 后，通过选中 GridView s 智能标记中的 "启用删除" 复选框，将删除功能添加到 GridView。 这会将 CommandField 添加到 GridView，其 `ShowDeleteButton` 属性设置为 `true`。

[![支持在 GridView 中删除](updating-and-deleting-existing-binary-data-cs/_static/image5.gif)](updating-and-deleting-existing-binary-data-cs/_static/image9.png)

**图 5**：启用在 GridView 中删除支持（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image10.png)）

请花点时间测试删除功能。 `Products` 表 s `CategoryID` 和 `Categories` 表 `CategoryID`之间存在外键，因此，如果您尝试删除前八个类别中的任何一种，您将获得外键约束冲突异常。 若要测试此功能，请添加一个新类别，同时提供小册子和图片。 图6所示的 "我的测试" 类别包括一个名为 `Test.pdf` 的测试小册子文件和一个测试图片。 图7显示了测试类别添加后的 GridView。

[![使用小册子和图像添加测试类别](updating-and-deleting-existing-binary-data-cs/_static/image6.gif)](updating-and-deleting-existing-binary-data-cs/_static/image11.png)

**图 6**：使用小册子和图像添加测试类别（[单击以查看完全尺寸的图像](updating-and-deleting-existing-binary-data-cs/_static/image12.png)）

[插入测试类别后 ![，它将显示在 GridView 中](updating-and-deleting-existing-binary-data-cs/_static/image7.gif)](updating-and-deleting-existing-binary-data-cs/_static/image13.png)

**图 7**：插入测试类别后，它将显示在 GridView 中（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image14.png)）

在 Visual Studio 中，刷新解决方案资源管理器。 你现在应该会在 `~/Brochures` 文件夹中看到一个新文件，`Test.pdf` （请参阅图8）。

接下来，单击 "测试类别" 行中的 "删除" 链接，使页面回发并引发 `CategoriesBLL` 类 `DeleteCategory` 方法。 这将调用 DAL s `Delete` 方法，导致适当的 `DELETE` 语句发送到数据库。 然后，将数据重新绑定到 GridView，并将标记发送回该测试类别不再存在的客户端。

尽管 "删除" 工作流从 `Categories` 表中成功删除了测试类别记录，但它并未从 web 服务器的文件系统中删除其手册文件。 刷新解决方案资源管理器，你将看到 `Test.pdf` 仍处于 `~/Brochures` 文件夹中。

![未从 Web 服务器的文件系统中删除 Test .pdf 文件](updating-and-deleting-existing-binary-data-cs/_static/image8.gif)

**图 8**：未从 Web 服务器的文件系统中删除 `Test.pdf` 文件

## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>步骤5：删除已删除的类别小册子文件

将二进制数据存储在数据库外部的缺点之一是，在删除关联的数据库记录时，必须采取额外的步骤来清理这些文件。 GridView 和 ObjectDataSource 提供在执行 delete 命令之前和之后激发的事件。 我们实际上需要为操作前和操作后事件创建事件处理程序。 删除 `Categories` 记录之前，我们需要确定其 PDF 文件路径，但不需要在删除类别之前删除 PDF，以防出现一些异常并且未删除类别。

在调用 ObjectDataSource s delete 命令之前激发了 GridView [`RowDeleting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)，而其[`RowDeleted` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx)在之后引发。 使用以下代码创建这两个事件的事件处理程序：

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample5.cs)]

在 `RowDeleting` 事件处理程序中，正在删除的行的 `CategoryID` 是从 GridView 的 `DataKeys` 集合中进行的，可以通过 `e.Keys` 集合在此事件处理程序中访问该集合。 接下来，调用 `CategoriesBLL` 类 `GetCategoryByCategoryID(categoryID)`，以返回有关要删除的记录的信息。 如果返回的 `CategoriesDataRow` 对象具有非`NULL``BrochurePath` 值，则它将存储在页变量中 `deletedCategorysPdfPath` 以便可以在 `RowDeleted` 事件处理程序中删除该文件。

> [!NOTE]
> 不是检索在 `RowDeleting` 事件处理程序中删除的 `Categories` 记录的 `BrochurePath` 详细信息，还可以将 `BrochurePath` 添加到 GridView s `DataKeyNames` 属性，并通过 `e.Keys` 集合访问记录 s 值。 这样做会稍微增加 GridView 的视图状态大小，但会减少所需的代码量，并保存到数据库的行程。

调用 ObjectDataSource s 基础 delete 命令后，将激发 GridView s `RowDeleted` 事件处理程序。 如果删除数据时没有任何例外，并且有 `deletedCategorysPdfPath`的值，则会从文件系统中删除 PDF。 请注意，清除与图片关联的类别的二进制数据不需要此额外代码。 这是因为图片数据直接存储在数据库中，因此删除 `Categories` 行将同时删除该类别的图片数据。

添加这两个事件处理程序后，再次运行此测试用例。 删除类别时，也会删除其关联的 PDF。

更新现有记录的关联二进制数据可提供一些有趣的挑战。 本教程的其余部分深入研究了将更新功能添加到小册子和图片中。 步骤6探讨了在步骤7查看更新图片时更新手册信息的方法。

## <a name="step-6-updating-a-category-s-brochure"></a>步骤6：更新类别手册

如关于[插入、更新和删除数据的概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中所述，GridView 提供内置行级编辑支持，如果正确配置了其基础数据源，则可以通过 checkbox 的勾选来实现这些支持。 目前，`CategoriesDataSource` ObjectDataSource 尚未配置为包含更新支持，因此让我们将其添加到中。

单击 "ObjectDataSource" 向导中的 "配置数据源" 链接，然后转到第二步。 由于在 `CategoriesBLL`中使用的 `DataObjectMethodAttribute`，更新下拉列表应自动使用接受四个输入参数的 `UpdateCategory` 重载（对于所有列，但 `Picture`）进行填充。 更改此参数，使其使用具有五个参数的重载。

[![将 ObjectDataSource 配置为使用包含图片参数的 UpdateCategory 方法](updating-and-deleting-existing-binary-data-cs/_static/image9.gif)](updating-and-deleting-existing-binary-data-cs/_static/image15.png)

**图 9**：将 ObjectDataSource 配置为使用包括 `Picture` 参数的 `UpdateCategory` 方法（[单击查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image16.png)）

ObjectDataSource 现在将包含其 `UpdateMethod` 属性的值以及对应的 `UpdateParameter`。 如步骤4中所述，在使用 "配置数据源" 向导时，Visual Studio 将 `OldValuesParameterFormatString` 属性设置为 `original_{0}`。 这将导致更新和删除方法调用出现问题。 因此，请完全清除此属性，或将其重置为默认 `{0}`。

完成向导并修复 `OldValuesParameterFormatString`后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample6.aspx)]

若要启用 GridView s 内置编辑功能，请从 GridView s 智能标记中选中 "启用编辑" 选项。 这会将 CommandField `ShowEditButton` 属性设置为 `true`，导致添加 "编辑" 按钮（并为正在编辑的行添加 "更新" 和 "取消" 按钮）。

[![配置 GridView 以支持编辑](updating-and-deleting-existing-binary-data-cs/_static/image10.gif)](updating-and-deleting-existing-binary-data-cs/_static/image17.png)

**图 10**：配置 GridView 以支持编辑（[单击查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image18.png)）

通过浏览器访问页面，然后单击 "编辑" 按钮之一。 `CategoryName` 和 `Description` BoundFields 以文本框的形式呈现。 `BrochurePath` TemplateField 缺少 `EditItemTemplate`，因此它将继续显示其 `ItemTemplate` 到小册子的链接。 `Picture` ImageField 呈现为一个文本框，其 `Text` 属性分配有 `DataImageUrlField` 值的值（在本例中为 `CategoryID`）。

[![GridView 缺少用于 BrochurePath 的编辑界面](updating-and-deleting-existing-binary-data-cs/_static/image11.gif)](updating-and-deleting-existing-binary-data-cs/_static/image19.png)

**图 11**： GridView 缺少 `BrochurePath` 的编辑界面（[单击查看全尺寸图像](updating-and-deleting-existing-binary-data-cs/_static/image20.png)）

## <a name="customizing-thebrochurepaths-editing-interface"></a>自定义编辑界面`BrochurePath`

需要为 `BrochurePath` TemplateField 创建一个编辑界面，该界面允许用户执行以下操作之一：

- 按原样保留类别小册子，
- 通过上传新的小册子或
- 完全删除类别的小册子（如果类别不再有关联的小册子）。

我们还需要更新 `Picture` ImageField s 编辑界面，但我们将在步骤7中介绍这一点。

从 GridView s 智能标记中，单击 "编辑模板" 链接，然后从下拉列表中选择 `BrochurePath` TemplateField s `EditItemTemplate`。 将 RadioButtonList Web 控件添加到此模板，将其 `ID` 属性设置为 "`BrochureOptions`"，并将其 `AutoPostBack` 属性设置为 "`true`"。 在属性窗口中，单击 `Items` 属性中的省略号，这将显示 "`ListItem` 集合编辑器"。 分别添加以下三个选项，分别 `Value` s 1、2和3：

- 使用当前手册
- 删除当前小册子
- 上传新小册子

将第一个 `ListItem` `Selected` 属性设置为 "`true`"。

![将三个 ListItems 添加到 RadioButtonList](updating-and-deleting-existing-binary-data-cs/_static/image12.gif)

**图 12**：向 RadioButtonList 添加三个 `ListItem`

在 RadioButtonList 下，添加名为 `BrochureUpload`的 FileUpload 控件。 将其 `Visible` 属性设置为 `false`。

[![将 RadioButtonList 和 FileUpload 控件添加到 EditItemTemplate](updating-and-deleting-existing-binary-data-cs/_static/image13.gif)](updating-and-deleting-existing-binary-data-cs/_static/image21.png)

**图 13**：将 RadioButtonList 和 FileUpload 控件添加到 `EditItemTemplate` （[单击查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image22.png)）

此 RadioButtonList 为用户提供三个选项。 其思想是，只有在选择了最后一个选项 "上传新的小册子" 时才会显示 FileUpload 控件。 若要完成此操作，请为 RadioButtonList s `SelectedIndexChanged` 事件创建事件处理程序，并添加以下代码：

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample7.cs)]

由于 RadioButtonList 和 FileUpload 控件在模板中，因此我们必须编写一些代码以编程方式访问这些控件。 `SelectedIndexChanged` 事件处理程序在 `sender` 输入参数中传递了 RadioButtonList 的引用。 若要获取 FileUpload 控件，需要获取 RadioButtonList 的父控件，并在其中使用 `FindControl("controlID")` 方法。 一旦我们引用了 RadioButtonList 和 FileUpload 控件，FileUpload control s `Visible` 属性将设置为仅当 RadioButtonList `SelectedValue` 等于3时才 `true`，这是上传新手册 `ListItem`的 `Value`。

使用此代码后，请花点时间测试编辑界面。 单击行的 "编辑" 按钮。 最初，应选择 "使用当前小册子" 选项。 更改所选索引会导致回发。 如果选择第三个选项，则会显示 FileUpload 控件，否则将隐藏该控件。 图14显示第一次单击 "编辑" 按钮时的编辑界面;图15显示了 "上传新的小册子" 选项之后的界面。

[![，请先选择 "使用当前小册子" 选项](updating-and-deleting-existing-binary-data-cs/_static/image14.gif)](updating-and-deleting-existing-binary-data-cs/_static/image23.png)

**图 14**：最初选择了 "使用当前小册子" 选项（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image24.png)）

[![选择 "上传新小册子" 选项会显示 FileUpload 控件](updating-and-deleting-existing-binary-data-cs/_static/image15.gif)](updating-and-deleting-existing-binary-data-cs/_static/image25.png)

**图 15**：选择 "上传新小册子" 选项会显示 FileUpload 控件（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image26.png)）

## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>保存小册子文件并更新`BrochurePath`列

单击 "GridView s 更新" 按钮时，将激发其 `RowUpdating` 事件。 调用 ObjectDataSource s update 命令，然后激发 GridView s `RowUpdated` 事件。 与删除工作流一样，我们需要为这两个事件创建事件处理程序。 在 `RowUpdating` 事件处理程序中，我们需要根据 `BrochureOptions` RadioButtonList 的 `SelectedValue` 确定要执行的操作：

- 如果 `SelectedValue` 为1，则需要继续使用相同的 `BrochurePath` 设置。 因此，需要将 ObjectDataSource `brochurePath` 参数设置为要更新的记录的现有 `BrochurePath` 值。 可以使用 `e.NewValues["brochurePath"] = value`设置 `brochurePath` 的 ObjectDataSource 参数。
- 如果 `SelectedValue` 为2，则需要将记录的 `BrochurePath` 值设置为 `NULL`。 这可以通过将 ObjectDataSource `brochurePath` 参数设置为 `Nothing`来实现，这将导致 `UPDATE` 语句中使用数据库 `NULL`。 如果正在删除现有的小册子文件，则需要删除现有文件。 但是，如果更新完成时不引发异常，我们只需要执行此操作。
- 如果 `SelectedValue` 为3，则我们需要确保用户已上传 PDF 文件，然后将其保存到文件系统并更新记录的 `BrochurePath` 列值。 此外，如果存在要替换的现有小册子文件，则需要删除之前的文件。 但是，如果更新完成时不引发异常，我们只需要执行此操作。

RadioButtonList s `SelectedValue` 为3时需要完成的步骤与 DetailsView s `ItemInserting` 事件处理程序使用的步骤完全相同。 当从我们在[上一教程](including-a-file-upload-option-when-adding-a-new-record-cs.md)中添加的 DetailsView 控件添加新的类别记录时，将执行此事件处理程序。 因此，它 behooves 将此功能重构为单独的方法。 具体而言，我将常用功能移到了两个方法中：

- `ProcessBrochureUpload(FileUpload, out bool)` 接受 FileUpload 控件实例作为输入，并使用输出布尔值指定是否应继续执行删除或编辑操作，或者是否应因某些验证错误而取消该操作。 如果未保存文件，此方法将返回保存的文件的路径或 `null`。
- 如果未 `null``deletedCategorysPdfPath`，`DeleteRememberedBrochurePath` 会删除页面变量中路径指定的文件 `deletedCategorysPdfPath`。

这两个方法的代码如下所示。 请注意上一教程中 `ProcessBrochureUpload` 与 DetailsView s `ItemInserting` 事件处理程序之间的相似性。 在本教程中，我已更新 DetailsView 的事件处理程序，以使用这些新方法。 下载与本教程关联的代码，查看 DetailsView 事件处理程序的修改情况。

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample8.cs)]

GridView `RowUpdating` 和 `RowUpdated` 事件处理程序使用 `ProcessBrochureUpload` 和 `DeleteRememberedBrochurePath` 方法，如以下代码所示：

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample9.cs)]

请注意，`RowUpdating` 事件处理程序如何使用一系列条件语句基于 `BrochureOptions` RadioButtonList s `SelectedValue` 属性值执行适当的操作。

使用此代码后，可以编辑类别，并使其使用当前小册子，不使用小册子，或上传新的手册。 继续尝试。在 `RowUpdating` 中设置断点，并 `RowUpdated` 事件处理程序获取工作流。

## <a name="step-7-uploading-a-new-picture"></a>步骤7：上传新图片

`Picture` ImageField s 编辑界面呈现为一个文本框，其中填充了其 `DataImageUrlField` 属性中的值。 在编辑工作流期间，GridView 会将参数传递给 ObjectDataSource，参数为 ImageField s `DataImageUrlField` 属性的值，而参数的值为输入到编辑界面的文本框中的值。 此行为适用于将图像保存为文件系统上的文件并且 `DataImageUrlField` 包含映像的完整 URL 的情况。 在这种情况下，编辑界面会在文本框中显示图像 s URL，用户可以更改该 URL 并将其保存回数据库。 当然，此默认接口不允许用户上传新图像，但它允许他们将图像的 URL 从当前值更改为另一个值。 但对于本教程而言，ImageField s 默认编辑接口无法满足要求，因为 `Picture` 二进制数据直接存储在数据库中，并且 `DataImageUrlField` 属性仅包含 `CategoryID`。

为了更好地了解当用户使用 ImageField 编辑行时在本教程中所发生的情况，请考虑以下示例：用户使用 `CategoryID` 10 编辑行，导致 `Picture` ImageField 呈现为带有值10的文本框。 假设用户将此文本框中的值更改为50，然后单击 "更新" 按钮。 发生回发，GridView 最初使用值50创建名为 `CategoryID` 的参数。 但是，在 GridView 发送此参数（以及 `CategoryName` 和 `Description` 参数）之前，它将添加到 `DataKeys` 集合的值中。 因此，它会用当前行的基础 `CategoryID` 值10覆盖 `CategoryID` 参数。 简而言之，ImageField s 编辑界面对此教程的编辑工作流不会有任何影响，因为 ImageField `DataImageUrlField` 属性的名称和网格 `DataKey` 值是相同的。

尽管 ImageField 可让你轻松地根据数据库数据显示图像，但我们并不想在编辑界面中提供 textbox。 相反，我们希望提供一个 FileUpload 控件，最终用户可以使用该控件更改类别的图片。 与 `BrochurePath` 值不同，对于这些教程，我们决定要求每个类别都有一张图片。 因此，我们不需要让用户指出没有关联的图片。用户可以上载新图片，也可以原样保留当前图片。

若要自定义 ImageField s 编辑界面，需要将其转换为 TemplateField。 从 GridView s 智能标记中，单击 "编辑列" 链接，选择 "ImageField"，然后单击 "将此字段转换为 TemplateField" 链接。

![将 ImageField 转换为 TemplateField](updating-and-deleting-existing-binary-data-cs/_static/image16.gif)

**图 16**：将 ImageField 转换为 TemplateField

以这种方式将 ImageField 转换为 TemplateField 会生成包含两个模板的 TemplateField。 如下面的声明性语法所示，`ItemTemplate` 包含一个图像 Web 控件，该控件的 `ImageUrl` 属性基于 ImageField s `DataImageUrlField` 和 `DataImageUrlFormatString` 属性使用数据绑定语法分配。 `EditItemTemplate` 包含一个文本框，其 `Text` 属性绑定到由 `DataImageUrlField` 属性指定的值。

[!code-aspx[Main](updating-and-deleting-existing-binary-data-cs/samples/sample10.aspx)]

需要将 `EditItemTemplate` 更新为使用 FileUpload 控件。 在 GridView s 智能标记中，单击 "编辑模板" 链接，然后从下拉列表中选择 `Picture` TemplateField s `EditItemTemplate`。 在模板中，应会看到一个文本框，将其删除。 接下来，将 "FileUpload" 控件从 "工具箱" 拖放到模板中，将其 `ID` 设置为 "`PictureUpload`"。 同时添加文本以更改类别的图片，指定新图片。 若要使类别的图片保持不变，请将该字段保留为空。

[![将 FileUpload 控件添加到 EditItemTemplate](updating-and-deleting-existing-binary-data-cs/_static/image17.gif)](updating-and-deleting-existing-binary-data-cs/_static/image27.png)

**图 17**：将 FileUpload 控件添加到 `EditItemTemplate` （[单击查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image28.png)）

自定义编辑界面后，在浏览器中查看进度。 在只读模式下查看行时，类别的图像将显示在之前，但单击 "编辑" 按钮会将图片列呈现为带有 FileUpload 控件的文本。

[![编辑界面包含 FileUpload 控件](updating-and-deleting-existing-binary-data-cs/_static/image18.gif)](updating-and-deleting-existing-binary-data-cs/_static/image29.png)

**图 18**：编辑界面包含一个 FileUpload 控件（[单击以查看完全大小的图像](updating-and-deleting-existing-binary-data-cs/_static/image30.png)）

请记住，ObjectDataSource 配置为调用 `CategoriesBLL` 类的 `UpdateCategory` 方法，该方法接受将图片的二进制数据作为 `byte` 数组的输入作为输入。 但是，如果此数组具有 `null` 值，则将调用备用 `UpdateCategory` 重载，这会发出不会修改 `Picture` 列的 `UPDATE` SQL 语句，从而使当前类别的当前图片保持不变。 因此，在 GridView `RowUpdating` 事件处理程序中，我们需要以编程方式引用 `PictureUpload` FileUpload 控件并确定是否已上传文件。 如果未上传一项，则*不*希望为 `picture` 参数指定值。 另一方面，如果在 `PictureUpload` FileUpload 控件中上传了文件，则需要确保它是 JPG 文件。 如果是，则可以通过 `picture` 参数将其二进制内容发送到 ObjectDataSource。

与步骤6中使用的代码一样，此处所需的很多代码已经存在于 DetailsView s `ItemInserting` 事件处理程序中。 因此，我已将公共功能重构为新方法 `ValidPictureUpload`，并将 `ItemInserting` 事件处理程序更新为使用此方法。

将以下代码添加到 GridView `RowUpdating` 事件处理程序的开头。 这一点很重要，因为如果上传了无效的图片文件，我们不希望将小册子保存到 web 服务器的文件系统，但在保存小册子文件的代码之前，这一点很重要。

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample11.cs)]

`ValidPictureUpload(FileUpload)` 方法采用 FileUpload 控件作为其唯一的输入参数，并检查上传的文件的扩展名，以确保上传的文件是 JPG;仅当上传图片文件时，才会调用此方法。 如果未上传任何文件，则不会设置 picture 参数，因此将使用其默认值 `null`。 如果上传了图片并且 `ValidPictureUpload` 返回 `true`，则会为 `picture` 参数分配已上传图像的二进制数据;如果该方法返回 `false`，则将取消更新工作流并退出事件处理程序。

从 DetailsView s `ItemInserting` 事件处理程序重构的 `ValidPictureUpload(FileUpload)` 方法代码如下：

[!code-csharp[Main](updating-and-deleting-existing-binary-data-cs/samples/sample12.cs)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>步骤8：将原始类别的图片替换为 JPGs

回忆一下，最初的八个类别图片是包装在 OLE 标头中的位图文件。 现在，我们已添加了编辑现有记录图片的功能，请花点时间将这些位图替换为 JPGs。 如果要继续使用当前类别的图片，可以通过执行以下步骤将其转换为 JPGs：

1. 将位图图像保存到硬盘驱动器。 访问浏览器中的 "`UpdatingAndDeleting.aspx`" 页，为前八个类别中的每一个，右键单击图像并选择保存图片。
2. 在所选的图像编辑器中打开图像。 例如，可以使用 Microsoft 画图。
3. 将位图另存为 JPG 图像。
4. 使用 JPG 文件通过编辑界面更新类别的图片。

编辑类别并上传 JPG 图像后，图像将不会在浏览器中呈现，因为 `DisplayCategoryPicture.aspx` 页面会从前8个类别的图片中去除前78个字节。 通过删除执行 OLE 标头去除的代码来解决此问题。 完成此操作后，`DisplayCategoryPicture.aspx``Page_Load` 事件处理程序应该只包含以下代码：

[!code-vb[Main](updating-and-deleting-existing-binary-data-cs/samples/sample13.vb)]

> [!NOTE]
> 插入和编辑接口的 `UpdatingAndDeleting.aspx` 页可以使用更多的工作。 DetailsView 和 GridView 中的 `CategoryName` 和 `Description` BoundFields 应转换为 Templatefield。 由于 `CategoryName` 不允许 `NULL` 值，因此应添加 RequiredFieldValidator。 "`Description`" 文本框可能会转换为多行文本框。 我将这些完成的润色留给您。

## <a name="summary"></a>摘要

本教程将介绍如何使用二进制数据。 在本教程和前三个教程中，我们了解了如何在文件系统中或直接在数据库中存储二进制数据。 用户通过从其硬盘中选择文件并将其上传到 web 服务器（可将其存储在文件系统上或插入到数据库中），向系统提供二进制数据。 ASP.NET 2.0 包含一个 FileUpload 控件，该控件可将此类接口提供为简单的拖放。 但是，如[上传文件](uploading-files-cs.md)教程中所述，FileUpload 控件仅适用于相对较小的文件上传，理想情况下不超过 mb。 我们还探讨了如何将上传的数据与基础数据模型相关联，以及如何从现有记录中编辑和删除二进制数据。

下一组教程将探讨各种缓存技术。 缓存提供了一种方法来改善应用程序的总体性能，方法是从开销较高的操作中提取结果，并将它们存储在可更快速访问的位置。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](including-a-file-upload-option-when-adding-a-new-record-cs.md)
> [下一页](uploading-files-vb.md)
