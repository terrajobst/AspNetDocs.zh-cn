---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 教程： SignalR 2 和 MVC 5 的实时聊天 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何使用 ASP.NET SignalR 2 创建实时聊天应用程序。 将 SignalR 添加到 MVC 5 应用程序。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600476"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a>教程： SignalR 2 和 MVC 5 的实时聊天

本教程介绍如何使用 ASP.NET SignalR 2 创建实时聊天应用程序。 将 SignalR 添加到 MVC 5 应用程序，并创建聊天视图来发送和显示消息。

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置项目
> * 运行示例
> * 检查代码

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>先决条件

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) ，提供**ASP.NET 和 web 开发**工作负荷。

## <a name="set-up-the-project"></a>设置项目

本部分演示如何使用 Visual Studio 2017 和 SignalR 2 创建一个空的 ASP.NET MVC 5 应用程序，添加 SignalR 库，并创建聊天应用程序。

1. 在 Visual Studio 中，创建C#一个面向 .NET Framework 4.5 的 ASP.NET 应用程序，将其命名为 SignalRChat，然后单击 "确定"。

    ![创建 web](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. 在**New ASP.NET Web 应用程序-SignalRMvcChat**中，选择 " **MVC** "，然后选择 "**更改身份验证**"。

1. 在 "**更改身份验证**" 中，选择 "**无身份验证**" 并单击 **"确定"**

    ![选择无身份验证](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. 在**New ASP.NET Web 应用程序-SignalRMvcChat**中，选择 **"确定"** 。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **新项**"。

1. 在 **"添加新项-SignalRChat**" 中，选择 "**安装** > **Visual C#**  > **Web** > " **SignalR** ，然后选择 " **SignalR Hub 类（v2）** "。

1. 将类命名为*ChatHub* ，并将其添加到项目。

    此步骤将创建*ChatHub.cs*类文件，并向项目中添加一组支持 SignalR 的脚本文件和程序集引用。

1. 将新的*ChatHub.cs*类文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加** > **类**"。

1. 将新类命名为*Startup* ，并将其添加到项目。

1. 将*Startup.cs*类文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. 在**解决方案资源管理器**中，选择 "**控制器**" > **HomeController.cs**"。

1. 将此方法添加到*HomeController.cs*。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    此方法返回在稍后的步骤中创建的**聊天**视图。

1. 在**解决方案资源管理器**中，右键单击 > **Home**"的"**视图**"，然后选择"**添加** >  **视图**"。

1. 在 "**添加视图**" 中，将新视图命名为 "**聊天**" 并选择 "**添加**"。

1. 将**Chat**的内容替换为以下代码：

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. 在**解决方案资源管理器**中，展开 "**脚本**"。

    JQuery 和 SignalR 的脚本库在项目中可见。

    > [!IMPORTANT]
    > 程序包管理器可能已安装了更高版本的 SignalR 脚本。

1. 检查代码块中的脚本引用是否对应于项目中的脚本文件的版本。

    从原始代码块编写引用脚本：

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. 如果二者不匹配，则更新该*cshtml*文件。

1. 从菜单栏中选择 "**文件**" > "**全部保存**"。

## <a name="run-the-sample"></a>运行示例

1. 在工具栏中，启用 "**脚本调试**"，然后选择 "播放" 按钮以调试模式运行该示例。

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. 当浏览器打开时，为聊天标识输入名称。

1. 从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。

1. 在每个浏览器中，输入唯一名称。

1. 现在，请添加注释，然后选择 "**发送**"。 在其他浏览器中重复此操作。 注释会实时显示。

    > [!NOTE]
    > 这个简单的聊天应用程序不会在服务器上维护讨论上下文。 中心将注释广播给所有当前用户。 稍后加入聊天的用户将看到从他们加入的时间添加的消息。

    了解如何在三种不同的浏览器中运行聊天应用程序。 当 Tom、Anand 和 Susan 发送消息时，所有浏览器都将实时更新：

    ![所有三个浏览器都显示相同的聊天历史记录](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. 在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。 有一个名为*hub*的脚本文件，SignalR 库会在运行时生成。 此文件管理 jQuery 脚本和服务器端代码之间的通信。

    ![脚本文档节点中自动生成的中心脚本](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a>检查代码

SignalR chat 应用程序演示了两个基本 SignalR 开发任务。 其中介绍了如何创建中心。 服务器使用该集线器作为主协调对象。 中心使用 SignalR jQuery library 来发送和接收消息。

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs 中的 SignalR 中心

在代码示例中，`ChatHub` 类派生自 `Microsoft.AspNet.SignalR.Hub` 类。 从 `Hub` 类派生是构建 SignalR 应用程序的一种有用方法。 可以在中心类上创建公共方法，并通过在网页中的脚本中调用这些方法来访问这些方法。

在聊天代码中，客户端调用 `ChatHub.Send` 方法来发送新消息。 集线器会通过调用 `Clients.All.addNewMessageToPage`将消息发送到所有客户端。

`Send` 方法演示了几个中心概念：

* 在中心声明公共方法，使客户端可以调用它们。

* 使用 `Microsoft.AspNet.SignalR.Hub.Clients` 动态属性与连接到此集线器的所有客户端通信。

* 在客户端上调用一个函数（如 `addNewMessageToPage` 函数）以更新客户端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a>SignalR 和 jQuery Chat

代码示例中的*Chat* view 文件演示了如何使用 SignalR jQuery 库与 SignalR 中心通信。  此代码将执行许多重要的任务。 它将创建对中心自动生成的代理的引用，并声明一个函数，服务器可以调用该函数将内容推送到客户端，并且启动连接以向中心发送消息。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> 在 JavaScript 中，对服务器类及其成员的引用位于 camelCase 中。 此代码示例将 JavaScript C#中的 `ChatHub` 类引用为 `chatHub`。

在此代码块中，你将在脚本中创建一个回调函数。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

服务器上的 hub 类调用此函数将内容更新推送到每个客户端。 对 `htmlEncode` 函数的可选调用显示了一种在页中显示消息内容之前对消息内容进行 HTML 编码的方法。 这是一种防止脚本注入的方式。

此代码将打开与中心的连接。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> 此方法确保在事件处理程序执行之前建立连接。

该代码启动连接，然后将其传递到 "聊天" 页的 "**发送**" 按钮上的 click 事件。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a>其他资源

有关 SignalR 的详细信息，请参阅以下资源：

* [SignalR 项目](http://signalr.net)

* [SignalR GitHub 和示例](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置项目
> * 运行示例
> * 检查代码

转到下一篇文章，了解如何创建使用 ASP.NET SignalR 2 的 web 应用程序，以提供高频率消息传递功能。
> [!div class="nextstepaction"]
> [具有高频率消息传送的 Web 应用](tutorial-high-frequency-realtime-with-signalr.md)