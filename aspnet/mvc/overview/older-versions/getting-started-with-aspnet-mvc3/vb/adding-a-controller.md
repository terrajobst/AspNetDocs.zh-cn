---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: 添加控制器（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434594"
---
# <a name="adding-a-controller-vb"></a><span data-ttu-id="77fd0-103">添加控制器 (VB)</span><span class="sxs-lookup"><span data-stu-id="77fd0-103">Adding a Controller (VB)</span></span>

<span data-ttu-id="77fd0-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="77fd0-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="77fd0-105">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="77fd0-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="77fd0-106">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="77fd0-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="77fd0-107">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="77fd0-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="77fd0-108">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="77fd0-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="77fd0-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="77fd0-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="77fd0-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="77fd0-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="77fd0-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="77fd0-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="77fd0-112">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="77fd0-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="77fd0-113">本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="77fd0-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="77fd0-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="77fd0-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="77fd0-115">如果愿意C#，请切换到本教程的[ C#版本](../cs/adding-a-controller.md)。</span><span class="sxs-lookup"><span data-stu-id="77fd0-115">If you prefer C#, switch to the [C# version](../cs/adding-a-controller.md) of this tutorial.</span></span>

<span data-ttu-id="77fd0-116">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="77fd0-116">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="77fd0-117">MVC 是用于开发应用程序的一种模式，因此，每个部分都有单独的责任：</span><span class="sxs-lookup"><span data-stu-id="77fd0-117">MVC is a pattern for developing applications such that each part has a separate responsibility:</span></span>

- <span data-ttu-id="77fd0-118">模型：应用程序的数据。</span><span class="sxs-lookup"><span data-stu-id="77fd0-118">Model: The data for your application.</span></span>
- <span data-ttu-id="77fd0-119">视图：你的应用程序将用于动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="77fd0-119">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="77fd0-120">控制器：用于处理对应用程序的传入 URL 请求、检索模型数据，然后指定用于呈现客户端响应的视图模板的类。</span><span class="sxs-lookup"><span data-stu-id="77fd0-120">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response to the client.</span></span>

<span data-ttu-id="77fd0-121">我们将在本教程中介绍所有这些概念，并说明如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="77fd0-121">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="77fd0-122">右键单击 "**解决方案资源管理器**中的"*控制器*"文件夹，然后选择"**添加控制器**"，创建新的控制器。</span><span class="sxs-lookup"><span data-stu-id="77fd0-122">Create a new controller by right-clicking the *Controllers* folder in **Solution Explorer** and then selecting **Add Controller**.</span></span>

<span data-ttu-id="77fd0-123">[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77fd0-123">[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="77fd0-124">将新控制器命名 &quot;HelloWorldController&quot; 并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="77fd0-124">Name your new controller &quot;HelloWorldController&quot; and click **Add**.</span></span>

<span data-ttu-id="77fd0-125">[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="77fd0-125">[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="77fd0-126">请注意，在右侧**解决方案资源管理器**，已为你创建了一个名为*HelloWorldController.cs*的新文件，并且该文件在 IDE 中处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="77fd0-126">Notice in **Solution Explorer** on the right that a new file has been created for you named *HelloWorldController.cs* and that the file is open in the IDE.</span></span>

<span data-ttu-id="77fd0-127">在新的 `public class HelloWorldController` 块中，创建两个类似于以下代码的新方法。</span><span class="sxs-lookup"><span data-stu-id="77fd0-127">Inside the new `public class HelloWorldController` block, create two new methods that look like the following code.</span></span> <span data-ttu-id="77fd0-128">作为示例，我们将直接从控制器返回 HTML 字符串。</span><span class="sxs-lookup"><span data-stu-id="77fd0-128">We'll return a string of HTML directly from the controller as an example.</span></span>

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

<span data-ttu-id="77fd0-129">控制器名为 `HelloWorldController`，新的方法名为 `Index`。</span><span class="sxs-lookup"><span data-stu-id="77fd0-129">Your controller is named `HelloWorldController` and your new method is named `Index`.</span></span> <span data-ttu-id="77fd0-130">运行应用程序（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="77fd0-130">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="77fd0-131">浏览器启动后，将 &quot;HelloWorld&quot; 追加到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="77fd0-131">Once your browser has started up, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="77fd0-132">（在我的计算机上，它是 `http://localhost:43246/HelloWorld`）你的浏览器将类似于下面的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="77fd0-132">(On my computer, it's `http://localhost:43246/HelloWorld`) Your browser will look like the screenshot below.</span></span> <span data-ttu-id="77fd0-133">在上面的方法中，代码直接返回了一个字符串。</span><span class="sxs-lookup"><span data-stu-id="77fd0-133">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="77fd0-134">我们告诉系统只需返回一些 HTML，就是这样！</span><span class="sxs-lookup"><span data-stu-id="77fd0-134">We told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="77fd0-135">ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。</span><span class="sxs-lookup"><span data-stu-id="77fd0-135">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="77fd0-136">ASP.NET MVC 使用的默认映射逻辑使用如下格式来控制要调用的代码：</span><span class="sxs-lookup"><span data-stu-id="77fd0-136">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is invoked:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="77fd0-137">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="77fd0-137">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="77fd0-138">因此， */HelloWorld*映射到 `HelloWorldController` 类。</span><span class="sxs-lookup"><span data-stu-id="77fd0-138">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="77fd0-139">URL 的第二部分确定要执行的类的操作方法。</span><span class="sxs-lookup"><span data-stu-id="77fd0-139">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="77fd0-140">因此， */HelloWorld/Index*将导致执行 `HelloWorldController` 类的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="77fd0-140">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="77fd0-141">请注意，我们只需要访问上面的 */HelloWorld* ，默认情况下使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="77fd0-141">Notice that we only had to visit */HelloWorld* above and the `Index` method was used by default.</span></span> <span data-ttu-id="77fd0-142">这是因为，名为 `Index` 的方法是将在控制器上调用的默认方法，如果未显式指定一个方法。</span><span class="sxs-lookup"><span data-stu-id="77fd0-142">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="77fd0-143">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="77fd0-143">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="77fd0-144">`Welcome` 方法将运行并返回字符串 &quot;这是欢迎操作方法 ...&quot;。</span><span class="sxs-lookup"><span data-stu-id="77fd0-144">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="77fd0-145">默认 MVC 映射 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="77fd0-145">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="77fd0-146">对于此 URL，控制器是 `HelloWorld` 的，`Welcome` 为方法。</span><span class="sxs-lookup"><span data-stu-id="77fd0-146">For this URL, the controller is `HelloWorld` and `Welcome` is the method.</span></span> <span data-ttu-id="77fd0-147">尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="77fd0-147">We haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="77fd0-148">让我们略微修改示例，以便我们可以将中的一些参数信息从 URL 传递到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*）。</span><span class="sxs-lookup"><span data-stu-id="77fd0-148">Let's modify the example slightly so that we can pass some parameter information in from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="77fd0-149">将 `Welcome` 方法更改为包含两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="77fd0-149">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="77fd0-150">请注意，我们已使用 VB 可选参数功能，指示如果没有为该参数传递值，则 `numTimes` 参数应默认为1。</span><span class="sxs-lookup"><span data-stu-id="77fd0-150">Note that we've used the VB optional parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

<span data-ttu-id="77fd0-151">运行应用程序并浏览到 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **。**</span><span class="sxs-lookup"><span data-stu-id="77fd0-151">Run your application and browse to `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`**.**</span></span> <span data-ttu-id="77fd0-152">可以为 `name` 和 `numtimes`尝试不同的值。</span><span class="sxs-lookup"><span data-stu-id="77fd0-152">You can try different values for `name` and `numtimes`.</span></span> <span data-ttu-id="77fd0-153">系统会自动将地址栏中的查询字符串中的命名参数映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="77fd0-153">The system automatically maps the named parameters from your query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="77fd0-154">在这两个示例中，控制器都在执行 MVC 的 VC 部分，即视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="77fd0-154">In both these examples the controller has been doing the VC portion of MVC — that is the view and controller work.</span></span> <span data-ttu-id="77fd0-155">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="77fd0-155">The controller is returning HTML directly.</span></span> <span data-ttu-id="77fd0-156">通常，我们不希望控制器直接返回 HTML，因为这对代码而言非常麻烦。</span><span class="sxs-lookup"><span data-stu-id="77fd0-156">Ordinarily we don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="77fd0-157">我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="77fd0-157">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="77fd0-158">我们来看看如何实现此目的。</span><span class="sxs-lookup"><span data-stu-id="77fd0-158">Let's look at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77fd0-159">[上一页](intro-to-aspnet-mvc-3.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="77fd0-159">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
