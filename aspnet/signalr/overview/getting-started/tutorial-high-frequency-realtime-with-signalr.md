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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600457"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>教程：通过 SignalR 2 创建高频实时应用

本教程介绍如何创建使用 ASP.NET SignalR 2 的 web 应用程序，以提供高频率消息传递功能。 在这种情况下，"高频率消息传递" 意味着服务器按固定费率发送更新。 每秒最多发送10条消息。

你创建的应用程序将显示一个用户可拖动的形状。 服务器会更新所有连接的浏览器中形状的位置，以匹配所拖动形状的位置。

本教程中介绍的概念具有实时游戏和其他模拟应用程序的应用程序。

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置项目
> * 创建基本应用程序
> * 在应用程序启动时映射到中心
> * 添加客户端
> * 运行应用
> * 添加客户端循环
> * 添加服务器循环
> * 添加平滑动画

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>先决条件

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) ，提供**ASP.NET 和 web 开发**工作负荷。

## <a name="set-up-the-project"></a>设置项目

在本部分中，将在 Visual Studio 2017 中创建项目。

本部分演示如何使用 Visual Studio 2017 创建空的 ASP.NET Web 应用程序并添加 SignalR 和 jQuery UI 库。

1. 在 Visual Studio 中，创建一个 ASP.NET Web 应用程序。

    ![创建 web](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. 在**新的 ASP.NET Web 应用程序-MoveShapeDemo**窗口中，保留**空**的选中状态，然后选择**确定**。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。

1. 在 **"添加新项-MoveShapeDemo**" 中，选择 "**安装** > **Visual C#**  > **Web** > " **SignalR** ，然后选择 " **SignalR Hub 类（v2）** "。

1. 将类命名为*MoveShapeHub* ，并将其添加到项目。

    此步骤将创建*MoveShapeHub.cs*类文件。 同时，它将一组支持 SignalR 的脚本文件和程序集引用添加到该项目中。

1.  > **NuGet 包管理器**" > **程序包管理器控制台**" 中选择 "**工具**"。

1. 在 "**程序包管理器控制台**" 中运行以下命令：

    ```console
    Install-Package jQuery.UI.Combined
    ```

    命令安装 jQuery UI 库。 用于对形状进行动画处理。

1. 在**解决方案资源管理器**中，展开 "脚本" 节点。

    ![脚本库引用](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    JQuery、jQueryUI 和 SignalR 的脚本库在项目中可见。

## <a name="create-the-base-application"></a>创建基本应用程序

在本部分中，将创建一个浏览器应用程序。 在每次鼠标移动事件期间，应用程序将形状的位置发送到服务器。 服务器会将此信息实时广播给其他所有连接的客户端。 稍后将详细介绍此应用程序。

1. 打开*MoveShapeHub.cs*文件。

1. 将*MoveShapeHub.cs*文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. 保存该文件。

`MoveShapeHub` 类是 SignalR 中心的实现。 与[使用 SignalR 的入门](tutorial-getting-started-with-signalr.md)教程一样，该中心还提供了一个客户端直接调用的方法。 在这种情况下，客户端将具有形状的新 X 和 Y 坐标的对象发送到服务器。 这些坐标将广播到所有其他已连接的客户端。 SignalR 使用 JSON 自动序列化此对象。

应用程序将 `ShapeModel` 对象发送到客户端。 它包含成员，用于存储形状的位置。 服务器上的对象的版本还具有跟踪正在存储的客户端数据的成员。 此对象可防止服务器将客户端的数据发回自身。 此成员使用 `JsonIgnore` 特性来阻止应用程序对数据进行序列化并将其发送回客户端。

## <a name="map-to-the-hub-when-app-starts"></a>在应用程序启动时映射到中心

接下来，在应用程序启动时设置到中心的映射。 在 SignalR 2 中，添加 OWIN startup 类将创建映射。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。

1. 在 "**添加新项"-MoveShapeDemo**选择 "**安装** > **Visual C#**  > **Web** "，然后选择 " **OWIN Startup 类**"。

1. 将类命名为 "*启动*"，然后选择 **"确定"** 。

1. 将*Startup.cs*文件中的默认代码替换为以下代码：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

当应用执行 `Configuration` 方法时，OWIN startup 类将调用 `MapSignalR`。 应用使用 `OwinStartup` 程序集特性将类添加到 OWIN 的启动进程。

## <a name="add-the-client"></a>添加客户端

为客户端添加 HTML 页面。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > " **HTML 页**"。

1. 将该页命名为**默认值**，然后选择 **"确定"** 。

1. 在**解决方案资源管理器**中，右键单击 " *Default .html* " 并选择 "**设为起始页**"。

1. 将*默认 .html*文件中的默认代码替换为以下代码：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. 在**解决方案资源管理器**中，展开 "**脚本**"。

    JQuery 和 SignalR 的脚本库在项目中可见。

    > [!IMPORTANT]
    > 包管理器安装 SignalR 脚本的更高版本。

1. 更新代码块中的脚本引用，使其与项目中的脚本文件版本相对应。

此 HTML 和 JavaScript 代码会创建一个名为 `shape`的红色 `div`。 它使用 jQuery library 启用形状的拖动行为，并使用 `drag` 事件将形状的位置发送到服务器。

## <a name="run-the-app"></a>运行应用

您可以运行应用程序，se'e 它工作。 当您在浏览器窗口周围拖动形状时，该形状也会移到其他浏览器中。

1. 在工具栏中，启用 "**脚本调试**"，然后选择 "播放" 按钮以调试模式运行应用程序。

    ![用户打开调试模式并选择 "播放" 的屏幕截图。](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    此时会打开一个浏览器窗口，并在右上角带有红色形状。

1. 复制页面的 URL。

1. 打开另一个浏览器，然后将 URL 粘贴到地址栏中。

1. 将该形状拖到一个浏览器窗口中。 其他浏览器窗口中的形状将如下所示。

当应用程序使用此方法运行时，它不是一种建议的编程模型。 发送的邮件数没有上限。 因此，客户端和服务器会使消息和性能下降。 此外，该应用在客户端上显示不连贯的动画。 这种抖动动画发生的原因是，形状会按每个方法即时移动。 如果形状平稳地移动到每个新位置，则效果更佳。 接下来，了解如何解决这些问题。

## <a name="add-the-client-loop"></a>添加客户端循环

将形状的位置发送到每个鼠标移动事件会创建不必要数量的网络流量。 应用需要限制客户端发送的消息。

使用 javascript `setInterval` 函数设置一个循环，该循环将新位置信息按固定速率发送到服务器。 此循环是 "游戏循环" 的基本表示形式。 这是一个重复调用的函数，用于驱动游戏的所有功能。

1. 将*默认 .html*文件中的客户端代码替换为以下代码：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > 必须再次替换脚本引用。 它们必须与项目中脚本的版本相匹配。

    此新代码将添加 `updateServerModel` 函数。 它按固定的频率调用。 只要 `moved` 标志指示存在要发送的新位置数据，函数就会将位置数据发送到服务器。

1. 选择 "播放" 按钮以启动应用程序

1. 复制页面的 URL。

1. 打开另一个浏览器，然后将 URL 粘贴到地址栏中。

1. 将该形状拖到一个浏览器窗口中。 其他浏览器窗口中的形状将如下所示。

由于应用会限制发送到服务器的消息数，因此，在第一次播放动画时不会显示为平滑。

## <a name="add-the-server-loop"></a>添加服务器循环

在当前的应用程序中，从服务器发送到客户端的消息将在收到消息时立即发送。 此网络流量显示了类似于客户端的问题。

应用程序的发送频率比需要的要多。 因此，连接可能会变得溢出。 本部分介绍如何更新服务器，以添加用于限制传出消息速率的计时器。

1. 将 `MoveShapeHub.cs` 的内容替换为以下代码：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. 选择 "播放" 按钮以启动应用程序。

1. 复制页面的 URL。

1. 打开另一个浏览器，然后将 URL 粘贴到地址栏中。

1. 将该形状拖到一个浏览器窗口中。

此代码扩展客户端以添加 `Broadcaster` 类。 新类使用 .NET framework 中的 `Timer` 类来限制传出消息。

了解中心本身是暂时性的。 它是每次需要时创建的。 因此，应用程序会将 `Broadcaster` 创建为单一实例。 它使用延迟初始化来将 `Broadcaster`的创建延迟到需要的时间。 这可确保应用程序在启动计时器之前完全创建第一个中心实例。

然后，调用客户端的 `UpdateShape` 函数，然后将其移出集线器的 `UpdateModel` 方法。 应用收到传入消息时，不再会立即调用此方法。 相反，应用以每秒25次调用的速率将消息发送到客户端。 此过程由 `Broadcaster` 类中的 `_broadcastLoop` 计时器进行管理。

最后，`Broadcaster` 类需要获取对当前操作的 `_hubContext` 中心的引用，而不是直接从中心调用客户端方法。 它获取具有 `GlobalHost`的引用。

## <a name="add-smooth-animation"></a>添加平滑动画

应用程序已几乎完成，但我们可以提高一项改进。 应用程序会在客户端上移动该形状，以响应服务器消息。 使用 JQuery UI 库的 `animate` 函数，而不是将形状的位置设置为服务器给定的新位置。 它可以在其当前位置和新位置之间平稳移动形状。

1. 更新*默认 .html*文件中客户端的 `updateShape` 方法，使其类似于突出显示的代码：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. 选择 "播放" 按钮以启动应用程序。

1. 复制页面的 URL。

1. 打开另一个浏览器，然后将 URL 粘贴到地址栏中。

1. 将该形状拖到一个浏览器窗口中。

在另一个窗口中的形状移动显示的是较差的抖动。 应用程序将在一段时间内插值，而不是针对每个传入消息进行一次设置。

此代码将形状从旧位置移到新位置。 服务器在动画间隔过程中提供形状的位置。 在本例中为100毫秒。 应用会在新动画开始之前清除该形状上运行的任何以前的动画。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>其他资源

刚才了解到的通信模式对于开发联机游戏和其他模拟非常有用，例如，[通过 SignalR 创建的 ShootR 游戏](https://shootr.azurewebsites.net/)。

有关 SignalR 的详细信息，请参阅以下资源：

* [SignalR 项目](http://signalr.net)

* [SignalR GitHub 和示例](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置项目
> * 已创建基本应用程序
> * 应用启动时映射到中心
> * 添加了客户端
> * 运行应用程序
> * 添加了客户端循环
> * 添加了服务器循环
> * 添加平滑动画

转到下一篇文章，了解如何创建使用 ASP.NET SignalR 2 提供服务器广播功能的 web 应用程序。
> [!div class="nextstepaction"]
> [SignalR 2 和服务器广播](tutorial-server-broadcast-with-signalr.md)