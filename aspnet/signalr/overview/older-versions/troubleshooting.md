---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 故障排除（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文介绍了开发 SignalR 应用程序时的常见问题。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468098"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="2d241-103">SignalR 疑难解答 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="2d241-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="2d241-104">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="2d241-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2d241-105">本文档介绍了 SignalR 的常见疑难解答问题。</span><span class="sxs-lookup"><span data-stu-id="2d241-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="2d241-106">本文档包含以下各节。</span><span class="sxs-lookup"><span data-stu-id="2d241-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="2d241-107">以静默方式在客户端和服务器之间调用方法失败</span><span class="sxs-lookup"><span data-stu-id="2d241-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="2d241-108">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="2d241-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="2d241-109">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="2d241-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="2d241-110">Visual Studio 问题</span><span class="sxs-lookup"><span data-stu-id="2d241-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="2d241-111">Internet Information Services 问题</span><span class="sxs-lookup"><span data-stu-id="2d241-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="2d241-112">Azure 问题</span><span class="sxs-lookup"><span data-stu-id="2d241-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="2d241-113">以静默方式在客户端和服务器之间调用方法失败</span><span class="sxs-lookup"><span data-stu-id="2d241-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="2d241-114">本部分介绍在客户端和服务器之间的方法调用失败的可能原因，而没有有意义的错误消息。</span><span class="sxs-lookup"><span data-stu-id="2d241-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="2d241-115">在 SignalR 应用程序中，服务器没有有关客户端实现的方法的信息;当服务器调用客户端方法时，方法名称和参数数据将发送到客户端，并且仅当该方法以服务器指定的格式存在时，才会执行此方法。</span><span class="sxs-lookup"><span data-stu-id="2d241-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="2d241-116">如果在客户端上找不到匹配的方法，则不会执行任何操作，并且不会在服务器上引发任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="2d241-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="2d241-117">若要进一步调查未调用的客户端方法，你可以在调用 start 方法之前打开中心日志记录，以查看来自服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="2d241-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="2d241-118">若要在 JavaScript 应用程序中启用日志记录，请参阅[如何启用客户端日志记录（JavaScript 客户端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="2d241-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="2d241-119">若要在 .NET 客户端应用程序中启用日志记录，请参阅[如何启用客户端日志记录（.Net 客户端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="2d241-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="2d241-120">拼写错误的方法、错误的方法签名或不正确的中心名称</span><span class="sxs-lookup"><span data-stu-id="2d241-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="2d241-121">如果被调用方法的名称或签名与客户端上的适当方法不完全匹配，则调用将失败。</span><span class="sxs-lookup"><span data-stu-id="2d241-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="2d241-122">验证服务器调用的方法名称是否与客户端上的方法的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="2d241-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="2d241-123">此外，SignalR 使用 camel 大小写方法创建中心代理，这在 JavaScript 中是合适的方法，因此，在服务器上调用 `SendMessage` 的方法将在客户端代理 `sendMessage` 中调用。</span><span class="sxs-lookup"><span data-stu-id="2d241-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="2d241-124">如果使用服务器端代码中的 `HubName` 属性，请验证所使用的名称是否与用于在客户端上创建集线器的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="2d241-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="2d241-125">如果不使用 `HubName` 属性，请验证 JavaScript 客户端中的中心名称是否采用 camel 大小写格式（如 chatHub 而不是 ChatHub）。</span><span class="sxs-lookup"><span data-stu-id="2d241-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="2d241-126">客户端上的重复方法名称</span><span class="sxs-lookup"><span data-stu-id="2d241-126">Duplicate method name on client</span></span>

<span data-ttu-id="2d241-127">验证在客户端上没有仅大小写不同的重复方法。</span><span class="sxs-lookup"><span data-stu-id="2d241-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="2d241-128">如果客户端应用程序有一个名为 `sendMessage`的方法，请验证是否也没有名为 `SendMessage` 的方法。</span><span class="sxs-lookup"><span data-stu-id="2d241-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="2d241-129">客户端上缺少 JSON 分析器</span><span class="sxs-lookup"><span data-stu-id="2d241-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="2d241-130">SignalR 要求提供 JSON 分析器以序列化服务器和客户端之间的调用。</span><span class="sxs-lookup"><span data-stu-id="2d241-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="2d241-131">如果客户端没有内置的 JSON 分析器（如 Internet Explorer 7），则需要在应用程序中包含一个。</span><span class="sxs-lookup"><span data-stu-id="2d241-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="2d241-132">可在[此处](http://nuget.org/packages/json2)下载 JSON 分析器。</span><span class="sxs-lookup"><span data-stu-id="2d241-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="2d241-133">混合中心和 PersistentConnection 语法</span><span class="sxs-lookup"><span data-stu-id="2d241-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="2d241-134">SignalR 使用两种通信模型：集线器和 PersistentConnections。</span><span class="sxs-lookup"><span data-stu-id="2d241-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="2d241-135">在客户端代码中，调用这两个通信模型的语法不同。</span><span class="sxs-lookup"><span data-stu-id="2d241-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="2d241-136">如果已在服务器代码中添加集线器，请验证所有客户端代码是否均使用正确的中心语法。</span><span class="sxs-lookup"><span data-stu-id="2d241-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="2d241-137">**在 JavaScript 客户端中创建 PersistentConnection 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="2d241-138">**在 Javascript 客户端中创建集线器代理的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="2d241-139">**C#将路由映射到 PersistentConnection 的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="2d241-140">**C#如果有多个应用程序，则将路由映射到中心或多个集线器的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="2d241-141">在添加订阅之前已启动连接</span><span class="sxs-lookup"><span data-stu-id="2d241-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="2d241-142">如果在将可从服务器调用的方法添加到代理之前启动了中心的连接，则不会收到消息。</span><span class="sxs-lookup"><span data-stu-id="2d241-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="2d241-143">以下 JavaScript 代码将不会正确启动集线器：</span><span class="sxs-lookup"><span data-stu-id="2d241-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="2d241-144">**不允许接收集线器消息的不正确的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="2d241-145">请改为在调用 Start 之前添加方法订阅：</span><span class="sxs-lookup"><span data-stu-id="2d241-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="2d241-146">**正确向中心添加订阅的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="2d241-147">中心代理上缺少方法名称</span><span class="sxs-lookup"><span data-stu-id="2d241-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="2d241-148">验证在服务器上定义的方法是否已在客户端上订阅。</span><span class="sxs-lookup"><span data-stu-id="2d241-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="2d241-149">即使服务器定义了方法，仍必须将它添加到客户端代理。</span><span class="sxs-lookup"><span data-stu-id="2d241-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="2d241-150">可以通过以下方式将方法添加到客户端代理（请注意，方法已添加到中心的 `client` 成员，而不是直接添加到中心）：</span><span class="sxs-lookup"><span data-stu-id="2d241-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="2d241-151">**向中心代理添加方法的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="2d241-152">未声明为公共的集线器或集线器方法</span><span class="sxs-lookup"><span data-stu-id="2d241-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="2d241-153">若要在客户端上可见，中心实现和方法必须声明为 `public`。</span><span class="sxs-lookup"><span data-stu-id="2d241-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="2d241-154">从不同的应用程序访问集线器</span><span class="sxs-lookup"><span data-stu-id="2d241-154">Accessing hub from a different application</span></span>

<span data-ttu-id="2d241-155">SignalR 中心只能通过实现 SignalR 客户端的应用程序进行访问。</span><span class="sxs-lookup"><span data-stu-id="2d241-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="2d241-156">SignalR 无法与其他通信库（如 SOAP 或 WCF web 服务）进行互操作。如果没有可用于目标平台的 SignalR 客户端，则无法直接访问服务器的终结点。</span><span class="sxs-lookup"><span data-stu-id="2d241-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="2d241-157">手动序列化数据</span><span class="sxs-lookup"><span data-stu-id="2d241-157">Manually serializing data</span></span>

<span data-ttu-id="2d241-158">SignalR 将自动使用 JSON 序列化方法参数，无需自行执行此操作。</span><span class="sxs-lookup"><span data-stu-id="2d241-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="2d241-159">远程集线器方法未在 OnDisconnected 函数中的客户端上执行</span><span class="sxs-lookup"><span data-stu-id="2d241-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="2d241-160">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-160">This behavior is by design.</span></span> <span data-ttu-id="2d241-161">调用 `OnDisconnected` 时，中心已进入 `Disconnected` 状态，该状态不允许调用其他集线器方法。</span><span class="sxs-lookup"><span data-stu-id="2d241-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="2d241-162">**C#在 OnDisconnected 事件中正确执行代码的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="2d241-163">已达到连接限制</span><span class="sxs-lookup"><span data-stu-id="2d241-163">Connection limit reached</span></span>

<span data-ttu-id="2d241-164">在客户端操作系统（如 Windows 7）上使用完整的 IIS 版本时，会施加10个连接限制。</span><span class="sxs-lookup"><span data-stu-id="2d241-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="2d241-165">使用客户端操作系统时，请改用 IIS Express 来避免此限制。</span><span class="sxs-lookup"><span data-stu-id="2d241-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="2d241-166">未正确设置跨域连接</span><span class="sxs-lookup"><span data-stu-id="2d241-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="2d241-167">如果跨域连接（SignalR URL 与宿主页面不在同一个域中的连接）未正确设置，则连接可能会失败，且不会出现错误消息。</span><span class="sxs-lookup"><span data-stu-id="2d241-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="2d241-168">有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="2d241-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="2d241-169">使用 NTLM （Active Directory）的连接在 .NET 客户端中不起作用</span><span class="sxs-lookup"><span data-stu-id="2d241-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="2d241-170">如果连接配置不正确，则使用域安全性的 .NET 客户端应用程序中的连接可能会失败。</span><span class="sxs-lookup"><span data-stu-id="2d241-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="2d241-171">若要在域环境中使用 SignalR，请设置所需的连接属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2d241-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="2d241-172">**C#实现连接凭据的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="2d241-173">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="2d241-173">Other connection issues</span></span>

<span data-ttu-id="2d241-174">本部分介绍连接过程中出现的特定症状或错误消息的原因和解决方法。</span><span class="sxs-lookup"><span data-stu-id="2d241-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="2d241-175">"必须在可以发送数据之前调用启动" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="2d241-176">如果在启动连接之前代码引用 SignalR 对象，则通常会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="2d241-177">处理程序的绑定和将调用在服务器上定义的方法的类似方法必须在连接完成后添加。</span><span class="sxs-lookup"><span data-stu-id="2d241-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="2d241-178">请注意，对 `Start` 的调用是异步的，因此调用后的代码可以在完成之前执行。</span><span class="sxs-lookup"><span data-stu-id="2d241-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="2d241-179">在连接完全启动后添加处理程序的最佳方式是将其放入一个回调函数，该函数作为参数传递给 start 方法：</span><span class="sxs-lookup"><span data-stu-id="2d241-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="2d241-180">**正确添加引用 SignalR 对象的事件处理程序的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="2d241-181">如果仍在引用 SignalR 对象，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="2d241-182">"301 永久移动" 或 "302 移动" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="2d241-183">如果项目包含一个名为 SignalR 的文件夹，该文件夹将干扰自动创建的代理，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="2d241-184">若要避免此错误，请不要在应用程序中使用称为 `SignalR` 的文件夹，或关闭自动代理生成。</span><span class="sxs-lookup"><span data-stu-id="2d241-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="2d241-185">有关更多详细信息，请参阅[生成的代理以及它所执行的](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)操作。</span><span class="sxs-lookup"><span data-stu-id="2d241-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="2d241-186">.NET 或 Silverlight 客户端中的 "403 禁止访问" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="2d241-187">此错误可能出现在未正确启用跨域通信的跨域环境中。</span><span class="sxs-lookup"><span data-stu-id="2d241-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="2d241-188">有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="2d241-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="2d241-189">若要在 Silverlight 客户端中建立跨域连接，请参阅[从 silverlight 客户端进行跨域连接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。</span><span class="sxs-lookup"><span data-stu-id="2d241-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="2d241-190">"找不到 404" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-190">"404 Not Found" error</span></span>

<span data-ttu-id="2d241-191">此问题有几个原因。</span><span class="sxs-lookup"><span data-stu-id="2d241-191">There are several causes for this issue.</span></span> <span data-ttu-id="2d241-192">验证以下所有内容：</span><span class="sxs-lookup"><span data-stu-id="2d241-192">Verify all of the following:</span></span>

- <span data-ttu-id="2d241-193">**集线器代理地址引用的格式不正确：** 如果对生成的中心代理地址的引用的格式不正确，则通常会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="2d241-194">验证对中心地址的引用是否正确。</span><span class="sxs-lookup"><span data-stu-id="2d241-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="2d241-195">有关详细信息，请参阅[如何引用动态生成的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。</span><span class="sxs-lookup"><span data-stu-id="2d241-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="2d241-196">添加**中心路由之前，向应用程序添加路由：** 如果你的应用程序使用其他路由，请验证添加的第一个路由是对 `MapHubs`的调用。</span><span class="sxs-lookup"><span data-stu-id="2d241-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="2d241-197">"500 内部服务器错误"</span><span class="sxs-lookup"><span data-stu-id="2d241-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="2d241-198">这是一种非常通用的错误，可能会产生多种原因。</span><span class="sxs-lookup"><span data-stu-id="2d241-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="2d241-199">错误的详细信息应该出现在服务器的事件日志中，也可以通过调试服务器找到。</span><span class="sxs-lookup"><span data-stu-id="2d241-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="2d241-200">可以通过打开服务器上的详细错误来获取更详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="2d241-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="2d241-201">有关详细信息，请参阅[如何处理中心类中的错误](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="2d241-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="2d241-202">"TypeError： &lt;hubType&gt; 未定义" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="2d241-203">如果未正确调用 `MapHubs`，则会导致此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="2d241-204">有关详细信息，请参阅[如何注册 SignalR 路由和配置 SignalR 选项](../guide-to-the-api/hubs-api-guide-server.md#route)。</span><span class="sxs-lookup"><span data-stu-id="2d241-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="2d241-205">用户代码未处理 JsonSerializationException</span><span class="sxs-lookup"><span data-stu-id="2d241-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="2d241-206">验证发送给方法的参数不包括非序列化类型（如文件句柄或数据库连接）。</span><span class="sxs-lookup"><span data-stu-id="2d241-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="2d241-207">如果需要在不想发送到客户端的服务器端对象上使用成员（出于安全原因或序列化的原因），请使用 `JSONIgnore` 特性。</span><span class="sxs-lookup"><span data-stu-id="2d241-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="2d241-208">"协议错误：未知传输" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="2d241-209">如果客户端不支持 SignalR 使用的传输，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="2d241-210">有关可与 SignalR 一起使用的浏览器的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="2d241-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="2d241-211">"JavaScript Hub 代理生成已禁用。"</span><span class="sxs-lookup"><span data-stu-id="2d241-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="2d241-212">如果设置 `DisableJavaScriptProxies`，同时在 `signalr/hubs`同时包含对动态生成的代理的引用，则会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="2d241-213">有关手动创建代理的详细信息，请参阅[生成的代理及其功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="2d241-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="2d241-214">"连接 ID 的格式不正确，或者" 用户标识在 active SignalR 连接期间无法更改 "错误</span><span class="sxs-lookup"><span data-stu-id="2d241-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="2d241-215">如果正在使用身份验证，并且在停止连接之前注销了客户端，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="2d241-216">解决方法是在注销客户端之前停止 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="2d241-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="2d241-217">"未捕获的错误： SignalR： jQuery 找不到。</span><span class="sxs-lookup"><span data-stu-id="2d241-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="2d241-218">请确保引用 jQuery，然后再引用 SignalR 文件 "错误</span><span class="sxs-lookup"><span data-stu-id="2d241-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="2d241-219">SignalR JavaScript 客户端需要 jQuery 才能运行。</span><span class="sxs-lookup"><span data-stu-id="2d241-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="2d241-220">验证对 jQuery 的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否在对 SignalR 的引用之前。</span><span class="sxs-lookup"><span data-stu-id="2d241-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="2d241-221">"未捕获 TypeError：无法读取属性"&lt;属性&gt;"未定义" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="2d241-222">此错误是由于未正确引用 jQuery 或中心代理而导致的。</span><span class="sxs-lookup"><span data-stu-id="2d241-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="2d241-223">验证对 jQuery 和中心代理的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否在对集线器代理的引用之前。</span><span class="sxs-lookup"><span data-stu-id="2d241-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="2d241-224">对集线器代理的默认引用如下所示：</span><span class="sxs-lookup"><span data-stu-id="2d241-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="2d241-225">**正确引用中心代理的 HTML 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2d241-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="2d241-226">"RuntimeBinderException 已被用户代码处理" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="2d241-227">如果使用 `Hub.On` 的错误重载，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="2d241-228">如果该方法具有返回值，则返回类型必须指定为泛型类型参数：</span><span class="sxs-lookup"><span data-stu-id="2d241-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="2d241-229">**在客户端上定义的方法（不生成代理）**</span><span class="sxs-lookup"><span data-stu-id="2d241-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="2d241-230">连接 ID 不一致或页面加载之间的连接中断</span><span class="sxs-lookup"><span data-stu-id="2d241-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="2d241-231">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-231">This behavior is by design.</span></span> <span data-ttu-id="2d241-232">由于中心对象承载于 page 对象中，因此在页面刷新时，中心将被销毁。</span><span class="sxs-lookup"><span data-stu-id="2d241-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="2d241-233">多页应用程序需要维护用户和连接 Id 之间的关联，以便它们在页面加载之间保持一致。</span><span class="sxs-lookup"><span data-stu-id="2d241-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="2d241-234">连接 Id 可以存储在服务器上的 `ConcurrentDictionary` 对象或数据库中。</span><span class="sxs-lookup"><span data-stu-id="2d241-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="2d241-235">"值不能为 null" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-235">"Value cannot be null" error</span></span>

<span data-ttu-id="2d241-236">当前不支持带有可选参数的服务器端方法;如果省略可选参数，则该方法将失败。</span><span class="sxs-lookup"><span data-stu-id="2d241-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="2d241-237">有关详细信息，请参阅[可选参数](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="2d241-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="2d241-238">"Firefox 无法与服务器建立连接，因为在 Firebug 中 &lt;地址&gt;" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="2d241-239">如果 WebSocket 传输的协商失败并且改为使用另一个传输，则会在 Firebug 中出现此错误消息。</span><span class="sxs-lookup"><span data-stu-id="2d241-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="2d241-240">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="2d241-241">.NET 客户端应用程序中的 "远程证书根据验证过程无效" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="2d241-242">如果服务器需要自定义客户端证书，则可以在发出请求之前将 x509certificate 添加到连接。</span><span class="sxs-lookup"><span data-stu-id="2d241-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="2d241-243">使用 `Connection.AddClientCertificate`将证书添加到连接。</span><span class="sxs-lookup"><span data-stu-id="2d241-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="2d241-244">身份验证超时后断开连接</span><span class="sxs-lookup"><span data-stu-id="2d241-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="2d241-245">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-245">This behavior is by design.</span></span> <span data-ttu-id="2d241-246">连接处于活动状态时，无法修改身份验证凭据;若要刷新凭据，必须停止并重新启动该连接。</span><span class="sxs-lookup"><span data-stu-id="2d241-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="2d241-247">使用 jQuery Mobile 时，OnConnected 调用了两次</span><span class="sxs-lookup"><span data-stu-id="2d241-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="2d241-248">jQuery Mobile 的 `initializePage` 函数强制重新执行每个页面中的脚本，从而创建另一个连接。</span><span class="sxs-lookup"><span data-stu-id="2d241-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="2d241-249">此问题的解决方案包括：</span><span class="sxs-lookup"><span data-stu-id="2d241-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="2d241-250">在 JavaScript 文件之前包括对 jQuery Mobile 的引用。</span><span class="sxs-lookup"><span data-stu-id="2d241-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="2d241-251">通过设置 `$.mobile.autoInitializePage = false`禁用 `initializePage` 函数。</span><span class="sxs-lookup"><span data-stu-id="2d241-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="2d241-252">等待页面完成初始化，然后再开始连接。</span><span class="sxs-lookup"><span data-stu-id="2d241-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="2d241-253">使用服务器发送事件的 Silverlight 应用程序中的消息延迟</span><span class="sxs-lookup"><span data-stu-id="2d241-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="2d241-254">在 Silverlight 上使用服务器发送的事件时，消息会被延迟。</span><span class="sxs-lookup"><span data-stu-id="2d241-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="2d241-255">若要改为强制使用长轮询，请在启动连接时使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="2d241-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="2d241-256">使用永久帧协议的 "权限被拒绝"</span><span class="sxs-lookup"><span data-stu-id="2d241-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="2d241-257">这是一个已知问题，请[参阅此](https://github.com/SignalR/SignalR/issues/1963)文。</span><span class="sxs-lookup"><span data-stu-id="2d241-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="2d241-258">使用最新 JQuery library 时可能会出现此症状;解决方法是将应用程序降级到 JQuery 1.8.2。</span><span class="sxs-lookup"><span data-stu-id="2d241-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="2d241-259">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="2d241-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="2d241-260">以下部分包含编译器和服务器端运行时错误的可能解决方案。</span><span class="sxs-lookup"><span data-stu-id="2d241-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="2d241-261">对中心实例的引用为 null</span><span class="sxs-lookup"><span data-stu-id="2d241-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="2d241-262">由于已为每个连接创建集线器实例，因此无法在代码中自行创建集线器的实例。</span><span class="sxs-lookup"><span data-stu-id="2d241-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="2d241-263">若要从中心自身外部调用集线器上的方法，请参阅[如何从中心类的外部调用客户端方法和管理组](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，了解如何获取对中心上下文的引用。</span><span class="sxs-lookup"><span data-stu-id="2d241-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="2d241-264">Httpcontext.current 为 null</span><span class="sxs-lookup"><span data-stu-id="2d241-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="2d241-265">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-265">This behavior is by design.</span></span> <span data-ttu-id="2d241-266">SignalR 不支持 ASP.NET 会话状态，因为启用会话状态将中断双工消息。</span><span class="sxs-lookup"><span data-stu-id="2d241-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="2d241-267">没有合适的替代方法</span><span class="sxs-lookup"><span data-stu-id="2d241-267">No suitable method to override</span></span>

<span data-ttu-id="2d241-268">如果使用的是较旧文档或博客中的代码，则可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="2d241-269">验证你未引用已更改或已弃用的方法的名称（如 `OnConnectedAsync`）。</span><span class="sxs-lookup"><span data-stu-id="2d241-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="2d241-270">HostContextExtensions. WebSocketServerUrl 为 null</span><span class="sxs-lookup"><span data-stu-id="2d241-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="2d241-271">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-271">This behavior is by design.</span></span> <span data-ttu-id="2d241-272">此成员已弃用，不应使用。</span><span class="sxs-lookup"><span data-stu-id="2d241-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="2d241-273">"名为 ' signalr ' 的路由已在路由集合中" 错误</span><span class="sxs-lookup"><span data-stu-id="2d241-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="2d241-274">如果应用程序调用了两次 `MapHubs`，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="2d241-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="2d241-275">一些示例应用程序直接在全局应用程序文件中调用 `MapHubs`;其他人在包装类中进行调用。</span><span class="sxs-lookup"><span data-stu-id="2d241-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="2d241-276">确保应用程序不会同时执行这两项操作。</span><span class="sxs-lookup"><span data-stu-id="2d241-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="2d241-277">Visual Studio 问题</span><span class="sxs-lookup"><span data-stu-id="2d241-277">Visual Studio issues</span></span>

<span data-ttu-id="2d241-278">本部分介绍 Visual Studio 中遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="2d241-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="2d241-279">脚本文档节点未出现在解决方案资源管理器</span><span class="sxs-lookup"><span data-stu-id="2d241-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="2d241-280">在调试过程中，我们的一些教程会将您定向到解决方案资源管理器中的 "脚本文档" 节点。</span><span class="sxs-lookup"><span data-stu-id="2d241-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="2d241-281">此节点由 JavaScript 调试器生成，仅在调试 Internet Explorer 中的浏览器客户端时显示;如果使用的是 Chrome 或 Firefox，则不会显示该节点。</span><span class="sxs-lookup"><span data-stu-id="2d241-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="2d241-282">如果另一个客户端调试器正在运行，如 Silverlight 调试器，JavaScript 调试器也不会运行。</span><span class="sxs-lookup"><span data-stu-id="2d241-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="2d241-283">SignalR 在 Visual Studio 2008 或更早版本上不起作用</span><span class="sxs-lookup"><span data-stu-id="2d241-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="2d241-284">此行为是设计使然。</span><span class="sxs-lookup"><span data-stu-id="2d241-284">This behavior is by design.</span></span> <span data-ttu-id="2d241-285">SignalR 需要 .NET Framework 4 或更高版本;这要求在 Visual Studio 2010 或更高版本中开发 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2d241-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="2d241-286">IIS 问题</span><span class="sxs-lookup"><span data-stu-id="2d241-286">IIS issues</span></span>

<span data-ttu-id="2d241-287">本部分包含与 Internet Information Services 有关的问题。</span><span class="sxs-lookup"><span data-stu-id="2d241-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="2d241-288">Routeconfig 调用后网站崩溃</span><span class="sxs-lookup"><span data-stu-id="2d241-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="2d241-289">此问题已在最新版本的 SignalR 中得到解决。</span><span class="sxs-lookup"><span data-stu-id="2d241-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="2d241-290">通过使用 NuGet 更新安装，验证你是否正在使用 SignalR 的最新发布版本。</span><span class="sxs-lookup"><span data-stu-id="2d241-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="2d241-291">Azure 问题</span><span class="sxs-lookup"><span data-stu-id="2d241-291">Azure issues</span></span>

<span data-ttu-id="2d241-292">本部分包含与 Microsoft Azure 有关的问题。</span><span class="sxs-lookup"><span data-stu-id="2d241-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="2d241-293">更改主题名称后，不通过 Azure 底板接收消息</span><span class="sxs-lookup"><span data-stu-id="2d241-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="2d241-294">Azure 底板使用的主题并不是用户可配置的。</span><span class="sxs-lookup"><span data-stu-id="2d241-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
