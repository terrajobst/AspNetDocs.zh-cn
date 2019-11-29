---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 发行说明 ASP.NET 和 Web 工具Microsoft Docs
author: microsoft
description: 本文档介绍 Visual Studio 2013 ASP.NET 和 Web 工具的版本。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600440"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="da2dc-103">适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具发行说明</span><span class="sxs-lookup"><span data-stu-id="da2dc-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="da2dc-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="da2dc-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="da2dc-105">本文档介绍 Visual Studio 2013 ASP.NET 和 Web 工具的版本。</span><span class="sxs-lookup"><span data-stu-id="da2dc-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="da2dc-106">内容</span><span class="sxs-lookup"><span data-stu-id="da2dc-106">Contents</span></span>

- [<span data-ttu-id="da2dc-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="da2dc-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="da2dc-108">文档</span><span class="sxs-lookup"><span data-stu-id="da2dc-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="da2dc-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="da2dc-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="da2dc-110">ASP.NET 和 Web 工具中 Visual Studio 2013 的新功能</span><span class="sxs-lookup"><span data-stu-id="da2dc-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="da2dc-111">一 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="da2dc-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="da2dc-112">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="da2dc-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="da2dc-113">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="da2dc-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="da2dc-114">浏览器链接</span><span class="sxs-lookup"><span data-stu-id="da2dc-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="da2dc-115">Visual Studio Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="da2dc-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="da2dc-116">Visual Studio 中的 Azure App Service Web 应用支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="da2dc-117">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="da2dc-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="da2dc-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="da2dc-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="da2dc-119">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="da2dc-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="da2dc-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="da2dc-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="da2dc-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="da2dc-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="da2dc-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="da2dc-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="da2dc-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="da2dc-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="da2dc-124">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="da2dc-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="da2dc-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="da2dc-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="da2dc-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="da2dc-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="da2dc-127">ASP.NET 应用挂起</span><span class="sxs-lookup"><span data-stu-id="da2dc-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="da2dc-128">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="da2dc-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="da2dc-129">安装说明</span><span class="sxs-lookup"><span data-stu-id="da2dc-129">Installation Notes</span></span>

<span data-ttu-id="da2dc-130">Visual Studio 2013 的 ASP.NET 和 Web 工具捆绑在主安装程序中，可在[此处](https://www.asp.net/downloads)下载。</span><span class="sxs-lookup"><span data-stu-id="da2dc-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="da2dc-131">Documentation</span><span class="sxs-lookup"><span data-stu-id="da2dc-131">Documentation</span></span>

<span data-ttu-id="da2dc-132">[ASP.NET 网站](https://www.asp.net/)提供了有关 Visual Studio 2013 ASP.NET 和 Web 工具的教程和其他信息。</span><span class="sxs-lookup"><span data-stu-id="da2dc-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="da2dc-133">软件要求</span><span class="sxs-lookup"><span data-stu-id="da2dc-133">Software Requirements</span></span>

<span data-ttu-id="da2dc-134">ASP.NET 和 Web 工具要求 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="da2dc-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="da2dc-135">ASP.NET 和 Web 工具中 Visual Studio 2013 的新功能</span><span class="sxs-lookup"><span data-stu-id="da2dc-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="da2dc-136">以下各节介绍了在版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="da2dc-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="da2dc-137">一 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="da2dc-137">One ASP.NET</span></span>

<span data-ttu-id="da2dc-138">随着 Visual Studio 2013 的发布，我们已开始使用 ASP.NET 技术来统一体验，以便你可以轻松地混合并匹配所需的技术。</span><span class="sxs-lookup"><span data-stu-id="da2dc-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="da2dc-139">例如，你可以使用 MVC 启动项目，并在以后轻松地将 Web 窗体页添加到项目，或在 Web 窗体项目中基架 Web Api。</span><span class="sxs-lookup"><span data-stu-id="da2dc-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="da2dc-140">其中一 ASP.NET 是使你作为开发人员更轻松地完成 ASP.NET 中所喜欢的操作。</span><span class="sxs-lookup"><span data-stu-id="da2dc-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="da2dc-141">无论你选择哪种技术，都可以放心地在一个 ASP.NET 的受信任基础框架上构建。</span><span class="sxs-lookup"><span data-stu-id="da2dc-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="da2dc-142">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="da2dc-142">New Web Project Experience</span></span>

<span data-ttu-id="da2dc-143">在 Visual Studio 2013 中，我们已增强了创建新的 web 项目的体验。</span><span class="sxs-lookup"><span data-stu-id="da2dc-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="da2dc-144">在 "**新建 ASP.NET Web 项目**" 对话框中，您可以选择所需的项目类型，配置任何技术组合（Web 窗体、MVC 和 Web API），配置身份验证选项，以及添加单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="da2dc-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新 ASP.NET 项目](release-notes/_static/image1.png)

<span data-ttu-id="da2dc-146">通过 "新建" 对话框，您可以更改许多模板的默认身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="da2dc-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="da2dc-147">例如，在创建 ASP.NET Web 窗体项目时，可以选择以下任一选项：</span><span class="sxs-lookup"><span data-stu-id="da2dc-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="da2dc-148">无身份验证</span><span class="sxs-lookup"><span data-stu-id="da2dc-148">No Authentication</span></span>
- <span data-ttu-id="da2dc-149">单个用户帐户（ASP.NET 成员身份或社交提供程序登录）</span><span class="sxs-lookup"><span data-stu-id="da2dc-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="da2dc-150">组织帐户（在 internet 应用程序中 Active Directory）</span><span class="sxs-lookup"><span data-stu-id="da2dc-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="da2dc-151">Windows 身份验证（在 intranet 应用程序中 Active Directory）</span><span class="sxs-lookup"><span data-stu-id="da2dc-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![身份验证选项](release-notes/_static/image2.png)

<span data-ttu-id="da2dc-153">有关用于创建 web 项目的新进程的详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="da2dc-154">有关新的身份验证选项的详细信息，请参阅本文档后面的[ASP.NET Identity](#TOC8) 。</span><span class="sxs-lookup"><span data-stu-id="da2dc-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="da2dc-155">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="da2dc-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="da2dc-156">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="da2dc-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="da2dc-157">这样，便可以轻松地将样板代码添加到项目中，以与数据模型交互。</span><span class="sxs-lookup"><span data-stu-id="da2dc-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="da2dc-158">在以前版本的 Visual Studio 中，基架限制为 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="da2dc-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="da2dc-159">使用 Visual Studio 2013，现在可以将基架用于任何 ASP.NET 项目，包括 Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="da2dc-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="da2dc-160">Visual Studio 2013 当前不支持为 Web 窗体项目生成页，但你仍可以通过将 MVC 依赖项添加到项目中，将基架与 Web 窗体一起使用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="da2dc-161">将来的更新中将添加对 Web 窗体的生成页的支持。</span><span class="sxs-lookup"><span data-stu-id="da2dc-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="da2dc-162">使用基架时，请确保在项目中安装所有必需的依赖项。</span><span class="sxs-lookup"><span data-stu-id="da2dc-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="da2dc-163">例如，如果从 ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用会自动添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="da2dc-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="da2dc-164">若要将 MVC 基架添加到 Web 窗体项目，请在对话框窗口中添加**新的基架项**，并选择 " **MVC 5 依赖**项"。</span><span class="sxs-lookup"><span data-stu-id="da2dc-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="da2dc-165">基架 MVC 有两个选项：最小和完整。</span><span class="sxs-lookup"><span data-stu-id="da2dc-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="da2dc-166">如果选择 "最小"，则只会将 NuGet 包和 ASP.NET MVC 的引用添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="da2dc-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="da2dc-167">如果选择 "完全" 选项，则会添加最小依赖项，以及 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="da2dc-168">对基架的支持：异步控制器使用实体框架6中的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="da2dc-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="da2dc-169">有关详细信息和教程，请参阅[ASP.NET 基架概述](aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="da2dc-170">Browser Link –浏览器和 Visual Studio 之间的 SignalR 通道</span><span class="sxs-lookup"><span data-stu-id="da2dc-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="da2dc-171">使用新的[浏览器链接](using-browser-link.md)功能，可以将多个浏览器连接到 Visual Studio，并通过单击工具栏中的按钮来刷新所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="da2dc-172">您可以将多个浏览器连接到您的开发站点（包括移动仿真程序），然后单击 "刷新" 以刷新所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="da2dc-173">Browser 链接还公开了一个 API，使开发人员能够编写浏览器链接扩展。</span><span class="sxs-lookup"><span data-stu-id="da2dc-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="da2dc-174">通过使开发人员能够利用浏览器链接 API，可以创建非常高级的方案，这些方案跨越 Visual Studio 和连接的任何浏览器之间的边界。</span><span class="sxs-lookup"><span data-stu-id="da2dc-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="da2dc-175">Web Essentials 利用 API 在 Visual Studio 与浏览器的开发人员工具之间创建集成体验，从而远程控制移动模拟器和更多。</span><span class="sxs-lookup"><span data-stu-id="da2dc-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="da2dc-176">Visual Studio Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="da2dc-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="da2dc-177">Visual Studio 2013 在 web 应用程序中包含用于 Razor 文件和 HTML 文件的新 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="da2dc-178">新的 HTML 编辑器提供了基于 HTML5 的单个统一架构。</span><span class="sxs-lookup"><span data-stu-id="da2dc-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="da2dc-179">它具有自动大括号完成，jQuery UI 和 AngularJS 特性 IntelliSense，特性 IntelliSense 分组，ID 和类名称 Intellisense，还包括更好的性能、格式设置和智能标记。</span><span class="sxs-lookup"><span data-stu-id="da2dc-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="da2dc-180">以下屏幕截图演示了如何在 HTML 编辑器中使用启动属性 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="da2dc-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 编辑器中的 Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="da2dc-182">Visual Studio 2013 还附带了内置的 CoffeeScript 和 LESS 编辑器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="da2dc-183">更少的编辑器附带了 CSS 编辑器中的所有酷功能，并在 @import 链中的所有更少文档之间提供了特定的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="da2dc-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="da2dc-184">Visual Studio 中的 Azure App Service Web 应用支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="da2dc-185">在使用用于 .NET 2.2 的 Azure SDK Visual Studio 2013 中，你可以使用**服务器资源管理器**与远程 web 应用直接交互。</span><span class="sxs-lookup"><span data-stu-id="da2dc-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="da2dc-186">你可以登录到 Azure 帐户、创建新的 web 应用、配置应用、查看实时日志等等。</span><span class="sxs-lookup"><span data-stu-id="da2dc-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="da2dc-187">SDK 2.2 发布后即将推出，你将能够在 Azure 中远程运行调试模式。</span><span class="sxs-lookup"><span data-stu-id="da2dc-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="da2dc-188">当你安装当前版本的 Azure SDK for .NET 时，Azure App Service Web 应用的大多数新功能也适用于 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="da2dc-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="da2dc-189">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="da2dc-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="da2dc-190">在 Azure App Service 中创建 ASP.NET web 应用</span><span class="sxs-lookup"><span data-stu-id="da2dc-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="da2dc-191">使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="da2dc-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="da2dc-192">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="da2dc-192">Web Publish Enhancements</span></span>

<span data-ttu-id="da2dc-193">Visual Studio 2013 包括新的和增强的 Web 发布功能。</span><span class="sxs-lookup"><span data-stu-id="da2dc-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="da2dc-194">下面是其中几个：</span><span class="sxs-lookup"><span data-stu-id="da2dc-194">Here are a few of them:</span></span>

- <span data-ttu-id="da2dc-195">轻松[实现 web.config 文件加密的自动化](https://go.microsoft.com/fwlink/?LinkId=325529)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="da2dc-196">（此链接和以下两个指向 MSDN 上的文档，这些文档在10/17 年的最晚日期之前可能不可用。）</span><span class="sxs-lookup"><span data-stu-id="da2dc-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="da2dc-197">[在部署过程中轻松地自动使应用程序脱机](https://go.microsoft.com/fwlink/?LinkId=325530)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="da2dc-198">将 Web 部署配置为[使用文件校验和，而不是上次更改日期](https://go.microsoft.com/fwlink/?LinkId=325531)，以确定应将哪些文件复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="da2dc-199">使用 FTP 或文件系统发布方法以及 Web 部署时，快速发布单个选定的文件（包括 web.config）。</span><span class="sxs-lookup"><span data-stu-id="da2dc-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="da2dc-200">有关 ASP.NET web 部署的详细信息，请参阅[ASP.NET 站点](https://go.microsoft.com/fwlink/?LinkId=322027)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="da2dc-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="da2dc-201">NuGet 2.7</span></span>

<span data-ttu-id="da2dc-202">NuGet 2.7 包括一组丰富的新功能，这些功能在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中有详细说明。</span><span class="sxs-lookup"><span data-stu-id="da2dc-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="da2dc-203">此版本的 NuGet 还无需向 NuGet 的包还原功能提供下载包的明确同意。</span><span class="sxs-lookup"><span data-stu-id="da2dc-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="da2dc-204">现在，通过安装 NuGet 授予同意（以及 NuGet 的 "首选项" 对话框中的关联复选框）。</span><span class="sxs-lookup"><span data-stu-id="da2dc-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="da2dc-205">现在，包还原功能在默认情况下是有效的。</span><span class="sxs-lookup"><span data-stu-id="da2dc-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="da2dc-206">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="da2dc-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="da2dc-207">一 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="da2dc-207">One ASP.NET</span></span>

<span data-ttu-id="da2dc-208">Web 窗体项目模板与新的 ASP.NET 体验无缝集成。</span><span class="sxs-lookup"><span data-stu-id="da2dc-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="da2dc-209">您可以向 Web 窗体项目添加 MVC 和 Web API 支持，并且可以使用一个 ASP.NET 项目创建向导配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="da2dc-210">有关详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="da2dc-211">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="da2dc-211">ASP.NET Identity</span></span>

<span data-ttu-id="da2dc-212">Web 窗体项目模板支持新的 ASP.NET Identity 框架。</span><span class="sxs-lookup"><span data-stu-id="da2dc-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="da2dc-213">此外，这些模板现在支持创建 Web 窗体 intranet 项目。</span><span class="sxs-lookup"><span data-stu-id="da2dc-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="da2dc-214">有关详细信息，请参阅**在 Visual Studio 2013 中创建 ASP.NET Web 项目**中的[身份验证方法](creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="da2dc-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="da2dc-215">Bootstrap</span></span>

<span data-ttu-id="da2dc-216">Web 窗体模板使用[启动](http://twitter.github.io/bootstrap/)，提供精美且响应迅速的外观，您可以轻松地对其进行自定义。</span><span class="sxs-lookup"><span data-stu-id="da2dc-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="da2dc-217">有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 "启动"](creating-web-projects-in-visual-studio.md#bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="da2dc-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="da2dc-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="da2dc-219">一 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="da2dc-219">One ASP.NET</span></span>

<span data-ttu-id="da2dc-220">Web MVC 项目模板与新的 ASP.NET 体验无缝集成。</span><span class="sxs-lookup"><span data-stu-id="da2dc-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="da2dc-221">你可以自定义 MVC 项目，并使用 ASP.NET 项目创建向导配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="da2dc-222">ASP.NET MVC 5 的介绍性教程可在[与 ASP.NET mvc 5 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)上找到。</span><span class="sxs-lookup"><span data-stu-id="da2dc-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="da2dc-223">有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将 ASP.NET mvc 4 和 WEB Api 项目升级到 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="da2dc-224">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="da2dc-224">ASP.NET Identity</span></span>

<span data-ttu-id="da2dc-225">MVC 项目模板已更新为使用 ASP.NET Identity 进行身份验证和标识管理。</span><span class="sxs-lookup"><span data-stu-id="da2dc-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="da2dc-226">有关 Facebook 和 Google 身份验证以及新的成员资格 API 的教程，请参阅[使用 facebook 和 Google OAuth2 创建 ASP.NET mvc 5 应用和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)和[创建具有 AUTH 和 SQL 数据库的 ASP.NET MVC 应用并将其部署到 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="da2dc-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="da2dc-227">Bootstrap</span></span>

<span data-ttu-id="da2dc-228">MVC 项目模板已更新为使用[引导](http://getbootstrap.com/)，提供精美且响应迅速的外观，你可以轻松地对其进行自定义。</span><span class="sxs-lookup"><span data-stu-id="da2dc-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="da2dc-229">有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 "启动"](creating-web-projects-in-visual-studio.md#bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="da2dc-230">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="da2dc-230">Authentication filters</span></span>

<span data-ttu-id="da2dc-231">身份验证筛选器是 ASP.NET MVC 中的一种新筛选器，它在 ASP.NET MVC 管道中的授权筛选器之前运行，并允许你为所有控制器指定每个操作的身份验证逻辑、每个控制器或全局。</span><span class="sxs-lookup"><span data-stu-id="da2dc-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="da2dc-232">身份验证筛选器处理请求中的凭据，并提供相应的主体。</span><span class="sxs-lookup"><span data-stu-id="da2dc-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="da2dc-233">身份验证筛选器还可以添加身份验证质询来响应未经授权的请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="da2dc-234">筛选器替代</span><span class="sxs-lookup"><span data-stu-id="da2dc-234">Filter overrides</span></span>

<span data-ttu-id="da2dc-235">你现在可以通过指定替代筛选器来覆盖应用于给定操作方法或控制器的筛选器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="da2dc-236">替代筛选器指定一组不应针对给定作用域（操作或控制器）运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="da2dc-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="da2dc-237">这样，便可以配置全局应用的筛选器，但不会将某些全局筛选器应用于特定操作或控制器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="da2dc-238">属性路由</span><span class="sxs-lookup"><span data-stu-id="da2dc-238">Attribute routing</span></span>

<span data-ttu-id="da2dc-239">ASP.NET MVC 现在支持属性路由，因为 Tim McCall （ [http://attributerouting.net](http://attributerouting.net)作者）的贡献。</span><span class="sxs-lookup"><span data-stu-id="da2dc-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="da2dc-240">使用属性路由，可以通过注释操作和控制器来指定路由。</span><span class="sxs-lookup"><span data-stu-id="da2dc-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="da2dc-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="da2dc-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="da2dc-242">属性路由</span><span class="sxs-lookup"><span data-stu-id="da2dc-242">Attribute routing</span></span>

<span data-ttu-id="da2dc-243">由于 Tim McCall （ [http://attributerouting.net](http://attributerouting.net)的作者）的贡献，ASP.NET Web API 现在支持属性路由。</span><span class="sxs-lookup"><span data-stu-id="da2dc-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="da2dc-244">使用属性路由，你可以通过批注你的操作和控制器来指定你的 Web API 路由，如下所示：</span><span class="sxs-lookup"><span data-stu-id="da2dc-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="da2dc-245">特性路由使你可以更好地控制 web API 中的 Uri。</span><span class="sxs-lookup"><span data-stu-id="da2dc-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="da2dc-246">例如，你可以使用单个 API 控制器轻松定义资源层次结构：</span><span class="sxs-lookup"><span data-stu-id="da2dc-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="da2dc-247">属性路由还提供了一种方便的语法来指定可选参数、默认值和路由约束：</span><span class="sxs-lookup"><span data-stu-id="da2dc-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="da2dc-248">有关属性路由的详细信息，请参阅[WEB API 2 中的属性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="da2dc-249">OAuth 2。0</span><span class="sxs-lookup"><span data-stu-id="da2dc-249">OAuth 2.0</span></span>

<span data-ttu-id="da2dc-250">Web API 和单页应用程序项目模板现在支持使用 OAuth 2.0 的授权。</span><span class="sxs-lookup"><span data-stu-id="da2dc-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="da2dc-251">OAuth 2.0 是一个框架，用于授权客户端对受保护资源的访问。</span><span class="sxs-lookup"><span data-stu-id="da2dc-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="da2dc-252">它适用于各种客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="da2dc-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="da2dc-253">支持 OAuth 2.0 基于 Microsoft OWIN 组件提供的用于持有者身份验证的新安全中间件和实现授权服务器角色。</span><span class="sxs-lookup"><span data-stu-id="da2dc-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="da2dc-254">或者，可以使用组织授权服务器（如 Azure Active Directory 或 Windows Server 2012 R2 中的 ADFS）来授权客户端。</span><span class="sxs-lookup"><span data-stu-id="da2dc-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="da2dc-255">OData 改进</span><span class="sxs-lookup"><span data-stu-id="da2dc-255">OData Improvements</span></span>

<span data-ttu-id="da2dc-256">**支持 $select、$expand、$batch 和 $value**</span><span class="sxs-lookup"><span data-stu-id="da2dc-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="da2dc-257">ASP.NET Web API OData 现在完全支持 $select、$expand 和 $value。</span><span class="sxs-lookup"><span data-stu-id="da2dc-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="da2dc-258">你还可以使用 $batch 来请求批处理和处理变更集。</span><span class="sxs-lookup"><span data-stu-id="da2dc-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="da2dc-259">使用 "$select" 和 "$expand" 选项，您可以更改从 OData 终结点返回的数据的形状。</span><span class="sxs-lookup"><span data-stu-id="da2dc-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="da2dc-260">有关详细信息，请参阅[WEB API OData 中的 $select 和 $expand 支持简介](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="da2dc-261">**改进的扩展性**</span><span class="sxs-lookup"><span data-stu-id="da2dc-261">**Improved extensibility**</span></span>

<span data-ttu-id="da2dc-262">OData 格式化程序现在可扩展。</span><span class="sxs-lookup"><span data-stu-id="da2dc-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="da2dc-263">可以添加 Atom 项元数据、支持命名流和媒体链接项、添加实例批注以及自定义链接的生成方式。</span><span class="sxs-lookup"><span data-stu-id="da2dc-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="da2dc-264">**不支持类型的支持**</span><span class="sxs-lookup"><span data-stu-id="da2dc-264">**Type-less support**</span></span>

<span data-ttu-id="da2dc-265">你现在可以构建 OData 服务，无需为你的实体类型定义 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="da2dc-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="da2dc-266">相反，OData 控制器可以获取或返回**IEdmObject**的实例，这些实例是 OData 格式化程序序列化/反序列化的。</span><span class="sxs-lookup"><span data-stu-id="da2dc-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="da2dc-267">**重用现有模型**</span><span class="sxs-lookup"><span data-stu-id="da2dc-267">**Reuse an existing model**</span></span>

<span data-ttu-id="da2dc-268">如果已有实体数据模型（EDM），则现在可以直接重复使用它，而无需生成新的实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="da2dc-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="da2dc-269">例如，如果使用实体框架，则可以使用 EF 为你生成的 EDM。</span><span class="sxs-lookup"><span data-stu-id="da2dc-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="da2dc-270">请求批处理</span><span class="sxs-lookup"><span data-stu-id="da2dc-270">Request Batching</span></span>

<span data-ttu-id="da2dc-271">请求批处理将多个操作合并为一个 HTTP POST 请求，以减少网络流量，并提供更流畅、更流畅的用户界面。</span><span class="sxs-lookup"><span data-stu-id="da2dc-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="da2dc-272">ASP.NET Web API 现在支持多个请求批处理策略：</span><span class="sxs-lookup"><span data-stu-id="da2dc-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="da2dc-273">使用 OData 服务的 $batch 终结点。</span><span class="sxs-lookup"><span data-stu-id="da2dc-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="da2dc-274">将多个请求打包为一个 MIME 多部分请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="da2dc-275">使用自定义批处理格式。</span><span class="sxs-lookup"><span data-stu-id="da2dc-275">Use a custom batching format.</span></span>

<span data-ttu-id="da2dc-276">若要启用请求批处理，只需将具有批处理处理程序的路由添加到 Web API 配置：</span><span class="sxs-lookup"><span data-stu-id="da2dc-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="da2dc-277">你还可以控制是按顺序还是按任意顺序执行请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="da2dc-278">可移植的 ASP.NET Web API 客户端</span><span class="sxs-lookup"><span data-stu-id="da2dc-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="da2dc-279">你现在可以使用 ASP.NET Web API 客户端创建可在 Windows 应用商店中工作和 Windows Phone 8 个应用程序的可移植类库。</span><span class="sxs-lookup"><span data-stu-id="da2dc-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="da2dc-280">你还可以创建可在客户端和服务器之间共享的可移植格式化程序。</span><span class="sxs-lookup"><span data-stu-id="da2dc-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="da2dc-281">改进的可测试性</span><span class="sxs-lookup"><span data-stu-id="da2dc-281">Improved Testability</span></span>

<span data-ttu-id="da2dc-282">Web API 2 使对 API 控制器进行单元测试变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="da2dc-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="da2dc-283">只需用请求消息和配置来实例化 API 控制器，然后调用要测试的操作方法。</span><span class="sxs-lookup"><span data-stu-id="da2dc-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="da2dc-284">还可以轻松地模拟执行链接生成的操作方法的**UrlHelper**类。</span><span class="sxs-lookup"><span data-stu-id="da2dc-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="da2dc-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="da2dc-285">IHttpActionResult</span></span>

<span data-ttu-id="da2dc-286">你现在可以实现 IHttpActionResult 来封装 Web API 操作方法的结果。</span><span class="sxs-lookup"><span data-stu-id="da2dc-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="da2dc-287">从 Web API 操作方法返回的 IHttpActionResult 由 ASP.NET Web API 运行时执行，以生成生成的响应消息。</span><span class="sxs-lookup"><span data-stu-id="da2dc-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="da2dc-288">可以从任何 Web API 操作返回 IHttpActionResult，以简化 Web API 实现单元测试。</span><span class="sxs-lookup"><span data-stu-id="da2dc-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="da2dc-289">为方便起见，提供了许多 IHttpActionResult 实现，包括返回特定状态代码、格式化内容或内容协商响应的结果。</span><span class="sxs-lookup"><span data-stu-id="da2dc-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="da2dc-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="da2dc-290">HttpRequestContext</span></span>

<span data-ttu-id="da2dc-291">新的**HttpRequestContext**跟踪与请求关联的任何状态，但不会立即从请求中获取。</span><span class="sxs-lookup"><span data-stu-id="da2dc-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="da2dc-292">例如，你可以使用**HttpRequestContext**来获取路由数据、与请求关联的主体、客户端证书、 **UrlHelper**和虚拟路径根。</span><span class="sxs-lookup"><span data-stu-id="da2dc-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="da2dc-293">您可以轻松地创建**HttpRequestContext** ，用于单元测试目的。</span><span class="sxs-lookup"><span data-stu-id="da2dc-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="da2dc-294">由于请求的主体与请求流动，而不是依赖于**thread.currentprincipal**，因此在请求的整个生存期内，主体现在可在 Web API 管道中使用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="da2dc-295">CORS</span><span class="sxs-lookup"><span data-stu-id="da2dc-295">CORS</span></span>

<span data-ttu-id="da2dc-296">由于 Brock Allen 的另一大贡献，ASP.NET 现在完全支持跨域请求共享（CORS）。</span><span class="sxs-lookup"><span data-stu-id="da2dc-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="da2dc-297">Browser security 阻止网页向另一个域发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="da2dc-298">[CORS](http://www.w3.org/TR/cors/)是一种 W3C 标准，可让服务器放宽相同的源策略。</span><span class="sxs-lookup"><span data-stu-id="da2dc-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="da2dc-299">使用 CORS，服务器可以在拒绝其他跨域请求时显式允许一些跨域请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="da2dc-300">Web API 2 现在支持 CORS，包括自动处理预检请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="da2dc-301">有关详细信息，请参阅[在 ASP.NET Web API 中启用跨域请求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="da2dc-302">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="da2dc-302">Authentication Filters</span></span>

<span data-ttu-id="da2dc-303">身份验证筛选器是 ASP.NET Web API 中的一种新筛选器，它在 ASP.NET Web API 管道中的授权筛选器之前运行，并允许你为所有控制器指定每个操作的身份验证逻辑、每个控制器或全局。</span><span class="sxs-lookup"><span data-stu-id="da2dc-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="da2dc-304">身份验证筛选器处理请求中的凭据，并提供相应的主体。</span><span class="sxs-lookup"><span data-stu-id="da2dc-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="da2dc-305">身份验证筛选器还可以添加身份验证质询来响应未经授权的请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="da2dc-306">筛选器替代</span><span class="sxs-lookup"><span data-stu-id="da2dc-306">Filter Overrides</span></span>

<span data-ttu-id="da2dc-307">你现在可以通过指定替代筛选器来覆盖应用于给定操作方法或控制器的筛选器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="da2dc-308">替代筛选器指定一组不应针对给定作用域（操作或控制器）运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="da2dc-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="da2dc-309">这样，便可以添加全局筛选器，但不会从特定操作或控制器中排除某些筛选器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="da2dc-310">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="da2dc-310">OWIN Integration</span></span>

<span data-ttu-id="da2dc-311">ASP.NET Web API 现在完全支持 OWIN，并且可以在任何支持 OWIN 的主机上运行。</span><span class="sxs-lookup"><span data-stu-id="da2dc-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="da2dc-312">还包括一个**HostAuthenticationFilter** ，它提供与 OWIN authentication 系统的集成。</span><span class="sxs-lookup"><span data-stu-id="da2dc-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="da2dc-313">借助 OWIN 集成，你可以在自己的进程中自承载 Web API 以及其他 OWIN 中间件，如 SignalR。</span><span class="sxs-lookup"><span data-stu-id="da2dc-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="da2dc-314">有关详细信息，请参阅[将 OWIN 用于自承载 ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="da2dc-315">ASP.NET SignalR 2。0</span><span class="sxs-lookup"><span data-stu-id="da2dc-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="da2dc-316">以下各节介绍 SignalR 2.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="da2dc-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="da2dc-317">构建于 OWIN</span><span class="sxs-lookup"><span data-stu-id="da2dc-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="da2dc-318">Routeconfig 和 MapConnection 现在是 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="da2dc-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="da2dc-319">跨域支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="da2dc-320">通过 Monotouch.dialog 和 MonoDroid 支持 iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="da2dc-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="da2dc-321">可移植 .NET 客户端</span><span class="sxs-lookup"><span data-stu-id="da2dc-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="da2dc-322">新的自主机包</span><span class="sxs-lookup"><span data-stu-id="da2dc-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="da2dc-323">向后兼容的服务器支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="da2dc-324">删除了对 .NET 4.0 的服务器支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="da2dc-325">将消息发送到客户端和组的列表</span><span class="sxs-lookup"><span data-stu-id="da2dc-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="da2dc-326">向特定用户发送消息</span><span class="sxs-lookup"><span data-stu-id="da2dc-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="da2dc-327">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="da2dc-328">简化集线器的单元测试</span><span class="sxs-lookup"><span data-stu-id="da2dc-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="da2dc-329">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="da2dc-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="da2dc-330">有关如何将现有的1.x 项目升级到 SignalR 2.0 的示例，请参阅[升级 SignalR 1.X 项目](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="da2dc-331">构建于 OWIN</span><span class="sxs-lookup"><span data-stu-id="da2dc-331">Built on OWIN</span></span>

<span data-ttu-id="da2dc-332">SignalR 2.0 完全建立在[OWIN （.net 的开放 Web 接口）](http://owin.org/)上。</span><span class="sxs-lookup"><span data-stu-id="da2dc-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="da2dc-333">此更改使 SignalR 的设置过程在 web 托管的 SignalR 应用程序与自托管的应用程序之间更加一致，但也需要进行大量的 API 更改。</span><span class="sxs-lookup"><span data-stu-id="da2dc-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="da2dc-334">Routeconfig 和 MapConnection 现在是 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="da2dc-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="da2dc-335">为了兼容 OWIN 标准，这些方法已重命名为 `MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="da2dc-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="da2dc-336">不带参数调用的 `MapSignalR` 将映射所有中心（如版本1.x 中的 `MapHubs`）;若要映射各个**PersistentConnection**对象，请将连接类型指定为类型参数，并将连接的 URL 扩展指定为第一个参数。</span><span class="sxs-lookup"><span data-stu-id="da2dc-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="da2dc-337">在 Owin startup 类中调用 `MapSignalR` 方法。</span><span class="sxs-lookup"><span data-stu-id="da2dc-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="da2dc-338">Visual Studio 2013 包含 Owin startup 类的新模板;若要使用此模板，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="da2dc-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="da2dc-339">右键单击项目</span><span class="sxs-lookup"><span data-stu-id="da2dc-339">Right-click on the project</span></span>
2. <span data-ttu-id="da2dc-340">选择 "**添加**"、"**新建项 ...** "</span><span class="sxs-lookup"><span data-stu-id="da2dc-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="da2dc-341">选择**Owin Startup 类**。</span><span class="sxs-lookup"><span data-stu-id="da2dc-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="da2dc-342">将新类命名为**Startup.cs**。</span><span class="sxs-lookup"><span data-stu-id="da2dc-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="da2dc-343">在**web 应用程序中，** 包含 `MapSignalR` 方法的 Owin startup 类随后使用 web.config 文件的 "应用程序设置" 节点中的条目添加到 Owin 的启动进程，如下所示。</span><span class="sxs-lookup"><span data-stu-id="da2dc-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="da2dc-344">在**自承载的应用程序**中，Startup 类作为 `WebApp.Start` 方法的类型参数进行传递。</span><span class="sxs-lookup"><span data-stu-id="da2dc-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="da2dc-345">**在 SignalR 1.x 中映射中心和连接（从 web 应用程序中的全局应用程序文件）：**</span><span class="sxs-lookup"><span data-stu-id="da2dc-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="da2dc-346">**在 SignalR 2.0 （来自 Owin Startup 类文件）中映射中心和连接：**</span><span class="sxs-lookup"><span data-stu-id="da2dc-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="da2dc-347">在**自承载的应用程序**中，Startup 类作为 `WebApp.Start` 方法的类型参数进行传递，如下所示。</span><span class="sxs-lookup"><span data-stu-id="da2dc-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="da2dc-348">跨域支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-348">Cross-Domain Support</span></span>

<span data-ttu-id="da2dc-349">在 SignalR 1.x 中，跨域请求由单个 EnableCrossDomain 标志控制。</span><span class="sxs-lookup"><span data-stu-id="da2dc-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="da2dc-350">此标志控制 JSONP 和 CORS 请求。</span><span class="sxs-lookup"><span data-stu-id="da2dc-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="da2dc-351">为了获得更大的灵活性，已从 SignalR 的服务器组件中删除了所有 CORS 支持（如果检测到浏览器支持，JavaScript 客户端仍使用 CORS），并提供了新的 OWIN 中间件以支持这些方案。</span><span class="sxs-lookup"><span data-stu-id="da2dc-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="da2dc-352">在 SignalR 2.0 中，如果在客户端上需要 JSONP （以支持较早的浏览器中的跨域请求），则需要通过将 `HubConfiguration` 对象的 `EnableJSONP` 设置为 `true`显式启用此功能，如下所示。</span><span class="sxs-lookup"><span data-stu-id="da2dc-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="da2dc-353">默认情况下，JSONP 处于禁用状态，因为它的安全性低于 CORS。</span><span class="sxs-lookup"><span data-stu-id="da2dc-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="da2dc-354">若要在 SignalR 2.0 中添加新的 CORS 中间件，请将 `Microsoft.Owin.Cors` 库添加到项目中，并在 SignalR 中间件之前调用 `UseCors`，如下一节所示。</span><span class="sxs-lookup"><span data-stu-id="da2dc-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="da2dc-355">**将 Owin 添加到你的项目**：若要安装此库，请在包管理器控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="da2dc-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="da2dc-356">此命令会将2.0.0 版本的包添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="da2dc-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="da2dc-357">**调用 UseCors**</span><span class="sxs-lookup"><span data-stu-id="da2dc-357">**Calling UseCors**</span></span>

<span data-ttu-id="da2dc-358">以下代码片段演示了如何在 SignalR 1.x 和2.0 中实现跨域连接。</span><span class="sxs-lookup"><span data-stu-id="da2dc-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="da2dc-359">**在 SignalR 1.x 中实现跨域请求（来自全局应用程序文件）**</span><span class="sxs-lookup"><span data-stu-id="da2dc-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="da2dc-360">**在 SignalR 2.0 中实现跨域请求（从C#代码文件）**</span><span class="sxs-lookup"><span data-stu-id="da2dc-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="da2dc-361">下面的代码演示如何在 SignalR 2.0 项目中启用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="da2dc-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="da2dc-362">此代码示例使用 `Map` 和 `RunSignalR` 而不是 `MapSignalR`，因此，CORS 中间件仅针对需要 CORS 支持的 SignalR 请求（而不是在 `MapSignalR`中指定的路径上的所有流量）运行。 `Map` 也可用于需要针对特定 URL 前缀（而不是整个应用程序）运行的任何其他中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="da2dc-363">通过 Monotouch.dialog 和 MonoDroid 支持 iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="da2dc-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="da2dc-364">已为 iOS 和 Android 客户端使用[Xamarin 库](https://xamarin.com/)中的 Monotouch.dialog 和 MonoDroid 组件添加了支持。</span><span class="sxs-lookup"><span data-stu-id="da2dc-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="da2dc-365">有关如何使用它们的详细信息，请参阅[使用 Xamarin 组件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="da2dc-366">当 SignalR RTW 版本可用时，这些组件将在[Xamarin 应用商店](https://store.xamarin.com/)中提供。</span><span class="sxs-lookup"><span data-stu-id="da2dc-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="da2dc-367"># # # 可移植的 .NET 客户端</span><span class="sxs-lookup"><span data-stu-id="da2dc-367">### Portable .NET client</span></span>

<span data-ttu-id="da2dc-368">为了更好地促进跨平台开发，Silverlight、WinRT 和 Windows Phone 客户端已替换为支持以下平台的单个可移植 .NET 客户端：</span><span class="sxs-lookup"><span data-stu-id="da2dc-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="da2dc-369">NET 4。5</span><span class="sxs-lookup"><span data-stu-id="da2dc-369">NET 4.5</span></span>
- <span data-ttu-id="da2dc-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="da2dc-370">Silverlight 5</span></span>
- <span data-ttu-id="da2dc-371">WinRT （适用于 Windows 应用商店应用的 .NET）</span><span class="sxs-lookup"><span data-stu-id="da2dc-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="da2dc-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="da2dc-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="da2dc-373">新的自主机包</span><span class="sxs-lookup"><span data-stu-id="da2dc-373">New Self-Host Package</span></span>

<span data-ttu-id="da2dc-374">现在提供了一个 NuGet 包，可让你更轻松地开始使用 SignalR 自托管（SignalR 应用程序托管在进程或其他应用程序中，而不是托管在 web 服务器中）。</span><span class="sxs-lookup"><span data-stu-id="da2dc-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="da2dc-375">若要升级使用 SignalR 1.x 生成的自承载项目，请删除 SignalR. Owin 包，并添加包。 "SignalR"。</span><span class="sxs-lookup"><span data-stu-id="da2dc-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="da2dc-376">有关自承载包入门的详细信息，请参阅[教程： SignalR 自承载](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="da2dc-377">向后兼容的服务器支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-377">Backward-compatible server support</span></span>

<span data-ttu-id="da2dc-378">在以前版本的 SignalR 中，客户端和服务器中使用的 SignalR 包的版本需要完全相同。</span><span class="sxs-lookup"><span data-stu-id="da2dc-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="da2dc-379">为了支持难以更新的胖客户端应用程序，SignalR 2.0 现在支持将更新的服务器版本与较旧的客户端配合使用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="da2dc-380">**注意： SignalR 2.0 不支持用较新的客户端版本生成的服务器。**</span><span class="sxs-lookup"><span data-stu-id="da2dc-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="da2dc-381">删除了对 .NET 4.0 的服务器支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="da2dc-382">SignalR 2.0 已删除对服务器与 .NET 4.0 的互操作性的支持。</span><span class="sxs-lookup"><span data-stu-id="da2dc-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="da2dc-383">.NET 4.5 必须与 SignalR 2.0 服务器一起使用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="da2dc-384">还有一个适用于 SignalR 2.0 的 .NET 4.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="da2dc-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="da2dc-385">将消息发送到客户端和组的列表</span><span class="sxs-lookup"><span data-stu-id="da2dc-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="da2dc-386">在 SignalR 2.0 中，可以使用客户端和组 Id 的列表发送消息。</span><span class="sxs-lookup"><span data-stu-id="da2dc-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="da2dc-387">下面的代码段演示了如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="da2dc-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="da2dc-388">**使用 PersistentConnection 将消息发送到客户端和组的列表**</span><span class="sxs-lookup"><span data-stu-id="da2dc-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="da2dc-389">**使用集线器将消息发送到客户端和组的列表**</span><span class="sxs-lookup"><span data-stu-id="da2dc-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="da2dc-390">向特定用户发送消息</span><span class="sxs-lookup"><span data-stu-id="da2dc-390">Sending a message to a specific user</span></span>

<span data-ttu-id="da2dc-391">此功能允许用户通过新的接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容：</span><span class="sxs-lookup"><span data-stu-id="da2dc-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="da2dc-392">**IUserIdProvider 接口**</span><span class="sxs-lookup"><span data-stu-id="da2dc-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="da2dc-393">默认情况下，将使用用户的 IPrincipal.Identity.Name 作为用户名。</span><span class="sxs-lookup"><span data-stu-id="da2dc-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="da2dc-394">在中心，你可以通过新的 API 向这些用户发送消息：</span><span class="sxs-lookup"><span data-stu-id="da2dc-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="da2dc-395">**使用客户端 API**</span><span class="sxs-lookup"><span data-stu-id="da2dc-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="da2dc-396">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="da2dc-396">Better Error Handling Support</span></span>

<span data-ttu-id="da2dc-397">用户现在可以从任何中心调用中引发**HubException** 。</span><span class="sxs-lookup"><span data-stu-id="da2dc-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="da2dc-398">**HubException**的构造函数可以采用字符串消息和对象额外的错误数据。</span><span class="sxs-lookup"><span data-stu-id="da2dc-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="da2dc-399">SignalR 会自动对异常进行序列化，并将其发送到客户端，在该客户端将使用该异常拒绝/使中心方法调用失败。</span><span class="sxs-lookup"><span data-stu-id="da2dc-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="da2dc-400">**显示详细的中心异常**设置与发送回客户端的**HubException**无关;始终发送。</span><span class="sxs-lookup"><span data-stu-id="da2dc-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="da2dc-401">**演示如何将 HubException 发送到客户端的服务器端代码**</span><span class="sxs-lookup"><span data-stu-id="da2dc-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="da2dc-402">**演示响应从服务器发送的 HubException 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="da2dc-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="da2dc-403">**.NET 客户端代码演示响应从服务器发送的 HubException**</span><span class="sxs-lookup"><span data-stu-id="da2dc-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="da2dc-404">简化集线器的单元测试</span><span class="sxs-lookup"><span data-stu-id="da2dc-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="da2dc-405">SignalR 2.0 在集线器上包含一个名为 `IHubCallerConnectionContext` 的接口，使其更易于创建模拟客户端调用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="da2dc-406">以下代码段演示了如何将此接口与常用测试能力[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)一起使用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="da2dc-407">**通过 xUnit.net 进行单元测试 SignalR**</span><span class="sxs-lookup"><span data-stu-id="da2dc-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="da2dc-408">**通过 moq 进行单元测试 SignalR**</span><span class="sxs-lookup"><span data-stu-id="da2dc-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="da2dc-409">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="da2dc-409">JavaScript error handling</span></span>

<span data-ttu-id="da2dc-410">在 SignalR 2.0 中，所有 JavaScript 错误处理回调都返回 JavaScript 错误对象，而不是原始字符串。</span><span class="sxs-lookup"><span data-stu-id="da2dc-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="da2dc-411">这允许 SignalR 将更丰富的信息流式传输到错误处理程序。</span><span class="sxs-lookup"><span data-stu-id="da2dc-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="da2dc-412">你可以从错误的 `source` 属性获取内部异常。</span><span class="sxs-lookup"><span data-stu-id="da2dc-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="da2dc-413">**处理 Start 的 JavaScript 客户端代码。 Fail 异常**</span><span class="sxs-lookup"><span data-stu-id="da2dc-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="da2dc-414">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="da2dc-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="da2dc-415">新的 ASP.NET 成员资格系统</span><span class="sxs-lookup"><span data-stu-id="da2dc-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="da2dc-416">ASP.NET Identity 是 ASP.NET 应用程序的新成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="da2dc-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="da2dc-417">ASP.NET Identity 可以轻松地将特定于用户的配置文件数据与应用程序数据相集成。</span><span class="sxs-lookup"><span data-stu-id="da2dc-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="da2dc-418">ASP.NET Identity 还允许您为应用程序中的用户配置文件选择持久性模型。</span><span class="sxs-lookup"><span data-stu-id="da2dc-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="da2dc-419">你可以将数据存储在 SQL Server 数据库或其他数据存储中，包括 Azure 存储表等 NoSQL 数据存储。</span><span class="sxs-lookup"><span data-stu-id="da2dc-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="da2dc-420">有关详细信息，请参阅**在 Visual Studio 2013 中创建 ASP.NET Web 项目**中的[单个用户帐户](creating-web-projects-in-visual-studio.md#indauth)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="da2dc-421">基于声明的身份验证</span><span class="sxs-lookup"><span data-stu-id="da2dc-421">Claims-based authentication</span></span>

<span data-ttu-id="da2dc-422">ASP.NET 现在支持基于声明的身份验证，其中用户的标识表示为来自受信任颁发者的一组声明。</span><span class="sxs-lookup"><span data-stu-id="da2dc-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="da2dc-423">用户可以使用应用程序数据库中维护的用户名和密码进行身份验证，或使用社交标识提供者（例如，Microsoft 帐户、Facebook、Google、Twitter），或通过 Azure Active Directory 或使用组织帐户进行身份验证。Active Directory 联合身份验证服务（ADFS）。</span><span class="sxs-lookup"><span data-stu-id="da2dc-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="da2dc-424">与 Azure Active Directory 和 Windows Server Active Directory 的集成</span><span class="sxs-lookup"><span data-stu-id="da2dc-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="da2dc-425">你现在可以创建使用 Azure Active Directory 或 Windows Server Active Directory （AD）进行身份验证的 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="da2dc-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="da2dc-426">有关详细信息，请参阅**在 Visual Studio 2013 中创建 ASP.NET Web 项目**中的[组织帐户](creating-web-projects-in-visual-studio.md#orgauth)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="da2dc-427">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="da2dc-427">OWIN Integration</span></span>

<span data-ttu-id="da2dc-428">ASP.NET authentication 现在基于可在任何基于 OWIN 的主机上使用的 OWIN 中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="da2dc-429">有关 OWIN 的详细信息，请参阅以下[MICROSOFT OWIN 组件](#TOC7)部分。</span><span class="sxs-lookup"><span data-stu-id="da2dc-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="da2dc-430">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="da2dc-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="da2dc-431">[开放式 Web Interface for .net](http://owin.org/) （OWIN）定义 .net web 服务器和 Web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="da2dc-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="da2dc-432">OWIN 使 web 应用程序与服务器分离，使 web 应用程序不可知。</span><span class="sxs-lookup"><span data-stu-id="da2dc-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="da2dc-433">例如，你可以在 IIS 中托管基于 OWIN 的 web 应用程序，或在自定义进程中自行托管该应用程序。</span><span class="sxs-lookup"><span data-stu-id="da2dc-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="da2dc-434">Microsoft OWIN 组件（也称为 Katana 项目）中引入的更改包括新服务器和主机组件、新的帮助程序库和中间件，以及新的身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="da2dc-435">有关 OWIN 和 Katana 的详细信息，请参阅[OWIN 和 Katana 中的新增功能](../../../aspnet/overview/owin-and-katana/index.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="da2dc-436">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序不能在 IIS 经典模式下运行;它们必须在集成模式下运行。**</span><span class="sxs-lookup"><span data-stu-id="da2dc-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="da2dc-437">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序必须在完全信任环境中运行。**</span><span class="sxs-lookup"><span data-stu-id="da2dc-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="da2dc-438">新服务器和主机</span><span class="sxs-lookup"><span data-stu-id="da2dc-438">New Servers and Hosts</span></span>

<span data-ttu-id="da2dc-439">在此版本中，添加了新组件以启用自托管方案。</span><span class="sxs-lookup"><span data-stu-id="da2dc-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="da2dc-440">这些组件包括以下 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="da2dc-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="da2dc-441">**Owin. HttpListener**。</span><span class="sxs-lookup"><span data-stu-id="da2dc-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="da2dc-442">提供一个 OWIN 服务器，该服务器使用**HttpListener**侦听 HTTP 请求并将其定向到 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="da2dc-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="da2dc-443">**Owin**为希望在自定义进程（如控制台应用程序或 Windows 服务）中自行承载 Owin 管道的开发人员提供了一个库。</span><span class="sxs-lookup"><span data-stu-id="da2dc-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="da2dc-444">**Owinhost.exe**。</span><span class="sxs-lookup"><span data-stu-id="da2dc-444">**OwinHost**.</span></span> <span data-ttu-id="da2dc-445">提供一个独立的可执行文件，该可执行文件包装 `Microsoft.Owin.Hosting` 并使你能够在无需编写自定义主机应用程序的情况下自行承载 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="da2dc-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="da2dc-446">此外，`Microsoft.Owin.Host.SystemWeb` 包现在使中间件能够向**SystemWeb**服务器提供提示，指出应在特定 ASP.NET 管道阶段调用中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="da2dc-447">此功能对于应在 ASP.NET 管道中及早运行的身份验证中间件特别有用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="da2dc-448">帮助程序库和中间件</span><span class="sxs-lookup"><span data-stu-id="da2dc-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="da2dc-449">尽管只能使用 OWIN 规范中的函数和类型定义编写 OWIN 组件，但新的 `Microsoft.Owin` 包提供了更易于用户使用的抽象集。</span><span class="sxs-lookup"><span data-stu-id="da2dc-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="da2dc-450">此包将几个早期包（例如 `Owin.Extensions`、`Owin.Types`）合并为一个结构良好的对象模型，该对象模型随后可供其他 OWIN 组件轻松使用。</span><span class="sxs-lookup"><span data-stu-id="da2dc-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="da2dc-451">事实上，大多数 Microsoft OWIN 组件现在都使用此包。</span><span class="sxs-lookup"><span data-stu-id="da2dc-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="da2dc-452">[OWIN](http://www.owin.org)应用程序无法在 IIS 经典模式下运行;它们必须在集成模式下运行。</span><span class="sxs-lookup"><span data-stu-id="da2dc-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="da2dc-453">[OWIN](http://www.owin.org)应用程序必须在完全信任环境中运行。</span><span class="sxs-lookup"><span data-stu-id="da2dc-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="da2dc-454">此版本还包括 Owin 包，其中包括用于验证正在运行的 OWIN 应用程序的中间件，以及用于帮助调查失败的错误页中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="da2dc-455">身份验证组件</span><span class="sxs-lookup"><span data-stu-id="da2dc-455">Authentication Components</span></span>

<span data-ttu-id="da2dc-456">可以使用以下身份验证组件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-456">The following authentication components are available.</span></span>

- <span data-ttu-id="da2dc-457">**Microsoft Owin**。</span><span class="sxs-lookup"><span data-stu-id="da2dc-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="da2dc-458">使用本地或基于云的目录服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="da2dc-459">**Owin**使用 cookie 启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="da2dc-460">此程序包以前名为 `Microsoft.Owin.Security.Forms`。</span><span class="sxs-lookup"><span data-stu-id="da2dc-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="da2dc-461">**Owin**使用 facebook 的基于 OAuth 的服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="da2dc-462">**Owin**使用 google 的基于 OpenID 的服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="da2dc-463">**Owin**使用 jwt 令牌启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="da2dc-464">**Owin. MicrosoftAccount**启用使用 Microsoft 帐户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="da2dc-465">**Microsoft Owin**。</span><span class="sxs-lookup"><span data-stu-id="da2dc-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="da2dc-466">提供 OAuth 授权服务器，以及用于对持有者令牌进行身份验证的中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="da2dc-467">**Owin**使用 twitter 的基于 OAuth 的服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="da2dc-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="da2dc-468">此版本还包括 `Microsoft.Owin.Cors` 包，其中包含用于处理跨源 HTTP 请求的中间件。</span><span class="sxs-lookup"><span data-stu-id="da2dc-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="da2dc-469">Visual Studio 2013 的最终版本中已删除对 JWT 签名的支持。</span><span class="sxs-lookup"><span data-stu-id="da2dc-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="da2dc-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="da2dc-470">Entity Framework 6</span></span>

<span data-ttu-id="da2dc-471">有关实体框架6中的新功能和其他更改的列表，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="da2dc-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="da2dc-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="da2dc-473">ASP.NET Razor 3 包含以下新功能：</span><span class="sxs-lookup"><span data-stu-id="da2dc-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="da2dc-474">支持选项卡编辑。</span><span class="sxs-lookup"><span data-stu-id="da2dc-474">Support for Tab editing.</span></span> <span data-ttu-id="da2dc-475">以前，使用 "**保留选项卡**" 选项时，Visual Studio 中的**格式文档**命令、自动缩进和自动格式设置不能正常工作。</span><span class="sxs-lookup"><span data-stu-id="da2dc-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="da2dc-476">此更改纠正了用于 tab 格式的 Razor 代码的 Visual Studio 格式设置。</span><span class="sxs-lookup"><span data-stu-id="da2dc-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="da2dc-477">在生成链接时支持 URL 重写规则。</span><span class="sxs-lookup"><span data-stu-id="da2dc-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="da2dc-478">删除安全透明特性。</span><span class="sxs-lookup"><span data-stu-id="da2dc-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="da2dc-479">这是一项重大更改，使 Razor 3 与 MVC4 及更早版本不兼容，而 Razor 2 与 MVC5 或针对 MVC5 编译的程序集不兼容。</span><span class="sxs-lookup"><span data-stu-id="da2dc-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="da2dc-480">Razor 3 从预发行版本中修复的问题，可在[此处](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="da2dc-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="da2dc-481">ASP.NET 应用挂起</span><span class="sxs-lookup"><span data-stu-id="da2dc-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="da2dc-482">ASP.NET 应用暂停是 .NET Framework 4.5.1 中的游戏变化功能，它在一台计算机上彻底更改用于承载大量 ASP.NET 站点的用户体验和经济模型。</span><span class="sxs-lookup"><span data-stu-id="da2dc-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="da2dc-483">有关详细信息，请参阅[ASP.NET 应用挂起–响应式 shared .net web 托管](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="da2dc-484">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="da2dc-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="da2dc-485">本部分介绍 Visual Studio 2013 的 ASP.NET 和 Web 工具中的已知问题和重大更改。</span><span class="sxs-lookup"><span data-stu-id="da2dc-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="da2dc-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="da2dc-486">NuGet</span></span>

- <span data-ttu-id="da2dc-487">[使用 SLN 文件时，新的包还原不适用于 Mono](https://nuget.codeplex.com/workitem/3596) -将在即将发布的 nuget.exe 下载和[nuget 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中得到解决。</span><span class="sxs-lookup"><span data-stu-id="da2dc-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="da2dc-488">[新包还原不适用于 Wix 项目](https://nuget.codeplex.com/workitem/3598)–将在即将发布的 nuget.exe 下载和[nuget 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中得到修复。</span><span class="sxs-lookup"><span data-stu-id="da2dc-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="da2dc-489">[自动包还原对于解决方案文件夹下的项目不起作用](https://nuget.codeplex.com/workitem/3625)–将在 NuGet 2.8 中进行修复。</span><span class="sxs-lookup"><span data-stu-id="da2dc-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="da2dc-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="da2dc-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="da2dc-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` 不会 `IQueryable<T>` 总是返回，因为我们添加了对 `$select` 和 `$expand`的支持。</span><span class="sxs-lookup"><span data-stu-id="da2dc-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="da2dc-492">`ODataQueryOptions<T>` 的前面的示例始终将从 `ApplyTo` 到 `IQueryable<T>`的返回值强制转换。</span><span class="sxs-lookup"><span data-stu-id="da2dc-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="da2dc-493">这是早期工作的，因为我们以前支持的查询选项（`$filter`、`$orderby`、`$skip``$top`）不会更改查询的形状。</span><span class="sxs-lookup"><span data-stu-id="da2dc-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="da2dc-494">现在，我们支持 `$select` 和 `$expand` `ApplyTo` 的返回值将不 `IQueryable<T>`。</span><span class="sxs-lookup"><span data-stu-id="da2dc-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="da2dc-495">如果使用的是前面的示例代码，则在客户端不发送 `$select` 和 `$expand`时，它将继续工作。</span><span class="sxs-lookup"><span data-stu-id="da2dc-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="da2dc-496">但是，如果要支持 `$select` 和 `$expand` 必须将该代码更改为此代码。</span><span class="sxs-lookup"><span data-stu-id="da2dc-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="da2dc-497">**在批处理请求期间，request. Url 或 RequestContext 为 null**</span><span class="sxs-lookup"><span data-stu-id="da2dc-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="da2dc-498">在批处理方案中，当从**Request**或**RequestContext**访问时， **UrlHelper**为 null。</span><span class="sxs-lookup"><span data-stu-id="da2dc-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="da2dc-499">此问题当前在此处跟踪：[对于批处理请求，BatchRequestContext 为 null](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="da2dc-500">此问题的解决方法是创建**UrlHelper**的新实例，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="da2dc-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="da2dc-501">**创建 UrlHelper 的新实例**</span><span class="sxs-lookup"><span data-stu-id="da2dc-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="da2dc-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="da2dc-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="da2dc-503">使用 MVC5 和 OrgAuth 时，如果有可进行 AntiForgerToken 验证的视图，则在将数据发布到视图时，可能会遇到以下错误：</span><span class="sxs-lookup"><span data-stu-id="da2dc-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="da2dc-504">**错误**：</span><span class="sxs-lookup"><span data-stu-id="da2dc-504">**Error**:</span></span>

    <span data-ttu-id="da2dc-505">*"/" 应用程序中出现服务器错误。*</span><span class="sxs-lookup"><span data-stu-id="da2dc-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="da2dc-506"><em>所提供的 ClaimsIdentity 上不存在类型为 "<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>" 或 "<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>" 的声明。若要使用基于声明的身份验证启用防伪令牌支持，请验证配置的声明提供程序是否在其生成的 ClaimsIdentity 实例上同时提供这两个声明。如果配置的声明提供程序改用不同的声明类型作为唯一标识符，则可以通过设置静态属性 AntiForgeryConfig 来配置它。</em></span><span class="sxs-lookup"><span data-stu-id="da2dc-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="da2dc-507">**解决方法**：</span><span class="sxs-lookup"><span data-stu-id="da2dc-507">**Workaround**:</span></span>

    <span data-ttu-id="da2dc-508">在 global.asax 中添加以下行以修复此问题：</span><span class="sxs-lookup"><span data-stu-id="da2dc-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="da2dc-509">这将在下一版本中修复。</span><span class="sxs-lookup"><span data-stu-id="da2dc-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="da2dc-510">将 MVC4 应用升级到 MVC5 后，生成并启动解决方案。</span><span class="sxs-lookup"><span data-stu-id="da2dc-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="da2dc-511">应会看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="da2dc-511">You should see the following error:</span></span>

    <span data-ttu-id="da2dc-512">的HostSection 不能强制转换为 [B] System.web. HostSection. e e。</span><span class="sxs-lookup"><span data-stu-id="da2dc-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="da2dc-513">在位置 "C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35" 的上下文 "默认" 中的 "System.web： Razor，Version = 2.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35" 类型中，键入。</span><span class="sxs-lookup"><span data-stu-id="da2dc-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="da2dc-514">类型 B 源自 "C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ 3.0.0.0" 的上下文 "Default" 中的 "System.web. Razor，Version ="、"Culture = 中性，PublicKeyToken = 31bf3856ad364e35"。</span><span class="sxs-lookup"><span data-stu-id="da2dc-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="da2dc-515">若要修复上述错误，请在项目中打开*所有*web.config 文件（包括 Views 文件夹中的文件），然后执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="da2dc-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="da2dc-516">将 "4.0.0.0" 版本的所有实例更新为 "5.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="da2dc-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="da2dc-517">更新 "3.0.0.0" 版本的所有匹配项，&quot;System.web&quot; 并将 &quot;为 "" 的 "&quot; System.web. r</span><span class="sxs-lookup"><span data-stu-id="da2dc-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="da2dc-518">例如，在进行上述更改后，程序集绑定应如下所示：</span><span class="sxs-lookup"><span data-stu-id="da2dc-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="da2dc-519">有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将 ASP.NET mvc 4 和 WEB Api 项目升级到 ASP.NET mvc 5 和 WEB api 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="da2dc-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="da2dc-520">将客户端验证与 jQuery 非引人注目验证一起使用时，验证消息对于类型为 "number" 的 HTML 输入元素有时是不正确的。</span><span class="sxs-lookup"><span data-stu-id="da2dc-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="da2dc-521">如果输入的数字无效，而不是需要有效数字的正确消息，则会显示必需值（"需要 Age 字段"）的验证错误。</span><span class="sxs-lookup"><span data-stu-id="da2dc-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="da2dc-522">此问题通常出现在 "创建" 和 "编辑" 视图中具有整数属性的模型的基架代码中。</span><span class="sxs-lookup"><span data-stu-id="da2dc-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="da2dc-523">若要解决此问题，请将编辑器帮助程序从以下内容更改：</span><span class="sxs-lookup"><span data-stu-id="da2dc-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="da2dc-524">结束时间：</span><span class="sxs-lookup"><span data-stu-id="da2dc-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="da2dc-525">ASP.NET MVC 5 不再支持部分信任。</span><span class="sxs-lookup"><span data-stu-id="da2dc-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="da2dc-526">链接到 MVC 或 WebAPI 二进制文件的项目应删除[SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性和[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="da2dc-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="da2dc-527">删除这些属性将消除编译器错误，如下所示。</span><span class="sxs-lookup"><span data-stu-id="da2dc-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="da2dc-528">请注意，在这种情况下，不能在同一个应用程序中使用4.0 和5.0 程序集。</span><span class="sxs-lookup"><span data-stu-id="da2dc-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="da2dc-529">需要将它们全部更新为5.0。</span><span class="sxs-lookup"><span data-stu-id="da2dc-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="da2dc-530">将网站托管在 intranet 区域中时，采用 Facebook 授权的 SPA 模板可能导致 IE 不稳定</span><span class="sxs-lookup"><span data-stu-id="da2dc-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="da2dc-531">SPA 模板提供与 Facebook 的外部登录。</span><span class="sxs-lookup"><span data-stu-id="da2dc-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="da2dc-532">当用模板创建的项目在本地运行时，登录可能会导致 IE 崩溃。</span><span class="sxs-lookup"><span data-stu-id="da2dc-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="da2dc-533">解决方案：</span><span class="sxs-lookup"><span data-stu-id="da2dc-533">Solution:</span></span>

1. <span data-ttu-id="da2dc-534">在 internet 区域中托管网站;或</span><span class="sxs-lookup"><span data-stu-id="da2dc-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="da2dc-535">在 IE 以外的浏览器中测试方案。</span><span class="sxs-lookup"><span data-stu-id="da2dc-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="da2dc-536">Web 窗体基架</span><span class="sxs-lookup"><span data-stu-id="da2dc-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="da2dc-537">Web 窗体基架已从 VS2013 中删除，并将在 Visual Studio 的未来更新中提供。</span><span class="sxs-lookup"><span data-stu-id="da2dc-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="da2dc-538">不过，你仍然可以通过添加 MVC 依赖项并为 MVC 生成基架，在 Web 窗体项目中使用基架。</span><span class="sxs-lookup"><span data-stu-id="da2dc-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="da2dc-539">你的项目将包含 Web 窗体和 MVC 的组合。</span><span class="sxs-lookup"><span data-stu-id="da2dc-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="da2dc-540">若要将 MVC 添加到 Web 窗体项目，请添加一个新的基架项，并选择 " **MVC 5 依赖**项"。</span><span class="sxs-lookup"><span data-stu-id="da2dc-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="da2dc-541">选择 "最小" 或 "完整"，具体取决于是否需要所有内容文件，如脚本。</span><span class="sxs-lookup"><span data-stu-id="da2dc-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="da2dc-542">然后，为 MVC 添加基架项，这将在项目中创建视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="da2dc-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="da2dc-543">MVC 和 Web API 基架-HTTP 404，未找到错误</span><span class="sxs-lookup"><span data-stu-id="da2dc-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="da2dc-544">如果将基架项添加到项目时遇到错误，你的项目可能会处于不一致的状态。</span><span class="sxs-lookup"><span data-stu-id="da2dc-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="da2dc-545">所做的某些更改将被回滚，但其他更改（如安装的 NuGet 包）将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="da2dc-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="da2dc-546">如果回滚路由配置更改，则在导航到基架项时，用户将收到 HTTP 404 错误。</span><span class="sxs-lookup"><span data-stu-id="da2dc-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="da2dc-547">解决方法：</span><span class="sxs-lookup"><span data-stu-id="da2dc-547">Workaround:</span></span>

- <span data-ttu-id="da2dc-548">若要为 MVC 修复此错误，请添加一个新的基架项，并选择 "MVC 5 依赖项（最小或全部）"。</span><span class="sxs-lookup"><span data-stu-id="da2dc-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="da2dc-549">此过程将向你的项目添加所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="da2dc-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="da2dc-550">为 Web API 修复此错误：</span><span class="sxs-lookup"><span data-stu-id="da2dc-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="da2dc-551">将 Webapiconfig.cs 类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="da2dc-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="da2dc-552">按如下所示在 Webapiconfig.cs 中的应用程序\_Start 方法中配置：</span><span class="sxs-lookup"><span data-stu-id="da2dc-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
