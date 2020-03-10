---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 教程：入门 SignalR 1.x 和 MVC 4 |Microsoft Docs
author: bradygaster
description: 使用 ASP.NET SignalR 和 ASP.NET MVC 4 构建实时聊天应用程序。
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468068"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="250e6-103">教程：入门 SignalR 1.x 和 MVC 4</span><span class="sxs-lookup"><span data-stu-id="250e6-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="250e6-104">作者： [Fletcher](https://github.com/pfletcher)、 [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="250e6-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="250e6-105">本教程介绍如何使用 ASP.NET SignalR 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="250e6-106">将 SignalR 添加到 MVC 4 应用程序，并创建聊天视图来发送和显示消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="250e6-107">概述</span><span class="sxs-lookup"><span data-stu-id="250e6-107">Overview</span></span>

<span data-ttu-id="250e6-108">本教程介绍了 ASP.NET SignalR 和 ASP.NET MVC 4 的实时 web 应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="250e6-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="250e6-109">本教程使用与[SignalR 入门教程](tutorial-getting-started-with-signalr.md)相同的聊天应用程序代码，但演示了如何将其添加到基于 Internet 模板的 MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="250e6-110">在本主题中，你将学习以下 SignalR 开发任务：</span><span class="sxs-lookup"><span data-stu-id="250e6-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="250e6-111">将 SignalR 库添加到 MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="250e6-112">创建集线器类以将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="250e6-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="250e6-113">使用网页中的 SignalR jQuery library 发送消息并显示中心更新。</span><span class="sxs-lookup"><span data-stu-id="250e6-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="250e6-114">以下屏幕截图显示了在浏览器中运行的已完成的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![聊天实例](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="250e6-116">个</span><span class="sxs-lookup"><span data-stu-id="250e6-116">Sections:</span></span>

- [<span data-ttu-id="250e6-117">设置项目</span><span class="sxs-lookup"><span data-stu-id="250e6-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="250e6-118">运行示例</span><span class="sxs-lookup"><span data-stu-id="250e6-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="250e6-119">检查代码</span><span class="sxs-lookup"><span data-stu-id="250e6-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="250e6-120">后续步骤</span><span class="sxs-lookup"><span data-stu-id="250e6-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="250e6-121">设置项目</span><span class="sxs-lookup"><span data-stu-id="250e6-121">Set up the Project</span></span>

<span data-ttu-id="250e6-122">先决条件：</span><span class="sxs-lookup"><span data-stu-id="250e6-122">Prerequisites:</span></span>

- <span data-ttu-id="250e6-123">Visual Studio 2010 SP1、Visual Studio 2012 或 Visual Studio 2012 Express。</span><span class="sxs-lookup"><span data-stu-id="250e6-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="250e6-124">如果没有 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)以获取免费的 visual Studio 2012 Express 开发工具。</span><span class="sxs-lookup"><span data-stu-id="250e6-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="250e6-125">对于 Visual Studio 2010，请安装[ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)。</span><span class="sxs-lookup"><span data-stu-id="250e6-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="250e6-126">本部分介绍如何创建 ASP.NET MVC 4 应用程序、如何添加 SignalR 库，以及如何创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="250e6-127">在 Visual Studio 中，创建一个 ASP.NET MVC 4 应用程序，将其命名为 SignalRChat，然后单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="250e6-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="250e6-128">在 VS 2010 中，选择 "Framework 版本" 下拉控件中的 **.NET Framework 4** 。</span><span class="sxs-lookup"><span data-stu-id="250e6-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="250e6-129">SignalR 代码在 .NET Framework 版本4和4.5 上运行。</span><span class="sxs-lookup"><span data-stu-id="250e6-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![创建 mvc web](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="250e6-131">选择 "Internet 应用程序" 模板，清除 "**创建单元测试项目**" 选项，然后单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="250e6-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![创建 mvc internet 站点](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="250e6-133">**> NuGet 包管理器 "> 包管理器控制台**中打开" 工具 "，并运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="250e6-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="250e6-134">此步骤将向项目添加一组启用 SignalR 功能的脚本文件和程序集引用。</span><span class="sxs-lookup"><span data-stu-id="250e6-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="250e6-135">在**解决方案资源管理器**展开 "脚本" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="250e6-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="250e6-136">请注意，SignalR 的脚本库已添加到项目。</span><span class="sxs-lookup"><span data-stu-id="250e6-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![库引用](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="250e6-138">在**解决方案资源管理器**中，右键单击项目，选择 "**添加" |新建文件夹**，并添加名为 "**中心**" 的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="250e6-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="250e6-139">右键单击 "**中心**" 文件夹，单击 "**添加" |类**，并创建名为C# **ChatHub.cs**的新类。</span><span class="sxs-lookup"><span data-stu-id="250e6-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="250e6-140">你将使用此类作为将消息发送到所有客户端的 SignalR 服务器集线器。</span><span class="sxs-lookup"><span data-stu-id="250e6-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="250e6-141">如果你使用 Visual Studio 2012 并安装了[ASP.NET 和 Web 工具2012.2 更新](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)，则可以使用 new SignalR 项模板来创建集线器类。</span><span class="sxs-lookup"><span data-stu-id="250e6-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="250e6-142">为此，请右键单击 "**中心**" 文件夹，单击 "**添加" |新建项**"，选择" **SignalR Hub 类（v1）** "，并将类命名为**ChatHub.cs**。</span><span class="sxs-lookup"><span data-stu-id="250e6-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="250e6-143">将**ChatHub**类中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="250e6-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="250e6-144">为项目打开**global.asax**文件，并添加对方法的调用，`RouteTable.Routes.MapHubs();` 作为 `Application_Start` 方法中的第一行代码。</span><span class="sxs-lookup"><span data-stu-id="250e6-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="250e6-145">此代码将注册 SignalR 中心的默认路由，并且必须在注册任何其他路由之前调用此代码。</span><span class="sxs-lookup"><span data-stu-id="250e6-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="250e6-146">已完成的 `Application_Start` 方法类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="250e6-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="250e6-147">编辑 controller **/HomeController**中找到的 `HomeController` 类，将以下方法添加到类。</span><span class="sxs-lookup"><span data-stu-id="250e6-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="250e6-148">此方法返回将在后面的步骤中创建的**聊天**视图。</span><span class="sxs-lookup"><span data-stu-id="250e6-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="250e6-149">在刚刚创建的 `Chat` 方法中右键单击，然后单击 "**添加视图**" 以创建新的视图文件。</span><span class="sxs-lookup"><span data-stu-id="250e6-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="250e6-150">在 "**添加视图**" 对话框中，确保选中复选框以**使用布局或母版页**（清除其他复选框），然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="250e6-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![添加视图](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="250e6-152">编辑名为 " **Chat**" 的新视图文件。</span><span class="sxs-lookup"><span data-stu-id="250e6-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="250e6-153">&lt;h2&gt; 标记后，粘贴以下 &lt;div&gt; 部分，并将代码块 `@section scripts` 到页面中。</span><span class="sxs-lookup"><span data-stu-id="250e6-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="250e6-154">此脚本使页面可以发送聊天消息和显示来自服务器的消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="250e6-155">下面的代码块中显示了聊天视图的完整代码。</span><span class="sxs-lookup"><span data-stu-id="250e6-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="250e6-156">将 SignalR 和其他脚本库添加到 Visual Studio 项目时，包管理器可能会安装比本主题中所示版本更新的脚本版本。</span><span class="sxs-lookup"><span data-stu-id="250e6-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="250e6-157">请确保代码中的脚本引用与你的项目中安装的脚本库的版本相匹配。</span><span class="sxs-lookup"><span data-stu-id="250e6-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="250e6-158">**全部保存**项目。</span><span class="sxs-lookup"><span data-stu-id="250e6-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="250e6-159">运行示例</span><span class="sxs-lookup"><span data-stu-id="250e6-159">Run the Sample</span></span>

1. <span data-ttu-id="250e6-160">按 F5 在调试模式下运行项目。</span><span class="sxs-lookup"><span data-stu-id="250e6-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="250e6-161">在浏览器地址行中，将 **/home/chat**追加到项目默认页的 URL。</span><span class="sxs-lookup"><span data-stu-id="250e6-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="250e6-162">聊天页面加载到浏览器实例中，并提示输入用户名。</span><span class="sxs-lookup"><span data-stu-id="250e6-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="250e6-164">输入用户名。</span><span class="sxs-lookup"><span data-stu-id="250e6-164">Enter a user name.</span></span>
4. <span data-ttu-id="250e6-165">复制浏览器地址行中的 URL，并使用它打开另外两个浏览器实例。</span><span class="sxs-lookup"><span data-stu-id="250e6-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="250e6-166">在每个浏览器实例中，输入唯一的用户名。</span><span class="sxs-lookup"><span data-stu-id="250e6-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="250e6-167">在每个浏览器实例中，添加注释并单击 "**发送**"。</span><span class="sxs-lookup"><span data-stu-id="250e6-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="250e6-168">注释应显示在所有浏览器实例中。</span><span class="sxs-lookup"><span data-stu-id="250e6-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="250e6-169">这个简单的聊天应用程序不会在服务器上维护讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="250e6-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="250e6-170">中心将注释广播给所有当前用户。</span><span class="sxs-lookup"><span data-stu-id="250e6-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="250e6-171">稍后加入聊天的用户将看到从他们加入的时间添加的消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="250e6-172">以下屏幕截图显示了在浏览器中运行的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![聊天浏览器](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="250e6-174">在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。</span><span class="sxs-lookup"><span data-stu-id="250e6-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="250e6-175">如果使用 Internet Explorer 作为浏览器，则此节点在调试模式中可见。</span><span class="sxs-lookup"><span data-stu-id="250e6-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="250e6-176">有一个名为 "**中心**" 的脚本文件，SignalR 库会在运行时动态生成该文件。</span><span class="sxs-lookup"><span data-stu-id="250e6-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="250e6-177">此文件管理 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="250e6-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="250e6-178">如果使用 Internet Explorer 之外的浏览器，还可以通过直接浏览到动态**中心**文件，例如 http://mywebsite/signalr/hubs。</span><span class="sxs-lookup"><span data-stu-id="250e6-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![生成的中心脚本](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="250e6-180">检查代码</span><span class="sxs-lookup"><span data-stu-id="250e6-180">Examine the Code</span></span>

<span data-ttu-id="250e6-181">SignalR chat 应用程序演示了两个基本的 SignalR 开发任务：将集线器创建为服务器上的主协调对象，并使用 SignalR jQuery library 发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="250e6-182">SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="250e6-182">SignalR Hubs</span></span>

<span data-ttu-id="250e6-183">在代码示例中， **ChatHub**类派生自**SignalR**类。</span><span class="sxs-lookup"><span data-stu-id="250e6-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="250e6-184">从**Hub**类派生是构建 SignalR 应用程序的一种有用方法。</span><span class="sxs-lookup"><span data-stu-id="250e6-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="250e6-185">可以在中心类上创建公共方法，并通过在网页中从 jQuery 脚本调用这些方法来访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="250e6-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="250e6-186">在聊天代码中，客户端调用**ChatHub**方法来发送新消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="250e6-187">然后，集线器会通过调用**addNewMessageToPage**将消息发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="250e6-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="250e6-188">**Send**方法演示了几个中心概念：</span><span class="sxs-lookup"><span data-stu-id="250e6-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="250e6-189">在中心声明公共方法，使客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="250e6-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="250e6-190">使用**SignalR**属性访问连接到此中心的所有客户端。</span><span class="sxs-lookup"><span data-stu-id="250e6-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="250e6-191">在客户端上调用 jQuery 函数（如 `addNewMessageToPage` 函数）以更新客户端。</span><span class="sxs-lookup"><span data-stu-id="250e6-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="250e6-192">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="250e6-192">SignalR and jQuery</span></span>

<span data-ttu-id="250e6-193">代码示例中的**Chat** view 文件演示了如何使用 SignalR jQuery 库与 SignalR 中心通信。</span><span class="sxs-lookup"><span data-stu-id="250e6-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="250e6-194">代码中的基本任务是为中心创建自动生成的代理的引用，并声明一个函数，服务器可以调用该函数将内容推送到客户端，并启动连接以向中心发送消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="250e6-195">下面的代码声明一个集线器的代理。</span><span class="sxs-lookup"><span data-stu-id="250e6-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="250e6-196">在 jQuery 中，对服务器类及其成员的引用采用 camel 大小写格式。</span><span class="sxs-lookup"><span data-stu-id="250e6-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="250e6-197">此代码示例将 jQuery C#中的**ChatHub**类引用为**ChatHub**。</span><span class="sxs-lookup"><span data-stu-id="250e6-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="250e6-198">如果要在C#jQuery 中引用 `ChatHub` 类和传统的 Pascal 大小写，请编辑 ChatHub.cs 类文件。</span><span class="sxs-lookup"><span data-stu-id="250e6-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="250e6-199">添加 `using` 语句以引用 `Microsoft.AspNet.SignalR.Hubs` 命名空间。</span><span class="sxs-lookup"><span data-stu-id="250e6-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="250e6-200">然后，将 `HubName` 特性添加到 `ChatHub` 类，例如 `[HubName("ChatHub")]`。</span><span class="sxs-lookup"><span data-stu-id="250e6-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="250e6-201">最后，将 jQuery 引用更新到 `ChatHub` 类。</span><span class="sxs-lookup"><span data-stu-id="250e6-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="250e6-202">下面的代码演示如何在脚本中创建回调函数。</span><span class="sxs-lookup"><span data-stu-id="250e6-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="250e6-203">服务器上的 hub 类调用此函数将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="250e6-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="250e6-204">对 `htmlEncode` 函数的可选调用显示了一种在页中显示消息内容之前对其进行编码的方法，作为一种防止脚本注入的方式。</span><span class="sxs-lookup"><span data-stu-id="250e6-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="250e6-205">下面的代码演示如何打开与中心的连接。</span><span class="sxs-lookup"><span data-stu-id="250e6-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="250e6-206">该代码启动连接，然后将其传递到 "聊天" 页的 "**发送**" 按钮上的 click 事件。</span><span class="sxs-lookup"><span data-stu-id="250e6-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="250e6-207">此方法确保在事件处理程序执行之前建立连接。</span><span class="sxs-lookup"><span data-stu-id="250e6-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="250e6-208">后续步骤</span><span class="sxs-lookup"><span data-stu-id="250e6-208">Next Steps</span></span>

<span data-ttu-id="250e6-209">您已经了解到，SignalR 是一个框架，用于构建实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="250e6-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="250e6-210">还了解了几个 SignalR 开发任务：如何将 SignalR 添加到 ASP.NET 应用程序、如何创建集线器类，以及如何从集线器发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="250e6-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="250e6-211">若要了解更高级的 SignalR 开发概念，请访问以下站点以获取 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="250e6-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="250e6-212">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="250e6-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="250e6-213">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="250e6-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="250e6-214">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="250e6-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
