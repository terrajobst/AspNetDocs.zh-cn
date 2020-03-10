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
# <a name="deploying-database-role-memberships-to-test-environments"></a>将数据库角色成员身份部署到测试环境

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何在将解决方案部署到测试环境时将用户帐户添加到数据库角色中。
> 
> 在将包含数据库项目的解决方案部署到过渡环境或生产环境时，通常不希望开发人员自动将用户帐户添加到数据库角色。 在大多数情况下，开发人员不知道哪些用户帐户需要添加到哪些数据库角色中，这些要求随时可能会更改。 但是，在将包含数据库项目的解决方案部署到开发或测试环境时，这种情况通常是不同的：
> 
> - 开发人员通常会定期重新部署解决方案，这种情况通常是一天。
> - 通常，在每次部署时都会重新创建数据库，这意味着在每次部署后，必须创建数据库用户并将其添加到角色。
> - 开发人员通常对目标开发或测试环境具有完全控制。
> 
> 在这种情况下，在部署过程中自动创建数据库用户并分配数据库角色成员身份通常是有益的。
> 
> 关键因素在于，此操作需要根据目标环境进行条件。 如果要部署到过渡环境或生产环境，则需要跳过该操作。 如果要部署到开发人员或测试环境，则需要部署角色成员身份，而无需进一步干预。 本主题介绍可用于解决此问题的一种方法。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

本主题假定：

- 按照[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述，使用拆分项目文件方法进行解决方案部署。
- 从项目文件调用 VSDBCMD 来部署数据库项目，如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述。

若要创建数据库用户并在将数据库项目部署到测试环境时分配角色成员身份，需要执行以下操作：

- 创建一个使所需的数据库发生更改的 Transact-sql 结构化查询语言（Transact-sql）脚本。
- 创建一个 Microsoft 生成引擎（MSBuild）目标，该目标使用 sqlcmd 实用程序来运行 SQL 脚本。
- 在将解决方案部署到测试环境时，将项目文件配置为调用目标。

本主题将演示如何执行上述每个过程。

## <a name="scripting-the-database-role-memberships"></a>为数据库角色成员身份编写脚本

您可以通过许多不同的方式，在您选择的任何位置创建 Transact-sql 脚本。 最简单的方法是在 Visual Studio 2010 的解决方案中创建脚本。

**创建 SQL 脚本**

1. 在 "**解决方案资源管理器**" 窗口中，展开您的数据库项目节点。
2. 右键单击 "**脚本**" 文件夹，指向 "**添加**"，然后单击 "**新建文件夹**"。
3. 键入**Test**作为文件夹名称，然后按 enter。
4. 右键单击**测试**文件夹，指向 "**添加**"，然后单击 "**脚本**"。
5. 在 "**添加新项**" 对话框中，为脚本提供一个有意义的名称（例如， **AddRoleMemberships**），然后单击 "**添加**"。

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. 在*AddRoleMemberships*文件中，添加以下 transact-sql 语句：

    1. 为将访问数据库的 SQL Server 登录名创建数据库用户。
    2. 将数据库用户添加到任何所需的数据库角色。
7. 该文件应如下所示：

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. 保存该文件。

## <a name="executing-the-script-on-the-target-database"></a>在目标数据库中执行脚本

理想情况下，在部署数据库项目时，您将运行任何所需的 Transact-sql 脚本作为后期部署脚本的一部分。 但是，后期部署脚本不允许你根据解决方案配置或生成属性执行条件逻辑。 替代方法是通过创建执行 sqlcmd 命令的**目标**元素，直接从 MSBuild 项目文件运行 SQL 脚本。 可以使用此命令在目标数据库上运行脚本：

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> 有关 sqlcmd 命令行选项的详细信息，请参阅[Sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。

在 MSBuild 目标中嵌入此命令之前，需要考虑要在什么条件下运行该脚本：

- 目标数据库必须存在，然后才能更改其角色成员身份。 因此，需要在数据库部署*后*运行此脚本。
- 您需要包含一个条件，以便只对测试环境执行该脚本。
- 如果你正在运行 "假设" 部署&#x2014;，如果你正在生成部署脚本，但并未实际运行，&#x2014;则不应运行 SQL 脚本。

如果使用 "[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)" 中所述的拆分项目文件方法（如联系人管理器示例解决方案所示），则可以按如下所示拆分 SQL 脚本的生成说明：

- 任何所需的特定于环境的属性（以及确定是否部署权限的属性）都应位于特定于环境的项目文件中（例如，环境*中的项目文件）。*
- MSBuild 目标本身以及任何在目标环境之间不会发生更改的属性都应转到通用项目文件中（例如， *Publish*）。

在特定于环境的项目文件中，需要定义数据库服务器名称、目标数据库名称，以及一个布尔属性，该属性允许用户指定是否部署角色成员身份。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

在通用项目文件中，需要提供 sqlcmd 可执行文件的位置以及要运行的 SQL 脚本的位置。 无论目标环境如何，这些属性都将保持不变。 还需要创建 MSBuild 目标以执行 sqlcmd 命令。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

请注意，可以将 sqlcmd 可执行文件的位置添加为静态属性，因为这可能对其他目标有用。 与此相反，您将 SQL 脚本的位置定义为目标中的动态属性的 sqlcmd 命令的语法，因为在执行目标之前不需要它们。 在这种情况下，仅当满足以下条件时才会执行**DeployTestDBPermissions**目标：

- **DeployTestDBRoleMemberships**属性设置为**true**。
- 用户未指定**WhatIf = true**标志。

最后，请不要忘记调用目标。 在*Publish*文件中，可以通过将目标添加到默认**FullPublish**目标的依赖项列表来执行此操作。 需要确保在执行**PublishDbPackages**目标之前不会执行**DeployTestDBPermissions**目标。

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a>结束语

本主题介绍了一种方法，在此方法中，你可以在部署数据库项目时将数据库用户和角色成员身份添加为部署后操作。 在测试环境中定期重新创建数据库时，这通常很有用，但在将数据库部署到过渡环境或生产环境时，通常应避免使用此方法。 因此，应确保使用必要的条件逻辑，以便仅在适当的时候创建数据库用户和角色成员身份。

## <a name="further-reading"></a>其他阅读材料

有关使用 VSDBCMD 部署数据库项目的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 有关为不同目标环境自定义数据库部署的指南，请参阅[自定义多个环境的数据库部署](customizing-database-deployments-for-multiple-environments.md)。 有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。 有关 sqlcmd 命令行选项的详细信息，请参阅[Sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。

> [!div class="step-by-step"]
> [上一页](customizing-database-deployments-for-multiple-environments.md)
> [下一页](deploying-membership-databases-to-enterprise-environments.md)
