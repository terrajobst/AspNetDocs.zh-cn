---
title: ASP.NET 4.7.2 VB MVC 的 SameSite cookie 示例
author: blowdart
description: ASP.NET 4.7.2 VB MVC 的 SameSite cookie 示例
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458407"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a>ASP.NET 4.7.2 VB MVC 的 SameSite cookie 示例

.NET Framework 4.7 内置了对[SameSite](https://www.owasp.org/index.php/SameSite)属性的支持，但它符合原始标准。
修补后的行为更改了 `SameSite.None` 的含义，以使用 `None`值发出属性，而不是根本就发出值。 如果要不发出该值，可以将 cookie 的 `SameSite` 属性设置为-1。

## <a name="writing-the-samesite-attribute"></a><a name="sampleCode"></a>编写 SameSite 属性

下面是如何在 cookie 上编写 SameSite 属性的示例;

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

会话状态的默认 sameSite 属性在会话设置的 "cookieSameSite" 参数中设置 `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>MVC 身份验证

基于 OWIN MVC cookie 的身份验证使用 cookie 管理器来启用 cookie 属性的更改。 [SameSiteCookieManager](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb)是此类的一个实现，你可以将其复制到你自己的项目中。 

必须确保 Owin 组件已升级到版本4.1.0 或更高版本。 检查 `packages.config` 文件，以确保所有版本号都匹配，例如。

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

身份验证组件必须配置为使用启动类中的 CookieManager;

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

Cookie 管理器必须在支持它的*每个*组件上设置，其中包括 CookieAuthentication 和 OpenIdConnectAuthentication。

SystemWebCookieManager 用于避免响应 cookie 集成的[已知问题](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)。

### <a name="running-the-sample"></a>运行示例

如果运行示例项目，请在初始页面上加载浏览器调试器，并使用它查看站点的 cookie 集合。
若要在 Microsoft Edge 和 Chrome 中进行此操作，请按 `F12` 选择 "`Application`" 选项卡，然后单击 "`Storage`" 部分中 "`Cookies`" 选项下的 "站点 URL"。

![浏览器调试器 Cookie 列表](sample/img/BrowserDebugger.png)

您可以从上图中看到，当您单击 "创建 SameSite Cookie" 按钮的 SameSite 属性值为 `Lax`，与在[示例代码](#sampleCode)中设置的值匹配时，示例创建的 cookie 就会看到该示例创建的 cookie。

## <a name="intercepting-cookies-you-do-not-control"></a><a name="interception"></a>拦截不控制的 cookie

.NET 4.5.2 引入了新的事件，用于截获标头的写入 `Response.AddOnSendingHeaders`。 这可用于在 cookie 返回到客户端计算机之前截获 cookie。 在示例中，我们将事件绑定到静态方法，该方法检查浏览器是否支持新的 sameSite 更改，如果未设置，则将 cookie 更改为不发出 `None` 属性。

请参阅[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) ，以[获取有关如何](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb)处理事件的示例，以及如何调整 cookie `sameSite` 属性（可将其复制到自己的代码中）。

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

您可以通过大致相同的方式更改特定的已命名 cookie 行为;下面的示例将 `Lax` 的默认身份验证 cookie 调整为支持 `None` 值的浏览器 `None`，或删除不支持 `None`的浏览器上的 sameSite 属性。

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

## <a name="more-information"></a>更多信息
 
[Chrome 更新](https://www.chromium.org/updates/same-site)

[OWIN SameSite 文档](/aspnet/samesite/owin-samesite)

[ASP.NET 文档](/aspnet/samesite/system-web-samesite)

[.NET SameSite 修补程序](/aspnet/samesite/kbs-samesite)