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
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="6e246-103">适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="6e246-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="6e246-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6e246-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6e246-105">本文档介绍 Visual Studio 2012 ASP.NET 和 Web 工具2013.1 的版本。</span><span class="sxs-lookup"><span data-stu-id="6e246-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="6e246-106">内容</span><span class="sxs-lookup"><span data-stu-id="6e246-106">Contents</span></span>

- [<span data-ttu-id="6e246-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="6e246-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="6e246-108">软件要求</span><span class="sxs-lookup"><span data-stu-id="6e246-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="6e246-109">Visual Studio 2012 ASP.NET 和 Web 工具2013.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="6e246-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="6e246-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="6e246-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="6e246-111">模板</span><span class="sxs-lookup"><span data-stu-id="6e246-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="6e246-112">ASP.NET MVC 5 模板</span><span class="sxs-lookup"><span data-stu-id="6e246-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="6e246-113">ASP.NET Web API 2 模板</span><span class="sxs-lookup"><span data-stu-id="6e246-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="6e246-114">项模板</span><span class="sxs-lookup"><span data-stu-id="6e246-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="6e246-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="6e246-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="6e246-116">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="6e246-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="6e246-117">Razor 编辑器</span><span class="sxs-lookup"><span data-stu-id="6e246-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="6e246-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="6e246-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="6e246-119">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="6e246-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="6e246-120">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="6e246-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="6e246-121">MVC 和 Web API 基架-HTTP 404，未找到错误</span><span class="sxs-lookup"><span data-stu-id="6e246-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="6e246-122">添加基架项后，Web 的 Visual Studio Express 2012 停止工作</span><span class="sxs-lookup"><span data-stu-id="6e246-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="6e246-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="6e246-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="6e246-124">使用 "浏览" 或按 F5 查看 cshtml 文件会导致服务器错误</span><span class="sxs-lookup"><span data-stu-id="6e246-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="6e246-125">Url 重写和颚化符（~）</span><span class="sxs-lookup"><span data-stu-id="6e246-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="6e246-126">模板</span><span class="sxs-lookup"><span data-stu-id="6e246-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="6e246-127">安装说明</span><span class="sxs-lookup"><span data-stu-id="6e246-127">Installation Notes</span></span>

<span data-ttu-id="6e246-128">[安装](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具2013.1。</span><span class="sxs-lookup"><span data-stu-id="6e246-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="6e246-129">软件要求</span><span class="sxs-lookup"><span data-stu-id="6e246-129">Software Requirements</span></span>

<span data-ttu-id="6e246-130">你必须具有 Visual Studio 2012 或适用于 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="6e246-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="6e246-131">Visual Studio 2012 ASP.NET 和 Web 工具2013.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="6e246-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="6e246-132">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="6e246-132">Bootstrap</span></span>

<span data-ttu-id="6e246-133">当基架 MVC 5 控制器和视图时，视图的标记将使用 "[启动](http://getbootstrap.com/)"。</span><span class="sxs-lookup"><span data-stu-id="6e246-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="6e246-134">模板</span><span class="sxs-lookup"><span data-stu-id="6e246-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="6e246-135">ASP.NET MVC 5 模板</span><span class="sxs-lookup"><span data-stu-id="6e246-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="6e246-136">我们添加了一个新的 MVC 5 模板。</span><span class="sxs-lookup"><span data-stu-id="6e246-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="6e246-137">它引用最新的 MVC 5 NuGet 包，你可以使用基架来添加控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="6e246-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="6e246-138">ASP.NET Web API 2 模板</span><span class="sxs-lookup"><span data-stu-id="6e246-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="6e246-139">我们添加了一个新的 Web API 2 模板。</span><span class="sxs-lookup"><span data-stu-id="6e246-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="6e246-140">它引用最新的 Web API 2 NuGet 包，你可以使用基架来添加控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="6e246-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="6e246-141">项模板</span><span class="sxs-lookup"><span data-stu-id="6e246-141">Item Templates</span></span>

<span data-ttu-id="6e246-142">我们为 MVC 5 视图、网页（Razor 3）和 Web API 2 控制器添加了新的项模板。</span><span class="sxs-lookup"><span data-stu-id="6e246-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="6e246-143">在添加新项时，它们会将相关 NuGet 包安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="6e246-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="6e246-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="6e246-144">Entity Framework 6</span></span>

<span data-ttu-id="6e246-145">使用实体框架基架 MVC 或 Web API 控制器时，将使用 Framework 6。</span><span class="sxs-lookup"><span data-stu-id="6e246-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="6e246-146">有关实体框架的详细信息，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="6e246-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="6e246-147">你还可以下载和安装适用于 Visual Studio 2012 的实体框架6工具。</span><span class="sxs-lookup"><span data-stu-id="6e246-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="6e246-148">请参阅[Get 实体框架](https://msdn.com/data/ee712906#tooling)。</span><span class="sxs-lookup"><span data-stu-id="6e246-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="6e246-149">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="6e246-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="6e246-150">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="6e246-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="6e246-151">这样，便可以轻松地将样板代码添加到项目中，以与数据模型交互。</span><span class="sxs-lookup"><span data-stu-id="6e246-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="6e246-152">在以前版本的 Visual Studio 中，基架限制为 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="6e246-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="6e246-153">使用此更新，现在可以将基架用于任何 ASP.NET 项目（包括 Web 窗体）。</span><span class="sxs-lookup"><span data-stu-id="6e246-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="6e246-154">此更新不支持为 Web 窗体项目生成页，但你仍然可以通过将 MVC 依赖项添加到项目中，将基架与 Web 窗体一起使用。</span><span class="sxs-lookup"><span data-stu-id="6e246-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="6e246-155">将来的更新中将添加对 Web 窗体的生成页的支持。</span><span class="sxs-lookup"><span data-stu-id="6e246-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="6e246-156">使用基架时，请确保在项目中安装所有必需的依赖项。</span><span class="sxs-lookup"><span data-stu-id="6e246-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="6e246-157">例如，如果从 ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用会自动添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="6e246-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="6e246-158">若要将 MVC 基架添加到 Web 窗体项目，请在对话框窗口中添加**新的基架项**，并选择 " **MVC 5 依赖**项"。</span><span class="sxs-lookup"><span data-stu-id="6e246-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="6e246-159">基架 MVC 有两个选项：最小和完整。</span><span class="sxs-lookup"><span data-stu-id="6e246-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="6e246-160">如果选择 "最小"，则只会将 NuGet 包和 ASP.NET MVC 的引用添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="6e246-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="6e246-161">如果选择 "完全" 选项，则会添加最小依赖项，以及 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="6e246-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="6e246-162">对基架的支持：异步控制器使用实体框架6中的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="6e246-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="6e246-163">有关详细信息和教程，请参阅[ASP.NET 基架概述](../2013/aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6e246-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="6e246-164">这些教程显示了 Visual Studio 2013 的基架，但也适用于 Visual Studio 2012 ASP.NET 和 Web 工具2013.1。</span><span class="sxs-lookup"><span data-stu-id="6e246-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="6e246-165">Razor 编辑器</span><span class="sxs-lookup"><span data-stu-id="6e246-165">Razor Editor</span></span>

<span data-ttu-id="6e246-166">通过此更新，Visual Studio 2012 现在支持 Razor 3 工具/编辑。</span><span class="sxs-lookup"><span data-stu-id="6e246-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="6e246-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="6e246-167">NuGet 2.7</span></span>

<span data-ttu-id="6e246-168">NuGet 2.7 包括一组丰富的新功能，这些功能在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中有详细说明。</span><span class="sxs-lookup"><span data-stu-id="6e246-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="6e246-169">此版本的 NuGet 不再需要用户显式允许 NuGet 还原缺少的包。</span><span class="sxs-lookup"><span data-stu-id="6e246-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="6e246-170">安装 NuGet 2.7 时，用户隐式同意自动还原缺少的包。</span><span class="sxs-lookup"><span data-stu-id="6e246-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="6e246-171">用户可以通过 Visual Studio 中的 NuGet 设置显式退出包还原。</span><span class="sxs-lookup"><span data-stu-id="6e246-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="6e246-172">此更改简化了包还原的工作方式。</span><span class="sxs-lookup"><span data-stu-id="6e246-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="6e246-173">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="6e246-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="6e246-174">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="6e246-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="6e246-175">MVC 和 Web API 基架-HTTP 404，未找到错误</span><span class="sxs-lookup"><span data-stu-id="6e246-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="6e246-176">如果将基架项添加到项目时遇到错误，你的项目可能会处于不一致的状态。</span><span class="sxs-lookup"><span data-stu-id="6e246-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="6e246-177">所做的某些更改将被回滚，但其他更改（如安装的 NuGet 包）将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="6e246-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="6e246-178">如果回滚路由配置更改，则在导航到基架项时，用户将收到 HTTP 404 错误。</span><span class="sxs-lookup"><span data-stu-id="6e246-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="6e246-179">若要为 MVC 修复此错误，请添加一个新的基架项，并选择 "MVC 5 依赖项（最小或全部）"。</span><span class="sxs-lookup"><span data-stu-id="6e246-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="6e246-180">此过程将向你的项目添加所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="6e246-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="6e246-181">为 Web API 修复此错误：</span><span class="sxs-lookup"><span data-stu-id="6e246-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="6e246-182">将以下 Webapiconfig.cs 类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="6e246-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="6e246-183">按如下所示在 Webapiconfig.cs 中的应用程序\_Start 方法中配置：</span><span class="sxs-lookup"><span data-stu-id="6e246-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="6e246-184">添加基架项后，Web 的 Visual Studio Express 2012 停止工作</span><span class="sxs-lookup"><span data-stu-id="6e246-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="6e246-185">如果在添加具有实体框架的基架项后 Visual Studio Express 2012 for Web 停止工作（例如使用实体框架的包含操作的 Web API 2 控制器），则 Visual Studio Express 未能加载程序集的本机映像依赖于 System.web。</span><span class="sxs-lookup"><span data-stu-id="6e246-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="6e246-186">若要更正此问题，请将 Visual Studio Express 配置为使用 System.web 的 MSIL 映像：</span><span class="sxs-lookup"><span data-stu-id="6e246-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="6e246-187">在管理员模式下打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="6e246-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="6e246-188">中转到%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE 或% ProgramFiles （x86）% \ Microsoft Visual Studio 11.0 \ Common7\IDE （适用于64位 Windows）。</span><span class="sxs-lookup"><span data-stu-id="6e246-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="6e246-189">在文本编辑器中打开 VWDExpress。</span><span class="sxs-lookup"><span data-stu-id="6e246-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="6e246-190">将以下行添加到 &lt;配置&gt;/&lt;运行时&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="6e246-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="6e246-191">重新启动 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="6e246-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="6e246-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="6e246-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="6e246-193">使用 "浏览" 或按 F5 查看 cshtml 文件会导致服务器错误</span><span class="sxs-lookup"><span data-stu-id="6e246-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="6e246-194">当你在 Visual Studio 2012 中创建 MVC 5 项目（或在 Visual Studio 2012 中打开，在 Visual Studio 2013 中创建的 MVC 5 项目），并尝试通过使用 "通过浏览" 或按 F5 来查看 cshtml 文件时，你将收到一个错误，指出 **"/" 应用程序中出现服务器错误**。</span><span class="sxs-lookup"><span data-stu-id="6e246-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="6e246-195">服务器尝试导航到 `http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="6e246-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="6e246-196">若要解决此问题，请将项目中的 "**启动操作**" 设置更改为 "**特定页面**"。</span><span class="sxs-lookup"><span data-stu-id="6e246-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="6e246-197">不需要为页面提供值。</span><span class="sxs-lookup"><span data-stu-id="6e246-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="6e246-198">做出此更改后，选择 "F5" 可导航到应用程序的根目录（`http://localhost:XXXX`）。</span><span class="sxs-lookup"><span data-stu-id="6e246-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="6e246-199">此行为与 Visual Studio 2013 中的 MVC 5 项目的行为不同，其中，**当前页面**设置将启动打开的页面。</span><span class="sxs-lookup"><span data-stu-id="6e246-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="6e246-200">Url 重写和颚化符（~）</span><span class="sxs-lookup"><span data-stu-id="6e246-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="6e246-201">升级到 ASP.NET Razor 3 或 ASP.NET MVC 5 之后，如果使用 URL 重写，则波形符（~）表示法可能无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="6e246-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="6e246-202">URL 重写会影响 HTML 元素中的波形符（~）表示法（例如 &lt;A/&gt;、&lt;SCRIPT/&gt;、&lt;LINK/&gt;），因此波形符不再映射到根目录。</span><span class="sxs-lookup"><span data-stu-id="6e246-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="6e246-203">例如，如果将**asp.net/content**的请求重写为**asp.net**，则 &lt;href = "~/content/"/&gt; 中的 href 属性将解析为 **/content/content/** ，而不是 **/** 。</span><span class="sxs-lookup"><span data-stu-id="6e246-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="6e246-204">若要取消此更改，你可以在每个网页或 BeginRequest 中的**应用程序\_** 中将**IIS\_WasUrlRewritten**上下文设置为 false。</span><span class="sxs-lookup"><span data-stu-id="6e246-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="6e246-205">模板</span><span class="sxs-lookup"><span data-stu-id="6e246-205">Templates</span></span>

<span data-ttu-id="6e246-206">当使用 Windows 8.1 或 Windows Server 2012 R2 上的 Visual Studio 2012 创建 ASP.NET MVC 项目时，Visual Studio 将显示一条错误消息，指出 "为 ASP.NET 4.5 配置 Web [url] 失败"。</span><span class="sxs-lookup"><span data-stu-id="6e246-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![配置错误](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="6e246-208">你会看到此错误，因为当 Visual Studio 2012 安装在这些版本的 Windows 上时，Visual Studio 不会启用 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="6e246-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="6e246-209">若要启用 ASP.NET 4.5，请执行 "[打开或关闭 Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)" 中所述的步骤。</span><span class="sxs-lookup"><span data-stu-id="6e246-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![打开或关闭 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="6e246-211">或者，你可以通过命令行启用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="6e246-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="6e246-212">在管理员模式下打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="6e246-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="6e246-213">运行以下命令以启用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="6e246-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
