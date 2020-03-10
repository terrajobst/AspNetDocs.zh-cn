---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
title: Forms 身份验证概述（C#） |Microsoft Docs
author: rick-anderson
description: 创建自定义路由
ms.author: riande
ms.date: 01/14/2008
ms.assetid: de2d65b9-aadc-42ba-abe1-4e87e66521a0
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 009c3f84e00d648ede4a15e530ceac2d23e01eec
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439664"
---
# <a name="an-overview-of-forms-authentication-c"></a>Forms 身份验证概述（C#）

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_CS.zip)或[下载 PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_cs.pdf)

> 在本教程中，我们将从单纯的讨论转变为实现;具体而言，我们将探讨如何实现窗体身份验证。 我们在本教程中开始构建的 web 应用程序将继续在后续教程中生成，因为我们从简单的 forms 身份验证转向成员身份和角色。
> 
> 有关此主题的详细信息，请参阅此视频：[在 ASP.NET 中使用基本 Forms 身份验证](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)。

## <a name="introduction"></a>简介

在[前面的教程](security-basics-and-asp-net-support-cs.md)中，我们讨论了 ASP.NET 提供的各种身份验证、授权和用户帐户选项。 在本教程中，我们将从单纯的讨论转变为实现;具体而言，我们将探讨如何实现窗体身份验证。 我们在本教程中开始构建的 web 应用程序将继续在后续教程中生成，因为我们从简单的 forms 身份验证转向成员身份和角色。

本教程首先深入了解 forms 身份验证工作流，这是我们在上一教程中讨论过的主题。 接下来，我们将创建 ASP.NET 网站，通过该网站演示 forms 身份验证的概念。 接下来，我们将配置站点以使用 forms 身份验证，创建一个简单的登录页，并查看如何在代码中确定是否对用户进行了身份验证，如果用户已登录，则为。

了解 forms 身份验证工作流，在 web 应用程序中启用它以及创建登录和注销页是构建支持用户帐户并通过网页对用户进行身份验证的 ASP.NET 应用程序的关键步骤。 因此，因为这些教程彼此独立，所以，即使你已在过去的项目中配置了窗体身份验证，我们也鼓励你完全完成本教程，再继续学习下一个教程。

## <a name="understanding-the-forms-authentication-workflow"></a>了解 Forms 身份验证工作流

当 ASP.NET 运行时处理对 ASP.NET 资源（如 ASP.NET 页或 ASP.NET Web 服务）的请求时，该请求会在其生命周期内引发大量事件。 在请求的开始和结束时引发的事件、对请求进行身份验证和授权时引发的事件、在发生未经处理的异常的情况下引发的事件等。 若要查看完整的事件列表，请参阅[HttpApplication 对象的事件](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)。

*HTTP 模块*是托管类，其代码是为了响应请求生命周期中的特定事件而执行的。 ASP.NET 附带了多个 HTTP 模块，这些模块在幕后执行基本任务。 与我们的讨论特别相关的两个内置 HTTP 模块：

- **[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** –通过检查 forms 身份验证票证（通常包含在用户的 cookie 集合中）对用户进行身份验证。 如果不存在 forms 身份验证票证，则用户为 anonymous。
- **[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** –确定当前用户是否有权访问所请求的 URL。 此模块通过咨询应用程序配置文件中指定的授权规则来确定授权机构。 ASP.NET 还包括通过咨询请求的文件 Acl 来确定权威的[`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) 。

`FormsAuthenticationModule` 在 `UrlAuthorizationModule` （和 `FileAuthorizationModule`）执行之前尝试对用户进行身份验证。 如果发出请求的用户无权访问请求的资源，则该授权模块将终止请求并返回[HTTP 401 未经授权](http://www.checkupdown.com/status/E401.html)状态。 在 Windows 身份验证方案中，将 HTTP 401 状态返回到浏览器。 此状态代码将导致浏览器通过模式对话框提示用户输入其凭据。 然而，使用 forms 身份验证时，不会将 HTTP 401 的未经授权状态发送到浏览器，因为 FormsAuthenticationModule 会检测到此状态，并将其修改为将用户重定向到登录页（通过[HTTP 302 重定向](http://www.checkupdown.com/status/E302.html)状态）。

登录页的责任是确定用户的凭据是否有效，如果是，则创建 forms 身份验证票证，并将用户重定向回他们尝试访问的页面。 身份验证票证包含在对网站页面的后续请求中，`FormsAuthenticationModule` 使用该票证来标识用户。

![Forms 身份验证工作流](an-overview-of-forms-authentication-cs/_static/image1.png)

**图 1**： Forms 身份验证工作流

### <a name="remembering-the-authentication-ticket-across-page-visits"></a>记住跨页面访问的身份验证票证

登录后，必须将 forms 身份验证票证发送回每个请求的 web 服务器，以便用户在浏览站点时仍保持登录。 通常通过将身份验证票证置于用户的 cookie 集合来完成此操作。 [Cookie](http://en.wikipedia.org/wiki/HTTP_cookie)是位于用户计算机上的小文本文件，并在每个请求的 HTTP 标头中传输到创建该 cookie 的网站。 因此，创建 forms 身份验证票证并将其存储在浏览器的 cookie 中后，每次访问该站点时，都会随请求一起发送身份验证票证，从而标识用户。

Cookie 的一个方面是其过期时间，即浏览器丢弃 cookie 的日期和时间。 当 forms 身份验证 cookie 过期时，用户将无法再进行身份验证，因此会成为匿名用户。 当用户从公共终端访问时，他们可能希望其身份验证票证在关闭浏览器时过期。 但从家里访问时，相同的用户可能希望在浏览器重新启动时记住身份验证票证，以便在每次访问站点时无需重新登录。 此决定通常由用户在登录页上的 "记住我" 复选框的形式进行。 在步骤3中，我们将检查如何在登录页中执行 "记住我" 复选框。 以下教程详细介绍了身份验证票证超时设置。

> [!NOTE]
> 用于登录到网站的用户代理可能不支持 cookie。 在这种情况下，ASP.NET 可以使用无 cookie forms 身份验证票证。 在此模式下，身份验证票证编码到 URL 中。 在下一教程中，我们将介绍如何使用无 cookie 身份验证票证以及如何创建和管理它们。

### <a name="the-scope-of-forms-authentication"></a>Forms 身份验证的范围

`FormsAuthenticationModule` 是托管代码，是 ASP.NET 运行时的一部分。 在 Microsoft [Internet Information Services （iis）](https://www.iis.net/) web 服务器版本7之前，IIS 的 HTTP 管道与 ASP.NET 运行时的管道之间存在不同的障碍。 简而言之，在 IIS 6 及更早版本中，`FormsAuthenticationModule` 仅在将请求从 IIS 委托给 ASP.NET 运行时时执行。 默认情况下，IIS 处理静态内容本身（如 HTML 页面和 CSS 文件），并且仅当请求扩展名为 .aspx、.asmx 或. foo.ashx 的页面时，才会向 ASP.NET 运行时发出请求。

但是，IIS 7 允许集成的 IIS 和 ASP.NET 管道。 使用几个配置设置，你可以设置 IIS 7 来为*所有*请求调用 FormsAuthenticationModule。 此外，借助 IIS 7，你可以为任何类型的文件定义 URL 授权规则。 有关详细信息，请参阅[IIS6 和 Iis7 安全性之间的更改](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above)、 [Web 平台安全](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)以及[了解 IIS7 URL 授权](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)。

简短故事：在 IIS 7 之前的版本中，你只能使用窗体身份验证来保护 ASP.NET 运行时处理的资源。 同样，URL 授权规则仅适用于 ASP.NET 运行时所处理的资源。 但在 IIS 7 中，可以将 FormsAuthenticationModule 和 UrlAuthorizationModule 集成到 IIS 的 HTTP 管道中，从而将此功能扩展到所有请求。

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>步骤1：创建本教程系列的 ASP.NET 网站

为了满足最广泛的受众的需要，我们将在本系列文章中生成的 ASP.NET 网站将通过 Microsoft 的 Visual Studio 2008 （ [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)）的免费版本来创建。 我们将在[Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx)数据库中实施 `SqlMembershipProvider` 的用户存储。 如果你使用的是 Visual Studio 2005 或不同版本的 Visual Studio 2008 或 SQL Server，别担心，这些步骤几乎完全相同，并且任何不重要的差异都将被指出。

> [!NOTE]
> 每个教程中使用的演示 web 应用程序均可供下载。 此下载的应用程序是通过面向 .NET Framework 版本3.5 的 Visual Web Developer 2008 创建的。 由于应用程序针对的是 .NET 3.5，因此它的 Web.config 文件包括附加的、3.5 特定的配置元素。 很长一段时间，如果你尚未在计算机上安装 .NET 3.5，下载的 web 应用程序将无法运行，而无需先从 web.config 中删除3.5 特定标记。

在我们可以配置 forms 身份验证之前，我们首先需要一个 ASP.NET 网站。 首先，创建新的基于文件系统的 ASP.NET 网站。 若要实现此目的，请启动 Visual Web Developer，然后在 "文件" 菜单中选择 "新建网站"，并显示 "新建网站" 对话框。 选择 ASP.NET 网站模板，将 "位置" 下拉列表设置为 "文件系统"，选择要放置该网站的文件夹，并将语言设置为C#。 这将创建一个新网站，其中包含默认的 .aspx ASP.NET 页、一个应用\_Data 文件夹和一个 web.config 文件。

> [!NOTE]
> Visual Studio 支持以下两种模式的项目管理：网站项目和 Web 应用程序项目。 网站项目缺少项目文件，而 Web 应用程序项目在 Visual Studio .NET 2002/2003 中模拟项目体系结构–它们包含一个项目文件，并将项目的源代码编译到一个程序集中，该程序集放置在/bin 文件夹中。 仅当 Web 应用程序项目模型被引入 Service Pack 1 时，Visual Studio 2005 最初才支持网站项目;Visual Studio 2008 提供两个项目模型。 但是，Visual Web Developer 2005 和2008版本仅支持网站项目。 我将使用网站项目模型。 如果你使用的是非速成版，并且想要使用[Web 应用程序项目模型](https://msdn.microsoft.com/library/aa730880%28vs.80%29.aspx)，则可以随意执行此操作，但请注意，你在屏幕上看到的内容和所显示的步骤以及这些教程中提供的说明之间可能存在一些差异。

[![创建基于文件系统的新网站](an-overview-of-forms-authentication-cs/_static/image3.png)](an-overview-of-forms-authentication-cs/_static/image2.png)

**图 2**：创建新的基于文件系统的网站（[单击查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image4.png)）

### <a name="adding-a-master-page"></a>添加母版页

接下来，将新的母版页添加到名为 "master" 的根目录中的站点。 [母版页](https://msdn.microsoft.com/library/wtxbf3hh.aspx)使页面开发人员能够定义可应用于 ASP.NET 页面的站点范围模板。 母版页的主要优点是，可以在单个位置定义站点的总体外观，从而可以轻松地更新或调整站点的布局。

[![将名为 "网站" 的母版页添加到网站](an-overview-of-forms-authentication-cs/_static/image6.png)](an-overview-of-forms-authentication-cs/_static/image5.png)

**图 3**：将名为 "网站" 的母版页添加到网站（[单击查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image7.png)）

在此母版页中定义站点范围的页面布局。 您可以使用设计视图并添加所需的任何布局或 Web 控件，也可以手动在源视图中添加标记。 我将我的母版页布局构造为模拟在 ASP.NET 2.0 教程系列中用于 *[处理数据](../../data-access/index.md)* 的布局（参见图4）。 母版页使用[级联样式表](http://www.w3schools.com/css/default.asp)，通过在文件样式 .css 中定义的 css 设置来定位和设置样式。 css （包含在本教程的关联下载中）。 虽然无法从下面显示的标记中进行说明，但定义了 CSS 规则，以便将导航 &lt;div&gt;的内容绝对定位，使其显示在左侧，并且固定宽度为200像素。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample1.aspx)]

母版页既定义静态页面布局，也定义可由使用母版页的 ASP.NET 页面编辑的区域。 这些内容可编辑区域由 `ContentPlaceHolder` 控件指示，可在内容 &lt;div&gt;中查看。 母版页有单个 `ContentPlaceHolder` （MainContent），但母版页的可能有多个 Contentplaceholder。

在上面输入的标记中，切换到设计视图显示母版页的布局。 使用此母版页的任何 ASP.NET 页面都将具有此统一布局，并能够指定 `MainContent` 区域的标记。

[使用 "设计" 视图查看母版页 ![](an-overview-of-forms-authentication-cs/_static/image9.png)](an-overview-of-forms-authentication-cs/_static/image8.png)

**图 4**：通过设计视图（[单击查看全尺寸图像](an-overview-of-forms-authentication-cs/_static/image10.png)）查看的母版页

### <a name="creating-content-pages"></a>创建内容页

此时，我们的网站中有一个 default.aspx 页，但它不使用我们刚刚创建的母版页。 尽管可以对网页的声明性标记进行操作以使用母版页，但如果该页不包含任何内容，则只需删除页面并将其重新添加到项目，并指定要使用的母版页，就更容易。 因此，请通过从项目中删除 default.aspx 来开始。

接下来，右键单击 "解决方案资源管理器中的项目名称，然后选择添加一个名为" default.aspx "的新 Web 窗体。 此时，选中 "选择母版页" 复选框，然后从列表中选择 "网站母版页"。

[![添加新的 default.aspx 页面选择以选择母版页](an-overview-of-forms-authentication-cs/_static/image12.png)](an-overview-of-forms-authentication-cs/_static/image11.png)

**图 5**：添加新的 default.aspx 页面选择以选择母版页（[单击以查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image13.png)）

![使用 "网站母版页" 母版页](an-overview-of-forms-authentication-cs/_static/image14.png)

**图 6**：使用网站母版页

> [!NOTE]
> 如果使用的是 Web 应用程序项目模型，则 "添加新项" 对话框不包含 "选择母版页" 复选框。 相反，您需要添加类型为 "Web 内容窗体" 的项。 选择 "Web 内容表单" 选项并单击 "添加" 后，Visual Studio 将显示图6中所示的相同的 "选择 Master" 对话框。

新的 default.aspx 页的声明性标记只包含一个 @Page 指令，该指令指定母版页文件的路径和母版页的 MainContent ContentPlaceHolder 的内容控件。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample2.aspx)]

现在，请将 default.aspx 留空。 我们将在本教程的后面部分返回内容以添加内容。

> [!NOTE]
> 母版页包含一个用于菜单或其他导航界面的部分。 在将来的教程中，我们将创建此类接口。

## <a name="step-2-enabling-forms-authentication"></a>步骤2：启用窗体身份验证

创建 ASP.NET 网站后，接下来的任务是启用表单身份验证。 应用程序的身份验证配置是通过 web.config 中的[`<authentication>` 元素](https://msdn.microsoft.com/library/532aee0e.aspx)指定的。`<authentication>` 元素包含名为 mode 的单个属性，该属性指定应用程序使用的身份验证模型。 此属性可以具有以下四个值之一：

- **Windows** –如前面的教程中所述，当应用程序使用 Windows 身份验证时，web 服务器负责对访问者进行身份验证，这通常是通过基本、摘要式或集成 Windows 身份验证来完成的。
- **Forms**–用户通过网页上的窗体进行身份验证。
- **Passport**–使用 Microsoft 的 Passport 网络对用户进行身份验证。
- **无**-不使用身份验证模型;所有访问者都是匿名的。

默认情况下，ASP.NET 应用程序使用 Windows 身份验证。 若要将身份验证类型更改为窗体身份验证，则需要将 `<authentication>` 元素的 mode 属性修改为 Forms。

如果你的项目尚未包含 web.config 文件，请通过在解决方案资源管理器中右键单击项目名称，选择 "添加新项"，然后添加 Web 配置文件来添加一个。

[![如果你的项目尚未包含 web.config，请立即添加](an-overview-of-forms-authentication-cs/_static/image16.png)](an-overview-of-forms-authentication-cs/_static/image15.png)

**图 7**：如果你的项目尚未包含 web.config，请立即添加它（[单击以查看完全大小的映像](an-overview-of-forms-authentication-cs/_static/image17.png)）

接下来，找到 `<authentication>` 元素，并将其更新为使用 forms 身份验证。 此更改之后，Web.config 文件的标记应如下所示：

[!code-xml[Main](an-overview-of-forms-authentication-cs/samples/sample3.xml)]

> [!NOTE]
> 由于 web.config 是一个 XML 文件，因此大小写很重要。 请确保将 mode 属性设置为 Forms，并使用大写 "F"。 如果使用不同的大小写，如 "forms"，则在通过浏览器访问站点时，会收到配置错误。

`<authentication>` 元素可以有选择性地包含 `<forms>` 子元素，其中包含特定于窗体身份验证的设置。 现在，让我们使用默认的 forms 身份验证设置。 在下一教程中，我们将更详细地探讨 `<forms>` 的子元素。

## <a name="step-3-building-the-login-page"></a>步骤3：生成登录页

为了支持窗体身份验证，我们的网站需要登录页。 如 "了解 Forms 身份验证工作流" 一节中所述，如果用户尝试访问无权查看的页，则 `FormsAuthenticationModule` 会自动将用户重定向到登录页。 还会有 ASP.NET 的 Web 控件，这些控件将向匿名用户显示登录页的链接。 这来了吗了 "登录" 页的 URL 是什么？

默认情况下，forms 身份验证系统要求登录页命名为 default.aspx，并放置在 web 应用程序的根目录中。 如果要使用不同的登录页 URL，可以通过在 web.config 中指定该 URL 来执行此操作。在后续教程中，我们将了解如何执行此操作。

登录页有三个责任：

1. 提供允许访问者输入其凭据的接口。
2. 确定提交的凭据是否有效。
3. 通过创建 forms 身份验证票证来 "登录" 用户。

### <a name="creating-the-login-pages-user-interface"></a>创建登录页的用户界面

首先，让我们开始学习第一个任务。 将新的 "ASP.NET" 页添加到名为 "Login" 的网站的根目录中，并将其与 "网站母版页" 母版页关联。

[![添加名为 ASP.NET 的新的 "](an-overview-of-forms-authentication-cs/_static/image19.png)](an-overview-of-forms-authentication-cs/_static/image18.png)

**图 8**：添加名为 ASP.NET 的新 "" 页（[单击以查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image20.png)）

典型的登录页接口包括两个文本框-一个用于用户名，一个用于其密码–一个用于提交窗体的按钮。 网站往往包含 "记住我" 复选框，如果选中，则会在浏览器重新启动时保持生成的身份验证票证。

将两个文本框添加到 Login，并将其 `ID` 属性分别设置为用户名和密码。 同时，将密码的 `TextMode` 属性设置为 Password。 接下来，添加 CheckBox 控件，将其 `ID` 属性设置为 RememberMe，并将其 `Text` 属性设置为 "记住我"。 随后，添加一个名为 "LoginButton" 的按钮，其 `Text` 属性设置为 "Login"。 最后，添加一个标签 Web 控件，并将其 `ID` 属性设置为 InvalidCredentialsMessage，其 `Text` 属性设置为 "你的用户名或密码无效。 请重试。 "，其 `ForeColor` 属性设置为 Red，其 `Visible` 属性设置为 False。

此时，屏幕应类似于图9中的屏幕截图，页面的声明性语法应该如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample4.aspx)]

[![登录页面包含两个文本框、复选框、按钮和标签](an-overview-of-forms-authentication-cs/_static/image22.png)](an-overview-of-forms-authentication-cs/_static/image21.png)

**图 9**：登录页面包含两个文本框：复选框、按钮和标签（[单击以查看完全尺寸的图像](an-overview-of-forms-authentication-cs/_static/image23.png)）

最后，为 LoginButton 的单击事件创建事件处理程序。 在设计器中，只需双击按钮控件即可创建此事件处理程序。

### <a name="determining-if-the-supplied-credentials-are-valid"></a>确定所提供的凭据是否有效

现在，我们需要在按钮的单击事件处理程序中实现任务2–确定所提供的凭据是否有效。 要执行此操作，需要有一个保存所有用户凭据的用户存储区，以便我们可以确定所提供的凭据是否与任何已知凭据匹配。

在 ASP.NET 2.0 之前，开发人员负责实现其自己的用户存储和编写代码，以针对商店验证提供的凭据。 大多数开发人员会在数据库中实现用户存储，并创建一个名为 "用户"、"用户名"、"密码"、"电子邮件"、"LastLoginDate" 等列的表。 此表中的每个用户帐户都有一条记录。 验证用户提供的凭据将涉及在数据库中查询匹配的用户名，然后确保数据库中的密码对应为提供的密码。

使用 ASP.NET 2.0，开发人员应使用成员资格提供程序之一来管理用户存储区。 在本系列教程中，我们将使用 SqlMembershipProvider，它使用用户存储的 SQL Server 数据库。 当使用 SqlMembershipProvider 时，我们需要实现特定的数据库架构，其中包含提供程序所需的表、视图和存储过程。 我们将在 SQL Server 教程中的***创建成员身份架构***中检查如何实现此架构。 使用成员资格提供程序时，验证用户的凭据非常简单，只调用[成员身份类](https://msdn.microsoft.com/library/system.web.security.membership.aspx)的[system.web.security.membership.validateuser （*username*， *password*）方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)，该方法返回一个布尔值，指示*用户名*和*密码*组合的有效性。 由于我们尚未实现 SqlMembershipProvider 的用户存储，我们目前无法使用成员身份类的 System.web.security.membership.validateuser 方法。

不要花费时间来构建自己的自定义用户数据库表（一旦我们实现了 SqlMembershipProvider，就会过时），而是在登录页本身中对有效凭据进行硬编码。 在 LoginButton 的 Click 事件处理程序中，添加以下代码：

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample5.cs)]

如您所见，有三个有效的用户帐户– Scott、Jisun 和 Sam，这三个都具有相同的密码（"密码"）。 此代码循环通过用户和密码阵列查找有效的用户名和密码匹配。 如果用户名和密码都有效，则需要登录用户，然后将其重定向到相应的页面。 如果凭据无效，则显示 "InvalidCredentialsMessage" 标签。

当用户输入有效凭据时，我曾提到过，它们将被重定向到 "适当的页"。 什么是合适的页面？ 请记住，当用户访问他们无权查看的页面时，FormsAuthenticationModule 会自动将其重定向到登录页。 在此过程中，它通过 ReturnUrl 参数在查询字符串中包含请求的 URL。 也就是说，如果用户试图访问 ProtectedPage，但没有授权，则 FormsAuthenticationModule 会将其重定向到：

Login.aspx?ReturnUrl=ProtectedPage.aspx

成功登录后，应将用户重定向回 ProtectedPage。 或者，用户可以访问他们自己的 volition 上的登录页面。 在这种情况下，在用户登录后，应将其发送到根文件夹的 default.aspx 页。

### <a name="logging-in-the-user"></a>用户登录

假设提供的凭据有效，我们需要创建 forms 身份验证票证，从而将用户登录到站点。 [System.web 命名空间](https://msdn.microsoft.com/library/system.web.security.aspx)中的[FormsAuthentication 类](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx)提供了用于通过 forms 身份验证系统登录和注销用户的各种方法。 尽管 FormsAuthentication 类中有几种方法，但我们在此方面感兴趣的三个方法是：

- [GetAuthCookie （*username*， *persistCookie*）](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) –为提供的名称*用户名*创建 forms 身份验证票证。 接下来，此方法创建并返回一个 HttpCookie 对象，该对象保存身份验证票证的内容。 如果*persistCookie*为 true，则将创建持久性 cookie。
- [SetAuthCookie （*username*， *persistCookie*）](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) –调用 GetAuthCookie （*username*， *persistCookie*）方法来生成 forms 身份验证 cookie。 然后，此方法将 GetAuthCookie 返回的 cookie 添加到 Cookie 集合（假定使用的是基于 cookie 的窗体身份验证; 否则，此方法将调用一个用于处理无 cookie 票证逻辑的内部类）。
- [Formsauthentication.redirectfromloginpage （*username*， *persistCookie*）](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) –此方法调用 SetAuthCookie （*username*， *persistCookie*），然后将用户重定向到相应的页面。

如果需要在将 cookie 写入 Cookie 集合之前修改身份验证票证，则 GetAuthCookie 非常方便。 如果要创建 forms 身份验证票证并将其添加到 Cookie 集合，但不希望将用户重定向到适当的页面，SetAuthCookie 将非常有用。 也许你想要将它们保留在登录页上，或将其发送到某个备用页。

由于我们要登录用户并将其重定向到相应的页面，因此，我们将使用 Formsauthentication.redirectfromloginpage。 更新 LoginButton 的 Click 事件处理程序，并将两个注释的 TODO 行替换为以下代码行：

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked);

创建 forms 身份验证票证时，我们将使用 "用户名" 文本框的 Text 属性作为 forms 身份验证票证*用户名*参数，并使用*PersistCookie*参数的 RememberMe 复选框的选中状态。

若要测试登录页，请在浏览器中访问它。 首先输入无效凭据，如用户名 "上场" 和密码 "错误"。 单击 "登录" 按钮时，将发生回发并显示 InvalidCredentialsMessage 标签。

[![在输入无效凭据时显示 InvalidCredentialsMessage 标签](an-overview-of-forms-authentication-cs/_static/image25.png)](an-overview-of-forms-authentication-cs/_static/image24.png)

**图 10**：输入无效凭据时显示 InvalidCredentialsMessage 标签（[单击以查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image26.png)）

接下来，输入有效的凭据，并单击 "登录" 按钮。 这次回发发生时，会创建一个 forms 身份验证票证，并自动重定向回默认 .aspx。 此时，您已登录到该网站，但没有显示表明您当前登录的视觉提示。 在步骤4中，我们将了解如何以编程方式确定用户是否已登录，以及如何识别访问页面的用户。

步骤5检查从网站注销用户的方法。

### <a name="securing-the-login-page"></a>保护登录页

当用户输入其凭据并提交登录页窗体时，凭据（包括她的密码）将通过 Internet 以*纯文本*形式传输到 web 服务器。 这意味着任何黑客探查网络流量都能看到用户名和密码。 若要防止出现这种情况，必须使用[安全套接字层（SSL）](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)加密网络流量。 这将确保在 web 服务器接收到浏览器之前，会对凭据（以及整页的 HTML 标记）进行加密。

除非你的网站包含敏感信息，否则你只需在登录页和其他页面上使用 SSL，否则，用户的密码将以纯文本格式通过网络发送。 你无需担心保护 forms 身份验证票证，因为默认情况下，它已进行加密和数字签名（以防篡改）。 以下教程提供了有关 forms 身份验证票证安全性的更全面讨论。

> [!NOTE]
> 许多金融和医疗网站配置为在经过身份验证的用户可访问的*所有*页面上使用 SSL。 如果要构建此类网站，可以配置 forms 身份验证系统，以便仅通过安全连接传输表单身份验证票证。 我们将在下一教程的 *[Forms 身份验证配置和高级主题](forms-authentication-configuration-and-advanced-topics-cs.md)* 中查看各种 forms 身份验证配置选项。

## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>步骤4：检测已验证身份的访问者并确定其身份

此时，我们已启用 forms 身份验证并创建了一个基本的登录页面，但我们仍要检查如何确定用户是否已通过身份验证或匿名身份验证。 在某些情况下，根据经过身份验证的用户还是匿名用户访问页面，我们可能希望显示不同的数据或信息。 而且，我们经常需要知道已经过身份验证的用户的身份。

接下来，我们将扩展现有的 default.aspx 页，以说明这些方法。 在 default.aspx 中，添加两个 Panel 控件，一个名为 AuthenticatedMessagePanel，另一个命名为 AnonymousMessagePanel。 在第一个面板中添加名为 "WelcomeBackMessage" 的 "标签" 控件。 在第二个面板中添加超链接控件，将其 Text 属性设置为 "登录"，并将其 NavigateUrl 属性设置为 "~/Login.aspx"。 此时，.aspx 的声明性标记应如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample6.aspx)]

正如你现在可能已猜到的那样，这里的思路是只向经过身份验证的访客显示 AuthenticatedMessagePanel，而只向匿名访人显示 AnonymousMessagePanel。 若要实现此目的，我们需要根据用户是否登录来设置这些面板的可见属性。

[IsAuthenticated 属性](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx)将返回一个布尔值，该值指示请求是否已经过身份验证。 将以下代码输入到页面\_Load 事件处理程序代码：

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample7.cs)]

将此代码放在一起后，通过浏览器访问 default.aspx。 假设你尚未登录，则会看到一个指向登录页的链接（参见图11）。 单击此链接并登录到网站。 正如我们在第3步中看到的那样，在输入凭据后，你将返回到 default.aspx，但此时该页显示 "欢迎回来！" 消息（请参阅图12）。

![匿名访问时，将显示 "登录" 链接](an-overview-of-forms-authentication-cs/_static/image27.png)

**图 11**：匿名访问时，将显示 "登录" 链接

![经过身份验证的用户将显示在](an-overview-of-forms-authentication-cs/_static/image28.png)

**图 12**：经过身份验证的用户显示为 "欢迎回来！" 消息

我们可以通过[HttpContext 对象](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)的[用户属性](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)来确定当前登录的用户的标识。 HttpContext 对象表示当前请求的相关信息，作为响应、请求和会话等常见 ASP.NET 对象的宿主。 用户属性表示当前 HTTP 请求的安全上下文，并实现[IPrincipal 接口](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)。

用户属性由 FormsAuthenticationModule 设置。 具体而言，当 FormsAuthenticationModule 在传入请求中找到 forms 身份验证票证时，它将创建一个新的 GenericPrincipal 对象，并将其分配给用户属性。

主体对象（如 GenericPrincipal）提供有关用户的标识及其所属的角色的信息。 IPrincipal 接口定义了两个成员：

- [IsInRole （](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx)角色标识）–一种方法，该方法返回一个布尔值，指示主体是否属于指定的角色。
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) –返回实现[IIdentity 接口](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)的对象的属性。 IIdentity 接口定义了三个属性： [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx)、 [IsAuthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)和[Name](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)。

我们可以使用以下代码确定当前访问者的名称：

string currentUsersName = User.Identity.Name;

使用窗体身份验证时，将为 GenericPrincipal 的标识属性创建一个[FormsIdentity 对象](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx)。 FormsIdentity 类始终返回 AuthenticationType 属性的字符串 "Forms"，并为其 IsAuthenticated 属性返回 true。 Name 属性返回创建 forms 身份验证票证时指定的用户名。 除了这三个属性，FormsIdentity 还包括通过其[票证属性](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)访问基础身份验证票证。 Ticket 属性返回类型为[FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)的对象，该对象的属性如过期、IsPersistent、IssueDate、Name 等。

需要注意的一点是，在 FormsAuthentication. GetAuthCookie （*username*， *PersistCookie*）、FormsAuthentication.*SetAuthCookie （Username，* *persistCookie*）和 FormsAuthentication （*username*， *formsauthentication.redirectfromloginpage*）方法中指定的*username*参数与 persistCookie 返回的值相同。 此外，通过将 User. Identity 强制转换为 FormsIdentity 对象，然后访问票证属性，可以获得通过这些方法创建的身份验证票证：

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample8.cs)]

让我们在 default.aspx 中提供更多个性化的消息。 \_Load 事件处理程序更新页面，使 "WelcomeBackMessage" 标签的 "Text" 属性分配有字符串 "欢迎回来， *username*！"

WelcomeBackMessage.Text = "Welcome back, " + User.Identity.Name + "!";

图13显示了此修改（以用户 Scott 身份登录时）的影响。

![欢迎消息包含当前登录的用户的名称](an-overview-of-forms-authentication-cs/_static/image29.png)

**图 13**：欢迎消息包含当前登录的用户的名称

### <a name="using-the-loginview-and-loginname-controls"></a>使用登录视图和 LoginName 控件

向经过身份验证的用户和匿名用户显示不同的内容是一个常见的要求;因此显示当前登录的用户的名称。 出于此原因，ASP.NET 包含两个 Web 控件，它们提供了图13中所示的相同功能，但不需要编写一行代码。

[登录视图控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)是一个基于模板的 Web 控件，可以轻松地向经过身份验证的用户和匿名用户显示不同的数据。 登录视图包括两个预定义的模板：

- AnonymousTemplate –添加到此模板的任何标记只显示给匿名访问者。
- LoggedInTemplate –仅向经过身份验证的用户显示此模板的标记。

接下来，将登录视图控件添加到站点的母版页。 不过，我们不只添加登录视图控件，而是添加一个新的 ContentPlaceHolder 控件，然后将登录视图控件放在该新 ContentPlaceHolder 中。 此决策的根本就会变得显而易见。

> [!NOTE]
> 除了 AnonymousTemplate 和 LoggedInTemplate 外，登录视图控件还可以包括特定于角色的模板。 特定于角色的模板仅向属于指定角色的用户显示标记。 在将来的教程中，我们将检查登录视图控件的基于角色的功能。

首先，将名为 LoginContent 的 ContentPlaceHolder 添加到导航 &lt;div&gt; 元素内的母版页中。 只需将 "ContentPlaceHolder" 控件从 "工具箱" 拖到 "源" 视图中，将生成的标记放置在 "TODO： Menu ..."全文.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample9.aspx)]

接下来，在 LoginContent ContentPlaceHolder 中添加登录视图控件。 放入母版页的 ContentPlaceHolder 控件中的内容被视为 ContentPlaceHolder 的*默认内容*。 也就是说，使用此母版页的 ASP.NET 页面可以为每个 ContentPlaceHolder 指定各自的内容，也可以使用母版页的默认内容。

登录视图和其他与登录相关的控件位于工具箱的 "登录" 选项卡中。

![工具箱中的登录视图控件](an-overview-of-forms-authentication-cs/_static/image30.png)

**图 14**：工具箱中的登录视图控件

接下来，将两个 &lt;br/&gt; 元素添加到登录视图控件之后，但仍在 ContentPlaceHolder 中。 此时，导航 &lt;div&gt; 元素的标记应如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample10.aspx)]

可以从设计器或声明性标记定义登录视图的模板。 在 Visual Studio 的设计器中，展开登录视图的智能标记，该标记将在下拉列表中列出已配置的模板。 在 AnonymousTemplate 中输入文本 "Hello，stranger";接下来，添加一个超链接控件，并将其 Text 和 NavigateUrl 属性分别设置为 "登录" 和 "~/Login.aspx"。

配置 AnonymousTemplate 后，请切换到 LoggedInTemplate 并输入文本 "欢迎回来"。 然后，将 "LoginName" 控件从 "工具箱" 拖动到 "LoggedInTemplate"，将其置于 "欢迎回来" 文本后。 如名称所示， [LoginName 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx)将显示当前登录的用户的名称。 在内部，LoginName 控件仅输出 User.Identity.Name 属性

在对登录视图的模板进行这些添加后，标记应如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample11.aspx)]

在站点的这种情况下，我们网站中的每一页都将显示不同的消息，具体取决于是否对用户进行了身份验证。 图15显示了通过用户 Jisun 通过浏览器访问的 default.aspx 页。 "欢迎回来，Jisun" 消息重复两次：一次在左侧的母版页导航部分中（通过我们刚刚添加的登录视图控件），一次在默认 .aspx 的内容区域（通过 Panel 控件和编程逻辑）。

![登录视图控件显示](an-overview-of-forms-authentication-cs/_static/image31.png)

**图 15**：登录视图控件显示 "欢迎回来，Jisun"。

由于我们已将登录视图添加到母版页，因此它可能会显示在我们的站点上的每一页中。 但是，可能存在不希望显示此消息的网页。 此类页面是登录页面，因为到登录页面的链接似乎不存在。 由于我们将登录视图控件放在母版页的 ContentPlaceHolder 中，因此我们可以在内容页中覆盖此默认标记。 打开 "登录 .aspx" 并前往设计器。 由于我们未在 ContentPlaceHolder 中为 LoginContent 显式定义 Content-type .aspx 中的内容控件，因此登录页面将显示此 ContentPlaceHolder 的母版页默认标记。 可以通过设计器看到此情况-LoginContent ContentPlaceHolder 显示默认标记（登录视图控件）。

[![登录页显示母版页的 LoginContent ContentPlaceHolder 的默认内容。](an-overview-of-forms-authentication-cs/_static/image33.png)](an-overview-of-forms-authentication-cs/_static/image32.png)

**图 16**：登录页显示母版页的 LoginContent ContentPlaceHolder 的默认内容（[单击以查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image34.png)）

若要重写 LoginContent ContentPlaceHolder 的默认标记，只需在设计器中右键单击该区域，然后从上下文菜单中选择 "创建自定义内容" 选项。 （使用 Visual Studio 2008 时，ContentPlaceHolder 包含一个智能标记，当选择此选项时，将提供相同的选项。）这会将新的内容控件添加到页面的标记中，从而允许我们为此页面定义自定义内容。 你可以在此处添加自定义消息，如 "请登录 ..."，但我们只需将其保留为空。

> [!NOTE]
> 在 Visual Studio 2005 中，创建自定义内容会在 ASP.NET 页中创建一个空的内容控件。 但在 Visual Studio 2008 中，创建自定义内容会将母版页的默认内容复制到新创建的内容控件中。 如果你使用的是 Visual Studio 2008，则在创建新的内容控件之后，请确保清除从母版页复制的内容。

图17显示了进行此更改后从浏览器访问的登录 .aspx 页。 请注意，左侧导航栏中没有 "Hello，stranger" 或 "欢迎回来， *username*" 消息 &lt;div&gt;。

[登录页 ![隐藏默认 LoginContent ContentPlaceHolder 的标记](an-overview-of-forms-authentication-cs/_static/image36.png)](an-overview-of-forms-authentication-cs/_static/image35.png)

**图 17**：登录页隐藏了默认 LoginContent ContentPlaceHolder 的标记（[单击以查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image37.png)）

## <a name="step-5-logging-out"></a>步骤5：注销

在步骤3中，我们介绍了如何生成登录页，以便将用户登录到站点，但我们尚未了解如何注销用户。除了在中记录用户的方法之外，FormsAuthentication 类还提供[SignOut 方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)。 SignOut 方法只是销毁 forms 身份验证票证，从而将用户记录到站点之外。

提供注销链接是一项常见功能，ASP.NET 包含专门设计用于记录用户的控件。[LoginStatus 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx)根据用户的身份验证状态显示 "Login" LinkButton 或 "注销" LinkButton。 为匿名用户呈现 "Login" LinkButton，而向经过身份验证的用户显示 "注销" LinkButton。 可以通过 LoginStatus 的 LoginText 和 LogoutText 属性配置 "Login" 和 "LinkButtons" 的文本。

单击 "登录名" LinkButton 会导致回发，从该回发将重定向到登录页。 单击 "注销" LinkButton 会导致 LoginStatus 控件调用 FormsAuthentication 方法，然后将用户重定向到页面。 已注销用户重定向到的页面取决于 LogoutAction 属性，该属性可分配给以下三个值之一：

- Refresh –默认值;将用户重定向到刚刚访问的页面。 如果他们刚访问的页面不允许匿名用户，则 FormsAuthenticationModule 会自动将用户重定向到登录页。

您可能想知道为什么要在此处执行重定向。 如果用户希望保留在同一页面上，为什么需要显式重定向？ 原因在于，单击 "注销" LinkButton 时，用户的 cookie 集合中仍有 forms 身份验证票证。 因此，回发请求是经过身份验证的请求。 LoginStatus 控件调用 SignOut 方法，但在 FormsAuthenticationModule 对用户进行身份验证后发生。 因此，显式重定向会导致浏览器重新请求页面。 当浏览器重新请求页面时，forms 身份验证票证已被删除，因此传入请求是匿名的。

- 重定向–用户重定向到由 LoginStatus 的 LogoutPageUrl 属性指定的 URL。
- RedirectToLoginPage –将用户重定向到登录页。

接下来，将 LoginStatus 控件添加到母版页，并将其配置为使用 "重定向" 选项将用户发送到一个页面，该页面会显示一条确认已注销的消息。首先在名为 "注销 .aspx" 的根目录中创建一个页面。 别忘了将此页与网站母版页关联。 接下来，在页面标记中输入一条消息，向用户说明他们已注销。

接下来，返回到网站母版页母版页，并在 LoginContent ContentPlaceHolder 中的登录视图下添加 LoginStatus 控件。 将 LoginStatus 控件的 LogoutAction 属性设置为 "重定向"，并将其 LogoutPageUrl 属性设置为 "~/Logout.aspx"。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample12.aspx)]

由于 LoginStatus 位于登录视图控件之外，因此它将同时对匿名用户和经过身份验证的用户显示，但这是正常的，因为 LoginStatus 会正确显示 "登录" 或 "注销" LinkButton。 添加了 LoginStatus 控件后，AnonymousTemplate 中的 "登录" 超链接是多余的，因此请将其删除。

图18在 Jisun 访问时显示了 default.aspx。 请注意，左栏显示消息 "欢迎回来，Jisun" 以及注销的链接。单击 "注销 LinkButton" 将导致回发，将 Jisun 从系统中注销，然后将她重定向到。 如图19所示，Jisun 到达注销时，她已经注销，因此是匿名的。 因此，左栏显示文本 "欢迎，stranger" 和登录页的链接。

[![default.aspx 显示](an-overview-of-forms-authentication-cs/_static/image39.png)](an-overview-of-forms-authentication-cs/_static/image38.png)

**图 18**： default.aspx 显示 "欢迎回来，Jisun" 和 "注销" LinkButton （[单击查看完全大小的映像](an-overview-of-forms-authentication-cs/_static/image40.png)）

[![注销 .aspx 显示](an-overview-of-forms-authentication-cs/_static/image42.png)](an-overview-of-forms-authentication-cs/_static/image41.png)

**图 19**： LinkButton 显示 "欢迎，Stranger" 和 "Login" （[单击查看完全大小的图像](an-overview-of-forms-authentication-cs/_static/image43.png)）

> [!NOTE]
> 我鼓励您自定义 "ContentPlaceHolder" 页，以隐藏母版页的 LoginContent （与在步骤4中为 .aspx 做的一样）。 原因是因为 LoginStatus 控件（位于 "Hello，stranger" 下的 LinkButton）将用户发送到在 ReturnUrl querystring 参数中传递当前 URL 的登录页。 简而言之，如果注销的用户单击此 LoginStatus 的 "Login" LinkButton，然后登录，则会将这些用户重定向回，这很容易混淆用户。

## <a name="summary"></a>摘要

在本教程中，我们首先检查 forms 身份验证工作流，然后在 ASP.NET 应用程序中实现 forms 身份验证。 Forms 身份验证由 FormsAuthenticationModule 提供支持，其中有两个责任：根据用户的 forms 身份验证票证标识用户，以及将未经授权的用户重定向到登录页。

.NET Framework 的 FormsAuthentication 类包括创建、检查和删除 forms 身份验证票证的方法。 IsAuthenticated 属性和用户对象提供额外的编程支持，以确定请求是否经过身份验证，以及有关用户身份的信息。 还提供了登录视图、LoginStatus 和 LoginName Web 控件，它们为开发人员提供了一种快速、无代码的方式来执行许多与登录相关的常见任务。 在以后的教程中，我们将更详细地介绍这些与登录相关的其他 Web 控件。

本教程大致概述了窗体身份验证。 我们未检查各种配置选项，查看无 cookie forms 身份验证票证的工作方式，或了解 ASP.NET 如何保护 forms 身份验证票证的内容。 在[下一教程](forms-authentication-configuration-and-advanced-topics-cs.md)中，我们将讨论这些主题和更多内容。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [IIS6 和 IIS7 安全性之间的更改](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [登录 ASP.NET 控件](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Professional ASP.NET 2.0 安全性、成员身份和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)（ISBN：978-0-7645-9698-8）
- [`<authentication>` 元素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [`<authentication>` 的 `<forms>` 元素](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教程中包含的主题的视频培训

- [在 ASP.NET 中使用基本 Forms 身份验证](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的主要审阅者是此教程系列已由许多有用的审阅者查看。 本教程的主管评审者包括 Alicja Maziarz、John Suru 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](security-basics-and-asp-net-support-cs.md)
> [下一页](forms-authentication-configuration-and-advanced-topics-cs.md)
