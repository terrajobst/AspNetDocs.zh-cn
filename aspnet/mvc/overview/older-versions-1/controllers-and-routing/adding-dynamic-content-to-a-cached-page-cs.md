---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 向缓存的页（C#）中添加动态内容 |Microsoft Docs
author: microsoft
description: 了解如何在同一页面中混合动态和缓存内容。 通过缓存后替换，可以显示动态内容，例如横幅广告 o 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486938"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>向缓存页添加动态内容 (C#)

由[Microsoft](https://github.com/microsoft)

> 了解如何在同一页面中混合动态和缓存内容。 通过缓存后替换，可以在已缓存的页面内显示动态内容，例如横幅广告或新闻项。

利用输出缓存，可以显著提高 ASP.NET MVC 应用程序的性能。 并非每次请求页面时都重新生成页面，只需生成一次页面并将其缓存在多个用户的内存中即可。

但出现问题。 如果需要在页面中显示动态内容，该怎么办？ 例如，假设您想要在页面上显示横幅广告。 您不希望对横幅广告进行缓存，以便每个用户都能看到非常相同的广告。 您不会这样做！

幸运的是，有一个简单的解决方案。 可以利用名为*后缓存替换*的 ASP.NET 框架功能。 使用缓存后替换，可以替换缓存在内存中的页面中的动态内容。

通常，当你通过使用 [OutputCache] 属性输出缓存页面时，将在服务器和客户端（web 浏览器）上缓存页面。 使用缓存后替换时，页仅缓存在服务器上。

#### <a name="using-post-cache-substitution"></a>使用缓存后替换

使用缓存后替换需要两个步骤。 首先，需要定义一个方法，该方法返回一个字符串，该字符串表示要在缓存页面中显示的动态内容。 接下来，调用 Httpresponse.cache WriteSubstitution （）方法将动态内容注入到页面中。

例如，假设您希望在缓存的页中随机显示不同的新闻项。 列表1中的类公开了一个名为 RenderNews （）的方法，该方法从三个新闻项的列表中随机返回一个新闻项。

**列表1– Models\News.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

若要利用缓存后替换，请调用 Httpresponse.cache WriteSubstitution （）方法。 WriteSubstitution （）方法设置代码以将缓存页的区域替换为动态内容。 WriteSubstitution （）方法用于在列表2的视图中显示随机新闻项。

**列表 2-Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

RenderNews 方法传递给 WriteSubstitution （）方法。 请注意，不会调用 RenderNews 方法（没有括号）。 相反，对方法的引用将传递给 WriteSubstitution （）。

索引视图被缓存。 视图由列表3中的控制器返回。 请注意，Index （）操作使用 [OutputCache] 属性修饰，这会导致索引视图缓存60秒。

**列表 3-Controllers\HomeController.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

即使已缓存索引视图，请求索引页时也会显示不同的随机新闻项。 请求 "索引" 页时，页面显示的时间不会更改60秒（参见图1）。 这种情况不会发生更改，证明页面已缓存。 但是，由 WriteSubstitution （）方法插入的内容–随机新闻项目–随每个请求而更改。

**图1–在缓存页面中注入动态新闻项**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>在 Helper 方法中使用后缓存替换

更简单的方法是利用缓存后的替换方法，将对 WriteSubstitution （）方法的调用封装到自定义帮助器方法中。 此方法由列表4中的 helper 方法说明。

**列表 4-AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

列表4包含一个静态类，该类公开两个方法： RenderBanner （）和 RenderBannerInternal （）。 RenderBanner （）方法表示实际的帮助器方法。 此方法扩展了标准 ASP.NET MVC HtmlHelper 类，以便您可以在视图中调用 RenderBanner （），就像使用任何其他帮助器方法一样。

RenderBanner （）方法调用 Httpresponse.cache （）方法将 RenderBannerInternal （）方法传递给 WriteSubstitution （）方法。

RenderBannerInternal （）方法是私有方法。 此方法不会公开为帮助器方法。 RenderBannerInternal （）方法从三个横幅广告图像的列表中随机返回一个横幅广告图像。

"列表 5" 中修改的索引视图说明了如何使用 RenderBanner （） helper 方法。 请注意，视图顶部包含附加的 &lt;% @ Import%&gt; 指令以导入 MvcApplication1 命名空间。 如果忽略导入此命名空间，则 RenderBanner （）方法不会在 Html 属性上显示为方法。

**列表5– Views\Home\Index.aspx （with RenderBanner （）方法）**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

在列表5中请求视图呈现的页面时，每个请求都会显示不同的横幅广告（参见图2）。 将缓存该页，但会通过 RenderBanner （） helper 方法动态注入标题广告。

**图 2-显示随机横幅广告的索引视图**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>摘要

本教程介绍了如何在缓存页面中动态更新内容。 已了解如何使用 Httpresponse.cache WriteSubstitution （）方法使动态内容注入到缓存页中。 还了解了如何在 HTML 帮助器方法中封装对 WriteSubstitution （）方法的调用。

尽可能利用缓存，这可能会对 web 应用程序的性能产生显著影响。 如本教程中所述，即使您需要在页面中显示动态内容，也可以利用缓存。

> [!div class="step-by-step"]
> [上一页](improving-performance-with-output-caching-cs.md)
> [下一页](creating-a-controller-cs.md)
