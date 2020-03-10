---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 教程：入门与 SignalR 1.x |Microsoft Docs
author: bradygaster
description: 在 HTML 页中使用 ASP.NET SignalR 生成实时聊天应用程序。
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505748"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a>教程： SignalR 1.x 入门

作者： [Fletcher](https://github.com/pfletcher)、 [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教程介绍如何使用 SignalR 创建实时聊天应用程序。 将 SignalR 添加到空的 ASP.NET web 应用程序，并创建用于发送和显示消息的 HTML 页面。

## <a name="overview"></a>概述

本教程介绍如何生成一个简单的基于浏览器的聊天应用程序，SignalR 开发。 将 SignalR 库添加到空的 ASP.NET web 应用程序，创建用于向客户端发送消息的集线器类，并创建允许用户发送和接收聊天消息的 HTML 页面。 有关演示如何使用 MVC 视图在 MVC 4 中创建聊天应用程序的类似教程，请参阅[使用 SignalR 和 MVC 4 入门](index.md)。

> [!NOTE]
> 本教程使用版本的 SignalR。 有关 SignalR 1.x 和2.0 之间的更改的详细信息，请参阅[升级 SignalR 1.X 项目](../releases/upgrading-signalr-1x-projects-to-20.md)。

SignalR 是一个开源 .NET 库，用于构建需要实时用户交互或实时数据更新的 web 应用程序。 示例包括社交应用程序、多用户游戏、业务协作和新闻、天气或金融更新应用程序。 这通常称为实时应用程序。

SignalR 简化了构建实时应用程序的过程。 它包括 ASP.NET 服务器库和 JavaScript 客户端库，以便更轻松地管理客户端-服务器连接和将内容更新推送到客户端。 可以将 SignalR 库添加到现有的 ASP.NET 应用程序中，以获取实时功能。

本教程演示以下 SignalR 开发任务：

- 将 SignalR 库添加到 ASP.NET web 应用程序。
- 创建集线器类以将内容推送到客户端。
- 使用网页中的 SignalR jQuery library 发送消息并显示中心更新。

以下屏幕截图显示了在浏览器中运行的聊天应用程序。 每个新用户都可以发布评论，并在用户加入聊天后查看添加的评论。

![聊天实例](tutorial-getting-started-with-signalr/_static/image1.png)

个

- [设置项目](#setup)
- [运行示例](#run)
- [检查代码](#code)
- [后续步骤](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>设置项目

本部分演示如何创建空的 ASP.NET web 应用程序、添加 SignalR 和创建聊天应用程序。

先决条件：

- Visual Studio 2010 SP1 或2012。 如果没有 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)以获取免费的 visual Studio 2012 Express 开发工具。
- [Microsoft ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)。 对于 Visual Studio 2012，此安装程序将新的 ASP.NET 功能（包括 SignalR 模板）添加到 Visual Studio。 对于 Visual Studio 2010 SP1，安装程序不可用，但你可以通过安装 SignalR NuGet 包来完成本教程，如安装步骤中所述。

以下步骤使用 Visual Studio 2012 创建 ASP.NET 空 Web 应用程序并添加 SignalR 库：

1. 在 Visual Studio 中创建 ASP.NET 空白 Web 应用程序。

    ![创建空 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. 通过选择 "工具" 打开**程序包管理器控制台** **|NuGet 包管理器 |程序包管理器控制台**。 在控制台窗口中输入以下命令：

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    此命令安装最新版本的 SignalR 1.x。
3. 在**解决方案资源管理器**中，右键单击项目，选择 "**添加" |类**。 将新类命名为**ChatHub**。
4. 在**解决方案资源管理器**展开 "脚本" 节点。 JQuery 和 SignalR 的脚本库在项目中可见。

    ![库引用](tutorial-getting-started-with-signalr/_static/image3.png)
5. 将**ChatHub**类中的代码替换为以下代码。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. 在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加" |新建项**。 在 "**添加新项**" 对话框中，选择 "**全局应用程序类**"，然后单击 "**添加**"。

    ![添加全局](tutorial-getting-started-with-signalr/_static/image4.png)
7. 将以下 `using` 语句添加到 Global.asax.cs 类中提供的 `using` 语句之后。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. 在全局类的 `Application_Start` 方法中添加以下代码行，以注册 SignalR 中心的默认路由。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. 在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加" |新建项**。 在 "**添加新项**" 对话框中，选择 "Html 页"，然后单击 "**添加**"。
10. 在**解决方案资源管理器**中，右键单击刚创建的 HTML 页面，然后单击 "**设为起始页**"。
11. 将 HTML 页面中的默认代码替换为以下代码。

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. **全部保存**项目。

<a id="run"></a>

## <a name="run-the-sample"></a>运行示例

1. 按 F5 在调试模式下运行项目。 HTML 页面加载到浏览器实例中，并提示输入用户名。

    ![输入用户名](tutorial-getting-started-with-signalr/_static/image5.png)
2. 输入用户名。
3. 复制浏览器地址行中的 URL，并使用它打开另外两个浏览器实例。 在每个浏览器实例中，输入唯一的用户名。
4. 在每个浏览器实例中，添加注释并单击 "**发送**"。 注释应显示在所有浏览器实例中。

    > [!NOTE]
    > 这个简单的聊天应用程序不会在服务器上维护讨论上下文。 中心将注释广播给所有当前用户。 稍后加入聊天的用户将看到从他们加入的时间添加的消息。

    以下屏幕截图显示了在三个浏览器实例中运行的聊天应用程序，其中的所有实例都在一个实例发送消息时进行更新：

    ![聊天浏览器](tutorial-getting-started-with-signalr/_static/image6.png)
5. 在**解决方案资源管理器**中，检查正在运行的应用程序的 "**脚本文档**" 节点。 有一个名为 "**中心**" 的脚本文件，SignalR 库会在运行时动态生成该文件。 此文件管理 jQuery 脚本和服务器端代码之间的通信。

    ![生成的中心脚本](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>检查代码

SignalR chat 应用程序演示了两个基本的 SignalR 开发任务：将集线器创建为服务器上的主协调对象，并使用 SignalR jQuery library 发送和接收消息。

### <a name="signalr-hubs"></a>SignalR 中心

在代码示例中， **ChatHub**类派生自**SignalR**类。 从**Hub**类派生是构建 SignalR 应用程序的一种有用方法。 可以在中心类上创建公共方法，并通过在网页中从 jQuery 脚本调用这些方法来访问这些方法。

在聊天代码中，客户端调用**ChatHub**方法来发送新消息。 然后，集线器会通过调用**broadcastMessage**将消息发送到所有客户端。

**Send**方法演示了几个中心概念：

- 在中心声明公共方法，使客户端可以调用它们。
- 使用**SignalR**动态属性来访问连接到此中心的所有客户端。
- 在客户端上调用 jQuery 函数（如 `broadcastMessage` 函数）以更新客户端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 和 jQuery

代码示例中的 HTML 页面显示了如何使用 SignalR jQuery 库与 SignalR 中心通信。 代码中的基本任务声明一个代理来引用中心，声明一个函数，服务器可以调用该函数将内容推送到客户端，并启动连接以将消息发送到中心。

下面的代码声明一个集线器的代理。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> 在 jQuery 中，对服务器类及其成员的引用采用 camel 大小写格式。 此代码示例将 jQuery C#中的**ChatHub**类引用为**ChatHub**。

下面的代码演示如何在脚本中创建回调函数。 服务器上的 hub 类调用此函数将内容更新推送到每个客户端。 在显示内容之前，HTML 对内容进行编码的两行均为可选，并显示一种防止脚本注入的简单方式。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

下面的代码演示如何打开与中心的连接。 该代码启动连接，然后将其传递给 HTML 页面的 "**发送**" 按钮上的 click 事件。

> [!NOTE]
> 此方法确保在事件处理程序执行之前建立连接。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>后续步骤

您已经了解到，SignalR 是一个框架，用于构建实时 web 应用程序。 还了解了几个 SignalR 开发任务：如何将 SignalR 添加到 ASP.NET 应用程序、如何创建集线器类，以及如何从集线器发送和接收消息。

可以通过将示例应用程序部署到托管提供程序，在本教程中或通过 Internet 提供的其他 SignalR 应用程序。 Microsoft 在免费的 microsoft [Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中为多达10个网站提供免费的 web 托管。 有关如何部署示例 SignalR 应用程序的演练，请参阅将[SignalR 入门示例发布为 Microsoft Azure](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)网站。 有关如何将 Visual Studio web 项目部署到 Microsoft Azure 网站的详细信息，请参阅将[ASP.NET 应用程序部署到 Microsoft azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)网站。 （注意： Microsoft Azure 网站当前不支持 WebSocket 传输。 当 WebSocket 传输不可用时，SignalR 会使用其他可用传输，如[SignalR 主题简介](index.md)部分中所述。）

若要了解更高级的 SignalR 开发概念，请访问以下站点以获取 SignalR 源代码和资源：

- [SignalR 项目](http://signalr.net)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
