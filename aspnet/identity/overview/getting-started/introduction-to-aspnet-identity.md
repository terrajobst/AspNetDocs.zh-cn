---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Identity 简介-ASP.NET 4。x
author: jongalloway
description: ASP.NET 成员资格系统在2005中引入了 ASP.NET 2.0，而且，由于 web 应用程序通常 。
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0268dfc16cd2cfb1e79ee14997a4c5eb247af950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471734"
---
# <a name="introduction-to-aspnet-identity"></a>ASP.NET Identity 简介

> ASP.NET 成员资格系统在2005中引入了 ASP.NET 2.0，因此，web 应用程序通常处理身份验证和授权的方式有很多更改。 当你为 web、手机或平板电脑构建新式应用程序时，ASP.NET Identity 是一种全新的外观。

## <a name="background-membership-in-aspnet"></a>背景： ASP.NET 中的成员身份

### <a name="aspnet-membership"></a>ASP.NET 成员身份

[ASP.NET 成员资格](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx)旨在解决在2005中常见的站点成员身份要求，这些要求涉及到 Forms 身份验证，以及用于用户名、密码和配置文件数据的 SQL Server 数据库。 现在，web 应用程序有一系列更广泛的数据存储选项，大多数开发人员希望使其站点能够使用社交标识提供程序进行身份验证和授权功能。 ASP.NET 成员资格设计的限制使得此转换变得很困难：

- 数据库架构是为 SQL Server 而设计的，不能对其进行更改。 你可以添加配置文件信息，但其他数据将打包到不同的表中，这使得除通过配置提供程序 API 之外的任何方法都难以访问。
- 提供程序系统使你可以更改后备数据存储，但系统围绕适用于关系数据库的假设而设计。 你可以编写一个提供程序来将成员身份信息存储在非关系存储机制（如 Azure 存储表）中，但之后必须通过编写大量代码来解决关系设计，并为不适用于 NoSQL 数据库的方法编写大量 `System.NotImplementedException` 异常。
- 由于登录/注销功能基于 Forms 身份验证，因此成员资格系统不能使用[OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)。 OWIN 包含用于身份验证的中间件组件，包括支持使用外部标识提供者（如 Microsoft 帐户、Facebook、Google、Twitter）的登录和使用本地 Active Directory 中的组织帐户登录Azure Active Directory。 OWIN 还包括对 OAuth 2.0、JWT 和 CORS 的支持。

### <a name="aspnet-simple-membership"></a>ASP.NET 简单成员身份

[ASP.NET 简单成员身份](../../../web-pages/overview/security/16-adding-security-and-membership.md)是作为 ASP.NET 网页的成员资格系统开发的。 它与 WebMatrix 和 Visual Studio 2010 SP1 一起发布。 简单成员资格的目标是便于将成员资格功能添加到网页应用程序中。

简单成员身份使自定义用户配置文件信息变得更加容易，但它仍与 ASP.NET 成员身份共享其他问题，并且存在一些限制：

- 很难将成员身份系统数据保存在非关系存储区中。
- 不能将其与 OWIN 一起使用。
- 它不适用于现有的 ASP.NET 成员资格提供程序，并且不能进行扩展。

### <a name="aspnet-universal-providers"></a>ASP.NET 通用提供程序

开发[ASP.NET 通用提供程序](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)是为了能够在 Microsoft Azure SQL 数据库中保留成员身份信息，它们也适用于 SQL Server Compact。 通用提供程序是在实体框架 Code First 上构建的，这意味着通用提供程序可用于在 EF 支持的任何存储中保存数据。 使用通用提供程序，数据库架构也被清理了很多。

通用提供程序是在 ASP.NET 成员身份基础结构的基础上构建的，因此它们仍具有与 SqlMembership 提供程序相同的限制。 也就是说，它们是为关系数据库而设计的，因此很难自定义配置文件和用户信息。 这些提供程序还会将 Forms 身份验证用于登录和注销功能。

## <a name="aspnet-identity"></a>ASP.NET 标识

随着 ASP.NET 中的成员身份案例的发展，ASP.NET 团队已经从客户的反馈中学到了很多知识。

用户通过输入用户在自己的应用程序中注册的用户名和密码将不再有效。 Web 已变得更社交。 用户通过社交渠道（例如 Facebook、Twitter 和其他社交网站）实时交互。 开发人员希望用户能够使用他们的社交标识登录，使他们能够在他们的网站上获得丰富的体验。 新式成员资格系统必须启用基于重定向的登录才能使用 Facebook、Twitter 和其他身份验证提供程序。

随着 web 开发的发展，web 开发模式也是如此。 应用程序代码的单元测试成为应用程序开发人员的核心问题。 在 2008 ASP.NET 中，基于模型-视图-控制器（MVC）模式添加了一个新的框架，可帮助开发人员生成单元测试 ASP.NET 应用程序。 想要对其应用程序逻辑进行单元测试的开发人员还希望能够通过成员资格系统完成此操作。

考虑到这些更改在 web 应用程序开发中，ASP.NET Identity 是以下列目标来开发的：

- **一 ASP.NET Identity 系统**

    - ASP.NET Identity 可用于所有 ASP.NET 框架，如 ASP.NET MVC、Web 窗体、网页、Web API 和 SignalR。
    - 在构建 web、手机、商店或混合应用程序时，可以使用 ASP.NET Identity。
- **轻松插入有关用户的配置文件数据**

    - 你可以控制用户和配置文件信息的架构。 例如，你可以轻松地让系统存储用户在你的应用程序中注册帐户时输入的出生日期。

- **持久性控件**

    - 默认情况下，ASP.NET Identity 系统在数据库中存储所有用户信息。 ASP.NET Identity 使用实体框架 Code First 实现其所有持久性机制。
    - 由于控制数据库架构，因此更改表名称或更改主键的数据类型等常见任务非常简单。
    - 无需引发 `System.NotImplementedExceptions` 异常，就可以轻松地插入不同的存储机制，如 SharePoint、Azure 存储表服务、NoSQL 数据库等。
- **单元可测试性**

    - ASP.NET Identity 使 web 应用程序可进行多个单元测试。 您可以为应用程序中使用 ASP.NET Identity 的部分编写单元测试。
- **角色提供程序**

    - 角色提供程序可让你按角色限制对应用程序的各个部分的访问。 您可以轻松地创建角色（如 "管理员"），并将用户添加到角色。
- **基于声明**

    - ASP.NET Identity 支持基于声明的身份验证，其中用户的标识表示为一组声明。 声明允许开发人员在描述用户身份时比允许的角色更有意义。 角色成员身份只是一个布尔值（成员或非成员），而声明可以包含有关用户的标识和成员身份的丰富信息。
- **社交登录提供程序**

    - 你可以轻松地将社交登录（例如 Microsoft 帐户、Facebook、Twitter、Google 和其他人）添加到你的应用程序，并将特定于用户的数据存储在应用程序中。

- **OWIN 集成**

    - ASP.NET authentication 现在基于可在任何基于 OWIN 的主机上使用的 OWIN 中间件。 ASP.NET Identity 在 System.web 上没有任何依赖关系。 它是一个完全兼容的 OWIN 框架，可用于任何 OWIN 托管的应用程序。
    - ASP.NET Identity 为网站中的用户登录/注销用户使用 OWIN Authentication。 这意味着，应用程序使用 OWIN CookieAuthentication 来执行此操作，而不是使用 FormsAuthentication 生成 cookie。
- **NuGet 包**

    - ASP.NET Identity 将作为 NuGet 包重新分发，此包安装在 Visual Studio 2017 附带的 ASP.NET MVC、Web 窗体和 Web API 模板中。 你可以从 NuGet 库中下载此 NuGet 包。
    - 以 NuGet 包的形式发布 ASP.NET Identity 使得 ASP.NET 团队能够更轻松地循环访问新功能和 bug 修复，并以灵活的方式将其提供给开发人员。

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity 入门

ASP.NET Identity 用于 ASP.NET MVC、Web 窗体、Web API 和 SPA 的 Visual Studio 2017 项目模板。 在本演练中，我们将演示项目模板如何使用 ASP.NET Identity 添加注册、登录和注销用户的功能。

使用以下过程实现 ASP.NET Identity。 本文的目的是为你概括了解 ASP.NET Identity;您可以逐步执行该操作，也可以仅阅读详细信息。 有关使用 ASP.NET Identity 创建应用的更多详细说明，包括使用新 API 添加用户、角色和配置文件信息，请参阅本文末尾的后续步骤部分。

1. 使用单个帐户创建 ASP.NET MVC 应用程序。 可以使用 ASP.NET MVC、Web Forms、Web API、SignalR 等中的 ASP.NET Identity。在本文中，我们将从 ASP.NET MVC 应用程序开始。  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. 创建的项目包含以下三个用于 ASP.NET Identity 的包。

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   此包具有实体框架的实现 ASP.NET Identity，它将 ASP.NET Identity 数据和架构保存到 SQL Server。
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   此包具有用于 ASP.NET Identity 的核心接口。 此包可用于为面向不同持久性存储（例如 Azure 表存储、NoSQL 数据库等）的 ASP.NET Identity 编写实现。
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   此包包含用于在 ASP.NET 应用程序中插入 OWIN authentication ASP.NET Identity 的功能。 向应用程序添加登录功能并调用 OWIN Cookie 身份验证中间件以生成 cookie 时，将使用此项。
3. 创建用户。  
   启动应用程序，然后单击 "**注册**" 链接以创建用户。 下图显示了收集用户名和密码的 "注册" 页。  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   当用户选择 "**注册**" 按钮时，帐户控制器的 `Register` 操作通过调用 ASP.NET Identity API 创建用户，如下所示：

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. 登录。  
   如果已成功创建用户，则会通过 `SignInAsync` 方法登录。  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]

   `SignInManager.SignInAsync` 方法生成[ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)。 由于 ASP.NET Identity 和 OWIN Cookie 身份验证是基于声明的系统，因此框架要求应用为用户生成 ClaimsIdentity。 ClaimsIdentity 包含用户的所有声明的相关信息，例如用户所属的角色。   
 
5. 注销。  
   选择 "**注销" 链接，** 以便在帐户控制器中调用注销操作。 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   上面突出显示的代码显示了 OWIN `AuthenticationManager.SignOut` 方法。 这类似于 Web 窗体中的[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)模块使用的[FormsAuthentication. SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)方法。

## <a name="components-of-aspnet-identity"></a>ASP.NET Identity 的组件

下图显示了 ASP.NET Identity 系统的组件（在[此](introduction-to-aspnet-identity/_static/image3.png)图上或在关系图上选择要放大的组件）。 绿色包构成了 ASP.NET Identity 系统。 所有其他包都是在 ASP.NET 应用程序中使用 ASP.NET Identity 系统所需的依赖项。

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

下面是前面未提到的 NuGet 包的简要说明：

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 使应用程序可以使用基于 cookie 的身份验证的中间件，类似于 ASP。NET 的窗体身份验证。
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 实体框架是 Microsoft 推荐用于关系数据库的数据访问技术。

## <a name="migrating-from-membership-to-aspnet-identity"></a>从成员身份迁移到 ASP.NET Identity

我们希望立即提供有关将使用 ASP.NET 成员身份或简单成员身份的现有应用迁移到新 ASP.NET Identity 系统的指导。

## <a name="next-steps"></a>后续步骤

- [使用 Facebook 和 Google OAuth2 创建 ASP.NET MVC 5 应用和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 本教程使用 ASP.NET Identity API 向用户数据库添加配置文件信息，以及如何使用 Google 和 Facebook 进行身份验证。
- [创建具有身份验证和 SQL 数据库的 ASP.NET MVC 应用程序并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 本教程演示如何使用标识 API 添加用户和角色。
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 示例应用程序，演示如何添加基本角色和用户支持，以及如何执行角色和用户管理。
