---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 在 ASP.NET MVC 中阻止跨站点请求伪造（CSRF）攻击
author: MikeWasson
description: 介绍跨站点请求伪造（CSRF）攻击，以及如何在 ASP.NET Web MVC 中实现反 CSRF 度量值。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447110"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>阻止 ASP.NET MVC 应用程序中的跨站点请求伪造（CSRF）攻击

作者： [Mike Wasson](https://github.com/MikeWasson)

跨站点请求伪造（CSRF）是一种攻击，其中恶意站点将请求发送到用户当前登录的有漏洞站点

下面是 CSRF 攻击的示例：

1. 用户使用窗体身份验证登录 `www.example.com`。
2. 服务器对用户进行身份验证。 来自服务器的响应包含一个身份验证 cookie。
3. 如果不注销，用户将访问恶意网站。 此恶意网站包含以下 HTML 格式： 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    请注意，窗体操作会发布到易受攻击的站点，而不是恶意站点。 这是 CSRF 的 "跨站点" 部分。
4. 用户单击 "提交" 按钮。 浏览器包含请求中的身份验证 cookie。
5. 请求在服务器上使用用户的身份验证上下文运行，并可执行允许经过身份验证的用户执行的任何操作。

尽管此示例要求用户单击 "窗体" 按钮，但恶意页面可以轻松地运行自动提交窗体的脚本。 而且，使用 SSL 不会阻止 CSRF 攻击，因为恶意站点可以发送 "https://" 请求。

通常，可以对使用 cookie 进行身份验证的网站执行 CSRF 攻击，因为浏览器会将所有相关 cookie 发送到目标网站。 但是，CSRF 攻击并不局限于利用 cookie。 例如，基本身份验证和摘要式身份验证也容易受到攻击。 用户使用基本或摘要式身份验证登录后。 浏览器会自动发送凭据，直到会话结束。

## <a name="anti-forgery-tokens"></a>防伪标记

为了帮助防止 CSRF 攻击，ASP.NET MVC 使用了防伪令牌，也称为*请求验证令牌*。

1. 客户端请求包含窗体的 HTML 页面。
2. 服务器在响应中包括两个标记。 一个令牌作为 cookie 发送。 另一个被置于隐藏的窗体字段中。 令牌是随机生成的，因此，攻击者无法猜测值。
3. 当客户端提交窗体时，它必须将两个令牌都发送回服务器。 客户端将 cookie 令牌作为 cookie 发送，并在表单数据内发送窗体令牌。 （当用户提交窗体时，浏览器客户端会自动执行此功能。）
4. 如果请求不包含这两个令牌，服务器将不允许该请求。

下面是带有隐藏的窗体标记的 HTML 窗体的示例：

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

由于存在相同的源策略，恶意页面无法读取用户的令牌，因此，防伪令牌工作正常。 （[相同源策略](http://www.w3.org/Security/wiki/Same_Origin_Policy)阻止在两个不同站点上托管的文档访问彼此的内容。 因此，在前面的示例中，恶意页面可以将请求发送到 example.com，但无法读取响应。）

若要防止 CSRF 攻击，请将防伪令牌与任何身份验证协议一起使用，浏览器会在用户登录后自动发送凭据。 这包括基于 cookie 的身份验证协议（如 forms 身份验证）以及基本和摘要式身份验证等协议。

对于任何 nonsafe 方法（POST、PUT、DELETE），都应需要防伪令牌。 此外，请确保安全方法（GET、HEAD）没有任何副作用。 而且，如果你启用了跨域支持（如 CORS 或 JSONP），则甚至安全方法（如 GET）都可能容易遭受 CSRF 攻击，使得攻击者能够读取可能敏感的数据。

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>ASP.NET MVC 中的防伪令牌

若要将防伪令牌添加到 Razor 页面，请使用**HtmlHelper. AntiForgeryToken** helper 方法：

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

此方法可添加隐藏的窗体字段，还可以设置 cookie 令牌。

## <a name="anti-csrf-and-ajax"></a>反 CSRF 和 AJAX

对于 AJAX 请求，窗体标记可能是一个问题，因为 AJAX 请求可能发送 JSON 数据，而不是 HTML 表单数据。 一种解决方法是在自定义 HTTP 标头中发送令牌。 以下代码使用 Razor 语法生成令牌，然后将令牌添加到 AJAX 请求。 令牌是通过调用**防伪**在服务器上生成的。

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

处理请求时，请从请求标头中提取令牌。 然后调用**防伪**方法来验证令牌。 如果标记无效，则**Validate**方法将引发异常。

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
