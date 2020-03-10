---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
title: 创建和管理角色（C#） |Microsoft Docs
author: rick-anderson
description: 本教程将探讨配置角色框架所需的步骤。 接下来，我们将构建网页来创建和删除角色。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 113f10b3-a19a-471b-8ff6-db3c79ce8a91
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
msc.type: authoredcontent
ms.openlocfilehash: a7883d0b05f2fa5a3fdac887f8c8b39d70418fb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520064"
---
# <a name="creating-and-managing-roles-c"></a>创建和管理角色 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.09.zip)或[下载 PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_cs.pdf)

> 本教程将探讨配置角色框架所需的步骤。 接下来，我们将构建网页来创建和删除角色。

## <a name="introduction"></a>简介

<a id="_msoanchor_1"></a>在[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程中，我们探讨了如何使用 URL 授权来限制一组页面中的某些用户，并探索了用于根据访问用户调整 ASP.NET 页面功能的声明性和编程技术。 但是，授予每个用户的页面访问权限或功能的权限，在存在多个用户帐户或用户的特权经常更改的情况下，这种情况会成为一项维护工作。 用户任何时候获得或失去执行特定任务的授权时，管理员都需要更新相应的 URL 授权规则、声明性标记和代码。

它通常有助于将用户划分到组或*角色*中，然后对角色按角色应用权限。 例如，大多数 web 应用程序都有一组特定的页面或任务，它们只为管理用户预留。 使用*基于用户的授权*教程中学习的技术，我们将添加相应的 URL 授权规则、声明性标记和代码，以允许指定的用户帐户执行管理任务。 但是，如果添加了新的管理员，或者如果现有管理员已撤消管理权限，则必须返回并更新配置文件和网页。 然而，使用角色，我们可以创建一个名为 "管理员" 的角色，并将这些受信任的用户分配给 "管理员" 角色。 接下来，我们将添加相应的 URL 授权规则、声明性标记和代码，以允许管理员角色执行各种管理任务。 此基础结构准备就绪后，将新管理员添加到该站点或删除现有管理员非常简单，只需要从管理员角色中包括或删除用户即可。 无需进行配置、声明性标记或代码更改。

ASP.NET 提供角色框架，用于定义角色并将其与用户帐户相关联。 使用角色框架，我们可以创建和删除角色，向角色添加用户或从中删除用户，确定属于特定角色的用户组，并判断用户是否属于特定角色。 配置角色框架后，我们可以通过 URL 授权规则限制每个角色对页面的访问，并基于当前登录用户的角色在页面上显示或隐藏其他信息或功能。

本教程将探讨配置角色框架所需的步骤。 接下来，我们将构建网页来创建和删除角色。 在将<a id="_msoanchor_2"> </a>[*角色分配给用户*](assigning-roles-to-users-cs.md)教程中，我们将介绍如何在角色中添加和删除用户。 在<a id="_msoanchor_3"> </a>[*基于角色的授权*](role-based-authorization-cs.md)教程中，我们将了解如何按角色限制对页面的访问，以及如何根据访问用户的角色调整页面功能。 让我们进入正题！

## <a name="step-1-adding-new-aspnet-pages"></a>步骤1：添加新的 ASP.NET 页面

在本教程和接下来的两个教程中，我们将检查各种与角色相关的函数和功能。 我们将需要一系列 ASP.NET 页面来实现这些教程中所讨论的主题。 让我们创建这些页面并更新站点图。

首先，在项目中创建一个名为 `Roles`的新文件夹。 接下来，将四个新的 ASP.NET 页面添加到 `Roles` 文件夹，将每个页面与 `Site.master` 的母版页链接。 命名页面：

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

此时，项目的解决方案资源管理器应类似于图1所示的屏幕截图。

[已将四个新页面添加到 "角色" 文件夹中 ![](creating-and-managing-roles-cs/_static/image2.png)](creating-and-managing-roles-cs/_static/image1.png)

**图 1**：已将四个新页面添加到 `Roles` 文件夹（[单击查看完全大小的图像](creating-and-managing-roles-cs/_static/image3.png)）

此时，每个页面都应具有两个内容控件，一个用于母版页的每个 Contentplaceholder： `MainContent` 和 `LoginContent`。

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample1.aspx)]

请记住，`LoginContent` ContentPlaceHolder 的默认标记会显示一个用于登录或注销站点的链接，具体取决于是否对用户进行了身份验证。 但在 ASP.NET 页中存在 `Content2` 内容控件，但会重写母版页的默认标记。 如我们在<a id="_msoanchor_4"> </a> [*Forms 身份验证概述*](../introduction/an-overview-of-forms-authentication-cs.md)教程中所述，替代默认标记对于我们不想在左列中显示与登录相关的选项的页面非常有用。

但对于这四个页面，我们想要为 `LoginContent` ContentPlaceHolder 显示母版页的默认标记。 因此，删除 `Content2` 内容控件的声明性标记。 完成此操作后，四个页面的标记中的每一个都应该只包含一个内容控件。

最后，让我们更新网站图（`Web.sitemap`）以包含这些新网页。 在为成员资格教程添加的 `<siteMapNode>` 后面添加以下 XML。

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample2.xml)]

更新站点地图后，通过浏览器访问站点。 如图2所示，左侧的导航包含角色教程中的项。

[已将四个新页面添加到 "角色" 文件夹中 ![](creating-and-managing-roles-cs/_static/image5.png)](creating-and-managing-roles-cs/_static/image4.png)

**图 2**：已将四个新页面添加到 `Roles` 文件夹（[单击查看完全大小的图像](creating-and-managing-roles-cs/_static/image6.png)）

## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>步骤2：指定和配置角色框架提供程序

与成员身份框架一样，角色框架是在提供程序模型的顶层生成的。 如<a id="_msoanchor_5"> </a>[*安全基础知识和 ASP.NET 支持*](../introduction/security-basics-and-asp-net-support-cs.md)教程中所述，.NET Framework 附带了三个内置角色提供商： [`AuthorizationStoreRoleProvider`](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx)、 [`WindowsTokenRoleProvider`](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)和[`SqlRoleProvider`](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)。 本教程系列重点介绍 `SqlRoleProvider`，它使用 Microsoft SQL Server 数据库作为角色存储。

下面的内容涵盖角色框架和 `SqlRoleProvider` 工作，就像成员身份框架和 `SqlMembershipProvider`一样。 .NET Framework 包含一个 `Roles` 类，该类充当角色框架的 API。 `Roles` 类具有静态方法，如 `CreateRole`、`DeleteRole`、`GetAllRoles`、`AddUserToRole`、`IsUserInRole`等。 当调用其中一种方法时，`Roles` 类会将调用委托给已配置的提供程序。 `SqlRoleProvider` 与特定于角色的表（`aspnet_Roles` 和 `aspnet_UsersInRoles`）一起使用以响应。

若要在应用程序中使用 `SqlRoleProvider` 提供程序，需要指定要用作存储的数据库。 `SqlRoleProvider` 要求指定的角色存储具有某些数据库表、视图和存储过程。 可以使用[`aspnet_regsql.exe` 工具](https://msdn.microsoft.com/library/ms229862.aspx)添加这些必需的数据库对象。 此时，我们已经有了一个数据库，其中包含 `SqlRoleProvider`所需的架构。 <a id="_msoanchor_6"></a>返回 SQL Server 教程创建[*成员身份架构*](../membership/creating-the-membership-schema-in-sql-server-cs.md)中创建一个名为 `SecurityTutorials.mdf` 的数据库，并使用 `aspnet_regsql.exe` 添加应用程序服务，其中包括 `SqlRoleProvider`所需的数据库对象。 因此，只需告诉角色框架启用角色支持并将 `SqlRoleProvider` 与 `SecurityTutorials.mdf` 数据库作为角色存储。

角色框架是通过应用程序 `Web.config` 文件中的 &lt;`roleManager`&gt; 元素配置的。 默认情况下，禁用角色支持。 若要启用它，必须将[&lt;`roleManager`&gt;](https://msdn.microsoft.com/library/ms164660.aspx)元素的 `enabled` 特性设置为，`true` 如下所示：

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample3.xml)]

默认情况下，所有 web 应用程序都有一个名为 `AspNetSqlRoleProvider` 类型 `SqlRoleProvider`的角色提供程序。 此默认提供程序在 `machine.config` 中注册（位于 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`）：

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample4.xml)]

提供程序的 `connectionStringName` 属性指定使用的角色存储区。 `AspNetSqlRoleProvider` 提供程序将此属性设置为 `LocalSqlServer`，默认情况下，它也在 `machine.config` 和点中定义为名为 `App_Data` `aspnet.mdf`文件夹中的 SQL Server 2005 Express Edition 数据库。

因此，如果只是启用角色框架而不在应用程序的 `Web.config` 文件中指定任何提供程序信息，则应用程序将使用默认注册的角色提供程序，`AspNetSqlRoleProvider`。 如果 `~/App_Data/aspnet.mdf` 数据库不存在，ASP.NET 运行时将自动创建它并添加应用程序服务架构。 但是，我们不想使用 `aspnet.mdf` 数据库;相反，我们想要使用已创建的 `SecurityTutorials.mdf` 数据库，并将应用程序服务架构添加到。 可以通过以下两种方式之一完成此修改：

- 为<strong>`Web.config`</strong>中<strong>`LocalSqlServer`</strong><strong>连接字符串名称</strong><strong>指定值</strong> <strong>。</strong> 通过覆盖 `Web.config`中的 `LocalSqlServer` 连接字符串名称值，我们可以使用默认的已注册角色提供程序（`AspNetSqlRoleProvider`）并使其与 `SecurityTutorials.mdf` 数据库一起正确使用。 有关此技术的详细信息，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章将[ASP.NET 2.0 应用程序服务配置为使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)。
- <strong>添加`SqlRoleProvider`类型的新注册的提供程序</strong> <strong>，并将其</strong><strong>`connectionStringName`</strong><strong>设置配置为指向</strong><strong>`SecurityTutorials.mdf`</strong><strong>数据库。</strong> 这是我在<a id="_msoanchor_7"> </a> [*SQL Server 教程中创建成员身份架构*](../membership/creating-the-membership-schema-in-sql-server-cs.md)时建议和使用的方法，也是我将在本教程中使用的方法。

将以下角色配置标记添加到 `Web.config` 文件中。 此标记将注册一个名为 `SecurityTutorialsSqlRoleProvider`的新提供程序。

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample5.xml)]

上面的标记将 `SecurityTutorialsSqlRoleProvider` 定义为默认提供程序（通过 `<roleManager>` 元素中的 `defaultProvider` 特性）。 它还将 `SecurityTutorialsSqlRoleProvider`的 `applicationName` 设置设置为 `SecurityTutorials`，这与成员资格提供程序（`SecurityTutorialsSqlMembershipProvider`）使用的 `applicationName` 设置相同。 尽管此处未显示，但 `SqlRoleProvider` 的[`<add>` 元素](https://msdn.microsoft.com/library/ms164662.aspx)还可能包含一个 `commandTimeout` 属性，用于指定数据库超时持续时间（以秒为单位）。 默认值为 30。

使用此配置标记后，便可以开始在应用程序中使用角色功能。

> [!NOTE]
> 上述配置标记说明了如何使用 &lt;`roleManager`&gt; 元素的 `enabled` 和 `defaultProvider` 特性。 还有多个其他属性会影响角色框架如何按用户关联角色信息。 我们会在<a id="_msoanchor_8"> </a>[*基于角色的授权*](role-based-authorization-cs.md)教程中检查这些设置。

## <a name="step-3-examining-the-roles-api"></a>步骤3：检查角色 API

Role framework 的功能通过[`Roles` 类](https://msdn.microsoft.com/library/system.web.security.roles.aspx)公开，该类包含用于执行基于角色的操作的十三个静态方法。 在步骤4和6中查看创建和删除角色时，将使用[`CreateRole`](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx)和[`DeleteRole`](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx)方法，这些方法可在系统中添加或删除角色。

若要获取系统中所有角色的列表，请使用[`GetAllRoles` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)（请参阅步骤5）。 [`RoleExists` 方法](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx)返回一个布尔值，该值指示指定的角色是否存在。

在下一教程中，我们将介绍如何将用户与角色相关联。 `Roles` 类的[`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)、 [`AddUserToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx)、 [`AddUsersToRole`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)和[`AddUsersToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx)方法将一个或多个用户添加到一个或多个角色。 若要从角色中删除用户，请使用[`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)、 [`RemoveUserFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx)、 [`RemoveUsersFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)或[`RemoveUsersFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx)方法。

<a id="_msoanchor_9"></a>在[*基于角色的授权*](role-based-authorization-cs.md)教程中，我们将探讨如何基于当前登录用户的角色以编程方式显示或隐藏功能。 为实现此目的，可以使用 `Role` 类的[`FindUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx)、 [`GetRolesForUser`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)、 [`GetUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)或[`IsUserInRole`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)方法。

> [!NOTE]
> 请记住，只要调用其中一种方法，`Roles` 类就会将调用委托给已配置的提供程序。 在我们的示例中，这意味着调用发送到 `SqlRoleProvider`。 然后，`SqlRoleProvider` 基于调用的方法执行相应的数据库操作。 例如，代码 `Roles.CreateRole("Administrators")` 生成 `SqlRoleProvider` 执行 `aspnet_Roles_CreateRole` 存储过程，该过程将新记录插入到名为 Administrators 的 `aspnet_Roles` 表中。

本教程的其余部分介绍如何使用 `Roles` 类的 `CreateRole`、`GetAllRoles`和 `DeleteRole` 方法来管理系统中的角色。

## <a name="step-4-creating-new-roles"></a>步骤4：创建新角色

角色提供了任意分组用户的方式，并且大多数情况下，这种分组用于更方便地应用授权规则。 但是，若要使用角色作为授权机制，首先需要定义应用程序中存在哪些角色。 遗憾的是，ASP.NET 不包含 CreateRoleWizard 控件。 为了添加新的角色，我们需要创建合适的用户界面，并亲自调用角色 API。 好消息是，这很容易完成。

> [!NOTE]
> 尽管没有 CreateRoleWizard Web 控件，但仍有 ASP.NET 的网站[管理工具](https://msdn.microsoft.com/library/ms228053.aspx)，该工具是一个本地 ASP.NET 应用程序，旨在帮助查看和管理 Web 应用程序的配置。 但是，由于两个原因，我并不是 ASP.NET 网站管理工具的一个大风扇。 首先，这是一个很大的错误，用户体验会很有必要。 其次，ASP.NET 网站管理工具设计为仅在本地工作，这意味着，如果需要远程管理活动站点上的角色，则必须构建自己的角色管理网页。 出于这两个原因，本教程和下一个教程将重点介绍如何在网页中构建必要的角色管理工具，而不是依赖于 ASP.NET 网站管理工具。

打开 `Roles` 文件夹中的 "`ManageRoles.aspx`" 页，并向页面添加一个文本框和一个按钮 Web 控件。 将 TextBox 控件的 `ID` 属性设置为 `RoleName`，按钮的 `ID` 和 `Text` 属性分别设置为 `CreateRoleButton` 和创建角色。 此时，页面的声明性标记应如下所示：

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample6.aspx)]

接下来，双击设计器中的 "`CreateRoleButton`" 按钮控件以创建 `Click` 事件处理程序，然后添加以下代码：

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample7.cs)]

上面的代码首先将在 "`RoleName`" 文本框中输入的剪裁角色名称分配给 `newRoleName` 变量。 接下来，调用 `Roles` 类的 `RoleExists` 方法来确定系统中是否已存在该角色 `newRoleName`。 如果角色不存在，则通过调用 `CreateRole` 方法创建。 如果向 `CreateRole` 方法传递系统中已存在的角色名称，则会引发 `ProviderException` 异常。 这就是代码首次检查以确保在调用 `CreateRole`之前该角色在系统中不存在的原因。 `Click` 事件处理程序通过清除 `RoleName` 文本框的 `Text` 属性来结束。

> [!NOTE]
> 如果用户没有在 "`RoleName`" 文本框中输入任何值，可能会想知道发生了什么情况。 如果传递到 `CreateRole` 方法的值为 `null` 或空字符串，则会引发异常。 同样，如果角色名称包含逗号，则会引发异常。 因此，页面应包含验证控件，以确保用户输入角色并且不包含任何逗号。 我为读者作了练习。

让我们创建一个名为 "管理员" 的角色。 通过浏览器访问 `ManageRoles.aspx` 页面，在文本框中键入 "管理员" （参见图3），然后单击 "创建角色" 按钮。

[![创建管理员角色](creating-and-managing-roles-cs/_static/image8.png)](creating-and-managing-roles-cs/_static/image7.png)

**图 3**：创建管理员角色（[单击以查看完全大小的映像](creating-and-managing-roles-cs/_static/image9.png)）

发生了什么情况？ 发生回发，但没有视觉提示，指出该角色实际上已添加到系统中。 我们将在步骤5中更新此页面以包括视觉反馈。 不过，现在可以通过转到 `SecurityTutorials.mdf` 数据库并显示 `aspnet_Roles` 表中的数据来验证角色是否已创建。 如图4所示，`aspnet_Roles` 表包含刚添加的管理员角色的记录。

[![aspnet_Roles 表有一个适用于管理员的行](creating-and-managing-roles-cs/_static/image11.png)](creating-and-managing-roles-cs/_static/image10.png)

**图 4**： "`aspnet_Roles`" 表为管理员提供了一行（[单击以查看完全大小的图像](creating-and-managing-roles-cs/_static/image12.png)）

## <a name="step-5-displaying-the-roles-in-the-system"></a>步骤5：显示系统中的角色

增加 `ManageRoles.aspx` 页面，使其包含系统中当前角色的列表。 若要实现此目的，请将 GridView 控件添加到页面，并将其 `ID` 属性设置为 `RoleList`。 接下来，使用以下代码将方法添加到名为 `DisplayRolesInGrid` 的页的代码隐藏类：

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample8.cs)]

`Roles` 类的 `GetAllRoles` 方法以字符串数组的形式返回系统中的所有角色。 然后，将此字符串数组绑定到 GridView。 若要在第一次加载页面时将角色列表绑定到 GridView，需要从页面的 `Page_Load` 事件处理程序中调用 `DisplayRolesInGrid` 方法。 当首次访问页面时，以下代码调用此方法，而不是在后续回发时调用。

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample9.cs)]

使用此代码后，请通过浏览器访问此页。 如图5所示，你应该看到一个网格，其中包含一个标记为 "Item" 的列。 网格为在步骤4中添加的管理员角色包含一行。

[![GridView 显示单个列中的角色](creating-and-managing-roles-cs/_static/image14.png)](creating-and-managing-roles-cs/_static/image13.png)

**图 5**： GridView 显示单个列中的角色（[单击以查看完全大小的图像](creating-and-managing-roles-cs/_static/image15.png)）

GridView 将显示一个标记为 "Item" 的列，因为 GridView 的 `AutoGenerateColumns` 属性设置为 True （默认值），这会导致 GridView 自动为其 `DataSource`中的每个属性创建一个列。 数组有一个属性，该属性表示数组中的元素，因此是 GridView 中的单个列。

使用 GridView 显示数据时，我更喜欢显式定义列，而不是由 GridView 隐式生成。 通过显式定义列，可以更轻松地对数据进行格式设置、重新排列列以及执行其他常见任务。 因此，让我们更新 GridView 的声明性标记，以便显式定义其列。

首先，将 GridView 的 `AutoGenerateColumns` 属性设置为 False。 接下来，将 "TemplateField" 添加到网格，将其 `HeaderText` 属性设置为 "角色"，并将其 `ItemTemplate` 配置为显示数组的内容。 若要实现此目的，请将名为 `RoleNameLabel` 的标签 Web 控件添加到 `ItemTemplate`，并将其 `Text` 属性绑定到 `Container.DataItem`。

可以通过声明方式或通过 GridView 的 "字段" 对话框和编辑模板界面来设置这些属性和 `ItemTemplate`的内容。 若要访问 "字段" 对话框，请单击 GridView 智能标记中的 "编辑列" 链接。 接下来，取消选中 "自动生成字段" 复选框，将 `AutoGenerateColumns` 属性设置为 False，并将 TemplateField 添加到 GridView，并将其 `HeaderText` 属性设置为 Role。 若要定义 `ItemTemplate`的内容，请从 GridView 的智能标记选择 "编辑模板" 选项。 将标签 Web 控件拖动到 `ItemTemplate`上，将其 `ID` 属性设置为 `RoleNameLabel`，并配置其数据绑定设置，以便将其 `Text` 属性绑定到 `Container.DataItem`。

不管你使用哪种方法，在完成后，GridView 生成的声明性标记应类似于以下内容。

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample10.aspx)]

> [!NOTE]
> 使用数据绑定语法 `<%# Container.DataItem %>`显示数组的内容。 有关在显示绑定到 GridView 的数组内容时使用此语法的详细说明，不在本教程的讨论范围之内。 有关此问题的详细信息，请参阅将[标量数组绑定到数据 Web 控件](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)。

目前，在首次访问页面时，`RoleList` GridView 仅绑定到角色列表。 需要在添加新角色时刷新网格。 若要完成此操作，请更新 "`CreateRoleButton`" 按钮的 `Click` 事件处理程序，以便在创建新角色时调用 `DisplayRolesInGrid` 方法。

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample11.cs)]

现在，当用户添加新角色时，`RoleList` GridView 会在回发时显示刚刚添加的角色，并提供成功创建角色的视觉反馈。 为了说明这一点，请通过浏览器访问 `ManageRoles.aspx` 页面，并添加一个名为监察员的角色。 单击 "创建角色" 按钮后，将不幸回发，并将更新网格，使其包括管理员以及新的角色监察员。

[已添加 "监察员" 角色 ![](creating-and-managing-roles-cs/_static/image17.png)](creating-and-managing-roles-cs/_static/image16.png)

**图 6**：添加了 "监察员" 角色（[单击以查看完全大小的映像](creating-and-managing-roles-cs/_static/image18.png)）

## <a name="step-6-deleting-roles"></a>步骤6：删除角色

此时，用户可以创建新角色，并从 "`ManageRoles.aspx`" 页查看所有现有角色。 允许用户也删除角色。 `Roles.DeleteRole` 方法有两个重载：

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) -*删除角色角色*。 如果角色包含一个或多个成员，则会引发异常。
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) -*删除角色角色*。 如果 `true`*throwOnPopulateRole* ，则在角色包含一个或多个成员时将引发异常。 如果 `false`*throwOnPopulateRole* ，则无论角色是否包含任何成员，都将被删除。 在内部，`DeleteRole(roleName)` 方法调用 `DeleteRole(roleName, true)`。

如果使用了 "工作的 `null`" 或 "空字符串" 或 *"包含逗号* *"，则*`DeleteRole` 方法也将引发异常。 如果*系统中不存在*该工作项，`DeleteRole` 会悄悄地失败，而不会引发异常。

接下来，我们将 `ManageRoles.aspx` 中的 GridView 补充为包含一个删除按钮，单击该按钮将删除所选角色。 首先将 "删除" 按钮添加到 GridView，方法是转到 "字段" 对话框并添加 "删除" 按钮，该按钮位于 "CommandField" 选项下。 使 "删除" 按钮成为最左侧的列，并将其 `DeleteText` 属性设置为 "删除角色"。

[![向 RoleList GridView 添加 "删除" 按钮](creating-and-managing-roles-cs/_static/image20.png)](creating-and-managing-roles-cs/_static/image19.png)

**图 7**：将 "删除" 按钮添加到 `RoleList` GridView （[单击以查看完全大小的图像](creating-and-managing-roles-cs/_static/image21.png)）

添加 "删除" 按钮后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample12.aspx)]

接下来，为 GridView 的 `RowDeleting` 事件创建事件处理程序。 这是在单击 "删除角色" 按钮时对回发引发的事件。 将以下代码添加到该事件处理程序中。

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample13.cs)]

代码首先以编程方式在单击了 "删除角色" 按钮的行中引用 `RoleNameLabel` Web 控件。 然后调用 `Roles.DeleteRole` 方法，并传入 `RoleNameLabel` 和 `false`的 `Text`，从而删除角色，无论是否存在任何与该角色关联的用户。 最后，将刷新 `RoleList` GridView，使刚删除的角色不再出现在网格中。

> [!NOTE]
> 删除角色之前，"删除角色" 按钮不需要用户进行任何类型的确认。 确认操作的最简单方法之一是通过客户端确认对话框。 有关此技术的详细信息，请参阅[删除时添加客户端确认](https://asp.net/learn/data-access/tutorial-42-cs.aspx)。

## <a name="summary"></a>摘要

许多 web 应用程序都有某些授权规则或页面级别的功能，这些功能仅适用于某些类的用户。 例如，可能有一组只有管理员才能访问的网页。 通常，根据角色定义规则更有用，而不是逐个用户地定义这些授权规则。 也就是说，更易于维护的方法是允许管理员角色的成员访问这些页面，然后将 Scott 和 Jisun 表示为用户，而不是明确地允许用户 Jisun 访问管理网页。Administrators 角色。

角色框架可以轻松创建和管理角色。 在本教程中，我们介绍了如何将角色框架配置为使用 `SqlRoleProvider`，后者使用 Microsoft SQL Server 数据库作为角色存储。 我们还创建了一个网页，其中列出了系统中的现有角色，并允许创建新角色并删除现有角色。 在后续教程中，我们将了解如何将用户分配到角色，以及如何应用基于角色的授权。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [检查 ASP.NET 2.0 的成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何：在 ASP.NET 2.0 中使用角色管理器](https://msdn.microsoft.com/library/ms998314.aspx)
- [角色提供程序](https://msdn.microsoft.com/library/aa478950.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [`<roleManager>` 元素的技术文档](https://msdn.microsoft.com/library/ms164660.aspx)
- [使用成员身份和角色管理器 Api](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者包括 Alicja Maziarz、Suchi Banerjee 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一部分](assigning-roles-to-users-cs.md)
