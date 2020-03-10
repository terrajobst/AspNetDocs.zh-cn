---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: 将 SignalR 用户映射到 SignalR 1.x 中的连接 |Microsoft Docs
author: bradygaster
description: 本主题说明如何保留有关用户及其连接的信息。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449996"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="49e8f-103">在 SignalR 1.x 中将 SignalR 用户映射到连接</span><span class="sxs-lookup"><span data-stu-id="49e8f-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="49e8f-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="49e8f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="49e8f-105">本主题说明如何保留有关用户及其连接的信息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="49e8f-106">简介</span><span class="sxs-lookup"><span data-stu-id="49e8f-106">Introduction</span></span>

<span data-ttu-id="49e8f-107">连接到中心的每个客户端传递唯一的连接 id。可以在中心上下文的 `Context.ConnectionId` 属性中检索此值。</span><span class="sxs-lookup"><span data-stu-id="49e8f-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="49e8f-108">如果你的应用程序需要将用户映射到连接 id 并保留该映射，则可以使用以下项之一：</span><span class="sxs-lookup"><span data-stu-id="49e8f-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="49e8f-109">[内存中存储](#inmemory)，如字典</span><span class="sxs-lookup"><span data-stu-id="49e8f-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="49e8f-110">每个用户的 SignalR 组</span><span class="sxs-lookup"><span data-stu-id="49e8f-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="49e8f-111">[永久、外部存储](#database)（如数据库表或 Azure 表存储）</span><span class="sxs-lookup"><span data-stu-id="49e8f-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="49e8f-112">本主题中显示了每个实现。</span><span class="sxs-lookup"><span data-stu-id="49e8f-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="49e8f-113">使用 `Hub` 类的 `OnConnected`、`OnDisconnected`和 `OnReconnected` 方法跟踪用户连接状态。</span><span class="sxs-lookup"><span data-stu-id="49e8f-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="49e8f-114">应用程序的最佳方法取决于：</span><span class="sxs-lookup"><span data-stu-id="49e8f-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="49e8f-115">承载应用程序的 web 服务器的数量。</span><span class="sxs-lookup"><span data-stu-id="49e8f-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="49e8f-116">是否需要获取当前连接的用户的列表。</span><span class="sxs-lookup"><span data-stu-id="49e8f-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="49e8f-117">应用程序或服务器重新启动时是否需要保留组和用户信息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="49e8f-118">调用外部服务器的延迟是否存在问题。</span><span class="sxs-lookup"><span data-stu-id="49e8f-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="49e8f-119">下表显示了适用于这些注意事项的方法。</span><span class="sxs-lookup"><span data-stu-id="49e8f-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="49e8f-120">多个服务器</span><span class="sxs-lookup"><span data-stu-id="49e8f-120">More than one server</span></span> | <span data-ttu-id="49e8f-121">获取当前连接的用户的列表</span><span class="sxs-lookup"><span data-stu-id="49e8f-121">Get list of currently connected users</span></span> | <span data-ttu-id="49e8f-122">重新启动后保留信息</span><span class="sxs-lookup"><span data-stu-id="49e8f-122">Persist information after restarts</span></span> | <span data-ttu-id="49e8f-123">最佳性能</span><span class="sxs-lookup"><span data-stu-id="49e8f-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="49e8f-124">内存中</span><span class="sxs-lookup"><span data-stu-id="49e8f-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="49e8f-125">单用户组</span><span class="sxs-lookup"><span data-stu-id="49e8f-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="49e8f-126">永久、外部</span><span class="sxs-lookup"><span data-stu-id="49e8f-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="49e8f-127">内存中存储</span><span class="sxs-lookup"><span data-stu-id="49e8f-127">In-memory storage</span></span>

<span data-ttu-id="49e8f-128">下面的示例演示如何在存储在内存中的字典中保留连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="49e8f-129">字典使用 `HashSet` 来存储连接 id。用户随时可以与 SignalR 应用程序建立多个连接。</span><span class="sxs-lookup"><span data-stu-id="49e8f-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="49e8f-130">例如，通过多个设备或多个浏览器选项卡连接的用户将拥有多个连接 id。</span><span class="sxs-lookup"><span data-stu-id="49e8f-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="49e8f-131">如果应用程序关闭，所有信息都将丢失，但会在用户重新建立连接时重新填充。</span><span class="sxs-lookup"><span data-stu-id="49e8f-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="49e8f-132">如果你的环境包含多个 web 服务器，则内存中存储不起作用，因为每个服务器都有一个单独的连接集合。</span><span class="sxs-lookup"><span data-stu-id="49e8f-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="49e8f-133">第一个示例演示一个类，该类管理用户到连接的映射。</span><span class="sxs-lookup"><span data-stu-id="49e8f-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="49e8f-134">HashSet 的密钥将是用户的名称。</span><span class="sxs-lookup"><span data-stu-id="49e8f-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="49e8f-135">下一个示例演示如何从集线器使用连接映射类。</span><span class="sxs-lookup"><span data-stu-id="49e8f-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="49e8f-136">类的实例存储在变量名称 `_connections`中。</span><span class="sxs-lookup"><span data-stu-id="49e8f-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="49e8f-137">单用户组</span><span class="sxs-lookup"><span data-stu-id="49e8f-137">Single-user groups</span></span>

<span data-ttu-id="49e8f-138">你可以为每个用户创建一个组，然后在你只需要访问该用户时向该组发送一条消息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="49e8f-139">每个组的名称是用户的名称。</span><span class="sxs-lookup"><span data-stu-id="49e8f-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="49e8f-140">如果用户有多个连接，则会将每个连接 id 添加到用户的组中。</span><span class="sxs-lookup"><span data-stu-id="49e8f-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="49e8f-141">用户断开连接时，不应手动将用户从组中删除。</span><span class="sxs-lookup"><span data-stu-id="49e8f-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="49e8f-142">此操作由 SignalR 框架自动执行。</span><span class="sxs-lookup"><span data-stu-id="49e8f-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="49e8f-143">下面的示例演示如何实现单用户组。</span><span class="sxs-lookup"><span data-stu-id="49e8f-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="49e8f-144">永久、外部存储</span><span class="sxs-lookup"><span data-stu-id="49e8f-144">Permanent, external storage</span></span>

<span data-ttu-id="49e8f-145">本主题说明如何使用数据库或 Azure 表存储来存储连接信息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="49e8f-146">当你有多个 web 服务器时，这种方法可正常工作，因为每个 web 服务器可以与相同的数据存储库交互。</span><span class="sxs-lookup"><span data-stu-id="49e8f-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="49e8f-147">如果 web 服务器停止工作或重新启动应用程序，则不会调用 `OnDisconnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="49e8f-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="49e8f-148">因此，您的数据存储库可能会记录不再有效的连接 id。</span><span class="sxs-lookup"><span data-stu-id="49e8f-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="49e8f-149">若要清理这些孤立记录，你可能希望使在与你的应用程序相关的时间范围之外创建的任何连接无效。</span><span class="sxs-lookup"><span data-stu-id="49e8f-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="49e8f-150">本节中的示例包含一个用于在创建连接时进行跟踪的值，但不显示如何清理旧记录，因为你可能想要将其作为后台进程执行。</span><span class="sxs-lookup"><span data-stu-id="49e8f-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="49e8f-151">数据库</span><span class="sxs-lookup"><span data-stu-id="49e8f-151">Database</span></span>

<span data-ttu-id="49e8f-152">下面的示例演示如何在数据库中保留连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="49e8f-153">您可以使用任何数据访问技术;但下面的示例演示如何使用实体框架定义模型。</span><span class="sxs-lookup"><span data-stu-id="49e8f-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="49e8f-154">这些实体模型对应于数据库表和字段。</span><span class="sxs-lookup"><span data-stu-id="49e8f-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="49e8f-155">根据应用程序的要求，数据结构可能会有很大的差别。</span><span class="sxs-lookup"><span data-stu-id="49e8f-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="49e8f-156">第一个示例演示如何定义可以与多个连接实体相关联的用户实体。</span><span class="sxs-lookup"><span data-stu-id="49e8f-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="49e8f-157">然后，可以从中心跟踪每个连接的状态，如下所示。</span><span class="sxs-lookup"><span data-stu-id="49e8f-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="49e8f-158">Azure 表存储</span><span class="sxs-lookup"><span data-stu-id="49e8f-158">Azure table storage</span></span>

<span data-ttu-id="49e8f-159">以下 Azure 表存储示例类似于数据库示例。</span><span class="sxs-lookup"><span data-stu-id="49e8f-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="49e8f-160">它不包含开始 Azure 表存储服务所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="49e8f-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="49e8f-161">有关信息，请参阅[如何通过 .net 使用表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="49e8f-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="49e8f-162">下面的示例显示了用于存储连接信息的表实体。</span><span class="sxs-lookup"><span data-stu-id="49e8f-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="49e8f-163">它按用户名对数据进行分区，并通过连接 id 识别每个实体，因此用户可随时拥有多个连接。</span><span class="sxs-lookup"><span data-stu-id="49e8f-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="49e8f-164">在中心，你可以跟踪每个用户的连接的状态。</span><span class="sxs-lookup"><span data-stu-id="49e8f-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
