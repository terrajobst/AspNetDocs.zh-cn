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
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>教程：入门 SignalR 1.x 和 MVC 4

作者： [Fletcher](https://github.com/pfletcher)、 [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教程介绍如何使用 ASP.NET SignalR 创建实时聊天应用程序。 将 SignalR 添加到 MVC 4 应用程序，并创建聊天视图来发送和显示消息。

## <a name="overview"></a>概述

本教程介绍了 ASP.NET SignalR 和 ASP.NET MVC 4 的实时 web 应用程序开发。 本教程使用与[SignalR 入门教程](tutorial-getting-started-with-signalr.md)相同的聊天应用程序代码，但演示了如何将其添加到基于 Internet 模板的 MVC 4 应用程序。

在本主题中，你将学习以下 SignalR 开发任务：

- 将 SignalR 库添加到 MVC 4 应用程序。
- 创建集线器类以将内容推送到客户端。
- 使用网页中的 SignalR jQuery library 发送消息并显示中心更新。

以下屏幕截图显示了在浏览器中运行的已完成的聊天应用程序。

![聊天实例](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

个

- [设置项目](#setup)
- [运行示例](#run)
- [检查代码](#code)
- [后续步骤](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>设置项目

先决条件：

- Visual Studio 2010 SP1、Visual Studio 2012 或 Visual Studio 2012 Express。 如果没有 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)以获取免费的 visual Studio 2012 Express 开发工具。
- 对于 Visual Studio 2010，请安装[ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)。

本部分介绍如何创建 ASP.NET MVC 4 应用程序、如何添加 SignalR 库，以及如何创建聊天应用程序。

1. 1. 在 Visual Studio 中，创建一个 ASP.NET MVC 4 应用程序，将其命名为 SignalRChat，然后单击 "确定"。

        > [!NOTE]
        > 在 VS 2010 中，选择 "Framework 版本" 下拉控件中的 **.NET Framework 4** 。 SignalR 代码在 .NET Framework 版本4和4.5 上运行。

        ![创建 mvc web](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. 选择 "Internet 应用程序" 模板，清除 "**创建单元测试项目**" 选项，然后单击 "确定"。

         ![创建 mvc internet 站点](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. **> NuGet 包管理器 "> 包管理器控制台**中打开" 工具 "，并运行以下命令。 此步骤将向项目添加一组启用 SignalR 功能的脚本文件和程序集引用。

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. 在**解决方案资源管理器**展开 "脚本" 文件夹。 请注意，SignalR 的脚本库已添加到项目。

         ![库引用](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. 在**解决方案资源管理器**中，右键单击项目，选择 "**添加" |新建文件夹**，并添加名为 "**中心**" 的新文件夹。
      6. 右键单击 "**中心**" 文件夹，单击 "**添加" |类**，并创建名为C# **ChatHub.cs**的新类。 你将使用此类作为将消息发送到所有客户端的 SignalR 服务器集线器。

> [!NOTE]
> 如果你使用 Visual Studio 2012 并安装了[ASP.NET 和 Web 工具2012.2 更新](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)，则可以使用 new SignalR 项模板来创建集线器类。 为此，请右键单击 "**中心**" 文件夹，单击 "**添加" |新建项**"，选择" **SignalR Hub 类（v1）** "，并将类命名为**ChatHub.cs**。

1. 将**ChatHub**类中的代码替换为以下代码。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. 为项目打开**global.asax**文件，并添加对方法的调用，`RouteTable.Routes.MapHubs();` 作为 `Application_Start` 方法中的第一行代码。 此代码将注册 SignalR 中心的默认路由，并且必须在注册任何其他路由之前调用此代码。 已完成的 `Application_Start` 方法类似于下面的示例。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. 编辑 controller **/HomeController**中找到的 `HomeController` 类，将以下方法添加到类。 此方法返回将在后面的步骤中创建的**聊天**视图。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. 在刚刚创建的 `Chat` 方法中右键单击，然后单击 "**添加视图**" 以创建新的视图文件。
5. 在 "**添加视图**" 对话框中，确保选中复选框以**使用布局或母版页**（清除其他复选框），然后单击 "**添加**"。

    ![添加视图](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. 编辑名为 " **Chat**" 的新视图文件。 &lt;h2&gt; 标记后，粘贴以下 &lt;div&gt; 部分，并将代码块 `@section scripts` 到页面中。 此脚本使页面可以发送聊天消息和显示来自服务器的消息。 下面的代码块中显示了聊天视图的完整代码。

    > [!IMPORTANT]
    > 将 SignalR 和其他脚本库添加到 Visual Studio 项目时，包管理器可能会安装比本主题中所示版本更新的脚本版本。 请确保代码中的脚本引用与你的项目中安装的脚本库的版本相匹配。

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. **全部保存**项目。

<a id="run"></a>

## <a name="run-the-sample"></a>运行示例

1. 按 F5 在调试模式下运行项目。
2. 在浏览器地址行中，将 **/home/chat**追加到项目默认页的 URL。 聊天页面加载到浏览器实例中，并提示输入用户名。

    ![输入用户名](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. 输入用户名。
4. 复制浏览器地址行中的 URL，并使用它打开另外两个浏览器实例。 在每个浏览器实例中，输入唯一的用户名。
5. 在每个浏览器实例中，添加注释并单击 "**发送**"。 注释应显示在所有浏览器实例中。

    > [!NOTE]
    > 这个简单的聊天应用程序不会在服务器上维护讨论上下文。 中心将注释广播给所有当前用户。 稍后加入聊天的用户将看到从他们加入的时间添加的消息。
6. 以下屏幕截图显示了在浏览器中运行的聊天应用程序。

    ![聊天浏览器](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. 在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。 如果使用 Internet Explorer 作为浏览器，则此节点在调试模式中可见。 有一个名为 "**中心**" 的脚本文件，SignalR 库会在运行时动态生成该文件。 此文件管理 jQuery 脚本和服务器端代码之间的通信。 如果使用 Internet Explorer 之外的浏览器，还可以通过直接浏览到动态**中心**文件，例如 http://mywebsite/signalr/hubs。

    ![生成的中心脚本](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>检查代码

SignalR chat 应用程序演示了两个基本的 SignalR 开发任务：将集线器创建为服务器上的主协调对象，并使用 SignalR jQuery library 发送和接收消息。

### <a name="signalr-hubs"></a>SignalR 中心

在代码示例中， **ChatHub**类派生自**SignalR**类。 从**Hub**类派生是构建 SignalR 应用程序的一种有用方法。 可以在中心类上创建公共方法，并通过在网页中从 jQuery 脚本调用这些方法来访问这些方法。

在聊天代码中，客户端调用**ChatHub**方法来发送新消息。 然后，集线器会通过调用**addNewMessageToPage**将消息发送到所有客户端。

**Send**方法演示了几个中心概念：

- 在中心声明公共方法，使客户端可以调用它们。
- 使用**SignalR**属性访问连接到此中心的所有客户端。
- 在客户端上调用 jQuery 函数（如 `addNewMessageToPage` 函数）以更新客户端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 和 jQuery

代码示例中的**Chat** view 文件演示了如何使用 SignalR jQuery 库与 SignalR 中心通信。 代码中的基本任务是为中心创建自动生成的代理的引用，并声明一个函数，服务器可以调用该函数将内容推送到客户端，并启动连接以向中心发送消息。

下面的代码声明一个集线器的代理。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> 在 jQuery 中，对服务器类及其成员的引用采用 camel 大小写格式。 此代码示例将 jQuery C#中的**ChatHub**类引用为**ChatHub**。 如果要在C#jQuery 中引用 `ChatHub` 类和传统的 Pascal 大小写，请编辑 ChatHub.cs 类文件。 添加 `using` 语句以引用 `Microsoft.AspNet.SignalR.Hubs` 命名空间。 然后，将 `HubName` 特性添加到 `ChatHub` 类，例如 `[HubName("ChatHub")]`。 最后，将 jQuery 引用更新到 `ChatHub` 类。

下面的代码演示如何在脚本中创建回调函数。 服务器上的 hub 类调用此函数将内容更新推送到每个客户端。 对 `htmlEncode` 函数的可选调用显示了一种在页中显示消息内容之前对其进行编码的方法，作为一种防止脚本注入的方式。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

下面的代码演示如何打开与中心的连接。 该代码启动连接，然后将其传递到 "聊天" 页的 "**发送**" 按钮上的 click 事件。

> [!NOTE]
> 此方法确保在事件处理程序执行之前建立连接。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>后续步骤

您已经了解到，SignalR 是一个框架，用于构建实时 web 应用程序。 还了解了几个 SignalR 开发任务：如何将 SignalR 添加到 ASP.NET 应用程序、如何创建集线器类，以及如何从集线器发送和接收消息。

若要了解更高级的 SignalR 开发概念，请访问以下站点以获取 SignalR 源代码和资源：

- [SignalR 项目](http://signalr.net)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
