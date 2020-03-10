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
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="30db1-103">使用 OWIN 自承载 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="30db1-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 

> <span data-ttu-id="30db1-104">本教程介绍如何使用 OWIN 在控制台应用程序中 ASP.NET Web API 承载 Web API 框架。</span><span class="sxs-lookup"><span data-stu-id="30db1-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="30db1-105">[开放式 Web Interface for .net](http://owin.org) （OWIN）定义 .net web 服务器和 Web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="30db1-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="30db1-106">OWIN 将 web 应用程序与服务器分离，这使得 OWIN 非常适合用于在你自己的进程（IIS 以外）中自承载 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="30db1-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="30db1-107">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="30db1-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="30db1-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="30db1-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="30db1-109">Web API 5.2。7</span><span class="sxs-lookup"><span data-stu-id="30db1-109">Web API 5.2.7</span></span>

> [!NOTE]
> <span data-ttu-id="30db1-110">可以在[github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)中找到本教程的完整源代码。</span><span class="sxs-lookup"><span data-stu-id="30db1-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="30db1-111">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="30db1-111">Create a console application</span></span>

<span data-ttu-id="30db1-112">在 "**文件**" 菜单**上，选择**"**项目**"。</span><span class="sxs-lookup"><span data-stu-id="30db1-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="30db1-113">从**安装**的 "**视觉C#对象**" 下，选择 " **Windows 桌面**"，然后选择 "**控制台应用（.net Framework）** "。</span><span class="sxs-lookup"><span data-stu-id="30db1-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="30db1-114">将项目命名为 "OwinSelfhostSample"，然后选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="30db1-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="30db1-115">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="30db1-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="30db1-116">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="30db1-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="30db1-117">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="30db1-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="30db1-118">这会安装 WebAPI OWIN selfhost 包和所有必需的 OWIN 包。</span><span class="sxs-lookup"><span data-stu-id="30db1-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="30db1-119">为自承载配置 Web API</span><span class="sxs-lookup"><span data-stu-id="30db1-119">Configure Web API for self-host</span></span>

<span data-ttu-id="30db1-120">在解决方案资源管理器中，右键单击项目并选择 "**添加** / **类**" 添加新类。</span><span class="sxs-lookup"><span data-stu-id="30db1-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="30db1-121">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="30db1-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="30db1-122">将此文件中的所有样本代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="30db1-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="30db1-123">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="30db1-123">Add a Web API controller</span></span>

<span data-ttu-id="30db1-124">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="30db1-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="30db1-125">在解决方案资源管理器中，右键单击项目并选择 "**添加** / **类**" 添加新类。</span><span class="sxs-lookup"><span data-stu-id="30db1-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="30db1-126">将此类命名为 `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="30db1-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="30db1-127">将此文件中的所有样本代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="30db1-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="30db1-128">启动 OWIN 主机，并使用 HttpClient 发出请求</span><span class="sxs-lookup"><span data-stu-id="30db1-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="30db1-129">将 Program.cs 文件中的所有样本代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="30db1-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="30db1-130">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="30db1-130">Run the application</span></span>

<span data-ttu-id="30db1-131">若要运行应用程序，请在 Visual Studio 中按 F5。</span><span class="sxs-lookup"><span data-stu-id="30db1-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="30db1-132">输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="30db1-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="30db1-133">其他资源</span><span class="sxs-lookup"><span data-stu-id="30db1-133">Additional resources</span></span>

[<span data-ttu-id="30db1-134">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="30db1-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="30db1-135">Azure 辅助角色中的主机 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="30db1-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
