---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署到测试 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591241"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="e148a-103">使用 Visual Studio 的 ASP.NET Web 部署：部署到测试</span><span class="sxs-lookup"><span data-stu-id="e148a-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>

<span data-ttu-id="e148a-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e148a-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="e148a-105">本系列教程演示如何使用 Visual Studio 2017 将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="e148a-105">This tutorial series shows how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider using Visual Studio 2017.</span></span> <span data-ttu-id="e148a-106">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e148a-106">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="e148a-107">有关部署到 Azure 的当前版本，请参阅[在 azure 中创建 ASP.NET Core web 应用](/azure/app-service/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="e148a-107">For a current version of deploying to Azure, see [Create an ASP.NET Core web app in Azure](/azure/app-service/app-service-web-get-started-dotnet).</span></span>

## <a name="overview"></a><span data-ttu-id="e148a-108">概述</span><span class="sxs-lookup"><span data-stu-id="e148a-108">Overview</span></span>

<span data-ttu-id="e148a-109">在本教程中，将 ASP.NET web 应用程序部署到本地计算机上的 Internet Information Server （IIS）。</span><span class="sxs-lookup"><span data-stu-id="e148a-109">In this tutorial, you'll deploy an ASP.NET web application to Internet Information Server (IIS) on your local computer.</span></span>

<span data-ttu-id="e148a-110">通常，在开发应用程序时，在 Visual Studio 中运行应用程序并对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="e148a-110">Generally when you develop an application, you run it and test it in Visual Studio.</span></span> <span data-ttu-id="e148a-111">默认情况下，Visual Studio 2017 中的 web 应用程序项目将 IIS Express 用作开发 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="e148a-111">By default, web application projects in Visual Studio 2017 use IIS Express as the development web server.</span></span> <span data-ttu-id="e148a-112">IIS Express 的行为与 Visual Studio 开发服务器（也称为 Cassini）完全相同，Visual Studio 2017 默认情况下使用。</span><span class="sxs-lookup"><span data-stu-id="e148a-112">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2017 uses by default.</span></span> <span data-ttu-id="e148a-113">但是，开发 web 服务器的工作方式与 IIS 完全相同。</span><span class="sxs-lookup"><span data-stu-id="e148a-113">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="e148a-114">因此，应用可以在 Visual Studio 中正确运行和测试，但在将其部署到 IIS 时将失败。</span><span class="sxs-lookup"><span data-stu-id="e148a-114">Consequently, an app could run and test correctly in Visual Studio but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="e148a-115">可以通过两种方式可靠地测试应用程序：</span><span class="sxs-lookup"><span data-stu-id="e148a-115">You can reliably test your application in two ways:</span></span>

1. <span data-ttu-id="e148a-116">使用你稍后将应用程序部署到生产环境时将使用的相同过程，将你的应用程序部署到你的开发计算机上的 IIS。</span><span class="sxs-lookup"><span data-stu-id="e148a-116">Deploy your application to IIS on your development computer using the same process that you'll use later to deploy it to your production environment.</span></span>

   <span data-ttu-id="e148a-117">你可以将 Visual Studio 配置为在运行 web 项目时使用 IIS，但不会测试你的部署过程。</span><span class="sxs-lookup"><span data-stu-id="e148a-117">You can configure Visual Studio to use IIS when you run a web project, but that wouldn't test your deployment process.</span></span> <span data-ttu-id="e148a-118">此方法验证你的部署过程，并且你的应用程序在 IIS 下正常运行。</span><span class="sxs-lookup"><span data-stu-id="e148a-118">This method validates your deployment process and that your application runs correctly under IIS.</span></span>

2. <span data-ttu-id="e148a-119">将应用程序部署到类似于生产环境的测试环境。</span><span class="sxs-lookup"><span data-stu-id="e148a-119">Deploy your application to a test environment similar to your production environment.</span></span> 
 
   <span data-ttu-id="e148a-120">这些教程的生产环境是 Azure App Service 中的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="e148a-120">The production environment for these tutorials is Web Apps in Azure App Service.</span></span> <span data-ttu-id="e148a-121">理想的测试环境是在 Azure 服务中创建的其他 web 应用。</span><span class="sxs-lookup"><span data-stu-id="e148a-121">The ideal test environment is an additional web app created in the Azure Service.</span></span> <span data-ttu-id="e148a-122">尽管设置的方式与生产 web 应用相同，但只是将其用于测试。</span><span class="sxs-lookup"><span data-stu-id="e148a-122">Though it would be set up the same way as a production web app, you would only use it for testing.</span></span>

<span data-ttu-id="e148a-123">选项2是最可靠的测试方法。</span><span class="sxs-lookup"><span data-stu-id="e148a-123">Option 2 is the most reliable way to test.</span></span> <span data-ttu-id="e148a-124">如果使用选项2，则不一定需要使用选项1。</span><span class="sxs-lookup"><span data-stu-id="e148a-124">If you use option 2, you don't necessarily need to use option 1.</span></span> <span data-ttu-id="e148a-125">但是，如果要部署到第三方托管提供商，则选项2可能不可行或开销较大，因此本教程系列将显示这两种方法。</span><span class="sxs-lookup"><span data-stu-id="e148a-125">However if you're deploying to a third-party hosting provider, option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="e148a-126">[部署到生产环境](deploying-to-production.md)教程中提供了选项2的指南。</span><span class="sxs-lookup"><span data-stu-id="e148a-126">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="e148a-127">有关在 Visual Studio 中使用 web 服务器的详细信息，请参阅[Visual studio for ASP.NET Web 项目中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e148a-127">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="e148a-128">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="e148a-128">Reminder: If you receive an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="download-the-contoso-university-starter-project"></a><span data-ttu-id="e148a-129">下载 Contoso 大学初学者项目</span><span class="sxs-lookup"><span data-stu-id="e148a-129">Download the Contoso University starter project</span></span>

<span data-ttu-id="e148a-130">下载并安装 Contoso 大学 Visual Studio starter 解决方案和项目。</span><span class="sxs-lookup"><span data-stu-id="e148a-130">Download and install the Contoso University Visual Studio starter solution and project.</span></span> <span data-ttu-id="e148a-131">此解决方案包含已完成的教程。</span><span class="sxs-lookup"><span data-stu-id="e148a-131">This solution contains the completed tutorial.</span></span> 

[<span data-ttu-id="e148a-132">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="e148a-132">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a><span data-ttu-id="e148a-133">安装 IIS</span><span class="sxs-lookup"><span data-stu-id="e148a-133">Install IIS</span></span>

<span data-ttu-id="e148a-134">若要在开发计算机上部署到 IIS，请确认已安装 IIS 和 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="e148a-134">To deploy to IIS on your development computer, confirm that IIS and Web Deploy are installed.</span></span> <span data-ttu-id="e148a-135">默认情况下，Visual Studio 会安装 Web 部署，但 IIS 不包含在默认的 Windows 10、Windows 8 或 Windows 7 配置中。</span><span class="sxs-lookup"><span data-stu-id="e148a-135">By default, Visual Studio installs Web Deploy, but IIS isn't included in the default Windows 10, Windows 8, or Windows 7 configuration.</span></span> <span data-ttu-id="e148a-136">如果已安装 IIS 并且默认应用程序池已设置为 .NET 4，请跳到[下一部分](#sqlexpress)。</span><span class="sxs-lookup"><span data-stu-id="e148a-136">If you've already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="e148a-137">建议使用[Web 平台安装程序（WPI）](https://www.microsoft.com/web/downloads/platform.aspx)安装 IIS 和 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="e148a-137">It's recommended you use the [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx) to install IIS and Web Deploy.</span></span> <span data-ttu-id="e148a-138">WPI 安装建议的 IIS 配置，其中包括 IIS 和 Web 部署先决条件（如有必要）。</span><span class="sxs-lookup"><span data-stu-id="e148a-138">WPI installs a recommended IIS configuration that includes IIS and Web Deploy prerequisites if necessary.</span></span>

   <span data-ttu-id="e148a-139">如果你已经安装了 IIS、Web 部署或任何所需的组件，则 WPI 仅安装缺少的内容。</span><span class="sxs-lookup"><span data-stu-id="e148a-139">If you've already installed IIS, Web Deploy, or any of their required components, the WPI installs only what is missing.</span></span>

   * <span data-ttu-id="e148a-140">使用 Web 平台安装程序安装 IIS 和 Web 部署：</span><span class="sxs-lookup"><span data-stu-id="e148a-140">Use the Web Platform Installer to install IIS and Web Deploy:</span></span>
    
     ![使用 WPI 安装 IIS](deploying-to-iis/_static/image30.png)

     ![使用 WPI 安装 Web 部署](deploying-to-iis/_static/image31.png)

     <span data-ttu-id="e148a-143">你将看到指示将安装 IIS 7 的消息。</span><span class="sxs-lookup"><span data-stu-id="e148a-143">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="e148a-144">该链接适用于 Windows 8 中的 IIS 8;但对于 Windows 8 及更高版本，请执行以下步骤，确保安装了 ASP.NET 4.7：</span><span class="sxs-lookup"><span data-stu-id="e148a-144">The link works for IIS 8 in Windows 8; but for Windows 8 and later, go through the following steps to make sure that ASP.NET 4.7 is installed:</span></span>

   * <span data-ttu-id="e148a-145">打开 **"控制面板"**  > **程序**" > "**程序和功能 "，**  > **启用或禁用 Windows 功能**。</span><span class="sxs-lookup"><span data-stu-id="e148a-145">Open **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off**.</span></span>

   * <span data-ttu-id="e148a-146">展开**Internet Information Services**、 **World Wide Web 服务**和**应用程序开发功能**。</span><span class="sxs-lookup"><span data-stu-id="e148a-146">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   
   * <span data-ttu-id="e148a-147">确认已选中 " **ASP.NET 4.7** "。</span><span class="sxs-lookup"><span data-stu-id="e148a-147">Confirm that **ASP.NET 4.7** is selected.</span></span>

     ![选择 ASP.NET 4。7](deploying-to-iis/_static/image1a.png)

   * <span data-ttu-id="e148a-149">确认已选择 "**万维网服务**和**IIS 管理控制台**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-149">Confirm that **World Wide Web Services** and **IIS Management Console** is selected.</span></span> <span data-ttu-id="e148a-150">这会安装 IIS 和 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="e148a-150">This installs IIS and IIS Manager.</span></span>
    
     ![选择 "万维网服务"](deploying-to-iis/_static/image24.png)    
  
   * <span data-ttu-id="e148a-152">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e148a-152">Select **OK**.</span></span> <span data-ttu-id="e148a-153">显示指示安装正在进行的对话框消息。</span><span class="sxs-lookup"><span data-stu-id="e148a-153">Dialog box messages indicating installation is taking place appear.</span></span>

<span data-ttu-id="e148a-154">安装 IIS 后，请运行**Iis 管理器**以确保将 .NET Framework 版本4分配给默认应用程序池。</span><span class="sxs-lookup"><span data-stu-id="e148a-154">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="e148a-155">按 WINDOWS + R 打开 "**运行**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="e148a-155">Press WINDOWS+R to open the **Run** dialog box.</span></span>

   <span data-ttu-id="e148a-156">（在 Windows 8 或更高版本上，在 "**开始**" 页上输入 "运行"。</span><span class="sxs-lookup"><span data-stu-id="e148a-156">(On Windows 8 or later, enter "run" on the **Start** page.</span></span> <span data-ttu-id="e148a-157">在 Windows 7 中，从 "**开始**" 菜单中选择 "**运行**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-157">In Windows 7, select **Run** from the **Start** menu.</span></span> <span data-ttu-id="e148a-158">如果 "**开始**" 菜单中没有 "**运行**"，请右键单击任务栏，选择 "**属性**"，选择 "**开始" 菜单**选项卡，选择 "**自定义**"，然后选择 "**运行命令**"。）</span><span class="sxs-lookup"><span data-stu-id="e148a-158">If **Run** isn't in the **Start** menu, right-click the taskbar, select **Properties**, select the **Start Menu** tab, select **Customize**, and select **Run command**.)</span></span>

2. <span data-ttu-id="e148a-159">输入 "inetmgr"，然后选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-159">Enter "inetmgr" and select **OK**.</span></span>

3. <span data-ttu-id="e148a-160">在 "**连接**" 窗格中，展开服务器节点，然后选择 "**应用程序池**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-160">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="e148a-161">如果将**DefaultAppPool**分配给 .net framework 版本4（如下图所示），请在 "**应用程序池**" 窗格中跳到下一部分。</span><span class="sxs-lookup"><span data-stu-id="e148a-161">In the **Application Pools** pane if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

   ![Inetmgr_showing_4. 0_app_pools](deploying-to-iis/_static/image5a.png)

4. <span data-ttu-id="e148a-163">如果只看到两个应用程序池，并且两者都设置为 .NET Framework 2.0，请在 IIS 中安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="e148a-163">If you see only two application pools and both are set to .NET Framework 2.0, install ASP.NET 4 in IIS.</span></span>

   <span data-ttu-id="e148a-164">对于 Windows 8 或更高版本，请参阅上一节说明，以确保已安装 ASP.NET 4.7，或参阅[如何在 windows 8 和 Windows Server 2012 上安装 ASP.NET 4.5](https://support.microsoft.com/kb/2736284)。</span><span class="sxs-lookup"><span data-stu-id="e148a-164">For Windows 8 or later, see the previous section's instructions for making sure that ASP.NET 4.7 is installed or see [How to install ASP.NET 4.5 on Windows 8 and Windows Server 2012](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="e148a-165">对于 Windows 7，通过右键单击 Windows "**开始**" 菜单中的 "**命令提示符**" 并选择 "以**管理员身份运行**"，打开 "命令提示符" 窗口。</span><span class="sxs-lookup"><span data-stu-id="e148a-165">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="e148a-166">运行[aspnet\_regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx) ，使用以下命令在 IIS 中安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="e148a-166">Run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS using the following commands.</span></span> <span data-ttu-id="e148a-167">（在32位系统中，将 "Framework64" 替换为 "框架"。）</span><span class="sxs-lookup"><span data-stu-id="e148a-167">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   <span data-ttu-id="e148a-168">此命令为 .NET Framework 4 创建新的应用程序池，但默认应用程序池将保持设置为2.0。</span><span class="sxs-lookup"><span data-stu-id="e148a-168">This command creates new application pools for the .NET Framework 4, but the default application pool will remain set to 2.0.</span></span> <span data-ttu-id="e148a-169">正在将面向 .NET 4 的应用程序部署到该应用程序池，因此请将应用程序池更改为 .NET 4。</span><span class="sxs-lookup"><span data-stu-id="e148a-169">You're deploying an application that targets .NET 4 to that application pool, so change the application pool to .NET 4.</span></span>

5. <span data-ttu-id="e148a-170">如果关闭了**IIS 管理器**，请再次运行它，展开服务器节点，然后选择 "**应用程序池**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-170">If you closed **IIS Manager**, run it again, expand the server node, and select **Application Pools**.</span></span>

6. <span data-ttu-id="e148a-171">在 "**应用程序池**" 窗格中，选择 " **DefaultAppPool**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-171">In the **Application Pools** pane, select **DefaultAppPool**.</span></span> <span data-ttu-id="e148a-172">在 "**操作**" 窗格中，选择 "**基本设置**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-172">In the **Actions** pane, select **Basic Settings**.</span></span>

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. <span data-ttu-id="e148a-174">在 "**编辑应用程序池**" 对话框中，将 " **.net clr 版本**" 更改为 " **.net clr 4.0.30319**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-174">In the **Edit Application Pool** dialog box, change the **.NET CLR version** to **.NET CLR v4.0.30319**.</span></span> <span data-ttu-id="e148a-175">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e148a-175">Select **OK**.</span></span>

   ![Selecting_. NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

<span data-ttu-id="e148a-177">你现在可以将 web 应用程序发布到 IIS。</span><span class="sxs-lookup"><span data-stu-id="e148a-177">You're now ready to publish a web application to IIS.</span></span> <span data-ttu-id="e148a-178">但首先要创建用于测试的数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-178">First, however, create databases for testing.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="e148a-179">安装 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="e148a-179">Install SQL Server Express</span></span>

<span data-ttu-id="e148a-180">LocalDB 不适用于 IIS，因此测试环境必须安装 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="e148a-180">LocalDB isn't designed to work in IIS, so your test environment has to have SQL Server Express installed.</span></span> <span data-ttu-id="e148a-181">如果使用的是 Visual Studio 2010 SQL Server Express，则默认情况下已安装该程序。</span><span class="sxs-lookup"><span data-stu-id="e148a-181">If you're using Visual Studio 2010 SQL Server Express, it's already installed by default.</span></span> <span data-ttu-id="e148a-182">如果使用的是 Visual Studio 2012 或更高版本，请安装 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="e148a-182">If you're using Visual Studio 2012 or later, install SQL Server Express.</span></span>

<span data-ttu-id="e148a-183">若要安装 SQL Server Express，请从下载中心下载并安装它[： Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)。</span><span class="sxs-lookup"><span data-stu-id="e148a-183">To install SQL Server Express, download and install it from [Download Center: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express).</span></span> 

<span data-ttu-id="e148a-184">在 SQL Server 安装中心的第一页上，选择 "**新建 SQL Server 独立安装或向现有安装添加功能**"，并按照说明接受默认选择。</span><span class="sxs-lookup"><span data-stu-id="e148a-184">On the first page of the SQL Server Installation Center, select **New SQL Server stand-alone installation or add features to an existing installation** and follow the instructions accepting the default choices.</span></span> <span data-ttu-id="e148a-185">在安装向导中，接受默认设置。</span><span class="sxs-lookup"><span data-stu-id="e148a-185">In the installation wizard, accept the default settings.</span></span> <span data-ttu-id="e148a-186">有关安装选项的详细信息，请参阅安装[SQL Server 从安装向导（安装程序）](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e148a-186">For more information about installation options, see [Install SQL Server from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="e148a-187">为测试环境创建 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="e148a-187">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="e148a-188">Contoso 大学应用程序有两个数据库：</span><span class="sxs-lookup"><span data-stu-id="e148a-188">The Contoso University application has two databases:</span></span> 

1. <span data-ttu-id="e148a-189">成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="e148a-189">Membership database</span></span> 
2. <span data-ttu-id="e148a-190">应用程序数据库</span><span class="sxs-lookup"><span data-stu-id="e148a-190">Application database</span></span> 

<span data-ttu-id="e148a-191">您可以将这些数据库部署到两个不同的数据库或单个数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-191">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="e148a-192">组合它们会使数据库在它们之间的联接更为容易。</span><span class="sxs-lookup"><span data-stu-id="e148a-192">Combining them makes database joins between them easier.</span></span> 

<span data-ttu-id="e148a-193">如果要部署到第三方托管提供商，则托管计划还可能会为您提供组合的原因。</span><span class="sxs-lookup"><span data-stu-id="e148a-193">If you're deploying to a third-party hosting provider, your hosting plan might also give you a reason to combine them.</span></span> <span data-ttu-id="e148a-194">例如，提供程序可能会为多个数据库收取更多的费用，甚至可能甚至不允许多个数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-194">For example, the provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="e148a-195">在本教程中，你将在测试环境中部署到两个数据库，并部署到过渡环境和生产环境中的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-195">In this tutorial, you'll deploy to two databases in the test environment and to one database in the staging and production environments.</span></span>

<span data-ttu-id="e148a-196">在 Visual Studio 的 "**视图**" 菜单中，选择 "**服务器资源管理器**" （visual Web Developer 中的**数据库资源管理器**）。</span><span class="sxs-lookup"><span data-stu-id="e148a-196">From the **View** menu in Visual Studio, select **Server Explorer** (**Database Explorer** in Visual Web Developer).</span></span> <span data-ttu-id="e148a-197">右键单击 "**数据连接**"，然后选择 "**新建 SQL Server 数据库**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-197">Right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="e148a-199">在 "新建**SQL Server 数据库**" 对话框的 "**服务器名称**" 框中，输入 ".\SQLExpress"，在 "**新数据库名称**" 框中输入 "ContosoUniversity"。</span><span class="sxs-lookup"><span data-stu-id="e148a-199">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box.</span></span> <span data-ttu-id="e148a-200">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e148a-200">Select **OK**.</span></span>

![创建 aspnet-ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="e148a-202">按照相同的过程创建名为 `ContosoUniversity`的新 SQL Server Express School 数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-202">Follow the same procedure to create a new SQL Server Express School database named `ContosoUniversity`.</span></span>

<span data-ttu-id="e148a-203">**服务器资源管理器**显示两个新数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-203">**Server Explorer** shows the two new databases.</span></span>

![服务器资源管理器中的新数据库](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="e148a-205">为新数据库创建授予脚本</span><span class="sxs-lookup"><span data-stu-id="e148a-205">Create a grant script for the new databases</span></span>

<span data-ttu-id="e148a-206">当应用程序在开发计算机上的 IIS 中运行时，应用程序将使用默认应用程序池的凭据来访问数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-206">When the application runs in IIS on your development computer, the application uses the default application pool's credentials to access the database.</span></span> <span data-ttu-id="e148a-207">但是，默认情况下，应用程序池没有打开数据库的权限。</span><span class="sxs-lookup"><span data-stu-id="e148a-207">However, by default, the application pool doesn't have permission to open the databases.</span></span> <span data-ttu-id="e148a-208">这意味着需要运行脚本来授予该权限。</span><span class="sxs-lookup"><span data-stu-id="e148a-208">This means you need to run a script to grant that permission.</span></span> <span data-ttu-id="e148a-209">在本部分中，你将创建该脚本并稍后运行它，以确保应用程序在 IIS 中运行时可以打开数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-209">In this section, you'll create that script and run it later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="e148a-210">在文本编辑器中，将以下 SQL 命令复制到一个新文件中，并将其另存为*Grant .sql*。</span><span class="sxs-lookup"><span data-stu-id="e148a-210">In a text editor, copy the following SQL commands into a new file and save it as *Grant.sql*.</span></span> 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

<span data-ttu-id="e148a-211">在 Visual Studio 中，打开 Contoso 大学解决方案。</span><span class="sxs-lookup"><span data-stu-id="e148a-211">In Visual Studio, open the Contoso University solution.</span></span> <span data-ttu-id="e148a-212">右键单击该解决方案（不是项目之一），然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-212">Right-click the solution (not one of the projects), and select **Add**.</span></span> <span data-ttu-id="e148a-213">选择 "**现有项**"，浏览到*Grant*，然后将其打开。</span><span class="sxs-lookup"><span data-stu-id="e148a-213">Select **Existing Item**, browse to *Grant.sql*, and open it.</span></span>

> [!NOTE]
> <span data-ttu-id="e148a-214">此脚本旨在与 SQL Server Express 2012 或更高版本以及在本教程中指定的 windows 10、Windows 8 或 Windows 7 中的 IIS 设置一起使用。</span><span class="sxs-lookup"><span data-stu-id="e148a-214">This script is designed to work with SQL Server Express 2012 or later and with the IIS settings in Windows 10, Windows 8, or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="e148a-215">如果使用的是其他版本的 SQL Server 或 Windows，或者在计算机上以不同的方式设置 IIS，则可能需要对此脚本进行更改。</span><span class="sxs-lookup"><span data-stu-id="e148a-215">If you're using a different version of SQL Server or Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="e148a-216">有关 SQL Server 脚本的详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="e148a-216">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> <span data-ttu-id="e148a-217">**安全说明**此脚本向用户提供对在运行时访问数据库的 `db_owner` 权限，您将在生产环境中使用该权限。</span><span class="sxs-lookup"><span data-stu-id="e148a-217">**Security Note** This script gives `db_owner` permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="e148a-218">在某些情况下，你可能想要指定具有仅用于部署的完整数据库架构更新权限的用户，并为运行时指定仅拥有读取和写入数据权限的其他用户。</span><span class="sxs-lookup"><span data-stu-id="e148a-218">In some scenarios, you might want to specify a user that has full database schema update permissions only for deployment and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="e148a-219">有关详细信息，请参阅本教程后面的[查看自动的 Web.config 更改 Code First 迁移](#reviewingmigrations)。</span><span class="sxs-lookup"><span data-stu-id="e148a-219">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="e148a-220">在应用程序数据库中运行 grant 脚本</span><span class="sxs-lookup"><span data-stu-id="e148a-220">Run the grant script in the application database</span></span>

<span data-ttu-id="e148a-221">你可以将发布配置文件配置为在部署期间在成员资格数据库中运行授予脚本，因为该数据库部署使用[dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)提供程序。</span><span class="sxs-lookup"><span data-stu-id="e148a-221">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) provider.</span></span> <span data-ttu-id="e148a-222">在 Code First 迁移部署过程中无法运行脚本，这是部署应用程序数据库的方式。</span><span class="sxs-lookup"><span data-stu-id="e148a-222">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="e148a-223">这意味着在应用程序数据库中进行部署之前，必须手动运行该脚本。</span><span class="sxs-lookup"><span data-stu-id="e148a-223">This means you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="e148a-224">在 Visual Studio 中，打开之前创建的*Grant .sql*文件。</span><span class="sxs-lookup"><span data-stu-id="e148a-224">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>

2. <span data-ttu-id="e148a-225">选择 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-225">Select **Connect**.</span></span> 

    ![连接按钮](deploying-to-iis/_static/image11.png)

3. <span data-ttu-id="e148a-227">在 "**连接到服务器**" 对话框中，输入 " *.\SQLExpress* " 作为**服务器名称**。</span><span class="sxs-lookup"><span data-stu-id="e148a-227">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**.</span></span> <span data-ttu-id="e148a-228">选择 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-228">Select **Connect**.</span></span>

4. <span data-ttu-id="e148a-229">在 "数据库" 下拉列表中，选择 " **ContosoUniversity**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-229">In the database drop-down list select **ContosoUniversity**.</span></span> <span data-ttu-id="e148a-230">选择 "**执行**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-230">Select **Execute**.</span></span> 

   ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="e148a-231">默认应用程序池标识现在在应用程序数据库中具有足够的权限，以便在应用程序运行时创建数据库表 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="e148a-231">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="e148a-232">发布到 IIS</span><span class="sxs-lookup"><span data-stu-id="e148a-232">Publish to IIS</span></span>

<span data-ttu-id="e148a-233">可以通过多种方式使用 Visual Studio 和 Web 部署部署到 IIS：</span><span class="sxs-lookup"><span data-stu-id="e148a-233">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

* <span data-ttu-id="e148a-234">使用 Visual Studio 一键式发布。</span><span class="sxs-lookup"><span data-stu-id="e148a-234">Use Visual Studio one-click publish.</span></span>
* <span data-ttu-id="e148a-235">从命令行发布。</span><span class="sxs-lookup"><span data-stu-id="e148a-235">Publish from the command line.</span></span>
* <span data-ttu-id="e148a-236">创建部署包，并使用 IIS 管理器进行安装。</span><span class="sxs-lookup"><span data-stu-id="e148a-236">Create a deployment package and install it using IIS Manager.</span></span> <span data-ttu-id="e148a-237">该包具有一个 .zip 文件，其中包含在 IIS 中安装站点所需的所有文件和元数据。</span><span class="sxs-lookup"><span data-stu-id="e148a-237">The package has a .zip file with all the files and metadata required to install a site in IIS.</span></span>
* <span data-ttu-id="e148a-238">使用命令行创建部署包并进行安装。</span><span class="sxs-lookup"><span data-stu-id="e148a-238">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="e148a-239">在前面的教程中，设置 Visual Studio 以自动完成部署任务的过程适用于所有这些方法。</span><span class="sxs-lookup"><span data-stu-id="e148a-239">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="e148a-240">在这些教程中，你将使用前两种方法。</span><span class="sxs-lookup"><span data-stu-id="e148a-240">In these tutorials, you'll use the first two methods.</span></span> <span data-ttu-id="e148a-241">有关使用部署包的信息，请参阅在 Visual Studio 和 ASP.NET 的 Web 部署内容映射中[创建和安装 web 部署包来部署 web 应用程序](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)。</span><span class="sxs-lookup"><span data-stu-id="e148a-241">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="e148a-242">在发布之前，请确保在管理员模式下运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e148a-242">Before publishing, make sure that you're running Visual Studio in administrator mode.</span></span> <span data-ttu-id="e148a-243">如果在标题栏中看不到 "**管理员**"，请关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e148a-243">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="e148a-244">在 Windows 8 （或更高版本 **）或**windows 7 "**开始**" 菜单中，右键单击 Visual Studio 图标，然后选择 "以**管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-244">In the Windows 8 (or later) **Start** page or the Windows 7 **Start** menu, right-click the Visual Studio icon and select **Run as Administrator**.</span></span> <span data-ttu-id="e148a-245">只有在发布到本地计算机上的 IIS 时才需要管理员模式。</span><span class="sxs-lookup"><span data-stu-id="e148a-245">Administrator mode is only required for publishing when you're publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="e148a-246">创建发布配置文件</span><span class="sxs-lookup"><span data-stu-id="e148a-246">Create the publish profile</span></span>

1. <span data-ttu-id="e148a-247">在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目（而不是**ContosoUniversity**项目）。</span><span class="sxs-lookup"><span data-stu-id="e148a-247">In **Solution Explorer**, right-click the **ContosoUniversity** project (not the **ContosoUniversity.DAL** project).</span></span> <span data-ttu-id="e148a-248">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="e148a-248">Select **Publish**.</span></span> <span data-ttu-id="e148a-249">此时将显示 "**发布**" 页。</span><span class="sxs-lookup"><span data-stu-id="e148a-249">The **Publish** page appears.</span></span>

2. <span data-ttu-id="e148a-250">选择 "**新建配置文件**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-250">Select **New Profile**.</span></span> <span data-ttu-id="e148a-251">此时将显示 "**选取发布目标**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="e148a-251">The **Pick a publish target** dialog box appears.</span></span>

3. <span data-ttu-id="e148a-252">选择 " **IIS"、"FTP" 等**。选择 "**创建配置文件**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-252">Select **IIS, FTP, etc**. Select **Create Profile**.</span></span> <span data-ttu-id="e148a-253">此时将显示**发布**向导。</span><span class="sxs-lookup"><span data-stu-id="e148a-253">The **Publish** wizard appears.</span></span>

   ![发布 Web 向导 "配置文件" 选项卡](deploying-to-iis/_static/image26.png)

4. <span data-ttu-id="e148a-255">从 "**发布方法**" 下拉菜单中选择 " **Web 部署**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-255">From the **Publish method** drop-down menu, select **Web Deploy**.</span></span>

5. <span data-ttu-id="e148a-256">对于 "**服务器**"，请输入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="e148a-256">For **Server**, enter *localhost*.</span></span>

6. <span data-ttu-id="e148a-257">对于 "**站点名称**"，输入*默认网站/ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="e148a-257">For **Site name**, enter *Default Web Site/ContosoUniversity*.</span></span>

7. <span data-ttu-id="e148a-258">对于 "**目标 URL**"，请输入 *http://localhost/ContosoUniversity* 。</span><span class="sxs-lookup"><span data-stu-id="e148a-258">For **Destination URL**, enter *http://localhost/ContosoUniversity*.</span></span>

   <span data-ttu-id="e148a-259">不需要 "**目标 URL** " 设置。</span><span class="sxs-lookup"><span data-stu-id="e148a-259">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="e148a-260">当 Visual Studio 完成应用程序的部署时，它会自动打开此 URL 的默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="e148a-260">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="e148a-261">如果你不希望在部署后自动打开浏览器，请将此框留空。</span><span class="sxs-lookup"><span data-stu-id="e148a-261">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

8. <span data-ttu-id="e148a-262">选择 "**验证连接**" 以验证设置是否正确，并且你可以连接到本地计算机上的 IIS。</span><span class="sxs-lookup"><span data-stu-id="e148a-262">Select **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

   <span data-ttu-id="e148a-263">绿色复选标记将验证连接是否成功。</span><span class="sxs-lookup"><span data-stu-id="e148a-263">A green check mark verifies that the connection is successful.</span></span>

   ![发布 Web 向导连接选项卡](deploying-to-iis/_static/image27.png)

9. <span data-ttu-id="e148a-265">选择 "**下一步**" 转到 "**设置**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="e148a-265">Select **Next** to advance to the **Settings** tab.</span></span>

10. <span data-ttu-id="e148a-266">"**配置**" 下拉框指定要部署的生成配置。</span><span class="sxs-lookup"><span data-stu-id="e148a-266">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="e148a-267">将其设置为 "**发布**" 的默认值。</span><span class="sxs-lookup"><span data-stu-id="e148a-267">Leave it set to the default value of **Release**.</span></span> <span data-ttu-id="e148a-268">在本教程中不会部署调试版本。</span><span class="sxs-lookup"><span data-stu-id="e148a-268">You won't be deploying Debug builds in this tutorial.</span></span>

11. <span data-ttu-id="e148a-269">展开 "**文件发布选项**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-269">Expand **File Publish Options**.</span></span> <span data-ttu-id="e148a-270">选择 **"从应用程序中排除文件\_Data 文件夹**。</span><span class="sxs-lookup"><span data-stu-id="e148a-270">Select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="e148a-271">在测试环境中，应用程序将访问在本地 SQL Server Express 实例中创建的数据库，而不是*应用\_Data*文件夹中的 .mdf 文件。</span><span class="sxs-lookup"><span data-stu-id="e148a-271">In the test environment, the application accesses the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>

12. <span data-ttu-id="e148a-272">在 "发布并**删除目标中的其他文件**" 复选框处于清除状态**时保留预编译**。</span><span class="sxs-lookup"><span data-stu-id="e148a-272">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    !["设置" 选项卡中的文件发布选项](deploying-to-iis/_static/image15a.png)

    <span data-ttu-id="e148a-274">预编译是主要用于大站点的选项。</span><span class="sxs-lookup"><span data-stu-id="e148a-274">Precompiling is an option that is useful mainly for large sites.</span></span> <span data-ttu-id="e148a-275">它可以在站点发布后第一次请求页面时减少启动时间。</span><span class="sxs-lookup"><span data-stu-id="e148a-275">It can reduce startup time the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="e148a-276">你不需要删除其他文件，因为这是首次部署，但目标文件夹中没有任何文件。</span><span class="sxs-lookup"><span data-stu-id="e148a-276">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e148a-277">如果你选择 "**删除目标中的其他文件**" 以便向同一站点进行后续部署，请确保使用预览功能，以便在部署之前提前了解哪些文件将被删除。</span><span class="sxs-lookup"><span data-stu-id="e148a-277">If you select **Remove additional files at destination** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="e148a-278">预期的行为是，Web 部署会删除已在项目中删除的目标服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="e148a-278">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="e148a-279">但会比较源文件夹和目标文件夹下的整个文件夹结构;在某些情况下，Web 部署可能会删除不想删除的文件。</span><span class="sxs-lookup"><span data-stu-id="e148a-279">However, the entire folder structure under the source and destination folders is compared; and in some scenarios, Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="e148a-280">例如，如果在将项目部署到根文件夹时在服务器上的子文件夹中有一个 web 应用程序，则该子文件夹将被删除。</span><span class="sxs-lookup"><span data-stu-id="e148a-280">For example if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="e148a-281">你可能在 contoso.com 的主站点上有一个项目，另一个项目用于 contoso.com/blog 的博客。</span><span class="sxs-lookup"><span data-stu-id="e148a-281">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="e148a-282">博客应用程序位于子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e148a-282">The blog application is in a subfolder.</span></span> <span data-ttu-id="e148a-283">如果您在部署主站点时选择了 "**删除目标位置的其他文件**"，则会删除该博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="e148a-283">If you select **Remove additional files at destination** when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="e148a-284">对于另一个示例，应用\_Data 文件夹可能会意外删除。</span><span class="sxs-lookup"><span data-stu-id="e148a-284">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="e148a-285">某些数据库（如 SQL Server Compact）将数据库文件存储在应用\_Data 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e148a-285">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="e148a-286">初始部署后，你不想在后续部署中继续复制数据库文件，因此，你可以在 "包/发布 Web" 选项卡上选择 "**排除应用程序\_数据**"。执行此操作后，如果选择了 "**在目标上删除其他文件**"，则在下一次发布时，将删除数据库文件和应用\_Data 文件夹本身。</span><span class="sxs-lookup"><span data-stu-id="e148a-286">After the initial deployment, you don't want to keep copying the database files in subsequent deployments, so you select  **Exclude App\_Data** on the Package/Publish Web tab. After you do that if you have **Remove additional files at destination** selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="e148a-287">为成员资格数据库配置部署</span><span class="sxs-lookup"><span data-stu-id="e148a-287">Configure deployment for the membership database</span></span>

<span data-ttu-id="e148a-288">以下步骤适用于对话框的 "**数据库**" 部分中的**DefaultConnection**数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-288">The following steps apply to the **DefaultConnection** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="e148a-289">在 "**远程连接字符串**" 框中，输入以下指向新 SQL Server Express 成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e148a-289">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   <span data-ttu-id="e148a-290">部署过程会将此连接字符串放在部署的 Web.config 文件中，原因是选择了 "**在运行时使用此连接字符串**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-290">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="e148a-291">还可以从**服务器资源管理器**获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e148a-291">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="e148a-292">在**服务器资源管理器**中，展开 "**数据连接**"，然后选择 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**数据库，然后从 "**属性**" 窗口复制**连接字符串**值。</span><span class="sxs-lookup"><span data-stu-id="e148a-292">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="e148a-293">该连接字符串将有一个可以删除的其他设置： `Pooling=False`。</span><span class="sxs-lookup"><span data-stu-id="e148a-293">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>

2. <span data-ttu-id="e148a-294">选择 "**更新数据库**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-294">Select **Update database**.</span></span>

   <span data-ttu-id="e148a-295">这会导致在部署过程中在目标数据库中创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="e148a-295">This causes the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="e148a-296">在后续步骤中，你将指定你需要运行的其他脚本：一个用于授予对默认应用程序池的数据库访问权限，另一个用于部署数据。</span><span class="sxs-lookup"><span data-stu-id="e148a-296">In next steps, you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>

3. <span data-ttu-id="e148a-297">选择 "**配置数据库更新**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-297">Select **Configure database updates**.</span></span>
 
4. <span data-ttu-id="e148a-298">在 "**配置数据库更新**" 对话框中，选择 "**添加 SQL 脚本**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-298">In the **Configure Database Updates** dialog box, select **Add SQL Script**.</span></span> <span data-ttu-id="e148a-299">导航到之前在解决方案文件夹中保存的*Grant .sql*脚本。</span><span class="sxs-lookup"><span data-stu-id="e148a-299">Navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>

5. <span data-ttu-id="e148a-300">重复此过程以添加*aspnet-data-dev*脚本。</span><span class="sxs-lookup"><span data-stu-id="e148a-300">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

   ![为成员资格数据库配置数据库更新](deploying-to-iis/_static/image16.png)

6. <span data-ttu-id="e148a-302">选择“关闭”。</span><span class="sxs-lookup"><span data-stu-id="e148a-302">Select **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="e148a-303">为应用程序数据库配置部署</span><span class="sxs-lookup"><span data-stu-id="e148a-303">Configure deployment for the application database</span></span>

<span data-ttu-id="e148a-304">当 Visual Studio 检测到实体框架 `DbContext` 类时，它将在 "**数据库**" 部分创建一个具有 "**执行 Code First 迁移**" 复选框而不是 "**更新数据库**" 复选框的条目。</span><span class="sxs-lookup"><span data-stu-id="e148a-304">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="e148a-305">对于本教程，你将使用此复选框来指定 Code First 迁移部署。</span><span class="sxs-lookup"><span data-stu-id="e148a-305">For this tutorial, you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="e148a-306">在某些情况下，你可能正在使用 `DbContext` 数据库，但你想要使用 dbDacFx 提供程序而不是迁移来部署数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-306">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="e148a-307">在这种情况下，请参阅 MSDN 上的 ASP.NET Web 部署常见问题解答中的[如何实现部署 Code First 数据库（不迁移](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)）。</span><span class="sxs-lookup"><span data-stu-id="e148a-307">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="e148a-308">以下步骤适用于对话框的 "**数据库**" 部分中的**SchoolContext**数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-308">The following steps apply to the **SchoolContext** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="e148a-309">在 "**远程连接字符串**" 框中，输入以下指向新 SQL Server Express 应用程序数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e148a-309">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   <span data-ttu-id="e148a-310">部署过程会将此连接字符串放在部署的 Web.config 文件中，原因是选择了 "**在运行时使用此连接字符串**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-310">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

   <span data-ttu-id="e148a-311">你还可以从**服务器资源管理器**获取应用程序数据库连接字符串，其方式与获取成员资格数据库连接字符串的方式相同。</span><span class="sxs-lookup"><span data-stu-id="e148a-311">You can also get the application database connection string from **Server Explorer** in the same way you got the membership database connection string.</span></span>

2. <span data-ttu-id="e148a-312">选择 **"执行 Code First 迁移（在应用程序启动时运行）** 。</span><span class="sxs-lookup"><span data-stu-id="e148a-312">Select **Execute Code First Migrations (runs on application start)**.</span></span>

   <span data-ttu-id="e148a-313">此选项将导致部署过程配置部署的 Web.config 文件以指定 `MigrateDatabaseToLatestVersion` 初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="e148a-313">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="e148a-314">当应用程序在部署后首次访问数据库时，此初始值设定项会将数据库自动更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="e148a-314">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="e148a-315">配置发布配置文件转换</span><span class="sxs-lookup"><span data-stu-id="e148a-315">Configure publish profile transforms</span></span>

1. <span data-ttu-id="e148a-316">选择“关闭”。</span><span class="sxs-lookup"><span data-stu-id="e148a-316">Select **Close**.</span></span> <span data-ttu-id="e148a-317">如果系统询问是否要保存更改，请选择 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="e148a-317">Select **Yes** when you are asked if you want to save changes.</span></span>

2. <span data-ttu-id="e148a-318">在**解决方案资源管理器**中，展开 "**属性**"，然后展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="e148a-318">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>

3. <span data-ttu-id="e148a-319">右键单击*CustomProfile .pubxml*并将其重命名为 *.pubxml*。</span><span class="sxs-lookup"><span data-stu-id="e148a-319">Right-click *CustomProfile.pubxml* and rename it *Test.pubxml*.</span></span>

4. <span data-ttu-id="e148a-320">右键单击 *.pubxml*。</span><span class="sxs-lookup"><span data-stu-id="e148a-320">Right-click *Test.pubxml*.</span></span> <span data-ttu-id="e148a-321">选择 "**添加配置转换**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-321">Select **Add Config Transform**.</span></span>

   ![添加配置转换菜单](deploying-to-iis/_static/image17.png)

   <span data-ttu-id="e148a-323">Visual Studio 将创建*web.config*转换文件并将其打开。</span><span class="sxs-lookup"><span data-stu-id="e148a-323">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>

5. <span data-ttu-id="e148a-324">在*web.config*转换文件中，将以下代码插入到紧靠在开始配置标记之后。</span><span class="sxs-lookup"><span data-stu-id="e148a-324">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="e148a-325">使用测试发布配置文件时，此转换会将环境指示器设置为 "测试"。</span><span class="sxs-lookup"><span data-stu-id="e148a-325">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="e148a-326">在部署的站点中，你将看到 "Contoso 大学" H1 标题后面的 "（测试）"。</span><span class="sxs-lookup"><span data-stu-id="e148a-326">In the deployed site, you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>

6. <span data-ttu-id="e148a-327">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="e148a-327">Save and close the file.</span></span>

7. <span data-ttu-id="e148a-328">右键单击 " *web.config* " 文件，然后选择 "**预览转换**"，以确保编码的转换生成所需的更改。</span><span class="sxs-lookup"><span data-stu-id="e148a-328">Right-click the *Web.Test.config* file and select **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="e148a-329">Web.config**预览**窗口显示了同时应用*web.config*转换和*web.config 转换的结果。 ""* 。</span><span class="sxs-lookup"><span data-stu-id="e148a-329">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="e148a-330">预览部署更新</span><span class="sxs-lookup"><span data-stu-id="e148a-330">Preview the deployment updates</span></span>

1. <span data-ttu-id="e148a-331">再次打开 "**发布 Web** " 向导（右键单击 ContosoUniversity 项目，选择 "**发布**"，然后选择 "**预览**"）。</span><span class="sxs-lookup"><span data-stu-id="e148a-331">Open the **Publish Web** wizard again (right-click the ContosoUniversity project, select **Publish**, then **Preview**).</span></span>

2. <span data-ttu-id="e148a-332">在 "**预览**" 对话框中，选择 "**开始预览**" 以查看要复制的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="e148a-332">In the **Preview** dialog box, select **Start Preview** to see a list of the files that will be copied.</span></span> 

   ![发布预览](deploying-to-iis/_static/image29.png)

   <span data-ttu-id="e148a-334">还可以选择 "**预览数据库**" 链接，查看将在成员资格数据库中运行的脚本。</span><span class="sxs-lookup"><span data-stu-id="e148a-334">You can also select the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="e148a-335">（没有为 Code First 迁移部署运行脚本，因此应用程序数据库无需预览。）</span><span class="sxs-lookup"><span data-stu-id="e148a-335">(No scripts are run for Code First Migrations deployment, so there's nothing to preview for the application database.)</span></span>

3. <span data-ttu-id="e148a-336">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="e148a-336">Select **Publish**.</span></span>

   <span data-ttu-id="e148a-337">如果 Visual Studio 未处于管理员模式，你可能会收到权限错误消息。</span><span class="sxs-lookup"><span data-stu-id="e148a-337">If Visual Studio is not in administrator mode, you might get a permissions error message.</span></span> <span data-ttu-id="e148a-338">在这种情况下，请关闭 Visual Studio，在管理员模式下打开它，然后再次尝试发布。</span><span class="sxs-lookup"><span data-stu-id="e148a-338">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

   <span data-ttu-id="e148a-339">如果 Visual Studio 处于管理员模式下，则 "**输出**" 窗口将报告成功的生成和发布。</span><span class="sxs-lookup"><span data-stu-id="e148a-339">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   <span data-ttu-id="e148a-341">如果在 "发布配置文件**连接**" 选项卡上的 "**目标 URL** " 框中输入了 URL，浏览器会自动打开到计算机上 IIS 中运行的 Contoso 大学主页。</span><span class="sxs-lookup"><span data-stu-id="e148a-341">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on your computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="e148a-342">测试环境中的测试</span><span class="sxs-lookup"><span data-stu-id="e148a-342">Test in the test environment</span></span>

<span data-ttu-id="e148a-343">请注意，环境指示器显示 "（测试）"，而不是 "（开发）"，这表明环境指示器的*web.config 转换已*成功。</span><span class="sxs-lookup"><span data-stu-id="e148a-343">Notice that the environment indicator shows "(Test)" instead of "(Dev)," which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="e148a-344">运行**讲师**页，验证 Code First 用指导员数据对数据库进行种子设定。</span><span class="sxs-lookup"><span data-stu-id="e148a-344">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="e148a-345">选择此页时，可能需要几分钟的时间才能加载，因为 Code First 会创建数据库，然后运行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="e148a-345">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="e148a-346">（如果你在主页上，则不会执行此操作，因为应用程序尚未尝试访问数据库。）</span><span class="sxs-lookup"><span data-stu-id="e148a-346">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="e148a-347">选择 "**学生**" 选项卡，验证部署的数据库是否没有学生。</span><span class="sxs-lookup"><span data-stu-id="e148a-347">Select the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="e148a-348">从 "**学生**" 菜单中选择 "**添加学生**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-348">Select **Add Students** from the **Students** menu.</span></span> <span data-ttu-id="e148a-349">添加一个学生，然后在 "**学生**" 页中查看新学生。</span><span class="sxs-lookup"><span data-stu-id="e148a-349">Add a student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="e148a-350">这将验证是否可以成功写入数据库。</span><span class="sxs-lookup"><span data-stu-id="e148a-350">This verifies that you can successfully write to the database.</span></span>

<span data-ttu-id="e148a-351">从**课程**菜单中，选择 "**更新信用**"。</span><span class="sxs-lookup"><span data-stu-id="e148a-351">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="e148a-352">**更新信用**页面需要管理员权限，因此将显示 "**登录**" 页。</span><span class="sxs-lookup"><span data-stu-id="e148a-352">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="e148a-353">输入先前创建的管理员帐户凭据（"admin" 和 "devpwd"）。</span><span class="sxs-lookup"><span data-stu-id="e148a-353">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="e148a-354">将显示 "**更新信用额度**" 页。</span><span class="sxs-lookup"><span data-stu-id="e148a-354">The **Update Credits** page is displayed.</span></span> <span data-ttu-id="e148a-355">这将验证你在上一教程中创建的管理员帐户是否已正确部署到测试环境中。</span><span class="sxs-lookup"><span data-stu-id="e148a-355">This verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="e148a-356">验证*c:\inetpub\wwwroot\ContosoUniversity*文件夹中是否存在只包含占位符文件的*ELMAH*文件夹。</span><span class="sxs-lookup"><span data-stu-id="e148a-356">Verify that an *ELMAH* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="e148a-357">查看自动 Code First 迁移的 web.config 更改</span><span class="sxs-lookup"><span data-stu-id="e148a-357">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="e148a-358">在 C:\inetpub\wwwroot\ContosoUniversity*中的已*部署应用程序中打开 web.config文件，并可以看到部署过程的配置 Code First 迁移将数据库自动更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="e148a-358">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="e148a-359">部署过程还为 Code First 迁移创建了一个新的连接字符串，以独占方式用于更新数据库架构：</span><span class="sxs-lookup"><span data-stu-id="e148a-359">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 连接字符串](deploying-to-iis/_static/image22.png)

<span data-ttu-id="e148a-361">使用此附加连接字符串，您可以为数据库架构更新指定一个用户帐户，并为应用程序数据访问指定不同的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="e148a-361">This additional connection string enables you to specify one user account for database schema updates and a different user account for application data access.</span></span> <span data-ttu-id="e148a-362">例如，可以将**db\_所有者**角色分配给应用程序的 Code First 迁移和**db\_** 与**db\_datawriter**角色。</span><span class="sxs-lookup"><span data-stu-id="e148a-362">For example, you could assign the **db\_owner** role to Code First Migrations and **db\_datareader** with **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="e148a-363">这是一种常见的深层防御模式，可防止应用程序中可能存在的恶意代码更改数据库架构。</span><span class="sxs-lookup"><span data-stu-id="e148a-363">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="e148a-364">（例如，这可能会在成功的 SQL 注入攻击中发生。）这些教程不使用这种模式。</span><span class="sxs-lookup"><span data-stu-id="e148a-364">(For example, this might happen in a successful SQL injection attack.) These tutorials don't use this pattern.</span></span> <span data-ttu-id="e148a-365">若要在方案中实现此模式，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="e148a-365">To implement this pattern in your scenario, take these steps:</span></span>

1. <span data-ttu-id="e148a-366">在 "**发布 Web** " 向导中的 "**设置**" 选项卡下，输入指定具有完整数据库架构更新权限的用户的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e148a-366">In the **Publish Web** wizard under the **Settings** tab, enter the connection string that specifies a user with full database schema update permissions.</span></span> <span data-ttu-id="e148a-367">清除 "**在运行时使用此连接字符串**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="e148a-367">Clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="e148a-368">在部署的 Web.config 文件中，这将成为 `DatabasePublish` 的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e148a-368">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>

2. <span data-ttu-id="e148a-369">为希望应用程序在运行时使用的连接字符串创建 web.config 文件转换。</span><span class="sxs-lookup"><span data-stu-id="e148a-369">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="e148a-370">总结</span><span class="sxs-lookup"><span data-stu-id="e148a-370">Summary</span></span>

<span data-ttu-id="e148a-371">现在，你已将应用程序部署到 IIS 开发计算机上，并在其中进行测试。</span><span class="sxs-lookup"><span data-stu-id="e148a-371">You've now deployed your application to IIS on your development computer and tested it there.</span></span>

![测试中的主页](deploying-to-iis/_static/image23.png)

<span data-ttu-id="e148a-373">这会验证部署过程是否已将应用程序的内容复制到适当的位置（不包括你不想部署的文件），同时还会在部署过程中正确 Web 部署配置 IIS。</span><span class="sxs-lookup"><span data-stu-id="e148a-373">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy) and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="e148a-374">在下一教程中，您将运行一个查找尚未完成的部署任务的测试：设置 "*榆树 ah* " 文件夹的文件夹权限。</span><span class="sxs-lookup"><span data-stu-id="e148a-374">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elm ah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="e148a-375">更多信息</span><span class="sxs-lookup"><span data-stu-id="e148a-375">More information</span></span>

<span data-ttu-id="e148a-376">有关在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e148a-376">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="e148a-377">[IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 站点上的概述。</span><span class="sxs-lookup"><span data-stu-id="e148a-377">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="e148a-378">Scott Guthrie 的博客[介绍 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e148a-378">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="e148a-379">[Visual Studio 中用于 ASP.NET Web 项目的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e148a-379">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="e148a-380">[IIS 与 ASP.NET 站点上的 ASP.NET 开发服务器之间的核心差异](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。</span><span class="sxs-lookup"><span data-stu-id="e148a-380">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="e148a-381">有关应用程序以中等信任模式运行时可能会出现的问题的信息，请参阅在 Rolla 站点的四个用户上[托管中等信任中的 ASP.NET 应用程序](http://www.4guysfromrolla.com/articles/100307-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e148a-381">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the four Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e148a-382">[上一页](project-properties.md)
> [下一页](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="e148a-382">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
