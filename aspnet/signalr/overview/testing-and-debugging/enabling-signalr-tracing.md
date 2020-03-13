---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: 启用 SignalR 跟踪 |Microsoft Docs
author: bradygaster
description: 本文档介绍如何为 SignalR 服务器和客户端启用和配置跟踪。 利用跟踪功能，您可以查看有关事件的诊断信息 。
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467438"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="413f4-104">启用 SignalR 跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="413f4-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="413f4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="413f4-106">本文档介绍如何为 SignalR 服务器和客户端启用和配置跟踪。</span><span class="sxs-lookup"><span data-stu-id="413f4-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="413f4-107">跟踪使你可以查看有关 SignalR 应用程序中事件的诊断信息。</span><span class="sxs-lookup"><span data-stu-id="413f4-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="413f4-108">本主题最初由 Fletcher 的写作。</span><span class="sxs-lookup"><span data-stu-id="413f4-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="413f4-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="413f4-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="413f4-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="413f4-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="413f4-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="413f4-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="413f4-112">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="413f4-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="413f4-113">问题和注释</span><span class="sxs-lookup"><span data-stu-id="413f4-113">Questions and comments</span></span>
>
> <span data-ttu-id="413f4-114">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="413f4-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="413f4-115">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="413f4-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="413f4-116">启用跟踪后，SignalR 应用程序会创建事件的日志项。</span><span class="sxs-lookup"><span data-stu-id="413f4-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="413f4-117">你可以从客户端和服务器记录事件。</span><span class="sxs-lookup"><span data-stu-id="413f4-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="413f4-118">跟踪服务器日志连接、扩展提供程序和消息总线事件。</span><span class="sxs-lookup"><span data-stu-id="413f4-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="413f4-119">对客户端的跟踪记录连接事件。</span><span class="sxs-lookup"><span data-stu-id="413f4-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="413f4-120">在 SignalR 2.1 和更高版本中，在客户端上进行的跟踪会记录中心调用消息的全部内容。</span><span class="sxs-lookup"><span data-stu-id="413f4-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="413f4-121">内容</span><span class="sxs-lookup"><span data-stu-id="413f4-121">Contents</span></span>

- [<span data-ttu-id="413f4-122">在服务器上启用跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="413f4-123">将服务器事件记录到文本文件</span><span class="sxs-lookup"><span data-stu-id="413f4-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="413f4-124">将服务器事件记录到事件日志中</span><span class="sxs-lookup"><span data-stu-id="413f4-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="413f4-125">在 .NET 客户端中启用跟踪（Windows 桌面应用程序）</span><span class="sxs-lookup"><span data-stu-id="413f4-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="413f4-126">向控制台记录桌面客户端事件</span><span class="sxs-lookup"><span data-stu-id="413f4-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="413f4-127">将桌面客户端事件记录到文本文件中</span><span class="sxs-lookup"><span data-stu-id="413f4-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="413f4-128">在 Windows Phone 8 个客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="413f4-129">将客户端事件 Windows Phone 日志记录到 UI</span><span class="sxs-lookup"><span data-stu-id="413f4-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="413f4-130">将客户端事件 Windows Phone 日志记录到调试控制台</span><span class="sxs-lookup"><span data-stu-id="413f4-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="413f4-131">在 JavaScript 客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="413f4-132">在服务器上启用跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-132">Enabling tracing on the server</span></span>

<span data-ttu-id="413f4-133">在应用程序的配置文件（App.config 或 web.config 中，具体取决于项目的类型）上启用对服务器的跟踪。指定要记录的事件的类别。</span><span class="sxs-lookup"><span data-stu-id="413f4-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="413f4-134">在配置文件中，还可以指定是使用[TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)的实现将事件记录到文本文件、Windows 事件日志还是自定义日志。</span><span class="sxs-lookup"><span data-stu-id="413f4-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="413f4-135">服务器事件类别包含以下消息种类：</span><span class="sxs-lookup"><span data-stu-id="413f4-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="413f4-136">Source</span><span class="sxs-lookup"><span data-stu-id="413f4-136">Source</span></span> | <span data-ttu-id="413f4-137">消息</span><span class="sxs-lookup"><span data-stu-id="413f4-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="413f4-138">SignalR.SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="413f4-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="413f4-139">SQL 消息总线扩展提供程序设置、数据库操作、错误和超时事件</span><span class="sxs-lookup"><span data-stu-id="413f4-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="413f4-140">SignalR.ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="413f4-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="413f4-141">Service bus 扩展提供程序主题创建和订阅、错误和消息传递事件</span><span class="sxs-lookup"><span data-stu-id="413f4-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="413f4-142">SignalR.RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="413f4-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="413f4-143">Redis 扩展提供程序连接、断开连接和错误事件</span><span class="sxs-lookup"><span data-stu-id="413f4-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="413f4-144">SignalR.ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="413f4-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="413f4-145">扩展消息传递事件</span><span class="sxs-lookup"><span data-stu-id="413f4-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="413f4-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="413f4-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="413f4-147">WebSocket 传输连接、断开连接、消息传递和错误事件</span><span class="sxs-lookup"><span data-stu-id="413f4-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="413f4-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="413f4-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="413f4-149">ServerSentEvents 传输连接、断开连接、消息传递和错误事件</span><span class="sxs-lookup"><span data-stu-id="413f4-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="413f4-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="413f4-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="413f4-151">ForeverFrame 传输连接、断开连接、消息传递和错误事件</span><span class="sxs-lookup"><span data-stu-id="413f4-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="413f4-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="413f4-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="413f4-153">LongPolling 传输连接、断开连接、消息传递和错误事件</span><span class="sxs-lookup"><span data-stu-id="413f4-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="413f4-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="413f4-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="413f4-155">传输连接、断开连接和 keepalive 事件</span><span class="sxs-lookup"><span data-stu-id="413f4-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="413f4-156">SignalR.ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="413f4-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="413f4-157">中心发现事件</span><span class="sxs-lookup"><span data-stu-id="413f4-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="413f4-158">将服务器事件记录到文本文件</span><span class="sxs-lookup"><span data-stu-id="413f4-158">Logging server events to text files</span></span>

<span data-ttu-id="413f4-159">下面的代码演示如何为每个事件类别启用跟踪。</span><span class="sxs-lookup"><span data-stu-id="413f4-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="413f4-160">此示例将应用程序配置为将事件记录到文本文件中。</span><span class="sxs-lookup"><span data-stu-id="413f4-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="413f4-161">**用于启用跟踪的 XML 服务器代码**</span><span class="sxs-lookup"><span data-stu-id="413f4-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="413f4-162">在上面的代码中，`SignalRSwitch` 项指定用于发送到指定日志的事件的[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="413f4-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="413f4-163">在这种情况下，它设置为 `Verbose` 这意味着记录所有调试和跟踪消息。</span><span class="sxs-lookup"><span data-stu-id="413f4-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="413f4-164">以下输出显示了使用上述配置文件的应用程序 `transports.log.txt` 文件中的条目。</span><span class="sxs-lookup"><span data-stu-id="413f4-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="413f4-165">它显示新连接、已删除的连接和传输检测信号事件。</span><span class="sxs-lookup"><span data-stu-id="413f4-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="413f4-166">将服务器事件记录到事件日志中</span><span class="sxs-lookup"><span data-stu-id="413f4-166">Logging server events to the event log</span></span>

<span data-ttu-id="413f4-167">若要将事件记录到事件日志而不是文本文件，请更改 "`sharedListeners`" 节点中的项的值。</span><span class="sxs-lookup"><span data-stu-id="413f4-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="413f4-168">下面的代码演示如何将服务器事件记录到事件日志中：</span><span class="sxs-lookup"><span data-stu-id="413f4-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="413f4-169">**用于将事件记录到事件日志的 XML 服务器代码**</span><span class="sxs-lookup"><span data-stu-id="413f4-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="413f4-170">事件记录在应用程序日志中，并通过事件查看器提供，如下所示：</span><span class="sxs-lookup"><span data-stu-id="413f4-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![显示 SignalR 日志的事件查看器](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="413f4-172">使用事件日志时，请将 " **TraceLevel** " 设置为 " **Error** "，以保持消息的可管理性。</span><span class="sxs-lookup"><span data-stu-id="413f4-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="413f4-173">在 .NET 客户端中启用跟踪（Windows 桌面应用程序）</span><span class="sxs-lookup"><span data-stu-id="413f4-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="413f4-174">.NET 客户端可以[使用对等](https://msdn.microsoft.com/library/system.io.textwriter.aspx)的实现将事件记录到控制台、文本文件或自定义日志。</span><span class="sxs-lookup"><span data-stu-id="413f4-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="413f4-175">若要在 .NET 客户端中启用日志记录，请将连接的 `TraceLevel` 属性设置为 TraceLevels 值，将 `TraceWriter` 属性设置[为有效的](https://msdn.microsoft.com/library/system.io.textwriter.aspx) [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="413f4-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="413f4-176">向控制台记录桌面客户端事件</span><span class="sxs-lookup"><span data-stu-id="413f4-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="413f4-177">下面C#的代码演示如何将 .net 客户端中的事件记录到控制台：</span><span class="sxs-lookup"><span data-stu-id="413f4-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="413f4-178">将桌面客户端事件记录到文本文件中</span><span class="sxs-lookup"><span data-stu-id="413f4-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="413f4-179">下面C#的代码演示如何将 .net 客户端中的事件记录到文本文件中：</span><span class="sxs-lookup"><span data-stu-id="413f4-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="413f4-180">以下输出显示了使用上述配置文件的应用程序 `ClientLog.txt` 文件中的条目。</span><span class="sxs-lookup"><span data-stu-id="413f4-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="413f4-181">它显示连接到服务器的客户端，以及调用 `addMessage`的客户端方法的中心：</span><span class="sxs-lookup"><span data-stu-id="413f4-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="413f4-182">在 Windows Phone 8 个客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="413f4-183">用于 Windows Phone 应用程序的 SignalR 应用程序与桌面应用程序使用相同的 .NET 客户端[，但不](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)能使用[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)将其写入到文件。</span><span class="sxs-lookup"><span data-stu-id="413f4-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="413f4-184">相反，您需要为跟踪创建[一个用于跟踪的自](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)定义实现。</span><span class="sxs-lookup"><span data-stu-id="413f4-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="413f4-185">将客户端事件 Windows Phone 日志记录到 UI</span><span class="sxs-lookup"><span data-stu-id="413f4-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="413f4-186">[SignalR 基本代码](https://github.com/SignalR/SignalR/archive/master.zip)包含一个 Windows Phone 示例，该示例使用名为 `TextBlockWriter`[的自定义](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)类型为实现将跟踪输出写入[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="413f4-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="413f4-187">可在**samples/SignalR**项目中找到此类。 WP8。</span><span class="sxs-lookup"><span data-stu-id="413f4-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="413f4-188">在创建 `TextBlockWriter`的实例时，传入当前[SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)，并在[system.windows.controls.stackpanel>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中创建用于跟踪输出的[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：</span><span class="sxs-lookup"><span data-stu-id="413f4-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="413f4-189">然后，跟踪输出将写入在传入的[system.windows.controls.stackpanel>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中创建的新[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：</span><span class="sxs-lookup"><span data-stu-id="413f4-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="413f4-190">将客户端事件 Windows Phone 日志记录到调试控制台</span><span class="sxs-lookup"><span data-stu-id="413f4-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="413f4-191">若要将输出发送到调试控制台而不是 UI，请创建一个写入 "调试" 窗口并将其分配给连接的[TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) [属性的 "分配"。](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="413f4-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="413f4-192">然后，跟踪信息将写入 Visual Studio 中的 "调试" 窗口：</span><span class="sxs-lookup"><span data-stu-id="413f4-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="413f4-193">在 JavaScript 客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="413f4-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="413f4-194">若要对连接启用客户端日志记录，请在调用 `start` 方法来建立连接之前，设置连接对象上的 `logging` 属性。</span><span class="sxs-lookup"><span data-stu-id="413f4-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="413f4-195">**用于对浏览器控制台启用跟踪的客户端 JavaScript 代码（包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="413f4-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="413f4-196">**用于对浏览器控制台启用跟踪的客户端 JavaScript 代码（不包含生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="413f4-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="413f4-197">启用跟踪后，JavaScript 客户端会将事件记录到浏览器控制台。</span><span class="sxs-lookup"><span data-stu-id="413f4-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="413f4-198">若要访问浏览器控制台，请参阅[监视传输](../getting-started/introduction-to-signalr.md#MonitoringTransports)。</span><span class="sxs-lookup"><span data-stu-id="413f4-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="413f4-199">以下屏幕截图显示了已启用跟踪的 SignalR JavaScript 客户端。</span><span class="sxs-lookup"><span data-stu-id="413f4-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="413f4-200">它在浏览器控制台中显示连接和中心调用事件：</span><span class="sxs-lookup"><span data-stu-id="413f4-200">It shows connection and hub invocation events in the browser console:</span></span>

![在浏览器控制台中 SignalR 跟踪事件](enabling-signalr-tracing/_static/image4.png)
