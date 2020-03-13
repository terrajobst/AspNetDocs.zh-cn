---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-cs
title: 创建用户帐户（C#） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将探讨如何使用成员身份框架（通过 SqlMembershipProvider）创建新的用户帐户。 我们将了解如何创建新的 。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: f175278c-6079-4d91-b9b4-2493ed43d9ec
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: 955592320e7d36c7ae3b9c03a361bee2183f1776
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512978"
---
# <a name="creating-user-accounts-c"></a>创建用户帐户 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_CS.zip)或[下载 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_cs.pdf)

> 在本教程中，我们将探讨如何使用成员身份框架（通过 SqlMembershipProvider）创建新的用户帐户。 我们将了解如何以编程方式和通过 ASP 创建新用户。NET 的内置 CreateUserWizard 控件。

## <a name="introduction"></a>简介

在<a id="_msoanchor_1"> </a>[前面的教程](creating-the-membership-schema-in-sql-server-cs.md)中，我们在数据库中安装了应用程序服务架构，后者添加了 `SqlMembershipProvider` 和 `SqlRoleProvider`所需的表、视图和存储过程。 这会创建我们在本系列的其余教程中所需的基础结构。 在本教程中，我们将探讨如何使用成员身份框架（通过 `SqlMembershipProvider`）来创建新的用户帐户。 我们将了解如何以编程方式和通过 ASP 创建新用户。NET 的内置 CreateUserWizard 控件。

除了学习如何创建新的用户帐户之外，我们还需要更新首次在 *<a id="_msoanchor_2"></a>[ forms authentication 概述](../introduction/an-overview-of-forms-authentication-cs.md)* 教程中创建的演示网站，并在 *<a id="https://www.asp.net/learn/security/tutorial-03-cs.aspx"></a>forms 身份验证配置和高级主题*教程中进行了改进。 我们的演示 web 应用程序具有一个登录页，该页面通过硬编码的用户名/密码对来验证用户的凭据。 此外，`Global.asax` 包括为经过身份验证的用户创建自定义 `IPrincipal` 和 `IIdentity` 对象的代码。 我们将更新登录页面，以根据成员身份框架验证用户的凭据，并删除自定义主体和标识逻辑。

让我们进入正题！

## <a name="the-forms-authentication-and-membership-checklist"></a>Forms 身份验证和成员清单

在开始使用成员身份框架之前，让我们花点时间回顾一下我们所做的重要步骤。 在基于窗体的身份验证方案中将成员身份框架与 `SqlMembershipProvider` 结合使用时，需要在 web 应用程序中实现成员资格功能之前执行以下步骤：

1. **启用基于窗体的身份验证。** 如我们在 *<a id="_msoanchor_4"></a>[forms 身份验证概述](../introduction/an-overview-of-forms-authentication-cs.md)* 中所述，通过编辑 `Web.config`，并将 `<authentication>` 元素的 `mode` 属性设置为 `Forms`，可以启用窗体身份验证。 启用窗体身份验证后，将检查每个传入请求中是否存在*forms 身份验证票证*（如果存在），则会标识请求者。
2. **将应用程序服务架构添加到相应的数据库。** 使用 `SqlMembershipProvider` 时，需要将应用程序服务架构安装到数据库。 通常，此架构将添加到保存应用程序数据模型的同一数据库。 *<a id="_msoanchor_5"></a>[在 SQL Server 教程中创建成员身份架构](creating-the-membership-schema-in-sql-server-cs.md)* 介绍了如何使用 `aspnet_regsql.exe` 工具实现此目的。
3. **自定义 Web 应用程序的设置，以引用步骤2中的数据库。** *在 SQL Server 教程中创建成员身份架构*介绍了两种配置 web 应用程序的方法，以便 `SqlMembershipProvider` 使用步骤2：修改 `LocalSqlServer` 连接字符串名称;或者，通过将新的已注册提供程序添加到成员身份框架提供程序列表，并自定义该新提供程序以使用步骤2中的数据库。

生成使用 `SqlMembershipProvider` 和基于窗体的身份验证的 web 应用程序时，需要执行以下三个步骤，然后才能使用 `Membership` 类或 ASP.NET 登录 Web 控件。 由于我们已在前面的教程中执行这些步骤，因此可以开始使用成员资格框架！

## <a name="step-1-adding-new-aspnet-pages"></a>步骤 1：添加新的 ASP.NET 页面

在本教程中，接下来的三个将检查与成员资格相关的各种功能。 我们将需要一系列 ASP.NET 页面来实现这些教程中所讨论的主题。 接下来，我们将创建这些页面，然后 `(Web.sitemap)`一个站点地图文件。

首先，在项目中创建一个名为 `Membership`的新文件夹。 接下来，将五个新的 ASP.NET 页面添加到 `Membership` 文件夹，将每个页面与 `Site.master` 的母版页链接。 命名页面：

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

此时，项目的解决方案资源管理器应类似于图1所示的屏幕截图。

[![五个新页面已添加到成员资格文件夹](creating-user-accounts-cs/_static/image2.png)](creating-user-accounts-cs/_static/image1.png)

**图 1**：已将五个新页面添加到 `Membership` 文件夹（[单击查看完全大小的图像](creating-user-accounts-cs/_static/image3.png)）

此时，每个页面都应具有两个内容控件，一个用于母版页的每个 Contentplaceholder： `MainContent` 和 `LoginContent`。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample1.aspx)]

请记住，`LoginContent` ContentPlaceHolder 的默认标记会显示一个用于登录或注销站点的链接，具体取决于是否对用户进行了身份验证。 但 `Content2` 内容控件的存在会替代母版页的默认标记。 如我们在 *<a id="_msoanchor_6"></a>[Forms 身份验证概述](../introduction/an-overview-of-forms-authentication-cs.md)* 教程中所述，这在页面中很有用，我们不想在左列中显示与登录相关的选项。

但对于这五个页面，我们想要为 `LoginContent` ContentPlaceHolder 显示母版页的默认标记。 因此，删除 `Content2` 内容控件的声明性标记。 完成此操作后，五个页面的标记中的每一个都应该只包含一个内容控件。

## <a name="step-2-creating-the-site-map"></a>步骤 2：创建站点地图

除最普通的网站外，还需要实现某种形式的导航用户界面。 导航用户界面可能是指向网站各个部分的链接的简单列表。 或者，这些链接可能排列为菜单或树视图。 作为页面开发人员，创建导航用户界面只是故事的一半。 我们还需要通过某种方式来定义站点的逻辑结构，这是一个可维护且可更新的方式。 添加新页面或删除现有页面后，我们希望能够更新单个源（站点地图），并使这些修改在站点的导航用户界面中反映出来。

这两个任务（定义站点地图和实现基于站点图的导航用户界面）可以轻松完成，因为在 ASP.NET 版本2.0 中添加了站点地图框架和导航 Web 控件。 使用站点地图框架，开发人员可以定义站点地图，然后通过编程 API （ [`SiteMap` 类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)）来访问它。 内置的导航 Web 控件包括[菜单控件](https://msdn.microsoft.com/library/bz09dy46.aspx)、 [TreeView 控件](https://msdn.microsoft.com/library/3eafky27.aspx)和[SiteMapPath 控件](https://msdn.microsoft.com/library/3eafky27.aspx)。

与成员身份和角色框架一样，站点地图框架是在[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)的顶层生成的。 站点地图提供程序类的工作是从永久性数据存储（如 XML 文件或数据库表）生成由 `SiteMap` 类使用的内存中结构。 该 .NET Framework 附带了一个默认的站点地图提供程序，该提供程序从 XML 文件（[`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)）读取站点地图数据，这是我们将在本教程中使用的提供程序。 有关某些备用站点地图提供程序的实现，请参阅本教程末尾的 "后续读取" 部分。

默认站点地图提供程序需要一个名为 `Web.sitemap` 的格式正确的 XML 文件，才能存在根目录。 由于我们使用的是此默认提供程序，因此需要添加此类文件，并以适当的 XML 格式定义站点图的结构。 若要添加文件，请在解决方案资源管理器中右键单击项目名称，然后选择 "添加新项"。 在对话框中，选择添加一个名为 "站点地图" 的文件，其名称为 `Web.sitemap`。

[![将名为 web.sitemap 的文件添加到项目的根目录](creating-user-accounts-cs/_static/image5.png)](creating-user-accounts-cs/_static/image4.png)

**图 2**：将名为 `Web.sitemap` 的文件添加到项目的根目录（[单击查看完全大小的映像](creating-user-accounts-cs/_static/image6.png)）

XML 站点地图文件将网站的结构定义为层次结构。 此层次结构关系通过 `<siteMapNode>` 元素的体系在 XML 文件中建模。 `Web.sitemap` 必须以具有恰好一个 `<siteMapNode>` 子节点的 `<siteMap>` 父节点开头。 此顶级 `<siteMapNode>` 元素表示层次结构的根，可以具有任意数量的子代节点。 每个 `<siteMapNode>` 元素都必须包含一个 `title` 属性，还可以选择包括 `url` 和 `description` 属性以及其他属性;每个非空 `url` 特性都必须是唯一的。

在 `Web.sitemap` 文件中输入以下 XML：

[!code-xml[Main](creating-user-accounts-cs/samples/sample2.xml)]

以上站点地图标记定义图3中所示的层次结构。

[![站点地图表示分层导航结构](creating-user-accounts-cs/_static/image8.png)](creating-user-accounts-cs/_static/image7.png)

**图 3**：站点地图表示分层的导航结构（[单击以查看完全大小的图像](creating-user-accounts-cs/_static/image9.png)）

## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>步骤 3：更新母版页以包含导航用户界面

ASP.NET 包含一些用于设计用户界面的与导航相关的 Web 控件。 其中包括菜单、TreeView 和 SiteMapPath 控件。 Menu 和 TreeView 控件分别在菜单或树中显示站点地图结构，而 SiteMapPath 显示一个痕迹导航，其中显示了当前正在访问的节点及其上级。 站点地图数据可以绑定到其他使用 SiteMapDataSource 的数据 Web 控件，并可通过 `SiteMap` 类以编程方式进行访问。

由于对站点地图框架和导航控件的全面讨论超出了本系列教程的范畴，而不是花时间手工编写自己的导航用户界面，而不是使用 *[ASP.NET 2.0](../../data-access/index.md)* 教程系列中的数据，而是使用一个 Repeater 控件来显示导航链接的两层项目符号列表，如图4所示。

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>在左列中添加一个两层链接列表

若要创建此接口，请将以下声明性标记添加到 `Site.master` 母版页的左侧列中，其中文本 "TODO：将在此处显示菜单 ... "当前位于。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample3.aspx)]

上述标记将名为 `menu` 的中继器控件绑定到 SiteMapDataSource，后者返回在 `Web.sitemap`中定义的站点地图层次结构。 由于 SiteMapDataSource 控件的[`ShowStartingNode` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)设置为 False，因此它将从 "Home" 节点的子代开始返回站点地图的层次结构。 中继器在 `<li>` 元素中显示每个节点（当前只是 "成员资格"）。 然后，内部中继器在嵌套的无序列表中显示当前节点的子节点。

图4显示了上述标记的呈现输出，以及我们在步骤2中创建的站点地图结构。 中继器呈现 vanilla 的无序列表标记;`Styles.css` 中定义的级联样式表规则负责具的布局。 有关上述标记如何工作的更详细说明，请参阅[母版页和站点导航](https://asp.net/learn/data-access/tutorial-03-cs.aspx)教程。

[![使用嵌套的无序列表呈现导航用户界面](creating-user-accounts-cs/_static/image11.png)](creating-user-accounts-cs/_static/image10.png)

**图 4**：使用嵌套的无序列表呈现导航用户界面（[单击以查看完全大小的图像](creating-user-accounts-cs/_static/image12.png)）

### <a name="adding-breadcrumb-navigation"></a>添加痕迹导航

除了左栏中的链接列表之外，我们还让每个页面显示一个[痕迹导航](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)。 痕迹导航是一个导航用户界面元素，可快速向用户显示其在站点层次结构中的当前位置。 SiteMapPath 控件使用站点地图框架来确定当前页面在站点地图中的位置，然后基于此信息显示痕迹导航。

具体而言，将 `<span>` 元素添加到母版页的标头 `<div>` 元素，并将新的 `<span>` 元素的 `class` 特性设置为 "痕迹导航"。 （`Styles.css` 类包含 "痕迹导航" 类的规则。）接下来，将 SiteMapPath 添加到此新的 `<span>` 元素。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample4.aspx)]

图5显示了访问 `~/Membership/CreatingUserAccounts.aspx`时 SiteMapPath 的输出。

[![痕迹导航显示当前页及其在站点地图中的上级](creating-user-accounts-cs/_static/image14.png)](creating-user-accounts-cs/_static/image13.png)

**图 5**：痕迹导航显示网站图中的当前页及其上级（[单击以查看完全大小的图像](creating-user-accounts-cs/_static/image15.png)）

## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>步骤 4：删除自定义主体和标识逻辑

在 *<a id="_msoanchor_7"></a>[Forms 身份验证配置和高级主题](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)* 教程中，我们介绍了如何将自定义主体和标识对象关联到经过身份验证的用户。 为此，我们需要在应用程序的 `PostAuthenticateRequest` 事件 `Global.asax` 中创建一个事件处理程序，该事件处理程序会在对用户进行身份验证 `FormsAuthenticationModule` 后触发。 在此事件处理程序中，我们使用我们在本教程中创建的 `CustomPrincipal` 和 `CustomIdentity` 对象替换了 `FormsAuthenticationModule` 添加的 `GenericPrincipal` 和 `FormsIdentity` 对象。

尽管自定义主体和标识对象在某些情况下非常有用，但在大多数情况下，`GenericPrincipal` 和 `FormsIdentity` 对象就足够了。 因此，我认为有必要返回到默认行为。 通过移除或注释掉 `PostAuthenticateRequest` 事件处理程序或完全删除 `Global.asax` 文件来进行此更改。

## <a name="step-5-programmatically-creating-a-new-user"></a>步骤 5：以编程方式创建新用户

若要通过成员身份框架创建新用户帐户，请使用 `Membership` 类的[`CreateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)。 此方法具有用于用户名、密码和其他用户相关字段的输入参数。 调用时，它会将新用户帐户的创建委托给配置的成员资格提供程序，然后返回一个表示刚刚创建的用户帐户的[`MembershipUser` 对象](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)。

`CreateUser` 方法具有四个重载，每个重载接受不同数量的输入参数：

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

这四种重载不同于收集的信息量。 例如，第一个重载只需要新用户帐户的用户名和密码，而另一个重载还需要用户的电子邮件地址。

这些重载存在是因为创建新用户帐户所需的信息取决于成员资格提供程序的配置设置。 在 *<a id="_msoanchor_8"></a>[SQL Server 教程中 创建成员身份架构](creating-the-membership-schema-in-sql-server-cs.md)* 中，我们检查了在 `Web.config` 中指定成员资格提供程序配置设置。 表2提供了配置设置的完整列表。

此类成员资格提供程序配置设置会影响可以使用的 `CreateUser` 重载，这是 `requiresQuestionAndAnswer` 设置。 如果 `requiresQuestionAndAnswer` 设置为 `true` （默认值），则在创建新的用户帐户时，必须指定安全问题和答案。 如果用户需要重置或更改其密码，以后会使用此信息。 具体而言，在这种情况下，他们会显示安全问题，必须输入正确答案才能重置或更改其密码。 因此，如果 `requiresQuestionAndAnswer` 设置为 `true` 则调用前两个 `CreateUser` 重载之一会导致异常，因为缺少安全问题和答案。 由于我们的应用程序当前配置为需要安全问题和答案，因此，在以编程方式创建用户时，我们需要使用后两种重载之一。

为了说明如何使用 `CreateUser` 方法，让我们创建一个用户界面，我们会在其中提示用户输入名称、密码、电子邮件和预定义安全问题的答案。 打开 `Membership` 文件夹中的 "`CreatingUserAccounts.aspx`" 页，并将以下 Web 控件添加到内容控件：

- 名为 `Username` 的文本框
- 名为 `Password`的文本框，其 `TextMode` 属性设置为 `Password`
- 名为 `Email` 的文本框
- 已清除其 `Text` 属性的名为 `SecurityQuestion` 的标签
- 名为 `SecurityAnswer` 的文本框
- 名为 `CreateAccountButton` 的按钮，其 Text 属性设置为 "创建用户帐户"
- 已清除其 `Text` 属性的名为 `CreateAccountResults` 的标签控件

此时，屏幕应类似于图6所示的屏幕截图。

[![将各种 Web 控件添加到 CreatingUserAccounts 页](creating-user-accounts-cs/_static/image17.png)](creating-user-accounts-cs/_static/image16.png)

**图 6**：将各种 Web 控件添加到 "`CreatingUserAccounts.aspx`" 页（[单击以查看完全大小的图像](creating-user-accounts-cs/_static/image18.png)）

"`SecurityQuestion` 标签" 和 "`SecurityAnswer`" 文本框旨在显示预定义的安全问题并收集用户的答案。 请注意，安全问题和答案都按用户单独存储，因此可以允许每个用户定义其自己的安全问题。 但是，在此示例中，我决定使用通用安全问题，即："您最喜欢的颜色是什么？"

若要实现此预定义的安全问题，请将一个常量添加到名为 `passwordQuestion`的页面的代码隐藏类中，并为其分配安全问题。 然后，在 `Page_Load` 事件处理程序中，将此常量分配给 `SecurityQuestion` 标签的 `Text` 属性：

[!code-csharp[Main](creating-user-accounts-cs/samples/sample5.cs)]

接下来，为 `CreateAccountButton`的 `Click` 事件创建事件处理程序并添加以下代码：

[!code-csharp[Main](creating-user-accounts-cs/samples/sample6.cs)]

`Click` 事件处理程序通过定义[`MembershipCreateStatus`](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)类型的名为 `createStatus` 的变量开始。 `MembershipCreateStatus` 是指示 `CreateUser` 操作状态的枚举。 例如，如果成功创建了用户帐户，则生成的 `MembershipCreateStatus` 实例将设置为 `Success`的值;另一方面，如果由于已存在具有相同用户名的用户而导致操作失败，则会将其设置为 `DuplicateUserName`的值。 在我们使用的 `CreateUser` 重载中，需要将 `MembershipCreateStatus` 实例作为 `out` 参数传递到方法中。 此参数在 `CreateUser` 方法中设置为适当的值，我们可以在方法调用后检查其值，以确定是否已成功创建用户帐户。

在调用 `CreateUser`之后（传入 `createStatus`），`switch` 语句用于根据分配给 `createStatus`的值输出适当的消息。 图7显示了成功创建新用户时的输出。 图8和9显示用户帐户未创建时的输出。 在图8中，访问者输入了一个不满足成员资格提供程序的配置设置中所述密码强度要求的五字母密码。 在图9中，访问者尝试使用现有用户名（在图7中创建的用户名）创建用户帐户。

[![已成功创建新用户帐户](creating-user-accounts-cs/_static/image20.png)](creating-user-accounts-cs/_static/image19.png)

**图 7**：已成功创建新用户帐户（[单击以查看完全大小的映像](creating-user-accounts-cs/_static/image21.png)）

[![未创建用户帐户，因为提供的密码太弱](creating-user-accounts-cs/_static/image23.png)](creating-user-accounts-cs/_static/image22.png)

**图 8**：用户帐户未创建，因为提供的密码太弱（[单击以查看完全大小的映像](creating-user-accounts-cs/_static/image24.png)）

[![由于用户名已在使用中而不创建用户帐户](creating-user-accounts-cs/_static/image26.png)](creating-user-accounts-cs/_static/image25.png)

**图 9**：由于用户名已被使用，因此不会创建用户帐户（[单击以查看完全大小的映像](creating-user-accounts-cs/_static/image27.png)）

> [!NOTE]
> 您可能想知道如何使用前两个 `CreateUser` 方法重载之一来确定是否成功或失败，这两种重载都没有 `MembershipCreateStatus`类型的参数。 在出现故障时，前两个重载引发[`MembershipCreateUserException` 异常](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx)，其中包含类型 `MembershipCreateStatus`的[`StatusCode` 属性](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx)。

创建一些用户帐户后，验证是否已通过列出 `SecurityTutorials.mdf` 数据库中的 `aspnet_Users` 和 `aspnet_Membership` 表的内容来创建帐户。 如图10所示，我已通过 `CreatingUserAccounts.aspx` 页添加了两个用户：Tito 和 Bruce。

[![成员资格用户存储中有两个用户：Tito 和 Bruce](creating-user-accounts-cs/_static/image29.png)](creating-user-accounts-cs/_static/image28.png)

**图 10**：成员资格用户存储中有两个用户：Tito 和 Bruce （[单击以查看完全大小的映像](creating-user-accounts-cs/_static/image30.png)）

虽然成员身份用户存储现在包含 Bruce 和 Tito 的帐户信息，但我们仍要实现允许 Bruce 或 Tito 登录到站点的功能。 目前，`Login.aspx` 根据一组硬编码的用户名/密码对来验证用户的凭据，而*不*会根据成员身份框架验证提供的凭据。 现在，在 `aspnet_Users` 中查看新用户帐户，并且 `aspnet_Membership` 表将必须足够。 在下一教程中， *<a id="_msoanchor_9"></a>[根据成员身份用户存储验证用户凭据](validating-user-credentials-against-the-membership-user-store-cs.md)* ，我们将更新登录页，以根据成员资格存储区进行验证。

> [!NOTE]
> 如果你在 `SecurityTutorials.mdf` 数据库中看不到任何用户，则可能是因为你的 web 应用程序正在使用默认的成员资格提供程序，`AspNetSqlMembershipProvider`，该提供程序使用 `ASPNETDB.mdf` 数据库作为其用户存储。 若要确定这是否是问题，请单击 "解决方案资源管理器中的" 刷新 "按钮。 如果已将名为 `ASPNETDB.mdf` 的数据库添加到 `App_Data` 文件夹，则会出现此问题。 返回到 *<a id="_msoanchor_10"></a>[在 SQL Server 教程中创建成员身份架构](creating-the-membership-schema-in-sql-server-cs.md)* 的步骤4，以获取有关如何正确配置成员资格提供程序的说明。

在大多数 "创建用户帐户" 方案中，访问者将向用户提供一个接口，用于输入用户名、密码、电子邮件和其他重要信息，此时会创建新帐户。 在此步骤中，我们将介绍如何使用 `Membership.CreateUser` 方法以编程方式基于用户的输入来添加新用户帐户。 但我们的代码刚刚创建了新用户帐户。 它不执行任何后续操作，例如，将用户登录到刚刚创建的用户帐户下的站点，或者向用户发送一封确认电子邮件。 这些附加步骤将需要按钮 `Click` 事件处理程序中的附加代码。

ASP.NET 附带了 CreateUserWizard 控件，该控件旨在处理用户帐户创建过程，从呈现用于创建新用户帐户的用户界面，到在成员身份框架中创建帐户并执行后帐户创建任务，如发送确认电子邮件和将刚刚创建的用户记录到站点。 使用 CreateUserWizard 控件就像将 CreateUserWizard 控件从工具箱拖到页面上，然后设置几个属性一样简单。 在大多数情况下，无需编写一行代码。 我们将在步骤6中详细探讨此超酷控件。

如果仅通过典型的 "创建帐户" 网页创建新的用户帐户，则不可能需要编写使用 `CreateUser` 方法的代码，因为 CreateUserWizard 控件可能会满足你的需求。 但是，在需要高度自定义的创建帐户用户体验的情况下，或者在需要通过备用接口以编程方式创建新用户帐户时，`CreateUser` 方法非常方便。 例如，你可能有一个允许用户上传包含其他应用程序的用户信息的 XML 文件的页面。 该页可能会分析上传的 XML 文件的内容，并通过调用 `CreateUser` 方法为 XML 中表示的每个用户创建一个新帐户。

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>步骤 6：使用 CreateUserWizard 控件创建新用户

ASP.NET 附带了大量登录 Web 控件。 这些控件有助于许多常见的用户帐户和登录相关方案。 [CreateUserWizard 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)是一个这样的控件，旨在提供用于将新用户帐户添加到成员身份框架的用户界面。

与许多其他登录相关的 Web 控件一样，无需编写任何代码即可使用 CreateUserWizard。 它直观地提供基于成员资格提供程序的配置设置的用户界面，并在用户输入所需信息并单击 "创建用户" 按钮后，在内部调用 `Membership` 类的 `CreateUser` 方法。 CreateUserWizard 控件非常可自定义。 在帐户创建过程的各个阶段，会触发一个事件宿主。 我们可以根据需要创建事件处理程序，以将自定义逻辑注入帐户创建工作流。 而且，CreateUserWizard 的外观非常灵活。 定义默认接口外观的属性有很多;如有必要，可将该控件转换为模板或添加其他用户注册 "步骤"。

首先，让我们看一下如何使用 CreateUserWizard 控件的默认接口和行为。 接下来，我们将探讨如何通过控件的属性和事件自定义外观。

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>检查 CreateUserWizard 的默认界面和行为

返回到 `Membership` 文件夹中的 "`CreatingUserAccounts.aspx`" 页，切换到 "设计" 或 "拆分" 模式，然后将 CreateUserWizard 控件添加到页面顶部。 CreateUserWizard 控件将在工具箱的登录控件部分下进行存档。 添加控件后，将其 `ID` 属性设置为 `RegisterUser`。 如图11所示的屏幕截图所示，CreateUserWizard 会呈现一个带有新用户用户名、密码、电子邮件地址和安全问题和答案的文本框界面。

[![CreateUserWizard 控件呈现通用创建用户界面](creating-user-accounts-cs/_static/image32.png)](creating-user-accounts-cs/_static/image31.png)

**图 11**：CreateUserWizard 控件呈现通用创建用户界面（[单击以查看完全大小的图像](creating-user-accounts-cs/_static/image33.png)）

让我们花点时间将 CreateUserWizard 控件生成的默认用户界面与我们在步骤5中创建的接口进行比较。 对于初学者，CreateUserWizard 控件允许访问者指定安全问题和答案，而我们手动创建的接口则使用预定义的安全问题。 CreateUserWizard 控件的界面还包括验证控件，而我们尚未对接口的窗体字段实施验证。 CreateUserWizard 控件接口包含一个 "确认密码" 文本框（以及一个 CompareValidator，以确保输入的 "Password" 和 "Compare Password" 文本框相同）。

有趣的是，CreateUserWizard 控件在呈现其用户界面时，会咨询成员资格提供程序的配置设置。 例如，仅当 "`requiresQuestionAndAnswer`" 设置为 "True" 时才会显示 "安全问题" 和 "答案" 文本框。 同样，CreateUserWizard 会自动添加 RegularExpressionValidator 控件，以确保满足密码强度要求，并基于 `minRequiredPasswordLength`、`minRequiredNonalphanumericCharacters`和 `passwordStrengthRegularExpression` 配置设置来设置其 `ErrorMessage` 和 `ValidationExpression` 属性。

如名称所示，CreateUserWizard 控件派生自[向导控件](https://msdn.microsoft.com/library/s2etd1ek.aspx)。 向导控件旨在提供用于完成多步骤任务的接口。 一个向导控件可能具有任意数量的 `WizardSteps`，其中每个都是定义该步骤的 HTML 和 Web 控件的模板。 向导控件最初显示第一 `WizardStep`，以及允许用户从一个步骤转到下一步的导航控件，或返回到前面的步骤。

如图11中的声明性标记所示，CreateUserWizard 控件的默认接口包括两个 `WizardSteps:`

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) –呈现接口以收集用于创建新用户帐户的信息。 此步骤如图11所示。
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) –呈现一条消息，指示已成功创建帐户。

可以通过将这些步骤转换为模板或添加自己的 `WizardSteps`来修改 CreateUserWizard 的外观和行为。 在*存储其他用户信息*教程中，我们将介绍如何将 `WizardStep` 添加到注册界面。

让我们看看操作中的 CreateUserWizard 控件。 通过浏览器访问 `CreatingUserAccounts.aspx` 页面。 首先，将一些无效值输入到 CreateUserWizard 的接口中。 尝试输入不符合密码强度要求的密码，或将 "用户名" 文本框留空。 CreateUserWizard 将显示适当的错误消息。 图12显示了尝试使用不足强密码创建用户时的输出。

[![CreateUserWizard 自动注入验证控件](creating-user-accounts-cs/_static/image35.png)](creating-user-accounts-cs/_static/image34.png)

**图 12**：CreateUserWizard 自动注入验证控件（[单击查看完全大小的图像](creating-user-accounts-cs/_static/image36.png)）

接下来，在 CreateUserWizard 中输入适当的值，然后单击 "创建用户" 按钮。 假设已输入必填字段并且密码强度足够，则 CreateUserWizard 将通过成员身份框架创建新的用户帐户，然后显示 `CompleteWizardStep`的接口（参见图13）。 在后台，CreateUserWizard 调用 `Membership.CreateUser` 方法，就像我们在步骤5中所做的一样。

[![已成功创建新用户帐户](creating-user-accounts-cs/_static/image38.png)](creating-user-accounts-cs/_static/image37.png)

**图 13**：已成功创建新用户帐户（[单击以查看完全大小的映像](creating-user-accounts-cs/_static/image39.png)）

> [!NOTE]
> 如图13所示，`CompleteWizardStep`的接口包含一个 "继续" 按钮。 但是，在这种情况下，单击它只是执行回发，使访问者保持在同一页面上。 在 "通过其属性自定义 CreateUserWizard 的外观和行为" 部分中，我们将介绍如何使用此按钮将访问者发送到 `Default.aspx` （或其他某个页面）。

创建新的用户帐户后，返回到 Visual Studio 并检查 `aspnet_Users`，并 `aspnet_Membership` 表中进行操作，如图10所示，验证是否已成功创建帐户。

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>通过其属性自定义 CreateUserWizard 的行为和外观

通过属性、`WizardSteps`和事件处理程序，可以通过多种方式自定义 CreateUserWizard。 在本部分中，我们将介绍如何通过其属性来自定义控件的外观;下一节将介绍如何通过事件处理程序扩展控件的行为。

几乎所有在 CreateUserWizard 控件的默认用户界面中显示的文本都可以通过其属性的很多进行自定义。 例如，文本框左侧显示的 "用户名"、"密码"、"确认密码"、"电子邮件"、"安全问题" 和 "安全答案" 标签可分别由[`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx)、 [`PasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx)、 [`ConfirmPasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx)、 [`EmailLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx)、 [`QuestionLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)和[`AnswerLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx)属性自定义。 同样，还有一些属性用于指定 `CreateUserWizardStep` 和 `CompleteWizardStep`中 "创建用户" 和 "继续" 按钮的文本，以及这些按钮是否呈现为按钮、LinkButtons 或 ImageButtons。

颜色、边框、字体和其他可视元素可通过样式属性的主机进行配置。 CreateUserWizard 控件本身具有常见的 Web 控件样式属性（`BackColor`、`BorderStyle`、`CssClass`、`Font`等），并且有许多用于定义 CreateUserWizard 界面特定部分的外观的样式属性。 例如， [`TextBoxStyle` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx)定义 `CreateUserWizardStep`中的文本框的样式，而[`TitleTextStyle` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx)定义标题的样式（"注册新帐户"）。

除了与外观相关的属性之外，还有许多属性会影响 CreateUserWizard 控件的行为。 如果设置为 True，则[`DisplayCancelButton` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)将在 "创建用户" 按钮旁显示 "取消" 按钮（默认值为 False）。 如果显示 "取消" 按钮，请确保同时设置 " [`CancelDestinationPageUrl`" 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)，该属性指定单击 "取消" 后要将用户发送到的页面。 如上一节所述，`CompleteWizardStep`界面中的 "继续" 按钮会导致回发，但会将访问者留在同一页面上。 若要在单击 "继续" 按钮后将访问者发送到其他页面，只需在 " [`ContinueDestinationPageUrl`" 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)中指定 URL。

让我们更新 `RegisterUser` CreateUserWizard 控件以显示 "取消" 按钮，并在单击 "取消" 或 "继续" 按钮后将访问者发送到 `Default.aspx`。 若要实现此目的，请将 `DisplayCancelButton` 属性设置为 True，并将 `CancelDestinationPageUrl` 和 `ContinueDestinationPageUrl` 属性设置为 "~/Default.aspx"。 图14显示了通过浏览器查看时更新的 CreateUserWizard。

[![Createuserwizardstep.contenttemplate 包含 "取消" 按钮](creating-user-accounts-cs/_static/image41.png)](creating-user-accounts-cs/_static/image40.png)

**图 14**：`CreateUserWizardStep` 包含 "取消" 按钮（[单击以查看完全大小的图像](creating-user-accounts-cs/_static/image42.png)）

当访问者输入用户名、密码、电子邮件地址和安全问题，并单击 "创建用户" 时，将创建新的用户帐户，并以该新创建的用户身份登录。 假设访问该页的人员为自己创建了一个新帐户，这可能是所需的行为。 但是，你可能想要允许管理员添加新的用户帐户。 在此过程中，将创建用户帐户，但管理员仍将以管理员身份（而不是新创建的帐户）登录。 此行为可通过布尔[`LoginCreatedUser` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)进行修改。

成员身份框架中的用户帐户包含批准的标志;未获批准的用户无法登录到站点。 默认情况下，新创建的帐户将标记为 "已批准"，从而允许用户立即登录到该站点。 但是，有可能将新的用户帐户标记为未批准。 也许你希望管理员可以在用户登录之前手动批准新用户;或者，您可能希望在允许用户登录之前验证注册时输入的电子邮件地址是否有效。 无论是哪种情况，都可以将 CreateUserWizard 控件的[`DisableCreatedUser` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)设置为 True （默认值为 False），以将新创建的用户帐户标记为未批准。

注释的其他与行为相关的属性包括 `AutoGeneratePassword` 和 `MailDefinition`。 如果[`AutoGeneratePassword` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx)设置为 True，则 `CreateUserWizardStep` 不会显示 "密码" 和 "确认密码" 文本框;而是使用 `Membership` 类的[`GeneratePassword` 方法](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)自动生成新创建的用户的密码。 `GeneratePassword` 方法构造指定长度的密码，并使用足够数量的非字母数字字符来满足配置的密码强度要求。

如果你想要将电子邮件发送到在帐户创建过程中指定的电子邮件地址，则[`MailDefinition` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)非常有用。 `MailDefinition` 属性包括一系列子属性，用于定义有关构造的电子邮件的信息。 这些子属性包括 `Subject`、`Priority`、`IsBodyHtml`、`From`、`CC`和 `BodyFileName`等选项。 [`BodyFileName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)指向包含电子邮件正文的文本文件或 HTML 文件。 正文支持两个预定义占位符： `<%UserName%>` 和 `<%Password%>`。 如果 `BodyFileName` 文件中存在这些占位符，则会将其替换为刚刚创建的用户的名称和密码。

> [!NOTE]
> `CreateUserWizard` 控件的 `MailDefinition` 属性仅指定在创建新帐户时发送的电子邮件的详细信息。 它不包含有关如何实际发送电子邮件的详细信息（即，是使用 SMTP 服务器还是使用邮件投递目录、任何身份验证信息等）。 需要在 `Web.config`中的 `<system.net>` 部分定义这些低级别的详细信息。 有关这些配置设置以及从 ASP.NET 2.0 发送电子邮件的详细信息，请参阅 SystemNetMail.com 和我的文章中的[常见问题解答](http://www.systemnetmail.com/)，并[在 ASP.NET 2.0 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)。

### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>使用事件处理程序扩展 CreateUserWizard 的行为

CreateUserWizard 控件在其工作流中引发了许多事件。 例如，在访问者输入用户名、密码和其他相关信息并单击 "创建用户" 按钮后，CreateUserWizard 控件会引发其[`CreatingUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)。 如果在创建过程中出现问题，则激发[`CreateUserError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx);但是，如果已成功创建用户，则会引发[`CreatedUser` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)。 还有其他 CreateUserWizard 控件事件会引发，但这是三个最无关的控件事件。

在某些情况下，我们可能需要通过为相应的事件创建事件处理程序来利用 CreateUserWizard 工作流。 为了说明这一点，让我们来增强 `RegisterUser` CreateUserWizard 控件，以便在用户名和密码上包含一些自定义验证。 特别是，让我们来增强 CreateUserWizard，使用户名不能包含前导空格或尾随空格，用户名不能出现在密码中的任何位置。 简而言之，我们想要阻止他人创建用户名（如 "Scott"），或使用用户名/密码组合，如 "Scott" 和 "Scott. 1234"。

为实现此目的，我们将为 `CreatingUser` 事件创建事件处理程序，以执行额外的验证检查。 如果提供的数据无效，我们需要取消创建进程。 还需要将 "标签" Web 控件添加到页面，以显示一条消息，说明用户名或密码无效。 首先将 "标签" 控件添加到 CreateUserWizard 控件下方，并将其 `ID` 属性设置为 "`InvalidUserNameOrPasswordMessage`"，并将其 `ForeColor` 属性设置为 "`Red`"。 清除其 `Text` 属性，并将其 `EnableViewState` 和 `Visible` 属性设置为 False。

[!code-aspx[Main](creating-user-accounts-cs/samples/sample7.aspx)]

接下来，为 CreateUserWizard 控件的 `CreatingUser` 事件创建事件处理程序。 若要创建事件处理程序，请在设计器中选择控件，然后前往属性窗口。 在该处单击闪电形图标，然后双击相应的事件以创建事件处理程序。

将以下代码添加到 `CreatingUser` 事件处理程序中：

[!code-csharp[Main](creating-user-accounts-cs/samples/sample8.cs)]

请注意，在 CreateUserWizard 控件中输入的用户名和密码可分别通过其[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)和[`Password` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)提供。 在上述事件处理程序中使用这些属性来确定提供的用户名是否包含前导空格或尾随空格，以及是否在密码中找到用户名。 如果满足上述任一条件，则会在 "`InvalidUserNameOrPasswordMessage`" 标签中显示错误消息，并将事件处理程序的 `e.Cancel` 属性设置为 "`true`"。 如果 `e.Cancel` 设置为 `true`，CreateUserWizard 会将其工作流短路，从而有效地取消用户帐户创建过程。

图15显示了用户输入具有前导空格的用户名时的 `CreatingUserAccounts.aspx` 屏幕截图。

[不允许使用带前导空格或尾随空格的用户名 ![](creating-user-accounts-cs/_static/image44.png)](creating-user-accounts-cs/_static/image43.png)

**图 15**：不允许使用带有前导空格或尾随空格的用户名（[单击查看完全大小的图像](creating-user-accounts-cs/_static/image45.png)）

> [!NOTE]
> 在 *<a id="_msoanchor_11"></a>[存储其他用户信息](storing-additional-user-information-cs.md)* 教程中，我们将看到一个使用 CreateUserWizard 控件的 `CreatedUser` 事件的示例。

## <a name="summary"></a>Summary

`Membership` 类的 `CreateUser` 方法在成员身份框架中创建新的用户帐户。 它通过委托对配置的成员资格提供程序的调用来实现此目的。 在 `SqlMembershipProvider`的情况下，`CreateUser` 方法会向 `aspnet_Users` 和 `aspnet_Membership` 数据库表中添加一条记录。

尽管可以通过编程方式创建新用户帐户（如我们在步骤5中看到的那样），但使用 CreateUserWizard 控件可以更快、更简单。 此控件呈现一个多步骤用户界面，用于收集用户信息并在成员身份框架中创建新用户。 在涵盖的下面，此控件使用步骤5中所述的相同 `Membership.CreateUser` 方法，但控件创建用户界面、验证控件并响应用户帐户创建错误，而无需编写代码的舔。

此时，我们已准备好创建新用户帐户的功能。 但是，登录页仍将对照我们在第二个教程中指定的硬编码凭据进行验证。 在<a id="_msoanchor_12"> </a>[下一教程](validating-user-credentials-against-the-membership-user-store-cs.md)中，我们将更新 `Login.aspx` 以根据成员身份框架验证用户提供的凭据。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [`CreateUser` 技术文档](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard 控件概述](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [创建基于文件系统的站点地图提供程序](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [使用 ASP.NET 2.0 向导控件创建分步用户界面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [检查 ASP.NET 2.0 的站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [母版页和站点导航](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [已等待的 SQL 站点地图提供程序](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](creating-the-membership-schema-in-sql-server-cs.md)
> [下一页](validating-user-credentials-against-the-membership-user-store-cs.md)
