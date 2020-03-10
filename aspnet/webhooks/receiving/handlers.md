---
uid: webhooks/receiving/handlers
title: ASP.NET Webhook 处理程序 |Microsoft Docs
author: rick-anderson
description: 如何处理 ASP.NET Webhook 中的请求。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518030"
---
# <a name="aspnet-webhooks-handlers"></a>ASP.NET Webhook 处理程序

Webhook 请求经过 WebHook 接收方的验证后，即可由用户代码进行处理。 这是*处理程序*的位置。 处理程序从[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)接口派生，但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)类，而不是直接从接口派生。

WebHook 请求可由一个或多个处理程序处理。 处理程序的调用顺序是根据其各自的*顺序*属性，从最低到最高，其中 order 是一个简单的整数（建议介于1到100之间）：

![WebHook 处理程序顺序属性关系图](_static/Handlers.png)

处理程序可以选择对 WebHookHandlerContext 设置*Response*属性，这将导致处理停止并将响应作为 HTTP 响应发送回 WebHook。 在上面的示例中，处理程序 C 不会被调用，因为它的顺序高于 B，而 B 设置响应。

设置响应通常仅适用于 Webhook，其中的响应可以将信息携带回原始 API。 例如，在 Webhook 的情况下，将响应回发到 WebHook 来源的通道。 如果处理程序只希望接收来自该特定接收方的 Webhook，则可以设置接收器属性。 如果未设置，则会为所有这些接收者调用它们。

响应的另一种常见用途是使用*410*的响应，以指示该 WebHook 不再处于活动状态，并且不会再提交更多请求。

默认情况下，所有 WebHook 接收方都将调用处理程序。 但是，如果将*接收方*属性设置为处理程序的名称，则该处理程序将仅接收来自该接收方的 WebHook 请求。

## <a name="processing-a-webhook"></a>处理 WebHook

调用处理程序时，它将获取一个[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) ，其中包含有关 WebHook 请求的信息。 数据通常是 HTTP 请求正文，可从*data*属性获得。

数据类型通常是 JSON 或 HTML 窗体数据，但可以根据需要将其转换为更具体的类型。 例如，ASP.NET Webhook 生成的自定义 Webhook 可强制转换为类型[CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) ，如下所示：

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>排队处理

如果在少数几秒钟内没有生成响应，则大多数 WebHook 发送程序都将重新发送 WebHook。 这意味着处理程序必须在该时间范围内完成处理，而不是再次调用它。

如果处理需要更长时间，或者单独处理，则可以使用[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)将 WebHook 请求提交到队列（例如[Azure 存储队列](https://msdn.microsoft.com/library/azure/dd179353.aspx)）。

下面提供了[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)实现的大纲：

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
