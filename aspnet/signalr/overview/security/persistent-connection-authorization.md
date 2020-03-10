---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 持久性连接的身份验证和授权 |Microsoft Docs
author: bradygaster
description: 本主题介绍如何在持久性连接上强制实施授权。 有关将安全性集成到 SignalR 应用程序的一般信息,。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467474"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a>SignalR 永久性连接身份验证和授权

作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题介绍如何在持久性连接上强制实施授权。 有关将安全性集成到 SignalR 应用程序的一般信息，请参阅[安全性简介](introduction-to-security.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="enforce-authorization"></a>强制授权

若要在使用[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)时强制执行授权规则，必须重写 `AuthorizeRequest` 方法。 不能将 `Authorize` 特性与持久性连接一起使用。 SignalR 框架在每次请求之前调用 `AuthorizeRequest` 方法，以验证用户是否有权执行请求的操作。 不会从客户端调用 `AuthorizeRequest` 方法;相反，你可以通过应用程序的标准身份验证机制来对用户进行身份验证。

下面的示例演示如何将请求限制为已通过身份验证的用户。

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

可以在 AuthorizeRequest 方法中添加任何自定义的授权逻辑;例如，检查用户是否属于特定角色。
