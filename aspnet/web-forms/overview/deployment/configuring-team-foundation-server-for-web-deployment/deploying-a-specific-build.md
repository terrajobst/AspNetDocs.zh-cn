---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 部署特定版本 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何将 web 包和数据库脚本从特定的先前版本部署到新的目标，例如过渡或生产流程图 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519572"
---
# <a name="deploying-a-specific-build"></a><span data-ttu-id="ea9b3-103">部署特定生成</span><span class="sxs-lookup"><span data-stu-id="ea9b3-103">Deploying a Specific Build</span></span>

<span data-ttu-id="ea9b3-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ea9b3-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ea9b3-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="ea9b3-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ea9b3-106">本主题介绍如何将 web 包和数据库脚本从特定的先前版本部署到新的目标，例如过渡环境或生产环境。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>

<span data-ttu-id="ea9b3-107">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="ea9b3-108">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中描述的拆分项目文件方法，其中，生成和部署过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含环境特定的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="ea9b3-109">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="ea9b3-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="ea9b3-110">Task Overview</span></span>

<span data-ttu-id="ea9b3-111">到目前为止，本教程集中的主题重点介绍如何在单步或自动过程中生成、打包和部署 web 应用程序和数据库。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="ea9b3-112">但是，在某些常见情况下，你需要从放置文件夹中的生成列表中选择要部署的资源。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="ea9b3-113">换句话说，最新的生成可能不是要部署的生成。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="ea9b3-114">请考虑上一主题中所述的持续集成（CI）方案，[创建支持部署的生成定义](creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="ea9b3-115">已在 Team Foundation Server （TFS）2010中创建了生成定义。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="ea9b3-116">开发人员每次将代码签入 TFS 时，团队生成将生成您的代码，创建 web 包和数据库脚本作为生成过程的一部分，运行任何单元测试，并将资源部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="ea9b3-117">根据你在创建生成定义时配置的保留策略，TFS 将保留特定数量的以前版本。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="ea9b3-118">现在，假设已对测试环境中的其中一种版本执行验证和验证测试，并且已准备好将应用程序部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="ea9b3-119">同时，开发人员可能已签入新代码。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="ea9b3-120">不需要重新生成解决方案并将其部署到过渡环境，而不希望将最新版本部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="ea9b3-121">相反，你希望部署在测试服务器上已验证并验证的特定生成。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="ea9b3-122">若要实现此目的，需要告知 Microsoft 生成引擎（MSBuild），其中查找生成特定生成的 web 包和数据库脚本。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="ea9b3-123">重写 OutputRoot 属性</span><span class="sxs-lookup"><span data-stu-id="ea9b3-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="ea9b3-124">在[示例解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)中， *Publish*文件声明名为**OutputRoot**的属性。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="ea9b3-125">顾名思义，这是包含生成过程生成的所有内容的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="ea9b3-126">在*Publish*文件中，可以看到**OutputRoot**属性指的是所有部署资源的根位置。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9b3-127">**OutputRoot**是常用的属性名称。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="ea9b3-128">视觉C#对象和 Visual Basic 项目文件也会将此属性声明为存储所有生成输出的根位置。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

<span data-ttu-id="ea9b3-129">如果希望项目文件从不同的位置&#x2014;（如以前的 TFS 生成&#x2014;的输出）部署 web 包和数据库脚本，只需重写**OutputRoot**属性。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="ea9b3-130">应将属性值设置为 Team Build server 上的相关生成文件夹。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="ea9b3-131">如果从命令行运行 MSBuild，则可将**OutputRoot**的值指定为命令行参数：</span><span class="sxs-lookup"><span data-stu-id="ea9b3-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

<span data-ttu-id="ea9b3-132">但是，在实践中，如果不打算使用生成输出 ，则&#x2014;还需要跳过生成目标，而无需构建解决方案。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="ea9b3-133">可以通过从命令行指定要执行的目标来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="ea9b3-133">You could do this by specifying the targets you want to execute from the command line:</span></span>

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

<span data-ttu-id="ea9b3-134">但在大多数情况下，你需要在 TFS 生成定义中生成部署逻辑。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="ea9b3-135">这使具有 "**队列生成**" 权限的用户可以通过连接到 TFS 服务器来触发来自任何 Visual Studio 安装的部署。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="ea9b3-136">创建生成定义以部署特定生成</span><span class="sxs-lookup"><span data-stu-id="ea9b3-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="ea9b3-137">下一过程介绍如何创建一个生成定义，使用户能够使用单个命令触发到过渡环境的部署。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="ea9b3-138">在这种情况下，你不希望生成定义实际构建你&#x2014;只想在自定义项目文件中执行部署逻辑的任何内容。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="ea9b3-139">如果文件在 Team Build 中运行，则*Publish*文件包含用于跳过**生成**目标的条件逻辑。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="ea9b3-140">它通过计算内置的**BuildingInTeamBuild**属性来实现此功能，如果您在 Team Build 中运行项目文件，此属性将自动设置为**true** 。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="ea9b3-141">因此，您可以跳过生成过程，只需运行项目文件来部署现有版本。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="ea9b3-142">**创建生成定义以手动触发部署**</span><span class="sxs-lookup"><span data-stu-id="ea9b3-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="ea9b3-143">在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，展开 "团队项目" 节点，右键单击 "**生成**"，然后单击 "**新建生成定义**"。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="ea9b3-144">在 "**常规**" 选项卡上，为生成定义指定一个名称（例如， **DeployToStaging**）和一个可选说明。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="ea9b3-145">在 "**触发器**" 选项卡上，选择 "**手动–签入" 不会触发新的生成**。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="ea9b3-146">在 "**生成默认值**" 选项卡上的 "**将生成输出复制到以下放置文件夹**" 框中，键入放置文件夹的通用命名约定（UNC）路径（例如 **\\TFSBUILD\Drops**）。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="ea9b3-147">在 "**进程**" 选项卡上的 "**生成过程文件**" 下拉列表中，选择 " **defaulttemplate.11.1.xaml** "。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="ea9b3-148">这是添加到所有新团队项目的默认生成过程模板之一。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="ea9b3-149">在 "**生成过程参数**" 表中，单击 "**要生成的项**" 行，然后单击**省略号**按钮。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="ea9b3-150">在 "**要生成的项**" 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="ea9b3-151">在 "**项类型**" 下拉列表中，选择 " **MSBuild 项目文件**"。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="ea9b3-152">浏览到用于控制部署过程的自定义项目文件的位置，选择该文件，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="ea9b3-153">在 "**要生成的项**" 对话框中，单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="ea9b3-154">在 "**生成过程参数**" 表中，展开 "**高级**" 部分。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="ea9b3-155">在 " **MSBuild 参数**" 行中，指定特定于环境的项目文件的位置，并为生成文件夹的位置添加占位符：</span><span class="sxs-lookup"><span data-stu-id="ea9b3-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="ea9b3-156">每次对生成进行排队时，需要重写**OutputRoot**值。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="ea9b3-157">下一过程中会介绍这一点。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="ea9b3-158">单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-158">Click **Save**.</span></span>

<span data-ttu-id="ea9b3-159">触发生成时，需要更新**OutputRoot**属性，使其指向要部署的生成。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="ea9b3-160">**从生成定义部署特定生成**</span><span class="sxs-lookup"><span data-stu-id="ea9b3-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="ea9b3-161">在 "**团队资源管理器**" 窗口中，右键单击生成定义，然后单击 "使**新生成入队**"。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="ea9b3-162">在 "**队列生成**" 对话框中的 "**参数**" 选项卡上，展开 "**高级**" 部分。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="ea9b3-163">在 " **MSBuild 参数**" 行中，将**OutputRoot**属性的值替换为生成文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="ea9b3-164">例如:</span><span class="sxs-lookup"><span data-stu-id="ea9b3-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="ea9b3-165">请确保在生成文件夹路径的末尾包含尾随斜杠。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="ea9b3-166">单击 "**队列**"。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-166">Click **Queue**.</span></span>

<span data-ttu-id="ea9b3-167">当你对生成进行排队时，项目文件将从你在**OutputRoot**属性中指定的生成放置文件夹部署数据库脚本和 web 包。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ea9b3-168">结束语</span><span class="sxs-lookup"><span data-stu-id="ea9b3-168">Conclusion</span></span>

<span data-ttu-id="ea9b3-169">本主题介绍了如何使用 split 项目文件部署模型从特定的先前版本发布部署资源，如 web 包和数据库脚本。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="ea9b3-170">其中介绍了如何重写**OutputRoot**属性，以及如何将部署逻辑并入 TFS 生成定义中。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ea9b3-171">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="ea9b3-171">Further Reading</span></span>

<span data-ttu-id="ea9b3-172">有关创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)和[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="ea9b3-173">有关如何对生成进行排队的详细指南，请参阅对[生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ea9b3-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ea9b3-174">[上一页](creating-a-build-definition-that-supports-deployment.md)
> [下一页](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="ea9b3-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>
