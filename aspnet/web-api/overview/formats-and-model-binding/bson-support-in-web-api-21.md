---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1-ASP.NET 4.x 中的 BSON 支持
author: MikeWasson
description: 演示如何在 Web API 控制器（服务器端）和用于 ASP.NET 4.x 的 .NET 客户端应用中使用 BSON。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519320"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="b2f2b-103">ASP.NET Web API 2.1 中的 BSON 支持</span><span class="sxs-lookup"><span data-stu-id="b2f2b-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="b2f2b-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b2f2b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b2f2b-105">本主题演示如何在 Web API 控制器（服务器端）和 .NET 客户端应用程序中使用 BSON。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="b2f2b-106">Web API 2.1 引入了对 BSON 的支持。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="b2f2b-107">什么是 BSON？</span><span class="sxs-lookup"><span data-stu-id="b2f2b-107">What is BSON?</span></span>

<span data-ttu-id="b2f2b-108">[BSON](http://bsonspec.org/)是二进制序列化格式。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="b2f2b-109">"BSON" 代表 "二进制 JSON"，但 BSON 和 JSON 的序列化方式非常不同。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="b2f2b-110">BSON 是 "类似于 JSON" 的，因为对象表示为名称/值对，类似于 JSON。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="b2f2b-111">与 JSON 不同，数值数据类型存储为字节，而不是字符串</span><span class="sxs-lookup"><span data-stu-id="b2f2b-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="b2f2b-112">BSON 旨在实现轻型、易于扫描，并可快速进行编码/解码。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="b2f2b-113">BSON 的大小与 JSON 相同。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="b2f2b-114">BSON 有效负载可能大于或小于 JSON 有效负载，具体取决于数据。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="b2f2b-115">对于序列化二进制数据（如图像文件），BSON 小于 JSON，因为二进制数据不是 base64 编码的。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="b2f2b-116">BSON 文档易于扫描，因为元素以长度字段为前缀，因此分析器可以跳过元素而不进行解码。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="b2f2b-117">编码和解码是高效的，因为数值数据类型存储为数字，而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="b2f2b-118">本机客户端（例如 .NET 客户端应用程序）可以从使用 BSON 来代替基于文本的格式（例如，JSON 或 XML）。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="b2f2b-119">对于浏览器客户端，你可能需要坚持 JSON，因为 JavaScript 可以直接转换 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="b2f2b-120">幸运的是，Web API 使用[内容协商](content-negotiation.md)，因此 API 可以同时支持这两种格式，并让客户端选择。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="b2f2b-121">在服务器上启用 BSON</span><span class="sxs-lookup"><span data-stu-id="b2f2b-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="b2f2b-122">在 Web API 配置中，将**BsonMediaTypeFormatter**添加到格式化程序集合。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="b2f2b-123">现在，如果客户端请求 "application/bson"，Web API 将使用 BSON 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="b2f2b-124">若要将 BSON 与其他媒体类型相关联，请将它们添加到 SupportedMediaTypes 集合中。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="b2f2b-125">以下代码将 "application/vnd.apple.mpegurl" 添加到受支持的媒体类型：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="b2f2b-126">示例 HTTP 会话</span><span class="sxs-lookup"><span data-stu-id="b2f2b-126">Example HTTP Session</span></span>

<span data-ttu-id="b2f2b-127">在此示例中，我们将使用下面的模型类和简单的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="b2f2b-128">客户端可能会发送以下 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="b2f2b-129">下面是响应：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="b2f2b-130">这里，我已将二进制数据替换 &quot;。&quot; 字符。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="b2f2b-131">Fiddler 的以下屏幕截图显示原始十六进制值。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="b2f2b-132">将 BSON 与 HttpClient 配合使用</span><span class="sxs-lookup"><span data-stu-id="b2f2b-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="b2f2b-133">.NET 客户端应用程序可以将 BSON 格式化程序与**HttpClient**配合使用。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="b2f2b-134">有关**HttpClient**的详细信息，请参阅[从 .Net 客户端调用 Web API](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="b2f2b-135">下面的代码将发送一个 GET 请求，该请求接受 BSON，然后在响应中反序列化 BSON 负载。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="b2f2b-136">若要从服务器请求 BSON，请将 Accept 标头设置为 "application/BSON"：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="b2f2b-137">若要反序列化响应正文，请使用**BsonMediaTypeFormatter**。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="b2f2b-138">此格式化程序不在默认的格式化程序集合中，因此在您读取响应正文时必须指定它：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="b2f2b-139">下一个示例演示如何发送包含 BSON 的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="b2f2b-140">此代码的大部分内容与前面的示例相同。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="b2f2b-141">但在**PostAsync**方法中，将**BsonMediaTypeFormatter**指定为格式化程序：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="b2f2b-142">序列化顶级基元类型</span><span class="sxs-lookup"><span data-stu-id="b2f2b-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="b2f2b-143">每个 BSON 文档都是键/值对的列表。BSON 规范未定义用于序列化单个原始值（如整数或字符串）的语法。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="b2f2b-144">为了解决此限制， **BsonMediaTypeFormatter**将基元类型视为一种特殊情况。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="b2f2b-145">在进行序列化之前，它将值转换为键/值对，其键为 "Value"。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="b2f2b-146">例如，假设 API 控制器返回整数：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="b2f2b-147">序列化之前，BSON 格式化程序将其转换为以下键/值对：</span><span class="sxs-lookup"><span data-stu-id="b2f2b-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="b2f2b-148">反序列化时，格式化程序将数据转换回原始值。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="b2f2b-149">但是，如果 web API 返回原始值，则使用不同 BSON 分析器的客户端需要处理这种情况。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="b2f2b-150">通常，应考虑返回结构化数据而不是原始值。</span><span class="sxs-lookup"><span data-stu-id="b2f2b-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2f2b-151">其他资源</span><span class="sxs-lookup"><span data-stu-id="b2f2b-151">Additional Resources</span></span>

[<span data-ttu-id="b2f2b-152">Web API BSON 示例</span><span class="sxs-lookup"><span data-stu-id="b2f2b-152">Web API BSON Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[<span data-ttu-id="b2f2b-153">媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="b2f2b-153">Media Formatters</span></span>](media-formatters.md)
