---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619243"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

- [概述](#overview)
- [安装说明](#installation-notes)
- [软件要求](#software-requirements)
- [文档](#documentation)
- [支持](#support)
- [将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新](#upgrading)
- [ASP.NET MVC 3 工具更新（2011年4月12日）](#tu-changes)

    - ["添加控制器" 对话框现在可以使用视图和数据访问代码基架控制器](#tu-AddControllerDialog)
    - ["ASP.NET MVC 3 新建项目" 对话框的改进](#tu-ImprovementsNewDialogBox)
    - [项目模板现在包括 Modernizr 1。7](#tu-Modernizr)
    - [项目模板包括 jQuery、jQuery UI 和 jQuery 验证的更新版本](#tu-UpdatedJQuery)
    - [项目模板现在包括 ADO.NET 实体框架4.1 作为预安装的 NuGet 包](#tu-EF)
    - [项目模板包括 JavaScript 库作为预安装的 NuGet 包](#tu-JavaScriptLibsNuget)
    - [已知问题](#tu-KI)
- [ASP.NET MVC 3 RTM （2011年1月13日）](#MVC3RTM)

    - [更改：已将 jQuery UI 版本更新到 1.8.7](#RTM-1)
    - [更改：已将默认 ModelMetadataProvider 更改回 DataAnnotationsModelMetadataProvider](#RTM-2)
    - 固定 [：粘贴包含空格的 Razor 表达式的一部分将导致其反向](#RTM-3)
    - 固定 [：重命名在编辑器中打开的 Razor 文件将禁用语法着色和 IntelliSense](#RTM-4)
    - [已知问题](#RTM-KI)
    - [重大更改](#RTM-BC)
- [ASP.NET MVC 3 候选发布2（2010年12月10日）](#_Toc2)

    - [项目模板已更改为包含 jQuery sqoop-user-guide-1.4.4、jQuery 验证1.7 和 jQuery UI 1.8.6 y UI 1.8。6](#_Toc2_1)
    - [添加了 "AdditionalMetadataAttribute" 类](#_Toc2_2)
    - [改进的视图基架](#_Toc2_3)
    - [添加了 Html Raw 方法](#_Toc2_3)
    - [重命名为 "ViewModel" 属性，并将 "View" 属性重命名为 "ViewBag"](#_Toc2_4)
    - [已将 "ControllerSessionStateAttribute" 类重命名为 "SessionStateAttribute"](#_Toc2_5)
    - [将 RemoteAttribute "Fields" 属性重命名为 "AdditionalFields"](#_Toc2_6)
    - [已将 "SkipRequestValidationAttribute" 重命名为 "AllowHtmlAttribute"](#_Toc2_7)
    - [更改了 "ValidationMessage" 方法以显示第一个有用的错误消息](#_Toc2_8)
    - [固定 @model 声明，不向文档中添加空白](#_Toc2_9)
    - [添加了 "FileExtensions" 属性以查看引擎，以支持引擎特定的文件名](#_Toc2_10)
    - [修复了 "Html.labelfor" 帮助程序，以便为 "For" 特性发出正确的值](#_Toc2_11)
    - [修复了在模型绑定期间为显式值指定优先级的 "RenderAction" 方法](#_Toc2_12)
    - [重大更改](#_Toc2_BC)
    - [已知问题](#_Toc2_KI)
- [ASP.NET MVC 3 候选发布（2010年11月9日）](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC 中的新功能](#_Toc276711785)
    - [NuGet 包管理器](#_Toc276711786)
    - [改进了 "新建项目" 对话框](#_Toc276711787)
    - [无会话控制器](#_Toc276711788)
    - [新验证属性](#_Toc276711789)
    - ["Html.labelfor" 和 "LabelForModel" 方法的新重载](#_Toc276711790)
    - [子操作输出缓存](#_Toc276711791)
    - ["添加视图" 对话框改进](#_Toc276711792)
    - [精细请求验证](#_Toc276711793)
    - [重大更改](#_Toc276711794)
    - [已知问题](#_Toc276711795)
- [ASP.NET.MVC 3 Beta 说明（Oct 6，2010）](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 Beta 中的新增功能](#0.1__Toc274034215)
    - [NuPack 包管理器](#0.1__Toc274034216)
    - [改进了 "新建项目" 对话框](#0.1__Toc274034217)
    - [在 Razor 视图中指定强类型模型的简化方法](#0.1__Toc274034218)
    - [支持新的 ASP.NET 网页帮助器方法](#0.1__Toc274034219)
    - [其他依赖关系注入支持](#0.1__Toc274034220)
    - [新支持基于 jQuery 的非引人注目 Ajax](#0.1__Toc274034221)
    - [新支持非引人注目的 jQuery 验证](#0.1__Toc274034222)
    - [适用于客户端验证和非引人注目 JavaScript 的新应用程序范围标志](#0.1__Toc274034223)
    - [新支持在视图运行之前运行的代码](#0.1__Toc274034224)
    - [新的对 VBHTML Razor 语法的支持](#0.1__Toc274034225)
    - [更精细地控制 ValidateInputAttribute](#0.1__Toc274034226)
    - [帮助器将下划线转换为使用匿名对象指定的 HTML 属性名称的连字符](#0.1__Toc274034227)
    - [Bug 修复](#0.1__Toc274034228)
    - [重大更改](#0.1__Toc274034229)
    - [已知问题](#0.1__Toc274034230)
- [否认](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>概述

本文档介绍适用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 版本。 ASP.NET MVC 是一个框架，用于开发使用模型-视图-控制器（MVC）模式的 Web 应用程序。 ASP.NET MVC 3 安装程序包含以下组件：

- ASP.NET MVC 3 运行时组件
- ASP.NET MVC 3 Visual Studio 2010 工具
- ASP.NET 网页运行时组件
- ASP.NET 网页 Visual Studio 2010 工具
- 适用于 .NET 的 Microsoft 程序包管理器（NuGet）
- 支持 Razor 语法的 Visual Studio 2010 更新。 （有关详细信息，请参阅知识库文章2483190。）

可在位于 URL 的 ASP.NET 网站上找到 ASP.NET MVC 3 的每个预发行版本的全套发行说明：

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>安装说明

若要使用 Web 平台安装程序（Web PI）安装 ASP.NET MVC 3 RTM，请访问以下页面：

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

或者，可以从以下页面下载适用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 安装程序：

https://go.microsoft.com/fwlink/?LinkID=208140

可以安装 ASP.NET MVC 3，并且可以与 ASP.NET MVC 2 并行运行。

<a id="software-requirements"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET MVC 3 运行时组件需要以下软件：

- .NET Framework 版本4。 

    ASP.NET MVC 3 Visual Studio 2010 工具需要以下软件：
- Visual Studio 2010 或 Visual Web Developer 2010 Express。

<a id="documentation"></a>
## <a name="documentation"></a>文档

以下 URL 的 MSDN 网站上提供了有关 ASP.NET MVC 的文档：

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

有关 ASP.NET MVC 的教程和其他信息可在 ASP.NET 网站的 MVC 页上找到，网址为：

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>支持

这是完全受支持的版本。 有关获取技术支持的信息可在[Microsoft 支持部门网站](https://support.microsoft.com/)上找到。

欢迎将与此版本有关的问题发布到 ASP.NET MVC 论坛中，ASP.NET 社区的成员经常能够在该论坛中提供非正式的支持：

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新

可以在同一台计算机上并行安装 ASP.NET MVC 3 与 ASP.NET MVC 2，这使你可以灵活选择何时将 ASP.NET MVC 2 应用程序升级到 ASP.NET MVC 3。

若要手动将现有 ASP.NET MVC 2 应用程序升级到版本3，请执行以下操作：

1. 在您的计算机上创建新的空 ASP.NET MVC 3 项目。 此项目将包含升级所需的一些文件。
2. 将以下文件从 ASP.NET MVC 3 项目复制到您的 ASP.NET MVC 2 项目的相应位置中。 您将需要更新对 jQuery 库的所有引用以说明新的文件名 (jQuery-1.5.1.js)： 

    - /Views/Web.config
    - /packages.config
    - /scripts/\*.js
    - /Content/themes/\*。\*
3. 将空 ASP.NET MVC 3 项目解决方案的根目录中的 "*包*" 文件夹复制到解决方案的根目录中，该目录位于解决方案的 .sln 文件所在的目录中。
4. 如果 ASP.NET MVC 2 项目包含任何区域，请将/Views/Web.config 文件复制到每个区域的*Views*文件夹中。
5. 在 ASP.NET MVC 2 项目中的两个 web.config 文件中，全局搜索并替换 ASP.NET MVC 版本。 查找以下内容： 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    将它替换为以下代码：

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. 在解决方案资源管理器中，删除对*system.web* （指向版本2中的 DLL）的引用，然后*添加对3.0.0.0 的引用（v* ： v）。
7. 添加对 System.web. .dll 和 System.web... e。 这些程序集位于以下文件夹中： 

    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies
    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies
8. 在“解决方案资源管理器”中右击项目名称，然后选择“卸载项目”。 然后再次右键单击项目名称，然后选择 *"编辑项目*名称 .csproj"。
9. 找到*ProjectTypeGuids*元素，并将 {F85E285D-A4E0-4152-9332-AB1D724D3325} 替换为 {E53F8FEA-EAE0-44A6-8774-FFD645390401}。
10. 保存更改，右击项目，然后选择“重新加载项目”。
11. 在应用程序的根 web.config 文件中，将以下设置添加到*程序集*部分。 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. 如果项目引用使用 ASP.NET MVC 2 编译的任何第三方库，请将以下突出显示的*bindingRedirect*元素添加到 web.config 文件中的 "*配置*" 部分下的应用程序根目录： 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 3 工具更新中的更改

本部分介绍自 ASP.NET MVC 3 RTM 版本以来在 ASP.NET MVC 3 工具更新版本中所做的更改。

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>“添加控制器”对话框现在可以使用视图和数据访问代码创建控制器的基架

创建基架是一种为应用程序快速生成控制器和视图的方法。 生成代码后，你可以对其进行编辑以满足项目的要求。

若要启动 ASP.NET MVC 3 中的 "*添加控制器*" 对话框，请在*解决方案资源管理器*中右键单击 "*控制器*" 文件夹，单击 "*添加*"，然后单击 "*控制器*"。 该对话框已进行了增强，提供了其他创建基架选项。

![](mvc3-release-notes/_static/image1.png)

默认情况下提供了三个可用的创建基架模板。

#### <a name="empty-controller"></a>空控制器

此模板将生成一个空的控制器文件。 此模板等效于不检查 ASP.NET MVC 的以前版本中*的 "创建"、"编辑"、"详细信息" 和 "删除" 方案的添加操作*。 如果选中此选项，则没有进一步可用的选项。

#### <a name="controller-with-empty-readwrite-actions"></a>包含空的读/写操作的控制器

此模板将生成一个控制器文件，其中包含所有必需的操作方法，但这些方法中没有实现代码。 此模板等效于在以前版本的 ASP.NET MVC 中检查 "*创建"、"编辑"、"详细信息" 和 "删除" 方案的 "添加操作*"。 如果选中此选项，则没有进一步可用的选项。

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>包含读/写操作和视图的控制器（使用 Entity Framework）

此模板使您能够快速创建一个可用的数据输入用户界面。 它将生成可处理各种常见要求和方案的代码，如下所示：

- *数据访问*。 生成的代码将读写数据库中的实体。 如果选择现有的数据上下文类，或者允许模板生成新的*DbContext*类，则它适用于实体框架 Code First 方法。 如果选择现有的*ObjectContext*类，还可以使用实体框架 Database First 或 Model First 方法。
- *验证*。 生成的代码将使用 ASP.NET MVC 模型绑定和元数据功能，以便根据在模型类上声明的规则来验证窗体提交。 这包括内置的验证规则，如*Required*和*StringLength*特性以及自定义验证规则。
- 一对多*关系*。 如果您定义模型类之间的一对多外键关系，则生成的代码将生成用于选择相关实体的下拉列表。 例如，您可能会定义下面的后跟“Entity Framework 代码优先”约定的模型类： 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    然后，当你为*product*类基架控制器时，其视图将允许用户为每个*产品*实例选择*类别*对象。

    此模板在 "*添加控制器*" 对话框中启用其他选项。 对于*模型类*，你可以在解决方案中选择任意模型类，确定用户将能够创建或编辑的数据类型：
- 如果您想要使用“Entity Framework 代码优先”，则可选择任意模型类。
- 如果您使用的是“Entity Framework 数据库优先”或“Entity Framework 模型优先”，则一定要选择在您的概念模型中定义的实体类。

对于*数据上下文类*，可以进行以下选择：

- 如果要使用 Code First 并且没有现有的数据上下文类，请选择 "新建数据上下文" * *。 然后，将为您生成一个数据上下文类。
- 如果您想要使用“代码优先”，并且具有一个现有的数据上下文类，则在此处选择该类。 将对它进行更新，以持久保存您已选择的模型类。
- 如果您使用的是“数据库优先”或“模型优先”，则在此处选择您的对象上下文类。

对于“视图”，请选择您想要使用的视图引擎；或者，如果您不想创建任何视图基架，则选择“无”。

你可以选择 "高级" 选择为生成的视图指定其他选项。 例如，您可选择要使用的布局或母版页。

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>“ASP.NET MVC 3 新建项目”对话框的改进

用于创建新的 ASP.NET MVC 3 项目的对话框包含多项改进，如下所示。

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>新的“Intranet 项目”模板

“项目模板”列表包含一个新的“Intranet 应用程序”模板。 此模板包含用于使用 Windows 身份验证而不是 Forms 身份验证构建 Web 应用程序的设置。 因为 intranet 应用程序需要某些无法在项目模板中封装的 IIS 设置，所以该模板包含一个自述文件，其中包含如何使项目模板在 IIS 中工作的说明。 以下 URL 的 MSDN 网站上提供了一个新的 Intranet 应用程序模板的文档：

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>项目模板现在支持 HTML5

新项目对话框现在包含用于向项目模板中添加 HTML5 特定功能的选项。 选择选项会导致生成包含新 HTML5 `<header>`、`<footer>`和 `<navigation>` 元素的视图。

请注意，浏览器的早期版本不支持 HTML5 特定的标记。 为了解决此限制，HTML5 项目模板包含对 Modernizr 库的引用。 （请参见下一节。）

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>项目模板现在包含 Modernizr 1.7

Modernizr 是一个 JavaScript 库，在尚不支持这些功能的浏览器中启用对 CSS 3 和 HTML5 的支持。 此库作为预安装的 NuGet 包包含在 ASP.NET MVC 3 项目的模板中。 有关 Modernizr 的详细信息，请参阅[http://www.modernizr.com/](http://www.modernizr.com/)。

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>项目模板包含 jQuery、jQuery UI 和 jQuery Validation 的更新版本

项目模板现在包含 jQuery 脚本的以下版本：

- jQuery 1.5.1
- jQuery 验证 1.8
- jQuery UI 1.8.11

这些库是作为预安装的 NuGet 包进行包含的。

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>项目模板现在包含 ADO.NET Entity Framework 4.1 作为预安装的 NuGet 包

ADO.NET 实体框架4.1 包括 Code First 功能。 “代码优先”是 ADO.NET Entity Framework 的一种新的开发模式，可作为现有的“数据库优先”和“模型优先”模式的替代方案。

“代码优先”侧重于使用通过 Visual Basic 或 C# 编写的 POCO 类（“纯旧 CLR 对象”）定义您的模型。 然后，可将这些类映射到现有数据库，或者用于生成数据库架构。 可以使用*DataAnnotations*属性或使用流畅 api 提供其他配置。

以下 Url 的 ASP.NET 网站上提供了有关使用 Code Firstwith ASP.NET MVC 的文档：

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>项目模板包含 JavaScript 库作为预安装的 NuGet 包

当你创建新的 ASP.NET MVC 3 项目时，该项目将包含前面提到的 JavaScript 文件（例如，Modernizr 库），方法是使用 NuGet 安装它们，而不是直接将脚本添加到项目模板中的 Scripts 文件夹目录. 这使您能够使用 NuGet，在发布脚本的新版本时将脚本更新为最新版本。

例如，考虑到经常发布新的 jQuery 版本，项目模板中包含的 jQuery 版本可能会在某个时候过期。 但是，由于 jQuery 是作为已安装的 NuGet 包进行包含的，因此，当有更新的 jQuery 版本可用时，在 NuGet 对话框中将会为您发出通知。

由于 jQuery 在文件名中包含版本号，因此，将 jQuery 更新为最新版本还需要更新引用 jQuery 文件的 `<script>` 标记，以使用新文件名。 其他包含的脚本库在脚本名中不包含版本号，因此，可以更轻松地将它们更新到最新版本。

<a id="tu-KI"></a>
## <a name="known-issues"></a>已知问题

- 在某些情况下，安装可能会失败，并出现错误消息 "安装失败，出现错误代码（0x80070643）"。 有关如何解决此问题的信息，请参阅[知识库文章 2531566](https://support.microsoft.com/kb/2531566)。
- 用于添加控制器的创建基架功能不会为利用 Entity Framework 内的实体继承支持的实体创建基架。 例如，给定*学生*类继承的基本*Person*类，则*student*类的基架将导致生成的代码不进行编译。
- 在解决方案文件夹中创建新的 ASP.NET MVC 3 项目会导致*NullReferenceException*错误。 解决方法是在解决方案的根中创建 ASP.NET MVC 3 项目，然后将其移到解决方案文件夹中。
- 在安装 ReSharper 时，IntelliSense for Razor 语法不起作用。 如果你已安装 ReSharper，并且想要充分利用 ASP.NET MVC 3 中的 Razor IntelliSense 支持，请参阅 Hadi Hariri 博客上的入门[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中讨论了如何将它们一起使用。
- 在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。
- 编辑 Razor 视图（cshtml 或。*vbhtml*文件），视图。 ASP.NET MVC 3 不包括 Razor 视图的任何代码段。aspxselecting ASP.NET MVC 的代码片段将显示
- 如果在未安装 Visual Studio 的计算机上安装适用于 Visual Web Developer Express 的 ASP.NET MVC 3，然后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。 如果在没有 Visual Web Developer 速成版的计算机上安装适用于 Visual Studio 的 ASP.NET MVC 3，然后再安装 Visual Web Developer Express，则会遇到同样的问题。

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM 中的更改

本部分介绍自 RC2 版本以来在 ASP.NET MVC 3 RTM 版本中所做的更改和 bug 修复。

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>更改：已将 jQuery UI 版本更新为1.8。7

Visual Studio 的 ASP.NET MVC 项目模板已更新，以包括 jQuery UI 库的最新版本。 这些模板还包括 jQuery UI 所需的最小资源文件集，如关联的 CSS 和图像文件。

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>更改：已将默认 ModelMetadataProvider 更改回 DataAnnotationsModelMetadataProvider

ASP.NET MVC 3 的 RC2 版本引入了一个*CachedDataAnnotationsMetadataProvider*类，它提供了在现有*DataAnnotationsModelMetadataProvider*类的基础上进行缓存以提高性能。 但是，在此实现中报告了一些 bug，因此更改已还原并移入 MVC 先期备货项目，该项目可在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)中找到。

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>已修复：粘贴包含空格的 Razor 表达式的一部分将导致其反向

在 ASP.NET MVC 3 的预发行版本中，当你将包含空格的 Razor 表达式的一部分粘贴到 Razor 文件中时，结果表达式将会反向。 例如，请考虑以下 Razor 代码块：

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

如果在第一个方法中选择 "第一个参数" 文本，并将其作为参数粘贴到第二个方法中，则结果如下所示：

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

正确的行为是粘贴操作应该导致以下内容：

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

此问题已在 RTM 版本中得到解决，以便在粘贴操作过程中正确保留表达式。

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>已修复：重命名在编辑器中打开的 Razor 文件将禁用语法着色和 IntelliSense

在编辑器窗口中打开文件时，使用解决方案资源管理器重命名 Razor 文件会导致语法突出显示和 IntelliSense 停止为该文件工作。 这是固定的，以便在重命名后保留突出显示和 IntelliSense。

<a id="RTM-KI"></a>
## <a name="known-issues"></a>已知问题

- 如果在 NuGet 包管理器控制台打开时关闭 Visual Studio 2010 SP1 Beta，则 Visual Studio 将崩溃并尝试重新启动。 这会在 Visual Studio 2010 SP1 的 RTM 版本中得到解决。
- ASP.NET MVC 3 安装程序只能安装初始版本的 NuGet 包管理器。 安装初始版本后，可以使用 Visual Studio 扩展管理器安装和更新 NuGet。 如果已安装 NuGet，请前往 Visual Studio 扩展库，更新到最新版本的 NuGet。
- 在解决方案文件夹中创建新的 ASP.NET MVC 3 项目会导致*NullReferenceException*错误。 解决方法是在解决方案的根中创建 ASP.NET MVC 3 项目，然后将其移到解决方案文件夹中。
- 安装程序所需的时间可能比以前版本的 ASP.NET MVC 长得多。 这是因为它会更新 Visual Studio 2010 的组件。
- 在安装 ReSharper 时，IntelliSense for Razor 语法不起作用。 如果你已安装 ReSharper，并且想要充分利用 ASP.NET MVC 3 中的 Razor IntelliSense 支持，请参阅 Hadi Hariri 博客上的入门[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中讨论了如何将它们一起使用。
- 使用 ASP.NET MVC 3 的 Beta 版创建的 CCSHTML 和 VBHTML 视图没有正确设置其生成操作，这会导致在发布项目时省略这些视图类型。 应将这些文件的 "生成操作" 值设置为 "内容"。 ASP.NET MVC 3 RTM 修复了新文件的这一问题，但没有更正使用预发行版本创建的项目的现有文件的设置。
- ![](mvc3-release-notes/_static/image3.png)
- 在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。
- 编辑 Razor 视图（cshtml 文件）时，Visual Studio 中的 "转向控制器" 菜单项将不可用，且没有代码段。
- 如果在未安装 Visual Studio 的计算机上安装适用于 Visual Web Developer Express 的 ASP.NET MVC 3，然后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。 如果在没有 Visual Web Developer 速成版的计算机上安装适用于 Visual Studio 的 ASP.NET MVC 3，然后再安装 Visual Web Developer Express，则会遇到同样的问题。

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>重大更改

- 在以前版本的 ASP.NET MVC 中，操作筛选器根据请求创建，但在少数情况下除外。 此行为从来都不是保证的行为，但只是实现详细信息，筛选器的协定是将它们视为无状态。 在 ASP.NET MVC 3 中，筛选器的缓存更严格。 因此，任何自定义操作筛选器都不正确地存储实例状态。
- 对于具有相同*顺序*值的异常筛选器，异常筛选器的执行顺序已更改。 在 ASP.NET MVC 2 及更早版本中，与操作方法上的异常筛选器具有相同*顺序*值的异常筛选器在操作方法上的异常筛选器之前执行。 如果未指定*顺序*值应用异常筛选器，通常会出现这种情况。 在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。 与早期版本一样，如果显式指定*order*属性，则筛选器将按指定顺序运行。
- 名为*FileExtensions*的新属性已添加到*VirtualPathProviderViewEngine*基类。 当 ASP.NET 按路径（而不是按名称）查找视图时，仅考虑此新属性所指定的列表中包含的文件扩展名的视图。 这是应用程序中的一项重大更改，其中注册了自定义生成提供程序，以便为 Web 窗体视图启用自定义文件扩展名，并使用完整路径而不是名称来引用这些视图。 解决方法是修改*FileExtensions*属性的值，使之包括自定义文件扩展名。
- 直接实现*IControllerFactory*接口的自定义控制器工厂实现必须提供已添加到此版本中的接口的新*GetControllerSessionBehavior*方法的实现。 通常，建议您不要直接实现此接口，而是从*DefaultControllerFactory*派生您的类。

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 RC2 中的更改

本部分介绍自 RC 版本以来在 ASP.NET MVC 3 RC2 版本中所做的更改（新增功能和 bug 修复）。

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>项目模板已更改为包含 jQuery sqoop-user-guide-1.4.4、jQuery 验证1.7 和 jQuery UI 1.8。6

ASP.NET MVC 3 的项目模板现在包含 jQuery、jQuery 验证和 jQuery UI 的最新版本。 jQuery UI 是项目模板的新增补充，提供有用的用户界面小组件。 有关 jQuery UI 的详细信息，请访问其主页： [http://jqueryui.com/](http://jqueryui.com/)。

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>添加了 "AdditionalMetadataAttribute" 类

可以使用*AdditionalMetadataAttribute*类来填充模型属性的*AdditionalValues*字典。

例如，假设视图模型的属性仅应显示给管理员。 该模型可以使用 AdminOnly 作为键，并使用新属性进行批注，如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

呈现产品视图模型时，此元数据可用于任何显示或编辑模板。 它由应用程序开发人员来解释元数据信息。

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>改进的视图基架

用于基架视图的 T4 模板现在可生成对模板帮助器方法（例如*html.editorfor* ）的调用，而不是*TextBoxFor*的帮助器。 当 "添加视图" 对话框生成视图时，此更改以数据批注特性的形式改进对模型上的元数据的支持。

"添加视图" 基架还包括根据约定，改进了模型中的主键信息的检测和使用情况。 例如，"添加视图" 对话框使用此信息来确保不将主键值基架为可编辑的窗体字段。

默认的编辑和创建模板包括对客户端验证所需的 jQuery 脚本的引用。

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>添加了 Html Raw 方法

默认情况下，Razor 视图引擎对所有值进行 HTML 编码。 例如，下面的代码段对问候语变量中的 HTML 进行编码，使其在页面中显示为 `<strong>Hello World!</strong>`。

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

当已知内容安全时，新的 *.html*方法会提供一种简单的方法来显示未编码的 Html。 下面的示例显示相同的字符串，但该字符串呈现为标记：

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>重命名为 "ViewModel" 属性，并将 "View" 属性重命名为 "ViewBag"

以前， *Controller*对应的*ViewModel*属性指向视图的*视图*属性。 这两个属性都提供使用动态属性访问器语法访问*ViewDataDictionary*对象的值的方法。 这两个属性都已重命名为相同，以避免混淆并使其更一致。

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>已将 "ControllerSessionStateAttribute" 类重命名为 "SessionStateAttribute"

ASP.NET MVC 3 的 RC 版本中引入了*ControllerSessionStateAttribute*类。 该属性已重命名为更简洁。

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>将 RemoteAttribute "Fields" 属性重命名为 "AdditionalFields"

*RemoteAttribute*类的 "*字段*" 属性导致用户之间出现一些混淆。 将该属性重命名为*AdditionalFields*可阐明其意图。

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>已将 "SkipRequestValidationAttribute" 重命名为 "AllowHtmlAttribute"

*SkipRequestValidationAttribute*属性已重命名为*AllowHtmlAttribute* ，以更好地表示其预期用途。

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>更改了 "ValidationMessage" 方法以显示第一个有用的错误消息

*ValidationMessage*方法已修复，以便显示第一个有用的错误消息，而不只是显示第一个错误。

在模型绑定过程中，可以从多个源填充*ModelState*字典，其中包含有关属性的错误消息，包括从模型本身（如果它实现*IValidatableObject*）、应用于属性的验证特性，以及在访问属性时引发的异常。

当*ValidationMessage*方法显示验证消息时，它会跳过包含异常的模型状态条目，因为这些条目通常不适用于最终用户。 相反，方法会查找不与异常相关联的第一条验证消息，并显示该消息。 如果未找到这样的消息，则默认为与第一个异常相关联的一般错误消息。

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>固定 @model 声明，不向文档中添加空白

在早期版本中，视图顶部的 `@model` 声明向呈现的 HTML 输出添加了一个空行。 这是固定的，因此声明不会引入空白。

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>添加了 "FileExtensions" 属性以查看引擎，以支持引擎特定的文件名

视图引擎可以使用显式视图路径返回视图，如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

第一个视图引擎始终尝试呈现视图。 默认情况下，Web 窗体视图引擎是第一个视图引擎;由于 Web 窗体引擎无法呈现 Razor 视图，因此将发生错误。 视图引擎现在具有一个*FileExtensions*属性，用于指定所支持的文件扩展名。 当 ASP.NET 确定视图引擎是否可以呈现文件时，将检查此属性。 这是一项重大更改，并在本文档的 "[重大更改](#_Toc2_BC)" 部分中提供了更多详细信息。

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>修复了 "Html.labelfor" 帮助程序，以便为 "For" 特性发出正确的值

修复了一个 bug，其中*html.labelfor*方法为与*输入*元素的*name*属性（而不是其 ID）匹配的*获取*属性。 根据 W3C， *for*特性应与*输入*元素的 ID 匹配。

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>修复了在模型绑定期间为显式值指定优先级的 "RenderAction" 方法

在早期版本中，在子操作内的模型绑定期间，将忽略传递给*RenderAction*方法的显式值，以支持当前窗体值。 此修补程序确保在模型绑定期间显式值优先。

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>重大更改

- 在以前版本的 ASP.NET MVC 中，操作筛选器是根据请求创建的，但在少数情况下除外。 此行为从来都不是保证的行为，但只是实现详细信息，筛选器的协定是将它们视为无状态。 在 ASP.NET MVC 3 中，筛选器的缓存更严格。 因此，任何自定义操作筛选器都不正确地存储实例状态。
- 对于具有相同*顺序*值的异常筛选器，异常筛选器的执行顺序已更改。 在 ASP.NET MVC 2 及更早版本中，在执行操作方法上的异常筛选器之前，控制器上的异常筛选器的*顺序*值与操作方法上的相同。 如果未指定*顺序*值应用了异常筛选器，通常会出现这种情况。 在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。 与早期版本一样，如果显式指定*order*属性，则筛选器将按指定顺序运行。
- 名为*FileExtensions*的新属性已添加到*VirtualPathProviderViewEngine*基类。 当 ASP.NET 按路径（而不是按名称）查找视图时，仅考虑此新属性所指定的列表中包含的文件扩展名的视图。 这是应用程序中的一项重大更改，其中注册了自定义生成提供程序，以便为 Web 窗体视图启用自定义文件扩展名，并使用完整路径而不是名称来引用这些视图。 解决方法是修改*FileExtensions*属性的值，使之包括自定义文件扩展名。
- 直接实现*IControllerFactory*接口的自定义控制器工厂实现必须提供已添加到此版本中的接口的新*GetControllerSessionBehavior*方法的实现。 通常，建议您不要直接实现此接口，而是从*DefaultControllerFactory*派生您的类。

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>已知问题

- ASP.NET MVC 3 安装程序只能安装初始版本的 NuGet 包管理器。 安装初始版本后，可以使用 Visual Studio 扩展管理器安装和更新 NuGet。 如果已安装 NuGet，请前往 Visual Studio 扩展库，更新到最新版本的 NuGet。
- 在解决方案文件夹中创建新的 ASP.NET MVC 3 项目会导致*NullReferenceException*错误。 解决方法是在解决方案的根中创建 ASP.NET MVC 3 项目，然后将其移到解决方案文件夹中。
- 安装程序所需的时间可能比以前版本的 ASP.NET MVC 长得多。 这是因为它会更新 Visual Studio 2010 的组件。
- 在安装 ReSharper 时，IntelliSense for Razor 语法不起作用。 如果你已安装 ReSharper，并且想要利用 ASP.NET MVC 3 RC2 中的 Razor IntelliSense 支持，请参阅 Hadi Hariri 博客上的入门[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中讨论了如何将它们一起使用。
- 使用 ASP.NET MVC 3 的 Beta 版创建的 CSHTML 和 VBHTML 视图没有正确设置其生成操作，这会导致在发布项目时省略这些视图类型。 应将这些文件的*生成操作*值设置为 "内容"。 ASP.NET MVC 3 RC2 修复了新文件的这一问题，但并不更正使用 Beta 版本创建的项目的现有文件的设置。![](mvc3-release-notes/_static/image4.png)
- 在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。
- 编辑 Razor 视图（cshtml 文件）时，Visual Studio 中的 "转向控制器" 菜单项将不可用，且没有代码段。
- 如果在未安装 Visual Studio 的计算机上安装适用于 Visual Web Developer Express 的 ASP.NET MVC 3，然后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。 如果在没有 Visual Web Developer 速成版的计算机上安装适用于 Visual Studio 的 ASP.NET MVC 3，然后再安装 Visual Web Developer Express，则会遇到同样的问题。
- 如果已安装 ASP.NET MVC 3 RC 2，则安装它不会更新 NuGet。 若要升级 NuGet，请访问 Visual Studio 扩展管理器，该管理器应显示为可用更新。 你可以从此处将 NuGet 升级到最新版本。

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 候选发布

ASP.NET MVC 候选发布版于2010年11月9日发布。

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC 中的新功能

本部分介绍自 Beta 版本后 ASP.NET MVC 3 RC 版本中引入的功能。

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet 程序包管理器

ASP.NET MVC 3 包括 NuGet 包管理器（以前称为 NuPack），这是用于向 Visual Studio 项目添加库和工具的集成包管理工具。 此工具可自动执行开发人员在源树中获取库所需的步骤。

在 Visual Studio 2010、Visual Studio 上下文菜单和一组 PowerShell cmdlet 中，你可以使用 NuGet 作为命令行工具，作为集成的控制台窗口。

有关 NuGet 的详细信息，请参阅[Nuget 文档](https://docs.microsoft.com/nuget/)。

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>改进了 "新建项目" 对话框

创建新项目时，"新建项目" 对话框现在允许你指定视图引擎以及 ASP.NET MVC 项目类型。

![](mvc3-release-notes/_static/image5.png)

此版本包含了对修改对话框中列出的模板和视图引擎列表的支持。

默认模板如下所示：

空。 包含 ASP.NET MVC 项目的最小文件集，其中包括 ASP.NET MVC 项目的默认目录结构、包含默认 ASP.NET MVC 样式的 web.config 文件以及包含默认 JavaScript 文件的脚本目录。

Internet 应用程序。 包含演示如何将成员资格提供程序与 ASP.NET MVC 一起使用的示例功能。

对话框中显示的项目模板的列表在 Windows 注册表中指定。

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>无会话控制器

新的*ControllerSessionStateAttribute*通过指定[SessionState. SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)枚举值，使你能够更好地控制控制器的会话状态行为。

下面的示例演示如何关闭对控制器的所有请求的会话状态。

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

下面的示例演示如何为控制器的所有请求设置只读会话状态。

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>新验证属性

#### <a name="compareattribute"></a>CompareAttribute

使用 new *CompareAttribute*验证特性可以比较模型的两个不同属性的值。 在下面的示例中， *ComparePassword*属性必须与*密码*字段匹配才能有效。

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

新的*RemoteAttribute*验证属性利用 jQuery 验证插件的远程验证程序，这使得客户端验证能够在执行实际验证逻辑的服务器上调用方法。

在下面的示例中， *UserName*属性应用了*RemoteAttribute* 。 在编辑视图中编辑此属性时，客户端验证将调用*UsersController*类上名为*UserNameAvailable*的操作，以便验证此字段。

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

下面的示例演示了相应的控制器。

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

默认情况下，应用该特性的属性名称将作为查询字符串参数发送到操作方法。

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>"Html.labelfor" 和 "LabelForModel" 方法的新重载

添加了*html.labelfor*和*LabelForModel*方法的新重载，使您可以指定标签文本。 下面的示例演示如何使用这些重载。

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>子操作输出缓存

*OutputCacheAttribute*支持通过使用*RenderAction*或*html. 操作*帮助器方法调用的子操作的输出缓存。 下面的示例演示了一个调用另一个操作的视图。

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*GetDate*操作用*OutputCacheAttribute*批注：

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

此代码运行时，对 Html. Action （"GetDate"）的调用的结果缓存了100秒。

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>"添加视图" 对话框改进

添加强类型视图时，"添加视图" 对话框现在会筛选出比以前版本更多的不适用类型，例如许多核心 .NET Framework 类型。 此外，该列表现在按类名而不是完全限定的类型名称进行排序，这使得查找类型变得更加容易。 例如，类型名称现在显示为，如下例所示：

ClassName （命名空间）

在以前的版本中，这会显示如下：

Namespace.ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>精细请求验证

*ValidateInputAttribute*的*Exclude*属性不再存在。 相反，若要在模型绑定期间为模型的特定属性跳过请求验证，请使用新的*SkipRequestValidationAttribute*。

例如，假设使用操作方法编辑博客文章：

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

下面的示例演示博客文章的视图模型。

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

当用户提交 Description 属性的某些标记时，模型绑定将由于请求验证而失败。 若要在博客文章说明的模型绑定期间禁用请求验证，请将*SkipRequpestValidationAttribute*应用到属性，如以下示例中所示：。

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

或者，若要关闭模型的每个属性的请求验证，请将值为*false*的*ValidateInputAttribute*应用到操作方法：

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>重大更改

- 对于具有相同*顺序*值的异常筛选器，异常筛选器的执行顺序已更改。 在 ASP.NET MVC 2 及更早版本中，与操作方法上的异常筛选器*顺序*相同的异常筛选器在操作方法上的异常筛选器之前执行。 如果未指定*顺序*值应用了异常筛选器，通常会出现这种情况。 在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。 与早期版本一样，如果显式指定*order*属性，则筛选器将按指定顺序运行。
- 向*VirtualPathProviderViewEngine*基类添加了名为*FileExtensions*的新属性。 当按路径（而不是按名称）查找视图时，仅考虑此新属性所指定的列表中包含的文件扩展名的视图。 这是对注册自定义生成提供程序以启用 web 窗体视图的自定义文件扩展名，并使用完整路径而不是名称引用这些视图的用户的重大更改。 解决方法是修改*FileExtensions*属性的值，使之包括自定义文件扩展名。

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>已知问题

- 安装程序要完成的时间可能比以前版本的 ASP.NET MVC 长得多，因为它会更新 Visual Studio 2010 的组件。
- 选择 astrongly 类型化视图基架只写属性时，"添加视图" 基架。 基架应始终忽略这些。 "添加视图" 对话框也会在生成 "编辑" 或 "创建" 视图时基架只读属性。 只读属性应该只基架显示和列表视图。
- 当 ASP.NET MVC 3 与异步 CTP 一起安装时，调试不起作用。 ASP.NET MVC 3 不能与 Async CTP 并行安装。 卸载 Async CTP 以修复调试。 有关更多详细信息，请阅读[此博客文章](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)，了解如何卸载 ASP.NET MVC 3 RC 的所有部分。
- 当安装 Resharper 时，Razor Intellisense 不起作用。 如果你已安装 ReSharper，并且想要充分利用 ASP.NET MVC 3 RC 中的 Razor intellisense 支持，请阅读[此博客文章](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)，其中介绍了如何立即使用它们。
- 用 ASP.NET MVC 3 的 Beta 版创建的 CSHTML 和 VBHTML 视图没有正确的生成操作，因此不会将其从发布中忽略。 应将这些文件的*生成操作*设置为 "内容"。 ASP.NET MVC 3 RC 修复了新文件的这一问题，但并不更正使用 Beta 版本创建的项目的现有文件的设置。
- 安装程序要完成的时间可能比以前版本的 ASP.NET MVC 长得多，因为它会更新 Visual Studio 2010 的组件。
- 选择 "编辑" 强类型视图时，"添加视图" 基架基架只读属性。 同样，只写属性基架用于 "显示" 视图。
- 在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。
- 安装 Visual Studio Async CTP 会导致与在 ASP.NET MVC 3 工具安装过程中包含的 Razor 版本发生冲突。 请确保不要在同一台计算机上同时安装 Visual Studio Async CTP 和 Razor 版本。
- 编辑 Razor 视图（cshtml 文件）时，Visual Studio 中的 "转向控制器" 菜单项将不可用，且没有代码段。

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 Beta

ASP.NET MVC 3 Beta 于2010年10月6日发布。 以下说明特定于 Beta 版本，并受上述 ASP.NET MVC 3 候选版本部分中提到的任何更新或更改的限制。

## <a id="0.1__Toc274034215"></a>New Featuresin ASP.NET MVC 3 Beta

<a id="0.1__Default_validation_system"></a>本部分介绍 ASP.NET MVC 3 Beta 版本中引入的功能。

### <a id="0.1__Toc274034216"></a>NuGet 包管理器

ASP.NET MVC 3 包括 NuGet 包管理器，它是一个用于向 Visual Studio 项目添加库和工具的集成包管理工具。 大多数情况下，它会自动执行开发人员在源树中获取库所需的步骤。

你可以使用 NuGet 作为命令行工具，作为 Visual Studio 2010 内的集成控制台窗口，从 Visual Studio 上下文菜单，以及 PowerShell cmdlet 集。

有关 NuGet 的详细信息，请参阅[Nuget 文档](https://docs.microsoft.com/nuget/)。

### <a id="0.1__Toc274034217"></a>改进了 "新建项目" 对话框

创建新项目时，"新建项目" 对话框现在允许你指定视图引擎以及 ASP.NET MVC 项目类型。

![](mvc3-release-notes/_static/image6.png)

此版本不包含对修改对话框中列出的模板和视图引擎列表的支持。

默认模板如下所示：

空。 包含 ASP.NET MVC 项目的一组最小文件，其中包括 ASP.NET MVC 项目的默认目录结构、包含默认 ASP.NET MVC 样式的小 MVC 文件和包含默认 JavaScript 文件的脚本目录。

Internet 应用程序。 包含演示如何在 ASP.NET MVC 内使用成员资格提供程序的示例功能。

### <a id="0.1__Toc274034218"></a>在 Razor 视图中指定强类型模型的简化方法

为类型强类型的 Razor 视图指定模型类型的方式已通过使用适用于 CSHTML 视图的 new @model 指令和用于 VBHTML 视图的 @ModelType 指令进行了简化。 在早期版本的 ASP.NET MVC 中，你将以这种方式为 Razor 视图指定强类型模型：

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

在此版本中，可以使用以下语法：

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>支持新的 ASP.NET 网页帮助器方法

新的 ASP.NET 网页技术包括一组帮助器方法，这些方法可用于将常用功能添加到视图和控制器。 ASP.NET MVC 3 支持在控制器和视图中使用这些帮助器方法（如果适用）。 这些方法包含在 System.web. 助手程序集中。 下表列出了几个 ASP.NET 网页帮助器方法。

| **Helper** | **说明** |
| --- | --- |
| Chart | 在视图中呈现图表。 包含诸如 ToWebImage、Chart 和 Chart 等方法。 |
| 加密 | 使用哈希算法来创建正确的加盐和哈希密码。 |
| WebGrid | 以网格的形式呈现对象（通常为数据库中的数据）的集合。 支持分页和排序。 |
| WebImage | 呈现图像。 |
| WebMail | 发送电子邮件。 |

以下 URL 中的 ASP.NET Razor 语法文档中提供了列出帮助程序和基本语法的快速参考主题：

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>其他依赖关系注入支持

当前版本是在 ASP.NET MVC 3 预览版1版本的基础上生成的，它包括对两个新服务和四个现有服务的额外支持，并改进了对依赖项解析和常见服务定位符的支持。

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>用于细化控制器实例化的新的 IControllerActivator 接口

新的 IControllerActivator 接口可更精细地控制通过依赖关系注入来实例化控制器的方式。 下面的示例演示了接口：

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

这与控制器工厂的角色比较。 控制器工厂是 IControllerFactory 接口的实现，该接口负责定位控制器类型并实例化该控制器类型的实例。

控制器激活程序只负责实例化控制器类型的实例。 它们不执行控制器类型查找。 找到正确的控制器类型后，控制器工厂应委托给 IControllerActivator 的实例以处理控制器的实际实例化。

DefaultControllerFactory 类具有接受 IControllerFactory 实例的新构造函数。 这使你可以应用依赖关系注入来管理控制器创建的这个方面，而无需覆盖默认的控制器类型查找行为。

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>Iservicelocator.getinstance 接口已替换为 IDependencyResolver

根据社区反馈，ASP.NET MVC 3 Beta 版本已将 Iservicelocator.getinstance 接口的使用替换为特定于 ASP.NET MVC 需求的简化 IDependencyResolver 接口。 下面的示例演示了新的接口：

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

作为此更改的一部分，ServiceLocator 类也被替换为 DependencyResolver 类。 依赖关系解析程序的注册类似于早期版本的 ASP.NET MVC：

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

此接口的实现应只委托到基础依赖关系注入容器，以便为请求的类型提供注册的服务。

当没有所请求类型的注册服务时，ASP.NET MVC 需要此接口的实现以从 GetService 返回 null，并从 GetServices 返回一个空集合。

新的 DependencyResolver 类允许注册实现新的 IDependencyResolver 接口或公共服务定位器接口（Iservicelocator.getinstance）的类。 有关常见服务定位符的详细信息，请参阅[GitHub 上的 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)。

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>用于细化视图页面实例化的新 IViewActivator 界面

新的 IViewPageActivator 接口可更精细地控制通过依赖关系注入来实例化视图页面的方式。 这同时适用于 WebFormView 实例和 RazorView 实例。 下面的示例演示了新的接口：

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

这些类现在接受 IViewPageActivator 构造函数参数，该参数允许你使用依赖关系注入来控制如何实例化 ViewPage、ViewUserControl 和 WebViewPage 类型。

#### <a name="new-dependency-resolver-support-for-existing-services"></a>新的依赖关系解析程序支持现有服务

新版本包括对以下服务的依赖关系解析支持：

- 模型验证提供程序。 可在依赖关系解析程序中注册实现 ModelValidatorProvider 的类，系统会将这些类用于支持客户端和服务器端验证。
- 模型元数据提供程序。 可在依赖关系解析程序中注册实现 ModelMetadataProvider 的单一类，系统会将其用于为模板化和验证系统提供元数据。
- 值提供程序。 可在依赖关系解析程序中注册实现 ValueProviderFactory 的类，系统将使用这些类来创建在模型绑定期间由控制器使用的值提供程序。
- 模型联编。 可在依赖关系解析程序中注册实现 IModelBinderProvider 的类，系统将使用这些类来创建模型绑定系统所使用的模型联编程序。

### <a id="0.1__Toc274034221"></a>新支持基于 jQuery 的非引人注目 Ajax

ASP.NET MVC 包含 Ajax helper 方法，如下所示：

- Ajax.ActionLink
- Ajax.RouteLink
- Ajax.BeginForm
- Ajax.BeginRouteForm

这些方法使用 JavaScript 在服务器上调用操作方法，而不是使用完全回发。 此功能已更新，以不引人注目的方式利用 jQuery。 这些帮助器方法使用*数据 ajax*前缀发出 HTML5 特性，而不是 intrusively 发出内联客户端脚本。 然后，通过引用相应的 JavaScript 文件，将行为应用到标记。 请确保引用以下 JavaScript 文件：

- jquery-1.4.1.js
- jquery.unobtrusive.ajax.js

默认情况下，在 ASP.NET MVC 3 新项目模板中的 web.config 文件中启用此功能，但对于现有项目，默认情况下已禁用。 有关详细信息，请参阅本文档后面的[为客户端验证和非引人注目的 JavaScript 添加应用程序范围标志](#0.1_AddedApplicationWideFlagsForClientValida)。

### <a id="0.1__Toc274034222"></a>新支持非引人注目的 jQuery 验证

默认情况下，ASP.NET MVC 3 Beta 以不引人注目的方式使用 jQuery 验证来执行客户端验证。 若要启用非介入式客户端验证，请在视图中执行类似于下面的调用：

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

这需要将 ViewContext 属性设置为 true，通过进行以下调用，可以执行此操作：

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

此外，请确保引用以下 JavaScript 文件。

- jquery-1.4.1.js
- jquery.validate.js
- jquery.validate.unobtrusive.js

默认情况下，在 ASP.NET MVC 3 新项目模板中的 web.config 文件中启用此功能，但对于现有项目，默认情况下已禁用。 有关详细信息，请参阅本文档后面的[用于客户端验证和非引人注目 JavaScript 的新应用程序范围标志](#0.1_AddedApplicationWideFlagsForClientValida)。

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>适用于客户端验证和非引人注目 JavaScript 的新应用程序范围标志

可以使用 HtmlHelper 类的静态成员全局启用或禁用客户端验证和非引人注目的 JavaScript，如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

默认情况下，默认项目模板启用非引人注目的 JavaScript。 你还可以使用以下设置在应用程序的根 web.config 文件中启用或禁用这些功能：

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

由于可以在默认情况下启用这些功能，因此会向 HtmlHelper 类引入新的重载，以允许你重写默认设置，如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

为了向后兼容，默认情况下，这两种功能都处于禁用状态。

### <a id="0.1__Toc274034224"></a>新支持在视图运行之前运行的代码

你现在可以将名为 \_viewstart.cshtml （或 \_viewstart.cshtml）的文件放在 Views 目录中，并向其添加将在该目录及其子目录中的多个视图之间共享的代码。 例如，可以将以下代码放入 ~/Views 文件夹中的 \_viewstart.cshtml 页面：

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

这会在 Views 文件夹及其所有子文件夹中以递归方式设置每个视图的布局页。 呈现视图时，\_viewstart.cshtml 文件中的代码在视图代码运行之前运行。 \_viewstart.cshtml 代码适用于该文件夹中的每个视图。

默认情况下，\_viewstart.cshtml 文件中的代码也适用于任何子文件夹中的视图。 但是，各个子文件夹可以具有其自己的 \_viewstart.cshtml 文件版本;在这种情况下，本地版本优先。 例如，若要运行 HomeController 的所有视图通用的代码，请在 ~/Views/Home 文件夹中放置一个 \_viewstart.cshtml 文件。

### <a id="0.1__Toc274034225"></a>新的对 VBHTML Razor 语法的支持

上一个 ASP.NET MVC 预览包括对使用基于的 Razor 语法的视图C#的支持。 这些视图使用 # 文件扩展名。 作为支持 Razor 的日常工作的一部分，ASP.NET MVC 3 Beta 引入了对 Visual Basic 中的 Razor 语法的支持，该文件使用了文件扩展名。

有关在 VBHTML 页中使用 Visual Basic 语法的介绍，请参阅以下 URL 中的教程：

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>更精细地控制 ValidateInputAttribute

ASP.NET MVC 始终包含 ValidateInputAttribute 类，该类调用核心 ASP.NET 请求验证基础结构，以确保传入请求不包含可能的恶意输入。 默认情况下，输入验证处于启用状态。 可以通过使用 ValidateInputAttribute 属性来禁用请求验证，如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

但是，许多 web 应用程序都有需要允许 HTML 的单独窗体字段，而其余字段不应。 ValidateInputAttribute 类现在允许你指定不应包含在请求验证中的字段的列表。

例如，如果您正在开发博客引擎，则您可能希望在 "正文" 和 "摘要" 字段中允许标记。 这些字段可能由两个输入元素表示，每个元素都具有与属性名称（"Body" 和 "Summary"）对应的 name 属性。 若要仅对这些字段禁用请求验证，请在 ValidateInput 类的 Exclude 属性中指定名称（以逗号分隔），如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>帮助器将下划线转换为使用匿名对象指定的 HTML 属性名称的连字符

使用 Helper 方法，你可以使用匿名对象指定属性名称/值对，如以下示例中所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

此方法不允许在属性名称中使用连字符，因为连字符不能用于 ASP.NET 中的属性名称。 但是，连字符对于自定义 HTML5 特性非常重要;例如，HTML5 使用 "data-" 前缀。

同时，下划线不能用于 HTML 中的属性名称，但在属性名称内有效。 因此，如果使用匿名对象指定属性，并且属性名称包含下划线，则 helper 方法会将下划线转换为连字符。 例如，以下 helper 语法使用下划线：

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

当 helper 运行时，上面的示例将呈现以下标记：

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>Bug 修复

Html.editorfor 和 DisplayFor 模板帮助器的默认对象模板现在支持在 DisplayAttribute 属性中指定的顺序。 （在以前的版本中，未使用 Order 设置。）

客户端验证现在支持验证应用了验证属性的重写属性。

默认情况下，JsonValueProviderFactory 已注册。

## <a id="0.1__Toc274034229"></a>重大更改

对于具有相同顺序值的异常筛选器，异常筛选器的执行顺序已更改。 在 ASP.NET MVC 2 及更早版本中，与操作方法上的异常筛选器顺序相同的异常筛选器在操作方法上的异常筛选器之前执行。 如果未指定顺序值应用了异常筛选器，通常会出现这种情况。 在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。 与早期版本一样，如果显式指定 Order 属性，则筛选器将按指定顺序运行。

## <a id="0.1__Toc274034230"></a>已知问题

在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。

Razor 视图没有 IntelliSense 支持或突出显示语法。 预计在 Visual Studio 中对 Razor 语法的支持将包含在更高版本中。

编辑 Razor 视图（CSHTML 文件）时，Visual Studio 中的<a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a> "前往控制器" 菜单项将不可用，且没有代码段。

使用 @model 语法指定强类型的 CSHTML 视图时，将无法识别类型的语言特定的快捷方式。 例如，@model int 将不起作用，但 @model Int32 将起作用。 此错误的解决方法是在指定模型类型时使用实际的类型名称。

使用 @model 语法指定强类型的 CSHTML 视图时（或 @ModelType 指定强类型的 VBHTML 视图）时，不支持可以为 null 的类型和数组声明。 例如，@model int？不受支持。 请改用 `@model Nullable<Int32>`。 也不支持语法 @model string [];请改用 `@model IList<string>`。

将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 时，请确保将以下内容添加到 web.config 文件的 appSettings 节：

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

存在一个已知问题，导致 Forms 身份验证始终将未经身份验证的用户重定向到 ~/Account/Login，忽略 Web.config 中使用的窗体身份验证设置。解决方法是添加以下应用设置。

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>否认

© 2011 Microsoft Corporation. 保留所有权利。 本文档按“原样”提供。 本文档中的信息和表达的观点，包括 URL 和其他 Internet 网站引用，如有更改恕不另行通知。 您自行承担其使用风险。

本文档未向您提供任何 Microsoft 产品中任何知识产权的任何合法权利。 您可为了内部参考目的复制和使用本文档。
