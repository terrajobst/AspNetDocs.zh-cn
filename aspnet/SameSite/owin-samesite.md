---
title: 使用 SameSite cookie 和用于 .NET 的开放 Web 界面（OWIN）
author: rick-anderson
description: 使用 SameSite cookie 和用于 .NET 的开放 Web 界面（OWIN）
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: a3353fd0f0332899aaba26b83aea0ff7c3a6d19b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439478"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a>SameSite cookie 和用于 .NET 的开放 Web 接口（OWIN）

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

`SameSite` 是一种[IETF](https://ietf.org/about/)草案，旨在应对跨站点请求伪造（CSRF）攻击。 [SameSite 2019 草案](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)：

* 默认情况下，将 cookie 视为 `SameSite=Lax`。
* 为了启用跨站点传递而显式断言 `SameSite=None` 的 cookie 应标记为 `Secure`。

`Lax` 适用于大多数应用 cookie。 某些形式的身份验证，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[ws-federation](https://auth0.com/docs/protocols/ws-fed)默认为基于 POST 的重定向。 基于后期的重定向会触发 `SameSite` 浏览器保护，因此，对这些组件禁用了 `SameSite`。 由于请求的流动方式不同，大多数[OAuth](https://oauth.net/)登录名不受影响。 默认情况下，所有其他组件**不会**设置 `SameSite`，并使用客户端默认行为（旧或新）。

`None` 参数会导致实现之前[2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)（例如，iOS 12）的客户端的兼容性问题。 请参阅本文档中的[支持旧版浏览器](#sob)。

发出 cookie 的每个 OWIN 组件都需要决定 `SameSite` 是否合适。

有关本文的 ASP.NET 4.x 版本，请参阅 <xref:samesite/system-web-samesite>。

## <a name="api-usage-with-samesite"></a>使用 SameSite 的 API 用法

`Microsoft.Owin` 具有其自己的 `SameSite` 实现：

* 这并不是直接依赖于 `System.Web`中的一个。
* `SameSite` 适用于 `Microsoft.Owin` 包、.NET 4.5 和更高版本不再的所有版本。
* 只有[SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)组件与 `System.Web` `HttpCookie` 类直接交互。

`SystemWebCookieManager` 依赖于 .NET 4.7.2 `System.Web` Api 来启用 `SameSite` 支持，并使用修补程序来更改行为。

[OWIN 和 system.web 响应 cookie 集成问题](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)中概述了使用 `SystemWebCookieManager` 的原因。 如果在 `System.Web`上运行，则建议 `SystemWebCookieManager`。

下面的代码将 `SameSite` 设置为 `Lax`：

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

以下 Api 使用 `SameSite`：

* [Owin. SameSiteMode](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [CookieOptions. SameSite](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* [Cookieauthenticationoptions.authenticationtype 类](/previous-versions/aspnet/dn385599(v%3Dvs.113)) <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [Cookieauthenticationoptions.authenticationtype. CookieSameSite](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))
* [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [SystemWebChunkingCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [Cookieauthenticationoptions.authenticationtype. CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [OpenIdConnectAuthenticationOptions. CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a>历史记录和更改

[Owin](https://www.nuget.org/packages/Microsoft.Owin/)从不支持[`SameSite` 2016 草案标准版](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)。

仅 `Microsoft.Owin` 4.1.0 和更高版本中提供对[SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)的支持。 以前的版本没有修补程序。

`SameSite` 规范的2019草案：

* **不**向后兼容2016草案。 有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。
* 指定默认情况下将 cookie 视为 `SameSite=Lax`。
* 指定显式断言 `SameSite=None` 以便启用跨站点传递的 cookie 应标记为 `Secure`。 `None` 是选择退出的新项。
* 默认[情况下，计划](https://chromestatus.com/feature/5088147346030592)在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。 浏览器已开始在2019中移动到此标准。
* 按照知识库文章中的说明，发布的修补程序支持。 有关详细信息，请参阅 <xref:samesite/kbs-samesite>。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>支持旧版浏览器

2016 `SameSite` 标准要求必须将未知值视为 `SameSite=Strict` 值。 从支持 2016 `SameSite` 标准的旧版浏览器访问的应用可能会在收到值为 `None`的 `SameSite` 属性时中断。 如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。 ASP.NET 不实现浏览器检测，因为用户代理值非常不稳定，并且经常更改。 [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))中的扩展点允许插入特定于用户代理的逻辑。
<!-- https://docs.microsoft.com/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

在 `Startup.Configuration`中，添加类似于下面的代码：

[!code-csharp[](sample/Startup1.cs?name=snippet)]

前面的代码需要 .NET 4.7.2 或更高版本 `SameSite` 修补程序。

下面的代码演示 `SameSiteCookieManager`的实现示例：

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

在前面的示例中，`DisallowsSameSiteNone` 在 `CheckSameSite` 方法中调用。 `DisallowsSameSiteNone` 是一种用于检测用户代理是否不支持 `SameSite` `None`的用户方法：

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

下面的代码演示 `DisallowsSameSiteNone` 方法示例：

> [!WARNING]
> 以下代码仅用于演示：
> * 不应将其视为已完成。
> * 它不维护或不受支持。

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>测试应用的 SameSite 问题

与远程站点（如通过第三方登录）交互的应用需要：

* 测试多个浏览器上的交互。
* 应用本文档中讨论的[浏览器检测和缓解措施](#sob)。

使用可选择新的 `SameSite` 行为的客户端版本测试 web 应用。 Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。 应用应用 `SameSite` 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari） 有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。

### <a name="test-with-chrome"></a>用 Chrome 测试

Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。 Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。 已启用适当测试标志的 Chrome 76 或77提供更准确的结果。 若要测试新的 `SameSite` 行为切换 `chrome://flags/#same-site-by-default-cookies`**启用**。 旧版本的 Chrome （75及更低版本）将报告为失败，并出现新的 `None` 设置。 请参阅本文档中的[支持旧版浏览器](#sob)。

Google 不会使旧版 chrome 版本可用。 遵循[下载 Chromium](https://www.chromium.org/getting-involved/download-chromium)中的说明来测试旧版 Chrome。 不要从通过搜索旧版 chrome 提供的**链接下载 chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>用 Safari 测试

Safari 12 严格实现了之前的草稿，在新的 `None` 值在 cookie 中时失败。 通过本文档中[支持旧版浏览](#sob)器的浏览器检测代码，可避免 `None`。 使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。 问题取决于基础 OS 版本。 已知 OSX Mojave （10.14）和 iOS 12 对于新 `SameSite` 行为存在兼容性问题。 将 OS 升级到 OSX Catalina （10.15）或 iOS 13 会解决此问题。 Safari 当前没有用于测试新规范行为的选择标记。

### <a name="test-with-firefox"></a>用 Firefox 测试

可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在 "`about:config`" 页面上选择 "`network.cookie.sameSite.laxByDefault`的功能标志。 以前版本的 Firefox 没有出现兼容性问题的报告。

### <a name="test-with-edge-browser"></a>通过 Edge 浏览器进行测试

Edge 支持旧 `SameSite` 标准。 边缘版本44与新的标准没有任何已知的兼容性问题。

### <a name="test-with-edge-chromium"></a>带边缘测试（Chromium）

`SameSite` 在 "`edge://flags/#same-site-by-default-cookies`" 页上设置标志。 未发现边缘 Chromium 的兼容性问题。

### <a name="test-with-electron"></a>用 Electron 进行测试

Electron 的版本包括较早版本的 Chromium。 例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。 你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。 请参阅下一节中的[支持旧版浏览器](#sob)。

## <a name="additional-resources"></a>其他资源

* [Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 说明](https://web.dev/samesite-cookies-explained/)
* [OWIN 和 System.web 响应 cookie 集成问题](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
