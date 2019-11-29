---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: 了解 ASP.NET AJAX 本地化 |Microsoft Docs
author: scottcate
description: 本地化是设计特定语言和区域性并将其集成到应用程序或应用程序组件的支持的过程。 Mic 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600887"
---
# <a name="understanding-aspnet-ajax-localization"></a><span data-ttu-id="58230-104">了解 ASP.NET AJAX 本地化</span><span class="sxs-lookup"><span data-stu-id="58230-104">Understanding ASP.NET AJAX Localization</span></span>

<span data-ttu-id="58230-105">作者： [Scott Cate](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="58230-105">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="58230-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="58230-106">Download PDF</span></span>](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> <span data-ttu-id="58230-107">本地化是设计特定语言和区域性并将其集成到应用程序或应用程序组件的支持的过程。</span><span class="sxs-lookup"><span data-stu-id="58230-107">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="58230-108">通过集成标准 .NET 本地化模型，Microsoft ASP.NET 平台为标准 ASP.NET 应用程序的本地化提供了广泛的支持;Microsoft AJAX Framework 利用集成模式来支持可执行本地化的各种方案。</span><span class="sxs-lookup"><span data-stu-id="58230-108">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span>

## <a name="introduction"></a><span data-ttu-id="58230-109">简介</span><span class="sxs-lookup"><span data-stu-id="58230-109">Introduction</span></span>

<span data-ttu-id="58230-110">Microsoft 的 ASP.NET 技术引入了面向对象的和事件驱动的编程模型，并将其与编译的代码的优势结合起来。</span><span class="sxs-lookup"><span data-stu-id="58230-110">Microsoft's ASP.NET technology brings an object-oriented and event-driven programming model and unites it with the benefits of compiled code.</span></span> <span data-ttu-id="58230-111">但是，它的服务器端处理模型在技术方面有一些固有的缺点，其中许多功能都可以通过 System.web 命名空间中包含的新功能来解决，后者在 .NET Framework3.5。</span><span class="sxs-lookup"><span data-stu-id="58230-111">However, its server-side processing model has several drawbacks inherent in the technology, many of which can be addressed by the new features included in the System.Web.Extensions namespace, which encapsulates the Microsoft AJAX Services in the .NET Framework 3.5.</span></span> <span data-ttu-id="58230-112">这些扩展启用了许多丰富的客户端功能，以前作为 ASP.NET 2.0 AJAX 扩展的一部分提供，但现在是框架基类库的一部分。</span><span class="sxs-lookup"><span data-stu-id="58230-112">These extensions enable many rich client features, previously available as part of the ASP.NET 2.0 AJAX Extensions, but now part of the Framework Base Class Library.</span></span> <span data-ttu-id="58230-113">此命名空间中的控件和功能包括页面的部分呈现，无需整页刷新、通过客户端脚本访问 Web 服务的能力（包括 ASP.NET 分析 API）以及用于镜像许多在 ASP.NET 服务器端控件集中显示的控件方案。</span><span class="sxs-lookup"><span data-stu-id="58230-113">Controls and features in this namespace include partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="58230-114">本白皮书介绍了 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库中存在的本地化功能，其中包含本地化支持的业务需求和对 web 中本地化的已集成支持.NET Framework 提供的应用程序。</span><span class="sxs-lookup"><span data-stu-id="58230-114">This whitepaper examines the localization features present in the Microsoft AJAX Framework and Microsoft AJAX Script Library, in the context of business need for localization support and reviewing already-integrated support for localization in web applications provided by the .NET Framework.</span></span> <span data-ttu-id="58230-115">Microsoft AJAX 脚本库利用了 .NET 应用程序已使用的 .resx 文件格式，该格式提供集成的 IDE 支持和可共享的资源类型。</span><span class="sxs-lookup"><span data-stu-id="58230-115">The Microsoft AJAX Script Library utilizes the .resx file format already used by .NET applications, which provides integrated IDE support and a shareable resource type.</span></span>

<span data-ttu-id="58230-116">本白皮书基于 Microsoft Visual Studio 2008 的 Beta 2 版本。</span><span class="sxs-lookup"><span data-stu-id="58230-116">This whitepaper is based on the Beta 2 release of Microsoft Visual Studio 2008.</span></span> <span data-ttu-id="58230-117">本白皮书还假设你将使用 Visual Studio 2008，而不是 Visual Web Developer Express，并将根据 Visual Studio 的用户界面提供演练。</span><span class="sxs-lookup"><span data-stu-id="58230-117">This whitepaper also assumes that you will be working with Visual Studio 2008, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="58230-118">一些代码示例将利用在 Visual Web Developer 速成版中可能不可用的项目模板。</span><span class="sxs-lookup"><span data-stu-id="58230-118">Some code samples will utilize project templates that may be unavailable in Visual Web Developer Express.</span></span>

## <a name="the-need-for-localization"></a><span data-ttu-id="58230-119">*本地化需要*</span><span class="sxs-lookup"><span data-stu-id="58230-119">*The Need for Localization*</span></span>

<span data-ttu-id="58230-120">特别是对于企业应用程序开发人员和组件开发人员而言，创建可了解区域性与语言差异的工具的功能已变得越来越重要。</span><span class="sxs-lookup"><span data-stu-id="58230-120">Particularly for enterprise application developers and component developers, the ability to create tools that can be aware of the differences between cultures and languages has become increasingly necessary.</span></span> <span data-ttu-id="58230-121">设计可适应客户端区域设置的组件可以提高开发人员的工作效率，并减少调整组件全局运行所需的工作量。</span><span class="sxs-lookup"><span data-stu-id="58230-121">Designing components with the ability to adapt to the locale of the client increases developer productivity and reduces the amount of work required for the adaptation of a component to function globally.</span></span>

<span data-ttu-id="58230-122">本地化是设计特定语言和区域性并将其集成到应用程序或应用程序组件的支持的过程。</span><span class="sxs-lookup"><span data-stu-id="58230-122">Localization is the process of designing and integrating support for a specific language and culture into an application or an application component.</span></span> <span data-ttu-id="58230-123">通过集成标准 .NET 本地化模型，Microsoft ASP.NET 平台为标准 ASP.NET 应用程序的本地化提供了广泛的支持;Microsoft AJAX Framework 利用集成模式来支持可执行本地化的各种方案。</span><span class="sxs-lookup"><span data-stu-id="58230-123">The Microsoft ASP.NET platform provides extensive support for localization for standard ASP.NET applications by integrating the standard .NET localization model; the Microsoft AJAX Framework utilize the integrated model to support the diverse scenarios in which localization can be performed.</span></span> <span data-ttu-id="58230-124">使用 Microsoft AJAX Framework，可以通过将脚本部署到附属程序集或利用静态文件系统结构来对脚本进行本地化。</span><span class="sxs-lookup"><span data-stu-id="58230-124">With the Microsoft AJAX Framework, scripts can either be localized by being deployed into satellite assemblies, or by utilizing a static file system structure.</span></span>

## <a name="embedding-scripts-with-satellite-assemblies"></a><span data-ttu-id="58230-125">*将脚本嵌入附属程序集*</span><span class="sxs-lookup"><span data-stu-id="58230-125">*Embedding Scripts with Satellite Assemblies*</span></span>

<span data-ttu-id="58230-126">与标准 .NET Framework 本地化策略一致，资源可以包括在附属程序集中。</span><span class="sxs-lookup"><span data-stu-id="58230-126">Consistent with the standard .NET Framework localization strategy, resources can be included in satellite assemblies.</span></span> <span data-ttu-id="58230-127">与二进制文件中的传统资源包含相比，附属程序集具有多项优势-任何指定的本地化都可以更新，而无需更新较大的映像，只需将附属程序集安装到项目文件夹和附属程序集均可部署，而不会导致主项目程序集重新加载。</span><span class="sxs-lookup"><span data-stu-id="58230-127">Satellite assemblies provide several advantages over traditional resource inclusion in binaries - any given localization can be updated without updating the larger image, additional localizations can be deployed simply by installing satellite assemblies into the project folder, and satellite assemblies can be deployed without causing a reload of the main project assembly.</span></span> <span data-ttu-id="58230-128">特别是在 ASP.NET 项目中，这是很有用的，因为它可以显著减少增量更新所使用的系统资源量，并最大限度地降低生产网站的使用。</span><span class="sxs-lookup"><span data-stu-id="58230-128">Particularly in ASP.NET projects, this is beneficial because it can significantly reduce the amount of system resources used by incremental updates, and minimally disrupts production website usage.</span></span>

<span data-ttu-id="58230-129">脚本嵌入到程序集中，方法是将它们包含在托管的 .resx （或编译的 .resources）文件中，这些文件将在编译时包含在程序集中。</span><span class="sxs-lookup"><span data-stu-id="58230-129">Scripts are embedded into assemblies by including them in managed .resx (or compiled .resources) files, which are included into the assembly at compile-time.</span></span> <span data-ttu-id="58230-130">然后通过程序集级别的属性，将其资源通过 AJAX 运行时生成的代码提供给脚本应用程序。</span><span class="sxs-lookup"><span data-stu-id="58230-130">Their resources are then made available to the script application through AJAX runtime-generated code, via assembly-level attributes</span></span>

<span data-ttu-id="58230-131">*嵌入的脚本文件的命名约定*</span><span class="sxs-lookup"><span data-stu-id="58230-131">*Naming Conventions for Embedded Script Files*</span></span>

<span data-ttu-id="58230-132">Microsoft AJAX Framework 脚本管理支持用于在部署和测试脚本时使用的各种选项，并且提供了有助于这些选项的指导原则。</span><span class="sxs-lookup"><span data-stu-id="58230-132">The Microsoft AJAX Framework script management supports a variety of options for use in deployment and testing of scripts, and guidelines are provided to facilitate these options.</span></span>

<span data-ttu-id="58230-133">*为了便于调试：*</span><span class="sxs-lookup"><span data-stu-id="58230-133">*To facilitate debugging:*</span></span>

<span data-ttu-id="58230-134">Release （生产）脚本不应在文件名中包含 `.debug` 限定符。</span><span class="sxs-lookup"><span data-stu-id="58230-134">Release (production) scripts should not include the `.debug` qualifier in the filename.</span></span> <span data-ttu-id="58230-135">为调试而设计的脚本应在文件名中包含 `.debug`。</span><span class="sxs-lookup"><span data-stu-id="58230-135">Scripts designed for debugging should include `.debug` in the filename.</span></span>

<span data-ttu-id="58230-136">*为简化本地化：*</span><span class="sxs-lookup"><span data-stu-id="58230-136">*To facilitate localization:*</span></span>

<span data-ttu-id="58230-137">非特定区域性脚本不应在文件的名称中包含任何区域性标识符。</span><span class="sxs-lookup"><span data-stu-id="58230-137">Neutral-culture scripts should not include any culture identifier in the name of the file.</span></span> <span data-ttu-id="58230-138">对于包含本地化资源的脚本，应在文件名中指定 ISO 语言代码。</span><span class="sxs-lookup"><span data-stu-id="58230-138">For scripts that contain localized resources, the ISO language code should be specified in the file name.</span></span> <span data-ttu-id="58230-139">例如，`es-CO` 代表西班牙语，哥伦比亚。</span><span class="sxs-lookup"><span data-stu-id="58230-139">For example, `es-CO` stands for Spanish, Columbia.</span></span>

<span data-ttu-id="58230-140">下表总结了包含示例的文件命名约定：</span><span class="sxs-lookup"><span data-stu-id="58230-140">The following table summarizes the file naming conventions with examples:</span></span>

| <span data-ttu-id="58230-141">{2&gt;文件名&lt;2}</span><span class="sxs-lookup"><span data-stu-id="58230-141">Filename</span></span> | <span data-ttu-id="58230-142">含义</span><span class="sxs-lookup"><span data-stu-id="58230-142">Meaning</span></span> |
| --- | --- |
| <span data-ttu-id="58230-143">Script</span><span class="sxs-lookup"><span data-stu-id="58230-143">Script.js</span></span> | <span data-ttu-id="58230-144">非特定于版本区域性的脚本。</span><span class="sxs-lookup"><span data-stu-id="58230-144">A release-version culture-neutral script.</span></span> |
| <span data-ttu-id="58230-145">Script node.js</span><span class="sxs-lookup"><span data-stu-id="58230-145">Script.debug.js</span></span> | <span data-ttu-id="58230-146">调试版本非特定于区域性的脚本。</span><span class="sxs-lookup"><span data-stu-id="58230-146">A debug-version culture-neutral script.</span></span> |
| <span data-ttu-id="58230-147">En-US</span><span class="sxs-lookup"><span data-stu-id="58230-147">Script.en-US.js</span></span> | <span data-ttu-id="58230-148">版本英语美国脚本。</span><span class="sxs-lookup"><span data-stu-id="58230-148">A release version English, United States script.</span></span> |
| <span data-ttu-id="58230-149">Script.debug.es-CO</span><span class="sxs-lookup"><span data-stu-id="58230-149">Script.debug.es-CO.js</span></span> | <span data-ttu-id="58230-150">Debug 版本西班牙语，哥伦比亚脚本。</span><span class="sxs-lookup"><span data-stu-id="58230-150">A debug-version Spanish, Columbia script.</span></span> |

## <a name="walkthrough-create-an-localized-embedded-script"></a><span data-ttu-id="58230-151">演练：创建本地化的嵌入脚本</span><span class="sxs-lookup"><span data-stu-id="58230-151">Walkthrough: Create an Localized, Embedded Script</span></span>

<span data-ttu-id="58230-152">*请注意：此演练要求使用 Visual Studio 2008，因为 Visual Web Developer Express 不包含用于类库项目的项目模板。*</span><span class="sxs-lookup"><span data-stu-id="58230-152">*Please note: this walkthrough requires the use of Visual Studio 2008 as Visual Web Developer Express does not include a project template for class library projects.*</span></span>

1. <span data-ttu-id="58230-153">使用集成的 ASP.NET AJAX Extension 创建新的网站项目。</span><span class="sxs-lookup"><span data-stu-id="58230-153">Create a new Web Site project with ASP.NET AJAX Extensions integrated.</span></span> <span data-ttu-id="58230-154">在名为 LocalizingResources 的解决方案中创建另一个项目（一个类库项目）。</span><span class="sxs-lookup"><span data-stu-id="58230-154">Create another project, a Class Library project, within the solution called LocalizingResources.</span></span>
2. <span data-ttu-id="58230-155">将名为 VerifyDeletion 的 Jscript 文件添加到 LocalizingResources 项目，并添加名为 DeletionResources 和 DeletionResources 的 .resx 资源文件。</span><span class="sxs-lookup"><span data-stu-id="58230-155">Add a Jscript file called VerifyDeletion.js to the LocalizingResources project, as well as .resx resources files called DeletionResources.resx and DeletionResources.es.resx.</span></span> <span data-ttu-id="58230-156">前者包含非特定区域性的资源;后者将包含西班牙语语言资源。</span><span class="sxs-lookup"><span data-stu-id="58230-156">The former will contain culture-neutral resources; the latter will contain Spanish-language resources.</span></span>
3. <span data-ttu-id="58230-157">将以下代码添加到 VerifyDeletion：</span><span class="sxs-lookup"><span data-stu-id="58230-157">Add the following code to VerifyDeletion.js:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

<span data-ttu-id="58230-158">对于使用 JavaScript Regex 语法不熟悉的对象，在单正斜杠中的文本（在上一个示例中，/FILENAME/是一个示例）表示 RegExp 对象。</span><span class="sxs-lookup"><span data-stu-id="58230-158">For those unfamiliar with JavaScript Regex syntax, text within single forward slashes (in the previous example, /FILENAME/ is an example) denotes a RegExp object.</span></span> <span data-ttu-id="58230-159">MSDN Library 包含广泛的 JavaScript 参考，可以联机找到 JavaScript 本机对象上的资源。</span><span class="sxs-lookup"><span data-stu-id="58230-159">The MSDN Library contains an extensive JavaScript reference, and resources on JavaScript native objects can be found online.</span></span>

1. <span data-ttu-id="58230-160">向 DeletionResources 添加以下资源字符串：</span><span class="sxs-lookup"><span data-stu-id="58230-160">Add the following resource strings to DeletionResources.resx:</span></span> 

    <span data-ttu-id="58230-161">**VerifyDelete**：是否确实要删除文件名？</span><span class="sxs-lookup"><span data-stu-id="58230-161">**VerifyDelete**: Are you sure you want to delete FILENAME?</span></span>

    <span data-ttu-id="58230-162">**已删除**：已删除文件名。</span><span class="sxs-lookup"><span data-stu-id="58230-162">**Deleted**: FILENAME has been deleted.</span></span>

1. <span data-ttu-id="58230-163">向 DeletionResources 添加以下资源字符串：</span><span class="sxs-lookup"><span data-stu-id="58230-163">Add the following resource strings to DeletionResources.es.resx:</span></span> 

    <span data-ttu-id="58230-164">**VerifyDelete**： Est seguro 查询 DESEE quitar FILENAME？</span><span class="sxs-lookup"><span data-stu-id="58230-164">**VerifyDelete**: Est seguro que desee quitar FILENAME?</span></span>

    <span data-ttu-id="58230-165">**已删除**： FILENAME se ha quitado。</span><span class="sxs-lookup"><span data-stu-id="58230-165">**Deleted**: FILENAME se ha quitado.</span></span>
2. <span data-ttu-id="58230-166">将以下代码行添加到 AssemblyInfo 文件：</span><span class="sxs-lookup"><span data-stu-id="58230-166">Add the following lines of code to the AssemblyInfo file:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. <span data-ttu-id="58230-167">向 LocalizingResources 项目添加对 System.web 和 System.object 的引用。</span><span class="sxs-lookup"><span data-stu-id="58230-167">Add references to System.Web and System.Web.Extensions to the LocalizingResources project.</span></span>
2. <span data-ttu-id="58230-168">从网站项目添加对 LocalizingResources 项目的引用。</span><span class="sxs-lookup"><span data-stu-id="58230-168">Add a reference to the LocalizingResources project from the Web Site project.</span></span>
3. <span data-ttu-id="58230-169">在 default.aspx 中，在网站项目下，用以下附加标记更新 ScriptManager 控件：</span><span class="sxs-lookup"><span data-stu-id="58230-169">In default.aspx, under the Web Site project, update the ScriptManager control with the following additional markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. <span data-ttu-id="58230-170">在页面上的任何位置，在默认情况下，包括以下标记：</span><span class="sxs-lookup"><span data-stu-id="58230-170">In default.aspx, anywhere on the page, include this markup:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. <span data-ttu-id="58230-171">按 F5。</span><span class="sxs-lookup"><span data-stu-id="58230-171">Press F5.</span></span> <span data-ttu-id="58230-172">如果系统提示，请启用调试。</span><span class="sxs-lookup"><span data-stu-id="58230-172">If prompted, enable debugging.</span></span> <span data-ttu-id="58230-173">加载页面后，按 "删除" 按钮。</span><span class="sxs-lookup"><span data-stu-id="58230-173">When the page is loaded, press the Delete button.</span></span> <span data-ttu-id="58230-174">请注意，系统会提示你输入英语（除非默认情况下，你的计算机设置为首选西班牙语语言资源）才能确认。</span><span class="sxs-lookup"><span data-stu-id="58230-174">Note that you are prompted in English (unless your computer is set to prefer Spanish-language resources by default) for confirmation.</span></span>
2. <span data-ttu-id="58230-175">关闭浏览器窗口并返回到 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="58230-175">Close the browser window and return to default.aspx.</span></span> <span data-ttu-id="58230-176">在 @Page 标头指令中，将 Culture 和 UICulture 的 auto 替换为 es。</span><span class="sxs-lookup"><span data-stu-id="58230-176">In the @Page header directive, replace auto for Culture and UICulture with es-ES.</span></span> <span data-ttu-id="58230-177">再次按 F5 在浏览器中重新启动 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="58230-177">Press F5 again to launch the web application in the browser again.</span></span> <span data-ttu-id="58230-178">这一次，请注意，系统会提示删除西班牙语中的文件：</span><span class="sxs-lookup"><span data-stu-id="58230-178">This time, note that you are prompted to delete the file in Spanish:</span></span>

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

<span data-ttu-id="58230-179">（[单击以查看完全大小的映像](understanding-asp-net-ajax-localization/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="58230-179">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image3.png))</span></span>

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

<span data-ttu-id="58230-180">（[单击以查看完全大小的映像](understanding-asp-net-ajax-localization/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="58230-180">([Click to view full-size image](understanding-asp-net-ajax-localization/_static/image6.png))</span></span>

<span data-ttu-id="58230-181">请注意，此演练有若干变化形式。</span><span class="sxs-lookup"><span data-stu-id="58230-181">Note that there are several variations for this walkthrough.</span></span> <span data-ttu-id="58230-182">例如，可以在页面加载过程中以编程方式向 ScriptManager 控件注册脚本。</span><span class="sxs-lookup"><span data-stu-id="58230-182">For instance, scripts could be registered with the ScriptManager control programmatically during page load.</span></span>

## <a name="including-a-static-script-file-structure"></a><span data-ttu-id="58230-183">*包括静态脚本文件结构*</span><span class="sxs-lookup"><span data-stu-id="58230-183">*Including a Static Script File Structure*</span></span>

<span data-ttu-id="58230-184">使用静态脚本文件进行部署时，会丧失使用固有的 .NET 本地化方案的一些优点。</span><span class="sxs-lookup"><span data-stu-id="58230-184">When using static script files for deployment, you lose some of the benefits of using the inherent .NET localization scheme.</span></span> <span data-ttu-id="58230-185">主要是：你丢失了从包含脚本资源文件生成的自动类型;例如，在上面的演练中，资源已由来自 ScriptManager 控件的名为 Message 的自动生成类型公开。</span><span class="sxs-lookup"><span data-stu-id="58230-185">Primarily visible is that you lose the automatic type generated from including script resource files; in the above walkthrough, for example, resources were exposed by an automatically-generated type called Message from the ScriptManager control.</span></span>

<span data-ttu-id="58230-186">不过，使用静态脚本文件结构有一些优点。</span><span class="sxs-lookup"><span data-stu-id="58230-186">There are, however, some benefits to using a static script file structure.</span></span> <span data-ttu-id="58230-187">可以在不重新编译和重新部署附属程序集的情况下执行更新，也可以通过使用静态文件结构来替代嵌入的脚本，从而集成可能未随组件一起提供的一小部分功能。</span><span class="sxs-lookup"><span data-stu-id="58230-187">Updates can be performed without recompiling and redeploying satellite assemblies, and the use of a static file structure can also be done to override embedded script, to integrate a minor piece of functionality that may not have been shipped with a component.</span></span>

<span data-ttu-id="58230-188">Microsoft 建议在项目编译期间自动生成脚本资源，以避免版本控制问题。</span><span class="sxs-lookup"><span data-stu-id="58230-188">Microsoft recommends avoiding a version control issue by automatically generating your script resources during project compilation.</span></span> <span data-ttu-id="58230-189">在维护广泛的脚本代码库时，确保代码更改反映在每个本地化脚本中可能会变得越来越困难。</span><span class="sxs-lookup"><span data-stu-id="58230-189">When maintaining an extensive script code base, it can become increasingly difficult to ensure that code changes are reflected in each localized script.</span></span> <span data-ttu-id="58230-190">作为替代方法，只需维护一个逻辑脚本和多个本地化脚本，生成项目时合并文件。</span><span class="sxs-lookup"><span data-stu-id="58230-190">As an alternative, you can simply maintain one logic script and multiple localization scripts, merging the files while building the project.</span></span>

<span data-ttu-id="58230-191">由于没有要以声明方式包含的资源，因此应通过将 `<asp:ScriptElement>` 元素添加为 ScriptManager 控件的 `<Scripts>` 标记的子元素，或通过编程方式将 `ScriptReference` 对象添加到运行时页上的 `ScriptManager` 控件的 `Scripts` 属性来引用静态脚本文件。</span><span class="sxs-lookup"><span data-stu-id="58230-191">Because there are not resources to declaratively include, static script files should be referenced either by adding `<asp:ScriptElement>` elements as a child of the `<Scripts>` tag of the ScriptManager control, or by programmatically adding `ScriptReference` objects to the `Scripts` property of the `ScriptManager` control on the page at runtime.</span></span>

## <a name="the-scriptmanager-and-its-role-in-localization"></a><span data-ttu-id="58230-192">*ScriptManager 及其在本地化中的角色*</span><span class="sxs-lookup"><span data-stu-id="58230-192">*The ScriptManager and its Role in Localization*</span></span>

<span data-ttu-id="58230-193">ScriptManager 为本地化的应用程序启用了几种自动行为：</span><span class="sxs-lookup"><span data-stu-id="58230-193">The ScriptManager enables several automatic behaviors for localized applications:</span></span>

- <span data-ttu-id="58230-194">它基于设置和命名约定自动定位脚本文件;例如，在调试模式下，它加载启用了调试的脚本，并基于浏览器的用户界面选择加载本地化的脚本。</span><span class="sxs-lookup"><span data-stu-id="58230-194">It automatically locates script files based on settings and naming conventions; for instance, it loads debug-enabled scripts when in debugging mode, and loads localized scripts based on the browser's user interface selection.</span></span>
- <span data-ttu-id="58230-195">它支持区域性的定义，其中包括自定义区域性。</span><span class="sxs-lookup"><span data-stu-id="58230-195">It enables the definition of cultures, including custom cultures.</span></span>
- <span data-ttu-id="58230-196">它支持通过 HTTP 压缩脚本文件。</span><span class="sxs-lookup"><span data-stu-id="58230-196">It enables the compression of script files over HTTP.</span></span>
- <span data-ttu-id="58230-197">它缓存脚本以有效地管理多个请求。</span><span class="sxs-lookup"><span data-stu-id="58230-197">It caches scripts to efficiently manage many requests.</span></span>
- <span data-ttu-id="58230-198">它通过将其通过加密的 URL 来管道来向脚本添加一个间接层。</span><span class="sxs-lookup"><span data-stu-id="58230-198">It adds a layer of indirection to scripts by piping them through an encrypted URL.</span></span>

<span data-ttu-id="58230-199">可以通过编程方式或声明性标记将脚本引用添加到 ScriptManager 控件。</span><span class="sxs-lookup"><span data-stu-id="58230-199">Script references can be added to the ScriptManager control either programmatically or by declarative markup.</span></span> <span data-ttu-id="58230-200">当处理嵌入在网站项目本身之外的程序集中的脚本时，声明性标记特别有用，因为在通过推送修订时，脚本的名称可能不会更改。</span><span class="sxs-lookup"><span data-stu-id="58230-200">Declarative markup is particularly useful when working with scripts embedded in assemblies other than the web site project itself, as the name of the script will likely not change as revisions are pushed through.</span></span>

## <a name="summary"></a><span data-ttu-id="58230-201">总结</span><span class="sxs-lookup"><span data-stu-id="58230-201">Summary</span></span>

<span data-ttu-id="58230-202">随着 web 应用程序越来越多地增长到更大的受众，需要能够更广泛的文化和社区成为业务模型的核心;电子商务 web 应用程序需要能够处理外国货币，内容管理系统不仅需要能够显示其内容，而且还需要提供其他语言的导航提示和表单字段，并且公司需要知道这种需要方便.</span><span class="sxs-lookup"><span data-stu-id="58230-202">As web applications grow to reach a larger audience, the need to be able to reach broader cultures and communities becomes core to a business model; e-commerce web applications need to be able to deal with foreign currencies, content management systems need to be able to not only present their content but also their navigation hints and form fields in other languages, and companies need to know that this need is accessible.</span></span>

<span data-ttu-id="58230-203">.NET Framework 本质上支持丰富的本地化框架，使用附属程序集和 XML 资源（.resx）文件来提供一种统一的方法来查找资源字符串和图像。</span><span class="sxs-lookup"><span data-stu-id="58230-203">The .NET Framework intrinsically supports a rich localization framework, utilizing satellite assemblies and XML resource (.resx) files to present a uniform way to look up resource strings and images.</span></span> <span data-ttu-id="58230-204">ASP.NET AJAX 扩展（包括 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库）提供了对客户端代码的此编程模型的支持，从而实现了简单的资源字符串查找。</span><span class="sxs-lookup"><span data-stu-id="58230-204">The ASP.NET AJAX Extensions, including the Microsoft AJAX Framework and Microsoft AJAX Script Library, provide support for this programming model into client-side code, enabling easy resource string lookups.</span></span> <span data-ttu-id="58230-205">附属程序集支持通过 ScriptResource 自动包含脚本资源（实际的 .js 文件），只要文件名遵循给定的命名方案即可。</span><span class="sxs-lookup"><span data-stu-id="58230-205">Satellite assemblies support the automatic inclusion of script resources (actual .js files) through ScriptResource.axd as long as the filenames follow a given naming scheme.</span></span> <span data-ttu-id="58230-206">通过这种支持，ASP.NET AJAX 扩展简化了脚本本地化和应用程序的全球化。</span><span class="sxs-lookup"><span data-stu-id="58230-206">With this support, the ASP.NET AJAX Extensions simplify the localization of scripts and the globalization of applications.</span></span>

## <a name="bio"></a><span data-ttu-id="58230-207">*Bio*</span><span class="sxs-lookup"><span data-stu-id="58230-207">*Bio*</span></span>

<span data-ttu-id="58230-208">Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="58230-208">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="58230-209">可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客</span><span class="sxs-lookup"><span data-stu-id="58230-209">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58230-210">[上一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [下一页](understanding-asp-net-ajax-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="58230-210">[Previous](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
[Next](understanding-asp-net-ajax-web-services.md)</span></span>
