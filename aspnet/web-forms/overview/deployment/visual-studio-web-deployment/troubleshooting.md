---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 使用 Visual Studio 的 ASP.NET Web 部署：疑难解答 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: b42476fca18b04f4557a216ee205cfd9220023e8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465092"
---
# <a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a><span data-ttu-id="45170-103">使用 Visual Studio 的 ASP.NET Web 部署：疑难解答</span><span class="sxs-lookup"><span data-stu-id="45170-103">ASP.NET Web Deployment using Visual Studio: Troubleshooting</span></span>

<span data-ttu-id="45170-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="45170-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="45170-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="45170-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="45170-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="45170-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="45170-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="45170-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="45170-108">本页介绍使用 Visual Studio 部署 ASP.NET web 应用程序时可能出现的一些常见问题。</span><span class="sxs-lookup"><span data-stu-id="45170-108">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="45170-109">对于每个问题，都提供了一个或多个可能的原因和相应的解决方案。</span><span class="sxs-lookup"><span data-stu-id="45170-109">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

<span data-ttu-id="45170-110">显示的方案适用于 Azure 和第三方托管提供程序。</span><span class="sxs-lookup"><span data-stu-id="45170-110">The scenarios shown apply to both Azure and third-party hosting providers.</span></span> <span data-ttu-id="45170-111">有关对 Azure 应用服务中的 Web 应用进行故障排除的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="45170-111">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

- [<span data-ttu-id="45170-112">使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="45170-112">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [<span data-ttu-id="45170-113">监视 Azure 应用服务中的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="45170-113">Monitor Web Apps in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- <span data-ttu-id="45170-114">[宣布推出 Windows AZURE SDK 2.0 for .net](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) （ScottGu 的博客，演示如何在 Visual Studio 中获取诊断日志）</span><span class="sxs-lookup"><span data-stu-id="45170-114">[Announcing the release of Windows Azure SDK 2.0 for .NET](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu's blog, shows how to get diagnostic logs in Visual Studio)</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="45170-115">"/" 应用程序中的服务器错误-当前自定义错误设置阻止远程查看错误的详细信息</span><span class="sxs-lookup"><span data-stu-id="45170-115">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-116">方案</span><span class="sxs-lookup"><span data-stu-id="45170-116">Scenario</span></span>

<span data-ttu-id="45170-117">将站点部署到远程主机之后，会收到一条错误消息，其中提及了 Web.config 文件中的 customErrors 设置，但未指示错误的实际原因：</span><span class="sxs-lookup"><span data-stu-id="45170-117">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-118">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-118">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-119">默认情况下，仅当你的 web 应用程序在本地计算机上运行时，ASP.NET 才会显示详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="45170-119">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="45170-120">通常，当您的 web 应用程序在 Internet 上公开可用时，您不想显示详细的错误信息，因为黑客可能能够利用此信息来查找应用程序中的漏洞。</span><span class="sxs-lookup"><span data-stu-id="45170-120">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="45170-121">但是，在部署站点或更新站点时，有时会出现问题，需要获取实际的错误消息。</span><span class="sxs-lookup"><span data-stu-id="45170-121">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="45170-122">若要使应用程序能够在远程主机上运行时显示详细的错误消息，请编辑 Web.config 文件以将 customErrors 模式设置为 off，重新部署应用程序，然后再次运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="45170-122">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set customErrors mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="45170-123">如果应用程序的 web.config 文件在 customErrors 元素中有一个 "" 元素，则将 mode 特性更改为 "off"。</span><span class="sxs-lookup"><span data-stu-id="45170-123">If the application Web.config file has a customErrors element in the system.web element, change the mode attribute to "off".</span></span> <span data-ttu-id="45170-124">否则，请将 customErrors 元素添加到 mode 特性设置为 "off" 的 "system.web" 元素中，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="45170-124">Otherwise add a customErrors element in the system.web element with the mode attribute set to "off", as shown in the following example:</span></span> 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. <span data-ttu-id="45170-125">部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="45170-125">Deploy the application.</span></span>
3. <span data-ttu-id="45170-126">运行该应用程序，并重复您之前执行的任何导致错误的操作。</span><span class="sxs-lookup"><span data-stu-id="45170-126">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="45170-127">现在，你可以看到实际的错误消息是什么。</span><span class="sxs-lookup"><span data-stu-id="45170-127">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="45170-128">解决错误后，还原原始 customErrors 设置并重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="45170-128">When you have resolved the error, restore the original customErrors setting and redeploy the application.</span></span>

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a><span data-ttu-id="45170-129">如果文件已存在，则无法创建/影像复制 ' ContosoUniversity '。</span><span class="sxs-lookup"><span data-stu-id="45170-129">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-130">方案</span><span class="sxs-lookup"><span data-stu-id="45170-130">Scenario</span></span>

<span data-ttu-id="45170-131">尝试在 Visual Studio 中运行项目时，会出现一个错误页面，其中包含类似于以下示例的消息：</span><span class="sxs-lookup"><span data-stu-id="45170-131">When you try to run a project in Visual Studio you get an error page with a message like the following example:</span></span>

<span data-ttu-id="45170-132">'/' 应用程序中出现服务器错误。</span><span class="sxs-lookup"><span data-stu-id="45170-132">Server Error in '/' Application.</span></span> <span data-ttu-id="45170-133">如果文件已存在，则无法创建/影像复制 ' ContosoUniversity '。</span><span class="sxs-lookup"><span data-stu-id="45170-133">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-134">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-134">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-135">请稍等片刻并刷新浏览器，或重新编译该站点，然后再次尝试运行它。</span><span class="sxs-lookup"><span data-stu-id="45170-135">Wait a minute and refresh the browser, or recompile the site and try running it again.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="45170-136">使用 SQL Server Compact 的网页中的访问被拒绝</span><span class="sxs-lookup"><span data-stu-id="45170-136">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-137">方案</span><span class="sxs-lookup"><span data-stu-id="45170-137">Scenario</span></span>

<span data-ttu-id="45170-138">当你部署使用 SQL Server Compact 的站点，并且在已部署的站点中运行访问该数据库的页面时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-138">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

<span data-ttu-id="45170-139">拒绝访问。</span><span class="sxs-lookup"><span data-stu-id="45170-139">Access is denied.</span></span> <span data-ttu-id="45170-140">（HRESULT 中的异常：0x80070005 （E\_ACCESSDENIED））</span><span class="sxs-lookup"><span data-stu-id="45170-140">(Exception from HRESULT: 0x80070005 (E\_ACCESSDENIED))</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-141">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-141">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-142">服务器上的网络服务帐户需要能够读取*bin\amd64*或*bin\x86*文件夹中的 SQL 服务压缩本机二进制文件，但它不具有对这些文件夹的读取权限。</span><span class="sxs-lookup"><span data-stu-id="45170-142">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="45170-143">设置*bin*文件夹的 "网络服务的读取权限"，并确保将权限扩展到子文件夹。</span><span class="sxs-lookup"><span data-stu-id="45170-143">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="45170-144">由于权限不足而无法读取配置文件</span><span class="sxs-lookup"><span data-stu-id="45170-144">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-145">方案</span><span class="sxs-lookup"><span data-stu-id="45170-145">Scenario</span></span>

<span data-ttu-id="45170-146">单击 Visual Studio 的 "发布" 按钮将应用程序部署到本地计算机上的 IIS 后，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-146">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

<span data-ttu-id="45170-147">读取 IIS 配置文件 "计算机/重定向" 时出错。</span><span class="sxs-lookup"><span data-stu-id="45170-147">An error occurred when reading the IIS Configuration File 'MACHINE/REDIRECTION'.</span></span> <span data-ttu-id="45170-148">执行此操作的标识为 .。。错误：无法读取配置文件，因为权限不足。</span><span class="sxs-lookup"><span data-stu-id="45170-148">The identity performing this operation was ... Error: Cannot read configuration file due to insufficient permissions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-149">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-149">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-150">若要在本地计算机上使用一键式 "发布到 IIS"，必须使用管理员权限运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="45170-150">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="45170-151">关闭 Visual Studio 并以管理员权限重新启动它。</span><span class="sxs-lookup"><span data-stu-id="45170-151">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="45170-152">无法连接到目标计算机 .。。使用指定的进程</span><span class="sxs-lookup"><span data-stu-id="45170-152">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-153">方案</span><span class="sxs-lookup"><span data-stu-id="45170-153">Scenario</span></span>

<span data-ttu-id="45170-154">单击 Visual Studio 的 "发布" 按钮以部署应用程序时，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-154">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-155">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-155">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-156">代理服务器中断了与目标服务器的通信。</span><span class="sxs-lookup"><span data-stu-id="45170-156">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="45170-157">在 Windows "控制面板" 或 Internet Explorer 中，选择 " **Internet 选项**"，然后选择 "**连接**" 选项卡。在 " **Internet 属性**" 对话框中，单击 " **LAN 设置**"。</span><span class="sxs-lookup"><span data-stu-id="45170-157">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="45170-158">在 "局域网 **（LAN）设置**" 对话框中，清除 "**自动检测设置**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="45170-158">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="45170-159">然后再次单击 "发布" 按钮。</span><span class="sxs-lookup"><span data-stu-id="45170-159">Then click the publish button again.</span></span>

<span data-ttu-id="45170-160">如果问题仍然存在，请与系统管理员联系，以确定可对代理或防火墙设置执行的操作。</span><span class="sxs-lookup"><span data-stu-id="45170-160">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="45170-161">发生此问题的原因是 Web 部署为 Web 管理服务部署使用非标准端口（8172）;对于其他连接，Web 部署使用端口80。</span><span class="sxs-lookup"><span data-stu-id="45170-161">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="45170-162">部署到第三方托管提供程序时，通常使用 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="45170-162">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="45170-163">默认的 .NET 4.0 应用程序池不存在</span><span class="sxs-lookup"><span data-stu-id="45170-163">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-164">方案</span><span class="sxs-lookup"><span data-stu-id="45170-164">Scenario</span></span>

<span data-ttu-id="45170-165">部署需要 .NET Framework 4 的应用程序时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-165">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

<span data-ttu-id="45170-166">默认的 .NET 4.0 应用程序池不存在，或无法添加应用程序。</span><span class="sxs-lookup"><span data-stu-id="45170-166">The default .NET 4.0 application pool does not exist or the application could not be added.</span></span> <span data-ttu-id="45170-167">请验证是否在此计算机上安装了 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="45170-167">Please verify that ASP.NET 4.0 is installed on this machine.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-168">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-168">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-169">IIS 中未安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="45170-169">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="45170-170">如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。</span><span class="sxs-lookup"><span data-stu-id="45170-170">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="45170-171">在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="45170-171">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

<span data-ttu-id="45170-172">你可能还需要手动设置默认应用程序池的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="45170-172">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="45170-173">有关详细信息，请参阅本系列中的将部署到 IIS 作为测试环境教程。</span><span class="sxs-lookup"><span data-stu-id="45170-173">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="45170-174">初始化字符串的格式不符合从索引0处开始的规范。</span><span class="sxs-lookup"><span data-stu-id="45170-174">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-175">方案</span><span class="sxs-lookup"><span data-stu-id="45170-175">Scenario</span></span>

<span data-ttu-id="45170-176">使用一键式发布部署应用程序后，在运行访问数据库的页时，会收到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-176">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

<span data-ttu-id="45170-177">初始化字符串的格式不符合从索引0处开始的规范。</span><span class="sxs-lookup"><span data-stu-id="45170-177">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-178">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-178">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-179">在部署*的站点*中打开 web.config 文件，然后检查连接字符串值是否以 `$(ReplaceableToken_`开头，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="45170-179">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplaceableToken_`, as in the following example:</span></span>

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

<span data-ttu-id="45170-180">如果连接字符串与此示例类似，则编辑项目文件，并将以下属性添加到适用于所有生成配置的 PropertyGroup 元素：</span><span class="sxs-lookup"><span data-stu-id="45170-180">If the connection strings look like this example, edit the project file and add the following property to the PropertyGroup element that is for all build configurations:</span></span>

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

<span data-ttu-id="45170-181">然后重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="45170-181">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="45170-182">HTTP 500 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="45170-182">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-183">方案</span><span class="sxs-lookup"><span data-stu-id="45170-183">Scenario</span></span>

<span data-ttu-id="45170-184">当你运行部署的站点时，你将看到以下错误消息，其中没有指示错误原因的特定信息：</span><span class="sxs-lookup"><span data-stu-id="45170-184">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

<span data-ttu-id="45170-185">HTTP 错误 500-内部服务器错误。</span><span class="sxs-lookup"><span data-stu-id="45170-185">HTTP Error 500 - Internal Server Error.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-186">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-186">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-187">出现500错误的原因有很多，但如果您遵循这些教程，其中一种可能的原因是您将 XML 元素放在某个 Web.config 转换文件的错误位置。</span><span class="sxs-lookup"><span data-stu-id="45170-187">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the Web.config transformation files.</span></span> <span data-ttu-id="45170-188">例如，如果将插入 &lt;位置&gt; 元素的转换添加到 &lt;system.web&gt; 下，而不是直接在 &lt;配置&gt;下，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="45170-188">For example, you would get this error if you put the transformation that inserts a &lt;location&gt; element under &lt;system.web&gt; instead of directly under &lt;configuration&gt;.</span></span> <span data-ttu-id="45170-189">您可以使用 web.config 转换预览功能来验证转换是否按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="45170-189">You can use the Web.config transform preview feature to verify that transformations are working as intended.</span></span> <span data-ttu-id="45170-190">如果找到编码错误的转换，则解决方案是更正转换文件并重新部署。</span><span class="sxs-lookup"><span data-stu-id="45170-190">The solution if you find a transform that was coded incorrectly is to correct the transformation file and redeploy.</span></span> <span data-ttu-id="45170-191">如果错误不明显，请尝试注释转换和重新部署，以查看导致500错误的转换。</span><span class="sxs-lookup"><span data-stu-id="45170-191">If an error isn't obvious, try commenting out transforms and redeploying to see which one is causing the 500 error.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="45170-192">HTTP 500.21 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="45170-192">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-193">方案</span><span class="sxs-lookup"><span data-stu-id="45170-193">Scenario</span></span>

<span data-ttu-id="45170-194">当你运行部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-194">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="45170-195">HTTP 错误 500.21-内部服务器错误。</span><span class="sxs-lookup"><span data-stu-id="45170-195">HTTP Error 500.21 - Internal Server Error.</span></span> <span data-ttu-id="45170-196">处理程序 "Pagehandlerfactory-isapi-集成" 的模块列表中有一个错误的模块 "ManagedPipelineHandler"。</span><span class="sxs-lookup"><span data-stu-id="45170-196">Handler "PageHandlerFactory-Integrated" has a bad module "ManagedPipelineHandler" in its module list.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-197">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-197">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-198">部署的站点的目标为 ASP.NET 4，但未在服务器上的 IIS 中注册 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="45170-198">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="45170-199">在服务器上打开提升的命令提示符，并通过运行以下命令来注册 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="45170-199">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

<span data-ttu-id="45170-200">你可能还需要手动设置默认应用程序池的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="45170-200">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="45170-201">有关详细信息，请参阅本系列中的将部署到 IIS 作为测试环境教程。</span><span class="sxs-lookup"><span data-stu-id="45170-201">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a><span data-ttu-id="45170-202">登录无法在应用\_数据中打开 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="45170-202">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-203">方案</span><span class="sxs-lookup"><span data-stu-id="45170-203">Scenario</span></span>

<span data-ttu-id="45170-204">在应用中*将 web.config 文件连接*字符串更新为指向 SQL Server Express 数据库的 *.Mdf*文件 *\_Data*文件夹，并且首次运行应用程序时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-204">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="45170-205">SqlClient. SqlException：无法打开登录所请求的数据库 "DatabaseName"。</span><span class="sxs-lookup"><span data-stu-id="45170-205">System.Data.SqlClient.SqlException: Cannot open database "DatabaseName" requested by the login.</span></span> <span data-ttu-id="45170-206">登录失败。</span><span class="sxs-lookup"><span data-stu-id="45170-206">The login failed.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-207">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-207">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-208">即使删除了以前存在的数据库的 *.mdf*文件， *.mdf*文件的名称也不能与计算机上存在的任何 SQL Server Express 数据库的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="45170-208">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="45170-209">将 *.mdf*文件的名称更改为从未用作数据库名称的名称，并更改*web.config*文件以使用新名称。</span><span class="sxs-lookup"><span data-stu-id="45170-209">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="45170-210">作为替代方法，可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除以前存在的 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="45170-210">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="45170-211">无法检查模型的兼容性</span><span class="sxs-lookup"><span data-stu-id="45170-211">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-212">方案</span><span class="sxs-lookup"><span data-stu-id="45170-212">Scenario</span></span>

<span data-ttu-id="45170-213">已*将 web.config 文件连接*字符串更新为指向新的 SQL Server Express 数据库，并且首次运行应用程序时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-213">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="45170-214">无法检查模型兼容性，因为数据库不包含模型元数据。</span><span class="sxs-lookup"><span data-stu-id="45170-214">Model compatibility cannot be checked because the database does not contain model metadata.</span></span> <span data-ttu-id="45170-215">确保已将 IncludeMetadataConvention 添加到 DbModelBuilder 约定。</span><span class="sxs-lookup"><span data-stu-id="45170-215">Ensure that IncludeMetadataConvention has been added to the DbModelBuilder conventions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-216">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-216">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-217">如果在您的计算机上曾经使用过您放置在 web.config 文件中的数据库名称，则可能已经存在包含某些表的数据库。</span><span class="sxs-lookup"><span data-stu-id="45170-217">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="45170-218">选择之前未在计算机上使用的新名称，*然后将 web.config 文件更改*为指向 "使用此新数据库名称"。</span><span class="sxs-lookup"><span data-stu-id="45170-218">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="45170-219">作为替代方法，可以使用[SQL Server Express 实用工具](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除现有数据库。</span><span class="sxs-lookup"><span data-stu-id="45170-219">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="45170-220">脚本尝试创建用户或角色时出现 SQL 错误</span><span class="sxs-lookup"><span data-stu-id="45170-220">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-221">方案</span><span class="sxs-lookup"><span data-stu-id="45170-221">Scenario</span></span>

<span data-ttu-id="45170-222">你使用的是在 "**包/发布 SQL** " 选项卡上配置的数据库部署，在部署过程中运行的 SQL 脚本包含 "创建用户" 或 "创建角色" 命令，在执行这些命令时脚本执行将失败。</span><span class="sxs-lookup"><span data-stu-id="45170-222">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="45170-223">您可能会看到更详细的消息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45170-223">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

<span data-ttu-id="45170-224">如果在 "**发布 Web** " 向导而不是 "**包/发布 SQL** " 选项卡中配置数据库部署后发生此错误，请在[配置和部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)论坛中创建一个线程，该解决方案将添加到此故障排除页。</span><span class="sxs-lookup"><span data-stu-id="45170-224">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-225">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-225">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-226">用于执行部署的用户帐户没有创建用户或角色的权限。</span><span class="sxs-lookup"><span data-stu-id="45170-226">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="45170-227">例如，托管公司可以将 db\_datareader、db\_datawriter 和 db\_ddladmin 角色分配给它为您设置的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="45170-227">For example, the hosting company might assign the db\_datareader, db\_datawriter, and db\_ddladmin roles to the user account that it sets up for you.</span></span> <span data-ttu-id="45170-228">它们足以用于创建大多数数据库对象，但不能用于创建用户或角色。</span><span class="sxs-lookup"><span data-stu-id="45170-228">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="45170-229">避免此错误的一种方法是从数据库部署中排除用户和角色。</span><span class="sxs-lookup"><span data-stu-id="45170-229">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="45170-230">为此，可以编辑数据库的自动生成脚本的 PreSource 元素，使其包含以下属性：</span><span class="sxs-lookup"><span data-stu-id="45170-230">You can do this by editing the PreSource element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

<span data-ttu-id="45170-231">有关如何编辑项目文件中的 PreSource 元素的信息，请参阅[如何：在项目文件中编辑部署设置](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="45170-231">For information about how to edit the PreSource element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="45170-232">如果你的开发数据库中的用户或角色需要位于目标数据库中，请与你的托管提供商联系以获得帮助。</span><span class="sxs-lookup"><span data-stu-id="45170-232">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="45170-233">在部署过程中运行自定义脚本时出现 SQL Server 超时错误</span><span class="sxs-lookup"><span data-stu-id="45170-233">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-234">方案</span><span class="sxs-lookup"><span data-stu-id="45170-234">Scenario</span></span>

<span data-ttu-id="45170-235">您已经指定了要在部署过程中运行的自定义 SQL 脚本，当 Web 部署运行它们时，它们将超时。</span><span class="sxs-lookup"><span data-stu-id="45170-235">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-236">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-236">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-237">运行具有不同事务模式的多个脚本会导致超时错误。</span><span class="sxs-lookup"><span data-stu-id="45170-237">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="45170-238">默认情况下，自动生成的脚本在事务中运行，但自定义脚本不会运行。</span><span class="sxs-lookup"><span data-stu-id="45170-238">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="45170-239">如果在 "**包/发布 SQL** " 选项卡上选择了 "**从现有数据库提取数据和/或架构**" 选项，并且添加自定义 SQL 脚本，则必须更改某些脚本的事务设置，以便所有脚本都使用相同的事务设置。</span><span class="sxs-lookup"><span data-stu-id="45170-239">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="45170-240">有关详细信息，请参阅[如何：使用 Web 应用程序项目部署数据库](https://msdn.microsoft.com/library/dd465343.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45170-240">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="45170-241">如果已配置事务设置，使所有这些设置都相同但仍然出现此错误，则一种可能的解决方法是单独运行脚本。</span><span class="sxs-lookup"><span data-stu-id="45170-241">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="45170-242">在 "**包/发布**SQL" 选项卡的 "**数据库脚本**" 网格中，清除导致超时错误的脚本的 "**包含**" 复选框，然后发布项目。</span><span class="sxs-lookup"><span data-stu-id="45170-242">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="45170-243">然后返回到 "**数据库脚本**" 网格，选中该脚本的 "**包含**" 复选框，并清除其他脚本的 "**包含**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="45170-243">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="45170-244">然后重新发布项目。</span><span class="sxs-lookup"><span data-stu-id="45170-244">Then publish the project again.</span></span> <span data-ttu-id="45170-245">这一次，当你发布时，只会运行选定的自定义脚本。</span><span class="sxs-lookup"><span data-stu-id="45170-245">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="45170-246">站点清单的流数据尚不可用</span><span class="sxs-lookup"><span data-stu-id="45170-246">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-247">方案</span><span class="sxs-lookup"><span data-stu-id="45170-247">Scenario</span></span>

<span data-ttu-id="45170-248">当使用带有 t （test）选项的*deploy .cmd*文件安装包时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-248">When you are installing a package using the *deploy.cmd* file with the t (test) option, you see the following error message:</span></span>

<span data-ttu-id="45170-249">错误： "sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript" 的流数据尚不可用。</span><span class="sxs-lookup"><span data-stu-id="45170-249">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-250">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-250">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-251">错误消息表示该命令无法生成测试报告。</span><span class="sxs-lookup"><span data-stu-id="45170-251">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="45170-252">但是，如果使用 y （实际安装）选项，则该命令可能运行。</span><span class="sxs-lookup"><span data-stu-id="45170-252">However, the command might run if you use the y (actual installation) option.</span></span> <span data-ttu-id="45170-253">此消息仅指示在测试模式下运行命令时出现问题。</span><span class="sxs-lookup"><span data-stu-id="45170-253">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="45170-254">此应用程序需要 ManagedRuntimeVersion v4。0</span><span class="sxs-lookup"><span data-stu-id="45170-254">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-255">方案</span><span class="sxs-lookup"><span data-stu-id="45170-255">Scenario</span></span>

<span data-ttu-id="45170-256">当你尝试部署时，你会看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-256">When you attempt to deploy, you see the following error message:</span></span>

<span data-ttu-id="45170-257">尝试使用的应用程序池的 "managedRuntimeVersion" 属性设置为 "v2.0"。</span><span class="sxs-lookup"><span data-stu-id="45170-257">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="45170-258">此应用程序需要 "4.0"。</span><span class="sxs-lookup"><span data-stu-id="45170-258">This application requires 'v4.0'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-259">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-259">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-260">IIS 中未安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="45170-260">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="45170-261">如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。</span><span class="sxs-lookup"><span data-stu-id="45170-261">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="45170-262">在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="45170-262">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="45170-263">无法强制转换 DeploymentProviderOptions</span><span class="sxs-lookup"><span data-stu-id="45170-263">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-264">方案</span><span class="sxs-lookup"><span data-stu-id="45170-264">Scenario</span></span>

<span data-ttu-id="45170-265">部署包时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-265">When you are deploying a package, you see the following error message:</span></span>

<span data-ttu-id="45170-266">无法将类型为 "DeploymentProviderOptions" 的对象强制转换为 "DeploymentProviderOptions" 类型。</span><span class="sxs-lookup"><span data-stu-id="45170-266">Unable to cast object of type 'Microsoft.Web.Deployment.DeploymentProviderOptions' to 'Microsoft.Web.Deployment.DeploymentProviderOptions'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-267">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-267">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-268">尝试使用 Web 部署 1.1 UI 从 IIS 管理器部署到安装了 Web 部署2.0 的服务器。</span><span class="sxs-lookup"><span data-stu-id="45170-268">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="45170-269">如果使用 IIS 远程管理工具通过导入包进行部署，请在建立连接时选中 "**可用的新功能**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="45170-269">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="45170-270">（仅当首次建立连接时，才会显示此对话框。</span><span class="sxs-lookup"><span data-stu-id="45170-270">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="45170-271">若要清除该连接并重新启动，请关闭 IIS 管理器，然后通过在命令提示符下输入 inetmgr/reset 来重新启动它。）如果列出的其中一项功能**WEB 部署 UI**，并且版本号低于8，则部署到的服务器可能同时安装了1.1 和2.0 版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="45170-271">To clear the connection and start over, close IIS Manager and start it up again by entering inetmgr /reset at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="45170-272">要从安装了2.0 的客户端进行部署，服务器必须仅安装 Web 部署2.0。</span><span class="sxs-lookup"><span data-stu-id="45170-272">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="45170-273">您必须与您的宿主提供商联系以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="45170-273">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="45170-274">无法加载 SQL Server Compact 的本机组件</span><span class="sxs-lookup"><span data-stu-id="45170-274">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-275">方案</span><span class="sxs-lookup"><span data-stu-id="45170-275">Scenario</span></span>

<span data-ttu-id="45170-276">当你运行部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-276">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="45170-277">无法加载与版本8482的 ADO.NET 提供程序对应的 SQL Server Compact 的本机组件。</span><span class="sxs-lookup"><span data-stu-id="45170-277">Unable to load the native components of SQL Server Compact corresponding to the ADO.NET provider of version 8482.</span></span> <span data-ttu-id="45170-278">安装 SQL Server Compact 的正确版本。</span><span class="sxs-lookup"><span data-stu-id="45170-278">Install the correct version of SQL Server Compact.</span></span> <span data-ttu-id="45170-279">有关更多详细信息，请参阅知识库文章974247。</span><span class="sxs-lookup"><span data-stu-id="45170-279">Refer to KB article 974247 for more details.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-280">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-280">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-281">部署的站点在应用程序的*bin*文件夹下没有*amd64*和*x86*子文件夹，其中包含本机程序集。</span><span class="sxs-lookup"><span data-stu-id="45170-281">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="45170-282">在安装了 SQL Server Compact 的计算机上，本机程序集位于*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*中。</span><span class="sxs-lookup"><span data-stu-id="45170-282">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="45170-283">若要将正确的文件导入到 Visual Studio 项目中正确的文件夹中，最好的方法是安装 NuGet SqlServerCompact 包。</span><span class="sxs-lookup"><span data-stu-id="45170-283">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="45170-284">包安装将添加一个后期生成脚本，用于将本机程序集复制到*amd64*和*x86*。</span><span class="sxs-lookup"><span data-stu-id="45170-284">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="45170-285">但是，若要部署这些文件，必须手动将其包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="45170-285">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="45170-286">有关详细信息，请参阅[部署 SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="45170-286">For more information, see the [Deploying SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="45170-287">Code First 应用程序部署实体框架后出现 "路径无效" 错误</span><span class="sxs-lookup"><span data-stu-id="45170-287">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-288">方案</span><span class="sxs-lookup"><span data-stu-id="45170-288">Scenario</span></span>

<span data-ttu-id="45170-289">部署一个应用程序，该应用程序使用 Entity Framework Code First 迁移和 DBMS （如 SQL Server Compact）将其数据库存储在应用\_Data 文件夹中的文件中。</span><span class="sxs-lookup"><span data-stu-id="45170-289">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="45170-290">你已 Code First 迁移配置为在第一次部署后创建数据库。</span><span class="sxs-lookup"><span data-stu-id="45170-290">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="45170-291">运行应用程序时，会收到类似于以下示例的错误消息：</span><span class="sxs-lookup"><span data-stu-id="45170-291">When you run the application you get an error message like the following example:</span></span>

<span data-ttu-id="45170-292">该路径无效。</span><span class="sxs-lookup"><span data-stu-id="45170-292">The path is not valid.</span></span> <span data-ttu-id="45170-293">检查数据库的目录。</span><span class="sxs-lookup"><span data-stu-id="45170-293">Check the directory for the database.</span></span> <span data-ttu-id="45170-294">[路径 = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]</span><span class="sxs-lookup"><span data-stu-id="45170-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-295">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-295">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-296">Code First 正在尝试创建数据库，但应用\_数据文件夹不存在。</span><span class="sxs-lookup"><span data-stu-id="45170-296">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="45170-297">你在部署时没有*应用\_Data*文件夹中的任何文件，或者在项目属性窗口的 "**包/发布 Web** " 选项卡上选择了 "**排除应用\_数据**"。</span><span class="sxs-lookup"><span data-stu-id="45170-297">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the Project Properties window.</span></span> <span data-ttu-id="45170-298">如果要将文件夹中的文件复制到服务器，部署过程不会在服务器上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="45170-298">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="45170-299">如果已在站点中设置了数据库，则如果在发布配置文件中选择了 "**删除目标位置的其他文件**"，则部署过程将删除文件和*应用\_Data*文件夹本身。</span><span class="sxs-lookup"><span data-stu-id="45170-299">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="45170-300">若要解决此问题，请在*应用\_Data*文件夹中放置一个占位符文件（如 .txt 文件），请确保未选择 "**排除应用"\_数据**并重新部署。</span><span class="sxs-lookup"><span data-stu-id="45170-300">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span>

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="45170-301">"无法使用与其基础 RCW 分离的 COM 对象。"</span><span class="sxs-lookup"><span data-stu-id="45170-301">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-302">方案</span><span class="sxs-lookup"><span data-stu-id="45170-302">Scenario</span></span>

<span data-ttu-id="45170-303">你已成功使用一键式发布来部署你的应用程序，然后你开始收到此错误：</span><span class="sxs-lookup"><span data-stu-id="45170-303">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

<span data-ttu-id="45170-304">Web 部署任务失败。</span><span class="sxs-lookup"><span data-stu-id="45170-304">Web deployment task failed.</span></span> <span data-ttu-id="45170-305">（无法完成对远程代理 URL "<https://serverurl.com/msdeploy.axd?site=sitename>" 的请求。）</span><span class="sxs-lookup"><span data-stu-id="45170-305">(Could not complete the request to remote agent URL '<https://serverurl.com/msdeploy.axd?site=sitename>'.)</span></span>  
 <span data-ttu-id="45170-306">无法完成对远程代理 URL "<https://url/msdeploy.axd?site=sitename>" 的请求。</span><span class="sxs-lookup"><span data-stu-id="45170-306">Could not complete the request to remote agent URL '<https://url/msdeploy.axd?site=sitename>'.</span></span>  
<span data-ttu-id="45170-307">请求已中止：请求已取消。</span><span class="sxs-lookup"><span data-stu-id="45170-307">The request was aborted: The request was canceled.</span></span>  
<span data-ttu-id="45170-308">不能使用与其基础 RCW 分离的 COM 对象。</span><span class="sxs-lookup"><span data-stu-id="45170-308">COM object that has been separated from its underlying RCW cannot be used.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-309">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-309">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-310">若要解决此错误，通常需要关闭并重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="45170-310">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="45170-311">部署失败，因为用于发布的用户凭据没有 setACL 机构</span><span class="sxs-lookup"><span data-stu-id="45170-311">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-312">方案</span><span class="sxs-lookup"><span data-stu-id="45170-312">Scenario</span></span>

<span data-ttu-id="45170-313">发布失败，并显示一条错误消息，指出你没有权限设置文件夹权限（你使用的用户帐户没有 setACL 权限）。</span><span class="sxs-lookup"><span data-stu-id="45170-313">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-314">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-314">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-315">默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="45170-315">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="45170-316">如果你知道站点文件夹上的默认权限是正确的，并且不需要设置，则可以通过将 **&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（影响单个配置文件）或 wpp 文件（以影响所有配置文件）来禁用此行为。</span><span class="sxs-lookup"><span data-stu-id="45170-316">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="45170-317">有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45170-317">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="45170-318">当应用程序尝试写入应用程序文件夹时出现 "拒绝访问" 错误</span><span class="sxs-lookup"><span data-stu-id="45170-318">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-319">方案</span><span class="sxs-lookup"><span data-stu-id="45170-319">Scenario</span></span>

<span data-ttu-id="45170-320">应用程序在尝试创建或编辑其中一个应用程序文件夹中的文件时出错，因为它不具有该文件夹的写权限。</span><span class="sxs-lookup"><span data-stu-id="45170-320">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-321">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-321">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-322">默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="45170-322">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="45170-323">如果你的应用程序需要对子文件夹的写访问权限，你可以设置该文件夹的权限，如此系列中的设置文件夹权限和部署到生产环境教程中所示。</span><span class="sxs-lookup"><span data-stu-id="45170-323">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the Setting Folder Permissions and Deploying to the Production Environment tutorials in this series.</span></span> <span data-ttu-id="45170-324">如果你的应用程序需要对该站点的根文件夹具有写入权限，则必须通过将 **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（以影响单个配置文件）或 wpp 文件（以影响所有配置文件）来防止其在根文件夹上设置只读访问权限。</span><span class="sxs-lookup"><span data-stu-id="45170-324">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="45170-325">有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45170-325">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="45170-326">配置错误-targetFramework 特性引用的版本晚于安装的 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="45170-326">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-327">方案</span><span class="sxs-lookup"><span data-stu-id="45170-327">Scenario</span></span>

<span data-ttu-id="45170-328">已成功发布面向 ASP.NET 4.5 的 web 项目，但当你运行应用程序（在 web.config 文件中将 customErrors 模式设置为 "off"）时，会收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="45170-328">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the customErrors mode set to "off" in the Web.config file) you get the following error:</span></span>

<span data-ttu-id="45170-329">Web.config 文件的 &lt;编译&gt; 元素中的 "targetFramework" 特性仅用于面向 .NET Framework 版本4.0 和更高版本（例如，"&lt;编译 targetFramework =" 4.0 "&gt;"）。</span><span class="sxs-lookup"><span data-stu-id="45170-329">The 'targetFramework' attribute in the &lt;compilation&gt; element of the Web.config file is used only to target version 4.0 and later of the .NET Framework (for example, '&lt;compilation targetFramework="4.0"&gt;').</span></span> <span data-ttu-id="45170-330">"TargetFramework" 属性当前引用的版本高于 .NET Framework 安装的版本。</span><span class="sxs-lookup"><span data-stu-id="45170-330">The 'targetFramework' attribute currently references a version that is later than the installed version of the .NET Framework.</span></span> <span data-ttu-id="45170-331">指定 .NET Framework 的有效目标版本，或者安装 .NET Framework 的所需版本。</span><span class="sxs-lookup"><span data-stu-id="45170-331">Specify a valid target version of the .NET Framework, or install the required version of the .NET Framework.</span></span>

<span data-ttu-id="45170-332">错误页面的 "源错误" 框中突出显示了 web.config 中的以下行：</span><span class="sxs-lookup"><span data-stu-id="45170-332">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

<span data-ttu-id="45170-333">&lt;编译 targetFramework = "4.5"/&gt;</span><span class="sxs-lookup"><span data-stu-id="45170-333">&lt;compilation targetFramework="4.5" /&gt;</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-334">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-334">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-335">服务器不支持 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="45170-335">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="45170-336">请与宿主提供商联系，以确定是否可以添加对 ASP.NET 4.5 的支持。</span><span class="sxs-lookup"><span data-stu-id="45170-336">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="45170-337">如果升级服务器不是一个选项，则必须部署面向 ASP.NET 4 或更早版本的 web 项目。</span><span class="sxs-lookup"><span data-stu-id="45170-337">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.</span></span>

<span data-ttu-id="45170-338">如果将 ASP.NET 4 或更早版本的 web 项目部署到相同的目标，请在 "**发布 web** " 向导的 "**设置**" 选项卡上选中 "**删除目标上的其他文件**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="45170-338">If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="45170-339">如果未选择 "**删除目标中的其他文件**"，则将继续获取配置错误页。</span><span class="sxs-lookup"><span data-stu-id="45170-339">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="45170-340">"项目**属性**" 窗口包含一个 "目标框架" 下拉列表，但不能通过只是将其从 **.NET Framework 4.5**改为 **.NET Framework 4**来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="45170-340">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="45170-341">如果将目标框架更改为早期版本，则该项目仍将引用更高版本的程序集，并且将不会运行。</span><span class="sxs-lookup"><span data-stu-id="45170-341">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="45170-342">你必须手动更改这些引用或创建一个面向 .NET Framework 4 或更早版本的新项目。</span><span class="sxs-lookup"><span data-stu-id="45170-342">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="45170-343">有关详细信息，请参阅网站[的 .NET Framework 目标](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="45170-343">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

## <a name="medium-trust-errors"></a><span data-ttu-id="45170-344">中等信任错误</span><span class="sxs-lookup"><span data-stu-id="45170-344">Medium Trust Errors</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-345">方案</span><span class="sxs-lookup"><span data-stu-id="45170-345">Scenario</span></span>

<span data-ttu-id="45170-346">在生产环境中运行应用程序时，它会获取与中等信任相关的错误。</span><span class="sxs-lookup"><span data-stu-id="45170-346">When you run your application in production, it gets an error related to medium trust.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-347">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-347">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-348">许多第三方托管提供商在中等信任环境下运行你的网站，这意味着不允许这样做。</span><span class="sxs-lookup"><span data-stu-id="45170-348">Many third-party hosting providers run your web site in medium trust, which means that there are some things it isn't allowed to do.</span></span> <span data-ttu-id="45170-349">例如，应用程序代码不能访问 Windows 注册表，也无法读取或写入您的应用程序的文件夹层次结构之外的文件。</span><span class="sxs-lookup"><span data-stu-id="45170-349">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="45170-350">默认情况下，你的应用程序在本地计算机上以*完全信任*的方式运行，这意味着应用程序可以执行在将其部署到生产环境时失败的操作。</span><span class="sxs-lookup"><span data-stu-id="45170-350">By default your application runs in *full trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span>

<span data-ttu-id="45170-351">你可以将应用程序配置为在本地 IIS 环境中的中等信任级别运行，以便进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="45170-351">You can configure the application to run in medium trust in the local IIS environment in order to troubleshoot.</span></span> <span data-ttu-id="45170-352">为此，请打开应用程序的*web.config*文件，并在**system.web**元素中添加一个**信任**元素，如本示例中所示。</span><span class="sxs-lookup"><span data-stu-id="45170-352">To do that, open the application *Web.config* file, and add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

<span data-ttu-id="45170-353">现在，应用程序将在 IIS 中的中等信任环境中运行，即使在本地计算机上也是如此。</span><span class="sxs-lookup"><span data-stu-id="45170-353">The application will now run in medium trust in IIS even on your local computer.</span></span>

<span data-ttu-id="45170-354">如果要部署到 Azure App Service，请不要执行此操作，因为 Azure 不需要中等信任。</span><span class="sxs-lookup"><span data-stu-id="45170-354">Don't do this if you are deploying to Azure App Service, because Azure does not require medium trust.</span></span> <span data-ttu-id="45170-355">在2012年2月编写本教程时，使用此方法使应用程序在中等信任环境下运行将导致 Azure 出错。</span><span class="sxs-lookup"><span data-stu-id="45170-355">At the time this tutorial is being written in February, 2012, using this method to make your application run in medium trust will cause an error in Azure.</span></span>

<span data-ttu-id="45170-356">如果使用 Entity Framework Code First 迁移并且要将部署到在中等信任环境下运行应用程序的宿主提供程序，请确保已安装版本5.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="45170-356">If you are using Entity Framework Code First Migrations and you are deploying to a hosting provider that runs your application in medium trust, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="45170-357">在实体框架版本4.3 中，迁移需要完全信任才能更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="45170-357">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>

## <a name="http-40417-not-found-error"></a><span data-ttu-id="45170-358">"找不到 HTTP 404.17" 错误</span><span class="sxs-lookup"><span data-stu-id="45170-358">HTTP 404.17 Not Found Error</span></span>

### <a name="scenario"></a><span data-ttu-id="45170-359">方案</span><span class="sxs-lookup"><span data-stu-id="45170-359">Scenario</span></span>

<span data-ttu-id="45170-360">当你在 IIS 中的开发计算机上运行部署的站点时，你将看到以下错误消息，报告服务器无法处理 default.aspx：</span><span class="sxs-lookup"><span data-stu-id="45170-360">When you run the deployed site on your development computer in IIS, you see the following error message reporting that the server can't process Default.aspx:</span></span>

<span data-ttu-id="45170-361">HTTP 错误 404.17-未找到</span><span class="sxs-lookup"><span data-stu-id="45170-361">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="45170-362">请求的内容将显示为脚本，而不会由静态文件处理程序提供。</span><span class="sxs-lookup"><span data-stu-id="45170-362">The requested content appears to be script and will not be served by the static file handler.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="45170-363">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="45170-363">Possible Cause and Solution</span></span>

<span data-ttu-id="45170-364">ASP.NET 4.5 可能未安装在您的计算机上。</span><span class="sxs-lookup"><span data-stu-id="45170-364">ASP.NET 4.5 might not be installed on your computer.</span></span> <span data-ttu-id="45170-365">请参阅本系列中的部署到 IIS 作为测试环境教程教程中的步骤，其中介绍了如何安装 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="45170-365">See the steps in the Deploying to IIS as a Test Environment tutorial in this series that explain how to install ASP.NET 4.5.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="45170-366">上一页</span><span class="sxs-lookup"><span data-stu-id="45170-366">Previous</span></span>](deploying-extra-files.md)
