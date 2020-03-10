---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：疑难解答（12/12） |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424034"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a><span data-ttu-id="84ed6-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：疑难解答（12/12）</span><span class="sxs-lookup"><span data-stu-id="84ed6-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Troubleshooting (12 of 12)</span></span>

<span data-ttu-id="84ed6-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="84ed6-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="84ed6-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="84ed6-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="84ed6-106">本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="84ed6-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="84ed6-107">如果安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="84ed6-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="84ed6-108">有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="84ed6-109">有关显示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Microsoft Azure 网站，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

<span data-ttu-id="84ed6-110">本页介绍使用 Visual Studio 部署 ASP.NET web 应用程序时可能出现的一些常见问题。</span><span class="sxs-lookup"><span data-stu-id="84ed6-110">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="84ed6-111">对于每个问题，都提供了一个或多个可能的原因和相应的解决方案。</span><span class="sxs-lookup"><span data-stu-id="84ed6-111">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="84ed6-112">"/" 应用程序中的服务器错误-当前自定义错误设置阻止远程查看错误的详细信息</span><span class="sxs-lookup"><span data-stu-id="84ed6-112">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-113">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-113">Scenario</span></span>

<span data-ttu-id="84ed6-114">将站点部署到远程主机之后，会收到一条错误消息，其中提及了 Web.config 文件中的 customErrors 设置，但未指示错误的实际原因：</span><span class="sxs-lookup"><span data-stu-id="84ed6-114">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-115">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-115">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-116">默认情况下，仅当你的 web 应用程序在本地计算机上运行时，ASP.NET 才会显示详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="84ed6-116">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="84ed6-117">通常，当您的 web 应用程序在 Internet 上公开可用时，您不想显示详细的错误信息，因为黑客可能能够利用此信息来查找应用程序中的漏洞。</span><span class="sxs-lookup"><span data-stu-id="84ed6-117">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="84ed6-118">但是，在部署站点或更新站点时，有时会出现问题，需要获取实际的错误消息。</span><span class="sxs-lookup"><span data-stu-id="84ed6-118">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="84ed6-119">若要使应用程序能够在远程主机上运行时显示详细的错误消息，请编辑 Web.config 文件以将 `customErrors` 模式设置为 off，重新部署应用程序，然后再次运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="84ed6-119">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set `customErrors` mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="84ed6-120">如果应用程序的 web.config 文件在 `system.web` 元素中具有 `customErrors` 元素，请将 `mode` 特性更改为 "off"。</span><span class="sxs-lookup"><span data-stu-id="84ed6-120">If the application Web.config file has a `customErrors` element in the `system.web` element, change the `mode` attribute to "off".</span></span> <span data-ttu-id="84ed6-121">否则，在 `mode` 特性设置为 "off" 的 `system.web` 元素中添加 `customErrors` 元素，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="84ed6-121">Otherwise add a `customErrors` element in the `system.web` element with the `mode` attribute set to "off", as shown in the following example:</span></span>

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. <span data-ttu-id="84ed6-122">部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="84ed6-122">Deploy the application.</span></span>
3. <span data-ttu-id="84ed6-123">运行该应用程序，并重复您之前执行的任何导致错误的操作。</span><span class="sxs-lookup"><span data-stu-id="84ed6-123">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="84ed6-124">现在，你可以看到实际的错误消息是什么。</span><span class="sxs-lookup"><span data-stu-id="84ed6-124">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="84ed6-125">解决错误后，还原原始 `customErrors` 设置并重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="84ed6-125">When you have resolved the error, restore the original `customErrors` setting and redeploy the application.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="84ed6-126">使用 SQL Server Compact 的网页中的访问被拒绝</span><span class="sxs-lookup"><span data-stu-id="84ed6-126">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-127">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-127">Scenario</span></span>

<span data-ttu-id="84ed6-128">当你部署使用 SQL Server Compact 的站点，并且在已部署的站点中运行访问该数据库的页面时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-128">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-129">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-129">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-130">服务器上的网络服务帐户需要能够读取*bin\amd64*或*bin\x86*文件夹中的 SQL 服务压缩本机二进制文件，但它不具有对这些文件夹的读取权限。</span><span class="sxs-lookup"><span data-stu-id="84ed6-130">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="84ed6-131">设置*bin*文件夹的 "网络服务的读取权限"，并确保将权限扩展到子文件夹。</span><span class="sxs-lookup"><span data-stu-id="84ed6-131">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="84ed6-132">由于权限不足而无法读取配置文件</span><span class="sxs-lookup"><span data-stu-id="84ed6-132">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-133">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-133">Scenario</span></span>

<span data-ttu-id="84ed6-134">单击 Visual Studio 的 "发布" 按钮将应用程序部署到本地计算机上的 IIS 后，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-134">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-135">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-135">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-136">若要在本地计算机上使用一键式 "发布到 IIS"，必须使用管理员权限运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="84ed6-136">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="84ed6-137">关闭 Visual Studio 并以管理员权限重新启动它。</span><span class="sxs-lookup"><span data-stu-id="84ed6-137">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="84ed6-138">无法连接到目标计算机 .。。使用指定的进程</span><span class="sxs-lookup"><span data-stu-id="84ed6-138">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-139">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-139">Scenario</span></span>

<span data-ttu-id="84ed6-140">单击 Visual Studio 的 "发布" 按钮以部署应用程序时，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-140">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-141">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-141">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-142">代理服务器中断了与目标服务器的通信。</span><span class="sxs-lookup"><span data-stu-id="84ed6-142">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="84ed6-143">在 Windows "控制面板" 或 Internet Explorer 中，选择 " **Internet 选项**"，然后选择 "**连接**" 选项卡。在 " **Internet 属性**" 对话框中，单击 " **LAN 设置**"。</span><span class="sxs-lookup"><span data-stu-id="84ed6-143">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="84ed6-144">在 "局域网 **（LAN）设置**" 对话框中，清除 "**自动检测设置**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="84ed6-144">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="84ed6-145">然后再次单击 "发布" 按钮。</span><span class="sxs-lookup"><span data-stu-id="84ed6-145">Then click the publish button again.</span></span>

<span data-ttu-id="84ed6-146">如果问题仍然存在，请与系统管理员联系，以确定可对代理或防火墙设置执行的操作。</span><span class="sxs-lookup"><span data-stu-id="84ed6-146">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="84ed6-147">发生此问题的原因是 Web 部署为 Web 管理服务部署使用非标准端口（8172）;对于其他连接，Web 部署使用端口80。</span><span class="sxs-lookup"><span data-stu-id="84ed6-147">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="84ed6-148">部署到第三方托管提供程序时，通常使用 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="84ed6-148">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="84ed6-149">默认的 .NET 4.0 应用程序池不存在</span><span class="sxs-lookup"><span data-stu-id="84ed6-149">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-150">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-150">Scenario</span></span>

<span data-ttu-id="84ed6-151">部署需要 .NET Framework 4 的应用程序时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-151">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-152">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-152">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-153">IIS 中未安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="84ed6-153">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="84ed6-154">如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。</span><span class="sxs-lookup"><span data-stu-id="84ed6-154">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="84ed6-155">在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="84ed6-155">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

<span data-ttu-id="84ed6-156">你可能还需要手动设置默认应用程序池的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="84ed6-156">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="84ed6-157">有关详细信息，请参阅 "[以测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) " 教程。</span><span class="sxs-lookup"><span data-stu-id="84ed6-157">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="84ed6-158">初始化字符串的格式不符合从索引0处开始的规范。</span><span class="sxs-lookup"><span data-stu-id="84ed6-158">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-159">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-159">Scenario</span></span>

<span data-ttu-id="84ed6-160">使用一键式发布部署应用程序后，在运行访问数据库的页时，会收到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-160">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-161">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-161">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-162">在部署*的站点*中打开 web.config 文件，然后检查连接字符串值是否以 `$(ReplaceableToken_`开头，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="84ed6-162">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplaceableToken_`, as in the following example:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

<span data-ttu-id="84ed6-163">如果连接字符串与此示例类似，则编辑项目文件，并将以下属性添加到适用于所有生成配置的 `PropertyGroup` 元素：</span><span class="sxs-lookup"><span data-stu-id="84ed6-163">If the connection strings look like this example, edit the project file and add the following property to the `PropertyGroup` element that is for all build configurations:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

<span data-ttu-id="84ed6-164">然后重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="84ed6-164">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="84ed6-165">HTTP 500 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="84ed6-165">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-166">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-166">Scenario</span></span>

<span data-ttu-id="84ed6-167">当你运行部署的站点时，你将看到以下错误消息，其中没有指示错误原因的特定信息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-167">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-168">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-168">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-169">出现500错误的原因有很多，但如果您遵循这些教程，其中一种可能的原因是您将 XML 元素放在一个 XML 转换文件的错误位置。</span><span class="sxs-lookup"><span data-stu-id="84ed6-169">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the XML transformation files.</span></span> <span data-ttu-id="84ed6-170">例如，如果将插入 `<location>` 元素的转换置于 `<system.web>` 下而不是直接在 `<configuration>`下，则会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="84ed6-170">For example, you would get this error if you put the transformation that inserts a `<location>` element under `<system.web>` instead of directly under `<configuration>`.</span></span> <span data-ttu-id="84ed6-171">这种情况下的解决方案是更正 XML 转换文件并重新部署。</span><span class="sxs-lookup"><span data-stu-id="84ed6-171">The solution in that case is to correct the XML transformation file and redeploy.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="84ed6-172">HTTP 500.21 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="84ed6-172">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-173">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-173">Scenario</span></span>

<span data-ttu-id="84ed6-174">当你运行部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-174">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-175">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-175">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-176">部署的站点的目标为 ASP.NET 4，但未在服务器上的 IIS 中注册 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="84ed6-176">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="84ed6-177">在服务器上打开提升的命令提示符，并通过运行以下命令来注册 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="84ed6-177">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

<span data-ttu-id="84ed6-178">你可能还需要手动设置默认应用程序池的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="84ed6-178">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="84ed6-179">有关详细信息，请参阅 "[以测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) " 教程。</span><span class="sxs-lookup"><span data-stu-id="84ed6-179">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a><span data-ttu-id="84ed6-180">登录无法在应用\_数据中打开 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="84ed6-180">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-181">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-181">Scenario</span></span>

<span data-ttu-id="84ed6-182">在应用中*将 web.config 文件连接*字符串更新为指向 SQL Server Express 数据库的 *.Mdf*文件 *\_Data*文件夹，并且首次运行应用程序时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-182">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-183">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-183">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-184">即使删除了以前存在的数据库的 *.mdf*文件， *.mdf*文件的名称也不能与计算机上存在的任何 SQL Server Express 数据库的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="84ed6-184">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="84ed6-185">将 *.mdf*文件的名称更改为从未用作数据库名称的名称，并更改*web.config*文件以使用新名称。</span><span class="sxs-lookup"><span data-stu-id="84ed6-185">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="84ed6-186">作为替代方法，可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除以前存在的 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="84ed6-186">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="84ed6-187">无法检查模型的兼容性</span><span class="sxs-lookup"><span data-stu-id="84ed6-187">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-188">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-188">Scenario</span></span>

<span data-ttu-id="84ed6-189">已*将 web.config 文件连接*字符串更新为指向新的 SQL Server Express 数据库，并且首次运行应用程序时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-189">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-190">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-190">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-191">如果在您的计算机上曾经使用过您放置在 web.config 文件中的数据库名称，则可能已经存在包含某些表的数据库。</span><span class="sxs-lookup"><span data-stu-id="84ed6-191">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="84ed6-192">选择之前未在计算机上使用的新名称，*然后将 web.config 文件更改*为指向 "使用此新数据库名称"。</span><span class="sxs-lookup"><span data-stu-id="84ed6-192">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="84ed6-193">作为替代方法，可以使用[SQL Server Express 实用工具](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除现有数据库。</span><span class="sxs-lookup"><span data-stu-id="84ed6-193">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="84ed6-194">脚本尝试创建用户或角色时出现 SQL 错误</span><span class="sxs-lookup"><span data-stu-id="84ed6-194">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-195">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-195">Scenario</span></span>

<span data-ttu-id="84ed6-196">你使用的是在 "**包/发布 SQL** " 选项卡上配置的数据库部署，在部署过程中运行的 SQL 脚本包含 "创建用户" 或 "创建角色" 命令，在执行这些命令时脚本执行将失败。</span><span class="sxs-lookup"><span data-stu-id="84ed6-196">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="84ed6-197">您可能会看到更详细的消息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84ed6-197">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

<span data-ttu-id="84ed6-198">如果在 "**发布 Web** " 向导而不是 "**包/发布 SQL** " 选项卡中配置数据库部署后发生此错误，请在[配置和部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)论坛中创建一个线程，该解决方案将添加到此故障排除页。</span><span class="sxs-lookup"><span data-stu-id="84ed6-198">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-199">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-199">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-200">用于执行部署的用户帐户没有创建用户或角色的权限。</span><span class="sxs-lookup"><span data-stu-id="84ed6-200">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="84ed6-201">例如，托管公司可以将 `db_datareader`、`db_datawriter`和 `db_ddladmin` 角色分配给它为你设置的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="84ed6-201">For example, the hosting company might assign the `db_datareader`, `db_datawriter`, and `db_ddladmin` roles to the user account that it sets up for you.</span></span> <span data-ttu-id="84ed6-202">它们足以用于创建大多数数据库对象，但不能用于创建用户或角色。</span><span class="sxs-lookup"><span data-stu-id="84ed6-202">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="84ed6-203">避免此错误的一种方法是从数据库部署中排除用户和角色。</span><span class="sxs-lookup"><span data-stu-id="84ed6-203">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="84ed6-204">为此，可以编辑数据库的自动生成脚本的 `PreSource` 元素，使其包含以下属性：</span><span class="sxs-lookup"><span data-stu-id="84ed6-204">You can do this by editing the `PreSource` element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

<span data-ttu-id="84ed6-205">有关如何编辑项目文件中的 `PreSource` 元素的信息，请参阅[如何：在项目文件中编辑部署设置](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-205">For information about how to edit the `PreSource` element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="84ed6-206">如果你的开发数据库中的用户或角色需要位于目标数据库中，请与你的托管提供商联系以获得帮助。</span><span class="sxs-lookup"><span data-stu-id="84ed6-206">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="84ed6-207">在部署过程中运行自定义脚本时出现 SQL Server 超时错误</span><span class="sxs-lookup"><span data-stu-id="84ed6-207">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-208">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-208">Scenario</span></span>

<span data-ttu-id="84ed6-209">您已经指定了要在部署过程中运行的自定义 SQL 脚本，当 Web 部署运行它们时，它们将超时。</span><span class="sxs-lookup"><span data-stu-id="84ed6-209">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-210">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-210">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-211">运行具有不同事务模式的多个脚本会导致超时错误。</span><span class="sxs-lookup"><span data-stu-id="84ed6-211">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="84ed6-212">默认情况下，自动生成的脚本在事务中运行，但自定义脚本不会运行。</span><span class="sxs-lookup"><span data-stu-id="84ed6-212">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="84ed6-213">如果在 "**包/发布 SQL** " 选项卡上选择了 "**从现有数据库提取数据和/或架构**" 选项，并且添加自定义 SQL 脚本，则必须更改某些脚本的事务设置，以便所有脚本都使用相同的事务设置。</span><span class="sxs-lookup"><span data-stu-id="84ed6-213">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="84ed6-214">有关详细信息，请参阅[如何：使用 Web 应用程序项目部署数据库](https://msdn.microsoft.com/library/dd465343.aspx)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-214">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="84ed6-215">如果已配置事务设置，使所有这些设置都相同但仍然出现此错误，则一种可能的解决方法是单独运行脚本。</span><span class="sxs-lookup"><span data-stu-id="84ed6-215">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="84ed6-216">在 "**包/发布**SQL" 选项卡的 "**数据库脚本**" 网格中，清除导致超时错误的脚本的 "**包含**" 复选框，然后发布项目。</span><span class="sxs-lookup"><span data-stu-id="84ed6-216">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="84ed6-217">然后返回到 "**数据库脚本**" 网格，选中该脚本的 "**包含**" 复选框，并清除其他脚本的 "**包含**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="84ed6-217">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="84ed6-218">然后重新发布项目。</span><span class="sxs-lookup"><span data-stu-id="84ed6-218">Then publish the project again.</span></span> <span data-ttu-id="84ed6-219">这一次，当你发布时，只会运行选定的自定义脚本。</span><span class="sxs-lookup"><span data-stu-id="84ed6-219">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="84ed6-220">站点清单的流数据尚不可用</span><span class="sxs-lookup"><span data-stu-id="84ed6-220">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-221">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-221">Scenario</span></span>

<span data-ttu-id="84ed6-222">使用带有 `t` （test）选项的 *.deploy .cmd*文件安装包时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-222">When you are installing a package using the *deploy.cmd* file with the `t` (test) option, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-223">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-223">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-224">错误消息表示该命令无法生成测试报告。</span><span class="sxs-lookup"><span data-stu-id="84ed6-224">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="84ed6-225">但是，如果使用 `y` （实际安装）选项，则该命令可能运行。</span><span class="sxs-lookup"><span data-stu-id="84ed6-225">However, the command might run if you use the `y` (actual installation) option.</span></span> <span data-ttu-id="84ed6-226">此消息仅指示在测试模式下运行命令时出现问题。</span><span class="sxs-lookup"><span data-stu-id="84ed6-226">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="84ed6-227">此应用程序需要 ManagedRuntimeVersion v4。0</span><span class="sxs-lookup"><span data-stu-id="84ed6-227">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-228">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-228">Scenario</span></span>

<span data-ttu-id="84ed6-229">当你尝试部署时，你会看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-229">When you attempt to deploy, you see the following error message:</span></span>

 <span data-ttu-id="84ed6-230">错误： "sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript" 的流数据尚不可用。</span><span class="sxs-lookup"><span data-stu-id="84ed6-230">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span> <span data-ttu-id="84ed6-231">尝试使用的应用程序池的 "managedRuntimeVersion" 属性设置为 "v2.0"。</span><span class="sxs-lookup"><span data-stu-id="84ed6-231">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="84ed6-232">此应用程序需要 "4.0"。</span><span class="sxs-lookup"><span data-stu-id="84ed6-232">This application requires 'v4.0'.</span></span> 

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-233">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-233">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-234">IIS 中未安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="84ed6-234">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="84ed6-235">如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。</span><span class="sxs-lookup"><span data-stu-id="84ed6-235">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="84ed6-236">在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：</span><span class="sxs-lookup"><span data-stu-id="84ed6-236">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="84ed6-237">无法强制转换 DeploymentProviderOptions</span><span class="sxs-lookup"><span data-stu-id="84ed6-237">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-238">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-238">Scenario</span></span>

<span data-ttu-id="84ed6-239">部署包时，将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-239">When you are deploying a package, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-240">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-240">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-241">尝试使用 Web 部署 1.1 UI 从 IIS 管理器部署到安装了 Web 部署2.0 的服务器。</span><span class="sxs-lookup"><span data-stu-id="84ed6-241">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="84ed6-242">如果使用 IIS 远程管理工具通过导入包进行部署，请在建立连接时选中 "**可用的新功能**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="84ed6-242">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="84ed6-243">（仅当首次建立连接时，才会显示此对话框。</span><span class="sxs-lookup"><span data-stu-id="84ed6-243">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="84ed6-244">若要清除连接并重新启动，请关闭 IIS 管理器，然后通过在命令提示符下输入 `inetmgr /reset` 来重新启动。）如果列出的其中一项功能**WEB 部署 UI**，并且版本号低于8，则部署到的服务器可能同时安装了1.1 和2.0 版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="84ed6-244">To clear the connection and start over, close IIS Manager and start it up again by entering `inetmgr /reset` at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="84ed6-245">要从安装了2.0 的客户端进行部署，服务器必须仅安装 Web 部署2.0。</span><span class="sxs-lookup"><span data-stu-id="84ed6-245">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="84ed6-246">您必须与您的宿主提供商联系以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="84ed6-246">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="84ed6-247">无法加载 SQL Server Compact 的本机组件</span><span class="sxs-lookup"><span data-stu-id="84ed6-247">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-248">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-248">Scenario</span></span>

<span data-ttu-id="84ed6-249">当你运行部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-249">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-250">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-250">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-251">部署的站点在应用程序的*bin*文件夹下没有*amd64*和*x86*子文件夹，其中包含本机程序集。</span><span class="sxs-lookup"><span data-stu-id="84ed6-251">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="84ed6-252">在安装了 SQL Server Compact 的计算机上，本机程序集位于*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*中。</span><span class="sxs-lookup"><span data-stu-id="84ed6-252">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="84ed6-253">若要将正确的文件导入到 Visual Studio 项目中正确的文件夹中，最好的方法是安装 NuGet SqlServerCompact 包。</span><span class="sxs-lookup"><span data-stu-id="84ed6-253">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="84ed6-254">包安装将添加一个后期生成脚本，用于将本机程序集复制到*amd64*和*x86*。</span><span class="sxs-lookup"><span data-stu-id="84ed6-254">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="84ed6-255">但是，若要部署这些文件，必须手动将其包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="84ed6-255">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="84ed6-256">有关详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="84ed6-256">For more information, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="84ed6-257">Code First 应用程序部署实体框架后出现 "路径无效" 错误</span><span class="sxs-lookup"><span data-stu-id="84ed6-257">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-258">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-258">Scenario</span></span>

<span data-ttu-id="84ed6-259">部署一个应用程序，该应用程序使用 Entity Framework Code First 迁移和 DBMS （如 SQL Server Compact）将其数据库存储在应用\_Data 文件夹中的文件中。</span><span class="sxs-lookup"><span data-stu-id="84ed6-259">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="84ed6-260">你已 Code First 迁移配置为在第一次部署后创建数据库。</span><span class="sxs-lookup"><span data-stu-id="84ed6-260">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="84ed6-261">运行应用程序时，会收到类似于以下示例的错误消息：</span><span class="sxs-lookup"><span data-stu-id="84ed6-261">When you run the application you get an error message like the following example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-262">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-262">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-263">Code First 正在尝试创建数据库，但应用\_数据文件夹不存在。</span><span class="sxs-lookup"><span data-stu-id="84ed6-263">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="84ed6-264">你在部署时没有*应用\_Data*文件夹中的任何文件，或者在**项目属性**窗口的 "**打包/发布 Web** " 选项卡上选择了 "**排除应用\_数据**"。</span><span class="sxs-lookup"><span data-stu-id="84ed6-264">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the **Project Properties** window.</span></span> <span data-ttu-id="84ed6-265">如果要将文件夹中的文件复制到服务器，部署过程不会在服务器上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="84ed6-265">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="84ed6-266">如果已在站点中设置了数据库，则如果在发布配置文件中选择了 "**删除目标位置的其他文件**"，则部署过程将删除文件和*应用\_Data*文件夹本身。</span><span class="sxs-lookup"><span data-stu-id="84ed6-266">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="84ed6-267">若要解决此问题，请在*应用\_Data*文件夹中放置一个占位符文件（如 .txt 文件），请确保未选择 "**排除应用"\_数据**并重新部署。</span><span class="sxs-lookup"><span data-stu-id="84ed6-267">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span> 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="84ed6-268">"无法使用与其基础 RCW 分离的 COM 对象。"</span><span class="sxs-lookup"><span data-stu-id="84ed6-268">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-269">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-269">Scenario</span></span>

<span data-ttu-id="84ed6-270">你已成功使用一键式发布来部署你的应用程序，然后你开始收到此错误：</span><span class="sxs-lookup"><span data-stu-id="84ed6-270">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-271">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-271">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-272">若要解决此错误，通常需要关闭并重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="84ed6-272">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="84ed6-273">部署失败，因为用于发布的用户凭据没有 setACL 机构</span><span class="sxs-lookup"><span data-stu-id="84ed6-273">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-274">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-274">Scenario</span></span>

<span data-ttu-id="84ed6-275">发布失败，并显示一条错误消息，指出你没有权限设置文件夹权限（你使用的用户帐户没有 setACL 权限）。</span><span class="sxs-lookup"><span data-stu-id="84ed6-275">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-276">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-276">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-277">默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="84ed6-277">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="84ed6-278">如果你知道站点文件夹上的默认权限是正确的，并且不需要设置，则可以通过将 **&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（影响单个配置文件）或 wpp 文件（以影响所有配置文件）来禁用此行为。</span><span class="sxs-lookup"><span data-stu-id="84ed6-278">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="84ed6-279">有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-279">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="84ed6-280">当应用程序尝试写入应用程序文件夹时出现 "拒绝访问" 错误</span><span class="sxs-lookup"><span data-stu-id="84ed6-280">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-281">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-281">Scenario</span></span>

<span data-ttu-id="84ed6-282">应用程序在尝试创建或编辑其中一个应用程序文件夹中的文件时出错，因为它不具有该文件夹的写权限。</span><span class="sxs-lookup"><span data-stu-id="84ed6-282">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-283">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-283">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-284">默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="84ed6-284">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="84ed6-285">如果你的应用程序需要对子文件夹的写访问权限，你可以设置该文件夹的权限，如[设置文件夹权限](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)和[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中所示。</span><span class="sxs-lookup"><span data-stu-id="84ed6-285">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the [Setting Folder Permissions](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) and [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorials.</span></span> <span data-ttu-id="84ed6-286">如果你的应用程序需要对该站点的根文件夹具有写入权限，则必须通过将 **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（以影响单个配置文件）或 wpp 文件（以影响所有配置文件）来防止其在根文件夹上设置只读访问权限。</span><span class="sxs-lookup"><span data-stu-id="84ed6-286">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="84ed6-287">有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-287">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span> <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="84ed6-288">配置错误-targetFramework 特性引用的版本晚于安装的 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="84ed6-288">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="84ed6-289">方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-289">Scenario</span></span>

<span data-ttu-id="84ed6-290">已成功发布面向 ASP.NET 4.5 的 web 项目，但当你运行应用程序时（在 web.config 文件中将 `customErrors` 模式设置为 "off"），会收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="84ed6-290">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the `customErrors` mode set to "off" in the Web.config file) you get the following error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

<span data-ttu-id="84ed6-291">错误页面的 "源错误" 框中突出显示了 web.config 中的以下行：</span><span class="sxs-lookup"><span data-stu-id="84ed6-291">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="84ed6-292">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="84ed6-292">Possible Cause and Solution</span></span>

<span data-ttu-id="84ed6-293">服务器不支持 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="84ed6-293">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="84ed6-294">请与宿主提供商联系，以确定是否可以添加对 ASP.NET 4.5 的支持。</span><span class="sxs-lookup"><span data-stu-id="84ed6-294">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="84ed6-295">如果升级服务器不是一个选项，则必须部署面向 ASP.NET 4 或更早版本的 web 项目。如果将 ASP.NET 4 或更早版本的 web 项目部署到相同的目标，请在 "**发布 web** " 向导的 "**设置**" 选项卡上选中 "**删除目标上的其他文件**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="84ed6-295">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="84ed6-296">如果未选择 "**删除目标中的其他文件**"，则将继续获取配置错误页。</span><span class="sxs-lookup"><span data-stu-id="84ed6-296">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="84ed6-297">"项目**属性**" 窗口包含一个 "目标框架" 下拉列表，但不能通过只是将其从 **.NET Framework 4.5**改为 **.NET Framework 4**来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="84ed6-297">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="84ed6-298">如果将目标框架更改为早期版本，则该项目仍将引用更高版本的程序集，并且将不会运行。</span><span class="sxs-lookup"><span data-stu-id="84ed6-298">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="84ed6-299">你必须手动更改这些引用或创建一个面向 .NET Framework 4 或更早版本的新项目。</span><span class="sxs-lookup"><span data-stu-id="84ed6-299">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="84ed6-300">有关详细信息，请参阅网站[的 .NET Framework 目标](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="84ed6-300">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="84ed6-301">上一页</span><span class="sxs-lookup"><span data-stu-id="84ed6-301">Previous</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
