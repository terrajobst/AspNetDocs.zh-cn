---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 添加控制器（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457816"
---
# <a name="adding-a-controller-c"></a><span data-ttu-id="72d5f-103">添加控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="72d5f-103">Adding a Controller (C#)</span></span>

<span data-ttu-id="72d5f-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="72d5f-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="72d5f-105">[此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="72d5f-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="72d5f-106">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="72d5f-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="72d5f-107">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="72d5f-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="72d5f-108">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="72d5f-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="72d5f-109">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="72d5f-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="72d5f-110">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="72d5f-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="72d5f-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="72d5f-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="72d5f-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="72d5f-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="72d5f-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="72d5f-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="72d5f-114">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="72d5f-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="72d5f-115">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="72d5f-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="72d5f-116">[下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="72d5f-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="72d5f-117">如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="72d5f-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="72d5f-118">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="72d5f-118">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="72d5f-119">MVC 是一种用于开发设计良好且易于维护的应用程序的模式。</span><span class="sxs-lookup"><span data-stu-id="72d5f-119">MVC is a pattern for developing applications that are well architected and easy to maintain.</span></span> <span data-ttu-id="72d5f-120">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="72d5f-120">MVC-based applications contain:</span></span>

- <span data-ttu-id="72d5f-121">控制器：用于处理对应用程序的传入请求、检索模型数据，然后指定将响应返回客户端的视图模板的类。</span><span class="sxs-lookup"><span data-stu-id="72d5f-121">Controllers: Classes that handle incoming requests to the application, retrieve model data, and then specify view templates that return a response to the client.</span></span>
- <span data-ttu-id="72d5f-122">模型：类，这些类表示应用程序的数据，并使用验证逻辑来强制执行该数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="72d5f-122">Models: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="72d5f-123">视图：应用程序用于动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="72d5f-123">Views: Template files that your application uses to dynamically generate HTML responses.</span></span>

<span data-ttu-id="72d5f-124">我们将在本系列教程中介绍所有这些概念，并向您演示如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="72d5f-124">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="72d5f-125">首先，让我们创建一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="72d5f-125">Let's begin by creating a controller class.</span></span> <span data-ttu-id="72d5f-126">在**解决方案资源管理器**中，右键单击 "*控制器*" 文件夹，然后选择 "**添加控制器**"。</span><span class="sxs-lookup"><span data-stu-id="72d5f-126">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

<span data-ttu-id="72d5f-127">将新控制器命名为 "HelloWorldController"。</span><span class="sxs-lookup"><span data-stu-id="72d5f-127">Name your new controller "HelloWorldController".</span></span> <span data-ttu-id="72d5f-128">保留默认模板为**空控制器**，并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="72d5f-128">Leave the default template as **Empty controller** and click **Add**.</span></span>

<span data-ttu-id="72d5f-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="72d5f-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="72d5f-130">请注意，**解决方案资源管理器**已创建名为*HelloWorldController.cs*的新文件。</span><span class="sxs-lookup"><span data-stu-id="72d5f-130">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="72d5f-131">文件在 IDE 中处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="72d5f-131">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="72d5f-132">在 `public class HelloWorldController` 块中，创建两个类似于以下代码的方法。</span><span class="sxs-lookup"><span data-stu-id="72d5f-132">Inside the `public class HelloWorldController` block, create two methods that look like the following code.</span></span> <span data-ttu-id="72d5f-133">控制器将返回 HTML 字符串作为示例。</span><span class="sxs-lookup"><span data-stu-id="72d5f-133">The controller will return a string of HTML as an example.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="72d5f-134">控制器名为 `HelloWorldController`，上面的第一个方法名为 `Index`。</span><span class="sxs-lookup"><span data-stu-id="72d5f-134">Your controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="72d5f-135">让我们从浏览器中调用它。</span><span class="sxs-lookup"><span data-stu-id="72d5f-135">Let's invoke it from a browser.</span></span> <span data-ttu-id="72d5f-136">运行应用程序（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="72d5f-136">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="72d5f-137">在浏览器中，将 "HelloWorld" 追加到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="72d5f-137">In the browser, append "HelloWorld" to the path in the address bar.</span></span> <span data-ttu-id="72d5f-138">（例如，在下图中，它 `http://localhost:43246/HelloWorld.`）浏览器中的页面将类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="72d5f-138">(For example, in the illustration below, it's `http://localhost:43246/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="72d5f-139">在上面的方法中，代码直接返回了一个字符串。</span><span class="sxs-lookup"><span data-stu-id="72d5f-139">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="72d5f-140">你已告诉系统只返回了一些 HTML，但确实返回了！</span><span class="sxs-lookup"><span data-stu-id="72d5f-140">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="72d5f-141">ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。</span><span class="sxs-lookup"><span data-stu-id="72d5f-141">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="72d5f-142">ASP.NET MVC 使用的默认映射逻辑使用如下格式来确定要调用的代码：</span><span class="sxs-lookup"><span data-stu-id="72d5f-142">The default mapping logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="72d5f-143">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="72d5f-143">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="72d5f-144">因此， */HelloWorld*映射到 `HelloWorldController` 类。</span><span class="sxs-lookup"><span data-stu-id="72d5f-144">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="72d5f-145">URL 的第二部分确定要执行的类的操作方法。</span><span class="sxs-lookup"><span data-stu-id="72d5f-145">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="72d5f-146">因此， */HelloWorld/Index*将导致执行 `HelloWorldController` 类的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="72d5f-146">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="72d5f-147">请注意，我们只需要浏览到 */HelloWorld* ，并且默认使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="72d5f-147">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="72d5f-148">这是因为，名为 `Index` 的方法是将在控制器上调用的默认方法，如果未显式指定一个方法。</span><span class="sxs-lookup"><span data-stu-id="72d5f-148">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="72d5f-149">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="72d5f-149">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="72d5f-150">`Welcome` 方法运行并返回字符串“这是 Welcome 操作方法...”。</span><span class="sxs-lookup"><span data-stu-id="72d5f-150">The `Welcome` method runs and returns the string "This is the Welcome action method...".</span></span> <span data-ttu-id="72d5f-151">默认 MVC 映射 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="72d5f-151">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="72d5f-152">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="72d5f-152">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="72d5f-153">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="72d5f-153">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="72d5f-154">让我们略微修改示例，以便可以将一些参数信息从 URL 传递到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*）。</span><span class="sxs-lookup"><span data-stu-id="72d5f-154">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="72d5f-155">将 `Welcome` 方法更改为包含两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="72d5f-155">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="72d5f-156">请注意，该代码使用C#可选的参数功能，指示如果没有为该参数传递值，则 `numTimes` 参数应默认为1。</span><span class="sxs-lookup"><span data-stu-id="72d5f-156">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="72d5f-157">运行应用程序并浏览到示例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="72d5f-157">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="72d5f-158">可在 URL 中对 `name` 和 `numtimes` 使用其他值。</span><span class="sxs-lookup"><span data-stu-id="72d5f-158">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="72d5f-159">系统自动将命名参数从地址栏中的查询字符串映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="72d5f-159">The system automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="72d5f-160">在这两个示例中，控制器都在执行 MVC 的 "VC" 部分，即视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="72d5f-160">In both these examples the controller has been doing the "VC" portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="72d5f-161">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="72d5f-161">The controller is returning HTML directly.</span></span> <span data-ttu-id="72d5f-162">通常情况下，你不希望控制器直接返回 HTML，因为这会对代码非常麻烦。</span><span class="sxs-lookup"><span data-stu-id="72d5f-162">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="72d5f-163">我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="72d5f-163">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="72d5f-164">接下来，我们来看看如何实现此目的。</span><span class="sxs-lookup"><span data-stu-id="72d5f-164">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="72d5f-165">[上一页](intro-to-aspnet-mvc-3.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="72d5f-165">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
