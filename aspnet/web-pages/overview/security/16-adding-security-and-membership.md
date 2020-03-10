---
uid: web-pages/overview/security/16-adding-security-and-membership
title: 将安全性和成员身份添加到 ASP.NET 网页（Razor）站点 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍了如何保护网站的安全，使某些页面仅供登录用户使用。 （你还将了解如何创建页 。
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 0be3e767a42939a3c343f6d4a730eb1d9a6b367c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509900"
---
# <a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>将安全性和成员身份添加到 ASP.NET 网页（Razor）站点

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何保护 ASP.NET 网页（Razor）网站，以便某些页面仅供登录的用户使用。 （你还将了解如何创建任何人都可以访问的页面。）
> 
> **你将学习的内容：** 
> 
> - 如何创建包含注册页和登录页的网站，以便在某些页面上，你可以将访问权限仅限制为成员。
> - 如何创建公共和仅限成员的页面。
> - 如何定义角色，这些角色是在你的站点上具有不同安全权限的组，以及如何将用户分配到角色。
> - 如何使用 CAPTCHA 阻止自动程序（bot）创建成员帐户。
>   
> 
> 下面是本文中介绍的 ASP.NET 功能：
> 
> - WebMatrix**入门网站**模板。
> - `WebSecurity` helper 和 `Roles` 类。
> - `ReCaptcha` 帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 3
> - ASP.NET Web 帮助程序库

你可以设置你的网站，以便用户可以登录到它&#8212; ，以便站点支持*成员资格*。 这可能会很多原因。 例如，你的站点可能具有仅可用于成员的页面。 在某些情况下，你可能需要用户登录才能向你发送反馈或留下评论。

即使你的网站支持成员身份，用户也不一定需要在使用网站上的某些页面之前登录。 未登录的用户称为*匿名用户*。

用户可以在你的网站上注册，然后可以登录到该网站。 网站要求提供用户名（电子邮件地址）和密码，以确认用户是否为其声明的身份。 登录和确认用户身份的这一过程称为*身份验证*。

可以采用不同的方式来设置安全性和成员身份：

- 如果使用的是 WebMatrix，一种简单的方法是基于**入门网站**模板创建新的站点。 此模板已配置为安全和成员身份，并且已具有注册页面、登录页等。

    模板创建的站点还提供一个选项，让用户使用 Facebook、Google 或 Twitter 等外部站点登录。
- 如果要将安全性添加到现有站点，或者不想使用**Starter site**模板，则可以创建自己的注册页面、登录页等。

本文重点介绍第一个选项 &mdash; 如何使用 "**入门网站**" 模板来添加安全性。 它还提供了一些有关如何实现您自己的安全性的基本信息，并提供了有关如何执行此操作的详细信息的链接。 此外，还提供了有关如何启用外部登录名的信息，这将在单独的文章中更详细地介绍。

## <a name="creating-website-security-using-the-starter-site-template"></a>使用 Starter Site 模板创建网站安全性

在 WebMatrix 中，可以使用 " **Starter Site** " 模板创建包含以下内容的网站：

- 用于存储成员的用户名和密码的数据库。
- 注册页面，用户可在其中注册。
- 登录和注销页。
- 密码恢复和重置页面。

下面的过程描述如何创建站点并对其进行配置。

1. 启动 WebMatrix，然后在 "**快速入门**" 页中，**从 "模板**" 中选择 "站点"。
2. 选择 "**入门网站**" 模板，然后单击 **"确定"** 。 WebMatrix 会创建一个新站点。
3. 在左窗格中，单击 "**文件**" 工作区选择器。
4. 在网站的根文件夹中，打开 *\_AppStart*文件，该文件是一个用于包含全局设置的特殊文件。 它包含一些使用 `//` 字符注释掉的语句：

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    这些语句将配置可用于发送电子邮件的 `WebMail` 帮助程序。 成员资格系统可以使用电子邮件在用户注册或要更改其密码时发送确认消息。 （例如，用户注册后，他们会收到一封电子邮件，其中包含一个链接，用户可单击该链接来完成注册过程。）

    发送电子邮件需要访问 SMTP 服务器，如向[ASP.NET 网页站点添加电子邮件](https://go.microsoft.com/fwlink/?LinkId=202899)中所述。 你将在本中心 *\_AppStart*文件中存储电子邮件设置，以便无需在每个可发送电子邮件的页面上重复编写电子邮件设置。 （你不需要配置 SMTP 设置来设置注册数据库; 仅当你想要从其电子邮件别名验证用户，并让用户重置忘记的密码时，才需要 SMTP 设置。）
5. 通过删除每个语句前面的 `//`，取消注释。

    如果你不想设置电子邮件确认，则可以跳过此步骤和下一步。 如果未设置 SMTP 值，则新帐户会立即可用，而无需确认电子邮件。
6. 在代码中修改以下电子邮件相关设置：

   - 将 `WebMail.SmtpServer` 设置为你有权访问的 SMTP 服务器的名称。
   - 将 `WebMail.EnableSsl` 设置为 `true`。 此设置通过加密来保护发送到 SMTP 服务器的凭据。
   - 将 `WebMail.UserName` 设置为 SMTP 服务器帐户的用户名。
   - 将 `WebMail.Password` 设置为 SMTP 服务器帐户的密码。
   - 将 `WebMail.From` 设置为你自己的电子邮件地址。 这是从其发送消息的电子邮件地址。

     > [!NOTE] 
     > 
     > **提示**有关这些属性的值的其他信息，请参阅在[为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkID=202906)中[配置电子邮件设置](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings)。
7. 保存并关闭 *\_AppStart*。
8. 在浏览器中运行*默认的. cshtml*页。

    ![安全-成员身份-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > 如果你看到一个错误，指出属性必须是 `ExtendedMembershipProvider`的实例，则该站点可能未配置为使用 ASP.NET 网页成员资格系统（SimpleMembership）。 如果宿主提供程序的服务器配置不同于本地服务器，则有时会出现这种情况。 若要解决此问题，请将以下元素添加到站点的*web.config*文件中：
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > 将此元素添加为 `<configuration>` 元素的子元素，并将其作为 `<system.web>` 元素的对等方。
9. 在页面的右上角，单击 "**注册**" 链接。 将显示 "*注册*" 页。
10. 输入用户名和密码，然后单击 "**注册**"。

    ![安全-成员身份-3](16-adding-security-and-membership/_static/image2.png)

    从**入门网站**模板创建网站时，将在站点的*应用\_Data*文件夹中创建名为 startersite.sdf 的数据库 *。* 注册过程中，用户信息会添加到数据库中。 如果设置 SMTP 值，会将一条消息发送到您使用的电子邮件地址，这样您就可以完成注册了。

    ![安全-成员身份-4](16-adding-security-and-membership/_static/image3.png)
11. 中转到你的电子邮件程序并找到邮件，其中包含你的确认代码和指向该站点的超链接。
12. 单击超链接以激活帐户。 确认超链接打开注册确认页面。

    ![安全-成员资格5](16-adding-security-and-membership/_static/image4.png)
13. 单击 "**登录**" 链接，然后使用注册的帐户登录。

      登录后，**登录名**和**注册**链接将替换为**注销**链接。 登录名显示为链接。 （链接可让你转到可在其中更改密码的页面。）

      ![安全-成员资格-6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 默认情况下，ASP.NET 网页会将凭据以明文形式发送到服务器（以用户可读的文本形式）。 生产站点应使用安全 HTTP （ https://，也称为*安全套接字层*或 SSL）来加密与服务器交换的敏感信息。 你可以通过将 `WebMail.EnableSsl=true` 设置为使用 SSL 来发送电子邮件，如前面的示例中所示。 有关 SSL 的详细信息，请参阅[保护 Web 通信：证书、SSL 和 https://](https://go.microsoft.com/fwlink/?LinkId=208660)。

## <a name="additional-membership-functionality-in-the-site"></a>站点中的其他成员资格功能

你的网站包含允许用户管理其帐户的其他功能。 用户可以执行以下操作：

- 更改其密码。 登录后，他们可以单击用户名（链接）。 这会将它们转到一个页面，用户可在其中创建新密码（*帐户/ChangePassword. cshtml*）。
- 恢复忘记的密码。 在登录页上，有一个链接（**您是否忘记了密码？** ），该链接将用户转到可在其中输入电子邮件地址的页面（*Account/ForgotPassword*）。 站点向他们发送一封电子邮件，其中包含一个链接，用户可单击该链接来设置新密码（*Account/PasswordReset*）。

你还可以让用户使用外部站点登录，如稍后所述。

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>创建成员专用页面

在此期间，任何人都可以浏览到网站中的任何页面。 但您可能希望拥有仅供已登录的用户（即，到成员）的页面。 ASP.NET 使你能够创建只能由登录的成员访问的页面。 通常，如果匿名用户试图访问仅成员页面，则会将其重定向到登录页。

在此过程中，你将创建一个文件夹，该文件夹将包含仅供登录用户使用的页面。

1. 在站点的根目录下，创建一个新文件夹。 （在功能区中，单击 "**新建**" 下面的箭头，然后选择 "**新建文件夹**"。）
2. 将新文件夹命名为 "*成员*"。
3. 在 "*成员*" 文件夹中，创建一个新页面，并将其命名为*MembersInformation*。
4. 将现有内容替换为以下代码和标记：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    此代码测试 `WebSecurity` 对象的 `IsAuthenticated` 属性，如果用户已登录，则返回 `true`。 如果用户未登录，则该代码会调用 `Response.Redirect` 将用户发送到*帐户*文件夹中的*登录名*页。

    重定向的 URL 包括一个 `returnUrl` 查询字符串值，该字符串值使用 `Request.Url.LocalPath` 设置当前页的路径。 如果在查询字符串中设置 `returnUrl` 值，如此（如果返回 URL 是本地路径），则登录页会在登录后将用户返回到此页。

    该代码还将 *\_SiteLayout*页设置为其布局页。 （有关布局页的详细信息，请参阅[在 ASP.NET 网页网站中创建一致布局](https://go.microsoft.com/fwlink/?LinkId=202891)。）
5. 运行站点。 如果仍处于登录状态，请单击页面顶部的 "**注销**" 按钮。
6. 在浏览器中，请求页 */Members/MembersInformation*。 例如，URL 可能如下所示：

    `http://localhost:38366/Members/MembersInformation`

    （端口号（38366）在 URL 中可能会有所不同。）

    你将重定向到 "*登录*" 页，因为你未登录。
7. 使用之前创建的帐户登录。 你将重定向回*MembersInformation*页面。 由于你已登录，这次你会看到页面内容。

若要保护对多个页面的访问，可以执行以下操作：

- 向每个页面添加安全检查。
- 在保存受保护页面的文件夹中创建 *\_PageStart*页面，并在其中添加安全检查。 *\_PageStart*页充当文件夹中所有页的一种全局页。 为[ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)，更详细地介绍了此方法。

## <a name="creating-security-for-groups-of-users-roles"></a>为用户组创建安全性（角色）

如果你的网站有很多成员，则在你让用户看到页面之前，单独检查每个用户的权限是不是有效的。 您可以改为创建单个成员所属的组或*角色*。 然后，可以根据角色检查权限。 在本部分中，你将创建一个 &quot;管理员&quot; 角色，然后创建一个可供用户（属于该角色的用户）访问的页面。

ASP.NET 成员资格系统设置为支持角色。 但是，与成员身份注册和登录名不同的是， **Starter Site**模板不包含可帮助您管理角色的页面。 （管理角色是一种管理任务，而不是用户任务。）但是，你可以直接在 WebMatrix 的成员资格数据库中添加组。

1. 在 WebMatrix 中，单击 "**数据库**" 工作区选择器。
2. 在左窗格中，打开 " *startersite.sdf* " 节点，打开 "**表**" 节点，然后双击 "*网页"\_"角色*" 表。

    ![安全-成员资格-7](16-adding-security-and-membership/_static/image6.png)
3. 添加名为 &quot;管理员&quot;的角色。 *RoleId*字段将自动填充。 （这是主键，已设置为 "标识" 字段，如在[ASP.NET 网页网站中使用数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893)中所述。）
4. 记下 " *RoleId* " 字段的值。 （如果这是你要定义的第一个角色，则为1。）

    ![安全-成员身份-8](16-adding-security-and-membership/_static/image7.png)
5. 关闭 "*网页\_角色*" 表。
6. 打开 " *UserProfile* " 表。
7. 记下表中一个或多个用户的*UserId*值，然后关闭该表。
8. 打开 *\_UserInRoles* "表中的" 网页 "，并在表中输入*UserID*和*RoleID*值。 例如，要将用户2置于 &quot;管理员&quot; 角色中，请输入以下值：

    ![安全-成员身份-9](16-adding-security-and-membership/_static/image8.png)
9. 关闭 *\_UsersInRoles* "表中的网页。

    定义角色后，可以配置一个可供处于该角色的用户访问的页面。
10. 在网站根文件夹中，创建一个名为*AdminError*的新页面，并将现有内容替换为以下代码。 如果用户不允许访问某个页面，此页面将为用户重定向到的页面。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. 在网站根文件夹中，创建一个名为*AdminOnly*的新页面，并将现有代码替换为以下代码：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    如果当前用户是指定角色（在这种情况下为 "管理员" 角色）的成员，则 `Roles.IsUserInRole` 方法返回 `true`。
12. 在浏览器中运行*默认的 cshtml* ，但不要登录。 （如果你已登录，请注销。）
13. 在浏览器的地址栏中，在 URL 中添加*AdminOnly* 。 （换言之，请求*AdminOnly*文件。）你将重定向到*AdminError*页面，因为你当前未以用户身份登录到 &quot;管理员&quot; 角色。
14. 返回到*默认的. cshtml* ，并以添加到 &quot;管理员&quot; 角色的用户身份登录。
15. 浏览到*AdminOnly*页。 此时会显示该页。

## <a name="preventing-automated-programs-from-joining-your-website"></a>阻止自动程序加入你的网站

登录页面不会阻止自动程序（有时称为*web 机器人*或*bot*）注册到你的网站。 此过程介绍如何为注册页启用 ReCaptcha 测试。

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. 在 ReCaptcha.Net （[http://recaptcha.net](http://recaptcha.net)）注册你的网站。 完成注册后，你将获得一个公钥和一个私钥。
2. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
3. 在*帐户*文件夹中，打开名为 " *Register*" 的文件。
4. 在页面顶部的代码中，查找以下行，并通过删除 `//` 注释字符来取消注释：

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. 将 `PRIVATE_KEY` 替换为你自己的 ReCaptcha 私钥。
6. 在页面标记中，删除页面标记中来自以下行的 `@*` 和 `*@` 注释字符：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. 将 `PUBLIC_KEY` 替换为你的密钥。
8. 如果尚未将其删除，请删除 `<div>` 元素，该元素包含以 "enable CAPTCHA 验证 ..." 开头的文本。 （删除整个 `<div>` 元素及其内容。）

9. 在浏览器中运行*默认值。* 如果你登录到站点，请单击 "**注销**" 链接。
10. 单击 "**注册**" 链接并使用 CAPTCHA 测试测试注册。

     ![安全-成员资格-10](16-adding-security-and-membership/_static/image9.png)

有关 `ReCaptcha` 帮助器的详细信息，请参阅[使用 CATPCHA 阻止自动程序（bot）使用 ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251967)网站。

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>允许用户使用外部站点登录

**入门网站**模板包含允许用户使用 Facebook、Windows Live、Twitter、Google 或 Yahoo 登录的代码和标记。 默认情况下，不启用此功能。 允许用户使用这些外部提供程序登录的一般过程如下所示：

- 确定要支持的外部站点。
- 如果需要，请前往该站点并设置一个登录应用。 （例如，必须执行此操作才能允许 Facebook 登录。）
- 在站点中配置提供程序。 在大多数情况下，只需取消注释 *\_AppStart*文件中的某些代码。
- 将标记添加到注册页面，使用户可以链接到外部站点以进行登录。 通常，你可以复制所需的标记并稍微更改文本。

可以在[从 ASP.NET 网页站点中的外部站点启用登录](https://go.microsoft.com/fwlink/?LinkId=251969)主题中找到分步说明。

用户从其他站点登录后，该用户将返回到你的网站，并将该登录名与你的网站*相关联*。 实际上，这会在你的站点中为用户的外部登录名创建成员资格条目。 这使你可以将成员身份（如角色）的普通功能与外部登录一起使用。

## <a name="adding-security-to-an-existing-website"></a>将安全性添加到现有网站

本文前面的过程依赖于使用**入门站点**模板作为网站安全的基础。 如果从**Starter site**模板开始，或从基于该模板的站点复制相关页面并不可行，则可以通过自己的方式对其进行编码来在自己的站点中实现相同类型的安全。 创建相同类型的页（注册、登录等），然后使用帮助器和类设置成员资格。

博客文章中介绍了[实现 ASP.NET Razor 安全性的最基本方法](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)。 大部分工作都是使用 `WebSecurity` 帮助器的以下方法和属性完成的：

- [WebSecurty. UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx)， [WebSecurity. CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx)。 通过这些方法，您可以确定是否已注册了某个人并注册了。
- [WebSecurty. IsAuthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx)。 此属性可让你确定当前用户是否已登录。 如果用户尚未登录，这会将用户重定向到登录页。
- [WebSecurity](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx)， [WebSecurity](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx)。 这些方法将用户登录或注销。
- [WebSecurity. CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx)。 此属性用于显示当前用户的登录名（如果用户已登录）。
- [WebSecurity. ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx)。 如果设置了用于注册的电子邮件确认，此方法非常有用。 （有关详细信息，请参阅博客文章[使用确认功能 ASP.NET 网页安全](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)。）

若要管理角色，可以使用[角色](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx)和[成员身份](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx)类，如博客项中所述。

## <a name="additional-resources"></a>其他资源

- [自定义站点范围内的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [保护 Web 通信：证书、SSL 和 https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [实现 ASP.NET Razor 安全性](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)并[使用确认功能 ASP.NET 网页安全](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)的最基本方法。 这些博客文章介绍了如何实现 ASP.NET 成员资格功能，而无需使用**入门网站**模板。
- [在 ASP.NET 网站中启用从外部站点进行登录](https://go.microsoft.com/fwlink/?LinkId=251969)
- [WebSecurity 类 API 参考](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99))（MSDN）
- [SimpleRoleProvider 类 API 参考](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99))（MSDN）
- [SimpleMembershipProvider 类 API 参考](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99))（MSDN）
