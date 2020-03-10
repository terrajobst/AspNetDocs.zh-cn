---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API 中的内容协商-ASP.NET 4。x
author: MikeWasson
description: 介绍 ASP.NET Web API 如何为 ASP.NET 4.x 实现 HTTP 内容协商。
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504656"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="c9b03-103">ASP.NET Web API 中的内容协商</span><span class="sxs-lookup"><span data-stu-id="c9b03-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="c9b03-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c9b03-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c9b03-105">本文介绍 ASP.NET Web API 如何实现 ASP.NET 4.x 的内容协商。</span><span class="sxs-lookup"><span data-stu-id="c9b03-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="c9b03-106">HTTP 规范（RFC 2616）将内容协商定义为 "当存在多个表示形式时，为给定响应选择最佳表示形式的过程"。</span><span class="sxs-lookup"><span data-stu-id="c9b03-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="c9b03-107">HTTP 中内容协商的主要机制是以下请求标头：</span><span class="sxs-lookup"><span data-stu-id="c9b03-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="c9b03-108">**接受：** 响应可接受的媒体类型，如 "application/json"、"application/xml" 或自定义媒体类型（如 &quot;application/vnd.apple.mpegurl + xml&quot;</span><span class="sxs-lookup"><span data-stu-id="c9b03-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="c9b03-109">**Accept-字符集：** 可以接受哪些字符集，例如 UTF-8 或 ISO 8859-1。</span><span class="sxs-lookup"><span data-stu-id="c9b03-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="c9b03-110">**接受编码：** 可接受的内容编码，如 gzip。</span><span class="sxs-lookup"><span data-stu-id="c9b03-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="c9b03-111">**接受语言：** 首选自然语言，如 "en-us"。</span><span class="sxs-lookup"><span data-stu-id="c9b03-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="c9b03-112">服务器还可以查看 HTTP 请求的其他部分。</span><span class="sxs-lookup"><span data-stu-id="c9b03-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="c9b03-113">例如，如果请求包含 X 请求的标头（指示 AJAX 请求），则在没有 Accept 标头的情况下，服务器可能会默认为 JSON。</span><span class="sxs-lookup"><span data-stu-id="c9b03-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="c9b03-114">本文介绍了 Web API 如何使用接受和接受字符集标头。</span><span class="sxs-lookup"><span data-stu-id="c9b03-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="c9b03-115">（目前没有对接受编码或接受语言的内置支持。）</span><span class="sxs-lookup"><span data-stu-id="c9b03-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="c9b03-116">序列化</span><span class="sxs-lookup"><span data-stu-id="c9b03-116">Serialization</span></span>

<span data-ttu-id="c9b03-117">如果 Web API 控制器将资源作为 CLR 类型返回，则管道会序列化返回值并将其写入 HTTP 响应正文。</span><span class="sxs-lookup"><span data-stu-id="c9b03-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="c9b03-118">例如，考虑以下控制器操作：</span><span class="sxs-lookup"><span data-stu-id="c9b03-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="c9b03-119">客户端可能会发送以下 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="c9b03-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="c9b03-120">在响应中，服务器可能会发送：</span><span class="sxs-lookup"><span data-stu-id="c9b03-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="c9b03-121">在此示例中，客户端请求了 JSON、Javascript 或 "任何内容" （\*/\*）。</span><span class="sxs-lookup"><span data-stu-id="c9b03-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="c9b03-122">服务器响应 `Product` 对象的 JSON 表示形式。</span><span class="sxs-lookup"><span data-stu-id="c9b03-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="c9b03-123">请注意，响应中的 Content-type 标头设置为 &quot;application/json&quot;。</span><span class="sxs-lookup"><span data-stu-id="c9b03-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="c9b03-124">控制器还可以返回**HttpResponseMessage**对象。</span><span class="sxs-lookup"><span data-stu-id="c9b03-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="c9b03-125">若要为响应正文指定 CLR 对象，请调用**CreateResponse**扩展方法：</span><span class="sxs-lookup"><span data-stu-id="c9b03-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="c9b03-126">此选项使你可以更好地控制响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c9b03-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="c9b03-127">可以设置状态代码、添加 HTTP 标头等。</span><span class="sxs-lookup"><span data-stu-id="c9b03-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="c9b03-128">序列化资源的对象称为*媒体格式化程序*。</span><span class="sxs-lookup"><span data-stu-id="c9b03-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="c9b03-129">媒体格式化程序派生自**MediaTypeFormatter**类。</span><span class="sxs-lookup"><span data-stu-id="c9b03-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="c9b03-130">Web API 提供用于 XML 和 JSON 的媒体格式化程序，你可以创建自定义格式化程序以支持其他媒体类型。</span><span class="sxs-lookup"><span data-stu-id="c9b03-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="c9b03-131">有关编写自定义格式化程序的信息，请参阅[媒体格式化](media-formatters.md)程序。</span><span class="sxs-lookup"><span data-stu-id="c9b03-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="c9b03-132">内容协商的工作方式</span><span class="sxs-lookup"><span data-stu-id="c9b03-132">How Content Negotiation Works</span></span>

<span data-ttu-id="c9b03-133">首先，管道从**HttpConfiguration**对象中获取**IContentNegotiator**服务。</span><span class="sxs-lookup"><span data-stu-id="c9b03-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="c9b03-134">它还从**HttpConfiguration**集合中获取媒体格式化程序列表。</span><span class="sxs-lookup"><span data-stu-id="c9b03-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="c9b03-135">接下来，管道将调用**IContentNegotiator**，传入：</span><span class="sxs-lookup"><span data-stu-id="c9b03-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="c9b03-136">要序列化的对象的类型</span><span class="sxs-lookup"><span data-stu-id="c9b03-136">The type of object to serialize</span></span>
- <span data-ttu-id="c9b03-137">媒体格式化程序的集合</span><span class="sxs-lookup"><span data-stu-id="c9b03-137">The collection of media formatters</span></span>
- <span data-ttu-id="c9b03-138">HTTP 请求</span><span class="sxs-lookup"><span data-stu-id="c9b03-138">The HTTP request</span></span>

<span data-ttu-id="c9b03-139">**Negotiate**方法返回两条信息：</span><span class="sxs-lookup"><span data-stu-id="c9b03-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="c9b03-140">要使用的格式化程序</span><span class="sxs-lookup"><span data-stu-id="c9b03-140">Which formatter to use</span></span>
- <span data-ttu-id="c9b03-141">响应的媒体类型</span><span class="sxs-lookup"><span data-stu-id="c9b03-141">The media type for the response</span></span>

<span data-ttu-id="c9b03-142">如果找不到格式化程序，则**Negotiate**方法返回**null**，并且客户端收到 HTTP 错误406（不可接受）。</span><span class="sxs-lookup"><span data-stu-id="c9b03-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="c9b03-143">下面的代码演示控制器如何直接调用内容协商：</span><span class="sxs-lookup"><span data-stu-id="c9b03-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="c9b03-144">此代码等效于管道自动执行的操作。</span><span class="sxs-lookup"><span data-stu-id="c9b03-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="c9b03-145">默认内容 Negotiator</span><span class="sxs-lookup"><span data-stu-id="c9b03-145">Default Content Negotiator</span></span>

<span data-ttu-id="c9b03-146">**DefaultContentNegotiator**类提供**IContentNegotiator**的默认实现。</span><span class="sxs-lookup"><span data-stu-id="c9b03-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="c9b03-147">它使用多个条件来选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="c9b03-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="c9b03-148">首先，格式化程序必须能够序列化该类型。</span><span class="sxs-lookup"><span data-stu-id="c9b03-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="c9b03-149">这可通过调用**CanWriteType**进行验证。</span><span class="sxs-lookup"><span data-stu-id="c9b03-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="c9b03-150">接下来，内容 negotiator 查看每个格式化程序，并评估它与 HTTP 请求的匹配程度。</span><span class="sxs-lookup"><span data-stu-id="c9b03-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="c9b03-151">若要评估匹配，内容 negotiator 会在格式化程序上看到两个问题：</span><span class="sxs-lookup"><span data-stu-id="c9b03-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="c9b03-152">**SupportedMediaTypes**集合，其中包含受支持的媒体类型的列表。</span><span class="sxs-lookup"><span data-stu-id="c9b03-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="c9b03-153">内容 negotiator 尝试将此列表与请求 Accept 标头匹配。</span><span class="sxs-lookup"><span data-stu-id="c9b03-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="c9b03-154">请注意，Accept 标头可以包含范围。</span><span class="sxs-lookup"><span data-stu-id="c9b03-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="c9b03-155">例如，"text/普通" 是文本/\* 或 \*/\*匹配项。</span><span class="sxs-lookup"><span data-stu-id="c9b03-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="c9b03-156">**MediaTypeMappings**集合，其中包含**MediaTypeMapping**对象的列表。</span><span class="sxs-lookup"><span data-stu-id="c9b03-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="c9b03-157">**MediaTypeMapping**类提供了一种通用的方法，可将 HTTP 请求与媒体类型进行匹配。</span><span class="sxs-lookup"><span data-stu-id="c9b03-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="c9b03-158">例如，它可以将自定义 HTTP 标头映射到特定的媒体类型。</span><span class="sxs-lookup"><span data-stu-id="c9b03-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="c9b03-159">如果有多个匹配项，则具有最高质量因素的匹配入选。</span><span class="sxs-lookup"><span data-stu-id="c9b03-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="c9b03-160">例如:</span><span class="sxs-lookup"><span data-stu-id="c9b03-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="c9b03-161">在此示例中，application/json 具有默示的质量系数1.0，因此优先于 application/xml。</span><span class="sxs-lookup"><span data-stu-id="c9b03-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="c9b03-162">如果未找到匹配项，则内容 negotiator 会尝试匹配请求正文的媒体类型（如果有）。</span><span class="sxs-lookup"><span data-stu-id="c9b03-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="c9b03-163">例如，如果请求包含 JSON 数据，则内容 negotiator 将查找 JSON 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="c9b03-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="c9b03-164">如果仍没有匹配项，则内容 negotiator 只会选取可序列化该类型的第一个格式化程序。</span><span class="sxs-lookup"><span data-stu-id="c9b03-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="c9b03-165">选择字符编码</span><span class="sxs-lookup"><span data-stu-id="c9b03-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="c9b03-166">选择格式化程序后，内容 negotiator 通过查看格式化程序上的**SupportedEncodings**属性来选择最佳字符编码，并将其与请求中的接受字符集标头匹配（如果有）。</span><span class="sxs-lookup"><span data-stu-id="c9b03-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
