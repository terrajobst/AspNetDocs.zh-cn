---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 使用 Web 场框架创建服务器场 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Web 场框架（WFF）2.0 从服务器集合创建和配置 web 服务器场。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517496"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a><span data-ttu-id="1e5a9-103">使用 Web Farm Framework 创建服务器场</span><span class="sxs-lookup"><span data-stu-id="1e5a9-103">Creating a Server Farm with the Web Farm Framework</span></span>

<span data-ttu-id="1e5a9-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="1e5a9-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="1e5a9-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="1e5a9-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="1e5a9-106">本主题介绍如何使用 Web 场框架（WFF）2.0 从服务器集合创建和配置 web 服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-106">This topic describes how to use the Web Farm Framework (WFF) 2.0 to create and configure a web server farm from a collection of servers.</span></span>

<span data-ttu-id="1e5a9-107">WFF 使你能够跨多个负载均衡的 web 服务器同步 web 平台产品和组件、web 应用程序、网站和配置设置。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-107">WFF lets you synchronize web platform products and components, web applications, websites, and configuration settings across multiple load-balanced web servers.</span></span> <span data-ttu-id="1e5a9-108">在需要多个 web 服务器（如过渡环境和生产环境）的情况下，这可以极大地简化部署和配置过程。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-108">In scenarios where you need more than one web server, like staging and production environments, this can vastly simplify your deployment and configuration process.</span></span> <span data-ttu-id="1e5a9-109">你可以将 web 应用程序部署到&#x2014;*主服务器*&#x2014;的一台服务器上，WFF 将在服务器场中的所有其他 web 服务器上自动复制该 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-109">You can deploy a web application to a single server&#x2014;the *primary server*&#x2014;and WFF will automatically replicate that web application on all the other web servers in the server farm.</span></span>

## <a name="understanding-the-web-farm-framework"></a><span data-ttu-id="1e5a9-110">了解 Web 场框架</span><span class="sxs-lookup"><span data-stu-id="1e5a9-110">Understanding the Web Farm Framework</span></span>

<span data-ttu-id="1e5a9-111">可以使用 WFF 2.0 预配、管理内容并将其部署到一组 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-111">You can use WFF 2.0 to provision, manage, and deploy content to a group of web servers.</span></span> <span data-ttu-id="1e5a9-112">WFF 部署由三个关键服务器角色组成：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-112">A WFF deployment consists of three key server roles:</span></span>

- <span data-ttu-id="1e5a9-113">*控制器服务器*。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-113">The *controller server*.</span></span> <span data-ttu-id="1e5a9-114">使用此服务器创建和配置 WFF 服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-114">You use this server to create and configure WFF server farms.</span></span> <span data-ttu-id="1e5a9-115">控制器服务器管理 web 平台组件、配置设置和服务器场中 web 服务器之间的应用程序的同步。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-115">The controller server manages the synchronization of web platform components, configuration settings, and applications between the web servers in a server farm.</span></span> <span data-ttu-id="1e5a9-116">在控制器服务器上安装 WFF 2.0，控制器服务器将依次在服务器场中的每台服务器上安装 WFF 代理。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-116">You install WFF 2.0 on the controller server, and the controller server will in turn install the WFF agent on each of the servers in a server farm.</span></span> <span data-ttu-id="1e5a9-117">控制器服务器在概念上并不属于任何 WFF 服务器场，单个控制器服务器可以管理多个服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-117">The controller server does not conceptually belong to any WFF server farm, and a single controller server can manage multiple server farms.</span></span> <span data-ttu-id="1e5a9-118">在此方案中，将使用单个 WFF 控制器服务器来创建和管理过渡服务器场和生产服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-118">In this scenario, you use a single WFF controller server to create and manage the staging server farm and the production server farm.</span></span>
- <span data-ttu-id="1e5a9-119">*主服务器*。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-119">The *primary server*.</span></span> <span data-ttu-id="1e5a9-120">每个 WFF 服务器场都包含单个主服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-120">Each WFF server farm includes a single primary server.</span></span> <span data-ttu-id="1e5a9-121">当你安装 web 平台组件或将应用程序部署到主服务器时，WFF 会将你所做的更改同步到服务器场中的所有其他服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-121">When you install web platform components or deploy applications to the primary server, the WFF synchronizes your changes to all the other servers in the server farm.</span></span>
- <span data-ttu-id="1e5a9-122">*辅助服务器*。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-122">The *secondary server*.</span></span> <span data-ttu-id="1e5a9-123">每个 WFF 服务器场都包含一个或多个辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-123">Each WFF server farm includes one or more secondary servers.</span></span> <span data-ttu-id="1e5a9-124">对主服务器所做的任何更改都会复制到服务器场中的每个辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-124">Any changes you make to the primary server are replicated to every secondary server within the server farm.</span></span>

<span data-ttu-id="1e5a9-125">这说明了这些服务器角色如何与 Fabrikam、Inc. 过渡和生产环境相关：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-125">This shows how these server roles relate to the Fabrikam, Inc. staging and production environments:</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

<span data-ttu-id="1e5a9-126">在此方案中，过渡环境和生产环境都配置为 WFF 服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-126">In this scenario, the staging environment and the production environment are both configured as WFF server farms.</span></span> <span data-ttu-id="1e5a9-127">单个 WFF 控制器服务器管理这两个服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-127">A single WFF controller server manages both farms.</span></span> <span data-ttu-id="1e5a9-128">在每个服务器场中，对主服务器所做的任何更改都会复制到每个辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-128">Within each server farm, any changes to the primary server are replicated to every secondary server.</span></span>

<span data-ttu-id="1e5a9-129">在开始配置过渡环境和生产环境之前，我们建议你阅读以下文章，以熟悉 WFF 2.0 的关键概念：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-129">Before you start to configure your staging and production environments, we recommend that you read these articles to familiarize yourself with the key concepts of WFF 2.0:</span></span>

- [<span data-ttu-id="1e5a9-130">用于 IIS 7 的 Web 场框架2.0 概述</span><span class="sxs-lookup"><span data-stu-id="1e5a9-130">Overview of the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805126)
- [<span data-ttu-id="1e5a9-131">使用用于 IIS 7 的 Web 场框架2.0 设置服务器场</span><span class="sxs-lookup"><span data-stu-id="1e5a9-131">Setting up a Server Farm with the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805127)
- [<span data-ttu-id="1e5a9-132">用于 IIS 7 的 Web 场框架2.0 的系统和平台要求</span><span class="sxs-lookup"><span data-stu-id="1e5a9-132">System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a><span data-ttu-id="1e5a9-133">任务概述</span><span class="sxs-lookup"><span data-stu-id="1e5a9-133">Task Overview</span></span>

<span data-ttu-id="1e5a9-134">若要完成本主题中的任务和演练，你将需要至少三个&#x2014;服务器：一个 WFF 控制器，一个是服务器场的主 web 服务器，并且是服务器场的一个或多个辅助 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-134">To complete the tasks and walkthroughs in this topic, you'll need at least three servers&#x2014;one WFF controller, one primary web server for the server farm, and one or more secondary web servers for the server farm.</span></span> <span data-ttu-id="1e5a9-135">你可以随时将更多辅助服务器添加到 WFF 服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-135">You can add more secondary servers to a WFF server farm at any time.</span></span> <span data-ttu-id="1e5a9-136">在高级别中，若要为过渡环境或生产环境创建和配置 WFF 服务器场，需要：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-136">At a high level, to create and configure a WFF server farm for your staging or production environment you'll need to:</span></span>

- <span data-ttu-id="1e5a9-137">通过安装 Internet Information Services （IIS）7.5 和 WFF 2.0 创建控制器服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-137">Create a controller server by installing Internet Information Services (IIS) 7.5 and WFF 2.0.</span></span>
- <span data-ttu-id="1e5a9-138">通过创建通用的管理员帐户并配置防火墙例外来准备主服务器和辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-138">Prepare primary and secondary servers by creating a common administrator account and configuring firewall exceptions.</span></span>
- <span data-ttu-id="1e5a9-139">使用控制器服务器上的 IIS 管理器来配置服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-139">Configure the server farm by using IIS Manager on the controller server.</span></span>
- <span data-ttu-id="1e5a9-140">使用 IIS 应用程序请求路由（ARR）或其他负载平衡技术配置负载平衡。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-140">Configure load balancing using IIS Application Request Routing (ARR) or an alternative load-balancing technology.</span></span>

<span data-ttu-id="1e5a9-141">本主题中的任务和演练假设你要从运行 Windows Server 2008 R2 的干净服务器版本开始。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-141">The tasks and walkthroughs in this topic assume that you're starting with clean server builds running Windows Server 2008 R2.</span></span> <span data-ttu-id="1e5a9-142">在开始之前，对于每个服务器，请确保：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-142">Before you begin, for each server, ensure that:</span></span>

- <span data-ttu-id="1e5a9-143">Windows Server 2008 R2 Service Pack 1 和所有可用更新均已安装。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-143">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="1e5a9-144">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-144">The server is domain-joined.</span></span>
- <span data-ttu-id="1e5a9-145">服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-145">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="1e5a9-146">有关将计算机加入域的详细信息，请参阅将[计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-146">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="1e5a9-147">有关配置静态 IP 地址的详细信息，请参阅[配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-147">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="create-the-wff-controller-server"></a><span data-ttu-id="1e5a9-148">创建 WFF 控制器服务器</span><span class="sxs-lookup"><span data-stu-id="1e5a9-148">Create the WFF Controller Server</span></span>

<span data-ttu-id="1e5a9-149">若要创建 WFF 控制器服务器，需要安装 IIS 7 或更高版本以及 WFF 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-149">To create a WFF controller server, you'll need to install both IIS 7 or later and WFF 2.0 or later.</span></span> <span data-ttu-id="1e5a9-150">在这两个方面，WFF 使用 IIS Web 部署工具（Web 部署）2.x 来同步场中的服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-150">Under the covers, WFF uses the IIS Web Deployment Tool (Web Deploy) 2.x to synchronize the servers in your farm.</span></span> <span data-ttu-id="1e5a9-151">如果使用 Web 平台安装程序安装 WFF，则安装程序将自动下载并安装 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-151">If you use the Web Platform Installer to install WFF, the installer will automatically download and install Web Deploy for you.</span></span>

<span data-ttu-id="1e5a9-152">**创建 WFF 控制器服务器**</span><span class="sxs-lookup"><span data-stu-id="1e5a9-152">**To create the WFF controller server**</span></span>

1. <span data-ttu-id="1e5a9-153">下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9739157)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-153">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9739157).</span></span>
2. <span data-ttu-id="1e5a9-154">在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-154">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="1e5a9-155">在窗口左侧的导航窗格中，单击 "**服务器**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-155">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="1e5a9-156">在 " **IIS 7 推荐的配置**" 行中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-156">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
5. <span data-ttu-id="1e5a9-157">在<strong>Web 场框架2中。</strong><em>x</em>行，单击 "<strong>添加</strong>"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-157">In the <strong>Web Farm Framework 2.</strong><em>x</em> row, click <strong>Add</strong>.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. <span data-ttu-id="1e5a9-158">单击“安装”。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-158">Click **Install**.</span></span> <span data-ttu-id="1e5a9-159">请注意，Web 平台安装程序已在安装列表中添加了 Web 部署工具和其他各种依赖关系。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-159">Notice that the Web Platform Installer has added the Web Deployment Tool, along with various other dependencies, to the installation list.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. <span data-ttu-id="1e5a9-160">查看许可条款，如果同意条款，请单击 "**我接受**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-160">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
8. <span data-ttu-id="1e5a9-161">安装完成后，单击 "**完成**"，然后关闭 " **Web 平台安装程序 3.0** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-161">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

## <a name="configure-the-primary-and-secondary-servers"></a><span data-ttu-id="1e5a9-162">配置主服务器和辅助服务器</span><span class="sxs-lookup"><span data-stu-id="1e5a9-162">Configure the Primary and Secondary Servers</span></span>

<span data-ttu-id="1e5a9-163">在创建 WFF 服务器场之前，应在将构成场的 web 服务器上完成一些准备任务：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-163">Before you create a WFF server farm, you should complete some preparation tasks on the web servers that will make up the farm:</span></span>

- <span data-ttu-id="1e5a9-164">添加防火墙例外以允许**核心网络**、**远程管理**以及**文件和打印机共享**功能与 WFF 控制器服务器进行通信。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-164">Add firewall exceptions to allow the **Core Networking**, **Remote Administration**, and **File and Printer Sharing** features to communicate with the WFF controller server.</span></span>
- <span data-ttu-id="1e5a9-165">在 Active Directory 中创建一个域帐户（例如， **FABRIKAM\stagingfarm**），并将其添加到每台服务器上的本地管理员组。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-165">Create a domain account (for example, **FABRIKAM\stagingfarm**) in Active Directory and add it to the local administrators group on each server.</span></span> <span data-ttu-id="1e5a9-166">创建服务器场时，将使用此帐户作为服务器场管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-166">You'll use this account as the server farm administrator account when you create the server farm.</span></span>

<span data-ttu-id="1e5a9-167">有关如何在 Windows 防火墙中配置这些防火墙例外的详细信息，请参阅[适用于 IIS 7 的 Web 场框架2.0 的系统和平台要求](https://go.microsoft.com/?linkid=9805128)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-167">For more information on how to configure these firewall exceptions in Windows Firewall, see [System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805128).</span></span> <span data-ttu-id="1e5a9-168">对于其他防火墙系统，请参阅产品文档。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-168">For other firewall systems, consult your product documentation.</span></span>

<span data-ttu-id="1e5a9-169">您可以使用下一个过程将域帐户添加到 Windows Server 2008 R2 中的本地管理员组。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-169">You can use the next procedure to add a domain account to the local administrators group in Windows Server 2008 R2.</span></span> <span data-ttu-id="1e5a9-170">你应在要添加到服务器场&#x2014;中的每个服务器上执行此过程，换言之，将同一个域帐户添加到主服务器和每个辅助服务器上的本地管理员组中。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-170">You should perform this procedure on every server that you want to add to the server farm&#x2014;in other words, add the same domain account to the local administrators group on the primary server and on each secondary server.</span></span>

<span data-ttu-id="1e5a9-171">**将域帐户添加到本地管理员组**</span><span class="sxs-lookup"><span data-stu-id="1e5a9-171">**To add a domain account to the local administrators group**</span></span>

1. <span data-ttu-id="1e5a9-172">在 "**开始**" 菜单上，指向 "**管理工具**"，然后单击 "**服务器管理器**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-172">On the **Start** menu, point to **Administrative Tools**, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="1e5a9-173">在 "**服务器管理器**" 窗口的树视图窗格中，展开 "**配置**"，展开 "**本地用户和组**"，然后单击 "**组**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-173">In the **Server Manager** window, in the tree view pane, expand **Configuration**, expand **Local Users and Groups**, and then click **Groups**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. <span data-ttu-id="1e5a9-174">在 "**组**" 窗格中，双击 "**管理员**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-174">In the **Groups** pane, double-click **Administrators**.</span></span>
4. <span data-ttu-id="1e5a9-175">在 "**管理员属性**" 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-175">In the **Administrators Properties** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="1e5a9-176">在 "**选择用户、计算机、服务帐户或组**" 对话框中，键入（或浏览）到你的域帐户（例如， **FABRIKAM\stagingfarm**），然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-176">In the **Select Users, Computers, Service Accounts, or Groups** dialog box, type (or browse) to your domain account (for example, **FABRIKAM\stagingfarm**), and then click **OK**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. <span data-ttu-id="1e5a9-177">在 "**管理员属性**" 对话框中，单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-177">In the **Administrators Properties** dialog box, click **OK**.</span></span>

<span data-ttu-id="1e5a9-178">服务器现在可以添加到服务器场中。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-178">Your servers are now ready to be added to a server farm.</span></span> <span data-ttu-id="1e5a9-179">对于主服务器，你可以在这两种情况下，将服务器配置为满足你在创建服务器场&#x2014;之前或之后的应用程序要求，WFF 将通过将相同的产品、组件或配置部署到辅助服务器来同步服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-179">In the case of the primary server, you can configure the server to meet your application requirements before or after you create the server farm&#x2014;in both cases, the WFF will synchronize the servers by deploying the same products, components, or configuration to your secondary servers.</span></span> <span data-ttu-id="1e5a9-180">为了简单起见，本教程假定你将在完成创建服务器场后配置主服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-180">For the sake of simplicity, this tutorial assumes that you'll configure the primary server when you've finished creating the server farm.</span></span>

## <a name="create-the-wff-server-farm"></a><span data-ttu-id="1e5a9-181">创建 WFF 服务器场</span><span class="sxs-lookup"><span data-stu-id="1e5a9-181">Create the WFF Server Farm</span></span>

<span data-ttu-id="1e5a9-182">此时，所有服务器都已准备好添加到 WFF 服务器场：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-182">At this point, all your servers are ready to be added to a WFF server farm:</span></span>

- <span data-ttu-id="1e5a9-183">已在控制器服务器上安装 WFF。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-183">You've installed WFF on the controller server.</span></span>
- <span data-ttu-id="1e5a9-184">你已在主和辅助 web 服务器上配置防火墙例外。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-184">You've configured firewall exceptions on your primary and secondary web servers.</span></span>
- <span data-ttu-id="1e5a9-185">已将域帐户添加到主和辅助 web 服务器上的本地管理员组。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-185">You've added a domain account to the local administrators group on your primary and secondary web servers.</span></span>

<span data-ttu-id="1e5a9-186">下一步是在 WFF 中创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-186">The next step is to create the server farm in WFF.</span></span> <span data-ttu-id="1e5a9-187">可以从 WFF 控制器服务器上的 IIS 管理器执行此操作。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-187">You can do this from IIS Manager on the WFF controller server.</span></span>

<span data-ttu-id="1e5a9-188">**创建 WFF 服务器场**</span><span class="sxs-lookup"><span data-stu-id="1e5a9-188">**To create a WFF server farm**</span></span>

1. <span data-ttu-id="1e5a9-189">在 WFF 控制器服务器上的 "**开始**" 菜单中，指向 "**管理工具**"，然后单击 " **Internet Information Services （IIS）管理器**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-189">On the WFF controller server, on the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="1e5a9-190">在 "**连接**" 窗格中，展开本地服务器节点，右键单击 "**服务器场**"，然后单击 "**创建服务器场**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-190">In the **Connections** pane, expand the local server node, right-click **Server Farms**, and then click **Create Server Farm**.</span></span>
3. <span data-ttu-id="1e5a9-191">在 "**创建服务器场**" 对话框中，为服务器场键入有意义的名称（例如，**过渡场**），然后选择 "**设置服务器场**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-191">In the **Create Server Farm** dialog box, type a meaningful name for the server farm (for example, **Staging Farm**), and then select **Provision server farm**.</span></span>
4. <span data-ttu-id="1e5a9-192">键入添加到每个服务器上的本地管理员组的域帐户的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-192">Type the user name and password of the domain account that you added to the local administrators group on each server.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. <span data-ttu-id="1e5a9-193">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-193">Click **Next**.</span></span>
6. <span data-ttu-id="1e5a9-194">在 "**添加服务器**" 页上，键入主服务器的完全限定的域名（FQDN），选择 "**主服务器**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-194">On the **Add Servers** page, type the fully qualified domain name (FQDN) of the primary server, select **Primary Server**, and then click **Add**.</span></span>
7. <span data-ttu-id="1e5a9-195">此时，WFF 将尝试使用所提供的凭据联系主服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-195">At this point, WFF will attempt to contact the primary server using the credentials you provided.</span></span> <span data-ttu-id="1e5a9-196">如果连接成功，则会将主服务器添加到 "**添加服务器**" 页上的表中。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-196">If the connection succeeds, the primary server will be added to the table on the **Add Servers** page.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="1e5a9-197">您可能已注意到，默认情况下，**服务器可用于负载平衡**。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-197">You might have noticed that **Server is available for Load Balancing** is selected by default.</span></span> <span data-ttu-id="1e5a9-198">WFF 使用 IIS ARR 模块来实现负载平衡，从而在服务器场中的 web 服务器之间分发请求。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-198">WFF uses the IIS ARR module to implement load balancing and thereby distribute requests across the web servers in your server farm.</span></span> <span data-ttu-id="1e5a9-199">在大多数情况下，如果想要使用第三方负载平衡解决方案，只需清除 "**服务器可用于负载平衡**" 选项。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-199">In most scenarios, you'd only clear the **Server is available for Load Balancing** option if you wanted to use a third-party load balancing solution instead.</span></span>
8. <span data-ttu-id="1e5a9-200">在 "**添加服务器**" 页上，键入第一个辅助服务器的 FQDN，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-200">On the **Add Servers** page, type the FQDN of your first secondary server, and then click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. <span data-ttu-id="1e5a9-201">对场中的任何其他辅助服务器重复步骤7，然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-201">Repeat step 7 for any additional secondary servers in your farm, and then click **Finish**.</span></span>

<span data-ttu-id="1e5a9-202">你的 WFF 服务器场现在已启动并正在运行。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-202">Your WFF server farm is now up and running.</span></span> <span data-ttu-id="1e5a9-203">在主服务器上安装的任何 web 平台产品或组件以及部署到主服务器的任何 web 应用程序或内容都将自动预配到所有辅助服务器上。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-203">Any web platform products or components that you install on the primary server, and any web applications or content that you deploy to the primary server, will be automatically provisioned on all your secondary servers.</span></span>

<span data-ttu-id="1e5a9-204">WFF 是一个广泛而又复杂的主题，你可以在[用于 IIS 7 的 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129)网站上了解有关该主题的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-204">WFF is a broad and complex topic, and you can learn more about it on the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span> <span data-ttu-id="1e5a9-205">但在这种情况下，需要注意以下两个功能区域：</span><span class="sxs-lookup"><span data-stu-id="1e5a9-205">For the time being, however, there are two features areas that you need to be aware of:</span></span>

- <span data-ttu-id="1e5a9-206">*应用程序预配*是指在服务器场中的所有辅助服务器上复制主服务器的内容（例如 web 应用程序和配置设置）的过程。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-206">*Application provisioning* is the process that replicates content from the primary server, like web applications and configuration settings, across all the secondary servers in the server farm.</span></span> <span data-ttu-id="1e5a9-207">例如，如果您将联系人管理器示例解决方案部署到主临时服务器，则 WFF 应用程序预配过程会将此解决方案部署到所有辅助暂存服务器。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-207">For example, if you deploy the Contact Manager sample solution to your primary staging server, the WFF application provisioning process will deploy this solution to all your secondary staging servers.</span></span> <span data-ttu-id="1e5a9-208">默认情况下，应用程序预配过程每隔30秒运行一次。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-208">By default, the application provisioning process runs every 30 seconds.</span></span>
- <span data-ttu-id="1e5a9-209">*平台设置*是将 web 平台产品和组件从主服务器同步到服务器场中的所有辅助服务器的过程。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-209">*Platform provisioning* is the process that synchronizes web platform products and components from the primary server to all the secondary servers in the server farm.</span></span> <span data-ttu-id="1e5a9-210">例如，如果在主过渡服务器上安装 ASP.NET MVC 3，则平台预配过程将使用 Web 平台安装程序在所有辅助暂存服务器上安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-210">For example, if you install ASP.NET MVC 3 on your primary staging server, the platform provisioning process will use the Web Platform Installer to install ASP.NET MVC 3 on all your secondary staging servers.</span></span> <span data-ttu-id="1e5a9-211">默认情况下，平台预配过程每五分钟运行一次。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-211">By default, the platform provisioning process runs every five minutes.</span></span>

<span data-ttu-id="1e5a9-212">你可以从 WFF 控制器服务器上的 IIS 管理器中管理基本应用程序和平台设置设置。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-212">You can manage basic application and platform provisioning settings from IIS Manager on your WFF controller server.</span></span>

<span data-ttu-id="1e5a9-213">**了解应用程序和平台预配设置**</span><span class="sxs-lookup"><span data-stu-id="1e5a9-213">**Explore application and platform provisioning settings**</span></span>

1. <span data-ttu-id="1e5a9-214">在 IIS 管理器的 "**连接**" 窗格中，选择服务器场。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-214">In IIS Manager, in the **Connections** pane, select your server farm.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. <span data-ttu-id="1e5a9-215">在 "**服务器场**" 窗格中，双击 "**应用程序设置**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-215">In the **Server Farm** pane, double-click **Application Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. <span data-ttu-id="1e5a9-216">如您所见，服务器场当前配置为每隔30秒同步主服务器和辅助服务器之间的 web 内容和配置设置。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-216">As you can see, the server farm is currently configured to synchronize web content and configuration settings between the primary server and the secondary servers every 30 seconds.</span></span>
4. <span data-ttu-id="1e5a9-217">单击 "**上一步**"，然后双击 "**平台设置**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-217">Click **Back**, and then double-click **Platform Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. <span data-ttu-id="1e5a9-218">正如您所看到的，当前已将服务器场配置为每隔五分钟同步主服务器和辅助服务器之间的 web 平台产品和组件。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-218">As you can see, the server farm is currently configured to synchronize web platform products and components between the primary server and the secondary servers every five minutes.</span></span>
6. <span data-ttu-id="1e5a9-219">单击 **“上一步”** 。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-219">Click **Back**.</span></span>
7. <span data-ttu-id="1e5a9-220">若要强制服务器场立即同步 web 平台产品，请在 "**操作**" 窗格中单击 "**预配平台**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-220">To force the server farm to synchronize web platform products immediately, in the **Actions** pane, click **Provision Platform**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > <span data-ttu-id="1e5a9-221">平台设置可能需要一段时间。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-221">Platform provisioning may take some time.</span></span> <span data-ttu-id="1e5a9-222">安装程序进程在服务器场中的辅助服务器上的后台运行。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-222">The installer process runs in the background on the secondary servers in your server farm.</span></span>
8. <span data-ttu-id="1e5a9-223">一旦你已允许足够的时间来完成预配过程，你可以验证你已添加到主服务器的产品和组件现在已在辅助服务器上复制。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-223">Once you've allowed sufficient time for the provisioning process to complete, you can verify that the products and components that you added to the primary server have now been replicated on the secondary servers.</span></span> <span data-ttu-id="1e5a9-224">例如，你可以登录到辅助服务器，并使用 "**服务器管理器**" 窗口验证是否已安装 web 服务器角色。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-224">For example, you can log on to a secondary server and use the **Server Manager** window to verify that the web server role has been installed.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. <span data-ttu-id="1e5a9-225">你还可以查看 "已安装的程序" 列表以验证是否添加了各种 web 平台组件。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-225">You can also check the installed programs list to verify that various web platform components have been added.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a><span data-ttu-id="1e5a9-226">配置负载均衡</span><span class="sxs-lookup"><span data-stu-id="1e5a9-226">Configure Load Balancing</span></span>

<span data-ttu-id="1e5a9-227">创建 web 场时，需要设置某种形式的负载均衡，以便在 web 服务器之间分发 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-227">When you create a web farm, you need to set up some form of load balancing to distribute HTTP requests between your web servers.</span></span> <span data-ttu-id="1e5a9-228">这可能是 Windows Server 2008 网络负载平衡、IIS ARR 或基于软件的第三方或基于硬件的负载平衡解决方案。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-228">This could be Windows Server 2008 network load balancing, IIS ARR, or a third-party software-based or hardware-based load balancing solution.</span></span>

<span data-ttu-id="1e5a9-229">WFF 旨在与 IIS ARR 紧密集成。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-229">WFF is designed to integrate closely with IIS ARR.</span></span> <span data-ttu-id="1e5a9-230">若要利用此集成，需要在 WFF 控制器服务器上安装 ARR 模块。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-230">To take advantage of this integration, you need to install the ARR module on the WFF controller server.</span></span> <span data-ttu-id="1e5a9-231">然后，你可以将所有 web 流量定向到控制器服务器，通常通过配置域名系统（DNS）记录。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-231">You then direct all your web traffic to the controller server, typically by configuring Domain Name System (DNS) records.</span></span> <span data-ttu-id="1e5a9-232">然后，控制器服务器将根据服务器可用性和其他各种条件在服务器场中的服务器之间分发传入的请求。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-232">The controller server will then distribute incoming requests among the servers in your farm, based on server availability and various other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="1e5a9-233">不需要对 WFF 使用 ARR;可以将 WFF 配置为使用第三方负载平衡解决方案。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-233">You don't have to use ARR with WFF; you can configure WFF to work with third-party load balancing solutions.</span></span> <span data-ttu-id="1e5a9-234">有关详细信息，请参阅[用于 IIS 7 的 Web 场框架2.0 概述](https://go.microsoft.com/?linkid=9805126)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-234">For more information, see [Overview of the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805126).</span></span>

<span data-ttu-id="1e5a9-235">使用 ARR 进行负载平衡是一个复杂的主题，其中大多数都超出了本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-235">Load balancing using ARR is a complex topic, most of which is beyond the scope of this tutorial.</span></span> <span data-ttu-id="1e5a9-236">但是，您可以使用下一个过程安装 ARR 模块，并开始进行负载平衡。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-236">However, you can use the next procedure to install the ARR module and get started with load balancing.</span></span>

<span data-ttu-id="1e5a9-237">**在 WFF 控制器服务器上设置负载均衡**</span><span class="sxs-lookup"><span data-stu-id="1e5a9-237">**To set up load balancing on the WFF controller server**</span></span>

1. <span data-ttu-id="1e5a9-238">在 WFF 控制器服务器上，启动 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-238">On the WFF controller server, launch the Web Platform Installer.</span></span>
2. <span data-ttu-id="1e5a9-239">在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-239">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="1e5a9-240">在窗口左侧的导航窗格中，单击 "**服务器**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-240">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="1e5a9-241">在**应用程序请求路由 2.5**行中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-241">In the **Application Request Routing 2.5** row, click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. <span data-ttu-id="1e5a9-242">单击 "**安装**"，然后按照**Web 平台安装**窗口中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-242">Click **Install**, and then follow the instructions in the **Web Platform Installation** window.</span></span>
6. <span data-ttu-id="1e5a9-243">安装完成后，启动 IIS 管理器，然后在 "**连接**" 窗格中，单击 "服务器场" 节点。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-243">When the installation is complete, launch IIS Manager, and in the **Connections** pane, click your server farm node.</span></span> <span data-ttu-id="1e5a9-244">请注意，已在 "**服务器场**" 窗格中添加了几个新图标。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-244">Notice that several new icons have been added to the **Server Farm** pane.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. <span data-ttu-id="1e5a9-245">在 "**服务器场**" 窗格中，双击 "**负载均衡**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-245">In the **Server Farm** pane, double-click **Load Balance**.</span></span>
8. <span data-ttu-id="1e5a9-246">在 "**负载平衡**" 窗格中，选择负载平衡算法（例如，**最小的请求**）。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-246">In the **Load Balance** pane, select a load balance algorithm (for example, **Least current request**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e5a9-247">有关负载平衡算法和其他配置设置的详细信息，请参阅[应用程序请求路由模块](https://go.microsoft.com/?linkid=9805130)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-247">For more information on load balancing algorithms and other configuration settings, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. <span data-ttu-id="1e5a9-248">在 "**操作**" 窗格中，单击 "**应用**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-248">In the **Actions** pane, click **Apply**.</span></span>

<span data-ttu-id="1e5a9-249">你现在已为服务器场中的服务器配置了基本负载平衡。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-249">You have now configured basic load balancing for the servers in your server farm.</span></span> <span data-ttu-id="1e5a9-250">如果将所有 web 场流量定向到控制器服务器，则会根据可用性和所选的负载平衡算法在服务器场中的服务器之间分配请求。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-250">If you direct all your web farm traffic to the controller server, the requests will be distributed between the servers in your farm according to availability and the load balancing algorithm you selected.</span></span>

<span data-ttu-id="1e5a9-251">若要详细了解如何通过 ARR 配置负载平衡，请参阅[应用程序请求路由模块](https://go.microsoft.com/?linkid=9805130)。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-251">For more information on how to configure load balancing with ARR, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

## <a name="monitor-the-server-farm"></a><span data-ttu-id="1e5a9-252">监视服务器场</span><span class="sxs-lookup"><span data-stu-id="1e5a9-252">Monitor the Server Farm</span></span>

<span data-ttu-id="1e5a9-253">你可以随时通过控制器服务器上的 IIS 管理器监视服务器场的运行状况。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-253">You can monitor the health of your server farm at any time through IIS Manager on the controller server.</span></span> <span data-ttu-id="1e5a9-254">在 "**连接**" 窗格中，展开服务器场，然后单击 "**服务器**"。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-254">In the **Connections** pane, expand your server farm, and then click **Servers**.</span></span> <span data-ttu-id="1e5a9-255">中间窗格将显示场中每个服务器的摘要，以及最近活动的跟踪日志。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-255">The center pane will show a summary of each server in the farm together with a trace log of recent activity.</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a><span data-ttu-id="1e5a9-256">结束语</span><span class="sxs-lookup"><span data-stu-id="1e5a9-256">Conclusion</span></span>

<span data-ttu-id="1e5a9-257">WFF 服务器场现在应启动并运行。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-257">Your WFF server farm should now be up and running.</span></span> <span data-ttu-id="1e5a9-258">你可以将主服务器配置为支持你首选&#x2014;的任何部署方法。有关详细信息&#x2014;，你的配置将在服务器场中的每个辅助服务器上复制。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-258">You can configure the primary server to support whichever deployment approach you prefer&#x2014;see the Further Reading section for details&#x2014;and your configuration will be replicated on each secondary server in the server farm.</span></span>

## <a name="further-reading"></a><span data-ttu-id="1e5a9-259">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="1e5a9-259">Further Reading</span></span>

<span data-ttu-id="1e5a9-260">有关配置和使用 WFF 的所有方面的更多指导，请参阅[适用于 IIS 7 的 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129)网站。</span><span class="sxs-lookup"><span data-stu-id="1e5a9-260">For more guidance on all aspects of configuring and using the WFF, see the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e5a9-261">[上一页](configuring-a-database-server-for-web-deploy-publishing.md)
> [下一页](configuring-deployment-properties-for-a-target-environment.md)</span><span class="sxs-lookup"><span data-stu-id="1e5a9-261">[Previous](configuring-a-database-server-for-web-deploy-publishing.md)
[Next](configuring-deployment-properties-for-a-target-environment.md)</span></span>
