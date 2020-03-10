---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和视图实现列表/详细信息 UI |Microsoft Docs
author: microsoft
description: 步骤4显示了如何将控制器添加到应用程序，该应用程序利用我们的模型为用户提供数据列表/详细信息导航体验 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486218"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="baa59-103">使用控制器和视图实现列表/详细信息 UI</span><span class="sxs-lookup"><span data-stu-id="baa59-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="baa59-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="baa59-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="baa59-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="baa59-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="baa59-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第4步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="baa59-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="baa59-107">步骤4显示了如何将控制器添加到应用程序，该应用程序利用我们的模型为用户提供针对 NerdDinner 站点上的就的数据列表/详细信息导航体验。</span><span class="sxs-lookup"><span data-stu-id="baa59-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="baa59-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="baa59-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="baa59-109">NerdDinner 步骤4：控制器和视图</span><span class="sxs-lookup"><span data-stu-id="baa59-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="baa59-110">对于传统的 web 框架（经典 ASP、PHP、ASP.NET Web 窗体等），传入 Url 通常映射到磁盘上的文件。</span><span class="sxs-lookup"><span data-stu-id="baa59-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="baa59-111">例如： "/Products.aspx" 或 "/Products.php" 等 URL 请求可能由 "Products" 或 "Products" 文件处理。</span><span class="sxs-lookup"><span data-stu-id="baa59-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="baa59-112">基于 Web 的 MVC 框架以略有不同的方式将 Url 映射到服务器代码。</span><span class="sxs-lookup"><span data-stu-id="baa59-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="baa59-113">它们不会将传入 Url 映射到文件，而是将 Url 映射到类的方法。</span><span class="sxs-lookup"><span data-stu-id="baa59-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="baa59-114">这些类称为 "控制器"，它们负责处理传入的 HTTP 请求，处理用户输入，检索和保存数据，确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他URL，等等）。</span><span class="sxs-lookup"><span data-stu-id="baa59-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="baa59-115">现在，我们已经为 NerdDinner 应用程序构建了一个基本模型，接下来我们要将一个控制器添加到该应用程序，该应用程序利用它来向用户提供针对网站上的就的数据列表/详细信息导航体验。</span><span class="sxs-lookup"><span data-stu-id="baa59-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="baa59-116">添加 DinnersController 控制器</span><span class="sxs-lookup"><span data-stu-id="baa59-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="baa59-117">首先，右键单击 web 项目中的 "控制器" 文件夹，然后选择 " **&gt;控制器**" 菜单命令（还可以通过键入 Ctrl-M、Ctrl-C 来执行此命令）：</span><span class="sxs-lookup"><span data-stu-id="baa59-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="baa59-118">这会显示 "添加控制器" 对话框：</span><span class="sxs-lookup"><span data-stu-id="baa59-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="baa59-119">我们会将新控制器命名为 "DinnersController"，并单击 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="baa59-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="baa59-120">然后，Visual Studio 会在我们的 \Controllers 目录下添加 DinnersController.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="baa59-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="baa59-121">它还将在代码编辑器中打开新的 DinnersController 类。</span><span class="sxs-lookup"><span data-stu-id="baa59-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="baa59-122">向 DinnersController 类添加 Index （）和 Details （）操作方法</span><span class="sxs-lookup"><span data-stu-id="baa59-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="baa59-123">我们想要使用我们的应用程序启用访问者来浏览即将到来的就列表，并允许他们单击列表中的任何晚餐来查看有关它的特定详细信息。</span><span class="sxs-lookup"><span data-stu-id="baa59-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="baa59-124">我们将通过从应用程序发布以下 Url 来实现此目的：</span><span class="sxs-lookup"><span data-stu-id="baa59-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="baa59-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="baa59-125">**URL**</span></span> | <span data-ttu-id="baa59-126">**目的**</span><span class="sxs-lookup"><span data-stu-id="baa59-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="baa59-127">*就*</span><span class="sxs-lookup"><span data-stu-id="baa59-127">*/Dinners/*</span></span> | <span data-ttu-id="baa59-128">显示即将发布的就的 HTML 列表</span><span class="sxs-lookup"><span data-stu-id="baa59-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="baa59-129">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="baa59-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="baa59-130">显示在 URL 中嵌入的 "id" 参数所指示的特定晚餐的详细信息-这将与数据库中晚餐的 DinnerID 匹配。</span><span class="sxs-lookup"><span data-stu-id="baa59-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="baa59-131">例如：/Dinners/Details/2 会显示一个 HTML 页面，其中包含有关其 DinnerID 值为2的晚餐的详细信息。</span><span class="sxs-lookup"><span data-stu-id="baa59-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="baa59-132">我们将通过将两个公共 "操作方法" 添加到 DinnersController 类（如下所示），发布这些 Url 的初始实现：</span><span class="sxs-lookup"><span data-stu-id="baa59-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="baa59-133">接下来，我们将运行 NerdDinner 应用程序，并使用浏览器对其进行调用。</span><span class="sxs-lookup"><span data-stu-id="baa59-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="baa59-134">键入 *"/Dinners/"* URL 将导致*Index （）* 方法运行，并且该方法将返回以下响应：</span><span class="sxs-lookup"><span data-stu-id="baa59-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="baa59-135">键入 *"/Dinners/Details/2"* URL 将导致*详细信息（）* 方法运行，并发送回以下响应：</span><span class="sxs-lookup"><span data-stu-id="baa59-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="baa59-136">您可能想知道，ASP.NET MVC 如何知道如何创建 DinnersController 类并调用这些方法呢？</span><span class="sxs-lookup"><span data-stu-id="baa59-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="baa59-137">若要了解如何使用路由，请快速了解路由的工作原理。</span><span class="sxs-lookup"><span data-stu-id="baa59-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="baa59-138">了解 ASP.NET MVC 路由</span><span class="sxs-lookup"><span data-stu-id="baa59-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="baa59-139">ASP.NET MVC 包含一个功能强大的 URL 路由引擎，该引擎在控制 Url 映射到控制器类的方式方面提供了很大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="baa59-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="baa59-140">它允许我们完全自定义 ASP.NET MVC 选择要创建的控制器类的方式，对其调用哪个方法，并配置不同的方法来自动分析 URL/Querystring 中的变量，并将这些变量作为参数参数传递给方法。</span><span class="sxs-lookup"><span data-stu-id="baa59-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="baa59-141">它为 SEO （搜索引擎优化）提供完全优化站点的灵活性，并发布应用程序所需的任何 URL 结构。</span><span class="sxs-lookup"><span data-stu-id="baa59-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="baa59-142">默认情况下，新的 ASP.NET MVC 项目附带了已注册的一组预配置的 URL 路由规则。</span><span class="sxs-lookup"><span data-stu-id="baa59-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="baa59-143">这样，我们就可以轻松地开始使用应用程序，而无需显式配置任何内容。</span><span class="sxs-lookup"><span data-stu-id="baa59-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="baa59-144">可以在我们的项目的 "应用程序" 类中找到默认路由规则注册，可以通过在项目的根目录中双击 "global.asax" 文件来打开这些注册：</span><span class="sxs-lookup"><span data-stu-id="baa59-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="baa59-145">默认的 ASP.NET MVC 路由规则在此类的 "RegisterRoutes" 方法中注册：</span><span class="sxs-lookup"><span data-stu-id="baa59-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="baa59-146">"路由。上面的 Maproute.html （） "方法调用使用 URL 格式注册将传入 Url 映射到控制器类的默认路由规则："/{controller}/{action}/{id} "–其中，" 控制器 "是要实例化的控制器类的名称，" action "是要对其调用的公共方法的名称，而" id "是嵌入在 URL 中的可选参数，可作为参数传递给方法。</span><span class="sxs-lookup"><span data-stu-id="baa59-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="baa59-147">传递给 "Maproute.html （）" 方法调用的第三个参数是在 URL （控制器 = "Home"、Action = "Index"、Id = ""）中不存在的情况下，用于控制器/操作/id 值的默认值集。</span><span class="sxs-lookup"><span data-stu-id="baa59-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="baa59-148">下面的表演示如何使用默认的 "<em>/{controllers}/{action}/{id}"</em>路由规则映射各种 url：</span><span class="sxs-lookup"><span data-stu-id="baa59-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="baa59-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="baa59-149">**URL**</span></span> | <span data-ttu-id="baa59-150">**控制器类**</span><span class="sxs-lookup"><span data-stu-id="baa59-150">**Controller Class**</span></span> | <span data-ttu-id="baa59-151">**操作方法**</span><span class="sxs-lookup"><span data-stu-id="baa59-151">**Action Method**</span></span> | <span data-ttu-id="baa59-152">**传递的参数**</span><span class="sxs-lookup"><span data-stu-id="baa59-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="baa59-153">*/Dinners/Details/2*</span><span class="sxs-lookup"><span data-stu-id="baa59-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="baa59-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="baa59-154">DinnersController</span></span> | <span data-ttu-id="baa59-155">详细信息（id）</span><span class="sxs-lookup"><span data-stu-id="baa59-155">Details(id)</span></span> | <span data-ttu-id="baa59-156">id=2</span><span class="sxs-lookup"><span data-stu-id="baa59-156">id=2</span></span> |
| <span data-ttu-id="baa59-157">*/Dinners/Edit/5*</span><span class="sxs-lookup"><span data-stu-id="baa59-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="baa59-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="baa59-158">DinnersController</span></span> | <span data-ttu-id="baa59-159">编辑（id）</span><span class="sxs-lookup"><span data-stu-id="baa59-159">Edit(id)</span></span> | <span data-ttu-id="baa59-160">id=5</span><span class="sxs-lookup"><span data-stu-id="baa59-160">id=5</span></span> |
| <span data-ttu-id="baa59-161">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="baa59-161">*/Dinners/Create*</span></span> | <span data-ttu-id="baa59-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="baa59-162">DinnersController</span></span> | <span data-ttu-id="baa59-163">Create()</span><span class="sxs-lookup"><span data-stu-id="baa59-163">Create()</span></span> | <span data-ttu-id="baa59-164">不适用</span><span class="sxs-lookup"><span data-stu-id="baa59-164">N/A</span></span> |
| <span data-ttu-id="baa59-165">*/Dinners*</span><span class="sxs-lookup"><span data-stu-id="baa59-165">*/Dinners*</span></span> | <span data-ttu-id="baa59-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="baa59-166">DinnersController</span></span> | <span data-ttu-id="baa59-167">Index （）</span><span class="sxs-lookup"><span data-stu-id="baa59-167">Index()</span></span> | <span data-ttu-id="baa59-168">不适用</span><span class="sxs-lookup"><span data-stu-id="baa59-168">N/A</span></span> |
| <span data-ttu-id="baa59-169">*/Home*</span><span class="sxs-lookup"><span data-stu-id="baa59-169">*/Home*</span></span> | <span data-ttu-id="baa59-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="baa59-170">HomeController</span></span> | <span data-ttu-id="baa59-171">Index （）</span><span class="sxs-lookup"><span data-stu-id="baa59-171">Index()</span></span> | <span data-ttu-id="baa59-172">不适用</span><span class="sxs-lookup"><span data-stu-id="baa59-172">N/A</span></span> |
| */* | <span data-ttu-id="baa59-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="baa59-173">HomeController</span></span> | <span data-ttu-id="baa59-174">Index （）</span><span class="sxs-lookup"><span data-stu-id="baa59-174">Index()</span></span> | <span data-ttu-id="baa59-175">不适用</span><span class="sxs-lookup"><span data-stu-id="baa59-175">N/A</span></span> |

<span data-ttu-id="baa59-176">最后三行显示使用的默认值（Controller = Home，Action = Index，Id = ""）。</span><span class="sxs-lookup"><span data-stu-id="baa59-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="baa59-177">由于已将 "Index" 方法注册为默认操作名称（如果未指定），因此 "/Dinners" 和 "/Home" Url 会使 Index （）操作方法在其控制器类上调用。</span><span class="sxs-lookup"><span data-stu-id="baa59-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="baa59-178">由于 "Home" 控制器注册为默认控制器（如果未指定），因此 "/" URL 将导致创建 HomeController，并对其调用 Index （）操作方法。</span><span class="sxs-lookup"><span data-stu-id="baa59-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="baa59-179">如果你不喜欢这些默认的 URL 路由规则，好消息就是可以轻松地更改-只需在上面的 RegisterRoutes 方法中编辑它们即可。</span><span class="sxs-lookup"><span data-stu-id="baa59-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="baa59-180">但对于我们的 NerdDinner 应用程序，我们不会更改任何默认的 URL 路由规则，而只是将其按原样使用。</span><span class="sxs-lookup"><span data-stu-id="baa59-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="baa59-181">使用我们的 DinnersController 中的 DinnerRepository</span><span class="sxs-lookup"><span data-stu-id="baa59-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="baa59-182">现在，我们将 DinnersController 的 Index （）和 Details （）操作方法的当前实现替换为使用我们的模型的实现。</span><span class="sxs-lookup"><span data-stu-id="baa59-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="baa59-183">我们将使用我们之前构建的 DinnerRepository 类来实现该行为。</span><span class="sxs-lookup"><span data-stu-id="baa59-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="baa59-184">首先，我们将添加一个引用 "NerdDinner" 命名空间的 "using" 语句，然后将 DinnerRepository 的实例声明为 DinnerController 类中的字段。</span><span class="sxs-lookup"><span data-stu-id="baa59-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="baa59-185">本章稍后将介绍 "依赖关系注入" 的概念，并为我们的控制器提供了另一种方法来获取对 DinnerRepository 的引用以实现更好的单元测试，但现在我们只需创建 DinnerRepository 的实例。与下面类似。</span><span class="sxs-lookup"><span data-stu-id="baa59-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="baa59-186">现在，我们已准备好使用检索到的数据模型对象生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="baa59-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="baa59-187">通过控制器使用视图</span><span class="sxs-lookup"><span data-stu-id="baa59-187">Using Views with our Controller</span></span>

<span data-ttu-id="baa59-188">尽管可以在操作方法中编写代码来汇编 HTML，然后使用*Response （）* helper 方法将其发送回客户端，但这种方法很快就会变得相当困难。</span><span class="sxs-lookup"><span data-stu-id="baa59-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="baa59-189">更好的方法是，仅在 DinnersController 操作方法中执行应用程序和数据逻辑，然后将呈现 HTML 响应所需的数据传递给单独的 "视图" 模板，该模板负责输出 HTML 表示形式的。</span><span class="sxs-lookup"><span data-stu-id="baa59-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="baa59-190">正如我们稍后将看到的，"视图" 模板是文本文件，通常包含 HTML 标记和嵌入的呈现代码的组合。</span><span class="sxs-lookup"><span data-stu-id="baa59-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="baa59-191">从视图呈现中分离我们的控制器逻辑带来了几大好处。</span><span class="sxs-lookup"><span data-stu-id="baa59-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="baa59-192">特别是，它有助于强制在应用程序代码和 UI 格式设置/呈现代码之间进行明确的 "问题分离"。</span><span class="sxs-lookup"><span data-stu-id="baa59-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="baa59-193">这样，就可以更轻松地将应用程序逻辑与 UI 呈现逻辑隔离。</span><span class="sxs-lookup"><span data-stu-id="baa59-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="baa59-194">这样就可以更轻松地修改 UI 呈现模板，而无需更改应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="baa59-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="baa59-195">而且，开发人员和设计人员可以更轻松地协作项目。</span><span class="sxs-lookup"><span data-stu-id="baa59-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="baa59-196">我们可以更新 DinnersController 类，以便通过将两个操作方法的方法签名从 "void" 改为 "ActionResult" 的返回类型，来指示要使用视图模板来发送回 HTML UI 响应。</span><span class="sxs-lookup"><span data-stu-id="baa59-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="baa59-197">然后，可以对控制器基类调用*View （）* helper 方法，以返回如下所示的 "ViewResult" 对象：</span><span class="sxs-lookup"><span data-stu-id="baa59-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="baa59-198">上面使用的*视图（）* 帮助器方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="baa59-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="baa59-199">*View （）* helper 方法的第一个参数是要用于呈现 HTML 响应的视图模板文件的名称。</span><span class="sxs-lookup"><span data-stu-id="baa59-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="baa59-200">第二个参数是一个模型对象，其中包含视图模板呈现 HTML 响应所需的数据。</span><span class="sxs-lookup"><span data-stu-id="baa59-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="baa59-201">在索引（）操作方法中，我们将调用*View （）* helper 方法，并指示我们要使用 "索引" 视图模板呈现就的 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="baa59-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="baa59-202">我们正在向视图模板传递一系列晚餐对象，以生成以下列表：</span><span class="sxs-lookup"><span data-stu-id="baa59-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="baa59-203">在我们的详细信息（）操作方法中，我们尝试使用 URL 内提供的 id 检索晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="baa59-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="baa59-204">如果找到有效的晚餐，我们将调用*View （）* helper 方法，这表示我们想要使用 "详细信息" 视图模板来呈现检索到的晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="baa59-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="baa59-205">如果请求的晚餐无效，我们将呈现一个有用的错误消息，指示不存在使用 "NotFound" 视图模板的晚餐（以及仅采用模板名称的*view （）* helper 方法的重载版本）：</span><span class="sxs-lookup"><span data-stu-id="baa59-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="baa59-206">现在，让我们实现 "NotFound"、"Details" 和 "Index" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="baa59-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="baa59-207">实现 "NotFound" 视图模板</span><span class="sxs-lookup"><span data-stu-id="baa59-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="baa59-208">首先，我们将实现 "NotFound" 视图模板，该模板会显示友好错误消息，指示找不到请求的晚餐。</span><span class="sxs-lookup"><span data-stu-id="baa59-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="baa59-209">我们将通过将文本光标置于控制器操作方法中来创建新的视图模板，然后右键单击并选择 "添加视图" 菜单命令（我们还可以通过键入 Ctrl-M、Ctrl + V）执行此命令：</span><span class="sxs-lookup"><span data-stu-id="baa59-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="baa59-210">这会显示如下所示的 "添加视图" 对话框。</span><span class="sxs-lookup"><span data-stu-id="baa59-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="baa59-211">默认情况下，对话框将预先填充要创建的视图的名称，以匹配启动对话框时光标所在的操作方法的名称（在本例中为 "详细信息"）。</span><span class="sxs-lookup"><span data-stu-id="baa59-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="baa59-212">由于我们要首先实现 "NotFound" 模板，因此我们将覆盖此视图名称，并将其设置为 "NotFound"：</span><span class="sxs-lookup"><span data-stu-id="baa59-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="baa59-213">当我们单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建一个新的 "NotFound" 视图模板（如果目录尚不存在，它也会创建）：</span><span class="sxs-lookup"><span data-stu-id="baa59-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="baa59-214">它还将在代码编辑器中打开新的 "NotFound" 视图模板：</span><span class="sxs-lookup"><span data-stu-id="baa59-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="baa59-215">默认情况下，查看模板具有两个 "内容区域"，可以在其中添加内容和代码。</span><span class="sxs-lookup"><span data-stu-id="baa59-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="baa59-216">第一种是允许我们自定义发送回的 HTML 页面的 "标题"。</span><span class="sxs-lookup"><span data-stu-id="baa59-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="baa59-217">第二种是允许我们自定义发送回的 HTML 页面的 "主要内容"。</span><span class="sxs-lookup"><span data-stu-id="baa59-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="baa59-218">若要实现我们的 "NotFound" 视图模板，我们将添加一些基本内容：</span><span class="sxs-lookup"><span data-stu-id="baa59-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="baa59-219">然后，可以在浏览器中进行尝试。</span><span class="sxs-lookup"><span data-stu-id="baa59-219">We can then try it out within the browser.</span></span> <span data-ttu-id="baa59-220">为此，请请求 *"/Dinners/Details/9999"* URL。</span><span class="sxs-lookup"><span data-stu-id="baa59-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="baa59-221">这将引用数据库中当前不存在的晚餐，并将导致我们的 DinnersController （）操作方法呈现我们的 "NotFound" 视图模板：</span><span class="sxs-lookup"><span data-stu-id="baa59-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="baa59-222">在上面的屏幕截图中，你会注意到，我们的基本视图模板继承了一组围绕屏幕上的主要内容的 HTML。</span><span class="sxs-lookup"><span data-stu-id="baa59-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="baa59-223">这是因为，我们的视图模板使用 "母版页" 模板，使我们能够在网站上的所有视图中应用一致的布局。</span><span class="sxs-lookup"><span data-stu-id="baa59-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="baa59-224">我们将在本教程的后面部分讨论母版页的工作方式。</span><span class="sxs-lookup"><span data-stu-id="baa59-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="baa59-225">实现 "详细信息" 视图模板</span><span class="sxs-lookup"><span data-stu-id="baa59-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="baa59-226">现在，我们实现了 "详细信息" 查看模板，该模板将为单个晚宴型号生成 HTML。</span><span class="sxs-lookup"><span data-stu-id="baa59-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="baa59-227">为此，我们将文本游标定位到详细信息操作方法，然后右键单击并选择 "添加视图" 菜单命令（或按 Ctrl-M、Ctrl + V）：</span><span class="sxs-lookup"><span data-stu-id="baa59-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="baa59-228">此时将显示 "添加视图" 对话框。</span><span class="sxs-lookup"><span data-stu-id="baa59-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="baa59-229">我们将保留默认视图名称（"详细信息"）。</span><span class="sxs-lookup"><span data-stu-id="baa59-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="baa59-230">还将在对话框中选中 "创建强类型视图" 复选框，并选择（使用 combobox 下拉列表）要从控制器传递到视图的模型类型的名称。</span><span class="sxs-lookup"><span data-stu-id="baa59-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="baa59-231">在此视图中，我们将传递晚餐对象（该类型的完全限定名称为 "NerdDinner"）：</span><span class="sxs-lookup"><span data-stu-id="baa59-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="baa59-232">与上一个模板不同，我们选择创建一个 "空视图"，这次我们将选择使用 "详细信息" 模板自动 "基架" 视图。</span><span class="sxs-lookup"><span data-stu-id="baa59-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="baa59-233">为此，我们可以在上面的对话框中更改 "查看内容" 下拉标记。</span><span class="sxs-lookup"><span data-stu-id="baa59-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="baa59-234">"基架" 会根据传递给它的晚餐对象，生成详细信息视图模板的初始实现。</span><span class="sxs-lookup"><span data-stu-id="baa59-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="baa59-235">这为我们提供了一种简单的方法，让我们快速开始使用视图模板实现。</span><span class="sxs-lookup"><span data-stu-id="baa59-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="baa59-236">单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建新的 "Details .aspx" 视图模板文件：</span><span class="sxs-lookup"><span data-stu-id="baa59-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="baa59-237">它还将在代码编辑器中打开新的 "Details .aspx" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="baa59-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="baa59-238">它将包含基于晚宴型号的详细信息视图的初始基架实现。</span><span class="sxs-lookup"><span data-stu-id="baa59-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="baa59-239">基架引擎使用 .NET 反射来查看公开给该类的公共属性，并基于它找到的每个类型添加适当的内容：</span><span class="sxs-lookup"><span data-stu-id="baa59-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="baa59-240">我们可以请求 *"/Dinners/Details/1"* URL 来查看此 "详细信息" 基架实现在浏览器中的外观。</span><span class="sxs-lookup"><span data-stu-id="baa59-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="baa59-241">使用此 URL 将显示我们在第一次创建数据库时手动添加到数据库中的就之一：</span><span class="sxs-lookup"><span data-stu-id="baa59-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="baa59-242">这会使我们快速启动并运行，并提供我们的详细信息 .aspx 视图的初始实现。</span><span class="sxs-lookup"><span data-stu-id="baa59-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="baa59-243">接下来，我们可以对其进行调整，以自定义 UI 以实现满意。</span><span class="sxs-lookup"><span data-stu-id="baa59-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="baa59-244">当我们更密切地查看详细信息 .aspx 模板时，我们会发现它包含静态 HTML 和嵌入的呈现代码。</span><span class="sxs-lookup"><span data-stu-id="baa59-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="baa59-245">&lt;%%&gt; 代码片段在视图模板呈现时执行代码，&lt;% =%&gt; 代码片段执行其中包含的代码，然后将结果呈现给模板的输出流。</span><span class="sxs-lookup"><span data-stu-id="baa59-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="baa59-246">我们可以在视图中编写代码，以便访问使用强类型 "模型" 属性从控制器传入的 "晚餐" 模型对象。</span><span class="sxs-lookup"><span data-stu-id="baa59-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="baa59-247">当在编辑器中访问此 "模型" 属性时，Visual Studio 将为我们提供完整的代码-intellisense：</span><span class="sxs-lookup"><span data-stu-id="baa59-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="baa59-248">让我们进行一些调整，以便最终详细信息视图模板的源如下所示：</span><span class="sxs-lookup"><span data-stu-id="baa59-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="baa59-249">当我们再次访问 *"/Dinners/Details/1"* URL 时，它现在将如下所示：</span><span class="sxs-lookup"><span data-stu-id="baa59-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="baa59-250">实现 "索引" 视图模板</span><span class="sxs-lookup"><span data-stu-id="baa59-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="baa59-251">现在，我们实现 "索引" 视图模板，该模板将生成即将发布的就的列表。</span><span class="sxs-lookup"><span data-stu-id="baa59-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="baa59-252">为此，我们将文本光标置于 Index 操作方法中，然后右键单击并选择 "添加视图" 菜单命令（或按 Ctrl-M、Ctrl + V）。</span><span class="sxs-lookup"><span data-stu-id="baa59-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="baa59-253">在 "添加视图" 对话框中，我们将保留名为 "Index" 的视图模板，并选中 "创建强类型视图" 复选框。</span><span class="sxs-lookup"><span data-stu-id="baa59-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="baa59-254">这一次，我们将选择自动生成 "列表" 视图模板，并选择 "NerdDinner" 作为传递到该视图的模型类型（这是因为我们指出我们要创建 "List" 基架，这将导致 "添加视图" 对话框假设我们将晚餐对象序列从控制器传递到视图）：</span><span class="sxs-lookup"><span data-stu-id="baa59-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="baa59-255">单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建一个新的 "Index .aspx" 视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="baa59-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="baa59-256">它将 "基架" 其中的初始实现，该实现提供传递到视图的就的 HTML 表列表。</span><span class="sxs-lookup"><span data-stu-id="baa59-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="baa59-257">当我们运行应用程序并访问 *"/Dinners/"* URL 时，它会呈现就的列表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="baa59-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="baa59-258">上面的表解决方案为我们的晚餐数据提供了类似于网格的布局，而这并不是我们想要的面向消费者的晚餐列表。</span><span class="sxs-lookup"><span data-stu-id="baa59-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="baa59-259">我们可以更新 node.js 视图模板，并对其进行修改，以列出更少的数据列，并使用 &lt;ul&gt; 元素，使用下面的代码呈现这些数据，而不是使用表：</span><span class="sxs-lookup"><span data-stu-id="baa59-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="baa59-260">我们将在上述 foreach 语句中使用 "var" 关键字，因为我们循环遍历模型中的每个晚餐。</span><span class="sxs-lookup"><span data-stu-id="baa59-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="baa59-261">不熟悉C# 3.0 的人员可能会认为，使用 "var" 意味着晚餐对象已后期绑定。</span><span class="sxs-lookup"><span data-stu-id="baa59-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="baa59-262">相反，它意味着编译器对强类型 "Model" 属性（其类型为 "IEnumerable&lt;晚宴&gt;"）使用类型推理，并将本地 "晚餐" 变量编译为晚餐类型，这意味着我们将在代码块中获取完整的 intellisense 和编译时检查：</span><span class="sxs-lookup"><span data-stu-id="baa59-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="baa59-263">当我们在浏览器中的 */Dinners* URL 上进行刷新时，更新视图现在如下所示：</span><span class="sxs-lookup"><span data-stu-id="baa59-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="baa59-264">这看起来很好，但目前还没有。</span><span class="sxs-lookup"><span data-stu-id="baa59-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="baa59-265">最后一步是让最终用户在列表中单击各个就，并查看其详细信息。</span><span class="sxs-lookup"><span data-stu-id="baa59-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="baa59-266">我们将通过呈现链接到 DinnersController 上的详细信息操作方法的 HTML hyperlink 元素来实现此操作。</span><span class="sxs-lookup"><span data-stu-id="baa59-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="baa59-267">可以通过以下两种方式之一在索引视图中生成这些超链接。</span><span class="sxs-lookup"><span data-stu-id="baa59-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="baa59-268">第一种方式是手动创建 HTML &lt;如下所示的&gt; 元素，在该元素中，我们将 &lt;%%&gt; 块嵌入到 &lt;的 HTML 元素中：&gt;</span><span class="sxs-lookup"><span data-stu-id="baa59-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="baa59-269">可使用的替代方法是利用 ASP.NET MVC 中的内置 "Html.actionlink （）" 帮助器方法，该方法支持以编程方式创建 HTML &lt;一个链接到控制器上其他操作方法的&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="baa59-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="baa59-270">Html 的第一个参数。 Html.actionlink （）帮助程序方法是要显示的链接文本（在本例中为晚餐的标题），第二个参数是我们要生成链接的控制器操作名称（在本例中为详细信息方法），第三个参数是要发送到操作的一组参数（实现为具有属性名称/值的匿名类型）。</span><span class="sxs-lookup"><span data-stu-id="baa59-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="baa59-271">在这种情况下，我们将指定要链接到的晚餐的 "id" 参数，并因为 ASP.NET MVC 中的默认 URL 路由规则是 "{Controller}/{Action}/{id}"，则 Html.actionlink （） helper 方法将生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="baa59-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="baa59-272">对于我们的索引 .aspx 视图，我们将使用 Html.actionlink （） helper 方法方法，并将列表中的每个晚宴链接到相应的详细信息 URL：</span><span class="sxs-lookup"><span data-stu-id="baa59-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="baa59-273">现在，当我们点击 */Dinners* URL 时，晚餐列表如下所示：</span><span class="sxs-lookup"><span data-stu-id="baa59-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="baa59-274">当我们单击列表中的任何就时，我们将导航以查看其详细信息：</span><span class="sxs-lookup"><span data-stu-id="baa59-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="baa59-275">基于约定的命名和 \Views 目录结构</span><span class="sxs-lookup"><span data-stu-id="baa59-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="baa59-276">ASP.NET MVC 应用程序默认情况下，在解析视图模板时使用基于约定的目录命名结构。</span><span class="sxs-lookup"><span data-stu-id="baa59-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="baa59-277">这允许开发人员在从控制器类内引用视图时避免必须完全限定位置路径。</span><span class="sxs-lookup"><span data-stu-id="baa59-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="baa59-278">默认情况下，ASP.NET MVC 将在应用程序下的 \* \Views\[ControllerName]\* 目录中查找视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="baa59-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="baa59-279">例如，我们一直在处理 DinnersController 类，该类显式引用三个视图模板： "Index"、"Details" 和 "NotFound"。</span><span class="sxs-lookup"><span data-stu-id="baa59-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="baa59-280">ASP.NET MVC 默认情况下会在应用程序根目录下的 *\Views\Dinners*目录中查找这些视图：</span><span class="sxs-lookup"><span data-stu-id="baa59-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="baa59-281">请注意，项目中当前有三个控制器类（DinnersController、HomeController 和 AccountController），默认情况下，在创建项目时添加了最后两个控制器类，其中有三个子目录（每个目录一个控制器）的 \Views。</span><span class="sxs-lookup"><span data-stu-id="baa59-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="baa59-282">从 Home 和 Accounts 控制器引用的视图将自动从各自的 *\Views\Home*和 *\Views\Account*目录解析其视图模板。</span><span class="sxs-lookup"><span data-stu-id="baa59-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="baa59-283">*\Views\Shared*子目录提供一种方式来存储在应用程序内跨多个控制器重复使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="baa59-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="baa59-284">当 ASP.NET MVC 尝试解析视图模板时，它将首先检查 *\Views\[控制器]* 特定的目录，如果找不到该视图模板，它将在 *\Views\Shared*目录中查找。</span><span class="sxs-lookup"><span data-stu-id="baa59-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="baa59-285">命名单独的视图模板时，建议的指导原则是将视图模板与导致其呈现的操作方法共享相同的名称。</span><span class="sxs-lookup"><span data-stu-id="baa59-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="baa59-286">例如，在我们的 "索引" 操作方法之上，使用 "索引" 视图呈现视图结果，并且 "详细信息" 操作方法使用 "详细信息" 视图呈现其结果。</span><span class="sxs-lookup"><span data-stu-id="baa59-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="baa59-287">这样就可以轻松地快速查看与每个操作关联的模板。</span><span class="sxs-lookup"><span data-stu-id="baa59-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="baa59-288">当视图模板与在控制器上调用的操作方法同名时，开发人员无需显式指定视图模板名称。</span><span class="sxs-lookup"><span data-stu-id="baa59-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="baa59-289">只需将 model 对象传递到 "View （）" 帮助器方法（无需指定视图名称），ASP.NET MVC 就会自动推断要使用 *\Views\[ControllerName]\[ActionName]* 查看要呈现的模板。</span><span class="sxs-lookup"><span data-stu-id="baa59-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="baa59-290">这样一来，我们就可以清理控制器代码，避免在代码中重复两次：</span><span class="sxs-lookup"><span data-stu-id="baa59-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="baa59-291">以上代码是为站点实现良好的晚餐列表/详细信息所需的所有内容。</span><span class="sxs-lookup"><span data-stu-id="baa59-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="baa59-292">下一步</span><span class="sxs-lookup"><span data-stu-id="baa59-292">Next Step</span></span>

<span data-ttu-id="baa59-293">我们现在已生成了一个良好的晚餐浏览体验。</span><span class="sxs-lookup"><span data-stu-id="baa59-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="baa59-294">现在，让我们启用 CRUD （创建、读取、更新、删除）数据窗体编辑支持。</span><span class="sxs-lookup"><span data-stu-id="baa59-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="baa59-295">[上一页](build-a-model-with-business-rule-validations.md)
> [下一页](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="baa59-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
