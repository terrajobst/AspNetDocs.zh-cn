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
# <a name="high-frequency-realtime-with-signalr-1x"></a>使用 SignalR 1.x 实现高频率实时功能

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教程介绍如何创建使用 ASP.NET SignalR 的 web 应用程序，以提供高频率消息传递功能。 在这种情况下，高频率消息传送是指按固定费率发送的更新;对于此应用程序，每秒最多10条消息。
> 
> 你将在本教程中创建的应用程序将显示一个用户可拖动的形状。 然后，将更新其他所有连接的浏览器中形状的位置，使其与所拖动的形状的位置相匹配。
> 
> 本教程中介绍的概念具有实时游戏和其他模拟应用程序的应用程序。
> 
> 欢迎使用教程中的注释。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。

## <a name="overview"></a>概述

本教程演示如何创建一个应用程序，用于实时与其他浏览器共享对象的状态。 我们要创建的应用程序称为 MoveShape。 "MoveShape" 页将显示用户可拖动的 HTML Div 元素;当用户拖动 Div 时，它的新位置将被发送到服务器，然后将通知所有其他连接的客户端更新形状的位置以使其匹配。

![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

本教程中创建的应用程序基于 Damian Edwards 的演示。 [此处](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)显示了包含此演示的视频。

本教程将首先演示如何从每个在拖动形状时激发的事件发送 SignalR 消息。 每次收到消息时，每个连接的客户端都将更新形状的本地版本的位置。

当应用程序使用此方法运行时，这不是一种建议的编程模型，因为对发送的消息数没有上限，因此客户端和服务器可能会占用消息，而性能会下降. 客户端上显示的动画也会断开连接，因为每个方法会将形状立即移动，而不是顺利地移动到每个新位置。 本教程的后面部分将演示如何创建一个计时器函数，该函数可限制客户端或服务器发送消息的最大速率，以及如何在位置之间平稳移动形状。 可以从[代码库](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下载本教程中创建的应用程序的最终版本。

本教程包含以下部分：

- [先决条件](#prerequisites)
- [创建项目](#createtheproject)
- [添加 ASP.NET SignalR 和 JQuery. UI NuGet 包](#nugetpackages)
- [创建基本应用程序](#baseapp)
- [添加客户端循环](#clientloop)
- [添加服务器循环](#serverloop)
- [在客户端上添加平滑动画](#animation)
- [其他步骤](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>系统必备

本教程需要 Visual Studio 2012 或 Visual Studio 2010。 如果使用的是 Visual Studio 2010，则项目将使用 .NET Framework 4，而不是 .NET Framework 4.5。

如果使用的是 Visual Studio 2012，建议安装[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。 此更新包含新功能，如对发布、新功能和新模板的增强功能。

如果安装了 Visual Studio 2010，请确保已安装[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。

<a id="createtheproject"></a>

## <a name="create-the-project"></a>创建项目

在本部分中，我们将在 Visual Studio 中创建项目。

1. 从“文件”菜单上，单击“新建项目”。
2. 在 "**新建项目**" 对话框中， **C#** 展开 "**模板**"，然后选择 " **Web**"。
3. 选择**ASP.NET 空 Web 应用程序**模板，将项目命名为*MoveShapeDemo*，然后单击 **"确定"** 。

    ![创建新项目](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a>添加 SignalR 和 JQuery. UI NuGet 包

可以通过安装 NuGet 包将 SignalR 功能添加到项目。 本教程还将使用 JQuery. UI 包允许拖动和动画处理形状。

1. 单击 "**工具" |NuGet 包管理器 |程序包管理器控制台**。
2. 在 "包管理器" 中输入以下命令。

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    SignalR 包会安装多个其他 NuGet 包作为依赖项。 安装完成后，你将拥有在 ASP.NET 应用程序中使用 SignalR 所需的所有服务器和客户端组件。
3. 在包管理器控制台中输入以下命令以安装 JQuery 和 JQuery. UI 包。

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>创建基本应用程序

在本部分中，我们将创建一个浏览器应用程序，用于在每次鼠标移动事件时将形状的位置发送到服务器。 然后，服务器将此信息广播到所有其他已连接的客户端。 稍后我们将在此应用程序中展开此应用程序。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**"、"**类 ...** "。将类命名为**MoveShapeHub** ，然后单击 "**添加**"。
2. 将新的**MoveShapeHub**类中的代码替换为以下代码。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    上述 `MoveShapeHub` 类是 SignalR 中心的实现。 与[使用 SignalR 的入门](index.md)教程一样，此中心具有一个方法，客户端将直接调用该方法。 在这种情况下，客户端将向服务器发送包含形状的新 X 和 Y 坐标的对象，然后将该对象广播给所有其他连接的客户端。 SignalR 将使用 JSON 自动序列化此对象。

    将发送到客户端（`ShapeModel`）的对象包含存储形状位置的成员。 服务器上的对象的版本还包含用于跟踪正在存储的客户端数据的成员，以便不会向给定客户端发送其自己的数据。 此成员使用 `JsonIgnore` 特性来防止将其序列化并发送到客户端。
3. 接下来，我们将在应用程序启动时设置中心。 在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加" |全局应用程序类**。 接受 "*全局*" 的默认名称，然后单击 **"确定"** 。

    ![添加全局应用程序类](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. 将以下 `using` 语句添加到 Global.asax.cs 类中提供的**using**语句后面。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. 在全局类的 `Application_Start` 方法中添加以下代码行，以便为 SignalR 注册默认路由。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    Global.asax 文件应如下所示：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. 接下来，我们将添加客户端。 在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加" |新建项**。 在 "**添加新项**" 对话框中，选择 " **Html 页**"。 为该页指定一个适当的名称（如**html**），然后单击 "**添加**"。
7. 在**解决方案资源管理器**中，右键单击刚创建的页面，然后单击 "**设为起始页**"。
8. 将 HTML 页面中的默认代码替换为以下代码片段。

    > [!NOTE]
    > 验证下面的脚本引用是否与 "脚本" 文件夹中添加到项目中的包匹配。 在 Visual Studio 2010 中，添加到项目中的 JQuery 和 SignalR 的版本可能与以下版本号不匹配。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    上述 HTML 和 JavaScript 代码创建一个名为 Shape 的红色 Div，使用 jQuery library 启用形状的拖动行为，并使用形状的 `drag` 事件将该形状的位置发送到服务器。
9. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到另一个浏览器窗口中。 在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>添加客户端循环

由于在每个鼠标移动事件上发送形状的位置都将产生不必要的网络流量，因此需要限制来自客户端的消息。 我们将使用 javascript `setInterval` 函数设置一个循环，该循环将新位置信息按固定速率发送到服务器。 此循环是 "游戏循环" 的一个非常基本的表示形式，它是一个重复调用的函数，用于驱动游戏或其他模拟的所有功能。

1. 更新 HTML 页面中的客户端代码，以匹配以下代码片段。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    以上更新添加了 `updateServerModel` 函数，该函数将按固定频率调用。 只要 `moved` 标志指示存在要发送的新位置数据，此函数就会将位置数据发送到服务器。
2. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到另一个浏览器窗口中。 在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。 由于发送到服务器的消息数将会受到限制，因此，在上一节中，动画将不会显示为平滑。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>添加服务器循环

在当前应用程序中，从服务器发送到客户端的消息将在收到消息时接收。 这就是在客户端上出现的类似问题;消息的发送频率比需要的多，因此连接可能会变得溢出。 本部分介绍如何更新服务器以实现限制传出消息速率的计时器。

1. 将 `MoveShapeHub.cs` 的内容替换为以下代码段。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    上面的代码将扩展客户端以添加 `Broadcaster` 类，该类使用 .NET framework 中的 `Timer` 类来限制传出消息。

    由于中心本身是暂时的（每次需要时都会创建），因此 `Broadcaster` 将创建为单一实例。 迟缓初始化（在 .NET 4 中引入）用于将其创建延迟到需要的时间，从而确保在启动计时器之前完全创建第一个中心实例。

    然后，调用客户端的 `UpdateModel` 方法，以便在收到传入消息时，不会立即立即调用客户端的 `UpdateShape` 函数。 相反，发送到客户端的消息的速率为每秒25次调用，由 `_broadcastLoop` 计时器从 `Broadcaster` 类中管理。

    最后，`Broadcaster` 类需要使用 `GlobalHost`获取对当前操作中心（`_hubContext`）的引用，而不是直接从中心调用客户端方法。
2. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到另一个浏览器窗口中。 在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。 与上一节相比，浏览器中将不会有明显的区别，但会限制发送到客户端的消息数。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>在客户端上添加平滑动画

应用程序已几乎完成，但在客户端上的形状运动中，它可以提高一项改进，因为它是在响应服务器消息时移动的。 我们将使用 JQuery UI 库的 `animate` 函数在其当前位置与新位置之间平稳移动，而不是将形状的位置设置为服务器给定的新位置。

1. 将客户端的 `updateShape` 方法更新为类似于以下突出显示的代码：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    上面的代码将形状从旧位置移动到由服务器在动画时间间隔（在本例中为100毫秒）的过程中指定的新位置。 新动画开始之前，将清除在该形状上运行的任何以前的动画。
2. 按 F5 启动应用程序。 复制页面的 URL，并将其粘贴到另一个浏览器窗口中。 在其中一个浏览器窗口中拖动形状;其他浏览器窗口中的形状应移动。 随着时间的推移，在另一个窗口中移动形状时应显示更少的抖动，而不是针对每个传入消息设置一次。

    ![应用程序窗口](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>其他步骤

在本教程中，已了解如何对在客户端和服务器之间发送高频消息的 SignalR 应用程序进行编程。 此通信模式适用于开发联机游戏和其他模拟，例如[通过 SignalR 创建的 ShootR 游戏](http://shootr.signalr.net)。

可以从[代码库](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下载本教程中创建的完整应用程序。

若要了解有关 SignalR 开发概念的详细信息，请访问 SignalR 源代码和资源的以下站点：

- [SignalR 项目](http://signalr.net)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
