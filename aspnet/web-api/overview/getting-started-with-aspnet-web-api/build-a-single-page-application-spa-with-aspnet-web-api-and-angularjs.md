---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 动手实验：使用 ASP.NET Web API 和 ASP.NET 4.x 构建单页应用程序（SPA）
author: rick-anderson
description: 分步编码：生成包含 ASP.NET Web API 的单页面应用程序（SPA），并 ASP.NET 4.x。
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448760"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="3082c-103">动手实验：使用 ASP.NET Web API 和 node.js 生成单页面应用程序（SPA）</span><span class="sxs-lookup"><span data-stu-id="3082c-103">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>

<span data-ttu-id="3082c-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="3082c-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="3082c-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="3082c-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="3082c-106">此动手实验演示了如何使用 ASP.NET Web API 和 ASP.NET 的 node.js 构建单页面应用程序（SPA）。</span><span class="sxs-lookup"><span data-stu-id="3082c-106">This hands on lab shows you how to build a Single Page Application (SPA) with ASP.NET Web API and Angular.js for ASP.NET 4.x.</span></span>

<span data-ttu-id="3082c-107">在此试验实验室中，你将利用这些技术来实现书呆子测验，这是一个基于 SPA 概念的琐碎内容网站。</span><span class="sxs-lookup"><span data-stu-id="3082c-107">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="3082c-108">首先，通过 ASP.NET Web API 实现服务层，以便公开所需的终结点来检索测验问题并存储答案。</span><span class="sxs-lookup"><span data-stu-id="3082c-108">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="3082c-109">然后，你将使用 AngularJS 和 CSS3 转换效果生成丰富且响应迅速的 UI。</span><span class="sxs-lookup"><span data-stu-id="3082c-109">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>

<span data-ttu-id="3082c-110">在传统 web 应用程序中，客户端（浏览器）通过请求页面来启动与服务器的通信。</span><span class="sxs-lookup"><span data-stu-id="3082c-110">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="3082c-111">服务器随后处理请求，并将页面的 HTML 发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="3082c-111">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="3082c-112">在后续与页面的交互（例如，用户导航到链接或提交包含数据的窗体）时，会将新请求发送到服务器，并再次开始此流：服务器处理请求并将新页发送到浏览器，以响应新操作请求ed。</span><span class="sxs-lookup"><span data-stu-id="3082c-112">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="3082c-113">在单页面应用程序（Spa）中，在初始请求后将整个页面加载到浏览器中，但后续交互会通过 Ajax 请求进行。</span><span class="sxs-lookup"><span data-stu-id="3082c-113">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="3082c-114">这意味着浏览器必须只更新页面中已更改的部分;无需重新加载整个页面。</span><span class="sxs-lookup"><span data-stu-id="3082c-114">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="3082c-115">SPA 方法会减少应用程序响应用户操作所需的时间，从而导致更流畅的体验。</span><span class="sxs-lookup"><span data-stu-id="3082c-115">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="3082c-116">SPA 的体系结构涉及传统 web 应用程序中不存在的某些挑战。</span><span class="sxs-lookup"><span data-stu-id="3082c-116">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="3082c-117">不过，新的技术（如 ASP.NET Web API）、AngularJS 的 JavaScript 框架以及 CSS3 提供的新样式功能使得设计和构建 Spa 变得非常容易。</span><span class="sxs-lookup"><span data-stu-id="3082c-117">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> 
> <span data-ttu-id="3082c-118">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。</span><span class="sxs-lookup"><span data-stu-id="3082c-118">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

## <a name="overview"></a><span data-ttu-id="3082c-119">概述</span><span class="sxs-lookup"><span data-stu-id="3082c-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="3082c-120">目标</span><span class="sxs-lookup"><span data-stu-id="3082c-120">Objectives</span></span>

<span data-ttu-id="3082c-121">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="3082c-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="3082c-122">创建 ASP.NET Web API 服务来发送和接收 JSON 数据</span><span class="sxs-lookup"><span data-stu-id="3082c-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="3082c-123">使用 AngularJS 创建响应式 UI</span><span class="sxs-lookup"><span data-stu-id="3082c-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="3082c-124">利用 CSS3 转换增强 UI 体验</span><span class="sxs-lookup"><span data-stu-id="3082c-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="3082c-125">系统必备</span><span class="sxs-lookup"><span data-stu-id="3082c-125">Prerequisites</span></span>

<span data-ttu-id="3082c-126">完成本动手实验需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="3082c-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="3082c-127">Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="3082c-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="3082c-128">安装</span><span class="sxs-lookup"><span data-stu-id="3082c-128">Setup</span></span>

<span data-ttu-id="3082c-129">若要运行此动手实验中的练习，您需要先设置您的环境。</span><span class="sxs-lookup"><span data-stu-id="3082c-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="3082c-130">打开 Windows 资源管理器并浏览到实验室的**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="3082c-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="3082c-131">右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。</span><span class="sxs-lookup"><span data-stu-id="3082c-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="3082c-132">如果显示了 "用户帐户控制" 对话框，请确认操作以继续。</span><span class="sxs-lookup"><span data-stu-id="3082c-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="3082c-133">确保在运行安装过程之前，您已检查本实验的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="3082c-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="3082c-134">使用代码段</span><span class="sxs-lookup"><span data-stu-id="3082c-134">Using the Code Snippets</span></span>

<span data-ttu-id="3082c-135">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="3082c-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="3082c-136">为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。</span><span class="sxs-lookup"><span data-stu-id="3082c-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="3082c-137">每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。</span><span class="sxs-lookup"><span data-stu-id="3082c-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="3082c-138">请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="3082c-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="3082c-139">在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。</span><span class="sxs-lookup"><span data-stu-id="3082c-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="3082c-140">如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="3082c-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="3082c-141">练习</span><span class="sxs-lookup"><span data-stu-id="3082c-141">Exercises</span></span>

<span data-ttu-id="3082c-142">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="3082c-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="3082c-143">创建 Web API</span><span class="sxs-lookup"><span data-stu-id="3082c-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="3082c-144">创建 SPA 接口</span><span class="sxs-lookup"><span data-stu-id="3082c-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="3082c-145">完成本实验的估计时间： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="3082c-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="3082c-146">首次启动 Visual Studio 时，必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="3082c-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="3082c-147">每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="3082c-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="3082c-148">此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="3082c-149">如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="3082c-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="3082c-150">练习1：创建 Web API</span><span class="sxs-lookup"><span data-stu-id="3082c-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="3082c-151">SPA 的关键部分之一是服务层。</span><span class="sxs-lookup"><span data-stu-id="3082c-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="3082c-152">它负责处理 UI 发送的 Ajax 调用并返回响应该调用的数据。</span><span class="sxs-lookup"><span data-stu-id="3082c-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="3082c-153">检索到的数据应以计算机可读格式显示，以便客户端对其进行分析和使用。</span><span class="sxs-lookup"><span data-stu-id="3082c-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="3082c-154">Web API 框架是 ASP.NET 堆栈的一部分，旨在使实现 HTTP 服务（通常通过 RESTful API 发送和接收 JSON 或 XML 格式的数据）变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="3082c-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="3082c-155">在本练习中，您将创建网站来托管书呆子测验应用程序，然后实现后端服务，以使用 ASP.NET Web API 公开和保存测验数据。</span><span class="sxs-lookup"><span data-stu-id="3082c-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="3082c-156">任务1–创建书呆子测验的初始项目</span><span class="sxs-lookup"><span data-stu-id="3082c-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="3082c-157">在此任务中，您将开始创建一个新的 ASP.NET MVC 项目，该项目支持 ASP.NET Web API 基于 Visual Studio 附带的**一种 ASP.NET**项目类型。</span><span class="sxs-lookup"><span data-stu-id="3082c-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="3082c-158">**一个 ASP.NET**统一了所有 ASP.NET 技术，并为你提供了根据需要进行混合和匹配的选项。</span><span class="sxs-lookup"><span data-stu-id="3082c-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="3082c-159">然后，将添加实体框架的模型类和数据库初始值设定项以插入测验问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-159">You will then add the Entity Framework's model classes and the database initializer to insert the quiz questions.</span></span>

1. <span data-ttu-id="3082c-160">打开 " **Web Visual Studio Express 2013** "，然后选择 "**文件" |新建项目 ...** 启动新解决方案。</span><span class="sxs-lookup"><span data-stu-id="3082c-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="3082c-161">![创建新项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "创建新项目")</span><span class="sxs-lookup"><span data-stu-id="3082c-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="3082c-162">*创建新项目*</span><span class="sxs-lookup"><span data-stu-id="3082c-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="3082c-163">在 "**新建项目**" 对话框中，选择 " **ASP.NET Web 应用程序**"。  **C#** 请确保选中 **.NET Framework 4.5** ，将其命名为*GeekQuiz*，选择一个**位置**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="3082c-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="3082c-164">![创建新的 ASP.NET Web 应用程序项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "创建新的 ASP.NET Web 应用程序项目")</span><span class="sxs-lookup"><span data-stu-id="3082c-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="3082c-165">*创建新的 ASP.NET Web 应用程序项目*</span><span class="sxs-lookup"><span data-stu-id="3082c-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="3082c-166">在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC** " 模板，然后选择 " **Web API** " 选项。</span><span class="sxs-lookup"><span data-stu-id="3082c-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="3082c-167">此外，请确保 "**身份验证**" 选项设置为 "**单个用户帐户**"。</span><span class="sxs-lookup"><span data-stu-id="3082c-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="3082c-168">单击 **“确定”** 继续。</span><span class="sxs-lookup"><span data-stu-id="3082c-168">Click **OK** to continue.</span></span>

    ![使用 MVC 模板创建新项目，包括 Web API 组件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="3082c-170">*使用 MVC 模板创建新项目，包括 Web API 组件*</span><span class="sxs-lookup"><span data-stu-id="3082c-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="3082c-171">在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的 "**模型**" 文件夹，然后选择 "**添加 |现有项 ...**</span><span class="sxs-lookup"><span data-stu-id="3082c-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="3082c-172">![添加现有项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "添加现有项")</span><span class="sxs-lookup"><span data-stu-id="3082c-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="3082c-173">*添加现有项*</span><span class="sxs-lookup"><span data-stu-id="3082c-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="3082c-174">在 "**添加现有项**" 对话框中，导航到 "**源/资产/型号**" 文件夹，然后选择 "所有文件"。</span><span class="sxs-lookup"><span data-stu-id="3082c-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="3082c-175">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="3082c-175">Click **Add**.</span></span>

    <span data-ttu-id="3082c-176">![添加模型资产](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "添加模型资产")</span><span class="sxs-lookup"><span data-stu-id="3082c-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="3082c-177">*添加模型资产*</span><span class="sxs-lookup"><span data-stu-id="3082c-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3082c-178">通过添加这些文件，您将为书呆子测验应用程序添加数据模型、实体框架的数据库上下文和数据库初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="3082c-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="3082c-179">**实体框架（EF）** 是一个对象关系映射器（ORM），使您可以通过使用概念应用程序模型进行编程来创建数据访问应用程序，而无需使用关系存储架构直接编程。</span><span class="sxs-lookup"><span data-stu-id="3082c-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="3082c-180">可在[此处](../../../entity-framework.md)详细了解实体框架。</span><span class="sxs-lookup"><span data-stu-id="3082c-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="3082c-181">下面是刚才添加的类的说明：</span><span class="sxs-lookup"><span data-stu-id="3082c-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="3082c-182">**TriviaOption：** 表示与测验题关联的单个选项</span><span class="sxs-lookup"><span data-stu-id="3082c-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="3082c-183">**TriviaQuestion：** 表示测验题，并通过**options**属性公开关联选项</span><span class="sxs-lookup"><span data-stu-id="3082c-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="3082c-184">**TriviaAnswer：** 表示用户在响应测验问题时选择的选项</span><span class="sxs-lookup"><span data-stu-id="3082c-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="3082c-185">**TriviaContext：** 表示书呆子测验应用程序的实体框架数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="3082c-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="3082c-186">此类派生自**DContext** ，并公开**DbSet**属性，这些属性表示上述实体的集合。</span><span class="sxs-lookup"><span data-stu-id="3082c-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="3082c-187">**TriviaDatabaseInitializer：** **TriviaContext**类的实体框架初始值设定项，该类继承自**CreateDatabaseIfNotExists**。</span><span class="sxs-lookup"><span data-stu-id="3082c-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="3082c-188">此类的默认行为是在数据库不存在时创建该数据库，并插入在**Seed**方法中指定的实体。</span><span class="sxs-lookup"><span data-stu-id="3082c-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="3082c-189">打开**Global.asax.cs**文件并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="3082c-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="3082c-190">在**应用程序\_Start**方法的开头添加以下代码，以将**TriviaDatabaseInitializer**设置为数据库初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="3082c-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="3082c-191">修改**Home**控制器以限制对经过身份验证的用户的访问。</span><span class="sxs-lookup"><span data-stu-id="3082c-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="3082c-192">为此，请打开 "**控制器**" 文件夹中的**HomeController.cs**文件，并将**授权**属性添加到**HomeController**类定义。</span><span class="sxs-lookup"><span data-stu-id="3082c-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="3082c-193">**授权**筛选器将检查是否对用户进行了身份验证。</span><span class="sxs-lookup"><span data-stu-id="3082c-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="3082c-194">如果用户未通过身份验证，则返回 HTTP 状态代码401（未授权），而无需调用该操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="3082c-195">您可以在全局、控制器级别或单个操作级别应用筛选器。</span><span class="sxs-lookup"><span data-stu-id="3082c-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="3082c-196">现在，您将自定义网页的布局和品牌。</span><span class="sxs-lookup"><span data-stu-id="3082c-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="3082c-197">为此，请打开视图中的 **\_布局 cshtml**文件 **|共享**文件夹，并通过将*ASP.NET 应用程序*替换为*书呆子测验*来更新 **&lt;标题&gt;** 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="3082c-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="3082c-198">在同一文件中，通过删除 "*关于*" 和 "*联系人*" 链接，然后重命名 "*开始* *播放*" 链接来更新导航栏。</span><span class="sxs-lookup"><span data-stu-id="3082c-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="3082c-199">此外，将*应用程序名称*链接重命名为 "*书呆子测验*"。</span><span class="sxs-lookup"><span data-stu-id="3082c-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="3082c-200">导航栏的 HTML 应类似于以下代码。</span><span class="sxs-lookup"><span data-stu-id="3082c-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="3082c-201">通过使用*书呆子测验*替换*My ASP.NET 应用程序*来更新布局页的页脚。</span><span class="sxs-lookup"><span data-stu-id="3082c-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="3082c-202">为此，请将 **&lt;页脚&gt;** 元素的内容替换为以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="3082c-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="3082c-203">任务2–创建 TriviaController Web API</span><span class="sxs-lookup"><span data-stu-id="3082c-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="3082c-204">在上一任务中，已创建书呆子测验 web 应用程序的初始结构。</span><span class="sxs-lookup"><span data-stu-id="3082c-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="3082c-205">你现在将生成一个简单的 Web API 服务，该服务与测验数据模型交互并公开以下操作：</span><span class="sxs-lookup"><span data-stu-id="3082c-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="3082c-206">**获取/api/trivia**：从测验列表中检索要由经过身份验证的用户回答的下一个问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="3082c-207">**POST/api/trivia**：存储经过身份验证的用户指定的测验应答。</span><span class="sxs-lookup"><span data-stu-id="3082c-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="3082c-208">你将使用 Visual Studio 提供的 ASP.NET 基架工具为 Web API 控制器类创建基线。</span><span class="sxs-lookup"><span data-stu-id="3082c-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="3082c-209">在**应用\_启动**文件夹内打开**WebApiConfig.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="3082c-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="3082c-210">此文件定义了 Web API 服务的配置，如如何将路由映射到 Web API 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="3082c-211">在文件的开头添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="3082c-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="3082c-212">将以下突出显示的代码添加到**Register**方法，以全局配置由 Web API 操作方法检索的 JSON 数据的格式化程序。</span><span class="sxs-lookup"><span data-stu-id="3082c-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="3082c-213">**CamelCasePropertyNamesContractResolver**自动将属性名称转换为*camel*大小写，这是 JavaScript 中属性名称的一般约定。</span><span class="sxs-lookup"><span data-stu-id="3082c-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="3082c-214">在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的 "**控制器**" 文件夹，然后选择 "**添加 |新建基架项 ...**</span><span class="sxs-lookup"><span data-stu-id="3082c-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="3082c-215">![创建新的基架项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "创建新的基架项")</span><span class="sxs-lookup"><span data-stu-id="3082c-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="3082c-216">*创建新的基架项*</span><span class="sxs-lookup"><span data-stu-id="3082c-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="3082c-217">在 "**添加基架**" 对话框中，确保已在左窗格中选择 "**通用**" 节点。</span><span class="sxs-lookup"><span data-stu-id="3082c-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="3082c-218">然后，在中间窗格中选择 " **WEB API 2 控制器-空**" 模板，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="3082c-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="3082c-219">![选择 "Web API 2 控制器" 空模板](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "选择 "Web API 2 控制器" 空模板")</span><span class="sxs-lookup"><span data-stu-id="3082c-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="3082c-220">*选择 "Web API 2 控制器" 空模板*</span><span class="sxs-lookup"><span data-stu-id="3082c-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3082c-221">**ASP.NET 基架**是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="3082c-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="3082c-222">Visual Studio 2013 包含用于 MVC 和 Web API 项目的预安装代码生成器。</span><span class="sxs-lookup"><span data-stu-id="3082c-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="3082c-223">如果要快速添加与数据模型交互的代码，以减少开发标准数据操作所需的时间，则应在项目中使用基架。</span><span class="sxs-lookup"><span data-stu-id="3082c-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="3082c-224">基架进程还可以确保在项目中安装所有必需的依赖项。</span><span class="sxs-lookup"><span data-stu-id="3082c-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="3082c-225">例如，如果您从一个空的 ASP.NET 项目开始，然后使用基架添加一个 Web API 控制器，则所需的 Web API NuGet 包和引用会自动添加到您的项目中。</span><span class="sxs-lookup"><span data-stu-id="3082c-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="3082c-226">在 "**添加控制器**" 对话框中，在 "**控制器名称**" 文本框中键入*TriviaController* ，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="3082c-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="3082c-227">![添加琐碎内容控制器](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "添加琐碎内容控制器")</span><span class="sxs-lookup"><span data-stu-id="3082c-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="3082c-228">*添加琐碎内容控制器*</span><span class="sxs-lookup"><span data-stu-id="3082c-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="3082c-229">然后，将**TriviaController.cs**文件添加到**GeekQuiz**项目的**控制器**文件夹中，其中包含一个空的**TriviaController**类。</span><span class="sxs-lookup"><span data-stu-id="3082c-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="3082c-230">在文件的开头添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="3082c-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="3082c-231">（代码段- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*）</span><span class="sxs-lookup"><span data-stu-id="3082c-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="3082c-232">在**TriviaController**类的开头添加以下代码，以定义、初始化和处置控制器中的**TriviaContext**实例。</span><span class="sxs-lookup"><span data-stu-id="3082c-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="3082c-233">（代码段- *AspNetWebApiSpa-Ex1-TriviaControllerContext*）</span><span class="sxs-lookup"><span data-stu-id="3082c-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="3082c-234">**TriviaController**的**Dispose**方法调用**TriviaContext**实例的**dispose**方法，这可确保在释放或垃圾回收**TriviaContext**实例时释放上下文对象使用的所有资源。</span><span class="sxs-lookup"><span data-stu-id="3082c-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="3082c-235">这包括关闭由实体框架打开的所有数据库连接。</span><span class="sxs-lookup"><span data-stu-id="3082c-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="3082c-236">在**TriviaController**类的末尾添加以下帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="3082c-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="3082c-237">此方法从数据库中检索要由指定用户应答的以下测验问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="3082c-238">（代码段- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*）</span><span class="sxs-lookup"><span data-stu-id="3082c-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="3082c-239">向**TriviaController**类添加以下**Get**操作方法。</span><span class="sxs-lookup"><span data-stu-id="3082c-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="3082c-240">此操作方法调用在上一步中定义的**NextQuestionAsync** helper 方法，以检索经过身份验证的用户的下一个问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="3082c-241">（代码段- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*）</span><span class="sxs-lookup"><span data-stu-id="3082c-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="3082c-242">在**TriviaController**类的末尾添加以下帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="3082c-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="3082c-243">此方法将指定的答案存储在数据库中，并返回一个布尔值，指示答案是否正确。</span><span class="sxs-lookup"><span data-stu-id="3082c-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="3082c-244">（代码段- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*）</span><span class="sxs-lookup"><span data-stu-id="3082c-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="3082c-245">将以下**Post**操作方法添加到**TriviaController**类。</span><span class="sxs-lookup"><span data-stu-id="3082c-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="3082c-246">此操作方法将答案与经过身份验证的用户相关联，并调用**StoreAsync** helper 方法。</span><span class="sxs-lookup"><span data-stu-id="3082c-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="3082c-247">然后，它使用 helper 方法返回的布尔值发送响应。</span><span class="sxs-lookup"><span data-stu-id="3082c-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="3082c-248">（代码段- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*）</span><span class="sxs-lookup"><span data-stu-id="3082c-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="3082c-249">修改 Web API 控制器，通过向**TriviaController**类定义添加**授权**特性来限制对经过身份验证的用户的访问。</span><span class="sxs-lookup"><span data-stu-id="3082c-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="3082c-250">任务3–运行解决方案</span><span class="sxs-lookup"><span data-stu-id="3082c-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="3082c-251">在此任务中，你将验证你在上一任务中生成的 Web API 服务是否按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="3082c-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="3082c-252">你将使用 Internet Explorer **F12 开发人员工具**来捕获网络流量，并检查 Web API 服务的完整响应。</span><span class="sxs-lookup"><span data-stu-id="3082c-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="3082c-253">请确保在 Visual Studio 工具栏上的 "**开始**" 按钮中选择了**Internet Explorer** 。</span><span class="sxs-lookup"><span data-stu-id="3082c-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 选项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. <span data-ttu-id="3082c-255">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="3082c-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="3082c-256">"**登录**" 页应出现在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="3082c-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3082c-257">当应用程序启动时，将触发默认 MVC 路由，该路由默认映射到**HomeController**类的**索引**操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="3082c-258">由于**HomeController**仅限于经过身份验证的用户（请记住，您在练习1中用**授权**属性修饰了该类），并且尚未对用户进行身份验证，因此应用程序会将原始请求重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="3082c-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="3082c-259">![运行解决方案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "运行解决方案")</span><span class="sxs-lookup"><span data-stu-id="3082c-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="3082c-260">*运行解决方案*</span><span class="sxs-lookup"><span data-stu-id="3082c-260">*Running the solution*</span></span>
2. <span data-ttu-id="3082c-261">单击 "**注册**" 以创建新用户。</span><span class="sxs-lookup"><span data-stu-id="3082c-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="3082c-262">![注册新用户](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "注册新用户")</span><span class="sxs-lookup"><span data-stu-id="3082c-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="3082c-263">*注册新用户*</span><span class="sxs-lookup"><span data-stu-id="3082c-263">*Registering a new user*</span></span>
3. <span data-ttu-id="3082c-264">在 "**注册**" 页上，输入**用户名**和**密码**，然后单击 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="3082c-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="3082c-265">![注册页面](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "注册页面")</span><span class="sxs-lookup"><span data-stu-id="3082c-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="3082c-266">*注册页面*</span><span class="sxs-lookup"><span data-stu-id="3082c-266">*Register page*</span></span>
4. <span data-ttu-id="3082c-267">应用程序将注册新帐户，并对用户进行身份验证并重定向回主页。</span><span class="sxs-lookup"><span data-stu-id="3082c-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="3082c-268">![用户已进行身份验证](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "用户已进行身份验证")</span><span class="sxs-lookup"><span data-stu-id="3082c-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="3082c-269">*用户已进行身份验证*</span><span class="sxs-lookup"><span data-stu-id="3082c-269">*User is authenticated*</span></span>
5. <span data-ttu-id="3082c-270">在浏览器中，按**F12**打开**开发人员工具**面板。</span><span class="sxs-lookup"><span data-stu-id="3082c-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="3082c-271">按**CTRL + 4**或单击**网络**图标，然后单击绿色箭头按钮开始捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="3082c-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="3082c-272">![启动 Web API 网络捕获](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "启动 Web API 网络捕获")</span><span class="sxs-lookup"><span data-stu-id="3082c-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="3082c-273">*启动 Web API 网络捕获*</span><span class="sxs-lookup"><span data-stu-id="3082c-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="3082c-274">将**api/琐碎内容**追加到浏览器地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="3082c-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="3082c-275">现在，你将从**TriviaController**中的**Get**操作方法检查响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3082c-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="3082c-276">![通过 Web API 检索下一个问题数据](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "通过 Web API 检索下一个问题数据")</span><span class="sxs-lookup"><span data-stu-id="3082c-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="3082c-277">*通过 Web API 检索下一个问题数据*</span><span class="sxs-lookup"><span data-stu-id="3082c-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="3082c-278">下载完成后，系统将提示您使用下载的文件进行操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="3082c-279">让对话框保持打开状态，以便能够通过 "开发人员工具" 窗口观看响应内容。</span><span class="sxs-lookup"><span data-stu-id="3082c-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="3082c-280">现在，你将检查响应的正文。</span><span class="sxs-lookup"><span data-stu-id="3082c-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="3082c-281">为此，请单击 "**详细信息**" 选项卡，然后单击 "**响应正文**"。</span><span class="sxs-lookup"><span data-stu-id="3082c-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="3082c-282">您可以使用 "属性"**选项**（这是**TriviaOption**对象的列表）的对象、 **id**和与**TriviaQuestion**类相对应的**标题**来检查下载的数据。</span><span class="sxs-lookup"><span data-stu-id="3082c-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="3082c-283">![查看 Web API 响应正文](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "查看 Web API 响应正文")</span><span class="sxs-lookup"><span data-stu-id="3082c-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="3082c-284">*查看 Web API 响应正文*</span><span class="sxs-lookup"><span data-stu-id="3082c-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="3082c-285">返回到 Visual Studio 并按**SHIFT + F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="3082c-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="3082c-286">练习2：创建 SPA 接口</span><span class="sxs-lookup"><span data-stu-id="3082c-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="3082c-287">在本练习中，您将首先构建书呆子测验的 web 前端部分，重点介绍使用**AngularJS**的单页应用程序交互。</span><span class="sxs-lookup"><span data-stu-id="3082c-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="3082c-288">然后，你将通过使用 CSS3 来执行丰富的动画来增强用户体验，并在从一个问题转换到下一个问题时提供上下文切换的视觉效果。</span><span class="sxs-lookup"><span data-stu-id="3082c-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="3082c-289">任务1–使用 AngularJS 创建 SPA 接口</span><span class="sxs-lookup"><span data-stu-id="3082c-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="3082c-290">在此任务中，您将使用**AngularJS**实现书呆子测验应用程序的客户端。</span><span class="sxs-lookup"><span data-stu-id="3082c-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="3082c-291">**AngularJS**是一个开源 JavaScript 框架，它将基于浏览器的应用程序与*模型-视图-控制器*（MVC）功能进行了补充，同时简化了开发和测试。</span><span class="sxs-lookup"><span data-stu-id="3082c-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="3082c-292">首先从 Visual Studio 的包管理器控制台安装 AngularJS。</span><span class="sxs-lookup"><span data-stu-id="3082c-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="3082c-293">然后，你将创建一个控制器来提供书呆子测验应用和视图的行为，以便使用 AngularJS 模板引擎呈现测验问题和答案。</span><span class="sxs-lookup"><span data-stu-id="3082c-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="3082c-294">有关 AngularJS 的详细信息，请参阅[[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)。</span><span class="sxs-lookup"><span data-stu-id="3082c-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>

1. <span data-ttu-id="3082c-295">打开**Visual Studio Express 2013 For Web** ，并打开位于**buildingappswithcachingservice-ex2-getproducts latency-cs-CreatingASPAInterface/Begin**文件夹中的**GeekQuiz**解决方案。</span><span class="sxs-lookup"><span data-stu-id="3082c-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="3082c-296">或者，你可以继续学习你在上一练习中获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="3082c-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="3082c-297">从 "**工具**" > **NuGet 包管理器**"中打开**包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="3082c-297">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="3082c-298">键入以下命令以安装**AngularJS** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="3082c-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="3082c-299">在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的 "**脚本**" 文件夹，然后选择 "**添加 |新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="3082c-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="3082c-300">将文件夹命名为 " **app** "，并按**enter**。</span><span class="sxs-lookup"><span data-stu-id="3082c-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="3082c-301">右键单击刚创建的**应用**文件夹，然后选择 "**添加 |JavaScript 文件**。</span><span class="sxs-lookup"><span data-stu-id="3082c-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![创建新的 JavaScript 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="3082c-303">*创建新的 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="3082c-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="3082c-304">在 "**指定项名称**" 对话框中，在 "**项名称**" 文本框中键入 "*测验-控制器*"，并单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="3082c-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![命名新的 JavaScript 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="3082c-306">*命名新的 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="3082c-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="3082c-307">在**quiz-controller**文件中，添加以下代码以声明和初始化 AngularJS **QuizCtrl**控制器。</span><span class="sxs-lookup"><span data-stu-id="3082c-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="3082c-308">（代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-AngularQuizController*）</span><span class="sxs-lookup"><span data-stu-id="3082c-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="3082c-309">**QuizCtrl**控制器的构造函数需要一个名为 **$scope**的 injectable 参数。</span><span class="sxs-lookup"><span data-stu-id="3082c-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="3082c-310">应通过将属性附加到 **$scope**对象，在构造函数中设置作用域的初始状态。</span><span class="sxs-lookup"><span data-stu-id="3082c-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="3082c-311">属性包含**视图模型**，在注册控制器时，模板将可对其进行访问。</span><span class="sxs-lookup"><span data-stu-id="3082c-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="3082c-312">**QuizCtrl**控制器是在名为**QuizApp**的模块中定义的。</span><span class="sxs-lookup"><span data-stu-id="3082c-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="3082c-313">模块是工作单元，可让你将应用程序分解为单独的组件。</span><span class="sxs-lookup"><span data-stu-id="3082c-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="3082c-314">使用模块的主要优点是代码更易于理解，并简化了单元测试、可重用性和可维护性。</span><span class="sxs-lookup"><span data-stu-id="3082c-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="3082c-315">现在，你将向范围中添加行为，以便对从视图触发的事件做出反应。</span><span class="sxs-lookup"><span data-stu-id="3082c-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="3082c-316">在**QuizCtrl**控制器的末尾添加以下代码，以定义 **$scope**对象中的**nextQuestion**函数。</span><span class="sxs-lookup"><span data-stu-id="3082c-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="3082c-317">（代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-AngularQuizControllerNextQuestion*）</span><span class="sxs-lookup"><span data-stu-id="3082c-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="3082c-318">此函数检索在上一练习中创建的**琐碎内容**Web API 中的下一个问题，并将问题数据附加到 **$scope**的对象。</span><span class="sxs-lookup"><span data-stu-id="3082c-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="3082c-319">在**QuizCtrl**控制器的末尾插入以下代码，以定义 **$scope**对象中的**sendAnswer**函数。</span><span class="sxs-lookup"><span data-stu-id="3082c-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="3082c-320">（代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-AngularQuizControllerSendAnswer*）</span><span class="sxs-lookup"><span data-stu-id="3082c-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="3082c-321">此函数将用户选择的答案发送到**琐碎内容**Web API，并将结果存储在 **$scope**对象中（即，如果答案是正确的）。</span><span class="sxs-lookup"><span data-stu-id="3082c-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="3082c-322">上面的**nextQuestion**和**SendAnswer**函数使用 AngularJS **$http**对象，通过浏览器中的 XMLHTTPREQUEST JavaScript 对象抽象与 Web API 的通信。</span><span class="sxs-lookup"><span data-stu-id="3082c-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="3082c-323">AngularJS 支持另一种服务，该服务提供更高级别的抽象，以通过 RESTful Api 对资源执行 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="3082c-324">AngularJS **$resource**对象具有一些操作方法，这些方法可提供高级行为，而无需与 **$http**对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="3082c-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="3082c-325">考虑在需要 CRUD 模型的情况下使用 **$resource**对象（有关信息，请参阅[$resource 文档](https://docs.angularjs.org/api/ngResource/service/$resource)）。</span><span class="sxs-lookup"><span data-stu-id="3082c-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="3082c-326">下一步是创建定义测验视图的 AngularJS 模板。</span><span class="sxs-lookup"><span data-stu-id="3082c-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="3082c-327">为此，请打开视图中的**索引 cshtml**文件 **|Home**文件夹，并将内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3082c-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="3082c-328">（代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-GeekQuizView*）</span><span class="sxs-lookup"><span data-stu-id="3082c-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="3082c-329">AngularJS 模板是一种声明性规范，使用模型和控制器中的信息将静态标记转换为用户在浏览器中看到的动态视图。</span><span class="sxs-lookup"><span data-stu-id="3082c-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="3082c-330">下面是可在模板中使用的 AngularJS 元素和元素特性的示例：</span><span class="sxs-lookup"><span data-stu-id="3082c-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="3082c-331">" **Ng-app** " 指令告诉 AngularJS 表示应用程序的根元素的 DOM 元素。</span><span class="sxs-lookup"><span data-stu-id="3082c-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="3082c-332">在声明指令的点， **ng 控制器**指令将控制器附加到 DOM。</span><span class="sxs-lookup"><span data-stu-id="3082c-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="3082c-333">大括号表示法 **{{}}** 表示在控制器中定义的作用域属性的绑定。</span><span class="sxs-lookup"><span data-stu-id="3082c-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="3082c-334">使用**ng-click**指令可调用在响应用户单击的范围内定义的函数。</span><span class="sxs-lookup"><span data-stu-id="3082c-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="3082c-335">打开**Content**文件夹中的**web.config**文件，并在该文件的末尾添加以下突出显示的样式，以提供测验视图的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="3082c-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="3082c-336">（代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-GeekQuizStyles*）</span><span class="sxs-lookup"><span data-stu-id="3082c-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="3082c-337">任务2–运行解决方案</span><span class="sxs-lookup"><span data-stu-id="3082c-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="3082c-338">在此任务中，你将使用通过 AngularJS 生成的新用户界面来执行该解决方案，以解答一些测验问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="3082c-339">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="3082c-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="3082c-340">注册新的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="3082c-340">Register a new user account.</span></span> <span data-ttu-id="3082c-341">为此，请按照练习1，任务3中所述的注册步骤操作。</span><span class="sxs-lookup"><span data-stu-id="3082c-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3082c-342">如果使用上一练习中的解决方案，则可以使用之前创建的用户帐户登录。</span><span class="sxs-lookup"><span data-stu-id="3082c-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="3082c-343">将显示 "**主页**"，其中显示了测验的第一个问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="3082c-344">单击其中一个选项即可回答问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="3082c-345">这会触发前面定义的**sendAnswer**函数，该函数将所选选项发送到**琐碎内容**Web API。</span><span class="sxs-lookup"><span data-stu-id="3082c-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="3082c-346">![回答问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "回答问题")</span><span class="sxs-lookup"><span data-stu-id="3082c-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="3082c-347">*回答问题*</span><span class="sxs-lookup"><span data-stu-id="3082c-347">*Answering a question*</span></span>
4. <span data-ttu-id="3082c-348">单击其中一个按钮后，将出现答案。</span><span class="sxs-lookup"><span data-stu-id="3082c-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="3082c-349">单击 "**下一问题**" 以显示以下问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="3082c-350">这会触发控制器中定义的**nextQuestion**函数。</span><span class="sxs-lookup"><span data-stu-id="3082c-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="3082c-351">![请求下一个问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "请求下一个问题")</span><span class="sxs-lookup"><span data-stu-id="3082c-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="3082c-352">*请求下一个问题*</span><span class="sxs-lookup"><span data-stu-id="3082c-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="3082c-353">接下来应该会出现问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-353">The next question should appear.</span></span> <span data-ttu-id="3082c-354">根据需要继续回答问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="3082c-355">完成所有问题后，应返回到第一个问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="3082c-356">![其他问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "其他问题")</span><span class="sxs-lookup"><span data-stu-id="3082c-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="3082c-357">*下一个问题*</span><span class="sxs-lookup"><span data-stu-id="3082c-357">*Next question*</span></span>
6. <span data-ttu-id="3082c-358">返回到 Visual Studio 并按**SHIFT + F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="3082c-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="3082c-359">任务3–使用 CSS3 创建翻转动画</span><span class="sxs-lookup"><span data-stu-id="3082c-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="3082c-360">在此任务中，你将使用 CSS3 属性来执行丰富的动画，方法是在解答问题后，在检索到下一个问题时添加一个翻转效果。</span><span class="sxs-lookup"><span data-stu-id="3082c-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="3082c-361">在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的**Content**文件夹，然后选择 "**添加 |现有项 ...**</span><span class="sxs-lookup"><span data-stu-id="3082c-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="3082c-362">![将现有项添加到 Content 文件夹](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "将现有项添加到 Content 文件夹")</span><span class="sxs-lookup"><span data-stu-id="3082c-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="3082c-363">*将现有项添加到 Content 文件夹*</span><span class="sxs-lookup"><span data-stu-id="3082c-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="3082c-364">在 "**添加现有项**" 对话框中，导航到 "**源/资源**" 文件夹，然后选择 "**反向**"。</span><span class="sxs-lookup"><span data-stu-id="3082c-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="3082c-365">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="3082c-365">Click **Add**.</span></span>

    <span data-ttu-id="3082c-366">![从资产中添加 Flip .css 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "从资产中添加 Flip .css 文件")</span><span class="sxs-lookup"><span data-stu-id="3082c-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="3082c-367">*从资产中添加 Flip .css 文件*</span><span class="sxs-lookup"><span data-stu-id="3082c-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="3082c-368">打开刚才添加的 "**翻转 .css** " 文件并检查其内容。</span><span class="sxs-lookup"><span data-stu-id="3082c-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="3082c-369">找到**翻转转换**注释。</span><span class="sxs-lookup"><span data-stu-id="3082c-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="3082c-370">此注释下的样式使用 CSS**透视**和**rotateY**转换来生成 &quot;卡片翻转&quot; 效果。</span><span class="sxs-lookup"><span data-stu-id="3082c-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="3082c-371">在 "翻转注释" 中找到 "**隐藏背面" 窗格**。</span><span class="sxs-lookup"><span data-stu-id="3082c-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="3082c-372">此注释下的样式通过将**隐**CSS 属性设置为*隐藏*，隐藏了正面朝远离查看器的面。</span><span class="sxs-lookup"><span data-stu-id="3082c-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="3082c-373">在**应用\_启动**文件夹内打开**BundleConfig.cs**文件，并在 **&quot;~/Content/css&quot;** 样式捆绑包中添加对**文件的**引用</span><span class="sxs-lookup"><span data-stu-id="3082c-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="3082c-374">按**F5**运行该解决方案，并以您的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="3082c-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="3082c-375">单击其中一个选项即可回答问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="3082c-376">请注意在视图间转换时的翻转效果。</span><span class="sxs-lookup"><span data-stu-id="3082c-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="3082c-377">![使用反转效果回答问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "使用反转效果回答问题")</span><span class="sxs-lookup"><span data-stu-id="3082c-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="3082c-378">*使用反转效果回答问题*</span><span class="sxs-lookup"><span data-stu-id="3082c-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="3082c-379">单击 "**下一问题**" 以检索以下问题。</span><span class="sxs-lookup"><span data-stu-id="3082c-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="3082c-380">翻转效果应再次出现。</span><span class="sxs-lookup"><span data-stu-id="3082c-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="3082c-381">![检索以下带有翻转效果的问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "检索以下带有翻转效果的问题")</span><span class="sxs-lookup"><span data-stu-id="3082c-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="3082c-382">*检索以下带有翻转效果的问题*</span><span class="sxs-lookup"><span data-stu-id="3082c-382">*Retrieving the following question with the flip effect*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="3082c-383">摘要</span><span class="sxs-lookup"><span data-stu-id="3082c-383">Summary</span></span>

<span data-ttu-id="3082c-384">通过完成本动手实验，你学习了如何：</span><span class="sxs-lookup"><span data-stu-id="3082c-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="3082c-385">使用 ASP.NET 基架创建 ASP.NET Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="3082c-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="3082c-386">实现 Web API Get 操作以检索下一个测验问题</span><span class="sxs-lookup"><span data-stu-id="3082c-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="3082c-387">实现 Web API 后操作以存储测验答案</span><span class="sxs-lookup"><span data-stu-id="3082c-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="3082c-388">从 Visual Studio 包管理器控制台安装 AngularJS</span><span class="sxs-lookup"><span data-stu-id="3082c-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="3082c-389">实现 AngularJS 模板和控制器</span><span class="sxs-lookup"><span data-stu-id="3082c-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="3082c-390">使用 CSS3 转换执行动画效果</span><span class="sxs-lookup"><span data-stu-id="3082c-390">Use CSS3 transitions to perform animation effects</span></span>
