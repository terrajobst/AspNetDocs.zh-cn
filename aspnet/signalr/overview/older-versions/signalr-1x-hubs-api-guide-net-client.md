---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR 中心 API 指南-.NET 客户端（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文档介绍了如何在 .NET 客户端中使用 SignalR 版本2的中心 API，例如 Windows 应用商店（WinRT）、WPF、Silverlight 和缺点 。
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505970"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a><span data-ttu-id="f29a2-103">ASP.NET SignalR 中心 API 指南-.NET 客户端（SignalR 1.x）</span><span class="sxs-lookup"><span data-stu-id="f29a2-103">ASP.NET SignalR Hubs API Guide - .NET Client (SignalR 1.x)</span></span>

<span data-ttu-id="f29a2-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f29a2-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f29a2-105">本文档介绍了如何在 .NET 客户端中使用 SignalR 版本2的中心 API，例如 Windows 应用商店（WinRT）、WPF、Silverlight 和控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="f29a2-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="f29a2-106">利用 SignalR 中心 API，你可以将服务器中的远程过程调用（Rpc）连接到已连接的客户端和客户端。</span><span class="sxs-lookup"><span data-stu-id="f29a2-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="f29a2-107">在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="f29a2-108">在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="f29a2-109">SignalR 负责处理所有的客户端到服务器的操作。</span><span class="sxs-lookup"><span data-stu-id="f29a2-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="f29a2-110">SignalR 还提供名为持久性连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="f29a2-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="f29a2-111">有关 SignalR、集线器和持久性连接的简介，或有关演示如何生成完整 SignalR 应用程序的教程，请参阅[SignalR-入门](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="f29a2-112">概述</span><span class="sxs-lookup"><span data-stu-id="f29a2-112">Overview</span></span>

<span data-ttu-id="f29a2-113">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="f29a2-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="f29a2-114">客户端设置</span><span class="sxs-lookup"><span data-stu-id="f29a2-114">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="f29a2-115">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="f29a2-115">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="f29a2-116">来自 Silverlight 客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="f29a2-116">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="f29a2-117">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="f29a2-117">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="f29a2-118">如何设置 WPF 客户端中的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="f29a2-118">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="f29a2-119">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="f29a2-119">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="f29a2-120">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-120">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="f29a2-121">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="f29a2-121">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="f29a2-122">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="f29a2-122">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="f29a2-123">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="f29a2-123">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="f29a2-124">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-124">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="f29a2-125">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-125">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="f29a2-126">带参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="f29a2-126">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="f29a2-127">带参数的方法，指定参数的动态对象</span><span class="sxs-lookup"><span data-stu-id="f29a2-127">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="f29a2-128">如何删除处理程序</span><span class="sxs-lookup"><span data-stu-id="f29a2-128">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="f29a2-129">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-129">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="f29a2-130">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="f29a2-130">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="f29a2-131">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="f29a2-131">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="f29a2-132">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="f29a2-132">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="f29a2-133">服务器可以调用的客户端方法的 WPF、Silverlight 和控制台应用程序代码示例</span><span class="sxs-lookup"><span data-stu-id="f29a2-133">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="f29a2-134">对于 .NET 客户端项目示例，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="f29a2-134">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="f29a2-135">[gustavo-GitHub.com 上的 armenta/SignalR](https://github.com/gustavo-armenta/SignalR-Samples) （WinRT，Silverlight，控制台应用程序示例）。</span><span class="sxs-lookup"><span data-stu-id="f29a2-135">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="f29a2-136">[DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GITHUB.COM （WPF 示例）。</span><span class="sxs-lookup"><span data-stu-id="f29a2-136">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="f29a2-137">GitHub.com 上的[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) （控制台应用示例）。</span><span class="sxs-lookup"><span data-stu-id="f29a2-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="f29a2-138">有关如何对服务器或 JavaScript 客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="f29a2-138">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="f29a2-139">SignalR 中心 API 指南-服务器</span><span class="sxs-lookup"><span data-stu-id="f29a2-139">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="f29a2-140">SignalR 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="f29a2-140">SignalR Hubs API Guide - JavaScript Client</span></span>](../guide-to-the-api/hubs-api-guide-javascript-client.md)

<span data-ttu-id="f29a2-141">API 参考主题的链接适用于 .NET 4.5 版本的 API。</span><span class="sxs-lookup"><span data-stu-id="f29a2-141">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="f29a2-142">如果使用的是 .NET 4，请参阅[.net 4 版本的 API 主题](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-142">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="f29a2-143">客户端设置</span><span class="sxs-lookup"><span data-stu-id="f29a2-143">Client setup</span></span>

<span data-ttu-id="f29a2-144">安装[SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 包（而不是[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包）（& e）。</span><span class="sxs-lookup"><span data-stu-id="f29a2-144">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="f29a2-145">对于 .NET 4 和 .NET 4.5，此包支持 WinRT、Silverlight、WPF、控制台应用程序和 Windows Phone 客户端。</span><span class="sxs-lookup"><span data-stu-id="f29a2-145">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="f29a2-146">如果客户端上的 SignalR 版本与服务器上的版本不同，则 SignalR 通常能够适应不同之处。</span><span class="sxs-lookup"><span data-stu-id="f29a2-146">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="f29a2-147">例如，当发布 SignalR 版本2.0，并在服务器上安装该版本时，服务器将支持安装了 1.1. x 的客户端以及安装有2.0 的客户端。</span><span class="sxs-lookup"><span data-stu-id="f29a2-147">For example, when SignalR version 2.0 is released and you install that on the server, the server will support clients that have 1.1.x installed as well as clients that have 2.0 installed.</span></span> <span data-ttu-id="f29a2-148">如果服务器上的版本与客户端上的版本之间的差异太大，则当客户端尝试建立连接时，SignalR 将引发 `InvalidOperationException` 异常。</span><span class="sxs-lookup"><span data-stu-id="f29a2-148">If the difference between the version on the server and the version on the client is too great, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="f29a2-149">错误消息为 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"。</span><span class="sxs-lookup"><span data-stu-id="f29a2-149">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="f29a2-150">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="f29a2-150">How to establish a connection</span></span>

<span data-ttu-id="f29a2-151">建立连接之前，必须先创建一个 `HubConnection` 对象并创建一个代理。</span><span class="sxs-lookup"><span data-stu-id="f29a2-151">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="f29a2-152">若要建立连接，请对 `HubConnection` 对象调用 `Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-152">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="f29a2-153">对于 JavaScript 客户端，你必须注册至少一个事件处理程序，然后才能调用 `Start` 方法来建立连接。</span><span class="sxs-lookup"><span data-stu-id="f29a2-153">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="f29a2-154">这不是 .NET 客户端所必需的。</span><span class="sxs-lookup"><span data-stu-id="f29a2-154">This is not necessary for .NET clients.</span></span> <span data-ttu-id="f29a2-155">对于 JavaScript 客户端，生成的代理代码会自动为服务器上存在的所有中心创建代理，并注册处理程序，以指示客户端打算使用哪些集线器。</span><span class="sxs-lookup"><span data-stu-id="f29a2-155">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="f29a2-156">但对于 .NET 客户端，你可以手动创建中心代理，因此 SignalR 假定你将使用为创建代理的任何集线器。</span><span class="sxs-lookup"><span data-stu-id="f29a2-156">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="f29a2-157">示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="f29a2-157">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="f29a2-158">有关如何指定其他基 URL 的信息，请参阅[ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-158">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="f29a2-159">`Start` 方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="f29a2-159">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="f29a2-160">若要确保后续代码行在建立连接之前不会执行，请使用 ASP.NET 4.5 异步方法中的 `await` 或在同步方法中 `.Wait()`。</span><span class="sxs-lookup"><span data-stu-id="f29a2-160">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="f29a2-161">请勿在 WinRT 客户端中使用 `.Wait()`。</span><span class="sxs-lookup"><span data-stu-id="f29a2-161">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<span data-ttu-id="f29a2-162">`HubConnection` 类是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="f29a2-162">The `HubConnection` class is thread-safe.</span></span>

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="f29a2-163">来自 Silverlight 客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="f29a2-163">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="f29a2-164">有关如何从 Silverlight 客户端启用跨域连接的信息，请参阅[使服务跨域边界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-164">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="f29a2-165">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="f29a2-165">How to configure the connection</span></span>

<span data-ttu-id="f29a2-166">在建立连接之前，您可以指定以下任一选项：</span><span class="sxs-lookup"><span data-stu-id="f29a2-166">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="f29a2-167">并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="f29a2-167">Concurrent connections limit.</span></span>
- <span data-ttu-id="f29a2-168">查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="f29a2-168">Query string parameters.</span></span>
- <span data-ttu-id="f29a2-169">传输方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-169">The transport method.</span></span>
- <span data-ttu-id="f29a2-170">HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="f29a2-170">HTTP headers.</span></span>
- <span data-ttu-id="f29a2-171">客户端证书。</span><span class="sxs-lookup"><span data-stu-id="f29a2-171">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="f29a2-172">如何设置 WPF 客户端中的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="f29a2-172">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="f29a2-173">在 WPF 客户端中，你可能必须将最大并发连接数从其默认值2增加到最大值。</span><span class="sxs-lookup"><span data-stu-id="f29a2-173">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="f29a2-174">建议值为10。</span><span class="sxs-lookup"><span data-stu-id="f29a2-174">The recommended value is 10.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="f29a2-175">有关详细信息，请参阅[ServicePointManager. servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-175">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="f29a2-176">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="f29a2-176">How to specify query string parameters</span></span>

<span data-ttu-id="f29a2-177">如果要在客户端连接时将数据发送到服务器，则可以将查询字符串参数添加到连接对象。</span><span class="sxs-lookup"><span data-stu-id="f29a2-177">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="f29a2-178">下面的示例演示如何在客户端代码中设置查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="f29a2-178">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="f29a2-179">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="f29a2-179">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="f29a2-180">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-180">How to specify the transport method</span></span>

<span data-ttu-id="f29a2-181">作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="f29a2-181">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="f29a2-182">如果已知道要使用的传输，可以绕过此协商过程。</span><span class="sxs-lookup"><span data-stu-id="f29a2-182">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="f29a2-183">若要指定传输方法，请将传输对象传入到 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-183">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="f29a2-184">下面的示例演示如何在客户端代码中指定传输方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-184">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="f29a2-185">[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空间包含可用于指定传输的以下类。 "的命名空间可用于指定传输。</span><span class="sxs-lookup"><span data-stu-id="f29a2-185">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="f29a2-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="f29a2-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="f29a2-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="f29a2-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="f29a2-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) （仅在服务器和客户端都使用 .net 4.5 时可用。）</span><span class="sxs-lookup"><span data-stu-id="f29a2-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="f29a2-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) （自动选择客户端和服务器支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="f29a2-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="f29a2-190">这是默认传输。</span><span class="sxs-lookup"><span data-stu-id="f29a2-190">This is the default transport.</span></span> <span data-ttu-id="f29a2-191">将此传入到 `Start` 方法与不传入任何内容相同。）</span><span class="sxs-lookup"><span data-stu-id="f29a2-191">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="f29a2-192">此列表中不包含 ForeverFrame 传输，因为它仅由浏览器使用。</span><span class="sxs-lookup"><span data-stu-id="f29a2-192">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="f29a2-193">有关如何在服务器代码中检查传输方法的信息，请参阅[ASP.NET SignalR HUB API 指南-服务器-如何从上下文属性获取有关客户端的信息](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-193">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="f29a2-194">有关传输和回退的详细信息，请参阅[SignalR-传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-194">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="f29a2-195">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="f29a2-195">How to specify HTTP headers</span></span>

<span data-ttu-id="f29a2-196">若要设置 HTTP 标头，请使用连接对象的 `Headers` 属性。</span><span class="sxs-lookup"><span data-stu-id="f29a2-196">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="f29a2-197">下面的示例演示如何添加 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="f29a2-197">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="f29a2-198">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="f29a2-198">How to specify client certificates</span></span>

<span data-ttu-id="f29a2-199">若要添加客户端证书，请对连接对象使用 `AddClientCertificate` 方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-199">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="f29a2-200">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="f29a2-200">How to create the Hub proxy</span></span>

<span data-ttu-id="f29a2-201">若要在客户端上定义集线器可以从服务器调用的方法，并在服务器上调用集线器上的方法，请通过对连接对象调用 `CreateHubProxy` 来为集线器创建代理。</span><span class="sxs-lookup"><span data-stu-id="f29a2-201">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="f29a2-202">传递给 `CreateHubProxy` 的字符串是中心类的名称，或 `HubName` 属性指定的名称（如果服务器上使用了一个名称）。</span><span class="sxs-lookup"><span data-stu-id="f29a2-202">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="f29a2-203">名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="f29a2-203">Name matching is case-insensitive.</span></span>

<span data-ttu-id="f29a2-204">**服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="f29a2-204">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="f29a2-205">**创建中心类的客户端代理**</span><span class="sxs-lookup"><span data-stu-id="f29a2-205">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="f29a2-206">如果使用 `HubName` 特性修饰中心类，请使用该名称。</span><span class="sxs-lookup"><span data-stu-id="f29a2-206">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="f29a2-207">**服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="f29a2-207">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="f29a2-208">**创建中心类的客户端代理**</span><span class="sxs-lookup"><span data-stu-id="f29a2-208">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="f29a2-209">代理对象是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="f29a2-209">The proxy object is thread-safe.</span></span> <span data-ttu-id="f29a2-210">事实上，如果用相同的 `hubName`多次调用 `HubConnection.CreateHubProxy`，则会获得相同的缓存 `IHubProxy` 对象。</span><span class="sxs-lookup"><span data-stu-id="f29a2-210">In fact, if you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="f29a2-211">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-211">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="f29a2-212">若要定义服务器可以调用的方法，请使用代理的 `On` 方法来注册事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="f29a2-212">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="f29a2-213">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="f29a2-213">Method name matching is case-insensitive.</span></span> <span data-ttu-id="f29a2-214">例如，服务器上的 `Clients.All.UpdateStockPrice` 会在客户端上执行 `updateStockPrice`、`updatestockprice`或 `UpdateStockPrice`。</span><span class="sxs-lookup"><span data-stu-id="f29a2-214">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="f29a2-215">不同的客户端平台对于你编写方法代码以更新 UI 的方式有不同的要求。</span><span class="sxs-lookup"><span data-stu-id="f29a2-215">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="f29a2-216">显示的示例适用于 WinRT （Windows 应用商店 .NET）客户端。</span><span class="sxs-lookup"><span data-stu-id="f29a2-216">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="f29a2-217">WPF、Silverlight 和控制台应用程序示例在[本主题后面的单独章节](#wpfsl)中提供。</span><span class="sxs-lookup"><span data-stu-id="f29a2-217">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="f29a2-218">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-218">Methods without parameters</span></span>

<span data-ttu-id="f29a2-219">如果正在处理的方法没有参数，请使用 `On` 方法的非泛型重载：</span><span class="sxs-lookup"><span data-stu-id="f29a2-219">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="f29a2-220">**调用不带参数的客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-220">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="f29a2-221">**从没有参数的服务器中调用的方法的 WinRT 客户端代码（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="f29a2-221">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="f29a2-222">带参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="f29a2-222">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="f29a2-223">如果正在处理的方法具有参数，请将参数的类型指定为 `On` 方法的泛型类型。</span><span class="sxs-lookup"><span data-stu-id="f29a2-223">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="f29a2-224">`On` 方法的泛型重载可用于指定多达8个参数（4在 Windows Phone 7 上）。</span><span class="sxs-lookup"><span data-stu-id="f29a2-224">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="f29a2-225">在下面的示例中，将一个参数发送到 `UpdateStockPrice` 方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-225">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="f29a2-226">**使用参数调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-226">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="f29a2-227">**用于参数的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="f29a2-227">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="f29a2-228">**从具有参数的服务器中调用的方法的 WinRT 客户端代码（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="f29a2-228">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="f29a2-229">带参数的方法，指定参数的动态对象</span><span class="sxs-lookup"><span data-stu-id="f29a2-229">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="f29a2-230">作为将参数指定为 `On` 方法的泛型类型的替代方法，可以将参数指定为动态对象：</span><span class="sxs-lookup"><span data-stu-id="f29a2-230">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="f29a2-231">**使用参数调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-231">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="f29a2-232">**用于参数的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="f29a2-232">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="f29a2-233">**从具有参数的服务器中调用的方法的 WinRT 客户端代码，对参数使用动态对象（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="f29a2-233">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="f29a2-234">如何删除处理程序</span><span class="sxs-lookup"><span data-stu-id="f29a2-234">How to remove a handler</span></span>

<span data-ttu-id="f29a2-235">若要删除处理程序，请调用其 `Dispose` 方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-235">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="f29a2-236">**从服务器调用的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-236">**Client code for a method called from server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="f29a2-237">**用于删除处理程序的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-237">**Client code to remove the handler**</span></span>

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="f29a2-238">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-238">How to call server methods from the client</span></span>

<span data-ttu-id="f29a2-239">若要在服务器上调用方法，请在中心代理上使用 `Invoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-239">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="f29a2-240">如果服务器方法没有返回值，请使用 `Invoke` 方法的非泛型重载。</span><span class="sxs-lookup"><span data-stu-id="f29a2-240">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="f29a2-241">**没有返回值的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-241">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="f29a2-242">**调用没有返回值的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-242">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="f29a2-243">如果服务器方法具有返回值，则将返回类型指定为 `Invoke` 方法的泛型类型。</span><span class="sxs-lookup"><span data-stu-id="f29a2-243">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="f29a2-244">**具有返回值并采用复杂类型参数的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-244">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="f29a2-245">**用于参数和返回值的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="f29a2-245">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="f29a2-246">**在 ASP.NET 4.5 异步方法中调用具有返回值并采用复杂类型参数的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-246">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="f29a2-247">**在同步方法中调用具有返回值并采用复杂类型参数的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-247">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="f29a2-248">`Invoke` 方法异步执行并返回一个 `Task` 对象。</span><span class="sxs-lookup"><span data-stu-id="f29a2-248">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="f29a2-249">如果未指定 `await` 或 `.Wait()`，则在调用的方法完成执行之前，将执行下一行代码。</span><span class="sxs-lookup"><span data-stu-id="f29a2-249">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="f29a2-250">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="f29a2-250">How to handle connection lifetime events</span></span>

<span data-ttu-id="f29a2-251">SignalR 提供以下连接生存期事件，你可以处理这些事件：</span><span class="sxs-lookup"><span data-stu-id="f29a2-251">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="f29a2-252">`Received`：在连接上接收到任何数据时引发。</span><span class="sxs-lookup"><span data-stu-id="f29a2-252">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="f29a2-253">提供接收的数据。</span><span class="sxs-lookup"><span data-stu-id="f29a2-253">Provides the received data.</span></span>
- <span data-ttu-id="f29a2-254">`ConnectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。</span><span class="sxs-lookup"><span data-stu-id="f29a2-254">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="f29a2-255">`Reconnecting`：基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="f29a2-255">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="f29a2-256">`Reconnected`：在基础传输重新连接后引发。</span><span class="sxs-lookup"><span data-stu-id="f29a2-256">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="f29a2-257">`StateChanged`：在连接状态发生更改时引发。</span><span class="sxs-lookup"><span data-stu-id="f29a2-257">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="f29a2-258">提供旧状态和新状态。</span><span class="sxs-lookup"><span data-stu-id="f29a2-258">Provides the old state and the new state.</span></span> <span data-ttu-id="f29a2-259">有关连接状态值的信息，请参阅[ConnectionState 枚举](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-259">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="f29a2-260">`Closed`：连接断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="f29a2-260">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="f29a2-261">例如，如果想要显示不是致命错误的警告消息，但会导致间歇连接问题（如缓慢或频繁断开连接），则应对 `ConnectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="f29a2-261">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="f29a2-262">有关详细信息，请参阅[了解和处理 SignalR 中的连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="f29a2-262">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="f29a2-263">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="f29a2-263">How to handle errors</span></span>

<span data-ttu-id="f29a2-264">如果未在服务器上显式启用详细的错误消息，则在出现错误后 SignalR 返回的异常对象包含有关错误的最小信息。</span><span class="sxs-lookup"><span data-stu-id="f29a2-264">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="f29a2-265">例如，如果对 `newContosoChatMessage` 的调用失败，则出于安全原因，不建议将错误对象中的错误消息包含 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 向生产中的客户端发送详细的错误消息，但如果想要启用详细的错误消息以进行故障排除，请在服务器上使用以下代码。</span><span class="sxs-lookup"><span data-stu-id="f29a2-265">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="f29a2-266">若要处理 SignalR 引发的错误，可以在连接对象上为 `Error` 事件添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="f29a2-266">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="f29a2-267">若要处理方法调用中的错误，请将代码包装在 try-catch 块中。</span><span class="sxs-lookup"><span data-stu-id="f29a2-267">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="f29a2-268">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="f29a2-268">How to enable client-side logging</span></span>

<span data-ttu-id="f29a2-269">若要启用客户端日志记录，请设置连接对象的 "`TraceLevel`" 和 "`TraceWriter`" 属性。</span><span class="sxs-lookup"><span data-stu-id="f29a2-269">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="f29a2-270">服务器可以调用的客户端方法的 WPF、Silverlight 和控制台应用程序代码示例</span><span class="sxs-lookup"><span data-stu-id="f29a2-270">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="f29a2-271">前面所示的代码示例用于定义服务器可以调用的客户端方法。</span><span class="sxs-lookup"><span data-stu-id="f29a2-271">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="f29a2-272">以下示例显示了适用于 WPF、Silverlight 和控制台应用程序客户端的等效代码。</span><span class="sxs-lookup"><span data-stu-id="f29a2-272">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="f29a2-273">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="f29a2-273">Methods without parameters</span></span>

<span data-ttu-id="f29a2-274">**从没有参数的服务器中调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-274">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="f29a2-275">**从没有参数的服务器中调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-275">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="f29a2-276">**不带参数的服务器中调用的方法的控制台应用程序客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-276">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="f29a2-277">带参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="f29a2-277">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="f29a2-278">**从具有参数的服务器中调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-278">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="f29a2-279">**从具有参数的服务器中调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-279">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="f29a2-280">**从具有参数的服务器中调用的方法的控制台应用程序客户端代码**</span><span class="sxs-lookup"><span data-stu-id="f29a2-280">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="f29a2-281">带参数的方法，指定参数的动态对象</span><span class="sxs-lookup"><span data-stu-id="f29a2-281">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="f29a2-282">**从具有参数的服务器中调用的方法的 WPF 客户端代码，对参数使用动态对象**</span><span class="sxs-lookup"><span data-stu-id="f29a2-282">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="f29a2-283">**从具有参数的服务器中调用的方法的 Silverlight 客户端代码，对参数使用动态对象**</span><span class="sxs-lookup"><span data-stu-id="f29a2-283">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="f29a2-284">**从具有参数的服务器中调用的方法的控制台应用程序客户端代码，对参数使用动态对象**</span><span class="sxs-lookup"><span data-stu-id="f29a2-284">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
