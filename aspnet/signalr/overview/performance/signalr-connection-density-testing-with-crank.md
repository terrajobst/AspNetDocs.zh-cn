---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: 曲柄的 SignalR 连接密度测试 |Microsoft Docs
author: bradygaster
description: 使用曲柄实现 SignalR 连接密度测试
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 901e039fbb81651ed18d560c99745b7e7f716e01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449870"
---
# <a name="signalr-connection-density-testing-with-crank"></a>使用曲柄实现 SignalR 连接密度测试

作者： [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍如何使用曲柄工具测试具有多个模拟客户端的应用程序。

当应用程序在其宿主环境（Azure web 角色、IIS 或使用 Owin 自承载的环境）中运行后，可以使用曲柄工具测试应用程序对高级别连接密度的响应。 宿主环境可以是 Internet Information Services （IIS）服务器、Owin 主机或 Azure web 角色。 （注意：性能计数器在 Azure App Service Web 应用中不可用，因此你将无法从连接密度测试获取性能数据。）

连接密度是指可以在服务器上建立的同时 TCP 连接数。 每个 TCP 连接产生自己的开销，打开大量空闲连接将最终产生内存瓶颈。

[SignalR 基本代码](https://github.com/signalr/signalr)包含一个名为**曲柄**的负载测试工具。 最新版本的曲柄可在 GitHub 上[的开发分支](https://github.com/SignalR/signalr/tree/dev)中找到。 可在[此处](https://github.com/SignalR/SignalR/archive/dev.zip)下载 SignalR Codebase 的开发分支的 Zip 存档。

曲柄可用于完全使服务器的内存饱和，以便计算服务器硬件上可能的空闲连接总数。 或者，您也可以使用曲柄在一定量的内存压力下负载测试服务器，方法是在达到特定计数或特定内存阈值之前向上斜连接。

测试时，务必使用远程客户端以避免对资源（即 TCP 连接和内存）的任何竞赛。 监视客户端，以确保它们不会遇到可能阻止服务器达到其全部容量（内存或 CPU）的任何瓶颈。 为了完全加载服务器，你可能需要增加客户端的数量。

### <a name="running-a-connection-density-test"></a>运行连接密度测试

本部分介绍在 SignalR 应用程序上运行连接密度测试所需的步骤。

1. 下载并生成[SignalR 基本代码的开发分支](https://github.com/SignalR/SignalR/archive/dev.zip)。 在命令提示符下，导航到 &lt;项目目录 "&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug。
2. 将应用程序部署到其预期的宿主环境。 记下应用程序所使用的终结点;例如，在[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中创建的应用程序中，终结点是 `http://<yourhost>:8080/signalr`的。
3. 在服务器上安装[SignalR 性能计数器](signalr-performance.md#perfcounters)。 如果你的应用程序在 Azure 上运行，请参阅[在 Azure Web 角色中使用 SignalR 性能计数器](using-signalr-performance-counters-in-an-azure-web-role.md)。

下载并生成基本代码并在主机上安装性能计数器后，可以在 `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` 文件夹中找到曲柄命令行工具。

曲柄工具的可用选项包括：

- **/？** ：显示帮助屏幕。 如果省略**Url**参数，还会显示可用选项。
- **/Url**： SignalR 连接的 Url。 此参数是必需的。 对于使用默认映射的 SignalR 应用程序，该路径将以 "/signalr" 结尾。
- **/传输**：使用的传输名称。 默认值为 `auto`，这将选择最佳的可用协议。 选项包括 `WebSockets`、`ServerSentEvents`和 `LongPolling` （由于使用的是 .NET 客户端而不是 Internet Explorer，因此不能使用`ForeverFrame` 曲柄的选项）。 有关 SignalR 如何选择传输的详细信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。
- **/BatchSize**：每个批处理中添加的客户端数。 默认值为 50。
- **/ConnectInterval**：添加连接之间的间隔（以毫秒为单位）。 默认值为 500。
- **/Connections**：用于对应用程序进行负载测试的连接数。 默认值为100000。
- **/ConnectTimeout**：中止测试之前的超时时间（秒）。 默认值为300。
- **MinServerMBytes**：达到最小服务器兆字节。 默认值为 500。
- **SendBytes**：发送到服务器的负载的大小（以字节为单位）。 默认值为 0。
- **SendInterval**：消息与服务器之间的延迟（以毫秒为单位）。 默认值为 500。
- **SendTimeout**：消息发送到服务器的超时值（以毫秒为单位）。 默认值为300。
- **ControllerUrl**：一个客户端将在其中承载控制器集线器的 Url。 默认值为 null （无控制器中心）。 当曲柄会话启动时，将启动控制器中心;控制器中心与曲柄之间不会有任何其他联系。
- **NumClients**：要连接到应用程序的模拟客户端数量。 默认值为1。
- **Logfile**：用于测试运行的日志文件的文件名。 默认值为 `crank.csv`。
- **SampleInterval**：性能计数器样本之间的时间（以毫秒为单位）。 默认值为 1000。
- **SignalRInstance**：服务器上的性能计数器的实例名称。 默认情况下，使用客户端连接状态。

### <a name="example"></a>示例

以下命令将使用100连接在 Azure 上测试一个名为 "ControllerHub" 的站点，该 `pfsignalr` 站点使用名为 "" 的集线器在端口8080上托管应用程序。

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
