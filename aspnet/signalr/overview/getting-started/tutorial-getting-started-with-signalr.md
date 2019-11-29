---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 教程： SignalR 2 的实时聊天 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600473"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="638e3-104">教程： SignalR 2 的实时聊天</span><span class="sxs-lookup"><span data-stu-id="638e3-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="638e3-105">本教程介绍如何使用 SignalR 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="638e3-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="638e3-106">将 SignalR 添加到空的 ASP.NET web 应用程序，并创建用于发送和显示消息的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="638e3-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="638e3-107">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="638e3-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="638e3-108">设置项目</span><span class="sxs-lookup"><span data-stu-id="638e3-108">Set up the project</span></span>
> * <span data-ttu-id="638e3-109">运行示例</span><span class="sxs-lookup"><span data-stu-id="638e3-109">Run the sample</span></span>
> * <span data-ttu-id="638e3-110">检查代码</span><span class="sxs-lookup"><span data-stu-id="638e3-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="638e3-111">先决条件</span><span class="sxs-lookup"><span data-stu-id="638e3-111">Prerequisites</span></span>

* <span data-ttu-id="638e3-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) ，提供**ASP.NET 和 web 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="638e3-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="638e3-113">设置项目</span><span class="sxs-lookup"><span data-stu-id="638e3-113">Set up the Project</span></span>

<span data-ttu-id="638e3-114">本部分演示如何使用 Visual Studio 2017 和 SignalR 2 创建一个空的 ASP.NET web 应用程序，添加 SignalR，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="638e3-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="638e3-115">在 Visual Studio 中，创建一个 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="638e3-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="638e3-117">在**新的 ASP.NET 项目-SignalRChat**窗口中，保留**空**的选中状态，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="638e3-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="638e3-118">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="638e3-119">在 **"添加新项-SignalRChat**" 中，选择 "**安装** > **Visual C#**  > **Web** > " **SignalR** ，然后选择 " **SignalR Hub 类（v2）** "。</span><span class="sxs-lookup"><span data-stu-id="638e3-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="638e3-120">将类命名为*ChatHub* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="638e3-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="638e3-121">此步骤将创建*ChatHub.cs*类文件，并向项目中添加一组支持 SignalR 的脚本文件和程序集引用。</span><span class="sxs-lookup"><span data-stu-id="638e3-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="638e3-122">将新的*ChatHub.cs*类文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="638e3-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="638e3-123">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="638e3-124">在 "**添加新项"-SignalRChat**选择 "**安装** > **Visual C#**  > **Web** "，然后选择 " **OWIN Startup 类**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="638e3-125">将类命名为*Startup* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="638e3-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="638e3-126">将*Startup*类中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="638e3-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="638e3-127">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > " **HTML 页**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="638e3-128">为新页*索引*命名，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="638e3-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="638e3-129">在**解决方案资源管理器**中，右键单击创建的 HTML 页面，然后选择 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="638e3-130">将 HTML 页面中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="638e3-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="638e3-131">在**解决方案资源管理器**中，展开 "**脚本**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="638e3-132">JQuery 和 SignalR 的脚本库在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="638e3-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="638e3-133">程序包管理器可能已安装了更高版本的 SignalR 脚本。</span><span class="sxs-lookup"><span data-stu-id="638e3-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="638e3-134">检查代码块中的脚本引用是否对应于项目中的脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="638e3-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="638e3-135">从原始代码块编写引用脚本：</span><span class="sxs-lookup"><span data-stu-id="638e3-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="638e3-136">如果二者不匹配，则更新 *.html*文件。</span><span class="sxs-lookup"><span data-stu-id="638e3-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="638e3-137">从菜单栏中选择 "**文件**" > "**全部保存**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="638e3-138">运行示例</span><span class="sxs-lookup"><span data-stu-id="638e3-138">Run the Sample</span></span>

1. <span data-ttu-id="638e3-139">在工具栏中，启用 "**脚本调试**"，然后选择 "播放" 按钮以调试模式运行该示例。</span><span class="sxs-lookup"><span data-stu-id="638e3-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="638e3-141">当浏览器打开时，为聊天标识输入名称。</span><span class="sxs-lookup"><span data-stu-id="638e3-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="638e3-142">从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="638e3-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="638e3-143">在每个浏览器中，输入唯一名称。</span><span class="sxs-lookup"><span data-stu-id="638e3-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="638e3-144">现在，请添加注释，然后选择 "**发送**"。</span><span class="sxs-lookup"><span data-stu-id="638e3-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="638e3-145">在其他浏览器中重复此操作。</span><span class="sxs-lookup"><span data-stu-id="638e3-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="638e3-146">注释会实时显示。</span><span class="sxs-lookup"><span data-stu-id="638e3-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="638e3-147">这个简单的聊天应用程序不会在服务器上维护讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="638e3-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="638e3-148">中心将注释广播给所有当前用户。</span><span class="sxs-lookup"><span data-stu-id="638e3-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="638e3-149">稍后加入聊天的用户将看到从他们加入的时间添加的消息。</span><span class="sxs-lookup"><span data-stu-id="638e3-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="638e3-150">了解如何在三种不同的浏览器中运行聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="638e3-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="638e3-151">当 Tom、Anand 和 Susan 发送消息时，所有浏览器都将实时更新：</span><span class="sxs-lookup"><span data-stu-id="638e3-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![所有三个浏览器都显示相同的聊天历史记录](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="638e3-153">在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。</span><span class="sxs-lookup"><span data-stu-id="638e3-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="638e3-154">有一个名为*hub*的脚本文件，SignalR 库会在运行时生成。</span><span class="sxs-lookup"><span data-stu-id="638e3-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="638e3-155">此文件管理 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="638e3-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![脚本文档节点中自动生成的中心脚本](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="638e3-157">检查代码</span><span class="sxs-lookup"><span data-stu-id="638e3-157">Examine the Code</span></span>

<span data-ttu-id="638e3-158">SignalRChat 应用程序演示了两个基本 SignalR 开发任务。</span><span class="sxs-lookup"><span data-stu-id="638e3-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="638e3-159">其中介绍了如何创建中心。</span><span class="sxs-lookup"><span data-stu-id="638e3-159">It shows you how to create a hub.</span></span> <span data-ttu-id="638e3-160">服务器使用该集线器作为主协调对象。</span><span class="sxs-lookup"><span data-stu-id="638e3-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="638e3-161">中心使用 SignalR jQuery library 来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="638e3-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="638e3-162">ChatHub.cs 中的 SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="638e3-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="638e3-163">在上面的代码示例中，`ChatHub` 类派生自 `Microsoft.AspNet.SignalR.Hub` 类。</span><span class="sxs-lookup"><span data-stu-id="638e3-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="638e3-164">从 `Hub` 类派生是构建 SignalR 应用程序的一种有用方法。</span><span class="sxs-lookup"><span data-stu-id="638e3-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="638e3-165">可以在中心类上创建公共方法，并通过在网页中的脚本中调用这些方法来使用这些方法。</span><span class="sxs-lookup"><span data-stu-id="638e3-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="638e3-166">在聊天代码中，客户端调用 `ChatHub.Send` 方法来发送新消息。</span><span class="sxs-lookup"><span data-stu-id="638e3-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="638e3-167">然后，集线器通过调用 `Clients.All.broadcastMessage`将消息发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="638e3-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="638e3-168">`Send` 方法演示了几个中心概念：</span><span class="sxs-lookup"><span data-stu-id="638e3-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="638e3-169">在中心声明公共方法，使客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="638e3-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="638e3-170">使用 `Microsoft.AspNet.SignalR.Hub.Clients` 动态属性与连接到此集线器的所有客户端通信。</span><span class="sxs-lookup"><span data-stu-id="638e3-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="638e3-171">在客户端上调用一个函数（如 `broadcastMessage` 函数）以更新客户端。</span><span class="sxs-lookup"><span data-stu-id="638e3-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="638e3-172">索引中的 SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="638e3-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="638e3-173">代码示例中的 "*索引*" 页显示了如何使用 SignalR jQuery 库与 SignalR 中心通信。</span><span class="sxs-lookup"><span data-stu-id="638e3-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="638e3-174">此代码将执行许多重要的任务。</span><span class="sxs-lookup"><span data-stu-id="638e3-174">The code carries out many important tasks.</span></span> <span data-ttu-id="638e3-175">它声明了一个代理来引用中心，并声明了一个函数，服务器可以调用该函数将内容推送到客户端，并启动一个连接将消息发送到中心。</span><span class="sxs-lookup"><span data-stu-id="638e3-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="638e3-176">在 JavaScript 中，对服务器类及其成员的引用必须是 camelCase。</span><span class="sxs-lookup"><span data-stu-id="638e3-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="638e3-177">此代码示例引用 JavaScript C#中的*ChatHub*类作为 `chatHub`。</span><span class="sxs-lookup"><span data-stu-id="638e3-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="638e3-178">在此代码块中，你将在脚本中创建一个回调函数。</span><span class="sxs-lookup"><span data-stu-id="638e3-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="638e3-179">服务器上的 hub 类调用此函数将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="638e3-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="638e3-180">在显示之前对内容进行 HTML 编码的两行是可选的，并显示一种防止脚本注入的好办法。</span><span class="sxs-lookup"><span data-stu-id="638e3-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="638e3-181">此代码将打开与中心的连接。</span><span class="sxs-lookup"><span data-stu-id="638e3-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="638e3-182">此方法可确保代码在事件处理程序执行之前建立连接。</span><span class="sxs-lookup"><span data-stu-id="638e3-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="638e3-183">该代码启动连接，然后将其传递给 HTML 页面的 "**发送**" 按钮上的 click 事件。</span><span class="sxs-lookup"><span data-stu-id="638e3-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="638e3-184">获取代码</span><span class="sxs-lookup"><span data-stu-id="638e3-184">Get the code</span></span>

[<span data-ttu-id="638e3-185">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="638e3-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="638e3-186">其他资源</span><span class="sxs-lookup"><span data-stu-id="638e3-186">Additional resources</span></span>

<span data-ttu-id="638e3-187">有关 SignalR 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="638e3-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="638e3-188">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="638e3-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="638e3-189">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="638e3-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="638e3-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="638e3-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="638e3-191">后续步骤</span><span class="sxs-lookup"><span data-stu-id="638e3-191">Next steps</span></span>

<span data-ttu-id="638e3-192">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="638e3-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="638e3-193">设置项目</span><span class="sxs-lookup"><span data-stu-id="638e3-193">Set up the project</span></span>
> * <span data-ttu-id="638e3-194">运行示例</span><span class="sxs-lookup"><span data-stu-id="638e3-194">Ran the sample</span></span>
> * <span data-ttu-id="638e3-195">检查代码</span><span class="sxs-lookup"><span data-stu-id="638e3-195">Examined the code</span></span>

<span data-ttu-id="638e3-196">转到下一篇文章，了解如何使用 SignalR 和 MVC 5。</span><span class="sxs-lookup"><span data-stu-id="638e3-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="638e3-197">SignalR 2 和 MVC 5</span><span class="sxs-lookup"><span data-stu-id="638e3-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)