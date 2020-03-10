---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 手动安装 Web 包 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在 Internet Information Services （IIS）中手动导入 web 部署包。 本主题介绍如何生成和打包 Web Applicati 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514886"
---
# <a name="manually-installing-web-packages"></a><span data-ttu-id="ae7f4-104">手动安装 Web 程序包</span><span class="sxs-lookup"><span data-stu-id="ae7f4-104">Manually Installing Web Packages</span></span>

<span data-ttu-id="ae7f4-105">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ae7f4-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ae7f4-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="ae7f4-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ae7f4-107">本主题介绍如何在 Internet Information Services （IIS）中手动导入 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-107">This topic describes how to manually import a web deployment package into Internet Information Services (IIS).</span></span>
> 
> <span data-ttu-id="ae7f4-108">"[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)" 一文介绍了如何将 IIS Web 部署工具（Web 部署）与 Microsoft 生成引擎（MSBuild）和 Web 发布管道（WPP）结合使用，以便将 Web 应用程序项目打包到一个 zip 文件中。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-108">The topic [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) described how the IIS Web Deployment Tool (Web Deploy), in conjunction with the Microsoft Build Engine (MSBuild) and the Web Publishing Pipeline (WPP), lets you package your web application projects into a single zip file.</span></span> <span data-ttu-id="ae7f4-109">此文件（通常称为 "web 部署包"，或简称为 "部署包"）包含 IIS 在 web 服务器上重新创建 web 应用程序所需的所有内容和配置信息。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-109">This file, commonly known as a web deployment package (or simply a deployment package), contains all the content and configuration information that IIS needs in order to re-create your web application on a web server.</span></span>
> 
> <span data-ttu-id="ae7f4-110">创建 web 部署包后，可以通过多种方式将其发布到 IIS 服务器。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-110">Once you've created a web deployment package, you can publish it to an IIS server in various ways.</span></span> <span data-ttu-id="ae7f4-111">在许多情况下，你将需要利用 MSBuild、WPP 和 Web 部署之间的集成点，以便在自动或单步构建和部署过程中以远程方式创建和安装 Web 包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-111">In a lot of scenarios, you'll want to take advantage of the integration points between MSBuild, the WPP, and Web Deploy to create and install web packages remotely as part of an automated or single-step build and deployment process.</span></span> <span data-ttu-id="ae7f4-112">[部署 Web 包](deploying-web-packages.md)中介绍了此过程。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-112">This process is described in [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="ae7f4-113">但这并不总是可行。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-113">However, this isn't always possible.</span></span> <span data-ttu-id="ae7f4-114">假设要将 web 应用程序部署到面向 Internet 的生产环境中。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-114">Suppose you want to deploy a web application to an Internet-facing production environment.</span></span> <span data-ttu-id="ae7f4-115">出于安全原因，在外围网络（也称为 DMZ、外围安全区域和外围子网）中，此类生产环境在不同于生成服务器的子网中的防火墙的最小可能性。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-115">For security reasons, such a production environment is at the very least likely to be behind a firewall on a subnet that is separate from the build server, in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet).</span></span> <span data-ttu-id="ae7f4-116">在许多情况下，生产环境将位于单独的域或物理上隔离的网络上。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-116">In lots of cases, the production environment will be on a separate domain or on a physically isolated network.</span></span>
> 
> <span data-ttu-id="ae7f4-117">在这些情况下，唯一的选择可能是将 web 包移植到目标服务器上，并手动将其导入到 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-117">In these scenarios, your only option may be to port the web package onto the destination server and manually import it into IIS.</span></span> <span data-ttu-id="ae7f4-118">尽管此方法阻止自动部署，但它仍然是一种用于发布 web 应用程序&#x2014;的非常有效的方法，只需将单个 zip 文件复制到 web 服务器，然后使用向导引导你完成导入过程。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-118">Although this approach precludes automated deployment, it's still a highly effective technique for publishing a web application&#x2014;you simply copy a single zip file to your web server and use a wizard to guide you through the import process.</span></span>

<span data-ttu-id="ae7f4-119">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="ae7f4-120">任务概述</span><span class="sxs-lookup"><span data-stu-id="ae7f4-120">Task Overview</span></span>

<span data-ttu-id="ae7f4-121">需要完成这些高级任务，才能将 web 部署包导入到 IIS：</span><span class="sxs-lookup"><span data-stu-id="ae7f4-121">You'll need to complete these high-level tasks to import a web deployment package into IIS:</span></span>

- <span data-ttu-id="ae7f4-122">使用 MSBuild 命令行、Team Build 或 Visual Studio 2010 创建 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-122">Create a web deployment package using the MSBuild command line, Team Build, or Visual Studio 2010.</span></span>
- <span data-ttu-id="ae7f4-123">将 web 包复制到目标 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-123">Copy the web package to the destination web server.</span></span>
- <span data-ttu-id="ae7f4-124">使用 IIS 管理器中的 "导入应用程序包" 向导安装 web 包，并为变量（如连接字符串和服务终结点）提供值。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-124">Use the Import Application Package Wizard in IIS Manager to install the web package and provide values for variables like connection strings and service endpoints.</span></span>

<span data-ttu-id="ae7f4-125">本主题将演示如何执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-125">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="ae7f4-126">本主题中的任务和演练假定您已熟悉 web 包、Web 部署和 WPP 后面的概念。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-126">The tasks and walkthroughs in this topic assume that you're already familiar with the concepts behind web packages, Web Deploy, and the WPP.</span></span> <span data-ttu-id="ae7f4-127">有关详细信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-127">For more information, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ae7f4-128">本主题最适用于为[Web 部署发布（脱机部署）配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)，这说明了如何安装所需的组件和准备 IIS 网站以便导入包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-128">This topic is best used in conjunction with [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), which explains how to install the required components and prepare an IIS website for package import.</span></span>

## <a name="create-a-web-deployment-package"></a><span data-ttu-id="ae7f4-129">创建 Web 部署包</span><span class="sxs-lookup"><span data-stu-id="ae7f4-129">Create a Web Deployment Package</span></span>

<span data-ttu-id="ae7f4-130">第一个任务是为要部署的 web 应用程序项目创建 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-130">The first task is to create a web deployment package for the web application project you want to deploy.</span></span> <span data-ttu-id="ae7f4-131">可以通过多种方式创建 web 包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-131">You can create web packages in a variety of ways.</span></span>

<span data-ttu-id="ae7f4-132">**方法1：使用 Visual Studio 在生成过程中创建包**</span><span class="sxs-lookup"><span data-stu-id="ae7f4-132">**Approach 1: Create a package as part of the build process with Visual Studio**</span></span>

<span data-ttu-id="ae7f4-133">你可以配置 web 应用程序项目，以便在每次生成后通过项目属性页上的 "**打包/发布 web** " 选项卡创建一个 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-133">You can configure your web application project to create a web deployment package after every build through the **Package/Publish Web** tab on the project property pages.</span></span> <span data-ttu-id="ae7f4-134">此过程在[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)中进行了介绍。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-134">This process is described in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="ae7f4-135">**方法2：使用 MSBuild 在生成过程中创建包**</span><span class="sxs-lookup"><span data-stu-id="ae7f4-135">**Approach 2: Create a package as part of the build process with MSBuild**</span></span>

<span data-ttu-id="ae7f4-136">如果通过使用 MSBuild 直接生成 web 应用程序项目（通过自定义 MSBuild 项目文件或从命令行生成），可以通过在命令中包括**DeployOnBuild = true**和**DeployTarget = package**属性，在生成过程中创建 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-136">If you build your web application project by using MSBuild directly, either through a custom MSBuild project file or from the command line, you can create a web deployment package as part of the build process by including the **DeployOnBuild=true** and **DeployTarget=Package** properties in your command.</span></span> <span data-ttu-id="ae7f4-137">[了解生成过程](understanding-the-build-process.md)中介绍了此过程。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-137">This process is described in [Understanding the Build Process](understanding-the-build-process.md).</span></span>

<span data-ttu-id="ae7f4-138">**方法3：在 Visual Studio 中按需创建包**</span><span class="sxs-lookup"><span data-stu-id="ae7f4-138">**Approach 3: Create a package on demand in Visual Studio**</span></span>

<span data-ttu-id="ae7f4-139">可在 Visual Studio 2010 中随时为 web 应用程序项目创建 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-139">You can create a web deployment package for a web application project at any time in Visual Studio 2010.</span></span> <span data-ttu-id="ae7f4-140">为此，请在 "**解决方案资源管理器**" 窗口中，右键单击 web 应用程序项目，然后单击 "**生成部署包**"。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-140">To do this, in the **Solution Explorer** window, right-click your web application project, and then click **Build Deployment Package**.</span></span>

![](manually-installing-web-packages/_static/image1.png)

<span data-ttu-id="ae7f4-141">**方法4：按需从命令行创建包**</span><span class="sxs-lookup"><span data-stu-id="ae7f4-141">**Approach 4: Create a package on demand from the command line**</span></span>

<span data-ttu-id="ae7f4-142">可以通过在 web 应用程序项目中使用 MSBuild 调用**包**目标，从命令行创建 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-142">You can create a web deployment package from the command line by invoking the **Package** target on your web application project using MSBuild.</span></span> <span data-ttu-id="ae7f4-143">命令应如下所示：</span><span class="sxs-lookup"><span data-stu-id="ae7f4-143">The command should resemble this:</span></span>

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

<span data-ttu-id="ae7f4-144">无论使用哪种方法，最终结果是相同的。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-144">Whichever approach you use, the end result is the same.</span></span> <span data-ttu-id="ae7f4-145">此 WPP 在你的 web 应用程序项目的输出文件夹中创建一个 web 部署包作为 zip 文件以及各种支持资源。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-145">The WPP creates a web deployment package as a zip file, together with various supporting resources, in the output folder for your web application project.</span></span>

![](manually-installing-web-packages/_static/image2.png)

<span data-ttu-id="ae7f4-146">当你计划手动导入 web 包时，只需 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-146">When you're planning to import the web package manually, you require only the zip file.</span></span> <span data-ttu-id="ae7f4-147">将此文件复制到目标 web 服务器，然后可以开始导入过程。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-147">Copy this file to your target web server and you can begin the import process.</span></span>

## <a name="import-a-web-package-into-iis"></a><span data-ttu-id="ae7f4-148">将 Web 包导入 IIS</span><span class="sxs-lookup"><span data-stu-id="ae7f4-148">Import a Web Package into IIS</span></span>

<span data-ttu-id="ae7f4-149">您可以使用下一个过程将本地文件系统中的 web 部署包导入到 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-149">You can use the next procedure to import a web deployment package from the local file system into an IIS website.</span></span> <span data-ttu-id="ae7f4-150">在执行此过程之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="ae7f4-150">Before you perform this procedure, ensure that you have:</span></span>

- <span data-ttu-id="ae7f4-151">已将 web 部署包复制到 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-151">Copied the web deployment package to the web server.</span></span>
- <span data-ttu-id="ae7f4-152">配置了用于托管应用程序的 IIS web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-152">Configured an IIS web server to host your application.</span></span>

<span data-ttu-id="ae7f4-153">有关将 IIS web 服务器配置为支持 web 部署包的详细信息，请参阅[配置 Web 服务器以进行 Web 部署发布（脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-153">For more information on configuring an IIS web server to support web deployment packages, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span>

<span data-ttu-id="ae7f4-154">**使用 IIS 管理器导入 web 部署包**</span><span class="sxs-lookup"><span data-stu-id="ae7f4-154">**To import a web deployment package using IIS Manager**</span></span>

1. <span data-ttu-id="ae7f4-155">在 IIS 管理器的 "**连接**" 窗格中，右键单击您的 IIS 网站，指向 "**部署**"，然后单击 "**导入应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-155">In IIS Manager, in the **Connections** pane, right-click your IIS website, point to **Deploy**, and then click **Import Application**.</span></span>

    ![](manually-installing-web-packages/_static/image3.png)
2. <span data-ttu-id="ae7f4-156">在 "导入应用程序包" 向导的 "**选择包**" 页上，浏览到 web 部署包所在的位置，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-156">In the Import Application Package Wizard, on the **Select the Package** page, browse to the location of your web deployment package, and then click **Next**.</span></span>
3. <span data-ttu-id="ae7f4-157">在 "**选择包的内容**" 页上，清除任何不需要的内容，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-157">On the **Select the Contents of the Package** page, clear any content that you don't require, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="ae7f4-158">在许多情况下，你可能不希望导入 web 部署包附带的所有内容。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-158">In a lot of cases, you may not want to import everything that comes with a web deployment package.</span></span> <span data-ttu-id="ae7f4-159">例如，你可能不希望允许 Web 部署替换关联的数据库。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-159">For example, you may not want to allow Web Deploy to replace the associated database.</span></span>  
    > <span data-ttu-id="ae7f4-160">"**授予权限**" 项设置目标文件系统的权限，以确保应用程序池标识可以访问存储网站内容的物理文件夹。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-160">The **Grant permissions** entries set permissions on the destination file system to ensure that the application pool identity can access the physical folder that stores the website content.</span></span> <span data-ttu-id="ae7f4-161">此外，将向 "匿名身份验证" 用户授予对文件夹的 "读取" 权限，以允许应用程序为多用途 Internet 邮件扩展（MIME）类型文件提供服务。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-161">In addition, the anonymous authentication user is granted read permission to the folder to let the application serve Multipurpose Internet Mail Extensions (MIME) type files.</span></span> <span data-ttu-id="ae7f4-162">如果需要，你可以删除这些条目并手动配置权限。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-162">If you prefer, you can remove these entries and configure permissions manually.</span></span>
4. <span data-ttu-id="ae7f4-163">在 "**输入应用程序包信息**" 页上，提供所需的信息。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-163">On the **Enter Application Package Information** page, provide the requested information.</span></span>

    ![](manually-installing-web-packages/_static/image5.png)
5. <span data-ttu-id="ae7f4-164">当你创建 web 包时，WPP 会分析你的应用程序的配置文件，并检测任何变量（如连接字符串和服务终结点）。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-164">When you create a web package, the WPP analyzes the configuration file for your application and detects any variables, like connection strings and service endpoints.</span></span> <span data-ttu-id="ae7f4-165">这种情况下：</span><span class="sxs-lookup"><span data-stu-id="ae7f4-165">In this case:</span></span>

    1. <span data-ttu-id="ae7f4-166">**应用程序路径**是要在其中安装应用程序的 IIS 路径。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-166">**Application Path** is the IIS path where you want to install your application.</span></span> <span data-ttu-id="ae7f4-167">此设置对于 WPP 创建的所有部署包都是通用的。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-167">This setting is common to all deployment packages that the WPP creates.</span></span>
    2. <span data-ttu-id="ae7f4-168">**ContactService 服务终结点地址**是应用程序用来与部署的 WCF 服务进行通信的地址。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-168">**ContactService Service Endpoint Address** is the address that the application should use to communicate with the deployed WCF service.</span></span> <span data-ttu-id="ae7f4-169">此设置对应于*web.config*文件中的条目。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-169">This setting corresponds to an entry in the *web.config* file.</span></span>
    3. <span data-ttu-id="ae7f4-170">第一个**连接字符串**设置是 Web 部署应该用于部署与应用程序关联的数据库的连接字符串（在本例中为 ASP.NET 成员资格数据库）。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-170">The first **Connection String** setting is the connection string that Web Deploy should use to deploy the database associated with the application (in this case an ASP.NET membership database).</span></span> <span data-ttu-id="ae7f4-171">此设置对应于 Visual Studio 中的 "**包/发布 SQL** " 选项卡上的设置。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-171">This setting corresponds to the setting on the **Package/Publish SQL** tab in Visual Studio.</span></span>
    4. <span data-ttu-id="ae7f4-172">第二个**连接字符串**设置是在启动和运行应用程序时，应用程序将实际用于与数据库通信的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-172">The second **Connection String** setting is the connection string that your application will actually use to communicate with the database when it's up and running.</span></span> <span data-ttu-id="ae7f4-173">这对应于*web.config 文件中的连接*字符串条目。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-173">This corresponds to a connection string entry in the *web.config* file.</span></span>

        > [!NOTE]
        > <span data-ttu-id="ae7f4-174">有关这些参数的来源的详细信息，请参阅[为 Web 包部署配置参数](configuring-parameters-for-web-package-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-174">For more information on where these parameters come from, see [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md).</span></span>
6. <span data-ttu-id="ae7f4-175">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-175">Click **Next**.</span></span>
7. <span data-ttu-id="ae7f4-176">如果这不是您首次将应用程序部署到此网站，系统将提示您指定是否要在安装之前删除所有现有内容。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-176">If this is not the first time you've deployed the application to this website, you'll be prompted to specify whether you want to delete all existing content prior to installation.</span></span> <span data-ttu-id="ae7f4-177">选择适合你的要求的选项，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-177">Choose the option that's appropriate for your requirements, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image6.png)
8. <span data-ttu-id="ae7f4-178">当 IIS 完成包的安装后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-178">When IIS has finished installing the package, click **Finish**.</span></span>

    ![](manually-installing-web-packages/_static/image7.png)

<span data-ttu-id="ae7f4-179">此时，已成功将 web 应用程序发布到 IIS。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-179">At this point, you've successfully published your web application to IIS.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ae7f4-180">结束语</span><span class="sxs-lookup"><span data-stu-id="ae7f4-180">Conclusion</span></span>

<span data-ttu-id="ae7f4-181">本主题介绍了如何使用 IIS 管理器将 web 部署包导入到 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-181">This topic described how to import a web deployment package into an IIS website using IIS Manager.</span></span> <span data-ttu-id="ae7f4-182">当安全或基础结构限制不可能或不希望进行远程部署时，这种 web 应用程序发布方法非常合适。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-182">This approach to web application publishing is appropriate when security or infrastructure constraints make remote deployment impossible or undesirable.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ae7f4-183">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="ae7f4-183">Further Reading</span></span>

<span data-ttu-id="ae7f4-184">有关如何配置 IIS web 服务器以支持手动导入 web 包的指南，请参阅[配置 Web 服务器以进行 Web 部署发布（脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-184">For guidance on how to configure an IIS web server to support manually importing a web package, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="ae7f4-185">有关部署 web 包的更多一般指南，请参阅[演练：使用 Web 部署包部署 Web 应用程序项目（第1部分，共4部分）](https://msdn.microsoft.com/library/dd483479.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae7f4-185">For more general guidance on deploying web packages, see [Walkthrough: Deploying a Web Application Project Using a Web Deployment Package (Part 1 of 4)](https://msdn.microsoft.com/library/dd483479.aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ae7f4-186">上一页</span><span class="sxs-lookup"><span data-stu-id="ae7f4-186">Previous</span></span>](creating-and-running-a-deployment-command-file.md)
