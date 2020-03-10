---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 路由概述（VB） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 显示 ASP.NET MVC 框架如何将浏览器请求映射到控制器操作。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486896"
---
# <a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="8c506-103">ASP.NET MVC 路由概述 (VB)</span><span class="sxs-lookup"><span data-stu-id="8c506-103">ASP.NET MVC Routing Overview (VB)</span></span>

<span data-ttu-id="8c506-104">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="8c506-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="8c506-105">在本教程中，Stephen Walther 显示 ASP.NET MVC 框架如何将浏览器请求映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="8c506-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="8c506-106">本教程介绍了每个称为*ASP.NET 路由*的 ASP.NET MVC 应用程序的重要功能。</span><span class="sxs-lookup"><span data-stu-id="8c506-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="8c506-107">ASP.NET 路由模块负责将传入浏览器请求映射到特定 MVC 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="8c506-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="8c506-108">在本教程结束时，您将了解标准路由表如何将请求映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="8c506-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="8c506-109">使用默认路由表</span><span class="sxs-lookup"><span data-stu-id="8c506-109">Using the Default Route Table</span></span>

<span data-ttu-id="8c506-110">在创建新的 ASP.NET MVC 应用程序时，应用程序已配置为使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="8c506-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="8c506-111">ASP.NET 路由是在两个位置设置的。</span><span class="sxs-lookup"><span data-stu-id="8c506-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="8c506-112">首先，应用程序的 Web 配置文件（Web.config 文件）启用了 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="8c506-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="8c506-113">配置文件中有四个部分与路由相关：system.web.httpModules 节、system.web.httpHandlers 节、system.webserver.modules 节和 system.webserver.handlers 节。</span><span class="sxs-lookup"><span data-stu-id="8c506-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="8c506-114">请注意不要删除这些节，因为如果没有这些节，路由将不再起作用。</span><span class="sxs-lookup"><span data-stu-id="8c506-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="8c506-115">其次，更重要的是，路由表是在应用程序的 Global.asax 文件中创建的。</span><span class="sxs-lookup"><span data-stu-id="8c506-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="8c506-116">Global.asax 文件是一个特殊文件，其中包含 ASP.NET 应用程序生命周期事件的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="8c506-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="8c506-117">路由表在 Application Start 事件中创建。</span><span class="sxs-lookup"><span data-stu-id="8c506-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="8c506-118">列表1中的文件包含 ASP.NET MVC 应用程序的默认 global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="8c506-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="8c506-119">**列表 1-global.asax**</span><span class="sxs-lookup"><span data-stu-id="8c506-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="8c506-120">MVC 应用程序首次启动时，将调用应用程序\_Start （）方法。</span><span class="sxs-lookup"><span data-stu-id="8c506-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="8c506-121">此方法反过来会调用 RegisterRoutes() 方法。</span><span class="sxs-lookup"><span data-stu-id="8c506-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="8c506-122">RegisterRoutes() 方法负责创建路由表。</span><span class="sxs-lookup"><span data-stu-id="8c506-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="8c506-123">默认路由表包含一个路由（名为 Default）。</span><span class="sxs-lookup"><span data-stu-id="8c506-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="8c506-124">默认路由将 URL 的第一段映射到控制器名称，将 URL 的第二段映射到控制器操作，并将第三段映射到名为**id**的参数。</span><span class="sxs-lookup"><span data-stu-id="8c506-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="8c506-125">假设你在 web 浏览器的地址栏中输入以下 URL：</span><span class="sxs-lookup"><span data-stu-id="8c506-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="8c506-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="8c506-126">/Home/Index/3</span></span>

<span data-ttu-id="8c506-127">默认路由将此 URL 映射到以下参数：</span><span class="sxs-lookup"><span data-stu-id="8c506-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="8c506-128">控制器 = Home</span><span class="sxs-lookup"><span data-stu-id="8c506-128">controller = Home</span></span>

- <span data-ttu-id="8c506-129">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="8c506-129">action = Index</span></span>

- <span data-ttu-id="8c506-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="8c506-130">id = 3</span></span>

<span data-ttu-id="8c506-131">请求 URL/Home/Index/3 时，将执行以下代码：</span><span class="sxs-lookup"><span data-stu-id="8c506-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="8c506-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="8c506-132">HomeController.Index(3)</span></span>

<span data-ttu-id="8c506-133">Default 路由包括所有三个参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="8c506-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="8c506-134">如果不提供控制器，则控制器参数默认为值**Home**。</span><span class="sxs-lookup"><span data-stu-id="8c506-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="8c506-135">如果不提供操作，则操作参数将默认为值**索引**。</span><span class="sxs-lookup"><span data-stu-id="8c506-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="8c506-136">最后，如果不提供 id，id 参数将默认为空字符串。</span><span class="sxs-lookup"><span data-stu-id="8c506-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="8c506-137">让我们看几个有关默认路由如何将 Url 映射到控制器操作的示例。</span><span class="sxs-lookup"><span data-stu-id="8c506-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="8c506-138">假设你在浏览器地址栏中输入以下 URL：</span><span class="sxs-lookup"><span data-stu-id="8c506-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="8c506-139">/Home</span><span class="sxs-lookup"><span data-stu-id="8c506-139">/Home</span></span>

<span data-ttu-id="8c506-140">由于 Default 路由参数存在默认值，输入此 URL 将导致 HomeController 类的 Index() 方法在列表 2 中被调用。</span><span class="sxs-lookup"><span data-stu-id="8c506-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="8c506-141">**列表 2-HomeController**</span><span class="sxs-lookup"><span data-stu-id="8c506-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="8c506-142">在列表2中，HomeController 类包含一个名为 Index （）的方法，该方法接受名为 Id 的单一参数。URL/Home 导致调用 Index （）方法时，不会将值视为 Id 参数的值。</span><span class="sxs-lookup"><span data-stu-id="8c506-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="8c506-143">由于 MVC 框架调用控制器操作的方式，URL/Home 还与列表3中 HomeController 类的 Index （）方法匹配。</span><span class="sxs-lookup"><span data-stu-id="8c506-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="8c506-144">**列表 3-HomeController （不带参数的索引操作）**</span><span class="sxs-lookup"><span data-stu-id="8c506-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="8c506-145">清单3中的 Index （）方法不接受任何参数。</span><span class="sxs-lookup"><span data-stu-id="8c506-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="8c506-146">URL/Home 将导致调用此索引（）方法。</span><span class="sxs-lookup"><span data-stu-id="8c506-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="8c506-147">URL/Home/Index/3 还会调用此方法（忽略 Id）。</span><span class="sxs-lookup"><span data-stu-id="8c506-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="8c506-148">URL/Home 还与列表4中 HomeController 类的 Index （）方法匹配。</span><span class="sxs-lookup"><span data-stu-id="8c506-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="8c506-149">**列表 4-HomeController （索引操作，参数可以为 null）**</span><span class="sxs-lookup"><span data-stu-id="8c506-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="8c506-150">在列表4中，Index （）方法有一个整数参数。</span><span class="sxs-lookup"><span data-stu-id="8c506-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="8c506-151">因为参数是一个可以为 null 的参数（可以不包含任何值），所以可以在不引发错误的情况下调用索引（）。</span><span class="sxs-lookup"><span data-stu-id="8c506-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="8c506-152">最后，在使用 URL/Home 的列表5中调用 Index （）方法将导致异常，因为 Id 参数*不*是可以为 null 的参数。</span><span class="sxs-lookup"><span data-stu-id="8c506-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="8c506-153">如果尝试调用 Index （）方法，则会获得图1中显示的错误。</span><span class="sxs-lookup"><span data-stu-id="8c506-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="8c506-154">**列出 HomeController （Id 参数的索引操作）**</span><span class="sxs-lookup"><span data-stu-id="8c506-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

<span data-ttu-id="8c506-155">[![调用需要参数值的控制器操作](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8c506-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="8c506-156">**图 01**：调用需要参数值的控制器操作（[单击以查看完全大小的图像](asp-net-mvc-routing-overview-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="8c506-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="8c506-157">另一方面，URL/Home/Index/3 的工作方式与清单5中的索引控制器操作非常相似。</span><span class="sxs-lookup"><span data-stu-id="8c506-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="8c506-158">请求/Home/Index/3 导致使用值为3的 Id 参数调用 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="8c506-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="8c506-159">摘要</span><span class="sxs-lookup"><span data-stu-id="8c506-159">Summary</span></span>

<span data-ttu-id="8c506-160">本教程的目的是提供 ASP.NET 路由的简要介绍。</span><span class="sxs-lookup"><span data-stu-id="8c506-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="8c506-161">我们检查了你使用新的 ASP.NET MVC 应用程序获取的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="8c506-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="8c506-162">已了解默认路由如何将 Url 映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="8c506-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c506-163">[上一页](creating-an-action-cs.md)
> [下一页](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8c506-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
