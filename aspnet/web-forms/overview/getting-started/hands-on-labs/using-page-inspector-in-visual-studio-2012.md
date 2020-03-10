---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 在 Visual Studio 2012 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: 在此动手实验中，你将发现一个新工具，用于在 Visual Studio 中查找和修复网页问题-Page Inspector。 Page Inspector 是一种新工具，
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473798"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="71118-104">在 Visual Studio 2012 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-104">Using Page Inspector in Visual Studio 2012</span></span>

<span data-ttu-id="71118-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="71118-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="71118-106">在此动手实验中，你将发现一个新工具，用于在 Visual Studio 中查找和修复网页问题-Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="71118-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="71118-107">Page Inspector 是一种新工具，它将浏览器诊断工具引入 Visual Studio，并提供浏览器、ASP.NET 和源代码之间的集成体验。</span><span class="sxs-lookup"><span data-stu-id="71118-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="71118-108">它直接在 Visual Studio IDE 内呈现网页（HTML、Web 窗体、ASP.NET MVC 或网页），并使你可以查看源代码和生成的输出。</span><span class="sxs-lookup"><span data-stu-id="71118-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="71118-109">Page Inspector 使你能够轻松地分解网站、快速构建页面并快速诊断问题。</span><span class="sxs-lookup"><span data-stu-id="71118-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="71118-110">如今我们有很多 Web 框架，可及时创建灵活、可缩放的网站，例如 ASP.NET MVC 和 WebForms。</span><span class="sxs-lookup"><span data-stu-id="71118-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="71118-111">另一方面，因为 IDE 不支持基于模板的页面和动态内容中的设计器视图，所以更难找到页面上的问题。</span><span class="sxs-lookup"><span data-stu-id="71118-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="71118-112">因此，必须在浏览器中打开这些网站才能查看他们对用户的显示方式。</span><span class="sxs-lookup"><span data-stu-id="71118-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="71118-113">Web 开发人员使用外部工具来查找定期在浏览器中运行的问题。</span><span class="sxs-lookup"><span data-stu-id="71118-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="71118-114">然后，它们返回 IDE 并开始修复。</span><span class="sxs-lookup"><span data-stu-id="71118-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="71118-115">IDE 中的这一前后活动，浏览器和分析工具可能效率低下，有时需要在每次重现问题时进行全新部署和缓存清洗。</span><span class="sxs-lookup"><span data-stu-id="71118-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="71118-116">Page Inspector 通过结合使用一组功能，将客户端（浏览器工具）与服务器（ASP.NET 和源代码）之间的 Web 开发的空白带入一起来。</span><span class="sxs-lookup"><span data-stu-id="71118-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="71118-117">使用 Page Inspector，可以查看源文件（包括服务器端代码）中的哪些元素生成了要在浏览器中呈现的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="71118-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="71118-118">还可以通过 Page Inspector 修改 CSS 属性和 DOM 元素特性，以查看立即反映在浏览器中的更改。</span><span class="sxs-lookup"><span data-stu-id="71118-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="71118-119">此动手实验将指导您完成 Page Inspector 功能，并向您演示如何使用这些功能来解决 Web 应用程序中的问题。</span><span class="sxs-lookup"><span data-stu-id="71118-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="71118-120">**此实验室包含两个使用类似流的练习，但面向不同的技术。如果你是 ASP.NET MVC 开发人员，请执行以下操作之一：如果你是 WebForms 开发人员，请执行两个练习**。</span><span class="sxs-lookup"><span data-stu-id="71118-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="71118-121">此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="71118-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="71118-122">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)提供。</span><span class="sxs-lookup"><span data-stu-id="71118-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="71118-123">目标</span><span class="sxs-lookup"><span data-stu-id="71118-123">Objectives</span></span>

<span data-ttu-id="71118-124">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="71118-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="71118-125">使用 Page Inspector 分解网站</span><span class="sxs-lookup"><span data-stu-id="71118-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="71118-126">检查和预览 CSS 样式更改与 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="71118-127">使用 Page Inspector 检测和修复网页中的问题</span><span class="sxs-lookup"><span data-stu-id="71118-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="71118-128">系统必备</span><span class="sxs-lookup"><span data-stu-id="71118-128">Prerequisites</span></span>

<span data-ttu-id="71118-129">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="71118-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="71118-130">适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。</span><span class="sxs-lookup"><span data-stu-id="71118-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="71118-131">Internet Explorer 9 或更高版本</span><span class="sxs-lookup"><span data-stu-id="71118-131">Internet Explorer 9 or higher</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="71118-132">练习</span><span class="sxs-lookup"><span data-stu-id="71118-132">Exercises</span></span>

<span data-ttu-id="71118-133">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="71118-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="71118-134">练习1：在 ASP.NET MVC 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="71118-135">练习2：在 WebForms 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="71118-136">每个练习都附带了一个起始解决方案，该解决方案位于练习的 "开始" 文件夹中，使您可以单独执行每个练习。</span><span class="sxs-lookup"><span data-stu-id="71118-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="71118-137">在练习的源代码中，您还会找到一个 End 文件夹，其中包含的 Visual Studio 解决方案的代码是完成相应练习中的步骤所产生的。</span><span class="sxs-lookup"><span data-stu-id="71118-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="71118-138">如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="71118-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

<span data-ttu-id="71118-139">完成本实验的估计时间： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="71118-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="71118-140">练习1：在 ASP.NET MVC 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="71118-141">在此练习中，您将学习如何使用**Page Inspector**预览和调试**ASP.NET MVC 4**解决方案。</span><span class="sxs-lookup"><span data-stu-id="71118-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="71118-142">首先，您将围绕该工具执行一小段重叠，以了解有助于 Web 调试过程的功能。</span><span class="sxs-lookup"><span data-stu-id="71118-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="71118-143">然后，您将在包含样式问题的网页中工作。</span><span class="sxs-lookup"><span data-stu-id="71118-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="71118-144">你将了解如何使用 Page Inspector 来查找生成问题并修复此问题的源代码。</span><span class="sxs-lookup"><span data-stu-id="71118-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="71118-145">任务 1-探索 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="71118-146">在此任务中，你将了解如何在 ASP.NET MVC 4 项目的上下文中使用 Page Inspector 显示照片库。</span><span class="sxs-lookup"><span data-stu-id="71118-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="71118-147">打开位于**Source/Ex1-MVC4/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="71118-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="71118-148">在继续之前，需要下载一些缺少的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="71118-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="71118-149">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="71118-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="71118-150">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="71118-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="71118-151">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="71118-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="71118-152">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="71118-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="71118-153">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="71118-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="71118-154">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="71118-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="71118-155">在解决方案资源管理器的 " **/Views/Home** " 项目文件夹下，找到 "**索引**" 视图，右键单击该文件夹，然后选择 **"在 Page Inspector 中查看**"。</span><span class="sxs-lookup"><span data-stu-id="71118-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="71118-156">![选择要预览的文件 Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "选择要预览的文件 Page Inspector")</span><span class="sxs-lookup"><span data-stu-id="71118-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="71118-157">*选择要预览的文件 Page Inspector*</span><span class="sxs-lookup"><span data-stu-id="71118-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="71118-158">"Page Inspector" 窗口将显示映射到所选源视图的 */Home/Index* URL。</span><span class="sxs-lookup"><span data-stu-id="71118-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![第一次联系 PageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="71118-160">*第一次与 Page Inspector*</span><span class="sxs-lookup"><span data-stu-id="71118-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="71118-161">Page Inspector 工具已集成到 Visual Studio 环境中。</span><span class="sxs-lookup"><span data-stu-id="71118-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="71118-162">该检查器包含一个嵌入式浏览器以及一个功能强大的 HTML 探查器。</span><span class="sxs-lookup"><span data-stu-id="71118-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="71118-163">请注意，无需运行解决方案即可查看页面的外观。</span><span class="sxs-lookup"><span data-stu-id="71118-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-164">当 Page Inspector 浏览器的宽度小于打开的页面的宽度时，将不会正确显示页面。</span><span class="sxs-lookup"><span data-stu-id="71118-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="71118-165">如果发生这种情况，请调整 Page Inspector 的宽度。</span><span class="sxs-lookup"><span data-stu-id="71118-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="71118-166">单击 Page Inspector 中的 "**文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71118-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="71118-167">你将看到构成索引页的所有源文件。</span><span class="sxs-lookup"><span data-stu-id="71118-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="71118-168">此功能有助于一目了然地识别所有元素，尤其是在使用分部视图和模板时。</span><span class="sxs-lookup"><span data-stu-id="71118-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="71118-169">请注意，如果单击这些链接，也可以打开每个文件。</span><span class="sxs-lookup"><span data-stu-id="71118-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![The-Files-tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="71118-171">*"文件" 选项卡*</span><span class="sxs-lookup"><span data-stu-id="71118-171">*The Files tab*</span></span>
5. <span data-ttu-id="71118-172">单击位于选项卡左侧的 "**切换检查模式**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="71118-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="71118-173">此工具可让你选择页面的任何元素，并查看其 HTML 和 Razor 代码。</span><span class="sxs-lookup"><span data-stu-id="71118-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![Toggle-Inspection-Mode-button](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="71118-175">*切换检查模式按钮*</span><span class="sxs-lookup"><span data-stu-id="71118-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="71118-176">在 Page Inspector 浏览器中，将鼠标指针移动到页面元素上。</span><span class="sxs-lookup"><span data-stu-id="71118-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="71118-177">在将鼠标指针移动到呈现的页的任何部分时，将显示元素类型，并在 Visual Studio 编辑器中突出显示相应的源标记或代码。</span><span class="sxs-lookup"><span data-stu-id="71118-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![操作中的检查模式](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="71118-179">*操作中的检查模式*</span><span class="sxs-lookup"><span data-stu-id="71118-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-180">不要最大化 Page Inspector 窗口，否则将无法看到显示源代码的预览选项卡。</span><span class="sxs-lookup"><span data-stu-id="71118-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="71118-181">如果在最大化时单击 Page Inspector 中的元素，则将显示选定内容的源代码，但它将隐藏 "Page Inspector" 窗口。</span><span class="sxs-lookup"><span data-stu-id="71118-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="71118-182">如果你注意到**索引 cshtml**文件，你会注意到，将突出显示生成所选元素的源代码部分。</span><span class="sxs-lookup"><span data-stu-id="71118-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="71118-183">此功能有助于对长源文件进行编辑，同时提供直接快捷的方法来访问代码。</span><span class="sxs-lookup"><span data-stu-id="71118-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![检查元素](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="71118-185">*检查元素*</span><span class="sxs-lookup"><span data-stu-id="71118-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="71118-186">单击 "**切换检查模式**" 按钮（![选择 "html" 选项卡以显示 Page Inspector 浏览器中呈现的 html 代码。](using-page-inspector-in-visual-studio-2012/_static/image7.png "选择 "HTML" 选项卡以显示 Page Inspector 浏览器中呈现的 HTML 代码。")</span><span class="sxs-lookup"><span data-stu-id="71118-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="71118-187">）来禁用游标。</span><span class="sxs-lookup"><span data-stu-id="71118-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="71118-188">选择 " **html** " 选项卡以显示 Page Inspector 浏览器中呈现的 html 代码。</span><span class="sxs-lookup"><span data-stu-id="71118-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="71118-189">在 HTML 标记中，找到带有 Koala 链接的列表项并将其选中。</span><span class="sxs-lookup"><span data-stu-id="71118-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="71118-190">请注意，在选择代码时，相应的输出会自动在浏览器中突出显示。</span><span class="sxs-lookup"><span data-stu-id="71118-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="71118-191">此功能可用于查看 HTML 块在页面上的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="71118-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="71118-192">![在页面中选择 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image8.png "在页面中选择 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="71118-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="71118-193">*在页面中选择 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="71118-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="71118-194">单击 "**切换检查模式**" 按钮以启用*检查模式*并单击导航栏。</span><span class="sxs-lookup"><span data-stu-id="71118-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="71118-195">在 HTML 代码的右侧，在 "样式" 窗格中，将显示一个列表，其中包含应用于所选元素的 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="71118-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-196">由于标头是网站布局的一部分，因此 Page Inspector 还将打开 \_Layout 文件，并突出显示受影响的代码段。</span><span class="sxs-lookup"><span data-stu-id="71118-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![发现样式](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="71118-198">*查找所选元素的样式和源文件*</span><span class="sxs-lookup"><span data-stu-id="71118-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="71118-199">启用切换检测指针后，将鼠标指针移动到蓝色的特色栏下方，并单击半圆圈。</span><span class="sxs-lookup"><span data-stu-id="71118-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="71118-200">![选择元素](using-page-inspector-in-visual-studio-2012/_static/image10.png "选择元素")</span><span class="sxs-lookup"><span data-stu-id="71118-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="71118-201">*选择元素*</span><span class="sxs-lookup"><span data-stu-id="71118-201">*Selecting an element*</span></span>
12. <span data-ttu-id="71118-202">在 "样式" 窗格中，找到 "**主-内容**" 组下的 "**背景图像**" 项。</span><span class="sxs-lookup"><span data-stu-id="71118-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="71118-203">**取消选中** **背景图像**，看看会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="71118-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="71118-204">你会注意到，浏览器会立即反映更改并隐藏圆圈。</span><span class="sxs-lookup"><span data-stu-id="71118-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-205">应用于 "Page Inspector 样式" 选项卡上的更改不会影响原始样式表。</span><span class="sxs-lookup"><span data-stu-id="71118-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="71118-206">您可以根据需要取消选中样式或更改它们的值，但它们将在刷新页面后还原。</span><span class="sxs-lookup"><span data-stu-id="71118-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="71118-207">![启用和禁用 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image11.png "启用和禁用 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="71118-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="71118-208">*启用和禁用 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="71118-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="71118-209">现在，使用检查模式在页眉上单击 "**你的徽标**"。</span><span class="sxs-lookup"><span data-stu-id="71118-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="71118-210">在 "**样式**" 选项卡中，找到 "**网站标题**" 组下的 "**字体大小**" CSS 属性。</span><span class="sxs-lookup"><span data-stu-id="71118-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="71118-211">双击属性值并将 2.3 em 值替换为**3 em**，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="71118-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="71118-212">请注意，标题看起来更大。</span><span class="sxs-lookup"><span data-stu-id="71118-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="71118-213">![更改 Page Inspector 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image12.png "更改 Page Inspector 中的 CSS 值")</span><span class="sxs-lookup"><span data-stu-id="71118-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="71118-214">*更改 Page Inspector 中的 CSS 值*</span><span class="sxs-lookup"><span data-stu-id="71118-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="71118-215">单击 "**跟踪样式**" 选项卡，该选项卡位于 Page Inspector 右窗格中。</span><span class="sxs-lookup"><span data-stu-id="71118-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="71118-216">这是查看应用于选择的所有样式的另一种方法，按属性名称排序。</span><span class="sxs-lookup"><span data-stu-id="71118-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSS 样式跟踪](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="71118-218">*对所选元素的 CSS 样式跟踪*</span><span class="sxs-lookup"><span data-stu-id="71118-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="71118-219">Page Inspector 的另一项功能是布局窗格。</span><span class="sxs-lookup"><span data-stu-id="71118-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="71118-220">使用检查模式，选择导航栏，然后单击右窗格中的 "**布局**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71118-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="71118-221">您将看到所选元素的准确大小，以及其偏移、边距、填充和边框大小。</span><span class="sxs-lookup"><span data-stu-id="71118-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="71118-222">请注意，您还可以通过此视图修改这些值。</span><span class="sxs-lookup"><span data-stu-id="71118-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="71118-223">![Page Inspector 中的元素布局](using-page-inspector-in-visual-studio-2012/_static/image14.png "Page Inspector 中的元素布局")</span><span class="sxs-lookup"><span data-stu-id="71118-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="71118-224">*Page Inspector 中的元素布局*</span><span class="sxs-lookup"><span data-stu-id="71118-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="71118-225">任务 2-查找和修复照片库中的样式问题</span><span class="sxs-lookup"><span data-stu-id="71118-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="71118-226">如何诊断 Visual Studio 早期版本的网页问题？</span><span class="sxs-lookup"><span data-stu-id="71118-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="71118-227">您可能很熟悉在 Visual Studio IDE 之外（例如 Internet Explorer 开发人员工具或 Firebug）运行的 web 调试工具。</span><span class="sxs-lookup"><span data-stu-id="71118-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="71118-228">浏览器仅了解 HTML、脚本和样式，而基础框架生成将呈现的 HTML。</span><span class="sxs-lookup"><span data-stu-id="71118-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="71118-229">出于此原因，通常需要部署整个站点以查看网页的外观。</span><span class="sxs-lookup"><span data-stu-id="71118-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="71118-230">当你想要检测并修复网站中的问题时，你可能需要执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="71118-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="71118-231">从 Visual Studio 运行解决方案，或在 web 服务器上部署页面。</span><span class="sxs-lookup"><span data-stu-id="71118-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="71118-232">在浏览器中，打开你使用的开发人员工具，或者只是打开源代码和样式并尝试匹配问题。</span><span class="sxs-lookup"><span data-stu-id="71118-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="71118-233">若要查找所涉及的文件，您可以使用 &quot;搜索&quot; 或 &quot;使用样式类的名称在文件&quot; 功能中搜索。</span><span class="sxs-lookup"><span data-stu-id="71118-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="71118-234">检测到错误后，停止 Web 浏览器和服务器。</span><span class="sxs-lookup"><span data-stu-id="71118-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="71118-235">清除浏览器缓存。</span><span class="sxs-lookup"><span data-stu-id="71118-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="71118-236">返回到 Visual Studio 以应用修补程序。</span><span class="sxs-lookup"><span data-stu-id="71118-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="71118-237">重复所有要测试的步骤。</span><span class="sxs-lookup"><span data-stu-id="71118-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="71118-238">由于 ASP.NET MVC 4 中没有实际 WYSIWYG，因此在运行或部署 web 应用程序后，会在稍后的阶段检测到大多数样式问题。</span><span class="sxs-lookup"><span data-stu-id="71118-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="71118-239">现在，通过 Page Inspector，可以在不运行解决方案的情况下预览任何页面。</span><span class="sxs-lookup"><span data-stu-id="71118-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="71118-240">在此任务中，您将使用 Page inspector 并修复照片库应用程序的一些问题。</span><span class="sxs-lookup"><span data-stu-id="71118-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="71118-241">使用 Page Inspector，找到该标头左侧的 "**注册**" 和 "**登录**" 链接。</span><span class="sxs-lookup"><span data-stu-id="71118-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="71118-242">请注意，链接不会显示在右侧的预期位置，它们显示为项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="71118-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="71118-243">现在，将链接向右对齐，并相应地对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="71118-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="71118-244">![查找注册和登录链接](using-page-inspector-in-visual-studio-2012/_static/image15.png "查找注册和登录链接")</span><span class="sxs-lookup"><span data-stu-id="71118-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="71118-245">*查找注册和登录链接*</span><span class="sxs-lookup"><span data-stu-id="71118-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="71118-246">选中 "切换检查模式" 时，单击 "关闭到"，但不要打开 "注册" 链接以打开其代码。</span><span class="sxs-lookup"><span data-stu-id="71118-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="71118-247">请注意，链接的源代码位于 **\_loginpartial.cshtml**文件中，而不是位于 \_的位置，也可能是您第一次查找的位置。</span><span class="sxs-lookup"><span data-stu-id="71118-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="71118-248">您已直接放置在正确的源文件中。</span><span class="sxs-lookup"><span data-stu-id="71118-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="71118-249">在 "**样式**" 选项卡中，找到并单击 " **\<" 部分 > "#login**项"，这是这些链接的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="71118-249">In the **Styles** tab, locate and click the **\<section> #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="71118-250">请注意，单击后，" **#login** " 样式会自动置于 "**站点导航**" 中。</span><span class="sxs-lookup"><span data-stu-id="71118-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="71118-251">而且，代码现已突出显示。</span><span class="sxs-lookup"><span data-stu-id="71118-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="71118-252">![选择 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image16.png "选择 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="71118-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="71118-253">*选择 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="71118-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="71118-254">通过删除开始和结束字符并保存**web.config**文件，取消突出显示的代码中的**文本对齐**属性。</span><span class="sxs-lookup"><span data-stu-id="71118-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="71118-255">Page Inspector 知道构成当前页的所有不同文件，并且它可以检测到这些文件中的任何一个发生更改的时间。</span><span class="sxs-lookup"><span data-stu-id="71118-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="71118-256">只要浏览器中的当前页与源文件不同步，它就会发出警报。</span><span class="sxs-lookup"><span data-stu-id="71118-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="71118-257">在 Page Inspector 浏览器中，单击地址栏下面的栏以重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="71118-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![重新加载页面](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="71118-259">*重新加载页面*</span><span class="sxs-lookup"><span data-stu-id="71118-259">*Reloading the page*</span></span>

    <span data-ttu-id="71118-260">现在，链接位于右侧，但其外观仍类似于项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="71118-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="71118-261">现在，你将删除项目符号并水平对齐链接。</span><span class="sxs-lookup"><span data-stu-id="71118-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![已更新页面](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="71118-263">*已更新页面*</span><span class="sxs-lookup"><span data-stu-id="71118-263">*Updated page*</span></span>
6. <span data-ttu-id="71118-264">使用检查模式，选择包含 &quot;注册&quot; 的任何 **&lt;li&gt;** 项，并 &quot;&quot; 的链接。</span><span class="sxs-lookup"><span data-stu-id="71118-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="71118-265">然后，单击 " **&lt;" 部分&gt; "#login** " 项 "以访问**样式。 css**代码。</span><span class="sxs-lookup"><span data-stu-id="71118-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="71118-266">![查找样式](using-page-inspector-in-visual-studio-2012/_static/image19.png "查找样式")</span><span class="sxs-lookup"><span data-stu-id="71118-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="71118-267">*查找样式*</span><span class="sxs-lookup"><span data-stu-id="71118-267">*Finding the style*</span></span>
7. <span data-ttu-id="71118-268">在**Style css**中，取消注释 **#login li**项的代码。</span><span class="sxs-lookup"><span data-stu-id="71118-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="71118-269">要添加的样式将隐藏项目符号并水平显示项。</span><span class="sxs-lookup"><span data-stu-id="71118-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="71118-270">![Restyling 登录链接](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling 登录链接")</span><span class="sxs-lookup"><span data-stu-id="71118-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="71118-271">*Restyling 登录链接*</span><span class="sxs-lookup"><span data-stu-id="71118-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="71118-272">保存**样式 .css**文件，然后单击地址下面的栏以重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="71118-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="71118-273">请注意，链接正确显示。</span><span class="sxs-lookup"><span data-stu-id="71118-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="71118-274">![与右侧对齐的链接](using-page-inspector-in-visual-studio-2012/_static/image21.png "与右侧对齐的链接")</span><span class="sxs-lookup"><span data-stu-id="71118-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="71118-275">*与右侧对齐的链接*</span><span class="sxs-lookup"><span data-stu-id="71118-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="71118-276">最后，您将更改标题标题。</span><span class="sxs-lookup"><span data-stu-id="71118-276">Finally, you will change the header title.</span></span> <span data-ttu-id="71118-277">使用检查模式在此处单击**你的徽标**，并访问生成它的源代码。</span><span class="sxs-lookup"><span data-stu-id="71118-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="71118-278">现在，你正处于 **\_Layout**，请将 "**你的徽标徽标**" 替换为 "**照片库**"。</span><span class="sxs-lookup"><span data-stu-id="71118-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="71118-279">保存并更新 Page Inspector 浏览器。</span><span class="sxs-lookup"><span data-stu-id="71118-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="71118-280">![分配新标题](using-page-inspector-in-visual-studio-2012/_static/image22.png "分配新标题")</span><span class="sxs-lookup"><span data-stu-id="71118-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="71118-281">*分配新标题*</span><span class="sxs-lookup"><span data-stu-id="71118-281">*Assigning a new title*</span></span>

    ![照片库页面](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="71118-283">*照片库页面已更新*</span><span class="sxs-lookup"><span data-stu-id="71118-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="71118-284">最后，选择**PhotoGallery**项目，并按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="71118-284">Finally, select the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="71118-285">签出所有更改都按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="71118-285">Check out all the changes work as expected.</span></span>

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="71118-286">练习2：在 WebForms 项目中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="71118-287">在此练习中，您将学习如何使用 Page Inspector 预览和调试 WebForms 解决方案。</span><span class="sxs-lookup"><span data-stu-id="71118-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="71118-288">你将首先对该工具执行简短的重叠，以了解有助于 Web 调试过程的 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="71118-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="71118-289">然后，您将在包含样式问题的网页中工作。</span><span class="sxs-lookup"><span data-stu-id="71118-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="71118-290">你将了解如何使用 Page Inspector 来查找生成问题并修复此问题的源代码。</span><span class="sxs-lookup"><span data-stu-id="71118-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="71118-291">任务 1-探索 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="71118-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="71118-292">在此任务中，你将了解如何在 WebForms 项目的上下文中使用 Page Inspector 功能，该项目显示照片库。</span><span class="sxs-lookup"><span data-stu-id="71118-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="71118-293">打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-WebForms/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="71118-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="71118-294">在继续之前，需要下载一些缺少的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="71118-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="71118-295">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="71118-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="71118-296">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="71118-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="71118-297">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="71118-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="71118-298">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="71118-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="71118-299">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="71118-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="71118-300">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="71118-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="71118-301">在解决方案资源管理器中，找到 " **default.aspx** " 页，右键单击它，然后选择 **"在 Page Inspector 中查看"** 。</span><span class="sxs-lookup"><span data-stu-id="71118-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="71118-302">![用 Page Inspector 打开 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image24.png "用 Page Inspector 打开 default.aspx")</span><span class="sxs-lookup"><span data-stu-id="71118-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="71118-303">*用 Page Inspector 打开 default.aspx*</span><span class="sxs-lookup"><span data-stu-id="71118-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="71118-304">"Page Inspector" 窗口将显示 "default.aspx"。</span><span class="sxs-lookup"><span data-stu-id="71118-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="71118-305">![在 Page Inspector 中查看 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image25.png "在 Page Inspector 中查看 default.aspx")</span><span class="sxs-lookup"><span data-stu-id="71118-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="71118-306">*在 Page Inspector 中查看 default.aspx*</span><span class="sxs-lookup"><span data-stu-id="71118-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="71118-307">Page Inspector 工具已集成到 Visual Studio 环境中。</span><span class="sxs-lookup"><span data-stu-id="71118-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="71118-308">该检查器包含一个嵌入浏览器以及一个将显示选定代码的功能强大的 HTML 探查器。</span><span class="sxs-lookup"><span data-stu-id="71118-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="71118-309">请注意，无需运行解决方案即可查看页面的外观。</span><span class="sxs-lookup"><span data-stu-id="71118-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-310">当 Page Inspector 浏览器的宽度小于打开的页面的宽度时，将不会正确显示页面。</span><span class="sxs-lookup"><span data-stu-id="71118-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="71118-311">如果发生这种情况，请调整 Page Inspector 的宽度。</span><span class="sxs-lookup"><span data-stu-id="71118-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="71118-312">单击 Page Inspector 中的 "**文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71118-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="71118-313">你将看到构成呈现的默认页面的所有源文件。</span><span class="sxs-lookup"><span data-stu-id="71118-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="71118-314">这是一种非常有用的功能，可帮助您一目了然地识别所有元素，尤其是在使用用户控件和母版页时。</span><span class="sxs-lookup"><span data-stu-id="71118-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="71118-315">请注意，你也可以导航到每个文件。</span><span class="sxs-lookup"><span data-stu-id="71118-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="71118-316">!["文件" 选项卡](using-page-inspector-in-visual-studio-2012/_static/image26.png ""文件" 选项卡")</span><span class="sxs-lookup"><span data-stu-id="71118-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="71118-317">*"文件" 选项卡*</span><span class="sxs-lookup"><span data-stu-id="71118-317">*The Files tab*</span></span>
5. <span data-ttu-id="71118-318">单击位于选项卡左侧的 "**切换检查模式**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="71118-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="71118-319">此工具可让你选择页面的任何元素，并查看其 HTML 代码和 .aspx 源。</span><span class="sxs-lookup"><span data-stu-id="71118-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="71118-320">![切换检查模式按钮](using-page-inspector-in-visual-studio-2012/_static/image27.png "切换检查模式按钮")</span><span class="sxs-lookup"><span data-stu-id="71118-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="71118-321">*切换检查模式按钮*</span><span class="sxs-lookup"><span data-stu-id="71118-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="71118-322">在 Page Inspector 浏览器中，将鼠标移到页面元素上。</span><span class="sxs-lookup"><span data-stu-id="71118-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="71118-323">在将鼠标指针移动到呈现的页的任何部分时，将显示元素类型，并在 Visual Studio 编辑器中突出显示相应的源标记或代码。</span><span class="sxs-lookup"><span data-stu-id="71118-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="71118-324">![操作中的检查模式](using-page-inspector-in-visual-studio-2012/_static/image28.png "操作中的检查模式")</span><span class="sxs-lookup"><span data-stu-id="71118-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="71118-325">*操作中的检查模式*</span><span class="sxs-lookup"><span data-stu-id="71118-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-326">不要最大化 Page Inspector 窗口，否则将无法看到显示源代码的预览选项卡。</span><span class="sxs-lookup"><span data-stu-id="71118-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="71118-327">如果在最大化时单击 Page Inspector 中的元素，则将显示选定内容的源代码，但它将隐藏 "Page Inspector" 窗口。</span><span class="sxs-lookup"><span data-stu-id="71118-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="71118-328">如果你注意到**默认的 .aspx**文件，你会注意到，将突出显示生成所选元素的源代码部分。</span><span class="sxs-lookup"><span data-stu-id="71118-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="71118-329">此功能简化了长源文件的版本，并提供了一种直接快捷的方法来访问代码。</span><span class="sxs-lookup"><span data-stu-id="71118-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="71118-330">![检查元素](using-page-inspector-in-visual-studio-2012/_static/image29.png "检查元素")</span><span class="sxs-lookup"><span data-stu-id="71118-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="71118-331">*检查元素*</span><span class="sxs-lookup"><span data-stu-id="71118-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="71118-332">单击 "**切换检查模式**" 按钮![（"html"](using-page-inspector-in-visual-studio-2012/_static/image30.png "选择-html-制表符-------------------------------------") ---------------------------------------</span><span class="sxs-lookup"><span data-stu-id="71118-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="71118-333">）（位于 Page Inspector 选项卡中）来禁用游标。</span><span class="sxs-lookup"><span data-stu-id="71118-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="71118-334">选择 " **html** " 选项卡以显示 Page Inspector 浏览器中呈现的 html 代码。</span><span class="sxs-lookup"><span data-stu-id="71118-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="71118-335">在 HTML 代码中，找到带有 Koala 链接的列表项并将其选中。</span><span class="sxs-lookup"><span data-stu-id="71118-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="71118-336">请注意，在选择代码时，相应的输出会自动突出显示 "浏览器"。</span><span class="sxs-lookup"><span data-stu-id="71118-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="71118-337">此功能可用于查看 HTML 块在页面上的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="71118-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="71118-338">![在页面中选择一个 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image31.png "在页面中选择一个 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="71118-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="71118-339">*在页面中选择一个 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="71118-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="71118-340">单击 "**切换检查模式**" 按钮以启用*检查模式*并单击导航栏。</span><span class="sxs-lookup"><span data-stu-id="71118-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="71118-341">在 HTML 代码的右侧，在 "样式" 窗格中，将显示一个列表，其中包含应用于所选元素的 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="71118-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-342">由于标头是网站布局的一部分，因此 Page Inspector 还将打开网站文件，并突出显示受影响的代码段。</span><span class="sxs-lookup"><span data-stu-id="71118-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="71118-343">![发现样式 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "查找所选元素的样式和源文件")</span><span class="sxs-lookup"><span data-stu-id="71118-343">![Discovering styles WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="71118-344">*查找所选元素的样式和源文件*</span><span class="sxs-lookup"><span data-stu-id="71118-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="71118-345">启用切换检测指针后，将鼠标指针移动到菜单栏的下方，并单击空白半圆圈。</span><span class="sxs-lookup"><span data-stu-id="71118-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="71118-346">![选择元素](using-page-inspector-in-visual-studio-2012/_static/image33.png "选择元素")</span><span class="sxs-lookup"><span data-stu-id="71118-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="71118-347">*选择元素*</span><span class="sxs-lookup"><span data-stu-id="71118-347">*Selecting an element*</span></span>
12. <span data-ttu-id="71118-348">在 "样式" 窗格中，找到 "**主-内容**" 组下的 "**背景图像**" 项。</span><span class="sxs-lookup"><span data-stu-id="71118-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="71118-349">**取消选中** **背景图像**，看看会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="71118-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="71118-350">你会注意到，浏览器会立即反映更改并隐藏圆圈。</span><span class="sxs-lookup"><span data-stu-id="71118-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71118-351">应用于 "Page Inspector 样式" 选项卡上的更改不会影响原始样式表。</span><span class="sxs-lookup"><span data-stu-id="71118-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="71118-352">您可以根据需要取消选中样式或更改它们的值，但它们将在刷新页面后还原。</span><span class="sxs-lookup"><span data-stu-id="71118-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="71118-353">![启用和禁用 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "启用和禁用 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="71118-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="71118-354">*启用和禁用 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="71118-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="71118-355">现在，使用检查模式在页眉上单击 "**你**的**徽标**"。</span><span class="sxs-lookup"><span data-stu-id="71118-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="71118-356">在 "**样式**" 选项卡中，找到 "**网站标题**" 组下的 "**字体大小**" CSS 属性。</span><span class="sxs-lookup"><span data-stu-id="71118-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="71118-357">双击属性一次以编辑其值。</span><span class="sxs-lookup"><span data-stu-id="71118-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="71118-358">将 2.3 em 值替换为**3em**，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="71118-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="71118-359">请注意，标题看起来更大。</span><span class="sxs-lookup"><span data-stu-id="71118-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="71118-360">![更改页面 Inspector2 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image35.png "更改 Page Inspector 中的 CSS 值")</span><span class="sxs-lookup"><span data-stu-id="71118-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="71118-361">*更改 Page Inspector 中的 CSS 值*</span><span class="sxs-lookup"><span data-stu-id="71118-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="71118-362">单击 "**跟踪样式**" 选项卡，该选项卡位于 Page Inspector 右窗格中。</span><span class="sxs-lookup"><span data-stu-id="71118-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="71118-363">这是查看应用于选择的所有样式的另一种方法，按属性名称排序。</span><span class="sxs-lookup"><span data-stu-id="71118-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="71118-364">![对所选元素的 CSS 样式跟踪](using-page-inspector-in-visual-studio-2012/_static/image36.png "对所选元素的 CSS 样式跟踪")</span><span class="sxs-lookup"><span data-stu-id="71118-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="71118-365">*对所选元素的 CSS 样式跟踪*</span><span class="sxs-lookup"><span data-stu-id="71118-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="71118-366">Page Inspector 的另一项功能是布局窗格。</span><span class="sxs-lookup"><span data-stu-id="71118-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="71118-367">使用检查模式，选择导航栏，然后单击右窗格中的 "**布局**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71118-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="71118-368">您将看到所选元素的准确大小，以及其偏移、边距、填充和边框大小。</span><span class="sxs-lookup"><span data-stu-id="71118-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="71118-369">请注意，您还可以通过此视图修改这些值。</span><span class="sxs-lookup"><span data-stu-id="71118-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="71118-370">![Page Inspector 中的元素布局](using-page-inspector-in-visual-studio-2012/_static/image37.png "Page Inspector 中的元素布局")</span><span class="sxs-lookup"><span data-stu-id="71118-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="71118-371">*Page Inspector 中的元素布局*</span><span class="sxs-lookup"><span data-stu-id="71118-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="71118-372">任务 2-查找和修复照片库中的样式问题</span><span class="sxs-lookup"><span data-stu-id="71118-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="71118-373">如何诊断 Visual Studio 早期版本的网页问题？</span><span class="sxs-lookup"><span data-stu-id="71118-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="71118-374">您可能很熟悉在 Visual Studio IDE 之外（例如 Internet Explorer 开发人员工具或 Firebug）运行的 web 调试工具。</span><span class="sxs-lookup"><span data-stu-id="71118-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="71118-375">浏览器仅了解 HTML、脚本和样式，而基础框架生成将呈现的 HTML。</span><span class="sxs-lookup"><span data-stu-id="71118-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="71118-376">出于此原因，通常需要部署整个站点以查看网页的外观。</span><span class="sxs-lookup"><span data-stu-id="71118-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="71118-377">当你想要检测并修复网站中的问题时，你可能需要执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="71118-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="71118-378">从 Visual Studio 运行解决方案，或在 web 服务器上部署页面。</span><span class="sxs-lookup"><span data-stu-id="71118-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="71118-379">在浏览器中，打开你使用的开发人员工具，或者只是打开源代码和样式并尝试匹配问题。</span><span class="sxs-lookup"><span data-stu-id="71118-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="71118-380">若要查找所涉及的文件，您已使用 &quot;搜索&quot; 或 &quot;使用样式类的名称在文件&quot; 功能中搜索。</span><span class="sxs-lookup"><span data-stu-id="71118-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="71118-381">检测到错误后，停止 Web 浏览器和服务器。</span><span class="sxs-lookup"><span data-stu-id="71118-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="71118-382">清除浏览器缓存。</span><span class="sxs-lookup"><span data-stu-id="71118-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="71118-383">返回到 Visual Studio 以应用修补程序。</span><span class="sxs-lookup"><span data-stu-id="71118-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="71118-384">重复所有要测试的步骤。</span><span class="sxs-lookup"><span data-stu-id="71118-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="71118-385">由于 ASP.NET WebForms 中没有实际 WYSIWYG，因此在运行或部署后，会在稍后的阶段检测到一些样式问题。</span><span class="sxs-lookup"><span data-stu-id="71118-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="71118-386">现在，通过 Page Inspector，可以在不运行解决方案的情况下预览任何页面。</span><span class="sxs-lookup"><span data-stu-id="71118-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="71118-387">在此任务中，您将使用 Page inspector 来修复照片库应用程序的某些问题。</span><span class="sxs-lookup"><span data-stu-id="71118-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="71118-388">在以下步骤中，你将检测并快速修复标头中的一些简单样式问题。</span><span class="sxs-lookup"><span data-stu-id="71118-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="71118-389">使用页面检查，找到位于页眉左侧的 "**注册**" 和 "**登录**" 链接。</span><span class="sxs-lookup"><span data-stu-id="71118-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="71118-390">请注意，该链接不会显示在右侧的预期位置。</span><span class="sxs-lookup"><span data-stu-id="71118-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="71118-391">现在，将链接向右对齐并相应地对其进行调整。</span><span class="sxs-lookup"><span data-stu-id="71118-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="71118-392">![位于左侧的 "登录" 链接](using-page-inspector-in-visual-studio-2012/_static/image38.png "位于左侧的 "登录" 链接")</span><span class="sxs-lookup"><span data-stu-id="71118-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="71118-393">*位于左侧的 "登录" 链接*</span><span class="sxs-lookup"><span data-stu-id="71118-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="71118-394">选中 "切换检查模式" 后，选择 "登录" 链接以打开其代码。</span><span class="sxs-lookup"><span data-stu-id="71118-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="71118-395">请注意，链接源代码位于**站点 .master**文件中，而不是在 default.aspx 页面中，这是你可能首先查看的位置;您已直接放置在正确的源文件中。</span><span class="sxs-lookup"><span data-stu-id="71118-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="71118-396">在 "**样式**" 选项卡中，找到并单击 " **&lt;" 部分&gt; "#login**项"，这是这些链接的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="71118-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="71118-397">请注意，单击后，" **#login** " 样式会自动置于 "**站点导航**" 中。</span><span class="sxs-lookup"><span data-stu-id="71118-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="71118-398">而且，代码现已突出显示。</span><span class="sxs-lookup"><span data-stu-id="71118-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="71118-399">![选择 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image39.png "选择 CSS 样式")</span><span class="sxs-lookup"><span data-stu-id="71118-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="71118-400">*选择 CSS 样式*</span><span class="sxs-lookup"><span data-stu-id="71118-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="71118-401">通过删除开始和结束字符并保存**web.config**文件，取消突出显示的代码中的**文本对齐**属性。</span><span class="sxs-lookup"><span data-stu-id="71118-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="71118-402">Page Inspector 知道构成当前页的所有不同文件，并且它可以检测到这些文件中的任何一个发生更改的时间。</span><span class="sxs-lookup"><span data-stu-id="71118-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="71118-403">只要浏览器中的当前页与源文件不同步，它就会发出警报。</span><span class="sxs-lookup"><span data-stu-id="71118-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="71118-404">在 Page Inspector 浏览器中，单击地址栏下面的栏以保存更改并重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="71118-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![重新加载页面](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="71118-406">*重新加载页面*</span><span class="sxs-lookup"><span data-stu-id="71118-406">*Reloading the page*</span></span>

    <span data-ttu-id="71118-407">现在，链接位于右侧，但其外观仍类似于项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="71118-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="71118-408">现在，你将删除项目符号并水平对齐链接。</span><span class="sxs-lookup"><span data-stu-id="71118-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![已更新页面](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="71118-410">*已更新页面*</span><span class="sxs-lookup"><span data-stu-id="71118-410">*Updated page*</span></span>
6. <span data-ttu-id="71118-411">使用检查模式，选择包含 &quot;注册&quot; 的任何 **&lt;li&gt;** 项，并 &quot;&quot; 的链接。</span><span class="sxs-lookup"><span data-stu-id="71118-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="71118-412">然后，单击 " **&lt;" 部分&gt; "#login** " 项 "以访问**样式。 css**代码。</span><span class="sxs-lookup"><span data-stu-id="71118-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="71118-413">![查找样式](using-page-inspector-in-visual-studio-2012/_static/image42.png "查找样式")</span><span class="sxs-lookup"><span data-stu-id="71118-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="71118-414">*查找样式*</span><span class="sxs-lookup"><span data-stu-id="71118-414">*Finding the style*</span></span>
7. <span data-ttu-id="71118-415">在**Style css**中，取消注释 **#login li**项的代码。</span><span class="sxs-lookup"><span data-stu-id="71118-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="71118-416">要添加的样式将隐藏项目符号并水平显示项。</span><span class="sxs-lookup"><span data-stu-id="71118-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="71118-417">![Restyling 登录链接](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling 登录链接")</span><span class="sxs-lookup"><span data-stu-id="71118-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="71118-418">*Restyling 登录链接*</span><span class="sxs-lookup"><span data-stu-id="71118-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="71118-419">保存**样式 .css**文件，然后单击地址下面的栏以重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="71118-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="71118-420">请注意，链接正确显示。</span><span class="sxs-lookup"><span data-stu-id="71118-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="71118-421">![与右侧对齐的链接](using-page-inspector-in-visual-studio-2012/_static/image44.png "与右侧对齐的链接")</span><span class="sxs-lookup"><span data-stu-id="71118-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="71118-422">*与右侧对齐的链接*</span><span class="sxs-lookup"><span data-stu-id="71118-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="71118-423">最后，您将更改标题标题。</span><span class="sxs-lookup"><span data-stu-id="71118-423">Finally, you will change the header title.</span></span> <span data-ttu-id="71118-424">请使用检查模式来单击文本，然后转到生成代码的源代码，而不是在所有文件中搜索 "**您的徽标"** 。</span><span class="sxs-lookup"><span data-stu-id="71118-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="71118-425">![查找站点标题](using-page-inspector-in-visual-studio-2012/_static/image45.png "查找站点标题")</span><span class="sxs-lookup"><span data-stu-id="71118-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="71118-426">*查找站点标题*</span><span class="sxs-lookup"><span data-stu-id="71118-426">*Finding the site title*</span></span>
10. <span data-ttu-id="71118-427">现在你位于 "**网站**" 中，用 "**照片库**" 替换 "**你的徽标**" 文本。</span><span class="sxs-lookup"><span data-stu-id="71118-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="71118-428">保存并更新 Page Inspector 浏览器。</span><span class="sxs-lookup"><span data-stu-id="71118-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="71118-429">![照片库页面已更新](using-page-inspector-in-visual-studio-2012/_static/image46.png "照片库页面已更新")</span><span class="sxs-lookup"><span data-stu-id="71118-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="71118-430">*照片库页面已更新*</span><span class="sxs-lookup"><span data-stu-id="71118-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="71118-431">最后，按**F5**运行应用程序。签出所有更改都按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="71118-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="71118-432">摘要</span><span class="sxs-lookup"><span data-stu-id="71118-432">Summary</span></span>

<span data-ttu-id="71118-433">完成此动手实验后，就可以了解到如何使用 Page Inspector 预览 Web 应用程序，而无需在浏览器中重新生成并运行该网站。</span><span class="sxs-lookup"><span data-stu-id="71118-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="71118-434">此外，还了解到了如何通过直接从呈现的输出访问源代码来快速查找和修复 bug。</span><span class="sxs-lookup"><span data-stu-id="71118-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="71118-435">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="71118-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="71118-436">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="71118-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="71118-437">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="71118-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="71118-438">请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="71118-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="71118-439">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="71118-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="71118-440">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="71118-440">Click on **Install Now**.</span></span> <span data-ttu-id="71118-441">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="71118-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="71118-442">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="71118-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="71118-443">![安装 Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="71118-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="71118-444">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="71118-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="71118-445">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="71118-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="71118-447">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="71118-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="71118-448">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="71118-448">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="71118-450">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="71118-450">*Installation progress*</span></span>
6. <span data-ttu-id="71118-451">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="71118-451">When the installation completes, click **Finish**.</span></span>

    ![安装完成](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="71118-453">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="71118-453">*Installation completed*</span></span>
7. <span data-ttu-id="71118-454">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="71118-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="71118-455">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="71118-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="71118-457">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="71118-457">*VS Express for Web tile*</span></span>
