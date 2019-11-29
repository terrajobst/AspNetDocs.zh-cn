---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-cs
title: 基于角色的授权（C#） |Microsoft Docs
author: rick-anderson
description: 本教程首先介绍角色框架如何将用户的角色与安全上下文相关联。 然后，它会检查如何应用基于角色的 URL 。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 4d9b63fa-c3d4-4e85-82b1-26ae3ba3ca1c
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 46153ab310bdee814baaa53c372fb92f8a23ce11
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619938"
---
# <a name="role-based-authorization-c"></a>基于角色的授权 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.11.zip)或[下载 PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_cs.pdf)

> 本教程首先介绍角色框架如何将用户的角色与安全上下文相关联。 然后，它会检查如何应用基于角色的 URL 授权规则。 接下来，我们将探讨如何使用声明性和编程方式来更改所显示的数据和 ASP.NET 页提供的功能。

## <a name="introduction"></a>简介

<a id="_msoanchor_1"></a>在[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程中，我们看到了如何使用 URL 授权来指定哪些用户可以访问一组特定页面。 只需在 `Web.config`中使用少量标记，我们就可以指示 ASP.NET 仅允许经过身份验证的用户访问某个页面。 或者，我们可以规定只允许用户 Tito 和 Bob，或指示允许除 Sam 之外的所有经过身份验证的用户。

除了 URL 授权之外，我们还介绍了用于控制显示的数据的声明性和编程技术，以及基于用户访问权限的页提供的功能。 特别是，我们创建了一个列出当前目录内容的页面。 任何人都可以访问此页，但只有经过身份验证的用户可以查看文件的内容，只有 Tito 可以删除这些文件。

按用户应用授权规则可能会增加簿记。 更易于维护的方法是使用基于角色的授权。 好消息是，我们为应用授权规则而处理的工具与使用用户帐户时所用的角色相同。 URL 授权规则可以指定角色而不是用户。 为经过身份验证和匿名用户呈现不同输出的登录视图控件可配置为基于登录用户的角色显示不同的内容。 角色 API 包含用于确定已登录用户的角色的方法。

本教程首先介绍角色框架如何将用户的角色与安全上下文相关联。 然后，它会检查如何应用基于角色的 URL 授权规则。 接下来，我们将探讨如何使用声明性和编程方式来更改所显示的数据和 ASP.NET 页提供的功能。 让我们进入正题！

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>了解角色如何与用户的安全上下文关联

每当请求进入 ASP.NET 管道时，它就会与安全上下文关联，其中包括标识请求者的信息。 使用窗体身份验证时，身份验证票证用作标识令牌。 如我们在<a id="_msoanchor_2"> </a> [*forms 身份验证*](../introduction/an-overview-of-forms-authentication-cs.md)和<a id="_msoanchor_3"> </a> [*forms 身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教程的概述中所述，`FormsAuthenticationModule` 负责确定请求程序的标识，这是在[`AuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)期间进行的。

如果找到有效的、未过期的身份验证票证，则 `FormsAuthenticationModule` 对其进行解码以确定请求者的标识。 它将创建一个新的 `GenericPrincipal` 对象并将其分配给 `HttpContext.User` 对象。 主体（如 `GenericPrincipal`）的用途是标识已经过身份验证的用户的名称以及她所属的角色。 这一目的很明显，所有主体对象都具有 `Identity` 属性和 `IsInRole(roleName)` 方法。 但 `FormsAuthenticationModule`对记录角色信息不感兴趣，并且它创建的 `GenericPrincipal` 对象不会指定任何角色。

如果启用了 Role framework，则[`RoleManagerModule`](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx)的 HTTP 模块将在 `FormsAuthenticationModule` 后步骤中的步骤，并在[`PostAuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)期间（该事件在 `AuthenticateRequest` 事件之后触发）确定经过身份验证的用户的角色。 如果请求来自经过身份验证的用户，则 `RoleManagerModule` 覆盖 `FormsAuthenticationModule` 创建的 `GenericPrincipal` 对象，并将其替换为[`RolePrincipal` 对象](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)。 `RolePrincipal` 类使用角色 API 来确定用户所属的角色。

图1描述了使用 forms 身份验证和角色框架时的 ASP.NET 管道工作流。 首先执行 `FormsAuthenticationModule`，通过其身份验证票证来标识用户，并创建新的 `GenericPrincipal` 对象。 接下来，`RoleManagerModule` 中的步骤，并用 `RolePrincipal` 对象覆盖 `GenericPrincipal` 对象。

如果匿名用户访问该站点，则 `FormsAuthenticationModule` 和 `RoleManagerModule` 都不会创建主体对象。

[使用窗体身份验证和角色框架时，为经过身份验证的用户 ![ASP.NET 管道事件](role-based-authorization-cs/_static/image2.png)](role-based-authorization-cs/_static/image1.png)

**图 1**：使用窗体身份验证和角色框架时经过身份验证的用户的 ASP.NET 管道事件（[单击以查看完全大小的图像](role-based-authorization-cs/_static/image3.png)）

### <a name="caching-role-information-in-a-cookie"></a>在 Cookie 中缓存角色信息

`RolePrincipal` 对象的 `IsInRole(roleName)` 方法将调用 `Roles.GetRolesForUser` 以获取用户的角色，以便确定用户是否为角色*角色的成员。* 使用 `SqlRoleProvider`时，这会导致对角色存储数据库的查询。 使用基于角色的 URL 授权规则时，将针对每个请求调用 `RolePrincipal`的 `IsInRole` 方法，该页面受基于角色的 URL 授权规则保护。 角色框架提供一个选项，用于在 cookie 中缓存用户的角色，而不必在每次请求时都查找数据库中的角色信息。

如果角色框架配置为在 cookie 中缓存用户的角色，则 `RoleManagerModule` 在 ASP.NET 管道的[`EndRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)中创建 cookie。 此 cookie 用于 `PostAuthenticateRequest`的后续请求中，这是创建 `RolePrincipal` 对象的时间。 如果 cookie 有效且未过期，则会分析 cookie 中的数据，并使用该数据填充用户的角色，从而保存 `RolePrincipal` 不必调用 `Roles` 类来确定用户的角色。 图2描绘了此工作流。

[![用户的角色信息可以存储在一个 Cookie 中，以提高性能](role-based-authorization-cs/_static/image5.png)](role-based-authorization-cs/_static/image4.png)

**图 2**：用户的角色信息可以存储在一个 Cookie 中，以提高性能（[单击查看完全大小的映像](role-based-authorization-cs/_static/image6.png)）

默认情况下，角色缓存 cookie 机制处于禁用状态。 可以通过 `Web.config`中的 `<roleManager>` 配置标记来启用此功能。 我们在<a id="_msoanchor_4"> </a>[*创建和管理角色*](creating-and-managing-roles-cs.md)教程中讨论了如何使用[`<roleManager>` 元素](https://msdn.microsoft.com/library/ms164660.aspx)来指定角色提供程序，因此，你应在应用程序的 `Web.config` 文件中具有此元素。 角色缓存 cookie 设置被指定为 `<roleManager>` 元素的属性，并在表1中汇总。

> [!NOTE]
> 表1中列出的配置设置指定了生成的角色缓存 cookie 的属性。 若要详细了解 cookie 及其工作原理，请阅读[此 cookie 教程](http://www.quirksmode.org/js/cookies.html)。

| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>描述</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              指示是否使用 cookie 缓存的布尔值。 默认为 `false`。                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     角色缓存 cookie 的名称。 默认值为 ".ASPXROLES "。                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                角色名称 cookie 的路径。 使用 path 特性，开发人员可以将 cookie 的作用域限制为特定的目录层次结构。 默认值为 "/"，通知浏览器将身份验证票证 cookie 发送到向域发出的任何请求。                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               指示用于保护角色缓存 cookie 的技术。 允许的值为： `All` （默认值）;`Encryption`;`None`;和 `Validation`。 有关这些保护级别的详细信息<a id="_anchor_5"> </a>，请参阅[*Forms 身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教程中的步骤3。                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   一个布尔值，指示是否需要 SSL 连接来传输身份验证 cookie。 默认值为 `false`。                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  指示每次用户在单个会话期间访问站点时是否重置 cookie 的超时值的布尔值。 默认值为 `false`。 仅当 `createPersistentCookie` 设置为 `true`时，此值才相关。                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         指定身份验证票证 cookie 过期的时间，以分钟为单位。 默认值为 `30`。 仅当 `createPersistentCookie` 设置为 `true`时，此值才相关。                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   一个布尔值，指定角色缓存 cookie 是会话 cookie 还是永久性 cookie。 如果 `false` （默认值），则使用会话 cookie，当浏览器关闭时将删除该 cookie。 如果 `true`，则使用持久性 cookie;它在创建后或上一次访问之后 `cookieTimeout` 的分钟数过期，具体取决于 `cookieSlidingExpiration`的值。                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 指定 cookie 的域值。 默认值为空字符串，这将使浏览器使用其发出的域（如 www.yourdomain.com）。 在这种情况下，在向子域发出请求（如 admin.yourdomain.com）时，<strong>不</strong>会发送 cookie。 如果要将 cookie 传递给所有子域，则需要自定义 `domain` 属性，并将其设置为 "yourdomain.com"。                                                                                                                                                 |
|    `maxCachedResults`     | 指定 cookie 中缓存的角色名称的最大数目。 默认值为 25。 `RoleManagerModule` 不会为属于多个 `maxCachedResults` 角色的用户创建 cookie。 因此，`RolePrincipal` 对象的 `IsInRole` 方法将使用 `Roles` 类来确定用户的角色。 `maxCachedResults` 存在的原因是许多用户代理不允许 cookie 大于4096字节。 因此，此上限旨在降低超过此大小限制的可能性。 如果角色名称非常长，请考虑指定一个较小的 `maxCachedResults` 值;contrariwise，如果你有极短的角色名称，则可能会增加此值。 |

**表1：** 角色缓存 Cookie 配置选项

让我们将应用程序配置为使用非持久性角色缓存 cookie。 若要实现此目的，请更新 `Web.config` 中的 `<roleManager>` 元素，使其包含以下与 cookie 相关的属性：

[!code-xml[Main](role-based-authorization-cs/samples/sample1.xml)]

我通过添加三个属性来更新 `<roleManager>` 元素： `cacheRolesInCookie`、`createPersistentCookie`和 `cookieProtection`。 通过将 `cacheRolesInCookie` 设置为 `true`，`RoleManagerModule` 现在会自动在 cookie 中缓存用户的角色，而不必在每个请求上查找用户的角色信息。 我将 `createPersistentCookie` 和 `cookieProtection` 属性分别设置为 `false` 和 `All`。 从技术上说，我不需要指定这些属性的值，因为我只是将其分配给了默认值，但我将它们放在此处以明确指出，我不使用永久性 cookie，并且 cookie 同时经过加密和验证。

就这么简单！ 之后，角色框架将在 cookie 中缓存用户的角色。 如果用户的浏览器不支持 cookie，或者如果删除或丢失了 cookie，则这一点很重要– `RolePrincipal` 对象只会使用 `Roles` 类，因为没有 cookie （或无效或过期）。

> [!NOTE]
> Microsoft 使用持久性角色缓存 cookie &amp; 实践组中的模式。 由于拥有角色缓存 cookie 足以证明角色成员身份，如果黑客可以通过某种方式获得对有效用户 cookie 的访问权限，则可以模拟该用户。 如果 cookie 保存在用户的浏览器上，则会出现这种情况的可能性。 有关此安全建议以及其他安全问题的详细信息，请参阅[ASP.NET 2.0 的安全问题列表](https://msdn.microsoft.com/library/ms998375.aspx)。

## <a name="step-1-defining-role-based-url-authorization-rules"></a>步骤1：定义基于角色的 URL 授权规则

如<a id="_msoanchor_6"> </a>[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程中所述，URL 授权提供一种方法，用于按用户或按角色限制对一组页面的访问。 使用带有 `<allow>` 和 `<deny>` 子元素的[`<authorization>` 元素](https://msdn.microsoft.com/library/8d82143t.aspx)`Web.config` 中的 URL 授权规则。 除了前面教程中讨论的与用户相关的授权规则之外，每个 `<allow>` 和 `<deny>` 子元素还可以包括：

- 特定角色
- 以逗号分隔的角色列表

例如，URL 授权规则将访问权限授予 "管理员" 和 "监察员" 角色中的用户，但拒绝所有其他用户的访问权限：

[!code-xml[Main](role-based-authorization-cs/samples/sample2.xml)]

上述标记中的 `<allow>` 元素指出允许使用 Administrators 和监察员角色;`<deny>` 元素指示*所有*用户被拒绝。

让我们配置应用程序，以便只有管理员角色中的用户才能访问 `ManageRoles.aspx`、`UsersAndRoles.aspx`和 `CreateUserWizardWithRoles.aspx` 页面，而 `RoleBasedAuthorization.aspx` 页面仍可供所有访问者访问。

若要实现此目的，请首先将 `Web.config` 文件添加到 `Roles` 文件夹。

[![将 Web.config 文件添加到 Roles 目录](role-based-authorization-cs/_static/image8.png)](role-based-authorization-cs/_static/image7.png)

**图 3**：向 `Roles` 目录添加 `Web.config` 文件（[单击以查看完全大小的映像](role-based-authorization-cs/_static/image9.png)）

接下来，将以下配置标记添加到 `Web.config`：

[!code-xml[Main](role-based-authorization-cs/samples/sample3.xml)]

`<system.web>` 部分中的 `<authorization>` 元素指示只有管理员角色中的用户才能访问 `Roles` 目录中的 ASP.NET 资源。 `<location>` 元素为 `RoleBasedAuthorization.aspx` 页定义一组备用 URL 授权规则，允许所有用户访问此页。

保存对 `Web.config`所做的更改后，以不在管理员角色中的用户身份登录，并尝试访问其中一个受保护的页面。 `UrlAuthorizationModule` 将检测您无权访问请求的资源;因此，`FormsAuthenticationModule` 会将您重定向到登录页。 登录页面随后会将您重定向到 `UnauthorizedAccess.aspx` 页面（请参阅图4）。 由于我们已添加到<a id="_msoanchor_7"> </a>[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程第2步中的登录页，因此最终从登录页面到 `UnauthorizedAccess.aspx` 的重定向会发生。 特别是，如果 querystring 包含 `ReturnUrl` 参数，则登录页会自动将任何经过身份验证的用户重定向到 `UnauthorizedAccess.aspx`，因为此参数指示用户在尝试查看无权查看的页后到达登录页。

[仅 ![管理员角色中的用户可以查看受保护的页面](role-based-authorization-cs/_static/image11.png)](role-based-authorization-cs/_static/image10.png)

**图 4**：只有管理员角色中的用户才能查看受保护的页面（[单击查看完全大小的图像](role-based-authorization-cs/_static/image12.png)）

注销，然后以管理员角色中的用户身份登录。 现在，你应该能够查看三个受保护的页面。

[![Tito 可以访问 UsersAndRoles 页面，因为他是 Administrators 角色](role-based-authorization-cs/_static/image14.png)](role-based-authorization-cs/_static/image13.png)

**图 5**： Tito 可以访问 `UsersAndRoles.aspx` 页面，因为他是管理员角色（[单击查看完全大小的图像](role-based-authorization-cs/_static/image15.png)）

> [!NOTE]
> 为角色或用户指定 URL 授权规则时-请务必记住，每次从上到下分析一次规则。 一旦找到匹配项，就会向用户授予或拒绝访问权限，具体取决于是否在 `<allow>` 或 `<deny>` 元素中找到了匹配项。 **如果未找到匹配项，则会向用户授予访问权限。** 因此，如果想要限制对一个或多个用户帐户的访问，则必须使用 `<deny>` 元素作为 URL 授权配置中的最后一个元素。 **如果 URL 授权规则不包括**`<deny>`**元素，则会向所有用户授予访问权限。** 若要更全面地了解如何分析 URL 授权规则，请参阅 " <a id="_msoanchor_8"> </a>[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程" 一节中的 "了解 `UrlAuthorizationModule` 如何使用授权规则来授予或拒绝访问" 一节。

## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>步骤2：基于当前已登录用户的角色限制功能

使用 URL 授权，可以轻松指定粗授权规则，这些规则规定了允许哪些标识，哪些标识被拒绝查看特定页面（或文件夹中的所有页面及其子文件夹）。 但是，在某些情况下，我们可能希望允许所有用户访问某个页面，但基于访问用户的角色限制该页面的功能。 这可能需要根据用户的角色显示或隐藏数据，或向属于特定角色的用户提供其他功能。

可以通过声明方式或编程方式（或通过这两种方式的某个组合）来实现此类精细的基于角色的授权规则。 在下一部分中，我们将了解如何通过登录视图控件实现声明性精细的授权。 接下来，我们将探讨编程技术。 但是，我们首先需要创建一个页面，使其功能依赖于用户访问它的角色，然后才能查看应用精细授权规则。

让我们创建一个页面，其中列出了 GridView 内系统中的所有用户帐户。 GridView 将包含每个用户的用户名、电子邮件地址、上次登录日期和有关用户的注释。 除了显示每个用户的信息外，GridView 还将包含编辑和删除功能。 首先，我们将创建此页面，其中包含可供所有用户使用的编辑和删除功能。 在 "使用登录视图控件" 和 "以编程方式限制功能" 部分中，我们将了解如何根据访问用户的角色启用或禁用这些功能。

> [!NOTE]
> 我们即将生成的 ASP.NET 页使用 GridView 控件来显示用户帐户。 由于本教程系列重点介绍 forms 身份验证、授权、用户帐户和角色，我不希望花太多时间讨论 GridView 控件的内部工作原理。 虽然本教程提供了有关设置此页面的具体分步说明，但它并不深入探讨某些选择的原因，或特定属性对呈现的输出的影响。 有关 GridView 控件的彻底检查，请 *[在 ASP.NET 2.0 教程系列中查看如何处理数据](../../data-access/index.md)* 。

首先打开 `Roles` 文件夹中的 "`RoleBasedAuthorization.aspx`" 页。 将 GridView 从页面拖到设计器上，并将其 `ID` 设置为 `UserGrid`。 稍后我们将编写调用 `Membership.GetAllUsers` 方法的代码，并将生成的 `MembershipUserCollection` 对象绑定到 GridView。 `MembershipUserCollection` 包含系统中每个用户帐户的 `MembershipUser` 对象;`MembershipUser` 对象具有 `UserName`、`Email`和 `LastLoginDate`等属性。

编写将用户帐户绑定到网格的代码之前，先来定义 GridView 的字段。 从 GridView 的智能标记中，单击 "编辑列" 链接以启动 "字段" 对话框（见图6）。 在此处，取消选中左下角的 "自动生成字段" 复选框。 由于我们希望此 GridView 包含编辑和删除功能，因此请添加 CommandField 并设置其 `ShowEditButton`，并 `ShowDeleteButton` 属性设置为 True。 接下来，添加四个字段，用于显示 `UserName`、`Email`、`LastLoginDate`和 `Comment` 属性。 对两个可编辑字段使用 BoundField （`UserName` 和 `LastLoginDate`）和 Templatefield （`Email` 和 `Comment`）。

使第一个 BoundField 显示 `UserName` 属性;将其 `HeaderText` 和 `DataField` 属性设置为 "UserName"。 此字段不可编辑，因此将其 `ReadOnly` 属性设置为 True。 将 `LastLoginDate` BoundField 设置为 "Last Login"，并将其 `DataField` `HeaderText` 设置为 "LastLoginDate"。 让我们将此 BoundField 的输出格式设置为仅显示日期（而不是日期和时间）。 若要实现此目的，请将此 BoundField 的 `HtmlEncode` 属性设置为 False，并将其 `DataFormatString` 属性设置为 "{0:d}"。 同时将 `ReadOnly` 属性设置为 True。

将两个 Templatefield 的 `HeaderText` 属性设置为 "Email" 和 "Comment"。

[![可以通过 "字段" 对话框配置 GridView 的字段](role-based-authorization-cs/_static/image17.png)](role-based-authorization-cs/_static/image16.png)

**图 6**：可以通过 "字段" 对话框（[单击查看完全大小的图像](role-based-authorization-cs/_static/image18.png)）来配置 GridView 的字段

现在，我们需要为 "Email" 和 "Comment" Templatefield 定义 `ItemTemplate` 和 `EditItemTemplate`。 将标签 Web 控件添加到每个 `ItemTemplate`，并将其 `Text` 属性分别绑定到 `Email` 和 `Comment` 属性。

对于 "Email" TemplateField，请将名为 `Email` 的文本框添加到 `EditItemTemplate`，并使用双向数据绑定将其 `Text` 属性绑定到 `Email` 属性。 将 RequiredFieldValidator 和 RegularExpressionValidator 添加到 `EditItemTemplate`，以确保编辑电子邮件属性的访问者已输入有效的电子邮件地址。 对于 "Comment" TemplateField，请将名为 `Comment` 的多行文本框添加到 `EditItemTemplate`中。 将文本框的 `Columns` 和 `Rows` 属性分别设置为40和4，然后使用双向数据绑定将其 `Text` 属性绑定到 `Comment` 属性。

配置这些 Templatefield 后，其声明性标记应如下所示：

[!code-aspx[Main](role-based-authorization-cs/samples/sample4.aspx)]

编辑或删除用户帐户时，我们需要知道该用户的 `UserName` 属性值。 将 GridView 的 `DataKeyNames` 属性设置为 "UserName"，以便可通过 GridView 的 `DataKeys` 集合获取此信息。

最后，将 ValidationSummary 控件添加到页面，并将其 `ShowMessageBox` 属性设置为 True，并将其 `ShowSummary` 属性设置为 False。 使用这些设置时，如果用户尝试编辑的用户帐户缺少电子邮件地址或电子邮件地址无效，ValidationSummary 将显示客户端警报。

[!code-aspx[Main](role-based-authorization-cs/samples/sample5.aspx)]

现在，我们已完成此页面的声明性标记。 接下来的任务是将用户帐户集绑定到 GridView。 向 `RoleBasedAuthorization.aspx` 页的代码隐藏类添加一个名为 `BindUserGrid` 的方法，该方法将 `Membership.GetAllUsers` 返回的 `MembershipUserCollection` 绑定到 `UserGrid` GridView。 在第一页上的 `Page_Load` 事件处理程序中调用此方法。

[!code-csharp[Main](role-based-authorization-cs/samples/sample6.cs)]

使用此代码后，请通过浏览器访问此页。 如图7所示，你应该看到一个 GridView，其中列出了系统中每个用户帐户的相关信息。

[![UserGrid GridView 列出系统中每个用户的相关信息](role-based-authorization-cs/_static/image20.png)](role-based-authorization-cs/_static/image19.png)

**图 7**： `UserGrid` GridView 列出有关系统中每个用户的信息（[单击查看完全大小的图像](role-based-authorization-cs/_static/image21.png)）

> [!NOTE]
> `UserGrid` GridView 列出了非分页界面中的所有用户。 此简单网格接口不适用于有多个用户的情况。 一种选择是将 GridView 配置为启用分页。 `Membership.GetAllUsers` 方法有两个重载：一个重载不接受输入参数并返回所有用户，另一个重载使用整数值作为页索引和页大小，并仅返回指定的用户子集。 第二个重载可用于更有效地浏览用户，因为它只返回用户帐户的精确子集，而不是*所有*用户帐户。 如果你拥有数千个用户帐户，则可能需要考虑使用基于筛选器的接口，它只显示用户名以选定字符开头的用户（例如）。 [`Membership.FindUsersByName method`](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)非常适合用于生成基于筛选器的用户界面。 在将来的教程中，我们将介绍如何构建此类接口。

当控件绑定到正确配置的数据源控件（如 SqlDataSource 或 ObjectDataSource）时，GridView 控件提供内置的编辑和删除支持。 不过，`UserGrid` GridView 以编程方式绑定数据，因此，我们必须编写代码来执行这两个任务。 具体而言，我们需要为 GridView 的 `RowEditing`、`RowCancelingEdit`、`RowUpdating`和 `RowDeleting` 事件创建事件处理程序，当访问者单击 GridView 的编辑、取消、更新或删除按钮时，将触发这些事件。

首先创建 GridView `RowEditing`、`RowCancelingEdit`和 `RowUpdating` 事件的事件处理程序，然后添加以下代码：

[!code-csharp[Main](role-based-authorization-cs/samples/sample7.cs)]

`RowEditing` 和 `RowCancelingEdit` 事件处理程序只需设置 GridView 的 `EditIndex` 属性，然后将用户帐户列表重新绑定到网格。 `RowUpdating` 事件处理程序中会出现有趣的内容。 此事件处理程序首先确保数据有效，然后从 `DataKeys` 集合获取已编辑用户帐户的 `UserName` 值。 然后以编程方式引用两个 Templatefield "`EditItemTemplate`" 中的 "`Email`" 和 "`Comment`" 文本框。 它们 `Text` 属性包含编辑过的电子邮件地址和注释。

为了通过成员身份 API 更新用户帐户，我们需要首先获取用户的信息，这是通过调用 `Membership.GetUser(userName)`来完成的。 然后，将用从编辑界面输入的两个文本框中输入的值来更新返回 `MembershipUser` 对象的 `Email` 和 `Comment` 属性。 最后，通过调用[`Membership.UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)保存这些修改。 `RowUpdating` 事件处理程序通过将 GridView 恢复为其预编辑接口完成。

接下来，创建 `RowDeleting` 事件处理程序，然后添加以下代码：

[!code-csharp[Main](role-based-authorization-cs/samples/sample8.cs)]

上述事件处理程序通过从 GridView 的 `DataKeys` 集合获取 `UserName` 值开始;然后，将此 `UserName` 值传递到成员身份类的[`DeleteUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)。 `DeleteUser` 方法将从系统中删除用户帐户，包括相关成员身份数据（如此用户所属的角色）。 删除用户之后，网格的 `EditIndex` 设置为-1 （如果用户在 "编辑" 模式下单击 "删除" 时单击了 "删除"），则调用 `BindUserGrid` 方法。

> [!NOTE]
> 删除用户帐户之前，"删除" 按钮不需要用户进行任何类型的确认。 我建议您添加某种形式的用户确认，以减少意外删除帐户的可能性。 确认操作的最简单方法之一是通过客户端确认对话框。 有关此技术的详细信息，请参阅[删除时添加客户端确认](https://asp.net/learn/data-access/tutorial-42-cs.aspx)。

验证该页是否按预期方式工作。 你应该能够编辑任何用户的电子邮件地址和评论，以及删除任何用户帐户。 由于 "`RoleBasedAuthorization.aspx`" 页可供所有用户访问，因此任何用户（甚至匿名访问者）都可以访问此页面并编辑和删除用户帐户！ 让我们更新此页，以便只有监察员和管理员角色中的用户可以编辑用户的电子邮件地址和评论，并且只有管理员才可以删除用户帐户。

"使用登录视图控件" 部分介绍了如何使用登录视图控件来显示特定于用户角色的说明。 如果管理员角色中的某个用户访问此页面，我们将显示有关如何编辑和删除用户的说明。 如果 "监察员" 角色中的用户到达此页，则将显示有关编辑用户的说明。 如果访问者是匿名的，或者不在主管或 Administrators 角色中，则将显示一条消息，说明他们无法编辑或删除用户帐户信息。 在 "以编程方式限制功能" 部分中，我们将编写代码，以编程方式基于用户的角色显示或隐藏 "编辑" 和 "删除" 按钮。

### <a name="using-the-loginview-control"></a>使用登录视图控件

正如我们在过去的教程中看到的那样，登录视图控件适用于为经过身份验证的用户和匿名用户显示不同的界面，但登录视图控件也可用于显示基于用户角色的不同标记。 让我们根据来访用户的角色使用登录视图控件来显示不同的说明。

首先，将登录视图添加到 `UserGrid` GridView 之上。 如前文所述，登录视图控件有两个内置模板： `AnonymousTemplate` 和 `LoggedInTemplate`。 在这两个模板中输入简短消息，通知用户他们无法编辑或删除任何用户信息。

[!code-aspx[Main](role-based-authorization-cs/samples/sample9.aspx)]

除了 `AnonymousTemplate` 和 `LoggedInTemplate`之外，登录视图控件还可以包括*RoleGroups*，它们是特定于角色的模板。 每个 RoleGroup 都包含一个 `Roles`，该属性指定 RoleGroup 应用于哪些角色。 `Roles` 属性可以设置为单个角色（如 "管理员"），也可以设置为以逗号分隔的角色列表（如 "Administrators，监察员"）。

若要管理 RoleGroups，请从控件的智能标记中单击 "编辑 RoleGroups" 链接，以显示 RoleGroup 集合编辑器。 添加两个新 RoleGroups。 将第一个 RoleGroup 的 `Roles` 属性设置为 "Administrators"，将第二个属性设置为 "主管"。

[![通过 RoleGroup 集合编辑器管理登录视图的特定于角色的模板](role-based-authorization-cs/_static/image23.png)](role-based-authorization-cs/_static/image22.png)

**图 8**：通过 RoleGroup 集合编辑器管理登录视图的特定于角色的模板（[单击以查看完全大小的图像](role-based-authorization-cs/_static/image24.png)）

单击 "确定" 以关闭 "RoleGroup 集合编辑器";这会更新登录视图的声明性标记，使其包含一个 `<RoleGroups>` 节，其中包含 RoleGroup 集合编辑器中定义的每个 RoleGroup 的 `<asp:RoleGroup>` 子元素。 此外，登录视图的智能标记中的 "视图" 下拉列表（最初仅列出 `AnonymousTemplate` 和 `LoggedInTemplate`）–现在还包括添加的 RoleGroups。

编辑 RoleGroups，以使 "监察员" 角色中的用户显示有关如何编辑用户帐户的说明，而 "管理员" 角色中的用户则显示有关编辑和删除的说明。 进行这些更改后，登录视图的声明性标记应如下所示。

[!code-aspx[Main](role-based-authorization-cs/samples/sample10.aspx)]

进行这些更改后，保存页面，然后通过浏览器进行访问。 首先以匿名用户身份访问该页面。 你应显示消息 "你未登录到系统。 因此，您无法编辑或删除任何用户信息。 " 然后以经过身份验证的用户身份登录，而不是在主管或 Administrators 角色中。 此时，你应该会看到消息 "你不是主管或 Administrators 角色的成员。 因此，您无法编辑或删除任何用户信息。 "

接下来，以作为监察员角色成员的用户身份登录。 此时应该会看到 "主管角色特定" 消息（请参阅图9）。 如果以管理员角色中的用户身份登录，则应该会看到管理员角色特定消息（请参阅图10）。

[![Bruce 显示特定于监察员角色的消息](role-based-authorization-cs/_static/image26.png)](role-based-authorization-cs/_static/image25.png)

**图 9**： Bruce 显示特定于主管角色的消息（[单击以查看完全大小的映像](role-based-authorization-cs/_static/image27.png)）

[![Tito 显示为管理员角色特定消息](role-based-authorization-cs/_static/image29.png)](role-based-authorization-cs/_static/image28.png)

**图 10**： Tito 显示了管理员特定于角色的消息（[单击以查看完全大小的映像](role-based-authorization-cs/_static/image30.png)）

如图9和10所示的屏幕截图，登录视图只呈现一个模板，即使应用了多个模板。 Bruce 和 Tito 都记录在用户中，但登录视图只呈现匹配的 RoleGroup，而不是 `LoggedInTemplate`。 此外，Tito 同时属于 Administrators 和监察员角色，而登录视图控件则呈现特定于管理员角色的模板而不是主管。

图11说明了登录视图控件用来确定要呈现的模板的工作流。 请注意，如果指定了多个 RoleGroup，则登录视图模板将呈现匹配的*第一个*RoleGroup。 换句话说，如果我们将监察员作为第一个 RoleGroup 和管理员 RoleGroup，则当 Tito 访问该页面时，他会看到监察员消息。

[![登录视图控件的工作流，以确定要呈现的模板](role-based-authorization-cs/_static/image32.png)](role-based-authorization-cs/_static/image31.png)

**图 11**：用于确定要呈现的模板的登录视图控件的工作流（[单击以查看完全大小的图像](role-based-authorization-cs/_static/image33.png)）

### <a name="programmatically-limiting-functionality"></a>以编程方式限制功能

尽管登录视图控件根据访问页面的用户角色显示不同的说明，但 "编辑" 和 "取消" 按钮对所有操作都保持可见。 我们需要以编程方式隐藏 "编辑" 和 "删除" 按钮，使其既不是主管也不是管理员角色的匿名访问者和用户。 对于不是管理员的用户，我们需要隐藏 "删除" 按钮。 为实现此目的，我们将编写一些代码，以编程方式引用 CommandField 的 Edit 和 Delete LinkButtons，并将其 `Visible` 属性设置为 `false`（如有必要）。

若要以编程方式引用 CommandField 中的控件，最简单的方法是先将其转换为模板。 若要实现此目的，请从 GridView 的智能标记中单击 "编辑列" 链接，从当前字段列表中选择 CommandField，然后单击 "将此字段转换为 TemplateField" 链接。 这会将 CommandField 转换为具有 `ItemTemplate` 和 `EditItemTemplate`的 TemplateField。 `ItemTemplate` 包含 "编辑" 和 "删除" LinkButtons，而 `EditItemTemplate` 则包含更新并取消 LinkButtons。

[![将 CommandField 转换为 TemplateField](role-based-authorization-cs/_static/image35.png)](role-based-authorization-cs/_static/image34.png)

**图 12**：将 CommandField 转换为 TemplateField （[单击以查看完全大小的图像](role-based-authorization-cs/_static/image36.png)）

更新 `ItemTemplate`中的编辑和删除 LinkButtons，并将其 `ID` 属性分别设置为 `EditButton` 和 `DeleteButton`的值。

[!code-aspx[Main](role-based-authorization-cs/samples/sample11.aspx)]

当数据绑定到 GridView 时，GridView 会枚举其 `DataSource` 属性中的记录并生成相应的 `GridViewRow` 对象。 创建每个 `GridViewRow` 对象时，都会激发 `RowCreated` 事件。 为了隐藏未经授权的用户的 "编辑" 和 "删除" 按钮，我们需要为此事件创建一个事件处理程序，并以编程方式引用编辑和删除 LinkButtons，并相应地设置其 `Visible` 属性。

创建 `RowCreated` 事件的事件处理程序，然后添加以下代码：

[!code-csharp[Main](role-based-authorization-cs/samples/sample12.cs)]

请记住，对于所有 GridView 行（包括标头、页脚、页导航界面等），*都*将激发 `RowCreated` 事件。 如果我们处理的数据行不处于编辑模式，我们只需要以编程方式引用编辑和删除 LinkButtons （因为编辑模式下的行具有更新和取消按钮，而不是编辑和删除）。 此检查由 `if` 语句处理。

如果我们处理的数据行不处于编辑模式，则将引用编辑和删除 LinkButtons，并根据 `User` 对象的 `IsInRole(roleName)` 方法返回的布尔值设置其 `Visible` 属性。 User 对象引用由 `RoleManagerModule`创建的主体;因此，`IsInRole(roleName)` 方法使用角色*API 来确定*当前访问者是否属于角色。

> [!NOTE]
> 我们可以直接使用 Role 类，将对 `User.IsInRole(roleName)` 的调用替换为对[`Roles.IsUserInRole(roleName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)的调用。 我决定在此示例中使用主体对象的 `IsInRole(roleName)` 方法，因为它比直接使用角色 API 更为有效。 在本教程的前面部分，我们将角色管理器配置为在 cookie 中缓存用户的角色。 只有在调用主体的 `IsInRole(roleName)` 方法时，才会使用此缓存 cookie 数据;直接调用角色 API 始终涉及到角色存储的行程。 即使角色未缓存在某个 cookie 中，调用主体对象的 `IsInRole(roleName)` 方法通常也更加有效，因为在请求过程中第一次调用该方法会缓存结果。 另一方面，角色 API 不会执行任何缓存。 由于 `RowCreated` 事件对于 GridView 中的每个行触发一次，因此使用 `User.IsInRole(roleName)` 只涉及到角色存储的一个行程，而 `Roles.IsUserInRole(roleName)` 需要*n*次行程，其中*n*是网格中显示的用户帐户数。

如果访问此页的用户是在管理员或主管角色中，"编辑" 按钮的 `Visible` 属性将设置为 `true`;否则，会将其设置为 `false`。 仅当用户为 Administrators 角色时，"删除" 按钮的 `Visible` 属性才设置为 `true`。

在浏览器中测试此页。 如果以匿名访问者或既不是管理员也不是管理员的用户身份访问该页，则 CommandField 为空;它仍存在，但作为不带 "编辑" 或 "删除" 按钮的瘦薄片。

> [!NOTE]
> 当非主管和非管理员访问页面时，可以完全隐藏 CommandField。 我将此留给读者的练习。

[对于非主管和非管理员，将隐藏 "编辑" 和 "删除" 按钮 ![](role-based-authorization-cs/_static/image38.png)](role-based-authorization-cs/_static/image37.png)

**图 13**：对非主管和非管理员隐藏 "编辑" 和 "删除" 按钮（[单击以查看完全大小的图像](role-based-authorization-cs/_static/image39.png)）

如果用户属于 "主管" 角色（而不是 "管理员" 角色）访问，他只看到 "编辑" 按钮。

[![当 "编辑" 按钮可用于主管时，"删除" 按钮将隐藏](role-based-authorization-cs/_static/image41.png)](role-based-authorization-cs/_static/image40.png)

**图 14**： "编辑" 按钮可用于主管，"删除" 按钮处于隐藏状态（[单击以查看完全大小的图像](role-based-authorization-cs/_static/image42.png)）

如果管理员进行访问，她可以访问 "编辑" 和 "删除" 按钮。

[只有管理员才能使用 "编辑" 和 "删除" 按钮 ![](role-based-authorization-cs/_static/image44.png)](role-based-authorization-cs/_static/image43.png)

**图 15**： "编辑" 和 "删除" 按钮仅适用于管理员（[单击以查看完全大小的图像](role-based-authorization-cs/_static/image45.png)）

## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>步骤3：将基于角色的授权规则应用于类和方法

在步骤2中，我们限制了对主管和管理员角色中的用户的编辑功能并仅向管理员删除功能。 为此，可以通过编程方式为未经授权的用户隐藏关联的用户界面元素。 此类度量值不保证未经授权的用户将无法执行特权操作。 可能有以后添加的用户界面元素，或者我们忘记了对未经授权用户隐藏的用户界面元素。 或者，黑客可能会发现一些其他方法来使 ASP.NET 页面执行所需的方法。

确保未经授权的用户无法访问特定功能的一种简单方法是使用[`PrincipalPermission` 特性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)来修饰该类或方法。 当 .NET 运行时使用一个类或执行它的一个方法时，它会进行检查以确保当前安全上下文具有权限。 `PrincipalPermission` 属性提供了一种机制，通过该机制可以定义这些规则。

本教程介绍了如何使用<a id="_msoanchor_9"> </a>[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程中的 `PrincipalPermission` 属性。 具体而言，我们了解了如何修饰 GridView 的 `SelectedIndexChanged` 和 `RowDeleting` 事件处理程序，以便它们只能由经过身份验证的用户和 Tito 执行。 `PrincipalPermission` 属性与角色一起使用。

接下来，我们将演示如何使用 GridView `RowUpdating` 上的 `PrincipalPermission` 属性，并 `RowDeleting` 事件处理程序禁止非授权用户执行。 我们需要做的就是在每个函数定义的顶部添加适当的属性：

[!code-csharp[Main](role-based-authorization-cs/samples/sample13.cs)]

`RowUpdating` 事件处理程序的属性规定，只有管理员或主管角色中的用户才能执行事件处理程序，因为 `RowDeleting` 事件处理程序上的属性将执行限制为 Administrators 角色中的用户。

> [!NOTE]
> `PrincipalPermission` 属性表示为 `System.Security.Permissions` 命名空间中的一个类。 请确保在代码隐藏类文件的顶部添加一个 `using System.Security.Permissions` 语句以导入此命名空间。

如果以某种方式，非管理员尝试执行 `RowDeleting` 事件处理程序，或者如果非管理员或非管理员尝试执行 `RowUpdating` 事件处理程序，.NET 运行时将引发 `SecurityException`。

[![如果安全上下文无权执行此方法，则会引发 SecurityException](role-based-authorization-cs/_static/image47.png)](role-based-authorization-cs/_static/image46.png)

**图 16**：如果安全上下文无权执行此方法，则会引发 `SecurityException` （[单击查看完全大小的映像](role-based-authorization-cs/_static/image48.png)）

除了 ASP.NET 页面以外，许多应用程序还具有一种体系结构，其中包括各种层，如业务逻辑和数据访问层。 这些层通常实现为类库，并提供用于执行业务逻辑和数据相关功能的类和方法。 `PrincipalPermission` 特性同样适用于将授权规则应用于这些层。

有关使用 `PrincipalPermission` 特性定义有关类和方法的授权规则的详细信息，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[使用 `PrincipalPermissionAttributes`将授权规则添加到业务层和数据层](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)。

## <a name="summary"></a>总结

在本教程中，我们介绍了如何根据用户的角色指定粗粒度和精细授权规则。 ASP.NET.使用 NET URL 授权功能，页面开发人员可以指定允许或拒绝哪些标识访问哪些页面。 正如我们在<a id="_msoanchor_10"> </a>[*基于用户的授权*](../membership/user-based-authorization-cs.md)教程中看到的那样，可以对每个用户应用 URL 授权规则。 它们还可以按角色按角色应用，如本教程的步骤1所示。

可以通过声明方式或编程方式应用精细授权规则。 在步骤2中，我们介绍了如何使用登录视图控件的 RoleGroups 功能基于访问用户的角色呈现不同的输出。 还介绍了如何以编程方式确定用户是否属于特定角色，以及如何相应地调整页面功能。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用 `PrincipalPermissionAttributes` 将授权规则添加到业务层和数据层](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [检查 ASP.NET 2.0 的成员资格、角色和配置文件：使用角色](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2.0 的安全问题列表](https://msdn.microsoft.com/library/ms998375.aspx)
- [`<roleManager>` 元素的技术文档](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的主管评审者包括 Suchi Banerjee 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](assigning-roles-to-users-cs.md)
> [下一页](creating-and-managing-roles-vb.md)
