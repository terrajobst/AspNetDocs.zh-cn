---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: （包括2011年4月的工具更新）ASP.NET MVC 3 是一个框架，用于生成基于标准的可缩放 web 应用程序，该应用程序使用完善的设计模式 。
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499646"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *（包括2011年4月的工具更新）*
> 
> ASP.NET MVC 3 是一个框架，用于生成可缩放的基于标准的 web 应用程序，该应用程序使用良好构建的设计模式以及 ASP.NET 和 .NET Framework 的强大功能。
> 
> 它与 ASP.NET MVC 2 并行安装，因此马上就开始使用吧！
> 
> 在[此处下载安装程序](https://go.microsoft.com/fwlink/?LinkID=208140)

## <a name="top-features"></a>顶级功能

- 集成基架系统通过 NuGet 可扩展
- 已启用 HTML 5 的项目模板
- 富有表现力的视图，包括新的 Razor 视图引擎
- 依赖关系注入和全局操作筛选器的强大挂钩
- 具有非引人注目 JavaScript、jQuery 验证和 JSON 绑定的丰富 JavaScript 支持
- *阅读[下面](#overview)的完整功能列表*

## <a name="top-links"></a>顶部链接

ASP.NET MVC 3 中的新增功能

- Phil Haack：已[发布 ASP.NET MVC 3](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman： [ASP.NET MVC3、WebMatrix、NuGet、IIS Express 和 Orchard 发布-在上下文中为 Microsoft 1 月版 Web 版本](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie：[宣布发布 ASP.NET MVC 3，IIS Express，SQL CE 4，Web 场框架，Orchard，WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 的发行说明](../whitepapers/mvc3-release-notes.md)

安装和帮助

- 使用[Web 平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)安装 ASP.NET MVC 3 （推荐）
- 使用[安装程序可执行文件](https://go.microsoft.com/fwlink/?LinkID=208140)安装 ASP.NET MVC 3
- 安装[ASP.NET MVC 3 For Visual Studio 11 开发人员预览版](https://go.microsoft.com/fwlink/?LinkID=208140)
- 阅读[简介到 ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- 获取帮助并讨论[论坛](https://forums.asp.net/1146.aspx)中的 ASP.NET MVC 3

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview（ASP.NET MVC 3 概述）

ASP.NET MVC 3 是在 ASP.NET MVC 1 和2上构建的，它添加了可简化代码和允许更深层扩展的强大功能。 本主题概述了此版本中包含的许多新功能，这些功能分为以下几个部分：

- [具有 MvcScaffold 集成的可扩展基架](#BM_MvcScaffolding)
- [已启用 HTML 5 的项目模板](#BM_HTML5)
- [Razor 视图引擎](#BM_TheRazorViewEngine)
- [支持多个视图引擎](#BM_Support_for_Multiple_View_Engines)
- [控制器改进](#BM_Controller_Improvements)
- [JavaScript 和 Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [模型验证改进](#BM_Model_Validation_Improvements)
- [依赖关系注入改进](#BM_Dependency_Injection_Improvements)
- [其他新功能](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>具有 MvcScaffold 集成的可扩展基架

如果你完全不熟悉框架，则新的基架系统使你可以更轻松地选择并有效地使用，如果你有经验并且已经了解你所做的工作，则可以自动执行常见的开发任务。

这是名为**MvcScaffolding**的新 NuGet*基架*包支持的。 许多软件技术使用术语 "基架" 来表示 "快速生成软件的基本大纲，然后可以编辑并自定义。 我们为 ASP.NET MVC 创建的基架包在多个方案中极有好处：

- **如果你是首次学习 ASP.NET MVC**，因为它提供了一些有用的工作代码的快捷方式，你可以根据需要对其进行编辑和调整。 它为你节省了 trauma 的时间，让你看看空白页面并不知道从何处着手！
- **如果你知道 ASP.NET MVC 并且现在正在探索一些新的附加设备技术**，如对象关系映射器、视图引擎、测试库等，因为该技术的创建者可能还为其创建了基架包。
- **如果您的工作过程中重复创建了类似的类或文件**，则可以创建自定义框架来输出测试装置、部署脚本或其他任何所需的文件。 你的团队中的每个人都可以使用你的自定义框架。

MvcScaffolding 中的其他功能包括：

- 支持C#和 VB 项目
- 支持 Razor 和 ASPX 视图引擎
- 支持将基架导入 ASP.NET MVC 区域和使用自定义视图布局/主控形状
- 可以通过编辑 T4 模板轻松自定义输出
- 你可以使用自定义 PowerShell 逻辑和自定义 T4 模板来添加全新的框架。 这些（及其提供的任何自定义参数）会自动显示在 "控制台" 选项卡的 "完成" 列表中。
- 你可以获取包含不同技术的其他框架的 NuGet 程序包（例如，有一个概念证明，一种用于 LINQ to SQL），并混合搭配它们

ASP.NET MVC 3 工具更新包括对此基架系统的出色 Visual Studio 支持，例如：

- "添加控制器" 对话框现在支持 "创建"、"读取"、"更新" 和 "删除" 控制器操作和相应视图的完全自动基架。 默认情况下，此基架使用 EF Code First 的数据访问代码。
- "添加控制器" 对话框支持通过 NuGet 包（如*MvcScaffolding*）进行*可扩展的基架*。 这允许将自定义基架插入对话框，使你可以为其他数据访问技术（例如 NHibernate，甚至是具有 ODBCDirect 的 JET）创建基架

有关 ASP.NET MVC 3 中的基架的详细信息，请参阅以下资源：

- Steve Sanderson 的文章系列，其中包括： 

    1. [简介：基架 ASP.NET MVC 3 project with the MvcScaffolding package](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [标准用法：典型用例和选项](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [一对多关系](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [基架操作和单元测试](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [覆盖 T4 模板](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [这篇文章：创建自定义框架](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselman 在他的 PDC 2010 讲座中发布[了一篇博客，其中包含 Microsoft "未命名的 Web 喜爱包"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 项目模板

"新建项目" 对话框包含一个复选框 "启用 HTML 5 版本的项目模板"。 这些模板利用 Modernizr 1.7 为底层浏览器中的 HTML 5 和 CSS 3 提供兼容性支持。

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Razor 视图引擎

ASP.NET MVC 3 附带了一个名为 Razor 的新视图引擎，它具有以下优势：

- Razor 语法简洁明了，需要最少的击键数。
- Razor 易于学习，其中部分原因是它基于现有语言，如C#和 Visual Basic。
- Visual Studio 包括 Razor 语法的 IntelliSense 和代码着色。
- Razor 视图可以进行单元测试，而无需运行应用程序或启动 web 服务器。

一些新的 Razor 功能包括：

- `@model` 语法，用于指定传递给视图的类型。
- `@* *@` 注释语法。
- 为整个站点指定一次默认值（例如 `layoutpage`）的功能。
- 用于显示文本的 `Html.Raw` 方法，无需对其进行 HTML 编码。
- 支持在多个视图中共享代码（ *\_viewstart.cshtml*或 *\_viewstart.cshtml*文件）。

Razor 还包括新的 HTML 帮助程序，如下所示：

- `Chart`。 呈现图表，提供与 ASP.NET 4 中的图表控件相同的功能。
- `WebGrid`。 呈现一个数据网格，其中包含分页和排序功能。
- `Crypto`。 使用哈希算法来创建正确的加盐和哈希密码。
- `WebImage`。 呈现图像。
- `WebMail`。 发送电子邮件。

有关 Razor 的详细信息，请参阅以下资源：

- [Scott Guthrie 的博客文章介绍了 Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthrie 的博客文章介绍 @model 关键字](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthrie 的博客文章介绍了 Razor 布局](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API 快速参考](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>支持多个视图引擎

在 ASP.NET MVC 3 中的 "**添加视图**" 对话框中，可以选择要使用的视图引擎，使用 "**新建项目**" 对话框可以指定项目的默认视图引擎。 您可以选择 Web 窗体视图引擎（ASPX）、Razor 或开源视图引擎，例如[Spark](http://sparkviewengine.com/)、 [NHaml](https://code.google.com/p/nhaml/)或[NDjango](http://ndjango.org/)。

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>控制器改进

### <a name="global-action-filters"></a>全局操作筛选器

有时，您需要在操作方法运行之前或操作方法运行之后执行逻辑。 为支持此操作，ASP.NET MVC 2 提供了操作筛选器。 操作筛选器是自定义属性，可提供用于向特定控制器操作方法添加操作前和操作后行为的声明性方法。 但是，在某些情况下，你可能想要指定适用于所有操作方法的操作前或操作后行为。 MVC 3 允许您通过将全局筛选器添加到 `GlobalFilters` 集合来指定全局筛选器。 有关全局操作筛选器的详细信息，请参阅以下资源：

- [在 MVC 3 预览版中，Scott Guthrie 的博客](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC 中的筛选](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>新的 "ViewBag" 属性

MVC 2 控制器支持 `ViewData` 属性，使你能够使用后期绑定字典 API 将数据传递给视图模板。 在 MVC 3 中，你还可以对 `ViewBag` 属性使用略微简单的语法来实现相同的目的。 例如，你可以编写 `ViewBag.Message="text"`，而不是编写 `ViewData["Message"]="text"`。 不需要定义任何强类型类来使用 `ViewBag` 属性。 由于它是动态属性，因此可以直接获取或设置属性，它将在运行时动态解析它们。 在内部，`ViewBag` 属性作为名称/值对存储在 `ViewData` 字典中。 （注意：在 MVC 3 的大多数预发布版本中，`ViewBag` 属性的名称都是 `ViewModel` 属性。）

### <a name="new-actionresult-types"></a>新 "ActionResult" 类型

以下 `ActionResult` 类型和相应的帮助器方法在 MVC 3 中是新增或增强的：

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。 向客户端返回 404 HTTP 状态代码。
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。 返回临时重定向（HTTP 302 状态代码）或永久重定向（HTTP 301 状态代码），具体取决于布尔参数。 与此更改一起，[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)类现在有三种执行永久重定向的方法： `RedirectPermanent`、`RedirectToRoutePermanent`和 `RedirectToActionPermanent`。 这些方法返回 `RedirectResult` 的实例，`Permanent` 属性设置为 "`true`"。
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。 返回用户指定的 HTTP 状态代码。

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript 和 Ajax 改进

默认情况下，MVC 3 中的 Ajax 和验证帮助程序使用不引人注目的 JavaScript 方法。 非引人注目的 JavaScript 避免将内联 JavaScript 注入到 HTML。 这会使你的 HTML 更小、更简洁，并使你可以更轻松地交换或自定义 JavaScript 库。 默认情况下，MVC 3 中的验证帮助器也使用 `jQueryValidate` 插件。 如果需要 MVC 2 行为，可以使用*web.config 文件设置*禁用非引人注目的 JavaScript。 有关 JavaScript 和 Ajax 改进的详细信息，请参阅以下资源：

- [维基百科网站上的非引人注目 JavaScript 的基本简介](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson 的非引人注目 JavaScript Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson 的非引人注目 JavaScript 验证 Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [使用 Razor 和非引人注目 JavaScript 创建 MVC 3 应用程序](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET 网站上的教程）
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>默认情况下启用客户端验证

在 MVC 的早期版本中，需要从视图中显式调用 `Html.EnableClientValidation` 方法才能启用客户端验证。 在 MVC 3 中，这不再是必需的，因为默认情况下会启用客户端验证。 （您可以使用*web.config 文件中的设置*来禁用此设置。）

为了使客户端验证正常工作，你仍需要在你的站点中引用相应的 jQuery 和 jQuery 验证库。 你可以在自己的服务器上托管这些库，或者从 Microsoft 或 Google 等 Cdn 的内容交付网络（CDN）中引用它们。

### <a name="remote-validator"></a>远程验证程序

ASP.NET MVC 3 支持新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)类，使你能够利用 jQuery 验证插件的远程验证程序支持。 这样，客户端验证库就可以自动调用您在服务器上定义的自定义方法，以便执行只能在服务器端执行的验证逻辑。

在下面的示例中，`Remote` 属性指定客户端验证将调用 `UsersController` 类上名为 `UserNameAvailable` 的操作，以便验证 `UserName` 字段。

[!code-csharp[Main](mvc3/samples/sample1.cs)]

下面的示例演示了相应的控制器。

[!code-csharp[Main](mvc3/samples/sample2.cs)]

有关如何使用 `Remote` 特性的详细信息，请参阅 MSDN library 中的[如何：在 ASP.NET MVC 中实现远程验证](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。

### <a name="json-binding-support"></a>JSON 绑定支持

ASP.NET MVC 3 包含内置 JSON 绑定支持，使操作方法可以接收 JSON 编码数据，并将其绑定到操作方法参数。 此功能在涉及客户端模板和数据绑定的方案中很有用。 （客户端模板使你可以通过使用在客户端上执行的模板来设置和显示单个数据项或数据项集。）MVC 3 使你能够轻松地通过发送和接收 JSON 数据的服务器上的操作方法连接客户端模板。 有关 JSON 绑定支持的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览版博客文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)的**JavaScript 和 AJAX 改进**部分。

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>模型验证改进

### <a name="dataannotations-metadata-attributes"></a>"DataAnnotations" 元数据属性

ASP.NET MVC 3 支持 `DataAnnotations` 元数据属性，如 `DisplayAttribute`。

### <a name="validationattribute-class"></a>"ValidationAttribute" 类

`ValidationAttribute` 类在 .NET Framework 4 中得到了改进，以支持一个新的 `IsValid` 重载，该重载提供有关当前验证上下文的详细信息，例如要验证的对象。 这可以实现更丰富的方案，在这些方案中，你可以基于模型的另一个属性验证当前值。 例如，使用 new `CompareAttribute` 特性可以比较模型的两个属性的值。 在下面的示例中，`ComparePassword` 属性必须匹配 `Password` 字段才能有效。

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>验证接口

通过[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)接口，您可以执行模型级别的验证，还可以提供验证错误消息，这些错误消息特定于整个模型的状态，或在模型中的两个属性之间。 在模型绑定时，MVC 3 现在从 `IValidatableObject` 接口检索错误，并使用内置的 HTML 窗体帮助程序在视图中自动标记或突出显示受影响的字段。

[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)接口允许 ASP.NET MVC 在运行时发现验证程序是否支持客户端验证。 此接口已经过设计，以便可以与各种验证框架集成。

有关验证接口的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览版博客文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)中的 "**模型验证改进**" 一节。 （但请注意，博客中的 "IValidateObject" 引用应为 "IValidatableObject"。）

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>依赖关系注入改进

ASP.NET MVC 3 为应用依赖关系注入（DI）以及与依赖关系注入或控制反转（IOC）容器的集成提供了更好的支持。 已在以下区域添加对 DI 的支持：

- 控制器（注册和注入控制器工厂，注入控制器）。
- 视图（注册和注入视图引擎，将依赖项注入到查看页中）。
- 操作筛选器（查找和注入筛选器）。
- 模型联编（注册和注入）。
- 模型验证提供程序（注册和注入）。
- 模型元数据提供程序（注册和注入）。
- 值提供程序（注册和注入）。

MVC 3 支持[公共服务定位器](https://github.com/unitycontainer/commonservicelocator)库和支持该库的 `IServiceLocator` 接口的任何 DI 容器。 它还支持新的 `IDependencyResolver` 接口，使其更易于集成 DI 框架。

有关 MVC 3 中的 DI 的详细信息，请参阅以下资源：

- [有关服务位置的 Brad Wilson 系列博客文章](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>其他新功能

### <a name="nuget-integration"></a>NuGet 集成

ASP.NET MVC 3 在其安装过程中自动安装并启用 NuGet。 NuGet 是一个免费的开源程序包管理器，可让你轻松地在项目中查找、安装和使用 .NET 库和工具。 它适用于所有 Visual Studio 项目类型（包括 ASP.NET Web 窗体和 ASP.NET MVC）。

NuGet 允许维护开源项目的开发人员（例如，Moq、NHibernate、Ninject、StructureMap、NUnit、Windsor、RhinoMocks 和 Elmah 等项目）将其库打包并注册到联机库。 如果 .NET 开发人员想要使用这些库之一来查找包并将其安装在其所使用的项目中，则可以使用此方法。

通过 ASP.NET 3 工具更新，项目模板包括 JavaScript 库预安装的 NuGet 包，因此可以通过 NuGet 更新它们。 还会将实体框架 Code First 预安装为 NuGet 包。

有关 NuGet 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/nuget/)。

### <a name="partial-page-output-caching"></a>部分页面输出缓存

从版本1开始，ASP.NET MVC 支持完整页面响应的输出缓存。 MVC 3 还支持部分页面输出缓存，这使你可以轻松地缓存响应的区域或片段。 有关缓存的详细信息，请参阅[Scott Guthrie 的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)的 "**部分页面输出缓存**" 部分，该部分介绍了 mvc 3 候选发布版和[Mvc 3 发行说明](../whitepapers/mvc3-release-notes.md)的**子操作输出缓存**部分。

### <a name="granular-control-over-request-validation"></a>精细控制请求验证

ASP.NET MVC 具有内置的请求验证，可自动帮助防范 XSS 和 HTML 注入攻击。 但是，有时你需要显式禁用请求验证，例如，如果你想让用户发布 HTML 内容（例如，在博客条目或 CMS 内容中）。 现在可以将[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性添加到模型或查看模型，以便在模型绑定期间对每个属性禁用请求验证。 有关请求验证的详细信息，请参阅以下资源：

- [Scott Guthrie 的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中的 "不**引人注目的 JavaScript 和验证**" 部分。
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>可扩展的 "新建项目" 对话框

在 ASP.NET MVC 3 中，你可以将项目模板、视图引擎和单元测试项目框架添加到 "**新建项目**" 对话框中。

### <a name="template-scaffolding-improvements"></a>模板基架改进

ASP.NET MVC 3 基架模板会更好地标识模型上的主键属性，并对其进行适当处理，而不是在早期版本的 MVC 中处理它们。 （例如，基架模板现在可确保主密钥不会基架为可编辑的窗体字段。）

默认情况下，创建和编辑基架现在使用 `Html.EditorFor` 帮助程序，而不是 `Html.TextBoxFor` 帮助程序。 这会在 "**添加视图**" 对话框生成视图时以数据批注特性的形式改进对模型上的元数据的支持。

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.labelfor" 和 "LabelForModel" 的新重载

添加了新的方法重载，可用于 `LabelFor` 和 `LabelForModel` 帮助器方法。 新重载允许您指定或覆盖标签文本。

### <a name="sessionless-controller-support"></a>无会话控制器支持

在 ASP.NET MVC 3 中，你可以指示你是否希望控制器类使用会话状态，如果为，则指示会话状态应为 "读/写" 还是 "只读"。 有关无会话控制器支持的详细信息，请参阅[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。

### <a name="new-additionalmetadataattribute-class"></a>新 "AdditionalMetadataAttribute" 类

您可以使用[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性来填充模型属性的 `ModelMetadata.AdditionalValues` 字典。 例如，如果视图模型具有只应显示给管理员的属性，则可以批注该属性，如以下示例中所示：

[!code-csharp[Main](mvc3/samples/sample4.cs)]

呈现产品视图模型时，此元数据可用于任何显示或编辑模板。 你需要解释元数据信息。

### <a name="accountcontroller-improvements"></a>AccountController 改进

Internet 项目模板中的 AccountController 已大幅提高。

### <a name="new-intranet-project-template"></a>新的 Intranet 项目模板

包含新的 Intranet 项目模板，该模板启用 Windows 身份验证并删除 AccountController。
