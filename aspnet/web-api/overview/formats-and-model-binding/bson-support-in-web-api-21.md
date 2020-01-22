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
# <a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1 中的 BSON 支持

作者： [Mike Wasson](https://github.com/MikeWasson)

本主题演示如何在 Web API 控制器（服务器端）和 .NET 客户端应用程序中使用 BSON。 Web API 2.1 引入了对 BSON 的支持。 

## <a name="what-is-bson"></a>什么是 BSON？

[BSON](http://bsonspec.org/)是二进制序列化格式。 "BSON" 代表 "二进制 JSON"，但 BSON 和 JSON 的序列化方式非常不同。 BSON 是 "类似于 JSON" 的，因为对象表示为名称/值对，类似于 JSON。 与 JSON 不同，数值数据类型存储为字节，而不是字符串

BSON 旨在实现轻型、易于扫描，并可快速进行编码/解码。

- BSON 的大小与 JSON 相同。 BSON 有效负载可能大于或小于 JSON 有效负载，具体取决于数据。 对于序列化二进制数据（如图像文件），BSON 小于 JSON，因为二进制数据不是 base64 编码的。
- BSON 文档易于扫描，因为元素以长度字段为前缀，因此分析器可以跳过元素而不进行解码。
- 编码和解码是高效的，因为数值数据类型存储为数字，而不是字符串。

本机客户端（例如 .NET 客户端应用程序）可以从使用 BSON 来代替基于文本的格式（例如，JSON 或 XML）。 对于浏览器客户端，你可能需要坚持 JSON，因为 JavaScript 可以直接转换 JSON 有效负载。

幸运的是，Web API 使用[内容协商](content-negotiation.md)，因此 API 可以同时支持这两种格式，并让客户端选择。

## <a name="enabling-bson-on-the-server"></a>在服务器上启用 BSON

在 Web API 配置中，将**BsonMediaTypeFormatter**添加到格式化程序集合。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

现在，如果客户端请求 "application/bson"，Web API 将使用 BSON 格式化程序。

若要将 BSON 与其他媒体类型相关联，请将它们添加到 SupportedMediaTypes 集合中。 以下代码将 "application/vnd.apple.mpegurl" 添加到受支持的媒体类型：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>示例 HTTP 会话

在此示例中，我们将使用下面的模型类和简单的 Web API 控制器：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

客户端可能会发送以下 HTTP 请求：

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

下面是响应：

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

这里，我已将二进制数据替换 &quot;。&quot; 字符。 Fiddler 的以下屏幕截图显示原始十六进制值。

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>将 BSON 与 HttpClient 配合使用

.NET 客户端应用程序可以将 BSON 格式化程序与**HttpClient**配合使用。 有关**HttpClient**的详细信息，请参阅[从 .Net 客户端调用 Web API](../advanced/calling-a-web-api-from-a-net-client.md)。

下面的代码将发送一个 GET 请求，该请求接受 BSON，然后在响应中反序列化 BSON 负载。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

若要从服务器请求 BSON，请将 Accept 标头设置为 "application/BSON"：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

若要反序列化响应正文，请使用**BsonMediaTypeFormatter**。 此格式化程序不在默认的格式化程序集合中，因此在您读取响应正文时必须指定它：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

下一个示例演示如何发送包含 BSON 的 POST 请求。

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

此代码的大部分内容与前面的示例相同。 但在**PostAsync**方法中，将**BsonMediaTypeFormatter**指定为格式化程序：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>序列化顶级基元类型

每个 BSON 文档都是键/值对的列表。BSON 规范未定义用于序列化单个原始值（如整数或字符串）的语法。

为了解决此限制， **BsonMediaTypeFormatter**将基元类型视为一种特殊情况。 在进行序列化之前，它将值转换为键/值对，其键为 "Value"。 例如，假设 API 控制器返回整数：

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

序列化之前，BSON 格式化程序将其转换为以下键/值对：

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

反序列化时，格式化程序将数据转换回原始值。 但是，如果 web API 返回原始值，则使用不同 BSON 分析器的客户端需要处理这种情况。 通常，应考虑返回结构化数据而不是原始值。

## <a name="additional-resources"></a>其他资源

[Web API BSON 示例](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[媒体格式化程序](media-formatters.md)
