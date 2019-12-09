---
title: 使用 SameSite cookie 和用于 .NET 的开放 Web 界面（OWIN）
author: rick-anderson
description: 使用 SameSite cookie 和用于 .NET 的开放 Web 界面（OWIN）
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: fc64315e8c3614e460c9a8d551bcb0848b3fe8f9
ms.sourcegitcommit: 516a168548252ff0eaae2c02ec4bd9ffcfa8375e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2019
ms.locfileid: "74951880"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a><span data-ttu-id="9a021-103">SameSite cookie 和用于 .NET 的开放 Web 接口（OWIN）</span><span class="sxs-lookup"><span data-stu-id="9a021-103">SameSite cookies and the Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="9a021-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9a021-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9a021-105">`SameSite` 是一种[IETF](https://ietf.org/about/)草案，旨在应对跨站点请求伪造（CSRF）攻击。</span><span class="sxs-lookup"><span data-stu-id="9a021-105">`SameSite` is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="9a021-106">[SameSite 2019 草案](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)：</span><span class="sxs-lookup"><span data-stu-id="9a021-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="9a021-107">默认情况下，将 cookie 视为 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="9a021-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="9a021-108">为了启用跨站点传递而显式断言 `SameSite=None` 的 cookie 应标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="9a021-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="9a021-109">`Lax` 适用于大多数应用 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a021-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="9a021-110">某些形式的身份验证，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[ws-federation](https://auth0.com/docs/protocols/ws-fed)默认为基于 POST 的重定向。</span><span class="sxs-lookup"><span data-stu-id="9a021-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="9a021-111">基于后期的重定向会触发 `SameSite` 浏览器保护，因此，对这些组件禁用了 `SameSite`。</span><span class="sxs-lookup"><span data-stu-id="9a021-111">The POST based redirects trigger the `SameSite` browser protections, so `SameSite` is disabled for these components.</span></span> <span data-ttu-id="9a021-112">由于请求的流动方式不同，大多数[OAuth](https://oauth.net/)登录名不受影响。</span><span class="sxs-lookup"><span data-stu-id="9a021-112">Most [OAuth](https://oauth.net/) logins aren't affected due to differences in how the request flows.</span></span> <span data-ttu-id="9a021-113">默认情况下，所有其他组件**不会**设置 `SameSite`，并使用客户端默认行为（旧或新）。</span><span class="sxs-lookup"><span data-stu-id="9a021-113">All other components do **not** set `SameSite` by default and use the clients default behavior (old or new).</span></span>

<span data-ttu-id="9a021-114">`None` 参数会导致实现之前[2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)（例如，iOS 12）的客户端的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="9a021-114">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="9a021-115">请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="9a021-115">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="9a021-116">发出 cookie 的每个 OWIN 组件都需要决定 `SameSite` 是否合适。</span><span class="sxs-lookup"><span data-stu-id="9a021-116">Each OWIN component that emits cookies needs to decide if `SameSite` is appropriate.</span></span>

<span data-ttu-id="9a021-117">有关本文的 ASP.NET 4.x 版本，请参阅 <xref:samesite/system-web-samesite>。</span><span class="sxs-lookup"><span data-stu-id="9a021-117">For the ASP.NET 4.x version of this article, see <xref:samesite/system-web-samesite>.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="9a021-118">使用 SameSite 的 API 用法</span><span class="sxs-lookup"><span data-stu-id="9a021-118">API usage with SameSite</span></span>

<span data-ttu-id="9a021-119">`Microsoft.Owin` 具有其自己的 `SameSite` 实现：</span><span class="sxs-lookup"><span data-stu-id="9a021-119">`Microsoft.Owin` has its own `SameSite` implementation:</span></span>

* <span data-ttu-id="9a021-120">这并不是直接依赖于 `System.Web`中的一个。</span><span class="sxs-lookup"><span data-stu-id="9a021-120">That is not directly dependent on the one in `System.Web`.</span></span>
* <span data-ttu-id="9a021-121">`SameSite` 适用于 `Microsoft.Owin` 包、.NET 4.5 和更高版本不再的所有版本。</span><span class="sxs-lookup"><span data-stu-id="9a021-121">`SameSite` works on all versions targetable by the `Microsoft.Owin` packages, .NET 4.5 and later.</span></span>
* <span data-ttu-id="9a021-122">只有[SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)组件与 `System.Web` `HttpCookie` 类直接交互。</span><span class="sxs-lookup"><span data-stu-id="9a021-122">Only the [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) component directly interacts with the `System.Web` `HttpCookie` class.</span></span>

<span data-ttu-id="9a021-123">`SystemWebCookieManager` 依赖于 .NET 4.7.2 `System.Web` Api 来启用 `SameSite` 支持，并使用修补程序来更改行为。</span><span class="sxs-lookup"><span data-stu-id="9a021-123">`SystemWebCookieManager` depends on the .NET 4.7.2 `System.Web` APIs to enable `SameSite` support, and the patches to change the behavior.</span></span>

<span data-ttu-id="9a021-124">[OWIN 和 system.web 响应 cookie 集成问题](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)中概述了使用 `SystemWebCookieManager` 的原因。</span><span class="sxs-lookup"><span data-stu-id="9a021-124">The reasons to use `SystemWebCookieManager` are outlined in [OWIN and System.Web response cookie integration issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues).</span></span> <span data-ttu-id="9a021-125">如果在 `System.Web`上运行，则建议 `SystemWebCookieManager`。</span><span class="sxs-lookup"><span data-stu-id="9a021-125">`SystemWebCookieManager` is recommended when running on `System.Web`.</span></span> 

<span data-ttu-id="9a021-126">下面的代码将 `SameSite` 设置为 `Lax`：</span><span class="sxs-lookup"><span data-stu-id="9a021-126">The following code sets `SameSite` to `Lax`:</span></span>

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

<span data-ttu-id="9a021-127">以下 Api 使用 `SameSite`：</span><span class="sxs-lookup"><span data-stu-id="9a021-127">The following APIs use `SameSite`:</span></span>

* [<span data-ttu-id="9a021-128">Owin. SameSiteMode</span><span class="sxs-lookup"><span data-stu-id="9a021-128">Microsoft.Owin.SameSiteMode</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [<span data-ttu-id="9a021-129">CookieOptions. SameSite</span><span class="sxs-lookup"><span data-stu-id="9a021-129">CookieOptions.SameSite</span></span>](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* <span data-ttu-id="9a021-130">[Cookieauthenticationoptions.authenticationtype 类](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="9a021-130">[CookieAuthenticationOptions Class](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span></span> <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [<span data-ttu-id="9a021-131">Cookieauthenticationoptions.authenticationtype. CookieSameSite</span><span class="sxs-lookup"><span data-stu-id="9a021-131">CookieAuthenticationOptions.CookieSameSite</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* <span data-ttu-id="9a021-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="9a021-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span></span>
* [<span data-ttu-id="9a021-133">SystemWebCookieManager</span><span class="sxs-lookup"><span data-stu-id="9a021-133">SystemWebCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [<span data-ttu-id="9a021-134">SystemWebChunkingCookieManager</span><span class="sxs-lookup"><span data-stu-id="9a021-134">SystemWebChunkingCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [<span data-ttu-id="9a021-135">Cookieauthenticationoptions.authenticationtype. CookieManager</span><span class="sxs-lookup"><span data-stu-id="9a021-135">CookieAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [<span data-ttu-id="9a021-136">OpenIdConnectAuthenticationOptions. CookieManager</span><span class="sxs-lookup"><span data-stu-id="9a021-136">OpenIdConnectAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a><span data-ttu-id="9a021-137">历史记录和更改</span><span class="sxs-lookup"><span data-stu-id="9a021-137">History and changes</span></span>

<span data-ttu-id="9a021-138">[Owin](https://www.nuget.org/packages/Microsoft.Owin/)从不支持[`SameSite` 2016 草案标准版](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)。</span><span class="sxs-lookup"><span data-stu-id="9a021-138">[Microsoft.Owin](https://www.nuget.org/packages/Microsoft.Owin/) never supported the [`SameSite` 2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="9a021-139">仅 `Microsoft.Owin` 4.1.0 和更高版本中提供对[SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)的支持。</span><span class="sxs-lookup"><span data-stu-id="9a021-139">Support for the [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) is only available in `Microsoft.Owin` 4.1.0 and later.</span></span> <span data-ttu-id="9a021-140">以前的版本没有修补程序。</span><span class="sxs-lookup"><span data-stu-id="9a021-140">There are no patches for prior versions.</span></span>

<span data-ttu-id="9a021-141">`SameSite` 规范的2019草案：</span><span class="sxs-lookup"><span data-stu-id="9a021-141">The 2019 draft of the `SameSite` specification:</span></span>

* <span data-ttu-id="9a021-142">**不**向后兼容2016草案。</span><span class="sxs-lookup"><span data-stu-id="9a021-142">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="9a021-143">有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="9a021-143">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="9a021-144">指定默认情况下将 cookie 视为 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="9a021-144">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="9a021-145">指定显式断言 `SameSite=None` 以便启用跨站点传递的 cookie 应标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="9a021-145">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="9a021-146">`None` 是选择退出的新项。</span><span class="sxs-lookup"><span data-stu-id="9a021-146">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="9a021-147">默认[情况下，计划](https://chromestatus.com/feature/5088147346030592)在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。</span><span class="sxs-lookup"><span data-stu-id="9a021-147">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="9a021-148">浏览器已开始在2019中移动到此标准。</span><span class="sxs-lookup"><span data-stu-id="9a021-148">Browsers started moving to this standard in 2019.</span></span>
* <span data-ttu-id="9a021-149">颁发的修补程序支持，如以下 KB 所述：</span><span class="sxs-lookup"><span data-stu-id="9a021-149">Is supported by patches issued as described in the following KB's:</span></span>
  * [<span data-ttu-id="9a021-150">知识库文章4531182</span><span class="sxs-lookup"><span data-stu-id="9a021-150">KB article 4531182</span></span>](https://support.microsoft.com/help/4531182/kb4531182)
  * [<span data-ttu-id="9a021-151">知识库文章4524421</span><span class="sxs-lookup"><span data-stu-id="9a021-151">KB article 4524421</span></span>](https://support.microsoft.com/help/4524421/kb4524421)

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="9a021-152">支持旧版浏览器</span><span class="sxs-lookup"><span data-stu-id="9a021-152">Supporting older browsers</span></span>

<span data-ttu-id="9a021-153">2016 `SameSite` 标准要求必须将未知值视为 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="9a021-153">The 2016 `SameSite` standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="9a021-154">从支持 2016 `SameSite` 标准的旧版浏览器访问的应用可能会在收到值为 `None`的 `SameSite` 属性时中断。</span><span class="sxs-lookup"><span data-stu-id="9a021-154">Apps accessed from older browsers which support the 2016 `SameSite` standard may break when they get a `SameSite` property with a value of `None`.</span></span> <span data-ttu-id="9a021-155">如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。</span><span class="sxs-lookup"><span data-stu-id="9a021-155">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="9a021-156">ASP.NET 不实现浏览器检测，因为用户代理值非常不稳定，并且经常更改。</span><span class="sxs-lookup"><span data-stu-id="9a021-156">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="9a021-157">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))中的扩展点允许插入特定于用户代理的逻辑。</span><span class="sxs-lookup"><span data-stu-id="9a021-157">An extension point in [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) allows plugging in User-Agent specific logic.</span></span>
<!-- https://docs.microsoft.com/en-us/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

<span data-ttu-id="9a021-158">在 `Startup.Configuration`中，添加类似于下面的代码：</span><span class="sxs-lookup"><span data-stu-id="9a021-158">In `Startup.Configuration`, add code similar to the following:</span></span>

[!code-csharp[](sample/Startup1.cs?name=snippet)]

<span data-ttu-id="9a021-159">前面的代码需要 .NET 4.7.2 或更高版本 `SameSite` 修补程序。</span><span class="sxs-lookup"><span data-stu-id="9a021-159">The preceding code requires the .NET 4.7.2 or later `SameSite` patch.</span></span>

<span data-ttu-id="9a021-160">下面的代码演示 `SameSiteCookieManager`的实现示例：</span><span class="sxs-lookup"><span data-stu-id="9a021-160">The following code shows an example implementation of `SameSiteCookieManager`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

<span data-ttu-id="9a021-161">在前面的示例中，`DisallowsSameSiteNone` 在 `CheckSameSite` 方法中调用。</span><span class="sxs-lookup"><span data-stu-id="9a021-161">In the preceding sample, `DisallowsSameSiteNone` is called in the `CheckSameSite` method.</span></span> <span data-ttu-id="9a021-162">`DisallowsSameSiteNone` 是一种用于检测用户代理是否不支持 `SameSite` `None`的用户方法：</span><span class="sxs-lookup"><span data-stu-id="9a021-162">`DisallowsSameSiteNone` is a user method that detects if the user agent doesn't support `SameSite` `None`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

<span data-ttu-id="9a021-163">下面的代码演示 `DisallowsSameSiteNone` 方法示例：</span><span class="sxs-lookup"><span data-stu-id="9a021-163">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="9a021-164">以下代码仅用于演示：</span><span class="sxs-lookup"><span data-stu-id="9a021-164">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="9a021-165">不应将其视为已完成。</span><span class="sxs-lookup"><span data-stu-id="9a021-165">It should not be considered complete.</span></span>
> * <span data-ttu-id="9a021-166">它不维护或不受支持。</span><span class="sxs-lookup"><span data-stu-id="9a021-166">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="9a021-167">测试应用的 SameSite 问题</span><span class="sxs-lookup"><span data-stu-id="9a021-167">Test apps for SameSite problems</span></span>

<span data-ttu-id="9a021-168">与远程站点（如通过第三方登录）交互的应用需要：</span><span class="sxs-lookup"><span data-stu-id="9a021-168">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="9a021-169">测试多个浏览器上的交互。</span><span class="sxs-lookup"><span data-stu-id="9a021-169">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="9a021-170">应用本文档中讨论的[浏览器检测和缓解措施](#sob)。</span><span class="sxs-lookup"><span data-stu-id="9a021-170">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="9a021-171">使用可选择新的 `SameSite` 行为的客户端版本测试 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9a021-171">Test web apps using a client version that can opt-in to the new `SameSite` behavior.</span></span> <span data-ttu-id="9a021-172">Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。</span><span class="sxs-lookup"><span data-stu-id="9a021-172">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="9a021-173">应用应用 `SameSite` 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari）</span><span class="sxs-lookup"><span data-stu-id="9a021-173">After your app applies the `SameSite` patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="9a021-174">有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="9a021-174">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="9a021-175">用 Chrome 测试</span><span class="sxs-lookup"><span data-stu-id="9a021-175">Test with Chrome</span></span>

<span data-ttu-id="9a021-176">Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。</span><span class="sxs-lookup"><span data-stu-id="9a021-176">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="9a021-177">Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。</span><span class="sxs-lookup"><span data-stu-id="9a021-177">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="9a021-178">已启用适当测试标志的 Chrome 76 或77提供更准确的结果。</span><span class="sxs-lookup"><span data-stu-id="9a021-178">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="9a021-179">若要测试新的 `SameSite` 行为切换 `chrome://flags/#same-site-by-default-cookies`**启用**。</span><span class="sxs-lookup"><span data-stu-id="9a021-179">To test the new `SameSite` behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="9a021-180">旧版本的 Chrome （75及更低版本）将报告为失败，并出现新的 `None` 设置。</span><span class="sxs-lookup"><span data-stu-id="9a021-180">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="9a021-181">请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="9a021-181">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="9a021-182">Google 不会使旧版 chrome 版本可用。</span><span class="sxs-lookup"><span data-stu-id="9a021-182">Google does not make older chrome versions available.</span></span> <span data-ttu-id="9a021-183">遵循[下载 Chromium](https://www.chromium.org/getting-involved/download-chromium)中的说明来测试旧版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="9a021-183">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="9a021-184">不要从通过搜索旧版 chrome 提供的**链接下载 chrome** 。</span><span class="sxs-lookup"><span data-stu-id="9a021-184">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="9a021-185">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="9a021-185">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="9a021-186">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="9a021-186">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="9a021-187">用 Safari 测试</span><span class="sxs-lookup"><span data-stu-id="9a021-187">Test with Safari</span></span>

<span data-ttu-id="9a021-188">Safari 12 严格实现了之前的草稿，在新的 `None` 值在 cookie 中时失败。</span><span class="sxs-lookup"><span data-stu-id="9a021-188">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="9a021-189">通过本文档中[支持旧版浏览](#sob)器的浏览器检测代码，可避免 `None`。</span><span class="sxs-lookup"><span data-stu-id="9a021-189">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="9a021-190">使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。</span><span class="sxs-lookup"><span data-stu-id="9a021-190">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="9a021-191">此问题依赖于基础操作系统版本。</span><span class="sxs-lookup"><span data-stu-id="9a021-191">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="9a021-192">已知 OSX Mojave （10.14）和 iOS 12 对于新 `SameSite` 行为存在兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="9a021-192">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new `SameSite` behavior.</span></span> <span data-ttu-id="9a021-193">将 OS 升级到 OSX Catalina （10.15）或 iOS 13 会解决此问题。</span><span class="sxs-lookup"><span data-stu-id="9a021-193">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="9a021-194">Safari 当前没有用于测试新规范行为的选择标记。</span><span class="sxs-lookup"><span data-stu-id="9a021-194">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="9a021-195">用 Firefox 测试</span><span class="sxs-lookup"><span data-stu-id="9a021-195">Test with Firefox</span></span>

<span data-ttu-id="9a021-196">可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在 "`about:config`" 页面上选择 "`network.cookie.sameSite.laxByDefault`的功能标志。</span><span class="sxs-lookup"><span data-stu-id="9a021-196">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="9a021-197">以前版本的 Firefox 没有出现兼容性问题的报告。</span><span class="sxs-lookup"><span data-stu-id="9a021-197">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="9a021-198">通过 Edge 浏览器进行测试</span><span class="sxs-lookup"><span data-stu-id="9a021-198">Test with Edge browser</span></span>

<span data-ttu-id="9a021-199">Edge 支持旧 `SameSite` 标准。</span><span class="sxs-lookup"><span data-stu-id="9a021-199">Edge supports the old `SameSite` standard.</span></span> <span data-ttu-id="9a021-200">边缘版本44与新的标准没有任何已知的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="9a021-200">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="9a021-201">带边缘测试（Chromium）</span><span class="sxs-lookup"><span data-stu-id="9a021-201">Test with Edge (Chromium)</span></span>

<span data-ttu-id="9a021-202">`SameSite` 在 "`edge://flags/#same-site-by-default-cookies`" 页上设置标志。</span><span class="sxs-lookup"><span data-stu-id="9a021-202">`SameSite` flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="9a021-203">未发现边缘 Chromium 的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="9a021-203">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="9a021-204">用 Electron 进行测试</span><span class="sxs-lookup"><span data-stu-id="9a021-204">Test with Electron</span></span>

<span data-ttu-id="9a021-205">Electron 的版本包括较早版本的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="9a021-205">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="9a021-206">例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。</span><span class="sxs-lookup"><span data-stu-id="9a021-206">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="9a021-207">你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。</span><span class="sxs-lookup"><span data-stu-id="9a021-207">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="9a021-208">请参阅下一节中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="9a021-208">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a021-209">其他资源</span><span class="sxs-lookup"><span data-stu-id="9a021-209">Additional resources</span></span>

* [<span data-ttu-id="9a021-210">Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置</span><span class="sxs-lookup"><span data-stu-id="9a021-210">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="9a021-211">SameSite cookie 说明</span><span class="sxs-lookup"><span data-stu-id="9a021-211">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="9a021-212">OWIN 和 System.web 响应 cookie 集成问题</span><span class="sxs-lookup"><span data-stu-id="9a021-212">OWIN and System.Web response cookie integration issues</span></span>](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)