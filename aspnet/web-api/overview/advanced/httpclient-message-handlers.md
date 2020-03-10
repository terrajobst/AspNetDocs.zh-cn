---
uid: web-api/overview/advanced/httpclient-message-handlers
title: HttpClient 消息处理程序 ASP.NET Web API-ASP.NET 4。x
author: MikeWasson
description: 为 ASP.NET 4.x 中的 ASP.NET Web API 创建自定义消息处理程序
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449276"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="3f5e0-103">ASP.NET Web API 中的 HttpClient 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="3f5e0-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="3f5e0-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3f5e0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3f5e0-105">*消息处理程序*是接收 http 请求并返回 http 响应的类。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="3f5e0-106">通常，一系列消息处理程序链接在一起。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="3f5e0-107">第一个处理程序接收 HTTP 请求，进行一些处理，并向下一个处理程序提供请求。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="3f5e0-108">在某个时间点，将创建响应，并在链中返回。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="3f5e0-109">此模式称为*委托*处理程序。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="3f5e0-110">在客户端， **HttpClient**类使用消息处理程序来处理请求。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="3f5e0-111">默认处理程序是**HttpClientHandler**，它通过网络发送请求并从服务器获取响应。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="3f5e0-112">可以将自定义消息处理程序插入客户端管道：</span><span class="sxs-lookup"><span data-stu-id="3f5e0-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="3f5e0-113">ASP.NET Web API 还会在服务器端使用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="3f5e0-114">有关详细信息，请参阅[HTTP 消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="3f5e0-115">自定义消息处理程序</span><span class="sxs-lookup"><span data-stu-id="3f5e0-115">Custom Message Handlers</span></span>

<span data-ttu-id="3f5e0-116">若要编写自定义消息处理程序，请从**DelegatingHandler**派生并重写**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="3f5e0-117">下面是方法签名：</span><span class="sxs-lookup"><span data-stu-id="3f5e0-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="3f5e0-118">方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="3f5e0-119">典型的实现会执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3f5e0-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="3f5e0-120">处理请求消息。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-120">Process the request message.</span></span>
2. <span data-ttu-id="3f5e0-121">调用 `base.SendAsync` 将请求发送到内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="3f5e0-122">内部处理程序返回响应消息。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-122">The inner handler returns a response message.</span></span> <span data-ttu-id="3f5e0-123">（此步骤是异步的。）</span><span class="sxs-lookup"><span data-stu-id="3f5e0-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="3f5e0-124">处理响应并将其返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="3f5e0-125">下面的示例演示将自定义标头添加到传出请求的消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="3f5e0-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="3f5e0-126">对 `base.SendAsync` 的调用是异步的。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="3f5e0-127">如果处理程序在此调用后执行任何操作，请使用**await**关键字在方法完成后继续执行。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="3f5e0-128">下面的示例演示了记录错误代码的处理程序。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="3f5e0-129">日志记录本身并不是很有趣，但此示例演示如何获取处理程序内的响应。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="3f5e0-130">向客户端管道添加消息处理程序</span><span class="sxs-lookup"><span data-stu-id="3f5e0-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="3f5e0-131">若要将自定义处理程序添加到**HttpClient**，请使用**HttpClientFactory**方法：</span><span class="sxs-lookup"><span data-stu-id="3f5e0-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="3f5e0-132">消息处理程序按您将其传递到**Create**方法的顺序进行调用。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="3f5e0-133">由于处理程序是嵌套的，因此响应消息以其他方向传输。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="3f5e0-134">也就是说，最后一个处理程序是获取响应消息的第一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="3f5e0-134">That is, the last handler is the first to get the response message.</span></span>
