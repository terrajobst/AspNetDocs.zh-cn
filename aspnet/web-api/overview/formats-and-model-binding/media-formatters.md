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
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="9fc25-103">ASP.NET Web API 2 中的媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="9fc25-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="9fc25-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9fc25-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9fc25-105">本教程演示如何在 ASP.NET Web API 中支持其他媒体格式。</span><span class="sxs-lookup"><span data-stu-id="9fc25-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="9fc25-106">Internet 媒体类型</span><span class="sxs-lookup"><span data-stu-id="9fc25-106">Internet Media Types</span></span>

<span data-ttu-id="9fc25-107">媒体类型（也称为 MIME 类型）标识一段数据的格式。</span><span class="sxs-lookup"><span data-stu-id="9fc25-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="9fc25-108">在 HTTP 中，媒体类型描述消息正文的格式。</span><span class="sxs-lookup"><span data-stu-id="9fc25-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="9fc25-109">媒体类型包括两个字符串：类型和子类型。</span><span class="sxs-lookup"><span data-stu-id="9fc25-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="9fc25-110">例如:</span><span class="sxs-lookup"><span data-stu-id="9fc25-110">For example:</span></span>

- <span data-ttu-id="9fc25-111">text/html</span><span class="sxs-lookup"><span data-stu-id="9fc25-111">text/html</span></span>
- <span data-ttu-id="9fc25-112">image/png</span><span class="sxs-lookup"><span data-stu-id="9fc25-112">image/png</span></span>
- <span data-ttu-id="9fc25-113">application/json</span><span class="sxs-lookup"><span data-stu-id="9fc25-113">application/json</span></span>

<span data-ttu-id="9fc25-114">当 HTTP 消息包含实体正文时，Content-type 标头指定消息正文的格式。</span><span class="sxs-lookup"><span data-stu-id="9fc25-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="9fc25-115">这会告诉接收方如何分析消息正文的内容。</span><span class="sxs-lookup"><span data-stu-id="9fc25-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="9fc25-116">例如，如果 HTTP 响应包含一个 PNG 图像，则响应可能具有以下标头。</span><span class="sxs-lookup"><span data-stu-id="9fc25-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="9fc25-117">当客户端发送请求消息时，它可以包含 Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="9fc25-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="9fc25-118">Accept 标头告诉服务器客户端要从服务器中获得哪些媒体类型。</span><span class="sxs-lookup"><span data-stu-id="9fc25-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="9fc25-119">例如:</span><span class="sxs-lookup"><span data-stu-id="9fc25-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="9fc25-120">此标头通知服务器客户端需要 HTML、XHTML 或 XML。</span><span class="sxs-lookup"><span data-stu-id="9fc25-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="9fc25-121">媒体类型决定了 Web API 如何序列化和反序列化 HTTP 消息正文。</span><span class="sxs-lookup"><span data-stu-id="9fc25-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="9fc25-122">Web API 提供对 XML、JSON、BSON 和 url 编码数据的内置支持，你可以通过编写*媒体格式化程序*来支持其他媒体类型。</span><span class="sxs-lookup"><span data-stu-id="9fc25-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="9fc25-123">若要创建媒体格式化程序，请从以下类之一派生：</span><span class="sxs-lookup"><span data-stu-id="9fc25-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="9fc25-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9fc25-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="9fc25-125">此类使用异步读写方法。</span><span class="sxs-lookup"><span data-stu-id="9fc25-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="9fc25-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9fc25-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="9fc25-127">此类派生自**MediaTypeFormatter** ，但使用同步读/写方法。</span><span class="sxs-lookup"><span data-stu-id="9fc25-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="9fc25-128">从**BufferedMediaTypeFormatter**派生更简单，因为没有异步代码，但这也意味着调用线程可以在 i/o 期间阻塞。</span><span class="sxs-lookup"><span data-stu-id="9fc25-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="9fc25-129">示例：创建 CSV 媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="9fc25-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="9fc25-130">下面的示例演示可将产品对象序列化为逗号分隔值（CSV）格式的媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="9fc25-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="9fc25-131">此示例使用教程中定义的产品类型[创建支持 CRUD 操作的 WEB API](../older-versions/creating-a-web-api-that-supports-crud-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="9fc25-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="9fc25-132">下面是 Product 对象的定义：</span><span class="sxs-lookup"><span data-stu-id="9fc25-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="9fc25-133">若要实现 CSV 格式化程序，请定义一个派生自**BufferedMediaTypeFormatter**的类：</span><span class="sxs-lookup"><span data-stu-id="9fc25-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="9fc25-134">在构造函数中，添加格式化程序支持的媒体类型。</span><span class="sxs-lookup"><span data-stu-id="9fc25-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="9fc25-135">在此示例中，格式化程序支持一种媒体类型，&quot;文本/csv&quot;：</span><span class="sxs-lookup"><span data-stu-id="9fc25-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="9fc25-136">重写**CanWriteType**方法以指示格式化程序可以序列化的类型：</span><span class="sxs-lookup"><span data-stu-id="9fc25-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="9fc25-137">在此示例中，格式化程序可以序列化单个 `Product` 对象以及 `Product` 对象的集合。</span><span class="sxs-lookup"><span data-stu-id="9fc25-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="9fc25-138">同样，重写**CanReadType**方法以指示格式化程序可以反序列化的类型。</span><span class="sxs-lookup"><span data-stu-id="9fc25-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="9fc25-139">在此示例中，格式化程序不支持反序列化，因此此方法只返回**false**。</span><span class="sxs-lookup"><span data-stu-id="9fc25-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="9fc25-140">最后，重写**WriteToStream**方法。</span><span class="sxs-lookup"><span data-stu-id="9fc25-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="9fc25-141">此方法通过将类型写入流来序列化该类型。</span><span class="sxs-lookup"><span data-stu-id="9fc25-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="9fc25-142">如果格式化程序支持反序列化，还请重写**ReadFromStream**方法。</span><span class="sxs-lookup"><span data-stu-id="9fc25-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="9fc25-143">向 Web API 管道添加媒体格式化程序</span><span class="sxs-lookup"><span data-stu-id="9fc25-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="9fc25-144">若要将媒体类型格式化程序添加到 Web API 管道，请使用**HttpConfiguration**对象上的 "**格式化**程序" 属性。</span><span class="sxs-lookup"><span data-stu-id="9fc25-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="9fc25-145">字符编码</span><span class="sxs-lookup"><span data-stu-id="9fc25-145">Character Encodings</span></span>

<span data-ttu-id="9fc25-146">媒体格式化程序还可以选择支持多种字符编码，例如 UTF-8 或 ISO 8859-1。</span><span class="sxs-lookup"><span data-stu-id="9fc25-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="9fc25-147">在构造函数中，将一个或[多个](https://msdn.microsoft.com/library/system.text.encoding.aspx)SupportedEncodings 类型添加到 " " 集合中。</span><span class="sxs-lookup"><span data-stu-id="9fc25-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="9fc25-148">首先放置默认编码。</span><span class="sxs-lookup"><span data-stu-id="9fc25-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="9fc25-149">在**WriteToStream**和**ReadFromStream**方法中，调用[MediaTypeFormatter](https://msdn.microsoft.com/library/hh969054.aspx)以选择首选字符编码。</span><span class="sxs-lookup"><span data-stu-id="9fc25-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="9fc25-150">此方法将请求标头与受支持的编码列表匹配。</span><span class="sxs-lookup"><span data-stu-id="9fc25-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="9fc25-151">从流中读取或写入时使用返回的**编码**：</span><span class="sxs-lookup"><span data-stu-id="9fc25-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
