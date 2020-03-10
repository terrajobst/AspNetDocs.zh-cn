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
# <a name="working-with-groups-in-signalr-1x"></a>在 SignalR 1.x 中使用组

作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题介绍如何将用户添加到组，以及如何保留组成员身份信息。

## <a name="overview"></a>概述

SignalR 中的组提供一种方法，用于将消息广播到连接的已连接客户端的指定子集。 一个组可以具有任意数量的客户端，客户端可以是任意数量的组的成员。 无需显式创建组。 实际上，在对组的调用中首次指定组的名称时，将自动创建一个组。添加，当你从其成员身份中删除最后一个连接时，会将其删除。 有关使用组的简介，请参阅 "中心 API-服务器指南" 中的[如何管理中心类中的组成员身份](index.md)。

没有用于获取组成员身份列表或组列表的 API。 SignalR 基于发布/订阅模型将消息发送到客户端和组，并且服务器不维护组或组成员身份列表。 这有助于最大程度地提高可伸缩性，因为每次将节点添加到 web 场时，SignalR 维护的任何状态都必须传播到新节点。

当使用 `Groups.Add` 方法将用户添加到组中时，用户会在当前连接的持续时间内接收到该组的消息，但该用户在此组中的成员身份不会保留在当前连接的范围之内。 如果要永久保留有关组和组成员身份的信息，则必须将该数据存储在存储库中，如数据库或 Azure 表存储。 然后，每次用户连接到应用程序时，都将从用户所属的存储库检索，并手动将该用户添加到这些组。

当暂时中断后，用户会自动重新加入之前分配的组。 自动重新加入组仅在重新连接时应用，而不会在建立新连接时使用。 从包含以前分配的组列表的客户端传递经过数字签名的令牌。 如果要验证用户是否属于请求的组，可以重写默认行为。

本主题包括以下部分：

- [添加和删除用户](#add)
- [调用组的成员](#call)
- [在数据库中存储组成员身份](#storedatabase)
- [在 Azure 表存储中存储组成员身份](#storeazuretable)
- [重新连接时验证组成员身份](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>添加和删除用户

若要在组中添加或删除用户，请调用[add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)或[remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法，并传入用户的连接 id 和组名称作为参数。 当连接结束时，无需手动从组中删除用户。

下面的示例演示了在中心方法中使用的 `Groups.Add` 和 `Groups.Remove` 方法。

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` 和 `Groups.Remove` 方法以异步方式执行。

如果要将客户端添加到组，并使用组立即将消息发送到客户端，则必须确保组。 Add 方法首先完成。 下面的代码示例演示如何执行此操作，一种方法是使用 .NET 4.5 中适用的代码，另一种方法是使用 .NET 4 中的代码。

#### <a name="asynchronous-net-45-example"></a>异步 .NET 4.5 示例

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>异步 .NET 4 示例

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

通常，调用 `Groups.Remove` 方法时不应包括 `await`，因为你尝试删除的连接 id 可能不再可用。 在这种情况下，请求超时后引发 `TaskCanceledException`。如果你的应用程序必须确保在将消息发送到组之前已从组中删除该用户，则可以在组之前添加 `await`。删除，然后捕获可能引发的 `TaskCanceledException` 异常。

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>调用组的成员

你可以将消息发送到组的所有成员，或者只发送到组的指定成员，如下面的示例中所示。

- 指定组中的**所有**连接的客户端。 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- 指定组中**除指定的客户端之外**的所有连接的客户端，由连接 ID 标识。 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- 指定组中**除调用客户端之外**的所有连接的客户端。 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>在数据库中存储组成员身份

下面的示例演示如何在数据库中保留组和用户信息。 您可以使用任何数据访问技术;但下面的示例演示如何使用实体框架定义模型。 这些实体模型对应于数据库表和字段。 根据应用程序的要求，数据结构可能会有很大的差别。 此示例包含一个名为 `ConversationRoom` 的类，该类对应用程序来说是唯一的，该应用程序使用户能够加入有关不同主题（如运动或园艺）的对话。 此示例还包括一个用于连接的类。 跟踪组成员身份不是绝对必需的，但通常是用于跟踪用户的强健解决方案的一部分。

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

然后，在中心中，可以从数据库中检索组和用户信息，并手动将用户添加到相应的组。 该示例不包含用于跟踪用户连接的代码。 在此示例中，不会在 `Groups.Add` 之前应用 `await` 关键字，因为消息不会立即发送到组的成员。 如果要在添加新成员后立即将消息发送到该组的所有成员，则需要应用 `await` 关键字来确保异步操作已完成。

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>在 Azure 表存储中存储组成员身份

使用 Azure 表存储来存储组和用户信息类似于使用数据库。 下面的示例显示了一个表实体，其中存储了用户名和组名。

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

在中心，你可以在用户连接时检索已分配的组。

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>重新连接时验证组成员身份

默认情况下，当从暂时中断重新连接时，SignalR 会自动将用户重新分配给相应的组，例如在连接断开之前断开并重新建立连接。重新连接时，会在令牌中传递用户的组信息，并在服务器上验证该令牌。 有关重新加入用户到组的验证过程的信息，请参阅重新[连接时重新加入组](index.md)。

通常，应在重新连接时使用自动重新加入组的默认行为。 SignalR 组不应作为一种安全机制来限制对敏感数据的访问。 但是，如果应用程序在重新连接时必须仔细检查用户的组成员身份，则可以重写默认行为。 更改默认行为可能会给数据库带来负担，因为必须为每个重新连接检索用户的组成员身份，而不只是在用户连接时进行检索。

如果必须在重新连接时验证组成员身份，请创建新的中心管道模块，该模块将返回已分配组的列表，如下所示。

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

然后，将该模块添加到中心管道，如下所示。

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
