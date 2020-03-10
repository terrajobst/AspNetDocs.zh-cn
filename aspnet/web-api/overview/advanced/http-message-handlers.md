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
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="941bb-103">ASP.NET Web API 中的 HTTP 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="941bb-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="941bb-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="941bb-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="941bb-105">*消息处理程序*是接收 http 请求并返回 http 响应的类。</span><span class="sxs-lookup"><span data-stu-id="941bb-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="941bb-106">消息处理程序派生自抽象**HttpMessageHandler**类。</span><span class="sxs-lookup"><span data-stu-id="941bb-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="941bb-107">通常，一系列消息处理程序链接在一起。</span><span class="sxs-lookup"><span data-stu-id="941bb-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="941bb-108">第一个处理程序接收 HTTP 请求，进行一些处理，并向下一个处理程序提供请求。</span><span class="sxs-lookup"><span data-stu-id="941bb-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="941bb-109">在某个时间点，将创建响应，并在链中返回。</span><span class="sxs-lookup"><span data-stu-id="941bb-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="941bb-110">此模式称为*委托*处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="941bb-111">服务器端消息处理程序</span><span class="sxs-lookup"><span data-stu-id="941bb-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="941bb-112">在服务器端，Web API 管道使用某些内置消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="941bb-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="941bb-113">**HttpServer**获取来自主机的请求。</span><span class="sxs-lookup"><span data-stu-id="941bb-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="941bb-114">**HttpRoutingDispatcher**根据路由调度请求。</span><span class="sxs-lookup"><span data-stu-id="941bb-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="941bb-115">**System.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**将请求发送到 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="941bb-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="941bb-116">您可以向管道添加自定义处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="941bb-117">消息处理程序适用于在 HTTP 消息级别（而不是控制器操作）上操作的交叉切削问题。</span><span class="sxs-lookup"><span data-stu-id="941bb-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="941bb-118">例如，消息处理程序可以：</span><span class="sxs-lookup"><span data-stu-id="941bb-118">For example, a message handler might:</span></span>

- <span data-ttu-id="941bb-119">读取或修改请求标头。</span><span class="sxs-lookup"><span data-stu-id="941bb-119">Read or modify request headers.</span></span>
- <span data-ttu-id="941bb-120">向响应添加响应标头。</span><span class="sxs-lookup"><span data-stu-id="941bb-120">Add a response header to responses.</span></span>
- <span data-ttu-id="941bb-121">在请求到达控制器之前对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="941bb-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="941bb-122">此关系图显示插入到管道中的两个自定义处理程序：</span><span class="sxs-lookup"><span data-stu-id="941bb-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="941bb-123">在客户端，HttpClient 还使用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="941bb-124">有关详细信息，请参阅[HttpClient 消息处理程序](httpclient-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="941bb-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="941bb-125">自定义消息处理程序</span><span class="sxs-lookup"><span data-stu-id="941bb-125">Custom Message Handlers</span></span>

<span data-ttu-id="941bb-126">若要编写自定义消息处理程序，请从**DelegatingHandler**派生并重写**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="941bb-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="941bb-127">此方法具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="941bb-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="941bb-128">方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="941bb-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="941bb-129">典型的实现会执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="941bb-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="941bb-130">处理请求消息。</span><span class="sxs-lookup"><span data-stu-id="941bb-130">Process the request message.</span></span>
2. <span data-ttu-id="941bb-131">调用 `base.SendAsync` 将请求发送到内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="941bb-132">内部处理程序返回响应消息。</span><span class="sxs-lookup"><span data-stu-id="941bb-132">The inner handler returns a response message.</span></span> <span data-ttu-id="941bb-133">（此步骤是异步的。）</span><span class="sxs-lookup"><span data-stu-id="941bb-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="941bb-134">处理响应并将其返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="941bb-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="941bb-135">下面是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="941bb-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="941bb-136">对 `base.SendAsync` 的调用是异步的。</span><span class="sxs-lookup"><span data-stu-id="941bb-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="941bb-137">如果处理程序在此调用后执行任何操作，请使用**await**关键字，如所示。</span><span class="sxs-lookup"><span data-stu-id="941bb-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="941bb-138">委托处理程序还可以跳过内部处理程序并直接创建响应：</span><span class="sxs-lookup"><span data-stu-id="941bb-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="941bb-139">如果委托处理程序在没有调用 `base.SendAsync`的情况下创建响应，则该请求将跳过管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="941bb-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="941bb-140">这对于验证请求的处理程序（创建错误响应）很有用。</span><span class="sxs-lookup"><span data-stu-id="941bb-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="941bb-141">向管道添加处理程序</span><span class="sxs-lookup"><span data-stu-id="941bb-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="941bb-142">若要在服务器端添加消息处理程序，请将该处理程序添加到**HttpConfiguration**集合。</span><span class="sxs-lookup"><span data-stu-id="941bb-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="941bb-143">如果使用了 "ASP.NET MVC 4 Web 应用程序" 模板来创建项目，可以在**webapiconfig.cs**类中执行此操作：</span><span class="sxs-lookup"><span data-stu-id="941bb-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="941bb-144">消息处理程序的调用顺序与它们在**MessageHandlers**集合中出现的顺序相同。</span><span class="sxs-lookup"><span data-stu-id="941bb-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="941bb-145">由于它们是嵌套的，因此响应消息以其他方向传输。</span><span class="sxs-lookup"><span data-stu-id="941bb-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="941bb-146">也就是说，最后一个处理程序是获取响应消息的第一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="941bb-147">请注意，不需要设置内部处理程序;Web API 框架会自动连接消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="941bb-148">如果你是[自承载](../older-versions/self-host-a-web-api.md)，请创建**HttpSelfHostConfiguration**类的实例，并将该处理程序添加到**MessageHandlers**集合中。</span><span class="sxs-lookup"><span data-stu-id="941bb-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="941bb-149">现在，让我们看一些自定义消息处理程序示例。</span><span class="sxs-lookup"><span data-stu-id="941bb-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="941bb-150">示例： X HTTP-方法-Override</span><span class="sxs-lookup"><span data-stu-id="941bb-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="941bb-151">X HTTP 方法-重写是非标准的 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="941bb-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="941bb-152">它适用于不能发送某些 HTTP 请求类型的客户端，例如 PUT 或 DELETE。</span><span class="sxs-lookup"><span data-stu-id="941bb-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="941bb-153">相反，客户端发送 POST 请求，并将 X HTTP 方法重写标头设置为所需的方法。</span><span class="sxs-lookup"><span data-stu-id="941bb-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="941bb-154">例如:</span><span class="sxs-lookup"><span data-stu-id="941bb-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="941bb-155">下面是添加对 X HTTP 方法重写的支持的消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="941bb-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="941bb-156">在**SendAsync**方法中，处理程序检查请求消息是 POST 请求，还是包含 X HTTP 方法-重写标头。</span><span class="sxs-lookup"><span data-stu-id="941bb-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="941bb-157">如果是，它将验证标头值，然后修改请求方法。</span><span class="sxs-lookup"><span data-stu-id="941bb-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="941bb-158">最后，处理程序调用 `base.SendAsync` 将消息传递到下一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="941bb-159">当请求到达**system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**类时， **system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**将根据更新的请求方法路由请求。</span><span class="sxs-lookup"><span data-stu-id="941bb-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="941bb-160">示例：添加自定义响应标头</span><span class="sxs-lookup"><span data-stu-id="941bb-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="941bb-161">下面是一个消息处理程序，它将自定义标头添加到每个响应消息：</span><span class="sxs-lookup"><span data-stu-id="941bb-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="941bb-162">首先，处理程序调用 `base.SendAsync` 将请求传递给内部消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="941bb-163">内部处理程序返回响应消息，但它使用**任务&lt;t&gt;** 对象以异步方式执行此操作。</span><span class="sxs-lookup"><span data-stu-id="941bb-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="941bb-164">直到 `base.SendAsync` 异步完成后，响应消息才可用。</span><span class="sxs-lookup"><span data-stu-id="941bb-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="941bb-165">此示例使用**await**关键字在 `SendAsync` 完成后以异步方式执行工作。</span><span class="sxs-lookup"><span data-stu-id="941bb-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="941bb-166">如果目标为 .NET Framework 4.0，请使用**任务**&lt;t&gt; **。System.threading.tasks.task.continuewith**方法：</span><span class="sxs-lookup"><span data-stu-id="941bb-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="941bb-167">示例：检查 API 密钥</span><span class="sxs-lookup"><span data-stu-id="941bb-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="941bb-168">某些 web 服务要求客户端在其请求中包含 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="941bb-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="941bb-169">下面的示例演示消息处理程序如何检查对有效 API 密钥的请求：</span><span class="sxs-lookup"><span data-stu-id="941bb-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="941bb-170">此处理程序在 URI 查询字符串中查找 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="941bb-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="941bb-171">（在本示例中，我们假定密钥是一个静态字符串。</span><span class="sxs-lookup"><span data-stu-id="941bb-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="941bb-172">实际实现可能会使用更复杂的验证。）如果查询字符串包含该键，则处理程序将该请求传递给内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="941bb-173">如果请求没有有效的密钥，则处理程序将创建状态为403，禁止的响应消息。</span><span class="sxs-lookup"><span data-stu-id="941bb-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="941bb-174">在这种情况下，处理程序不会调用 `base.SendAsync`，因此内部处理程序绝不会接收请求，也不会执行控制器。</span><span class="sxs-lookup"><span data-stu-id="941bb-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="941bb-175">因此，控制器可以假定所有传入请求都有有效的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="941bb-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="941bb-176">如果 API 密钥仅适用于某些控制器操作，请考虑使用操作筛选器而不是消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="941bb-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="941bb-177">操作筛选器在执行 URI 路由之后运行。</span><span class="sxs-lookup"><span data-stu-id="941bb-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="941bb-178">按路由消息处理程序</span><span class="sxs-lookup"><span data-stu-id="941bb-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="941bb-179">**HttpConfiguration**集合中的处理程序全局应用。</span><span class="sxs-lookup"><span data-stu-id="941bb-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="941bb-180">此外，还可以在定义路由时向特定路由添加消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="941bb-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="941bb-181">在此示例中，如果请求 URI 与 "Route2" 匹配，则会将请求调度到 `MessageHandler2`。</span><span class="sxs-lookup"><span data-stu-id="941bb-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="941bb-182">下图显示了这两个路由的管道：</span><span class="sxs-lookup"><span data-stu-id="941bb-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="941bb-183">请注意，`MessageHandler2` 替换默认**system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**。</span><span class="sxs-lookup"><span data-stu-id="941bb-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="941bb-184">在此示例中，`MessageHandler2` 将创建响应，与 "Route2" 匹配的请求永远不会发送到控制器。</span><span class="sxs-lookup"><span data-stu-id="941bb-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="941bb-185">这使你可以将整个 Web API 控制器机制替换为你自己的自定义终结点。</span><span class="sxs-lookup"><span data-stu-id="941bb-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="941bb-186">或者，每个路由消息处理程序可以委托给**system.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync**，后者随后会调度到控制器。</span><span class="sxs-lookup"><span data-stu-id="941bb-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="941bb-187">下面的代码演示如何配置此路由：</span><span class="sxs-lookup"><span data-stu-id="941bb-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
