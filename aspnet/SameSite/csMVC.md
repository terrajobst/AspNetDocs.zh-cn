---
title: SameSite cookie 示例 ASP.NET 4.7.2 C# MVC
author: blowdart
description: SameSite cookie 示例 ASP.NET 4.7.2 C# MVC
ms.author: riande
ms.date: 2/15/2019
uid: samesite/csMVC
ms.openlocfilehash: dcbd0bee009669fb747d74e6ccef07fbae70a236
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438200"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-mvc"></a><span data-ttu-id="ef184-103">SameSite cookie 示例 ASP.NET 4.7.2 C# MVC</span><span class="sxs-lookup"><span data-stu-id="ef184-103">SameSite cookie sample for ASP.NET 4.7.2 C# MVC</span></span>

<span data-ttu-id="ef184-104">.NET Framework 4.7 内置了对[SameSite](https://www.owasp.org/index.php/SameSite)属性的支持，但它符合原始标准。</span><span class="sxs-lookup"><span data-stu-id="ef184-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="ef184-105">修补后的行为更改了 `SameSite.None` 的含义，以使用 `None`值发出属性，而不是根本就发出值。</span><span class="sxs-lookup"><span data-stu-id="ef184-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="ef184-106">如果要不发出该值，可以将 cookie 的 `SameSite` 属性设置为-1。</span><span class="sxs-lookup"><span data-stu-id="ef184-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="ef184-107">编写 SameSite 属性</span><span class="sxs-lookup"><span data-stu-id="ef184-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="ef184-108">下面是如何在 cookie 上编写 SameSite 属性的示例;</span><span class="sxs-lookup"><span data-stu-id="ef184-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookieSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for Same
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="ef184-109">会话状态的默认 sameSite 属性在会话设置的 "cookieSameSite" 参数中设置 `web.config`</span><span class="sxs-lookup"><span data-stu-id="ef184-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="ef184-110">MVC 身份验证</span><span class="sxs-lookup"><span data-stu-id="ef184-110">MVC Authentication</span></span>

<span data-ttu-id="ef184-111">基于 OWIN MVC cookie 的身份验证使用 cookie 管理器来启用 cookie 属性的更改。</span><span class="sxs-lookup"><span data-stu-id="ef184-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="ef184-112">[SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs)是此类的一个实现，你可以将其复制到你自己的项目中。</span><span class="sxs-lookup"><span data-stu-id="ef184-112">The [SameSiteCookieManager.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieManager.cs) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="ef184-113">必须确保 Owin 组件已升级到版本4.1.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ef184-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="ef184-114">检查 `packages.config` 文件，以确保所有版本号都匹配，例如。</span><span class="sxs-lookup"><span data-stu-id="ef184-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="ef184-115">然后，必须将身份验证组件配置为使用 startup 类中的 CookieManager;</span><span class="sxs-lookup"><span data-stu-id="ef184-115">The authentication components must then be configured to use the CookieManager in your startup class;</span></span>

```c#
public void Configuration(IAppBuilder app)
{
    app.UseCookieAuthentication(new CookieAuthenticationOptions
    {
        CookieSameSite = SameSiteMode.None,
        CookieHttpOnly = true,
        CookieSecure = CookieSecureOption.Always,
        CookieManager = new SameSiteCookieManager(new SystemWebCookieManager())
    });
}
```

<span data-ttu-id="ef184-116">Cookie 管理器必须在支持它的*每个*组件上设置，其中包括 CookieAuthentication 和 OpenIdConnectAuthentication。</span><span class="sxs-lookup"><span data-stu-id="ef184-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="ef184-117">SystemWebCookieManager 用于避免响应 cookie 集成的[已知问题](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)。</span><span class="sxs-lookup"><span data-stu-id="ef184-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="ef184-118">运行示例</span><span class="sxs-lookup"><span data-stu-id="ef184-118">Running the sample</span></span>

<span data-ttu-id="ef184-119">如果运行示例项目，请在初始页面上加载浏览器调试器，并使用它查看站点的 cookie 集合。</span><span class="sxs-lookup"><span data-stu-id="ef184-119">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="ef184-120">若要在 Edge 和 Chrome 中进行此操作，请按 `F12` 选择 "`Application`" 选项卡，然后单击 "`Storage`" 部分中 "`Cookies`" 选项下的 "站点 URL"。</span><span class="sxs-lookup"><span data-stu-id="ef184-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![浏览器调试器 Cookie 列表](sample/img/BrowserDebugger.png)

<span data-ttu-id="ef184-122">你可以从上图中看到，当你单击 "创建 Cookie" 按钮的 SameSite 属性值为 `Lax`（与[示例代码](#sampleCode)中设置的值匹配）时，该示例所创建的 cookie 就会看到。</span><span class="sxs-lookup"><span data-stu-id="ef184-122">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="ef184-123">拦截不控制的 cookie</span><span class="sxs-lookup"><span data-stu-id="ef184-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="ef184-124">.NET 4.5.2 引入了新的事件，用于截获标头的写入 `Response.AddOnSendingHeaders`。</span><span class="sxs-lookup"><span data-stu-id="ef184-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="ef184-125">这可用于在 cookie 返回到客户端计算机之前截获 cookie。</span><span class="sxs-lookup"><span data-stu-id="ef184-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="ef184-126">在示例中，我们将事件绑定到静态方法，该方法检查浏览器是否支持新的 sameSite 更改，如果未设置，则将 cookie 更改为不发出 `None` 属性。</span><span class="sxs-lookup"><span data-stu-id="ef184-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="ef184-127">有关挂钩事件的示例，请参阅[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) ，有关处理事件的示例，请参阅[SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) ，并调整 cookie `sameSite` 属性（可将其复制到自己的代码中）。</span><span class="sxs-lookup"><span data-stu-id="ef184-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpMVC5/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="ef184-128">您可以通过大致相同的方式更改特定的已命名 cookie 行为;下面的示例将 `Lax` 的默认身份验证 cookie 调整为支持 `None` 值的浏览器 `None`，或删除不支持 `None`的浏览器上的 sameSite 属性。</span><span class="sxs-lookup"><span data-stu-id="ef184-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

### <a name="more-information"></a><span data-ttu-id="ef184-129">详细信息</span><span class="sxs-lookup"><span data-stu-id="ef184-129">More Information</span></span>
 
[<span data-ttu-id="ef184-130">Chrome 更新</span><span class="sxs-lookup"><span data-stu-id="ef184-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="ef184-131">OWIN SameSite 文档</span><span class="sxs-lookup"><span data-stu-id="ef184-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="ef184-132">ASP.NET 文档</span><span class="sxs-lookup"><span data-stu-id="ef184-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="ef184-133">.NET SameSite 修补程序</span><span class="sxs-lookup"><span data-stu-id="ef184-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)