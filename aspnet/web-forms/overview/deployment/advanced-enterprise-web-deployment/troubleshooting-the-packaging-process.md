---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 打包过程疑难解答 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何通过使用 M ... 中的 EnablePackageProcessLoggingAndAssert 属性来收集有关打包过程的详细信息。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509750"
---
# <a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="180c2-103">打包过程故障排除</span><span class="sxs-lookup"><span data-stu-id="180c2-103">Troubleshooting the Packaging Process</span></span>

<span data-ttu-id="180c2-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="180c2-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="180c2-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="180c2-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="180c2-106">本主题介绍如何通过使用 Microsoft 生成引擎（MSBuild）中的**EnablePackageProcessLoggingAndAssert**属性来收集有关打包过程的详细信息。</span><span class="sxs-lookup"><span data-stu-id="180c2-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="180c2-107">将**EnablePackageProcessLoggingAndAssert**属性设置为**true**时，MSBuild 将：</span><span class="sxs-lookup"><span data-stu-id="180c2-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="180c2-108">向生成日志添加有关打包过程的其他信息。</span><span class="sxs-lookup"><span data-stu-id="180c2-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="180c2-109">在某些情况下（例如，如果在打包列表中找到了重复的文件），记录错误。</span><span class="sxs-lookup"><span data-stu-id="180c2-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="180c2-110">在*项目名称*\_Package 文件夹中创建日志目录，并使用该目录记录有关要打包的文件的信息。</span><span class="sxs-lookup"><span data-stu-id="180c2-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="180c2-111">如果打包过程失败，或者 web 部署包不包含所需的文件，则可以使用此信息对过程进行故障排除，查明出现问题的位置。</span><span class="sxs-lookup"><span data-stu-id="180c2-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="180c2-112">仅当使用**调试**配置生成项目时， **EnablePackageProcessLoggingAndAssert**属性才适用。</span><span class="sxs-lookup"><span data-stu-id="180c2-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="180c2-113">在其他配置中将忽略该属性。</span><span class="sxs-lookup"><span data-stu-id="180c2-113">The property is ignored in other configurations.</span></span>

<span data-ttu-id="180c2-114">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="180c2-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="180c2-115">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="180c2-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="180c2-116">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="180c2-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="180c2-117">了解 EnablePackageProcessLoggingAndAssert 属性</span><span class="sxs-lookup"><span data-stu-id="180c2-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="180c2-118">[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)介绍了 Web 发布管道（WPP）如何提供一组可扩展 msbuild 功能的 msbuild 目标，并使其能够与 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web 部署）集成。</span><span class="sxs-lookup"><span data-stu-id="180c2-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="180c2-119">打包 web 应用程序项目时，会调用 WPP 目标。</span><span class="sxs-lookup"><span data-stu-id="180c2-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="180c2-120">许多这些 WPP 目标包括在**EnablePackageProcessLoggingAndAssert**属性设置为**true**时记录附加信息的条件逻辑。</span><span class="sxs-lookup"><span data-stu-id="180c2-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="180c2-121">例如，如果你查看**包**目标，可以看到它会创建一个附加的日志目录，并将文件列表写入文本文件，如果**EnablePackageProcessLoggingAndAssert**等于**true**。</span><span class="sxs-lookup"><span data-stu-id="180c2-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="180c2-122">此 WPP 目标是在 "% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web" 文件夹中的 " *web.config* " 文件中定义的。</span><span class="sxs-lookup"><span data-stu-id="180c2-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="180c2-123">可在 Visual Studio 2010 或任何 XML 编辑器中打开此文件并查看目标。</span><span class="sxs-lookup"><span data-stu-id="180c2-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="180c2-124">请注意不要修改该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="180c2-124">Take care not to modify the contents of the file.</span></span>

## <a name="enabling-the-additional-logging"></a><span data-ttu-id="180c2-125">启用其他日志记录</span><span class="sxs-lookup"><span data-stu-id="180c2-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="180c2-126">可以通过多种方式提供**EnablePackageProcessLoggingAndAssert**属性的值，具体取决于生成项目的方式。</span><span class="sxs-lookup"><span data-stu-id="180c2-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="180c2-127">如果从命令行生成项目，则可以将**EnablePackageProcessLoggingAndAssert**属性的值作为命令行参数提供：</span><span class="sxs-lookup"><span data-stu-id="180c2-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

<span data-ttu-id="180c2-128">如果要使用自定义项目文件来生成项目，可以在**MSBuild**任务的**Properties**特性中包括**EnablePackageProcessLoggingAndAssert**值：</span><span class="sxs-lookup"><span data-stu-id="180c2-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

<span data-ttu-id="180c2-129">如果使用 Team Foundation Server （TFS）生成定义生成项目，可以在 " **MSBuild 参数**" 行中为**EnablePackageProcessLoggingAndAssert**属性提供值：![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="180c2-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="180c2-130">有关创建和配置生成定义的详细信息，请参阅[创建支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="180c2-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>

<span data-ttu-id="180c2-131">或者，如果要在每个生成中包含包，可以修改 web 应用程序项目的项目文件，以将**EnablePackageProcessLoggingAndAssert**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="180c2-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="180c2-132">应将属性添加到 .csproj 或 .vbproj 文件中的第一个**PropertyGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="180c2-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a><span data-ttu-id="180c2-133">查看日志文件</span><span class="sxs-lookup"><span data-stu-id="180c2-133">Reviewing the Log Files</span></span>

<span data-ttu-id="180c2-134">当你生成并打包**EnablePackageProcessLoggingAndAssert**设置为**true**的 web 应用程序项目时，MSBuild 将在*项目名称*\_package 文件夹中创建一个名为 Log 的附加文件夹。</span><span class="sxs-lookup"><span data-stu-id="180c2-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="180c2-135">日志文件夹包含各种文件：</span><span class="sxs-lookup"><span data-stu-id="180c2-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="180c2-136">你看到的文件列表将因你的项目和生成过程中的功能而异。</span><span class="sxs-lookup"><span data-stu-id="180c2-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="180c2-137">但是，这些文件通常用于在过程的各个阶段记录 WPP 正在收集的文件的列表：</span><span class="sxs-lookup"><span data-stu-id="180c2-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="180c2-138">*PreExcludePipelineCollectFilesPhaseFileList*文件列出了 MSBuild 在为排除指定的任何文件被删除之前收集的文件。</span><span class="sxs-lookup"><span data-stu-id="180c2-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="180c2-139">删除为排除指定的任何文件后， *AfterExcludeFilesFilesList*文件将包含已修改的文件列表。</span><span class="sxs-lookup"><span data-stu-id="180c2-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="180c2-140">有关从打包过程中排除文件和文件夹的详细信息，请参阅[从部署中排除文件和文件夹](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="180c2-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="180c2-141">*AfterTransformWebConfig*文件列出了在*执行任何 web.config*转换后为打包收集的文件。</span><span class="sxs-lookup"><span data-stu-id="180c2-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="180c2-142">在此列表中，所有特定于配置的*web.config*转换文件（如*web.config*和 web.config）都将从要打包的文件列表中*排除。*</span><span class="sxs-lookup"><span data-stu-id="180c2-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="180c2-143">单个转换后的*web.config*将包含在其位置。</span><span class="sxs-lookup"><span data-stu-id="180c2-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="180c2-144">*PostAutoParameterizationWebConfigConnectionStrings*文件包含已参数化*web.config 文件中*的连接字符串之后的文件列表。</span><span class="sxs-lookup"><span data-stu-id="180c2-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="180c2-145">在部署包时，可以通过此过程将连接字符串替换为目标环境的正确设置。</span><span class="sxs-lookup"><span data-stu-id="180c2-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="180c2-146">*Prepackage*文件包含要包含在包中的已完成的预生成文件列表。</span><span class="sxs-lookup"><span data-stu-id="180c2-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="180c2-147">其他日志文件的名称通常对应于 WPP 目标。</span><span class="sxs-lookup"><span data-stu-id="180c2-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="180c2-148">你可以通过查看% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的 " *Microsoft* web.config" 文件来查看这些目标。</span><span class="sxs-lookup"><span data-stu-id="180c2-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>

<span data-ttu-id="180c2-149">如果你的 web 包的内容不是你所期望的内容，则查看这些文件可能是在处理过程中的哪个点发生错误的有用方法。</span><span class="sxs-lookup"><span data-stu-id="180c2-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="180c2-150">结束语</span><span class="sxs-lookup"><span data-stu-id="180c2-150">Conclusion</span></span>

<span data-ttu-id="180c2-151">本主题介绍了如何使用 MSBuild 中的**EnablePackageProcessLoggingAndAssert**属性对打包过程进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="180c2-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="180c2-152">它介绍了向生成过程提供属性值的不同方法，并介绍了在将属性设置为**true**时所记录的其他信息。</span><span class="sxs-lookup"><span data-stu-id="180c2-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="180c2-153">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="180c2-153">Further Reading</span></span>

<span data-ttu-id="180c2-154">有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="180c2-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="180c2-155">有关 WPP 以及它如何管理打包过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="180c2-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="180c2-156">有关如何从 web 部署包中排除特定文件和文件夹的指导，请参阅[从部署中排除文件和文件夹](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="180c2-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="180c2-157">上一页</span><span class="sxs-lookup"><span data-stu-id="180c2-157">Previous</span></span>](running-windows-powershell-scripts-from-msbuild-project-files.md)
