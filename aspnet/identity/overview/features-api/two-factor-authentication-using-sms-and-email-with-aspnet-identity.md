---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: 使用 SMS 和电子邮件的双因素身份验证与 ASP.NET Identity ASP.NET 4。x
author: HaoK
description: 本教程将演示如何使用 SMS 和电子邮件设置双因素身份验证（2FA）。 本文由 Rick Anderson （@RickAndMSFT）、Pr 。
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 5f5218ca6c65ed3a2cd39d4e100349efa35d14cd
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115099"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>使用 SMS 和电子邮件的双因素身份验证 ASP.NET Identity

作者： [Hao Kung](https://github.com/HaoK)， [Pranav Rastogi 撰写](https://github.com/rustd)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Suhas Joshi](https://github.com/suhasj)

> 本教程将演示如何使用 SMS 和电子邮件设置双因素身份验证（2FA）。
> 
> 本文是由 Rick Anderson （[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)）、Pranav rastogi 撰写（[@rustd](https://twitter.com/rustd)）、Hao Kung 和 Suhas Joshi 编写的。 NuGet 示例主要由 Hao Kung 编写。

本主题涵盖以下内容：

- [构建标识示例](#build)
- [设置 SMS 以实现双重身份验证](#SMS)
- [启用双因素身份验证](#enable2)
- [如何注册双因素身份验证提供程序](#reg)
- [合并社会和本地登录帐户](#combine)
- [防止暴力破解攻击](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>构建标识示例

在本部分中，你将使用 NuGet 下载我们将使用的示例。 首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。

> [!NOTE]
> 警告：若要完成本教程，您必须安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) 。

1. 创建新的***空***ASP.NET Web 项目。
2. 在 "程序包管理器控制台" 中，输入以下命令：  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   在本教程中，我们将使用[SendGrid](http://sendgrid.com/)发送电子邮件和[Twilio](https://www.twilio.com/)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms 短信。 `Identity.Samples` 包将安装要使用的代码。
3. 将[项目设置为使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. *可选*：按照 "我的[电子邮件确认" 教程](account-confirmation-and-password-recovery-with-aspnet-identity.md)中的说明挂钩 SendGrid，然后运行该应用程序并注册电子邮件帐户。
5. *可选：* 从示例中删除演示电子邮件链接确认代码（帐户控制器中的 `ViewBag.Link` 代码。 请参阅 `DisplayEmail` 和 `ForgotPasswordConfirmation` 操作方法和 razor 视图）。
6. *可选：* 从 "管理" 和 "帐户" 控制器以及*Views\Account\VerifyCode.cshtml*和*Views\Manage\VerifyPhoneNumber.cshtml* razor 视图中删除 `ViewBag.Status` 代码。 或者，你可以保留 `ViewBag.Status` 显示来测试此应用在本地的工作方式，而无需挂接和发送电子邮件和短信。

> [!NOTE]
> 警告：如果更改此示例中的任何安全设置，则生产应用将需要进行安全审核，显式调用所做的更改。

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a>设置 SMS 以实现双重身份验证

本教程提供了使用 Twilio 或 ASPSMS 的说明，但你可以使用任何其他 SMS 提供程序。

1. **使用 SMS 提供程序创建用户帐户**  
  
   创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。
2. **安装其他包或添加服务引用**  
  
   Twilio  
   在 "程序包管理器控制台" 中，输入以下命令：  
    `Install-Package Twilio`  
  
   ASPSMS:  
   需要添加以下服务引用：  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   地址:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   命名空间:  
    `ASPSMSX2`
3. **了解 SMS 提供程序用户凭据**  
  
   Twilio  
   在 Twilio 帐户的 "**仪表板**" 选项卡中，复制 "**帐户 SID** " 和 "**身份验证令牌**"。  
  
   ASPSMS:  
   从帐户设置中，导航到**用户密钥**，并将其与自定义**密码**一起复制。  
  
   稍后我们将这些值存储在变量 `SMSAccountIdentification` 和 `SMSAccountPassword` 中。
4. **指定 SenderID/发起方**  
  
   Twilio  
   从 "**数字**" 选项卡中，复制 Twilio 的电话号码。  
  
   ASPSMS:  
   在 "**解锁**工作项" 菜单中，解锁一个或多个发信方，或选择一个字母数字发信方（并非所有网络都支持）。  
  
   稍后我们将此值存储在变量 `SMSAccountFrom` 中。
5. **将 SMS 提供程序凭据传输到应用中**  
  
   向应用程序提供凭据和发件人电话号码：

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > 安全性-永远不要将敏感数据存储在源代码中。 帐户和凭据将添加到上面的代码中，以使示例简单。 请参阅吴建 Atten 的 [ASP.NET MVC：保留](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)的源代码管理的专用设置。
6. **将数据传输到 SMS 提供程序**  
  
   在*应用\_Start\IdentityConfig.cs*文件中配置 `SmsService` 类。  
  
   根据所使用的 SMS 提供程序，激活 " **Twilio** " 或 " **ASPSMS** " 部分： 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. 运行该应用，然后用之前注册的帐户登录。
8. 单击您的 "用户 ID"，在 `Manage` 控制器中激活 `Index` 操作方法。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. 单击“添加”。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. 几秒钟后，会收到一条包含验证码的短信。 输入并按 "**提交**"。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. "管理" 视图显示已添加的电话号码。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>检查代码

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

`Manage` 控制器中的 `Index` 操作方法基于之前的操作设置状态消息，并提供链接来更改本地密码或添加本地帐户。 `Index` 方法还显示状态或你的2FA 电话号码、外部登录名、启用2FA，并记住此浏览器的2FA 方法（稍后将进行介绍）。 单击标题栏中的用户 ID （电子邮件）不会传递消息。 单击**电话号码：删除**链接将 `Message=RemovePhoneSuccess` 作为查询字符串。  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber` 操作方法会显示一个对话框，用于输入可接收短信消息的电话号码。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

单击 "**发送验证码**" 按钮会将电话号码发送到 HTTP POST `AddPhoneNumber` 操作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync` 方法将生成在 SMS 消息中设置的安全令牌。 如果已配置 SMS 服务，则会将令牌作为字符串发送 &quot;你的安全代码是 &lt;令牌&gt;&quot;。 要以异步方式调用 `SmsService.SendAsync` 方法，然后将应用重定向到 `VerifyPhoneNumber` 操作方法（显示以下对话框），您可以在其中输入验证代码。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

输入代码并单击 "提交" 后，代码会发布到 HTTP POST `VerifyPhoneNumber` 操作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync` 方法检查已发布的安全代码。 如果代码正确，则会将电话号码添加到 `AspNetUsers` 表的 `PhoneNumber` 字段。 如果调用成功，则调用 `SignInAsync` 方法：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent` 参数设置是否在多个请求之间保留身份验证会话。

更改安全配置文件时，会生成新的安全戳，并将其存储在*AspNetUsers*表的 `SecurityStamp` 字段中。 请注意，"`SecurityStamp`" 字段不同于 "安全" cookie。 安全 cookie 不会存储在 `AspNetUsers` 表中（或标识 DB 中的任何其他位置）。 安全 cookie 令牌使用[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)自签名，并使用 `UserId, SecurityStamp` 和过期时间信息创建。

Cookie 中间件检查每个请求的 cookie。 `Startup` 类中的 `SecurityStampValidator` 方法将按 `validateInterval`指定的方式，定期访问数据库并检查安全标记。 这种情况仅每30分钟发生一次（在我们的示例中），除非你更改安全配置文件。 选择了30分钟间隔，以最大程度地减少对数据库的行程。

对安全配置文件进行任何更改时，需要调用 `SignInAsync` 方法。 当安全配置文件更改时，数据库将更新 `SecurityStamp` 字段，而不调用 `SignInAsync` 方法，*只*需在 OWIN 管道到达数据库（`validateInterval`）时才会保持登录状态。 可以通过将 `SignInAsync` 方法更改为立即返回，并将 cookie `validateInterval` 属性设置为30分钟到5秒，来对此进行测试：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

在上述代码更改的情况下，你可以更改安全配置文件（例如，通过更改**启用了两个因素**的状态），在 `SecurityStampValidator.OnValidateIdentity` 方法失败时，将在5秒后注销。 删除 `SignInAsync` 方法中的返回行，使另一个安全配置文件发生更改，并且不会被注销。`SignInAsync` 方法会生成新的安全 cookie。

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>启用双因素身份验证

在示例应用中，需要使用 UI 启用双因素身份验证（2FA）。 若要启用2FA，请在导航栏中单击你的用户 ID （电子邮件别名）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
单击 "启用 2FA"。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) 注销，然后重新登录。 如果已启用电子邮件（请参阅[上一个教程](account-confirmation-and-password-recovery-with-aspnet-identity.md)），可以为2FA 选择 SMS 或电子邮件。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) 此时会显示 "验证代码" 页，您可以在其中输入代码（通过短信或电子邮件）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) 单击 "**记住此浏览器**" 复选框会使你不需要使用2FA 登录到该计算机和浏览器。 如果启用2FA 并单击 "**记住"，此浏览器**将为你提供强大的2FA 防护，防止恶意用户尝试访问你的帐户，只要他们无权访问你的计算机。 你可以在你经常使用的任何专用计算机上执行此操作。 通过设置**记住此浏览器**，你可以从不经常使用的计算机获得2FA 的增强的安全性，并且你无需在自己的计算机上使用2FA。 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>如何注册双因素身份验证提供程序

创建新 MVC 项目时， *IdentityConfig.cs*文件包含以下代码来注册双因素身份验证提供程序：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>为2FA 添加电话号码

`Manage` 控制器中的 `AddPhoneNumber` 操作方法会生成一个安全令牌，并将其发送到你提供的电话号码。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

发送令牌后，它会重定向到 `VerifyPhoneNumber` 操作方法，你可以在该方法中输入代码，以便为2FA 注册 SMS。 在验证了电话号码之前，不会使用 SMS 2FA。

## <a name="enabling-2fa"></a>启用2FA

`EnableTFA` 操作方法启用2FA：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

请注意，必须调用 `SignInAsync`，因为 enable 2FA 是对安全配置文件的更改。 当启用2FA 时，用户将需要使用2FA 登录，并使用已注册的2FA 方法（示例中的 SMS 和电子邮件）。

可以添加更多的2FA 提供程序（如 QR 码生成器），也可以编写自己的提供程序（请参阅将[Google 身份验证器与 ASP.NET Identity 一起使用](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)）。

> [!NOTE]
> 2FA 代码是使用[基于时间的一次性密码算法](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)生成的，代码的有效期为6分钟。 如果输入代码所用的时间超过6分钟，则将收到无效的代码错误消息。

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>合并社会和本地登录帐户

可以通过单击电子邮件链接来合并本地帐户和社交帐户。 在下面的序列中 &quot;RickAndMSFT@gmail.com&quot; 最初创建为本地登录名，但你可以先将该帐户创建为社交日志，然后添加本地登录名。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

单击 "**管理**" 链接。 请注意与此帐户关联的0个外部（社交登录）。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

单击 "其他登录服务" 链接，并接受应用请求。 这两个帐户已合并，你将能够使用这两个帐户进行登录。 你可能希望用户在身份验证服务中的社交日志关闭或无法访问其社交帐户时添加本地帐户。

在下图中，Tom 是中的社交登录（可从 **外部登录中查看：1** 显示在页面上）。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

单击 "**选择密码**" 可添加与同一帐户关联的本地日志。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>防止暴力破解攻击

可以通过启用用户锁定来保护应用上的帐户免遭字典攻击。 `ApplicationUserManager Create` 方法中的以下代码将配置锁定：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

上述代码仅启用了双因素身份验证的锁定。 虽然你可以通过在帐户控制器的 `Login` 方法中将 `shouldLockout` 更改为 true 来启用登录名锁定，但建议你不要为登录名启用锁定，因为这会使帐户容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)登录攻击。 在示例代码中，对在 `ApplicationDbInitializer Seed` 方法中创建的管理员帐户禁用锁定：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>要求用户具有已验证的电子邮件帐户

以下代码要求用户先获得经过验证的电子邮件帐户，然后才能登录：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>提供对2FA 要求的检查方式

本地登录和社交日志均检查是否启用了2FA。 如果启用了2FA，则 `SignInManager` logon 方法返回 `SignInStatus.RequiresVerification`，并且用户将被重定向到 `SendCode` 操作方法，在该方法中，他们必须输入代码以按顺序完成日志。 如果用户在用户本地 cookie 上设置了 RememberMe，则 `SignInManager` 将返回 `SignInStatus.Success`，并且不需要通过2FA。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

下面的代码演示 `SendCode` 操作方法。 [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)是使用为用户启用的所有2FA 方法创建的。 [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)传递给[DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper，使用户可以选择2FA 方法（通常为电子邮件和短信）。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

用户发布2FA 方法后，将调用 `HTTP POST SendCode` 操作方法，`SignInManager` 发送2FA 代码，并将用户重定向到 `VerifyCode` 操作方法，用户可以在其中输入代码以完成登录。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA 锁定

虽然你可以在登录密码尝试失败时设置帐户锁定，但该方法会使你的登录容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)锁定。 建议仅将帐户锁定用于2FA。 创建 `ApplicationUserManager` 时，示例代码将 2FA `MaxFailedAccessAttemptsBeforeLockout` 锁定设置为5。 用户登录（通过本地帐户或社交帐户）后，每次在2FA 中尝试失败，并且如果达到最大尝试次数，则用户将被锁定5分钟（可以使用 `DefaultAccountLockoutTimeSpan`设置锁定超时时间）。

<a id="addRes"></a>

## <a name="additional-resources"></a>其他资源

- [ASP.NET Identity 推荐的资源](../getting-started/aspnet-identity-recommended-resources.md)标识博客、视频、教程和优秀链接的完整列表。
- [带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)还演示如何将配置文件信息添加到用户表中。
- [ASP.NET MVC 和标识2.0：了解 John Atten 的基础知识](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)。
- [帐户确认和密码恢复与 ASP.NET Identity](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET 标识简介](../getting-started/introduction-to-aspnet-identity.md)
- [公告 ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) By Pranav RASTOGI 撰写的 RTM。
- [ASP.NET Identity 2.0：设置帐户验证和由 John Atten](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 的双重身份验证。
