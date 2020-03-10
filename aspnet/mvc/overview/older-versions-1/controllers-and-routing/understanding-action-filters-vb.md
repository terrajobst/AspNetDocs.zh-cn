---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 了解操作筛选器（VB） |Microsoft Docs
author: microsoft
description: 本教程的目的是说明操作筛选器。 操作筛选器是一个属性，可应用于控制器操作--或整个控制器 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 263658231ccaa7863508c691a3570bc00b9e8039
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486584"
---
# <a name="understanding-action-filters-vb"></a><span data-ttu-id="8cf44-104">了解操作筛选器 (VB)</span><span class="sxs-lookup"><span data-stu-id="8cf44-104">Understanding Action Filters (VB)</span></span>

<span data-ttu-id="8cf44-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8cf44-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8cf44-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="8cf44-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> <span data-ttu-id="8cf44-107">本教程的目的是说明操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="8cf44-108">操作筛选器是一种可应用于控制器操作（或整个控制器）的属性，用于修改操作的执行方式。</span><span class="sxs-lookup"><span data-stu-id="8cf44-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="8cf44-109">了解操作筛选器</span><span class="sxs-lookup"><span data-stu-id="8cf44-109">Understanding Action Filters</span></span>

<span data-ttu-id="8cf44-110">本教程的目的是说明操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="8cf44-111">操作筛选器是一种可应用于控制器操作（或整个控制器）的属性，用于修改操作的执行方式。</span><span class="sxs-lookup"><span data-stu-id="8cf44-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="8cf44-112">ASP.NET MVC 框架包含多个操作筛选器：</span><span class="sxs-lookup"><span data-stu-id="8cf44-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="8cf44-113">OutputCache –此操作筛选器将控制器操作的输出缓存指定的一段时间。</span><span class="sxs-lookup"><span data-stu-id="8cf44-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="8cf44-114">HandleError –此操作筛选器处理控制器操作执行时引发的错误。</span><span class="sxs-lookup"><span data-stu-id="8cf44-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="8cf44-115">授权–此操作筛选器使你可以限制对特定用户或角色的访问。</span><span class="sxs-lookup"><span data-stu-id="8cf44-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="8cf44-116">还可以创建自己的自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="8cf44-117">例如，你可能想要创建自定义操作筛选器以实现自定义身份验证系统。</span><span class="sxs-lookup"><span data-stu-id="8cf44-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="8cf44-118">或者，您可能想要创建一个操作筛选器来修改控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="8cf44-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="8cf44-119">在本教程中，你将了解如何从头开始构建操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="8cf44-120">我们创建了一个日志操作筛选器，该筛选器将操作处理的不同阶段记录到 Visual Studio "输出" 窗口中。</span><span class="sxs-lookup"><span data-stu-id="8cf44-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="8cf44-121">使用操作筛选器</span><span class="sxs-lookup"><span data-stu-id="8cf44-121">Using an Action Filter</span></span>

<span data-ttu-id="8cf44-122">操作筛选器是一个属性。</span><span class="sxs-lookup"><span data-stu-id="8cf44-122">An action filter is an attribute.</span></span> <span data-ttu-id="8cf44-123">您可以将大多数操作筛选器应用于单个控制器操作或整个控制器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="8cf44-124">例如，列表1中的数据控制器公开一个名为 `Index()` 的操作，该操作返回当前时间。</span><span class="sxs-lookup"><span data-stu-id="8cf44-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="8cf44-125">此操作通过 `OutputCache` 操作筛选器修饰。</span><span class="sxs-lookup"><span data-stu-id="8cf44-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="8cf44-126">此筛选器使操作返回的值缓存10秒。</span><span class="sxs-lookup"><span data-stu-id="8cf44-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="8cf44-127">**列表1– `Controllers\DataController.vb`**</span><span class="sxs-lookup"><span data-stu-id="8cf44-127">**Listing 1 – `Controllers\DataController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

<span data-ttu-id="8cf44-128">如果重复调用 `Index()` 操作，方法是在浏览器的地址栏中输入 URL/Data/Index，并多次点击 "刷新" 按钮，则会看到相同的时间为10秒。</span><span class="sxs-lookup"><span data-stu-id="8cf44-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="8cf44-129">`Index()` 操作的输出将缓存10秒（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="8cf44-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="8cf44-130">[![缓存时间](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8cf44-130">[![Cached time](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span></span>

<span data-ttu-id="8cf44-131">**图 01**：缓存时间（[单击以查看完全大小的图像](understanding-action-filters-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="8cf44-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-vb/_static/image3.png))</span></span>

<span data-ttu-id="8cf44-132">在列表1中，单个操作筛选器– `OutputCache` 操作筛选器–应用于 `Index()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="8cf44-133">如果需要，可以将多个操作筛选器应用于同一操作。</span><span class="sxs-lookup"><span data-stu-id="8cf44-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="8cf44-134">例如，你可能想要将 `OutputCache` 和 `HandleError` 操作筛选器应用于同一操作。</span><span class="sxs-lookup"><span data-stu-id="8cf44-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="8cf44-135">在列表1中，`OutputCache` 操作筛选器将应用于 `Index()` 操作。</span><span class="sxs-lookup"><span data-stu-id="8cf44-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="8cf44-136">您还可以将此特性应用于 `DataController` 类本身。</span><span class="sxs-lookup"><span data-stu-id="8cf44-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="8cf44-137">在这种情况下，由控制器公开的任何操作返回的结果将缓存10秒。</span><span class="sxs-lookup"><span data-stu-id="8cf44-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="8cf44-138">不同类型的筛选器</span><span class="sxs-lookup"><span data-stu-id="8cf44-138">The Different Types of Filters</span></span>

<span data-ttu-id="8cf44-139">ASP.NET MVC 框架支持四种不同类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="8cf44-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="8cf44-140">授权筛选器–实现 `IAuthorizationFilter` 特性。</span><span class="sxs-lookup"><span data-stu-id="8cf44-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="8cf44-141">操作筛选器–实现 `IActionFilter` 特性。</span><span class="sxs-lookup"><span data-stu-id="8cf44-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="8cf44-142">结果筛选器–实现 `IResultFilter` 特性。</span><span class="sxs-lookup"><span data-stu-id="8cf44-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="8cf44-143">异常筛选器–实现 `IExceptionFilter` 特性。</span><span class="sxs-lookup"><span data-stu-id="8cf44-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="8cf44-144">筛选器按照上面列出的顺序执行。</span><span class="sxs-lookup"><span data-stu-id="8cf44-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="8cf44-145">例如，始终先执行授权筛选器，然后在每个其他类型的筛选器之后始终执行操作筛选器和异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="8cf44-146">授权筛选器用于实现控制器操作的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="8cf44-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="8cf44-147">例如，授权筛选器就是授权筛选器的一个示例。</span><span class="sxs-lookup"><span data-stu-id="8cf44-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="8cf44-148">操作筛选器包含执行控制器操作之前和之后执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="8cf44-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="8cf44-149">例如，可以使用操作筛选器来修改控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="8cf44-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="8cf44-150">结果筛选器包含执行视图结果之前和之后执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="8cf44-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="8cf44-151">例如，你可能想要在视图呈现给浏览器之前修改视图结果。</span><span class="sxs-lookup"><span data-stu-id="8cf44-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="8cf44-152">异常筛选器是要运行的最后一类筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="8cf44-153">您可以使用异常筛选器来处理控制器操作或控制器操作结果引发的错误。</span><span class="sxs-lookup"><span data-stu-id="8cf44-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="8cf44-154">还可以使用异常筛选器记录错误。</span><span class="sxs-lookup"><span data-stu-id="8cf44-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="8cf44-155">每种不同类型的筛选器都按特定顺序执行。</span><span class="sxs-lookup"><span data-stu-id="8cf44-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="8cf44-156">如果要控制执行相同类型的筛选器的顺序，则可以设置筛选器的 Order 属性。</span><span class="sxs-lookup"><span data-stu-id="8cf44-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="8cf44-157">所有操作筛选器的基类都是 `System.Web.Mvc.FilterAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="8cf44-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="8cf44-158">如果要实现特定类型的筛选器，则需要创建一个继承自基本筛选器类的类，并实现一个或多个 IAuthorizationFilter、IActionFilter、IResultFilter 或 ExceptionFilter 接口。</span><span class="sxs-lookup"><span data-stu-id="8cf44-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the IAuthorizationFilter, IActionFilter, IResultFilter, or ExceptionFilter interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="8cf44-159">基本 ActionFilterAttribute 类</span><span class="sxs-lookup"><span data-stu-id="8cf44-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="8cf44-160">为了使你能够更轻松地实现自定义操作筛选器，ASP.NET MVC 框架包含一个基本 `ActionFilterAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="8cf44-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="8cf44-161">此类同时实现 `IActionFilter` 和 `IResultFilter` 接口，并继承自 `Filter` 类。</span><span class="sxs-lookup"><span data-stu-id="8cf44-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="8cf44-162">此处的术语并不完全一致。</span><span class="sxs-lookup"><span data-stu-id="8cf44-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="8cf44-163">从技术上说，继承自 ActionFilterAttribute 类的类既是操作筛选器，也是结果筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="8cf44-164">但是，在松散意义上，word 操作筛选器用于引用 ASP.NET MVC 框架中的任何类型的筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="8cf44-165">基本 ActionFilterAttribute 类具有以下可重写的方法：</span><span class="sxs-lookup"><span data-stu-id="8cf44-165">The base ActionFilterAttribute class has the following methods that you can override:</span></span>

- <span data-ttu-id="8cf44-166">OnActionExecuting –在执行控制器操作之前调用此方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="8cf44-167">OnActionExecuted –在执行控制器操作后调用此方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="8cf44-168">OnResultExecuting –在执行控制器操作结果之前调用此方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="8cf44-169">OnResultExecuted –在执行控制器操作结果后调用此方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="8cf44-170">在下一部分中，我们将了解如何实现上述每种不同的方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="8cf44-171">创建日志操作筛选器</span><span class="sxs-lookup"><span data-stu-id="8cf44-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="8cf44-172">为了说明如何生成自定义操作筛选器，我们将创建一个自定义操作筛选器，用于将处理控制器操作的阶段记录到 Visual Studio "输出" 窗口中。</span><span class="sxs-lookup"><span data-stu-id="8cf44-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="8cf44-173">我们的 `LogActionFilter` 包含在清单2中。</span><span class="sxs-lookup"><span data-stu-id="8cf44-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="8cf44-174">**列表2– `ActionFilters\LogActionFilter.vb`**</span><span class="sxs-lookup"><span data-stu-id="8cf44-174">**Listing 2 – `ActionFilters\LogActionFilter.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

<span data-ttu-id="8cf44-175">在列表2中，`OnActionExecuting()`、`OnActionExecuted()`、`OnResultExecuting()`和 `OnResultExecuted()` 方法均调用 `Log()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="8cf44-176">方法的名称和当前路由数据将传递到 `Log()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8cf44-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="8cf44-177">`Log()` 方法将消息写入 Visual Studio 输出窗口（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="8cf44-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="8cf44-178">[![写入 Visual Studio 输出窗口](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8cf44-178">[![Writing to the Visual Studio Output window](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span></span>

<span data-ttu-id="8cf44-179">**图 02**：写入到 Visual Studio "输出" 窗口（[单击以查看完全大小的图像](understanding-action-filters-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="8cf44-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-vb/_static/image6.png))</span></span>

<span data-ttu-id="8cf44-180">列表3中的 Home 控制器说明了如何对整个控制器类应用日志操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="8cf44-181">每当调用由 Home 控制器公开的任何操作时（`Index()` 方法或 `About()` 方法），处理该操作的阶段都将记录到 Visual Studio 的 "输出" 窗口中。</span><span class="sxs-lookup"><span data-stu-id="8cf44-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="8cf44-182">**列表 3-`Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="8cf44-182">**Listing 3 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a><span data-ttu-id="8cf44-183">摘要</span><span class="sxs-lookup"><span data-stu-id="8cf44-183">Summary</span></span>

<span data-ttu-id="8cf44-184">本教程介绍了如何 ASP.NET MVC 操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="8cf44-185">已了解四种不同类型的筛选器：授权筛选器、操作筛选器、结果筛选器和异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="8cf44-186">还了解了基本 `ActionFilterAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="8cf44-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="8cf44-187">最后，您学习了如何实现简单的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8cf44-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="8cf44-188">我们创建了一个日志操作筛选器，该筛选器将处理控制器操作的阶段记录到 Visual Studio "输出" 窗口中。</span><span class="sxs-lookup"><span data-stu-id="8cf44-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8cf44-189">[上一页](asp-net-mvc-routing-overview-vb.md)
> [下一页](improving-performance-with-output-caching-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8cf44-189">[Previous](asp-net-mvc-routing-overview-vb.md)
[Next](improving-performance-with-output-caching-vb.md)</span></span>
