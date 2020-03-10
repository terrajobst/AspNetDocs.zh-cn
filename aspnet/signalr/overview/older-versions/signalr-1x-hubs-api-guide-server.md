---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR Hub API 指南-Server （SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文档介绍如何对 SignalR 版本1.1 的 ASP.NET SignalR Hub API 的服务器端编程，并提供代码示例 demonstratin 。
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: d9cd3fad36c0300d96c6dbdc61291ef119da2327
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468128"
---
# <a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="9e449-103">ASP.NET SignalR Hub API 指南-Server （SignalR 1.x）</span><span class="sxs-lookup"><span data-stu-id="9e449-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>

<span data-ttu-id="9e449-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9e449-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="9e449-105">本文档介绍了如何对 SignalR 版本1.1 的 ASP.NET SignalR Hub API 的服务器端进行编程，其中的代码示例演示了常见选项。</span><span class="sxs-lookup"><span data-stu-id="9e449-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="9e449-106">利用 SignalR 中心 API，你可以将服务器中的远程过程调用（Rpc）连接到已连接的客户端和客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="9e449-107">在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="9e449-108">在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="9e449-109">SignalR 负责处理所有的客户端到服务器的操作。</span><span class="sxs-lookup"><span data-stu-id="9e449-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="9e449-110">SignalR 还提供名为持久性连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="9e449-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="9e449-111">有关 SignalR、集线器和持久性连接的简介，或有关演示如何生成完整 SignalR 应用程序的教程，请参阅[SignalR-入门](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9e449-112">概述</span><span class="sxs-lookup"><span data-stu-id="9e449-112">Overview</span></span>

<span data-ttu-id="9e449-113">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="9e449-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="9e449-114">如何注册 SignalR 路由并配置 SignalR 选项</span><span class="sxs-lookup"><span data-stu-id="9e449-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="9e449-115">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="9e449-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="9e449-116">配置 SignalR 选项</span><span class="sxs-lookup"><span data-stu-id="9e449-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="9e449-117">如何创建和使用集线器类</span><span class="sxs-lookup"><span data-stu-id="9e449-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="9e449-118">中心对象生存期</span><span class="sxs-lookup"><span data-stu-id="9e449-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="9e449-119">JavaScript 客户端中集线器名称的大小写大小写</span><span class="sxs-lookup"><span data-stu-id="9e449-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="9e449-120">多个中心</span><span class="sxs-lookup"><span data-stu-id="9e449-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="9e449-121">如何在 Hub 类中定义客户端可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="9e449-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="9e449-122">JavaScript 客户端中方法名称的大小写大小写</span><span class="sxs-lookup"><span data-stu-id="9e449-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="9e449-123">何时异步执行</span><span class="sxs-lookup"><span data-stu-id="9e449-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="9e449-124">定义重载</span><span class="sxs-lookup"><span data-stu-id="9e449-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="9e449-125">如何从中心类调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="9e449-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="9e449-126">选择将接收 RPC 的客户端</span><span class="sxs-lookup"><span data-stu-id="9e449-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="9e449-127">没有方法名称的编译时验证</span><span class="sxs-lookup"><span data-stu-id="9e449-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="9e449-128">不区分大小写的方法名称匹配</span><span class="sxs-lookup"><span data-stu-id="9e449-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="9e449-129">异步执行</span><span class="sxs-lookup"><span data-stu-id="9e449-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="9e449-130">如何从中心类管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="9e449-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="9e449-131">异步执行添加和移除方法</span><span class="sxs-lookup"><span data-stu-id="9e449-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="9e449-132">组成员持久性</span><span class="sxs-lookup"><span data-stu-id="9e449-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="9e449-133">单用户组</span><span class="sxs-lookup"><span data-stu-id="9e449-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="9e449-134">如何处理中心类中的连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="9e449-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="9e449-135">如果调用 OnConnected、OnDisconnected 和 OnReconnected</span><span class="sxs-lookup"><span data-stu-id="9e449-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="9e449-136">未填充调用方状态</span><span class="sxs-lookup"><span data-stu-id="9e449-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="9e449-137">如何从上下文属性获取有关客户端的信息</span><span class="sxs-lookup"><span data-stu-id="9e449-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="9e449-138">如何在客户端和中心类之间传递状态</span><span class="sxs-lookup"><span data-stu-id="9e449-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="9e449-139">如何处理中心类中的错误</span><span class="sxs-lookup"><span data-stu-id="9e449-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="9e449-140">如何从中心类的外部调用客户端方法和管理组</span><span class="sxs-lookup"><span data-stu-id="9e449-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="9e449-141">调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="9e449-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="9e449-142">管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="9e449-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="9e449-143">如何启用跟踪</span><span class="sxs-lookup"><span data-stu-id="9e449-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="9e449-144">如何自定义集线器管道</span><span class="sxs-lookup"><span data-stu-id="9e449-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="9e449-145">有关如何对客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="9e449-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="9e449-146">SignalR 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="9e449-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="9e449-147">SignalR 中心 API 指南-.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="9e449-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="9e449-148">API 参考主题的链接适用于 .NET 4.5 版本的 API。</span><span class="sxs-lookup"><span data-stu-id="9e449-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="9e449-149">如果使用的是 .NET 4，请参阅[.net 4 版本的 API 主题](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9e449-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="9e449-150">如何注册 SignalR 路由并配置 SignalR 选项</span><span class="sxs-lookup"><span data-stu-id="9e449-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="9e449-151">若要定义客户端将用于连接到中心的路由，请在应用程序启动时调用[routeconfig](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="9e449-152">`MapHubs` 是 `System.Web.Routing.RouteCollection` 类的[扩展方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9e449-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="9e449-153">下面的示例演示如何在*global.asax*文件中定义 SignalR hub 路由。</span><span class="sxs-lookup"><span data-stu-id="9e449-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="9e449-154">如果要将 SignalR 功能添加到 ASP.NET MVC 应用程序，请确保将 SignalR 路由添加到其他路由之前。</span><span class="sxs-lookup"><span data-stu-id="9e449-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="9e449-155">有关详细信息，请参阅[教程：入门 With SignalR AND MVC 4](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="9e449-156">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="9e449-156">The /signalr URL</span></span>

<span data-ttu-id="9e449-157">默认情况下，客户端将用于连接到中心的路由 URL 为 "/signalr"。</span><span class="sxs-lookup"><span data-stu-id="9e449-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="9e449-158">（请不要将此 URL 与自动生成的 JavaScript 文件的 "/signalr/hubs" URL 混淆。</span><span class="sxs-lookup"><span data-stu-id="9e449-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="9e449-159">有关生成的代理的详细信息，请参阅[SignalR 中心 API 指南-JavaScript 客户端-生成的代理及其功能](index.md)。）</span><span class="sxs-lookup"><span data-stu-id="9e449-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="9e449-160">可能会出现一些特殊情况，使此基 URL 无法用于 SignalR;例如，你的项目中有一个名为*signalr*的文件夹，并且你不希望更改该名称。</span><span class="sxs-lookup"><span data-stu-id="9e449-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="9e449-161">在这种情况下，可以更改基 URL，如以下示例中所示（将示例代码中的 "/signalr" 替换为所需 URL）。</span><span class="sxs-lookup"><span data-stu-id="9e449-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="9e449-162">**指定 URL 的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="9e449-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="9e449-163">**指定 URL 的 JavaScript 客户端代码（包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="9e449-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="9e449-164">**指定 URL （不包含生成的代理）的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="9e449-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="9e449-165">**指定 URL 的 .NET 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="9e449-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="9e449-166">配置 SignalR 选项</span><span class="sxs-lookup"><span data-stu-id="9e449-166">Configuring SignalR Options</span></span>

<span data-ttu-id="9e449-167">使用 `MapHubs` 方法的重载可指定自定义 URL、自定义依赖关系解析程序和以下选项：</span><span class="sxs-lookup"><span data-stu-id="9e449-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="9e449-168">从浏览器客户端启用跨域调用。</span><span class="sxs-lookup"><span data-stu-id="9e449-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="9e449-169">通常情况下，当浏览器从 `http://contoso.com`加载页面时，SignalR 连接位于同一域中 `http://contoso.com/signalr`。</span><span class="sxs-lookup"><span data-stu-id="9e449-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="9e449-170">如果 `http://contoso.com` 的页面与 `http://fabrikam.com/signalr`建立连接，则这是一个跨域连接。</span><span class="sxs-lookup"><span data-stu-id="9e449-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="9e449-171">出于安全原因，在默认情况下将禁用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="9e449-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="9e449-172">有关详细信息，请参阅[ASP.NET SignalR HUB API 指南-JavaScript 客户端-如何建立跨域连接](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="9e449-173">启用详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="9e449-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="9e449-174">出现错误时，SignalR 的默认行为是向客户端发送一条通知消息，而不会详细说明发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="9e449-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="9e449-175">不建议在生产环境中向客户端发送详细的错误信息，因为恶意用户可能会对你的应用程序使用该信息。</span><span class="sxs-lookup"><span data-stu-id="9e449-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="9e449-176">若要进行故障排除，可以使用此选项来暂时启用更丰富的错误报告。</span><span class="sxs-lookup"><span data-stu-id="9e449-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="9e449-177">禁用自动生成的 JavaScript 代理文件。</span><span class="sxs-lookup"><span data-stu-id="9e449-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="9e449-178">默认情况下，会生成一个带有中心类代理的 JavaScript 文件，以响应 URL "/signalr/hubs"。</span><span class="sxs-lookup"><span data-stu-id="9e449-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="9e449-179">如果你不想使用 JavaScript 代理，或者要手动生成此文件并在客户端中引用物理文件，则可以使用此选项来禁用代理生成。</span><span class="sxs-lookup"><span data-stu-id="9e449-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="9e449-180">有关详细信息，请参阅[SignalR 中心 API 指南-JavaScript 客户端-如何为 SignalR 生成的代理创建物理文件](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="9e449-181">下面的示例演示如何在对 `MapHubs` 方法的调用中指定 SignalR 连接 URL 和这些选项。</span><span class="sxs-lookup"><span data-stu-id="9e449-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="9e449-182">若要指定自定义 URL，请将示例中的 "/signalr" 替换为要使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="9e449-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="9e449-183">如何创建和使用集线器类</span><span class="sxs-lookup"><span data-stu-id="9e449-183">How to create and use Hub classes</span></span>

<span data-ttu-id="9e449-184">若要创建集线器，请创建一个从[Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)派生的类。</span><span class="sxs-lookup"><span data-stu-id="9e449-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="9e449-185">下面的示例演示了聊天应用程序的简单集线器类。</span><span class="sxs-lookup"><span data-stu-id="9e449-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="9e449-186">在此示例中，连接的客户端可以调用 `NewContosoChatMessage` 方法，在此情况下，接收的数据将广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="9e449-187">中心对象生存期</span><span class="sxs-lookup"><span data-stu-id="9e449-187">Hub object lifetime</span></span>

<span data-ttu-id="9e449-188">不会在服务器上实例化 Hub 类或从自己的代码中调用其方法;SignalR 中心管道完成的所有操作。</span><span class="sxs-lookup"><span data-stu-id="9e449-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="9e449-189">SignalR 创建中心类的新实例，每次需要处理集线器操作时，例如客户端连接、断开连接或对服务器进行方法调用时。</span><span class="sxs-lookup"><span data-stu-id="9e449-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="9e449-190">由于 Hub 类的实例是暂时性的，因此不能使用它们来维护对下一个方法调用的状态。</span><span class="sxs-lookup"><span data-stu-id="9e449-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="9e449-191">每次服务器接收来自客户端的方法调用时，中心类的新实例就会处理该消息。</span><span class="sxs-lookup"><span data-stu-id="9e449-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="9e449-192">若要通过多个连接和方法调用来维护状态，请使用一些其他方法（例如数据库）或中心类的静态变量，或不从 `Hub`派生的不同类。</span><span class="sxs-lookup"><span data-stu-id="9e449-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="9e449-193">如果在内存中保留数据，则使用方法（如中心类上的静态变量）将在应用程序域回收时丢失数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="9e449-194">如果要将消息从你自己的运行中心类的代码中发送到客户端，则无法通过实例化集线器类实例来执行此操作，但可以通过获取中心类的 SignalR 上下文对象的引用来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="9e449-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="9e449-195">有关详细信息，请参阅本主题后面的[如何从此中心类外部调用客户端方法和管理组](#callfromoutsidehub)。</span><span class="sxs-lookup"><span data-stu-id="9e449-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="9e449-196">JavaScript 客户端中集线器名称的大小写大小写</span><span class="sxs-lookup"><span data-stu-id="9e449-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="9e449-197">默认情况下，JavaScript 客户端使用类名的 camel 大小写形式引用中心。</span><span class="sxs-lookup"><span data-stu-id="9e449-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="9e449-198">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="9e449-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="9e449-199">前面的示例在 JavaScript 代码中称为 `contosoChatHub`。</span><span class="sxs-lookup"><span data-stu-id="9e449-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="9e449-200">**服务器**</span><span class="sxs-lookup"><span data-stu-id="9e449-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="9e449-201">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="9e449-202">若要为客户端指定不同的名称，请添加 `HubName` 特性。</span><span class="sxs-lookup"><span data-stu-id="9e449-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="9e449-203">使用 `HubName` 特性时，JavaScript 客户端上不会更改为 camel 大小写格式。</span><span class="sxs-lookup"><span data-stu-id="9e449-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="9e449-204">**服务器**</span><span class="sxs-lookup"><span data-stu-id="9e449-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="9e449-205">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="9e449-206">多个中心</span><span class="sxs-lookup"><span data-stu-id="9e449-206">Multiple Hubs</span></span>

<span data-ttu-id="9e449-207">可以在一个应用程序中定义多个集线器类。</span><span class="sxs-lookup"><span data-stu-id="9e449-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="9e449-208">当你执行此操作时，将共享连接，但组是不同的：</span><span class="sxs-lookup"><span data-stu-id="9e449-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="9e449-209">所有客户端都将使用相同的 URL 来与服务建立 SignalR 连接（如果指定了 "/signalr" 或自定义 URL），并且该连接用于该服务定义的所有中心。</span><span class="sxs-lookup"><span data-stu-id="9e449-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="9e449-210">与定义单个类中的所有集线器功能相比，多个中心没有性能差异。</span><span class="sxs-lookup"><span data-stu-id="9e449-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="9e449-211">所有中心获取相同的 HTTP 请求信息。</span><span class="sxs-lookup"><span data-stu-id="9e449-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="9e449-212">由于所有中心共享相同的连接，因此服务器获取的 HTTP 请求信息仅是建立 SignalR 连接的原始 HTTP 请求的信息。</span><span class="sxs-lookup"><span data-stu-id="9e449-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="9e449-213">如果使用连接请求通过指定查询字符串将信息从客户端传递到服务器，则不能向不同的中心提供不同的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="9e449-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="9e449-214">所有集线器都将接收相同的信息。</span><span class="sxs-lookup"><span data-stu-id="9e449-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="9e449-215">生成的 JavaScript 代理文件将包含一个文件中所有中心的代理。</span><span class="sxs-lookup"><span data-stu-id="9e449-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="9e449-216">有关 JavaScript 代理的信息，请参阅[SignalR 中心 API 指南-JavaScript 客户端-生成的代理及其功能](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="9e449-217">组在中心内定义。</span><span class="sxs-lookup"><span data-stu-id="9e449-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="9e449-218">在 SignalR 中，可以定义要广播到已连接的客户端子集的命名组。</span><span class="sxs-lookup"><span data-stu-id="9e449-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="9e449-219">为每个中心单独维护组。</span><span class="sxs-lookup"><span data-stu-id="9e449-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="9e449-220">例如，名为 "Administrators" 的组将包括一组适用于你的 `ContosoChatHub` 类的客户端，相同的组名将引用一组不同的客户端作为 `StockTickerHub` 类。</span><span class="sxs-lookup"><span data-stu-id="9e449-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="9e449-221">如何在 Hub 类中定义客户端可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="9e449-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="9e449-222">若要在要从客户端调用的中心公开方法，请声明一个公共方法，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="9e449-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="9e449-223">您可以指定返回类型和参数（包括复杂类型和数组），就像在任何C#方法中一样。</span><span class="sxs-lookup"><span data-stu-id="9e449-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="9e449-224">您在参数中接收或返回到调用方的任何数据都通过使用 JSON 在客户端和服务器之间进行通信，而 SignalR 会自动处理复杂对象和对象数组的绑定。</span><span class="sxs-lookup"><span data-stu-id="9e449-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="9e449-225">JavaScript 客户端中方法名称的大小写大小写</span><span class="sxs-lookup"><span data-stu-id="9e449-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="9e449-226">默认情况下，JavaScript 客户端通过使用方法名称的 camel 大小写形式来引用中心方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="9e449-227">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="9e449-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="9e449-228">**服务器**</span><span class="sxs-lookup"><span data-stu-id="9e449-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="9e449-229">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="9e449-230">若要为客户端指定不同的名称，请添加 `HubMethodName` 特性。</span><span class="sxs-lookup"><span data-stu-id="9e449-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="9e449-231">**服务器**</span><span class="sxs-lookup"><span data-stu-id="9e449-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="9e449-232">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="9e449-233">何时异步执行</span><span class="sxs-lookup"><span data-stu-id="9e449-233">When to execute asynchronously</span></span>

<span data-ttu-id="9e449-234">如果该方法将是长时间运行的，或者必须执行涉及等待的工作（如数据库查找或 web 服务调用），则通过返回[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)（代替 `void` 返回）或[task&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx)对象（取代 `T` 返回类型）使中心方法异步。</span><span class="sxs-lookup"><span data-stu-id="9e449-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="9e449-235">当你从方法返回 `Task` 对象时，SignalR 会等待 `Task` 完成，然后将已解包的结果发送回客户端，因此在客户端编写方法调用的方式没有差别。</span><span class="sxs-lookup"><span data-stu-id="9e449-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="9e449-236">使中心方法异步可避免在使用 WebSocket 传输时阻止连接。</span><span class="sxs-lookup"><span data-stu-id="9e449-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="9e449-237">当集线器方法同步执行且传输为 WebSocket 时，将阻止来自同一客户端的集线器上的方法的后续调用，直到集线器方法完成。</span><span class="sxs-lookup"><span data-stu-id="9e449-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="9e449-238">下面的示例演示了编码为同步或异步运行的同一方法，后跟用于调用任一版本的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="9e449-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="9e449-239">**同步**</span><span class="sxs-lookup"><span data-stu-id="9e449-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="9e449-240">**ASP.NET 4。5**</span><span class="sxs-lookup"><span data-stu-id="9e449-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="9e449-241">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="9e449-242">有关如何在 ASP.NET 4.5 中使用异步方法的详细信息，请参阅[在 ASP.NET MVC 4 中使用异步方法](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="9e449-243">定义重载</span><span class="sxs-lookup"><span data-stu-id="9e449-243">Defining Overloads</span></span>

<span data-ttu-id="9e449-244">如果要定义方法的重载，每个重载中的参数数量必须不同。</span><span class="sxs-lookup"><span data-stu-id="9e449-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="9e449-245">如果只是通过指定不同的参数类型来区分重载，则中心类将编译，但当客户端尝试调用某个重载时，SignalR 服务将在运行时引发异常。</span><span class="sxs-lookup"><span data-stu-id="9e449-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="9e449-246">如何从中心类调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="9e449-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="9e449-247">若要从服务器调用客户端方法，请使用集线器类中方法的 `Clients` 属性。</span><span class="sxs-lookup"><span data-stu-id="9e449-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="9e449-248">下面的示例演示了在所有连接的客户端上调用 `addNewMessageToPage` 的服务器代码，以及在 JavaScript 客户端中定义方法的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="9e449-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="9e449-249">**服务器**</span><span class="sxs-lookup"><span data-stu-id="9e449-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="9e449-250">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="9e449-251">无法从客户端方法获取返回值;`int x = Clients.All.add(1,1)` 语法不起作用。</span><span class="sxs-lookup"><span data-stu-id="9e449-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="9e449-252">可以指定复杂类型和参数的数组。</span><span class="sxs-lookup"><span data-stu-id="9e449-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="9e449-253">下面的示例将一个复杂类型传递给方法参数中的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="9e449-254">**使用复杂对象调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="9e449-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="9e449-255">**定义复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="9e449-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="9e449-256">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="9e449-257">选择将接收 RPC 的客户端</span><span class="sxs-lookup"><span data-stu-id="9e449-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="9e449-258">Clients 属性返回一个[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)对象，该对象提供几个选项用于指定哪些客户端将接收 RPC：</span><span class="sxs-lookup"><span data-stu-id="9e449-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="9e449-259">所有已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="9e449-260">仅调用客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="9e449-261">除调用客户端之外的所有客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="9e449-262">由连接 ID 标识的特定客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="9e449-263">此示例在调用客户端上调用 `addContosoChatMessageToPage`，其效果与使用 `Clients.Caller`相同。</span><span class="sxs-lookup"><span data-stu-id="9e449-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="9e449-264">除指定客户端之外的所有连接的客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="9e449-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="9e449-265">指定组中的所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="9e449-266">指定组中除指定的客户端之外的所有连接的客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="9e449-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="9e449-267">指定组中除调用客户端之外的所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="9e449-268">没有方法名称的编译时验证</span><span class="sxs-lookup"><span data-stu-id="9e449-268">No compile-time validation for method names</span></span>

<span data-ttu-id="9e449-269">指定的方法名称被解释为动态对象，这意味着它没有 IntelliSense 或编译时验证。</span><span class="sxs-lookup"><span data-stu-id="9e449-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="9e449-270">在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="9e449-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="9e449-271">当执行方法调用时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有与名称匹配的方法，则调用该方法，并将参数值传递给该方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="9e449-272">如果在客户端上找不到匹配的方法，则不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="9e449-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="9e449-273">有关在调用客户端方法时 SignalR 传输到后台客户端的数据格式的信息，请参阅[SignalR 简介](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="9e449-274">不区分大小写的方法名称匹配</span><span class="sxs-lookup"><span data-stu-id="9e449-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="9e449-275">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="9e449-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="9e449-276">例如，服务器上的 `Clients.All.addContosoChatMessageToPage` 会在客户端上执行 `AddContosoChatMessageToPage`、`addcontosochatmessagetopage`或 `addContosoChatMessageToPage`。</span><span class="sxs-lookup"><span data-stu-id="9e449-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="9e449-277">异步执行</span><span class="sxs-lookup"><span data-stu-id="9e449-277">Asynchronous execution</span></span>

<span data-ttu-id="9e449-278">调用的方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="9e449-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="9e449-279">对客户端调用方法之后的任何代码都将立即执行，而无需等待 SignalR 完成将数据传输到客户端的操作，除非指定后续代码行应等待方法完成。</span><span class="sxs-lookup"><span data-stu-id="9e449-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="9e449-280">下面的代码示例演示如何按顺序执行两个客户端方法：一种方法是使用 .NET 4.5 中的代码，另一种方法是在 .NET 4 中使用的代码。</span><span class="sxs-lookup"><span data-stu-id="9e449-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="9e449-281">**.NET 4.5 示例**</span><span class="sxs-lookup"><span data-stu-id="9e449-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="9e449-282">**.NET 4 示例**</span><span class="sxs-lookup"><span data-stu-id="9e449-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="9e449-283">如果使用 `await` 或 `ContinueWith` 等待客户端方法在下一行代码执行之前完成，这并不意味着客户端将在执行下一行代码之前实际接收消息。</span><span class="sxs-lookup"><span data-stu-id="9e449-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="9e449-284">仅客户端方法调用的 "完成" 表示 SignalR 已完成发送消息所需的所有操作。</span><span class="sxs-lookup"><span data-stu-id="9e449-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="9e449-285">如果需要客户端接收消息的验证，则必须自行编写该机制。</span><span class="sxs-lookup"><span data-stu-id="9e449-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="9e449-286">例如，可以在中心对 `MessageReceived` 方法进行编码，并且在 `MessageReceived` 客户端上的 `addContosoChatMessageToPage` 方法中，你可以在完成需要在客户端上执行的任何工作。</span><span class="sxs-lookup"><span data-stu-id="9e449-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="9e449-287">在中心 `MessageReceived` 中，你可以执行任何操作，具体取决于原始方法调用的实际客户端接收和处理。</span><span class="sxs-lookup"><span data-stu-id="9e449-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="9e449-288">如何使用字符串变量作为方法名称</span><span class="sxs-lookup"><span data-stu-id="9e449-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="9e449-289">如果要使用字符串变量作为方法名称来调用客户端方法，请 `IClientProxy` 将 `Clients.All` （或 `Clients.Others`，`Clients.Caller`等）强制转换为，然后调用[invoke （方法名称，参数 ...）](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9e449-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="9e449-290">如何从中心类管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="9e449-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="9e449-291">SignalR 中的组提供一种方法，用于将消息广播到连接的已连接客户端的指定子集。</span><span class="sxs-lookup"><span data-stu-id="9e449-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="9e449-292">一个组可以具有任意数量的客户端，客户端可以是任意数量的组的成员。</span><span class="sxs-lookup"><span data-stu-id="9e449-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="9e449-293">若要管理组成员身份，请使用 Hub 类的 `Groups` 属性提供的[添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)和[移除](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="9e449-294">下面的示例演示了在客户端代码调用的集线器方法中使用的 `Groups.Add` 和 `Groups.Remove` 方法，以及调用它们的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="9e449-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="9e449-295">**服务器**</span><span class="sxs-lookup"><span data-stu-id="9e449-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="9e449-296">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="9e449-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="9e449-297">无需显式创建组。</span><span class="sxs-lookup"><span data-stu-id="9e449-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="9e449-298">实际上，在对 `Groups.Add`的调用中首次指定组的名称时，会自动创建一个组，并在从其成员身份中删除最后一个连接时将其删除。</span><span class="sxs-lookup"><span data-stu-id="9e449-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="9e449-299">没有用于获取组成员身份列表或组列表的 API。</span><span class="sxs-lookup"><span data-stu-id="9e449-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="9e449-300">SignalR 基于发布[/订阅模型](http://en.wikipedia.org/wiki/Publish/subscribe)将消息发送到客户端和组，并且服务器不维护组或组成员身份列表。</span><span class="sxs-lookup"><span data-stu-id="9e449-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="9e449-301">这有助于最大程度地提高可伸缩性，因为每次将节点添加到 web 场时，SignalR 维护的任何状态都必须传播到新节点。</span><span class="sxs-lookup"><span data-stu-id="9e449-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="9e449-302">异步执行添加和移除方法</span><span class="sxs-lookup"><span data-stu-id="9e449-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="9e449-303">`Groups.Add` 和 `Groups.Remove` 方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="9e449-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="9e449-304">如果要将客户端添加到组，并使用组立即将消息发送到客户端，必须确保 `Groups.Add` 方法先完成。</span><span class="sxs-lookup"><span data-stu-id="9e449-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="9e449-305">下面的代码示例演示如何执行此操作，一种方法是使用 .NET 4.5 中适用的代码，另一种方法是使用 .NET 4 中的代码</span><span class="sxs-lookup"><span data-stu-id="9e449-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="9e449-306">**.NET 4.5 示例**</span><span class="sxs-lookup"><span data-stu-id="9e449-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="9e449-307">**.NET 4 示例**</span><span class="sxs-lookup"><span data-stu-id="9e449-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="9e449-308">组成员持久性</span><span class="sxs-lookup"><span data-stu-id="9e449-308">Group membership persistence</span></span>

<span data-ttu-id="9e449-309">SignalR 跟踪连接，而不是用户，因此，如果希望用户在每次建立连接时都位于同一个组中，则必须在每次用户建立新连接时调用 `Groups.Add`。</span><span class="sxs-lookup"><span data-stu-id="9e449-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="9e449-310">暂时断开连接后，SignalR 可能会自动恢复连接。</span><span class="sxs-lookup"><span data-stu-id="9e449-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="9e449-311">在这种情况下，SignalR 将还原相同的连接，而不建立新的连接，因此客户端的组成员身份将自动还原。</span><span class="sxs-lookup"><span data-stu-id="9e449-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="9e449-312">即使暂时中断是服务器重启或失败的结果，也可能出现这种情况，因为每个客户端（包括组成员身份）的连接状态都将往返给客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="9e449-313">如果服务器发生故障，并且在连接超时之前被新服务器替换，则客户端可以自动重新连接到新的服务器并重新注册其所属的组。</span><span class="sxs-lookup"><span data-stu-id="9e449-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="9e449-314">当连接丢失或连接超时时，或者当客户端断开连接时（例如，当浏览器导航到新页面时），组成员身份将会丢失。</span><span class="sxs-lookup"><span data-stu-id="9e449-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="9e449-315">用户下次连接时将是新连接。</span><span class="sxs-lookup"><span data-stu-id="9e449-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="9e449-316">若要在同一个用户建立新连接时维护组成员身份，你的应用程序必须跟踪用户和组之间的关联，并在每次用户建立新连接时还原组成员身份。</span><span class="sxs-lookup"><span data-stu-id="9e449-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="9e449-317">有关连接和重新连接的详细信息，请参阅本主题后面的[如何处理 Hub 类中的连接生存期事件](#connectionlifetime)。</span><span class="sxs-lookup"><span data-stu-id="9e449-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="9e449-318">单用户组</span><span class="sxs-lookup"><span data-stu-id="9e449-318">Single-user groups</span></span>

<span data-ttu-id="9e449-319">使用 SignalR 的应用程序通常需要跟踪用户和连接之间的关联，以便知道哪个用户已发送消息以及哪些用户应该接收消息。</span><span class="sxs-lookup"><span data-stu-id="9e449-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="9e449-320">组用于执行此操作的两种常用模式之一。</span><span class="sxs-lookup"><span data-stu-id="9e449-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="9e449-321">单用户组。</span><span class="sxs-lookup"><span data-stu-id="9e449-321">Single-user groups.</span></span>

    <span data-ttu-id="9e449-322">你可以指定用户名作为组名称，并在每次用户连接或重新连接时将当前连接 ID 添加到组。</span><span class="sxs-lookup"><span data-stu-id="9e449-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="9e449-323">向发送到组的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="9e449-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="9e449-324">此方法的缺点是，组不会提供一种方法来找出用户处于联机还是脱机状态。</span><span class="sxs-lookup"><span data-stu-id="9e449-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="9e449-325">跟踪用户名和连接 Id 之间的关联。</span><span class="sxs-lookup"><span data-stu-id="9e449-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="9e449-326">你可以在每个用户名与字典或数据库中的一个或多个连接 Id 之间存储关联，并在每次用户连接或断开连接时更新存储的数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="9e449-327">若要向用户发送消息，请指定连接 Id。</span><span class="sxs-lookup"><span data-stu-id="9e449-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="9e449-328">此方法的一个缺点是它会占用更多内存。</span><span class="sxs-lookup"><span data-stu-id="9e449-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="9e449-329">如何处理中心类中的连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="9e449-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="9e449-330">处理连接生存期事件的典型原因是跟踪用户是否已连接，以及跟踪用户名和连接 Id 之间的关联。</span><span class="sxs-lookup"><span data-stu-id="9e449-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="9e449-331">若要在客户端连接或断开连接时运行你自己的代码，请重写中心类的 `OnConnected`、`OnDisconnected`和 `OnReconnected` 虚拟方法，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="9e449-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="9e449-332">如果调用 OnConnected、OnDisconnected 和 OnReconnected</span><span class="sxs-lookup"><span data-stu-id="9e449-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="9e449-333">每次浏览器导航到新页时，必须建立新的连接，这意味着 SignalR 将执行 `OnDisconnected` 方法，后跟 `OnConnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="9e449-334">建立新连接时，SignalR 始终创建新的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="9e449-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="9e449-335">当 SignalR 可自动从其恢复的连接（如在连接超时之前暂时断开和重新连接）时，将调用 `OnReconnected` 方法。当客户端断开连接并且 SignalR 无法自动重新连接时（例如，当浏览器导航到新页面时），将调用 `OnDisconnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="9e449-336">因此，给定客户端的可能的事件序列 `OnConnected`、`OnReconnected``OnDisconnected`;或 `OnConnected`，`OnDisconnected`。</span><span class="sxs-lookup"><span data-stu-id="9e449-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="9e449-337">你不会看到给定连接 `OnConnected`、`OnDisconnected``OnReconnected` 的顺序。</span><span class="sxs-lookup"><span data-stu-id="9e449-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="9e449-338">在某些情况下（例如服务器出现故障或应用程序域回收时）不会调用 `OnDisconnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="9e449-339">当另一个服务器联机或应用程序域完成其回收时，某些客户端可能能够重新连接并激发 `OnReconnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="9e449-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="9e449-340">有关详细信息，请参阅[了解和处理 SignalR 中的连接生存期事件](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="9e449-341">未填充调用方状态</span><span class="sxs-lookup"><span data-stu-id="9e449-341">Caller state not populated</span></span>

<span data-ttu-id="9e449-342">连接生存期事件处理程序方法是从服务器调用的，这意味着在客户端上的 `state` 对象中放置的任何状态都不会在服务器上的 `Caller` 属性中填充。</span><span class="sxs-lookup"><span data-stu-id="9e449-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="9e449-343">有关 `state` 对象和 `Caller` 属性的信息，请参阅本主题后面的[如何在客户端和 Hub 类之间传递状态](#passstate)。</span><span class="sxs-lookup"><span data-stu-id="9e449-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="9e449-344">如何从上下文属性获取有关客户端的信息</span><span class="sxs-lookup"><span data-stu-id="9e449-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="9e449-345">若要获取有关客户端的信息，请使用 Hub 类的 `Context` 属性。</span><span class="sxs-lookup"><span data-stu-id="9e449-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="9e449-346">`Context` 属性返回一个[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)对象，该对象提供对以下信息的访问：</span><span class="sxs-lookup"><span data-stu-id="9e449-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="9e449-347">调用客户端的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="9e449-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="9e449-348">连接 ID 是 SignalR 分配的 GUID （您不能在自己的代码中指定值）。</span><span class="sxs-lookup"><span data-stu-id="9e449-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="9e449-349">每个连接都有一个连接 ID，如果应用程序中有多个中心，则所有中心都将使用相同的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="9e449-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="9e449-350">HTTP 标头数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="9e449-351">还可以从 `Context.Headers`获取 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="9e449-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="9e449-352">对同一事情进行多次引用的原因是：首先创建了 `Context.Headers`，后来添加了 `Context.Request` 属性，并保留了 `Context.Headers` 以便向后兼容。</span><span class="sxs-lookup"><span data-stu-id="9e449-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="9e449-353">查询字符串数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="9e449-354">您还可以从 `Context.QueryString`获取查询字符串数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="9e449-355">在此属性中获取的查询字符串是与建立 SignalR 连接的 HTTP 请求一起使用的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="9e449-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="9e449-356">您可以通过配置连接在客户端中添加查询字符串参数，这是将客户端的数据从客户端传递到服务器的一种简便方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="9e449-357">下面的示例演示了在使用生成的代理时在 JavaScript 客户端中添加查询字符串的一种方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="9e449-358">有关设置查询字符串参数的详细信息，请参阅[JavaScript](index.md)和[.net](index.md)客户端的 API 指南。</span><span class="sxs-lookup"><span data-stu-id="9e449-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="9e449-359">可以在查询字符串数据中找到用于连接的传输方法，还可以在 SignalR 内部使用某些其他值：</span><span class="sxs-lookup"><span data-stu-id="9e449-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="9e449-360">`transportMethod` 的值将为 "Websocket"、"serverSentEvents"、"foreverFrame" 或 "longPolling"。</span><span class="sxs-lookup"><span data-stu-id="9e449-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="9e449-361">请注意，如果您在 `OnConnected` 事件处理程序方法中检查此值，则在某些情况下，您最初可能会获得一个传输值，它不是连接的最终协商传输方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="9e449-362">在这种情况下，方法将引发异常，稍后在建立最终传输方法时将再次调用该方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="9e449-363">Cookie。</span><span class="sxs-lookup"><span data-stu-id="9e449-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="9e449-364">你还可以从 `Context.RequestCookies`获取 cookie。</span><span class="sxs-lookup"><span data-stu-id="9e449-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="9e449-365">用户信息。</span><span class="sxs-lookup"><span data-stu-id="9e449-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="9e449-366">请求的 HttpContext 对象：</span><span class="sxs-lookup"><span data-stu-id="9e449-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="9e449-367">使用此方法而不是获取 `HttpContext.Current` 来获取 SignalR 连接的 `HttpContext` 对象。</span><span class="sxs-lookup"><span data-stu-id="9e449-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="9e449-368">如何在客户端和中心类之间传递状态</span><span class="sxs-lookup"><span data-stu-id="9e449-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="9e449-369">客户端代理提供一个 `state` 对象，您可以在其中存储要使用每个方法调用传输到服务器的数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="9e449-370">在服务器上，可以通过客户端调用的集线器方法中的 `Clients.Caller` 属性访问此数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="9e449-371">`OnConnected`、`OnDisconnected`和 `OnReconnected`的连接生存期事件处理程序方法不会填充 `Clients.Caller` 属性。</span><span class="sxs-lookup"><span data-stu-id="9e449-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="9e449-372">在这两个方向上创建或更新 `state` 对象和 `Clients.Caller` 属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="9e449-373">您可以更新服务器中的值，并将这些值传递回客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="9e449-374">下面的示例演示了 JavaScript 客户端代码，该代码存储每个方法调用的用于传输到服务器的状态。</span><span class="sxs-lookup"><span data-stu-id="9e449-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="9e449-375">下面的示例演示 .NET 客户端中的等效代码。</span><span class="sxs-lookup"><span data-stu-id="9e449-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="9e449-376">在你的中心类中，你可以访问 `Clients.Caller` 属性中的这些数据。</span><span class="sxs-lookup"><span data-stu-id="9e449-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="9e449-377">下面的示例演示了检索上一示例中引用的状态的代码。</span><span class="sxs-lookup"><span data-stu-id="9e449-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="9e449-378">用于保持状态的这种机制不适用于大量数据，因为放入 `state` 或 `Clients.Caller` 属性的所有内容都将随每个方法调用一起往返。</span><span class="sxs-lookup"><span data-stu-id="9e449-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="9e449-379">它适用于较小的项，例如用户名或计数器。</span><span class="sxs-lookup"><span data-stu-id="9e449-379">It's useful for smaller items such as user names or counters.</span></span>

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="9e449-380">如何处理中心类中的错误</span><span class="sxs-lookup"><span data-stu-id="9e449-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="9e449-381">若要处理中心类方法中发生的错误，请使用以下方法之一或同时使用这两种方法之一：</span><span class="sxs-lookup"><span data-stu-id="9e449-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="9e449-382">在 try-catch 块中包装方法代码，并记录 exception 对象。</span><span class="sxs-lookup"><span data-stu-id="9e449-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="9e449-383">出于调试目的，您可以将异常发送到客户端，但出于安全原因，不建议将详细信息发送到生产中的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="9e449-384">创建处理[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法的集线器管道模块。</span><span class="sxs-lookup"><span data-stu-id="9e449-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="9e449-385">下面的示例演示一个管道模块，该模块记录错误，后跟 global.asax 中的代码，该模块将模块注入集线器管道。</span><span class="sxs-lookup"><span data-stu-id="9e449-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="9e449-386">有关集线器管道模块的详细信息，请参阅本主题后面的[如何自定义集线器管道](#hubpipeline)。</span><span class="sxs-lookup"><span data-stu-id="9e449-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="9e449-387">如何启用跟踪</span><span class="sxs-lookup"><span data-stu-id="9e449-387">How to enable tracing</span></span>

<span data-ttu-id="9e449-388">若要启用服务器端跟踪，请将一个 system.exception 元素添加到 Web.config 文件中，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="9e449-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="9e449-389">在 Visual Studio 中运行应用程序时，可以在 "**输出**" 窗口中查看日志。</span><span class="sxs-lookup"><span data-stu-id="9e449-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="9e449-390">如何从中心类的外部调用客户端方法和管理组</span><span class="sxs-lookup"><span data-stu-id="9e449-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="9e449-391">若要从不同于中心类的类调用客户端方法，请获取对中心的 SignalR 上下文对象的引用，并使用该对象调用客户端上的方法或管理组。</span><span class="sxs-lookup"><span data-stu-id="9e449-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="9e449-392">下面的示例 `StockTicker` 类获取上下文对象，将其存储在类的实例中，将类实例存储在静态属性中，并使用 singleton 类实例中的上下文对连接到名为 `StockTickerHub`的集线器的客户端调用 `updateStockPrice` 方法。</span><span class="sxs-lookup"><span data-stu-id="9e449-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="9e449-393">如果需要在长生存期的对象中多次使用上下文，请获取引用一次并保存，而不是每次都重新获取。</span><span class="sxs-lookup"><span data-stu-id="9e449-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="9e449-394">只要获取上下文，就可以确保 SignalR 将消息以集线器方法发出客户端方法调用的相同顺序发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="9e449-395">有关演示如何使用集线器的 SignalR 上下文的教程，请参阅[使用 ASP.NET SignalR 进行服务器广播](index.md)。</span><span class="sxs-lookup"><span data-stu-id="9e449-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="9e449-396">调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="9e449-396">Calling client methods</span></span>

<span data-ttu-id="9e449-397">您可以指定将接收 RPC 的客户端，但选择的选项比从集线器类调用时更少。</span><span class="sxs-lookup"><span data-stu-id="9e449-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="9e449-398">出现这种情况的原因是上下文未与客户端的特定调用相关联，因此，任何需要了解当前连接 ID 的方法（如 `Clients.Others`、`Clients.Caller`或 `Clients.OthersInGroup`）都不可用。</span><span class="sxs-lookup"><span data-stu-id="9e449-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="9e449-399">可用选项如下：</span><span class="sxs-lookup"><span data-stu-id="9e449-399">The following options are available:</span></span>

- <span data-ttu-id="9e449-400">所有已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="9e449-401">由连接 ID 标识的特定客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="9e449-402">除指定客户端之外的所有连接的客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="9e449-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="9e449-403">指定组中的所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="9e449-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="9e449-404">指定组中除指定的客户端之外的所有连接的客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="9e449-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="9e449-405">如果要从中心类中的方法调用到非集线器类，可以传入当前连接 ID 并将其与 `Clients.Client`、`Clients.AllExcept`或 `Clients.Group` 一起使用，以模拟 `Clients.Caller`、`Clients.Others`或 `Clients.OthersInGroup`。</span><span class="sxs-lookup"><span data-stu-id="9e449-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="9e449-406">在下面的示例中，`MoveShapeHub` 类将连接 ID 传递到 `Broadcaster` 类，以便 `Broadcaster` 类可以模拟 `Clients.Others`。</span><span class="sxs-lookup"><span data-stu-id="9e449-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="9e449-407">管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="9e449-407">Managing group membership</span></span>

<span data-ttu-id="9e449-408">对于管理组，你具有与在 Hub 类中相同的选项。</span><span class="sxs-lookup"><span data-stu-id="9e449-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="9e449-409">将客户端添加到组</span><span class="sxs-lookup"><span data-stu-id="9e449-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="9e449-410">从组中删除客户端</span><span class="sxs-lookup"><span data-stu-id="9e449-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="9e449-411">如何自定义集线器管道</span><span class="sxs-lookup"><span data-stu-id="9e449-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="9e449-412">SignalR 使你能够将自己的代码注入中心管道。</span><span class="sxs-lookup"><span data-stu-id="9e449-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="9e449-413">下面的示例演示一个自定义中心管道模块，该模块记录从客户端接收的每个传入方法调用，以及在客户端上调用的传出方法调用：</span><span class="sxs-lookup"><span data-stu-id="9e449-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="9e449-414">*Global.asax*文件中的以下代码注册要在中心管道中运行的模块：</span><span class="sxs-lookup"><span data-stu-id="9e449-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="9e449-415">有许多不同的方法可以重写。</span><span class="sxs-lookup"><span data-stu-id="9e449-415">There are many different methods that you can override.</span></span> <span data-ttu-id="9e449-416">有关完整列表，请参阅[HubPipelineModule 方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9e449-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
