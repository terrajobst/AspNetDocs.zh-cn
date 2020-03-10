---
uid: web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
title: 如何实现：在 ASP.NET 路由中使用 Url？ | Microsoft Docs
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何在使用 ASP.NET 路由的网站中指定 Url。 首先，创建一个网站，并在总帐中定义路由 。
ms.author: riande
ms.date: 10/15/2010
ms.assetid: 08f9d0a7-cfa0-4914-a672-8a64295d7ba8
msc.legacyurl: /web-forms/videos/net-4/routing/how-do-i-work-with-urls-in-aspnet-routing
msc.type: video
ms.openlocfilehash: eb1060fd9cc9469dc2b1d2e918823316c36840cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455690"
---
# <a name="how-do-i-work-with-urls-in-aspnet-routing"></a><span data-ttu-id="ef0aa-105">如何实现：在 ASP.NET 路由中使用 Url？</span><span class="sxs-lookup"><span data-stu-id="ef0aa-105">How Do I: Work with URLs in ASP.NET Routing?</span></span>

<span data-ttu-id="ef0aa-106">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="ef0aa-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="ef0aa-107">在此视频中，Chris 像素演示了如何在使用 ASP.NET 路由的网站中指定 Url。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-107">In this video Chris Pels shows how to specify URLs in a web site that utilizes ASP.NET routing.</span></span> <span data-ttu-id="ef0aa-108">首先，创建一个网站，并在全局应用程序类（global.asax）中定义路由。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-108">First, a web site is created and routing is defined in the Global Application Class (.asax).</span></span> <span data-ttu-id="ef0aa-109">接下来，将创建一个示例网页，并使用标准的 "硬编码" 方法（例如 "~/Stats/Visitors"）将基于定义的路由的 URL 添加到页面。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-109">Next, a sample web page is created and a URL based upon a defined route is added to the page using the standard "hard coded" approach, e.g., "~/Stats/Visitors".</span></span> <span data-ttu-id="ef0aa-110">然后，会向页面中添加另一个链接，该链接使用接受路由名称和参数的 RouteValue 方法在标记中动态生成相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-110">Another link is then added to the page which dynamically generates the same URL in markup using the RouteValue method which accepts the route name and parameters.</span></span> <span data-ttu-id="ef0aa-111">然后，使用代码而不是直接在页面中实现标记来实现相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-111">The same URL is then implemented using code rather than markup directly in the page.</span></span> <span data-ttu-id="ef0aa-112">然后，将更改原始路由和物理页面位置，从而导致硬编码的链接不再工作，而动态生成的链接也能正常运行。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-112">The original route and physical page location are then changed, resulting in the hard coded link no longer working whereas both dynamically generated links function properly.</span></span> <span data-ttu-id="ef0aa-113">最后，将讨论动态生成的链接的值。</span><span class="sxs-lookup"><span data-stu-id="ef0aa-113">Finally, the value of dynamically generated links is then discussed.</span></span>

[<span data-ttu-id="ef0aa-114">&#9654;观看视频（20分钟）</span><span class="sxs-lookup"><span data-stu-id="ef0aa-114">&#9654; Watch video (20 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-work-with-urls-in-aspnet-routing)

> [!div class="step-by-step"]
> [<span data-ttu-id="ef0aa-115">上一页</span><span class="sxs-lookup"><span data-stu-id="ef0aa-115">Previous</span></span>](how-do-i-use-routing-with-aspnet-web-forms.md)
