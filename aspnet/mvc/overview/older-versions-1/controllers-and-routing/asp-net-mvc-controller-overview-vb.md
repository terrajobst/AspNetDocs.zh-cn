---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 控制器概述（VB） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 介绍了 ASP.NET MVC 控制器。 了解如何创建新控制器并返回不同类型的操作 res 。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486920"
---
# <a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="179f3-104">ASP.NET MVC 控制器概述 (VB)</span><span class="sxs-lookup"><span data-stu-id="179f3-104">ASP.NET MVC Controller Overview (VB)</span></span>

<span data-ttu-id="179f3-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="179f3-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="179f3-106">在本教程中，Stephen Walther 介绍了 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="179f3-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="179f3-107">了解如何创建新控制器并返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="179f3-108">本教程将探讨 ASP.NET MVC 控制器、控制器操作和操作结果的相关主题。</span><span class="sxs-lookup"><span data-stu-id="179f3-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="179f3-109">完成本教程后，你将了解如何使用控制器来控制访问者与 ASP.NET MVC 网站交互的方式。</span><span class="sxs-lookup"><span data-stu-id="179f3-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="179f3-110">了解控制器</span><span class="sxs-lookup"><span data-stu-id="179f3-110">Understanding Controllers</span></span>

<span data-ttu-id="179f3-111">MVC 控制器负责响应针对 ASP.NET MVC 网站发出的请求。</span><span class="sxs-lookup"><span data-stu-id="179f3-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="179f3-112">每个浏览器请求将映射到特定的控制器。</span><span class="sxs-lookup"><span data-stu-id="179f3-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="179f3-113">例如，假设你在浏览器的地址栏中输入以下 URL：</span><span class="sxs-lookup"><span data-stu-id="179f3-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="179f3-114">在这种情况下，将调用名为 ProductController 的控制器。</span><span class="sxs-lookup"><span data-stu-id="179f3-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="179f3-115">ProductController 负责生成对浏览器请求的响应。</span><span class="sxs-lookup"><span data-stu-id="179f3-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="179f3-116">例如，控制器可能会将特定视图返回到浏览器，或者控制器可能会将用户重定向到另一个控制器。</span><span class="sxs-lookup"><span data-stu-id="179f3-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="179f3-117">列表1包含一个名为 ProductController 的简单控制器。</span><span class="sxs-lookup"><span data-stu-id="179f3-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="179f3-118">**Listing1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="179f3-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="179f3-119">从列表1可以看出，控制器只是类（一种 Visual Basic 的 .NET 或C#类）。</span><span class="sxs-lookup"><span data-stu-id="179f3-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="179f3-120">控制器是一个派生自基 System.web 类的类。</span><span class="sxs-lookup"><span data-stu-id="179f3-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="179f3-121">由于控制器继承自此基类，控制器继承了几个免费的有用方法（稍后我们将讨论这些方法）。</span><span class="sxs-lookup"><span data-stu-id="179f3-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="179f3-122">了解控制器操作</span><span class="sxs-lookup"><span data-stu-id="179f3-122">Understanding Controller Actions</span></span>

<span data-ttu-id="179f3-123">控制器公开控制器操作。</span><span class="sxs-lookup"><span data-stu-id="179f3-123">A controller exposes controller actions.</span></span> <span data-ttu-id="179f3-124">操作是在浏览器地址栏中输入特定 URL 时调用的控制器上的方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="179f3-125">例如，假设您对以下 URL 发出请求：</span><span class="sxs-lookup"><span data-stu-id="179f3-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="179f3-126">在这种情况下，将在 ProductController 类上调用 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="179f3-127">Index （）方法是控制器操作的一个示例。</span><span class="sxs-lookup"><span data-stu-id="179f3-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="179f3-128">控制器操作必须是控制器类的公共方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="179f3-129">默认情况下，Visual Basic.NET 方法为公共方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="179f3-130">请注意，你添加到控制器类的任何公共方法都将自动作为控制器操作公开（必须小心，因为 universe 中的任何人只需在浏览器地址栏中键入正确的 URL 即可调用控制器操作）。</span><span class="sxs-lookup"><span data-stu-id="179f3-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="179f3-131">控制器操作必须满足一些额外的要求。</span><span class="sxs-lookup"><span data-stu-id="179f3-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="179f3-132">用作控制器操作的方法不能重载。</span><span class="sxs-lookup"><span data-stu-id="179f3-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="179f3-133">而且，控制器操作不能是静态方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="179f3-134">除了这样，你可以将任何方法仅用作控制器操作。</span><span class="sxs-lookup"><span data-stu-id="179f3-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="179f3-135">了解操作结果</span><span class="sxs-lookup"><span data-stu-id="179f3-135">Understanding Action Results</span></span>

<span data-ttu-id="179f3-136">控制器操作返回称为*操作结果*的内容。</span><span class="sxs-lookup"><span data-stu-id="179f3-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="179f3-137">操作结果是控制器操作为响应浏览器请求而返回的内容。</span><span class="sxs-lookup"><span data-stu-id="179f3-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="179f3-138">ASP.NET MVC 框架支持多种类型的操作结果，其中包括：</span><span class="sxs-lookup"><span data-stu-id="179f3-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="179f3-139">ViewResult-表示 HTML 和标记。</span><span class="sxs-lookup"><span data-stu-id="179f3-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="179f3-140">EmptyResult-不表示任何结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="179f3-141">RedirectResult-表示重定向到新的 URL。</span><span class="sxs-lookup"><span data-stu-id="179f3-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="179f3-142">JsonResult-表示可在 AJAX 应用程序中使用的 JavaScript 对象表示法结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="179f3-143">JavaScriptResult-表示 JavaScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="179f3-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="179f3-144">ContentResult-表示文本结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="179f3-145">FileContentResult-表示可下载的文件（包含二进制内容）。</span><span class="sxs-lookup"><span data-stu-id="179f3-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="179f3-146">FilePathResult-表示可下载的文件（具有路径）。</span><span class="sxs-lookup"><span data-stu-id="179f3-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="179f3-147">FileStreamResult-表示可下载的文件（带有文件流）。</span><span class="sxs-lookup"><span data-stu-id="179f3-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="179f3-148">所有这些操作结果都从基本 ActionResult 类继承。</span><span class="sxs-lookup"><span data-stu-id="179f3-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="179f3-149">在大多数情况下，控制器操作返回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="179f3-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="179f3-150">例如，清单2中的索引控制器操作返回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="179f3-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="179f3-151">**列表 2-Controllers\BookController.vb**</span><span class="sxs-lookup"><span data-stu-id="179f3-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="179f3-152">当操作返回 ViewResult 时，会将 HTML 返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="179f3-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="179f3-153">清单2中的 Index （）方法会将名为 Index 的视图返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="179f3-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="179f3-154">请注意，清单2中的 Index （）操作不返回 ViewResult （）。</span><span class="sxs-lookup"><span data-stu-id="179f3-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="179f3-155">相反，控制器基类的 View （）方法会被调用。</span><span class="sxs-lookup"><span data-stu-id="179f3-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="179f3-156">通常不会直接返回操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="179f3-157">相反，你可以调用控制器基类的下列方法之一：</span><span class="sxs-lookup"><span data-stu-id="179f3-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="179f3-158">视图-返回 ViewResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="179f3-159">重定向-返回 RedirectResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="179f3-160">RedirectToAction-返回 RedirectToRouteResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="179f3-161">RedirectToRoute-返回 RedirectToRouteResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="179f3-162">Json-返回 JsonResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="179f3-163">JavaScriptResult-返回 JavaScriptResult。</span><span class="sxs-lookup"><span data-stu-id="179f3-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="179f3-164">Content-返回 ContentResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="179f3-165">File-返回 FileContentResult、FilePathResult 或 FileStreamResult，具体取决于传递给方法的参数。</span><span class="sxs-lookup"><span data-stu-id="179f3-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="179f3-166">因此，如果想要将视图返回到浏览器，请调用 View （）方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="179f3-167">若要将用户从一个控制器操作重定向到另一个控制器操作，请调用 RedirectToAction （）方法。</span><span class="sxs-lookup"><span data-stu-id="179f3-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="179f3-168">例如，"清单 3" 中的 "详细信息" （）操作显示视图或将用户重定向到 Index （）操作，具体取决于 Id 参数是否具有值。</span><span class="sxs-lookup"><span data-stu-id="179f3-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="179f3-169">**列表 3-Customercontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="179f3-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="179f3-170">ContentResult 操作结果是特殊的。</span><span class="sxs-lookup"><span data-stu-id="179f3-170">The ContentResult action result is special.</span></span> <span data-ttu-id="179f3-171">你可以使用 ContentResult 操作结果以纯文本形式返回操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="179f3-172">例如，列表4中的 Index （）方法以纯文本而不是 HTML 格式返回一条消息。</span><span class="sxs-lookup"><span data-stu-id="179f3-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="179f3-173">**列表 4-Controllers\StatusController.vb**</span><span class="sxs-lookup"><span data-stu-id="179f3-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="179f3-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="179f3-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="179f3-175">System.Web.Mvc.Controller</span><span class="sxs-lookup"><span data-stu-id="179f3-175">System.Web.Mvc.Controller</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="179f3-176">调用 StatusController （）操作时，不会返回视图。</span><span class="sxs-lookup"><span data-stu-id="179f3-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="179f3-177">相反，原始文本 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="179f3-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="179f3-178">返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="179f3-178">is returned to the browser.</span></span>

<span data-ttu-id="179f3-179">如果控制器操作返回的结果不是操作结果（例如，日期或整数），结果将自动包装在 ContentResult 中。</span><span class="sxs-lookup"><span data-stu-id="179f3-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="179f3-180">例如，当调用列表5中 WorkController 的 Index （）操作时，日期会自动返回为 ContentResult。</span><span class="sxs-lookup"><span data-stu-id="179f3-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="179f3-181">**列表 5-WorkController**</span><span class="sxs-lookup"><span data-stu-id="179f3-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="179f3-182">列表5中的 Index （）操作返回 DateTime 对象。</span><span class="sxs-lookup"><span data-stu-id="179f3-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="179f3-183">ASP.NET MVC 框架将 DateTime 对象转换为字符串，并自动在 ContentResult 中包装 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="179f3-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="179f3-184">浏览器以纯文本形式接收日期和时间。</span><span class="sxs-lookup"><span data-stu-id="179f3-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="179f3-185">摘要</span><span class="sxs-lookup"><span data-stu-id="179f3-185">Summary</span></span>

<span data-ttu-id="179f3-186">本教程的目的是介绍 ASP.NET MVC 控制器、控制器操作和控制器操作结果的概念。</span><span class="sxs-lookup"><span data-stu-id="179f3-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="179f3-187">在第一部分中，您学习了如何将新的控制器添加到 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="179f3-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="179f3-188">接下来，已了解控制器的公共方法如何作为控制器操作公开给 universe。</span><span class="sxs-lookup"><span data-stu-id="179f3-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="179f3-189">最后，我们讨论了可从控制器操作返回的不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="179f3-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="179f3-190">具体而言，我们讨论了如何从控制器操作返回 ViewResult、RedirectToActionResult 和 ContentResult。</span><span class="sxs-lookup"><span data-stu-id="179f3-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="179f3-191">[上一页](creating-a-custom-route-constraint-cs.md)
> [下一页](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="179f3-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
