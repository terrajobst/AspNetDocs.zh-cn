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
# <a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API 中的内容协商

作者： [Mike Wasson](https://github.com/MikeWasson)

本文介绍 ASP.NET Web API 如何实现 ASP.NET 4.x 的内容协商。

HTTP 规范（RFC 2616）将内容协商定义为 "当存在多个表示形式时，为给定响应选择最佳表示形式的过程"。 HTTP 中内容协商的主要机制是以下请求标头：

- **接受：** 响应可接受的媒体类型，如 "application/json"、"application/xml" 或自定义媒体类型（如 &quot;application/vnd.apple.mpegurl + xml&quot;
- **Accept-字符集：** 可以接受哪些字符集，例如 UTF-8 或 ISO 8859-1。
- **接受编码：** 可接受的内容编码，如 gzip。
- **接受语言：** 首选自然语言，如 "en-us"。

服务器还可以查看 HTTP 请求的其他部分。 例如，如果请求包含 X 请求的标头（指示 AJAX 请求），则在没有 Accept 标头的情况下，服务器可能会默认为 JSON。

本文介绍了 Web API 如何使用接受和接受字符集标头。 （目前没有对接受编码或接受语言的内置支持。）

## <a name="serialization"></a>序列化

如果 Web API 控制器将资源作为 CLR 类型返回，则管道会序列化返回值并将其写入 HTTP 响应正文。

例如，考虑以下控制器操作：

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

客户端可能会发送以下 HTTP 请求：

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

在响应中，服务器可能会发送：

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

在此示例中，客户端请求了 JSON、Javascript 或 "任何内容" （\*/\*）。 服务器响应 `Product` 对象的 JSON 表示形式。 请注意，响应中的 Content-type 标头设置为 &quot;application/json&quot;。

控制器还可以返回**HttpResponseMessage**对象。 若要为响应正文指定 CLR 对象，请调用**CreateResponse**扩展方法：

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

此选项使你可以更好地控制响应的详细信息。 可以设置状态代码、添加 HTTP 标头等。

序列化资源的对象称为*媒体格式化程序*。 媒体格式化程序派生自**MediaTypeFormatter**类。 Web API 提供用于 XML 和 JSON 的媒体格式化程序，你可以创建自定义格式化程序以支持其他媒体类型。 有关编写自定义格式化程序的信息，请参阅[媒体格式化](media-formatters.md)程序。

## <a name="how-content-negotiation-works"></a>内容协商的工作方式

首先，管道从**HttpConfiguration**对象中获取**IContentNegotiator**服务。 它还从**HttpConfiguration**集合中获取媒体格式化程序列表。

接下来，管道将调用**IContentNegotiator**，传入：

- 要序列化的对象的类型
- 媒体格式化程序的集合
- HTTP 请求

**Negotiate**方法返回两条信息：

- 要使用的格式化程序
- 响应的媒体类型

如果找不到格式化程序，则**Negotiate**方法返回**null**，并且客户端收到 HTTP 错误406（不可接受）。

下面的代码演示控制器如何直接调用内容协商：

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

此代码等效于管道自动执行的操作。

## <a name="default-content-negotiator"></a>默认内容 Negotiator

**DefaultContentNegotiator**类提供**IContentNegotiator**的默认实现。 它使用多个条件来选择格式化程序。

首先，格式化程序必须能够序列化该类型。 这可通过调用**CanWriteType**进行验证。

接下来，内容 negotiator 查看每个格式化程序，并评估它与 HTTP 请求的匹配程度。 若要评估匹配，内容 negotiator 会在格式化程序上看到两个问题：

- **SupportedMediaTypes**集合，其中包含受支持的媒体类型的列表。 内容 negotiator 尝试将此列表与请求 Accept 标头匹配。 请注意，Accept 标头可以包含范围。 例如，"text/普通" 是文本/\* 或 \*/\*匹配项。
- **MediaTypeMappings**集合，其中包含**MediaTypeMapping**对象的列表。 **MediaTypeMapping**类提供了一种通用的方法，可将 HTTP 请求与媒体类型进行匹配。 例如，它可以将自定义 HTTP 标头映射到特定的媒体类型。

如果有多个匹配项，则具有最高质量因素的匹配入选。 例如:

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

在此示例中，application/json 具有默示的质量系数1.0，因此优先于 application/xml。

如果未找到匹配项，则内容 negotiator 会尝试匹配请求正文的媒体类型（如果有）。 例如，如果请求包含 JSON 数据，则内容 negotiator 将查找 JSON 格式化程序。

如果仍没有匹配项，则内容 negotiator 只会选取可序列化该类型的第一个格式化程序。

## <a name="selecting-a-character-encoding"></a>选择字符编码

选择格式化程序后，内容 negotiator 通过查看格式化程序上的**SupportedEncodings**属性来选择最佳字符编码，并将其与请求中的接受字符集标头匹配（如果有）。
