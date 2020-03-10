---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: 在 Azure App Service 中将 SignalR 用于 Web 应用 |Microsoft Docs
author: bradygaster
description: 本文档介绍如何配置 Microsoft Azure 上运行的 SignalR 应用程序。 教程 Visual Studio 2013 或 Vis 中使用的软件版本 。
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450182"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>在 Azure 应用服务中通过 Web 应用使用 SignalR

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍如何配置 Microsoft Azure 上运行的 SignalR 应用程序。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)或 Visual Studio 2012
> - .NET 4.5
> - SignalR 版本2
> - 适用于 Visual Studio 2013 的 Azure SDK 2.3 或2012
>
>
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)、 [StackOverflow.com](http://stackoverflow.com/)或[Microsoft Azure 论坛](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)。

## <a name="table-of-contents"></a>目录

- [介绍](#introduction)
- [将 SignalR Web 应用部署到 Azure App Service](#deploying)
- [在 Azure App Service 上启用 Websocket](#websocket)
- [使用 Azure Redis 缓存底板](#backplane)
- [后续步骤](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>简介

ASP.NET SignalR 可用于在服务器和 web 或 .NET 客户端之间引入新的交互级别。 托管在 Azure 中时，SignalR 的应用程序可以利用在云中运行的高度可用、可缩放且高性能的环境。

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>将 SignalR Web 应用部署到 Azure App Service

SignalR 不会将应用程序部署到 Azure 与部署到本地服务器的任何特定复杂之处。 可以在 Azure 中托管使用 SignalR 的应用程序，而无需更改配置或其他设置（但对于 Websocket 支持，请参阅下面[Azure App Service 上的启用 websocket](#websocket) 。）对于本教程，请将[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中创建的应用程序部署到 Azure。

**先决条件**

- Visual Studio 2013。 如果没有 Visual Studio，则在安装 Azure SDK 时，将 Visual Studio 2013 Express for Web。
- [用于 Visual Studio 2013 的 AZURE sdk 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409)或[用于 Visual Studio 2012 的 azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)。
- 若要完成本教程，你需要一个 Azure 订阅。 可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，或[注册试用版订阅](https://azure.microsoft.com/pricing/free-trial/)。

### <a name="deploying-a-signalr-web-app-to-azure"></a>将 SignalR web 应用部署到 Azure

1. 完成[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)，或者从[代码库](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下载完成的项目。
2. 在 Visual Studio 中，选择 "**生成**"，**发布 SignalR Chat**。
3. 在 "发布 Web" 对话框中，选择 "Microsoft Azure 网站"。

    ![选择 Azure 网站](using-signalr-with-azure-web-sites/_static/image1.png)
4. 如果你未登录到 Microsoft 帐户，请单击 "选择现有网站" 对话框中的 "**登录 ...** "，然后登录。

    ![选择现有网站](using-signalr-with-azure-web-sites/_static/image2.png)    ![登录 Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. 在 "选择现有网站" 对话框中，单击 "**新建**"。

    ![新建网站](using-signalr-with-azure-web-sites/_static/image4.png)
6. 在 "在 Microsoft Azure 上创建站点" 对话框中，输入唯一的应用名称。 在 "区域" 下拉列表中选择离你最近的区域。 单击 **“创建”** 。

    ![在 Azure 中创建网站](using-signalr-with-azure-web-sites/_static/image5.png)
7. 在 "发布 Web" 对话框中，单击 "**发布**"。

    ![发布站点](using-signalr-with-azure-web-sites/_static/image6.png)
8. 当应用完成发布时，Azure App Service Web Apps 中承载的 SignalR Chat 应用程序将在浏览器中打开。

    ![站点在浏览器中打开](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>在 Azure App Service Web 应用上启用 Websocket

需要在 web 应用中显式启用 Websocket，才能在 SignalR 应用程序中使用;否则，将使用其他协议（有关详细信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)）。

若要在 Azure App Service Web 应用上使用 Websocket，请在 web 应用的 "配置" 部分中启用它。 为此，请在[Azure 管理门户](https://manage.windowsazure.com/)中打开 web 应用，并选择 "配置"。

![配置选项卡](using-signalr-with-azure-web-sites/_static/image8.png)

在配置页的顶部，确保将 .NET 4.5 用于 web 应用。

![.NET framework 4.5 版设置](using-signalr-with-azure-web-sites/_static/image9.png)

在 "配置" 页上，在 " **websocket** " 设置中选择 **"打开**"。

![Websocket 设置：开启](using-signalr-with-azure-web-sites/_static/image10.png)

在配置页的底部，选择 "**保存**" 以保存所做的更改。

![保存设置](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>使用 Azure Redis 缓存底板

如果你使用 web 应用的多个实例，并且这些实例的用户需要彼此交互（例如，在一个实例中创建的聊天消息可以访问连接到其他实例的用户），则必须在应用程序中实现[Azure Redis 缓存底板](../performance/scaleout-with-redis.md)。

<a id="nextsteps"></a>
## <a name="next-steps"></a>后续步骤

有关 Azure App Service 中 Web 应用的详细信息，请参阅[Web 应用概述](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)。
