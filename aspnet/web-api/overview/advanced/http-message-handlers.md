---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API-ASP.NET 4.x 中的 HTTP 消息处理程序
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的 HTTP 消息处理程序的概述
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504926"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 中的 HTTP 消息处理程序

作者： [Mike Wasson](https://github.com/MikeWasson)

*消息处理程序*是接收 http 请求并返回 http 响应的类。 消息处理程序派生自抽象**HttpMessageHandler**类。

通常，一系列消息处理程序链接在一起。 第一个处理程序接收 HTTP 请求，进行一些处理，并向下一个处理程序提供请求。 在某个时间点，将创建响应，并在链中返回。 此模式称为*委托*处理程序。

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>服务器端消息处理程序

在服务器端，Web API 管道使用某些内置消息处理程序：

- **HttpServer**获取来自主机的请求。
- **HttpRoutingDispatcher**根据路由调度请求。
- **System.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**将请求发送到 Web API 控制器。

您可以向管道添加自定义处理程序。 消息处理程序适用于在 HTTP 消息级别（而不是控制器操作）上操作的交叉切削问题。 例如，消息处理程序可以：

- 读取或修改请求标头。
- 向响应添加响应标头。
- 在请求到达控制器之前对其进行验证。

此关系图显示插入到管道中的两个自定义处理程序：

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> 在客户端，HttpClient 还使用消息处理程序。 有关详细信息，请参阅[HttpClient 消息处理程序](httpclient-message-handlers.md)。

## <a name="custom-message-handlers"></a>自定义消息处理程序

若要编写自定义消息处理程序，请从**DelegatingHandler**派生并重写**SendAsync**方法。 此方法具有以下签名：

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。 典型的实现会执行以下操作：

1. 处理请求消息。
2. 调用 `base.SendAsync` 将请求发送到内部处理程序。
3. 内部处理程序返回响应消息。 （此步骤是异步的。）
4. 处理响应并将其返回给调用方。

下面是一个简单的示例：

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> 对 `base.SendAsync` 的调用是异步的。 如果处理程序在此调用后执行任何操作，请使用**await**关键字，如所示。

委托处理程序还可以跳过内部处理程序并直接创建响应：

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

如果委托处理程序在没有调用 `base.SendAsync`的情况下创建响应，则该请求将跳过管道的其余部分。 这对于验证请求的处理程序（创建错误响应）很有用。

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>向管道添加处理程序

若要在服务器端添加消息处理程序，请将该处理程序添加到**HttpConfiguration**集合。 如果使用了 "ASP.NET MVC 4 Web 应用程序" 模板来创建项目，可以在**webapiconfig.cs**类中执行此操作：

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

消息处理程序的调用顺序与它们在**MessageHandlers**集合中出现的顺序相同。 由于它们是嵌套的，因此响应消息以其他方向传输。 也就是说，最后一个处理程序是获取响应消息的第一个处理程序。

请注意，不需要设置内部处理程序;Web API 框架会自动连接消息处理程序。

如果你是[自承载](../older-versions/self-host-a-web-api.md)，请创建**HttpSelfHostConfiguration**类的实例，并将该处理程序添加到**MessageHandlers**集合中。

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

现在，让我们看一些自定义消息处理程序示例。

## <a name="example-x-http-method-override"></a>示例： X HTTP-方法-Override

X HTTP 方法-重写是非标准的 HTTP 标头。 它适用于不能发送某些 HTTP 请求类型的客户端，例如 PUT 或 DELETE。 相反，客户端发送 POST 请求，并将 X HTTP 方法重写标头设置为所需的方法。 例如:

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

下面是添加对 X HTTP 方法重写的支持的消息处理程序：

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

在**SendAsync**方法中，处理程序检查请求消息是 POST 请求，还是包含 X HTTP 方法-重写标头。 如果是，它将验证标头值，然后修改请求方法。 最后，处理程序调用 `base.SendAsync` 将消息传递到下一个处理程序。

当请求到达**system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**类时， **system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**将根据更新的请求方法路由请求。

## <a name="example-adding-a-custom-response-header"></a>示例：添加自定义响应标头

下面是一个消息处理程序，它将自定义标头添加到每个响应消息：

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

首先，处理程序调用 `base.SendAsync` 将请求传递给内部消息处理程序。 内部处理程序返回响应消息，但它使用**任务&lt;t&gt;** 对象以异步方式执行此操作。 直到 `base.SendAsync` 异步完成后，响应消息才可用。

此示例使用**await**关键字在 `SendAsync` 完成后以异步方式执行工作。 如果目标为 .NET Framework 4.0，请使用**任务**&lt;t&gt; **。System.threading.tasks.task.continuewith**方法：

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>示例：检查 API 密钥

某些 web 服务要求客户端在其请求中包含 API 密钥。 下面的示例演示消息处理程序如何检查对有效 API 密钥的请求：

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

此处理程序在 URI 查询字符串中查找 API 密钥。 （在本示例中，我们假定密钥是一个静态字符串。 实际实现可能会使用更复杂的验证。）如果查询字符串包含该键，则处理程序将该请求传递给内部处理程序。

如果请求没有有效的密钥，则处理程序将创建状态为403，禁止的响应消息。 在这种情况下，处理程序不会调用 `base.SendAsync`，因此内部处理程序绝不会接收请求，也不会执行控制器。 因此，控制器可以假定所有传入请求都有有效的 API 密钥。

> [!NOTE]
> 如果 API 密钥仅适用于某些控制器操作，请考虑使用操作筛选器而不是消息处理程序。 操作筛选器在执行 URI 路由之后运行。

## <a name="per-route-message-handlers"></a>按路由消息处理程序

**HttpConfiguration**集合中的处理程序全局应用。

此外，还可以在定义路由时向特定路由添加消息处理程序：

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

在此示例中，如果请求 URI 与 "Route2" 匹配，则会将请求调度到 `MessageHandler2`。 下图显示了这两个路由的管道：

![](http-message-handlers/_static/image4.png)

请注意，`MessageHandler2` 替换默认**system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**。 在此示例中，`MessageHandler2` 将创建响应，与 "Route2" 匹配的请求永远不会发送到控制器。 这使你可以将整个 Web API 控制器机制替换为你自己的自定义终结点。

或者，每个路由消息处理程序可以委托给**system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**，后者随后会调度到控制器。

![](http-message-handlers/_static/image5.png)

下面的代码演示如何配置此路由：

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
