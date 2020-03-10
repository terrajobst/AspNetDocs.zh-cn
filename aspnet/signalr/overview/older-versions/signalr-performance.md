---
uid: signalr/overview/older-versions/signalr-performance
title: SignalR Performance （SignalR 1.x） |Microsoft Docs
author: bradygaster
description: SignalR 性能
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 915fd822caae9bbcb0a688c6dd7a5b2bda12c9df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468104"
---
# <a name="signalr-performance-signalr-1x"></a><span data-ttu-id="3ab14-103">SignalR 性能 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="3ab14-103">SignalR Performance (SignalR 1.x)</span></span>

<span data-ttu-id="3ab14-104">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="3ab14-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3ab14-105">本主题介绍如何在 SignalR 应用程序中设计、度量和提高性能。</span><span class="sxs-lookup"><span data-stu-id="3ab14-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>

<span data-ttu-id="3ab14-106">有关 SignalR 性能和缩放的最新演示，请参阅[使用 ASP.NET SignalR 缩放实时 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="3ab14-107">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="3ab14-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="3ab14-108">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="3ab14-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="3ab14-109">优化 SignalR 服务器的性能</span><span class="sxs-lookup"><span data-stu-id="3ab14-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="3ab14-110">性能问题疑难解答</span><span class="sxs-lookup"><span data-stu-id="3ab14-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="3ab14-111">使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="3ab14-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="3ab14-112">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="3ab14-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="3ab14-113">其他资源</span><span class="sxs-lookup"><span data-stu-id="3ab14-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="3ab14-114">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="3ab14-114">Design considerations</span></span>

<span data-ttu-id="3ab14-115">本部分介绍在设计 SignalR 应用程序的过程中可以实现的模式，以确保不会通过生成不必要的网络流量来影响性能。</span><span class="sxs-lookup"><span data-stu-id="3ab14-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="3ab14-116">限制消息频率</span><span class="sxs-lookup"><span data-stu-id="3ab14-116">Throttling message frequency</span></span>

<span data-ttu-id="3ab14-117">即使在以高频率（如实时游戏应用程序）发送消息的应用程序中，大多数应用程序也不需要发送多条消息。</span><span class="sxs-lookup"><span data-stu-id="3ab14-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="3ab14-118">若要减少每个客户端生成的流量量，可实现消息循环，使消息循环排队并发送出比固定速率更高的消息（即，如果此时间内有消息，则每秒发送的消息数最多一次）要发送的 terval）。</span><span class="sxs-lookup"><span data-stu-id="3ab14-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="3ab14-119">有关将消息限制为特定速率（来自客户端和服务器）的示例应用程序，请参阅[使用 SignalR 的高频率实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="3ab14-120">减小消息大小</span><span class="sxs-lookup"><span data-stu-id="3ab14-120">Reducing message size</span></span>

<span data-ttu-id="3ab14-121">可以通过减小序列化对象的大小来减小 SignalR 消息的大小。</span><span class="sxs-lookup"><span data-stu-id="3ab14-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="3ab14-122">在服务器代码中，如果要发送的对象包含不需要传输的属性，则通过使用 `JsonIgnore` 属性防止这些属性被序列化。</span><span class="sxs-lookup"><span data-stu-id="3ab14-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="3ab14-123">属性的名称也存储在消息中;可以使用 `JsonProperty` 特性来缩短属性的名称。</span><span class="sxs-lookup"><span data-stu-id="3ab14-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="3ab14-124">下面的代码示例演示如何排除将某个属性发送到客户端，以及如何缩短属性名称：</span><span class="sxs-lookup"><span data-stu-id="3ab14-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="3ab14-125">**.NET 服务器代码，该代码演示了用于排除发送到客户端的数据的 JsonIgnore 特性，以及用于减小消息大小的 JsonProperty 特性**</span><span class="sxs-lookup"><span data-stu-id="3ab14-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="3ab14-126">若要在客户端代码中保留可读性/可维护性，在收到消息后，可将缩略属性名称重新映射到友好名称。</span><span class="sxs-lookup"><span data-stu-id="3ab14-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="3ab14-127">下面的代码示例演示了一种可能的方法：将缩短的名称重新映射到较长的名称，方法是定义消息协定（映射），并使用 `reMap` 函数将协定应用到优化的消息类：</span><span class="sxs-lookup"><span data-stu-id="3ab14-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="3ab14-128">**将简化的属性名称重新映射到用户可读名称的客户端 JavaScript 代码**</span><span class="sxs-lookup"><span data-stu-id="3ab14-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="3ab14-129">使用相同的方法，还可以将客户端的消息中的名称缩写给服务器。</span><span class="sxs-lookup"><span data-stu-id="3ab14-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="3ab14-130">减小消息对象的内存占用量（即用于消息的内存量）也可以提高性能。</span><span class="sxs-lookup"><span data-stu-id="3ab14-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="3ab14-131">例如，如果不需要 `int` 的完整范围，可以改为使用 `short` 或 `byte`。</span><span class="sxs-lookup"><span data-stu-id="3ab14-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="3ab14-132">由于消息存储在服务器内存中的消息总线上，因此减少消息大小也可能解决服务器内存问题。</span><span class="sxs-lookup"><span data-stu-id="3ab14-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="3ab14-133">优化 SignalR 服务器的性能</span><span class="sxs-lookup"><span data-stu-id="3ab14-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="3ab14-134">以下配置设置可用于优化服务器，以在 SignalR 应用程序中获得更好的性能。</span><span class="sxs-lookup"><span data-stu-id="3ab14-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="3ab14-135">有关如何在 ASP.NET 应用程序中提高性能的常规信息，请参阅[改善 ASP.NET 性能](https://msdn.microsoft.com/library/ff647787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="3ab14-136">**SignalR 配置设置**</span><span class="sxs-lookup"><span data-stu-id="3ab14-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="3ab14-137">**DefaultMessageBufferSize**：默认情况下，SignalR 每次连接时在内存中保留1000消息。</span><span class="sxs-lookup"><span data-stu-id="3ab14-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="3ab14-138">如果正在使用大消息，这可能会产生内存问题，可以通过减少该值来缓解此问题。</span><span class="sxs-lookup"><span data-stu-id="3ab14-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="3ab14-139">此设置可在 ASP.NET 应用程序中的 `Application_Start` 事件处理程序中设置，或在自承载应用程序的 OWIN startup 类的 `Configuration` 方法中设置。</span><span class="sxs-lookup"><span data-stu-id="3ab14-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="3ab14-140">下面的示例演示如何减小此值以便减少应用程序的内存占用量，以减少使用的服务器内存量：</span><span class="sxs-lookup"><span data-stu-id="3ab14-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="3ab14-141">**Global.asax 中用于减小默认消息缓冲区大小的 .NET server 代码**</span><span class="sxs-lookup"><span data-stu-id="3ab14-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="3ab14-142">**IIS 配置设置**</span><span class="sxs-lookup"><span data-stu-id="3ab14-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="3ab14-143">**每个应用程序的最大并发请求**数：增加并发 IIS 请求数将增加可用于为请求提供服务的服务器资源。</span><span class="sxs-lookup"><span data-stu-id="3ab14-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="3ab14-144">默认值为 5000;若要增加此设置，请在提升的命令提示符下执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3ab14-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="3ab14-145">**ASP.NET 配置设置**</span><span class="sxs-lookup"><span data-stu-id="3ab14-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="3ab14-146">本部分包含可在 `aspnet.config` 文件中设置的配置设置。</span><span class="sxs-lookup"><span data-stu-id="3ab14-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="3ab14-147">此文件位于以下两个位置之一，具体取决于平台：</span><span class="sxs-lookup"><span data-stu-id="3ab14-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="3ab14-148">可提高 SignalR 性能的 ASP.NET 设置包括：</span><span class="sxs-lookup"><span data-stu-id="3ab14-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="3ab14-149">**每 CPU 的最大并发请求**数：增加此设置可以缓解性能瓶颈。</span><span class="sxs-lookup"><span data-stu-id="3ab14-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="3ab14-150">若要增加此设置，请将以下配置设置添加到 `aspnet.config` 文件：</span><span class="sxs-lookup"><span data-stu-id="3ab14-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="3ab14-151">**请求队列限制**：当连接总数超出 `maxConcurrentRequestsPerCPU` 设置时，ASP.NET 将使用队列启动限制请求。</span><span class="sxs-lookup"><span data-stu-id="3ab14-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="3ab14-152">若要增加队列的大小，可以增加 `requestQueueLimit` 设置。</span><span class="sxs-lookup"><span data-stu-id="3ab14-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="3ab14-153">为此，请将以下配置设置添加到 `config/machine.config` 中的 `processModel` 节点（而不是 `aspnet.config`）：</span><span class="sxs-lookup"><span data-stu-id="3ab14-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="3ab14-154">性能问题故障排除</span><span class="sxs-lookup"><span data-stu-id="3ab14-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="3ab14-155">本部分介绍在应用程序中查找性能瓶颈的方法。</span><span class="sxs-lookup"><span data-stu-id="3ab14-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="3ab14-156">验证是否正在使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="3ab14-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="3ab14-157">尽管 SignalR 可以使用各种传输来实现客户端与服务器之间的通信，但 WebSocket 提供了显著的性能优势，如果客户端和服务器支持，则应使用这些传输。</span><span class="sxs-lookup"><span data-stu-id="3ab14-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="3ab14-158">若要确定客户端和服务器是否满足 WebSocket 的要求，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="3ab14-159">若要确定应用程序中使用的传输，可以使用浏览器开发人员工具，并检查日志以查看连接所使用的传输。</span><span class="sxs-lookup"><span data-stu-id="3ab14-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="3ab14-160">有关在 Internet Explorer 和 Chrome 中使用浏览器开发工具的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="3ab14-161">使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="3ab14-161">Using SignalR performance counters</span></span>

<span data-ttu-id="3ab14-162">本部分介绍如何启用和使用 `Microsoft.AspNet.SignalR.Utils` 包中找到的 SignalR 性能计数器。</span><span class="sxs-lookup"><span data-stu-id="3ab14-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="3ab14-163">安装 signalr</span><span class="sxs-lookup"><span data-stu-id="3ab14-163">Installing signalr.exe</span></span>

<span data-ttu-id="3ab14-164">可以使用名为 SignalR 的实用工具将性能计数器添加到服务器。</span><span class="sxs-lookup"><span data-stu-id="3ab14-164">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="3ab14-165">若要安装此实用程序，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3ab14-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="3ab14-166">在 Visual Studio 中，选择 "**工具**" > **Nuget 包管理器** > **管理解决方案的 NuGet 包**</span><span class="sxs-lookup"><span data-stu-id="3ab14-166">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="3ab14-167">搜索**signalr. utils**，并选择 "安装"。</span><span class="sxs-lookup"><span data-stu-id="3ab14-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="3ab14-168">接受许可协议以安装包。</span><span class="sxs-lookup"><span data-stu-id="3ab14-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="3ab14-169">SignalR 将安装到 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`。</span><span class="sxs-lookup"><span data-stu-id="3ab14-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="3ab14-170">通过 SignalR 安装性能计数器</span><span class="sxs-lookup"><span data-stu-id="3ab14-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="3ab14-171">若要安装 SignalR 性能计数器，请在提升的命令提示符中使用以下参数运行 SignalR：</span><span class="sxs-lookup"><span data-stu-id="3ab14-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="3ab14-172">若要删除 SignalR 性能计数器，请在提升的命令提示符中使用以下参数运行 SignalR：</span><span class="sxs-lookup"><span data-stu-id="3ab14-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="3ab14-173">SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="3ab14-173">SignalR Performance counters</span></span>

<span data-ttu-id="3ab14-174">实用工具包将安装下列性能计数器。</span><span class="sxs-lookup"><span data-stu-id="3ab14-174">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="3ab14-175">"Total" 计数器测量自上次应用程序池或服务器重新启动后发生的事件数。</span><span class="sxs-lookup"><span data-stu-id="3ab14-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="3ab14-176">**连接指标**</span><span class="sxs-lookup"><span data-stu-id="3ab14-176">**Connection metrics**</span></span>

<span data-ttu-id="3ab14-177">以下度量值测量发生的连接生存期事件。</span><span class="sxs-lookup"><span data-stu-id="3ab14-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="3ab14-178">有关详细信息，请参阅[了解和处理连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="3ab14-179">**连接已连接**</span><span class="sxs-lookup"><span data-stu-id="3ab14-179">**Connections Connected**</span></span>
- <span data-ttu-id="3ab14-180">**连接已重新连接**</span><span class="sxs-lookup"><span data-stu-id="3ab14-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="3ab14-181">**断开连接**</span><span class="sxs-lookup"><span data-stu-id="3ab14-181">**Connections Disconnected**</span></span>
- <span data-ttu-id="3ab14-182">**当前连接数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-182">**Connections Current**</span></span>

<span data-ttu-id="3ab14-183">**消息度量值**</span><span class="sxs-lookup"><span data-stu-id="3ab14-183">**Message metrics**</span></span>

<span data-ttu-id="3ab14-184">以下度量值测量由 SignalR 生成的消息流量。</span><span class="sxs-lookup"><span data-stu-id="3ab14-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="3ab14-185">**接收的连接消息总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="3ab14-186">**已发送的连接消息总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="3ab14-187">**每秒接收的连接消息数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="3ab14-188">**发送的连接消息/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="3ab14-189">**消息总线指标**</span><span class="sxs-lookup"><span data-stu-id="3ab14-189">**Message bus metrics**</span></span>

<span data-ttu-id="3ab14-190">以下度量值度量通过内部 SignalR 消息总线的流量，其中放置了所有传入和传出 SignalR 消息的队列。</span><span class="sxs-lookup"><span data-stu-id="3ab14-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="3ab14-191">发送或广播消息时，会将其**发布**。</span><span class="sxs-lookup"><span data-stu-id="3ab14-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="3ab14-192">在此上下文中，**订阅服务器**是对消息总线的订阅;这应该等于客户端数量加上服务器本身。</span><span class="sxs-lookup"><span data-stu-id="3ab14-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="3ab14-193">已**分配的工作线程**是将数据发送到活动连接的组件;**繁忙辅助角色**是指主动发送消息的辅助角色。</span><span class="sxs-lookup"><span data-stu-id="3ab14-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="3ab14-194">**消息总线接收消息总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="3ab14-195">**每秒接收的消息总线消息数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="3ab14-196">**消息总线消息已发布总计**</span><span class="sxs-lookup"><span data-stu-id="3ab14-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="3ab14-197">**发布的消息总线消息数/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="3ab14-198">**消息总线订阅服务器当前**</span><span class="sxs-lookup"><span data-stu-id="3ab14-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="3ab14-199">**消息总线订阅服务器总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="3ab14-200">**消息总线订阅者数/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="3ab14-201">**消息总线分配的工作线程**</span><span class="sxs-lookup"><span data-stu-id="3ab14-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="3ab14-202">**消息总线繁忙辅助角色**</span><span class="sxs-lookup"><span data-stu-id="3ab14-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="3ab14-203">**消息总线主题当前**</span><span class="sxs-lookup"><span data-stu-id="3ab14-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="3ab14-204">**错误度量值**</span><span class="sxs-lookup"><span data-stu-id="3ab14-204">**Error metrics**</span></span>

<span data-ttu-id="3ab14-205">以下度量值度量 SignalR 消息流量生成的错误。</span><span class="sxs-lookup"><span data-stu-id="3ab14-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="3ab14-206">集线器**解析**错误发生在无法解析集线器或集线器方法时。</span><span class="sxs-lookup"><span data-stu-id="3ab14-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="3ab14-207">**中心调用**错误是调用集线器方法时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="3ab14-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="3ab14-208">**传输**错误是 HTTP 请求或响应期间引发的连接错误。</span><span class="sxs-lookup"><span data-stu-id="3ab14-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="3ab14-209">**错误：全部总计**</span><span class="sxs-lookup"><span data-stu-id="3ab14-209">**Errors: All Total**</span></span>
- <span data-ttu-id="3ab14-210">**错误：全部/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="3ab14-211">**错误：集线器解析总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="3ab14-212">**错误：集线器分辨率/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="3ab14-213">**错误：集线器调用总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="3ab14-214">**错误：集线器调用数/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="3ab14-215">**错误：传输总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="3ab14-216">**错误：传输数/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="3ab14-217">**扩展指标**</span><span class="sxs-lookup"><span data-stu-id="3ab14-217">**Scaleout metrics**</span></span>

<span data-ttu-id="3ab14-218">以下度量值度量扩展提供程序生成的流量和错误。</span><span class="sxs-lookup"><span data-stu-id="3ab14-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="3ab14-219">此上下文中的**流**是扩展提供程序使用的缩放单位;如果使用 SQL Server，则这是一个表; 如果使用了服务总线，则为一个主题，如果使用了 Redis，则为一个订阅。</span><span class="sxs-lookup"><span data-stu-id="3ab14-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="3ab14-220">默认情况下，只使用一个流，但这可以通过 SQL Server 和服务总线上的配置增加。</span><span class="sxs-lookup"><span data-stu-id="3ab14-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="3ab14-221">**缓冲**流是进入出错状态的流;当流处于出错状态时，发送到底板的所有消息都将立即失败，直到流不再出错。</span><span class="sxs-lookup"><span data-stu-id="3ab14-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="3ab14-222">**发送队列长度**是已发布但尚未发送的消息数。</span><span class="sxs-lookup"><span data-stu-id="3ab14-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="3ab14-223">**扩展消息总线消息数/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="3ab14-224">**扩展流总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="3ab14-225">**扩展流打开**</span><span class="sxs-lookup"><span data-stu-id="3ab14-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="3ab14-226">**扩展流缓冲**</span><span class="sxs-lookup"><span data-stu-id="3ab14-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="3ab14-227">**扩展错误总数**</span><span class="sxs-lookup"><span data-stu-id="3ab14-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="3ab14-228">**扩展错误数/秒**</span><span class="sxs-lookup"><span data-stu-id="3ab14-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="3ab14-229">**扩展发送队列长度**</span><span class="sxs-lookup"><span data-stu-id="3ab14-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="3ab14-230">有关这些计数器度量的详细信息，请参阅[SignalR 扩展 With Azure Service Bus](scaleout-with-windows-azure-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab14-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="3ab14-231">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="3ab14-231">Using other performance counters</span></span>

<span data-ttu-id="3ab14-232">以下性能计数器对于监视应用程序的性能可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="3ab14-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="3ab14-233">**内存**</span><span class="sxs-lookup"><span data-stu-id="3ab14-233">**Memory**</span></span>

- <span data-ttu-id="3ab14-234">所有堆中的 .NET CLR 内存 # 字节（适用于 w3wp.exe）</span><span class="sxs-lookup"><span data-stu-id="3ab14-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="3ab14-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="3ab14-235">**ASP.NET**</span></span>

- <span data-ttu-id="3ab14-236">ASP. NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="3ab14-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="3ab14-237">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="3ab14-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="3ab14-238">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="3ab14-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="3ab14-239">**CPU**</span><span class="sxs-lookup"><span data-stu-id="3ab14-239">**CPU**</span></span>

- <span data-ttu-id="3ab14-240">处理器 Information\Processor 时间</span><span class="sxs-lookup"><span data-stu-id="3ab14-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="3ab14-241">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="3ab14-241">**TCP/IP**</span></span>

- <span data-ttu-id="3ab14-242">已建立 TCPv6/连接</span><span class="sxs-lookup"><span data-stu-id="3ab14-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="3ab14-243">已建立 TCPv4/连接</span><span class="sxs-lookup"><span data-stu-id="3ab14-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="3ab14-244">**Web 服务**</span><span class="sxs-lookup"><span data-stu-id="3ab14-244">**Web Service**</span></span>

- <span data-ttu-id="3ab14-245">Web Service\current connections 连接</span><span class="sxs-lookup"><span data-stu-id="3ab14-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="3ab14-246">Web Service\Maximum 连接</span><span class="sxs-lookup"><span data-stu-id="3ab14-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="3ab14-247">**线程处理**</span><span class="sxs-lookup"><span data-stu-id="3ab14-247">**Threading**</span></span>

- <span data-ttu-id="3ab14-248">当前逻辑线程\# 的 .NET CLR LocksAndThreads</span><span class="sxs-lookup"><span data-stu-id="3ab14-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="3ab14-249">.NET CLR LocksAnd 线程\# 当前物理线程</span><span class="sxs-lookup"><span data-stu-id="3ab14-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="3ab14-250">其他资源</span><span class="sxs-lookup"><span data-stu-id="3ab14-250">Other Resources</span></span>

<span data-ttu-id="3ab14-251">有关 ASP.NET 性能监视和优化的详细信息，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="3ab14-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="3ab14-252">[ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="3ab14-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="3ab14-253">IIS 7.5、IIS 7.0 和 IIS 6.0 上的 ASP.NET 线程使用情况</span><span class="sxs-lookup"><span data-stu-id="3ab14-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="3ab14-254">&lt;applicationPool&gt; 元素（Web 设置）</span><span class="sxs-lookup"><span data-stu-id="3ab14-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
