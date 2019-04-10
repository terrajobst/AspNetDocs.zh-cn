---
uid: web-api/overview/advanced/httpclient-message-handlers
title: HttpClient 消息处理程序在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 为在 ASP.NET 中的 ASP.NET Web API 创建自定义消息处理程序 4.x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: bd52396064cd7007ee17705ba86b02aaf27cb4f0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401720"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="72d06-103">ASP.NET Web API 中的 HttpClient 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="72d06-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="72d06-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="72d06-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="72d06-105">一个*消息处理程序*是收到 HTTP 请求并返回 HTTP 响应的类。</span><span class="sxs-lookup"><span data-stu-id="72d06-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="72d06-106">通常情况下，消息处理程序的一系列链接在一起。</span><span class="sxs-lookup"><span data-stu-id="72d06-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="72d06-107">第一个处理程序收到 HTTP 请求、 执行某些处理，并提供请求下一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="72d06-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="72d06-108">在某些时候，响应创建，并将返回链。</span><span class="sxs-lookup"><span data-stu-id="72d06-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="72d06-109">此模式称为*委派*处理程序。</span><span class="sxs-lookup"><span data-stu-id="72d06-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="72d06-110">客户端侧**HttpClient**类使用消息处理程序来处理请求。</span><span class="sxs-lookup"><span data-stu-id="72d06-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="72d06-111">默认处理程序是**HttpClientHandler**，其通过网络发送请求，并从服务器获取响应。</span><span class="sxs-lookup"><span data-stu-id="72d06-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="72d06-112">可以插入到客户端管道的自定义消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="72d06-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="72d06-113">ASP.NET Web API 在服务器端还使用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="72d06-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="72d06-114">有关详细信息，请参阅[HTTP 消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="72d06-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="72d06-115">自定义消息处理程序</span><span class="sxs-lookup"><span data-stu-id="72d06-115">Custom Message Handlers</span></span>

<span data-ttu-id="72d06-116">若要编写自定义消息处理程序，从派生**System.Net.Http.DelegatingHandler**并重写**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="72d06-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="72d06-117">以下是方法签名：</span><span class="sxs-lookup"><span data-stu-id="72d06-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="72d06-118">该方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="72d06-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="72d06-119">典型实现执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="72d06-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="72d06-120">处理请求消息。</span><span class="sxs-lookup"><span data-stu-id="72d06-120">Process the request message.</span></span>
2. <span data-ttu-id="72d06-121">调用`base.SendAsync`将请求发送到的内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="72d06-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="72d06-122">内部处理程序返回响应消息。</span><span class="sxs-lookup"><span data-stu-id="72d06-122">The inner handler returns a response message.</span></span> <span data-ttu-id="72d06-123">（此步骤是异步的。）</span><span class="sxs-lookup"><span data-stu-id="72d06-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="72d06-124">处理响应并将其返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="72d06-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="72d06-125">下面的示例显示了将自定义标头添加到传出请求的消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="72d06-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="72d06-126">对调用`base.SendAsync`是异步的。</span><span class="sxs-lookup"><span data-stu-id="72d06-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="72d06-127">如果此调用后，该处理程序执行任何工作，使用**await**关键字在方法完成后恢复执行。</span><span class="sxs-lookup"><span data-stu-id="72d06-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="72d06-128">下面的示例演示的处理程序日志错误代码。</span><span class="sxs-lookup"><span data-stu-id="72d06-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="72d06-129">日志记录本身不是很有趣，但该示例演示如何获取在处理程序的响应。</span><span class="sxs-lookup"><span data-stu-id="72d06-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="72d06-130">将消息处理程序添加到客户端管道</span><span class="sxs-lookup"><span data-stu-id="72d06-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="72d06-131">若要添加到自定义处理程序**HttpClient**，使用**HttpClientFactory.Create**方法：</span><span class="sxs-lookup"><span data-stu-id="72d06-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="72d06-132">消息处理程序调用传递到它们的顺序**创建**方法。</span><span class="sxs-lookup"><span data-stu-id="72d06-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="72d06-133">嵌套的处理程序，因为在另一个方向传输时的响应消息。</span><span class="sxs-lookup"><span data-stu-id="72d06-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="72d06-134">也就是说，最后一个处理程序是获取响应消息的第一个。</span><span class="sxs-lookup"><span data-stu-id="72d06-134">That is, the last handler is the first to get the response message.</span></span>
