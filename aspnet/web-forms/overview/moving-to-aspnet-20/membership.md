---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成员身份 |Microsoft Docs
author: microsoft
description: ASP.NET 成员资格建立在 ASP.NET 1.x 中窗体身份验证模型成功的基础之上。 ASP.NET Forms 身份验证提供了一种简便的方法来 incorp 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521702"
---
# <a name="membership"></a>成员身份

由[Microsoft](https://github.com/microsoft)

> ASP.NET 成员资格建立在 ASP.NET 1.x 中窗体身份验证模型成功的基础之上。 ASP.NET Forms 身份验证提供了一种方便的方法，可将登录窗体合并到 ASP.NET 应用程序中，并针对数据库或其他数据存储来验证用户。

ASP.NET 成员资格建立在 ASP.NET 1.x 中窗体身份验证模型成功的基础之上。 ASP.NET Forms 身份验证提供了一种方便的方法，可将登录窗体合并到 ASP.NET 应用程序中，并针对数据库或其他数据存储来验证用户。 使用 FormsAuthentication 类的成员可以处理用于身份验证的 cookie，检查有效的登录名，记录用户，等等。但是，在 ASP.NET 1.x 应用程序中实现 Forms 身份验证可能需要相当多的代码。

ASP.NET 2.0 中的成员资格是单独使用窗体身份验证的主要进步。 （与 Forms 身份验证结合使用时，成员资格最可靠，但不要求使用窗体身份验证。）如您所见，您可以使用 ASP.NET 成员身份和 ASP.NET 2.0 中的登录控件来实现功能强大的成员资格系统，而无需编写大量代码。

## <a name="implementing-membership-in-aspnet-20"></a>在 ASP.NET 2.0 中实现成员资格

成员资格通过以下四个步骤实现。 请记住，有许多子步骤以及可实现的可选配置也是如此。 这些步骤旨在说明配置成员身份的大图。

1. 创建成员资格数据库（如果 SQL Server 用作成员资格存储区。）
2. 指定应用程序配置文件中的成员资格选项。 （默认情况下启用成员身份。）
3. 确定要使用的成员资格存储区的类型。 选项包括： 

    - Microsoft SQL Server （版本7.0 或更高版本）
    - Active Directory 存储
    - 自定义成员资格提供程序
4. 为 ASP.NET Forms 身份验证配置应用程序。 同样，成员资格旨在利用 Forms 身份验证，但不要求使用窗体身份验证。
5. 定义成员身份的用户帐户，并根据需要配置角色。

## <a name="creating-the-membership-database"></a>创建成员资格数据库

如果使用 SQL Server 7.0 或更高版本作为成员资格存储区，则可以使用 aspnet\_regsql 实用工具（最轻松地从 Visual Studio .NET 2005 命令提示符获取）来配置数据库。 Aspnet\_regsql 实用工具可用作命令提示符工具或通过 GUI 向导。 向导方法是配置数据库的最简单方法。 若要访问该向导，只需运行以下命令：

`aspnet_regsql W`

运行该命令后，将显示 ASP.NET SQL Server 安装向导，如下所示。

![](membership/_static/image1.jpg)

**图1**

ASP.NET SQL Server 安装向导将在您在向导中指定的实例中创建网站。 但是，ASP.NET 将使用 machine.config 文件中的连接字符串连接到数据库。 默认情况下，此连接字符串将指向 SQL Server 2005 实例，因此，如果使用 SQL Server 2000 或 SQL Server 7.0 实例，则需要修改 machine.config 文件中的连接字符串。 可在此处找到该连接字符串：

[!code-xml[Main](membership/samples/sample1.xml)]

遗憾的是，如果不修改连接字符串，ASP.NET 将不会给您带来描述性错误。 这只是因为您并未创建数据库。 在上面的示例中，我修改了指向本地 SQL Server 2000 实例的连接字符串。

## <a name="specifying-configuration-and-adding-users-and-roles"></a>指定配置并添加用户和角色

配置成员身份的下一步是将所需的信息添加到应用程序的 web.config 文件中。 在 ASP.NET 1.x 中，修改 web.config 文件有时很难，因为使用的是 lowerCamelCase，而缺少 Intellisense。 Visual Studio .NET 2005 通过为配置文件使用 Intellisense 使任务更容易，但通过提供用于编辑配置文件的 Web 界面，ASP.NET 2.0 进一步提高了一步。

可以通过单击解决方案资源管理器工具栏上的 "ASP.NET 配置" 按钮来启动 Web 界面，如下所示。 还可以通过在插入登录控件时显示的弹出窗口启动 Web 界面。

![](membership/_static/image2.jpg)

**图2**

这将启动如下所示的 ASP.NET 网站管理工具。 ASP.NET 网站管理是一个四个选项卡界面，可让你轻松管理应用程序设置。 提供以下选项卡：

- **Home**
- **安全**配置用户、角色和访问权限。
- **应用程序**配置应用程序设置。
- **提供程序**配置和测试应用程序成员资格提供程序。

网站管理工具可让你轻松地创建新用户、创建新角色以及管理用户和角色。 此功能在 Windows 界面中不可用。 Windows 界面允许你轻松定义授权设置，以及添加、删除和管理不在网站管理工具中的提供程序和功能。

若要启动 Windows 界面，请打开 Internet Information Services 管理单元，右键单击应用程序，然后选择 "属性"。 单击 "ASP.NET" 选项卡，然后单击 "编辑配置" 按钮。 （若要启用 "编辑配置" 按钮，应用程序必须在 ASP.NET 2.0 下运行。 也可以在 ASP.NET 对话框中配置 ASP.NET 版本。）将显示 ASP.NET 配置设置对话框，如下所示。

![](membership/_static/image3.jpg)

**图3**

在 "常规" 选项卡上，将列出连接字符串和应用程序设置。 斜体中的任何设置都是在父配置文件（machine.config 或更高级别的 web.config）中定义的，而斜体的设置则来自应用程序配置文件。 如果在应用程序级别添加、删除或编辑设置，则 ASP.NET 将在应用程序级别的 web.config 中添加、删除或修改设置，而不是从继承它的配置文件中移除设置。

"身份验证" 选项卡如下所示。 这是你将在其中配置成员资格设置的位置。 可以在此处配置窗体身份验证设置、成员资格提供程序和角色提供程序。

![](membership/_static/image4.jpg)

**图4**

## <a name="implementing-membership-in-your-application"></a>在应用程序中实现成员资格

在应用程序中实现 ASP.NET 2.0 成员身份的最简单方法是使用提供的登录控件。 此方法允许实现 ASP.NET 2.0 成员资格的基本知识，无需编写任何代码。

ASP.NET 2.0 中提供以下登录控件：

## <a name="login-control"></a>登录控件

Login 控件提供一个接口，供某人登录到你的成员资格系统。 它提供 "用户名" 和 "密码" 文本框，以及一个 "登录" 按钮。 许多其他常见功能，如用于注册尚未执行此操作的人员的链接、允许用户在后续访问时自动登录的复选框、密码提示的链接等。登录控件的所有功能都可通过控件的属性进行自定义。

在 ASP.NET 1.x 中，开发人员在使用窗体身份验证时，必须编写大量代码来执行查找。 借助 ASP.NET 2.0 成员身份，无需编写任何代码即可验证用户。 ASP.NET 会自动为用户执行查找。 （如果在不使用 ASP.NET 成员身份的情况下使用登录控件，则可以使用**OnAuthenticate**方法来验证用户。）

## <a name="loginview-control"></a>LoginView 控件

登录视图控件是默认情况下提供两个模板的模板化控件。AnonymousTemplate 和 LoggedInTemplate。 显示的模板取决于用户是否登录到成员身份系统。 此控件通常用于在用户尚未登录时显示登录控件，并在用户登录时显示 LoginStatus 控件和/或其他登录控件。 如果在 ASP.NET 应用程序中使用角色管理，则登录视图控件可以基于用户角色显示特定模板。 （稍后将详细介绍 ASP.NET 角色管理。）

## <a name="passwordrecovery-control"></a>PasswordRecovery 控件

PasswordRecovery 控件允许用户使用其当前密码或重置其密码来接收电子邮件。 明文和加密密码可以恢复，并通过电子邮件发送给用户。 如果对密码进行哈希处理，则无法对其进行恢复。 用户需要执行密码重置。

## <a name="loginstatus-control"></a>LoginStatus 控件

LoginStatus 控件用于向未登录的用户以及当前登录的用户显示一条注销指示器的登录指示器。 IsAuthenticated 属性用于确定要显示的指示器。 LoginStatus 控件显示的指示器可以是文本（通过**LoginText**和**LogoutText**属性实现）或图像（通过**LoginImageUrl**和**LogoutImageUrl**属性来实现）。

当用户通过 LoginStatus 控件注销时，他（她）将重定向到**LogoutPageUrl**属性指定的 URL。 如果未设置该属性，则刷新当前页面。 由于站点可能受到 Forms 身份验证的保护，因此刷新当前页面会将用户重定向到站点的登录页。

## <a name="loginname-control"></a>LoginName 控件

LoginName 控件显示当前登录到网站的用户的用户名。

## <a name="createuserwizard-control"></a>CreateUserWizard 控件

CreateUserWizard 控件为用户提供了一种方便的方法来注册你的成员资格系统。 可以通过如下所示的接口添加步骤（作为 WizardSteps 的集合实现）。

![](membership/_static/image5.jpg)

**图5**

CreateUserWizard 是一个模板化控件，该控件派生自 Wizard 类并提供以下模板：

- **System.windows.controls.headereditemscontrol.headertemplate**此模板控制向导的标题外观。
- **SidebarTemplate**此模板控制向导边栏的外观。
- **StartNavigationTemplate**此模板控制导航在开始步骤中的外观。
- **StepNavigationTemplate**当不在开始或完成步骤中时，此模板控制导航区域的外观。
- **FinishNavigationTemplate**此模板控制在完成步骤时导航区域的外观。

此外，对于添加到向导的每个步骤，ASP.NET 将创建一个自定义模板，该模板包含该步骤的 System.windows.controls.contentcontrol.contenttemplate 和 CustomNavigationTemplate。 有关自定义 CreateUserWizard 的完整详细信息，请参阅 VS.NET 2005 文档：

## <a name="changepassword-control"></a>ChangePassword 控件

ChangePassword 控件允许用户更改其密码。 如果 DisplayUserName 属性为 true （默认值为 false），则用户可以在未登录时更改其密码。 如果用户已登录，并且 DisplayUserName 属性为 true，*则用户将*可以更改未登录的另一个用户的密码，以使用户知道该用户的用户 ID。

请记住，如果你希望用户能够在无需登录的情况下更改密码，则需要确保显示 ChangePassword 控件的页面允许匿名访问。 很明显，用户必须提供旧密码才能更改密码。

## <a name="role-management"></a>角色管理

使用角色管理，可以将用户分配到特定角色，然后根据该角色限制对特定文件或文件夹的访问。 角色管理还提供了一个 API，使你能够以编程方式确定 someones 角色或确定特定角色中的所有用户并相应地做出响应。

角色管理并不是 ASP.NET 成员身份的要求，也不要求成员身份来使用角色管理。 但是，这两个方法都非常合适，开发人员可能会将它们彼此结合使用。

若要在应用程序中启用角色管理，请在 web.config 文件中进行以下更改：

[!code-xml[Main](membership/samples/sample2.xml)]

当**cacheRolesInCookie**属性设置为 true 时，ASP.NET 会在客户端上的 cookie 中缓存用户角色成员身份。 这允许在不调用 RoleProvider 的情况下进行角色查找。 使用此属性时，鼓励开发人员确保将**cookieProtection**属性设置为 All。 （这是默认设置。）这可确保 cookie 数据已加密，并有助于确保 cookie 内容未被更改。 可以使用网站管理工具添加角色。 它允许你轻松定义角色、根据这些角色配置对站点各部分的访问权限，并将用户分配到角色。

![](membership/_static/image6.jpg)

**图6**

如上所示，只需输入角色的名称，然后单击 "添加角色" 即可添加新角色。 可以通过在现有角色列表中单击相应的链接来管理或删除现有角色。

管理角色时，可以添加或删除用户，如下所示。

![](membership/_static/image7.jpg)

**图7**

通过选中 "用户处于角色中" 复选框，你可以轻松地将用户添加到特定角色。 ASP.NET 将自动用适当的条目更新你的成员资格数据库。 你还需要为应用程序配置访问规则。 ASP.NET 1.x 开发人员熟悉了如何通过 web.config 文件中的 &lt;authorization&gt; 元素来执行此操作，并且 ASP.NET 2.0 中仍提供该选项。 但是，使用网站管理工具管理访问规则更为容易，如下所示。

![](membership/_static/image8.jpg)

**图8**

在这种情况下，将突出显示 "管理" 文件夹（由于该工具以浅灰色突出显示它很难查看），并且已授予管理员角色访问权限。 拒绝所有其他用户。 你可以单击 head 图标以选择一个规则，然后使用 "上移" 和 "下移" 按钮来排列规则。 与 ASP.NET &lt;授权&gt; 元素一样，规则按它们出现的顺序进行处理。 换句话说，如果上面的快照中的规则顺序已撤消，则任何人都无法访问管理文件夹，因为 ASP.NET 将遇到的第一个规则是 "拒绝每个人" 文件夹的规则。

ASP.NET 2.0 将 web.config 文件添加到要为其指定访问规则的文件夹。 可以通过配置文件或网站管理工具编辑访问规则。 换句话说，网站管理工具只是一个接口，通过它可以在用户友好的环境中编辑配置文件。

## <a name="using-roles-in-code"></a>在代码中使用角色

从版本1.x 开始，角色管理的 API 尚未更改。 **IsInRole**方法用于确定用户是否属于特定角色。

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET 还会将 RolePrincipal 实例创建为当前上下文的成员。 RolePrincipal 对象可用于获取用户所属的所有角色，如下所示：

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>将 RoleGroups 与登录视图控件一起使用

现在，你已了解角色管理和成员身份，接下来我们将简要介绍登录视图控件如何利用 ASP.NET 2.0 中的此功能。 如前所述，登录视图控件是模板化控件，默认情况下包含两个模板;AnonymousTemplate 和 LoggedInTemplate。 在 "登录视图任务" 对话框中，可以使用以下链接（如下所示）编辑 RoleGroups。

![](membership/_static/image9.jpg)

**图9**

每个 RoleGroup 对象都包含一个字符串数组，用于定义 RoleGroup 应用于哪些角色。 若要将新的 RoleGroup 添加到登录视图控件，请单击 "编辑 RoleGroups" 链接。 在上面的图像中，可以看到我为管理员添加了新的 RoleGroup。 通过从 "视图" 下拉列表中选择 "RoleGroup （RoleGroup [0]"），我可以配置只向管理员角色的成员显示的模板。 在下图中，我添加了一个新的 RoleGroup，适用于 "销售" 角色和 "分发" 角色的成员。 这会将第二个 RoleGroup 添加到 "登录视图任务" 对话框中的 "视图" 下拉列表中，任何添加到该模板的内容都将由 "销售" 或 "分发" 角色中的任何用户看到

![](membership/_static/image10.jpg)

**图10**

## <a name="overriding-the-existing-membership-provider"></a>重写现有成员资格提供程序

可以通过几种方式来扩展 ASP.NET 成员身份的功能。 首先，可以通过从 SqlMembershipProvider 类继承并重写其方法来更改现有功能。 例如，如果你想要在创建用户时实现自己的功能，则可以创建你自己的从 SqlMembershipProvider 继承的类，如下所示：

[!code-csharp[Main](membership/samples/sample5.cs)]

另一方面，如果要创建自己的提供程序（例如，将成员身份信息存储在 Access 数据库中），则可以创建自己的提供程序。

## <a name="creating-your-own-membership-provider"></a>创建自己的成员资格提供程序

若要创建自己的成员资格提供程序，首先需要创建一个从 MembershipProvider 类继承的类。 如果使用的是 VB.NET，Visual Studio 2005 将为需要重写的所有方法添加存根。 如果你使用C#的是，则它将添加存根。

需要重写以下项：

- ApplicationName 属性
- ChangePassword 函数
- ChangePasswordQuestionAndAnswer 函数
- CreateUser 函数
- DeleteUser 函数
- EnablePasswordReset 属性
- EnablePasswordRetrieval 属性
- FindUsersByEmail 函数
- FindUsersByName 函数
- GetAllUsers 函数
- GetNumberOfUsersOnline 函数
- GetPassword 函数
- GetUser 函数
- GetUserNameByEmail 函数
- MaxInvalidPasswordAttempts 属性
- MinRequiredNonAlphanumericCharacters 属性
- MinRequiredPasswordLength 属性
- PasswordAttemptWindow 属性
- PasswordFormat 属性
- PasswordStrengthRegularExpression 属性
- RequiresQuestionAndAnswer 属性
- RequiresUniqueEmail 属性
- ResetPassword 函数
- 解锁用户函数
- UpdateUser 函数
- System.web.security.membership.validateuser 函数

这相当于作为C#开发人员实现的列表。 你可能会发现，无需任何实现即可在 VB.NET 中创建类，然后使用 .NET 反射器或类似的工具将代码转换C#为。

应将连接字符串和其他属性设置为 Initialize 方法中的默认值。 （当在运行时加载提供程序时，将触发 Initialize 方法。）Initialize 方法的第二个参数的类型为 NameValueCollection，是对 &lt;添加与 web.config 文件中的自定义提供程序相关联&gt; 元素的引用。 该条目如下所示：

[!code-xml[Main](membership/samples/sample6.xml)]

下面是 Initialize 方法的示例。

[!code-csharp[Main](membership/samples/sample7.cs)]

若要在用户提交登录窗体时验证用户，你需要使用 System.web.security.membership.validateuser 方法。 当用户在登录控件中单击 "登录" 按钮时，将激发此方法。 您将在此方法中放置执行用户查找的代码。

正如您所看到的，编写自己的成员资格提供程序并不困难，并允许您扩展 ASP.NET 2.0 的这一功能强大的功能。
