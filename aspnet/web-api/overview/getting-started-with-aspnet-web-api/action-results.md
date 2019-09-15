---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2 中的操作结果-ASP.NET 4。x
author: MikeWasson
description: 介绍 ASP.NET Web API 如何将控制器操作的返回值转换为 ASP.NET 4.x 中的 HTTP 响应消息。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985841"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="800c0-103">Web API 2 的操作结果</span><span class="sxs-lookup"><span data-stu-id="800c0-103">Action Results in Web API 2</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="800c0-104">本主题介绍 ASP.NET Web API 如何将控制器操作的返回值转换为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="800c0-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="800c0-105">Web API 控制器操作可以返回以下任何内容：</span><span class="sxs-lookup"><span data-stu-id="800c0-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="800c0-106">void</span><span class="sxs-lookup"><span data-stu-id="800c0-106">void</span></span>
2. <span data-ttu-id="800c0-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="800c0-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="800c0-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="800c0-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="800c0-109">其他类型</span><span class="sxs-lookup"><span data-stu-id="800c0-109">Some other type</span></span>

<span data-ttu-id="800c0-110">根据返回的这种情况，Web API 将使用不同的机制来创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="800c0-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="800c0-111">返回类型</span><span class="sxs-lookup"><span data-stu-id="800c0-111">Return type</span></span> | <span data-ttu-id="800c0-112">Web API 如何创建响应</span><span class="sxs-lookup"><span data-stu-id="800c0-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="800c0-113">void</span><span class="sxs-lookup"><span data-stu-id="800c0-113">void</span></span> | <span data-ttu-id="800c0-114">返回空的204（无内容）</span><span class="sxs-lookup"><span data-stu-id="800c0-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="800c0-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="800c0-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="800c0-116">直接转换为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="800c0-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="800c0-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="800c0-117">**IHttpActionResult**</span></span> | <span data-ttu-id="800c0-118">调用**ExecuteAsync**创建**HttpResponseMessage**，然后将其转换为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="800c0-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="800c0-119">其他类型</span><span class="sxs-lookup"><span data-stu-id="800c0-119">Other type</span></span> | <span data-ttu-id="800c0-120">将序列化的返回值写入响应正文;返回200（OK）。</span><span class="sxs-lookup"><span data-stu-id="800c0-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="800c0-121">本主题的其余部分将更详细地介绍每个选项。</span><span class="sxs-lookup"><span data-stu-id="800c0-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="800c0-122">void</span><span class="sxs-lookup"><span data-stu-id="800c0-122">void</span></span>

<span data-ttu-id="800c0-123">如果返回类型为`void`，Web API 只会返回一个空 HTTP 响应，状态代码为204（无内容）。</span><span class="sxs-lookup"><span data-stu-id="800c0-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="800c0-124">示例控制器：</span><span class="sxs-lookup"><span data-stu-id="800c0-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="800c0-125">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="800c0-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="800c0-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="800c0-126">HttpResponseMessage</span></span>

<span data-ttu-id="800c0-127">如果操作返回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 会将返回值直接转换为 HTTP 响应消息，并使用**HttpResponseMessage**对象的属性来填充响应。</span><span class="sxs-lookup"><span data-stu-id="800c0-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="800c0-128">此选项提供了对响应消息的大量控制。</span><span class="sxs-lookup"><span data-stu-id="800c0-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="800c0-129">例如，以下控制器操作设置缓存控制标头。</span><span class="sxs-lookup"><span data-stu-id="800c0-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="800c0-130">响应：</span><span class="sxs-lookup"><span data-stu-id="800c0-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="800c0-131">如果向**CreateResponse**方法传递域模型，Web API 将使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)将序列化模型写入响应正文。</span><span class="sxs-lookup"><span data-stu-id="800c0-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="800c0-132">Web API 使用请求中的 Accept 标头来选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="800c0-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="800c0-133">有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="800c0-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="800c0-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="800c0-134">IHttpActionResult</span></span>

<span data-ttu-id="800c0-135">Web API 2 中引入了**IHttpActionResult**接口。</span><span class="sxs-lookup"><span data-stu-id="800c0-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="800c0-136">实质上，它定义了**HttpResponseMessage**工厂。</span><span class="sxs-lookup"><span data-stu-id="800c0-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="800c0-137">下面是使用**IHttpActionResult**接口的一些优点：</span><span class="sxs-lookup"><span data-stu-id="800c0-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="800c0-138">简化控制器的[单元测试](../testing-and-debugging/unit-testing-controllers-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="800c0-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="800c0-139">将用于创建 HTTP 响应的公共逻辑移到单独的类中。</span><span class="sxs-lookup"><span data-stu-id="800c0-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="800c0-140">通过隐藏构造响应的低级别细节，使控制器操作的意图更清晰。</span><span class="sxs-lookup"><span data-stu-id="800c0-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="800c0-141">**IHttpActionResult**包含单一方法**ExecuteAsync**，它以异步方式创建**HttpResponseMessage**实例。</span><span class="sxs-lookup"><span data-stu-id="800c0-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="800c0-142">如果控制器操作返回**IHttpActionResult**，Web API 将调用**ExecuteAsync**方法来创建**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="800c0-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="800c0-143">然后，将**HttpResponseMessage**转换为 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="800c0-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="800c0-144">下面是创建纯文本响应的**IHttpActionResult**的简单实现：</span><span class="sxs-lookup"><span data-stu-id="800c0-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="800c0-145">示例控制器操作：</span><span class="sxs-lookup"><span data-stu-id="800c0-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="800c0-146">响应：</span><span class="sxs-lookup"><span data-stu-id="800c0-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="800c0-147">更频繁地使用在 IHttpActionResult 命名空间中定义的 **[实现。](https://msdn.microsoft.com/library/system.web.http.results.aspx)**</span><span class="sxs-lookup"><span data-stu-id="800c0-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="800c0-148">**ApiController**类定义返回这些内置操作结果的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="800c0-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="800c0-149">在以下示例中，如果请求与现有产品 ID 不匹配，则控制器将调用[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)来创建404（未找到）响应。</span><span class="sxs-lookup"><span data-stu-id="800c0-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="800c0-150">否则，控制器将调用[ApiController](https://msdn.microsoft.com/library/dn314591.aspx)，这将创建一个包含该产品的200（OK）响应。</span><span class="sxs-lookup"><span data-stu-id="800c0-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="800c0-151">其他返回类型</span><span class="sxs-lookup"><span data-stu-id="800c0-151">Other Return Types</span></span>

<span data-ttu-id="800c0-152">对于所有其他返回类型，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)来序列化返回值。</span><span class="sxs-lookup"><span data-stu-id="800c0-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="800c0-153">Web API 将序列化的值写入响应正文。</span><span class="sxs-lookup"><span data-stu-id="800c0-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="800c0-154">响应状态代码为200（正常）。</span><span class="sxs-lookup"><span data-stu-id="800c0-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="800c0-155">这种方法的缺点是，您不能直接返回错误代码，如404。</span><span class="sxs-lookup"><span data-stu-id="800c0-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="800c0-156">但是，可以针对错误代码引发**带有 httpresponseexception** 。</span><span class="sxs-lookup"><span data-stu-id="800c0-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="800c0-157">有关详细信息，请参阅[中的异常处理 ASP.NET Web API](../error-handling/exception-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="800c0-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="800c0-158">Web API 使用请求中的 Accept 标头来选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="800c0-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="800c0-159">有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="800c0-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="800c0-160">示例请求</span><span class="sxs-lookup"><span data-stu-id="800c0-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="800c0-161">示例响应</span><span class="sxs-lookup"><span data-stu-id="800c0-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
