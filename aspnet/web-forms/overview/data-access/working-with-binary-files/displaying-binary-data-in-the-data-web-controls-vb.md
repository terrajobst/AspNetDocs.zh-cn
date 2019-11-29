---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: 显示数据 Web 控件中的二进制数据（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将介绍用于在网页上显示二进制数据的选项，包括图像文件的显示和 "下载" 链接的设置 。
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 27c901af092aa990f557750dc5d2c42ba2644c02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640688"
---
# <a name="displaying-binary-data-in-the-data-web-controls-vb"></a>显示数据 Web 控件中的二进制数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe)或[下载 PDF](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> 在本教程中，我们将介绍用于在网页上显示二进制数据的选项，包括图像文件的显示以及 PDF 文件的 "下载" 链接。

## <a name="introduction"></a>简介

在前面的教程中，我们探讨了两种方法，用于将二进制数据与应用程序的基础数据模型相关联，并使用 FileUpload 控件将文件从浏览器上传到 web 服务器的文件系统。 我们尚未看到如何将上传的二进制数据与数据模型关联。 也就是说，将文件上传并保存到文件系统后，必须将文件的路径存储在相应的数据库记录中。 如果数据直接存储在数据库中，则上传的二进制数据无需保存到文件系统，但必须注入到数据库中。

但在查看将数据与数据模型关联之前，让我们先了解如何向最终用户提供二进制数据。 呈现文本数据非常简单，但应如何呈现二进制数据？ 当然，它取决于二进制数据的类型。 对于图像，我们可能希望显示图像;对于 Pdf、Microsoft Word 文档、ZIP 文件和其他类型的二进制数据，提供下载链接可能更合适。

在本教程中，我们将介绍如何使用数据 Web 控件（如 GridView 和 DetailsView）来向其关联的文本数据显示二进制数据。 在下一教程中，我们将重点介绍如何将上传的文件与数据库相关联。

## <a name="step-1-providingbrochurepathvalues"></a>步骤1：提供`BrochurePath`值

`Categories` 表中的 `Picture` 列已经包含不同类别图像的二进制数据。 具体而言，每条记录的 `Picture` 列都包含有纹理、低质量、16色位图图像的二进制内容。 每个类别的图像宽度为172像素，120像素高，使用约 11 KB。 另外，`Picture` 列中的二进制内容包括78字节的[OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding)标头，在显示图像之前必须将其去除。 存在此标头信息，因为 Northwind 数据库在 Microsoft Access 中具有其根。 在 Access 中，二进制数据使用 OLE Object 数据类型进行存储，该数据类型在此标头 get-date。 现在，我们将了解如何从这些低质量图像中去除标头以显示图片。 在将来的教程中，我们将构建一个用于更新类别 `Picture` 列的接口，并将使用 OLE 标头的位图图像替换为不必要的 OLE 标头的等效 JPG 图像。

在前面的教程中，我们介绍了如何使用 FileUpload 控件。 因此，您可以继续将小册子文件添加到 web 服务器的文件系统中。 但这样做不会更新 `Categories` 表中的 `BrochurePath` 列。 在下一教程中，我们将了解如何实现此目的，但现在我们需要为此列手动提供值。

在本教程中，你将在 "`~/Brochures`" 文件夹中找到7个 PDF 小册子文件，其中每个类别都有 "海鲜" 除外。 我有意省略了添加海鲜手册，旨在说明如何处理并非所有记录都具有关联的二进制数据的情况。 若要用这些值更新 `Categories` 表，请在服务器资源管理器中右键单击 `Categories` 节点，然后选择 "显示表数据"。 然后，为包含小册子的每个类别的小册子文件输入虚拟路径，如图1所示。 由于 "海鲜" 类别没有手册，请将其 `BrochurePath` 列 "值保留为 `NULL`。

[![手动输入 "类别" 表的 BrochurePath 列的值](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**图 1**：手动输入 `Categories` 表 `BrochurePath` 列的值（[单击以查看完全大小的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png)）

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>步骤2：为 GridView 中的手册提供下载链接

使用为 `Categories` 表提供的 `BrochurePath` 值，我们可以创建一个 GridView，其中列出了每个类别以及用于下载类别手册的链接。 在步骤4中，我们将扩展此 GridView，还会显示类别的图像。

首先，将 GridView 从工具箱拖动到 `BinaryData` 文件夹中 `DisplayOrDownloadData.aspx` 页面的设计器上。 将 GridView `ID` 设置为 `Categories` 并通过 GridView s 智能标记，选择将其绑定到新的数据源。 具体而言，将其绑定到名为 `CategoriesDataSource` 的 ObjectDataSource，该 ObjectDataSource 使用 `CategoriesBLL` 对象 s `GetCategories()` 方法检索数据。

[![创建一个名为 CategoriesDataSource 的新 ObjectDataSource](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**图 2**：创建名为 `CategoriesDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png)）

[![将 ObjectDataSource 配置为使用 CategoriesBLL 类](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**图 3**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类（[单击以查看完全大小的映像](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png)）

[![使用 GetCategories （）方法检索类别列表](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**图 4**：使用 `GetCategories()` 方法检索类别列表（[单击以查看完全大小的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png)）

完成 "配置数据源" 向导后，Visual Studio 会自动将 BoundField 添加到 `CategoryID`的 `Categories` GridView，`CategoryName`，`Description`，`NumberOfProducts`和 `BrochurePath` `DataColumn`。 继续并删除 `NumberOfProducts` BoundField，因为 `GetCategories()` 方法查询不检索此信息。 同时删除 `CategoryID` BoundField，并分别将 `CategoryName` 和 `BrochurePath` BoundFields `HeaderText` 属性分别重命名为 "类别" 和 "小册子"。 进行这些更改后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

通过浏览器查看此页（参见图5）。 列出了8个类别中的每一个。 具有 `BrochurePath` 值的七个类别在各自的 BoundField 中显示 `BrochurePath` 值。 对于其 `BrochurePath`具有 `NULL` 值的海鲜，将显示空单元。

[![列出了每个类别的 Name、Description 和 BrochurePath 值](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**图 5**：列出了每个类别的 "名称"、"说明" 和 "`BrochurePath` 值（[单击以查看完全大小的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png)）

我们想要创建到小册子的链接，而不是显示 `BrochurePath` 列的文本。 为此，请删除 `BrochurePath` BoundField，并将其替换为 HyperLinkField。 将新的 HyperLinkField s `HeaderText` 属性设置为小册子，将其 `Text` 属性设置为 "查看手册"，并将其 `DataNavigateUrlFields` 属性设置为 "`BrochurePath`"。

![添加 BrochurePath 的 HyperLinkField](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**图 6**：为 `BrochurePath` 添加 HyperLinkField

这会将一个链接列添加到 GridView，如图7所示。 单击 "查看小册子" 链接将直接在浏览器中显示 PDF，或提示用户下载文件，具体取决于是否安装了 PDF 读取器和浏览器设置。

[可以通过单击 "查看小册子" 链接 ![查看类别](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**图 7**：可以通过单击 "查看小册子" 链接来查看类别的小册子（[单击以查看完全大小的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png)）

[显示 "![类别" 手册 PDF](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**图 8**：显示了类别的手册 PDF （[单击以查看完全大小的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png)）

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>隐藏没有手册的类别的查看小册子文本

如图7所示，`BrochurePath` HyperLinkField 将显示所有记录的 `Text` 属性值（"查看小册子"），而不管是否有 `BrochurePath`的非`NULL` 值。 当然，如果 `NULL``BrochurePath`，则链接将显示为 "仅文本"，与 "海鲜" 类别相同（请参阅图7）。 如果没有显示文本视图小册子，则在没有 `BrochurePath` 值的情况下，不显示某些替代文本，如没有可用的小册子。

为了提供此行为，我们需要使用 TemplateField，其内容是通过调用页面方法生成的，该方法基于 `BrochurePath` 值发出相应的输出。 首先，我们将[使用 GridView 控件](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)教程中的 templatefield 来探索这种格式设置技术。

选择 `BrochurePath` HyperLinkField，然后单击 "编辑列" 对话框中的 "将此字段转换为 TemplateField" 链接，将 HyperLinkField 转换为 TemplateField。

![将 HyperLinkField 转换为 TemplateField](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**图 9**：将 HyperLinkField 转换为 TemplateField

这将创建一个具有 `ItemTemplate` 的 TemplateField，其中包含一个 `NavigateUrl` 属性绑定到 `BrochurePath` 值的超链接 Web 控件。 将此标记替换为对方法的调用 `GenerateBrochureLink`，并传入 `BrochurePath`的值：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

接下来，在名为 `GenerateBrochureLink` 的 ASP.NET 页 s 代码隐藏类中创建一个 `Protected` 方法，该方法返回 `String`，并接受 `Object` 作为输入参数。

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

此方法确定传入的 `Object` 值是否为数据库 `NULL` 如果是，则返回一条消息，指示该类别缺少一个手册。 否则，如果存在 `BrochurePath` 值，则它显示在超链接中。 请注意，如果存在 `BrochurePath` 值，则将它传递到[`ResolveUrl(url)` 方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)中。 此方法解析传入的*url*，并将 `~` 字符替换为适当的虚拟路径。 例如，如果应用程序的根 `/Tutorial55`，`ResolveUrl("~/Brochures/Meats.pdf")` 将返回 `/Tutorial55/Brochures/Meat.pdf`。

图10显示了应用这些更改后的页面。 请注意，"海鲜" 类别的 "`BrochurePath`" 字段现在显示文本 "无可用的内容"。

[![没有手册的这些类别没有可用的文本](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**图 10**：没有手册的这些类别显示没有小册子的文本（[单击查看完全尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png)）

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>步骤3：添加网页以显示类别的图片

当用户访问 ASP.NET 页面时，他们将收到 ASP.NET 页的 HTML。 收到的 HTML 只是文本，不包含任何二进制数据。 任何附加的二进制数据（如图像、声音文件、Macromedia Flash 应用程序、嵌入的 Windows Media Player 视频等）都作为独立的资源存在于 web 服务器上。 HTML 包含对这些文件的引用，但不包括文件的实际内容。

例如，在 HTML 中，`<img>` 元素用于引用图片，`src` 属性指向图像文件，如下所示：

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

当浏览器收到此 HTML 时，它会向 web 服务器发出另一个请求，以检索图像文件的二进制内容，然后在浏览器中显示该文件。 相同的概念也适用于任何二进制数据。 在步骤2中，不会将小册子作为页的 HTML 标记的一部分发送到浏览器。 所呈现的 HTML 提供的超链接，单击该超链接后，浏览器将直接请求 PDF 文档。

若要显示或允许用户下载驻留在数据库中的二进制数据，我们需要创建一个单独的网页来返回数据。 对于我们的应用程序，只有一个二进制数据字段直接存储在数据库中类别的图片中。 因此，我们需要一个页面，该页面在调用时返回特定类别的图像数据。

将新的 "ASP.NET" 页添加到名为 `DisplayCategoryPicture.aspx`的 `BinaryData` 文件夹。 执行此操作时，请取消选中 "选择母版页" 复选框。 此页需要 querystring 中的 `CategoryID` 值，并返回该类别 `Picture` 列的二进制数据。 由于此页面返回二进制数据而不是其他任何内容，因此在 HTML 部分中不需要任何标记。 因此，请单击左下角的 "源" 选项卡，然后删除除 `<%@ Page %>` 指令之外的所有页标记。 也就是说，`DisplayCategoryPicture.aspx` 的声明性标记应该包含一行：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

如果在 `<%@ Page %>` 指令中看到 `MasterPageFile` 属性，请将其删除。

在页的代码隐藏类中，将以下代码添加到 `Page_Load` 事件处理程序：

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

此代码首先将 `CategoryID` querystring 值读入名为 `categoryID`的变量中。 接下来，通过调用 `CategoriesBLL` 类 `GetCategoryWithBinaryDataByCategoryID(categoryID)` 方法检索图片数据。 此数据通过使用 `Response.BinaryWrite(data)` 方法返回到客户端，但在调用此之前，必须删除 `Picture` 的列值 s OLE 标头。 这是通过创建一个名为 `strippedImageData` 的 `Byte` 数组来完成的，该数组78包含的字符数要小于 `Picture` 列中的字符。 [`Array.Copy` 方法](https://msdn.microsoft.com/library/z50k9bft.aspx)用于将数据从位置78开始复制到 `strippedImageData`的 `category.Picture`。

`Response.ContentType` 属性指定要返回的内容的[MIME 类型](http://en.wikipedia.org/wiki/MIME)，以便浏览器知道如何呈现内容。 由于 `Categories` 表 s `Picture` 列是位图图像，此处使用位图 MIME 类型（image/bmp）。 如果省略 MIME 类型，则大多数浏览器仍然会正确显示图像，因为它们可以根据图像文件的二进制数据的内容来推断类型。 但是，尽可能包含 MIME 类型是明智的。 有关[MIME 媒体类型](http://www.iana.org/assignments/media-types/)的完整列表，请参阅[Internet 编号分配机构的网站](http://www.iana.org/)。

创建此页面后，可以通过访问 `DisplayCategoryPicture.aspx?CategoryID=categoryID`查看特定类别的图片。 图11显示了饮料类别的图片，可以从 `DisplayCategoryPicture.aspx?CategoryID=1`进行查看。

[显示 "饮料" 类别的图片 ![](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**图 11**：显示饮料类别的图片（[单击以查看完全尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png)）

如果在访问 `DisplayCategoryPicture.aspx?CategoryID=categoryID`时，你将收到一个异常，该异常读取无法将类型为 "system.string" 的对象转换为类型 "system.string []"，这可能会导致这种情况。 首先，`Categories` 表 s `Picture` 列允许 `NULL` 值。 但 `DisplayCategoryPicture.aspx` 页假定存在一个非`NULL` 值。 如果 `CategoriesDataTable` 具有 `NULL` 值，则无法直接访问该的 `Picture` 属性。 如果确实要为 `Picture` 列允许 `NULL` 值，则需要包含以下条件：

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

上面的代码假定在 `Images` 文件夹中有一个名为 `NoPictureAvailable.gif` 的图像文件，需要在没有图片的情况下为这些类别显示。

如果 `GetCategoryWithBinaryDataByCategoryID` 方法的 `CategoriesTableAdapter` `SELECT` 语句已恢复到主查询的列列表，则也可能会导致此异常，如果您使用的是即席 SQL 语句，并为 TableAdapter s 主查询重新运行向导，则可能会发生这种情况。 检查以确保 `GetCategoryWithBinaryDataByCategoryID` 方法 s `SELECT` 语句仍包含 `Picture` 列。

> [!NOTE]
> 每次访问 `DisplayCategoryPicture.aspx` 时，都将访问数据库并返回指定的类别的图片数据。 如果类别的图片自从用户最后一次查看后没有发生更改，则会浪费精力。 幸运的是，HTTP 允许*条件性获取*。 使用条件 GET 时，发出 HTTP 请求的客户端将发送[`If-Modified-Since` http 标头，该标头](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)提供客户端上次从 web 服务器检索该资源的日期和时间。 如果自指定日期起，内容未更改，则 web 服务器可能会使用[未修改的状态代码（304）](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)进行响应，并且放弃将回发请求的资源 s 内容。 简而言之，此方法使 web 服务器不需要在客户端上次访问资源后对其发送回内容。

但是，若要实现此行为，要求您将 `PictureLastModified` 列添加到 `Categories` 表中，以便在上一次更新 `Picture` 列时进行捕获，以及检查 `If-Modified-Since` 标头的代码。 有关 `If-Modified-Since` 标头和条件获取工作流的详细信息，请参阅[RSS 黑客的 Http 条件 get](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) ，并[深入了解如何在 ASP.NET 页中执行 http 请求](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)。

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>步骤4：在 GridView 中显示类别图片

现在，我们有了一个显示特定类别图片的网页，可以使用[图像 web 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx)或指向 `DisplayCategoryPicture.aspx?CategoryID=categoryID`的 HTML `<img>` 元素来显示它。 其 URL 由数据库数据确定的映像可以使用 ImageField 在 GridView 或 DetailsView 中显示。 ImageField 包含 `DataImageUrlField` 和 `DataImageUrlFormatString` 属性，这些属性的工作方式类似于 HyperLinkField `DataNavigateUrlFields` 和 `DataNavigateUrlFormatString` 属性。

让我们通过添加 ImageField 来显示每个类别的图片，从而增加 `DisplayOrDownloadData.aspx` 中的 `Categories` GridView。 只需添加 ImageField，并将其 `DataImageUrlField` 和 `DataImageUrlFormatString` 属性分别设置为 `CategoryID` 和 `DisplayCategoryPicture.aspx?CategoryID={0}`。 这将创建一个 GridView 列，用于呈现一个 `<img>` 元素，该元素的 `src` 属性引用 `DisplayCategoryPicture.aspx?CategoryID={0}`，其中 {0} 被替换为 GridView 行 `CategoryID` 值。

![向 GridView 添加 ImageField](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**图 12**：向 GridView 添加 ImageField

添加 ImageField 后，GridView 的声明性语法应该如下所示：

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

请花点时间查看浏览器中的此页。 请注意每条记录现在如何包含类别的图片。

[![为每行显示类别的图片](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**图 13**：为每行显示类别的图片（[单击查看完全尺寸的图像](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png)）

## <a name="summary"></a>总结

在本教程中，我们介绍了如何提供二进制数据。 数据的显示方式取决于数据的类型。 对于 PDF 手册文件，我们向用户提供了一个 View 宣传册链接，单击该链接后，用户就可以直接使用 PDF 文件。 对于 "类别" 图，我们首先创建了一个页面，用于检索和返回数据库中的二进制数据，然后使用该页面显示 GridView 中的每个类别图片。

现在，我们已经介绍了如何显示二进制数据，接下来可以检查如何针对数据库执行插入、更新和删除操作。 在下一教程中，我们将介绍如何将上传的文件与相应的数据库记录相关联。 在本教程中，我们将了解如何更新现有的二进制数据，以及如何在删除其关联的记录时删除二进制数据。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Teresa Murphy 和 Dave Gardner。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](uploading-files-vb.md)
> [下一页](including-a-file-upload-option-when-adding-a-new-record-vb.md)
