---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: 使用 SMS 双因素身份验证创建 ASP.NET Web 窗体应用（C#） |Microsoft Docs
author: Erikre
description: 本教程介绍如何生成具有双因素身份验证的 ASP.NET Web 窗体应用。 本教程旨在补充标题为 Cr 的教程 。
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455978"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>创建具有 SMS 双因素身份验证功能的 ASP.NET Web 窗体应用 (C#)

作者： [Erik Reitan](https://github.com/Erikre)

[下载具有电子邮件和 SMS 双因素身份验证的 ASP.NET Web 窗体应用](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> 本教程介绍如何生成具有双因素身份验证的 ASP.NET Web 窗体应用。 本教程旨在补充标题为 "[创建包含用户注册的安全 ASP.NET Web 窗体应用程序"、电子邮件确认和密码重置](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)的教程。 此外，本教程基于 Rick Anderson 的[MVC 教程](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。

## <a name="introduction"></a>简介

本教程将指导你完成使用 Visual Studio 创建支持双因素身份验证的 ASP.NET Web 窗体应用程序所需的步骤。 双重身份验证是一种额外的用户身份验证步骤。 此额外步骤会在登录过程中生成唯一的个人标识号（PIN）。 PIN 通常以电子邮件或短信形式发送给用户。 然后，你的应用程序的用户会在登录时输入 PIN 作为额外的身份验证度量值。

### <a name="tutorial-tasks-and-information"></a>教程任务和信息：

- [创建 ASP.NET Web 窗体应用](#createWebForms)
- [设置 SMS 和双因素身份验证](#SMS)
- [为注册用户启用双因素身份验证](#use2FA)
- [其他资源](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>创建 ASP.NET Web 窗体应用

首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 同时安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。 此外，还需要创建[Twilio](https://www.twilio.com/try-twilio)帐户，如下所述。

> [!NOTE]
> 重要提示：若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

1. 创建新项目（**文件** -&gt; "**新建项目**"），然后在 "**新建项目**" 对话框中选择 " **ASP.NET Web 应用程序**" 模板以及 .NET Framework 版本的4.5.2。
2. 在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web 窗体**" 模板。 将默认身份验证保留为**单独的用户帐户**。 然后单击 **"确定"** 以创建新项目。  
    ![新的 ASP.NET 项目 "对话框](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. 为项目启用安全套接字层（SSL）。 按照[使用 Web 窗体教程系列的入门](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)的为**项目启用 SSL**部分中提供的步骤进行操作。
4. 在 Visual Studio 中，打开**程序包管理器控制台**（"**工具**" -&gt; **NuGet 包**管理器 " -&gt;**包管理器控制台**"），然后输入以下命令：  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>设置 SMS 和双因素身份验证

本教程使用 Twilio，但你可以使用任何 SMS 提供程序。

1. 创建[Twilio](https://www.twilio.com/try-twilio)帐户。
2. 在 Twilio 帐户的 "**仪表板**" 选项卡中，复制 "**帐户 SID** " 和 "**身份验证令牌"。** 稍后会将它们添加到应用。
3. 在 "**数字**" 选项卡上，也复制 Twilio 的**电话号码**。
4. 使应用程序可以使用 Twilio**帐户 SID**、**身份验证令牌**和**电话号码**。 为了简单起见，将这些值存储在*web.config 文件中。* 部署到 Azure 时，可以在 "网站配置" 选项卡上的 " **appSettings** " 部分中安全地存储这些值。另外，在添加电话号码时，只使用数字。   
   请注意，您还可以添加 SendGrid 凭据。 SendGrid 是一种电子邮件通知服务。 有关如何启用 SendGrid 的详细信息，请参阅教程[使用用户注册创建安全 ASP.NET Web 窗体应用、电子邮件确认和密码重置](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)的教程中的 "挂钩 SendGrid" 部分。

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > 安全性-永远不要将敏感数据存储在源代码中。 在此示例中，帐户和凭据存储在*web.config 文件的* **appSettings**节中。 在 Azure 上，您可以安全地存储这些值在 **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。 相关信息，请参阅 Rick Anderson 的主题，其中标题为[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。
5. 通过使以下修改突出显示为黄色，在应用中配置 `SmsService` 类 *\_Start\IdentityConfig.cs*文件： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. 将以下 `using` 语句添加到*IdentityConfig.cs*文件的开头： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. 通过删除黄色突出显示的行来更新*帐户/管理 .aspx*文件：  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. 在*Manage.aspx.cs*代码隐藏的 `Page_Load` 处理程序中，取消注释以黄色突出显示的代码行，使其如下所示： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. 在*帐户*/*TwoFactorAuthenticationSignIn.aspx.cs*的代码隐藏中，通过添加以下用黄色突出显示的代码来更新 `Page_Load` 处理程序： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   通过进行上述代码更改，包含身份验证选项的 "提供程序" DropDownList 不会重置为第一个值。 这样，用户就可以在进行身份验证时成功选择要使用的所有选项，而不仅仅是第一个选项。
10. 在**解决方案资源管理器**中，右键单击 " *default.aspx* "，然后选择 "**设为起始页**"。
11. 通过测试应用程序，首先构建应用（按**Ctrl**+**Shift**+**B**），然后运行应用（**F5**），并选择 "**注册**" 以创建新的用户帐户，或者选择 "注册" 以创建新的用户帐户，或者如果用户帐户已注册，则选择 "**登录**"。
12. （作为用户）登录后，单击导航栏中的 "用户 ID" （电子邮件地址），以显示 "**管理帐户**" 页（管理 .aspx）。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. 单击 "**管理帐户**" 页上的 "**电话号码**" 旁边的 "**添加**"。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. 添加你（用户）要接收短信（短信）的电话号码，然后单击 "**提交**" 按钮。   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    此时，应用将*使用 web.config 中*的凭据联系 Twilio。 将向与用户帐户关联的电话发送一条短信（短信）。 可以通过查看 Twilio 仪表板来验证 Twilio 消息是否已发送。
15. 几秒钟后，与用户帐户关联的电话将获取包含验证码的短信。 输入验证码，并按 "**提交**"。  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>为注册用户启用双因素身份验证

此时，已为应用启用了双因素身份验证。 要使用户使用双因素身份验证，只需使用 UI 即可更改其设置。 

1. 作为你的应用程序的用户，你可以通过单击导航栏中的用户 ID （电子邮件别名）来显示 "**管理帐户**" 页，为你的特定帐户启用双重身份验证。然后单击 "**启用**" 链接，为该帐户启用双重身份验证。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. 注销，然后重新登录。 如果已启用电子邮件，则可以选择 "SMS" 或 "电子邮件" 以进行双因素身份验证。 如果尚未启用电子邮件，请参阅标题为 "[使用用户注册创建安全 ASP.NET Web 窗体应用程序" 的教程、电子邮件确认和密码重置](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. 此时将显示 "双因素身份验证" 页，您可以在其中输入代码（来自短信或电子邮件）。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 单击 "**记住此浏览器**" 复选框将使你不需要使用双因素身份验证，以便在使用所选的浏览器和设备时进行登录。 如果恶意用户无法访问你的设备，则启用双因素身份验证，并单击 "**记住此浏览器**" 将为你提供方便的单步密码访问，同时仍然保留强双因素身份验证保护，以确保不受信任的设备的所有访问。 可以在您经常使用任何专用设备上执行此操作。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [使用 SMS 和 ASP.NET 标识的双因素身份验证](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [指向 ASP.NET Identity 推荐资源的链接](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web 窗体教程系列-添加 OAuth 2.0 提供程序](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web 窗体教程系列-为项目启用 SSL](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [在 Facebook 中创建应用并将应用连接到项目](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
