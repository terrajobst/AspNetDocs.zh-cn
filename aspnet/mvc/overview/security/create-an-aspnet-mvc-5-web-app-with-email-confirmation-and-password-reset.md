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
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>创建具有登录、电子邮件确认和密码重置功能的安全 ASP.NET MVC 5 Web 应用 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

本教程演示如何使用 ASP.NET Identity 成员身份系统通过电子邮件确认和密码重置生成 ASP.NET MVC 5 web 应用。

有关本教程中使用 .NET Core 的更新版本，请参阅[ASP.NET Core 中的帐户确认和密码恢复](/aspnet/core/security/authentication/accconfirm)。

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>创建 ASP.NET MVC 应用

首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

> [!NOTE]
> 警告：若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

1. 创建新的 ASP.NET Web 项目，并选择 MVC 模板。 Web 窗体还支持 ASP.NET Identity，因此你可以按照 web 窗体应用程序中的类似步骤进行操作。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 将默认身份验证保留为**单独的用户帐户**。 如果要在 Azure 中托管应用程序，请选中复选框。 稍后在本教程中，我们将部署到 Azure。 可以[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
3. 将[项目设置为使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. 运行应用程序，单击 "**注册**" 链接并注册用户。 此时，电子邮件的唯一验证是带有[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性。
5. 在服务器资源管理器中，导航到 "**数据 Connections\DefaultConnection\Tables\AspNetUsers**"，右键单击并选择 "**打开表定义**"。

    下图显示了 `AspNetUsers` 架构：

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. 右键单击**AspNetUsers**表，然后选择 "**显示表数据**"。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 此时，尚未确认电子邮件。
7. 单击该行，然后选择 "删除"。 你将在下一步中再次添加这封电子邮件，并发送一封确认电子邮件。

## <a name="email-confirmation"></a>电子邮件确认

最佳做法是确认新用户注册的电子邮件，以验证他们是否未模拟其他用户（即，他们未注册其他人的电子邮件）。 假设你有讨论论坛，则需要防止 `"bob@example.com"` 注册为 `"joe@contoso.com"`。 如果未确认电子邮件，`"joe@contoso.com"` 可能会从你的应用收到不需要的电子邮件。 假设 Bob 意外注册为 `"bib@example.com"` 并且未注意到，他无法使用密码恢复，因为该应用没有正确的电子邮件。 电子邮件确认仅提供对 bot 的有限保护，不提供对已确定垃圾邮件发送者的保护，它们具有可用于注册的许多工作电子邮件别名。

通常，在通过电子邮件、短信或其他机制确认新用户之前，要阻止新用户将任何数据发布到您的网站。 <a id="build"></a>在下面的部分中，我们将启用电子邮件确认并修改代码，以防止新注册的用户登录，直到他们的电子邮件经过确认。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>挂钩 SendGrid

本部分中的说明不是最新的。 有关更新的说明，请参阅[配置 SendGrid 电子邮件提供程序](/aspnet/core/security/authentication/accconfirm#configure-email-provider)。

虽然本教程仅介绍了如何通过[SendGrid](http://sendgrid.com/)添加电子邮件通知，但你可以使用 SMTP 和其他机制发送电子邮件（请参阅[其他资源](#addRes)）。

1. 在“包管理器控制台”中，输入以下命令： 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. 请参阅[Azure SendGrid 注册页](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)并注册免费的 SendGrid 帐户。 通过在*App_Start/identityconfig.cs*中添加类似于以下内容的代码来配置 SendGrid：

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

需要添加以下内容：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

为了简单起见，我们将应用程序设置*存储在 web.config 文件中*：

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> 安全性-永远不要将敏感数据存储在源代码中。 帐户和凭据存储在 appSetting 中。 在 Azure 上，您可以安全地存储这些值在 **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。 请参阅[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。

### <a name="enable-email-confirmation-in-the-account-controller"></a>在帐户控制器中启用电子邮件确认

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

验证*Views\Account\ConfirmEmail.cshtml*文件的 razor 语法是否正确。 （第一行中的 @ 字符可能已丢失。 )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

运行应用并单击 "注册" 链接。 提交注册表单后，即已登录。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

检查你的电子邮件帐户，并单击链接以确认你的电子邮件。

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>登录前需要确认电子邮件

当前用户完成注册表单后，用户将登录。 通常需要确认其电子邮件，然后才能将其记录在日志中。 在下面的部分中，我们将修改代码，要求新用户在登录之前获得确认电子邮件（经过身份验证）。 用以下突出显示的更改更新 `HttpPost Register` 方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

通过注释掉 `SignInAsync` 方法，注册不会登录用户。 `TempData["ViewBagLink"] = callbackUrl;` 行可用于[调试应用](#dbg)并测试注册，而无需发送电子邮件。 `ViewBag.Message` 用于显示确认说明。 [下载示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)包含的代码可用于测试电子邮件确认，而无需设置电子邮件，也可用于调试应用程序。

创建 `Views\Shared\Info.cshtml` 文件，并添加以下 razor 标记：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

将[授权属性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)添加到主控制器的 `Contact` 操作方法。 您可以单击 "**联系人**" 链接来验证匿名用户无权访问和经过身份验证的用户是否具有访问权限。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

还必须更新 `HttpPost Login` 操作方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

更新*Views\Shared\Error.cshtml*视图以显示错误消息：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

删除**AspNetUsers**表中的所有帐户，其中包含要测试的电子邮件别名。 运行应用并验证你是否无法登录，直到你确认电子邮件地址。 确认电子邮件地址后，单击 "**联系人**" 链接。

<a id="reset"></a>
## <a name="password-recoveryreset"></a>密码恢复/重置

从帐户控制器的 `HttpPost ForgotPassword` 操作方法中删除注释字符：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

从*Views\Account\Login.cshtml* razor 视图文件的 "`ForgotPassword` [html.actionlink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) " 中删除注释字符：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

"登录" 页现在将显示用于重置密码的链接。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>重新发送电子邮件确认链接

用户创建新的本地帐户后，会通过电子邮件发送确认链接，用户在登录之前需要使用这些帐户。 如果用户意外删除了确认电子邮件，或电子邮件永不送达，则他们将需要再次发送确认链接。 下面的代码更改显示了如何启用此操作。

将以下帮助器方法添加到*Controllers\AccountController.cs*文件的底部：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

更新 Register 方法以使用新帮助器：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

如果尚未确认用户帐户，请更新 Login 方法以重新发送密码：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>合并社会和本地登录帐户

可以通过单击电子邮件链接来合并本地帐户和社交帐户。 在以下序列中， **RickAndMSFT@gmail.com** 首先创建为本地登录名，但你可以先将该帐户创建为社交日志，然后添加本地登录名。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

单击 "**管理**" 链接。 请注意 **外部登录名：0** 与此帐户关联。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

单击 "其他登录服务" 链接，并接受应用请求。 这两个帐户已合并，你将能够使用这两个帐户进行登录。 你可能希望用户在身份验证服务中的社交日志关闭或无法访问其社交帐户时添加本地帐户。

在下图中，Tom 是中的社交登录（可从 **外部登录中查看：1** 显示在页面上）。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

单击 "**选择密码**" 可添加与同一帐户关联的本地日志。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>更深入地确认电子邮件

本主题中的教程[帐户确认和密码恢复 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)将深入了解更多详细信息。

<a id="dbg"></a>
## <a name="debugging-the-app"></a>调试应用程序

如果未收到包含链接的电子邮件：

- 检查垃圾邮件文件夹。
- 登录到你的 SendGrid 帐户，并单击 "[电子邮件" 活动链接](https://sendgrid.com/logs/index)。

若要在没有电子邮件的情况下测试验证链接，请下载[已完成的示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。 确认链接和确认代码将显示在该页上。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [指向 ASP.NET Identity 推荐资源的链接](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)更详细地介绍密码恢复和帐户确认。
- [带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程介绍如何使用 Facebook 和 Google OAuth 2 授权编写 ASP.NET MVC 5 应用。 它还说明如何向标识数据库添加其他数据。
- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教程添加 Azure 部署，如何使用角色保护应用，如何使用成员资格 API 添加用户和角色以及其他安全功能。
- [为 OAuth 2 创建 Google 应用并将应用连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [在 Facebook 中创建应用并将应用连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [在项目中设置 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
