---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
title: 恢复和更改密码（VB） |Microsoft Docs
author: rick-anderson
description: ASP.NET 包含两个用于帮助恢复和更改密码的 Web 控件。 PasswordRecovery 控件使访问者能够恢复其丢失的 pa 。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: f9adcb5d-6d70-4885-a3bf-ed95efb4da1a
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ed1df9455af94a86ce59ecc06c55846a4880596
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618859"
---
# <a name="recovering-and-changing-passwords-vb"></a>恢复和更改密码 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.13.zip)或[下载 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_vb.pdf)

> ASP.NET 包含两个用于帮助恢复和更改密码的 Web 控件。 PasswordRecovery 控件使访问者能够恢复其丢失的密码。 ChangePassword 控件允许用户更新其密码。 与我们在本系列教程中看到的其他与登录相关的 Web 控件一样，PasswordRecovery 和 ChangePassword 控件适用于后台的成员身份框架，用于重置或修改用户的密码。

## <a name="introduction"></a>简介

在我的银行、公用事业公司、手机公司、电子邮件帐户和个性化 web 门户的网站之间，我像大多数人一样，我要记住许多不同的密码。 由于有这么多的凭据需要记住，这种情况并不太常见，人们忘记了自己的密码。 为此，提供用户帐户的网站需要为用户提供一种恢复其密码的方法。 此过程通常涉及生成新的随机密码，并通过电子邮件将其发送给用户在文件上的电子邮件地址。 收到新密码后，大多数用户都返回到该站点，并将其密码从随机生成的密码更改为更容易记住的密码。

ASP.NET 包含两个用于帮助恢复和更改密码的 Web 控件。 PasswordRecovery 控件使访问者能够恢复其丢失的密码。 ChangePassword 控件允许用户更新其密码。 与我们在本系列教程中看到的其他与登录相关的 Web 控件一样，PasswordRecovery 和 ChangePassword 控件适用于后台的成员身份框架，用于重置或修改用户的密码。

在本教程中，我们将使用这两个控件进行检查。 我们还将了解如何通过 `MembershipUser` 类的 `ChangePassword` 和 `ResetPassword` 方法以编程方式更改和重置用户的密码。

## <a name="step-1-helping-users-recover-lost-passwords"></a>步骤1：帮助用户恢复丢失的密码

支持用户帐户的所有网站都需要为用户提供一些用于恢复其忘记的密码的机制。 好消息是，通过 PasswordRecovery Web 控件，实现 ASP.NET 中的此类功能非常简单。 PasswordRecovery 控件呈现一个接口，该接口提示用户输入其用户名，并在需要时提示其安全问题的答案。 然后，通过电子邮件向用户发送其密码。

> [!NOTE]
> 由于电子邮件以纯文本方式在网络上传输，因此通过电子邮件发送用户密码会带来安全风险。

PasswordRecovery 控件包含三个视图：

- **用户名**-提示访问者输入用户名。 这是初始视图。
- **问题**-将用户的用户名和安全问题显示为文本，并将用户的文本框输入到安全问题的答案。
- **成功**-显示一条消息，告知用户其密码已通过电子邮件发送。

显示的视图和 PasswordRecovery 控件执行的操作取决于下列成员身份配置设置：

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

成员身份框架的 `RequiresQuestionAndAnswer` 设置指示用户在注册帐户时是否必须指定安全问题和答案。 如我们在<a id="_msoanchor_1"> </a>[*创建用户帐户*](../membership/creating-user-accounts-vb.md)教程中所述，如果 `RequiresQuestionAndAnswer` 为 True （默认值），则 CreateUserWizard 的接口包含新用户的安全问题和答案的 TextBox 控件;如果 `RequiresQuestionAndAnswer` 为 False，则不收集此类信息。 同样，如果 `RequiresQuestionAndAnswer` 为 True，则在用户输入用户名后，PasswordRecovery 控件将显示问题视图;仅当用户输入正确的安全答案时才会恢复密码。 但是，如果 `RequiresQuestionAndAnswer` 为 False，则 PasswordRecovery 控件将从 "用户名" 视图直接移至 "成功" 视图。

用户提供用户名或用户名和安全答案后，如果 `RequiresQuestionAndAnswer` 为 True，则 PasswordRecovery 会向用户发送其密码。 如果 `EnablePasswordRetrieval` 选项设置为 True，则用户通过电子邮件发送其当前密码。 如果将其设置为 False，并将 `EnablePasswordReset` 设置为 True，则 PasswordRecovery 控件将为用户生成一个新的随机密码，并向其发送电子邮件。 如果 `EnablePasswordRetrieval` 和 `EnablePasswordReset` 均为 False，则 PasswordRecovery 控件将引发异常。

> [!NOTE]
> 请记住，`SqlMembershipProvider` 以以下三种格式之一存储用户密码：清除、哈希（默认值）或加密。 使用的存储机制取决于成员身份配置设置;演示程序使用经过哈希处理的密码格式。 使用哈希密码格式时，`EnablePasswordRetrieval` 选项必须设置为 False，因为系统无法从存储在数据库中的哈希版本确定用户的实际密码。

图1说明了成员身份配置如何影响 PasswordRecovery 的接口和行为。

[![RequiresQuestionAndAnswer、EnablePasswordRetrieval 和 EnablePasswordReset 影响 PasswordRecovery 控件的外观和行为](recovering-and-changing-passwords-vb/_static/image2.png)](recovering-and-changing-passwords-vb/_static/image1.png)

**图 1**： `RequiresQuestionAndAnswer`、`EnablePasswordRetrieval`和 `EnablePasswordReset` 影响 PasswordRecovery 控件的外观和行为（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image3.png)）

> [!NOTE]
> <a id="_msoanchor_2"></a>在 SQL Server 教程中[*创建成员身份架构*](../membership/creating-the-membership-schema-in-sql-server-vb.md)中，我们通过将 `RequiresQuestionAndAnswer` 设置为 true，`EnablePasswordRetrieval` 设置为 False，并 `EnablePasswordReset` 为 true 来配置成员资格提供程序。

### <a name="using-the-passwordrecovery-control"></a>使用 PasswordRecovery 控件

让我们看一下如何在 ASP.NET 页中使用 PasswordRecovery 控件。 打开 `RecoverPassword.aspx` 并将 PasswordRecovery 控件从工具箱拖放到设计器上;将其 `ID` 设置为 `RecoverPwd`。 与登录和 CreateUserWizard Web 控件一样，PasswordRecovery 控件的视图呈现丰富的复合接口，其中包括标签、文本框、按钮和验证控件。 您可以通过控件的样式属性或通过将视图转换为模板来自定义视图的外观。 对于感兴趣的读者来说，我将其作为练习。

当用户访问此页面时，她将输入用户名并单击 "提交" 按钮。 由于我们在成员身份配置设置中将 `RequiresQuestionAndAnswer` 属性设置为 True，因此 PasswordRecovery 控件将显示 "问题" 视图。 用户输入正确的安全答案并单击 "提交" 后，PasswordRecovery 控件会将用户的密码更新为随机生成的密码，并通过电子邮件将此密码发送到文件上的电子邮件地址。 所有这些都是可能的，但我们必须编写一行代码！

在测试此页之前，有一个要配置的最后一段配置：需要在 `Web.config`中指定邮件传递设置。 PasswordRecovery 控件依赖于这些设置来发送电子邮件。

邮件传递配置通过[`<system.net>` 元素](https://msdn.microsoft.com/library/6484zdc1.aspx)的[`<mailSettings>` 元素](https://msdn.microsoft.com/library/w355a94k.aspx)来指定。 使用[`<smtp>` 元素](https://msdn.microsoft.com/library/ms164240.aspx)来指示传递方法和默认的 "发件人" 地址。 以下标记将邮件设置配置为在端口25上使用名为 `smtp.example.com` 的网络 SMTP 服务器，并使用用户名和密码的用户名/密码凭据。

> [!NOTE]
> `<system.net>` 是根 `<configuration>` 元素的子元素和 `<system.web>`的同级元素。 因此，请不要将 `<system.net>` 元素放在 `<system.web>` 元素内;而是将其置于同一级别。

[!code-xml[Main](recovering-and-changing-passwords-vb/samples/sample1.xml)]

除了使用网络上的 SMTP 服务器以外，还可以指定要发送的电子邮件应存放到的拾取目录。

配置 SMTP 设置后，请通过浏览器访问 `RecoverPassword.aspx` 页面。 首先尝试输入用户存储中不存在的用户名。 如图2所示，PasswordRecovery 控件显示一条消息，指示无法访问用户信息。 消息的文本可通过控件的[`UserNameFailureText` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)进行自定义。

[![如果输入无效用户名，则显示一条错误消息](recovering-and-changing-passwords-vb/_static/image5.png)](recovering-and-changing-passwords-vb/_static/image4.png)

**图 2**：如果输入了无效用户名，将显示一条错误消息（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image6.png)）

现在输入用户名。 使用系统中帐户的用户名，其中包含可访问的电子邮件地址以及你知道的安全答案。 输入用户名并单击 "提交" 后，PasswordRecovery 控件将显示其 "问题" 视图。 与 "用户名" 视图一样，如果输入错误答案，PasswordRecovery 控件会显示错误消息（请参阅图3）。 使用[`QuestionFailureText` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx)可自定义此错误消息。

[如果用户输入的安全答案无效，则会显示 ![错误消息](recovering-and-changing-passwords-vb/_static/image8.png)](recovering-and-changing-passwords-vb/_static/image7.png)

**图 3**：如果用户输入无效的安全答案（[单击查看完全大小的映像](recovering-and-changing-passwords-vb/_static/image9.png)），则显示一条错误消息

最后，输入正确的安全答案，然后单击 "提交"。 在后台，PasswordRecovery 控件生成随机密码，将其分配给用户帐户，发送一封电子邮件，告知用户其新密码（请参阅图4），然后显示 "成功" 视图。

[![使用新密码向用户发送电子邮件](recovering-and-changing-passwords-vb/_static/image11.png)](recovering-and-changing-passwords-vb/_static/image10.png)

**图 4**：向用户发送一封电子邮件，其中包含新密码（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image12.png)）

### <a name="customizing-the-email"></a>自定义电子邮件

PasswordRecovery 控件发送的默认电子邮件相当暗（参见图4）。 将从 `<smtp>` 元素的 `from` 属性中指定的帐户发送消息，其中包含主题密码和纯文本正文：

请返回到站点并使用以下信息登录。

用户名：*用户名*

密码：*密码*

可以通过 PasswordRecovery 控件的[`SendingMail` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)的事件处理程序以编程方式自定义此消息，也可以通过[`MailDefinition` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)以声明方式自定义此消息。 让我们浏览一下这两个选项。

在发送电子邮件之前，将立即触发 `SendingMail` 事件，这是我们最后一次用来以编程方式调整电子邮件的机会。 引发此事件时，会向事件处理程序传递类型[`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)的对象，其 `Message` 属性包含对要发送的电子邮件的引用。

为 `SendingMail` 事件创建事件处理程序并添加以下代码，以编程方式将 `webmaster@example.com` 添加到 CC 列表。

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample2.vb)]

还可以通过声明性方式配置电子邮件。 PasswordRecovery 的 `MailDefinition` 属性是[`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)类型的对象。 `MailDefinition` 类提供与电子邮件相关的属性的宿主，其中包括 `From`、`CC`、`Priority`、`Subject`、`IsBodyHtml`、`BodyFileName`和其他属性。 对于初学者，请将[`Subject` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx)设置为比默认使用的（密码）更具描述性的内容，如你的密码已重置 。

若要自定义电子邮件的正文，我们需要创建一个包含正文内容的单独电子邮件模板文件。 首先在名为 `EmailTemplates`的网站中创建一个新文件夹。 接下来，向此文件夹中添加名为 "`PasswordRecovery.txt`" 的新文本文件，并添加以下内容：

[!code-aspx[Main](recovering-and-changing-passwords-vb/samples/sample3.aspx)]

请注意 `<%UserName%>` 和 `<%Password%>`使用占位符。 在发送电子邮件之前，PasswordRecovery 控件会自动将这两个占位符替换为用户的用户名和已恢复密码。

最后，将 `MailDefinition`的[`BodyFileName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)指向刚刚创建的电子邮件模板（`~/EmailTemplates/PasswordRecovery.txt`）。

进行这些更改后，请重新访问 `RecoverPassword.aspx` 页面，并输入你的用户名和安全答案。 您收到的电子邮件应类似于图5所示。 请注意，`webmaster@example.com` 已是抄送，并已更新主题和正文。

[已更新 "主题"、"正文" 和 "抄送" 列表 ![](recovering-and-changing-passwords-vb/_static/image14.png)](recovering-and-changing-passwords-vb/_static/image13.png)

**图 5**： "主题"、"正文" 和 "抄送" 列表已更新（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image15.png)）

若要将 HTML 格式的电子邮件集[`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx)设置为 True （默认值为 False），并更新电子邮件模板以包含 HTML。

`MailDefinition` 属性对 PasswordRecovery 类不是唯一的。 如我们将在步骤2中看到的那样，ChangePassword 控件还提供 `MailDefinition` 属性。 而且，CreateUserWizard 控件包含这样一个属性，你可以将其配置为自动向新用户发送欢迎电子邮件。

> [!NOTE]
> 当前左侧导航栏中没有用于到达 `RecoverPassword.aspx` 页面的链接。 如果用户无法成功登录到站点，则该用户只会对访问此页感兴趣。 因此，请更新 `Login.aspx` 页面以包括指向 `RecoverPassword.aspx` 页面的链接。

### <a name="programmatically-resetting-a-users-password"></a>以编程方式重置用户的密码

重置用户密码时，PasswordRecovery 控件将调用 `MembershipUser` 对象的[`ResetPassword` 方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)。 此方法有两个重载：

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -重置用户的密码。 如果 `RequiresQuestionAndAnswer` 为 False，则使用此重载。
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -仅当提供的*securityAnswer*正确时重置用户的密码。 如果 `RequiresQuestionAndAnswer` 为 True，则使用此重载。

两个重载都返回新的、随机生成的密码。

与成员身份框架中的其他方法一样，`ResetPassword` 方法委托给已配置的提供程序。 `SqlMembershipProvider` 调用 `aspnet_Membership_ResetPassword` 存储过程，并传入用户的用户名、新密码以及提供的密码答案，包括其他字段。 该存储过程可确保密码答案匹配，然后更新用户的密码。

几个低级别的实现说明：

- 锁定的用户无法重置其密码。 但未经批准的用户可能会。 在<a id="_msoanchor_3"> </a>[*解锁和批准用户*](unlocking-and-approving-user-accounts-vb.md)帐户教程中，我们将更详细地讨论锁定和批准的状态。
- 如果密码答案不正确，则会增加用户的密码答案尝试计数。 如果在指定的时间范围内发生指定数量的无效安全答案尝试，则用户将被锁定。

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>有关如何生成随机密码的单词

图4和5中的电子邮件中显示的随机生成的密码由成员身份类的[`GeneratePassword` 方法](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)创建。 此方法接受两个整数输入参数-*长度*和*numberOfNonAlphanumericCharacters* ，并返回至少*长度*字符至少为*numberOfNonAlphanumericCharacters*的非字母数字字符的字符串。 如果从成员身份类或与登录相关的 Web 控件中调用此方法，则这两个参数的值由成员身份配置的 `MinRequiredPasswordLength` 和 `MinRequiredNonalphanumericCharacters` 属性确定，该属性分别设置为7和1。

`GeneratePassword` 方法使用加密型强随机数生成器，以确保选择了多少个随机字符。 此外，`GeneratePassword` `Public`，这意味着，如果需要生成随机字符串或密码，则可以直接从 ASP.NET 应用程序使用它。

> [!NOTE]
> `SqlMembershipProvider` 类始终生成长度至少为14个字符的随机密码，因此如果 `MinRequiredPasswordLength` 小于14，则将忽略其值。

## <a name="step-2-changing-passwords"></a>步骤2：更改密码

随机生成的密码很难记住。 请考虑图4： `WWGUZv(f2yM:Bd`中所示的密码。 尝试将其提交到内存！ 不用说，在向用户发送此类随机生成的密码后，她需要将密码更改为更容易记住的内容。

使用 "ChangePassword" 控件创建一个界面，以便用户可以更改其密码。 与 PasswordRecovery 控件非常类似，ChangePassword 控件包含两个视图：更改密码和成功。 "更改密码" 视图会提示用户输入其旧密码和新密码。 提供正确的旧密码和满足最小长度和非字母数字字符要求的新密码后，ChangePassword 控件会更新用户的密码并显示 "成功" 视图。

> [!NOTE]
> ChangePassword 控件通过调用 `MembershipUser` 对象的[`ChangePassword` 方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)来修改用户的密码。 ChangePassword 方法接受两个 `String` 输入参数- *oldPassword*和*newPassword*，并更新用户与*newPassword*的帐户，假设提供的*oldPassword*是正确的。

打开 `ChangePassword.aspx` 页面，向页面添加一个 ChangePassword 控件，并将其命名为 `ChangePwd`。 此时，设计视图应显示 "更改密码" 视图（见图6）。 与 PasswordRecovery 控件一样，可以通过控件的智能标记在视图之间切换。 此外，这些视图的外观可以通过各种样式属性进行自定义，也可以通过将它们转换为模板进行自定义。

[![向页面添加 ChangePassword 控件](recovering-and-changing-passwords-vb/_static/image17.png)](recovering-and-changing-passwords-vb/_static/image16.png)

**图 6**：将 ChangePassword 控件添加到页面（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image18.png)）

ChangePassword 控件可以更新当前已登录用户的密码*或*其他指定用户的密码。 如图6所示，默认的 "更改密码" 视图仅呈现三个 TextBox 控件：一个用于旧密码，两个用于新密码。 此默认接口用于更新当前已登录用户的密码。

若要使用 ChangePassword 控件更新其他用户的密码，请将控件的[`DisplayUserName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx)设置为 True。 这样做会向页面添加第四个文本框，并提示输入要更改密码的用户的用户名。

如果希望注销用户更改其密码，而无需登录，将 `DisplayUserName` 设置为 "True" 会很有用。 从个人角度来看，在要求用户更改其密码之前，不会有任何问题需要用户登录。 因此，将 `DisplayUserName` 设置为 False （默认值）。 然而，在做出此决定的过程中，我们实际上会阻止匿名用户访问此页。 更新站点的 URL 授权规则，以便拒绝匿名用户访问 `ChangePassword.aspx`。 如果需要刷新 URL 授权规则语法上的内存，请返回到<a id="_msoanchor_4"> </a>[*基于用户的授权*](../membership/user-based-authorization-vb.md)教程。

> [!NOTE]
> 可能看起来 `DisplayUserName` 属性对允许管理员更改其他用户的密码很有用。 但是，即使将 `DisplayUserName` 设置为 True，也必须知道并输入正确的旧密码。 我们将讨论允许管理员在步骤3中更改用户密码的方法。

通过浏览器访问 `ChangePassword.aspx` 页面并更改密码。 请注意，如果输入的新密码无法满足成员身份配置中指定的密码长度和非字母数字字符要求，则会显示一条错误消息（请参阅图7）。

[![向页面添加 ChangePassword 控件](recovering-and-changing-passwords-vb/_static/image20.png)](recovering-and-changing-passwords-vb/_static/image19.png)

**图 7**：将 ChangePassword 控件添加到页面（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image21.png)）

输入正确的旧密码和有效的新密码后，已登录用户的密码已更改，并显示 "成功" 视图。

### <a name="sending-a-confirmation-email"></a>发送确认电子邮件

默认情况下，ChangePassword 控件不会将电子邮件发送到刚更新了其密码的用户。 如果要发送电子邮件，只需配置该控件的 `MailDefinition` 属性。 让我们配置 ChangePassword 控件，以便向用户发送包含其新密码的 HTML 格式电子邮件。

首先在名为 `ChangePassword.htm``EmailTemplates` 文件夹中创建一个新文件。 添加以下标记：

[!code-html[Main](recovering-and-changing-passwords-vb/samples/sample4.html)]

接下来，将 ChangePassword 控件的 `MailDefinition` 属性的 `BodyFileName`、`IsBodyHtml`和 `Subject` 属性分别设置为 ~/EmailTemplates/ChangePassword.htm、True，并且密码已更改！。

进行这些更改后，重新访问页面并再次更改密码。 此时，ChangePassword 控件会向用户的电子邮件地址发送一封自定义的 HTML 格式的电子邮件，如图8所示。

[![电子邮件通知用户其密码已更改](recovering-and-changing-passwords-vb/_static/image23.png)](recovering-and-changing-passwords-vb/_static/image22.png)

**图 8**：电子邮件通知用户其密码已更改（[单击查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image24.png)）

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>步骤3：允许管理员更改用户密码

支持用户帐户的应用程序中的一项常见功能是使管理用户能够更改其他用户的密码。 有时，此功能是必需的，因为系统不能让用户更改自己的密码。 在这种情况下，使用户恢复忘记的密码的唯一方法是让管理员为其分配新密码。 然而，对于 PasswordRecovery 和 ChangePassword 控件，管理用户无需忙于更改用户密码，因为用户能够自行完成此操作。

但是，如果您的客户端一定管理用户应能够更改其他用户的密码，该怎么办？ 遗憾的是，添加此功能可能是一种工作。 若要更改用户的密码，必须向 `MembershipUser` 对象的 `ChangePassword` 方法提供旧密码和新密码，但管理员无需知道用户密码即可修改该用户的密码。

一种解决方法是先重置用户的密码，然后使用如下代码将其更改为新密码：

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample5.vb)]

此代码首先检索有关*用户名*的信息，这是管理员希望更改其密码的用户。 接下来，调用 `ResetPassword` 方法，该方法为用户分配新的随机密码。 此随机生成的密码由方法返回，并存储在变量 `resetPwd`中。 现在我们知道了用户的密码，可以通过调用 `ChangePassword`对其进行更改。

问题在于，此代码仅在设置了成员身份系统配置时才适用，因此 `RequiresQuestionAndAnswer` 为 False。 如果 `RequiresQuestionAndAnswer` 为 True，与我们的应用程序一样，则需要将 `ResetPassword` 方法传递到安全答案，否则将引发异常。

如果成员身份框架配置为需要安全问题和答案，但你的客户端一定管理员能够更改用户的密码，则有三个选项：

- 将你的双手掷到你的空气中，并告诉客户端这只是一个无法完成的事情。
- 将 `RequiresQuestionAndAnswer` 设置为 False。 这会导致应用程序不太安全。 假设恶意用户已获得对另一个用户的电子邮件收件箱的访问权限。 可能是被泄露的用户离开了其办公桌去吃午餐，或者他们的工作站没有锁定，或者他们的电子邮件来自公共终端并且未注销。在任一情况下，恶意用户都可以访问 `RecoverPassword.aspx` 页面，并输入用户的用户名。 然后，系统会通过电子邮件发送恢复的密码，而不提示您提供安全答案。
- 绕过成员身份框架创建的抽象层，并直接使用 SQL Server 数据库。 成员身份架构包含一个名为 `aspnet_Membership_SetPassword` 的存储过程，该过程设置用户的密码，不需要安全答案或旧密码即可完成其任务。

这些选项中的任何一个都不是很有吸引力，但这也是开发人员的生命周期。

接下来，我实现了第三种方法，即编写绕过 `Membership` 和 `MembershipUser` 类的代码，并直接对 `SecurityTutorials` 数据库进行操作。

> [!NOTE]
> 通过直接处理数据库，成员身份框架提供的封装会被损坏。 此决策将我们与 `SqlMembershipProvider`联系起来，使代码变得更小。 此外，如果成员身份架构发生更改，则在未来版本的 ASP.NET 中，此代码可能无法按预期工作。 此方法是一种解决方法，如大多数解决方法，并不是最佳做法的示例。

此代码有一些不严重位，并且非常长。 因此，在本教程中，我不想对其进行深入研究。 如果对了解详细信息感兴趣，请下载本教程的代码，并访问 `~/Administration/ManageUsers.aspx` 页面。 在<a id="_msoanchor_5"> </a>[前面的教程](building-an-interface-to-select-one-user-account-from-many-vb.md)中创建的此页列出了每个用户。 我已经更新了 GridView，使其包含指向 `UserInformation.aspx` 页面的链接，并通过查询字符串传递选定用户的用户名。 "`UserInformation.aspx`" 页将显示有关所选用户和用于更改其密码的文本框的信息（请参阅图9）。

输入新密码后，在第二个文本框中确认该密码，然后单击 "更新用户" 按钮，将调用回发可以和 `aspnet_Membership_SetPassword` 存储过程，从而更新用户的密码。 我鼓励这些读者对此功能感兴趣，以更熟悉代码，并尝试扩展功能，将电子邮件发送到用户的密码已更改。

[![管理员可以更改用户的密码](recovering-and-changing-passwords-vb/_static/image26.png)](recovering-and-changing-passwords-vb/_static/image25.png)

**图 9**：管理员可以更改用户的密码（[单击以查看完全大小的图像](recovering-and-changing-passwords-vb/_static/image27.png)）

> [!NOTE]
> 如果成员身份框架配置为以明文或哈希格式存储密码，则当前仅适用于 `UserInformation.aspx` 页。 尽管邀请你添加此功能，但它缺少加密新密码的代码。 我建议添加所需的代码的方法是使用反编译程序等[反射](http://www.aisto.com/roeder/dotnet/)器来检查 .NET Framework 中方法的源代码：首先检查 `SqlMembershipProvider` 类的 `ChangePassword` 方法。 这是我用来编写用于创建密码哈希的代码的方法。

## <a name="summary"></a>总结

ASP.NET 提供了两个控件来帮助用户管理其密码。 PasswordRecovery 控件对于忘记了密码的用户非常有用。 根据成员身份框架的配置，用户可以通过电子邮件发送其现有密码或随机生成的新密码。 通过 ChangePassword 控件，用户可以更新其密码。

与登录名和 CreateUserWizard 控件一样，PasswordRecovery 和 ChangePassword 控件呈现丰富的用户界面，而无需编写声明性标记或代码行的舔。 如果默认用户界面不能满足您的需要，则可以通过各种样式属性对其进行自定义。 或者，控件的接口可能会转换为模板，以获得更精细的控制。 在后台，这些控件使用成员资格 API，调用 `MembershipUser` 对象的 `ResetPassword` 和 `ChangePassword` 方法。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ChangePassword 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` 常见问题](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者包括 Michael Emmings 和 Suchi Banerjee。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](building-an-interface-to-select-one-user-account-from-many-vb.md)
> [下一页](unlocking-and-approving-user-accounts-vb.md)
