---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: SignalR 扩展与 Azure 服务总线（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449936"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a>使用 Azure 服务总线的 SignalR 横向扩展 (SignalR 1.x)

作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

在本教程中，将 SignalR 应用程序部署到 Microsoft Azure Web 角色，使用服务总线底板将消息分发给每个角色实例。

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

先决条件：

- 一个 Microsoft Azure 帐户。
- [Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。
- Visual Studio 2012。

Service bus 底板还与[适用于 Windows Server 的服务总线](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)版本1.1 兼容。 但是，它与适用于 Windows Server 的服务总线1.0 版不兼容。

## <a name="pricing"></a>定价

Service Bus 底板使用主题发送消息。 有关最新定价信息，请参阅[服务总线](https://azure.microsoft.com/pricing/details/service-bus/)。 撰写本文时，可以每月发送1000000条消息，小于 $1。 该底板为 SignalR 集线器方法的每个调用发送服务总线消息。 还有一些用于连接、断开连接、加入或离开组等的控制消息。 在大多数应用程序中，大多数消息流量均为集线器方法调用。

## <a name="overview"></a>概述

在学习详细教程之前，下面简要概述了你将执行的操作。

1. 使用 Windows Azure 门户创建新的 Service Bus 命名空间。
2. 将以下 NuGet 包添加到应用程序： 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR。](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. 创建 SignalR 应用程序。
4. 将以下代码添加到 global.asax 以配置底板： 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

对于每个应用程序，请为 "YourAppName" 选择不同的值。 不要跨多个应用程序使用相同的值。

## <a name="create-the-azure-services"></a>创建 Azure 服务

按照[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中的说明创建云服务。 按照 "如何：使用快速创建创建云服务" 一节中的步骤进行操作。 对于本教程，无需上载证书。

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

按照[如何使用服务总线主题/订阅](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)中的说明创建新的服务总线命名空间。 按照 "创建服务命名空间" 一节中的步骤进行操作。

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 请确保为云服务和服务总线命名空间选择相同的区域。

## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

启动 Visual Studio。 在“文件”菜单上，单击“新建项目”

在 "**新建项目**" 对话框中，展开 "**视觉对象C#** "。 在 "**已安装模板**" 下，选择 "**云**"，然后选择 " **microsoft Azure 云服务**"。 保持默认值 .NET Framework 4.5。 将应用程序命名为 ChatService，然后单击 **"确定"** 。

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

在 "**新建 Microsoft Azure 云服务**" 对话框中，选择 "ASP.NET MVC 4 Web 角色"。 单击右箭头按钮（ **&gt;** ）可将该角色添加到解决方案中。

将鼠标悬停在新角色上，使铅笔图标可见。 单击此图标可重命名角色。 将角色命名为 "SignalRChat"，然后单击 **"确定**"。

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

在**New ASP.NET MVC 4 项目**向导中，选择 " **Internet 应用程序**"。 单击“确定”。 项目向导将创建两个项目：

- ChatService：此项目是 Microsoft Azure 应用程序。 它定义了 Azure 角色和其他配置选项。
- SignalRChat：此项目是 ASP.NET MVC 4 项目。

## <a name="create-the-signalr-chat-application"></a>创建 SignalR Chat 应用程序

若要创建聊天应用程序，请按照教程[入门 With SignalR AND MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)"中的步骤进行操作。

使用 NuGet 安装所需的库。 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在 "**程序包管理器控制台**" 窗口中，输入以下命令：

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

使用 `-ProjectName` 选项将包安装到 ASP.NET MVC 项目，而不是 Windows Azure 项目。

## <a name="configure-the-backplane"></a>配置底板

在应用程序的 global.asax 文件中，添加以下代码：

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

现在，需要获取服务总线连接字符串。 在 Azure 门户中，选择你创建的服务总线命名空间，然后单击 "访问密钥" 图标。

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

将连接字符串复制到剪贴板，然后将其粘贴到*connectionString*变量中。

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>部署到 Azure

在解决方案资源管理器中，展开 "ChatService" 项目中的 "**角色**" 文件夹。

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

右键单击 "SignalRChat" 角色，然后选择 "**属性**"。 选择 "**配置**" 选项卡。在 "**实例**" 下选择2。 你还可以将 VM 大小设置为 "**特小**"。

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

保存更改。

在解决方案资源管理器中，右键单击 ChatService 项目。 选择“发布”。

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

如果这是您首次发布到 Windows Azure，则必须下载您的凭据。 在**发布**向导中，单击 "登录以下载凭据"。 这会提示你登录到 Windows Azure 门户并下载发布设置文件。

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

单击 "**导入**" 并选择已下载的发布设置文件。

单击 **“下一步”** 。 在 "**发布设置**" 对话框中的 "**云服务**" 下，选择之前创建的云服务。

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

单击“发布”。 部署应用程序并启动 Vm 可能需要几分钟时间。

现在，在运行聊天应用程序时，角色实例将使用服务总线主题通过 Azure 服务总线进行通信。 主题是允许多个订阅服务器的消息队列。

该底板会自动创建主题和订阅。 若要查看订阅和消息活动，请打开 Azure 门户，选择服务总线命名空间，然后单击 "主题"。

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

需要几分钟时间，消息活动才会显示在仪表板中。

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

SignalR 管理主题生存期。 只要部署了你的应用程序，就不要尝试手动删除主题或更改主题的设置。
