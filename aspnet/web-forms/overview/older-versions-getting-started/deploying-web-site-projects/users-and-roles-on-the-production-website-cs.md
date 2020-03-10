---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 生产网站上的用户和角色（C#） |Microsoft Docs
author: rick-anderson
description: ASP.NET 网站管理工具（WSAT）提供了一个基于 web 的用户界面，用于配置成员身份和角色设置，以及创建、编辑 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: c47bd2c1661f129dd8856916de04b8ba459fbfec
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441218"
---
# <a name="users-and-roles-on-the-production-website-c"></a>生产网站上的用户和角色（C#）

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET 网站管理工具（WSAT）提供了一个基于 web 的用户界面，用于配置成员身份和角色设置，以及用于创建、编辑和删除用户和角色。 遗憾的是，WSAT 仅适用于从 localhost 访问的情况，这意味着你无法通过浏览器访问生产网站的管理工具。 好消息是，有一些解决方法，可以在生产环境中管理用户和角色。 本教程将探讨这些解决方法和其他解决方法。

## <a name="introduction"></a>简介

ASP.NET 2.0 引入了多个*应用程序服务*，它们是一套可添加到 web 应用程序中的构建基块服务。 在[*配置使用应用程序服务*教程的网站](configuring-a-website-that-uses-application-services-cs.md)时，我们向书籍评论网站添加了成员身份和角色服务。 成员资格服务简化了用户帐户的创建和管理。角色服务提供了一个 API，用于将用户分类为组。 本书审核网站有三个用户帐户： Scott、Jisun 和 Alice，以及管理员角色中具有 Scott 和 Jisun 的单个角色和管理员。

ASP.NET.网络的应用程序服务不依赖于特定实现。 相反，您需要指示应用程序服务使用特定的*提供程序*，并且该提供程序使用特定的技术实现该服务。 我们已将书籍评论 web 应用程序配置为使用成员身份和角色服务的 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序。 这两个提供程序将用户帐户和角色信息存储在 SQL Server 数据库中，是托管在 web 托管公司的基于 Internet 的 web 应用程序的最常用的提供程序。

使用成员身份和角色服务的开发人员面临的一个常见问题是管理生产环境中的用户和角色。 如何从生产网站删除用户帐户、添加新角色或将现有用户添加到现有角色？ 本教程探讨了用于管理生产网站上的用户和角色的不同技术。

## <a name="using-the-aspnet-web-site-administration-tool"></a>使用 ASP.NET 网站管理工具

ASP.NET 包含一个[网站管理工具](https://msdn.microsoft.com/library/yy40ytx0.aspx)（WSAT），可让用户轻松地创建和管理用户帐户和角色，并指定基于用户和角色的授权规则。 若要使用 WSAT，请在解决方案资源管理器中单击 "ASP.NET 配置" 图标，或单击 "网站" 或 "项目" 菜单，然后选择 "ASP.NET" 配置选项。 这两种方法都将启动 web 浏览器，并将其指向类似于以下地址的 WSAT： `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT 分为三个部分：

- **安全性**-管理用户、角色和授权规则。
- **ApplicationConfiguration** -在此处管理 &lt;appSettings&gt; 和 SMTP 设置。 还可以使应用程序脱机，并在此处管理调试和跟踪设置，并指定默认的自定义错误页。
- **ProviderConfiguration** -配置应用程序服务使用的提供程序。

安全部分（如**图 1**所示）包含用于创建新用户、管理用户、创建和管理角色以及创建和管理访问规则的链接。 在此处，你可以将新角色添加到系统、删除现有用户或在特定用户帐户中添加或删除角色。

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**图 1**： WSAT 安全部分包含用于管理用户和角色的选项  
（[单击以查看完全大小的映像](users-and-roles-on-the-production-website-cs/_static/image3.png)）

遗憾的是，WSAT 只能在本地访问。 你无法访问你的远程生产网站上的 WSAT;如果访问 `www.yoursite.com/asp.netwebadminfiles/default.aspx` 收到 "404 未找到" 响应。 支持 WSAT 的代码使用 .NET Framework 中的 `Membership` 和 `Roles` 类来创建、编辑和删除用户和角色。 这些类参考 web 应用程序的配置信息，以确定要使用的提供程序;返回到[*配置使用应用程序服务*教程的网站](configuring-a-website-that-uses-application-services-cs.md)时，我们将书籍评论网站设置为使用 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序。 这引起将 `<membership>` 和 `<roleManager>` 部分添加到 `Web.config`。

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

请注意，`<membership>` 和 `<roleManager>` 部分分别引用其 `type` 特性中的 `SqlMembershipProvider` 和 `SqlRoleProvider` 提供程序。 这些提供程序将用户和角色信息存储在指定的 SQL Server 数据库中。 这些提供程序使用的数据库由在 `~/ConfigSections/databaseConnectionStrings.config` 文件中定义的 `connectionStringName` 特性 `ReviewsConnectionString`指定。 请记住，开发环境中的 `databaseConnectionStrings.config` 文件包含开发数据库的连接字符串，而生产中的 `databaseConnectionStrings.config` 文件包含生产数据库的连接字符串。

简而言之，必须通过开发环境在本地访问 WSAT，并与 `databaseConnectionStrings.config` 文件中指定的数据库中的用户和角色信息一起工作。 因此，如果在开发环境中更改 `databaseConnectionStrings.config` 文件中的连接字符串信息，则可以在本地使用 WSAT 来管理生产环境中的用户和角色。

为了说明此功能，请在开发环境中打开 Visual Studio 中的 `databaseConnectionStrings.config` 文件，并将开发数据库连接字符串替换为生产数据库连接字符串。 然后，启动 WSAT，前往 "安全" 选项卡，然后添加一个名为 Sam、密码为 "password！" 的新用户。 （少于引号）。 **图 2**显示了创建此帐户时的 "WSAT" 屏幕。

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**图 2**：在生产环境中创建名为 Sam 的新用户  
（[单击以查看完全大小的映像](users-and-roles-on-the-production-website-cs/_static/image6.png)）

由于我们将 `databaseConnectionStrings.config` 中的连接字符串更改为指向生产数据库服务器，因此在生产环境中已将 Sam 添加为用户。 若要验证这一点，请将 `databaseConnectionStrings.config` 文件中的连接字符串更改回开发数据库，然后访问开发环境中的 `Login.aspx` 页。 尝试以 Sam 身份登录（请参阅**图 3**）。

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**图 3**：无法在开发环境中以 Sam 身份登录  
（[单击以查看完全大小的映像](users-and-roles-on-the-production-website-cs/_static/image9.png)）

无法在开发环境中以 Sam 身份登录，因为本地数据库中不存在用户帐户信息。 相反，已添加到生产数据库中。 若要验证这一点，请在开发和生产数据库中查看 `aspnet_Users` 表的内容。 在开发环境中，用户 Scott、Jisun 和 Alice 应该只有三个记录。 不过，生产数据库中的 `aspnet_Users` 表具有四个记录： Scott、Jisun、Alice 和 Sam。 因此，Sam 可以通过生产环境中的网站登录，但不能通过开发环境进行登录。

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**图 4**： Sam 可以在生产网站上登录  
（[单击以查看完全大小的映像](users-and-roles-on-the-production-website-cs/_static/image12.png)）

> [!NOTE]
> 使用 WSAT 完成后，请不要忘记将 `databaseConnectionStrings.config` 文件中的连接字符串更改回开发数据库的连接字符串，否则，在通过开发环境测试站点时将使用生产数据。 另外，请记住，尽管我们刚才讨论的技术允许我们使用 WSAT 来远程管理用户和角色、对任何其他 WSAT 配置选项（访问规则、SMTP 设置、调试和跟踪设置等）的更改，修改 `Web.config` 文件。 因此，对这些设置所做的任何更改都适用于开发环境，不适用于生产环境。

## <a name="creating-custom-user-and-role-management-web-pages"></a>创建自定义用户和角色管理网页

WSAT 提供了用于管理用户和角色的现成系统，但只能在本地启动，并需要对连接字符串信息进行更改，以便管理生产环境中的用户和角色。 大多数支持用户帐户的网站还包括多个用户和角色管理网页，这些网页使管理员能够管理网站中的用户和角色。 此类基于 web 的管理页面使管理用户和角色变得更加容易，并且对于可能有很多管理员或管理员无法访问或使用 Visual Studio 启动 WSAT 的管理员来说非常重要。

ASP.NET 包括许多内置登录相关的 Web 控件，使您可以轻松地将很多这些管理网页实现为拖放。 例如，你可以通过将 CreateUserWizard 控件拖到页面上并设置几个属性，为管理员创建一个用于创建新用户帐户的页面。 事实上，**图 2**所示的 WSAT 中用于创建用户的页面使用的 CreateUserWizard 控件可以添加到页面中。 而且，成员资格和角色服务功能可通过 `Membership` 以编程方式提供，并 `Roles` .NET Framework 中的类。 通过这些类，您可以编写代码来创建、编辑和删除用户和角色，以及在角色中添加或删除用户，以及执行其他用户和与角色相关的任务。

在[*配置使用应用程序服务*教程的网站](configuring-a-website-that-uses-application-services-cs.md)中，我向 `Admin` 文件夹中添加了一个名为 `CreateAccount.aspx`的页面。 此页面允许管理员向站点添加新的用户帐户，并指定新创建的用户是否为管理员角色（请参阅**图 5**）。

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**图 5**：管理员可以创建新的用户帐户  
（[单击以查看完全大小的映像](users-and-roles-on-the-production-website-cs/_static/image15.png)）

若要详细了解如何构建用户和角色管理页，以及如何使用 `Membership` 和 `Roles` 类以及与登录相关的 ASP.NET Web 控件的分步说明，请参阅[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。 你将在其中找到有关如何生成用于创建新帐户、创建和管理角色、将用户分配到角色以及其他常见管理任务的网页的指导。

若要在生产网站上实现类似于 WSAT 的功能，你始终可以构建自己的一系列实现 WSAT 功能的网页。 若要开始，请查看 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`的文件夹中的 WSAT 源代码。 另一种方法是使用 Dan Clem 的 WSAT 替代项，他在本文中分享[自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)。 Dan 会指导读者完成构建类似于 WSAT 的自定义工具的过程，包括其应用程序用于下载的源代码（ C#在中为），并提供有关将自定义的 WSAT 添加到托管网站的逐步说明。

## <a name="summary"></a>摘要

ASP.NET 网站管理工具（WSAT）可与成员资格和角色应用程序服务结合使用，以管理您的网站的用户和角色信息。 遗憾的是，WSAT 只能在本地访问，不能从您的生产网站访问。 但是，通过将开发环境中的连接字符串更改为指向生产数据库，你可以使用 WSAT 来管理生产网站上的用户和角色。

尽管 WSAT 方法可以快速轻松地管理用户和角色，但它需要从 Visual Studio 启动 WSAT 以及对连接字符串信息进行临时更改。 WSAT 提供了在生产环境中管理用户和角色的快速方法，但对于具有多个管理员的网站或没有或不熟悉 Visual Studio 和 WSAT 的管理员而言，此方法不能正常工作。 由于这些原因，大多数支持用户帐户的网站都包含一组管理网页。 这样的一组网页消除了 WSAT 的需要，并由任何计算机的各种管理用户使用。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [正在检查 ASP。网络的成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [网站管理工具概述](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [上一页](precompiling-your-website-cs.md)
> [下一页](asp-net-hosting-options-vb.md)
