---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SignalR 扩展 with SQL Server （SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431126"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a>使用 SQL Server 的 SignalR 横向扩展 (SignalR 1.x)

作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

在本教程中，你将使用 SQL Server 在部署在两个不同 IIS 实例中的 SignalR 应用程序之间分配消息。 您还可以在一台测试计算机上运行本教程，但若要获得完整的效果，您需要将 SignalR 应用程序部署到两个或更多服务器。 还必须在一台服务器或单独的专用服务器上安装 SQL Server。 另一种方法是使用 Azure 上的 Vm 运行教程。

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>系统必备

Microsoft SQL Server 2005 或更高版本。 底板支持 SQL Server 的桌面版本和服务器版本。 它不支持 SQL Server Compact Edition 或 Azure SQL 数据库。 （如果你的应用程序托管在 Azure 上，请考虑改用服务总线底板。）

## <a name="overview"></a>概述

在学习详细教程之前，下面简要概述了你将执行的操作。

1. 创建新的空数据库。 该底板将在此数据库中创建所需的表。
2. 将以下 NuGet 包添加到应用程序： 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR。](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. 创建 SignalR 应用程序。
4. 将以下代码添加到 global.asax 以配置底板： 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a>配置数据库

确定应用程序是否将使用 Windows 身份验证或 SQL Server 身份验证来访问数据库。 无论如何，请确保数据库用户具有登录、创建架构和创建表的权限。

为要使用的底板创建新数据库。 您可以为数据库指定任意名称。 不需要在数据库中创建任何表;底板将创建所需的表。

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>启用 Service Broker

建议为底板数据库启用 Service Broker。 Service Broker 为 SQL Server 中的消息和队列提供本机支持，从而使底板更有效地接收更新。 （但是，底板也无需 Service Broker 即可工作。）

若要检查是否启用了 Service Broker，请在**sys.databases**目录视图中查询**是否\_Broker\_enabled**列。

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

若要启用 Service Broker，请使用以下 SQL 查询：

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> 如果此查询显示为死锁，请确保没有任何应用程序连接到数据库。

如果已启用跟踪，则跟踪还将显示是否启用 Service Broker。

## <a name="create-a-signalr-application"></a>创建 SignalR 应用程序

通过以下任一教程创建 SignalR 应用程序：

- [入门与 SignalR](../getting-started/tutorial-getting-started-with-signalr.md)
- [入门 SignalR 和 MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)

接下来，我们将修改聊天应用程序，以支持 SQL Server 的扩展。 首先，将 SignalR NuGet 包添加到项目。 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

接下来，打开 global.asax 文件。 将以下代码添加到**应用程序\_Start**方法：

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>部署并运行应用程序

准备 Windows Server 实例以部署 SignalR 应用程序。

添加 IIS 角色。 包括 "应用程序开发" 功能，包括 WebSocket 协议。

![](scaleout-with-sql-server/_static/image4.png)

还包括管理服务（在 "管理工具" 下列出）。

![](scaleout-with-sql-server/_static/image5.png)

**安装 3.0 Web 部署。** 当你运行 IIS 管理器时，它将提示你安装 Microsoft Web 平台，或者你可以[下载该安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)。 在平台安装程序中，搜索 Web 部署并安装 Web 部署3。0

![](scaleout-with-sql-server/_static/image6.png)

检查 Web 管理服务是否正在运行。 如果不是，则启动该服务。 （如果在 Windows 服务列表中看不到 Web 管理服务，请确保在添加 IIS 角色时已安装管理服务。）

最后，为 TCP 打开端口8172。 这是 Web 部署工具使用的端口。

现在，你已准备好将 Visual Studio 项目从开发计算机部署到服务器。 在解决方案资源管理器中，右键单击该解决方案，然后单击 "**发布**"。

有关 web 部署的详细文档，请参阅[Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。

如果将应用程序部署到两个服务器，则可以在单独的浏览器窗口中打开每个实例，并查看每个实例是否分别接收 SignalR 消息。 （当然，在生产环境中，这两个服务器会位于负载均衡器的后面。）

![](scaleout-with-sql-server/_static/image7.png)

运行应用程序后，可以看到 SignalR 已在数据库中自动创建了表：

![](scaleout-with-sql-server/_static/image8.png)

SignalR 管理表。 只要部署了应用程序，请不要删除行、修改表等。
