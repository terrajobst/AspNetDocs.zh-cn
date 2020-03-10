---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 动手实验：包含 SignalR 的实时 Web 应用程序 |Microsoft Docs
author: bradygaster
description: 实时 Web 应用程序可以将服务器端内容实时推送到已连接的客户端。 对于 ASP.NET 开发人员，ASP 。
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431666"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a>动手实验：包含 SignalR 的实时 Web 应用程序

由[Web 训练营团队](https://twitter.com/webcamps)使用

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[下载 Web 训练营培训工具包，10月2015版](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> 实时 Web 应用程序可以将服务器端内容实时推送到已连接的客户端。 对于 ASP.NET 开发人员而言， **ASP.NET SignalR**是一个库，用于向应用程序添加实时 web 功能。 它利用了多个传输，可在客户端和服务器的最佳传输中自动选择最佳的可用传输。 它利用了**WebSocket**，这是一个 HTML5 API，可在浏览器和服务器之间实现双向通信。
> 
> **SignalR**还提供了一个简单的高级 API，用于在你的 ASP.NET 应用程序中执行服务器到客户端 RPC （在客户端的浏览器中调用 JavaScript 函数），并为连接管理添加有用的挂钩，如连接/断开连接事件、分组连接和授权。
> 
> **SignalR**是对在客户端和服务器之间进行实时工作所需的某些传输的抽象。 **SignalR**连接以 HTTP 开头，然后将其升级到**WebSocket**连接（如果可用）。 **WebSocket**是适用于**SignalR**的理想传输，因为它可以最有效地使用服务器内存，具有最低的延迟，并且具有最基本的功能（如客户端和服务器之间的全双工通信），但它也具有最严格的要求： **WebSocket**要求服务器使用**Windows server 2012**或**windows 8**，以及 **.NET Framework 4.5**。 如果未满足这些要求， **SignalR**将尝试使用其他传输进行连接（如*Ajax 长时间轮询*）。
> 
> **SignalR** API 包含两种用于在客户端和服务器之间进行通信的模型：**持久性连接**和**中心**。 **连接**表示用于发送单接收方、分组或广播消息的简单终结点。 **中心**是一种基于连接 API 构建的更高级别管道，它允许客户端和服务器直接调用方法。
> 
> ![SignalR 体系结构](real-time-web-applications-with-signalr/_static/image1.png)
> 
> 所有示例代码和代码段都包含在2015年10月发布的 Web 训练营培训工具包中， [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)提供。  请注意，此页上的 "安装程序" 链接不再工作。改为使用 "资产" 部分下的链接之一。

<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 使用 SignalR 将通知从服务器发送到客户端。
- 使用**SQL Server**Scale Out SignalR 应用程序。

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下各项：

- Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行此动手实验中的练习，您需要先设置您的环境。

1. 打开 Windows 资源管理器窗口并浏览到实验室的**源**文件夹。
2. 右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。
3. 如果显示了 "用户帐户控制" 对话框，请确认操作以继续。

> [!NOTE]
> 确保在运行安装过程之前，您已检查本实验的所有依赖项。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。

> [!NOTE]
> 每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。 请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。 在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。 如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。

---

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [使用 SignalR 处理实时数据](#Exercise1)
2. [使用 SQL Server 横向扩展](#Exercise2)

完成本实验的估计时间： **60 分钟**

> [!NOTE]
> 首次启动 Visual Studio 时，必须选择一个预定义的设置集合。 每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。 此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。 如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>练习1：使用 SignalR 处理实时数据

尽管聊天通常用作示例，但您可以使用实时 Web 功能完成更多工作。 用户每次刷新网页以查看新数据或页面实现 Ajax 长轮询以检索新数据时，都可以使用 SignalR。

SignalR 支持**服务器推送**或**广播**功能;它会自动处理连接管理。 对于客户端-服务器通信的经典 HTTP 连接，为每个请求重新建立连接，但 SignalR 在客户端和服务器之间提供持续连接。 在 SignalR 中，服务器代码使用远程过程调用（RPC）来调用浏览器中的客户端代码，而不是我们今天知道的请求-响应模型。

在此练习中，您将配置**书呆子测验**应用程序以使用 SignalR 显示带有更新的指标的统计信息仪表板，而无需刷新整个页面。

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>任务1–浏览书呆子测验 Statistics 页面

在此任务中，您将完成应用程序并验证统计信息页的显示方式，以及如何改进信息的更新方式。

1. 打开**Web Visual Studio Express 2013** ，然后打开**Source\Ex1-WorkingWithRealTimeData\Begin**文件夹中的**GeekQuiz**解决方案。
2. 按 **“F5”** 运行该解决方案。 "**登录**" 页应出现在浏览器中。

    ![运行解决方案](real-time-web-applications-with-signalr/_static/image2.png "运行解决方案")

    *运行解决方案*
3. 在页面右上角单击 "**注册**"，以在应用程序中创建新用户。

    ![注册链接](real-time-web-applications-with-signalr/_static/image3.png "注册链接")

    *注册链接*
4. 在 "**注册**" 页上，输入**用户名**和**密码**，然后单击 "**注册**"。

    ![注册用户](real-time-web-applications-with-signalr/_static/image4.png "注册用户")

    *注册用户*
5. 应用程序将注册新帐户，并对用户进行身份验证，并重新定向回显示第一个测验问题的主页。
6. 在新窗口中打开 "**统计信息**" 页，并将 "**主页**" 和 "**统计信息**" 页并排放置。

    ![并行窗口](real-time-web-applications-with-signalr/_static/image5.png "并行窗口")

    *并行窗口*
7. 在**主页**中，通过单击其中一个选项来回答问题。

    ![回答问题](real-time-web-applications-with-signalr/_static/image6.png "回答问题")

    *回答问题*
8. 单击其中一个按钮后，将出现答案。

    ![答案正确](real-time-web-applications-with-signalr/_static/image7.png "答案正确")

    *正确回答的问题*
9. 请注意，"统计信息" 页中提供的信息已过时。 刷新页面以查看更新后的结果。

    ![统计信息页](real-time-web-applications-with-signalr/_static/image8.png "统计信息页")

    *统计信息页*
10. 返回到 Visual Studio，然后停止调试。

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>任务 2-将 SignalR 添加到书呆子测验以显示联机图表

在此任务中，将 SignalR 添加到解决方案，并在将新的答案发送到服务器时将更新发送到客户端。

1. 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后单击 "**程序包管理器控制台**"。
2. 在 "**包管理器控制台**" 窗口中，执行以下命令：

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR 包安装](real-time-web-applications-with-signalr/_static/image9.png "SignalR 包安装")

    *SignalR 包安装*

   > [!NOTE]
   > 在安装全新 MVC 5 应用程序的**SignalR** NuGet 包版本2.0.2 时，需要在安装 SignalR 之前，手动将**OWIN**包更新到2.0.1 版（或更高版本）。 为此，可以在**Package Manager Console**中执行以下脚本：
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > 在未来版本的 SignalR 中，OWIN 依赖项会自动更新。
3. 在**解决方案资源管理器**中，展开 "**脚本**" 文件夹，注意 SignalR *js*文件已添加到解决方案中。

    ![SignalR JavaScript 引用](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 引用")

    *SignalR JavaScript 引用*
4. 在**解决方案资源管理器**中，右键单击**GeekQuiz**项目，选择 "**添加** | "**新建文件夹**"，并将其命名为"**中心**"。
5. 右键单击 "**中心**" 文件夹，然后选择 "**添加 |新建项**。

    ![添加新项](real-time-web-applications-with-signalr/_static/image11.png "添加新项")

    *添加新项*
6. 在 "**添加新项**" 对话框中，选择**视觉C#对象 |Web |SignalR**节点在左窗格中，从中间窗格中选择 " **SignalR Hub 类（v2）** "，将文件命名为**StatisticsHub.cs** ，然后单击 "**添加**"。

    !["添加新项" 对话框](real-time-web-applications-with-signalr/_static/image12.png ""添加新项" 对话框")

    *"添加新项" 对话框*
7. 将**StatisticsHub**类中的代码替换为以下代码。

    （代码段- *RealTimeSignalR-Ex1-StatisticsHubClass*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. 打开**Startup.cs** ，并在**配置**方法的末尾添加以下行。

    （代码段- *RealTimeSignalR-Ex1-MapSignalR*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. 打开 "**服务**" 文件夹内的 " **StatisticsService.cs** " 页，并添加以下 using 指令。

    （代码段- *RealTimeSignalR-Ex1-UsingDirectives*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. 若要通知连接的客户端的更新，请先检索当前连接的**上下文**对象。 **Hub**对象包含向单个客户端发送消息或向所有连接的客户端发送消息的方法。 将以下方法添加到**StatisticsService**类，以便广播统计信息数据。

    （代码段- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > 在上面的代码中，你使用的是任意方法名称来调用客户端上的函数（即： *updateStatistics*）。 指定的方法名称被解释为动态对象，这意味着它没有 IntelliSense 或编译时验证。 在运行时计算表达式。 当执行方法调用时，SignalR 会将方法名称和参数值发送到客户端。 如果客户端具有与名称匹配的方法，则调用该方法并将参数值传递给它。 如果在客户端上找不到匹配的方法，则不会引发错误。 有关详细信息，请参阅[ASP.NET SignalR HUB API 指南](../guide-to-the-api/hubs-api-guide-server.md)。
11. 打开 "**控制器**" 文件夹内的 " **TriviaController.cs** " 页，并添加以下 using 指令。

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. 将以下突出显示的代码添加到**Post**操作方法。

    （代码段- *RealTimeSignalR-Ex1-NotifyUpdatesCall*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. 在视图中打开 " **Statistics** " 页 **|主**文件夹。 找到**脚本**部分，并在部分开头添加以下脚本引用。

    （代码段- *RealTimeSignalR-Ex1-SignalRScriptReferences*）

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > 将 SignalR 和其他脚本库添加到 Visual Studio 项目时，包管理器可能会安装比本主题中所示版本更新的 SignalR 脚本文件的版本。 请确保代码中的脚本引用与你的项目中安装的脚本库的版本相匹配。
14. 添加以下突出显示的代码，以将客户端连接到 SignalR 中心，并在从中心接收到新消息时更新统计信息数据。

    （代码段- *RealTimeSignalR-Ex1-SignalRClientCode*）

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    在此代码中，你将创建一个中心代理并注册事件处理程序以侦听服务器发送的消息。 在这种情况下，需要侦听通过*updateStatistics*方法发送的消息。

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>任务3–运行解决方案

在此任务中，您将运行解决方案以验证是否在回答新问题后使用 SignalR 自动更新了统计信息视图。

1. 按 **“F5”** 运行该解决方案。

    > [!NOTE]
    > 如果尚未登录到应用程序，请以在任务1中创建的用户身份登录。
2. 在新窗口中打开 "**统计信息**" 页，并将 "**主页**" 和 "**统计信息**" 页并排放置在任务1中。
3. 在**主页**中，通过单击其中一个选项来回答问题。

    ![回答其他问题](real-time-web-applications-with-signalr/_static/image13.png "回答其他问题")

    *回答其他问题*
4. 单击其中一个按钮后，将出现答案。 请注意，在用更新的信息回答问题后，会自动更新页面上的统计信息，而无需刷新整个页面。

    ![应答后刷新的统计信息页](real-time-web-applications-with-signalr/_static/image14.png "应答后刷新的统计信息页")

    *应答后刷新的统计信息页*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>练习2：使用 SQL Server 进行扩展

缩放 web 应用程序时，通常可以选择*纵向扩展*和*横向扩展*选项。 *向上缩放*意味着使用较大的服务器，具有更多资源（CPU、RAM 等），而向*外扩展*意味着添加更多服务器来处理负载。 后一种问题是客户端可以路由到不同的服务器。 连接到一台服务器的客户端将不会接收来自其他服务器的消息。

可以通过使用名为*底板*的组件来解决这些问题，以便在服务器之间转发消息。 启用底板后，每个应用程序实例会将消息发送到底板，并将其转发到其他应用程序实例。

目前有三种类型的 SignalR：

- **Windows Azure 服务总线**。 服务总线是一种消息传递基础结构，允许组件发送松散耦合的消息。
- **SQL Server**。 SQL Server 底板将消息写入 SQL 表中。 底板使用 Service Broker 来实现高效的消息传送。 不过，如果未启用 Service Broker，它也会起作用。
- **Redis**。 Redis 是内存中的键-值存储。 Redis 支持发布/订阅（"pub/sub"）模式来发送消息。

每条消息都是通过消息总线发送的。 消息总线实现了[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，该接口提供发布/订阅抽象。 通过使用为该底板设计的总线替换默认的**IMessageBus** ，可以使用底板。

每个服务器实例通过总线连接到底板。 发送消息时，消息会发送到底板，并且底板会将其发送到每台服务器。 当服务器从底板收到消息时，它会将消息存储在它的本地缓存中。 服务器随后将消息从其本地缓存传递给客户端。

有关 SignalR 底板工作方式的详细信息，请阅读此[文](../performance/scaleout-in-signalr.md)。

> [!NOTE]
> 在某些情况下，底板可能成为瓶颈。 下面是一些典型的 SignalR 方案：
> 
> - [服务器广播](tutorial-server-broadcast-with-signalr.md)（例如，股票行情）：对于此方案，背板工作良好，因为服务器控制发送消息的速率。
> - [客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）：在这种情况下，如果消息数量随客户端数量的增加，则底板可能是瓶颈;也就是说，如果随着更多客户端的加入，消息的速率会按比例增加。
> - [高频实时](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）：不建议在此方案中使用底板。

在此练习中，您将使用**SQL Server**在**书呆子测验**应用程序间分发消息。 你将在一台测试计算机上运行这些任务来了解如何设置配置，但为了获得完整效果，你将需要将 SignalR 应用程序部署到两个或更多服务器。 还必须在一台服务器或单独的专用服务器上安装 SQL Server。

![使用 SQL Server 关系图 Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>任务 1-了解方案

在此任务中，你将在本地计算机上运行2个模拟多个 IIS 实例的**书呆子**的实例。 在这种情况下，当在一个应用程序上回答琐碎内容问题时，不会在第二个实例的 "统计信息" 页上收到更新通知。 此模拟类似于在多个实例上部署应用程序，并使用负载均衡器与它们进行通信的环境。

1. 打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-ScalingOutWithSQLServer/begin**文件夹中的**Begin .sln**解决方案。 加载后，你会注意到**服务器资源管理器**解决方案包含两个具有相同结构但名称不同的项目。 这会模拟在本地计算机上运行同一应用程序的两个实例。

    ![模拟书呆子测验的2个实例的开始解决方案](real-time-web-applications-with-signalr/_static/image16.png "模拟书呆子测验的2个实例的开始解决方案")

    *模拟书呆子测验的2个实例的开始解决方案*
2. 右键单击解决方案节点，然后选择 "**属性**"，打开解决方案的 "属性" 页。 在 "**启动项目**" 下，选择 "**多个启动项目**"，并更改两个项目的 "**操作**"*值。*

    ![启动多个项目](real-time-web-applications-with-signalr/_static/image17.png "启动多个项目")

    *启动多个项目*
3. 按 **“F5”** 运行该解决方案。 应用程序将在不同的端口中启动两个**书呆子测验**实例，模拟同一个应用程序的多个实例。 将其中一个浏览器固定在屏幕的左侧和右侧。 使用你的凭据登录或注册新用户。 登录后，将 "琐碎内容" 页保留在左侧，然后在浏览器中的右侧浏览到 "**统计信息**" 页。

    ![并行书呆子测验](real-time-web-applications-with-signalr/_static/image18.png)

    *并行书呆子测验*

    ![不同端口中的书呆子测验](real-time-web-applications-with-signalr/_static/image19.png)

    *不同端口中的书呆子测验*
4. 在左侧浏览器中开始回答问题，你会注意到未更新正确浏览器中的 "**统计信息**" 页。 这是因为**SignalR**使用本地缓存在其客户端上分发消息，此方案模拟多个实例，因此不会在它们之间共享缓存。 可以通过测试相同的步骤，但使用单个应用来验证**SignalR**是否正常工作。 在以下任务中，您将配置底板以跨实例复制消息。
5. 返回到 Visual Studio，然后停止调试。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>任务2–创建 SQL Server 底板

在此任务中，你将创建一个将用作**书呆子测验**应用程序的底板的数据库。 你将使用**SQL Server 对象资源管理器**浏览服务器并初始化数据库。 此外，还将启用**Service Broker**。

1. 在**Visual Studio**中，打开菜单**视图**并选择**SQL Server 对象资源管理器**。
2. 右键单击 " **SQL Server** " 节点，然后选择 "**添加 SQL Server ...** " 选项，以连接到 LocalDB 实例。

    ![添加 SQL Server 实例](real-time-web-applications-with-signalr/_static/image20.png "添加 SQL Server 实例")

    *将 SQL Server 实例添加到 SQL Server 对象资源管理器*
3. 将**服务器名称**设置为 *（localdb） \v11.0* ，并将**Windows 身份验证**设置为身份验证模式。 单击“ **连接** ”以继续。

    ![连接到 LocalDB](real-time-web-applications-with-signalr/_static/image21.png "连接到 LocalDB")

    *连接到 LocalDB*
4. 现在，你已连接到 LocalDB 实例，你将需要创建一个将代表 SignalR 的 SQL Server 底板的数据库。 为此，请右键单击 "**数据库**" 节点，然后选择 "**添加新数据库**"。

    ![添加新数据库](real-time-web-applications-with-signalr/_static/image22.png "添加新数据库")

    *添加新数据库*
5. 将数据库名称设置为*SignalR* ，并单击 **"确定"** 以创建它。

    ![创建 SignalR 数据库](real-time-web-applications-with-signalr/_static/image23.png "创建 SignalR 数据库")

    *创建 SignalR 数据库*

    > [!NOTE]
    > 您可以为数据库选择任何名称。
6. 为了更有效地从底板接收更新，建议为数据库启用 Service Broker。 Service Broker 为 SQL Server 中的消息传递和排队提供本机支持。 在没有 Service Broker 的情况下，底板也能正常工作。 右键单击数据库并选择 "**新建查询**" 以打开新的查询。

    ![打开新查询](real-time-web-applications-with-signalr/_static/image24.png "打开新查询")

    *打开新查询*
7. 若要检查是否启用了 Service Broker，请在**sys.databases**目录视图中查询**是否\_Broker\_enabled**列。 在最近打开的查询窗口中执行以下脚本。

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![查询 Service Broker 状态](real-time-web-applications-with-signalr/_static/image25.png "查询 Service Broker 状态")

    *查询 Service Broker 状态*
8. 如果的值为数据库 **\_broker\_enabled**列 &quot;0&quot;，请使用以下命令启用它。 将 **&lt;数据库&gt;** 替换为创建数据库时设置的名称（例如： SignalR）。

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![启用 Service Broker](real-time-web-applications-with-signalr/_static/image26.png "启用 Service Broker")

    *启用 Service Broker*

    > [!NOTE]
    > 如果此查询显示为死锁，请确保没有任何应用程序连接到数据库。

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>任务3–配置 SignalR 应用程序

在此任务中，你将配置**书呆子测验**以连接到 SQL Server 底板。 你将首先添加**SignalR** NuGet 包，并将连接字符串设置为你的底板数据库。

1. 从 "**工具**" > **NuGet 包管理器**"中打开**包管理器控制台**。 请确保在 "**默认项目**" 下拉列表中选择 " **GeekQuiz**项目"。 键入以下命令以安装**SignalR** NuGet 包。

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. 重复上述步骤，但这一次是 project **GeekQuiz2**。
3. 若要配置 SQL Server 底板，请打开**GeekQuiz**项目的**Startup.cs**文件并将以下代码添加到**configure**方法。 将**数据库&gt;** 替换为在创建 SQL Server 底板时使用的数据库名称&lt;。 对于**GeekQuiz2**项目，请重复此步骤。

    （代码段- *RealTimeSignalR-buildingappswithcachingservice-ex2-getproducts latency-cs-StartupConfiguration*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. 现在，两个项目都配置为使用 SQL Server 底板，请按**F5**同时运行它们。
5. 同样， **Visual Studio**将在不同的端口中启动**书呆子测验**的两个实例。 在屏幕的左侧和右侧固定其中一个浏览器，然后用您的凭据登录。 将琐碎内容页保留在左侧，并在右侧浏览器中 pagein 到 " **Statistics** "。
6. 在左侧浏览器中开始回答问题。 这一次，由于底板将更新**统计信息**页。 在应用程序之间切换（**统计信息**现在位于左侧，**琐碎内容**位于右侧），并重复该测试以验证其是否适用于这两个实例。 该底板充当每个连接服务器的消息*共享缓存*，每个服务器都将这些消息存储在自己的本地缓存中，以分发到连接的客户端。
7. 返回到 Visual Studio，然后停止调试。
8. SQL Server 底板组件会自动在指定的数据库上生成必要的表。 在**SQL Server 对象资源管理器**面板中，打开为底板创建的数据库（例如： SignalR），然后展开其表。 应会看到以下表：

    ![底板生成的表](real-time-web-applications-with-signalr/_static/image27.png)

    *底板生成的表*
9. 右键单击 **\_0**表的 SignalR，然后选择 "**查看数据**"。

    ![查看 SignalR 底板消息表](real-time-web-applications-with-signalr/_static/image28.png)

    *查看 SignalR 底板消息表*
10. 解答琐碎内容问题时，可以看到发送到**中心**的不同消息。 该底板将这些消息分发给任何连接的实例。

    ![底板消息表](real-time-web-applications-with-signalr/_static/image29.png)

    *底板消息表*

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

在此动手实验中，你已了解如何使用**集线器**将**SignalR**添加到你的应用程序并将通知从服务器发送到连接的客户端。 此外，还了解了如何在多个 IIS 实例中部署应用程序时，通过使用*底板*组件来扩展应用程序。
