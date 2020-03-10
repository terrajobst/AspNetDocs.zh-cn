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
# <a name="aspnet-mvc-4"></a><span data-ttu-id="ed225-103">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ed225-103">ASP.NET MVC 4</span></span>

> <span data-ttu-id="ed225-104">本文档介绍 Visual Studio 2010 的 ASP.NET MVC 4 Beta 版本。</span><span class="sxs-lookup"><span data-stu-id="ed225-104">This document describes the release of ASP.NET MVC 4 Beta for Visual Studio 2010.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="ed225-105">这不是最新版本。</span><span class="sxs-lookup"><span data-stu-id="ed225-105">This is not the most current release.</span></span> <span data-ttu-id="ed225-106">[此处](mvc4-release-notes.md)提供了 ASP.NET MVC 4 RC 发行说明。</span><span class="sxs-lookup"><span data-stu-id="ed225-106">The ASP.NET MVC 4 RC release notes are available [here](mvc4-release-notes.md).</span></span>

- [<span data-ttu-id="ed225-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="ed225-107">Installation Notes</span></span>](#_Toc303253802)
- [<span data-ttu-id="ed225-108">文档</span><span class="sxs-lookup"><span data-stu-id="ed225-108">Documentation</span></span>](#_Toc303253803)
- [<span data-ttu-id="ed225-109">支持</span><span class="sxs-lookup"><span data-stu-id="ed225-109">Support</span></span>](#_Toc303253804)
- [<span data-ttu-id="ed225-110">软件要求</span><span class="sxs-lookup"><span data-stu-id="ed225-110">Software Requirements</span></span>](#_Toc303253805)
- [<span data-ttu-id="ed225-111">将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ed225-111">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>](#_Toc303253806)
- [<span data-ttu-id="ed225-112">ASP.NET MVC 4 Beta 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ed225-112">New Features in ASP.NET MVC 4 Beta</span></span>](#_Toc303253807)

    - [<span data-ttu-id="ed225-113">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="ed225-113">ASP.NET Web API</span></span>](#_Toc317096197)
    - [<span data-ttu-id="ed225-114">ASP.NET 单页面应用程序</span><span class="sxs-lookup"><span data-stu-id="ed225-114">ASP.NET Single Page Application</span></span>](#_Toc317096198)
    - [<span data-ttu-id="ed225-115">默认项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="ed225-115">Enhancements to Default Project Templates</span></span>](#_Toc303253808)
    - [<span data-ttu-id="ed225-116">移动项目模板</span><span class="sxs-lookup"><span data-stu-id="ed225-116">Mobile Project Template</span></span>](#_Toc303253809)
    - [<span data-ttu-id="ed225-117">显示模式</span><span class="sxs-lookup"><span data-stu-id="ed225-117">Display Modes</span></span>](#_Toc303253810)
    - [<span data-ttu-id="ed225-118">jQuery Mobile、视图切换器和浏览器替代</span><span class="sxs-lookup"><span data-stu-id="ed225-118">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>](#_Toc303253811)
    - [<span data-ttu-id="ed225-119">Visual Studio 中用于代码生成的食谱</span><span class="sxs-lookup"><span data-stu-id="ed225-119">Recipes for Code Generation in Visual Studio</span></span>](#_Toc303253812)
    - [<span data-ttu-id="ed225-120">异步控制器的任务支持</span><span class="sxs-lookup"><span data-stu-id="ed225-120">Task Support for Asynchronous Controllers</span></span>](#_Toc303253813)
    - [<span data-ttu-id="ed225-121">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="ed225-121">Azure SDK</span></span>](#_Toc303253814)
    - [<span data-ttu-id="ed225-122">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="ed225-122">Known Issues and Breaking Changes</span></span>](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a><span data-ttu-id="ed225-123">安装说明</span><span class="sxs-lookup"><span data-stu-id="ed225-123">Installation Notes</span></span>

<span data-ttu-id="ed225-124">可使用 Web 平台安装程序从[ASP.NET mvc 4 主页](../mvc/mvc4.md)安装适用于 Visual Studio 2010 的 ASP.NET Mvc 4 Beta 版。</span><span class="sxs-lookup"><span data-stu-id="ed225-124">ASP.NET MVC 4 Beta for Visual Studio 2010 can be installed from the [ASP.NET MVC 4 home page](../mvc/mvc4.md) using the Web Platform Installer.</span></span>

<span data-ttu-id="ed225-125">在安装 ASP.NET MVC 4 Beta 之前，必须先卸载任何以前安装的 ASP.NET MVC 4 预览版。</span><span class="sxs-lookup"><span data-stu-id="ed225-125">You must uninstall any previously installed previews of ASP.NET MVC 4 prior to installing ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="ed225-126">此版本与 .NET Framework 4.5 开发人员预览版不兼容。</span><span class="sxs-lookup"><span data-stu-id="ed225-126">This release is not compatible with the .NET Framework 4.5 Developer Preview.</span></span> <span data-ttu-id="ed225-127">安装 ASP.NET MVC 4 Beta 之前，必须先卸载 .NET 4.5 开发者预览版。</span><span class="sxs-lookup"><span data-stu-id="ed225-127">You must uninstall the .NET 4.5 Developer Preview before installing the ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="ed225-128">可以安装 ASP.NET MVC 4，并且可以并行运行与 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="ed225-128">ASP.NET MVC 4 can be installed and can run side-by-side with ASP.NET MVC 3.</span></span>

<a id="_Toc303253803"></a>
## <a name="documentation"></a><span data-ttu-id="ed225-129">文档</span><span class="sxs-lookup"><span data-stu-id="ed225-129">Documentation</span></span>

<span data-ttu-id="ed225-130">ASP.NET MVC 的文档可以在位于以下 URL 的 MSDN 网站上找到：</span><span class="sxs-lookup"><span data-stu-id="ed225-130">Documentation for ASP.NET MVC is available on the MSDN website at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

<span data-ttu-id="ed225-131">ASP.NET 网站（[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)）的 MVC 4 页面上提供了有关 ASP.NET MVC 的教程和其他信息。</span><span class="sxs-lookup"><span data-stu-id="ed225-131">Tutorials and other information about ASP.NET MVC are available on the MVC 4 page of the ASP.NET website ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span></span>

<a id="_Toc303253804"></a>
## <a name="support"></a><span data-ttu-id="ed225-132">支持</span><span class="sxs-lookup"><span data-stu-id="ed225-132">Support</span></span>

<span data-ttu-id="ed225-133">这是预览版本，不正式支持。</span><span class="sxs-lookup"><span data-stu-id="ed225-133">This is a preview release and is not officially supported.</span></span> <span data-ttu-id="ed225-134">如果你对此版本有任何疑问，请将其发布到 ASP.NET MVC 论坛（[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)），其中 ASP.NET 社区的成员通常能够提供非正式支持。</span><span class="sxs-lookup"><span data-stu-id="ed225-134">If you have questions about working with this release, post them to the ASP.NET MVC forum ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a><span data-ttu-id="ed225-135">软件要求</span><span class="sxs-lookup"><span data-stu-id="ed225-135">Software Requirements</span></span>

<span data-ttu-id="ed225-136">适用于 Visual Studio 的 ASP.NET MVC 4 组件需要 PowerShell 2.0 和 Visual Studio 2010 Service Pack 1 或带有 Service Pack 1 的 Visual Web Developer Express 2010。</span><span class="sxs-lookup"><span data-stu-id="ed225-136">The ASP.NET MVC 4 components for Visual Studio require PowerShell 2.0 and either Visual Studio 2010 with Service Pack 1 or Visual Web Developer Express 2010 with Service Pack 1.</span></span>

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a><span data-ttu-id="ed225-137">将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="ed225-137">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>

<span data-ttu-id="ed225-138">可以在同一台计算机上并行安装 ASP.NET MVC 4 与 ASP.NET MVC 3，这使你可以灵活选择何时将 ASP.NET MVC 3 应用程序升级到 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="ed225-138">ASP.NET MVC 4 can be installed side by side with ASP.NET MVC 3 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 3 application to ASP.NET MVC 4.</span></span>

<span data-ttu-id="ed225-139">升级的最简单方法是创建一个新的 ASP.NET MVC 4 项目，并将现有 MVC 3 项目中的所有视图、控制器、代码和内容文件复制到新项目，然后更新新项目中的程序集引用以匹配旧项目。</span><span class="sxs-lookup"><span data-stu-id="ed225-139">The simplest way to upgrade is to create a new ASP.NET MVC 4 project and copy all the views, controllers, code, and content files from the existing MVC 3 project to the new project and then to update the assembly references in the new project to match the old project.</span></span> <span data-ttu-id="ed225-140">如果已更改 MVC 3 项目中的 web.config 文件，还必须将这些更改合并到 MVC 4 项目中的 web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="ed225-140">If you have made changes to the Web.config file in the MVC 3 project, you must also merge those changes into the Web.config file in the MVC 4 project.</span></span>

<span data-ttu-id="ed225-141">若要手动将现有的 ASP.NET MVC 3 应用程序升级到版本4，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ed225-141">To manually upgrade an existing ASP.NET MVC 3 application to version 4, do the following:</span></span>

1. <span data-ttu-id="ed225-142">在项目的所有 web.config 文件中（项目的根目录中有一个文件，在 Views 文件夹中，一个位于项目中每个区域的 Views 文件夹中），替换以下文本的每个实例：</span><span class="sxs-lookup"><span data-stu-id="ed225-142">In all Web.config files in the project (there is one in the root of the project, one in the Views folder, and one in the Views folder for each area in your project), replace every instance of the following text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="ed225-143">，其中包含以下相应的文本：</span><span class="sxs-lookup"><span data-stu-id="ed225-143">with the following corresponding text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. <span data-ttu-id="ed225-144">在根 web.config 文件中，将 "*网页： Version* " 元素更新为 "2.0.0.0" 并添加值为 "true" 的新*PreserveLoginUrl*键：</span><span class="sxs-lookup"><span data-stu-id="ed225-144">In the root Web.config file, update the *webPages:Version* element to "2.0.0.0" and add a new *PreserveLoginUrl* key that has the value "true":</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. <span data-ttu-id="ed225-145">在解决方案资源管理器中，删除对*system.web*的引用（指向版本 3 DLL）。</span><span class="sxs-lookup"><span data-stu-id="ed225-145">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the version 3 DLL).</span></span> <span data-ttu-id="ed225-146">然后，*添加对4.0.0.0 的引用（v* ）。</span><span class="sxs-lookup"><span data-stu-id="ed225-146">Then add a reference to *System.Web.Mvc* (v4.0.0.0).</span></span> <span data-ttu-id="ed225-147">特别是，进行以下更改以更新程序集引用。</span><span class="sxs-lookup"><span data-stu-id="ed225-147">In particular, make the following changes to update the assembly references.</span></span> <span data-ttu-id="ed225-148">以下为详细信息：</span><span class="sxs-lookup"><span data-stu-id="ed225-148">Here are the details:</span></span>

    1. <span data-ttu-id="ed225-149">在解决方案资源管理器中，删除对以下程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="ed225-149">In Solution Explorer, delete the references to the following assemblies:</span></span> 

        - <span data-ttu-id="ed225-150">*System.web*（v 3.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-150">*System.Web.Mvc*(v3.0.0.0)</span></span>
        - <span data-ttu-id="ed225-151">*System.web*（1.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-151">*System.Web.WebPages*(v1.0.0.0)</span></span>
        - <span data-ttu-id="ed225-152">*System.web*（1.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-152">*System.Web.Razor*(v1.0.0.0)</span></span>
        - <span data-ttu-id="ed225-153">*System.web. Deployment*（1.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span></span>
        - <span data-ttu-id="ed225-154">*System.web. Razor*（1.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span></span>
    2. <span data-ttu-id="ed225-155">添加对以下程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="ed225-155">Add a references to the following assemblies:</span></span> 

        - <span data-ttu-id="ed225-156">*System.web*（v 4.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-156">*System.Web.Mvc*(v4.0.0.0)</span></span>
        - <span data-ttu-id="ed225-157">*System.web*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-157">*System.Web.WebPages*(v2.0.0.0)</span></span>
        - <span data-ttu-id="ed225-158">*System.web. Razor*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-158">*System.Web.Razor*(v2.0.0.0)</span></span>
        - <span data-ttu-id="ed225-159">*System.web. Deployment*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span></span>
        - <span data-ttu-id="ed225-160">*System.web. Razor*（v 2.0.0.0）</span><span class="sxs-lookup"><span data-stu-id="ed225-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span></span>
4. <span data-ttu-id="ed225-161">在解决方案资源管理器中，右键单击项目名称，然后选择 "卸载项目"。</span><span class="sxs-lookup"><span data-stu-id="ed225-161">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="ed225-162">然后再次右键单击该名称，然后选择 "编辑*项目*名称 .csproj"。</span><span class="sxs-lookup"><span data-stu-id="ed225-162">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
5. <span data-ttu-id="ed225-163">找到*ProjectTypeGuids*元素，并将 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 替换为 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。</span><span class="sxs-lookup"><span data-stu-id="ed225-163">Locate the *ProjectTypeGuids* element and replace {E53F8FEA-EAE0-44A6-8774-FFD645390401} with {E3E379DF-F4C6-4180-9B81-6769533ABE47}.</span></span>
6. <span data-ttu-id="ed225-164">保存所做的更改，关闭正在编辑的项目（.csproj）文件，右键单击该项目，然后选择 "重新加载项目"。</span><span class="sxs-lookup"><span data-stu-id="ed225-164">Save the changes, close the project (.csproj) file you were editing, right-click the project, and then select Reload Project.</span></span>
7. <span data-ttu-id="ed225-165">如果项目引用使用以前版本的 ASP.NET MVC 编译的任何第三方库，请打开根 web.config 文件，并在*配置*节下添加以下三个*bindingRedirect*元素：</span><span class="sxs-lookup"><span data-stu-id="ed225-165">If the project references any third-party libraries that are compiled using previous versions of ASP.NET MVC, open the root Web.config file and add the following three *bindingRedirect* elements under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a><span data-ttu-id="ed225-166">ASP.NET MVC 4 Beta 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ed225-166">New Features in ASP.NET MVC 4 Beta</span></span>

<span data-ttu-id="ed225-167">本部分介绍 ASP.NET MVC 4 Beta 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="ed225-167">This section describes features that have been introduced in the ASP.NET MVC 4 Beta release.</span></span>

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="ed225-168">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="ed225-168">ASP.NET Web API</span></span>

<span data-ttu-id="ed225-169">ASP.NET MVC 4 现在包括了 ASP.NET Web API，这是一个新的框架，用于创建可访问范围广泛的客户端（包括浏览器和移动设备）的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="ed225-169">ASP.NET MVC 4 now includes ASP.NET Web API, a new framework for creating HTTP services that can reach a broad range of clients including browsers and mobile devices.</span></span> <span data-ttu-id="ed225-170">ASP.NET Web API 也是用于生成 RESTful 服务的理想平台。</span><span class="sxs-lookup"><span data-stu-id="ed225-170">ASP.NET Web API is also an ideal platform for building RESTful services.</span></span>

<span data-ttu-id="ed225-171">ASP.NET Web API 包括对以下功能的支持：</span><span class="sxs-lookup"><span data-stu-id="ed225-171">ASP.NET Web API includes support for the following features:</span></span>

- <span data-ttu-id="ed225-172">**新式 HTTP 编程模型：** 使用新的强类型 HTTP 对象模型直接访问和处理 Web Api 中的 HTTP 请求和响应。</span><span class="sxs-lookup"><span data-stu-id="ed225-172">**Modern HTTP programming model:** Directly access and manipulate HTTP requests and responses in your Web APIs using a new, strongly typed HTTP object model.</span></span> <span data-ttu-id="ed225-173">可以通过新的 HttpClient 类型在客户端上对称提供相同的编程模型和 HTTP 管道。</span><span class="sxs-lookup"><span data-stu-id="ed225-173">The same programming model and HTTP pipeline is symmetrically available on the client through the new HttpClient type.</span></span>
- <span data-ttu-id="ed225-174">**完全支持路由**： web api 现在支持一组完整的路由功能，这些功能始终是 Web 堆栈的一部分，包括路由参数和约束。</span><span class="sxs-lookup"><span data-stu-id="ed225-174">**Full support for routes**: Web APIs now support the full set of route capabilities that have always been a part of the Web stack, including route parameters and constraints.</span></span> <span data-ttu-id="ed225-175">此外，映射到操作完全支持约定，因此您不再需要将属性（例如 [HttpPost]）应用于您的类和方法。</span><span class="sxs-lookup"><span data-stu-id="ed225-175">Additionally, mapping to actions has full support for conventions, so you no longer need to apply attributes such as [HttpPost] to your classes and methods.</span></span>
- <span data-ttu-id="ed225-176">**内容协商**：客户端和服务器可以协同工作，确定从 API 返回的数据的正确格式。</span><span class="sxs-lookup"><span data-stu-id="ed225-176">**Content negotiation**: The client and server can work together to determine the right format for data being returned from an API.</span></span> <span data-ttu-id="ed225-177">我们提供对 XML、JSON 和格式 URL 编码格式的默认支持，你可以通过添加自己的格式化程序，甚至替换默认的内容协商策略来扩展此支持。</span><span class="sxs-lookup"><span data-stu-id="ed225-177">We provide default support for XML, JSON, and Form URL-encoded formats, and you can extend this support by adding your own formatters, or even replace the default content negotiation strategy.</span></span>
- <span data-ttu-id="ed225-178">**模型绑定和验证：** 模型联编程序提供了一种简单的方法，可以从 HTTP 请求的各个部分提取数据，并将这些消息部分转换为可由 Web API 操作使用的 .NET 对象。</span><span class="sxs-lookup"><span data-stu-id="ed225-178">**Model binding and validation:** Model binders provide an easy way to extract data from various parts of an HTTP request and convert those message parts into .NET objects which can be used by the Web API actions.</span></span>
- <span data-ttu-id="ed225-179">**筛选器：** Web Api 现在支持筛选器，其中包括众所周知的筛选器，例如 "[授权]" 属性。</span><span class="sxs-lookup"><span data-stu-id="ed225-179">**Filters:** Web APIs now supports filters, including well-known filters such as the [Authorize] attribute.</span></span> <span data-ttu-id="ed225-180">你可以为操作、授权和异常处理编写和插入你自己的筛选器。</span><span class="sxs-lookup"><span data-stu-id="ed225-180">You can author and plug in your own filters for actions, authorization and exception handling.</span></span>
- <span data-ttu-id="ed225-181">**查询撰写：** 通过只返回 IQueryable&lt;T&gt;，Web API 将支持通过 OData URL 约定进行查询。</span><span class="sxs-lookup"><span data-stu-id="ed225-181">**Query composition:** By simply returning IQueryable&lt;T&gt;, your Web API will support querying via the OData URL conventions.</span></span>
- <span data-ttu-id="ed225-182">**提高了 HTTP 详细信息的可测试性：** Web API 操作现在可以与 HttpRequestMessage 和 HttpResponseMessage 的实例一起使用，而不是在静态上下文对象中设置 HTTP 详细信息。</span><span class="sxs-lookup"><span data-stu-id="ed225-182">**Improved testability of HTTP details:** Rather than setting HTTP details in static context objects, Web API actions can now work with instances of HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="ed225-183">除了使用 HTTP 类型外，还存在这些对象的泛型版本。</span><span class="sxs-lookup"><span data-stu-id="ed225-183">Generic versions of these objects also exist to let you work with your custom types in addition to the HTTP types.</span></span>
- <span data-ttu-id="ed225-184">**通过 DependencyResolver 改进了控制反转（IoC）：** Web API 现在使用由 MVC 的依赖关系解析程序实现的服务定位器模式来获取许多不同设施的实例。</span><span class="sxs-lookup"><span data-stu-id="ed225-184">**Improved Inversion of Control (IoC) via DependencyResolver:** Web API now uses the service locator pattern implemented by MVC's dependency resolver to obtain instances for many different facilities.</span></span>
- <span data-ttu-id="ed225-185">**基于代码的配置：** Web API 配置仅通过代码完成，使配置文件保持干净整洁。</span><span class="sxs-lookup"><span data-stu-id="ed225-185">**Code-based configuration:** Web API configuration is accomplished solely through code, leaving your config files clean.</span></span>
- <span data-ttu-id="ed225-186">**自承载：** 除了使用路由的全部功能和 Web API 的其他功能，web Api 还可以在自己的进程中托管在自己的进程中。</span><span class="sxs-lookup"><span data-stu-id="ed225-186">**Self-host:** Web APIs can be hosted in your own process in addition to IIS while still using the full power of routes and other features of Web API.</span></span>

<span data-ttu-id="ed225-187">有关 ASP.NET Web API 的详细信息，请访问[https://www.asp.net/web-api](../web-api/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ed225-187">For more details on ASP.NET Web API please visit [https://www.asp.net/web-api](../web-api/index.md).</span></span>

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a><span data-ttu-id="ed225-188">ASP.NET 单页面应用程序</span><span class="sxs-lookup"><span data-stu-id="ed225-188">ASP.NET Single Page Application</span></span>

<span data-ttu-id="ed225-189">ASP.NET MVC 4 现在包括了使用 JavaScript 和 Web Api 生成单页面应用程序以及使用很多客户端交互的体验的早期预览版。</span><span class="sxs-lookup"><span data-stu-id="ed225-189">ASP.NET MVC 4 now includes an early preview of the experience for building single page applications with significant client-side interactions using JavaScript and Web APIs.</span></span> <span data-ttu-id="ed225-190">此支持包括：</span><span class="sxs-lookup"><span data-stu-id="ed225-190">This support includes:</span></span>

- <span data-ttu-id="ed225-191">一组用于与缓存数据进行更丰富的本地交互的 JavaScript 库</span><span class="sxs-lookup"><span data-stu-id="ed225-191">A set of JavaScript libraries for richer local interactions with cached data</span></span>
- <span data-ttu-id="ed225-192">工作单元和 DAL 支持的其他 Web API 组件</span><span class="sxs-lookup"><span data-stu-id="ed225-192">Additional Web API components for unit of work and DAL support</span></span>
- <span data-ttu-id="ed225-193">带有基架的 MVC 项目模板，用于快速入门</span><span class="sxs-lookup"><span data-stu-id="ed225-193">An MVC project template with scaffolding to get started quickly</span></span>

<span data-ttu-id="ed225-194">有关 ASP.NET MVC 4 中的单页面应用程序支持的更多详细信息，请访问[https://www.asp.net/single-page-application](../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ed225-194">For more details on the Single Page Application support in ASP.NET MVC 4 please visit [https://www.asp.net/single-page-application](../single-page-application/index.md).</span></span>

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a><span data-ttu-id="ed225-195">默认项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="ed225-195">Enhancements to Default Project Templates</span></span>

<span data-ttu-id="ed225-196">已更新用于创建新 ASP.NET MVC 4 项目的模板，以创建更新式的网站：</span><span class="sxs-lookup"><span data-stu-id="ed225-196">The template that is used to create new ASP.NET MVC 4 projects has been updated to create a more modern-looking website:</span></span>

![](mvc4-beta-release-notes/_static/image1.png)

<span data-ttu-id="ed225-197">除了修饰改进之外，新模板中还提供了改进的功能。</span><span class="sxs-lookup"><span data-stu-id="ed225-197">In addition to cosmetic improvements, there's improved functionality in the new template.</span></span> <span data-ttu-id="ed225-198">该模板使用一种称为自适应呈现的技术，在桌面浏览器和移动浏览器中看起来很好，无需任何自定义。</span><span class="sxs-lookup"><span data-stu-id="ed225-198">The template employs a technique called adaptive rendering to look good in both desktop browsers and mobile browsers without any customization.</span></span>

![](mvc4-beta-release-notes/_static/image2.png)

<span data-ttu-id="ed225-199">若要查看操作中的自适应呈现，可以使用移动仿真程序，或者尝试将桌面浏览器窗口的大小调整为更小。</span><span class="sxs-lookup"><span data-stu-id="ed225-199">To see adaptive rendering in action, you can use a mobile emulator or just try resizing the desktop browser window to be smaller.</span></span> <span data-ttu-id="ed225-200">当浏览器窗口变小时，该页的布局将更改。</span><span class="sxs-lookup"><span data-stu-id="ed225-200">When the browser window gets small enough, the layout of the page will change.</span></span>

<span data-ttu-id="ed225-201">默认项目模板的另一增强功能是使用 JavaScript 提供更丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="ed225-201">Another enhancement to the default project template is the use of JavaScript to provide a richer UI.</span></span> <span data-ttu-id="ed225-202">在模板中使用的登录名和注册链接是如何使用 jQuery UI 对话框提供丰富的登录屏幕的示例：</span><span class="sxs-lookup"><span data-stu-id="ed225-202">The Login and Register links that are used in the template are examples of how to use the jQuery UI Dialog to present a rich login screen:</span></span>

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a><span data-ttu-id="ed225-203">移动项目模板</span><span class="sxs-lookup"><span data-stu-id="ed225-203">Mobile Project Template</span></span>

<span data-ttu-id="ed225-204">如果要开始一个新项目，并且想要创建专门用于移动和平板电脑浏览器的站点，则可以使用 "新建移动应用程序" 项目模板。</span><span class="sxs-lookup"><span data-stu-id="ed225-204">If you're starting a new project and want to create a site specifically for mobile and tablet browsers, you can use the new Mobile Application project template.</span></span> <span data-ttu-id="ed225-205">这基于 jQuery Mobile，这是一个用于生成触摸优化 UI 的开源库：</span><span class="sxs-lookup"><span data-stu-id="ed225-205">This is based on jQuery Mobile, an open-source library for building touch-optimized UI:</span></span>

![](mvc4-beta-release-notes/_static/image4.png)

<span data-ttu-id="ed225-206">此模板包含与 Internet 应用程序模板相同的应用程序结构（控制器代码几乎完全相同），但它使用 jQuery Mobile 进行了样式设计，使其在基于触摸的移动设备上看起来良好且表现良好。</span><span class="sxs-lookup"><span data-stu-id="ed225-206">This template contains the same application structure as the Internet Application template (and the controller code is virtually identical), but it's styled using jQuery Mobile to look good and behave well on touch-based mobile devices.</span></span> <span data-ttu-id="ed225-207">若要详细了解如何构建和样式移动 UI，请参阅[JQuery mobile 项目网站](http://jquerymobile.com/)。</span><span class="sxs-lookup"><span data-stu-id="ed225-207">To learn more about how to structure and style mobile UI, see the [jQuery Mobile project website](http://jquerymobile.com/).</span></span>

<span data-ttu-id="ed225-208">如果你已经有想要将移动优化视图添加到的面向桌面的站点，或如果你想要创建为桌面和移动浏览器提供不同样式视图的单一站点，则可以使用新的显示模式功能。</span><span class="sxs-lookup"><span data-stu-id="ed225-208">If you already have a desktop-oriented site that you want to add mobile-optimized views to, or if you want to create a single site that serves differently styled views to desktop and mobile browsers, you can use the new Display Modes feature.</span></span> <span data-ttu-id="ed225-209">（请参见下一节。）</span><span class="sxs-lookup"><span data-stu-id="ed225-209">(See the next section.)</span></span>

<a id="_Toc303253810"></a>
### <a name="display-modes"></a><span data-ttu-id="ed225-210">显示模式</span><span class="sxs-lookup"><span data-stu-id="ed225-210">Display Modes</span></span>

<span data-ttu-id="ed225-211">使用新的显示模式功能，应用程序可以根据发出请求的浏览器选择视图。</span><span class="sxs-lookup"><span data-stu-id="ed225-211">The new Display Modes feature lets an application select views depending on the browser that's making the request.</span></span> <span data-ttu-id="ed225-212">例如，如果桌面浏览器请求主页，则该应用程序可能会使用 Views\Home\Index.cshtml 模板。</span><span class="sxs-lookup"><span data-stu-id="ed225-212">For example, if a desktop browser requests the Home page, the application might use the Views\Home\Index.cshtml template.</span></span> <span data-ttu-id="ed225-213">如果移动浏览器请求主页，则应用程序可能返回 Views\Home\Index.mobile.cshtml 模板。</span><span class="sxs-lookup"><span data-stu-id="ed225-213">If a mobile browser requests the Home page, the application might return the Views\Home\Index.mobile.cshtml template.</span></span>

<span data-ttu-id="ed225-214">还可以为特定的浏览器类型重写布局和分区。</span><span class="sxs-lookup"><span data-stu-id="ed225-214">Layouts and partials can also be overridden for particular browser types.</span></span> <span data-ttu-id="ed225-215">例如:</span><span class="sxs-lookup"><span data-stu-id="ed225-215">For example:</span></span>

- <span data-ttu-id="ed225-216">如果你的 Views\Shared 文件夹同时包含 \_的和 \_Layout 模板，则默认情况下，应用程序将在移动浏览器的请求期间使用 \_Layout，并在其他请求期间 \_布局。</span><span class="sxs-lookup"><span data-stu-id="ed225-216">If your Views\Shared folder contains both the \_Layout.cshtml and \_Layout.mobile.cshtml templates, by default the application will use \_Layout.mobile.cshtml during requests from mobile browsers and \_Layout.cshtml during other requests.</span></span>
- <span data-ttu-id="ed225-217">如果文件夹同时包含 \_MyPartial 和 \_MyPartial，则指令 @Html.Partial（"\_MyPartial"）将在移动浏览器的请求期间呈现 \_MyPartial，在其他请求期间 \_MyPartial。</span><span class="sxs-lookup"><span data-stu-id="ed225-217">If a folder contains both \_MyPartial.cshtml and \_MyPartial.mobile.cshtml, the instruction @Html.Partial("\_MyPartial") will render \_MyPartial.mobile.cshtml during requests from mobile browsers, and \_MyPartial.cshtml during other requests.</span></span>

<span data-ttu-id="ed225-218">如果要为其他设备创建更具体的视图、布局或分部视图，则可以注册新的*DefaultDisplayMode*实例，以指定当请求满足特定条件时要搜索的名称。</span><span class="sxs-lookup"><span data-stu-id="ed225-218">If you want to create more specific views, layouts, or partial views for other devices, you can register a new *DefaultDisplayMode* instance to specify which name to search for when a request satisfies particular conditions.</span></span> <span data-ttu-id="ed225-219">例如，可以将以下代码添加到 global.asax 文件中的*应用程序\_Start*方法，以将字符串 "iPhone" 注册为在 Apple iPhone 浏览器发出请求时适用的显示模式：</span><span class="sxs-lookup"><span data-stu-id="ed225-219">For example, you could add the following code to the *Application\_Start* method in the Global.asax file to register the string "iPhone" as a display mode that applies when the Apple iPhone browser makes a request:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

<span data-ttu-id="ed225-220">此代码运行后，当 Apple iPhone 浏览器发出请求时，你的应用程序将使用 Views\Shared _Layout\\（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="ed225-220">After this code runs, when an Apple iPhone browser makes a request, your application will use the Views\Shared\\_Layout.iPhone.cshtml layout (if it exists).</span></span>

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a><span data-ttu-id="ed225-221">jQuery Mobile、视图切换器和浏览器替代</span><span class="sxs-lookup"><span data-stu-id="ed225-221">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>

<span data-ttu-id="ed225-222">jQuery Mobile 是用于构建触摸优化 web UI 的开源库。</span><span class="sxs-lookup"><span data-stu-id="ed225-222">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="ed225-223">如果要将 jQuery Mobile 用于 ASP.NET MVC 4 应用程序，可以下载并安装可帮助你入门的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ed225-223">If you want to use jQuery Mobile with an ASP.NET MVC 4 application, you can download and install a NuGet package that helps you get started.</span></span> <span data-ttu-id="ed225-224">若要从 Visual Studio 包管理器控制台安装，请键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ed225-224">To install it from the Visual Studio Package Manager Console, type the following command:</span></span>

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

<span data-ttu-id="ed225-225">这将安装 jQuery Mobile 和一些 helper 文件，其中包括：</span><span class="sxs-lookup"><span data-stu-id="ed225-225">This installs jQuery Mobile and some helper files, including the following:</span></span>

- <span data-ttu-id="ed225-226">Views/Shared/\_Layout，它是基于 jQuery Mobile 的布局。</span><span class="sxs-lookup"><span data-stu-id="ed225-226">Views/Shared/\_Layout.Mobile.cshtml, which is a jQuery Mobile-based layout.</span></span>
- <span data-ttu-id="ed225-227">视图切换器组件，由 Views/Shared/\_ViewSwitcher 分部视图和 ViewSwitcherController.cs 控制器组成。</span><span class="sxs-lookup"><span data-stu-id="ed225-227">A view-switcher component, which consists of the Views/Shared/\_ViewSwitcher.cshtml partial view and the ViewSwitcherController.cs controller.</span></span>

<span data-ttu-id="ed225-228">安装包后，使用移动浏览器运行应用程序（或等效项，如 Firefox[用户代理切换](http://chrispederick.com/work/user-agent-switcher/)器外接程序）。</span><span class="sxs-lookup"><span data-stu-id="ed225-228">After you install the package, run your application using a mobile browser (or equivalent, like the Firefox [User Agent Switcher](http://chrispederick.com/work/user-agent-switcher/) add-on).</span></span> <span data-ttu-id="ed225-229">你将看到页面看上去差别很大，因为 jQuery Mobile 处理布局和样式。</span><span class="sxs-lookup"><span data-stu-id="ed225-229">You'll see that your pages look quite different, because jQuery Mobile handles layout and styling.</span></span> <span data-ttu-id="ed225-230">若要利用此内容，可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ed225-230">To take advantage of this, you can do the following:</span></span>

- <span data-ttu-id="ed225-231">如前面的[显示模式](#_Toc303253810)所述创建特定于移动设备的视图重写（例如，创建 Views\Home\Index.mobile.cshtml 以替代移动浏览器的 Views\Home\Index.cshtml）。</span><span class="sxs-lookup"><span data-stu-id="ed225-231">Create mobile-specific view overrides as described under [Display Modes](#_Toc303253810) earlier (for example, create Views\Home\Index.mobile.cshtml to override Views\Home\Index.cshtml for mobile browsers).</span></span>
- <span data-ttu-id="ed225-232">若要详细了解如何在移动视图中添加触控优化的 UI 元素，请阅读[JQuery mobile 文档](http://jquerymobile.com/)。</span><span class="sxs-lookup"><span data-stu-id="ed225-232">Read the [jQuery Mobile documentation](http://jquerymobile.com/) to learn more about how to add touch-optimized UI elements in mobile views.</span></span>

<span data-ttu-id="ed225-233">移动优化的网页约定是添加一个链接，其文本的内容类似于桌面视图或完整站点模式，使用户能够切换到页面的桌面版本。</span><span class="sxs-lookup"><span data-stu-id="ed225-233">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="ed225-234">JQuery. node.js 包包含一个用于此目的的视图切换器组件示例。</span><span class="sxs-lookup"><span data-stu-id="ed225-234">The jQuery.Mobile.MVC package includes a sample view-switcher component for this purpose.</span></span> <span data-ttu-id="ed225-235">它在默认的 Views\Shared\\_Layout 中使用，在呈现页面时，它如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed225-235">It's used in the default Views\Shared\\_Layout.Mobile.cshtml view, and it looks like this when the page is rendered:</span></span>

![](mvc4-beta-release-notes/_static/image5.png)

<span data-ttu-id="ed225-236">如果访问者单击此链接，则会切换到同一页面的桌面版本。</span><span class="sxs-lookup"><span data-stu-id="ed225-236">If visitors click the link, they're switched to the desktop version of the same page.</span></span>

<span data-ttu-id="ed225-237">由于默认情况下，桌面布局不包括视图切换器，因此访问者将无法访问移动模式。</span><span class="sxs-lookup"><span data-stu-id="ed225-237">Because your desktop layout will not include a view switcher by default, visitors won't have a way to get to mobile mode.</span></span> <span data-ttu-id="ed225-238">若要启用此操作，请将以下对 *\_ViewSwitcher*的引用添加到桌面布局，只需在 *&lt;body&gt;* 元素内：</span><span class="sxs-lookup"><span data-stu-id="ed225-238">To enable this, add the following reference to *\_ViewSwitcher* to your desktop layout, just inside the *&lt;body&gt;* element:</span></span>

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="ed225-239">视图切换器使用称为 "浏览器重写" 的新功能。</span><span class="sxs-lookup"><span data-stu-id="ed225-239">The view switcher uses a new feature called Browser Overriding.</span></span> <span data-ttu-id="ed225-240">此功能使应用程序可以处理请求，就好像这些请求来自于它们实际来自的浏览器（用户代理）。</span><span class="sxs-lookup"><span data-stu-id="ed225-240">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they're actually from.</span></span> <span data-ttu-id="ed225-241">下表列出了浏览器重写提供的方法。</span><span class="sxs-lookup"><span data-stu-id="ed225-241">The following table lists the methods that Browser Overriding provides.</span></span>

| `HttpContext.SetOverriddenBrowser(userAgentString)` | <span data-ttu-id="ed225-242">使用指定的用户代理，重写请求的实际用户代理值。</span><span class="sxs-lookup"><span data-stu-id="ed225-242">Overrides the request's actual user agent value using the specified user agent.</span></span> |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | <span data-ttu-id="ed225-243">如果未指定替代，则返回请求的用户代理替代值或实际的用户代理字符串。</span><span class="sxs-lookup"><span data-stu-id="ed225-243">Returns the request's user agent override value, or the actual user agent string if no override has been specified.</span></span> |
| `HttpContext.GetOverriddenBrowser()` | <span data-ttu-id="ed225-244">返回一个*HttpBrowserCapabilitiesBase*实例，该实例对应于当前为请求设置的用户代理（实际或重写）。</span><span class="sxs-lookup"><span data-stu-id="ed225-244">Returns an *HttpBrowserCapabilitiesBase* instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="ed225-245">可以使用此值获取属性，如*IsMobileDevice*。</span><span class="sxs-lookup"><span data-stu-id="ed225-245">You can use this value to get properties such as *IsMobileDevice*.</span></span> |
| `HttpContext.ClearOverriddenBrowser()` | <span data-ttu-id="ed225-246">删除任何针对当前请求重写的用户代理。</span><span class="sxs-lookup"><span data-stu-id="ed225-246">Removes any overridden user agent for the current request.</span></span> |

<span data-ttu-id="ed225-247">浏览器重写是 ASP.NET MVC 4 的一项核心功能，即使不安装 jQuery. node.js 包也是如此。</span><span class="sxs-lookup"><span data-stu-id="ed225-247">Browser Overriding is a core feature of ASP.NET MVC 4 and is available even if you don't install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="ed225-248">但是，它只会影响视图、布局和分部视图选择，而不会影响依赖于*请求 .browser*对象的任何其他 ASP.NET 功能。</span><span class="sxs-lookup"><span data-stu-id="ed225-248">However, it affects only view, layout, and partial-view selection — it does not affect any other ASP.NET feature that depends on the *Request.Browser* object.</span></span>

<span data-ttu-id="ed225-249">默认情况下，使用 cookie 存储用户代理替代。</span><span class="sxs-lookup"><span data-stu-id="ed225-249">By default, the user-agent override is stored using a cookie.</span></span> <span data-ttu-id="ed225-250">如果要在其他位置（例如，在数据库中）存储替代，可以替换默认提供程序（*BrowserOverrideStores*）。</span><span class="sxs-lookup"><span data-stu-id="ed225-250">If you want to store the override elsewhere (for example, in a database), you can replace the default provider (*BrowserOverrideStores.Current*).</span></span> <span data-ttu-id="ed225-251">此提供程序的文档将提供给 ASP.NET MVC 的更高版本。</span><span class="sxs-lookup"><span data-stu-id="ed225-251">Documentation for this provider will be available to accompany a later release of ASP.NET MVC.</span></span>

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a><span data-ttu-id="ed225-252">Visual Studio 中用于代码生成的食谱</span><span class="sxs-lookup"><span data-stu-id="ed225-252">Recipes for Code Generation in Visual Studio</span></span>

<span data-ttu-id="ed225-253">使用新的食谱功能，Visual Studio 可基于可使用 NuGet 安装的包生成特定于解决方案的代码。</span><span class="sxs-lookup"><span data-stu-id="ed225-253">The new Recipes feature enables Visual Studio to generate solution-specific code based on packages that you can install using NuGet.</span></span> <span data-ttu-id="ed225-254">通过食谱框架，开发人员可以轻松编写代码生成插件，还可以使用它来替换 "添加区域"、"添加控制器" 和 "添加视图" 的内置代码生成器。</span><span class="sxs-lookup"><span data-stu-id="ed225-254">The Recipes framework makes it easy for developers to write code-generation plugins, which you can also use to replace the built-in code generators for Add Area, Add Controller, and Add View.</span></span> <span data-ttu-id="ed225-255">因为食谱以 NuGet 包的形式部署，所以可以轻松地将其签入源控件并自动与项目上的所有开发人员共享。</span><span class="sxs-lookup"><span data-stu-id="ed225-255">Because recipes are deployed as NuGet packages, they can easily be checked into source control and shared with all developers on the project automatically.</span></span> <span data-ttu-id="ed225-256">它们还可用于每个解决方案。</span><span class="sxs-lookup"><span data-stu-id="ed225-256">They are also available on a per-solution basis.</span></span>

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a><span data-ttu-id="ed225-257">异步控制器的任务支持</span><span class="sxs-lookup"><span data-stu-id="ed225-257">Task Support for Asynchronous Controllers</span></span>

<span data-ttu-id="ed225-258">你现在可以将异步操作方法作为返回类型为*task*或 task 的对象的单个方法写入 *&lt;ActionResult&gt;* 。</span><span class="sxs-lookup"><span data-stu-id="ed225-258">You can now write asynchronous action methods as single methods that return an object of type *Task* or *Task&lt;ActionResult&gt;*.</span></span>

<span data-ttu-id="ed225-259">例如，如果使用的是 Visual C# 5 （或使用[Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)），则可以创建一个类似于下面的异步操作方法：</span><span class="sxs-lookup"><span data-stu-id="ed225-259">For example, if you're using Visual C# 5 (or using the [Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)), you can create an asynchronous action method that looks like the following:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

<span data-ttu-id="ed225-260">在上一操作方法中，对*newsService*和*sportsService*的调用是异步调用的，并且不会阻止线程池中的线程。</span><span class="sxs-lookup"><span data-stu-id="ed225-260">In the previous action method, the calls to *newsService.GetHeadlinesAsync* and *sportsService.GetScoresAsync* are called asynchronously and do not block a thread from the thread pool.</span></span>

<span data-ttu-id="ed225-261">返回*任务*实例的异步操作方法还可以支持超时。</span><span class="sxs-lookup"><span data-stu-id="ed225-261">Asynchronous action methods that return *Task* instances can also support timeouts.</span></span> <span data-ttu-id="ed225-262">若要使操作方法可取消，请将*CancellationToken*类型的参数添加到操作方法签名中。</span><span class="sxs-lookup"><span data-stu-id="ed225-262">To make your action method cancellable, add a parameter of type *CancellationToken* to the action method signature.</span></span> <span data-ttu-id="ed225-263">下面的示例显示一个异步操作方法，该操作方法的超时为2500毫秒，在出现超时的情况下，将向客户端显示*超时*视图。</span><span class="sxs-lookup"><span data-stu-id="ed225-263">The following example shows an asynchronous action method that has a timeout of 2500 milliseconds and that displays a *TimedOut* view to the client if a timeout occurs.</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a><span data-ttu-id="ed225-264">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="ed225-264">Azure SDK</span></span>

<span data-ttu-id="ed225-265">ASP.NET MVC 4 Beta 支持 Microsoft Azure SDK 1.5 2011 年9月版。</span><span class="sxs-lookup"><span data-stu-id="ed225-265">ASP.NET MVC 4 Beta supports the September 2011 1.5 release of the Windows Azure SDK.</span></span>

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="ed225-266">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="ed225-266">Known Issues and Breaking Changes</span></span>

- <span data-ttu-id="ed225-267">**安装 ASP.NET MVC 4 Beta 后，Visual Studio 2010 Service Pack 1 中的 CSHTML/VBHTML 编辑器在 cshtml/VBHTML 文件中键入代码段或 JavaScript 后，可能会暂停很长时间。**</span><span class="sxs-lookup"><span data-stu-id="ed225-267">**After installing ASP.NET MVC 4 Beta, the CSHTML/VBHTML editor in Visual Studio 2010 Service Pack 1 CSHTML/VBHTML editor may pause for a long time after typing snippet or JavaScript inside cshtml or vbhtml files.**</span></span> <span data-ttu-id="ed225-268">仅在刚刚创建且尚未编译的 ASP.NET MVC 4 应用程序中进行此操作。</span><span class="sxs-lookup"><span data-stu-id="ed225-268">This occurs only in ASP.NET MVC 4 applications which have just been created and have not yet been compiled.</span></span>

    <span data-ttu-id="ed225-269">解决方法是编译项目以获取 bin 文件夹中的程序集。</span><span class="sxs-lookup"><span data-stu-id="ed225-269">The workaround is to compile the project to get the assemblies in the bin folder.</span></span> <span data-ttu-id="ed225-270">请注意，如果您清除了从 bin 文件夹中删除程序集的项目，则会出现编辑器问题。</span><span class="sxs-lookup"><span data-stu-id="ed225-270">Note, if you clean the project which removes the assemblies from the bin folder, the editor problem will come back.</span></span>

    <span data-ttu-id="ed225-271">这将在下一版本中得到更正。</span><span class="sxs-lookup"><span data-stu-id="ed225-271">This will be corrected in the next release.</span></span>
- <span data-ttu-id="ed225-272">**C#适用于 Visual Studio 11 Beta 的项目模板在 Global.asax.cs 中包含不正确的连接字符串。**</span><span class="sxs-lookup"><span data-stu-id="ed225-272">**C# Project templates for Visual Studio 11 Beta contain an incorrect connection string in Global.asax.cs.**</span></span> <span data-ttu-id="ed225-273">在 Visual Studio 11 Beta 中创建的项目的 Application\_Start 方法中指定的默认连接包含一个 LocalDB 连接字符串，其中包含非转义反斜杠（\) 字符。</span><span class="sxs-lookup"><span data-stu-id="ed225-273">The default connection specified in the Application\_Start method for projects created in Visual Studio 11 Beta contain a LocalDB connection string which contains an unescaped backslash (\) character.</span></span> <span data-ttu-id="ed225-274">这会导致在尝试访问实体框架 DbContext 时出现连接错误，这将生成 SqlException。</span><span class="sxs-lookup"><span data-stu-id="ed225-274">This results in a connection error upon attempts to access a Entity Framework DbContext, which generates a SqlException.</span></span>

    <span data-ttu-id="ed225-275">若要更正此问题，请将应用中的反斜杠字符转义\_Start Global.asax.cs 方法，使其如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed225-275">To correct this issue, escape the backslash character in the App\_Start method of Global.asax.cs so that it reads as follows:</span></span>

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- <span data-ttu-id="ed225-276">**在 .NET 4.0 下运行时，面向 .NET 4.5 的 ASP.NET MVC 4 应用程序将引发 FileLoadException，尝试访问该程序集。**</span><span class="sxs-lookup"><span data-stu-id="ed225-276">**ASP.NET MVC 4 applications which target .NET 4.5 will throw a FileLoadException upon attempt to access the System.Net.Http.dll assembly when run under .NET 4.0.**</span></span> <span data-ttu-id="ed225-277">在 .NET 4.5 中创建的 ASP.NET MVC 4 应用程序包含绑定重定向，此重定向将导致 FileLoadException，这表明 "无法加载文件或程序集 ' 系统 .Net. Http ' 或它的一个依赖项"。</span><span class="sxs-lookup"><span data-stu-id="ed225-277">ASP.NET MVC 4 applications created under .NET 4.5 contain a binding redirect that will result in a FileLoadException which that states "Could not load file or assembly 'System.Net.Http' or one of its dependencies."</span></span> <span data-ttu-id="ed225-278">当在安装了 .NET 4.0 的系统上执行应用程序时。</span><span class="sxs-lookup"><span data-stu-id="ed225-278">when the application is executed on a system with .NET 4.0 installed.</span></span> <span data-ttu-id="ed225-279">若要更正此问题，请从 web.config 中删除以下绑定重定向：</span><span class="sxs-lookup"><span data-stu-id="ed225-279">To correct this issue, remove the following binding redirect from web.config:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    <span data-ttu-id="ed225-280">修改后的 web.config 中的程序集绑定元素应如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed225-280">The assembly binding element in the modified web.config should appear as follows:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <span data-ttu-id="ed225-281"><strong>从区域内</strong><strong>调用时，Visual Basic 项目中的 "添加控制器" 项模板将生成不正确的命名空间</strong>。</span><span class="sxs-lookup"><span data-stu-id="ed225-281"><strong>The "Add Controller" item template in Visual Basic projects generates an incorrect namespace when invoked</strong><strong>from inside an area.</strong></span></span> <span data-ttu-id="ed225-282">将控制器添加到使用 Visual Basic 的 ASP.NET MVC 项目中的某个区域时，项模板会将错误的命名空间插入控制器。</span><span class="sxs-lookup"><span data-stu-id="ed225-282">When you add a controller to an area in an ASP.NET MVC project that uses Visual Basic, the item template inserts the wrong namespace into the controller.</span></span> <span data-ttu-id="ed225-283">在导航到控制器中的任何操作时，结果为 "找不到文件" 错误。</span><span class="sxs-lookup"><span data-stu-id="ed225-283">The result is a "file not found" error when you navigate to any action in the controller.</span></span>  
  
  <span data-ttu-id="ed225-284">生成的命名空间忽略根命名空间后面的所有内容。</span><span class="sxs-lookup"><span data-stu-id="ed225-284">The generated namespace omits everything after the root namespace.</span></span> <span data-ttu-id="ed225-285">例如，生成的命名空间为*RootNamespace* ，但应为*RootNamespace* 。</span><span class="sxs-lookup"><span data-stu-id="ed225-285">For example, the namespace generated is *RootNamespace* but should be *RootNamespace.Areas.AreaName.Controllers* .</span></span>
- <span data-ttu-id="ed225-286">**Razor 视图引擎中的重大更改。**</span><span class="sxs-lookup"><span data-stu-id="ed225-286">**Breaking changes in the Razor View Engine.**</span></span> <span data-ttu-id="ed225-287">作为 Razor 分析器重写的一部分，将从*system.web*中删除以下类型：</span><span class="sxs-lookup"><span data-stu-id="ed225-287">As part of a rewrite of the Razor parser, the following types were removed from *System.Web.Mvc.Razor*:</span></span> 

    - <span data-ttu-id="ed225-288">*ModelSpan*</span><span class="sxs-lookup"><span data-stu-id="ed225-288">*ModelSpan*</span></span>
    - <span data-ttu-id="ed225-289">*MvcVBRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="ed225-289">*MvcVBRazorCodeGenerator*</span></span>
    - <span data-ttu-id="ed225-290">*MvcCSharpRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="ed225-290">*MvcCSharpRazorCodeGenerator*</span></span>
    - <span data-ttu-id="ed225-291">*MvcVBRazorCodeParser*</span><span class="sxs-lookup"><span data-stu-id="ed225-291">*MvcVBRazorCodeParser*</span></span>

  <span data-ttu-id="ed225-292">还删除了以下方法：</span><span class="sxs-lookup"><span data-stu-id="ed225-292">The following methods were also removed:</span></span> 

    - <span data-ttu-id="ed225-293">*MvcCSharpRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*</span><span class="sxs-lookup"><span data-stu-id="ed225-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
    - <span data-ttu-id="ed225-294">*MvcWebPageRazorHost. DecorateCodeGenerator （System.web. RazorCodeGenerator）*</span><span class="sxs-lookup"><span data-stu-id="ed225-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span></span>
    - <span data-ttu-id="ed225-295">*MvcVBRazorCodeParser. ParseInheritsStatement （System.web. CodeBlockInfo）*</span><span class="sxs-lookup"><span data-stu-id="ed225-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
- <span data-ttu-id="ed225-296">**当 WebData 包含在 ASP.NET MVC 4 应用程序的/bin 目录中时，它将接管用于窗体身份验证的 URL。**</span><span class="sxs-lookup"><span data-stu-id="ed225-296">**When WebMatrix.WebData.dll is included in the /bin directory of an ASP.NET MVC 4 apps, it takes over the URL for forms authentication.**</span></span> <span data-ttu-id="ed225-297">将 WebData 程序集添加到应用程序（例如，在使用 "添加可部署的依赖项" 对话框时选择 "使用 Razor 语法 ASP.NET 网页" 时）会将身份验证登录重定向重定向到/account/logon，而不是默认的 ASP.NET MVC 帐户控制器所需的/account/login。</span><span class="sxs-lookup"><span data-stu-id="ed225-297">Adding the WebMatrix.WebData.dll assembly to your application (for example, by selecting "ASP.NET Web Pages with Razor Syntax" when using the Add Deployable Dependencies dialog) will override the authentication login redirect to /account/logon rather than /account/login as expected by the default ASP.NET MVC Account Controller.</span></span> <span data-ttu-id="ed225-298">若要防止此行为并使用在 web.config 的身份验证部分中指定的 URL，可以添加一个名为 PreserveLoginUrl 的 appSetting，并将其设置为 true：</span><span class="sxs-lookup"><span data-stu-id="ed225-298">To prevent this behavior and use the URL specified already in the authentication section of web.config, you can add an appSetting called PreserveLoginUrl and set it to true:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- <span data-ttu-id="ed225-299">**尝试安装 Visual Studio 2010 和 Visual Web Developer 2010 的并行安装的 ASP.NET MVC 4 时，NuGet 包管理器无法安装。**</span><span class="sxs-lookup"><span data-stu-id="ed225-299">**The NuGet package manager fails to install when attempting to install ASP.NET MVC 4 for side by side installations of Visual Studio 2010 and Visual Web Developer 2010.**</span></span> <span data-ttu-id="ed225-300">若要与 ASP.NET MVC 4 并行运行 Visual Studio 2010 和 Visual Web Developer 2010，则必须在安装了两个版本的 Visual Studio 后安装 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="ed225-300">To run Visual Studio 2010 and Visual Web Developer 2010 side by side with ASP.NET MVC 4 you must install ASP.NET MVC 4 after both versions of Visual Studio have already been installed.</span></span>
- <span data-ttu-id="ed225-301">**如果已卸载了必备组件，则卸载 ASP.NET MVC 4 会失败。**</span><span class="sxs-lookup"><span data-stu-id="ed225-301">**Uninstalling ASP.NET MVC 4 fails if prerequisites have already been uninstalled.**</span></span> <span data-ttu-id="ed225-302">若要完全卸载 ASP.NET MVC 4you，必须先卸载 ASP.NET MVC 4，然后再卸载 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ed225-302">To cleanly uninstall ASP.NET MVC 4you must uninstall ASP.NET MVC 4 prior to uninstalling Visual Studio.</span></span>
- <span data-ttu-id="ed225-303">**运行默认的 Web API 项目会显示错误地指示用户使用不存在的 RegisterApis 方法添加路由的指令。**</span><span class="sxs-lookup"><span data-stu-id="ed225-303">**Running a default Web API project shows instructions that incorrectly direct the user to add routes using the RegisterApis method, which doesn't exist.**</span></span> <span data-ttu-id="ed225-304">应使用 ASP.NET 路由表在 RegisterRoutes 方法中添加路由。</span><span class="sxs-lookup"><span data-stu-id="ed225-304">Routes should be added in the RegisterRoutes method using the ASP.NET route table.</span></span>
- <span data-ttu-id="ed225-305">**安装 ASP.NET MVC 4 Beta 中断 ASP.NET MVC 3 RTM 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="ed225-305">**Installing ASP.NET MVC 4 Beta breaks ASP.NET MVC 3 RTM applications.**</span></span> <span data-ttu-id="ed225-306">使用 RTM 版本创建的 ASP.NET MVC 3 应用程序（而不是 ASP.NET MVC 3 工具更新版本）需要进行以下更改才能与 ASP.NET MVC 4 Beta 并行工作。</span><span class="sxs-lookup"><span data-stu-id="ed225-306">ASP.NET MVC 3 applications that were created with the RTM release (not with the ASP.NET MVC 3 Tools Update release) require the following changes in order to work side-by-side with ASP.NET MVC 4 Beta.</span></span> <span data-ttu-id="ed225-307">生成项目但不进行这些更新会导致编译错误。</span><span class="sxs-lookup"><span data-stu-id="ed225-307">Building the project without making these updates results in compilation errors.</span></span> 

    <span data-ttu-id="ed225-308">**所需更新**</span><span class="sxs-lookup"><span data-stu-id="ed225-308">**Required updates**</span></span>

  1. <span data-ttu-id="ed225-309">在根 web.config 文件中，添加一个新的 *&lt;appSettings&gt;* 项，其中包含密钥 "*网页：版本*" 和 " *1.0.0.0*" 值。</span><span class="sxs-lookup"><span data-stu-id="ed225-309">In the root Web.config file, add a new *&lt;appSettings&gt;* entry with the key *webPages:Version* and the value *1.0.0.0*.</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. <span data-ttu-id="ed225-310">在解决方案资源管理器中，右键单击项目名称，然后选择 "卸载项目"。</span><span class="sxs-lookup"><span data-stu-id="ed225-310">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="ed225-311">然后再次右键单击该名称，然后选择 "编辑*项目*名称 .csproj"。</span><span class="sxs-lookup"><span data-stu-id="ed225-311">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
  3. <span data-ttu-id="ed225-312">找到以下程序集引用：</span><span class="sxs-lookup"><span data-stu-id="ed225-312">Locate the following assembly references:</span></span> 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      <span data-ttu-id="ed225-313">将它们替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="ed225-313">Replace them with the following:</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. <span data-ttu-id="ed225-314">保存所做的更改，关闭正在编辑的项目（.csproj）文件，然后右键单击该项目，然后选择 "重新加载"。</span><span class="sxs-lookup"><span data-stu-id="ed225-314">Save the changes, close the project (.csproj) file you were editing, and then right-click the project and select Reload.</span></span>
