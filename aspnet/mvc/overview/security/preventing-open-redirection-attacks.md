---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 阻止打开重定向攻击C#（） |Microsoft Docs
author: jongalloway
description: 本教程介绍如何在 ASP.NET MVC 应用程序中阻止开放重定向攻击。 本教程将讨论已进行的更改 。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432584"
---
# <a name="preventing-open-redirection-attacks-c"></a>阻止打开重定向攻击 (C#)

作者： [Jon Galloway](https://github.com/jongalloway)

> 本教程介绍如何在 ASP.NET MVC 应用程序中阻止开放重定向攻击。 本教程讨论了在 ASP.NET MVC 3 的 AccountController 中所做的更改，并演示了如何在现有的 ASP.NET MVC 1.0 和2应用程序中应用这些更改。

## <a name="what-is-an-open-redirection-attack"></a>什么是开放重定向攻击？

重定向到通过请求（如 querystring 或窗体数据）指定的 URL 的任何 web 应用程序可能会被篡改，以将用户重定向到外部恶意 URL。 这种篡改称为 "开放重定向攻击"。

每当应用程序逻辑重定向到指定的 URL 时，必须验证重定向 URL 是否未被篡改。 用于 ASP.NET MVC 1.0 和 ASP.NET MVC 2 的默认 AccountController 中使用的登录名容易受到开放重定向攻击。 幸运的是，可以轻松地更新现有应用程序，以使用 ASP.NET MVC 3 预览版中的更正。

若要了解该漏洞，请查看登录重定向在默认的 ASP.NET MVC 2 Web 应用程序项目中的工作原理。 在此应用程序中，尝试访问具有 [授权] 属性的控制器操作会将未经授权的用户重定向到/Account/LogOn 视图。 这种重定向到/Account/LogOn 的将包含一个 returnUrl 查询字符串参数，以便用户在成功登录后可以返回到最初请求的 URL。

在下面的屏幕截图中，我们可以看到，如果未登录，尝试访问/Account/ChangePassword 视图会导致重定向到/Account/LogOn？ReturnUrl =% 2fAccount% 2fChangePassword% 2f。

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**图 01**：具有打开的重定向的登录页

由于未对 ReturnUrl querystring 参数进行验证，攻击者可以将其修改为将任何 URL 地址注入到参数中，以执行开放重定向攻击。 为了演示这一点，我们可以将 ReturnUrl 参数修改为[http://bing.com](http://bing.com)，因此生成的登录 URL 将为/Account/LogOn？ReturnUrl =<http://www.bing.com/>。 成功登录到站点后，会重定向到[http://bing.com](http://bing.com)。 由于此重定向未经过验证，因此它可能会指向尝试欺骗用户的恶意网站。

### <a name="a-more-complex-open-redirection-attack"></a>更复杂的打开重定向攻击

由于攻击者知道我们尝试登录到特定网站，从而使我们容易遭受[网络钓鱼攻击](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)，因此打开重定向攻击尤其危险。 例如，攻击者可能会向网站用户发送恶意电子邮件以尝试捕获其密码。 让我们看一下如何在 NerdDinner 站点上工作。 （请注意，实时 NerdDinner 站点已更新，以防止开放重定向攻击。）

首先，攻击者向我们发送 NerdDinner 上的登录页面的链接，该链接包含重定向到其伪造的页面：

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

请注意，返回 URL 指向 nerddiner.com，这在单词晚餐中缺少 "n"。 在此示例中，这是攻击者控制的域。 访问上述链接时，将转到合法的 NerdDinner.com 登录页。

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**图 02**：包含打开的重定向的 NerdDinner 登录页

当我们正确登录后，ASP.NET MVC AccountController 的登录操作会将我们重定向到 returnUrl querystring 参数中指定的 URL。 在这种情况下，它是攻击者输入的 URL， [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)。 除非我们非常密切，否则我们很可能不会注意到这一点，特别是因为攻击者小心确保其伪造的页面看起来与合法登录页面完全相同。 此登录页面包含一个错误消息，该错误消息要求再次登录。 笨拙我们，我们必须键入错误的密码。

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**图 03**：伪造的 NerdDinner 登录屏幕

重新键入用户名和密码时，伪造的登录页面会保存信息，并将信息发送回合法的 NerdDinner.com 站点。 此时，NerdDinner.com 站点已经过身份验证，因此伪造的登录页面可以直接重定向到该页面。 最终的结果是攻击者提供了用户名和密码，并且我们不知道我们已向其提供了用户名和密码。

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>查看 AccountController LogOn 操作中有漏洞的代码

ASP.NET MVC 2 应用程序中登录操作的代码如下所示。 请注意，在成功登录后，控制器返回重定向到 returnUrl。 你可以看到，不会对 returnUrl 参数执行任何验证。

**列表1– ASP.NET 中的 MVC 2 登录操作 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

现在，让我们看看 ASP.NET MVC 3 登录操作的更改。 已通过在名为 `IsLocalUrl()`的 System.web helper 类中调用新方法，将此代码更改为验证 returnUrl 参数。

**列表2– ASP.NET 中的 MVC 3 登录操作 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

这已更改为通过调用 System.web helper 类中的新方法来验证 return URL 参数，`IsLocalUrl()`。

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>保护 ASP.NET MVC 1.0 和 MVC 2 应用程序

通过添加 IsLocalUrl （） helper 方法并更新登录操作来验证 returnUrl 参数，我们可以利用现有 ASP.NET MVC 1.0 和2应用程序中的 ASP.NET MVC 3 更改。

UrlHelper IsLocalUrl （）方法实际上只是调用了 System.web 中的一个方法，因为 ASP.NET 网页应用程序也使用此验证。

**列表 3-ASP.NET MVC 3 UrlHelper 中的 IsLocalUrl （）方法 `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost 方法包含实际的验证逻辑，如列表4中所示。

**从 System.web RequestExtensions 类中列出4– IsUrlLocalToHost （）方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

在我们的 ASP.NET MVC 1.0 或2应用程序中，我们会将 IsLocalUrl （）方法添加到 AccountController，但建议在可能的情况下将其添加到单独的帮助器类。 我们将对 IsLocalUrl （）的 ASP.NET MVC 3 版本进行两处小的更改，使其在 AccountController 内部工作。 首先，我们会将其从公共方法更改为私有方法，因为控制器中的公共方法可以作为控制器操作访问。 其次，我们将修改对应用程序主机检查 URL 主机的调用。 该调用会使用 UrlHelper 类中的本地 RequestContext 字段。 而不使用此。RequestContext，我们将使用这种情况。请求。 下面的代码演示了修改后的 IsLocalUrl （）方法，以用于 ASP.NET MVC 1.0 和2应用程序中的控制器类。

**列出5– IsLocalUrl （）方法，该方法经过修改后可用于 MVC 控制器类**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

现在，IsLocalUrl （）方法已准备就绪，可以从登录操作调用它来验证 returnUrl 参数，如以下代码所示。

**列出6–验证 returnUrl 参数的已更新登录方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

现在，我们可以尝试使用外部返回 URL 登录，来测试打开的重定向攻击。 我们使用/Account/LogOn？ReturnUrl = 再次<http://www.bing.com/>。

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**图 04**：测试更新的登录操作

成功登录后，将重定向到 Home/Index 控制器操作，而不是外部 URL。

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**图 05**：打开重定向攻击失效

## <a name="summary"></a>摘要

当在应用程序的 URL 中将重定向 Url 作为参数传递时，可能会出现 "打开重定向攻击"。 ASP.NET MVC 3 模板包含用于防范开放重定向攻击的代码。 可以将此代码添加到 ASP.NET MVC 1.0 和2应用程序的一些修改。 若要防止在登录 ASP.NET 1.0 和2应用程序时出现的重定向攻击，请添加 IsLocalUrl （）方法并验证登录操作中的 returnUrl 参数。
