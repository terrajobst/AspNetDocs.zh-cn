---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 在 ASP.NET Web API 中发送 HTML 窗体数据：文件上传和多部分 ASP.NET 4。x
author: MikeWasson
description: 本教程演示如何将文件上传到 web API。 还介绍了如何处理多部分 MIME 数据。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449210"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>在 ASP.NET Web API 中发送 HTML 窗体数据：文件上传和多部分 MIME

作者： [Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>第2部分：文件上传和多部分 MIME

本教程演示如何将文件上传到 web API。 还介绍了如何处理多部分 MIME 数据。

> [!NOTE]
> [下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)。

下面是用于上载文件的 HTML 窗体的示例：

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

此窗体包含文本输入控件和文件输入控件。 当窗体包含文件输入控件时， **enctype**特性应始终 &quot;多部分/窗体数据&quot;，这将指定窗体将作为多部分 MIME 消息发送。

通过查看示例请求，可以最轻松地了解多部分 MIME 消息的格式：

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

此消息分为两*部分*，分别用于每个窗体控件。 部分边界由以破折号开头的行指示。

> [!NOTE]
> 部分边界包含随机组件（&quot;41184676334&quot;），以确保边界字符串不会意外出现在消息部分中。

每个消息部分都包含一个或多个标头，后面是部分内容。

- 内容处置标头包含控件的名称。 对于文件，它还包含文件名。
- Content-type 标头介绍了该部分中的数据。 如果省略此标头，则默认值为 text/简洁。

在上面的示例中，用户使用内容类型 image/jpeg 上传了一个名为 GrandCanyon 的文件;并且文本输入的值为 &quot;夏天假期&quot;。

## <a name="file-upload"></a>文件上传

现在，让我们看看从多部分 MIME 消息读取文件的 Web API 控制器。 控制器将异步读取文件。 Web API 使用[基于任务的编程模型](https://msdn.microsoft.com/library/dd460693.aspx)支持异步操作。 首先，如果你针对的是支持**async**和**await**关键字的 .NET Framework 4.5，则代码为。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

请注意，控制器操作不采用任何参数。 这是因为，我们处理操作中的请求正文，而不调用媒体类型格式化程序。

**IsMultipartContent**方法检查请求是否包含多部分 MIME 消息。 否则，控制器将返回 HTTP 状态代码415（不支持的媒体类型）。

**MultipartFormDataStreamProvider**类是一个帮助器对象，它为上传的文件分配文件流。 若要读取多部分 MIME 消息，请调用**ReadAsMultipartAsync**方法。 此方法提取所有消息部分，并将其写入**MultipartFormDataStreamProvider**提供的流中。

当方法完成时，可以从**FileData**属性获取有关文件的信息，该属性是**MultipartFileData**对象的集合。

- **MultipartFileData**是服务器上保存文件的本地文件名。
- **MultipartFileData**包含部件标题（*而不*是请求标头）。 你可以使用它来访问\_处置和 Content-type 标头的内容。

顾名思义， **ReadAsMultipartAsync**是一种异步方法。 若要在方法完成后执行工作，请使用[延续任务](https://msdn.microsoft.com/library/ee372288.aspx)（.net 4.0）或**await**关键字（.net 4.5）。

下面是前面代码的 .NET Framework 4.0 版本：

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>读取窗体控件数据

我前面介绍的 HTML 窗体具有文本输入控件。

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

可以从**MultipartFormDataStreamProvider**的**FormData**属性中获取该控件的值。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData**是包含窗体控件的名称/值对的**NameValueCollection** 。 集合可以包含重复键。 请考虑以下形式：

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

请求正文可能如下所示：

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

在这种情况下， **FormData**集合将包含以下键/值对：

- 行程：往返行程
- 选项：不间断
- 选项：日期
- 座位：窗口
