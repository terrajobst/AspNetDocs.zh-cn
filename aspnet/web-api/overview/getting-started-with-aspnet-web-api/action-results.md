---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: 操作会导致 Web API 2 的 ASP.NET 4.x
author: MikeWasson
description: 描述如何 ASP.NET Web API 将返回值转换到 ASP.NET 中的 HTTP 响应消息的控制器操作从 4.x。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 87f71938a5c5f38d3a456ba9339540f67e236e1a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400888"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="fd070-103">Web API 2 的操作结果</span><span class="sxs-lookup"><span data-stu-id="fd070-103">Action Results in Web API 2</span></span>

<span data-ttu-id="fd070-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fd070-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fd070-105">本主题介绍如何 ASP.NET Web API 都将转换为 HTTP 响应消息的控制器操作的返回值。</span><span class="sxs-lookup"><span data-stu-id="fd070-105">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="fd070-106">Web API 控制器操作可以返回以下任一项：</span><span class="sxs-lookup"><span data-stu-id="fd070-106">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="fd070-107">void</span><span class="sxs-lookup"><span data-stu-id="fd070-107">void</span></span>
2. <span data-ttu-id="fd070-108">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="fd070-108">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="fd070-109">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="fd070-109">**IHttpActionResult**</span></span>
4. <span data-ttu-id="fd070-110">某些其他类型</span><span class="sxs-lookup"><span data-stu-id="fd070-110">Some other type</span></span>

<span data-ttu-id="fd070-111">具体取决于以下哪种返回时，Web API 使用另一种机制来创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="fd070-111">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="fd070-112">返回类型</span><span class="sxs-lookup"><span data-stu-id="fd070-112">Return type</span></span> | <span data-ttu-id="fd070-113">Web API 创建响应的方式</span><span class="sxs-lookup"><span data-stu-id="fd070-113">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="fd070-114">void</span><span class="sxs-lookup"><span data-stu-id="fd070-114">void</span></span> | <span data-ttu-id="fd070-115">返回空 204 （无内容）</span><span class="sxs-lookup"><span data-stu-id="fd070-115">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="fd070-116">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="fd070-116">**HttpResponseMessage**</span></span> | <span data-ttu-id="fd070-117">转换为直接 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="fd070-117">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="fd070-118">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="fd070-118">**IHttpActionResult**</span></span> | <span data-ttu-id="fd070-119">调用**ExecuteAsync**来创建**HttpResponseMessage**，然后将转换为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="fd070-119">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="fd070-120">其他类型</span><span class="sxs-lookup"><span data-stu-id="fd070-120">Other type</span></span> | <span data-ttu-id="fd070-121">将序列化的返回值写入到响应正文中;返回 200 （正常）。</span><span class="sxs-lookup"><span data-stu-id="fd070-121">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="fd070-122">本主题的其余部分将介绍更多详细信息中的每个选项。</span><span class="sxs-lookup"><span data-stu-id="fd070-122">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="fd070-123">void</span><span class="sxs-lookup"><span data-stu-id="fd070-123">void</span></span>

<span data-ttu-id="fd070-124">如果返回类型为`void`，Web API 仅返回状态代码 204 （无内容） 的空 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="fd070-124">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="fd070-125">示例控制器：</span><span class="sxs-lookup"><span data-stu-id="fd070-125">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="fd070-126">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="fd070-126">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="fd070-127">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="fd070-127">HttpResponseMessage</span></span>

<span data-ttu-id="fd070-128">如果操作返回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 的返回值直接将转换为 HTTP 响应消息中，使用的属性**HttpResponseMessage**要填充对象响应。</span><span class="sxs-lookup"><span data-stu-id="fd070-128">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="fd070-129">此选项可提供大量控制的响应消息。</span><span class="sxs-lookup"><span data-stu-id="fd070-129">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="fd070-130">例如，以下控制器操作设置的缓存控制标头。</span><span class="sxs-lookup"><span data-stu-id="fd070-130">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="fd070-131">响应：</span><span class="sxs-lookup"><span data-stu-id="fd070-131">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="fd070-132">如果传递到的域模型**CreateResponse**方法中，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)将写入响应正文的序列化的模型。</span><span class="sxs-lookup"><span data-stu-id="fd070-132">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="fd070-133">Web API 使用 Accept 标头中请求选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="fd070-133">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="fd070-134">有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="fd070-134">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="fd070-135">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="fd070-135">IHttpActionResult</span></span>

<span data-ttu-id="fd070-136">**IHttpActionResult** Web API 2 中引入了接口。</span><span class="sxs-lookup"><span data-stu-id="fd070-136">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="fd070-137">从根本上来说，它定义**HttpResponseMessage**工厂。</span><span class="sxs-lookup"><span data-stu-id="fd070-137">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="fd070-138">以下是使用的一些优势**IHttpActionResult**接口：</span><span class="sxs-lookup"><span data-stu-id="fd070-138">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="fd070-139">可简化[单元测试](../testing-and-debugging/unit-testing-controllers-in-web-api.md)你的控制器。</span><span class="sxs-lookup"><span data-stu-id="fd070-139">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="fd070-140">将移动到单独的类创建 HTTP 响应的常见逻辑。</span><span class="sxs-lookup"><span data-stu-id="fd070-140">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="fd070-141">隐藏构造响应的低级别的详细信息，从而使更清晰，控制器操作的目的。</span><span class="sxs-lookup"><span data-stu-id="fd070-141">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="fd070-142">**IHttpActionResult**包含一个方法**ExecuteAsync**，以便以异步方式创建**HttpResponseMessage**实例。</span><span class="sxs-lookup"><span data-stu-id="fd070-142">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="fd070-143">如果控制器操作返回**IHttpActionResult**，Web API 调用**ExecuteAsync**方法创建**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="fd070-143">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="fd070-144">然后它会将转换**HttpResponseMessage**到 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="fd070-144">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="fd070-145">下面是一个简单的实现**IHttpActionResult**创建纯文本响应：</span><span class="sxs-lookup"><span data-stu-id="fd070-145">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="fd070-146">示例控制器操作：</span><span class="sxs-lookup"><span data-stu-id="fd070-146">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="fd070-147">响应：</span><span class="sxs-lookup"><span data-stu-id="fd070-147">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="fd070-148">更多时候，您将使用**IHttpActionResult**中定义的实现**[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 命名空间。</span><span class="sxs-lookup"><span data-stu-id="fd070-148">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="fd070-149">**ApiController**类定义返回这些内置操作结果的帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="fd070-149">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="fd070-150">在以下示例中，如果请求不匹配现有的产品 ID，在控制器调用[ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)创建 404 （未找到） 响应。</span><span class="sxs-lookup"><span data-stu-id="fd070-150">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="fd070-151">否则，控制器会调用[ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx)，用于创建 200 （正常） 响应，包含该产品。</span><span class="sxs-lookup"><span data-stu-id="fd070-151">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="fd070-152">其他的返回类型</span><span class="sxs-lookup"><span data-stu-id="fd070-152">Other Return Types</span></span>

<span data-ttu-id="fd070-153">对于所有其他返回类型，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)要序列化的返回值。</span><span class="sxs-lookup"><span data-stu-id="fd070-153">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="fd070-154">Web API 将序列化的值写入到响应正文。</span><span class="sxs-lookup"><span data-stu-id="fd070-154">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="fd070-155">响应状态代码为 200 （正常）。</span><span class="sxs-lookup"><span data-stu-id="fd070-155">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="fd070-156">此方法的缺点是，不能直接返回错误代码，如 404。</span><span class="sxs-lookup"><span data-stu-id="fd070-156">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="fd070-157">但是，您可能会引发**HttpResponseException**的错误代码。</span><span class="sxs-lookup"><span data-stu-id="fd070-157">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="fd070-158">有关详细信息，请参阅[ASP.NET Web API 中的异常处理](../error-handling/exception-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="fd070-158">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="fd070-159">Web API 使用 Accept 标头中请求选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="fd070-159">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="fd070-160">有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="fd070-160">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="fd070-161">示例请求</span><span class="sxs-lookup"><span data-stu-id="fd070-161">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="fd070-162">示例响应：</span><span class="sxs-lookup"><span data-stu-id="fd070-162">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
