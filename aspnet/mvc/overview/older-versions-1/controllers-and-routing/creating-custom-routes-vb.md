---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 创建自定义路由（VB） |Microsoft Docs
author: microsoft
description: 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将了解如何修改 global.asax 文件中的默认路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486692"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="8dd9f-104">创建自定义路由 (VB)</span><span class="sxs-lookup"><span data-stu-id="8dd9f-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="8dd9f-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8dd9f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8dd9f-106">了解如何将自定义路由添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="8dd9f-107">在本教程中，您将了解如何修改 global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="8dd9f-108">本教程介绍如何将自定义路由添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="8dd9f-109">了解如何使用自定义路由修改 global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="8dd9f-110">在 ASP.NET MVC 应用程序中，默认路由表将正常运行。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="8dd9f-111">但是，你可能会发现你有特殊的路由需求。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="8dd9f-112">在这种情况下，你可以创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="8dd9f-113">例如，假设您要构建一个博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="8dd9f-114">你可能需要处理传入的请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8dd9f-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="8dd9f-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="8dd9f-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="8dd9f-116">当用户输入此请求时，你想要返回与日期12/25/2009 对应的博客条目。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="8dd9f-117">若要处理此类型的请求，需要创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="8dd9f-118">列表1中的 Global.asa 文件包含一个名为 "博客" 的新自定义路由，该路由处理类似于/Archive/*输入日期*的请求。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="8dd9f-119">**列表 1-global.asax （带有自定义路由）**</span><span class="sxs-lookup"><span data-stu-id="8dd9f-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="8dd9f-120">添加到路由表中的路由顺序非常重要。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="8dd9f-121">新的自定义博客路由将添加到现有默认路由之前。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="8dd9f-122">如果你反转了顺序，则始终会调用默认路由，而不是自定义路由。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="8dd9f-123">自定义博客路由匹配所有以/Archive/. 开头的请求</span><span class="sxs-lookup"><span data-stu-id="8dd9f-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="8dd9f-124">因此，它匹配以下所有 Url：</span><span class="sxs-lookup"><span data-stu-id="8dd9f-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="8dd9f-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="8dd9f-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="8dd9f-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="8dd9f-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="8dd9f-127">/Archive/apple</span><span class="sxs-lookup"><span data-stu-id="8dd9f-127">/Archive/apple</span></span>

<span data-ttu-id="8dd9f-128">自定义路由会将传入请求映射到名为 Archive 的控制器，并调用 Entry （）操作。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="8dd9f-129">调用 Entry （）方法时，输入日期将作为名为 entryDate 的参数进行传递。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="8dd9f-130">可以在清单2中将博客自定义路由用于控制器。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="8dd9f-131">**列表 2-ArchiveController**</span><span class="sxs-lookup"><span data-stu-id="8dd9f-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="8dd9f-132">请注意，列表2中的 Entry （）方法接受 DateTime 类型的参数。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="8dd9f-133">MVC 框架的智能足以将输入日期从 URL 转换为日期时间值。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="8dd9f-134">如果 URL 中的输入日期参数无法转换为 DateTime，则会引发错误（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="8dd9f-135">**图 1-转换参数时出错**</span><span class="sxs-lookup"><span data-stu-id="8dd9f-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="8dd9f-136">[!["新建项目" 对话框](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8dd9f-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="8dd9f-137">**图 01**：转换参数时出错（[单击以查看完全大小的图像](creating-custom-routes-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="8dd9f-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="8dd9f-138">摘要</span><span class="sxs-lookup"><span data-stu-id="8dd9f-138">Summary</span></span>

<span data-ttu-id="8dd9f-139">本教程的目的是演示如何创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="8dd9f-140">已了解如何将自定义路由添加到表示博客条目的 Global.asa 文件中的路由表。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="8dd9f-141">本文介绍了如何将博客条目请求映射到名为 ArchiveController 的控制器，以及一个名为 Entry （）的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="8dd9f-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8dd9f-142">[上一页](asp-net-mvc-controller-overview-vb.md)
> [下一页](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8dd9f-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
