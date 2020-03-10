---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用基本身份验证。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447632"
---
# <a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API 中的基本身份验证

作者： [Mike Wasson](https://github.com/MikeWasson)

基本身份验证在[RFC 2617 中定义，HTTP 身份验证：基本和摘要式访问身份验证](http://www.ietf.org/rfc/rfc2617.txt)。

缺点

- 用户凭据是在请求中发送的。
- 凭据以纯文本形式发送。
- 凭据随每个请求一起发送。
- 除了在浏览器会话结束以外，没有办法注销。
- 易受跨站点请求伪造（CSRF）的攻击;需要反 CSRF 度量值。

优点

- Internet 标准版。
- 受所有主要浏览器的支持。
- 相对简单的协议。

基本身份验证的工作原理如下所示：

1. 如果请求要求身份验证，则服务器将返回401（未授权）。 响应包括 WWW 身份验证标头，指示服务器支持基本身份验证。
2. 客户端向授权标头中的客户端凭据发送另一个请求。 凭据的格式为字符串 "名称： password"，采用 base64 编码。 凭据未加密。

基本身份验证在 "领域" 的上下文中执行。 服务器在 WWW 身份验证标头中包含领域的名称。 用户的凭据在该领域内有效。 领域的确切范围由服务器定义。 例如，你可以定义多个领域来对资源进行分区。

![](basic-authentication/_static/image1.png)

由于凭据未加密发送，因此基本身份验证仅通过 HTTPS 进行保护。 请参阅[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。

基本身份验证也容易受到 CSRF 攻击。 用户输入凭据后，浏览器会在会话期间自动将其发送到相同域的后续请求。 这包括 AJAX 请求。 请参阅[防止跨站点请求伪造（CSRF）攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。

## <a name="basic-authentication-with-iis"></a>带有 IIS 的基本身份验证

IIS 支持基本身份验证，但有一些需要注意的事项：根据用户的 Windows 凭据对用户进行身份验证。 这意味着用户必须拥有服务器域中的帐户。 对于面向公众的网站，通常需要针对 ASP.NET 成员资格提供程序进行身份验证。

若要使用 IIS 启用基本身份验证，请在 ASP.NET 项目的 web.config 中将身份验证模式设置为 "Windows"：

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

在此模式下，IIS 使用 Windows 凭据进行身份验证。 此外，还必须在 IIS 中启用基本身份验证。 在 IIS 管理器中转到 "功能" 视图，选择 "身份验证"，并启用基本身份验证。

![](basic-authentication/_static/image2.png)

在 Web API 项目中，为需要身份验证的任何控制器操作添加 `[Authorize]` 特性。

客户端通过设置请求中的 Authorization 标头对自身进行身份验证。 浏览器客户端会自动执行此步骤。 Nonbrowser 客户端将需要设置标头。

## <a name="basic-authentication-with-custom-membership"></a>具有自定义成员身份的基本身份验证

如前所述，IIS 中内置的基本身份验证使用 Windows 凭据。 这意味着你需要为你的宿主服务器上的用户创建帐户。 但对于 internet 应用程序，用户帐户通常存储在外部数据库中。

下面的代码演示如何执行基本身份验证。 您可以通过替换 `CheckPassword` 方法来轻松插入 ASP.NET 成员资格提供程序，这是本示例中的一个虚方法。

在 Web API 2 中，应考虑编写[身份验证筛选器](authentication-filters.md)或[OWIN 中间件](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模块。

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

若要启用 HTTP 模块，请将以下内容添加到**system.webserver 节中的 web.config**文件中：

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

将 "; Yourassemblyname&gt" 替换为程序集的名称（不包括 "dll" 扩展名）。

你应禁用其他身份验证方案，如窗体或 Windows 身份验证。
