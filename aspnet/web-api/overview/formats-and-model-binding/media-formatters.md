---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2 中的媒体格式化程序-ASP.NET 4。x
author: MikeWasson
description: 演示如何在 ASP.NET Web API for ASP.NET 4.x 中支持其他媒体格式。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448940"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的媒体格式化程序

作者： [Mike Wasson](https://github.com/MikeWasson)

本教程演示如何在 ASP.NET Web API 中支持其他媒体格式。

## <a name="internet-media-types"></a>Internet 媒体类型

媒体类型（也称为 MIME 类型）标识一段数据的格式。 在 HTTP 中，媒体类型描述消息正文的格式。 媒体类型包括两个字符串：类型和子类型。 例如:

- text/html
- image/png
- application/json

当 HTTP 消息包含实体正文时，Content-type 标头指定消息正文的格式。 这会告诉接收方如何分析消息正文的内容。

例如，如果 HTTP 响应包含一个 PNG 图像，则响应可能具有以下标头。

[!code-console[Main](media-formatters/samples/sample1.cmd)]

当客户端发送请求消息时，它可以包含 Accept 标头。 Accept 标头告诉服务器客户端要从服务器中获得哪些媒体类型。 例如:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

此标头通知服务器客户端需要 HTML、XHTML 或 XML。

媒体类型决定了 Web API 如何序列化和反序列化 HTTP 消息正文。 Web API 提供对 XML、JSON、BSON 和 url 编码数据的内置支持，你可以通过编写*媒体格式化程序*来支持其他媒体类型。

若要创建媒体格式化程序，请从以下类之一派生：

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。 此类使用异步读写方法。
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。 此类派生自**MediaTypeFormatter** ，但使用同步读/写方法。

从**BufferedMediaTypeFormatter**派生更简单，因为没有异步代码，但这也意味着调用线程可以在 i/o 期间阻塞。

## <a name="example-creating-a-csv-media-formatter"></a>示例：创建 CSV 媒体格式化程序

下面的示例演示可将产品对象序列化为逗号分隔值（CSV）格式的媒体类型格式化程序。 此示例使用教程中定义的产品类型[创建支持 CRUD 操作的 WEB API](../older-versions/creating-a-web-api-that-supports-crud-operations.md)。 下面是 Product 对象的定义：

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

若要实现 CSV 格式化程序，请定义一个派生自**BufferedMediaTypeFormatter**的类：

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

在构造函数中，添加格式化程序支持的媒体类型。 在此示例中，格式化程序支持一种媒体类型，&quot;文本/csv&quot;：

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

重写**CanWriteType**方法以指示格式化程序可以序列化的类型：

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

在此示例中，格式化程序可以序列化单个 `Product` 对象以及 `Product` 对象的集合。

同样，重写**CanReadType**方法以指示格式化程序可以反序列化的类型。 在此示例中，格式化程序不支持反序列化，因此此方法只返回**false**。

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

最后，重写**WriteToStream**方法。 此方法通过将类型写入流来序列化该类型。 如果格式化程序支持反序列化，还请重写**ReadFromStream**方法。

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>向 Web API 管道添加媒体格式化程序

若要将媒体类型格式化程序添加到 Web API 管道，请使用**HttpConfiguration**对象上的 "**格式化**程序" 属性。

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>字符编码

媒体格式化程序还可以选择支持多种字符编码，例如 UTF-8 或 ISO 8859-1。

在构造函数中，将一个或[多个](https://msdn.microsoft.com/library/system.text.encoding.aspx)SupportedEncodings 类型添加到 " " 集合中。 首先放置默认编码。

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

在**WriteToStream**和**ReadFromStream**方法中，调用[MediaTypeFormatter](https://msdn.microsoft.com/library/hh969054.aspx)以选择首选字符编码。 此方法将请求标头与受支持的编码列表匹配。 从流中读取或写入时使用返回的**编码**：

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
