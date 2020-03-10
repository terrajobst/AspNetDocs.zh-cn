---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: 创建自定义路由约束（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何创建自定义路由约束。 我们实现了一个简单的自定义约束，可防止路由与 w 。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486788"
---
# <a name="creating-a-custom-route-constraint-vb"></a><span data-ttu-id="c4fe4-104">创建自定义路由约束 (VB)</span><span class="sxs-lookup"><span data-stu-id="c4fe4-104">Creating a Custom Route Constraint (VB)</span></span>

<span data-ttu-id="c4fe4-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c4fe4-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="c4fe4-106">Stephen Walther 演示了如何创建自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="c4fe4-107">我们实现了一个简单的自定义约束，当浏览器请求从远程计算机发出请求时，它会阻止路由匹配。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="c4fe4-108">本教程的目的是演示如何创建自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="c4fe4-109">使用自定义路由约束，可以防止路由匹配，除非有某些自定义条件匹配。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="c4fe4-110">在本教程中，我们将创建一个 Localhost 路由约束。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="c4fe4-111">Localhost 路由约束仅匹配从本地计算机发出的请求。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="c4fe4-112">不匹配 Internet 上的远程请求。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="c4fe4-113">通过实现 IRouteConstraint 接口实现自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="c4fe4-114">这是一个非常简单的接口，用于描述单一方法：</span><span class="sxs-lookup"><span data-stu-id="c4fe4-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="c4fe4-115">方法返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-115">The method returns a Boolean value.</span></span> <span data-ttu-id="c4fe4-116">如果返回 False，则与该约束关联的路由将不与浏览器请求匹配。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-116">If you return False, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="c4fe4-117">Localhost 约束包含在列表1中。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="c4fe4-118">**列表 1-LocalhostConstraint**</span><span class="sxs-lookup"><span data-stu-id="c4fe4-118">**Listing 1 - LocalhostConstraint.vb**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="c4fe4-119">列表1中的约束利用 HttpRequest 类公开的 IsLocal 属性。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="c4fe4-120">当请求的 IP 地址是127.0.0.1 或请求的 IP 地址与服务器的 IP 地址相同时，此属性返回 true。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="c4fe4-121">在 global.asax 文件中定义的路由内使用自定义约束。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="c4fe4-122">清单2中的 global.asax 文件使用 Localhost 约束来阻止任何人请求管理页，除非他们发出来自本地服务器的请求。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="c4fe4-123">例如，当从远程服务器发出请求时，/Admin/DeleteAll 的请求将会失败。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="c4fe4-124">**列表 2-global.asax**</span><span class="sxs-lookup"><span data-stu-id="c4fe4-124">**Listing 2 - Global.asax**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="c4fe4-125">本地主机约束在管理路由的定义中使用。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="c4fe4-126">远程浏览器请求不会匹配此路由。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="c4fe4-127">但请注意，在 global.asax 中定义的其他路由可能与同一请求匹配。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="c4fe4-128">必须了解的是，约束阻止特定路由匹配请求，而不是在 global.asax 文件中定义的所有路由。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="c4fe4-129">请注意，默认路由已从清单2的 global.asax 文件中注释掉。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="c4fe4-130">如果包括默认路由，则默认路由将与管理控制器的请求相匹配。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="c4fe4-131">在这种情况下，即使其请求与管理路由不匹配，远程用户仍可以调用管理控制器的操作。</span><span class="sxs-lookup"><span data-stu-id="c4fe4-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c4fe4-132">上一页</span><span class="sxs-lookup"><span data-stu-id="c4fe4-132">Previous</span></span>](creating-a-route-constraint-vb.md)
