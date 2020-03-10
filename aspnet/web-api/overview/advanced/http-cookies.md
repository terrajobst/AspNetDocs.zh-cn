---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API 中的 HTTP Cookie-ASP.NET 4。x
author: MikeWasson
description: 介绍如何在 ASP.NET 4.x 的 Web API 中发送和接收 HTTP cookie。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449312"
---
# <a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API 中的 HTTP Cookie

作者： [Mike Wasson](https://github.com/MikeWasson)

本主题介绍如何在 Web API 中发送和接收 HTTP cookie。

## <a name="background-on-http-cookies"></a>HTTP Cookie 的背景

本部分简要概述了如何在 HTTP 级别实现 cookie。 有关详细信息，请参阅[RFC 6265](http://tools.ietf.org/html/rfc6265)。

Cookie 是服务器在 HTTP 响应中发送的一段数据。 客户端（可选）存储 cookie 并在后续请求中返回。 这允许客户端和服务器共享状态。 若要设置 cookie，服务器会在响应中包括一个集 Cookie 标头。 Cookie 的格式为名称-值对，具有可选属性。 例如:

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

下面是一个具有属性的示例：

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

若要将 cookie 返回到服务器，客户端会在以后的请求中包含 Cookie 标头。

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

HTTP 响应可以包括多个设置 Cookie 标头。

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

客户端使用一个 Cookie 标头返回多个 cookie。

[!code-console[Main](http-cookies/samples/sample5.cmd)]

Cookie 的范围和持续时间由设置 Cookie 标头中的以下属性控制：

- **域**：告知客户端哪个域应接收 cookie。 例如，如果域为 "example.com"，则客户端会将该 cookie 返回到 example.com 的每个子域。 如果未指定，则域为源服务器。
- **路径**：将 cookie 限制为域中的指定路径。 如果未指定，则使用请求 URI 的路径。
- **过期**：为 cookie 设置到期日期。 当 cookie 过期时，客户端会将其删除。
- **最大期限**：设置 cookie 的最大生存期。 客户端在达到最长期限时删除 cookie。

如果同时设置了 `Expires` 和 `Max-Age`，则 `Max-Age` 优先。 如果未设置，则在当前会话结束时，客户端将删除 cookie。 （"会话" 的确切含义由用户代理决定。）

但请注意，客户端可能会忽略 cookie。 例如，出于隐私原因，用户可能禁用 cookie。 在客户端过期之前，客户端可能会删除 cookie，或限制存储的 cookie 数。 出于隐私原因，客户端通常会拒绝 "第三方" cookie，其中域与源服务器不匹配。 简而言之，服务器不应依赖于取回它所设置的 cookie。

## <a name="cookies-in-web-api"></a>Web API 中的 cookie

若要将 cookie 添加到 HTTP 响应，请创建表示该 cookie 的**CookieHeaderValue**实例。 然后调用**AddCookies**扩展方法，该方法在**系统 .net 中定义。HttpResponseHeadersExtensions**类用于添加 cookie。

例如，下面的代码在控制器操作中添加了一个 cookie：

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

请注意， **AddCookies**采用**CookieHeaderValue**实例的数组。

若要从客户端请求中提取 cookie，请调用**GetCookies**方法：

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

**CookieHeaderValue**包含**CookieState**实例的集合。 每个**CookieState**都表示一个 cookie。 按照如下所示，使用索引器方法获取**CookieState** 。

## <a name="structured-cookie-data"></a>结构化 Cookie 数据

许多浏览器会限制它们将存储&#8212;总数的 cookie 数和每个域的数量。 因此，可以将结构化数据放入单个 cookie，而不是设置多个 cookie。

> [!NOTE]
> RFC 6265 未定义 cookie 数据的结构。

使用**CookieHeaderValue**类，可以传递 cookie 数据的名称/值对列表。 这些名称-值对在 Set-Cookie 标头中编码为 URL 编码的格式数据：

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

前面的代码生成以下 Set-Cookie 标头：

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

**CookieState**类提供了一个索引器方法，用于从请求消息中的 cookie 读取子值：

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>示例：在消息处理程序中设置和检索 Cookie

前面的示例演示如何在 Web API 控制器中使用 cookie。 另一种方法是使用[消息处理程序](http-message-handlers.md)。 与控制器相比，在管道中调用消息处理程序。 在请求到达控制器之前，消息处理程序可以从请求读取 cookie，或在控制器生成响应后将 cookie 添加到响应中。

![](http-cookies/_static/image2.png)

下面的代码演示了用于创建会话 Id 的消息处理程序。 会话 ID 存储在一个 cookie 中。 处理程序将检查会话 cookie 的请求。 如果请求不包括 cookie，处理程序会生成新的会话 ID。 在这两种情况下，处理程序将会话 ID 存储在**HttpRequestMessage**属性包中。 它还将会话 cookie 添加到 HTTP 响应。

此实现不会验证来自客户端的会话 ID 是否确实由服务器颁发。 不要将其用作身份验证形式！ 示例的要点是显示 HTTP cookie 管理。

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

控制器可以从**HttpRequestMessage**属性包获取会话 ID。

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
