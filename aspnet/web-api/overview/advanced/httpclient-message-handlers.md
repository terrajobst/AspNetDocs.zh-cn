---
uid: web-api/overview/advanced/httpclient-message-handlers
title: HttpClient 消息处理程序 ASP.NET Web API-ASP.NET 4。x
author: MikeWasson
description: 为 ASP.NET 4.x 中的 ASP.NET Web API 创建自定义消息处理程序
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449276"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 中的 HttpClient 消息处理程序

作者： [Mike Wasson](https://github.com/MikeWasson)

*消息处理程序*是接收 http 请求并返回 http 响应的类。

通常，一系列消息处理程序链接在一起。 第一个处理程序接收 HTTP 请求，进行一些处理，并向下一个处理程序提供请求。 在某个时间点，将创建响应，并在链中返回。 此模式称为*委托*处理程序。

![](httpclient-message-handlers/_static/image1.png)

在客户端， **HttpClient**类使用消息处理程序来处理请求。 默认处理程序是**HttpClientHandler**，它通过网络发送请求并从服务器获取响应。 可以将自定义消息处理程序插入客户端管道：

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> ASP.NET Web API 还会在服务器端使用消息处理程序。 有关详细信息，请参阅[HTTP 消息处理程序](http-message-handlers.md)。

## <a name="custom-message-handlers"></a>自定义消息处理程序

若要编写自定义消息处理程序，请从**DelegatingHandler**派生并重写**SendAsync**方法。 下面是方法签名：

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。 典型的实现会执行以下操作：

1. 处理请求消息。
2. 调用 `base.SendAsync` 将请求发送到内部处理程序。
3. 内部处理程序返回响应消息。 （此步骤是异步的。）
4. 处理响应并将其返回给调用方。

下面的示例演示将自定义标头添加到传出请求的消息处理程序：

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

对 `base.SendAsync` 的调用是异步的。 如果处理程序在此调用后执行任何操作，请使用**await**关键字在方法完成后继续执行。 下面的示例演示了记录错误代码的处理程序。 日志记录本身并不是很有趣，但此示例演示如何获取处理程序内的响应。

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>向客户端管道添加消息处理程序

若要将自定义处理程序添加到**HttpClient**，请使用**HttpClientFactory**方法：

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

消息处理程序按您将其传递到**Create**方法的顺序进行调用。 由于处理程序是嵌套的，因此响应消息以其他方向传输。 也就是说，最后一个处理程序是获取响应消息的第一个处理程序。
