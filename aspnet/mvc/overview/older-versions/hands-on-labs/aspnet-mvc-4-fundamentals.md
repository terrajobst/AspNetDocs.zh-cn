---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 基础 |Microsoft Docs
author: rick-anderson
description: 此动手实验基于 MVC （模型视图控制器）音乐商店，这是一个教程应用程序，介绍如何使用 ASP.NET MV 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484568"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="fe6f1-103">ASP.NET MVC 4 基础知识</span><span class="sxs-lookup"><span data-stu-id="fe6f1-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="fe6f1-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="fe6f1-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="fe6f1-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="fe6f1-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="fe6f1-106">此动手实验基于 MVC （模型视图控制器）音乐商店，这是一个教程应用程序，介绍如何使用 ASP.NET MVC 和 Visual Studio 的分步说明。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="fe6f1-107">在整个实验室中，您将学习这一简单功能，同时还能利用这些技术。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="fe6f1-108">你将从一个简单的应用程序开始，并将生成该应用程序，直到你具有一个功能完备的 ASP.NET MVC 4 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="fe6f1-109">此实验室与 ASP.NET MVC 4 结合使用。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="fe6f1-110">若要浏览教程应用程序的 ASP.NET MVC 3 版本，可以在[mvc-音乐存储](https://github.com/evilDave/MVC-Music-Store)中找到它。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="fe6f1-111">此动手实验假设开发人员在 Web 开发技术（例如 HTML 和 JavaScript）中拥有经验。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="fe6f1-112">所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="fe6f1-113">[ASP.NET MVC 4 基础](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)上提供了特定于此实验室的项目。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="fe6f1-114">音乐应用商店应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-114">The Music Store application</span></span>

<span data-ttu-id="fe6f1-115">将在整个实验室中生成的音乐应用商店 web 应用程序由三个主要部分组成：购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="fe6f1-116">访问者将能够按流派浏览唱片集，将唱片集添加到购物车，查看其选择内容，最后继续结帐以登录并完成订单。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="fe6f1-117">此外，商店管理员还可以管理可用唱集及其主要属性。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="fe6f1-118">![音乐应用商店屏幕](aspnet-mvc-4-fundamentals/_static/image1.png "音乐应用商店屏幕")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="fe6f1-119">*音乐应用商店屏幕*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="fe6f1-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="fe6f1-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="fe6f1-121">将使用**模型视图控制器（MVC）** 构建音乐应用商店应用程序，这种体系结构模式将应用程序分成三个主要组件：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="fe6f1-122">**模型**：模型对象是应用程序中实现域逻辑的部分。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="fe6f1-123">通常，模型对象还检索模型状态并将其存储在数据库中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="fe6f1-124">**视图：** 视图是显示应用程序的用户界面（UI）的组件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="fe6f1-125">通常，此 UI 是用模型数据创建的。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="fe6f1-126">例如，将根据唱片集对象的当前状态显示文本框和下拉列表的影集的 "编辑" 视图。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="fe6f1-127">**控制器：** 控制器是处理用户交互、操作模型并最终选择视图以呈现 UI 的组件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="fe6f1-128">在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="fe6f1-129">MVC 模式可帮助你创建应用程序，用于分离应用程序的不同方面（输入逻辑、业务逻辑和 UI 逻辑），同时在这些元素之间提供松散耦合。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="fe6f1-130">这种隔离可帮助你在构建应用程序时管理复杂性，因为它允许你一次集中关注实现的一个方面。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="fe6f1-131">此外，MVC 模式使测试应用程序变得轻松，同时鼓励使用测试驱动开发（TDD）来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="fe6f1-132">**ASP.NET MVC**框架提供 ASP.NET Web 窗体模式的替代方法，用于创建基于 ASP.NET MVC 的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="fe6f1-133">**ASP.NET MVC**框架是一种轻型、高度可测试的表示框架，与基于 Web 窗体的应用程序一样，它与现有的 ASP.NET 功能（如母版页和基于成员身份的身份验证）集成，因此你可以获得核心 .net framework 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="fe6f1-134">如果已熟悉 ASP.NET Web 窗体，则这非常有用，因为你已使用的所有库也可用于 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="fe6f1-135">此外，MVC 应用程序的三个主要组件之间的松散耦合还可促进并行开发。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="fe6f1-136">例如，一个开发人员可以使用该视图，另一个开发人员可以处理控制器逻辑，而第三位开发人员可以专注于模型中的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="fe6f1-137">目标</span><span class="sxs-lookup"><span data-stu-id="fe6f1-137">Objectives</span></span>

<span data-ttu-id="fe6f1-138">在此动手实验中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="fe6f1-139">根据音乐应用商店应用程序教程从头开始创建 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="fe6f1-140">添加控制器以处理网站主页的 Url，并浏览其主要功能</span><span class="sxs-lookup"><span data-stu-id="fe6f1-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="fe6f1-141">添加视图以自定义显示的内容及其样式</span><span class="sxs-lookup"><span data-stu-id="fe6f1-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="fe6f1-142">添加模型类以包含和管理数据和域逻辑</span><span class="sxs-lookup"><span data-stu-id="fe6f1-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="fe6f1-143">使用视图模型模式将信息从控制器操作传递到视图模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="fe6f1-144">浏览 internet 应用程序的 ASP.NET MVC 4 新模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="fe6f1-145">系统必备</span><span class="sxs-lookup"><span data-stu-id="fe6f1-145">Prerequisites</span></span>

<span data-ttu-id="fe6f1-146">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="fe6f1-147">[Visual Studio 2012 Express For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （有关如何安装的说明，请参阅[附录 A](#AppendixA) ）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="fe6f1-148">安装</span><span class="sxs-lookup"><span data-stu-id="fe6f1-148">Setup</span></span>

<span data-ttu-id="fe6f1-149">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="fe6f1-150">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="fe6f1-151">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="fe6f1-152">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[C： &quot;附录 C：&quot;的代码段](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="fe6f1-153">练习</span><span class="sxs-lookup"><span data-stu-id="fe6f1-153">Exercises</span></span>

<span data-ttu-id="fe6f1-154">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="fe6f1-155">练习1：创建 MusicStore ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="fe6f1-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="fe6f1-156">练习2：创建控制器</span><span class="sxs-lookup"><span data-stu-id="fe6f1-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="fe6f1-157">练习3：向控制器传递参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="fe6f1-158">练习4：创建视图</span><span class="sxs-lookup"><span data-stu-id="fe6f1-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="fe6f1-159">练习5：创建视图模型</span><span class="sxs-lookup"><span data-stu-id="fe6f1-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="fe6f1-160">练习6：在视图中使用参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="fe6f1-161">练习7：重叠 ASP.NET MVC 4 新模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="fe6f1-162">每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="fe6f1-163">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="fe6f1-164">完成本实验的估计时间： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="fe6f1-165">练习1：创建 MusicStore ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="fe6f1-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="fe6f1-166">在此练习中，您将学习如何在 Visual Studio 2012 Express for Web 及其主文件夹组织中创建 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="fe6f1-167">此外，你将了解如何添加新控制器并使其在应用程序的主页中显示一个简单的字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="fe6f1-168">任务 1-创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="fe6f1-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="fe6f1-169">在此任务中，你将使用 MVC Visual Studio 模板创建一个空的 ASP.NET MVC 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="fe6f1-170">开始**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="fe6f1-171">在“文件”菜单上，单击“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="fe6f1-172">在 "**新建项目**" 对话框中，选择 " **ASP.NET MVC 4 Web 应用程序**" 项目类型，该类型位于 "  **C#Visual，** **web**模板列表" 下。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="fe6f1-173">将**名称**更改为*MvcMusicStore*。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="fe6f1-174">在此练习的源文件夹中，将解决方案的位置设置为新的**Begin**文件夹，例如 **[\Source\Ex01-CreatingMusicStoreProject\Begin]** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="fe6f1-175">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-175">Click **OK**.</span></span>

    <span data-ttu-id="fe6f1-176">!["创建新项目" 对话框](aspnet-mvc-4-fundamentals/_static/image2.png ""创建新项目" 对话框")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="fe6f1-177">*"创建新项目" 对话框*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="fe6f1-178">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 "**基本**" 模板，并确保所选的**视图引擎**为**Razor**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="fe6f1-179">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-179">Click **OK**.</span></span>

    <span data-ttu-id="fe6f1-180">!["新建 ASP.NET MVC 4 项目" 对话框](aspnet-mvc-4-fundamentals/_static/image3.png ""新建 ASP.NET MVC 4 项目" 对话框")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="fe6f1-181">*"新建 ASP.NET MVC 4 项目" 对话框*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="fe6f1-182">任务 2-探索解决方案结构</span><span class="sxs-lookup"><span data-stu-id="fe6f1-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="fe6f1-183">ASP.NET MVC 框架包含一个 Visual Studio 项目模板，可帮助你创建支持 MVC 模式的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="fe6f1-184">此模板使用所需的文件夹、项模板和配置文件项创建一个新的 ASP.NET MVC Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="fe6f1-185">在此任务中，您将检查解决方案结构，以了解所涉及的元素以及它们之间的关系。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="fe6f1-186">以下文件夹包含在所有 ASP.NET MVC 应用程序中，因为 ASP.NET MVC 框架默认情况下使用 &quot;约定 over 配置&quot; 方法，并基于文件夹命名约定做出一些默认假设。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="fe6f1-187">创建项目后，请查看在右侧的解决方案资源管理器中创建的文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="fe6f1-188">![解决方案资源管理器中的 ASP.NET MVC 文件夹结构](aspnet-mvc-4-fundamentals/_static/image4.png "解决方案资源管理器中的 ASP.NET MVC 文件夹结构")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="fe6f1-189">*解决方案资源管理器中的 ASP.NET MVC 文件夹结构*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="fe6f1-190">**控制器**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-190">**Controllers**.</span></span> <span data-ttu-id="fe6f1-191">此文件夹将包含控制器类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="fe6f1-192">在基于 MVC 的应用程序中，控制器负责处理最终用户交互、操作模型，并最终选择用于呈现 UI 的视图。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="fe6f1-193">MVC 框架要求所有控制器的名称以 &quot;控制器&quot;结束，例如 HomeController、LoginController 或 ProductController。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="fe6f1-194">**模型**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-194">**Models**.</span></span> <span data-ttu-id="fe6f1-195">此文件夹是为表示 MVC Web 应用程序的应用程序模型的类提供的。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="fe6f1-196">这通常包括定义对象的代码和用于与数据存储区交互的逻辑。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="fe6f1-197">通常，实际模型对象将位于单独的类库中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="fe6f1-198">但是，在创建新的应用程序时，您可能会包括类，然后在开发周期的稍后阶段将它们移到单独的类库中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="fe6f1-199">**视图**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-199">**Views**.</span></span> <span data-ttu-id="fe6f1-200">此文件夹是视图的建议位置，这些组件负责显示应用程序的用户界面。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="fe6f1-201">除了与呈现视图相关的任何其他文件，视图还使用 .aspx、.ascx、# 和 .master 文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="fe6f1-202">Views 文件夹包含每个控制器的文件夹;文件夹以控制器名称前缀命名。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="fe6f1-203">例如，如果你有一个名为**HomeController**的控制器，Views 文件夹将包含名为 Home 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="fe6f1-204">默认情况下，当 ASP.NET MVC 框架加载视图时，它将在 Views\controllerName 文件夹（**views [controllerName] [action] .aspx**）或 Razor 视图的（**views [ControllerName] [action]** ）中查找具有请求的视图名称的 .aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fe6f1-205">除了前面列出的文件夹，MVC Web 应用程序还使用**global.asax**文件设置全局 URL 路由默认值，并使用**web.config 文件来**配置应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="fe6f1-206">任务 3-添加 HomeController</span><span class="sxs-lookup"><span data-stu-id="fe6f1-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="fe6f1-207">在不使用 MVC 框架的 ASP.NET 应用程序中，用户交互按照页面以及从这些页面引发和处理事件的方式进行组织。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="fe6f1-208">相比之下，用户与 ASP.NET MVC 应用程序的交互是围绕控制器及其操作方法组织的。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="fe6f1-209">另一方面，ASP.NET MVC 框架将 Url 映射到称为控制器的类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="fe6f1-210">控制器处理传入的请求，处理用户输入和交互，执行适当的应用程序逻辑，并确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他 URL 等）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="fe6f1-211">对于显示 HTML，控制器类通常会调用单独的视图组件来生成请求的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="fe6f1-212">在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="fe6f1-213">在此任务中，你将添加一个控制器类，该类将处理指向音乐应用商店网站主页的 Url。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="fe6f1-214">在解决方案资源管理器中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后选择 "**控制器**" 命令：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="fe6f1-215">![添加控制器命令](aspnet-mvc-4-fundamentals/_static/image5.png "添加控制器命令")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="fe6f1-216">*添加控制器命令*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="fe6f1-217">"**添加控制器**" 对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="fe6f1-218">将控制器命名为*HomeController* ，然后按 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="fe6f1-219">!["添加控制器" 对话框](aspnet-mvc-4-fundamentals/_static/image6.png ""添加控制器" 对话框")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="fe6f1-220">*"添加控制器" 对话框*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="fe6f1-221">**在 controller 文件夹中**创建文件**HomeController.cs** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="fe6f1-222">为了使**HomeController**返回其索引操作的字符串，请将**Index**方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="fe6f1-223">（代码段- *ASP.NET MVC 4 基础-Ex1 HomeController Index*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="fe6f1-224">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="fe6f1-225">在此任务中，你将在 web 浏览器中尝试应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="fe6f1-226">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="fe6f1-227">项目已编译并且本地 IIS Web 服务器启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="fe6f1-228">本地 IIS Web 服务器将自动打开指向 Web 服务器 URL 的 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="fe6f1-229">![在 web 浏览器中运行的应用程序](aspnet-mvc-4-fundamentals/_static/image7.png "在 web 浏览器中运行的应用程序")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="fe6f1-230">*在 web 浏览器中运行的应用程序*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-231">本地 IIS Web 服务器将按随机可用端口号运行网站。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="fe6f1-232">在上图中，站点正在 `http://localhost:50103/`上运行，因此使用的是端口50103。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="fe6f1-233">端口号可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-233">Your port number may vary.</span></span>
2. <span data-ttu-id="fe6f1-234">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="fe6f1-235">练习2：创建控制器</span><span class="sxs-lookup"><span data-stu-id="fe6f1-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="fe6f1-236">在此练习中，您将学习如何更新控制器以实现音乐应用商店应用程序的简单功能。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="fe6f1-237">该控制器将定义用于处理以下每个特定请求的操作方法：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="fe6f1-238">音乐应用商店中音乐流派的列表页</span><span class="sxs-lookup"><span data-stu-id="fe6f1-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="fe6f1-239">列出特定流派的所有音乐唱片集的浏览页</span><span class="sxs-lookup"><span data-stu-id="fe6f1-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="fe6f1-240">显示特定音乐唱片集相关信息的详细信息页</span><span class="sxs-lookup"><span data-stu-id="fe6f1-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="fe6f1-241">对于本练习的作用域，这些操作将只返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="fe6f1-242">任务 1-添加新的 StoreController 类</span><span class="sxs-lookup"><span data-stu-id="fe6f1-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="fe6f1-243">在此任务中，将添加新的控制器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="fe6f1-244">如果尚未打开，请启动**VS Express for Web 2012**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="fe6f1-245">在 "**文件**" 菜单中，选择 "**打开项目**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="fe6f1-246">在 "打开项目" 对话框中，浏览到**Source\Ex02-CreatingAController\Begin**，选择 "**开始**"，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="fe6f1-247">或者，您也可以继续使用在完成上一练习后获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="fe6f1-248">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fe6f1-249">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fe6f1-250">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fe6f1-251">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fe6f1-252">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fe6f1-253">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fe6f1-254">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fe6f1-255">添加新控制器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-255">Add the new controller.</span></span> <span data-ttu-id="fe6f1-256">为此，请在解决方案资源管理器中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后选择 "**控制器**" 命令。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="fe6f1-257">将**控制器名称**更改为*StoreController*，并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="fe6f1-258">!["添加控制器" 对话框](aspnet-mvc-4-fundamentals/_static/image8.png ""添加控制器" 对话框")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="fe6f1-259">*"添加控制器" 对话框*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="fe6f1-260">任务 2-修改 StoreController 的操作</span><span class="sxs-lookup"><span data-stu-id="fe6f1-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="fe6f1-261">在此任务中，您将修改称为**操作**的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="fe6f1-262">操作负责处理 URL 请求，并确定应发送回调用 URL 的浏览器或用户的内容。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="fe6f1-263">**StoreController**类已经有了**Index**方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="fe6f1-264">稍后将在本实验室中使用它来实现列出音乐商店所有流派的页面。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="fe6f1-265">现在，只需将**Index**方法替换为以下代码，即可从 Store （）&quot;返回字符串 &quot;Hello：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="fe6f1-266">（代码段- *ASP.NET MVC 4 基础-Buildingappswithcachingservice-ex2-getproducts latency-cs StoreController Index*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="fe6f1-267">添加**浏览**和**详细信息**方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="fe6f1-268">为此，请将以下代码添加到**StoreController**：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="fe6f1-269">（代码段- *ASP.NET MVC 4 基础-Buildingappswithcachingservice-ex2-getproducts latency-cs StoreController BrowseAndDetails*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="fe6f1-270">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="fe6f1-271">在此任务中，你将在 web 浏览器中尝试应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="fe6f1-272">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-273">项目在**主页**中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="fe6f1-274">更改 URL 以验证每个操作的实现。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="fe6f1-275">**/Store**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-275">**/Store**.</span></span> <span data-ttu-id="fe6f1-276">你将看到 **&quot;Hello From Store （）&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="fe6f1-277">**/Store/Browse**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-277">**/Store/Browse**.</span></span> <span data-ttu-id="fe6f1-278">你将看到 **&quot;Hello From Store. Browse （）&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="fe6f1-279">**/Store/Details**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-279">**/Store/Details**.</span></span> <span data-ttu-id="fe6f1-280">你将看到 **&quot;Hello From Store. Details （）&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="fe6f1-281">![浏览 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "浏览 StoreBrowse")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="fe6f1-282">*浏览/Store/Browse*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="fe6f1-283">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="fe6f1-284">练习3：向控制器传递参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="fe6f1-285">到现在为止，您已经从控制器返回常量字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="fe6f1-286">在本练习中，您将学习如何使用 URL 和 querystring 将参数传递给控制器，然后使方法操作使用文本响应浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="fe6f1-287">任务 1-将流派参数添加到 StoreController</span><span class="sxs-lookup"><span data-stu-id="fe6f1-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="fe6f1-288">在此任务中，您将使用**查询字符串**将参数发送到**StoreController**中的**Browse**操作方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="fe6f1-289">如果尚未打开，请启动**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="fe6f1-290">在 "**文件**" 菜单中，选择 "**打开项目**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="fe6f1-291">在 "打开项目" 对话框中，浏览到**Source\Ex03-PassingParametersToAController\Begin**，选择 "**开始**"，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="fe6f1-292">或者，您也可以继续使用在完成上一练习后获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="fe6f1-293">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fe6f1-294">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fe6f1-295">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fe6f1-296">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fe6f1-297">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fe6f1-298">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fe6f1-299">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fe6f1-300">打开**StoreController**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-300">Open **StoreController** class.</span></span> <span data-ttu-id="fe6f1-301">为此，请在 "**解决方案资源管理器**中，展开"**控制器**"文件夹，然后双击" **StoreController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="fe6f1-302">更改**Browse**方法，并添加一个字符串参数来请求特定的流派。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="fe6f1-303">调用时，ASP.NET MVC 会自动将名为 "**流派**" 的任何 querystring 或窗体 post 参数传递到此操作方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="fe6f1-304">为此，请将**Browse**方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="fe6f1-305">（代码段- *ASP.NET MVC 4 基础-Section-cs StoreController BrowseMethod*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="fe6f1-306">你使用的是**Httputility.javascriptstringencode server.htmlencode**实用工具方法，以防止用户使用/Store/Browse 之类的链接将 Javascript 注入到视图中 **？流派 =&lt;脚本&gt;window。 location = "[http://hackersite.com](http://hackersite.com)"&lt;/script&gt;** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="fe6f1-307">有关进一步说明，请访问[此 msdn 文章](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="fe6f1-308">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="fe6f1-309">在此任务中，你将在 web 浏览器中试用应用程序并使用**流派**参数。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="fe6f1-310">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-311">项目在**主页**中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="fe6f1-312">将 URL 更改为 */Store/Browse？流派 = Disco*验证操作是否收到流派参数。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="fe6f1-313">![浏览 StoreBrowseGenre = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "浏览 StoreBrowseGenre = Disco")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="fe6f1-314">*浏览/Store/Browse？流派 = Disco*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="fe6f1-315">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="fe6f1-316">任务 3-添加嵌入在 URL 中的 Id 参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="fe6f1-317">在此任务中，你将使用**URL**将**Id**参数传递给**StoreController**的**详细信息**操作方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="fe6f1-318">ASP.NET MVC 的默认路由约定是将操作方法名称后面的 URL 段视为名为**Id**的参数。如果操作方法包含名为 Id 的参数，则 ASP.NET MVC 会自动将 URL 段作为参数传递给你。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="fe6f1-319">在 URL**存储/详细信息/5**中， **Id**将解释为**5**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="fe6f1-320">更改**StoreController**的**详细信息**方法，添加一个名为**id**的**int**参数。为此，请将**详细信息**方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="fe6f1-321">（代码段- *ASP.NET MVC 4 基础-Section-cs StoreController DetailsMethod*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="fe6f1-322">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="fe6f1-323">在此任务中，你将在 web 浏览器中试用应用程序并使用**Id**参数。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="fe6f1-324">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-325">项目在**主页**中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="fe6f1-326">将 URL 更改为 " */Store/Details/5* " 以验证操作是否收到 id 参数。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="fe6f1-327">![浏览 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "浏览 StoreDetails5")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="fe6f1-328">*浏览/Store/Details/5*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="fe6f1-329">练习4：创建视图</span><span class="sxs-lookup"><span data-stu-id="fe6f1-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="fe6f1-330">到目前为止，您已经从控制器操作返回了字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="fe6f1-331">尽管这是了解控制器工作方式的有用方法，但并不是实际的 Web 应用程序的构建方式。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="fe6f1-332">视图是提供更好的方法，可让你使用模板文件在浏览器中生成 HTML。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="fe6f1-333">在本练习中，您将学习如何添加布局母版页，以便为常见 HTML 内容设置模板、用于增强网站外观的样式表，以及用于使 HomeController 返回 HTML 的视图模板。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="fe6f1-334">任务 1-修改文件 \_layout</span><span class="sxs-lookup"><span data-stu-id="fe6f1-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="fe6f1-335">文件 **~/Views/Shared/\_layout**允许您设置一个模板，以便在整个网站中使用通用 HTML。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="fe6f1-336">在此任务中，您将添加一个具有公共标题的布局母版页，其中包含指向主页和存储区的链接。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="fe6f1-337">如果尚未打开，请启动**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="fe6f1-338">在 "**文件**" 菜单中，选择 "**打开项目**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="fe6f1-339">在 "打开项目" 对话框中，浏览到**Source\Ex04-CreatingAView\Begin**，选择 "**开始**"，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="fe6f1-340">或者，您也可以继续使用在完成上一练习后获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="fe6f1-341">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fe6f1-342">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fe6f1-343">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fe6f1-344">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fe6f1-345">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fe6f1-346">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fe6f1-347">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fe6f1-348">文件<strong>\_layout</strong>包含网站上所有页的 HTML 容器布局。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="fe6f1-349">它包括 HTML 响应的<strong>&lt;html&gt;</strong>元素，以及<strong>&lt;head&gt;</strong>和<strong>&lt;正文&gt;</strong>元素。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="fe6f1-350">HTML 正文中的<strong>@RenderBody（）</strong>标识查看模板将能够用动态内容填充的区域。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="fe6f1-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="fe6f1-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="fe6f1-352">添加一个公共标题，其中包含指向主页的链接和网站中所有页面上的存储区。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="fe6f1-353">为此，请在下面 &lt;body&gt; 语句中添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="fe6f1-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="fe6f1-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="fe6f1-355">包含一个 div，用于呈现每个页面的正文部分。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="fe6f1-356">将<strong>@RenderBody（）</strong>替换为以下突出显示的代码C#：（）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="fe6f1-357">您知道吗？</span><span class="sxs-lookup"><span data-stu-id="fe6f1-357">Did you know?</span></span> <span data-ttu-id="fe6f1-358">Visual Studio 2012 提供了一些代码段，使你可以轻松地将常用代码添加到 HTML、代码文件等中！</span><span class="sxs-lookup"><span data-stu-id="fe6f1-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="fe6f1-359">通过键入 **&lt;div&gt;** 并按**tab**两次以插入完整的**div**标记来尝试此方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="fe6f1-360">任务 2-添加 CSS 样式表</span><span class="sxs-lookup"><span data-stu-id="fe6f1-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="fe6f1-361">空项目模板包含一个非常简单的 CSS 文件，其中只包含用于显示基本窗体和验证消息的样式。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="fe6f1-362">您将使用其他 CSS 和图像（可能由设计器提供）来增强网站的外观。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="fe6f1-363">在此任务中，您将添加 CSS 样式表以定义站点的样式。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="fe6f1-364">此实验室的**Source\Assets\Content**文件夹中包括了 CSS 文件和映像。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="fe6f1-365">若要将它们添加到应用程序，请将其内容从**Windows 资源管理器**窗口拖到 Visual Studio Express for Web 中的**解决方案资源管理器**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="fe6f1-366">![拖动样式内容](aspnet-mvc-4-fundamentals/_static/image12.png "拖动样式内容")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="fe6f1-367">*拖动样式内容*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="fe6f1-368">将显示一个警告对话框，要求确认是否替换**Site .css**文件和一些现有的图像。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="fe6f1-369">选中 "**应用到所有项**"，然后单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="fe6f1-370">任务 3-添加视图模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="fe6f1-371">在此任务中，你将添加一个视图模板以生成将使用在本练习中添加的布局母版页和 CSS 的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="fe6f1-372">若要在浏览网站的主页时使用视图模板，首先需要指出， **HomeController Index**方法将返回一个**视图**，而不是返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="fe6f1-373">打开**HomeController**类并更改其**Index**方法以返回**ActionResult**，并使其返回**View （）** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="fe6f1-374">（代码段- *ASP.NET MVC 4 基础-Ex4 HomeController Index*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="fe6f1-375">现在，需要添加相应的视图模板。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="fe6f1-376">为此，请在**索引**操作方法中**右键单击**，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="fe6f1-377">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="fe6f1-378">![从 Index 方法中添加视图](aspnet-mvc-4-fundamentals/_static/image13.png "从 Index 方法中添加视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="fe6f1-379">*从 Index 方法中添加视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="fe6f1-380">将显示 "**添加视图**" 对话框以生成视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="fe6f1-381">默认情况下，此对话框预先填充视图模板的名称，使其与将使用它的操作方法匹配。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="fe6f1-382">因为你在 HomeController 中使用了**索引**操作方法中的 "**添加视图**" 上下文菜单，所以 "**添加视图**" 对话框中的默认视图名称为 "索引"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="fe6f1-383">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-383">Click **Add**.</span></span>

    <span data-ttu-id="fe6f1-384">![添加视图对话框](aspnet-mvc-4-fundamentals/_static/image14.png "添加视图对话框")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="fe6f1-385">*添加视图对话框*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="fe6f1-386">Visual Studio 将在**Views\Home**文件夹中生成一个**索引. cshtml**视图模板，然后将其打开。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="fe6f1-387">![已创建主索引视图](aspnet-mvc-4-fundamentals/_static/image15.png "已创建主索引视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="fe6f1-388">*已创建主索引视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-389">**索引 cshtml**文件的名称和位置与默认的 ASP.NET MVC 命名约定相关。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="fe6f1-390">文件夹 \Views\**home*\* 与控制器名称（**home**控制器）匹配。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="fe6f1-391">视图模板名称（**Index**）匹配将显示视图的控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="fe6f1-392">这样，当使用此命名约定返回视图时，ASP.NET MVC 就不必显式指定视图模板的名称或位置。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="fe6f1-393">生成的视图模板基于之前定义的 **\_布局 cshtml**模板。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="fe6f1-394">将 ViewBag 属性更新为**home**，将主要内容更改为 **"** 主页"，如下面的代码所示：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="fe6f1-395">在解决方案资源管理器中选择 " **MvcMusicStore**项目"，并按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="fe6f1-396">任务4：验证</span><span class="sxs-lookup"><span data-stu-id="fe6f1-396">Task 4: Verification</span></span>

<span data-ttu-id="fe6f1-397">若要验证是否正确执行了上一练习中的所有步骤，请按以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="fe6f1-398">在浏览器中打开应用程序时，应注意以下事项：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="fe6f1-399">HomeController 的索引操作方法会找到并显示 **\Views\Home\Index.cshtml**视图模板，即使代码调用了**返回视图（）** ，因为视图模板遵循了标准命名约定。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="fe6f1-400">"主页" 页显示在 **\Views\Home\Index.cshtml**视图模板内定义的欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="fe6f1-401">主页使用 **\_layout**模板，因此欢迎消息包含在标准网站 HTML 布局中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="fe6f1-402">![使用定义的 LayoutPage 和样式的主索引视图](aspnet-mvc-4-fundamentals/_static/image16.png "使用定义的 LayoutPage 和样式的主索引视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="fe6f1-403">*使用定义的 LayoutPage 和样式的主索引视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="fe6f1-404">练习5：创建视图模型</span><span class="sxs-lookup"><span data-stu-id="fe6f1-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="fe6f1-405">到目前为止，你已使视图显示了硬编码的 HTML，但为了创建动态 web 应用程序，视图模板应接收来自控制器的信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="fe6f1-406">用于此目的的一种常见方法是**ViewModel**模式，该模式允许控制器打包生成相应 HTML 响应所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="fe6f1-407">在此练习中，您将学习如何创建 ViewModel 类并添加所需的属性：存储中的流派数量以及这些流派的列表。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="fe6f1-408">您还将更新 StoreController 以使用创建的 ViewModel，最后，您将创建一个新的视图模板，该模板将在页面中显示所述的属性。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="fe6f1-409">任务 1-创建 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="fe6f1-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="fe6f1-410">在此任务中，你将创建一个 ViewModel 类，该类将实现商店流派列表方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="fe6f1-411">如果尚未打开，请启动**VS Express for Web**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="fe6f1-412">在 "**文件**" 菜单中，选择 "**打开项目**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="fe6f1-413">在 "打开项目" 对话框中，浏览到**Source\Ex05-CreatingAViewModel\Begin**，选择 "**开始**"，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="fe6f1-414">或者，您也可以继续使用在完成上一练习后获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="fe6f1-415">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fe6f1-416">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fe6f1-417">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fe6f1-418">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fe6f1-419">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fe6f1-420">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fe6f1-421">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fe6f1-422">创建用于保存 ViewModel 的**viewmodel**文件夹。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="fe6f1-423">为此，请右键单击顶级**MvcMusicStore**项目，选择 "**添加**"，然后选择 "**新建文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="fe6f1-424">![添加新文件夹](aspnet-mvc-4-fundamentals/_static/image17.png "添加新文件夹")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="fe6f1-425">*添加新文件夹*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="fe6f1-426">将文件夹命名为*viewmodel*。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="fe6f1-427">![解决方案资源管理器中的 Viewmodel 文件夹](aspnet-mvc-4-fundamentals/_static/image18.png "解决方案资源管理器中的 Viewmodel 文件夹")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="fe6f1-428">*解决方案资源管理器中的 Viewmodel 文件夹*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="fe6f1-429">创建**ViewModel**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="fe6f1-430">为此，请右键单击最近创建的**viewmodel**文件夹，选择 "**添加**"，然后选择 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="fe6f1-431">在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*StoreIndexViewModel.cs*，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="fe6f1-432">![添加新类](aspnet-mvc-4-fundamentals/_static/image19.png "添加新类")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="fe6f1-433">*添加新类*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-433">*Adding a new Class*</span></span>

    <span data-ttu-id="fe6f1-434">![创建 StoreIndexViewModel 类](aspnet-mvc-4-fundamentals/_static/image20.png "创建 StoreIndexViewModel 类")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="fe6f1-435">*创建 StoreIndexViewModel 类*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="fe6f1-436">任务 2-将属性添加到 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="fe6f1-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="fe6f1-437">需要将 StoreController 中的两个参数传递给视图模板，才能生成所需的 HTML 响应：存储中的流派数量和这些流派的列表。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="fe6f1-438">在此任务中，您将这两个属性添加到**StoreIndexViewModel**类： **NumberOfGenres** （整数）和**流派**（字符串列表）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="fe6f1-439">将**NumberOfGenres**和**流派**属性添加到**StoreIndexViewModel**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="fe6f1-440">为此，请向类定义添加以下两行：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="fe6f1-441">（代码段- *ASP.NET MVC 4 基础-Ex5 StoreIndexViewModel properties*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="fe6f1-442">**{Get; set;}** 表示法利用了C#自动实现的属性功能。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="fe6f1-443">它提供属性的优点，而无需声明支持字段。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="fe6f1-444">任务 3-将 StoreController 更新为使用 StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="fe6f1-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="fe6f1-445">**StoreIndexViewModel**类将从**StoreController**的**Index**方法传递到视图模板所需的信息封装为生成响应。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="fe6f1-446">在此任务中，你将更新**StoreController**以使用**StoreIndexViewModel**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="fe6f1-447">打开**StoreController**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="fe6f1-448">![打开 StoreController 类](aspnet-mvc-4-fundamentals/_static/image21.png "打开 StoreController 类")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="fe6f1-449">*打开 StoreController 类*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="fe6f1-450">若要使用**StoreController**中的**StoreIndexViewModel**类，请在**StoreController**代码的顶部添加以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="fe6f1-451">（代码段- *ASP.NET MVC 4 基础-Ex5 StoreIndexViewModel Using viewmodel*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="fe6f1-452">更改**StoreController**的**索引**操作方法，使其创建并填充**StoreIndexViewModel**对象，然后将其传递给视图模板以生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-453">在实验室 &quot;ASP.NET MVC 模型和数据访问&quot; 您将编写用于从数据库检索存储流派列表的代码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="fe6f1-454">在下面的代码中，将创建将填充**StoreIndexViewModel**的虚拟数据流派的**列表**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="fe6f1-455">创建并设置**StoreIndexViewModel**对象后，它将作为参数传递给**视图**方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="fe6f1-456">这表示视图模板将使用该对象来生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="fe6f1-457">将**Index**方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="fe6f1-458">（代码段- *ASP.NET MVC 4 基础-Ex5 StoreController Index 方法*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="fe6f1-459">如果不熟悉C#，则可以假设使用**var**表示**viewModel**变量为后期绑定。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="fe6f1-460">这不是正确的- C#编译器将根据分配给变量的内容来使用类型推理来确定**viewModel**类型是否为**StoreIndexViewModel**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="fe6f1-461">此外，通过将本地**viewModel**变量编译为**StoreIndexViewModel**类型，可以获取编译时检查和 Visual Studio 代码编辑器支持。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="fe6f1-462">任务 4-创建使用 StoreIndexViewModel 的视图模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="fe6f1-463">在此任务中，您将创建一个视图模板，该模板将使用从控制器传递的 StoreIndexViewModel 对象来显示流派列表。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="fe6f1-464">在创建新的视图模板之前，让我们生成项目，以便 "**添加视图" 对话框**了解**StoreIndexViewModel**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="fe6f1-465">通过选择 "**生成**" 菜单项生成项目，然后**生成 MvcMusicStore**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="fe6f1-466">![生成项目](aspnet-mvc-4-fundamentals/_static/image22.png "生成项目")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="fe6f1-467">*生成项目*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-467">*Building the project*</span></span>
2. <span data-ttu-id="fe6f1-468">创建新的视图模板。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-468">Create a new View template.</span></span> <span data-ttu-id="fe6f1-469">为此，请在**索引**方法中右键单击，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="fe6f1-470">![添加视图](aspnet-mvc-4-fundamentals/_static/image23.png "添加视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="fe6f1-471">*添加视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-471">*Adding a View*</span></span>
3. <span data-ttu-id="fe6f1-472">由于 "**添加视图" 对话框**是从**StoreController**调用的，因此它将在默认情况下添加到 **\Views\Store\Index.cshtml**文件中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="fe6f1-473">选中 "**创建强类型视图**" 复选框，然后选择 " **StoreIndexViewModel** " 作为**模型类**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="fe6f1-474">此外，请确保所选的视图引擎为**Razor**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="fe6f1-475">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-475">Click **Add**.</span></span>

    <span data-ttu-id="fe6f1-476">![添加视图对话框](aspnet-mvc-4-fundamentals/_static/image24.png "添加视图对话框")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="fe6f1-477">*添加视图对话框*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-477">*Add View Dialog*</span></span>

    <span data-ttu-id="fe6f1-478">将创建并打开 " **\Views\Store\Index.cshtml** " 视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="fe6f1-479">根据在上一步中提供给 "**添加视图**" 对话框的信息，视图模板需要**StoreIndexViewModel**实例作为要用于生成 HTML 响应的数据。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="fe6f1-480">你会注意到，模板在中C#继承 `ViewPage<musicstore.viewmodels.storeindexviewmodel>`。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="fe6f1-481">任务 5-更新视图模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="fe6f1-482">在此任务中，您将更新在上一任务中创建的视图模板以检索流派的数目及其在页面中的名称。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="fe6f1-483">您将使用 @ 语法（通常称为 &quot;代码片段&quot;）来执行视图模板中的代码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="fe6f1-484">在**索引的 cshtml**文件中 **，将其**代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="fe6f1-485">循环遍历**StoreIndexViewModel**中的流派列表，并使用**FOREACH**循环创建 HTML **&lt;ul&gt;** 列表。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="fe6f1-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="fe6f1-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="fe6f1-487">按**F5**运行应用程序并浏览 **/Store**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="fe6f1-488">你将看到在**StoreIndexViewModel**对象中**传递给视图**模板的流派列表。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="fe6f1-489">![显示流派列表的视图](aspnet-mvc-4-fundamentals/_static/image26.png "显示流派列表的视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="fe6f1-490">*显示流派列表的视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="fe6f1-491">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="fe6f1-492">练习6：在视图中使用参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="fe6f1-493">在练习3中，你学习了如何将参数传递给控制器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="fe6f1-494">在此练习中，您将学习如何在视图模板中使用这些参数。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="fe6f1-495">为此，你将首先引入有助于管理你的数据和域逻辑的类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="fe6f1-496">此外，你将了解如何创建指向 ASP.NET MVC 应用程序内的页面的链接，而无需担心 URL 路径编码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="fe6f1-497">任务 1-添加模型类</span><span class="sxs-lookup"><span data-stu-id="fe6f1-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="fe6f1-498">与 Viewmodel 不同，只是为了将信息从控制器传递到视图，而生成的模型类包含和管理数据和域逻辑。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="fe6f1-499">在此任务中，您将添加两个模型类来表示这些概念：**流派**和**唱片集**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="fe6f1-500">如果尚未打开，请启动**VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="fe6f1-501">在 "**文件**" 菜单中，选择 "**打开项目**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="fe6f1-502">在 "打开项目" 对话框中，浏览到**Source\Ex06-UsingParametersInView\Begin**，选择 "**开始**"，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="fe6f1-503">或者，您也可以继续使用在完成上一练习后获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="fe6f1-504">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="fe6f1-505">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="fe6f1-506">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="fe6f1-507">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="fe6f1-508">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="fe6f1-509">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="fe6f1-510">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="fe6f1-511">添加**流派**模型类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="fe6f1-512">为此，请在**解决方案资源管理器**中右键单击 "**模型**" 文件夹，选择 "**添加**"，然后选择 "**新建项**" 选项。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="fe6f1-513">在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*Genre.cs*，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="fe6f1-514">![添加类](aspnet-mvc-4-fundamentals/_static/image27.png "添加类")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="fe6f1-515">*添加新项*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-515">*Adding a new item*</span></span>

    <span data-ttu-id="fe6f1-516">![添加流派模型类](aspnet-mvc-4-fundamentals/_static/image28.png "添加流派模型类")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="fe6f1-517">*添加流派模型类*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="fe6f1-518">向流派类添加**Name**属性。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="fe6f1-519">为此，请添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-519">To do this, add the following code:</span></span>

    <span data-ttu-id="fe6f1-520">（代码段- *ASP.NET MVC 4 基础-Ex6 流派*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="fe6f1-521">按照与前面相同的过程操作，添加一个**唱片集**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="fe6f1-522">为此，请在**解决方案资源管理器**中右键单击 "**模型**" 文件夹，选择 "**添加**"，然后选择 "**新建项**" 选项。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="fe6f1-523">在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*Album.cs*，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="fe6f1-524">向唱片集类添加两个属性： "**流派**" 和 "**标题**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="fe6f1-525">为此，请添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-525">To do this, add the following code:</span></span>

    <span data-ttu-id="fe6f1-526">（代码段- *ASP.NET MVC 4 基础-Ex6 唱片集*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="fe6f1-527">任务 2-添加 StoreBrowseViewModel</span><span class="sxs-lookup"><span data-stu-id="fe6f1-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="fe6f1-528">此任务中将使用**StoreBrowseViewModel**来显示与所选流派匹配的唱片集。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="fe6f1-529">在此任务中，您将创建此类，然后添加两个属性来处理**流派**及其**唱片集**的列表。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="fe6f1-530">添加**StoreBrowseViewModel**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="fe6f1-531">为此，请在**解决方案资源管理器**中右键单击**viewmodel**文件夹，选择 "**添加**"，然后选择 "**新建项**" 选项。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="fe6f1-532">在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*StoreBrowseViewModel.cs*，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="fe6f1-533">在**StoreBrowseViewModel**类中添加对模型的引用。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="fe6f1-534">为此，请使用命名空间添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="fe6f1-535">（代码段- *ASP.NET MVC 4 基础-Ex6 UsingModel*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="fe6f1-536">将两个属性添加到**StoreBrowseViewModel**类：**流派**和**唱片集**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="fe6f1-537">为此，请添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-537">To do this, add the following code:</span></span>

    <span data-ttu-id="fe6f1-538">（代码段- *ASP.NET MVC 4 基础-Ex6 ModelProperties*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="fe6f1-539">什么是**list&lt;唱片集&gt;** ？：此定义使用**列表&lt;t&gt;** 类型，其中**t**限制此**列表**的元素所属的类型，在此示例中为**唱片集**（或其任意后代）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="fe6f1-540">此功能用于设计类和方法，以延迟一种或多种类型的规范，直到客户端代码声明并实例化类或方法，这一功能C#称为**泛型**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="fe6f1-541">**List&lt;t&gt;** 是**ArrayList**类型的泛型等效项，并在**system.web**命名空间中可用。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="fe6f1-542">使用**泛型**的优点之一是，由于指定了类型，因此您无需注意类型检查操作，例如将元素强制转换为**影集**，就像对**ArrayList**进行操作一样。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="fe6f1-543">任务 3-在 StoreController 中使用 New ViewModel</span><span class="sxs-lookup"><span data-stu-id="fe6f1-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="fe6f1-544">在此任务中，您将修改**StoreController**的**浏览**和**详细信息**操作方法以使用新的**StoreBrowseViewModel**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="fe6f1-545">在**StoreController**类中添加对模型文件夹的引用。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="fe6f1-546">为此，请展开**解决方案资源管理器**中的 "**控制器**" 文件夹，然后打开**StoreController**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="fe6f1-547">然后添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-547">Then add the following code:</span></span>

    <span data-ttu-id="fe6f1-548">（代码段- *ASP.NET MVC 4 基础-Ex6 UsingModelInController*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="fe6f1-549">替换**浏览**操作方法以使用**StoreViewBrowseController**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="fe6f1-550">您将创建一个流派和两个包含虚拟数据的新的唱集对象（在下一个动手实验中，您将使用数据库中的真实数据）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="fe6f1-551">为此，请将**Browse**方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="fe6f1-552">（代码段- *ASP.NET MVC 4 基础-Ex6 BrowseMethod*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="fe6f1-553">替换**详细信息**操作方法以使用**StoreViewBrowseController**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="fe6f1-554">您将创建一个新的**唱片集**对象以返回到**视图**中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="fe6f1-555">为此，请将**详细信息**方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="fe6f1-556">（代码段- *ASP.NET MVC 4 基础-Ex6 DetailsMethod*）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="fe6f1-557">任务 4-添加浏览视图模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="fe6f1-558">在此任务中，您将添加一个**浏览**视图以显示针对特定流派找到的唱集。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="fe6f1-559">在创建新的视图模板之前，应生成项目，以便 "**添加视图**" 对话框知道要使用的**ViewModel**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="fe6f1-560">通过选择 "**生成**" 菜单项生成项目，然后**生成 MvcMusicStore**。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="fe6f1-561">添加 "**浏览**" 视图。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-561">Add a **Browse** View.</span></span> <span data-ttu-id="fe6f1-562">为此，请在**StoreController**的 "**浏览**操作" 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="fe6f1-563">在 "**添加视图**" 对话框中，验证视图名称是否为 "**浏览**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="fe6f1-564">选中 "**创建强类型视图**" 复选框，然后从 "**模型类**" 下拉列表中选择 " **StoreBrowseViewModel** "。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="fe6f1-565">让其他字段保留其默认值。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="fe6f1-566">然后单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-566">Then click **Add**.</span></span>

    <span data-ttu-id="fe6f1-567">![添加浏览视图](aspnet-mvc-4-fundamentals/_static/image29.png "添加浏览视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="fe6f1-568">*添加浏览视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="fe6f1-569">修改**Browse**以显示流派的信息，访问传递到视图模板的**StoreBrowseViewModel**对象。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="fe6f1-570">为此，请将内容替换为以下内容：（C#）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="fe6f1-571">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="fe6f1-572">在此任务中，您将测试**browse**方法是否从**浏览**方法操作检索相册。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="fe6f1-573">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-574">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-574">The project starts in the Home page.</span></span> <span data-ttu-id="fe6f1-575">将 URL 更改为 **/Store/Browse？流派 = Disco**验证操作是否返回了两个唱片集。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="fe6f1-576">![浏览存储 Disco 唱集](aspnet-mvc-4-fundamentals/_static/image30.png "浏览存储 Disco 唱集")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="fe6f1-577">*浏览存储 Disco 唱集*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="fe6f1-578">任务 6-显示有关特定唱片集的信息</span><span class="sxs-lookup"><span data-stu-id="fe6f1-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="fe6f1-579">在此任务中，您将实现 "**存储/详细信息**" 视图以显示有关特定唱片集的信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="fe6f1-580">在此动手实验中，您将显示的有关唱片集的所有内容都已包含在**视图**模板中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="fe6f1-581">因此，你将使用当前的**StoreBrowseViewModel**模板将唱片集传递给它，而不是创建**StoreDetailsViewModel**类。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="fe6f1-582">如果需要，请关闭浏览器以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="fe6f1-583">为**StoreController**的**详细信息**操作方法添加新的**详细信息**视图。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="fe6f1-584">为此，请在**StoreController**类中右键单击**详细信息**方法，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="fe6f1-585">在 "**添加视图**" 对话框中，验证**视图名称**是否为 "**详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="fe6f1-586">选中 "**创建强类型视图**" 复选框，然后从 "**模型类**" 下拉框中选择 "**唱片集**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="fe6f1-587">让其他字段保留其默认值。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="fe6f1-588">然后单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-588">Then click **Add**.</span></span> <span data-ttu-id="fe6f1-589">这会创建并打开 **\Views\Store\Details.cshtml**文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="fe6f1-590">![添加详细信息视图](aspnet-mvc-4-fundamentals/_static/image31.png "添加详细信息视图")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="fe6f1-591">*添加详细信息视图*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="fe6f1-592">修改**详细信息 cshtml**文件以显示唱片集的信息，并访问传递到视图模板的**唱片集**对象。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="fe6f1-593">为此，请将内容替换为以下内容：（C#）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="fe6f1-594">任务 7-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="fe6f1-595">在此任务中，您将测试**详细**信息视图是否从**详细信息操作**方法中检索唱片集的信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="fe6f1-596">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-597">项目在**主页**中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="fe6f1-598">将 URL 更改为 " **/Store/Details/5** " 以验证唱片集的信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="fe6f1-599">![浏览唱片集详细信息](aspnet-mvc-4-fundamentals/_static/image32.png "浏览唱片集详细信息")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="fe6f1-600">*浏览唱片集的详细信息*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="fe6f1-601">任务 8-在页面之间添加链接</span><span class="sxs-lookup"><span data-stu-id="fe6f1-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="fe6f1-602">在此任务中，你将在 "应用商店" 视图中添加一个链接，使每个流派名称中有一个链接到相应的 **/Store/Browse** URL。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="fe6f1-603">这样一来，当您单击某个流派（例如**disco**）时，它将导航到 **/Store/Browse？流派 = Disco** URL。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="fe6f1-604">如果需要，请关闭浏览器以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="fe6f1-605">更新 "**索引**" 页以添加指向**浏览**页的链接。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="fe6f1-606">为此，请在**解决方案资源管理器**展开**Views**文件夹，再展开 "**存储**" 文件夹，然后双击 "**索引**" 页。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="fe6f1-607">添加指向浏览视图的链接，指示所选流派。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="fe6f1-608">为此，请将以下突出显示的代码替换 **&lt;li&gt;** 标记中：C#（）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="fe6f1-609">另一种方法是直接链接到页面，代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="fe6f1-610">&lt;href =&quot;/Store/Browse？流派 =@genreName&quot;&gt;@genreName/a &lt;&gt;</span><span class="sxs-lookup"><span data-stu-id="fe6f1-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="fe6f1-611">尽管此方法有效，但它依赖于硬编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="fe6f1-612">如果以后重命名控制器，则必须手动更改此指令。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="fe6f1-613">更好的替代方法是使用**HTML 帮助器**方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="fe6f1-614">ASP.NET MVC 包含可用于此类任务的 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="fe6f1-615">使用**html.actionlink （）** helper 方法，可以轻松地生成 html **&lt;&gt;** 链接，确保 url 路径正确地进行 url 编码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="fe6f1-616">Html.actionlink 有多个重载。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="fe6f1-617">在本练习中，您将使用一个带有三个参数的：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="fe6f1-618">链接文本，将显示流派名称</span><span class="sxs-lookup"><span data-stu-id="fe6f1-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="fe6f1-619">控制器操作名称（**浏览**）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="fe6f1-620">路由参数值，同时指定名称（**流派**）和值（**流派名称**）</span><span class="sxs-lookup"><span data-stu-id="fe6f1-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="fe6f1-621">任务 9-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="fe6f1-622">在此任务中，将测试是否显示每个流派，并提供指向相应 **/Store/Browse** URL 的链接。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="fe6f1-623">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-624">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-624">The project starts in the Home page.</span></span> <span data-ttu-id="fe6f1-625">将 URL 更改为 " **/Store** " 以验证每个流派是否链接到相应的 **/Store/Browse** URL。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="fe6f1-626">![浏览具有浏览页链接的流派](aspnet-mvc-4-fundamentals/_static/image33.png "浏览具有浏览页链接的流派")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="fe6f1-627">*浏览具有浏览页链接的流派*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="fe6f1-628">任务 10-使用动态 ViewModel 集合传递值</span><span class="sxs-lookup"><span data-stu-id="fe6f1-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="fe6f1-629">在此任务中，您将学习一种简单而有效的方法，可在控制器和视图之间传递值，而无需在模型中进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="fe6f1-630">ASP.NET MVC 4 提供 &quot;ViewModel&quot;的集合，可将其分配给任何动态值，也可在控制器和视图中进行访问。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="fe6f1-631">现在，你将使用 ViewBag 动态集合将 &quot;**带有星标&quot; 流派**的列表从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="fe6f1-632">"商店索引" 视图将访问**ViewModel**并显示信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="fe6f1-633">如果需要，请关闭浏览器以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="fe6f1-634">打开**StoreController.cs**并修改**Index**方法，以便在 ViewModel 集合中创建带有星标流派列表：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="fe6f1-635">你还可以使用语法**ViewBag [&quot;带有星标&quot;]** 来访问这些属性。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="fe6f1-636">**&quot;"带有星标"&quot;** 的星形图标包含在此实验室的 " **Source\Assets\Images** " 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="fe6f1-637">若要将该应用程序添加到应用程序，请将其内容从**Windows 资源管理器**窗口拖到 Visual Web Developer Express 中的**解决方案资源管理器**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="fe6f1-638">![向解决方案添加星形图像](aspnet-mvc-4-fundamentals/_static/image34.png "向解决方案添加星形图像")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="fe6f1-639">*向解决方案添加星形图像*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="fe6f1-640">打开 "查看**存储/索引**" 并修改内容。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="fe6f1-641">你将在**ViewBag**集合中读取 &quot;带有星标&quot; 属性，并询问当前流派名称是否在列表中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="fe6f1-642">在这种情况下，你将向流派链接显示一个星形图标。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="fe6f1-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="fe6f1-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="fe6f1-644">任务 11-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="fe6f1-645">在此任务中，您将测试带有星标流派是否显示星形图标。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="fe6f1-646">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="fe6f1-647">项目在**主页**中启动。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="fe6f1-648">将 URL 更改为 " **/Store** " 以验证每个特色流派是否具有 "尊重" 标签：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="fe6f1-649">![浏览具有带有星标元素的流派](aspnet-mvc-4-fundamentals/_static/image35.png "浏览具有带有星标元素的流派")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="fe6f1-650">*浏览具有带有星标元素的流派*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="fe6f1-651">练习7：重叠 ASP.NET MVC 4 新模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="fe6f1-652">在此练习中，你将了解 ASP.NET MVC 4 项目模板中的增强功能，其中介绍了新模板的最相关功能。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="fe6f1-653">任务1：浏览 ASP.NET MVC 4 Internet 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="fe6f1-654">如果尚未打开，请启动**VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="fe6f1-655">选择**文件 |新建 |项目**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="fe6f1-656">在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="fe6f1-657">将项目**命名**为 " *MusicStore* " 并更新**解决方案名称**以*开始*，然后选择一个位置（或保留默认值），然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="fe6f1-658">![创建新的 ASP.NET MVC 4 项目](aspnet-mvc-4-fundamentals/_static/image36.png "创建新的 ASP.NET MVC 4 项目")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="fe6f1-659">*创建新的 ASP.NET MVC 4 项目*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="fe6f1-660">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**" 项目模板，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="fe6f1-661">请注意，可以选择 Razor 或 ASPX 作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="fe6f1-662">![创建新的 ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-fundamentals/_static/image37.png "创建新的 ASP.NET MVC 4 Internet 应用程序")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="fe6f1-663">*创建新的 ASP.NET MVC 4 Internet 应用程序*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-664">ASP.NET MVC 3 中引入了 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="fe6f1-665">其目标是最大程度地减少文件中所需的字符和击键数量，从而实现快速、流畅的编码工作流。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="fe6f1-666">Razor 利用现有C#的/VB （或其他）语言技能，并提供了一个模板标记语法，可实现出色的 HTML 构造工作流。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="fe6f1-667">按**F5**运行解决方案并查看续订的模板。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="fe6f1-668">您可以查看以下功能：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="fe6f1-669">**新式模板**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-669">**Modern-style templates**</span></span>

        <span data-ttu-id="fe6f1-670">这些模板已续订，提供了更新式的样式。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="fe6f1-671">![ASP.NET MVC 4 改变模板](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 改变模板")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="fe6f1-672">*ASP.NET MVC 4 改变模板*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="fe6f1-673">**自适应呈现**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="fe6f1-674">查看调整浏览器窗口的大小，并注意页面布局如何动态适应新的窗口大小。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="fe6f1-675">这些模板使用自适应呈现技术在桌面和移动平台中正确呈现，无需进行任何自定义。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="fe6f1-676">![不同浏览器大小的 ASP.NET MVC 4 项目模板](aspnet-mvc-4-fundamentals/_static/image39.png "不同浏览器大小的 ASP.NET MVC 4 项目模板")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="fe6f1-677">*不同浏览器大小的 ASP.NET MVC 4 项目模板*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="fe6f1-678">关闭浏览器以停止调试器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="fe6f1-679">现在，你可以浏览解决方案并查看项目模板中 ASP.NET MVC 4 引入的一些新功能。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="fe6f1-680">![ASP.NET MVC4-应用程序-项目-模板](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 Internet 应用程序项目模板")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="fe6f1-681">*ASP.NET MVC 4 Internet 应用程序项目模板*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="fe6f1-682">**HTML5 标记**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-682">**HTML5 markup**</span></span>

       <span data-ttu-id="fe6f1-683">浏览模板视图以找出新的主题标记，例如，在**主**文件夹内打开**About。**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="fe6f1-684">![新模板，使用 Razor 和 HTML5 标记](aspnet-mvc-4-fundamentals/_static/image41.png "新模板，使用 Razor 和 HTML5 标记")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="fe6f1-685">*新模板，使用 Razor 和 HTML5 标记*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="fe6f1-686">**包括 JavaScript 库**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="fe6f1-687">**jquery**： jquery 简化了 HTML 文档遍历、事件处理、动画处理和 Ajax 交互。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="fe6f1-688">**JQUERY UI**：此库为基于 JQuery JavaScript 库的底层交互和动画、高级效果和 themeable 小组件提供抽象。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="fe6f1-689">可以在[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中了解 jQuery 和 jquery UI。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="fe6f1-690">**KnockoutJS**： ASP.NET MVC 4 默认模板现在包括**KnockoutJS**，这是一个 javascript MVVM 框架，可让你使用 JavaScript 和 HTML 创建丰富且响应迅速的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="fe6f1-691">与 ASP.NET MVC 3 一样，jQuery 和 jQuery UI 库也包含在 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="fe6f1-692">可在以下链接中获取有关 KnockOutJS 库的详细信息： [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="fe6f1-693">**Modernizr**：此库自动运行，在使用 HTML5 和 CSS3 技术时，使你的网站与旧版浏览器兼容。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="fe6f1-694">可在以下链接中获取有关 Modernizr 库的详细信息： [http://www.modernizr.com/](http://www.modernizr.com/)。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="fe6f1-695">**解决方案中包含的 SimpleMembership**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="fe6f1-696">SimpleMembership 已被设计为以前的 ASP.NET 角色和成员资格提供程序系统的替换。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="fe6f1-697">它具有许多新功能，使开发人员能够更轻松地以更灵活的方式保护网页。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="fe6f1-698">Internet 模板已经设置了几项来集成 SimpleMembership，例如，AccountController 准备使用 OAuthWebSecurity （适用于 OAuth 帐户注册、登录、管理等）和 Web 安全。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="fe6f1-699">![解决方案中包含的 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "解决方案中包含的 SimpleMembership")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="fe6f1-700">*解决方案中包含的 SimpleMembership*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="fe6f1-701">在 MSDN 中查找有关[OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx)的详细信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="fe6f1-702">此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="fe6f1-703">摘要</span><span class="sxs-lookup"><span data-stu-id="fe6f1-703">Summary</span></span>

<span data-ttu-id="fe6f1-704">完成此动手实验后，你已了解 ASP.NET MVC 的基础知识：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="fe6f1-705">MVC 应用程序的核心元素及其交互方式</span><span class="sxs-lookup"><span data-stu-id="fe6f1-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="fe6f1-706">如何创建 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="fe6f1-707">如何添加和配置控制器来处理通过 URL 和 querystring 传递的参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="fe6f1-708">如何添加布局母版页，为常见 HTML 内容设置模板; 用于增强外观的样式表和用于显示 HTML 内容的视图模板</span><span class="sxs-lookup"><span data-stu-id="fe6f1-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="fe6f1-709">如何使用 ViewModel 模式将属性传递给视图模板以显示动态信息</span><span class="sxs-lookup"><span data-stu-id="fe6f1-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="fe6f1-710">如何使用传递给视图模板中的控制器的参数</span><span class="sxs-lookup"><span data-stu-id="fe6f1-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="fe6f1-711">如何将链接添加到 ASP.NET MVC 应用程序内的页面</span><span class="sxs-lookup"><span data-stu-id="fe6f1-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="fe6f1-712">如何在视图中添加和使用动态属性</span><span class="sxs-lookup"><span data-stu-id="fe6f1-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="fe6f1-713">ASP.NET MVC 4 项目模板中的增强功能</span><span class="sxs-lookup"><span data-stu-id="fe6f1-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="fe6f1-714">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="fe6f1-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="fe6f1-715">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="fe6f1-716">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="fe6f1-717">请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="fe6f1-718">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="fe6f1-719">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-719">Click on **Install Now**.</span></span> <span data-ttu-id="fe6f1-720">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="fe6f1-721">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="fe6f1-722">![安装 Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="fe6f1-723">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="fe6f1-724">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="fe6f1-726">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="fe6f1-727">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-727">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="fe6f1-729">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-729">*Installation progress*</span></span>
6. <span data-ttu-id="fe6f1-730">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-730">When the installation completes, click **Finish**.</span></span>

    ![安装完成](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="fe6f1-732">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-732">*Installation completed*</span></span>
7. <span data-ttu-id="fe6f1-733">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="fe6f1-734">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="fe6f1-736">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="fe6f1-737">附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="fe6f1-738">本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="fe6f1-739">任务 1-从 Microsoft Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="fe6f1-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="fe6f1-740">请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-741">借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="fe6f1-742">你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="fe6f1-743">![登录到 Windows Azure 门户](aspnet-mvc-4-fundamentals/_static/image48.png "登录到 Microsoft Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="fe6f1-744">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="fe6f1-745">单击命令栏上的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="fe6f1-746">![创建新网站](aspnet-mvc-4-fundamentals/_static/image49.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="fe6f1-747">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="fe6f1-748">单击 "**计算** | **网站**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="fe6f1-749">然后选择 "**快速创建**" 选项。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="fe6f1-750">为新网站提供可用 URL，并单击 "**创建**网站"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-751">Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="fe6f1-752">使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="fe6f1-753">它不包括设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="fe6f1-754">![使用 "快速创建" 创建新网站](aspnet-mvc-4-fundamentals/_static/image50.png "使用“快速创建”创建新网站")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="fe6f1-755">*使用 "快速创建" 创建新网站*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="fe6f1-756">请**等到新网站创建完毕。**</span><span class="sxs-lookup"><span data-stu-id="fe6f1-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="fe6f1-757">创建网站后，单击 " **URL** " 列下的链接。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="fe6f1-758">检查新网站是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="fe6f1-759">![浏览到新网站](aspnet-mvc-4-fundamentals/_static/image51.png "浏览到新网站")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="fe6f1-760">*浏览到新网站*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="fe6f1-761">![网站正在运行](aspnet-mvc-4-fundamentals/_static/image52.png "网站正在运行")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="fe6f1-762">*网站正在运行*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-762">*Web site running*</span></span>
6. <span data-ttu-id="fe6f1-763">返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="fe6f1-764">![打开网站管理页](aspnet-mvc-4-fundamentals/_static/image53.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="fe6f1-765">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="fe6f1-766">在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-767">*发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="fe6f1-768">发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="fe6f1-769">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="fe6f1-770">![下载网站发布配置文件](aspnet-mvc-4-fundamentals/_static/image54.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="fe6f1-771">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="fe6f1-772">将发布配置文件下载到已知位置。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="fe6f1-773">在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="fe6f1-774">![正在保存发布配置文件](aspnet-mvc-4-fundamentals/_static/image55.png "正在保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="fe6f1-775">*正在保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="fe6f1-776">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="fe6f1-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="fe6f1-777">如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="fe6f1-778">如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="fe6f1-779">你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="fe6f1-780">可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="fe6f1-781">如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="fe6f1-782">记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="fe6f1-783">请不要创建数据库，因为它将在后面的阶段创建。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="fe6f1-784">![SQL 数据库服务器仪表板](aspnet-mvc-4-fundamentals/_static/image56.png "SQL 数据库服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="fe6f1-785">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="fe6f1-786">在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="fe6f1-787">为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](aspnet-mvc-4-fundamentals/_static/image57.png)" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![添加客户端 IP 地址](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="fe6f1-789">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="fe6f1-790">将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="fe6f1-792">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="fe6f1-793">任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="fe6f1-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="fe6f1-794">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="fe6f1-795">在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="fe6f1-796">![发布应用程序](aspnet-mvc-4-fundamentals/_static/image60.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="fe6f1-797">*发布网站*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="fe6f1-798">导入您在第一个任务中保存的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="fe6f1-799">![导入发布配置文件](aspnet-mvc-4-fundamentals/_static/image61.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="fe6f1-800">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="fe6f1-801">单击 "**验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-801">Click **Validate Connection**.</span></span> <span data-ttu-id="fe6f1-802">验证完成后，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe6f1-803">验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="fe6f1-804">![正在验证连接](aspnet-mvc-4-fundamentals/_static/image62.png "正在验证连接")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="fe6f1-805">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-805">*Validating connection*</span></span>
4. <span data-ttu-id="fe6f1-806">在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="fe6f1-807">![Web 部署配置](aspnet-mvc-4-fundamentals/_static/image63.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="fe6f1-808">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="fe6f1-809">按如下所示配置数据库连接：</span><span class="sxs-lookup"><span data-stu-id="fe6f1-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="fe6f1-810">在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="fe6f1-811">在 "**用户名**" 中键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="fe6f1-812">在 "**密码**" 中键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="fe6f1-813">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="fe6f1-814">![正在配置目标连接字符串](aspnet-mvc-4-fundamentals/_static/image64.png "正在配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="fe6f1-815">*正在配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="fe6f1-816">然后单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-816">Then click **OK**.</span></span> <span data-ttu-id="fe6f1-817">系统提示创建数据库时，单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="fe6f1-818">![创建数据库](aspnet-mvc-4-fundamentals/_static/image65.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="fe6f1-819">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-819">*Creating the database*</span></span>
7. <span data-ttu-id="fe6f1-820">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="fe6f1-821">再单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-821">Then click **Next**.</span></span>

    <span data-ttu-id="fe6f1-822">![指向 SQL 数据库的连接字符串](aspnet-mvc-4-fundamentals/_static/image66.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="fe6f1-823">*指向 SQL 数据库的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="fe6f1-824">在 "**预览**" 页上，单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="fe6f1-825">![发布 web 应用程序](aspnet-mvc-4-fundamentals/_static/image67.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="fe6f1-826">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="fe6f1-827">发布过程完成后，您的默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="fe6f1-828">![发布到 Windows Azure 的应用程序](aspnet-mvc-4-fundamentals/_static/image68.png "发布到 Windows Azure 的应用程序")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="fe6f1-829">*发布到 Windows Azure 的应用程序*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="fe6f1-830">附录 C：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="fe6f1-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="fe6f1-831">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="fe6f1-832">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="fe6f1-833">![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-fundamentals/_static/image69.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="fe6f1-834">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="fe6f1-835">***使用键盘添加代码片段（C#仅限）***</span><span class="sxs-lookup"><span data-stu-id="fe6f1-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="fe6f1-836">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="fe6f1-837">开始键入代码片段名称（不含空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="fe6f1-838">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="fe6f1-839">选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="fe6f1-840">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="fe6f1-841">![开始键入代码片段名称](aspnet-mvc-4-fundamentals/_static/image70.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="fe6f1-842">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="fe6f1-843">![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-fundamentals/_static/image71.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="fe6f1-844">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="fe6f1-845">![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-fundamentals/_static/image72.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="fe6f1-846">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="fe6f1-847">***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2.</span><span class="sxs-lookup"><span data-stu-id="fe6f1-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="fe6f1-848">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="fe6f1-849">选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="fe6f1-850">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="fe6f1-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="fe6f1-851">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-fundamentals/_static/image73.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="fe6f1-852">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="fe6f1-853">![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-fundamentals/_static/image74.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="fe6f1-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="fe6f1-854">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="fe6f1-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
