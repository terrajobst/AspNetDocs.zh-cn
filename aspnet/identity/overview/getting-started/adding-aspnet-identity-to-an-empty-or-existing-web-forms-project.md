---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: 将 ASP.NET Identity 添加到空白或现有 Web 窗体项目-ASP.NET 4。x
author: raquelsa
description: 本教程介绍如何将 ASP.NET Identity （ASP.NET 的成员资格系统）添加到 ASP.NET 应用程序。 创建新的 Web 窗体或 MVC 时 。
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471974"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>向空的或现有的 Web 窗体项目添加 ASP.NET Identity

> 本教程介绍如何将[ASP.NET Identity](introduction-to-aspnet-identity.md) （ASP.NET 的新成员资格系统）添加到 ASP.NET 应用程序。
> 
> 当你在 Visual Studio 2017 RTM 中使用个人帐户创建新的 Web 窗体或 MVC 项目时，Visual Studio 将安装所有必需的包，并为你添加所有必要的类。 本教程将演示将 ASP.NET Identity 支持添加到现有 Web 窗体项目或新的空项目的步骤。 我将概述所有需要安装的 NuGet 包以及需要添加的类。 我将浏览用于注册新用户和登录的示例 Web 窗体，同时突出显示用于用户管理和身份验证的所有主入口点 Api。 此示例将使用基于实体框架生成的 SQL 数据存储 ASP.NET Identity 默认实现。 本教程将为 SQL 数据库使用 LocalDB。
> 

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity 入门

1. 首先，安装并运行[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。
2. 从起始页中选择 "**新建项目**"，或者可以使用菜单并依次选择 "**文件**" 和 "**新建项目**"。
3. 在左侧窗格中，展开 **" C#视觉对象**"，选择 " **web**"，然后选择 " **ASP.NET web 应用程序（.net Framework）** "。 将项目命名为 "WebFormsIdentity"，然后选择 **"确定**"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. 在 "**新建 ASP.NET 项目**" 对话框中，选择 "**空**" 模板。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   请注意，"**更改身份验证**" 按钮已禁用，且此模板中未提供任何身份验证支持。 利用 Web 窗体、MVC 和 Web API 模板，你可以选择身份验证方法。

## <a name="add-identity-packages-to-your-app"></a>向应用程序添加标识包

在解决方案资源管理器中，右键单击项目并选择 "**管理 NuGet 包**"。 搜索并安装 " **EntityFramework** " 包。 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
请注意，此包将安装依赖项包： **EntityFramework**和**Microsoft ASP.NET 标识核心**。

## <a name="add-a-web-form-to-register-users"></a>添加 web 窗体以注册用户

1. 在**解决方案资源管理器**中，右键单击项目并选择 "**添加**"，然后选择 " **Web 窗体**"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. 在 "**指定项目的名称**" 对话框中，将新的 web 窗体命名为**Register**，然后选择 **"确定"**
3. 将生成的*Register .aspx*文件中的标记替换为以下代码。 代码所作更改为突出显示状态。 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > 这只是在创建新的 ASP.NET Web 窗体项目时所创建的*Register .aspx*文件的简化版本。 上面的标记将添加窗体字段和用于注册新用户的按钮。
4. 打开*Register.aspx.cs*文件，并将该文件的内容替换为以下代码：

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. 上面的代码是在创建新的 ASP.NET Web 窗体项目时创建的*Register.aspx.cs*文件的简化版本。
    > 2. *IdentityUser*类是*IUser*接口的默认 EntityFramework 实现。 *IUser*接口是 ASP.NET Identity 核心上用户的最小界面。
    > 3. *UserStore*类是用户存储的默认 EntityFramework 实现。 此类实现 ASP.NET Identity 核心的最小接口： *IUserStore*、 *IUserLoginStore*、 *IUserClaimStore*和*IUserRoleStore*。
    > 4. *UserManager*类公开用户相关的 api，这些 api 会自动将更改保存到*UserStore*。
    > 5. *IdentityResult*类表示标识操作的结果。
5. 在**解决方案资源管理器**中，右键单击项目并选择 "**添加**"，**添加 "ASP.NET" 文件夹**，然后单击 "**应用\_数据**"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. 打开 web.config*文件，* 并添加用于存储用户信息的数据库的连接字符串项。 将在运行时通过 EntityFramework 为标识实体创建数据库。 在创建新的 Web 窗体项目时，连接字符串类似于创建的字符串。 突出显示的代码显示了应添加的标记：

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > 对于 Visual Studio 2015 或更高版本，请在连接字符串中将 `(localdb)\v11.0` 替换为 `(localdb)\MSSQLLocalDB`。
    
7. 右键单击项目中的 *"文件"* ，然后选择 "**设为起始页**"。 按 Ctrl + F5 生成并运行 web 应用程序。 输入新用户名和密码，然后选择 "**注册**"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity 支持验证，在此示例中，你可以验证来自标识核心包的用户和密码验证程序的默认行为。 用户（`UserValidator`）的默认验证程序具有属性 `AllowOnlyAlphanumericUserNames`，其默认值设置为 "`true`"。 密码（`MinimumLengthValidator`）的默认验证程序确保密码至少包含6个字符。 这些验证程序是 `UserManager` 上的属性，如果要进行自定义验证，则可以重写这些属性。

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>验证 LocalDb 标识数据库和生成的表实体框架

1. 在 "**视图**" 菜单中，选择**服务器资源管理器**。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. 展开**DefaultConnection （WebFormsIdentity）** ，展开 "**表**"，右键单击**AspNetUsers** ，然后选择 "**显示表数据**"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>配置应用程序进行 OWIN 身份验证

此时，我们仅添加了对创建用户的支持。 现在，我们将演示如何添加身份验证来登录用户。 ASP.NET Identity 使用 Microsoft OWIN Authentication 中间件进行窗体身份验证。 OWIN Cookie 身份验证是一个 cookie 和基于声明的身份验证机制，可由[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)或 IIS 上托管的任何框架使用。 使用此模型时，可以跨多个框架（包括 ASP.NET MVC 和 Web 窗体）使用相同的身份验证包。 有关 project Katana 以及如何在主机中运行中间件的详细信息，请参阅[使用 Katana 项目入门](https://msdn.microsoft.com/magazine/dn451439.aspx)。

## <a name="install-authentication-packages-to-your-application"></a>将身份验证包安装到应用程序

1. 在解决方案资源管理器中，右键单击项目并选择 "**管理 NuGet 包**"。 搜索并安装 " ***Owin*** " 包。 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. 搜索并安装 Owin. ***SystemWeb***包。

    > [!NOTE]
    > **Owin**包包含一组 Owin 扩展类，以管理和配置要 ASP.NET Identity 核心包使用的 Owin 身份验证中间件。
    > **Owin**包包含 Owin 服务器，该服务器允许基于 Owin 的应用程序使用 ASP.NET 请求管道在 IIS 上运行。 有关详细信息，请参阅[IIS 集成管道中的 OWIN 中间件](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)。

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>添加 OWIN 启动和身份验证配置类

1. 在**解决方案资源管理器**中，右键单击项目，选择 "**添加**"，然后单击 "**添加新项**"。 在 "搜索文本框" 对话框中，键入 "*owin*"。 将类命名为 "*Startup*" 并选择 "**添加**"。 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. 在 Startup.cs 文件中，添加以下突出显示的代码以配置 OWIN cookie 身份验证。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > 此类包含用于指定 OWIN startup 类的 `OwinStartup` 特性。 每个 OWIN 应用程序都有一个 startup 类，您可以在其中为应用程序管道指定组件。 有关此模型的详细信息，请参阅[OWIN Startup Class 检测](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md)。

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>添加 web 窗体以便在用户注册和登录

1. 打开*Register.aspx.cs*文件，并添加以下代码，以便在注册成功时登录用户。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - 由于 ASP.NET Identity 和 OWIN Cookie 身份验证是基于声明的系统，因此框架要求应用开发人员为用户生成[ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) 。 ClaimsIdentity 包含用户的所有声明的相关信息，例如用户所属的角色。 你还可以在此阶段为用户添加更多声明。
    > - 你可以使用 OWIN 中的 AuthenticationManager 并调用 `SignIn` 并传入 ClaimsIdentity，如上文所示）登录用户。 此代码还将登录用户并生成 cookie。 此调用类似于[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模块使用的[FormAuthentication。](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx)
2. 在**解决方案资源管理器**中，右键单击项目，选择 "**添加**"，然后选择 " **Web 窗体**"。 将 web 窗体命名为**Login**。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. 将该*登录 .aspx*文件的内容替换为以下代码：

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. 将*Login.aspx.cs*文件的内容替换为以下内容：

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` 现在会检查当前用户的状态，并根据其 `Context.User.Identity.IsAuthenticated` 状态采取措施。
    >   **显示登录的用户名**： Microsoft ASP.NET 标识框架已在[IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)上添加了扩展方法，该方法允许你获取已登录用户的 `UserName` 和 `UserId`。 这些扩展方法是在 `Microsoft.AspNet.Identity.Core` 程序集中定义的。 这些扩展方法是[HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)的替代方法。
    > - 登录方法： `This` 方法替换此示例中以前的 `CreateUser_Click` 方法，并在成功创建用户后登录用户。   
    >   Microsoft OWIN Framework 已在 `System.Web.HttpContext` 上添加了扩展方法，使你可以获取对 `IOwinContext`的引用。 这些扩展方法是在 `Microsoft.Owin.Host.SystemWeb` 程序集中定义的。 `OwinContext` 类公开了一个 `IAuthenticationManager` 属性，该属性表示当前请求上可用的身份验证中间件功能。 您可以使用 OWIN 中的 `AuthenticationManager`，然后调用 `SignIn` 并传入 `ClaimsIdentity`，如上所示。 由于 ASP.NET Identity 和 OWIN Cookie 身份验证是基于声明的系统，因此框架要求该应用为用户生成 `ClaimsIdentity`。 `ClaimsIdentity` 包含有关用户的所有声明的信息，例如用户所属的角色。 你还可以在此阶段为用户添加更多声明。此代码将登录用户并生成 cookie。 此调用类似于[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模块使用的[FormAuthentication。](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx)
    > - `SignOut` 方法：从 OWIN 获取对 `AuthenticationManager` 的引用，并调用 `SignOut`。 这类似于[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模块使用的[FormsAuthentication. SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)方法。
5. 按**Ctrl + F5**生成并运行 web 应用程序。 输入新用户名和密码，然后选择 "**注册**"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   注意：此时，将创建新用户并登录。
6. 选择 "**注销**" 按钮。 你将被重定向到登录窗体。
7. 输入无效的用户名或密码，然后选择 "**登录**" 按钮。 
   `UserManager.Find` 方法将返回 null，并将显示错误消息： "*用户名或密码无效*"。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
