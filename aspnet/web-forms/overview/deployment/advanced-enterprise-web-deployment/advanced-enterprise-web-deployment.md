---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: 高级企业 Web 部署 |Microsoft Docs
author: jrjlee
description: 本教程将向您演示如何在许多企业部署方案中执行所需的各种任务。 对于意大利语 translati 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bf4c7d021763017592483df35cb717295c4924aa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474956"
---
# <a name="advanced-enterprise-web-deployment"></a>高级企业 Web 部署

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程将向您演示如何在许多企业部署方案中执行所需的各种任务。
> 
> 有关这些教程的意大利语翻译，请访问[http://www.lucamorelli.it](http://www.lucamorelli.it)。

这构成了一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案来表示具有真实复杂性级别的 WEB 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="scenario-overview"></a>方案概述

[企业 Web 部署：方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中介绍了这些教程的高级方案。 建议你在开始学习本教程之前查看此主题。

## <a name="how-to-use-this-tutorial"></a>如何使用本教程

- 本教程中的每个主题都是独立的，它解决了企业部署方案中发生的特定挑战或问题。 不需要按任何特定顺序处理这些主题。 不过，本教程介绍了一些高级任务。 因此，您应熟悉[企业教程中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)所涉及的概念和技术，以便充分利用此内容。
- 本教程包括以下主题：
- [执行 "What If" 部署](performing-a-what-if-deployment.md)。 在许多情况下，你需要在实际进行任何更改之前，确定在目标环境或任何现有内容上建议的部署的影响。 本主题介绍如何运行 "假设" 部署来生成日志文件和数据库更新脚本，就好像已将内容部署到目标环境一样，无需进行任何更改。 分析这些资源可帮助你在实时部署之前发现任何潜在问题。
- [自定义多个环境的数据库部署](customizing-database-deployments-for-multiple-environments.md)。 将数据库项目部署到多个目标时，通常需要为每个目标环境自定义部署属性。 例如，在测试环境中，您通常会在每次部署时重新创建数据库，而在过渡环境或生产环境中，您更有可能进行增量更新以保留数据。 本主题介绍如何通过为每个目标环境创建环境特定的部署配置（sqldeployment）文件，将这些属性更改合并到部署逻辑中。
- 将数据库角色成员身份部署到测试环境。 当你在每次部署&#x2014;时重新创建数据库时（例如，作为持续集成（CI）生成并部署到测试环境&#x2014;的一部分），通常需要每次配置数据库角色成员身份。 例如，你通常需要向与你的 web 应用程序关联的应用程序池标识授予权限。 本主题介绍如何通过向部署逻辑添加后期部署 SQL 脚本来自动执行此过程。
- [将成员资格数据库部署到企业环境](deploying-membership-databases-to-enterprise-environments.md)。 ASP.NET 成员资格数据库具有各种特征，这会使部署过程复杂化。 例如，仅限架构的部署将使数据库处于不可操作状态。 在大多数情况下，最好直接在每个目标环境中创建成员资格数据库。 但是，如果您确实需要部署成员资格数据库，则本主题将介绍一些可用于满足固有挑战的方法。
- [从部署中排除文件和文件夹](excluding-files-and-folders-from-deployment.md)。 在某些情况下，你需要将 web 包的内容定制为特定的目标环境。 例如，你可能想要在部署到测试环境时包括所有版本的 JavaScript 库，以支持客户端调试，但在部署到过渡环境或生产环境时，请使用缩小版本的库。 本主题介绍如何在包创建过程中排除特定的文件和文件夹。
- 使[Web 应用程序脱机，并 Web 部署](taking-web-applications-offline-with-web-deploy.md)。 将解决方案部署到过渡环境或生产环境时，通常需要在部署过程中使 web 应用程序处于脱机状态。 本主题介绍如何在部署过程开始时将*应用\_脱机 .htm*文件添加到 web 应用程序，并将其删除。 当*应用\_脱机 .htm*文件时，浏览 web 应用程序的任何用户将自动重定向到*应用\_脱机 .htm*文件。
- [从 MSBuild 运行 Windows PowerShell 脚本](running-windows-powershell-scripts-from-msbuild-project-files.md)。 许多部署方案需要更复杂的部署后操作，例如将自定义事件源添加到注册表或在 SQL Server 实例之间配置复制。 通常通过 Windows PowerShell 脚本来完成这些操作。 本主题介绍如何在生成和部署过程中从 Microsoft 生成引擎（MSBuild）项目文件中运行 Windows PowerShell 脚本。
- [排查打包过程问题](troubleshooting-the-packaging-process.md)。 Web 发布管道（WPP）定义了一个名为**EnablePackageProcessLoggingAndAssert**的 MSBuild 属性，可用于生成有关 Web 应用程序项目打包过程的详细信息。 本主题介绍属性的作用以及如何使用它。

## <a name="key-technologies"></a>关键技术

本教程重点介绍如何使用这些产品和技术来支持自动生成和 web 部署：

- Visual Studio 2010 和 Team Foundation Server （TFS）2010
- MSBuild 和 TFS Team Build
- Internet Information Services （IIS）7。5
- IIS Web 部署工具（Web 部署）2。1
- VSDBCMD 数据库部署实用工具

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这构成了一系列有关企业级 web 部署的五个教程的组成部分。 这些是系列中的其他教程：

- [在企业方案中部署 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容为教程系列提供了上下文背景。 它介绍了教程方案，并说明了整个系列中描述的任务和演练如何适应更广泛的应用程序生命周期管理（ALM）过程。
- [企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程介绍了 MSBuild 项目文件、WPP、Web 部署和其他相关技术。 它说明了如何使用这些工具来管理复杂的部署过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows server 以支持各种部署方案，包括使用 Web 部署代理服务（远程代理）或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 本指南提供了有关为自己的环境选择适当的部署方法的指导，并介绍了如何使用 Web 场框架（WFF）在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [为 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 TFS 以支持各种部署方案，包括作为 CI 过程的一部分自动部署和手动触发特定生成的部署。

> [!div class="step-by-step"]
> [下一部分](performing-a-what-if-deployment.md)
