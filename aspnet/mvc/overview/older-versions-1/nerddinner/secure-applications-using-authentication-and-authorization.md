---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用身份验证和授权保护应用程序 |Microsoft Docs
author: microsoft
description: 步骤9显示了如何添加身份验证和授权以保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到网站才能创建 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486422"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>使用身份验证和授权保护应用程序

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第9步，其中演练了如何使用 ASP.NET MVC 1 构建一个小型的、完整的 web 应用程序。
> 
> 步骤9显示了如何添加身份验证和授权来保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到站点来创建新的就，并且只有托管晚餐的用户才能在以后编辑。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner 步骤9：身份验证和授权

现在，我们的 NerdDinner 应用程序授予访问该站点的任何人创建和编辑任何晚餐的详细信息的能力。 让我们对此进行更改，以使用户需要注册并登录到站点来创建新的就，并添加限制，以便仅托管晚餐的用户可以在以后编辑该限制。

为此，我们将使用身份验证和授权来确保应用程序的安全。

### <a name="understanding-authentication-and-authorization"></a>了解身份验证和授权

*身份验证*是指标识并验证访问应用程序的客户端标识的过程。 更简单地说，它与确定最终用户访问网站时的身份相关。 ASP.NET 支持通过多种方式对浏览器用户进行身份验证。 对于 Internet web 应用程序，使用最常用的身份验证方法称为 "Forms 身份验证"。 使用窗体身份验证，开发人员可以在其应用程序中创作 HTML 登录窗体，然后根据数据库或其他密码凭据存储来验证最终用户提交的用户名/密码。 如果用户名/密码组合正确，则开发人员可以要求 ASP.NET 发出加密的 HTTP cookie，以便在将来的请求中标识用户。 我们将通过 NerdDinner 应用程序使用 forms 身份验证。

*授权*是指确定经过身份验证的用户是否有权访问特定 URL/资源或执行某些操作的过程。 例如，在我们的 NerdDinner 应用程序中，我们想要授权只有登录的用户才能访问 */Dinners/Create* URL 并创建新的就。 我们还需要添加授权逻辑，以便仅托管晚餐的用户可以对其进行编辑，并拒绝对所有其他用户的编辑权限。

### <a name="forms-authentication-and-the-accountcontroller"></a>Forms 身份验证和 AccountController

创建新的 ASP.NET MVC 应用程序时，ASP.NET MVC 的默认 Visual Studio 项目模板会自动启用表单身份验证。 它还自动向项目添加预先生成的帐户登录页实现，这使得在站点内集成安全性变得非常简单。

"默认网站"。当访问用户的用户未通过身份验证时，它会在站点的右上角显示 "登录" 链接：

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

单击 "登录" 链接会将用户带到 */Account/LogOn* URL：

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

尚未注册的访问者可以通过单击 "注册" 链接来执行此操作，方法是单击 "注册" 链接（将其转到 */Account/Register* URL 并允许他们输入帐户详细信息）：

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

单击 "注册" 按钮将在 ASP.NET 成员资格系统中创建新用户，并使用 forms 身份验证对用户进行身份验证。

当用户登录时，站点。主节点将更改页面的右上方，以输出 "欢迎 [username]！" 消息并呈现一个 "注销" 链接，而不是 "登录" 链接。 单击 "注销" 链接会注销用户：

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

上述登录、注销和注册功能是在 AccountController 类中实现的，该类在创建项目时由 Visual Studio 添加到了项目中。 使用 \Views\Account 目录中的视图模板来实现 AccountController 的 UI：

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 类使用 ASP.NET Forms Authentication 系统颁发加密的身份验证 cookie，并使用 ASP.NET 成员资格 API 来存储和验证用户名/密码。 ASP.NET 成员资格 API 是可扩展的，可使用任何密码凭据存储。 ASP.NET 附带内置成员资格提供程序实现，用于在 SQL 数据库中或 Active Directory 中存储用户名/密码。

我们可以通过在项目根目录中打开 "web.config" 文件并查找其中 &lt;成员身份&gt; 部分来配置 NerdDinner 应用程序应使用的成员资格提供程序。 默认情况下，在创建项目时添加的 web.config 将注册 SQL 成员资格提供程序，并将其配置为使用一个名为 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 的连接字符串来指定数据库位置。

默认 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 连接字符串（在 web.config 文件的 &lt;connectionStrings&gt; 部分中指定）配置为使用 SQL Express。 它指向名为 "ASPNETDB.MDF" 的 SQL Express 数据库。MDF "的应用程序\_数据" 目录下。 如果此数据库在应用程序中首次使用成员资格 API 时不存在，ASP.NET 将自动创建数据库并在其中预配相应的成员资格数据库架构：

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

如果使用的不是 SQL Express，我们想要使用完全 SQL Server 实例（或连接到远程数据库），只需在 web.config 文件中更新 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 连接字符串，并确保相应的成员身份架构已添加到它指向的数据库。 可以在 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目录中运行 "aspnet\_regsql" 实用程序，以将相应的成员身份和其他 ASP.NET 应用程序服务的架构添加到数据库中。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>使用 [授权] 筛选器授权/Dinners/Create URL

我们无需编写任何代码即可为 NerdDinner 应用程序启用安全的身份验证和帐户管理实现。 用户可以向我们的应用程序注册新帐户，还可以登录/注销网站。

现在，我们可以将授权逻辑添加到应用程序，并使用访问者的身份验证状态和用户名控制其在站点中可以和不能执行的操作。 首先，让我们将授权逻辑添加到我们的 DinnersController 类的 "创建" 操作方法。 具体来说，我们将要求必须登录访问 */Dinners/Create* URL 的用户。 如果未登录，我们会将它们重定向到登录页，以便他们可以登录。

实现此逻辑非常简单。 我们只需将 [授权] 筛选器属性添加到创建操作方法，如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 支持创建 "操作筛选器" 的功能，该操作筛选器可用于实现可在操作方法中以声明方式应用的可重复使用的逻辑。 [授权] 筛选器是 ASP.NET MVC 提供的内置操作筛选器之一，它使开发人员能够以声明方式将授权规则应用到操作方法和控制器类。

如果应用时不带任何参数（如上所示），[授权] 筛选器将强制执行操作方法请求的用户必须登录–并且它会自动将浏览器重定向到登录 URL （如果它们不存在）。 执行此重定向时，最初请求的 URL 将作为 querystring 参数传递（例如：/Account/LogOn？ReturnUrl =% 2fDinners% 2fCreate）。 然后，在用户登录后，AccountController 会将用户重定向回最初请求的 URL。

[授权] 筛选器可以指定指定 "用户" 或 "角色" 属性的功能，该属性可用于要求用户同时登录到允许用户或允许的安全角色的列表。 例如，以下代码仅允许两个特定用户 "scottgu" 和 "billg" 访问/Dinners/Create URL：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

不过，在代码中嵌入特定的用户名往往会变得非常容易。 更好的方法是定义代码检查的高级 "角色"，然后使用数据库或 active directory 系统将用户映射到角色（使实际用户映射列表可以从代码外部存储）。 ASP.NET 包括内置角色管理 API 以及内置角色提供程序集（包括 SQL 和 Active Directory 的内置角色提供程序集），可帮助执行此用户/角色映射。 然后，我们可以更新代码，以便只允许特定 "管理员" 角色中的用户访问/Dinners/Create URL：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>创建就时使用 User.Identity.Name 属性

我们可以使用控制器基类上公开的 User.Identity.Name 属性来检索请求的当前已登录用户的用户名。

之前当我们实现了 Create （）操作方法的 HTTP POST 版本时，我们已将晚餐的 "HostedBy" 属性硬编码为静态字符串。 现在，我们可以更新此代码以改为使用 User.Identity.Name 属性，并为创建晚餐的主机自动添加 RSVP：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

由于我们已将 [授权] 特性添加到 Create （）方法，因此 ASP.NET MVC 可确保仅在用户访问/Dinners/Create URL 的用户登录到站点时才执行操作方法。 因此，User.Identity.Name 属性值将始终包含有效的用户名。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>编辑就时使用 User.Identity.Name 属性

现在，让我们添加一些限制用户的授权逻辑，使用户只能编辑他们自己所托管的就的属性。

为帮助实现此目标，我们首先将 "IsHostedBy （用户名）" 帮助器方法添加到晚餐对象（在前面构建的 Dinner.cs 分部类中）。 此帮助器方法返回 true 或 false，具体取决于所提供的用户名是否与晚餐 HostedBy 属性匹配，并封装对它们执行不区分大小写的字符串比较所需的逻辑：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

然后，将 [授权] 特性添加到 DinnersController 类中的 Edit （）操作方法。 这将确保用户必须登录才能请求 */Dinners/Edit/[id]* URL。

然后，可以将代码添加到使用 IsHostedBy （用户名）帮助程序方法的编辑方法，以验证登录的用户是否与晚餐主机匹配。 如果用户不是主机，将显示 "InvalidOwner" 视图并终止请求。 执行此操作的代码如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

然后，可以右键单击 \Views\Dinners 目录，然后选择 "添加&gt;视图" 菜单命令以创建新的 "InvalidOwner" 视图。 我们会在其中填充以下错误消息：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

现在，当用户尝试编辑他们不拥有的晚餐时，他们将收到一条错误消息：

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

对于控制器中的 Delete （）操作方法，我们可以重复相同的步骤，以锁定删除就的权限，并确保只有晚餐的主机才能将其删除。

### <a name="showinghiding-edit-and-delete-links"></a>显示/隐藏编辑和删除链接

我们将从详细信息 URL 链接到我们的 DinnersController 类的编辑和删除操作方法：

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

当前显示的是编辑和删除操作链接，而不考虑到详细信息 URL 的访问者是否是晚餐的主机。 让我们对此进行更改，以便仅在访问用户是晚餐的所有者时显示链接。

DinnersController 中的详细信息（）操作方法检索晚餐对象，然后将其作为模型对象传递到我们的视图模板：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

我们可以使用如下所示的 IsHostedBy （）帮助程序方法将视图模板更新为有条件地显示/隐藏 "编辑" 和 "删除" 链接：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>后续步骤

现在，让我们看看如何使用 AJAX 为经过身份验证的用户提供 RSVP for 就。

> [!div class="step-by-step"]
> [上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)
