---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 创建支持部署的生成定义 |Microsoft Docs
author: jrjlee
description: 如果要在 Team Foundation Server （TFS）2010中执行任何类型的生成，则需要在团队项目中创建生成定义。 本主题 des 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489008"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a><span data-ttu-id="a1542-104">创建支持部署的生成定义</span><span class="sxs-lookup"><span data-stu-id="a1542-104">Creating a Build Definition That Supports Deployment</span></span>

<span data-ttu-id="a1542-105">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a1542-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a1542-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a1542-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a1542-107">如果要在 Team Foundation Server （TFS）2010中执行任何类型的生成，则需要在团队项目中创建生成定义。</span><span class="sxs-lookup"><span data-stu-id="a1542-107">If you want to perform any kind of build in Team Foundation Server (TFS) 2010, you need to create a build definition within your team project.</span></span> <span data-ttu-id="a1542-108">本主题介绍如何在 TFS 中创建新的生成定义，以及如何在 Team Build 中作为生成过程的一部分来控制 web 部署。</span><span class="sxs-lookup"><span data-stu-id="a1542-108">This topic describes how to create a new build definition in TFS and how to control web deployment as part of the build process in Team Build.</span></span>

<span data-ttu-id="a1542-109">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="a1542-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="a1542-110">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中描述的拆分项目文件方法，其中，生成和部署过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含环境特定的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="a1542-110">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="a1542-111">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="a1542-111">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="a1542-112">任务概述</span><span class="sxs-lookup"><span data-stu-id="a1542-112">Task Overview</span></span>

<span data-ttu-id="a1542-113">生成定义是控制 TFS 中团队项目的生成方式和时间的机制。</span><span class="sxs-lookup"><span data-stu-id="a1542-113">A build definition is the mechanism that controls how and when builds occur for team projects in TFS.</span></span> <span data-ttu-id="a1542-114">每个生成定义指定：</span><span class="sxs-lookup"><span data-stu-id="a1542-114">Each build definition specifies:</span></span>

- <span data-ttu-id="a1542-115">要生成的项，如 Visual Studio 解决方案文件或自定义 Microsoft 生成引擎（MSBuild）项目文件。</span><span class="sxs-lookup"><span data-stu-id="a1542-115">The things you want to build, like Visual Studio solution files or custom Microsoft Build Engine (MSBuild) project files.</span></span>
- <span data-ttu-id="a1542-116">确定生成应发生的条件的条件，如手动触发器、持续集成（CI）或封闭签入。</span><span class="sxs-lookup"><span data-stu-id="a1542-116">The criteria that determine when a build should take place, like manual triggers, continuous integration (CI), or gated check-ins.</span></span>
- <span data-ttu-id="a1542-117">团队生成应将生成输出发送到的位置，包括部署项目，例如 web 包和数据库脚本。</span><span class="sxs-lookup"><span data-stu-id="a1542-117">The location to which Team Build should send build outputs, including deployment artifacts like web packages and database scripts.</span></span>
- <span data-ttu-id="a1542-118">应保留每个生成的时间量。</span><span class="sxs-lookup"><span data-stu-id="a1542-118">The amount of time that each build should be retained.</span></span>
- <span data-ttu-id="a1542-119">生成过程的各种其他参数。</span><span class="sxs-lookup"><span data-stu-id="a1542-119">Various other parameters of the build process.</span></span>

> [!NOTE]
> <span data-ttu-id="a1542-120">有关生成定义的详细信息，请参阅[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1542-120">For more information on build definitions, see [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span>

<span data-ttu-id="a1542-121">本主题将演示如何创建使用 CI 的生成定义，以便在开发人员签入新内容时触发生成。</span><span class="sxs-lookup"><span data-stu-id="a1542-121">This topic will show you how to create a build definition that uses CI, so that a build is triggered when a developer checks in new content.</span></span> <span data-ttu-id="a1542-122">如果生成成功，则生成服务运行自定义项目文件以将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="a1542-122">If the build succeeds, the build service runs a custom project file to deploy the solution to a test environment.</span></span>

<span data-ttu-id="a1542-123">触发生成时，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a1542-123">When you trigger a build, these actions need to happen:</span></span>

- <span data-ttu-id="a1542-124">首先，团队构建应生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="a1542-124">First, Team Build should build the solution.</span></span> <span data-ttu-id="a1542-125">作为此过程的一部分，团队生成将调用 Web 发布管道（WPP）以生成解决方案中每个 web 应用程序项目的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="a1542-125">As part of this process, Team Build will invoke the Web Publishing Pipeline (WPP) to generate web deployment packages for each of the web application projects in the solution.</span></span> <span data-ttu-id="a1542-126">Team Build 还将运行与解决方案关联的所有单元测试。</span><span class="sxs-lookup"><span data-stu-id="a1542-126">Team Build will also run any unit tests associated with the solution.</span></span>
- <span data-ttu-id="a1542-127">如果解决方案生成失败，则团队生成不需要进一步操作。</span><span class="sxs-lookup"><span data-stu-id="a1542-127">If the solution build fails, Team Build should take no further action.</span></span> <span data-ttu-id="a1542-128">应将单元测试失败视为生成失败。</span><span class="sxs-lookup"><span data-stu-id="a1542-128">Unit test failures should be treated as a build failure.</span></span>
- <span data-ttu-id="a1542-129">如果解决方案生成成功，则团队生成应运行控制解决方案部署的自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="a1542-129">If the solution build succeeds, Team Build should run the custom project file that controls the deployment of the solution.</span></span> <span data-ttu-id="a1542-130">作为此过程的一部分，Team Build 将调用 Internet Information Services （IIS） Web 部署工具（Web 部署）在目标 Web 服务器上安装打包的 web 应用程序，并且它将调用 VSDBCMD 实用工具来运行数据库创建目标数据库服务器上的脚本。</span><span class="sxs-lookup"><span data-stu-id="a1542-130">As part of this process, Team Build will invoke the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to install the packaged web applications on the destination web servers, and it will invoke the VSDBCMD.exe utility to run database creation scripts on the destination database servers.</span></span>

<span data-ttu-id="a1542-131">这说明了该过程：</span><span class="sxs-lookup"><span data-stu-id="a1542-131">This illustrates the process:</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

<span data-ttu-id="a1542-132">[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案包含自定义的 msbuild 项目文件 *，该*文件可从 msbuild 或 Team Build 中运行。</span><span class="sxs-lookup"><span data-stu-id="a1542-132">The [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution includes a custom MSBuild project file, *Publish.proj*, that you can run from MSBuild or Team Build.</span></span> <span data-ttu-id="a1542-133">如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述，此项目文件定义了将 web 包和数据库部署到目标环境的逻辑。</span><span class="sxs-lookup"><span data-stu-id="a1542-133">As described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), this project file defines the logic that deploys your web packages and databases to a target environment.</span></span> <span data-ttu-id="a1542-134">此文件包含在生成和打包过程中运行的逻辑，如果该过程在 Team Build 中运行，则只保留运行的部署任务。</span><span class="sxs-lookup"><span data-stu-id="a1542-134">The file includes logic that omits the building and packaging process if it's running in Team Build, leaving just the deployment tasks to run.</span></span> <span data-ttu-id="a1542-135">这是因为，当你以这种方式自动执行部署时，通常需要确保解决方案成功生成，并在部署过程开始之前通过所有单元测试。</span><span class="sxs-lookup"><span data-stu-id="a1542-135">This is because when you automate deployment in this way, you'll typically want to ensure that the solution builds successfully and passes any unit tests before the deployment process commences.</span></span>

<span data-ttu-id="a1542-136">下一节将介绍如何通过创建新的生成定义来实现此过程。</span><span class="sxs-lookup"><span data-stu-id="a1542-136">The next section explains how to implement this process by creating a new build definition.</span></span>

> [!NOTE]
> <span data-ttu-id="a1542-137">在此&#x2014;过程中，单个自动过程生成、测试和部署解决方案&#x2014;可能最适合部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="a1542-137">This procedure&#x2014;in which a single automated process builds, tests, and deploys a solution&#x2014;is likely to be most suited to deployment to test environments.</span></span> <span data-ttu-id="a1542-138">对于过渡环境和生产环境，您很可能希望从已在测试环境中验证和验证的以前版本部署内容。</span><span class="sxs-lookup"><span data-stu-id="a1542-138">For staging and production environments you're a lot more likely to want to deploy content from a previous build that you've already verified and validated in a test environment.</span></span> <span data-ttu-id="a1542-139">下一主题[部署特定生成](deploying-a-specific-build.md)中介绍了此方法。</span><span class="sxs-lookup"><span data-stu-id="a1542-139">This approach is described in the next topic, [Deploying a Specific Build](deploying-a-specific-build.md).</span></span>

### <a name="who-performs-this-procedure"></a><span data-ttu-id="a1542-140">谁执行此过程？</span><span class="sxs-lookup"><span data-stu-id="a1542-140">Who Performs This Procedure?</span></span>

<span data-ttu-id="a1542-141">通常，TFS 管理员执行此过程。</span><span class="sxs-lookup"><span data-stu-id="a1542-141">Typically, a TFS administrator performs this procedure.</span></span> <span data-ttu-id="a1542-142">在某些情况下，开发人员团队负责人可能负责 TFS 中的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="a1542-142">In some cases, a developer team leader may take responsibility for the team project collection in TFS.</span></span> <span data-ttu-id="a1542-143">若要创建新的生成定义，你必须是包含你的解决方案的团队项目集合的 "**项目集合生成管理员**" 组的成员。</span><span class="sxs-lookup"><span data-stu-id="a1542-143">In order to create a new build definition, you need to be a member of the **Project Collection Build Administrators** group for the team project collection that contains your solution.</span></span>

## <a name="create-a-build-definition-for-ci-and-deployment"></a><span data-ttu-id="a1542-144">创建 CI 和部署的生成定义</span><span class="sxs-lookup"><span data-stu-id="a1542-144">Create a Build Definition for CI and Deployment</span></span>

<span data-ttu-id="a1542-145">下一过程介绍如何创建 CI 触发的生成定义。</span><span class="sxs-lookup"><span data-stu-id="a1542-145">The next procedure describes how to create a build definition that CI triggers.</span></span> <span data-ttu-id="a1542-146">如果生成成功，则使用自定义 MSBuild 项目文件中的逻辑来部署解决方案。</span><span class="sxs-lookup"><span data-stu-id="a1542-146">If the build succeeds, the solution is deployed using the logic in a custom MSBuild project file.</span></span>

<span data-ttu-id="a1542-147">**为 CI 和部署创建生成定义**</span><span class="sxs-lookup"><span data-stu-id="a1542-147">**To create a build definition for CI and deployment**</span></span>

1. <span data-ttu-id="a1542-148">在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，展开 "团队项目" 节点，右键单击 "**生成**"，然后单击 "**新建生成定义**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-148">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. <span data-ttu-id="a1542-149">在 "**常规**" 选项卡上，为生成定义指定一个名称（例如， **DeployToTest**）和一个可选说明。</span><span class="sxs-lookup"><span data-stu-id="a1542-149">On the **General** tab, give the build definition a name (for example, **DeployToTest**) and an optional description.</span></span>
3. <span data-ttu-id="a1542-150">在 "**触发器**" 选项卡上，选择要触发新生成的条件。</span><span class="sxs-lookup"><span data-stu-id="a1542-150">On the **Trigger** tab, select the criteria on which you want to trigger a new build.</span></span> <span data-ttu-id="a1542-151">例如，如果想要生成解决方案并将其部署到测试环境，则每次开发人员签入新代码时，请选择 "**持续集成**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-151">For example, if you want to build the solution and deploy to the test environment every time a developer checks in new code, select **Continuous Integration**.</span></span>
4. <span data-ttu-id="a1542-152">在 "**生成默认值**" 选项卡上的 "**将生成输出复制到以下放置文件夹**" 框中，键入放置文件夹的通用命名约定（UNC）路径（例如 **\\TFSBUILD\Drops**）。</span><span class="sxs-lookup"><span data-stu-id="a1542-152">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="a1542-153">此放置位置存储多个版本，具体取决于你配置的保留策略。</span><span class="sxs-lookup"><span data-stu-id="a1542-153">This drop location stores several builds, depending on the retention policy you configure.</span></span> <span data-ttu-id="a1542-154">如果要将部署项目从特定生成发布到过渡环境或生产环境，可在此处找到这些项目。</span><span class="sxs-lookup"><span data-stu-id="a1542-154">When you want to publish deployment artifacts from a specific build to a staging or production environment, this is where you'll find them.</span></span>
5. <span data-ttu-id="a1542-155">在 "**进程**" 选项卡上的 "**生成过程文件**" 下拉列表中，选择 " **defaulttemplate.11.1.xaml** "。</span><span class="sxs-lookup"><span data-stu-id="a1542-155">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="a1542-156">这是添加到所有新团队项目的默认生成过程模板之一。</span><span class="sxs-lookup"><span data-stu-id="a1542-156">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="a1542-157">在 "**生成过程参数**" 表中，单击 "**要生成的项**" 行，然后单击**省略号**按钮。</span><span class="sxs-lookup"><span data-stu-id="a1542-157">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. <span data-ttu-id="a1542-158">在 "**要生成的项**" 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-158">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="a1542-159">浏览到解决方案文件的位置，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="a1542-159">Browse to the location of your solution file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. <span data-ttu-id="a1542-160">在 "**要生成的项**" 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-160">In the **Items to Build** dialog box, click **Add**.</span></span>
10. <span data-ttu-id="a1542-161">在 "**项类型**" 下拉列表中，选择 " **MSBuild 项目文件**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-161">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
11. <span data-ttu-id="a1542-162">浏览到用于控制部署过程的自定义项目文件的位置，选择该文件，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="a1542-162">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. <span data-ttu-id="a1542-163">"**要生成的项**" 对话框现在应显示两个项。</span><span class="sxs-lookup"><span data-stu-id="a1542-163">The **Items to Build** dialog box should now show two items.</span></span> <span data-ttu-id="a1542-164">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="a1542-164">Click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. <span data-ttu-id="a1542-165">在 "**进程**" 选项卡上的 "**生成过程参数**" 表中，展开 "**高级**" 部分。</span><span class="sxs-lookup"><span data-stu-id="a1542-165">On the **Process** tab, in the **Build process parameters** table, expand the **Advanced** section.</span></span>
14. <span data-ttu-id="a1542-166">在 " **MSBuild 参数**" 行中，添加要*生成的任何*项所需的 MSBuild 命令行参数。</span><span class="sxs-lookup"><span data-stu-id="a1542-166">In the **MSBuild Arguments** row, add any MSBuild command-line arguments that *either* of your items to build requires.</span></span> <span data-ttu-id="a1542-167">在 Contact Manager 解决方案方案中，需要以下参数：</span><span class="sxs-lookup"><span data-stu-id="a1542-167">In the Contact Manager solution scenario, these arguments are required:</span></span>

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. <span data-ttu-id="a1542-168">在此示例中：</span><span class="sxs-lookup"><span data-stu-id="a1542-168">In this example:</span></span>

    1. <span data-ttu-id="a1542-169">当你生成联系人管理器解决方案时， **DeployOnBuild = true**和**DeployTarget = package**参数是必需的。</span><span class="sxs-lookup"><span data-stu-id="a1542-169">The **DeployOnBuild=true** and **DeployTarget=package** arguments are required when you build the Contact Manager solution.</span></span> <span data-ttu-id="a1542-170">这会指示 MSBuild 在生成每个 web 应用程序项目后创建 web 部署包，如[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="a1542-170">This instructs MSBuild to create web deployment packages after building each web application project, as described in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>
    2. <span data-ttu-id="a1542-171">当你生成*Publish*文件时， **TargetEnvPropsFile**参数是必需的。</span><span class="sxs-lookup"><span data-stu-id="a1542-171">The **TargetEnvPropsFile** argument is required when you build the *Publish.proj* file.</span></span> <span data-ttu-id="a1542-172">此属性指示特定于环境的配置文件的位置，如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="a1542-172">This property indicates the location of the environment-specific configuration file, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>
16. <span data-ttu-id="a1542-173">在 "**保留策略**" 选项卡上，根据需要配置要保留的每种类型的生成数。</span><span class="sxs-lookup"><span data-stu-id="a1542-173">On the **Retention Policy** tab, configure how many builds of each type you want to retain as required.</span></span>
17. <span data-ttu-id="a1542-174">单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="a1542-174">Click **Save**.</span></span>

## <a name="queue-a-build"></a><span data-ttu-id="a1542-175">将生成排入队列</span><span class="sxs-lookup"><span data-stu-id="a1542-175">Queue a Build</span></span>

<span data-ttu-id="a1542-176">此时，您已创建了至少一个新的生成定义。</span><span class="sxs-lookup"><span data-stu-id="a1542-176">At this point, you have created at least one new build definition.</span></span> <span data-ttu-id="a1542-177">你定义的生成过程现在将根据你在生成定义中指定的触发器运行。</span><span class="sxs-lookup"><span data-stu-id="a1542-177">The build process you defined will now run according to the triggers you specified in the build definition.</span></span>

<span data-ttu-id="a1542-178">如果已将生成定义配置为使用 CI，则可以通过两种方式来测试生成定义：</span><span class="sxs-lookup"><span data-stu-id="a1542-178">If you've configured your build definition to use CI, you can test your build definition in two ways:</span></span>

- <span data-ttu-id="a1542-179">将某些内容签入到团队项目以触发自动生成。</span><span class="sxs-lookup"><span data-stu-id="a1542-179">Check in some content to the team project to trigger an automatic build.</span></span>
- <span data-ttu-id="a1542-180">手动对生成进行排队。</span><span class="sxs-lookup"><span data-stu-id="a1542-180">Queue a build manually.</span></span>

<span data-ttu-id="a1542-181">**手动对生成进行排队**</span><span class="sxs-lookup"><span data-stu-id="a1542-181">**To queue a build manually**</span></span>

1. <span data-ttu-id="a1542-182">在 "**团队资源管理器**" 窗口中，右键单击生成定义，然后单击 "使**新生成入队**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-182">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. <span data-ttu-id="a1542-183">在 "**队列生成**" 对话框中，查看 "生成属性"，然后单击 "**队列**"。</span><span class="sxs-lookup"><span data-stu-id="a1542-183">In the **Queue Build** dialog box, review the build properties, and then click **Queue**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

<span data-ttu-id="a1542-184">若要查看生成&#x2014;的进度和结果，而不考虑是否手动触发，或者在 "&#x2014;**团队资源管理器**" 窗口中自动双击生成定义。</span><span class="sxs-lookup"><span data-stu-id="a1542-184">To review the progress and the outcome of a build&#x2014;regardless of whether it was triggered manually or automatically&#x2014;double-click the build definition in the **Team Explorer** window.</span></span> <span data-ttu-id="a1542-185">这将打开 "**生成资源管理器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="a1542-185">This will open a **Build Explorer** tab.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

<span data-ttu-id="a1542-186">在这里，你可以对失败的生成进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="a1542-186">From here, you can troubleshoot failed builds.</span></span> <span data-ttu-id="a1542-187">如果双击单个生成，则可以查看摘要信息，并单击 "到详细日志文件"。</span><span class="sxs-lookup"><span data-stu-id="a1542-187">If you double-click an individual build, you can view summary information and click through to detailed log files.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

<span data-ttu-id="a1542-188">您可以使用此信息对失败的生成进行故障排除并解决所有问题，然后再尝试其他生成。</span><span class="sxs-lookup"><span data-stu-id="a1542-188">You can use this information to troubleshoot failed builds and address any problems before you attempt another build.</span></span>

> [!NOTE]
> <span data-ttu-id="a1542-189">在您向生成服务器授予目标环境中所需的任何权限之前，执行部署逻辑的生成可能会失败。</span><span class="sxs-lookup"><span data-stu-id="a1542-189">Builds that execute deployment logic are likely to fail until you have granted the build server any permissions required in the destination environment.</span></span> <span data-ttu-id="a1542-190">有关详细信息，请参阅[配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a1542-190">For more information, see [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span>

## <a name="monitor-the-build-process"></a><span data-ttu-id="a1542-191">监视生成过程</span><span class="sxs-lookup"><span data-stu-id="a1542-191">Monitor the Build Process</span></span>

<span data-ttu-id="a1542-192">TFS 提供范围广泛的功能，可帮助您监视生成过程。</span><span class="sxs-lookup"><span data-stu-id="a1542-192">TFS provides a broad range of functionality to help you monitor the build process.</span></span> <span data-ttu-id="a1542-193">例如，TFS 可以在生成完成时向你发送电子邮件，或在任务栏通知区域中显示警报。</span><span class="sxs-lookup"><span data-stu-id="a1542-193">For example, TFS can send you an email or display alerts in your taskbar notification area when a build has completed.</span></span> <span data-ttu-id="a1542-194">有关详细信息，请参阅[运行和监视生成](https://msdn.microsoft.com/library/ms181721.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1542-194">For more information, see [Run and Monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="a1542-195">结束语</span><span class="sxs-lookup"><span data-stu-id="a1542-195">Conclusion</span></span>

<span data-ttu-id="a1542-196">本主题介绍了如何在 TFS 中创建生成定义。</span><span class="sxs-lookup"><span data-stu-id="a1542-196">This topic described how to create a build definition in TFS.</span></span> <span data-ttu-id="a1542-197">生成定义是为 CI 配置的，因此每当开发人员将内容签入到团队项目时，生成过程都将运行。</span><span class="sxs-lookup"><span data-stu-id="a1542-197">The build definition is configured for CI, so the build process runs whenever a developer checks in content to the team project.</span></span> <span data-ttu-id="a1542-198">生成定义执行自定义 MSBuild 项目文件，以将 web 包和数据库脚本部署到目标服务器环境。</span><span class="sxs-lookup"><span data-stu-id="a1542-198">The build definition executes a custom MSBuild project file to deploy web packages and database scripts to a target server environment.</span></span>

<span data-ttu-id="a1542-199">为了使自动部署在生成过程中成功，您需要向目标 web 服务器和目标数据库服务器上的生成服务帐户授予适当的权限。</span><span class="sxs-lookup"><span data-stu-id="a1542-199">In order for an automated deployment to succeed as part of a build process, you'll need to grant appropriate permissions to the build service account on the target web servers and the target database server.</span></span> <span data-ttu-id="a1542-200">本教程中的最后一个主题是[配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)，介绍如何识别和配置从 Team build server 进行自动部署所需的权限。</span><span class="sxs-lookup"><span data-stu-id="a1542-200">The final topic in this tutorial, [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md), describes how to identify and configure the permissions required for automated deployment from a Team Build server.</span></span>

## <a name="further-reading"></a><span data-ttu-id="a1542-201">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="a1542-201">Further Reading</span></span>

<span data-ttu-id="a1542-202">有关创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)和[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1542-202">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="a1542-203">有关如何对生成进行排队的详细指南，请参阅对[生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1542-203">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1542-204">[上一页](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一页](deploying-a-specific-build.md)</span><span class="sxs-lookup"><span data-stu-id="a1542-204">[Previous](configuring-a-tfs-build-server-for-web-deployment.md)
[Next](deploying-a-specific-build.md)</span></span>
