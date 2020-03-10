---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: 通过 SignalR 1.x 实现高频实时 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何创建使用 ASP.NET SignalR 的 web 应用程序，以提供高频率消息传递功能。 高频率消息 。
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505712"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a><span data-ttu-id="4523d-104">使用 SignalR 1.x 实现高频率实时功能</span><span class="sxs-lookup"><span data-stu-id="4523d-104">High-Frequency Realtime with SignalR 1.x</span></span>

<span data-ttu-id="4523d-105">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="4523d-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4523d-106">本教程介绍如何创建使用 ASP.NET SignalR 的 web 应用程序，以提供高频率消息传递功能。</span><span class="sxs-lookup"><span data-stu-id="4523d-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="4523d-107">在这种情况下，高频率消息传送是指按固定费率发送的更新;对于此应用程序，每秒最多10条消息。</span><span class="sxs-lookup"><span data-stu-id="4523d-107">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="4523d-108">你将在本教程中创建的应用程序将显示一个用户可拖动的形状。</span><span class="sxs-lookup"><span data-stu-id="4523d-108">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="4523d-109">然后，将更新其他所有连接的浏览器中形状的位置，使其与所拖动的形状的位置相匹配。</span><span class="sxs-lookup"><span data-stu-id="4523d-109">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="4523d-110">本教程中介绍的概念具有实时游戏和其他模拟应用程序的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-110">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> <span data-ttu-id="4523d-111">欢迎使用教程中的注释。</span><span class="sxs-lookup"><span data-stu-id="4523d-111">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="4523d-112">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="4523d-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="4523d-113">概述</span><span class="sxs-lookup"><span data-stu-id="4523d-113">Overview</span></span>

<span data-ttu-id="4523d-114">本教程演示如何创建一个应用程序，用于实时与其他浏览器共享对象的状态。</span><span class="sxs-lookup"><span data-stu-id="4523d-114">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="4523d-115">我们要创建的应用程序称为 MoveShape。</span><span class="sxs-lookup"><span data-stu-id="4523d-115">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="4523d-116">"MoveShape" 页将显示用户可拖动的 HTML Div 元素;当用户拖动 Div 时，它的新位置将被发送到服务器，然后将通知所有其他连接的客户端更新形状的位置以使其匹配。</span><span class="sxs-lookup"><span data-stu-id="4523d-116">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="4523d-118">本教程中创建的应用程序基于 Damian Edwards 的演示。</span><span class="sxs-lookup"><span data-stu-id="4523d-118">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="4523d-119">[此处](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)显示了包含此演示的视频。</span><span class="sxs-lookup"><span data-stu-id="4523d-119">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="4523d-120">本教程将首先演示如何从每个在拖动形状时激发的事件发送 SignalR 消息。</span><span class="sxs-lookup"><span data-stu-id="4523d-120">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="4523d-121">每次收到消息时，每个连接的客户端都将更新形状的本地版本的位置。</span><span class="sxs-lookup"><span data-stu-id="4523d-121">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="4523d-122">当应用程序使用此方法运行时，这不是一种建议的编程模型，因为对发送的消息数没有上限，因此客户端和服务器可能会占用消息，而性能会下降.</span><span class="sxs-lookup"><span data-stu-id="4523d-122">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="4523d-123">客户端上显示的动画也会断开连接，因为每个方法会将形状立即移动，而不是顺利地移动到每个新位置。</span><span class="sxs-lookup"><span data-stu-id="4523d-123">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="4523d-124">本教程的后面部分将演示如何创建一个计时器函数，该函数可限制客户端或服务器发送消息的最大速率，以及如何在位置之间平稳移动形状。</span><span class="sxs-lookup"><span data-stu-id="4523d-124">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="4523d-125">可以从[代码库](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下载本教程中创建的应用程序的最终版本。</span><span class="sxs-lookup"><span data-stu-id="4523d-125">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="4523d-126">本教程包含以下部分：</span><span class="sxs-lookup"><span data-stu-id="4523d-126">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="4523d-127">先决条件</span><span class="sxs-lookup"><span data-stu-id="4523d-127">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="4523d-128">创建项目</span><span class="sxs-lookup"><span data-stu-id="4523d-128">Create the project</span></span>](#createtheproject)
- [<span data-ttu-id="4523d-129">添加 ASP.NET SignalR 和 JQuery. UI NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4523d-129">Add the ASP.NET SignalR and JQuery.UI NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="4523d-130">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="4523d-130">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="4523d-131">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="4523d-131">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="4523d-132">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="4523d-132">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="4523d-133">在客户端上添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="4523d-133">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="4523d-134">其他步骤</span><span class="sxs-lookup"><span data-stu-id="4523d-134">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="4523d-135">系统必备</span><span class="sxs-lookup"><span data-stu-id="4523d-135">Prerequisites</span></span>

<span data-ttu-id="4523d-136">本教程需要 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="4523d-136">This tutorial requires Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="4523d-137">如果使用的是 Visual Studio 2010，则项目将使用 .NET Framework 4，而不是 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="4523d-137">If Visual Studio 2010 is used, the project will use .NET Framework 4 rather than .NET Framework 4.5.</span></span>

<span data-ttu-id="4523d-138">如果使用的是 Visual Studio 2012，建议安装[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="4523d-138">If you are using Visual Studio 2012, it's recommended that you install the [ASP.NET and Web Tools 2012.2 update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="4523d-139">此更新包含新功能，如对发布、新功能和新模板的增强功能。</span><span class="sxs-lookup"><span data-stu-id="4523d-139">This update contains new features such as enhancements to publishing, new functionality, and new templates.</span></span>

<span data-ttu-id="4523d-140">如果安装了 Visual Studio 2010，请确保已安装[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。</span><span class="sxs-lookup"><span data-stu-id="4523d-140">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createtheproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="4523d-141">创建项目</span><span class="sxs-lookup"><span data-stu-id="4523d-141">Create the project</span></span>

<span data-ttu-id="4523d-142">在本部分中，我们将在 Visual Studio 中创建项目。</span><span class="sxs-lookup"><span data-stu-id="4523d-142">In this section, we'll create the project in Visual Studio.</span></span>

1. <span data-ttu-id="4523d-143">从“文件”菜单上，单击“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="4523d-143">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="4523d-144">在 "**新建项目**" 对话框中， **C#** 展开 "**模板**"，然后选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="4523d-144">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="4523d-145">选择**ASP.NET 空 Web 应用程序**模板，将项目命名为*MoveShapeDemo*，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="4523d-145">Select the **ASP.NET Empty Web Application** template, name the project *MoveShapeDemo*, and click **OK**.</span></span>

    ![创建新项目](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a><span data-ttu-id="4523d-147">添加 SignalR 和 JQuery. UI NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4523d-147">Add the SignalR and JQuery.UI NuGet Packages</span></span>

<span data-ttu-id="4523d-148">可以通过安装 NuGet 包将 SignalR 功能添加到项目。</span><span class="sxs-lookup"><span data-stu-id="4523d-148">You can add SignalR functionality to a project by installing a NuGet package.</span></span> <span data-ttu-id="4523d-149">本教程还将使用 JQuery. UI 包允许拖动和动画处理形状。</span><span class="sxs-lookup"><span data-stu-id="4523d-149">This tutorial will also use the JQuery.UI package for allowing the shape to be dragged and animated.</span></span>

1. <span data-ttu-id="4523d-150">单击 "**工具" |NuGet 包管理器 |程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="4523d-150">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="4523d-151">在 "包管理器" 中输入以下命令。</span><span class="sxs-lookup"><span data-stu-id="4523d-151">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="4523d-152">SignalR 包会安装多个其他 NuGet 包作为依赖项。</span><span class="sxs-lookup"><span data-stu-id="4523d-152">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="4523d-153">安装完成后，你将拥有在 ASP.NET 应用程序中使用 SignalR 所需的所有服务器和客户端组件。</span><span class="sxs-lookup"><span data-stu-id="4523d-153">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>
3. <span data-ttu-id="4523d-154">在包管理器控制台中输入以下命令以安装 JQuery 和 JQuery. UI 包。</span><span class="sxs-lookup"><span data-stu-id="4523d-154">Enter the following command into the package manager console to install the JQuery and JQuery.UI packages.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="4523d-155">创建基本应用程序</span><span class="sxs-lookup"><span data-stu-id="4523d-155">Create the base application</span></span>

<span data-ttu-id="4523d-156">在本部分中，我们将创建一个浏览器应用程序，用于在每次鼠标移动事件时将形状的位置发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="4523d-156">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="4523d-157">然后，服务器将此信息广播到所有其他已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="4523d-157">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="4523d-158">稍后我们将在此应用程序中展开此应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-158">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="4523d-159">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**"、"**类 ...** "。将类命名为**MoveShapeHub** ，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4523d-159">In **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="4523d-160">将新的**MoveShapeHub**类中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="4523d-160">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="4523d-161">上述 `MoveShapeHub` 类是 SignalR 中心的实现。</span><span class="sxs-lookup"><span data-stu-id="4523d-161">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="4523d-162">与[使用 SignalR 的入门](index.md)教程一样，此中心具有一个方法，客户端将直接调用该方法。</span><span class="sxs-lookup"><span data-stu-id="4523d-162">As in the [Getting Started with SignalR](index.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="4523d-163">在这种情况下，客户端将向服务器发送包含形状的新 X 和 Y 坐标的对象，然后将该对象广播给所有其他连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="4523d-163">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="4523d-164">SignalR 将使用 JSON 自动序列化此对象。</span><span class="sxs-lookup"><span data-stu-id="4523d-164">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="4523d-165">将发送到客户端（`ShapeModel`）的对象包含存储形状位置的成员。</span><span class="sxs-lookup"><span data-stu-id="4523d-165">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="4523d-166">服务器上的对象的版本还包含用于跟踪正在存储的客户端数据的成员，以便不会向给定客户端发送其自己的数据。</span><span class="sxs-lookup"><span data-stu-id="4523d-166">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="4523d-167">此成员使用 `JsonIgnore` 特性来防止将其序列化并发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="4523d-167">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>
3. <span data-ttu-id="4523d-168">接下来，我们将在应用程序启动时设置中心。</span><span class="sxs-lookup"><span data-stu-id="4523d-168">Next, we'll set up the hub when the application starts.</span></span> <span data-ttu-id="4523d-169">在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加" |全局应用程序类**。</span><span class="sxs-lookup"><span data-stu-id="4523d-169">In **Solution Explorer**, right-click the project, then click **Add | Global Application Class**.</span></span> <span data-ttu-id="4523d-170">接受 "*全局*" 的默认名称，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="4523d-170">Accept the default name of *Global* and click **OK**.</span></span>

    ![添加全局应用程序类](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. <span data-ttu-id="4523d-172">将以下 `using` 语句添加到 Global.asax.cs 类中提供的**using**语句后面。</span><span class="sxs-lookup"><span data-stu-id="4523d-172">Add the following `using` statement after the provided **using** statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. <span data-ttu-id="4523d-173">在全局类的 `Application_Start` 方法中添加以下代码行，以便为 SignalR 注册默认路由。</span><span class="sxs-lookup"><span data-stu-id="4523d-173">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="4523d-174">Global.asax 文件应如下所示：</span><span class="sxs-lookup"><span data-stu-id="4523d-174">Your global.asax file should look like the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. <span data-ttu-id="4523d-175">接下来，我们将添加客户端。</span><span class="sxs-lookup"><span data-stu-id="4523d-175">Next, we'll add the client.</span></span> <span data-ttu-id="4523d-176">在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加" |新建项**。</span><span class="sxs-lookup"><span data-stu-id="4523d-176">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="4523d-177">在 "**添加新项**" 对话框中，选择 " **Html 页**"。</span><span class="sxs-lookup"><span data-stu-id="4523d-177">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="4523d-178">为该页指定一个适当的名称（如**html**），然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4523d-178">Give the page an appropriate name (like **Default.html**) and click **Add**.</span></span>
7. <span data-ttu-id="4523d-179">在**解决方案资源管理器**中，右键单击刚创建的页面，然后单击 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="4523d-179">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
8. <span data-ttu-id="4523d-180">将 HTML 页面中的默认代码替换为以下代码片段。</span><span class="sxs-lookup"><span data-stu-id="4523d-180">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4523d-181">验证下面的脚本引用是否与 "脚本" 文件夹中添加到项目中的包匹配。</span><span class="sxs-lookup"><span data-stu-id="4523d-181">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span> <span data-ttu-id="4523d-182">在 Visual Studio 2010 中，添加到项目中的 JQuery 和 SignalR 的版本可能与以下版本号不匹配。</span><span class="sxs-lookup"><span data-stu-id="4523d-182">In Visual Studio 2010, the version of JQuery and SignalR added to the project may not match the version numbers below.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    <span data-ttu-id="4523d-183">上述 HTML 和 JavaScript 代码创建一个名为 Shape 的红色 Div，使用 jQuery library 启用形状的拖动行为，并使用形状的 `drag` 事件将该形状的位置发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="4523d-183">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
9. <span data-ttu-id="4523d-184">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-184">Start the application by pressing F5.</span></span> <span data-ttu-id="4523d-185">复制页面的 URL，并将其粘贴到另一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="4523d-185">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="4523d-186">在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="4523d-186">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="4523d-188">添加客户端循环</span><span class="sxs-lookup"><span data-stu-id="4523d-188">Add the client loop</span></span>

<span data-ttu-id="4523d-189">由于在每个鼠标移动事件上发送形状的位置都将产生不必要的网络流量，因此需要限制来自客户端的消息。</span><span class="sxs-lookup"><span data-stu-id="4523d-189">Since sending the location of the shape on every mouse move event will create an unnecessary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="4523d-190">我们将使用 javascript `setInterval` 函数设置一个循环，该循环将新位置信息按固定速率发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="4523d-190">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="4523d-191">此循环是 "游戏循环" 的一个非常基本的表示形式，它是一个重复调用的函数，用于驱动游戏或其他模拟的所有功能。</span><span class="sxs-lookup"><span data-stu-id="4523d-191">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="4523d-192">更新 HTML 页面中的客户端代码，以匹配以下代码片段。</span><span class="sxs-lookup"><span data-stu-id="4523d-192">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    <span data-ttu-id="4523d-193">以上更新添加了 `updateServerModel` 函数，该函数将按固定频率调用。</span><span class="sxs-lookup"><span data-stu-id="4523d-193">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="4523d-194">只要 `moved` 标志指示存在要发送的新位置数据，此函数就会将位置数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="4523d-194">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="4523d-195">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-195">Start the application by pressing F5.</span></span> <span data-ttu-id="4523d-196">复制页面的 URL，并将其粘贴到另一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="4523d-196">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="4523d-197">在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="4523d-197">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="4523d-198">由于发送到服务器的消息数将会受到限制，因此，在上一节中，动画将不会显示为平滑。</span><span class="sxs-lookup"><span data-stu-id="4523d-198">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="4523d-200">添加服务器循环</span><span class="sxs-lookup"><span data-stu-id="4523d-200">Add the server loop</span></span>

<span data-ttu-id="4523d-201">在当前应用程序中，从服务器发送到客户端的消息将在收到消息时接收。</span><span class="sxs-lookup"><span data-stu-id="4523d-201">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="4523d-202">这就是在客户端上出现的类似问题;消息的发送频率比需要的多，因此连接可能会变得溢出。</span><span class="sxs-lookup"><span data-stu-id="4523d-202">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="4523d-203">本部分介绍如何更新服务器以实现限制传出消息速率的计时器。</span><span class="sxs-lookup"><span data-stu-id="4523d-203">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="4523d-204">将 `MoveShapeHub.cs` 的内容替换为以下代码段。</span><span class="sxs-lookup"><span data-stu-id="4523d-204">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="4523d-205">上面的代码将扩展客户端以添加 `Broadcaster` 类，该类使用 .NET framework 中的 `Timer` 类来限制传出消息。</span><span class="sxs-lookup"><span data-stu-id="4523d-205">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="4523d-206">由于中心本身是暂时的（每次需要时都会创建），因此 `Broadcaster` 将创建为单一实例。</span><span class="sxs-lookup"><span data-stu-id="4523d-206">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="4523d-207">迟缓初始化（在 .NET 4 中引入）用于将其创建延迟到需要的时间，从而确保在启动计时器之前完全创建第一个中心实例。</span><span class="sxs-lookup"><span data-stu-id="4523d-207">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="4523d-208">然后，调用客户端的 `UpdateModel` 方法，以便在收到传入消息时，不会立即立即调用客户端的 `UpdateShape` 函数。</span><span class="sxs-lookup"><span data-stu-id="4523d-208">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="4523d-209">相反，发送到客户端的消息的速率为每秒25次调用，由 `_broadcastLoop` 计时器从 `Broadcaster` 类中管理。</span><span class="sxs-lookup"><span data-stu-id="4523d-209">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="4523d-210">最后，`Broadcaster` 类需要使用 `GlobalHost`获取对当前操作中心（`_hubContext`）的引用，而不是直接从中心调用客户端方法。</span><span class="sxs-lookup"><span data-stu-id="4523d-210">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="4523d-211">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-211">Start the application by pressing F5.</span></span> <span data-ttu-id="4523d-212">复制页面的 URL，并将其粘贴到另一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="4523d-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="4523d-213">在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="4523d-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="4523d-214">与上一节相比，浏览器中将不会有明显的区别，但会限制发送到客户端的消息数。</span><span class="sxs-lookup"><span data-stu-id="4523d-214">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="4523d-216">在客户端上添加平滑动画</span><span class="sxs-lookup"><span data-stu-id="4523d-216">Add smooth animation on the client</span></span>

<span data-ttu-id="4523d-217">应用程序已几乎完成，但在客户端上的形状运动中，它可以提高一项改进，因为它是在响应服务器消息时移动的。</span><span class="sxs-lookup"><span data-stu-id="4523d-217">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="4523d-218">我们将使用 JQuery UI 库的 `animate` 函数在其当前位置与新位置之间平稳移动，而不是将形状的位置设置为服务器给定的新位置。</span><span class="sxs-lookup"><span data-stu-id="4523d-218">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="4523d-219">将客户端的 `updateShape` 方法更新为类似于以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="4523d-219">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    <span data-ttu-id="4523d-220">上面的代码将形状从旧位置移动到由服务器在动画时间间隔（在本例中为100毫秒）的过程中指定的新位置。</span><span class="sxs-lookup"><span data-stu-id="4523d-220">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="4523d-221">新动画开始之前，将清除在该形状上运行的任何以前的动画。</span><span class="sxs-lookup"><span data-stu-id="4523d-221">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="4523d-222">按 F5 启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-222">Start the application by pressing F5.</span></span> <span data-ttu-id="4523d-223">复制页面的 URL，并将其粘贴到另一个浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="4523d-223">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="4523d-224">在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。</span><span class="sxs-lookup"><span data-stu-id="4523d-224">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="4523d-225">随着时间的推移，在另一个窗口中移动形状时应显示更少的抖动，而不是针对每个传入消息设置一次。</span><span class="sxs-lookup"><span data-stu-id="4523d-225">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="4523d-227">其他步骤</span><span class="sxs-lookup"><span data-stu-id="4523d-227">Further Steps</span></span>

<span data-ttu-id="4523d-228">在本教程中，已了解如何对在客户端和服务器之间发送高频消息的 SignalR 应用程序进行编程。</span><span class="sxs-lookup"><span data-stu-id="4523d-228">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="4523d-229">此通信模式适用于开发联机游戏和其他模拟，例如[通过 SignalR 创建的 ShootR 游戏](http://shootr.signalr.net)。</span><span class="sxs-lookup"><span data-stu-id="4523d-229">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="4523d-230">可以从[代码库](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下载本教程中创建的完整应用程序。</span><span class="sxs-lookup"><span data-stu-id="4523d-230">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="4523d-231">若要了解有关 SignalR 开发概念的详细信息，请访问 SignalR 源代码和资源的以下站点：</span><span class="sxs-lookup"><span data-stu-id="4523d-231">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="4523d-232">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="4523d-232">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="4523d-233">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="4523d-233">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="4523d-234">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="4523d-234">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
