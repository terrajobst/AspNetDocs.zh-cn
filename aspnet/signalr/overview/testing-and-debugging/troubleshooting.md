---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR 故障排除 |Microsoft Docs
author: bradygaster
description: 本文介绍了开发 SignalR 应用程序时的常见问题。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: bcd273d839aed64ad2712eb503dd1942a2d4e355
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467432"
---
# <a name="signalr-troubleshooting"></a><span data-ttu-id="4caad-103">SignalR 疑难解答</span><span class="sxs-lookup"><span data-stu-id="4caad-103">SignalR Troubleshooting</span></span>

<span data-ttu-id="4caad-104">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="4caad-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4caad-105">本文档介绍了 SignalR 的常见疑难解答问题。</span><span class="sxs-lookup"><span data-stu-id="4caad-105">This document describes common troubleshooting issues with SignalR.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="4caad-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="4caad-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="4caad-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4caad-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="4caad-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="4caad-108">.NET 4.5</span></span>
> - <span data-ttu-id="4caad-109">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="4caad-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="4caad-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="4caad-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="4caad-111">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4caad-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="4caad-112">问题和注释</span><span class="sxs-lookup"><span data-stu-id="4caad-112">Questions and comments</span></span>
>
> <span data-ttu-id="4caad-113">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="4caad-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="4caad-114">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="4caad-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="4caad-115">本文档包含以下各节。</span><span class="sxs-lookup"><span data-stu-id="4caad-115">This document contains the following sections.</span></span>

- [<span data-ttu-id="4caad-116">以静默方式在客户端和服务器之间调用方法失败</span><span class="sxs-lookup"><span data-stu-id="4caad-116">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="4caad-117">配置 IIS websocket，使其能够检测到死客户端</span><span class="sxs-lookup"><span data-stu-id="4caad-117">Configuring IIS websockets to ping/pong to detect a dead client</span></span>](#pong)
- [<span data-ttu-id="4caad-118">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="4caad-118">Other connection issues</span></span>](#other)
- [<span data-ttu-id="4caad-119">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="4caad-119">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="4caad-120">Visual Studio 问题</span><span class="sxs-lookup"><span data-stu-id="4caad-120">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="4caad-121">Internet Information Services 问题</span><span class="sxs-lookup"><span data-stu-id="4caad-121">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="4caad-122">Microsoft Azure 问题</span><span class="sxs-lookup"><span data-stu-id="4caad-122">Microsoft Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="4caad-123">以静默方式在客户端和服务器之间调用方法失败</span><span class="sxs-lookup"><span data-stu-id="4caad-123">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="4caad-124">本部分介绍在客户端和服务器之间的方法调用失败的可能原因，而没有有意义的错误消息。</span><span class="sxs-lookup"><span data-stu-id="4caad-124">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="4caad-125">在 SignalR 应用程序中，服务器没有有关客户端实现的方法的信息;当服务器调用客户端方法时，方法名称和参数数据将发送到客户端，并且仅当该方法以服务器指定的格式存在时，才会执行此方法。</span><span class="sxs-lookup"><span data-stu-id="4caad-125">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="4caad-126">如果在客户端上找不到匹配的方法，则不会执行任何操作，并且不会在服务器上引发任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="4caad-126">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="4caad-127">若要进一步调查未调用的客户端方法，你可以在调用 start 方法之前打开中心日志记录，以查看来自服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="4caad-127">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="4caad-128">若要在 JavaScript 应用程序中启用日志记录，请参阅[如何启用客户端日志记录（JavaScript 客户端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="4caad-128">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="4caad-129">若要在 .NET 客户端应用程序中启用日志记录，请参阅[如何启用客户端日志记录（.Net 客户端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="4caad-129">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="4caad-130">拼写错误的方法、错误的方法签名或不正确的中心名称</span><span class="sxs-lookup"><span data-stu-id="4caad-130">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="4caad-131">如果被调用方法的名称或签名与客户端上的适当方法不完全匹配，则调用将失败。</span><span class="sxs-lookup"><span data-stu-id="4caad-131">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="4caad-132">验证服务器调用的方法名称是否与客户端上的方法的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="4caad-132">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="4caad-133">此外，SignalR 使用 camel 大小写方法创建中心代理，这在 JavaScript 中是合适的方法，因此，在服务器上调用 `SendMessage` 的方法将在客户端代理 `sendMessage` 中调用。</span><span class="sxs-lookup"><span data-stu-id="4caad-133">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="4caad-134">如果使用服务器端代码中的 `HubName` 属性，请验证所使用的名称是否与用于在客户端上创建集线器的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="4caad-134">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="4caad-135">如果不使用 `HubName` 属性，请验证 JavaScript 客户端中的中心名称是否采用 camel 大小写格式（如 chatHub 而不是 ChatHub）。</span><span class="sxs-lookup"><span data-stu-id="4caad-135">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="4caad-136">客户端上的重复方法名称</span><span class="sxs-lookup"><span data-stu-id="4caad-136">Duplicate method name on client</span></span>

<span data-ttu-id="4caad-137">验证在客户端上没有仅大小写不同的重复方法。</span><span class="sxs-lookup"><span data-stu-id="4caad-137">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="4caad-138">如果客户端应用程序有一个名为 `sendMessage`的方法，请验证是否也没有名为 `SendMessage` 的方法。</span><span class="sxs-lookup"><span data-stu-id="4caad-138">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="4caad-139">客户端上缺少 JSON 分析器</span><span class="sxs-lookup"><span data-stu-id="4caad-139">Missing JSON parser on the client</span></span>

<span data-ttu-id="4caad-140">SignalR 要求提供 JSON 分析器以序列化服务器和客户端之间的调用。</span><span class="sxs-lookup"><span data-stu-id="4caad-140">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="4caad-141">如果客户端没有内置的 JSON 分析器（如 Internet Explorer 7），则需要在应用程序中包含一个。</span><span class="sxs-lookup"><span data-stu-id="4caad-141">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="4caad-142">可在[此处](http://nuget.org/packages/json2)下载 JSON 分析器。</span><span class="sxs-lookup"><span data-stu-id="4caad-142">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="4caad-143">混合中心和 PersistentConnection 语法</span><span class="sxs-lookup"><span data-stu-id="4caad-143">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="4caad-144">SignalR 使用两种通信模型：集线器和 PersistentConnections。</span><span class="sxs-lookup"><span data-stu-id="4caad-144">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="4caad-145">在客户端代码中，调用这两个通信模型的语法不同。</span><span class="sxs-lookup"><span data-stu-id="4caad-145">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="4caad-146">如果已在服务器代码中添加集线器，请验证所有客户端代码是否均使用正确的中心语法。</span><span class="sxs-lookup"><span data-stu-id="4caad-146">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="4caad-147">**在 JavaScript 客户端中创建 PersistentConnection 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-147">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="4caad-148">**在 Javascript 客户端中创建集线器代理的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-148">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="4caad-149">**C#将路由映射到 PersistentConnection 的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-149">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="4caad-150">**C#如果有多个应用程序，则将路由映射到中心或多个集线器的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-150">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="4caad-151">在添加订阅之前已启动连接</span><span class="sxs-lookup"><span data-stu-id="4caad-151">Connection started before subscriptions are added</span></span>

<span data-ttu-id="4caad-152">如果在将可从服务器调用的方法添加到代理之前启动了中心的连接，则不会收到消息。</span><span class="sxs-lookup"><span data-stu-id="4caad-152">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="4caad-153">以下 JavaScript 代码将不会正确启动集线器：</span><span class="sxs-lookup"><span data-stu-id="4caad-153">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="4caad-154">**不允许接收集线器消息的不正确的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-154">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="4caad-155">请改为在调用 Start 之前添加方法订阅：</span><span class="sxs-lookup"><span data-stu-id="4caad-155">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="4caad-156">**正确向中心添加订阅的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-156">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="4caad-157">中心代理上缺少方法名称</span><span class="sxs-lookup"><span data-stu-id="4caad-157">Missing method name on the hub proxy</span></span>

<span data-ttu-id="4caad-158">验证在服务器上定义的方法是否已在客户端上订阅。</span><span class="sxs-lookup"><span data-stu-id="4caad-158">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="4caad-159">即使服务器定义了方法，仍必须将它添加到客户端代理。</span><span class="sxs-lookup"><span data-stu-id="4caad-159">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="4caad-160">可以通过以下方式将方法添加到客户端代理（请注意，方法已添加到中心的 `client` 成员，而不是直接添加到中心）：</span><span class="sxs-lookup"><span data-stu-id="4caad-160">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="4caad-161">**向中心代理添加方法的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-161">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="4caad-162">未声明为公共的集线器或集线器方法</span><span class="sxs-lookup"><span data-stu-id="4caad-162">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="4caad-163">若要在客户端上可见，中心实现和方法必须声明为 `public`。</span><span class="sxs-lookup"><span data-stu-id="4caad-163">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="4caad-164">从不同的应用程序访问集线器</span><span class="sxs-lookup"><span data-stu-id="4caad-164">Accessing hub from a different application</span></span>

<span data-ttu-id="4caad-165">SignalR 中心只能通过实现 SignalR 客户端的应用程序进行访问。</span><span class="sxs-lookup"><span data-stu-id="4caad-165">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="4caad-166">SignalR 无法与其他通信库（如 SOAP 或 WCF web 服务）进行互操作。如果没有可用于目标平台的 SignalR 客户端，则无法直接访问服务器的终结点。</span><span class="sxs-lookup"><span data-stu-id="4caad-166">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="4caad-167">手动序列化数据</span><span class="sxs-lookup"><span data-stu-id="4caad-167">Manually serializing data</span></span>

<span data-ttu-id="4caad-168">SignalR 将自动使用 JSON 序列化方法参数，无需自行执行此操作。</span><span class="sxs-lookup"><span data-stu-id="4caad-168">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="4caad-169">远程集线器方法未在 OnDisconnected 函数中的客户端上执行</span><span class="sxs-lookup"><span data-stu-id="4caad-169">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="4caad-170">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-170">This behavior is by design.</span></span> <span data-ttu-id="4caad-171">调用 `OnDisconnected` 时，中心已进入 `Disconnected` 状态，该状态不允许调用其他集线器方法。</span><span class="sxs-lookup"><span data-stu-id="4caad-171">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="4caad-172">**C#在 OnDisconnected 事件中正确执行代码的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-172">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a><span data-ttu-id="4caad-173">OnDisconnect 未在一致时间触发</span><span class="sxs-lookup"><span data-stu-id="4caad-173">OnDisconnect not firing at consistent times</span></span>

<span data-ttu-id="4caad-174">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-174">This behavior is by design.</span></span> <span data-ttu-id="4caad-175">当用户尝试使用活动的 SignalR 连接离开页面时，SignalR 客户端会尽力尝试通知服务器客户端连接将停止的情况。</span><span class="sxs-lookup"><span data-stu-id="4caad-175">When a user attempts to navigate away from a page with an active SignalR connection, the SignalR client will then make a best-effort attempt to notify the server that the client connection will be stopped.</span></span> <span data-ttu-id="4caad-176">如果 SignalR 客户端的最大努力尝试无法访问服务器，则服务器将在稍后可配置的 `DisconnectTimeout` 之后释放连接，此时将触发 `OnDisconnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="4caad-176">If the SignalR client's best-effort attempt fails to reach the server, the server will dispose of the connection after a configurable `DisconnectTimeout` later, at which time the `OnDisconnected` event will fire.</span></span> <span data-ttu-id="4caad-177">如果 SignalR 客户端的尽力尝试成功，则 `OnDisconnected` 事件会立即触发。</span><span class="sxs-lookup"><span data-stu-id="4caad-177">If the SignalR client's best-effort attempt is successful, the `OnDisconnected` event will fire immediately.</span></span>

<span data-ttu-id="4caad-178">有关设置 `DisconnectTimeout` 设置的信息，请参阅[处理连接生存期事件： DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)。</span><span class="sxs-lookup"><span data-stu-id="4caad-178">For information on setting the `DisconnectTimeout` setting, see [Handling connection lifetime events: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).</span></span>

### <a name="connection-limit-reached"></a><span data-ttu-id="4caad-179">已达到连接限制</span><span class="sxs-lookup"><span data-stu-id="4caad-179">Connection limit reached</span></span>

<span data-ttu-id="4caad-180">在客户端操作系统（如 Windows 7）上使用完整的 IIS 版本时，会施加10个连接限制。</span><span class="sxs-lookup"><span data-stu-id="4caad-180">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="4caad-181">使用客户端操作系统时，请改用 IIS Express 来避免此限制。</span><span class="sxs-lookup"><span data-stu-id="4caad-181">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="4caad-182">未正确设置跨域连接</span><span class="sxs-lookup"><span data-stu-id="4caad-182">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="4caad-183">如果跨域连接（SignalR URL 与宿主页面不在同一个域中的连接）未正确设置，则连接可能会失败，且不会出现错误消息。</span><span class="sxs-lookup"><span data-stu-id="4caad-183">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="4caad-184">有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="4caad-184">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="4caad-185">使用 NTLM （Active Directory）的连接在 .NET 客户端中不起作用</span><span class="sxs-lookup"><span data-stu-id="4caad-185">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="4caad-186">如果连接配置不正确，则使用域安全性的 .NET 客户端应用程序中的连接可能会失败。</span><span class="sxs-lookup"><span data-stu-id="4caad-186">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="4caad-187">若要在域环境中使用 SignalR，请设置所需的连接属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4caad-187">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="4caad-188">**C#实现连接凭据的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-188">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a><span data-ttu-id="4caad-189">配置 IIS websocket，使其能够检测到死客户端</span><span class="sxs-lookup"><span data-stu-id="4caad-189">Configuring IIS websockets to ping/pong to detect a dead client</span></span>

<span data-ttu-id="4caad-190">SignalR 服务器不知道客户端是否已死，它们依赖于连接失败（即，`OnClose` 回调）底层 websocket 发出的通知。</span><span class="sxs-lookup"><span data-stu-id="4caad-190">SignalR servers don't know if the client is dead or not and they rely on notification from the underlying websocket for connection failures, that is, the `OnClose` callback.</span></span> <span data-ttu-id="4caad-191">此问题的一种解决方法是配置 IIS websocket，为你配置 ping/乒乓球。</span><span class="sxs-lookup"><span data-stu-id="4caad-191">One solution to this problem is to configure IIS websockets to do the ping/pong for you.</span></span> <span data-ttu-id="4caad-192">这可确保当连接意外中断时，连接将关闭。</span><span class="sxs-lookup"><span data-stu-id="4caad-192">This ensures that your connection will close if it breaks unexpectedly.</span></span> <span data-ttu-id="4caad-193">有关详细信息，请参阅[此 stackoverflow 文章](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)。</span><span class="sxs-lookup"><span data-stu-id="4caad-193">For more information see [this stackoverflow post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).</span></span>

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="4caad-194">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="4caad-194">Other connection issues</span></span>

<span data-ttu-id="4caad-195">本部分介绍连接过程中出现的特定症状或错误消息的原因和解决方法。</span><span class="sxs-lookup"><span data-stu-id="4caad-195">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="4caad-196">"必须在可以发送数据之前调用启动" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-196">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="4caad-197">如果在启动连接之前代码引用 SignalR 对象，则通常会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-197">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="4caad-198">处理程序的绑定和将调用在服务器上定义的方法的类似方法必须在连接完成后添加。</span><span class="sxs-lookup"><span data-stu-id="4caad-198">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="4caad-199">请注意，对 `Start` 的调用是异步的，因此调用后的代码可以在完成之前执行。</span><span class="sxs-lookup"><span data-stu-id="4caad-199">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="4caad-200">在连接完全启动后添加处理程序的最佳方式是将其放入一个回调函数，该函数作为参数传递给 start 方法：</span><span class="sxs-lookup"><span data-stu-id="4caad-200">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="4caad-201">**正确添加引用 SignalR 对象的事件处理程序的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-201">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="4caad-202">如果仍在引用 SignalR 对象，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-202">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="4caad-203">"301 永久移动" 或 "302 移动" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-203">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="4caad-204">如果项目包含一个名为 SignalR 的文件夹，该文件夹将干扰自动创建的代理，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-204">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="4caad-205">若要避免此错误，请不要在应用程序中使用称为 `SignalR` 的文件夹，或关闭自动代理生成。</span><span class="sxs-lookup"><span data-stu-id="4caad-205">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="4caad-206">有关更多详细信息，请参阅[生成的代理以及它所执行的](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)操作。</span><span class="sxs-lookup"><span data-stu-id="4caad-206">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="4caad-207">.NET 或 Silverlight 客户端中的 "403 禁止访问" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-207">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="4caad-208">此错误可能出现在未正确启用跨域通信的跨域环境中。</span><span class="sxs-lookup"><span data-stu-id="4caad-208">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="4caad-209">有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="4caad-209">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="4caad-210">若要在 Silverlight 客户端中建立跨域连接，请参阅[从 silverlight 客户端进行跨域连接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。</span><span class="sxs-lookup"><span data-stu-id="4caad-210">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="4caad-211">"找不到 404" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-211">"404 Not Found" error</span></span>

<span data-ttu-id="4caad-212">此问题有几个原因。</span><span class="sxs-lookup"><span data-stu-id="4caad-212">There are several causes for this issue.</span></span> <span data-ttu-id="4caad-213">验证以下所有内容：</span><span class="sxs-lookup"><span data-stu-id="4caad-213">Verify all of the following:</span></span>

- <span data-ttu-id="4caad-214">**集线器代理地址引用的格式不正确：** 如果对生成的中心代理地址的引用的格式不正确，则通常会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-214">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="4caad-215">验证对中心地址的引用是否正确。</span><span class="sxs-lookup"><span data-stu-id="4caad-215">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="4caad-216">有关详细信息，请参阅[如何引用动态生成的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。</span><span class="sxs-lookup"><span data-stu-id="4caad-216">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="4caad-217">添加**中心路由之前，向应用程序添加路由：** 如果你的应用程序使用其他路由，请验证添加的第一个路由是对 `MapSignalR`的调用。</span><span class="sxs-lookup"><span data-stu-id="4caad-217">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapSignalR`.</span></span>
- <span data-ttu-id="4caad-218">**在不更新无扩展名 url 的情况下使用 IIS 7 或7.5：** 使用 IIS 7 或7.5 需要更新无扩展名 Url，以便服务器可在 `/signalr/hubs`提供对集线器定义的访问权限。</span><span class="sxs-lookup"><span data-stu-id="4caad-218">**Using IIS 7 or 7.5 without the update for extensionless URLs:** Using IIS 7 or 7.5 requires an update for extensionless URLs so that the server can provide access to the hub definitions at `/signalr/hubs`.</span></span> <span data-ttu-id="4caad-219">可在[此处](https://support.microsoft.com/kb/980368)找到该更新。</span><span class="sxs-lookup"><span data-stu-id="4caad-219">The update can be found [here](https://support.microsoft.com/kb/980368).</span></span>
- <span data-ttu-id="4caad-220">**IIS 缓存过期或已损坏：** 若要验证缓存内容是否未过期，请在 PowerShell 窗口中输入以下命令以清除缓存：</span><span class="sxs-lookup"><span data-stu-id="4caad-220">**IIS cache out of date or corrupt:** To verify that the cache contents are not out of date, enter the following command in a PowerShell window to clear the cache:</span></span>

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a><span data-ttu-id="4caad-221">"500 内部服务器错误"</span><span class="sxs-lookup"><span data-stu-id="4caad-221">"500 Internal Server Error"</span></span>

<span data-ttu-id="4caad-222">这是一种非常通用的错误，可能会产生多种原因。</span><span class="sxs-lookup"><span data-stu-id="4caad-222">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="4caad-223">错误的详细信息应该出现在服务器的事件日志中，也可以通过调试服务器找到。</span><span class="sxs-lookup"><span data-stu-id="4caad-223">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="4caad-224">可以通过打开服务器上的详细错误来获取更详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="4caad-224">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="4caad-225">有关详细信息，请参阅[如何处理中心类中的错误](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="4caad-225">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

<span data-ttu-id="4caad-226">如果未正确配置防火墙或代理，导致重写请求标头，则通常会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-226">This error is also commonly seen if a firewall or proxy is not configured properly, causing the request headers to be rewritten.</span></span> <span data-ttu-id="4caad-227">解决方法是确保在防火墙或代理上启用了端口80。</span><span class="sxs-lookup"><span data-stu-id="4caad-227">The solution is to make sure that port 80 is enabled on the firewall or proxy.</span></span>

### <a name="unexpected-response-code-500"></a><span data-ttu-id="4caad-228">"意外的响应代码： 500"</span><span class="sxs-lookup"><span data-stu-id="4caad-228">"Unexpected response code: 500"</span></span>

<span data-ttu-id="4caad-229">如果应用程序中使用的 .NET framework 版本与 web.config 中指定的版本不匹配，则可能出现此错误。解决方法是验证应用程序设置和 web.config 文件中是否使用了 .NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="4caad-229">This error may occur if the version of .NET framework used in the application does not match the version specified in Web.Config. The solution is to verify that .NET 4.5 is used in both the application settings and the Web.Config file.</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="4caad-230">"TypeError： &lt;hubType&gt; 未定义" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-230">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="4caad-231">如果未正确调用 `MapSignalR`，则会导致此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-231">This error will result if the call to `MapSignalR` is not made properly.</span></span> <span data-ttu-id="4caad-232">有关详细信息，请参阅[如何注册 SignalR 中间件和配置 SignalR 选项](../guide-to-the-api/hubs-api-guide-server.md#route)。</span><span class="sxs-lookup"><span data-stu-id="4caad-232">See [How to register SignalR Middleware and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="4caad-233">用户代码未处理 JsonSerializationException</span><span class="sxs-lookup"><span data-stu-id="4caad-233">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="4caad-234">验证发送给方法的参数不包括非序列化类型（如文件句柄或数据库连接）。</span><span class="sxs-lookup"><span data-stu-id="4caad-234">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="4caad-235">如果需要在不想发送到客户端的服务器端对象上使用成员（出于安全原因或序列化的原因），请使用 `JSONIgnore` 特性。</span><span class="sxs-lookup"><span data-stu-id="4caad-235">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="4caad-236">"协议错误：未知传输" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-236">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="4caad-237">如果客户端不支持 SignalR 使用的传输，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-237">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="4caad-238">有关可与 SignalR 一起使用的浏览器的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="4caad-238">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="4caad-239">"JavaScript Hub 代理生成已禁用。"</span><span class="sxs-lookup"><span data-stu-id="4caad-239">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="4caad-240">如果设置 `DisableJavaScriptProxies`，同时在 `signalr/hubs`同时包含对动态生成的代理的引用，则会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-240">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="4caad-241">有关手动创建代理的详细信息，请参阅[生成的代理及其功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="4caad-241">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="4caad-242">"连接 ID 的格式不正确，或者" 用户标识在 active SignalR 连接期间无法更改 "错误</span><span class="sxs-lookup"><span data-stu-id="4caad-242">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="4caad-243">如果正在使用身份验证，并且在停止连接之前注销了客户端，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-243">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="4caad-244">解决方法是在注销客户端之前停止 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="4caad-244">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="4caad-245">"未捕获的错误： SignalR： jQuery 找不到。</span><span class="sxs-lookup"><span data-stu-id="4caad-245">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="4caad-246">请确保引用 jQuery，然后再引用 SignalR 文件 "错误</span><span class="sxs-lookup"><span data-stu-id="4caad-246">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="4caad-247">SignalR JavaScript 客户端需要 jQuery 才能运行。</span><span class="sxs-lookup"><span data-stu-id="4caad-247">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="4caad-248">验证对 jQuery 的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否在对 SignalR 的引用之前。</span><span class="sxs-lookup"><span data-stu-id="4caad-248">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="4caad-249">"未捕获 TypeError：无法读取属性"&lt;属性&gt;"未定义" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-249">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="4caad-250">此错误是由于未正确引用 jQuery 或中心代理而导致的。</span><span class="sxs-lookup"><span data-stu-id="4caad-250">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="4caad-251">验证对 jQuery 和中心代理的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否在对集线器代理的引用之前。</span><span class="sxs-lookup"><span data-stu-id="4caad-251">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="4caad-252">对集线器代理的默认引用如下所示：</span><span class="sxs-lookup"><span data-stu-id="4caad-252">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="4caad-253">**正确引用中心代理的 HTML 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="4caad-253">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="4caad-254">"RuntimeBinderException 已被用户代码处理" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-254">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="4caad-255">如果使用 `Hub.On` 的错误重载，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-255">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="4caad-256">如果该方法具有返回值，则返回类型必须指定为泛型类型参数：</span><span class="sxs-lookup"><span data-stu-id="4caad-256">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="4caad-257">**在客户端上定义的方法（不生成代理）**</span><span class="sxs-lookup"><span data-stu-id="4caad-257">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="4caad-258">连接 ID 不一致或页面加载之间的连接中断</span><span class="sxs-lookup"><span data-stu-id="4caad-258">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="4caad-259">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-259">This behavior is by design.</span></span> <span data-ttu-id="4caad-260">由于中心对象承载于 page 对象中，因此在页面刷新时，中心将被销毁。</span><span class="sxs-lookup"><span data-stu-id="4caad-260">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="4caad-261">多页应用程序需要维护用户和连接 Id 之间的关联，以便它们在页面加载之间保持一致。</span><span class="sxs-lookup"><span data-stu-id="4caad-261">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="4caad-262">连接 Id 可以存储在服务器上的 `ConcurrentDictionary` 对象或数据库中。</span><span class="sxs-lookup"><span data-stu-id="4caad-262">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="4caad-263">"值不能为 null" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-263">"Value cannot be null" error</span></span>

<span data-ttu-id="4caad-264">当前不支持带有可选参数的服务器端方法;如果省略可选参数，则该方法将失败。</span><span class="sxs-lookup"><span data-stu-id="4caad-264">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="4caad-265">有关详细信息，请参阅[可选参数](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="4caad-265">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="4caad-266">"Firefox 无法与服务器建立连接，因为在 Firebug 中 &lt;地址&gt;" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-266">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="4caad-267">如果 WebSocket 传输的协商失败并且改为使用另一个传输，则会在 Firebug 中出现此错误消息。</span><span class="sxs-lookup"><span data-stu-id="4caad-267">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="4caad-268">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-268">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="4caad-269">.NET 客户端应用程序中的 "远程证书根据验证过程无效" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-269">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="4caad-270">如果服务器需要自定义客户端证书，则可以在发出请求之前将 x509certificate 添加到连接。</span><span class="sxs-lookup"><span data-stu-id="4caad-270">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="4caad-271">使用 `Connection.AddClientCertificate`将证书添加到连接。</span><span class="sxs-lookup"><span data-stu-id="4caad-271">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="4caad-272">身份验证超时后断开连接</span><span class="sxs-lookup"><span data-stu-id="4caad-272">Connection drops after authentication times out</span></span>

<span data-ttu-id="4caad-273">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-273">This behavior is by design.</span></span> <span data-ttu-id="4caad-274">连接处于活动状态时，无法修改身份验证凭据;若要刷新凭据，必须停止并重新启动该连接。</span><span class="sxs-lookup"><span data-stu-id="4caad-274">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="4caad-275">使用 jQuery Mobile 时，OnConnected 调用了两次</span><span class="sxs-lookup"><span data-stu-id="4caad-275">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="4caad-276">jQuery Mobile 的 `initializePage` 函数强制重新执行每个页面中的脚本，从而创建另一个连接。</span><span class="sxs-lookup"><span data-stu-id="4caad-276">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="4caad-277">此问题的解决方案包括：</span><span class="sxs-lookup"><span data-stu-id="4caad-277">Solutions for this issue include:</span></span>

- <span data-ttu-id="4caad-278">在 JavaScript 文件之前包括对 jQuery Mobile 的引用。</span><span class="sxs-lookup"><span data-stu-id="4caad-278">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="4caad-279">通过设置 `$.mobile.autoInitializePage = false`禁用 `initializePage` 函数。</span><span class="sxs-lookup"><span data-stu-id="4caad-279">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="4caad-280">等待页面完成初始化，然后再开始连接。</span><span class="sxs-lookup"><span data-stu-id="4caad-280">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="4caad-281">使用服务器发送事件的 Silverlight 应用程序中的消息延迟</span><span class="sxs-lookup"><span data-stu-id="4caad-281">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="4caad-282">在 Silverlight 上使用服务器发送的事件时，消息会被延迟。</span><span class="sxs-lookup"><span data-stu-id="4caad-282">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="4caad-283">若要改为强制使用长轮询，请在启动连接时使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="4caad-283">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="4caad-284">使用永久帧协议的 "权限被拒绝"</span><span class="sxs-lookup"><span data-stu-id="4caad-284">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="4caad-285">这是一个已知问题，请[参阅此](https://github.com/SignalR/SignalR/issues/1963)文。</span><span class="sxs-lookup"><span data-stu-id="4caad-285">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="4caad-286">使用最新 JQuery library 时可能会出现此症状;解决方法是将应用程序降级到 JQuery 1.8.2。</span><span class="sxs-lookup"><span data-stu-id="4caad-286">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a><span data-ttu-id="4caad-287">"InvalidOperationException：不是有效的 web 套接字请求。</span><span class="sxs-lookup"><span data-stu-id="4caad-287">"InvalidOperationException: Not a valid web socket request.</span></span>

<span data-ttu-id="4caad-288">如果使用 WebSocket 协议，但网络代理正在修改请求标头，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-288">This error may occur if the WebSocket protocol is used, but the network proxy is modifying the request headers.</span></span> <span data-ttu-id="4caad-289">解决方法是将代理配置为允许端口80上的 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="4caad-289">The solution is to configure the proxy to allow WebSocket on port 80.</span></span>

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a><span data-ttu-id="4caad-290">"异常：当客户端调用服务器上的方法时，无法解析 &lt;方法名&gt; 方法</span><span class="sxs-lookup"><span data-stu-id="4caad-290">"Exception: &lt;method name&gt; method could not be resolved" when client calls method on server</span></span>

<span data-ttu-id="4caad-291">如果使用了无法在 JSON 有效负载中发现的数据类型（如数组），则可能导致此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-291">This error can result from using data types that cannot be discovered in a JSON payload, such as Array.</span></span> <span data-ttu-id="4caad-292">解决方法是使用 JSON 可发现的数据类型，如 IList。</span><span class="sxs-lookup"><span data-stu-id="4caad-292">The workaround is to use a data type that is discoverable by JSON, such as IList.</span></span> <span data-ttu-id="4caad-293">有关详细信息，请参阅[.Net 客户端无法通过数组参数调用中心方法](https://github.com/SignalR/SignalR/issues/2672)。</span><span class="sxs-lookup"><span data-stu-id="4caad-293">For more information, see [.NET Client unable to call hub methods with array parameters](https://github.com/SignalR/SignalR/issues/2672).</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="4caad-294">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="4caad-294">Compilation and server-side errors</span></span>

 <span data-ttu-id="4caad-295">以下部分包含编译器和服务器端运行时错误的可能解决方案。</span><span class="sxs-lookup"><span data-stu-id="4caad-295">The following section contains possible solutions to compiler and server-side runtime errors.</span></span>

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="4caad-296">对中心实例的引用为 null</span><span class="sxs-lookup"><span data-stu-id="4caad-296">Reference to Hub instance is null</span></span>

<span data-ttu-id="4caad-297">由于已为每个连接创建集线器实例，因此无法在代码中自行创建集线器的实例。</span><span class="sxs-lookup"><span data-stu-id="4caad-297">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="4caad-298">若要从中心自身外部调用集线器上的方法，请参阅[如何从中心类的外部调用客户端方法和管理组](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，了解如何获取对中心上下文的引用。</span><span class="sxs-lookup"><span data-stu-id="4caad-298">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="4caad-299">Httpcontext.current 为 null</span><span class="sxs-lookup"><span data-stu-id="4caad-299">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="4caad-300">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-300">This behavior is by design.</span></span> <span data-ttu-id="4caad-301">SignalR 不支持 ASP.NET 会话状态，因为启用会话状态将中断双工消息。</span><span class="sxs-lookup"><span data-stu-id="4caad-301">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="4caad-302">没有合适的替代方法</span><span class="sxs-lookup"><span data-stu-id="4caad-302">No suitable method to override</span></span>

<span data-ttu-id="4caad-303">如果使用的是较旧文档或博客中的代码，则可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-303">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="4caad-304">验证你未引用已更改或已弃用的方法的名称（如 `OnConnectedAsync`）。</span><span class="sxs-lookup"><span data-stu-id="4caad-304">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="4caad-305">HostContextExtensions. WebSocketServerUrl 为 null</span><span class="sxs-lookup"><span data-stu-id="4caad-305">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="4caad-306">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-306">This behavior is by design.</span></span> <span data-ttu-id="4caad-307">此成员已弃用，不应使用。</span><span class="sxs-lookup"><span data-stu-id="4caad-307">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="4caad-308">"名为 ' signalr ' 的路由已在路由集合中" 错误</span><span class="sxs-lookup"><span data-stu-id="4caad-308">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="4caad-309">如果应用程序调用了两次 `MapSignalR`，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="4caad-309">This error will be seen if `MapSignalR` is called twice by your application.</span></span> <span data-ttu-id="4caad-310">一些示例应用程序直接在 Startup 类中调用 `MapSignalR`;其他人在包装类中进行调用。</span><span class="sxs-lookup"><span data-stu-id="4caad-310">Some example applications call `MapSignalR` directly in the Startup class; others make the call in a wrapper class.</span></span> <span data-ttu-id="4caad-311">确保应用程序不会同时执行这两项操作。</span><span class="sxs-lookup"><span data-stu-id="4caad-311">Ensure that your application does not do both.</span></span>

### <a name="websocket-is-not-used"></a><span data-ttu-id="4caad-312">不使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="4caad-312">WebSocket is not used</span></span>

<span data-ttu-id="4caad-313">如果已验证服务器和客户端是否满足 WebSocket 的要求（在[支持的平台](../getting-started/supported-platforms.md)文档中列出），则需要在服务器上启用 websocket。</span><span class="sxs-lookup"><span data-stu-id="4caad-313">If you have verified that your server and clients meet the requirements for WebSocket (listed in the [Supported Platforms](../getting-started/supported-platforms.md) document), you will need to enable WebSocket on your server.</span></span> <span data-ttu-id="4caad-314">可在[此处](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)找到有关如何执行此操作的说明。</span><span class="sxs-lookup"><span data-stu-id="4caad-314">Instructions for doing this can be found [here](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

### <a name="connection-is-undefined"></a><span data-ttu-id="4caad-315">$. 连接未定义</span><span class="sxs-lookup"><span data-stu-id="4caad-315">$.connection is undefined</span></span>

<span data-ttu-id="4caad-316">此错误表示未正确加载页面上的脚本，或者无法访问或不正确地访问集线器代理。</span><span class="sxs-lookup"><span data-stu-id="4caad-316">This error indicates that either the scripts on a page are not being loaded properly, or the hub proxy is not reachable or is being accessed incorrectly.</span></span> <span data-ttu-id="4caad-317">验证页面上的脚本引用是否对应于项目中加载的脚本，以及在服务器运行时可在浏览器中访问/signalr/hubs。</span><span class="sxs-lookup"><span data-stu-id="4caad-317">Verify that the script references on your page correspond to the scripts loaded in your project, and that /signalr/hubs can be accessed in a browser when the server is running.</span></span>

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a><span data-ttu-id="4caad-318">找不到编译动态表达式所需的一个或多个类型</span><span class="sxs-lookup"><span data-stu-id="4caad-318">One or more types required to compile a dynamic expression cannot be found</span></span>

<span data-ttu-id="4caad-319">此错误表示缺少 `Microsoft.CSharp` 库。</span><span class="sxs-lookup"><span data-stu-id="4caad-319">This error indicates that the `Microsoft.CSharp` library is missing.</span></span> <span data-ttu-id="4caad-320">将其添加到 "**程序集-&gt;框架**" 选项卡中。</span><span class="sxs-lookup"><span data-stu-id="4caad-320">Add it in the **Assemblies-&gt;Framework** tab.</span></span>

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a><span data-ttu-id="4caad-321">无法从客户端访问调用方状态。调用方位于 Visual Basic 或强类型中心中;"从类型 ' 任务（of 对象）" 转换为类型 "String" 无效 "错误</span><span class="sxs-lookup"><span data-stu-id="4caad-321">Caller state cannot be accessed from Clients.Caller in Visual Basic or in a strongly typed hub; "Conversion from type 'Task(Of Object)' to type 'String' is not valid" error</span></span>

<span data-ttu-id="4caad-322">若要访问 Visual Basic 或强类型中心中的调用方状态，请使用 `Clients.CallerState` 属性（在 SignalR 2.1 中引入），而不是 `Clients.Caller`。</span><span class="sxs-lookup"><span data-stu-id="4caad-322">To access caller state in Visual Basic or in a strongly typed hub, use the `Clients.CallerState` property (introduced in SignalR 2.1) instead of `Clients.Caller`.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="4caad-323">Visual Studio 问题</span><span class="sxs-lookup"><span data-stu-id="4caad-323">Visual Studio issues</span></span>

<span data-ttu-id="4caad-324">本部分介绍 Visual Studio 中遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="4caad-324">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="4caad-325">脚本文档节点未出现在解决方案资源管理器</span><span class="sxs-lookup"><span data-stu-id="4caad-325">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="4caad-326">在调试过程中，我们的一些教程会将您定向到解决方案资源管理器中的 "脚本文档" 节点。</span><span class="sxs-lookup"><span data-stu-id="4caad-326">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="4caad-327">此节点由 JavaScript 调试器生成，仅在调试 Internet Explorer 中的浏览器客户端时显示;如果使用的是 Chrome 或 Firefox，则不会显示该节点。</span><span class="sxs-lookup"><span data-stu-id="4caad-327">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="4caad-328">如果另一个客户端调试器正在运行，如 Silverlight 调试器，JavaScript 调试器也不会运行。</span><span class="sxs-lookup"><span data-stu-id="4caad-328">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="4caad-329">SignalR 在 Visual Studio 2008 或更早版本上不起作用</span><span class="sxs-lookup"><span data-stu-id="4caad-329">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="4caad-330">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="4caad-330">This behavior is by design.</span></span> <span data-ttu-id="4caad-331">SignalR 需要 .NET Framework 4 或更高版本;这要求在 Visual Studio 2010 或更高版本中开发 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4caad-331">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span> <span data-ttu-id="4caad-332">SignalR 的服务器组件要求 4.5 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="4caad-332">The server component of SignalR requires .NET Framework 4.5.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="4caad-333">IIS 问题</span><span class="sxs-lookup"><span data-stu-id="4caad-333">IIS issues</span></span>

<span data-ttu-id="4caad-334">本部分包含与 Internet Information Services 有关的问题。</span><span class="sxs-lookup"><span data-stu-id="4caad-334">This section contains issues with Internet Information Services.</span></span>

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a><span data-ttu-id="4caad-335">SignalR 适用于 Visual Studio 开发服务器，但在 IIS 中不适用</span><span class="sxs-lookup"><span data-stu-id="4caad-335">SignalR works on Visual Studio development server, but not in IIS</span></span>

<span data-ttu-id="4caad-336">IIS 7.0 和7.5 支持 SignalR，但必须添加对无扩展名 Url 的支持。</span><span class="sxs-lookup"><span data-stu-id="4caad-336">SignalR is supported on IIS 7.0 and 7.5, but support for extensionless URLs must be added.</span></span> <span data-ttu-id="4caad-337">若要添加对无扩展名 Url 的支持，请参阅[https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span><span class="sxs-lookup"><span data-stu-id="4caad-337">To add support for extensionless URLs, see [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span></span>

<span data-ttu-id="4caad-338">SignalR 要求在服务器上安装 ASP.NET （默认情况下未在 IIS 上安装 ASP.NET）。</span><span class="sxs-lookup"><span data-stu-id="4caad-338">SignalR requires ASP.NET to be installed on the server (ASP.NET is not installed on IIS by default).</span></span> <span data-ttu-id="4caad-339">若要安装 ASP.NET，请参阅[ASP.NET 下载](https://www.asp.net/downloads)。</span><span class="sxs-lookup"><span data-stu-id="4caad-339">To install ASP.NET, see [ASP.NET Downloads](https://www.asp.net/downloads).</span></span>

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a><span data-ttu-id="4caad-340">Microsoft Azure 问题</span><span class="sxs-lookup"><span data-stu-id="4caad-340">Microsoft Azure issues</span></span>

<span data-ttu-id="4caad-341">本部分包含与 Microsoft Azure 有关的问题。</span><span class="sxs-lookup"><span data-stu-id="4caad-341">This section contains issues with Microsoft Azure.</span></span>

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a><span data-ttu-id="4caad-342">在 Azure 辅助角色中托管 SignalR 时的 FileLoadException</span><span class="sxs-lookup"><span data-stu-id="4caad-342">FileLoadException when hosting SignalR in an Azure Worker Role</span></span>

<span data-ttu-id="4caad-343">在 Azure 辅助角色中托管 SignalR 可能会导致例外 "无法加载文件或程序集 ' Owin，Version = 2.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="4caad-343">Hosting SignalR in an Azure Worker Role might result in the exception "Could not load file or assembly 'Microsoft.Owin, Version=2.0.0.0".</span></span> <span data-ttu-id="4caad-344">这是 NuGet 的已知问题;不会在 Azure 辅助角色项目中自动添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="4caad-344">This is a known issue with NuGet; Binding redirects are not added automatically in Azure Worker Role projects.</span></span> <span data-ttu-id="4caad-345">若要解决此问题，可以手动添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="4caad-345">To fix this, you can add the binding redirects manually.</span></span> <span data-ttu-id="4caad-346">将以下行添加到辅助角色项目的 `app.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="4caad-346">Add the following lines to the `app.config` file for your Worker Role project.</span></span>

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="4caad-347">更改主题名称后，不通过 Azure 底板接收消息</span><span class="sxs-lookup"><span data-stu-id="4caad-347">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="4caad-348">Azure 底板使用的主题在内部维护;它们不是用户可配置的。</span><span class="sxs-lookup"><span data-stu-id="4caad-348">The topics used by the Azure backplane are maintained internally; they are not intended to be user-configurable.</span></span>
