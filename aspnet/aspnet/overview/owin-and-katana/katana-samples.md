---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 示例 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472346"
---
# <a name="katana-samples"></a>Katana 示例

由[Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 示例

 | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)的**ASP.NET 路由示例**  
在某些应用程序中，需要将 Asp.Net 路由表中的 OWIN 组件与非 OWIN 组件挂钩。 此示例演示如何使用 RouteCollection 扩展方法 MapOwinPath 和 MapOwinRoute 提供的。

 | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)的**分支管道示例**  
OWIN 请求处理管道不需要是线性的，它们可以以不同的方式进行分支以处理请求。 此示例演示如何根据请求路径或其他请求数据（如标头）构造分支管道。 这些组件在 Owin nuget 包中提供。

**自定义服务器示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
演示如何在自承载 OWIN 时使用自定义 OWIN 服务器。

 | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)的**嵌入式示例**  
某些 OWIN 服务器可以在自己的进程中运行（&quot;自承载&quot;）。 此示例演示如何使用 Owin nuget 包提供的工具启动 OWIN 应用程序。

**HelloWorld 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN 是一种 HTTP 服务器 API 抽象，可跨不同服务器实现应用程序的可移植性。 此示例演示如何使用 OWIN 抽象抽象方法的一些**简单包装**编写一个 Hello World 应用程序，并在 ASP.NET 之类的 web 服务器上运行该应用程序。

**Hello World 原始 OWIN 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
此示例演示如何使用**原始**OWIN 抽象编写一个 Hello World 应用程序，并在类似于 Asp.Net 的 web 服务器上运行该应用程序。

**SignalR 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
演示如何使用 OWIN/Katana 自行托管 SignalR。 有关自承载 SignalR 的详细信息，请参阅[教程： SignalR 自承载](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

 | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)的**静态文件示例**   
演示如何使用 OWIN/Katana 为静态文件支持 HTTP 请求。

**WEB API** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
此示例演示如何在 IIS 中承载 OWIN，以及如何将 Web API 添加到 OWIN 管道。

 | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)  的**Web 套接字示例**  
演示如何使用 OWIN 类在中支持 Web 套[接字。](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)
