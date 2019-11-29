---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
title: 安全基础知识和 ASP.NET 支持（VB） |Microsoft Docs
author: rick-anderson
description: 这是一系列教程中的第一篇教程，这些教程将探讨通过 web 窗体验证访问者的方法，授权访问 partic 。
ms.author: riande
ms.date: 01/13/2008
ms.assetid: ab68a92b-fc81-40a4-a7dc-406625d2c5d4
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
msc.type: authoredcontent
ms.openlocfilehash: 99e986013cb5a923ddb150022013e3a75852ce55
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621615"
---
# <a name="security-basics-and-aspnet-support-vb"></a>安全基础知识和 ASP.NET 支持 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_vb.pdf)

> 这是一系列教程中的第一个教程，这些教程将探讨通过 web 窗体验证访问者、授权访问特定页面和功能以及管理 ASP.NET 应用程序中的用户帐户的方法。

## <a name="introduction"></a>简介

什么是论坛、电子商务网站、联机电子邮件网站、门户网站和社交网站的共同之处？ 它们都提供*用户帐户*。 提供用户帐户的站点必须提供多个服务。 新的访问者至少需要能够创建帐户并返回访问者必须能够登录。 此类 web 应用程序可以基于已登录的用户做出决策：某些页面或操作可能仅限于登录用户或特定部分用户;其他页面可能显示特定于已登录用户的信息，或者可能显示更多或更少信息，具体取决于查看该页的用户。

这是一系列教程中的第一个教程，这些教程将探讨通过 web 窗体验证访问者、授权访问特定页面和功能以及管理 ASP.NET 应用程序中的用户帐户的方法。 在这些教程中，我们将讨论如何：

- 标识并将用户登录到网站
- 使用 ASP。用于管理用户帐户的网络成员身份框架
- 创建、更新和删除用户帐户
- 基于登录用户限制对网页、目录或特定功能的访问权限
- 使用 ASP。将用户帐户与角色关联的 NET Role framework
- 管理用户角色
- 基于登录用户的角色限制对网页、目录或特定功能的访问权限
- 自定义和扩展 ASP。网络安全 Web 控件

这些教程旨在简洁明了，并提供有关多个屏幕截图的分步说明，以直观地完成此过程。 每个教程都在C#和 Visual Basic 版本中提供，并包括所使用的完整代码的下载。 （第一个教程重点介绍高级视点中的安全概念，因此不包含任何关联的代码。）

在本教程中，我们将讨论重要的安全概念和 ASP.NET 中提供的功能，以帮助实现 forms 身份验证、授权、用户帐户和角色。 让我们进入正题！

> [!NOTE]
> 安全性是任何应用程序的一个重要方面，涉及到物理、技术和策略决策，并且需要进行大量的规划和域知识。 本系列教程不应作为开发安全 web 应用程序的指南。 相反，它专门侧重于 forms 身份验证、授权、用户帐户和角色。 尽管本系列文章中讨论了某些安全概念，但其他一些问题仍是未探索的。

## <a name="authentication-authorization-user-accounts-and-roles"></a>身份验证、授权、用户帐户和角色

身份验证、授权、用户帐户和角色是在本系列教程中非常常使用的四个术语，因此我想要花点时间在 web 安全上下文中定义这些术语。 在客户端-服务器模型（如 Internet）中，在许多情况下，服务器需要标识发出请求的客户端。 *身份验证*是认定客户端标识的过程。 已成功标识的客户端被视为*经过身份验证*。 不可识别的客户端被称为*未经身份验证*或*匿名*的。

安全身份验证系统至少涉及到以下三个方面之一：[你知道的内容、你的内容或你的内容](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)。 大多数 web 应用程序依赖于客户端知道的内容，例如密码或 PIN。 例如，用于标识用户的用户名和密码的信息称为*凭据*。 本系列教程重点介绍*窗体身份验证*，这是一种身份验证模式，用户通过在网页窗体中提供凭据，用户可以登录到网站。 以前，我们已经历过这种类型的身份验证。 中转到任何电子商务站点。 当你准备好签出时，系统会要求你通过在网页上的文本框中输入用户名和密码进行登录。

除了标识客户端外，服务器还需要限制可访问的资源或功能，具体取决于发出请求的客户端。 *授权*是指确定特定用户是否有权访问特定资源或功能的过程。

*用户帐户*是保存有关特定用户的信息的存储。 用户帐户必须最少包含唯一标识用户的信息，例如用户的登录名和密码。 除这一重要信息外，用户帐户可能包含：用户的电子邮件地址;创建帐户的日期和时间;上次登录的日期和时间;名字和姓氏;电话号码;和邮件地址。 使用窗体身份验证时，用户帐户信息通常存储在关系数据库中，如 Microsoft SQL Server。

支持用户帐户的 Web 应用程序可以选择将用户分组为*角色*。 角色只是应用于用户的标签，并提供用于定义授权规则和页面级别功能的抽象。 例如，某个网站可能包含一个管理员角色，该角色的授权规则禁止除管理员之外的任何人访问一组特定网页。 而且，所有用户都可以访问的各种页面（包括非管理员）可能会显示其他数据，或在管理员角色中的用户访问时提供额外的功能。 使用角色，我们可以逐个角色地定义这些授权规则，而不是按用户来定义这些规则。

## <a name="authenticating-users-in-an-aspnet-application"></a>在 ASP.NET 应用程序中对用户进行身份验证

当用户在其浏览器的 "地址" 窗口中输入 URL 或单击链接时，浏览器将为指定的内容对 web 服务器进行[超文本传输协议（HTTP）](http://en.wikipedia.org/wiki/HTTP)请求，将其作为 ASP.NET 页、图像、JavaScript 文件或任何其他类型的内容。 Web 服务器负责返回所请求的内容。 在执行此操作时，它必须确定请求的相关信息，包括发出请求的人员以及标识是否有权检索请求的内容。

默认情况下，浏览器发送的 HTTP 请求缺少任何种类的标识信息。 但如果浏览器包含身份验证信息，则 web 服务器将启动身份验证工作流，该工作流将尝试标识发出请求的客户端。 身份验证工作流的步骤取决于 web 应用程序所使用的身份验证类型。 ASP.NET 支持三种类型的身份验证： Windows、Passport 和表单。 本系列教程重点介绍窗体身份验证，但我们需要花几分钟时间来比较和对比 Windows 身份验证用户存储和工作流。

### <a name="authentication-via-windows-authentication"></a>通过 Windows 身份验证进行身份验证

Windows 身份验证工作流使用以下身份验证方法之一：

- 基本身份验证
- 摘要式身份验证
- Windows 集成身份验证

所有这三种方法的工作方式大致相同：在未经授权的匿名请求到达时，web 服务器回发 HTTP 响应，指出需要授权才能继续。 然后，浏览器会显示一个模式对话框，提示用户输入其用户名和密码（请参阅图1）。 然后，通过 HTTP 标头将此信息发送回 web 服务器。

![模式对话框会提示用户输入其凭据](security-basics-and-asp-net-support-vb/_static/image1.png)

**图 1**：模式对话框会提示用户输入其凭据

针对 web 服务器的 Windows 用户存储对提供的凭据进行验证。 这意味着你的 web 应用程序中的每个经过身份验证的用户都必须在你的组织中有一个 Windows 帐户。 这在 intranet 方案中很常见。 事实上，在 intranet 设置中使用 Windows 集成身份验证时，浏览器会自动为 web 服务器提供用于登录网络的凭据，从而禁止显示图1中所示的对话框。 虽然 Windows 身份验证非常适合 intranet 应用程序，但它通常不可行适用于 Internet 应用程序，因为你不希望为每个注册到站点的用户创建 Windows 帐户。

### <a name="authentication-via-forms-authentication"></a>通过 Forms 身份验证进行身份验证

另一方面，窗体身份验证是 Internet web 应用程序的理想选择。 回忆一下，窗体身份验证通过提示用户通过 web 窗体输入其凭据来标识用户。 因此，当用户尝试访问未经授权的资源时，会自动将其重定向到登录页，用户可以在其中输入其凭据。 然后，将根据自定义用户存储（通常为数据库）对提交的凭据进行验证。

验证提交的凭据后，将为用户创建*forms 身份验证票证*。 此票证表示用户已通过身份验证，并包括标识信息，例如用户名。 Forms 身份验证票证通常作为 cookie 存储在客户端计算机上。 因此，对该网站的后续访问包含 HTTP 请求中的 forms 身份验证票证，从而使 web 应用程序能够在用户登录后对其进行标识。

图2说明了来自高级 vantage 点的窗体身份验证工作流。 请注意，ASP.NET 中的身份验证和授权部分如何充当两个不同的实体。 Forms 身份验证系统标识用户（或报告他们是匿名的）。 授权系统确定用户是否有权访问所请求的资源。 如果用户未授权（如在尝试匿名访问 ProtectedPage 时在图2中所示），则授权系统会报告用户被拒绝，导致 forms 身份验证系统自动将用户重定向到登录页。

用户成功登录后，后续 HTTP 请求将包含 forms 身份验证票证。 Forms 身份验证系统仅标识用户，即确定用户是否可以访问请求的资源的授权系统。

![Forms 身份验证工作流](security-basics-and-asp-net-support-vb/_static/image2.png)

**图 2**： Forms 身份验证工作流

我们将在接下来的两个教程中深入探讨 forms 身份验证，[其中概述了 Forms 身份验证](an-overview-of-forms-authentication-vb.md)和[Forms 身份验证配置和高级主题](forms-authentication-configuration-and-advanced-topics-vb.md)。 有关 ASP 的详细信息。NET 的身份验证选项，请参阅[ASP.NET authentication](https://msdn.microsoft.com/library/eeyk640h.aspx)。

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>限制对网页、目录和页面功能的访问

ASP.NET 包含两种方法来确定特定用户是否有权访问特定文件或目录：

- **文件授权**-由于 ASP.NET 页面和 web 服务是作为驻留在 web 服务器文件系统上的文件来实现的，因此可以通过访问控制列表（acl）来指定对这些文件的访问权限。 文件授权最常用于 Windows 身份验证，因为 Acl 是适用于 Windows 帐户的权限。 使用 forms 身份验证时，所有操作系统和文件系统级请求均由同一 Windows 帐户执行，而不考虑访问站点的用户。
- **Url 授权**-对于 url 授权，页面开发人员在 web.config 中指定授权规则。这些授权规则指定允许哪些用户或角色访问应用程序中的某些页面或目录，或者拒绝用户或角色访问。

文件授权和 URL 授权定义用于访问特定目录中的特定 ASP.NET 页面或所有 ASP.NET 页面的授权规则。 使用这些技术，我们可以指示 ASP.NET 拒绝特定用户对特定页面的请求，或允许访问一组用户，并拒绝对其他人的访问。 所有用户都可以访问页面的情况如何，但页面的功能取决于用户？ 例如，许多支持用户帐户的站点都有一些页面，这些页面为经过身份验证的用户与匿名用户显示不同的内容或数据。 匿名用户可能会看到一个用于登录到站点的链接，而经过身份验证的用户将看到一条消息，如 "欢迎回来"、"*用户名*" 和 "注销" 链接。另一个示例：查看拍卖网站上的项时，将看到不同的信息，具体取决于你是 bidder 还是建构拍卖项。

此类级调整可以通过声明方式或以编程方式完成。 若要为匿名用户显示与经过身份验证的用户不同的内容，只需将[登录视图控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)拖到页面上，并在其 AnonymousTemplate 和 LoggedInTemplate 模板中输入适当的内容。 或者，您可以通过编程方式确定当前请求是否经过身份验证、用户是谁以及他们所属的角色（如果有）。 您可以使用此信息来显示或隐藏页面上网格或面板中的列。

此系列包括三个侧重于授权的教程。 ***基于用户的授权***检查如何限制特定用户帐户对目录中的一个或多个页面的访问。***基于角色的授权***在角色级别提供授权规则;最后，***基于当前登录用户的显示内容***教程介绍了如何根据访问页面的用户修改特定页面的内容和功能。 有关 ASP 的详细信息。NET 的授权选项，请参阅[ASP.NET authorization](https://msdn.microsoft.com/library/wce3kxhd.aspx)。

## <a name="user-accounts-and-roles"></a>用户帐户和角色

ASP.NET.NET 的窗体身份验证为用户提供了一种基础结构，使用户能够登录到站点并在页面访问中记住其身份验证状态。 和 URL 授权提供一个框架，用于限制对 ASP.NET 应用程序中的特定文件或文件夹的访问。 但这两种功能都不提供存储用户帐户信息或管理角色的方法。

在 ASP.NET 2.0 之前，开发人员负责创建自己的用户和角色存储。 它们也位于挂钩上，用于设计用户界面，并为重要的用户帐户相关页面（如登录页和用于创建新帐户的页面）编写代码。 如果没有 ASP.NET 中的任何内置用户帐户框架，则实现用户帐户的每个开发人员都必须在自己的问题（如如何实现存储密码或其他敏感信息）上进行设计决策？我应对密码长度和强度施加哪些指导原则？

如今，使用*成员身份框架*和内置登录 Web 控件，在 ASP.NET 应用程序中实现用户帐户要简单得多。 成员身份框架是[system.web 命名空间](https://msdn.microsoft.com/library/system.web.security.aspx)中的少数类，提供用于执行与用户帐户相关的重要任务的功能。 成员身份框架中的键类是[成员身份类](https://msdn.microsoft.com/library/system.web.security.membership.aspx)，其方法如下：

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- System.web.security.membership.validateuser

成员身份框架使用[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，该模型将成员身份框架的 API 与实现完全分离。 这使开发人员能够使用公共 API，但使他们能够使用满足其应用程序自定义需求的实现。 简而言之，成员身份类定义框架的基本功能（方法、属性和事件），但并不实际提供任何实现细节。 相反，成员资格类的方法将调用配置的提供程序，该提供程序将执行实际工作。 例如，当调用成员身份类的 CreateUser 方法时，成员身份类不知道用户存储的详细信息。 它不知道用户是在数据库中还是在 XML 文件或其他存储中进行维护。 成员身份类检查 web 应用程序的配置，以确定要将调用委托给哪个提供程序，并且该提供程序类负责在相应的用户存储中实际创建新的用户帐户。 图3演示了这种交互。

Microsoft 在 .NET Framework 中附带了两个成员资格提供程序类：

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -在 Active Directory 和 Active Directory 应用程序模式（ADAM）服务器中实现成员身份 API。
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -实现 SQL Server 数据库中的成员身份 API。

本教程系列专门针对 SqlMembershipProvider。

[![提供程序模型允许将不同的实现无缝插入框架](security-basics-and-asp-net-support-vb/_static/image4.png)](security-basics-and-asp-net-support-vb/_static/image3.png)

**图 03**：提供程序模型允许将不同的实现无缝插入框架（[单击以查看完全大小的图像](security-basics-and-asp-net-support-vb/_static/image5.png)）

提供程序模型的优点是，可由 Microsoft、第三方供应商或单独开发人员开发，并无缝地插入成员身份框架。 例如，Microsoft 已发布[了 Microsoft Access 数据库的成员资格提供程序](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)。 有关成员资格提供程序的详细信息，请参阅[提供程序工具包](https://msdn.microsoft.com/asp.net/aa336558.aspx)，其中包括成员资格提供程序的演练、示例自定义提供程序、提供程序模型上100页的文档以及内置成员资格提供程序（即 ActiveDirectoryMembershipProvider 和 SqlMembershipProvider）的完整源代码。

ASP.NET 2.0 还引入了角色框架。 与成员身份框架一样，角色框架是在提供程序模型的顶层生成的。 其 API 通过[role 类](https://msdn.microsoft.com/library/system.web.security.roles.aspx)公开，.NET Framework 附带了三个提供程序类：

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -在授权管理器策略存储区中管理角色信息，如 ACTIVE DIRECTORY 或 ADAM。
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -实现 SQL Server 数据库中的角色。
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -基于访问者的 Windows 组关联角色信息。 此方法通常与 Windows 身份验证一起使用。

本教程系列专门针对 SqlRoleProvider。

由于提供程序模型包括单个正向 API （成员身份和角色类），因此可以围绕该 API 构建功能，而无需担心实现细节-这些功能由页面所选的提供程序进行处理开发. 此统一 API 允许 Microsoft 和第三方供应商构建与成员身份和角色框架进行交互的 Web 控件。 ASP.NET 附带了一些用于实现常见用户帐户用户界面的[登录 Web 控件](https://msdn.microsoft.com/library/ms178329.aspx)。 例如，[登录控件会](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)提示用户输入其凭据，对其进行验证，然后通过 forms 身份验证将它们记录在中。 [登录视图控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)提供模板，用于显示匿名用户的不同标记与经过身份验证的用户，或基于用户角色的不同标记。 [CreateUserWizard 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx)提供了创建新用户帐户的分步用户界面。

下面的内容涵盖各种登录控件与成员身份和角色框架的交互。 大多数登录控件都无需编写一行代码即可实现。 我们将在以后的教程中更详细地检查这些控件，包括用于扩展和自定义其功能的技术。

## <a name="summary"></a>总结

支持用户帐户的所有 web 应用程序都需要类似的功能，例如：允许用户登录，并使其登录状态在跨页访问时保留;用于创建帐户的新访问者的网页;还能让页面开发人员指定哪些资源、数据和功能可用于哪些用户或角色。 由于 forms 身份验证、URL 授权以及成员身份和角色框架，在 ASP.NET 应用程序中，对用户进行身份验证和授权以及管理用户帐户和角色的任务非常易于完成。

在接下来的几个教程中，我们将通过逐步地从头开始构建有效的 web 应用程序来检查这些方面。 在接下来的两个教程中，我们将详细探讨 forms 身份验证。 我们将看到窗体身份验证工作流在运行中，仔细分析了 forms 身份验证票证，讨论了安全问题，并了解如何配置 forms 身份验证系统，同时构建允许访问者登录和注销的 web 应用程序。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 2.0 成员资格、角色、Forms 身份验证和安全资源](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2.0 安全指南](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET 身份验证](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET 授权](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET 登录控件概述](https://msdn.microsoft.com/library/ms178329.aspx)
- [检查 ASP.NET 2.0 的成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何实现：使用成员身份和角色保护我的站点？](https://asp.net/learn/videos/video-45.aspx) （视频）
- [成员资格简介](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN 安全开发人员中心](https://msdn.microsoft.com/security/default.aspx)
- [Professional ASP.NET 2.0 安全性、成员身份和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)（ISBN：978-0-7645-9698-8）
- [提供商工具包](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主要审阅者是此教程系列已由许多有用的审阅者查看。 本教程的主管评审者包括 Alicja Maziarz、John Suru 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](forms-authentication-configuration-and-advanced-topics-cs.md)
> [下一页](an-overview-of-forms-authentication-vb.md)
