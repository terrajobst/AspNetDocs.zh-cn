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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586754"
---
# <a name="aspnet-mvc-3"></a><span data-ttu-id="b8efb-103">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="b8efb-103">ASP.NET MVC 3</span></span>

> <span data-ttu-id="b8efb-104">*（包括2011年4月的工具更新）*</span><span class="sxs-lookup"><span data-stu-id="b8efb-104">*(includes April 2011 Tools Update)*</span></span>
> 
> <span data-ttu-id="b8efb-105">ASP.NET MVC 3 是一个框架，用于生成可缩放的基于标准的 web 应用程序，该应用程序使用良好构建的设计模式以及 ASP.NET 和 .NET Framework 的强大功能。</span><span class="sxs-lookup"><span data-stu-id="b8efb-105">ASP.NET MVC 3 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework.</span></span>
> 
> <span data-ttu-id="b8efb-106">它与 ASP.NET MVC 2 并行安装，因此马上就开始使用吧！</span><span class="sxs-lookup"><span data-stu-id="b8efb-106">It installs side-by-side with ASP.NET MVC 2, so get started using it today!</span></span>
> 
> <span data-ttu-id="b8efb-107">在[此处下载安装程序](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="b8efb-107">Download the [installer here](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>

## <a name="top-features"></a><span data-ttu-id="b8efb-108">顶级功能</span><span class="sxs-lookup"><span data-stu-id="b8efb-108">Top Features</span></span>

- <span data-ttu-id="b8efb-109">集成基架系统通过 NuGet 可扩展</span><span class="sxs-lookup"><span data-stu-id="b8efb-109">Integrated Scaffolding system extensible via NuGet</span></span>
- <span data-ttu-id="b8efb-110">已启用 HTML 5 的项目模板</span><span class="sxs-lookup"><span data-stu-id="b8efb-110">HTML 5 enabled project templates</span></span>
- <span data-ttu-id="b8efb-111">富有表现力的视图，包括新的 Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="b8efb-111">Expressive Views including the new Razor View Engine</span></span>
- <span data-ttu-id="b8efb-112">依赖关系注入和全局操作筛选器的强大挂钩</span><span class="sxs-lookup"><span data-stu-id="b8efb-112">Powerful hooks with Dependency Injection and Global Action Filters</span></span>
- <span data-ttu-id="b8efb-113">具有非引人注目 JavaScript、jQuery 验证和 JSON 绑定的丰富 JavaScript 支持</span><span class="sxs-lookup"><span data-stu-id="b8efb-113">Rich JavaScript support with unobtrusive JavaScript, jQuery Validation, and JSON binding</span></span>
- <span data-ttu-id="b8efb-114">*阅读[下面](#overview)的完整功能列表*</span><span class="sxs-lookup"><span data-stu-id="b8efb-114">*Read the full feature list [below](#overview)*</span></span>

## <a name="top-links"></a><span data-ttu-id="b8efb-115">顶部链接</span><span class="sxs-lookup"><span data-stu-id="b8efb-115">Top Links</span></span>

<span data-ttu-id="b8efb-116">ASP.NET MVC 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="b8efb-116">What's New in ASP.NET MVC 3</span></span>

- <span data-ttu-id="b8efb-117">Phil Haack：已[发布 ASP.NET MVC 3](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="b8efb-117">Phil Haack: [ASP.NET MVC 3 Released](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span></span>
- <span data-ttu-id="b8efb-118">Scott Hanselman： [ASP.NET MVC3、WebMatrix、NuGet、IIS Express 和 Orchard 发布-在上下文中为 Microsoft 1 月版 Web 版本](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span><span class="sxs-lookup"><span data-stu-id="b8efb-118">Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express and Orchard released - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span></span>
- <span data-ttu-id="b8efb-119">Scott Guthrie：[宣布发布 ASP.NET MVC 3，IIS Express，SQL CE 4，Web 场框架，Orchard，WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span><span class="sxs-lookup"><span data-stu-id="b8efb-119">Scott Guthrie: [Announcing release of ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span></span>
- [<span data-ttu-id="b8efb-120">ASP.NET MVC 3 的发行说明</span><span class="sxs-lookup"><span data-stu-id="b8efb-120">Release Notes for ASP.NET MVC 3</span></span>](../whitepapers/mvc3-release-notes.md)

<span data-ttu-id="b8efb-121">安装和帮助</span><span class="sxs-lookup"><span data-stu-id="b8efb-121">Installation and Help</span></span>

- <span data-ttu-id="b8efb-122">使用[Web 平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)安装 ASP.NET MVC 3 （推荐）</span><span class="sxs-lookup"><span data-stu-id="b8efb-122">Install ASP.NET MVC 3 using the [Web Platform Installer (recommended)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span></span>
- <span data-ttu-id="b8efb-123">使用[安装程序可执行文件](https://go.microsoft.com/fwlink/?LinkID=208140)安装 ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="b8efb-123">Install ASP.NET MVC 3 using the [installer executable](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="b8efb-124">安装[ASP.NET MVC 3 For Visual Studio 11 开发人员预览版](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="b8efb-124">Install [ASP.NET MVC 3 for Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="b8efb-125">阅读[简介到 ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span><span class="sxs-lookup"><span data-stu-id="b8efb-125">Read the [Intro to ASP.NET MVC 3 tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span></span>
- <span data-ttu-id="b8efb-126">获取帮助并讨论[论坛](https://forums.asp.net/1146.aspx)中的 ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="b8efb-126">Get help and discuss ASP.NET MVC 3 in the [forums](https://forums.asp.net/1146.aspx)</span></span>

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a><span data-ttu-id="b8efb-127">ASP.NET MVC 3 Overview（ASP.NET MVC 3 概述）</span><span class="sxs-lookup"><span data-stu-id="b8efb-127">ASP.NET MVC 3 Overview</span></span>

<span data-ttu-id="b8efb-128">ASP.NET MVC 3 是在 ASP.NET MVC 1 和2上构建的，它添加了可简化代码和允许更深层扩展的强大功能。</span><span class="sxs-lookup"><span data-stu-id="b8efb-128">ASP.NET MVC 3 builds on ASP.NET MVC 1 and 2, adding great features that both simplify your code and allow deeper extensibility.</span></span> <span data-ttu-id="b8efb-129">本主题概述了此版本中包含的许多新功能，这些功能分为以下几个部分：</span><span class="sxs-lookup"><span data-stu-id="b8efb-129">This topic provides an overview of many of the new features that are included in this release, organized into the following sections:</span></span>

- [<span data-ttu-id="b8efb-130">具有 MvcScaffold 集成的可扩展基架</span><span class="sxs-lookup"><span data-stu-id="b8efb-130">Extensible Scaffolding with MvcScaffold integration</span></span>](#BM_MvcScaffolding)
- [<span data-ttu-id="b8efb-131">已启用 HTML 5 的项目模板</span><span class="sxs-lookup"><span data-stu-id="b8efb-131">HTML 5 enabled project templates</span></span>](#BM_HTML5)
- [<span data-ttu-id="b8efb-132">Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="b8efb-132">The Razor View Engine</span></span>](#BM_TheRazorViewEngine)
- [<span data-ttu-id="b8efb-133">支持多个视图引擎</span><span class="sxs-lookup"><span data-stu-id="b8efb-133">Support for Multiple View Engines</span></span>](#BM_Support_for_Multiple_View_Engines)
- [<span data-ttu-id="b8efb-134">控制器改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-134">Controller Improvements</span></span>](#BM_Controller_Improvements)
- [<span data-ttu-id="b8efb-135">JavaScript 和 Ajax</span><span class="sxs-lookup"><span data-stu-id="b8efb-135">JavaScript and Ajax</span></span>](#BM_JavaScript_and_Ajax_Improvements)
- [<span data-ttu-id="b8efb-136">模型验证改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-136">Model Validation Improvements</span></span>](#BM_Model_Validation_Improvements)
- [<span data-ttu-id="b8efb-137">依赖关系注入改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-137">Dependency Injection Improvements</span></span>](#BM_Dependency_Injection_Improvements)
- [<span data-ttu-id="b8efb-138">其他新功能</span><span class="sxs-lookup"><span data-stu-id="b8efb-138">Other New Features</span></span>](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a><span data-ttu-id="b8efb-139">具有 MvcScaffold 集成的可扩展基架</span><span class="sxs-lookup"><span data-stu-id="b8efb-139">Extensible Scaffolding with MvcScaffold integration</span></span>

<span data-ttu-id="b8efb-140">如果你完全不熟悉框架，则新的基架系统使你可以更轻松地选择并有效地使用，如果你有经验并且已经了解你所做的工作，则可以自动执行常见的开发任务。</span><span class="sxs-lookup"><span data-stu-id="b8efb-140">The new Scaffolding system makes it easier to pick up and start using productively if you're entirely new to the framework, and to automate common development tasks if you're experienced and already know what you're doing.</span></span>

<span data-ttu-id="b8efb-141">这是名为**MvcScaffolding**的新 NuGet*基架*包支持的。</span><span class="sxs-lookup"><span data-stu-id="b8efb-141">This is supported by new NuGet *scaffolding* package called **MvcScaffolding**.</span></span> <span data-ttu-id="b8efb-142">许多软件技术使用术语 "基架" 来表示 "快速生成软件的基本大纲，然后可以编辑并自定义。</span><span class="sxs-lookup"><span data-stu-id="b8efb-142">The term "Scaffolding" is used by many software technologies to mean "quickly generating a basic outline of your software that you can then edit and customize".</span></span> <span data-ttu-id="b8efb-143">我们为 ASP.NET MVC 创建的基架包在多个方案中极有好处：</span><span class="sxs-lookup"><span data-stu-id="b8efb-143">The scaffolding package we're creating for ASP.NET MVC is greatly beneficial in several scenarios:</span></span>

- <span data-ttu-id="b8efb-144">**如果你是首次学习 ASP.NET MVC**，因为它提供了一些有用的工作代码的快捷方式，你可以根据需要对其进行编辑和调整。</span><span class="sxs-lookup"><span data-stu-id="b8efb-144">**If you're learning ASP.NET MVC for the first time**, because it gives you a fast way to get some useful, working code, that you can then edit and adapt according to your needs.</span></span> <span data-ttu-id="b8efb-145">它为你节省了 trauma 的时间，让你看看空白页面并不知道从何处着手！</span><span class="sxs-lookup"><span data-stu-id="b8efb-145">It saves you from the trauma of looking at a blank page and having no idea where to start!</span></span>
- <span data-ttu-id="b8efb-146">**如果你知道 ASP.NET MVC 并且现在正在探索一些新的附加设备技术**，如对象关系映射器、视图引擎、测试库等，因为该技术的创建者可能还为其创建了基架包。</span><span class="sxs-lookup"><span data-stu-id="b8efb-146">**If you know ASP.NET MVC well and are now exploring some new add-on technology** such as an object-relational mapper, a view engine, a testing library, etc., because the creator of that technology may have also created a scaffolding package for it.</span></span>
- <span data-ttu-id="b8efb-147">**如果您的工作过程中重复创建了类似的类或文件**，则可以创建自定义框架来输出测试装置、部署脚本或其他任何所需的文件。</span><span class="sxs-lookup"><span data-stu-id="b8efb-147">**If your work involves repeatedly creating similar classes or files of some sort**, because you can create custom scaffolders that output test fixtures, deployment scripts, or whatever else you need.</span></span> <span data-ttu-id="b8efb-148">你的团队中的每个人都可以使用你的自定义框架。</span><span class="sxs-lookup"><span data-stu-id="b8efb-148">Everyone on your team can use your custom scaffolders, too.</span></span>

<span data-ttu-id="b8efb-149">MvcScaffolding 中的其他功能包括：</span><span class="sxs-lookup"><span data-stu-id="b8efb-149">Other features in MvcScaffolding include:</span></span>

- <span data-ttu-id="b8efb-150">支持C#和 VB 项目</span><span class="sxs-lookup"><span data-stu-id="b8efb-150">Support for C# and VB projects</span></span>
- <span data-ttu-id="b8efb-151">支持 Razor 和 ASPX 视图引擎</span><span class="sxs-lookup"><span data-stu-id="b8efb-151">Support for the Razor and ASPX view engines</span></span>
- <span data-ttu-id="b8efb-152">支持将基架导入 ASP.NET MVC 区域和使用自定义视图布局/主控形状</span><span class="sxs-lookup"><span data-stu-id="b8efb-152">Supports scaffolding into ASP.NET MVC areas and using custom view layouts/masters</span></span>
- <span data-ttu-id="b8efb-153">可以通过编辑 T4 模板轻松自定义输出</span><span class="sxs-lookup"><span data-stu-id="b8efb-153">You can easily customize the output by editing T4 templates</span></span>
- <span data-ttu-id="b8efb-154">你可以使用自定义 PowerShell 逻辑和自定义 T4 模板来添加全新的框架。</span><span class="sxs-lookup"><span data-stu-id="b8efb-154">You can add entirely new scaffolders using custom PowerShell logic and custom T4 templates.</span></span> <span data-ttu-id="b8efb-155">这些（及其提供的任何自定义参数）会自动显示在 "控制台" 选项卡的 "完成" 列表中。</span><span class="sxs-lookup"><span data-stu-id="b8efb-155">These (and any custom parameters you've given them) automatically appear in the console tab-completion list.</span></span>
- <span data-ttu-id="b8efb-156">你可以获取包含不同技术的其他框架的 NuGet 程序包（例如，有一个概念证明，一种用于 LINQ to SQL），并混合搭配它们</span><span class="sxs-lookup"><span data-stu-id="b8efb-156">You can get NuGet packages containing additional scaffolders for different technologies (e.g., there's a proof-of-concept one for LINQ to SQL now) and mix and match them together</span></span>

<span data-ttu-id="b8efb-157">ASP.NET MVC 3 工具更新包括对此基架系统的出色 Visual Studio 支持，例如：</span><span class="sxs-lookup"><span data-stu-id="b8efb-157">The ASP.NET MVC 3 Tools Update includes great Visual Studio support for this scaffolding system, such as:</span></span>

- <span data-ttu-id="b8efb-158">"添加控制器" 对话框现在支持 "创建"、"读取"、"更新" 和 "删除" 控制器操作和相应视图的完全自动基架。</span><span class="sxs-lookup"><span data-stu-id="b8efb-158">Add Controller Dialog now supports full automatic scaffolding of Create, Read, Update, and Delete controller actions and corresponding views.</span></span> <span data-ttu-id="b8efb-159">默认情况下，此基架使用 EF Code First 的数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="b8efb-159">By default, this scaffolds data access code using EF Code First.</span></span>
- <span data-ttu-id="b8efb-160">"添加控制器" 对话框支持通过 NuGet 包（如*MvcScaffolding*）进行*可扩展的基架*。</span><span class="sxs-lookup"><span data-stu-id="b8efb-160">Add Controller Dialog supports *extensible scaffolds* via NuGet packages such as *MvcScaffolding*.</span></span> <span data-ttu-id="b8efb-161">这允许将自定义基架插入对话框，使你可以为其他数据访问技术（例如 NHibernate，甚至是具有 ODBCDirect 的 JET）创建基架</span><span class="sxs-lookup"><span data-stu-id="b8efb-161">This allows plugging in custom scaffolds into the dialog which would allow you to create scaffolds for other data access technologies such as NHibernate or even JET with ODBCDirect if you're so inclined!</span></span>

<span data-ttu-id="b8efb-162">有关 ASP.NET MVC 3 中的基架的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b8efb-162">For more information about Scaffolding in ASP.NET MVC 3, see the following resources:</span></span>

- <span data-ttu-id="b8efb-163">Steve Sanderson 的文章系列，其中包括：</span><span class="sxs-lookup"><span data-stu-id="b8efb-163">Steve Sanderson's post series, including:</span></span> 

    1. [<span data-ttu-id="b8efb-164">简介：基架 ASP.NET MVC 3 project with the MvcScaffolding package</span><span class="sxs-lookup"><span data-stu-id="b8efb-164">Introduction: Scaffold your ASP.NET MVC 3 project with the MvcScaffolding package</span></span>](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [<span data-ttu-id="b8efb-165">标准用法：典型用例和选项</span><span class="sxs-lookup"><span data-stu-id="b8efb-165">Standard usage: Typical use cases and options</span></span>](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [<span data-ttu-id="b8efb-166">一对多关系</span><span class="sxs-lookup"><span data-stu-id="b8efb-166">One-to-Many Relationships</span></span>](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [<span data-ttu-id="b8efb-167">基架操作和单元测试</span><span class="sxs-lookup"><span data-stu-id="b8efb-167">Scaffolding Actions and Unit Tests</span></span>](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [<span data-ttu-id="b8efb-168">覆盖 T4 模板</span><span class="sxs-lookup"><span data-stu-id="b8efb-168">Overriding the T4 templates</span></span>](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [<span data-ttu-id="b8efb-169">这篇文章：创建自定义框架</span><span class="sxs-lookup"><span data-stu-id="b8efb-169">This post: Creating custom scaffolders</span></span>](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- <span data-ttu-id="b8efb-170">Scott Hanselman 在他的 PDC 2010 讲座中发布[了一篇博客，其中包含 Microsoft "未命名的 Web 喜爱包"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span><span class="sxs-lookup"><span data-stu-id="b8efb-170">Scott Hanselman's post from his PDC 2010 session [Building a Blog with Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span></span>
- [<span data-ttu-id="b8efb-171">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="b8efb-171">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a><span data-ttu-id="b8efb-172">HTML 5 项目模板</span><span class="sxs-lookup"><span data-stu-id="b8efb-172">HTML 5 Project Templates</span></span>

<span data-ttu-id="b8efb-173">"新建项目" 对话框包含一个复选框 "启用 HTML 5 版本的项目模板"。</span><span class="sxs-lookup"><span data-stu-id="b8efb-173">The New Project dialog includes a checkbox enable HTML 5 versions of project templates.</span></span> <span data-ttu-id="b8efb-174">这些模板利用 Modernizr 1.7 为底层浏览器中的 HTML 5 和 CSS 3 提供兼容性支持。</span><span class="sxs-lookup"><span data-stu-id="b8efb-174">These templates leverage Modernizr 1.7 to provide compatibility support for HTML 5 and CSS 3 in down-level browsers.</span></span>

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a><span data-ttu-id="b8efb-175">Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="b8efb-175">The Razor View Engine</span></span>

<span data-ttu-id="b8efb-176">ASP.NET MVC 3 附带了一个名为 Razor 的新视图引擎，它具有以下优势：</span><span class="sxs-lookup"><span data-stu-id="b8efb-176">ASP.NET MVC 3 comes with a new view engine named Razor that offers the following benefits:</span></span>

- <span data-ttu-id="b8efb-177">Razor 语法简洁明了，需要最少的击键数。</span><span class="sxs-lookup"><span data-stu-id="b8efb-177">Razor syntax is clean and concise, requiring a minimum number of keystrokes.</span></span>
- <span data-ttu-id="b8efb-178">Razor 易于学习，其中部分原因是它基于现有语言，如C#和 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="b8efb-178">Razor is easy to learn, in part because it's based on existing languages like C# and Visual Basic.</span></span>
- <span data-ttu-id="b8efb-179">Visual Studio 包括 Razor 语法的 IntelliSense 和代码着色。</span><span class="sxs-lookup"><span data-stu-id="b8efb-179">Visual Studio includes IntelliSense and code colorization for Razor syntax.</span></span>
- <span data-ttu-id="b8efb-180">Razor 视图可以进行单元测试，而无需运行应用程序或启动 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b8efb-180">Razor views can be unit tested without requiring that you run the application or launch a web server.</span></span>

<span data-ttu-id="b8efb-181">一些新的 Razor 功能包括：</span><span class="sxs-lookup"><span data-stu-id="b8efb-181">Some new Razor features include the following:</span></span>

- <span data-ttu-id="b8efb-182">`@model` 语法，用于指定传递给视图的类型。</span><span class="sxs-lookup"><span data-stu-id="b8efb-182">`@model` syntax for specifying the type being passed to the view.</span></span>
- <span data-ttu-id="b8efb-183">`@* *@` 注释语法。</span><span class="sxs-lookup"><span data-stu-id="b8efb-183">`@* *@` comment syntax.</span></span>
- <span data-ttu-id="b8efb-184">为整个站点指定一次默认值（例如 `layoutpage`）的功能。</span><span class="sxs-lookup"><span data-stu-id="b8efb-184">The ability to specify defaults (such as `layoutpage`) once for an entire site.</span></span>
- <span data-ttu-id="b8efb-185">用于显示文本的 `Html.Raw` 方法，无需对其进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="b8efb-185">The `Html.Raw` method for displaying text without HTML-encoding it.</span></span>
- <span data-ttu-id="b8efb-186">支持在多个视图中共享代码（ *\_viewstart.cshtml*或 *\_viewstart.cshtml*文件）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-186">Support for sharing code among multiple views (*\_viewstart.cshtml* or *\_viewstart.vbhtml* files).</span></span>

<span data-ttu-id="b8efb-187">Razor 还包括新的 HTML 帮助程序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8efb-187">Razor also includes  new HTML helpers, such as the following:</span></span>

- <span data-ttu-id="b8efb-188">`Chart`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-188">`Chart`.</span></span> <span data-ttu-id="b8efb-189">呈现图表，提供与 ASP.NET 4 中的图表控件相同的功能。</span><span class="sxs-lookup"><span data-stu-id="b8efb-189">Renders a chart, offering the same features as the chart control in ASP.NET 4.</span></span>
- <span data-ttu-id="b8efb-190">`WebGrid`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-190">`WebGrid`.</span></span> <span data-ttu-id="b8efb-191">呈现一个数据网格，其中包含分页和排序功能。</span><span class="sxs-lookup"><span data-stu-id="b8efb-191">Renders a data grid, complete with paging and sorting functionality.</span></span>
- <span data-ttu-id="b8efb-192">`Crypto`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-192">`Crypto`.</span></span> <span data-ttu-id="b8efb-193">使用哈希算法来创建正确的加盐和哈希密码。</span><span class="sxs-lookup"><span data-stu-id="b8efb-193">Uses hashing algorithms to create properly salted and hashed passwords.</span></span>
- <span data-ttu-id="b8efb-194">`WebImage`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-194">`WebImage`.</span></span> <span data-ttu-id="b8efb-195">呈现图像。</span><span class="sxs-lookup"><span data-stu-id="b8efb-195">Renders an image.</span></span>
- <span data-ttu-id="b8efb-196">`WebMail`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-196">`WebMail`.</span></span> <span data-ttu-id="b8efb-197">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="b8efb-197">Sends an email message.</span></span>

<span data-ttu-id="b8efb-198">有关 Razor 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b8efb-198">For more information about Razor, see the following resources:</span></span>

- [<span data-ttu-id="b8efb-199">Scott Guthrie 的博客文章介绍了 Razor</span><span class="sxs-lookup"><span data-stu-id="b8efb-199">Scott Guthrie's blog post introducing Razor</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [<span data-ttu-id="b8efb-200">Scott Guthrie 的博客文章介绍 @model 关键字</span><span class="sxs-lookup"><span data-stu-id="b8efb-200">Scott Guthrie's blog post introducing the @model keyword</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [<span data-ttu-id="b8efb-201">Scott Guthrie 的博客文章介绍了 Razor 布局</span><span class="sxs-lookup"><span data-stu-id="b8efb-201">Scott Guthrie's blog post introducing Razor layouts</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [<span data-ttu-id="b8efb-202">Razor API 快速参考</span><span class="sxs-lookup"><span data-stu-id="b8efb-202">Razor API Quick Reference</span></span>](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [<span data-ttu-id="b8efb-203">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="b8efb-203">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a><span data-ttu-id="b8efb-204">支持多个视图引擎</span><span class="sxs-lookup"><span data-stu-id="b8efb-204">Support for Multiple View Engines</span></span>

<span data-ttu-id="b8efb-205">在 ASP.NET MVC 3 中的 "**添加视图**" 对话框中，可以选择要使用的视图引擎，使用 "**新建项目**" 对话框可以指定项目的默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="b8efb-205">The **Add View** dialog box in ASP.NET MVC 3 lets you choose the view engine you want to work with, and the **New Project** dialog box lets you specify the default view engine for a project.</span></span> <span data-ttu-id="b8efb-206">您可以选择 Web 窗体视图引擎（ASPX）、Razor 或开源视图引擎，例如[Spark](http://sparkviewengine.com/)、 [NHaml](https://code.google.com/p/nhaml/)或[NDjango](http://ndjango.org/)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-206">You can choose the Web Forms view engine (ASPX), Razor, or an open-source view engine such as [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), or [NDjango](http://ndjango.org/).</span></span>

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a><span data-ttu-id="b8efb-207">控制器改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-207">Controller Improvements</span></span>

### <a name="global-action-filters"></a><span data-ttu-id="b8efb-208">全局操作筛选器</span><span class="sxs-lookup"><span data-stu-id="b8efb-208">Global Action Filters</span></span>

<span data-ttu-id="b8efb-209">有时，您需要在操作方法运行之前或操作方法运行之后执行逻辑。</span><span class="sxs-lookup"><span data-stu-id="b8efb-209">Sometimes you want to perform logic either before an action method runs or after an action method runs.</span></span> <span data-ttu-id="b8efb-210">为支持此操作，ASP.NET MVC 2 提供了操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="b8efb-210">To support this, ASP.NET MVC 2 provided action filters.</span></span> <span data-ttu-id="b8efb-211">操作筛选器是自定义属性，可提供用于向特定控制器操作方法添加操作前和操作后行为的声明性方法。</span><span class="sxs-lookup"><span data-stu-id="b8efb-211">Action filters are custom attributes that provide a declarative means to add pre-action and post-action behavior to specific controller action methods.</span></span> <span data-ttu-id="b8efb-212">但是，在某些情况下，你可能想要指定适用于所有操作方法的操作前或操作后行为。</span><span class="sxs-lookup"><span data-stu-id="b8efb-212">However, in some cases you might want to specify pre-action or post-action behavior that applies to all action methods.</span></span> <span data-ttu-id="b8efb-213">MVC 3 允许您通过将全局筛选器添加到 `GlobalFilters` 集合来指定全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="b8efb-213">MVC 3 lets you specify global filters by adding them to the `GlobalFilters` collection.</span></span> <span data-ttu-id="b8efb-214">有关全局操作筛选器的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b8efb-214">For more information about global action filters, see the following resources:</span></span>

- [<span data-ttu-id="b8efb-215">在 MVC 3 预览版中，Scott Guthrie 的博客</span><span class="sxs-lookup"><span data-stu-id="b8efb-215">Scott Guthrie's blog on the MVC 3 Preview</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- <span data-ttu-id="b8efb-216">[ASP.NET MVC 中的筛选](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="b8efb-216">[Filtering in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span></span>

### <a name="new-viewbag-property"></a><span data-ttu-id="b8efb-217">新的 "ViewBag" 属性</span><span class="sxs-lookup"><span data-stu-id="b8efb-217">New "ViewBag" Property</span></span>

<span data-ttu-id="b8efb-218">MVC 2 控制器支持 `ViewData` 属性，使你能够使用后期绑定字典 API 将数据传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="b8efb-218">MVC 2 controllers support a `ViewData` property that enables you to pass data to a view template using a late-bound dictionary API.</span></span> <span data-ttu-id="b8efb-219">在 MVC 3 中，你还可以对 `ViewBag` 属性使用略微简单的语法来实现相同的目的。</span><span class="sxs-lookup"><span data-stu-id="b8efb-219">In MVC 3, you can also use somewhat simpler syntax with the `ViewBag` property to accomplish the same purpose.</span></span> <span data-ttu-id="b8efb-220">例如，你可以编写 `ViewBag.Message="text"`，而不是编写 `ViewData["Message"]="text"`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-220">For example, instead of writing `ViewData["Message"]="text"`, you can write `ViewBag.Message="text"`.</span></span> <span data-ttu-id="b8efb-221">不需要定义任何强类型类来使用 `ViewBag` 属性。</span><span class="sxs-lookup"><span data-stu-id="b8efb-221">You do not need to define any strongly-typed classes to use the `ViewBag` property.</span></span> <span data-ttu-id="b8efb-222">由于它是动态属性，因此可以直接获取或设置属性，它将在运行时动态解析它们。</span><span class="sxs-lookup"><span data-stu-id="b8efb-222">Because it is a dynamic property, you can instead just get or set properties and it will resolve them dynamically at run time.</span></span> <span data-ttu-id="b8efb-223">在内部，`ViewBag` 属性作为名称/值对存储在 `ViewData` 字典中。</span><span class="sxs-lookup"><span data-stu-id="b8efb-223">Internally, `ViewBag` properties are stored as name/value pairs in the `ViewData` dictionary.</span></span> <span data-ttu-id="b8efb-224">（注意：在 MVC 3 的大多数预发布版本中，`ViewBag` 属性的名称都是 `ViewModel` 属性。）</span><span class="sxs-lookup"><span data-stu-id="b8efb-224">(Note: in most pre-release versions of MVC 3, the `ViewBag` property was named the `ViewModel` property.)</span></span>

### <a name="new-actionresult-types"></a><span data-ttu-id="b8efb-225">新 "ActionResult" 类型</span><span class="sxs-lookup"><span data-stu-id="b8efb-225">New "ActionResult" Types</span></span>

<span data-ttu-id="b8efb-226">以下 `ActionResult` 类型和相应的帮助器方法在 MVC 3 中是新增或增强的：</span><span class="sxs-lookup"><span data-stu-id="b8efb-226">The following `ActionResult` types and corresponding helper methods are new or enhanced in MVC 3:</span></span>

- <span data-ttu-id="b8efb-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx).</span></span> <span data-ttu-id="b8efb-228">向客户端返回 404 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="b8efb-228">Returns a 404 HTTP status code to the client.</span></span>
- <span data-ttu-id="b8efb-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx).</span></span> <span data-ttu-id="b8efb-230">返回临时重定向（HTTP 302 状态代码）或永久重定向（HTTP 301 状态代码），具体取决于布尔参数。</span><span class="sxs-lookup"><span data-stu-id="b8efb-230">Returns a temporary redirect (HTTP 302 status code) or a permanent redirect (HTTP 301 status code), depending on a Boolean parameter.</span></span> <span data-ttu-id="b8efb-231">与此更改一起，[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)类现在有三种执行永久重定向的方法： `RedirectPermanent`、`RedirectToRoutePermanent`和 `RedirectToActionPermanent`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-231">In conjunction with this change, the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) class now has three methods for performing permanent redirects: `RedirectPermanent`, `RedirectToRoutePermanent`, and `RedirectToActionPermanent`.</span></span> <span data-ttu-id="b8efb-232">这些方法返回 `RedirectResult` 的实例，`Permanent` 属性设置为 "`true`"。</span><span class="sxs-lookup"><span data-stu-id="b8efb-232">These methods return an instance of `RedirectResult` with the `Permanent` property set to `true`.</span></span>
- <span data-ttu-id="b8efb-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span></span> <span data-ttu-id="b8efb-234">返回用户指定的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="b8efb-234">Returns a user-specified HTTP status code.</span></span>

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a><span data-ttu-id="b8efb-235">JavaScript 和 Ajax 改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-235">JavaScript and Ajax Improvements</span></span>

<span data-ttu-id="b8efb-236">默认情况下，MVC 3 中的 Ajax 和验证帮助程序使用不引人注目的 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="b8efb-236">By default, Ajax and validation helpers in MVC 3 use an unobtrusive JavaScript approach.</span></span> <span data-ttu-id="b8efb-237">非引人注目的 JavaScript 避免将内联 JavaScript 注入到 HTML。</span><span class="sxs-lookup"><span data-stu-id="b8efb-237">Unobtrusive JavaScript avoids injecting inline JavaScript into HTML.</span></span> <span data-ttu-id="b8efb-238">这会使你的 HTML 更小、更简洁，并使你可以更轻松地交换或自定义 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="b8efb-238">This makes your HTML smaller and less cluttered, and makes it easier to swap out or customize JavaScript libraries.</span></span> <span data-ttu-id="b8efb-239">默认情况下，MVC 3 中的验证帮助器也使用 `jQueryValidate` 插件。</span><span class="sxs-lookup"><span data-stu-id="b8efb-239">Validation helpers in MVC 3 also use the `jQueryValidate` plugin by default.</span></span> <span data-ttu-id="b8efb-240">如果需要 MVC 2 行为，可以使用*web.config 文件设置*禁用非引人注目的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="b8efb-240">If you want MVC 2 behavior, you can disable unobtrusive JavaScript using a *web.config* file setting.</span></span> <span data-ttu-id="b8efb-241">有关 JavaScript 和 Ajax 改进的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b8efb-241">For more information about JavaScript and Ajax improvements, see the following resources:</span></span>

- [<span data-ttu-id="b8efb-242">维基百科网站上的非引人注目 JavaScript 的基本简介</span><span class="sxs-lookup"><span data-stu-id="b8efb-242">Basic introduction to unobtrusive JavaScript on the Wikipedia site</span></span>](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [<span data-ttu-id="b8efb-243">Brad Wilson 的非引人注目 JavaScript Post</span><span class="sxs-lookup"><span data-stu-id="b8efb-243">Brad Wilson's Unobtrusive JavaScript Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [<span data-ttu-id="b8efb-244">Brad Wilson 的非引人注目 JavaScript 验证 Post</span><span class="sxs-lookup"><span data-stu-id="b8efb-244">Brad Wilson's Unobtrusive JavaScript Validation Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- <span data-ttu-id="b8efb-245">[使用 Razor 和非引人注目 JavaScript 创建 MVC 3 应用程序](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET 网站上的教程）</span><span class="sxs-lookup"><span data-stu-id="b8efb-245">[Creating a MVC 3 Application with Razor and Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial on the ASP.NET site)</span></span>
- [<span data-ttu-id="b8efb-246">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="b8efb-246">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a><span data-ttu-id="b8efb-247">默认情况下启用客户端验证</span><span class="sxs-lookup"><span data-stu-id="b8efb-247">Client-Side Validation Enabled by Default</span></span>

<span data-ttu-id="b8efb-248">在 MVC 的早期版本中，需要从视图中显式调用 `Html.EnableClientValidation` 方法才能启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="b8efb-248">In earlier versions of MVC, you need to explicitly call the `Html.EnableClientValidation` method from a view in order to enable client-side validation.</span></span> <span data-ttu-id="b8efb-249">在 MVC 3 中，这不再是必需的，因为默认情况下会启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="b8efb-249">In MVC 3 this is no longer required because client-side validation is enabled by default.</span></span> <span data-ttu-id="b8efb-250">（您可以使用*web.config 文件中的设置*来禁用此设置。）</span><span class="sxs-lookup"><span data-stu-id="b8efb-250">(You can disable this using a setting in the *web.config* file.)</span></span>

<span data-ttu-id="b8efb-251">为了使客户端验证正常工作，你仍需要在你的站点中引用相应的 jQuery 和 jQuery 验证库。</span><span class="sxs-lookup"><span data-stu-id="b8efb-251">In order for client-side validation to work, you still need to reference the appropriate jQuery and jQuery Validation libraries in your site.</span></span> <span data-ttu-id="b8efb-252">你可以在自己的服务器上托管这些库，或者从 Microsoft 或 Google 等 Cdn 的内容交付网络（CDN）中引用它们。</span><span class="sxs-lookup"><span data-stu-id="b8efb-252">You can host those libraries on your own server or reference them from a content delivery network (CDN) like the CDNs from Microsoft or Google.</span></span>

### <a name="remote-validator"></a><span data-ttu-id="b8efb-253">远程验证程序</span><span class="sxs-lookup"><span data-stu-id="b8efb-253">Remote Validator</span></span>

<span data-ttu-id="b8efb-254">ASP.NET MVC 3 支持新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)类，使你能够利用 jQuery 验证插件的远程验证程序支持。</span><span class="sxs-lookup"><span data-stu-id="b8efb-254">ASP.NET MVC 3 supports the new [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) class that enables you to take advantage of the jQuery Validation plug-in's remote validator support.</span></span> <span data-ttu-id="b8efb-255">这样，客户端验证库就可以自动调用您在服务器上定义的自定义方法，以便执行只能在服务器端执行的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="b8efb-255">This enables the client-side validation library to automatically call a custom method that you define on the server in order to perform validation logic that can only be done server-side.</span></span>

<span data-ttu-id="b8efb-256">在下面的示例中，`Remote` 属性指定客户端验证将调用 `UsersController` 类上名为 `UserNameAvailable` 的操作，以便验证 `UserName` 字段。</span><span class="sxs-lookup"><span data-stu-id="b8efb-256">In the following example, the `Remote` attribute specifies that client validation will call an action named `UserNameAvailable` on the `UsersController` class in order to validate the `UserName` field.</span></span>

[!code-csharp[Main](mvc3/samples/sample1.cs)]

<span data-ttu-id="b8efb-257">下面的示例演示了相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="b8efb-257">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3/samples/sample2.cs)]

<span data-ttu-id="b8efb-258">有关如何使用 `Remote` 特性的详细信息，请参阅 MSDN library 中的[如何：在 ASP.NET MVC 中实现远程验证](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-258">For more information about how to use the `Remote` attribute, see [How to: Implement Remote Validation in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in the MSDN library.</span></span>

### <a name="json-binding-support"></a><span data-ttu-id="b8efb-259">JSON 绑定支持</span><span class="sxs-lookup"><span data-stu-id="b8efb-259">JSON Binding Support</span></span>

<span data-ttu-id="b8efb-260">ASP.NET MVC 3 包含内置 JSON 绑定支持，使操作方法可以接收 JSON 编码数据，并将其绑定到操作方法参数。</span><span class="sxs-lookup"><span data-stu-id="b8efb-260">ASP.NET MVC 3 includes built-in JSON binding support that enables action methods to receive JSON-encoded data and model-bind it to action-method parameters.</span></span> <span data-ttu-id="b8efb-261">此功能在涉及客户端模板和数据绑定的方案中很有用。</span><span class="sxs-lookup"><span data-stu-id="b8efb-261">This capability is useful in scenarios involving client templates and data binding.</span></span> <span data-ttu-id="b8efb-262">（客户端模板使你可以通过使用在客户端上执行的模板来设置和显示单个数据项或数据项集。）MVC 3 使你能够轻松地通过发送和接收 JSON 数据的服务器上的操作方法连接客户端模板。</span><span class="sxs-lookup"><span data-stu-id="b8efb-262">(Client templates enable you to format and display a single data item or set of data items by using templates that execute on the client.) MVC 3 enables you to easily connect client templates with action methods on the server that send and receive JSON data.</span></span> <span data-ttu-id="b8efb-263">有关 JSON 绑定支持的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览版博客文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)的**JavaScript 和 AJAX 改进**部分。</span><span class="sxs-lookup"><span data-stu-id="b8efb-263">For more information about JSON binding support, see the **JavaScript and AJAX Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span>

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a><span data-ttu-id="b8efb-264">模型验证改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-264">Model Validation Improvements</span></span>

### <a name="dataannotations-metadata-attributes"></a><span data-ttu-id="b8efb-265">"DataAnnotations" 元数据属性</span><span class="sxs-lookup"><span data-stu-id="b8efb-265">"DataAnnotations" Metadata Attributes</span></span>

<span data-ttu-id="b8efb-266">ASP.NET MVC 3 支持 `DataAnnotations` 元数据属性，如 `DisplayAttribute`。</span><span class="sxs-lookup"><span data-stu-id="b8efb-266">ASP.NET MVC 3 supports `DataAnnotations` metadata attributes such as `DisplayAttribute`.</span></span>

### <a name="validationattribute-class"></a><span data-ttu-id="b8efb-267">"ValidationAttribute" 类</span><span class="sxs-lookup"><span data-stu-id="b8efb-267">"ValidationAttribute" Class</span></span>

<span data-ttu-id="b8efb-268">`ValidationAttribute` 类在 .NET Framework 4 中得到了改进，以支持一个新的 `IsValid` 重载，该重载提供有关当前验证上下文的详细信息，例如要验证的对象。</span><span class="sxs-lookup"><span data-stu-id="b8efb-268">The `ValidationAttribute` class was improved in the .NET Framework 4 to support a new `IsValid` overload that provides more information about the current validation context, such as what object is being validated.</span></span> <span data-ttu-id="b8efb-269">这可以实现更丰富的方案，在这些方案中，你可以基于模型的另一个属性验证当前值。</span><span class="sxs-lookup"><span data-stu-id="b8efb-269">This enables richer scenarios where you can validate the current value based on another property of the model.</span></span> <span data-ttu-id="b8efb-270">例如，使用 new `CompareAttribute` 特性可以比较模型的两个属性的值。</span><span class="sxs-lookup"><span data-stu-id="b8efb-270">For example, the new `CompareAttribute` attribute lets you compare the values of two properties of a model.</span></span> <span data-ttu-id="b8efb-271">在下面的示例中，`ComparePassword` 属性必须匹配 `Password` 字段才能有效。</span><span class="sxs-lookup"><span data-stu-id="b8efb-271">In the following example, the `ComparePassword` property must match the `Password` field in order to be valid.</span></span>

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a><span data-ttu-id="b8efb-272">验证接口</span><span class="sxs-lookup"><span data-stu-id="b8efb-272">Validation Interfaces</span></span>

<span data-ttu-id="b8efb-273">通过[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)接口，您可以执行模型级别的验证，还可以提供验证错误消息，这些错误消息特定于整个模型的状态，或在模型中的两个属性之间。</span><span class="sxs-lookup"><span data-stu-id="b8efb-273">The [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) interface enables you to perform model-level validation, and it enables you to provide validation error messages that are specific to the state of the overall model, or between two properties within the model.</span></span> <span data-ttu-id="b8efb-274">在模型绑定时，MVC 3 现在从 `IValidatableObject` 接口检索错误，并使用内置的 HTML 窗体帮助程序在视图中自动标记或突出显示受影响的字段。</span><span class="sxs-lookup"><span data-stu-id="b8efb-274">MVC 3 now retrieves errors from the `IValidatableObject` interface when model binding, and automatically flags or highlights affected fields within a view using the built-in HTML form helpers.</span></span>

<span data-ttu-id="b8efb-275">[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)接口允许 ASP.NET MVC 在运行时发现验证程序是否支持客户端验证。</span><span class="sxs-lookup"><span data-stu-id="b8efb-275">The [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) interface enables ASP.NET MVC to discover at run time whether a validator has support for client validation.</span></span> <span data-ttu-id="b8efb-276">此接口已经过设计，以便可以与各种验证框架集成。</span><span class="sxs-lookup"><span data-stu-id="b8efb-276">This interface has been designed so that it can be integrated with a variety of validation frameworks.</span></span>

<span data-ttu-id="b8efb-277">有关验证接口的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览版博客文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)中的 "**模型验证改进**" 一节。</span><span class="sxs-lookup"><span data-stu-id="b8efb-277">For more information about validation interfaces, see the **Model Validation Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span> <span data-ttu-id="b8efb-278">（但请注意，博客中的 "IValidateObject" 引用应为 "IValidatableObject"。）</span><span class="sxs-lookup"><span data-stu-id="b8efb-278">(However, note that the reference to "IValidateObject" in the blog should be "IValidatableObject".)</span></span>

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a><span data-ttu-id="b8efb-279">依赖关系注入改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-279">Dependency Injection Improvements</span></span>

<span data-ttu-id="b8efb-280">ASP.NET MVC 3 为应用依赖关系注入（DI）以及与依赖关系注入或控制反转（IOC）容器的集成提供了更好的支持。</span><span class="sxs-lookup"><span data-stu-id="b8efb-280">ASP.NET MVC 3 provides better support for applying Dependency Injection (DI) and for integrating with Dependency Injection or Inversion of Control (IOC) containers.</span></span> <span data-ttu-id="b8efb-281">已在以下区域添加对 DI 的支持：</span><span class="sxs-lookup"><span data-stu-id="b8efb-281">Support for DI has been added in the following areas:</span></span>

- <span data-ttu-id="b8efb-282">控制器（注册和注入控制器工厂，注入控制器）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-282">Controllers (registering and injecting controller factories, injecting controllers).</span></span>
- <span data-ttu-id="b8efb-283">视图（注册和注入视图引擎，将依赖项注入到查看页中）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-283">Views (registering and injecting view engines, injecting dependencies into view pages).</span></span>
- <span data-ttu-id="b8efb-284">操作筛选器（查找和注入筛选器）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-284">Action filters (locating and injecting filters).</span></span>
- <span data-ttu-id="b8efb-285">模型联编（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-285">Model binders (registering and injecting).</span></span>
- <span data-ttu-id="b8efb-286">模型验证提供程序（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-286">Model validation providers (registering and injecting).</span></span>
- <span data-ttu-id="b8efb-287">模型元数据提供程序（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-287">Model metadata providers (registering and injecting).</span></span>
- <span data-ttu-id="b8efb-288">值提供程序（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-288">Value providers (registering and injecting).</span></span>

<span data-ttu-id="b8efb-289">MVC 3 支持[公共服务定位器](https://github.com/unitycontainer/commonservicelocator)库和支持该库的 `IServiceLocator` 接口的任何 DI 容器。</span><span class="sxs-lookup"><span data-stu-id="b8efb-289">MVC 3 supports the [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) library and any DI container that supports that library's `IServiceLocator` interface.</span></span> <span data-ttu-id="b8efb-290">它还支持新的 `IDependencyResolver` 接口，使其更易于集成 DI 框架。</span><span class="sxs-lookup"><span data-stu-id="b8efb-290">It also supports a new `IDependencyResolver` interface that makes it easier to integrate DI frameworks.</span></span>

<span data-ttu-id="b8efb-291">有关 MVC 3 中的 DI 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b8efb-291">For more information about DI in MVC 3, see the following resources:</span></span>

- [<span data-ttu-id="b8efb-292">有关服务位置的 Brad Wilson 系列博客文章</span><span class="sxs-lookup"><span data-stu-id="b8efb-292">Brad Wilson's series of blog posts on Service Location</span></span>](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [<span data-ttu-id="b8efb-293">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="b8efb-293">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a><span data-ttu-id="b8efb-294">其他新功能</span><span class="sxs-lookup"><span data-stu-id="b8efb-294">Other New Features</span></span>

### <a name="nuget-integration"></a><span data-ttu-id="b8efb-295">NuGet 集成</span><span class="sxs-lookup"><span data-stu-id="b8efb-295">NuGet Integration</span></span>

<span data-ttu-id="b8efb-296">ASP.NET MVC 3 在其安装过程中自动安装并启用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="b8efb-296">ASP.NET MVC 3 automatically installs and enables NuGet as part of its setup.</span></span> <span data-ttu-id="b8efb-297">NuGet 是一个免费的开源程序包管理器，可让你轻松地在项目中查找、安装和使用 .NET 库和工具。</span><span class="sxs-lookup"><span data-stu-id="b8efb-297">NuGet is a free open-source package manager that makes it easy to find, install, and use .NET libraries and tools in your projects.</span></span> <span data-ttu-id="b8efb-298">它适用于所有 Visual Studio 项目类型（包括 ASP.NET Web 窗体和 ASP.NET MVC）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-298">It works with all Visual Studio project types (including ASP.NET Web Forms and ASP.NET MVC).</span></span>

<span data-ttu-id="b8efb-299">NuGet 允许维护开源项目的开发人员（例如，Moq、NHibernate、Ninject、StructureMap、NUnit、Windsor、RhinoMocks 和 Elmah 等项目）将其库打包并注册到联机库。</span><span class="sxs-lookup"><span data-stu-id="b8efb-299">NuGet enables developers who maintain open source projects (for example, projects like Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, and Elmah) to package their libraries and register them in an online gallery.</span></span> <span data-ttu-id="b8efb-300">如果 .NET 开发人员想要使用这些库之一来查找包并将其安装在其所使用的项目中，则可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="b8efb-300">It is then easy for .NET developers who want to use one of these libraries to find the package and install it in projects they are working on.</span></span>

<span data-ttu-id="b8efb-301">通过 ASP.NET 3 工具更新，项目模板包括 JavaScript 库预安装的 NuGet 包，因此可以通过 NuGet 更新它们。</span><span class="sxs-lookup"><span data-stu-id="b8efb-301">With the ASP.NET 3 Tools Update, project templates include JavaScript libraries pre-installed NuGet packages, so they are updatable via NuGet.</span></span> <span data-ttu-id="b8efb-302">还会将实体框架 Code First 预安装为 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b8efb-302">Entity Framework Code First is also pre-installed as a NuGet package.</span></span>

<span data-ttu-id="b8efb-303">有关 NuGet 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-303">For more information about NuGet, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a name="partial-page-output-caching"></a><span data-ttu-id="b8efb-304">部分页面输出缓存</span><span class="sxs-lookup"><span data-stu-id="b8efb-304">Partial-Page Output Caching</span></span>

<span data-ttu-id="b8efb-305">从版本1开始，ASP.NET MVC 支持完整页面响应的输出缓存。</span><span class="sxs-lookup"><span data-stu-id="b8efb-305">ASP.NET MVC has supported output caching of full page responses since version 1.</span></span> <span data-ttu-id="b8efb-306">MVC 3 还支持部分页面输出缓存，这使你可以轻松地缓存响应的区域或片段。</span><span class="sxs-lookup"><span data-stu-id="b8efb-306">MVC 3 also supports partial-page output caching, which allows you to easily cache regions or fragments of a response.</span></span> <span data-ttu-id="b8efb-307">有关缓存的详细信息，请参阅[Scott Guthrie 的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)的 "**部分页面输出缓存**" 部分，该部分介绍了 mvc 3 候选发布版和[Mvc 3 发行说明](../whitepapers/mvc3-release-notes.md)的**子操作输出缓存**部分。</span><span class="sxs-lookup"><span data-stu-id="b8efb-307">For more information about caching, see the **Partial Page Output Caching** section of [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) and the **Child Action Output Caching** section of the [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="granular-control-over-request-validation"></a><span data-ttu-id="b8efb-308">精细控制请求验证</span><span class="sxs-lookup"><span data-stu-id="b8efb-308">Granular Control over Request Validation</span></span>

<span data-ttu-id="b8efb-309">ASP.NET MVC 具有内置的请求验证，可自动帮助防范 XSS 和 HTML 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="b8efb-309">ASP.NET MVC has built-in request validation that automatically helps protect against XSS and HTML injection attacks.</span></span> <span data-ttu-id="b8efb-310">但是，有时你需要显式禁用请求验证，例如，如果你想让用户发布 HTML 内容（例如，在博客条目或 CMS 内容中）。</span><span class="sxs-lookup"><span data-stu-id="b8efb-310">However, sometimes you want to explicitly disable request validation, such as if you want to let users post HTML content (for example, in blog entries or CMS content).</span></span> <span data-ttu-id="b8efb-311">现在可以将[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性添加到模型或查看模型，以便在模型绑定期间对每个属性禁用请求验证。</span><span class="sxs-lookup"><span data-stu-id="b8efb-311">You can now add an [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) attribute to models or view models to disable request validation on a per-property basis during model binding.</span></span> <span data-ttu-id="b8efb-312">有关请求验证的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b8efb-312">For more information about request validation, see the following resources:</span></span>

- <span data-ttu-id="b8efb-313">[Scott Guthrie 的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中的 "不**引人注目的 JavaScript 和验证**" 部分。</span><span class="sxs-lookup"><span data-stu-id="b8efb-313">The **Unobtrusive JavaScript and Validation** section in [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).</span></span>
- [<span data-ttu-id="b8efb-314">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="b8efb-314">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a><span data-ttu-id="b8efb-315">可扩展的 "新建项目" 对话框</span><span class="sxs-lookup"><span data-stu-id="b8efb-315">Extensible "New Project" Dialog Box</span></span>

<span data-ttu-id="b8efb-316">在 ASP.NET MVC 3 中，你可以将项目模板、视图引擎和单元测试项目框架添加到 "**新建项目**" 对话框中。</span><span class="sxs-lookup"><span data-stu-id="b8efb-316">In ASP.NET MVC 3 you can add project templates, view engines, and unit test project frameworks to the **New Project** dialog box.</span></span>

### <a name="template-scaffolding-improvements"></a><span data-ttu-id="b8efb-317">模板基架改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-317">Template Scaffolding Improvements</span></span>

<span data-ttu-id="b8efb-318">ASP.NET MVC 3 基架模板会更好地标识模型上的主键属性，并对其进行适当处理，而不是在早期版本的 MVC 中处理它们。</span><span class="sxs-lookup"><span data-stu-id="b8efb-318">ASP.NET MVC 3 scaffolding templates do a better job of identifying primary-key properties on models and handling them appropriately than in earlier versions of MVC.</span></span> <span data-ttu-id="b8efb-319">（例如，基架模板现在可确保主密钥不会基架为可编辑的窗体字段。）</span><span class="sxs-lookup"><span data-stu-id="b8efb-319">(For example, the scaffolding templates now make sure that the primary key is not scaffolded as an editable form field.)</span></span>

<span data-ttu-id="b8efb-320">默认情况下，创建和编辑基架现在使用 `Html.EditorFor` 帮助程序，而不是 `Html.TextBoxFor` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="b8efb-320">By default, the Create and Edit scaffolds now use the `Html.EditorFor` helper instead of the `Html.TextBoxFor` helper.</span></span> <span data-ttu-id="b8efb-321">这会在 "**添加视图**" 对话框生成视图时以数据批注特性的形式改进对模型上的元数据的支持。</span><span class="sxs-lookup"><span data-stu-id="b8efb-321">This improves support for metadata on the model in the form of data annotation attributes when the **Add View** dialog box generates a view.</span></span>

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a><span data-ttu-id="b8efb-322">"Html.labelfor" 和 "LabelForModel" 的新重载</span><span class="sxs-lookup"><span data-stu-id="b8efb-322">New Overloads for "Html.LabelFor" and "Html.LabelForModel"</span></span>

<span data-ttu-id="b8efb-323">添加了新的方法重载，可用于 `LabelFor` 和 `LabelForModel` 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="b8efb-323">New method overloads have been added for the `LabelFor` and `LabelForModel` helper methods.</span></span> <span data-ttu-id="b8efb-324">新重载允许您指定或覆盖标签文本。</span><span class="sxs-lookup"><span data-stu-id="b8efb-324">The new overloads enable you to specify or override the label text.</span></span>

### <a name="sessionless-controller-support"></a><span data-ttu-id="b8efb-325">无会话控制器支持</span><span class="sxs-lookup"><span data-stu-id="b8efb-325">Sessionless Controller Support</span></span>

<span data-ttu-id="b8efb-326">在 ASP.NET MVC 3 中，你可以指示你是否希望控制器类使用会话状态，如果为，则指示会话状态应为 "读/写" 还是 "只读"。</span><span class="sxs-lookup"><span data-stu-id="b8efb-326">In ASP.NET MVC 3 you can indicate whether you want a controller class to use session state, and if so, whether session state should be read/write or read-only.</span></span> <span data-ttu-id="b8efb-327">有关无会话控制器支持的详细信息，请参阅[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="b8efb-327">For more information about sessionless controller support, see [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="new-additionalmetadataattribute-class"></a><span data-ttu-id="b8efb-328">新 "AdditionalMetadataAttribute" 类</span><span class="sxs-lookup"><span data-stu-id="b8efb-328">New "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="b8efb-329">您可以使用[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性来填充模型属性的 `ModelMetadata.AdditionalValues` 字典。</span><span class="sxs-lookup"><span data-stu-id="b8efb-329">You can use the [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) attribute to populate the `ModelMetadata.AdditionalValues` dictionary for a model property.</span></span> <span data-ttu-id="b8efb-330">例如，如果视图模型具有只应显示给管理员的属性，则可以批注该属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="b8efb-330">For example, if a view model has a property that should be displayed only to an administrator, you can annotate that property as shown in the following example:</span></span>

[!code-csharp[Main](mvc3/samples/sample4.cs)]

<span data-ttu-id="b8efb-331">呈现产品视图模型时，此元数据可用于任何显示或编辑模板。</span><span class="sxs-lookup"><span data-stu-id="b8efb-331">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="b8efb-332">你需要解释元数据信息。</span><span class="sxs-lookup"><span data-stu-id="b8efb-332">It is up to you to interpret the metadata information.</span></span>

### <a name="accountcontroller-improvements"></a><span data-ttu-id="b8efb-333">AccountController 改进</span><span class="sxs-lookup"><span data-stu-id="b8efb-333">AccountController improvements</span></span>

<span data-ttu-id="b8efb-334">Internet 项目模板中的 AccountController 已大幅提高。</span><span class="sxs-lookup"><span data-stu-id="b8efb-334">The AccountController in the Internet project template has been greatly improved.</span></span>

### <a name="new-intranet-project-template"></a><span data-ttu-id="b8efb-335">新的 Intranet 项目模板</span><span class="sxs-lookup"><span data-stu-id="b8efb-335">New Intranet Project Template</span></span>

<span data-ttu-id="b8efb-336">包含新的 Intranet 项目模板，该模板启用 Windows 身份验证并删除 AccountController。</span><span class="sxs-lookup"><span data-stu-id="b8efb-336">A new Intranet Project Template is included which enables Windows Authentication and removes the AccountController.</span></span>
