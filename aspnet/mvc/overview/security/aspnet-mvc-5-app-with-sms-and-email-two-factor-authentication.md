---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: ASP.NET MVC 5 应用（带有 SMS 和电子邮件双因素身份验证） |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍如何使用双因素身份验证生成 ASP.NET MVC 5 web 应用。 应完成创建安全的 ASP.NET MVC 5 web 应用
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457591"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="3e4d5-104">具有 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用</span><span class="sxs-lookup"><span data-stu-id="3e4d5-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>

<span data-ttu-id="3e4d5-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3e4d5-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="3e4d5-106">本教程介绍如何使用双因素身份验证生成 ASP.NET MVC 5 web 应用。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="3e4d5-107">在继续操作之前，应完成[创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="3e4d5-108">可在[此处](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)下载完成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="3e4d5-109">下载内容包含调试帮助程序，可让你在不设置电子邮件或 SMS 提供程序的情况下测试电子邮件确认和短信。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="3e4d5-110">本教程由[Rick Anderson](https://blogs.msdn.com/rickAndy) （Twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ）编写。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

- [<span data-ttu-id="3e4d5-111">创建 ASP.NET MVC 应用</span><span class="sxs-lookup"><span data-stu-id="3e4d5-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="3e4d5-112">设置 SMS 以实现双重身份验证</span><span class="sxs-lookup"><span data-stu-id="3e4d5-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="3e4d5-113">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="3e4d5-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="3e4d5-114">其他资源</span><span class="sxs-lookup"><span data-stu-id="3e4d5-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="3e4d5-115">创建 ASP.NET MVC 应用</span><span class="sxs-lookup"><span data-stu-id="3e4d5-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="3e4d5-116">首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="3e4d5-117">安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="3e4d5-118">警告：在继续操作之前，应完成[创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="3e4d5-119">若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="3e4d5-120">创建新的 ASP.NET Web 项目，并选择 MVC 模板。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="3e4d5-121">Web 窗体还支持 ASP.NET Identity，因此你可以按照 web 窗体应用程序中的类似步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="3e4d5-122">将默认身份验证保留为**单独的用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="3e4d5-123">如果要在 Azure 中托管应用程序，请选中复选框。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="3e4d5-124">稍后在本教程中，我们将部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="3e4d5-125">可以[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="3e4d5-126">将[项目设置为使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="3e4d5-127">设置 SMS 以实现双重身份验证</span><span class="sxs-lookup"><span data-stu-id="3e4d5-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="3e4d5-128">本教程提供了使用 Twilio 或 ASPSMS 的说明，但你可以使用任何其他 SMS 提供程序。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="3e4d5-129">**使用 SMS 提供程序创建用户帐户**</span><span class="sxs-lookup"><span data-stu-id="3e4d5-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="3e4d5-130">创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="3e4d5-131">**安装其他包或添加服务引用**</span><span class="sxs-lookup"><span data-stu-id="3e4d5-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="3e4d5-132">Twilio</span><span class="sxs-lookup"><span data-stu-id="3e4d5-132">Twilio:</span></span>  
   <span data-ttu-id="3e4d5-133">在“包管理器控制台”中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3e4d5-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="3e4d5-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="3e4d5-134">ASPSMS:</span></span>  
   <span data-ttu-id="3e4d5-135">需要添加以下服务引用：</span><span class="sxs-lookup"><span data-stu-id="3e4d5-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="3e4d5-136">地址:</span><span class="sxs-lookup"><span data-stu-id="3e4d5-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="3e4d5-137">命名空间:</span><span class="sxs-lookup"><span data-stu-id="3e4d5-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="3e4d5-138">**了解 SMS 提供程序用户凭据**</span><span class="sxs-lookup"><span data-stu-id="3e4d5-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="3e4d5-139">Twilio</span><span class="sxs-lookup"><span data-stu-id="3e4d5-139">Twilio:</span></span>  
   <span data-ttu-id="3e4d5-140">在 Twilio 帐户的 "**仪表板**" 选项卡中，复制 "**帐户 SID** " 和 "**身份验证令牌**"。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="3e4d5-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="3e4d5-141">ASPSMS:</span></span>  
   <span data-ttu-id="3e4d5-142">从帐户设置中，导航到**用户密钥**，并将其与自定义**密码**一起复制。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="3e4d5-143">稍后我们将这些值存储在 web.config*文件中的 `"SMSAccountIdentification"`* 和 `"SMSAccountPassword"`。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="3e4d5-144">**指定 SenderID/发起方**</span><span class="sxs-lookup"><span data-stu-id="3e4d5-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="3e4d5-145">Twilio</span><span class="sxs-lookup"><span data-stu-id="3e4d5-145">Twilio:</span></span>  
   <span data-ttu-id="3e4d5-146">从 "**数字**" 选项卡中，复制 Twilio 的电话号码。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="3e4d5-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="3e4d5-147">ASPSMS:</span></span>  
   <span data-ttu-id="3e4d5-148">在 "**解锁**工作项" 菜单中，解锁一个或多个发信方，或选择一个字母数字发信方（并非所有网络都支持）。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="3e4d5-149">稍后我们*将在 web.config 文件中*将此值存储 `"SMSAccountFrom"`。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="3e4d5-150">**将 SMS 提供程序凭据传输到应用中**</span><span class="sxs-lookup"><span data-stu-id="3e4d5-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="3e4d5-151">使凭据和发件人电话号码可用于应用。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="3e4d5-152">为了简单起见，我们将这些值存储在 web.config*文件中*。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="3e4d5-153">部署到 Azure 时，可以安全地将值存储在 "网站配置" 选项卡上的 "**应用设置**" 部分。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="3e4d5-154">安全性-永远不要将敏感数据存储在源代码中。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="3e4d5-155">帐户和凭据将添加到上面的代码中，以使示例简单。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="3e4d5-156">请参阅[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="3e4d5-157">**将数据传输到 SMS 提供程序**</span><span class="sxs-lookup"><span data-stu-id="3e4d5-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="3e4d5-158">在*应用\_Start\IdentityConfig.cs*文件中配置 `SmsService` 类。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="3e4d5-159">根据所使用的 SMS 提供程序，激活 " **Twilio** " 或 " **ASPSMS** " 部分：</span><span class="sxs-lookup"><span data-stu-id="3e4d5-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="3e4d5-160">更新*Views\Manage\Index.cshtml* Razor 视图：（注意：不要只删除退出代码中的注释，使用下面的代码。）</span><span class="sxs-lookup"><span data-stu-id="3e4d5-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="3e4d5-161">验证 `ManageController` 中的 `EnableTwoFactorAuthentication` 和 `DisableTwoFactorAuthentication` 操作方法是否具有[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)属性：</span><span class="sxs-lookup"><span data-stu-id="3e4d5-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="3e4d5-162">运行该应用，然后用之前注册的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="3e4d5-163">单击您的 "用户 ID"，在 `Manage` 控制器中激活 `Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="3e4d5-164">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="3e4d5-165">`AddPhoneNumber` 操作方法会显示一个对话框，用于输入可接收短信消息的电话号码。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="3e4d5-166">几秒钟后，会收到一条包含验证码的短信。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="3e4d5-167">输入并按 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="3e4d5-168">"管理" 视图显示已添加的电话号码。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="3e4d5-169">启用双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="3e4d5-169">Enable two-factor authentication</span></span>

<span data-ttu-id="3e4d5-170">在模板生成的应用中，需要使用 UI 启用双因素身份验证（2FA）。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="3e4d5-171">若要启用2FA，请在导航栏中单击你的用户 ID （电子邮件别名）。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="3e4d5-172">单击 "启用 2FA"。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="3e4d5-173">注销，然后重新登录。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-173">Logout, then log back in.</span></span> <span data-ttu-id="3e4d5-174">如果已启用电子邮件（请参阅[上一个教程](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)），可以为2FA 选择 SMS 或电子邮件。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="3e4d5-175">此时会显示 "验证代码" 页，您可以在其中输入代码（通过短信或电子邮件）。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="3e4d5-176">单击 "**记住此浏览器**" 复选框会使你不需要使用2FA 在你选中此复选框时使用的浏览器和设备登录。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="3e4d5-177">只要恶意用户无法访问你的设备，启用2FA 并单击 "记住"，**此浏览器**将为你提供便利的单步密码访问权限，同时仍保留对来自不受信任设备的所有访问的强2FA 保护。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="3e4d5-178">可以在您经常使用任何专用设备上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="3e4d5-179">本教程简要介绍了如何在新的 ASP.NET MVC 应用程序上启用2FA。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="3e4d5-180">本教程[使用 SMS 的双因素身份验证和带 ASP.NET Identity 的电子邮件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)将详细介绍该示例的代码。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="3e4d5-181">其他资源</span><span class="sxs-lookup"><span data-stu-id="3e4d5-181">Additional Resources</span></span>

- <span data-ttu-id="3e4d5-182">[使用 SMS 和电子邮件的双因素身份验证 ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)详细介绍了双重身份验证</span><span class="sxs-lookup"><span data-stu-id="3e4d5-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="3e4d5-183">指向 ASP.NET Identity 推荐资源的链接</span><span class="sxs-lookup"><span data-stu-id="3e4d5-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="3e4d5-184">[帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)更详细地介绍密码恢复和帐户确认。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="3e4d5-185">[带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程介绍如何使用 Facebook 和 Google OAuth 2 授权编写 ASP.NET MVC 5 应用。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="3e4d5-186">它还说明如何向标识数据库添加其他数据。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="3e4d5-187">[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="3e4d5-188">本教程添加 Azure 部署，如何使用角色保护应用，如何使用成员资格 API 添加用户和角色以及其他安全功能。</span><span class="sxs-lookup"><span data-stu-id="3e4d5-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="3e4d5-189">为 OAuth 2 创建 Google 应用并将应用连接到项目</span><span class="sxs-lookup"><span data-stu-id="3e4d5-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="3e4d5-190">在 Facebook 中创建应用并将应用连接到项目</span><span class="sxs-lookup"><span data-stu-id="3e4d5-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="3e4d5-191">在项目中设置 SSL</span><span class="sxs-lookup"><span data-stu-id="3e4d5-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [<span data-ttu-id="3e4d5-192">如何设置C#和 ASP.NET MVC 开发环境</span><span class="sxs-lookup"><span data-stu-id="3e4d5-192">How to set up your C# and ASP.NET MVC development environment</span></span>](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
