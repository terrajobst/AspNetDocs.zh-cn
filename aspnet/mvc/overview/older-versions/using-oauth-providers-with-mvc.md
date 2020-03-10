---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: 将 OAuth 提供程序与 MVC 4 一起使用 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何生成一个 ASP.NET MVC 4 web 应用程序，该应用程序允许用户使用来自外部提供程序的凭据（如 Facebo ...）登录。
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433364"
---
# <a name="using-oauth-providers-with-mvc-4"></a>通过 MVC 4 使用 OAuth 提供程序

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何生成一个 ASP.NET MVC 4 web 应用程序，该应用程序允许用户使用来自外部提供程序（如 Facebook、Twitter、Microsoft 或 Google）的凭据登录，然后将这些提供程序中的某些功能集成到你的web 应用程序。 为简单起见，本教程重点介绍如何使用 Facebook 中的凭据。
> 
> 若要在 ASP.NET MVC 5 web 应用程序中使用外部凭据，请参阅使用[Facebook 和 Google OAuth2 创建 ASP.NET MVC 5 应用和 OpenID 登录](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
> 
> 如果在您的网站中启用这些凭据，则会带来明显的优势，因为数百万用户已经拥有了具有这些外部提供商的帐户。 如果用户无需创建和记住一组新凭据，则可能更倾向于注册你的站点。 此外，在用户通过其中一个提供程序登录后，你可以将社交操作纳入提供商。

## <a name="what-youll-build"></a>要生成的内容

在本教程中，主要有两个目标：

1. 允许用户使用 OAuth 提供程序提供的凭据登录。
2. 从提供程序中检索帐户信息，并将该信息与网站的帐户注册集成。

尽管本教程中的示例重点介绍如何使用 Facebook 作为身份验证提供程序，但你可以修改代码以使用任何提供程序。 实现任何提供程序的步骤与你将在本教程中看到的步骤非常类似。 直接调用提供程序的 API 集时，你只会注意到明显差异。

## <a name="prerequisites"></a>系统必备

- Web [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

Or

- Microsoft Visual Studio 2010 SP1 或[Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

此外，本主题假定您具有有关 ASP.NET MVC 和 Visual Studio 的基本知识。 如果需要 ASP.NET MVC 4 简介，请参阅[ASP.NET mvc 4 简介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中，创建一个新的 ASP.NET MVC 4 Web 应用程序，并将其命名为 &quot;OAuthMVC&quot;。 可以为 .NET Framework 4.5 或4。

![创建项目](using-oauth-providers-with-mvc/_static/image1.png)

在 New ASP.NET MVC 4 项目窗口中，选择 " **Internet 应用程序**"，并将**Razor**保留为视图引擎。

![选择 Internet 应用程序](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>启用提供程序

使用 Internet 应用程序模板创建 MVC 4 web 应用程序时，将使用应用\_Start 文件夹中名为 "AuthConfig.cs" 的文件创建该项目。

![AuthConfig 文件](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig 文件包含用于注册外部身份验证提供程序的客户端的代码。 默认情况下，此代码已被注释掉，因此没有启用任何外部提供程序。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

必须取消注释此代码才能使用外部身份验证客户端。 仅取消注释要包含在站点中的提供程序。 对于本教程，将只启用 Facebook 凭据。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

请注意，在上面的示例中，该方法包含用于注册参数的空字符串。 如果现在尝试运行应用程序，应用程序会引发参数异常，因为参数不允许使用空字符串。 若要提供有效值，您必须向外部提供程序注册您的网站，如下一节所示。

## <a name="registering-with-an-external-provider"></a>使用外部提供程序进行注册

若要使用来自外部提供程序的凭据对用户进行身份验证，必须向提供程序注册您的网站。 注册站点时，会收到注册客户端时要包含的参数（如密钥或 id 和机密）。 您必须拥有一个要使用的提供程序的帐户。

本教程不提供使用这些提供程序进行注册所必须执行的全部步骤。 这些步骤通常比较简单。 若要成功注册您的网站，请按照这些网站上提供的说明操作。 若要开始注册您的网站，请查看下列门户的开发人员网站：

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

向 Facebook 注册站点时，可以为站点域提供 &quot;localhost&quot;，并为 URL `&quot; http://localhost/&quot;` 提供 URL，如下图所示。 使用 localhost 适用于大多数提供程序，但目前不适用于 Microsoft 提供商。 对于 Microsoft 提供程序，您必须包含一个有效的网站 URL。

![注册站点](using-oauth-providers-with-mvc/_static/image4.png)

在上图中，已删除应用程序 id、应用程序密钥和联系人电子邮件的值。 当你实际注册站点时，这些值将存在。 你需要记下应用程序 id 和应用程序机密的值，因为你会将它们添加到你的应用程序。

## <a name="creating-test-users"></a>创建测试用户

如果你不介意使用现有 Facebook 帐户来测试网站，则可以跳过此部分。

可以在 Facebook 应用管理页中轻松地为应用程序创建测试用户。 你可以使用这些测试帐户登录到你的站点。 通过单击左侧导航窗格中的 "**角色**" 链接，然后单击 "**创建**" 链接，创建测试用户。

![创建测试用户](using-oauth-providers-with-mvc/_static/image5.png)

Facebook 站点会自动创建你请求的测试帐户数。

## <a name="adding-application-id-and-secret-from-the-provider"></a>从提供程序中添加应用程序 ID 和密码

现在，你已从 Facebook 接收了 id 和机密，请返回到 AuthConfig 文件，并将它们作为参数值添加。 下面显示的值不是实际值。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>用外部凭据登录

这就是在站点中启用外部凭据所必须执行的所有操作。 运行应用程序，并单击右上角的 "登录" 链接。 该模板将自动识别已将 Facebook 注册为提供程序，并包括提供程序的按钮。 如果注册多个提供程序，则会自动包含每个提供程序的按钮。

![外部登录](using-oauth-providers-with-mvc/_static/image6.png)

本教程不介绍如何自定义外部提供程序的 "登录" 按钮。 有关此信息，请参阅[使用 OAuth/OpenID 时自定义登录 UI](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。

单击 "Facebook" 按钮，以 Facebook 凭据登录。 当你选择一个外部提供程序时，你会被重定向到该站点并提示该服务登录。

下图显示了 Facebook 的登录屏幕。 请注意，你正在使用 Facebook 帐户登录到名为 oauthmvcexample 的站点。

![facebook 身份验证](using-oauth-providers-with-mvc/_static/image7.png)

使用 Facebook 凭据登录后，页面将向用户通知网站将有权访问基本信息。

![请求权限](using-oauth-providers-with-mvc/_static/image8.png)

选择 "**转向应用**" 后，用户必须注册该站点。 下图显示了用户使用 Facebook 凭据登录后的注册页面。 通常，用户名以提供者的名称预先填充。

![register](using-oauth-providers-with-mvc/_static/image9.png)

单击 "**注册**" 完成注册。 关闭浏览器。

你可以看到，新帐户已添加到数据库中。 在服务器资源管理器中，打开**DefaultConnection**数据库并打开 "**表**" 文件夹。

![数据库表](using-oauth-providers-with-mvc/_static/image10.png)

右键单击 " **UserProfile** " 表，然后选择 "**显示表数据**"。

![显示数据](using-oauth-providers-with-mvc/_static/image11.png)

你将看到已添加的新帐户。 查看**网页\_OAuthMembership**表中的数据。 你将看到与你刚添加的帐户的外部提供程序相关的更多数据。

如果只想启用外部身份验证，则已完成。 但是，你可以将提供程序中的信息进一步集成到新的用户注册过程中，如以下部分所示。

## <a name="create-models-for-additional-user-information"></a>为其他用户信息创建模型

正如你在前面的部分中所看到的那样，无需检索用于内置帐户注册工作的任何其他信息。 但是，大多数外部提供程序会传回有关用户的其他信息。 以下各节说明如何保留该信息并将其保存到数据库中。 具体来说，您将保留用户的全名、用户个人网页的 URI 以及一个指示 Facebook 是否验证了帐户的值。

您将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)添加用于存储其他用户信息的表。 您要将表添加到现有数据库，因此您首先需要创建当前数据库的快照。 通过创建当前数据库的快照，稍后可以创建只包含新表的迁移。 若要创建当前数据库的快照，请执行以下操作：

1. 打开**包管理器控制台**
2. 运行命令**启用-迁移**
3. 运行命令 "**添加迁移初始– IgnoreChanges** "
4. 运行命令**更新-数据库**

现在，您将添加新属性。 在 "模型" 文件夹中，打开 AccountModels.cs 文件，并找到 RegisterExternalLoginModel 类。 RegisterExternalLoginModel 类包含从身份验证提供程序返回的值。 添加名为 FullName 和 Link 的属性，如下所示。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

同样，在 AccountModels.cs 中，添加一个名为 ExtraUserInformation 的新类。 此类表示将在数据库中创建的新表。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

在 UsersContext 类中，添加以下突出显示的代码，为新类创建 DbSet 属性。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

你现在已准备好创建新表。 再次打开包管理器控制台，这一次：

1. 运行命令**添加迁移 AddExtraUserInformation**
2. 运行命令**更新-数据库**

新表现在存在于数据库中。

## <a name="retrieve-the-additional-data"></a>检索其他数据

可以通过两种方法来检索其他用户数据。 第一种方法是保留默认情况下在身份验证请求期间传递回的用户数据。 第二种方法是专门调用提供程序 API 并请求详细信息。 FullName 和 Link 的值将由 Facebook 自动传回。 一个值，该值指示 Facebook 是否已验证该帐户是通过调用 Facebook API 来检索的。 首先，填充 FullName 和 Link 的值，然后您将获得已验证的值。

若要检索其他用户数据，请打开 "**控制器**" 文件夹中的**AccountController.cs**文件。

此文件包含用于记录、注册和管理帐户的逻辑。 具体而言，请注意称为**ExternalLoginCallback**和**ExternalLoginConfirmation**的方法。 在这些方法中，你可以添加代码，以便为你的应用程序自定义外部登录操作。 **ExternalLoginCallback**方法的第一行包含：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

其他用户数据会传递回**VerifyAuthentication**方法返回的**AuthenticationResult**对象的**ExtraData**属性。 Facebook 客户端在**ExtraData**属性中包含以下值：

- id
- NAME
- 链接
- gender
- accesstoken

其他提供程序在 ExtraData 属性中将具有类似但略有不同的数据。

如果用户是站点的新用户，则将检索某些其他数据并将该数据传递到确认视图。 仅当用户是站点的新用户时，才会运行方法中的最后一个代码块。 替换以下行：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

替换为以下行：

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

此更改仅包含 FullName 和 Link 属性的值。

在**ExternalLoginConfirmation**方法中，按下面突出显示的代码修改代码以保存其他用户信息。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>调整视图

您从提供程序中检索的其他用户数据将显示在 "注册" 页中。

**在/** **帐户**"文件夹中，打开**ExternalLoginConfirmation**。 在 "用户名" 的现有字段下面，为 FullName、Link 和 PictureLink 添加字段。

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

你现在已准备好运行应用程序，并注册了附加信息已保存的新用户。 你必须有一个尚未注册到站点的帐户。 你可以使用不同的测试帐户，也可以删除**UserProfile**和网页中的行， **\_OAuthMembership**表中要重用的帐户。 通过删除这些行，你将确保再次注册该帐户。

运行应用程序并注册新用户。 请注意，这次确认页面包含更多值。

![register](using-oauth-providers-with-mvc/_static/image12.png)

完成注册后，关闭浏览器。 查看数据库中的**ExtraUserInformation**表中的新值。

## <a name="install-nuget-package-for-facebook-api"></a>安装 Facebook API 的 NuGet 包

Facebook 提供了一个[API](https://developers.facebook.com/docs/reference/apis/) ，你可以调用它来执行操作。 你可以通过指示发送 HTTP 请求或使用安装 NuGet 包（有助于发送这些请求）来调用 Facebook API。 本教程演示了如何使用 NuGet 包，但安装 NuGet 包并不重要。 本教程演示如何使用 Facebook C# SDK 包。 还有其他 NuGet 包可帮助调用 Facebook API。

从 "**管理 NuGet 包**" 窗口中，选择C# Facebook SDK 包。

![安装包](using-oauth-providers-with-mvc/_static/image13.png)

你将使用 Facebook C# SDK 调用需要用户访问令牌的操作。 下一节将演示如何获取访问令牌。

## <a name="retrieve-access-token"></a>检索访问令牌

大多数外部提供程序在验证用户凭据后，将返回访问令牌。 此访问令牌非常重要，因为它使你可以调用仅适用于经过身份验证的用户的操作。 因此，当您想要提供更多功能时，检索和存储访问令牌是必不可少的。

根据外部提供程序，访问令牌的有效期仅限一段时间。 若要确保你拥有有效的访问令牌，你将在每次用户登录时检索它，并将其存储为会话值，而不是将其保存到数据库。

在**ExternalLoginCallback**方法中，访问令牌也会在**AuthenticationResult**对象的**ExtraData**属性中传回。 将突出显示的代码添加到**ExternalLoginCallback** ，以将访问令牌保存到**Session**对象中。 每次用户使用 Facebook 帐户登录时，都会运行此代码。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

尽管此示例从 Facebook 检索一个访问令牌，但你可以通过名为 &quot;accesstoken&quot;的同一密钥从任何外部提供商那里检索访问令牌。

## <a name="logging-off"></a>注销

默认的**注销**方法会将用户记录在应用程序之外，但不会将用户从外部提供程序中注销。 若要将用户从 Facebook 注销，并在用户注销后阻止令牌持续，你可以将以下突出显示的代码添加到 AccountController 中的**注销**方法。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

在 `next` 参数中提供的值是用户注销 Facebook 后要使用的 URL。 在本地计算机上进行测试时，应为本地站点提供正确的端口号。 在生产环境中，你将提供一个默认页面，如 contoso.com。

## <a name="retrieve-user-information-that-requires-the-access-token"></a>检索需要访问令牌的用户信息

现在，你已存储访问令牌并安装了 Facebook C# SDK 包，可以将它们一起用于请求 facebook 中的其他用户信息。 在**ExternalLoginConfirmation**方法中，通过传递访问令牌的值来创建**FacebookClient**类的实例。 请求经过身份验证的当前用户的**验证**属性的值。 **验证**的属性指示 Facebook 是否已通过某种其他方式验证了帐户，如将消息发送到手机。 将该值保存在数据库中。

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

您将再次需要为用户删除数据库中的记录，或者使用其他 Facebook 帐户。

运行应用程序，并注册新用户。 查看**ExtraUserInformation**表，查看已验证属性的值。

## <a name="conclusion"></a>结束语

在本教程中，已创建了一个与 Facebook 集成的、用于用户身份验证和注册数据的站点。 已了解为 MVC 4 web 应用程序设置的默认行为，以及如何自定义该默认行为。

## <a name="related-topics"></a>相关主题

- [创建具有身份验证和 SQL 数据库的 ASP.NET MVC 应用程序并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
