---
title: SameSite cookie sample for ASP.NET 4.7.2 C# WebForms
author: blowdart
description: SameSite cookie sample for ASP.NET 4.7.2 C# WebForms
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458419"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>SameSite cookie sample for ASP.NET 4.7.2 C# WebForms

.NET Framework 4.7 内置了对[SameSite](https://www.owasp.org/index.php/SameSite)属性的支持，但它符合原始标准。
修补后的行为更改了 `SameSite.None` 的含义，以使用 `None`值发出属性，而不是根本就发出值。 如果要不发出该值，可以将 cookie 的 `SameSite` 属性设置为-1。

## <a name="sampleCode"></a>编写 SameSite 属性

下面是如何在 cookie 上编写 SameSite 属性的示例;

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
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

Forms 身份验证 cookie 的默认 sameSite 属性在 `web.config` 中窗体身份验证设置的 `cookieSameSite` 参数中设置。 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

会话状态的默认 sameSite 属性还在会话设置的 "cookieSameSite" 参数中设置 `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

.NET 11 2019 月版更新将窗体身份验证和会话 `lax` 的默认设置更改为最兼容的设置，但是，如果将页面嵌入到 iframe，则可能需要将此设置恢复为 "无"，然后添加下面所示的[拦截](#interception)代码以根据浏览器功能调整 `none` 行为。

### <a name="running-the-sample"></a>运行示例

如果运行示例项目，请在初始页面上加载浏览器调试器，并使用它查看站点的 cookie 集合。
若要在 Edge 和 Chrome 中进行此操作，请按 `F12` 选择 "`Application`" 选项卡，然后单击 "`Storage`" 部分中 "`Cookies`" 选项下的 "站点 URL"。

![浏览器调试器 Cookie 列表](sample/img/BrowserDebugger.png)

你可以从上图中看到，当你单击 "创建 Cookie" 按钮的 SameSite 属性值为 `Lax`（与[示例代码](#sampleCode)中设置的值匹配）时，该示例所创建的 cookie 就会看到。

## <a name="interception"></a>拦截不控制的 cookie

.NET 4.5.2 引入了新的事件，用于截获标头的写入 `Response.AddOnSendingHeaders`。 这可用于在 cookie 返回到客户端计算机之前截获 cookie。 在示例中，我们将事件绑定到静态方法，该方法检查浏览器是否支持新的 sameSite 更改，如果未设置，则将 cookie 更改为不发出 `None` 属性。

有关挂钩事件的示例，请参阅[global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) ，并参阅[SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) ，了解如何处理事件并调整 cookie `sameSite` 特性。

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

您可以通过大致相同的方式更改特定的已命名 cookie 行为;下面的示例将 `Lax` 的默认身份验证 cookie 调整为支持 `None` 值的浏览器 `None`，或删除不支持 `None`的浏览器上的 sameSite 属性。

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

## <a name="more-information"></a>更多信息

[Chrome 更新](https://www.chromium.org/updates/same-site)

[ASP.NET 文档](/aspnet/samesite/system-web-samesite)

[.NET SameSite 修补程序](/aspnet/samesite/kbs-samesite)