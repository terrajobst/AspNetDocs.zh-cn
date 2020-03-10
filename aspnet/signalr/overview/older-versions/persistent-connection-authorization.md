---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR 持久性连接的身份验证和授权（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本主题介绍如何在持久性连接上强制实施授权。 有关将安全性集成到 SignalR 应用程序的一般信息,。
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431186"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>SignalR 永久性连接身份验证和授权 (SignalR 1.x)

作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题介绍如何在持久性连接上强制实施授权。 有关将安全性集成到 SignalR 应用程序的一般信息，请参阅[安全性简介](index.md)。

## <a name="enforce-authorization"></a>强制授权

若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)时强制执行授权规则，必须重写 `AuthorizeRequest` 方法。 不能将 `Authorize` 特性与持久性连接一起使用。 SignalR 框架在每次请求之前调用 `AuthorizeRequest` 方法，以验证用户是否有权执行请求的操作。 不会从客户端调用 `AuthorizeRequest` 方法;相反，你可以通过应用程序的标准身份验证机制来对用户进行身份验证。

下面的示例演示如何将请求限制为已通过身份验证的用户。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

可以在 AuthorizeRequest 方法中添加任何自定义的授权逻辑;例如，检查用户是否属于特定角色。
