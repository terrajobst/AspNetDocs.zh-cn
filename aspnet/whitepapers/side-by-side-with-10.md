---
uid: whitepapers/side-by-side-with-10
title: ASP.NET 并行执行 .NET Framework 1.0 和 1.1 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍如何在计算机上安装 .NET 1.0 和 .NET 1.1，使 ASP.NET Web 应用程序能够在任一版本的 fram 上运行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513830"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="eab84-103">.NET Framework 1.0 和 .NET Framework 1.1 的 ASP.NET 并行执行</span><span class="sxs-lookup"><span data-stu-id="eab84-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="eab84-104">本白皮书介绍如何在计算机上安装 .NET 1.0 和 .NET 1.1，以允许 ASP.NET Web 应用程序在任一版本的 framework 上运行。</span><span class="sxs-lookup"><span data-stu-id="eab84-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="eab84-105">适用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="eab84-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="eab84-106">在 ASP.NET 中，当应用程序安装在同一台计算机上时，它们被称为并行运行，但使用不同版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="eab84-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="eab84-107">以下主题介绍如何为并行执行配置 ASP.NET 应用程序，并提供有关的详细步骤：</span><span class="sxs-lookup"><span data-stu-id="eab84-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="eab84-108">维护你的 Web 应用程序在安装过程中 .NET Framework 版本1.0 的映射</span><span class="sxs-lookup"><span data-stu-id="eab84-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="eab84-109">将 Web 应用程序映射到 .NET Framework 的特定版本</span><span class="sxs-lookup"><span data-stu-id="eab84-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="eab84-110">查找网站正在使用的 .NET Framework 的版本</span><span class="sxs-lookup"><span data-stu-id="eab84-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="eab84-111">传统上，在计算机上更新组件或应用程序时，将删除较旧的版本，并将其替换为较新的版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="eab84-112">如果新版本与以前的版本不兼容，则通常会断开使用组件或应用程序的其他应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="eab84-113">.NET Framework 支持并行执行，这允许同时在同一台计算机上安装程序集或应用程序的多个版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="eab84-114">由于可以同时安装多个版本，因此托管应用程序可以选择使用哪个版本，而不影响使用不同版本的应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="eab84-115">默认情况下，在安装 .NET Framework 版本1.1 的过程中，所有现有的 ASP.NET 应用程序都将自动重新配置为使用 .NET Framework 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="eab84-116">如果你不希望 ASP.NET 应用程序默认 .NET Framework 1.1，请单击[此处](#1)了解如何在安装过程中阻止此操作。</span><span class="sxs-lookup"><span data-stu-id="eab84-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="eab84-117">如果将 Web 服务器更新为 .NET Framework 1.1，并且希望一个或多个 Web 应用程序运行 .NET Framework 1.0，则需要更新 Internet Information Services （IIS）脚本映射。</span><span class="sxs-lookup"><span data-stu-id="eab84-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="eab84-118">脚本映射是将特定 Web 应用程序的 .aspx 文件扩展名映射到 .NET Framework 版本的机制。</span><span class="sxs-lookup"><span data-stu-id="eab84-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="eab84-119">单击[此处](#2)了解如何将 Web 应用程序映射到 .NET Framework 的特定版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="eab84-120">你可以使用 Internet 信息管理器或 ASP.NET IIS 注册工具（Aspnet\_regiis）来找出哪个 .NET Framework 版本正在运行特定的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="eab84-121">单击[此处](#3)了解如何查找网站正在使用的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="eab84-122">迁移到 .NET Framework 1.1 时，需要考虑的一个事项是 .NET Framework 的每个版本都使用其自己的 Machine.config 文件。</span><span class="sxs-lookup"><span data-stu-id="eab84-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="eab84-123">因此，如果 Web 管理员已对 machine.config 文件进行了更改，则这些更改必须迁移到 .NET Framework 1.1 Machine.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="eab84-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="eab84-124">在安装过程中维护 Web 应用程序到 .NET Framework 1.0 的映射</span><span class="sxs-lookup"><span data-stu-id="eab84-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="eab84-125">默认情况下，在安装过程中将自动重新配置所有现有的 ASP.NET 应用程序，以使用较新版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="eab84-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="eab84-126">使用较新版本的 .NET Framework，应用程序可以充分利用新版本中包含的改进和新增功能。</span><span class="sxs-lookup"><span data-stu-id="eab84-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="eab84-127">同时，Web 管理员（可能需要对更新的应用程序进行精细控制）可以防止安装 .NET Framework 期间自动重映射所有现有的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="eab84-128">若要防止整个 ASP.NET 应用程序自动重新映射到较新版本的 .NET Framework，Web 管理员可以在 Dotnetfx.exe 安装程序中使用/noaspupgrade 命令行选项。</span><span class="sxs-lookup"><span data-stu-id="eab84-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="eab84-129">**阻止将 ASP.NET 应用程序的总重新映射到较新版本**</span><span class="sxs-lookup"><span data-stu-id="eab84-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="eab84-130">转到“开始”。</span><span class="sxs-lookup"><span data-stu-id="eab84-130">Go to **Start**.</span></span>
2. <span data-ttu-id="eab84-131">单击 "**运行**"。</span><span class="sxs-lookup"><span data-stu-id="eab84-131">Click on **run**.</span></span>
3. <span data-ttu-id="eab84-132">键入“cmd”。</span><span class="sxs-lookup"><span data-stu-id="eab84-132">Type **cmd**.</span></span>
4. <span data-ttu-id="eab84-133">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="eab84-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="eab84-134">在命令提示符下，键入以下行开始安装 .NET Framework： **dotnetfx.exe/c： "install/noaspupgrade？"** 。</span><span class="sxs-lookup"><span data-stu-id="eab84-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="eab84-135">在 Microsoft .NET Framework 1.1 安装程序中单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="eab84-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="eab84-136">这将启动 .NET Framework 1.1 的设置过程。</span><span class="sxs-lookup"><span data-stu-id="eab84-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="eab84-137">将 Web 应用程序映射到 .NET Framework 的特定版本</span><span class="sxs-lookup"><span data-stu-id="eab84-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="eab84-138">.NET Framework 的每个版本都包含一个 ASP.NET IIS 注册工具（Aspnet\_regiis）的版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="eab84-139">管理员可以使用此工具指定在 .NET Framework 的特定版本下运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="eab84-140">这称为将 Web 应用程序映射到 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="eab84-141">管理员必须选择与要与 Web 应用程序关联的 .NET Framework 版本对应的 Aspnet\_regiis。</span><span class="sxs-lookup"><span data-stu-id="eab84-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="eab84-142">例如，要指定网站使用 .NET Framework 1.1 的管理员必须使用 .NET Framework 1.1 随附的 Aspnet\_regiis。</span><span class="sxs-lookup"><span data-stu-id="eab84-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="eab84-143">1\.0 版的 Aspnet\_regiis 位于：</span><span class="sxs-lookup"><span data-stu-id="eab84-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="eab84-144">C:\WINDOWS\Microsoft.NET\Framework\\**v v1.0.3705**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="eab84-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="eab84-145">版本1的 Aspnet\_regiis，1位于：</span><span class="sxs-lookup"><span data-stu-id="eab84-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="eab84-146">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="eab84-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="eab84-147">Aspnet\_regiis 为映射 Web 应用程序的脚本提供两个选项：</span><span class="sxs-lookup"><span data-stu-id="eab84-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="eab84-148">**-s**设置路径及其子目录中的脚本映射。</span><span class="sxs-lookup"><span data-stu-id="eab84-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="eab84-149">**-sn**仅在路径中设置脚本映射。</span><span class="sxs-lookup"><span data-stu-id="eab84-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="eab84-150">路径定义 Web 应用程序 IIS 元数据路径，该路径是以 W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} 的形式定义的。</span><span class="sxs-lookup"><span data-stu-id="eab84-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="eab84-151">例如，对于 "默认网站" 下名为 "门户" 的 Web 应用程序，元数据库路径为 W3SVC/1/ROOT/门户。</span><span class="sxs-lookup"><span data-stu-id="eab84-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="eab84-152">请注意，还可以使用称为 "元数据库编辑器" 的工具来获取元数据库路径。</span><span class="sxs-lookup"><span data-stu-id="eab84-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="eab84-153">你可以从[https://support.microsoft.com/default.aspx?scid=kb; 232068;](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)的 Microsoft 支持部门网站下载此工具。</span><span class="sxs-lookup"><span data-stu-id="eab84-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="eab84-154">运行 Aspnet\_regiis-s W3SVC/1/ROOT/门户来更新门户 IIS script map 及其 subapplication。</span><span class="sxs-lookup"><span data-stu-id="eab84-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="eab84-155">运行 Aspnet\_regiis-sn W3SVC/1/ROOT/门户来更新门户 IIS 脚本映射，而不影响门户子目录中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="eab84-156">查找 Web 应用程序正在使用的 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="eab84-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="eab84-157">管理员可以使用 Internet Service Manager 来查找 .NET Framework 运行网站的版本。</span><span class="sxs-lookup"><span data-stu-id="eab84-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="eab84-158">不同的操作系统版本以不同的方式启动 Internet Service Manager。</span><span class="sxs-lookup"><span data-stu-id="eab84-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="eab84-159">若要启动服务管理器，请执行下列步骤。</span><span class="sxs-lookup"><span data-stu-id="eab84-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="eab84-160">**启动 Internet Service Manager**</span><span class="sxs-lookup"><span data-stu-id="eab84-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="eab84-161">转到“开始”。</span><span class="sxs-lookup"><span data-stu-id="eab84-161">Go to **Start**.</span></span>
2. <span data-ttu-id="eab84-162">单击 "**运行**"。</span><span class="sxs-lookup"><span data-stu-id="eab84-162">Click on **run**.</span></span>
3. <span data-ttu-id="eab84-163">键入**inetmgr**。</span><span class="sxs-lookup"><span data-stu-id="eab84-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="eab84-164">从 Internet Service Manager 中，选择想要了解其版本 .NET Framework 的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eab84-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="eab84-165">右键单击 Web 应用程序，然后单击 "属性" **。**</span><span class="sxs-lookup"><span data-stu-id="eab84-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="eab84-166">在 "属性" 窗口中，选择 "**配置"。**</span><span class="sxs-lookup"><span data-stu-id="eab84-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="eab84-167">从 "应用程序映射" 表中，选择 **.aspx**，然后单击 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="eab84-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="eab84-168">从 "**可执行文件**" 文本框中，通过滚动查看版本目录。</span><span class="sxs-lookup"><span data-stu-id="eab84-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="eab84-169">如果版本目录为1.1.4322，则将应用程序映射到 .NET Framework 1.1。</span><span class="sxs-lookup"><span data-stu-id="eab84-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="eab84-170">相反，如果版本目录是 v v1.0.3705，则会将应用程序映射到 .NET Framework 1.0。</span><span class="sxs-lookup"><span data-stu-id="eab84-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
