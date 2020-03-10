---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 本文档介绍 Visual Studio 2010 的 ASP.NET MVC 4 Beta 版本。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419840"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> 本文档介绍 Visual Studio 2010 的 ASP.NET MVC 4 Beta 版本。
> 
> > [!NOTE]
> > 这不是最新版本。 [此处](mvc4-release-notes.md)提供了 ASP.NET MVC 4 RC 发行说明。

- [安装说明](#_Toc303253802)
- [文档](#_Toc303253803)
- [支持](#_Toc303253804)
- [软件要求](#_Toc303253805)
- [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](#_Toc303253806)
- [ASP.NET MVC 4 Beta 中的新增功能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [ASP.NET 单页面应用程序](#_Toc317096198)
    - [默认项目模板的增强功能](#_Toc303253808)
    - [移动项目模板](#_Toc303253809)
    - [显示模式](#_Toc303253810)
    - [jQuery Mobile、视图切换器和浏览器替代](#_Toc303253811)
    - [Visual Studio 中用于代码生成的食谱](#_Toc303253812)
    - [异步控制器的任务支持](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [已知问题和重大更改](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>安装说明

可使用 Web 平台安装程序从[ASP.NET mvc 4 主页](../mvc/mvc4.md)安装适用于 Visual Studio 2010 的 ASP.NET Mvc 4 Beta 版。

在安装 ASP.NET MVC 4 Beta 之前，必须先卸载任何以前安装的 ASP.NET MVC 4 预览版。

此版本与 .NET Framework 4.5 开发人员预览版不兼容。 安装 ASP.NET MVC 4 Beta 之前，必须先卸载 .NET 4.5 开发者预览版。

可以安装 ASP.NET MVC 4，并且可以并行运行与 ASP.NET MVC 3。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>文档

ASP.NET MVC 的文档可以在位于以下 URL 的 MSDN 网站上找到：

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET 网站（[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)）的 MVC 4 页面上提供了有关 ASP.NET MVC 的教程和其他信息。

<a id="_Toc303253804"></a>
## <a name="support"></a>支持

这是预览版本，不正式支持。 如果你对此版本有任何疑问，请将其发布到 ASP.NET MVC 论坛（[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)），其中 ASP.NET 社区的成员通常能够提供非正式支持。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>软件要求

适用于 Visual Studio 的 ASP.NET MVC 4 组件需要 PowerShell 2.0 和 Visual Studio 2010 Service Pack 1 或带有 Service Pack 1 的 Visual Web Developer Express 2010。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4

可以在同一台计算机上并行安装 ASP.NET MVC 4 与 ASP.NET MVC 3，这使你可以灵活选择何时将 ASP.NET MVC 3 应用程序升级到 ASP.NET MVC 4。

升级的最简单方法是创建一个新的 ASP.NET MVC 4 项目，并将现有 MVC 3 项目中的所有视图、控制器、代码和内容文件复制到新项目，然后更新新项目中的程序集引用以匹配旧项目。 如果已更改 MVC 3 项目中的 web.config 文件，还必须将这些更改合并到 MVC 4 项目中的 web.config 文件中。

若要手动将现有的 ASP.NET MVC 3 应用程序升级到版本4，请执行以下操作：

1. 在项目的所有 web.config 文件中（项目的根目录中有一个文件，在 Views 文件夹中，一个位于项目中每个区域的 Views 文件夹中），替换以下文本的每个实例：

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    ，其中包含以下相应的文本：

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. 在根 web.config 文件中，将 "*网页： Version* " 元素更新为 "2.0.0.0" 并添加值为 "true" 的新*PreserveLoginUrl*键：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. 在解决方案资源管理器中，删除对*system.web*的引用（指向版本 3 DLL）。 然后，*添加对4.0.0.0 的引用（v* ）。 特别是，进行以下更改以更新程序集引用。 以下为详细信息：

    1. 在解决方案资源管理器中，删除对以下程序集的引用： 

        - *System.web*（v 3.0.0.0）
        - *System.web*（1.0.0.0）
        - *System.web*（1.0.0.0）
        - *System.web. Deployment*（1.0.0.0）
        - *System.web. Razor*（1.0.0.0）
    2. 添加对以下程序集的引用： 

        - *System.web*（v 4.0.0.0）
        - *System.web*（v 2.0.0.0）
        - *System.web. Razor*（v 2.0.0.0）
        - *System.web. Deployment*（v 2.0.0.0）
        - *System.web. Razor*（v 2.0.0.0）
4. 在解决方案资源管理器中，右键单击项目名称，然后选择 "卸载项目"。 然后再次右键单击该名称，然后选择 "编辑*项目*名称 .csproj"。
5. 找到*ProjectTypeGuids*元素，并将 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 替换为 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。
6. 保存所做的更改，关闭正在编辑的项目（.csproj）文件，右键单击该项目，然后选择 "重新加载项目"。
7. 如果项目引用使用以前版本的 ASP.NET MVC 编译的任何第三方库，请打开根 web.config 文件，并在*配置*节下添加以下三个*bindingRedirect*元素： 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>ASP.NET MVC 4 Beta 中的新增功能

本部分介绍 ASP.NET MVC 4 Beta 版本中引入的功能。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 现在包括了 ASP.NET Web API，这是一个新的框架，用于创建可访问范围广泛的客户端（包括浏览器和移动设备）的 HTTP 服务。 ASP.NET Web API 也是用于生成 RESTful 服务的理想平台。

ASP.NET Web API 包括对以下功能的支持：

- **新式 HTTP 编程模型：** 使用新的强类型 HTTP 对象模型直接访问和处理 Web Api 中的 HTTP 请求和响应。 可以通过新的 HttpClient 类型在客户端上对称提供相同的编程模型和 HTTP 管道。
- **完全支持路由**： web api 现在支持一组完整的路由功能，这些功能始终是 Web 堆栈的一部分，包括路由参数和约束。 此外，映射到操作完全支持约定，因此您不再需要将属性（例如 [HttpPost]）应用于您的类和方法。
- **内容协商**：客户端和服务器可以协同工作，确定从 API 返回的数据的正确格式。 我们提供对 XML、JSON 和格式 URL 编码格式的默认支持，你可以通过添加自己的格式化程序，甚至替换默认的内容协商策略来扩展此支持。
- **模型绑定和验证：** 模型联编程序提供了一种简单的方法，可以从 HTTP 请求的各个部分提取数据，并将这些消息部分转换为可由 Web API 操作使用的 .NET 对象。
- **筛选器：** Web Api 现在支持筛选器，其中包括众所周知的筛选器，例如 "[授权]" 属性。 你可以为操作、授权和异常处理编写和插入你自己的筛选器。
- **查询撰写：** 通过只返回 IQueryable&lt;T&gt;，Web API 将支持通过 OData URL 约定进行查询。
- **提高了 HTTP 详细信息的可测试性：** Web API 操作现在可以与 HttpRequestMessage 和 HttpResponseMessage 的实例一起使用，而不是在静态上下文对象中设置 HTTP 详细信息。 除了使用 HTTP 类型外，还存在这些对象的泛型版本。
- **通过 DependencyResolver 改进了控制反转（IoC）：** Web API 现在使用由 MVC 的依赖关系解析程序实现的服务定位器模式来获取许多不同设施的实例。
- **基于代码的配置：** Web API 配置仅通过代码完成，使配置文件保持干净整洁。
- **自承载：** 除了使用路由的全部功能和 Web API 的其他功能，web Api 还可以在自己的进程中托管在自己的进程中。

有关 ASP.NET Web API 的详细信息，请访问[https://www.asp.net/web-api](../web-api/index.md)。

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET 单页面应用程序

ASP.NET MVC 4 现在包括了使用 JavaScript 和 Web Api 生成单页面应用程序以及使用很多客户端交互的体验的早期预览版。 此支持包括：

- 一组用于与缓存数据进行更丰富的本地交互的 JavaScript 库
- 工作单元和 DAL 支持的其他 Web API 组件
- 带有基架的 MVC 项目模板，用于快速入门

有关 ASP.NET MVC 4 中的单页面应用程序支持的更多详细信息，请访问[https://www.asp.net/single-page-application](../single-page-application/index.md)。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>默认项目模板的增强功能

已更新用于创建新 ASP.NET MVC 4 项目的模板，以创建更新式的网站：

![](mvc4-beta-release-notes/_static/image1.png)

除了修饰改进之外，新模板中还提供了改进的功能。 该模板使用一种称为自适应呈现的技术，在桌面浏览器和移动浏览器中看起来很好，无需任何自定义。

![](mvc4-beta-release-notes/_static/image2.png)

若要查看操作中的自适应呈现，可以使用移动仿真程序，或者尝试将桌面浏览器窗口的大小调整为更小。 当浏览器窗口变小时，该页的布局将更改。

默认项目模板的另一增强功能是使用 JavaScript 提供更丰富的 UI。 在模板中使用的登录名和注册链接是如何使用 jQuery UI 对话框提供丰富的登录屏幕的示例：

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>移动项目模板

如果要开始一个新项目，并且想要创建专门用于移动和平板电脑浏览器的站点，则可以使用 "新建移动应用程序" 项目模板。 这基于 jQuery Mobile，这是一个用于生成触摸优化 UI 的开源库：

![](mvc4-beta-release-notes/_static/image4.png)

此模板包含与 Internet 应用程序模板相同的应用程序结构（控制器代码几乎完全相同），但它使用 jQuery Mobile 进行了样式设计，使其在基于触摸的移动设备上看起来良好且表现良好。 若要详细了解如何构建和样式移动 UI，请参阅[JQuery mobile 项目网站](http://jquerymobile.com/)。

如果你已经有想要将移动优化视图添加到的面向桌面的站点，或如果你想要创建为桌面和移动浏览器提供不同样式视图的单一站点，则可以使用新的显示模式功能。 （请参见下一节。）

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>显示模式

使用新的显示模式功能，应用程序可以根据发出请求的浏览器选择视图。 例如，如果桌面浏览器请求主页，则该应用程序可能会使用 Views\Home\Index.cshtml 模板。 如果移动浏览器请求主页，则应用程序可能返回 Views\Home\Index.mobile.cshtml 模板。

还可以为特定的浏览器类型重写布局和分区。 例如:

- 如果你的 Views\Shared 文件夹同时包含 \_的和 \_Layout 模板，则默认情况下，应用程序将在移动浏览器的请求期间使用 \_Layout，并在其他请求期间 \_布局。
- 如果文件夹同时包含 \_MyPartial 和 \_MyPartial，则指令 @Html.Partial（"\_MyPartial"）将在移动浏览器的请求期间呈现 \_MyPartial，在其他请求期间 \_MyPartial。

如果要为其他设备创建更具体的视图、布局或分部视图，则可以注册新的*DefaultDisplayMode*实例，以指定当请求满足特定条件时要搜索的名称。 例如，可以将以下代码添加到 global.asax 文件中的*应用程序\_Start*方法，以将字符串 "iPhone" 注册为在 Apple iPhone 浏览器发出请求时适用的显示模式：

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

此代码运行后，当 Apple iPhone 浏览器发出请求时，你的应用程序将使用 Views\Shared _Layout\\（如果存在）。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile、视图切换器和浏览器替代

jQuery Mobile 是用于构建触摸优化 web UI 的开源库。 如果要将 jQuery Mobile 用于 ASP.NET MVC 4 应用程序，可以下载并安装可帮助你入门的 NuGet 包。 若要从 Visual Studio 包管理器控制台安装，请键入以下命令：

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

这将安装 jQuery Mobile 和一些 helper 文件，其中包括：

- Views/Shared/\_Layout，它是基于 jQuery Mobile 的布局。
- 视图切换器组件，由 Views/Shared/\_ViewSwitcher 分部视图和 ViewSwitcherController.cs 控制器组成。

安装包后，使用移动浏览器运行应用程序（或等效项，如 Firefox[用户代理切换](http://chrispederick.com/work/user-agent-switcher/)器外接程序）。 你将看到页面看上去差别很大，因为 jQuery Mobile 处理布局和样式。 若要利用此内容，可以执行以下操作：

- 如前面的[显示模式](#_Toc303253810)所述创建特定于移动设备的视图重写（例如，创建 Views\Home\Index.mobile.cshtml 以替代移动浏览器的 Views\Home\Index.cshtml）。
- 若要详细了解如何在移动视图中添加触控优化的 UI 元素，请阅读[JQuery mobile 文档](http://jquerymobile.com/)。

移动优化的网页约定是添加一个链接，其文本的内容类似于桌面视图或完整站点模式，使用户能够切换到页面的桌面版本。 JQuery. node.js 包包含一个用于此目的的视图切换器组件示例。 它在默认的 Views\Shared\\_Layout 中使用，在呈现页面时，它如下所示：

![](mvc4-beta-release-notes/_static/image5.png)

如果访问者单击此链接，则会切换到同一页面的桌面版本。

由于默认情况下，桌面布局不包括视图切换器，因此访问者将无法访问移动模式。 若要启用此操作，请将以下对 *\_ViewSwitcher*的引用添加到桌面布局，只需在 *&lt;body&gt;* 元素内：

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

视图切换器使用称为 "浏览器重写" 的新功能。 此功能使应用程序可以处理请求，就好像这些请求来自于它们实际来自的浏览器（用户代理）。 下表列出了浏览器重写提供的方法。

| `HttpContext.SetOverriddenBrowser(userAgentString)` | 使用指定的用户代理，重写请求的实际用户代理值。 |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | 如果未指定替代，则返回请求的用户代理替代值或实际的用户代理字符串。 |
| `HttpContext.GetOverriddenBrowser()` | 返回一个*HttpBrowserCapabilitiesBase*实例，该实例对应于当前为请求设置的用户代理（实际或重写）。 可以使用此值获取属性，如*IsMobileDevice*。 |
| `HttpContext.ClearOverriddenBrowser()` | 删除任何针对当前请求重写的用户代理。 |

浏览器重写是 ASP.NET MVC 4 的一项核心功能，即使不安装 jQuery. node.js 包也是如此。 但是，它只会影响视图、布局和分部视图选择，而不会影响依赖于*请求 .browser*对象的任何其他 ASP.NET 功能。

默认情况下，使用 cookie 存储用户代理替代。 如果要在其他位置（例如，在数据库中）存储替代，可以替换默认提供程序（*BrowserOverrideStores*）。 此提供程序的文档将提供给 ASP.NET MVC 的更高版本。

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>Visual Studio 中用于代码生成的食谱

使用新的食谱功能，Visual Studio 可基于可使用 NuGet 安装的包生成特定于解决方案的代码。 通过食谱框架，开发人员可以轻松编写代码生成插件，还可以使用它来替换 "添加区域"、"添加控制器" 和 "添加视图" 的内置代码生成器。 因为食谱以 NuGet 包的形式部署，所以可以轻松地将其签入源控件并自动与项目上的所有开发人员共享。 它们还可用于每个解决方案。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>异步控制器的任务支持

你现在可以将异步操作方法作为返回类型为*task*或 task 的对象的单个方法写入 *&lt;ActionResult&gt;* 。

例如，如果使用的是 Visual C# 5 （或使用[Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)），则可以创建一个类似于下面的异步操作方法：

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

在上一操作方法中，对*newsService*和*sportsService*的调用是异步调用的，并且不会阻止线程池中的线程。

返回*任务*实例的异步操作方法还可以支持超时。 若要使操作方法可取消，请将*CancellationToken*类型的参数添加到操作方法签名中。 下面的示例显示一个异步操作方法，该操作方法的超时为2500毫秒，在出现超时的情况下，将向客户端显示*超时*视图。

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 Beta 支持 Microsoft Azure SDK 1.5 2011 年9月版。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

- **安装 ASP.NET MVC 4 Beta 后，Visual Studio 2010 Service Pack 1 中的 CSHTML/VBHTML 编辑器在 cshtml/VBHTML 文件中键入代码段或 JavaScript 后，可能会暂停很长时间。** 仅在刚刚创建且尚未编译的 ASP.NET MVC 4 应用程序中进行此操作。

    解决方法是编译项目以获取 bin 文件夹中的程序集。 请注意，如果您清除了从 bin 文件夹中删除程序集的项目，则会出现编辑器问题。

    这将在下一版本中得到更正。
- **C#适用于 Visual Studio 11 Beta 的项目模板在 Global.asax.cs 中包含不正确的连接字符串。** 在 Visual Studio 11 Beta 中创建的项目的 Application\_Start 方法中指定的默认连接包含一个 LocalDB 连接字符串，其中包含非转义反斜杠（\) 字符。 这会导致在尝试访问实体框架 DbContext 时出现连接错误，这将生成 SqlException。

    若要更正此问题，请将应用中的反斜杠字符转义\_Start Global.asax.cs 方法，使其如下所示：

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **在 .NET 4.0 下运行时，面向 .NET 4.5 的 ASP.NET MVC 4 应用程序将引发 FileLoadException，尝试访问该程序集。** 在 .NET 4.5 中创建的 ASP.NET MVC 4 应用程序包含绑定重定向，此重定向将导致 FileLoadException，这表明 "无法加载文件或程序集 ' 系统 .Net. Http ' 或它的一个依赖项"。 当在安装了 .NET 4.0 的系统上执行应用程序时。 若要更正此问题，请从 web.config 中删除以下绑定重定向：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    修改后的 web.config 中的程序集绑定元素应如下所示：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <strong>从区域内</strong><strong>调用时，Visual Basic 项目中的 "添加控制器" 项模板将生成不正确的命名空间</strong>。 将控制器添加到使用 Visual Basic 的 ASP.NET MVC 项目中的某个区域时，项模板会将错误的命名空间插入控制器。 在导航到控制器中的任何操作时，结果为 "找不到文件" 错误。  
  
  生成的命名空间忽略根命名空间后面的所有内容。 例如，生成的命名空间为*RootNamespace* ，但应为*RootNamespace* 。
- **Razor 视图引擎中的重大更改。** 作为 Razor 分析器重写的一部分，将从*system.web*中删除以下类型： 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  还删除了以下方法： 

    - *MvcCSharpRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
    - *MvcWebPageRazorHost. DecorateCodeGenerator （System.web. RazorCodeGenerator）*
    - *MvcVBRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*
- **当 WebData 包含在 ASP.NET MVC 4 应用程序的/bin 目录中时，它将接管用于窗体身份验证的 URL。** 将 WebData 程序集添加到应用程序（例如，在使用 "添加可部署的依赖项" 对话框时选择 "使用 Razor 语法 ASP.NET 网页" 时）会将身份验证登录重定向重定向到/account/logon，而不是默认的 ASP.NET MVC 帐户控制器所需的/account/login。 若要防止此行为并使用在 web.config 的身份验证部分中指定的 URL，可以添加一个名为 PreserveLoginUrl 的 appSetting，并将其设置为 true： 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **尝试安装 Visual Studio 2010 和 Visual Web Developer 2010 的并行安装的 ASP.NET MVC 4 时，NuGet 包管理器无法安装。** 若要与 ASP.NET MVC 4 并行运行 Visual Studio 2010 和 Visual Web Developer 2010，则必须在安装了两个版本的 Visual Studio 后安装 ASP.NET MVC 4。
- **如果已卸载了必备组件，则卸载 ASP.NET MVC 4 会失败。** 若要完全卸载 ASP.NET MVC 4you，必须先卸载 ASP.NET MVC 4，然后再卸载 Visual Studio。
- **运行默认的 Web API 项目会显示错误地指示用户使用不存在的 RegisterApis 方法添加路由的指令。** 应使用 ASP.NET 路由表在 RegisterRoutes 方法中添加路由。
- **安装 ASP.NET MVC 4 Beta 中断 ASP.NET MVC 3 RTM 应用程序。** 使用 RTM 版本创建的 ASP.NET MVC 3 应用程序（而不是 ASP.NET MVC 3 工具更新版本）需要进行以下更改才能与 ASP.NET MVC 4 Beta 并行工作。 生成项目但不进行这些更新会导致编译错误。 

    **所需更新**

  1. 在根 web.config 文件中，添加一个新的 *&lt;appSettings&gt;* 项，其中包含密钥 "*网页：版本*" 和 " *1.0.0.0*" 值。

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. 在解决方案资源管理器中，右键单击项目名称，然后选择 "卸载项目"。 然后再次右键单击该名称，然后选择 "编辑*项目*名称 .csproj"。
  3. 找到以下程序集引用： 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      将它们替换为以下内容：

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. 保存所做的更改，关闭正在编辑的项目（.csproj）文件，然后右键单击该项目，然后选择 "重新加载"。
