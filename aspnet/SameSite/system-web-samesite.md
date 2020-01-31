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
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="d08a9-103">在 ASP.NET 中使用 SameSite cookie</span><span class="sxs-lookup"><span data-stu-id="d08a9-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="d08a9-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d08a9-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d08a9-105">SameSite 是一种[IETF](https://ietf.org/about/)草案标准，旨在提供一些针对跨站点请求伪造（CSRF）攻击的防护。</span><span class="sxs-lookup"><span data-stu-id="d08a9-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="d08a9-106">最初在[2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)中起草草案标准版已在[2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)中更新。</span><span class="sxs-lookup"><span data-stu-id="d08a9-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="d08a9-107">更新的标准与以前的标准不是向后兼容，以下是最明显的区别：</span><span class="sxs-lookup"><span data-stu-id="d08a9-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="d08a9-108">默认情况下，不带 SameSite 标头的 cookie 被视为 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="d08a9-109">`SameSite=None` 必须用于允许跨站点 cookie。</span><span class="sxs-lookup"><span data-stu-id="d08a9-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="d08a9-110">断言 `SameSite=None` 的 cookie 也必须标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="d08a9-111">[2016 标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允许值 SameSite = None，导致某些实现将此类 Cookie 视为 SameSite = Strict。</span><span class="sxs-lookup"><span data-stu-id="d08a9-111">The value SameSite=None is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as SameSite=Strict.</span></span> <span data-ttu-id="d08a9-112">请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-112">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="d08a9-113">`SameSite=Lax` 设置适用于大多数应用程序 cookie。</span><span class="sxs-lookup"><span data-stu-id="d08a9-113">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="d08a9-114">某些形式的身份验证，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[ws-federation](https://auth0.com/docs/protocols/ws-fed)默认为基于 POST 的重定向。</span><span class="sxs-lookup"><span data-stu-id="d08a9-114">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="d08a9-115">基于后期的重定向会触发 SameSite 浏览器保护，因此，对这些组件禁用了 SameSite。</span><span class="sxs-lookup"><span data-stu-id="d08a9-115">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="d08a9-116">由于请求的流动方式不同，大多数[OAuth](https://oauth.net/)登录名不受影响。</span><span class="sxs-lookup"><span data-stu-id="d08a9-116">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="d08a9-117">使用 `iframe` 的应用程序可能会遇到 `SameSite=Lax` 或 `SameSite=Strict` cookie 的问题，因为 iframe 被视为跨站点方案。</span><span class="sxs-lookup"><span data-stu-id="d08a9-117">Applications that use `iframe` may experience issues with `SameSite=Lax` or `SameSite=Strict` cookies because iframes are treated as cross-site scenarios.</span></span>

<span data-ttu-id="d08a9-118">发出 cookie 的每个 ASP.NET 组件都需要确定 SameSite 是否适用。</span><span class="sxs-lookup"><span data-stu-id="d08a9-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="d08a9-119">在安装 2019 .Net SameSite 更新后，请参阅应用程序问题的[已知问题](#known)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="d08a9-120">在 ASP.NET 4.7.2 和4.8 中使用 SameSite</span><span class="sxs-lookup"><span data-stu-id="d08a9-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="d08a9-121">.Net 4.7.2 和4.8 支持 SameSite 的[2019 草案标准](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)，因为年12月2019更新发布。</span><span class="sxs-lookup"><span data-stu-id="d08a9-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="d08a9-122">开发人员可以使用[HttpCookie 属性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)以编程方式控制 SameSite 标头的值。</span><span class="sxs-lookup"><span data-stu-id="d08a9-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="d08a9-123">将 `SameSite` 属性设置为 `Strict`、`Lax`或 `None` 会导致这些值用 cookie 写入网络中。</span><span class="sxs-lookup"><span data-stu-id="d08a9-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="d08a9-124">将其设置为等于 `(SameSiteMode)(-1)` 指示网络上不应包含 cookie 的 SameSite 标头。</span><span class="sxs-lookup"><span data-stu-id="d08a9-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="d08a9-125">[HttpCookie 属性](/dotnet/api/system.web.httpcookie.secure)（或配置文件中的 "requireSSL"）可用于将 cookie 标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="d08a9-126">新 `HttpCookie` 实例将默认为 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="d08a9-127">可以在 `system.web/httpCookies` 配置节中重写这些默认值，其中字符串 `"Unspecified"` 是 `(SameSiteMode)(-1)`的友好仅配置语法：</span><span class="sxs-lookup"><span data-stu-id="d08a9-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="d08a9-128">ASP.Net 还为这些功能颁发了自己的四个特定 cookie：匿名身份验证、Forms 身份验证、会话状态和角色管理。</span><span class="sxs-lookup"><span data-stu-id="d08a9-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="d08a9-129">在运行时获取的这些 cookie 的实例可以使用 `SameSite` 和 `Secure` 属性进行操作，就像使用任何其他 HttpCookie 实例一样。</span><span class="sxs-lookup"><span data-stu-id="d08a9-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="d08a9-130">然而，由于 SameSite 标准的大杂烩出现，这四个功能 cookie 的配置选项不一致。</span><span class="sxs-lookup"><span data-stu-id="d08a9-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="d08a9-131">相关配置节和属性的默认值如下所示。</span><span class="sxs-lookup"><span data-stu-id="d08a9-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="d08a9-132">如果某个功能没有 `SameSite` 或 `Secure` 相关属性，则该功能将回退前面讨论的 `system.web/httpCookies` 部分中配置的默认值。</span><span class="sxs-lookup"><span data-stu-id="d08a9-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

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

<span data-ttu-id="d08a9-133">**注意**：目前仅可 `system.web/httpCookies@sameSite` "未指定"。</span><span class="sxs-lookup"><span data-stu-id="d08a9-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="d08a9-134">我们希望在以后的更新中，将类似语法添加到前面所示的 cookieSameSite 属性。</span><span class="sxs-lookup"><span data-stu-id="d08a9-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="d08a9-135">在代码中设置 `(SameSiteMode)(-1)` 仍适用于这些 cookie 的实例。 \*</span><span class="sxs-lookup"><span data-stu-id="d08a9-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="d08a9-136">历史记录和更改</span><span class="sxs-lookup"><span data-stu-id="d08a9-136">History and changes</span></span>

<span data-ttu-id="d08a9-137">SameSite 支持是在使用[2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)的 .net 4.7.2 中首次实现的。</span><span class="sxs-lookup"><span data-stu-id="d08a9-137">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="d08a9-138">2019年11月19日更新了 Windows 更新后的 .NET 4.7.2 + 2016 标准版和2019标准版。</span><span class="sxs-lookup"><span data-stu-id="d08a9-138">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="d08a9-139">其他版本的 Windows 即将推出其他更新。</span><span class="sxs-lookup"><span data-stu-id="d08a9-139">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="d08a9-140">有关更多信息，请参见<xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="d08a9-140">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="d08a9-141">SameSite 规范的2019草案：</span><span class="sxs-lookup"><span data-stu-id="d08a9-141">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="d08a9-142">**不**向后兼容2016草案。</span><span class="sxs-lookup"><span data-stu-id="d08a9-142">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="d08a9-143">有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-143">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="d08a9-144">指定默认情况下将 cookie 视为 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-144">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="d08a9-145">指定显式断言 `SameSite=None` 以便启用跨站点传递的 cookie 也应该标记为 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-145">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="d08a9-146">按照上面列出的 KB 中所述，发布的修补程序支持。</span><span class="sxs-lookup"><span data-stu-id="d08a9-146">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="d08a9-147">默认[情况下，计划](https://chromestatus.com/feature/5088147346030592)在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。</span><span class="sxs-lookup"><span data-stu-id="d08a9-147">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="d08a9-148">浏览器已开始在2019中移动到此标准。</span><span class="sxs-lookup"><span data-stu-id="d08a9-148">Browsers started moving to this standard in 2019.</span></span>

<a name="known"><a/>

## <a name="known-issues"></a><span data-ttu-id="d08a9-149">已知问题</span><span class="sxs-lookup"><span data-stu-id="d08a9-149">Known Issues</span></span>

<span data-ttu-id="d08a9-150">因为2016和2019草案规范不兼容，所以，11月 2019 .Net Framework 更新引入了一些可能会中断的更改。</span><span class="sxs-lookup"><span data-stu-id="d08a9-150">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="d08a9-151">会话状态和窗体身份验证 cookie 现在作为 `Lax` 写入到网络，而不是未指定。</span><span class="sxs-lookup"><span data-stu-id="d08a9-151">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="d08a9-152">大多数应用程序都适用于 `SameSite=Lax` cookie，在使用 `iframe` 的站点或应用程序中发布的应用程序可能会发现其会话状态或窗体授权 cookie 没有按预期方式使用。</span><span class="sxs-lookup"><span data-stu-id="d08a9-152">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="d08a9-153">若要解决此情况，请在前面所述的相应配置节中更改 `cookieSameSite` 值。</span><span class="sxs-lookup"><span data-stu-id="d08a9-153">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="d08a9-154">HttpCookies 在代码或配置中显式设置 `SameSite=None` 现在使用 cookie 写入该值，而以前省略了该值。</span><span class="sxs-lookup"><span data-stu-id="d08a9-154">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="d08a9-155">这可能会导致旧版浏览器出现一些仅支持2016草案标准的问题。</span><span class="sxs-lookup"><span data-stu-id="d08a9-155">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="d08a9-156">面向支持2019草案标准的浏览器 `SameSite=None` cookie 时，还应将其标记 `Secure` 或无法识别。</span><span class="sxs-lookup"><span data-stu-id="d08a9-156">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="d08a9-157">若要恢复为不写入 `SameSite=None`的2016行为，请使用 "应用设置" `aspnet:SupressSameSiteNone=true`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-157">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="d08a9-158">请注意，这将适用于应用中的所有 HttpCookies。</span><span class="sxs-lookup"><span data-stu-id="d08a9-158">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="d08a9-159">Azure App Service — SameSite cookie 处理</span><span class="sxs-lookup"><span data-stu-id="d08a9-159">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="d08a9-160">请参阅[Azure App Service-SameSite cookie 处理和 .NET Framework 4.7.2 修补程序](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)，以获取有关 Azure App Service 如何在 .net 4.7.2 apps 中配置 SameSite 行为的信息。</span><span class="sxs-lookup"><span data-stu-id="d08a9-160">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="d08a9-161">支持旧版浏览器</span><span class="sxs-lookup"><span data-stu-id="d08a9-161">Supporting older browsers</span></span>

<span data-ttu-id="d08a9-162">2016 SameSite 标准规定，未知值必须被视为 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="d08a9-162">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="d08a9-163">从支持 2016 SameSite 标准的旧版浏览器访问的应用可能会在收到值为 "`None`" 的 SameSite 属性时中断。</span><span class="sxs-lookup"><span data-stu-id="d08a9-163">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="d08a9-164">如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。</span><span class="sxs-lookup"><span data-stu-id="d08a9-164">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="d08a9-165">ASP.NET 不实现浏览器检测，因为用户代理值非常不稳定，并且经常更改。</span><span class="sxs-lookup"><span data-stu-id="d08a9-165">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="d08a9-166">可以在 <xref:HTTP.HttpCookie> 调用站点调用以下代码：</span><span class="sxs-lookup"><span data-stu-id="d08a9-166">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="d08a9-167">在前面的示例中，`MyUserAgentDetectionLib.DisallowsSameSiteNone` 是一个用户提供的库，用于检测用户代理是否不支持 SameSite `None`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-167">In the preceding sample, `MyUserAgentDetectionLib.DisallowsSameSiteNone` is a user supplied library that detects if the user agent doesn't support SameSite `None`.</span></span> <span data-ttu-id="d08a9-168">下面的代码演示 `DisallowsSameSiteNone` 方法示例：</span><span class="sxs-lookup"><span data-stu-id="d08a9-168">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="d08a9-169">以下代码仅用于演示：</span><span class="sxs-lookup"><span data-stu-id="d08a9-169">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="d08a9-170">不应将其视为已完成。</span><span class="sxs-lookup"><span data-stu-id="d08a9-170">It should not be considered complete.</span></span>
> * <span data-ttu-id="d08a9-171">它不维护或不受支持。</span><span class="sxs-lookup"><span data-stu-id="d08a9-171">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="d08a9-172">测试应用的 SameSite 问题</span><span class="sxs-lookup"><span data-stu-id="d08a9-172">Test apps for SameSite problems</span></span>

<span data-ttu-id="d08a9-173">与远程站点（如通过第三方登录）交互的应用需要：</span><span class="sxs-lookup"><span data-stu-id="d08a9-173">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="d08a9-174">测试多个浏览器上的交互。</span><span class="sxs-lookup"><span data-stu-id="d08a9-174">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="d08a9-175">应用本文档中讨论的[浏览器检测和缓解措施](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-175">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="d08a9-176">使用可选择新的 SameSite 行为的客户端版本测试 web 应用。</span><span class="sxs-lookup"><span data-stu-id="d08a9-176">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="d08a9-177">Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。</span><span class="sxs-lookup"><span data-stu-id="d08a9-177">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="d08a9-178">应用应用 SameSite 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari）</span><span class="sxs-lookup"><span data-stu-id="d08a9-178">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="d08a9-179">有关详细信息，请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-179">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="d08a9-180">用 Chrome 测试</span><span class="sxs-lookup"><span data-stu-id="d08a9-180">Test with Chrome</span></span>

<span data-ttu-id="d08a9-181">Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。</span><span class="sxs-lookup"><span data-stu-id="d08a9-181">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="d08a9-182">Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。</span><span class="sxs-lookup"><span data-stu-id="d08a9-182">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="d08a9-183">已启用适当测试标志的 Chrome 76 或77提供更准确的结果。</span><span class="sxs-lookup"><span data-stu-id="d08a9-183">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="d08a9-184">若要测试新的 SameSite 行为，请切换 `chrome://flags/#same-site-by-default-cookies`**启用**。</span><span class="sxs-lookup"><span data-stu-id="d08a9-184">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="d08a9-185">旧版本的 Chrome （75及更低版本）将报告为失败，并出现新的 `None` 设置。</span><span class="sxs-lookup"><span data-stu-id="d08a9-185">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="d08a9-186">请参阅本文档中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-186">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="d08a9-187">Google 不会使旧版 chrome 版本可用。</span><span class="sxs-lookup"><span data-stu-id="d08a9-187">Google does not make older chrome versions available.</span></span> <span data-ttu-id="d08a9-188">遵循[下载 Chromium](https://www.chromium.org/getting-involved/download-chromium)中的说明来测试旧版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="d08a9-188">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="d08a9-189">不要从通过搜索旧版 chrome 提供的**链接下载 chrome** 。</span><span class="sxs-lookup"><span data-stu-id="d08a9-189">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="d08a9-190">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="d08a9-190">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="d08a9-191">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="d08a9-191">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="d08a9-192">用 Safari 测试</span><span class="sxs-lookup"><span data-stu-id="d08a9-192">Test with Safari</span></span>

<span data-ttu-id="d08a9-193">Safari 12 严格实现了之前的草稿，在新的 `None` 值在 cookie 中时失败。</span><span class="sxs-lookup"><span data-stu-id="d08a9-193">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="d08a9-194">通过本文档中[支持旧版浏览](#sob)器的浏览器检测代码，可避免 `None`。</span><span class="sxs-lookup"><span data-stu-id="d08a9-194">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="d08a9-195">使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。</span><span class="sxs-lookup"><span data-stu-id="d08a9-195">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="d08a9-196">问题取决于基础 OS 版本。</span><span class="sxs-lookup"><span data-stu-id="d08a9-196">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="d08a9-197">已知 OSX Mojave （10.14）和 iOS 12 与新的 SameSite 行为存在兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d08a9-197">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="d08a9-198">将 OS 升级到 OSX Catalina （10.15）或 iOS 13 会解决此问题。</span><span class="sxs-lookup"><span data-stu-id="d08a9-198">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="d08a9-199">Safari 当前没有用于测试新规范行为的选择标记。</span><span class="sxs-lookup"><span data-stu-id="d08a9-199">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="d08a9-200">用 Firefox 测试</span><span class="sxs-lookup"><span data-stu-id="d08a9-200">Test with Firefox</span></span>

<span data-ttu-id="d08a9-201">可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在 "`about:config`" 页面上选择 "`network.cookie.sameSite.laxByDefault`的功能标志。</span><span class="sxs-lookup"><span data-stu-id="d08a9-201">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="d08a9-202">以前版本的 Firefox 没有出现兼容性问题的报告。</span><span class="sxs-lookup"><span data-stu-id="d08a9-202">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="d08a9-203">通过 Edge 浏览器进行测试</span><span class="sxs-lookup"><span data-stu-id="d08a9-203">Test with Edge browser</span></span>

<span data-ttu-id="d08a9-204">Edge 支持旧的 SameSite 标准。</span><span class="sxs-lookup"><span data-stu-id="d08a9-204">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="d08a9-205">边缘版本44与新的标准没有任何已知的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d08a9-205">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="d08a9-206">带边缘测试（Chromium）</span><span class="sxs-lookup"><span data-stu-id="d08a9-206">Test with Edge (Chromium)</span></span>

<span data-ttu-id="d08a9-207">在 `edge://flags/#same-site-by-default-cookies` 页上设置 SameSite 标志。</span><span class="sxs-lookup"><span data-stu-id="d08a9-207">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="d08a9-208">未发现边缘 Chromium 的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="d08a9-208">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="d08a9-209">用 Electron 进行测试</span><span class="sxs-lookup"><span data-stu-id="d08a9-209">Test with Electron</span></span>

<span data-ttu-id="d08a9-210">Electron 的版本包括较早版本的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="d08a9-210">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="d08a9-211">例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。</span><span class="sxs-lookup"><span data-stu-id="d08a9-211">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="d08a9-212">你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。</span><span class="sxs-lookup"><span data-stu-id="d08a9-212">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="d08a9-213">请参阅下一节中的[支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="d08a9-213">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d08a9-214">其他资源</span><span class="sxs-lookup"><span data-stu-id="d08a9-214">Additional resources</span></span>

* [<span data-ttu-id="d08a9-215">即将推出 SameSite Cookie 更改 ASP.NET 和 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d08a9-215">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="d08a9-216">Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置</span><span class="sxs-lookup"><span data-stu-id="d08a9-216">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="d08a9-217">SameSite cookie 说明</span><span class="sxs-lookup"><span data-stu-id="d08a9-217">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
