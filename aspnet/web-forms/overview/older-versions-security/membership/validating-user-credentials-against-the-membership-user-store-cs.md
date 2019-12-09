---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: 针对成员身份用户存储（C#）验证用户凭据 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将介绍如何使用编程方式和登录控件 ... 为成员身份用户存储验证用户凭据。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: aaf6df6f52253ef0f7369a7e77211b6786b97db1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618051"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>针对成员身份用户存储验证用户凭据 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip)或[下载 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> 在本教程中，我们将介绍如何使用编程方式和登录控件验证用户凭据与成员资格用户存储。 我们还将介绍如何自定义登录控件的外观和行为。

## <a name="introduction"></a>简介

在<a id="Tutorial05"> </a>[前面的教程](creating-user-accounts-cs.md)中，我们介绍了如何在成员身份框架中创建新的用户帐户。 首先，我们将了解如何通过 `Membership` 类的 `CreateUser` 方法以编程方式创建用户帐户，然后使用 CreateUserWizard Web 控件进行检查。 但是，登录页当前根据用户名和密码对的硬编码列表对提供的凭据进行验证。 我们需要更新登录页的逻辑，以便它根据成员身份框架的用户存储区来验证凭据。

与创建用户帐户非常类似，可以通过编程方式或声明方式验证凭据。 成员资格 API 包含一个方法，用于以编程方式根据用户存储区来验证用户的凭据。 和 ASP.NET 随登录 Web 控件一起提供，后者使用用户名和密码的文本框以及用于登录的按钮来呈现用户界面。

在本教程中，我们将介绍如何使用编程方式和登录控件验证用户凭据与成员资格用户存储。 我们还将介绍如何自定义登录控件的外观和行为。 让我们进入正题！

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>步骤1：根据成员身份用户存储验证凭据

对于使用 forms 身份验证的网站，用户可以通过访问登录页面并输入其凭据登录到网站。 然后，将这些凭据与用户存储进行比较。 如果这些凭据有效，则向用户授予 forms 身份验证票证，这是一个指示访问者身份和身份验证的安全令牌。

若要针对成员身份框架验证用户，请使用 `Membership` 类的[`ValidateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)。 `ValidateUser` 方法采用两个输入参数- *`username`* 和 *`password`* ，并返回一个布尔值，指示凭据是否有效。 与我们在上一教程中所述的 `CreateUser` 方法类似，`ValidateUser` 方法将实际验证委托给已配置的成员资格提供程序。

`SqlMembershipProvider` 通过 `aspnet_Membership_GetPasswordWithFormat` 存储过程获取指定用户的密码来验证提供的凭据。 回忆一下，`SqlMembershipProvider` 使用以下三种格式之一来存储用户密码：明文、加密或哈希。 `aspnet_Membership_GetPasswordWithFormat` 存储过程以原始格式返回密码。 对于加密或哈希密码，`SqlMembershipProvider` 会将传入 `ValidateUser` 方法的 *`password`* 值转换为其等效的加密或哈希状态，然后将其与从数据库中返回的内容进行比较。 如果存储在数据库中的密码与用户输入的格式化密码相匹配，则凭据有效。

让我们更新登录页（~/`Login.aspx`），以便它根据成员身份框架用户存储验证提供的凭据。 我们在<a id="Tutorial02"> </a>[*窗体身份验证概述*](../introduction/an-overview-of-forms-authentication-cs.md)教程中创建了此登录页，并创建了一个包含两个文本框的 "用户名" 和 "密码" 文本框、"记住我" 复选框和一个 "登录" 按钮（参见图1）。 此代码根据用户名和密码对的硬编码列表（Scott/密码、Jisun/密码和 Sam/密码）来验证输入的凭据。 <a id="Tutorial03"></a>在[*forms 身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教程中，我们更新了登录页的代码，以将其他信息存储在 Forms 身份验证票证的 `UserData` 属性中。

[登录页的接口 ![包括两个文本框、一个 CheckBoxList 和一个按钮](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**图 1**：登录页的接口包括两个文本框：一个 CheckBoxList 和一个按钮（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png)）

登录页的用户界面可以保持不变，但我们需要将登录按钮的 `Click` 事件处理程序替换为针对成员身份框架用户存储验证用户的代码。 更新事件处理程序，使其代码如下所示：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

此代码非常简单。 首先，我们调用 `Membership.ValidateUser` 方法，并传入提供的用户名和密码。 如果该方法返回 true，则用户通过 `FormsAuthentication` 类的 Formsauthentication.redirectfromloginpage 方法登录到网站。 （如我们在<a id="Tutorial2"> </a> [*Forms 身份验证概述*](../introduction/an-overview-of-forms-authentication-cs.md)教程中所述，`FormsAuthentication.RedirectFromLoginPage` 会创建 forms 身份验证票证，然后将用户重定向到适当的页面。）但是，如果凭据无效，则会显示 `InvalidCredentialsMessage` 标签，通知用户其用户名或密码不正确。

就这么简单！

若要测试登录页面是否按预期运行，请尝试使用在前面的教程中创建的用户帐户之一登录。 或者，如果尚未创建帐户，请继续从 "`~/Membership/CreatingUserAccounts.aspx`" 页中创建一个帐户。

> [!NOTE]
> 当用户输入其凭据并提交登录页表单时，凭据（包括她的密码）将通过 Internet 以*纯文本*形式传输到 web 服务器。 这意味着任何黑客探查网络流量都能看到用户名和密码。 若要防止出现这种情况，必须使用[安全套接字层（SSL）](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)加密网络流量。 这将确保在 web 服务器接收到浏览器之前，会对凭据（以及整页的 HTML 标记）进行加密。

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>成员资格框架如何处理无效的登录尝试

当访问者到达登录页面并提交其凭据时，他们的浏览器会向登录页发出 HTTP 请求。 如果凭据有效，HTTP 响应将在 cookie 中包含身份验证票证。 因此，尝试侵入网站的黑客可能会创建一个程序，该程序使用有效的用户名并在密码上猜测来向登录页发送 HTTP 请求。 如果密码推测正确，则登录页将返回身份验证票证 cookie，此时程序知道该 cookie 已跌倒有效的用户名/密码对。 通过暴力破解，此类程序可能能够碰到用户密码，尤其是在密码较弱的情况下。

若要防止这种暴力攻击，成员身份框架会锁定用户，前提是在某个时间段内有一定次数的失败登录尝试。 可以通过以下两个成员资格提供程序配置设置来配置确切的参数：

- `maxInvalidPasswordAttempts`-指定用户在帐户被锁定之前的时间段内允许多少次无效密码尝试。默认值为5。
- `passwordAttemptWindow`-表示指定的无效登录尝试次数将导致帐户被锁定的时间段，以分钟为单位。默认值为10。

如果用户已被锁定，她将无法登录，直到管理员解锁其帐户。 锁定用户时，`ValidateUser` 方法将*始终*返回 `false`，即使提供了有效凭据也是如此。 尽管此行为降低了黑客通过暴力破解方法进入你的站点的可能性，但最终最终会锁定一个有效的用户，该用户只是忘记了自己的密码，或者无意中出现了 Caps Lock 或出现了错误的键入日期。

遗憾的是，没有用于解锁用户帐户的内置工具。 为了解除帐户锁定，你可以直接修改数据库，将 `aspnet_Membership` 表中的 "`IsLockedOut`" 字段更改为相应的用户帐户，或者创建一个基于 web 的界面，其中列出已锁定的帐户，其中包含用于解锁它们的选项。 在将来的教程中，我们将介绍如何创建用于完成常见用户帐户和与角色相关任务的管理界面。

> [!NOTE]
> `ValidateUser` 方法的一个缺点是，当提供的凭据无效时，它不会提供任何有关原因的解释。 凭据可能无效，因为用户存储区中没有匹配的用户名/密码对，或者用户尚未获得批准，或用户已被锁定。在步骤4中，我们将了解如何在登录尝试失败时向用户显示更详细的消息。

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>步骤2：通过登录 Web 控件收集凭据

[登录 Web 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)呈现的默认用户界面非常类似于我们在<a id="SKM5"> </a> [*Forms 身份验证概述*](../introduction/an-overview-of-forms-authentication-cs.md)教程中创建的用户界面。 使用登录控件，使我们能够创建用于收集访问者凭据的接口。 而且，登录控件会自动登录用户（假定提交的凭据有效），从而使我们不必编写任何代码。

让我们更新 `Login.aspx`，将手动创建的接口和代码替换为登录控件。 首先，删除 `Login.aspx`中的现有标记和代码。 您可以完全删除它，或者只是将其注释掉。若要注释声明性标记，请将其括在 `<%--` 和 `--%>` 分隔符。 您可以手动输入这些分隔符，或者如图2所示，您可以选择要注释掉的文本，然后单击工具栏中的 "选定的行" 图标注释掉。 同样，可以使用注释掉所选的行图标注释掉代码隐藏类中的选定代码。

[![在 default.aspx 中注释掉现有声明性标记和源代码](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**图 2**：在 `Login.aspx` 中注释掉现有声明性标记和源代码（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png)）

> [!NOTE]
> 在 Visual Studio 2005 中查看声明性标记时，"注释掉所选行" 图标不可用。 如果未使用 Visual Studio 2008，则需要手动添加 `<%--` 和 `--%>` 分隔符。

接下来，将 "登录" 控件从 "工具箱" 拖到页面上，然后将其 `ID` 属性设置为 "`myLogin`"。 此时，屏幕应类似于图3所示。 请注意，登录控件的默认界面包含 "用户名" 和 "密码" 的 TextBox 控件、"下次记住我" 复选框和 "登录" 按钮。 这两个文本框还有 `RequiredFieldValidator` 控件。

[![将登录控件添加到页面](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**图 3**：将登录控件添加到页面（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png)）

我们已经完成了！ 单击登录控件的 "登录" 按钮时，将发生回发，登录控件将调用 `Membership.ValidateUser` 方法，并传入输入的用户名和密码。 如果凭据无效，登录控件会显示一条消息，指出这样。 但是，如果凭据有效，则登录控件会创建 forms 身份验证票证，并将用户重定向到相应的页面。

登录控件使用四个因素来确定成功登录时要将用户重定向到的适当页面：

- 登录控件是否位于由 forms 身份验证配置中 `loginUrl` 设置定义的登录页上;此设置的默认值为 `Login.aspx`
- 存在 `ReturnUrl` querystring 参数
- 登录控件的[`DestinationUrl` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)的值
- Forms 身份验证配置设置中指定的 `defaultUrl` 值;此设置的默认值为 `Default.aspx`

图4描述了登录控件如何使用这四个参数到达其相应的页面决定。

[![将登录控件添加到页面](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**图 4**：将登录控件添加到页面（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png)）

通过访问浏览器并以成员身份框架中的现有用户身份登录，花点时间测试登录控件。

登录控件的呈现接口具有高度的可配置性。 有许多属性会影响其外观;而且，可以将登录控件转换为模板，以便精确地控制用户界面元素的布局。 此步骤的其余部分将检查如何自定义外观和布局。

### <a name="customizing-the-login-controls-appearance"></a>自定义登录控件的外观

登录控件的默认属性设置将使用 "用户名" 和 "密码" 输入的 "用户名" 和 "密码" 输入的 "记住我" 复选框和 "登录" 按钮呈现具有标题（登录）、文本框和标签控件的用户界面。 这些元素的外观均可通过登录控件的大量属性进行配置。 此外，还可以通过设置一个属性或两个来添加其他用户界面元素（例如指向用于创建新用户帐户的页面的链接）。

让我们花点时间来 gussy 登录控件的外观。 由于 `Login.aspx` 页面的顶部已经显示了 "登录" 页的顶部，因此登录控件的标题是多余的。 因此，请清除[`TitleText` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx)值，以便删除登录控件的标题。

两个 TextBox 控件左侧的 "用户名：" 和 "密码：" 标签分别可通过 " [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) " 和 " [`PasswordLabelText`" 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)进行自定义。 让我们更改 "用户名：" 标签以阅读用户名：。 标签和文本框样式可分别通过[`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx)和[`TextBoxStyle` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)进行配置。

"下次记住我" 复选框的文本属性可通过登录控件的[`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx)进行设置，其默认的选中状态可通过[`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) （默认为 False）进行配置。 继续操作并将 `RememberMeSet` 属性设置为 True，以便默认选中 "记住我下一次" 复选框。

登录控件提供了两个属性，用于调整其用户界面控件的布局。 [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx)指示用户名：和密码：标签是显示在其对应的文本框（默认值）或其上方的左侧。 [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx)指示用户名和密码输入是垂直的（在另一个上）还是水平放置。 我要使这两个属性设置为其默认值，但是我建议您尝试将这两个属性设置为非默认值，以查看结果结果。

> [!NOTE]
> 在下一部分中，配置登录控件的布局时，我们将介绍如何使用模板定义布局控件的用户界面元素的精确布局。

是否通过将[`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx)和[`CreateUserUrl` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx)设置为 "尚未注册" 来将登录控件的属性设置 创建帐户！ 和 `~/Membership/CreatingUserAccounts.aspx`。 这会向登录控件的接口添加一个超链接，该超链接指向在<a id="SKM6"> </a>[上一教程](creating-user-accounts-cs.md)中创建的页面。 登录控件的[`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx)和[`HelpPageUrl` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx)以及[`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx)和[`PasswordRecoveryUrl` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx)的工作方式相同，它将链接到帮助页和密码恢复页。

进行这些属性更改后，登录控件的声明性标记和外观应类似于图5所示。

[![登录控件的属性值决定了其外观](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**图 5**：登录控件的属性值决定了其外观（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png)）

### <a name="configuring-the-login-controls-layout"></a>配置登录控件的布局

登录 Web 控件的默认用户界面在 HTML `<table>`中布局界面。 但如果我们需要更好地控制呈现的输出，该怎么办？ 也许我们需要将 `<table>` 替换为一系列 `<div>` 标记。 如果我们的应用程序需要其他凭据进行身份验证，该怎么办？ 例如，许多金融网站要求用户不仅提供用户名和密码，还需要提供个人标识号（PIN）或其他标识信息。 无论原因是什么，都可以将登录控件转换为模板，以便可以显式定义接口的声明性标记。

我们需要执行两项操作，以便更新登录控件以收集其他凭据：

1. 更新登录控件的接口以包含用于收集其他凭据的 Web 控件。
2. 重写登录控件的内部身份验证逻辑，以便仅在用户的用户名和密码有效并且其其他凭据有效时才对其进行身份验证。

若要完成第一个任务，需要将登录控件转换为模板，并添加必要的 Web 控件。 对于第二个任务，可以通过为控件的[`Authenticate` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)创建事件处理程序来取代登录控件的身份验证逻辑。

让我们更新登录控件，使其提示用户输入其用户名、密码和电子邮件地址，并且仅当提供的电子邮件地址与文件上的电子邮件地址匹配时才对用户进行身份验证。 首先需要将登录控件的接口转换为模板。 从登录控件的智能标记中，选择 "转换为模板" 选项。

[![将登录控件转换为模板](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**图 6**：将登录控件转换为模板（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png)）

> [!NOTE]
> 若要将登录控件恢复为其预模板版本，请单击控件的智能标记中的 "重置" 链接。

将登录控件转换为模板会将 `LayoutTemplate` 添加到控件的声明性标记中，其中包含 HTML 元素和定义用户界面的 Web 控件。 如图7所示，将控件转换为模板会从属性窗口中移除许多属性，如 `TitleText`、`CreateUserUrl`等，因为在使用模板时将忽略这些属性值。

[当登录控件转换为模板时，![更少的属性可用](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**图 7**：将登录控件转换为模板时的可用属性更少（[单击查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png)）

`LayoutTemplate` 中的 HTML 标记可以根据需要进行修改。 同样，也可以随意将任何新的 Web 控件添加到模板。 但重要的是，登录控件的核心 Web 控件保留在模板中，并将其分配 `ID` 值。 特别是，不要删除或重命名 `UserName` 或 `Password` 文本框、"`RememberMe`" 复选框、"`LoginButton`" 按钮、"`FailureText`" 标签或 `RequiredFieldValidator` 控件。

若要收集访问者的电子邮件地址，需要在模板中添加一个文本框。 在包含 "`Password`" 文本框的表行（`<tr>`）和保留 "下次记住我" 复选框的表行之间添加以下声明性标记：

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

添加 "`Email`" 文本框后，请通过浏览器访问此页。 如图8所示，登录控件的用户界面现在包含第三个文本框。

[![登录控件现在包含用户电子邮件地址的文本框](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**图 8**：登录控件现在包含用户电子邮件地址的文本框（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png)）

此时，登录控件仍使用 `Membership.ValidateUser` 方法来验证提供的凭据。 同样，在 "`Email`" 文本框中输入的值与用户是否可以登录无关。 在步骤3中，我们将介绍如何替代登录控件的身份验证逻辑，以便仅在用户名和密码有效并且所提供的电子邮件地址与文件上的电子邮件地址匹配时才将凭据视为有效。

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>步骤3：修改登录控件的身份验证逻辑

当访问者提供自己的凭据并单击 "登录" 按钮时，回发可以和登录控件会通过其身份验证工作流进行。 工作流首先引发[`LoggingIn` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)。 与此事件关联的任何事件处理程序都可以通过将 `e.Cancel` 属性设置为 `true`来取消登录操作。

如果未取消登录操作，则工作流将通过引发[`Authenticate` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)进行。 如果有 `Authenticate` 事件的事件处理程序，则负责确定所提供的凭据是否有效。 如果未指定任何事件处理程序，则登录控件将使用 `Membership.ValidateUser` 方法来确定凭据的有效性。

如果提供的凭据有效，则创建 forms 身份验证票证，引发[`LoggedIn` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx)，并将用户重定向到相应的页面。 但是，如果凭据被视为无效，则会引发[`LoginError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx)，并显示一条消息，告知用户其凭据无效。 默认情况下，在失败时，登录控件只需将其 `FailureText` 标签控件的 Text 属性设置为失败消息（登录尝试不成功。 请重试。 但是，如果将登录控件的[`FailureAction` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx)设置为 `RedirectToLoginPage`，则登录控件会向登录页发出 `Response.Redirect`，并追加 querystring 参数 `loginfailure=1` （这会导致登录控件显示失败消息）。

图9提供身份验证工作流的流程图。

[![登录控件的身份验证工作流](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**图 9**：登录控件的身份验证工作流（[单击以查看完全大小的映像](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png)）

> [!NOTE]
> 如果您想知道何时使用 `FailureAction`的 `RedirectToLogin` 页选项，请考虑以下方案。 现在，当匿名用户访问时，`Site.master` 母版页当前包含在左列中显示的文本 stranger，但假设我们想要将该文本替换为登录控件。 这将允许匿名用户从网站上的任何页面登录，而不需要他们直接访问登录页。 但是，如果用户无法通过母版页呈现的登录控件登录，则可以将它们重定向到登录页（`Login.aspx`），因为该页面可能包括其他说明、链接和其他帮助，例如，用于创建新帐户或检索丢失密码的链接（未添加到母版页中）。

### <a name="creating-theauthenticateevent-handler"></a>创建`Authenticate`事件处理程序

为了插入自定义身份验证逻辑，需要为登录控件的 `Authenticate` 事件创建事件处理程序。 为 `Authenticate` 事件创建事件处理程序将生成以下事件处理程序定义：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

正如您所看到的，`Authenticate` 事件处理程序将[`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx)类型的对象作为它的第二个输入参数传递。 `AuthenticateEventArgs` 类包含一个名为 `Authenticated` 的布尔值属性，该属性用于指定提供的凭据是否有效。 然后，我们的任务是在此处编写代码来确定所提供的凭据是否有效，并相应地设置 `e.Authenticate` 属性。

### <a name="determining-and-validating-the-supplied-credentials"></a>确定和验证提供的凭据

使用登录控件的[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx)和[`Password` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx)来确定用户输入的用户名和密码凭据。 若要确定输入到任何其他 Web 控件（例如在上一步中添加的 `Email` 文本框）中输入的值，请使用 *`LoginControlID`* `.FindControl`（" *`controlID`* "）来获取对模板中的 Web 控件的编程引用，其 `ID` 属性等于 *`controlID`* 。 例如，若要获取对 `Email` 文本框的引用，请使用以下代码：

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

若要验证用户的凭据，需要执行两项操作：

1. 确保提供的用户名和密码有效
2. 确保输入的电子邮件地址与尝试登录的用户的文件中的电子邮件地址匹配

若要完成第一次检查，只需使用 `Membership.ValidateUser` 方法，就像我们在步骤1中看到的那样。 对于第二个检查，需要确定用户的电子邮件地址，以便我们可以将其与在 TextBox 控件中输入的电子邮件地址进行比较。 若要获取有关特定用户的信息，请使用 `Membership` 类的[`GetUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)。

`GetUser` 方法有很多重载。 如果在不传递任何参数的情况下使用，则它将返回有关当前已登录用户的信息。 若要获取有关特定用户的信息，请调用 `GetUser` 传入用户名。 无论采用哪种方式，`GetUser` 都将返回一个[`MembershipUser` 对象](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)，该对象的属性如 `UserName`、`Email`、`IsApproved`、`IsOnline`等。

下面的代码实现了这两个检查。 如果通过，则将 `e.Authenticate` 设置为 `true`，否则将为其分配 `false`。

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

使用此代码后，尝试以有效用户的身份登录，并输入正确的用户名、密码和电子邮件地址。 再次尝试此方法，但这一次有意使用错误的电子邮件地址（请参阅图10）。 最后，使用不存在的用户名进行第三次尝试。 在第一种情况下，应成功登录到站点，但在最后两种情况下，应会看到登录控件的无效凭据消息。

[提供不正确的电子邮件地址时，![Tito 无法登录](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**图 10**：当提供不正确的电子邮件地址时，Tito 无法登录（[单击以查看完全大小的图像](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png)）

> [!NOTE]
> 如在步骤1中，成员身份框架如何处理无效的登录尝试部分中所述，当调用 `Membership.ValidateUser` 方法并且传递的凭据无效时，它将跟踪无效的登录尝试并锁定用户，前提是在指定的时间范围内超过特定阈值的无效尝试。 由于自定义身份验证逻辑调用 `ValidateUser` 方法，因此有效用户名的密码不正确将增加无效的登录尝试计数器，但如果用户名和密码有效，但电子邮件地址不正确，则此计数器不会增加。 此行为很可能适用，因为黑客不太可能知道用户名和密码，而需要使用暴力破解技术来确定用户的电子邮件地址。

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>步骤4：提高登录控件的无效凭据消息

当用户尝试使用无效凭据登录时，登录控件会显示一条消息，说明登录尝试失败。 具体而言，控件显示由其[`FailureText` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)指定的消息，该属性的默认值为登录尝试失败。 请稍后重试。

回忆一下，用户的凭据可能无效的原因有很多：

- 用户名可能不存在
- 用户名存在，但密码无效
- 用户名和密码有效，但用户尚未获得批准
- 用户名和密码有效，但用户被锁定（很可能是因为它们超过指定时间范围内的无效登录尝试次数）

使用自定义身份验证逻辑时，可能还有其他原因。 例如，在步骤3中编写的代码中，用户名和密码可能是有效的，但电子邮件地址可能不正确。

无论凭据为何无效，登录控件都将显示相同的错误消息。 如果用户的帐户尚未获得批准或已被锁定，则缺乏反馈可能会造成混淆。不过，有一点工作，我们可以让登录控件显示更适当的消息。

每当用户尝试使用无效凭据登录时，登录控件会引发其 `LoginError` 事件。 继续操作并为此事件创建事件处理程序，并添加以下代码：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

上述代码首先将登录控件的 `FailureText` 属性设置为默认值（登录尝试不成功。 请重试。 然后，它会检查提供的用户名是否映射到现有的用户帐户。 如果是这样，它将咨询生成的 `MembershipUser` 对象的 `IsLockedOut` 并 `IsApproved` 属性，以确定该帐户是否已锁定或尚未获得批准。 在任一情况下，`FailureText` 属性都将更新为相应的值。

若要测试此代码，有意尝试以现有用户身份登录，但使用的密码不正确。 请在10分钟时间范围内的行中执行此操作，该帐户将被锁定。如图11所示，后续登录尝试始终会失败（即使密码正确），但现在会显示更具描述性的信息，因为尝试无效的登录尝试次数过多。 请与管理员联系，让你的帐户解除锁定。

[![Tito 执行了太多无效的登录尝试并且已被锁定](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**图 11**： Tito 执行了过多无效的登录尝试并且已被锁定（[单击以查看完全大小的映像](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png)）

## <a name="summary"></a>总结

在本教程之前，我们的登录页根据用户名/密码对的硬编码列表验证了提供的凭据。 在本教程中，我们更新了页面，以根据成员身份框架验证凭据。 在步骤1中，我们查看了以编程方式使用 `Membership.ValidateUser` 方法。 在步骤2中，我们将手动创建的用户界面和代码替换为登录控件。

登录控件将呈现标准登录用户界面，并根据成员身份框架自动验证用户的凭据。 此外，在出现有效凭据时，登录控件会通过 forms 身份验证对用户进行签名。 简而言之，只需将登录控件拖到页面上，无需额外的声明性标记或代码，即可获得功能齐全的登录用户体验。 而且，登录控件可高度自定义，允许对呈现的用户界面和身份验证逻辑进行精细的控制。

此时，我们的网站的访问者可以创建新的用户帐户并登录到站点，但我们仍需要根据经过身份验证的用户来限制对页面的访问。 目前，任何经过身份验证或匿名的用户都可以查看网站上的任何页面。 除了控制每个用户对网站页面的访问权限，我们可能会有某些页面的功能依赖于用户。 下一教程介绍了如何基于登录用户限制访问权限和页面内功能。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [显示要锁定的和未批准的用户的自定义消息](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [检查 ASP.NET 2.0 的成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何：创建 ASP.NET 登录页](https://msdn.microsoft.com/library/ms178331.aspx)
- [登录控件技术文档](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [使用登录控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Teresa Murphy 和 Michael Olivero。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](creating-user-accounts-cs.md)
> [下一页](user-based-authorization-cs.md)
