---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 发行说明 ASP.NET 和 Web 工具Microsoft Docs
author: microsoft
description: 本文档介绍 Visual Studio 2013 ASP.NET 和 Web 工具的版本。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600440"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具发行说明

由[Microsoft](https://github.com/microsoft)

> 本文档介绍 Visual Studio 2013 ASP.NET 和 Web 工具的版本。

## <a name="contents"></a>内容

- [安装说明](#TOC1)
- [文档](#TOC2)
- [软件要求](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>ASP.NET 和 Web 工具中 Visual Studio 2013 的新功能

- [一 ASP.NET](#TOC6)
- [新的 Web 项目体验](#newproj)
- [ASP.NET 基架](#scaffold)
- [浏览器链接](#browser-link)
- [Visual Studio Web 编辑器增强功能](#web-editor)
- [Visual Studio 中的 Azure App Service Web 应用支持](#waws)
- [Web 发布增强功能](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web 窗体](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN 组件](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET 应用挂起](#TOC15)
- [已知问题和重大更改](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>安装说明

Visual Studio 2013 的 ASP.NET 和 Web 工具捆绑在主安装程序中，可在[此处](https://www.asp.net/downloads)下载。

<a id="TOC2"></a>
## <a name="documentation"></a>Documentation

[ASP.NET 网站](https://www.asp.net/)提供了有关 Visual Studio 2013 ASP.NET 和 Web 工具的教程和其他信息。

<a id="TOC4"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET 和 Web 工具要求 Visual Studio 2013。

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>ASP.NET 和 Web 工具中 Visual Studio 2013 的新功能

以下各节介绍了在版本中引入的功能。

<a id="TOC6"></a>
## <a name="one-aspnet"></a>一 ASP.NET

随着 Visual Studio 2013 的发布，我们已开始使用 ASP.NET 技术来统一体验，以便你可以轻松地混合并匹配所需的技术。 例如，你可以使用 MVC 启动项目，并在以后轻松地将 Web 窗体页添加到项目，或在 Web 窗体项目中基架 Web Api。 其中一 ASP.NET 是使你作为开发人员更轻松地完成 ASP.NET 中所喜欢的操作。 无论你选择哪种技术，都可以放心地在一个 ASP.NET 的受信任基础框架上构建。

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>新的 Web 项目体验

在 Visual Studio 2013 中，我们已增强了创建新的 web 项目的体验。 在 "**新建 ASP.NET Web 项目**" 对话框中，您可以选择所需的项目类型，配置任何技术组合（Web 窗体、MVC 和 Web API），配置身份验证选项，以及添加单元测试项目。

![新 ASP.NET 项目](release-notes/_static/image1.png)

通过 "新建" 对话框，您可以更改许多模板的默认身份验证选项。 例如，在创建 ASP.NET Web 窗体项目时，可以选择以下任一选项：

- 无身份验证
- 单个用户帐户（ASP.NET 成员身份或社交提供程序登录）
- 组织帐户（在 internet 应用程序中 Active Directory）
- Windows 身份验证（在 intranet 应用程序中 Active Directory）

![身份验证选项](release-notes/_static/image2.png)

有关用于创建 web 项目的新进程的详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。 有关新的身份验证选项的详细信息，请参阅本文档后面的[ASP.NET Identity](#TOC8) 。

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET 基架

ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。 这样，便可以轻松地将样板代码添加到项目中，以与数据模型交互。

在以前版本的 Visual Studio 中，基架限制为 ASP.NET MVC 项目。 使用 Visual Studio 2013，现在可以将基架用于任何 ASP.NET 项目，包括 Web 窗体。 Visual Studio 2013 当前不支持为 Web 窗体项目生成页，但你仍可以通过将 MVC 依赖项添加到项目中，将基架与 Web 窗体一起使用。 将来的更新中将添加对 Web 窗体的生成页的支持。

使用基架时，请确保在项目中安装所有必需的依赖项。 例如，如果从 ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用会自动添加到你的项目中。

若要将 MVC 基架添加到 Web 窗体项目，请在对话框窗口中添加**新的基架项**，并选择 " **MVC 5 依赖**项"。 基架 MVC 有两个选项：最小和完整。 如果选择 "最小"，则只会将 NuGet 包和 ASP.NET MVC 的引用添加到你的项目中。 如果选择 "完全" 选项，则会添加最小依赖项，以及 MVC 项目所需的内容文件。

对基架的支持：异步控制器使用实体框架6中的新异步功能。

有关详细信息和教程，请参阅[ASP.NET 基架概述](aspnet-scaffolding-overview.md)。

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Browser Link –浏览器和 Visual Studio 之间的 SignalR 通道

使用新的[浏览器链接](using-browser-link.md)功能，可以将多个浏览器连接到 Visual Studio，并通过单击工具栏中的按钮来刷新所有浏览器。 您可以将多个浏览器连接到您的开发站点（包括移动仿真程序），然后单击 "刷新" 以刷新所有浏览器。 Browser 链接还公开了一个 API，使开发人员能够编写浏览器链接扩展。

![](release-notes/_static/image3.png)

通过使开发人员能够利用浏览器链接 API，可以创建非常高级的方案，这些方案跨越 Visual Studio 和连接的任何浏览器之间的边界。 Web Essentials 利用 API 在 Visual Studio 与浏览器的开发人员工具之间创建集成体验，从而远程控制移动模拟器和更多。

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web 编辑器增强功能

Visual Studio 2013 在 web 应用程序中包含用于 Razor 文件和 HTML 文件的新 HTML 编辑器。 新的 HTML 编辑器提供了基于 HTML5 的单个统一架构。 它具有自动大括号完成，jQuery UI 和 AngularJS 特性 IntelliSense，特性 IntelliSense 分组，ID 和类名称 Intellisense，还包括更好的性能、格式设置和智能标记。

以下屏幕截图演示了如何在 HTML 编辑器中使用启动属性 IntelliSense。

![HTML 编辑器中的 Intellisense](release-notes/_static/image4.png)

Visual Studio 2013 还附带了内置的 CoffeeScript 和 LESS 编辑器。 更少的编辑器附带了 CSS 编辑器中的所有酷功能，并在 @import 链中的所有更少文档之间提供了特定的 Intellisense。

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio 中的 Azure App Service Web 应用支持

在使用用于 .NET 2.2 的 Azure SDK Visual Studio 2013 中，你可以使用**服务器资源管理器**与远程 web 应用直接交互。 你可以登录到 Azure 帐户、创建新的 web 应用、配置应用、查看实时日志等等。 SDK 2.2 发布后即将推出，你将能够在 Azure 中远程运行调试模式。 当你安装当前版本的 Azure SDK for .NET 时，Azure App Service Web 应用的大多数新功能也适用于 Visual Studio 2012。

有关更多信息，请参见以下资源：

- [在 Azure App Service 中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web 发布增强功能

Visual Studio 2013 包括新的和增强的 Web 发布功能。 下面是其中几个：

- 轻松[实现 web.config 文件加密的自动化](https://go.microsoft.com/fwlink/?LinkId=325529)。 （此链接和以下两个指向 MSDN 上的文档，这些文档在10/17 年的最晚日期之前可能不可用。）
- [在部署过程中轻松地自动使应用程序脱机](https://go.microsoft.com/fwlink/?LinkId=325530)。
- 将 Web 部署配置为[使用文件校验和，而不是上次更改日期](https://go.microsoft.com/fwlink/?LinkId=325531)，以确定应将哪些文件复制到服务器。
- 使用 FTP 或文件系统发布方法以及 Web 部署时，快速发布单个选定的文件（包括 web.config）。

有关 ASP.NET web 部署的详细信息，请参阅[ASP.NET 站点](https://go.microsoft.com/fwlink/?LinkId=322027)。

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包括一组丰富的新功能，这些功能在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中有详细说明。

此版本的 NuGet 还无需向 NuGet 的包还原功能提供下载包的明确同意。 现在，通过安装 NuGet 授予同意（以及 NuGet 的 "首选项" 对话框中的关联复选框）。 现在，包还原功能在默认情况下是有效的。

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

### <a name="one-aspnet"></a>一 ASP.NET

Web 窗体项目模板与新的 ASP.NET 体验无缝集成。 您可以向 Web 窗体项目添加 MVC 和 Web API 支持，并且可以使用一个 ASP.NET 项目创建向导配置身份验证。 有关详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。

### <a name="aspnet-identity"></a>ASP.NET 标识

Web 窗体项目模板支持新的 ASP.NET Identity 框架。 此外，这些模板现在支持创建 Web 窗体 intranet 项目。 有关详细信息，请参阅**在 Visual Studio 2013 中创建 ASP.NET Web 项目**中的[身份验证方法](creating-web-projects-in-visual-studio.md#auth)。

### <a name="bootstrap"></a>Bootstrap

Web 窗体模板使用[启动](http://twitter.github.io/bootstrap/)，提供精美且响应迅速的外观，您可以轻松地对其进行自定义。 有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 "启动"](creating-web-projects-in-visual-studio.md#bootstrap)。

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>一 ASP.NET

Web MVC 项目模板与新的 ASP.NET 体验无缝集成。 你可以自定义 MVC 项目，并使用 ASP.NET 项目创建向导配置身份验证。 ASP.NET MVC 5 的介绍性教程可在[与 ASP.NET mvc 5 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)上找到。

有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将 ASP.NET mvc 4 和 WEB Api 项目升级到 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。

### <a name="aspnet-identity"></a>ASP.NET 标识

MVC 项目模板已更新为使用 ASP.NET Identity 进行身份验证和标识管理。 有关 Facebook 和 Google 身份验证以及新的成员资格 API 的教程，请参阅[使用 facebook 和 Google OAuth2 创建 ASP.NET mvc 5 应用和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)和[创建具有 AUTH 和 SQL 数据库的 ASP.NET MVC 应用并将其部署到 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。

### <a name="bootstrap"></a>Bootstrap

MVC 项目模板已更新为使用[引导](http://getbootstrap.com/)，提供精美且响应迅速的外观，你可以轻松地对其进行自定义。 有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 "启动"](creating-web-projects-in-visual-studio.md#bootstrap)。

### <a name="authentication-filters"></a>身份验证筛选器

身份验证筛选器是 ASP.NET MVC 中的一种新筛选器，它在 ASP.NET MVC 管道中的授权筛选器之前运行，并允许你为所有控制器指定每个操作的身份验证逻辑、每个控制器或全局。 身份验证筛选器处理请求中的凭据，并提供相应的主体。 身份验证筛选器还可以添加身份验证质询来响应未经授权的请求。

### <a name="filter-overrides"></a>筛选器替代

你现在可以通过指定替代筛选器来覆盖应用于给定操作方法或控制器的筛选器。 替代筛选器指定一组不应针对给定作用域（操作或控制器）运行的筛选器类型。 这样，便可以配置全局应用的筛选器，但不会将某些全局筛选器应用于特定操作或控制器。

### <a name="attribute-routing"></a>属性路由

ASP.NET MVC 现在支持属性路由，因为 Tim McCall （ [http://attributerouting.net](http://attributerouting.net)作者）的贡献。 使用属性路由，可以通过注释操作和控制器来指定路由。

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>属性路由

由于 Tim McCall （ [http://attributerouting.net](http://attributerouting.net)的作者）的贡献，ASP.NET Web API 现在支持属性路由。 使用属性路由，你可以通过批注你的操作和控制器来指定你的 Web API 路由，如下所示：

[!code-csharp[Main](release-notes/samples/sample1.cs)]

特性路由使你可以更好地控制 web API 中的 Uri。 例如，你可以使用单个 API 控制器轻松定义资源层次结构：

[!code-csharp[Main](release-notes/samples/sample2.cs)]

属性路由还提供了一种方便的语法来指定可选参数、默认值和路由约束：

[!code-csharp[Main](release-notes/samples/sample3.cs)]

有关属性路由的详细信息，请参阅[WEB API 2 中的属性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。

### <a name="oauth-20"></a>OAuth 2。0

Web API 和单页应用程序项目模板现在支持使用 OAuth 2.0 的授权。 OAuth 2.0 是一个框架，用于授权客户端对受保护资源的访问。 它适用于各种客户端，包括浏览器和移动设备。

支持 OAuth 2.0 基于 Microsoft OWIN 组件提供的用于持有者身份验证的新安全中间件和实现授权服务器角色。 或者，可以使用组织授权服务器（如 Azure Active Directory 或 Windows Server 2012 R2 中的 ADFS）来授权客户端。

### <a name="odata-improvements"></a>OData 改进

**支持 $select、$expand、$batch 和 $value**

ASP.NET Web API OData 现在完全支持 $select、$expand 和 $value。 你还可以使用 $batch 来请求批处理和处理变更集。

使用 "$select" 和 "$expand" 选项，您可以更改从 OData 终结点返回的数据的形状。 有关详细信息，请参阅[WEB API OData 中的 $select 和 $expand 支持简介](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。

**改进的扩展性**

OData 格式化程序现在可扩展。 可以添加 Atom 项元数据、支持命名流和媒体链接项、添加实例批注以及自定义链接的生成方式。

**不支持类型的支持**

你现在可以构建 OData 服务，无需为你的实体类型定义 CLR 类型。 相反，OData 控制器可以获取或返回**IEdmObject**的实例，这些实例是 OData 格式化程序序列化/反序列化的。

**重用现有模型**

如果已有实体数据模型（EDM），则现在可以直接重复使用它，而无需生成新的实体数据模型。 例如，如果使用实体框架，则可以使用 EF 为你生成的 EDM。

### <a name="request-batching"></a>请求批处理

请求批处理将多个操作合并为一个 HTTP POST 请求，以减少网络流量，并提供更流畅、更流畅的用户界面。 ASP.NET Web API 现在支持多个请求批处理策略：

- 使用 OData 服务的 $batch 终结点。
- 将多个请求打包为一个 MIME 多部分请求。
- 使用自定义批处理格式。

若要启用请求批处理，只需将具有批处理处理程序的路由添加到 Web API 配置：

[!code-csharp[Main](release-notes/samples/sample4.cs)]

你还可以控制是按顺序还是按任意顺序执行请求。

### <a name="portable-aspnet-web-api-client"></a>可移植的 ASP.NET Web API 客户端

你现在可以使用 ASP.NET Web API 客户端创建可在 Windows 应用商店中工作和 Windows Phone 8 个应用程序的可移植类库。 你还可以创建可在客户端和服务器之间共享的可移植格式化程序。

### <a name="improved-testability"></a>改进的可测试性

Web API 2 使对 API 控制器进行单元测试变得更加容易。 只需用请求消息和配置来实例化 API 控制器，然后调用要测试的操作方法。 还可以轻松地模拟执行链接生成的操作方法的**UrlHelper**类。

### <a name="ihttpactionresult"></a>IHttpActionResult

你现在可以实现 IHttpActionResult 来封装 Web API 操作方法的结果。 从 Web API 操作方法返回的 IHttpActionResult 由 ASP.NET Web API 运行时执行，以生成生成的响应消息。 可以从任何 Web API 操作返回 IHttpActionResult，以简化 Web API 实现单元测试。 为方便起见，提供了许多 IHttpActionResult 实现，包括返回特定状态代码、格式化内容或内容协商响应的结果。

### <a name="httprequestcontext"></a>HttpRequestContext

新的**HttpRequestContext**跟踪与请求关联的任何状态，但不会立即从请求中获取。 例如，你可以使用**HttpRequestContext**来获取路由数据、与请求关联的主体、客户端证书、 **UrlHelper**和虚拟路径根。 您可以轻松地创建**HttpRequestContext** ，用于单元测试目的。

由于请求的主体与请求流动，而不是依赖于**thread.currentprincipal**，因此在请求的整个生存期内，主体现在可在 Web API 管道中使用。

### <a name="cors"></a>CORS

由于 Brock Allen 的另一大贡献，ASP.NET 现在完全支持跨域请求共享（CORS）。

Browser security 阻止网页向另一个域发出 AJAX 请求。 [CORS](http://www.w3.org/TR/cors/)是一种 W3C 标准，可让服务器放宽相同的源策略。 使用 CORS，服务器可以在拒绝其他跨域请求时显式允许一些跨域请求。

Web API 2 现在支持 CORS，包括自动处理预检请求。 有关详细信息，请参阅[在 ASP.NET Web API 中启用跨域请求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。

### <a name="authentication-filters"></a>身份验证筛选器

身份验证筛选器是 ASP.NET Web API 中的一种新筛选器，它在 ASP.NET Web API 管道中的授权筛选器之前运行，并允许你为所有控制器指定每个操作的身份验证逻辑、每个控制器或全局。 身份验证筛选器处理请求中的凭据，并提供相应的主体。 身份验证筛选器还可以添加身份验证质询来响应未经授权的请求。

### <a name="filter-overrides"></a>筛选器替代

你现在可以通过指定替代筛选器来覆盖应用于给定操作方法或控制器的筛选器。 替代筛选器指定一组不应针对给定作用域（操作或控制器）运行的筛选器类型。 这样，便可以添加全局筛选器，但不会从特定操作或控制器中排除某些筛选器。

### <a name="owin-integration"></a>OWIN 集成

ASP.NET Web API 现在完全支持 OWIN，并且可以在任何支持 OWIN 的主机上运行。 还包括一个**HostAuthenticationFilter** ，它提供与 OWIN authentication 系统的集成。

借助 OWIN 集成，你可以在自己的进程中自承载 Web API 以及其他 OWIN 中间件，如 SignalR。 有关详细信息，请参阅[将 OWIN 用于自承载 ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2。0

以下各节介绍 SignalR 2.0 的功能。

- [构建于 OWIN](#builtonowin)
- [Routeconfig 和 MapConnection 现在是 MapSignalR](#MapSignalR)
- [跨域支持](#crossdomain)
- [通过 Monotouch.dialog 和 MonoDroid 支持 iOS 和 Android](#mobile)
- [可移植 .NET 客户端](#portable)
- [新的自主机包](#selfhost)
- [向后兼容的服务器支持](#backwardcompat)
- [删除了对 .NET 4.0 的服务器支持](#remove40)
- [将消息发送到客户端和组的列表](#messagelist)
- [向特定用户发送消息](#sendtouser)
- [更好的错误处理支持](#errorhandling)
- [简化集线器的单元测试](#unittesting)
- [JavaScript 错误处理](#javascripterror)

有关如何将现有的1.x 项目升级到 SignalR 2.0 的示例，请参阅[升级 SignalR 1.X 项目](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>构建于 OWIN

SignalR 2.0 完全建立在[OWIN （.net 的开放 Web 接口）](http://owin.org/)上。 此更改使 SignalR 的设置过程在 web 托管的 SignalR 应用程序与自托管的应用程序之间更加一致，但也需要进行大量的 API 更改。

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>Routeconfig 和 MapConnection 现在是 MapSignalR

为了兼容 OWIN 标准，这些方法已重命名为 `MapSignalR`。 不带参数调用的 `MapSignalR` 将映射所有中心（如版本1.x 中的 `MapHubs`）;若要映射各个**PersistentConnection**对象，请将连接类型指定为类型参数，并将连接的 URL 扩展指定为第一个参数。

在 Owin startup 类中调用 `MapSignalR` 方法。 Visual Studio 2013 包含 Owin startup 类的新模板;若要使用此模板，请执行以下操作：

1. 右键单击项目
2. 选择 "**添加**"、"**新建项 ...** "
3. 选择**Owin Startup 类**。 将新类命名为**Startup.cs**。

在**web 应用程序中，** 包含 `MapSignalR` 方法的 Owin startup 类随后使用 web.config 文件的 "应用程序设置" 节点中的条目添加到 Owin 的启动进程，如下所示。

在**自承载的应用程序**中，Startup 类作为 `WebApp.Start` 方法的类型参数进行传递。

**在 SignalR 1.x 中映射中心和连接（从 web 应用程序中的全局应用程序文件）：** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**在 SignalR 2.0 （来自 Owin Startup 类文件）中映射中心和连接：** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

在**自承载的应用程序**中，Startup 类作为 `WebApp.Start` 方法的类型参数进行传递，如下所示。

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>跨域支持

在 SignalR 1.x 中，跨域请求由单个 EnableCrossDomain 标志控制。 此标志控制 JSONP 和 CORS 请求。 为了获得更大的灵活性，已从 SignalR 的服务器组件中删除了所有 CORS 支持（如果检测到浏览器支持，JavaScript 客户端仍使用 CORS），并提供了新的 OWIN 中间件以支持这些方案。

在 SignalR 2.0 中，如果在客户端上需要 JSONP （以支持较早的浏览器中的跨域请求），则需要通过将 `HubConfiguration` 对象的 `EnableJSONP` 设置为 `true`显式启用此功能，如下所示。 默认情况下，JSONP 处于禁用状态，因为它的安全性低于 CORS。

若要在 SignalR 2.0 中添加新的 CORS 中间件，请将 `Microsoft.Owin.Cors` 库添加到项目中，并在 SignalR 中间件之前调用 `UseCors`，如下一节所示。

**将 Owin 添加到你的项目**：若要安装此库，请在包管理器控制台中运行以下命令：

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

此命令会将2.0.0 版本的包添加到你的项目。

**调用 UseCors**

以下代码片段演示了如何在 SignalR 1.x 和2.0 中实现跨域连接。

**在 SignalR 1.x 中实现跨域请求（来自全局应用程序文件）**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**在 SignalR 2.0 中实现跨域请求（从C#代码文件）**

下面的代码演示如何在 SignalR 2.0 项目中启用 CORS 或 JSONP。 此代码示例使用 `Map` 和 `RunSignalR` 而不是 `MapSignalR`，因此，CORS 中间件仅针对需要 CORS 支持的 SignalR 请求（而不是在 `MapSignalR`中指定的路径上的所有流量）运行。 `Map` 也可用于需要针对特定 URL 前缀（而不是整个应用程序）运行的任何其他中间件。

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>通过 Monotouch.dialog 和 MonoDroid 支持 iOS 和 Android

已为 iOS 和 Android 客户端使用[Xamarin 库](https://xamarin.com/)中的 Monotouch.dialog 和 MonoDroid 组件添加了支持。 有关如何使用它们的详细信息，请参阅[使用 Xamarin 组件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。 当 SignalR RTW 版本可用时，这些组件将在[Xamarin 应用商店](https://store.xamarin.com/)中提供。

<a id="portable"></a># # # 可移植的 .NET 客户端

为了更好地促进跨平台开发，Silverlight、WinRT 和 Windows Phone 客户端已替换为支持以下平台的单个可移植 .NET 客户端：

- NET 4。5
- Silverlight 5
- WinRT （适用于 Windows 应用商店应用的 .NET）
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>新的自主机包

现在提供了一个 NuGet 包，可让你更轻松地开始使用 SignalR 自托管（SignalR 应用程序托管在进程或其他应用程序中，而不是托管在 web 服务器中）。 若要升级使用 SignalR 1.x 生成的自承载项目，请删除 SignalR. Owin 包，并添加包。 "SignalR"。 有关自承载包入门的详细信息，请参阅[教程： SignalR 自承载](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>向后兼容的服务器支持

在以前版本的 SignalR 中，客户端和服务器中使用的 SignalR 包的版本需要完全相同。 为了支持难以更新的胖客户端应用程序，SignalR 2.0 现在支持将更新的服务器版本与较旧的客户端配合使用。 **注意： SignalR 2.0 不支持用较新的客户端版本生成的服务器。**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>删除了对 .NET 4.0 的服务器支持

SignalR 2.0 已删除对服务器与 .NET 4.0 的互操作性的支持。 .NET 4.5 必须与 SignalR 2.0 服务器一起使用。 还有一个适用于 SignalR 2.0 的 .NET 4.0 客户端。

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>将消息发送到客户端和组的列表

在 SignalR 2.0 中，可以使用客户端和组 Id 的列表发送消息。 下面的代码段演示了如何执行此操作。

**使用 PersistentConnection 将消息发送到客户端和组的列表**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**使用集线器将消息发送到客户端和组的列表**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>向特定用户发送消息

此功能允许用户通过新的接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容：

**IUserIdProvider 接口**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

默认情况下，将使用用户的 IPrincipal.Identity.Name 作为用户名。

在中心，你可以通过新的 API 向这些用户发送消息：

**使用客户端 API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>更好的错误处理支持

用户现在可以从任何中心调用中引发**HubException** 。 **HubException**的构造函数可以采用字符串消息和对象额外的错误数据。 SignalR 会自动对异常进行序列化，并将其发送到客户端，在该客户端将使用该异常拒绝/使中心方法调用失败。

**显示详细的中心异常**设置与发送回客户端的**HubException**无关;始终发送。

**演示如何将 HubException 发送到客户端的服务器端代码**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**演示响应从服务器发送的 HubException 的 JavaScript 客户端代码**

[!code-html[Main](release-notes/samples/sample16.html)]

**.NET 客户端代码演示响应从服务器发送的 HubException**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>简化集线器的单元测试

SignalR 2.0 在集线器上包含一个名为 `IHubCallerConnectionContext` 的接口，使其更易于创建模拟客户端调用。 以下代码段演示了如何将此接口与常用测试能力[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)一起使用。

**通过 xUnit.net 进行单元测试 SignalR**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**通过 moq 进行单元测试 SignalR**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 错误处理

在 SignalR 2.0 中，所有 JavaScript 错误处理回调都返回 JavaScript 错误对象，而不是原始字符串。 这允许 SignalR 将更丰富的信息流式传输到错误处理程序。 你可以从错误的 `source` 属性获取内部异常。

**处理 Start 的 JavaScript 客户端代码。 Fail 异常**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET 标识

### <a name="new-aspnet-membership-system"></a>新的 ASP.NET 成员资格系统

ASP.NET Identity 是 ASP.NET 应用程序的新成员资格系统。 ASP.NET Identity 可以轻松地将特定于用户的配置文件数据与应用程序数据相集成。 ASP.NET Identity 还允许您为应用程序中的用户配置文件选择持久性模型。 你可以将数据存储在 SQL Server 数据库或其他数据存储中，包括 Azure 存储表等 NoSQL 数据存储。 有关详细信息，请参阅**在 Visual Studio 2013 中创建 ASP.NET Web 项目**中的[单个用户帐户](creating-web-projects-in-visual-studio.md#indauth)。

### <a name="claims-based-authentication"></a>基于声明的身份验证

ASP.NET 现在支持基于声明的身份验证，其中用户的标识表示为来自受信任颁发者的一组声明。 用户可以使用应用程序数据库中维护的用户名和密码进行身份验证，或使用社交标识提供者（例如，Microsoft 帐户、Facebook、Google、Twitter），或通过 Azure Active Directory 或使用组织帐户进行身份验证。Active Directory 联合身份验证服务（ADFS）。

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>与 Azure Active Directory 和 Windows Server Active Directory 的集成

你现在可以创建使用 Azure Active Directory 或 Windows Server Active Directory （AD）进行身份验证的 ASP.NET 项目。 有关详细信息，请参阅**在 Visual Studio 2013 中创建 ASP.NET Web 项目**中的[组织帐户](creating-web-projects-in-visual-studio.md#orgauth)。

### <a name="owin-integration"></a>OWIN 集成

ASP.NET authentication 现在基于可在任何基于 OWIN 的主机上使用的 OWIN 中间件。 有关 OWIN 的详细信息，请参阅以下[MICROSOFT OWIN 组件](#TOC7)部分。

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 组件

[开放式 Web Interface for .net](http://owin.org/) （OWIN）定义 .net web 服务器和 Web 应用程序之间的抽象。 OWIN 使 web 应用程序与服务器分离，使 web 应用程序不可知。 例如，你可以在 IIS 中托管基于 OWIN 的 web 应用程序，或在自定义进程中自行托管该应用程序。

Microsoft OWIN 组件（也称为 Katana 项目）中引入的更改包括新服务器和主机组件、新的帮助程序库和中间件，以及新的身份验证中间件。

有关 OWIN 和 Katana 的详细信息，请参阅[OWIN 和 Katana 中的新增功能](../../../aspnet/overview/owin-and-katana/index.md)。

**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序不能在 IIS 经典模式下运行;它们必须在集成模式下运行。**

**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序必须在完全信任环境中运行。**

### <a name="new-servers-and-hosts"></a>新服务器和主机

在此版本中，添加了新组件以启用自托管方案。 这些组件包括以下 NuGet 包：

- **Owin. HttpListener**。 提供一个 OWIN 服务器，该服务器使用**HttpListener**侦听 HTTP 请求并将其定向到 OWIN 管道。
- **Owin**为希望在自定义进程（如控制台应用程序或 Windows 服务）中自行承载 Owin 管道的开发人员提供了一个库。
- **Owinhost.exe**。 提供一个独立的可执行文件，该可执行文件包装 `Microsoft.Owin.Hosting` 并使你能够在无需编写自定义主机应用程序的情况下自行承载 OWIN 管道。

此外，`Microsoft.Owin.Host.SystemWeb` 包现在使中间件能够向**SystemWeb**服务器提供提示，指出应在特定 ASP.NET 管道阶段调用中间件。 此功能对于应在 ASP.NET 管道中及早运行的身份验证中间件特别有用。

### <a name="helper-libraries-and-middleware"></a>帮助程序库和中间件

尽管只能使用 OWIN 规范中的函数和类型定义编写 OWIN 组件，但新的 `Microsoft.Owin` 包提供了更易于用户使用的抽象集。 此包将几个早期包（例如 `Owin.Extensions`、`Owin.Types`）合并为一个结构良好的对象模型，该对象模型随后可供其他 OWIN 组件轻松使用。 事实上，大多数 Microsoft OWIN 组件现在都使用此包。

> [!NOTE]
> [OWIN](http://www.owin.org)应用程序无法在 IIS 经典模式下运行;它们必须在集成模式下运行。

> [!NOTE]
> [OWIN](http://www.owin.org)应用程序必须在完全信任环境中运行。

此版本还包括 Owin 包，其中包括用于验证正在运行的 OWIN 应用程序的中间件，以及用于帮助调查失败的错误页中间件。

### <a name="authentication-components"></a>身份验证组件

可以使用以下身份验证组件。

- **Microsoft Owin**。 使用本地或基于云的目录服务启用身份验证。
- **Owin**使用 cookie 启用身份验证。 此程序包以前名为 `Microsoft.Owin.Security.Forms`。
- **Owin**使用 facebook 的基于 OAuth 的服务启用身份验证。
- **Owin**使用 google 的基于 OpenID 的服务启用身份验证。
- **Owin**使用 jwt 令牌启用身份验证。
- **Owin. MicrosoftAccount**启用使用 Microsoft 帐户进行身份验证。
- **Microsoft Owin**。 提供 OAuth 授权服务器，以及用于对持有者令牌进行身份验证的中间件。
- **Owin**使用 twitter 的基于 OAuth 的服务启用身份验证。

此版本还包括 `Microsoft.Owin.Cors` 包，其中包含用于处理跨源 HTTP 请求的中间件。

> [!NOTE]
> Visual Studio 2013 的最终版本中已删除对 JWT 签名的支持。

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

有关实体框架6中的新功能和其他更改的列表，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3 包含以下新功能：

- 支持选项卡编辑。 以前，使用 "**保留选项卡**" 选项时，Visual Studio 中的**格式文档**命令、自动缩进和自动格式设置不能正常工作。 此更改纠正了用于 tab 格式的 Razor 代码的 Visual Studio 格式设置。
- 在生成链接时支持 URL 重写规则。
- 删除安全透明特性。
  > [!NOTE]
  > 这是一项重大更改，使 Razor 3 与 MVC4 及更早版本不兼容，而 Razor 2 与 MVC5 或针对 MVC5 编译的程序集不兼容。

Razor 3 从预发行版本中修复的问题，可在[此处](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到 Visual Studio 2013。

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET 应用挂起

ASP.NET 应用暂停是 .NET Framework 4.5.1 中的游戏变化功能，它在一台计算机上彻底更改用于承载大量 ASP.NET 站点的用户体验和经济模型。 有关详细信息，请参阅[ASP.NET 应用挂起–响应式 shared .net web 托管](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

本部分介绍 Visual Studio 2013 的 ASP.NET 和 Web 工具中的已知问题和重大更改。

### <a name="nuget"></a>NuGet

- [使用 SLN 文件时，新的包还原不适用于 Mono](https://nuget.codeplex.com/workitem/3596) -将在即将发布的 nuget.exe 下载和[nuget 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中得到解决。
- [新包还原不适用于 Wix 项目](https://nuget.codeplex.com/workitem/3598)–将在即将发布的 nuget.exe 下载和[nuget 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中得到修复。
- [自动包还原对于解决方案文件夹下的项目不起作用](https://nuget.codeplex.com/workitem/3625)–将在 NuGet 2.8 中进行修复。

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)` 不会 `IQueryable<T>` 总是返回，因为我们添加了对 `$select` 和 `$expand`的支持。

    `ODataQueryOptions<T>` 的前面的示例始终将从 `ApplyTo` 到 `IQueryable<T>`的返回值强制转换。 这是早期工作的，因为我们以前支持的查询选项（`$filter`、`$orderby`、`$skip``$top`）不会更改查询的形状。 现在，我们支持 `$select` 和 `$expand` `ApplyTo` 的返回值将不 `IQueryable<T>`。

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    如果使用的是前面的示例代码，则在客户端不发送 `$select` 和 `$expand`时，它将继续工作。 但是，如果要支持 `$select` 和 `$expand` 必须将该代码更改为此代码。

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **在批处理请求期间，request. Url 或 RequestContext 为 null**

    在批处理方案中，当从**Request**或**RequestContext**访问时， **UrlHelper**为 null。

    此问题当前在此处跟踪：[对于批处理请求，BatchRequestContext 为 null](http://aspnetwebstack.codeplex.com/workitem/1301)。

    此问题的解决方法是创建**UrlHelper**的新实例，如以下示例中所示：

    **创建 UrlHelper 的新实例**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. 使用 MVC5 和 OrgAuth 时，如果有可进行 AntiForgerToken 验证的视图，则在将数据发布到视图时，可能会遇到以下错误：

    **错误**：

    *"/" 应用程序中出现服务器错误。*

    <em>所提供的 ClaimsIdentity 上不存在类型为 "<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>" 或 "<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>" 的声明。若要使用基于声明的身份验证启用防伪令牌支持，请验证配置的声明提供程序是否在其生成的 ClaimsIdentity 实例上同时提供这两个声明。如果配置的声明提供程序改用不同的声明类型作为唯一标识符，则可以通过设置静态属性 AntiForgeryConfig 来配置它。</em>

    **解决方法**：

    在 global.asax 中添加以下行以修复此问题：

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    这将在下一版本中修复。
2. 将 MVC4 应用升级到 MVC5 后，生成并启动解决方案。 应会看到以下错误：

    的HostSection 不能强制转换为 [B] System.web. HostSection. e e。 在位置 "C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35" 的上下文 "默认" 中的 "System.web： Razor，Version = 2.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35" 类型中，键入。 类型 B 源自 "C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ 3.0.0.0" 的上下文 "Default" 中的 "System.web. Razor，Version ="、"Culture = 中性，PublicKeyToken = 31bf3856ad364e35"。

    若要修复上述错误，请在项目中打开*所有*web.config 文件（包括 Views 文件夹中的文件），然后执行以下操作：

   1. 将 "4.0.0.0" 版本的所有实例更新为 "5.0.0.0"。
   2. 更新 "3.0.0.0" 版本的所有匹配项，&quot;System.web&quot; 并将 &quot;为 "" 的 "&quot; System.web. r

      例如，在进行上述更改后，程序集绑定应如下所示：

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将 ASP.NET mvc 4 和 WEB Api 项目升级到 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。
3. 将客户端验证与 jQuery 非引人注目验证一起使用时，验证消息对于类型为 "number" 的 HTML 输入元素有时是不正确的。 如果输入的数字无效，而不是需要有效数字的正确消息，则会显示必需值（"需要 Age 字段"）的验证错误。

    此问题通常出现在 "创建" 和 "编辑" 视图中具有整数属性的模型的基架代码中。

    若要解决此问题，请将编辑器帮助程序从以下内容更改：

    `@Html.EditorFor(person => person.Age)`

    结束时间：

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 不再支持部分信任。 链接到 MVC 或 WebAPI 二进制文件的项目应删除[SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性和[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性。 删除这些属性将消除编译器错误，如下所示。

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 请注意，在这种情况下，不能在同一个应用程序中使用4.0 和5.0 程序集。 需要将它们全部更新为5.0。

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>将网站托管在 intranet 区域中时，采用 Facebook 授权的 SPA 模板可能导致 IE 不稳定

SPA 模板提供与 Facebook 的外部登录。 当用模板创建的项目在本地运行时，登录可能会导致 IE 崩溃。

解决方案：

1. 在 internet 区域中托管网站;或

2. 在 IE 以外的浏览器中测试方案。

### <a name="web-forms-scaffolding"></a>Web 窗体基架

Web 窗体基架已从 VS2013 中删除，并将在 Visual Studio 的未来更新中提供。 不过，你仍然可以通过添加 MVC 依赖项并为 MVC 生成基架，在 Web 窗体项目中使用基架。 你的项目将包含 Web 窗体和 MVC 的组合。

若要将 MVC 添加到 Web 窗体项目，请添加一个新的基架项，并选择 " **MVC 5 依赖**项"。 选择 "最小" 或 "完整"，具体取决于是否需要所有内容文件，如脚本。 然后，为 MVC 添加基架项，这将在项目中创建视图和控制器。

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 基架-HTTP 404，未找到错误

如果将基架项添加到项目时遇到错误，你的项目可能会处于不一致的状态。 所做的某些更改将被回滚，但其他更改（如安装的 NuGet 包）将不会回滚。 如果回滚路由配置更改，则在导航到基架项时，用户将收到 HTTP 404 错误。

解决方法：

- 若要为 MVC 修复此错误，请添加一个新的基架项，并选择 "MVC 5 依赖项（最小或全部）"。 此过程将向你的项目添加所需的所有更改。
- 为 Web API 修复此错误：

  1. 将 Webapiconfig.cs 类添加到项目。

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 按如下所示在 Webapiconfig.cs 中的应用程序\_Start 方法中配置：

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
