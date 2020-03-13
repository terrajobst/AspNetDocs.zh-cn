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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432818"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>具有 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程介绍如何使用双因素身份验证生成 ASP.NET MVC 5 web 应用。 在继续操作之前，应完成[创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。 可在[此处](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)下载完成的应用程序。 下载内容包含调试帮助程序，可让你在不设置电子邮件或 SMS 提供程序的情况下测试电子邮件确认和短信。
> 
> 本教程由[Rick Anderson](https://blogs.msdn.com/rickAndy) （Twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ）编写。

- [创建 ASP.NET MVC 应用](#createMvc)
- [设置 SMS 以实现双重身份验证](#SMS)
- [启用双因素身份验证](#enable2)
- [其他资源](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>创建 ASP.NET MVC 应用

首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

> [!NOTE]
> 警告：在继续操作之前，应完成[创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。 若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

1. 创建新的 ASP.NET Web 项目，并选择 MVC 模板。 Web 窗体还支持 ASP.NET Identity，因此你可以按照 web 窗体应用程序中的类似步骤进行操作。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 将默认身份验证保留为**单独的用户帐户**。 如果要在 Azure 中托管应用程序，请选中复选框。 稍后在本教程中，我们将部署到 Azure。 可以[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
3. 将[项目设置为使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a>设置 SMS 以实现双重身份验证

本教程提供了使用 Twilio 或 ASPSMS 的说明，但你可以使用任何其他 SMS 提供程序。

1. **使用 SMS 提供程序创建用户帐户**  
  
   创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。
2. **安装其他包或添加服务引用**  
  
   Twilio  
   在“包管理器控制台”中，输入以下命令：  
    `Install-Package Twilio`  
  
   ASPSMS:  
   需要添加以下服务引用：  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   地址:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   命名空间:  
    `ASPSMSX2`
3. **了解 SMS 提供程序用户凭据**  
  
   Twilio  
   在 Twilio 帐户的 "**仪表板**" 选项卡中，复制 "**帐户 SID** " 和 "**身份验证令牌**"。  
  
   ASPSMS:  
   从帐户设置中，导航到**用户密钥**，并将其与自定义**密码**一起复制。  
  
   稍后我们将这些值存储在 web.config*文件中的 `"SMSAccountIdentification"`* 和 `"SMSAccountPassword"`。
4. **指定 SenderID/发起方**  
  
   Twilio  
   从 "**数字**" 选项卡中，复制 Twilio 的电话号码。  
  
   ASPSMS:  
   在 "**解锁**工作项" 菜单中，解锁一个或多个发信方，或选择一个字母数字发信方（并非所有网络都支持）。  
  
   稍后我们*将在 web.config 文件中*将此值存储 `"SMSAccountFrom"`。
5. **将 SMS 提供程序凭据传输到应用中**  
  
   使凭据和发件人电话号码可用于应用。 为了简单起见，我们将这些值存储在 web.config*文件中*。 部署到 Azure 时，可以安全地将值存储在 "网站配置" 选项卡上的 "**应用设置**" 部分。 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > 安全性-永远不要将敏感数据存储在源代码中。 帐户和凭据将添加到上面的代码中，以使示例简单。 请参阅[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
6. **将数据传输到 SMS 提供程序**  
  
   在*应用\_Start\IdentityConfig.cs*文件中配置 `SmsService` 类。  
  
   根据所使用的 SMS 提供程序，激活 " **Twilio** " 或 " **ASPSMS** " 部分： 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. 更新*Views\Manage\Index.cshtml* Razor 视图：（注意：不要只删除退出代码中的注释，使用下面的代码。）  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. 验证 `ManageController` 中的 `EnableTwoFactorAuthentication` 和 `DisableTwoFactorAuthentication` 操作方法是否具有[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)属性：  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. 运行该应用，然后用之前注册的帐户登录。
10. 单击您的 "用户 ID"，在 `Manage` 控制器中激活 `Index` 操作方法。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. 单击“添加”。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` 操作方法会显示一个对话框，用于输入可接收短信消息的电话号码。

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 几秒钟后，会收到一条包含验证码的短信。 输入并按 "**提交**"。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. "管理" 视图显示已添加的电话号码。

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>启用双因素身份验证

在模板生成的应用中，需要使用 UI 启用双因素身份验证（2FA）。 若要启用2FA，请在导航栏中单击你的用户 ID （电子邮件别名）。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

单击 "启用 2FA"。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

注销，然后重新登录。 如果已启用电子邮件（请参阅[上一个教程](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)），可以为2FA 选择 SMS 或电子邮件。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

此时会显示 "验证代码" 页，您可以在其中输入代码（通过短信或电子邮件）。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

单击 "**记住此浏览器**" 复选框会使你不需要使用2FA 在你选中此复选框时使用的浏览器和设备登录。 只要恶意用户无法访问你的设备，启用2FA 并单击 "记住"，**此浏览器**将为你提供便利的单步密码访问权限，同时仍保留对来自不受信任设备的所有访问的强2FA 保护。 可以在您经常使用任何专用设备上执行此操作。

本教程简要介绍了如何在新的 ASP.NET MVC 应用程序上启用2FA。 本教程[使用 SMS 的双因素身份验证和带 ASP.NET Identity 的电子邮件](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)将详细介绍该示例的代码。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [使用 SMS 和电子邮件的双因素身份验证 ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)详细介绍了双重身份验证
- [指向 ASP.NET Identity 推荐资源的链接](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)更详细地介绍密码恢复和帐户确认。
- [带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程介绍如何使用 Facebook 和 Google OAuth 2 授权编写 ASP.NET MVC 5 应用。 它还说明如何向标识数据库添加其他数据。
- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教程添加 Azure 部署，如何使用角色保护应用，如何使用成员资格 API 添加用户和角色以及其他安全功能。
- [为 OAuth 2 创建 Google 应用并将应用连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [在 Facebook 中创建应用并将应用连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [在项目中设置 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [如何设置C#和 ASP.NET MVC 开发环境](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
