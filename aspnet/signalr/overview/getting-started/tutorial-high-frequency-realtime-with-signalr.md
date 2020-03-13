---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 教程：通过 SignalR 2 创建高频实时应用 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何创建使用 ASP.NET SignalR 的 web 应用程序，以提供高频率消息传递功能。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450116"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="bd18c-103">教程：通过 SignalR 2 创建高频实时应用</span><span class="sxs-lookup"><span data-stu-id="bd18c-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="bd18c-104">本教程介绍如何创建使用 ASP.NET SignalR 2 的 web 应用程序，以提供高频率消息传递功能。</span><span class="sxs-lookup"><span data-stu-id="bd18c-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="bd18c-105">在这种情况下，"高频率消息传递" 意味着服务器按固定费率发送更新。</span><span class="sxs-lookup"><span data-stu-id="bd18c-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="bd18c-106">每秒最多发送10条消息。</span><span class="sxs-lookup"><span data-stu-id="bd18c-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="bd18c-107">你创建的应用程序将显示一个用户可拖动的形状。</span><span class="sxs-lookup"><span data-stu-id="bd18c-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="bd18c-108">服务器会更新所有连接的浏览器中形状的位置，以匹配所拖动形状的位置。</span><span class="sxs-lookup"><span data-stu-id="bd18c-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="bd18c-109">本教程中介绍的概念具有实时游戏和其他模拟应用程序的应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="bd18c-110">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="bd18c-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd18c-111">设置项目</span><span class="sxs-lookup"><span data-stu-id="bd18c-111">Set up the project</span></span>
> * <span data-ttu-id="bd18c-112">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="bd18c-112">Create the base application</span></span>
> * <span data-ttu-id="bd18c-113">在应用程序启动时映射到中心</span><span class="sxs-lookup"><span data-stu-id="bd18c-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="bd18c-114">添加客户端</span><span class="sxs-lookup"><span data-stu-id="bd18c-114">Add the client</span></span>
> * <span data-ttu-id="bd18c-115">运行应用</span><span class="sxs-lookup"><span data-stu-id="bd18c-115">Run the app</span></span>
> * <span data-ttu-id="bd18c-116">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="bd18c-116">Add the client loop</span></span>
> * <span data-ttu-id="bd18c-117">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="bd18c-117">Add the server loop</span></span>
> * <span data-ttu-id="bd18c-118">添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="bd18c-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="bd18c-119">系统必备</span><span class="sxs-lookup"><span data-stu-id="bd18c-119">Prerequisites</span></span>

* <span data-ttu-id="bd18c-120">带有 ASP.NET 和 Web 开发工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="bd18c-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="bd18c-121">设置项目</span><span class="sxs-lookup"><span data-stu-id="bd18c-121">Set up the project</span></span>

<span data-ttu-id="bd18c-122">在本部分中，将在 Visual Studio 2017 中创建项目。</span><span class="sxs-lookup"><span data-stu-id="bd18c-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="bd18c-123">本部分演示如何使用 Visual Studio 2017 创建空的 ASP.NET Web 应用程序并添加 SignalR 和 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="bd18c-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="bd18c-124">在 Visual Studio 中，创建一个 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![创建 web](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="bd18c-126">在**新的 ASP.NET Web 应用程序-MoveShapeDemo**窗口中，保留**空**的选中状态，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="bd18c-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="bd18c-127">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。</span><span class="sxs-lookup"><span data-stu-id="bd18c-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="bd18c-128">在 **"添加新项-MoveShapeDemo**" 中，选择 "**安装** > **Visual C#**  > **Web** > " **SignalR** ，然后选择 " **SignalR Hub 类（v2）** "。</span><span class="sxs-lookup"><span data-stu-id="bd18c-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="bd18c-129">将类命名为*MoveShapeHub* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="bd18c-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="bd18c-130">此步骤将创建*MoveShapeHub.cs*类文件。</span><span class="sxs-lookup"><span data-stu-id="bd18c-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="bd18c-131">同时，它将一组支持 SignalR 的脚本文件和程序集引用添加到该项目中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="bd18c-132">选择“工具” > “NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="bd18c-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="bd18c-133">在 "**程序包管理器控制台**" 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="bd18c-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="bd18c-134">命令安装 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="bd18c-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="bd18c-135">用于对形状进行动画处理。</span><span class="sxs-lookup"><span data-stu-id="bd18c-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="bd18c-136">在**解决方案资源管理器**中，展开 "脚本" 节点。</span><span class="sxs-lookup"><span data-stu-id="bd18c-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![脚本库引用](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="bd18c-138">JQuery、jQueryUI 和 SignalR 的脚本库在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="bd18c-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="bd18c-139">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="bd18c-139">Create the base application</span></span>

<span data-ttu-id="bd18c-140">在本部分中，将创建一个浏览器应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-140">In this section, you create a browser application.</span></span> <span data-ttu-id="bd18c-141">在每次鼠标移动事件期间，应用程序将形状的位置发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="bd18c-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="bd18c-142">服务器会将此信息实时广播给其他所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="bd18c-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="bd18c-143">稍后将详细介绍此应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="bd18c-144">打开*MoveShapeHub.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="bd18c-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="bd18c-145">将*MoveShapeHub.cs*文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bd18c-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="bd18c-146">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="bd18c-146">Save the file.</span></span>

<span data-ttu-id="bd18c-147">`MoveShapeHub` 类是 SignalR 中心的实现。</span><span class="sxs-lookup"><span data-stu-id="bd18c-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="bd18c-148">与[使用 SignalR 的入门](tutorial-getting-started-with-signalr.md)教程一样，该中心还提供了一个客户端直接调用的方法。</span><span class="sxs-lookup"><span data-stu-id="bd18c-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="bd18c-149">在这种情况下，客户端将具有形状的新 X 和 Y 坐标的对象发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="bd18c-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="bd18c-150">这些坐标将广播到所有其他已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="bd18c-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="bd18c-151">SignalR 使用 JSON 自动序列化此对象。</span><span class="sxs-lookup"><span data-stu-id="bd18c-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="bd18c-152">应用程序将 `ShapeModel` 对象发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="bd18c-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="bd18c-153">它包含成员，用于存储形状的位置。</span><span class="sxs-lookup"><span data-stu-id="bd18c-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="bd18c-154">服务器上的对象的版本还具有跟踪正在存储的客户端数据的成员。</span><span class="sxs-lookup"><span data-stu-id="bd18c-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="bd18c-155">此对象可防止服务器将客户端的数据发回自身。</span><span class="sxs-lookup"><span data-stu-id="bd18c-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="bd18c-156">此成员使用 `JsonIgnore` 特性来阻止应用程序对数据进行序列化并将其发送回客户端。</span><span class="sxs-lookup"><span data-stu-id="bd18c-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="bd18c-157">在应用程序启动时映射到中心</span><span class="sxs-lookup"><span data-stu-id="bd18c-157">Map to the hub when app starts</span></span>

<span data-ttu-id="bd18c-158">接下来，在应用程序启动时设置到中心的映射。</span><span class="sxs-lookup"><span data-stu-id="bd18c-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="bd18c-159">在 SignalR 2 中，添加 OWIN startup 类将创建映射。</span><span class="sxs-lookup"><span data-stu-id="bd18c-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="bd18c-160">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。</span><span class="sxs-lookup"><span data-stu-id="bd18c-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="bd18c-161">在 "**添加新项"-MoveShapeDemo**选择 "**安装** > **Visual C#**  > **Web** "，然后选择 " **OWIN Startup 类**"。</span><span class="sxs-lookup"><span data-stu-id="bd18c-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="bd18c-162">将类命名为 "*启动*"，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="bd18c-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="bd18c-163">将*Startup.cs*文件中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bd18c-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="bd18c-164">当应用执行 `Configuration` 方法时，OWIN startup 类将调用 `MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="bd18c-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="bd18c-165">应用使用 `OwinStartup` 程序集特性将类添加到 OWIN 的启动进程。</span><span class="sxs-lookup"><span data-stu-id="bd18c-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="bd18c-166">添加客户端</span><span class="sxs-lookup"><span data-stu-id="bd18c-166">Add the client</span></span>

<span data-ttu-id="bd18c-167">为客户端添加 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="bd18c-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="bd18c-168">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > " **HTML 页**"。</span><span class="sxs-lookup"><span data-stu-id="bd18c-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="bd18c-169">将该页命名为**默认值**，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="bd18c-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="bd18c-170">在**解决方案资源管理器**中，右键单击 " *Default .html* " 并选择 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="bd18c-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="bd18c-171">将*默认 .html*文件中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bd18c-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="bd18c-172">在**解决方案资源管理器**中，展开 "**脚本**"。</span><span class="sxs-lookup"><span data-stu-id="bd18c-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="bd18c-173">JQuery 和 SignalR 的脚本库在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="bd18c-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bd18c-174">包管理器安装 SignalR 脚本的更高版本。</span><span class="sxs-lookup"><span data-stu-id="bd18c-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="bd18c-175">更新代码块中的脚本引用，使其与项目中的脚本文件版本相对应。</span><span class="sxs-lookup"><span data-stu-id="bd18c-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="bd18c-176">此 HTML 和 JavaScript 代码会创建一个名为 `shape`的红色 `div`。</span><span class="sxs-lookup"><span data-stu-id="bd18c-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="bd18c-177">它使用 jQuery library 启用形状的拖动行为，并使用 `drag` 事件将形状的位置发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="bd18c-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="bd18c-178">运行应用</span><span class="sxs-lookup"><span data-stu-id="bd18c-178">Run the app</span></span>

<span data-ttu-id="bd18c-179">您可以运行应用程序，se'e 它工作。</span><span class="sxs-lookup"><span data-stu-id="bd18c-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="bd18c-180">当您在浏览器窗口周围拖动形状时，该形状也会移到其他浏览器中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="bd18c-181">在工具栏中，启用 "**脚本调试**"，然后选择 "播放" 按钮以调试模式运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![用户打开调试模式并选择 "播放" 的屏幕截图。](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="bd18c-183">此时会打开一个浏览器窗口，并在右上角带有红色形状。</span><span class="sxs-lookup"><span data-stu-id="bd18c-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="bd18c-184">复制页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="bd18c-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="bd18c-185">打开另一个浏览器，然后将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="bd18c-186">将该形状拖到一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="bd18c-187">其他浏览器窗口中的形状将如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd18c-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="bd18c-188">当应用程序使用此方法运行时，它不是一种建议的编程模型。</span><span class="sxs-lookup"><span data-stu-id="bd18c-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="bd18c-189">发送的邮件数没有上限。</span><span class="sxs-lookup"><span data-stu-id="bd18c-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="bd18c-190">因此，客户端和服务器会使消息和性能下降。</span><span class="sxs-lookup"><span data-stu-id="bd18c-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="bd18c-191">此外，该应用在客户端上显示不连贯的动画。</span><span class="sxs-lookup"><span data-stu-id="bd18c-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="bd18c-192">这种抖动动画发生的原因是，形状会按每个方法即时移动。</span><span class="sxs-lookup"><span data-stu-id="bd18c-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="bd18c-193">如果形状平稳地移动到每个新位置，则效果更佳。</span><span class="sxs-lookup"><span data-stu-id="bd18c-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="bd18c-194">接下来，了解如何解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="bd18c-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="bd18c-195">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="bd18c-195">Add the client loop</span></span>

<span data-ttu-id="bd18c-196">将形状的位置发送到每个鼠标移动事件会创建不必要数量的网络流量。</span><span class="sxs-lookup"><span data-stu-id="bd18c-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="bd18c-197">应用需要限制客户端发送的消息。</span><span class="sxs-lookup"><span data-stu-id="bd18c-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="bd18c-198">使用 javascript `setInterval` 函数设置一个循环，该循环将新位置信息按固定速率发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="bd18c-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="bd18c-199">此循环是 "游戏循环" 的基本表示形式。</span><span class="sxs-lookup"><span data-stu-id="bd18c-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="bd18c-200">这是一个重复调用的函数，用于驱动游戏的所有功能。</span><span class="sxs-lookup"><span data-stu-id="bd18c-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="bd18c-201">将*默认 .html*文件中的客户端代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bd18c-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="bd18c-202">必须再次替换脚本引用。</span><span class="sxs-lookup"><span data-stu-id="bd18c-202">You have to replace the script references again.</span></span> <span data-ttu-id="bd18c-203">它们必须与项目中脚本的版本相匹配。</span><span class="sxs-lookup"><span data-stu-id="bd18c-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="bd18c-204">此新代码将添加 `updateServerModel` 函数。</span><span class="sxs-lookup"><span data-stu-id="bd18c-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="bd18c-205">它按固定的频率调用。</span><span class="sxs-lookup"><span data-stu-id="bd18c-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="bd18c-206">只要 `moved` 标志指示存在要发送的新位置数据，函数就会将位置数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="bd18c-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="bd18c-207">选择 "播放" 按钮以启动应用程序</span><span class="sxs-lookup"><span data-stu-id="bd18c-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="bd18c-208">复制页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="bd18c-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="bd18c-209">打开另一个浏览器，然后将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="bd18c-210">将该形状拖到一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="bd18c-211">其他浏览器窗口中的形状将如下所示。</span><span class="sxs-lookup"><span data-stu-id="bd18c-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="bd18c-212">由于应用会限制发送到服务器的消息数，因此，在第一次播放动画时不会显示为平滑。</span><span class="sxs-lookup"><span data-stu-id="bd18c-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="bd18c-213">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="bd18c-213">Add the server loop</span></span>

<span data-ttu-id="bd18c-214">在当前的应用程序中，从服务器发送到客户端的消息将在收到消息时立即发送。</span><span class="sxs-lookup"><span data-stu-id="bd18c-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="bd18c-215">此网络流量显示了类似于客户端的问题。</span><span class="sxs-lookup"><span data-stu-id="bd18c-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="bd18c-216">应用程序的发送频率比需要的要多。</span><span class="sxs-lookup"><span data-stu-id="bd18c-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="bd18c-217">因此，连接可能会变得溢出。</span><span class="sxs-lookup"><span data-stu-id="bd18c-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="bd18c-218">本部分介绍如何更新服务器，以添加用于限制传出消息速率的计时器。</span><span class="sxs-lookup"><span data-stu-id="bd18c-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="bd18c-219">将 `MoveShapeHub.cs` 的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="bd18c-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="bd18c-220">选择 "播放" 按钮以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="bd18c-221">复制页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="bd18c-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="bd18c-222">打开另一个浏览器，然后将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="bd18c-223">将该形状拖到一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="bd18c-224">此代码扩展客户端以添加 `Broadcaster` 类。</span><span class="sxs-lookup"><span data-stu-id="bd18c-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="bd18c-225">新类使用 .NET framework 中的 `Timer` 类来限制传出消息。</span><span class="sxs-lookup"><span data-stu-id="bd18c-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="bd18c-226">了解中心本身是暂时性的。</span><span class="sxs-lookup"><span data-stu-id="bd18c-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="bd18c-227">它是每次需要时创建的。</span><span class="sxs-lookup"><span data-stu-id="bd18c-227">It's created every time it's needed.</span></span> <span data-ttu-id="bd18c-228">因此，应用程序会将 `Broadcaster` 创建为单一实例。</span><span class="sxs-lookup"><span data-stu-id="bd18c-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="bd18c-229">它使用延迟初始化来将 `Broadcaster`的创建延迟到需要的时间。</span><span class="sxs-lookup"><span data-stu-id="bd18c-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="bd18c-230">这可确保应用程序在启动计时器之前完全创建第一个中心实例。</span><span class="sxs-lookup"><span data-stu-id="bd18c-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="bd18c-231">然后，调用客户端的 `UpdateShape` 函数，然后将其移出集线器的 `UpdateModel` 方法。</span><span class="sxs-lookup"><span data-stu-id="bd18c-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="bd18c-232">应用收到传入消息时，不再会立即调用此方法。</span><span class="sxs-lookup"><span data-stu-id="bd18c-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="bd18c-233">相反，应用以每秒25次调用的速率将消息发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="bd18c-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="bd18c-234">此过程由 `Broadcaster` 类中的 `_broadcastLoop` 计时器进行管理。</span><span class="sxs-lookup"><span data-stu-id="bd18c-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="bd18c-235">最后，`Broadcaster` 类需要获取对当前操作的 `_hubContext` 中心的引用，而不是直接从中心调用客户端方法。</span><span class="sxs-lookup"><span data-stu-id="bd18c-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="bd18c-236">它获取具有 `GlobalHost`的引用。</span><span class="sxs-lookup"><span data-stu-id="bd18c-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="bd18c-237">添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="bd18c-237">Add smooth animation</span></span>

<span data-ttu-id="bd18c-238">应用程序已几乎完成，但我们可以提高一项改进。</span><span class="sxs-lookup"><span data-stu-id="bd18c-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="bd18c-239">应用程序会在客户端上移动该形状，以响应服务器消息。</span><span class="sxs-lookup"><span data-stu-id="bd18c-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="bd18c-240">使用 JQuery UI 库的 `animate` 函数，而不是将形状的位置设置为服务器给定的新位置。</span><span class="sxs-lookup"><span data-stu-id="bd18c-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="bd18c-241">它可以在其当前位置和新位置之间平稳移动形状。</span><span class="sxs-lookup"><span data-stu-id="bd18c-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="bd18c-242">更新*默认 .html*文件中客户端的 `updateShape` 方法，使其类似于突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="bd18c-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="bd18c-243">选择 "播放" 按钮以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="bd18c-244">复制页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="bd18c-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="bd18c-245">打开另一个浏览器，然后将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="bd18c-246">将该形状拖到一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="bd18c-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="bd18c-247">在另一个窗口中的形状移动显示的是较差的抖动。</span><span class="sxs-lookup"><span data-stu-id="bd18c-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="bd18c-248">应用程序将在一段时间内插值，而不是针对每个传入消息进行一次设置。</span><span class="sxs-lookup"><span data-stu-id="bd18c-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="bd18c-249">此代码将形状从旧位置移到新位置。</span><span class="sxs-lookup"><span data-stu-id="bd18c-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="bd18c-250">服务器在动画间隔过程中提供形状的位置。</span><span class="sxs-lookup"><span data-stu-id="bd18c-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="bd18c-251">在本例中为100毫秒。</span><span class="sxs-lookup"><span data-stu-id="bd18c-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="bd18c-252">应用会在新动画开始之前清除该形状上运行的任何以前的动画。</span><span class="sxs-lookup"><span data-stu-id="bd18c-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="bd18c-253">获取代码</span><span class="sxs-lookup"><span data-stu-id="bd18c-253">Get the code</span></span>

[<span data-ttu-id="bd18c-254">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="bd18c-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="bd18c-255">其他资源</span><span class="sxs-lookup"><span data-stu-id="bd18c-255">Additional resources</span></span>

<span data-ttu-id="bd18c-256">刚才了解到的通信模式对于开发联机游戏和其他模拟非常有用，例如，[通过 SignalR 创建的 ShootR 游戏](https://shootr.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="bd18c-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="bd18c-257">有关 SignalR 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="bd18c-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="bd18c-258">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="bd18c-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="bd18c-259">SignalR GitHub 和示例</span><span class="sxs-lookup"><span data-stu-id="bd18c-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="bd18c-260">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="bd18c-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="bd18c-261">后续步骤</span><span class="sxs-lookup"><span data-stu-id="bd18c-261">Next steps</span></span>

<span data-ttu-id="bd18c-262">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="bd18c-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd18c-263">设置项目</span><span class="sxs-lookup"><span data-stu-id="bd18c-263">Set up the project</span></span>
> * <span data-ttu-id="bd18c-264">已创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="bd18c-264">Created the base application</span></span>
> * <span data-ttu-id="bd18c-265">应用启动时映射到中心</span><span class="sxs-lookup"><span data-stu-id="bd18c-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="bd18c-266">添加了客户端</span><span class="sxs-lookup"><span data-stu-id="bd18c-266">Added the client</span></span>
> * <span data-ttu-id="bd18c-267">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bd18c-267">Ran the app</span></span>
> * <span data-ttu-id="bd18c-268">添加了客户端循环</span><span class="sxs-lookup"><span data-stu-id="bd18c-268">Added the client loop</span></span>
> * <span data-ttu-id="bd18c-269">添加了服务器循环</span><span class="sxs-lookup"><span data-stu-id="bd18c-269">Added the server loop</span></span>
> * <span data-ttu-id="bd18c-270">添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="bd18c-270">Added smooth animation</span></span>

<span data-ttu-id="bd18c-271">转到下一篇文章，了解如何创建使用 ASP.NET SignalR 2 提供服务器广播功能的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bd18c-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bd18c-272">SignalR 2 和服务器广播</span><span class="sxs-lookup"><span data-stu-id="bd18c-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)