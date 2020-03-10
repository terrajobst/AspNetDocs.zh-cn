---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 创建路由约束（C#） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 演示了如何通过使用正则表达式创建路由约束来控制浏览器请求如何匹配路由。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470162"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="e581e-103">创建路由约束 (C#)</span><span class="sxs-lookup"><span data-stu-id="e581e-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="e581e-104">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e581e-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e581e-105">在本教程中，Stephen Walther 演示了如何通过使用正则表达式创建路由约束来控制浏览器请求如何匹配路由。</span><span class="sxs-lookup"><span data-stu-id="e581e-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="e581e-106">使用路由约束可以限制与特定路由匹配的浏览器请求。</span><span class="sxs-lookup"><span data-stu-id="e581e-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="e581e-107">可以使用正则表达式指定路由约束。</span><span class="sxs-lookup"><span data-stu-id="e581e-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="e581e-108">例如，假设你已在 global.asax 文件中的列表1中定义路由。</span><span class="sxs-lookup"><span data-stu-id="e581e-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="e581e-109">**列表 1-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="e581e-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="e581e-110">列表1包含名为 Product 的路由。</span><span class="sxs-lookup"><span data-stu-id="e581e-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="e581e-111">您可以使用产品路由将浏览器请求映射到列表2中包含的 ProductController。</span><span class="sxs-lookup"><span data-stu-id="e581e-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="e581e-112">**列表 2-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="e581e-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="e581e-113">请注意，产品控制器公开的详细信息（）操作接受名为 "productId" 的单个参数。</span><span class="sxs-lookup"><span data-stu-id="e581e-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="e581e-114">此参数是一个整数参数。</span><span class="sxs-lookup"><span data-stu-id="e581e-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="e581e-115">列表1中定义的路由将匹配以下任何 Url：</span><span class="sxs-lookup"><span data-stu-id="e581e-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="e581e-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="e581e-116">/Product/23</span></span>
- <span data-ttu-id="e581e-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="e581e-117">/Product/7</span></span>

<span data-ttu-id="e581e-118">遗憾的是，该路由还会匹配以下 Url：</span><span class="sxs-lookup"><span data-stu-id="e581e-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="e581e-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="e581e-119">/Product/blah</span></span>
- <span data-ttu-id="e581e-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="e581e-120">/Product/apple</span></span>

<span data-ttu-id="e581e-121">由于 Details （）操作需要整数参数，因此，如果请求包含整数值以外的值，则会导致错误。</span><span class="sxs-lookup"><span data-stu-id="e581e-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="e581e-122">例如，如果在浏览器中键入 URL/Product/apple，则会收到图1中的错误页。</span><span class="sxs-lookup"><span data-stu-id="e581e-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="e581e-123">[!["新建项目" 对话框](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e581e-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="e581e-124">**图 01**：查看页面分解（[单击以查看完全大小的图像](creating-a-route-constraint-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="e581e-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="e581e-125">你真正想要做的只是匹配包含适当整数 productId 的 Url。</span><span class="sxs-lookup"><span data-stu-id="e581e-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="e581e-126">定义路由时，可以使用约束来限制与路由匹配的 Url。</span><span class="sxs-lookup"><span data-stu-id="e581e-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="e581e-127">清单3中修改后的产品路由包含仅匹配整数的正则表达式约束。</span><span class="sxs-lookup"><span data-stu-id="e581e-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="e581e-128">**列表 3-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="e581e-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="e581e-129">正则表达式 \d + 匹配一个或多个整数。</span><span class="sxs-lookup"><span data-stu-id="e581e-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="e581e-130">此约束会导致产品路由与以下 Url 匹配：</span><span class="sxs-lookup"><span data-stu-id="e581e-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="e581e-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="e581e-131">/Product/3</span></span>
- <span data-ttu-id="e581e-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="e581e-132">/Product/8999</span></span>

<span data-ttu-id="e581e-133">但不是以下 Url：</span><span class="sxs-lookup"><span data-stu-id="e581e-133">But not the following URLs:</span></span>

- <span data-ttu-id="e581e-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="e581e-134">/Product/apple</span></span>
- <span data-ttu-id="e581e-135">/Product</span><span class="sxs-lookup"><span data-stu-id="e581e-135">/Product</span></span>

- <span data-ttu-id="e581e-136">这些浏览器请求将由其他路由处理; 如果没有匹配的路由，则将返回 *"找不到资源"* 错误。</span><span class="sxs-lookup"><span data-stu-id="e581e-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e581e-137">[上一页](creating-custom-routes-cs.md)
> [下一页](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e581e-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
