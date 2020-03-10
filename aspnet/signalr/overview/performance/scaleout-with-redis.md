---
uid: signalr/overview/performance/scaleout-with-redis
title: SignalR 扩展 with Redis |Microsoft Docs
author: bradygaster
description: 本主题中使用的软件版本 Visual Studio 2013 .NET 4.5 SignalR 版本2本主题的早期版本。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467774"
---
# <a name="signalr-scaleout-with-redis"></a>使用 Redis 的 SignalR 横向扩展

作者： [Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2。4
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

在本教程中，你将使用[Redis](http://redis.io/)在部署在两个不同 IIS 实例上的 SignalR 应用程序中分发消息。

Redis 是内存中的键-值存储。 它还支持发布/订阅模型的消息传送系统。 SignalR Redis 底板使用发布/订阅功能将消息转发到其他服务器。

![](scaleout-with-redis/_static/image1.png)

对于本教程，你将使用三个服务器：

- 运行 Windows 的两台服务器，你将使用它来部署 SignalR 应用程序。
- 一台运行 Linux 的服务器，你将使用它来运行 Redis。 对于本教程中的屏幕截图，我使用的是 Ubuntu 12.04 TLS。

如果没有要使用的三个物理服务器，则可以在 Hyper-v 上创建 Vm。 另一种方法是在 Azure 上创建 Vm。

尽管本教程使用的是官方 Redis 实现，但也有来自 MSOpenTech 的[Redis 的 Windows 端口](https://github.com/MSOpenTech/redis)。 安装和配置不同，但步骤是相同的。

> [!NOTE]
>
> 带 Redis 的 SignalR 扩展不支持 Redis 群集。

## <a name="overview"></a>概述

在学习详细教程之前，下面简要概述了你将执行的操作。

1. 安装 Redis 并启动 Redis 服务器。
2. 将以下 NuGet 包添加到应用程序：

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. 创建 SignalR 应用程序。
4. 将以下代码添加到 Startup.cs 以配置底板：

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-v 上的 Ubuntu

使用 Windows Hyper-v，你可以轻松地在 Windows Server 上创建 Ubuntu VM。

从[http://www.ubuntu.com](http://www.ubuntu.com/)下载 Ubuntu ISO。

在 Hyper-v 中，添加新的 VM。 在 "**连接虚拟硬盘**" 步骤中，选择 "**创建虚拟硬盘**"。

![](scaleout-with-redis/_static/image2.png)

在 "**安装选项**" 步骤中，选择 "**映像文件（.iso）** "，单击 "**浏览**"，然后浏览到 Ubuntu 安装 iso。

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>安装 Redis

按照[http://redis.io/download](http://redis.io/download)上的步骤下载并生成 Redis。

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

这会在 `src` 目录中生成 Redis 二进制文件。

默认情况下，Redis 不需要密码。 若要设置密码，请编辑位于源代码的根目录中的 `redis.conf` 文件。 （请在编辑之前创建文件的备份副本）将以下指令添加到 `redis.conf`：

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

现在启动 Redis 服务器：

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

打开端口6379，这是 Redis 侦听的默认端口。 （可以在配置文件中更改端口号。）

## <a name="create-the-signalr-application"></a>创建 SignalR 应用程序

通过以下任一教程创建 SignalR 应用程序：

- [入门 SignalR 2。0](../getting-started/tutorial-getting-started-with-signalr.md)
- [入门 SignalR 2.0 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

接下来，我们将修改聊天应用程序，以支持 Redis 的扩展。 首先，将 `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet 包添加到项目。 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

接下来，打开 Startup.cs 文件。 将以下代码添加到**配置**方法：

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "服务器" 是运行 Redis 的服务器的名称。
- *端口*号
- "密码" 是在 redis 文件中定义的密码。
- "AppName" 是任意字符串。 SignalR 创建具有此名称的 Redis pub/sub 通道。

例如:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>部署并运行应用程序

准备 Windows Server 实例以部署 SignalR 应用程序。

添加 IIS 角色。 包括 "应用程序开发" 功能，包括 WebSocket 协议。

![](scaleout-with-redis/_static/image5.png)

还包括管理服务（在 "管理工具" 下列出）。

![](scaleout-with-redis/_static/image6.png)

**安装 3.0 Web 部署。** 当你运行 IIS 管理器时，它将提示你安装 Microsoft Web 平台，或者你可以[下载该安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)。 在平台安装程序中，搜索 Web 部署并安装 Web 部署3。0

![](scaleout-with-redis/_static/image7.png)

检查 Web 管理服务是否正在运行。 如果不是，则启动该服务。 （如果在 Windows 服务列表中看不到 Web 管理服务，请确保在添加 IIS 角色时已安装管理服务。）

默认情况下，Web 管理服务在 TCP 端口8172上进行侦听。 在 Windows 防火墙中创建新的入站规则，以允许端口8172上的 TCP 流量。 有关详细信息，请参阅[配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。 （如果在 Azure 上托管 Vm，则可以直接在 Azure 门户中执行此操作。 请参阅[如何设置虚拟机的终结点](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。）

现在，你已准备好将 Visual Studio 项目从开发计算机部署到服务器。 在解决方案资源管理器中，右键单击该解决方案，然后单击 "**发布**"。

有关 web 部署的详细文档，请参阅[Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。

如果将应用程序部署到两个服务器，则可以在单独的浏览器窗口中打开每个实例，并查看每个实例是否分别接收 SignalR 消息。 （当然，在生产环境中，这两个服务器会位于负载均衡器的后面。）

![](scaleout-with-redis/_static/image8.png)

如果你想要查看发送到 Redis 的消息，可以使用**Redis-cli**客户端，该客户端安装有 Redis。

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
