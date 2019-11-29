---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: 以队列为中心的工作模式（使用 Azure 生成实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: c73b070f11366e781bcea70ffc84fd49a47d469a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582763"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>以队列为中心的工作模式（使用 Azure 生成实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

以前，我们发现，使用多个服务可能会导致 "复合" SLA，其中应用的有效 SLA 是各个 Sla 的*产品*。 例如，Fix It 应用使用网站、存储和 SQL 数据库。 如果这些服务中有任何一个失败，应用将向用户返回错误。

缓存是处理只读内容的暂时性故障的好方法。 但如果您的应用程序需要执行工作，该怎么办？ 例如，当用户提交新的 Fix It 任务时，应用程序不能只是将任务放入缓存中。 应用需要将 Fix It 任务写入永久性数据存储中，以便可以对其进行处理。

这就是以队列为中心的工作模式。 此模式允许在 web 层和后端服务之间进行松散耦合。

下面是该模式的工作方式。 当应用程序收到请求时，它会将工作项放入队列，并立即返回响应。 然后，单独的后端进程将从队列中提取工作项并执行工作。

以队列为中心的工作模式适用于：

- 耗费时间（高延迟）的工作。
- 需要外部服务的工作可能并非始终可用。
- 占用大量资源（高 CPU）的工作。
- 可以受益于费率评分（遭受突发负载猝发）的工作。

## <a name="reduced-latency"></a>减少延迟

每次执行耗时的工作时，队列都非常有用。 如果任务花费几秒钟或更长时间，而不是阻止最终用户，请将工作项放入队列中。 告诉用户 "我们正在处理该用户"，然后使用队列侦听器在后台处理该任务。

例如，在联机零售商处购买物品时，网站会立即确认订单。 但这并不意味着您的内容已在交付卡车中。 它们将任务放入队列中，并在后台执行信用检查、准备要装运的项目等。

对于具有较短延迟的方案，与以同步方式执行任务相比，总的端到端时间可能会更长。 但即便如此，其他优点也可能超过该缺点。

## <a name="increased-reliability"></a>提高了可靠性

在此版本中，我们一直在查看到目前为止，web 前端与 SQL 数据库后端紧密耦合。 如果 SQL 数据库服务不可用，则用户会收到错误消息。 如果重试不起作用（也就是说，故障不是暂时性的），则唯一可以执行的操作是显示错误，并要求用户稍后再试一次。

![显示 SQL 数据库后端失败时 web 前端失败的关系图](queue-centric-work-pattern/_static/image1.png)

使用队列时，当用户提交 Fix It 任务时，应用程序会将消息写入队列。 消息负载是任务的[JSON](http://json.org/)表示形式。 将消息写入队列后，应用会立即返回并立即向用户显示一条成功消息。

如果任何后端服务（如 SQL 数据库或队列侦听器）脱机，则用户仍然可以提交新的 Fix It 任务。 消息只会排队等候，直到后端服务再次可用。 此时，即将出现积压工作（backlog）的后端服务。

![显示出现 SQL 数据库错误时 web 前端继续运行的关系图](queue-centric-work-pattern/_static/image2.png)

而且，现在你可以添加更多后端逻辑，而无需担心前端的复原能力。 例如，你可能想要在分配新的修补程序时向所有者发送一封电子邮件或短信。 如果电子邮件或短信服务变得不可用，你可以处理所有其他内容，然后将消息放入单独的队列中，以便发送电子邮件/短信消息。

以前，我们有效的 SLA 是 &times; 存储 &times; SQL 数据库的 Web 应用 = 99.7%。 （请参阅[设计以经受故障](design-to-survive-failures.md)。）

当我们将应用程序更改为使用队列时，web 前端仅依赖于 Web 应用和存储，用于99.8% 的复合 SLA。 （请注意，队列是 Azure 存储服务的一部分，因此，它们包含在与 blob 存储相同的 SLA 中。）

如果你甚至需要更好于99.8%，则可以在两个不同的区域中创建两个队列。 将一个指定为主节点，将另一个作为辅助副本。 在应用中，如果主队列不可用，则故障转移到辅助队列。 同时无法同时使用的可能性非常小。

## <a name="rate-leveling-and-independent-scaling"></a>分级调配和独立缩放

队列还适用于称为*速率调节*或*负载分级*的内容。

Web 应用通常容易遭受流量突发。 尽管可以使用自动缩放来自动添加 web 服务器来处理增加的 web 流量，但自动缩放可能无法快速响应，以致无法处理负载突然高峰。 如果 web 服务器可以通过将消息写入队列来卸载其中的某些工作，则它们可以处理更多流量。 然后，后端服务可以从队列中读取消息并对其进行处理。 当传入负载变化时，队列的深度将增大或缩小。

由于很多情况下都在关闭到后端服务的工作，web 层可以更轻松地响应突发流量高峰。 你可以节省资金，因为任何给定数量的流量都可以通过较少的 web 服务器进行处理。

你可以独立缩放 web 层和后端服务。 例如，你可能需要三个 web 服务器，但只有一个服务器处理队列消息。 或者，如果是在后台运行需要进行大量计算的任务，可能需要更多后端服务器。

![](queue-centric-work-pattern/_static/image3.png)

自动缩放适用于后端服务以及 web 层。 您可以根据后端 Vm 的 CPU 使用情况，增加或减少正在处理队列中任务的 Vm 的数量。 也可以根据队列中的项数自动缩放。 例如，可以指示自动缩放尝试在队列中保留的项不超过10个。 如果队列包含10个以上的项，自动缩放将添加 Vm。 当他们追赶时，自动缩放将细分额外的 Vm。

## <a name="adding-queues-to-the-fix-it-application"></a>将队列添加到 Fix It 应用程序

若要实现队列模式，需要对 Fix It 应用进行两次更改。

- 当用户提交新的 Fix It 任务时，将该任务放置在队列中，而不是将其写入数据库。
- 创建一个后端服务，该服务处理队列中的消息。

对于队列，我们将使用[Azure 队列存储服务](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)。 另一种方法是使用[Azure 服务总线](https://docs.microsoft.com/azure/service-bus/)。

若要确定要使用的队列服务，请考虑应用需要如何发送和接收队列中的消息：

- 如果你有合作方和竞争使用者，请考虑使用 Azure 队列存储服务。 "协作发生器" 指的是将消息添加到队列的多个进程。 "竞争使用者" 是指多个进程将消息从队列中提取出来以进行处理，但任何给定的消息只能由一个 "使用者" 处理。 如果你需要更多的吞吐量，而不能使用单个队列，请使用其他队列和/或其他存储帐户。
- 如果需要[发布/订阅模型](http://en.wikipedia.org/wiki/Publish/subscribe)，请考虑使用 Azure 服务总线队列。

Fix It 应用适合合作的创建者和竞争使用者模型。

还有一个需要考虑的应用程序可用性。 队列存储服务是用于 blob 存储的同一服务的一部分，因此使用它对 SLA 没有影响。 Azure 服务总线是一个独立的服务，它具有自己的 SLA。 如果我们使用了服务总线队列，则必须考虑额外的 SLA 百分比，而我们的复合 SLA 会降低。 选择队列服务时，请确保了解你选择的应用程序可用性的影响。 有关详细信息，请参阅[Resources](#resources)部分。

## <a name="creating-queue-messages"></a>创建队列消息

若要在队列中放置 Fix It 任务，web 前端执行以下步骤：

1. 创建[CloudQueueClient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx)实例。 `CloudQueueClient` 实例用于对队列服务执行请求。
2. 如果该队列尚不存在，请创建它。
3. 序列化 Fix It 任务。
4. 调用[CloudQueue AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx)将消息放到队列中。

我们会在新 `FixItQueueManager` 类的构造函数和 `SendMessageAsync` 方法中执行此操作。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

此处，我们使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)库将 fix it 序列化为 Json 格式。 您可以使用您喜欢的任何序列化方法。 JSON 的优点是用户可读，但不如 XML 更复杂。

生产质量代码将添加错误处理逻辑、在数据库不可用时暂停、更干净地处理恢复、在应用程序启动时创建队列，以及管理 "[病毒" 消息](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)。 （病毒消息是因为某种原因而无法处理的消息。 不希望病毒消息驻留在队列中，辅助角色将继续尝试处理它们、失败、重试、失败等。

在前端 MVC 应用程序中，我们需要更新创建新任务的代码。 不要将任务放入存储库中，而是调用上面所示的 `SendMessageAsync` 方法。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>处理队列消息

若要在队列中处理消息，我们将创建后端服务。 后端服务将运行一个无限循环，该循环执行以下步骤：

1. 获取队列中的下一条消息。
2. 将消息反序列化为 Fix It task。
3. 将 Fix It 任务写入数据库。

为了托管后端服务，我们将创建一个包含*辅助角色*的 Azure 云服务。 辅助角色包含一个或多个可执行后端处理的 Vm。 在这些 Vm 中运行的代码会在队列可用时从队列中提取消息。 对于每条消息，我们将反序列化 JSON 有效负载，并使用之前在 web 层中使用的相同存储库将 Fix It Task 实体的实例写入数据库。

以下步骤演示如何将辅助角色项目添加到具有标准 web 项目的解决方案。 这些步骤已经在可下载的 Fix It 项目中完成。

首先，将云服务项目添加到 Visual Studio 解决方案。 右键单击该解决方案，然后依次选择 "**添加**"、"**新建项目**"。 在左侧窗格中，展开 **" C#视觉对象**"，然后选择 "**云**"。

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

在 "**新建 Azure 云服务**" 对话框的左窗格中，展开 "**视觉对象C#**  " 节点。 选择 "**辅助角色**"，然后单击右箭头图标。

![](queue-centric-work-pattern/_static/image6.png)

（请注意，你还可以添加一个*web 角色*。 我们可以在同一云服务中运行修补程序前端，而不是在 Azure 网站中运行。 这在前端和后端之间的连接变得更加容易协调。 不过，为了简单起见，我们将前端保存在一个 Azure App Service 的 Web 应用中，并仅在云服务中运行后端。）

默认名称将分配给辅助角色。 若要更改名称，请将鼠标悬停在右窗格中的辅助角色上，并单击铅笔图标。

![](queue-centric-work-pattern/_static/image7.png)

单击 **"确定"** 以完成对话框。 这会将两个项目添加到 Visual Studio 解决方案中。

- 定义云服务（包括配置信息）的 Azure 项目。
- 定义辅助角色的辅助角色项目。

![](queue-centric-work-pattern/_static/image8.png)

有关详细信息，请参阅[使用 Visual Studio 创建 Azure 项目。](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)

在辅助角色中，我们通过调用前面看到的 `FixItQueueManager` 类的 `ProcessMessageAsync` 方法来轮询消息。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync` 方法将检查是否存在等待的消息。 如果有一个，则会将消息反序列化为一个 `FixItTask` 实体，并将该实体保存在数据库中。 它会循环，直到队列为空。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

轮询队列消息会产生较小的事务费用，因此，当没有消息等待处理时，辅助角色的 `RunAsync` 方法将等待一秒钟，然后通过调用 `Task.Delay(1000)`再次轮询。

在 web 项目中，添加异步代码可以自动提高性能，因为 IIS 会管理有限的线程池。 辅助角色项目中不会出现这种情况。 若要改善辅助角色的可伸缩性，可以编写多线程代码或使用异步代码来实现[并行编程](https://msdn.microsoft.com/library/ff963553.aspx)。 该示例不实现并行编程，而是演示如何使代码异步，以便实现并行编程。

## <a name="summary"></a>总结

在本章中，你已了解如何通过实现以队列为中心的工作模式来提高应用程序的响应能力、可靠性和可伸缩性。

这是此电子书中涵盖的13个模式的最后一部分，但还有许多其他模式和实践可帮助你构建成功的云应用。 [最后一章](more-patterns-and-guidance.md)提供了一些链接，这些链接指向13个模式中尚未介绍的主题的资源。

<a id="resources"></a>
## <a name="resources"></a>资源

有关队列的详细信息，请参阅以下资源。

文档：

- [Microsoft Azure 存储队列第1部分：入门](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-storage-queues-part-1-getting-started/)。 按罗马字 Schacherl 的文章。
- [执行后台任务](https://msdn.microsoft.com/library/ff803365.aspx)，[将应用程序移到云中第5章，第](https://msdn.microsoft.com/library/ff728592.aspx)5 章是 Microsoft 模式和实践。 （特别是["使用 Azure 存储队列"](https://msdn.microsoft.com/library/ff803365.aspx#sec7)一节。）
- [在 Azure 上最大限度地提高基于队列的消息传送解决方案的可伸缩性和成本效益的最佳实践](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx)。 白皮书： Valery Mizonov。
- [比较 Azure 队列和服务总线队列](https://msdn.microsoft.com/magazine/jj159884.aspx)。 MSDN 杂志文章提供了可帮助你选择要使用的队列服务的其他信息。 本文提及服务总线依赖于 ACS 进行身份验证，这意味着当 ACS 不可用时，你的 SB 队列将不可用。 不过，自从编写本文后，SB 已更改，使你可以使用[SAS 令牌](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx)作为 ACS 的替代方法。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅异步消息传递入门，管道和筛选器模式，补偿事务模式，争用使用者模式，CQRS 模式。
- [CQRS 旅程](https://msdn.microsoft.com/library/jj554200)。 有关 CQRS 的电子书（由 Microsoft 模式和实践）。

视频：

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分视频系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景是通过 Microsoft 客户咨询团队（CAT）的实际客户体验。 有关 Azure 存储服务和队列的简介，请参阅从35:13 开始的剧集5。

> [!div class="step-by-step"]
> [上一页](distributed-caching.md)
> [下一页](more-patterns-and-guidance.md)
