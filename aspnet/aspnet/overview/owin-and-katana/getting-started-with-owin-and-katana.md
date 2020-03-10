---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: 入门与 OWIN 和 Katana |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472442"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="7167d-102">OWIN 和 Katana 入门</span><span class="sxs-lookup"><span data-stu-id="7167d-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="7167d-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7167d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7167d-104">[开放式 Web Interface for .net （OWIN）](http://owin.org/)定义 .net web 服务器和 Web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="7167d-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="7167d-105">通过将 web 服务器与应用程序分离，OWIN 可以更轻松地创建用于 .NET web 开发的中间件。</span><span class="sxs-lookup"><span data-stu-id="7167d-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="7167d-106">此外，OWIN 使你可以更轻松地将 web 应用程序&#8212;移植到其他主机（例如，在 Windows 服务或其他进程中自承载）。</span><span class="sxs-lookup"><span data-stu-id="7167d-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="7167d-107">OWIN 是社区拥有的规范，而不是实现。</span><span class="sxs-lookup"><span data-stu-id="7167d-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="7167d-108">Katana 项目是由 Microsoft 开发的一组开源 OWIN 组件。</span><span class="sxs-lookup"><span data-stu-id="7167d-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="7167d-109">有关 OWIN 和 Katana 的一般概述，请参阅[Project Katana 的概述](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="7167d-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="7167d-110">在本文中，我将直接转到代码开始。</span><span class="sxs-lookup"><span data-stu-id="7167d-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="7167d-111">本教程使用[Visual Studio 2013 候选发布版](https://go.microsoft.com/fwlink/?LinkId=306566)，但你也可以使用 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="7167d-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="7167d-112">下面是一些在 Visual Studio 2012 中所述步骤不同的步骤。</span><span class="sxs-lookup"><span data-stu-id="7167d-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="7167d-113">在 IIS 中承载 OWIN</span><span class="sxs-lookup"><span data-stu-id="7167d-113">Host OWIN in IIS</span></span>

<span data-ttu-id="7167d-114">在本部分中，我们将在 IIS 中托管 OWIN。</span><span class="sxs-lookup"><span data-stu-id="7167d-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="7167d-115">使用此选项，你可以灵活地将 OWIN 管道与可组合性的成熟功能集结合使用。</span><span class="sxs-lookup"><span data-stu-id="7167d-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="7167d-116">使用此选项时，OWIN 应用程序会在 ASP.NET 请求管道中运行。</span><span class="sxs-lookup"><span data-stu-id="7167d-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="7167d-117">首先，创建一个新的 ASP.NET Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="7167d-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="7167d-118">（在 Visual Studio 2012 中，使用 ASP.NET 空白 Web 应用程序项目类型。）</span><span class="sxs-lookup"><span data-stu-id="7167d-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="7167d-119">在 "**新建 ASP.NET 项目**" 对话框中，选择 "**空**" 模板。</span><span class="sxs-lookup"><span data-stu-id="7167d-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="7167d-120">添加 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="7167d-120">Add NuGet Packages</span></span>

<span data-ttu-id="7167d-121">接下来，添加所需的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="7167d-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="7167d-122">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="7167d-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7167d-123">在 "程序包管理器控制台" 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7167d-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="7167d-124">添加 Startup 类</span><span class="sxs-lookup"><span data-stu-id="7167d-124">Add a Startup Class</span></span>

<span data-ttu-id="7167d-125">接下来，添加 OWIN startup 类。</span><span class="sxs-lookup"><span data-stu-id="7167d-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="7167d-126">在解决方案资源管理器中，右键单击项目并选择 "**添加**"，然后选择 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="7167d-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="7167d-127">在 "**添加新项**" 对话框中，选择 " **Owin Startup class**"。</span><span class="sxs-lookup"><span data-stu-id="7167d-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="7167d-128">有关配置 startup 类的详细信息，请参阅[OWIN Startup Class 检测](owin-startup-class-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="7167d-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="7167d-129">将以下代码添加到 `Startup1.Configuration` 方法中：</span><span class="sxs-lookup"><span data-stu-id="7167d-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="7167d-130">此代码将简单的中间件添加到 OWIN 管道，并将其作为接收**IOwinContext**实例的函数来实现。</span><span class="sxs-lookup"><span data-stu-id="7167d-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="7167d-131">当服务器收到 HTTP 请求时，OWIN 管道将调用中间件。</span><span class="sxs-lookup"><span data-stu-id="7167d-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="7167d-132">中间件设置响应的内容类型并写入响应正文。</span><span class="sxs-lookup"><span data-stu-id="7167d-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="7167d-133">Visual Studio 2013 中提供了 OWIN Startup 类模板。</span><span class="sxs-lookup"><span data-stu-id="7167d-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="7167d-134">如果使用的是 Visual Studio 2012，只需添加一个名为 `Startup1`的新空类，并粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="7167d-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="7167d-135">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="7167d-135">Run the Application</span></span>

<span data-ttu-id="7167d-136">按下 F5 以便开始调试。</span><span class="sxs-lookup"><span data-stu-id="7167d-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="7167d-137">Visual Studio 将打开一个浏览器窗口以 `http://localhost:*port*/`。</span><span class="sxs-lookup"><span data-stu-id="7167d-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="7167d-138">该页应如下所示：</span><span class="sxs-lookup"><span data-stu-id="7167d-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="7167d-139">控制台应用程序中的自承载 OWIN</span><span class="sxs-lookup"><span data-stu-id="7167d-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="7167d-140">在自定义过程中，可以轻松地将此应用程序从承载 IIS 托管到自承载。</span><span class="sxs-lookup"><span data-stu-id="7167d-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="7167d-141">借助 IIS 托管，IIS 既充当 HTTP 服务器，又充当承载服务的进程。</span><span class="sxs-lookup"><span data-stu-id="7167d-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="7167d-142">使用自承载，你的应用程序将创建进程，并使用**HttpListener**类作为 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="7167d-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="7167d-143">在 Visual Studio 中创建新的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="7167d-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="7167d-144">在 "程序包管理器控制台" 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7167d-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="7167d-145">将本教程第1部分中的 `Startup1` 类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="7167d-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="7167d-146">不需要修改此类。</span><span class="sxs-lookup"><span data-stu-id="7167d-146">You don't need to modify this class.</span></span>

<span data-ttu-id="7167d-147">按如下所示实现应用程序的 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="7167d-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="7167d-148">运行控制台应用程序时，服务器开始侦听 `http://localhost:9000`。</span><span class="sxs-lookup"><span data-stu-id="7167d-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="7167d-149">如果在 web 浏览器中导航到此地址，将显示 "Hello world" 页面。</span><span class="sxs-lookup"><span data-stu-id="7167d-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="7167d-150">添加 OWIN 诊断</span><span class="sxs-lookup"><span data-stu-id="7167d-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="7167d-151">Owin 包包含捕获未经处理的异常的中间件，并显示包含错误详细信息的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="7167d-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="7167d-152">此页的工作方式非常类似于 ASP.NET 错误页，有时称为 "[黄屏死亡](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" （YSOD）。</span><span class="sxs-lookup"><span data-stu-id="7167d-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="7167d-153">与 YSOD 一样，Katana 错误页在开发期间很有用，但最好在生产模式下禁用它。</span><span class="sxs-lookup"><span data-stu-id="7167d-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="7167d-154">若要在项目中安装诊断包，请在 "包管理器控制台" 窗口中键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7167d-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="7167d-155">更改 `Startup1.Configuration` 方法中的代码，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7167d-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="7167d-156">现在，使用 CTRL + F5 运行应用程序而不进行调试，以便 Visual Studio 不会在异常上中断。</span><span class="sxs-lookup"><span data-stu-id="7167d-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="7167d-157">应用程序的行为与以前相同，直到你导航到 `http://localhost/fail`，此时应用程序会引发异常。</span><span class="sxs-lookup"><span data-stu-id="7167d-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="7167d-158">错误页中间件将捕获异常，并显示包含有关错误的信息的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="7167d-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="7167d-159">您可以单击选项卡以查看堆栈、查询字符串、cookie、请求标头和 OWIN 环境变量。</span><span class="sxs-lookup"><span data-stu-id="7167d-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="7167d-160">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7167d-160">Next Steps</span></span>

- [<span data-ttu-id="7167d-161">OWIN 启动类检测</span><span class="sxs-lookup"><span data-stu-id="7167d-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="7167d-162">使用 OWIN 自承载 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="7167d-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="7167d-163">使用 OWIN 自承载 SignalR</span><span class="sxs-lookup"><span data-stu-id="7167d-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
