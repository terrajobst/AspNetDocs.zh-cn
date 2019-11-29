---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
title: 配置使用应用程序服务的网站（VB） |Microsoft Docs
author: rick-anderson
description: ASP.NET 版本2.0 引入了一系列应用程序服务，它们是 .NET Framework 的一部分，用作一套构建基块服务，
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 9c31a42f-d8bb-4c0f-9ccc-597d4f70ac42
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
msc.type: authoredcontent
ms.openlocfilehash: 19e7258b558372259c7554a36c6ad73ce572dfa8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588675"
---
# <a name="configuring-a-website-that-uses-application-services-vb"></a>配置使用应用程序服务的网站 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_VB.zip)或[下载 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_vb.pdf)

> ASP.NET 版本2.0 引入了一系列应用程序服务，它们是 .NET Framework 的一部分，可用作构建基块服务套件，你可以使用这些服务将丰富的功能添加到你的 web 应用程序。 本教程介绍如何在生产环境中配置网站以使用应用程序服务，并解决在生产环境中管理用户帐户和角色时遇到的常见问题。

## <a name="introduction"></a>简介

ASP.NET 版本2.0 引入了一系列*应用程序服务*，它们是 .NET Framework 的一部分，可用作构建基块服务套件，你可以使用这些服务将丰富的功能添加到你的 web 应用程序。 应用程序服务包括：

- **成员身份**-用于创建和管理用户帐户的 API。
- **角色**-用于将用户分组到组中的 API。
- **Profile** -用于存储自定义的特定于用户的内容的 API。
- **站点地图**-一种 API，用于以层次结构的形式定义站点的逻辑结构，然后可以通过导航控件（如菜单和痕迹导航）显示该结构。
- **个性化设置**-用于维护自定义首选项的 API，最常用于[*webpart*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)。
- **运行状况监视**-一种 API，用于监视正在运行的 web 应用程序的性能、安全性、错误和其他系统运行状况指标。

应用程序服务 Api 不与特定的实现相关联。 相反，您需要指示应用程序服务使用特定的*提供程序*，并且该提供程序使用特定的技术实现该服务。 Web 托管公司托管的基于 Internet 的 web 应用程序最常用的提供程序是使用 SQL Server 数据库实现的提供程序。 例如，`SqlMembershipProvider` 是在 Microsoft SQL Server 数据库中存储用户帐户信息的成员资格 API 的提供程序。

在部署应用程序时，使用应用程序服务和 SQL Server 提供程序会增加一些挑战。 对于初学者，必须在开发和生产数据库中正确地创建应用程序服务数据库对象，并进行相应的初始化。 还需要进行重要的配置设置。

> [!NOTE]
> 应用程序服务 Api 是使用[*提供程序模型*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)设计的，该设计模式允许在运行时提供 API s 实现细节。 .NET Framework 附带了许多可供使用的应用程序服务提供程序，如 `SqlMembershipProvider` 和 `SqlRoleProvider`，它们是使用 SQL Server 数据库实现的成员身份和角色 Api 的提供程序。 你还可以创建自定义提供程序并将其插入。 事实上，书籍评论 web 应用程序已经包含站点地图 API （`ReviewSiteMapProvider`）的自定义提供程序，该提供程序将从数据库中的 `Genres` 和 `Books` 表中的数据构造站点地图。

本教程首先介绍如何扩展书籍评论 web 应用程序以使用成员身份和角色 Api。 然后，它将指导您部署一个使用应用程序服务和 SQL Server 数据库实现的 web 应用程序，并解决在生产环境中管理用户帐户和角色的常见问题。

## <a name="updates-to-the-book-reviews-application"></a>书籍的更新评审应用程序

在过去的几个教程中，书籍回顾 web 应用程序已从静态网站更新为动态、数据驱动的 web 应用程序，其中包含一组管理流派和评审的管理页面。 但是，此管理部分当前不受保护-任何知道（或猜测）管理页 URL 的用户都可以在我们的站点上 waltz 和创建、编辑或删除评论。 保护网站特定部分的常见方法是实现用户帐户，然后使用 URL 授权规则限制对某些用户或角色的访问。 本教程介绍可供下载的书籍检查 web 应用程序支持用户帐户和角色。 它有一个名为 "管理员" 的角色，并且只有此角色中的用户才能访问 "管理" 页。

> [!NOTE]
> 我在一本书中创建了三个用户帐户。 所有三个用户都具有相同的密码： **password！** Scott 和 Jisun 是管理员角色，Alice 不是。 匿名用户仍可访问站点的非管理页面。 也就是说，你无需登录即可访问站点，除非你想要管理它，在这种情况下，你必须以 "管理员" 角色中的用户身份登录。

书籍 "查看应用程序" 母版页已更新，可为经过身份验证的用户和匿名用户提供不同的用户界面。 如果匿名用户访问该站点，她看到的是右上角的 "登录" 链接。 经过身份验证的用户将看到消息 "欢迎回来， *username*！" 和一个用于注销的链接。还有一个登录页（`~/Login.aspx`），其中包含一个登录 Web 控件，该控件提供用户界面和用于验证访问者的逻辑。 只有管理员才能创建新帐户。 （在 `~/Admin` 文件夹中有用于创建和管理用户帐户的页面。）

### <a name="configuring-the-membership-and-roles-apis"></a>配置成员资格和角色 Api

本书回顾 web 应用程序使用成员身份和角色 Api 来支持用户帐户，并将这些用户分组为角色（即管理员角色）。 使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序类，因为我们想要将帐户和角色信息存储在 SQL Server 数据库中。

> [!NOTE]
> 本教程并未详细介绍如何配置 web 应用程序以支持成员身份和角色 Api。 若要全面了解这些 Api 以及配置网站以使用它们所需执行的步骤，请阅读[*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。

若要将应用程序服务用于 SQL Server 数据库，必须首先将这些提供程序使用的数据库对象添加到要在其中存储用户帐户和角色信息的数据库。 这些必要的数据库对象包括各种表、视图和存储过程。 除非另外指定，否则 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序类将使用位于应用程序 `App_Data` 文件夹中名为 `ASPNETDB` SQL Server Express Edition 数据库;如果此类数据库不存在，则会在运行时使用这些访问接口的必要数据库对象自动创建它。

通常，在存储特定于应用程序的数据的数据库中创建应用程序服务数据库对象是可行的，通常是理想的选择。 该 .NET Framework 附带了一个名为 `aspnet_regsql.exe` 的工具，该工具在指定的数据库上安装数据库对象。 我事先使用此工具将这些对象添加到 `App_Data` 文件夹（开发数据库）中的 `Reviews.mdf` 数据库。 我们将在本教程的后面部分介绍如何使用此工具，将这些对象添加到生产数据库中。

如果将应用程序服务数据库对象添加到 `ASPNETDB` 以外的数据库，则需要自定义 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序类配置，使其使用适当的数据库。 若要自定义成员资格提供程序，请在 `Web.config`中的 `<system.web>` 节内添加[ *&lt;成员身份&gt; 元素*](https://msdn.microsoft.com/library/1b9hw62f.aspx)。使用[ *&lt;roleManager&gt; 元素*](https://msdn.microsoft.com/library/ms164660.aspx)配置角色提供程序。 以下代码片段取自 `Web.config` 的书籍查看应用程序，并显示成员身份和角色 Api 的配置设置。 请注意，两个注册新的提供程序 `ReviewMembership` 和 `ReviewRole`，分别使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序。

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample1.xml)]

`Web.config` 文件 s `<authentication>` 元素也已配置为支持基于窗体的身份验证。

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>限制对管理页的访问

通过 ASP.NET，可以轻松地按用户或按角色的*URL 授权*功能授予或拒绝对特定文件或文件夹的访问权限。 （我们会在*iis 与 ASP.NET 开发服务器教程之间*简要介绍了 url 授权，并说明了 iis 和 ASP.NET 开发服务器如何以不同的方式针对静态内容和动态内容应用 url 授权规则。）由于我们希望禁止访问 "管理员" 角色中的用户以外的 `~/Admin` 文件夹，因此需要将 URL 授权规则添加到此文件夹。 具体而言，URL 授权规则需要允许管理员角色中的用户拒绝所有其他用户。 为此，可将 `Web.config` 文件添加到 `~/Admin` 文件夹中，其中包含以下内容：

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample3.xml)]

若要详细了解 ASP.NET s URL 授权功能以及如何使用它来拼写用户和角色的授权规则，请务必阅读[*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)中的[*基于用户的授权*](../../older-versions-security/membership/user-based-authorization-vb.md)和[*基于角色的授权*](../../older-versions-security/roles/role-based-authorization-vb.md)教程。

## <a name="deploying-a-web-application-that-uses-application-services"></a>部署使用应用程序服务的 Web 应用程序

在部署使用应用程序服务的网站和在数据库中存储应用程序服务信息的提供程序时，必须在生产数据库中创建应用程序服务所需的数据库对象。 最初，生产数据库不包含这些对象，因此，在首次部署应用程序时（或在添加应用程序服务后首次部署应用程序时），您必须执行额外的步骤以在生产数据库。

如果要将在开发环境中创建的用户帐户复制到生产环境，则在部署使用应用程序服务的网站时可能会出现另一项挑战。 即使你将在开发环境中创建的用户帐户成功地复制到生产数据库中，但这些用户无法在生产环境中登录到 web 应用程序，具体取决于成员身份和角色配置。 我们将查看此问题的原因并讨论如何防止发生此问题。

ASP.NET 附带了一个不错的[*网站管理工具（WSAT）* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) ，可从 Visual Studio 启动，并允许通过基于 Web 的界面管理用户帐户、角色和授权规则。 遗憾的是，WSAT 仅适用于本地网站，这意味着它不能用于远程管理生产环境中 web 应用程序的用户帐户、角色和授权规则。 我们将看看如何通过不同的方式实现生产网站中类似于 WSAT 的行为。

### <a name="adding-the-database-objects-using-aspnet_regsqlexe"></a>使用 aspnet\_regsql 添加数据库对象

*部署数据库*教程介绍了如何将表和数据从开发数据库复制到生产数据库，当然，这些技术也可以用来将应用程序服务数据库对象复制到生产数据库中。 另一个选项是 `aspnet_regsql.exe` 工具，它可在数据库中添加或删除应用程序服务数据库对象。

> [!NOTE]
> `aspnet_regsql.exe` 工具在指定的数据库上创建数据库对象。 它不会将这些数据库对象中的数据从开发数据库迁移到生产数据库。 如果要将开发数据库中的用户帐户和角色信息复制到生产数据库，请使用*部署数据库*教程中所述的方法。

让我们看看如何使用 `aspnet_regsql.exe` 工具将数据库对象添加到生产数据库中。 首先打开 Windows 资源管理器并导航到计算机上的 .NET Framework 2.0 版目录，% WINDIR% \NET\Framework\v2.0.50727。 你应找到 `aspnet_regsql.exe` 工具。 此工具可从命令行使用，但它还包括图形用户界面;双击 `aspnet_regsql.exe` 文件以启动其图形组件。

该工具首先显示初始屏幕，其中说明了其用途。 单击 "下一步" 转到 "选择安装选项" 屏幕，如图1所示。 从这里，你可以选择添加应用程序服务数据库对象或从数据库中删除它们。 由于我们要将这些对象添加到生产数据库，因此请选择 "为应用程序服务配置 SQL Server" 选项，然后单击 "下一步"。

[![选择为应用程序服务配置 SQL Server](configuring-a-website-that-uses-application-services-vb/_static/image2.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image1.jpg)

**图 1**：选择为应用程序服务配置 SQL Server （[单击查看完全大小的图像](configuring-a-website-that-uses-application-services-vb/_static/image3.jpg)）

在 "选择服务器和数据库" 屏幕上，提示输入连接到数据库的信息。 输入 web 托管公司提供的数据库服务器、安全凭据和数据库名称，然后单击 "下一步"。

> [!NOTE]
> 输入数据库服务器和凭据后，展开 "数据库" 下拉列表时可能会出现错误。 `aspnet_regsql.exe` 工具将查询 `sysdatabases` 系统表以检索服务器上的数据库列表，但某些 web 宿主公司会锁定其数据库服务器，以便此信息不会公开提供。 如果收到此错误，可以直接在下拉列表中键入数据库名称。

[![为该工具提供数据库的连接信息](configuring-a-website-that-uses-application-services-vb/_static/image5.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image4.jpg)

**图 2**：向该工具提供数据库的连接信息（[单击以查看完全大小的映像](configuring-a-website-that-uses-application-services-vb/_static/image6.jpg)）

后续屏幕汇总了即将发生的操作，即应用程序服务数据库对象将添加到指定的数据库。 单击 "下一步" 完成此操作。 几分钟后，将显示最后一个屏幕，指出已添加数据库对象（请参阅图3）。

[![成功！应用程序服务数据库对象已添加到生产数据库中](configuring-a-website-that-uses-application-services-vb/_static/image8.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image7.jpg)

**图 3**：成功！ 应用程序服务数据库对象已添加到生产数据库（[单击查看完全大小的映像](configuring-a-website-that-uses-application-services-vb/_static/image9.jpg)）

若要验证应用程序服务数据库对象是否已成功添加到生产数据库，请打开 SQL Server Management Studio 并连接到生产数据库。 如图4所示，你现在应看到数据库中的应用程序服务数据库表、`aspnet_Applications`、`aspnet_Membership`、`aspnet_Users`等。

[![确认数据库对象已添加到生产数据库中](configuring-a-website-that-uses-application-services-vb/_static/image11.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image10.jpg)

**图 4**：确认数据库对象已添加到生产数据库（[单击查看完全大小的映像](configuring-a-website-that-uses-application-services-vb/_static/image12.jpg)）

仅在首次部署 web 应用程序时，或在开始使用应用程序服务后首次使用时，才需要使用 `aspnet_regsql.exe` 工具。 一旦这些数据库对象位于生产数据库中，就不需要重新添加或修改它们。

### <a name="copying-user-accounts-from-development-to-production"></a>将用户帐户从开发复制到生产

使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序类将应用程序服务信息存储在 SQL Server 数据库中时，用户帐户和角色信息将存储在不同的数据库表中，这些表包括 `aspnet_Users`、`aspnet_Membership`、`aspnet_Roles`和 `aspnet_UsersInRoles`等。 如果在开发过程中，您在开发环境中创建用户帐户，则可以通过从相应数据库表复制相应的记录，在生产环境中复制这些用户帐户。 如果你使用数据库发布向导来部署应用程序服务数据库对象，则可能还选择复制记录，这将导致在开发期间创建的用户帐户也会在生产环境中进行。 但是，根据您的配置设置，您可能会发现，在开发中创建并复制到生产的帐户的用户无法从生产网站登录。 提供了哪些功能？

`SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序类的设计使单个数据库可以充当多个应用程序的用户存储，因此，每个应用程序理论上都有一个具有相同名称的重叠用户名和角色的用户。 为了实现这种灵活性，数据库将维护 `aspnet_Applications` 表中的应用程序列表，并且每个用户与其中一个应用程序相关联。 具体而言，`aspnet_Users` 表有一个 `ApplicationId` 列，该列将每个用户与 `aspnet_Applications` 表中的一条记录联系起来。

除了 `ApplicationId` 列外，`aspnet_Applications` 表还包含一个 `ApplicationName` 列，该列为应用程序提供了更友好的名称。 当网站尝试使用用户帐户（如从登录页验证用户凭据）时，它必须告知 `SqlMembershipProvider` 类要使用的应用程序。 通常通过提供应用程序名称来实现此功能，此值来自 `Web.config` 中的提供程序配置（具体来说是通过 `applicationName` 属性进行）。

但是，如果未在 `Web.config`中指定 `applicationName` 特性，会发生什么情况呢？ 在这种情况下，成员资格系统使用应用程序根路径作为 `applicationName` 值。 如果未在 `Web.config`中显式设置 `applicationName` 属性，则开发环境和生产环境可能会使用不同的应用程序根目录，因此会与应用程序服务中的不同应用程序名称关联。 如果发生这种不匹配，则在开发环境中创建的用户将有与生产环境的 `ApplicationId` 值不匹配的 `ApplicationId` 值。 最终结果是，这些用户将无法登录。

> [!NOTE]
> 如果你发现自己在这种情况下，将用户帐户复制到生产时使用不匹配的 `ApplicationId` 值，则可以编写一个查询，将这些错误的 `ApplicationId` 值更新为在生产环境中使用的 `ApplicationId`。 更新之后，在开发环境中创建帐户的用户现在可以登录到生产环境中的 web 应用程序。

好消息是，你可以执行一个简单的步骤来确保两个环境使用相同的 `ApplicationId`-在 `Web.config` 中为所有应用程序服务提供程序显式设置 `applicationName` 特性。 我在 `<membership>` 和 `<roleManager>` 元素中显式将 `applicationName` 特性设置为 "BookReviews"，这是 `Web.config` 所示的此代码段。

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample4.xml)]

若要深入了解如何设置 `applicationName` 属性及其背后的基本原理，请参阅[*Scott Guthrie*](https://weblogs.asp.net/scottgu/) s 博客文章：[*配置 ASP.NET 成员身份和其他提供程序时，请始终设置 applicationName 属性*](https://weblogs.asp.net/scottgu/443634)。

### <a name="managing-user-accounts-in-the-production-environment"></a>在生产环境中管理用户帐户

使用 ASP.NET 网站管理工具（WSAT），可以轻松创建和管理用户帐户、定义和应用角色，以及拼写用户和基于角色的授权规则。 可以通过转到 "解决方案资源管理器" 并单击 "ASP.NET" "配置" 图标，或转到 "网站" 或 "项目" 菜单，然后选择 "ASP.NET" 配置菜单项，从 Visual Studio 启动 WSAT。 遗憾的是，WSAT 只能用于本地网站。 因此，不能使用工作站中的 WSAT 来管理生产环境中的网站。

好消息是，WSAT 提供的所有功能都通过成员身份和角色 Api 以编程方式提供;此外，许多 WSAT 屏幕都使用标准的 ASP.NET 登录相关控件。 简而言之，你可以将 ASP.NET 页面添加到你的网站，该网站提供必要的管理功能。

请记住，更早的教程已将书籍评论 web 应用程序更新为包含 `~/Admin` 文件夹，此文件夹已配置为仅允许管理员角色中的用户使用。 我向此文件夹添加了一个名为 `CreateAccount.aspx` 的页面，管理员可从中创建新的用户帐户。 此页面使用 CreateUserWizard 控件显示用于创建新用户帐户的用户界面和后端逻辑。 另外，我自定义了控件以包含一个复选框，该复选框会提示是否还应将新用户添加到管理员角色中（请参阅图5）。 通过少许工作，您可以构建一组自定义页面，用于实现用户和角色管理相关的任务，这些任务将由 WSAT 提供。

> [!NOTE]
> 若要详细了解如何结合使用成员身份和角色 Api 以及与登录相关的 ASP.NET Web 控件，请参阅[*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。 有关自定义 CreateUserWizard 控件的详细信息，请参阅[*创建用户帐户*](../../older-versions-security/membership/creating-user-accounts-vb.md)和[*存储其他用户信息*](../../older-versions-security/membership/storing-additional-user-information-vb.md)教程，或查看[*Erich Peterson*](http://www.erichpeterson.com/) s 文章，[*自定义 CreateUserWizard 控件*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)。

[![管理员可以创建新的用户帐户](configuring-a-website-that-uses-application-services-vb/_static/image14.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image13.jpg)

**图 5**：管理员可以创建新的用户帐户（[单击查看完全大小的映像](configuring-a-website-that-uses-application-services-vb/_static/image15.jpg)）

如果需要 WSAT 的全部功能，请使用 "查看[*自己的网站管理工具*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)"，其中作者 Dan Clem 逐步完成构建自定义 WSAT 工具的过程。 Dan 共享其应用程序的源代码（在C#中），并提供将其添加到托管网站的分步说明。

## <a name="summary"></a>总结

部署使用应用程序服务数据库实现的 web 应用程序时，必须首先确保生产数据库具有必要的数据库对象。 可以使用在 "*部署数据库*" 教程中讨论的技术来添加这些对象。或者，您可以使用 `aspnet_regsql.exe` 工具，如本教程中所述。 我们围绕的其他挑战：同步开发环境和生产环境中使用的应用程序名称（如果您希望在开发环境中创建的用户和角色在生产环境中有效，这一点很重要）和技术管理生产环境中的用户和角色。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [*ASP.NET SQL Server 注册工具（aspnet_regsql .exe）* ](https://msdn.microsoft.com/library/ms229862.aspx)
- [*为 SQL Server 创建应用程序服务数据库*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*在 SQL Server 中创建成员身份架构*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb.md)
- [*检查 ASP.NET 的成员资格、角色和配置文件*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*滚动你自己的网站管理工具*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*网站安全教程*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*网站管理工具概述*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [上一页](configuring-the-production-web-application-to-use-the-production-database-vb.md)
> [下一页](strategies-for-database-development-and-deployment-vb.md)
