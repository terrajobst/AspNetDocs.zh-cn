---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: SignalR 1.x 中的扩展简介 |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9bad72d31a0ebc491910ebb128b3b3a7fb537958
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431210"
---
# <a name="introduction-to-scaleout-in-signalr-1x"></a><span data-ttu-id="9822a-102">SignalR 1.x 的横向扩展简介</span><span class="sxs-lookup"><span data-stu-id="9822a-102">Introduction to Scaleout in SignalR 1.x</span></span>

<span data-ttu-id="9822a-103">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="9822a-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="9822a-104">通常，可通过两种方式缩放 web 应用程序：*向上缩放*和向*外*缩放。</span><span class="sxs-lookup"><span data-stu-id="9822a-104">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="9822a-105">向上缩放意味着使用较大的服务器（或更大的 VM）和更多的 RAM、Cpu 等。</span><span class="sxs-lookup"><span data-stu-id="9822a-105">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="9822a-106">Scale out 意味着添加更多服务器来处理负载。</span><span class="sxs-lookup"><span data-stu-id="9822a-106">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="9822a-107">向上缩放的问题是快速达到了计算机大小限制。</span><span class="sxs-lookup"><span data-stu-id="9822a-107">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="9822a-108">除此之外，还需要向外扩展。但是，当你横向扩展时，客户端可以路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="9822a-108">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="9822a-109">连接到一台服务器的客户端将不会接收来自其他服务器的消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-109">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="9822a-110">一种解决方法是使用称为*底板*的组件在服务器之间转发消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-110">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="9822a-111">启用底板后，每个应用程序实例会将消息发送到底板，并将其转发到其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="9822a-111">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="9822a-112">（在电子设备中，底板是一组并行连接器。</span><span class="sxs-lookup"><span data-stu-id="9822a-112">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="9822a-113">通过类比，SignalR 背板连接多台服务器。）</span><span class="sxs-lookup"><span data-stu-id="9822a-113">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="9822a-114">SignalR 目前提供三个底板：</span><span class="sxs-lookup"><span data-stu-id="9822a-114">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="9822a-115">**Azure 服务总线**。</span><span class="sxs-lookup"><span data-stu-id="9822a-115">**Azure Service Bus**.</span></span> <span data-ttu-id="9822a-116">服务总线是一种消息传递基础结构，允许组件以松散耦合的方式发送消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-116">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="9822a-117">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="9822a-117">**Redis**.</span></span> <span data-ttu-id="9822a-118">Redis 是内存中的键-值存储。</span><span class="sxs-lookup"><span data-stu-id="9822a-118">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="9822a-119">Redis 支持发布/订阅（"pub/sub"）模式来发送消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-119">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="9822a-120">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="9822a-120">**SQL Server**.</span></span> <span data-ttu-id="9822a-121">SQL Server 底板将消息写入 SQL 表中。</span><span class="sxs-lookup"><span data-stu-id="9822a-121">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="9822a-122">底板使用 Service Broker 来实现高效的消息传送。</span><span class="sxs-lookup"><span data-stu-id="9822a-122">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="9822a-123">不过，如果未启用 Service Broker，它也会起作用。</span><span class="sxs-lookup"><span data-stu-id="9822a-123">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="9822a-124">如果在 Azure 上部署应用程序，请考虑使用 Azure 服务总线底板。</span><span class="sxs-lookup"><span data-stu-id="9822a-124">If you deploy your application on Azure, consider using the Azure Service Bus backplane.</span></span> <span data-ttu-id="9822a-125">如果要部署到自己的服务器场，请考虑 SQL Server 或 Redis 底板。</span><span class="sxs-lookup"><span data-stu-id="9822a-125">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="9822a-126">以下主题包含每个底板的分步教程：</span><span class="sxs-lookup"><span data-stu-id="9822a-126">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="9822a-127">使用 Azure 服务总线的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="9822a-127">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="9822a-128">使用 Redis 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="9822a-128">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="9822a-129">使用 SQL Server 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="9822a-129">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="9822a-130">实现</span><span class="sxs-lookup"><span data-stu-id="9822a-130">Implementation</span></span>

<span data-ttu-id="9822a-131">在 SignalR 中，通过消息总线发送每条消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-131">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="9822a-132">消息总线实现了[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，该接口提供发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="9822a-132">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="9822a-133">通过使用为该底板设计的总线替换默认的**IMessageBus** ，可以使用底板。</span><span class="sxs-lookup"><span data-stu-id="9822a-133">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="9822a-134">例如，Redis 的消息总线为[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，并使用 Redis [pub/sub](http://redis.io/topics/pubsub)机制来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-134">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="9822a-135">每个服务器实例通过总线连接到底板。</span><span class="sxs-lookup"><span data-stu-id="9822a-135">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="9822a-136">发送消息时，消息会发送到底板，并且底板会将其发送到每台服务器。</span><span class="sxs-lookup"><span data-stu-id="9822a-136">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="9822a-137">当服务器从底板收到消息时，它会将该消息放入其本地缓存。</span><span class="sxs-lookup"><span data-stu-id="9822a-137">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="9822a-138">服务器随后将消息从其本地缓存传递给客户端。</span><span class="sxs-lookup"><span data-stu-id="9822a-138">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="9822a-139">对于每个客户端连接，使用游标跟踪客户端读取消息流的进度。</span><span class="sxs-lookup"><span data-stu-id="9822a-139">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="9822a-140">（游标表示消息流中的位置。）如果客户端断开连接，然后重新连接，则它会向该客户端请求到达客户端游标值之后的所有消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-140">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="9822a-141">当连接使用[长轮询](../getting-started/introduction-to-signalr.md#transports)时，会发生相同的情况。</span><span class="sxs-lookup"><span data-stu-id="9822a-141">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="9822a-142">长时间轮询请求完成后，客户端将打开一个新连接，并请求到达光标之后的消息。</span><span class="sxs-lookup"><span data-stu-id="9822a-142">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="9822a-143">即使在重新连接时将客户端路由到不同的服务器，也可以使用游标机制。</span><span class="sxs-lookup"><span data-stu-id="9822a-143">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="9822a-144">该底板可识别所有服务器，客户端连接到哪个服务器无关紧要。</span><span class="sxs-lookup"><span data-stu-id="9822a-144">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="9822a-145">限制</span><span class="sxs-lookup"><span data-stu-id="9822a-145">Limitations</span></span>

<span data-ttu-id="9822a-146">使用底板时，最大消息吞吐量低于客户端直接与单服务器节点对话的时间。</span><span class="sxs-lookup"><span data-stu-id="9822a-146">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="9822a-147">这是因为底板会将每条消息转发到每个节点，因此底板可能成为瓶颈。</span><span class="sxs-lookup"><span data-stu-id="9822a-147">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="9822a-148">此限制是否是问题取决于应用程序。</span><span class="sxs-lookup"><span data-stu-id="9822a-148">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="9822a-149">例如，下面是一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="9822a-149">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="9822a-150">[服务器广播](tutorial-server-broadcast-with-aspnet-signalr.md)（例如，股票行情）：对于此方案，背板工作良好，因为服务器控制发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="9822a-150">[Server broadcast](tutorial-server-broadcast-with-aspnet-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="9822a-151">[客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）：在这种情况下，如果消息数量随客户端数量的增加，则底板可能是瓶颈;也就是说，如果随着更多客户端的加入，消息的速率会按比例增加。</span><span class="sxs-lookup"><span data-stu-id="9822a-151">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="9822a-152">[高频实时](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）：不建议在此方案中使用底板。</span><span class="sxs-lookup"><span data-stu-id="9822a-152">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="9822a-153">为 SignalR 扩展启用跟踪</span><span class="sxs-lookup"><span data-stu-id="9822a-153">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="9822a-154">若要启用对底板的跟踪，请将以下部分添加到 web.config 文件中的根**配置**元素下面：</span><span class="sxs-lookup"><span data-stu-id="9822a-154">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
