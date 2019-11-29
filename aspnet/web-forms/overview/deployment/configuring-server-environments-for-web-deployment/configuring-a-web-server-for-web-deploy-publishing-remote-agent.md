---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 为 Web 部署发布配置 Web 服务器（远程代理） |Microsoft Docs
author: jrjlee
description: 本主题介绍如何将 Internet Information Services （IIS） web 服务器配置为支持使用 IIS Web 部署的 web 发布和部署 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: ce0d246afdfb65c2ea15a287064511e7d1d58622
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589052"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a><span data-ttu-id="4914f-103">配置用于 Web 部署发布的 Web 服务器（远程代理）</span><span class="sxs-lookup"><span data-stu-id="4914f-103">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>

<span data-ttu-id="4914f-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4914f-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4914f-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="4914f-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4914f-106">本主题介绍如何使用 IIS Web 部署工具（Web 部署）远程代理服务配置 Internet Information Services （IIS） web 服务器，以支持 web 发布和部署。</span><span class="sxs-lookup"><span data-stu-id="4914f-106">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deployment Tool (Web Deploy) Remote Agent Service.</span></span>
> 
> <span data-ttu-id="4914f-107">使用 Web 部署2.0 或更高版本时，有三种主要方法可用于将应用程序或站点获取到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4914f-107">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="4914f-108">你可以：</span><span class="sxs-lookup"><span data-stu-id="4914f-108">You can:</span></span>
> 
> - <span data-ttu-id="4914f-109">使用*Web 部署远程代理服务*。</span><span class="sxs-lookup"><span data-stu-id="4914f-109">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="4914f-110">此方法需要较少的 web 服务器配置，但你需要提供本地服务器管理员的凭据才能将任何内容部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="4914f-110">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="4914f-111">使用*Web 部署处理程序*。</span><span class="sxs-lookup"><span data-stu-id="4914f-111">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="4914f-112">这种方法更复杂，需要进行更多初始工作才能设置 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4914f-112">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="4914f-113">但是，在使用此方法时，可以将 IIS 配置为允许非管理员用户执行部署。</span><span class="sxs-lookup"><span data-stu-id="4914f-113">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="4914f-114">Web 部署处理程序仅在 IIS 版本7或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="4914f-114">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="4914f-115">使用*脱机部署*。</span><span class="sxs-lookup"><span data-stu-id="4914f-115">Use *offline deployment*.</span></span> <span data-ttu-id="4914f-116">此方法需要最少的 web 服务器配置，但服务器管理员必须手动将 web 包复制到服务器上，并通过 IIS 管理器将其导入。</span><span class="sxs-lookup"><span data-stu-id="4914f-116">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="4914f-117">有关这些方法的主要功能、优点和缺点的详细信息，请参阅[选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="4914f-117">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a><span data-ttu-id="4914f-118">Web 部署远程代理是否适合你？</span><span class="sxs-lookup"><span data-stu-id="4914f-118">Is the Web Deploy Remote Agent the Right Approach for You?</span></span>

<span data-ttu-id="4914f-119">是的，如果要部署内容的用户可以在目标服务器上提供管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="4914f-119">Yes, if the user who will deploy the content can supply the credentials of an administrator on the destination server.</span></span> <span data-ttu-id="4914f-120">此方法在以下类型的方案中通常是必需的：</span><span class="sxs-lookup"><span data-stu-id="4914f-120">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="4914f-121">开发或测试环境，开发人员可以完全控制目标 web 服务器和数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="4914f-121">Development or test environments, where the developer has full control over the destination web server and database server.</span></span>
- <span data-ttu-id="4914f-122">小型组织，其中单个用户或一小组用户可以控制整个应用程序生命周期。</span><span class="sxs-lookup"><span data-stu-id="4914f-122">Smaller organizations in which a single user or a small group of users has control over the entire application lifecycle.</span></span>

<span data-ttu-id="4914f-123">在许多大型组织中，特别是在过渡环境或生产环境中，向用户授予对 web 服务器的管理员权限通常是不现实的。</span><span class="sxs-lookup"><span data-stu-id="4914f-123">In lots of larger organizations, and particularly for staging or production environments, it's often not realistic to give users administrator rights on web servers.</span></span> <span data-ttu-id="4914f-124">对于托管的 web 服务器，这种情况尤其不可能出现。</span><span class="sxs-lookup"><span data-stu-id="4914f-124">In the case of hosted web servers, this is especially unlikely to be the case.</span></span> <span data-ttu-id="4914f-125">此外，如果计划从生成服务器自动进行部署，则可能不希望使用管理员凭据来完成部署过程。</span><span class="sxs-lookup"><span data-stu-id="4914f-125">In addition, if you're planning to automate deployment from a build server, you may not want to use administrator credentials for the deployment process.</span></span> <span data-ttu-id="4914f-126">在这些情况下，将 web 服务器配置为支持使用[Web 部署处理程序](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)的部署可能会提供更好的选择。</span><span class="sxs-lookup"><span data-stu-id="4914f-126">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Handler](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) may provide a more satisfactory choice.</span></span>

## <a name="task-overview"></a><span data-ttu-id="4914f-127">任务概述</span><span class="sxs-lookup"><span data-stu-id="4914f-127">Task Overview</span></span>

<span data-ttu-id="4914f-128">本主题说明如何使用 Web 部署远程代理方法将 Internet Information Services （IIS） 7.5 web 服务器配置为接受和部署远程计算机上的 web 包。</span><span class="sxs-lookup"><span data-stu-id="4914f-128">This topic describes how to configure an Internet Information Services (IIS) 7.5 web server to accept and deploy web packages from a remote computer using the Web Deploy Remote Agent approach.</span></span> <span data-ttu-id="4914f-129">你需要：</span><span class="sxs-lookup"><span data-stu-id="4914f-129">You'll need to:</span></span>

- <span data-ttu-id="4914f-130">安装 IIS 7.5 和 IIS 7 建议的配置。</span><span class="sxs-lookup"><span data-stu-id="4914f-130">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="4914f-131">安装 Web 部署2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4914f-131">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="4914f-132">创建一个 IIS 网站来托管已部署的内容。</span><span class="sxs-lookup"><span data-stu-id="4914f-132">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="4914f-133">确保 Web 部署代理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="4914f-133">Ensure that the Web Deployment Agent Service is running.</span></span>

<span data-ttu-id="4914f-134">若要专门托管示例解决方案，还需要：</span><span class="sxs-lookup"><span data-stu-id="4914f-134">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="4914f-135">安装 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="4914f-135">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="4914f-136">安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="4914f-136">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="4914f-137">本主题将演示如何执行上述每个过程。</span><span class="sxs-lookup"><span data-stu-id="4914f-137">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="4914f-138">本主题中的任务和演练假设你开始使用运行 Windows Server 2008 R2 的干净服务器版本。</span><span class="sxs-lookup"><span data-stu-id="4914f-138">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="4914f-139">继续之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="4914f-139">Before you continue, ensure that:</span></span>

- <span data-ttu-id="4914f-140">Windows Server 2008 R2 Service Pack 1 和所有可用更新均已安装。</span><span class="sxs-lookup"><span data-stu-id="4914f-140">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="4914f-141">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="4914f-141">The server is domain-joined.</span></span>
- <span data-ttu-id="4914f-142">服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="4914f-142">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="4914f-143">有关将计算机加入域的详细信息，请参阅将[计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="4914f-143">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="4914f-144">有关配置静态 IP 地址的详细信息，请参阅[配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="4914f-144">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="4914f-145">远程代理服务支持 IIS 6，无需加入到域。</span><span class="sxs-lookup"><span data-stu-id="4914f-145">The Remote Agent service is supported by IIS 6 onwards and does not require you to be joined to a domain.</span></span> <span data-ttu-id="4914f-146">不过，本教程中的步骤是在 IIS 7.5 上进行开发和测试的，其他版本的过程可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="4914f-146">However, the steps in this tutorial were developed and tested on IIS 7.5 and procedures for other versions may vary.</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="4914f-147">安装产品和组件</span><span class="sxs-lookup"><span data-stu-id="4914f-147">Install Products and Components</span></span>

<span data-ttu-id="4914f-148">本部分将指导你完成在 web 服务器上安装所需的产品和组件。</span><span class="sxs-lookup"><span data-stu-id="4914f-148">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="4914f-149">在开始之前，好的做法是运行 Windows 更新以确保服务器完全处于最新状态。</span><span class="sxs-lookup"><span data-stu-id="4914f-149">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="4914f-150">在这种情况下，需要安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="4914f-150">In this case, you need to install these things:</span></span>

- <span data-ttu-id="4914f-151">**IIS 7 建议的配置**。</span><span class="sxs-lookup"><span data-stu-id="4914f-151">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="4914f-152">这将在你的 web 服务器上启用**Web 服务器（IIS）** 角色，并安装用于托管 ASP.NET 应用程序的 IIS 模块和组件集。</span><span class="sxs-lookup"><span data-stu-id="4914f-152">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="4914f-153">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="4914f-153">**.NET Framework 4.0**.</span></span> <span data-ttu-id="4914f-154">这是运行在此版本的 .NET Framework 上构建的应用程序所必需的。</span><span class="sxs-lookup"><span data-stu-id="4914f-154">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="4914f-155">**Web 部署工具2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="4914f-155">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="4914f-156">这会在服务器上安装 Web 部署（及其基础可执行文件）。</span><span class="sxs-lookup"><span data-stu-id="4914f-156">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="4914f-157">在此过程中，它将安装并启动 Web 部署代理服务。</span><span class="sxs-lookup"><span data-stu-id="4914f-157">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="4914f-158">此服务允许你从远程计算机部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="4914f-158">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="4914f-159">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="4914f-159">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="4914f-160">这将安装运行 MVC 3 应用程序所需的程序集。</span><span class="sxs-lookup"><span data-stu-id="4914f-160">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="4914f-161">本演练介绍了如何使用 Web 平台安装程序来安装和配置所需的组件。</span><span class="sxs-lookup"><span data-stu-id="4914f-161">This walkthrough describes the use of the Web Platform Installer to install and configure the required components.</span></span> <span data-ttu-id="4914f-162">尽管无需使用 Web 平台安装程序，但它可以通过自动检测依赖项并确保始终获取最新的产品版本来简化安装过程。</span><span class="sxs-lookup"><span data-stu-id="4914f-162">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="4914f-163">有关详细信息，请参阅[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="4914f-163">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="4914f-164">**安装所需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="4914f-164">**To install the required products and components**</span></span>

1. <span data-ttu-id="4914f-165">下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="4914f-165">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="4914f-166">安装完成后，Web 平台安装程序将自动启动。</span><span class="sxs-lookup"><span data-stu-id="4914f-166">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4914f-167">你现在可以从 "**开始**" 菜单启动 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="4914f-167">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="4914f-168">为此，请在 "**开始**" 菜单上，单击 "**所有程序**"，然后单击 " **Microsoft Web 平台安装程序**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-168">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="4914f-169">在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-169">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="4914f-170">在窗口左侧的导航窗格中，单击 "**框架**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-170">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="4914f-171">在**Microsoft .NET Framework 4** "行中，如果尚未安装 .NET Framework，请单击"**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-171">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4914f-172">可能已通过 Windows 更新安装 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="4914f-172">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="4914f-173">如果产品或组件已安装，Web 平台安装程序将通过将 "**添加**" 按钮替换为**安装**的文本来指示这一点。</span><span class="sxs-lookup"><span data-stu-id="4914f-173">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. <span data-ttu-id="4914f-174">在**ASP.NET MVC 3 （Visual Studio 2010）** 行中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-174">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="4914f-175">在导航窗格中，单击 "**服务器**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-175">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="4914f-176">在 " **IIS 7 推荐的配置**" 行中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-176">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="4914f-177">在**Web 部署工具 2.1**行中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-177">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="4914f-178">单击“安装”。</span><span class="sxs-lookup"><span data-stu-id="4914f-178">Click **Install**.</span></span> <span data-ttu-id="4914f-179">Web 平台安装程序将显示产品&#x2014;列表以及要安装的任何关联依赖关系&#x2014;，并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="4914f-179">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. <span data-ttu-id="4914f-180">查看许可条款，如果同意条款，请单击 "**我接受**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-180">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="4914f-181">安装完成后，单击 "**完成**"，然后关闭 " **Web 平台安装程序 3.0** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="4914f-181">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="4914f-182">如果在安装 IIS 之前安装了 .NET Framework 4.0，则需要运行[ASP.NET Iis 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)（aspnet\_regiis），以将最新版本的 ASP.NET 注册到 iis。</span><span class="sxs-lookup"><span data-stu-id="4914f-182">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="4914f-183">如果不这样做，你会发现 IIS 将提供静态内容（如 HTML 文件），而不会有任何问题，但当你尝试浏览到 ASP.NET 内容时，它将返回**HTTP 错误404.0 –找不**到。</span><span class="sxs-lookup"><span data-stu-id="4914f-183">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="4914f-184">您可以使用此过程来确保 ASP.NET 4.0 已注册。</span><span class="sxs-lookup"><span data-stu-id="4914f-184">You can use this procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="4914f-185">**向 IIS 注册 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="4914f-185">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="4914f-186">单击 "**开始**"，然后键入**命令提示符**。</span><span class="sxs-lookup"><span data-stu-id="4914f-186">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="4914f-187">在搜索结果中，右键单击 "**命令提示符**"，然后单击 "**以管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-187">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="4914f-188">在命令提示符窗口中，导航到 " **%windir%\microsoft.net\framework\v4.0.30319 (对于**" 目录。</span><span class="sxs-lookup"><span data-stu-id="4914f-188">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="4914f-189">键入以下命令，然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="4914f-189">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. <span data-ttu-id="4914f-190">如果你打算随时托管64位 web 应用程序，则还应将 ASP.NET 的64位版本注册到 IIS。</span><span class="sxs-lookup"><span data-stu-id="4914f-190">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="4914f-191">为此，请在命令提示符窗口中导航到 **%windir%\microsoft.net\framework64\v4.0.30319 (对于**目录。</span><span class="sxs-lookup"><span data-stu-id="4914f-191">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="4914f-192">键入以下命令，然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="4914f-192">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

<span data-ttu-id="4914f-193">作为一种很好的做法，请再次使用 Windows 更新，下载并安装适用于已安装的新产品和组件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="4914f-193">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="4914f-194">配置 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="4914f-194">Configure the IIS Website</span></span>

<span data-ttu-id="4914f-195">你需要创建并配置一个 IIS 网站来托管内容，然后才能将 web 内容部署到你的服务器。</span><span class="sxs-lookup"><span data-stu-id="4914f-195">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="4914f-196">Web 部署只能将 web 包部署到现有 IIS 网站;它无法为你创建网站。</span><span class="sxs-lookup"><span data-stu-id="4914f-196">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="4914f-197">在高级别上，需要完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="4914f-197">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="4914f-198">在文件系统上创建一个文件夹以托管你的内容。</span><span class="sxs-lookup"><span data-stu-id="4914f-198">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="4914f-199">创建一个 IIS 网站来提供内容，并将其与本地文件夹关联。</span><span class="sxs-lookup"><span data-stu-id="4914f-199">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="4914f-200">向本地文件夹上的应用程序池标识授予读取权限。</span><span class="sxs-lookup"><span data-stu-id="4914f-200">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="4914f-201">尽管不会阻止你将内容部署到 IIS 中的默认网站，但对于除测试或演示方案之外的任何内容，不建议使用此方法。</span><span class="sxs-lookup"><span data-stu-id="4914f-201">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="4914f-202">若要模拟生产环境，应该创建一个新的 IIS 网站，其中包含特定于应用程序要求的设置。</span><span class="sxs-lookup"><span data-stu-id="4914f-202">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="4914f-203">**创建和配置 IIS 网站**</span><span class="sxs-lookup"><span data-stu-id="4914f-203">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="4914f-204">在本地文件系统上，创建用于存储内容的文件夹（例如， **C:\DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="4914f-204">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="4914f-205">在 "**开始**" 菜单上，指向 "**管理工具**"，然后单击 " **Internet Information Services （IIS）管理器**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-205">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="4914f-206">在 IIS 管理器的 "**连接**" 窗格中，展开服务器节点（例如， **TESTWEB1**）。</span><span class="sxs-lookup"><span data-stu-id="4914f-206">In IIS Manager, in the **Connections** pane, expand the server node (for example, **TESTWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. <span data-ttu-id="4914f-207">右键单击 "**站点**" 节点，然后单击 "**添加网站**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-207">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="4914f-208">在 "**站点名称**" 框中，键入 IIS 网站的名称（例如， **DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="4914f-208">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="4914f-209">在 "**物理路径**" 框中，键入（或浏览到）本地文件夹的路径（例如， **C:\DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="4914f-209">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="4914f-210">在 "**端口**" 框中，键入要在其上托管网站的端口号（例如， **85**）。</span><span class="sxs-lookup"><span data-stu-id="4914f-210">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4914f-211">对于 HTTP，标准端口号为80，对于 HTTPS 则为443。</span><span class="sxs-lookup"><span data-stu-id="4914f-211">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="4914f-212">但是，如果你在端口80上托管此网站，你将需要停止默认网站，然后才能访问你的站点。</span><span class="sxs-lookup"><span data-stu-id="4914f-212">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="4914f-213">将 "**主机名**" 框保留为空，除非你想要为网站配置域名系统（DNS）记录，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="4914f-213">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="4914f-214">在生产环境中，你可能想要在端口80上托管你的网站，并配置主机标头和匹配的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="4914f-214">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="4914f-215">有关在 IIS 7 中配置主机标头的详细信息，请参阅[配置网站的主机标头（IIS 7）](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="4914f-215">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="4914f-216">有关 Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅[Dns 服务器概述](https://technet.microsoft.com/library/cc770392.aspx)和[dns 服务器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="4914f-216">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="4914f-217">在 "**操作**" 窗格中的 "**编辑站点**" 下，单击 "**绑定**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-217">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="4914f-218">在 "**站点绑定**" 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-218">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. <span data-ttu-id="4914f-219">在 "**添加站点绑定**" 对话框中，将 " **IP 地址**" 和 "**端口**" 设置为与现有站点配置匹配。</span><span class="sxs-lookup"><span data-stu-id="4914f-219">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="4914f-220">在 "**主机名**" 框中，键入 web 服务器的名称（例如， **TESTWEB1**），然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="4914f-220">In the **Host name** box, type the name of your web server (for example, **TESTWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="4914f-221">第一个站点绑定允许使用 IP 地址和端口或 `http://localhost:85`本地访问站点。</span><span class="sxs-lookup"><span data-stu-id="4914f-221">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="4914f-222">第二个站点绑定允许使用计算机名称（例如 http://testweb1:85) ，从域中的其他计算机访问站点。</span><span class="sxs-lookup"><span data-stu-id="4914f-222">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://testweb1:85).</span></span>
13. <span data-ttu-id="4914f-223">在 "**站点绑定**" 对话框中，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-223">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="4914f-224">在 "**连接**" 窗格中，单击 "**应用程序池**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-224">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="4914f-225">在 "**应用程序池**" 窗格中，右键单击应用程序池的名称，然后单击 "**基本设置**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-225">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="4914f-226">默认情况下，应用程序池的名称将与网站的名称匹配（例如， **DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="4914f-226">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="4914f-227">在 **.NET Framework 版本**"列表中，选择" **.NET Framework v 4.0.30319**"，然后单击 **" 确定 "** 。</span><span class="sxs-lookup"><span data-stu-id="4914f-227">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="4914f-228">示例解决方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="4914f-228">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="4914f-229">这并不是对 Web 部署一般的要求。</span><span class="sxs-lookup"><span data-stu-id="4914f-229">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="4914f-230">为了使你的网站提供内容，应用程序池标识必须对存储内容的本地文件夹具有读取权限。</span><span class="sxs-lookup"><span data-stu-id="4914f-230">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="4914f-231">在 IIS 7.5 中，应用程序池默认使用唯一的应用程序池标识运行（与以前版本的 IIS 不同，应用程序池通常使用 Network Service 帐户运行）。</span><span class="sxs-lookup"><span data-stu-id="4914f-231">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="4914f-232">应用程序池标识不是真实的用户帐户，并且不会显示在任何用户或组&#x2014;的列表中，而是在启动应用程序池时动态创建。</span><span class="sxs-lookup"><span data-stu-id="4914f-232">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="4914f-233">每个应用程序池标识都作为隐藏项添加到本地**IIS\_iis-iusrs**安全组。</span><span class="sxs-lookup"><span data-stu-id="4914f-233">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="4914f-234">若要授予对文件或文件夹上的应用程序池标识的权限，可以使用两个选项：</span><span class="sxs-lookup"><span data-stu-id="4914f-234">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="4914f-235">使用 IIS AppPool\</strong ><em>[应用程序池名称]</em>（例如<strong>IIS AppPool\DemoSite</strong>）的 <strong>格式，直接将权限分配给应用程序池标识。</span><span class="sxs-lookup"><span data-stu-id="4914f-235">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="4914f-236">将权限分配给**IIS\_iis-iusrs**组。</span><span class="sxs-lookup"><span data-stu-id="4914f-236">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="4914f-237">最常见的方法是将权限分配给本地**IIS\_iis-iusrs**组，因为此方法允许你在不重新配置文件系统权限的情况下更改应用程序池。</span><span class="sxs-lookup"><span data-stu-id="4914f-237">The most common approach is to assign permissions to the local **IIS\_IUSRS** group because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="4914f-238">下一过程使用此基于组的方法。</span><span class="sxs-lookup"><span data-stu-id="4914f-238">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="4914f-239">有关 IIS 7.5 中的应用程序池标识的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="4914f-239">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="4914f-240">**配置 IIS 网站的文件夹权限**</span><span class="sxs-lookup"><span data-stu-id="4914f-240">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="4914f-241">在 Windows 资源管理器中，浏览到本地文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="4914f-241">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="4914f-242">右键单击该文件夹，然后单击 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-242">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="4914f-243">在 "**安全**" 选项卡上，单击 "**编辑**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-243">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="4914f-244">单击 "**位置**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-244">Click **Locations**.</span></span> <span data-ttu-id="4914f-245">在 "**位置**" 对话框中，选择本地服务器，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="4914f-245">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. <span data-ttu-id="4914f-246">在 "**选择用户或组**" 对话框中，键入**IIS\_Iis-iusrs**，单击 "**检查名称**"，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="4914f-246">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="4914f-247">在 "<em>[文件夹名称]</em>的权限" 对话框中，请注意，默认情况下已为新组分配 "<strong>读取 &amp; 执行</strong>"、"<strong>列出文件夹内容</strong>" 和 "<strong>读取</strong>" 权限。</span><span class="sxs-lookup"><span data-stu-id="4914f-247">In the <strong>Permissions for</strong><em>[folder name]</em>dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="4914f-248">保持不变，并单击<strong>"确定"</strong>。</span><span class="sxs-lookup"><span data-stu-id="4914f-248">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="4914f-249">单击<strong>"确定"</strong>以关闭 " <em>[文件夹名称]</em><strong>属性</strong>" 对话框。</span><span class="sxs-lookup"><span data-stu-id="4914f-249">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

<span data-ttu-id="4914f-250">作为最终任务，在尝试将任何 web 包部署到服务器之前，应确保 Web 部署代理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="4914f-250">As a final task before you attempt to deploy any web packages to your server, you should ensure that the Web Deployment Agent Service is running.</span></span> <span data-ttu-id="4914f-251">从远程计算机部署包时，Web 部署代理服务负责提取和安装包的内容。</span><span class="sxs-lookup"><span data-stu-id="4914f-251">When you deploy a package from a remote computer, the Web Deployment Agent Service is responsible for extracting and installing the contents of the package.</span></span> <span data-ttu-id="4914f-252">默认情况下，当你安装 Web 部署工具并在网络服务标识下运行时，将启动该服务。</span><span class="sxs-lookup"><span data-stu-id="4914f-252">The service is started by default when you install the Web Deployment Tool and runs under the Network Service identity.</span></span>

<span data-ttu-id="4914f-253">你可以使用各种命令行实用工具或 Windows PowerShell cmdlet 来检查服务是否以多种不同的方式运行。</span><span class="sxs-lookup"><span data-stu-id="4914f-253">You can check whether a service is running in multiple different ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="4914f-254">此过程描述了一个简单的基于 UI 的方法。</span><span class="sxs-lookup"><span data-stu-id="4914f-254">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="4914f-255">**检查 Web 部署代理服务是否正在运行**</span><span class="sxs-lookup"><span data-stu-id="4914f-255">**To check that the Web Deployment Agent Service is running**</span></span>

1. <span data-ttu-id="4914f-256">在“开始” 菜单上，指向“管理工具”，然后单击“服务”。</span><span class="sxs-lookup"><span data-stu-id="4914f-256">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="4914f-257">找到 " **Web 部署代理服务**" 行，然后验证 "**状态**" 是否设置为 "**已启动**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-257">Locate the **Web Deployment Agent Service** row, and verify that the **Status** is set to **Started**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. <span data-ttu-id="4914f-258">如果该服务尚未启动，则单击 "**启动**"。</span><span class="sxs-lookup"><span data-stu-id="4914f-258">If the service is not already started, click **Start**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="4914f-259">配置防火墙例外</span><span class="sxs-lookup"><span data-stu-id="4914f-259">Configure Firewall Exceptions</span></span>

<span data-ttu-id="4914f-260">默认情况下，远程代理服务在 TCP 端口80上侦听，网址为：</span><span class="sxs-lookup"><span data-stu-id="4914f-260">By default, the Remote Agent Service listens on TCP port 80, at this URL:</span></span>

<http://servername.com/MSDEPLOYAGENTSERVICE>

<span data-ttu-id="4914f-261">在大多数情况下，你无需为远程代理服务配置任何其他防火墙规则，因为 web 服务器通常在端口80上侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="4914f-261">In most cases, you won't need to configure any additional firewall rules for the Remote Agent Service because web servers typically listen for HTTP requests on port 80.</span></span> <span data-ttu-id="4914f-262">如果自定义安装以侦听非标准端口，则需要根据需要配置防火墙例外。</span><span class="sxs-lookup"><span data-stu-id="4914f-262">If you customized your installation to listen on a nonstandard port, you'll need to configure firewall exceptions as required.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4914f-263">结束语</span><span class="sxs-lookup"><span data-stu-id="4914f-263">Conclusion</span></span>

<span data-ttu-id="4914f-264">此时，web 服务器已准备好接受并安装远程计算机上的 web 包。</span><span class="sxs-lookup"><span data-stu-id="4914f-264">At this point, your web server is ready to accept and install web packages from a remote computer.</span></span> <span data-ttu-id="4914f-265">尝试将 web 应用程序部署到服务器之前，可能需要检查以下要点：</span><span class="sxs-lookup"><span data-stu-id="4914f-265">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="4914f-266">是否已向 IIS 注册 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="4914f-266">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="4914f-267">应用程序池标识是否具有对你的网站的源文件夹的 "读取" 访问权限？</span><span class="sxs-lookup"><span data-stu-id="4914f-267">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="4914f-268">Web 部署代理服务是否正在运行？</span><span class="sxs-lookup"><span data-stu-id="4914f-268">Is the Web Deployment Agent Service running?</span></span>

## <a name="further-reading"></a><span data-ttu-id="4914f-269">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="4914f-269">Further Reading</span></span>

<span data-ttu-id="4914f-270">有关如何配置自定义 Microsoft 生成引擎（MSBuild）项目文件以将 web 包部署到远程代理服务的指南，请参阅[配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="4914f-270">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Remote Agent Service, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4914f-271">[上一页](scenario-configuring-a-production-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span><span class="sxs-lookup"><span data-stu-id="4914f-271">[Previous](scenario-configuring-a-production-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span></span>
