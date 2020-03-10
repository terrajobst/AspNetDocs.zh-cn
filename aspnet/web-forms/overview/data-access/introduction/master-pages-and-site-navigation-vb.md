---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-vb
title: 母版页和站点导航（VB） |Microsoft Docs
author: rick-anderson
description: 用户友好网站的一项常见特征是，它们具有一致的站点范围的页面布局和导航方案。 本教程介绍了如何
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 022801d8-a327-4d0c-8780-6094c9cee00d
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a2b5ba8c1781f1194f951a44661a8f7dd095f41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78426026"
---
# <a name="master-pages-and-site-navigation-vb"></a>母版页和站点导航 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_3_VB.exe)或[下载 PDF](master-pages-and-site-navigation-vb/_static/datatutorial03vb1.pdf)

> 用户友好网站的一项常见特征是，它们具有一致的站点范围的页面布局和导航方案。 本教程介绍如何在可以轻松更新的所有页面上创建一致的外观。

## <a name="introduction"></a>简介

用户友好网站的一项常见特征是，它们具有一致的站点范围的页面布局和导航方案。 ASP.NET 2.0 引入了两项新功能，可大大简化站点范围的页面布局和导航方案：母版页和站点导航方案。 母版页允许开发人员使用指定的可编辑区域创建站点范围的模板。 然后，可以将此模板应用于站点中的 ASP.NET 页。 此类 ASP.NET 页面只需提供母版页的指定可编辑区域的内容。母版页中所有其他标记在使用母版页的所有 ASP.NET 页上都是相同的。 此模型允许开发人员定义和集中站点范围的页面布局，从而更容易地在可以轻松更新的所有页面上创建一致的外观。

[站点导航系统](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)为页面开发人员提供了一种机制，供页面开发人员定义站点地图和 API，以便以编程方式查询该站点地图。 使用新的导航 Web 控件 Menu、TreeView 和 SiteMapPath，可以轻松地在公共导航用户界面元素中呈现全部或部分站点地图。 我们将使用默认的站点导航提供程序，这意味着我们的网站图将在 XML 格式的文件中定义。

为了说明这些概念并使我们的教程网站更易于使用，让我们在本课中定义站点范围的页面布局，实现站点地图，并添加导航 UI。 在本教程结束时，我们将获得精美的网站设计，用于构建教程网页。

[![本教程的最终结果](master-pages-and-site-navigation-vb/_static/image2.png)](master-pages-and-site-navigation-vb/_static/image1.png)

**图 1**：本教程的最终结果（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image3.png)）

## <a name="step-1-creating-the-master-page"></a>步骤1：创建母版页

第一步是创建站点的母版页。 现在，我们的网站仅由类型化数据集（`Northwind.xsd`、`App_Code` 文件夹）、BLL 类（`ProductsBLL.vb`、`CategoriesBLL.vb`等，它们都在 `App_Code` 文件夹中）、数据库（`NORTHWND.MDF`文件夹中的 `App_Data`）、配置文件（`Web.config`）和 CSS 样式表文件（`Styles.css`）组成。 由于我们将在以后的教程中更详细地 reexamining 这些示例，我清理了从前两个教程中使用 DAL 和 BLL 演示的这些页面和文件。

![项目中的文件](master-pages-and-site-navigation-vb/_static/image4.png)

**图 2**：项目中的文件

若要创建母版页，请在解决方案资源管理器中右键单击项目名称，然后选择 "添加新项"。 然后从模板列表中选择 "母版页类型"，并将其命名 `Site.master`。

[![将新的母版页添加到网站](master-pages-and-site-navigation-vb/_static/image6.png)](master-pages-and-site-navigation-vb/_static/image5.png)

**图 3**：向网站添加新的母版页（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image7.png)）

在此母版页中定义站点范围的页面布局。 您可以使用设计视图并添加所需的任何布局或 Web 控件，也可以手动在源视图中添加标记。 在我的母版页中，我将[级联样式表](http://www.w3schools.com/css/default.asp)用于通过在外部文件 `Style.css`中定义的 CSS 设置来定位和样式。 虽然无法从下面显示的标记中进行说明，但定义了 CSS 规则，以便将导航 `<div>`的内容绝对定位，使其显示在左侧，并且固定宽度为200像素。

站点主

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample1.aspx)]

母版页既定义静态页面布局，也定义可由使用母版页的 ASP.NET 页面编辑的区域。 这些内容可编辑区域由 ContentPlaceHolder 控件指示，可在内容 `<div>`中查看。 母版页有一个 ContentPlaceHolder （`MainContent`），但母版页的可能有多个 Contentplaceholder。

在上面输入的标记中，切换到设计视图显示母版页的布局。 使用此母版页的任何 ASP.NET 页面都将具有此统一布局，并能够指定 `MainContent` 区域的标记。

[使用 "设计" 视图查看母版页 ![](master-pages-and-site-navigation-vb/_static/image9.png)](master-pages-and-site-navigation-vb/_static/image8.png)

**图 4**：通过设计视图（[单击查看全尺寸图像](master-pages-and-site-navigation-vb/_static/image10.png)）查看的母版页

## <a name="step-2-adding-a-homepage-to-the-website"></a>步骤2：将主页添加到网站

定义母版页后，可以添加网站的 ASP.NET 页面。 首先，让我们添加 `Default.aspx`网站主页。 右键单击 "解决方案资源管理器中的项目名称，然后选择" 添加新项 "。 从 "模板" 列表中选择 "Web 窗体" 选项，并将文件命名 `Default.aspx`。 同时，选中 "选择母版页" 复选框。

[![添加新的 Web 窗体，选中 "选择母版页" 复选框](master-pages-and-site-navigation-vb/_static/image12.png)](master-pages-and-site-navigation-vb/_static/image11.png)

**图 5**：添加新的 Web 窗体，选中 "选择母版页" 复选框（[单击查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image13.png)）

单击 "确定" 按钮后，系统将要求您选择此新 ASP.NET 页应使用的母版页。 虽然你的项目中可以有多个母版页，但我们只有一个母版页。

[![选择此 ASP.NET 页应使用的母版页](master-pages-and-site-navigation-vb/_static/image15.png)](master-pages-and-site-navigation-vb/_static/image14.png)

**图 6**：选择此 ASP.NET 页应使用的母版页（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image16.png)）

选取母版页后，新的 ASP.NET 页面将包含以下标记：

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample2.aspx)]

在 `@Page` 指令中，有一个对使用的母版页文件的引用（`MasterPageFile="~/Site.master"`），ASP.NET 页的标记包含在母版页中定义的每个 ContentPlaceHolder 控件的内容控件，并 `ContentPlaceHolderID` 将内容控件映射到特定 ContentPlaceHolder。 内容控件是您要在相应 ContentPlaceHolder 中显示的标记的位置。 将 `@Page` 指令的 `Title` 属性设置为 Home，并向内容控件添加一些欢迎内容：

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample3.aspx)]

通过 `@Page` 指令中的 `Title` 属性，我们可以从 ASP.NET 页设置页面标题，即使在母版页中定义了 `<title>` 元素也是如此。 还可以使用 `Page.Title`以编程方式设置标题。 另请注意，母版页对样式表的引用（如 `Style.css`）会自动更新，以便它们可以在任何 ASP.NET 页上工作，而与 ASP.NET 页相对于母版页的目录无关。

切换到设计视图可以看到页面在浏览器中的显示方式。 请注意，在 "ASP.NET" 页的设计视图中，只有内容可编辑区域是可编辑的，在母版页中定义的非 ContentPlaceHolder 标记将灰显。

[!["ASP.NET" 页的 "设计" 视图显示可编辑区域和不可编辑区域](master-pages-and-site-navigation-vb/_static/image18.png)](master-pages-and-site-navigation-vb/_static/image17.png)

**图 7**： "ASP.NET" 页的 "设计" 视图显示可编辑区域和不可编辑区域（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image19.png)）

当浏览器访问 `Default.aspx` 页面时，ASP.NET 引擎会自动合并页面的母版页内容和 ASP。NET 的内容，并将合并的内容呈现到发送给请求浏览器的最终 HTML 中。 更新母版页的内容时，使用此母版页的所有 ASP.NET 页面将在下一次请求时将其内容 remerged 为新的母版页内容。 简而言之，母版页模型允许定义单一页面布局模板（母版页），其更改会立即反映在整个站点中。

## <a name="adding-additional-aspnet-pages-to-the-website"></a>向网站添加其他 ASP.NET 页面

让我们花点时间将其他 ASP.NET 页面存根添加到站点，最终将保存各种报告演示。 总共会有35个演示，而不是创建所有的存根页面，只需创建前几页即可。 由于还将有很多类别的演示，因此更好地管理演示添加类别的文件夹。 现在添加以下三个文件夹：

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

最后，添加新文件，如图8中的解决方案资源管理器所示。 添加每个文件时，请记住选中 "选择母版页" 复选框。

![添加以下文件](master-pages-and-site-navigation-vb/_static/image20.png)

**图 8**：添加以下文件

## <a name="step-2-creating-a-site-map"></a>步骤2：创建站点映射

管理包含多个页面的网站的难题之一是为访问者提供一种直接的方法来浏览网站。 首先，必须定义站点的导航结构。 接下来，必须将此结构转换为可导航的用户界面元素，例如菜单或痕迹导航。 最后，在将新页面添加到站点并删除现有页面之前，需要维护和更新整个流程。 在 ASP.NET 2.0 之前，开发人员自行负责创建网站的导航结构，对其进行维护，并将其转换为可导航的用户界面元素。 但对于 ASP.NET 2.0，开发人员可以利用非常灵活的内置站点导航系统。

ASP.NET 2.0 站点导航系统为开发人员提供了一种方法，用于定义站点地图，然后通过编程 API 访问此信息。 ASP.NET 附带了一个站点地图提供程序，该提供程序希望站点地图数据存储在以特定方式进行格式化的 XML 文件中。 但由于站点导航系统是在[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)的基础上构建的，因此可以对其进行扩展，以支持序列化站点地图信息的替代方法。 Jeff Prosise 的文章中，[你已在等待的 SQL 站点地图提供程序](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)演示了如何创建一个站点地图提供程序，用于将站点地图存储在 SQL Server 数据库中;另一种方法是[基于文件系统结构创建站点地图提供程序](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)。

但对于本教程，我们将使用 ASP.NET 2.0 附带的默认站点地图提供程序。 若要创建站点地图，只需右键单击 "解决方案资源管理器中的项目名称，选择" 添加新项 "，然后选择" 站点地图 "选项。 将名称保留为 "`Web.sitemap`"，然后单击 "添加" 按钮。

[![将网站图添加到你的项目](master-pages-and-site-navigation-vb/_static/image22.png)](master-pages-and-site-navigation-vb/_static/image21.png)

**图 9**：向项目添加站点地图（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image23.png)）

站点地图文件是一个 XML 文件。 请注意，Visual Studio 为站点地图结构提供 IntelliSense。 站点地图文件必须将 `<siteMap>` 节点作为根节点，该节点必须正好包含一个 `<siteMapNode>` 子元素。 首先 `<siteMapNode>` 元素可以包含任意数量的后代 `<siteMapNode>` 元素。

定义用于模拟文件系统结构的站点地图。 也就是说，为三个文件夹中的每个文件夹添加一个 `<siteMapNode>` 元素，为这些文件夹中的每个 ASP.NET 页面添加子 `<siteMapNode>` 元素，如下所示：

Web.sitemap

[!code-xml[Main](master-pages-and-site-navigation-vb/samples/sample4.xml)]

站点地图定义网站的导航结构，该结构是描述网站各个部分的层次结构。 `Web.sitemap` 中的每个 `<siteMapNode>` 元素都表示站点的导航结构中的一个部分。

[![站点地图表示分层导航结构](master-pages-and-site-navigation-vb/_static/image25.png)](master-pages-and-site-navigation-vb/_static/image24.png)

**图 10**：站点地图表示分层的导航结构（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image26.png)）

ASP.NET 通过 .NET Framework 的[站点地图类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)公开站点地图的结构。 此类具有一个 `CurrentNode` 属性，该属性返回有关用户当前访问的部分的信息;`RootNode` 属性返回站点图的根（在我们的站点图中）。 `CurrentNode` 和 `RootNode` 属性都返回[SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)实例，这些实例具有 `ParentNode`、`ChildNodes`、`NextSibling`、`PreviousSibling`等属性，从而允许遍历站点地图层次结构。

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>步骤3：基于站点地图显示菜单

访问 ASP.NET 2.0 中的数据可通过编程方式（如 ASP.NET 1.x）或通过新[数据源控件](https://msdn.microsoft.com/library/ms227679.aspx)以声明方式完成。 有几个内置的数据源控件，如 SqlDataSource 控件、用于访问关系数据库数据的数据源控件、ObjectDataSource 控件、用于从类访问数据的控件等。 你甚至可以创建自己的[自定义数据源控件](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)。

数据源控件充当 ASP.NET 页与基础数据之间的代理。 为了显示数据源控件检索到的数据，通常会将另一个 Web 控件添加到页面，并将其绑定到数据源控件。 若要将 Web 控件绑定到数据源控件，只需将 Web 控件的 `DataSourceID` 属性设置为数据源控件的 `ID` 属性的值。

为了帮助处理网站图的数据，ASP.NET 包含 SiteMapDataSource 控件，该控件允许我们将 Web 控件绑定到网站的网站图。 两个 Web 控件 TreeView 和菜单通常用于提供导航用户界面。 若要将站点地图数据绑定到这两个控件之一，只需将 SiteMapDataSource 添加到页面，并将其设置为 `DataSourceID` 属性的 TreeView 或 Menu 控件。 例如，我们可以使用以下标记向母版页添加菜单控件：

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample5.aspx)]

为了更好地控制发出的 HTML，我们可以将 SiteMapDataSource 控件绑定到 Repeater 控件，如下所示：

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample6.aspx)]

SiteMapDataSource 控件一次返回一个级别的站点地图层次结构，从根站点地图节点开始（在我们的站点映射中），然后是下一级别（基本报表、筛选报表和自定义格式设置）等。 将 SiteMapDataSource 绑定到中继器时，它会枚举返回的第一个级别，并实例化第一个级别中每个 `SiteMapNode` 实例的 `ItemTemplate`。 若要访问 `SiteMapNode`的特定属性，我们可以使用 `Eval(propertyName)`，这就是我们为每个 `SiteMapNode`的 `Url` 和 `Title` 属性获取 HyperLink 控件的方式。

上述中继器示例将呈现以下标记：

[!code-html[Main](master-pages-and-site-navigation-vb/samples/sample7.html)]

这些站点地图节点（基本报表、筛选报表和自定义格式设置）构成了呈现的*第二级*站点映射，而不是第一个。 这是因为 SiteMapDataSource 的 `ShowStartingNode` 属性设置为 False，导致 SiteMapDataSource 绕过根站点地图节点，而是首先返回站点地图层次结构中的第二个级别。

若要显示基本报表、筛选报表和自定义格式 `SiteMapNode` 的子节点，可以将另一个 Repeater 添加到初始 Repeater 的 `ItemTemplate`中。 此第二个 Repeater 将绑定到 `SiteMapNode` 实例的 `ChildNodes` 属性，如下所示：

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample8.aspx)]

这两个中继器会生成以下标记（为了简洁起见，已经删除了某些标记）：

[!code-html[Main](master-pages-and-site-navigation-vb/samples/sample9.html)]

使用从[Rachel Andrew](http://www.rachelandrew.co.uk/)的书籍中选择的 CSS 样式[css Anthology：101基本提示、技巧、&amp; 黑客](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance)、`<ul>` 和 `<li>` 元素的样式，以使标记产生以下视觉输出：

![由两个中继器和一些 CSS 组成的菜单](master-pages-and-site-navigation-vb/_static/image27.png)

**图 11**：由两个中继器和一些 CSS 组成的菜单

此菜单位于母版页中并绑定到 `Web.sitemap`中定义的站点图，这意味着对站点图的任何更改将立即反映在使用 `Site.master` 母版页的所有页面上。

## <a name="disabling-viewstate"></a>禁用 ViewState

所有 ASP.NET 控件都可以选择将其状态保存到[视图状态](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/)，该状态在呈现的 HTML 中序列化为隐藏的窗体字段。 视图状态由控件用来记住跨回发的以编程方式更改的状态，例如绑定到数据 Web 控件的数据。 当视图状态允许跨回发记住信息时，它会增加必须发送到客户端的标记的大小，并且如果未经过密切监视，则可能会导致严重页面膨胀。 对于将数十个额外的标记添加到页面中，数据 Web 控件（特别是 GridView）尤其棘手。 虽然宽带或 intranet 用户的此类增长可能会忽略不计，但对于拨号用户，视图状态可能会在往返行程中增加几秒钟。

若要查看视图状态的影响，请访问浏览器中的页面，然后查看网页发送的源（在 Internet Explorer 中，单击 "查看" 菜单，然后选择 "源" 选项）。 还可以打开[页面跟踪](https://msdn.microsoft.com/library/sfbfw58f.aspx)，查看页面上每个控件使用的视图状态分配。 视图状态信息在名为 `__VIEWSTATE`的隐藏窗体字段中序列化，该字段位于开始 `<form>` 标记后面的 `<div>` 元素中。 仅当使用 Web 窗体时才会保留视图状态;如果 ASP.NET 页在其声明性语法中不包含 `<form runat="server">`，则在呈现的标记中将不会有 `__VIEWSTATE` 的隐藏窗体字段。

母版页生成的 `__VIEWSTATE` 窗体字段向页面的生成标记添加大约1800字节。 由于 SiteMapDataSource 控件的内容将保留在视图状态中，因此这一额外的膨胀主要是在 Repeater 控件中。 尽管额外的1800字节可能并不太大，但在使用包含多个字段和记录的 GridView 时，视图状态可以通过10个或更多的因子轻松 swell。

可以通过将 `EnableViewState` 属性设置为 `False`来禁用页或控件级别的视图状态，从而减少所呈现标记的大小。 由于数据 Web 控件的视图状态会在每次回发时将绑定到数据 Web 控件的数据保持不变，因此，在为数据 Web 控件禁用视图状态时，必须在每个回发上绑定数据。 在 ASP.NET 版本1.x 中，此责任落在页面开发人员的需要肩负上;但对于 ASP.NET 2.0，数据 Web 控件将在每次回发时重新绑定到其数据源控件（如果需要）。

若要缩小页面的视图状态，请将 Repeater 控件的 `EnableViewState` 属性设置为 `False`。 可以通过设计器中的属性窗口或在源视图中以声明方式完成此操作。 做出此更改后，中继器的声明性标记应如下所示：

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample10.aspx)]

在此更改后，页面的呈现视图状态大小已缩小为仅52字节，而视图状态大小节省97%！ 在本系列教程中，我们默认禁用数据 Web 控件的视图状态，以便减小呈现的标记的大小。 在大多数示例中，`EnableViewState` 属性将设置为 `False` 并完成，而不提及。 只有在启用视图状态时，才会对其进行讨论，以便数据 Web 控件能够提供其预期功能。

## <a name="step-4-adding-breadcrumb-navigation"></a>步骤4：添加痕迹导航

若要完成母版页，请向每个页面添加一个痕迹导航 UI 元素。 痕迹导航会快速向用户显示其在站点层次结构中的当前位置。 在 ASP.NET 2.0 中添加痕迹只是将 SiteMapPath 控件添加到页面上;无需任何代码。

对于我们的站点，请将此控件添加到标头 `<div>`：

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample11.aspx)]

痕迹导航显示用户在站点图层次结构中访问的当前页面以及该站点地图节点的 "上级"，一直到根节点（位于我们的站点图中）。

![痕迹导航显示当前页及其在站点地图层次结构中的上级](master-pages-and-site-navigation-vb/_static/image28.png)

**图 12**：痕迹导航显示当前页及其在站点地图层次结构中的上级

## <a name="step-5-adding-the-default-page-for-each-section"></a>步骤5：为每个部分添加默认页面

我们的网站中的教程划分为不同类别的基本报告、筛选、自定义格式等，并使用每个类别的文件夹和相应教程作为该文件夹中的 ASP.NET 页面。 此外，每个文件夹都包含一个 `Default.aspx` 页面。 对于此默认页面，我们将显示当前部分的所有教程。 也就是说，对于 `BasicReporting` 文件夹中的 `Default.aspx`，我们需要链接到 `SimpleDisplay.aspx`、`DeclarativeParams.aspx`和 `ProgrammaticParams.aspx`。 接下来，我们可以使用 `SiteMap` 类和数据 Web 控件基于 `Web.sitemap`中定义的站点地图来显示此信息。

让我们再次使用中继器显示未排序的列表，但这次我们将显示教程的标题和说明。 由于用于实现此目的的标记和代码需要为每个 `Default.aspx` 页重复，因此，我们可以将此 UI 逻辑封装在[用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)中。 在名为 `UserControls` 的网站中创建一个文件夹，并添加到名为 `SectionLevelTutorialListing.ascx`的 Web 用户控件的新项，并添加以下标记：

[![将新的 Web 用户控件添加到 Usercontrol 文件夹](master-pages-and-site-navigation-vb/_static/image30.png)](master-pages-and-site-navigation-vb/_static/image29.png)

**图 13**：将新的 Web 用户控件添加到 `UserControls` 文件夹（[单击查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image31.png)）

SectionLevelTutorialListing.ascx

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.vb

[!code-vb[Main](master-pages-and-site-navigation-vb/samples/sample13.vb)]

在以前的中继器示例中，我们以声明方式将 `SiteMap` 数据绑定到中继器;但 `SectionLevelTutorialListing` 用户控件以编程方式执行此操作。 在 `Page_Load` 事件处理程序中，将进行检查以确保此页的 URL 映射到站点地图中的节点。 如果在没有相应 `<siteMapNode>` 条目的页面中使用此用户控件，`SiteMap.CurrentNode` 将返回 `Nothing`，并且不会将任何数据绑定到 Repeater。 假设我们有 `CurrentNode`，则将其 `ChildNodes` 集合绑定到中继器。 由于我们已设置了站点映射，因此每个部分中的 "`Default.aspx`" 页是该部分中所有教程的父节点，此代码将显示该部分教程的链接和说明，如以下屏幕截图所示。

创建此中继器后，打开每个文件夹中的 `Default.aspx` 页面，进入设计视图，只需将用户控件从解决方案资源管理器拖到要在其中显示教程列表的设计图面。

[![用户控件已添加到 default.aspx](master-pages-and-site-navigation-vb/_static/image33.png)](master-pages-and-site-navigation-vb/_static/image32.png)

**图 14**：已将用户控件添加到 `Default.aspx` （[单击查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image34.png)）

[![列出了基本报表教程](master-pages-and-site-navigation-vb/_static/image36.png)](master-pages-and-site-navigation-vb/_static/image35.png)

**图 15**：列出了基本报表教程（[单击以查看完全大小的图像](master-pages-and-site-navigation-vb/_static/image37.png)）

## <a name="summary"></a>摘要

定义站点地图并完成母版页后，我们为数据相关的教程提供了一致的页面布局和导航方案。 无论我们将多少页添加到我们的网站，更新站点范围的页面布局或站点导航信息都是一种快速而简单的过程，因为此信息是集中式的。 具体而言，页面布局信息在母版页 `Site.master` 中定义，并在 `Web.sitemap`中的站点映射中定义。 我们无需编写*任何*代码即可实现此站点范围的页面布局和导航机制，并在 Visual Studio 中保留完整的 WYSIWYG 设计器支持。

完成了数据访问层和业务逻辑层，并定义了一致的页面布局和站点导航后，就可以开始探索常见的报表模式了。 在接下来的三个教程中，我们将介绍显示从 GridView、DetailsView 和 FormView 控件中的 BLL 检索到的数据的基本报表任务。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 母版页概述](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [ASP.NET 2.0 中的母版页](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 设计模板](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET 站点导航概述](https://msdn.microsoft.com/library/e468hxky.aspx)
- [检查 ASP.NET 2.0 的站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 站点导航功能](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [了解 ASP.NET 视图状态](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [如何：为 ASP.NET 页启用跟踪](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET 用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Liz Shulok、Dennis Patterson 将和 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-a-business-logic-layer-vb.md)
