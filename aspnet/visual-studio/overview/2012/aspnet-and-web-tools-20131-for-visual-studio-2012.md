---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: 适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1 的发行说明 |Microsoft Docs
author: microsoft
description: 本文档介绍 Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的版本。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467102"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 发行说明

由[Microsoft](https://github.com/microsoft)

> 本文档介绍 Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的版本。

## <a name="contents"></a>内容

- [安装说明](#install)
- [软件要求](#requirements)
- Visual Studio 2012 ASP.NET 和 Web 工具2013.1 中的新增功能

    - [Bootstrap](#bootstrap)
    - [模板](#templates)

        - [ASP.NET MVC 5 模板](#mvc5template)
        - [ASP.NET Web API 2 模板](#apitemplate)
        - [项模板](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 基架](#scaffold)
    - [Razor 编辑器](#razor)
    - [NuGet 2.7](#nuget)
- 已知问题和重大更改

    - [ASP.NET 基架](#issuescaffolding)

        - [MVC 和 Web API 基架-HTTP 404，未找到错误](#404issue)
        - [添加基架项后，Web 的 Visual Studio Express 2012 停止工作](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [使用 "浏览" 或按 F5 查看 cshtml 文件会导致服务器错误](#browseissue)
        - [Url 重写和颚化符（~）](#rewriteissue)
    - [模板](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>安装说明

[安装](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1。

<a id="requirements"></a>
## <a name="software-requirements"></a>软件要求

你必须具有 Visual Studio 2012 或适用于 Web 的 Visual Studio Express 2012。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 ASP.NET 和 Web 工具2013.1 中的新增功能

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Bootstrap

当基架 MVC 5 控制器和视图时，视图的标记将使用 "[启动](http://getbootstrap.com/)"。

<a id="templates"></a>
### <a name="templates"></a>模板

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 模板

我们添加了一个新的 MVC 5 模板。 它引用最新的 MVC 5 NuGet 包，你可以使用基架来添加控制器和视图。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 模板

我们添加了一个新的 Web API 2 模板。 它引用最新的 Web API 2 NuGet 包，你可以使用基架来添加控制器和视图。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>项模板

我们为 MVC 5 视图、网页（Razor 3）和 Web API 2 控制器添加了新的项模板。 在添加新项时，它们会将相关 NuGet 包安装到项目中。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

使用实体框架基架 MVC 或 Web API 控制器时，将使用 Framework 6。 有关实体框架的详细信息，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。

你还可以下载和安装适用于 Visual Studio 2012 的实体框架6工具。 请参阅[Get 实体框架](https://msdn.com/data/ee712906#tooling)。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 基架

ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。 这样，便可以轻松地将样板代码添加到项目中，以与数据模型交互。

在以前版本的 Visual Studio 中，基架限制为 ASP.NET MVC 项目。 使用此更新，现在可以将基架用于任何 ASP.NET 项目（包括 Web 窗体）。 此更新不支持为 Web 窗体项目生成页，但你仍然可以通过将 MVC 依赖项添加到项目中，将基架与 Web 窗体一起使用。 将来的更新中将添加对 Web 窗体的生成页的支持。

使用基架时，请确保在项目中安装所有必需的依赖项。 例如，如果从 ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用会自动添加到你的项目中。

若要将 MVC 基架添加到 Web 窗体项目，请在对话框窗口中添加**新的基架项**，并选择 " **MVC 5 依赖**项"。 基架 MVC 有两个选项：最小和完整。 如果选择 "最小"，则只会将 NuGet 包和 ASP.NET MVC 的引用添加到你的项目中。 如果选择 "完全" 选项，则会添加最小依赖项，以及 MVC 项目所需的内容文件。

对基架的支持：异步控制器使用实体框架6中的新异步功能。

有关详细信息和教程，请参阅[ASP.NET 基架概述](../2013/aspnet-scaffolding-overview.md)。 这些教程显示了 Visual Studio 2013 的基架，但也适用于 Visual Studio 2012 ASP.NET 和 Web 工具2013.1。

<a id="razor"></a>
### <a name="razor-editor"></a>Razor 编辑器

通过此更新，Visual Studio 2012 现在支持 Razor 3 工具/编辑。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包括一组丰富的新功能，这些功能在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中有详细说明。

此版本的 NuGet 不再需要用户显式允许 NuGet 还原缺少的包。 安装 NuGet 2.7 时，用户隐式同意自动还原缺少的包。 用户可以通过 Visual Studio 中的 NuGet 设置显式退出包还原。 此更改简化了包还原的工作方式。

## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 基架

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 基架-HTTP 404，未找到错误

如果将基架项添加到项目时遇到错误，你的项目可能会处于不一致的状态。 所做的某些更改将被回滚，但其他更改（如安装的 NuGet 包）将不会回滚。 如果回滚路由配置更改，则在导航到基架项时，用户将收到 HTTP 404 错误。

若要为 MVC 修复此错误，请添加一个新的基架项，并选择 "MVC 5 依赖项（最小或全部）"。 此过程将向你的项目添加所需的所有更改。

为 Web API 修复此错误：

1. 将以下 Webapiconfig.cs 类添加到项目。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 按如下所示在 Webapiconfig.cs 中的应用程序\_Start 方法中配置：

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>添加基架项后，Web 的 Visual Studio Express 2012 停止工作

如果在添加具有实体框架的基架项后 Visual Studio Express 2012 for Web 停止工作（例如使用实体框架的包含操作的 Web API 2 控制器），则 Visual Studio Express 未能加载程序集的本机映像依赖于 System.web。

若要更正此问题，请将 Visual Studio Express 配置为使用 System.web 的 MSIL 映像：

1. 在管理员模式下打开命令提示符。
2. 中转到%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE 或% ProgramFiles （x86）% \ Microsoft Visual Studio 11.0 \ Common7\IDE （适用于64位 Windows）。
3. 在文本编辑器中打开 VWDExpress。
4. 将以下行添加到 &lt;配置&gt;/&lt;运行时&gt; 元素：  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 重新启动 Web 的 Visual Studio Express 2012。

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>使用 "浏览" 或按 F5 查看 cshtml 文件会导致服务器错误

当你在 Visual Studio 2012 中创建 MVC 5 项目（或在 Visual Studio 2012 中打开，在 Visual Studio 2013 中创建的 MVC 5 项目），并尝试通过使用 "通过浏览" 或按 F5 来查看 cshtml 文件时，你将收到一个错误，指出 **"/" 应用程序中出现服务器错误**。 服务器尝试导航到 `http://localhost:XXXX/Views/../XXXX.cshtml`

若要解决此问题，请将项目中的 "**启动操作**" 设置更改为 "**特定页面**"。 不需要为页面提供值。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

做出此更改后，选择 "F5" 可导航到应用程序的根目录（`http://localhost:XXXX`）。 此行为与 Visual Studio 2013 中的 MVC 5 项目的行为不同，其中，**当前页面**设置将启动打开的页面。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 重写和颚化符（~）

升级到 ASP.NET Razor 3 或 ASP.NET MVC 5 之后，如果使用 URL 重写，则波形符（~）表示法可能无法正常工作。 URL 重写会影响 HTML 元素中的波形符（~）表示法（例如 &lt;A/&gt;、&lt;SCRIPT/&gt;、&lt;LINK/&gt;），因此波形符不再映射到根目录。

例如，如果将**asp.net/content**的请求重写为**asp.net**，则 &lt;href = "~/content/"/&gt; 中的 href 属性将解析为 **/content/content/** ，而不是 **/** 。 若要取消此更改，你可以在每个网页或 BeginRequest 中的**应用程序\_** 中将**IIS\_WasUrlRewritten**上下文设置为 false。

<a id="templateissue"></a>
### <a name="templates"></a>模板

当使用 Windows 8.1 或 Windows Server 2012 R2 上的 Visual Studio 2012 创建 ASP.NET MVC 项目时，Visual Studio 将显示一条错误消息，指出 "为 ASP.NET 4.5 配置 Web [url] 失败"。

![配置错误](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

你会看到此错误，因为当 Visual Studio 2012 安装在这些版本的 Windows 上时，Visual Studio 不会启用 ASP.NET 4.5 功能。 若要启用 ASP.NET 4.5，请执行 "[打开或关闭 Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)" 中所述的步骤。

![打开或关闭 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

或者，你可以通过命令行启用 ASP.NET 4.5。

1. 在管理员模式下打开命令提示符。
2. 运行以下命令以启用 ASP.NET 4.5。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
