---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 使用用户注册、电子邮件确认和密码重置（C#）创建安全的 ASP.NET Web 窗体应用程序 |Microsoft Docs
author: Erikre
description: 本教程介绍如何使用 ASP.NET Identity 成员，使用用户注册、电子邮件确认和密码重置来构建 ASP.NET Web 窗体应用 。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: af3653bc164810126bc3bf8f1b1794d75642d807
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507128"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a><span data-ttu-id="efd2b-103">创建具有用户注册、电子邮件确认和密码重置功能的安全 ASP.NET Web 窗体应用 (C#)</span><span class="sxs-lookup"><span data-stu-id="efd2b-103">Create a secure ASP.NET Web Forms app with user registration, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="efd2b-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="efd2b-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="efd2b-105">本教程介绍如何使用 ASP.NET Identity 成员身份系统，使用用户注册、电子邮件确认和密码重置构建 ASP.NET Web 窗体应用。</span><span class="sxs-lookup"><span data-stu-id="efd2b-105">This tutorial shows you how to build an ASP.NET Web Forms app with user registration, email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="efd2b-106">本教程基于 Rick Anderson 的[MVC 教程](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。</span><span class="sxs-lookup"><span data-stu-id="efd2b-106">This tutorial was based on Rick Anderson's [MVC tutorial](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="efd2b-107">简介</span><span class="sxs-lookup"><span data-stu-id="efd2b-107">Introduction</span></span>

<span data-ttu-id="efd2b-108">本教程将指导你完成使用 Visual Studio 和 ASP.NET 4.5 创建 ASP.NET Web 窗体应用程序所需的步骤，以使用用户注册、电子邮件确认和密码重置创建安全的 Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="efd2b-108">This tutorial guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio and ASP.NET 4.5 to create a secure Web Forms app with user registration, email confirmation and password reset.</span></span>

### <a name="tutorial-tasks-and-information"></a><span data-ttu-id="efd2b-109">教程任务和信息：</span><span class="sxs-lookup"><span data-stu-id="efd2b-109">Tutorial Tasks and Information:</span></span>

- [<span data-ttu-id="efd2b-110">创建 ASP.NET Web 窗体应用</span><span class="sxs-lookup"><span data-stu-id="efd2b-110">Create an ASP.NET Web Forms app</span></span>](#createWebForms)
- [<span data-ttu-id="efd2b-111">挂钩 SendGrid</span><span class="sxs-lookup"><span data-stu-id="efd2b-111">Hook Up SendGrid</span></span>](#SG)
- [<span data-ttu-id="efd2b-112">登录前需要确认电子邮件</span><span class="sxs-lookup"><span data-stu-id="efd2b-112">Require Email Confirmation Before Log In</span></span>](#require)
- [<span data-ttu-id="efd2b-113">密码恢复和重置</span><span class="sxs-lookup"><span data-stu-id="efd2b-113">Password Recovery and Reset</span></span>](#reset)
- [<span data-ttu-id="efd2b-114">重新发送电子邮件确认链接</span><span class="sxs-lookup"><span data-stu-id="efd2b-114">Resend Email Confirmation Link</span></span>](#rsend)
- [<span data-ttu-id="efd2b-115">应用故障排除</span><span class="sxs-lookup"><span data-stu-id="efd2b-115">Troubleshooting the App</span></span>](#dbg)
- [<span data-ttu-id="efd2b-116">其他资源</span><span class="sxs-lookup"><span data-stu-id="efd2b-116">Additional Resources</span></span>](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a><span data-ttu-id="efd2b-117">创建 ASP.NET Web 窗体应用</span><span class="sxs-lookup"><span data-stu-id="efd2b-117">Create an ASP.NET Web Forms App</span></span>

<span data-ttu-id="efd2b-118">首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="efd2b-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="efd2b-119">同时安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="efd2b-119">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher as well.</span></span>

> [!NOTE]
> <span data-ttu-id="efd2b-120">警告：若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="efd2b-120">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="efd2b-121">创建新项目（**文件** -&gt; "**新建项目**"），然后从 "**新建项目**" 对话框中选择 " **ASP.NET Web 应用程序**" 模板和最新 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="efd2b-121">Create a new project (**File** -&gt; **New Project**) and select the **ASP.NET Web Application** template and the latest .NET Framework version from the **New Project** dialog box.</span></span>
2. <span data-ttu-id="efd2b-122">在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web 窗体**" 模板。</span><span class="sxs-lookup"><span data-stu-id="efd2b-122">From the **New ASP.NET Project** dialog box, select the **Web Forms** template.</span></span> <span data-ttu-id="efd2b-123">将默认身份验证保留为**单独的用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="efd2b-123">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="efd2b-124">如果要在 Azure 中托管应用程序，请选中 "**在云中保留主机**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="efd2b-124">If you'd like to host the app in Azure, leave the **Host in the cloud** check box checked.</span></span>   
 <span data-ttu-id="efd2b-125">然后单击 **"确定"** 以创建新项目。</span><span class="sxs-lookup"><span data-stu-id="efd2b-125">Then, click **OK** to create the new project.</span></span>  
    <span data-ttu-id="efd2b-126">![新的 ASP.NET 项目 "对话框](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="efd2b-126">![New ASP.NET Project dialog box](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span></span>
3. <span data-ttu-id="efd2b-127">为项目启用安全套接字层（SSL）。</span><span class="sxs-lookup"><span data-stu-id="efd2b-127">Enable Secure Sockets Layer (SSL) for the project.</span></span> <span data-ttu-id="efd2b-128">按照[使用 Web 窗体教程系列的入门](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)的为**项目启用 SSL**部分中提供的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="efd2b-128">Follow the steps available in the **Enable SSL for the Project** section of the [Getting Started with Web Forms tutorial series](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span></span>
4. <span data-ttu-id="efd2b-129">运行应用程序，单击 "**注册**" 链接并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-129">Run the app, click the **Register** link and register a new user.</span></span> <span data-ttu-id="efd2b-130">此时，电子邮件的唯一验证基于[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性，以确保电子邮件地址的格式正确。</span><span class="sxs-lookup"><span data-stu-id="efd2b-130">At this point, the only validation on the email is based on the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute to ensure the email address is well-formed.</span></span> <span data-ttu-id="efd2b-131">你将修改代码来添加电子邮件确认。</span><span class="sxs-lookup"><span data-stu-id="efd2b-131">You will modify the code to add email confirmation.</span></span> <span data-ttu-id="efd2b-132">关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="efd2b-132">Close the browser window.</span></span>
5. <span data-ttu-id="efd2b-133">在 Visual Studio**服务器资源管理器**中（**查看** -&gt;**服务器资源管理器**），导航到 "**数据 Connections\DefaultConnection\Tables\AspNetUsers**"，右键单击并选择 "**打开表定义**"。</span><span class="sxs-lookup"><span data-stu-id="efd2b-133">In **Server Explorer** of Visual Studio (**View** -&gt; **Server Explorer**), navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span> 

    <span data-ttu-id="efd2b-134">下图显示了 `AspNetUsers` 表架构：</span><span class="sxs-lookup"><span data-stu-id="efd2b-134">The following image shows the `AspNetUsers` table schema:</span></span>

    ![AspNetUsers 表架构](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="efd2b-136">在**服务器资源管理器**中，右键单击**AspNetUsers**表并选择 "**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="efd2b-136">In **Server Explorer**, right-click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
  
    ![AspNetUsers 表数据](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="efd2b-138">此时，尚未确认注册用户的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="efd2b-138">At this point the email for the registered user has not been confirmed.</span></span>
7. <span data-ttu-id="efd2b-139">单击该行，然后选择 "删除" 以删除该用户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-139">Click on the row and select delete to delete the user.</span></span> <span data-ttu-id="efd2b-140">你将在下一步中再次添加这封电子邮件，并向电子邮件地址发送一封确认消息。</span><span class="sxs-lookup"><span data-stu-id="efd2b-140">You'll add this email again in the next step and send a confirmation message to the email address.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="efd2b-141">电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="efd2b-141">Email Confirmation</span></span>

<span data-ttu-id="efd2b-142">最佳做法是在注册新用户时确认电子邮件，以验证他们是否未模拟其他用户（即，他们尚未注册其他人的电子邮件）。</span><span class="sxs-lookup"><span data-stu-id="efd2b-142">It's a best practice to confirm the email during the registration of a new user to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="efd2b-143">假设你有讨论论坛，则需要防止 `"bob@cpandl.com"` 注册为 `"joe@contoso.com"`。</span><span class="sxs-lookup"><span data-stu-id="efd2b-143">Suppose you had a discussion forum, you would want to prevent `"bob@cpandl.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="efd2b-144">如果未确认电子邮件，`"joe@contoso.com"` 可能会从你的应用收到不需要的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="efd2b-144">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="efd2b-145">假设 Bob 意外注册为 `"bib@cpandl.com"` 并且未注意到，他无法使用密码恢复，因为该应用没有正确的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="efd2b-145">Suppose Bob accidentally registered as `"bib@cpandl.com"` and hadn't noticed it, he wouldn't be able to use password recovery because the app doesn't have his correct email.</span></span> <span data-ttu-id="efd2b-146">电子邮件确认仅提供对 bot 的有限保护，不会为确定的垃圾邮件提供保护。</span><span class="sxs-lookup"><span data-stu-id="efd2b-146">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers.</span></span>

<span data-ttu-id="efd2b-147">通常，你希望在用户通过电子邮件、短信或其他机制确认之前，阻止新用户将任何数据发布到你的网站。</span><span class="sxs-lookup"><span data-stu-id="efd2b-147">You generally want to prevent new users from posting any data to your website before they have been confirmed by either email, an SMS text message or another mechanism.</span></span> <span data-ttu-id="efd2b-148">在下面的部分中，我们将启用电子邮件确认并修改代码，以防止新注册的用户登录，直到他们的电子邮件经过确认。</span><span class="sxs-lookup"><span data-stu-id="efd2b-148">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span> <span data-ttu-id="efd2b-149">你将在本教程中使用电子邮件服务 SendGrid。</span><span class="sxs-lookup"><span data-stu-id="efd2b-149">You'll use the email service SendGrid in this tutorial.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="efd2b-150">挂钩 SendGrid</span><span class="sxs-lookup"><span data-stu-id="efd2b-150">Hook up SendGrid</span></span>

<span data-ttu-id="efd2b-151">由于本教程已编写，SendGrid 已更改了 API。</span><span class="sxs-lookup"><span data-stu-id="efd2b-151">SendGrid has changed it's API since this tutorial was written.</span></span> <span data-ttu-id="efd2b-152">有关最新的 SendGrid 说明，请参阅[SendGrid](http://sendgrid.com/)或[启用帐户确认和密码恢复](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)。</span><span class="sxs-lookup"><span data-stu-id="efd2b-152">For current SendGrid instructions, see [SendGrid](http://sendgrid.com/) or [Enable account confirmation and password recovery](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery).</span></span>

<span data-ttu-id="efd2b-153">虽然本教程仅介绍了如何通过[SendGrid](http://sendgrid.com/)添加电子邮件通知，但你可以使用 SMTP 和其他机制发送电子邮件（请参阅[其他资源](#addRes)）。</span><span class="sxs-lookup"><span data-stu-id="efd2b-153">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="efd2b-154">在 Visual Studio 中，打开**程序包管理器控制台**（"**工具**" -&gt; **NuGet 包**管理器 " -&gt;**包管理器控制台**"），然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="efd2b-154">In Visual Studio, open the **Package Manager Console** (**Tools** -&gt; **NuGet Package Manger** -&gt; **Package Manager Console**), and enter the following command:</span></span>  
    `Install-Package SendGrid`
2. <span data-ttu-id="efd2b-155">请参阅[Azure SendGrid 注册页](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)并注册免费的 SendGrid 帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-155">Go to the [Azure SendGrid sign-up page](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) and register for free SendGrid account.</span></span> <span data-ttu-id="efd2b-156">你还可以直接在[SendGrid 的站点](http://www.sendgrid.com)上注册免费的 SendGrid 帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-156">You can also sign-up for a free SendGrid account directly on [SendGrid's site](http://www.sendgrid.com).</span></span>
3. <span data-ttu-id="efd2b-157">从**解决方案资源管理器**打开*应用\_"开始*" 文件夹中的*IdentityConfig.cs*文件，并将以下突出显示的代码添加到 `EmailService` 类以配置**SendGrid**：</span><span class="sxs-lookup"><span data-stu-id="efd2b-157">From **Solution Explorer** open the *IdentityConfig.cs* file in the *App\_Start* folder and add the following code highlighted in yellow to the `EmailService` class to configure **SendGrid**:</span></span>

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. <span data-ttu-id="efd2b-158">另外，将以下 `using` 语句添加到*IdentityConfig.cs*文件的开头：</span><span class="sxs-lookup"><span data-stu-id="efd2b-158">Also, add the following `using` statements to the beginning of the *IdentityConfig.cs* file:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. <span data-ttu-id="efd2b-159">若要使此示例简单，请将电子邮件服务帐户值存储在*web.config 文件的*`appSettings` 部分。</span><span class="sxs-lookup"><span data-stu-id="efd2b-159">To keep this sample simple, you'll store the email service account values in the `appSettings` section of the *web.config* file.</span></span> <span data-ttu-id="efd2b-160">将以下以黄色突出显示的 XML 添加到项目根目录中的*web.config 文件：*</span><span class="sxs-lookup"><span data-stu-id="efd2b-160">Add the following XML highlighted in yellow to the *web.config* file at the root of your project:</span></span>

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > <span data-ttu-id="efd2b-161">安全性-永远不要将敏感数据存储在源代码中。</span><span class="sxs-lookup"><span data-stu-id="efd2b-161">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="efd2b-162">在此示例中，帐户和凭据存储在*web.config 文件的* **appSetting**节中。</span><span class="sxs-lookup"><span data-stu-id="efd2b-162">In this example, the account and credentials are stored in the **appSetting** section of the *Web.config* file.</span></span> <span data-ttu-id="efd2b-163">在 Azure 上，您可以安全地存储这些值在 **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="efd2b-163">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="efd2b-164">相关信息，请参阅 Rick Anderson 的主题，其标题为[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](https://go.microsoft.com/fwlink/?LinkId=513141)。</span><span class="sxs-lookup"><span data-stu-id="efd2b-164">For related information see Rick Anderson's topic titled [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span></span>
6. <span data-ttu-id="efd2b-165">添加电子邮件服务值以反映 SendGrid 的身份验证值（用户名和密码），以便可以成功地从应用发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="efd2b-165">Add the email service values to reflect your SendGrid authentication values (User Name and Password) so that you can successful send email from your app.</span></span> <span data-ttu-id="efd2b-166">请确保使用你的 SendGrid 帐户名称，而不是 SendGrid 提供的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="efd2b-166">Be sure to use your SendGrid account name rather than the email address you provided SendGrid.</span></span>

### <a name="enable-email-confirmation"></a><span data-ttu-id="efd2b-167">启用电子邮件确认</span><span class="sxs-lookup"><span data-stu-id="efd2b-167">Enable Email Confirmation</span></span>

 <span data-ttu-id="efd2b-168">若要启用电子邮件确认，你将使用以下步骤修改注册代码。</span><span class="sxs-lookup"><span data-stu-id="efd2b-168">To enable email confirmation, you'll modify the registration code using the following steps.</span></span>  

1. <span data-ttu-id="efd2b-169">在*帐户*文件夹中，打开*Register.aspx.cs*代码隐藏并更新 `CreateUser_Click` 方法，以启用以下突出显示的更改：</span><span class="sxs-lookup"><span data-stu-id="efd2b-169">In the *Account* folder, open the *Register.aspx.cs* code-behind and update the `CreateUser_Click` method to enable the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. <span data-ttu-id="efd2b-170">在**解决方案资源管理器**中，右键单击 " *default.aspx* "，然后选择 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="efd2b-170">In **Solution Explorer**, right-click *Default.aspx* and select **Set As Start Page**.</span></span>
3. <span data-ttu-id="efd2b-171">按 F5 运行应用 **。**</span><span class="sxs-lookup"><span data-stu-id="efd2b-171">Run the app by pressing **F5.**</span></span> <span data-ttu-id="efd2b-172">显示该页后，单击 "**注册**" 链接以显示 "注册" 页。</span><span class="sxs-lookup"><span data-stu-id="efd2b-172">After the page is displayed, click the **Register** link to display the Register page.</span></span>
4. <span data-ttu-id="efd2b-173">输入你的电子邮件和密码，然后单击 "**注册**" 按钮，通过 SendGrid 发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="efd2b-173">Enter your email and password, then click the **Register** button to send an email message via SendGrid.</span></span>  
   <span data-ttu-id="efd2b-174">项目和代码的当前状态将允许用户在完成注册表单后登录，即使他们没有确认其帐户也是如此。</span><span class="sxs-lookup"><span data-stu-id="efd2b-174">The current state of your project and code will allow the user to log in once they complete the registration form, even though they haven't confirmed their account.</span></span>
5. <span data-ttu-id="efd2b-175">检查你的电子邮件帐户，并单击链接以确认你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="efd2b-175">Check your email account and click on the link to confirm your email.</span></span>  
   <span data-ttu-id="efd2b-176">提交注册表单后，你将登录。</span><span class="sxs-lookup"><span data-stu-id="efd2b-176">Once you submit the registration form, you will be logged in.</span></span>  
    ![示例网站-登录](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="efd2b-178">登录前需要确认电子邮件</span><span class="sxs-lookup"><span data-stu-id="efd2b-178">Require Email Confirmation Before Log In</span></span>

<span data-ttu-id="efd2b-179">尽管已确认电子邮件帐户，但此时无需单击验证电子邮件中包含的链接即可完全登录。</span><span class="sxs-lookup"><span data-stu-id="efd2b-179">Although you have confirmed the email account, at this point you would not need to click on the link contained in the verification email to be fully signed-in.</span></span> <span data-ttu-id="efd2b-180">在下一节中，你将修改需要新用户在登录之前获得确认电子邮件的代码（经过身份验证）。</span><span class="sxs-lookup"><span data-stu-id="efd2b-180">In the following section, you will modify the code requiring new users to have a confirmed email before they are logged in (authenticated).</span></span>

1. <span data-ttu-id="efd2b-181">在 Visual Studio**解决方案资源管理器**中，在 "*帐户*" 文件夹中包含的*Register.aspx.cs*代码隐藏中更新 `CreateUser_Click` 事件，其中包含以下突出显示的更改：</span><span class="sxs-lookup"><span data-stu-id="efd2b-181">In **Solution Explorer** of Visual Studio, update the `CreateUser_Click` event in the *Register.aspx.cs* code-behind contained in the *Accounts* folder with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. <span data-ttu-id="efd2b-182">在*Login.aspx.cs*代码隐藏中更新 `LogIn` 方法，并提供以下突出显示的更改：</span><span class="sxs-lookup"><span data-stu-id="efd2b-182">Update the `LogIn` method in the *Login.aspx.cs* code-behind with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a><span data-ttu-id="efd2b-183">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="efd2b-183">Run the Application</span></span>

 <span data-ttu-id="efd2b-184">现在，你已实现代码以检查是否已确认用户的电子邮件地址，你可以在 "**注册**" 和 "**登录**" 页上检查该功能。</span><span class="sxs-lookup"><span data-stu-id="efd2b-184">Now that you have implemented the code to check whether a user's email address has been confirmed, you can check the functionality on both the **Register** and **Login** pages.</span></span> 

1. <span data-ttu-id="efd2b-185">删除**AspNetUsers**表中包含要测试的电子邮件别名的所有帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-185">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
2. <span data-ttu-id="efd2b-186">运行应用（**F5**）并验证你在确认电子邮件地址之前无法以用户身份注册。</span><span class="sxs-lookup"><span data-stu-id="efd2b-186">Run the app (**F5**) and verify you cannot register as a user until you have confirmed your email address.</span></span>
3. <span data-ttu-id="efd2b-187">在通过刚刚发送的电子邮件确认新帐户之前，请尝试用新帐户登录。</span><span class="sxs-lookup"><span data-stu-id="efd2b-187">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
 <span data-ttu-id="efd2b-188">你将看到你无法登录，并且你必须有已确认的电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-188">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span>
4. <span data-ttu-id="efd2b-189">确认电子邮件地址后，登录到该应用。</span><span class="sxs-lookup"><span data-stu-id="efd2b-189">Once you confirm your email address, log in to the app.</span></span>

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a><span data-ttu-id="efd2b-190">密码恢复和重置</span><span class="sxs-lookup"><span data-stu-id="efd2b-190">Password Recovery and Reset</span></span>

1. <span data-ttu-id="efd2b-191">在 Visual Studio 中，从*帐户*文件夹所包含的*Forgot.aspx.cs*代码隐藏中的 `Forgot` 方法中删除注释字符，使该方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="efd2b-191">In Visual Studio, remove the comment characters from the `Forgot` method in the *Forgot.aspx.cs* code-behind contained in the *Account* folder, so that the method appears as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. <span data-ttu-id="efd2b-192">打开 "*登录 .aspx* " 页。</span><span class="sxs-lookup"><span data-stu-id="efd2b-192">Open the *Login.aspx* page.</span></span> <span data-ttu-id="efd2b-193">将标记替换到**loginForm**节末尾附近，如下所示：</span><span class="sxs-lookup"><span data-stu-id="efd2b-193">Replace the markup near the end of the **loginForm** section as highlighted below:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. <span data-ttu-id="efd2b-194">打开*Login.aspx.cs*代码隐藏，取消注释 `Page_Load` 事件处理程序中以黄色突出显示的以下代码行：</span><span class="sxs-lookup"><span data-stu-id="efd2b-194">Open the *Login.aspx.cs* code-behind and uncomment the following line of code highlighted in yellow from the `Page_Load` event handler:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. <span data-ttu-id="efd2b-195">按 F5 运行应用 **。**</span><span class="sxs-lookup"><span data-stu-id="efd2b-195">Run the app by pressing **F5.**</span></span> <span data-ttu-id="efd2b-196">显示该页后，单击 "**登录**" 链接。</span><span class="sxs-lookup"><span data-stu-id="efd2b-196">After the page is displayed, click the **Log in** link.</span></span>
5. <span data-ttu-id="efd2b-197">单击 "**忘记了密码？"** 链接以显示 "**忘记密码**" 页面。</span><span class="sxs-lookup"><span data-stu-id="efd2b-197">Click the **Forgot your password?** link to display the **Forgot Password** page.</span></span>
6. <span data-ttu-id="efd2b-198">输入你的电子邮件地址，然后单击 "**提交**" 按钮，将电子邮件发送到你的地址，以便你可以重置密码。</span><span class="sxs-lookup"><span data-stu-id="efd2b-198">Enter your email address and click the **Submit** button to send an email to your address which will allow you to reset your password.</span></span>   
   <span data-ttu-id="efd2b-199">检查电子邮件帐户，并单击链接以显示 "**重置密码**" 页。</span><span class="sxs-lookup"><span data-stu-id="efd2b-199">Check your email account and click on the link to display the **Reset Password** page.</span></span>
7. <span data-ttu-id="efd2b-200">在 "**重置密码**" 页上，输入你的电子邮件、密码和确认密码。</span><span class="sxs-lookup"><span data-stu-id="efd2b-200">On the **Reset Password** page, enter your email, password, and confirmed password.</span></span> <span data-ttu-id="efd2b-201">然后，按 "**重置**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="efd2b-201">Then, press the **Reset** button.</span></span>  
   <span data-ttu-id="efd2b-202">成功重置密码后，将显示 "**更改密码**" 页。</span><span class="sxs-lookup"><span data-stu-id="efd2b-202">When you successfully reset your password, the **Password Changed** page will be displayed.</span></span> <span data-ttu-id="efd2b-203">现在可以用新密码登录。</span><span class="sxs-lookup"><span data-stu-id="efd2b-203">Now you can log in with your new password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="efd2b-204">重新发送电子邮件确认链接</span><span class="sxs-lookup"><span data-stu-id="efd2b-204">Resend Email Confirmation Link</span></span>

<span data-ttu-id="efd2b-205">用户创建新的本地帐户后，会通过电子邮件发送确认链接，用户在登录之前需要使用这些帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-205">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="efd2b-206">如果用户意外删除了确认电子邮件，或电子邮件永不送达，则他们将需要再次发送确认链接。</span><span class="sxs-lookup"><span data-stu-id="efd2b-206">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="efd2b-207">下面的代码更改显示了如何启用此操作。</span><span class="sxs-lookup"><span data-stu-id="efd2b-207">The following code changes show how to enable this.</span></span>

1. <span data-ttu-id="efd2b-208">在 Visual Studio 中，打开**Login.aspx.cs**代码隐藏，并在 `LogIn` 事件处理程序之后添加以下事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="efd2b-208">In Visual Studio, open the **Login.aspx.cs** code-behind and add the following event handler after the `LogIn` event handler:</span></span>   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. <span data-ttu-id="efd2b-209">通过更改黄色突出显示的代码，在*Login.aspx.cs*代码隐藏中修改 `LogIn` 事件处理程序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="efd2b-209">Modify the `LogIn` event handler in the *Login.aspx.cs* code-behind by changing the code highlighted in yellow as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. <span data-ttu-id="efd2b-210">通过添加黄色突出显示的代码来更新*登录 .aspx*页，如下所示：</span><span class="sxs-lookup"><span data-stu-id="efd2b-210">Update the *Login.aspx* page by adding the code highlighted in yellow as follows:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. <span data-ttu-id="efd2b-211">删除**AspNetUsers**表中包含要测试的电子邮件别名的所有帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-211">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
5. <span data-ttu-id="efd2b-212">运行应用（**F5**）并注册电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="efd2b-212">Run the app (**F5**) and register your email address.</span></span>
6. <span data-ttu-id="efd2b-213">在通过刚刚发送的电子邮件确认新帐户之前，请尝试用新帐户登录。</span><span class="sxs-lookup"><span data-stu-id="efd2b-213">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
   <span data-ttu-id="efd2b-214">你将看到你无法登录，并且你必须有已确认的电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-214">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span> <span data-ttu-id="efd2b-215">此外，你现在可以将确认消息重新发送到你的电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="efd2b-215">In addition, you can now resend a confirmation message to your email account.</span></span>
7. <span data-ttu-id="efd2b-216">输入你的电子邮件地址和密码，然后按 "**重新发送确认**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="efd2b-216">Enter your email address and password, then press the **Resend confirmation** button.</span></span>
8. <span data-ttu-id="efd2b-217">根据新发送的电子邮件确认电子邮件地址后，登录到该应用。</span><span class="sxs-lookup"><span data-stu-id="efd2b-217">Once you confirm your email address based on the newly sent email message, log in to the app.</span></span>

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a><span data-ttu-id="efd2b-218">应用故障排除</span><span class="sxs-lookup"><span data-stu-id="efd2b-218">Troubleshooting the App</span></span>

<span data-ttu-id="efd2b-219">如果未收到包含用于验证凭据的链接的电子邮件：</span><span class="sxs-lookup"><span data-stu-id="efd2b-219">If you don't receive an email containing the link to verify your credentials:</span></span>

- <span data-ttu-id="efd2b-220">检查垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="efd2b-220">Check your junk or spam folder.</span></span>
- <span data-ttu-id="efd2b-221">登录到你的 SendGrid 帐户，并单击 "[电子邮件" 活动链接](https://sendgrid.com/logs/index)。</span><span class="sxs-lookup"><span data-stu-id="efd2b-221">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>
- <span data-ttu-id="efd2b-222">请确保将 SendGrid 用户帐户名用作*web.config 值而不是 SendGrid*帐户电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="efd2b-222">Be certain you used your SendGrid user account name as a *Web.config* value rather than your SendGrid account email address.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="efd2b-223">其他资源</span><span class="sxs-lookup"><span data-stu-id="efd2b-223">Additional Resources</span></span>

- [<span data-ttu-id="efd2b-224">指向 ASP.NET Identity 推荐资源的链接</span><span class="sxs-lookup"><span data-stu-id="efd2b-224">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [<span data-ttu-id="efd2b-225">帐户确认和密码恢复与 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="efd2b-225">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="efd2b-226">ASP.NET Web 窗体教程系列-添加 OAuth 2.0 提供程序</span><span class="sxs-lookup"><span data-stu-id="efd2b-226">ASP.NET Web Forms tutorial series - Add an OAuth 2.0 Provider</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [<span data-ttu-id="efd2b-227">使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="efd2b-227">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [<span data-ttu-id="efd2b-228">ASP.NET Web 窗体教程系列-为项目启用 SSL</span><span class="sxs-lookup"><span data-stu-id="efd2b-228">ASP.NET Web Forms tutorial series - Enable SSL for the Project</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
