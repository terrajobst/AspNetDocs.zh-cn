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
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="1f808-104">在 Azure 应用服务中通过 Web 应用使用 SignalR</span><span class="sxs-lookup"><span data-stu-id="1f808-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="1f808-105">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="1f808-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="1f808-106">本文档介绍如何配置 Microsoft Azure 上运行的 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f808-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1f808-107">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="1f808-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="1f808-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)或 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1f808-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="1f808-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1f808-109">.NET 4.5</span></span>
> - <span data-ttu-id="1f808-110">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="1f808-110">SignalR version 2</span></span>
> - <span data-ttu-id="1f808-111">适用于 Visual Studio 2013 的 Azure SDK 2.3 或2012</span><span class="sxs-lookup"><span data-stu-id="1f808-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="1f808-112">问题和注释</span><span class="sxs-lookup"><span data-stu-id="1f808-112">Questions and comments</span></span>
>
> <span data-ttu-id="1f808-113">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="1f808-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="1f808-114">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)、 [StackOverflow.com](http://stackoverflow.com/)或[Microsoft Azure 论坛](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)。</span><span class="sxs-lookup"><span data-stu-id="1f808-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="1f808-115">目录</span><span class="sxs-lookup"><span data-stu-id="1f808-115">Table of Contents</span></span>

- [<span data-ttu-id="1f808-116">介绍</span><span class="sxs-lookup"><span data-stu-id="1f808-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="1f808-117">将 SignalR Web 应用部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1f808-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="1f808-118">在 Azure App Service 上启用 Websocket</span><span class="sxs-lookup"><span data-stu-id="1f808-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="1f808-119">使用 Azure Redis 缓存底板</span><span class="sxs-lookup"><span data-stu-id="1f808-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="1f808-120">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1f808-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="1f808-121">简介</span><span class="sxs-lookup"><span data-stu-id="1f808-121">Introduction</span></span>

<span data-ttu-id="1f808-122">ASP.NET SignalR 可用于在服务器和 web 或 .NET 客户端之间引入新的交互级别。</span><span class="sxs-lookup"><span data-stu-id="1f808-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="1f808-123">托管在 Azure 中时，SignalR 的应用程序可以利用在云中运行的高度可用、可缩放且高性能的环境。</span><span class="sxs-lookup"><span data-stu-id="1f808-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="1f808-124">将 SignalR Web 应用部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1f808-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="1f808-125">SignalR 不会将应用程序部署到 Azure 与部署到本地服务器的任何特定复杂之处。</span><span class="sxs-lookup"><span data-stu-id="1f808-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="1f808-126">可以在 Azure 中托管使用 SignalR 的应用程序，而无需更改配置或其他设置（但对于 Websocket 支持，请参阅下面[Azure App Service 上的启用 websocket](#websocket) 。）对于本教程，请将[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中创建的应用程序部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1f808-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="1f808-127">**先决条件**</span><span class="sxs-lookup"><span data-stu-id="1f808-127">**Prerequisites**</span></span>

- <span data-ttu-id="1f808-128">Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="1f808-128">Visual Studio 2013.</span></span> <span data-ttu-id="1f808-129">如果没有 Visual Studio，则在安装 Azure SDK 时，将 Visual Studio 2013 Express for Web。</span><span class="sxs-lookup"><span data-stu-id="1f808-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="1f808-130">[用于 Visual Studio 2013 的 AZURE sdk 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409)或[用于 Visual Studio 2012 的 azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)。</span><span class="sxs-lookup"><span data-stu-id="1f808-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="1f808-131">若要完成本教程，你需要一个 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="1f808-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="1f808-132">可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，或[注册试用版订阅](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1f808-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="1f808-133">将 SignalR web 应用部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="1f808-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="1f808-134">完成[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)，或者从[代码库](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下载完成的项目。</span><span class="sxs-lookup"><span data-stu-id="1f808-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="1f808-135">在 Visual Studio 中，选择 "**生成**"，**发布 SignalR Chat**。</span><span class="sxs-lookup"><span data-stu-id="1f808-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="1f808-136">在 "发布 Web" 对话框中，选择 "Microsoft Azure 网站"。</span><span class="sxs-lookup"><span data-stu-id="1f808-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![选择 Azure 网站](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="1f808-138">如果你未登录到 Microsoft 帐户，请单击 "选择现有网站" 对话框中的 "**登录 ...** "，然后登录。</span><span class="sxs-lookup"><span data-stu-id="1f808-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![选择现有网站](using-signalr-with-azure-web-sites/_static/image2.png)    ![登录 Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="1f808-141">在 "选择现有网站" 对话框中，单击 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="1f808-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![新建网站](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="1f808-143">在 "在 Microsoft Azure 上创建站点" 对话框中，输入唯一的应用名称。</span><span class="sxs-lookup"><span data-stu-id="1f808-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="1f808-144">在 "区域" 下拉列表中选择离你最近的区域。</span><span class="sxs-lookup"><span data-stu-id="1f808-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="1f808-145">单击 **“创建”** 。</span><span class="sxs-lookup"><span data-stu-id="1f808-145">Click **Create**.</span></span>

    ![在 Azure 中创建网站](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="1f808-147">在 "发布 Web" 对话框中，单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="1f808-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![发布站点](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="1f808-149">当应用完成发布时，Azure App Service Web Apps 中承载的 SignalR Chat 应用程序将在浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="1f808-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![站点在浏览器中打开](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="1f808-151">在 Azure App Service Web 应用上启用 Websocket</span><span class="sxs-lookup"><span data-stu-id="1f808-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="1f808-152">需要在 web 应用中显式启用 Websocket，才能在 SignalR 应用程序中使用;否则，将使用其他协议（有关详细信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)）。</span><span class="sxs-lookup"><span data-stu-id="1f808-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="1f808-153">若要在 Azure App Service Web 应用上使用 Websocket，请在 web 应用的 "配置" 部分中启用它。</span><span class="sxs-lookup"><span data-stu-id="1f808-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="1f808-154">为此，请在[Azure 管理门户](https://manage.windowsazure.com/)中打开 web 应用，并选择 "配置"。</span><span class="sxs-lookup"><span data-stu-id="1f808-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![配置选项卡](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="1f808-156">在配置页的顶部，确保将 .NET 4.5 用于 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1f808-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET framework 4.5 版设置](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="1f808-158">在 "配置" 页上，在 " **websocket** " 设置中选择 **"打开**"。</span><span class="sxs-lookup"><span data-stu-id="1f808-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Websocket 设置：开启](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="1f808-160">在配置页的底部，选择 "**保存**" 以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="1f808-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![保存设置](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="1f808-162">使用 Azure Redis 缓存底板</span><span class="sxs-lookup"><span data-stu-id="1f808-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="1f808-163">如果你使用 web 应用的多个实例，并且这些实例的用户需要彼此交互（例如，在一个实例中创建的聊天消息可以访问连接到其他实例的用户），则必须在应用程序中实现[Azure Redis 缓存底板](../performance/scaleout-with-redis.md)。</span><span class="sxs-lookup"><span data-stu-id="1f808-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="1f808-164">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1f808-164">Next Steps</span></span>

<span data-ttu-id="1f808-165">有关 Azure App Service 中 Web 应用的详细信息，请参阅[Web 应用概述](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)。</span><span class="sxs-lookup"><span data-stu-id="1f808-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
