---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2 中的操作结果-ASP.NET 4。x
author: MikeWasson
description: 介绍 ASP.NET Web API 如何将控制器操作的返回值转换为 ASP.NET 4.x 中的 HTTP 响应消息。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448772"
---
# <a name="action-results-in-web-api-2"></a>Web API 2 的操作结果

[!INCLUDE[](~/includes/coreWebAPI.md)]

本主题介绍 ASP.NET Web API 如何将控制器操作的返回值转换为 HTTP 响应消息。

Web API 控制器操作可以返回以下任何内容：

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. 其他类型

根据返回的这种情况，Web API 将使用不同的机制来创建 HTTP 响应。

| 返回类型 | Web API 如何创建响应 |
| --- | --- |
| void | 返回空的204（无内容） |
| **HttpResponseMessage** | 直接转换为 HTTP 响应消息。 |
| **IHttpActionResult** | 调用**ExecuteAsync**创建**HttpResponseMessage**，然后将其转换为 HTTP 响应消息。 |
| 其他类型 | 将序列化的返回值写入响应正文;返回200（OK）。 |

本主题的其余部分将更详细地介绍每个选项。

## <a name="void"></a>void

如果返回类型为 `void`，Web API 只会返回空 HTTP 响应，状态代码为204（无内容）。

示例控制器：

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP 响应：

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

如果操作返回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 会将返回值直接转换为 HTTP 响应消息，并使用**HttpResponseMessage**对象的属性来填充响应。

此选项提供了对响应消息的大量控制。 例如，以下控制器操作设置缓存控制标头。

[!code-csharp[Main](action-results/samples/sample3.cs)]

响应：

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

如果向**CreateResponse**方法传递域模型，Web API 将使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)将序列化模型写入响应正文。

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API 使用请求中的 Accept 标头来选择格式化程序。 有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。

## <a name="ihttpactionresult"></a>IHttpActionResult

Web API 2 中引入了**IHttpActionResult**接口。 实质上，它定义了**HttpResponseMessage**工厂。 下面是使用**IHttpActionResult**接口的一些优点：

- 简化控制器的[单元测试](../testing-and-debugging/unit-testing-controllers-in-web-api.md)。
- 将用于创建 HTTP 响应的公共逻辑移到单独的类中。
- 通过隐藏构造响应的低级别细节，使控制器操作的意图更清晰。

**IHttpActionResult**包含单一方法**ExecuteAsync**，它以异步方式创建**HttpResponseMessage**实例。

[!code-csharp[Main](action-results/samples/sample6.cs)]

如果控制器操作返回**IHttpActionResult**，Web API 将调用**ExecuteAsync**方法来创建**HttpResponseMessage**。 然后，将**HttpResponseMessage**转换为 HTTP 响应消息。

下面是创建纯文本响应的**IHttpActionResult**的简单实现：

[!code-csharp[Main](action-results/samples/sample7.cs)]

示例控制器操作：

[!code-csharp[Main](action-results/samples/sample8.cs)]

响应：

[!code-console[Main](action-results/samples/sample9.cmd)]

更频繁地使用在 IHttpActionResult 命名空间中定义的 **[实现。](https://msdn.microsoft.com/library/system.web.http.results.aspx)** **ApiController**类定义返回这些内置操作结果的帮助器方法。

在以下示例中，如果请求与现有产品 ID 不匹配，则控制器将调用[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)来创建404（未找到）响应。 否则，控制器将调用[ApiController](https://msdn.microsoft.com/library/dn314591.aspx)，这将创建一个包含该产品的200（OK）响应。

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>其他返回类型

对于所有其他返回类型，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)来序列化返回值。 Web API 将序列化的值写入响应正文。 响应状态代码为200（正常）。

[!code-csharp[Main](action-results/samples/sample11.cs)]

这种方法的缺点是，您不能直接返回错误代码，如404。 但是，可以针对错误代码引发**带有 httpresponseexception** 。 有关详细信息，请参阅[中的异常处理 ASP.NET Web API](../error-handling/exception-handling.md)。

Web API 使用请求中的 Accept 标头来选择格式化程序。 有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。

示例请求

[!code-console[Main](action-results/samples/sample12.cmd)]

示例响应

[!code-console[Main](action-results/samples/sample13.cmd)]
