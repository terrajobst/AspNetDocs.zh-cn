---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 将数据库角色成员身份部署到测试环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在将解决方案部署到测试环境时将用户帐户添加到数据库角色中。 在部署包含 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474944"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="5ecc4-104">将数据库角色成员身份部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="5ecc4-104">Deploying Database Role Memberships to Test Environments</span></span>

<span data-ttu-id="5ecc4-105">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="5ecc4-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="5ecc4-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="5ecc4-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="5ecc4-107">本主题介绍如何在将解决方案部署到测试环境时将用户帐户添加到数据库角色中。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="5ecc4-108">在将包含数据库项目的解决方案部署到过渡环境或生产环境时，通常不希望开发人员自动将用户帐户添加到数据库角色。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="5ecc4-109">在大多数情况下，开发人员不知道哪些用户帐户需要添加到哪些数据库角色中，这些要求随时可能会更改。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="5ecc4-110">但是，在将包含数据库项目的解决方案部署到开发或测试环境时，这种情况通常是不同的：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="5ecc4-111">开发人员通常会定期重新部署解决方案，这种情况通常是一天。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="5ecc4-112">通常，在每次部署时都会重新创建数据库，这意味着在每次部署后，必须创建数据库用户并将其添加到角色。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="5ecc4-113">开发人员通常对目标开发或测试环境具有完全控制。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="5ecc4-114">在这种情况下，在部署过程中自动创建数据库用户并分配数据库角色成员身份通常是有益的。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="5ecc4-115">关键因素在于，此操作需要根据目标环境进行条件。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="5ecc4-116">如果要部署到过渡环境或生产环境，则需要跳过该操作。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="5ecc4-117">如果要部署到开发人员或测试环境，则需要部署角色成员身份，而无需进一步干预。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="5ecc4-118">本主题介绍可用于解决此问题的一种方法。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-118">This topic describes one approach you can use to address this challenge.</span></span>

<span data-ttu-id="5ecc4-119">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="5ecc4-120">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="5ecc4-121">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="5ecc4-122">任务概述</span><span class="sxs-lookup"><span data-stu-id="5ecc4-122">Task Overview</span></span>

<span data-ttu-id="5ecc4-123">本主题假定：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-123">This topic assumes that:</span></span>

- <span data-ttu-id="5ecc4-124">按照[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述，使用拆分项目文件方法进行解决方案部署。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="5ecc4-125">从项目文件调用 VSDBCMD 来部署数据库项目，如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="5ecc4-126">若要创建数据库用户并在将数据库项目部署到测试环境时分配角色成员身份，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="5ecc4-127">创建一个使所需的数据库发生更改的 Transact-sql 结构化查询语言（Transact-sql）脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="5ecc4-128">创建一个 Microsoft 生成引擎（MSBuild）目标，该目标使用 sqlcmd 实用程序来运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="5ecc4-129">在将解决方案部署到测试环境时，将项目文件配置为调用目标。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="5ecc4-130">本主题将演示如何执行上述每个过程。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="5ecc4-131">为数据库角色成员身份编写脚本</span><span class="sxs-lookup"><span data-stu-id="5ecc4-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="5ecc4-132">您可以通过许多不同的方式，在您选择的任何位置创建 Transact-sql 脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="5ecc4-133">最简单的方法是在 Visual Studio 2010 的解决方案中创建脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="5ecc4-134">**创建 SQL 脚本**</span><span class="sxs-lookup"><span data-stu-id="5ecc4-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="5ecc4-135">在 "**解决方案资源管理器**" 窗口中，展开您的数据库项目节点。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="5ecc4-136">右键单击 "**脚本**" 文件夹，指向 "**添加**"，然后单击 "**新建文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="5ecc4-137">键入**Test**作为文件夹名称，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="5ecc4-138">右键单击**测试**文件夹，指向 "**添加**"，然后单击 "**脚本**"。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="5ecc4-139">在 "**添加新项**" 对话框中，为脚本提供一个有意义的名称（例如， **AddRoleMemberships**），然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="5ecc4-140">在*AddRoleMemberships*文件中，添加以下 transact-sql 语句：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="5ecc4-141">为将访问数据库的 SQL Server 登录名创建数据库用户。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="5ecc4-142">将数据库用户添加到任何所需的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="5ecc4-143">该文件应如下所示：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="5ecc4-144">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="5ecc4-145">在目标数据库中执行脚本</span><span class="sxs-lookup"><span data-stu-id="5ecc4-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="5ecc4-146">理想情况下，在部署数据库项目时，您将运行任何所需的 Transact-sql 脚本作为后期部署脚本的一部分。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="5ecc4-147">但是，后期部署脚本不允许你根据解决方案配置或生成属性执行条件逻辑。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="5ecc4-148">替代方法是通过创建执行 sqlcmd 命令的**目标**元素，直接从 MSBuild 项目文件运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="5ecc4-149">可以使用此命令在目标数据库上运行脚本：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-149">You can use this command to run your script on the target database:</span></span>

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> <span data-ttu-id="5ecc4-150">有关 sqlcmd 命令行选项的详细信息，请参阅[Sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

<span data-ttu-id="5ecc4-151">在 MSBuild 目标中嵌入此命令之前，需要考虑要在什么条件下运行该脚本：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="5ecc4-152">目标数据库必须存在，然后才能更改其角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="5ecc4-153">因此，需要在数据库部署*后*运行此脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="5ecc4-154">您需要包含一个条件，以便只对测试环境执行该脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="5ecc4-155">如果你正在运行 "假设" 部署&#x2014;，如果你正在生成部署脚本，但并未实际运行，&#x2014;则不应运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="5ecc4-156">如果使用 "[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)" 中所述的拆分项目文件方法（如联系人管理器示例解决方案所示），则可以按如下所示拆分 SQL 脚本的生成说明：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="5ecc4-157">任何所需的特定于环境的属性（以及确定是否部署权限的属性）都应位于特定于环境的项目文件中（例如，环境*中的项目文件）。*</span><span class="sxs-lookup"><span data-stu-id="5ecc4-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="5ecc4-158">MSBuild 目标本身以及任何在目标环境之间不会发生更改的属性都应转到通用项目文件中（例如， *Publish*）。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="5ecc4-159">在特定于环境的项目文件中，需要定义数据库服务器名称、目标数据库名称，以及一个布尔属性，该属性允许用户指定是否部署角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

<span data-ttu-id="5ecc4-160">在通用项目文件中，需要提供 sqlcmd 可执行文件的位置以及要运行的 SQL 脚本的位置。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="5ecc4-161">无论目标环境如何，这些属性都将保持不变。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="5ecc4-162">还需要创建 MSBuild 目标以执行 sqlcmd 命令。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

<span data-ttu-id="5ecc4-163">请注意，可以将 sqlcmd 可执行文件的位置添加为静态属性，因为这可能对其他目标有用。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="5ecc4-164">与此相反，您将 SQL 脚本的位置定义为目标中的动态属性的 sqlcmd 命令的语法，因为在执行目标之前不需要它们。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="5ecc4-165">在这种情况下，仅当满足以下条件时才会执行**DeployTestDBPermissions**目标：</span><span class="sxs-lookup"><span data-stu-id="5ecc4-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="5ecc4-166">**DeployTestDBRoleMemberships**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="5ecc4-167">用户未指定**WhatIf = true**标志。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="5ecc4-168">最后，请不要忘记调用目标。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="5ecc4-169">在*Publish*文件中，可以通过将目标添加到默认**FullPublish**目标的依赖项列表来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="5ecc4-170">需要确保在执行**PublishDbPackages**目标之前不会执行**DeployTestDBPermissions**目标。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a><span data-ttu-id="5ecc4-171">结束语</span><span class="sxs-lookup"><span data-stu-id="5ecc4-171">Conclusion</span></span>

<span data-ttu-id="5ecc4-172">本主题介绍了一种方法，在此方法中，你可以在部署数据库项目时将数据库用户和角色成员身份添加为部署后操作。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="5ecc4-173">在测试环境中定期重新创建数据库时，这通常很有用，但在将数据库部署到过渡环境或生产环境时，通常应避免使用此方法。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="5ecc4-174">因此，应确保使用必要的条件逻辑，以便仅在适当的时候创建数据库用户和角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="5ecc4-175">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="5ecc4-175">Further Reading</span></span>

<span data-ttu-id="5ecc4-176">有关使用 VSDBCMD 部署数据库项目的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="5ecc4-177">有关为不同目标环境自定义数据库部署的指南，请参阅[自定义多个环境的数据库部署](customizing-database-deployments-for-multiple-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="5ecc4-178">有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="5ecc4-179">有关 sqlcmd 命令行选项的详细信息，请参阅[Sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5ecc4-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5ecc4-180">[上一页](customizing-database-deployments-for-multiple-environments.md)
> [下一页](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="5ecc4-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>
