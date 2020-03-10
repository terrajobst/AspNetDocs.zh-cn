---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 使用 ASP.NET 网页（Razor）站点中的外部站点登录 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何使用 Facebook、Google、Twitter、Yahoo 和其他站点登录到你的 ASP.NET 网页（Razor）站点—也就是说，如何支持 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518786"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET 网页（Razor）站点中的外部站点登录

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 Facebook、Google、Twitter、Yahoo 和其他站点登录到你的 ASP.NET 网页（Razor）站点—也就是说，如何在站点中支持 OAuth 和 OpenID。
> 
> 学习内容：
> 
> - 当你使用 WebMatrix 入门网站模板时，如何允许来自其他站点的登录。
> 
> 这是本文中介绍的 ASP.NET 功能：
> 
> - `OAuthWebSecurity` 帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 3

ASP.NET 网页包括对[OAuth](http://oauth.net/)和[OpenID](http://openid.net/)提供程序的支持。 使用这些提供程序，你可以让用户使用其现有的 Facebook、Twitter、Microsoft 和 Google 凭据登录到你的站点。 例如，若要使用 Facebook 帐户登录，用户只需选择一个 Facebook 图标，该图标会将其重定向到 Facebook 登录页，用户在其中输入其用户信息。 然后，他们可以将 Facebook 登录名与其在你的站点上的帐户相关联。 网页成员资格功能的相关增强功能是，用户可以将多个登录名（包括来自社交网站的登录名）与网站上的单个帐户关联起来。

此图显示了 "**入门网站**" 模板中的登录页，用户可以在其中选择 Facebook、Twitter、Google 或 Microsoft 图标来启用使用外部帐户登录：

![外部提供程序](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

你可以通过取消注释**入门网站**模板中的几行代码来启用 OAuth 和 OpenID 成员身份。 用于 OAuth 和 OpenID 提供程序的方法和属性位于 `WebMatrix.Security.OAuthWebSecurity` 类中。 "**入门网站**" 模板包括完整的成员身份基础结构、"登录" 页和 "成员资格数据库"，以及让用户使用本地凭据或其他站点中的凭据登录到你的站点所需的所有代码。

本部分举例说明如何允许用户从外部站点登录到基于 "**入门网站**" 模板的站点。 创建入门站点后，可以执行以下操作（详细信息如下）：

- 对于使用 OAuth 提供程序（Facebook、Twitter 和 Microsoft）的站点，请在外部站点上创建应用程序。 这会提供为这些站点调用登录功能所需的应用程序密钥。
- 对于使用 OpenID 提供程序（Google）的站点，无需创建应用程序。 对于所有这些站点，您必须具有一个帐户才能登录和创建开发人员应用程序。

    > [!NOTE]
    > Microsoft 应用程序仅接受工作网站的实时 URL，因此不能使用本地网站 URL 来测试登录名。
- 编辑网站中的一些文件，以便指定适当的身份验证提供程序并将登录名提交到要使用的站点。

本文提供了有关以下任务的单独说明：

- [启用 Google 登录](#To_enable_Google_logins)
- [启用 Facebook 登录](#To_enable_Facebook_logins)
- [启用 Twitter 登录](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>启用 Google 登录

1. 创建或打开基于 WebMatrix 入门网站模板的 ASP.NET 网页站点。
2. 打开 *\_AppStart* "页，取消注释以下代码行。 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>测试 Google login

1. 运行站点的*默认.* # 页，然后选择 "**登录**" 按钮。
2. 在 "*登录*" 页上，在 "**使用其他服务登录**" 部分中，选择 " **Google** " 或 " **Yahoo**提交" 按钮。 此示例使用 Google 登录名。 

    网页将请求重定向到 Google 登录页。

    ![Google 登录](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 输入现有 Google 帐户的凭据。
4. 如果 Google 询问你是否允许*Localhost*使用帐户中的信息，请单击 "**允许**"。

    此代码使用 Google 令牌对用户进行身份验证，然后在你的网站上返回到此页面。 此页面允许用户将其 Google 登录名与网站上的现有帐户关联，或者他们可以在你的站点上注册新帐户以将外部登录名关联。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. 选择 "**关联**" 按钮。 浏览器返回到应用程序的主页。

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>启用 Facebook 登录

1. 如果你尚未登录，请前往[Facebook 开发人员站点](https://developers.facebook.com/apps)（登录）。
2. 选择 "**新建应用**程序" 按钮，然后按照提示命名并创建新的应用程序。
3. 在 "**选择应用将如何与 Facebook 集成**" 部分中，选择 "**网站**" 部分。
4. 在 "**网站 url** " 字段中填入网站的 url （例如 `http://www.example.com`）。 **域**字段是可选的;您可以使用此来为整个域（如*example.com*）提供身份验证。 

    > [!NOTE]
    > 如果你在本地计算机上运行的站点的 URL 如 `http://localhost:12345` （其中数字是本地端口号），则可以将此值添加到用于测试网站的 "**网站 URL** " 字段。 但是，只要本地站点的端口号发生更改，就需要更新应用程序的 "**网站 URL** " 字段。
5. 选择 "**保存更改**" 按钮。
6. 再次选择 "**应用**" 选项卡，然后查看应用程序的起始页。
7. 复制应用程序的应用**ID**和应用**密钥**值，并将其粘贴到临时文本文件中。 你将在网站代码中将这些值传递到 Facebook 提供程序。
8. 退出 Facebook 开发人员网站。

现在，你将更改网站中的两个页面，以便用户能够使用其 Facebook 帐户登录到站点。

1. 创建或打开基于 WebMatrix 入门网站模板的 ASP.NET 网页站点。
2. 打开 *\_AppStart* "页，取消注释 Facebook OAuth 提供程序的代码。 取消注释代码块如下所示： 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. 将 Facebook 应用程序的**应用 ID**值复制为 `appId` 参数的值（在引号内）。
4. 从 Facebook 应用程序中复制**应用程序密钥**值作为 `appSecret` 参数值。
5. 保存并关闭文件。

### <a name="testing-facebook-login"></a>测试 Facebook 登录

1. 运行该站点的 "*默认值*" 页，然后选择 "**登录**" 按钮。
2. 在 "*登录*" 页上，在 "**使用其他服务登录**" 部分中，选择 " **Facebook** " 图标。 

    网页将请求重定向到 Facebook 登录页。

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. 登录到 Facebook 帐户。 

    该代码使用 Facebook 令牌对你进行身份验证，然后返回到一个页面，可在其中将 Facebook 登录名与站点的登录名相关联。 你的用户名或电子邮件地址将填充到表单上的 "**电子邮件**" 字段。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. 选择 "**关联**" 按钮。 

    浏览器返回到主页并且您已登录。

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>启用 Twitter 登录

1. 浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。
2. 选择 "**创建应用程序**" 链接，然后登录到站点。
3. 在 "**创建应用程序**" 窗体中，填写 "**名称**" 和 "**说明**" 字段。
4. 在 "**网站**" 字段中，输入网站的 URL （例如 `http://www.example.com`）。 

    > [!NOTE]
    > 如果要在本地测试网站（使用 `http://localhost:12345`的 URL），Twitter 可能不会接受 URL。 但是，你可以使用本地环回 IP 地址（例如 `http://127.0.0.1:12345`）。 这简化了本地测试应用程序的过程。 但是，每次你的本地站点的端口号发生变化时，你将需要更新应用程序的 "**网站**" 字段。
5. 在 "**回调 URL** " 字段中，输入你希望用户在登录到 Twitter 后返回到的页面 URL。 例如，要将用户发送到起始站点（将识别其登录状态）的主页，请输入你在 "**网站**" 字段中输入的相同 URL。
6. 接受这些条款，然后选择 "**创建 Twitter 应用程序**" 按钮。
7. 在 "**我的应用程序**" 登陆页上，选择您创建的应用程序。
8. 在 "**详细信息**" 选项卡上，滚动到底部，然后选择 "**创建我的访问令牌**" 按钮。
9. 在 "**详细信息**" 选项卡上，复制应用程序的 "**使用者密钥**" 和 "**使用者机密**" 值，并将其粘贴到临时文本文件中。 你将在网站代码中将这些值传递给 Twitter 提供商。
10. 退出 Twitter 站点。

现在，你将更改网站中的两个页面，以便用户能够使用其 Twitter 帐户登录到站点。

1. 创建或打开基于 WebMatrix 入门网站模板的 ASP.NET 网页站点。
2. 打开 *\_AppStart* "页，取消对 Twitter OAuth 提供程序的代码的注释。 取消注释代码块如下所示： 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. 将 Twitter 应用程序的**使用者密钥**值复制为 `consumerKey` 参数的值（在引号内）。
4. 复制 Twitter 应用程序的**使用者机密**值作为 `consumerSecret` 参数的值。
5. 保存并关闭文件。

### <a name="testing-twitter-login"></a>测试 Twitter 登录

1. 运行网站的*默认.* # 页，然后选择 "**登录**" 按钮。
2. 在 "*登录*" 页上，在 "**使用其他服务登录**" 部分中，选择 " **Twitter** " 图标。 

    网页将请求重定向到所创建的应用程序的 Twitter 登录页。

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. 登录到 Twitter 帐户。
4. 此代码使用 Twitter 令牌对用户进行身份验证，并返回到可将登录名与网站帐户关联的页面。 你的姓名或电子邮件地址将填充到表单上的 "**电子邮件**" 字段中。

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. 选择 "**关联**" 按钮。 

    浏览器返回到主页并且您已登录。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [自定义站点范围内的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [将安全性和成员身份添加到 ASP.NET 网页站点](https://go.microsoft.com/fwlink/?LinkID=202904)
