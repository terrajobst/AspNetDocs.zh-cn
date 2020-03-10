---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API 中的 Forms 身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用 Forms 身份验证。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484376"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API 中的 Forms 身份验证

作者： [Mike Wasson](https://github.com/MikeWasson)

Forms 身份验证使用 HTML 窗体将用户的凭据发送到服务器。 它不是 Internet 标准。 Forms 身份验证仅适用于从 web 应用程序调用的 web Api，以便用户可以与 HTML 窗体进行交互。

| 优点 | 缺点 |
| --- | --- |
| -易于实现：内置于 ASP.NET 中。 -使用 ASP.NET 成员资格提供程序，以便于管理用户帐户。 | -不是标准 HTTP 身份验证机制;使用 HTTP cookie，而不是标准授权标头。 -要求使用浏览器客户端。 -以纯文本形式发送凭据。 -易受跨站点请求伪造（CSRF）的攻击;需要反 CSRF 度量值。 -难于从 nonbrowser 客户端使用。 登录需要浏览器。 -在请求中发送用户凭据。 -某些用户禁用 cookie。 |

简单地说，ASP.NET 中的窗体身份验证的工作方式如下：

1. 客户端请求要求身份验证的资源。
2. 如果用户未通过身份验证，则服务器将返回 HTTP 302 （找到）并重定向到登录页。
3. 用户输入凭据并提交窗体。
4. 服务器返回重定向回原始 URI 的另一个 HTTP 302。 此响应包括身份验证 cookie。
5. 客户端会再次请求资源。 请求包括身份验证 cookie，因此服务器将授予请求。

![](forms-authentication/_static/image1.png)

有关详细信息，请参阅[Forms 身份验证概述。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>将 Forms 身份验证用于 Web API

若要创建使用窗体身份验证的应用程序，请在 MVC 4 项目向导中选择 "Internet 应用程序" 模板。 此模板创建用于帐户管理的 MVC 控制器。 你还可以使用 ASP.NET 秋季2012更新中提供的 "单页面应用程序" 模板。

在 web API 控制器中，可以使用 `[Authorize]` 特性来限制访问权限，如[使用 [授权] 特性](authentication-and-authorization-in-aspnet-web-api.md#auth3)中所述。

Forms 身份验证使用会话 cookie 对请求进行身份验证。 浏览器自动向目标网站发送所有相关 cookie。 此功能使得表单身份验证很容易遭受跨站点请求伪造（CSRF）攻击，请参阅[防止跨站点请求伪造（CSRF）攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。

Forms 身份验证不会对用户的凭据进行加密。 因此，除非与 SSL 一起使用，否则 forms 身份验证不安全。 请参阅[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。
