---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 呈现移动设备 ASP.NET 网页（Razor）站点 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）站点中创建将在移动设备上正确呈现的页面。 你将学习的内容：操作方法 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454352"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>呈现移动设备 ASP.NET 网页（Razor）站点

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）站点中创建将在移动设备上正确呈现的页面。
> 
> 学习内容：
> 
> - 如何使用命名约定来指定某个页面专门用于移动设备。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

ASP.NET 网页允许你创建自定义显示以在移动设备或其他设备上呈现内容。

若要在 ASP.NET 网页站点中创建特定于设备的页面，最简单的方法是使用如下所示的文件命名模式： *FileName。* 你可以创建两个版本的页（例如，一个名为*myfile.txt*的页，一个名为*myfile.txt*）。 在运行时，当移动设备请求*myfile.txt*时，ASP.NET 将呈现*myfile.txt*中的内容。 否则，将呈现*myfile.txt* 。

下面的示例演示如何通过添加移动设备的内容页来启用移动呈现。 *Page1*包含内容以及导航边栏。 *Page1*包含相同的内容，但省略了侧栏。

1. 在 ASP.NET 网页的站点中，创建一个名为 " *Page1* " 的文件，并将当前内容替换为以下标记。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. 创建一个名为 " *Page1* " 的文件，并将现有内容替换为以下标记。 请注意，此页的移动版本省略了导航部分，以便更好地在较小的屏幕上进行呈现。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. 运行桌面浏览器并浏览到*Page1*。 ![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. 运行移动浏览器（或移动设备模拟器）并浏览到*Page1。* （请注意，不包括*mobile。* 作为 URL 的一部分。）即使请求是*ASP.NET，也*会呈现*page1*。

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> 若要测试移动页，可以使用在台式计算机上运行的移动设备模拟器。 使用此工具，您可以像在移动设备上查看网页一样对其进行测试（也就是，显示区域通常更小）。 模拟器的一个示例是用于 Mozilla Firefox 的[用户代理切换器外接程序](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)，它使你可以从 Firefox 的桌面版本模拟各种移动浏览器。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[Windows Phone 模拟器](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
