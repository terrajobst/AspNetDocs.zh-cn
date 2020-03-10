---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 在 ASP.NET Web API 中发送 HTML 窗体数据： url 编码 ASP.NET
author: MikeWasson
description: 本文介绍如何使用 ASP.NET 4.x 将 url 编码数据发布到 Web API 控制器
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449240"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>在 ASP.NET Web API 中发送 HTML 窗体数据：窗体 url 编码数据

作者： [Mike Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>第1部分：窗体 url 编码数据

本文介绍了如何将 url 编码数据发布到 Web API 控制器。

- [HTML 窗体概述](#overview_of_html_forms)
- [发送复杂类型](#sending_complex_types)
- [通过 AJAX 发送窗体数据](#sending_form_data_via_ajax)
- [发送简单类型](#sending_simple_types)

> [!NOTE]
> [下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML 窗体概述

HTML 窗体使用 GET 或 POST 将数据发送到服务器。 **Form**元素的**METHOD**属性提供 HTTP 方法：

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

默认方法为 GET。 如果窗体使用 GET，则窗体数据在 URI 中将编码为查询字符串。 如果窗体使用 POST，则窗体数据将置于请求正文中。 对于已发布的数据， **enctype**特性指定请求正文的格式：

| enctype | 说明 |
| --- | --- |
| application/x-www-form-urlencoded | 窗体数据被编码为名称/值对，类似于 URI 查询字符串。 这是 POST 的默认格式。 |
| 多部分/窗体数据 | 表单数据编码为多部分 MIME 消息。 如果要将文件上传到服务器，则使用此格式。 |

本文的第1部分介绍了 x-www 格式的 url 编码格式。 [第2部分](sending-html-form-data-part-2.md)介绍多部分 MIME。

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>发送复杂类型

通常，您将发送由多个窗体控件中的值组成的复杂类型。 请考虑以下代表状态更新的模型：

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

下面是通过 POST 接受 `Update` 对象的 Web API 控制器。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> 此控制器使用[基于操作的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此路由模板 &quot;api/{controller}/{action}/{id}&quot;。 客户端会将数据发布到 &quot;/api/updates/complex&quot;。

现在，让我们编写一个 HTML 窗体供用户提交状态更新。

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

请注意，窗体上的**操作**属性是控制器操作的 URI。 下面是在中输入一些值的窗体：

![](sending-html-form-data-part-1/_static/image1.png)

当用户单击 "提交" 时，浏览器发送 HTTP 请求，如下所示：

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

请注意，请求正文包含格式为名称/值对的窗体数据。 Web API 会自动将名称/值对转换为 `Update` 类的实例。

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>通过 AJAX 发送窗体数据

当用户提交窗体时，浏览器从当前页面导航到，并呈现响应消息的正文。 当响应为 HTML 页面时，这是正常的。 但对于 web API，响应正文通常为空或包含结构化数据（如 JSON）。 在这种情况下，使用 AJAX 请求发送窗体数据会更有意义，使页面可以处理响应。

下面的代码演示如何使用 jQuery 发布表单数据。

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery **submit**函数将 form 操作替换为新函数。 这将覆盖 "提交" 按钮的默认行为。 **序列化**函数会将窗体数据序列化为名称/值对。 若要将表单数据发送到服务器，请调用 `$.post()`。

请求完成后，`.success()` 或 `.error()` 处理程序将向用户显示相应的消息。

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>发送简单类型

在前面的部分中，我们发送了复杂类型，该类型的 Web API 反序列化为模型类的实例。 您还可以发送简单类型，如字符串。

> [!NOTE]
> 在发送简单类型之前，请考虑改为将值包装在复杂类型中。 这为你提供了服务器端模型验证的优点，并使你可以在需要时更轻松地扩展模型。

发送简单类型的基本步骤是相同的，但有两个细微差别。 首先，在控制器中，必须用**FromBody**属性修饰参数名称。

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

默认情况下，Web API 尝试从请求 URI 获取简单类型。 **FromBody**特性告诉 Web API 从请求正文中读取值。

> [!NOTE]
> Web API 最多读取一次响应正文，因此一个操作的一个参数只能来自请求正文。 如果需要从请求正文中获取多个值，请定义一个复杂类型。

其次，客户端需要发送以下格式的值：

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

具体而言，简单类型的名称/值对的名称部分必须为空。 并非所有浏览器都支持 HTML 窗体，但您在脚本中创建了以下格式，如下所示：

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

下面是一个示例窗体：

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

下面是用于提交窗体值的脚本。 与前一个脚本的唯一区别是传递到**post**函数的参数。

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

可以使用相同的方法来发送简单类型的数组：

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>其他资源

[第2部分：文件上传和多部分 MIME](sending-html-form-data-part-2.md)
