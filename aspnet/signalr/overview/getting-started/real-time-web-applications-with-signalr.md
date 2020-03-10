---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 动手实验：包含 SignalR 的实时 Web 应用程序 |Microsoft Docs
author: bradygaster
description: 实时 Web 应用程序可以将服务器端内容实时推送到已连接的客户端。 对于 ASP.NET 开发人员，ASP 。
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431666"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="b9ea5-104">动手实验：包含 SignalR 的实时 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="b9ea5-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>

<span data-ttu-id="b9ea5-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="b9ea5-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="b9ea5-106">下载 Web 训练营培训工具包，10月2015版</span><span class="sxs-lookup"><span data-stu-id="b9ea5-106">Download Web Camps Training Kit, October 2015 Release</span></span>](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> <span data-ttu-id="b9ea5-107">实时 Web 应用程序可以将服务器端内容实时推送到已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="b9ea5-108">对于 ASP.NET 开发人员而言， **ASP.NET SignalR**是一个库，用于向应用程序添加实时 web 功能。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="b9ea5-109">它利用了多个传输，可在客户端和服务器的最佳传输中自动选择最佳的可用传输。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="b9ea5-110">它利用了**WebSocket**，这是一个 HTML5 API，可在浏览器和服务器之间实现双向通信。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="b9ea5-111">**SignalR**还提供了一个简单的高级 API，用于在你的 ASP.NET 应用程序中执行服务器到客户端 RPC （在客户端的浏览器中调用 JavaScript 函数），并为连接管理添加有用的挂钩，如连接/断开连接事件、分组连接和授权。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="b9ea5-112">**SignalR**是对在客户端和服务器之间进行实时工作所需的某些传输的抽象。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="b9ea5-113">**SignalR**连接以 HTTP 开头，然后将其升级到**WebSocket**连接（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="b9ea5-114">**WebSocket**是适用于**SignalR**的理想传输，因为它可以最有效地使用服务器内存，具有最低的延迟，并且具有最基本的功能（如客户端和服务器之间的全双工通信），但它也具有最严格的要求： **WebSocket**要求服务器使用**Windows server 2012**或**windows 8**，以及 **.NET Framework 4.5**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="b9ea5-115">如果未满足这些要求， **SignalR**将尝试使用其他传输进行连接（如*Ajax 长时间轮询*）。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="b9ea5-116">**SignalR** API 包含两种用于在客户端和服务器之间进行通信的模型：**持久性连接**和**中心**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="b9ea5-117">**连接**表示用于发送单接收方、分组或广播消息的简单终结点。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="b9ea5-118">**中心**是一种基于连接 API 构建的更高级别管道，它允许客户端和服务器直接调用方法。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 体系结构](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="b9ea5-120">所有示例代码和代码段都包含在2015年10月发布的 Web 训练营培训工具包中， [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)提供。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-120">All sample code and snippets are included in the Web Camps Training Kit, October 2015 Release, available at [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).</span></span>  <span data-ttu-id="b9ea5-121">请注意，此页上的 "安装程序" 链接不再工作。改为使用 "资产" 部分下的链接之一。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-121">Please note that the Installer link on that page no longer works; use one of the links under the Assets section instead.</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="b9ea5-122">概述</span><span class="sxs-lookup"><span data-stu-id="b9ea5-122">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b9ea5-123">目标</span><span class="sxs-lookup"><span data-stu-id="b9ea5-123">Objectives</span></span>

<span data-ttu-id="b9ea5-124">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="b9ea5-125">使用 SignalR 将通知从服务器发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-125">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="b9ea5-126">使用**SQL Server**Scale Out SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-126">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b9ea5-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="b9ea5-127">Prerequisites</span></span>

<span data-ttu-id="b9ea5-128">完成本动手实验需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="b9ea5-129">Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="b9ea5-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b9ea5-130">安装</span><span class="sxs-lookup"><span data-stu-id="b9ea5-130">Setup</span></span>

<span data-ttu-id="b9ea5-131">若要运行此动手实验中的练习，您需要先设置您的环境。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-131">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="b9ea5-132">打开 Windows 资源管理器窗口并浏览到实验室的**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-132">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="b9ea5-133">右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-133">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="b9ea5-134">如果显示了 "用户帐户控制" 对话框，请确认操作以继续。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-134">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="b9ea5-135">确保在运行安装过程之前，您已检查本实验的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-135">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="b9ea5-136">使用代码段</span><span class="sxs-lookup"><span data-stu-id="b9ea5-136">Using the Code Snippets</span></span>

<span data-ttu-id="b9ea5-137">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-137">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="b9ea5-138">为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-138">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="b9ea5-139">每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-139">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="b9ea5-140">请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-140">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="b9ea5-141">在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-141">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="b9ea5-142">如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-142">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b9ea5-143">练习</span><span class="sxs-lookup"><span data-stu-id="b9ea5-143">Exercises</span></span>

<span data-ttu-id="b9ea5-144">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-144">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="b9ea5-145">使用 SignalR 处理实时数据</span><span class="sxs-lookup"><span data-stu-id="b9ea5-145">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="b9ea5-146">使用 SQL Server 横向扩展</span><span class="sxs-lookup"><span data-stu-id="b9ea5-146">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="b9ea5-147">完成本实验的估计时间： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="b9ea5-147">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="b9ea5-148">首次启动 Visual Studio 时，必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-148">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="b9ea5-149">每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-149">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="b9ea5-150">此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-150">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="b9ea5-151">如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-151">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="b9ea5-152">练习1：使用 SignalR 处理实时数据</span><span class="sxs-lookup"><span data-stu-id="b9ea5-152">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="b9ea5-153">尽管聊天通常用作示例，但您可以使用实时 Web 功能完成更多工作。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-153">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="b9ea5-154">用户每次刷新网页以查看新数据或页面实现 Ajax 长轮询以检索新数据时，都可以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-154">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="b9ea5-155">SignalR 支持**服务器推送**或**广播**功能;它会自动处理连接管理。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-155">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="b9ea5-156">对于客户端-服务器通信的经典 HTTP 连接，为每个请求重新建立连接，但 SignalR 在客户端和服务器之间提供持续连接。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-156">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="b9ea5-157">在 SignalR 中，服务器代码使用远程过程调用（RPC）来调用浏览器中的客户端代码，而不是我们今天知道的请求-响应模型。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-157">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="b9ea5-158">在此练习中，您将配置**书呆子测验**应用程序以使用 SignalR 显示带有更新的指标的统计信息仪表板，而无需刷新整个页面。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-158">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="b9ea5-159">任务1–浏览书呆子测验 Statistics 页面</span><span class="sxs-lookup"><span data-stu-id="b9ea5-159">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="b9ea5-160">在此任务中，您将完成应用程序并验证统计信息页的显示方式，以及如何改进信息的更新方式。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-160">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="b9ea5-161">打开**Web Visual Studio Express 2013** ，然后打开**Source\Ex1-WorkingWithRealTimeData\Begin**文件夹中的**GeekQuiz**解决方案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-161">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="b9ea5-162">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-162">Press **F5** to run the solution.</span></span> <span data-ttu-id="b9ea5-163">"**登录**" 页应出现在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-163">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="b9ea5-164">![运行解决方案](real-time-web-applications-with-signalr/_static/image2.png "运行解决方案")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-164">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="b9ea5-165">*运行解决方案*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-165">*Running the solution*</span></span>
3. <span data-ttu-id="b9ea5-166">在页面右上角单击 "**注册**"，以在应用程序中创建新用户。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-166">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="b9ea5-167">![注册链接](real-time-web-applications-with-signalr/_static/image3.png "注册链接")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-167">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="b9ea5-168">*注册链接*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-168">*Register link*</span></span>
4. <span data-ttu-id="b9ea5-169">在 "**注册**" 页上，输入**用户名**和**密码**，然后单击 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-169">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="b9ea5-170">![注册用户](real-time-web-applications-with-signalr/_static/image4.png "注册用户")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-170">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="b9ea5-171">*注册用户*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-171">*Registering a user*</span></span>
5. <span data-ttu-id="b9ea5-172">应用程序将注册新帐户，并对用户进行身份验证，并重新定向回显示第一个测验问题的主页。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-172">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="b9ea5-173">在新窗口中打开 "**统计信息**" 页，并将 "**主页**" 和 "**统计信息**" 页并排放置。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-173">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="b9ea5-174">![并行窗口](real-time-web-applications-with-signalr/_static/image5.png "并行窗口")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-174">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="b9ea5-175">*并行窗口*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-175">*Side-by-side windows*</span></span>
7. <span data-ttu-id="b9ea5-176">在**主页**中，通过单击其中一个选项来回答问题。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-176">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="b9ea5-177">![回答问题](real-time-web-applications-with-signalr/_static/image6.png "回答问题")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-177">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="b9ea5-178">*回答问题*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-178">*Answering a question*</span></span>
8. <span data-ttu-id="b9ea5-179">单击其中一个按钮后，将出现答案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-179">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="b9ea5-180">![答案正确](real-time-web-applications-with-signalr/_static/image7.png "答案正确")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-180">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="b9ea5-181">*正确回答的问题*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-181">*Question answered correctly*</span></span>
9. <span data-ttu-id="b9ea5-182">请注意，"统计信息" 页中提供的信息已过时。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-182">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="b9ea5-183">刷新页面以查看更新后的结果。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-183">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="b9ea5-184">![统计信息页](real-time-web-applications-with-signalr/_static/image8.png "统计信息页")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-184">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="b9ea5-185">*统计信息页*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-185">*Statistics page*</span></span>
10. <span data-ttu-id="b9ea5-186">返回到 Visual Studio，然后停止调试。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-186">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="b9ea5-187">任务 2-将 SignalR 添加到书呆子测验以显示联机图表</span><span class="sxs-lookup"><span data-stu-id="b9ea5-187">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="b9ea5-188">在此任务中，将 SignalR 添加到解决方案，并在将新的答案发送到服务器时将更新发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-188">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="b9ea5-189">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后单击 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-189">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="b9ea5-190">在 "**包管理器控制台**" 窗口中，执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-190">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="b9ea5-191">![SignalR 包安装](real-time-web-applications-with-signalr/_static/image9.png "SignalR 包安装")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-191">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="b9ea5-192">*SignalR 包安装*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-192">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="b9ea5-193">在安装全新 MVC 5 应用程序的**SignalR** NuGet 包版本2.0.2 时，需要在安装 SignalR 之前，手动将**OWIN**包更新到2.0.1 版（或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-193">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="b9ea5-194">为此，可以在**Package Manager Console**中执行以下脚本：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-194">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="b9ea5-195">在未来版本的 SignalR 中，OWIN 依赖项会自动更新。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-195">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="b9ea5-196">在**解决方案资源管理器**中，展开 "**脚本**" 文件夹，注意 SignalR *js*文件已添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-196">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="b9ea5-197">![SignalR JavaScript 引用](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 引用")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-197">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="b9ea5-198">*SignalR JavaScript 引用*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-198">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="b9ea5-199">在**解决方案资源管理器**中，右键单击**GeekQuiz**项目，选择 "**添加** | "**新建文件夹**"，并将其命名为"**中心**"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-199">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="b9ea5-200">右键单击 "**中心**" 文件夹，然后选择 "**添加 |新建项**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-200">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="b9ea5-201">![添加新项](real-time-web-applications-with-signalr/_static/image11.png "添加新项")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-201">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="b9ea5-202">*添加新项*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-202">*Add new item*</span></span>
6. <span data-ttu-id="b9ea5-203">在 "**添加新项**" 对话框中，选择**视觉C#对象 |Web |SignalR**节点在左窗格中，从中间窗格中选择 " **SignalR Hub 类（v2）** "，将文件命名为**StatisticsHub.cs** ，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-203">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="b9ea5-204">!["添加新项" 对话框](real-time-web-applications-with-signalr/_static/image12.png ""添加新项" 对话框")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-204">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="b9ea5-205">*"添加新项" 对话框*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-205">*Add new item dialog box*</span></span>
7. <span data-ttu-id="b9ea5-206">将**StatisticsHub**类中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-206">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="b9ea5-207">（代码段- *RealTimeSignalR-Ex1-StatisticsHubClass*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-207">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="b9ea5-208">打开**Startup.cs** ，并在**配置**方法的末尾添加以下行。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-208">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="b9ea5-209">（代码段- *RealTimeSignalR-Ex1-MapSignalR*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-209">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="b9ea5-210">打开 "**服务**" 文件夹内的 " **StatisticsService.cs** " 页，并添加以下 using 指令。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-210">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="b9ea5-211">（代码段- *RealTimeSignalR-Ex1-UsingDirectives*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-211">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="b9ea5-212">若要通知连接的客户端的更新，请先检索当前连接的**上下文**对象。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-212">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="b9ea5-213">**Hub**对象包含向单个客户端发送消息或向所有连接的客户端发送消息的方法。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-213">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="b9ea5-214">将以下方法添加到**StatisticsService**类，以便广播统计信息数据。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-214">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="b9ea5-215">（代码段- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-215">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="b9ea5-216">在上面的代码中，你使用的是任意方法名称来调用客户端上的函数（即： *updateStatistics*）。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-216">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="b9ea5-217">指定的方法名称被解释为动态对象，这意味着它没有 IntelliSense 或编译时验证。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-217">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="b9ea5-218">在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-218">The expression is evaluated at run time.</span></span> <span data-ttu-id="b9ea5-219">当执行方法调用时，SignalR 会将方法名称和参数值发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-219">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="b9ea5-220">如果客户端具有与名称匹配的方法，则调用该方法并将参数值传递给它。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-220">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="b9ea5-221">如果在客户端上找不到匹配的方法，则不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-221">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="b9ea5-222">有关详细信息，请参阅[ASP.NET SignalR HUB API 指南](../guide-to-the-api/hubs-api-guide-server.md)。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-222">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="b9ea5-223">打开 "**控制器**" 文件夹内的 " **TriviaController.cs** " 页，并添加以下 using 指令。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-223">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="b9ea5-224">将以下突出显示的代码添加到**Post**操作方法。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-224">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="b9ea5-225">（代码段- *RealTimeSignalR-Ex1-NotifyUpdatesCall*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-225">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="b9ea5-226">在视图中打开 " **Statistics** " 页 **|主**文件夹。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-226">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="b9ea5-227">找到**脚本**部分，并在部分开头添加以下脚本引用。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-227">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="b9ea5-228">（代码段- *RealTimeSignalR-Ex1-SignalRScriptReferences*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-228">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="b9ea5-229">将 SignalR 和其他脚本库添加到 Visual Studio 项目时，包管理器可能会安装比本主题中所示版本更新的 SignalR 脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-229">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="b9ea5-230">请确保代码中的脚本引用与你的项目中安装的脚本库的版本相匹配。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-230">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="b9ea5-231">添加以下突出显示的代码，以将客户端连接到 SignalR 中心，并在从中心接收到新消息时更新统计信息数据。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-231">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="b9ea5-232">（代码段- *RealTimeSignalR-Ex1-SignalRClientCode*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="b9ea5-233">在此代码中，你将创建一个中心代理并注册事件处理程序以侦听服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-233">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="b9ea5-234">在这种情况下，需要侦听通过*updateStatistics*方法发送的消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-234">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="b9ea5-235">任务3–运行解决方案</span><span class="sxs-lookup"><span data-stu-id="b9ea5-235">Task 3 – Running the Solution</span></span>

<span data-ttu-id="b9ea5-236">在此任务中，您将运行解决方案以验证是否在回答新问题后使用 SignalR 自动更新了统计信息视图。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-236">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="b9ea5-237">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-237">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9ea5-238">如果尚未登录到应用程序，请以在任务1中创建的用户身份登录。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-238">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="b9ea5-239">在新窗口中打开 "**统计信息**" 页，并将 "**主页**" 和 "**统计信息**" 页并排放置在任务1中。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-239">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="b9ea5-240">在**主页**中，通过单击其中一个选项来回答问题。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-240">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="b9ea5-241">![回答其他问题](real-time-web-applications-with-signalr/_static/image13.png "回答其他问题")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-241">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="b9ea5-242">*回答其他问题*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-242">*Answering another question*</span></span>
4. <span data-ttu-id="b9ea5-243">单击其中一个按钮后，将出现答案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-243">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="b9ea5-244">请注意，在用更新的信息回答问题后，会自动更新页面上的统计信息，而无需刷新整个页面。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-244">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="b9ea5-245">![应答后刷新的统计信息页](real-time-web-applications-with-signalr/_static/image14.png "应答后刷新的统计信息页")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-245">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="b9ea5-246">*应答后刷新的统计信息页*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-246">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="b9ea5-247">练习2：使用 SQL Server 进行扩展</span><span class="sxs-lookup"><span data-stu-id="b9ea5-247">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="b9ea5-248">缩放 web 应用程序时，通常可以选择*纵向扩展*和*横向扩展*选项。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-248">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="b9ea5-249">*向上缩放*意味着使用较大的服务器，具有更多资源（CPU、RAM 等），而向*外扩展*意味着添加更多服务器来处理负载。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-249">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="b9ea5-250">后一种问题是客户端可以路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-250">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="b9ea5-251">连接到一台服务器的客户端将不会接收来自其他服务器的消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-251">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="b9ea5-252">可以通过使用名为*底板*的组件来解决这些问题，以便在服务器之间转发消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-252">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="b9ea5-253">启用底板后，每个应用程序实例会将消息发送到底板，并将其转发到其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-253">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="b9ea5-254">目前有三种类型的 SignalR：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-254">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="b9ea5-255">**Windows Azure 服务总线**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-255">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="b9ea5-256">服务总线是一种消息传递基础结构，允许组件发送松散耦合的消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-256">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="b9ea5-257">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-257">**SQL Server**.</span></span> <span data-ttu-id="b9ea5-258">SQL Server 底板将消息写入 SQL 表中。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-258">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="b9ea5-259">底板使用 Service Broker 来实现高效的消息传送。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-259">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="b9ea5-260">不过，如果未启用 Service Broker，它也会起作用。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-260">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="b9ea5-261">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-261">**Redis**.</span></span> <span data-ttu-id="b9ea5-262">Redis 是内存中的键-值存储。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-262">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="b9ea5-263">Redis 支持发布/订阅（"pub/sub"）模式来发送消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-263">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="b9ea5-264">每条消息都是通过消息总线发送的。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-264">Every message is sent through a message bus.</span></span> <span data-ttu-id="b9ea5-265">消息总线实现了[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，该接口提供发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-265">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="b9ea5-266">通过使用为该底板设计的总线替换默认的**IMessageBus** ，可以使用底板。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-266">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="b9ea5-267">每个服务器实例通过总线连接到底板。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-267">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="b9ea5-268">发送消息时，消息会发送到底板，并且底板会将其发送到每台服务器。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-268">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="b9ea5-269">当服务器从底板收到消息时，它会将消息存储在它的本地缓存中。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-269">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="b9ea5-270">服务器随后将消息从其本地缓存传递给客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-270">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="b9ea5-271">有关 SignalR 底板工作方式的详细信息，请阅读此[文](../performance/scaleout-in-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-271">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b9ea5-272">在某些情况下，底板可能成为瓶颈。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-272">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="b9ea5-273">下面是一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-273">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="b9ea5-274">[服务器广播](tutorial-server-broadcast-with-signalr.md)（例如，股票行情）：对于此方案，背板工作良好，因为服务器控制发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-274">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="b9ea5-275">[客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）：在这种情况下，如果消息数量随客户端数量的增加，则底板可能是瓶颈;也就是说，如果随着更多客户端的加入，消息的速率会按比例增加。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-275">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="b9ea5-276">[高频实时](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）：不建议在此方案中使用底板。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-276">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

<span data-ttu-id="b9ea5-277">在此练习中，您将使用**SQL Server**在**书呆子测验**应用程序间分发消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-277">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="b9ea5-278">你将在一台测试计算机上运行这些任务来了解如何设置配置，但为了获得完整效果，你将需要将 SignalR 应用程序部署到两个或更多服务器。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-278">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="b9ea5-279">还必须在一台服务器或单独的专用服务器上安装 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-279">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![使用 SQL Server 关系图 Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="b9ea5-281">任务 1-了解方案</span><span class="sxs-lookup"><span data-stu-id="b9ea5-281">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="b9ea5-282">在此任务中，你将在本地计算机上运行2个模拟多个 IIS 实例的**书呆子**的实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-282">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="b9ea5-283">在这种情况下，当在一个应用程序上回答琐碎内容问题时，不会在第二个实例的 "统计信息" 页上收到更新通知。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-283">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="b9ea5-284">此模拟类似于在多个实例上部署应用程序，并使用负载均衡器与它们进行通信的环境。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-284">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="b9ea5-285">打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-ScalingOutWithSQLServer/begin**文件夹中的**Begin .sln**解决方案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-285">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="b9ea5-286">加载后，你会注意到**服务器资源管理器**解决方案包含两个具有相同结构但名称不同的项目。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-286">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="b9ea5-287">这会模拟在本地计算机上运行同一应用程序的两个实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-287">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="b9ea5-288">![模拟书呆子测验的2个实例的开始解决方案](real-time-web-applications-with-signalr/_static/image16.png "模拟书呆子测验的2个实例的开始解决方案")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-288">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="b9ea5-289">*模拟书呆子测验的2个实例的开始解决方案*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-289">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="b9ea5-290">右键单击解决方案节点，然后选择 "**属性**"，打开解决方案的 "属性" 页。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-290">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="b9ea5-291">在 "**启动项目**" 下，选择 "**多个启动项目**"，并更改两个项目的 "**操作**"*值。*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-291">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="b9ea5-292">![启动多个项目](real-time-web-applications-with-signalr/_static/image17.png "启动多个项目")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-292">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="b9ea5-293">*启动多个项目*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-293">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="b9ea5-294">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-294">Press **F5** to run the solution.</span></span> <span data-ttu-id="b9ea5-295">应用程序将在不同的端口中启动两个**书呆子测验**实例，模拟同一个应用程序的多个实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-295">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="b9ea5-296">将其中一个浏览器固定在屏幕的左侧和右侧。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-296">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="b9ea5-297">使用你的凭据登录或注册新用户。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-297">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="b9ea5-298">登录后，将 "琐碎内容" 页保留在左侧，然后在浏览器中的右侧浏览到 "**统计信息**" 页。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-298">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![并行书呆子测验](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="b9ea5-300">*并行书呆子测验*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-300">*Geek Quiz Side by Side*</span></span>

    ![不同端口中的书呆子测验](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="b9ea5-302">*不同端口中的书呆子测验*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-302">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="b9ea5-303">在左侧浏览器中开始回答问题，你会注意到未更新正确浏览器中的 "**统计信息**" 页。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-303">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="b9ea5-304">这是因为**SignalR**使用本地缓存在其客户端上分发消息，此方案模拟多个实例，因此不会在它们之间共享缓存。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-304">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="b9ea5-305">可以通过测试相同的步骤，但使用单个应用来验证**SignalR**是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-305">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="b9ea5-306">在以下任务中，您将配置底板以跨实例复制消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-306">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="b9ea5-307">返回到 Visual Studio，然后停止调试。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-307">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="b9ea5-308">任务2–创建 SQL Server 底板</span><span class="sxs-lookup"><span data-stu-id="b9ea5-308">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="b9ea5-309">在此任务中，你将创建一个将用作**书呆子测验**应用程序的底板的数据库。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-309">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="b9ea5-310">你将使用**SQL Server 对象资源管理器**浏览服务器并初始化数据库。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-310">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="b9ea5-311">此外，还将启用**Service Broker**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-311">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="b9ea5-312">在**Visual Studio**中，打开菜单**视图**并选择**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-312">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="b9ea5-313">右键单击 " **SQL Server** " 节点，然后选择 "**添加 SQL Server ...** " 选项，以连接到 LocalDB 实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-313">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="b9ea5-314">![添加 SQL Server 实例](real-time-web-applications-with-signalr/_static/image20.png "添加 SQL Server 实例")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-314">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="b9ea5-315">*将 SQL Server 实例添加到 SQL Server 对象资源管理器*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-315">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="b9ea5-316">将**服务器名称**设置为 *（localdb） \v11.0* ，并将**Windows 身份验证**设置为身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-316">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="b9ea5-317">单击“ **连接** ”以继续。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-317">Click **Connect** to continue.</span></span>

    <span data-ttu-id="b9ea5-318">![连接到 LocalDB](real-time-web-applications-with-signalr/_static/image21.png "连接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-318">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="b9ea5-319">*连接到 LocalDB*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-319">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="b9ea5-320">现在，你已连接到 LocalDB 实例，你将需要创建一个将代表 SignalR 的 SQL Server 底板的数据库。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-320">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="b9ea5-321">为此，请右键单击 "**数据库**" 节点，然后选择 "**添加新数据库**"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-321">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="b9ea5-322">![添加新数据库](real-time-web-applications-with-signalr/_static/image22.png "添加新数据库")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-322">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="b9ea5-323">*添加新数据库*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-323">*Adding a new database*</span></span>
5. <span data-ttu-id="b9ea5-324">将数据库名称设置为*SignalR* ，并单击 **"确定"** 以创建它。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-324">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="b9ea5-325">![创建 SignalR 数据库](real-time-web-applications-with-signalr/_static/image23.png "创建 SignalR 数据库")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-325">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="b9ea5-326">*创建 SignalR 数据库*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-326">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9ea5-327">您可以为数据库选择任何名称。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-327">You can choose any name for the database.</span></span>
6. <span data-ttu-id="b9ea5-328">为了更有效地从底板接收更新，建议为数据库启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-328">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="b9ea5-329">Service Broker 为 SQL Server 中的消息传递和排队提供本机支持。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-329">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="b9ea5-330">在没有 Service Broker 的情况下，底板也能正常工作。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-330">The backplane also works without Service Broker.</span></span> <span data-ttu-id="b9ea5-331">右键单击数据库并选择 "**新建查询**" 以打开新的查询。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-331">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="b9ea5-332">![打开新查询](real-time-web-applications-with-signalr/_static/image24.png "打开新查询")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-332">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="b9ea5-333">*打开新查询*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-333">*Opening a New Query*</span></span>
7. <span data-ttu-id="b9ea5-334">若要检查是否启用了 Service Broker，请在**sys.databases**目录视图中查询**是否\_Broker\_enabled**列。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-334">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="b9ea5-335">在最近打开的查询窗口中执行以下脚本。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-335">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="b9ea5-336">![查询 Service Broker 状态](real-time-web-applications-with-signalr/_static/image25.png "查询 Service Broker 状态")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-336">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="b9ea5-337">*查询 Service Broker 状态*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-337">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="b9ea5-338">如果的值为数据库 **\_broker\_enabled**列 &quot;0&quot;，请使用以下命令启用它。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-338">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="b9ea5-339">将 **&lt;数据库&gt;** 替换为创建数据库时设置的名称（例如： SignalR）。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-339">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="b9ea5-340">![启用 Service Broker](real-time-web-applications-with-signalr/_static/image26.png "启用 Service Broker")</span><span class="sxs-lookup"><span data-stu-id="b9ea5-340">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="b9ea5-341">*启用 Service Broker*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-341">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9ea5-342">如果此查询显示为死锁，请确保没有任何应用程序连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-342">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="b9ea5-343">任务3–配置 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="b9ea5-343">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="b9ea5-344">在此任务中，你将配置**书呆子测验**以连接到 SQL Server 底板。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-344">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="b9ea5-345">你将首先添加**SignalR** NuGet 包，并将连接字符串设置为你的底板数据库。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-345">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="b9ea5-346">从 "**工具**" > **NuGet 包管理器**"中打开**包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-346">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="b9ea5-347">请确保在 "**默认项目**" 下拉列表中选择 " **GeekQuiz**项目"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-347">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="b9ea5-348">键入以下命令以安装**SignalR** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-348">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="b9ea5-349">重复上述步骤，但这一次是 project **GeekQuiz2**。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-349">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="b9ea5-350">若要配置 SQL Server 底板，请打开**GeekQuiz**项目的**Startup.cs**文件并将以下代码添加到**configure**方法。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-350">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="b9ea5-351">将**数据库&gt;** 替换为在创建 SQL Server 底板时使用的数据库名称&lt;。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-351">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="b9ea5-352">对于**GeekQuiz2**项目，请重复此步骤。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-352">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="b9ea5-353">（代码段- *RealTimeSignalR-buildingappswithcachingservice-ex2-getproducts latency-cs-StartupConfiguration*）</span><span class="sxs-lookup"><span data-stu-id="b9ea5-353">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="b9ea5-354">现在，两个项目都配置为使用 SQL Server 底板，请按**F5**同时运行它们。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-354">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="b9ea5-355">同样， **Visual Studio**将在不同的端口中启动**书呆子测验**的两个实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-355">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="b9ea5-356">在屏幕的左侧和右侧固定其中一个浏览器，然后用您的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-356">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="b9ea5-357">将琐碎内容页保留在左侧，并在右侧浏览器中 pagein 到 " **Statistics** "。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-357">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="b9ea5-358">在左侧浏览器中开始回答问题。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-358">Start answering questions in the left browser.</span></span> <span data-ttu-id="b9ea5-359">这一次，由于底板将更新**统计信息**页。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-359">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="b9ea5-360">在应用程序之间切换（**统计信息**现在位于左侧，**琐碎内容**位于右侧），并重复该测试以验证其是否适用于这两个实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-360">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="b9ea5-361">该底板充当每个连接服务器的消息*共享缓存*，每个服务器都将这些消息存储在自己的本地缓存中，以分发到连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-361">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="b9ea5-362">返回到 Visual Studio，然后停止调试。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-362">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="b9ea5-363">SQL Server 底板组件会自动在指定的数据库上生成必要的表。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-363">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="b9ea5-364">在**SQL Server 对象资源管理器**面板中，打开为底板创建的数据库（例如： SignalR），然后展开其表。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-364">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="b9ea5-365">应会看到以下表：</span><span class="sxs-lookup"><span data-stu-id="b9ea5-365">You should see the following tables:</span></span>

    ![底板生成的表](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="b9ea5-367">*底板生成的表*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-367">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="b9ea5-368">右键单击 **\_0**表的 SignalR，然后选择 "**查看数据**"。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-368">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![查看 SignalR 底板消息表](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="b9ea5-370">*查看 SignalR 底板消息表*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-370">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="b9ea5-371">解答琐碎内容问题时，可以看到发送到**中心**的不同消息。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-371">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="b9ea5-372">该底板将这些消息分发给任何连接的实例。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-372">The backplane distributes these messages to any connected instance.</span></span>

    ![底板消息表](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="b9ea5-374">*底板消息表*</span><span class="sxs-lookup"><span data-stu-id="b9ea5-374">*Backplane Messages Table*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b9ea5-375">摘要</span><span class="sxs-lookup"><span data-stu-id="b9ea5-375">Summary</span></span>

<span data-ttu-id="b9ea5-376">在此动手实验中，你已了解如何使用**集线器**将**SignalR**添加到你的应用程序并将通知从服务器发送到连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-376">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="b9ea5-377">此外，还了解了如何在多个 IIS 实例中部署应用程序时，通过使用*底板*组件来扩展应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9ea5-377">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
