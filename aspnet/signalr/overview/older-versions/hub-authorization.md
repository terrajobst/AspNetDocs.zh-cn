---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR 中心的身份验证和授权（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本主题介绍如何限制哪些用户或角色可以访问中心方法。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450038"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a>SignalR 中心身份验证和授权 (SignalR 1.x)

作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题介绍如何限制哪些用户或角色可以访问中心方法。

## <a name="overview"></a>概述

本主题包含以下各节：

- [授权属性](#authorizeattribute)
- [要求对所有中心进行身份验证](#requireauth)
- [自定义授权](#custom)
- [向客户端传递身份验证信息](#passauth)
- [.NET 客户端的身份验证选项](#authoptions)

    - [带有 Forms 身份验证的 Cookie](#cookie)
    - [Windows 身份验证](#windows)
    - [连接头](#header)
    - [证书](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>授权属性

SignalR 提供[授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性以指定哪些用户或角色有权访问集线器或方法。 此属性位于 `Microsoft.AspNet.SignalR` 命名空间中。 将 `Authorize` 特性应用于中心中的集线器或特定方法。 将 `Authorize` 特性应用于 hub 类时，指定的授权要求将应用于中心中的所有方法。 下面显示了你可以应用的不同类型的授权要求。 如果没有 `Authorize` 属性，则中心上的所有公共方法都可用于连接到集线器的客户端。

如果你在 web 应用程序中定义了名为 "Admin" 的角色，则可以指定只有该角色中的用户可以使用以下代码访问中心。

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

或者，你可以指定一个中心包含一个可供所有用户使用的方法，以及一个仅适用于经过身份验证的用户的第二种方法，如下所示。

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

以下示例解决了不同的授权方案：

- `[Authorize]` –仅限经过身份验证的用户
- `[Authorize(Roles = "Admin,Manager")]` –仅指定角色中经过身份验证的用户
- `[Authorize(Users = "user1,user2")]` –只有具有指定用户名的经过身份验证的用户
- `[Authorize(RequireOutgoing=false)]` –只有经过身份验证的用户可以调用中心，但从服务器到客户端的调用不受授权限制，例如，当只有特定用户可以发送消息，但所有其他用户都可以接收消息时。 RequireOutgoing 属性只能应用于整个中心，而不能应用于中心内的个人方法。 当 RequireOutgoing 未设置为 false 时，仅从服务器中调用满足授权要求的用户。

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>要求对所有中心进行身份验证

在应用程序启动时，可以通过调用[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)方法，要求对应用程序中的所有中心和集线器方法进行身份验证。 如果有多个中心并想要为所有中心强制实施身份验证要求，则可以使用此方法。 利用此方法，无法指定角色、用户或传出授权。 只能指定仅限经过身份验证的用户访问集线器方法。 不过，你仍然可以将授权属性应用于中心或方法，以指定其他要求。 除了身份验证的基本要求外，还会应用在特性中指定的任何要求。

下面的示例显示了一个 Global.asa 文件，该文件将所有集线器方法限制为已通过身份验证的用户。

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

如果在处理 SignalR 请求后调用 `RequireAuthentication()` 方法，SignalR 将引发 `InvalidOperationException` 异常。 引发此异常的原因是，在调用管道后，不能将模块添加到 HubPipeline 中。 前面的示例演示如何在 `Application_Start` 方法中调用 `RequireAuthentication` 方法，该方法在处理第一个请求之前执行一次。

<a id="custom"></a>

## <a name="customized-authorization"></a>自定义授权

如果需要自定义如何确定授权，可以创建一个派生自 `AuthorizeAttribute` 的类，并重写[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。 为每个请求调用此方法，以确定用户是否有权完成该请求。 在重写的方法中，为授权方案提供必要的逻辑。 下面的示例演示如何通过基于声明的标识来强制执行授权。

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>向客户端传递身份验证信息

可能需要在客户端上运行的代码中使用身份验证信息。 在客户端上调用方法时传递所需的信息。 例如，聊天应用程序方法可以作为参数传递用户的用户名称，如下所示。

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

或者，你可以创建一个对象来表示身份验证信息，并将该对象作为参数传递，如下所示。

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

永远不要将一个客户端的连接 id 传递到其他客户端，因为恶意用户可以使用它来模拟该客户端的请求。

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET 客户端的身份验证选项

如果你有一个 .NET 客户端（如控制台应用程序），该应用程序与限制为已通过身份验证的用户的集线器进行交互，则可以通过 cookie、连接头或证书传递身份验证凭据。 本节中的示例演示如何使用不同的方法对用户进行身份验证。 它们不是功能齐全的 SignalR 应用程序。 有关包含 SignalR 的 .NET 客户端的详细信息，请参阅[中心 API 指南-.Net 客户端](../guide-to-the-api/hubs-api-guide-net-client.md)。

<a id="cookie"></a>

### <a name="cookie"></a>Cookie

当你的 .NET 客户端与使用 ASP.NET Forms 身份验证的集线器进行交互时，你将需要在连接上手动设置身份验证 cookie。 将该 cookie 添加到[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)对象上的 `CookieContainer` 属性。 下面的示例演示了一个控制台应用程序，该应用程序从网页中检索身份验证 cookie 并将该 cookie 添加到连接。 示例中的 URL `https://www.contoso.com/RemoteLogin` 指向需要创建的网页。 该页将检索已发布的用户名和密码，并尝试用凭据登录用户。

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

控制台应用会将凭据发布到 www.contoso.com/RemoteLogin，这可能表示包含以下代码隐藏文件的空页面。

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows 身份验证

使用 Windows 身份验证时，可以通过使用[DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)属性传递当前用户的凭据。 将连接的凭据设置为 DefaultCredentials 的值。

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>连接头

如果你的应用程序未使用 cookie，你可以将用户信息传递到连接标头。 例如，可以在 connection 标头中传递令牌。

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

然后，在中心中验证用户的令牌。

<a id="certificate"></a>

### <a name="certificate"></a>证书

可以传递客户端证书来验证用户。 在创建连接时添加证书。 下面的示例演示如何将客户端证书添加到连接;它不会显示完整的控制台应用程序。 它使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)类，该类提供多种不同的方法来创建证书。

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
