---
uid: signalr/overview/older-versions/scaleout-with-redis
title: SignalR 扩展 with Redis （SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431204"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="1d731-102">使用 Redis 的 SignalR 横向扩展 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="1d731-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="1d731-103">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="1d731-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="1d731-104">在本教程中，你将使用[Redis](http://redis.io/)在部署在两个不同 IIS 实例上的 SignalR 应用程序中分发消息。</span><span class="sxs-lookup"><span data-stu-id="1d731-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="1d731-105">Redis 是内存中的键-值存储。</span><span class="sxs-lookup"><span data-stu-id="1d731-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="1d731-106">它还支持发布/订阅模型的消息传送系统。</span><span class="sxs-lookup"><span data-stu-id="1d731-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="1d731-107">SignalR Redis 底板使用发布/订阅功能将消息转发到其他服务器。</span><span class="sxs-lookup"><span data-stu-id="1d731-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="1d731-108">对于本教程，你将使用三个服务器：</span><span class="sxs-lookup"><span data-stu-id="1d731-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="1d731-109">运行 Windows 的两台服务器，你将使用它来部署 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d731-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="1d731-110">一台运行 Linux 的服务器，你将使用它来运行 Redis。</span><span class="sxs-lookup"><span data-stu-id="1d731-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="1d731-111">对于本教程中的屏幕截图，我使用的是 Ubuntu 12.04 TLS。</span><span class="sxs-lookup"><span data-stu-id="1d731-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="1d731-112">如果没有要使用的三个物理服务器，则可以在 Hyper-v 上创建 Vm。</span><span class="sxs-lookup"><span data-stu-id="1d731-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="1d731-113">另一种方法是在 Azure 上创建 Vm。</span><span class="sxs-lookup"><span data-stu-id="1d731-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="1d731-114">尽管本教程使用的是官方 Redis 实现，但也有来自 MSOpenTech 的[Redis 的 Windows 端口](https://github.com/MSOpenTech/redis)。</span><span class="sxs-lookup"><span data-stu-id="1d731-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="1d731-115">安装和配置不同，但步骤是相同的。</span><span class="sxs-lookup"><span data-stu-id="1d731-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1d731-116">带 Redis 的 SignalR 扩展不支持 Redis 群集。</span><span class="sxs-lookup"><span data-stu-id="1d731-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="1d731-117">概述</span><span class="sxs-lookup"><span data-stu-id="1d731-117">Overview</span></span>

<span data-ttu-id="1d731-118">在学习详细教程之前，下面简要概述了你将执行的操作。</span><span class="sxs-lookup"><span data-stu-id="1d731-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="1d731-119">安装 Redis 并启动 Redis 服务器。</span><span class="sxs-lookup"><span data-stu-id="1d731-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="1d731-120">将以下 NuGet 包添加到应用程序：</span><span class="sxs-lookup"><span data-stu-id="1d731-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="1d731-121">SignalR</span><span class="sxs-lookup"><span data-stu-id="1d731-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="1d731-122">SignalR. Redis</span><span class="sxs-lookup"><span data-stu-id="1d731-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="1d731-123">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d731-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="1d731-124">将以下代码添加到 global.asax 以配置底板：</span><span class="sxs-lookup"><span data-stu-id="1d731-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="1d731-125">Hyper-v 上的 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1d731-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="1d731-126">使用 Windows Hyper-v，你可以轻松地在 Windows Server 上创建 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="1d731-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="1d731-127">从[http://www.ubuntu.com](http://www.ubuntu.com/)下载 Ubuntu ISO。</span><span class="sxs-lookup"><span data-stu-id="1d731-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="1d731-128">在 Hyper-v 中，添加新的 VM。</span><span class="sxs-lookup"><span data-stu-id="1d731-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="1d731-129">在 "**连接虚拟硬盘**" 步骤中，选择 "**创建虚拟硬盘**"。</span><span class="sxs-lookup"><span data-stu-id="1d731-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="1d731-130">在 "**安装选项**" 步骤中，选择 "**映像文件（.iso）** "，单击 "**浏览**"，然后浏览到 Ubuntu 安装 iso。</span><span class="sxs-lookup"><span data-stu-id="1d731-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="1d731-131">安装 Redis</span><span class="sxs-lookup"><span data-stu-id="1d731-131">Install Redis</span></span>

<span data-ttu-id="1d731-132">按照[http://redis.io/download](http://redis.io/download)上的步骤下载并生成 Redis。</span><span class="sxs-lookup"><span data-stu-id="1d731-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="1d731-133">这会在 `src` 目录中生成 Redis 二进制文件。</span><span class="sxs-lookup"><span data-stu-id="1d731-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="1d731-134">默认情况下，Redis 不需要密码。</span><span class="sxs-lookup"><span data-stu-id="1d731-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="1d731-135">若要设置密码，请编辑位于源代码的根目录中的 `redis.conf` 文件。</span><span class="sxs-lookup"><span data-stu-id="1d731-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="1d731-136">（请在编辑之前创建文件的备份副本）将以下指令添加到 `redis.conf`：</span><span class="sxs-lookup"><span data-stu-id="1d731-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="1d731-137">现在启动 Redis 服务器：</span><span class="sxs-lookup"><span data-stu-id="1d731-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="1d731-138">打开端口6379，这是 Redis 侦听的默认端口。</span><span class="sxs-lookup"><span data-stu-id="1d731-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="1d731-139">（可以在配置文件中更改端口号。）</span><span class="sxs-lookup"><span data-stu-id="1d731-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="1d731-140">创建 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="1d731-140">Create the SignalR Application</span></span>

<span data-ttu-id="1d731-141">通过以下任一教程创建 SignalR 应用程序：</span><span class="sxs-lookup"><span data-stu-id="1d731-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="1d731-142">入门与 SignalR</span><span class="sxs-lookup"><span data-stu-id="1d731-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="1d731-143">入门 SignalR 和 MVC 4</span><span class="sxs-lookup"><span data-stu-id="1d731-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="1d731-144">接下来，我们将修改聊天应用程序，以支持 Redis 的扩展。</span><span class="sxs-lookup"><span data-stu-id="1d731-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="1d731-145">首先，将 SignalR NuGet 包添加到项目。</span><span class="sxs-lookup"><span data-stu-id="1d731-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="1d731-146">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="1d731-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="1d731-147">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="1d731-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="1d731-148">接下来，打开 global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="1d731-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="1d731-149">将以下代码添加到**应用程序\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="1d731-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="1d731-150">"服务器" 是运行 Redis 的服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="1d731-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="1d731-151">*端口*号</span><span class="sxs-lookup"><span data-stu-id="1d731-151">*port* is the port number</span></span>
- <span data-ttu-id="1d731-152">"密码" 是在 redis 文件中定义的密码。</span><span class="sxs-lookup"><span data-stu-id="1d731-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="1d731-153">"AppName" 是任意字符串。</span><span class="sxs-lookup"><span data-stu-id="1d731-153">"AppName" is any string.</span></span> <span data-ttu-id="1d731-154">SignalR 创建具有此名称的 Redis pub/sub 通道。</span><span class="sxs-lookup"><span data-stu-id="1d731-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="1d731-155">例如:</span><span class="sxs-lookup"><span data-stu-id="1d731-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="1d731-156">部署并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1d731-156">Deploy and Run the Application</span></span>

<span data-ttu-id="1d731-157">准备 Windows Server 实例以部署 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d731-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="1d731-158">添加 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="1d731-158">Add the IIS role.</span></span> <span data-ttu-id="1d731-159">包括 "应用程序开发" 功能，包括 WebSocket 协议。</span><span class="sxs-lookup"><span data-stu-id="1d731-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="1d731-160">还包括管理服务（在 "管理工具" 下列出）。</span><span class="sxs-lookup"><span data-stu-id="1d731-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="1d731-161">**安装 3.0 Web 部署。**</span><span class="sxs-lookup"><span data-stu-id="1d731-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="1d731-162">当你运行 IIS 管理器时，它将提示你安装 Microsoft Web 平台，或者你可以[下载该安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="1d731-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="1d731-163">在平台安装程序中，搜索 Web 部署并安装 Web 部署3。0</span><span class="sxs-lookup"><span data-stu-id="1d731-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="1d731-164">检查 Web 管理服务是否正在运行。</span><span class="sxs-lookup"><span data-stu-id="1d731-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="1d731-165">如果不是，则启动该服务。</span><span class="sxs-lookup"><span data-stu-id="1d731-165">If not, start the service.</span></span> <span data-ttu-id="1d731-166">（如果在 Windows 服务列表中看不到 Web 管理服务，请确保在添加 IIS 角色时已安装管理服务。）</span><span class="sxs-lookup"><span data-stu-id="1d731-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="1d731-167">默认情况下，Web 管理服务在 TCP 端口8172上进行侦听。</span><span class="sxs-lookup"><span data-stu-id="1d731-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="1d731-168">在 Windows 防火墙中创建新的入站规则，以允许端口8172上的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="1d731-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="1d731-169">有关详细信息，请参阅[配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1d731-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="1d731-170">（如果在 Azure 上托管 Vm，则可以直接在 Azure 门户中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="1d731-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="1d731-171">请参阅[如何设置虚拟机的终结点](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。）</span><span class="sxs-lookup"><span data-stu-id="1d731-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="1d731-172">现在，你已准备好将 Visual Studio 项目从开发计算机部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="1d731-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="1d731-173">在解决方案资源管理器中，右键单击该解决方案，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="1d731-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="1d731-174">有关 web 部署的详细文档，请参阅[Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="1d731-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="1d731-175">如果将应用程序部署到两个服务器，则可以在单独的浏览器窗口中打开每个实例，并查看每个实例是否分别接收 SignalR 消息。</span><span class="sxs-lookup"><span data-stu-id="1d731-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="1d731-176">（当然，在生产环境中，这两个服务器会位于负载均衡器的后面。）</span><span class="sxs-lookup"><span data-stu-id="1d731-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="1d731-177">如果你想要查看发送到 Redis 的消息，可以使用**Redis-cli**客户端，该客户端安装有 Redis。</span><span class="sxs-lookup"><span data-stu-id="1d731-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
