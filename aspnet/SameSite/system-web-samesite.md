---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 了解如何使用在 ASP.NET 中 SameSite cookie
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c81ca38648609aa5347d2a8cc11889fc85d81711
ms.sourcegitcommit: 4d439e01c82c7c95b19216fedaf5b1a11a1deb06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76826609"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>在 ASP.NET 中使用 SameSite cookie

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite 是一种[IETF](https://ietf.org/about/)草案标准，旨在提供一些针对跨站点请求伪造（CSRF）攻击的防护。 最初在[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)中起草草案标准版已在[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)中更新。 更新的标准与以前的标准不是向后兼容，以下是最明显的区别：

* 默认情况下，不带 SameSite 标头的 cookie 被视为 `SameSite=Lax`。
* `SameSite=None` 必须用于允许跨站点 cookie。
* 断言 `SameSite=None` 的 cookie 也必须标记为 `Secure`。
* [2016 标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允许值 SameSite = None，导致某些实现将此类 Cookie 视为 SameSite = Strict。 请参阅本文档中的[支持旧版浏览器](#sob)。

`SameSite=Lax` 设置适用于大多数应用程序 cookie。 某些形式的身份验证，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[ws-federation](https://auth0.com/docs/protocols/ws-fed)默认为基于 POST 的重定向。 基于后期的重定向会触发 SameSite 浏览器保护，因此，对这些组件禁用了 SameSite。 由于请求的流动方式不同，大多数[OAuth](https://oauth.net/)登录名不受影响。

使用 `iframe` 的应用程序可能会遇到 `SameSite=Lax` 或 `SameSite=Strict` cookie 的问题，因为 iframe 被视为跨站点方案。

发出 cookie 的每个 ASP.NET 组件都需要确定 SameSite 是否适用。

在安装 2019 .Net SameSite 更新后，请参阅应用程序问题的[已知问题](#known)。

## <a name="using-samesite-in-aspnet-472-and-48"></a>在 ASP.NET 4.7.2 和4.8 中使用 SameSite

.Net 4.7.2 和4.8 支持 SameSite 的[2019 草案标准](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)，因为年12月2019更新发布。 开发人员可以使用[HttpCookie 属性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)以编程方式控制 SameSite 标头的值。 将 `SameSite` 属性设置为 `Strict`、`Lax`或 `None` 会导致这些值用 cookie 写入网络中。 将其设置为等于 `(SameSiteMode)(-1)` 指示网络上不应包含 cookie 的 SameSite 标头。 [HttpCookie 属性](/dotnet/api/system.web.httpcookie.secure)（或配置文件中的 "requireSSL"）可用于将 cookie 标记为 `Secure`。

新 `HttpCookie` 实例将默认为 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false`。 可以在 `system.web/httpCookies` 配置节中重写这些默认值，其中字符串 `"Unspecified"` 是 `(SameSiteMode)(-1)`的友好仅配置语法：

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net 还为这些功能颁发了自己的四个特定 cookie：匿名身份验证、Forms 身份验证、会话状态和角色管理。 在运行时获取的这些 cookie 的实例可以使用 `SameSite` 和 `Secure` 属性进行操作，就像使用任何其他 HttpCookie 实例一样。 然而，由于 SameSite 标准的大杂烩出现，这四个功能 cookie 的配置选项不一致。 相关配置节和属性的默认值如下所示。 如果某个功能没有 `SameSite` 或 `Secure` 相关属性，则该功能将回退前面讨论的 `system.web/httpCookies` 部分中配置的默认值。

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequiresSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**注意**：目前仅可 `system.web/httpCookies@sameSite` "未指定"。 我们希望在以后的更新中，将类似语法添加到前面所示的 cookieSameSite 属性。 在代码中设置 `(SameSiteMode)(-1)` 仍适用于这些 cookie 的实例。 *

## <a name="history-and-changes"></a>历史记录和更改

SameSite 支持是在使用[2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)的 .net 4.7.2 中首次实现的。

2019年11月19日更新了 Windows 更新后的 .NET 4.7.2 + 2016 标准版和2019标准版。 其他版本的 Windows 即将推出其他更新。 有关更多信息，请参见<xref:samesite/kbs-samesite>。

 SameSite 规范的2019草案：

* **不**向后兼容2016草案。 有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。
* 指定默认情况下将 cookie 视为 `SameSite=Lax`。
* 指定显式断言 `SameSite=None` 以便启用跨站点传递的 cookie 也应该标记为 `Secure`。
* 按照上面列出的 KB 中所述，发布的修补程序支持。
* 默认[情况下，计划](https://chromestatus.com/feature/5088147346030592)在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。 浏览器已开始在2019中移动到此标准。

<a name="known"><a/>

## <a name="known-issues"></a>已知问题

因为2016和2019草案规范不兼容，所以，11月 2019 .Net Framework 更新引入了一些可能会中断的更改。

* 会话状态和窗体身份验证 cookie 现在作为 `Lax` 写入到网络，而不是未指定。
  * 大多数应用程序都适用于 `SameSite=Lax` cookie，在使用 `iframe` 的站点或应用程序中发布的应用程序可能会发现其会话状态或窗体授权 cookie 没有按预期方式使用。 若要解决此情况，请在前面所述的相应配置节中更改 `cookieSameSite` 值。
* HttpCookies 在代码或配置中显式设置 `SameSite=None` 现在使用 cookie 写入该值，而以前省略了该值。 这可能会导致旧版浏览器出现一些仅支持2016草案标准的问题。
  * 面向支持2019草案标准的浏览器 `SameSite=None` cookie 时，还应将其标记 `Secure` 或无法识别。
  * 若要恢复为不写入 `SameSite=None`的2016行为，请使用 "应用设置" `aspnet:SupressSameSiteNone=true`。 请注意，这将适用于应用中的所有 HttpCookies。

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service — SameSite cookie 处理

请参阅[Azure App Service-SameSite cookie 处理和 .NET Framework 4.7.2 修补程序](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)，以获取有关 Azure App Service 如何在 .net 4.7.2 apps 中配置 SameSite 行为的信息。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>支持旧版浏览器

2016 SameSite 标准规定，未知值必须被视为 `SameSite=Strict` 值。 从支持 2016 SameSite 标准的旧版浏览器访问的应用可能会在收到值为 "`None`" 的 SameSite 属性时中断。 如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。 ASP.NET 不实现浏览器检测，因为用户代理值非常不稳定，并且经常更改。 可以在 <xref:HTTP.HttpCookie> 调用站点调用以下代码：

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

在前面的示例中，`MyUserAgentDetectionLib.DisallowsSameSiteNone` 是一个用户提供的库，用于检测用户代理是否不支持 SameSite `None`。 下面的代码演示 `DisallowsSameSiteNone` 方法示例：

> [!WARNING]
> 以下代码仅用于演示：
> * 不应将其视为已完成。
> * 它不维护或不受支持。

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>测试应用的 SameSite 问题

与远程站点（如通过第三方登录）交互的应用需要：

* 测试多个浏览器上的交互。
* 应用本文档中讨论的[浏览器检测和缓解措施](#sob)。

使用可选择新的 SameSite 行为的客户端版本测试 web 应用。 Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。 应用应用 SameSite 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari） 有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。

### <a name="test-with-chrome"></a>用 Chrome 测试

Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。 Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。 已启用适当测试标志的 Chrome 76 或77提供更准确的结果。 若要测试新的 SameSite 行为，请切换 `chrome://flags/#same-site-by-default-cookies`**启用**。 旧版本的 Chrome （75及更低版本）将报告为失败，并出现新的 `None` 设置。 请参阅本文档中的[支持旧版浏览器](#sob)。

Google 不会使旧版 chrome 版本可用。 遵循[下载 Chromium](https://www.chromium.org/getting-involved/download-chromium)中的说明来测试旧版 Chrome。 不要从通过搜索旧版 chrome 提供的**链接下载 chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>用 Safari 测试

Safari 12 严格实现了之前的草稿，在新的 `None` 值在 cookie 中时失败。 通过本文档中[支持旧版浏览](#sob)器的浏览器检测代码，可避免 `None`。 使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。 问题取决于基础 OS 版本。 已知 OSX Mojave （10.14）和 iOS 12 与新的 SameSite 行为存在兼容性问题。 将 OS 升级到 OSX Catalina （10.15）或 iOS 13 会解决此问题。 Safari 当前没有用于测试新规范行为的选择标记。

### <a name="test-with-firefox"></a>用 Firefox 测试

可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在 "`about:config`" 页面上选择 "`network.cookie.sameSite.laxByDefault`的功能标志。 以前版本的 Firefox 没有出现兼容性问题的报告。

### <a name="test-with-edge-browser"></a>通过 Edge 浏览器进行测试

Edge 支持旧的 SameSite 标准。 边缘版本44与新的标准没有任何已知的兼容性问题。

### <a name="test-with-edge-chromium"></a>带边缘测试（Chromium）

在 `edge://flags/#same-site-by-default-cookies` 页上设置 SameSite 标志。 未发现边缘 Chromium 的兼容性问题。

### <a name="test-with-electron"></a>用 Electron 进行测试

Electron 的版本包括较早版本的 Chromium。 例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。 你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。 请参阅下一节中的[支持旧版浏览器](#sob)。

## <a name="additional-resources"></a>其他资源

* [即将推出 SameSite Cookie 更改 ASP.NET 和 ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 说明](https://web.dev/samesite-cookies-explained/)
