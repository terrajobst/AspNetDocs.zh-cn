---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: BSON 的支持 ASP.NET Web API 2.1-ASP.NET 4.x
author: MikeWasson
description: 演示如何为 ASP.NET Web API 控制器 （服务器端） 和.NET 客户端应用中使用 BSON 4.x。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 911e2abcfd277075b3cba71e624ec6390b99a15e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382221"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="54e8c-103">在 ASP.NET Web API 2.1 对 BSON 的支持</span><span class="sxs-lookup"><span data-stu-id="54e8c-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="54e8c-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="54e8c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="54e8c-105">本主题演示如何在 Web API 控制器 （服务器端） 和.NET 客户端应用中使用 BSON。</span><span class="sxs-lookup"><span data-stu-id="54e8c-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="54e8c-106">Web API 2.1 引入了对 BSON 的支持。</span><span class="sxs-lookup"><span data-stu-id="54e8c-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="54e8c-107">BSON 是什么？</span><span class="sxs-lookup"><span data-stu-id="54e8c-107">What is BSON?</span></span>

<span data-ttu-id="54e8c-108">[BSON](http://bsonspec.org/)是一种二进制序列化格式。</span><span class="sxs-lookup"><span data-stu-id="54e8c-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="54e8c-109">"BSON"代表"二进制 JSON"，但 BSON 和 JSON 进行序列化有很大不同。</span><span class="sxs-lookup"><span data-stu-id="54e8c-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="54e8c-110">BSON 是"类似于 JSON 的"，因为对象表示为名称 / 值对，类似于 JSON。</span><span class="sxs-lookup"><span data-stu-id="54e8c-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="54e8c-111">不同于 JSON，数字数据类型存储为字节，不是字符串</span><span class="sxs-lookup"><span data-stu-id="54e8c-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="54e8c-112">BSON 旨在轻量、 易于扫描和快速地进行编码/解码。</span><span class="sxs-lookup"><span data-stu-id="54e8c-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="54e8c-113">BSON 是可比得上大小为 JSON。</span><span class="sxs-lookup"><span data-stu-id="54e8c-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="54e8c-114">具体取决于数据，BSON 有效负载可能小于或大于 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="54e8c-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="54e8c-115">用于序列化二进制数据，如图像文件，BSON 小于 JSON，因为二进制数据不是 base64 编码。</span><span class="sxs-lookup"><span data-stu-id="54e8c-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="54e8c-116">BSON 文档很容易扫描的原因是元素前缀长度的字段，因此分析器可以跳过，元素不解码它们。</span><span class="sxs-lookup"><span data-stu-id="54e8c-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="54e8c-117">编码和解码有效，因为是数值数据类型存储为数字，不是字符串。</span><span class="sxs-lookup"><span data-stu-id="54e8c-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="54e8c-118">本机客户端，如.NET 客户端应用可以受益于使用 BSON 代替基于文本的格式，如 JSON 或 XML 中。</span><span class="sxs-lookup"><span data-stu-id="54e8c-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="54e8c-119">对于浏览器客户端，您可能需要坚持使用 JSON，因为 JavaScript 直接转换 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="54e8c-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="54e8c-120">幸运的是，Web API 使用[内容协商](content-negotiation.md)，因此你的 API 可以支持这两种格式，并允许客户端选择。</span><span class="sxs-lookup"><span data-stu-id="54e8c-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="54e8c-121">在服务器上启用 BSON</span><span class="sxs-lookup"><span data-stu-id="54e8c-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="54e8c-122">在 Web API 配置中，添加**BsonMediaTypeFormatter**到格式化程序集合。</span><span class="sxs-lookup"><span data-stu-id="54e8c-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="54e8c-123">现在如果客户端请求"application/bson"，Web API 将使用 BSON 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="54e8c-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="54e8c-124">若要将 BSON 与其他媒体类型相关联，请将它们添加到 SupportedMediaTypes 集合。</span><span class="sxs-lookup"><span data-stu-id="54e8c-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="54e8c-125">下面的代码添加到受支持的媒体类型"application/vnd.contoso":</span><span class="sxs-lookup"><span data-stu-id="54e8c-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="54e8c-126">示例 HTTP 会话</span><span class="sxs-lookup"><span data-stu-id="54e8c-126">Example HTTP Session</span></span>

<span data-ttu-id="54e8c-127">对于此示例中，我们将使用以下的 model 类以及一个简单的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="54e8c-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="54e8c-128">客户端可能会发送以下 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="54e8c-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="54e8c-129">下面是响应：</span><span class="sxs-lookup"><span data-stu-id="54e8c-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="54e8c-130">此处我已替换为二进制数据， &quot;。&quot;字符。</span><span class="sxs-lookup"><span data-stu-id="54e8c-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="54e8c-131">下面的屏幕截图所示 Fiddler 原始的十六进制值。</span><span class="sxs-lookup"><span data-stu-id="54e8c-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="54e8c-132">使用 HttpClient BSON</span><span class="sxs-lookup"><span data-stu-id="54e8c-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="54e8c-133">.NET 客户端应用程序可以使用 BSON 格式化程序与**HttpClient**。</span><span class="sxs-lookup"><span data-stu-id="54e8c-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="54e8c-134">有关详细信息**HttpClient**，请参阅[调用 Web API 从.NET 客户端](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="54e8c-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="54e8c-135">下面的代码将发送 GET 请求，用于接受 BSON，并随后在响应中的 BSON 有效负载反序列化。</span><span class="sxs-lookup"><span data-stu-id="54e8c-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="54e8c-136">若要从服务器请求 BSON，设置为"application/bson"Accept 标头：</span><span class="sxs-lookup"><span data-stu-id="54e8c-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="54e8c-137">若要反序列化响应正文，使用**BsonMediaTypeFormatter**。</span><span class="sxs-lookup"><span data-stu-id="54e8c-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="54e8c-138">此格式化程序不在默认格式化程序集合，因此你需要时读取响应正文中指定它：</span><span class="sxs-lookup"><span data-stu-id="54e8c-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="54e8c-139">以下示例演示如何发送包含 BSON 的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="54e8c-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="54e8c-140">此代码大部分是上一示例相同。</span><span class="sxs-lookup"><span data-stu-id="54e8c-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="54e8c-141">但在**PostAsync**方法中，指定**BsonMediaTypeFormatter**作为格式化程序：</span><span class="sxs-lookup"><span data-stu-id="54e8c-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="54e8c-142">顶级基元类型进行序列化</span><span class="sxs-lookup"><span data-stu-id="54e8c-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="54e8c-143">BSON 的每个文档是键/值对的列表。BSON 规范并未定义用于序列化单个的原始值，例如整数或字符串的语法。</span><span class="sxs-lookup"><span data-stu-id="54e8c-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="54e8c-144">若要解决此限制， **BsonMediaTypeFormatter**基元类型视为一种特殊情况。</span><span class="sxs-lookup"><span data-stu-id="54e8c-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="54e8c-145">序列化之前, 它将值转换为键/值对使用密钥"值"。</span><span class="sxs-lookup"><span data-stu-id="54e8c-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="54e8c-146">例如，假设你的 API 控制器返回一个整数：</span><span class="sxs-lookup"><span data-stu-id="54e8c-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="54e8c-147">序列化之前, BSON 格式化程序将此转换为以下键/值对：</span><span class="sxs-lookup"><span data-stu-id="54e8c-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="54e8c-148">当您反序列化时，格式化程序将数据转换回原始值。</span><span class="sxs-lookup"><span data-stu-id="54e8c-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="54e8c-149">但是，使用不同的 BSON 分析器的客户端将需要处理这种情况下，如果你的 web API 返回原始值。</span><span class="sxs-lookup"><span data-stu-id="54e8c-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="54e8c-150">一般情况下，应考虑返回结构化的数据，而不是原始值。</span><span class="sxs-lookup"><span data-stu-id="54e8c-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54e8c-151">其他资源</span><span class="sxs-lookup"><span data-stu-id="54e8c-151">Additional Resources</span></span>

[<span data-ttu-id="54e8c-152">Web API BSON 示例</span><span class="sxs-lookup"><span data-stu-id="54e8c-152">Web API BSON Sample</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[<span data-ttu-id="54e8c-153">媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="54e8c-153">Media Formatters</span></span>](media-formatters.md)
