---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: Visual Studio 2013 发行说明 ASP.NET 和 Web 工具 2013.2 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 22d4d4afd6963f23d6cfef1745a859c20b69d599
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505448"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具 2013.2 发行说明

由[Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>安装说明

适用于 Visual Studio 2013.2 的 ASP.NET 和 Web 工具捆绑在主安装程序中，并且可作为[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)的一部分下载。

## <a name="documentation"></a>文档

[ASP.NET](https://www.asp.net/)网站提供了有关 Visual Studio 2013.2 ASP.NET 和 Web 工具的教程和其他信息。

## <a name="software-requirements"></a>软件要求

Visual Studio 2013.2 ASP.NET 和 Web 工具需要 Visual Studio 2013。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio 2013.2 的 ASP.NET 和 Web 工具中的新增功能

以下各节介绍了在版本中引入的功能。

- [一个 ASP.NET 项目模板](#oneaspnet)
- [在 IIS Express 上启动 Web 应用程序时支持 SSL](#ssl)
- [Visual Studio Web 编辑器增强功能](#vswebeditor)
- [浏览器链接](#browserlink)
- [在 Visual Studio 中支持 Azure App Service Web 应用](#waws)
- [创建新的 Web 项目时创建远程 Azure 资源](#AzureResources)
- [Web 发布增强功能](#webpublish)
- [ASP.NET 基架](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web 窗体](#webforms)
- [ASP.NET MVC 5.1。2](#mvc)
- [ASP.NET Web API 2.1。2](#webapi)
- [ASP.NET 网页3.1。2](#webpages)
- [实体框架6。1](#ef)
- [ASP.NET Identity 2.0。0](#identity)
- [Microsoft OWIN 组件](#owin)
- [ASP.NET SignalR 2.0。2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>一个 ASP.NET 项目模板

- 对 ASP.NET 项目模板的更新，以支持帐户确认和密码重置。
- 更新 ASP.NET Web API 模板，以支持使用本地组织帐户进行身份验证。
- ASP.NET SPA 模板现在包含基于 MVC 和服务器端视图的身份验证。 该模板具有只能由经过身份验证的用户访问的 WebAPI 控制器。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>在 IIS Express 上启动 Web 应用程序时支持 SSL

为了消除在 localhost 上浏览和调试 HTTPS 时的安全警告，我们添加了一个对话框，以允许 Internet Explorer 和 Chrome 信任自签名的 IIS express SSL 证书。

例如，web 项目属性可以设置为使用 SSL。 单击 F4 打开 "属性" 对话框。 将 "**已启用 SSL** " 更改为 true。 复制 SSL URL。

![启用 SSL 的属性](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

将 "web 项目" 属性页的 "web" 选项卡设置为使用基于 HTTPS 的 URL （SSL URL 将 `https://localhost:44300/`，除非你之前已创建 SSL 网站。）

![设置项目 URL （HTTPS）](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

按 Ctrl+F5 以运行应用程序。 遵照说明信任 IIS Express 生成的自我签署证书。

![SSL 警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

阅读 "**安全警告**" 对话框，如果要安装代表 localhost 的证书，请单击 **"是"** 。

![安全警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

浏览器中将显示该网站，但不显示证书警告。

![HTTPS 页，无警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox 会使用自己的证书存储区，因此会显示警告。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web 编辑器增强功能

- **新的 json 项目项和编辑器**：我们已将 JSON 项目项和编辑器添加到 Visual Studio。 当前 JSON 编辑器的功能包括着色、语法验证、大括号完成、大纲显示、工具选项设置等。

    ![JSON 编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense 现在支持[JSON 架构](http://json-schema.org/)v3 和 v4。 有一个用于选择现有架构、编辑本地架构路径或只需将项目 JSON 文件拖放到其中以获取相对路径的架构组合框。

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 架构编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **New Sass （SCSS）编辑器**：我们在 VS2013 RTM 中添加了更少的内容，现在有一个 Sass 项目项和编辑器。 Sass 编辑器功能相当于更少的编辑器，包括着色、可变和 Mixin IntelliSense、注释/取消注释、快速信息、格式设置、语法验证、大纲显示、转到定义、颜色选取器、工具选项设置等。

    ![添加新项： SCSS 样式表](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![样式表编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML、Razor、CSS、LESS 和 Sass 文档中的新 URL 选取器：** VS 2013 附带了 Web 窗体页之外的无 URL 选取器。 用于 HTML、Razor、CSS、LESS 和 Sass 编辑器的新 URL 选取器是一个无对话框、熟知的、可理解 "..." 并针对 img 标记和链接筛选文件列表。

    ![图像标记的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![视图的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS 的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **通过添加更多功能来更新编辑器**
- **挖空 Intellisense 升级**：我们添加了一个非标准的挖空语法，用于 VS Intellisense，"ko-VS-editor viewModel：" 语法。 它可用于在页上使用以下形式的注释绑定到多个视图模型：

    ![挖空 Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    我们还添加了对嵌套 ViewModel IntelliSense 的支持，因此，你可以深入了解 ViewModel 上的深层嵌套的对象。

    `<div data-bind="text: foo.bar.baz.etc" />`

    显示的 IntelliSense 是 JavaScript 对象的完整 IntelliSense。

    ![显示完整 JavaScript 对象的 Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML、Razor、CSS、LESS 和 Sass 文档中的新 URL 选取器：在**Web 窗体页面之外没有 URL 选取器附带了 VS 2013。 用于 HTML、Razor、CSS、LESS 和 Sass 编辑器的新 URL 选取器是一个无对话框、熟知的、可理解 "..." 并针对 img 标记和链接筛选文件列表。

    ![图像标记的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![视图的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS 的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>浏览器链接

- 浏览器链接现在支持 HTTPS 连接，并且在仪表板中将列出该链接，前提是该证书受浏览器信任。
- 静态 HTML 源映射
- SPA 支持映射数据
- 自动更新映射数据

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>在 Visual Studio 中支持 Azure App Service Web 应用

- **支持 Azure 登录。**
- **Web 应用的远程调试和远程视图**：现在，我们支持在 "服务器资源管理器" 中的 web 应用内容文件 Azure App Service 和远程视图[中对 web 应用进行远程调试](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>创建新的 Web 项目时创建远程 Azure 资源

在 "新建 web 应用程序" 对话框中添加了一个 Azure ["创建远程资源"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)复选框。 通过选择它，你将能够集成创建新的 web 应用程序的体验、设置用于测试的 Azure 发布站点以及使用几个简单的步骤创建发布配置文件。

![Azure 资源的新项目](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![发布到 Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 发布增强功能

- 提高发布的用户体验。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 基架

- **枚举支持：** 如果模型正在使用枚举，则 MVC Scaffolder 将为 Enum 生成下拉列表。 这会在 MVC 中使用枚举帮助程序。
- **启动支持**：在 MVC 基架中更新 html.editorfor 模板，使其使用启动类。
- **包支持**： Mvc 和 Web api 框架将为 Mvc 和 web api 添加5.1 包

以下屏幕截图演示了基架模型。

- 模型代码：

     ![模型代码](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 编译模型代码，右键单击，然后选择 "**添加**"、"**新建基架项**"。

     ![添加新的基架项](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **使用实体框架选择包含视图的 MVC5 控制器**：

     ![添加具有视图的新 MVC5 控制器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- 使用模型**添加控制器**：

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 检查生成的代码，例如 Views/WeekdayModels/EnumDropDownListFor 包含包含的 `@Html.EnumDropDownListFor`： ![视图](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 运行页面，查看生成的枚举 combobox，请注意，如果值可以为 null，则可以为组合框选择空字符串。 例如，"**创建**" 页会显示以下内容：

    ![允许空字符串的组合框](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM 将于2014年4月发布。 下面是发行说明中的突出要点，请查看[完整的发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.8)，了解有关这些更改的详细信息。

- **目标 Windows Phone 8.1 应用程序**： NuGet 2.8.1 现在支持使用目标框架名字对象 "WindowsPhoneApp"、"WPA"、"WindowsPhoneApp81" 和 "WPA81" 以 Windows Phone 8.1 应用程序为目标。

- **依赖项的修补程序解析**：解决包依赖关系时，NuGet 一直实现了一个策略，该策略选择满足包的依赖项的最低主要和次要包版本。 但与主要和次要版本不同的是，修补程序版本总是解析为最高版本。 尽管此行为是善意的，但它却缺乏了安装具有依赖项的包的确定性。
- **DependencyVersion 开关**：尽管 NuGet 2.8 更改了用于解决依赖项的*默认*行为，但它还在包管理器控制台中通过-DependencyVersion 开关更精确地控制依赖项解析过程。 开关允许将依赖项解析为可能的最低版本（默认行为）、可能的最高版本或最高的次要版本或修补程序版本。 此开关仅适用于 powershell 命令中的安装包。
- **DependencyVersion 特性**：除了上面详细说明的-DependencyVersion 开关外，nuget 还允许在 nuget.exe 文件中设置新属性，以定义默认值（如果未在 "安装包" 的调用中指定-DependencyVersion 开关）。 任何安装包操作的 "NuGet 包管理器" 对话框也会遵守此值。 若要设置此值，请将以下属性添加到 nuget .config 文件：

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **使用-WhatIf 预览 Nuget 操作**：某些 nuget 包可能具有深层依赖项关系图，因此，在安装、卸载或更新操作过程中，它可帮助您首先了解将发生的情况。 NuGet 2.8 添加了标准 PowerShell-如果切换到 "安装包"、"卸载包" 和 "更新包" 命令，则会将应用命令的整个关闭内容可视化。
- **降级包**：安装包的预发布版本以调查新功能并决定回滚到上次稳定版本的情况并不少见。 在 NuGet 2.8 之前，这是卸载预发行包及其依赖项，然后安装早期版本的多步骤过程。 不过，对于 NuGet 2.8，更新包现在会将整个包关闭（例如包的依赖关系树）回滚到以前的版本。
- **开发依赖项**：许多不同类型的功能可作为 NuGet 包提供-包括用于优化开发过程的工具。 这些组件虽然可以有助于开发新包，但在以后发布时，不应将其视为新包的依赖项。 使用 NuGet 2.8，包可以将 nuspec 文件中的自身标识为 developmentDependency。 安装后，还会将此元数据添加到安装包的项目的 package 文件中。 稍后在 nuget.exe 包期间为 NuGet 依赖项分析包 .config 文件时，它将排除标记为开发依赖项的依赖项。
- **不同平台的单独包 .Config 文件**：为多个目标平台开发应用程序时，对于各自的每个生成环境，都有不同的项目文件。 在不同的项目文件中使用不同的 NuGet 包也很常见，因为包具有不同平台的不同级别的支持。 NuGet 2.8 通过为不同于平台的项目文件创建不同的包 .config 文件，为此方案提供了改进的支持。
- **回退到本地缓存**：尽管 nuget 包通常是使用网络连接从远程库[使用的，](http://www.nuget.org)但在很多情况下客户端未连接。 如果没有网络连接，NuGet 客户端将无法成功安装包-即使这些包已在本地 NuGet 缓存中的客户端计算机上。 NuGet 2.8 将自动缓存回退添加到程序包管理器控制台。

    缓存回退功能不需要任何特定的命令参数。 此外，缓存回退当前仅在包管理器控制台中运行-"包管理器" 对话框中当前未使用该行为。
- **Bug 修复**：在更新包-重新安装命令中，所做的主要 Bug 修复之一是性能改进。

    除了这些功能和前面提到的性能修复外，此版本的 NuGet 还包括许多其他 bug 修复。 此版本中解决了181的总问题。 有关 NuGet 2.8 中已修复工作项的完整列表，请查看此版本的[NuGet 问题跟踪](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)程序。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

- Web 窗体模板现在演示如何对 ASP.NET Identity 进行帐户确认和密码重置。
- 实体数据源控件和实体框架6的动态数据提供程序。 有关更多详细信息，请参阅以下 MSDN 博客：[实体框架6的动态数据提供程序和 EntityDataSource 控件](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)。

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [属性路由改进](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [对编辑器模板的启动支持](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [视图中的枚举支持](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [对 MinLength/MaxLength 特性的非引人注目支持](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [支持非引人注目 Ajax 中的 "this" 上下文](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 各种[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1。2

- [全局错误处理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [特性路由增强功能](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [帮助页改进](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute 支持](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [更好地支持异步筛选器](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [客户端格式设置库的查询分析](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 各种[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET 网页3.1。2

- 各种[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>实体框架6。1

对于运行时和工具，实体框架已更新为6.1 版。 实体框架（EF）6.1 是实体框架6的一个小更新，它包含许多 bug 修复和新功能。 有关 EF 6.1 的详细信息，包括有关新功能的文档的链接，请参阅[实体框架版本历史记录](https://msdn.microsoft.com/data/jj574253)。 此版本中的新增功能包括：

- **工具合并**为创建新的 EF 模型提供了一种一致的方法。 此功能扩展了 ADO.NET 实体数据模型向导以支持创建 Code First 模型，包括从现有数据库进行反向工程。 这些功能之前已在 EF Power Tools 中提供 Beta 版质量。
- **处理事务提交失败**提供了新的[CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) ，它利用新引入的截获事务操作的能力。 **CommitFailureHandler**允许在提交事务的同时从连接故障中自动恢复。
- **IndexAttribute**允许通过将属性放置在 Code First 模型中的属性上来指定索引。 然后 Code First 将在数据库中创建相应的索引。
- **公共映射 API**提供对信息 EF 的访问，以了解如何将属性和类型映射到数据库中的列和表。 在以前的版本中，此 API 是内部的。
- **能够通过应用程序/web.config 文件配置侦听器**（允许添加侦听器而无需重新编译应用程序）。
- **DatabaseLogger**是一个新的侦听器，使用它可以轻松地将所有数据库操作记录到文件中。 与上一项功能结合使用，可以轻松地针对已部署的应用程序的数据库操作进行日志记录，而无需重新编译。
- 改进了**迁移模型更改检测**，使基架迁移更准确;还大大增强了更改检测过程的性能。
- **性能改进**，包括在初始化期间降低数据库操作、在更多方案中优化 null 相等性比较、更快速地生成视图（创建模型）以及更有效地具体化具有多个关联的跟踪实体。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0。0

- **双重身份验证**： ASP.NET Identity 现在支持双因素身份验证。 双因素身份验证向用户帐户提供额外的安全层，以防密码泄露。 对于这两个因素代码，还会受到暴力破解攻击。
- **帐户锁定：** 提供一种方法，用于在用户不正确地输入其密码或双因素代码时锁定用户。 可以配置无效的尝试次数和用户的时间跨度。 开发人员可以根据需要关闭特定用户帐户的帐户锁定。
- **帐户确认：** ASP.NET Identity 系统现在支持帐户确认。 这是当今大多数网站中相当常见的方案。在此情况下，当你在网站上注册新帐户时，你需要确认你的电子邮件，然后才能在网站中执行任何操作。 电子邮件确认会很有用，因为它会阻止创建虚假的帐户。 如果你使用电子邮件作为与网站用户（如论坛站点、银行、电子商务或社交网站）进行通信的方法，这将非常有用。
- **密码重置：** 密码重置是一项功能，如果用户忘记了密码，则可以重置密码。
- **安全戳记（注销任何位置）：** 支持在用户更改其密码或任何其他与安全相关的信息（如 Facebook、Google、Microsoft 帐户等）时为用户重新生成安全令牌的方法。 这是为了确保所有用旧密码生成的令牌失效。 在示例项目中，如果更改用户的密码，则会为用户生成一个新的令牌，并使任何以前的令牌失效。 此功能为应用程序提供了额外的安全层，因为在更改密码时，你将从已登录到此应用程序的任何位置（所有其他浏览器）注销。
- **使主键类型适用于用户和角色**：在 ASP.NET Identity 1.0 中，表用户和角色的主键类型为字符串。 这意味着在使用实体框架将 ASP.NET Identity 系统保存在 SQL Server 中时，我们使用的是 nvarchar。 基于传入反馈，在 Stack Overflow 上围绕此默认实现提供了许多讨论。 我们提供了一个扩展性挂钩，你可以在其中指定 "用户" 和 "角色" 表的主密钥。 如果要迁移应用程序，并且应用程序存储的 Userid 是 Guid 或整数，则此扩展性挂钩特别有用。
- **支持用户和角色的 iqueryable**：增加了对 UsersStore 和 RolesStore 上的 iqueryable 的支持，你可以轻松获取用户和角色的列表。
- **支持通过 UserManager 的删除操作**
- **用户名索引**：在 ASP.NET Identity 实体框架实现中，我们通过使用 EF 6.1.0 中的新 IndexAttribute 为用户名添加了唯一索引。 这可以确保用户名始终唯一，而且没有争用条件，因为这种情况下可能会出现重复的用户名。
- **增强型密码验证程序：** ASP.NET Identity 1.0 中提供的密码验证程序是一个非常基本的密码验证程序，只验证最小长度。 有一个新的密码验证程序，使你能够更好地控制密码的复杂性。 请注意，即使你启用了此密码中的所有设置，也建议你为用户帐户启用双重身份验证。
- **IdentityFactory 中间件/CreatePerOwinContext**：

    - **用户管理器**：可使用工厂实现从 OWIN 上下文中获取 UserManager 的实例。 此模式与用于从 OWIN 上下文中获取用于登录和 SignOut 的 AuthenticationManager 类似。 这是一种获取应用程序每个请求的 UserManager 实例的建议方法。
    - **DbContextFactory**： ASP.NET Identity 使用实体框架在 SQL Server 中持久保存标识系统。 为此，标识系统具有对 ApplicationDbContext 的引用。 DbContextFactory 中间件返回每个请求的 ApplicationDbContext 的实例，你可以在应用程序中使用该实例。
- **ASP.NET Identity 示例 nuget 包**：示例 nuget 包可让你更轻松地安装和运行 ASP.NET Identity 的示例，并遵循最佳做法。 这是一个示例 ASP.NET MVC 应用程序。 在生产环境中部署之前，请修改代码以适应你的应用程序。 应在空的 ASP.NET 应用程序中安装该示例。 有关包的详细信息，请参阅以下博客文章：[宣布 ASP.NET Identity 2.0.0 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 组件

此版本中已修复了很多 bug。 有关更多详细信息，请参阅[2.1.0 版本的发行说明](https://katanaproject.codeplex.com/releases/view/113281)。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0。2

此版本中已修复了很多 bug。 有关更多详细信息，请参阅[2.0.2 版本的发行说明](https://github.com/SignalR/SignalR/releases/tag/2.0.2)。
