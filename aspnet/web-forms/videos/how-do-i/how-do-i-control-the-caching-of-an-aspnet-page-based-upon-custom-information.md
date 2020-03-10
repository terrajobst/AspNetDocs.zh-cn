---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[如何实现：]基于自定义信息控制 ASP.NET 页面的缓存 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何控制基于自定义信息缓存 ASP.NET 页面的条件。 将创建一个示例页，然后创建
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506768"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="a9d22-104">[如何实现：]基于自定义信息控制 ASP.NET 页面的缓存</span><span class="sxs-lookup"><span data-stu-id="a9d22-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="a9d22-105">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="a9d22-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="a9d22-106">在此视频中，Chris 像素演示了如何控制基于自定义信息缓存 ASP.NET 页面的条件。</span><span class="sxs-lookup"><span data-stu-id="a9d22-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="a9d22-107">将创建一个示例页，然后将 OutputCache 指令与包含自定义值的 VaryByCustom 属性一起使用。</span><span class="sxs-lookup"><span data-stu-id="a9d22-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="a9d22-108">接下来，在 global.asax 模块中重写 GetVaryCustomByString （）方法，该模块提供自定义属性的处理。</span><span class="sxs-lookup"><span data-stu-id="a9d22-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="a9d22-109">在该方法中，将返回一个字符串，该字符串唯一标识页面的缓存版本。</span><span class="sxs-lookup"><span data-stu-id="a9d22-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="a9d22-110">最后，还讨论了如何使用自定义值进行缓存，以多种方式用于网站。</span><span class="sxs-lookup"><span data-stu-id="a9d22-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="a9d22-111">&#9654;观看视频（12分钟）</span><span class="sxs-lookup"><span data-stu-id="a9d22-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
