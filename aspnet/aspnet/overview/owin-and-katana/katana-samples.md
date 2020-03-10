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
# <a name="katana-samples"></a><span data-ttu-id="9020e-102">Katana 示例</span><span class="sxs-lookup"><span data-stu-id="9020e-102">Katana Samples</span></span>

<span data-ttu-id="9020e-103">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9020e-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="9020e-104">Katana 示例</span><span class="sxs-lookup"><span data-stu-id="9020e-104">Katana Samples</span></span>

<span data-ttu-id="9020e-105"> | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)的**ASP.NET 路由示例**</span><span class="sxs-lookup"><span data-stu-id="9020e-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="9020e-106">在某些应用程序中，需要将 Asp.Net 路由表中的 OWIN 组件与非 OWIN 组件挂钩。</span><span class="sxs-lookup"><span data-stu-id="9020e-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="9020e-107">此示例演示如何使用 RouteCollection 扩展方法 MapOwinPath 和 MapOwinRoute 提供的。</span><span class="sxs-lookup"><span data-stu-id="9020e-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="9020e-108"> | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)的**分支管道示例**</span><span class="sxs-lookup"><span data-stu-id="9020e-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="9020e-109">OWIN 请求处理管道不需要是线性的，它们可以以不同的方式进行分支以处理请求。</span><span class="sxs-lookup"><span data-stu-id="9020e-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="9020e-110">此示例演示如何根据请求路径或其他请求数据（如标头）构造分支管道。</span><span class="sxs-lookup"><span data-stu-id="9020e-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="9020e-111">这些组件在 Owin nuget 包中提供。</span><span class="sxs-lookup"><span data-stu-id="9020e-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="9020e-112">**自定义服务器示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="9020e-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="9020e-113">演示如何在自承载 OWIN 时使用自定义 OWIN 服务器。</span><span class="sxs-lookup"><span data-stu-id="9020e-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="9020e-114"> | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)的**嵌入式示例**</span><span class="sxs-lookup"><span data-stu-id="9020e-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="9020e-115">某些 OWIN 服务器可以在自己的进程中运行（&quot;自承载&quot;）。</span><span class="sxs-lookup"><span data-stu-id="9020e-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="9020e-116">此示例演示如何使用 Owin nuget 包提供的工具启动 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9020e-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="9020e-117">**HelloWorld 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="9020e-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="9020e-118">OWIN 是一种 HTTP 服务器 API 抽象，可跨不同服务器实现应用程序的可移植性。</span><span class="sxs-lookup"><span data-stu-id="9020e-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="9020e-119">此示例演示如何使用 OWIN 抽象抽象方法的一些**简单包装**编写一个 Hello World 应用程序，并在 ASP.NET 之类的 web 服务器上运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="9020e-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="9020e-120">**Hello World 原始 OWIN 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="9020e-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="9020e-121">此示例演示如何使用**原始**OWIN 抽象编写一个 Hello World 应用程序，并在类似于 Asp.Net 的 web 服务器上运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="9020e-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="9020e-122">**SignalR 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="9020e-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="9020e-123">演示如何使用 OWIN/Katana 自行托管 SignalR。</span><span class="sxs-lookup"><span data-stu-id="9020e-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="9020e-124">有关自承载 SignalR 的详细信息，请参阅[教程： SignalR 自承载](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="9020e-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="9020e-125"> | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)的**静态文件示例** </span><span class="sxs-lookup"><span data-stu-id="9020e-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="9020e-126">演示如何使用 OWIN/Katana 为静态文件支持 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="9020e-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="9020e-127">**WEB API** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="9020e-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="9020e-128">此示例演示如何在 IIS 中承载 OWIN，以及如何将 Web API 添加到 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="9020e-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="9020e-129"> | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)  的**Web 套接字示例**</span><span class="sxs-lookup"><span data-stu-id="9020e-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="9020e-130">演示如何使用 OWIN 类在中支持 Web 套[接字。](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="9020e-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
