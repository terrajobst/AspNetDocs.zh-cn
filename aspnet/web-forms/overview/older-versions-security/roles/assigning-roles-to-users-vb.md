---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
title: 向用户分配角色（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将构建两个 ASP.NET 页面，以帮助管理用户属于哪些角色。 第一页将包含用于查看哪些内容的工具 。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: fd208ee9-69cc-4467-9783-b4e039bdd1d3
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
msc.type: authoredcontent
ms.openlocfilehash: b53df4494eb0faef7c5e4547c2bf95e5fb071298
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74577859"
---
# <a name="assigning-roles-to-users-vb"></a>向用户分配角色 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.10.zip)或[下载 PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_vb.pdf)

> 在本教程中，我们将构建两个 ASP.NET 页面，以帮助管理用户属于哪些角色。 第一页将包含一些工具，用于查看用户属于给定角色、特定用户所属的角色，以及从特定角色分配或删除特定用户的能力。 在第二页中，将增加 CreateUserWizard 控件，使其包含指定新创建的用户所属的角色的步骤。 这在管理员能够创建新用户帐户的情况下很有用。

## <a name="introduction"></a>简介

<a id="_msoanchor_1"> </a>[上一教程](creating-and-managing-roles-vb.md)检查了角色框架和 `SqlRoleProvider`;我们已了解如何使用 `Roles` 类创建、检索和删除角色。 除了创建和删除角色外，我们还需要能够分配角色的用户或从中删除用户。 遗憾的是，ASP.NET 不附带任何 Web 控件来管理用户属于哪些角色。 相反，我们必须创建自己的 ASP.NET 页面来管理这些关联。 好消息是向角色中添加和删除用户非常简单。 `Roles` 类包含许多用于向一个或多个角色添加一个或多个用户的方法。

在本教程中，我们将构建两个 ASP.NET 页面，以帮助管理用户属于哪些角色。 第一页将包含一些工具，用于查看用户属于给定角色、特定用户所属的角色，以及从特定角色分配或删除特定用户的能力。 在第二页中，将增加 CreateUserWizard 控件，使其包含指定新创建的用户所属的角色的步骤。 这在管理员能够创建新用户帐户的情况下很有用。

让我们进入正题！

## <a name="listing-what-users-belong-to-what-roles"></a>列出哪些用户属于哪些角色

本教程中的第一个业务顺序是创建可将用户分配到角色的网页。 在我们考虑如何将用户分配到角色之前，让我们首先重点介绍如何确定哪些用户属于哪些角色。 显示此信息的方法有两种： "按角色" 或 "按用户"。 我们可以允许访问者选择角色，然后向其显示属于该角色的所有用户（"按角色" 显示），也可以提示访问者选择一个用户，然后向其显示分配给该用户的角色（"按用户" 显示）。

在访问者希望知道属于特定角色的用户组的情况下，"按角色" 视图非常有用。当访问者需要了解特定用户的角色时，"按用户" 视图是理想选择。 让我们的页面包括 "按角色" 和 "按用户" 界面。

首先，我们将创建 "按用户" 界面。 此接口包含下拉列表和复选框列表。 下拉列表将用系统中的用户集填充;这些复选框将枚举角色。 从下拉列表中选择用户将检查用户所属的角色。 然后，访问该页面的人员可以选中或取消选中相应的复选框，以便在相应的角色中添加或删除所选用户。

> [!NOTE]
> 对于可能有数百个用户帐户的网站，使用下拉列表列出用户帐户并不是理想选择。 下拉列表旨在允许用户从相对较短的选项列表中选择一个项。 随着列表项的数量的增加，这种方法很快就会变得困难。 如果要构建的网站可能有大量的用户帐户，则可能需要考虑使用其他用户界面，如可分页的 GridView 或可筛选的界面，该界面将提示访问者选择一个字母，然后仅显示用户名以选定字母开头的用户。

## <a name="step-1-building-the-by-user-user-interface"></a>步骤1：生成 "按用户" 用户界面

打开 "`UsersAndRoles.aspx`" 页。 在页面顶部，添加名为 `ActionStatus` 的标签 Web 控件并清除其 `Text` 属性。 我们将使用此标签提供有关所执行操作的反馈，并显示类似于 "用户 Tito 已添加到管理员角色的消息" 或 "用户 Jisun 已从主管角色中删除"。 为了使这些消息与众不同，请将标签的 `CssClass` 属性设置为 "重要"。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample1.aspx)]

接下来，将以下 CSS 类定义添加到 `Styles.css` 样式表中：

[!code-css[Main](assigning-roles-to-users-vb/samples/sample2.css)]

此 CSS 定义指示浏览器使用大的红色字体显示标签。 图1通过 Visual Studio 设计器显示了这一效果。

[![标签的 CssClass 属性生成较大的红色字体](assigning-roles-to-users-vb/_static/image2.png)](assigning-roles-to-users-vb/_static/image1.png)

**图 1**：标签的 `CssClass` 属性生成较大的红色字体（[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image3.png)）

接下来，将 "DropDownList" 添加到页面，将其 `ID` 属性设置为 "`UserList`"，并将其 `AutoPostBack` 属性设置为 "True"。 我们将使用此 DropDownList 来列出系统中的所有用户。 此 DropDownList 将绑定到 MembershipUser 对象的集合。 由于我们希望 DropDownList 显示 MembershipUser 对象的 UserName 属性（并将其用作列表项的值），请将 DropDownList 的 `DataTextField` 和 `DataValueField` 属性设置为 "UserName"。

在 DropDownList 下，添加一个名为 `UsersRoleList`的中继器。 此中继器会将系统中的所有角色列出为一系列的复选框。 使用以下声明性标记定义中继器 `ItemTemplate`：

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample3.aspx)]

`ItemTemplate` 标记包含名为 `RoleCheckBox`的单个复选框 Web 控件。 复选框的 `AutoPostBack` 属性设置为 True，`Text` 属性绑定到 `Container.DataItem`。 之所以只 `Container.DataItem` databinding 语法，是因为 role framework 以字符串数组的形式返回角色名称的列表，而这是我们将绑定到 Repeater 的字符串数组。 有关为何使用此语法来显示绑定到数据 Web 控件的数组内容的详细说明不在本教程的讨论范围之内。 有关此问题的详细信息，请参阅将[标量数组绑定到数据 Web 控件](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)。

此时，"用户" 接口的声明性标记应如下所示：

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample4.aspx)]

现在，我们可以编写代码将用户帐户集绑定到 DropDownList，并将角色集绑定到中继器。 在该页的代码隐藏类中，使用以下代码添加一个名为 `BindUsersToUserList` 的方法和一个名为 `BindRolesList`的方法：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample5.vb)]

`BindUsersToUserList` 方法通过[`Membership.GetAllUsers` 方法](https://msdn.microsoft.com/library/dy8swhya.aspx)检索系统中的所有用户帐户。 这会返回[`MembershipUserCollection` 对象](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)，该对象是[`MembershipUser` 实例](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)的集合。 然后将此集合绑定到 `UserList` DropDownList。 构成集合的 `MembershipUser` 实例包含各种属性，如 `UserName`、`Email`、`CreationDate`和 `IsOnline`。 为了指示 DropDownList 显示 `UserName` 属性的值，请确保已将 `UserList` DropDownList 的 `DataTextField` 和 `DataValueField` 属性设置为 "UserName"。

> [!NOTE]
> `Membership.GetAllUsers` 方法有两个重载：一个重载不接受输入参数并返回所有用户，另一个重载使用整数值作为页索引和页大小，并仅返回指定的用户子集。 当可分页用户界面元素中显示大量用户帐户时，第二个重载可用于更有效地浏览用户，因为它只返回用户帐户的精确子集，而不是所有用户帐户。

`BindRolesToList` 方法首先调用 `Roles` 类的[`GetAllRoles` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)，该方法返回包含系统中的角色的字符串数组。 然后，将此字符串数组绑定到 Repeater。

最后，在第一次加载页面时，需要调用这两种方法。 将以下代码添加到 `Page_Load` 事件处理程序中：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample6.vb)]

完成此代码后，请花点时间通过浏览器访问页面;屏幕应类似于图2。 所有用户帐户都在下拉列表中填充，并且在该下拉列表中，每个角色都显示为复选框。 由于我们将 DropDownList 和 Checkbox 的 `AutoPostBack` 属性设置为 True，因此更改所选用户或选中或取消选中角色会导致回发。 但不执行任何操作，因为我们尚未编写代码来处理这些操作。 我们将在接下来的两个部分中处理这些任务。

[![页面显示用户和角色](assigning-roles-to-users-vb/_static/image5.png)](assigning-roles-to-users-vb/_static/image4.png)

**图 2**：页面显示用户和角色（[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image6.png)）

### <a name="checking-the-roles-the-selected-user-belongs-to"></a>正在检查选定用户所属的角色

第一次加载页面时，或每当访问者从下拉列表中选择新用户时，我们需要更新 `UsersRoleList`的复选框，以便仅当所选用户属于该角色时才选中 "给定角色" 复选框。 若要完成此操作，请使用以下代码创建一个名为 `CheckRolesForSelectedUser` 的方法：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample7.vb)]

上述代码首先确定所选用户是谁。 然后，它使用 Role 类的[`GetRolesForUser(userName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)，以字符串数组的形式返回指定用户的角色集。 接下来，将枚举中继器项，并以编程方式引用每个项的 `RoleCheckBox` 复选框。 仅当该复选框对应的角色包含在 `selectedUsersRoles` 字符串数组中时，才会检查该复选框。

> [!NOTE]
> 如果使用 ASP.NET 版本2.0，则不会编译 `Linq.Enumerable.Contains(Of String)(...)` 语法。 `Contains(Of String)` 方法是[LINQ 库](http://en.wikipedia.org/wiki/Language_Integrated_Query)的一部分，这是 ASP.NET 3.5 的新手。 如果仍在使用 ASP.NET 版本2.0，请改用[`Array.IndexOf(Of String)` 方法](https://msdn.microsoft.com/library/eha9t187.aspx)。

在以下两种情况下，需要调用 `CheckRolesForSelectedUser` 方法：首次加载页面时，无论何时更改 `UserList` DropDownList 的所选索引。 因此，请从 `Page_Load` 事件处理程序调用此方法（在对 `BindUsersToUserList` 和 `BindRolesToList`调用之后）。 此外，为 DropDownList 的 `SelectedIndexChanged` 事件创建事件处理程序，并从该事件中调用此方法。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample8.vb)]

使用此代码后，可以通过浏览器对页面进行测试。 不过，由于 `UsersAndRoles.aspx` 页面目前不具备将用户分配到角色的能力，因此没有用户拥有角色。 接下来，我们将创建用于将用户分配到角色的接口，因此，你可以将此代码用于此代码，并验证它是否以后这样做，或者可以通过将记录插入到 `aspnet_UsersInRoles` 表中，手动将用户添加到角色，以便立即测试此功能。

### <a name="assigning-and-removing-users-from-roles"></a>分配和删除角色中的用户

当访问者在 `UsersRoleList` Repeater 中选中或取消选中某个复选框时，需要在相应的角色中添加或删除所选用户。 复选框的 `AutoPostBack` 属性当前设置为 True，这会导致在选择或取消选择 Repeater 中的任何一个复选框时都将导致回发。 简而言之，需要为复选框的 `CheckChanged` 事件创建事件处理程序。 由于复选框在中继器控件中，因此需要手动添加事件处理程序管道。 首先将事件处理程序作为 `Protected` 方法添加到代码隐藏类，如下所示：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample9.vb)]

稍后我们将返回为此事件处理程序编写代码。 但首先让我们完成事件处理管道。 从 Repeater 的 `ItemTemplate`中的复选框添加 `OnCheckedChanged="RoleCheckBox_CheckChanged"`。 此语法将 `RoleCheckBox_CheckChanged` 事件处理程序线路到 `RoleCheckBox`的 `CheckedChanged` 事件。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample10.aspx)]

最终任务是完成 `RoleCheckBox_CheckChanged` 事件处理程序。 我们需要通过引用引发事件的 CheckBox 控件开始，因为此复选框实例告诉我们哪些角色是通过其 `Text` 进行检查或取消选中的，并 `Checked` 属性。 将此信息与所选用户的用户名一起使用，我们通过 `Roles` 类的[`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)或[`RemoveUserFromRole` 方法](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)，在角色中添加或删除用户。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample11.vb)]

上述代码首先以编程方式引用引发事件的复选框，该复选框可通过 `sender` 输入参数获得。 如果选中该复选框，则选定的用户将添加到指定的角色中，否则将从角色中删除这些用户。 在任一情况下，"`ActionStatus`" 标签都将显示一条消息，该消息汇总刚才执行的操作。

请花点时间通过浏览器进行测试。 选择 "用户 Tito"，然后将 Tito 添加到 "管理员" 和 "监察员" 角色。

[![Tito 已添加到 "管理员" 和 "监察员" 角色](assigning-roles-to-users-vb/_static/image8.png)](assigning-roles-to-users-vb/_static/image7.png)

**图 3**： Tito 已添加到 "管理员" 和 "监察员" 角色（[单击以查看完全大小的映像](assigning-roles-to-users-vb/_static/image9.png)）

接下来，从下拉列表中选择 "用户 Bruce"。 存在回发，并通过 `CheckRolesForSelectedUser`更新中继器的复选框。 由于 Bruce 并不属于任何角色，因此将取消选中这两个复选框。 接下来，将 Bruce 添加到监察员角色。

[![Bruce 已添加到 "监察员" 角色](assigning-roles-to-users-vb/_static/image11.png)](assigning-roles-to-users-vb/_static/image10.png)

**图 4**： Bruce 已添加到 "监察员" 角色（[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image12.png)）

若要进一步验证 `CheckRolesForSelectedUser` 方法的功能，请选择 Tito 或 Bruce 以外的用户。 请注意复选框如何自动取消选中，表示它们不属于任何角色。 返回到 Tito。 应选中 "管理员" 和 "主管" 复选框。

## <a name="step-2-building-the-by-roles-user-interface"></a>步骤2：生成 "按角色" 用户界面

此时，我们已完成 "按用户" 界面，并已准备好开始处理 "按角色" 界面。 "按角色" 界面提示用户从下拉列表中选择一个角色，然后显示 GridView 中属于该角色的用户集。

向 `UsersAndRoles.aspx page`添加另一个 DropDownList 控件。 将此项放置在 Repeater 控件的下面，将其命名为 `RoleList`，并将其 `AutoPostBack` 属性设置为 True。 在该下，添加一个 GridView 并将其命名 `RolesUserList`。 此 GridView 将列出属于所选角色的用户。 将 GridView 的 `AutoGenerateColumns` 属性设置为 False，将 TemplateField 添加到网格的 `Columns` 集合，并将其 `HeaderText` 属性设置为 "Users"。 定义 TemplateField 的 `ItemTemplate`，使其在名为 `UserNameLabel`的标签的 `Text` 属性中显示数据绑定表达式的值 `Container.DataItem`。

添加并配置 GridView 后，"按角色" 接口的声明性标记应如下所示：

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample12.aspx)]

我们需要用系统中的角色集来填充 `RoleList` DropDownList。 若要实现此目的，请更新 `BindRolesToList` 方法，以便将 `Roles.GetAllRoles` 方法返回的字符串数组绑定到 `RolesList` DropDownList （以及 `UsersRoleList` 中继器）。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample13.vb)]

添加了 `BindRolesToList` 方法的最后两行，以将角色集绑定到 `RoleList` DropDownList 控件。 图5显示了通过浏览器查看时的最终结果–用系统角色填充的下拉列表。

[![角色会显示在 RoleList DropDownList 中。](assigning-roles-to-users-vb/_static/image14.png)](assigning-roles-to-users-vb/_static/image13.png)

**图 5**：角色显示在 `RoleList` DropDownList （[单击查看完全大小的图像](assigning-roles-to-users-vb/_static/image15.png)）

### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>显示属于所选角色的用户

第一次加载页面时，或从 `RoleList` DropDownList 中选择新角色时，需要显示 GridView 中属于该角色的用户的列表。 使用以下代码创建名为 `DisplayUsersBelongingToRole` 的方法：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample14.vb)]

此方法首先从 `RoleList` DropDownList 中获取所选角色。 然后，它使用[`Roles.GetUsersInRole(roleName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)检索属于该角色的用户的用户名的字符串数组。 然后，将此数组绑定到 `RolesUserList` GridView。

需要在两种情况下调用此方法：初始加载页面时，当 `RoleList` DropDownList 中所选的角色发生变化时。 因此，更新 `Page_Load` 事件处理程序，以便在调用 `CheckRolesForSelectedUser`之后调用此方法。 接下来，为 `RoleList`的 `SelectedIndexChanged` 事件创建事件处理程序，并从该事件中调用此方法。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample15.vb)]

此代码准备就绪后，`RolesUserList` GridView 应显示属于所选角色的用户。 如图6所示，监察员角色由以下两个成员组成： Bruce 和 Tito。

[![GridView 列出属于所选角色的用户](assigning-roles-to-users-vb/_static/image17.png)](assigning-roles-to-users-vb/_static/image16.png)

**图 6**： GridView 列出属于所选角色的用户（[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image18.png)）

### <a name="removing-users-from-the-selected-role"></a>正在从所选角色中删除用户

让我们增加 `RolesUserList` GridView，使其包含 "删除" 按钮的列。 单击特定用户的 "删除" 按钮会将其从该角色中删除。

首先将 "删除" 按钮字段添加到 GridView。 使此字段显示为最左侧的记录，并将其 `DeleteText` 属性从 "删除" （默认值）更改为 "删除"。

[![添加](assigning-roles-to-users-vb/_static/image20.png)](assigning-roles-to-users-vb/_static/image19.png)

**图 7**：将 "删除" 按钮添加到 GridView （[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image21.png)）

单击 "删除" 按钮时，将引发可以事件，并引发 GridView 的 `RowDeleting` 事件。 需要为此事件创建一个事件处理程序并编写从所选角色中删除该用户的代码。 创建事件处理程序，然后添加以下代码：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample16.vb)]

代码首先确定所选的角色名称。 然后，它从单击 "删除" 按钮的行以编程方式引用 `UserNameLabel` 控件，以便确定要删除的用户的用户名。 然后，通过调用 `Roles.RemoveUserFromRole` 方法从角色中删除该用户。 然后，将刷新 `RolesUserList` GridView，并通过 "`ActionStatus` 标签" 控件显示一条消息。

> [!NOTE]
> 从角色中删除用户之前，"删除" 按钮不需要用户进行任何类型的确认。 我邀请您添加某个级别的用户确认。 确认操作的最简单方法之一是通过客户端确认对话框。 有关此技术的详细信息，请参阅[删除时添加客户端确认](https://asp.net/learn/data-access/tutorial-42-vb.aspx)。

图8显示了从 "监督程序" 组中删除用户 Tito 之后的页面。

[![遗憾的是，Tito 不再是监察员](assigning-roles-to-users-vb/_static/image23.png)](assigning-roles-to-users-vb/_static/image22.png)

**图 8**：唉，Tito 不再是监察员（[单击查看完全尺寸的图像](assigning-roles-to-users-vb/_static/image24.png)）

### <a name="adding-new-users-to-the-selected-role"></a>向所选角色添加新用户

除了从所选角色中删除用户，此页的访问者还应能够将用户添加到所选角色。 将用户添加到所选角色的最佳界面取决于预期拥有的用户帐户数。 如果你的网站仅容纳几个用户帐户或更少的用户帐户，则可以在此处使用 DropDownList。 如果可能有数千个用户帐户，则需要包含一个用户界面，该用户界面允许访问者逐页浏览帐户、搜索特定帐户或以其他方式筛选用户帐户。

对于此页，我们将使用一个非常简单的接口，不管系统中的用户帐户数量如何，都可以使用该接口。 也就是说，我们将使用文本框，提示访问者键入要添加到所选角色的用户的用户名。 如果不存在具有该名称的用户，或如果用户已是角色的成员，则将在 `ActionStatus` 标签中显示一条消息。 但如果用户存在并且不是角色的成员，我们会将其添加到角色并刷新网格。

在 GridView 下面添加文本框和按钮。 将文本框的 `ID` 设置为 "`UserNameToAddToRole`，并将按钮的 `ID` 和 `Text` 属性分别设置为" `AddUserToRoleButton` "和" 将用户添加到角色 "。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample17.aspx)]

接下来，为 `AddUserToRoleButton` 创建 `Click` 事件处理程序并添加以下代码：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample18.vb)]

`Click` 事件处理程序中的大部分代码执行各种验证检查。 它可确保访问者在 "`UserNameToAddToRole`" 文本框中提供了用户名，用户存在于系统中，并且用户不属于所选角色。 如果其中任何一项检查失败，则会在 `ActionStatus` 中显示相应的消息，并退出事件处理程序。 如果所有检查都通过，则用户通过 `Roles.AddUserToRole` 方法添加到角色。 完成后，将清除该文本框的 `Text` 属性，将刷新 GridView，并且 `ActionStatus` 标签将显示一条消息，指示已将指定的用户成功添加到所选角色。

> [!NOTE]
> 为了确保指定用户不属于所选角色，我们使用[`Roles.IsUserInRole(userName, roleName)` 方法](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)，该方法返回一个布尔值，指示用户名是否为角色*名称*的*成员。* 在下一教程中， <a id="_msoanchor_2"></a>我们将在[下一教程](role-based-authorization-vb.md)中再次使用此方法。

通过浏览器访问页面，然后从 `RoleList` DropDownList 中选择 "监察员" 角色。 尝试输入无效用户名–您应该会看到一条消息，说明用户在系统中不存在。

[![不能将不存在的用户添加到角色](assigning-roles-to-users-vb/_static/image26.png)](assigning-roles-to-users-vb/_static/image25.png)

**图 9**：不能将不存在的用户添加到角色（[单击以查看完全大小的映像](assigning-roles-to-users-vb/_static/image27.png)）

现在，请尝试添加有效的用户。 继续，将 Tito 重新添加到监察员角色。

[![Tito 再次成为监督员！](assigning-roles-to-users-vb/_static/image29.png)](assigning-roles-to-users-vb/_static/image28.png)

**图 10**： Tito 再次成为监督员！  （[单击以查看完全大小的映像](assigning-roles-to-users-vb/_static/image30.png)）

## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>步骤3：交叉更新 "按用户" 和 "按角色" 接口

"`UsersAndRoles.aspx`" 页面提供了用于管理用户和角色的两个不同的接口。 目前，这两个接口彼此独立操作，因此在一个接口中进行的更改可能不会立即反映到另一个接口中。 例如，假设该页的访问者从 `RoleList` DropDownList 中选择了 "监察员" 角色，该角色将 Bruce 和 Tito 列为其成员。 接下来，访问者从 `UserList` DropDownList 中选择 "Tito"，这会检查 `UsersRoleList` Repeater 中的 "管理员" 和 "主管" 复选框。 如果访问者随后从 Repeater 中取消选中管理员角色，则会从 "监察员" 角色中删除 Tito，但此修改不会反映在 "按角色" 界面中。 GridView 仍将显示 Tito，作为 "主管" 角色的成员。

若要解决此问题，我们需要在 `UsersRoleList` Repeater 中选中或取消选中某个角色时，刷新 GridView。 同样，无论何时删除用户或将其添加到 "按角色" 界面中的角色，我们都需要刷新中继器。

"按用户" 界面中的中继器通过调用 `CheckRolesForSelectedUser` 方法进行刷新。 可以在 `RolesUserList` GridView 的 `RowDeleting` 事件处理程序中修改 "按角色" 接口，并使用 "`AddUserToRoleButton`" 按钮的 `Click` 事件处理程序。 因此，我们需要从这些方法中调用 `CheckRolesForSelectedUser` 方法。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample19.vb)]

同样，通过调用 `DisplayUsersBelongingToRole` 方法，并通过 `RoleCheckBox_CheckChanged` 事件处理程序修改 "按用户" 接口，来刷新 "按角色" 接口中的 GridView。 因此，我们需要从此事件处理程序中调用 `DisplayUsersBelongingToRole` 方法。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample20.vb)]

通过这些次要代码更改，"按用户" 和 "按角色" 接口现在会正确交叉更新。 若要对此进行验证，请访问浏览器中的页面，并分别从 `UserList` 和 `RoleList` DropDownLists 中选择 Tito 和主管。 请注意，当你在 "按用户" 界面中取消选择 Tito 的 "主管" 角色时，将自动从 "按角色" 接口中的 GridView 中删除 Tito。 通过 "按角色" 接口将 Tito 添加回监察员角色后，会自动重新检查 "按用户" 界面中的 "监察员" 复选框。

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>步骤4：自定义 CreateUserWizard 以包含 "指定角色" 步骤

<a id="_msoanchor_3"></a>在[*创建用户帐户*](../membership/creating-user-accounts-vb.md)教程中，我们了解了如何使用 CreateUserWizard Web 控件来提供用于创建新用户帐户的接口。 可以通过以下两种方式之一使用 CreateUserWizard 控件：

- 作为访问者在站点上创建自己的用户帐户的方法，并
- 作为管理员创建新帐户的方法

在第一个用例中，访问者访问网站并填写 CreateUserWizard，输入其信息以便在站点上注册。 在第二种情况下，管理员为其他人创建了一个新帐户。

当管理员为某个其他人创建帐户时，允许管理员指定新用户帐户所属的角色可能会很有帮助。 在<a id="_msoanchor_4"> </a> [*存储* *其他用户信息*](../membership/storing-additional-user-information-vb.md)教程中，我们了解了如何通过添加其他 `WizardSteps`自定义 CreateUserWizard。 让我们看看如何向 CreateUserWizard 添加其他步骤，以便指定新用户的角色。

打开 `CreateUserWizardWithRoles.aspx` 页面并添加一个名为 `RegisterUserWithRoles`的 CreateUserWizard 控件。 将控件的 `ContinueDestinationPageUrl` 属性设置为 "~/Default.aspx"。 由于这里的思路是，管理员将使用此 CreateUserWizard 控件创建新的用户帐户，并将该控件的 `LoginCreatedUser` 属性设置为 False。 此 `LoginCreatedUser` 属性指定访问者是否作为刚创建的用户自动登录，并且默认为 True。 我们将其设置为 False，因为当管理员创建新帐户时，我们希望将其作为自己的登录。

接下来，选择 "添加/删除 `WizardSteps`..."选项从 CreateUserWizard 的智能标记中添加新 `WizardStep`，并将其 `ID` 设置为 "`SpecifyRolesStep`"。 将 `SpecifyRolesStep WizardStep` 移到 "注册新帐户" 步骤之后，在 "完成" 步骤之前。 将 `WizardStep`的 `Title` 属性设置为 "指定角色"、将其 `StepType` 属性设置为 `Step`，并将其 `AllowReturn` 属性设置为 False。

[![添加](assigning-roles-to-users-vb/_static/image32.png)](assigning-roles-to-users-vb/_static/image31.png)

**图 11**：向 CreateUserWizard 添加 "指定角色" `WizardStep` （[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image33.png)）

此更改后，CreateUserWizard 的声明性标记应如下所示：

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample21.aspx)]

在 "指定角色" `WizardStep`中，添加一个名为 `RoleList.` 的 CheckBoxList，此 CheckBoxList 将列出可用的角色，使访问该页的人员可以检查新创建的用户所属的角色。

我们保留了两个编码任务：首先，必须用系统中的角色填充 `RoleList` CheckBoxList;其次，当用户从 "指定角色" 步骤移到 "完成" 步骤时，需要将创建的用户添加到选定的角色。 可以在 `Page_Load` 事件处理程序中完成第一项任务。 以下代码以编程方式引用第一次访问页面时的 `RoleList` 复选框，并将系统中的角色绑定到该页面。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample22.vb)]

上述代码应熟悉。 在<a id="_msoanchor_5"> </a> [*存储* *其他用户信息*](../membership/storing-additional-user-information-vb.md)教程中，我们使用了两个 `FindControl` 语句从自定义 `WizardStep`中引用 Web 控件。 在本教程的前面部分，将角色绑定到 CheckBoxList 的代码。

若要执行第二个编程任务，需要了解 "指定角色" 步骤的完成时间。 回忆一下，CreateUserWizard 有一个 `ActiveStepChanged` 事件，每次访问者导航到另一个步骤时都会触发此事件。 在这里，我们可以确定用户是否已达到 "完成" 步骤;如果是这样，我们需要将该用户添加到选定的角色。

为 `ActiveStepChanged` 事件创建事件处理程序并添加以下代码：

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample23.vb)]

如果用户刚到达 "已完成" 步骤，事件处理程序会枚举 `RoleList` CheckBoxList 的项目，并且刚刚创建的用户将分配到所选角色。

通过浏览器访问此页。 CreateUserWizard 中的第一步是标准 "注册新帐户" 步骤，该步骤会提示输入新用户的用户名、密码、电子邮件和其他关键信息。 输入用于创建名为 Wanda 的新用户的信息。

[![创建一个名为 Wanda 的新用户](assigning-roles-to-users-vb/_static/image35.png)](assigning-roles-to-users-vb/_static/image34.png)

**图 12**：创建名为 Wanda 的新用户（[单击以查看完全大小的图像](assigning-roles-to-users-vb/_static/image36.png)）

单击 "创建用户" 按钮。 CreateUserWizard 在内部调用 `Membership.CreateUser` 方法，创建新的用户帐户，然后执行下一步 "指定角色"。 此处列出了系统角色。 选中 "监察员" 复选框，然后单击 "下一步"。

[![使 Wanda 成为主管角色的成员](assigning-roles-to-users-vb/_static/image38.png)](assigning-roles-to-users-vb/_static/image37.png)

**图 13**：将 Wanda 设置为主管角色的成员（[单击以查看完全大小的映像](assigning-roles-to-users-vb/_static/image39.png)）

单击 "下一步" 将导致回发并将 `ActiveStep` 更新为 "完成" 步骤。 在 `ActiveStepChanged` 事件处理程序中，将最近创建的用户帐户分配给 "监察员" 角色。 若要验证这一点，请返回 `UsersAndRoles.aspx` 页面，并从 `RoleList` DropDownList 中选择 "监察员"。 如图14所示，监察员现在由三个用户组成： Bruce、Tito 和 Wanda。

[![Bruce、Tito 和 Wanda 都是所有主管](assigning-roles-to-users-vb/_static/image41.png)](assigning-roles-to-users-vb/_static/image40.png)

**图 14**： Bruce、Tito 和 Wanda 均为主管（[单击查看全尺寸图像](assigning-roles-to-users-vb/_static/image42.png)）

## <a name="summary"></a>总结

角色框架提供了一些方法，用于检索有关特定用户的角色和方法的信息，以确定哪些用户属于指定的角色。 此外，还提供了多种方法来向一个或多个角色添加和删除一个或多个用户。 在本教程中，我们只重点介绍两种方法： `AddUserToRole` 和 `RemoveUserFromRole`。 还有其他变体，旨在将多个用户添加到单个角色并向一个用户分配多个角色。

本教程还介绍了如何扩展 CreateUserWizard 控件以包含用于指定新创建的用户角色的 `WizardStep`。 此类步骤可帮助管理员简化为新用户创建用户帐户的过程。

此时，我们已了解如何创建和删除角色，以及如何在角色中添加和删除用户。 但我们尚未介绍如何应用基于角色的授权。 <a id="_msoanchor_6"></a>在[以下教程](role-based-authorization-vb.md)中，我们将查看按角色定义的 URL 授权规则，以及如何基于当前登录用户的角色限制页面级功能。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 网站管理工具概述](https://msdn.microsoft.com/library/ms228053.aspx)
- [正在检查 ASP。网络的成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-and-managing-roles-vb.md)
> [下一页](role-based-authorization-vb.md)
