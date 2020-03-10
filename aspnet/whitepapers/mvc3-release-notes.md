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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78501038"
---
# <a name="aspnet-mvc-3"></a><span data-ttu-id="8fdf5-102">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="8fdf5-102">ASP.NET MVC 3</span></span>

- [<span data-ttu-id="8fdf5-103">概述</span><span class="sxs-lookup"><span data-stu-id="8fdf5-103">Overview</span></span>](#overview)
- [<span data-ttu-id="8fdf5-104">安装说明</span><span class="sxs-lookup"><span data-stu-id="8fdf5-104">Installation Notes</span></span>](#installation-notes)
- [<span data-ttu-id="8fdf5-105">软件要求</span><span class="sxs-lookup"><span data-stu-id="8fdf5-105">Software Requirements</span></span>](#software-requirements)
- [<span data-ttu-id="8fdf5-106">文档</span><span class="sxs-lookup"><span data-stu-id="8fdf5-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="8fdf5-107">支持</span><span class="sxs-lookup"><span data-stu-id="8fdf5-107">Support</span></span>](#support)
- [<span data-ttu-id="8fdf5-108">将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="8fdf5-108">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>](#upgrading)
- [<span data-ttu-id="8fdf5-109">ASP.NET MVC 3 工具更新（2011年4月12日）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-109">ASP.NET MVC 3 Tools Update (April 12, 2011)</span></span>](#tu-changes)

    - [<span data-ttu-id="8fdf5-110">"添加控制器" 对话框现在可以使用视图和数据访问代码基架控制器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-110">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>](#tu-AddControllerDialog)
    - [<span data-ttu-id="8fdf5-111">"ASP.NET MVC 3 新建项目" 对话框的改进</span><span class="sxs-lookup"><span data-stu-id="8fdf5-111">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>](#tu-ImprovementsNewDialogBox)
    - [<span data-ttu-id="8fdf5-112">项目模板现在包括 Modernizr 1。7</span><span class="sxs-lookup"><span data-stu-id="8fdf5-112">Project templates now include Modernizr 1.7</span></span>](#tu-Modernizr)
    - [<span data-ttu-id="8fdf5-113">项目模板包括 jQuery、jQuery UI 和 jQuery 验证的更新版本</span><span class="sxs-lookup"><span data-stu-id="8fdf5-113">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>](#tu-UpdatedJQuery)
    - [<span data-ttu-id="8fdf5-114">项目模板现在包括 ADO.NET 实体框架4.1 作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8fdf5-114">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>](#tu-EF)
    - [<span data-ttu-id="8fdf5-115">项目模板包括 JavaScript 库作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8fdf5-115">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>](#tu-JavaScriptLibsNuget)
    - [<span data-ttu-id="8fdf5-116">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-116">Known Issues</span></span>](#tu-KI)
- [<span data-ttu-id="8fdf5-117">ASP.NET MVC 3 RTM （2011年1月13日）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-117">ASP.NET MVC 3 RTM (January 13, 2011)</span></span>](#MVC3RTM)

    - [<span data-ttu-id="8fdf5-118">Change：已将 jQuery UI 版本更新为1.8。7</span><span class="sxs-lookup"><span data-stu-id="8fdf5-118">Change: Updated the version of jQuery UI to 1.8.7</span></span>](#RTM-1)
    - [<span data-ttu-id="8fdf5-119">更改：将默认 ModelMetadataProvider 更改回 DataAnnotationsModelMetadataProvider</span><span class="sxs-lookup"><span data-stu-id="8fdf5-119">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>](#RTM-2)
    - [<span data-ttu-id="8fdf5-120">已修复：粘贴包含空格的 Razor 表达式的一部分将导致其反向</span><span class="sxs-lookup"><span data-stu-id="8fdf5-120">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>](#RTM-3)
    - [<span data-ttu-id="8fdf5-121">已修复：重命名在编辑器中打开的 Razor 文件将禁用语法着色和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="8fdf5-121">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>](#RTM-4)
    - [<span data-ttu-id="8fdf5-122">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-122">Known Issues</span></span>](#RTM-KI)
    - [<span data-ttu-id="8fdf5-123">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-123">Breaking Changes</span></span>](#RTM-BC)
- [<span data-ttu-id="8fdf5-124">ASP.NET MVC 3 候选发布2（2010年12月10日）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-124">ASP.NET MVC 3 Release Candidate 2 (December 10, 2010)</span></span>](#_Toc2)

    - [<span data-ttu-id="8fdf5-125">项目模板已更改为包含 jQuery sqoop-user-guide-1.4.4、jQuery 验证1.7 和 jQuery UI 1.8.6 y UI 1.8。6</span><span class="sxs-lookup"><span data-stu-id="8fdf5-125">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6y UI 1.8.6</span></span>](#_Toc2_1)
    - [<span data-ttu-id="8fdf5-126">添加了 "AdditionalMetadataAttribute" 类</span><span class="sxs-lookup"><span data-stu-id="8fdf5-126">Added "AdditionalMetadataAttribute" Class</span></span>](#_Toc2_2)
    - [<span data-ttu-id="8fdf5-127">改进的视图基架</span><span class="sxs-lookup"><span data-stu-id="8fdf5-127">Improved View Scaffolding</span></span>](#_Toc2_3)
    - [<span data-ttu-id="8fdf5-128">添加了 Html Raw 方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-128">Added Html.Raw Method</span></span>](#_Toc2_3)
    - [<span data-ttu-id="8fdf5-129">重命名为 "ViewModel" 属性，并将 "View" 属性重命名为 "ViewBag"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-129">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>](#_Toc2_4)
    - [<span data-ttu-id="8fdf5-130">已将 "ControllerSessionStateAttribute" 类重命名为 "SessionStateAttribute"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-130">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>](#_Toc2_5)
    - [<span data-ttu-id="8fdf5-131">将 RemoteAttribute "Fields" 属性重命名为 "AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-131">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>](#_Toc2_6)
    - [<span data-ttu-id="8fdf5-132">已将 "SkipRequestValidationAttribute" 重命名为 "AllowHtmlAttribute"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-132">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>](#_Toc2_7)
    - [<span data-ttu-id="8fdf5-133">更改了 "ValidationMessage" 方法以显示第一个有用的错误消息</span><span class="sxs-lookup"><span data-stu-id="8fdf5-133">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>](#_Toc2_8)
    - [<span data-ttu-id="8fdf5-134">固定 @model 声明，不向文档中添加空白</span><span class="sxs-lookup"><span data-stu-id="8fdf5-134">Fixed @model Declaration to not Add Whitespace to the Document</span></span>](#_Toc2_9)
    - [<span data-ttu-id="8fdf5-135">添加了 "FileExtensions" 属性以查看引擎，以支持引擎特定的文件名</span><span class="sxs-lookup"><span data-stu-id="8fdf5-135">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>](#_Toc2_10)
    - [<span data-ttu-id="8fdf5-136">修复了 "Html.labelfor" 帮助程序，以便为 "For" 特性发出正确的值</span><span class="sxs-lookup"><span data-stu-id="8fdf5-136">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>](#_Toc2_11)
    - [<span data-ttu-id="8fdf5-137">修复了在模型绑定期间为显式值指定优先级的 "RenderAction" 方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-137">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>](#_Toc2_12)
    - [<span data-ttu-id="8fdf5-138">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-138">Breaking Changes</span></span>](#_Toc2_BC)
    - [<span data-ttu-id="8fdf5-139">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-139">Known Issues</span></span>](#_Toc2_KI)
- [<span data-ttu-id="8fdf5-140">ASP.NET MVC 3 候选发布（2010年11月9日）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-140">ASP.NET MVC 3 Release Candidate (Nov 9, 2010)</span></span>](#TOC_ASP_NET_3_RC)

    - [<span data-ttu-id="8fdf5-141">ASP.NET MVC 3 RC 中的新功能</span><span class="sxs-lookup"><span data-stu-id="8fdf5-141">New Features in ASP.NET MVC 3 RC</span></span>](#_Toc276711785)
    - [<span data-ttu-id="8fdf5-142">NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-142">NuGet Package Manager</span></span>](#_Toc276711786)
    - [<span data-ttu-id="8fdf5-143">改进了 "新建项目" 对话框</span><span class="sxs-lookup"><span data-stu-id="8fdf5-143">Improved "New Project" Dialog Box</span></span>](#_Toc276711787)
    - [<span data-ttu-id="8fdf5-144">无会话控制器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-144">Sessionless Controllers</span></span>](#_Toc276711788)
    - [<span data-ttu-id="8fdf5-145">新验证属性</span><span class="sxs-lookup"><span data-stu-id="8fdf5-145">New Validation Attributes</span></span>](#_Toc276711789)
    - [<span data-ttu-id="8fdf5-146">"Html.labelfor" 和 "LabelForModel" 方法的新重载</span><span class="sxs-lookup"><span data-stu-id="8fdf5-146">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>](#_Toc276711790)
    - [<span data-ttu-id="8fdf5-147">子操作输出缓存</span><span class="sxs-lookup"><span data-stu-id="8fdf5-147">Child Action Output Caching</span></span>](#_Toc276711791)
    - [<span data-ttu-id="8fdf5-148">"添加视图" 对话框改进</span><span class="sxs-lookup"><span data-stu-id="8fdf5-148">"Add View" Dialog Box Improvements</span></span>](#_Toc276711792)
    - [<span data-ttu-id="8fdf5-149">精细请求验证</span><span class="sxs-lookup"><span data-stu-id="8fdf5-149">Granular Request Validation</span></span>](#_Toc276711793)
    - [<span data-ttu-id="8fdf5-150">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-150">Breaking Changes</span></span>](#_Toc276711794)
    - [<span data-ttu-id="8fdf5-151">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-151">Known Issues</span></span>](#_Toc276711795)
- [<span data-ttu-id="8fdf5-152">ASP.NET.MVC 3 Beta 说明（Oct 6，2010）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-152">ASP.MVC 3 Beta Notes (Oct 6, 2010)</span></span>](#TOC_ASP_NET_3_Beta)

    - [<span data-ttu-id="8fdf5-153">ASP.NET MVC 3 Beta 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="8fdf5-153">New Features in ASP.NET MVC 3 Beta</span></span>](#0.1__Toc274034215)
    - [<span data-ttu-id="8fdf5-154">NuPack 包管理器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-154">NuPack Package Manager</span></span>](#0.1__Toc274034216)
    - [<span data-ttu-id="8fdf5-155">改进了 "新建项目" 对话框</span><span class="sxs-lookup"><span data-stu-id="8fdf5-155">Improved New Project Dialog Box</span></span>](#0.1__Toc274034217)
    - [<span data-ttu-id="8fdf5-156">在 Razor 视图中指定强类型模型的简化方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-156">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>](#0.1__Toc274034218)
    - [<span data-ttu-id="8fdf5-157">支持新的 ASP.NET 网页帮助器方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-157">Support for New ASP.NET Web Pages Helper Methods</span></span>](#0.1__Toc274034219)
    - [<span data-ttu-id="8fdf5-158">其他依赖关系注入支持</span><span class="sxs-lookup"><span data-stu-id="8fdf5-158">Additional Dependency Injection Support</span></span>](#0.1__Toc274034220)
    - [<span data-ttu-id="8fdf5-159">新支持基于 jQuery 的非引人注目 Ajax</span><span class="sxs-lookup"><span data-stu-id="8fdf5-159">New Support for Unobtrusive jQuery-Based Ajax</span></span>](#0.1__Toc274034221)
    - [<span data-ttu-id="8fdf5-160">新支持非引人注目的 jQuery 验证</span><span class="sxs-lookup"><span data-stu-id="8fdf5-160">New Support for Unobtrusive jQuery Validation</span></span>](#0.1__Toc274034222)
    - [<span data-ttu-id="8fdf5-161">适用于客户端验证和非引人注目 JavaScript 的新应用程序范围标志</span><span class="sxs-lookup"><span data-stu-id="8fdf5-161">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>](#0.1__Toc274034223)
    - [<span data-ttu-id="8fdf5-162">新支持在视图运行之前运行的代码</span><span class="sxs-lookup"><span data-stu-id="8fdf5-162">New Support for Code that Runs Before Views Run</span></span>](#0.1__Toc274034224)
    - [<span data-ttu-id="8fdf5-163">新的对 VBHTML Razor 语法的支持</span><span class="sxs-lookup"><span data-stu-id="8fdf5-163">New Support for the VBHTML Razor Syntax</span></span>](#0.1__Toc274034225)
    - [<span data-ttu-id="8fdf5-164">更精细地控制 ValidateInputAttribute</span><span class="sxs-lookup"><span data-stu-id="8fdf5-164">More Granular Control over ValidateInputAttribute</span></span>](#0.1__Toc274034226)
    - [<span data-ttu-id="8fdf5-165">帮助器将下划线转换为使用匿名对象指定的 HTML 属性名称的连字符</span><span class="sxs-lookup"><span data-stu-id="8fdf5-165">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>](#0.1__Toc274034227)
    - [<span data-ttu-id="8fdf5-166">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="8fdf5-166">Bug Fixes</span></span>](#0.1__Toc274034228)
    - [<span data-ttu-id="8fdf5-167">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-167">Breaking Changes</span></span>](#0.1__Toc274034229)
    - [<span data-ttu-id="8fdf5-168">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-168">Known Issues</span></span>](#0.1__Toc274034230)
- [<span data-ttu-id="8fdf5-169">否认</span><span class="sxs-lookup"><span data-stu-id="8fdf5-169">Disclaimer</span></span>](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a><span data-ttu-id="8fdf5-170">概述</span><span class="sxs-lookup"><span data-stu-id="8fdf5-170">Overview</span></span>

<span data-ttu-id="8fdf5-171">本文档介绍适用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-171">This document describes the release of ASP.NET MVC 3 RTM for Visual Studio 2010.</span></span> <span data-ttu-id="8fdf5-172">ASP.NET MVC 是一个框架，用于开发使用模型-视图-控制器（MVC）模式的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-172">ASP.NET MVC is a framework for developing Web applications that uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="8fdf5-173">ASP.NET MVC 3 安装程序包含以下组件：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-173">The ASP.NET MVC 3 installer includes the following components:</span></span>

- <span data-ttu-id="8fdf5-174">ASP.NET MVC 3 运行时组件</span><span class="sxs-lookup"><span data-stu-id="8fdf5-174">ASP.NET MVC 3 runtime components</span></span>
- <span data-ttu-id="8fdf5-175">ASP.NET MVC 3 Visual Studio 2010 工具</span><span class="sxs-lookup"><span data-stu-id="8fdf5-175">ASP.NET MVC 3 Visual Studio 2010 tools</span></span>
- <span data-ttu-id="8fdf5-176">ASP.NET 网页运行时组件</span><span class="sxs-lookup"><span data-stu-id="8fdf5-176">ASP.NET Web Pages run-time components</span></span>
- <span data-ttu-id="8fdf5-177">ASP.NET 网页 Visual Studio 2010 工具</span><span class="sxs-lookup"><span data-stu-id="8fdf5-177">ASP.NET Web Pages Visual Studio 2010 tools</span></span>
- <span data-ttu-id="8fdf5-178">适用于 .NET 的 Microsoft 程序包管理器（NuGet）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-178">Microsoft Package Manager for .NET (NuGet)</span></span>
- <span data-ttu-id="8fdf5-179">支持 Razor 语法的 Visual Studio 2010 更新。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-179">An update for Visual Studio 2010 that enables support for Razor syntax.</span></span> <span data-ttu-id="8fdf5-180">（有关详细信息，请参阅知识库文章2483190。）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-180">(For details, see KnowledgeBase article 2483190.)</span></span>

<span data-ttu-id="8fdf5-181">可在位于 URL 的 ASP.NET 网站上找到 ASP.NET MVC 3 的每个预发行版本的全套发行说明：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-181">The full set of release notes for each pre-release version of ASP.NET MVC 3 can be found on the ASP.NET website at the following URL:</span></span>

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a><span data-ttu-id="8fdf5-182">安装说明</span><span class="sxs-lookup"><span data-stu-id="8fdf5-182">Installation Notes</span></span>

<span data-ttu-id="8fdf5-183">若要使用 Web 平台安装程序（Web PI）安装 ASP.NET MVC 3 RTM，请访问以下页面：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-183">To install ASP.NET MVC 3 RTM using the Web Platform Installer (Web PI), visit the following page:</span></span>

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

<span data-ttu-id="8fdf5-184">或者，可以从以下页面下载适用于 Visual Studio 2010 的 ASP.NET MVC 3 RTM 安装程序：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-184">Alternatively, you can download the installer for ASP.NET MVC 3 RTM for Visual Studio 2010 from the following page:</span></span>

https://go.microsoft.com/fwlink/?LinkID=208140

<span data-ttu-id="8fdf5-185">可以安装 ASP.NET MVC 3，并且可以与 ASP.NET MVC 2 并行运行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-185">ASP.NET MVC 3 can be installed and can run side-by-side with ASP.NET MVC 2.</span></span>

<a id="software-requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="8fdf5-186">软件要求</span><span class="sxs-lookup"><span data-stu-id="8fdf5-186">Software Requirements</span></span>

<span data-ttu-id="8fdf5-187">ASP.NET MVC 3 运行时组件需要以下软件：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-187">The ASP.NET MVC 3 run-time components require the following software:</span></span>

- <span data-ttu-id="8fdf5-188">.NET Framework 版本4。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-188">.NET Framework version 4.</span></span> 

    <span data-ttu-id="8fdf5-189">ASP.NET MVC 3 Visual Studio 2010 工具需要以下软件：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-189">ASP.NET MVC 3 Visual Studio 2010 tools require the following software:</span></span>
- <span data-ttu-id="8fdf5-190">Visual Studio 2010 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-190">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="8fdf5-191">文档</span><span class="sxs-lookup"><span data-stu-id="8fdf5-191">Documentation</span></span>

<span data-ttu-id="8fdf5-192">以下 URL 的 MSDN 网站上提供了有关 ASP.NET MVC 的文档：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-192">Documentation for ASP.NET MVC is available on the MSDN Web site at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

<span data-ttu-id="8fdf5-193">有关 ASP.NET MVC 的教程和其他信息可在 ASP.NET 网站的 MVC 页上找到，网址为：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-193">Tutorials and other information about ASP.NET MVC are available on the MVC page of the ASP.NET Web site at the following URL:</span></span>

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a><span data-ttu-id="8fdf5-194">支持</span><span class="sxs-lookup"><span data-stu-id="8fdf5-194">Support</span></span>

<span data-ttu-id="8fdf5-195">这是完全受支持的版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-195">This is a fully supported release.</span></span> <span data-ttu-id="8fdf5-196">有关获取技术支持的信息可在[Microsoft 支持部门网站](https://support.microsoft.com/)上找到。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-196">Information about getting technical support can be found at the [Microsoft Support website](https://support.microsoft.com/).</span></span>

<span data-ttu-id="8fdf5-197">欢迎将与此版本有关的问题发布到 ASP.NET MVC 论坛中，ASP.NET 社区的成员经常能够在该论坛中提供非正式的支持：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-197">Also feel free to post questions about this release to the ASP.NET MVC forum, where members of the ASP.NET community are frequently able to provide informal support:</span></span>

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a><span data-ttu-id="8fdf5-198">将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="8fdf5-198">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="8fdf5-199">可以在同一台计算机上并行安装 ASP.NET MVC 3 与 ASP.NET MVC 2，这使你可以灵活选择何时将 ASP.NET MVC 2 应用程序升级到 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-199">ASP.NET MVC 3 can be installed side by side with ASP.NET MVC 2 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 2 application to ASP.NET MVC 3.</span></span>

<span data-ttu-id="8fdf5-200">若要手动将现有 ASP.NET MVC 2 应用程序升级到版本3，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-200">To manually upgrade an existing ASP.NET MVC 2 application to version 3, do the following:</span></span>

1. <span data-ttu-id="8fdf5-201">在您的计算机上创建新的空 ASP.NET MVC 3 项目。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-201">Create a new empty ASP.NET MVC 3 project on your computer.</span></span> <span data-ttu-id="8fdf5-202">此项目将包含升级所需的一些文件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-202">This project will contain some files that are required for the upgrade.</span></span>
2. <span data-ttu-id="8fdf5-203">将以下文件从 ASP.NET MVC 3 项目复制到您的 ASP.NET MVC 2 项目的相应位置中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-203">Copy the following files from the ASP.NET MVC 3 project into the corresponding location of your ASP.NET MVC 2 project.</span></span> <span data-ttu-id="8fdf5-204">您将需要更新对 jQuery 库的所有引用以说明新的文件名 (jQuery-1.5.1.js)：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-204">You'll need to update any references to the jQuery library to account for the new filename ( jQuery-1.5.1.js):</span></span> 

    - <span data-ttu-id="8fdf5-205">/Views/Web.config</span><span class="sxs-lookup"><span data-stu-id="8fdf5-205">/Views/Web.config</span></span>
    - <span data-ttu-id="8fdf5-206">/packages.config</span><span class="sxs-lookup"><span data-stu-id="8fdf5-206">/packages.config</span></span>
    - <span data-ttu-id="8fdf5-207">/scripts/\*.js</span><span class="sxs-lookup"><span data-stu-id="8fdf5-207">/scripts/\*.js</span></span>
    - <span data-ttu-id="8fdf5-208">/Content/themes/\*。\*</span><span class="sxs-lookup"><span data-stu-id="8fdf5-208">/Content/themes/\*.\*</span></span>
3. <span data-ttu-id="8fdf5-209">将空 ASP.NET MVC 3 项目解决方案的根目录中的 "*包*" 文件夹复制到解决方案的根目录中，该目录位于解决方案的 .sln 文件所在的目录中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-209">Copy the *packages* folder in the root of the empty ASP.NET MVC 3 project solution into the root of your solution, which is in the directory where the solution's .sln file is located.</span></span>
4. <span data-ttu-id="8fdf5-210">如果 ASP.NET MVC 2 项目包含任何区域，请将/Views/Web.config 文件复制到每个区域的*Views*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-210">If your ASP.NET MVC 2 project contains any areas, copy the /Views/Web.config file to the *Views* folder of each area.</span></span>
5. <span data-ttu-id="8fdf5-211">在 ASP.NET MVC 2 项目中的两个 web.config 文件中，全局搜索并替换 ASP.NET MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-211">In both Web.config files in the ASP.NET MVC 2 project, globally search and replace the ASP.NET MVC version.</span></span> <span data-ttu-id="8fdf5-212">查找以下内容：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-212">Find the following:</span></span> 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="8fdf5-213">将其替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-213">Replace it with the following:</span></span>

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. <span data-ttu-id="8fdf5-214">在解决方案资源管理器中，删除对*system.web* （指向版本2中的 DLL）的引用，然后*添加对3.0.0.0 的引用（v* ： v）。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-214">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the DLL from version 2), then add a reference to *System.Web.Mvc* (v3.0.0.0).</span></span>
7. <span data-ttu-id="8fdf5-215">添加对 System.web. .dll 和 System.web... e。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-215">Add a reference to System.Web.WebPages.dll and System.Web.Helpers.dll.</span></span> <span data-ttu-id="8fdf5-216">这些程序集位于以下文件夹中：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-216">These assemblies are located in the following folders:</span></span> 

    - <span data-ttu-id="8fdf5-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span><span class="sxs-lookup"><span data-stu-id="8fdf5-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span></span>
    - <span data-ttu-id="8fdf5-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span><span class="sxs-lookup"><span data-stu-id="8fdf5-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span></span>
8. <span data-ttu-id="8fdf5-219">在“解决方案资源管理器”中右击项目名称，然后选择“卸载项目”。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-219">In Solution Explorer, right-click the project name and select Unload Project.</span></span> <span data-ttu-id="8fdf5-220">然后再次右键单击项目名称，然后选择 *"编辑项目*名称 .csproj"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-220">Then right-click the project name again and select Edit *ProjectName*.csproj.</span></span>
9. <span data-ttu-id="8fdf5-221">找到*ProjectTypeGuids*元素，并将 {F85E285D-A4E0-4152-9332-AB1D724D3325} 替换为 {E53F8FEA-EAE0-44A6-8774-FFD645390401}。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-221">Locate the *ProjectTypeGuids* element and replace {F85E285D-A4E0-4152-9332-AB1D724D3325} with {E53F8FEA-EAE0-44A6-8774-FFD645390401}.</span></span>
10. <span data-ttu-id="8fdf5-222">保存更改，右击项目，然后选择“重新加载项目”。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-222">Save the changes, right-click the project, and then select Reload Project.</span></span>
11. <span data-ttu-id="8fdf5-223">在应用程序的根 web.config 文件中，将以下设置添加到*程序集*部分。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-223">In the application's root Web.config file, add the following settings to the *assemblies* section.</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. <span data-ttu-id="8fdf5-224">如果项目引用使用 ASP.NET MVC 2 编译的任何第三方库，请将以下突出显示的*bindingRedirect*元素添加到 web.config 文件中的 "*配置*" 部分下的应用程序根目录：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-224">If the project references any third-party libraries that are compiled using ASP.NET MVC 2, add the following highlighted *bindingRedirect* element to the Web.config file in the application root under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a><span data-ttu-id="8fdf5-225">ASP.NET MVC 3 工具更新中的更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-225">Changes in ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="8fdf5-226">本部分介绍自 ASP.NET MVC 3 RTM 版本以来在 ASP.NET MVC 3 工具更新版本中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-226">This section describes changes made in the ASP.NET MVC 3 Tools Update release since the ASP.NET MVC 3 RTM release.</span></span>

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a><span data-ttu-id="8fdf5-227">“添加控制器”对话框现在可以使用视图和数据访问代码创建控制器的基架</span><span class="sxs-lookup"><span data-stu-id="8fdf5-227">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>

<span data-ttu-id="8fdf5-228">创建基架是一种为应用程序快速生成控制器和视图的方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-228">Scaffolding is a way of quickly generating a controller and views for your application.</span></span> <span data-ttu-id="8fdf5-229">生成代码后，你可以对其进行编辑以满足项目的要求。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-229">After the code has been generated, you can edit it to meet your project's requirements.</span></span>

<span data-ttu-id="8fdf5-230">若要启动 ASP.NET MVC 3 中的 "*添加控制器*" 对话框，请在*解决方案资源管理器*中右键单击 "*控制器*" 文件夹，单击 "*添加*"，然后单击 "*控制器*"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-230">To launch the *Add Controller* dialog box in ASP.NET MVC 3, right-click the *Controllers* folder in *Solution Explorer*, click *Add*, and then click *Controller*.</span></span> <span data-ttu-id="8fdf5-231">该对话框已进行了增强，提供了其他创建基架选项。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-231">The dialog box has been enhanced to offer additional scaffolding options.</span></span>

![](mvc3-release-notes/_static/image1.png)

<span data-ttu-id="8fdf5-232">默认情况下提供了三个可用的创建基架模板。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-232">There are three scaffolding templates available by default.</span></span>

#### <a name="empty-controller"></a><span data-ttu-id="8fdf5-233">空控制器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-233">Empty Controller</span></span>

<span data-ttu-id="8fdf5-234">此模板将生成一个空的控制器文件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-234">This template generates an empty controller file.</span></span> <span data-ttu-id="8fdf5-235">此模板等效于不检查 ASP.NET MVC 的以前版本中*的 "创建"、"编辑"、"详细信息" 和 "删除" 方案的添加操作*。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-235">This template is equivalent to not checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="8fdf5-236">如果选中此选项，则没有进一步可用的选项。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-236">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-empty-readwrite-actions"></a><span data-ttu-id="8fdf5-237">包含空的读/写操作的控制器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-237">Controller with empty read/write actions</span></span>

<span data-ttu-id="8fdf5-238">此模板将生成一个控制器文件，其中包含所有必需的操作方法，但这些方法中没有实现代码。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-238">This template generates a controller file that has all the required action methods but no implementation code in the methods.</span></span> <span data-ttu-id="8fdf5-239">此模板等效于在以前版本的 ASP.NET MVC 中检查 "*创建"、"编辑"、"详细信息" 和 "删除" 方案的 "添加操作*"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-239">This template is equivalent to checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="8fdf5-240">如果选中此选项，则没有进一步可用的选项。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-240">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a><span data-ttu-id="8fdf5-241">包含读/写操作和视图的控制器（使用 Entity Framework）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-241">Controller with read/write actions and views, using Entity Framework</span></span>

<span data-ttu-id="8fdf5-242">此模板使您能够快速创建一个可用的数据输入用户界面。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-242">This template enables you to quickly create a working data-entry user interface.</span></span> <span data-ttu-id="8fdf5-243">它将生成可处理各种常见要求和方案的代码，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-243">It generates code that handles a range of common requirements and scenarios, such as the following:</span></span>

- <span data-ttu-id="8fdf5-244">*数据访问*。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-244">*Data access*.</span></span> <span data-ttu-id="8fdf5-245">生成的代码将读写数据库中的实体。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-245">The generated code reads and writes entities in a database.</span></span> <span data-ttu-id="8fdf5-246">如果选择现有的数据上下文类，或者允许模板生成新的*DbContext*类，则它适用于实体框架 Code First 方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-246">It works with the Entity Framework Code First approach if you choose an existing data context class or if you let the template generate a new *DbContext* class.</span></span> <span data-ttu-id="8fdf5-247">如果选择现有的*ObjectContext*类，还可以使用实体框架 Database First 或 Model First 方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-247">It also works with the Entity Framework Database First or Model First approach if you choose an existing *ObjectContext* class.</span></span>
- <span data-ttu-id="8fdf5-248">*验证*。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-248">*Validation*.</span></span> <span data-ttu-id="8fdf5-249">生成的代码将使用 ASP.NET MVC 模型绑定和元数据功能，以便根据在模型类上声明的规则来验证窗体提交。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-249">The generated code uses ASP.NET MVC model binding and metadata features so that form submissions are validated according to rules declared on your model class.</span></span> <span data-ttu-id="8fdf5-250">这包括内置的验证规则，如*Required*和*StringLength*特性以及自定义验证规则。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-250">This includes built-in validation rules, such as the *Required* and *StringLength* attributes, and custom validation rules.</span></span>
- <span data-ttu-id="8fdf5-251">一对多*关系*。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-251">*One-to-many relationships*.</span></span> <span data-ttu-id="8fdf5-252">如果您定义模型类之间的一对多外键关系，则生成的代码将生成用于选择相关实体的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-252">If you define one-to-many foreign-key relationships between your model classes, the generated code will produce drop-down lists for selecting related entities.</span></span> <span data-ttu-id="8fdf5-253">例如，您可能会定义下面的后跟“Entity Framework 代码优先”约定的模型类：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-253">For example, you might define the following model classes following Entity Framework Code First conventions:</span></span> 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    <span data-ttu-id="8fdf5-254">然后，当你为*product*类基架控制器时，其视图将允许用户为每个*产品*实例选择*类别*对象。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-254">When you then scaffold a controller for the *Product* class, its views will allow users to choose a *Category* object for each *Product* instance.</span></span>

    <span data-ttu-id="8fdf5-255">此模板在 "*添加控制器*" 对话框中启用其他选项。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-255">This template enables additional options in the *Add Controller* dialog box.</span></span> <span data-ttu-id="8fdf5-256">对于*模型类*，你可以在解决方案中选择任意模型类，确定用户将能够创建或编辑的数据类型：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-256">For *Model class*, you can choose any model class in your solution, which determines the type of data that users will be able to create or edit:</span></span>
- <span data-ttu-id="8fdf5-257">如果您想要使用“Entity Framework 代码优先”，则可选择任意模型类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-257">If you want to use Entity Framework Code First, you can choose any model class.</span></span>
- <span data-ttu-id="8fdf5-258">如果您使用的是“Entity Framework 数据库优先”或“Entity Framework 模型优先”，则一定要选择在您的概念模型中定义的实体类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-258">If you are using Entity Framework Database First or Entity Framework Model First, be sure to choose an entity class defined in your conceptual model.</span></span>

<span data-ttu-id="8fdf5-259">对于*数据上下文类*，可以进行以下选择：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-259">For *Data Context class*, you can make these choices:</span></span>

- <span data-ttu-id="8fdf5-260">如果要使用 Code First 并且没有现有的数据上下文类，请选择 "新建数据上下文" \* \*。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-260">If you want to use Code First and have no existing data context class, choose \*\*New data context \*\*.</span></span> <span data-ttu-id="8fdf5-261">然后，将为您生成一个数据上下文类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-261">A data context class will then be generated for you.</span></span>
- <span data-ttu-id="8fdf5-262">如果您想要使用“代码优先”，并且具有一个现有的数据上下文类，则在此处选择该类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-262">If you want to use Code First and have an existing data context class, choose it here.</span></span> <span data-ttu-id="8fdf5-263">将对它进行更新，以持久保存您已选择的模型类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-263">It will be updated to persist the model class you have selected.</span></span>
- <span data-ttu-id="8fdf5-264">如果您使用的是“数据库优先”或“模型优先”，则在此处选择您的对象上下文类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-264">If you are using Database First or Model First, choose your object context class here.</span></span>

<span data-ttu-id="8fdf5-265">对于“视图”，请选择您想要使用的视图引擎；或者，如果您不想创建任何视图基架，则选择“无”。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-265">For Views, choose the view engine you want to use, or choose None if you don't want to scaffold any views.</span></span>

<span data-ttu-id="8fdf5-266">你可以选择 "高级" 选择为生成的视图指定其他选项。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-266">You can select Advanced Optionsto specify further options for the generated views.</span></span> <span data-ttu-id="8fdf5-267">例如，您可选择要使用的布局或母版页。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-267">For example, you can choose the layout or master page to use.</span></span>

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a><span data-ttu-id="8fdf5-268">“ASP.NET MVC 3 新建项目”对话框的改进</span><span class="sxs-lookup"><span data-stu-id="8fdf5-268">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>

<span data-ttu-id="8fdf5-269">用于创建新的 ASP.NET MVC 3 项目的对话框包含多项改进，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-269">The dialog box you use to create new ASP.NET MVC 3 projects includes multiple improvements, as listed below.</span></span>

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a><span data-ttu-id="8fdf5-270">新的“Intranet 项目”模板</span><span class="sxs-lookup"><span data-stu-id="8fdf5-270">New "Intranet Project" Template</span></span>

<span data-ttu-id="8fdf5-271">“项目模板”列表包含一个新的“Intranet 应用程序”模板。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-271">The Project Template list includes a new Intranet Application template.</span></span> <span data-ttu-id="8fdf5-272">此模板包含用于使用 Windows 身份验证而不是 Forms 身份验证构建 Web 应用程序的设置。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-272">This template contains settings for building a web application using Windows authentication instead of forms authentication.</span></span> <span data-ttu-id="8fdf5-273">因为 intranet 应用程序需要某些无法在项目模板中封装的 IIS 设置，所以该模板包含一个自述文件，其中包含如何使项目模板在 IIS 中工作的说明。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-273">Because an intranet application requires some IIS settings that can't be encapsulated in a project template, the template includes a readme file with instructions for how to make the project template work in IIS.</span></span> <span data-ttu-id="8fdf5-274">以下 URL 的 MSDN 网站上提供了一个新的 Intranet 应用程序模板的文档：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-274">Documentation for the a new Intranet Application template is available on the MSDN website at the following URL:</span></span>

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a><span data-ttu-id="8fdf5-275">项目模板现在支持 HTML5</span><span class="sxs-lookup"><span data-stu-id="8fdf5-275">Project templates are now HTML5 enabled</span></span>

<span data-ttu-id="8fdf5-276">新项目对话框现在包含用于向项目模板中添加 HTML5 特定功能的选项。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-276">The new-project dialog box now contains an option to add HTML5-specific features to the project templates.</span></span> <span data-ttu-id="8fdf5-277">选择选项会导致生成包含新 HTML5 `<header>`、`<footer>`和 `<navigation>` 元素的视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-277">Selecting the option causes views to be generated that contain the new HTML5 `<header>`, `<footer>`, and `<navigation>` elements.</span></span>

<span data-ttu-id="8fdf5-278">请注意，浏览器的早期版本不支持 HTML5 特定的标记。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-278">Note that earlier versions of browsers do not support HTML5-specific tags.</span></span> <span data-ttu-id="8fdf5-279">为了解决此限制，HTML5 项目模板包含对 Modernizr 库的引用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-279">To address this limitation, the HTML5 project templates include a reference to the Modernizr library.</span></span> <span data-ttu-id="8fdf5-280">（请参见下一节。）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-280">(See the next section.)</span></span>

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a><span data-ttu-id="8fdf5-281">项目模板现在包含 Modernizr 1.7</span><span class="sxs-lookup"><span data-stu-id="8fdf5-281">Project templates now include Modernizr 1.7</span></span>

<span data-ttu-id="8fdf5-282">Modernizr 是一个 JavaScript 库，在尚不支持这些功能的浏览器中启用对 CSS 3 和 HTML5 的支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-282">Modernizr is a JavaScript library that enables support for CSS 3 and HTML5 in browsers that do not yet support these features.</span></span> <span data-ttu-id="8fdf5-283">此库作为预安装的 NuGet 包包含在 ASP.NET MVC 3 项目的模板中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-283">This library is included as a pre-installed NuGet package in templates for ASP.NET MVC 3 projects.</span></span> <span data-ttu-id="8fdf5-284">有关 Modernizr 的详细信息，请参阅[http://www.modernizr.com/](http://www.modernizr.com/)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-284">For more information about Modernizr, see [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a><span data-ttu-id="8fdf5-285">项目模板包含 jQuery、jQuery UI 和 jQuery Validation 的更新版本</span><span class="sxs-lookup"><span data-stu-id="8fdf5-285">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>

<span data-ttu-id="8fdf5-286">项目模板现在包含 jQuery 脚本的以下版本：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-286">The project templates now include the following versions of the jQuery scripts:</span></span>

- <span data-ttu-id="8fdf5-287">jQuery 1.5.1</span><span class="sxs-lookup"><span data-stu-id="8fdf5-287">jQuery 1.5.1</span></span>
- <span data-ttu-id="8fdf5-288">jQuery 验证 1.8</span><span class="sxs-lookup"><span data-stu-id="8fdf5-288">jQuery Validation 1.8</span></span>
- <span data-ttu-id="8fdf5-289">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="8fdf5-289">jQuery UI 1.8.11</span></span>

<span data-ttu-id="8fdf5-290">这些库是作为预安装的 NuGet 包进行包含的。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-290">These libraries are included as pre-installed NuGet packages.</span></span>

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a><span data-ttu-id="8fdf5-291">项目模板现在包含 ADO.NET Entity Framework 4.1 作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8fdf5-291">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>

<span data-ttu-id="8fdf5-292">ADO.NET 实体框架4.1 包括 Code First 功能。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-292">The ADO.NET Entity Framework 4.1 includes the Code First feature.</span></span> <span data-ttu-id="8fdf5-293">“代码优先”是 ADO.NET Entity Framework 的一种新的开发模式，可作为现有的“数据库优先”和“模型优先”模式的替代方案。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-293">Code First is a new development pattern for the ADO.NET Entity Framework that provides an alternative to the existing Database First and Model First patterns.</span></span>

<span data-ttu-id="8fdf5-294">“代码优先”侧重于使用通过 Visual Basic 或 C# 编写的 POCO 类（“纯旧 CLR 对象”）定义您的模型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-294">Code First is focused around defining your model using POCO classes ("plain old CLR objects") written in Visual Basic or C#.</span></span> <span data-ttu-id="8fdf5-295">然后，可将这些类映射到现有数据库，或者用于生成数据库架构。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-295">These classes can then be mapped to an existing database or be used to generate a database schema.</span></span> <span data-ttu-id="8fdf5-296">可以使用*DataAnnotations*属性或使用流畅 api 提供其他配置。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-296">Additional configuration can be supplied using *DataAnnotations* attributes or using fluent APIs.</span></span>

<span data-ttu-id="8fdf5-297">以下 Url 的 ASP.NET 网站上提供了有关使用 Code Firstwith ASP.NET MVC 的文档：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-297">Documentation for using Code Firstwith ASP.NET MVC is available on the ASP.NET website at the following URLs:</span></span>

<span data-ttu-id="8fdf5-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="8fdf5-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span></span>

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a><span data-ttu-id="8fdf5-299">项目模板包含 JavaScript 库作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8fdf5-299">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>

<span data-ttu-id="8fdf5-300">当你创建新的 ASP.NET MVC 3 项目时，该项目将包含前面提到的 JavaScript 文件（例如，Modernizr 库），方法是使用 NuGet 安装它们，而不是直接将脚本添加到项目模板中的 Scripts 文件夹目录.</span><span class="sxs-lookup"><span data-stu-id="8fdf5-300">When you create a new ASP.NET MVC 3 project, the project includes the JavaScript files mentioned previously (for example, the Modernizr library) by installing them using NuGet instead of directly adding the scripts to the Scripts folder in the project template contents.</span></span> <span data-ttu-id="8fdf5-301">这使您能够使用 NuGet，在发布脚本的新版本时将脚本更新为最新版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-301">This enables you to use NuGet to update the scripts to the latest version when new versions of the scripts are released.</span></span>

<span data-ttu-id="8fdf5-302">例如，考虑到经常发布新的 jQuery 版本，项目模板中包含的 jQuery 版本可能会在某个时候过期。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-302">For example, given the frequency of new jQuery releases, the version of jQuery included in the project template will at some point be out of date.</span></span> <span data-ttu-id="8fdf5-303">但是，由于 jQuery 是作为已安装的 NuGet 包进行包含的，因此，当有更新的 jQuery 版本可用时，在 NuGet 对话框中将会为您发出通知。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-303">However, because jQuery is included as an installed NuGet package, you will be notified in the NuGet dialog box when newer versions of jQuery are available.</span></span>

<span data-ttu-id="8fdf5-304">由于 jQuery 在文件名中包含版本号，因此，将 jQuery 更新为最新版本还需要更新引用 jQuery 文件的 `<script>` 标记，以使用新文件名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-304">Because jQuery includes the version number in the file name, updating jQuery to the latest version also requires updating the `<script>` tag that references the jQuery file to use the new file name.</span></span> <span data-ttu-id="8fdf5-305">其他包含的脚本库在脚本名中不包含版本号，因此，可以更轻松地将它们更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-305">Other included script libraries do not include the version number in the script name, so they can be more easily updated to their latest versions.</span></span>

<a id="tu-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="8fdf5-306">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-306">Known Issues</span></span>

- <span data-ttu-id="8fdf5-307">在某些情况下，安装可能会失败，并出现错误消息 "安装失败，出现错误代码（0x80070643）"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-307">In some cases, installation may fail with the error message "Installation failed with error code (0x80070643)".</span></span> <span data-ttu-id="8fdf5-308">有关如何解决此问题的信息，请参阅[知识库文章 2531566](https://support.microsoft.com/kb/2531566)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-308">For information about how to work around this issue, see [KnowledgeBase article 2531566](https://support.microsoft.com/kb/2531566).</span></span>
- <span data-ttu-id="8fdf5-309">用于添加控制器的创建基架功能不会为利用 Entity Framework 内的实体继承支持的实体创建基架。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-309">The scaffolding for adding a controller does not scaffold entities that take advantage of entity inheritance support within Entity Framework.</span></span> <span data-ttu-id="8fdf5-310">例如，给定*学生*类继承的基本*Person*类，则*student*类的基架将导致生成的代码不进行编译。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-310">For example, given a base *Person* class that's inherited by a *Student* class, scaffolding the *Student* class will result in generated code that does not compile.</span></span>
- <span data-ttu-id="8fdf5-311">在解决方案文件夹中创建新的 ASP.NET MVC 3 项目会导致*NullReferenceException*错误。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-311">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="8fdf5-312">解决方法是在解决方案的根中创建 ASP.NET MVC 3 项目，然后将其移到解决方案文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-312">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="8fdf5-313">在安装 ReSharper 时，IntelliSense for Razor 语法不起作用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-313">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="8fdf5-314">如果你已安装 ReSharper，并且想要充分利用 ASP.NET MVC 3 中的 Razor IntelliSense 支持，请参阅 Hadi Hariri 博客上的入门[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中讨论了如何将它们一起使用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-314">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="8fdf5-315">在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-315">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="8fdf5-316">编辑 Razor 视图（cshtml 或。*vbhtml*文件），视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-316">When you are editing a Razor view (.cshtml or .*vbhtml* file), views.</span></span> <span data-ttu-id="8fdf5-317">ASP.NET MVC 3 不包括 Razor 视图的任何代码段。aspxselecting ASP.NET MVC 的代码片段将显示</span><span class="sxs-lookup"><span data-stu-id="8fdf5-317">ASP.NET MVC 3 does not include any snippets for Razor views..aspxselecting a code snippet for ASP.NET MVC will show snippets for</span></span>
- <span data-ttu-id="8fdf5-318">如果在未安装 Visual Studio 的计算机上安装适用于 Visual Web Developer Express 的 ASP.NET MVC 3，然后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-318">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="8fdf5-319">Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-319">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="8fdf5-320">如果在没有 Visual Web Developer 速成版的计算机上安装适用于 Visual Studio 的 ASP.NET MVC 3，然后再安装 Visual Web Developer Express，则会遇到同样的问题。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-320">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a><span data-ttu-id="8fdf5-321">ASP.NET MVC 3 RTM 中的更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-321">Changes in ASP.NET MVC 3 RTM</span></span>

<span data-ttu-id="8fdf5-322">本部分介绍自 RC2 版本以来在 ASP.NET MVC 3 RTM 版本中所做的更改和 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-322">This section describes changes and bug fixes made in the ASP.NET MVC 3 RTM release since the RC2 release.</span></span>

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a><span data-ttu-id="8fdf5-323">Change：已将 jQuery UI 版本更新为1.8。7</span><span class="sxs-lookup"><span data-stu-id="8fdf5-323">Change: Updated the version of jQuery UI to 1.8.7</span></span>

<span data-ttu-id="8fdf5-324">Visual Studio 的 ASP.NET MVC 项目模板已更新，以包括 jQuery UI 库的最新版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-324">The ASP.NET MVC project templates for Visual Studio were updated to include the latest version of the jQuery UI library.</span></span> <span data-ttu-id="8fdf5-325">这些模板还包括 jQuery UI 所需的最小资源文件集，如关联的 CSS 和图像文件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-325">The templates also include the minimal set of resource files required by jQuery UI, such as the associated CSS and image files.</span></span>

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a><span data-ttu-id="8fdf5-326">更改：将默认 ModelMetadataProvider 更改回 DataAnnotationsModelMetadataProvider</span><span class="sxs-lookup"><span data-stu-id="8fdf5-326">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>

<span data-ttu-id="8fdf5-327">ASP.NET MVC 3 的 RC2 版本引入了一个*CachedDataAnnotationsMetadataProvider*类，它提供了在现有*DataAnnotationsModelMetadataProvider*类的基础上进行缓存以提高性能。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-327">The RC2 release of ASP.NET MVC 3 introduced a *CachedDataAnnotationsMetadataProvider* class that provided caching on top of the existing *DataAnnotationsModelMetadataProvider* class as a performance improvement.</span></span> <span data-ttu-id="8fdf5-328">但是，在此实现中报告了一些 bug，因此更改已还原并移入 MVC 先期备货项目，该项目可在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)中找到。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-328">However, some bugs were reported with this implementation, so the change has been reverted and moved into the MVC Futures project, which is available at [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack).</span></span>

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a><span data-ttu-id="8fdf5-329">已修复：粘贴包含空格的 Razor 表达式的一部分将导致其反向</span><span class="sxs-lookup"><span data-stu-id="8fdf5-329">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>

<span data-ttu-id="8fdf5-330">在 ASP.NET MVC 3 的预发行版本中，当你将包含空格的 Razor 表达式的一部分粘贴到 Razor 文件中时，结果表达式将会反向。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-330">In pre-release versions of ASP.NET MVC 3, when you paste a part of a Razor expression that contains whitespace into a Razor file, the resulting expression is reversed.</span></span> <span data-ttu-id="8fdf5-331">例如，请考虑以下 Razor 代码块：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-331">For example, consider the following Razor code block:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

<span data-ttu-id="8fdf5-332">如果在第一个方法中选择 "第一个参数" 文本，并将其作为参数粘贴到第二个方法中，则结果如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-332">If you select the text "first param" in the first method and paste it as an argument into the second method, the result is as follows:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="8fdf5-333">正确的行为是粘贴操作应该导致以下内容：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-333">The correct behavior is that the paste operation should result in the following:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

<span data-ttu-id="8fdf5-334">此问题已在 RTM 版本中得到解决，以便在粘贴操作过程中正确保留表达式。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-334">This issue has been fixed in the RTM release so that the expression is correctly preserved during the paste operation.</span></span>

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a><span data-ttu-id="8fdf5-335">已修复：重命名在编辑器中打开的 Razor 文件将禁用语法着色和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="8fdf5-335">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>

<span data-ttu-id="8fdf5-336">在编辑器窗口中打开文件时，使用解决方案资源管理器重命名 Razor 文件会导致语法突出显示和 IntelliSense 停止为该文件工作。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-336">Renaming a Razor file using Solution Explorer while the file is opened in the editor window causes syntax highlighting and IntelliSense to stop working for that file.</span></span> <span data-ttu-id="8fdf5-337">这是固定的，以便在重命名后保留突出显示和 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-337">This has been fixed so that highlighting and IntelliSense are maintained after a rename.</span></span>

<a id="RTM-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="8fdf5-338">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-338">Known Issues</span></span>

- <span data-ttu-id="8fdf5-339">如果在 NuGet 包管理器控制台打开时关闭 Visual Studio 2010 SP1 Beta，则 Visual Studio 将崩溃并尝试重新启动。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-339">If you close Visual Studio 2010 SP1 Beta while the NuGet Package Manager Console is open, Visual Studio crashes and attempts to restart.</span></span> <span data-ttu-id="8fdf5-340">这会在 Visual Studio 2010 SP1 的 RTM 版本中得到解决。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-340">This will be fixed in the RTM release of Visual Studio 2010 SP1.</span></span>
- <span data-ttu-id="8fdf5-341">ASP.NET MVC 3 安装程序只能安装初始版本的 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-341">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="8fdf5-342">安装初始版本后，可以使用 Visual Studio 扩展管理器安装和更新 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-342">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="8fdf5-343">如果已安装 NuGet，请前往 Visual Studio 扩展库，更新到最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-343">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="8fdf5-344">在解决方案文件夹中创建新的 ASP.NET MVC 3 项目会导致*NullReferenceException*错误。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-344">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="8fdf5-345">解决方法是在解决方案的根中创建 ASP.NET MVC 3 项目，然后将其移到解决方案文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-345">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="8fdf5-346">安装程序所需的时间可能比以前版本的 ASP.NET MVC 长得多。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-346">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="8fdf5-347">这是因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-347">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="8fdf5-348">在安装 ReSharper 时，IntelliSense for Razor 语法不起作用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-348">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="8fdf5-349">如果你已安装 ReSharper，并且想要充分利用 ASP.NET MVC 3 中的 Razor IntelliSense 支持，请参阅 Hadi Hariri 博客上的入门[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中讨论了如何将它们一起使用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-349">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="8fdf5-350">使用 ASP.NET MVC 3 的 Beta 版创建的 CCSHTML 和 VBHTML 视图没有正确设置其生成操作，这会导致在发布项目时省略这些视图类型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-350">CCSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="8fdf5-351">应将这些文件的 "生成操作" 值设置为 "内容"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-351">The Build Action value for these files should be set to "Content".</span></span> <span data-ttu-id="8fdf5-352">ASP.NET MVC 3 RTM 修复了新文件的这一问题，但没有更正使用预发行版本创建的项目的现有文件的设置。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-352">ASP.NET MVC 3 RTM fixes this issue for new files, but doesn't correct the setting for existing files for a project created with prerelease versions.</span></span>
- ![](mvc3-release-notes/_static/image3.png)
- <span data-ttu-id="8fdf5-353">在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-353">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="8fdf5-354">编辑 Razor 视图（cshtml 文件）时，Visual Studio 中的 "转向控制器" 菜单项将不可用，且没有代码段。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-354">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="8fdf5-355">如果在未安装 Visual Studio 的计算机上安装适用于 Visual Web Developer Express 的 ASP.NET MVC 3，然后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-355">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="8fdf5-356">Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-356">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="8fdf5-357">如果在没有 Visual Web Developer 速成版的计算机上安装适用于 Visual Studio 的 ASP.NET MVC 3，然后再安装 Visual Web Developer Express，则会遇到同样的问题。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-357">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="8fdf5-358">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-358">Breaking Changes</span></span>

- <span data-ttu-id="8fdf5-359">在以前版本的 ASP.NET MVC 中，操作筛选器根据请求创建，但在少数情况下除外。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-359">In previous versions of ASP.NET MVC, action filters are create per request except in a few cases.</span></span> <span data-ttu-id="8fdf5-360">此行为从来都不是保证的行为，但只是实现详细信息，筛选器的协定是将它们视为无状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-360">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="8fdf5-361">在 ASP.NET MVC 3 中，筛选器的缓存更严格。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-361">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="8fdf5-362">因此，任何自定义操作筛选器都不正确地存储实例状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-362">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="8fdf5-363">对于具有相同*顺序*值的异常筛选器，异常筛选器的执行顺序已更改。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-363">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="8fdf5-364">在 ASP.NET MVC 2 及更早版本中，与操作方法上的异常筛选器具有相同*顺序*值的异常筛选器在操作方法上的异常筛选器之前执行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-364">In ASP.NET MVC 2 and earlier, exception filters on the controller that have the same *Order* value as those on an action method are executed before the exception filters on the action method.</span></span> <span data-ttu-id="8fdf5-365">如果未指定*顺序*值应用异常筛选器，通常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-365">This would typically be the case when exception filters are applied without a specified *Order* value.</span></span> <span data-ttu-id="8fdf5-366">在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-366">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="8fdf5-367">与早期版本一样，如果显式指定*order*属性，则筛选器将按指定顺序运行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-367">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="8fdf5-368">名为*FileExtensions*的新属性已添加到*VirtualPathProviderViewEngine*基类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-368">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="8fdf5-369">当 ASP.NET 按路径（而不是按名称）查找视图时，仅考虑此新属性所指定的列表中包含的文件扩展名的视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-369">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="8fdf5-370">这是应用程序中的一项重大更改，其中注册了自定义生成提供程序，以便为 Web 窗体视图启用自定义文件扩展名，并使用完整路径而不是名称来引用这些视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-370">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="8fdf5-371">解决方法是修改*FileExtensions*属性的值，使之包括自定义文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-371">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="8fdf5-372">直接实现*IControllerFactory*接口的自定义控制器工厂实现必须提供已添加到此版本中的接口的新*GetControllerSessionBehavior*方法的实现。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-372">Custom controller factory implementations that directly implement the *IControllerFactory* interface must provide an implementation of the new *GetControllerSessionBehavior* method that was added to the interface in this release.</span></span> <span data-ttu-id="8fdf5-373">通常，建议您不要直接实现此接口，而是从*DefaultControllerFactory*派生您的类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-373">In general, it is recommended that you do not implement this interface directly and instead derive your class from *DefaultControllerFactory*.</span></span>

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a><span data-ttu-id="8fdf5-374">ASP.NET MVC 3 RC2 中的更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-374">Changes in ASP.NET MVC 3 RC2</span></span>

<span data-ttu-id="8fdf5-375">本部分介绍自 RC 版本以来在 ASP.NET MVC 3 RC2 版本中所做的更改（新增功能和 bug 修复）。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-375">This section describes changes (new features and bug fixes) made in the ASP.NET MVC 3 RC2 release since the RC release.</span></span>

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a><span data-ttu-id="8fdf5-376">项目模板已更改为包含 jQuery sqoop-user-guide-1.4.4、jQuery 验证1.7 和 jQuery UI 1.8。6</span><span class="sxs-lookup"><span data-stu-id="8fdf5-376">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6</span></span>

<span data-ttu-id="8fdf5-377">ASP.NET MVC 3 的项目模板现在包含 jQuery、jQuery 验证和 jQuery UI 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-377">The project templates for ASP.NET MVC 3 now include the latest versions of jQuery, jQuery Validation, and jQuery UI.</span></span> <span data-ttu-id="8fdf5-378">jQuery UI 是项目模板的新增补充，提供有用的用户界面小组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-378">jQuery UI is a new addition to the project templates and provides useful user interface widgets.</span></span> <span data-ttu-id="8fdf5-379">有关 jQuery UI 的详细信息，请访问其主页： [http://jqueryui.com/](http://jqueryui.com/)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-379">For more information about jQuery UI, visit their homepage: [http://jqueryui.com/](http://jqueryui.com/).</span></span>

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a><span data-ttu-id="8fdf5-380">添加了 "AdditionalMetadataAttribute" 类</span><span class="sxs-lookup"><span data-stu-id="8fdf5-380">Added "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="8fdf5-381">可以使用*AdditionalMetadataAttribute*类来填充模型属性的*AdditionalValues*字典。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-381">You can use the *AdditionalMetadataAttribute* class to populate the *ModelMetadata.AdditionalValues* dictionary for a model property.</span></span>

<span data-ttu-id="8fdf5-382">例如，假设视图模型的属性仅应显示给管理员。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-382">For example, suppose a view model has properties that should be displayed only to an administrator.</span></span> <span data-ttu-id="8fdf5-383">该模型可以使用 AdminOnly 作为键，并使用新属性进行批注，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-383">That model can be annotated with the new attribute using AdminOnly as the key and true as the value, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

<span data-ttu-id="8fdf5-384">呈现产品视图模型时，此元数据可用于任何显示或编辑模板。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-384">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="8fdf5-385">它由应用程序开发人员来解释元数据信息。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-385">It is up to you as application developer to interpret the metadata information.</span></span>

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a><span data-ttu-id="8fdf5-386">改进的视图基架</span><span class="sxs-lookup"><span data-stu-id="8fdf5-386">Improved View Scaffolding</span></span>

<span data-ttu-id="8fdf5-387">用于基架视图的 T4 模板现在可生成对模板帮助器方法（例如*html.editorfor* ）的调用，而不是*TextBoxFor*的帮助器。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-387">The T4 templates used for scaffolding views now generate calls to template helper methods such as *EditorFor* instead of helpers such as *TextBoxFor*.</span></span> <span data-ttu-id="8fdf5-388">当 "添加视图" 对话框生成视图时，此更改以数据批注特性的形式改进对模型上的元数据的支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-388">This change improves support for metadata on the model in the form of data annotation attributes when the Add View dialog box generates a view.</span></span>

<span data-ttu-id="8fdf5-389">"添加视图" 基架还包括根据约定，改进了模型中的主键信息的检测和使用情况。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-389">The Add View scaffolding also includes improved detection and usage of primary key information on the model, based on convention.</span></span> <span data-ttu-id="8fdf5-390">例如，"添加视图" 对话框使用此信息来确保不将主键值基架为可编辑的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-390">For example, the Add View dialog box uses this information to ensure that the primary key value is not scaffolded as an editable form field.</span></span>

<span data-ttu-id="8fdf5-391">默认的编辑和创建模板包括对客户端验证所需的 jQuery 脚本的引用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-391">The default Edit and Create templates include references to the jQuery scripts needed for client validation.</span></span>

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a><span data-ttu-id="8fdf5-392">添加了 Html Raw 方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-392">Added Html.Raw Method</span></span>

<span data-ttu-id="8fdf5-393">默认情况下，Razor 视图引擎对所有值进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-393">By default, the Razor view engine HTML-encodes all values.</span></span> <span data-ttu-id="8fdf5-394">例如，下面的代码段对问候语变量中的 HTML 进行编码，使其在页面中显示为 `<strong>Hello World!</strong>`。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-394">For example, the following code snippet encodes the HTML inside the greeting variable so that it is displayed in the page as `<strong>Hello World!</strong>`.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

<span data-ttu-id="8fdf5-395">当已知内容安全时，新的 *.html*方法会提供一种简单的方法来显示未编码的 Html。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-395">The new *Html.Raw* method provides a simple way of displaying unencoded HTML when the content is known to be safe.</span></span> <span data-ttu-id="8fdf5-396">下面的示例显示相同的字符串，但该字符串呈现为标记：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-396">The following example displays the same string, but the string is rendered as markup:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a><span data-ttu-id="8fdf5-397">重命名为 "ViewModel" 属性，并将 "View" 属性重命名为 "ViewBag"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-397">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>

<span data-ttu-id="8fdf5-398">以前， *Controller*对应的*ViewModel*属性指向视图的*视图*属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-398">Previously, the *ViewModel* property of *Controller* corresponded to the *View* property of a view.</span></span> <span data-ttu-id="8fdf5-399">这两个属性都提供使用动态属性访问器语法访问*ViewDataDictionary*对象的值的方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-399">Both of these properties provide a way to access values of the *ViewDataDictionary* object using dynamic property-accessor syntax.</span></span> <span data-ttu-id="8fdf5-400">这两个属性都已重命名为相同，以避免混淆并使其更一致。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-400">Both properties have been renamed to be the same in order to avoid confusion and to be more consistent.</span></span>

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a><span data-ttu-id="8fdf5-401">已将 "ControllerSessionStateAttribute" 类重命名为 "SessionStateAttribute"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-401">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>

<span data-ttu-id="8fdf5-402">ASP.NET MVC 3 的 RC 版本中引入了*ControllerSessionStateAttribute*类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-402">The *ControllerSessionStateAttribute* class was introduced in the RC release of ASP.NET MVC 3.</span></span> <span data-ttu-id="8fdf5-403">该属性已重命名为更简洁。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-403">The property was renamed to be more succinct.</span></span>

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a><span data-ttu-id="8fdf5-404">将 RemoteAttribute "Fields" 属性重命名为 "AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-404">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>

<span data-ttu-id="8fdf5-405">*RemoteAttribute*类的 "*字段*" 属性导致用户之间出现一些混淆。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-405">The *RemoteAttribute* class's *Fields* property caused some confusion among users.</span></span> <span data-ttu-id="8fdf5-406">将该属性重命名为*AdditionalFields*可阐明其意图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-406">Renaming this property to *AdditionalFields* clarifies its intent.</span></span>

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a><span data-ttu-id="8fdf5-407">已将 "SkipRequestValidationAttribute" 重命名为 "AllowHtmlAttribute"</span><span class="sxs-lookup"><span data-stu-id="8fdf5-407">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>

<span data-ttu-id="8fdf5-408">*SkipRequestValidationAttribute*属性已重命名为*AllowHtmlAttribute* ，以更好地表示其预期用途。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-408">The *SkipRequestValidationAttribute* attribute was renamed to *AllowHtmlAttribute* to better represent its intended usage.</span></span>

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a><span data-ttu-id="8fdf5-409">更改了 "ValidationMessage" 方法以显示第一个有用的错误消息</span><span class="sxs-lookup"><span data-stu-id="8fdf5-409">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>

<span data-ttu-id="8fdf5-410">*ValidationMessage*方法已修复，以便显示第一个有用的错误消息，而不只是显示第一个错误。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-410">The *Html.ValidationMessage* method was fixed to show the first useful error message instead of simply displaying the first error.</span></span>

<span data-ttu-id="8fdf5-411">在模型绑定过程中，可以从多个源填充*ModelState*字典，其中包含有关属性的错误消息，包括从模型本身（如果它实现*IValidatableObject*）、应用于属性的验证特性，以及在访问属性时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-411">During model binding, the *ModelState* dictionary can be populated from multiple sources with error messages about the property, including from the model itself (if it implements *IValidatableObject*), from validation attributes applied to the property, and from exceptions thrown while the property is being accessed.</span></span>

<span data-ttu-id="8fdf5-412">当*ValidationMessage*方法显示验证消息时，它会跳过包含异常的模型状态条目，因为这些条目通常不适用于最终用户。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-412">When the *Html.ValidationMessage* method displays a validation message, it skips model-state entries that include an exception, because these are generally not intended for the end user.</span></span> <span data-ttu-id="8fdf5-413">相反，方法会查找不与异常相关联的第一条验证消息，并显示该消息。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-413">Instead, the method looks for the first validation message that is not associated with an exception and displays that message.</span></span> <span data-ttu-id="8fdf5-414">如果未找到这样的消息，则默认为与第一个异常相关联的一般错误消息。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-414">If no such message is found, it defaults to a generic error message that is associated with the first exception.</span></span>

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a><span data-ttu-id="8fdf5-415">固定 @model 声明，不向文档中添加空白</span><span class="sxs-lookup"><span data-stu-id="8fdf5-415">Fixed @model Declaration to not Add Whitespace to the Document</span></span>

<span data-ttu-id="8fdf5-416">在早期版本中，视图顶部的 `@model` 声明向呈现的 HTML 输出添加了一个空行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-416">In earlier releases, the `@model` declaration at the top of a view added a blank line to the rendered HTML output.</span></span> <span data-ttu-id="8fdf5-417">这是固定的，因此声明不会引入空白。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-417">This has been fixed so that the declaration does not introduce whitespace.</span></span>

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a><span data-ttu-id="8fdf5-418">添加了 "FileExtensions" 属性以查看引擎，以支持引擎特定的文件名</span><span class="sxs-lookup"><span data-stu-id="8fdf5-418">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>

<span data-ttu-id="8fdf5-419">视图引擎可以使用显式视图路径返回视图，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-419">A view engine can return a view using an explicit view path as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

<span data-ttu-id="8fdf5-420">第一个视图引擎始终尝试呈现视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-420">The first view engine always attempts to render the view.</span></span> <span data-ttu-id="8fdf5-421">默认情况下，Web 窗体视图引擎是第一个视图引擎;由于 Web 窗体引擎无法呈现 Razor 视图，因此将发生错误。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-421">By default, the Web Forms view engine is the first view engine; because the Web Forms engine cannot render a Razor view, an error occurs.</span></span> <span data-ttu-id="8fdf5-422">视图引擎现在具有一个*FileExtensions*属性，用于指定所支持的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-422">View engines now have a *FileExtensions* property that is used to specify which file extensions they support.</span></span> <span data-ttu-id="8fdf5-423">当 ASP.NET 确定视图引擎是否可以呈现文件时，将检查此属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-423">This property is checked when ASP.NET determines whether a view engine can render a file.</span></span> <span data-ttu-id="8fdf5-424">这是一项重大更改，并在本文档的 "[重大更改](#_Toc2_BC)" 部分中提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-424">This is a breaking change and more details are included in the [Breaking Changes](#_Toc2_BC) section of this document.</span></span>

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a><span data-ttu-id="8fdf5-425">修复了 "Html.labelfor" 帮助程序，以便为 "For" 特性发出正确的值</span><span class="sxs-lookup"><span data-stu-id="8fdf5-425">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>

<span data-ttu-id="8fdf5-426">修复了一个 bug，其中*html.labelfor*方法为与*输入*元素的*name*属性（而不是其 ID）匹配的*获取*属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-426">A bug was fixed where the *LabelFor* method rendered a *for* attribute that matches the *input* element's *name* attribute instead of its ID.</span></span> <span data-ttu-id="8fdf5-427">根据 W3C， *for*特性应与*输入*元素的 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-427">According to the W3C, the *for* attribute should match the *input* element's ID.</span></span>

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a><span data-ttu-id="8fdf5-428">修复了在模型绑定期间为显式值指定优先级的 "RenderAction" 方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-428">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>

<span data-ttu-id="8fdf5-429">在早期版本中，在子操作内的模型绑定期间，将忽略传递给*RenderAction*方法的显式值，以支持当前窗体值。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-429">In earlier versions, explicit values that were passed to the *RenderAction* method were being ignored in favor of the current form values during model binding inside a child action.</span></span> <span data-ttu-id="8fdf5-430">此修补程序确保在模型绑定期间显式值优先。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-430">The fix ensures that explicit values take precedence during model binding.</span></span>

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="8fdf5-431">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-431">Breaking Changes</span></span>

- <span data-ttu-id="8fdf5-432">在以前版本的 ASP.NET MVC 中，操作筛选器是根据请求创建的，但在少数情况下除外。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-432">In previous versions of ASP.NET MVC, action filters were created per request except in a few cases.</span></span> <span data-ttu-id="8fdf5-433">此行为从来都不是保证的行为，但只是实现详细信息，筛选器的协定是将它们视为无状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-433">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="8fdf5-434">在 ASP.NET MVC 3 中，筛选器的缓存更严格。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-434">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="8fdf5-435">因此，任何自定义操作筛选器都不正确地存储实例状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-435">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="8fdf5-436">对于具有相同*顺序*值的异常筛选器，异常筛选器的执行顺序已更改。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-436">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="8fdf5-437">在 ASP.NET MVC 2 及更早版本中，在执行操作方法上的异常筛选器之前，控制器上的异常筛选器的*顺序*值与操作方法上的相同。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-437">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* value as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="8fdf5-438">如果未指定*顺序*值应用了异常筛选器，通常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-438">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="8fdf5-439">在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-439">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="8fdf5-440">与早期版本一样，如果显式指定*order*属性，则筛选器将按指定顺序运行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-440">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="8fdf5-441">名为*FileExtensions*的新属性已添加到*VirtualPathProviderViewEngine*基类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-441">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="8fdf5-442">当 ASP.NET 按路径（而不是按名称）查找视图时，仅考虑此新属性所指定的列表中包含的文件扩展名的视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-442">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="8fdf5-443">这是应用程序中的一项重大更改，其中注册了自定义生成提供程序，以便为 Web 窗体视图启用自定义文件扩展名，并使用完整路径而不是名称来引用这些视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-443">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="8fdf5-444">解决方法是修改*FileExtensions*属性的值，使之包括自定义文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-444">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="8fdf5-445">直接实现*IControllerFactory*接口的自定义控制器工厂实现必须提供已添加到此版本中的接口的新*GetControllerSessionBehavior*方法的实现。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-445">Custom controller factory implementations that directly implement the *IControllerFactory* interface must provide an implementation of the new *GetControllerSessionBehavior* method that was added to the interface in this release.</span></span> <span data-ttu-id="8fdf5-446">通常，建议您不要直接实现此接口，而是从*DefaultControllerFactory*派生您的类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-446">In general, it is recommended that you do not implement this interface directly and instead derive your class from *DefaultControllerFactory*.</span></span>

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a><span data-ttu-id="8fdf5-447">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-447">Known Issues</span></span>

- <span data-ttu-id="8fdf5-448">ASP.NET MVC 3 安装程序只能安装初始版本的 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-448">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="8fdf5-449">安装初始版本后，可以使用 Visual Studio 扩展管理器安装和更新 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-449">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="8fdf5-450">如果已安装 NuGet，请前往 Visual Studio 扩展库，更新到最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-450">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="8fdf5-451">在解决方案文件夹中创建新的 ASP.NET MVC 3 项目会导致*NullReferenceException*错误。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-451">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="8fdf5-452">解决方法是在解决方案的根中创建 ASP.NET MVC 3 项目，然后将其移到解决方案文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-452">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="8fdf5-453">安装程序所需的时间可能比以前版本的 ASP.NET MVC 长得多。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-453">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="8fdf5-454">这是因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-454">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="8fdf5-455">在安装 ReSharper 时，IntelliSense for Razor 语法不起作用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-455">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="8fdf5-456">如果你已安装 ReSharper，并且想要利用 ASP.NET MVC 3 RC2 中的 Razor IntelliSense 支持，请参阅 Hadi Hariri 博客上的入门[Razor intellisense 和 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) ，其中讨论了如何将它们一起使用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-456">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3 RC2, see the entry [Razor Intellisense and ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="8fdf5-457">使用 ASP.NET MVC 3 的 Beta 版创建的 CSHTML 和 VBHTML 视图没有正确设置其生成操作，这会导致在发布项目时省略这些视图类型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-457">CSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="8fdf5-458">应将这些文件的*生成操作*值设置为 "内容"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-458">The *Build Action* value for these files should be set to Content".</span></span> <span data-ttu-id="8fdf5-459">ASP.NET MVC 3 RC2 修复了新文件的这一问题，但并不更正使用 Beta 版本创建的项目的现有文件的设置。![](mvc3-release-notes/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8fdf5-459">ASP.NET MVC 3 RC2 fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta version.![](mvc3-release-notes/_static/image4.png)</span></span>
- <span data-ttu-id="8fdf5-460">在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-460">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="8fdf5-461">编辑 Razor 视图（cshtml 文件）时，Visual Studio 中的 "转向控制器" 菜单项将不可用，且没有代码段。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-461">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="8fdf5-462">如果在未安装 Visual Studio 的计算机上安装适用于 Visual Web Developer Express 的 ASP.NET MVC 3，然后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-462">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="8fdf5-463">Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-463">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="8fdf5-464">如果在没有 Visual Web Developer 速成版的计算机上安装适用于 Visual Studio 的 ASP.NET MVC 3，然后再安装 Visual Web Developer Express，则会遇到同样的问题。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-464">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>
- <span data-ttu-id="8fdf5-465">如果已安装 ASP.NET MVC 3 RC 2，则安装它不会更新 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-465">Installing ASP.NET MVC 3 RC 2 does not update NuGet if you already have it installed.</span></span> <span data-ttu-id="8fdf5-466">若要升级 NuGet，请访问 Visual Studio 扩展管理器，该管理器应显示为可用更新。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-466">To upgrade NuGet, go to the Visual Studio Extension manager and it should show up as an available update.</span></span> <span data-ttu-id="8fdf5-467">你可以从此处将 NuGet 升级到最新版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-467">You can upgrade NuGet to the latest release from there.</span></span>

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a><span data-ttu-id="8fdf5-468">ASP.NET MVC 3 候选发布</span><span class="sxs-lookup"><span data-stu-id="8fdf5-468">ASP.NET MVC 3 Release Candidate</span></span>

<span data-ttu-id="8fdf5-469">ASP.NET MVC 候选发布版于2010年11月9日发布。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-469">ASP.NET MVC Release Candidate was released on November 9, 2010.</span></span>

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a><span data-ttu-id="8fdf5-470">ASP.NET MVC 3 RC 中的新功能</span><span class="sxs-lookup"><span data-stu-id="8fdf5-470">New Features in ASP.NET MVC 3 RC</span></span>

<span data-ttu-id="8fdf5-471">本部分介绍自 Beta 版本后 ASP.NET MVC 3 RC 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-471">This section describes features that have been introduced in the ASP.NET MVC 3 RC release since the Beta release.</span></span>

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a><span data-ttu-id="8fdf5-472">NuGet 程序包管理器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-472">NuGet Package Manager</span></span>

<span data-ttu-id="8fdf5-473">ASP.NET MVC 3 包括 NuGet 包管理器（以前称为 NuPack），这是用于向 Visual Studio 项目添加库和工具的集成包管理工具。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-473">ASP.NET MVC 3 includes the NuGet Package Manager (formerly known as NuPack), which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="8fdf5-474">此工具可自动执行开发人员在源树中获取库所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-474">This tool automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="8fdf5-475">在 Visual Studio 2010、Visual Studio 上下文菜单和一组 PowerShell cmdlet 中，你可以使用 NuGet 作为命令行工具，作为集成的控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-475">You can work with NuGet as a command-line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as a set of PowerShell cmdlets.</span></span>

<span data-ttu-id="8fdf5-476">有关 NuGet 的详细信息，请参阅[Nuget 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-476">For more information about NuGet, read the [Nuget Documentation](https://docs.microsoft.com/nuget/).</span></span>

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a><span data-ttu-id="8fdf5-477">改进了 "新建项目" 对话框</span><span class="sxs-lookup"><span data-stu-id="8fdf5-477">Improved "New Project" Dialog Box</span></span>

<span data-ttu-id="8fdf5-478">创建新项目时，"新建项目" 对话框现在允许你指定视图引擎以及 ASP.NET MVC 项目类型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-478">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image5.png)

<span data-ttu-id="8fdf5-479">此版本包含了对修改对话框中列出的模板和视图引擎列表的支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-479">Support for modifying the list of templates and view engines listed in the dialog box is included in this release.</span></span>

<span data-ttu-id="8fdf5-480">默认模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-480">The default templates are the following:</span></span>

<span data-ttu-id="8fdf5-481">空。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-481">Empty.</span></span> <span data-ttu-id="8fdf5-482">包含 ASP.NET MVC 项目的最小文件集，其中包括 ASP.NET MVC 项目的默认目录结构、包含默认 ASP.NET MVC 样式的 web.config 文件以及包含默认 JavaScript 文件的脚本目录。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-482">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="8fdf5-483">Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-483">Internet Application.</span></span> <span data-ttu-id="8fdf5-484">包含演示如何将成员资格提供程序与 ASP.NET MVC 一起使用的示例功能。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-484">Contains sample functionality that demonstrates how to use the membership provider with ASP.NET MVC.</span></span>

<span data-ttu-id="8fdf5-485">对话框中显示的项目模板的列表在 Windows 注册表中指定。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-485">The list of project templates that is displayed in the dialog box is specified in the Windows registry.</span></span>

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a><span data-ttu-id="8fdf5-486">无会话控制器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-486">Sessionless Controllers</span></span>

<span data-ttu-id="8fdf5-487">新的*ControllerSessionStateAttribute*通过指定[SessionState. SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)枚举值，使你能够更好地控制控制器的会话状态行为。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-487">The new *ControllerSessionStateAttribute* gives you more control over session-state behavior for controllers by specifying a [System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) enumeration value.</span></span>

<span data-ttu-id="8fdf5-488">下面的示例演示如何关闭对控制器的所有请求的会话状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-488">The following example shows how to turn off session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

<span data-ttu-id="8fdf5-489">下面的示例演示如何为控制器的所有请求设置只读会话状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-489">The following example shows how to set read-only session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a><span data-ttu-id="8fdf5-490">新验证属性</span><span class="sxs-lookup"><span data-stu-id="8fdf5-490">New Validation Attributes</span></span>

#### <a name="compareattribute"></a><span data-ttu-id="8fdf5-491">CompareAttribute</span><span class="sxs-lookup"><span data-stu-id="8fdf5-491">CompareAttribute</span></span>

<span data-ttu-id="8fdf5-492">使用 new *CompareAttribute*验证特性可以比较模型的两个不同属性的值。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-492">The new *CompareAttribute* validation attribute lets you compare the values of two different properties of a model.</span></span> <span data-ttu-id="8fdf5-493">在下面的示例中， *ComparePassword*属性必须与*密码*字段匹配才能有效。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-493">In the following example, the *ComparePassword* property must match the *Password* field in order to be valid.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a><span data-ttu-id="8fdf5-494">RemoteAttribute</span><span class="sxs-lookup"><span data-stu-id="8fdf5-494">RemoteAttribute</span></span>

<span data-ttu-id="8fdf5-495">新的*RemoteAttribute*验证属性利用 jQuery 验证插件的远程验证程序，这使得客户端验证能够在执行实际验证逻辑的服务器上调用方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-495">The new *RemoteAttribute* validation attribute takes advantage of the jQuery Validation plug-in's remote validator, which enables client-side validation to call a method on the server that performs the actual validation logic.</span></span>

<span data-ttu-id="8fdf5-496">在下面的示例中， *UserName*属性应用了*RemoteAttribute* 。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-496">In the following example, the *UserName* property has the *RemoteAttribute* applied.</span></span> <span data-ttu-id="8fdf5-497">在编辑视图中编辑此属性时，客户端验证将调用*UsersController*类上名为*UserNameAvailable*的操作，以便验证此字段。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-497">When editing this property in an Edit view, client validation will call an action named *UserNameAvailable* on the *UsersController* class in order to validate this field.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

<span data-ttu-id="8fdf5-498">下面的示例演示了相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-498">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

<span data-ttu-id="8fdf5-499">默认情况下，应用该特性的属性名称将作为查询字符串参数发送到操作方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-499">By default, the property name that the attribute is applied to is sent to the action method as a query-string parameter.</span></span>

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a><span data-ttu-id="8fdf5-500">"Html.labelfor" 和 "LabelForModel" 方法的新重载</span><span class="sxs-lookup"><span data-stu-id="8fdf5-500">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>

<span data-ttu-id="8fdf5-501">添加了*html.labelfor*和*LabelForModel*方法的新重载，使您可以指定标签文本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-501">New overloads have been added for the *LabelFor* and *LabelForModel* methods that let you specify the label text.</span></span> <span data-ttu-id="8fdf5-502">下面的示例演示如何使用这些重载。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-502">The following example shows how to use these overloads.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a><span data-ttu-id="8fdf5-503">子操作输出缓存</span><span class="sxs-lookup"><span data-stu-id="8fdf5-503">Child Action Output Caching</span></span>

<span data-ttu-id="8fdf5-504">*OutputCacheAttribute*支持通过使用*RenderAction*或*html. 操作*帮助器方法调用的子操作的输出缓存。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-504">The *OutputCacheAttribute* supports output caching of child actions that are called by using the *Html.RenderAction* or *Html.Action* helper methods.</span></span> <span data-ttu-id="8fdf5-505">下面的示例演示了一个调用另一个操作的视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-505">The following example shows a view that calls another action.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

<span data-ttu-id="8fdf5-506">*GetDate*操作用*OutputCacheAttribute*批注：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-506">The *GetDate* action is annotated with the *OutputCacheAttribute*:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

<span data-ttu-id="8fdf5-507">此代码运行时，对 Html. Action （"GetDate"）的调用的结果缓存了100秒。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-507">When this code runs, the result of the call to Html.Action("GetDate") is cached for 100 seconds.</span></span>

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a><span data-ttu-id="8fdf5-508">"添加视图" 对话框改进</span><span class="sxs-lookup"><span data-stu-id="8fdf5-508">"Add View" Dialog Box Improvements</span></span>

<span data-ttu-id="8fdf5-509">添加强类型视图时，"添加视图" 对话框现在会筛选出比以前版本更多的不适用类型，例如许多核心 .NET Framework 类型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-509">When you add a strongly typed view, the Add View dialog box now filters out more non-applicable types than in previous releases, such as many core .NET Framework types.</span></span> <span data-ttu-id="8fdf5-510">此外，该列表现在按类名而不是完全限定的类型名称进行排序，这使得查找类型变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-510">Also, the list is now sorted by the class name and not by the fully qualified type name, which makes it easier to find types.</span></span> <span data-ttu-id="8fdf5-511">例如，类型名称现在显示为，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-511">For example, the type name is now displayed as in the following example:</span></span>

<span data-ttu-id="8fdf5-512">ClassName （命名空间）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-512">ClassName (namespace)</span></span>

<span data-ttu-id="8fdf5-513">在以前的版本中，这会显示如下：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-513">In earlier releases, this would have been displayed as the following:</span></span>

<span data-ttu-id="8fdf5-514">Namespace.ClassName</span><span class="sxs-lookup"><span data-stu-id="8fdf5-514">Namespace.ClassName</span></span>

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a><span data-ttu-id="8fdf5-515">精细请求验证</span><span class="sxs-lookup"><span data-stu-id="8fdf5-515">Granular Request Validation</span></span>

<span data-ttu-id="8fdf5-516">*ValidateInputAttribute*的*Exclude*属性不再存在。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-516">The *Exclude* property of *ValidateInputAttribute* no longer exists.</span></span> <span data-ttu-id="8fdf5-517">相反，若要在模型绑定期间为模型的特定属性跳过请求验证，请使用新的*SkipRequestValidationAttribute*。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-517">Instead, to have request validation skipped for specific properties of a model during model binding, use the new *SkipRequestValidationAttribute*.</span></span>

<span data-ttu-id="8fdf5-518">例如，假设使用操作方法编辑博客文章：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-518">For example, suppose an action method is used to edit a blog post:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

<span data-ttu-id="8fdf5-519">下面的示例演示博客文章的视图模型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-519">The following example shows the view model for a blog post.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

<span data-ttu-id="8fdf5-520">当用户提交 Description 属性的某些标记时，模型绑定将由于请求验证而失败。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-520">When a user submits some markup for the Description property, model binding will fail due to request validation.</span></span> <span data-ttu-id="8fdf5-521">若要在博客文章说明的模型绑定期间禁用请求验证，请将*SkipRequpestValidationAttribute*应用到属性，如以下示例中所示：。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-521">To disable request validation during model binding for the blog post Description, apply the *SkipRequpestValidationAttribute* to the property, as shown in this example:.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

<span data-ttu-id="8fdf5-522">或者，若要关闭模型的每个属性的请求验证，请将值为*false*的*ValidateInputAttribute*应用到操作方法：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-522">Alternatively, to turn off request validation for every property of the model, apply *ValidateInputAttribute* with a value of *false* to the action method:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a><span data-ttu-id="8fdf5-523">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-523">Breaking Changes</span></span>

- <span data-ttu-id="8fdf5-524">对于具有相同*顺序*值的异常筛选器，异常筛选器的执行顺序已更改。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-524">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="8fdf5-525">在 ASP.NET MVC 2 及更早版本中，与操作方法上的异常筛选器*顺序*相同的异常筛选器在操作方法上的异常筛选器之前执行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-525">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="8fdf5-526">如果未指定*顺序*值应用了异常筛选器，通常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-526">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="8fdf5-527">在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-527">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="8fdf5-528">与早期版本一样，如果显式指定*order*属性，则筛选器将按指定顺序运行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-528">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="8fdf5-529">向*VirtualPathProviderViewEngine*基类添加了名为*FileExtensions*的新属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-529">Added a new property named *FileExtensions* to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="8fdf5-530">当按路径（而不是按名称）查找视图时，仅考虑此新属性所指定的列表中包含的文件扩展名的视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-530">When looking up a view by path (and not by name), only views with a file extension contained in the list specified by this new property is considered.</span></span> <span data-ttu-id="8fdf5-531">这是对注册自定义生成提供程序以启用 web 窗体视图的自定义文件扩展名，并使用完整路径而不是名称引用这些视图的用户的重大更改。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-531">This is a breaking change for those who register a custom build provider to enable a custom file extension for web form views and are referencing those views by using a full path rather than a name.</span></span> <span data-ttu-id="8fdf5-532">解决方法是修改*FileExtensions*属性的值，使之包括自定义文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-532">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>

<a id="_Toc276711795"></a>
## <a name="known-issues"></a><span data-ttu-id="8fdf5-533">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-533">Known Issues</span></span>

- <span data-ttu-id="8fdf5-534">安装程序要完成的时间可能比以前版本的 ASP.NET MVC 长得多，因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-534">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="8fdf5-535">选择 astrongly 类型化视图基架只写属性时，"添加视图" 基架。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-535">The Add View scaffolding when selecting astrongly typed view scaffolds write-only properties.</span></span> <span data-ttu-id="8fdf5-536">基架应始终忽略这些。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-536">These should always be ignored by scaffolding.</span></span> <span data-ttu-id="8fdf5-537">"添加视图" 对话框也会在生成 "编辑" 或 "创建" 视图时基架只读属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-537">The Add View dialog also scaffolds read-only properties when generating an "Edit" or "Create" view.</span></span> <span data-ttu-id="8fdf5-538">只读属性应该只基架显示和列表视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-538">Read-only properties should only be scaffolded for the Display and List views.</span></span>
- <span data-ttu-id="8fdf5-539">当 ASP.NET MVC 3 与异步 CTP 一起安装时，调试不起作用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-539">Debugging doesn't work when ASP.NET MVC 3 is installed alongside the Async CTP.</span></span> <span data-ttu-id="8fdf5-540">ASP.NET MVC 3 不能与 Async CTP 并行安装。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-540">ASP.NET MVC 3 cannot be installed side-by-side with the Async CTP.</span></span> <span data-ttu-id="8fdf5-541">卸载 Async CTP 以修复调试。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-541">Uninstall the Async CTP to repair debugging.</span></span> <span data-ttu-id="8fdf5-542">有关更多详细信息，请阅读[此博客文章](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)，了解如何卸载 ASP.NET MVC 3 RC 的所有部分。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-542">For more details, read [this blog post](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) about uninstalling all the pieces of ASP.NET MVC 3 RC.</span></span>
- <span data-ttu-id="8fdf5-543">当安装 Resharper 时，Razor Intellisense 不起作用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-543">Razor Intellisense does not work when Resharper is installed.</span></span> <span data-ttu-id="8fdf5-544">如果你已安装 ReSharper，并且想要充分利用 ASP.NET MVC 3 RC 中的 Razor intellisense 支持，请阅读[此博客文章](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)，其中介绍了如何立即使用它们。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-544">If you have ReSharper installed and want to take advantage of the Razor intellisense support in ASP.NET MVC 3 RC, please read [this blog post](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) from JetBrains which discusses ways to use them together today.</span></span>
- <span data-ttu-id="8fdf5-545">用 ASP.NET MVC 3 的 Beta 版创建的 CSHTML 和 VBHTML 视图没有正确的生成操作，因此不会将其从发布中忽略。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-545">CSHTML and VBHTML views created with Beta of ASP.NET MVC 3 do not have their build action correctly which omits them from publishing.</span></span> <span data-ttu-id="8fdf5-546">应将这些文件的*生成操作*设置为 "内容"。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-546">The *Build Action* for these files should be set to "Content".</span></span> <span data-ttu-id="8fdf5-547">ASP.NET MVC 3 RC 修复了新文件的这一问题，但并不更正使用 Beta 版本创建的项目的现有文件的设置。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-547">ASP.NET MVC 3 RC fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta.</span></span>
- <span data-ttu-id="8fdf5-548">安装程序要完成的时间可能比以前版本的 ASP.NET MVC 长得多，因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-548">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="8fdf5-549">选择 "编辑" 强类型视图时，"添加视图" 基架基架只读属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-549">The Add View scaffolding when selecting an "Edit" strongly typed view scaffolds read only properties.</span></span> <span data-ttu-id="8fdf5-550">同样，只写属性基架用于 "显示" 视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-550">Likewise, write-only properties are scaffolded for "Display" views.</span></span>
- <span data-ttu-id="8fdf5-551">在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-551">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="8fdf5-552">安装 Visual Studio Async CTP 会导致与在 ASP.NET MVC 3 工具安装过程中包含的 Razor 版本发生冲突。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-552">Installing the Visual Studio Async CTP causes a conflict with the Razor release that is included as part of the ASP.NET MVC 3 tooling installation.</span></span> <span data-ttu-id="8fdf5-553">请确保不要在同一台计算机上同时安装 Visual Studio Async CTP 和 Razor 版本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-553">Make sure that you do not try to install both the Visual Studio Async CTP and the Razor release on the same machine.</span></span>
- <span data-ttu-id="8fdf5-554">编辑 Razor 视图（cshtml 文件）时，Visual Studio 中的 "转向控制器" 菜单项将不可用，且没有代码段。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-554">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a><span data-ttu-id="8fdf5-555">ASP.NET MVC 3 Beta</span><span class="sxs-lookup"><span data-stu-id="8fdf5-555">ASP.NET MVC 3 Beta</span></span>

<span data-ttu-id="8fdf5-556">ASP.NET MVC 3 Beta 于2010年10月6日发布。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-556">ASP.NET MVC 3 Beta was released on October 6, 2010.</span></span> <span data-ttu-id="8fdf5-557">以下说明特定于 Beta 版本，并受上述 ASP.NET MVC 3 候选版本部分中提到的任何更新或更改的限制。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-557">The following notes are specific to the Beta release, and are subject to any updates or changes referenced in the ASP.NET MVC 3 Release Candidate section above.</span></span>

## <a id="0.1__Toc274034215"></a><span data-ttu-id="8fdf5-558">New Featuresin ASP.NET MVC 3 Beta</span><span class="sxs-lookup"><span data-stu-id="8fdf5-558">New Featuresin ASP.NET MVC 3 Beta</span></span>

<a id="0.1__Default_validation_system"></a><span data-ttu-id="8fdf5-559">本部分介绍 ASP.NET MVC 3 Beta 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-559">This section describes features that have been introduced in the ASP.NET MVC 3 Beta release.</span></span>

### <a id="0.1__Toc274034216"></a><span data-ttu-id="8fdf5-560">NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="8fdf5-560">NuGet Package Manager</span></span>

<span data-ttu-id="8fdf5-561">ASP.NET MVC 3 包括 NuGet 包管理器，它是一个用于向 Visual Studio 项目添加库和工具的集成包管理工具。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-561">ASP.NET MVC 3 includes NuGet Package Manager, which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="8fdf5-562">大多数情况下，它会自动执行开发人员在源树中获取库所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-562">For the most part, it automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="8fdf5-563">你可以使用 NuGet 作为命令行工具，作为 Visual Studio 2010 内的集成控制台窗口，从 Visual Studio 上下文菜单，以及 PowerShell cmdlet 集。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-563">You can work with NuGet as a command line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as set of PowerShell cmdlets.</span></span>

<span data-ttu-id="8fdf5-564">有关 NuGet 的详细信息，请参阅[Nuget 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-564">For more information about NuGet, read the [NuGet Documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a id="0.1__Toc274034217"></a><span data-ttu-id="8fdf5-565">改进了 "新建项目" 对话框</span><span class="sxs-lookup"><span data-stu-id="8fdf5-565">Improved New Project Dialog Box</span></span>

<span data-ttu-id="8fdf5-566">创建新项目时，"新建项目" 对话框现在允许你指定视图引擎以及 ASP.NET MVC 项目类型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-566">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image6.png)

<span data-ttu-id="8fdf5-567">此版本不包含对修改对话框中列出的模板和视图引擎列表的支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-567">Support for modifying the list of templates and view engines listed in the dialog box is not included in this release.</span></span>

<span data-ttu-id="8fdf5-568">默认模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-568">The default templates are the following:</span></span>

<span data-ttu-id="8fdf5-569">空。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-569">Empty.</span></span> <span data-ttu-id="8fdf5-570">包含 ASP.NET MVC 项目的一组最小文件，其中包括 ASP.NET MVC 项目的默认目录结构、包含默认 ASP.NET MVC 样式的小 MVC 文件和包含默认 JavaScript 文件的脚本目录。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-570">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a small Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="8fdf5-571">Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-571">Internet Application.</span></span> <span data-ttu-id="8fdf5-572">包含演示如何在 ASP.NET MVC 内使用成员资格提供程序的示例功能。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-572">Contains sample functionality that demonstrates how to use the membership provider within ASP.NET MVC.</span></span>

### <a id="0.1__Toc274034218"></a><span data-ttu-id="8fdf5-573">在 Razor 视图中指定强类型模型的简化方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-573">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>

<span data-ttu-id="8fdf5-574">为类型强类型的 Razor 视图指定模型类型的方式已通过使用适用于 CSHTML 视图的 new @model 指令和用于 VBHTML 视图的 @ModelType 指令进行了简化。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-574">The way to specify the model type for strongly typed Razor views has been simplified by using the new @model directive for CSHTML views and @ModelType directive for VBHTML views.</span></span> <span data-ttu-id="8fdf5-575">在早期版本的 ASP.NET MVC 中，你将以这种方式为 Razor 视图指定强类型模型：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-575">In earlier versions of ASP.NET MVC, you would specify a strongly typed model for Razor views this way:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

<span data-ttu-id="8fdf5-576">在此版本中，可以使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-576">In this release, you can use the following syntax:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a><span data-ttu-id="8fdf5-577">支持新的 ASP.NET 网页帮助器方法</span><span class="sxs-lookup"><span data-stu-id="8fdf5-577">Support for New ASP.NET Web Pages Helper Methods</span></span>

<span data-ttu-id="8fdf5-578">新的 ASP.NET 网页技术包括一组帮助器方法，这些方法可用于将常用功能添加到视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-578">The new ASP.NET Web Pages technology includes a set of helper methods that are useful for adding commonly used functionality to views and controllers.</span></span> <span data-ttu-id="8fdf5-579">ASP.NET MVC 3 支持在控制器和视图中使用这些帮助器方法（如果适用）。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-579">ASP.NET MVC 3 supports using these helper methods within controllers and views (where appropriate).</span></span> <span data-ttu-id="8fdf5-580">这些方法包含在 System.web. 助手程序集中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-580">These methods are contained in the System.Web.Helpers assembly.</span></span> <span data-ttu-id="8fdf5-581">下表列出了几个 ASP.NET 网页帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-581">The following table lists a few of the ASP.NET Web Pages helper methods.</span></span>

| <span data-ttu-id="8fdf5-582">**Helper**</span><span class="sxs-lookup"><span data-stu-id="8fdf5-582">**Helper**</span></span> | <span data-ttu-id="8fdf5-583">**描述**</span><span class="sxs-lookup"><span data-stu-id="8fdf5-583">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8fdf5-584">Chart</span><span class="sxs-lookup"><span data-stu-id="8fdf5-584">Chart</span></span> | <span data-ttu-id="8fdf5-585">在视图中呈现图表。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-585">Renders a chart within a view.</span></span> <span data-ttu-id="8fdf5-586">包含诸如 ToWebImage、Chart 和 Chart 等方法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-586">Contains methods such as Chart.ToWebImage, Chart.Save, and Chart.Write.</span></span> |
| <span data-ttu-id="8fdf5-587">加密</span><span class="sxs-lookup"><span data-stu-id="8fdf5-587">Crypto</span></span> | <span data-ttu-id="8fdf5-588">使用哈希算法来创建正确的加盐和哈希密码。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-588">Uses hashing algorithms to create properly salted and hashed passwords.</span></span> |
| <span data-ttu-id="8fdf5-589">WebGrid</span><span class="sxs-lookup"><span data-stu-id="8fdf5-589">WebGrid</span></span> | <span data-ttu-id="8fdf5-590">以网格的形式呈现对象（通常为数据库中的数据）的集合。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-590">Renders a collection of objects (typically, data from a database) as a grid.</span></span> <span data-ttu-id="8fdf5-591">支持分页和排序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-591">Supports paging and sorting.</span></span> |
| <span data-ttu-id="8fdf5-592">WebImage</span><span class="sxs-lookup"><span data-stu-id="8fdf5-592">WebImage</span></span> | <span data-ttu-id="8fdf5-593">呈现图像。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-593">Renders an image.</span></span> |
| <span data-ttu-id="8fdf5-594">WebMail</span><span class="sxs-lookup"><span data-stu-id="8fdf5-594">WebMail</span></span> | <span data-ttu-id="8fdf5-595">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-595">Sends an email message.</span></span> |

<span data-ttu-id="8fdf5-596">以下 URL 中的 ASP.NET Razor 语法文档中提供了列出帮助程序和基本语法的快速参考主题：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-596">A quick reference topic that lists the helpers and basic syntax is available as part of the ASP.NET Razor syntax documentation at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a><span data-ttu-id="8fdf5-597">其他依赖关系注入支持</span><span class="sxs-lookup"><span data-stu-id="8fdf5-597">Additional Dependency Injection Support</span></span>

<span data-ttu-id="8fdf5-598">当前版本是在 ASP.NET MVC 3 预览版1版本的基础上生成的，它包括对两个新服务和四个现有服务的额外支持，并改进了对依赖项解析和常见服务定位符的支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-598">Building on the ASP.NET MVC 3 Preview 1 release, the current release includes added support for two new services and four existing services, and improved support for dependency resolution and the Common Service Locator.</span></span>

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a><span data-ttu-id="8fdf5-599">用于细化控制器实例化的新的 IControllerActivator 接口</span><span class="sxs-lookup"><span data-stu-id="8fdf5-599">New IControllerActivator Interface for Fine-Grained Controller Instantiation</span></span>

<span data-ttu-id="8fdf5-600">新的 IControllerActivator 接口可更精细地控制通过依赖关系注入来实例化控制器的方式。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-600">The new IControllerActivator interface provides more fine-grained control over how controllers are instantiated via dependency injection.</span></span> <span data-ttu-id="8fdf5-601">下面的示例演示了接口：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-601">The following example shows the interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

<span data-ttu-id="8fdf5-602">这与控制器工厂的角色比较。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-602">Contrast this to the role of the controller factory.</span></span> <span data-ttu-id="8fdf5-603">控制器工厂是 IControllerFactory 接口的实现，该接口负责定位控制器类型并实例化该控制器类型的实例。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-603">A controller factory is an implementation of the IControllerFactory interface, which is responsible both for locating a controller type and for instantiating an instance of that controller type.</span></span>

<span data-ttu-id="8fdf5-604">控制器激活程序只负责实例化控制器类型的实例。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-604">Controller activators are responsible only for instantiating an instance of a controller type.</span></span> <span data-ttu-id="8fdf5-605">它们不执行控制器类型查找。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-605">They do not perform the controller type lookup.</span></span> <span data-ttu-id="8fdf5-606">找到正确的控制器类型后，控制器工厂应委托给 IControllerActivator 的实例以处理控制器的实际实例化。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-606">After locating a proper controller type, controller factories should delegate to an instance of IControllerActivator to handle the actual instantiation of the controller.</span></span>

<span data-ttu-id="8fdf5-607">DefaultControllerFactory 类具有接受 IControllerFactory 实例的新构造函数。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-607">The DefaultControllerFactory class has a new constructor that accepts an IControllerFactory instance.</span></span> <span data-ttu-id="8fdf5-608">这使你可以应用依赖关系注入来管理控制器创建的这个方面，而无需覆盖默认的控制器类型查找行为。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-608">This lets you apply Dependency Injection to manage this aspect of controller creation without having to override the default controller-type lookup behavior.</span></span>

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a><span data-ttu-id="8fdf5-609">Iservicelocator.getinstance 接口已替换为 IDependencyResolver</span><span class="sxs-lookup"><span data-stu-id="8fdf5-609">IServiceLocator Interface Replaced with IDependencyResolver</span></span>

<span data-ttu-id="8fdf5-610">根据社区反馈，ASP.NET MVC 3 Beta 版本已将 Iservicelocator.getinstance 接口的使用替换为特定于 ASP.NET MVC 需求的简化 IDependencyResolver 接口。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-610">Based on community feedback, the ASP.NET MVC 3 Beta release has replaced the use of the IServiceLocator interface with a slimmed-down IDependencyResolver interface specific to the needs of ASP.NET MVC.</span></span> <span data-ttu-id="8fdf5-611">下面的示例演示了新的接口：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-611">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

<span data-ttu-id="8fdf5-612">作为此更改的一部分，ServiceLocator 类也被替换为 DependencyResolver 类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-612">As part of this change, the ServiceLocator class was also replaced with the DependencyResolver class.</span></span> <span data-ttu-id="8fdf5-613">依赖关系解析程序的注册类似于早期版本的 ASP.NET MVC：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-613">Registration of a dependency resolver is similar to earlier versions of ASP.NET MVC:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

<span data-ttu-id="8fdf5-614">此接口的实现应只委托到基础依赖关系注入容器，以便为请求的类型提供注册的服务。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-614">Implementations of this interface should simply delegate to the underlying dependency injection container to provide the registered service for the requested type.</span></span>

<span data-ttu-id="8fdf5-615">当没有所请求类型的注册服务时，ASP.NET MVC 需要此接口的实现以从 GetService 返回 null，并从 GetServices 返回一个空集合。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-615">When there are no registered services of the requested type, ASP.NET MVC expects implementations of this interface to return null from GetService and to return an empty collection from GetServices.</span></span>

<span data-ttu-id="8fdf5-616">新的 DependencyResolver 类允许注册实现新的 IDependencyResolver 接口或公共服务定位器接口（Iservicelocator.getinstance）的类。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-616">The new DependencyResolver class lets you register classes that implement either the new IDependencyResolver interface or the Common Service Locator interface (IServiceLocator).</span></span> <span data-ttu-id="8fdf5-617">有关常见服务定位符的详细信息，请参阅[GitHub 上的 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-617">For more information about Common Service Locator, see [CommonServiceLocator on GitHub](https://github.com/unitycontainer/commonservicelocator).</span></span>

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a><span data-ttu-id="8fdf5-618">用于细化视图页面实例化的新 IViewActivator 界面</span><span class="sxs-lookup"><span data-stu-id="8fdf5-618">New IViewActivator Interface for Fine-Grained View Page Instantiation</span></span>

<span data-ttu-id="8fdf5-619">新的 IViewPageActivator 接口可更精细地控制通过依赖关系注入来实例化视图页面的方式。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-619">The new IViewPageActivator interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="8fdf5-620">这同时适用于 WebFormView 实例和 RazorView 实例。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-620">This applies to both WebFormView instances and RazorView instances.</span></span> <span data-ttu-id="8fdf5-621">下面的示例演示了新的接口：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-621">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

<span data-ttu-id="8fdf5-622">这些类现在接受 IViewPageActivator 构造函数参数，该参数允许你使用依赖关系注入来控制如何实例化 ViewPage、ViewUserControl 和 WebViewPage 类型。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-622">These classes now accept an IViewPageActivator constructor argument, which lets you use dependency injection to control how the ViewPage, ViewUserControl, and WebViewPage types are instantiated.</span></span>

#### <a name="new-dependency-resolver-support-for-existing-services"></a><span data-ttu-id="8fdf5-623">新的依赖关系解析程序支持现有服务</span><span class="sxs-lookup"><span data-stu-id="8fdf5-623">New Dependency Resolver Support for Existing Services</span></span>

<span data-ttu-id="8fdf5-624">新版本包括对以下服务的依赖关系解析支持：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-624">The new release includes dependency resolution support for the following services:</span></span>

- <span data-ttu-id="8fdf5-625">模型验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-625">Model validation providers.</span></span> <span data-ttu-id="8fdf5-626">可在依赖关系解析程序中注册实现 ModelValidatorProvider 的类，系统会将这些类用于支持客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-626">Classes that implement ModelValidatorProvider can be registered in the dependency resolver, and the system will use them to support client- and server-side validation.</span></span>
- <span data-ttu-id="8fdf5-627">模型元数据提供程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-627">Model metadata provider.</span></span> <span data-ttu-id="8fdf5-628">可在依赖关系解析程序中注册实现 ModelMetadataProvider 的单一类，系统会将其用于为模板化和验证系统提供元数据。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-628">A single class that implements ModelMetadataProvider can be registered in the dependency resolver, and the system will use it to provide metadata for the templating and validation systems.</span></span>
- <span data-ttu-id="8fdf5-629">值提供程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-629">Value providers.</span></span> <span data-ttu-id="8fdf5-630">可在依赖关系解析程序中注册实现 ValueProviderFactory 的类，系统将使用这些类来创建在模型绑定期间由控制器使用的值提供程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-630">Classes that implement ValueProviderFactory can be registered in the dependency resolver, and the system will use them to create value providers that are consumed by the controller and during model binding.</span></span>
- <span data-ttu-id="8fdf5-631">模型联编。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-631">Model binders.</span></span> <span data-ttu-id="8fdf5-632">可在依赖关系解析程序中注册实现 IModelBinderProvider 的类，系统将使用这些类来创建模型绑定系统所使用的模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-632">Classes that implement IModelBinderProvider can be registered in the dependency resolver, and the system will use them to create model binders that are consumed by the model binding system.</span></span>

### <a id="0.1__Toc274034221"></a><span data-ttu-id="8fdf5-633">新支持基于 jQuery 的非引人注目 Ajax</span><span class="sxs-lookup"><span data-stu-id="8fdf5-633">New Support for Unobtrusive jQuery-Based Ajax</span></span>

<span data-ttu-id="8fdf5-634">ASP.NET MVC 包含 Ajax helper 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-634">ASP.NET MVC includes Ajax helper methods such as the following:</span></span>

- <span data-ttu-id="8fdf5-635">Ajax.ActionLink</span><span class="sxs-lookup"><span data-stu-id="8fdf5-635">Ajax.ActionLink</span></span>
- <span data-ttu-id="8fdf5-636">Ajax.RouteLink</span><span class="sxs-lookup"><span data-stu-id="8fdf5-636">Ajax.RouteLink</span></span>
- <span data-ttu-id="8fdf5-637">Ajax.BeginForm</span><span class="sxs-lookup"><span data-stu-id="8fdf5-637">Ajax.BeginForm</span></span>
- <span data-ttu-id="8fdf5-638">Ajax.BeginRouteForm</span><span class="sxs-lookup"><span data-stu-id="8fdf5-638">Ajax.BeginRouteForm</span></span>

<span data-ttu-id="8fdf5-639">这些方法使用 JavaScript 在服务器上调用操作方法，而不是使用完全回发。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-639">These methods use JavaScript to invoke an action method on the server rather than using a full postback.</span></span> <span data-ttu-id="8fdf5-640">此功能已更新，以不引人注目的方式利用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-640">This functionality has been updated to take advantage of jQuery in an unobtrusive manner.</span></span> <span data-ttu-id="8fdf5-641">这些帮助器方法使用*数据 ajax*前缀发出 HTML5 特性，而不是 intrusively 发出内联客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-641">Rather than intrusively emitting inline client scripts, these helper methods separate the behavior from the markup by emitting HTML5 attributes using the *data-ajax* prefix.</span></span> <span data-ttu-id="8fdf5-642">然后，通过引用相应的 JavaScript 文件，将行为应用到标记。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-642">Behavior is then applied to the markup by referencing the appropriate JavaScript files.</span></span> <span data-ttu-id="8fdf5-643">请确保引用以下 JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-643">Make sure that the following JavaScript files are referenced:</span></span>

- <span data-ttu-id="8fdf5-644">jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="8fdf5-644">jquery-1.4.1.js</span></span>
- <span data-ttu-id="8fdf5-645">jquery.unobtrusive.ajax.js</span><span class="sxs-lookup"><span data-stu-id="8fdf5-645">jquery.unobtrusive.ajax.js</span></span>

<span data-ttu-id="8fdf5-646">默认情况下，在 ASP.NET MVC 3 新项目模板中的 web.config 文件中启用此功能，但对于现有项目，默认情况下已禁用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-646">This feature is enabled by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="8fdf5-647">有关详细信息，请参阅本文档后面的[为客户端验证和非引人注目的 JavaScript 添加应用程序范围标志](#0.1_AddedApplicationWideFlagsForClientValida)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-647">For more information, see [Added application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

### <a id="0.1__Toc274034222"></a><span data-ttu-id="8fdf5-648">新支持非引人注目的 jQuery 验证</span><span class="sxs-lookup"><span data-stu-id="8fdf5-648">New Support for Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="8fdf5-649">默认情况下，ASP.NET MVC 3 Beta 以不引人注目的方式使用 jQuery 验证来执行客户端验证。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-649">By default, ASP.NET MVC 3 Beta uses jQuery validation in an unobtrusive manner in order to perform client-side validation.</span></span> <span data-ttu-id="8fdf5-650">若要启用非介入式客户端验证，请在视图中执行类似于下面的调用：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-650">To enable unobtrusive client validation, make a call like the following from within a view:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

<span data-ttu-id="8fdf5-651">这需要将 ViewContext 属性设置为 true，通过进行以下调用，可以执行此操作：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-651">This requires that ViewContext.UnobtrusiveJavaScriptEnabled property is set to true, which you can do by making the following call:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

<span data-ttu-id="8fdf5-652">此外，请确保引用以下 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-652">Also make sure the following JavaScript files are referenced.</span></span>

- <span data-ttu-id="8fdf5-653">jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="8fdf5-653">jquery-1.4.1.js</span></span>
- <span data-ttu-id="8fdf5-654">jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="8fdf5-654">jquery.validate.js</span></span>
- <span data-ttu-id="8fdf5-655">jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="8fdf5-655">jquery.validate.unobtrusive.js</span></span>

<span data-ttu-id="8fdf5-656">默认情况下，在 ASP.NET MVC 3 新项目模板中的 web.config 文件中启用此功能，但对于现有项目，默认情况下已禁用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-656">This feature is enabled on by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="8fdf5-657">有关详细信息，请参阅本文档后面的[用于客户端验证和非引人注目 JavaScript 的新应用程序范围标志](#0.1_AddedApplicationWideFlagsForClientValida)。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-657">For more information, see [New application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a><span data-ttu-id="8fdf5-658">适用于客户端验证和非引人注目 JavaScript 的新应用程序范围标志</span><span class="sxs-lookup"><span data-stu-id="8fdf5-658">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>

<span data-ttu-id="8fdf5-659">可以使用 HtmlHelper 类的静态成员全局启用或禁用客户端验证和非引人注目的 JavaScript，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-659">You can enable or disable client validation and unobtrusive JavaScript globally using static members of the HtmlHelper class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

<span data-ttu-id="8fdf5-660">默认情况下，默认项目模板启用非引人注目的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-660">The default project templates enable unobtrusive JavaScript by default.</span></span> <span data-ttu-id="8fdf5-661">你还可以使用以下设置在应用程序的根 web.config 文件中启用或禁用这些功能：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-661">You can also enable or disable these features in the root Web.config file of your application using the following settings:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

<span data-ttu-id="8fdf5-662">由于可以在默认情况下启用这些功能，因此会向 HtmlHelper 类引入新的重载，以允许你重写默认设置，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-662">Because you can enable these features by default, new overloads were introduced to the HtmlHelper class that let you override the default settings, as shown in the following examples:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

<span data-ttu-id="8fdf5-663">为了向后兼容，默认情况下，这两种功能都处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-663">For backward compatibility, both of these features are disabled by default.</span></span>

### <a id="0.1__Toc274034224"></a><span data-ttu-id="8fdf5-664">新支持在视图运行之前运行的代码</span><span class="sxs-lookup"><span data-stu-id="8fdf5-664">New Support for Code that Runs Before Views Run</span></span>

<span data-ttu-id="8fdf5-665">你现在可以将名为 \_viewstart.cshtml （或 \_viewstart.cshtml）的文件放在 Views 目录中，并向其添加将在该目录及其子目录中的多个视图之间共享的代码。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-665">You can now put a file named \_viewstart.cshtml (or \_viewstart.vbhtml) in the Views directory and add code to it that will be shared among multiple views in that directory and its subdirectories.</span></span> <span data-ttu-id="8fdf5-666">例如，可以将以下代码放入 ~/Views 文件夹中的 \_viewstart.cshtml 页面：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-666">For example, you might put the following code into the \_viewstart.cshtml page in the ~/Views folder:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

<span data-ttu-id="8fdf5-667">这会在 Views 文件夹及其所有子文件夹中以递归方式设置每个视图的布局页。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-667">This sets the layout page for every view within the Views folder and all its subfolders recursively.</span></span> <span data-ttu-id="8fdf5-668">呈现视图时，\_viewstart.cshtml 文件中的代码在视图代码运行之前运行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-668">When a view is being rendered, the code in the \_viewstart.cshtml file runs before the view code runs.</span></span> <span data-ttu-id="8fdf5-669">\_viewstart.cshtml 代码适用于该文件夹中的每个视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-669">The \_viewstart.cshtml code applies to every view in that folder.</span></span>

<span data-ttu-id="8fdf5-670">默认情况下，\_viewstart.cshtml 文件中的代码也适用于任何子文件夹中的视图。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-670">By default, the code in the \_viewstart.cshtml file also applies to views in any subfolder.</span></span> <span data-ttu-id="8fdf5-671">但是，各个子文件夹可以具有其自己的 \_viewstart.cshtml 文件版本;在这种情况下，本地版本优先。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-671">However, individual subfolders can have their own version of the \_viewstart.cshtml file; in that case, the local version takes precedence.</span></span> <span data-ttu-id="8fdf5-672">例如，若要运行 HomeController 的所有视图通用的代码，请在 ~/Views/Home 文件夹中放置一个 \_viewstart.cshtml 文件。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-672">For example, to run code that is common to all views for the HomeController, put a \_viewstart.cshtml file in the ~/Views/Home folder.</span></span>

### <a id="0.1__Toc274034225"></a><span data-ttu-id="8fdf5-673">新的对 VBHTML Razor 语法的支持</span><span class="sxs-lookup"><span data-stu-id="8fdf5-673">New Support for the VBHTML Razor Syntax</span></span>

<span data-ttu-id="8fdf5-674">上一个 ASP.NET MVC 预览包括对使用基于的 Razor 语法的视图C#的支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-674">The previous ASP.NET MVC preview included support for views using Razor syntax based on C#.</span></span> <span data-ttu-id="8fdf5-675">这些视图使用 # 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-675">These views use the .cshtml file extension.</span></span> <span data-ttu-id="8fdf5-676">作为支持 Razor 的日常工作的一部分，ASP.NET MVC 3 Beta 引入了对 Visual Basic 中的 Razor 语法的支持，该文件使用了文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-676">As part of ongoing work to support Razor, the ASP.NET MVC 3 Beta introduces support for the Razor syntax in Visual Basic, which uses the .vbhtml file extension.</span></span>

<span data-ttu-id="8fdf5-677">有关在 VBHTML 页中使用 Visual Basic 语法的介绍，请参阅以下 URL 中的教程：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-677">For an introduction to using Visual Basic syntax in VBHTML pages, see the tutorial at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a><span data-ttu-id="8fdf5-678">更精细地控制 ValidateInputAttribute</span><span class="sxs-lookup"><span data-stu-id="8fdf5-678">More Granular Control over ValidateInputAttribute</span></span>

<span data-ttu-id="8fdf5-679">ASP.NET MVC 始终包含 ValidateInputAttribute 类，该类调用核心 ASP.NET 请求验证基础结构，以确保传入请求不包含可能的恶意输入。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-679">ASP.NET MVC has always included the ValidateInputAttribute class, which invokes the core ASP.NET request validation infrastructure to make sure that the incoming request does not contain potentially malicious input.</span></span> <span data-ttu-id="8fdf5-680">默认情况下，输入验证处于启用状态。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-680">By default, input validation is enabled.</span></span> <span data-ttu-id="8fdf5-681">可以通过使用 ValidateInputAttribute 属性来禁用请求验证，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-681">It is possible to disable request validation by using the ValidateInputAttribute attribute, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

<span data-ttu-id="8fdf5-682">但是，许多 web 应用程序都有需要允许 HTML 的单独窗体字段，而其余字段不应。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-682">However, many web applications have individual form fields that need to allow HTML, while the remaining fields should not.</span></span> <span data-ttu-id="8fdf5-683">ValidateInputAttribute 类现在允许你指定不应包含在请求验证中的字段的列表。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-683">The ValidateInputAttribute class now lets you specify a list of fields that should not be included in request validation.</span></span>

<span data-ttu-id="8fdf5-684">例如，如果您正在开发博客引擎，则您可能希望在 "正文" 和 "摘要" 字段中允许标记。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-684">For example, if you are developing a blog engine, you might want to allow markup in the Body and Summary fields.</span></span> <span data-ttu-id="8fdf5-685">这些字段可能由两个输入元素表示，每个元素都具有与属性名称（"Body" 和 "Summary"）对应的 name 属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-685">These fields might be represented by two input element, each with a name attribute corresponding to the property name ("Body" and "Summary").</span></span> <span data-ttu-id="8fdf5-686">若要仅对这些字段禁用请求验证，请在 ValidateInput 类的 Exclude 属性中指定名称（以逗号分隔），如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-686">To disable request validation for these fields only, specify the names (comma-separated) in the Exclude property of the ValidateInput class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a><span data-ttu-id="8fdf5-687">帮助器将下划线转换为使用匿名对象指定的 HTML 属性名称的连字符</span><span class="sxs-lookup"><span data-stu-id="8fdf5-687">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>

<span data-ttu-id="8fdf5-688">使用 Helper 方法，你可以使用匿名对象指定属性名称/值对，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-688">Helper methods let you specify attribute name/value pairs using an anonymous object, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

<span data-ttu-id="8fdf5-689">此方法不允许在属性名称中使用连字符，因为连字符不能用于 ASP.NET 中的属性名称。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-689">This approach doesn't let you use hyphens in the attribute name, because a hyphen cannot be used for a property name in ASP.NET.</span></span> <span data-ttu-id="8fdf5-690">但是，连字符对于自定义 HTML5 特性非常重要;例如，HTML5 使用 "data-" 前缀。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-690">However, hyphens are important for custom HTML5 attributes; for example, HTML5 uses the "data-" prefix.</span></span>

<span data-ttu-id="8fdf5-691">同时，下划线不能用于 HTML 中的属性名称，但在属性名称内有效。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-691">At the same time, underscores cannot be used for attribute names in HTML, but are valid within property names.</span></span> <span data-ttu-id="8fdf5-692">因此，如果使用匿名对象指定属性，并且属性名称包含下划线，则 helper 方法会将下划线转换为连字符。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-692">Therefore, if you specify attributes using an anonymous object, and if the attribute names include an underscore,, helper methods will convert the underscores to hyphens.</span></span> <span data-ttu-id="8fdf5-693">例如，以下 helper 语法使用下划线：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-693">For example, the following helper syntax uses an underscore:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

<span data-ttu-id="8fdf5-694">当 helper 运行时，上面的示例将呈现以下标记：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-694">The previous example renders the following markup when the helper runs:</span></span>

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a><span data-ttu-id="8fdf5-695">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="8fdf5-695">Bug Fixes</span></span>

<span data-ttu-id="8fdf5-696">Html.editorfor 和 DisplayFor 模板帮助器的默认对象模板现在支持在 DisplayAttribute 属性中指定的顺序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-696">The default object template for the EditorFor and DisplayFor template helpers now supports the ordering specified in the DisplayAttribute.Order property.</span></span> <span data-ttu-id="8fdf5-697">（在以前的版本中，未使用 Order 设置。）</span><span class="sxs-lookup"><span data-stu-id="8fdf5-697">(In previous versions, the Order setting was not used.)</span></span>

<span data-ttu-id="8fdf5-698">客户端验证现在支持验证应用了验证属性的重写属性。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-698">Client validation now supports validation of overridden properties that have validation attributes applied.</span></span>

<span data-ttu-id="8fdf5-699">默认情况下，JsonValueProviderFactory 已注册。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-699">JsonValueProviderFactory is now registered by default.</span></span>

## <a id="0.1__Toc274034229"></a><span data-ttu-id="8fdf5-700">重大更改</span><span class="sxs-lookup"><span data-stu-id="8fdf5-700">Breaking Changes</span></span>

<span data-ttu-id="8fdf5-701">对于具有相同顺序值的异常筛选器，异常筛选器的执行顺序已更改。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-701">The order of execution for exception filters has changed for exception filters that have the same Order value.</span></span> <span data-ttu-id="8fdf5-702">在 ASP.NET MVC 2 及更早版本中，与操作方法上的异常筛选器顺序相同的异常筛选器在操作方法上的异常筛选器之前执行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-702">In ASP.NET MVC 2 and earlier, exception filters on the controller with the same Order as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="8fdf5-703">如果未指定顺序值应用了异常筛选器，通常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-703">This would typically be the case when exception filters were applied without a specified Order value.</span></span> <span data-ttu-id="8fdf5-704">在 ASP.NET MVC 3 中，此顺序已反转，以便首先执行最具体的异常处理程序。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-704">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="8fdf5-705">与早期版本一样，如果显式指定 Order 属性，则筛选器将按指定顺序运行。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-705">As in earlier versions, if the Order property is explicitly specified, the filters are run in the specified order.</span></span>

## <a id="0.1__Toc274034230"></a>  <span data-ttu-id="8fdf5-706">已知问题</span><span class="sxs-lookup"><span data-stu-id="8fdf5-706">Known Issues</span></span>

<span data-ttu-id="8fdf5-707">在安装过程中，EULA 接受对话框在一个小于预期的窗口中显示许可条款。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-707">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>

<span data-ttu-id="8fdf5-708">Razor 视图没有 IntelliSense 支持或突出显示语法。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-708">Razor views do not have IntelliSense support nor syntax highlighting.</span></span> <span data-ttu-id="8fdf5-709">预计在 Visual Studio 中对 Razor 语法的支持将包含在更高版本中。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-709">It is anticipated that support for Razor syntax in Visual Studio will be included as part of a later release.</span></span>

<span data-ttu-id="8fdf5-710">编辑 Razor 视图（CSHTML 文件）时，Visual Studio 中的<a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a> "前往控制器" 菜单项将不可用，且没有代码段。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-710">When you are editing a Razor view (CSHTML file), the <a id="0.1__Toc224729061"></a><a id="0.1__Toc238051347"></a> Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<span data-ttu-id="8fdf5-711">使用 @model 语法指定强类型的 CSHTML 视图时，将无法识别类型的语言特定的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-711">When using the @model syntax to specify a strongly typed CSHTML view, language-specific shortcuts for types are not recognized.</span></span> <span data-ttu-id="8fdf5-712">例如，@model int 将不起作用，但 @model Int32 将起作用。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-712">For example, @model int will not work, but @model Int32 will work.</span></span> <span data-ttu-id="8fdf5-713">此错误的解决方法是在指定模型类型时使用实际的类型名称。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-713">The workaround for this bug is to use the actual type name when you specify the model type.</span></span>

<span data-ttu-id="8fdf5-714">使用 @model 语法指定强类型的 CSHTML 视图时（或 @ModelType 指定强类型的 VBHTML 视图）时，不支持可以为 null 的类型和数组声明。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-714">When using the @model syntax to specify a strongly typed CSHTML view (or @ModelType to specify a strongly typed VBHTML view), nullable types and array declarations are not supported.</span></span> <span data-ttu-id="8fdf5-715">例如，@model int？不受支持。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-715">For example, @model int? is not supported.</span></span> <span data-ttu-id="8fdf5-716">请改用 `@model Nullable<Int32>`。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-716">Instead, use `@model Nullable<Int32>`.</span></span> <span data-ttu-id="8fdf5-717">也不支持语法 @model string [];请改用 `@model IList<string>`。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-717">The syntax @model string[] is also not supported; instead, use `@model IList<string>`.</span></span>

<span data-ttu-id="8fdf5-718">将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 时，请确保将以下内容添加到 web.config 文件的 appSettings 节：</span><span class="sxs-lookup"><span data-stu-id="8fdf5-718">When you upgrade an ASP.NET MVC 2 project to ASP.NET MVC 3, make sure to add the following to the appSettings section of the Web.config file:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

<span data-ttu-id="8fdf5-719">存在一个已知问题，导致 Forms 身份验证始终将未经身份验证的用户重定向到 ~/Account/Login，忽略 Web.config 中使用的窗体身份验证设置。解决方法是添加以下应用设置。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-719">There's a known issue that causes Forms Authentication to always redirect unauthenticated users to ~/Account/Login, ignoring the forms authentication setting used in Web.config. The workaround is to add the following app setting.</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a><span data-ttu-id="8fdf5-720">否认</span><span class="sxs-lookup"><span data-stu-id="8fdf5-720">Disclaimer</span></span>

<span data-ttu-id="8fdf5-721">© 2011 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-721">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="8fdf5-722">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-722">All rights reserved.</span></span> <span data-ttu-id="8fdf5-723">本文档“按原样”提供。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-723">This document is provided "as-is."</span></span> <span data-ttu-id="8fdf5-724">本文档中的信息和表达的观点，包括 URL 和其他 Internet 网站引用，如有更改恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-724">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span> <span data-ttu-id="8fdf5-725">您自行承担其使用风险。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-725">You bear the risk of using it.</span></span>

<span data-ttu-id="8fdf5-726">本文档未向您提供任何 Microsoft 产品中任何知识产权的任何合法权利。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-726">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="8fdf5-727">您可为了内部参考目的复制和使用本文档。</span><span class="sxs-lookup"><span data-stu-id="8fdf5-727">You may copy and use this document for your internal, reference purposes.</span></span>
