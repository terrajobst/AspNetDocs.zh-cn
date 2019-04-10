---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 生成 RESTful Api 与 ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: 动手实验：在 ASP.NET 中使用 Web API 4.x 生成一个简单的 REST API 为联系人管理器应用程序。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3ba7f2d186e6f0837a32f69f964cec19fe625953
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391476"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="593ab-103">生成使用 ASP.NET Web API 的 RESTful Api</span><span class="sxs-lookup"><span data-stu-id="593ab-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="593ab-104">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="593ab-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="593ab-105">动手实验：在 ASP.NET 中使用 Web API 4.x 生成一个简单的 REST API 为联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="593ab-106">您还将生成客户端以使用 API。</span><span class="sxs-lookup"><span data-stu-id="593ab-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="593ab-107">近年来，它已成为清除 HTTP 不再仅仅用于提供 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="593ab-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="593ab-108">它也是一个强大的平台，用于构建 Web Api，使用少数几个动词 （GET、 POST 等） 以及几个简单的概念类似于*Uri*并*标头*。</span><span class="sxs-lookup"><span data-stu-id="593ab-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="593ab-109">ASP.NET Web API 是一组简化 HTTP 编程的组件。</span><span class="sxs-lookup"><span data-stu-id="593ab-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="593ab-110">因为它基于 ASP.NET MVC 运行时，Web API 将自动处理 HTTP 的低级别传输详细信息。</span><span class="sxs-lookup"><span data-stu-id="593ab-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="593ab-111">同时，Web API 自然会公开 HTTP 编程模型。</span><span class="sxs-lookup"><span data-stu-id="593ab-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="593ab-112">实际上，Web API 的一个目标是向*不*抽象出 HTTP 的现实。</span><span class="sxs-lookup"><span data-stu-id="593ab-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="593ab-113">因此，Web API 是灵活且易于扩展。</span><span class="sxs-lookup"><span data-stu-id="593ab-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="593ab-114">REST 体系结构风格已被证明是利用 HTTP-的有效方法，尽管它并不是 HTTP 的唯一有效方法。</span><span class="sxs-lookup"><span data-stu-id="593ab-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="593ab-115">联系人管理器将公开用于列出、 添加和删除联系人，以及其他基于 Rest。</span><span class="sxs-lookup"><span data-stu-id="593ab-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="593ab-116">本实验需要基本了解 HTTP，其余部分，并假定你已基本了解 HTML、 JavaScript 和 jQuery。</span><span class="sxs-lookup"><span data-stu-id="593ab-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="593ab-117">ASP.NET 网站上有一个专用于在 ASP.NET Web API 框架的区域[ https://asp.net/web-api ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="593ab-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="593ab-118">此站点将继续提供最新信息、 示例和新闻与 Web API，因此它请经常查看如果你想要深入了解创建可用于几乎任何设备或开发框架自定义 Web Api 的画面。</span><span class="sxs-lookup"><span data-stu-id="593ab-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="593ab-119">ASP.NET Web API，类似于 ASP.NET MVC 4 中，有很大的灵活性方面将服务层与允许您使用多个可用的依赖关系注入框架变得相当容易的控制器分离开来。</span><span class="sxs-lookup"><span data-stu-id="593ab-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="593ab-120">演示如何使用依赖关系注入在 ASP.NET Web API 项目中，你可以下载它从 Ninject 的 MSDN 中没有一个好的示例[此处](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)。</span><span class="sxs-lookup"><span data-stu-id="593ab-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="593ab-121">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="593ab-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="593ab-122">目标</span><span class="sxs-lookup"><span data-stu-id="593ab-122">Objectives</span></span>

<span data-ttu-id="593ab-123">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="593ab-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="593ab-124">实现 rest 样式 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="593ab-125">从 HTML 客户端调用 API</span><span class="sxs-lookup"><span data-stu-id="593ab-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="593ab-126">系统必备</span><span class="sxs-lookup"><span data-stu-id="593ab-126">Prerequisites</span></span>

<span data-ttu-id="593ab-127">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="593ab-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="593ab-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 B](#AppendixB)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="593ab-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="593ab-129">安装</span><span class="sxs-lookup"><span data-stu-id="593ab-129">Setup</span></span>

**<span data-ttu-id="593ab-130">安装代码片段</span><span class="sxs-lookup"><span data-stu-id="593ab-130">Installing Code Snippets</span></span>**

<span data-ttu-id="593ab-131">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="593ab-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="593ab-132">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="593ab-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="593ab-133">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 a:使用代码片段](#AppendixA)&quot;。</span><span class="sxs-lookup"><span data-stu-id="593ab-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="593ab-134">练习</span><span class="sxs-lookup"><span data-stu-id="593ab-134">Exercises</span></span>

<span data-ttu-id="593ab-135">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="593ab-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="593ab-136">练习 1:创建只读的 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="593ab-137">练习 2:创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="593ab-138">练习 3:使用从 HTML 客户端 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="593ab-139">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="593ab-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="593ab-140">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="593ab-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="593ab-141">估计的时间才能完成此实验：**60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="593ab-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="593ab-142">练习 1:创建只读的 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="593ab-143">在此练习中，将为联系人管理器实现只读的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="593ab-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="593ab-144">任务 1-创建 API 项目</span><span class="sxs-lookup"><span data-stu-id="593ab-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="593ab-145">在本任务中，您将使用新的 ASP.NET web 项目模板创建 Web API web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="593ab-146">运行**Visual Studio 2012 Express for Web**，为此，请转到**启动**并键入**VS Express for Web**然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="593ab-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="593ab-147">从**文件**菜单中，选择**新项目**。</span><span class="sxs-lookup"><span data-stu-id="593ab-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="593ab-148">选择**Visual C# |Web**项目类型从项目类型树视图，然后选择**ASP.NET MVC 4 Web 应用程序**项目类型。</span><span class="sxs-lookup"><span data-stu-id="593ab-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="593ab-149">将项目的**名称**到*ContactManager*并**解决方案名称**到*开始*，然后单击**确定**.</span><span class="sxs-lookup"><span data-stu-id="593ab-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="593ab-150">![创建新的 ASP.NET MVC 4.0 Web 应用程序项目](build-restful-apis-with-aspnet-web-api/_static/image1.png "创建新的 ASP.NET MVC 4.0 Web 应用程序项目")</span><span class="sxs-lookup"><span data-stu-id="593ab-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    *<span data-ttu-id="593ab-151">创建新的 ASP.NET MVC 4.0 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="593ab-151">Creating a new ASP.NET MVC 4.0 Web Application Project</span></span>*
3. <span data-ttu-id="593ab-152">在 ASP.NET MVC 4 项目类型对话框中，选择**Web API**项目类型。</span><span class="sxs-lookup"><span data-stu-id="593ab-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="593ab-153">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="593ab-153">Click **OK**.</span></span>

    <span data-ttu-id="593ab-154">![指定 Web API 项目类型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 项目类型")</span><span class="sxs-lookup"><span data-stu-id="593ab-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    *<span data-ttu-id="593ab-155">指定 Web API 项目类型</span><span class="sxs-lookup"><span data-stu-id="593ab-155">Specifying the Web API project type</span></span>*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="593ab-156">任务 2-创建联系人管理器 API 控制器</span><span class="sxs-lookup"><span data-stu-id="593ab-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="593ab-157">在本任务中，将创建 API 方法将驻留在其中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="593ab-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="593ab-158">删除名为的文件**ValuesController.cs**内**控制器**从项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="593ab-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="593ab-159">右键单击**控制器**文件夹中该项目并选择**添加 |控制器**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="593ab-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="593ab-160">![向项目添加新的控制器](build-restful-apis-with-aspnet-web-api/_static/image3.png "向项目添加新的控制器")</span><span class="sxs-lookup"><span data-stu-id="593ab-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    *<span data-ttu-id="593ab-161">向项目添加新的控制器</span><span class="sxs-lookup"><span data-stu-id="593ab-161">Adding a new controller to the project</span></span>*
3. <span data-ttu-id="593ab-162">在中**添加控制器**对话框中，选择**空 API 控制器**的模板菜单中。</span><span class="sxs-lookup"><span data-stu-id="593ab-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="593ab-163">控制器类命名**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="593ab-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="593ab-164">然后，单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="593ab-164">Then, click **Add.**</span></span>

    <span data-ttu-id="593ab-165">![使用添加控制器对话框创建新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用添加控制器对话框创建新的 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="593ab-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    *<span data-ttu-id="593ab-166">使用添加控制器对话框创建新的 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="593ab-166">Using the Add Controller dialog to create a new Web API controller</span></span>*
4. <span data-ttu-id="593ab-167">将以下代码添加到**ContactController**。</span><span class="sxs-lookup"><span data-stu-id="593ab-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="593ab-168">(代码段- *Web API 实验-Ex01-获取 API 方法*)</span><span class="sxs-lookup"><span data-stu-id="593ab-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="593ab-169">按**F5**调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="593ab-170">Web API 项目的默认主页应显示。</span><span class="sxs-lookup"><span data-stu-id="593ab-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="593ab-171">![ASP.NET Web API 应用程序的默认主页](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 应用程序的默认主页")</span><span class="sxs-lookup"><span data-stu-id="593ab-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    *<span data-ttu-id="593ab-172">ASP.NET Web API 应用程序的默认主页</span><span class="sxs-lookup"><span data-stu-id="593ab-172">The default home page of an ASP.NET Web API application</span></span>*
6. <span data-ttu-id="593ab-173">在 Internet Explorer 窗口中，按**F12**键以打开**开发人员工具**窗口。</span><span class="sxs-lookup"><span data-stu-id="593ab-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="593ab-174">单击**网络**选项卡，然后依次**启动捕获**按钮开始到窗口中捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="593ab-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="593ab-175">![打开网络选项卡并启动网络捕获](build-restful-apis-with-aspnet-web-api/_static/image6.png "打开网络选项卡并启动网络捕获")</span><span class="sxs-lookup"><span data-stu-id="593ab-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    *<span data-ttu-id="593ab-176">打开网络选项卡并启动网络捕获</span><span class="sxs-lookup"><span data-stu-id="593ab-176">Opening the network tab and initiating network capture</span></span>*
7. <span data-ttu-id="593ab-177">追加与浏览器的地址栏中的 URL **/api/contact** ，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="593ab-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="593ab-178">传输的详细信息会在网络捕获窗口中显示。</span><span class="sxs-lookup"><span data-stu-id="593ab-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="593ab-179">请注意，响应的 MIME 类型是**应用程序 /json**。</span><span class="sxs-lookup"><span data-stu-id="593ab-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="593ab-180">此示例演示默认输出格式的 JSON 的方式。</span><span class="sxs-lookup"><span data-stu-id="593ab-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="593ab-181">![在网络视图中查看 Web API 请求的输出](build-restful-apis-with-aspnet-web-api/_static/image7.png "网络视图中查看 Web API 请求的输出")</span><span class="sxs-lookup"><span data-stu-id="593ab-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    *<span data-ttu-id="593ab-182">在网络视图中查看 Web API 请求的输出</span><span class="sxs-lookup"><span data-stu-id="593ab-182">Viewing the output of the Web API request in the Network view</span></span>*

    > [!NOTE]
    > <span data-ttu-id="593ab-183">Internet Explorer 10 的默认行为现在将询问如果用户想要保存或打开生成的 Web API 调用的流。</span><span class="sxs-lookup"><span data-stu-id="593ab-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="593ab-184">输出将包含 Web API URL 调用的 JSON 结果的文本文件。</span><span class="sxs-lookup"><span data-stu-id="593ab-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="593ab-185">若要查看通过开发人员工具窗口的响应的内容将不取消对话框。</span><span class="sxs-lookup"><span data-stu-id="593ab-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="593ab-186">单击**转到详细视图**按钮以查看有关此 API 调用的响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="593ab-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="593ab-187">![切换到详细视图](build-restful-apis-with-aspnet-web-api/_static/image8.png "切换到详细信息视图")</span><span class="sxs-lookup"><span data-stu-id="593ab-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    *<span data-ttu-id="593ab-188">切换到详细视图</span><span class="sxs-lookup"><span data-stu-id="593ab-188">Switch to Detailed View</span></span>*
9. <span data-ttu-id="593ab-189">单击**响应正文**选项卡以查看实际的 JSON 响应文本。</span><span class="sxs-lookup"><span data-stu-id="593ab-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="593ab-190">![查看 JSON 输出网络监视器中的文本](build-restful-apis-with-aspnet-web-api/_static/image9.png "查看 JSON 输出网络监视器中的文本")</span><span class="sxs-lookup"><span data-stu-id="593ab-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    *<span data-ttu-id="593ab-191">在网络监视器中查看 JSON 输出文本</span><span class="sxs-lookup"><span data-stu-id="593ab-191">Viewing the JSON output text in the network monitor</span></span>*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="593ab-192">任务 3-创建联系人的模型和增加为 Contact Controller</span><span class="sxs-lookup"><span data-stu-id="593ab-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="593ab-193">在本任务中，将创建 API 方法将驻留在其中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="593ab-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="593ab-194">右键单击**模型**文件夹，然后选择**添加 |类...** 从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="593ab-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="593ab-195">![向 web 应用程序中添加新模型](build-restful-apis-with-aspnet-web-api/_static/image10.png "向 web 应用程序中添加新模型")</span><span class="sxs-lookup"><span data-stu-id="593ab-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    *<span data-ttu-id="593ab-196">向 web 应用程序中添加新模型</span><span class="sxs-lookup"><span data-stu-id="593ab-196">Adding a new model to the web application</span></span>*
2. <span data-ttu-id="593ab-197">在中**添加新项**对话框中，将新文件命名**Contact.cs**单击**添加。**</span><span class="sxs-lookup"><span data-stu-id="593ab-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="593ab-198">![创建新的联系人类文件](build-restful-apis-with-aspnet-web-api/_static/image11.png "创建新的联系人类文件")</span><span class="sxs-lookup"><span data-stu-id="593ab-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    *<span data-ttu-id="593ab-199">创建新的联系人类文件</span><span class="sxs-lookup"><span data-stu-id="593ab-199">Creating the new Contact class file</span></span>*
3. <span data-ttu-id="593ab-200">将以下突出显示的代码添加到**联系人**类。</span><span class="sxs-lookup"><span data-stu-id="593ab-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="593ab-201">(代码段- *Web API 实验-Ex01-Contact 类*)</span><span class="sxs-lookup"><span data-stu-id="593ab-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="593ab-202">在**ContactController**类中，选择 word**字符串**中的方法定义**获取**方法，并键入单词*联系人*。</span><span class="sxs-lookup"><span data-stu-id="593ab-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="593ab-203">在键入的单词后, 指示器将出现在单词的开头**联系人**。</span><span class="sxs-lookup"><span data-stu-id="593ab-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="593ab-204">可以按住**Ctrl**键和按句点 （.） 键或单击使用鼠标打开在代码编辑器中，以自动填充帮助对话框图标**使用**指令的模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="593ab-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![对于命名空间声明中使用 Intellisense 协助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *<span data-ttu-id="593ab-206">对于命名空间声明中使用 Intellisense 协助</span><span class="sxs-lookup"><span data-stu-id="593ab-206">Using Intellisense assistance for namespace declarations</span></span>*
5. <span data-ttu-id="593ab-207">修改的代码**获取**方法，以便它返回联系人模型实例的数组。</span><span class="sxs-lookup"><span data-stu-id="593ab-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="593ab-208">(代码段-*返回的联系人列表 Web API 实验-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="593ab-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="593ab-209">按**F5**调试 web 应用程序在浏览器中的。</span><span class="sxs-lookup"><span data-stu-id="593ab-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="593ab-210">若要查看 API 的响应输出所做的更改，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="593ab-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="593ab-211">在浏览器打开后，按**F12**如果开发人员工具还不打开。</span><span class="sxs-lookup"><span data-stu-id="593ab-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="593ab-212">单击**网络**选项卡。</span><span class="sxs-lookup"><span data-stu-id="593ab-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="593ab-213">按**启动捕获**按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="593ab-214">添加 URL 后缀 **/api/contact**到的 URL 地址栏，然后按**Enter**密钥。</span><span class="sxs-lookup"><span data-stu-id="593ab-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="593ab-215">按**转到详细视图**按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="593ab-216">选择**响应正文**选项卡。应会看到表示联系人实例的数组的序列化的形式的 JSON 字符串。</span><span class="sxs-lookup"><span data-stu-id="593ab-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="593ab-217">![JSON 序列化复杂的 Web API 方法调用的输出](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 序列化复杂的 Web API 方法调用的输出")</span><span class="sxs-lookup"><span data-stu-id="593ab-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      *<span data-ttu-id="593ab-218">复杂的 Web API 方法调用的序列化的 JSON 输出</span><span class="sxs-lookup"><span data-stu-id="593ab-218">JSON serialized output of a complex Web API method call</span></span>*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="593ab-219">任务 4-解压缩功能集成到服务层</span><span class="sxs-lookup"><span data-stu-id="593ab-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="593ab-220">此任务将演示如何功能提取到服务层，以方便开发人员可以将其服务的功能与控制器层，从而允许实际完成工作的服务的可重用性。</span><span class="sxs-lookup"><span data-stu-id="593ab-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="593ab-221">在解决方案根目录中创建一个新文件夹并将其命名**Services**。</span><span class="sxs-lookup"><span data-stu-id="593ab-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="593ab-222">若要执行此操作，右键单击**ContactManager**项目，选择**添加** | **新文件夹**，其命名为*服务*。</span><span class="sxs-lookup"><span data-stu-id="593ab-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="593ab-223">![创建服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image14.png "创建服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="593ab-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    *<span data-ttu-id="593ab-224">正在创建服务文件夹</span><span class="sxs-lookup"><span data-stu-id="593ab-224">Creating Services folder</span></span>*
2. <span data-ttu-id="593ab-225">右键单击**Services**文件夹，然后选择**添加 |类...** 从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="593ab-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="593ab-226">![将新类添加到服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image15.png "将新类添加到服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="593ab-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    *<span data-ttu-id="593ab-227">将新类添加到服务文件夹</span><span class="sxs-lookup"><span data-stu-id="593ab-227">Adding a new class to the Services folder</span></span>*
3. <span data-ttu-id="593ab-228">当**添加新项**对话框出现时，将新类命名**ContactRepository**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="593ab-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="593ab-229">![创建一个类文件以包含联系人存储库服务层的代码](build-restful-apis-with-aspnet-web-api/_static/image16.png "创建类文件以包含联系人存储库服务层的代码")</span><span class="sxs-lookup"><span data-stu-id="593ab-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    *<span data-ttu-id="593ab-230">创建一个类文件以包含联系人存储库服务层的代码</span><span class="sxs-lookup"><span data-stu-id="593ab-230">Creating a class file to contain the code for the Contact Repository service layer</span></span>*
4. <span data-ttu-id="593ab-231">添加 using 指令**ContactRepository.cs**文件以包括模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="593ab-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="593ab-232">将以下突出显示的代码添加到**ContactRepository.cs**文件以实现 GetAllContacts 方法。</span><span class="sxs-lookup"><span data-stu-id="593ab-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="593ab-233">(代码段- *Web API 实验-Ex01-联系人存储库*)</span><span class="sxs-lookup"><span data-stu-id="593ab-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="593ab-234">打开**ContactController.cs**文件如果已打开。</span><span class="sxs-lookup"><span data-stu-id="593ab-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="593ab-235">将以下代码添加到该文件的命名空间声明部分使用语句。</span><span class="sxs-lookup"><span data-stu-id="593ab-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="593ab-236">将以下突出显示的代码添加到**ContactController.cs**类添加一个私有字段来表示存储库的实例，以便成员可以产生的类的其余部分使用的服务实现。</span><span class="sxs-lookup"><span data-stu-id="593ab-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="593ab-237">(代码段-*的 Web API 实验-Ex01-联系人控制器*)</span><span class="sxs-lookup"><span data-stu-id="593ab-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="593ab-238">更改**获取**方法，以便它可以使用联系人存储库服务。</span><span class="sxs-lookup"><span data-stu-id="593ab-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="593ab-239">(代码段-*通过存储库返回的联系人列表 Web API 实验-Ex01-*)</span><span class="sxs-lookup"><span data-stu-id="593ab-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="593ab-240">放置一个断点**ContactController**的**获取**方法定义。</span><span class="sxs-lookup"><span data-stu-id="593ab-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="593ab-241">![将断点添加到联系人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "将断点添加到联系人控制器")</span><span class="sxs-lookup"><span data-stu-id="593ab-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   *<span data-ttu-id="593ab-242">将断点添加到联系人控制器</span><span class="sxs-lookup"><span data-stu-id="593ab-242">Adding breakpoints to the contact controller</span></span>*
11. <span data-ttu-id="593ab-243">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="593ab-244">在浏览器打开后，按**F12**打开开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="593ab-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="593ab-245">单击**网络**选项卡。</span><span class="sxs-lookup"><span data-stu-id="593ab-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="593ab-246">单击**启动捕获**按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="593ab-247">追加后缀的地址栏中的 URL **/api/contact**然后按**Enter**加载 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="593ab-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="593ab-248">Visual Studio 2012 应中断一次**获取**方法开始执行。</span><span class="sxs-lookup"><span data-stu-id="593ab-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="593ab-249">![Get 方法中的重大](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 方法中的重大")</span><span class="sxs-lookup"><span data-stu-id="593ab-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   *<span data-ttu-id="593ab-250">Get 方法中的重大</span><span class="sxs-lookup"><span data-stu-id="593ab-250">Breaking within the Get method</span></span>*
17. <span data-ttu-id="593ab-251">按 F5 继续。</span><span class="sxs-lookup"><span data-stu-id="593ab-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="593ab-252">返回到 Internet Explorer 如果它尚未处于焦点模式。</span><span class="sxs-lookup"><span data-stu-id="593ab-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="593ab-253">请注意网络捕获窗口。</span><span class="sxs-lookup"><span data-stu-id="593ab-253">Note the network capture window.</span></span>

    <span data-ttu-id="593ab-254">![网络中显示的 Web API 调用结果的 Internet 资源管理器视图](build-restful-apis-with-aspnet-web-api/_static/image19.png "网络中显示的 Web API 调用结果的 Internet 资源管理器视图")</span><span class="sxs-lookup"><span data-stu-id="593ab-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    *<span data-ttu-id="593ab-255">在 Internet Explorer 中显示的 Web API 调用的结果的网络视图</span><span class="sxs-lookup"><span data-stu-id="593ab-255">Network view in Internet Explorer showing results of the Web API call</span></span>*
19. <span data-ttu-id="593ab-256">单击**转到详细视图**按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="593ab-257">单击**响应正文**选项卡。请注意 JSON 输出的 API 调用，以及它如何表示两个服务层来检索的联系人。</span><span class="sxs-lookup"><span data-stu-id="593ab-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="593ab-258">![在开发人员工具窗口中查看 Web API 的 JSON 输出](build-restful-apis-with-aspnet-web-api/_static/image20.png "开发人员工具窗口中查看 Web API 的 JSON 输出")</span><span class="sxs-lookup"><span data-stu-id="593ab-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    *<span data-ttu-id="593ab-259">在开发人员工具窗口中查看 Web API 的 JSON 输出</span><span class="sxs-lookup"><span data-stu-id="593ab-259">Viewing the JSON output from the Web API in the developer tools window</span></span>*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="593ab-260">练习 2:创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="593ab-261">在此练习中，将实现 POST 和 PUT 方法的联系人管理器中，若要启用与数据编辑功能。</span><span class="sxs-lookup"><span data-stu-id="593ab-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="593ab-262">任务 1-打开 Web API 项目</span><span class="sxs-lookup"><span data-stu-id="593ab-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="593ab-263">在本任务中，你将准备以增强，以便它可以接受用户输入在练习 1 中创建的 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="593ab-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="593ab-264">运行**Visual Studio 2012 Express for Web**，为此，请转到**启动**并键入**VS Express for Web**然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="593ab-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="593ab-265">打开**开始**解决方案位于**源/Ex02-ReadWriteWebAPI/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="593ab-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="593ab-266">否则，可能会继续使用 **最终** 解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="593ab-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="593ab-267">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="593ab-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="593ab-268">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="593ab-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="593ab-269">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="593ab-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="593ab-270">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="593ab-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="593ab-271">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="593ab-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="593ab-272">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="593ab-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="593ab-273">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="593ab-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="593ab-274">打开**Services/ContactRepository.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="593ab-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="593ab-275">任务 2-将数据暂留功能添加到联系人存储库实现</span><span class="sxs-lookup"><span data-stu-id="593ab-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="593ab-276">在此任务中，您将扩展，以便它可以保存并接受用户输入和新联系人实例在练习 1 中创建的 Web API 项目的 ContactRepository 类。</span><span class="sxs-lookup"><span data-stu-id="593ab-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="593ab-277">添加到下面的常量**ContactRepository**类来表示 web 服务器缓存项密钥名称的更高版本在此练习中的名称。</span><span class="sxs-lookup"><span data-stu-id="593ab-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="593ab-278">添加到构造函数**ContactRepository**包含下面的代码。</span><span class="sxs-lookup"><span data-stu-id="593ab-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="593ab-279">(代码段- *Web API 实验-Ex02-联系人存储库构造函数*)</span><span class="sxs-lookup"><span data-stu-id="593ab-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="593ab-280">修改的代码**GetAllContacts**方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="593ab-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="593ab-281">(代码段- *Web API 实验-Ex02-获取所有联系人*)</span><span class="sxs-lookup"><span data-stu-id="593ab-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="593ab-282">此示例用于演示目的，并将使用 web 服务器的缓存作为存储介质，以便这些值将可供多个客户端同时，而不使用会话存储机制或请求存储生存期。</span><span class="sxs-lookup"><span data-stu-id="593ab-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="593ab-283">一个可以使用实体框架、 XML 存储或任何其他一种替代 web 服务器缓存。</span><span class="sxs-lookup"><span data-stu-id="593ab-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="593ab-284">实现一个名为的新方法**SaveContact**到**ContactRepository**类执行的将联系人保存工作。</span><span class="sxs-lookup"><span data-stu-id="593ab-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="593ab-285">**SaveContact**方法应采用单个**联系人**参数和返回一个布尔值，该值指示成功或失败。</span><span class="sxs-lookup"><span data-stu-id="593ab-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="593ab-286">(代码段- *Web API 实验-Ex02-实现 SaveContact 方法*)</span><span class="sxs-lookup"><span data-stu-id="593ab-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="593ab-287">练习 3:使用从 HTML 客户端 Web API</span><span class="sxs-lookup"><span data-stu-id="593ab-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="593ab-288">在此练习中，您将创建 HTML 客户端调用 Web API。</span><span class="sxs-lookup"><span data-stu-id="593ab-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="593ab-289">此客户端将使用 Web API 通过 JavaScript 促进数据交换，并将使用 HTML 标记的 web 浏览器中显示的结果。</span><span class="sxs-lookup"><span data-stu-id="593ab-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="593ab-290">任务 1-修改索引视图用于显示联系人提供 GUI</span><span class="sxs-lookup"><span data-stu-id="593ab-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="593ab-291">在本任务中，将修改 web 应用程序以支持在 HTML 浏览器中显示的现有联系人列表的要求的默认索引视图。</span><span class="sxs-lookup"><span data-stu-id="593ab-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="593ab-292">打开**Visual Studio 2012 Express for Web**如果已打开。</span><span class="sxs-lookup"><span data-stu-id="593ab-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="593ab-293">打开**开始**解决方案位于**源/Ex03-ConsumingWebAPI/开始/** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="593ab-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="593ab-294">否则，可能会继续使用 **最终** 解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="593ab-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="593ab-295">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="593ab-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="593ab-296">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="593ab-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="593ab-297">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="593ab-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="593ab-298">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="593ab-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="593ab-299">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="593ab-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="593ab-300">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="593ab-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="593ab-301">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="593ab-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="593ab-302">打开**Index.cshtml**文件位于**Views/Home**文件夹。</span><span class="sxs-lookup"><span data-stu-id="593ab-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="593ab-303">Div 元素中的 HTML 代码替换 id**正文**，以便它看起来像下面的代码。</span><span class="sxs-lookup"><span data-stu-id="593ab-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="593ab-304">要执行对 Web API 的 HTTP 请求的文件的底部添加以下 Javascript 代码。</span><span class="sxs-lookup"><span data-stu-id="593ab-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="593ab-305">打开**ContactController.cs**文件如果已打开。</span><span class="sxs-lookup"><span data-stu-id="593ab-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="593ab-306">上放置一个断点**获取**方法**ContactController**类。</span><span class="sxs-lookup"><span data-stu-id="593ab-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="593ab-307">![将断点放置在 API 控制器的 Get 方法](build-restful-apis-with-aspnet-web-api/_static/image21.png "将断点放置在 API 控制器的 Get 方法")</span><span class="sxs-lookup"><span data-stu-id="593ab-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    *<span data-ttu-id="593ab-308">将断点放置在 API 控制器的 Get 方法</span><span class="sxs-lookup"><span data-stu-id="593ab-308">Placing a breakpoint on the Get method of the API controller</span></span>*
8. <span data-ttu-id="593ab-309">按 F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="593ab-309">Press **F5** to run the project.</span></span> <span data-ttu-id="593ab-310">在浏览器将加载 HTML 文档。</span><span class="sxs-lookup"><span data-stu-id="593ab-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="593ab-311">请确保您浏览到你的应用程序的根 URL。</span><span class="sxs-lookup"><span data-stu-id="593ab-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="593ab-312">在页面加载并执行 JavaScript，将命中断点和执行代码将暂停控制器中。</span><span class="sxs-lookup"><span data-stu-id="593ab-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="593ab-313">![使用 VS Express for Web 的 Web API 调用到调试](build-restful-apis-with-aspnet-web-api/_static/image22.png "调试到使用 VS Express for Web 的 Web API 调用")</span><span class="sxs-lookup"><span data-stu-id="593ab-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    *<span data-ttu-id="593ab-314">使用 Visual Studio 2012 Express for Web 的 Web API 调用调试</span><span class="sxs-lookup"><span data-stu-id="593ab-314">Debugging into the Web API call using Visual Studio 2012 Express for Web</span></span>*
10. <span data-ttu-id="593ab-315">删除该断点并按**F5**或调试工具栏上的**继续**按钮以继续加载在浏览器中的视图。</span><span class="sxs-lookup"><span data-stu-id="593ab-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="593ab-316">Web API 调用完成后应会看到从 Web API 返回在浏览器中调用显示为列表项的联系人。</span><span class="sxs-lookup"><span data-stu-id="593ab-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="593ab-317">![在浏览器中显示为列表项的 API 调用的结果](build-restful-apis-with-aspnet-web-api/_static/image23.png "API 调用在浏览器中显示为列表项的结果")</span><span class="sxs-lookup"><span data-stu-id="593ab-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    *<span data-ttu-id="593ab-318">在浏览器中显示为列表项的 API 调用的结果</span><span class="sxs-lookup"><span data-stu-id="593ab-318">Results of the API call displayed in the browser as list items</span></span>*
11. <span data-ttu-id="593ab-319">停止调试。</span><span class="sxs-lookup"><span data-stu-id="593ab-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="593ab-320">任务 2-修改索引视图创建联系人提供 GUI</span><span class="sxs-lookup"><span data-stu-id="593ab-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="593ab-321">在此任务中，将继续修改索引视图的 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="593ab-322">窗体将添加到 HTML 页面，将捕获用户输入并将其发送到 Web API 以创建新的联系人，并将创建新的 Web API 控制器方法以从图形用户界面收集日期。</span><span class="sxs-lookup"><span data-stu-id="593ab-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="593ab-323">打开**ContactController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="593ab-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="593ab-324">将新方法添加到名为的控制器类**Post**如下面的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="593ab-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="593ab-325">(代码段- *Web API 实验室-Ex03-Post 方法*)</span><span class="sxs-lookup"><span data-stu-id="593ab-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="593ab-326">打开**Index.cshtml**文件在 Visual Studio 中，如果已打开。</span><span class="sxs-lookup"><span data-stu-id="593ab-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="593ab-327">将以下 HTML 代码之后添加上一任务中的未排序列表添加到该文件。</span><span class="sxs-lookup"><span data-stu-id="593ab-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="593ab-328">在文档底部的脚本元素中，添加以下突出显示的代码以处理按钮单击事件，会将数据发布到 Web API 使用的 HTTP POST 调用。</span><span class="sxs-lookup"><span data-stu-id="593ab-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="593ab-329">在中**ContactController.cs**上, 放置一个断点**Post**方法。</span><span class="sxs-lookup"><span data-stu-id="593ab-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="593ab-330">按**F5**在浏览器中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="593ab-331">页面加载后在浏览器中，键入新的联系人名称和 Id，然后单击**保存**按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="593ab-332">![在浏览器中加载客户端 HTML 文档](build-restful-apis-with-aspnet-web-api/_static/image24.png "在浏览器中加载客户端 HTML 文档")</span><span class="sxs-lookup"><span data-stu-id="593ab-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    *<span data-ttu-id="593ab-333">在浏览器中加载客户端 HTML 文档</span><span class="sxs-lookup"><span data-stu-id="593ab-333">The client HTML document loaded in the browser</span></span>*
9. <span data-ttu-id="593ab-334">当在调试器窗口的分页符**Post**方法，请查阅的属性**联系**参数。</span><span class="sxs-lookup"><span data-stu-id="593ab-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="593ab-335">值应匹配窗体中输入的数据。</span><span class="sxs-lookup"><span data-stu-id="593ab-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="593ab-336">![从客户端发送到 Web API 的联系人对象](build-restful-apis-with-aspnet-web-api/_static/image25.png "联系人对象从客户端发送到 Web API")</span><span class="sxs-lookup"><span data-stu-id="593ab-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    *<span data-ttu-id="593ab-337">正在从客户端发送到 Web API 的联系人对象</span><span class="sxs-lookup"><span data-stu-id="593ab-337">The Contact object being sent to the Web API from the client</span></span>*
10. <span data-ttu-id="593ab-338">单步执行之前在调试器中的方法**响应**创建变量。</span><span class="sxs-lookup"><span data-stu-id="593ab-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="593ab-339">在观察**局部变量**在调试器窗口中的，您将看到已设置的所有属性。</span><span class="sxs-lookup"><span data-stu-id="593ab-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="593ab-340">![在调试器中的创建之后的响应](build-restful-apis-with-aspnet-web-api/_static/image26.png "在调试器中的创建之后的响应")</span><span class="sxs-lookup"><span data-stu-id="593ab-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   *<span data-ttu-id="593ab-341">在调试器中的创建之后响应</span><span class="sxs-lookup"><span data-stu-id="593ab-341">The response following creation in the debugger</span></span>*
11. <span data-ttu-id="593ab-342">如果按下**F5**或单击**继续**请求将在调试器中完成。</span><span class="sxs-lookup"><span data-stu-id="593ab-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="593ab-343">新联系人后切换回浏览器时，已添加到联系人存储的列表**ContactRepository**实现。</span><span class="sxs-lookup"><span data-stu-id="593ab-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="593ab-344">![在浏览器反映成功创建新的联系人实例](build-restful-apis-with-aspnet-web-api/_static/image27.png "浏览器反映成功创建新的连接实例")</span><span class="sxs-lookup"><span data-stu-id="593ab-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   *<span data-ttu-id="593ab-345">在浏览器反映成功创建新的连接实例</span><span class="sxs-lookup"><span data-stu-id="593ab-345">The browser reflects successful creation of the new contact instance</span></span>*

> [!NOTE]
> <span data-ttu-id="593ab-346">此外，可以部署此应用程序对 Azure 以下[附录 c:ASP.NET MVC 4 应用程序使用 Web 部署发布](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="593ab-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>


---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="593ab-347">总结</span><span class="sxs-lookup"><span data-stu-id="593ab-347">Summary</span></span>

<span data-ttu-id="593ab-348">此实验介绍了可以使用新的 ASP.NET Web API 框架和使用框架的 RESTful Web Api 的实现。</span><span class="sxs-lookup"><span data-stu-id="593ab-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="593ab-349">在这里，您可以创建新的存储库可帮助数据暂留使用任意数量的机制并连接该服务而不是作为示例，请参见此体验中提供的简单一个。</span><span class="sxs-lookup"><span data-stu-id="593ab-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="593ab-350">Web API 支持很多其他功能，例如启用以支持 HTTP 和 JSON 或 XML 的任何语言编写的非 HTML 客户端的通信。</span><span class="sxs-lookup"><span data-stu-id="593ab-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="593ab-351">承载 Web API 是典型的 web 应用程序外部的能力也是可能的以及是创建您自己的序列化格式的功能。</span><span class="sxs-lookup"><span data-stu-id="593ab-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="593ab-352">ASP.NET 网站上有一个专用于在 ASP.NET Web API 框架的区域[ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="593ab-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="593ab-353">此站点将继续提供最新信息、 示例和新闻与 Web API，因此它请经常查看如果你想要深入了解创建可用于几乎任何设备或开发框架自定义 Web Api 的画面。</span><span class="sxs-lookup"><span data-stu-id="593ab-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="593ab-354">附录 a:使用代码片段</span><span class="sxs-lookup"><span data-stu-id="593ab-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="593ab-355">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="593ab-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="593ab-356">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="593ab-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="593ab-357">![使用 Visual Studio 代码段代码插入到你的项目](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="593ab-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

*<span data-ttu-id="593ab-358">使用 Visual Studio 代码段代码插入到你的项目</span><span class="sxs-lookup"><span data-stu-id="593ab-358">Using Visual Studio code snippets to insert code into your project</span></span>*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="593ab-359">若要添加代码段使用键盘 (仅限 C#)</span><span class="sxs-lookup"><span data-stu-id="593ab-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="593ab-360">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="593ab-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="593ab-361">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="593ab-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="593ab-362">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="593ab-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="593ab-363">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="593ab-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="593ab-364">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="593ab-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="593ab-365">![开始键入代码段名称](build-restful-apis-with-aspnet-web-api/_static/image29.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="593ab-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    *<span data-ttu-id="593ab-366">开始键入代码段名称</span><span class="sxs-lookup"><span data-stu-id="593ab-366">Start typing the snippet name</span></span>*

    <span data-ttu-id="593ab-367">![按 tab 键以选择突出显示代码段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="593ab-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    *<span data-ttu-id="593ab-368">按 tab 键以选择突出显示代码段</span><span class="sxs-lookup"><span data-stu-id="593ab-368">Press Tab to select the highlighted snippet</span></span>*

    <span data-ttu-id="593ab-369">![再次按 Tab 和代码段将 expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="593ab-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    *<span data-ttu-id="593ab-370">再次按 Tab 和代码段将扩展</span><span class="sxs-lookup"><span data-stu-id="593ab-370">Press Tab again and the snippet will expand</span></span>*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="593ab-371">若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）</span><span class="sxs-lookup"><span data-stu-id="593ab-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="593ab-372">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="593ab-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="593ab-373">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="593ab-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="593ab-374">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="593ab-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="593ab-375">![右键单击你想要插入代码段和选择插入代码段](build-restful-apis-with-aspnet-web-api/_static/image32.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="593ab-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    *<span data-ttu-id="593ab-376">右键单击你想要插入代码段和选择插入代码段</span><span class="sxs-lookup"><span data-stu-id="593ab-376">Right-click where you want to insert the code snippet and select Insert Snippet</span></span>*

    <span data-ttu-id="593ab-377">![通过单击选择列表中中的相关代码片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="593ab-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    *<span data-ttu-id="593ab-378">通过单击选择列表中中的相关代码片段</span><span class="sxs-lookup"><span data-stu-id="593ab-378">Pick the relevant snippet from the list, by clicking on it</span></span>*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="593ab-379">附录 b:安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="593ab-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="593ab-380">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="593ab-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="593ab-381">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="593ab-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="593ab-382">转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="593ab-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="593ab-383">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="593ab-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="593ab-384">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="593ab-384">Click on **Install Now**.</span></span> <span data-ttu-id="593ab-385">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="593ab-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="593ab-386">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="593ab-387">![安装 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="593ab-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    *<span data-ttu-id="593ab-388">安装 Visual Studio Express</span><span class="sxs-lookup"><span data-stu-id="593ab-388">Install Visual Studio Express</span></span>*
4. <span data-ttu-id="593ab-389">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="593ab-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *<span data-ttu-id="593ab-391">接受许可条款</span><span class="sxs-lookup"><span data-stu-id="593ab-391">Accepting the license terms</span></span>*
5. <span data-ttu-id="593ab-392">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="593ab-392">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *<span data-ttu-id="593ab-394">安装进度</span><span class="sxs-lookup"><span data-stu-id="593ab-394">Installation progress</span></span>*
6. <span data-ttu-id="593ab-395">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="593ab-395">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *<span data-ttu-id="593ab-397">安装已完成</span><span class="sxs-lookup"><span data-stu-id="593ab-397">Installation completed</span></span>*
7. <span data-ttu-id="593ab-398">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="593ab-399">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="593ab-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *<span data-ttu-id="593ab-401">VS Express for Web 磁贴</span><span class="sxs-lookup"><span data-stu-id="593ab-401">VS Express for Web tile</span></span>*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="593ab-402">附录 c:ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="593ab-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="593ab-403">本附录将演示如何从 Azure 门户创建新的网站和发布应用程序获取按照本实验中，利用 Azure 提供的 Web 部署发布功能。</span><span class="sxs-lookup"><span data-stu-id="593ab-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="593ab-404">任务 1-从 Azure 门户创建新的 Web 站点</span><span class="sxs-lookup"><span data-stu-id="593ab-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="593ab-405">转到[Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="593ab-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="593ab-406">借助 Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。</span><span class="sxs-lookup"><span data-stu-id="593ab-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="593ab-407">你可以注册[此处](https://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="593ab-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="593ab-408">![登录到 Windows Azure 门户](build-restful-apis-with-aspnet-web-api/_static/image39.png "登录到 Windows Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="593ab-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    *<span data-ttu-id="593ab-409">登录到门户</span><span class="sxs-lookup"><span data-stu-id="593ab-409">Log on to Portal</span></span>*
2. <span data-ttu-id="593ab-410">单击**新建**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="593ab-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="593ab-411">![创建新的 Web 站点](build-restful-apis-with-aspnet-web-api/_static/image40.png "创建新的 Web 站点")</span><span class="sxs-lookup"><span data-stu-id="593ab-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    *<span data-ttu-id="593ab-412">创建新的 Web 站点</span><span class="sxs-lookup"><span data-stu-id="593ab-412">Creating a new Web Site</span></span>*
3. <span data-ttu-id="593ab-413">单击**计算** | **网站**。</span><span class="sxs-lookup"><span data-stu-id="593ab-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="593ab-414">然后选择**快速创建**选项。</span><span class="sxs-lookup"><span data-stu-id="593ab-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="593ab-415">为新网站提供可用的 URL，然后单击**创建网站**。</span><span class="sxs-lookup"><span data-stu-id="593ab-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="593ab-416">Azure 是可以控制和管理在云中运行的 web 应用程序的主机。</span><span class="sxs-lookup"><span data-stu-id="593ab-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="593ab-417">快速创建选项，可部署到 Azure 门户外部的已完成的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="593ab-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="593ab-418">它不包括用于设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="593ab-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="593ab-419">![创建新的网站使用快速创建](build-restful-apis-with-aspnet-web-api/_static/image41.png "创建新的网站使用快速创建")</span><span class="sxs-lookup"><span data-stu-id="593ab-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    *<span data-ttu-id="593ab-420">创建新的网站使用快速创建</span><span class="sxs-lookup"><span data-stu-id="593ab-420">Creating a new Web Site using Quick Create</span></span>*
4. <span data-ttu-id="593ab-421">等到新**网站**创建。</span><span class="sxs-lookup"><span data-stu-id="593ab-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="593ab-422">创建网站后，单击下面的链接**URL**列。</span><span class="sxs-lookup"><span data-stu-id="593ab-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="593ab-423">检查新的 Web 站点正常工作。</span><span class="sxs-lookup"><span data-stu-id="593ab-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="593ab-424">![浏览到新的 web 站点](build-restful-apis-with-aspnet-web-api/_static/image42.png "浏览到新的 web 站点")</span><span class="sxs-lookup"><span data-stu-id="593ab-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    *<span data-ttu-id="593ab-425">浏览到新的 web 站点</span><span class="sxs-lookup"><span data-stu-id="593ab-425">Browsing to the new web site</span></span>*

    <span data-ttu-id="593ab-426">![正在运行的网站](build-restful-apis-with-aspnet-web-api/_static/image43.png "正在运行的网站")</span><span class="sxs-lookup"><span data-stu-id="593ab-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    *<span data-ttu-id="593ab-427">正在运行的网站</span><span class="sxs-lookup"><span data-stu-id="593ab-427">Web site running</span></span>*
6. <span data-ttu-id="593ab-428">返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="593ab-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="593ab-429">![打开网站管理页](build-restful-apis-with-aspnet-web-api/_static/image44.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="593ab-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    *<span data-ttu-id="593ab-430">打开网站管理页</span><span class="sxs-lookup"><span data-stu-id="593ab-430">Opening the Web Site management pages</span></span>*
7. <span data-ttu-id="593ab-431">在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。</span><span class="sxs-lookup"><span data-stu-id="593ab-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="593ab-432">*发布配置文件*包含所有发布到 Azure 的每个启用的发布方法的 web 应用程序所需的信息。</span><span class="sxs-lookup"><span data-stu-id="593ab-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="593ab-433">发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="593ab-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="593ab-434">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="593ab-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="593ab-435">![正在下载网站发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image45.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="593ab-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    *<span data-ttu-id="593ab-436">正在下载网站发布配置文件</span><span class="sxs-lookup"><span data-stu-id="593ab-436">Downloading the Web Site publish profile</span></span>*
8. <span data-ttu-id="593ab-437">下载发布配置文件到已知位置。</span><span class="sxs-lookup"><span data-stu-id="593ab-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="593ab-438">进一步在此练习中将了解如何使用此文件发布到 Azure 的 web 应用程序从 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="593ab-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="593ab-439">![保存发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image46.png "保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="593ab-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    *<span data-ttu-id="593ab-440">保存发布配置文件</span><span class="sxs-lookup"><span data-stu-id="593ab-440">Saving the publish profile file</span></span>*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="593ab-441">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="593ab-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="593ab-442">如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="593ab-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="593ab-443">如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="593ab-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="593ab-444">用于存储应用程序数据库，将需要 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="593ab-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="593ab-445">可以从在 Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**.</span><span class="sxs-lookup"><span data-stu-id="593ab-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="593ab-446">如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="593ab-447">请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="593ab-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="593ab-448">不创建数据库，因为它将在后面的阶段中创建。</span><span class="sxs-lookup"><span data-stu-id="593ab-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="593ab-449">![SQL 数据库服务器仪表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="593ab-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    *<span data-ttu-id="593ab-450">SQL 数据库服务器仪表板</span><span class="sxs-lookup"><span data-stu-id="593ab-450">SQL Database Server Dashboard</span></span>*
2. <span data-ttu-id="593ab-451">在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。</span><span class="sxs-lookup"><span data-stu-id="593ab-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="593ab-452">若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png)按钮。</span><span class="sxs-lookup"><span data-stu-id="593ab-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![添加客户端 IP 地址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *<span data-ttu-id="593ab-454">添加客户端 IP 地址</span><span class="sxs-lookup"><span data-stu-id="593ab-454">Adding Client IP Address</span></span>*
3. <span data-ttu-id="593ab-455">一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="593ab-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *<span data-ttu-id="593ab-457">确认更改</span><span class="sxs-lookup"><span data-stu-id="593ab-457">Confirm Changes</span></span>*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="593ab-458">任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布</span><span class="sxs-lookup"><span data-stu-id="593ab-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="593ab-459">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="593ab-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="593ab-460">在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="593ab-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="593ab-461">![发布应用程序](build-restful-apis-with-aspnet-web-api/_static/image51.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="593ab-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    *<span data-ttu-id="593ab-462">发布此网站</span><span class="sxs-lookup"><span data-stu-id="593ab-462">Publishing the web site</span></span>*
2. <span data-ttu-id="593ab-463">导入发布配置文件保存在第一个任务。</span><span class="sxs-lookup"><span data-stu-id="593ab-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="593ab-464">![导入发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image52.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="593ab-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    *<span data-ttu-id="593ab-465">导入发布配置文件</span><span class="sxs-lookup"><span data-stu-id="593ab-465">Importing publish profile</span></span>*
3. <span data-ttu-id="593ab-466">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="593ab-466">Click **Validate Connection**.</span></span> <span data-ttu-id="593ab-467">验证完成后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="593ab-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="593ab-468">请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。</span><span class="sxs-lookup"><span data-stu-id="593ab-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="593ab-469">![验证连接](build-restful-apis-with-aspnet-web-api/_static/image53.png "验证连接")</span><span class="sxs-lookup"><span data-stu-id="593ab-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    *<span data-ttu-id="593ab-470">验证连接</span><span class="sxs-lookup"><span data-stu-id="593ab-470">Validating connection</span></span>*
4. <span data-ttu-id="593ab-471">在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="593ab-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="593ab-472">![Web 部署配置](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="593ab-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    *<span data-ttu-id="593ab-473">Web 部署配置</span><span class="sxs-lookup"><span data-stu-id="593ab-473">Web deploy configuration</span></span>*
5. <span data-ttu-id="593ab-474">配置数据库连接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="593ab-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="593ab-475">在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。</span><span class="sxs-lookup"><span data-stu-id="593ab-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="593ab-476">在中**用户名**键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="593ab-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="593ab-477">在中**密码**键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="593ab-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="593ab-478">键入新的数据库名称，例如：*MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="593ab-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="593ab-479">![配置目标连接字符串](build-restful-apis-with-aspnet-web-api/_static/image55.png "配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="593ab-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     *<span data-ttu-id="593ab-480">配置目标连接字符串</span><span class="sxs-lookup"><span data-stu-id="593ab-480">Configuring destination connection string</span></span>*
6. <span data-ttu-id="593ab-481">然后单击“确定” 。</span><span class="sxs-lookup"><span data-stu-id="593ab-481">Then click **OK**.</span></span> <span data-ttu-id="593ab-482">当系统提示你创建数据库时，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="593ab-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="593ab-483">![创建数据库](build-restful-apis-with-aspnet-web-api/_static/image56.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="593ab-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    *<span data-ttu-id="593ab-484">创建数据库</span><span class="sxs-lookup"><span data-stu-id="593ab-484">Creating the database</span></span>*
7. <span data-ttu-id="593ab-485">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。</span><span class="sxs-lookup"><span data-stu-id="593ab-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="593ab-486">然后，单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="593ab-486">Then click **Next**.</span></span>

    <span data-ttu-id="593ab-487">![连接字符串指向 SQL 数据库](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL 数据库连接字符串")</span><span class="sxs-lookup"><span data-stu-id="593ab-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    *<span data-ttu-id="593ab-488">连接字符串指向 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="593ab-488">Connection string pointing to SQL Database</span></span>*
8. <span data-ttu-id="593ab-489">在中**预览版**页上，单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="593ab-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="593ab-490">![Web 应用程序发布](build-restful-apis-with-aspnet-web-api/_static/image58.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="593ab-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    *<span data-ttu-id="593ab-491">Web 应用程序发布</span><span class="sxs-lookup"><span data-stu-id="593ab-491">Publishing the web application</span></span>*
9. <span data-ttu-id="593ab-492">在发布过程完成后，在默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="593ab-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="593ab-493">![应用程序发布到 Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "应用程序发布到 Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="593ab-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    *<span data-ttu-id="593ab-494">应用程序发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="593ab-494">Application published to Azure</span></span>*
