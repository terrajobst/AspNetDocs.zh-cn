---
title: SameSite cookie sample for ASP.NET 4.7.2 VB WebForms
author: blowdart
description: SameSite cookie sample for ASP.NET 4.7.2 VB WebForms
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbWF
ms.openlocfilehash: 8979edecc5acf7dac81b9f53d31af00389f4727c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458383"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-webforms"></a><span data-ttu-id="4af1b-103">SameSite cookie sample for ASP.NET 4.7.2 VB WebForms</span><span class="sxs-lookup"><span data-stu-id="4af1b-103">SameSite cookie sample for ASP.NET 4.7.2 VB WebForms</span></span>
<span data-ttu-id="4af1b-104">.NET Framework 4.7 内置了对[SameSite](https://www.owasp.org/index.php/SameSite)属性的支持，但它符合原始标准。</span><span class="sxs-lookup"><span data-stu-id="4af1b-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="4af1b-105">修补后的行为更改了 `SameSite.None` 的含义，以使用 `None`值发出属性，而不是根本就发出值。</span><span class="sxs-lookup"><span data-stu-id="4af1b-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="4af1b-106">如果要不发出该值，可以将 cookie 的 `SameSite` 属性设置为-1。</span><span class="sxs-lookup"><span data-stu-id="4af1b-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="4af1b-107">编写 SameSite 属性</span><span class="sxs-lookup"><span data-stu-id="4af1b-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="4af1b-108">下面是如何在 cookie 上编写 SameSite 属性的示例;</span><span class="sxs-lookup"><span data-stu-id="4af1b-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="4af1b-109">Forms 身份验证 cookie 的默认 sameSite 属性在 `web.config` 中窗体身份验证设置的 `cookieSameSite` 参数中设置。</span><span class="sxs-lookup"><span data-stu-id="4af1b-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="4af1b-110">会话状态的默认 sameSite 属性还在会话设置的 "cookieSameSite" 参数中设置 `web.config`</span><span class="sxs-lookup"><span data-stu-id="4af1b-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="4af1b-111">.NET 11 2019 月版更新将窗体身份验证和会话 `lax` 的默认设置更改为最兼容的设置，但是，如果将页面嵌入到 iframe，则可能需要将此设置恢复为 "无"，然后添加下面所示的[拦截](#interception)代码以根据浏览器功能调整 `none` 行为。</span><span class="sxs-lookup"><span data-stu-id="4af1b-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="4af1b-112">运行示例</span><span class="sxs-lookup"><span data-stu-id="4af1b-112">Running the sample</span></span>

<span data-ttu-id="4af1b-113">如果运行示例项目，请在初始页面上加载浏览器调试器，并使用它查看站点的 cookie 集合。</span><span class="sxs-lookup"><span data-stu-id="4af1b-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="4af1b-114">若要在 Edge 和 Chrome 中进行此操作，请按 `F12` 选择 "`Application`" 选项卡，然后单击 "`Storage`" 部分中 "`Cookies`" 选项下的 "站点 URL"。</span><span class="sxs-lookup"><span data-stu-id="4af1b-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![浏览器调试器 Cookie 列表](sample/img/BrowserDebugger.png)

<span data-ttu-id="4af1b-116">你可以从上图中看到，当你单击 "创建 Cookie" 按钮的 SameSite 属性值为 `Lax`（与[示例代码](#sampleCode)中设置的值匹配）时，该示例所创建的 cookie 就会看到。</span><span class="sxs-lookup"><span data-stu-id="4af1b-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="4af1b-117">拦截不控制的 cookie</span><span class="sxs-lookup"><span data-stu-id="4af1b-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="4af1b-118">.NET 4.5.2 引入了新的事件，用于截获标头的写入 `Response.AddOnSendingHeaders`。</span><span class="sxs-lookup"><span data-stu-id="4af1b-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="4af1b-119">这可用于在 cookie 返回到客户端计算机之前截获 cookie。</span><span class="sxs-lookup"><span data-stu-id="4af1b-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="4af1b-120">在示例中，我们将事件绑定到静态方法，该方法检查浏览器是否支持新的 sameSite 更改，如果未设置，则将 cookie 更改为不发出 `None` 属性。</span><span class="sxs-lookup"><span data-stu-id="4af1b-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="4af1b-121">有关挂钩事件的示例，请参阅[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) ，并参阅[SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) ，了解如何处理事件并调整 cookie `sameSite` 特性。</span><span class="sxs-lookup"><span data-stu-id="4af1b-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>


```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

<span data-ttu-id="4af1b-122">您可以通过大致相同的方式更改特定的已命名 cookie 行为;下面的示例将 `Lax` 的默认身份验证 cookie 调整为支持 `None` 值的浏览器 `None`，或删除不支持 `None`的浏览器上的 sameSite 属性。</span><span class="sxs-lookup"><span data-stu-id="4af1b-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a><span data-ttu-id="4af1b-123">更多信息</span><span class="sxs-lookup"><span data-stu-id="4af1b-123">More Information</span></span>

[<span data-ttu-id="4af1b-124">Chrome 更新</span><span class="sxs-lookup"><span data-stu-id="4af1b-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="4af1b-125">ASP.NET 文档</span><span class="sxs-lookup"><span data-stu-id="4af1b-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="4af1b-126">.NET SameSite 修补程序</span><span class="sxs-lookup"><span data-stu-id="4af1b-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)