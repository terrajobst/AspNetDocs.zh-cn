---
uid: signalr/overview/performance/scaleout-in-signalr
title: SignalR 中的扩展简介 |Microsoft Docs
author: bradygaster
description: 本主题中使用的软件版本 Visual Studio 2013 .NET 4.5 SignalR 版本2本主题的早期版本。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14dc22f99a43b566903c59fb23b7d419350f4a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467780"
---
# <a name="introduction-to-scaleout-in-signalr"></a><span data-ttu-id="9120c-103">SignalR 的横向扩展简介</span><span class="sxs-lookup"><span data-stu-id="9120c-103">Introduction to Scaleout in SignalR</span></span>

<span data-ttu-id="9120c-104">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="9120c-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="9120c-105">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="9120c-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="9120c-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9120c-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="9120c-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9120c-107">.NET 4.5</span></span>
> - <span data-ttu-id="9120c-108">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="9120c-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="9120c-109">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="9120c-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="9120c-110">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="9120c-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="9120c-111">问题和注释</span><span class="sxs-lookup"><span data-stu-id="9120c-111">Questions and comments</span></span>
>
> <span data-ttu-id="9120c-112">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="9120c-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="9120c-113">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="9120c-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="9120c-114">通常，可通过两种方式缩放 web 应用程序：*向上缩放*和向*外*缩放。</span><span class="sxs-lookup"><span data-stu-id="9120c-114">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="9120c-115">向上缩放意味着使用较大的服务器（或更大的 VM）和更多的 RAM、Cpu 等。</span><span class="sxs-lookup"><span data-stu-id="9120c-115">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="9120c-116">Scale out 意味着添加更多服务器来处理负载。</span><span class="sxs-lookup"><span data-stu-id="9120c-116">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="9120c-117">向上缩放的问题是快速达到了计算机大小限制。</span><span class="sxs-lookup"><span data-stu-id="9120c-117">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="9120c-118">除此之外，还需要向外扩展。但是，当你横向扩展时，客户端可以路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="9120c-118">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="9120c-119">连接到一台服务器的客户端将不会接收来自其他服务器的消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-119">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="9120c-120">一种解决方法是使用称为*底板*的组件在服务器之间转发消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-120">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="9120c-121">启用底板后，每个应用程序实例会将消息发送到底板，并将其转发到其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="9120c-121">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="9120c-122">（在电子设备中，底板是一组并行连接器。</span><span class="sxs-lookup"><span data-stu-id="9120c-122">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="9120c-123">通过类比，SignalR 背板连接多台服务器。）</span><span class="sxs-lookup"><span data-stu-id="9120c-123">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="9120c-124">SignalR 目前提供三个底板：</span><span class="sxs-lookup"><span data-stu-id="9120c-124">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="9120c-125">**Azure 服务总线**。</span><span class="sxs-lookup"><span data-stu-id="9120c-125">**Azure Service Bus**.</span></span> <span data-ttu-id="9120c-126">服务总线是一种消息传递基础结构，允许组件以松散耦合的方式发送消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-126">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="9120c-127">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="9120c-127">**Redis**.</span></span> <span data-ttu-id="9120c-128">Redis 是内存中的键-值存储。</span><span class="sxs-lookup"><span data-stu-id="9120c-128">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="9120c-129">Redis 支持发布/订阅（"pub/sub"）模式来发送消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-129">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="9120c-130">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="9120c-130">**SQL Server**.</span></span> <span data-ttu-id="9120c-131">SQL Server 底板将消息写入 SQL 表中。</span><span class="sxs-lookup"><span data-stu-id="9120c-131">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="9120c-132">底板使用 Service Broker 来实现高效的消息传送。</span><span class="sxs-lookup"><span data-stu-id="9120c-132">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="9120c-133">不过，如果未启用 Service Broker，它也会起作用。</span><span class="sxs-lookup"><span data-stu-id="9120c-133">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="9120c-134">如果在 Azure 上部署应用程序，请考虑使用[Azure Redis 缓存](https://azure.microsoft.com/services/cache/)的 Redis 底板。</span><span class="sxs-lookup"><span data-stu-id="9120c-134">If you deploy your application on Azure, consider using the Redis backplane using [Azure Redis Cache](https://azure.microsoft.com/services/cache/).</span></span> <span data-ttu-id="9120c-135">如果要部署到自己的服务器场，请考虑 SQL Server 或 Redis 底板。</span><span class="sxs-lookup"><span data-stu-id="9120c-135">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="9120c-136">以下主题包含每个底板的分步教程：</span><span class="sxs-lookup"><span data-stu-id="9120c-136">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="9120c-137">使用 Azure 服务总线的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="9120c-137">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="9120c-138">使用 Redis 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="9120c-138">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="9120c-139">使用 SQL Server 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="9120c-139">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="9120c-140">实现</span><span class="sxs-lookup"><span data-stu-id="9120c-140">Implementation</span></span>

<span data-ttu-id="9120c-141">在 SignalR 中，通过消息总线发送每条消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-141">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="9120c-142">消息总线实现了[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，该接口提供发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="9120c-142">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="9120c-143">通过使用为该底板设计的总线替换默认的**IMessageBus** ，可以使用底板。</span><span class="sxs-lookup"><span data-stu-id="9120c-143">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="9120c-144">例如，Redis 的消息总线为[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，并使用 Redis [pub/sub](http://redis.io/topics/pubsub)机制来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-144">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="9120c-145">每个服务器实例通过总线连接到底板。</span><span class="sxs-lookup"><span data-stu-id="9120c-145">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="9120c-146">发送消息时，消息会发送到底板，并且底板会将其发送到每台服务器。</span><span class="sxs-lookup"><span data-stu-id="9120c-146">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="9120c-147">当服务器从底板收到消息时，它会将该消息放入其本地缓存。</span><span class="sxs-lookup"><span data-stu-id="9120c-147">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="9120c-148">服务器随后将消息从其本地缓存传递给客户端。</span><span class="sxs-lookup"><span data-stu-id="9120c-148">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="9120c-149">对于每个客户端连接，使用游标跟踪客户端读取消息流的进度。</span><span class="sxs-lookup"><span data-stu-id="9120c-149">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="9120c-150">（游标表示消息流中的位置。）如果客户端断开连接，然后重新连接，则它会向该客户端请求到达客户端游标值之后的所有消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-150">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="9120c-151">当连接使用[长轮询](../getting-started/introduction-to-signalr.md#transports)时，会发生相同的情况。</span><span class="sxs-lookup"><span data-stu-id="9120c-151">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="9120c-152">长时间轮询请求完成后，客户端将打开一个新连接，并请求到达光标之后的消息。</span><span class="sxs-lookup"><span data-stu-id="9120c-152">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="9120c-153">即使在重新连接时将客户端路由到不同的服务器，也可以使用游标机制。</span><span class="sxs-lookup"><span data-stu-id="9120c-153">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="9120c-154">该底板可识别所有服务器，客户端连接到哪个服务器无关紧要。</span><span class="sxs-lookup"><span data-stu-id="9120c-154">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="9120c-155">限制</span><span class="sxs-lookup"><span data-stu-id="9120c-155">Limitations</span></span>

<span data-ttu-id="9120c-156">使用底板时，最大消息吞吐量低于客户端直接与单服务器节点对话的时间。</span><span class="sxs-lookup"><span data-stu-id="9120c-156">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="9120c-157">这是因为底板会将每条消息转发到每个节点，因此底板可能成为瓶颈。</span><span class="sxs-lookup"><span data-stu-id="9120c-157">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="9120c-158">此限制是否是问题取决于应用程序。</span><span class="sxs-lookup"><span data-stu-id="9120c-158">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="9120c-159">例如，下面是一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="9120c-159">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="9120c-160">[服务器广播](../getting-started/tutorial-server-broadcast-with-signalr.md)（例如，股票行情）：对于此方案，背板工作良好，因为服务器控制发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="9120c-160">[Server broadcast](../getting-started/tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="9120c-161">[客户端到客户端](../getting-started/tutorial-getting-started-with-signalr.md)（如聊天）：在这种情况下，如果消息数量随客户端数量的增加，则底板可能是瓶颈;也就是说，如果随着更多客户端的加入，消息的速率会按比例增加。</span><span class="sxs-lookup"><span data-stu-id="9120c-161">[Client-to-client](../getting-started/tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="9120c-162">[高频实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）：不建议在此方案中使用底板。</span><span class="sxs-lookup"><span data-stu-id="9120c-162">[High-frequency realtime](../getting-started/tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="9120c-163">为 SignalR 扩展启用跟踪</span><span class="sxs-lookup"><span data-stu-id="9120c-163">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="9120c-164">若要启用对底板的跟踪，请将以下部分添加到 web.config 文件中的根**配置**元素下面：</span><span class="sxs-lookup"><span data-stu-id="9120c-164">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
