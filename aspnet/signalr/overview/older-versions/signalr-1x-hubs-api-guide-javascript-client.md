---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1.x 中心 API 指南-JavaScript 客户端 |Microsoft Docs
author: bradygaster
description: 本文档介绍了如何在 JavaScript 客户端（如浏览器和 Windows 应用商店（WinJS）应用 ... 中使用适用于 SignalR 版本1.1 的中心 API
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431102"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="b7e07-103">SignalR 1.x 中心 API 指南 - JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="b7e07-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>

<span data-ttu-id="b7e07-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b7e07-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b7e07-105">本文档介绍了如何在 JavaScript 客户端（如浏览器和 Windows 应用商店（WinJS）应用程序）中使用适用于 SignalR 版本1.1 的中心 API。</span><span class="sxs-lookup"><span data-stu-id="b7e07-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="b7e07-106">利用 SignalR 中心 API，你可以将服务器中的远程过程调用（Rpc）连接到已连接的客户端和客户端。</span><span class="sxs-lookup"><span data-stu-id="b7e07-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="b7e07-107">在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="b7e07-108">在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="b7e07-109">SignalR 负责处理所有的客户端到服务器的操作。</span><span class="sxs-lookup"><span data-stu-id="b7e07-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="b7e07-110">SignalR 还提供名为持久性连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="b7e07-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="b7e07-111">有关 SignalR、集线器和持久性连接的简介，或有关演示如何生成完整 SignalR 应用程序的教程，请参阅[SignalR-入门](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="b7e07-112">概述</span><span class="sxs-lookup"><span data-stu-id="b7e07-112">Overview</span></span>

<span data-ttu-id="b7e07-113">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="b7e07-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="b7e07-114">生成的代理以及它为你执行的操作</span><span class="sxs-lookup"><span data-stu-id="b7e07-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="b7e07-115">何时使用生成的代理</span><span class="sxs-lookup"><span data-stu-id="b7e07-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="b7e07-116">客户端设置</span><span class="sxs-lookup"><span data-stu-id="b7e07-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="b7e07-117">如何引用动态生成的代理</span><span class="sxs-lookup"><span data-stu-id="b7e07-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="b7e07-118">如何为 SignalR 生成的代理创建物理文件</span><span class="sxs-lookup"><span data-stu-id="b7e07-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="b7e07-119">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="b7e07-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="b7e07-120">$. 连接中心是 hubConnection （）创建的同一对象</span><span class="sxs-lookup"><span data-stu-id="b7e07-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="b7e07-121">开始方法的异步执行</span><span class="sxs-lookup"><span data-stu-id="b7e07-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="b7e07-122">如何建立跨域连接</span><span class="sxs-lookup"><span data-stu-id="b7e07-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="b7e07-123">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="b7e07-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="b7e07-124">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="b7e07-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="b7e07-125">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="b7e07-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="b7e07-126">如何获取集线器类的代理</span><span class="sxs-lookup"><span data-stu-id="b7e07-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="b7e07-127">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="b7e07-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="b7e07-128">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="b7e07-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="b7e07-129">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="b7e07-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="b7e07-130">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="b7e07-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="b7e07-131">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="b7e07-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="b7e07-132">有关如何对服务器或 .NET 客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b7e07-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="b7e07-133">SignalR 中心 API 指南-服务器</span><span class="sxs-lookup"><span data-stu-id="b7e07-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="b7e07-134">SignalR 中心 API 指南-.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="b7e07-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="b7e07-135">API 参考主题的链接适用于 .NET 4.5 版本的 API。</span><span class="sxs-lookup"><span data-stu-id="b7e07-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="b7e07-136">如果使用的是 .NET 4，请参阅[.net 4 版本的 API 主题](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="b7e07-137">生成的代理以及它为你执行的操作</span><span class="sxs-lookup"><span data-stu-id="b7e07-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="b7e07-138">你可以对 JavaScript 客户端进行编程，以便使用或不使用 SignalR 生成的代理来与 SignalR 服务进行通信。</span><span class="sxs-lookup"><span data-stu-id="b7e07-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="b7e07-139">代理的作用是简化用于连接的代码的语法，编写服务器调用的方法，并在服务器上调用方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="b7e07-140">当你编写代码来调用服务器方法时，生成的代理使你可以使用类似于执行本地函数的语法：你可以编写 `serverMethod(arg1, arg2)` 而不是 `invoke('serverMethod', arg1, arg2)`。</span><span class="sxs-lookup"><span data-stu-id="b7e07-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="b7e07-141">如果错误键入服务器方法名称，生成的代理语法还会启用立即和可识别的客户端错误。</span><span class="sxs-lookup"><span data-stu-id="b7e07-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="b7e07-142">如果手动创建定义代理的文件，还可以获取对编写调用服务器方法的代码的 IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="b7e07-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="b7e07-143">例如，假设您在服务器上具有以下中心类：</span><span class="sxs-lookup"><span data-stu-id="b7e07-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="b7e07-144">下面的代码示例演示了在服务器上调用 `NewContosoChatMessage` 方法以及从服务器接收 `addContosoChatMessageToPage` 方法的调用时，JavaScript 代码的外观。</span><span class="sxs-lookup"><span data-stu-id="b7e07-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="b7e07-145">**与生成的代理**</span><span class="sxs-lookup"><span data-stu-id="b7e07-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="b7e07-146">**没有生成的代理**</span><span class="sxs-lookup"><span data-stu-id="b7e07-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="b7e07-147">何时使用生成的代理</span><span class="sxs-lookup"><span data-stu-id="b7e07-147">When to use the generated proxy</span></span>

<span data-ttu-id="b7e07-148">如果要为服务器调用的客户端方法注册多个事件处理程序，则不能使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="b7e07-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="b7e07-149">否则，你可以选择使用生成的代理，而不是基于编码首选项。</span><span class="sxs-lookup"><span data-stu-id="b7e07-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="b7e07-150">如果选择不使用此方法，则无需在客户端代码中引用 `script` 元素中的 "signalr/hub" URL。</span><span class="sxs-lookup"><span data-stu-id="b7e07-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="b7e07-151">客户端设置</span><span class="sxs-lookup"><span data-stu-id="b7e07-151">Client setup</span></span>

<span data-ttu-id="b7e07-152">JavaScript 客户端需要引用 jQuery 和 SignalR core JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="b7e07-153">JQuery 版本必须是1.6.4 或主要版本，如1.7.2、1.8.2 或1.9.1。</span><span class="sxs-lookup"><span data-stu-id="b7e07-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="b7e07-154">如果决定使用生成的代理，则还需要引用 SignalR 生成的代理 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="b7e07-155">下面的示例演示在使用生成的代理的 HTML 页中，引用可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="b7e07-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="b7e07-156">这些引用必须按以下顺序包含： jQuery first、SignalR core 之后，以及 SignalR 代理 last。</span><span class="sxs-lookup"><span data-stu-id="b7e07-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="b7e07-157">如何引用动态生成的代理</span><span class="sxs-lookup"><span data-stu-id="b7e07-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="b7e07-158">在前面的示例中，对 SignalR 生成的代理的引用是动态生成的 JavaScript 代码，而不是物理文件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="b7e07-159">SignalR 会动态地为代理创建 JavaScript 代码，并将其提供给客户端，以响应 "/signalr/hubs" URL。</span><span class="sxs-lookup"><span data-stu-id="b7e07-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="b7e07-160">如果在 `MapHubs` 方法中为服务器上的 SignalR 连接指定了不同的基 URL，则动态生成的代理文件的 URL 为自定义 URL，后面追加了 "/hubs"。</span><span class="sxs-lookup"><span data-stu-id="b7e07-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="b7e07-161">对于 Windows 8 （Windows 应用商店） JavaScript 客户端，请使用物理代理文件而不是动态生成的文件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="b7e07-162">有关详细信息，请参阅本主题后面的[如何为 SignalR 生成的代理创建物理文件](#manualproxy)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="b7e07-163">在 ASP.NET MVC 4 Razor 视图中，使用波形符在代理文件引用中引用应用程序根目录：</span><span class="sxs-lookup"><span data-stu-id="b7e07-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="b7e07-164">有关在 MVC 4 中使用 SignalR 的详细信息，请参阅[使用 SignalR 和 MVC 4 入门](tutorial-getting-started-with-signalr-and-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="b7e07-165">在 ASP.NET MVC 3 Razor 视图中，为代理文件引用使用 `Url.Content`：</span><span class="sxs-lookup"><span data-stu-id="b7e07-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="b7e07-166">在 ASP.NET Web 窗体应用程序中，为代理文件引用使用 `ResolveClientUrl`，或使用应用根相对路径（以颚化符开头）通过 ScriptManager 注册它：</span><span class="sxs-lookup"><span data-stu-id="b7e07-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="b7e07-167">作为一般规则，请使用与指定用于 CSS 或 JavaScript 文件的 "/signalr/hubs" URL 相同的方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="b7e07-168">如果在不使用波形符的情况下指定 URL，则在 Visual Studio 中使用 IIS Express 进行测试时，应用程序将正常工作，但在部署到完整 IIS 时将失败并出现404错误。</span><span class="sxs-lookup"><span data-stu-id="b7e07-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="b7e07-169">有关详细信息，请参阅 MSDN 网站上的在[Visual Studio for ASP.NET Web 项目的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)中**解析对根级资源的引用**。</span><span class="sxs-lookup"><span data-stu-id="b7e07-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="b7e07-170">在调试模式下运行 Visual Studio 2012 中的 web 项目时，如果使用 Internet Explorer 作为浏览器，则可以在**脚本文档**下的**解决方案资源管理器**中查看该代理文件，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="b7e07-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![JavaScript 在解决方案资源管理器中生成的代理文件](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="b7e07-172">若要查看文件的内容，请双击 "**中心**"。</span><span class="sxs-lookup"><span data-stu-id="b7e07-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="b7e07-173">如果使用的不是 Visual Studio 2012 和 Internet Explorer，或者不处于调试模式，还可以通过浏览到 "/signalR/hubs" URL 来获取文件的内容。</span><span class="sxs-lookup"><span data-stu-id="b7e07-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="b7e07-174">例如，如果你的站点正在 `http://localhost:56699`上运行，请在浏览器中转到 `http://localhost:56699/SignalR/hubs`。</span><span class="sxs-lookup"><span data-stu-id="b7e07-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="b7e07-175">如何为 SignalR 生成的代理创建物理文件</span><span class="sxs-lookup"><span data-stu-id="b7e07-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="b7e07-176">作为动态生成的代理的替代方法，可以创建包含代理代码的物理文件，并引用该文件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="b7e07-177">您可能想要执行此操作以控制缓存或绑定行为，或者在编码对服务器方法的调用时获取 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="b7e07-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="b7e07-178">若要创建代理文件，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="b7e07-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="b7e07-179">安装[SignalR. Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b7e07-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="b7e07-180">打开命令提示符并浏览到包含 SignalR 文件的 "*工具*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="b7e07-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="b7e07-181">"工具" 文件夹位于以下位置：</span><span class="sxs-lookup"><span data-stu-id="b7e07-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="b7e07-182">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b7e07-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="b7e07-183">*.Dll*的路径通常为项目文件夹中的*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="b7e07-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="b7e07-184">此命令在*signalr*所在的文件夹中创建名为*node.js*的文件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="b7e07-185">将*服务器 .js*文件放在项目中的适当文件夹中，将其重命名为适用于你的应用程序，并在 "signalr/hub" 引用的位置添加对该文件的引用。</span><span class="sxs-lookup"><span data-stu-id="b7e07-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="b7e07-186">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="b7e07-186">How to establish a connection</span></span>

<span data-ttu-id="b7e07-187">建立连接之前，必须先创建连接对象、创建代理，并为可从服务器调用的方法注册事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="b7e07-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="b7e07-188">设置代理和事件处理程序后，通过调用 `start` 方法来建立连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="b7e07-189">如果使用生成的代理，则无需在自己的代码中创建连接对象，因为生成的代理代码会为你执行该连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="b7e07-190">**建立连接（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="b7e07-191">**建立连接（没有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="b7e07-192">示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="b7e07-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="b7e07-193">有关如何指定其他基 URL 的信息，请参阅[ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="b7e07-194">通常，在调用 `start` 方法之前注册事件处理程序以建立连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="b7e07-195">如果要在建立连接后注册某些事件处理程序，可以这样做，但必须在调用 `start` 方法之前注册至少一个事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="b7e07-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="b7e07-196">导致这种情况的原因之一是，应用程序中可以有很多的中心，但如果只打算使用其中一种，则不希望在每个中心触发 `OnConnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="b7e07-197">建立连接后，在集线器代理上存在客户端方法会告诉 SignalR 触发 `OnConnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="b7e07-198">如果在调用 `start` 方法之前未注册任何事件处理程序，你将能够在中心调用方法，但不会调用中心的 `OnConnected` 方法，也不会从服务器中调用任何客户端方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="b7e07-199">$. 连接中心是 hubConnection （）创建的同一对象</span><span class="sxs-lookup"><span data-stu-id="b7e07-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="b7e07-200">如示例中所示，当你使用生成的代理时，`$.connection.hub` 引用连接对象。</span><span class="sxs-lookup"><span data-stu-id="b7e07-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="b7e07-201">这是通过在不使用生成的代理时调用 `$.hubConnection()` 获取的相同对象。</span><span class="sxs-lookup"><span data-stu-id="b7e07-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="b7e07-202">生成的代理代码通过执行以下语句来创建连接：</span><span class="sxs-lookup"><span data-stu-id="b7e07-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![在生成的代理文件中创建连接](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="b7e07-204">当你使用生成的代理时，你可以使用 `$.connection.hub` 执行任何操作，当你未使用生成的代理时，你可以对连接对象执行此操作。</span><span class="sxs-lookup"><span data-stu-id="b7e07-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="b7e07-205">开始方法的异步执行</span><span class="sxs-lookup"><span data-stu-id="b7e07-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="b7e07-206">`start` 方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="b7e07-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="b7e07-207">它将返回[JQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)，这意味着你可以通过调用 `pipe`、`done`和 `fail`等方法来添加回调函数。</span><span class="sxs-lookup"><span data-stu-id="b7e07-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="b7e07-208">如果你有想要在建立连接后执行的代码（例如，对服务器方法的调用），请将该代码放入回调函数或从回调函数调用它。</span><span class="sxs-lookup"><span data-stu-id="b7e07-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="b7e07-209">`.done` 回调方法在建立连接之后、在服务器上的 `OnConnected` 事件处理程序方法中完成执行的任何代码之后执行。</span><span class="sxs-lookup"><span data-stu-id="b7e07-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="b7e07-210">如果将前面的示例中的 "当前连接的" 语句作为 `start` 方法调用（而不是在 `.done` 回调）之后的下一行代码，则在建立连接之前将执行 `console.log` 行，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="b7e07-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![编写在建立连接后运行的代码的错误方法](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="b7e07-212">如何建立跨域连接</span><span class="sxs-lookup"><span data-stu-id="b7e07-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="b7e07-213">通常情况下，当浏览器从 `http://contoso.com`加载页面时，SignalR 连接位于同一域中 `http://contoso.com/signalr`。</span><span class="sxs-lookup"><span data-stu-id="b7e07-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="b7e07-214">如果 `http://contoso.com` 的页面与 `http://fabrikam.com/signalr`建立连接，则这是一个跨域连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="b7e07-215">出于安全原因，在默认情况下将禁用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="b7e07-216">若要建立跨域连接，请确保在服务器上启用跨域连接，并在创建连接对象时指定连接 URL。</span><span class="sxs-lookup"><span data-stu-id="b7e07-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="b7e07-217">SignalR 将使用适当的技术进行跨域连接，例如[JSONP](http://en.wikipedia.org/wiki/JSONP)或[CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="b7e07-218">在服务器上，当你调用 `MapHubs` 方法时，请通过选择该选项来启用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="b7e07-219">在客户端上，在创建连接对象（没有生成的代理）时或在调用 start 方法（包含生成的代理）之前，指定 URL。</span><span class="sxs-lookup"><span data-stu-id="b7e07-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="b7e07-220">**指定跨域连接的客户端代码（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="b7e07-221">**指定跨域连接的客户端代码（没有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="b7e07-222">使用 `$.hubConnection` 构造函数时，无需将 `signalr` 包含在 URL 中，因为它是自动添加的（除非指定 `useDefaultUrl` `false`）。</span><span class="sxs-lookup"><span data-stu-id="b7e07-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="b7e07-223">你可以创建与不同终结点的多个连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="b7e07-224">不要在代码中将 `jQuery.support.cors` 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="b7e07-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![请勿将 jQuery. 支持 cors 设置为 true](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="b7e07-226">SignalR 处理 JSONP 或 CORS 的使用。</span><span class="sxs-lookup"><span data-stu-id="b7e07-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="b7e07-227">如果将 `jQuery.support.cors` 设置为 true，则将禁用 JSONP，因为这会导致 SignalR 假定浏览器支持 CORS。</span><span class="sxs-lookup"><span data-stu-id="b7e07-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="b7e07-228">当你连接到 localhost URL 时，Internet Explorer 10 不会将其视为跨域连接，因此，即使你未在服务器上启用跨域连接，应用程序也会在本地使用 IE 10。</span><span class="sxs-lookup"><span data-stu-id="b7e07-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="b7e07-229">有关使用 Internet Explorer 9 的跨域连接的信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="b7e07-230">有关将跨域连接与 Chrome 一起使用的信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="b7e07-231">示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="b7e07-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="b7e07-232">有关如何指定其他基 URL 的信息，请参阅[ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="b7e07-233">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="b7e07-233">How to configure the connection</span></span>

<span data-ttu-id="b7e07-234">在建立连接之前，您可以指定查询字符串参数或指定传输方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="b7e07-235">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="b7e07-235">How to specify query string parameters</span></span>

<span data-ttu-id="b7e07-236">如果要在客户端连接时将数据发送到服务器，则可以将查询字符串参数添加到连接对象。</span><span class="sxs-lookup"><span data-stu-id="b7e07-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="b7e07-237">下面的示例演示如何在客户端代码中设置查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="b7e07-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="b7e07-238">**在调用 start 方法之前设置查询字符串值（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="b7e07-239">**在调用 start 方法之前设置查询字符串值（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="b7e07-240">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="b7e07-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="b7e07-241">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="b7e07-241">How to specify the transport method</span></span>

<span data-ttu-id="b7e07-242">作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="b7e07-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="b7e07-243">如果已知道要使用的传输，则在调用 `start` 方法时，可以通过指定传输方法来绕过此协商过程。</span><span class="sxs-lookup"><span data-stu-id="b7e07-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="b7e07-244">**用于指定传输方法（带有生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="b7e07-245">**指定传输方法（不包含生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="b7e07-246">作为替代方法，你可以按你希望 SignalR 尝试的顺序指定多个传输方法：</span><span class="sxs-lookup"><span data-stu-id="b7e07-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="b7e07-247">**指定自定义传输回退方案（使用生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="b7e07-248">**指定自定义传输回退方案（不包含生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="b7e07-249">您可以使用以下值来指定传输方法：</span><span class="sxs-lookup"><span data-stu-id="b7e07-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="b7e07-250">Websocket</span><span class="sxs-lookup"><span data-stu-id="b7e07-250">"webSockets"</span></span>
- <span data-ttu-id="b7e07-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="b7e07-251">"foreverFrame"</span></span>
- <span data-ttu-id="b7e07-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="b7e07-252">"serverSentEvents"</span></span>
- <span data-ttu-id="b7e07-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="b7e07-253">"longPolling"</span></span>

<span data-ttu-id="b7e07-254">下面的示例演示如何查明某个连接正在使用哪种传输方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="b7e07-255">**显示连接使用的传输方法（使用生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="b7e07-256">**显示连接使用的传输方法（没有生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="b7e07-257">有关如何在服务器代码中检查传输方法的信息，请参阅[ASP.NET SignalR HUB API 指南-服务器-如何从上下文属性获取有关客户端的信息](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="b7e07-258">有关传输和回退的详细信息，请参阅[SignalR-传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="b7e07-259">如何获取集线器类的代理</span><span class="sxs-lookup"><span data-stu-id="b7e07-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="b7e07-260">你创建的每个连接对象将封装有关与包含一个或多个中心类的 SignalR 服务的连接的信息。</span><span class="sxs-lookup"><span data-stu-id="b7e07-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="b7e07-261">若要与 Hub 类通信，可以使用自己创建的代理对象（如果不使用生成的代理）或为你生成。</span><span class="sxs-lookup"><span data-stu-id="b7e07-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="b7e07-262">在客户端上，代理名称为集线器类名的 camel 大小写形式。</span><span class="sxs-lookup"><span data-stu-id="b7e07-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="b7e07-263">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="b7e07-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="b7e07-264">**服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="b7e07-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="b7e07-265">**获取对中心生成的客户端代理的引用**</span><span class="sxs-lookup"><span data-stu-id="b7e07-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="b7e07-266">**创建中心类的客户端代理（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="b7e07-267">如果使用 `HubName` 特性来修饰中心类，请使用完全相同的名称，而无需更改大小写。</span><span class="sxs-lookup"><span data-stu-id="b7e07-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="b7e07-268">**服务器上具有 HubName 属性的中心类**</span><span class="sxs-lookup"><span data-stu-id="b7e07-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="b7e07-269">**获取对中心生成的客户端代理的引用**</span><span class="sxs-lookup"><span data-stu-id="b7e07-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="b7e07-270">**创建中心类的客户端代理（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="b7e07-271">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="b7e07-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="b7e07-272">若要定义服务器可从集线器调用的方法，请使用生成的代理的 `client` 属性向中心代理添加一个事件处理程序，如果未使用生成的代理，则调用 `on` 方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="b7e07-273">参数可以是复杂对象。</span><span class="sxs-lookup"><span data-stu-id="b7e07-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="b7e07-274">在调用 `start` 方法之前添加事件处理程序以建立连接。</span><span class="sxs-lookup"><span data-stu-id="b7e07-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="b7e07-275">（如果要在调用 `start` 方法后添加事件处理程序，请参阅本文档前面[如何建立连接](#establishconnection)中的说明，并使用所示的语法来定义方法，而不使用生成的代理。）</span><span class="sxs-lookup"><span data-stu-id="b7e07-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="b7e07-276">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b7e07-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="b7e07-277">例如，服务器上的 `Clients.All.addContosoChatMessageToPage` 会在客户端上执行 `AddContosoChatMessageToPage`、`addContosoChatMessageToPage`或 `addcontosochatmessagetopage`。</span><span class="sxs-lookup"><span data-stu-id="b7e07-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="b7e07-278">**定义客户端上的方法（具有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="b7e07-279">**用于在客户端上定义方法的另一种方法（带有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="b7e07-280">**定义客户端上的方法（不包含生成的代理，或在调用 start 方法之后添加）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="b7e07-281">**调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="b7e07-282">下面的示例包含一个作为方法参数的复杂对象。</span><span class="sxs-lookup"><span data-stu-id="b7e07-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="b7e07-283">**在采用复杂对象（使用生成的代理）的客户端上定义方法**</span><span class="sxs-lookup"><span data-stu-id="b7e07-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="b7e07-284">**在采用复杂对象（没有生成的代理）的客户端上定义方法**</span><span class="sxs-lookup"><span data-stu-id="b7e07-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="b7e07-285">**定义复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="b7e07-286">**使用复杂对象调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="b7e07-287">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="b7e07-287">How to call server methods from the client</span></span>

<span data-ttu-id="b7e07-288">若要从客户端调用服务器方法，请在不使用生成的代理的情况下，使用生成的代理的 `server` 属性或中心代理上的 `invoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="b7e07-289">返回值可以是复杂对象。</span><span class="sxs-lookup"><span data-stu-id="b7e07-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="b7e07-290">在集线器上传入方法名称的 camel 大小写形式。</span><span class="sxs-lookup"><span data-stu-id="b7e07-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="b7e07-291">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="b7e07-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="b7e07-292">下面的示例演示如何调用没有返回值的服务器方法，以及如何调用具有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="b7e07-293">**不带 HubMethodName 属性的服务器方法**</span><span class="sxs-lookup"><span data-stu-id="b7e07-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="b7e07-294">**定义在参数中传递的复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="b7e07-295">**调用服务器方法（与生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="b7e07-296">**调用服务器方法（没有生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="b7e07-297">如果使用 `HubMethodName` 特性修饰了 Hub 方法，请在不更改大小写的情况下使用该名称。</span><span class="sxs-lookup"><span data-stu-id="b7e07-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="b7e07-298">具有 HubMethodName 属性的**服务器方法**</span><span class="sxs-lookup"><span data-stu-id="b7e07-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="b7e07-299">**调用服务器方法（与生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="b7e07-300">**调用服务器方法（没有生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="b7e07-301">前面的示例演示如何调用没有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="b7e07-302">下面的示例演示如何调用具有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="b7e07-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="b7e07-303">**具有返回值的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="b7e07-304">用于返回值的**Stock 类**</span><span class="sxs-lookup"><span data-stu-id="b7e07-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="b7e07-305">**调用服务器方法（与生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="b7e07-306">**调用服务器方法（没有生成的代理）的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="b7e07-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="b7e07-307">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="b7e07-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="b7e07-308">SignalR 提供以下连接生存期事件，你可以处理这些事件：</span><span class="sxs-lookup"><span data-stu-id="b7e07-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="b7e07-309">`starting`：在通过连接发送任何数据之前引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="b7e07-310">`received`：在连接上接收到任何数据时引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="b7e07-311">提供接收的数据。</span><span class="sxs-lookup"><span data-stu-id="b7e07-311">Provides the received data.</span></span>
- <span data-ttu-id="b7e07-312">`connectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="b7e07-313">`reconnecting`：基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="b7e07-314">`reconnected`：在基础传输重新连接后引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="b7e07-315">`stateChanged`：在连接状态发生更改时引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="b7e07-316">提供旧状态和新状态（连接、连接、重新连接或断开连接）。</span><span class="sxs-lookup"><span data-stu-id="b7e07-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="b7e07-317">`disconnected`：连接断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="b7e07-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="b7e07-318">例如，如果要在存在可能导致明显延迟的连接问题时显示警告消息，请处理 `connectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="b7e07-319">**处理 connectionSlow 事件（与生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="b7e07-320">**处理 connectionSlow 事件（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="b7e07-321">有关详细信息，请参阅[了解和处理 SignalR 中的连接生存期事件](index.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="b7e07-322">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="b7e07-322">How to handle errors</span></span>

<span data-ttu-id="b7e07-323">SignalR JavaScript 客户端提供可为其添加处理程序的 `error` 事件。</span><span class="sxs-lookup"><span data-stu-id="b7e07-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="b7e07-324">还可以使用 fail 方法为服务器方法调用导致的错误添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="b7e07-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="b7e07-325">如果未在服务器上显式启用详细的错误消息，则在出现错误后 SignalR 返回的异常对象包含有关错误的最小信息。</span><span class="sxs-lookup"><span data-stu-id="b7e07-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="b7e07-326">例如，如果对 `newContosoChatMessage` 的调用失败，则出于安全原因，不建议将错误对象中的错误消息包含 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 向生产中的客户端发送详细的错误消息，但如果想要启用详细的错误消息以进行故障排除，请在服务器上使用以下代码。</span><span class="sxs-lookup"><span data-stu-id="b7e07-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="b7e07-327">下面的示例演示如何为错误事件添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="b7e07-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="b7e07-328">**添加错误处理程序（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="b7e07-329">**添加错误处理程序（没有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="b7e07-330">下面的示例演示如何处理方法调用中的错误。</span><span class="sxs-lookup"><span data-stu-id="b7e07-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="b7e07-331">**处理方法调用中的错误（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="b7e07-332">**处理方法调用中的错误（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="b7e07-333">如果方法调用失败，则也会引发 `error` 事件，因此将执行 `error` 方法处理程序和 `.fail` 方法回调中的代码。</span><span class="sxs-lookup"><span data-stu-id="b7e07-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="b7e07-334">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="b7e07-334">How to enable client-side logging</span></span>

<span data-ttu-id="b7e07-335">若要对连接启用客户端日志记录，请在调用 `start` 方法来建立连接之前，设置连接对象上的 `logging` 属性。</span><span class="sxs-lookup"><span data-stu-id="b7e07-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="b7e07-336">**启用日志记录（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="b7e07-337">**启用日志记录（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="b7e07-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="b7e07-338">若要查看日志，请打开浏览器的开发人员工具，并切换到 "控制台" 选项卡。有关显示如何执行此操作的分步说明和屏幕截图的教程，请参阅[使用 ASP.NET Signalr 进行服务器广播-启用日志记录](index.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e07-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
