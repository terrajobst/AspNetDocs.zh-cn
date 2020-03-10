---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SignalR 扩展 SQL Server |Microsoft Docs
author: bradygaster
description: 本主题中使用的软件版本 Visual Studio 2013 .NET 4.5 SignalR 版本2本主题的早期版本。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467738"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="a0d49-103">使用 SQL Server 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="a0d49-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="a0d49-104">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a0d49-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="a0d49-105">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a0d49-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="a0d49-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a0d49-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="a0d49-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="a0d49-107">.NET 4.5</span></span>
> - <span data-ttu-id="a0d49-108">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="a0d49-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="a0d49-109">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="a0d49-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="a0d49-110">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d49-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="a0d49-111">问题和注释</span><span class="sxs-lookup"><span data-stu-id="a0d49-111">Questions and comments</span></span>
>
> <span data-ttu-id="a0d49-112">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="a0d49-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a0d49-113">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="a0d49-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="a0d49-114">在本教程中，你将使用 SQL Server 在部署在两个不同 IIS 实例中的 SignalR 应用程序之间分配消息。</span><span class="sxs-lookup"><span data-stu-id="a0d49-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="a0d49-115">您还可以在一台测试计算机上运行本教程，但若要获得完整的效果，您需要将 SignalR 应用程序部署到两个或更多服务器。</span><span class="sxs-lookup"><span data-stu-id="a0d49-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="a0d49-116">还必须在一台服务器或单独的专用服务器上安装 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a0d49-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="a0d49-117">另一种方法是使用 Azure 上的 Vm 运行教程。</span><span class="sxs-lookup"><span data-stu-id="a0d49-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="a0d49-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="a0d49-118">Prerequisites</span></span>

<span data-ttu-id="a0d49-119">Microsoft SQL Server 2005 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="a0d49-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="a0d49-120">底板支持 SQL Server 的桌面版本和服务器版本。</span><span class="sxs-lookup"><span data-stu-id="a0d49-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="a0d49-121">它不支持 SQL Server Compact Edition 或 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="a0d49-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="a0d49-122">（如果你的应用程序托管在 Azure 上，请考虑改用服务总线底板。）</span><span class="sxs-lookup"><span data-stu-id="a0d49-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="a0d49-123">概述</span><span class="sxs-lookup"><span data-stu-id="a0d49-123">Overview</span></span>

<span data-ttu-id="a0d49-124">在学习详细教程之前，下面简要概述了你将执行的操作。</span><span class="sxs-lookup"><span data-stu-id="a0d49-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="a0d49-125">创建新的空数据库。</span><span class="sxs-lookup"><span data-stu-id="a0d49-125">Create a new empty database.</span></span> <span data-ttu-id="a0d49-126">该底板将在此数据库中创建所需的表。</span><span class="sxs-lookup"><span data-stu-id="a0d49-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="a0d49-127">将以下 NuGet 包添加到应用程序：</span><span class="sxs-lookup"><span data-stu-id="a0d49-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="a0d49-128">SignalR</span><span class="sxs-lookup"><span data-stu-id="a0d49-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="a0d49-129">SignalR。</span><span class="sxs-lookup"><span data-stu-id="a0d49-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="a0d49-130">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0d49-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="a0d49-131">将以下代码添加到 Startup.cs 以配置底板：</span><span class="sxs-lookup"><span data-stu-id="a0d49-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="a0d49-132">此代码会将底板配置为[TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)的默认值。</span><span class="sxs-lookup"><span data-stu-id="a0d49-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="a0d49-133">有关更改这些值的信息，请参阅[SignalR Performance：扩展度量](signalr-performance.md#scaleout_metrics)值。</span><span class="sxs-lookup"><span data-stu-id="a0d49-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="a0d49-134">配置数据库</span><span class="sxs-lookup"><span data-stu-id="a0d49-134">Configure the Database</span></span>

<span data-ttu-id="a0d49-135">确定应用程序是否将使用 Windows 身份验证或 SQL Server 身份验证来访问数据库。</span><span class="sxs-lookup"><span data-stu-id="a0d49-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="a0d49-136">无论如何，请确保数据库用户具有登录、创建架构和创建表的权限。</span><span class="sxs-lookup"><span data-stu-id="a0d49-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="a0d49-137">为要使用的底板创建新数据库。</span><span class="sxs-lookup"><span data-stu-id="a0d49-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="a0d49-138">您可以为数据库指定任意名称。</span><span class="sxs-lookup"><span data-stu-id="a0d49-138">You can give the database any name.</span></span> <span data-ttu-id="a0d49-139">不需要在数据库中创建任何表;底板将创建所需的表。</span><span class="sxs-lookup"><span data-stu-id="a0d49-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="a0d49-140">启用 Service Broker</span><span class="sxs-lookup"><span data-stu-id="a0d49-140">Enable Service Broker</span></span>

<span data-ttu-id="a0d49-141">建议为底板数据库启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="a0d49-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="a0d49-142">Service Broker 为 SQL Server 中的消息和队列提供本机支持，从而使底板更有效地接收更新。</span><span class="sxs-lookup"><span data-stu-id="a0d49-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="a0d49-143">（但是，底板也无需 Service Broker 即可工作。）</span><span class="sxs-lookup"><span data-stu-id="a0d49-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="a0d49-144">若要检查是否启用了 Service Broker，请在**sys.databases**目录视图中查询**是否\_Broker\_enabled**列。</span><span class="sxs-lookup"><span data-stu-id="a0d49-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="a0d49-145">若要启用 Service Broker，请使用以下 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="a0d49-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="a0d49-146">如果此查询显示为死锁，请确保没有任何应用程序连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="a0d49-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="a0d49-147">如果已启用跟踪，则跟踪还将显示是否启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="a0d49-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="a0d49-148">创建 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="a0d49-148">Create a SignalR Application</span></span>

<span data-ttu-id="a0d49-149">通过以下任一教程创建 SignalR 应用程序：</span><span class="sxs-lookup"><span data-stu-id="a0d49-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="a0d49-150">入门 SignalR 2。0</span><span class="sxs-lookup"><span data-stu-id="a0d49-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="a0d49-151">入门 SignalR 2.0 和 MVC 5</span><span class="sxs-lookup"><span data-stu-id="a0d49-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="a0d49-152">接下来，我们将修改聊天应用程序，以支持 SQL Server 的扩展。</span><span class="sxs-lookup"><span data-stu-id="a0d49-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="a0d49-153">首先，将 SignalR NuGet 包添加到项目。</span><span class="sxs-lookup"><span data-stu-id="a0d49-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="a0d49-154">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="a0d49-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a0d49-155">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a0d49-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="a0d49-156">接下来，打开 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="a0d49-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="a0d49-157">将以下代码添加到**Configure**方法：</span><span class="sxs-lookup"><span data-stu-id="a0d49-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="a0d49-158">部署并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="a0d49-158">Deploy and Run the Application</span></span>

<span data-ttu-id="a0d49-159">准备 Windows Server 实例以部署 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0d49-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="a0d49-160">添加 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="a0d49-160">Add the IIS role.</span></span> <span data-ttu-id="a0d49-161">包括 "应用程序开发" 功能，包括 WebSocket 协议。</span><span class="sxs-lookup"><span data-stu-id="a0d49-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="a0d49-162">还包括管理服务（在 "管理工具" 下列出）。</span><span class="sxs-lookup"><span data-stu-id="a0d49-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="a0d49-163">**安装 3.0 Web 部署。**</span><span class="sxs-lookup"><span data-stu-id="a0d49-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="a0d49-164">当你运行 IIS 管理器时，它将提示你安装 Microsoft Web 平台，或者你可以[下载该安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="a0d49-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="a0d49-165">在平台安装程序中，搜索 Web 部署并安装 Web 部署3。0</span><span class="sxs-lookup"><span data-stu-id="a0d49-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="a0d49-166">检查 Web 管理服务是否正在运行。</span><span class="sxs-lookup"><span data-stu-id="a0d49-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="a0d49-167">如果不是，则启动该服务。</span><span class="sxs-lookup"><span data-stu-id="a0d49-167">If not, start the service.</span></span> <span data-ttu-id="a0d49-168">（如果在 Windows 服务列表中看不到 Web 管理服务，请确保在添加 IIS 角色时已安装管理服务。）</span><span class="sxs-lookup"><span data-stu-id="a0d49-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="a0d49-169">最后，为 TCP 打开端口8172。</span><span class="sxs-lookup"><span data-stu-id="a0d49-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="a0d49-170">这是 Web 部署工具使用的端口。</span><span class="sxs-lookup"><span data-stu-id="a0d49-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="a0d49-171">现在，你已准备好将 Visual Studio 项目从开发计算机部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="a0d49-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="a0d49-172">在解决方案资源管理器中，右键单击该解决方案，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="a0d49-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="a0d49-173">有关 web 部署的详细文档，请参阅[Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d49-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="a0d49-174">如果将应用程序部署到两个服务器，则可以在单独的浏览器窗口中打开每个实例，并查看每个实例是否分别接收 SignalR 消息。</span><span class="sxs-lookup"><span data-stu-id="a0d49-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="a0d49-175">（当然，在生产环境中，这两个服务器会位于负载均衡器的后面。）</span><span class="sxs-lookup"><span data-stu-id="a0d49-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="a0d49-176">运行应用程序后，可以看到 SignalR 已在数据库中自动创建了表：</span><span class="sxs-lookup"><span data-stu-id="a0d49-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="a0d49-177">SignalR 管理表。</span><span class="sxs-lookup"><span data-stu-id="a0d49-177">SignalR manages the tables.</span></span> <span data-ttu-id="a0d49-178">只要部署了应用程序，请不要删除行、修改表等。</span><span class="sxs-lookup"><span data-stu-id="a0d49-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
