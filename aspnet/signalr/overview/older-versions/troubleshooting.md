---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 故障排除（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文介绍了开发 SignalR 应用程序时的常见问题。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468098"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR 疑难解答 (SignalR 1.x)

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了 SignalR 的常见疑难解答问题。

本文档包含以下各节。

- [以静默方式在客户端和服务器之间调用方法失败](#connection)
- [其他连接问题](#other)
- [编译和服务器端错误](#server)
- [Visual Studio 问题](#vs)
- [Internet Information Services 问题](#iis)
- [Azure 问题](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>以静默方式在客户端和服务器之间调用方法失败

本部分介绍在客户端和服务器之间的方法调用失败的可能原因，而没有有意义的错误消息。 在 SignalR 应用程序中，服务器没有有关客户端实现的方法的信息;当服务器调用客户端方法时，方法名称和参数数据将发送到客户端，并且仅当该方法以服务器指定的格式存在时，才会执行此方法。 如果在客户端上找不到匹配的方法，则不会执行任何操作，并且不会在服务器上引发任何错误消息。

若要进一步调查未调用的客户端方法，你可以在调用 start 方法之前打开中心日志记录，以查看来自服务器的调用。 若要在 JavaScript 应用程序中启用日志记录，请参阅[如何启用客户端日志记录（JavaScript 客户端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。 若要在 .NET 客户端应用程序中启用日志记录，请参阅[如何启用客户端日志记录（.Net 客户端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>拼写错误的方法、错误的方法签名或不正确的中心名称

如果被调用方法的名称或签名与客户端上的适当方法不完全匹配，则调用将失败。 验证服务器调用的方法名称是否与客户端上的方法的名称匹配。 此外，SignalR 使用 camel 大小写方法创建中心代理，这在 JavaScript 中是合适的方法，因此，在服务器上调用 `SendMessage` 的方法将在客户端代理 `sendMessage` 中调用。 如果使用服务器端代码中的 `HubName` 属性，请验证所使用的名称是否与用于在客户端上创建集线器的名称相匹配。 如果不使用 `HubName` 属性，请验证 JavaScript 客户端中的中心名称是否采用 camel 大小写格式（如 chatHub 而不是 ChatHub）。

### <a name="duplicate-method-name-on-client"></a>客户端上的重复方法名称

验证在客户端上没有仅大小写不同的重复方法。 如果客户端应用程序有一个名为 `sendMessage`的方法，请验证是否也没有名为 `SendMessage` 的方法。

### <a name="missing-json-parser-on-the-client"></a>客户端上缺少 JSON 分析器

SignalR 要求提供 JSON 分析器以序列化服务器和客户端之间的调用。 如果客户端没有内置的 JSON 分析器（如 Internet Explorer 7），则需要在应用程序中包含一个。 可在[此处](http://nuget.org/packages/json2)下载 JSON 分析器。

### <a name="mixing-hub-and-persistentconnection-syntax"></a>混合中心和 PersistentConnection 语法

SignalR 使用两种通信模型：集线器和 PersistentConnections。 在客户端代码中，调用这两个通信模型的语法不同。 如果已在服务器代码中添加集线器，请验证所有客户端代码是否均使用正确的中心语法。

**在 JavaScript 客户端中创建 PersistentConnection 的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**在 Javascript 客户端中创建集线器代理的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C#将路由映射到 PersistentConnection 的服务器代码**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C#如果有多个应用程序，则将路由映射到中心或多个集线器的服务器代码**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>在添加订阅之前已启动连接

如果在将可从服务器调用的方法添加到代理之前启动了中心的连接，则不会收到消息。 以下 JavaScript 代码将不会正确启动集线器：

**不允许接收集线器消息的不正确的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

请改为在调用 Start 之前添加方法订阅：

**正确向中心添加订阅的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>中心代理上缺少方法名称

验证在服务器上定义的方法是否已在客户端上订阅。 即使服务器定义了方法，仍必须将它添加到客户端代理。 可以通过以下方式将方法添加到客户端代理（请注意，方法已添加到中心的 `client` 成员，而不是直接添加到中心）：

**向中心代理添加方法的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>未声明为公共的集线器或集线器方法

若要在客户端上可见，中心实现和方法必须声明为 `public`。

### <a name="accessing-hub-from-a-different-application"></a>从不同的应用程序访问集线器

SignalR 中心只能通过实现 SignalR 客户端的应用程序进行访问。 SignalR 无法与其他通信库（如 SOAP 或 WCF web 服务）进行互操作。如果没有可用于目标平台的 SignalR 客户端，则无法直接访问服务器的终结点。

### <a name="manually-serializing-data"></a>手动序列化数据

SignalR 将自动使用 JSON 序列化方法参数，无需自行执行此操作。

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>远程集线器方法未在 OnDisconnected 函数中的客户端上执行

此行为是设计使然。 调用 `OnDisconnected` 时，中心已进入 `Disconnected` 状态，该状态不允许调用其他集线器方法。

**C#在 OnDisconnected 事件中正确执行代码的服务器代码**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>已达到连接限制

在客户端操作系统（如 Windows 7）上使用完整的 IIS 版本时，会施加10个连接限制。 使用客户端操作系统时，请改用 IIS Express 来避免此限制。

### <a name="cross-domain-connection-not-set-up-properly"></a>未正确设置跨域连接

如果跨域连接（SignalR URL 与宿主页面不在同一个域中的连接）未正确设置，则连接可能会失败，且不会出现错误消息。 有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>使用 NTLM （Active Directory）的连接在 .NET 客户端中不起作用

如果连接配置不正确，则使用域安全性的 .NET 客户端应用程序中的连接可能会失败。 若要在域环境中使用 SignalR，请设置所需的连接属性，如下所示：

**C#实现连接凭据的客户端代码**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>其他连接问题

本部分介绍连接过程中出现的特定症状或错误消息的原因和解决方法。

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"必须在可以发送数据之前调用启动" 错误

如果在启动连接之前代码引用 SignalR 对象，则通常会出现此错误。 处理程序的绑定和将调用在服务器上定义的方法的类似方法必须在连接完成后添加。 请注意，对 `Start` 的调用是异步的，因此调用后的代码可以在完成之前执行。 在连接完全启动后添加处理程序的最佳方式是将其放入一个回调函数，该函数作为参数传递给 start 方法：

**正确添加引用 SignalR 对象的事件处理程序的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

如果仍在引用 SignalR 对象，则会出现此错误。

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 永久移动" 或 "302 移动" 错误

如果项目包含一个名为 SignalR 的文件夹，该文件夹将干扰自动创建的代理，则可能出现此错误。 若要避免此错误，请不要在应用程序中使用称为 `SignalR` 的文件夹，或关闭自动代理生成。 有关更多详细信息，请参阅[生成的代理以及它所执行的](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)操作。

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 或 Silverlight 客户端中的 "403 禁止访问" 错误

此错误可能出现在未正确启用跨域通信的跨域环境中。 有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。 若要在 Silverlight 客户端中建立跨域连接，请参阅[从 silverlight 客户端进行跨域连接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。

### <a name="404-not-found-error"></a>"找不到 404" 错误

此问题有几个原因。 验证以下所有内容：

- **集线器代理地址引用的格式不正确：** 如果对生成的中心代理地址的引用的格式不正确，则通常会出现此错误。 验证对中心地址的引用是否正确。 有关详细信息，请参阅[如何引用动态生成的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。
- 添加**中心路由之前，向应用程序添加路由：** 如果你的应用程序使用其他路由，请验证添加的第一个路由是对 `MapHubs`的调用。

### <a name="500-internal-server-error"></a>"500 内部服务器错误"

这是一种非常通用的错误，可能会产生多种原因。 错误的详细信息应该出现在服务器的事件日志中，也可以通过调试服务器找到。 可以通过打开服务器上的详细错误来获取更详细的错误信息。 有关详细信息，请参阅[如何处理中心类中的错误](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError： &lt;hubType&gt; 未定义" 错误

如果未正确调用 `MapHubs`，则会导致此错误。 有关详细信息，请参阅[如何注册 SignalR 路由和配置 SignalR 选项](../guide-to-the-api/hubs-api-guide-server.md#route)。

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>用户代码未处理 JsonSerializationException

验证发送给方法的参数不包括非序列化类型（如文件句柄或数据库连接）。 如果需要在不想发送到客户端的服务器端对象上使用成员（出于安全原因或序列化的原因），请使用 `JSONIgnore` 特性。

### <a name="protocol-error-unknown-transport-error"></a>"协议错误：未知传输" 错误

如果客户端不支持 SignalR 使用的传输，则可能出现此错误。 有关可与 SignalR 一起使用的浏览器的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript Hub 代理生成已禁用。"

如果设置 `DisableJavaScriptProxies`，同时在 `signalr/hubs`同时包含对动态生成的代理的引用，则会发生此错误。 有关手动创建代理的详细信息，请参阅[生成的代理及其功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"连接 ID 的格式不正确，或者" 用户标识在 active SignalR 连接期间无法更改 "错误

如果正在使用身份验证，并且在停止连接之前注销了客户端，则可能出现此错误。 解决方法是在注销客户端之前停止 SignalR 连接。

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"未捕获的错误： SignalR： jQuery 找不到。 请确保引用 jQuery，然后再引用 SignalR 文件 "错误

SignalR JavaScript 客户端需要 jQuery 才能运行。 验证对 jQuery 的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否在对 SignalR 的引用之前。

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"未捕获 TypeError：无法读取属性"&lt;属性&gt;"未定义" 错误

此错误是由于未正确引用 jQuery 或中心代理而导致的。 验证对 jQuery 和中心代理的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否在对集线器代理的引用之前。 对集线器代理的默认引用如下所示：

**正确引用中心代理的 HTML 客户端代码**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException 已被用户代码处理" 错误

如果使用 `Hub.On` 的错误重载，则可能出现此错误。 如果该方法具有返回值，则返回类型必须指定为泛型类型参数：

**在客户端上定义的方法（不生成代理）**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>连接 ID 不一致或页面加载之间的连接中断

此行为是设计使然。 由于中心对象承载于 page 对象中，因此在页面刷新时，中心将被销毁。 多页应用程序需要维护用户和连接 Id 之间的关联，以便它们在页面加载之间保持一致。 连接 Id 可以存储在服务器上的 `ConcurrentDictionary` 对象或数据库中。

### <a name="value-cannot-be-null-error"></a>"值不能为 null" 错误

当前不支持带有可选参数的服务器端方法;如果省略可选参数，则该方法将失败。 有关详细信息，请参阅[可选参数](https://github.com/SignalR/SignalR/issues/324)。

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox 无法与服务器建立连接，因为在 Firebug 中 &lt;地址&gt;" 错误

如果 WebSocket 传输的协商失败并且改为使用另一个传输，则会在 Firebug 中出现此错误消息。 此行为是设计使然。

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET 客户端应用程序中的 "远程证书根据验证过程无效" 错误

如果服务器需要自定义客户端证书，则可以在发出请求之前将 x509certificate 添加到连接。 使用 `Connection.AddClientCertificate`将证书添加到连接。

### <a name="connection-drops-after-authentication-times-out"></a>身份验证超时后断开连接

此行为是设计使然。 连接处于活动状态时，无法修改身份验证凭据;若要刷新凭据，必须停止并重新启动该连接。

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>使用 jQuery Mobile 时，OnConnected 调用了两次

jQuery Mobile 的 `initializePage` 函数强制重新执行每个页面中的脚本，从而创建另一个连接。 此问题的解决方案包括：

- 在 JavaScript 文件之前包括对 jQuery Mobile 的引用。
- 通过设置 `$.mobile.autoInitializePage = false`禁用 `initializePage` 函数。
- 等待页面完成初始化，然后再开始连接。

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>使用服务器发送事件的 Silverlight 应用程序中的消息延迟

在 Silverlight 上使用服务器发送的事件时，消息会被延迟。 若要改为强制使用长轮询，请在启动连接时使用以下内容：

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>使用永久帧协议的 "权限被拒绝"

这是一个已知问题，请[参阅此](https://github.com/SignalR/SignalR/issues/1963)文。 使用最新 JQuery library 时可能会出现此症状;解决方法是将应用程序降级到 JQuery 1.8.2。

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>编译和服务器端错误

 以下部分包含编译器和服务器端运行时错误的可能解决方案。 

### <a name="reference-to-hub-instance-is-null"></a>对中心实例的引用为 null

由于已为每个连接创建集线器实例，因此无法在代码中自行创建集线器的实例。 若要从中心自身外部调用集线器上的方法，请参阅[如何从中心类的外部调用客户端方法和管理组](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，了解如何获取对中心上下文的引用。

### <a name="httpcontextcurrentsession-is-null"></a>Httpcontext.current 为 null

此行为是设计使然。 SignalR 不支持 ASP.NET 会话状态，因为启用会话状态将中断双工消息。

### <a name="no-suitable-method-to-override"></a>没有合适的替代方法

如果使用的是较旧文档或博客中的代码，则可能会看到此错误。 验证你未引用已更改或已弃用的方法的名称（如 `OnConnectedAsync`）。

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions. WebSocketServerUrl 为 null

此行为是设计使然。 此成员已弃用，不应使用。

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"名为 ' signalr ' 的路由已在路由集合中" 错误

如果应用程序调用了两次 `MapHubs`，则会出现此错误。 一些示例应用程序直接在全局应用程序文件中调用 `MapHubs`;其他人在包装类中进行调用。 确保应用程序不会同时执行这两项操作。

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio 问题

本部分介绍 Visual Studio 中遇到的问题。

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>脚本文档节点未出现在解决方案资源管理器

在调试过程中，我们的一些教程会将您定向到解决方案资源管理器中的 "脚本文档" 节点。 此节点由 JavaScript 调试器生成，仅在调试 Internet Explorer 中的浏览器客户端时显示;如果使用的是 Chrome 或 Firefox，则不会显示该节点。 如果另一个客户端调试器正在运行，如 Silverlight 调试器，JavaScript 调试器也不会运行。

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR 在 Visual Studio 2008 或更早版本上不起作用

此行为是设计使然。 SignalR 需要 .NET Framework 4 或更高版本;这要求在 Visual Studio 2010 或更高版本中开发 SignalR 应用程序。

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 问题

本部分包含与 Internet Information Services 有关的问题。

### <a name="web-site-crashes-after-maphubs-call"></a>Routeconfig 调用后网站崩溃

此问题已在最新版本的 SignalR 中得到解决。 通过使用 NuGet 更新安装，验证你是否正在使用 SignalR 的最新发布版本。

<a id="azure"></a>

## <a name="azure-issues"></a>Azure 问题

本部分包含与 Microsoft Azure 有关的问题。

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>更改主题名称后，不通过 Azure 底板接收消息

Azure 底板使用的主题并不是用户可配置的。
