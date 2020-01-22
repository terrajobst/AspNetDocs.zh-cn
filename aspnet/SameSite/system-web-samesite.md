---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 了解如何使用在 ASP.NET 中 SameSite cookie
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: d2160bd9aeb93398b49b3a0e5e7a8a4404a5bc63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519188"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="d23e5-103">在 ASP.NET 中使用 SameSite cookie</span><span class="sxs-lookup"><span data-stu-id="d23e5-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="d23e5-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d23e5-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d23e5-105">SameSite 是一种[IETF](https://ietf.org/about/)草案，旨在针对跨站点请求伪造（CSRF）攻击提供某些防护。</span><span class="sxs-lookup"><span data-stu-id="d23e5-105">SameSite is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="d23e5-106">[SameSite 2019 草案](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)：</span><span class="sxs-lookup"><span data-stu-id="d23e5-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="d23e5-107">默认情况下，将 cookie 视为 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="d23e5-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="d23e5-108">为了启用跨站点传递而显式断言 `SameSite=None` 的 cookie 应标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="d23e5-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="d23e5-109">`Lax` 适用于大多数应用 cookie。</span><span class="sxs-lookup"><span data-stu-id="d23e5-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="d23e5-110">某些形式的身份验证，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[ws-federation](https://auth0.com/docs/protocols/ws-fed)默认为基于 POST 的重定向。</span><span class="sxs-lookup"><span data-stu-id="d23e5-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="d23e5-111">基于后期的重定向会触发 SameSite 浏览器保护，因此，对这些组件禁用了 SameSite。</span><span class="sxs-lookup"><span data-stu-id="d23e5-111">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="d23e5-112">由于请求的流动方式不同，大多数[OAuth](https://oauth.net/)登录名不受影响。</span><span class="sxs-lookup"><span data-stu-id="d23e5-112">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="d23e5-113">`None` 参数会导致实现之前[2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)（例如，iOS 12）的客户端的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d23e5-113">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="d23e5-114">请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-114">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="d23e5-115">发出 cookie 的每个 ASP.NET 组件都需要确定 SameSite 是否适用。</span><span class="sxs-lookup"><span data-stu-id="d23e5-115">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="d23e5-116">使用 SameSite 的 API 用法</span><span class="sxs-lookup"><span data-stu-id="d23e5-116">API usage with SameSite</span></span>

<span data-ttu-id="d23e5-117">请参阅[HttpCookie. SameSite 属性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)</span><span class="sxs-lookup"><span data-stu-id="d23e5-117">See [HttpCookie.SameSite Property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="d23e5-118">历史记录和更改</span><span class="sxs-lookup"><span data-stu-id="d23e5-118">History and changes</span></span>

<span data-ttu-id="d23e5-119">SameSite 支持是在使用[2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)的 .net 4.7.2 中首次实现的。</span><span class="sxs-lookup"><span data-stu-id="d23e5-119">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="d23e5-120">2019年11月19日更新了 Windows 更新后的 .NET 4.7.2 + 2016 标准版和2019标准版。</span><span class="sxs-lookup"><span data-stu-id="d23e5-120">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="d23e5-121">其他版本的 Windows 即将推出其他更新。</span><span class="sxs-lookup"><span data-stu-id="d23e5-121">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="d23e5-122">有关更多信息，请参见<xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="d23e5-122">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="d23e5-123">SameSite 规范的2019草案：</span><span class="sxs-lookup"><span data-stu-id="d23e5-123">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="d23e5-124">**不**向后兼容2016草案。</span><span class="sxs-lookup"><span data-stu-id="d23e5-124">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="d23e5-125">有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-125">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="d23e5-126">指定默认情况下将 cookie 视为 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="d23e5-126">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="d23e5-127">指定显式断言 `SameSite=None` 以便启用跨站点传递的 cookie 应标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="d23e5-127">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="d23e5-128">`None` 是选择退出的新项。</span><span class="sxs-lookup"><span data-stu-id="d23e5-128">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="d23e5-129">按照上面列出的 KB 中所述，发布的修补程序支持。</span><span class="sxs-lookup"><span data-stu-id="d23e5-129">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="d23e5-130">默认[情况下，计划](https://chromestatus.com/feature/5088147346030592)在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。</span><span class="sxs-lookup"><span data-stu-id="d23e5-130">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="d23e5-131">浏览器已开始在2019中移动到此标准。</span><span class="sxs-lookup"><span data-stu-id="d23e5-131">Browsers started moving to this standard in 2019.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="d23e5-132">Azure App Service — SameSite cookie 处理</span><span class="sxs-lookup"><span data-stu-id="d23e5-132">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="d23e5-133">有关详细信息，请参阅[Azure App Service-SameSite cookie 处理和 .NET Framework 4.7.2 修补程序](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-133">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for more information.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="d23e5-134">支持旧版浏览器</span><span class="sxs-lookup"><span data-stu-id="d23e5-134">Supporting older browsers</span></span>

<span data-ttu-id="d23e5-135">2016 SameSite 标准规定，未知值必须被视为 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="d23e5-135">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="d23e5-136">从支持 2016 SameSite 标准的旧版浏览器访问的应用可能会在收到值为 "`None`" 的 SameSite 属性时中断。</span><span class="sxs-lookup"><span data-stu-id="d23e5-136">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="d23e5-137">如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。</span><span class="sxs-lookup"><span data-stu-id="d23e5-137">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="d23e5-138">ASP.NET 不实现浏览器检测，因为用户代理值非常不稳定，并且经常更改。</span><span class="sxs-lookup"><span data-stu-id="d23e5-138">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="d23e5-139">可以在 <xref:HTTP.HttpCookie> 调用站点调用以下代码：</span><span class="sxs-lookup"><span data-stu-id="d23e5-139">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="d23e5-140">在前面的示例中，`MyUserAgentDetectionLib.DisallowsSameSiteNone` 是一个用户提供的库，用于检测用户代理是否不支持 SameSite `None`。</span><span class="sxs-lookup"><span data-stu-id="d23e5-140">In the preceding sample, `MyUserAgentDetectionLib.DisallowsSameSiteNone` is a user supplied library that detects if the user agent doesn't support SameSite `None`.</span></span> <span data-ttu-id="d23e5-141">下面的代码演示 `DisallowsSameSiteNone` 方法示例：</span><span class="sxs-lookup"><span data-stu-id="d23e5-141">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="d23e5-142">以下代码仅用于演示：</span><span class="sxs-lookup"><span data-stu-id="d23e5-142">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="d23e5-143">不应将其视为已完成。</span><span class="sxs-lookup"><span data-stu-id="d23e5-143">It should not be considered complete.</span></span>
> * <span data-ttu-id="d23e5-144">它不维护或不受支持。</span><span class="sxs-lookup"><span data-stu-id="d23e5-144">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="d23e5-145">测试应用的 SameSite 问题</span><span class="sxs-lookup"><span data-stu-id="d23e5-145">Test apps for SameSite problems</span></span>

<span data-ttu-id="d23e5-146">与远程站点（如通过第三方登录）交互的应用需要：</span><span class="sxs-lookup"><span data-stu-id="d23e5-146">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="d23e5-147">测试多个浏览器上的交互。</span><span class="sxs-lookup"><span data-stu-id="d23e5-147">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="d23e5-148">应用本文档中讨论的[浏览器检测和缓解措施](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-148">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="d23e5-149">使用可选择新的 SameSite 行为的客户端版本测试 web 应用。</span><span class="sxs-lookup"><span data-stu-id="d23e5-149">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="d23e5-150">Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。</span><span class="sxs-lookup"><span data-stu-id="d23e5-150">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="d23e5-151">应用应用 SameSite 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari）</span><span class="sxs-lookup"><span data-stu-id="d23e5-151">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="d23e5-152">有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-152">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="d23e5-153">用 Chrome 测试</span><span class="sxs-lookup"><span data-stu-id="d23e5-153">Test with Chrome</span></span>

<span data-ttu-id="d23e5-154">Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。</span><span class="sxs-lookup"><span data-stu-id="d23e5-154">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="d23e5-155">Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。</span><span class="sxs-lookup"><span data-stu-id="d23e5-155">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="d23e5-156">已启用适当测试标志的 Chrome 76 或77提供更准确的结果。</span><span class="sxs-lookup"><span data-stu-id="d23e5-156">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="d23e5-157">若要测试新的 SameSite 行为，请切换 `chrome://flags/#same-site-by-default-cookies`**启用**。</span><span class="sxs-lookup"><span data-stu-id="d23e5-157">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="d23e5-158">旧版本的 Chrome （75及更低版本）将报告为失败，并出现新的 `None` 设置。</span><span class="sxs-lookup"><span data-stu-id="d23e5-158">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="d23e5-159">请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-159">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="d23e5-160">Google 不会使旧版 chrome 版本可用。</span><span class="sxs-lookup"><span data-stu-id="d23e5-160">Google does not make older chrome versions available.</span></span> <span data-ttu-id="d23e5-161">遵循[下载 Chromium](https://www.chromium.org/getting-involved/download-chromium)中的说明来测试旧版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="d23e5-161">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="d23e5-162">不要从通过搜索旧版 chrome 提供的**链接下载 chrome** 。</span><span class="sxs-lookup"><span data-stu-id="d23e5-162">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="d23e5-163">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="d23e5-163">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="d23e5-164">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="d23e5-164">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="d23e5-165">用 Safari 测试</span><span class="sxs-lookup"><span data-stu-id="d23e5-165">Test with Safari</span></span>

<span data-ttu-id="d23e5-166">Safari 12 严格实现了之前的草稿，在新的 `None` 值在 cookie 中时失败。</span><span class="sxs-lookup"><span data-stu-id="d23e5-166">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="d23e5-167">通过本文档中[支持旧版浏览](#sob)器的浏览器检测代码，可避免 `None`。</span><span class="sxs-lookup"><span data-stu-id="d23e5-167">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="d23e5-168">使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。</span><span class="sxs-lookup"><span data-stu-id="d23e5-168">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="d23e5-169">问题取决于基础 OS 版本。</span><span class="sxs-lookup"><span data-stu-id="d23e5-169">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="d23e5-170">已知 OSX Mojave （10.14）和 iOS 12 与新的 SameSite 行为存在兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d23e5-170">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="d23e5-171">将 OS 升级到 OSX Catalina （10.15）或 iOS 13 会解决此问题。</span><span class="sxs-lookup"><span data-stu-id="d23e5-171">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="d23e5-172">Safari 当前没有用于测试新规范行为的选择标记。</span><span class="sxs-lookup"><span data-stu-id="d23e5-172">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="d23e5-173">用 Firefox 测试</span><span class="sxs-lookup"><span data-stu-id="d23e5-173">Test with Firefox</span></span>

<span data-ttu-id="d23e5-174">可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在 "`about:config`" 页面上选择 "`network.cookie.sameSite.laxByDefault`的功能标志。</span><span class="sxs-lookup"><span data-stu-id="d23e5-174">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="d23e5-175">以前版本的 Firefox 没有出现兼容性问题的报告。</span><span class="sxs-lookup"><span data-stu-id="d23e5-175">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="d23e5-176">通过 Edge 浏览器进行测试</span><span class="sxs-lookup"><span data-stu-id="d23e5-176">Test with Edge browser</span></span>

<span data-ttu-id="d23e5-177">Edge 支持旧的 SameSite 标准。</span><span class="sxs-lookup"><span data-stu-id="d23e5-177">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="d23e5-178">边缘版本44与新的标准没有任何已知的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d23e5-178">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="d23e5-179">带边缘测试（Chromium）</span><span class="sxs-lookup"><span data-stu-id="d23e5-179">Test with Edge (Chromium)</span></span>

<span data-ttu-id="d23e5-180">在 `edge://flags/#same-site-by-default-cookies` 页上设置 SameSite 标志。</span><span class="sxs-lookup"><span data-stu-id="d23e5-180">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="d23e5-181">未发现边缘 Chromium 的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d23e5-181">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="d23e5-182">用 Electron 进行测试</span><span class="sxs-lookup"><span data-stu-id="d23e5-182">Test with Electron</span></span>

<span data-ttu-id="d23e5-183">Electron 的版本包括较早版本的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="d23e5-183">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="d23e5-184">例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。</span><span class="sxs-lookup"><span data-stu-id="d23e5-184">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="d23e5-185">你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。</span><span class="sxs-lookup"><span data-stu-id="d23e5-185">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="d23e5-186">请参阅下一节中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d23e5-186">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d23e5-187">其他资源</span><span class="sxs-lookup"><span data-stu-id="d23e5-187">Additional resources</span></span>

* [<span data-ttu-id="d23e5-188">Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置</span><span class="sxs-lookup"><span data-stu-id="d23e5-188">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="d23e5-189">SameSite cookie 说明</span><span class="sxs-lookup"><span data-stu-id="d23e5-189">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
