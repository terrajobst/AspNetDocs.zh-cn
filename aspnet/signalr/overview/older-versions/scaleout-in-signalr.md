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
# <a name="introduction-to-scaleout-in-signalr-1x"></a>SignalR 1.x 的横向扩展简介

作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

通常，可通过两种方式缩放 web 应用程序：*向上缩放*和向*外*缩放。

- 向上缩放意味着使用较大的服务器（或更大的 VM）和更多的 RAM、Cpu 等。
- Scale out 意味着添加更多服务器来处理负载。

向上缩放的问题是快速达到了计算机大小限制。 除此之外，还需要向外扩展。但是，当你横向扩展时，客户端可以路由到不同的服务器。 连接到一台服务器的客户端将不会接收来自其他服务器的消息。

![](scaleout-in-signalr/_static/image1.png)

一种解决方法是使用称为*底板*的组件在服务器之间转发消息。 启用底板后，每个应用程序实例会将消息发送到底板，并将其转发到其他应用程序实例。 （在电子设备中，底板是一组并行连接器。 通过类比，SignalR 背板连接多台服务器。）

![](scaleout-in-signalr/_static/image2.png)

SignalR 目前提供三个底板：

- **Azure 服务总线**。 服务总线是一种消息传递基础结构，允许组件以松散耦合的方式发送消息。
- **Redis**。 Redis 是内存中的键-值存储。 Redis 支持发布/订阅（"pub/sub"）模式来发送消息。
- **SQL Server**。 SQL Server 底板将消息写入 SQL 表中。 底板使用 Service Broker 来实现高效的消息传送。 不过，如果未启用 Service Broker，它也会起作用。

如果在 Azure 上部署应用程序，请考虑使用 Azure 服务总线底板。 如果要部署到自己的服务器场，请考虑 SQL Server 或 Redis 底板。

以下主题包含每个底板的分步教程：

- [使用 Azure 服务总线的 SignalR 横向扩展](scaleout-with-windows-azure-service-bus.md)
- [使用 Redis 的 SignalR 横向扩展](scaleout-with-redis.md)
- [使用 SQL Server 的 SignalR 横向扩展](scaleout-with-sql-server.md)

## <a name="implementation"></a>实现

在 SignalR 中，通过消息总线发送每条消息。 消息总线实现了[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，该接口提供发布/订阅抽象。 通过使用为该底板设计的总线替换默认的**IMessageBus** ，可以使用底板。 例如，Redis 的消息总线为[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，并使用 Redis [pub/sub](http://redis.io/topics/pubsub)机制来发送和接收消息。

每个服务器实例通过总线连接到底板。 发送消息时，消息会发送到底板，并且底板会将其发送到每台服务器。 当服务器从底板收到消息时，它会将该消息放入其本地缓存。 服务器随后将消息从其本地缓存传递给客户端。

对于每个客户端连接，使用游标跟踪客户端读取消息流的进度。 （游标表示消息流中的位置。）如果客户端断开连接，然后重新连接，则它会向该客户端请求到达客户端游标值之后的所有消息。 当连接使用[长轮询](../getting-started/introduction-to-signalr.md#transports)时，会发生相同的情况。 长时间轮询请求完成后，客户端将打开一个新连接，并请求到达光标之后的消息。

即使在重新连接时将客户端路由到不同的服务器，也可以使用游标机制。 该底板可识别所有服务器，客户端连接到哪个服务器无关紧要。

## <a name="limitations"></a>限制

使用底板时，最大消息吞吐量低于客户端直接与单服务器节点对话的时间。 这是因为底板会将每条消息转发到每个节点，因此底板可能成为瓶颈。 此限制是否是问题取决于应用程序。 例如，下面是一些典型的 SignalR 方案：

- [服务器广播](tutorial-server-broadcast-with-aspnet-signalr.md)（例如，股票行情）：对于此方案，背板工作良好，因为服务器控制发送消息的速率。
- [客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）：在这种情况下，如果消息数量随客户端数量的增加，则底板可能是瓶颈;也就是说，如果随着更多客户端的加入，消息的速率会按比例增加。
- [高频实时](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）：不建议在此方案中使用底板。

## <a name="enabling-tracing-for-signalr-scaleout"></a>为 SignalR 扩展启用跟踪

若要启用对底板的跟踪，请将以下部分添加到 web.config 文件中的根**配置**元素下面：

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
