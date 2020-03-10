---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 使用个人帐户和本地登录名保护 Web API ASP.NET Web API 2.2 |Microsoft Docs
author: MikeWasson
description: 本主题演示如何使用 OAuth2 对成员资格数据库进行身份验证的 web API 的安全。 教程中使用的软件版本 Visual Studio 201 。
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447176"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>在 ASP.NET Web API 2.2 中使用个人帐户和本地登录保护 Web API

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载示例应用](https://github.com/MikeWasson/LocalAccountsApp)

> 本主题演示如何使用 OAuth2 对成员资格数据库进行身份验证的 web API 的安全。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - [Visual Studio 2013 Update 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [Web API 2。2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Identity 2。1](../../../identity/index.md)

在 Visual Studio 2013 中，Web API 项目模板提供了三个身份验证选项：

- **个人帐户。** 应用使用成员资格数据库。
- **组织帐户。** 用户通过其 Azure Active Directory、Office 365 或本地 Active Directory 凭据进行登录。
- **Windows 身份验证。** 此选项适用于 Intranet 应用程序，并使用 Windows 身份验证 IIS 模块。

有关这些选项的更多详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)。

单个帐户为用户提供了两种登录方式：

- **本地登录名**。 用户在站点上注册，并输入用户名和密码。 此应用将密码哈希存储在成员资格数据库中。 当用户登录时，ASP.NET Identity 系统会验证密码。
- **社交登录**。 用户使用外部服务（如 Facebook、Microsoft 或 Google）登录。 应用仍会在成员资格数据库中为用户创建一个条目，但不会存储任何凭据。 用户通过登录到外部服务进行身份验证。

本文介绍本地登录方案。 对于本地和社交登录，Web API 都使用 OAuth2 来对请求进行身份验证。 但对于本地和社交登录，凭据流是不同的。

在本文中，我将演示一个简单的应用程序，该应用程序允许用户登录并将经过身份验证的 AJAX 调用发送到 web API。 你可以在[此处](https://github.com/MikeWasson/LocalAccountsApp)下载代码示例。 该自述文件介绍了如何在 Visual Studio 中从头开始创建示例。

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

示例应用使用挖空的数据绑定和 jQuery 来发送 AJAX 请求。 我将重点介绍 AJAX 调用，因此，您不需要了解本文的挖空。

在此过程中，我将介绍：

- 应用在客户端执行的操作。
- 服务器上发生了什么情况。
- 中间的 HTTP 流量。

首先，我们需要定义一些 OAuth2 术语。

- *资源*。 可以保护的某些数据片段。
- *资源服务器*。 承载资源的服务器。
- *资源所有者*。 可授予对资源的访问权限的实体。 （通常为用户。）
- *Client*：要访问资源的应用。 在本文中，客户端是一个 web 浏览器。
- *访问令牌*。 用于授予对资源的访问权限的令牌。
- *持有者令牌*。 特定类型的访问令牌，其中包含任何人都可以使用令牌的属性。 换句话说，客户端不需要加密密钥或其他机密即可使用持有者令牌。 出于此原因，持有者令牌只应在 HTTPS 上使用，并且应具有相对较短的过期时间。
- *授权服务器*。 提供访问令牌的服务器。

应用程序可以同时充当授权服务器和资源服务器。 Web API 项目模板遵循此模式。

## <a name="local-login-credential-flow"></a>本地登录凭据流

对于本地登录，Web API 使用 OAuth2 中定义的[资源所有者密码流](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)。

1. 用户在客户端中输入名称和密码。
2. 客户端会将这些凭据发送到授权服务器。
3. 授权服务器对凭据进行身份验证并返回一个访问令牌。
4. 若要访问受保护的资源，客户端在 HTTP 请求的授权标头中包含访问令牌。

![](individual-accounts-in-web-api/_static/image3.png)

当你在 Web API 项目模板中选择**单个帐户**时，该项目将包括验证用户凭据和颁发令牌的授权服务器。 下图显示了 Web API 组件方面的相同凭据流。

![](individual-accounts-in-web-api/_static/image4.png)

在这种情况下，Web API 控制器充当资源服务器。 身份验证筛选器验证访问令牌，而 **[授权]** 属性用于保护资源。 当控制器或操作具有 " **[授权]** " 属性时，对该控制器或操作的所有请求都必须经过身份验证。 否则，将拒绝授权，并且 Web API 将返回401（未授权）错误。

授权服务器和身份验证筛选器都调用[OWIN 中间件](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)组件来处理 OAuth2 的详细信息。 在本教程的后面部分，我将更详细地介绍设计。

## <a name="sending-an-unauthorized-request"></a>发送未经授权的请求

若要开始，请运行应用，并单击 "**调用 API** " 按钮。 请求完成后，"**结果**" 框中会显示一条错误消息。 这是因为请求不包含访问令牌，因此请求未经授权。

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

"**调用 API** " 按钮将 AJAX 请求发送到 ~/api/values，后者调用 Web API 控制器操作。 下面是发送 AJAX 请求的 JavaScript 代码部分。 在示例应用中，所有 JavaScript 应用代码位于 Scripts\app.js 文件中。

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

在用户登录之前，没有持有者令牌，因此请求中没有任何授权标头。 这将导致请求返回401错误。

下面是 HTTP 请求。 （我使用[Fiddler](http://www.telerik.com/fiddler)捕获 HTTP 流量。）

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

HTTP 响应：

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

请注意，响应包含一个 Www 验证标头，其质询设置为 "持有者"。 指示服务器需要持有者令牌的。

## <a name="register-a-user"></a>注册用户

在应用的 "**注册**" 部分中，输入电子邮件和密码，然后单击 "**注册**" 按钮。

对于本示例，无需使用有效的电子邮件地址，但真正的应用会确认该地址。 （请参阅[创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。）对于密码，请使用类似于 "Password1！" 的内容，其中包含大写字母、小写字母、数字和非字母数字字符。 为了使应用程序保持简单，我省略了客户端验证，因此，如果密码格式有问题，会收到400（错误请求）错误。

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

"**注册**" 按钮将 POST 请求发送到 ~/api/Account/Register/。 请求正文是一个包含用户名和密码的 JSON 对象。 下面是发送请求的 JavaScript 代码：

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

HTTP 请求：

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

HTTP 响应：

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

此请求由 `AccountController` 类处理。 在内部，`AccountController` 使用 ASP.NET Identity 来管理成员资格数据库。

如果从 Visual Studio 本地运行应用，用户帐户将存储在 LocalDB 中的 AspNetUsers 表中。 若要在 Visual Studio 中查看表，请单击 "**视图**" 菜单，选择 "**服务器资源管理器**"，然后展开 "**数据连接**"。

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>获取访问令牌

到目前为止，我们尚未执行任何 OAuth，但现在我们会在请求访问令牌时，在操作中看到 OAuth 授权服务器。 在示例应用程序的 "**登录**" 区域中，输入电子邮件和密码，并单击 "**登录**"。

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

"**登录**" 按钮向令牌终结点发送请求。 请求正文包含以下形式的 url 编码数据：

- 授予\_类型： "密码"
- username： &lt;用户的电子邮件&gt;
- 密码： &lt;密码&gt;

下面是发送 AJAX 请求的 JavaScript 代码：

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

如果请求成功，授权服务器将在响应正文中返回一个访问令牌。 请注意，我们将标记存储在会话存储中，以便在稍后将请求发送到 API 时使用。 与某些形式的身份验证不同（例如基于 cookie 的身份验证），浏览器不会自动在后续请求中包含访问令牌。 应用程序必须显式执行此操作。 这是一件好事，因为它限制了[CSRF 漏洞](preventing-cross-site-request-forgery-csrf-attacks.md)。

HTTP 请求：

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

你可以看到该请求包含用户的凭据。 *必须*使用 HTTPS 来提供传输层安全性。

HTTP 响应：

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

为方便起见，我缩进了 JSON 并截断了访问令牌，这是一个很长的时间。

`access_token`、`token_type`和 `expires_in` 属性由 OAuth2 规范定义。其他属性（`userName`、`.issued`和 `.expires`）只用于提供信息。 您可以在/Providers/ApplicationOAuthProvider.cs 文件的 `TokenEndpoint` 方法中找到添加这些附加属性的代码。

## <a name="send-an-authenticated-request"></a>发送经过身份验证的请求

现在我们有了持有者令牌，接下来我们可以向 API 发出经过身份验证的请求。 这是通过设置请求中的 Authorization 标头来完成的。 再次单击 "**调用 API** " 按钮以查看此。

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

HTTP 请求：

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

HTTP 响应：

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>注销

由于浏览器不缓存凭据或访问令牌，因此注销只需从会话存储中删除令牌即可 "忘记密码"：

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>了解各个帐户的项目模板

当你在 "ASP.NET Web 应用程序" 项目模板中选择**单个帐户**时，该项目包括：

- OAuth2 授权服务器。
- 用于管理用户帐户的 Web API 终结点
- 用于存储用户帐户的 EF 模型。

下面是实现这些功能的主要应用程序类：

- `AccountController`。 提供用于管理用户帐户的 Web API 终结点。 `Register` 操作是本教程中使用的唯一操作。 类上的其他方法支持重置密码、社交登录和其他功能。
- `ApplicationUser`，在/Models/IdentityModels.cs. 中定义 此类是成员资格数据库中用户帐户的 EF 模型。
- `ApplicationUserManager`，在/App\_Start/IdentityConfig 中定义。 cs 此类派生自[UserManager](https://msdn.microsoft.com/library/dn613290.aspx) ，对用户帐户执行操作，例如创建新用户、验证密码等，并自动保存对数据库所做的更改。
- `ApplicationOAuthProvider`。 此对象将插入到 OWIN 中间件，并处理中间件所引发的事件。 它派生自[OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)。

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>配置授权服务器

在 StartupAuth.cs 中，以下代码将配置 OAuth2 授权服务器。

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

`TokenEndpointPath` 属性是授权服务器终结点的 URL 路径。 这是应用用于获取持有者令牌的 URL。

`Provider` 属性指定插入到 OWIN 中间件的提供程序，并处理中间件所引发的事件。

下面是应用想要获取令牌时的基本流程：

1. 若要获取访问令牌，应用会将请求发送到 ~/Token。
2. OAuth 中间件调用提供程序 `GrantResourceOwnerCredentials`。
3. 提供程序调用 `ApplicationUserManager` 来验证凭据并创建声明标识。
4. 如果成功，则提供程序将创建用于生成令牌的身份验证票证。

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

OAuth 中间件不知道有关用户帐户的任何信息。 提供程序在中间件和 ASP.NET Identity 之间进行通信。 有关实施授权服务器的详细信息，请参阅[OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)。

### <a name="configuring-web-api-to-use-bearer-tokens"></a>将 Web API 配置为使用持有者令牌

在 `WebApiConfig.Register` 方法中，以下代码将设置 Web API 管道的身份验证：

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

**HostAuthenticationFilter**类启用使用持有者令牌进行身份验证。

**Config.suppressdefaulthostauthentication**方法告诉 Web API 忽略任何在请求之前通过 IIS 或 OWIN 中间件进行的身份验证。 如此，便可以限制 Web API 仅使用持有者令牌进行身份验证。

> [!NOTE]
> 特别是，你的应用程序的 MVC 部分可能使用 forms 身份验证，该身份验证将凭据存储在一个 cookie 中。 基于 Cookie 的身份验证需要使用防伪令牌来防止 CSRF 攻击。 这对于 web Api 是一个问题，因为 web API 无法方便地将防伪标记发送到客户端。 （有关此问题的更多背景信息，请参阅[在 WEB API 中阻止 CSRF 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。）调用**config.suppressdefaulthostauthentication**可确保 Web API 容易受到 cookie 中存储的凭据的 CSRF 攻击。

当客户端请求受保护的资源时，以下是 Web API 管道中发生的情况：

1. **HostAuthentication**筛选器调用 OAuth 中间件来验证令牌。
2. 中间件将令牌转换为声明标识。
3. 此时，请求已*通过身份验证*，但未*获得授权*。
4. 授权筛选器检查声明标识。 如果声明向用户授权该资源，则请求已获得授权。 默认情况下， **[授权]** 属性将对任何经过身份验证的请求进行授权。 但是，你可以按角色或其他声明授权。 有关详细信息，请参阅[WEB API 中的身份验证和授权](authentication-and-authorization-in-aspnet-web-api.md)。
5. 如果前面的步骤成功，控制器将返回受保护的资源。 否则，客户端将收到401（未授权）错误。

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>其他资源

- [ASP.NET Identity](../../../identity/index.md)
- [了解适用于 VS2013 RC 的 SPA 模板中的安全功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)。 Hongye Sun 的 MSDN 博客文章。
- [二级 WEB API 个人帐户模板–第2部分：本地帐户](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。 Dominick Baier 的博客文章。
- [主机身份验证和具有 OWIN 的 WEB API](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)。 Brock Allen 的 `SuppressDefaultHostAuthentication` 和 `HostAuthenticationFilter` 的很好的说明。
- [自定义 VS 2013 模板 ASP.NET Identity 中的配置文件信息](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。 MSDN 博客文章 Pranav Rastogi 撰写。
- [ASP.NET Identity 中的 UserManager 类的按请求生存期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。 MSDN 博客文章 Suhas Joshi，具有对 `UserManager` 类的良好说明。
