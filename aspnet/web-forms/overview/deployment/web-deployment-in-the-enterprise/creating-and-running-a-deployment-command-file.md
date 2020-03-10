---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 创建并运行部署命令文件 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何生成一个命令文件，该命令文件将允许你使用 Microsoft 生成引擎（MSBuild）项目文件作为单步执行 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514976"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="06851-103">创建并运行部署命令文件</span><span class="sxs-lookup"><span data-stu-id="06851-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="06851-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="06851-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="06851-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="06851-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="06851-106">本主题介绍如何生成一个命令文件，该文件将允许使用 Microsoft 生成引擎（MSBuild）项目文件作为单步骤、可重复的过程运行部署。</span><span class="sxs-lookup"><span data-stu-id="06851-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="06851-107">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;[联系人管理器](the-contact-manager-solution.md)解决方案来表示具有真实复杂性级别的 WEB 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="06851-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="06851-108">这些教程核心的部署方法基于[理解生成过程](understanding-the-build-process.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="06851-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="06851-109">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="06851-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="06851-110">流程概述</span><span class="sxs-lookup"><span data-stu-id="06851-110">Process Overview</span></span>

<span data-ttu-id="06851-111">在本主题中，你将了解如何创建并运行一个命令文件，该文件使用这些项目文件来执行目标环境的可重复部署。</span><span class="sxs-lookup"><span data-stu-id="06851-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="06851-112">实质上，命令文件只需包含以下 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="06851-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="06851-113">指示 MSBuild 执行环境无关的*Publish*文件。</span><span class="sxs-lookup"><span data-stu-id="06851-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="06851-114">指示*Publish*文件，其中包含特定于环境的项目设置以及在何处可以找到它。</span><span class="sxs-lookup"><span data-stu-id="06851-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="06851-115">创建 MSBuild 命令</span><span class="sxs-lookup"><span data-stu-id="06851-115">Create an MSBuild Command</span></span>

<span data-ttu-id="06851-116">如[了解生成过程](understanding-the-build-process.md)中所述，环境特定的项目*文件（例如，环境*&#x2014;特定的项目文件&#x2014;）设计为在生成时导入到与环境无关的*Publish*文件中。</span><span class="sxs-lookup"><span data-stu-id="06851-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="06851-117">这两个文件一起提供了一组完整的说明，告诉 MSBuild 如何生成和部署解决方案。</span><span class="sxs-lookup"><span data-stu-id="06851-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="06851-118">*Publish*文件使用**import**元素导入特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="06851-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="06851-119">因此，当你使用 Msbuild.exe 生成并部署 Contact Manager 解决方案时，你需要：</span><span class="sxs-lookup"><span data-stu-id="06851-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="06851-120">在*Publish*文件上运行 msbuild.exe。</span><span class="sxs-lookup"><span data-stu-id="06851-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="06851-121">通过提供名为**TargetEnvPropsFile**的命令行参数来指定环境特定的项目文件的位置。</span><span class="sxs-lookup"><span data-stu-id="06851-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="06851-122">为此，MSBuild 命令应如下所示：</span><span class="sxs-lookup"><span data-stu-id="06851-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="06851-123">从这里开始，这是一个简单的步骤，可以将其迁移到可重复的单步部署。</span><span class="sxs-lookup"><span data-stu-id="06851-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="06851-124">只需将 MSBuild 命令添加到 .cmd 文件即可。</span><span class="sxs-lookup"><span data-stu-id="06851-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="06851-125">在 "联系人管理器" 解决方案中，"发布" 文件夹包含一个名为 "Publish-Dev" 的文件，该文件执行此*命令*。</span><span class="sxs-lookup"><span data-stu-id="06851-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="06851-126">**/Fl**开关指示 msbuild 在调用 msbuild.exe 的工作目录中创建一个名为*msbuild.exe*的日志文件。</span><span class="sxs-lookup"><span data-stu-id="06851-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="06851-127">若要部署或重新部署 Contact Manager 解决方案，只需运行*Publish-Dev*文件。</span><span class="sxs-lookup"><span data-stu-id="06851-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="06851-128">运行该文件时，MSBuild 将：</span><span class="sxs-lookup"><span data-stu-id="06851-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="06851-129">生成解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="06851-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="06851-130">为 web 应用程序项目生成可部署的 web 包。</span><span class="sxs-lookup"><span data-stu-id="06851-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="06851-131">为数据库项目生成 .dbschema 和 deploymanifest 文件。</span><span class="sxs-lookup"><span data-stu-id="06851-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="06851-132">将 web 包部署到 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="06851-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="06851-133">将数据库部署到数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="06851-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="06851-134">运行部署</span><span class="sxs-lookup"><span data-stu-id="06851-134">Run the Deployment</span></span>

<span data-ttu-id="06851-135">为目标环境创建了命令文件后，只需运行该文件就能完成整个部署。</span><span class="sxs-lookup"><span data-stu-id="06851-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="06851-136">**将 Contact Manager 解决方案部署到测试环境**</span><span class="sxs-lookup"><span data-stu-id="06851-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="06851-137">在开发人员工作站上，打开 Windows 资源管理器，然后浏览到*Publish-Dev*文件的位置。</span><span class="sxs-lookup"><span data-stu-id="06851-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="06851-138">双击该文件以运行该文件。</span><span class="sxs-lookup"><span data-stu-id="06851-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="06851-139">如果出现 "**打开文件–安全警告**" 对话框，请单击 "**运行**"。</span><span class="sxs-lookup"><span data-stu-id="06851-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="06851-140">如果正确设置了配置设置和测试服务器，则 "命令提示符" 窗口将在 MSBuild 完成项目文件处理后显示 "**生成成功**" 消息。</span><span class="sxs-lookup"><span data-stu-id="06851-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="06851-141">如果这是你第一次将解决方案部署到此环境中，则需要将测试 web 服务器计算机帐户添加到**ContactManager**数据库上**db\_datawriter**和**db\_datareader**角色。</span><span class="sxs-lookup"><span data-stu-id="06851-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="06851-142">为[Web 部署发布配置数据库服务器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)中介绍了此过程。</span><span class="sxs-lookup"><span data-stu-id="06851-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="06851-143">仅需在创建数据库时分配这些权限。</span><span class="sxs-lookup"><span data-stu-id="06851-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="06851-144">默认情况下，生成过程将不会在每次部署&#x2014;时重新创建数据库，而是将现有数据库与最新架构进行比较，并仅进行所需的更改。</span><span class="sxs-lookup"><span data-stu-id="06851-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="06851-145">因此，在首次部署解决方案时，只需映射这些数据库角色。</span><span class="sxs-lookup"><span data-stu-id="06851-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="06851-146">打开 Internet Explorer 并浏览到联系人管理器应用程序的 URL （例如 `http://testweb1:85/ContactManager/`）。</span><span class="sxs-lookup"><span data-stu-id="06851-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="06851-147">验证应用程序是否按预期工作，以及是否能够添加联系人。</span><span class="sxs-lookup"><span data-stu-id="06851-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="06851-148">结束语</span><span class="sxs-lookup"><span data-stu-id="06851-148">Conclusion</span></span>

<span data-ttu-id="06851-149">通过创建包含 MSBuild 说明的命令文件，可以快速轻松地构建多项目解决方案并将其部署到特定目标环境。</span><span class="sxs-lookup"><span data-stu-id="06851-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="06851-150">如果需要反复将解决方案部署到多个目标环境，可以创建多个命令文件。</span><span class="sxs-lookup"><span data-stu-id="06851-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="06851-151">在每个命令文件中，MSBuild 命令将生成相同的通用项目文件，但它会指定其他特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="06851-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="06851-152">例如，要发布到开发人员或测试环境的命令文件可能包含以下 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="06851-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="06851-153">要发布到过渡环境的命令文件可能包含以下 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="06851-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="06851-154">有关如何为自己的服务器环境自定义特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="06851-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="06851-155">还可以通过在 MSBuild 命令中重写属性或设置各种其他开关，为每个环境自定义生成过程。</span><span class="sxs-lookup"><span data-stu-id="06851-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="06851-156">有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06851-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="06851-157">[上一页](deploying-database-projects.md)
> [下一页](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="06851-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
