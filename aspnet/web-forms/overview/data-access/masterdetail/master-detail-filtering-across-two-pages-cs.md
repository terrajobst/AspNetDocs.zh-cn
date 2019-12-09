---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: 跨两个页面的母版/C#详细信息筛选（） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将通过使用 GridView 列出数据库中的供应商来实现此模式。 GridView 中的每个供应商行都包含一个视图 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: ccb3bfa5f215ba6e65b8a10b40041d5c2896c7e3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620029"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>跨两个页面的母版/详细信息筛选 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe)或[下载 PDF](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> 在本教程中，我们将通过使用 GridView 列出数据库中的供应商来实现此模式。 GridView 中的每个供应商行将包含一个 "查看产品" 链接，单击此链接时，用户将进入单独的页面，其中列出了所选供应商提供的产品。

## <a name="introduction"></a>简介

在前两个教程中，我们看到了如何[使用 DropDownLists 在单个网页中显示大纲/详细信息报表](master-detail-filtering-with-a-dropdownlist-cs.md)，以[显示 "母版" 记录，并显示 GridView 或 DetailsView 控件](master-detail-filtering-with-two-dropdownlists-cs.md)以显示 "详细信息"。 用于主/详细信息报表的另一种常见模式是在一个网页上创建主记录，并在另一个网页上显示详细信息。 类似于[ASP.NET 论坛](https://forums.asp.net/)的论坛网站是此模式的一个很好的示例。 ASP.NET 论坛由各种论坛组成入门、Web 窗体、数据呈现控件等。 每个论坛由多个线程组成，每个线程由多个帖子组成。 ASP.NET 论坛主页上列出了论坛。 单击论坛 whisks 您的 "`ShowForum.aspx`" 页，其中列出了该论坛的线索。 同样，单击某个线程会使你转到 `ShowPost.aspx`，这将显示已单击的线程的 post。

在本教程中，我们将通过使用 GridView 列出数据库中的供应商来实现此模式。 GridView 中的每个供应商行将包含一个 "查看产品" 链接，单击此链接时，用户将进入单独的页面，其中列出了所选供应商提供的产品。

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>步骤1：将`SupplierListMaster.aspx`和`ProductsForSupplierDetails.aspx`页面添加到`Filtering`文件夹

在第三个教程中定义页面布局时，我们在 `BasicReporting`、`Filtering`和 `CustomFormatting` 文件夹中添加了多个 "starter" 页面。 但是，我们此时并未为本教程添加入门页面，因此请花点时间将两个新页面添加到 `Filtering` 文件夹中： `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx`。 `SupplierListMaster.aspx` 将在 `ProductsForSupplierDetails.aspx` 会显示所选供应商的产品时列出 "主" 记录（供应商）。

创建这两个新页面时，请确保将它们与 `Site.master` 母版页关联。

![将 SupplierListMaster 和 ProductsForSupplierDetails 页添加到筛选文件夹](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**图 1**：将 `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx` 页面添加到 `Filtering` 文件夹

此外，在项目中添加新页时，请确保相应地更新站点地图文件 `Web.sitemap`。 对于本教程，只需使用以下 XML 内容将 `SupplierListMaster.aspx` 页面添加到站点地图，作为筛选报告 `<siteMapNode>` 元素的子元素：

[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> 添加新的 ASP.NET 页面时，可以使用[Allen](http://odetocode.com/Blogs/scott/)的免费 Visual Studio[站点导航宏](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)，帮助自动更新站点映射文件。

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>步骤2：在`SupplierListMaster.aspx` 中显示供应商列表

创建 `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx` 页面后，下一步就是在 `SupplierListMaster.aspx`中创建供应商的 GridView。 将 GridView 添加到页面，并将其绑定到新的 ObjectDataSource。 此 ObjectDataSource 应使用 `SuppliersBLL` 类的 `GetSuppliers()` 方法返回所有供应商。

[![选择 SuppliersBLL 类](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**图 2**：选择 `SuppliersBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image4.png)）

[![将 ObjectDataSource 配置为使用 GetSuppliers （）方法](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**图 3**：将 ObjectDataSource 配置为使用 `GetSuppliers()` 方法（[单击查看完全大小的映像](master-detail-filtering-across-two-pages-cs/_static/image7.png)）

我们需要在每个 GridView 行中包含标题为 "查看产品" 的链接，在单击此链接时，将使用户通过 querystring `ProductsForSupplierDetails.aspx` 传入所选行的 `SupplierID` 值。 例如，如果用户单击东京商贸供应商的 "查看产品" 链接（其 `SupplierID` 值为4），则应将其发送到 `ProductsForSupplierDetails.aspx?SupplierID=4`。

若要实现此目的，请将[HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx)添加到 gridview，这会向每个 gridview 行添加一个超链接。 从 GridView 的智能标记中单击 "编辑列" 链接开始。 接下来，从左上角的列表中选择 "HyperLinkField"，然后单击 "添加"，在 GridView 的字段列表中包括 HyperLinkField。

[![向 GridView 添加 HyperLinkField](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**图 4**：向 GridView 添加 HyperLinkField （[单击查看完全尺寸的图像](master-detail-filtering-across-two-pages-cs/_static/image10.png)）

可以将 HyperLinkField 配置为对每个 GridView 行中的链接使用相同的文本或 URL 值，也可以将这些值基于绑定到每个特定行的数据值。 若要在所有行中指定静态值，请使用 HyperLinkField 的 `Text` 或 `NavigateUrl` 属性。 由于我们希望所有行的链接文本都是相同的，因此请将 HyperLinkField 的 `Text` 属性设置为 "查看产品"。

[![将 HyperLinkField 的 Text 属性设置为 "查看产品"](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**图 5**：将 HyperLinkField 的 `Text` 属性设置为 "查看产品" （[单击查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image13.png)）

若要将文本或 URL 值设置为基于绑定到 GridView 行的基础数据，请指定要在 `DataTextField` 或 `DataNavigateUrlFields` 属性中从其拉取文本或 URL 值的数据字段。 只能将 `DataTextField` 设置为单个数据字段;但是，可以将 `DataNavigateUrlFields`设置为数据字段的逗号分隔列表。 我们经常需要将文本或 URL 基于当前行的数据字段值和一些静态标记的组合。 例如，在本教程中，我们想要 `ProductsForSupplierDetails.aspx?SupplierID=supplierID`HyperLinkField 链接的 URL，其中 *`supplierID`* 每个 GridView 的 row's `SupplierID` 值。 请注意，此处需要静态值和数据驱动值：链接 URL 的 `ProductsForSupplierDetails.aspx?SupplierID=` 部分是静态的，而 *`supplierID`* 部分是数据驱动的，因为其值是每行自己的 `SupplierID` 值。

若要指示静态值和数据驱动的值的组合，请使用 "`DataTextFormatString`" 和 "`DataNavigateUrlFormatString`" 属性。 在这些属性中，根据需要输入静态标记，然后使用标记 `{0}` 要显示 `DataTextField` 或 `DataNavigateUrlFields` 属性中指定的字段值的位置。 如果 `DataNavigateUrlFields` 属性指定了多个字段，请使用 `{0}` 要插入第一个字段值的位置，为第二个字段值 `{1}`，依此类推。

在我们的教程中，我们需要将 `DataNavigateUrlFields` 属性设置为 `SupplierID`，因为这是一个数据字段，该字段的值需要按行自定义，而 `DataNavigateUrlFormatString` 属性 `ProductsForSupplierDetails.aspx?SupplierID={0}`。

[![将 HyperLinkField 配置为包含基于供应商的正确链接 URL](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**图 6**：将 HyperLinkField 配置为包含基于 `SupplierID` 的正确链接 URL （[单击查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image16.png)）

添加 HyperLinkField 后，可以随意自定义并重新排列 GridView 字段。 下面的标记显示了一些次要的字段级自定义项后的 GridView。

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

请花点时间查看浏览器中的 "`SupplierListMaster.aspx`" 页。 如图7所示，页面当前列出了包括 "查看产品" 链接在内的所有供应商。 单击 "查看产品" 链接将转到 `ProductsForSupplierDetails.aspx`，并沿查询字符串中的供应商 `SupplierID`。

[每个供应商行 ![包含 "查看产品" 链接](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**图 7**：每个供应商行包含一个 "查看产品" 链接（[单击以查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image19.png)）

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>步骤3：在`ProductsForSupplierDetails.aspx` 中列出供应商的产品

此时，`SupplierListMaster.aspx` 页会将用户发送到 `ProductsForSupplierDetails.aspx`，并将所选供应商的 `SupplierID` 传递到查询字符串。 本教程的最后一步是在 `ProductsForSupplierDetails.aspx` 中显示 GridView 中的产品，其 `SupplierID` 等于通过 querystring 传递的 `SupplierID`。 若要开始此 `ProductsForSupplierDetails.aspx` 开始，请使用名为 `ProductsBySupplierDataSource` 的新 ObjectDataSource 控件，该控件从 `ProductsBLL` 类中调用 `GetProductsBySupplierID(supplierID)` 方法。

[![添加名为 ProductsBySupplierDataSource 的新 ObjectDataSource](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**图 8**：添加名为 `ProductsBySupplierDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](master-detail-filtering-across-two-pages-cs/_static/image22.png)）

[![选择 ProductsBLL 类](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**图 9**：选择 `ProductsBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image25.png)）

[![让 ObjectDataSource 调用 GetProductsBySupplierID （供应商）方法](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**图 10**：使 ObjectDataSource 调用 `GetProductsBySupplierID(supplierID)` 方法（[单击查看完全大小的映像](master-detail-filtering-across-two-pages-cs/_static/image28.png)）

"配置数据源" 向导的最后一步要求我们提供 `GetProductsBySupplierID(supplierID)` 方法 *`supplierID`* 参数的源。 若要使用查询字符串值，请将参数源设置为 QueryString，并输入要在 "QueryStringField" 文本框中使用的 querystring 值的名称（`SupplierID`）。

[![从供应商参数值填充供应商参数值](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**图 11**：从 `SupplierID` Querystring 值填充 *`supplierID`* 参数值（[单击以查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image31.png)）

就这么简单！ 图12通过单击 `SupplierListMaster.aspx`中的东京商贸链接，显示 "`ProductsForSupplierDetails.aspx`" 页面。

[显示了东京商贸提供的产品 ![](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**图 12**：显示了东京商贸提供的产品（[单击查看全尺寸图像](master-detail-filtering-across-two-pages-cs/_static/image34.png)）

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>在`ProductsForSupplierDetails.aspx` 中显示供应商信息

如图12所示，`ProductsForSupplierDetails.aspx` 页只列出了查询字符串中指定的 `SupplierID` 所提供的产品。 但是，直接发送到此页面的人不知道图12显示了东京商贸的产品。 若要解决此情况，还可以在此页中显示供应商信息。

首先，将 FormView 添加到 "产品" GridView 之上。 创建一个名为 `SuppliersDataSource` 的新 ObjectDataSource 控件，该控件调用 `SuppliersBLL` 类的 `GetSupplierBySupplierID(supplierID)` 方法。

[![选择 SuppliersBLL 类](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**图 13**：选择 `SuppliersBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image37.png)）

[![让 ObjectDataSource 调用 GetSupplierBySupplierID （供应商）方法](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**图 14**：使 ObjectDataSource 调用 `GetSupplierBySupplierID(supplierID)` 方法（[单击查看完全大小的映像](master-detail-filtering-across-two-pages-cs/_static/image40.png)）

与 `ProductsBySupplierDataSource`一样，将 *`supplierID`* 参数分配给 `SupplierID` querystring 值的值。

[![从供应商参数值填充供应商参数值](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**图 15**：从 `SupplierID` Querystring 值填充 *`supplierID`* 参数值（[单击以查看完全大小的映像](master-detail-filtering-across-two-pages-cs/_static/image43.png)）

将 FormView 绑定到设计视图中的 ObjectDataSource 时，Visual Studio 将自动创建 FormView 的 `ItemTemplate`、`InsertItemTemplate`和 `EditItemTemplate`，其中包含由 ObjectDataSource 返回的每个数据字段的标签和 TextBox Web 控件。 因为我们只是想要显示供应商信息，可以随意删除 `InsertItemTemplate` 和 `EditItemTemplate`。 接下来，编辑 ItemTemplate，使其在 `<h3>` 元素中显示供应商的公司名称，以及公司名称下的地址、城市、国家/地区和电话号码。 另外，还可以手动设置 FormView 的 `DataSourceID`，并创建 `ItemTemplate` 标记，就像我们在 "[通过 ObjectDataSource 显示数据](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" 教程中所做的那样。

完成编辑后，FormView 的声明性标记应如下所示：

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

图16显示了上面详细说明的供应商信息之后 `ProductsForSupplierDetails.aspx` 页的屏幕截图。

[![产品列表包括有关供应商的摘要](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**图 16**：产品列表包括有关供应商的摘要（[单击以查看完全尺寸的图像](master-detail-filtering-across-two-pages-cs/_static/image46.png)）

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>应用`ProductsForSupplierDetails.aspx`UI 的最后润色

若要改善此报表的用户体验，我们应该在 "`ProductsForSupplierDetails.aspx`" 页中添加一些内容。 目前，用户可从 "`ProductsForSupplierDetails.aspx`" 页返回到供应商列表的唯一方式是单击其浏览器的 "后退" 按钮。 让我们将超链接控件添加到链接回 `SupplierListMaster.aspx`的 `ProductsForSupplierDetails.aspx` 页面，从而为用户返回主列表提供了另一种方法。

[![添加超链接控件以使用户返回到 SupplierListMaster](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**图 17**：添加一个超链接控件以使用户回到 `SupplierListMaster.aspx` （[单击查看完全大小的图像](master-detail-filtering-across-two-pages-cs/_static/image49.png)）

如果用户单击没有任何产品的供应商的 "查看产品" 链接，则 `ProductsForSupplierDetails.aspx` 中的 `ProductsBySupplierDataSource` ObjectDataSource 不会返回任何结果。 绑定到 ObjectDataSource 的 GridView 不会在用户浏览器的页面上呈现导致空白区域的任何标记。 为了更清晰地传达给用户，如果没有与所选供应商关联的产品，我们可以将 GridView 的 `EmptyDataText` 属性设置为在出现这种情况时要显示的消息。 我已将此属性设置为 "没有此供应商提供的产品"

默认情况下，Northwinds 数据库中的所有供应商都至少提供一个产品。 但是，在本教程中，我手动修改了 `Products` 表，以便供应商 Escargots Nouveaux 不再与任何产品关联。 图18显示了进行此更改之后，Escargots Nouveaux 的详细信息页。

[通知 ![用户供应商未提供任何产品](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**图 18**：通知用户供应商未提供任何产品（[单击查看完全尺寸的图像](master-detail-filtering-across-two-pages-cs/_static/image52.png)）

## <a name="summary"></a>总结

虽然大纲/详细信息报表可以在单个页面上显示主记录和详细记录，但在许多网站中，它们在两个网页之间分隔开。 在本教程中，我们将介绍如何通过 "主" 网页和 "详细信息" 页中列出的关联产品中列出的供应商，来实现此类主/从报表。 主网页中的每个供应商行都包含指向详细信息页的链接，该链接通过行的 `SupplierID` 值传递。 使用 GridView 的 HyperLinkField 可以轻松地添加这类特定于行的链接。

在 "详细信息" 页中，通过调用 `ProductsBLL` 类的 `GetProductsBySupplierID(supplierID)` 方法来为指定的供应商检索那些产品。 *`supplierID`* 参数值是使用 querystring 作为参数源以声明方式指定的。 还介绍了如何使用 FormView 在详细信息页中显示供应商详细信息。

我们的[下一教程](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)是主/详细信息报表中的最后一个教程。 我们将介绍如何在 GridView 中显示一系列产品，其中每行都有一个 "选择" 按钮。 单击 "选择" 按钮将在同一页面上的 DetailsView 控件中显示该产品的详细信息。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-with-two-dropdownlists-cs.md)
> [下一页](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
