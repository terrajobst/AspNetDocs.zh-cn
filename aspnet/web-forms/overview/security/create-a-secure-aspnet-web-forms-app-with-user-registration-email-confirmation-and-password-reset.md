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
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>创建具有用户注册、电子邮件确认和密码重置功能的安全 ASP.NET Web 窗体应用 (C#)

作者： [Erik Reitan](https://github.com/Erikre)

> 本教程介绍如何使用 ASP.NET Identity 成员身份系统，使用用户注册、电子邮件确认和密码重置构建 ASP.NET Web 窗体应用。 本教程基于 Rick Anderson 的[MVC 教程](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。

## <a name="introduction"></a>简介

本教程将指导你完成使用 Visual Studio 和 ASP.NET 4.5 创建 ASP.NET Web 窗体应用程序所需的步骤，以使用用户注册、电子邮件确认和密码重置创建安全的 Web 窗体应用程序。

### <a name="tutorial-tasks-and-information"></a>教程任务和信息：

- [创建 ASP.NET Web 窗体应用](#createWebForms)
- [挂钩 SendGrid](#SG)
- [登录前需要确认电子邮件](#require)
- [密码恢复和重置](#reset)
- [重新发送电子邮件确认链接](#rsend)
- [应用故障排除](#dbg)
- [其他资源](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>创建 ASP.NET Web 窗体应用

首先，安装并运行[适用于 Web 或 Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 的 [Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 同时安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

> [!NOTE]
> 警告：若要完成本教程，您必须安装[Visual Studio 2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

1. 创建新项目（**文件** -&gt; "**新建项目**"），然后从 "**新建项目**" 对话框中选择 " **ASP.NET Web 应用程序**" 模板和最新 .NET Framework 版本。
2. 在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web 窗体**" 模板。 将默认身份验证保留为**单独的用户帐户**。 如果要在 Azure 中托管应用程序，请选中 "**在云中保留主机**" 复选框。   
 然后单击 **"确定"** 以创建新项目。  
    ![新的 ASP.NET 项目 "对话框](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. 为项目启用安全套接字层（SSL）。 按照[使用 Web 窗体教程系列的入门](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)的为**项目启用 SSL**部分中提供的步骤进行操作。
4. 运行应用程序，单击 "**注册**" 链接并注册新用户。 此时，电子邮件的唯一验证基于[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性，以确保电子邮件地址的格式正确。 你将修改代码来添加电子邮件确认。 关闭浏览器窗口。
5. 在 Visual Studio**服务器资源管理器**中（**查看** -&gt;**服务器资源管理器**），导航到 "**数据 Connections\DefaultConnection\Tables\AspNetUsers**"，右键单击并选择 "**打开表定义**"。 

    下图显示了 `AspNetUsers` 表架构：

    ![AspNetUsers 表架构](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. 在**服务器资源管理器**中，右键单击**AspNetUsers**表并选择 "**显示表数据**"。  
  
    ![AspNetUsers 表数据](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 此时，尚未确认注册用户的电子邮件。
7. 单击该行，然后选择 "删除" 以删除该用户。 你将在下一步中再次添加这封电子邮件，并向电子邮件地址发送一封确认消息。

## <a name="email-confirmation"></a>电子邮件确认

最佳做法是在注册新用户时确认电子邮件，以验证他们是否未模拟其他用户（即，他们尚未注册其他人的电子邮件）。 假设你有讨论论坛，则需要防止 `"bob@cpandl.com"` 注册为 `"joe@contoso.com"`。 如果未确认电子邮件，`"joe@contoso.com"` 可能会从你的应用收到不需要的电子邮件。 假设 Bob 意外注册为 `"bib@cpandl.com"` 并且未注意到，他无法使用密码恢复，因为该应用没有正确的电子邮件。 电子邮件确认仅提供对 bot 的有限保护，不会为确定的垃圾邮件提供保护。

通常，你希望在用户通过电子邮件、短信或其他机制确认之前，阻止新用户将任何数据发布到你的网站。 在下面的部分中，我们将启用电子邮件确认并修改代码，以防止新注册的用户登录，直到他们的电子邮件经过确认。 你将在本教程中使用电子邮件服务 SendGrid。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>挂钩 SendGrid

由于本教程已编写，SendGrid 已更改了 API。 有关最新的 SendGrid 说明，请参阅[SendGrid](http://sendgrid.com/)或[启用帐户确认和密码恢复](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)。

虽然本教程仅介绍了如何通过[SendGrid](http://sendgrid.com/)添加电子邮件通知，但你可以使用 SMTP 和其他机制发送电子邮件（请参阅[其他资源](#addRes)）。

1. 在 Visual Studio 中，打开**程序包管理器控制台**（"**工具**" -&gt; **NuGet 包**管理器 " -&gt;**包管理器控制台**"），然后输入以下命令：  
    `Install-Package SendGrid`
2. 请参阅[Azure SendGrid 注册页](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)并注册免费的 SendGrid 帐户。 你还可以直接在[SendGrid 的站点](http://www.sendgrid.com)上注册免费的 SendGrid 帐户。
3. 从**解决方案资源管理器**打开*应用\_"开始*" 文件夹中的*IdentityConfig.cs*文件，并将以下突出显示的代码添加到 `EmailService` 类以配置**SendGrid**：

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. 另外，将以下 `using` 语句添加到*IdentityConfig.cs*文件的开头： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. 若要使此示例简单，请将电子邮件服务帐户值存储在*web.config 文件的*`appSettings` 部分。 将以下以黄色突出显示的 XML 添加到项目根目录中的*web.config 文件：*

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > 安全性-永远不要将敏感数据存储在源代码中。 在此示例中，帐户和凭据存储在*web.config 文件的* **appSetting**节中。 在 Azure 上，您可以安全地存储这些值在 **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。 相关信息，请参阅 Rick Anderson 的主题，其标题为[将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](https://go.microsoft.com/fwlink/?LinkId=513141)。
6. 添加电子邮件服务值以反映 SendGrid 的身份验证值（用户名和密码），以便可以成功地从应用发送电子邮件。 请确保使用你的 SendGrid 帐户名称，而不是 SendGrid 提供的电子邮件地址。

### <a name="enable-email-confirmation"></a>启用电子邮件确认

 若要启用电子邮件确认，你将使用以下步骤修改注册代码。  

1. 在*帐户*文件夹中，打开*Register.aspx.cs*代码隐藏并更新 `CreateUser_Click` 方法，以启用以下突出显示的更改： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. 在**解决方案资源管理器**中，右键单击 " *default.aspx* "，然后选择 "**设为起始页**"。
3. 按 F5 运行应用 **。** 显示该页后，单击 "**注册**" 链接以显示 "注册" 页。
4. 输入你的电子邮件和密码，然后单击 "**注册**" 按钮，通过 SendGrid 发送电子邮件。  
   项目和代码的当前状态将允许用户在完成注册表单后登录，即使他们没有确认其帐户也是如此。
5. 检查你的电子邮件帐户，并单击链接以确认你的电子邮件。  
   提交注册表单后，你将登录。  
    ![示例网站-登录](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>登录前需要确认电子邮件

尽管已确认电子邮件帐户，但此时无需单击验证电子邮件中包含的链接即可完全登录。 在下一节中，你将修改需要新用户在登录之前获得确认电子邮件的代码（经过身份验证）。

1. 在 Visual Studio**解决方案资源管理器**中，在 "*帐户*" 文件夹中包含的*Register.aspx.cs*代码隐藏中更新 `CreateUser_Click` 事件，其中包含以下突出显示的更改： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. 在*Login.aspx.cs*代码隐藏中更新 `LogIn` 方法，并提供以下突出显示的更改： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>运行应用程序

 现在，你已实现代码以检查是否已确认用户的电子邮件地址，你可以在 "**注册**" 和 "**登录**" 页上检查该功能。 

1. 删除**AspNetUsers**表中包含要测试的电子邮件别名的所有帐户。
2. 运行应用（**F5**）并验证你在确认电子邮件地址之前无法以用户身份注册。
3. 在通过刚刚发送的电子邮件确认新帐户之前，请尝试用新帐户登录。  
 你将看到你无法登录，并且你必须有已确认的电子邮件帐户。
4. 确认电子邮件地址后，登录到该应用。

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>密码恢复和重置

1. 在 Visual Studio 中，从*帐户*文件夹所包含的*Forgot.aspx.cs*代码隐藏中的 `Forgot` 方法中删除注释字符，使该方法如下所示： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. 打开 "*登录 .aspx* " 页。 将标记替换到**loginForm**节末尾附近，如下所示： 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. 打开*Login.aspx.cs*代码隐藏，取消注释 `Page_Load` 事件处理程序中以黄色突出显示的以下代码行： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. 按 F5 运行应用 **。** 显示该页后，单击 "**登录**" 链接。
5. 单击 "**忘记了密码？"** 链接以显示 "**忘记密码**" 页面。
6. 输入你的电子邮件地址，然后单击 "**提交**" 按钮，将电子邮件发送到你的地址，以便你可以重置密码。   
   检查电子邮件帐户，并单击链接以显示 "**重置密码**" 页。
7. 在 "**重置密码**" 页上，输入你的电子邮件、密码和确认密码。 然后，按 "**重置**" 按钮。  
   成功重置密码后，将显示 "**更改密码**" 页。 现在可以用新密码登录。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>重新发送电子邮件确认链接

用户创建新的本地帐户后，会通过电子邮件发送确认链接，用户在登录之前需要使用这些帐户。 如果用户意外删除了确认电子邮件，或电子邮件永不送达，则他们将需要再次发送确认链接。 下面的代码更改显示了如何启用此操作。

1. 在 Visual Studio 中，打开**Login.aspx.cs**代码隐藏，并在 `LogIn` 事件处理程序之后添加以下事件处理程序：   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. 通过更改黄色突出显示的代码，在*Login.aspx.cs*代码隐藏中修改 `LogIn` 事件处理程序，如下所示： 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. 通过添加黄色突出显示的代码来更新*登录 .aspx*页，如下所示： 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. 删除**AspNetUsers**表中包含要测试的电子邮件别名的所有帐户。
5. 运行应用（**F5**）并注册电子邮件地址。
6. 在通过刚刚发送的电子邮件确认新帐户之前，请尝试用新帐户登录。  
   你将看到你无法登录，并且你必须有已确认的电子邮件帐户。 此外，你现在可以将确认消息重新发送到你的电子邮件帐户。
7. 输入你的电子邮件地址和密码，然后按 "**重新发送确认**" 按钮。
8. 根据新发送的电子邮件确认电子邮件地址后，登录到该应用。

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>应用故障排除

如果未收到包含用于验证凭据的链接的电子邮件：

- 检查垃圾邮件文件夹。
- 登录到你的 SendGrid 帐户，并单击 "[电子邮件" 活动链接](https://sendgrid.com/logs/index)。
- 请确保将 SendGrid 用户帐户名用作*web.config 值而不是 SendGrid*帐户电子邮件地址。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [指向 ASP.NET Identity 推荐资源的链接](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Web 窗体教程系列-添加 OAuth 2.0 提供程序](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web 窗体教程系列-为项目启用 SSL](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
