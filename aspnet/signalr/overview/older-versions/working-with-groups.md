---
uid: signalr/overview/older-versions/working-with-groups
title: 在 SignalR 1.x 中使用组 |Microsoft Docs
author: bradygaster
description: 本主题介绍如何通过中心 API 持久保存组成员身份信息。
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467894"
---
# <a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="22445-103">在 SignalR 1.x 中使用组</span><span class="sxs-lookup"><span data-stu-id="22445-103">Working with Groups in SignalR 1.x</span></span>

<span data-ttu-id="22445-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="22445-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="22445-105">本主题介绍如何将用户添加到组，以及如何保留组成员身份信息。</span><span class="sxs-lookup"><span data-stu-id="22445-105">This topic describes how to add users to groups and persist group membership information.</span></span>

## <a name="overview"></a><span data-ttu-id="22445-106">概述</span><span class="sxs-lookup"><span data-stu-id="22445-106">Overview</span></span>

<span data-ttu-id="22445-107">SignalR 中的组提供一种方法，用于将消息广播到连接的已连接客户端的指定子集。</span><span class="sxs-lookup"><span data-stu-id="22445-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="22445-108">一个组可以具有任意数量的客户端，客户端可以是任意数量的组的成员。</span><span class="sxs-lookup"><span data-stu-id="22445-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="22445-109">无需显式创建组。</span><span class="sxs-lookup"><span data-stu-id="22445-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="22445-110">实际上，在对组的调用中首次指定组的名称时，将自动创建一个组。添加，当你从其成员身份中删除最后一个连接时，会将其删除。</span><span class="sxs-lookup"><span data-stu-id="22445-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="22445-111">有关使用组的简介，请参阅 "中心 API-服务器指南" 中的[如何管理中心类中的组成员身份](index.md)。</span><span class="sxs-lookup"><span data-stu-id="22445-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="22445-112">没有用于获取组成员身份列表或组列表的 API。</span><span class="sxs-lookup"><span data-stu-id="22445-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="22445-113">SignalR 基于发布/订阅模型将消息发送到客户端和组，并且服务器不维护组或组成员身份列表。</span><span class="sxs-lookup"><span data-stu-id="22445-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="22445-114">这有助于最大程度地提高可伸缩性，因为每次将节点添加到 web 场时，SignalR 维护的任何状态都必须传播到新节点。</span><span class="sxs-lookup"><span data-stu-id="22445-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="22445-115">当使用 `Groups.Add` 方法将用户添加到组中时，用户会在当前连接的持续时间内接收到该组的消息，但该用户在此组中的成员身份不会保留在当前连接的范围之内。</span><span class="sxs-lookup"><span data-stu-id="22445-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="22445-116">如果要永久保留有关组和组成员身份的信息，则必须将该数据存储在存储库中，如数据库或 Azure 表存储。</span><span class="sxs-lookup"><span data-stu-id="22445-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="22445-117">然后，每次用户连接到应用程序时，都将从用户所属的存储库检索，并手动将该用户添加到这些组。</span><span class="sxs-lookup"><span data-stu-id="22445-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="22445-118">当暂时中断后，用户会自动重新加入之前分配的组。</span><span class="sxs-lookup"><span data-stu-id="22445-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="22445-119">自动重新加入组仅在重新连接时应用，而不会在建立新连接时使用。</span><span class="sxs-lookup"><span data-stu-id="22445-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="22445-120">从包含以前分配的组列表的客户端传递经过数字签名的令牌。</span><span class="sxs-lookup"><span data-stu-id="22445-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="22445-121">如果要验证用户是否属于请求的组，可以重写默认行为。</span><span class="sxs-lookup"><span data-stu-id="22445-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="22445-122">本主题包括以下部分：</span><span class="sxs-lookup"><span data-stu-id="22445-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="22445-123">添加和删除用户</span><span class="sxs-lookup"><span data-stu-id="22445-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="22445-124">调用组的成员</span><span class="sxs-lookup"><span data-stu-id="22445-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="22445-125">在数据库中存储组成员身份</span><span class="sxs-lookup"><span data-stu-id="22445-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="22445-126">在 Azure 表存储中存储组成员身份</span><span class="sxs-lookup"><span data-stu-id="22445-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="22445-127">重新连接时验证组成员身份</span><span class="sxs-lookup"><span data-stu-id="22445-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="22445-128">添加和删除用户</span><span class="sxs-lookup"><span data-stu-id="22445-128">Adding and removing users</span></span>

<span data-ttu-id="22445-129">若要在组中添加或删除用户，请调用[add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)或[remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法，并传入用户的连接 id 和组名称作为参数。</span><span class="sxs-lookup"><span data-stu-id="22445-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="22445-130">当连接结束时，无需手动从组中删除用户。</span><span class="sxs-lookup"><span data-stu-id="22445-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="22445-131">下面的示例演示了在中心方法中使用的 `Groups.Add` 和 `Groups.Remove` 方法。</span><span class="sxs-lookup"><span data-stu-id="22445-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="22445-132">`Groups.Add` 和 `Groups.Remove` 方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="22445-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="22445-133">如果要将客户端添加到组，并使用组立即将消息发送到客户端，则必须确保组。 Add 方法首先完成。</span><span class="sxs-lookup"><span data-stu-id="22445-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="22445-134">下面的代码示例演示如何执行此操作，一种方法是使用 .NET 4.5 中适用的代码，另一种方法是使用 .NET 4 中的代码。</span><span class="sxs-lookup"><span data-stu-id="22445-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="22445-135">异步 .NET 4.5 示例</span><span class="sxs-lookup"><span data-stu-id="22445-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="22445-136">异步 .NET 4 示例</span><span class="sxs-lookup"><span data-stu-id="22445-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="22445-137">通常，调用 `Groups.Remove` 方法时不应包括 `await`，因为你尝试删除的连接 id 可能不再可用。</span><span class="sxs-lookup"><span data-stu-id="22445-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="22445-138">在这种情况下，请求超时后引发 `TaskCanceledException`。如果你的应用程序必须确保在将消息发送到组之前已从组中删除该用户，则可以在组之前添加 `await`。删除，然后捕获可能引发的 `TaskCanceledException` 异常。</span><span class="sxs-lookup"><span data-stu-id="22445-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="22445-139">调用组的成员</span><span class="sxs-lookup"><span data-stu-id="22445-139">Calling members of a group</span></span>

<span data-ttu-id="22445-140">你可以将消息发送到组的所有成员，或者只发送到组的指定成员，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="22445-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="22445-141">指定组中的**所有**连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="22445-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="22445-142">指定组中**除指定的客户端之外**的所有连接的客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="22445-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="22445-143">指定组中**除调用客户端之外**的所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="22445-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="22445-144">在数据库中存储组成员身份</span><span class="sxs-lookup"><span data-stu-id="22445-144">Storing group membership in a database</span></span>

<span data-ttu-id="22445-145">下面的示例演示如何在数据库中保留组和用户信息。</span><span class="sxs-lookup"><span data-stu-id="22445-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="22445-146">您可以使用任何数据访问技术;但下面的示例演示如何使用实体框架定义模型。</span><span class="sxs-lookup"><span data-stu-id="22445-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="22445-147">这些实体模型对应于数据库表和字段。</span><span class="sxs-lookup"><span data-stu-id="22445-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="22445-148">根据应用程序的要求，数据结构可能会有很大的差别。</span><span class="sxs-lookup"><span data-stu-id="22445-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="22445-149">此示例包含一个名为 `ConversationRoom` 的类，该类对应用程序来说是唯一的，该应用程序使用户能够加入有关不同主题（如运动或园艺）的对话。</span><span class="sxs-lookup"><span data-stu-id="22445-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="22445-150">此示例还包括一个用于连接的类。</span><span class="sxs-lookup"><span data-stu-id="22445-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="22445-151">跟踪组成员身份不是绝对必需的，但通常是用于跟踪用户的强健解决方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="22445-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="22445-152">然后，在中心中，可以从数据库中检索组和用户信息，并手动将用户添加到相应的组。</span><span class="sxs-lookup"><span data-stu-id="22445-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="22445-153">该示例不包含用于跟踪用户连接的代码。</span><span class="sxs-lookup"><span data-stu-id="22445-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="22445-154">在此示例中，不会在 `Groups.Add` 之前应用 `await` 关键字，因为消息不会立即发送到组的成员。</span><span class="sxs-lookup"><span data-stu-id="22445-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="22445-155">如果要在添加新成员后立即将消息发送到该组的所有成员，则需要应用 `await` 关键字来确保异步操作已完成。</span><span class="sxs-lookup"><span data-stu-id="22445-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="22445-156">在 Azure 表存储中存储组成员身份</span><span class="sxs-lookup"><span data-stu-id="22445-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="22445-157">使用 Azure 表存储来存储组和用户信息类似于使用数据库。</span><span class="sxs-lookup"><span data-stu-id="22445-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="22445-158">下面的示例显示了一个表实体，其中存储了用户名和组名。</span><span class="sxs-lookup"><span data-stu-id="22445-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="22445-159">在中心，你可以在用户连接时检索已分配的组。</span><span class="sxs-lookup"><span data-stu-id="22445-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="22445-160">重新连接时验证组成员身份</span><span class="sxs-lookup"><span data-stu-id="22445-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="22445-161">默认情况下，当从暂时中断重新连接时，SignalR 会自动将用户重新分配给相应的组，例如在连接断开之前断开并重新建立连接。重新连接时，会在令牌中传递用户的组信息，并在服务器上验证该令牌。</span><span class="sxs-lookup"><span data-stu-id="22445-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="22445-162">有关重新加入用户到组的验证过程的信息，请参阅重新[连接时重新加入组](index.md)。</span><span class="sxs-lookup"><span data-stu-id="22445-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="22445-163">通常，应在重新连接时使用自动重新加入组的默认行为。</span><span class="sxs-lookup"><span data-stu-id="22445-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="22445-164">SignalR 组不应作为一种安全机制来限制对敏感数据的访问。</span><span class="sxs-lookup"><span data-stu-id="22445-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="22445-165">但是，如果应用程序在重新连接时必须仔细检查用户的组成员身份，则可以重写默认行为。</span><span class="sxs-lookup"><span data-stu-id="22445-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="22445-166">更改默认行为可能会给数据库带来负担，因为必须为每个重新连接检索用户的组成员身份，而不只是在用户连接时进行检索。</span><span class="sxs-lookup"><span data-stu-id="22445-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="22445-167">如果必须在重新连接时验证组成员身份，请创建新的中心管道模块，该模块将返回已分配组的列表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="22445-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="22445-168">然后，将该模块添加到中心管道，如下所示。</span><span class="sxs-lookup"><span data-stu-id="22445-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
