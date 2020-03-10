---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 动手实验：一个 ASP.NET：集成 ASP.NET Web 窗体、MVC 和 Web API |Microsoft Docs
author: rick-anderson
description: ASP.NET 是一个框架，用于构建网站、应用程序和服务（使用 MVC、Web API 等专用技术）。 带有扩展 ASP.NET h 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505454"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="8f43b-104">动手实验：一个 ASP.NET：集成 ASP.NET Web 窗体、MVC 和 Web API</span><span class="sxs-lookup"><span data-stu-id="8f43b-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="8f43b-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="8f43b-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="8f43b-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="8f43b-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="8f43b-107">ASP.NET 是一个框架，用于构建网站、应用程序和服务（使用 MVC、Web API 等专用技术）。</span><span class="sxs-lookup"><span data-stu-id="8f43b-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="8f43b-108">由于扩展 ASP.NET 的创建和表示需要集成这些技术，因此，最新的工作就是使用**一个 ASP.NET**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="8f43b-109">Visual Studio 2013 引入了一个新的统一项目系统，可让你在一个项目中构建应用程序并使用所有 ASP.NET 技术。</span><span class="sxs-lookup"><span data-stu-id="8f43b-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="8f43b-110">此功能无需在项目开始时选取一种技术并坚持使用，而是鼓励在一个项目中使用多个 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="8f43b-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="8f43b-111">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。</span><span class="sxs-lookup"><span data-stu-id="8f43b-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="8f43b-112">概述</span><span class="sxs-lookup"><span data-stu-id="8f43b-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="8f43b-113">目标</span><span class="sxs-lookup"><span data-stu-id="8f43b-113">Objectives</span></span>

<span data-ttu-id="8f43b-114">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="8f43b-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="8f43b-115">基于**一个 ASP.NET**项目类型创建网站</span><span class="sxs-lookup"><span data-stu-id="8f43b-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="8f43b-116">在同一项目中使用不同的**ASP.NET**框架，如**MVC**和**Web API**</span><span class="sxs-lookup"><span data-stu-id="8f43b-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="8f43b-117">标识**ASP.NET**应用程序的主要组件</span><span class="sxs-lookup"><span data-stu-id="8f43b-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="8f43b-118">利用**ASP.NET 基架**框架自动创建控制器和视图，以根据模型类执行 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="8f43b-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="8f43b-119">为每个作业使用合适的工具公开计算机和人工可读格式的相同信息集</span><span class="sxs-lookup"><span data-stu-id="8f43b-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="8f43b-120">系统必备</span><span class="sxs-lookup"><span data-stu-id="8f43b-120">Prerequisites</span></span>

<span data-ttu-id="8f43b-121">完成本动手实验需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="8f43b-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="8f43b-122">Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="8f43b-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="8f43b-123">Visual Studio 2013 Update 1</span><span class="sxs-lookup"><span data-stu-id="8f43b-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="8f43b-124">安装</span><span class="sxs-lookup"><span data-stu-id="8f43b-124">Setup</span></span>

<span data-ttu-id="8f43b-125">若要运行此动手实验中的练习，您需要先设置您的环境。</span><span class="sxs-lookup"><span data-stu-id="8f43b-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="8f43b-126">打开 Windows 资源管理器并浏览到实验室的**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8f43b-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="8f43b-127">右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。</span><span class="sxs-lookup"><span data-stu-id="8f43b-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="8f43b-128">如果显示了 "用户帐户控制" 对话框，请确认操作以继续。</span><span class="sxs-lookup"><span data-stu-id="8f43b-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="8f43b-129">确保在运行安装过程之前，您已检查本实验的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="8f43b-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="8f43b-130">使用代码段</span><span class="sxs-lookup"><span data-stu-id="8f43b-130">Using the Code Snippets</span></span>

<span data-ttu-id="8f43b-131">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="8f43b-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="8f43b-132">为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。</span><span class="sxs-lookup"><span data-stu-id="8f43b-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="8f43b-133">每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。</span><span class="sxs-lookup"><span data-stu-id="8f43b-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="8f43b-134">请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="8f43b-135">在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。</span><span class="sxs-lookup"><span data-stu-id="8f43b-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="8f43b-136">如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="8f43b-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="8f43b-137">练习</span><span class="sxs-lookup"><span data-stu-id="8f43b-137">Exercises</span></span>

<span data-ttu-id="8f43b-138">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="8f43b-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="8f43b-139">创建新的 Web 窗体项目</span><span class="sxs-lookup"><span data-stu-id="8f43b-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="8f43b-140">使用基架创建 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="8f43b-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="8f43b-141">使用基架创建 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="8f43b-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="8f43b-142">完成本实验的估计时间： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="8f43b-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="8f43b-143">首次启动 Visual Studio 时，必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="8f43b-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="8f43b-144">每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="8f43b-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="8f43b-145">此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="8f43b-146">如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="8f43b-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="8f43b-147">练习1：创建新的 Web 窗体项目</span><span class="sxs-lookup"><span data-stu-id="8f43b-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="8f43b-148">在此练习中，你将使用**ASP.NET**统一项目体验在 Visual Studio 2013 中创建一个新的 Web 窗体网站，这将允许你轻松地将 Web 窗体、MVC 和 web API 组件集成到同一个应用程序中。</span><span class="sxs-lookup"><span data-stu-id="8f43b-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="8f43b-149">然后，你将浏览生成的解决方案并确定其部件，最后你会看到网站正在运行。</span><span class="sxs-lookup"><span data-stu-id="8f43b-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="8f43b-150">任务1–使用一 ASP.NET 体验创建新站点</span><span class="sxs-lookup"><span data-stu-id="8f43b-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="8f43b-151">在此任务中，你将基于 " **ASP.NET** " 项目类型在 Visual Studio 中开始创建新网站。</span><span class="sxs-lookup"><span data-stu-id="8f43b-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="8f43b-152">**一个 ASP.NET**统一了所有 ASP.NET 技术，并为你提供了根据需要进行混合和匹配的选项。</span><span class="sxs-lookup"><span data-stu-id="8f43b-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="8f43b-153">然后，你将识别应用程序中并行存在的 Web 窗体、MVC 和 Web API 的不同组件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="8f43b-154">打开 " **Web Visual Studio Express 2013** "，然后选择 "**文件" |新建项目 ...** 启动新解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![创建新项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="8f43b-156">*创建新项目*</span><span class="sxs-lookup"><span data-stu-id="8f43b-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="8f43b-157">在 "**新建项目**" 对话框中，选择 " **ASP.NET Web 应用程序**"。  **C#"Web** " 选项卡，并确保选择 **.NET Framework 4.5** "。</span><span class="sxs-lookup"><span data-stu-id="8f43b-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="8f43b-158">将项目命名为*MyHybridSite*，选择一个**位置**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="8f43b-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![新的 ASP.NET Web 应用程序项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="8f43b-160">*创建新的 ASP.NET Web 应用程序项目*</span><span class="sxs-lookup"><span data-stu-id="8f43b-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="8f43b-161">在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web 窗体**" 模板，并选择 " **MVC**和**Web API**选项"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="8f43b-162">此外，请确保 "**身份验证**" 选项设置为 "**单个用户帐户**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="8f43b-163">单击 **“确定”** 继续。</span><span class="sxs-lookup"><span data-stu-id="8f43b-163">Click **OK** to continue.</span></span>

    ![使用 Web 窗体模板创建新的项目，包括 Web API 和 MVC 组件](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="8f43b-165">*使用 Web 窗体模板创建新的项目，包括 Web API 和 MVC 组件*</span><span class="sxs-lookup"><span data-stu-id="8f43b-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="8f43b-166">你现在可以浏览生成的解决方案的结构。</span><span class="sxs-lookup"><span data-stu-id="8f43b-166">You can now explore the structure of the generated solution.</span></span>

    ![探索生成的解决方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="8f43b-168">*探索生成的解决方案*</span><span class="sxs-lookup"><span data-stu-id="8f43b-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="8f43b-169">**帐户：** 此文件夹包含要注册的 Web 窗体页，登录并管理应用程序的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="8f43b-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="8f43b-170">当在 Web 窗体项目模板的配置过程中选择**单个用户帐户**身份验证选项时，将添加此文件夹。</span><span class="sxs-lookup"><span data-stu-id="8f43b-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="8f43b-171">**模型：** 此文件夹将包含表示应用程序数据的类。</span><span class="sxs-lookup"><span data-stu-id="8f43b-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="8f43b-172">**控制器**和**视图**： **ASP.NET MVC**和**ASP.NET Web API**组件需要这些文件夹。</span><span class="sxs-lookup"><span data-stu-id="8f43b-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="8f43b-173">你将在下一练习中探索 MVC 和 Web API 技术。</span><span class="sxs-lookup"><span data-stu-id="8f43b-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="8f43b-174">Default.aspx **、default.aspx**和 **.aspx**文件是预定义的 Web 窗体**页，你**可以使用它们作为开始点来构建特定于你的应用程序的页面。</span><span class="sxs-lookup"><span data-stu-id="8f43b-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="8f43b-175">这些文件的编程逻辑位于一个单独的文件中，该文件称为 &quot;代码隐藏&quot; 文件，该文件具有 &quot;&quot; 或 &quot;&quot; 扩展（具体取决于所使用的语言）。</span><span class="sxs-lookup"><span data-stu-id="8f43b-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="8f43b-176">代码隐藏逻辑在服务器上运行，并动态生成页面的 HTML 输出。</span><span class="sxs-lookup"><span data-stu-id="8f43b-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="8f43b-177">**Master**和**node.js 页面定义**了应用程序中的所有页面的外观和标准行为。</span><span class="sxs-lookup"><span data-stu-id="8f43b-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="8f43b-178">双击**default.aspx**文件，浏览页面的内容。</span><span class="sxs-lookup"><span data-stu-id="8f43b-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![浏览 default.aspx 页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="8f43b-180">*浏览 default.aspx 页*</span><span class="sxs-lookup"><span data-stu-id="8f43b-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-181">文件顶部的**Page**指令定义 Web 窗体页的属性。</span><span class="sxs-lookup"><span data-stu-id="8f43b-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="8f43b-182">例如， **MasterPageFile**属性指定母版页的路径（在本例中为 "*站点母版页*"），**继承**属性定义要继承的页面的代码隐藏类。</span><span class="sxs-lookup"><span data-stu-id="8f43b-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="8f43b-183">此类位于由代码**隐藏**特性确定的文件中。</span><span class="sxs-lookup"><span data-stu-id="8f43b-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="8f43b-184">**Asp： Content**控件保存页面的实际内容（文本、标记和控件），并映射到母版页上的**asp： ContentPlaceHolder**控件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="8f43b-185">在这种情况下，将在 "MainContent *" 页中*定义的 " " 控件内呈现页面内容。</span><span class="sxs-lookup"><span data-stu-id="8f43b-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="8f43b-186">展开**应用\_启动**文件夹，然后注意**WebApiConfig.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="8f43b-187">Visual Studio 将该文件包含在生成的解决方案中，因为在配置项目时包含一个 ASP.NET 模板。</span><span class="sxs-lookup"><span data-stu-id="8f43b-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="8f43b-188">打开**WebApiConfig.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="8f43b-189">在*webapiconfig.cs*类中，你将找到与 web api 关联的配置，该配置将 HTTP 路由映射到**web api 控制器**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="8f43b-190">打开**RouteConfig.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="8f43b-191">在*RegisterRoutes*方法中，你将找到与 mvc 关联的配置，该配置将 HTTP 路由映射到**mvc 控制器**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="8f43b-192">任务2–运行解决方案</span><span class="sxs-lookup"><span data-stu-id="8f43b-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="8f43b-193">在此任务中，你将运行生成的解决方案，浏览应用及其一些功能，如 URL 重写和内置身份验证。</span><span class="sxs-lookup"><span data-stu-id="8f43b-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="8f43b-194">若要运行解决方案，请按**F5**或单击工具栏上的 "**开始**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8f43b-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="8f43b-195">应用程序主页应在浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="8f43b-195">The application home page should open in the browser.</span></span>

    ![运行解决方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="8f43b-197">验证是否正在调用 Web 窗体页。</span><span class="sxs-lookup"><span data-stu-id="8f43b-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="8f43b-198">为此，请将 **/contact.aspx**追加到地址栏中的 URL，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![友好的 URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="8f43b-200">*友好 Url*</span><span class="sxs-lookup"><span data-stu-id="8f43b-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-201">如您所见，URL 将更改为 **/contact**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="8f43b-202">从**ASP.NET 4**开始，URL 路由功能已添加到 Web 窗体，因此你可以编写类似 *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* 的 url，而不是 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* 。</span><span class="sxs-lookup"><span data-stu-id="8f43b-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="8f43b-203">有关详细信息，请参阅[URL 路由](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="8f43b-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="8f43b-204">现在，你将浏览集成到应用程序中的身份验证流。</span><span class="sxs-lookup"><span data-stu-id="8f43b-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="8f43b-205">为此，请单击页面右上角的 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![注册新用户](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="8f43b-207">*注册新用户*</span><span class="sxs-lookup"><span data-stu-id="8f43b-207">*Registering a new user*</span></span>
4. <span data-ttu-id="8f43b-208">在 "**注册**" 页上，输入**用户名**和**密码**，然后单击 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![注册页面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="8f43b-210">*注册页面*</span><span class="sxs-lookup"><span data-stu-id="8f43b-210">*Register page*</span></span>
5. <span data-ttu-id="8f43b-211">应用程序将注册新帐户，并对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="8f43b-211">The application registers the new account, and the user is authenticated.</span></span>

    ![用户已进行身份验证](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="8f43b-213">*用户已进行身份验证*</span><span class="sxs-lookup"><span data-stu-id="8f43b-213">*User authenticated*</span></span>
6. <span data-ttu-id="8f43b-214">返回到 Visual Studio 并按**SHIFT + F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="8f43b-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="8f43b-215">练习2：使用基架创建 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="8f43b-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="8f43b-216">在本练习中，你将利用 Visual Studio 提供的 ASP.NET 基架框架来创建 ASP.NET MVC 5 控制器，其中包含操作和 Razor 视图来执行 CRUD 操作，而无需编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="8f43b-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="8f43b-217">基架进程将使用实体框架 Code First 在 SQL 数据库中生成数据上下文和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="8f43b-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="8f43b-218">**关于实体框架 Code First**</span><span class="sxs-lookup"><span data-stu-id="8f43b-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="8f43b-219">实体框架（EF）是一个对象关系映射器（ORM），使您可以通过使用概念应用程序模型进行编程来创建数据访问应用程序，而无需使用关系存储架构直接编程。</span><span class="sxs-lookup"><span data-stu-id="8f43b-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="8f43b-220">利用实体框架 Code First 建模工作流，你可以使用自己的域类来表示 EF 在执行查询、更改跟踪和更新功能时所依赖的模型。</span><span class="sxs-lookup"><span data-stu-id="8f43b-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="8f43b-221">使用 Code First 开发工作流，无需通过创建数据库或指定架构来启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="8f43b-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="8f43b-222">相反，您可以编写为您的应用程序定义最适当的域模型对象的标准 .NET 类，实体框架将为您创建数据库。</span><span class="sxs-lookup"><span data-stu-id="8f43b-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="8f43b-223">可在[此处](../../../entity-framework.md)详细了解实体框架。</span><span class="sxs-lookup"><span data-stu-id="8f43b-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="8f43b-224">任务1–创建新模型</span><span class="sxs-lookup"><span data-stu-id="8f43b-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="8f43b-225">你现在将定义**Person**类，这将是基架进程用来创建 MVC 控制器和视图的模型。</span><span class="sxs-lookup"><span data-stu-id="8f43b-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="8f43b-226">首先要创建**Person**模型类，并使用基架功能自动创建控制器中的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="8f43b-227">打开**Visual Studio Express 2013 For Web** ，并打开位于**buildingappswithcachingservice-ex2-getproducts latency-cs-MvcScaffolding/Begin**文件夹中的**MyHybridSite**解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="8f43b-228">或者，你可以继续学习你在上一练习中获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="8f43b-229">在**解决方案资源管理器**中，右键单击**MyHybridSite**项目的 "**模型**" 文件夹，然后选择 "**添加 |类 ...** 。</span><span class="sxs-lookup"><span data-stu-id="8f43b-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![添加 Person 模型类](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="8f43b-231">*添加 Person 模型类*</span><span class="sxs-lookup"><span data-stu-id="8f43b-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="8f43b-232">在 "**添加新项**" 对话框中，将文件命名为 " *Person.cs* "，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![创建 Person 模型类](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="8f43b-234">*创建 Person 模型类*</span><span class="sxs-lookup"><span data-stu-id="8f43b-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="8f43b-235">将**Person.cs**文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="8f43b-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="8f43b-236">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="8f43b-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="8f43b-237">（代码段- *BringingTogetherOneAspNet-buildingappswithcachingservice-ex2-getproducts latency-cs-PersonClass*）</span><span class="sxs-lookup"><span data-stu-id="8f43b-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="8f43b-238">在**解决方案资源管理器**中，右键单击**MyHybridSite**项目并选择 "**生成**"，或按**CTRL + SHIFT + B**生成项目。</span><span class="sxs-lookup"><span data-stu-id="8f43b-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="8f43b-239">任务2–创建 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="8f43b-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="8f43b-240">创建**人员**模型后，将使用带有实体框架的 ASP.NET MVC 基架为**Person**创建 CRUD 控制器操作和视图。</span><span class="sxs-lookup"><span data-stu-id="8f43b-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="8f43b-241">在**解决方案资源管理器**中，右键单击**MyHybridSite**项目的 "**控制器**" 文件夹，然后选择 "**添加 |新建基架项 ...**</span><span class="sxs-lookup"><span data-stu-id="8f43b-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![创建新的基架控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="8f43b-243">*创建新的基架控制器*</span><span class="sxs-lookup"><span data-stu-id="8f43b-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="8f43b-244">在 "**添加基架**" 对话框中，选择 **"包含视图的 MVC 5 控制器，使用实体框架**"，然后单击 "**添加"。**</span><span class="sxs-lookup"><span data-stu-id="8f43b-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![选择包含视图和实体框架的 MVC 5 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="8f43b-246">*选择包含视图和实体框架的 MVC 5 控制器*</span><span class="sxs-lookup"><span data-stu-id="8f43b-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="8f43b-247">将*MvcPersonController*设置为**控制器名称**，选择 "**使用异步控制器操作**" 选项，并选择**Person （MyHybridSite）** 作为**模型类**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![使用基架添加 MVC 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="8f43b-249">*使用基架添加 MVC 控制器*</span><span class="sxs-lookup"><span data-stu-id="8f43b-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="8f43b-250">在 "**数据上下文类**" 下，单击 "**新建数据上下文 ...** "。</span><span class="sxs-lookup"><span data-stu-id="8f43b-250">Under **Data context class**, click **New data context...**.</span></span>

    ![创建新的数据上下文](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="8f43b-252">*创建新的数据上下文*</span><span class="sxs-lookup"><span data-stu-id="8f43b-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="8f43b-253">在 "**新建数据上下文**" 对话框中，将新的数据上下文命名为*PersonContext* ，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![创建新的 PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="8f43b-255">*创建新的 PersonContext 类型*</span><span class="sxs-lookup"><span data-stu-id="8f43b-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="8f43b-256">单击 "**添加**" 以创建具有基架的**人员**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="8f43b-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="8f43b-257">然后，Visual Studio 将生成控制器操作、人员数据上下文和 Razor 视图。</span><span class="sxs-lookup"><span data-stu-id="8f43b-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![用基架创建 MVC 控制器之后](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="8f43b-259">*用基架创建 MVC 控制器之后*</span><span class="sxs-lookup"><span data-stu-id="8f43b-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="8f43b-260">打开 "**控制器**" 文件夹中的**MvcPersonController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="8f43b-261">请注意，CRUD 操作方法已自动生成。</span><span class="sxs-lookup"><span data-stu-id="8f43b-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="8f43b-262">通过从前面步骤中的 "基架" 选项中选择 "**使用异步控制器操作**" 复选框，Visual Studio 将为涉及到 Person 数据上下文访问权限的所有操作生成异步操作方法。</span><span class="sxs-lookup"><span data-stu-id="8f43b-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="8f43b-263">建议为长时间运行的非 CPU 绑定的请求使用异步操作方法，以避免在处理请求时阻止 Web 服务器执行工作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="8f43b-264">任务3–运行解决方案</span><span class="sxs-lookup"><span data-stu-id="8f43b-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="8f43b-265">在此任务中，您将再次运行该解决方案以验证**人员**的视图是否按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="8f43b-266">您将添加一个新人员来验证是否已成功将其保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="8f43b-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="8f43b-267">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="8f43b-268">导航到 **/MvcPerson**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="8f43b-269">显示人员列表的基架视图应显示。</span><span class="sxs-lookup"><span data-stu-id="8f43b-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="8f43b-270">单击 "**新建**" 以添加新人员。</span><span class="sxs-lookup"><span data-stu-id="8f43b-270">Click **Create New** to add a new person.</span></span>

    ![导航到基架 MVC 视图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="8f43b-272">*导航到基架 MVC 视图*</span><span class="sxs-lookup"><span data-stu-id="8f43b-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="8f43b-273">在 "**创建**" 视图中，为人员提供**名称**和**年龄**，并单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![添加新人员](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="8f43b-275">*添加新人员*</span><span class="sxs-lookup"><span data-stu-id="8f43b-275">*Adding a new person*</span></span>
5. <span data-ttu-id="8f43b-276">新用户将添加到列表。</span><span class="sxs-lookup"><span data-stu-id="8f43b-276">The new person is added to the list.</span></span> <span data-ttu-id="8f43b-277">在元素列表中，单击 "**详细信息**" 以显示人员的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="8f43b-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="8f43b-278">然后，在**详细信息**视图中，单击 "**返回到列表**"，返回到列表视图。</span><span class="sxs-lookup"><span data-stu-id="8f43b-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![人员的详细信息视图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="8f43b-280">*人员的详细信息视图*</span><span class="sxs-lookup"><span data-stu-id="8f43b-280">*Person's details view*</span></span>
6. <span data-ttu-id="8f43b-281">单击 "**删除**" 链接以删除该用户。</span><span class="sxs-lookup"><span data-stu-id="8f43b-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="8f43b-282">在 "**删除**" 视图中，单击 "**删除**" 确认操作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![删除人员](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="8f43b-284">*删除人员*</span><span class="sxs-lookup"><span data-stu-id="8f43b-284">*Deleting a person*</span></span>
7. <span data-ttu-id="8f43b-285">返回到 Visual Studio 并按**SHIFT + F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="8f43b-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="8f43b-286">练习3：使用基架创建 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="8f43b-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="8f43b-287">Web API 框架是 ASP.NET 堆栈的一部分，旨在使实现 HTTP 服务更简单，通常通过 RESTful API 发送和接收 JSON 或 XML 格式的数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="8f43b-288">在此练习中，您将再次使用 ASP.NET 基架以生成 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="8f43b-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="8f43b-289">您将使用上一练习中的同一**person**和**PersonContext**类，以 JSON 格式提供同一个人数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="8f43b-290">你将了解如何以不同的方式在同一个 ASP.NET 应用程序中公开相同的资源。</span><span class="sxs-lookup"><span data-stu-id="8f43b-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="8f43b-291">任务1–创建 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="8f43b-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="8f43b-292">在此任务中，您将创建一个新的**WEB API 控制器**，它将以计算机可使用的格式（如 JSON）公开用户数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="8f43b-293">如果尚未打开，请打开**Visual Studio Express 2013 For Web** ，并打开位于**section-cs-WebAPI/Begin**文件夹中的**MyHybridSite**解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="8f43b-294">或者，你可以继续学习你在上一练习中获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-295">如果从练习3开始处理开始的解决方案，请按**CTRL + SHIFT + B**生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="8f43b-296">在**解决方案资源管理器**中，右键单击**MyHybridSite**项目的 "**控制器**" 文件夹，然后选择 "**添加 |新建基架项 ...**</span><span class="sxs-lookup"><span data-stu-id="8f43b-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![创建新的基架控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="8f43b-298">*创建新的基架控制器*</span><span class="sxs-lookup"><span data-stu-id="8f43b-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="8f43b-299">在 "**添加基架**" 对话框中，选择左窗格中的 " **web api** "，然后在中间窗格中选择 "**包含实体框架操作的 web api 2 控制器**"，并单击 "**添加"。**</span><span class="sxs-lookup"><span data-stu-id="8f43b-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="8f43b-300">![选择包含操作和实体框架的 Web API 2 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "选择包含操作和实体框架的 Web API 2 控制器")</span><span class="sxs-lookup"><span data-stu-id="8f43b-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="8f43b-301">*选择包含操作和实体框架的 Web API 2 控制器*</span><span class="sxs-lookup"><span data-stu-id="8f43b-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="8f43b-302">将*ApiPersonController*设置为**控制器名称**，选择 "**使用异步控制器操作**" 选项，并分别选择**Person （MyHybridSite）** 和**PersonContext （MyHybridSite）** 作为**模型**和**数据上下文**类。</span><span class="sxs-lookup"><span data-stu-id="8f43b-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="8f43b-303">然后单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="8f43b-303">Then click **Add**.</span></span>

    <span data-ttu-id="8f43b-304">![使用基架添加 Web API 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "使用基架添加 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="8f43b-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="8f43b-305">*使用基架添加 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="8f43b-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="8f43b-306">然后，Visual Studio 将生成具有四个 CRUD 操作的**ApiPersonController**类来处理数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="8f43b-307">![创建具有基架的 Web API 控制器之后](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "创建具有基架的 Web API 控制器之后")</span><span class="sxs-lookup"><span data-stu-id="8f43b-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="8f43b-308">*创建具有基架的 Web API 控制器之后*</span><span class="sxs-lookup"><span data-stu-id="8f43b-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="8f43b-309">打开**ApiPersonController.cs**文件并检查*GetPeople*操作方法。</span><span class="sxs-lookup"><span data-stu-id="8f43b-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="8f43b-310">此方法查询**PersonContext**类型的 db 字段，以获取人员数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="8f43b-311">现在，请注意方法定义上方的注释。</span><span class="sxs-lookup"><span data-stu-id="8f43b-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="8f43b-312">它提供公开此操作的 URI，你将在下一任务中使用此操作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="8f43b-313">默认情况下，Web API 配置为将查询捕获到 */api*路径，以避免与 MVC 控制器冲突。</span><span class="sxs-lookup"><span data-stu-id="8f43b-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="8f43b-314">如果需要更改此设置，请参阅[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="8f43b-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="8f43b-315">任务2–运行解决方案</span><span class="sxs-lookup"><span data-stu-id="8f43b-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="8f43b-316">在此任务中，您将使用 Internet Explorer **F12 开发人员工具**来检查 Web API 控制器的完整响应。</span><span class="sxs-lookup"><span data-stu-id="8f43b-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="8f43b-317">你将了解如何捕获网络流量，以便更深入地了解应用程序数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="8f43b-318">请确保在 Visual Studio 工具栏上的 "**开始**" 按钮中选择了**Internet Explorer** 。</span><span class="sxs-lookup"><span data-stu-id="8f43b-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 选项](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="8f43b-320">**F12 开发人员工具**具有一组广泛的功能，不在此动手实验中介绍。</span><span class="sxs-lookup"><span data-stu-id="8f43b-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="8f43b-321">如果要了解有关详细信息，请参阅[使用 F12 开发人员工具](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="8f43b-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="8f43b-322">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-323">为了正确执行此任务，应用程序需要有数据。</span><span class="sxs-lookup"><span data-stu-id="8f43b-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="8f43b-324">如果数据库为空，则可以返回到练习2中的任务3，并按照如何使用 MVC 视图创建新人员的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="8f43b-325">在浏览器中，按**F12**打开**开发人员工具**面板。</span><span class="sxs-lookup"><span data-stu-id="8f43b-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="8f43b-326">按**CTRL** + **4**或单击**网络**图标，然后单击绿色箭头按钮开始捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="8f43b-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="8f43b-327">![启动 Web API 网络捕获](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "启动 Web API 网络捕获")</span><span class="sxs-lookup"><span data-stu-id="8f43b-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="8f43b-328">*启动 Web API 网络捕获*</span><span class="sxs-lookup"><span data-stu-id="8f43b-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="8f43b-329">将**api/ApiPerson**追加到浏览器地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="8f43b-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="8f43b-330">现在，你将从**ApiPersonController**检查响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8f43b-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="8f43b-331">![通过 Web API 检索人员数据](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "通过 Web API 检索人员数据")</span><span class="sxs-lookup"><span data-stu-id="8f43b-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="8f43b-332">*通过 Web API 检索人员数据*</span><span class="sxs-lookup"><span data-stu-id="8f43b-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-333">下载完成后，系统将提示您使用下载的文件进行操作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="8f43b-334">让对话框保持打开状态，以便能够通过 "开发人员工具" 窗口观看响应内容。</span><span class="sxs-lookup"><span data-stu-id="8f43b-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="8f43b-335">现在，你将检查响应的正文。</span><span class="sxs-lookup"><span data-stu-id="8f43b-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="8f43b-336">为此，请单击 "**详细信息**" 选项卡，然后单击 "**响应正文**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="8f43b-337">您可以检查下载的数据是否是对象的列表，这些对象具有与**Person**类对应的 " **Id**"、"**名称**" 和 "**年龄**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="8f43b-338">![查看 Web API 响应正文](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "查看 Web API 响应正文")</span><span class="sxs-lookup"><span data-stu-id="8f43b-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="8f43b-339">*查看 Web API 响应正文*</span><span class="sxs-lookup"><span data-stu-id="8f43b-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="8f43b-340">任务3–添加 Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="8f43b-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="8f43b-341">创建 Web API 时，创建帮助页非常有用，以便其他开发人员知道如何调用 API。</span><span class="sxs-lookup"><span data-stu-id="8f43b-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="8f43b-342">您可以手动创建和更新文档页，但最好是自动生成文档页，以避免执行维护工作。</span><span class="sxs-lookup"><span data-stu-id="8f43b-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="8f43b-343">在此任务中，你将使用 Nuget 包自动向解决方案生成 Web API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="8f43b-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="8f43b-344">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后单击 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="8f43b-345">在 "**包管理器控制台**" 窗口中，执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8f43b-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="8f43b-346">**WebApi. HelpPage**包将安装所需的程序集，并添加 "**区域/HelpPage** " 文件夹下 "帮助" 页的 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="8f43b-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="8f43b-347">![HelpPage 面积图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 面积图")</span><span class="sxs-lookup"><span data-stu-id="8f43b-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="8f43b-348">*HelpPage 面积图*</span><span class="sxs-lookup"><span data-stu-id="8f43b-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="8f43b-349">默认情况下，帮助页包含文档的占位符字符串。</span><span class="sxs-lookup"><span data-stu-id="8f43b-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="8f43b-350">您可以使用 XML 文档注释来创建文档。</span><span class="sxs-lookup"><span data-stu-id="8f43b-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="8f43b-351">若要启用此功能，请打开**HelpPageConfig.cs**文件，该文件位于 "**区域/HelpPage/应用\_Start** " 文件夹中，并取消注释以下行：</span><span class="sxs-lookup"><span data-stu-id="8f43b-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="8f43b-352">在**解决方案资源管理器**中，右键单击**MyHybridSite**项目，选择 "**属性**"，然后单击 "**生成**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8f43b-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="8f43b-353">![生成选项卡](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "生成部分")</span><span class="sxs-lookup"><span data-stu-id="8f43b-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="8f43b-354">*生成选项卡*</span><span class="sxs-lookup"><span data-stu-id="8f43b-354">*Build tab*</span></span>
5. <span data-ttu-id="8f43b-355">在 "**输出**" 下，选择 " **XML 文档文件**"。</span><span class="sxs-lookup"><span data-stu-id="8f43b-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="8f43b-356">在 "编辑" 框中，键入**App\_Data/xml**。</span><span class="sxs-lookup"><span data-stu-id="8f43b-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="8f43b-357">!["生成" 选项卡中的输出部分](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png ""生成" 选项卡中的输出部分")</span><span class="sxs-lookup"><span data-stu-id="8f43b-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="8f43b-358">*"生成" 选项卡中的输出部分*</span><span class="sxs-lookup"><span data-stu-id="8f43b-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="8f43b-359">按**CTRL** + **S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="8f43b-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="8f43b-360">从 "**控制器**" 文件夹打开**ApiPersonController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8f43b-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="8f43b-361">在*GetPeople*方法签名和 *//GET api/ApiPerson*注释之间输入一个新行，然后键入三个正斜杠。</span><span class="sxs-lookup"><span data-stu-id="8f43b-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-362">Visual Studio 会自动插入定义方法文档的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="8f43b-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="8f43b-363">为*GetPeople*方法添加摘要文本和返回值。</span><span class="sxs-lookup"><span data-stu-id="8f43b-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="8f43b-364">其外观应如下所示。</span><span class="sxs-lookup"><span data-stu-id="8f43b-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="8f43b-365">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="8f43b-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="8f43b-366">将 **/help**追加到地址栏中的 URL，浏览到 "帮助" 页。</span><span class="sxs-lookup"><span data-stu-id="8f43b-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="8f43b-367">![ASP.NET Web API 帮助页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 帮助页")</span><span class="sxs-lookup"><span data-stu-id="8f43b-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="8f43b-368">*ASP.NET Web API 帮助页*</span><span class="sxs-lookup"><span data-stu-id="8f43b-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f43b-369">页面的主要内容是 Api 表，按控制器分组。</span><span class="sxs-lookup"><span data-stu-id="8f43b-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="8f43b-370">表项是使用**IApiExplorer**接口动态生成的。</span><span class="sxs-lookup"><span data-stu-id="8f43b-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="8f43b-371">如果添加或更新 API 控制器，下一次生成应用程序时，该表会自动更新。</span><span class="sxs-lookup"><span data-stu-id="8f43b-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="8f43b-372">" **API** " 列列出 HTTP 方法和相对 URI。</span><span class="sxs-lookup"><span data-stu-id="8f43b-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="8f43b-373">"**说明**" 列包含已从方法的文档中提取的信息。</span><span class="sxs-lookup"><span data-stu-id="8f43b-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="8f43b-374">请注意，在 "说明" 列中将显示在方法定义上方添加的说明。</span><span class="sxs-lookup"><span data-stu-id="8f43b-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="8f43b-375">![API 方法说明](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 方法说明")</span><span class="sxs-lookup"><span data-stu-id="8f43b-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="8f43b-376">*API 方法说明*</span><span class="sxs-lookup"><span data-stu-id="8f43b-376">*API method description*</span></span>
13. <span data-ttu-id="8f43b-377">单击其中一个 API 方法可以导航到包含更多详细信息（包括示例响应正文）的页面。</span><span class="sxs-lookup"><span data-stu-id="8f43b-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="8f43b-378">![详细信息页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "详细信息页")</span><span class="sxs-lookup"><span data-stu-id="8f43b-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="8f43b-379">*详细信息页*</span><span class="sxs-lookup"><span data-stu-id="8f43b-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="8f43b-380">摘要</span><span class="sxs-lookup"><span data-stu-id="8f43b-380">Summary</span></span>

<span data-ttu-id="8f43b-381">通过完成本动手实验，你学习了如何：</span><span class="sxs-lookup"><span data-stu-id="8f43b-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="8f43b-382">在 Visual Studio 2013 中使用一种 ASP.NET 体验创建新的 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="8f43b-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="8f43b-383">将多个 ASP.NET 技术集成到一个项目中</span><span class="sxs-lookup"><span data-stu-id="8f43b-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="8f43b-384">使用 ASP.NET 基架从模型类生成 MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="8f43b-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="8f43b-385">生成 Web API 控制器，该控制器通过使用异步编程和数据访问等功能实体框架</span><span class="sxs-lookup"><span data-stu-id="8f43b-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="8f43b-386">为控制器自动生成 Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="8f43b-386">Automatically generate Web API Help Pages for your controllers</span></span>
