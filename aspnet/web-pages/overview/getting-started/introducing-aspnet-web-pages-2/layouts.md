---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: 介绍 ASP.NET 网页-创建一致的布局 |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍如何使用布局为使用 ASP.NET 网页的站点上的页面创建一致的外观。 它假定您已完成 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422744"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>简介 ASP.NET 网页-创建一致的布局

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程介绍如何使用*布局*为使用 ASP.NET 网页的站点上的页面创建一致的外观。 假设已[在 ASP.NET 网页中通过删除数据库数据](https://go.microsoft.com/fwlink/?LinkId=251584)完成了序列。
> 
> 学习内容：
> 
> - 布局页的含义。
> - 如何将布局页与动态内容组合在一起。
> - 如何将值传递到布局页。

## <a name="about-layouts"></a>关于布局

到目前为止，已经完成了所有独立页面。 它们全都属于同一站点，但它们没有任何常见的元素或标准的外观。

大多数站点都具有一致的外观和布局。 例如，如果你访问[Microsoft.com/web](https://www.microsoft.com/web/)站点并进行查找，你会看到这些页面都遵循整体布局和视觉主题：

![显示标头、导航区域、内容区域和页脚布局的 Microsoft.com/web 网站页面](layouts/_static/image1.png)

创建此布局的*低效*方法是在每个页面上分别定义标题、导航栏和页脚。 每次都要复制相同的标记。 如果要更改某些内容（例如，更新页脚），则必须单独更改每个页面。

这就是*布局页面*的位置。 在 ASP.NET 网页中，可以定义为网站上的页面提供总体容器的布局页面。 例如，"布局" 页可以包含页眉、导航区和页脚。 "布局" 页包含一个占位符，其中包含主要内容。

然后，可以定义单独的内容页，其中只包含该页的标记和代码。 内容页面不必是完整的 HTML 页面;它们甚至不必有 `<body>` 元素。 它们还具有一行代码，告诉 ASP.NET 要在其中显示内容的布局页。 下面的图片显示了此关系的具体工作原理：

![显示两个内容页以及它们适用的布局页的概念图](layouts/_static/image2.png)

当你在操作中看到此交互时，可以轻松理解这种交互。 在本教程中，你将更改电影页面以使用布局。

## <a name="adding-a-layout-page"></a>添加布局页

首先创建一个布局页面，用于定义具有页眉、页脚和主要内容区域的典型页面布局。 在 WebPagesMovies 网站中，添加一个名为 *\_* 的 CSHTML 页面。

前导下划线（`_`）字符很重要。 如果页的名称以下划线开头，则 ASP.NET 不会直接将该页发送到浏览器。 此约定允许您定义站点所需的页面，但用户不能直接请求。

将页面中的内容替换为以下内容：

[!code-html[Main](layouts/samples/sample1.html)]

如您所见，此标记只是 HTML，它使用 `<div>` 元素来定义页面中的三个节，另外还有一个 `<div>` 元素用来保存这三个部分。 页脚包含一小段代码： `@DateTime.Now.Year`，它将在页面的该位置呈现当前年份。

请注意，有一个指向样式表的链接，*其名称为 ""。* 样式表将定义元素的物理布局的详细信息。 稍后你将创建它。

此 *\_布局*`@Render.Body()` 中唯一的一项功能是行。 这是在此布局与另一个页面合并时内容将移到的占位符。

## <a name="adding-a-css-file"></a>添加 .css 文件

定义页上元素的实际排列（即外观）的首选方法是使用级联样式表（CSS）规则。 因此，你将创建一个包含新布局规则的 *.css*文件。

在 WebMatrix 中，选择你的站点的根目录。 然后，在功能区的 "**文件**" 选项卡中，单击 "**新建**" 按钮下的箭头，然后单击 "**新建文件夹**"。

![功能区中的 "新建" 下面的 "新建文件夹" 选项。](layouts/_static/image3.png)

将新文件夹命名为*样式*。

![命名新文件夹 "样式"](layouts/_static/image4.png)

在 "新建*样式*" 文件夹中，*创建名为 "" 的文件*。

![创建新的电影 .css 文件](layouts/_static/image5.png)

将新 *.css*文件的内容替换为以下内容：

[!code-css[Main](layouts/samples/sample2.css)]

除了说明两个情况外，我们不会涉及到这些 CSS 规则。 其中一种做法是：除了设置字体和大小以外，规则还使用绝对定位来确定页眉、页脚和主要内容区域的位置。 如果你不熟悉 CSS 中的定位，可以在 W3Schools 网站上阅读[Css 定位](http://www.w3schools.com/css/css_positioning.asp)教程。

需要注意的另一点是，在底部，我们复制了最初在 "*电影. cshtml* " 文件中单独定义的样式规则。 [通过使用 ASP.NET 网页](https://go.microsoft.com/fwlink/?LinkId=251580)教程使向表添加条纹的 `WebGrid` 帮助程序呈现标记，在介绍中使用了这些规则。 （如果要为样式定义使用 *.css*文件，则也可以将整个网站的样式规则放在一起。）

## <a name="updating-the-movies-file-to-use-the-layout"></a>更新影片文件以使用布局

现在，你可以更新站点中的现有文件，以使用新的布局。 打开*电影. cshtml*文件。 在顶部，作为第一行代码，添加以下内容：

[!code-csharp[Main](layouts/samples/sample3.cs)]

该页现在以这种方式开始：

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

这一行代码告诉 ASP.NET 当*电影*页面运行时，应将其与 *\_布局 cshtml*文件合并。

由于*影院*文件现在使用布局页面，因此你可以从 *\_布局 cshtml*文件中删除由的 "*电影. cshtml* " 页中的标记。 `<!DOCTYPE>`、`<html>`和 `<body>` 打开和关闭标记。 提取整个 `<head>` 元素及其内容，其中包括网格的样式规则，因为现在已经在 *.css*文件中获得了这些规则。 在此过程中，将现有 `<h1>` 元素更改为 `<h2>` 元素;布局页中已有 `<h1>` 元素。 将 `<h2>` 文本更改为 "列出电影"。

通常无需在内容页中进行这些更改。 当你使用布局页启动站点时，将创建不包含所有这些元素的内容页面。 不过，在这种情况下，你要将独立页面转换为使用布局的页面，因此会有一点清理。

完成后，"*电影*" 页将如下所示：

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>测试布局

现在，可以看到布局的外观。 在 WebMatrix 中，右键*单击 ""* ，然后选择 "**在浏览器中启动**"。 当浏览器显示该页时，它将如下所示：

![使用布局呈现的电影页面](layouts/_static/image6.png)

ASP.NET 已将 "" 页的内容合并到 `RenderBody` 方法所在的 *\_Layout。* 当然，\_的*布局. cshtml*页引用定义页面外观的 *.css*文件。

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>更新 AddMovie 页以使用布局

布局的真正优点在于，您可以将它们用于站点中的所有页面。 打开*AddMovie*页。

你可能会注意到， *AddMovie*页最初在其中有一些 CSS 规则用于定义验证错误消息的外观。 由于你的网站现在具有一个 *.css*文件，因此你可以将这些规则移动到 *.css*文件中。 从*AddMovie*文件中删除它们，并将它们添加到 "*电影*" 文件的底部。 正在移动以下规则：

[!code-css[Main](layouts/samples/sample6.css)]

现在，在*AddMovie*中对所做的更改进行相同的更改 *：添加*`Layout="~/_Layout.cshtml;`，并删除目前无关的 HTML 标记。 将 `<h1>` 元素更改为 `<h2>`。 完成后，页面将如下所示：

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

运行页面。 现在，它如下图所示：

![使用布局呈现的 "添加电影" 页面](layouts/_static/image7.png)

需要对站点中的页面（ *EditMovie*和*DeleteMovie*）进行类似的更改。 但是，在执行此操作之前，您可以对布局进行另一个更改，使其变得更加灵活。

## <a name="passing-title-information-to-the-layout-page"></a>将标题信息传递到布局页

你创建的 *\_Layout* `<title>` 元素的元素设置为 "我的电影网站"。 大多数浏览器将此元素的内容显示为选项卡上的文本：

![在浏览器选项卡中显示的页面 &lt;标题&gt; 元素](layouts/_static/image8.png)

此标题信息是通用的。 假设您希望标题文本更特定于当前页。 （标题文本还由搜索引擎用来确定页面的内容。）可以将信息从诸如*AddMovie 或*的内容页传递到布局页，然后使用该信息自定义布局页的呈现内容。

再次打开 "*电影. cshtml* " 页。 在顶部的代码中，添加以下行：

[!code-csharp[Main](layouts/samples/sample8.cs)]

`Page` 对象可用于所有的*cshtml*页，用于实现此目的，即在页与其布局之间共享信息。

打开 *\_布局. cshtml* "页。 更改 `<title>` 元素，使其类似于以下标记：

[!code-html[Main](layouts/samples/sample9.html)]

此代码会在页中该位置的 `Page.Title` 属性右侧呈现任何内容。

运行 "*电影*" 页。 这次，"浏览器" 选项卡会显示你作为 `Page.Title`值传递的内容：

![显示动态创建的标题的浏览器选项卡](layouts/_static/image9.png)

如果需要，请在浏览器中查看页面源。 您可以看到 `<title>` 元素呈现为 `<title>List Movies</title>`。

> [!TIP] 
> 
> **Page 对象**
> 
> `Page` 的一项有用功能是动态对象-`Title` 属性不是固定或保留的名称。 可以将*任何*名称用于 `Page` 对象的值。 例如，你可以通过使用名为 `Page.CurrentName` 或 `Page.MyPage`的属性轻松地传递标题。 唯一的限制是，名称必须遵循可命名属性的常规规则。 （例如，名称不能包含空格。）
> 
> 可以通过使用 `Page` 对象传递任意数量的值。 如果要将电影信息传递到布局页面，可以使用 `Page.MovieTitle` 和 `Page.Genre` 和 `Page.MovieYear`之类的内容传递值。 （或你为存储信息而所用的任何其他名称。）唯一的要求（可能是显而易见的要求）是您必须在 "内容" 页和 "布局" 页中使用相同的名称。
> 
> 使用 `Page` 对象传递的信息并不局限于布局页上显示的文本。 您可以将某个值传递到布局页，然后 "布局" 页中的代码可以使用该值来决定是显示该页的某个部分、要使用什么 *.css*文件等。 在 `Page` 对象中传递的值与您在代码中使用的任何其他值类似。 这只是值源自内容页，并传递到布局页。

打开*AddMovie*页面，并在代码顶部添加一行，以提供*AddMovie*页面的标题：

[!code-csharp[Main](layouts/samples/sample10.cs)]

运行*AddMovie*页。 你将在此处看到新标题：

![显示动态创建的 "添加电影" 标题的浏览器选项卡](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>更新剩余页面以使用布局

现在，你可以完成站点中的其余页面，使其使用新的布局。 依次打开*EditMovie*和*DeleteMovie* ，并在每个中进行相同的更改。

添加链接到布局页的代码行：

[!code-csharp[Main](layouts/samples/sample11.cs)]

添加线条以设置页面标题：

[!code-csharp[Main](layouts/samples/sample12.cs)]

或：

[!code-csharp[Main](layouts/samples/sample13.cs)]

删除所有无关的 HTML 标记，基本上只保留位于 `<body>` 元素内的位（和顶部的代码块）。

将 `<h1>` 元素更改为 `<h2>` 元素。

进行这些更改后，请对每个更改进行测试，并确保其正确显示并且标题正确。

## <a name="parting-thoughts-about-layout-pages"></a>有关布局页的分型想法

在本教程中，您将创建一个 *\_的布局. cshtml*页，并使用 `RenderBody` 方法来合并另一个页面中的内容。 这是在网页中使用布局的基本模式。

布局页中有一些其他功能，我们没有在此介绍。 例如，您可以嵌套布局页，一个布局页可以反过来引用另一个。 如果要使用需要不同布局的站点的子节，则嵌套布局会很有用。 你还可以使用其他方法（例如 `RenderSection`）在布局页面中设置命名节。

布局页和 *.css*文件的组合非常强大。 正如你将在下一系列教程中看到的那样，在 WebMatrix 中，你可以基于*模板*创建一个网站，该网站提供了一个具有预生成功能的网站。 这些模板充分利用了布局页和 CSS，创建外观非常好并且具有菜单等功能的网站。 下面是基于模板的网站主页的屏幕截图，其中显示了使用布局页和 CSS 的功能：

![WebMatrix 站点模板创建的布局，显示标题、导航区域、内容区域、可选部分和登录链接](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>完整的电影页面列表（已更新为使用布局页面）

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>"添加电影" 页的完整页面列表（已更新布局）

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>删除电影页面的完整页面列表（已更新布局）

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>编辑电影页面的完整页面列表（已更新布局）

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>下一步

在下一教程中，你将了解如何将网站发布到 Internet，以便每个人都可以看到它。

## <a name="additional-resources"></a>其他资源

- [创建一致的外观](https://go.microsoft.com/fwlink/?LinkID=202891)，这篇文章提供了有关如何使用布局的更多详细信息。 还介绍了如何将值传递到显示或隐藏某些内容的布局页。
- [使用 Razor 的嵌套布局页](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)-Mike Brind 博客提供了有关如何嵌套布局页的示例。 （包括页面的下载。）

> [!div class="step-by-step"]
> [上一页](deleting-data.md)
> [下一页](publishing.md)
