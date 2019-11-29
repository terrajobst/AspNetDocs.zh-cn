---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: 生成自定义数据库驱动的站点地图提供程序（VB） |Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 中的默认站点地图提供程序检索静态 XML 文件中的数据。 尽管基于 XML 的提供程序适用于许多小型和中型 siz 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 78051696bd75e1d574f55b1c5d5891fe67c3030d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74630114"
---
# <a name="building-a-custom-database-driven-site-map-provider-vb"></a>生成自定义数据库驱动站点地图提供程序 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip)或[下载 PDF](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> ASP.NET 2.0 中的默认站点地图提供程序检索静态 XML 文件中的数据。 虽然基于 XML 的提供程序适用于许多小型和中型网站，但更大的 Web 应用程序需要更多的动态站点地图。 在本教程中，我们将构建一个自定义站点地图提供程序，该提供程序从业务逻辑层检索其数据，然后从数据库中检索数据。

## <a name="introduction"></a>简介

ASP.NET 2.0 s 站点地图功能使页面开发人员能够在某个持久性媒体（如 XML 文件）中定义 web 应用程序的站点地图。 定义后，可以通过[`System.Web` 命名空间](https://msdn.microsoft.com/library/system.web.aspx)中的[`SiteMap` 类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)或通过各种导航 Web 控件以编程方式访问站点地图数据，如 SiteMapPath、Menu 和 TreeView 控件。 站点地图系统使用[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，以便可以创建不同的站点地图序列化实现并将其插入到 web 应用程序中。 ASP.NET 2.0 附带的默认站点地图提供程序在 XML 文件中保留了站点地图结构。 回到[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，我们创建了一个名为 `Web.sitemap` 的文件，其中包含此结构，并且已使用每个新的教程部分更新其 XML。

如果站点地图的结构是非常静态的，例如这些教程，则基于 XML 的默认站点地图提供程序工作正常。 但在许多情况下，需要更多动态站点地图。 请考虑图1中显示的站点地图，其中每个类别和产品都显示为网站结构中的部分。 使用此站点地图，访问与根节点相对应的网页可能会列出所有类别，而访问特定类别的网页会列出该类别的产品，查看特定的产品网页会显示该产品的详细信息。

[![类别和产品构成站点地图 s 结构](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**图 1**：类别和产品构成了站点地图 s 结构（[单击以查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png)）

虽然此基于类别和产品的结构可能会硬编码到 `Web.sitemap` 文件中，但每次添加、删除或重命名类别或产品时，都需要更新该文件。 因此，如果在从数据库中检索到其结构，或理想情况下从应用程序体系结构的业务逻辑层中检索到站点地图维护，则会大大简化。 这样，在添加、重命名或删除产品和类别时，站点地图会自动更新以反映这些更改。

由于 ASP.NET 2.0 s 站点地图序列化是在提供程序模型的基础上构建的，因此我们可以创建自己的自定义站点地图提供程序，用于从备用数据存储区（例如数据库或体系结构）获取其数据。 在本教程中，我们将构建一个自定义提供程序，用于从 BLL 检索其数据。 让我们开始吧！

> [!NOTE]
> 在本教程中创建的自定义站点地图提供程序与应用程序体系结构和数据模型紧密耦合。 Jeff Prosise 将[站点地图存储在 SQL Server 中](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)，而[SQL 站点地图提供程序已在等待](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)文章检查在 SQL Server 中存储站点地图数据的通用方法。

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>步骤1：创建自定义站点地图提供程序网页

在开始创建自定义站点地图提供程序之前，让我们先添加本教程所需的 ASP.NET 页面。 首先添加一个名为 `SiteMapProvider`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

同时将 `CustomProviders` 子文件夹添加到 `App_Code` 文件夹。

![为站点地图提供程序相关教程添加 ASP.NET 页](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**图 2**：为站点地图提供程序相关教程添加 ASP.NET 页

由于此部分只有一个教程，因此，我们不需要 `Default.aspx` 列出章节教程。 `Default.aspx` 将显示 GridView 控件中的类别。 我们将在步骤2中解决此情况。

接下来，更新 `Web.sitemap` 以包含对 `Default.aspx` 页的引用。 具体而言，请在缓存 `<siteMapNode>`后面添加以下标记：

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧的菜单中包含了用于唯一站点地图提供程序教程的一项。

![站点映射现在包含用于站点地图提供程序教程的条目](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**图 3**：站点映射现在包含用于站点地图提供程序教程的条目

本教程的主要重点是说明如何创建自定义站点地图提供程序，以及如何将 web 应用程序配置为使用该访问接口。 具体而言，我们将生成一个提供程序，该提供程序返回一个站点地图，其中包含一个根节点以及每个类别和产品的节点，如图1中所示。 通常，站点地图中的每个节点都可以指定一个 URL。 对于我们的站点地图，根节点 s URL 将 `~/SiteMapProvider/Default.aspx`，这将列出数据库中的所有类别。 网站图中的每个类别节点都有一个指向 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`的 URL，它将列出指定*类别 id*中的所有产品。 最后，每个产品网站地图节点将指向 `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`，这将显示特定产品的详细信息。

首先，我们需要创建 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 页面。 这些页面分别在步骤2、3和4中完成。 由于本教程的主旨是是在站点地图提供商的基础上完成的，并且由于过去的教程介绍了如何创建这类多页面大纲/详细信息报告，因此我们将经历步骤2到4。 如果需要有关创建跨越多页的主/详细信息报表的复习，请参阅 "[跨两个页面的大纲/详细筛选](../masterdetail/master-detail-filtering-across-two-pages-vb.md)" 教程。

## <a name="step-2-displaying-a-list-of-categories"></a>步骤2：显示类别列表

打开 `SiteMapProvider` 文件夹中的 "`Default.aspx`" 页，然后将 GridView 从工具箱拖到设计器上，并将其 `ID` 设置为 "`Categories`"。 从 GridView s 智能标记中，将其绑定到名为 `CategoriesDataSource` 的新 ObjectDataSource，并对其进行配置，使其使用 `CategoriesBLL` class s `GetCategories` 方法检索其数据。 由于此 GridView 只显示类别而不提供数据修改功能，因此请将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![使用 GetCategories 方法将 ObjectDataSource 配置为返回类别](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**图 4**：将 ObjectDataSource 配置为使用 `GetCategories` 方法返回类别（[单击以查看完全大小的映像](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**图 5**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png)）

完成 "配置数据源" 向导后，Visual Studio 将为 `CategoryID`、`CategoryName`、`Description`、`NumberOfProducts`和 `BrochurePath`添加 BoundField。 编辑 GridView，使其仅包含 `CategoryName` 和 `Description` BoundFields，并将 `CategoryName` BoundField `HeaderText` 属性更新为 "类别"。

接下来，添加 HyperLinkField 并将其定位到最左侧的字段。 将 `DataNavigateUrlFields` 属性设置为 `CategoryID`，将 `DataNavigateUrlFormatString` 属性设置为 "`~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`"。 将 `Text` 属性设置为 "查看产品"。

![将 HyperLinkField 添加到类别 GridView](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**图 6**：将 HyperLinkField 添加到 `Categories` GridView

创建 ObjectDataSource 并自定义 GridView 字段之后，这两个控件的声明性标记将如下所示：

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

图7显示了通过浏览器查看 `Default.aspx`。 单击类别 "查看产品" 链接可将你带到 `ProductsByCategory.aspx?CategoryID=categoryID`，我们将在步骤3中进行构建。

[每个类别 ![列出了 "查看产品" 链接](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**图 7**：列出了每个类别以及 "查看产品" 链接（[单击以查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png)）

## <a name="step-3-listing-the-selected-category-s-products"></a>步骤3：列出选定类别的产品

打开 "`ProductsByCategory.aspx`" 页面并添加一个 GridView，并将其命名为 `ProductsByCategory`。 将 GridView 从其智能标记绑定到名为 `ProductsByCategoryDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法，并将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![使用 ProductsBLL Class s GetProductsByCategoryID （类别 Id）方法](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**图 8**：使用 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法（[单击以查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png)）

"配置数据源" 向导中的最后一步提示输入*类别 id*的参数源。 由于此信息通过 querystring 字段 `CategoryID`传递，因此请从下拉列表中选择 "QueryString"，然后在 "QueryStringField" 文本框中输入 "类别 Id"，如图9所示。 单击“完成”按钮以完成向导。

[![使用 "类别 id" 参数的 "类别 Id" 字段](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**图 9**：对*类别 id*参数使用 `CategoryID` Querystring 字段（[单击以查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png)）

完成向导后，Visual Studio 会将相应的 BoundFields 和 CheckBoxField 添加到 "产品数据" 字段的 GridView。 删除除 `ProductName`、`UnitPrice`和 `SupplierName` 的所有 BoundFields。 将这三个 BoundFields `HeaderText` 属性分别自定义为读取产品、价格和供应商。 将 `UnitPrice` BoundField 的格式设置为货币。

接下来，添加 HyperLinkField 并将其移动到最左侧位置。 将其 `Text` 属性设置为查看详细信息，将其 `DataNavigateUrlFields` 属性设置为 `ProductID`，并将其 `DataNavigateUrlFormatString` 属性设置为 `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`。

![添加指向 ProductDetails 的视图详细信息 HyperLinkField](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**图 10**：添加指向 `ProductDetails.aspx` 的视图详细信息 HyperLinkField

进行这些自定义后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

返回到通过浏览器查看 `Default.aspx`，并单击 "查看饮料" 的 "产品" 链接。 这会使您 `ProductsByCategory.aspx?CategoryID=1`，并在 Northwind 数据库中显示属于饮料类别的产品的名称、价格和供应商（参见图11）。 欢迎随时进一步增强此页面，使其包含一个用于将用户返回到类别列表页（`Default.aspx`）的链接和一个显示所选类别名称和说明的 DetailsView 或 FormView 控件。

[显示饮料姓名、价格和供应商的 ![](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**图 11**：显示饮料姓名、价格和供应商（[单击查看完全尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png)）

## <a name="step-4-showing-a-product-s-details"></a>步骤4：显示产品详细信息

最后一页 `ProductDetails.aspx`"将显示选定产品的详细信息。 打开 `ProductDetails.aspx` 并将 DetailsView 从工具箱拖到设计器上。 将 "DetailsView s" `ID` 属性设置为 "`ProductInfo` 并清除其 `Height` 和 `Width` 属性值。 从其智能标记中，将 DetailsView 绑定到名为 `ProductDataSource`的新 ObjectDataSource，配置 ObjectDataSource 以便从 `ProductsBLL` 类 s `GetProductByProductID(productID)` 方法拉取其数据。 与第2步和第3步中创建的上一个网页一样，将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![将 ObjectDataSource 配置为使用 GetProductByProductID （productID）方法](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**图 12**：将 ObjectDataSource 配置为使用 `GetProductByProductID(productID)` 方法（[单击查看完全大小的映像](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png)）

"配置数据源" 向导的最后一步提示输入*productID*参数的源。 由于此数据通过 querystring 字段 `ProductID`，因此请将下拉列表设置为 QueryString，将 QueryStringField 文本框设置为 ProductID。 最后，单击 "完成" 按钮以完成该向导。

[![将 productID 参数配置为从 ProductID Querystring 字段请求其值](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**图 13**：将*productID*参数配置为从 `ProductID` Querystring 字段拉取其值（[单击以查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png)）

完成 "配置数据源" 向导后，Visual Studio 将在 "产品数据" 字段的 DetailsView 中创建相应的 BoundFields 和一个 CheckBoxField。 删除 `ProductID`、`SupplierID`和 `CategoryID` BoundFields，并根据需要配置其余字段。 经过少量的美观配置后，DetailsView 和 ObjectDataSource 的声明性标记如下所示：

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

若要测试此页，请返回到 `Default.aspx` 并单击 "饮料" 类别的 "查看产品"。 在饮料产品列表中，单击 Chai 茶的 "查看详细信息" 链接。 这会使你转到 `ProductDetails.aspx?ProductID=1`，其中显示 Chai 茶 s 详细信息（参见图14）。

[显示 ![Chai 茶 s 供应商、类别、价格和其他信息](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**图 14**：显示 Chai 茶的供应商、类别、价格和其他信息（[单击查看全尺寸图像](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png)）

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>步骤5：了解站点地图提供程序的内部工作原理

站点地图在 web 服务器的内存中表示为构成层次结构的 `SiteMapNode` 实例的集合。 必须有且仅有一个根，所有非根节点必须正好有一个父节点，并且所有节点可能具有任意数量的子节点。 每个 `SiteMapNode` 对象表示网站 s 结构中的一个部分;这些部分通常具有相应的网页。 因此， [`SiteMapNode` 类](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)具有 `Title`、`Url`和 `Description`等属性，这些属性提供了 `SiteMapNode` 表示的部分的信息。 还有一个 `Key` 属性，用于唯一标识层次结构中的每个 `SiteMapNode`，以及用于建立此层次结构的属性 `ChildNodes`、`ParentNode`、`NextSibling`、`PreviousSibling`等。

图15显示了图1中的一般站点地图结构，但更详细地介绍了实现细节。

[![每个 SiteMapNode 都具有诸如标题、Url、密钥等属性](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**图 15**：每个 `SiteMapNode` 都具有诸如 `Title`、`Url`、`Key`等属性（[单击查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif)）

站点地图可通过[`System.Web` 命名空间](https://msdn.microsoft.com/library/system.web.aspx)中的[`SiteMap` 类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)进行访问。 此类 `RootNode` 属性返回站点地图 s `SiteMapNode` 实例;`CurrentNode` 返回其 `Url` 属性与当前请求的页面的 URL 匹配的 `SiteMapNode`。 此类由 ASP.NET 2.0 s 导航 Web 控件在内部使用。

当访问 `SiteMap` 类的属性时，它必须将站点地图结构从一些持久性媒体序列化到内存中。 但是，站点地图序列化逻辑未硬编码到 `SiteMap` 类中。 相反，在运行时，`SiteMap` 类将确定要用于序列化的站点地图*提供程序*。 默认情况下，使用[`XmlSiteMapProvider` 类](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)，这会从格式正确的 XML 文件中读取站点地图 s 的结构。 不过，通过一些工作，我们可以创建自己的自定义站点地图提供程序。

所有站点地图提供程序都必须派生自[`SiteMapProvider` 类，该类](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)包含站点地图提供程序所需的基本方法和属性，但省略了许多实现细节。 第二类[`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)扩展 `SiteMapProvider` 类，并包含所需功能的更可靠的实现。 在内部，`StaticSiteMapProvider` 将站点映射的 `SiteMapNode` 实例存储在一个 `Hashtable` 中，并提供 `AddNode(child, parent)`、`RemoveNode(siteMapNode),` 和 `Clear()` 的方法，这些方法可在内部 `SiteMapNode` 添加和删除 `Hashtable`。 `XmlSiteMapProvider` 派生自 `StaticSiteMapProvider`。

创建扩展 `StaticSiteMapProvider`的自定义站点地图提供程序时，必须重写以下两个抽象方法： [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx)和[`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx)。 正如其名称所示，`BuildSiteMap`负责从持久性存储区加载站点地图结构，并在内存中构建它。 `GetRootNodeCore` 在站点地图中返回根节点。

在 web 应用程序可以使用站点地图提供程序之前，必须在应用程序配置中注册它。 默认情况下，使用 `AspNetXmlSiteMapProvider`名称注册 `XmlSiteMapProvider` 类。 若要注册其他站点地图提供程序，请将以下标记添加到 `Web.config`：

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

*Name*值向提供者分配一个可读的名称，同时*键入*指定站点地图提供程序的完全限定的类型名称。 在创建自定义站点地图提供程序后，我们将探讨步骤7中 "*名称*" 和 "*类型*" 值的具体值。

在第一次从 `SiteMap` 类访问站点地图提供程序类时，它将实例化，并在 web 应用程序的生存期内保留在内存中。 由于只有一个站点地图提供程序实例可以从多个并发网站访问者调用，因此提供程序的方法必须是*线程安全*的。

出于性能和可伸缩性的原因，请务必缓存内存中的站点地图结构并返回此缓存的结构，而不是在每次调用 `BuildSiteMap` 方法时重新创建。 每个用户可以对每个页面请求调用 `BuildSiteMap` 数次，具体取决于页面上使用的导航控件和站点地图结构的深度。 在任何情况下，如果我们在每次调用时都不会将站点地图结构缓存在 `BuildSiteMap` 中，则需要重新检索体系结构中的产品和类别信息（这将导致对数据库的查询）。 如前面的缓存教程中所述，缓存的数据可能会过时。 为了应对这种情况，我们可以使用基于时间或 SQL 缓存依赖项的 expiries。

> [!NOTE]
> 站点地图提供程序可以有选择地重写[`Initialize` 方法](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)。 在第一次实例化站点地图提供程序时，将调用 `Initialize`，并在 `<add>` 元素（如： `<add name="name" type="type" customAttribute="value" />`）中将分配给提供程序的任何自定义特性传递到 `Web.config` 中。 如果要允许页面开发人员指定不同于站点地图提供程序的相关设置，而无需修改提供程序的代码，则此方法非常有用。 例如，如果从数据库直接读取类别和产品数据而不是通过体系结构，我们可能希望让页面开发人员通过 `Web.config` 指定数据库连接字符串，而不是在提供程序代码中使用硬编码值。 我们将在步骤6中生成的自定义站点地图提供程序不会重写此 `Initialize` 方法。 有关使用 `Initialize` 方法的示例，请参阅[在 SQL Server 文章中](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)了解[Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s 存储站点地图。

## <a name="step-6-creating-the-custom-site-map-provider"></a>步骤6：创建自定义站点地图提供程序

若要创建自定义站点地图提供程序，该提供程序从 Northwind 数据库的类别和产品中生成网站地图，我们需要创建一个扩展 `StaticSiteMapProvider`的类。 在步骤1中，我要求您在 `App_Code` 文件夹中添加一个 `CustomProviders` 文件夹-将一个新类添加到名为 `NorthwindSiteMapProvider`的此文件夹中。 将下面的代码添加到 `NorthwindSiteMapProvider` 类中:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

首先，让我们从[`lock` 的语句](https://msdn.microsoft.com/library/c5kehkcz.aspx)开始探索此类 `BuildSiteMap` 方法。 `lock` 语句一次只允许一个线程进入，从而序列化其代码的访问权限，防止两个并发线程单步执行另一个手脚。

类级别 `SiteMapNode` 变量 `root` 用于缓存站点地图结构。 第一次构造站点地图时，或在基础数据修改后首次构造时，将 `Nothing` `root`，并构造站点地图结构。 在构造过程中，会将站点地图 s 根节点分配到 `root`，以便在下次调用此方法时，`root` 不会 `Nothing`。 因此，只要 `root` 不 `Nothing`，就会将站点地图结构返回给调用方，而不必重新创建它。

如果根 `Nothing`，则将从产品和类别信息创建站点地图结构。 站点地图是通过创建 `SiteMapNode` 实例，然后通过调用 `StaticSiteMapProvider` class s `AddNode` 方法生成的。 `AddNode` 执行内部簿记，将分类 `SiteMapNode` 实例存储在 `Hashtable`中。 开始构造层次结构之前，首先调用 `Clear` 方法，该方法从内部 `Hashtable`中清除元素。 接下来，`ProductsBLL` 类 s `GetProducts` 方法和生成的 `ProductsDataTable` 存储在局部变量中。

站点地图的构造首先创建根节点并将其分配给 `root`。 此处和在此 `BuildSiteMap` 中使用的[`SiteMapNode` 构造函数](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx)的重载将传递以下信息：

- 对站点地图提供程序的引用（`Me`）。
- `Key`的 `SiteMapNode`。 对于每个 `SiteMapNode`，此必需的值必须是唯一的。
- `Url`的 `SiteMapNode`。 `Url` 是可选的，但是如果提供，则每个 `SiteMapNode` 的 `Url` 值都必须是唯一的。
- 需要 `SiteMapNode` `Title`。

`AddNode(root)` 方法调用将 `SiteMapNode` `root` 添加到站点地图作为根。 接下来，枚举 `ProductsDataTable` 中的每个 `ProductRow`。 如果已存在当前产品类别的 `SiteMapNode`，则引用它。 否则，将通过 `AddNode(categoryNode, root)` 方法调用创建类别的新 `SiteMapNode`，并将其添加为 `SiteMapNode``root` 的子项。 找到或创建相应类别 `SiteMapNode` "节点后，将为当前产品创建一个 `SiteMapNode`，并通过 `AddNode(productNode, categoryNode)`将其添加为类别 `SiteMapNode` 的子级。 请注意，`SiteMapNode` s `Url` 属性值的类别 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`，而产品 `SiteMapNode` `Url` 属性分配 `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`。

> [!NOTE]
> 对于其 `CategoryID` 具有数据库 `NULL` 值的那些产品将按类别 `SiteMapNode` 进行分组，其 `Title` 属性设置为 None，其 `Url` 属性设置为空字符串。 我决定将 `Url` 设置为空字符串，因为 `ProductBLL` 类 `GetProductsByCategory(categoryID)` 方法目前不能仅返回那些具有 `NULL` `CategoryID` 值的产品。 此外，我还希望演示导航控件如何呈现缺少 `Url` 属性值的 `SiteMapNode`。 我建议您扩展本教程，使 "无 `SiteMapNode` s `Url` 属性指向 `ProductsByCategory.aspx`，但只显示具有 `NULL` `CategoryID` 值的产品。

构造站点地图后，会使用 `Categories` 上的 SQL 缓存依赖关系将任意对象添加到数据缓存中，并通过 `AggregateCacheDependency` 对象 `Products` 表。 使用*Sql 缓存依赖项*，我们在前面的教程中探讨了如何使用 sql 缓存依赖项。 不过，自定义站点地图提供程序使用数据缓存的重载，该重载还 `Insert` 方法。 在从缓存中移除对象时，此重载接受作为其最终输入参数的委托。 具体来说，我们传入了一个新的[`CacheItemRemovedCallback` 委托](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx)，该委托指向在 `NorthwindSiteMapProvider` 类中进一步定义的 `OnSiteMapChanged` 方法。

> [!NOTE]
> 站点地图的内存中表示形式通过类级变量进行缓存 `root`。 由于自定义站点地图提供程序类只有一个实例，并且该实例在 web 应用程序中的所有线程之间共享，因此此类变量用作缓存。 `BuildSiteMap` 方法还使用数据缓存，但仅作为在 `Categories` 或 `Products` 表中的基础数据库数据更改时接收通知的方法。 请注意，放入数据缓存中的值只是当前日期和时间。 实际的站点地图数据*不*放入数据缓存中。

`BuildSiteMap` 方法通过返回站点地图的根节点完成。

其余方法非常简单。 `GetRootNodeCore` 负责返回根节点。 由于 `BuildSiteMap` 返回根，因此 `GetRootNodeCore` 只返回 `BuildSiteMap` 返回值。 删除缓存项时，`OnSiteMapChanged` 方法将 `root` 返回 `Nothing`。 当根设置回 `Nothing`时，下次调用 `BuildSiteMap` 时，将重新生成站点地图结构。 最后，`CachedDate` 属性返回存储在数据缓存中的日期和时间值（如果存在这样的值）。 页面开发人员可以使用此属性来确定上次缓存站点地图数据的时间。

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>步骤7：注册`NorthwindSiteMapProvider`

为了使 web 应用程序能够使用在步骤6中创建的 `NorthwindSiteMapProvider` 站点地图提供程序，我们需要在 `Web.config`的 `<siteMap>` 部分注册它。 具体而言，请在 `Web.config`中的 `<system.web>` 元素内添加以下标记：

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

此标记执行两个操作：首先，它指示内置 `AspNetXmlSiteMapProvider` 是默认站点地图提供程序;其次，它将在步骤6中创建的自定义站点地图提供程序注册为用户友好名称 Northwind。

> [!NOTE]
> 对于位于应用程序 `App_Code` 文件夹中的站点地图提供程序，`type` 属性的值只是类名。 此外，还可以在单独的类库项目中创建自定义站点地图提供程序，并将编译的程序集放置在 web 应用程序的 `/Bin` 目录中。 在这种情况下，`type` 属性值将为*Namespace*。*ClassName*， *AssemblyName* 。

更新 `Web.config`后，请花点时间在浏览器中查看教程中的任何页面。 请注意，左侧的导航界面仍显示 `Web.sitemap`中定义的部分和教程。 这是因为我们将 `AspNetXmlSiteMapProvider` 作为默认提供程序。 为了创建使用 `NorthwindSiteMapProvider`的导航用户界面元素，我们需要显式指定应使用 Northwind 站点地图提供程序。 我们将在步骤8中了解如何实现此目的。

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>步骤8：使用自定义站点地图提供程序显示站点地图信息

在 `Web.config`中创建并注册自定义站点地图提供程序后，我们就可以将导航控件添加到 `SiteMapProvider` 文件夹中的 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 页。 首先打开 `Default.aspx` 页面，然后将 `SiteMapPath` 从工具箱拖到设计器上。 SiteMapPath 控件位于 "工具箱" 的 "导航" 部分。

[![将 SiteMapPath 添加到 default.aspx](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**图 16**：将 SiteMapPath 添加到 `Default.aspx` （[单击查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif)）

SiteMapPath 控件显示一个痕迹导航，指示当前在站点地图中的位置。 我们在母版页*和站点导航*教程中的母版页顶部添加了 SiteMapPath。

请花点时间查看浏览器中的此页。 图16中添加的 SiteMapPath 使用默认的站点地图提供程序，从 `Web.sitemap`提取其数据。 因此，痕迹导航显示 Home &gt; 自定义站点地图，就像右上角的痕迹。

[![痕迹导航使用默认的站点地图提供程序](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**图 17**：痕迹导航使用默认的站点地图提供程序（[单击查看完全尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif)）

若要在图16中添加 SiteMapPath，请使用我们在步骤6中创建的自定义站点地图提供程序，并将其 " [`SiteMapProvider`" 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx)设置为 "Northwind"，并将该名称分配给 `Web.config`的 `NorthwindSiteMapProvider`。 遗憾的是，设计器将继续使用默认的站点地图提供程序，但如果在更改此属性后通过浏览器访问该页，则会看到痕迹导航现在使用自定义站点地图提供程序。

[![痕迹现在使用自定义站点地图提供程序 NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**图 18**：痕迹导航现在使用自定义站点地图提供程序 `NorthwindSiteMapProvider` （[单击查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif)）

SiteMapPath 控件在 "`ProductsByCategory.aspx`" 和 "`ProductDetails.aspx`" 页中显示功能更高的用户界面。 将 SiteMapPath 添加到这些页，同时将两个中的 `SiteMapProvider` 属性设置为 Northwind。 从 `Default.aspx` 单击 "饮料" 的 "查看产品" 链接，然后在 "Chai 茶" 的 "查看详细信息" 链接上单击。 如图19所示，痕迹导航包括当前站点地图部分（Chai 茶）及其上级：饮料和所有类别。

[![痕迹现在使用自定义站点地图提供程序 NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**图 19**：痕迹导航现在使用自定义站点地图提供程序 `NorthwindSiteMapProvider` （[单击查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png)）

除 SiteMapPath 外，还可以使用其他导航用户界面元素，例如菜单和 TreeView 控件。 本教程的下载中的 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 页，例如，所有包括菜单控件（请参阅图20）。 有关 ASP.NET 2.0 中的导航控件和站点地图系统的详细信息，请参阅查看[ASP.NET 2.0 s 站点导航功能](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)和[使用](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) [ASP.NET 2.0 快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/)的站点导航控件部分。

[![菜单控件列出每个类别和产品](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**图 20**：菜单控件列出了每个类别和产品（[单击以查看完全大小的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif)）

如本教程前面所述，可以通过 `SiteMap` 类以编程方式访问站点地图结构。 下面的代码返回默认提供程序的根 `SiteMapNode`：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

由于 `AspNetXmlSiteMapProvider` 是我们的应用程序的默认提供程序，以上代码将返回在 `Web.sitemap`中定义的根节点。 若要引用除默认值以外的站点地图提供程序，请使用 `SiteMap` 类[`Providers` 属性](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx)，如下所示：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

其中， *name*是自定义站点地图提供程序（web 应用程序）的名称。

若要访问特定于站点地图提供程序的成员，请使用 `SiteMap.Providers["name"]` 来检索提供程序实例，然后将其强制转换为相应的类型。 例如，若要在 ASP.NET 页中显示 `NorthwindSiteMapProvider` s `CachedDate` 属性，请使用以下代码：

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> 请务必测试 SQL 缓存依赖关系功能。 访问 `Default.aspx`、`ProductsByCategory.aspx`和 `ProductDetails.aspx` 页后，请在 "编辑"、"插入" 和 "删除" 部分中找到其中一个教程，然后编辑类别或产品的名称。 然后返回到 `SiteMapProvider` 文件夹中的某个页面。 假设已为轮询机制传递了足够的时间来记录对基础数据库的更改，则应更新站点地图以显示新的产品或类别名称。

## <a name="summary"></a>总结

ASP.NET 2.0 s 站点地图功能包括一个 `SiteMap` 类、许多内置的导航 Web 控件和一个需要将站点地图信息保存到 XML 文件的默认站点地图提供程序。 若要从某个其他源（例如数据库、应用程序的体系结构或远程 Web 服务）使用站点地图信息，我们需要创建自定义站点地图提供程序。 这涉及到从 `SiteMapProvider` 类创建直接或间接派生的类。

在本教程中，我们了解了如何创建自定义站点地图提供程序，该提供程序基于产品和类别信息剔除从应用程序体系结构中的站点图。 我们的提供程序扩展了 `StaticSiteMapProvider` 类，引起创建了检索数据的 `BuildSiteMap` 方法，构造了站点地图层次结构，并在类级变量中缓存了生成的结构。 在修改基础 `Categories` 或 `Products` 数据时，我们使用了一个包含回调函数的 SQL 缓存依赖项来使缓存的结构无效。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [在 SQL Server 中存储站点映射](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)，并在[以前等待的 SQL 站点地图提供程序](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)中存储
- [ASP.NET 2.0 s 提供程序模型的外观](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [提供商工具包](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [检查 ASP.NET 2.0 s 站点导航功能](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Dave Gardner、Zack、Teresa Murphy 和 Bernadette Leigh。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一部分](building-a-custom-database-driven-site-map-provider-cs.md)
