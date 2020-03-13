---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 教程：与 SignalR 2 和 MVC 5 实时聊天 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何使用 ASP.NET SignalR 2 创建实时聊天应用程序。 将 SignalR 添加到 MVC 5 应用程序。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431618"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="7a4b8-104">教程：通过 SignalR 2 和 MVC 5 进行实时聊天</span><span class="sxs-lookup"><span data-stu-id="7a4b8-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="7a4b8-105">本教程介绍如何使用 ASP.NET SignalR 2 创建实时聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="7a4b8-106">将 SignalR 添加到 MVC 5 应用程序，并创建聊天视图来发送和显示消息。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="7a4b8-107">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a4b8-108">设置项目</span><span class="sxs-lookup"><span data-stu-id="7a4b8-108">Set up the project</span></span>
> * <span data-ttu-id="7a4b8-109">运行示例</span><span class="sxs-lookup"><span data-stu-id="7a4b8-109">Run the sample</span></span>
> * <span data-ttu-id="7a4b8-110">检查代码</span><span class="sxs-lookup"><span data-stu-id="7a4b8-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="7a4b8-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="7a4b8-111">Prerequisites</span></span>

* <span data-ttu-id="7a4b8-112">带有 ASP.NET 和 Web 开发工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="7a4b8-113">设置项目</span><span class="sxs-lookup"><span data-stu-id="7a4b8-113">Set up the Project</span></span>

<span data-ttu-id="7a4b8-114">本部分演示如何使用 Visual Studio 2017 和 SignalR 2 创建一个空的 ASP.NET MVC 5 应用程序，添加 SignalR 库，并创建聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="7a4b8-115">在 Visual Studio 中，创建C#一个面向 .NET Framework 4.5 的 ASP.NET 应用程序，将其命名为 SignalRChat，然后单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="7a4b8-117">在**New ASP.NET Web 应用程序-SignalRMvcChat**中，选择 " **MVC** "，然后选择 "**更改身份验证**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="7a4b8-118">在 "**更改身份验证**" 中，选择 "**无身份验证**" 并单击 **"确定"**</span><span class="sxs-lookup"><span data-stu-id="7a4b8-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![选择无身份验证](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="7a4b8-120">在**New ASP.NET Web 应用程序-SignalRMvcChat**中，选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="7a4b8-121">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="7a4b8-122">在 **"添加新项-SignalRChat**" 中，选择 "**安装** > **Visual C#**  > **Web** > " **SignalR** ，然后选择 " **SignalR Hub 类（v2）** "。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="7a4b8-123">将类命名为*ChatHub* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="7a4b8-124">此步骤将创建*ChatHub.cs*类文件，并向项目中添加一组支持 SignalR 的脚本文件和程序集引用。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="7a4b8-125">将新的*ChatHub.cs*类文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="7a4b8-126">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **类**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="7a4b8-127">将新类命名为*Startup* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="7a4b8-128">将*Startup.cs*类文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="7a4b8-129">在**解决方案资源管理器**中，选择 "**控制器**" > **HomeController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="7a4b8-130">将此方法添加到*HomeController.cs*。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="7a4b8-131">此方法返回在稍后的步骤中创建的**聊天**视图。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="7a4b8-132">在**解决方案资源管理器**中，右键单击 > **Home**"的"**视图**"，然后选择"**添加** >  **视图**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="7a4b8-133">在 "**添加视图**" 中，将新视图命名为 "**聊天**" 并选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="7a4b8-134">将**Chat**的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="7a4b8-135">在**解决方案资源管理器**中，展开 "**脚本**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="7a4b8-136">JQuery 和 SignalR 的脚本库在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7a4b8-137">程序包管理器可能已安装了更高版本的 SignalR 脚本。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="7a4b8-138">检查代码块中的脚本引用是否对应于项目中的脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="7a4b8-139">从原始代码块编写引用脚本：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="7a4b8-140">如果二者不匹配，则更新该*cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="7a4b8-141">从菜单栏中选择 "**文件**" > "**全部保存**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="7a4b8-142">运行示例</span><span class="sxs-lookup"><span data-stu-id="7a4b8-142">Run the Sample</span></span>

1. <span data-ttu-id="7a4b8-143">在工具栏中，启用 "**脚本调试**"，然后选择 "播放" 按钮以调试模式运行该示例。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="7a4b8-145">当浏览器打开时，为聊天标识输入名称。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="7a4b8-146">从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="7a4b8-147">在每个浏览器中，输入唯一名称。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="7a4b8-148">现在，请添加注释，然后选择 "**发送**"。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="7a4b8-149">在其他浏览器中重复此操作。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="7a4b8-150">注释会实时显示。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7a4b8-151">这个简单的聊天应用程序不会在服务器上维护讨论上下文。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="7a4b8-152">中心将注释广播给所有当前用户。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="7a4b8-153">稍后加入聊天的用户将看到从他们加入的时间添加的消息。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="7a4b8-154">了解如何在三种不同的浏览器中运行聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="7a4b8-155">当 Tom、Anand 和 Susan 发送消息时，所有浏览器都将实时更新：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![所有三个浏览器都显示相同的聊天历史记录](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="7a4b8-157">在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="7a4b8-158">有一个名为*hub*的脚本文件，SignalR 库会在运行时生成。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="7a4b8-159">此文件管理 jQuery 脚本和服务器端代码之间的通信。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![脚本文档节点中自动生成的中心脚本](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="7a4b8-161">检查代码</span><span class="sxs-lookup"><span data-stu-id="7a4b8-161">Examine the Code</span></span>

<span data-ttu-id="7a4b8-162">SignalR chat 应用程序演示了两个基本 SignalR 开发任务。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="7a4b8-163">其中介绍了如何创建中心。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-163">It shows you how to create a hub.</span></span> <span data-ttu-id="7a4b8-164">服务器使用该集线器作为主协调对象。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="7a4b8-165">中心使用 SignalR jQuery library 来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="7a4b8-166">ChatHub.cs 中的 SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="7a4b8-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="7a4b8-167">在代码示例中，`ChatHub` 类派生自 `Microsoft.AspNet.SignalR.Hub` 类。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="7a4b8-168">从 `Hub` 类派生是构建 SignalR 应用程序的一种有用方法。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="7a4b8-169">可以在中心类上创建公共方法，并通过在网页中的脚本中调用这些方法来访问这些方法。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="7a4b8-170">在聊天代码中，客户端调用 `ChatHub.Send` 方法来发送新消息。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="7a4b8-171">集线器会通过调用 `Clients.All.addNewMessageToPage`将消息发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="7a4b8-172">`Send` 方法演示了几个中心概念：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="7a4b8-173">在中心声明公共方法，使客户端可以调用它们。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="7a4b8-174">使用 `Microsoft.AspNet.SignalR.Hub.Clients` 动态属性与连接到此集线器的所有客户端通信。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="7a4b8-175">在客户端上调用一个函数（如 `addNewMessageToPage` 函数）以更新客户端。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="7a4b8-176">SignalR 和 jQuery Chat</span><span class="sxs-lookup"><span data-stu-id="7a4b8-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="7a4b8-177">代码示例中的*Chat* view 文件演示了如何使用 SignalR jQuery 库与 SignalR 中心通信。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="7a4b8-178">此代码将执行许多重要的任务。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-178">The code carries out many important tasks.</span></span> <span data-ttu-id="7a4b8-179">它将创建对中心自动生成的代理的引用，并声明一个函数，服务器可以调用该函数将内容推送到客户端，并且启动连接以向中心发送消息。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="7a4b8-180">在 JavaScript 中，对服务器类及其成员的引用位于 camelCase 中。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="7a4b8-181">此代码示例将 JavaScript C#中的 `ChatHub` 类引用为 `chatHub`。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="7a4b8-182">在此代码块中，你将在脚本中创建一个回调函数。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="7a4b8-183">服务器上的 hub 类调用此函数将内容更新推送到每个客户端。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="7a4b8-184">对 `htmlEncode` 函数的可选调用显示了一种在页中显示消息内容之前对消息内容进行 HTML 编码的方法。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="7a4b8-185">这是一种防止脚本注入的方式。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="7a4b8-186">此代码将打开与中心的连接。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="7a4b8-187">此方法确保在事件处理程序执行之前建立连接。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="7a4b8-188">该代码启动连接，然后将其传递到 "聊天" 页的 "**发送**" 按钮上的 click 事件。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="7a4b8-189">获取代码</span><span class="sxs-lookup"><span data-stu-id="7a4b8-189">Get the code</span></span>

[<span data-ttu-id="7a4b8-190">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="7a4b8-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="7a4b8-191">其他资源</span><span class="sxs-lookup"><span data-stu-id="7a4b8-191">Additional resources</span></span>

<span data-ttu-id="7a4b8-192">有关 SignalR 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="7a4b8-193">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="7a4b8-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="7a4b8-194">SignalR GitHub 和示例</span><span class="sxs-lookup"><span data-stu-id="7a4b8-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="7a4b8-195">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="7a4b8-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="7a4b8-196">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7a4b8-196">Next steps</span></span>

<span data-ttu-id="7a4b8-197">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="7a4b8-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a4b8-198">设置项目</span><span class="sxs-lookup"><span data-stu-id="7a4b8-198">Set up the project</span></span>
> * <span data-ttu-id="7a4b8-199">运行示例</span><span class="sxs-lookup"><span data-stu-id="7a4b8-199">Ran the sample</span></span>
> * <span data-ttu-id="7a4b8-200">检查代码</span><span class="sxs-lookup"><span data-stu-id="7a4b8-200">Examined the code</span></span>

<span data-ttu-id="7a4b8-201">转到下一篇文章，了解如何创建使用 ASP.NET SignalR 2 的 web 应用程序，以提供高频率消息传递功能。</span><span class="sxs-lookup"><span data-stu-id="7a4b8-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7a4b8-202">具有高频率消息传送的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="7a4b8-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)