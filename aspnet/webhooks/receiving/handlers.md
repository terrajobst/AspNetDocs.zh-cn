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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="2cef2-103">ASP.NET Webhook 处理程序</span><span class="sxs-lookup"><span data-stu-id="2cef2-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="2cef2-104">Webhook 请求经过 WebHook 接收方的验证后，即可由用户代码进行处理。</span><span class="sxs-lookup"><span data-stu-id="2cef2-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="2cef2-105">这是*处理程序*的位置。</span><span class="sxs-lookup"><span data-stu-id="2cef2-105">This is where *handlers* come in.</span></span> <span data-ttu-id="2cef2-106">处理程序从[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)接口派生，但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)类，而不是直接从接口派生。</span><span class="sxs-lookup"><span data-stu-id="2cef2-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="2cef2-107">WebHook 请求可由一个或多个处理程序处理。</span><span class="sxs-lookup"><span data-stu-id="2cef2-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="2cef2-108">处理程序的调用顺序是根据其各自的*顺序*属性，从最低到最高，其中 order 是一个简单的整数（建议介于1到100之间）：</span><span class="sxs-lookup"><span data-stu-id="2cef2-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 处理程序顺序属性关系图](_static/Handlers.png)

<span data-ttu-id="2cef2-110">处理程序可以选择对 WebHookHandlerContext 设置*Response*属性，这将导致处理停止并将响应作为 HTTP 响应发送回 WebHook。</span><span class="sxs-lookup"><span data-stu-id="2cef2-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="2cef2-111">在上面的示例中，处理程序 C 不会被调用，因为它的顺序高于 B，而 B 设置响应。</span><span class="sxs-lookup"><span data-stu-id="2cef2-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="2cef2-112">设置响应通常仅适用于 Webhook，其中的响应可以将信息携带回原始 API。</span><span class="sxs-lookup"><span data-stu-id="2cef2-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="2cef2-113">例如，在 Webhook 的情况下，将响应回发到 WebHook 来源的通道。</span><span class="sxs-lookup"><span data-stu-id="2cef2-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="2cef2-114">如果处理程序只希望接收来自该特定接收方的 Webhook，则可以设置接收器属性。</span><span class="sxs-lookup"><span data-stu-id="2cef2-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="2cef2-115">如果未设置，则会为所有这些接收者调用它们。</span><span class="sxs-lookup"><span data-stu-id="2cef2-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="2cef2-116">响应的另一种常见用途是使用*410*的响应，以指示该 WebHook 不再处于活动状态，并且不会再提交更多请求。</span><span class="sxs-lookup"><span data-stu-id="2cef2-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="2cef2-117">默认情况下，所有 WebHook 接收方都将调用处理程序。</span><span class="sxs-lookup"><span data-stu-id="2cef2-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="2cef2-118">但是，如果将*接收方*属性设置为处理程序的名称，则该处理程序将仅接收来自该接收方的 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="2cef2-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="2cef2-119">处理 WebHook</span><span class="sxs-lookup"><span data-stu-id="2cef2-119">Processing a WebHook</span></span>

<span data-ttu-id="2cef2-120">调用处理程序时，它将获取一个[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) ，其中包含有关 WebHook 请求的信息。</span><span class="sxs-lookup"><span data-stu-id="2cef2-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="2cef2-121">数据通常是 HTTP 请求正文，可从*data*属性获得。</span><span class="sxs-lookup"><span data-stu-id="2cef2-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="2cef2-122">数据类型通常是 JSON 或 HTML 窗体数据，但可以根据需要将其转换为更具体的类型。</span><span class="sxs-lookup"><span data-stu-id="2cef2-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="2cef2-123">例如，ASP.NET Webhook 生成的自定义 Webhook 可强制转换为类型[CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2cef2-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="2cef2-124">排队处理</span><span class="sxs-lookup"><span data-stu-id="2cef2-124">Queued Processing</span></span>

<span data-ttu-id="2cef2-125">如果在少数几秒钟内没有生成响应，则大多数 WebHook 发送程序都将重新发送 WebHook。</span><span class="sxs-lookup"><span data-stu-id="2cef2-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="2cef2-126">这意味着处理程序必须在该时间范围内完成处理，而不是再次调用它。</span><span class="sxs-lookup"><span data-stu-id="2cef2-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="2cef2-127">如果处理需要更长时间，或者单独处理，则可以使用[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)将 WebHook 请求提交到队列（例如[Azure 存储队列](https://msdn.microsoft.com/library/azure/dd179353.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="2cef2-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="2cef2-128">下面提供了[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)实现的大纲：</span><span class="sxs-lookup"><span data-stu-id="2cef2-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
