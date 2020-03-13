---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: SignalR 扩展与 Azure 服务总线 |Microsoft Docs
author: bradygaster
description: 本主题中使用的软件版本 Visual Studio 2013 本主题的 SignalR 1.x 版本的本主题的 .NET 4.5 SignalR 版本2早期版本,。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467732"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a>使用 Azure 服务总线的 SignalR 横向扩展

作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

在本教程中，将 SignalR 应用程序部署到 Microsoft Azure Web 角色，使用服务总线底板将消息分发给每个角色实例。 （也可以[在 Azure App Service 中](https://docs.microsoft.com/azure/app-service-web/)将服务总线底板用于 web 应用。）

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

先决条件：

- 一个 Microsoft Azure 帐户。
- [Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。
- Visual Studio 2012 或 2013。

Service bus 底板还与[适用于 Windows Server 的服务总线](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)版本1.1 兼容。 但是，它与适用于 Windows Server 的服务总线1.0 版不兼容。

## <a name="pricing"></a>定价

Service Bus 底板使用主题发送消息。 有关最新定价信息，请参阅[服务总线](https://azure.microsoft.com/pricing/details/service-bus/)。 撰写本文时，可以每月发送1000000条消息，小于 $1。 该底板为 SignalR 集线器方法的每个调用发送服务总线消息。 还有一些用于连接、断开连接、加入或离开组等的控制消息。 在大多数应用程序中，大多数消息流量均为集线器方法调用。

## <a name="overview"></a>概述

在学习详细教程之前，下面简要概述了你将执行的操作。

1. 使用 Windows Azure 门户创建新的 Service Bus 命名空间。
2. 将以下 NuGet 包添加到应用程序： 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)或 SignalR. [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)
3. 创建 SignalR 应用程序。
4. 将以下代码添加到 Startup.cs 以配置底板： 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

此代码会将底板配置为[TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)的默认值。 有关更改这些值的信息，请参阅 [SignalR 性能：扩展指标](signalr-performance.md#scaleout_metrics)。

对于每个应用程序，请为 "YourAppName" 选择不同的值。 不要跨多个应用程序使用相同的值。

## <a name="create-the-azure-services"></a>创建 Azure 服务

按照[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中的说明创建云服务。 按照 "如何：使用 "快速创建" 创建云服务。 对于本教程，无需上载证书。

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

按照[如何使用服务总线主题/订阅](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)中的说明创建新的服务总线命名空间。 按照 "创建服务命名空间" 一节中的步骤进行操作。

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 请确保为云服务和服务总线命名空间选择相同的区域。

## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

启动 Visual Studio。 在“文件”菜单上，单击“新建项目”

在 "**新建项目**" 对话框中，展开 "**视觉对象C#** "。 在 "**已安装模板**" 下，选择 "**云**"，然后选择 " **microsoft Azure 云服务**"。 保持默认值 .NET Framework 4.5。 将应用程序命名为 ChatService，然后单击 **"确定"** 。

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

在 "**新建 Microsoft Azure 云服务**" 对话框中，选择 "ASP.NET Web 角色"。 单击右箭头按钮（ **&gt;** ）可将该角色添加到解决方案中。

将鼠标悬停在新角色上，使铅笔图标可见。 单击此图标可重命名角色。 将角色命名为 "SignalRChat"，然后单击 **"确定**"。

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC**"，然后单击 "确定"。

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

项目向导将创建两个项目：

- ChatService:此项目是 Microsoft Azure 应用程序。 它定义了 Azure 角色和其他配置选项。
- SignalRChat:此项目是你的 ASP.NET MVC 5 项目。

## <a name="create-the-signalr-chat-application"></a>创建 SignalR Chat 应用程序

若要创建聊天应用程序，请按照教程[入门 With SignalR AND MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)"中的步骤进行操作。

使用 NuGet 安装所需的库。 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在 "**程序包管理器控制台**" 窗口中，输入以下命令：

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

使用 `-ProjectName` 选项将包安装到 ASP.NET MVC 项目，而不是 Windows Azure 项目。

## <a name="configure-the-backplane"></a>配置底板

在应用程序的 Startup.cs 文件中，添加以下代码：

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

现在，需要获取服务总线连接字符串。 在 Azure 门户中，选择你创建的服务总线命名空间，然后单击 "访问密钥" 图标。

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

将连接字符串复制到剪贴板，然后将其粘贴到*connectionString*变量中。

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>部署到 Azure

在解决方案资源管理器中，展开 "ChatService" 项目中的 "**角色**" 文件夹。

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

右键单击 "SignalRChat" 角色，然后选择 "**属性**"。 选择“配置”选项卡。在 "**实例**" 下选择2。 你还可以将 VM 大小设置为 "**特小**"。

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

保存更改。

在解决方案资源管理器中，右键单击 ChatService 项目。 选择“发布”。

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

如果这是您首次发布到 Windows Azure，则必须下载您的凭据。 在**发布**向导中，单击 "登录以下载凭据"。 这会提示你登录到 Windows Azure 门户并下载发布设置文件。

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

单击 "**导入**" 并选择已下载的发布设置文件。

单击 **“下一步”** 。 在 "**发布设置**" 对话框中的 "**云服务**" 下，选择之前创建的云服务。

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

单击“发布”。 部署应用程序并启动 Vm 可能需要几分钟时间。

现在，在运行聊天应用程序时，角色实例将使用服务总线主题通过 Azure 服务总线进行通信。 主题是允许多个订阅服务器的消息队列。

该底板会自动创建主题和订阅。 若要查看订阅和消息活动，请打开 Azure 门户，选择服务总线命名空间，然后单击 "主题"。

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

需要几分钟时间，消息活动才会显示在仪表板中。

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

SignalR 管理主题生存期。 只要部署了你的应用程序，就不要尝试手动删除主题或更改主题的设置。

## <a name="troubleshooting"></a>故障排除

**InvalidOperationException "唯一支持的 IsolationLevel 为" IsolationLevel "。**

如果操作的事务级别设置为 `Serializable`以外的其他内容，则可能出现此错误。 验证是否未对其他事务级别执行任何操作。
