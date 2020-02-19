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
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456733"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="dfe22-104">使用 SMS 和电子邮件的双因素身份验证 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="dfe22-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="dfe22-105">作者： [Hao Kung](https://github.com/HaoK)， [Pranav Rastogi 撰写](https://github.com/rustd)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="dfe22-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="dfe22-106">本教程将演示如何使用 SMS 和电子邮件设置双因素身份验证（2FA）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="dfe22-107">本文是由 Rick Anderson （[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)）、Pranav rastogi 撰写（[@rustd](https://twitter.com/rustd)）、Hao Kung 和 Suhas Joshi 编写的。</span><span class="sxs-lookup"><span data-stu-id="dfe22-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="dfe22-108">NuGet 示例主要由 Hao Kung 编写。</span><span class="sxs-lookup"><span data-stu-id="dfe22-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="dfe22-109">本主题涵盖以下内容：</span><span class="sxs-lookup"><span data-stu-id="dfe22-109">This topic covers the following:</span></span>

- [<span data-ttu-id="dfe22-110">构建标识示例</span><span class="sxs-lookup"><span data-stu-id="dfe22-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="dfe22-111">设置 SMS 以实现双重身份验证</span><span class="sxs-lookup"><span data-stu-id="dfe22-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="dfe22-112">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="dfe22-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="dfe22-113">如何注册双因素身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="dfe22-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="dfe22-114">合并社会和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="dfe22-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="dfe22-115">防止暴力破解攻击</span><span class="sxs-lookup"><span data-stu-id="dfe22-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="dfe22-116">构建标识示例</span><span class="sxs-lookup"><span data-stu-id="dfe22-116">Building the Identity sample</span></span>

<span data-ttu-id="dfe22-117">在本部分中，你将使用 NuGet 下载我们将使用的示例。</span><span class="sxs-lookup"><span data-stu-id="dfe22-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="dfe22-118">首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="dfe22-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="dfe22-119">安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="dfe22-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="dfe22-120">警告：若要完成本教程，您必须安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) 。</span><span class="sxs-lookup"><span data-stu-id="dfe22-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="dfe22-121">创建新的***空***ASP.NET Web 项目。</span><span class="sxs-lookup"><span data-stu-id="dfe22-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="dfe22-122">在 "程序包管理器控制台" 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="dfe22-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="dfe22-123">在本教程中，我们将使用[SendGrid](http://sendgrid.com/)发送电子邮件和[Twilio](https://www.twilio.com/)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms 短信。</span><span class="sxs-lookup"><span data-stu-id="dfe22-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="dfe22-124">`Identity.Samples` 包将安装要使用的代码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="dfe22-125">将[项目设置为使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="dfe22-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="dfe22-126">*可选*：按照 "我的[电子邮件确认" 教程](account-confirmation-and-password-recovery-with-aspnet-identity.md)中的说明挂钩 SendGrid，然后运行该应用程序并注册电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="dfe22-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="dfe22-127">*可选：* 从示例中删除演示电子邮件链接确认代码（帐户控制器中的 `ViewBag.Link` 代码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="dfe22-128">请参阅 `DisplayEmail` 和 `ForgotPasswordConfirmation` 操作方法和 razor 视图）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="dfe22-129">*可选：* 从 "管理" 和 "帐户" 控制器以及*Views\Account\VerifyCode.cshtml*和*Views\Manage\VerifyPhoneNumber.cshtml* razor 视图中删除 `ViewBag.Status` 代码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="dfe22-130">或者，你可以保留 `ViewBag.Status` 显示来测试此应用在本地的工作方式，而无需挂接和发送电子邮件和短信。</span><span class="sxs-lookup"><span data-stu-id="dfe22-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="dfe22-131">警告：如果更改此示例中的任何安全设置，则生产应用将需要进行安全审核，显式调用所做的更改。</span><span class="sxs-lookup"><span data-stu-id="dfe22-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="dfe22-132">设置 SMS 以实现双重身份验证</span><span class="sxs-lookup"><span data-stu-id="dfe22-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="dfe22-133">本教程提供了使用 Twilio 或 ASPSMS 的说明，但你可以使用任何其他 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="dfe22-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="dfe22-134">**使用 SMS 提供程序创建用户帐户**</span><span class="sxs-lookup"><span data-stu-id="dfe22-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="dfe22-135">创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。</span><span class="sxs-lookup"><span data-stu-id="dfe22-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="dfe22-136">**安装其他包或添加服务引用**</span><span class="sxs-lookup"><span data-stu-id="dfe22-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="dfe22-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="dfe22-137">Twilio:</span></span>  
   <span data-ttu-id="dfe22-138">在“包管理器控制台”中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="dfe22-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="dfe22-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="dfe22-139">ASPSMS:</span></span>  
   <span data-ttu-id="dfe22-140">需要添加以下服务引用：</span><span class="sxs-lookup"><span data-stu-id="dfe22-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="dfe22-141">地址:</span><span class="sxs-lookup"><span data-stu-id="dfe22-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="dfe22-142">命名空间:</span><span class="sxs-lookup"><span data-stu-id="dfe22-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="dfe22-143">**了解 SMS 提供程序用户凭据**</span><span class="sxs-lookup"><span data-stu-id="dfe22-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="dfe22-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="dfe22-144">Twilio:</span></span>  
   <span data-ttu-id="dfe22-145">在 Twilio 帐户的 "**仪表板**" 选项卡中，复制 "**帐户 SID** " 和 "**身份验证令牌**"。</span><span class="sxs-lookup"><span data-stu-id="dfe22-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="dfe22-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="dfe22-146">ASPSMS:</span></span>  
   <span data-ttu-id="dfe22-147">从帐户设置中，导航到**用户密钥**，并将其与自定义**密码**一起复制。</span><span class="sxs-lookup"><span data-stu-id="dfe22-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="dfe22-148">稍后我们将这些值存储在变量 `SMSAccountIdentification` 和 `SMSAccountPassword` 中。</span><span class="sxs-lookup"><span data-stu-id="dfe22-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="dfe22-149">**指定 SenderID/发起方**</span><span class="sxs-lookup"><span data-stu-id="dfe22-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="dfe22-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="dfe22-150">Twilio:</span></span>  
   <span data-ttu-id="dfe22-151">从 "**数字**" 选项卡中，复制 Twilio 的电话号码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="dfe22-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="dfe22-152">ASPSMS:</span></span>  
   <span data-ttu-id="dfe22-153">在 "**解锁**工作项" 菜单中，解锁一个或多个发信方，或选择一个字母数字发信方（并非所有网络都支持）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="dfe22-154">稍后我们将此值存储在变量 `SMSAccountFrom` 中。</span><span class="sxs-lookup"><span data-stu-id="dfe22-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="dfe22-155">**将 SMS 提供程序凭据传输到应用中**</span><span class="sxs-lookup"><span data-stu-id="dfe22-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="dfe22-156">向应用程序提供凭据和发件人电话号码：</span><span class="sxs-lookup"><span data-stu-id="dfe22-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="dfe22-157">安全性-永远不要将敏感数据存储在源代码中。</span><span class="sxs-lookup"><span data-stu-id="dfe22-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="dfe22-158">帐户和凭据将添加到上面的代码中，以使示例简单。</span><span class="sxs-lookup"><span data-stu-id="dfe22-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="dfe22-159">请参阅吴建 Atten 的 [ASP.NET MVC：保留](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)的源代码管理的专用设置。</span><span class="sxs-lookup"><span data-stu-id="dfe22-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="dfe22-160">**将数据传输到 SMS 提供程序**</span><span class="sxs-lookup"><span data-stu-id="dfe22-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="dfe22-161">在*应用\_Start\IdentityConfig.cs*文件中配置 `SmsService` 类。</span><span class="sxs-lookup"><span data-stu-id="dfe22-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="dfe22-162">根据所使用的 SMS 提供程序，激活 " **Twilio** " 或 " **ASPSMS** " 部分：</span><span class="sxs-lookup"><span data-stu-id="dfe22-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="dfe22-163">运行该应用，然后用之前注册的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="dfe22-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="dfe22-164">单击您的 "用户 ID"，在 `Manage` 控制器中激活 `Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="dfe22-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="dfe22-165">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="dfe22-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="dfe22-166">几秒钟后，会收到一条包含验证码的短信。</span><span class="sxs-lookup"><span data-stu-id="dfe22-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="dfe22-167">输入并按 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="dfe22-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="dfe22-168">"管理" 视图显示已添加的电话号码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="dfe22-169">检查代码</span><span class="sxs-lookup"><span data-stu-id="dfe22-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="dfe22-170">`Manage` 控制器中的 `Index` 操作方法基于之前的操作设置状态消息，并提供链接来更改本地密码或添加本地帐户。</span><span class="sxs-lookup"><span data-stu-id="dfe22-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="dfe22-171">`Index` 方法还显示状态或你的2FA 电话号码、外部登录名、启用2FA，并记住此浏览器的2FA 方法（稍后将进行介绍）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="dfe22-172">单击标题栏中的用户 ID （电子邮件）不会传递消息。</span><span class="sxs-lookup"><span data-stu-id="dfe22-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="dfe22-173">单击**电话号码：删除**链接将 `Message=RemovePhoneSuccess` 作为查询字符串。</span><span class="sxs-lookup"><span data-stu-id="dfe22-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="dfe22-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="dfe22-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="dfe22-175">`AddPhoneNumber` 操作方法会显示一个对话框，用于输入可接收短信消息的电话号码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="dfe22-176">单击 "**发送验证码**" 按钮会将电话号码发送到 HTTP POST `AddPhoneNumber` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="dfe22-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="dfe22-177">`GenerateChangePhoneNumberTokenAsync` 方法将生成在 SMS 消息中设置的安全令牌。</span><span class="sxs-lookup"><span data-stu-id="dfe22-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="dfe22-178">如果已配置 SMS 服务，则会将令牌作为字符串发送 &quot;你的安全代码是 &lt;令牌&gt;&quot;。</span><span class="sxs-lookup"><span data-stu-id="dfe22-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="dfe22-179">要以异步方式调用 `SmsService.SendAsync` 方法，然后将应用重定向到 `VerifyPhoneNumber` 操作方法（显示以下对话框），您可以在其中输入验证代码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="dfe22-180">输入代码并单击 "提交" 后，代码会发布到 HTTP POST `VerifyPhoneNumber` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="dfe22-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="dfe22-181">`ChangePhoneNumberAsync` 方法检查已发布的安全代码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="dfe22-182">如果代码正确，则会将电话号码添加到 `AspNetUsers` 表的 `PhoneNumber` 字段。</span><span class="sxs-lookup"><span data-stu-id="dfe22-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="dfe22-183">如果调用成功，则调用 `SignInAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="dfe22-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="dfe22-184">`isPersistent` 参数设置是否在多个请求之间保留身份验证会话。</span><span class="sxs-lookup"><span data-stu-id="dfe22-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="dfe22-185">更改安全配置文件时，会生成新的安全戳，并将其存储在*AspNetUsers*表的 `SecurityStamp` 字段中。</span><span class="sxs-lookup"><span data-stu-id="dfe22-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="dfe22-186">请注意，"`SecurityStamp`" 字段不同于 "安全" cookie。</span><span class="sxs-lookup"><span data-stu-id="dfe22-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="dfe22-187">安全 cookie 不会存储在 `AspNetUsers` 表中（或标识 DB 中的任何其他位置）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="dfe22-188">安全 cookie 令牌使用[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)自签名，并使用 `UserId, SecurityStamp` 和过期时间信息创建。</span><span class="sxs-lookup"><span data-stu-id="dfe22-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="dfe22-189">Cookie 中间件检查每个请求的 cookie。</span><span class="sxs-lookup"><span data-stu-id="dfe22-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="dfe22-190">`Startup` 类中的 `SecurityStampValidator` 方法将按 `validateInterval`指定的方式，定期访问数据库并检查安全标记。</span><span class="sxs-lookup"><span data-stu-id="dfe22-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="dfe22-191">这种情况仅每30分钟发生一次（在我们的示例中），除非你更改安全配置文件。</span><span class="sxs-lookup"><span data-stu-id="dfe22-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="dfe22-192">选择了30分钟间隔，以最大程度地减少对数据库的行程。</span><span class="sxs-lookup"><span data-stu-id="dfe22-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="dfe22-193">对安全配置文件进行任何更改时，需要调用 `SignInAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="dfe22-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="dfe22-194">当安全配置文件更改时，数据库将更新 `SecurityStamp` 字段，而不调用 `SignInAsync` 方法，*只*需在 OWIN 管道到达数据库（`validateInterval`）时才会保持登录状态。</span><span class="sxs-lookup"><span data-stu-id="dfe22-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="dfe22-195">可以通过将 `SignInAsync` 方法更改为立即返回，并将 cookie `validateInterval` 属性设置为30分钟到5秒，来对此进行测试：</span><span class="sxs-lookup"><span data-stu-id="dfe22-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="dfe22-196">在上述代码更改的情况下，你可以更改安全配置文件（例如，通过更改**启用了两个因素**的状态），在 `SecurityStampValidator.OnValidateIdentity` 方法失败时，将在5秒后注销。</span><span class="sxs-lookup"><span data-stu-id="dfe22-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="dfe22-197">删除 `SignInAsync` 方法中的返回行，使另一个安全配置文件发生更改，并且不会被注销。`SignInAsync` 方法会生成新的安全 cookie。</span><span class="sxs-lookup"><span data-stu-id="dfe22-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="dfe22-198">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="dfe22-198">Enable two-factor authentication</span></span>

<span data-ttu-id="dfe22-199">在示例应用中，需要使用 UI 启用双因素身份验证（2FA）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="dfe22-200">若要启用2FA，请在导航栏中单击你的用户 ID （电子邮件别名）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="dfe22-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="dfe22-201">单击 "启用 2FA"。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="dfe22-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="dfe22-202">注销，然后重新登录。</span><span class="sxs-lookup"><span data-stu-id="dfe22-202">Log out, then log back in.</span></span> <span data-ttu-id="dfe22-203">如果已启用电子邮件（请参阅[上一个教程](account-confirmation-and-password-recovery-with-aspnet-identity.md)），可以为2FA 选择 SMS 或电子邮件。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="dfe22-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="dfe22-204">此时会显示 "验证代码" 页，您可以在其中输入代码（通过短信或电子邮件）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="dfe22-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="dfe22-205">单击 "**记住此浏览器**" 复选框会使你不需要使用2FA 登录到该计算机和浏览器。</span><span class="sxs-lookup"><span data-stu-id="dfe22-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="dfe22-206">如果启用2FA 并单击 "**记住"，此浏览器**将为你提供强大的2FA 防护，防止恶意用户尝试访问你的帐户，只要他们无权访问你的计算机。</span><span class="sxs-lookup"><span data-stu-id="dfe22-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="dfe22-207">你可以在你经常使用的任何专用计算机上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="dfe22-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="dfe22-208">通过设置**记住此浏览器**，你可以从不经常使用的计算机获得2FA 的增强的安全性，并且你无需在自己的计算机上使用2FA。</span><span class="sxs-lookup"><span data-stu-id="dfe22-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="dfe22-209">如何注册双因素身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="dfe22-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="dfe22-210">创建新 MVC 项目时， *IdentityConfig.cs*文件包含以下代码来注册双因素身份验证提供程序：</span><span class="sxs-lookup"><span data-stu-id="dfe22-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="dfe22-211">为2FA 添加电话号码</span><span class="sxs-lookup"><span data-stu-id="dfe22-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="dfe22-212">`Manage` 控制器中的 `AddPhoneNumber` 操作方法会生成一个安全令牌，并将其发送到你提供的电话号码。</span><span class="sxs-lookup"><span data-stu-id="dfe22-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="dfe22-213">发送令牌后，它会重定向到 `VerifyPhoneNumber` 操作方法，你可以在该方法中输入代码，以便为2FA 注册 SMS。</span><span class="sxs-lookup"><span data-stu-id="dfe22-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="dfe22-214">在验证了电话号码之前，不会使用 SMS 2FA。</span><span class="sxs-lookup"><span data-stu-id="dfe22-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="dfe22-215">启用2FA</span><span class="sxs-lookup"><span data-stu-id="dfe22-215">Enabling 2FA</span></span>

<span data-ttu-id="dfe22-216">`EnableTFA` 操作方法启用2FA：</span><span class="sxs-lookup"><span data-stu-id="dfe22-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="dfe22-217">请注意，必须调用 `SignInAsync`，因为 enable 2FA 是对安全配置文件的更改。</span><span class="sxs-lookup"><span data-stu-id="dfe22-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="dfe22-218">当启用2FA 时，用户将需要使用2FA 登录，并使用已注册的2FA 方法（示例中的 SMS 和电子邮件）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="dfe22-219">可以添加更多的2FA 提供程序（如 QR 码生成器），也可以编写自己的提供程序（请参阅将[Google 身份验证器与 ASP.NET Identity 一起使用](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="dfe22-220">2FA 代码是使用[基于时间的一次性密码算法](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)生成的，代码的有效期为6分钟。</span><span class="sxs-lookup"><span data-stu-id="dfe22-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="dfe22-221">如果输入代码所用的时间超过6分钟，则将收到无效的代码错误消息。</span><span class="sxs-lookup"><span data-stu-id="dfe22-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="dfe22-222">合并社会和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="dfe22-222">Combine social and local login accounts</span></span>

<span data-ttu-id="dfe22-223">可以通过单击电子邮件链接来合并本地帐户和社交帐户。</span><span class="sxs-lookup"><span data-stu-id="dfe22-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="dfe22-224">在下面的序列中 &quot;RickAndMSFT@gmail.com&quot; 最初创建为本地登录名，但你可以先将该帐户创建为社交日志，然后添加本地登录名。</span><span class="sxs-lookup"><span data-stu-id="dfe22-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="dfe22-225">单击 "**管理**" 链接。</span><span class="sxs-lookup"><span data-stu-id="dfe22-225">Click on the **Manage** link.</span></span> <span data-ttu-id="dfe22-226">请注意与此帐户关联的0个外部（社交登录）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="dfe22-227">单击 "其他登录服务" 链接，并接受应用请求。</span><span class="sxs-lookup"><span data-stu-id="dfe22-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="dfe22-228">这两个帐户已合并，你将能够使用这两个帐户进行登录。</span><span class="sxs-lookup"><span data-stu-id="dfe22-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="dfe22-229">你可能希望用户在身份验证服务中的社交日志关闭或无法访问其社交帐户时添加本地帐户。</span><span class="sxs-lookup"><span data-stu-id="dfe22-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="dfe22-230">在下图中，Tom 是中的社交登录（可从 **外部登录中查看：1** 显示在页面上）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="dfe22-231">单击 "**选择密码**" 可添加与同一帐户关联的本地日志。</span><span class="sxs-lookup"><span data-stu-id="dfe22-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="dfe22-232">防止暴力破解攻击</span><span class="sxs-lookup"><span data-stu-id="dfe22-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="dfe22-233">可以通过启用用户锁定来保护应用上的帐户免遭字典攻击。</span><span class="sxs-lookup"><span data-stu-id="dfe22-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="dfe22-234">`ApplicationUserManager Create` 方法中的以下代码将配置锁定：</span><span class="sxs-lookup"><span data-stu-id="dfe22-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="dfe22-235">上述代码仅启用了双因素身份验证的锁定。</span><span class="sxs-lookup"><span data-stu-id="dfe22-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="dfe22-236">虽然你可以通过在帐户控制器的 `Login` 方法中将 `shouldLockout` 更改为 true 来启用登录名锁定，但建议你不要为登录名启用锁定，因为这会使帐户容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)登录攻击。</span><span class="sxs-lookup"><span data-stu-id="dfe22-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="dfe22-237">在示例代码中，对在 `ApplicationDbInitializer Seed` 方法中创建的管理员帐户禁用锁定：</span><span class="sxs-lookup"><span data-stu-id="dfe22-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="dfe22-238">要求用户具有已验证的电子邮件帐户</span><span class="sxs-lookup"><span data-stu-id="dfe22-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="dfe22-239">以下代码要求用户先获得经过验证的电子邮件帐户，然后才能登录：</span><span class="sxs-lookup"><span data-stu-id="dfe22-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="dfe22-240">提供对2FA 要求的检查方式</span><span class="sxs-lookup"><span data-stu-id="dfe22-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="dfe22-241">本地登录和社交日志均检查是否启用了2FA。</span><span class="sxs-lookup"><span data-stu-id="dfe22-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="dfe22-242">如果启用了2FA，则 `SignInManager` logon 方法返回 `SignInStatus.RequiresVerification`，并且用户将被重定向到 `SendCode` 操作方法，在该方法中，他们必须输入代码以按顺序完成日志。</span><span class="sxs-lookup"><span data-stu-id="dfe22-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="dfe22-243">如果用户在用户本地 cookie 上设置了 RememberMe，则 `SignInManager` 将返回 `SignInStatus.Success`，并且不需要通过2FA。</span><span class="sxs-lookup"><span data-stu-id="dfe22-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="dfe22-244">下面的代码演示 `SendCode` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="dfe22-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="dfe22-245">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)是使用为用户启用的所有2FA 方法创建的。</span><span class="sxs-lookup"><span data-stu-id="dfe22-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="dfe22-246">[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)传递给[DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper，使用户可以选择2FA 方法（通常为电子邮件和短信）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="dfe22-247">用户发布2FA 方法后，将调用 `HTTP POST SendCode` 操作方法，`SignInManager` 发送2FA 代码，并将用户重定向到 `VerifyCode` 操作方法，用户可以在其中输入代码以完成登录。</span><span class="sxs-lookup"><span data-stu-id="dfe22-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="dfe22-248">2FA 锁定</span><span class="sxs-lookup"><span data-stu-id="dfe22-248">2FA Lockout</span></span>

<span data-ttu-id="dfe22-249">虽然你可以在登录密码尝试失败时设置帐户锁定，但该方法会使你的登录容易受到[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)锁定。</span><span class="sxs-lookup"><span data-stu-id="dfe22-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="dfe22-250">建议仅将帐户锁定用于2FA。</span><span class="sxs-lookup"><span data-stu-id="dfe22-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="dfe22-251">创建 `ApplicationUserManager` 时，示例代码将 2FA `MaxFailedAccessAttemptsBeforeLockout` 锁定设置为5。</span><span class="sxs-lookup"><span data-stu-id="dfe22-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="dfe22-252">用户登录（通过本地帐户或社交帐户）后，每次在2FA 中尝试失败，并且如果达到最大尝试次数，则用户将被锁定5分钟（可以使用 `DefaultAccountLockoutTimeSpan`设置锁定超时时间）。</span><span class="sxs-lookup"><span data-stu-id="dfe22-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="dfe22-253">其他资源</span><span class="sxs-lookup"><span data-stu-id="dfe22-253">Additional Resources</span></span>

- <span data-ttu-id="dfe22-254">[ASP.NET Identity 推荐的资源](../getting-started/aspnet-identity-recommended-resources.md)标识博客、视频、教程和优秀链接的完整列表。</span><span class="sxs-lookup"><span data-stu-id="dfe22-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="dfe22-255">[带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)还演示如何将配置文件信息添加到用户表中。</span><span class="sxs-lookup"><span data-stu-id="dfe22-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="dfe22-256">[ASP.NET MVC 和标识2.0：了解 John Atten 的基础知识](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dfe22-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="dfe22-257">帐户确认和密码恢复与 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="dfe22-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="dfe22-258">ASP.NET 标识简介</span><span class="sxs-lookup"><span data-stu-id="dfe22-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="dfe22-259">[公告 ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) By Pranav RASTOGI 撰写的 RTM。</span><span class="sxs-lookup"><span data-stu-id="dfe22-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="dfe22-260">[ASP.NET Identity 2.0：设置帐户验证和由 John Atten](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 的双重身份验证。</span><span class="sxs-lookup"><span data-stu-id="dfe22-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
