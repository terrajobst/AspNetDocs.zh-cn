---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: 将 ASP.NET MVC 用于不同版本的 IIS （C#） |Microsoft Docs
author: microsoft
description: 在本教程中，将了解如何使用 Internet Information Services 的不同版本的 ASP.NET MVC 和 URL 路由。 了解不同的策略 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 3b0a9509c0600f3598fd1218a7b383430548d4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486524"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a><span data-ttu-id="91c5d-104">通过不同版本的 IIS 使用 ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="91c5d-104">Using ASP.NET MVC with Different Versions of IIS (C#)</span></span>

<span data-ttu-id="91c5d-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="91c5d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="91c5d-106">在本教程中，将了解如何使用 Internet Information Services 的不同版本的 ASP.NET MVC 和 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="91c5d-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="91c5d-107">你将了解将 ASP.NET MVC 与 IIS 7.0 （经典模式）、IIS 6.0 和 iis 的早期版本结合使用的不同策略。</span><span class="sxs-lookup"><span data-stu-id="91c5d-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="91c5d-108">ASP.NET MVC 框架依赖于 ASP.NET 路由，将浏览器请求路由到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="91c5d-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="91c5d-109">为了充分利用 ASP.NET 路由，你可能需要在 web 服务器上执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="91c5d-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="91c5d-110">这一切都取决于应用程序的 Internet Information Services （IIS）和请求处理模式的版本。</span><span class="sxs-lookup"><span data-stu-id="91c5d-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="91c5d-111">下面是不同版本的 IIS 的摘要：</span><span class="sxs-lookup"><span data-stu-id="91c5d-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="91c5d-112">IIS 7.0 （集成模式）-使用 ASP.NET 路由无需特殊配置。</span><span class="sxs-lookup"><span data-stu-id="91c5d-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="91c5d-113">IIS 7.0 （经典模式）-需要执行特殊配置才能使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="91c5d-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="91c5d-114">IIS 6.0 或更低-需要执行特殊配置才能使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="91c5d-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="91c5d-115">最新版本的 IIS 为版本7.5 （在 Win7 上）。</span><span class="sxs-lookup"><span data-stu-id="91c5d-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="91c5d-116">Iis 7 的 IIS 包含在 Windows Server 2008 和 VISTA/SP1 及更高版本中。</span><span class="sxs-lookup"><span data-stu-id="91c5d-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="91c5d-117">你还可以在任何版本的 Vista 操作系统（Home Basic 除外）上安装 IIS 7.0 （请参阅[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="91c5d-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="91c5d-118">IIS 7.0 支持两种模式来处理请求。</span><span class="sxs-lookup"><span data-stu-id="91c5d-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="91c5d-119">您可以使用集成模式或经典模式。</span><span class="sxs-lookup"><span data-stu-id="91c5d-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="91c5d-120">在集成模式下使用 IIS 7.0 时，无需执行任何特殊的配置步骤。</span><span class="sxs-lookup"><span data-stu-id="91c5d-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="91c5d-121">但是，在经典模式下使用 IIS 7.0 时，需要执行其他配置。</span><span class="sxs-lookup"><span data-stu-id="91c5d-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="91c5d-122">Microsoft Windows Server 2003 包括 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="91c5d-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="91c5d-123">使用 Windows Server 2003 操作系统时，不能将 IIS 6.0 升级到 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="91c5d-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="91c5d-124">使用 IIS 6.0 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="91c5d-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="91c5d-125">Microsoft Windows XP Professional 包括 IIS 5.1。</span><span class="sxs-lookup"><span data-stu-id="91c5d-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="91c5d-126">使用 IIS 5.1 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="91c5d-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="91c5d-127">最后，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包括 IIS 5.0。</span><span class="sxs-lookup"><span data-stu-id="91c5d-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="91c5d-128">使用 IIS 5.0 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="91c5d-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="91c5d-129">集成模式与经典模式</span><span class="sxs-lookup"><span data-stu-id="91c5d-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="91c5d-130">IIS 7.0 可以使用两种不同的请求处理模式来处理请求：集成和经典。</span><span class="sxs-lookup"><span data-stu-id="91c5d-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="91c5d-131">集成模式提供更好的性能和更多功能。</span><span class="sxs-lookup"><span data-stu-id="91c5d-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="91c5d-132">包含经典模式是为了与 IIS 的早期版本向后兼容。</span><span class="sxs-lookup"><span data-stu-id="91c5d-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="91c5d-133">请求处理模式取决于应用程序池。</span><span class="sxs-lookup"><span data-stu-id="91c5d-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="91c5d-134">通过确定与应用程序关联的应用程序池，你可以确定特定的 web 应用程序所使用的处理模式。</span><span class="sxs-lookup"><span data-stu-id="91c5d-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="91c5d-135">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="91c5d-135">Follow these steps:</span></span>

1. <span data-ttu-id="91c5d-136">启动 Internet Information Services 管理器</span><span class="sxs-lookup"><span data-stu-id="91c5d-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="91c5d-137">在 "连接" 窗口中，选择一个应用程序</span><span class="sxs-lookup"><span data-stu-id="91c5d-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="91c5d-138">在 "操作" 窗口中，单击 "**基本设置**" 链接以打开 "编辑应用程序" 对话框（请参阅图1）</span><span class="sxs-lookup"><span data-stu-id="91c5d-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="91c5d-139">记下所选的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="91c5d-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="91c5d-140">默认情况下，IIS 配置为支持两个应用程序池： **DefaultAppPool**和**经典 .net AppPool**。</span><span class="sxs-lookup"><span data-stu-id="91c5d-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="91c5d-141">如果选择了 "DefaultAppPool"，则你的应用程序将在集成请求处理模式下运行。</span><span class="sxs-lookup"><span data-stu-id="91c5d-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="91c5d-142">如果选择了经典 .NET AppPool，你的应用程序将在经典请求处理模式下运行。</span><span class="sxs-lookup"><span data-stu-id="91c5d-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="91c5d-143">[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="91c5d-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span></span>

<span data-ttu-id="91c5d-144">**图 1**：检测请求处理模式（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="91c5d-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span></span>

<span data-ttu-id="91c5d-145">请注意，你可以在 "编辑应用程序" 对话框中修改 "请求处理" 模式。</span><span class="sxs-lookup"><span data-stu-id="91c5d-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="91c5d-146">单击 "选择" 按钮并更改与应用程序关联的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="91c5d-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="91c5d-147">请注意，将 ASP.NET 应用程序从经典模式更改为集成模式时存在兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="91c5d-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="91c5d-148">有关详细信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="91c5d-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="91c5d-149">在 Windows Vista 和 Windows Server 2008 上将 ASP.NET 1.1 升级到 IIS 7.0-- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="91c5d-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>
- <span data-ttu-id="91c5d-150">与 IIS 7.0 的 ASP.NET 集成- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="91c5d-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="91c5d-151">如果 ASP.NET 应用程序使用的是 DefaultAppPool，则无需执行任何附加步骤即可获得 ASP.NET 路由（因而 ASP.NET MVC）才能正常工作。</span><span class="sxs-lookup"><span data-stu-id="91c5d-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="91c5d-152">但是，如果将 ASP.NET 应用程序配置为使用经典 .NET AppPool，然后继续阅读，则有更多工作要做。</span><span class="sxs-lookup"><span data-stu-id="91c5d-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="91c5d-153">将 ASP.NET MVC 与较旧版本的 IIS 一起使用</span><span class="sxs-lookup"><span data-stu-id="91c5d-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="91c5d-154">如果需要使用比 IIS 7.0 更早版本的 ASP.NET MVC，或者需要在经典模式下使用 IIS 7.0，则有两个选择。</span><span class="sxs-lookup"><span data-stu-id="91c5d-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="91c5d-155">首先，可以修改路由表以使用文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="91c5d-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="91c5d-156">例如，你应该请求 URL （如/Store/Details），而不是请求 URL （如/Store.aspx/Details.）。</span><span class="sxs-lookup"><span data-stu-id="91c5d-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="91c5d-157">第二种方法是创建一个名为*通配符脚本映射*的内容。</span><span class="sxs-lookup"><span data-stu-id="91c5d-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="91c5d-158">使用通配符脚本映射，可以将每个请求映射到 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="91c5d-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="91c5d-159">如果你无法访问你的 web 服务器（例如，你的 ASP.NET MVC 应用程序由 Internet 服务提供商托管），则需要使用第一个选项。</span><span class="sxs-lookup"><span data-stu-id="91c5d-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="91c5d-160">如果你不想修改 Url 的外观，并且可以访问你的 web 服务器，则可以使用第二个选项。</span><span class="sxs-lookup"><span data-stu-id="91c5d-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="91c5d-161">我们将在以下各节中详细探讨每个选项。</span><span class="sxs-lookup"><span data-stu-id="91c5d-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="91c5d-162">向路由表添加扩展</span><span class="sxs-lookup"><span data-stu-id="91c5d-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="91c5d-163">若要使 ASP.NET 路由与较旧版本的 IIS 一起使用，最简单的方法是修改 global.asax 文件中的路由表。</span><span class="sxs-lookup"><span data-stu-id="91c5d-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="91c5d-164">列表1中的默认和未修改的 Global.asa 文件配置一个名为默认路由的路由。</span><span class="sxs-lookup"><span data-stu-id="91c5d-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="91c5d-165">**列表 1-global.asax （未修改）**</span><span class="sxs-lookup"><span data-stu-id="91c5d-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

<span data-ttu-id="91c5d-166">通过在列表1中配置的默认路由，你可以路由如下所示的 Url：</span><span class="sxs-lookup"><span data-stu-id="91c5d-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="91c5d-167">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="91c5d-167">/Home/Index</span></span>

<span data-ttu-id="91c5d-168">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="91c5d-168">/Product/Details/3</span></span>

<span data-ttu-id="91c5d-169">/Product</span><span class="sxs-lookup"><span data-stu-id="91c5d-169">/Product</span></span>

<span data-ttu-id="91c5d-170">遗憾的是，较旧版本的 IIS 不会将这些请求传递到 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="91c5d-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="91c5d-171">因此，这些请求不会路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="91c5d-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="91c5d-172">例如，如果发出浏览器请求 URL/Home/Index，则会收到图2中的错误页。</span><span class="sxs-lookup"><span data-stu-id="91c5d-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="91c5d-173">[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="91c5d-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span></span>

<span data-ttu-id="91c5d-174">**图 2**：收到 "找不到 404" 错误（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="91c5d-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span></span>

<span data-ttu-id="91c5d-175">较早版本的 IIS 仅将某些请求映射到 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="91c5d-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="91c5d-176">请求必须为具有正确文件扩展名的 URL。</span><span class="sxs-lookup"><span data-stu-id="91c5d-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="91c5d-177">例如，/SomePage.aspx 的请求将映射到 ASP.NET framework。</span><span class="sxs-lookup"><span data-stu-id="91c5d-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="91c5d-178">但是，/SomePage.htm 的请求不会。</span><span class="sxs-lookup"><span data-stu-id="91c5d-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="91c5d-179">因此，若要使 ASP.NET 路由正常工作，必须修改默认路由，使其包含映射到 ASP.NET 框架的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="91c5d-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="91c5d-180">这是使用名为 `registermvc.wsf`的脚本来完成的。</span><span class="sxs-lookup"><span data-stu-id="91c5d-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="91c5d-181">它包含在 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`中的 ASP.NET MVC 1 版本中，但从 ASP.NET 2 开始，此脚本已移至 ASP.NET 先期备货， [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)提供。</span><span class="sxs-lookup"><span data-stu-id="91c5d-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="91c5d-182">执行此脚本会向 IIS 注册一个新的 mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="91c5d-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="91c5d-183">注册 mvc 扩展后，可以修改 global.asax 文件中的路由，以便路由使用 mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="91c5d-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="91c5d-184">清单2中修改的 Global.asa 文件与较旧版本的 IIS 一起使用。</span><span class="sxs-lookup"><span data-stu-id="91c5d-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="91c5d-185">**列表 2-global.asax （已通过扩展进行修改）**</span><span class="sxs-lookup"><span data-stu-id="91c5d-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

<span data-ttu-id="91c5d-186">**重要提示**：请记得在更改 global.asax 文件后再次生成 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="91c5d-186">**Important**: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="91c5d-187">清单2中的 global.asax 文件有两个重要更改。</span><span class="sxs-lookup"><span data-stu-id="91c5d-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="91c5d-188">现在，global.asax 中定义了两个路由。</span><span class="sxs-lookup"><span data-stu-id="91c5d-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="91c5d-189">默认路由的 URL 模式（第一个路由）现在如下所示：</span><span class="sxs-lookup"><span data-stu-id="91c5d-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="91c5d-190">{controller}.mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="91c5d-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="91c5d-191">添加 mvc 扩展会更改 ASP.NET 路由模块截获的文件类型。</span><span class="sxs-lookup"><span data-stu-id="91c5d-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="91c5d-192">进行此更改后，ASP.NET MVC 应用程序现在会路由请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="91c5d-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="91c5d-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="91c5d-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="91c5d-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="91c5d-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="91c5d-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="91c5d-195">/Product.mvc/</span></span>

<span data-ttu-id="91c5d-196">第二个路由，根路由是新的。</span><span class="sxs-lookup"><span data-stu-id="91c5d-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="91c5d-197">根路由的此 URL 模式为空字符串。</span><span class="sxs-lookup"><span data-stu-id="91c5d-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="91c5d-198">对于对应用程序的根目录进行的匹配请求，此路由是必需的。</span><span class="sxs-lookup"><span data-stu-id="91c5d-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="91c5d-199">例如，根路由将匹配类似于下面的请求：</span><span class="sxs-lookup"><span data-stu-id="91c5d-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="91c5d-200">对路由表进行这些修改后，需要确保应用程序中的所有链接都与这些新的 URL 模式兼容。</span><span class="sxs-lookup"><span data-stu-id="91c5d-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="91c5d-201">换句话说，请确保所有的链接都包含 mvc 扩展名。</span><span class="sxs-lookup"><span data-stu-id="91c5d-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="91c5d-202">如果使用 Html.actionlink （）帮助器方法来生成链接，则不需要进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="91c5d-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="91c5d-203">可以不使用 registermvc 脚本，而是向 IIS 添加新的扩展，并将其手动映射到 ASP.NET framework。</span><span class="sxs-lookup"><span data-stu-id="91c5d-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="91c5d-204">当你自己添加新扩展时，请确保未选中标有 "**验证该文件是否存在**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="91c5d-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="91c5d-205">托管服务器</span><span class="sxs-lookup"><span data-stu-id="91c5d-205">Hosted Server</span></span>

<span data-ttu-id="91c5d-206">您不会始终有权访问您的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="91c5d-206">You don't always have access to your web server.</span></span> <span data-ttu-id="91c5d-207">例如，如果使用 Internet 宿主提供程序托管 ASP.NET MVC 应用程序，则无需访问 IIS。</span><span class="sxs-lookup"><span data-stu-id="91c5d-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="91c5d-208">在这种情况下，应使用映射到 ASP.NET 框架的现有文件扩展名之一。</span><span class="sxs-lookup"><span data-stu-id="91c5d-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="91c5d-209">映射到 ASP.NET 的文件扩展名的示例包括 .aspx、axd 和. foo.ashx 扩展。</span><span class="sxs-lookup"><span data-stu-id="91c5d-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="91c5d-210">例如，在列表3中修改的 global.asax 文件使用 .aspx 扩展名而不是 mvc 扩展名。</span><span class="sxs-lookup"><span data-stu-id="91c5d-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="91c5d-211">**列表 3-global.asax （已修改为 .aspx 扩展名）**</span><span class="sxs-lookup"><span data-stu-id="91c5d-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

<span data-ttu-id="91c5d-212">清单3中的 Global.asa 文件与以前的 Global.asa 文件完全相同，只是它使用 .aspx 扩展名而不是 mvc 扩展名。</span><span class="sxs-lookup"><span data-stu-id="91c5d-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="91c5d-213">无需在远程 web 服务器上执行任何设置即可使用 .aspx 扩展。</span><span class="sxs-lookup"><span data-stu-id="91c5d-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="91c5d-214">创建通配符脚本映射</span><span class="sxs-lookup"><span data-stu-id="91c5d-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="91c5d-215">如果不想修改 ASP.NET MVC 应用程序的 Url，并且有权访问 web 服务器，则可以使用其他选项。</span><span class="sxs-lookup"><span data-stu-id="91c5d-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="91c5d-216">你可以创建一个通配符脚本映射，用于将对 web 服务器的所有请求映射到 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="91c5d-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="91c5d-217">通过这种方式，可以将默认的 ASP.NET MVC 路由表与 IIS 7.0 （在经典模式下）或 IIS 6.0 一起使用。</span><span class="sxs-lookup"><span data-stu-id="91c5d-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="91c5d-218">请注意，此选项会使 IIS 截获针对 web 服务器发出的每个请求。</span><span class="sxs-lookup"><span data-stu-id="91c5d-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="91c5d-219">这包括图像、经典 ASP 页面和 HTML 页面的请求。</span><span class="sxs-lookup"><span data-stu-id="91c5d-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="91c5d-220">因此，启用 ASP.NET 的通配符脚本映射确实会影响性能。</span><span class="sxs-lookup"><span data-stu-id="91c5d-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="91c5d-221">下面介绍如何为 IIS 7.0 启用通配符脚本映射：</span><span class="sxs-lookup"><span data-stu-id="91c5d-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="91c5d-222">在 "连接" 窗口中选择应用程序</span><span class="sxs-lookup"><span data-stu-id="91c5d-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="91c5d-223">请确保已选择 "**功能**视图"</span><span class="sxs-lookup"><span data-stu-id="91c5d-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="91c5d-224">双击 "**处理程序映射**" 按钮</span><span class="sxs-lookup"><span data-stu-id="91c5d-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="91c5d-225">单击 "**添加通配符脚本映射**" 链接（见图3）</span><span class="sxs-lookup"><span data-stu-id="91c5d-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="91c5d-226">输入 aspnet\_isapi .dll 文件的路径（可以从 Pagehandlerfactory-isapi 脚本映射复制此路径）</span><span class="sxs-lookup"><span data-stu-id="91c5d-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="91c5d-227">输入名称 MVC</span><span class="sxs-lookup"><span data-stu-id="91c5d-227">Enter the name MVC</span></span>
7. <span data-ttu-id="91c5d-228">单击 **"确定"** 按钮</span><span class="sxs-lookup"><span data-stu-id="91c5d-228">Click the **OK** button</span></span>

<span data-ttu-id="91c5d-229">[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="91c5d-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span></span>

<span data-ttu-id="91c5d-230">**图 3**：使用 IIS 7.0 创建通配符脚本映射（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="91c5d-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span></span>

<span data-ttu-id="91c5d-231">按照以下步骤使用 IIS 6.0 创建通配符脚本映射：</span><span class="sxs-lookup"><span data-stu-id="91c5d-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="91c5d-232">右键单击网站，然后选择 "属性"</span><span class="sxs-lookup"><span data-stu-id="91c5d-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="91c5d-233">选择 "**主目录**" 选项卡</span><span class="sxs-lookup"><span data-stu-id="91c5d-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="91c5d-234">单击 "**配置**" 按钮</span><span class="sxs-lookup"><span data-stu-id="91c5d-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="91c5d-235">选择 "**映射**" 选项卡</span><span class="sxs-lookup"><span data-stu-id="91c5d-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="91c5d-236">单击 "**插入**" 按钮（见图4）</span><span class="sxs-lookup"><span data-stu-id="91c5d-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="91c5d-237">将 aspnet\_的路径粘贴到可执行字段中（可从 .aspx 文件的脚本映射复制此路径）</span><span class="sxs-lookup"><span data-stu-id="91c5d-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="91c5d-238">取消选中标有 "**验证该文件是否存在**" 的复选框</span><span class="sxs-lookup"><span data-stu-id="91c5d-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="91c5d-239">单击 **"确定"** 按钮</span><span class="sxs-lookup"><span data-stu-id="91c5d-239">Click the **OK** button</span></span>

<span data-ttu-id="91c5d-240">[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="91c5d-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span></span>

<span data-ttu-id="91c5d-241">**图 4**：使用 IIS 6.0 创建通配符脚本映射（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="91c5d-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span></span>

<span data-ttu-id="91c5d-242">启用通配符脚本映射后，需要修改 global.asax 文件中的路由表，使其包含根路由。</span><span class="sxs-lookup"><span data-stu-id="91c5d-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="91c5d-243">否则，在对应用程序的根页发出请求时，会收到图5中的错误页。</span><span class="sxs-lookup"><span data-stu-id="91c5d-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="91c5d-244">可以在清单4中使用修改后的 global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="91c5d-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="91c5d-245">[!["新建项目" 对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="91c5d-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span></span>

<span data-ttu-id="91c5d-246">**图 5**：缺少根路由错误（[单击以查看完全大小的映像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="91c5d-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span></span>

<span data-ttu-id="91c5d-247">**列表 4-global.asax （已在根路由中修改）**</span><span class="sxs-lookup"><span data-stu-id="91c5d-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

<span data-ttu-id="91c5d-248">为 IIS 7.0 或 IIS 6.0 启用通配符脚本映射后，可以发出请求来处理默认路由表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="91c5d-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="91c5d-249">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="91c5d-249">/Home/Index</span></span>

<span data-ttu-id="91c5d-250">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="91c5d-250">/Product/Details/3</span></span>

<span data-ttu-id="91c5d-251">/Product</span><span class="sxs-lookup"><span data-stu-id="91c5d-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="91c5d-252">摘要</span><span class="sxs-lookup"><span data-stu-id="91c5d-252">Summary</span></span>

<span data-ttu-id="91c5d-253">本教程的目的是说明如何在使用较旧版本的 IIS （或经典模式下的 IIS 7.0）时使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="91c5d-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="91c5d-254">我们讨论了两种方法来获取 ASP.NET 路由，以便使用较旧版本的 IIS：修改默认路由表或创建通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="91c5d-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="91c5d-255">第一个选项要求修改 ASP.NET MVC 应用程序中使用的 Url。</span><span class="sxs-lookup"><span data-stu-id="91c5d-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="91c5d-256">第一种方法的一个非常重要的优点是，您不需要访问 web 服务器即可修改路由表。</span><span class="sxs-lookup"><span data-stu-id="91c5d-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="91c5d-257">这意味着，即使在向 Internet 托管公司托管 ASP.NET MVC 应用程序时，也可以使用第一个选项。</span><span class="sxs-lookup"><span data-stu-id="91c5d-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="91c5d-258">第二种方法是创建通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="91c5d-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="91c5d-259">此第二个选项的优点是不需要修改 Url。</span><span class="sxs-lookup"><span data-stu-id="91c5d-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="91c5d-260">此第二个选项的缺点是它可能会影响 ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="91c5d-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="91c5d-261">下一部分</span><span class="sxs-lookup"><span data-stu-id="91c5d-261">Next</span></span>](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
