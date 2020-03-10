---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API-ASP.NET 4.x 中的异常处理
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504698"
---
# <a name="exception-handling-in-aspnet-web-api"></a>ASP.NET Web API 中的异常处理

作者： [Mike Wasson](https://github.com/MikeWasson)

本文介绍了 ASP.NET Web API 中的错误和异常处理。

- [带有 httpresponseexception](#httpresponserexception)
- [异常筛选器](#exception_filters)
- [注册异常筛选器](#registering_exception_filters)
- [HttpError](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

如果 Web API 控制器引发未捕获的异常，会发生什么情况？ 默认情况下，大多数异常都转换为 HTTP 响应，状态代码为500，内部服务器错误。

**带有 httpresponseexception**类型是一种特殊情况。 此异常返回在异常构造函数中指定的任何 HTTP 状态代码。 例如，如果*id*参数无效，则以下方法返回404，但找不到。

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

为了更好地控制响应，你还可以构造整个响应消息，并将其包含在**带有 httpresponseexception 中：** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>异常筛选器

可以通过编写*异常筛选器*来自定义 Web API 处理异常的方式。 当控制器方法引发*不*是**带有 httpresponseexception**异常的任何未经处理的异常时，将执行异常筛选器。 **带有 httpresponseexception**类型是一种特殊情况，因为它专用于返回 HTTP 响应。

异常筛选器实现了**IExceptionFilter**接口。 编写异常筛选器的最简单方法是从**ExceptionFilterAttribute**类派生，并重写**OnException**方法。

> [!NOTE]
> ASP.NET Web API 中的异常筛选器类似于 ASP.NET MVC 中的筛选器。 但是，它们分别在单独的命名空间和函数中声明。 特别是，MVC 中使用的**HandleErrorAttribute**类不处理 Web API 控制器引发的异常。

下面的筛选器将**NotImplementedException**异常转换为 HTTP 状态代码501，而未实现：

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

**HttpActionExecutedContext**对象的**Response**属性包含将发送到客户端的 HTTP 响应消息。

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>注册异常筛选器

可通过多种方法注册 Web API 异常筛选器：

- 按操作
- 按控制器
- 全局

要将筛选器应用到特定的操作，请将筛选器作为特性添加到该操作：

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

若要将筛选器应用于控制器上的所有操作，请将筛选器作为属性添加到控制器类：

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

若要将筛选器全局应用到所有 Web API 控制器，请将筛选器的实例添加到**GlobalConfiguration**集合。 此集合中的异常筛选器将应用到任何 Web API 控制器操作。

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

如果使用 "ASP.NET MVC 4 Web 应用程序" 项目模板来创建项目，请将 Web API 配置代码置于 `WebApiConfig` 类中，该代码位于应用\_启动文件夹中：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>HttpError

**HttpError**对象提供了一种一致的方式来在响应正文中返回错误信息。 下面的示例演示如何在响应正文中返回包含**HttpError**的 HTTP 状态代码404（未找到）。

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**CreateErrorResponse**是在**HttpRequestMessageExtensions**类中定义的扩展方法。 在内部， **CreateErrorResponse**创建一个**HttpError**实例，然后创建一个包含**HttpError**的**HttpResponseMessage** 。

在此示例中，如果方法成功，它将在 HTTP 响应中返回产品。 但如果找不到请求的产品，HTTP 响应会在请求正文中包含**HttpError** 。 响应可能如下所示：

[!code-console[Main](exception-handling/samples/sample9.cmd)]

请注意，在此示例中， **HttpError**已序列化为 JSON。 使用**HttpError**的一个优点是，它与任何其他强类型模型进行相同的[内容协商](../formats-and-model-binding/content-negotiation.md)和序列化过程。

### <a name="httperror-and-model-validation"></a>HttpError 和模型验证

对于模型验证，可以将模型状态传递到**CreateErrorResponse**，以便在响应中包括验证错误：

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

此示例可能返回以下响应：

[!code-console[Main](exception-handling/samples/sample11.cmd)]

有关模型验证的详细信息，请参阅[中的模型验证 ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。

### <a name="using-httperror-with-httpresponseexception"></a>将 HttpError 与带有 httpresponseexception 配合使用

前面的示例从控制器操作返回**HttpResponseMessage**消息，但也可以使用**带有 httpresponseexception**返回**HttpError**。 这使您可以在正常的成功情况下返回强类型化的模型，同时在出现错误时仍会返回**HttpError** ：

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
