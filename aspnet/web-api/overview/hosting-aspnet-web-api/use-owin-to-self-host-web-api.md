---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自托管 ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: 本教程演示如何在一个控制台应用程序中托管 ASP.NET Web API 的代码。
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: a67db0bd061846af2db3599e0843ed7c6a22db1e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59386510"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="7d8a3-103">使用 OWIN 自托管 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="7d8a3-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 


> <span data-ttu-id="7d8a3-104">本教程演示如何使用 OWIN 自托管 Web API 框架的控制台应用程序中托管 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="7d8a3-105">[用于.NET 开放 Web 接口](http://owin.org)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="7d8a3-106">OWIN 将从服务器中，这使 OWIN 适合于自承载在 IIS 外部自己进程中的 web 应用程序的 web 应用程序中分离出来。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7d8a3-107">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="7d8a3-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="7d8a3-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7d8a3-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="7d8a3-109">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="7d8a3-109">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="7d8a3-110">您可以在本教程中找到完整的源代码[github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="7d8a3-111">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="7d8a3-111">Create a console application</span></span>

<span data-ttu-id="7d8a3-112">上**文件**菜单中，**新建**，然后选择**项目**。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="7d8a3-113">从**已安装**下**Visual C#** ，选择**Windows Desktop** ，然后选择**控制台应用 (.Net Framework)**。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="7d8a3-114">将项目命名为"OwinSelfhostSample"，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="7d8a3-115">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="7d8a3-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="7d8a3-116">从**工具**菜单中，选择**NuGet 包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7d8a3-117">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7d8a3-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="7d8a3-118">这将安装 WebAPI OWIN selfhost 包和所有所需的 OWIN 包。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="7d8a3-119">配置 Web API 的自托管</span><span class="sxs-lookup"><span data-stu-id="7d8a3-119">Configure Web API for self-host</span></span>

<span data-ttu-id="7d8a3-120">在解决方案资源管理器，右键单击该项目并选择**外** / **类**以添加一个新类。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="7d8a3-121">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="7d8a3-122">使用以下内容替换所有样板代码，此文件中：</span><span class="sxs-lookup"><span data-stu-id="7d8a3-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="7d8a3-123">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="7d8a3-123">Add a Web API controller</span></span>

<span data-ttu-id="7d8a3-124">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="7d8a3-125">在解决方案资源管理器，右键单击该项目并选择**外** / **类**以添加一个新类。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="7d8a3-126">将此类命名为 `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="7d8a3-127">使用以下内容替换所有样板代码，此文件中：</span><span class="sxs-lookup"><span data-stu-id="7d8a3-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="7d8a3-128">启动 OWIN 主机并使 HttpClient 的请求</span><span class="sxs-lookup"><span data-stu-id="7d8a3-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="7d8a3-129">使用以下内容替换所有 Program.cs 文件中的样板代码：</span><span class="sxs-lookup"><span data-stu-id="7d8a3-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="7d8a3-130">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="7d8a3-130">Run the application</span></span>

<span data-ttu-id="7d8a3-131">若要运行该应用程序，请在 Visual Studio 中按 F5。</span><span class="sxs-lookup"><span data-stu-id="7d8a3-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="7d8a3-132">输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="7d8a3-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="7d8a3-133">其他资源</span><span class="sxs-lookup"><span data-stu-id="7d8a3-133">Additional resources</span></span>

[<span data-ttu-id="7d8a3-134">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="7d8a3-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="7d8a3-135">承载在 Azure 辅助角色中的 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="7d8a3-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
