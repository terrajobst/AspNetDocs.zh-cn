---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 中的新增功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 是一个框架，用于生成可缩放的基于标准的 web 应用程序，该应用程序使用良好构建的设计模式以及 ASP.NET 和 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057033"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="9a745-103">ASP.NET MVC 4 的新增功能</span><span class="sxs-lookup"><span data-stu-id="9a745-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="9a745-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="9a745-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="9a745-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="9a745-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="9a745-106">ASP.NET MVC 4 是一个框架，用于生成可缩放的基于标准的 web 应用程序，该应用程序使用良好构建的设计模式以及 ASP.NET 和 .NET framework 的强大功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="9a745-107">这一新的第四个版本的框架侧重于使移动 web 应用程序的开发变得更简单。</span><span class="sxs-lookup"><span data-stu-id="9a745-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="9a745-108">首先，当你创建新的 ASP.NET MVC 4 项目时，现在可以使用一个移动应用程序项目模板来构建专用于移动设备的独立应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="9a745-109">此外，ASP.NET MVC 4 还通过 jQuery NuGet 包与 jQuery Mobile 集成。</span><span class="sxs-lookup"><span data-stu-id="9a745-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="9a745-110">jQuery Mobile 是一个基于 HTML5 的框架，用于开发与所有常用移动设备平台（包括 Windows Phone、iPhone、Android 等）兼容的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9a745-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="9a745-111">但是，如果你需要特殊化，ASP.NET MVC 4 还可以为不同的设备提供不同的视图，并提供特定于设备的优化。</span><span class="sxs-lookup"><span data-stu-id="9a745-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="9a745-112">在此动手实验中，你将从 ASP.NET MVC 4 &quot;Internet 应用程序&quot; 项目模板开始，以创建照片库应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="9a745-113">你将使用 jQuery Mobile 和 ASP.NET MVC 4 的新功能逐步提高应用，使其与不同的移动设备和桌面 web 浏览器兼容。</span><span class="sxs-lookup"><span data-stu-id="9a745-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="9a745-114">你还将了解用于代码生成的新代码食谱，以及 ASP.NET MVC 4 如何通过支持 Task&lt;ActionResult&gt; 返回类型来更轻松地编写异步操作方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="9a745-115">所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。</span><span class="sxs-lookup"><span data-stu-id="9a745-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="9a745-116">[ASP.NET 4.5 中 Web 窗体的新增功能中](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)提供了此实验室特定的项目。</span><span class="sxs-lookup"><span data-stu-id="9a745-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="9a745-117">目标</span><span class="sxs-lookup"><span data-stu-id="9a745-117">Objectives</span></span>

<span data-ttu-id="9a745-118">在此动手实验中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="9a745-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="9a745-119">充分利用 ASP.NET MVC 项目模板的增强功能，包括新的移动应用程序项目模板</span><span class="sxs-lookup"><span data-stu-id="9a745-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="9a745-120">使用 HTML5 视区属性和 CSS 媒体查询改善移动设备上的显示</span><span class="sxs-lookup"><span data-stu-id="9a745-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="9a745-121">使用 jQuery Mobile 进行渐进式增强，并构建触摸优化 web UI</span><span class="sxs-lookup"><span data-stu-id="9a745-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="9a745-122">创建特定于移动设备的视图</span><span class="sxs-lookup"><span data-stu-id="9a745-122">Create mobile-specific views</span></span>
- <span data-ttu-id="9a745-123">使用视图切换器组件在应用程序的移动视图与桌面视图之间切换</span><span class="sxs-lookup"><span data-stu-id="9a745-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="9a745-124">使用任务支持创建异步控制器</span><span class="sxs-lookup"><span data-stu-id="9a745-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="9a745-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9a745-125">Prerequisites</span></span>

<span data-ttu-id="9a745-126">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="9a745-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="9a745-127">[适用于 Web 或高级的 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （有关如何安装的说明，请参阅[附录 B](#AppendixB) ）。</span><span class="sxs-lookup"><span data-stu-id="9a745-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="9a745-128">[ASP.NET MVC 4](../../../mvc4.md) （包含在 Microsoft Visual Studio 2012 安装中）</span><span class="sxs-lookup"><span data-stu-id="9a745-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="9a745-129">Windows Phone 模拟器（包括在[Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)中）</span><span class="sxs-lookup"><span data-stu-id="9a745-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="9a745-130">可选-附带**电气 Plum IPhone 模拟器**扩展的[WebMatrix 2](https://www.microsoft.com/web/webmatrix/) （仅适用于使用 iPhone 模拟器浏览 Web 应用程序的练习3）</span><span class="sxs-lookup"><span data-stu-id="9a745-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="9a745-131">安装</span><span class="sxs-lookup"><span data-stu-id="9a745-131">Setup</span></span>

<span data-ttu-id="9a745-132">在整个实验室文档中，系统会指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="9a745-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="9a745-133">为方便起见，其中的大多数代码都作为 Visual Studio Code 代码段提供，你可以在 Visual Studio 中使用这些代码段，以避免手动添加它。</span><span class="sxs-lookup"><span data-stu-id="9a745-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="9a745-134">安装代码片段：</span><span class="sxs-lookup"><span data-stu-id="9a745-134">To install the code snippets:</span></span>

1. <span data-ttu-id="9a745-135">打开 Windows 资源管理器窗口并浏览到实验室的**Source\Setup**文件夹。</span><span class="sxs-lookup"><span data-stu-id="9a745-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="9a745-136">双击此文件夹中的**Setup .cmd**文件以安装 Visual Studio code 代码段。</span><span class="sxs-lookup"><span data-stu-id="9a745-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="9a745-137">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[A &quot;附录 A：使用代码段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="9a745-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="9a745-138">练习</span><span class="sxs-lookup"><span data-stu-id="9a745-138">Exercises</span></span>

<span data-ttu-id="9a745-139">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="9a745-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="9a745-140">New ASP.NET MVC 4 项目模板</span><span class="sxs-lookup"><span data-stu-id="9a745-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="9a745-141">创建照片库 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="9a745-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="9a745-142">添加对移动设备的支持</span><span class="sxs-lookup"><span data-stu-id="9a745-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="9a745-143">使用异步控制器</span><span class="sxs-lookup"><span data-stu-id="9a745-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="9a745-144">每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="9a745-145">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="9a745-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="9a745-146">完成本实验的估计时间： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="9a745-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="9a745-147">练习1： New ASP.NET MVC 4 项目模板</span><span class="sxs-lookup"><span data-stu-id="9a745-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="9a745-148">在此练习中，你将了解 ASP.NET MVC 4 项目模板中的增强功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="9a745-149">除了 Internet 应用程序模板外，在 MVC 3 中，此版本现在包含用于移动应用程序的单独模板。</span><span class="sxs-lookup"><span data-stu-id="9a745-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="9a745-150">首先，您将了解每个模板的一些相关功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="9a745-151">然后，使用正确的方法在不同的平台上正确呈现页面。</span><span class="sxs-lookup"><span data-stu-id="9a745-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="9a745-152">任务 1-浏览 Internet 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="9a745-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="9a745-153">打开**Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="9a745-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="9a745-154">选择**文件 |新建 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="9a745-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="9a745-155">在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序 "。**</span><span class="sxs-lookup"><span data-stu-id="9a745-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="9a745-156">将项目命名为**PhotoGallery**，选择一个位置（或保留默认值），然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-157">稍后将自定义要创建的 PhotoGallery ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="9a745-158">![创建新项目](whats-new-in-aspnet-mvc-4/_static/image1.png "创建新项目")</span><span class="sxs-lookup"><span data-stu-id="9a745-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="9a745-159">*创建新项目*</span><span class="sxs-lookup"><span data-stu-id="9a745-159">*Creating a new project*</span></span>
3. <span data-ttu-id="9a745-160">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**" 项目模板，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="9a745-161">请确保已选择 Razor 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9a745-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="9a745-162">![创建新的 ASP.NET MVC 4 Internet 应用程序](whats-new-in-aspnet-mvc-4/_static/image2.png "创建新的 ASP.NET MVC 4 Internet 应用程序")</span><span class="sxs-lookup"><span data-stu-id="9a745-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="9a745-163">*创建新的 ASP.NET MVC 4 Internet 应用程序*</span><span class="sxs-lookup"><span data-stu-id="9a745-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-164">ASP.NET MVC 3 中引入了 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="9a745-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="9a745-165">其目标是最大程度地减少文件中所需的字符和击键数量，从而实现快速、流畅的编码工作流。</span><span class="sxs-lookup"><span data-stu-id="9a745-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="9a745-166">Razor 利用了C#现有/VB （或其他）语言技能，并提供了一个模板标记语法，可实现出色的 HTML 构造工作流。</span><span class="sxs-lookup"><span data-stu-id="9a745-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="9a745-167">按**F5**运行解决方案并查看续订的模板。</span><span class="sxs-lookup"><span data-stu-id="9a745-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="9a745-168">您可以查看以下功能：</span><span class="sxs-lookup"><span data-stu-id="9a745-168">You can check out the following features:</span></span>

    <span data-ttu-id="9a745-169">**新式模板**</span><span class="sxs-lookup"><span data-stu-id="9a745-169">**Modern-style templates**</span></span>

    <span data-ttu-id="9a745-170">这些模板已续订，提供了更新式的样式。</span><span class="sxs-lookup"><span data-stu-id="9a745-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="9a745-171">![ASP.NET MVC 4 改变模板](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 改变模板")</span><span class="sxs-lookup"><span data-stu-id="9a745-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="9a745-172">*ASP.NET MVC 4 改变模板*</span><span class="sxs-lookup"><span data-stu-id="9a745-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="9a745-173">![新建联系人页](whats-new-in-aspnet-mvc-4/_static/image4.png "新建联系人页")</span><span class="sxs-lookup"><span data-stu-id="9a745-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="9a745-174">*新建联系人页*</span><span class="sxs-lookup"><span data-stu-id="9a745-174">*New Contact page*</span></span>

    <span data-ttu-id="9a745-175">**自适应呈现**</span><span class="sxs-lookup"><span data-stu-id="9a745-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="9a745-176">查看调整浏览器窗口的大小，并注意页面布局如何动态适应新的窗口大小。</span><span class="sxs-lookup"><span data-stu-id="9a745-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="9a745-177">这些模板使用自适应呈现技术在桌面和移动平台中正确呈现，无需进行任何自定义。</span><span class="sxs-lookup"><span data-stu-id="9a745-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="9a745-178">![不同浏览器大小的 ASP.NET MVC 4 项目模板](whats-new-in-aspnet-mvc-4/_static/image5.png "不同浏览器大小的 ASP.NET MVC 4 项目模板")</span><span class="sxs-lookup"><span data-stu-id="9a745-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="9a745-179">*不同浏览器大小的 ASP.NET MVC 4 项目模板*</span><span class="sxs-lookup"><span data-stu-id="9a745-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="9a745-180">**JavaScript 更丰富的 UI**</span><span class="sxs-lookup"><span data-stu-id="9a745-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="9a745-181">默认项目模板的另一增强功能是使用 JavaScript 提供更具交互性的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="9a745-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="9a745-182">在模板中使用的登录名和寄存器链接求知欲了如何使用 jQuery 验证来验证客户端的输入字段。</span><span class="sxs-lookup"><span data-stu-id="9a745-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 验证](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="9a745-184">*jQuery 验证*</span><span class="sxs-lookup"><span data-stu-id="9a745-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-185">请注意两个登录部分，在第一部分中，你可以使用站点中的注册帐户登录，也可以使用其他身份验证服务（例如，默认情况下禁用）登录。</span><span class="sxs-lookup"><span data-stu-id="9a745-185">Notice the two log in sections, in the first section you can log in using a registered account from the site and in the second section you can alternatively log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="9a745-186">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9a745-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="9a745-187">打开位于**应用\_Start**文件夹下的文件**AuthConfig.cs** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="9a745-188">删除最后一行中的注释，为*OAuth*身份验证注册 Google 客户端。</span><span class="sxs-lookup"><span data-stu-id="9a745-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="9a745-189">请注意，可以使用任何 OpenID 或 OAuth 服务（如 Facebook、Twitter、Microsoft 等）轻松启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="9a745-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="9a745-190">按**F5**运行解决方案，然后导航到登录页。</span><span class="sxs-lookup"><span data-stu-id="9a745-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="9a745-191">选择 " **Google**服务" 以登录。</span><span class="sxs-lookup"><span data-stu-id="9a745-191">Select **Google** service to log in.</span></span>

    ![选择登录服务](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="9a745-193">*选择登录服务*</span><span class="sxs-lookup"><span data-stu-id="9a745-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="9a745-194">使用 Google 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9a745-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="9a745-195">允许站点（localhost）从 Google 帐户中检索信息。</span><span class="sxs-lookup"><span data-stu-id="9a745-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="9a745-196">最后，你必须在站点中注册以关联 Google 帐户。</span><span class="sxs-lookup"><span data-stu-id="9a745-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![关联 Google 帐户](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="9a745-198">*关联 Google 帐户*</span><span class="sxs-lookup"><span data-stu-id="9a745-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="9a745-199">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9a745-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="9a745-200">现在，浏览解决方案，查看项目模板中的 ASP.NET MVC 4 引入的一些其他新功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="9a745-201">![ASP.NET MVC 4 Internet 应用程序项目模板](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet 应用程序项目模板")</span><span class="sxs-lookup"><span data-stu-id="9a745-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="9a745-202">*ASP.NET MVC 4 Internet 应用程序项目模板*</span><span class="sxs-lookup"><span data-stu-id="9a745-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="9a745-203">**HTML 5 标记**</span><span class="sxs-lookup"><span data-stu-id="9a745-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="9a745-204">浏览模板视图以找出新的主题标记。</span><span class="sxs-lookup"><span data-stu-id="9a745-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="9a745-205">![新模板，使用 Razor 和 HTML5 标记关于 cshtml。](whats-new-in-aspnet-mvc-4/_static/image10.png "新模板，使用 Razor 和 HTML5 标记关于 cshtml。")</span><span class="sxs-lookup"><span data-stu-id="9a745-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="9a745-206">*新模板，使用 Razor 和 HTML5 标记（关于 cshtml）。*</span><span class="sxs-lookup"><span data-stu-id="9a745-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="9a745-207">**更新的 JavaScript 库**</span><span class="sxs-lookup"><span data-stu-id="9a745-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="9a745-208">ASP.NET MVC 4 默认模板现在包括 KnockoutJS，这是一个 JavaScript MVVM 框架，可让你使用 JavaScript 和 HTML 创建丰富且响应迅速的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="9a745-209">与在 MVC3 中一样，jQuery 和 jQuery UI 库也包含在 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="9a745-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9a745-210">可在以下链接中获取有关 KnockOutJS 库的详细信息： [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="9a745-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="9a745-211">此外，还可以了解[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中的 jQuery 和 jquery UI。</span><span class="sxs-lookup"><span data-stu-id="9a745-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="9a745-212">任务 2-浏览移动应用程序模板</span><span class="sxs-lookup"><span data-stu-id="9a745-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="9a745-213">ASP.NET MVC 4 简化了移动和平板浏览器的网站开发。</span><span class="sxs-lookup"><span data-stu-id="9a745-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="9a745-214">此模板的应用程序结构与 Internet 应用程序模板相同（请注意，控制器代码几乎完全相同），但其样式已修改为在基于触摸的移动设备中正确呈现。</span><span class="sxs-lookup"><span data-stu-id="9a745-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="9a745-215">选择**文件 |新建 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="9a745-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="9a745-216">在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序 "。**</span><span class="sxs-lookup"><span data-stu-id="9a745-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="9a745-217">将项目命名为**PhotoGallery**，选择一个位置（或保留默认值），选择 &quot;添加到解决方案&quot; 并单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="9a745-218">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 "**移动应用程序**" 项目模板，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="9a745-219">请确保已选择 Razor 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9a745-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="9a745-220">![创建新的 ASP.NET MVC 4 移动应用程序](whats-new-in-aspnet-mvc-4/_static/image11.png "创建新的 ASP.NET MVC 4 移动应用程序")</span><span class="sxs-lookup"><span data-stu-id="9a745-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="9a745-221">*创建新的 ASP.NET MVC 4 移动应用程序*</span><span class="sxs-lookup"><span data-stu-id="9a745-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="9a745-222">现在，你可以浏览解决方案并查看适用于 mobile 的 ASP.NET MVC 4 解决方案模板引入的一些新功能：</span><span class="sxs-lookup"><span data-stu-id="9a745-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="9a745-223">**jQuery Mobile 库**</span><span class="sxs-lookup"><span data-stu-id="9a745-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="9a745-224">"移动应用程序" 项目模板包含 jQuery Mobile 库，这是用于移动浏览器兼容性的开源库。</span><span class="sxs-lookup"><span data-stu-id="9a745-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="9a745-225">jQuery Mobile 可对支持 CSS 和 JavaScript 的移动浏览器应用渐进增强。</span><span class="sxs-lookup"><span data-stu-id="9a745-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="9a745-226">渐进式增强功能允许所有浏览器显示网页的基本内容，而仅允许最强大的浏览器显示丰富的内容。</span><span class="sxs-lookup"><span data-stu-id="9a745-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="9a745-227">JQuery Mobile style 中包含的 JavaScript 和 CSS 文件可帮助移动浏览器适应屏幕内容，而无需在页面标记中进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-包含模板中的](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="9a745-229">*模板中包含的 jQuery mobile 库*</span><span class="sxs-lookup"><span data-stu-id="9a745-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="9a745-230">**基于 HTML5 的标记**</span><span class="sxs-lookup"><span data-stu-id="9a745-230">**HTML5 based markup**</span></span>

        ![移动应用程序-使用-HTML5-标记](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="9a745-232">*使用 HTML5 标记的移动应用程序模板（登录名和索引. cshtml）*</span><span class="sxs-lookup"><span data-stu-id="9a745-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="9a745-233">按**F5**运行解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="9a745-234">打开**Windows Phone 7 模拟器**。</span><span class="sxs-lookup"><span data-stu-id="9a745-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="9a745-235">在手机的 "开始" 屏幕上，打开 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="9a745-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="9a745-236">查看桌面应用程序的启动 URL，并从手机浏览到该 URL （例如 `http://localhost:[PortNumber]/`）。</span><span class="sxs-lookup"><span data-stu-id="9a745-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="9a745-237">现在，你可以输入登录页面或查看 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="9a745-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="9a745-238">请注意，网站的样式基于适用于移动设备的新地铁应用。</span><span class="sxs-lookup"><span data-stu-id="9a745-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="9a745-239">ASP.NET MVC 4 项目模板已正确显示在移动设备上，请确保页面的所有元素都可见且已启用。</span><span class="sxs-lookup"><span data-stu-id="9a745-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="9a745-240">请注意，标题上的链接足够大，可以单击或点击。</span><span class="sxs-lookup"><span data-stu-id="9a745-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="9a745-241">![移动设备中的项目模板页](whats-new-in-aspnet-mvc-4/_static/image14.png "移动设备中的项目模板页")</span><span class="sxs-lookup"><span data-stu-id="9a745-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="9a745-242">*移动设备中的项目模板页*</span><span class="sxs-lookup"><span data-stu-id="9a745-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="9a745-243">新模板还使用**视区 meta 标记**。</span><span class="sxs-lookup"><span data-stu-id="9a745-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="9a745-244">大多数移动浏览器定义虚拟浏览器窗口或 &quot;视区的宽度&quot;，该值大于移动设备的实际宽度。</span><span class="sxs-lookup"><span data-stu-id="9a745-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="9a745-245">这使移动浏览器能够在虚拟显示内显示整个网页。</span><span class="sxs-lookup"><span data-stu-id="9a745-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="9a745-246">利用**视区 meta 标记**，web 开发人员可以设置移动设备上浏览器区域的宽度、高度和比例 **。**</span><span class="sxs-lookup"><span data-stu-id="9a745-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="9a745-247">适用于移动应用程序的 ASP.NET MVC 4 模板在布局模板（*Views\Shared\_layout*）中将视区设置为设备宽度（&quot;width = 设备宽度&quot;），以便所有页面都将其视区设置为设备屏幕宽度。</span><span class="sxs-lookup"><span data-stu-id="9a745-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="9a745-248">请注意，视区 meta 标记将不会更改默认浏览器视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="9a745-249">打开位于 "视图" 中 **\_布局 ...** **共享**文件夹，并注释视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="9a745-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="9a745-250">运行应用程序（如果尚未打开），并查看不同之处。</span><span class="sxs-lookup"><span data-stu-id="9a745-250">Run the application, if not already opened, and check out the differences.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="9a745-251">![注释视区 meta 标记后的站点](whats-new-in-aspnet-mvc-4/_static/image15.png "注释视区 meta 标记后的站点")</span><span class="sxs-lookup"><span data-stu-id="9a745-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="9a745-252">*注释视区 meta 标记后的站点*</span><span class="sxs-lookup"><span data-stu-id="9a745-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="9a745-253">在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="9a745-254">取消注释视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="9a745-254">Uncomment the viewport meta tag.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="9a745-255">任务 3-使用自适应呈现</span><span class="sxs-lookup"><span data-stu-id="9a745-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="9a745-256">在此任务中，你将学习在不进行任何自定义的情况下，在移动设备和 Web 浏览器上正确呈现网页的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="9a745-257">您已经使用了类似用途的视区 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="9a745-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="9a745-258">现在，您将满足另一个功能强大的方法：*自适应呈现*。</span><span class="sxs-lookup"><span data-stu-id="9a745-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="9a745-259">自适应呈现是一种技术，使用**CSS3 媒体查询**自定义应用于页面的样式。</span><span class="sxs-lookup"><span data-stu-id="9a745-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="9a745-260">媒体查询定义样式表中的条件，在特定条件下对 CSS 样式进行分组。</span><span class="sxs-lookup"><span data-stu-id="9a745-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="9a745-261">仅当条件为 true 时，才将样式应用于已声明的对象。</span><span class="sxs-lookup"><span data-stu-id="9a745-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="9a745-262">自适应呈现技术提供的灵活性使您能够在不同设备上显示网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="9a745-263">您可以在单个样式表中定义任意数量的样式，而无需编写逻辑代码来选择样式。</span><span class="sxs-lookup"><span data-stu-id="9a745-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="9a745-264">因此，它是一种非常巧妙的页面样式调整方法，因为它减少了用于呈现的代码和逻辑的数量。</span><span class="sxs-lookup"><span data-stu-id="9a745-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="9a745-265">另一方面，带宽消耗会增加，因为 CSS 文件的大小可能会略微增长。</span><span class="sxs-lookup"><span data-stu-id="9a745-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="9a745-266">通过使用自适应呈现技术，你的网站将**正常显示，而与浏览器无关。**</span><span class="sxs-lookup"><span data-stu-id="9a745-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="9a745-267">但是，您应该考虑是否需要考虑带宽额外负载。</span><span class="sxs-lookup"><span data-stu-id="9a745-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="9a745-268">媒体查询的基本格式为： @media \[范围： all |手持式 |打印 |投影 |屏幕\] （[属性：值] 和 。[属性：值]）</span><span class="sxs-lookup"><span data-stu-id="9a745-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>

<span data-ttu-id="9a745-269">媒体查询示例： &gt; **@media all 和（最大宽度：1000px）和（最小宽度：700px） {}：** 700px 和1000px 之间的所有解决方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-269">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="9a745-270">**@media 屏幕和（最小宽度：400px）和（最大宽度：700px） {...}：** 仅适用于屏幕。</span><span class="sxs-lookup"><span data-stu-id="9a745-270">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="9a745-271">分辨率必须介于400和700px 之间。</span><span class="sxs-lookup"><span data-stu-id="9a745-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="9a745-272">**@media 手持型和（最小宽度：20em）、屏幕和（最小宽度：20em） {...}：** 对于手持设备（移动设备和设备）和屏幕。</span><span class="sxs-lookup"><span data-stu-id="9a745-272">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="9a745-273">最小宽度必须大于20em。</span><span class="sxs-lookup"><span data-stu-id="9a745-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="9a745-274">可以在[W3C 网站](http://www.w3.org/TR/css3-mediaqueries/)上找到有关此内容的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9a745-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>

<span data-ttu-id="9a745-275">现在，你将浏览自适应呈现的工作原理，提高 ASP.NET MVC 4 默认网站模板的可读性。</span><span class="sxs-lookup"><span data-stu-id="9a745-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="9a745-276">打开你在任务1创建的**PhotoGallery**解决方案，然后选择 " **PhotoGallery** " 项目。</span><span class="sxs-lookup"><span data-stu-id="9a745-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="9a745-277">按**F5**运行解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="9a745-278">调整浏览器的宽度，将窗口设置为半或小于其原始大小的四分之一。</span><span class="sxs-lookup"><span data-stu-id="9a745-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="9a745-279">请注意标题中的项会发生什么情况：某些元素将不会显示在标头的可见区域中。</span><span class="sxs-lookup"><span data-stu-id="9a745-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="9a745-280">从 Visual Studio 解决方案资源管理器中打开位于**内容**项目文件夹中的**web.config**文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-280">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="9a745-281">按**CTRL + F**打开 Visual Studio 集成搜索，并编写 `@media` 以查找**CSS 媒体查询**。</span><span class="sxs-lookup"><span data-stu-id="9a745-281">Press **CTRL + F** to open Visual Studio integrated search, and write `@media` to locate the **CSS media query**.</span></span>

    <span data-ttu-id="9a745-282">此模板中定义的媒体查询条件的工作方式如下：当浏览器的窗口大小低于**850 像素**时，应用的 CSS 规则是此媒体块中定义的规则。</span><span class="sxs-lookup"><span data-stu-id="9a745-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="9a745-283">![查找媒体查询](whats-new-in-aspnet-mvc-4/_static/image16.png "查找媒体查询")</span><span class="sxs-lookup"><span data-stu-id="9a745-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="9a745-284">*查找媒体查询*</span><span class="sxs-lookup"><span data-stu-id="9a745-284">*Locating the media query*</span></span>
4. <span data-ttu-id="9a745-285">将 850 px 中设置的最大宽度属性值替换为**10px**，以便禁用自适应呈现，并按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="9a745-286">返回到浏览器，并按**CTRL + F5**以使用您所做的更改刷新页面。</span><span class="sxs-lookup"><span data-stu-id="9a745-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="9a745-287">请注意，在调整窗口的宽度时，两个页面之间的差异。</span><span class="sxs-lookup"><span data-stu-id="9a745-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="9a745-288">![在左侧，页面正在应用 @media 样式，则省略样式](whats-new-in-aspnet-mvc-4/_static/image17.png "在左侧，页面正在应用 @media 样式，则省略样式")</span><span class="sxs-lookup"><span data-stu-id="9a745-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="9a745-289">*在左侧，页面正在应用 @media 样式，则省略样式*</span><span class="sxs-lookup"><span data-stu-id="9a745-289">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="9a745-290">现在，我们来看看移动设备上发生的情况：</span><span class="sxs-lookup"><span data-stu-id="9a745-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="9a745-291">![在左侧，页面正在应用 @media 样式，则省略样式](whats-new-in-aspnet-mvc-4/_static/image18.png "在左侧，页面正在应用 @media 样式，则省略样式")</span><span class="sxs-lookup"><span data-stu-id="9a745-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="9a745-292">*在左侧，页面正在应用 @media 样式，则省略样式*</span><span class="sxs-lookup"><span data-stu-id="9a745-292">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="9a745-293">尽管你会注意到，在 Web 浏览器中呈现页面时所做的更改并不重要，但在使用移动设备时，差别会变得更加明显。</span><span class="sxs-lookup"><span data-stu-id="9a745-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="9a745-294">在图像的左侧，可以看到自定义样式提高了可读性。</span><span class="sxs-lookup"><span data-stu-id="9a745-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="9a745-295">自适应呈现可用于更多方案，使您可以更轻松地将条件样式应用于网站并使用巧妙的方法解决常见的样式问题。</span><span class="sxs-lookup"><span data-stu-id="9a745-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="9a745-296">视区 meta 标记和 CSS 媒体查询并不特定于 ASP.NET MVC 4，因此你可以在任何 web 应用程序中利用这些功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="9a745-297">在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="9a745-298">练习2：创建照片库 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="9a745-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="9a745-299">在此练习中，您将使用照片库应用程序来显示照片。</span><span class="sxs-lookup"><span data-stu-id="9a745-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="9a745-300">你将从 ASP.NET MVC 4 项目模板开始，然后添加功能以从服务中检索照片，并将其显示在主页中。</span><span class="sxs-lookup"><span data-stu-id="9a745-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="9a745-301">在以下练习中，你将更新此解决方案以增强它在移动设备上的显示方式。</span><span class="sxs-lookup"><span data-stu-id="9a745-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="9a745-302">任务 1-创建模拟照片服务</span><span class="sxs-lookup"><span data-stu-id="9a745-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="9a745-303">在此任务中，您将创建照片服务的模拟，以检索将在库中显示的内容。</span><span class="sxs-lookup"><span data-stu-id="9a745-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="9a745-304">为此，您将添加一个新的控制器，它将只返回包含每张照片数据的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="9a745-305">如果尚未打开，请打开**Visual Studio** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="9a745-306">选择**文件 |新建 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="9a745-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="9a745-307">在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序 "。**</span><span class="sxs-lookup"><span data-stu-id="9a745-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="9a745-308">将项目命名为**PhotoGallery**，选择一个位置（或保留默认值），然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="9a745-309">或者，你可以从**练习 1**中的现有 ASP.NET MVC 4 **Internet 应用程序**解决方案继续工作，并跳过下一步。</span><span class="sxs-lookup"><span data-stu-id="9a745-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="9a745-310">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**" 项目模板，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="9a745-311">请确保选择 "Razor" 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9a745-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="9a745-312">在**解决方案资源管理器**中，右键单击项目 **\_"数据**" 文件夹中的 "应用"，然后选择 "**添加 |现有项**。</span><span class="sxs-lookup"><span data-stu-id="9a745-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="9a745-313">浏览到此实验室的**Source\Assets\App\_Data**文件夹，并**添加文件。**</span><span class="sxs-lookup"><span data-stu-id="9a745-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="9a745-314">创建名为**PhotoController**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="9a745-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="9a745-315">为此，请右键单击 "**控制器**" 文件夹，然后单击 "**添加**"，然后选择 "**控制器"。**</span><span class="sxs-lookup"><span data-stu-id="9a745-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="9a745-316">填写控制器名称，保留**空 MVC 控制器**模板并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="9a745-317">![添加 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "添加 PhotoController")</span><span class="sxs-lookup"><span data-stu-id="9a745-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="9a745-318">*添加 PhotoController*</span><span class="sxs-lookup"><span data-stu-id="9a745-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="9a745-319">将**Index**方法替换为以下**库**操作，并返回最近添加到项目的 JSON 文件中的内容。</span><span class="sxs-lookup"><span data-stu-id="9a745-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="9a745-320">（代码段- *ASP.NET MVC 4 实验室-Ex02 操作*）</span><span class="sxs-lookup"><span data-stu-id="9a745-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="9a745-321">按**F5**运行解决方案，然后浏览到以下 URL，以便测试模拟 photo service： `http://localhost:[port]/photo/gallery` （[端口] 值取决于启动应用程序的当前端口）。</span><span class="sxs-lookup"><span data-stu-id="9a745-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="9a745-322">对此 URL 的请求应检索**照片 json**文件的内容。</span><span class="sxs-lookup"><span data-stu-id="9a745-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="9a745-323">![测试模拟照片服务](whats-new-in-aspnet-mvc-4/_static/image20.png "测试模拟照片服务")</span><span class="sxs-lookup"><span data-stu-id="9a745-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="9a745-324">*测试模拟照片服务*</span><span class="sxs-lookup"><span data-stu-id="9a745-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="9a745-325">在实际实现中，可以使用[ASP.NET Web API](../../../../web-api/index.md)来实现照片库服务。</span><span class="sxs-lookup"><span data-stu-id="9a745-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="9a745-326">ASP.NET Web API 是一种框架，可让你轻松地生成可访问范围广泛的客户端（包括浏览器和移动设备）的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="9a745-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="9a745-327">ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。</span><span class="sxs-lookup"><span data-stu-id="9a745-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="9a745-328">任务 2-显示照片库</span><span class="sxs-lookup"><span data-stu-id="9a745-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="9a745-329">在此任务中，您将使用在本练习的第一个任务中创建的模拟服务来更新主页以显示照片库。</span><span class="sxs-lookup"><span data-stu-id="9a745-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="9a745-330">您将添加模型文件并更新库视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="9a745-331">在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="9a745-332">在 "**模型**" 文件夹中创建**Photo**类。</span><span class="sxs-lookup"><span data-stu-id="9a745-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="9a745-333">为此，请右键单击 "**模型**" 文件夹，选择 "**添加**"，然后单击 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="9a745-334">然后，将名称设置为**Photo.cs** ，并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="9a745-335">将以下成员添加到**Photo**类中。</span><span class="sxs-lookup"><span data-stu-id="9a745-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="9a745-336">（代码段- *ASP.NET MVC 4 实验室-Ex02*）</span><span class="sxs-lookup"><span data-stu-id="9a745-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="9a745-337">从“控制器”文件夹打开 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="9a745-338">添加下面的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="9a745-338">Add the following using statements.</span></span>

    <span data-ttu-id="9a745-339">（代码段- *ASP.NET MVC 4 Lab-Ex02-HomeController using*）</span><span class="sxs-lookup"><span data-stu-id="9a745-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="9a745-340">更新**索引**操作以使用**HttpClient**检索库数据，然后使用**JavaScriptSerializer**将其反序列化到视图模型。</span><span class="sxs-lookup"><span data-stu-id="9a745-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="9a745-341">（代码段- *ASP.NET MVC 4 Ex02-索引操作*）</span><span class="sxs-lookup"><span data-stu-id="9a745-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="9a745-342">打开位于 Views\Home 文件夹下的 **文件，** 并将所有内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="9a745-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="9a745-343">此代码循环访问从服务中检索到的所有照片，并将其显示为未排序列表。</span><span class="sxs-lookup"><span data-stu-id="9a745-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="9a745-344">（代码段- *ASP.NET MVC 4 Ex02-Photo List*）</span><span class="sxs-lookup"><span data-stu-id="9a745-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="9a745-345">在**解决方案资源管理器**中，右键单击项目的 "**内容**" 文件夹，然后选择 "**添加 |现有项**。</span><span class="sxs-lookup"><span data-stu-id="9a745-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="9a745-346">浏览到此实验室的**Source\Assets\Content**文件夹并添加**web.config 文件。**</span><span class="sxs-lookup"><span data-stu-id="9a745-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="9a745-347">需要确认它的替换。</span><span class="sxs-lookup"><span data-stu-id="9a745-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="9a745-348">如果已打开**web.config**文件，则还必须确认是否要重新加载文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="9a745-349">打开文件资源管理器，将位于此实验室的**Source\Assets**文件夹下的整个**照片**文件夹复制到解决方案资源管理器中项目的根文件夹下。</span><span class="sxs-lookup"><span data-stu-id="9a745-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="9a745-350">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-350">Run the application.</span></span> <span data-ttu-id="9a745-351">现在，你应看到在库中显示照片的主页。</span><span class="sxs-lookup"><span data-stu-id="9a745-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="9a745-352">![照片库](whats-new-in-aspnet-mvc-4/_static/image21.png "照片库")</span><span class="sxs-lookup"><span data-stu-id="9a745-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="9a745-353">*照片库*</span><span class="sxs-lookup"><span data-stu-id="9a745-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="9a745-354">在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="9a745-355">练习3：添加对移动设备的支持</span><span class="sxs-lookup"><span data-stu-id="9a745-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="9a745-356">ASP.NET MVC 4 中的一个重要更新是支持移动开发。</span><span class="sxs-lookup"><span data-stu-id="9a745-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="9a745-357">在此练习中，你将通过扩展你在上一练习中创建的 PhotoGallery 解决方案来浏览移动应用程序的 ASP.NET MVC 4 新功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="9a745-358">任务 1-在 ASP.NET MVC 4 应用程序中安装 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="9a745-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="9a745-359">打开位于**Source/section-cs-MobileSupport/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="9a745-360">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="9a745-361">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="9a745-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="9a745-362">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="9a745-363">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="9a745-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="9a745-364">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9a745-365">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="9a745-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="9a745-366">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="9a745-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="9a745-367">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="9a745-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="9a745-368">通过单击 " > **NuGet 包管理器** > **包管理器控制台**" 菜单选项中的 "**工具**" 打开**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="9a745-368">Open the **Package Manager Console** by clicking the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="9a745-369">![打开 NuGet 包管理器控制台](whats-new-in-aspnet-mvc-4/_static/image22.png "打开 NuGet 包管理器控制台")</span><span class="sxs-lookup"><span data-stu-id="9a745-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="9a745-370">*打开 NuGet 包管理器控制台*</span><span class="sxs-lookup"><span data-stu-id="9a745-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="9a745-371">在 "包管理器控制台" 中运行以下命令以安装**jQuery** . node.js 包。</span><span class="sxs-lookup"><span data-stu-id="9a745-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="9a745-372">jQuery Mobile 是用于构建触摸优化 web UI 的开源库。</span><span class="sxs-lookup"><span data-stu-id="9a745-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="9a745-373">JQuery. node.js NuGet 包包含用于将 jQuery Mobile 与 ASP.NET MVC 4 应用程序结合使用的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-374">通过运行以下命令，你将从 Nuget 下载 jQuery library。</span><span class="sxs-lookup"><span data-stu-id="9a745-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="9a745-375">PM</span><span class="sxs-lookup"><span data-stu-id="9a745-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="9a745-376">此命令安装 jQuery Mobile 和一些 helper 文件，包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="9a745-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="9a745-377">**Views/Shared/\_layout。** node.js：是一种针对小屏幕优化的基于 jQuery mobile 的布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="9a745-378">当网站收到来自移动浏览器的请求时，它会将原始布局（\_Layout）替换为此布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="9a745-379">视图切换器组件：由**Views/Shared/\_ViewSwitcher**分部视图和**ViewSwitcherController.cs**控制器组成。</span><span class="sxs-lookup"><span data-stu-id="9a745-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="9a745-380">此组件将在移动浏览器上显示一个链接，以使用户能够切换到页面的桌面版本。</span><span class="sxs-lookup"><span data-stu-id="9a745-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="9a745-381">![具有移动支持的照片库项目](whats-new-in-aspnet-mvc-4/_static/image23.png "Ph带有移动支持的照片库项目</span><span class="sxs-lookup"><span data-stu-id="9a745-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="9a745-382">*具有移动支持的照片库项目*</span><span class="sxs-lookup"><span data-stu-id="9a745-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="9a745-383">注册移动捆绑包。</span><span class="sxs-lookup"><span data-stu-id="9a745-383">Register the Mobile bundles.</span></span> <span data-ttu-id="9a745-384">为此，请打开**Global.asax.cs**文件并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="9a745-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="9a745-385">（代码段- *ASP.NET MVC 4 Ex03-注册移动包*）</span><span class="sxs-lookup"><span data-stu-id="9a745-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="9a745-386">使用桌面 web 浏览器运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="9a745-387">打开位于 "开始" 菜单中的**Windows Phone 7 仿真程序** **|所有程序 |Windows Phone SDK 7.1 |Windows Phone 模拟器。**</span><span class="sxs-lookup"><span data-stu-id="9a745-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="9a745-388">在手机的 "开始" 屏幕上，打开 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="9a745-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="9a745-389">查看应用程序启动的 URL，并通过手机浏览器（例如 `http://localhost:[PortNumber]/`）浏览到该 URL。</span><span class="sxs-lookup"><span data-stu-id="9a745-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="9a745-390">你会注意到，在 Windows Phone 模拟器中，你的应用程序的外观有所不同，因为 jQuery. node.js 在你的项目中创建了新资产，其中显示了为移动设备优化的视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="9a745-391">请注意手机顶部的消息，其中显示了切换到桌面视图的链接。</span><span class="sxs-lookup"><span data-stu-id="9a745-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="9a745-392">此外，在应用程序中安装的包所创建的 **\_布局.** node.js 布局也是如此。</span><span class="sxs-lookup"><span data-stu-id="9a745-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-393">到目前为止，没有可返回到移动视图的链接。</span><span class="sxs-lookup"><span data-stu-id="9a745-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="9a745-394">它将包含在更高版本中。</span><span class="sxs-lookup"><span data-stu-id="9a745-394">It will be included in later versions.</span></span>

    <span data-ttu-id="9a745-395">![照片库主页的移动视图](whats-new-in-aspnet-mvc-4/_static/image24.png "照片库主页的移动视图")</span><span class="sxs-lookup"><span data-stu-id="9a745-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="9a745-396">*照片库主页的移动视图*</span><span class="sxs-lookup"><span data-stu-id="9a745-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="9a745-397">在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="9a745-398">任务 2-创建移动视图</span><span class="sxs-lookup"><span data-stu-id="9a745-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="9a745-399">在此任务中，你将创建一个移动版本的索引视图，并将内容改编以便在移动设备中更好地显示。</span><span class="sxs-lookup"><span data-stu-id="9a745-399">In this task, you will create a mobile version of the index view with content adapted for better appearance in mobile devices.</span></span>

1. <span data-ttu-id="9a745-400">复制**Views\Home\Index.cshtml**视图并将其粘贴以创建副本，并将新文件重命名**为 "** "。</span><span class="sxs-lookup"><span data-stu-id="9a745-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="9a745-401">打开新创建的**索引.** node.js 视图，并将现有 &lt;ul&gt; 标记替换为此代码。</span><span class="sxs-lookup"><span data-stu-id="9a745-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="9a745-402">通过执行此操作，你将使用 jQuery Mobile 数据批注更新 &lt;ul&gt; 标记，以使用 jQuery 中的移动主题。</span><span class="sxs-lookup"><span data-stu-id="9a745-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="9a745-403">请注意：</span><span class="sxs-lookup"><span data-stu-id="9a745-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="9a745-404">设置为**listview**的**数据角色**属性将使用 listview 样式呈现列表。</span><span class="sxs-lookup"><span data-stu-id="9a745-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="9a745-405">"**数据嵌入**" 特性设置为 "true" 将显示具有圆角边框和边距的列表。</span><span class="sxs-lookup"><span data-stu-id="9a745-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="9a745-406">"**数据筛选器**" 属性设置为 " **true** " 将生成一个搜索框。</span><span class="sxs-lookup"><span data-stu-id="9a745-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="9a745-407">可以在项目文档中了解有关 jQuery Mobile 约定的详细信息： [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="9a745-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="9a745-408">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="9a745-409">切换到**Windows Phone 模拟器**并刷新站点。</span><span class="sxs-lookup"><span data-stu-id="9a745-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="9a745-410">请注意库列表的新外观和外观，以及顶部的新 "搜索" 框。</span><span class="sxs-lookup"><span data-stu-id="9a745-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="9a745-411">然后，在 "搜索" 框中键入一个词（例如， **Tulips**），在照片库中开始搜索。</span><span class="sxs-lookup"><span data-stu-id="9a745-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="9a745-412">![使用带有筛选功能的 listview 样式的库](whats-new-in-aspnet-mvc-4/_static/image25.png "使用带有筛选功能的 listview 样式的库")</span><span class="sxs-lookup"><span data-stu-id="9a745-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="9a745-413">*使用带有筛选功能的 listview 样式的库*</span><span class="sxs-lookup"><span data-stu-id="9a745-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="9a745-414">总而言之，已使用 View Mobilizer 食谱创建索引视图的副本，该副本具有 &quot;移动&quot; 后缀。</span><span class="sxs-lookup"><span data-stu-id="9a745-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="9a745-415">此后缀指示 ASP.NET MVC 4，每个从移动设备生成的请求都将使用此索引副本。</span><span class="sxs-lookup"><span data-stu-id="9a745-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="9a745-416">此外，还更新了索引视图的移动版本，使用 jQuery Mobile 增强了移动设备中的站点外观。</span><span class="sxs-lookup"><span data-stu-id="9a745-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="9a745-417">返回到**Content**文件夹下的 Visual Studio**并打开 "node.js"。**</span><span class="sxs-lookup"><span data-stu-id="9a745-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="9a745-418">修复照片标题的位置，使其显示在图像的右侧。</span><span class="sxs-lookup"><span data-stu-id="9a745-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="9a745-419">为此，请将以下代码添加到 node.js**文件中。**</span><span class="sxs-lookup"><span data-stu-id="9a745-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="9a745-420">CSS</span><span class="sxs-lookup"><span data-stu-id="9a745-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="9a745-421">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="9a745-422">切换回**Windows Phone 模拟器**并刷新站点。</span><span class="sxs-lookup"><span data-stu-id="9a745-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="9a745-423">请注意，照片标题现在正确定位。</span><span class="sxs-lookup"><span data-stu-id="9a745-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="9a745-424">![位于图像右侧的标题](whats-new-in-aspnet-mvc-4/_static/image26.png "位于图像右侧的标题")</span><span class="sxs-lookup"><span data-stu-id="9a745-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="9a745-425">*位于图像右侧的标题*</span><span class="sxs-lookup"><span data-stu-id="9a745-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="9a745-426">任务 3-jQuery Mobile Themes</span><span class="sxs-lookup"><span data-stu-id="9a745-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="9a745-427">JQuery Mobile 中的每个布局和小组件都围绕面向对象的新 CSS 框架设计，使你可以将完整的统一视觉对象设计主题应用到站点和应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="9a745-428">jQuery Mobile 的默认主题包括5个样本，其中包含字母（a、b、c、d、e），用于快速参考。</span><span class="sxs-lookup"><span data-stu-id="9a745-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="9a745-429">在此任务中，你将更新移动布局以使用不同于默认设置的主题。</span><span class="sxs-lookup"><span data-stu-id="9a745-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="9a745-430">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9a745-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="9a745-431">打开位于 Views\Shared 中的 **\_** 文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="9a745-432">查找数据角色设置为 &quot;页面&quot; 并将**数据主题**更新为 &quot;**e**&quot;的 div 元素。</span><span class="sxs-lookup"><span data-stu-id="9a745-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="9a745-433">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="9a745-434">刷新**Windows Phone 模拟器**中的站点，并注意新的颜色方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="9a745-435">![具有不同配色方案的移动版式](whats-new-in-aspnet-mvc-4/_static/image27.png "具有不同配色方案的移动版式")</span><span class="sxs-lookup"><span data-stu-id="9a745-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="9a745-436">*具有不同配色方案的移动版式*</span><span class="sxs-lookup"><span data-stu-id="9a745-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="9a745-437">任务 4-使用视图切换器组件和浏览器覆盖功能</span><span class="sxs-lookup"><span data-stu-id="9a745-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="9a745-438">移动优化的网页约定是添加一个链接，其文本的内容类似于桌面视图或完整站点模式，使用户能够切换到页面的桌面版本。</span><span class="sxs-lookup"><span data-stu-id="9a745-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="9a745-439">JQuery. node.js 包在 **\_Layout**视图中包含用于此目的的示例**视图切换**器组件。</span><span class="sxs-lookup"><span data-stu-id="9a745-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="9a745-440">![用于切换到桌面视图的链接](whats-new-in-aspnet-mvc-4/_static/image28.png "用于切换到桌面视图的链接")</span><span class="sxs-lookup"><span data-stu-id="9a745-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="9a745-441">*用于切换到桌面视图的链接*</span><span class="sxs-lookup"><span data-stu-id="9a745-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="9a745-442">视图切换器使用称为 "**浏览器重写**" 的新功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="9a745-443">此功能使应用程序可以处理请求，就好像这些请求来自于它们实际来自的浏览器（用户代理）。</span><span class="sxs-lookup"><span data-stu-id="9a745-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="9a745-444">在此任务中，你将了解 jQuery 所添加的视图切换器的示例实现，而新浏览器则覆盖 ASP.NET MVC 4 中的功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="9a745-445">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9a745-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="9a745-446">打开位于 Views\Shared 文件夹下的 **\_** " " 视图，并注意作为分部视图引用的视图切换器组件。</span><span class="sxs-lookup"><span data-stu-id="9a745-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="9a745-447">![使用视图切换器组件的移动布局](whats-new-in-aspnet-mvc-4/_static/image29.png "使用视图切换器组件的移动布局")</span><span class="sxs-lookup"><span data-stu-id="9a745-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="9a745-448">*使用视图切换器组件的移动布局*</span><span class="sxs-lookup"><span data-stu-id="9a745-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="9a745-449">打开 **\_ViewSwitcher**分部视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="9a745-450">分部视图使用新方法**ViewContext GetOverriddenBrowser （）** 来确定 web 请求的来源，并显示相应的链接以切换到桌面或移动视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="9a745-451">**GetOverriddenBrowser**方法返回一个**HttpBrowserCapabilitiesBase**实例，该实例对应于当前为请求设置的用户代理（实际或重写）。</span><span class="sxs-lookup"><span data-stu-id="9a745-451">The **GetOverriddenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="9a745-452">可以使用此值获取属性，如**IsMobileDevice**。</span><span class="sxs-lookup"><span data-stu-id="9a745-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="9a745-453">![ViewSwitcher 分部视图](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 分部视图")</span><span class="sxs-lookup"><span data-stu-id="9a745-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="9a745-454">*ViewSwitcher 分部视图*</span><span class="sxs-lookup"><span data-stu-id="9a745-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="9a745-455">打开位于 "**控制器**" 文件夹中的**ViewSwitcherController.cs**类。</span><span class="sxs-lookup"><span data-stu-id="9a745-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="9a745-456">查看 ViewSwitcher 组件中的链接是否调用了 SwitchView 操作，并注意新的 HttpContext 方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="9a745-457">**ClearOverriddenBrowser （）** 方法删除当前请求的任何重写的用户代理。</span><span class="sxs-lookup"><span data-stu-id="9a745-457">The **HttpContext.ClearOverriddenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="9a745-458">**SetOverriddenBrowser （）** 方法使用指定的用户代理覆盖请求的实际用户代理值。</span><span class="sxs-lookup"><span data-stu-id="9a745-458">The **HttpContext.SetOverriddenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="9a745-459">![ViewSwitcher 控制器](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 控制器 "）</span><span class="sxs-lookup"><span data-stu-id="9a745-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="9a745-460">*ViewSwitcher 控制器*</span><span class="sxs-lookup"><span data-stu-id="9a745-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="9a745-461">浏览器重写是 ASP.NET MVC 4 的一项核心功能，即使不安装 jQuery. node.js 包也是如此。</span><span class="sxs-lookup"><span data-stu-id="9a745-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="9a745-462">但是，此功能只会影响视图、布局和分部视图，而不会影响依赖于请求 .Browser 对象的任何功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="9a745-463">任务 5-在桌面视图中添加视图切换器</span><span class="sxs-lookup"><span data-stu-id="9a745-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="9a745-464">在此任务中，你将更新桌面布局以包含视图切换器。</span><span class="sxs-lookup"><span data-stu-id="9a745-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="9a745-465">这将允许移动用户在浏览桌面视图时返回到移动视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="9a745-466">刷新**Windows Phone 模拟器**中的站点。</span><span class="sxs-lookup"><span data-stu-id="9a745-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="9a745-467">单击库顶部的 "**桌面视图**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9a745-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="9a745-468">请注意，桌面视图中没有视图切换器允许返回到移动视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="9a745-469">返回到 Visual Studio 并打开 **\_布局. cshtml**视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="9a745-470">查找 login 节，并插入一个对 **\_LogOnPartial**分部视图下面 **\_ViewSwitcher**分部视图的调用。</span><span class="sxs-lookup"><span data-stu-id="9a745-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="9a745-471">然后，按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="9a745-472">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="9a745-473">刷新 Windows Phone 模拟器中的页面，然后双击屏幕进行放大。</span><span class="sxs-lookup"><span data-stu-id="9a745-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="9a745-474">请注意，主页现在会显示从移动到桌面视图切换的**移动视图**链接。</span><span class="sxs-lookup"><span data-stu-id="9a745-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="9a745-475">![在桌面视图中呈现的视图切换器](whats-new-in-aspnet-mvc-4/_static/image32.png "在桌面视图中呈现的视图切换器")</span><span class="sxs-lookup"><span data-stu-id="9a745-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="9a745-476">*在桌面视图中呈现的视图切换器*</span><span class="sxs-lookup"><span data-stu-id="9a745-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="9a745-477">再次切换到移动视图并浏览到 "**关于**" 页（ http://localhost [port]/Home/About）。</span><span class="sxs-lookup"><span data-stu-id="9a745-477">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="9a745-478">请注意，即使尚未创建 "关于" 视图，"关于" 页也会使用移动布局（\_Layout）来显示。</span><span class="sxs-lookup"><span data-stu-id="9a745-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="9a745-479">![关于页面](whats-new-in-aspnet-mvc-4/_static/image33.png "“关于”页面")</span><span class="sxs-lookup"><span data-stu-id="9a745-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="9a745-480">*关于页面*</span><span class="sxs-lookup"><span data-stu-id="9a745-480">*About page*</span></span>
8. <span data-ttu-id="9a745-481">最后，在桌面 Web 浏览器中打开该站点。</span><span class="sxs-lookup"><span data-stu-id="9a745-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="9a745-482">请注意，前面的所有更新都不会影响桌面视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="9a745-483">![PhotoGallery 桌面视图](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 桌面视图")</span><span class="sxs-lookup"><span data-stu-id="9a745-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="9a745-484">*PhotoGallery 桌面视图*</span><span class="sxs-lookup"><span data-stu-id="9a745-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="9a745-485">任务 6-创建新的显示模式</span><span class="sxs-lookup"><span data-stu-id="9a745-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="9a745-486">使用新的显示模式功能，应用程序可以根据生成请求的浏览器选择视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="9a745-487">例如，如果桌面浏览器请求主页，应用程序将返回**Views\Home\Index.cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="9a745-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="9a745-488">然后，如果移动浏览器请求主页，应用程序将返回**Views\Home\Index.mobile.cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="9a745-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="9a745-489">在此任务中，您将为 iPhone 设备创建自定义布局，并且必须模拟来自 iPhone 设备的请求。</span><span class="sxs-lookup"><span data-stu-id="9a745-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="9a745-490">为此，可以使用 iPhone 模拟器/模拟器（如[电气移动模拟器](http://www.electricplum.com/)）或带有修改用户代理的加载项的浏览器。</span><span class="sxs-lookup"><span data-stu-id="9a745-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="9a745-491">有关如何在 Safari 浏览器中设置用户代理字符串以模拟 iPhone 的说明，请参阅[如何让 Safari](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的博客中伪装成 IE。</span><span class="sxs-lookup"><span data-stu-id="9a745-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="9a745-492">**请注意，此任务是可选的，可以在整个实验室中继续执行，而无需执行此任务。**</span><span class="sxs-lookup"><span data-stu-id="9a745-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="9a745-493">在 Visual Studio 中，按**SHIFT** + **F5**停止调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="9a745-494">打开**Global.asax.cs**并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="9a745-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="9a745-495">将以下突出显示的代码添加到应用程序\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="9a745-496">（代码段- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*）</span><span class="sxs-lookup"><span data-stu-id="9a745-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="9a745-497">已在静态**DisplayModeProvider**静态列表中注册了**名为 &quot;iPhone&quot;** 的新 DefaultDisplayMode，该名称将与每个传入请求匹配。</span><span class="sxs-lookup"><span data-stu-id="9a745-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="9a745-498">如果传入请求包含 &quot;iPhone&quot;的字符串，则 ASP.NET MVC 将查找其名称包含 &quot;iPhone&quot; 后缀的视图。</span><span class="sxs-lookup"><span data-stu-id="9a745-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="9a745-499">0参数指示新模式的特定方式;例如，此视图比常规 &quot;移动&quot; 规则更具体，与移动设备的请求相匹配。</span><span class="sxs-lookup"><span data-stu-id="9a745-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="9a745-500">此代码运行后，当 iPhone 浏览器生成请求时，你的应用程序将使用**Views\Shared\\_Layout**将在后续步骤中创建的布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="9a745-501">这种测试 iPhone 请求的方法已为演示目的进行了简化，并可能不会按预期方式针对每个 iPhone 用户代理字符串（例如，测试区分大小写）。</span><span class="sxs-lookup"><span data-stu-id="9a745-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="9a745-502">在 Views\Shared 文件夹中创建 **\_** 的文件的副本，并将该副本重命名为 &quot;\_&quot;**Layout** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.cshtml**&quot;.</span></span>
5. <span data-ttu-id="9a745-503">打开你在上一步中创建 **\_Layout. cshtml** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-503">Open **\_Layout.iPhone.cshtml** you created in the previous step.</span></span>
6. <span data-ttu-id="9a745-504">查找数据角色属性设置为 "**页**" 的 div 元素，并将 "**数据"-"主题**" 属性更改**为 &quot;&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="9a745-505">现在，ASP.NET MVC 4 应用程序中有3个布局：</span><span class="sxs-lookup"><span data-stu-id="9a745-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="9a745-506">**\_布局。 cshtml**：用于桌面浏览器的默认布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="9a745-507">**\_layout**：移动设备使用的默认布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="9a745-508">**\_layout**： iphone 设备的特定布局，使用不同的配色方案来区分 \_的布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="9a745-509">按**F5**运行应用程序并浏览**Windows Phone 模拟器**中的站点。</span><span class="sxs-lookup"><span data-stu-id="9a745-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="9a745-510">打开**iphone 模拟器**（有关如何安装和配置 iPhone 模拟器的说明，请参阅[附录 C](#AppendixC) ），并浏览到站点。</span><span class="sxs-lookup"><span data-stu-id="9a745-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="9a745-511">请注意，每个电话使用特定的模板。</span><span class="sxs-lookup"><span data-stu-id="9a745-511">Notice that each phone is using the specific template.</span></span>

    ![使用-设备 2-不同的视图](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="9a745-513">*为每个移动设备使用不同的视图*</span><span class="sxs-lookup"><span data-stu-id="9a745-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="9a745-514">练习4：使用异步控制器</span><span class="sxs-lookup"><span data-stu-id="9a745-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="9a745-515">Microsoft .NET Framework 4.5 介绍了和 Visual Basic 中C#的新语言功能，以便为 .net 编程中的异步提供新的基础。</span><span class="sxs-lookup"><span data-stu-id="9a745-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="9a745-516">这一新基础使异步编程与-相关，并与同步编程一样简单。</span><span class="sxs-lookup"><span data-stu-id="9a745-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="9a745-517">现在可以使用**AsyncController**类在 ASP.NET MVC 4 中编写异步操作方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="9a745-518">对于长时间运行的非 CPU 绑定请求，可以使用异步操作方法。</span><span class="sxs-lookup"><span data-stu-id="9a745-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="9a745-519">这可以避免在处理请求时阻止 Web 服务器执行工作。</span><span class="sxs-lookup"><span data-stu-id="9a745-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="9a745-520">AsyncController 类通常用于长时间运行的 Web 服务调用。</span><span class="sxs-lookup"><span data-stu-id="9a745-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="9a745-521">本练习介绍 ASP.NET MVC 4 中异步操作的基本知识。</span><span class="sxs-lookup"><span data-stu-id="9a745-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="9a745-522">如果需要深入了解，可以查看以下文章： [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="9a745-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="9a745-523">任务 1-实现异步控制器</span><span class="sxs-lookup"><span data-stu-id="9a745-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="9a745-524">打开位于**Source/Ex4-Async/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="9a745-525">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="9a745-526">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="9a745-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="9a745-527">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="9a745-528">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="9a745-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="9a745-529">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9a745-530">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="9a745-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="9a745-531">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="9a745-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="9a745-532">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="9a745-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="9a745-533">从 "**控制器**" 文件夹打开**HomeController.cs**类。</span><span class="sxs-lookup"><span data-stu-id="9a745-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="9a745-534">添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="9a745-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="9a745-535">更新**HomeController**类，使其从**AsyncController**继承。</span><span class="sxs-lookup"><span data-stu-id="9a745-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="9a745-536">从 AsyncController 派生的控制器使 ASP.NET 能够处理异步请求，并且它们仍可为同步操作方法提供服务。</span><span class="sxs-lookup"><span data-stu-id="9a745-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="9a745-537">将**async**关键字添加到**Index**方法，并使其返回类型**任务&lt;ActionResult&gt;** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="9a745-538">**Async**关键字是 .NET Framework 4.5 提供的新关键字之一;它通知编译器此方法包含异步代码。</span><span class="sxs-lookup"><span data-stu-id="9a745-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="9a745-539">**Task**对象表示在将来的某个时间点可能完成的异步操作。</span><span class="sxs-lookup"><span data-stu-id="9a745-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="9a745-540">替换**客户端。** 使用 await 关键字的完整异步版本的 GetAsync （）调用，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9a745-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="9a745-541">（代码段- *ASP.NET MVC 4 Lab-Ex04-GetAsync*）</span><span class="sxs-lookup"><span data-stu-id="9a745-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="9a745-542">在以前的版本中，你使用**Task**对象的**Result**属性来阻止线程，直到返回结果（同步版本）。</span><span class="sxs-lookup"><span data-stu-id="9a745-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="9a745-543">添加**await**关键字告诉编译器异步等待从方法调用返回的任务。</span><span class="sxs-lookup"><span data-stu-id="9a745-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="9a745-544">这意味着，在等待的方法完成后，代码的其余部分将作为回调执行。</span><span class="sxs-lookup"><span data-stu-id="9a745-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="9a745-545">需要注意的另一点是，您无需更改您的 try-catch 块即可执行此操作：仍将捕获在后台或前台发生的异常，而不会使用框架提供的处理程序执行任何额外的工作。</span><span class="sxs-lookup"><span data-stu-id="9a745-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="9a745-546">更改代码，通过将行替换为新代码来继续异步实现，如下所示</span><span class="sxs-lookup"><span data-stu-id="9a745-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="9a745-547">（代码段- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*）</span><span class="sxs-lookup"><span data-stu-id="9a745-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="9a745-548">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-548">Run the application.</span></span> <span data-ttu-id="9a745-549">你将注意到没有重大更改，但你的代码不会阻止线程池中的线程，从而更好地使用服务器资源和提高性能。</span><span class="sxs-lookup"><span data-stu-id="9a745-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-550">若要详细了解实验室中新的异步编程功能，请 &quot; **.net 4.5 中的异步编程C#功能，以及**Visual Studio 培训工具包中包含的和 Visual Basic&quot;。</span><span class="sxs-lookup"><span data-stu-id="9a745-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="9a745-551">任务 2-用取消标记处理超时</span><span class="sxs-lookup"><span data-stu-id="9a745-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="9a745-552">返回任务实例的异步操作方法还可以支持超时。</span><span class="sxs-lookup"><span data-stu-id="9a745-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="9a745-553">在此任务中，您将更新 Index 方法代码，以使用取消标记处理超时情况。</span><span class="sxs-lookup"><span data-stu-id="9a745-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="9a745-554">返回到 Visual Studio 并按**SHIFT + F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="9a745-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="9a745-555">将以下 using 语句添加到**HomeController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="9a745-556">更新索引操作以接收**CancellationToken**参数。</span><span class="sxs-lookup"><span data-stu-id="9a745-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="9a745-557">更新**GetAsync**调用以传递取消标记。</span><span class="sxs-lookup"><span data-stu-id="9a745-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="9a745-558">（代码段- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*）</span><span class="sxs-lookup"><span data-stu-id="9a745-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="9a745-559">使用设置为500毫秒的**AsyncTimeout**特性装饰*索引*方法，并使用配置为通过重定向到**超时**视图来处理**TaskCanceledException**的**HandleError**属性。</span><span class="sxs-lookup"><span data-stu-id="9a745-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="9a745-560">（代码段- *ASP.NET MVC 4 Lab-Ex04*）</span><span class="sxs-lookup"><span data-stu-id="9a745-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="9a745-561">打开**PhotoController**类并更新**库**方法，以延迟执行1000毫秒（1秒）以模拟长时间运行的任务。</span><span class="sxs-lookup"><span data-stu-id="9a745-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 milliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="9a745-562">打开 web.config**文件，** 并添加以下元素，启用自定义错误。</span><span class="sxs-lookup"><span data-stu-id="9a745-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="9a745-563">在**Views\Shared**中创建一个名为**超时**的新视图，并使用默认布局。</span><span class="sxs-lookup"><span data-stu-id="9a745-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="9a745-564">在解决方案资源管理器中，右键单击**Views\Shared**文件夹，然后选择 "**添加 |视图**。</span><span class="sxs-lookup"><span data-stu-id="9a745-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="9a745-565">![为每个移动设备使用不同的视图](whats-new-in-aspnet-mvc-4/_static/image36.png "为每个移动设备使用不同的视图")</span><span class="sxs-lookup"><span data-stu-id="9a745-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="9a745-566">*为每个移动设备使用不同的视图*</span><span class="sxs-lookup"><span data-stu-id="9a745-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="9a745-567">按如下所示更新**超时**视图内容。</span><span class="sxs-lookup"><span data-stu-id="9a745-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="9a745-568">运行应用程序并导航到根 URL。</span><span class="sxs-lookup"><span data-stu-id="9a745-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="9a745-569">你添加了一个**线程。睡眠**1000 毫秒，你将会收到超时错误，该错误由**AsyncTimeout**属性生成，并由**HandleError**属性捕获。</span><span class="sxs-lookup"><span data-stu-id="9a745-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="9a745-570">![处理超时异常](whats-new-in-aspnet-mvc-4/_static/image37.png "处理超时异常")</span><span class="sxs-lookup"><span data-stu-id="9a745-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="9a745-571">*处理超时异常*</span><span class="sxs-lookup"><span data-stu-id="9a745-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="9a745-572">此外，还可以遵循[附录 D：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixD)Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="9a745-573">总结</span><span class="sxs-lookup"><span data-stu-id="9a745-573">Summary</span></span>

<span data-ttu-id="9a745-574">在此动手实验中，你已发现 ASP.NET MVC 4 中的一些新功能。</span><span class="sxs-lookup"><span data-stu-id="9a745-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="9a745-575">讨论了以下概念：</span><span class="sxs-lookup"><span data-stu-id="9a745-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="9a745-576">充分利用 ASP.NET MVC 项目模板的增强功能，包括新的移动应用程序项目模板</span><span class="sxs-lookup"><span data-stu-id="9a745-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="9a745-577">使用 HTML5 视区属性和 CSS 媒体查询改善移动设备上的显示</span><span class="sxs-lookup"><span data-stu-id="9a745-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="9a745-578">使用 jQuery Mobile 进行渐进式增强，并构建触摸优化 web UI</span><span class="sxs-lookup"><span data-stu-id="9a745-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="9a745-579">创建特定于移动设备的视图</span><span class="sxs-lookup"><span data-stu-id="9a745-579">Create mobile-specific views</span></span>
- <span data-ttu-id="9a745-580">使用视图切换器组件在应用程序的移动视图与桌面视图之间切换</span><span class="sxs-lookup"><span data-stu-id="9a745-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="9a745-581">使用任务支持创建异步控制器</span><span class="sxs-lookup"><span data-stu-id="9a745-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="9a745-582">附录 A：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="9a745-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="9a745-583">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="9a745-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="9a745-584">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="9a745-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="9a745-585">![使用 Visual Studio code 代码段将代码插入到项目中](whats-new-in-aspnet-mvc-4/_static/image38.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="9a745-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="9a745-586">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="9a745-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="9a745-587">***使用键盘添加代码片段（C#仅限）***</span><span class="sxs-lookup"><span data-stu-id="9a745-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="9a745-588">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="9a745-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="9a745-589">开始键入代码片段名称（不含空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="9a745-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="9a745-590">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="9a745-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="9a745-591">选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="9a745-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="9a745-592">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="9a745-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="9a745-593">![开始键入代码片段名称](whats-new-in-aspnet-mvc-4/_static/image39.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="9a745-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="9a745-594">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="9a745-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="9a745-595">![按 Tab 键以选择突出显示的代码段](whats-new-in-aspnet-mvc-4/_static/image40.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="9a745-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="9a745-596">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="9a745-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="9a745-597">![再次按 Tab 键，代码片段将展开](whats-new-in-aspnet-mvc-4/_static/image41.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="9a745-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="9a745-598">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="9a745-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="9a745-599">***使用鼠标添加代码片段（C#、VISUAL BASIC 和 XML）***</span><span class="sxs-lookup"><span data-stu-id="9a745-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="9a745-600">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="9a745-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="9a745-601">选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="9a745-602">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="9a745-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="9a745-603">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](whats-new-in-aspnet-mvc-4/_static/image42.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="9a745-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="9a745-604">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="9a745-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="9a745-605">![通过单击从列表中选择相关的代码片段](whats-new-in-aspnet-mvc-4/_static/image43.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="9a745-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="9a745-606">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="9a745-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="9a745-607">附录 B：安装 Web Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="9a745-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="9a745-608">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="9a745-609">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="9a745-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="9a745-610">请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="9a745-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="9a745-611">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并*使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web*的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="9a745-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="9a745-612">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-612">Click on **Install Now**.</span></span> <span data-ttu-id="9a745-613">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="9a745-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="9a745-614">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="9a745-615">![安装 Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="9a745-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="9a745-616">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="9a745-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="9a745-617">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="9a745-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="9a745-619">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="9a745-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="9a745-620">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="9a745-620">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="9a745-622">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="9a745-622">*Installation progress*</span></span>
6. <span data-ttu-id="9a745-623">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-623">When the installation completes, click **Finish**.</span></span>

    ![安装完成](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="9a745-625">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="9a745-625">*Installation completed*</span></span>
7. <span data-ttu-id="9a745-626">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="9a745-627">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="9a745-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="9a745-629">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="9a745-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="9a745-630">附录 C：安装 WebMatrix 2 和 iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="9a745-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="9a745-631">若要在模拟的 iPhone 设备中运行站点，可以使用 WebMatrix 扩展 &quot;适用于 iPhone&quot;的电子移动模拟器。</span><span class="sxs-lookup"><span data-stu-id="9a745-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="9a745-632">此外，还可以配置相同的扩展，以便从 Visual Studio 2012 运行模拟器。</span><span class="sxs-lookup"><span data-stu-id="9a745-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="9a745-633">任务 1-安装 WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="9a745-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="9a745-634">请参阅[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="9a745-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="9a745-635">或者，如果你已经安装了 Web 平台安装程序，则可以打开该安装程序并搜索产品 &quot;*WebMatrix 2*&quot;。</span><span class="sxs-lookup"><span data-stu-id="9a745-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="9a745-636">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-636">Click on **Install Now**.</span></span> <span data-ttu-id="9a745-637">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="9a745-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="9a745-638">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="9a745-639">![安装 WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "安装 WebMatrix 2")</span><span class="sxs-lookup"><span data-stu-id="9a745-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="9a745-640">*安装 WebMatrix 2*</span><span class="sxs-lookup"><span data-stu-id="9a745-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="9a745-641">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="9a745-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="9a745-642">![接受许可条款](whats-new-in-aspnet-mvc-4/_static/image50.png "接受许可条款")</span><span class="sxs-lookup"><span data-stu-id="9a745-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="9a745-643">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="9a745-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="9a745-644">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="9a745-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="9a745-645">![安装进度](whats-new-in-aspnet-mvc-4/_static/image51.png "安装进度")</span><span class="sxs-lookup"><span data-stu-id="9a745-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="9a745-646">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="9a745-646">*Installation progress*</span></span>
6. <span data-ttu-id="9a745-647">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="9a745-648">![安装完成](whats-new-in-aspnet-mvc-4/_static/image52.png "安装完成")</span><span class="sxs-lookup"><span data-stu-id="9a745-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="9a745-649">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="9a745-649">*Installation completed*</span></span>
7. <span data-ttu-id="9a745-650">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="9a745-651">任务 2-安装 iPhone 模拟器扩展</span><span class="sxs-lookup"><span data-stu-id="9a745-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="9a745-652">运行**WebMatrix**并打开任何现有网站，或创建新网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="9a745-653">单击 "**主页**" 功能区中的 "**运行**" 按钮，然后选择 "**添加新**的"。</span><span class="sxs-lookup"><span data-stu-id="9a745-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="9a745-654">![正在添加新的 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image53.png "正在添加新的 WebMatrix 扩展")</span><span class="sxs-lookup"><span data-stu-id="9a745-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="9a745-655">*正在添加新的 WebMatrix 扩展*</span><span class="sxs-lookup"><span data-stu-id="9a745-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="9a745-656">选择**IPhone 模拟器**，然后单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="9a745-657">![浏览 WebMatrix 扩展](whats-new-in-aspnet-mvc-4/_static/image54.png "浏览 WebMatrix 扩展")</span><span class="sxs-lookup"><span data-stu-id="9a745-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="9a745-658">*浏览 WebMatrix 扩展*</span><span class="sxs-lookup"><span data-stu-id="9a745-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="9a745-659">在 "包详细信息" 中，单击 "**安装**" 以继续安装扩展。</span><span class="sxs-lookup"><span data-stu-id="9a745-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="9a745-660">![iPhone 模拟器扩展](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 模拟器扩展")</span><span class="sxs-lookup"><span data-stu-id="9a745-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="9a745-661">*iPhone 模拟器扩展*</span><span class="sxs-lookup"><span data-stu-id="9a745-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="9a745-662">阅读并接受该扩展 EULA。</span><span class="sxs-lookup"><span data-stu-id="9a745-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="9a745-663">![WebMatrix 扩展 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 扩展 EULA")</span><span class="sxs-lookup"><span data-stu-id="9a745-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="9a745-664">*WebMatrix 扩展 EULA*</span><span class="sxs-lookup"><span data-stu-id="9a745-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="9a745-665">现在，你可以使用 iPhone 模拟器选项从 WebMatrix 运行你的网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="9a745-666">![使用 iPhone 运行](whats-new-in-aspnet-mvc-4/_static/image57.png "使用 iPhone 运行")</span><span class="sxs-lookup"><span data-stu-id="9a745-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="9a745-667">*使用 iPhone 运行*</span><span class="sxs-lookup"><span data-stu-id="9a745-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="9a745-668">任务 3-配置 Visual Studio 2012 以运行 iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="9a745-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="9a745-669">打开**Visual Studio 2012**并打开任何网站或创建新的项目。</span><span class="sxs-lookup"><span data-stu-id="9a745-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="9a745-670">单击 "运行" 按钮上的向下箭头，然后选择 "**浏览方式**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="9a745-671">![浏览方式](whats-new-in-aspnet-mvc-4/_static/image58.png "浏览方式")</span><span class="sxs-lookup"><span data-stu-id="9a745-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="9a745-672">*浏览方式*</span><span class="sxs-lookup"><span data-stu-id="9a745-672">*Browse with*</span></span>
3. <span data-ttu-id="9a745-673">在 &quot;浏览&quot; "对话框中，单击"**添加**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="9a745-674">在 &quot;添加程序&quot; "对话框中，使用以下值：</span><span class="sxs-lookup"><span data-stu-id="9a745-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="9a745-675">**Program**： C:\Users\*{CurrentUser} \* \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *（相应地更新路径）*</span><span class="sxs-lookup"><span data-stu-id="9a745-675">**Program**: C:\Users\*{CurrentUser}\*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
   - <span data-ttu-id="9a745-676">**参数**： &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="9a745-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="9a745-677">**友好名称**： iPhone 模拟器</span><span class="sxs-lookup"><span data-stu-id="9a745-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="9a745-678">![添加程序](whats-new-in-aspnet-mvc-4/_static/image59.png "添加程序")</span><span class="sxs-lookup"><span data-stu-id="9a745-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="9a745-679">*添加要浏览的程序*</span><span class="sxs-lookup"><span data-stu-id="9a745-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="9a745-680">单击 **"确定"** 并关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="9a745-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="9a745-681">现在，你可以从 Visual Studio 2012 在 iPhone 模拟器中运行你的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="9a745-682">![通过 iPhone 模拟器进行浏览](whats-new-in-aspnet-mvc-4/_static/image60.png "通过 iPhone 模拟器进行浏览")</span><span class="sxs-lookup"><span data-stu-id="9a745-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="9a745-683">*通过 iPhone 模拟器进行浏览*</span><span class="sxs-lookup"><span data-stu-id="9a745-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="9a745-684">附录 D：使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="9a745-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="9a745-685">本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="9a745-686">任务 1-从 Microsoft Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="9a745-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="9a745-687">请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="9a745-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-688">借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。</span><span class="sxs-lookup"><span data-stu-id="9a745-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="9a745-689">你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。</span><span class="sxs-lookup"><span data-stu-id="9a745-689">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="9a745-690">![登录到 Windows Azure 门户](whats-new-in-aspnet-mvc-4/_static/image61.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="9a745-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="9a745-691">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="9a745-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="9a745-692">单击命令栏上的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="9a745-693">![创建新网站](whats-new-in-aspnet-mvc-4/_static/image62.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="9a745-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="9a745-694">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="9a745-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="9a745-695">单击 "**计算** | **网站**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="9a745-696">然后选择 "**快速创建**" 选项。</span><span class="sxs-lookup"><span data-stu-id="9a745-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="9a745-697">为新网站提供可用 URL，并单击 "**创建**网站"。</span><span class="sxs-lookup"><span data-stu-id="9a745-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-698">Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a745-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="9a745-699">使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="9a745-700">它不包括设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="9a745-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="9a745-701">![使用 "快速创建" 创建新网站](whats-new-in-aspnet-mvc-4/_static/image63.png "使用 "快速创建" 创建新网站")</span><span class="sxs-lookup"><span data-stu-id="9a745-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="9a745-702">*使用 "快速创建" 创建新网站*</span><span class="sxs-lookup"><span data-stu-id="9a745-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="9a745-703">请**等到新网站创建完毕。**</span><span class="sxs-lookup"><span data-stu-id="9a745-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="9a745-704">创建网站后，单击 " **URL** " 列下的链接。</span><span class="sxs-lookup"><span data-stu-id="9a745-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="9a745-705">检查新网站是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="9a745-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="9a745-706">![浏览到新网站](whats-new-in-aspnet-mvc-4/_static/image64.png "浏览到新网站")</span><span class="sxs-lookup"><span data-stu-id="9a745-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="9a745-707">*浏览到新网站*</span><span class="sxs-lookup"><span data-stu-id="9a745-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="9a745-708">![网站正在运行](whats-new-in-aspnet-mvc-4/_static/image65.png "网站正在运行")</span><span class="sxs-lookup"><span data-stu-id="9a745-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="9a745-709">*网站正在运行*</span><span class="sxs-lookup"><span data-stu-id="9a745-709">*Web site running*</span></span>
6. <span data-ttu-id="9a745-710">返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="9a745-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="9a745-711">![打开网站管理页](whats-new-in-aspnet-mvc-4/_static/image66.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="9a745-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="9a745-712">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="9a745-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="9a745-713">在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9a745-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-714">*发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="9a745-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="9a745-715">发布配置文件包含连接到每个终结点并对其进行身份验证所需的 Url、用户凭据和数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="9a745-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="9a745-716">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="9a745-717">![下载网站发布配置文件](whats-new-in-aspnet-mvc-4/_static/image67.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="9a745-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="9a745-718">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="9a745-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="9a745-719">将发布配置文件下载到已知位置。</span><span class="sxs-lookup"><span data-stu-id="9a745-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="9a745-720">在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="9a745-721">![正在保存发布配置文件](whats-new-in-aspnet-mvc-4/_static/image68.png "正在保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="9a745-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="9a745-722">*正在保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="9a745-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="9a745-723">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="9a745-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="9a745-724">如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="9a745-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="9a745-725">如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="9a745-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="9a745-726">你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="9a745-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="9a745-727">可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="9a745-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="9a745-728">如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。</span><span class="sxs-lookup"><span data-stu-id="9a745-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="9a745-729">记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="9a745-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="9a745-730">请不要创建数据库，因为它将在后面的阶段创建。</span><span class="sxs-lookup"><span data-stu-id="9a745-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="9a745-731">![SQL 数据库服务器仪表板](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL 数据库服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="9a745-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="9a745-732">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="9a745-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="9a745-733">在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="9a745-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="9a745-734">为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](whats-new-in-aspnet-mvc-4/_static/image70.png)" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9a745-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="9a745-736">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="9a745-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="9a745-737">将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。</span><span class="sxs-lookup"><span data-stu-id="9a745-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="9a745-739">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="9a745-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="9a745-740">任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="9a745-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="9a745-741">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="9a745-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="9a745-742">在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="9a745-743">![发布应用程序](whats-new-in-aspnet-mvc-4/_static/image73.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="9a745-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="9a745-744">*发布网站*</span><span class="sxs-lookup"><span data-stu-id="9a745-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="9a745-745">导入您在第一个任务中保存的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="9a745-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="9a745-746">![导入发布配置文件](whats-new-in-aspnet-mvc-4/_static/image74.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="9a745-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="9a745-747">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="9a745-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="9a745-748">单击 "**验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-748">Click **Validate Connection**.</span></span> <span data-ttu-id="9a745-749">验证完成后，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9a745-750">验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="9a745-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="9a745-751">![正在验证连接](whats-new-in-aspnet-mvc-4/_static/image75.png "正在验证连接")</span><span class="sxs-lookup"><span data-stu-id="9a745-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="9a745-752">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="9a745-752">*Validating connection*</span></span>
4. <span data-ttu-id="9a745-753">在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="9a745-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="9a745-754">![Web 部署配置](whats-new-in-aspnet-mvc-4/_static/image76.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="9a745-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="9a745-755">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="9a745-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="9a745-756">按如下所示配置数据库连接：</span><span class="sxs-lookup"><span data-stu-id="9a745-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="9a745-757">在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。</span><span class="sxs-lookup"><span data-stu-id="9a745-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="9a745-758">在 "**用户名**" 中键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="9a745-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="9a745-759">在 "**密码**" 中键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="9a745-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="9a745-760">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="9a745-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="9a745-761">![正在配置目标连接字符串](whats-new-in-aspnet-mvc-4/_static/image77.png "正在配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="9a745-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="9a745-762">*正在配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="9a745-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="9a745-763">然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="9a745-763">Then click **OK**.</span></span> <span data-ttu-id="9a745-764">系统提示创建数据库时，单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="9a745-765">![创建数据库](whats-new-in-aspnet-mvc-4/_static/image78.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="9a745-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="9a745-766">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="9a745-766">*Creating the database*</span></span>
7. <span data-ttu-id="9a745-767">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="9a745-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="9a745-768">然后单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="9a745-768">Then click **Next**.</span></span>

    <span data-ttu-id="9a745-769">![指向 SQL 数据库的连接字符串](whats-new-in-aspnet-mvc-4/_static/image79.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="9a745-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="9a745-770">*指向 SQL 数据库的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="9a745-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="9a745-771">在 "**预览**" 页上，单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="9a745-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="9a745-772">![发布 web 应用程序](whats-new-in-aspnet-mvc-4/_static/image80.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="9a745-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="9a745-773">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="9a745-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="9a745-774">发布过程完成后，您的默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="9a745-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="9a745-775">![发布到 Windows Azure 的应用程序](whats-new-in-aspnet-mvc-4/_static/image81.png "发布到 Windows Azure 的应用程序")</span><span class="sxs-lookup"><span data-stu-id="9a745-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="9a745-776">*发布到 Windows Azure 的应用程序*</span><span class="sxs-lookup"><span data-stu-id="9a745-776">*Application published to Windows Azure*</span></span>
