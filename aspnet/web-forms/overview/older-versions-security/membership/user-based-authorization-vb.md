---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-vb
title: 基于用户的授权（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将探讨如何通过多种方法来限制对页面的访问和限制页面级功能。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: bc937e9d-5c14-4fc4-aec7-440da924dd18
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: dfac0c6fa955e59c6ea996533f2447e89ec8d468
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587973"
---
# <a name="user-based-authorization-vb"></a>基于用户的身份验证 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_VB.zip)或[下载 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_vb.pdf)

> 在本教程中，我们将探讨如何通过多种方法来限制对页面的访问和限制页面级功能。

## <a name="introduction"></a>简介

大多数提供用户帐户的 web 应用程序都在部分中执行操作，以限制某些访问者访问站点内的某些页面。 例如，在大多数在线 messageboard 网站中，所有用户（匿名和身份验证）都能够查看 messageboard 的文章，但只有经过身份验证的用户可以访问网页来创建新帖子。 可能有一些只有特定用户（或一组特定用户）可以访问的管理页面。 而且，页级别功能可能会因用户而异。 查看文章列表时，经过身份验证的用户会显示一个用于分级每个帖子的界面，而此界面对匿名访问者不可用。

ASP.NET 可以轻松定义基于用户的授权规则。 在 `Web.config`中，只需一些标记，就可以锁定特定网页或整个目录，以便只能访问指定的用户子集。 可以基于当前登录的用户通过编程方式或声明性方式打开或关闭页面级功能。

在本教程中，我们将探讨如何通过多种方法来限制对页面的访问和限制页面级功能。 让我们进入正题！

## <a name="a-look-at-the-url-authorization-workflow"></a>查看 URL 授权工作流

如[*表单身份验证概述*](../introduction/an-overview-of-forms-authentication-vb.md)教程中所述，当 ASP.NET 运行时处理 ASP.NET 资源的请求时，请求会在其生命周期内引发许多事件。 *HTTP 模块*是托管类，其代码是为了响应请求生命周期中的特定事件而执行的。 ASP.NET 附带了多个 HTTP 模块，这些模块在幕后执行基本任务。

[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)一个这样的 HTTP 模块。 如前面的教程中所述，`FormsAuthenticationModule` 的主要功能是确定当前请求的标识。 这可以通过检查 forms 身份验证票证来完成，该票证可以位于 cookie 中或嵌入在 URL 中。 此标识发生在[`AuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)期间。

另一个重要的 HTTP 模块是[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)，这是为了响应[`AuthorizeRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)（在 `AuthenticateRequest` 事件之后发生）。 `UrlAuthorizationModule` 检查 `Web.config` 中的配置标记，以确定当前标识是否有权访问指定的页。 此过程称为*URL 授权*。

我们将在步骤1中检查 URL 授权规则的语法，但首先我们来看看 `UrlAuthorizationModule` 的作用，具体取决于请求是否已获授权。 如果 `UrlAuthorizationModule` 确定请求已获得授权，则不执行任何操作，请求会在其生命周期中继续执行。 但是，如果请求*未*获授权，则 `UrlAuthorizationModule` 中止生命周期，并指示 `Response` 对象返回 " [HTTP 401" 未经授权](http://www.checkupdown.com/status/E401.html)状态。 使用窗体身份验证时，此 HTTP 401 状态绝不会返回给客户端，因为如果 `FormsAuthenticationModule` 检测到 HTTP 401 状态，则会将其修改为[http 302 重定向](http://www.checkupdown.com/status/E302.html)到登录页。

图1说明了 ASP.NET 管道、`FormsAuthenticationModule`的工作流，以及未授权请求到达时的 `UrlAuthorizationModule`。 具体而言，图1显示了 `ProtectedPage.aspx`的匿名访问者发出的请求，该请求是拒绝匿名用户访问的页面。 由于访问者是匿名的，`UrlAuthorizationModule` 中止请求并返回 HTTP 401 未经授权状态。 然后，`FormsAuthenticationModule` 将401状态转换为302重定向到登录页。 通过登录页对用户进行身份验证后，会将其重定向到 `ProtectedPage.aspx`。 这次 `FormsAuthenticationModule` 会根据用户的身份验证票证来确定用户身份。 现在，访问者已经过身份验证，`UrlAuthorizationModule` 允许访问该页面。

[![Forms 身份验证和 URL 授权工作流](user-based-authorization-vb/_static/image2.png)](user-based-authorization-vb/_static/image1.png)

**图 1**： Forms 身份验证和 URL 授权工作流（[单击以查看完全大小的图像](user-based-authorization-vb/_static/image3.png)）

图1描述了匿名访问者尝试访问匿名用户无法使用的资源时所发生的交互。 在这种情况下，匿名访问者将重定向到登录页，其中包含她尝试访问 querystring 中指定的页。 用户成功登录后，她将自动重定向回最初尝试查看的资源。

如果匿名用户发出了未经授权的请求，则此工作流非常简单，访问者可以轻松了解发生的情况和原因。 但请记住，`FormsAuthenticationModule` 会将*任何*未经授权的用户重定向到登录页，即使请求由经过身份验证的用户发出。 如果经过身份验证的用户尝试访问她缺少授权的页面，这可能会导致用户体验混乱。

假设我们的网站已配置了其 URL 授权规则，以便 ASP.NET 页面 `OnlyTito.aspx` 仅 accessibly 为 Tito。 现在，假设 Sam 访问该站点，登录，然后尝试访问 `OnlyTito.aspx`。 `UrlAuthorizationModule` 将暂停请求生命周期，并返回 HTTP 401 "未经授权" 状态，`FormsAuthenticationModule` 该状态将检测并将 Sam 重定向到登录页。 尽管 Sam 已登录，但她可能会想知道为什么会将她发回登录页。 她可能会因为某种原因而丢失了她的登录凭据，或输入了无效的凭据。 如果 Sam 从登录页重新输入她的凭据，她将再次登录（再次）并重定向到 `OnlyTito.aspx`。 `UrlAuthorizationModule` 将检测 Sam 是否无法访问此页，她将返回到登录页。

图2演示了这种混乱的工作流。

[![默认工作流可能导致混乱的循环](user-based-authorization-vb/_static/image5.png)](user-based-authorization-vb/_static/image4.png)

**图 2**：默认工作流可能会产生混乱的循环（[单击查看完全大小的图像](user-based-authorization-vb/_static/image6.png)）

图2中所示的工作流可以快速 befuddle，甚至是最精通计算机的访问者。 在步骤2中，我们将探讨防止这种混乱循环的方法。

> [!NOTE]
> ASP.NET 使用两种机制来确定当前用户是否可以访问特定网页： URL 授权和文件授权。 文件授权由[`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)实现，它通过咨询请求的文件 acl 来确定权威。 文件授权最常用于 Windows 身份验证，因为 Acl 是适用于 Windows 帐户的权限。 使用 forms 身份验证时，所有操作系统和文件系统级请求均由同一 Windows 帐户执行，而不考虑访问站点的用户。 由于本教程系列重点介绍 forms 身份验证，因此我们不会讨论文件授权。

### <a name="the-scope-of-url-authorization"></a>URL 授权的范围

`UrlAuthorizationModule` 是托管代码，是 ASP.NET 运行时的一部分。 在 Microsoft [Internet Information Services （iis）](https://www.iis.net/) web 服务器版本7之前，IIS 的 HTTP 管道与 ASP.NET 运行时的管道之间存在不同的障碍。 简而言之，在 IIS 6 及更早版本中，ASP。仅当请求从 IIS 委托到 ASP.NET 运行时时，才会执行网络的 `UrlAuthorizationModule`。 默认情况下，IIS 会处理静态内容本身（如 HTML 页面和 CSS、JavaScript 和映像文件），并仅在请求扩展名为 `.aspx`、`.asmx`或 `.ashx` 的页面时，将请求发送到 ASP.NET 运行时。

但是，IIS 7 允许集成的 IIS 和 ASP.NET 管道。 使用几个配置设置，你可以设置 IIS 7 来为*所有*请求调用 `UrlAuthorizationModule`，这意味着可以为任何类型的文件定义 URL 授权规则。 此外，IIS 7 包含自己的 URL 授权引擎。 有关 ASP.NET 集成和 IIS 7 的本机 URL 授权功能的详细信息，请参阅[了解 IIS7 Url 授权](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)。 若要深入了解 ASP.NET 和 IIS 7 集成，请选择 Shahram Khosravi 书籍、*专业 IIS 7 和 ASP.NET 集成编程*（ISBN：978-0470152539）的副本。

简而言之，在 IIS 7 之前的版本中，URL 授权规则仅适用于 ASP.NET 运行时所处理的资源。 但使用 IIS 7，可以使用 IIS 的本机 URL 授权功能或集成 ASP。将网络 `UrlAuthorizationModule` 到 IIS 的 HTTP 管道，从而将此功能扩展到所有请求。

> [!NOTE]
> ASP 的方式有一些细微的差异。NET 的 `UrlAuthorizationModule` 和 IIS 7 的 URL 授权功能处理授权规则。 本教程不会检查 IIS 7 的 URL 授权功能，也不会检查如何对与 `UrlAuthorizationModule`进行的授权规则进行分析。 有关这些主题的详细信息，请参阅 MSDN 上或[www.iis.net](https://www.iis.net/)上的 IIS 7 文档。

## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>步骤1：在`Web.config` 中定义 URL 授权规则

`UrlAuthorizationModule` 根据应用程序配置中定义的 URL 授权规则，确定是授予还是拒绝特定标识的请求资源的访问权限。 授权规则在[`<authorization>` 元素](https://msdn.microsoft.com/library/8d82143t.aspx)中以 `<allow>` 和 `<deny>` 子元素的形式进行拼写。 每个 `<allow>` 和 `<deny>` 子元素可以指定：

- 特定用户
- 以逗号分隔的用户列表
- 所有匿名用户，由问号（？）表示
- 所有用户，由星号（\*）表示

以下标记说明了如何使用 URL 授权规则允许用户 Tito 和 Scott，并拒绝所有其他用户：

[!code-xml[Main](user-based-authorization-vb/samples/sample1.xml)]

`<allow>` 元素定义了允许的用户-Tito 和 Scott-但 `<deny>` 元素会指示*所有*用户被拒绝。

> [!NOTE]
> `<allow>` 和 `<deny>` 元素还可以指定角色的授权规则。 我们将在将来的教程中检查基于角色的授权。

以下设置授予 Sam 以外的任何人的访问权限：

[!code-xml[Main](user-based-authorization-vb/samples/sample2.xml)]

若要仅允许经过身份验证的用户，请使用以下配置，这将拒绝对所有匿名用户的访问：

[!code-xml[Main](user-based-authorization-vb/samples/sample3.xml)]

授权规则在 `Web.config` 中的 `<system.web>` 元素内定义，并应用于 web 应用程序中的所有 ASP.NET 资源。 通常，应用程序的不同部分具有不同的授权规则。 例如，在电子商务网站上，所有访问者都可能细读产品，请参阅产品评论，搜索目录，等等。 但是，只有经过身份验证的用户可以访问结帐或页面来管理一个发货历史记录。 而且，只能通过选择用户（如站点管理员）访问站点的某些部分。

ASP.NET 使为站点中的不同文件和文件夹定义不同的授权规则变得简单。 根文件夹的 `Web.config` 文件中指定的授权规则适用于站点中的所有 ASP.NET 资源。 但是，可以通过使用 `<authorization>` 部分添加 `Web.config` 来覆盖特定文件夹的默认授权设置。

让我们更新网站，以便只有经过身份验证的用户可以访问 `Membership` 文件夹中的 ASP.NET 页。 若要实现此目的，我们需要将 `Web.config` 文件添加到 `Membership` 文件夹中，并将其授权设置设置为 "拒绝匿名用户"。 右键单击解决方案资源管理器中的 "`Membership`" 文件夹，从上下文菜单中选择 "添加新项" 菜单，然后添加名为 "`Web.config`" 的新 Web 配置文件。

[![将 Web.config 文件添加到成员资格文件夹](user-based-authorization-vb/_static/image8.png)](user-based-authorization-vb/_static/image7.png)

**图 3**：将 `Web.config` 文件添加到 `Membership` 文件夹（[单击查看完全大小的图像](user-based-authorization-vb/_static/image9.png)）

此时，你的项目应包含两个 `Web.config` 文件：一个位于根目录中，另一个位于 `Membership` 文件夹中。

[![应用程序现在应包含两个 web.config 文件](user-based-authorization-vb/_static/image11.png)](user-based-authorization-vb/_static/image10.png)

**图 4**：应用程序现在应包含两个 `Web.config` 文件（[单击以查看完全大小的图像](user-based-authorization-vb/_static/image12.png)）

更新 `Membership` 文件夹中的配置文件，使其禁止匿名用户访问。

[!code-xml[Main](user-based-authorization-vb/samples/sample4.xml)]

就这么简单！

若要测试此更改，请在浏览器中访问主页，并确保已注销。由于 ASP.NET 应用程序的默认行为是允许所有访问者，而且由于未对根目录的 `Web.config` 文件进行任何授权修改，因此，我们能够以匿名访问者身份访问根目录中的文件。

单击左栏中的 "创建用户帐户" 链接。 这会转到 `~/Membership/CreatingUserAccounts.aspx`。 由于 `Membership` 文件夹中的 `Web.config` 文件定义了禁止匿名访问的授权规则，`UrlAuthorizationModule` 中止请求并返回 HTTP 401 未经授权状态。 `FormsAuthenticationModule` 将其修改为302重定向状态，并将我们发送到登录页。 请注意，我们尝试访问的页（`CreatingUserAccounts.aspx`）通过 `ReturnUrl` querystring 参数传递到登录页。

[![因为 URL 授权规则禁止匿名访问，所以我们将重定向到登录页](user-based-authorization-vb/_static/image14.png)](user-based-authorization-vb/_static/image13.png)

**图 5**：由于 URL 授权规则禁止匿名访问，我们将重定向到登录页（[单击以查看完全大小的映像](user-based-authorization-vb/_static/image15.png)）

成功登录后，会重定向到 "`CreatingUserAccounts.aspx`" 页面。 这次 `UrlAuthorizationModule` 允许访问页面，因为我们不再是匿名的。

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>将 URL 授权规则应用于特定位置

`Web.config` 的 `<system.web>` 部分中定义的授权设置适用于该目录及其子目录中的所有 ASP.NET 资源（除非另一个 `Web.config` 文件重写）。 然而，在某些情况下，我们可能希望给定目录中的所有 ASP.NET 资源具有特定的授权配置，但只有一个或两个特定页面。 这可以通过将 `<location>` 元素添加到 `Web.config`中来实现，将其指向授权规则不同的文件，并在其中定义其唯一的授权规则。

为了说明如何使用 `<location>` 元素覆盖特定资源的配置设置，我们自定义授权设置，以便只有 Tito 可以访问 `CreatingUserAccounts.aspx`。 若要实现此目的，请将 `<location>` 元素添加到 `Membership` 文件夹的 `Web.config` 文件，并更新其标记，使其类似于以下内容：

[!code-xml[Main](user-based-authorization-vb/samples/sample5.xml)]

`<system.web>` 中的 `<authorization>` 元素定义了 `Membership` 文件夹及其子文件夹中 ASP.NET 资源的默认 URL 授权规则。 `<location>` 元素允许我们覆盖特定资源的这些规则。 在上述标记中，`<location>` 元素引用 `CreatingUserAccounts.aspx` 页，并指定它的授权规则，例如允许 Tito，但拒绝其他所有人。

若要测试此授权更改，请先以匿名用户身份访问该网站。 如果你尝试访问 `Membership` 文件夹中的任何页面（如 `UserBasedAuthorization.aspx`），`UrlAuthorizationModule` 将拒绝该请求，你会被重定向到登录页。 以 "Scott" 的身份登录后，可以访问 `Membership` 文件夹中*除 `CreatingUserAccounts.aspx`之外*的任何页面。 尝试访问 `CreatingUserAccounts.aspx` 作为任何人（但 Tito 登录）将导致未经授权的访问尝试，并将你重定向回登录页。

> [!NOTE]
> `<location>` 元素必须出现在配置的 `<system.web>` 元素之外。 需要为要重写其授权设置的每个资源使用单独的 `<location>` 元素。

### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>介绍`UrlAuthorizationModule`如何使用授权规则来授予或拒绝访问权限

`UrlAuthorizationModule` 通过一次分析 URL 授权规则（从第一个标识符开始并向下工作），确定是否为特定 URL 授权特定标识。 一旦找到匹配项，就会向用户授予或拒绝访问权限，具体取决于是否在 `<allow>` 或 `<deny>` 元素中找到了匹配项。 <strong>如果未找到匹配项，则会向用户授予访问权限。</strong> 因此，如果要限制访问，则必须使用 `<deny>` 元素作为 URL 授权配置中的最后一个元素。 <strong>如果省略</strong><strong>`<deny>`</strong><strong>元素，则会向所有用户授予访问权限。</strong>

为了更好地了解 `UrlAuthorizationModule` 用来确定机构的过程，请考虑我们在此步骤中前面讨论的示例 URL 授权规则。 第一个规则是允许访问 Tito 和 Scott 的 `<allow>` 元素。 第二个规则是拒绝所有人的访问的 `<deny>` 元素。 如果匿名用户访问，`UrlAuthorizationModule` 会询问，匿名是 Scott 还是 Tito？ 当然，答案是不是的，因此它会前进到第二个规则。 每个人集中都是匿名的吗？ 由于此处的答案是肯定的，`<deny>` 规则已生效，访问者将重定向到登录页。 同样，如果 Jisun 正在访问，则 `UrlAuthorizationModule` 首先会询问，是 Jisun 还是 Tito？ 由于她不是，`UrlAuthorizationModule` 继续第二个问题，每个人都在 Jisun？ 她是，我们也被拒绝访问。 最后，如果 Tito 访问，`UrlAuthorizationModule` 提出的第一个问题是赞成答案，因此 Tito 被授予访问权限。

由于 `UrlAuthorizationModule` 处理从上到下的授权规则，在任何匹配时停止，因此，在不太具体的规则之前有更具体的规则是非常重要的。 也就是说，若要定义禁止 Jisun 和匿名用户的授权规则，但允许所有其他经过身份验证的用户，请从最具体的规则开始，其中一个规则会影响 Jisun，然后继续执行不太具体的规则-这些规则允许所有其他操作经过身份验证的用户，但拒绝所有匿名用户。 以下 URL 授权规则通过首先拒绝 Jisun 并拒绝任何匿名用户来实现此策略。 除 Jisun 以外的任何经过身份验证的用户都将被授予访问权限，因为 `<deny>` 这两个语句都不匹配。

[!code-xml[Main](user-based-authorization-vb/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>步骤2：针对未经授权的经过身份验证的用户修复工作流

正如我们在本教程前面的 "查看 URL 授权工作流" 一节中讨论的那样，无论何时，如果未经授权的请求发生，`UrlAuthorizationModule` 都将中止请求并返回 HTTP 401 未经授权状态。 此401状态由 `FormsAuthenticationModule` 修改为将用户发送到登录页的302重定向状态。 此工作流在任何未经授权的请求上发生，即使用户已进行身份验证。

将经过身份验证的用户返回到登录页可能会将它们混淆，因为它们已经登录系统。 使用少许工作，我们可以通过将发出未经授权的请求的经过身份验证的用户重定向到说明他们尝试访问受限页面的页面，来改进此工作流。

首先，在 web 应用程序的根文件夹中创建一个名为 `UnauthorizedAccess.aspx`的新 "ASP.NET" 页;请不要忘记将此页面与 `Site.master` 母版页关联。 创建此页后，删除引用 `LoginContent` ContentPlaceHolder 的内容控件，以便显示母版页的默认内容。 接下来，添加一条说明该情况的消息，即用户尝试访问受保护的资源。 添加此类消息后，`UnauthorizedAccess.aspx` 页的声明性标记应如下所示：

[!code-aspx[Main](user-based-authorization-vb/samples/sample7.aspx)]

现在，我们需要更改工作流，以便在经过身份验证的用户执行未经授权的请求时，会将其发送到 `UnauthorizedAccess.aspx` 页，而不是登录页。 将未经授权的请求重定向到登录页的逻辑隐藏在 `FormsAuthenticationModule` 类的私有方法中，因此我们无法自定义此行为。 然而，我们可以执行的操作是将自己的逻辑添加到登录页，以便在需要时将用户重定向到 `UnauthorizedAccess.aspx`。

当 `FormsAuthenticationModule` 将未经授权的访问者重定向到登录页时，它会将请求的未经授权 URL 附加到名为 `ReturnUrl`的 querystring。 例如，如果未经授权的用户尝试访问 `OnlyTito.aspx`，则 `FormsAuthenticationModule` 会将它们重定向到 `Login.aspx?ReturnUrl=OnlyTito.aspx`。 因此，如果使用包含 `ReturnUrl` 参数的查询字符串的已验证用户访问登录页，则我们知道此未经身份验证的用户刚刚试图访问她无权查看的页。 在这种情况下，我们希望将她重定向到 `UnauthorizedAccess.aspx`。

若要实现此目的，请将以下代码添加到登录页的 `Page_Load` 事件处理程序中：

[!code-vb[Main](user-based-authorization-vb/samples/sample8.vb)]

上述代码将经过身份验证的未经授权用户重定向到 `UnauthorizedAccess.aspx` 页。 若要查看此逻辑操作，请访问站点作为匿名访问者，并单击左栏中的 "创建用户帐户" 链接。 这会转到 "`~/Membership/CreatingUserAccounts.aspx`" 页面，该页面在步骤1中配置为仅允许访问 Tito。 由于禁止匿名用户，`FormsAuthenticationModule` 会将我们重定向回登录页。

此时，我们是匿名的，因此 `Request.IsAuthenticated` 返回 `False`，并且我们不会重定向到 `UnauthorizedAccess.aspx`。 相反，将显示登录页。 以除 Tito 以外的用户身份登录，如 Bruce。 输入相应凭据后，登录页将重新定向到 `~/Membership/CreatingUserAccounts.aspx`。 但是，由于只有 Tito 可以访问此页，因此我们无权查看它并立即返回到登录页。 但是，这一次 `Request.IsAuthenticated` 返回 `True` （并且 `ReturnUrl` querystring 参数存在），因此我们将重定向到 `UnauthorizedAccess.aspx` 页。

[![经过身份验证，未授权的用户会重定向到 UnauthorizedAccess](user-based-authorization-vb/_static/image17.png)](user-based-authorization-vb/_static/image16.png)

**图 6**：经过身份验证的未经授权的用户将重定向到 `UnauthorizedAccess.aspx` （[单击查看完全大小的图像](user-based-authorization-vb/_static/image18.png)）

此自定义工作流提供了一个更为明智的、更简单的用户体验，方法是将图2中所示的周期短路。

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>步骤3：基于当前登录的用户限制功能

通过 URL 授权，可轻松指定粗授权规则。 如我们在步骤1中所述，使用 URL 授权，我们可以简洁地说明允许哪些标识，哪些标识被拒绝查看某个文件夹中的特定页面或所有页面。 但是，在某些情况下，我们可能希望允许所有用户访问某个页面，但会根据访问该页面的用户限制其功能。

请考虑电子商务网站的情况，该网站允许经过身份验证的访问者查看其产品。 匿名用户访问产品页时，他们将只看到产品信息，而不会有机会进行评审。 但是，访问同一页面的经过身份验证的用户将看到查看界面。 如果经过身份验证的用户尚未查看此产品，则该界面会使他们提交审核;否则，会向他们显示先前提交的评审。 为了使此方案更进一步，"产品" 页可能会显示其他信息并为那些适用于电子商务公司的用户提供扩展功能。 例如，"产品" 页可能会列出库存库存，并包括在由员工访问时用于编辑产品价格和说明的选项。

可以通过声明方式或编程方式（或通过这两种方式的某个组合）来实现此类精细授权规则。 在下一部分中，我们将了解如何通过登录视图控件实现精细的授权。 接下来，我们将探讨编程技术。 但在查看应用精细授权规则之前，首先需要创建一个页面，该页面的功能依赖于用户访问它。

让我们创建一个页面，其中列出了 GridView 中特定目录中的文件。 除了列出每个文件的名称、大小和其他信息外，GridView 还将包括两个 LinkButtons 列：一个标题为 "视图"，一个标题为 "删除"。 如果单击视图 LinkButton，将显示所选文件的内容;如果单击删除 LinkButton，则该文件将被删除。 首先，创建此页面，使其 "查看" 和 "删除" 功能可供所有用户使用。 在中，使用登录视图控件和以编程方式限制功能部分，我们将了解如何根据访问页面的用户启用或禁用这些功能。

> [!NOTE]
> 我们即将生成的 ASP.NET 页使用 GridView 控件显示文件列表。 由于本教程系列重点介绍 forms 身份验证、授权、用户帐户和角色，我不希望花太多时间讨论 GridView 控件的内部工作原理。 虽然本教程提供了有关设置此页面的具体分步说明，但它并不深入探讨某些选择的原因，或特定属性对呈现的输出的影响。 若要全面检查 GridView 控件，请参阅 *[ASP.NET 2.0 教程系列中的使用数据](../../data-access/index.md)* 。

首先打开 `Membership` 文件夹中的 `UserBasedAuthorization.aspx` 文件，然后将 GridView 控件添加到名为 `FilesGrid`的页面。 从 GridView 的智能标记中，单击 "编辑列" 链接以启动 "字段" 对话框。 在此处，取消选中左下角的 "自动生成字段" 复选框。 接下来，从左上角添加 "选择" 按钮、"删除" 按钮和两个 BoundFields （"选择" 和 "删除" 按钮可在 CommandField 类型下找到）。 将 "选择" 按钮的 `SelectText` 属性设置为 "查看"，并将第一个 BoundField 的 `HeaderText` 和 `DataField` 属性设置为 "名称"。 将第二个 BoundField 的 `HeaderText` 属性设置为大小（以字节为单位），将其 `DataField` 属性设置为 Length，将其 `DataFormatString` `HtmlEncode` {0:N0} 属性设置为 "False"。

配置 GridView 列后，单击 "确定" 以关闭 "字段" 对话框。 在属性窗口中，将 GridView 的 `DataKeyNames` 属性设置为 "`FullName`"。 此时，GridView 的声明性标记应如下所示：

[!code-aspx[Main](user-based-authorization-vb/samples/sample9.aspx)]

创建 GridView 标记后，就可以编写代码来检索特定目录中的文件，并将它们绑定到 GridView。 将以下代码添加到页面的 `Page_Load` 事件处理程序中：

[!code-vb[Main](user-based-authorization-vb/samples/sample10.vb)]

上面的代码使用[`DirectoryInfo` 类](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx)获取应用程序根文件夹中的文件列表。 [`GetFiles()` 方法](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx)将目录中的所有文件作为[`FileInfo` 对象](https://msdn.microsoft.com/library/system.io.fileinfo.aspx)的数组返回，然后将其绑定到 GridView。 `FileInfo` 对象具有多个属性，如 `Name`、`Length`和 `IsReadOnly`，等等。 从其声明性标记中可以看到，GridView 只显示 `Name` 和 `Length` 属性。

> [!NOTE]
> `DirectoryInfo` 和 `FileInfo` 类在[`System.IO` 命名空间](https://msdn.microsoft.com/library/system.io.aspx)中找到。 因此，您需要将这些类名称作为命名空间名称的开头，或者将命名空间导入类文件（通过 `Imports System.IO`）。

请花点时间通过浏览器访问此页。 它将显示驻留在应用程序的根目录中的文件的列表。 单击任意视图或删除 LinkButtons 将导致回发，但不会执行任何操作，因为我们尚未创建必要的事件处理程序。

[![GridView 列出 Web 应用程序的根目录中的文件](user-based-authorization-vb/_static/image20.png)](user-based-authorization-vb/_static/image19.png)

**图 7**： GridView 列出了 Web 应用程序的根目录中的文件（[单击以查看完全大小的映像](user-based-authorization-vb/_static/image21.png)）

我们需要一种方法来显示所选文件的内容。 返回到 Visual Studio，并将名为 `FileContents` 的文本框添加到 GridView 之上。 将其 `TextMode` 属性设置为 `MultiLine` 及其 `Columns`，并将 `Rows` 属性分别设置为95% 和10。

[!code-aspx[Main](user-based-authorization-vb/samples/sample11.aspx)]

接下来，为 GridView 的[`SelectedIndexChanged` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx)创建事件处理程序并添加以下代码：

[!code-vb[Main](user-based-authorization-vb/samples/sample12.vb)]

此代码使用 GridView 的 `SelectedValue` 属性来确定所选文件的完整文件名。 在内部，引用 `DataKeys` 集合以获取 `SelectedValue`，因此，必须将 GridView 的 `DataKeyNames` 属性设置为 Name，如此步骤中前面所述。 [`File` 类](https://msdn.microsoft.com/library/system.io.file.aspx)用于将所选文件的内容读入字符串中，然后将其分配给 `FileContents` 文本框的 `Text` 属性，从而在页面上显示所选文件的内容。

[![在文本框中显示所选文件的内容](user-based-authorization-vb/_static/image23.png)](user-based-authorization-vb/_static/image22.png)

**图 8**：在文本框中显示所选文件的内容（[单击以查看完全尺寸的图像](user-based-authorization-vb/_static/image24.png)）

> [!NOTE]
> 如果查看包含 HTML 标记的文件的内容，然后尝试查看或删除文件，则将收到 `HttpRequestValidationException` 错误。 出现这种情况的原因是，在回发时，文本框的内容将发送回 web 服务器。 默认情况下，只要检测到潜在的危险回发内容（如 HTML 标记），ASP.NET 就会引发 `HttpRequestValidationException` 错误。 若要禁用此错误，请通过将 `ValidateRequest="false"` 添加到 `@Page` 指令来关闭对该页的请求验证。 有关请求验证的优点以及禁用它时应采取的措施的详细信息，请阅读[请求验证-阻止脚本攻击](https://asp.net/learn/whitepapers/request-validation/)。

最后，使用以下代码为 GridView 的[`RowDeleting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)添加事件处理程序：

[!code-vb[Main](user-based-authorization-vb/samples/sample13.vb)]

该代码只是在 "`FileContents`" 文本框中显示要删除的文件的完整名称，*而无需*实际删除该文件。

[单击 "删除" 按钮 ![实际上不会删除该文件](user-based-authorization-vb/_static/image26.png)](user-based-authorization-vb/_static/image25.png)

**图 9**：单击 "删除" 按钮并不会实际删除该文件（[单击查看完全尺寸的图像](user-based-authorization-vb/_static/image27.png)）

在步骤1中，我们配置了 URL 授权规则，禁止匿名用户查看 `Membership` 文件夹中的页面。 为了更好地展示精细的身份验证，让匿名用户可以访问 `UserBasedAuthorization.aspx` 页面，但功能有限。 若要打开此页面，使其可供所有用户访问，请将以下 `<location>` 元素添加到 `Membership` 文件夹中的 `Web.config` 文件：

[!code-xml[Main](user-based-authorization-vb/samples/sample14.xml)]

添加此 `<location>` 元素后，通过注销站点来测试新的 URL 授权规则。 作为匿名用户，你应该可以访问 `UserBasedAuthorization.aspx` 页面。

目前，任何经过身份验证或匿名的用户都可以访问 `UserBasedAuthorization.aspx` 页面并查看或删除文件。 让我们这样做是为了让只有经过身份验证的用户可以查看文件的内容，并且只有 Tito 可以删除文件。 可以通过声明方式、编程方式或通过这两种方法的组合应用此类精细授权规则。 让我们使用声明性方法来限制谁可以查看文件的内容;我们将使用编程方法来限制可以删除文件的用户。

### <a name="using-the-loginview-control"></a>使用登录视图控件

正如我们在过去的教程中看到的那样，登录视图控件适用于为经过身份验证的用户和匿名用户显示不同的界面，并提供一种简单的方法来隐藏匿名用户无法访问的功能。 由于匿名用户无法查看或删除文件，因此当经过身份验证的用户访问页面时，只需显示 "`FileContents`" 文本框。 若要实现此目的，请将登录视图控件添加到页面上，将其命名为 `LoginViewForFileContentsTextBox`，并将 `FileContents` 文本框的声明性标记移到登录视图控件的 `LoggedInTemplate`中。

[!code-aspx[Main](user-based-authorization-vb/samples/sample15.aspx)]

无法再从代码隐藏类直接访问登录视图模板中的 Web 控件。 例如，`FilesGrid` GridView 的 `SelectedIndexChanged` 和 `RowDeleting` 事件处理程序当前引用 `FileContents` TextBox 控件，其代码如下所示：

[!code-aspx[Main](user-based-authorization-vb/samples/sample16.aspx)]

但是，此代码不再有效。 通过将 `FileContents` 文本框移动到 `LoggedInTemplate` 无法直接访问文本框。 相反，我们必须使用 `FindControl("controlId")` 方法以编程方式引用控件。 更新 `FilesGrid` 事件处理程序以引用文本框，如下所示：

[!code-vb[Main](user-based-authorization-vb/samples/sample17.vb)]

将文本框移到登录视图的 `LoggedInTemplate` 并更新页面的代码以使用 `FindControl("controlId")` 模式引用 TextBox 后，请以匿名用户身份访问该页面。 如图10所示，不显示 "`FileContents`" 文本框。 但仍会显示视图 LinkButton。

[![登录视图控件仅为经过身份验证的用户呈现 FileContents TextBox](user-based-authorization-vb/_static/image29.png)](user-based-authorization-vb/_static/image28.png)

**图 10**：登录视图控件仅为经过身份验证的用户渲染 `FileContents` 文本框（[单击查看完全大小的图像](user-based-authorization-vb/_static/image30.png)）

隐藏匿名用户的 "查看" 按钮的一种方法是将 GridView 字段转换为 TemplateField。 这会生成一个模板，其中包含视图 LinkButton 的声明性标记。 然后，可以将登录视图控件添加到 TemplateField，并将 LinkButton 放在登录视图的 `LoggedInTemplate`中，从而隐藏了匿名访问者的 "查看" 按钮。 若要实现此目的，请在 GridView 的智能标记中单击 "编辑列" 链接以启动 "字段" 对话框。 接下来，选择左下角列表中的 "选择" 按钮，然后单击 "将此字段转换为 TemplateField" 链接。 这样做会修改该字段的声明性标记：

[!code-aspx[Main](user-based-authorization-vb/samples/sample18.aspx)]

 结束时间： 

[!code-aspx[Main](user-based-authorization-vb/samples/sample19.aspx)]

 此时，我们可以将登录视图添加到 TemplateField 中。 以下标记仅为经过身份验证的用户显示 LinkButton 视图。 

[!code-aspx[Main](user-based-authorization-vb/samples/sample20.aspx)]

如图11所示，最终结果并不是因为即使隐藏了列中的视图 LinkButtons，仍会显示视图列。 在下一部分中，我们将介绍如何隐藏整个 GridView 列（而不仅仅是 LinkButton）。

[![登录视图控件隐藏匿名访问者的视图 LinkButtons](user-based-authorization-vb/_static/image32.png)](user-based-authorization-vb/_static/image31.png)

**图 11**：登录视图控件隐藏了匿名访问者的视图 LinkButtons （[单击查看完全大小的图像](user-based-authorization-vb/_static/image33.png)）

### <a name="programmatically-limiting-functionality"></a>以编程方式限制功能

在某些情况下，声明性技术不足以将功能限制到页面。 例如，某些页面功能的可用性可能依赖于超出用户访问页面的用户是否为匿名或通过身份验证的条件。 在这种情况下，可以通过编程方式显示或隐藏各种用户界面元素。

为了以编程方式限制功能，我们需要执行两项任务：

1. 确定访问页的用户是否可以访问该功能，并
2. 基于用户是否有权访问相关功能，以编程方式修改用户界面。

为了演示这两个任务的应用程序，让我们仅允许 Tito 删除 GridView 中的文件。 然后，我们的第一个任务是确定是否 Tito 访问页面。 确定后，需要隐藏（或显示） GridView 的删除列。 GridView 的列可通过其 `Columns` 属性访问;仅当列 `Visible` 属性设置为 `True` （默认值）时，才会呈现该列。

在将数据绑定到 GridView 之前，将以下代码添加到 `Page_Load` 事件处理程序：

[!code-vb[Main](user-based-authorization-vb/samples/sample21.vb)]

如我们在[*Forms 身份验证概述*](../introduction/an-overview-of-forms-authentication-vb.md)教程中所述，`User.Identity.Name` 返回标识的名称。 这对应于在登录控件中输入的用户名。 如果 Tito 访问该页，则 GridView 的第二列的 `Visible` 属性设置为 `True`;否则，将其设置为 `False`。 最终的结果是，当 Tito 以外的其他人访问该页面时，另一个已通过身份验证的用户或匿名用户，则不会呈现删除列（见图12）;但是，当 Tito 访问该页面时，"删除" 列会出现（见图13）。

[当 Tito 以外的其他人访问 Delete 列时，不会呈现该删除列（如 Bruce） ![](user-based-authorization-vb/_static/image35.png)](user-based-authorization-vb/_static/image34.png)

**图 12**：除 Tito 以外的其他人（如 Bruce）访问 Delete 列时，不会呈现该删除列（[单击以查看完全大小的图像](user-based-authorization-vb/_static/image36.png)）

[![为 Tito 呈现 Delete 列](user-based-authorization-vb/_static/image38.png)](user-based-authorization-vb/_static/image37.png)

**图 13**：为 Tito 呈现删除列（[单击以查看完全大小的图像](user-based-authorization-vb/_static/image39.png)）

## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>步骤4：将授权规则应用于类和方法

在步骤3中，我们不允许匿名用户查看文件内容和禁止所有用户，但 Tito 删除文件。 为实现此目的，通过声明性和编程技术隐藏了未经授权的访问者的关联用户界面元素。 对于我们的简单示例，正确地隐藏用户界面元素非常简单，但对于更复杂的站点，可能有许多不同的方法来执行相同的功能呢？ 在将此功能限制给未经授权的用户的情况下，如果我们忘记隐藏或禁用所有适用的用户界面元素，会发生什么情况呢？

确保未经授权的用户无法访问特定功能的一种简单方法是使用[`PrincipalPermission` 特性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)来修饰该类或方法。 当 .NET 运行时使用一个类或执行它的一个方法时，它会进行检查以确保当前安全上下文有权使用类或执行方法。 `PrincipalPermission` 属性提供了一种机制，通过该机制可以定义这些规则。

接下来，我们将演示如何使用 GridView `SelectedIndexChanged` 上的 `PrincipalPermission` 属性，并 `RowDeleting` 事件处理程序禁止匿名用户和 Tito 以外的用户执行。 我们需要做的就是在每个函数定义的顶部添加适当的属性：

[!code-vb[Main](user-based-authorization-vb/samples/sample22.vb)]

`SelectedIndexChanged` 事件处理程序的属性规定，只有经过身份验证的用户才能执行事件处理程序，因为 `RowDeleting` 事件处理程序的属性将执行限制为 Tito。

> [!NOTE]
> 特性可应用于类、方法、属性或事件。 在添加属性时，它必须是类、方法、属性或事件声明语句的一部分。 由于 Visual Basic 使用换行符作为语句分隔符，因此，特性必须与声明一起显示在同一行上，或者与行继续符（下划线）出现在其上方。 在上面的代码段中，行继续符用于将属性放置在一行上，并将方法声明放置在另一行上。

如果用户不是 Tito 的用户尝试执行 `RowDeleting` 事件处理程序或未经身份验证的用户尝试执行 `SelectedIndexChanged` 事件处理程序，.NET 运行时将引发 `SecurityException`。

[![如果安全上下文无权执行此方法，则会引发 SecurityException](user-based-authorization-vb/_static/image41.png)](user-based-authorization-vb/_static/image40.png)

**图 14**：如果安全上下文无权执行此方法，则会引发 `SecurityException` （[单击查看完全大小的映像](user-based-authorization-vb/_static/image42.png)）

> [!NOTE]
> 若要允许多个安全上下文访问类或方法，请使用每个安全上下文的 `PrincipalPermission` 特性来修饰类或方法。 也就是说，若要允许 Tito 和 Bruce 执行 `RowDeleting` 事件处理程序，请添加*两个*`PrincipalPermission` 属性：

[!code-vb[Main](user-based-authorization-vb/samples/sample23.vb)]

除了 ASP.NET 页面以外，许多应用程序还具有一种体系结构，其中包括各种层，如业务逻辑和数据访问层。 这些层通常实现为类库，并提供用于执行业务逻辑和数据相关功能的类和方法。 `PrincipalPermission` 特性适用于将授权规则应用于这些层。

有关使用 `PrincipalPermission` 特性定义有关类和方法的授权规则的详细信息，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[使用 `PrincipalPermissionAttributes`将授权规则添加到业务层和数据层](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)。

## <a name="summary"></a>总结

在本教程中，我们介绍了如何应用基于用户的授权规则。 我们首先来看一下 ASP。NET 的 URL 授权框架。 对于每个请求，ASP.NET 引擎的 `UrlAuthorizationModule` 会检查在应用程序配置中定义的 URL 授权规则，以确定标识是否有权访问所请求的资源。 简而言之，使用 URL 授权，可以轻松地为特定页面或特定目录中的所有页面指定授权规则。

URL 授权框架逐页应用授权规则。 使用 URL 授权，请求标识有权访问特定资源。 但在许多情况下，调用更精细的授权规则。 我们可能需要让每个人都能访问某个页面，但要显示不同的数据或提供不同的功能，具体取决于访问页面的用户，而不是定义谁可以访问某个页面。 页面级授权通常涉及隐藏特定的用户界面元素，以防止未经授权的用户访问禁止的功能。 此外，还可以使用属性来限制对某些用户的类和其方法的访问。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用 `PrincipalPermissionAttributes` 将授权规则添加到业务层和数据层](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 授权](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IIS6 和 IIS7 安全性之间的更改](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [配置特定文件和子目录](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [限制基于用户的数据修改功能](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb.md)
- [登录视图控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [了解 IIS7 URL 授权](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 技术文档](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [在 ASP.NET 2.0 中处理数据](../../data-access/index.md)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](validating-user-credentials-against-the-membership-user-store-vb.md)
> [下一页](storing-additional-user-information-vb.md)
