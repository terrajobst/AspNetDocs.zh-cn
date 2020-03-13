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
# <a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="a4579-103">使用 Azure 服务总线的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="a4579-103">SignalR Scaleout with Azure Service Bus</span></span>

<span data-ttu-id="a4579-104">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a4579-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="a4579-105">在本教程中，将 SignalR 应用程序部署到 Microsoft Azure Web 角色，使用服务总线底板将消息分发给每个角色实例。</span><span class="sxs-lookup"><span data-stu-id="a4579-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="a4579-106">（也可以[在 Azure App Service 中](https://docs.microsoft.com/azure/app-service-web/)将服务总线底板用于 web 应用。）</span><span class="sxs-lookup"><span data-stu-id="a4579-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="a4579-107">先决条件：</span><span class="sxs-lookup"><span data-stu-id="a4579-107">Prerequisites:</span></span>

- <span data-ttu-id="a4579-108">一个 Microsoft Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="a4579-108">A Windows Azure account.</span></span>
- <span data-ttu-id="a4579-109">[Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="a4579-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="a4579-110">Visual Studio 2012 或 2013。</span><span class="sxs-lookup"><span data-stu-id="a4579-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="a4579-111">Service bus 底板还与[适用于 Windows Server 的服务总线](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)版本1.1 兼容。</span><span class="sxs-lookup"><span data-stu-id="a4579-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="a4579-112">但是，它与适用于 Windows Server 的服务总线1.0 版不兼容。</span><span class="sxs-lookup"><span data-stu-id="a4579-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="a4579-113">定价</span><span class="sxs-lookup"><span data-stu-id="a4579-113">Pricing</span></span>

<span data-ttu-id="a4579-114">Service Bus 底板使用主题发送消息。</span><span class="sxs-lookup"><span data-stu-id="a4579-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="a4579-115">有关最新定价信息，请参阅[服务总线](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="a4579-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="a4579-116">撰写本文时，可以每月发送1000000条消息，小于 $1。</span><span class="sxs-lookup"><span data-stu-id="a4579-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="a4579-117">该底板为 SignalR 集线器方法的每个调用发送服务总线消息。</span><span class="sxs-lookup"><span data-stu-id="a4579-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="a4579-118">还有一些用于连接、断开连接、加入或离开组等的控制消息。</span><span class="sxs-lookup"><span data-stu-id="a4579-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="a4579-119">在大多数应用程序中，大多数消息流量均为集线器方法调用。</span><span class="sxs-lookup"><span data-stu-id="a4579-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="a4579-120">概述</span><span class="sxs-lookup"><span data-stu-id="a4579-120">Overview</span></span>

<span data-ttu-id="a4579-121">在学习详细教程之前，下面简要概述了你将执行的操作。</span><span class="sxs-lookup"><span data-stu-id="a4579-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="a4579-122">使用 Windows Azure 门户创建新的 Service Bus 命名空间。</span><span class="sxs-lookup"><span data-stu-id="a4579-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="a4579-123">将以下 NuGet 包添加到应用程序：</span><span class="sxs-lookup"><span data-stu-id="a4579-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="a4579-124">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="a4579-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="a4579-125">[SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)或 SignalR. [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="a4579-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="a4579-126">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4579-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="a4579-127">将以下代码添加到 Startup.cs 以配置底板：</span><span class="sxs-lookup"><span data-stu-id="a4579-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="a4579-128">此代码会将底板配置为[TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)的默认值。</span><span class="sxs-lookup"><span data-stu-id="a4579-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="a4579-129">有关更改这些值的信息，请参阅 [SignalR 性能：扩展指标](signalr-performance.md#scaleout_metrics)。</span><span class="sxs-lookup"><span data-stu-id="a4579-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="a4579-130">对于每个应用程序，请为 "YourAppName" 选择不同的值。</span><span class="sxs-lookup"><span data-stu-id="a4579-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="a4579-131">不要跨多个应用程序使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="a4579-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="a4579-132">创建 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="a4579-132">Create the Azure Services</span></span>

<span data-ttu-id="a4579-133">按照[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中的说明创建云服务。</span><span class="sxs-lookup"><span data-stu-id="a4579-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="a4579-134">按照 "如何：使用 "快速创建" 创建云服务。</span><span class="sxs-lookup"><span data-stu-id="a4579-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="a4579-135">对于本教程，无需上载证书。</span><span class="sxs-lookup"><span data-stu-id="a4579-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="a4579-136">按照[如何使用服务总线主题/订阅](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)中的说明创建新的服务总线命名空间。</span><span class="sxs-lookup"><span data-stu-id="a4579-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="a4579-137">按照 "创建服务命名空间" 一节中的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="a4579-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="a4579-138">请确保为云服务和服务总线命名空间选择相同的区域。</span><span class="sxs-lookup"><span data-stu-id="a4579-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="a4579-139">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="a4579-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="a4579-140">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a4579-140">Start Visual Studio.</span></span> <span data-ttu-id="a4579-141">在“文件”菜单上，单击“新建项目”</span><span class="sxs-lookup"><span data-stu-id="a4579-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="a4579-142">在 "**新建项目**" 对话框中，展开 "**视觉对象C#** "。</span><span class="sxs-lookup"><span data-stu-id="a4579-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="a4579-143">在 "**已安装模板**" 下，选择 "**云**"，然后选择 " **microsoft Azure 云服务**"。</span><span class="sxs-lookup"><span data-stu-id="a4579-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="a4579-144">保持默认值 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="a4579-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="a4579-145">将应用程序命名为 ChatService，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="a4579-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="a4579-146">在 "**新建 Microsoft Azure 云服务**" 对话框中，选择 "ASP.NET Web 角色"。</span><span class="sxs-lookup"><span data-stu-id="a4579-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="a4579-147">单击右箭头按钮（ **&gt;** ）可将该角色添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="a4579-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="a4579-148">将鼠标悬停在新角色上，使铅笔图标可见。</span><span class="sxs-lookup"><span data-stu-id="a4579-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="a4579-149">单击此图标可重命名角色。</span><span class="sxs-lookup"><span data-stu-id="a4579-149">Click this icon to rename the role.</span></span> <span data-ttu-id="a4579-150">将角色命名为 "SignalRChat"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="a4579-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="a4579-151">在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC**"，然后单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="a4579-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="a4579-152">项目向导将创建两个项目：</span><span class="sxs-lookup"><span data-stu-id="a4579-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="a4579-153">ChatService:此项目是 Microsoft Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4579-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="a4579-154">它定义了 Azure 角色和其他配置选项。</span><span class="sxs-lookup"><span data-stu-id="a4579-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="a4579-155">SignalRChat:此项目是你的 ASP.NET MVC 5 项目。</span><span class="sxs-lookup"><span data-stu-id="a4579-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="a4579-156">创建 SignalR Chat 应用程序</span><span class="sxs-lookup"><span data-stu-id="a4579-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="a4579-157">若要创建聊天应用程序，请按照教程[入门 With SignalR AND MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)"中的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="a4579-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="a4579-158">使用 NuGet 安装所需的库。</span><span class="sxs-lookup"><span data-stu-id="a4579-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="a4579-159">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="a4579-159">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a4579-160">在 "**程序包管理器控制台**" 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a4579-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="a4579-161">使用 `-ProjectName` 选项将包安装到 ASP.NET MVC 项目，而不是 Windows Azure 项目。</span><span class="sxs-lookup"><span data-stu-id="a4579-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="a4579-162">配置底板</span><span class="sxs-lookup"><span data-stu-id="a4579-162">Configure the Backplane</span></span>

<span data-ttu-id="a4579-163">在应用程序的 Startup.cs 文件中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="a4579-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="a4579-164">现在，需要获取服务总线连接字符串。</span><span class="sxs-lookup"><span data-stu-id="a4579-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="a4579-165">在 Azure 门户中，选择你创建的服务总线命名空间，然后单击 "访问密钥" 图标。</span><span class="sxs-lookup"><span data-stu-id="a4579-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="a4579-166">将连接字符串复制到剪贴板，然后将其粘贴到*connectionString*变量中。</span><span class="sxs-lookup"><span data-stu-id="a4579-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="a4579-167">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="a4579-167">Deploy to Azure</span></span>

<span data-ttu-id="a4579-168">在解决方案资源管理器中，展开 "ChatService" 项目中的 "**角色**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="a4579-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="a4579-169">右键单击 "SignalRChat" 角色，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="a4579-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="a4579-170">选择“配置”选项卡。在 "**实例**" 下选择2。</span><span class="sxs-lookup"><span data-stu-id="a4579-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="a4579-171">你还可以将 VM 大小设置为 "**特小**"。</span><span class="sxs-lookup"><span data-stu-id="a4579-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="a4579-172">保存更改。</span><span class="sxs-lookup"><span data-stu-id="a4579-172">Save the changes.</span></span>

<span data-ttu-id="a4579-173">在解决方案资源管理器中，右键单击 ChatService 项目。</span><span class="sxs-lookup"><span data-stu-id="a4579-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="a4579-174">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="a4579-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="a4579-175">如果这是您首次发布到 Windows Azure，则必须下载您的凭据。</span><span class="sxs-lookup"><span data-stu-id="a4579-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="a4579-176">在**发布**向导中，单击 "登录以下载凭据"。</span><span class="sxs-lookup"><span data-stu-id="a4579-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="a4579-177">这会提示你登录到 Windows Azure 门户并下载发布设置文件。</span><span class="sxs-lookup"><span data-stu-id="a4579-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="a4579-178">单击 "**导入**" 并选择已下载的发布设置文件。</span><span class="sxs-lookup"><span data-stu-id="a4579-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="a4579-179">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="a4579-179">Click **Next**.</span></span> <span data-ttu-id="a4579-180">在 "**发布设置**" 对话框中的 "**云服务**" 下，选择之前创建的云服务。</span><span class="sxs-lookup"><span data-stu-id="a4579-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="a4579-181">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="a4579-181">Click **Publish**.</span></span> <span data-ttu-id="a4579-182">部署应用程序并启动 Vm 可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="a4579-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="a4579-183">现在，在运行聊天应用程序时，角色实例将使用服务总线主题通过 Azure 服务总线进行通信。</span><span class="sxs-lookup"><span data-stu-id="a4579-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="a4579-184">主题是允许多个订阅服务器的消息队列。</span><span class="sxs-lookup"><span data-stu-id="a4579-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="a4579-185">该底板会自动创建主题和订阅。</span><span class="sxs-lookup"><span data-stu-id="a4579-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="a4579-186">若要查看订阅和消息活动，请打开 Azure 门户，选择服务总线命名空间，然后单击 "主题"。</span><span class="sxs-lookup"><span data-stu-id="a4579-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="a4579-187">需要几分钟时间，消息活动才会显示在仪表板中。</span><span class="sxs-lookup"><span data-stu-id="a4579-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="a4579-188">SignalR 管理主题生存期。</span><span class="sxs-lookup"><span data-stu-id="a4579-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="a4579-189">只要部署了你的应用程序，就不要尝试手动删除主题或更改主题的设置。</span><span class="sxs-lookup"><span data-stu-id="a4579-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a4579-190">故障排除</span><span class="sxs-lookup"><span data-stu-id="a4579-190">Troubleshooting</span></span>

<span data-ttu-id="a4579-191">**InvalidOperationException "唯一支持的 IsolationLevel 为" IsolationLevel "。**</span><span class="sxs-lookup"><span data-stu-id="a4579-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="a4579-192">如果操作的事务级别设置为 `Serializable`以外的其他内容，则可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="a4579-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="a4579-193">验证是否未对其他事务级别执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="a4579-193">Verify that no operations are being performed with other transaction levels.</span></span>
