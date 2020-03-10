---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN ASP.NET Web API-ASP.NET 4。x
author: rick-anderson
description: 介绍如何在控制台应用程序中承载 ASP.NET Web API 的代码教程。
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448328"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>使用 OWIN 自承载 ASP.NET Web API 

> 本教程介绍如何使用 OWIN 在控制台应用程序中 ASP.NET Web API 承载 Web API 框架。
>
> [开放式 Web Interface for .net](http://owin.org) （OWIN）定义 .net web 服务器和 Web 应用程序之间的抽象。 OWIN 将 web 应用程序与服务器分离，这使得 OWIN 非常适合用于在你自己的进程（IIS 以外）中自承载 web 应用程序。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Web API 5.2。7

> [!NOTE]
> 可以在[github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)中找到本教程的完整源代码。

## <a name="create-a-console-application"></a>创建控制台应用程序

在 "**文件**" 菜单**上，选择**"**项目**"。 从**安装**的 "**视觉C#对象**" 下，选择 " **Windows 桌面**"，然后选择 "**控制台应用（.net Framework）** "。 将项目命名为 "OwinSelfhostSample"，然后选择 **"确定**"。

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>添加 Web API 和 OWIN 包

从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

这会安装 WebAPI OWIN selfhost 包和所有必需的 OWIN 包。

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>为自承载配置 Web API

在解决方案资源管理器中，右键单击项目并选择 "**添加** / **类**" 添加新类。 将此类命名为 `Startup`。

![](use-owin-to-self-host-web-api/_static/image5.png)

将此文件中的所有样本代码替换为以下代码：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>添加 Web API 控制器

接下来，添加 Web API 控制器类。 在解决方案资源管理器中，右键单击项目并选择 "**添加** / **类**" 添加新类。 将此类命名为 `ValuesController`。

将此文件中的所有样本代码替换为以下代码：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>启动 OWIN 主机，并使用 HttpClient 发出请求

将 Program.cs 文件中的所有样本代码替换为以下代码：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>运行此应用程序

若要运行应用程序，请在 Visual Studio 中按 F5。 输出应如下所示：

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>其他资源

[项目 Katana 概述](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure 辅助角色中的主机 ASP.NET Web API](host-aspnet-web-api-in-an-azure-worker-role.md)
