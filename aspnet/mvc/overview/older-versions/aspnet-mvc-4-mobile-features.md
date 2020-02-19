---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 移动功能 |Microsoft Docs
author: Rick-Anderson
description: 现在，在 Azure 网站上部署 ASP.NET MVC 5 移动 Web 应用程序的代码示例中提供了本教程的 MVC 5 版本。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457643"
---
# <a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 移动功能

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 现在，在[Azure 网站上部署 ASP.NET mvc 5 移动 Web 应用程序](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)的代码示例中提供了本教程的 MVC 5 版本。

本教程将指导你了解如何使用 ASP.NET MVC 4 Web 应用程序中的移动功能。 对于本教程，可以使用[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual web Developer 2010 Express Service Pack 1 （&quot;Visual web DEVELOPER 或 VWD&quot;）。 你可以使用 Visual Studio 的专业版（如果已有）。

在开始之前，请确保已安装下列必备组件。

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) （推荐）或 Visual Studio Web DEVELOPER Express SP1。 Visual Studio 2012 包含 ASP.NET MVC 4。 如果使用的是 Visual Web Developer 2010，则必须安装[ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)。

还需要安装移动浏览器模拟器。 以下版本均可：

- [Windows 7 Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。 （本教程的大部分屏幕快照中都使用这种模拟器。）
- 更改用户代理字符串以模拟 iPhone。 请参阅[此](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)博客文章。
- [Opera 移动模拟器](http://www.opera.com/developer/tools/mobile/)
- 将用户代理设置为 iPhone 的[Apple Safari](http://www.apple.com/safari/download/) 。 有关如何将 Safari 中的用户代理设置为 "iPhone" 的说明，请参阅[如何让 Safari 假设它](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的博客上。

本主题可以附带包含具有 C# 源代码的 Visual Studio：

- [初学者项目下载](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [已完成项目下载](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>所需操作

在本教程中，你将向[初学者项目](https://go.microsoft.com/fwlink/?LinkId=228307)中提供的简单会议列表应用程序添加移动功能。 以下屏幕截图显示了已完成的应用程序的 "标记" 页，如[Windows 7 Phone 模拟器](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)中所示。 请参阅[Windows Phone 模拟器的键盘映射](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)，简化键盘输入。

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

可以通过设置[用户代理字符串](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)，使用 Internet Explorer 版本9或10、FireFox 或 Chrome 来开发移动应用程序。 下图显示了使用 Internet Explorer 模拟 iPhone 的已完成教程。 可以使用 Internet Explorer F-12 开发人员工具和[Fiddler 工具](http://www.fiddler2.com/fiddler2/)来帮助调试应用程序。

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>将要学到的技能

学习内容：

- ASP.NET MVC 4 模板如何使用 HTML5 `viewport` 属性和自适应呈现来改善移动设备上的显示效果。
- 如何创建移动特定视图。
- 如何创建视图切换器，以便用户能够在应用程序的移动视图与桌面视图间切换。

### <a name="getting-started"></a>入门

使用以下链接下载初学者项目的会议列表应用程序：[下载](https://go.microsoft.com/fwlink/?LinkId=228307)。 然后在 Windows 资源管理器中，右键单击*mvcmobile.sln*文件，然后选择 "**属性**"。 在 " **Mvcmobile.sln 属性**" 对话框中，选择 "**取消阻止**" 按钮。 （取消阻止后，尝试使用从 Web 下载的 *.zip* 文件时，不再显示安全警告。）

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

右键单击 " *mvcmobile.sln* " 文件，然后选择 "**全部提取**" 来解压缩该文件。 在 Visual Studio 中，打开*mvcmobile.sln*文件。

按 Ctrl + F5 运行该应用程序，它将在桌面浏览器中显示。 启动移动浏览器模拟器，将会议应用程序的 URL 复制到模拟器，然后单击 "**按标记浏览**" 链接。 如果您使用的是 Windows Phone Emulator，则在 URL 栏中单击并按“暂停”键来访问键盘。 下图显示了*AllTags*视图（选择 "**按标记浏览" 时**）。

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

显示内容在移动设备上一目了然。 选择 ASP.NET 链接。

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET 标签视图显示非常混乱。 例如，"**日期**" 列很难阅读。 稍后在本教程中，你将创建一个*AllTags*视图的版本，该版本专门用于移动浏览器并使显示可读。

注意：目前移动缓存引擎中存在错误。 对于生产应用程序，必须安装[Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 包。 有关修补程序的详细信息，请参阅[ASP.NET MVC 4 移动缓存 Bug](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 。

## <a name="css-media-queries"></a>CSS 媒体查询

[Css 媒体查询](http://www.w3.org/TR/css3-mediaqueries/)是媒体类型的 css 扩展。 它们允许您创建规则来覆盖特定浏览器（用户代理）的默认 CSS 规则。 面向移动浏览器的 CSS 的通用规则是定义最大屏幕大小。 创建新的 ASP.NET MVC 4 Internet 项目时创建的*Content\Site.css*文件包含以下媒体查询：

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

如果浏览器窗口的宽度为850像素或更小，则它将使用此媒体块内的 CSS 规则。 您可以使用如下所示的 CSS 媒体查询，在小型浏览器（如移动浏览器）上更好地显示 HTML 内容，而不是为桌面浏览器的更大显示而设计的默认 CSS 规则。

## <a name="the-viewport-meta-tag"></a>视区元标记

大多数移动浏览器定义一个虚拟浏览器窗口宽度（*视区*），该宽度远远大于移动设备的实际宽度。 这允许移动浏览器在虚拟显示中适应整个网页。 然后，用户可以放大感兴趣的内容。 但是，如果将视区宽度设置为实际设备宽度，则不需要缩放，因为内容适合移动浏览器。

ASP.NET MVC 4 布局文件中的视区 `<meta>` 标记将视区设置为设备宽度。 以下行显示 ASP.NET MVC 4 布局文件中 `<meta>` 标记的视区。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>检查 CSS 媒体查询和视区 Meta 标记的影响

在编辑器中打开 " *Views\Shared"\\_Layout* ，并注释掉视区 `<meta>` 标记。 下面的标记显示了注释掉的行。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

在编辑器中打开*MvcMobile\Content\Site.css*文件，并将 "媒体" 查询中的最大宽度更改为零像素。 这会阻止在移动浏览器中使用 CSS 规则。 以下行显示了修改后的媒体查询：

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

保存更改并在移动浏览器模拟器中浏览到会议应用程序。 下图中的小文本是删除视区 `<meta>` 标记的结果。 如果没有视区 `<meta>` 标记，浏览器将缩小为默认视区宽度（对于大多数移动浏览器，则为850像素或更宽）。

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

撤消所做的更改：在布局文件中取消注释视区 `<meta>` 标记，并在*web.config*文件中将媒体查询还原为850像素。 保存你所做的更改并刷新移动浏览器，以验证移动友好的显示是否已还原。

视区 `<meta>` 标记和 CSS 媒体查询并不特定于 ASP.NET MVC 4，你可以在任何 web 应用程序中利用这些功能。 但现在它们内置于创建新的 ASP.NET MVC 4 项目时生成的文件中。

有关视区 `<meta>` 标记的详细信息，请参阅[第二个视区的 tale](http://www.quirksmode.org/mobile/viewports2.html)。

在下一部分中，将了解如何提供移动浏览器特定的视图。

## <a name="overriding-views-layouts-and-partial-views"></a>重写视图、布局和分部视图

ASP.NET MVC 4 中的一个重要新功能是一种允许您针对常规移动浏览器、单个移动浏览器或任何特定浏览器重写任何视图（包括布局和分部视图）的简单机制。 要提供移动特定的视图，可以复制视图文件并在文件名中添加 *.Mobile*。 例如，若要创建移动*索引*视图，请将*Views\Home\Index.cshtml*复制到*Views\Home\Index.Mobile.cshtml*。

在本节中，将创建一个移动特定布局文件。

若要开始，请将*Views\Shared\\_Layout*中复制到*Views\Shared\\_Layout*。 打开 *\_* **MVC4** ，并将标题从 "会议" 更改为 "**会议（移动）** "。

在每个 `Html.ActionLink` 调用中，删除每*个链接中*的 "浏览者"。 以下代码显示已完成的移动布局文件主体部分。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

将*Views\Home\AllTags.cshtml*文件复制到*Views\Home\AllTags.Mobile.cshtml*。 打开新文件，将 `<h2>` 元素从 "Tags" 更改为 "Tags （M）"：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

使用桌面浏览器和移动浏览器模拟器浏览到标签页。 移动浏览器模拟器显示您所做的两处改动。

[![p2m_layoutTags mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

与此相反，桌面显示没有变化。

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>特定于浏览器的视图

除了移动特定和桌面特定的视图以外，还可以为单个浏览器创建视图。 例如，可以创建专门针对 iPhone 浏览器的视图。 在本节中，将为 iPhone 浏览器和 iPhone 版本的 *AllTags* 视图创建布局。

打开*global.asax*文件，并将以下代码添加到 `Application_Start` 方法。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

此代码定义要与每个传入请求匹配的名为“iPhone”的新显示模式。 如果传入请求与定义的条件（即，如果用户代理包含字符串“iPhone”）匹配，则 ASP.NET MVC 将查找名称包含“iPhone”后缀的视图。

在代码中右键单击 `DefaultDisplayMode`，选择“解析”，并选择 `using System.Web.WebPages;`。 这会向 `System.Web.WebPages` 命名空间添加引用，该命名空间中定义了 `DisplayModes` 和 `DefaultDisplayMode` 类型。

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

或者，也可以简单地将以下行手动添加到文件的 `using` 章节。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

*Global.asax*文件的完整内容如下所示。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

保存更改。 将*MvcMobile\Views\Shared\\_Layout*文件复制到*MvcMobile\Views\Shared\\_Layout*。 打开新文件，然后将 `h1` 标题从 "`Conference (Mobile)`" 更改为 "`Conference (iPhone)`"。

将*MvcMobile\Views\Home\AllTags.Mobile.cshtml*文件复制到*MvcMobile\Views\Home\AllTags.iPhone.cshtml*。 在新文件中，将 `<h2>` 元素从 "Tags （M）" 更改为 "Tags （iPhone）"。

运行应用程序。 运行移动浏览器模拟器，确保将其用户代理设置为“iPhone”，并浏览到 *AllTags* 视图。 以下屏幕截图显示了[Safari](http://www.apple.com/safari/download/)浏览器中呈现的*AllTags*视图。 可在[此处](https://support.apple.com/kb/DL1531)下载适用于 Windows 的 Safari。

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

在本节中，我们已了解如何创建移动布局和视图，以及如何为特定的设备（如 iPhone）创建布局和视图。 在下一部分中，你将了解如何利用 jQuery Mobile 获得更引人注目的移动视图。

## <a name="using-jquery-mobile"></a>使用 jQuery Mobile

[JQuery mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)库提供了一个可在所有主要移动浏览器上使用的用户界面框架。 jQuery Mobile 可对支持 CSS 和 JavaScript 的移动浏览器应用*渐进增强*。 渐进增强允许所有浏览器显示网页的基本内容，同时允许更强大的浏览器和设备拥有更丰富的显示。 jQuery Mobile 中包括的 JavaScript 和 CSS 文件为众多元素设定了样式来适应移动浏览器，无需对标记做任何更改。

在本部分中，你将安装*jquery* NuGet 包，它将安装 jquery Mobile 和视图切换器小组件。

若要开始，请删除之前创建的*共享\\_Layout*并*共享\\_Layout* 。

将*Views\Home\AllTags.Mobile.cshtml*和*Views\Home\AllTags.iPhone.cshtml*文件重命名为*Views\Home\AllTags.iPhone.cshtml.hide*和*Views\Home\AllTags.Mobile.cshtml.hide*。 由于这些文件不再具有*ASP.NET 扩展名，* 因此它们不会被 MVC 运行时用来呈现*AllTags*视图。

通过执行以下操作安装*jQuery* NuGet 包：

1. 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. 在 "**程序包管理器控制台**" 中，输入 `Install-Package jQuery.Mobile.MVC -version 1.0.0`

下图显示了 NuGet jQuery. Mvcmobile.sln 项目添加并更改的文件。 添加的文件的文件名后面追加了 [add]。 该图像不显示添加到*Content\images*文件夹中的 GIF 和 PNG 文件。

![](aspnet-mvc-4-mobile-features/_static/image21.png)

jQuery.Mobile.MVC NuGet 程序包将安装以下内容：

- *应用\_Start\BundleMobileConfig.cs*文件，该文件用于引用添加的 jQuery JAVASCRIPT 和 CSS 文件。 必须按照下面的说明并引用该文件中定义的移动捆绑。
- jQuery Mobile CSS 文件。
- `ViewSwitcher` 控制器小组件（*Controllers\ViewSwitcherController.cs*）。
- jQuery Mobile JavaScript 文件。
- JQuery Mobile 样式的布局文件（*Views\Shared\\_Layout*。
- 视图切换器分部视图 *（MvcMobile\Views\Shared\\_ViewSwitcher*），它在每个页面的顶部提供一个链接，用于从桌面视图切换到移动视图，反之亦然。
- <em>Content\images</em>文件夹中的几个<em>.png</em>和<em>.gif</em>图像文件。

打开*global.asax*文件，并添加以下代码作为 `Application_Start` 方法的最后一行。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

下面的代码显示完整的*global.asax*文件。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> 如果你使用的是 Internet Explorer 9，但在黄色突出显示中看不到上面的 "`BundleMobileConfig`" 行，请单击 IE 中!["兼容性视图" 按钮（关闭](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg ""兼容性视图" 按钮的图片（关闭）")）的 "[兼容性视图" 按钮](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)图片，使图标从!["兼容性视图" 按钮（"关闭"）](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg ""兼容性视图" 按钮的图片（关闭）")的大纲图片更改为!["兼容性视图" 按钮（打开](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg ""兼容性视图" 按钮的图片（on）")）的纯色图片。 或者，您也可以在 FireFox 或 Chrome 中查看本教程。

打开*MvcMobile\Views\Shared\\_Layout*文件，并直接在 `Html.Partial` 调用后添加以下标记：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

完整的*MvcMobile\Views\Shared\\_Layout*的文件如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

构建应用程序，在移动浏览器模拟器中浏览到*AllTags*视图。 会看到如下内容：

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> 可以通过将 IE 或 Chrome 的[用户代理字符串设置](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)为 iPhone，然后使用 F-12 开发人员工具来调试移动特定代码。 如果你的移动浏览器未将 "**主页**"、"**发言人**"、"**标签**" 和 "**日期**" 链接显示为按钮，则对 jQuery mobile 脚本和 CSS 文件的引用可能不正确。

除了样式更改之外，你还可以看到 "**移动视图**" 和一个链接，通过该链接，你可以从移动视图切换到桌面视图。 选择 "**桌面视图**" 链接，随即显示桌面视图。

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

桌面视图不提供直接导航回移动视图的途径。 现在来修复此问题。 打开*Views\Shared\\_Layout cshtml*文件。 在页面 `body` 元素的正下方，添加以下代码，用于呈现视图切换器小组件：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

在移动浏览器中刷新 " *AllTags* " 视图。 您现在可以在桌面和移动视图间导航了。

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> 调试说明：可以将以下代码添加到 Views\Shared\\_ViewSwitcher 的末尾，以便在使用浏览器时帮助调试视图。将用户代理字符串设置为移动设备。
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> 并将以下标题添加到*Views\Shared\\_Layout cshtml*文件中。
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

在桌面浏览器中浏览到*AllTags*页。 因为只将视图切换器小组件添加到了移动布局页面中，所以在桌面浏览器中未显示该小组件。 在教程的稍后部分中，您将学习如何将视图切换器小组件添加到桌面视图中。

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>改进发言人列表

在移动浏览器中，选择“发言人”链接。 因为没有移动视图（*allspeakers.mobile.cshtml*），所以使用移动布局视图（ *\_* allspeakers.mobile.cshtml）呈现默认的演讲者（）（可能为英语）。

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

你可以通过将 `RequireConsistentDisplayMode` 设置为 `true` 在视图中的 *_ViewStart\\视图*中，在移动布局内全局禁用默认（非移动）视图，如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

将 `RequireConsistentDisplayMode` 设置为 `true`时，移动布局（<em>\_layout</em>）只用于移动视图。 （也就是说，视图文件的格式为<em>* * ViewName</em><em>。</em>如果你的移动布局不太适合你的非移动视图，则可能需要将 `RequireConsistentDisplayMode` 设置为 `true`。 下面的屏幕截图显示当 `RequireConsistentDisplayMode` 设置为 `true`时，如何呈现 "<em>发言人</em>" 页面。

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

您可以通过在视图文件中将 `RequireConsistentDisplayMode` 设置为 `false` 来禁用视图中一致的显示模式。 *Views\Home\AllSpeakers.cshtml*文件中的以下标记将 `RequireConsistentDisplayMode` 设置为 `false`：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>创建移动发言人视图

正如你刚才看到的，"*发言人*" 视图是可读的，但链接很小，难于在移动设备上点击。 在本部分中，你将创建一个移动特定的 "*发言人*" 视图，它看起来像一个现代移动应用程序，它显示的是大、易于点击的链接，并包含一个搜索框，用于快速查找扬声器。

将*allspeakers.mobile.cshtml*复制到*allspeakers.mobile.cshtml*。 打开*allspeakers.mobile.cshtml*文件并删除 `<h2>` 标题元素。

在 `<ul>` 标记中，添加 `data-role` 属性，并将其值设置为 "`listview`"。 与其他[`data-*` 属性](http://html5doctor.com/html5-custom-data-attributes/)一样，`data-role="listview"` 使大型列表项更易于点击。 完成的标记如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

刷新移动浏览器。 更新的视图如下所示：

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

尽管移动视图得到了改进，但很难在较长的发言人列表中导航。 若要解决此问题，请在 `<ul>` 标记中添加 `data-filter` 属性，并将其设置为 `true`。 下面的代码演示 `ul` 标记。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

下图显示了 `data-filter` 属性生成的页面顶部的 "搜索筛选器" 框。

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

当您在搜索框中键入每个字母时，jQuery Mobile 将筛选显示的列表，如下图所示。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>改善标记列表

与默认 "*发言人*" 视图一样，"*标记*" 视图是可读的，但链接比较小，难于在移动设备上点击。 在本部分中，您将修复 "*标记*" 视图，与修复 "*发言人*" 视图的方式相同。

删除 &quot;隐藏*Views\Home\AllTags.Mobile.cshtml.hide*文件的&quot; 后缀，使名称为*Views\Home\AllTags.Mobile.cshtml*。 打开重命名的文件，并删除 `<h2>` 元素。

将 `data-role` 和 `data-filter` 属性添加到 `<ul>` 标记，如下所示：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

下图显示了字母 `J`上的 "标记" 页筛选。

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>改进日期列表

你可以像改进 "*发言人*" 和 "*标签*" 视图那样改进 "*日期*" 视图，使其更易于在移动设备上使用。

将*Views\Home\AllDates.cshtml*文件复制到*Views\Home\AllDates.Mobile.cshtml*。 打开新文件并删除 `<h2>` 元素。

向 `<ul>` 标记添加 `data-role="listview"`，如下所示：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

下图显示了 "**日期**" 页面与 "`data-role`" 属性相同的外观。

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)将*Views\Home\AllDates.Mobile.cshtml*文件的内容替换为以下代码：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

此代码按日期将所有会话分组。 它为每个新日期创建一条列表分隔线，在分隔线下列出一天的所有会话。 当此代码运行时，它看起来像这样：

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>改进 SessionsTable 视图

在本节中，您将创建一个移动特定的会话视图。 我们所做的更改将比在我们创建的其他视图中更广泛。

在移动浏览器中，点击 "**发言人**" 按钮，然后在搜索框中输入 `Sc`。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

点击**Scott Hanselman**链接。

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

正如您所看到的，显示的内容难以在移动浏览器上阅读。 日期列难于阅读，标签列也超出了视图。 若要解决此问题，请将*Views\Home\SessionsTable.cshtml*复制到*Views\Home\SessionsTable.Mobile.cshtml*，然后将该文件的内容替换为以下代码：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

该代码移除了 Room 和 Tag 列，将标题、发言人和日期设置为竖式，这样，即可在移动浏览器中阅读所有此类信息。 下图反映了代码更改。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>改进 SessionByCode 视图

最后，您将创建一个特定于移动设备的*SessionByCode*视图。 在移动浏览器中，点击 "**发言人**" 按钮，然后在搜索框中输入 `Sc`。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

点击**Scott Hanselman**链接。 将显示 Scott Hanselman 的会话。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

选择 **"Microsoft 欢迎使用 Web 堆栈"** 链接的概述。

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

默认桌面视图虽然不错，但仍可以改进。

将*views\home\sessionbycode.cshtml 复制*复制到*Views\Home\SessionByCode.Mobile.cshtml* ，并将*Views\Home\SessionByCode.Mobile.cshtml*文件的内容替换为以下标记：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

新标记使用 `data-role` 特性来改进视图的布局。

刷新移动浏览器。 下图反映你刚才所做的代码更改：

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup 和评审

本教程介绍了 ASP.NET MVC 4 开发者预览版的新移动功能。 移动功能包括：

- 覆盖全局视图和单个视图的布局、视图和分部视图的功能。
- 使用 `RequireConsistentDisplayMode` 属性控制布局和部分重写强制。
- 移动视图的视图切换器小组件（而不是在桌面视图中显示）。
- 支持特定的浏览器，例如 iPhone 浏览器。

## <a name="see-also"></a>另请参阅

- [JQuery mobile](http://jquerymobile.com)站点。
- [jQuery Mobile 概述](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C 建议移动 Web 应用程序的最佳做法](http://www.w3.org/TR/mwabp/)
- [用于媒体查询的 W3C 候选建议方案](http://www.w3.org/TR/css3-mediaqueries/)
