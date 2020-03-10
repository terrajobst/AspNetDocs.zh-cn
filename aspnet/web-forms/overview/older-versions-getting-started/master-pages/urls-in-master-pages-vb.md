---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-vb
title: 母版页中的 Url （VB） |Microsoft Docs
author: rick-anderson
description: 解决母版页中的 Url 如何中断，因为母版页文件与内容页在不同的相对目录中。 查看变基 。
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 43d1e83c-0092-4dcf-977c-e709c4dce7c3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 01627988f68bb619969a5fe3cfaae68fe70b5d4f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441104"
---
# <a name="urls-in-master-pages-vb"></a>母版页中的 URL (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_VB.zip)或[下载 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_VB.pdf)

> 解决母版页中的 Url 如何中断，因为母版页文件与内容页在不同的相对目录中。 在声明性语法中通过 ~ 查看变基 Url，并以编程方式使用 ResolveUrl 和 ResolveClientUrl。 （同时查看

## <a name="introduction"></a>简介

在我们目前已看到的所有示例中，母版页和内容页面都位于同一个文件夹（网站的根文件夹）中。 但这并不是因为主页面和内容页必须在同一文件夹中。 当然，你可以在子文件夹中创建内容页。 同样，您也可以创建一个 `~/MasterPages/` 文件夹来放置站点的母版页。

将母版页和内容页面置于不同文件夹中的一个潜在问题涉及到一些断开的 Url。 如果母版页在超链接、图像或其他元素中包含相对 Url，则该链接将对于驻留在其他文件夹中的内容页无效。 在本教程中，我们将探讨此问题的根源以及解决方法。

## <a name="the-problem-with-relative-urls"></a>相对 Url 的问题

如果网页上指向的资源的位置相对于网站的文件夹结构中网页的位置，则该网页上的 URL 称为*相对 url* 。 不以前导正斜杠（`/`）或协议（如 `http://`）开头的任何 URL 是相对的，因为浏览器会根据包含 URL 的网页的位置对其进行解析。

例如，我们的网站有一个 `~/Images/` 文件夹，其中包含一个图像文件，`PoweredByASPNET.gif`。 母版页文件 `Site.master` 在 `footerContent` 区域中有一个 `<img>` 元素，该元素具有以下标记：

[!code-html[Main](urls-in-master-pages-vb/samples/sample1.html)]

`<img>` 元素中的 `src` 属性值是相对 URL，因为它不以 `/` 或 `http://`开头。 简而言之，`src` 属性值通知浏览器在 `Images` 子文件夹中查找名为 "`PoweredByASPNET.gif`" 的文件。

在访问内容页时，上述标记将直接发送到浏览器。 请花点时间访问 `About.aspx` 并查看发送到浏览器的 HTML 源。 您会发现，母版页中的标记完全相同。

[!code-html[Main](urls-in-master-pages-vb/samples/sample2.html)]

如果内容页位于根文件夹中（如 `About.aspx`），则一切都按预期方式运行，因为相对于根文件夹有一个 `Images` 子文件夹。 但是，如果内容页与母版页不在同一文件夹中，则会中断。 为了说明这一点，请创建一个名为 `Admin`的子文件夹。 接下来，将名为 `Default.aspx` 的内容页添加到 `Admin` 文件夹，并确保将新页绑定到 `Site.master` 母版页。

> [!NOTE]
> 在母版页教程的 "[*指定标题、Meta 标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)" 中，我们创建了一个名为 `BasePage` 的自定义基类类，该页面类自动设置内容页的标题（如果未显式分配）。 别忘了，新创建的页的代码隐藏类派生自 `BasePage` 以便它可以利用此功能。

创建此内容页后，解决方案资源管理器应类似于图1。

![已向项目添加了一个新文件夹和 ASP.NET 页](urls-in-master-pages-vb/_static/image1.png)

**图 01**：已将新文件夹和 ASP.NET 页添加到项目中

接下来，更新 `Web.sitemap` 文件，为本课添加新的 `<siteMapNode>` 条目。 下面的 XML 演示完整的 `Web.sitemap` 标记，该标记现在包含第三个 `<siteMapNode>` 元素的加法。

[!code-xml[Main](urls-in-master-pages-vb/samples/sample3.xml)]

新创建的 `Default.aspx` 页应具有四个与 `Site.master`中的四个 Contentplaceholder 相对应的内容控件。 向引用 `MainContent` ContentPlaceHolder 的内容控件添加一些文本，然后通过浏览器访问该页面。 如图2所示，浏览器找不到 `PoweredByASPNET.gif` 的图像文件。 这是怎么回事？

与 `About.aspx` 页面一样，为 `footerContent` 区域发送 `~/Admin/Default.aspx` 内容页：

[!code-html[Main](urls-in-master-pages-vb/samples/sample4.html)]

由于 `<img>` 元素的 `src` 属性是相对 URL，因此浏览器将尝试查找相对于网页文件夹位置的 `Images` 文件夹。 换句话说，浏览器正在查找 `Admin/Images/PoweredByASPNET.gif`的图像文件。

[![找不到 PoweredByASPNET 映像文件](urls-in-master-pages-vb/_static/image3.png)](urls-in-master-pages-vb/_static/image2.png)

**图 02**：找不到 `PoweredByASPNET.gif` 图像文件（[单击以查看完全大小的映像](urls-in-master-pages-vb/_static/image4.png)）

### <a name="replacing-relative-urls-with-absolute-urls"></a>用绝对 Url 替换相对 Url

相对 URL 的相对 URL 是*绝对 url*，该 url 以正斜杠（`/`）或协议（如 `http://`）开头。 由于绝对 URL 指定了资源在已知的固定点的位置，因此，无论网页在网站的文件夹结构中的位置如何，同一绝对 URL 在任何网页中都有效。

若要更正图2中所示的损坏图像，需要更新 `<img>` 元素的 `src` 属性，使其使用绝对 URL 而不是相对 URL。 若要确定正确的绝对 URL，请访问网站中的网页之一，然后检查地址栏。 图2中的地址栏显示了 web 应用程序的完全限定路径 `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_VB/`。 因此，我们可以将 `<img>` 元素的 `src` 属性更新为以下两个绝对 Url 之一：

- `/ASPNET_MasterPages_Tutorial_04_VB/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_VB/Images/PoweredByASPNET.gif`

请花点时间使用上面所示的窗体之一将 `<img>` 元素的 `src` 属性更新为绝对 URL，然后通过浏览器访问 `~/Admin/Default.aspx` 页面。 这次，浏览器将正确查找并显示 `PoweredByASPNET.gif` 图像文件（请参阅图3）。

[![PoweredByASPNET 图像现在显示](urls-in-master-pages-vb/_static/image6.png)](urls-in-master-pages-vb/_static/image5.png)

**图 03**：此时将显示 `PoweredByASPNET.gif` 图像（[单击以查看完全大小的图像](urls-in-master-pages-vb/_static/image7.png)）

虽然绝对 URL 中的硬编码工作正常，但它会将 HTML 紧密耦合到网站的服务器和文件夹位置，这可能会发生变化。 使用形式 `http://localhost:3908/...` 的绝对 URL 是脆弱的，因为每次启动 Visual Studio 的内置 ASP.NET 开发 Web 服务器时，会自动选择 localhost 前面的端口号。 同样，`http://localhost` 部分仅在本地测试时才有效。 将代码部署到生产服务器后，URL 基准将更改为其他内容，如 `http://www.yourserver.com`。 格式 `/ASPNET_MasterPages_Tutorial_04_VB/...` 的绝对 URL 也会受到相同的易受攻击，因为这种应用程序的路径在开发和生产服务器之间是不同的。

好消息是，ASP.NET 提供了一个方法，用于在运行时生成有效的相对 URL。

## <a name="usingandresolveclienturl"></a>使用`~`和`ResolveClientUrl`

ASP.NET 使页面开发人员可以使用波形符（`~`）指示 web 应用程序的根，而不是硬编码为绝对 URL。 例如，在本教程的前面部分，我使用了文本中的表示法 `~/Admin/Default.aspx` 引用 `Admin` 文件夹中的 `Default.aspx` 页。 `~` 指示 `Admin` 文件夹是 web 应用程序的根的子文件夹。

`Control` 类的[`ResolveClientUrl` 方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx)采用 URL，并将其修改为适用于控件所在网页的相对 URL。 例如，从 `About.aspx` 调用 `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` 会返回 `Images/PoweredByASPNET.gif`。 但从 `~/Admin/Default.aspx`调用它将返回 `./Images/PoweredByASPNET.gif`。

> [!NOTE]
> 由于所有 ASP.NET 服务器控件都派生自 `Control` 类，因此所有服务器控件都有权访问 `ResolveClientUrl` 方法。 即使 `Page` 类派生自 `Control` 类，这意味着你可以直接从 ASP.NET 页面的代码隐藏类使用此方法。

### <a name="usingin-the-declarative-markup"></a>在声明性标记中使用`~`

几个 ASP.NET Web 控件包括 URL 相关的属性： HyperLink 控件具有 `NavigateUrl` 属性;图像控件具有 `ImageUrl` 属性;依此类推。 呈现时，这些控件将与 URL 相关的属性值传递到 `ResolveClientUrl`。 因此，如果这些属性包含用于指示 web 应用程序的根的 `~`，则 URL 将修改为有效的相对 URL。

请记住，只有 ASP.NET 服务器控件才能转换其 URL 相关属性中的 `~`。 如果 `~` 出现在静态 HTML 标记中，如 `<img src="~/Images/PoweredByASPNET.gif" />`，则 ASP.NET 引擎会将 `~` 连同 HTML 内容的其余部分一起发送到浏览器。 浏览器假定 `~` 是 URL 的一部分。 例如，如果浏览器收到标记 `<img src="~/Images/PoweredByASPNET.gif" />` 它假定存在一个名为 `~` 的子文件夹，该子文件夹 `Images` 包含图像文件 `PoweredByASPNET.gif`。

若要修复 `Site.master`中的图像标记，请使用 ASP.NET 图像 Web 控件替换现有的 `<img>` 元素。 将图像 Web 控件的 `ID` 设置为 `PoweredByImage`，其 `ImageUrl` 属性设置为 `~/Images/PoweredByASPNET.gif`，并将其 `AlternateText` 属性设置为 "ASP.NET！"

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample5.aspx)]

对母版页进行此更改后，再次重新访问 `~/Admin/Default.aspx` 页。 这次 `PoweredByASPNET.gif` 图像文件将显示在页面中（请参阅图3）。 呈现图像 Web 控件时，将使用 `ResolveClientUrl` 方法解析其 `ImageUrl` 属性值。 在 `~/Admin/Default.aspx` 会将 `ImageUrl` 转换为相应的相对 URL，如 HTML 源的以下代码片段所示：

[!code-html[Main](urls-in-master-pages-vb/samples/sample6.html)]

> [!NOTE]
> 除了在基于 URL 的 Web 控件属性中使用以外，还可以在调用 `Response.Redirect` 和 `Server.MapPath` 方法时使用 `~`。 此外，如果需要，还可以从 ASP.NET 或母版页的声明性标记中直接调用 `ResolveClientUrl` 方法;请参阅[Fritz 绘图纸](https://www.pluralsight.com/blogs/fritz/)的博客文章[，使用标记中的 `ResolveClientUrl`](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)。

## <a name="fixing-the-master-pages-remaining-relative-urls"></a>修复母版页的其余相对 Url

除了我们刚刚修复的 `footerContent` 中的 `<img>` 元素外，母版页包含一个需要我们注意的相对 URL。 `topContent` 区域包括指向 `Default.aspx`的链接 "母版页教程"。

[!code-html[Main](urls-in-master-pages-vb/samples/sample7.html)]

由于此 URL 是相对的，因此它会将用户发送到他们所访问的内容页文件夹中的 "`Default.aspx`" 页。 若要使此链接始终指向根文件夹中的 `Default.aspx`，需要将 `<a>` 元素替换为超链接 Web 控件，以便我们可以使用 `~` 表示法。

删除 `<a>` 元素标记并在其位置添加超链接控件。 将超链接的 `ID` 设置为 `lnkHome`，其 `NavigateUrl` 属性设置为 `~/Default.aspx`，并将其 `Text` 属性设置为 "母版页教程"。

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample8.aspx)]

就这么简单！ 此时，无论母版页和内容页面位于哪个文件夹，都可以根据内容页面呈现母版页中的所有 Url。

### <a name="automatic-url-resolution-in-theheadsection"></a>`<head>`部分中的自动 URL 解析

在[*使用母版页创建站点范围布局*](creating-a-site-wide-layout-using-master-pages-vb.md)教程中，我们在 `<head>` 区域中的 `Styles.css` 文件中添加了 `<link>`：

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample9.aspx)]

虽然 `<link>` 元素的 `href` 属性是相对的，但它会在运行时自动转换为相应的路径。 正如我们在母版页教程中[*指定标题、元标记和其他 HTML 标题*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)中所述，`<head>` 区域实际上是服务器端控件，它使其能够在呈现时修改其内部控件的内容。

若要验证这一点，请重新访问 `~/Admin/Default.aspx` 页面，并查看发送到浏览器的 HTML 源。 如下面的代码段所示，`<link>` 元素的 `href` 属性已自动修改为适当的相对 URL，`./Styles.css`。

[!code-html[Main](urls-in-master-pages-vb/samples/sample10.html)]

## <a name="summary"></a>摘要

母版页通常包含链接、图像和其他必须通过 URL 指定的外部资源。 由于同一文件夹中可能不存在母版页和内容页，因此 abstain 使用相对 Url 很重要。 尽管可以使用硬编码的绝对 Url，但这样做会将绝对 URL 紧密耦合到 web 应用程序。 如果绝对 URL 发生更改，则在移动或部署 web 应用程序时通常会发生更改-您必须记得返回并更新绝对 Url。

理想的方法是使用波形符（`~`）来指示应用程序根目录。 包含与 URL 相关的属性的 ASP.NET Web 控件在运行时将 `~` 映射到应用程序根目录。 在内部，Web 控件使用 `Control` 类的 `ResolveClientUrl` 方法来生成有效的相对 URL。 此方法是公共的，可从每个服务器控件（包括 `Page` 类）使用，因此，如果需要，你可以从代码隐藏类以编程方式使用它。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 中的母版页](http://www.odetocode.com/Articles/419.aspx)
- [母版页中的 URL 变基](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [在标记中使用 `ResolveClientUrl`](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
> [下一页](control-id-naming-in-content-pages-vb.md)
