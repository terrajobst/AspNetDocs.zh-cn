---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 执行 What If 部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web 部署）和 V ...，来执行 "假设" （或模拟）部署。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510332"
---
# <a name="performing-a-what-if-deployment"></a><span data-ttu-id="20dbc-103">执行“What If”部署</span><span class="sxs-lookup"><span data-stu-id="20dbc-103">Performing a "What If" Deployment</span></span>

<span data-ttu-id="20dbc-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="20dbc-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="20dbc-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="20dbc-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="20dbc-106">本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web 部署）和 VSDBCMD 来执行 "假设" （或模拟）部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="20dbc-107">这样，你就可以在实际部署应用程序之前，确定你的部署逻辑对特定目标环境的影响。</span><span class="sxs-lookup"><span data-stu-id="20dbc-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>

<span data-ttu-id="20dbc-108">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="20dbc-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="20dbc-109">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中描述的拆分项目文件方法，其中，生成和部署过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含环境特定的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="20dbc-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="20dbc-110">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="20dbc-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="20dbc-111">为 Web 包执行 "What If" 部署</span><span class="sxs-lookup"><span data-stu-id="20dbc-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="20dbc-112">Web 部署包含了一些功能，可用于在 "假设" （或 "试用"）模式下执行部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="20dbc-113">当你在 "假设" 模式下部署项目时，Web 部署会生成一个日志文件，就像你已执行部署一样，但它实际上不会更改目标服务器上的任何内容。</span><span class="sxs-lookup"><span data-stu-id="20dbc-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="20dbc-114">查看日志文件可帮助你了解部署在目标服务器上的影响，具体取决于：</span><span class="sxs-lookup"><span data-stu-id="20dbc-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="20dbc-115">添加的内容。</span><span class="sxs-lookup"><span data-stu-id="20dbc-115">What will get added.</span></span>
- <span data-ttu-id="20dbc-116">将更新的内容。</span><span class="sxs-lookup"><span data-stu-id="20dbc-116">What will get updated.</span></span>
- <span data-ttu-id="20dbc-117">删除的内容。</span><span class="sxs-lookup"><span data-stu-id="20dbc-117">What will get deleted.</span></span>

<span data-ttu-id="20dbc-118">由于 "假设" 部署实际上不会更改目标服务器上的任何内容，因此它无法始终预测部署是否会成功。</span><span class="sxs-lookup"><span data-stu-id="20dbc-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="20dbc-119">如[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)中所述，可以通过两种方式使用 Web 部署以两&#x2014;种方式部署 web 包：直接使用 msdeploy.exe 命令行实用程序或运行生成过程生成的 *.deploy .cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="20dbc-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="20dbc-120">如果要直接使用 Msdeploy.exe，可以通过将 **– whatif**标志添加到命令来运行 "假设" 部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="20dbc-121">例如，若要评估在将 ContactManager 包部署到过渡环境时将发生的情况，Msdeploy.exe 命令应如下所示：</span><span class="sxs-lookup"><span data-stu-id="20dbc-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

<span data-ttu-id="20dbc-122">如果对 "假设" 部署的结果感到满意，则可以删除 **– whatif**标志来运行实时部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="20dbc-123">有关 Msdeploy.exe 的命令行选项的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="20dbc-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>

<span data-ttu-id="20dbc-124">如果你使用的是 *.deploy .cmd*文件，则可以在命令中包含 **/t**标志（试用模式）标志，而不是在命令中包含 **/y**标志（"是" 或 "更新" 模式）来运行 "假设"。</span><span class="sxs-lookup"><span data-stu-id="20dbc-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="20dbc-125">例如，若要评估通过运行 *.deploy .cmd*文件部署 ContactManager 包时将发生的情况，命令应如下所示：</span><span class="sxs-lookup"><span data-stu-id="20dbc-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

<span data-ttu-id="20dbc-126">当你对 "试用模式" 部署的结果感到满意后，可以将 **/t**标志替换为 **/y**标志，以运行实时部署：</span><span class="sxs-lookup"><span data-stu-id="20dbc-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="20dbc-127">有关 *.deploy .cmd*文件的命令行选项的详细信息，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="20dbc-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="20dbc-128">如果在未指定任何标志的情况下运行 *.deploy .cmd*文件，则命令提示符将显示可用标志的列表。</span><span class="sxs-lookup"><span data-stu-id="20dbc-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>

## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="20dbc-129">为数据库执行 "What If" 部署</span><span class="sxs-lookup"><span data-stu-id="20dbc-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="20dbc-130">本部分假设你要使用 VSDBCMD 实用工具执行基于架构的增量数据库部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="20dbc-131">[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)中更详细地介绍了这种方法。</span><span class="sxs-lookup"><span data-stu-id="20dbc-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="20dbc-132">在应用此处所述的概念之前，我们建议你熟悉本主题。</span><span class="sxs-lookup"><span data-stu-id="20dbc-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="20dbc-133">在**部署**模式下使用 VSDBCMD 时，可以使用 **/Dd** （或 **/DEPLOYTODATABASE**）标志来控制 VSDBCMD 是实际部署数据库还是只生成部署脚本。</span><span class="sxs-lookup"><span data-stu-id="20dbc-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="20dbc-134">如果要部署 .dbschema 文件，这是行为：</span><span class="sxs-lookup"><span data-stu-id="20dbc-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="20dbc-135">如果指定 **/dd +** 或 **/Dd**，则 VSDBCMD 将生成部署脚本并部署数据库。</span><span class="sxs-lookup"><span data-stu-id="20dbc-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="20dbc-136">如果指定 **/dd-** 或省略开关，则 VSDBCMD 将仅生成部署脚本。</span><span class="sxs-lookup"><span data-stu-id="20dbc-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="20dbc-137">如果部署的是 deploymanifest 文件而不是 .dbschema 文件，则 **/dd**开关的行为要复杂得多。</span><span class="sxs-lookup"><span data-stu-id="20dbc-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="20dbc-138">实质上，如果 deploymanifest 文件包含值为**True**的**DeployToDatabase**元素，则 VSDBCMD 将忽略 **/dd**开关的值。</span><span class="sxs-lookup"><span data-stu-id="20dbc-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="20dbc-139">[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)完全说明了此行为。</span><span class="sxs-lookup"><span data-stu-id="20dbc-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>

<span data-ttu-id="20dbc-140">例如，若要为**ContactManager**数据库生成部署脚本而不实际部署数据库，则 VSDBCMD 命令应如下所示：</span><span class="sxs-lookup"><span data-stu-id="20dbc-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

<span data-ttu-id="20dbc-141">VSDBCMD 是一个差异数据库部署工具，因此部署脚本会动态生成，以包含更新当前数据库（如果存在）到指定架构所需的所有 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="20dbc-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="20dbc-142">查看部署脚本是一种有用的方法，用于确定您的部署对当前数据库及其包含的数据产生的影响。</span><span class="sxs-lookup"><span data-stu-id="20dbc-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="20dbc-143">例如，你可能想要确定：</span><span class="sxs-lookup"><span data-stu-id="20dbc-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="20dbc-144">是否将删除任何现有的表，以及是否将导致数据丢失。</span><span class="sxs-lookup"><span data-stu-id="20dbc-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="20dbc-145">操作的顺序是否会产生数据丢失的风险，例如，是拆分或合并表。</span><span class="sxs-lookup"><span data-stu-id="20dbc-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="20dbc-146">如果你对部署脚本感到满意，则可以使用 **/dd +** 标志重复 VSDBCMD 以进行更改。</span><span class="sxs-lookup"><span data-stu-id="20dbc-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="20dbc-147">或者，您可以编辑部署脚本以满足您的要求，然后在数据库服务器上手动执行它。</span><span class="sxs-lookup"><span data-stu-id="20dbc-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="20dbc-148">将 "What If" 功能集成到自定义项目文件</span><span class="sxs-lookup"><span data-stu-id="20dbc-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="20dbc-149">在更复杂的部署方案中，你将需要使用自定义 Microsoft 生成引擎（MSBuild）项目文件来封装生成和部署逻辑，如[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="20dbc-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="20dbc-150">例如，在[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案中，*发布*文件：</span><span class="sxs-lookup"><span data-stu-id="20dbc-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="20dbc-151">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="20dbc-151">Builds the solution.</span></span>
- <span data-ttu-id="20dbc-152">使用 Web 部署打包和部署 ContactManager 应用程序。</span><span class="sxs-lookup"><span data-stu-id="20dbc-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="20dbc-153">使用 Web 部署打包和部署 ContactManager 应用程序。</span><span class="sxs-lookup"><span data-stu-id="20dbc-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="20dbc-154">部署**ContactManager**数据库。</span><span class="sxs-lookup"><span data-stu-id="20dbc-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="20dbc-155">以这种方式将多个 web 包和/或数据库的部署集成到单个步骤过程中时，您可能还希望在 "假设" 模式下执行整个部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="20dbc-156">*发布 proj*文件演示了如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="20dbc-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="20dbc-157">首先，需要创建属性以存储 "假设值" 值：</span><span class="sxs-lookup"><span data-stu-id="20dbc-157">First, you need to create a property to store the "what if" value:</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

<span data-ttu-id="20dbc-158">在这种情况下，你已经创建了一个名为**WhatIf**的属性，其默认值为**false**。</span><span class="sxs-lookup"><span data-stu-id="20dbc-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="20dbc-159">用户可以通过将命令行参数中的属性设置为**true** ，来重写此值，如稍后所示。</span><span class="sxs-lookup"><span data-stu-id="20dbc-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="20dbc-160">下一阶段是参数化任何 Web 部署和 VSDBCMD 命令，使标志反映**WhatIf**属性值。</span><span class="sxs-lookup"><span data-stu-id="20dbc-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="20dbc-161">例如，下一个目标（从*Publish*文件开始，并简化）会运行 *.deploy .cmd*文件来部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="20dbc-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="20dbc-162">默认情况下，该命令包含 **/y**开关（"是" 或 "更新" 模式）。</span><span class="sxs-lookup"><span data-stu-id="20dbc-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="20dbc-163">如果 " **WhatIf** " 设置为 " **true**"，则会将其替换为 **/t**开关（试用或 "假设" 模式）。</span><span class="sxs-lookup"><span data-stu-id="20dbc-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

<span data-ttu-id="20dbc-164">同样，下一个目标使用 VSDBCMD 实用程序来部署数据库。</span><span class="sxs-lookup"><span data-stu-id="20dbc-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="20dbc-165">默认情况下，不包括 **/dd**开关。</span><span class="sxs-lookup"><span data-stu-id="20dbc-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="20dbc-166">这意味着 VSDBCMD 将生成一个部署脚本，但不会部署该数据库&#x2014;，即 "假设" 方案。</span><span class="sxs-lookup"><span data-stu-id="20dbc-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="20dbc-167">如果**WhatIf**属性未设置为**true**，则将添加 **/dd**开关，并且 VSDBCMD 将部署该数据库。</span><span class="sxs-lookup"><span data-stu-id="20dbc-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

<span data-ttu-id="20dbc-168">您可以使用相同的方法参数化项目文件中的所有相关命令。</span><span class="sxs-lookup"><span data-stu-id="20dbc-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="20dbc-169">如果要运行 "假设" 部署，只需从命令行提供**WhatIf**属性值即可：</span><span class="sxs-lookup"><span data-stu-id="20dbc-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

<span data-ttu-id="20dbc-170">通过这种方式，您可以在单个步骤中为所有项目组件运行 "假设" 部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="20dbc-171">结束语</span><span class="sxs-lookup"><span data-stu-id="20dbc-171">Conclusion</span></span>

<span data-ttu-id="20dbc-172">本主题介绍了如何使用 Web 部署、VSDBCMD 和 MSBuild 来运行 "假设" 部署。</span><span class="sxs-lookup"><span data-stu-id="20dbc-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="20dbc-173">"假设" 部署可让你在实际对目标环境进行任何更改之前评估建议的部署的影响。</span><span class="sxs-lookup"><span data-stu-id="20dbc-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="20dbc-174">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="20dbc-174">Further Reading</span></span>

<span data-ttu-id="20dbc-175">有关 Web 部署命令行语法的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="20dbc-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="20dbc-176">有关使用 *.deploy*文件时的命令行选项的指导，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="20dbc-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="20dbc-177">有关 VSDBCMD 命令行语法的指导，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)。</span><span class="sxs-lookup"><span data-stu-id="20dbc-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20dbc-178">[上一页](advanced-enterprise-web-deployment.md)
> [下一页](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="20dbc-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>
