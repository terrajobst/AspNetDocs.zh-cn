---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
title: 解锁和审批用户帐户（C#） |Microsoft Docs
author: rick-anderson
description: 本教程介绍如何生成一个网页，以便管理员管理用户的锁定状态和批准状态。 我们还将了解如何批准新用户 o 。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 5346aab1-9974-489f-a065-ae3883b8a350
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: c19f7dfac0ddd12c2b4f3388a71a8ca0f71cbb18
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74580175"
---
# <a name="unlocking-and-approving-user-accounts-c"></a>解锁和审批用户帐户 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.14.zip)或[下载 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_cs.pdf)

> 本教程介绍如何生成一个网页，以便管理员管理用户的锁定状态和批准状态。 我们还将了解如何仅在验证新用户的电子邮件地址后批准它们。

## <a name="introduction"></a>简介

除了用户名、密码和电子邮件，每个用户帐户都有两个状态字段，这些字段规定用户是否可以登录到站点：已锁定并已批准。 如果用户在指定的分钟数内提供的凭据无效，则该用户会被自动锁定（默认设置会在10分钟内的5次无效登录尝试后锁定用户）。 已批准状态在某些情况下非常有用，在这种情况下，在新用户能够登录到站点之前必须执行一些操作。 例如，用户可能需要先验证其电子邮件地址，或在管理员批准后才可以登录。

由于锁定或未批准的用户无法登录，因此只需要知道如何重置这些状态。 ASP.NET 不包括任何内置功能或用于管理用户的已锁定状态的 Web 控件，部分原因是需要在每个站点上逐个处理这些决策。 某些站点可能会自动批准所有新用户帐户（默认行为）。 其他人拥有管理员批准新帐户或不批准用户，直到他们访问发送到注册时提供的电子邮件地址的链接。 同样，在管理员重置其状态之前，某些站点可能会锁定用户，而其他站点则会向锁定用户发送一封电子邮件，其中包含他们可以访问的 URL 来解锁其帐户。

本教程介绍如何生成一个网页，以便管理员管理用户的锁定状态和批准状态。 我们还将了解如何仅在验证新用户的电子邮件地址后批准它们。

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>步骤1：管理用户的锁定状态和批准状态

<a id="Tutorial12"></a>在[*生成接口以从多个教程中选择一个用户帐户*](building-an-interface-to-select-one-user-account-from-many-cs.md)时，我们构建了一个页面，其中列出了分页、筛选的 GridView 中的每个用户帐户。 该网格列出每个用户的姓名和电子邮件、其批准和锁定状态、当前是否联机以及有关用户的任何注释。 为了管理用户的批准和锁定状态，我们可以使此网格可编辑。 若要更改用户的已批准状态，管理员首先查找用户帐户，然后编辑相应的 GridView 行，选中或取消选中 "已批准" 复选框。 此外，我们还可以通过单独的 ASP.NET 页面来管理批准和锁定状态。

在本教程中，我们将使用两个 ASP.NET 页面： `ManageUsers.aspx` 和 `UserInformation.aspx`。 这里的思路是 `ManageUsers.aspx` 列出系统中的用户帐户，而 `UserInformation.aspx` 使管理员可以管理特定用户的已批准和锁定状态。 我们的第一个业务顺序是在 `ManageUsers.aspx` 中增加 GridView，使其包含一个呈现为一列链接的 HyperLinkField。 我们希望每个链接都指向 `UserInformation.aspx?user=UserName`，其中*UserName*是要编辑的用户的名称。

> [!NOTE]
> 如果下载了用于<a id="Tutorial13"> </a>[*恢复和更改密码*](recovering-and-changing-passwords-cs.md)的代码教程，你可能已注意到 `ManageUsers.aspx` 页面已经包含一组 "管理" 链接，并且 `UserInformation.aspx` 页面提供了用于更改所选用户的密码的接口。 我决定不复制与本教程关联的代码中的功能，因为它的工作原理是规避成员身份 API 并直接使用 SQL Server 数据库来更改用户的密码。 本教程与 `UserInformation.aspx` 页面从头开始。

### <a name="adding-manage-links-to-theuseraccountsgridview"></a>将 "管理" 链接添加到`UserAccounts`GridView

打开 "`ManageUsers.aspx`" 页并向 `UserAccounts` GridView 添加 HyperLinkField。 将 HyperLinkField 的 `Text` 属性设置为 "管理"，并将其 `DataNavigateUrlFields` 和 `DataNavigateUrlFormatString` 属性分别设置为 `UserName` 和 "UserInformation？ user ={0}"。 这些设置将配置 HyperLinkField，以便所有超链接都显示文本 "Manage"，但每个链接都将在相应的*用户名*值中传递到 querystring。

将 HyperLinkField 添加到 GridView 后，请花一点时间通过浏览器查看 `ManageUsers.aspx` 页面。 如图1所示，每个 GridView 行现在都包含一个 "管理" 链接。 Bruce 指向 `UserInformation.aspx?user=Bruce`的 "管理" 链接，而 Dave 的 "管理" 链接指向 `UserInformation.aspx?user=Dave`。

[![HyperLinkField 添加](unlocking-and-approving-user-accounts-cs/_static/image2.png)](unlocking-and-approving-user-accounts-cs/_static/image1.png)

**图 1**： HyperLinkField 为每个用户帐户添加 "管理" 链接（[单击以查看完全大小的映像](unlocking-and-approving-user-accounts-cs/_static/image3.png)）

稍后我们将为 `UserInformation.aspx` 页创建用户界面和代码，但首先我们来讨论如何以编程方式更改用户的已锁定和批准状态。 [`MembershipUser` 类](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)具有[`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)和[`IsApproved` 属性](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)。 该 `IsLockedOut` 属性为只读。 没有以编程方式锁定用户的机制;若要解锁用户，请使用 `MembershipUser` 类的[`UnlockUser` 方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)。 `IsApproved` 属性是可读和可写的。 若要保存对此属性所做的任何更改，我们需要调用 `Membership` 类的[`UpdateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)，并传入经过修改的 `MembershipUser` 对象。

由于 `IsApproved` 属性是可读和可写的，因此 CheckBox 控件可能是用于配置此属性的最佳用户界面元素。 但是，对于 `IsLockedOut` 属性，复选框将不起作用，因为管理员无法锁定用户，因此她只能解锁用户。 适用于 `IsLockedOut` 属性的用户界面是一个按钮，单击该按钮将解除锁定用户帐户。 仅当用户已锁定时，此按钮才会启用。

### <a name="creating-theuserinformationaspxpage"></a>创建`UserInformation.aspx`页

现在，我们已准备好在 `UserInformation.aspx`中实现用户界面。 打开此页并添加以下 Web 控件：

- 一个超链接控件，单击它时，会将管理员返回到 `ManageUsers.aspx` 页。
- 用于显示选定用户的名称的标签 Web 控件。 将此标签的 `ID` 设置为 `UserNameLabel` 并清除其 `Text` 属性。
- 名为 `IsApproved`的 CheckBox 控件。 将其 `AutoPostBack` 属性设置为 `true`。
- 用于显示用户上次锁定日期的标签控件。 `LastLockedOutDateLabel` 命名此标签，并清除其 `Text` 属性。
- 用于解锁用户的按钮。 将此按钮命名 `UnlockUserButton`，并将其 `Text` 属性设置为 "解锁用户"。
- 用于显示状态消息的标签控件，如 "用户的已批准状态已更新"。 将此控件命名为 `StatusMessage`，清除其 `Text` 属性，并将其 `CssClass` 属性设置为 "`Important`"。 （`Styles.css` 样式表文件中定义了 `Important` CSS 类; 它以一种较大的红色字体显示相应文本。）

添加这些控件后，Visual Studio 中的设计视图应类似于图2中的屏幕截图。

[![创建 UserInformation 的用户界面](unlocking-and-approving-user-accounts-cs/_static/image5.png)](unlocking-and-approving-user-accounts-cs/_static/image4.png)

**图 2**：为 `UserInformation.aspx` 创建用户界面（[单击查看完全大小的图像](unlocking-and-approving-user-accounts-cs/_static/image6.png)）

完成用户界面后，接下来的任务是根据所选用户的信息设置 `IsApproved` 复选框和其他控件。 为该页的 `Load` 事件创建事件处理程序并添加以下代码：

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample1.cs)]

上述代码首先确保这是第一次访问页面而不是后续回发。 然后，它读取通过 `user` querystring 字段传递的用户名，并通过 `Membership.GetUser(username)` 方法检索有关该用户帐户的信息。 如果未通过 querystring 提供用户名，或者找不到指定的用户，则会将管理员发送回 `ManageUsers.aspx` 页面。

然后，将在 `UserNameLabel` 中显示 `MembershipUser` 对象的 `UserName` 值，并根据 `IsApproved` 属性值检查 `IsApproved` 复选框。

`MembershipUser` 对象的[`LastLockoutDate` 属性](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx)返回一个 `DateTime` 值，该值指示上次锁定用户的时间。如果用户从未被锁定，则返回的值取决于成员资格提供程序。 创建新帐户时，`SqlMembershipProvider` 会将 `aspnet_Membership` 表的 `LastLockoutDate` 字段设置为 "`1754-01-01 12:00:00 AM`"。 如果 `LastLockoutDate` 属性在2000年之前发生，则上述代码将在 `LastLockoutDateLabel` 中显示空字符串;否则，`LastLockoutDate` 属性的日期部分将显示在标签中。 `UnlockUserButton'` s `Enabled` 属性设置为用户的锁定状态，这意味着只有在用户被锁定时才会启用此按钮。

花点时间通过浏览器测试 `UserInformation.aspx` 页面。 当然，您需要从 `ManageUsers.aspx` 开始，然后选择要管理的用户帐户。 收到 `UserInformation.aspx`时，请注意，只有在用户获得批准后，才会检查 `IsApproved` 复选框。 如果用户曾经被锁定，则会显示其上次锁定日期。 只有用户当前被锁定时，"解锁用户" 按钮才会启用。选中或取消选中 `IsApproved` 复选框或单击 "解锁用户" 按钮会导致回发，但不会对用户帐户进行任何修改，因为我们尚未为这些事件创建事件处理程序。

返回到 Visual Studio 并为 `IsApproved` CheckBox 的 `CheckedChanged` 事件创建事件处理程序，并为 `UnlockUser` 按钮的 `Click` 事件创建事件处理程序。 在 `CheckedChanged` 事件处理程序中，将用户的 `IsApproved` 属性设置为复选框的 `Checked` 属性，然后通过调用 `Membership.UpdateUser`保存更改。 在 `Click` 事件处理程序中，只需调用 `MembershipUser` 对象的 `UnlockUser` 方法。 在这两个事件处理程序中，在 `StatusMessage` 标签中显示适当的消息。

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample2.cs)]

### <a name="testing-theuserinformationaspxpage"></a>测试`UserInformation.aspx`页

准备好这些事件处理程序后，请重新访问页面并撤销用户的批准。 如图3所示，你应该在页面上看到一条简短消息，指示已成功修改用户的 `IsApproved` 属性。

[![丽丽已获批准](unlocking-and-approving-user-accounts-cs/_static/image8.png)](unlocking-and-approving-user-accounts-cs/_static/image7.png)

**图 3**： Chris 未批准（[单击以查看完全大小的图像](unlocking-and-approving-user-accounts-cs/_static/image9.png)）

接下来，注销并尝试以用户身份未审批的用户身份登录。 由于用户未获批准，因此无法登录。 默认情况下，如果用户无法登录，无论原因是什么，登录控件都将显示相同的消息。 但在使用<a id="Tutorial6"> </a>[*成员资格用户存储验证用户凭据*](../membership/validating-user-credentials-against-the-membership-user-store-cs.md)教程中，我们将了解如何增强登录控件以显示更合适的消息。 如图4所示，Chris 显示了一条消息，说明他无法登录，因为他的帐户尚未获得批准。

[![Chris 无法登录，因为他的帐户未经批准](unlocking-and-approving-user-accounts-cs/_static/image11.png)](unlocking-and-approving-user-accounts-cs/_static/image10.png)

**图 4**： Chris 不能登录，因为他的帐户未经批准（[单击查看完全大小的图像](unlocking-and-approving-user-accounts-cs/_static/image12.png)）

若要测试锁定功能，请尝试以已批准的用户身份登录，但使用的密码不正确。 重复此过程所需的次数，直到用户的帐户被锁定。如果尝试从锁定的帐户登录，则还会更新登录控件以显示自定义消息。 当你在登录页上看到以下消息时，知道帐户已被锁定： "你的帐户已被锁定，因为无效的登录尝试次数过多。 请与管理员联系以解锁你的帐户。 "

返回到 "`ManageUsers.aspx`" 页，然后单击已锁定用户的 "管理" 链接。 如图5所示，应在 "解锁用户" 按钮处于启用状态 `LastLockedOutDateLabel`。 单击 "解锁用户" 按钮以解锁用户帐户。 解锁用户后，他们将能够再次登录。

[![Dave 已被锁定在系统之外](unlocking-and-approving-user-accounts-cs/_static/image14.png)](unlocking-and-approving-user-accounts-cs/_static/image13.png)

**图 5**： Dave 已在系统中被锁定（[单击以查看完全大小的映像](unlocking-and-approving-user-accounts-cs/_static/image15.png)）

## <a name="step-2-specifying-new-users-approved-status"></a>步骤2：指定新用户的 "批准" 状态

如果希望在新用户能够登录和访问站点的用户特定功能之前执行某些操作，则 "已批准" 状态非常有用。 例如，你可能正在运行一个专用网站，在该网站中，除登录名和注册页之外的所有页只能由经过身份验证的用户访问。 但是，如果 stranger 到达网站，找到注册页并创建帐户会怎样呢？ 若要防止这种情况发生，可以将注册页移动到 `Administration` 文件夹，并要求管理员手动创建每个帐户。 或者，你可以允许任何人注册，但在管理员批准用户帐户之前禁止网站访问。

默认情况下，CreateUserWizard 控件会批准新帐户。 您可以使用控件的[`DisableCreatedUser` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)来配置此行为。 将此属性设置为 "`true`"，以不批准新用户帐户。

> [!NOTE]
> 默认情况下，CreateUserWizard 控件会自动记录新用户帐户。 此行为是由控件的[`LoginCreatedUser` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)决定的。 由于未批准的用户无法登录到站点，因此当 `DisableCreatedUser` 时 `true` 新用户帐户不会登录到站点，无论 `LoginCreatedUser` 属性的值如何。

如果通过 `Membership.CreateUser` 方法以编程方式创建新的用户帐户，若要创建未经批准的用户帐户，请使用接受新用户的 `IsApproved` 属性值作为输入参数的重载之一。

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>步骤3：通过验证用户的电子邮件地址来批准用户

许多支持用户帐户的网站在验证注册时所提供的电子邮件地址之前，不会批准新用户。 此验证过程通常用于阻止 bot、垃圾邮件制造者和其他 ne'er-井，因为它需要唯一的经过验证的电子邮件地址，并在注册过程中添加额外的步骤。 使用此模型时，当新用户注册时，将发送一封电子邮件，其中包含指向验证页面的链接。 访问该链接时，用户已证实收到电子邮件，因此提供的电子邮件地址有效。 验证页面负责批准用户。 这种情况可能会自动发生，从而批准到达此页的任何用户，或仅在用户提供一些其他信息（如[CAPTCHA](http://en.wikipedia.org/wiki/Captcha)）后。

为了适应此工作流，我们需要首先更新 "帐户创建" 页，以便新用户未经批准。 打开 `Membership` 文件夹中的 "`EnhancedCreateUserWizard.aspx`" 页，并将 CreateUserWizard 控件的 `DisableCreatedUser` 属性设置为 "`true`"。

接下来，我们需要将 CreateUserWizard 控件配置为向新用户发送一封电子邮件，其中包含有关如何验证其帐户的说明。 具体而言，我们将在电子邮件中包含一个指向 `Verification.aspx` 页面（我们尚未创建）的链接，通过查询字符串传递新用户的 `UserId`。 `Verification.aspx` 页面将查找指定的用户并将其标记为 "已批准"。

### <a name="sending-a-verification-email-to-new-users"></a>向新用户发送验证电子邮件

若要从 CreateUserWizard 控件发送电子邮件，请相应地配置其 `MailDefinition` 属性。 如<a id="Tutorial13"> </a>[前面的教程](recovering-and-changing-passwords-cs.md)中所述，ChangePassword 和 PasswordRecovery 控件包括一个[`MailDefinition` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)，该属性的工作方式与 CreateUserWizard 控件的相同。

> [!NOTE]
> 若要使用 `MailDefinition` 属性，需要在 `Web.config`中指定邮件传递选项。 有关详细信息，请参阅[在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)。

首先在 `EmailTemplates` 文件夹中创建一个名为 `CreateUserWizard.txt` 的新电子邮件模板。 对于模板，请使用以下文本：

[!code-aspx[Main](unlocking-and-approving-user-accounts-cs/samples/sample3.aspx)]

将 `MailDefinition'` s `BodyFileName` 属性设置为 "~/EmailTemplates/CreateUserWizard.txt"，并将其 `Subject` 属性设置为 "欢迎使用我的网站！ 请激活你的帐户。 "

请注意，`CreateUserWizard.txt` 电子邮件模板包含 `<%VerificationUrl%>` 占位符。 这是将在其中放置 `Verification.aspx` 页面的 URL 的位置。 CreateUserWizard 会自动将 `<%UserName%>` 和 `<%Password%>` 占位符替换为新帐户的用户名和密码，但不存在内置 `<%VerificationUrl%>` 占位符。 我们需要手动将其替换为合适的验证 URL。

若要完成此操作，请为 CreateUserWizard 的[`SendingMail` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx)创建事件处理程序并添加以下代码：

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample4.cs)]

`SendingMail` 事件在 `CreatedUser` 事件之后激发，这意味着，上一事件处理程序执行新用户帐户的时间已创建。 可以通过调用 `Membership.GetUser` 方法来访问新用户的 `UserId` 值，并传入 CreateUserWizard 控件中输入的 `UserName`。 接下来，验证 URL 的格式。 语句 `Request.Url.GetLeftPart(UriPartial.Authority)` 返回 URL 的 `http://yourserver.com` 部分;`Request.ApplicationPath` 返回应用程序的根路径。 然后将验证 URL 定义为 `Verification.aspx?ID=userId`。 然后将这两个字符串连接起来以形成完整的 URL。 最后，电子邮件正文（`e.Message.Body`） `<%VerificationUrl%>` 替换为完整的 URL。

最终效果是新用户未经批准，这意味着他们不能登录到网站。 而且，它们会自动发送一封电子邮件，其中包含指向验证 URL 的链接（参见图6）。

[![新用户将收到一封电子邮件，其中包含指向验证 URL 的链接](unlocking-and-approving-user-accounts-cs/_static/image17.png)](unlocking-and-approving-user-accounts-cs/_static/image16.png)

**图 6**：新用户接收到一封电子邮件，其中包含指向验证 URL 的链接（[单击以查看完全大小的图像](unlocking-and-approving-user-accounts-cs/_static/image18.png)）

> [!NOTE]
> CreateUserWizard 控件的默认 CreateUserWizard 步骤显示一条消息，告知用户已创建其帐户并显示 "继续" 按钮。 单击此操作会将用户转到控件的 `ContinueDestinationPageUrl` 属性指定的 URL。 `EnhancedCreateUserWizard.aspx` 中的 CreateUserWizard 配置为将新用户发送到 `~/Membership/AdditionalUserInfo.aspx`，这会提示用户提供其家乡、主页 URL 和签名。 因为此信息只能通过登录的用户添加，所以更新此属性以便将用户发送回站点的主页（`~/Default.aspx`）是有意义的。 此外，还应增加 `EnhancedCreateUserWizard.aspx` 页面或 CreateUserWizard 步骤，通知用户他们已发送验证电子邮件，除非按照此电子邮件中的说明进行操作，否则不会激活其帐户。 我将这些修改留给读者进行。

### <a name="creating-the-verification-page"></a>创建验证页

最后一个任务是创建 `Verification.aspx` 页。 将此页添加到根文件夹，并将其与 `Site.master` 母版页关联。 正如我们已在网站中添加的大多数内容页中所做的那样，删除引用 `LoginContent` ContentPlaceHolder 的内容控件，使内容页使用母版页的默认内容。

将 "标签" Web 控件添加到 "`Verification.aspx`" 页，将其 `ID` 设置为 "`StatusMessage`" 并清除其 "文本" 属性。 接下来，创建 `Page_Load` 事件处理程序并添加以下代码：

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample5.cs)]

以上代码的大部分代码验证是否存在通过 querystring 提供的 `UserId`，它是有效的 `Guid` 值，并且它引用现有的用户帐户。 如果所有这些检查都通过，则批准用户帐户;否则，将显示适当的状态消息。

图7显示了通过浏览器访问时的 `Verification.aspx` 页面。

[![新用户的帐户现已获得批准](unlocking-and-approving-user-accounts-cs/_static/image20.png)](unlocking-and-approving-user-accounts-cs/_static/image19.png)

**图 7**：新用户的帐户现已获得批准（[单击查看完全大小的映像](unlocking-and-approving-user-accounts-cs/_static/image21.png)）

## <a name="summary"></a>总结

所有成员身份用户帐户都有两个状态来确定用户是否可以登录到站点： `IsLockedOut` 和 `IsApproved`。 若要登录，用户必须 `true` 这两个属性。

用户的锁定状态用作一种安全措施，以降低黑客通过暴力破解方法进入站点的可能性。 具体而言，如果在某个时间段内有一定数量的无效登录尝试，用户将被锁定。 这些界限可通过 `Web.config`中的成员资格提供程序设置进行配置。

已批准状态通常用作禁止新用户登录，直到某些操作早于当前的方法。 站点可能需要管理员首先批准新帐户，或者通过验证其电子邮件地址（如步骤3中所述）。

很高兴编程！

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](recovering-and-changing-passwords-cs.md)
> [下一页](building-an-interface-to-select-one-user-account-from-many-vb.md)
