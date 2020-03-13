---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 教程：SignalR 2 的实时聊天 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431564"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>教程：通过 SignalR 2 进行实时聊天

本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序，并创建用于发送和显示消息的 HTML 页面。

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置项目
> * 运行示例
> * 检查代码

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>系统必备

* 带有 ASP.NET 和 Web 开发工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。

## <a name="set-up-the-project"></a>设置项目

本部分演示如何使用 Visual Studio 2017 和 SignalR 2 创建一个空的 ASP.NET web 应用程序，添加 SignalR，并创建聊天应用程序。

1. 在 Visual Studio 中，创建一个 ASP.NET Web 应用程序。

    ![创建 web](tutorial-getting-started-with-signalr/_static/image2.png)

1. 在**新的 ASP.NET 项目-SignalRChat**窗口中，保留**空**的选中状态，然后选择 **"确定"** 。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。

1. 在 **"添加新项-SignalRChat**" 中，选择 "**安装** > **Visual C#**  > **Web** > " **SignalR** ，然后选择 " **SignalR Hub 类（v2）** "。

1. 将类命名为*ChatHub* ，并将其添加到项目。

    此步骤将创建*ChatHub.cs*类文件，并向项目中添加一组支持 SignalR 的脚本文件和程序集引用。

1. 将新的*ChatHub.cs*类文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。

1. 在 "**添加新项"-SignalRChat**选择 "**安装** > **Visual C#**  > **Web** "，然后选择 " **OWIN Startup 类**"。

1. 将类命名为*Startup* ，并将其添加到项目。

1. 将*Startup*类中的默认代码替换为以下代码：

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > " **HTML 页**"。

1. 为新页*索引*命名，然后选择 **"确定"** 。

1. 在**解决方案资源管理器**中，右键单击创建的 HTML 页面，然后选择 "**设为起始页**"。

1. 将 HTML 页面中的默认代码替换为以下代码：

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. 在**解决方案资源管理器**中，展开 "**脚本**"。

    JQuery 和 SignalR 的脚本库在项目中可见。

    > [!IMPORTANT]
    > 程序包管理器可能已安装了更高版本的 SignalR 脚本。

1. 检查代码块中的脚本引用是否对应于项目中的脚本文件的版本。

    从原始代码块编写引用脚本：

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. 如果二者不匹配，则更新 *.html*文件。

1. 从菜单栏中选择 "**文件**" > "**全部保存**"。

## <a name="run-the-sample"></a>运行示例

1. 在工具栏中，启用 "**脚本调试**"，然后选择 "播放" 按钮以调试模式运行该示例。

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image3.png)

1. 当浏览器打开时，为聊天标识输入名称。

1. 从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。

1. 在每个浏览器中，输入唯一名称。

1. 现在，请添加注释，然后选择 "**发送**"。 在其他浏览器中重复此操作。 注释会实时显示。

    > [!NOTE]
    > 这个简单的聊天应用程序不会在服务器上维护讨论上下文。 中心将注释广播给所有当前用户。 稍后加入聊天的用户将看到从他们加入的时间添加的消息。

    了解如何在三种不同的浏览器中运行聊天应用程序。 当 Tom、Anand 和 Susan 发送消息时，所有浏览器都将实时更新：

    ![所有三个浏览器都显示相同的聊天历史记录](tutorial-getting-started-with-signalr/_static/image4.png)

1. 在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。 有一个名为*hub*的脚本文件，SignalR 库会在运行时生成。 此文件管理 jQuery 脚本和服务器端代码之间的通信。

    ![脚本文档节点中自动生成的中心脚本](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>检查代码

SignalRChat 应用程序演示了两个基本 SignalR 开发任务。 其中介绍了如何创建中心。 服务器使用该集线器作为主协调对象。 中心使用 SignalR jQuery library 来发送和接收消息。

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs 中的 SignalR 中心

在上面的代码示例中，`ChatHub` 类派生自 `Microsoft.AspNet.SignalR.Hub` 类。 从 `Hub` 类派生是构建 SignalR 应用程序的一种有用方法。 可以在中心类上创建公共方法，并通过在网页中的脚本中调用这些方法来使用这些方法。

在聊天代码中，客户端调用 `ChatHub.Send` 方法来发送新消息。 然后，集线器通过调用 `Clients.All.broadcastMessage`将消息发送到所有客户端。

`Send` 方法演示了几个中心概念：

* 在中心声明公共方法，使客户端可以调用它们。

* 使用 `Microsoft.AspNet.SignalR.Hub.Clients` 动态属性与连接到此集线器的所有客户端通信。

* 在客户端上调用一个函数（如 `broadcastMessage` 函数）以更新客户端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>索引中的 SignalR 和 jQuery

代码示例中的 "*索引*" 页显示了如何使用 SignalR jQuery 库与 SignalR 中心通信。 此代码将执行许多重要的任务。 它声明了一个代理来引用中心，并声明了一个函数，服务器可以调用该函数将内容推送到客户端，并启动一个连接将消息发送到中心。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> 在 JavaScript 中，对服务器类及其成员的引用必须是 camelCase。 此代码示例引用 JavaScript C#中的*ChatHub*类作为 `chatHub`。

在此代码块中，你将在脚本中创建一个回调函数。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

服务器上的 hub 类调用此函数将内容更新推送到每个客户端。 在显示之前对内容进行 HTML 编码的两行是可选的，并显示一种防止脚本注入的好办法。

此代码将打开与中心的连接。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> 此方法可确保代码在事件处理程序执行之前建立连接。

该代码启动连接，然后将其传递给 HTML 页面的 "**发送**" 按钮上的 click 事件。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>其他资源

有关 SignalR 的详细信息，请参阅以下资源：

* [SignalR 项目](http://signalr.net)

* [SignalR Github 和示例](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>后续步骤

在本教程中，你将：

> [!div class="checklist"]
> * 设置项目
> * 运行示例
> * 检查代码

转到下一篇文章，了解如何使用 SignalR 和 MVC 5。
> [!div class="nextstepaction"]
> [SignalR 2 和 MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)