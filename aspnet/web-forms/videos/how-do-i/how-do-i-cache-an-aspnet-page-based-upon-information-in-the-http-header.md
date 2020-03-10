---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[如何实现：] 根据 HTTP 标头中的信息缓存 ASP.NET 页 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何根据页面的 HTTP 标头中的信息，在 ASP.NET 输出缓存中保留页面。 首先，可能的 HTTP 页眉
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506972"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="255c6-104">[如何实现：] 基于 HTTP 标头中的信息缓存 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="255c6-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="255c6-105">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="255c6-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="255c6-106">在此视频中，Chris 像素演示了如何根据页面的 HTTP 标头中的信息，在 ASP.NET 输出缓存中保留页面。</span><span class="sxs-lookup"><span data-stu-id="255c6-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="255c6-107">首先，检查可能的 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="255c6-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="255c6-108">然后，将创建一个示例页，然后将 OutputCache 指令与包含值 "accept-language" （HTTP 标头）的 VaryByHeader 属性结合使用，以根据用户浏览器的语言控制缓存。</span><span class="sxs-lookup"><span data-stu-id="255c6-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="255c6-109">在 IE 中查看示例页，该页面设置为英语，然后在 FireFox 中设置为使用法语。</span><span class="sxs-lookup"><span data-stu-id="255c6-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="255c6-110">最后，讨论将缓存定义移动到 web.config 文件中的 CacheProfile 的选项。</span><span class="sxs-lookup"><span data-stu-id="255c6-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="255c6-111">&#9654;观看视频（12分钟）</span><span class="sxs-lookup"><span data-stu-id="255c6-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
