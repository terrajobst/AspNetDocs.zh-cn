---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 创建具有登录、电子邮件确认和密码重置C#的安全 ASP.NET MVC 5 web 应用 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何使用 ASP.NET Identity 成员身份系统通过电子邮件确认和密码重置生成 ASP.NET MVC 5 web 应用。 你的 ca 。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 6169c972ad0f4ee2079d3638c54a5accc4b8b3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432734"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="24dde-104">创建具有登录、电子邮件确认和密码重置功能的安全 ASP.NET MVC 5 Web 应用 (C#)</span><span class="sxs-lookup"><span data-stu-id="24dde-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="24dde-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="24dde-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="24dde-106">本教程演示如何使用 ASP.NET Identity 成员身份系统通过电子邮件确认和密码重置生成 ASP.NET MVC 5 web 应用。</span><span class="sxs-lookup"><span data-stu-id="24dde-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="24dde-107">有关本教程中使用 .NET Core 的更新版本，请参阅[ASP.NET Core 中的帐户确认和密码恢复](/aspnet/core/security/authentication/accconfirm)。</span><span class="sxs-lookup"><span data-stu-id="24dde-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core](/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="24dde-108">创建 ASP.NET MVC 应用</span><span class="sxs-lookup"><span data-stu-id="24dde-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="24dde-109">首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="24dde-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="24dde-110">安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="24dde-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="24dde-111">警告：若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="24dde-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="24dde-112">创建新的 ASP.NET Web 项目，并选择 MVC 模板。</span><span class="sxs-lookup"><span data-stu-id="24dde-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="24dde-113">Web 窗体还支持 ASP.NET Identity，因此你可以按照 web 窗体应用程序中的类似步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="24dde-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="24dde-114">将默认身份验证保留为**单独的用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="24dde-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="24dde-115">如果要在 Azure 中托管应用程序，请选中复选框。</span><span class="sxs-lookup"><span data-stu-id="24dde-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="24dde-116">稍后在本教程中，我们将部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="24dde-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="24dde-117">可以[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="24dde-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="24dde-118">将[项目设置为使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="24dde-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="24dde-119">运行应用程序，单击 "**注册**" 链接并注册用户。</span><span class="sxs-lookup"><span data-stu-id="24dde-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="24dde-120">此时，电子邮件的唯一验证是带有[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="24dde-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="24dde-121">在服务器资源管理器中，导航到 "**数据 Connections\DefaultConnection\Tables\AspNetUsers**"，右键单击并选择 "**打开表定义**"。</span><span class="sxs-lookup"><span data-stu-id="24dde-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="24dde-122">下图显示了 `AspNetUsers` 架构：</span><span class="sxs-lookup"><span data-stu-id="24dde-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="24dde-123">右键单击**AspNetUsers**表，然后选择 "**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="24dde-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="24dde-124">此时，尚未确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="24dde-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="24dde-125">单击该行，然后选择 "删除"。</span><span class="sxs-lookup"><span data-stu-id="24dde-125">Click on the row and select delete.</span></span> <span data-ttu-id="24dde-126">你将在下一步中再次添加这封电子邮件，并发送一封确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="24dde-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="24dde-127">电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="24dde-127">Email confirmation</span></span>

<span data-ttu-id="24dde-128">最佳做法是确认新用户注册的电子邮件，以验证他们是否未模拟其他用户（即，他们未注册其他人的电子邮件）。</span><span class="sxs-lookup"><span data-stu-id="24dde-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="24dde-129">假设你有讨论论坛，则需要防止 `"bob@example.com"` 注册为 `"joe@contoso.com"`。</span><span class="sxs-lookup"><span data-stu-id="24dde-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="24dde-130">如果未确认电子邮件，`"joe@contoso.com"` 可能会从你的应用收到不需要的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="24dde-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="24dde-131">假设 Bob 意外注册为 `"bib@example.com"` 并且未注意到，他无法使用密码恢复，因为该应用没有正确的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="24dde-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="24dde-132">电子邮件确认仅提供对 bot 的有限保护，不提供对已确定垃圾邮件发送者的保护，它们具有可用于注册的许多工作电子邮件别名。</span><span class="sxs-lookup"><span data-stu-id="24dde-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="24dde-133">通常，在通过电子邮件、短信或其他机制确认新用户之前，要阻止新用户将任何数据发布到您的网站。</span><span class="sxs-lookup"><span data-stu-id="24dde-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="24dde-134">在下面的部分中，我们将启用电子邮件确认并修改代码，以防止新注册的用户登录，直到他们的电子邮件经过确认。</span><span class="sxs-lookup"><span data-stu-id="24dde-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="24dde-135">挂钩 SendGrid</span><span class="sxs-lookup"><span data-stu-id="24dde-135">Hook up SendGrid</span></span>

<span data-ttu-id="24dde-136">本部分中的说明不是最新的。</span><span class="sxs-lookup"><span data-stu-id="24dde-136">The instructions in this section are not current.</span></span> <span data-ttu-id="24dde-137">有关更新的说明，请参阅[配置 SendGrid 电子邮件提供程序](/aspnet/core/security/authentication/accconfirm#configure-email-provider)。</span><span class="sxs-lookup"><span data-stu-id="24dde-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="24dde-138">虽然本教程仅介绍了如何通过[SendGrid](http://sendgrid.com/)添加电子邮件通知，但你可以使用 SMTP 和其他机制发送电子邮件（请参阅[其他资源](#addRes)）。</span><span class="sxs-lookup"><span data-stu-id="24dde-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="24dde-139">在“包管理器控制台”中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="24dde-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="24dde-140">请参阅[Azure SendGrid 注册页](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)并注册免费的 SendGrid 帐户。</span><span class="sxs-lookup"><span data-stu-id="24dde-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="24dde-141">通过在*App_Start/identityconfig.cs*中添加类似于以下内容的代码来配置 SendGrid：</span><span class="sxs-lookup"><span data-stu-id="24dde-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="24dde-142">需要添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="24dde-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="24dde-143">为了简单起见，我们将应用程序设置*存储在 web.config 文件中*：</span><span class="sxs-lookup"><span data-stu-id="24dde-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="24dde-144">安全性-永远不要将敏感数据存储在源代码中。</span><span class="sxs-lookup"><span data-stu-id="24dde-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="24dde-145">帐户和凭据存储在 appSetting 中。</span><span class="sxs-lookup"><span data-stu-id="24dde-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="24dde-146">在 Azure 上，您可以安全地存储这些值在 **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="24dde-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="24dde-147">请参阅[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="24dde-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="24dde-148">在帐户控制器中启用电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="24dde-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="24dde-149">验证*Views\Account\ConfirmEmail.cshtml*文件的 razor 语法是否正确。</span><span class="sxs-lookup"><span data-stu-id="24dde-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="24dde-150">（第一行中的 @ 字符可能已丢失。</span><span class="sxs-lookup"><span data-stu-id="24dde-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="24dde-151">)</span><span class="sxs-lookup"><span data-stu-id="24dde-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="24dde-152">运行应用并单击 "注册" 链接。</span><span class="sxs-lookup"><span data-stu-id="24dde-152">Run the app and click the Register link.</span></span> <span data-ttu-id="24dde-153">提交注册表单后，即已登录。</span><span class="sxs-lookup"><span data-stu-id="24dde-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="24dde-154">检查你的电子邮件帐户，并单击链接以确认你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="24dde-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="24dde-155">登录前需要确认电子邮件</span><span class="sxs-lookup"><span data-stu-id="24dde-155">Require email confirmation before log in</span></span>

<span data-ttu-id="24dde-156">当前用户完成注册表单后，用户将登录。</span><span class="sxs-lookup"><span data-stu-id="24dde-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="24dde-157">通常需要确认其电子邮件，然后才能将其记录在日志中。</span><span class="sxs-lookup"><span data-stu-id="24dde-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="24dde-158">在下面的部分中，我们将修改代码，要求新用户在登录之前获得确认电子邮件（经过身份验证）。</span><span class="sxs-lookup"><span data-stu-id="24dde-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="24dde-159">用以下突出显示的更改更新 `HttpPost Register` 方法：</span><span class="sxs-lookup"><span data-stu-id="24dde-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="24dde-160">通过注释掉 `SignInAsync` 方法，注册不会登录用户。</span><span class="sxs-lookup"><span data-stu-id="24dde-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="24dde-161">`TempData["ViewBagLink"] = callbackUrl;` 行可用于[调试应用](#dbg)并测试注册，而无需发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="24dde-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="24dde-162">`ViewBag.Message` 用于显示确认说明。</span><span class="sxs-lookup"><span data-stu-id="24dde-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="24dde-163">[下载示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)包含的代码可用于测试电子邮件确认，而无需设置电子邮件，也可用于调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="24dde-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="24dde-164">创建 `Views\Shared\Info.cshtml` 文件，并添加以下 razor 标记：</span><span class="sxs-lookup"><span data-stu-id="24dde-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="24dde-165">将[授权属性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)添加到主控制器的 `Contact` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="24dde-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="24dde-166">您可以单击 "**联系人**" 链接来验证匿名用户无权访问和经过身份验证的用户是否具有访问权限。</span><span class="sxs-lookup"><span data-stu-id="24dde-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="24dde-167">还必须更新 `HttpPost Login` 操作方法：</span><span class="sxs-lookup"><span data-stu-id="24dde-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="24dde-168">更新*Views\Shared\Error.cshtml*视图以显示错误消息：</span><span class="sxs-lookup"><span data-stu-id="24dde-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="24dde-169">删除**AspNetUsers**表中的所有帐户，其中包含要测试的电子邮件别名。</span><span class="sxs-lookup"><span data-stu-id="24dde-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="24dde-170">运行应用并验证你是否无法登录，直到你确认电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="24dde-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="24dde-171">确认电子邮件地址后，单击 "**联系人**" 链接。</span><span class="sxs-lookup"><span data-stu-id="24dde-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="24dde-172">密码恢复/重置</span><span class="sxs-lookup"><span data-stu-id="24dde-172">Password recovery/reset</span></span>

<span data-ttu-id="24dde-173">从帐户控制器的 `HttpPost ForgotPassword` 操作方法中删除注释字符：</span><span class="sxs-lookup"><span data-stu-id="24dde-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="24dde-174">从*Views\Account\Login.cshtml* razor 视图文件的 "`ForgotPassword` [html.actionlink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) " 中删除注释字符：</span><span class="sxs-lookup"><span data-stu-id="24dde-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="24dde-175">"登录" 页现在将显示用于重置密码的链接。</span><span class="sxs-lookup"><span data-stu-id="24dde-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="24dde-176">重新发送电子邮件确认链接</span><span class="sxs-lookup"><span data-stu-id="24dde-176">Resend email confirmation link</span></span>

<span data-ttu-id="24dde-177">用户创建新的本地帐户后，会通过电子邮件发送确认链接，用户在登录之前需要使用这些帐户。</span><span class="sxs-lookup"><span data-stu-id="24dde-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="24dde-178">如果用户意外删除了确认电子邮件，或电子邮件永不送达，则他们将需要再次发送确认链接。</span><span class="sxs-lookup"><span data-stu-id="24dde-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="24dde-179">下面的代码更改显示了如何启用此操作。</span><span class="sxs-lookup"><span data-stu-id="24dde-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="24dde-180">将以下帮助器方法添加到*Controllers\AccountController.cs*文件的底部：</span><span class="sxs-lookup"><span data-stu-id="24dde-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="24dde-181">更新 Register 方法以使用新帮助器：</span><span class="sxs-lookup"><span data-stu-id="24dde-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="24dde-182">如果尚未确认用户帐户，请更新 Login 方法以重新发送密码：</span><span class="sxs-lookup"><span data-stu-id="24dde-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="24dde-183">合并社会和本地登录帐户</span><span class="sxs-lookup"><span data-stu-id="24dde-183">Combine social and local login accounts</span></span>

<span data-ttu-id="24dde-184">可以通过单击电子邮件链接来合并本地帐户和社交帐户。</span><span class="sxs-lookup"><span data-stu-id="24dde-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="24dde-185">在以下序列中， **RickAndMSFT@gmail.com** 首先创建为本地登录名，但你可以先将该帐户创建为社交日志，然后添加本地登录名。</span><span class="sxs-lookup"><span data-stu-id="24dde-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="24dde-186">单击 "**管理**" 链接。</span><span class="sxs-lookup"><span data-stu-id="24dde-186">Click on the **Manage** link.</span></span> <span data-ttu-id="24dde-187">请注意 **外部登录名：0** 与此帐户关联。</span><span class="sxs-lookup"><span data-stu-id="24dde-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="24dde-188">单击 "其他登录服务" 链接，并接受应用请求。</span><span class="sxs-lookup"><span data-stu-id="24dde-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="24dde-189">这两个帐户已合并，你将能够使用这两个帐户进行登录。</span><span class="sxs-lookup"><span data-stu-id="24dde-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="24dde-190">你可能希望用户在身份验证服务中的社交日志关闭或无法访问其社交帐户时添加本地帐户。</span><span class="sxs-lookup"><span data-stu-id="24dde-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="24dde-191">在下图中，Tom 是中的社交登录（可从 **外部登录中查看：1** 显示在页面上）。</span><span class="sxs-lookup"><span data-stu-id="24dde-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="24dde-192">单击 "**选择密码**" 可添加与同一帐户关联的本地日志。</span><span class="sxs-lookup"><span data-stu-id="24dde-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="24dde-193">更深入地确认电子邮件</span><span class="sxs-lookup"><span data-stu-id="24dde-193">Email confirmation in more depth</span></span>

<span data-ttu-id="24dde-194">本主题中的教程[帐户确认和密码恢复 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)将深入了解更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="24dde-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="24dde-195">调试应用程序</span><span class="sxs-lookup"><span data-stu-id="24dde-195">Debugging the app</span></span>

<span data-ttu-id="24dde-196">如果未收到包含链接的电子邮件：</span><span class="sxs-lookup"><span data-stu-id="24dde-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="24dde-197">检查垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="24dde-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="24dde-198">登录到你的 SendGrid 帐户，并单击 "[电子邮件" 活动链接](https://sendgrid.com/logs/index)。</span><span class="sxs-lookup"><span data-stu-id="24dde-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="24dde-199">若要在没有电子邮件的情况下测试验证链接，请下载[已完成的示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。</span><span class="sxs-lookup"><span data-stu-id="24dde-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="24dde-200">确认链接和确认代码将显示在该页上。</span><span class="sxs-lookup"><span data-stu-id="24dde-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="24dde-201">其他资源</span><span class="sxs-lookup"><span data-stu-id="24dde-201">Additional Resources</span></span>

- [<span data-ttu-id="24dde-202">指向 ASP.NET Identity 推荐资源的链接</span><span class="sxs-lookup"><span data-stu-id="24dde-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="24dde-203">[帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)更详细地介绍密码恢复和帐户确认。</span><span class="sxs-lookup"><span data-stu-id="24dde-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="24dde-204">[带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程介绍如何使用 Facebook 和 Google OAuth 2 授权编写 ASP.NET MVC 5 应用。</span><span class="sxs-lookup"><span data-stu-id="24dde-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="24dde-205">它还说明如何向标识数据库添加其他数据。</span><span class="sxs-lookup"><span data-stu-id="24dde-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="24dde-206">[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="24dde-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="24dde-207">本教程添加 Azure 部署，如何使用角色保护应用，如何使用成员资格 API 添加用户和角色以及其他安全功能。</span><span class="sxs-lookup"><span data-stu-id="24dde-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="24dde-208">为 OAuth 2 创建 Google 应用并将应用连接到项目</span><span class="sxs-lookup"><span data-stu-id="24dde-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="24dde-209">在 Facebook 中创建应用并将应用连接到项目</span><span class="sxs-lookup"><span data-stu-id="24dde-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="24dde-210">在项目中设置 SSL</span><span class="sxs-lookup"><span data-stu-id="24dde-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
