---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
title: 正在上载文件（VB） |Microsoft Docs
author: rick-anderson
description: 了解如何允许用户将二进制文件（如 Word 或 PDF 文档）上传到你的网站，并将其存储在服务器的文件系统中。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: f7c00fbd-652c-433d-8ed3-0e5168a4d4df
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0d57ef2f1e8132f19777a7d14e94611c68adcd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615446"
---
# <a name="uploading-files-vb"></a>上载文件 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_VB.exe)或[下载 PDF](uploading-files-vb/_static/datatutorial54vb1.pdf)

> 了解如何允许用户将二进制文件（如 Word 或 PDF 文档）上载到您的网站，这些文件可能存储在服务器的文件系统或数据库中。

## <a name="introduction"></a>简介

到目前为止，我们所检查的所有教程都专门处理文本数据。 但是，许多应用程序都有捕获文本和二进制数据的数据模型。 联机可追溯网站可能允许用户上传图片，使其与配置文件关联。 招聘网站可让用户以 Microsoft Word 或 PDF 文档的形式上传其简历。

使用二进制数据添加了一系列新的挑战。 我们必须确定如何将二进制数据存储在应用程序中。 必须更新用于插入新记录的接口，以允许用户从其计算机上传文件，并且必须采取额外的步骤来显示或提供一种方式来下载与记录关联的二进制数据。 在本教程中，接下来的三个教程将探讨如何应对这些挑战。 在这些教程结束时，我们将生成一个功能齐全的应用程序，它将图片和 PDF 手册与每个类别关联起来。 在本教程中，我们将介绍用于存储二进制数据的不同方法，并探索如何使用户能够从其计算机上传文件，并将其保存在 web 服务器的文件系统上。

> [!NOTE]
> 作为应用程序的数据模型的一部分的二进制数据有时[称为 "二进制](http://en.wikipedia.org/wiki/Binary_large_object)大型对象" 的缩写。 在这些教程中，我选择了使用术语二进制数据，但术语 BLOB 是同义词。

## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>步骤1：创建使用二进制数据网页

在开始探索与添加对二进制数据的支持相关的挑战之前，首先请花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程和接下来的三个页面中创建这些页面。 首先添加一个名为 `BinaryData`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`

![为二进制数据相关教程添加 ASP.NET 页](uploading-files-vb/_static/image1.gif)

**图 1**：为与二进制数据相关的教程添加 ASP.NET 页

与在其他文件夹中一样，`BinaryData` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](uploading-files-vb/_static/image2.gif)](uploading-files-vb/_static/image1.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](uploading-files-vb/_static/image2.png)）

最后，将这些页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在增强 GridView `<siteMapNode>`之后添加以下标记：

[!code-xml[Main](uploading-files-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧的菜单中包含用于处理二进制数据教程的项。

![站点映射现在包含用于处理二进制数据教程的条目](uploading-files-vb/_static/image3.gif)

**图 3**：站点地图现在包含用于处理二进制数据教程的条目

## <a name="step-2-deciding-where-to-store-the-binary-data"></a>步骤2：确定二进制数据的存储位置

与应用程序的数据模型相关联的二进制数据可以存储在以下两个位置之一：在 web 服务器的文件系统上，引用存储在数据库中的文件;或直接在数据库本身内（请参阅图4）。 每种方法都有其自己的一组优点和缺点，并提供更详细的讨论。

[![二进制数据可以存储在文件系统上，也可以直接存储在数据库中](uploading-files-vb/_static/image4.gif)](uploading-files-vb/_static/image3.png)

**图 4**：可在文件系统中或直接在数据库中存储二进制数据（[单击以查看完全大小的映像](uploading-files-vb/_static/image4.png)）

假设我们想要扩展 Northwind 数据库，以便将图片与每个产品关联起来。 一种选择是将这些图像文件存储在 web 服务器的文件系统上，并在 `Products` 表中记录该路径。 使用此方法时，我们将 `ImagePath` 列添加到 `varchar(200)`类型的 `Products` 表中。 当用户上传 Chai 的图片时，该图片可能存储在 web 服务器的文件系统上 `~/Images/Tea.jpg`，其中 `~` 表示应用程序的物理路径。 也就是说，如果网站以 `C:\Websites\Northwind\`的物理路径为根，则 `~/Images/Tea.jpg` 等效于 `C:\Websites\Northwind\Images\Tea.jpg`。 上传图像文件后，我们将更新 `Products` 表中的 Chai 记录，使其 `ImagePath` 列引用新图像的路径。 如果我们决定将所有产品映像都放置在应用程序的 `Images` 文件夹中，则可以使用 `~/Images/Tea.jpg` 或仅 `Tea.jpg`。

将二进制数据存储在文件系统上的主要优点是：

- **简化实现**，因为我们很快就会看到，存储和检索直接存储在数据库中的二进制数据比通过文件系统处理数据更多。 此外，若要让用户查看或下载二进制数据，必须向其提供指向该数据的 URL。 如果数据驻留在 web 服务器的文件系统上，则 URL 非常简单。 但是，如果数据存储在数据库中，则需要创建一个网页，该网页将从数据库中检索并返回数据。
- **更大的二进制数据访问权限**，其他服务或应用程序可能需要对这些数据进行访问，而不能从数据库中提取数据。 例如，与每个产品关联的图像可能还需要通过[FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)供用户使用，在这种情况下，我们需要在文件系统上存储二进制数据。
- **性能**如果将二进制数据存储在文件系统中，则数据库服务器和 web 服务器之间的需求和网络拥塞将小于二进制数据直接存储在数据库中。

将二进制数据存储在文件系统上的主要缺点是它将数据与数据库分离。 如果从 `Products` 表中删除记录，则不会自动删除 web 服务器的文件系统上的相关文件。 我们必须编写额外的代码来删除该文件，否则，文件系统将会变得杂乱，并使用未使用的孤立文件。 而且，在备份数据库时，还必须确保在文件系统上备份关联的二进制数据。 将数据库移到另一个站点或服务器上会带来类似的挑战。

或者，可以通过创建 `varbinary`类型的列，将二进制数据直接存储在 Microsoft SQL Server 2005 数据库中。 与其他可变长度数据类型一样，可以指定此列中可包含的二进制数据的最大长度。 例如，若要保留最多5000个字节，请使用 `varbinary(5000)`;`varbinary(MAX)` 允许的最大存储大小为 2 GB。

直接在数据库中存储二进制数据的主要优点是二进制数据和数据库记录之间的紧密耦合。 这极大地简化了数据库管理任务，例如备份或将数据库移动到不同的站点或服务器。 此外，删除记录将自动删除相应的二进制数据。 将二进制数据存储在数据库中也有更多微妙的好处。 有关更深入的讨论，请参阅[使用 ASP.NET 2.0 将二进制文件直接存储在数据库中](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx)。

> [!NOTE]
> 在 Microsoft SQL Server 2000 及更早版本中，`varbinary` 数据类型的最大限制为8000个字节。 若要存储最多 2 GB 的二进制数据，需改为使用[`image` 数据类型](https://msdn.microsoft.com/library/ms187993.aspx)。 但在 SQL Server 2005 中添加 `MAX` 时，`image` 数据类型已弃用。 它仍支持向后兼容，但 Microsoft 已公布 SQL Server 的未来版本中将删除 `image` 数据类型。

如果使用的是较旧的数据模型，可能会看到 `image` 的数据类型。 Northwind 数据库 `Categories` 表具有一个 `Picture` 列，可用于存储该类别的图像文件的二进制数据。 由于 Northwind 数据库在 Microsoft Access 和早期版本的 SQL Server 中具有其根，因此此列的类型为 `image`。

对于本教程和接下来的三个方法，我们将使用这两种方法。 `Categories` 表已有一个 `Picture` 列，用于存储类别的图像的二进制内容。 接下来，我们将添加一列 `BrochurePath`，用于在 web 服务器文件系统上存储 PDF 路径，该路径可用于提供对类别的打印质量精美概述。

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>步骤3：将`BrochurePath`列添加到`Categories`表

目前，"类别" 表只有四列： `CategoryID`、`CategoryName`、`Description`和 `Picture`。 除了这些字段之外，我们还需要添加一个新的，它将指向类别的手册（如果存在）。 若要添加此列，请访问服务器资源管理器，向下钻取到表中，右键单击 `Categories` 表，然后选择 "打开表定义" （参见图5）。 如果看不到 "服务器资源管理器"，请从 "视图" 菜单中选择 "服务器资源管理器" 选项，或按 Ctrl + Alt + S 打开它。

将新 `varchar(200)` 列添加到名为 `BrochurePath` 的 `Categories` 表中，并允许 `NULL`，并单击 "保存" 图标（或按 Ctrl + S）。

[![将 BrochurePath 列添加到 "类别" 表](uploading-files-vb/_static/image5.gif)](uploading-files-vb/_static/image5.png)

**图 5**：将 `BrochurePath` 列添加到 `Categories` 表（[单击查看完全大小的图像](uploading-files-vb/_static/image6.png)）

## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>步骤4：将体系结构更新为使用`Picture`和`BrochurePath`列

数据访问层（DAL）中的 `CategoriesDataTable` 当前定义了四个 `DataColumn`： `CategoryID`、`CategoryName`、`Description`和 `NumberOfProducts`。 如果我们最初在[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中设计了此 DataTable，则 `CategoriesDataTable` 仅包含前三列;[使用带有详细信息 DataList 教程的主记录的项目符号列表在主/详细信息](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)中添加了 `NumberOfProducts` 列。

如*创建数据访问层*中所述，类型化数据集中的数据表构成了业务对象。 Tableadapter 负责与数据库进行通信，并在查询结果中填充业务对象。 `CategoriesDataTable` 由 `CategoriesTableAdapter`填充，其中包含三种数据检索方法：

- `GetCategories()` 执行 TableAdapter s 主查询，并返回 `Categories` 表中所有记录的 `CategoryID`、`CategoryName`和 `Description` 字段。 主查询由自动生成的 `Insert` 和 `Update` 方法使用。
- `GetCategoryByCategoryID(categoryID)` 返回类别的 `CategoryID`、`CategoryName`和 `Description` 字段，其 `CategoryID` 等于类别*id*。
- `GetCategoriesAndNumberOfProducts()`-返回 `Categories` 表中所有记录的 `CategoryID`、`CategoryName`和 `Description` 字段。 还使用子查询返回与每个类别关联的产品数。

请注意，这些查询都不会返回 `Categories` 表 `Picture` 或 `BrochurePath` 列;`CategoriesDataTable` 也不为这些字段提供 `DataColumn`。 为了处理图片并 `BrochurePath` 属性，我们需要首先将其添加到 `CategoriesDataTable`，然后更新 `CategoriesTableAdapter` 类以返回这些列。

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>添加`Picture`和`BrochurePath``DataColumn`

首先，将这两列添加到 `CategoriesDataTable`。 右键单击 `CategoriesDataTable` 的标题，从上下文菜单中选择 "添加"，然后选择 "列" 选项。 这会在名为 `Column1`的 DataTable 中创建新 `DataColumn`。 将此列重命名为 `Picture`。 在属性窗口中，将 `DataColumn` s `DataType` 属性设置为 `System.Byte[]` （这不是下拉列表中的选项; 您需要在下拉列表中键入）。

[![创建一个名为 Picture 的 DataColumn，其数据类型为 system.string []](uploading-files-vb/_static/image6.gif)](uploading-files-vb/_static/image7.png)

**图 6**：创建一个名为 `Picture` 的 `DataColumn`，其 `DataType` 为 `System.Byte[]` （[单击查看完全大小的图像](uploading-files-vb/_static/image8.png)）

将另一 `DataColumn` 添加到 DataTable，并使用默认的 `DataType` 值（`System.String`）将其命名为 `BrochurePath`。

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>从 TableAdapter 返回`Picture`和`BrochurePath`值

将这两个 `DataColumn` 添加到 `CategoriesDataTable`中后，就可以更新 `CategoriesTableAdapter`了。 我们可以在主 TableAdapter 查询中同时返回这两个列值，但这会在每次调用 `GetCategories()` 方法时返回二进制数据。 现在，让我们更新主 TableAdapter 查询，使其返回 `BrochurePath` 并创建一个返回特定类别 `Picture` 列的其他数据检索方法。

若要更新主 TableAdapter 查询，请右键单击 `CategoriesTableAdapter` 的标头，然后从上下文菜单中选择 "配置" 选项。 这会显示 "表适配器配置向导"，过去的几个教程中已介绍了这种情况。 更新查询以恢复 `BrochurePath`，然后单击 "完成"。

[![更新 SELECT 语句中的列列表，同时返回 BrochurePath](uploading-files-vb/_static/image7.gif)](uploading-files-vb/_static/image9.png)

**图 7**：更新 `SELECT` 语句中的列列表，同时返回 `BrochurePath` （[单击查看完全大小的图像](uploading-files-vb/_static/image10.png)）

对 TableAdapter 使用即席 SQL 语句时，更新主查询中的列列表将更新 TableAdapter 中所有 `SELECT` 查询方法的列列表。 这意味着 `GetCategoryByCategoryID(categoryID)` 方法已更新为返回 `BrochurePath` 列，这可能是我们预期的。 不过，它还更新了 `GetCategoriesAndNumberOfProducts()` 方法中的列列表，并删除了返回每个类别的产品数量的子查询！ 因此，我们需要 `SELECT` 查询更新此方法。 右键单击 `GetCategoriesAndNumberOfProducts()` 方法，然后选择 "配置"，并将 `SELECT` 查询恢复为其原始值：

[!code-sql[Main](uploading-files-vb/samples/sample2.sql)]

接下来，创建一个新的 TableAdapter 方法，该方法返回 `Picture` 列值的特定类别。 右键单击 `CategoriesTableAdapter` 的标头，然后选择 "添加查询" 选项以启动 "TableAdapter 查询配置向导"。 如果要使用即席 SQL 语句、新存储过程或现有存储过程查询数据，则此向导的第一步会询问我们。 选择 "使用 SQL 语句"，然后单击 "下一步"。 由于我们将返回一行，因此选择第二步中的 "选择行" 选项。

[![选择 "使用 SQL 语句" 选项](uploading-files-vb/_static/image8.gif)](uploading-files-vb/_static/image11.png)

**图 8**：选择 "使用 SQL 语句" 选项（[单击以查看完全大小的映像](uploading-files-vb/_static/image12.png)）

[![，因为查询将从 "类别" 表返回一条记录，请选择 "选择"，这将返回行](uploading-files-vb/_static/image9.gif)](uploading-files-vb/_static/image13.png)

**图 9**：由于查询将从 "类别" 表返回一条记录，请选择 "选择"，这将返回行（[单击查看完全大小的图像](uploading-files-vb/_static/image14.png)）

在第三步中，输入以下 SQL 查询，然后单击 "下一步"：

[!code-sql[Main](uploading-files-vb/samples/sample3.sql)]

最后一步是选择新方法的名称。 使用 `FillCategoryWithBinaryDataByCategoryID` 和 `GetCategoryWithBinaryDataByCategoryID` 填充 DataTable 并分别返回 DataTable 模式。 单击“完成”按钮以完成向导。

[![选择 TableAdapter s 方法的名称](uploading-files-vb/_static/image10.gif)](uploading-files-vb/_static/image15.png)

**图 10**：选择 TableAdapter s 方法的名称（[单击以查看完全大小的映像](uploading-files-vb/_static/image16.png)）

> [!NOTE]
> 完成表适配器查询配置向导后，您可能会看到一个对话框，通知您新的命令文本返回的数据与主查询的架构不同。 简而言之，向导注意到，TableAdapter s 主查询 `GetCategories()` 返回的架构与我们刚刚创建的架构不同。 但这正是我们所希望的，因此可以忽略此消息。

另外，请记住，如果你使用的是即席 SQL 语句，并使用向导在以后的某个时间点更改 TableAdapter s 主查询，它会将 `GetCategoryWithBinaryDataByCategoryID` 方法 s `SELECT` 语句的列列表修改为仅包括主查询中的那些列（也就是说，它将从查询中删除 `Picture` 列）。 您必须手动更新列列表才能返回 `Picture` 列，这类似于在此步骤前面的 `GetCategoriesAndNumberOfProducts()` 方法所做的操作。

将两个 `DataColumn` s 添加到 `CategoriesDataTable` 并将 `GetCategoryWithBinaryDataByCategoryID` 方法添加到 `CategoriesTableAdapter`后，类型化数据集设计器中的这些类应类似于图11中的屏幕截图。

![数据集设计器包含新的列和方法](uploading-files-vb/_static/image11.gif)

**图 11**：数据集设计器包含新的列和方法

## <a name="updating-the-business-logic-layer-bll"></a>更新业务逻辑层（BLL）

当 DAL 经过更新后，剩下的就是增加业务逻辑层（BLL）以包括新的 `CategoriesTableAdapter` 方法的方法。 将以下方法添加到 `CategoriesBLL` 类：

[!code-vb[Main](uploading-files-vb/samples/sample4.vb)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>步骤5：将文件从客户端上传到 Web 服务器

收集二进制数据时，此数据通常由最终用户提供。 若要捕获此信息，用户需要能够将文件从其计算机上传到 web 服务器。 上传的数据需要与数据模型集成，这可能意味着将文件保存到 web 服务器的文件系统，并将路径添加到数据库中，或将二进制内容直接写入数据库。 在此步骤中，我们将介绍如何允许用户将文件从其计算机上传到服务器。 在下一教程中，我们将重点介绍如何将上传的文件与数据模型集成。

ASP.NET 2.0 s new [FileUpload Web 控件](https://msdn.microsoft.com/library/ms227677(VS.80).aspx)提供一种机制，让用户将文件从其计算机发送到 Web 服务器。 FileUpload 控件呈现为 `<input>` 元素，其 `type` 属性设置为 "文件"，浏览器会将其显示为具有 "浏览" 按钮的文本框。 单击 "浏览" 按钮将弹出一个对话框，用户可以从中选择文件。 当窗体回发时，所选文件的内容与回发一起发送。 在服务器端，有关上传的文件的信息可通过 FileUpload 控件的属性进行访问。

若要演示如何上传文件，请打开 `BinaryData` 文件夹中的 `FileUpload.aspx` 页面，将 FileUpload 控件从工具箱拖到设计器上，并将 control s `ID` 属性设置为 `UploadTest`。 接下来，添加一个按钮 Web 控件，设置其 `ID`，并 `Text` 属性分别 `UploadButton` 和上传选定的文件。 最后，将 "标签" Web 控件置于按钮的下方，清除其 `Text` 属性，并将其 `ID` 属性设置为 "`UploadDetails`"。

[![将 FileUpload 控件添加到 ASP.NET 页](uploading-files-vb/_static/image12.gif)](uploading-files-vb/_static/image17.png)

**图 12**：向 "ASP.NET" 页添加 FileUpload 控件（[单击以查看完全大小的图像](uploading-files-vb/_static/image18.png)）

图13显示了通过浏览器查看的此页。 请注意，单击 "浏览" 按钮将打开 "文件选择" 对话框，允许用户从其计算机中选择文件。 选择文件后，单击 "上传选定的文件" 按钮将导致回发，以将所选文件的二进制内容发送到 web 服务器。

[![用户可以选择要从其计算机上传到服务器的文件](uploading-files-vb/_static/image13.gif)](uploading-files-vb/_static/image19.png)

**图 13**：用户可以选择要从其计算机上传到服务器的文件（[单击以查看完全大小的映像](uploading-files-vb/_static/image20.png)）

在回发时，可以将上传的文件保存到文件系统中，也可以直接通过流使用它的二进制数据。 在此示例中，让我们创建一个 `~/Brochures` 文件夹，然后将上传的文件保存到其中。 首先将 `Brochures` 文件夹作为根目录的子文件夹添加到站点。 接下来，为 `UploadButton` 的 `Click` 事件创建事件处理程序并添加以下代码：

[!code-vb[Main](uploading-files-vb/samples/sample5.vb)]

FileUpload 控件提供各种属性用于处理已上载的数据。 例如， [`HasFile` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx)指示用户是否已上传文件，而[`FileBytes` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx)则以字节数组的形式提供对上传的二进制数据的访问。 `Click` 事件处理程序首先确保文件已上传。 如果文件已上传，则标签将显示上传的文件的名称、文件大小（以字节为单位）以及内容类型。

> [!NOTE]
> 若要确保用户上传文件，您可以检查 `HasFile` 属性，如果 `False`，则显示警告，否则您可以改为使用[RequiredFieldValidator 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx)。

FileUpload `SaveAs(filePath)` 将上传的文件保存到指定的*filePath*。 *filePath*必须是*物理路径*（`C:\Websites\Brochures\SomeFile.pdf`），而不是*虚拟* *路径*（`/Brochures/SomeFile.pdf`）。 [`Server.MapPath(virtPath)` 方法](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx)获取虚拟路径，并返回其相应的物理路径。 此处 `~/Brochures/fileName`虚拟路径，其中*fileName*是上传的文件的名称。 有关虚拟路径和物理路径以及使用 `Server.MapPath`的详细信息，请参阅[使用 Server. MapPath](http://www.4guysfromrolla.com/webtech/121799-1.shtml) 。

完成 `Click` 事件处理程序后，请花点时间在浏览器中测试页面。 单击 "浏览" 按钮并从硬盘中选择文件，然后单击 "上传选定的文件" 按钮。 回发会将所选文件的内容发送到 web 服务器，该服务器随后会在将文件保存到 `~/Brochures` 文件夹之前，显示有关该文件的信息。 上传文件后，返回到 Visual Studio，然后单击 "解决方案资源管理器中的" 刷新 "按钮。 应会在 ~/Brochures 文件夹中看到刚上传的文件！

[![已将文件 EvolutionValley 上传到 Web 服务器](uploading-files-vb/_static/image14.gif)](uploading-files-vb/_static/image21.png)

**图 14**：已将文件 `EvolutionValley.jpg` 上传到 Web 服务器（[单击查看完全大小的图像](uploading-files-vb/_static/image22.png)）

![EvolutionValley 已保存到 ~/Brochures 文件夹](uploading-files-vb/_static/image15.gif)

**图 15**： `EvolutionValley.jpg` 已保存到 `~/Brochures` 文件夹中

## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>将上传的文件保存到文件系统的微妙之处

将文件上传到 web 服务器的文件系统时，必须解决几个微妙之处。 首先，我们有安全问题。 若要将文件保存到文件系统，用于执行 ASP.NET 页面的安全上下文必须具有写入权限。 ASP.NET 开发 Web 服务器在当前用户帐户的上下文中运行。 如果使用 Microsoft s Internet Information Services （IIS）作为 web 服务器，则安全上下文取决于 IIS 的版本及其配置。

将文件保存到文件系统的另一项挑战就是对文件进行命名。 目前，我们的页面使用与客户端计算机上的文件相同的名称将所有上传的文件保存到 `~/Brochures` 目录。 如果用户 A 上传 `Brochure.pdf`名称的小册子，则该文件将保存为 `~/Brochure/Brochure.pdf`。 但如果以后用户 B 上传的不同小册子文件具有相同的文件名（`Brochure.pdf`），该怎么办？ 使用现在的代码，用户 A 将在用户 B 上传时覆盖 s 文件。

有多种方法可以解决文件名冲突。 一种选择是禁止上传文件（如果已存在同名的文件）。 使用此方法时，当用户 B 尝试上传名为 `Brochure.pdf`的文件时，系统不会保存其文件，而是显示一条消息，告知用户 B 对文件进行重命名，然后重试。 另一种方法是使用唯一的文件名保存文件，这可能是[全局唯一标识符（GUID）](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) ，也可能是相应数据库记录的主键列中的值（假设上载与数据模型中的特定行相关联）。 在下一教程中，我们将更详细地探讨这些选项。

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>大量二进制数据所涉及的挑战

这些教程假定捕获的二进制数据大小适中。 使用非常大的二进制数据文件（几兆字节或更大）会带来新的挑战，超出了这些教程的范围。 例如，默认情况下，ASP.NET 将拒绝超过 4 MB 的上传，尽管可通过 `Web.config`中的[`<httpRuntime>` 元素](https://msdn.microsoft.com/library/e1f13641.aspx)进行配置。 IIS 还会施加自己的文件上传大小限制。 有关详细信息，请参阅[IIS 上传文件大小](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html)。 而且，上载大文件所需的时间可能会超过默认的110秒，ASP.NET 将等待请求。 在处理大型文件时，也会出现内存和性能问题。

对于大型文件上传，FileUpload 控件不切实际。 当文件的内容被发送到服务器时，最终用户必须耐心等待，无需确认其上传正在进行。 在处理可在几秒钟内上载的小型文件时，这并不是问题，但在处理较大的文件可能需要几分钟时间上传时可能会遇到问题。 有各种第三方文件上传控件更适合处理大的上载，其中的许多供应商提供了进度指示器和 ActiveX 上传管理器，它们提供了更加精美的用户体验。

如果你的应用程序需要处理大文件，则需要仔细调查这些挑战，并根据特定需求查找合适的解决方案。

## <a name="summary"></a>总结

构建需要捕获二进制数据的应用程序带来了许多挑战。 在本教程中，我们探讨了前两个步骤：决定存储二进制数据的位置，并允许用户通过网页上传二进制内容。 在接下来的三个教程中，我们将了解如何将已上传的数据与数据库中的记录相关联，以及如何在其文本数据字段旁显示二进制数据。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用大值数据类型](https://msdn.microsoft.com/library/ms178158.aspx)
- [FileUpload 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 FileUpload 服务器控件](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [文件上传的深色面](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Teresa Murphy 和 Bernadette Leigh。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](updating-and-deleting-existing-binary-data-cs.md)
> [下一页](displaying-binary-data-in-the-data-web-controls-vb.md)
