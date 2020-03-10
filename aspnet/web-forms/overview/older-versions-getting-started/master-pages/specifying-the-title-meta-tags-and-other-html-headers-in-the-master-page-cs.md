---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
title: 指定母版页中的标题、元标记和其他 HTML 标头（C#） |Microsoft Docs
author: rick-anderson
description: 查看用于在 "内容" 页中定义母版页中的 &lt;head&gt; 元素的不同技术。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 0aa1c84f-c9e2-4699-b009-0e28643ecbc6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: a4ec96a5b90f664655d554c064f9d50e76ad2d58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474530"
---
# <a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-c"></a>指定母版页中的标题、元标记和其他 HTML 标头 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_CS.zip)或[下载 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_CS.pdf)

> 查看用于在 "内容" 页中定义母版页中的 &lt;head&gt; 元素的不同技术。

## <a name="introduction"></a>简介

默认情况下，在 Visual Studio 2008 中创建的新母版页具有两个 ContentPlaceHolder 控件：一个名为 head，位于 `<head>` 元素中;并在 Web 窗体中放置一个名为 `ContentPlaceHolder1`。 `ContentPlaceHolder1` 的目的是在 Web 窗体中定义可以逐页自定义的区域。 `head` ContentPlaceHolder 使页面能够将自定义内容添加到 `<head>` 部分。 （当然，可以修改或删除这两个 Contentplaceholder，并且可能会向母版页添加其他 ContentPlaceHolder。 母版页 `Site.master`当前有四个 ContentPlaceHolder 控件。）

HTML `<head>` 元素充当有关不属于文档本身的网页文档的信息的存储库。 其中包括网页标题、搜索引擎或内部爬网程序使用的元信息，以及指向外部资源（如 RSS 源、JavaScript 和 CSS 文件）的链接。 其中的某些信息可能与网站中的所有页面相关。 例如，你可能希望为每个 ASP.NET 页全局导入相同的 CSS 规则和 JavaScript 文件。 但 `<head>` 元素的某些部分是页特定的。 页面标题是一个主要的示例。

在本教程中，我们将检查如何在母版页及其内容页中定义全局和特定于页的 `<head>` 节标记。

## <a name="examining-the-master-pagesheadsection"></a>检查母版页的`<head>`部分

Visual Studio 2008 创建的默认母版页文件在其 `<head>` 部分中包含以下标记：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample1.aspx)]

请注意，`<head>` 元素包含一个 `runat="server"` 属性，该属性指示它是服务器控件（而不是静态 HTML）。 所有 ASP.NET 页派生自 `System.Web.UI` 命名空间中的[`Page` 类](https://msdn.microsoft.com/library/system.web.ui.page.aspx)。 此类包含一个 `Header` 属性，该属性提供对页面的 `<head>` 区域的访问权限。 使用[`Header` 属性](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx)，我们可以设置 ASP.NET 页面的标题或向呈现的 `<head>` 部分添加其他标记。 然后，可以通过在页面的 `Page_Load` 事件处理程序中编写一段代码，自定义内容页的 `<head>` 元素。 我们检查如何以编程方式在步骤1中设置页面的标题。

上面 `<head>` 元素中所示的标记还包括一个名为 head 的 ContentPlaceHolder 控件。 此 ContentPlaceHolder 控件不是必需的，因为内容页可以通过编程方式将自定义内容添加到 `<head>` 元素。 但在内容页需要将静态标记添加到 `<head>` 元素的情况下很有用，因为可以通过声明方式将静态标记添加到相应的内容控件，而不是以编程方式添加。

除了 `<title>` 元素和 head ContentPlaceHolder 外，母版页的 `<head>` 元素应包含所有页面共有的所有 `<head>`级标记。 在我们的网站中，所有页面都使用 `Styles.css` 文件中定义的 CSS 规则。 因此，我们更新了 "[*使用母版页创建站点范围布局*](creating-a-site-wide-layout-using-master-pages-cs.md)" 教程中的 `<head>` 元素，以包含相应的 `<link>` 元素。 `Site.master` 母版页的当前 `<head>` 标记如下所示。

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>步骤1：设置内容页的标题

网页标题是通过 `<title>` 元素指定的。 必须将每个页面的标题设置为合适的值。 访问某个页面时，其标题将显示在浏览器的标题栏中。 此外，在为页面添加书签时，浏览器使用页面标题作为书签的建议名称。 另外，许多搜索引擎在显示搜索结果时显示页面的标题。

> [!NOTE]
> 默认情况下，Visual Studio 会将母版页中的 `<title>` 元素设置为 "无标题页"。 同样，新的 ASP.NET 页也将其 `<title>` 设置为 "无标题页"。 由于可能很容易忘记将页面的标题设置为适当的值，因此 Internet 上的多个页面的标题为 "无标题页"。 在 Google for 带有此标题的网页中，会返回大约2460000的结果。 即使 Microsoft 也容易发布标题为 "无标题页" 的网页。 撰写本文时，Google search 在 Microsoft.com 域中报告了236这样的网页。

ASP.NET 页可通过以下方式之一指定其标题：

- 通过将值直接置于 `<title>` 元素中
- 在 `<%@ Page %>` 指令中使用 `Title` 特性
- 使用 `Page.Title="title"` 或 `Page.Header.Title="title"`等代码以编程方式设置页面的 `Title` 属性。

内容页没有 `<title>` 元素，因为它是在母版页中定义的。 因此，若要设置内容页的标题，可以使用 `<%@ Page %>` 指令的 `Title` 特性，也可以通过编程方式进行设置。

### <a name="setting-the-pages-title-declaratively"></a>以声明方式设置页面标题

内容页的标题可通过[`<%@ Page %>` 指令](https://msdn.microsoft.com/library/ydy4x04a.aspx)的 `Title` 属性以声明方式进行设置。 可以通过直接修改 `<%@ Page %>` 指令或属性窗口来设置此属性。 让我们看看这两种方法。

从 "源" 视图中，找到 `<%@ Page %>` 指令，该指令位于页面的声明性标记的顶部。 `Default.aspx` 的 `<%@ Page %>` 指令如下：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample3.aspx)]

`<%@ Page %>` 指令指定 ASP.NET 引擎在分析和编译页面时使用的特定于页的属性。 这包括其母版页文件、其代码文件的位置及其标题以及其他信息。

默认情况下，在创建新的内容页时，Visual Studio 会将 `Title` 特性设置为无标题页。 将 `Default.aspx`的 `Title` 属性从 "无标题页面" 更改为 "母版页教程"，然后通过浏览器查看页面。 图1显示了浏览器的标题栏，其中反映了新的页面标题。

![现在，浏览器的标题栏显示 &quot;母版页教程&quot;，而不是 &quot;无标题页&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image1.png)

**图 01**：浏览器的标题栏现在显示 "母版页教程" 而不是 "无标题页"

还可以从属性窗口设置页的标题。 从 "属性窗口中，从下拉列表中选择" 文档 "以加载页面级属性，其中包括" `Title` "属性。 图2显示了 `Title` 设置为 "母版页教程" 后的属性窗口。

![你还可以从 "属性" 窗口配置标题。](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image2.png)

**图 02**：你也可以从 "属性" 窗口配置标题

### <a name="setting-the-pages-title-programmatically"></a>以编程方式设置页面标题

ASP.NET 引擎呈现页面时，母版页的 `<head runat="server">` 标记将转换为[`HtmlHead` 的类](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx)实例。 `HtmlHead` 类具有一个[`Title` 属性](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx)，其值在呈现的 `<title>` 元素中反映出来。 可以通过 `Page.Header.Title`从 ASP.NET 页的代码隐藏类访问此属性;还可以通过 `Page.Title`访问此同一属性。

若要以编程方式设置页面标题的设置，请导航到 `About.aspx` 页的代码隐藏类，并为该页的 `Load` 事件创建事件处理程序。 接下来，将页面的标题设置为 "母版页教程：： About：： *date*"，其中*date*为当前日期。 添加此代码后，`Page_Load` 事件处理程序应类似于以下内容：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample4.cs)]

图3显示了访问 `About.aspx` 页面时浏览器的标题栏。

![页面标题以编程方式设置并包含当前日期](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image3.png)

**图 03**：页面标题以编程方式设置并包含当前日期

## <a name="step-2-automatically-assigning-a-page-title"></a>步骤2：自动分配页面标题

如我们在步骤1中所述，可以通过声明方式或编程方式设置页面的标题。 但是，如果您忘记将标题显式更改为更具描述性的内容，则页面将具有默认标题 "无标题页"。 理想情况下，如果未显式指定其值，则会为我们自动设置页面的标题。 例如，如果在运行时页面的标题为 "无标题页"，我们可能希望将标题自动更新为与 ASP.NET 页的文件名相同。 好消息是，有一点前期工作就可以自动分配标题了。

所有 ASP.NET 网页均派生自 `System.Web.UI` 命名空间中的 `Page` 类。 `Page` 类定义 ASP.NET 页面所需的最少功能，并公开 `IsPostBack`、`IsValid`、`Request`和 `Response`等重要属性。 通常，web 应用程序中的每个页面都需要其他特性或功能。 提供此方法的一种常用方法是创建一个自定义基本页类。 自定义基本页类是您创建的类，该类派生自 `Page` 类并包含附加功能。 一旦创建了此基类，就可以让 ASP.NET 页面从其派生（而不是 `Page` 类），从而为 ASP.NET 页面提供扩展功能。

在此步骤中，我们将创建一个基本页，如果未显式设置标题，则会自动将该页面的标题设置为 ASP.NET 页的文件名。 步骤3介绍了如何根据站点地图设置页面标题。

> [!NOTE]
> 创建和使用自定义基类类的彻底检查超出了本系列教程的范围。 有关详细信息，请阅读将[自定义基类用于 ASP.NET 页面的代码隐藏类](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)。

### <a name="creating-the-base-page-class"></a>创建基本页类

我们的第一个任务是创建基类类，该类是一个扩展 `Page` 类的类。 首先，通过右键单击解决方案资源管理器中的项目名称，选择 "添加 ASP.NET" 文件夹，然后选择 "`App_Code`"，开始向项目添加 `App_Code` 文件夹。 接下来，右键单击 "`App_Code`" 文件夹，并添加名为 "`BasePage.cs`" 的新类。 图4显示了 `App_Code` 文件夹和 `BasePage.cs` 类添加后解决方案资源管理器。

![添加 App_Code 文件夹和名为 BasePage 的类](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image4.png)

**图 04**：添加 `App_Code` 文件夹和名为 `BasePage` 的类

> [!NOTE]
> Visual Studio 支持以下两种模式的项目管理：网站项目和 Web 应用程序项目。 `App_Code` 文件夹设计为与网站项目模型一起使用。 如果使用的是 Web 应用程序项目模型，请将 `BasePage.cs` 类放置在一个名为 "`App_Code`以外的文件夹，如 `Classes`"。 有关本主题的详细信息，请参阅将网站[项目迁移到 Web 应用程序项目](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)。

因为自定义基本页充当 ASP.NET 页的代码隐藏类的基类，所以它需要扩展 `Page` 类。

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample5.cs)]

每次请求 ASP.NET 页时，它都会经历一系列阶段，请求页中的 culminating 将呈现为 HTML。 可以通过重写 `Page` 类的 `OnEvent` 方法来利用阶段。 对于我们的基本页，如果未通过 `LoadComplete` 阶段显式指定标题，则会自动设置该标题（这在您可能已经猜到 `Load` 阶段后发生）。

若要实现此目的，请重写 `OnLoadComplete` 方法，并输入以下代码：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample6.cs)]

`OnLoadComplete` 方法首先确定 `Title` 属性是否尚未显式设置。 如果 `Title` 属性为 `null`，则为空字符串，或具有值 "无标题页"，则会将其分配给请求的 ASP.NET 页的文件名。 例如，可以通过 `Request.PhysicalPath` 属性访问请求的 ASP.NET 页 `C:\MySites\Tutorial03\Login.aspx`的物理路径。 `Path.GetFileNameWithoutExtension` 方法仅提取文件名部分，然后将此文件名分配给 `Page.Title` 属性。

> [!NOTE]
> 我邀请您增强这一逻辑，以改善标题的格式。 例如，如果 `Company-Products.aspx`页面的文件名，则上述代码将生成标题 "Company-Products"，但理想情况下，破折号会替换为空格，如 "公司产品" 中所示。 另外，请考虑在出现大小写更改时添加一个空格。 也就是说，请考虑添加代码，将文件名 `OurBusinessHours.aspx` 转换为 "我们的营业时间" 的标题。

### <a name="having-the-content-pages-inherit-the-base-page-class"></a>使内容页继承基本页类

现在，我们需要更新站点中的 ASP.NET 页面，使其从自定义基本页（`BasePage`）而不是 `Page` 类派生。 若要完成此操作，请转到每个代码隐藏类，并从以下位置更改类声明：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample7.cs)]

到:

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample8.cs)]

完成此操作后，通过浏览器访问站点。 如果访问其标题被显式设置的页面（如 `Default.aspx` 或 `About.aspx`），则使用显式指定的标题。 但是，如果您访问其标题尚未从默认值（"无标题页"）更改的页，则基本页类会将标题设置为该页的文件名。

图5显示了通过浏览器查看 `MultipleContentPlaceHolders.aspx` 页面。 请注意，标题正好是页面的文件名（更少扩展名），"MultipleContentPlaceHolders"。

[![如果未显式指定标题，则自动使用页面的文件名](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image5.png)

**图 05**：如果未显式指定标题，则自动使用页面的文件名（[单击以查看完全大小的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image7.png)）

## <a name="step-3-basing-the-page-title-on-the-site-map"></a>步骤3：在站点图上基于页面标题

ASP.NET 提供了一个强大的站点地图框架，使页面开发人员能够在外部资源（如 XML 文件或数据库表）中定义一个层次结构的站点地图，并提供 Web 控件以显示有关站点地图的信息（例如 SiteMapPath）。菜单和 TreeView 控件）。

还可以从 ASP.NET 页的代码隐藏类以编程方式访问站点地图结构。 通过这种方式，我们可以自动将页面标题设置为站点地图中其对应节点的标题。 让我们来增强在步骤2中创建的 `BasePage` 类，使其提供此功能。 但首先我们需要为站点创建一个站点图。

> [!NOTE]
> 本教程假定读者已经熟悉 ASP。净地图功能。 有关使用站点地图的详细信息，请参阅我的多部分文章系列，[检查 ASP。网络导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)。

### <a name="creating-the-site-map"></a>创建站点地图

站点地图系统是在[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)的上方构建的，后者将站点地图 API 与在内存和永久存储之间序列化站点地图信息的逻辑分离。 .NET Framework 附带了[`XmlSiteMapProvider` 类](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)，这是默认的站点地图提供程序。 顾名思义，`XmlSiteMapProvider` 使用 XML 文件作为其站点地图存储区。 让我们使用此提供程序来定义我们的网站图。

首先在网站的根文件夹中创建一个名为 "`Web.sitemap`" 的站点映射文件。 若要实现此目的，请在解决方案资源管理器中右键单击网站名称，选择 "添加新项"，然后选择 "站点地图" 模板。 确保该文件命名为 "`Web.sitemap`"，然后单击 "添加"。

[![将名为 web.sitemap 的文件添加到网站的根文件夹中](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image8.png)

**图 06**：将名为 `Web.sitemap` 的文件添加到网站的根文件夹（[单击查看完全大小的映像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image10.png)）

将以下 XML 添加到 `Web.sitemap` 文件：

[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample9.xml)]

此 XML 定义图7中所示的层次结构站点地图结构。

![站点地图当前由三个站点地图节点组成](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image11.png)

**图 07**：站点地图当前由三个站点地图节点组成

我们将在将来的教程中更新站点地图结构，因为我们添加了新的示例。

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>更新母版页以包含导航 Web 控件

现在我们已定义了一个站点地图，接下来请更新母版页，使其包含导航 Web 控件。 具体而言，让我们将 "ListView" 控件添加到 "课程" 部分中的左栏，该部分将呈现一个无序列表，其中包含站点地图中定义的每个节点的列表项。

> [!NOTE]
> ListView 控件是 ASP.NET 版本3.5 的新控件。 如果使用的是早期版本的 ASP.NET，请改用 Repeater 控件。 有关 ListView 控件的详细信息，请参阅[Using ASP.NET 3.5 的 ListView 和 DataPager 控件](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)。

首先从课程部分删除现有的无序列表标记。 接下来，将 "ListView" 控件从 "工具箱" 拖放到课程标题的下方。 ListView 位于工具箱的 "数据" 部分，另一个视图控件与其他视图控件相同： GridView、DetailsView 和 FormView。 将 ListView 的 ID 属性设置为 `LessonsList`。

从 "数据源配置向导" 中，选择将 ListView 绑定到名为 `LessonsDataSource`的新 SiteMapDataSource 控件。 SiteMapDataSource 控件从站点地图系统返回层次结构。

[![将 SiteMapDataSource 控件绑定到 LessonsList ListView 控件](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image12.png)

**图 08**：将 SiteMapDataSource 控件绑定到 `LessonsList` ListView 控件（[单击以查看完全大小的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image14.png)）

创建 SiteMapDataSource 控件后，需要定义 ListView 的模板，使其为 SiteMapDataSource 控件返回的每个节点呈现一个列表项。 可使用以下模板标记完成此操作：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample10.aspx)]

`LayoutTemplate` 为无序列表（`<ul>...</ul>`）生成标记，而 `ItemTemplate` 将 SiteMapDataSource 返回的每个项呈现为包含指向特定课程的链接的列表项（`<li>`）。

配置 ListView 的模板后，请访问网站。 如图9所示，"课程" 部分包含一个项目符号项 Home。 在哪里可以使用多个 ContentPlaceHolder 控件课程？ SiteMapDataSource 旨在返回分层的数据集，但 ListView 控件只能显示层次结构的一个级别。 因此，只显示 SiteMapDataSource 返回的第一级站点地图节点。

[![课程部分包含单个列表项](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image15.png)

**图 09**：课程部分包含单个列表项（[单击以查看完全大小的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image17.png)）

若要显示多个级别，可以在 `ItemTemplate`中嵌套多个 Listview。 本技术在[*母版页和*](../../data-access/introduction/master-pages-and-site-navigation-cs.md)使用[数据教程系列](../../data-access/index.md)的站点导航教程中进行了检查。 但是，在本教程系列中，我们的网站图只包含两个级别：主页（顶层）;并且每个课程都作为 Home 的子项。 我们可以通过将 SiteMapDataSource[属性`ShowStartingNode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)设置为 `false`来指示不返回起始节点，而不是手工编写嵌套的 ListView。 最终效果是，SiteMapDataSource 首先返回站点地图节点的第二层。

进行此更改后，ListView 将显示关于和使用多个 ContentPlaceHolder 控件课程的项目符号项，但省略 Home 的项目符号项。 若要解决此情况，可以在 `LayoutTemplate`中为 Home 显式添加项目符号项：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample11.aspx)]

通过将 SiteMapDataSource 配置为省略开始节点并显式添加 Home 项目符号项，"课程" 部分现在会显示预期的输出。

[![课程部分包含 Home 和每个子节点的项目符号项](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image18.png)

**图 10**： "课程" 部分包含 "主页" 和每个子节点的项目符号项（[单击以查看完全大小的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image20.png)）

### <a name="setting-the-title-based-on-the-site-map"></a>基于站点地图设置标题

站点映射到位后，可将 `BasePage` 类更新为使用在站点图中指定的标题。 正如我们在步骤2中所做的那样，如果页面的标题尚未由页面开发人员显式设置，则我们只希望使用 "站点地图" 节点的标题。 如果请求的页面没有显式设置的页面标题，并且在站点映射中找不到，则我们将回退到使用请求的页面的文件名（较少扩展名），就像我们在步骤2中所做的那样。 图11说明了此决策过程。

![如果没有显式设置的页面标题，则使用相应的网站地图节点的标题](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image21.png)

**图 11**：在没有显式设置页面标题的情况下，将使用相应的网站地图节点的标题

更新 `BasePage` 类的 `OnLoadComplete` 方法以包含以下代码：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample12.cs)]

与之前一样，`OnLoadComplete` 方法首先确定是否已显式设置页面的标题。 如果 `Page.Title` `null`，则为空字符串，或者为其分配值 "无标题页"，则代码会自动将一个值分配给 `Page.Title`。

若要确定要使用的标题，代码首先引用[`SiteMap` 类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)的[`CurrentNode` 属性](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)。 `CurrentNode` 返回站点地图中对应于当前请求的页面的[`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)实例。 假设当前请求的页面在站点地图中找到，则 `SiteMapNode`的 `Title` 属性分配给页面的标题。 如果当前请求的页不在站点地图中，`CurrentNode` 将返回 `null`，并且将请求的页的文件名用作标题（如步骤2中所述）。

图12显示了通过浏览器查看 `MultipleContentPlaceHolders.aspx` 页面。 由于未显式设置此页面的标题，因此改用其对应的站点地图节点的标题。

![从站点地图中提取 MultipleContentPlaceHolders 页的标题](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image22.png)

**图 12**：从站点地图请求 `MultipleContentPlaceHolders.aspx` 页面的标题

## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>步骤4：将其他特定于页的标记添加到`<head>`节

步骤1、2和3查看逐页自定义 `<title>` 元素。 除了 `<title>`之外，`<head>` 部分可能包含 `<meta>` 元素和 `<link>` 元素。 如本教程前面所述，`Site.master`的 `<head>` 部分包含要 `Styles.css`的 `<link>` 元素。 由于此 `<link>` 元素在母版页中定义，因此它包含在所有内容页的 `<head>` 部分中。 但我们如何逐页地添加 `<meta>` 和 `<link>` 元素呢？

向 `<head>` 部分添加特定于页面的内容的最简单方法是在母版页中创建 ContentPlaceHolder 控件。 我们已经有了这样的 ContentPlaceHolder （名为 `head`）。 因此，若要添加自定义 `<head>` 标记，请在页面中创建相应的内容控件，并将标记放在此处。

为了说明如何向页面中添加自定义 `<head>` 标记，我们将向我们的当前内容页集提供 `<meta>` 的说明元素。 `<meta>` description 元素提供了有关网页的简要说明;大多数搜索引擎在显示搜索结果时将此信息以某种形式纳入。

`<meta>` description 元素具有以下格式：

[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample13.html)]

若要将此标记添加到内容页，请将以上文本添加到映射到母版页头 ContentPlaceHolder 的内容控件中。 例如，若要定义 `Default.aspx`的 `<meta>` description 元素，请添加以下标记：

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample14.aspx)]

由于 head ContentPlaceHolder 不在 HTML 页的正文中，因此添加到内容控件的标记不会显示在设计视图中。 若要查看 `<meta>` description 元素，请通过浏览器 `Default.aspx` 访问。 加载页面后，请查看源，并注意 "`<head>`" 部分包括内容控件中指定的标记。

请花点时间将 `<meta>` 说明元素添加到 `About.aspx`、`MultipleContentPlaceHolders.aspx`和 `Login.aspx`。

### <a name="programmatically-adding-markup-to-theheadregion"></a>以编程方式将标记添加到`<head>`区域

Head ContentPlaceHolder 允许我们以声明方式向母版页的 `<head>` 区域添加自定义标记。 还可以通过编程方式添加自定义标记。 请记住，`Page` 类的 `Header` 属性返回在母版页中定义的 `HtmlHead` 实例（`<head runat="server">`）。

当要添加的内容为动态时，能够以编程方式向 `<head>` 区域添加内容非常有用。 它可能基于访问该页的用户，可能是从数据库中提取的。 无论出于何种原因，你都可以通过将控件添加到控件集合来向 `HtmlHead` 添加内容，如下所示：

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample15.cs)]

上面的代码将 `<meta>` 关键字元素添加到 `<head>` 区域中，该区域提供了用逗号分隔的描述页面的关键字列表。 请注意，若要添加 `<meta>` 标记，请创建[`HtmlMeta`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx)实例，设置其 `Name` 和 `Content` 属性，然后将其添加到 `Header`的 `Controls` 集合中。 同样，若要以编程方式添加 `<link>` 元素，请创建[`HtmlLink`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx)对象，设置其属性，然后将其添加到 `Header`的 `Controls` 集合。

> [!NOTE]
> 若要添加任意标记，请创建[`LiteralControl`](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx)实例，设置其 `Text` 属性，然后将其添加到 `Header`的 `Controls` 集合。

## <a name="summary"></a>摘要

在本教程中，我们将介绍多种方法来逐页添加 `<head>` 区域标记。 母版页应该包含具有 ContentPlaceHolder 的 `HtmlHead` 实例（`<head runat="server">`）。 `HtmlHead` 实例允许内容页以编程方式访问 `<head>` 区域，并以声明方式和编程方式设置页面的标题;ContentPlaceHolder 控件允许通过内容控件以声明方式将自定义标记添加到 `<head>` 部分。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [在 ASP.NET 中动态设置页面的标题](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [正在检查 ASP。网络站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [如何使用 HTML Meta 标记](http://searchenginewatch.com/showPage.html?page=2167931)
- [ASP.NET 中的母版页](http://www.odetocode.com/articles/419.aspx)
- [使用 ASP.NET 3.5 的 ListView 和 DataPager 控件](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [为 ASP.NET 页的代码隐藏类使用自定义基类](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Zack 的 Suchi Banerjee。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](multiple-contentplaceholders-and-default-content-cs.md)
> [下一页](urls-in-master-pages-cs.md)
