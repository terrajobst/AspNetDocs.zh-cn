---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: 从 MSBuild 项目文件中运行 Windows PowerShell 脚本 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在生成和部署过程中运行 Windows PowerShell 脚本。 你可以在本地运行脚本 (换而言之，在 b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441446"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a><span data-ttu-id="a21f1-104">从 MSBuild 项目文件中运行 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="a21f1-104">Running Windows PowerShell Scripts from MSBuild Project Files</span></span>

<span data-ttu-id="a21f1-105">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a21f1-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a21f1-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a21f1-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a21f1-107">本主题介绍如何在生成和部署过程中运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-107">This topic describes how to run a Windows PowerShell script as part of a build and deployment process.</span></span> <span data-ttu-id="a21f1-108">你可以在本地（即在生成服务器上）或远程运行脚本，例如在目标 web 服务器或数据库服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="a21f1-108">You can run a script locally (in other words, on the build server) or remotely, like on a destination web server or database server.</span></span>
> 
> <span data-ttu-id="a21f1-109">你可能想要运行部署后的 Windows PowerShell 脚本的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="a21f1-109">There are lots of reasons why you might want to run a post-deployment Windows PowerShell script.</span></span> <span data-ttu-id="a21f1-110">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="a21f1-110">For example, you might want to:</span></span>
> 
> - <span data-ttu-id="a21f1-111">将自定义事件源添加到注册表。</span><span class="sxs-lookup"><span data-stu-id="a21f1-111">Add a custom event source to the registry.</span></span>
> - <span data-ttu-id="a21f1-112">生成用于上传的文件系统目录。</span><span class="sxs-lookup"><span data-stu-id="a21f1-112">Generate a file system directory for uploads.</span></span>
> - <span data-ttu-id="a21f1-113">清理生成目录。</span><span class="sxs-lookup"><span data-stu-id="a21f1-113">Clean up build directories.</span></span>
> - <span data-ttu-id="a21f1-114">将条目写入自定义日志文件。</span><span class="sxs-lookup"><span data-stu-id="a21f1-114">Write entries to a custom log file.</span></span>
> - <span data-ttu-id="a21f1-115">发送电子邮件邀请用户发送到新预配的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a21f1-115">Send emails inviting users to a newly provisioned web application.</span></span>
> - <span data-ttu-id="a21f1-116">创建具有适当权限的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="a21f1-116">Create user accounts with the appropriate permissions.</span></span>
> - <span data-ttu-id="a21f1-117">在 SQL Server 实例之间配置复制。</span><span class="sxs-lookup"><span data-stu-id="a21f1-117">Configure replication between SQL Server instances.</span></span>
> 
> <span data-ttu-id="a21f1-118">本主题将说明如何从 Microsoft 生成引擎（MSBuild）项目文件中的自定义目标以本地方式或远程方式运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-118">This topic will show you how to run Windows PowerShell scripts both locally and remotely from a custom target in a Microsoft Build Engine (MSBuild) project file.</span></span>

<span data-ttu-id="a21f1-119">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="a21f1-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="a21f1-120">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="a21f1-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="a21f1-121">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="a21f1-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="a21f1-122">任务概述</span><span class="sxs-lookup"><span data-stu-id="a21f1-122">Task Overview</span></span>

<span data-ttu-id="a21f1-123">若要在自动或单步部署过程中运行 Windows PowerShell 脚本，需要完成以下高级任务：</span><span class="sxs-lookup"><span data-stu-id="a21f1-123">To run a Windows PowerShell script as part of an automated or single-step deployment process, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="a21f1-124">将 Windows PowerShell 脚本添加到解决方案和源代码管理。</span><span class="sxs-lookup"><span data-stu-id="a21f1-124">Add the Windows PowerShell script to your solution and to source control.</span></span>
- <span data-ttu-id="a21f1-125">创建调用 Windows PowerShell 脚本的命令。</span><span class="sxs-lookup"><span data-stu-id="a21f1-125">Create a command that invokes your Windows PowerShell script.</span></span>
- <span data-ttu-id="a21f1-126">在命令中转义任何保留的 XML 字符。</span><span class="sxs-lookup"><span data-stu-id="a21f1-126">Escape any reserved XML characters in your command.</span></span>
- <span data-ttu-id="a21f1-127">在自定义 MSBuild 项目文件中创建一个目标，并使用**Exec**任务来运行命令。</span><span class="sxs-lookup"><span data-stu-id="a21f1-127">Create a target in your custom MSBuild project file and use the **Exec** task to run your command.</span></span>

<span data-ttu-id="a21f1-128">本主题将演示如何执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="a21f1-128">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="a21f1-129">本主题中的任务和演练假设你已熟悉 MSBuild 目标和属性，并且你了解如何使用自定义 MSBuild 项目文件来驱动生成和部署过程。</span><span class="sxs-lookup"><span data-stu-id="a21f1-129">The tasks and walkthroughs in this topic assume that you're already familiar with MSBuild targets and properties, and that you understand how to use a custom MSBuild project file to drive a build and deployment process.</span></span> <span data-ttu-id="a21f1-130">有关详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="a21f1-130">For more information, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

## <a name="creating-and-adding-windows-powershell-scripts"></a><span data-ttu-id="a21f1-131">创建和添加 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="a21f1-131">Creating and Adding Windows PowerShell Scripts</span></span>

<span data-ttu-id="a21f1-132">本主题中的任务使用名为**LogDeploy**的 Windows PowerShell 脚本示例，演示如何从 MSBuild 运行脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-132">The tasks in this topic use a sample Windows PowerShell script named **LogDeploy.ps1** to illustrate how to run scripts from MSBuild.</span></span> <span data-ttu-id="a21f1-133">**LogDeploy**脚本包含一个用于将单行条目写入日志文件的简单函数：</span><span class="sxs-lookup"><span data-stu-id="a21f1-133">The **LogDeploy.ps1** script contains a simple function that writes a single-line entry to a log file:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

<span data-ttu-id="a21f1-134">**LogDeploy**脚本接受两个参数。</span><span class="sxs-lookup"><span data-stu-id="a21f1-134">The **LogDeploy.ps1** script accepts two parameters.</span></span> <span data-ttu-id="a21f1-135">第一个参数表示要向其中添加条目的日志文件的完整路径，第二个参数表示要在日志文件中记录的部署目标。</span><span class="sxs-lookup"><span data-stu-id="a21f1-135">The first parameter represents the full path to the log file to which you want to add an entry, and the second parameter represents the deployment destination that you want to record in the log file.</span></span> <span data-ttu-id="a21f1-136">运行该脚本时，它会将行添加到日志文件中，格式如下：</span><span class="sxs-lookup"><span data-stu-id="a21f1-136">When you run the script, it adds a line to the log file in this format:</span></span>

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

<span data-ttu-id="a21f1-137">若要使**LogDeploy**脚本可用于 MSBuild，需执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a21f1-137">To make the **LogDeploy.ps1** script available to MSBuild, you need to:</span></span>

- <span data-ttu-id="a21f1-138">将脚本添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="a21f1-138">Add the script to source control.</span></span>
- <span data-ttu-id="a21f1-139">在 Visual Studio 2010 中将脚本添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="a21f1-139">Add the script to your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="a21f1-140">无论你是计划在生成服务器上运行脚本还是在远程计算机上运行脚本，都不需要使用解决方案内容部署脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-140">You don't need to deploy the script with your solution content, regardless of whether you plan to run the script on the build server or on a remote computer.</span></span> <span data-ttu-id="a21f1-141">一种选择是将脚本添加到解决方案文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a21f1-141">One option is to add the script to a solution folder.</span></span> <span data-ttu-id="a21f1-142">在联系人管理器示例中，由于要在部署过程中使用 Windows PowerShell 脚本，因此将脚本添加到发布解决方案文件夹是有意义的。</span><span class="sxs-lookup"><span data-stu-id="a21f1-142">In the Contact Manager example, because you want to use the Windows PowerShell script as part of the deployment process, it makes sense to add the script to the Publish solution folder.</span></span>

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

<span data-ttu-id="a21f1-143">解决方案文件夹的内容将以源材料的形式复制到生成服务器。</span><span class="sxs-lookup"><span data-stu-id="a21f1-143">The contents of solution folders are copied to build servers as source material.</span></span> <span data-ttu-id="a21f1-144">但是，它们不构成任何项目输出的任何部分。</span><span class="sxs-lookup"><span data-stu-id="a21f1-144">However, they form no part of any project output.</span></span>

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a><span data-ttu-id="a21f1-145">在生成服务器上执行 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="a21f1-145">Executing a Windows PowerShell Script on the Build Server</span></span>

<span data-ttu-id="a21f1-146">在某些情况下，可能需要在生成项目的计算机上运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-146">In some scenarios, you may want to run Windows PowerShell scripts on the computer that builds your projects.</span></span> <span data-ttu-id="a21f1-147">例如，你可以使用 Windows PowerShell 脚本来清理生成文件夹，或将条目写入自定义日志文件。</span><span class="sxs-lookup"><span data-stu-id="a21f1-147">For example, you might use a Windows PowerShell script to clean up build folders or write entries to a custom log file.</span></span>

<span data-ttu-id="a21f1-148">就语法而言，从 MSBuild 项目文件中运行 Windows PowerShell 脚本与从常规命令提示符下运行 Windows PowerShell 脚本相同。</span><span class="sxs-lookup"><span data-stu-id="a21f1-148">In terms of syntax, running a Windows PowerShell script from an MSBuild project file is the same as running a Windows PowerShell script from a regular command prompt.</span></span> <span data-ttu-id="a21f1-149">需要调用 ngen.exe 可执行文件，并使用 **–命令**开关提供 Windows powershell 要运行的命令。</span><span class="sxs-lookup"><span data-stu-id="a21f1-149">You need to invoke the powershell.exe executable and use the **–command** switch to provide the commands you want Windows PowerShell to run.</span></span> <span data-ttu-id="a21f1-150">（在 Windows PowerShell v2 中，你还可以使用 **-file**开关）。</span><span class="sxs-lookup"><span data-stu-id="a21f1-150">(In Windows PowerShell v2, you can also use the **–file** switch).</span></span> <span data-ttu-id="a21f1-151">此命令应采用以下格式：</span><span class="sxs-lookup"><span data-stu-id="a21f1-151">The command should take this format:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

<span data-ttu-id="a21f1-152">例如:</span><span class="sxs-lookup"><span data-stu-id="a21f1-152">For example:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

<span data-ttu-id="a21f1-153">如果脚本的路径包含空格，则需要将文件路径用单引号引起来，并在前面加上 "&" 符。</span><span class="sxs-lookup"><span data-stu-id="a21f1-153">If the path to your script includes spaces, you need to enclose the file path in single quotes preceded by an ampersand.</span></span> <span data-ttu-id="a21f1-154">不能使用双引号，因为已使用双引号将命令括起来：</span><span class="sxs-lookup"><span data-stu-id="a21f1-154">You can't use double quotes, because you've already used them to enclose the command:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

<span data-ttu-id="a21f1-155">从 MSBuild 调用此命令时还有一些其他注意事项。</span><span class="sxs-lookup"><span data-stu-id="a21f1-155">There are a few additional considerations when you invoke this command from MSBuild.</span></span> <span data-ttu-id="a21f1-156">首先，应包括 **–非交互式**标志，以确保脚本安静地执行。</span><span class="sxs-lookup"><span data-stu-id="a21f1-156">First, you should include the **–NonInteractive** flag to ensure that the script executes quietly.</span></span> <span data-ttu-id="a21f1-157">接下来，应包含具有相应参数值的 **– set-executionpolicy**标志。</span><span class="sxs-lookup"><span data-stu-id="a21f1-157">Next, you should include the **–ExecutionPolicy** flag with an appropriate argument value.</span></span> <span data-ttu-id="a21f1-158">此参数指定 Windows PowerShell 将应用于脚本的执行策略，并允许你替代默认执行策略，这可能会阻止脚本的执行。</span><span class="sxs-lookup"><span data-stu-id="a21f1-158">This specifies the execution policy that Windows PowerShell will apply to your script and allows you to override the default execution policy, which may prevent execution of your script.</span></span> <span data-ttu-id="a21f1-159">可以从以下参数值中进行选择：</span><span class="sxs-lookup"><span data-stu-id="a21f1-159">You can choose from these argument values:</span></span>

- <span data-ttu-id="a21f1-160">如果值为 "**无限制**"，则将允许 Windows PowerShell 执行脚本，而不管脚本是否已签名。</span><span class="sxs-lookup"><span data-stu-id="a21f1-160">A value of **Unrestricted** will allow Windows PowerShell to execute your script, regardless of whether the script is signed.</span></span>
- <span data-ttu-id="a21f1-161">如果值为**RemoteSigned** ，则 Windows PowerShell 将允许 Windows PowerShell 执行在本地计算机上创建的未签名脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-161">A value of **RemoteSigned** will allow Windows PowerShell to execute unsigned scripts that were created on the local machine.</span></span> <span data-ttu-id="a21f1-162">但是，必须对在其他位置创建的脚本进行签名。</span><span class="sxs-lookup"><span data-stu-id="a21f1-162">However, scripts that were created elsewhere must be signed.</span></span> <span data-ttu-id="a21f1-163">（实际上，不太可能在生成服务器上本地创建 Windows PowerShell 脚本）。</span><span class="sxs-lookup"><span data-stu-id="a21f1-163">(In practice, you're very unlikely to have created a Windows PowerShell script locally on a build server).</span></span>
- <span data-ttu-id="a21f1-164">值**AllSigned**将允许 Windows PowerShell 仅执行签名的脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-164">A value of **AllSigned** will allow Windows PowerShell to execute signed scripts only.</span></span>

<span data-ttu-id="a21f1-165">默认的执行策略受到**限制**，这会阻止 Windows PowerShell 运行任何脚本文件。</span><span class="sxs-lookup"><span data-stu-id="a21f1-165">The default execution policy is **Restricted**, which prevents Windows PowerShell from running any script files.</span></span>

<span data-ttu-id="a21f1-166">最后，需要对 Windows PowerShell 命令中出现的任何保留的 XML 字符进行转义：</span><span class="sxs-lookup"><span data-stu-id="a21f1-166">Finally, you need to escape any reserved XML characters that occur in your Windows PowerShell command:</span></span>

- <span data-ttu-id="a21f1-167">将单引号替换 **&amp;**</span><span class="sxs-lookup"><span data-stu-id="a21f1-167">Replace single quotes with **&amp;apos;**</span></span>
- <span data-ttu-id="a21f1-168">用 **&amp;** 替换双引号</span><span class="sxs-lookup"><span data-stu-id="a21f1-168">Replace double quotes with **&amp;quot;**</span></span>
- <span data-ttu-id="a21f1-169">将 & 替换 **&amp;amp;**</span><span class="sxs-lookup"><span data-stu-id="a21f1-169">Replace ampersands with **&amp;amp;**</span></span>

- <span data-ttu-id="a21f1-170">进行这些更改时，命令将如下所示：</span><span class="sxs-lookup"><span data-stu-id="a21f1-170">When you make these changes, your command will resemble this:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

<span data-ttu-id="a21f1-171">在自定义 MSBuild 项目文件中，可以创建一个新的目标，并使用**Exec**任务运行此命令：</span><span class="sxs-lookup"><span data-stu-id="a21f1-171">Within your custom MSBuild project file, you can create a new target and use the **Exec** task to run this command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

<span data-ttu-id="a21f1-172">在此示例中，请注意：</span><span class="sxs-lookup"><span data-stu-id="a21f1-172">In this example, note that:</span></span>

- <span data-ttu-id="a21f1-173">任何变量（如参数值和 Windows PowerShell 可执行文件的位置）都声明为 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="a21f1-173">Any variables, like parameter values and the location of the Windows PowerShell executable, are declared as MSBuild properties.</span></span>
- <span data-ttu-id="a21f1-174">包括条件，使用户能够从命令行重写这些值。</span><span class="sxs-lookup"><span data-stu-id="a21f1-174">Conditions are included to enable users to override these values from the command line.</span></span>
- <span data-ttu-id="a21f1-175">**MSDeployComputerName**属性在项目文件中的其他位置声明。</span><span class="sxs-lookup"><span data-stu-id="a21f1-175">The **MSDeployComputerName** property is declared elsewhere in the project file.</span></span>

<span data-ttu-id="a21f1-176">当你作为生成过程的一部分执行此目标时，Windows PowerShell 将运行你的命令并将日志条目写入指定的文件。</span><span class="sxs-lookup"><span data-stu-id="a21f1-176">When you execute this target as part of your build process, Windows PowerShell will run your command and write a log entry to the file you specified.</span></span>

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a><span data-ttu-id="a21f1-177">在远程计算机上执行 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="a21f1-177">Executing a Windows PowerShell Script on a Remote Computer</span></span>

<span data-ttu-id="a21f1-178">Windows PowerShell 可以通过[Windows 远程管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)（WinRM）在远程计算机上运行脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-178">Windows PowerShell is capable of running scripts on remote computers through [Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span></span> <span data-ttu-id="a21f1-179">为此，需要使用[命令调用](https://technet.microsoft.com/library/dd347578.aspx)cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a21f1-179">To do this, you need to use the [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span></span> <span data-ttu-id="a21f1-180">这使你可以针对一台或多台远程计算机执行脚本，而无需将该脚本复制到远程计算机。</span><span class="sxs-lookup"><span data-stu-id="a21f1-180">This lets you execute your script against one or more remote computers without copying the script to the remote computers.</span></span> <span data-ttu-id="a21f1-181">所有结果都将返回到运行脚本的本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="a21f1-181">Any results are returned to the local computer from which you ran the script.</span></span>

> [!NOTE]
> <span data-ttu-id="a21f1-182">在使用**Invoke** cmdlet 在远程计算机上执行 Windows PowerShell 脚本之前，你需要配置 WinRM 侦听器以接受远程消息。</span><span class="sxs-lookup"><span data-stu-id="a21f1-182">Before you use the **Invoke-Command** cmdlet to execute Windows PowerShell scripts on a remote computer, you need to configure a WinRM listener to accept remote messages.</span></span> <span data-ttu-id="a21f1-183">可以通过在远程计算机上运行命令**winrm quickconfig**来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a21f1-183">You can do this by running the command **winrm quickconfig** on the remote computer.</span></span> <span data-ttu-id="a21f1-184">有关详细信息，请参阅[Windows 远程管理的安装和配置](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a21f1-184">For more information, see [Installation and Configuration for Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).</span></span>

<span data-ttu-id="a21f1-185">在 Windows PowerShell 窗口中，可以使用此语法在远程计算机上运行**LogDeploy**脚本：</span><span class="sxs-lookup"><span data-stu-id="a21f1-185">From a Windows PowerShell window, you'd use this syntax to run the **LogDeploy.ps1** script on a remote computer:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> <span data-ttu-id="a21f1-186">使用**Invoke 命令**运行脚本文件的方法有多种，但当需要提供参数值并使用空格管理路径时，这种方法最简单。</span><span class="sxs-lookup"><span data-stu-id="a21f1-186">There are various other ways of using **Invoke-Command** to run a script file, but this approach is the most straightforward when you need to provide parameter values and manage paths with spaces.</span></span>

<span data-ttu-id="a21f1-187">在命令提示符下运行此命令时，需要调用 Windows PowerShell 可执行文件，并使用 **– command**参数来提供说明：</span><span class="sxs-lookup"><span data-stu-id="a21f1-187">When you run this from a command prompt, you need to invoke the Windows PowerShell executable and use the **–command** parameter to provide your instructions:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

<span data-ttu-id="a21f1-188">与前面一样，在从 MSBuild 运行命令时，需要提供一些附加的开关并转义任何保留的 XML 字符：</span><span class="sxs-lookup"><span data-stu-id="a21f1-188">As before, you need to provide some additional switches and escape any reserved XML characters when you run the command from MSBuild:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

<span data-ttu-id="a21f1-189">最后，与之前一样，你可以使用自定义 MSBuild 目标内的**Exec**任务来执行命令：</span><span class="sxs-lookup"><span data-stu-id="a21f1-189">Finally, as before, you can use the **Exec** task within a custom MSBuild target to execute your command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

<span data-ttu-id="a21f1-190">作为生成过程的一部分执行此目标时，Windows PowerShell 将在 **– computername**参数中指定的计算机上运行脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-190">When you execute this target as part of your build process, Windows PowerShell will run your script on the computer you specified in the **–computername** argument.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a21f1-191">结束语</span><span class="sxs-lookup"><span data-stu-id="a21f1-191">Conclusion</span></span>

<span data-ttu-id="a21f1-192">本主题介绍了如何从 MSBuild 项目文件中运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="a21f1-192">This topic described how to run a Windows PowerShell script from an MSBuild project file.</span></span> <span data-ttu-id="a21f1-193">您可以使用此方法在本地或远程计算机上运行 Windows PowerShell 脚本，作为自动或单步构建和部署过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="a21f1-193">You can use this approach to run a Windows PowerShell script, either locally or on a remote computer, as part of an automated or single-step build and deployment process.</span></span>

## <a name="further-reading"></a><span data-ttu-id="a21f1-194">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="a21f1-194">Further Reading</span></span>

<span data-ttu-id="a21f1-195">有关对 Windows PowerShell 脚本进行签名和管理执行策略的指南，请参阅[运行 Windows Powershell 脚本](https://technet.microsoft.com/library/ee176949.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a21f1-195">For guidance on signing Windows PowerShell scripts and managing execution policies, see [Running Windows PowerShell Scripts](https://technet.microsoft.com/library/ee176949.aspx).</span></span> <span data-ttu-id="a21f1-196">有关从远程计算机运行 Windows PowerShell 命令的指南，请参阅[运行远程命令](https://technet.microsoft.com/library/dd819505.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a21f1-196">For guidance on running Windows PowerShell commands from a remote computer, see [Running Remote Commands](https://technet.microsoft.com/library/dd819505.aspx).</span></span>

<span data-ttu-id="a21f1-197">有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="a21f1-197">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a21f1-198">[上一页](taking-web-applications-offline-with-web-deploy.md)
> [下一页](troubleshooting-the-packaging-process.md)</span><span class="sxs-lookup"><span data-stu-id="a21f1-198">[Previous](taking-web-applications-offline-with-web-deploy.md)
[Next](troubleshooting-the-packaging-process.md)</span></span>
