---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 开发概述 |Microsoft Docs
author: rick-anderson
description: 本文档概述了 the.NET Framework 4 和 Visual Studio 2010 中包含的 ASP.NET 的许多新功能。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: ecde48f6bd88ee5f569bfeb8b70c26a50bc869c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511430"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="ee087-103">ASP.NET 4 和 Visual Studio 2010 Web 开发概述</span><span class="sxs-lookup"><span data-stu-id="ee087-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>

> <span data-ttu-id="ee087-104">本文档概述了 the.NET Framework 4 和 Visual Studio 2010 中包含的 ASP.NET 的许多新功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="ee087-105">下载此白皮书</span><span class="sxs-lookup"><span data-stu-id="ee087-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

<span data-ttu-id="ee087-106">**内容**</span><span class="sxs-lookup"><span data-stu-id="ee087-106">**Contents**</span></span>

<span data-ttu-id="ee087-107">**[核心服务](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="ee087-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
[<span data-ttu-id="ee087-108">Web.config 文件重构</span><span class="sxs-lookup"><span data-stu-id="ee087-108">Web.config File Refactoring</span></span>](#0.2__Toc253429239 "_Toc253429239")  
[<span data-ttu-id="ee087-109">可扩展的输出缓存</span><span class="sxs-lookup"><span data-stu-id="ee087-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="ee087-110">自动启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="ee087-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="ee087-111">永久重定向页面</span><span class="sxs-lookup"><span data-stu-id="ee087-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="ee087-112">收缩会话状态</span><span class="sxs-lookup"><span data-stu-id="ee087-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="ee087-113">展开允许的 Url 范围</span><span class="sxs-lookup"><span data-stu-id="ee087-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="ee087-114">可扩展请求验证</span><span class="sxs-lookup"><span data-stu-id="ee087-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="ee087-115">对象缓存和对象缓存扩展性</span><span class="sxs-lookup"><span data-stu-id="ee087-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="ee087-116">可扩展的 HTML、URL 和 HTTP 标头编码</span><span class="sxs-lookup"><span data-stu-id="ee087-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="ee087-117">单个工作进程中单个应用程序的性能监视</span><span class="sxs-lookup"><span data-stu-id="ee087-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="ee087-118">多目标</span><span class="sxs-lookup"><span data-stu-id="ee087-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="ee087-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="ee087-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="ee087-120">Web 窗体和 MVC 中包含的 jQuery</span><span class="sxs-lookup"><span data-stu-id="ee087-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="ee087-121">内容交付网络支持</span><span class="sxs-lookup"><span data-stu-id="ee087-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="ee087-122">ScriptManager 显式脚本</span><span class="sxs-lookup"><span data-stu-id="ee087-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="ee087-123">**[Web 窗体](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="ee087-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="ee087-124">用 MetaKeywords 和 MetaDescription 属性设置 Meta 标记</span><span class="sxs-lookup"><span data-stu-id="ee087-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="ee087-125">启用各个控件的视图状态</span><span class="sxs-lookup"><span data-stu-id="ee087-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="ee087-126">对浏览器功能的更改</span><span class="sxs-lookup"><span data-stu-id="ee087-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="ee087-127">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="ee087-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="ee087-128">设置客户端 Id</span><span class="sxs-lookup"><span data-stu-id="ee087-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="ee087-129">保持数据控件中的行选择</span><span class="sxs-lookup"><span data-stu-id="ee087-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="ee087-130">ASP.NET 图表控件</span><span class="sxs-lookup"><span data-stu-id="ee087-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="ee087-131">用 QueryExtender 控件筛选数据</span><span class="sxs-lookup"><span data-stu-id="ee087-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="ee087-132">Html 编码的代码表达式</span><span class="sxs-lookup"><span data-stu-id="ee087-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="ee087-133">项目模板更改</span><span class="sxs-lookup"><span data-stu-id="ee087-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="ee087-134">CSS 改进</span><span class="sxs-lookup"><span data-stu-id="ee087-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="ee087-135">在隐藏字段周围隐藏 div 元素</span><span class="sxs-lookup"><span data-stu-id="ee087-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="ee087-136">为模板化控件呈现外部表</span><span class="sxs-lookup"><span data-stu-id="ee087-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="ee087-137">ListView 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="ee087-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="ee087-138">CheckBoxList 和 RadioButtonList 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="ee087-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="ee087-139">菜单控件改进</span><span class="sxs-lookup"><span data-stu-id="ee087-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="ee087-140">Wizard 和 CreateUserWizard 控件56</span><span class="sxs-lookup"><span data-stu-id="ee087-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="ee087-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="ee087-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="ee087-142">区域支持</span><span class="sxs-lookup"><span data-stu-id="ee087-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="ee087-143">数据-批注属性验证支持</span><span class="sxs-lookup"><span data-stu-id="ee087-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="ee087-144">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="ee087-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="ee087-145">**[动态数据](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="ee087-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="ee087-146">为现有项目启用动态数据</span><span class="sxs-lookup"><span data-stu-id="ee087-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="ee087-147">声明性 DynamicDataManager 控件语法</span><span class="sxs-lookup"><span data-stu-id="ee087-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="ee087-148">实体模板</span><span class="sxs-lookup"><span data-stu-id="ee087-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="ee087-149">Url 和电子邮件地址的新字段模板</span><span class="sxs-lookup"><span data-stu-id="ee087-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="ee087-150">创建带有 DynamicHyperLink 控件的链接</span><span class="sxs-lookup"><span data-stu-id="ee087-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="ee087-151">数据模型中的继承支持</span><span class="sxs-lookup"><span data-stu-id="ee087-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="ee087-152">支持多对多关系（仅实体框架）</span><span class="sxs-lookup"><span data-stu-id="ee087-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="ee087-153">用于控制显示和支持枚举的新属性</span><span class="sxs-lookup"><span data-stu-id="ee087-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="ee087-154">增强的筛选器支持</span><span class="sxs-lookup"><span data-stu-id="ee087-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="ee087-155">**[Visual Studio 2010 Web 开发改进](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="ee087-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="ee087-156">提高了 CSS 兼容性</span><span class="sxs-lookup"><span data-stu-id="ee087-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="ee087-157">HTML 和 JavaScript 代码段</span><span class="sxs-lookup"><span data-stu-id="ee087-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="ee087-158">JavaScript IntelliSense 增强功能</span><span class="sxs-lookup"><span data-stu-id="ee087-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="ee087-159">**[用 Visual Studio 2010 部署 Web 应用程序](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="ee087-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="ee087-160">Web 打包</span><span class="sxs-lookup"><span data-stu-id="ee087-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="ee087-161">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="ee087-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="ee087-162">数据库部署</span><span class="sxs-lookup"><span data-stu-id="ee087-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="ee087-163">Web 应用程序一键式发布</span><span class="sxs-lookup"><span data-stu-id="ee087-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="ee087-164">资源</span><span class="sxs-lookup"><span data-stu-id="ee087-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="ee087-165">**[否认](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="ee087-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="ee087-166">核心服务</span><span class="sxs-lookup"><span data-stu-id="ee087-166">Core Services</span></span>

<span data-ttu-id="ee087-167">ASP.NET 4 引入了许多功能，可改善核心 ASP.NET 服务，例如输出缓存和会话状态存储。</span><span class="sxs-lookup"><span data-stu-id="ee087-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="ee087-168">Web.config 文件重构</span><span class="sxs-lookup"><span data-stu-id="ee087-168">Web.config File Refactoring</span></span>

<span data-ttu-id="ee087-169">由于添加了新功能（如 Ajax、路由和与 IIS 7 的集成），包含 Web 应用程序配置的 `Web.config` 文件在过去的几个 .NET Framework 版本中已大大增长。</span><span class="sxs-lookup"><span data-stu-id="ee087-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="ee087-170">这样就无需使用 Visual Studio 之类的工具，就可以更轻松地配置或启动新的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="ee087-171">在中，.NET Framework 4 中的主要配置元素已移动到 `machine.config` 文件中，应用程序现在继承这些设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="ee087-172">这允许 ASP.NET 4 应用程序中的 `Web.config` 文件为空或仅包含以下行，这两行为 Visual Studio 指定应用程序面向的框架版本：</span><span class="sxs-lookup"><span data-stu-id="ee087-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="ee087-173">可扩展的输出缓存</span><span class="sxs-lookup"><span data-stu-id="ee087-173">Extensible Output Caching</span></span>

<span data-ttu-id="ee087-174">自 ASP.NET 1.0 发布之日起，输出缓存使开发人员能够将生成的页面、控件和 HTTP 响应的输出存储在内存中。</span><span class="sxs-lookup"><span data-stu-id="ee087-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="ee087-175">在后续 Web 请求中，ASP.NET 可以通过从内存中检索生成的输出，而不是从头开始重新生成输出来更快地提供内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="ee087-176">但是，这种方法有一个限制：始终必须将生成的内容存储在内存中，并且在遇到大量流量的服务器上，输出缓存使用的内存可能会与 Web 应用程序的其他部分中的内存需求争夺。</span><span class="sxs-lookup"><span data-stu-id="ee087-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="ee087-177">ASP.NET 4 将可扩展性点添加到输出缓存，使你能够配置一个或多个自定义输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="ee087-178">输出缓存提供程序可以使用任何存储机制来保存 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="ee087-179">这样，便可以为各种持久性机制（包括本地或远程磁盘、云存储和分布式缓存引擎）创建自定义输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="ee087-180">将自定义输出缓存提供程序创建为从新的*方便*类型派生的类。</span><span class="sxs-lookup"><span data-stu-id="ee087-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="ee087-181">然后，可以使用*outputCache*元素的新*provider*子节在 `Web.config` 文件中配置该提供程序，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="ee087-182">默认情况下，在 ASP.NET 4 中，所有 HTTP 响应、呈现的页面和控件都使用内存中输出缓存，如前面的示例所示，其中*defaultProvider*属性设置为 AspNetInternalProvider。</span><span class="sxs-lookup"><span data-stu-id="ee087-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="ee087-183">通过为*defaultProvider*指定不同的提供程序名称，可以更改用于 Web 应用程序的默认输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="ee087-184">此外，还可以为每个控件和每个请求选择不同的输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="ee087-185">为不同的 Web 用户控件选择不同的输出缓存提供程序的最简单方法是使用 control 指令中的 new *providerName*属性以声明方式执行此操作，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="ee087-186">为 HTTP 请求指定不同的输出缓存提供程序需要更多的工作。</span><span class="sxs-lookup"><span data-stu-id="ee087-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="ee087-187">不以声明方式指定提供程序，而是覆盖 `Global.asax` 文件中的新的*GetOuputCacheProviderName*方法，以编程方式指定要用于特定请求的提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="ee087-188">下面的示例演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="ee087-189">通过向 ASP.NET 4 添加输出缓存提供程序扩展性，你现在可以为你的网站提供更主动、更智能的输出缓存策略。</span><span class="sxs-lookup"><span data-stu-id="ee087-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="ee087-190">例如，现在可以在内存中缓存站点的 "前10个" 页，同时缓存可在磁盘上获取较低流量的页面。</span><span class="sxs-lookup"><span data-stu-id="ee087-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="ee087-191">或者，你可以为呈现的页面缓存每个不同的不同组合，但使用分布式缓存，以便从前端 Web 服务器卸载内存消耗。</span><span class="sxs-lookup"><span data-stu-id="ee087-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="ee087-192">自动启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="ee087-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="ee087-193">在处理第一个请求之前，某些 Web 应用程序需要加载大量数据或执行昂贵的初始化处理。</span><span class="sxs-lookup"><span data-stu-id="ee087-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="ee087-194">在早期版本的 ASP.NET 中，对于这种情况，必须设计自定义方法来 "唤醒" ASP.NET 应用程序，然后在*应用程序*中运行初始化代码，\_在 `Global.asax` 文件中加载方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="ee087-195">当 ASP.NET 4 在 Windows Server 2008 R2 上的 IIS 7.5 上运行时，可以使用一个名为 "*自动启动*" 的新的可伸缩性功能，该功能直接满足此方案。</span><span class="sxs-lookup"><span data-stu-id="ee087-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="ee087-196">自动启动功能提供了一种控制方法，用于启动应用程序池、初始化 ASP.NET 应用程序，然后接受 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="ee087-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ee087-197">Iis 7.5 的 IIS 应用程序预热模块</span><span class="sxs-lookup"><span data-stu-id="ee087-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="ee087-198">IIS 团队已发布 IIS 7.5 的应用程序预热模块的第一个 beta 版测试版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="ee087-199">这会使应用程序的预热比之前介绍的更简单。</span><span class="sxs-lookup"><span data-stu-id="ee087-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="ee087-200">您可以指定在 Web 应用程序接受来自网络的请求之前要执行的资源 Url，而不是编写自定义代码。</span><span class="sxs-lookup"><span data-stu-id="ee087-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="ee087-201">启动 IIS 服务（如果将 IIS 应用程序池配置为*AlwaysRunning*）和 iis 工作进程回收时，会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="ee087-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="ee087-202">在回收期间，旧的 IIS 工作进程将继续执行请求，直到新生成的工作进程完全准备好，这样应用程序就不会遇到中断或 unprimed 缓存引起的其他问题。</span><span class="sxs-lookup"><span data-stu-id="ee087-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="ee087-203">请注意，此模块适用于 ASP.NET 的任何版本，从版本2.0 开始。</span><span class="sxs-lookup"><span data-stu-id="ee087-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="ee087-204">有关详细信息，请参阅 IIS.net 网站上的[应用程序预热](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)。</span><span class="sxs-lookup"><span data-stu-id="ee087-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="ee087-205">有关演示如何使用预热功能的演练，请参阅 IIS.net 网站上[的使用 IIS 7.5 应用程序预热模块入门](https://www.iis.net/learn/manage)。</span><span class="sxs-lookup"><span data-stu-id="ee087-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>

<span data-ttu-id="ee087-206">若要使用自动启动功能，IIS 管理员会在 IIS 7.5 中将应用程序池设置为使用 `applicationHost.config` 文件中的以下配置自动启动：</span><span class="sxs-lookup"><span data-stu-id="ee087-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="ee087-207">由于单个应用程序池可以包含多个应用程序，因此可以使用 `applicationHost.config` 文件中的以下配置来指定要自动启动的单个应用程序：</span><span class="sxs-lookup"><span data-stu-id="ee087-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="ee087-208">当 IIS 7.5 服务器冷启动或单个应用程序池被回收时，IIS 7.5 会使用 `applicationHost.config` 文件中的信息来确定需要自动启动的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="ee087-209">对于标记为自动启动的每个应用程序，IIS 7.5 向 ASP.NET 4 发送请求，以在应用程序暂时不接受 HTTP 请求的状态下启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="ee087-210">当它处于此状态时，ASP.NET 将实例化由*serviceAutoStartProvider*属性定义的类型（如前面的示例所示），并调用其公共入口点。</span><span class="sxs-lookup"><span data-stu-id="ee087-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="ee087-211">通过实现*IProcessHostPreloadClient*接口，可以创建具有所需入口点的托管自动启动类型，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="ee087-212">在*预加载*方法中运行初始化代码并且方法返回后，ASP.NET 应用程序就可以处理请求了。</span><span class="sxs-lookup"><span data-stu-id="ee087-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="ee087-213">随着将自动启动添加到 IIS .5 和 ASP.NET 4，你现在已有一个明确定义的方法，用于在处理第一个 HTTP 请求之前执行开销较高的应用程序初始化。</span><span class="sxs-lookup"><span data-stu-id="ee087-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="ee087-214">例如，你可以使用新的自动启动功能来初始化应用程序，然后向负载平衡器发出信号，指示该应用程序已初始化并准备接受 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="ee087-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="ee087-215">永久重定向页面</span><span class="sxs-lookup"><span data-stu-id="ee087-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="ee087-216">Web 应用程序中常见的做法是在一段时间内四处移动页面和其他内容，这可能导致搜索引擎中的过时链接堆积。</span><span class="sxs-lookup"><span data-stu-id="ee087-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="ee087-217">在 ASP.NET 中，开发人员通过使用*响应重定向*方法将请求转发到旧 url。</span><span class="sxs-lookup"><span data-stu-id="ee087-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="ee087-218">但是，*重定向*方法会发出 Http 302 发现（临时重定向）响应，这会在用户尝试访问旧 url 时产生额外的 HTTP 往返。</span><span class="sxs-lookup"><span data-stu-id="ee087-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="ee087-219">ASP.NET 4 添加了新的*RedirectPermanent*帮助器方法，可轻松发出 HTTP 301 移动的永久响应，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="ee087-220">用于识别永久重定向的搜索引擎和其他用户代理将存储与内容关联的新 URL，从而消除了浏览器进行临时重定向时的不必要的往返过程。</span><span class="sxs-lookup"><span data-stu-id="ee087-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="ee087-221">收缩会话状态</span><span class="sxs-lookup"><span data-stu-id="ee087-221">Shrinking Session State</span></span>

<span data-ttu-id="ee087-222">ASP.NET 提供了两个默认选项，用于在 Web 场中存储会话状态：一个会话状态提供程序，该提供程序调用进程外会话状态服务器，以及一个将数据存储在 Microsoft SQL Server 数据库中的会话状态提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="ee087-223">因为这两个选项都涉及将状态信息存储在 Web 应用程序的工作进程之外，所以必须在将会话状态发送到远程存储之前对其进行序列化。</span><span class="sxs-lookup"><span data-stu-id="ee087-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="ee087-224">根据开发人员在会话状态中保存的信息量，序列化数据的大小可能会很大。</span><span class="sxs-lookup"><span data-stu-id="ee087-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="ee087-225">对于这两种进程外会话状态提供程序，ASP.NET 4 引入了新的压缩选项。</span><span class="sxs-lookup"><span data-stu-id="ee087-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="ee087-226">如果下面的示例中所示的*compressionEnabled*配置选项设置为*true*，则 ASP.NET 将使用 .NET Framework *GZipStream*类来压缩（并解压缩）序列化会话状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="ee087-227">通过简单地将新属性添加到 `Web.config` 文件，在 Web 服务器上具有备用 CPU 周期的应用程序可以在序列化会话状态数据的大小上实现大幅降低。</span><span class="sxs-lookup"><span data-stu-id="ee087-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="ee087-228">展开允许的 Url 范围</span><span class="sxs-lookup"><span data-stu-id="ee087-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="ee087-229">ASP.NET 4 引入了用于扩展应用程序 Url 大小的新选项。</span><span class="sxs-lookup"><span data-stu-id="ee087-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="ee087-230">以前版本的 ASP.NET 根据 NTFS 文件路径限制将 URL 路径长度限制为260个字符。</span><span class="sxs-lookup"><span data-stu-id="ee087-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="ee087-231">在 ASP.NET 4 中，可以使用两个新的*httpRuntime*配置属性，根据应用程序的需要增加（或减少）此限制。</span><span class="sxs-lookup"><span data-stu-id="ee087-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="ee087-232">下面的示例显示了这些新的属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="ee087-233">若要允许更长或更短的路径（不包括协议、服务器名称和查询字符串的 URL 部分），请修改 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="ee087-234">若要允许更长或更短的查询字符串，请修改 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 属性的值。</span><span class="sxs-lookup"><span data-stu-id="ee087-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="ee087-235">ASP.NET 4 还允许您配置 URL 字符检查所使用的字符。</span><span class="sxs-lookup"><span data-stu-id="ee087-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="ee087-236">当 ASP.NET 在 URL 的路径部分找到无效字符时，它将拒绝该请求并发出 HTTP 400 错误。</span><span class="sxs-lookup"><span data-stu-id="ee087-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="ee087-237">在以前版本的 ASP.NET 中，URL 字符检查限制为固定的字符集。</span><span class="sxs-lookup"><span data-stu-id="ee087-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="ee087-238">在 ASP.NET 4 中，可以使用*httpRuntime*配置元素的新*requestPathInvalidCharacters*属性自定义一组有效字符，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidCharacters* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="ee087-239">默认情况下， *requestPathInvalidCharacters*属性将8个字符定义为无效。</span><span class="sxs-lookup"><span data-stu-id="ee087-239">By default, the *requestPathInvalidCharacters* attribute defines eight characters as invalid.</span></span> <span data-ttu-id="ee087-240">（在默认情况下分配给*requestPathInvalidCharacters*的字符串中，小于号（&lt;）、大于号（&gt;）和 & 号（&amp;）字符经过编码，因为 `Web.config` 文件是一个 XML 文件。）您可以根据需要自定义无效字符集。</span><span class="sxs-lookup"><span data-stu-id="ee087-240">(In the string that is assigned to *requestPathInvalidCharacters* by default, the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="ee087-241">请注意，ASP.NET 4 始终拒绝在 ASCII 范围0x00 到0x1F 中包含字符的 URL 路径，因为这些字符是在 IETF （[http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)）的 RFC 2396 中定义的无效 url 字符。</span><span class="sxs-lookup"><span data-stu-id="ee087-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="ee087-242">在运行 IIS 6 或更高版本的 Windows Server 版本上，http.sys 协议设备驱动程序会自动拒绝包含这些字符的 Url。</span><span class="sxs-lookup"><span data-stu-id="ee087-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="ee087-243">可扩展请求验证</span><span class="sxs-lookup"><span data-stu-id="ee087-243">Extensible Request Validation</span></span>

<span data-ttu-id="ee087-244">ASP.NET 请求验证会搜索传入的 HTTP 请求数据，查找通常在跨站点脚本（XSS）攻击中使用的字符串。</span><span class="sxs-lookup"><span data-stu-id="ee087-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="ee087-245">如果发现潜在的 XSS 字符串，请求验证会标记可疑字符串并返回错误。</span><span class="sxs-lookup"><span data-stu-id="ee087-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="ee087-246">内置请求验证仅在发现 XSS 攻击中使用的最常见字符串时才会返回错误。</span><span class="sxs-lookup"><span data-stu-id="ee087-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="ee087-247">以前尝试使 XSS 验证更积极会导致误报太多。</span><span class="sxs-lookup"><span data-stu-id="ee087-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="ee087-248">但是，客户可能想要对更积极的请求进行验证，或者相反，可能想要为特定页面或特定类型的请求有意放松 XSS 检查。</span><span class="sxs-lookup"><span data-stu-id="ee087-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="ee087-249">在 ASP.NET 4 中，已对请求验证功能进行了扩展，使你可以使用自定义请求验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="ee087-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="ee087-250">若要扩展请求验证，请创建一个从新的*Util*类型派生的类，并将应用程序（位于 `Web.config` 文件的*httpRuntime*部分）配置为使用自定义类型。</span><span class="sxs-lookup"><span data-stu-id="ee087-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="ee087-251">下面的示例演示如何配置自定义请求验证类：</span><span class="sxs-lookup"><span data-stu-id="ee087-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="ee087-252">新的*requestValidationType*属性需要指定提供自定义请求验证的类的标准 .NET Framework 类型标识符字符串。</span><span class="sxs-lookup"><span data-stu-id="ee087-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="ee087-253">对于每个请求，ASP.NET 会调用自定义类型来处理每个传入的 HTTP 请求数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="ee087-254">传入 URL、所有 HTTP 标头（cookie 和自定义标头）和实体正文都可由自定义请求验证类进行检查，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="ee087-255">对于不希望检查一段传入 HTTP 数据的情况，请求验证类可以回退为通过只调用 base 来运行 ASP.NET 默认请求验证 *。IsValidRequestString。*</span><span class="sxs-lookup"><span data-stu-id="ee087-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="ee087-256">对象缓存和对象缓存扩展性</span><span class="sxs-lookup"><span data-stu-id="ee087-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="ee087-257">自首次发布以来，ASP.NET 已包含一个功能强大的内存中对象*缓存（）。*</span><span class="sxs-lookup"><span data-stu-id="ee087-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="ee087-258">缓存实现非常流行，因为它已在非 Web 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="ee087-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="ee087-259">不过，Windows 窗体或 WPF 应用程序在 `System.Web.dll` 中包含对的引用只是为了能够使用 ASP.NET 对象缓存，这种方法很难。</span><span class="sxs-lookup"><span data-stu-id="ee087-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="ee087-260">为了使缓存可供所有应用程序使用，.NET Framework 4 引入了新的程序集、新的命名空间、某些基类型和具体的缓存实现。</span><span class="sxs-lookup"><span data-stu-id="ee087-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="ee087-261">新的 `System.Runtime.Caching.dll` 程序集在*system.web*命名空间中包含新的缓存 API。</span><span class="sxs-lookup"><span data-stu-id="ee087-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="ee087-262">命名空间包含两个核心类集：</span><span class="sxs-lookup"><span data-stu-id="ee087-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="ee087-263">提供构建任何类型的自定义缓存实现的基础的抽象类型。</span><span class="sxs-lookup"><span data-stu-id="ee087-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="ee087-264">具体的内存中对象缓存实现（ *MemoryCache*类）。</span><span class="sxs-lookup"><span data-stu-id="ee087-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="ee087-265">新的*MemoryCache*类在 ASP.NET 缓存上密切建模，并与 ASP.NET 共享了许多内部缓存引擎逻辑。</span><span class="sxs-lookup"><span data-stu-id="ee087-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="ee087-266">尽管已*更新了 system.exception 中的*公共缓存 api 以支持开发自定义缓存，但如果你使用了 ASP.NET*缓存*对象，你将在新的 api 中找到熟悉的概念。</span><span class="sxs-lookup"><span data-stu-id="ee087-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="ee087-267">对于新的*MemoryCache*类和支持基本 api 的深入讨论，需要一个完整的文档。</span><span class="sxs-lookup"><span data-stu-id="ee087-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="ee087-268">不过，下面的示例为您提供了新的缓存 API 的工作原理。</span><span class="sxs-lookup"><span data-stu-id="ee087-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="ee087-269">该示例是针对 Windows 窗体的应用程序编写的，不依赖于 `System.Web.dll`。</span><span class="sxs-lookup"><span data-stu-id="ee087-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="ee087-270">可扩展的 HTML、URL 和 HTTP 标头编码</span><span class="sxs-lookup"><span data-stu-id="ee087-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="ee087-271">在 ASP.NET 4 中，可以为以下常见文本编码任务创建自定义编码例程：</span><span class="sxs-lookup"><span data-stu-id="ee087-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="ee087-272">HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-272">HTML encoding.</span></span>
- <span data-ttu-id="ee087-273">URL 编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-273">URL encoding.</span></span>
- <span data-ttu-id="ee087-274">HTML 特性编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="ee087-275">编码出站 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="ee087-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="ee087-276">你可以通过从新的*Util*类型派生来创建自定义编码器，然后将 ASP.NET 配置为使用 `Web.config` 文件的*httpRuntime*部分中的自定义类型，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="ee087-277">配置自定义编码器后，只要调用*httputility.javascriptstringencode*或*HttpServerUtility*类的公共编码方法，ASP.NET 就会自动调用自定义编码实现。</span><span class="sxs-lookup"><span data-stu-id="ee087-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="ee087-278">这允许 Web 开发团队的一个部分创建可实现严格的字符编码的自定义编码器，而其他 Web 开发团队则继续使用公共 ASP.NET 编码 Api。</span><span class="sxs-lookup"><span data-stu-id="ee087-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="ee087-279">通过在*httpRuntime*元素中集中配置自定义编码器，可以确保来自公共 ASP.NET 编码 api 的所有文本编码调用都通过自定义编码器路由。</span><span class="sxs-lookup"><span data-stu-id="ee087-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="ee087-280">单个工作进程中单个应用程序的性能监视</span><span class="sxs-lookup"><span data-stu-id="ee087-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="ee087-281">为了增加可在单个服务器上托管的网站的数量，许多托管商在单个辅助进程中运行多个 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="ee087-282">但是，如果多个应用程序使用单个共享工作进程，则服务器管理员很难识别遇到问题的单个应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="ee087-283">ASP.NET 4 利用 CLR 引入的新的资源监视功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="ee087-284">若要启用此功能，可以将以下 XML 配置代码段添加到 `aspnet.config` 配置文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="ee087-285">请注意，`aspnet.config` 文件位于安装了 .NET Framework 的目录中。</span><span class="sxs-lookup"><span data-stu-id="ee087-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="ee087-286">它不是 `Web.config` 的文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-286">It is not the `Web.config` file.</span></span>

<span data-ttu-id="ee087-287">启用*appDomainResourceMonitoring*功能后，"ASP.NET 应用程序" 性能类别中会提供两个新的性能计数器： *% 托管处理器时间*和*使用的托管内存*。</span><span class="sxs-lookup"><span data-stu-id="ee087-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="ee087-288">这两个性能计数器都使用新的 CLR 应用程序-域资源管理功能来跟踪单个 ASP.NET 应用程序的估计 CPU 时间和托管内存使用率。</span><span class="sxs-lookup"><span data-stu-id="ee087-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="ee087-289">因此，使用 ASP.NET 4，管理员现在可以更精细地查看单个辅助进程中运行的单个应用程序的资源消耗情况。</span><span class="sxs-lookup"><span data-stu-id="ee087-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="ee087-290">多目标</span><span class="sxs-lookup"><span data-stu-id="ee087-290">Multi-Targeting</span></span>

<span data-ttu-id="ee087-291">你可以创建面向特定版本的 .NET Framework 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="ee087-292">在 ASP.NET 4 中，`Web.config` 文件的*编译*元素中的一个新属性允许以 .NET Framework 4 和更高版本为目标。</span><span class="sxs-lookup"><span data-stu-id="ee087-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="ee087-293">如果显式以 .NET Framework 4 为目标，并且在 `Web.config` 文件（如*system.object*的条目）中包含可选元素，则对于 .NET Framework 4，这些元素必须是正确的。</span><span class="sxs-lookup"><span data-stu-id="ee087-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="ee087-294">（如果未显式定位到 .NET Framework 4，则将从 `Web.config` 文件中缺少某个条目推断出目标框架。）</span><span class="sxs-lookup"><span data-stu-id="ee087-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="ee087-295">下面的示例演示如何在 `Web.config` 文件的*编译*元素中使用*targetFramework*特性。</span><span class="sxs-lookup"><span data-stu-id="ee087-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="ee087-296">请注意以下有关特定版本的 .NET Framework 的信息：</span><span class="sxs-lookup"><span data-stu-id="ee087-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="ee087-297">在 .NET Framework 4 应用程序池中，如果 `Web.config` 文件不包括*targetFramework*特性或缺少 `Web.config` 文件，则 ASP.NET 生成系统会将 .NET Framework 4 作为目标。</span><span class="sxs-lookup"><span data-stu-id="ee087-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="ee087-298">（你可能需要对应用程序进行编码更改，使其在 .NET Framework 4 下运行。）</span><span class="sxs-lookup"><span data-stu-id="ee087-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="ee087-299">如果包括*targetFramework*属性，并且在 `Web.config` 文件中定义了*system.web*元素，则此文件必须包含 .NET Framework 4 的正确条目。</span><span class="sxs-lookup"><span data-stu-id="ee087-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="ee087-300">如果使用*aspnet\_编译器*命令预编译应用程序（如在生成环境中），则必须为目标框架使用正确版本的*aspnet\_编译器*命令。</span><span class="sxs-lookup"><span data-stu-id="ee087-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="ee087-301">使用附带 .NET Framework 2.0 （%WINDIR%\Microsoft.NET\Framework\v2.0.50727）的编译器编译 .NET Framework 3.5 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="ee087-302">使用 .NET Framework 4 附带的编译器编译使用该框架或更高版本创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="ee087-303">在运行时，编译器将使用计算机上安装的最新 framework 程序集（因此在 GAC 中）。</span><span class="sxs-lookup"><span data-stu-id="ee087-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="ee087-304">如果稍后将更新到框架（例如，安装了假设版本4.1），则可以使用较新版本的 framework 中的功能，即使*targetFramework*属性面向较低版本（如4.0）。</span><span class="sxs-lookup"><span data-stu-id="ee087-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="ee087-305">（但是，在 Visual Studio 2010 或使用*aspnet\_编译器*命令时，使用该框架的新功能将导致编译器错误）。</span><span class="sxs-lookup"><span data-stu-id="ee087-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="ee087-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="ee087-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="ee087-307">Web 窗体和 MVC 中包含的 jQuery</span><span class="sxs-lookup"><span data-stu-id="ee087-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="ee087-308">Web 窗体和 MVC 的 Visual Studio 模板都包含开放源代码 jQuery library。</span><span class="sxs-lookup"><span data-stu-id="ee087-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="ee087-309">创建新网站或项目时，将创建一个包含以下3个文件的脚本文件夹：</span><span class="sxs-lookup"><span data-stu-id="ee087-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="ee087-310">/Selfservice/scripts/jquery-1.10.2.min.js 1.4.1 – jQuery library 的用户可读的 unminified 版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="ee087-311">/Selfservice/scripts/jquery-1.10.2.min.js 14.1 版– jQuery library 的缩小版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="ee087-312">/Selfservice/scripts/jquery-1.10.2.min.js 1.4.1-vsdoc-jQuery library 的 Intellisense 文档文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="ee087-313">开发应用程序时包括 jQuery 的 unminified 版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="ee087-314">为生产应用程序包括 jQuery 的缩小版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="ee087-315">例如，下面的 Web 窗体页演示了如何使用 jQuery 将 ASP.NET TextBox 控件的背景色更改为黄色。</span><span class="sxs-lookup"><span data-stu-id="ee087-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="ee087-316">内容交付网络支持</span><span class="sxs-lookup"><span data-stu-id="ee087-316">Content Delivery Network Support</span></span>

<span data-ttu-id="ee087-317">通过 Microsoft Ajax 内容交付网络（CDN），可以轻松地将 ASP.NET Ajax 和 jQuery 脚本添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="ee087-318">例如，只需将 `<script>` 标记添加到页面中，就可以开始使用 jQuery library，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="ee087-319">通过利用 Microsoft Ajax CDN，可以显著改进 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="ee087-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="ee087-320">Microsoft Ajax CDN 的内容缓存在位于世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="ee087-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="ee087-321">此外，Microsoft Ajax CDN 使浏览器可以对位于不同域的网站重用缓存的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="ee087-322">Microsoft Ajax 内容交付网络支持 SSL （HTTPS），以防需要使用安全套接字层来提供网页。</span><span class="sxs-lookup"><span data-stu-id="ee087-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="ee087-323">当 CDN 不可用时，实施回退。</span><span class="sxs-lookup"><span data-stu-id="ee087-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="ee087-324">测试回退。</span><span class="sxs-lookup"><span data-stu-id="ee087-324">Test the fallback.</span></span>

<span data-ttu-id="ee087-325">若要了解有关 Microsoft Ajax CDN 的详细信息，请访问以下网站：</span><span class="sxs-lookup"><span data-stu-id="ee087-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="ee087-326">ASP.NET ScriptManager 支持 Microsoft Ajax CDN。</span><span class="sxs-lookup"><span data-stu-id="ee087-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="ee087-327">只需设置一个属性 EnableCdn 属性，即可从 CDN 检索所有 ASP.NET framework JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="ee087-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="ee087-328">将 EnableCdn 属性设置为值 true 后，ASP.NET 框架将从 CDN 检索所有 ASP.NET framework JavaScript 文件，其中包括用于验证和 UpdatePanel 的所有 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="ee087-329">设置此属性可能会对 web 应用程序的性能产生极大的影响。</span><span class="sxs-lookup"><span data-stu-id="ee087-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="ee087-330">可以使用 WebResource 属性为自己的 JavaScript 文件设置 CDN 路径。</span><span class="sxs-lookup"><span data-stu-id="ee087-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="ee087-331">新的 CdnPath 属性指定将 EnableCdn 属性设置为值 true 时使用的 CDN 的路径：</span><span class="sxs-lookup"><span data-stu-id="ee087-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="ee087-332">ScriptManager 显式脚本</span><span class="sxs-lookup"><span data-stu-id="ee087-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="ee087-333">过去，如果使用了 ASP.NET ScriptManger，则需要加载整个单一 ASP.NET Ajax 库。</span><span class="sxs-lookup"><span data-stu-id="ee087-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="ee087-334">通过利用新的 AjaxFrameworkMode 属性，您可以准确控制加载 ASP.NET Ajax 库的哪些组件并仅加载所需的 ASP.NET Ajax 库的组件。</span><span class="sxs-lookup"><span data-stu-id="ee087-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="ee087-335">可以将 AjaxFrameworkMode 属性设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="ee087-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="ee087-336">已启用--指定 ScriptManager 控件自动包括 Microsoftajax.js 脚本文件，该文件是每个核心框架脚本的合并脚本文件（旧版行为）。</span><span class="sxs-lookup"><span data-stu-id="ee087-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="ee087-337">Disabled-指定禁用所有 Microsoft Ajax script 功能，并且 ScriptManager 控件不自动引用任何脚本。</span><span class="sxs-lookup"><span data-stu-id="ee087-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="ee087-338">显式--指定您将显式包括对页面所需的单独框架核心脚本文件的脚本引用，并且您将包括对每个脚本文件所需的依赖项的引用。</span><span class="sxs-lookup"><span data-stu-id="ee087-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="ee087-339">例如，如果将 AjaxFrameworkMode 属性设置为值 Explicit，则可以指定所需的特定 ASP.NET Ajax 组件脚本：</span><span class="sxs-lookup"><span data-stu-id="ee087-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="ee087-340">Web Forms — Web 窗体</span><span class="sxs-lookup"><span data-stu-id="ee087-340">Web Forms</span></span>

<span data-ttu-id="ee087-341">自发布 ASP.NET 1.0 以来，Web 窗体已成为 ASP.NET 中的核心功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="ee087-342">ASP.NET 4 的此区域已提供许多增强功能，其中包括：</span><span class="sxs-lookup"><span data-stu-id="ee087-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="ee087-343">设置*meta*标记的功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="ee087-344">更好地控制视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-344">More control over view state.</span></span>
- <span data-ttu-id="ee087-345">使用浏览器功能的更简单方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="ee087-346">支持对 Web 窗体使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="ee087-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="ee087-347">更好地控制生成的 Id。</span><span class="sxs-lookup"><span data-stu-id="ee087-347">More control over generated IDs.</span></span>
- <span data-ttu-id="ee087-348">可以在数据控件中保留选定的行。</span><span class="sxs-lookup"><span data-stu-id="ee087-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="ee087-349">更好地控制*FormView*和*ListView*控件中呈现的 HTML。</span><span class="sxs-lookup"><span data-stu-id="ee087-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="ee087-350">对数据源控件的筛选支持。</span><span class="sxs-lookup"><span data-stu-id="ee087-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="ee087-351">用 MetaKeywords 和 MetaDescription 属性设置 Meta 标记</span><span class="sxs-lookup"><span data-stu-id="ee087-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="ee087-352">ASP.NET 4 将两个属性添加到*页面*类*MetaKeywords*和*MetaDescription*。</span><span class="sxs-lookup"><span data-stu-id="ee087-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="ee087-353">这两个属性表示页面中对应的*元*标记，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="ee087-354">这两个属性的工作方式与页面的 "*标题*" 属性相同。</span><span class="sxs-lookup"><span data-stu-id="ee087-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="ee087-355">它们遵循以下规则：</span><span class="sxs-lookup"><span data-stu-id="ee087-355">They follow these rules:</span></span>

1. <span data-ttu-id="ee087-356">如果*head*元素中没有与 MetaDescription 的属性名称匹配的*元*标记（即*MetaKeywords*的 name = "关键字"，而的名称 = "description"），则在呈现时将元标记添加到页面中，然后将*元*标记添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="ee087-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="ee087-357">如果已存在具有这些名称的*元*标记，则这些属性将充当现有标记的内容的 get 和 set 方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="ee087-358">您可以在运行时设置这些属性，这样您就可以从数据库或其他数据源中获取内容，并使您可以动态设置标记来描述特定页面的用途。</span><span class="sxs-lookup"><span data-stu-id="ee087-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="ee087-359">你还可以在 Web 窗体页标记顶部的 *@ Page*指令中设置*关键字*和*说明*属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="ee087-360">这会重写页面中已声明的*元*标记内容（如果有）。</span><span class="sxs-lookup"><span data-stu-id="ee087-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="ee087-361">Description*元*标记的内容用于改进 Google 中的搜索列表预览。</span><span class="sxs-lookup"><span data-stu-id="ee087-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="ee087-362">（有关详细信息，请参阅 Google 网站管理员中心博客上的[使用元说明改善代码段功能改进](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html)。）Google 和 Windows Live 搜索不会将关键字的内容用于任何内容，但其他搜索引擎可能会。</span><span class="sxs-lookup"><span data-stu-id="ee087-362">(For details, see [Improve snippets with a meta description makeover](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="ee087-363">有关详细信息，请参阅搜索引擎指南网站上的[元关键字建议](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)。</span><span class="sxs-lookup"><span data-stu-id="ee087-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="ee087-364">这些新属性是一个简单的功能，但它们会使你不需要手动添加这些属性或通过编写自己的代码来创建*元*标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="ee087-365">启用各个控件的视图状态</span><span class="sxs-lookup"><span data-stu-id="ee087-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="ee087-366">默认情况下，将为页面启用视图状态，结果是页面上的每个控件都可能存储视图状态，即使应用程序不需要。</span><span class="sxs-lookup"><span data-stu-id="ee087-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="ee087-367">视图状态数据包含在页面生成的标记中，并增加了向客户端发送页面并回发页面所需的时间。</span><span class="sxs-lookup"><span data-stu-id="ee087-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="ee087-368">如果存储的视图状态超出了所需的数量，可能会导致性能显著下降。</span><span class="sxs-lookup"><span data-stu-id="ee087-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="ee087-369">在早期版本的 ASP.NET 中，开发人员可以禁用各个控件的视图状态，以便减小页面大小，但必须为单个控件显式执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="ee087-370">在 ASP.NET 4 中，Web 服务器控件包含一个*ViewStateMode*属性，该属性使你可以默认禁用视图状态，然后只为需要在页面中使用它的控件启用该状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="ee087-371">*ViewStateMode*属性采用包含三个值的枚举： *Enabled*、 *Disabled*和*Inherit*。</span><span class="sxs-lookup"><span data-stu-id="ee087-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="ee087-372">*启用*后，将启用该控件的视图状态，并为任何设置为*继承*或没有任何设置的子控件启用视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="ee087-373">*Disabled*禁用视图状态，而*Inherit*指定控件使用父控件中的*ViewStateMode*设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="ee087-374">下面的示例演示*ViewStateMode*属性的工作方式。</span><span class="sxs-lookup"><span data-stu-id="ee087-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="ee087-375">以下页面中的控件的标记和代码包括*ViewStateMode*属性的值：</span><span class="sxs-lookup"><span data-stu-id="ee087-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="ee087-376">正如您所看到的，代码禁用了 PlaceHolder1 控件的视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="ee087-377">子 label1 控件继承此属性值（inherits 是控件的*ViewStateMode*的默认值），*因此不保存*任何视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="ee087-378">在 PlaceHolder2 控件中， *ViewStateMode*设置为*Enabled*，因此 label2 继承此属性并保存视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="ee087-379">第一次加载页面时，两个*标签*控件的*Text*属性都设置为字符串 "[DynamicValue]"。</span><span class="sxs-lookup"><span data-stu-id="ee087-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="ee087-380">这些设置的作用是：当页面首次加载时，浏览器中将显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="ee087-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="ee087-381">已禁用 `: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="ee087-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="ee087-382">已启用：`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="ee087-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="ee087-383">但回发后，将显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="ee087-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="ee087-384">已禁用 `: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="ee087-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="ee087-385">已启用：`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="ee087-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="ee087-386">Label1 控件（其*ViewStateMode*值设置为 "*已禁用*"）未保留其在代码中设置为的值。</span><span class="sxs-lookup"><span data-stu-id="ee087-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="ee087-387">但是，label2 控件（其*ViewStateMode*值设置为 "*已启用*"）已保持其状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="ee087-388">你还可以在 *@ Page*指令中设置*ViewStateMode* ，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="ee087-389">*Page*类只是另一个控件;它充当页面中所有其他控件的父控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="ee087-390">为*页*的实例*启用*了*ViewStateMode*的默认值。</span><span class="sxs-lookup"><span data-stu-id="ee087-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="ee087-391">由于控件默认为*继承*，因此控件将继承*Enabled*属性值，除非你在页或控件级别设置*ViewStateMode* 。</span><span class="sxs-lookup"><span data-stu-id="ee087-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="ee087-392">*ViewStateMode*属性的值确定仅在*EnableViewState*属性设置为*true*时是否维护视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="ee087-393">如果将*EnableViewState*属性设置为*false*，则即使将*ViewStateMode*设置为 "*已启用*"，也不会维护视图状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="ee087-394">此功能的一个不错用途是在母版页中使用*ContentPlaceHolder*控件，你可以在其中将*ViewStateMode*设置为 "*已禁用*"，然后为*ContentPlaceHolder*控件单独启用该母版页，这些控件又包含需要视图状态的控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="ee087-395">对浏览器功能的更改</span><span class="sxs-lookup"><span data-stu-id="ee087-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="ee087-396">ASP.NET 确定用户使用的浏览器功能，该浏览器使用一种名为*浏览器功能*的功能来浏览您的网站。</span><span class="sxs-lookup"><span data-stu-id="ee087-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="ee087-397">浏览器功能由*HttpBrowserCapabilities*对象表示（由*请求. Browser*属性公开）。</span><span class="sxs-lookup"><span data-stu-id="ee087-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="ee087-398">例如，可以使用*HttpBrowserCapabilities*对象来确定当前浏览器的类型和版本是否支持特定版本的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="ee087-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="ee087-399">或者，你可以使用*HttpBrowserCapabilities*对象来确定请求是否来自移动设备。</span><span class="sxs-lookup"><span data-stu-id="ee087-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="ee087-400">*HttpBrowserCapabilities*对象由一组浏览器定义文件驱动。</span><span class="sxs-lookup"><span data-stu-id="ee087-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="ee087-401">这些文件包含有关特定浏览器的功能的信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="ee087-402">在 ASP.NET 4 中，这些浏览器定义文件已更新为包含有关最近引入的浏览器和设备（如 Google Chrome、运动 BlackBerry 智能手机和 Apple iPhone）的信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="ee087-403">以下列表显示了新的浏览器定义文件：</span><span class="sxs-lookup"><span data-stu-id="ee087-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="ee087-404">*blackberry 浏览器*</span><span class="sxs-lookup"><span data-stu-id="ee087-404">*blackberry.browser*</span></span>
- <span data-ttu-id="ee087-405">*chrome. browser*</span><span class="sxs-lookup"><span data-stu-id="ee087-405">*chrome.browser*</span></span>
- <span data-ttu-id="ee087-406">*默认浏览器*</span><span class="sxs-lookup"><span data-stu-id="ee087-406">*Default.browser*</span></span>
- <span data-ttu-id="ee087-407">*firefox 浏览器*</span><span class="sxs-lookup"><span data-stu-id="ee087-407">*firefox.browser*</span></span>
- <span data-ttu-id="ee087-408">*网关。浏览器*</span><span class="sxs-lookup"><span data-stu-id="ee087-408">*gateway.browser*</span></span>
- <span data-ttu-id="ee087-409">*通用 .browser*</span><span class="sxs-lookup"><span data-stu-id="ee087-409">*generic.browser*</span></span>
- <span data-ttu-id="ee087-410">*ie*</span><span class="sxs-lookup"><span data-stu-id="ee087-410">*ie.browser*</span></span>
- <span data-ttu-id="ee087-411">*iemobile*</span><span class="sxs-lookup"><span data-stu-id="ee087-411">*iemobile.browser*</span></span>
- <span data-ttu-id="ee087-412">*iphone. browser*</span><span class="sxs-lookup"><span data-stu-id="ee087-412">*iphone.browser*</span></span>
- <span data-ttu-id="ee087-413">*opera*</span><span class="sxs-lookup"><span data-stu-id="ee087-413">*opera.browser*</span></span>
- <span data-ttu-id="ee087-414">*safari 浏览器*</span><span class="sxs-lookup"><span data-stu-id="ee087-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="ee087-415">使用浏览器功能提供程序</span><span class="sxs-lookup"><span data-stu-id="ee087-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="ee087-416">在 ASP.NET 版本 3.5 Service Pack 1 中，可以使用以下方式定义浏览器的功能：</span><span class="sxs-lookup"><span data-stu-id="ee087-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="ee087-417">在计算机级别上，你可以在以下文件夹中创建或更新 `.browser` XML 文件：</span><span class="sxs-lookup"><span data-stu-id="ee087-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="ee087-418">定义浏览器功能后，可以从 Visual Studio 命令提示符运行以下命令，以便重新生成浏览器功能程序集并将其添加到 GAC：</span><span class="sxs-lookup"><span data-stu-id="ee087-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="ee087-419">对于单个应用程序，在应用程序的 `App_Browsers` 文件夹中创建 `.browser` 文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="ee087-420">这些方法要求你更改 XML 文件，对于计算机级更改，你必须在运行 aspnet\_regbrowsers 进程后重新启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="ee087-421">ASP.NET 4 包含一项称为*浏览器功能提供程序*的功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="ee087-422">顾名思义，这允许您生成一个提供程序，然后您可以使用自己的代码来确定浏览器的功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="ee087-423">实际上，开发人员通常不会定义自定义浏览器功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="ee087-424">浏览器文件很难更新，更新这些文件的过程相当复杂，因此，使用和定义 `.browser` 文件的 XML 语法可能会很复杂。</span><span class="sxs-lookup"><span data-stu-id="ee087-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="ee087-425">如果有常见的浏览器定义语法，或是包含最新的浏览器定义的数据库，甚至是此类数据库的 Web 服务，则使此过程变得简单得多。</span><span class="sxs-lookup"><span data-stu-id="ee087-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="ee087-426">新的浏览器功能提供程序功能使得第三方开发人员可以实现这些方案。</span><span class="sxs-lookup"><span data-stu-id="ee087-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="ee087-427">使用 new ASP.NET 4 browser 功能提供程序功能时，有两种主要方法：扩展 ASP.NET 浏览器功能定义功能，或完全替换。</span><span class="sxs-lookup"><span data-stu-id="ee087-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="ee087-428">以下各节介绍了如何替换功能，以及如何对其进行扩展。</span><span class="sxs-lookup"><span data-stu-id="ee087-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="ee087-429">替换 ASP.NET 浏览器功能功能</span><span class="sxs-lookup"><span data-stu-id="ee087-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="ee087-430">若要完全替换 ASP.NET 浏览器功能定义功能，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ee087-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="ee087-431">创建一个派生自*HttpCapabilitiesProvider*的提供程序类，该提供程序类将重写*GetBrowserCapabilities*方法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="ee087-432">此示例中的代码创建一个新的*HttpBrowserCapabilities*对象，该对象仅指定名为 browser 的功能，并将该功能设置为 MyCustomBrowser。</span><span class="sxs-lookup"><span data-stu-id="ee087-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="ee087-433">将提供程序注册到应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="ee087-434">若要将提供程序与应用程序一起使用，必须将*提供程序*特性添加到 `Web.config` 或 `Machine.config` 文件中的*browserCaps*部分。</span><span class="sxs-lookup"><span data-stu-id="ee087-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="ee087-435">（你还可以在*location*元素中为应用程序中的特定目录定义提供程序属性，例如在特定移动设备的文件夹中。）下面的示例演示如何在配置文件中设置*provider*特性：</span><span class="sxs-lookup"><span data-stu-id="ee087-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="ee087-436">注册新的浏览器功能定义的另一种方法是使用代码，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="ee087-437">此代码必须在 `Global.asax` 文件 *\_开始事件的应用程序*中运行。</span><span class="sxs-lookup"><span data-stu-id="ee087-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="ee087-438">对*BrowserCapabilitiesProvider*类所做的任何更改必须在执行应用程序中的任何代码之前发生，以确保缓存对于解析的*HttpCapabilitiesBase*对象保持有效状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="ee087-439">缓存 HttpBrowserCapabilities 对象</span><span class="sxs-lookup"><span data-stu-id="ee087-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="ee087-440">前面的示例有一个问题，即每次调用自定义提供程序来获取*HttpBrowserCapabilities*对象时，代码都将运行。</span><span class="sxs-lookup"><span data-stu-id="ee087-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="ee087-441">这可能会在每个请求期间发生多次。</span><span class="sxs-lookup"><span data-stu-id="ee087-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="ee087-442">在此示例中，提供程序的代码不会执行许多操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="ee087-443">但是，如果你的自定义提供程序中的代码执行了大量工作来获取*HttpBrowserCapabilities*对象，则这可能会影响性能。</span><span class="sxs-lookup"><span data-stu-id="ee087-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="ee087-444">若要防止此情况发生，可以缓存*HttpBrowserCapabilities*对象。</span><span class="sxs-lookup"><span data-stu-id="ee087-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="ee087-445">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="ee087-445">Follow these steps:</span></span>

1. <span data-ttu-id="ee087-446">创建一个派生自*HttpCapabilitiesProvider*的类，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="ee087-447">在此示例中，代码通过调用自定义 BuildCacheKey 方法生成一个缓存密钥，并通过调用自定义 GetCacheTime 方法获取缓存的时间长度。</span><span class="sxs-lookup"><span data-stu-id="ee087-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="ee087-448">然后，该代码将解析的*HttpBrowserCapabilities*对象添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="ee087-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="ee087-449">可以从缓存中检索对象，并可在后续请求中重复使用自定义提供程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="ee087-450">按照前面的过程中所述，将提供程序注册到应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="ee087-451">扩展 ASP.NET 浏览器功能功能</span><span class="sxs-lookup"><span data-stu-id="ee087-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="ee087-452">上一部分介绍了如何在 ASP.NET 4 中创建新的*HttpBrowserCapabilities*对象。</span><span class="sxs-lookup"><span data-stu-id="ee087-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="ee087-453">还可以通过将新的浏览器功能定义添加到已在 ASP.NET 中的功能，来扩展 ASP.NET 浏览器功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="ee087-454">可以在不使用 XML 浏览器定义的情况下执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="ee087-455">下面的过程演示了如何操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="ee087-456">创建一个从*HttpCapabilitiesEvaluator*派生的类，它将重写*GetBrowserCapabilities*方法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="ee087-457">此代码首先使用 ASP.NET 浏览器功能功能来尝试标识浏览器。</span><span class="sxs-lookup"><span data-stu-id="ee087-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="ee087-458">但是，如果未根据请求中定义的信息来标识浏览器（即，如果*HttpBrowserCapabilities*对象的*browser*属性为字符串 "Unknown"），则代码将调用自定义提供程序（MyBrowserCapabilitiesEvaluator）来标识浏览器。</span><span class="sxs-lookup"><span data-stu-id="ee087-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="ee087-459">按照前面的示例中所述，将提供程序注册到应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="ee087-460">通过向现有功能定义添加新功能来扩展浏览器功能功能</span><span class="sxs-lookup"><span data-stu-id="ee087-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="ee087-461">除了创建自定义浏览器定义提供程序并动态创建新的浏览器定义以外，还可以使用其他功能来扩展现有的浏览器定义。</span><span class="sxs-lookup"><span data-stu-id="ee087-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="ee087-462">这使你可以使用接近所需内容的定义，但仅缺少几个功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="ee087-463">为此，请执行下列步骤。</span><span class="sxs-lookup"><span data-stu-id="ee087-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="ee087-464">创建一个从*HttpCapabilitiesEvaluator*派生的类，它将重写*GetBrowserCapabilities*方法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="ee087-465">示例代码扩展现有的 ASP.NET *HttpCapabilitiesEvaluator*类，并通过使用以下代码获取与当前请求定义匹配的*HttpBrowserCapabilities*对象：</span><span class="sxs-lookup"><span data-stu-id="ee087-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="ee087-466">然后，代码可以添加或修改此浏览器的功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="ee087-467">可以通过两种方式来指定新的浏览器功能：</span><span class="sxs-lookup"><span data-stu-id="ee087-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="ee087-468">将键/值对添加到由*HttpCapabilitiesBase*对象的*功能*属性公开的*IDictionary*对象。</span><span class="sxs-lookup"><span data-stu-id="ee087-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="ee087-469">在上面的示例中，代码添加了一个名为 "多点触控" 的功能，其值为*true*。</span><span class="sxs-lookup"><span data-stu-id="ee087-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="ee087-470">设置*HttpCapabilitiesBase*对象的现有属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="ee087-471">在上面的示例中，代码将 "*帧*" 属性设置为 " *true*"。</span><span class="sxs-lookup"><span data-stu-id="ee087-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="ee087-472">此属性只是由*功能*属性公开的*IDictionary*对象的访问器。</span><span class="sxs-lookup"><span data-stu-id="ee087-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="ee087-473">请注意，此模型适用于*HttpBrowserCapabilities*的任何属性，包括控件适配器。</span><span class="sxs-lookup"><span data-stu-id="ee087-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="ee087-474">按照前面的过程中所述，将提供程序注册到应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="ee087-475">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="ee087-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="ee087-476">ASP.NET 4 添加了对使用 Web 窗体的路由的内置支持。</span><span class="sxs-lookup"><span data-stu-id="ee087-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="ee087-477">通过路由，你可以将应用程序配置为接受未映射到物理文件的请求 Url。</span><span class="sxs-lookup"><span data-stu-id="ee087-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="ee087-478">相反，你可以使用路由来定义对用户有意义的 Url，并可以帮助你的应用程序使用搜索引擎优化（SEO）。</span><span class="sxs-lookup"><span data-stu-id="ee087-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="ee087-479">例如，显示现有应用程序中的产品类别的页面的 URL 可能类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="ee087-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="ee087-480">通过使用路由，你可以将应用程序配置为接受以下 URL 来呈现相同的信息：</span><span class="sxs-lookup"><span data-stu-id="ee087-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="ee087-481">从 ASP.NET 3.5 SP1 开始，路由已可用。</span><span class="sxs-lookup"><span data-stu-id="ee087-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="ee087-482">（有关如何在 ASP.NET 3.5 SP1 中使用路由的示例，请参阅 Phil Haack 的博客上的[使用 WebForms 路由](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "此项的标题。")的条目。）但是，ASP.NET 4 包含一些使使用路由更容易的功能，其中包括：</span><span class="sxs-lookup"><span data-stu-id="ee087-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.") on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="ee087-483">*PageRouteHandler*类，它是在定义路由时使用的简单 HTTP 处理程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-483">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="ee087-484">类将数据传递到请求路由到的页面。</span><span class="sxs-lookup"><span data-stu-id="ee087-484">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="ee087-485">新属性*HttpRequest RequestContext*和*RouteData* （这是*HttpRequest* RequestContext 对象的代理）。</span><span class="sxs-lookup"><span data-stu-id="ee087-485">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="ee087-486">通过这些属性，可更轻松地访问从路由传递的信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-486">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="ee087-487">下面是在*RouteUrlExpressionBuilder*和*RouteValueExpressionBuilder*中定义的以下新的表达式生成器：）：</span><span class="sxs-lookup"><span data-stu-id="ee087-487">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="ee087-488">*RouteUrl*，它提供了一种简单的方法来创建与 ASP.NET 服务器控件内的路由 url 相对应的 url。</span><span class="sxs-lookup"><span data-stu-id="ee087-488">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="ee087-489">*RouteValue*，它提供了一种从*RouteContext*对象中提取信息的简单方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-489">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="ee087-490">*RouteParameter*类，可更轻松地将*RouteContext*对象中包含的数据传递到数据源控件的查询（类似于[*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="ee087-490">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="ee087-491">Web 窗体页的路由</span><span class="sxs-lookup"><span data-stu-id="ee087-491">Routing for Web Forms Pages</span></span>

<span data-ttu-id="ee087-492">下面的示例演示如何使用*路由*类的新的*MapPageRoute*方法定义 Web 窗体路由：</span><span class="sxs-lookup"><span data-stu-id="ee087-492">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="ee087-493">ASP.NET 4 引入了*MapPageRoute*方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-493">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="ee087-494">下面的示例与上一示例中所示的 SearchRoute 定义等效，但使用*PageRouteHandler*类。</span><span class="sxs-lookup"><span data-stu-id="ee087-494">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="ee087-495">该示例中的代码将路由映射到一个物理页面（在第一个路由中），以 `~/search.aspx`。</span><span class="sxs-lookup"><span data-stu-id="ee087-495">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="ee087-496">第一个路由定义还指定了应从 URL 中提取名为 searchterm 的参数并将其传递到页面。</span><span class="sxs-lookup"><span data-stu-id="ee087-496">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="ee087-497">*MapPageRoute*方法支持以下方法重载：</span><span class="sxs-lookup"><span data-stu-id="ee087-497">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="ee087-498">*MapPageRoute （string routeName，string routeUrl，string physicalFile，bool checkPhysicalUrlAccess）*</span><span class="sxs-lookup"><span data-stu-id="ee087-498">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="ee087-499">*MapPageRoute （string routeName，string routeUrl，string physicalFile，bool checkPhysicalUrlAccess，RouteValueDictionary 默认值）*</span><span class="sxs-lookup"><span data-stu-id="ee087-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="ee087-500">*MapPageRoute （string routeName，string routeUrl，string physicalFile，bool checkPhysicalUrlAccess，RouteValueDictionary 默认值，RouteValueDictionary 约束）*</span><span class="sxs-lookup"><span data-stu-id="ee087-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="ee087-501">*CheckPhysicalUrlAccess*参数指定路由是否应检查要路由到的物理页面的安全权限（在本例中为 searchterm），以及对传入 URL 的权限（在本例中为 search/{}）。</span><span class="sxs-lookup"><span data-stu-id="ee087-501">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="ee087-502">如果*checkPhysicalUrlAccess*的值为*false*，则仅检查传入 URL 的权限。</span><span class="sxs-lookup"><span data-stu-id="ee087-502">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="ee087-503">使用如下设置在 `Web.config` 文件中定义这些权限：</span><span class="sxs-lookup"><span data-stu-id="ee087-503">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="ee087-504">在示例配置中，拒绝访问除管理员角色中的用户以外的所有用户的物理页面 `search.aspx`。</span><span class="sxs-lookup"><span data-stu-id="ee087-504">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="ee087-505">如果将*checkPhysicalUrlAccess*参数设置为*true* （默认值），则仅允许管理员用户访问 URL/search/{searchterm}，因为物理页面搜索 .aspx 仅限于该角色中的用户。</span><span class="sxs-lookup"><span data-stu-id="ee087-505">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="ee087-506">如果将*checkPhysicalUrlAccess*设置为*false* ，并按前面的示例所示配置了站点，则允许所有经过身份验证的用户访问 URL/search/{searchterm}。</span><span class="sxs-lookup"><span data-stu-id="ee087-506">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="ee087-507">在 Web 窗体页中读取路由信息</span><span class="sxs-lookup"><span data-stu-id="ee087-507">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="ee087-508">在 "Web 窗体" 物理页的代码中，可以使用两个新属性（或其他对象已添加到*RouteData*对象的其他信息）来访问路由已从 URL 中提取的信息： *RequestContext*和*RouteData*。</span><span class="sxs-lookup"><span data-stu-id="ee087-508">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="ee087-509">（*RouteData*包装 HttpRequest. *RequestContext. RouteData*.）下面的示例演示如何使用*RouteData*。</span><span class="sxs-lookup"><span data-stu-id="ee087-509">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="ee087-510">此代码提取为 searchterm 参数传递的值，如前面的示例路由中所定义的那样。</span><span class="sxs-lookup"><span data-stu-id="ee087-510">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="ee087-511">请考虑以下请求 URL：</span><span class="sxs-lookup"><span data-stu-id="ee087-511">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="ee087-512">发出此请求时，将在 "`search.aspx`" 页中呈现 "scott" 一词。</span><span class="sxs-lookup"><span data-stu-id="ee087-512">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="ee087-513">访问标记中的路由信息</span><span class="sxs-lookup"><span data-stu-id="ee087-513">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="ee087-514">上一部分中所述的方法演示如何在 Web 窗体页中的代码中获取路由数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-514">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="ee087-515">你还可以使用标记中的表达式，这些表达式可让你访问相同的信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-515">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="ee087-516">表达式生成器是一种功能强大且巧妙的方法来处理声明性代码。</span><span class="sxs-lookup"><span data-stu-id="ee087-516">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="ee087-517">（有关详细信息，请参阅 Phil Haack 的博客上的入门[版自定义表达式生成器](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)。）</span><span class="sxs-lookup"><span data-stu-id="ee087-517">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="ee087-518">ASP.NET 4 包含用于 Web 窗体路由的两个新表达式生成器。</span><span class="sxs-lookup"><span data-stu-id="ee087-518">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="ee087-519">下面的示例演示如何使用它们。</span><span class="sxs-lookup"><span data-stu-id="ee087-519">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="ee087-520">在此示例中， *RouteUrl*表达式用于定义基于路由参数的 URL。</span><span class="sxs-lookup"><span data-stu-id="ee087-520">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="ee087-521">这使你无需将完整的 URL 硬编码为标记，并使你可以在以后更改 URL 结构，而无需更改此链接。</span><span class="sxs-lookup"><span data-stu-id="ee087-521">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="ee087-522">根据前面定义的路由，此标记生成以下 URL：</span><span class="sxs-lookup"><span data-stu-id="ee087-522">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="ee087-523">ASP.NET 根据输入参数自动处理正确的路由（也就是说，它会生成正确的 URL）。</span><span class="sxs-lookup"><span data-stu-id="ee087-523">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="ee087-524">您还可以在表达式中包含一个路由名称，这允许您指定要使用的路由。</span><span class="sxs-lookup"><span data-stu-id="ee087-524">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="ee087-525">下面的示例演示如何使用*RouteValue*表达式。</span><span class="sxs-lookup"><span data-stu-id="ee087-525">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="ee087-526">当包含此控件的页运行时，值 "scott" 将显示在标签中。</span><span class="sxs-lookup"><span data-stu-id="ee087-526">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="ee087-527">使用*RouteValue*表达式可以轻松地在标记中使用路由数据，并避免在标记中使用更复杂的 RouteData ["x"] 语法。</span><span class="sxs-lookup"><span data-stu-id="ee087-527">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="ee087-528">对数据源控件参数使用路由数据</span><span class="sxs-lookup"><span data-stu-id="ee087-528">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="ee087-529">使用*RouteParameter*类可以将路由数据指定为数据源控件中查询的参数值。</span><span class="sxs-lookup"><span data-stu-id="ee087-529">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="ee087-530">它[的工作方式非常类似](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)于类，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-530">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="ee087-531">在这种情况下，路由参数 searchterm 的值将用于*Select*语句中的 @companyname 参数。</span><span class="sxs-lookup"><span data-stu-id="ee087-531">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the *Select* statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="ee087-532">设置客户端 Id</span><span class="sxs-lookup"><span data-stu-id="ee087-532">Setting Client IDs</span></span>

<span data-ttu-id="ee087-533">新的*ClientIDMode*属性解决了 ASP.NET 中的长期问题，即控件如何为其呈现的元素创建*id*属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-533">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="ee087-534">如果你的应用程序包括引用这些元素的客户端脚本，则了解呈现元素的*id*属性是很重要的。</span><span class="sxs-lookup"><span data-stu-id="ee087-534">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="ee087-535">为 Web 服务器控件呈现的 HTML 中的*id*属性是根据控件的*ClientID*属性生成的。</span><span class="sxs-lookup"><span data-stu-id="ee087-535">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="ee087-536">在 ASP.NET 4 之前，从*ClientID*属性生成*id*属性的算法已将命名容器（若有）与 id 连接在一起，在重复控件（如数据控件）的情况下，可以添加前缀和序列号。</span><span class="sxs-lookup"><span data-stu-id="ee087-536">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="ee087-537">虽然这始终保证页面中控件的 Id 是唯一的，但算法导致了不可预测的控件 Id，因此很难在客户端脚本中引用它们。</span><span class="sxs-lookup"><span data-stu-id="ee087-537">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="ee087-538">新的*ClientIDMode*属性使你可以更精确地指定为控件生成客户端 ID 的方式。</span><span class="sxs-lookup"><span data-stu-id="ee087-538">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="ee087-539">可以为任何控件设置*ClientIDMode*属性，包括页面的。</span><span class="sxs-lookup"><span data-stu-id="ee087-539">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="ee087-540">可能的设置如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-540">Possible settings are the following:</span></span>

- <span data-ttu-id="ee087-541">*AutoID* –这等效于用于生成*ClientID*属性值的算法，该算法在早期版本的 ASP.NET 中使用。</span><span class="sxs-lookup"><span data-stu-id="ee087-541">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="ee087-542">*Static* –指定*ClientID*值将与 id 相同，而不会连接父命名容器的 id。</span><span class="sxs-lookup"><span data-stu-id="ee087-542">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="ee087-543">这对于 Web 用户控件很有用。</span><span class="sxs-lookup"><span data-stu-id="ee087-543">This can be useful in Web user controls.</span></span> <span data-ttu-id="ee087-544">由于 Web 用户控件可以位于不同的页上和不同的容器控件中，因此很难为使用*AutoID*算法的控件编写客户端脚本，因为你无法预测 ID 值将是什么。</span><span class="sxs-lookup"><span data-stu-id="ee087-544">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="ee087-545">*可预测*–此选项主要用于使用重复模板的数据控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-545">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="ee087-546">它连接控件的命名容器的 ID 属性，但生成的*ClientID*值不包含类似于 "ctlxxx" 的字符串。</span><span class="sxs-lookup"><span data-stu-id="ee087-546">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="ee087-547">此设置与控件的*ClientIDRowSuffix*属性结合使用。</span><span class="sxs-lookup"><span data-stu-id="ee087-547">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="ee087-548">将*ClientIDRowSuffix*属性设置为数据字段的名称，该字段的值将用作生成的*ClientID*值的后缀。</span><span class="sxs-lookup"><span data-stu-id="ee087-548">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="ee087-549">通常使用数据记录的主键作为*ClientIDRowSuffix*值。</span><span class="sxs-lookup"><span data-stu-id="ee087-549">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="ee087-550">*Inherit* –此设置是控件的默认行为;它指定控件的 ID 生成与其父级相同。</span><span class="sxs-lookup"><span data-stu-id="ee087-550">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="ee087-551">可以在页级别设置*ClientIDMode*属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-551">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="ee087-552">这会为当前页中的所有控件定义默认的*ClientIDMode*值。</span><span class="sxs-lookup"><span data-stu-id="ee087-552">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="ee087-553">页面级别的默认*ClientIDMode*值为*AutoID*，并且控件级别的默认*ClientIDMode*值将*继承*。</span><span class="sxs-lookup"><span data-stu-id="ee087-553">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="ee087-554">因此，如果你未在代码中的任何位置设置此属性，则所有控件将默认为*AutoID*算法。</span><span class="sxs-lookup"><span data-stu-id="ee087-554">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="ee087-555">在 *@ page*指令中设置页面级别的值，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-555">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="ee087-556">你还可以在配置文件中的 "计算机" 级别或应用程序级别上设置*ClientIDMode*值。</span><span class="sxs-lookup"><span data-stu-id="ee087-556">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="ee087-557">这将为应用程序中所有页面上的所有控件定义默认的*ClientIDMode*设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-557">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="ee087-558">如果在计算机级别设置了值，则它将为该计算机上的所有网站定义默认的*ClientIDMode*设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-558">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="ee087-559">下面的示例演示配置文件中的*ClientIDMode*设置：</span><span class="sxs-lookup"><span data-stu-id="ee087-559">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="ee087-560">如前文所述， *ClientID*属性的值派生自控件父对象的命名容器。</span><span class="sxs-lookup"><span data-stu-id="ee087-560">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="ee087-561">在某些情况下，例如在使用母版页时，控件可能最终会生成类似于以下呈现的 HTML 中的 Id：</span><span class="sxs-lookup"><span data-stu-id="ee087-561">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="ee087-562">尽管标记中显示的*输入*元素（来自*TextBox*控件）在页面（嵌套的*ContentPlaceholder*控件）中仅有两个深层命名容器，但最终结果是一个控件 ID，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-562">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="ee087-563">此 ID 在页面中是唯一的，但在大多数情况下不必要太长。</span><span class="sxs-lookup"><span data-stu-id="ee087-563">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="ee087-564">假设您想要减少呈现的 ID 的长度，并对生成该 ID 的方式具有更大的控制权。</span><span class="sxs-lookup"><span data-stu-id="ee087-564">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="ee087-565">（例如，您想要消除 "ctlxxx" 前缀。）实现此目的的最简单方法是设置*ClientIDMode*属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-565">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="ee087-566">在此示例中，最外面的*NamingPanel*元素的*ClientIDMode*属性设置为*Static* ，并将内层*NamingControl*元素设置为*可预测*。</span><span class="sxs-lookup"><span data-stu-id="ee087-566">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="ee087-567">这些设置会生成以下标记（页面的其余部分和母版页假定为与上一示例中的相同）：</span><span class="sxs-lookup"><span data-stu-id="ee087-567">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="ee087-568">*静态*设置具有重置最外面的*NamingPanel*元素中的任何控件的命名层次结构，以及从生成的 id 中删除*ContentPlaceHolder*和*MasterPage* id 的效果。</span><span class="sxs-lookup"><span data-stu-id="ee087-568">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="ee087-569">（所呈现元素的*name*属性不受影响，因此会为事件、视图状态等保留正常的 ASP.NET 功能。）重置命名层次结构的副作用是，即使将*NamingPanel*元素的标记移到不同的*ContentPlaceholder*控件，呈现的客户端 id 仍保持不变。</span><span class="sxs-lookup"><span data-stu-id="ee087-569">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="ee087-570">请注意，您需要确保呈现的控件 Id 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ee087-570">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="ee087-571">如果不是，则它可能会中断任何需要单独 HTML 元素的唯一 Id 的功能，如客户端*document.getelementbyid*函数。</span><span class="sxs-lookup"><span data-stu-id="ee087-571">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="ee087-572">在数据绑定控件中创建可预测的客户端 Id</span><span class="sxs-lookup"><span data-stu-id="ee087-572">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="ee087-573">旧算法为数据绑定列表控件中的控件生成的*ClientID*值可能很长，而且不是真正可预测的。</span><span class="sxs-lookup"><span data-stu-id="ee087-573">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="ee087-574">*ClientIDMode*功能可帮助你更好地控制如何生成这些 id。</span><span class="sxs-lookup"><span data-stu-id="ee087-574">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="ee087-575">以下示例中的标记包含*ListView*控件：</span><span class="sxs-lookup"><span data-stu-id="ee087-575">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="ee087-576">在上面的示例中， *ClientIDMode*和*RowClientIDRowSuffix*属性在标记中设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-576">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="ee087-577">*ClientIDRowSuffix*属性只能在数据绑定控件中使用，它的行为因所使用的控件而异。</span><span class="sxs-lookup"><span data-stu-id="ee087-577">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="ee087-578">不同之处如下：</span><span class="sxs-lookup"><span data-stu-id="ee087-578">The differences are these:</span></span>

- <span data-ttu-id="ee087-579">*GridView*控件-可以指定数据源中的一个或多个列的名称，这些列在运行时组合在一起以创建客户端 id。</span><span class="sxs-lookup"><span data-stu-id="ee087-579">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="ee087-580">例如，如果将*RowClientIDRowSuffix*设置为 "ProductName，ProductId"，则呈现元素的控件 id 将具有如下格式：</span><span class="sxs-lookup"><span data-stu-id="ee087-580">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="ee087-581">*ListView*控件-可以指定数据源中追加到客户端 ID 的单个列。</span><span class="sxs-lookup"><span data-stu-id="ee087-581">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="ee087-582">例如，如果将*ClientIDRowSuffix*设置为 "ProductName"，则呈现的控件 id 的格式将如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-582">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="ee087-583">在这种情况下，尾随1是从当前数据项的产品 ID 派生的。</span><span class="sxs-lookup"><span data-stu-id="ee087-583">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="ee087-584">*Repeater*控件—此控件不支持*ClientIDRowSuffix*属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-584">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="ee087-585">在*Repeater*控件中，使用当前行的索引。</span><span class="sxs-lookup"><span data-stu-id="ee087-585">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="ee087-586">将 ClientIDMode = "可预测" 与*Repeater*控件一起使用时，将生成具有以下格式的客户端 id：</span><span class="sxs-lookup"><span data-stu-id="ee087-586">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="ee087-587">尾随0是当前行的索引。</span><span class="sxs-lookup"><span data-stu-id="ee087-587">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="ee087-588">*FormView*和*DetailsView*控件不显示多行，因此它们不支持*ClientIDRowSuffix*属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-588">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="ee087-589">保持数据控件中的行选择</span><span class="sxs-lookup"><span data-stu-id="ee087-589">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="ee087-590">*GridView*和*ListView*控件可以让用户选择行。</span><span class="sxs-lookup"><span data-stu-id="ee087-590">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="ee087-591">在以前版本的 ASP.NET 中，选择已基于页面上的行索引。</span><span class="sxs-lookup"><span data-stu-id="ee087-591">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="ee087-592">例如，如果在第1页上选择第三项，然后移至第2页，则将选中该页上的第三项。</span><span class="sxs-lookup"><span data-stu-id="ee087-592">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="ee087-593">仅在 .NET Framework 3.5 SP1 中的动态数据项目中最初支持暂留选择。</span><span class="sxs-lookup"><span data-stu-id="ee087-593">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="ee087-594">启用此功能时，当前所选项将基于项的数据键。</span><span class="sxs-lookup"><span data-stu-id="ee087-594">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="ee087-595">这意味着，如果您在第1页上选择第三行并移动到第2页，则第2页上不会选择任何内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-595">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="ee087-596">向后移动到第1页时，第三行仍处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="ee087-596">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="ee087-597">现在，所有项目*中的* *GridView*和*ListView*控件都支持持久化选择，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-597">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="ee087-598">ASP.NET 图表控件</span><span class="sxs-lookup"><span data-stu-id="ee087-598">ASP.NET Chart Control</span></span>

<span data-ttu-id="ee087-599">ASP.NET*图表*控件展开 .NET Framework 中的数据可视化产品。</span><span class="sxs-lookup"><span data-stu-id="ee087-599">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="ee087-600">使用*图表*控件，可以创建 ASP.NET 页面，它们具有直观且引人注目的图表，可用于复杂的统计或财务分析。</span><span class="sxs-lookup"><span data-stu-id="ee087-600">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="ee087-601">ASP.NET*图表*控件作为 .NET Framework 版本 3.5 SP1 版本的外接程序引入，并且属于 .NET Framework 4 版本。</span><span class="sxs-lookup"><span data-stu-id="ee087-601">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="ee087-602">控件包含以下功能：</span><span class="sxs-lookup"><span data-stu-id="ee087-602">The control includes the following features:</span></span>

- <span data-ttu-id="ee087-603">35 种不同的图表类型。</span><span class="sxs-lookup"><span data-stu-id="ee087-603">35 distinct chart types.</span></span>
- <span data-ttu-id="ee087-604">不限数量的图表区、标题、图例和批注。</span><span class="sxs-lookup"><span data-stu-id="ee087-604">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="ee087-605">适用于所有图表元素的各种外观设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-605">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="ee087-606">三维支持大多数图表类型。</span><span class="sxs-lookup"><span data-stu-id="ee087-606">3-D support for most chart types.</span></span>
- <span data-ttu-id="ee087-607">可自动适应数据点的智能数据标签。</span><span class="sxs-lookup"><span data-stu-id="ee087-607">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="ee087-608">条带线、刻度分隔线和对数刻度。</span><span class="sxs-lookup"><span data-stu-id="ee087-608">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="ee087-609">包含 50 多个用于数据分析和转换的财务和统计公式。</span><span class="sxs-lookup"><span data-stu-id="ee087-609">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="ee087-610">简单的图表数据绑定和操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-610">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="ee087-611">支持常用数据格式（如日期、时间和货币）。</span><span class="sxs-lookup"><span data-stu-id="ee087-611">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="ee087-612">支持交互和事件驱动的自定义，包括使用 Ajax 的客户端 click 事件。</span><span class="sxs-lookup"><span data-stu-id="ee087-612">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="ee087-613">状态管理。</span><span class="sxs-lookup"><span data-stu-id="ee087-613">State management.</span></span>
- <span data-ttu-id="ee087-614">二进制流。</span><span class="sxs-lookup"><span data-stu-id="ee087-614">Binary streaming.</span></span>

<span data-ttu-id="ee087-615">下图显示了 ASP.NET 图表控件生成的财务图表的示例。</span><span class="sxs-lookup"><span data-stu-id="ee087-615">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="ee087-616">图2： ASP.NET 图表控件示例</span><span class="sxs-lookup"><span data-stu-id="ee087-616">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="ee087-617">有关如何使用 ASP.NET 图表控件的更多示例，请在 MSDN 网站上的[Microsoft 图表控件的示例环境](https://go.microsoft.com/fwlink/?LinkId=128300)中下载示例代码。</span><span class="sxs-lookup"><span data-stu-id="ee087-617">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="ee087-618">可以在[图表控件论坛](https://go.microsoft.com/fwlink/?LinkId=128713)上找到更多社区内容示例。</span><span class="sxs-lookup"><span data-stu-id="ee087-618">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="ee087-619">向 ASP.NET 页添加图表控件</span><span class="sxs-lookup"><span data-stu-id="ee087-619">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="ee087-620">下面的示例演示如何使用标记将*图表*控件添加到 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="ee087-620">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="ee087-621">在此示例中，*图表*控件为静态数据点生成柱形图。</span><span class="sxs-lookup"><span data-stu-id="ee087-621">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="ee087-622">使用三维图表</span><span class="sxs-lookup"><span data-stu-id="ee087-622">Using 3-D Charts</span></span>

<span data-ttu-id="ee087-623">*Chart*控件包含*ChartAreas*集合，该集合可以包含定义图表区特征的*ChartArea*对象。</span><span class="sxs-lookup"><span data-stu-id="ee087-623">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="ee087-624">例如，若要对图表区使用三维，请使用*Area3DStyle*属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-624">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="ee087-625">下图显示了一个三维图表，其中包含四系列*条形*图类型。</span><span class="sxs-lookup"><span data-stu-id="ee087-625">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="ee087-626">图 3: 3-D 条形图</span><span class="sxs-lookup"><span data-stu-id="ee087-626">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="ee087-627">使用刻度分隔线和对数刻度</span><span class="sxs-lookup"><span data-stu-id="ee087-627">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="ee087-628">刻度分隔线和对数刻度是向图表添加复杂的两种附加方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-628">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="ee087-629">这些功能特定于图表区域中的每个轴。</span><span class="sxs-lookup"><span data-stu-id="ee087-629">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="ee087-630">例如，若要在图表区域的主 Y 轴上使用这些功能，请在*ChartArea*对象中使用*IsLogarithmic*和*ScaleBreakStyle*属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-630">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="ee087-631">以下代码片段演示如何在主 Y 轴上使用刻度分隔线。</span><span class="sxs-lookup"><span data-stu-id="ee087-631">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="ee087-632">下图显示了启用了刻度分隔线的 Y 轴。</span><span class="sxs-lookup"><span data-stu-id="ee087-632">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="ee087-633">图4：刻度分隔线</span><span class="sxs-lookup"><span data-stu-id="ee087-633">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="ee087-634">用 QueryExtender 控件筛选数据</span><span class="sxs-lookup"><span data-stu-id="ee087-634">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="ee087-635">对于创建数据驱动网页的开发人员而言，一项非常常见的任务就是筛选数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-635">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="ee087-636">这通常是通过在数据源控件中生成*Where*子句来执行的。</span><span class="sxs-lookup"><span data-stu-id="ee087-636">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="ee087-637">这种方法可能比较复杂，在某些情况下， *Where*语法不允许你利用基础数据库的全部功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-637">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="ee087-638">为了更轻松地进行筛选，在 ASP.NET 4 中添加了一个新的*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-638">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="ee087-639">此控件可以添加到*EntityDataSource*或*LinqDataSource*控件中，以便筛选这些控件返回的数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-639">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="ee087-640">由于*QueryExtender*控件依赖于 LINQ，因此在将数据发送到页面之前，将在数据库服务器上应用筛选器，这会产生非常高效的操作。</span><span class="sxs-lookup"><span data-stu-id="ee087-640">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="ee087-641">*QueryExtender*控件支持多种筛选选项。</span><span class="sxs-lookup"><span data-stu-id="ee087-641">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="ee087-642">以下各节介绍了这些选项，并提供有关如何使用这些选项的示例。</span><span class="sxs-lookup"><span data-stu-id="ee087-642">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="ee087-643">搜索</span><span class="sxs-lookup"><span data-stu-id="ee087-643">Search</span></span>

<span data-ttu-id="ee087-644">对于 search 选项， *QueryExtender*控件在指定字段中执行搜索。</span><span class="sxs-lookup"><span data-stu-id="ee087-644">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="ee087-645">在下面的示例中，控件使用在 TextBoxSearch 控件中输入的文本，并在 `ProductName` 中搜索其内容，并 `Supplier.CompanyName` 从*LinqDataSource*控件返回的数据中的列。</span><span class="sxs-lookup"><span data-stu-id="ee087-645">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="ee087-646">范围</span><span class="sxs-lookup"><span data-stu-id="ee087-646">Range</span></span>

<span data-ttu-id="ee087-647">范围选项与搜索选项类似，但指定了一对值来定义范围。</span><span class="sxs-lookup"><span data-stu-id="ee087-647">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="ee087-648">在下面的示例中， *QueryExtender*控件搜索从*LinqDataSource*控件返回的数据中的 `UnitPrice` 列。</span><span class="sxs-lookup"><span data-stu-id="ee087-648">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="ee087-649">从页面上的 TextBoxFrom 和 TextBoxTo 控件读取范围。</span><span class="sxs-lookup"><span data-stu-id="ee087-649">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="ee087-650">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="ee087-650">PropertyExpression</span></span>

<span data-ttu-id="ee087-651">使用 "属性表达式" 选项可以定义与属性值的比较。</span><span class="sxs-lookup"><span data-stu-id="ee087-651">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="ee087-652">如果表达式的计算结果为*true*，则返回正在检查的数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-652">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="ee087-653">在下面的示例中， *QueryExtender*控件通过将 `Discontinued` 列中的数据与页面上的 CheckBoxDiscontinued 控件中的值进行比较来筛选数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-653">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="ee087-654">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="ee087-654">CustomExpression</span></span>

<span data-ttu-id="ee087-655">最后，您可以指定要用于*QueryExtender*控件的自定义表达式。</span><span class="sxs-lookup"><span data-stu-id="ee087-655">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="ee087-656">使用此选项可以在定义自定义筛选器逻辑的页面中调用函数。</span><span class="sxs-lookup"><span data-stu-id="ee087-656">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="ee087-657">下面的示例演示如何以声明方式在*QueryExtender*控件中指定自定义表达式。</span><span class="sxs-lookup"><span data-stu-id="ee087-657">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="ee087-658">下面的示例演示*QueryExtender*控件调用的自定义函数。</span><span class="sxs-lookup"><span data-stu-id="ee087-658">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="ee087-659">在这种情况下，代码使用 LINQ 查询来筛选数据，而不是使用包含*Where*子句的数据库查询。</span><span class="sxs-lookup"><span data-stu-id="ee087-659">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="ee087-660">这些示例一次只显示一个在*QueryExtender*控件中使用的表达式。</span><span class="sxs-lookup"><span data-stu-id="ee087-660">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="ee087-661">但是，可以在*QueryExtender*控件内包含多个表达式。</span><span class="sxs-lookup"><span data-stu-id="ee087-661">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="ee087-662">Html 编码的代码表达式</span><span class="sxs-lookup"><span data-stu-id="ee087-662">Html Encoded Code Expressions</span></span>

<span data-ttu-id="ee087-663">某些 ASP.NET 站点（特别是 ASP.NET MVC）很大程度上依赖于使用 `<%`= `expression %>` 语法（通常称为 "代码片段"）来向响应中写入一些文本。</span><span class="sxs-lookup"><span data-stu-id="ee087-663">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="ee087-664">使用代码表达式时，很容易忘记对文本进行 HTML 编码，如果文本来自用户输入，则会使页面进入 XSS （跨站点脚本）攻击。</span><span class="sxs-lookup"><span data-stu-id="ee087-664">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="ee087-665">ASP.NET 4 引入了以下新的代码表达式语法：</span><span class="sxs-lookup"><span data-stu-id="ee087-665">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="ee087-666">此语法在写入响应时默认使用 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-666">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="ee087-667">此新表达式有效地转换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="ee087-667">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="ee087-668">例如，&lt;%： Request ["U s"]%&gt; 对*Request ["u s"]* 的值执行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-668">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="ee087-669">此功能的目的是为了能够将旧语法的所有实例替换为新语法，以便不会强制决定要使用的每个步骤。</span><span class="sxs-lookup"><span data-stu-id="ee087-669">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="ee087-670">但是，在某些情况下，输出文本应为 HTML 或已经过编码，在这种情况下，这可能会导致双重编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-670">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="ee087-671">对于这种情况，ASP.NET 4 引入了一个新接口*IHtmlString*，同时提供了具体的实现*HtmlString*。</span><span class="sxs-lookup"><span data-stu-id="ee087-671">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="ee087-672">通过这些类型的实例，你可以指示已正确编码（或以其他方式检查）返回值以使其显示为 HTML，因此不应再次对值进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="ee087-672">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="ee087-673">例如，以下内容不应为（并且不是） HTML 编码：</span><span class="sxs-lookup"><span data-stu-id="ee087-673">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="ee087-674">ASP.NET MVC 2 helper 方法已更新为使用此新语法，因此它们不是双精度编码，而只是在运行 ASP.NET 4 时。</span><span class="sxs-lookup"><span data-stu-id="ee087-674">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="ee087-675">当使用 ASP.NET 3.5 SP1 运行应用程序时，此新语法不起作用。</span><span class="sxs-lookup"><span data-stu-id="ee087-675">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="ee087-676">请记住，这不能保证防范 XSS 攻击。</span><span class="sxs-lookup"><span data-stu-id="ee087-676">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="ee087-677">例如，使用不在引号中的属性值的 HTML 可以包含仍然容易受到攻击的用户输入。</span><span class="sxs-lookup"><span data-stu-id="ee087-677">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="ee087-678">请注意，ASP.NET 控件和 ASP.NET MVC 帮助器的输出始终将属性值包含在引号中，这是建议的方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-678">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="ee087-679">同样，此语法不执行 JavaScript 编码，例如在基于用户输入创建 JavaScript 字符串时。</span><span class="sxs-lookup"><span data-stu-id="ee087-679">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="ee087-680">项目模板更改</span><span class="sxs-lookup"><span data-stu-id="ee087-680">Project Template Changes</span></span>

<span data-ttu-id="ee087-681">在早期版本的 ASP.NET 中，当你使用 Visual Studio 创建新的网站项目或 Web 应用程序项目时，生成的项目仅包含 default.aspx 页面、默认 `Web.config` 文件和 `App_Data` 文件夹，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-681">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="ee087-682">Visual Studio 还支持空白网站项目类型，不包含任何文件，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-682">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="ee087-683">结果就是，对于初学者来说，如何构建生产型 Web 应用程序非常少。</span><span class="sxs-lookup"><span data-stu-id="ee087-683">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="ee087-684">因此，ASP.NET 4 引入了三个新模板，一个用于空 Web 应用程序项目，另一个用于 Web 应用程序和网站项目。</span><span class="sxs-lookup"><span data-stu-id="ee087-684">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="ee087-685">空 Web 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="ee087-685">Empty Web Application Template</span></span>

<span data-ttu-id="ee087-686">顾名思义，空 Web 应用程序模板是一种被去除的 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="ee087-686">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="ee087-687">从 Visual Studio 的 "新建项目" 对话框中选择此项目模板，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-687">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="ee087-688">（[单击以查看完全大小的映像](overview/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="ee087-688">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="ee087-689">创建空的 ASP.NET Web 应用程序时，Visual Studio 会创建以下文件夹布局：</span><span class="sxs-lookup"><span data-stu-id="ee087-689">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="ee087-690">这类似于早期版本的 ASP.NET 的空白网站布局，但有一个例外。</span><span class="sxs-lookup"><span data-stu-id="ee087-690">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="ee087-691">在 Visual Studio 2010 中，空 Web 应用程序和空网站项目包含以下最小 `Web.config` 文件，其中包含 Visual Studio 用于标识项目所针对的框架的信息：</span><span class="sxs-lookup"><span data-stu-id="ee087-691">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="ee087-692">如果没有此*targetFramework*属性，Visual Studio 默认为面向 .NET Framework 2.0，以便在打开较旧的应用程序时保持兼容性。</span><span class="sxs-lookup"><span data-stu-id="ee087-692">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="ee087-693">Web 应用程序和网站项目模板</span><span class="sxs-lookup"><span data-stu-id="ee087-693">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="ee087-694">Visual Studio 2010 附带的其他两个新项目模板包含重大更改。</span><span class="sxs-lookup"><span data-stu-id="ee087-694">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="ee087-695">下图显示了在创建新的 Web 应用程序项目时创建的项目布局。</span><span class="sxs-lookup"><span data-stu-id="ee087-695">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="ee087-696">（网站项目的布局几乎完全相同。）</span><span class="sxs-lookup"><span data-stu-id="ee087-696">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="ee087-697">项目包含一些在早期版本中未创建的文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-697">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="ee087-698">此外，新的 Web 应用程序项目配置有基本成员资格功能，这使你可以快速开始保护新应用程序的访问。</span><span class="sxs-lookup"><span data-stu-id="ee087-698">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="ee087-699">由于此包含，新项目的 `Web.config` 文件包含用于配置成员资格、角色和配置文件的项。</span><span class="sxs-lookup"><span data-stu-id="ee087-699">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="ee087-700">下面的示例演示了用于新的 Web 应用程序项目的 `Web.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-700">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="ee087-701">（在这种情况下， *roleManager*处于禁用状态。）</span><span class="sxs-lookup"><span data-stu-id="ee087-701">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="ee087-702">（[单击以查看完全大小的映像](overview/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="ee087-702">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="ee087-703">项目还包含 `Account` 目录中的第二个 `Web.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-703">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="ee087-704">第二个配置文件提供了一种方法，用于保护对非登录用户的 ChangePassword 页的访问。</span><span class="sxs-lookup"><span data-stu-id="ee087-704">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="ee087-705">下面的示例显示第二个 `Web.config` 文件的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-705">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="ee087-706">默认情况下，在新项目模板中创建的页面还包含比早期版本更多的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-706">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="ee087-707">该项目包含一个默认母版页和 CSS 文件，默认页（default.aspx）默认配置为使用母版页。</span><span class="sxs-lookup"><span data-stu-id="ee087-707">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="ee087-708">结果是，当你首次运行 Web 应用程序或网站时，默认的（home）页已正常运行。</span><span class="sxs-lookup"><span data-stu-id="ee087-708">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="ee087-709">事实上，它类似于启动新 MVC 应用程序时看到的默认页面。</span><span class="sxs-lookup"><span data-stu-id="ee087-709">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="ee087-710">（[单击以查看完全大小的映像](overview/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="ee087-710">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="ee087-711">对项目模板进行这些更改的目的是提供有关如何开始构建新的 Web 应用程序的指导。</span><span class="sxs-lookup"><span data-stu-id="ee087-711">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="ee087-712">使用语义正确、严格符合 XHTML 1.0 的标记和使用 CSS 指定的布局时，模板中的页表示生成 ASP.NET 4 Web 应用程序的最佳实践。</span><span class="sxs-lookup"><span data-stu-id="ee087-712">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="ee087-713">默认页面还具有两列布局，你可以轻松地对其进行自定义。</span><span class="sxs-lookup"><span data-stu-id="ee087-713">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="ee087-714">例如，假设你要为新的 Web 应用程序更改某些颜色，并插入你的公司徽标来代替我的 ASP.NET 应用程序徽标。</span><span class="sxs-lookup"><span data-stu-id="ee087-714">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="ee087-715">为此，请在 `Content` 下创建一个新目录来存储徽标图像：</span><span class="sxs-lookup"><span data-stu-id="ee087-715">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="ee087-716">若要将图像添加到页面中，请打开 `Site.Master` 文件，查找 ASP.NET 应用程序文本的定义位置，并将其替换为其*src*属性设置为新徽标图像的*image*元素，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-716">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="ee087-717">（[单击以查看完全大小的映像](overview/_static/image22.png)）</span><span class="sxs-lookup"><span data-stu-id="ee087-717">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="ee087-718">然后，你可以转到 web.config 文件并修改 CSS 类定义，以更改页面的背景色以及页眉的背景色。</span><span class="sxs-lookup"><span data-stu-id="ee087-718">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="ee087-719">这些更改的结果是，可以使用非常少的精力显示自定义主页：</span><span class="sxs-lookup"><span data-stu-id="ee087-719">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="ee087-720">（[单击以查看完全大小的映像](overview/_static/image25.png)）</span><span class="sxs-lookup"><span data-stu-id="ee087-720">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="ee087-721">CSS 改进</span><span class="sxs-lookup"><span data-stu-id="ee087-721">CSS Improvements</span></span>

<span data-ttu-id="ee087-722">ASP.NET 4 中的主要工作区域之一是帮助呈现符合最新 HTML 标准的 HTML。</span><span class="sxs-lookup"><span data-stu-id="ee087-722">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="ee087-723">这包括对 ASP.NET Web 服务器控件使用 CSS 样式的方式的更改。</span><span class="sxs-lookup"><span data-stu-id="ee087-723">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="ee087-724">用于呈现的兼容性设置</span><span class="sxs-lookup"><span data-stu-id="ee087-724">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="ee087-725">默认情况下，如果 Web 应用程序或网站面向 .NET Framework 4，则*pages*元素的*controlRenderingCompatibilityVersion*属性将设置为 "4.0"。</span><span class="sxs-lookup"><span data-stu-id="ee087-725">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="ee087-726">此元素在计算机级 `Web.config` 文件中定义，并且默认情况下适用于所有 ASP.NET 4 应用程序：</span><span class="sxs-lookup"><span data-stu-id="ee087-726">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="ee087-727">*ControlRenderingCompatibility*的值是一个字符串，它允许将来的版本中可能出现新版本定义。</span><span class="sxs-lookup"><span data-stu-id="ee087-727">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="ee087-728">在当前版本中，此属性支持以下值：</span><span class="sxs-lookup"><span data-stu-id="ee087-728">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="ee087-729">"3.5".</span><span class="sxs-lookup"><span data-stu-id="ee087-729">"3.5".</span></span> <span data-ttu-id="ee087-730">此设置表示旧的呈现和标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-730">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="ee087-731">控件呈现的标记比向后兼容100%，并遵循*xhtmlConformance*属性的设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-731">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="ee087-732">"4.0".</span><span class="sxs-lookup"><span data-stu-id="ee087-732">"4.0".</span></span> <span data-ttu-id="ee087-733">如果属性具有此设置，ASP.NET Web 服务器控件将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ee087-733">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="ee087-734">*XhtmlConformance*属性始终被视为 "Strict"。</span><span class="sxs-lookup"><span data-stu-id="ee087-734">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="ee087-735">因此，控件呈现 XHTML 1.0 严格标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-735">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="ee087-736">禁用非输入控件将不再呈现无效样式。</span><span class="sxs-lookup"><span data-stu-id="ee087-736">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="ee087-737">现在，隐藏字段周围的*div*元素的样式为，因此它们不会干扰用户创建的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="ee087-737">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="ee087-738">Menu 控件呈现语义正确并符合辅助功能准则的标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-738">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="ee087-739">验证控件不呈现内联样式。</span><span class="sxs-lookup"><span data-stu-id="ee087-739">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="ee087-740">之前呈现的 border = "0" 的控件（从 ASP.NET*表*控件派生的控件和 ASP.NET*图像*控件）不再呈现此特性。</span><span class="sxs-lookup"><span data-stu-id="ee087-740">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="ee087-741">禁用控件</span><span class="sxs-lookup"><span data-stu-id="ee087-741">Disabling Controls</span></span>

<span data-ttu-id="ee087-742">在 ASP.NET 3.5 SP1 及更早版本中，框架在 HTML 标记中为其*Enabled*属性设置为*false*的任何控件呈现*已禁用*的特性。</span><span class="sxs-lookup"><span data-stu-id="ee087-742">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="ee087-743">但是，根据 HTML 4.01 规范，仅*输入*元素应具有此属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-743">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="ee087-744">在 ASP.NET 4 中，可以将*controlRenderingCompatibilityVersion*属性设置为 "3.5"，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-744">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="ee087-745">您可以为 "*标签*" 控件创建标记，如下所示，这将禁用控件：</span><span class="sxs-lookup"><span data-stu-id="ee087-745">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="ee087-746">"*标签*" 控件将呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="ee087-746">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="ee087-747">在 ASP.NET 4 中，可以将*controlRenderingCompatibilityVersion*设置为 "4.0"。</span><span class="sxs-lookup"><span data-stu-id="ee087-747">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* to "4.0".</span></span> <span data-ttu-id="ee087-748">在这种情况下，当控件的*Enabled*属性设置为*false*时，只有呈现*输入*元素的控件才会呈现*禁用*的特性。</span><span class="sxs-lookup"><span data-stu-id="ee087-748">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="ee087-749">不呈现 HTML*输入*元素的控件而是呈现一个引用 CSS 类的*类*特性，你可以使用该 CSS 类定义控件的禁用外观。</span><span class="sxs-lookup"><span data-stu-id="ee087-749">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="ee087-750">例如，在前面的示例中显示的*标签*控件将生成以下标记：</span><span class="sxs-lookup"><span data-stu-id="ee087-750">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="ee087-751">为此控件指定的类的默认值为 "aspNetDisabled"。</span><span class="sxs-lookup"><span data-stu-id="ee087-751">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="ee087-752">但是，可以通过设置*WebControl*类的静态*DisabledCssClass*静态属性来更改此默认值。</span><span class="sxs-lookup"><span data-stu-id="ee087-752">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="ee087-753">对于控件开发人员，还可以使用*SupportsDisabledAttribute*属性定义要用于特定控件的行为。</span><span class="sxs-lookup"><span data-stu-id="ee087-753">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="ee087-754">在隐藏字段周围隐藏 div 元素</span><span class="sxs-lookup"><span data-stu-id="ee087-754">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="ee087-755">ASP.NET 2.0 和更高版本会在*div*元素中呈现系统特定的隐藏字段（如用于存储视图状态信息的*隐藏*元素），以便符合 XHTML 标准。</span><span class="sxs-lookup"><span data-stu-id="ee087-755">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="ee087-756">但是，当 CSS 规则影响页面上的*div*元素时，这可能会导致问题。</span><span class="sxs-lookup"><span data-stu-id="ee087-756">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="ee087-757">例如，它可能会导致在隐藏的*div*元素周围出现一条像素的行。</span><span class="sxs-lookup"><span data-stu-id="ee087-757">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="ee087-758">在 ASP.NET 4 中，包含由 ASP.NET 生成的隐藏字段的*div*元素添加 CSS 类引用，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-758">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="ee087-759">然后，你可以定义仅适用于 ASP.NET 生成的*隐藏*元素的 CSS 类，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-759">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="ee087-760">为模板化控件呈现外部表</span><span class="sxs-lookup"><span data-stu-id="ee087-760">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="ee087-761">默认情况下，支持模板的以下 ASP.NET Web 服务器控件将自动包装在用于应用内联样式的外部表中：</span><span class="sxs-lookup"><span data-stu-id="ee087-761">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="ee087-762">*FormView*</span><span class="sxs-lookup"><span data-stu-id="ee087-762">*FormView*</span></span>
- <span data-ttu-id="ee087-763">*登录*</span><span class="sxs-lookup"><span data-stu-id="ee087-763">*Login*</span></span>
- <span data-ttu-id="ee087-764">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="ee087-764">*PasswordRecovery*</span></span>
- <span data-ttu-id="ee087-765">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="ee087-765">*ChangePassword*</span></span>
- <span data-ttu-id="ee087-766">*向导*</span><span class="sxs-lookup"><span data-stu-id="ee087-766">*Wizard*</span></span>
- <span data-ttu-id="ee087-767">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="ee087-767">*CreateUserWizard*</span></span>

<span data-ttu-id="ee087-768">已将名为*RenderOuterTable*的新属性添加到这些控件，这些控件允许从标记中删除外部表。</span><span class="sxs-lookup"><span data-stu-id="ee087-768">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="ee087-769">例如，请看下面的*FormView*控件示例：</span><span class="sxs-lookup"><span data-stu-id="ee087-769">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="ee087-770">此标记将向页面呈现以下输出，其中包含一个 HTML 表：</span><span class="sxs-lookup"><span data-stu-id="ee087-770">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="ee087-771">若要防止呈现表，可以设置*FormView*控件的*RenderOuterTable*属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-771">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="ee087-772">前面的示例将呈现以下输出，而不包含*table*、 *tr*和*td*元素：</span><span class="sxs-lookup"><span data-stu-id="ee087-772">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="ee087-773">内容</span><span class="sxs-lookup"><span data-stu-id="ee087-773">Content</span></span>

<span data-ttu-id="ee087-774">这种增强功能使你可以更轻松地使用 CSS 设置控件内容的样式，因为控件不呈现意外标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-774">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="ee087-775">请注意，此更改将禁用对 Visual Studio 2010 设计器中的自动格式化函数的支持，因为不再有可以承载由自动格式选项生成的样式属性的*table*元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-775">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="ee087-776">ListView 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="ee087-776">ListView Control Enhancements</span></span>

<span data-ttu-id="ee087-777">*ListView*控件已经更易于在 ASP.NET 4 中使用。</span><span class="sxs-lookup"><span data-stu-id="ee087-777">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="ee087-778">早期版本的控件要求您指定一个包含具有已知 ID 的服务器控件的布局模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-778">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="ee087-779">下面的标记显示了如何在 ASP.NET 3.5 中使用*ListView*控件的典型示例。</span><span class="sxs-lookup"><span data-stu-id="ee087-779">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="ee087-780">在 ASP.NET 4 中， *ListView*控件不需要布局模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-780">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="ee087-781">上一示例中所示的标记可以替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="ee087-781">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="ee087-782">CheckBoxList 和 RadioButtonList 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="ee087-782">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="ee087-783">在 ASP.NET 3.5 中，可以使用以下两个设置指定*CheckBoxList*和*RadioButtonList*的布局：</span><span class="sxs-lookup"><span data-stu-id="ee087-783">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="ee087-784">*Flow*。</span><span class="sxs-lookup"><span data-stu-id="ee087-784">*Flow*.</span></span> <span data-ttu-id="ee087-785">控件呈现*横跨*元素以包含其内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-785">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="ee087-786">*表*。</span><span class="sxs-lookup"><span data-stu-id="ee087-786">*Table*.</span></span> <span data-ttu-id="ee087-787">控件呈现一个*表*元素以包含其内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-787">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="ee087-788">下面的示例演示其中每个控件的标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-788">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="ee087-789">默认情况下，控件呈现的 HTML 类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="ee087-789">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="ee087-790">由于这些控件包含项的列表，因此为了呈现语义正确的 HTML，它们应使用 HTML 列表（*li*）元素呈现其内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-790">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="ee087-791">这使使用辅助技术阅读网页的用户更容易，并使控件更易于使用 CSS 进行样式。</span><span class="sxs-lookup"><span data-stu-id="ee087-791">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="ee087-792">在 ASP.NET 4 中， *CheckBoxList*和*RadioButtonList*控件支持*RepeatLayout*属性的以下新值：</span><span class="sxs-lookup"><span data-stu-id="ee087-792">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="ee087-793">*OrderedList* –内容在*ol*元素内呈现为*li*元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-793">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="ee087-794">*UnorderedList* –内容呈现为*ul*元素中的*li*元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-794">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="ee087-795">下面的示例演示如何使用这些新值。</span><span class="sxs-lookup"><span data-stu-id="ee087-795">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="ee087-796">上述标记生成以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="ee087-796">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="ee087-797">注意如果将*RepeatLayout*设置为*OrderedList*或*UnorderedList*，则不能再使用*RepeatDirection*属性，如果在标记或代码中设置了该属性，则会在运行时引发异常。</span><span class="sxs-lookup"><span data-stu-id="ee087-797">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="ee087-798">属性不具有值，因为这些控件的可视布局是使用 CSS 定义的。</span><span class="sxs-lookup"><span data-stu-id="ee087-798">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="ee087-799">菜单控件改进</span><span class="sxs-lookup"><span data-stu-id="ee087-799">Menu Control Improvements</span></span>

<span data-ttu-id="ee087-800">在 ASP.NET 4 之前， *Menu*控件呈现一系列 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="ee087-800">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="ee087-801">这使得在设置内联属性之外应用 CSS 样式变得更加困难，也不符合辅助功能标准。</span><span class="sxs-lookup"><span data-stu-id="ee087-801">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="ee087-802">在 ASP.NET 4 中，控件现在使用由无序列表和列表元素组成的语义标记呈现 HTML。</span><span class="sxs-lookup"><span data-stu-id="ee087-802">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="ee087-803">下面的示例演示了*菜单*控件的 ASP.NET 页中的标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-803">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="ee087-804">页面呈现时，控件将生成以下 HTML （为清楚起见，省略了*onclick*代码）：</span><span class="sxs-lookup"><span data-stu-id="ee087-804">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="ee087-805">除了呈现改进外，还可以使用焦点管理改进菜单键盘导航。</span><span class="sxs-lookup"><span data-stu-id="ee087-805">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="ee087-806">当*Menu*控件获得焦点时，可以使用箭头键来浏览元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-806">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="ee087-807">*Menu*控件现在还附加可访问的丰富 internet 应用程序（ARIA）角色和[属性 w，](http://www.w3.org/TR/wai-aria-practices/#menu "菜单 ARIA 指导原则")以提高可访问性。</span><span class="sxs-lookup"><span data-stu-id="ee087-807">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="ee087-808">Menu 控件的样式呈现在页面顶部的样式块中，而不是在包含呈现的 HTML 元素的行中。</span><span class="sxs-lookup"><span data-stu-id="ee087-808">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="ee087-809">如果要对控件的样式进行完全控制，则可以将新的*IncludeStyleBlock*属性设置为*false*，在这种情况下，不会发出样式块。</span><span class="sxs-lookup"><span data-stu-id="ee087-809">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="ee087-810">使用此属性的一种方法是使用 Visual Studio 设计器中的自动格式功能设置菜单的外观。</span><span class="sxs-lookup"><span data-stu-id="ee087-810">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="ee087-811">然后，可以运行页面，打开页面源，然后将呈现的样式块复制到外部 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-811">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="ee087-812">在 Visual Studio 中，撤消样式设置，并将*IncludeStyleBlock*设置为*false*。</span><span class="sxs-lookup"><span data-stu-id="ee087-812">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="ee087-813">结果就是使用外部样式表中的样式定义了菜单外观。</span><span class="sxs-lookup"><span data-stu-id="ee087-813">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="ee087-814">Wizard 和 CreateUserWizard 控件</span><span class="sxs-lookup"><span data-stu-id="ee087-814">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="ee087-815">ASP.NET*向导*和*CreateUserWizard*控件支持可用于定义其呈现的 HTML 的模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-815">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="ee087-816">（*CreateUserWizard*派生自*向导*。）下面的示例演示完全模板化*CreateUserWizard*控件的标记：</span><span class="sxs-lookup"><span data-stu-id="ee087-816">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="ee087-817">控件呈现的 HTML 类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="ee087-817">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="ee087-818">在 ASP.NET 3.5 SP1 中，尽管可以更改模板内容，但仍对*向导*控件的输出具有有限的控制。</span><span class="sxs-lookup"><span data-stu-id="ee087-818">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="ee087-819">在 ASP.NET 4 中，可以创建*LayoutTemplate*模板并插入*占位符*控件（使用保留名称）来指定*向导控件*的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="ee087-819">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="ee087-820">下面的示例演示了这一点：</span><span class="sxs-lookup"><span data-stu-id="ee087-820">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="ee087-821">该示例在*LayoutTemplate*元素中包含以下命名占位符：</span><span class="sxs-lookup"><span data-stu-id="ee087-821">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="ee087-822">*headerPlaceholder* –在运行时，这会替换为*system.windows.controls.headereditemscontrol.headertemplate*元素的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-822">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="ee087-823">*sideBarPlaceholder* –在运行时，这会替换为*SideBarTemplate*元素的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-823">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="ee087-824">*wizardStepPlaceHolder* –在运行时，这会替换为*WizardStepTemplate*元素的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-824">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="ee087-825">*navigationPlaceholder* –在运行时，这会替换为你定义的任何导航模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-825">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="ee087-826">使用占位符的示例中的标记会呈现以下 HTML （不包含模板中实际定义的内容）：</span><span class="sxs-lookup"><span data-stu-id="ee087-826">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="ee087-827">现在，唯一不是用户定义的 HTML 是*span*元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-827">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="ee087-828">（我们预计在将来的版本中，甚至不会呈现*span*元素。）现在，可以完全控制*向导*控件生成的所有内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-828">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="ee087-829">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ee087-829">ASP.NET MVC</span></span>

<span data-ttu-id="ee087-830">ASP.NET MVC 已作为外接程序框架引入到3月2009的 ASP.NET 3.5 SP1。</span><span class="sxs-lookup"><span data-stu-id="ee087-830">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="ee087-831">Visual Studio 2010 包括 ASP.NET MVC 2，其中包括新特性和功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-831">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="ee087-832">区域支持</span><span class="sxs-lookup"><span data-stu-id="ee087-832">Areas Support</span></span>

<span data-ttu-id="ee087-833">通过区域，你可以将控制器和视图分组到大型应用程序中与其他部分的相对隔离的部分。</span><span class="sxs-lookup"><span data-stu-id="ee087-833">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="ee087-834">每个区域均可作为单独的 ASP.NET MVC 项目实现，然后主应用程序可以引用该项目。</span><span class="sxs-lookup"><span data-stu-id="ee087-834">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="ee087-835">这有助于在构建大型应用程序时管理复杂性，使多个团队能够在单个应用程序中协同工作。</span><span class="sxs-lookup"><span data-stu-id="ee087-835">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="ee087-836">数据-批注属性验证支持</span><span class="sxs-lookup"><span data-stu-id="ee087-836">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="ee087-837">*DataAnnotations*特性使你可以通过使用元数据特性将验证逻辑附加到模型。</span><span class="sxs-lookup"><span data-stu-id="ee087-837">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="ee087-838">ASP.NET 3.5 SP1 中的 ASP.NET 动态数据引入了*DataAnnotations*属性。</span><span class="sxs-lookup"><span data-stu-id="ee087-838">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="ee087-839">这些属性已集成到默认模型联编程序中，并提供用于验证用户输入的元数据驱动的方法。</span><span class="sxs-lookup"><span data-stu-id="ee087-839">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="ee087-840">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="ee087-840">Templated Helpers</span></span>

<span data-ttu-id="ee087-841">模板化帮助器允许您自动将编辑和显示模板与数据类型相关联。</span><span class="sxs-lookup"><span data-stu-id="ee087-841">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="ee087-842">例如，您可以使用模板帮助器指定为*system.web*值自动呈现日期选取器 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-842">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="ee087-843">这类似于 ASP.NET 动态数据中的字段模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-843">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="ee087-844">*Html.editorfor*和*DisplayFor*帮助器方法为呈现标准数据类型以及具有多个属性的复杂对象提供内置支持。</span><span class="sxs-lookup"><span data-stu-id="ee087-844">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="ee087-845">它们还通过让你将数据批注特性（如*DisplayName*和*ScaffoldColumn* ）应用于*ViewModel*对象，从而自定义呈现。</span><span class="sxs-lookup"><span data-stu-id="ee087-845">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="ee087-846">通常需要进一步自定义 UI 帮助器的输出，并完全控制生成的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-846">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="ee087-847">*Html.editorfor*和*DisplayFor*帮助器方法使用模板化机制支持此功能，该机制允许您定义可以重写和控制呈现的输出的外部模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-847">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="ee087-848">可以为类单独呈现模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-848">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="ee087-849">Dynamic Data — 动态数据</span><span class="sxs-lookup"><span data-stu-id="ee087-849">Dynamic Data</span></span>

<span data-ttu-id="ee087-850">动态数据是 .NET Framework 在3.5 年 SP1 版本2008中引入的。</span><span class="sxs-lookup"><span data-stu-id="ee087-850">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="ee087-851">此功能为创建数据驱动的应用程序提供了许多增强功能，其中包括：</span><span class="sxs-lookup"><span data-stu-id="ee087-851">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="ee087-852">用于快速生成数据驱动的网站的 RAD 体验。</span><span class="sxs-lookup"><span data-stu-id="ee087-852">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="ee087-853">基于数据模型中定义的约束的自动验证。</span><span class="sxs-lookup"><span data-stu-id="ee087-853">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="ee087-854">通过使用动态数据项目中的字段模板，可以轻松更改为*GridView*和*DetailsView*控件中的字段生成的标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-854">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="ee087-855">注意有关详细信息，请参阅 MSDN Library 中的[动态数据文档](https://msdn.microsoft.com/library/cc488545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee087-855">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="ee087-856">对于 ASP.NET 4，动态数据已得到了增强，使开发人员能够更轻松地快速生成数据驱动的网站。</span><span class="sxs-lookup"><span data-stu-id="ee087-856">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="ee087-857">为现有项目启用动态数据</span><span class="sxs-lookup"><span data-stu-id="ee087-857">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="ee087-858">.NET Framework 3.5 SP1 随附的动态数据功能引入了以下新功能：</span><span class="sxs-lookup"><span data-stu-id="ee087-858">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="ee087-859">字段模板–它们为数据绑定控件提供基于数据类型的模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-859">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="ee087-860">字段模板提供了一种更简单的方法来自定义数据控件的外观，而不是使用每个字段的模板字段。</span><span class="sxs-lookup"><span data-stu-id="ee087-860">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="ee087-861">验证-动态数据允许你使用数据类上的属性为常见方案指定验证，如必填字段、范围检查、类型检查、使用正则表达式的模式匹配和自定义验证。</span><span class="sxs-lookup"><span data-stu-id="ee087-861">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="ee087-862">验证由数据控件强制执行。</span><span class="sxs-lookup"><span data-stu-id="ee087-862">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="ee087-863">不过，这些功能具有以下要求：</span><span class="sxs-lookup"><span data-stu-id="ee087-863">However, these features had the following requirements:</span></span>

- <span data-ttu-id="ee087-864">数据访问层必须基于实体框架或 LINQ to SQL。</span><span class="sxs-lookup"><span data-stu-id="ee087-864">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="ee087-865">这些功能唯一支持的数据源控件是*EntityDataSource*控件或*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-865">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="ee087-866">功能需要使用动态数据创建的 Web 项目或动态数据实体模板，才能拥有支持该功能所需的所有文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-866">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="ee087-867">ASP.NET 4 中动态数据支持的主要目标是为任何 ASP.NET 应用程序启用动态数据的新功能。</span><span class="sxs-lookup"><span data-stu-id="ee087-867">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="ee087-868">下面的示例演示可以利用现有页面中动态数据功能的控件的标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-868">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="ee087-869">在该页的代码中，必须添加以下代码才能为这些控件启用动态数据支持：</span><span class="sxs-lookup"><span data-stu-id="ee087-869">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="ee087-870">当*GridView*控件处于编辑模式时，动态数据自动验证输入的数据的格式是否正确。</span><span class="sxs-lookup"><span data-stu-id="ee087-870">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="ee087-871">如果不是，则显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="ee087-871">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="ee087-872">此功能还提供了其他优点，例如，能够指定插入模式的默认值。</span><span class="sxs-lookup"><span data-stu-id="ee087-872">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="ee087-873">如果没有动态数据，若要为字段实现默认值，则必须附加到事件，找到控件（使用*FindControl*），并设置其值。</span><span class="sxs-lookup"><span data-stu-id="ee087-873">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="ee087-874">在 ASP.NET 4 中， *EnableDynamicData*调用支持第二个参数，该参数可让你为对象上的任何字段传递默认值，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ee087-874">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="ee087-875">声明性 DynamicDataManager 控件语法</span><span class="sxs-lookup"><span data-stu-id="ee087-875">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="ee087-876">*DynamicDataManager*控件已增强，因此你可以通过声明方式配置它，就像在 ASP.NET 中的大多数控件（而不只是在代码中）一样。</span><span class="sxs-lookup"><span data-stu-id="ee087-876">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="ee087-877">*DynamicDataManager*控件的标记类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="ee087-877">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="ee087-878">此标记为*DynamicDataManager*控件的*先*节中引用的 GridView1 控件启用动态数据行为。</span><span class="sxs-lookup"><span data-stu-id="ee087-878">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="ee087-879">实体模板</span><span class="sxs-lookup"><span data-stu-id="ee087-879">Entity Templates</span></span>

<span data-ttu-id="ee087-880">实体模板提供了一种新的方法，用于自定义数据布局，而无需创建自定义页面。</span><span class="sxs-lookup"><span data-stu-id="ee087-880">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="ee087-881">页面模板使用*FormView*控件（而不是在早期版本的动态数据中的页模板中使用的*DetailsView*控件）和*DynamicEntity*控件来呈现实体模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-881">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="ee087-882">这使您可以更好地控制动态数据呈现的标记。</span><span class="sxs-lookup"><span data-stu-id="ee087-882">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="ee087-883">以下列表显示了包含实体模板的新项目目录布局：</span><span class="sxs-lookup"><span data-stu-id="ee087-883">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="ee087-884">`EntityTemplate` 目录包含用于显示数据模型对象的模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-884">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="ee087-885">默认情况下，对象是使用 `Default.ascx` 模板呈现的，该模板提供的标记与 ASP.NET 3.5 SP1 中动态数据使用的*DetailsView*控件所创建的标记类似。</span><span class="sxs-lookup"><span data-stu-id="ee087-885">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="ee087-886">下面的示例演示 `Default.ascx` 控件的标记：</span><span class="sxs-lookup"><span data-stu-id="ee087-886">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="ee087-887">可以编辑默认模板来更改整个站点的外观。</span><span class="sxs-lookup"><span data-stu-id="ee087-887">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="ee087-888">有用于显示、编辑和插入操作的模板。</span><span class="sxs-lookup"><span data-stu-id="ee087-888">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="ee087-889">可以基于数据对象的名称添加新模板，以更改一种类型的对象的外观。</span><span class="sxs-lookup"><span data-stu-id="ee087-889">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="ee087-890">例如，你可以添加以下模板：</span><span class="sxs-lookup"><span data-stu-id="ee087-890">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="ee087-891">该模板可能包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="ee087-891">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="ee087-892">新的实体模板将在页面上通过使用新的*DynamicEntity*控件显示。</span><span class="sxs-lookup"><span data-stu-id="ee087-892">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="ee087-893">在运行时，此控件将替换为实体模板的内容。</span><span class="sxs-lookup"><span data-stu-id="ee087-893">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="ee087-894">下面的标记显示了使用实体模板的 `Detail.aspx` 页模板中的*FormView*控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-894">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="ee087-895">请注意标记中的*DynamicEntity*元素。</span><span class="sxs-lookup"><span data-stu-id="ee087-895">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="ee087-896">Url 和电子邮件地址的新字段模板</span><span class="sxs-lookup"><span data-stu-id="ee087-896">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="ee087-897">ASP.NET 4 引入了两个新的内置字段模板 `EmailAddress.ascx` 和 `Url.ascx`。</span><span class="sxs-lookup"><span data-stu-id="ee087-897">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="ee087-898">这些模板用于标记为*EmailAddress*的字段或包含*DataType*属性的*Url* 。</span><span class="sxs-lookup"><span data-stu-id="ee087-898">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="ee087-899">对于*EmailAddress*对象，该字段显示为使用*mailto：* 协议创建的超链接。</span><span class="sxs-lookup"><span data-stu-id="ee087-899">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="ee087-900">当用户单击该链接时，它将打开用户的电子邮件客户端并创建一个主干消息。</span><span class="sxs-lookup"><span data-stu-id="ee087-900">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="ee087-901">类型为*Url*的对象显示为普通超链接。</span><span class="sxs-lookup"><span data-stu-id="ee087-901">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="ee087-902">下面的示例演示如何标记字段。</span><span class="sxs-lookup"><span data-stu-id="ee087-902">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="ee087-903">创建带有 DynamicHyperLink 控件的链接</span><span class="sxs-lookup"><span data-stu-id="ee087-903">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="ee087-904">动态数据使用 .NET Framework 3.5 SP1 中添加的新路由功能来控制最终用户访问网站时看到的 Url。</span><span class="sxs-lookup"><span data-stu-id="ee087-904">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="ee087-905">使用新的*DynamicHyperLink*控件可以轻松地生成指向动态数据网站中的页面的链接。</span><span class="sxs-lookup"><span data-stu-id="ee087-905">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="ee087-906">下面的示例演示如何使用*DynamicHyperLink*控件：</span><span class="sxs-lookup"><span data-stu-id="ee087-906">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="ee087-907">此标记基于 `Global.asax` 文件中定义的路由，创建指向 `Products` 表的列表页的链接。</span><span class="sxs-lookup"><span data-stu-id="ee087-907">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="ee087-908">控件将自动使用动态数据页所基于的默认表名称。</span><span class="sxs-lookup"><span data-stu-id="ee087-908">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="ee087-909">数据模型中的继承支持</span><span class="sxs-lookup"><span data-stu-id="ee087-909">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="ee087-910">实体框架和 LINQ to SQL 支持其数据模型中的继承。</span><span class="sxs-lookup"><span data-stu-id="ee087-910">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="ee087-911">这种情况的一个示例可能是具有 `InsurancePolicy` 表的数据库。</span><span class="sxs-lookup"><span data-stu-id="ee087-911">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="ee087-912">它还可能包含与 `InsurancePolicy` 具有相同字段的 `CarPolicy` 和 `HousePolicy` 表，然后添加更多字段。</span><span class="sxs-lookup"><span data-stu-id="ee087-912">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="ee087-913">已将动态数据修改为理解数据模型中的继承对象，并支持继承的表的基架。</span><span class="sxs-lookup"><span data-stu-id="ee087-913">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="ee087-914">支持多对多关系（仅实体框架）</span><span class="sxs-lookup"><span data-stu-id="ee087-914">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="ee087-915">实体框架对表之间的多对多关系提供了丰富的支持，这是通过在*实体*对象上以集合的形式公开关系来实现的。</span><span class="sxs-lookup"><span data-stu-id="ee087-915">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="ee087-916">添加了新的 `ManyToMany.ascx` 和 `ManyToMany_Edit.ascx` 字段模板，以支持显示和编辑多对多关系中涉及的数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-916">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="ee087-917">用于控制显示和支持枚举的新属性</span><span class="sxs-lookup"><span data-stu-id="ee087-917">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="ee087-918">添加了*DisplayAttribute* ，使你可以更进一步控制字段的显示方式。</span><span class="sxs-lookup"><span data-stu-id="ee087-918">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="ee087-919">动态数据的早期版本中的*DisplayName*属性允许您更改用作字段标题的名称。</span><span class="sxs-lookup"><span data-stu-id="ee087-919">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="ee087-920">新的*DisplayAttribute*类可用于指定用于显示字段的更多选项，如字段的显示顺序以及是否将字段用作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ee087-920">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="ee087-921">此属性还提供对*GridView*控件中标签使用的名称的独立控制、 *DetailsView*控件中使用的名称、字段的帮助文本以及用于字段的水印（如果字段接受文本输入）。</span><span class="sxs-lookup"><span data-stu-id="ee087-921">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="ee087-922">添加了*EnumDataTypeAttribute*类，以便将字段映射到枚举。</span><span class="sxs-lookup"><span data-stu-id="ee087-922">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="ee087-923">将此特性应用于字段时，请指定枚举类型。</span><span class="sxs-lookup"><span data-stu-id="ee087-923">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="ee087-924">动态数据使用新 `Enumeration.ascx` 字段模板创建用于显示和编辑枚举值的 UI。</span><span class="sxs-lookup"><span data-stu-id="ee087-924">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="ee087-925">模板将数据库中的值映射到枚举中的名称。</span><span class="sxs-lookup"><span data-stu-id="ee087-925">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="ee087-926">增强的筛选器支持</span><span class="sxs-lookup"><span data-stu-id="ee087-926">Enhanced Support for Filters</span></span>

<span data-ttu-id="ee087-927">动态数据1.0 随内置筛选器提供，用于布尔列和外键列。</span><span class="sxs-lookup"><span data-stu-id="ee087-927">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="ee087-928">筛选器不允许您指定是否显示这些筛选器或它们的显示顺序。</span><span class="sxs-lookup"><span data-stu-id="ee087-928">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="ee087-929">新的*DisplayAttribute*属性通过提供对列是否显示为筛选器并按其显示顺序进行控制来解决这两个问题。</span><span class="sxs-lookup"><span data-stu-id="ee087-929">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="ee087-930">另外一项增强功能是[为了使用](#0.2__QueryExtender "_QueryExtender")Web 窗体的新功能，已经编写了筛选支持。</span><span class="sxs-lookup"><span data-stu-id="ee087-930">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="ee087-931">这样，便可以创建筛选器，而无需了解将与筛选器一起使用的数据源控件。</span><span class="sxs-lookup"><span data-stu-id="ee087-931">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="ee087-932">除了这些扩展外，筛选器也已转换为模板控件，使您可以添加新筛选器。</span><span class="sxs-lookup"><span data-stu-id="ee087-932">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="ee087-933">最后，前面提到的*DisplayAttribute*类允许重写默认筛选器，其方式与*UIHint*允许重写列的默认字段模板的方式相同。</span><span class="sxs-lookup"><span data-stu-id="ee087-933">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="ee087-934">Visual Studio 2010 Web 开发改进</span><span class="sxs-lookup"><span data-stu-id="ee087-934">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="ee087-935">Visual Studio 2010 中的 Web 开发已得到增强，以实现更好的 CSS 兼容性，更高的效率，通过 HTML 和 ASP.NET 的标记段和新的动态 IntelliSense JavaScript 提高。</span><span class="sxs-lookup"><span data-stu-id="ee087-935">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="ee087-936">提高了 CSS 兼容性</span><span class="sxs-lookup"><span data-stu-id="ee087-936">Improved CSS Compatibility</span></span>

<span data-ttu-id="ee087-937">Visual Studio 2010 中的 Visual Web Developer 设计器已更新，以提高 CSS 2.1 标准的符合性。</span><span class="sxs-lookup"><span data-stu-id="ee087-937">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="ee087-938">设计器更好地保留了 HTML 源的完整性，比早期版本的 Visual Studio 更可靠。</span><span class="sxs-lookup"><span data-stu-id="ee087-938">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="ee087-939">此外，还制定了体系结构改进功能，使其能够更好地实现呈现、布局和可维护性。</span><span class="sxs-lookup"><span data-stu-id="ee087-939">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="ee087-940">HTML 和 JavaScript 代码段</span><span class="sxs-lookup"><span data-stu-id="ee087-940">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="ee087-941">在 HTML 编辑器中，IntelliSense 自动完成标记名。</span><span class="sxs-lookup"><span data-stu-id="ee087-941">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="ee087-942">IntelliSense 代码段功能自动完成整个标记等。</span><span class="sxs-lookup"><span data-stu-id="ee087-942">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="ee087-943">在 Visual Studio 2010 中，在 Visual Studio 早期版本中受C#支持的 JavaScript、和 Visual Basic 支持 IntelliSense 代码片段。</span><span class="sxs-lookup"><span data-stu-id="ee087-943">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="ee087-944">Visual Studio 2010 包括超过200的代码段，可帮助你自动完成常见的 ASP.NET 和 HTML 标记，包括必需的属性（如 runat = "server"）以及特定于标记的常见属性（如*ID*、 *DataSourceID*、 *ControlToValidate*和*文本*）。</span><span class="sxs-lookup"><span data-stu-id="ee087-944">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="ee087-945">您可以下载其他代码段，也可以编写自己的代码片段，以封装您或您的团队用于常见任务的标记块。</span><span class="sxs-lookup"><span data-stu-id="ee087-945">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="ee087-946">JavaScript IntelliSense 增强功能</span><span class="sxs-lookup"><span data-stu-id="ee087-946">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="ee087-947">在 Visual 2010 中，JavaScript IntelliSense 经过了重新设计，以提供更丰富的编辑体验。</span><span class="sxs-lookup"><span data-stu-id="ee087-947">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="ee087-948">IntelliSense 现在可识别由方法（如*registerNamespace* ）和其他 JavaScript 框架使用的类似技术动态生成的对象。</span><span class="sxs-lookup"><span data-stu-id="ee087-948">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="ee087-949">提高了性能，以便分析较大的脚本库，并显示 IntelliSense，只需很少或没有处理延迟。</span><span class="sxs-lookup"><span data-stu-id="ee087-949">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="ee087-950">为了支持几乎所有第三方库和支持各种编码样式，兼容性已大幅增加。</span><span class="sxs-lookup"><span data-stu-id="ee087-950">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="ee087-951">文档注释现在会在你键入时进行分析，并将立即由 IntelliSense 使用。</span><span class="sxs-lookup"><span data-stu-id="ee087-951">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="ee087-952">用 Visual Studio 2010 部署 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="ee087-952">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="ee087-953">当 ASP.NET 开发人员部署 Web 应用程序时，他们通常会发现他们遇到如下问题：</span><span class="sxs-lookup"><span data-stu-id="ee087-953">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="ee087-954">部署到共享宿主站点需要诸如 FTP 等技术，这可能会很慢。</span><span class="sxs-lookup"><span data-stu-id="ee087-954">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="ee087-955">此外，您必须手动执行一些任务，如运行 SQL 脚本来配置数据库，您必须更改 IIS 设置，如将虚拟目录文件夹配置为应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-955">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="ee087-956">在企业环境中，除了部署 Web 应用程序文件之外，管理员经常必须修改 ASP.NET 配置文件和 IIS 设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-956">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="ee087-957">数据库管理员必须运行一系列 SQL 脚本来使应用程序数据库运行。</span><span class="sxs-lookup"><span data-stu-id="ee087-957">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="ee087-958">此类安装非常耗费人力，通常需要几小时才能完成，并且必须仔细记录。</span><span class="sxs-lookup"><span data-stu-id="ee087-958">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="ee087-959">Visual Studio 2010 包括的技术可解决这些问题，并使你能够无缝部署 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ee087-959">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="ee087-960">其中一种技术是 IIS Web 部署工具（Msdeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="ee087-960">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="ee087-961">Visual Studio 2010 中的 Web 部署功能包括以下主要方面：</span><span class="sxs-lookup"><span data-stu-id="ee087-961">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="ee087-962">Web 打包</span><span class="sxs-lookup"><span data-stu-id="ee087-962">Web packaging</span></span>
- <span data-ttu-id="ee087-963">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="ee087-963">Web.config transformation</span></span>
- <span data-ttu-id="ee087-964">数据库部署</span><span class="sxs-lookup"><span data-stu-id="ee087-964">Database deployment</span></span>
- <span data-ttu-id="ee087-965">Web 应用程序一键式发布</span><span class="sxs-lookup"><span data-stu-id="ee087-965">One-click publish for Web applications</span></span>

<span data-ttu-id="ee087-966">以下各节提供了有关这些功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-966">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="ee087-967">Web 打包</span><span class="sxs-lookup"><span data-stu-id="ee087-967">Web Packaging</span></span>

<span data-ttu-id="ee087-968">Visual Studio 2010 使用 Msdeploy.exe 工具为应用程序创建压缩（.zip）文件，该文件称为*Web 包*。</span><span class="sxs-lookup"><span data-stu-id="ee087-968">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="ee087-969">包文件包含有关应用程序的元数据以及以下内容：</span><span class="sxs-lookup"><span data-stu-id="ee087-969">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="ee087-970">IIS 设置，其中包括应用程序池设置、错误页设置等。</span><span class="sxs-lookup"><span data-stu-id="ee087-970">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="ee087-971">实际的 Web 内容，其中包括网页、用户控件、静态内容（图像和 HTML 文件）等。</span><span class="sxs-lookup"><span data-stu-id="ee087-971">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="ee087-972">SQL Server 数据库架构和数据。</span><span class="sxs-lookup"><span data-stu-id="ee087-972">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="ee087-973">安全证书、要在 GAC 中安装的组件、注册表设置等。</span><span class="sxs-lookup"><span data-stu-id="ee087-973">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="ee087-974">Web 包可以复制到任何服务器，然后使用 IIS 管理器手动安装。</span><span class="sxs-lookup"><span data-stu-id="ee087-974">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="ee087-975">或者，对于自动部署，可以使用命令行命令或使用部署 Api 来安装包。</span><span class="sxs-lookup"><span data-stu-id="ee087-975">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="ee087-976">Visual Studio 2010 提供内置的 MSBuild 任务和目标，以创建 Web 包。</span><span class="sxs-lookup"><span data-stu-id="ee087-976">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="ee087-977">有关详细信息，请参阅 MSDN 网站上的[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)和 Vishal Joshi 的博客上[创建 web 包的10多个原因](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)。</span><span class="sxs-lookup"><span data-stu-id="ee087-977">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="ee087-978">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="ee087-978">Web.config Transformation</span></span>

<span data-ttu-id="ee087-979">对于 Web 应用程序部署，Visual Studio 2010 引入了[XML 文档转换（XDT）](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)，这是一项功能，可用于将 `Web.config` 文件从开发设置转换为生产设置。</span><span class="sxs-lookup"><span data-stu-id="ee087-979">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="ee087-980">转换设置是在名为 `web.debug.config`、`web.release.config`等的转换文件中指定的。</span><span class="sxs-lookup"><span data-stu-id="ee087-980">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="ee087-981">（这些文件的名称与 MSBuild 配置匹配。）转换文件只包含需要对已部署 `Web.config` 文件进行的更改。</span><span class="sxs-lookup"><span data-stu-id="ee087-981">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="ee087-982">使用简单语法指定更改。</span><span class="sxs-lookup"><span data-stu-id="ee087-982">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="ee087-983">下面的示例演示了在部署发布配置时可能生成的 `web.release.config` 文件的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee087-983">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="ee087-984">示例中的 Replace 关键字指定在部署过程中，`Web.config` 文件中的*connectionString*节点将替换为示例中列出的值。</span><span class="sxs-lookup"><span data-stu-id="ee087-984">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="ee087-985">有关详细信息，请参阅 MSDN <a id="0.2_a"></a>网站上的 Web[应用程序项目部署的 web.config 转换语法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)和[web 部署：](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) Vishal Joshi 的博客上的 web.config 转换。</span><span class="sxs-lookup"><span data-stu-id="ee087-985">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="ee087-986">数据库部署</span><span class="sxs-lookup"><span data-stu-id="ee087-986">Database Deployment</span></span>

<span data-ttu-id="ee087-987">Visual Studio 2010 部署包可以包含对 SQL Server 数据库的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="ee087-987">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="ee087-988">作为包定义的一部分，你需要为源数据库提供连接字符串。</span><span class="sxs-lookup"><span data-stu-id="ee087-988">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="ee087-989">当你创建 Web 包时，Visual Studio 2010 将为数据库架构创建 SQL 脚本，并根据需要为数据创建 SQL 脚本，然后将这些脚本添加到包中。</span><span class="sxs-lookup"><span data-stu-id="ee087-989">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="ee087-990">你还可以提供自定义 SQL 脚本，并指定它们应在服务器上运行的顺序。</span><span class="sxs-lookup"><span data-stu-id="ee087-990">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="ee087-991">在部署时，提供适用于目标服务器的连接字符串;然后，部署过程使用此连接字符串运行创建数据库架构并添加数据的脚本。</span><span class="sxs-lookup"><span data-stu-id="ee087-991">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="ee087-992">此外，通过使用一键式发布，可以配置部署，以便在将应用程序发布到远程共享宿主站点时直接发布数据库。</span><span class="sxs-lookup"><span data-stu-id="ee087-992">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="ee087-993">有关详细信息，请参阅 MSDN 网站上的[如何：使用 Web 应用程序项目部署数据库](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)和[使用 VS 2010 的数据库部署](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 的博客。</span><span class="sxs-lookup"><span data-stu-id="ee087-993">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="ee087-994">Web 应用程序一键式发布</span><span class="sxs-lookup"><span data-stu-id="ee087-994">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="ee087-995">通过 Visual Studio 2010，你还可以使用 IIS 远程管理服务将 Web 应用程序发布到远程服务器。</span><span class="sxs-lookup"><span data-stu-id="ee087-995">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="ee087-996">你可以为托管帐户创建发布配置文件，或者为测试服务器或临时服务器创建发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="ee087-996">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="ee087-997">每个配置文件可以安全地保存适当的凭据。</span><span class="sxs-lookup"><span data-stu-id="ee087-997">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="ee087-998">然后，你可以通过使用 Web 一键式发布工具栏，只需要一次单击即可将其部署到任何目标服务器。</span><span class="sxs-lookup"><span data-stu-id="ee087-998">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="ee087-999">使用 Visual Studio 2010，还可以使用 MSBuild 命令行进行发布。</span><span class="sxs-lookup"><span data-stu-id="ee087-999">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="ee087-1000">这使您可以将您的团队生成环境配置为在持续集成模型中包含发布。</span><span class="sxs-lookup"><span data-stu-id="ee087-1000">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="ee087-1001">有关详细信息，请参阅 MSDN 网站上的 "[如何：使用一键式发布和 Web 部署部署 Web 应用程序项目](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)" 和[Web 1-单击 "使用 VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)在 Vishal Joshi 的博客上发布"。</span><span class="sxs-lookup"><span data-stu-id="ee087-1001">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="ee087-1002">若要查看有关 Visual Studio 2010 中 Web 应用程序部署的视频演示，请参阅 Vishal Joshi 的博客上[的 VS 2010 For Web Developer](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) preview。</span><span class="sxs-lookup"><span data-stu-id="ee087-1002">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="ee087-1003">资源</span><span class="sxs-lookup"><span data-stu-id="ee087-1003">Resources</span></span>

<span data-ttu-id="ee087-1004">以下网站提供了有关 ASP.NET 4 和 Visual Studio 2010 的其他信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-1004">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="ee087-1005">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 网站上的 ASP.NET 4 的官方文档。</span><span class="sxs-lookup"><span data-stu-id="ee087-1005">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="ee087-1006">[https://www.asp.net/](https://www.asp.net/) — ASP.NET 团队自己的网站。</span><span class="sxs-lookup"><span data-stu-id="ee087-1006">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="ee087-1007">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx)和[ASP.NET 动态数据内容映射](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)— ASP.NET 团队网站上的联机资源和 ASP.NET 动态数据的官方文档。</span><span class="sxs-lookup"><span data-stu-id="ee087-1007">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="ee087-1008">[https://www.asp.net/ajax/](../../ajax/index.md) -ASP.NET Ajax 开发的主要 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="ee087-1008">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="ee087-1009">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) （Visual Web Developer 团队博客），其中包含有关 Visual Studio 2010 中功能的信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-1009">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="ee087-1010">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET 的预览版本的主要 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="ee087-1010">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="ee087-1011">免责声明</span><span class="sxs-lookup"><span data-stu-id="ee087-1011">Disclaimer</span></span>

<span data-ttu-id="ee087-1012">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="ee087-1012">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="ee087-1013">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="ee087-1013">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="ee087-1014">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="ee087-1014">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="ee087-1015">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="ee087-1015">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="ee087-1016">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="ee087-1016">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="ee087-1017">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="ee087-1017">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="ee087-1018">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="ee087-1018">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="ee087-1019">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="ee087-1019">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="ee087-1020">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="ee087-1020">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="ee087-1021">除非另有说明，否则本示例中描述的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件关联应推断地址、徽标、人物、地点或事件。</span><span class="sxs-lookup"><span data-stu-id="ee087-1021">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="ee087-1022">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="ee087-1022">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="ee087-1023">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="ee087-1023">All rights reserved.</span></span>

<span data-ttu-id="ee087-1024">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="ee087-1024">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="ee087-1025">本文档所涉及的真实公司和产品名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="ee087-1025">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
