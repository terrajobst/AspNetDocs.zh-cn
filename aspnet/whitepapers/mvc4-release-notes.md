---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 本文档介绍 ASP.NET MVC 4 的版本。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: b57480bd0274fbb76c600dfb0dd09037bdcbf1e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454232"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> 本文档介绍 ASP.NET MVC 4 的版本。

- [安装说明](#_Toc303253802)
- [文档](#_Toc303253803)
- [支持](#_Toc303253804)
- [软件要求](#_Toc303253805)
- [ASP.NET MVC 4 中的新增功能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [默认项目模板的增强功能](#_Toc303253808)
    - [移动项目模板](#_Toc303253809)
    - [显示模式](#_Toc303253810)
    - [jQuery Mobile、视图切换器和浏览器替代](#_Toc303253811)
    - [异步控制器的任务支持](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [数据库迁移](#_Toc303253818)
    - [空项目模板](#_Toc303253819)
    - [将控制器添加到任何项目文件夹](#_Toc303253820)
    - [捆绑和缩小](#_Toc303253821)
    - [使用 OAuth 和 OpenID 启用来自 Facebook 和其他站点的登录名](#_Toc303253822)
- [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](#_Toc303253806)
- [ASP.NET MVC 4 候选发布中的更改](#_Toc303253817)
- [已知问题和重大更改](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>安装说明

可使用 Web 平台安装程序从[ASP.NET mvc 4 主页](../mvc/mvc4.md)安装 ASP.NET mvc 4 For Visual Studio 2010。

建议在安装 ASP.NET MVC 4 之前，卸载任何以前安装的 ASP.NET MVC 4 预览版。 你可以将 ASP.NET MVC 4 Beta 和候选发布版本升级到 ASP.NET MVC 4，而无需卸载。

此版本与 .NET Framework 4.5 的任何预览版本都不兼容。 安装 ASP.NET MVC 4 之前，必须将 .NET Framework 4.5 的任何已安装的预览版本单独升级到最终版本。

ASP.NET MVC 4 可以与 ASP.NET MVC 3 并行安装和运行。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>文档

ASP.NET MVC 的文档可以在位于以下 URL 的 MSDN 网站上找到：

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET 网站（[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)）的 MVC 4 页面上提供了有关 ASP.NET MVC 的教程和其他信息。

<a id="_Toc303253804"></a>
## <a name="support"></a>支持

完全支持 ASP.NET MVC 4。 如果你对使用此发布有任何疑问，还可以将其发布到 ASP.NET MVC 论坛（[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)），其中 ASP.NET 社区的成员通常能够提供非正式支持。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>软件要求

适用于 Visual Studio 的 ASP.NET MVC 4 组件需要 PowerShell 2.0 和 Visual Studio 2010 Service Pack 1 或带有 Service Pack 1 的 Visual Web Developer Express 2010。

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>ASP.NET MVC 4 中的新增功能

本部分介绍 ASP.NET MVC 4 版本中引入的功能。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 包括 ASP.NET Web API，这是一个新的框架，用于创建可访问范围广泛的客户端（包括浏览器和移动设备）的 HTTP 服务。 ASP.NET Web API 也是用于生成 RESTful 服务的理想平台。

ASP.NET Web API 包括对以下功能的支持：

- **新式 HTTP 编程模型：** 使用新的强类型 HTTP 对象模型直接访问和处理 Web Api 中的 HTTP 请求和响应。 可以通过新的*HttpClient*类型在客户端上对称提供相同的编程模型和 HTTP 管道。
- **完全支持路由：** ASP.NET Web API 支持 ASP.NET 路由的整套路由功能，包括路由参数和约束。 此外，使用简单约定将操作映射到 HTTP 方法。
- **内容协商：** 客户端和服务器可以协同工作，确定从 web API 返回的数据的正确格式。 ASP.NET Web API 提供对 XML、JSON 和格式 URL 编码格式的默认支持，你可以通过添加自己的格式化程序，甚至替换默认的内容协商策略来扩展此支持。
- **模型绑定和验证：** 模型联编程序提供了一种简单的方法，可以从 HTTP 请求的各个部分提取数据，并将这些消息部分转换为可由 Web API 操作使用的 .NET 对象。 还可以基于数据批注对操作参数执行验证。
- **筛选器：** ASP.NET Web API 支持包含常见筛选器的筛选器，例如 " *[授权]* " 属性。 你可以为操作、授权和异常处理编写和插入你自己的筛选器。
- **查询撰写：** 对返回*IQueryable*的操作使用 " *[可查询]* " 筛选器属性，以支持通过 OData 查询约定查询 web API。
- **改进**的可测试性：Web API 操作与*HttpRequestMessage*和*HttpResponseMessage*的实例一起使用，而不是在静态上下文对象中设置 HTTP 详细信息。 创建单元测试项目和 Web API 项目，以便快速开始编写 Web API 功能的单元测试。
- **基于代码的配置：** ASP.NET Web API 配置仅通过代码完成，使配置文件保持干净。 使用提供的服务定位器模式配置扩展点。
- **改进了对控制反转（IoC）容器的支持：** ASP.NET Web API 通过改进的依赖关系解析程序抽象为 IoC 容器提供强大支持
- **自承载：** 除了使用路由的全部功能和 Web API 的其他功能，web Api 还可以在自己的进程中托管在自己的进程中。
- **创建自定义帮助和测试页：** 现在，你可以通过使用 new *IApiExplorer*服务获取 web api 的完整运行时说明，轻松为 web api 生成自定义帮助和测试页面。
- **监视和诊断：** ASP.NET Web API 现在提供了轻型跟踪基础结构，使你可以轻松地与现有的日志记录解决方案（例如，系统诊断、ETW 和第三方日志记录框架）相集成。 可以通过提供*ITraceWriter*实现并将其添加到 web API 配置来启用跟踪。
- **链接生成：** 使用 ASP.NET Web API *UrlHelper*生成指向同一个应用程序中的相关资源的链接。
- **WEB API 项目模板：** 选择新的 "Web API" 项目，并在 "新建 MVC 4 项目向导" 中快速启动并运行 ASP.NET Web API。
- **基架：** 使用 "**添加控制器**" 对话框，可以根据基于实体框架的模型类型快速基架 web API 控制器。

有关 ASP.NET Web API 的详细信息，请访问[https://www.asp.net/web-api](../web-api/index.md)。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>默认项目模板的增强功能

已更新用于创建新 ASP.NET MVC 4 项目的模板，以创建更新式的网站：

![](mvc4-release-notes/_static/image1.png)

除了修饰改进之外，新模板中还提供了改进的功能。 该模板使用一种称为自适应呈现的技术，在桌面浏览器和移动浏览器中看起来很好，无需任何自定义。

![](mvc4-release-notes/_static/image2.png)

若要查看操作中的自适应呈现，可以使用移动仿真程序，或者尝试将桌面浏览器窗口的大小调整为更小。 当浏览器窗口变小时，该页的布局将更改。

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>移动项目模板

如果要开始一个新项目，并且想要创建专门用于移动和平板电脑浏览器的站点，则可以使用 "新建移动应用程序" 项目模板。 这基于 jQuery Mobile，这是一个用于生成触摸优化 UI 的开源库：

![](mvc4-release-notes/_static/image3.png)

此模板包含与 Internet 应用程序模板相同的应用程序结构（控制器代码几乎完全相同），但它使用 jQuery Mobile 进行了样式设计，使其在基于触摸的移动设备上看起来良好且表现良好。 若要详细了解如何构建和样式移动 UI，请参阅[JQuery mobile 项目网站](http://jquerymobile.com/)。

如果你已经有想要将移动优化视图添加到的面向桌面的站点，或如果你想要创建为桌面和移动浏览器提供不同样式视图的单一站点，则可以使用新的显示模式功能。 （请参见下一节。）

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>显示模式

使用新的显示模式功能，应用程序可以根据发出请求的浏览器选择视图。 例如，如果桌面浏览器请求主页，则该应用程序可能会使用 Views\Home\Index.cshtml 模板。 如果移动浏览器请求主页，则应用程序可能返回 Views\Home\Index.mobile.cshtml 模板。

还可以为特定的浏览器类型重写布局和分区。 例如:

- 如果你的 Views\Shared 文件夹同时包含 \_的和 \_Layout 模板，则默认情况下，应用程序将在移动浏览器的请求期间使用 \_Layout，并在其他请求期间 \_布局。
- 如果文件夹同时包含 \_MyPartial 和 \_MyPartial，则指令 @Html.Partial（"\_MyPartial"）将在移动浏览器的请求期间呈现 \_MyPartial，在其他请求期间 \_MyPartial。

如果要为其他设备创建更具体的视图、布局或分部视图，则可以注册新的*DefaultDisplayMode*实例，以指定当请求满足特定条件时要搜索的名称。 例如，可以将以下代码添加到 global.asax 文件中的*应用程序\_Start*方法，以将字符串 "iPhone" 注册为在 Apple iPhone 浏览器发出请求时适用的显示模式：

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

此代码运行后，当 Apple iPhone 浏览器发出请求时，你的应用程序将使用 Views\Shared _Layout\\（如果存在）。 有关显示模式的详细信息，请参阅[ASP.NET MVC 4 移动功能](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)。 使用 DisplayModeProvider 的应用程序应安装[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 包。 [ASP.NET 秋季2012更新](https://go.microsoft.com/fwlink/?LinkID=271322)包括新项目模板中的[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 包。 有关修补程序的详细信息，请参阅[ASP.NET MVC 4 移动缓存 Bug Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile 和 Mobile 功能

有关使用 jQuery Mobile 通过 ASP.NET MVC 4 构建移动应用程序的信息，请参阅教程[ASP.NET mvc 4 移动功能](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>异步控制器的任务支持

你现在可以将异步操作方法作为返回类型为*task*或 task 的对象的单个方法写入 *&lt;ActionResult&gt;* 。

 有关详细信息，请参阅[在 ASP.NET MVC 4 中使用异步方法](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 支持1.6 和更高版本的 Microsoft Azure SDK。

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>数据库迁移

ASP.NET MVC 4 项目现在包括实体框架5。 实体框架5的一项强大功能是对数据库迁移的支持。 利用此功能，您可以在保留数据库中的数据的同时，使用以代码为中心的迁移轻松地发展您的数据库架构。 有关数据库迁移的详细信息，请参阅[ASP.NET MVC 4 简介教程](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)中的向[电影模型和表添加新字段](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md)。

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>空项目模板

MVC 空项目模板现在确实为空，因此你可以从完全干净的平板开始。 以前版本的空项目模板已重命名为 "基本"。

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>将控制器添加到任何项目文件夹

现在可以右键单击，然后从 MVC 项目的任何文件夹中选择 "**添加控制器**"。 这使您可以更灵活地组织您需要的控制器，包括将 MVC 和 Web API 控制器保存在单独的文件夹中。

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>Bundling and Minification（绑定和缩小）

绑定和缩减框架使你可以通过将单个文件合并为脚本和 CSS 的单个捆绑文件来减少网页需要的 HTTP 请求数。 然后，它可以通过缩小绑定的内容来减小这些请求的总大小。 缩小可以包括诸如消除空白这样的活动，以缩短变量名称，甚至根据其语义折叠 CSS 选择器。 捆绑是在代码中声明和配置的，并且可以通过 helper 方法在视图中轻松引用，此方法可生成指向绑定的单个链接，或在调试时将多个链接链接到捆绑的单个内容。 有关详细信息，请参阅[捆绑和缩减](../mvc/overview/performance/bundling-and-minification.md)。

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>使用 OAuth 和 OpenID 启用来自 Facebook 和其他站点的登录名

ASP.NET MVC 4 Internet 项目模板中的默认模板现在包含对使用 DotNetOpenAuth 库的 OAuth 和 OpenID 登录名的支持。 有关配置 OAuth 或 OpenID 提供程序的信息，请参阅[WebForms、MVC 和网页的 oauth/Openid 支持](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx)和[ASP.NET 网页中的 oauth 和 openid 功能文档](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4

可以在同一台计算机上并行安装 ASP.NET MVC 4 与 ASP.NET MVC 3，这使你可以灵活选择何时将 ASP.NET MVC 3 应用程序升级到 ASP.NET MVC 4。

升级的最简单方法是创建一个新的 ASP.NET MVC 4 项目并将所有视图、控制器、代码和内容文件从现有 MVC 3 项目复制到新项目，然后更新新项目中的程序集引用以匹配中的任何非 MVC 模板你使用的 cluded assembiles。 如果已更改 MVC 3 项目中的 web.config 文件，还必须将这些更改合并到 MVC 4 项目中的 web.config 文件中。

若要手动将现有的 ASP.NET MVC 3 应用程序升级到版本4，请执行以下操作：

1. 在项目的所有 web.config 文件中（在项目的根目录中有一个文件，在 Views 文件夹中，一个位于项目中每个区域的 Views 文件夹中），替换以下文本的每个实例（注意： System.web，Version = 1.0.0.0）用 Visual Studio 2012 创建的项目）： 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    ，其中包含以下相应的文本：

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. 在根 web.config 文件中，将 "*网页： Version* " 元素更新为 "2.0.0.0" 并添加值为 "true" 的新*PreserveLoginUrl*键： 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. 在解决方案资源管理器中，右键单击 "引用"，然后选择 "管理 NuGet 包"。 在左窗格中，选择 " **Online\NuGet 官方包源**"，并更新以下内容：

    - ASP.NET MVC 4
    - （可选） jQuery、jQuery 验证和 jQuery UI
    - 可有可无实体框架
    - (Optonal)Modernizr
4. 在解决方案资源管理器中，右键单击项目名称，然后选择 "卸载项目"。 然后再次右键单击该名称，然后选择 "编辑*项目*名称 .csproj"。
5. 找到*ProjectTypeGuids*元素，并将 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 替换为 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。
6. 保存所做的更改，关闭正在编辑的项目（.csproj）文件，右键单击该项目，然后选择 "重新加载项目"。
7. 如果项目引用使用以前版本的 ASP.NET MVC 编译的任何第三方库，请打开根 web.config 文件，并在*配置*节下添加以下三个*bindingRedirect*元素： 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 候选发布中的更改

可在此处找到 ASP.NET MVC 4 候选发行版的发行说明：

下面总结了此版本中从 ASP.NET MVC 4 候选发布版本的主要变化：

- **每个控制器配置：** 可以使用实现*IControllerConfiguration*的自定义特性来设置其自己的格式化程序、操作选择器和参数联编程序的特性。 ASP.NET Web API *HttpControllerConfigurationAttribute*已删除。
- **按路由消息处理程序：** 你现在可以在给定路由的请求链中指定最终消息处理程序。 这样，就可以支持结合框架使用路由调度到自己的（非*IHttpController*）终结点。
- **进度通知：** *ProgressMessageHandler*为要上传的请求实体和正在下载的响应实体生成进度通知。 使用此处理程序，可以跟踪上载请求正文或下载响应正文的距离。
- **推送内容：** 使用*PushStreamContent*类可以实现以下方案：数据生成者希望使用流直接写入请求或响应（无论是同步还是异步）。 当*PushStreamContent*准备接受数据时，它会使用输出流调用操作委托。 然后，开发人员可以根据需要写入流，并在写入完成后关闭流。 *PushStreamContent*检测流的关闭并完成用于写出内容的基础异步*任务*。
- **创建错误响应：** 使用*HttpError*类型可一致地将错误信息（如验证错误和异常）表示为*IncludeErrorDetailPolicy*。 使用新的*CreateErrorResponse*扩展方法，可以轻松地使用*HttpError*作为内容创建错误响应。 *HttpError*内容是完全的内容协商。
- **已删除 MediaRangeMapping：** 媒体类型范围现在由默认的内容 negotiator 处理。
- **简单类型参数的默认参数绑定现在为 [FromUri]：** 在的早期版本中 ASP.NET Web API 使用模型绑定的简单类型参数的默认参数绑定。 简单类型参数的默认参数绑定现在为 *[FromUri]* 。
- **操作选择采用必需参数：** 如果提供了来自 URI 的所有必需参数，ASP.NET Web API 中的操作选择现在将仅选择一个操作。 通过为操作方法签名中的参数提供默认值，可以将参数指定为可选。
- **自定义 HTTP 参数绑定：** 使用*ParameterBindingAttribute*为特定操作参数自定义参数绑定，或使用*HttpConfiguration*上的*ParameterBindingRules*来更广泛地自定义参数绑定。
- **MediaTypeFormatter 改进：** 格式化程序现在有权访问完整的*HttpContent*实例。
- **主机缓冲策略选择：** 在 ASP.NET Web API 中实现并配置*IHostBufferPolicySelector*服务，以允许主机确定何时使用缓冲的策略。
- **以不可知的方式访问客户端证书：** 使用*GetClientCertificate*扩展方法从请求消息中获取提供的客户端证书。
- **内容协商扩展性：** 通过从*DefaultContentNegotiator*派生并覆盖你喜欢的内容协商的任何方面来自定义内容协商。
- **支持返回406无法接受的响应：** 你现在可以通过创建*DefaultContentNegotiator*并将*excludeMatchOnTypeOnly*参数设置为*true*来找不到合适的格式化程序，从而在 ASP.NET Web API 中返回406。
- 将**表单数据作为 NameValueCollection 或 JToken 读取：** 您可以分别使用*ParseQueryString*和*ReadAsFormDataAsync*扩展方法，在 URI 查询字符串或请求正文中读取窗体数据作为*NameValueCollection* 。 同样，您可以分别使用*TryReadQueryAsJson*和*ReadAsAsync*&lt;t&gt; 扩展方法，将 URI 查询字符串或请求正文中的窗体数据读取为*JToken* 。
- **多部分改进：** 现在，可以编写一个 MultipartStreamProvider，该完全定制为可读取的 MIME 多部分数据类型，并以最佳方式向用户显示结果。 你还可以在*MultipartStreamProvider*上挂钩 post 处理步骤，使实现能够在 MIME 多部分正文部分中执行所需的任何后期处理。 例如， *MultipartFormDataStreamProvider*实现读取 HTML 窗体数据部分，并将其添加到*NameValueCollection* ，以便从调用方轻松获取它们。
- **链接生成改进：** *UrlHelper*不再依赖于*system.web.http.controllers.httpcontrollercontext*。 你现在可以从提供*HttpRequestMessage*的任何上下文中访问*UrlHelper* 。
- **消息处理程序执行顺序更改：** 消息处理程序现在按其配置顺序而不是按相反的顺序执行。
- **用于接线消息处理程序的帮助程序：** 新*HttpClientFactory*可以连接*DelegatingHandlers* ，并使用所需的管道准备就绪来创建*HttpClient* 。 它还提供了使用替代内部处理程序进行布线（默认值为*HttpClientHandler*）的功能，以及使用*HttpMessageInvoker*或其他*DelegatingHandler*而不是*HttpClient*作为顶级调用程序时进行布线。
- **对 ASP.NET Web 优化中的 cdn 的支持：** ASP.NET Web 优化现在提供对 CDN 备用路径的支持，使你能够为每个包指定一个附加 URL，该 URL 指向内容分发网络上的同一资源。 通过支持 Cdn，您可以使您的脚本和样式捆绑在地理上离您的 Web 应用程序的最终使用者更近。 当 CDN 不可用时，生产应用应实施回退。 测试回退。
- **ASP.NET Web API 路由和配置已移动到*webapiconfig.cs。注册*可在测试代码中 resused 的静态方法。** ASP.NET Web API 路由之前已添加到*RegisterRoutes*以及标准 MVC 路由。 现在会在单独的*webapiconfig.cs*方法中处理默认的 ASP.NET Web API 路由和配置，以便进行测试。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

- **返回移动视图时，ASP.NET MVC 4 的 RC 和 RTM 版本会错误地返回缓存的桌面视图。**

    - 有关修补程序的详细信息，请参阅[ASP.NET MVC 4 移动缓存 Bug](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 。 可以从[修复的 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 包安装此修补程序。
- **Razor 视图引擎中的重大更改**。 以下类型已从*system.web*中删除： 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  还删除了以下方法： 

    - *MvcCSharpRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
    - *MvcWebPageRazorHost. DecorateCodeGenerator （System.web. RazorCodeGenerator）*
    - *MvcVBRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
- **当 WebData 包含在 ASP.NET MVC 4 应用程序的/bin 目录中时，它将接管用于窗体身份验证的 URL。** 将 WebData 程序集添加到应用程序（例如，在使用 "添加可部署的依赖项" 对话框时选择 "使用 Razor 语法 ASP.NET 网页" 时）会将身份验证登录重定向重定向到/account/logon，而不是默认的 ASP.NET MVC 帐户控制器所需的/account/login。 若要防止此行为并使用在 web.config 的身份验证部分中指定的 URL，可以添加一个名为 PreserveLoginUrl 的 appSetting，并将其设置为 true： 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **尝试安装 Visual Studio 2010 和 Visual Web Developer 2010 的并行安装的 ASP.NET MVC 4 时，NuGet 包管理器无法安装。** 若要与 ASP.NET MVC 4 并行运行 Visual Studio 2010 和 Visual Web Developer 2010，则必须在安装了两个版本的 Visual Studio 后安装 ASP.NET MVC 4。
- **如果已卸载了必备组件，则卸载 ASP.NET MVC 4 会失败。** 若要完全卸载 ASP.NET MVC 4you，必须先卸载 ASP.NET MVC 4，然后再卸载 Visual Studio。
- **安装 ASP.NET MVC 4 中断 ASP.NET MVC 3 RTM 应用程序。** 使用 RTM 版本创建的 ASP.NET MVC 3 应用程序（而不是[ASP.NET mvc 3 工具更新](https://www.microsoft.com/download/details.aspx?id=1491)版本）需要进行以下更改才能与 ASP.NET MVC 4 并行工作。 生成项目但不进行这些更新会导致编译错误。 

    **所需更新**

  1. 在根 web.config 文件中，添加一个新的 *&lt;appSettings&gt;* 项，其中包含密钥 "*网页：版本*" 和 " *1.0.0.0*" 值。 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. 在解决方案资源管理器中，右键单击项目名称，然后选择 "卸载项目"。 然后再次右键单击该名称，然后选择 "编辑*项目*名称 .csproj"。
  3. 找到以下程序集引用： 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      将它们替换为以下内容：

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. 保存所做的更改，关闭正在编辑的项目（.csproj）文件，然后右键单击该项目，然后选择 "重新加载"。

- 将**ASP.NET MVC 4 项目更改为目标为4.0 的4.5 不会更新 EntityFramework 程序集引用：** 如果在针对4.5 后将 ASP.NET MVC 4 项目更改为目标4.0，则对 EntityFramework 程序集的引用仍将指向4.5 版本。 若要解决此问题，请卸载并重新安装 EntityFramework NuGet 包。
- **403 在从4.5 更改为目标4.0 后，在 Azure 上运行 ASP.NET MVC 4 应用程序时禁止：** 如果在针对4.5 后将 ASP.NET MVC 4 项目更改为目标4.0，然后将其部署到 Azure，则在运行时可能会看到 403 "禁止访问" 错误。 若要解决此问题，请将以下内容添加到 web.config： `<modules runAllManagedModulesForAllRequests="true" />`
- **在 Razor 文件中的字符串文本中键入 "\' 时，Visual Studio 2012 会崩溃。** 若要解决此问题，请首先输入字符串文字的右引号。
- <strong>浏览到 &quot;帐户/管理&quot; Internet 模板会导致 CHS、修订和 CHT 语言出现运行时错误。</strong> 若要修复此问题，请修改页面，将其作为<em>&lt;强&gt;</em>标记中的唯一内容来分离<em>@User.Identity.Name</em> 。
- **Azure 网站内不支持 Google 和 LinkedIn 访问接口。** 部署到 Azure 网站时使用备用身份验证提供程序。
- **将 UriPathExtensionMapping 与 IIS 8 Express/IIS 一起使用时，当你尝试使用该扩展时，会收到 404 "找不到" 错误。** 静态文件处理程序将干扰对使用*UriPathExtensionMappings*的 web api 的请求。 在 web.config 中设置*runAllManagedModulesForAllRequests = true* ，以解决此问题。
- **不调用 Execute 方法。** 所有 MVC 控制器现在始终都以异步方式执行。
