---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 为 Web 部署配置 Team Foundation Server |Microsoft Docs
author: jrjlee
description: 本教程将演示如何配置 Team Foundation Server （TFS）2010来构建解决方案并将 web 内容部署到各种目标环境。 此 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 638d696abbc5f05957c0ed2eb7ebb65fce7813ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424202"
---
# <a name="configuring-team-foundation-server-for-web-deployment"></a>配置用于 Web 部署的 Team Foundation Server

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程将演示如何配置 Team Foundation Server （TFS）2010来构建解决方案并将 web 内容部署到各种目标环境。 这包括持续集成（CI）方案，在此方案中，每次开发人员进行更改时都会自动部署内容。 它还可以包括手动触发器方案，在测试环境中验证并验证生成后，管理员可能需要触发特定生成到过渡环境的部署。 本教程中的主题将指导你完成整个配置过程，其中包括：
> 
> - 如何在 TFS 中创建新的团队项目。
> - 如何将内容添加到源代码管理。
> - 如何配置生成服务器以支持 CI 和部署。
> - 如何创建包含部署逻辑的生成定义。
> - 如何配置自动部署的权限。
> 
> 有关这些教程的意大利语翻译，请访问[http://www.lucamorelli.it](http://www.lucamorelli.it)。

本教程假定你已安装 TFS 2010，并在初始配置过程中创建了一个团队项目集合。 [Visual Studio 2010 的 Team Foundation 安装指南](https://go.microsoft.com/?linkid=9805132)提供了有关这些任务的全面指导。

## <a name="context"></a>上下文

这构成了一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案来表示具有真实复杂性级别的 WEB 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="scenario-overview"></a>方案概述

[企业 Web 部署：方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中介绍了这些教程的高级方案。 建议你在开始学习本教程之前查看此主题。

## <a name="how-to-use-this-tutorial"></a>如何使用本教程

如果这是你第一次执行本教程中所述的任务，或如果你想要按照示例解决方案使用示例，则应按顺序浏览教程主题。 或者，您可以使用各个主题作为特定任务的指南。 本教程包括以下主题：

- [在 TFS 中创建团队项目](creating-a-team-project-in-tfs.md)。 "团队项目" 是用于在 TFS 中进行源代码管理和生成的核心单元。 你需要先创建一个团队项目，然后才能向源代码管理添加内容或创建生成定义。
- [向源代码管理添加内容](adding-content-to-source-control.md)。 创建团队项目后，可以开始将内容添加到源代码管理。 你需要添加你的项目和解决方案以及任何外部依赖关系，然后才能开始配置生成。
- [配置用于 Web 部署的 TFS 生成服务器](configuring-a-tfs-build-server-for-web-deployment.md)。 如果要生成团队项目内容，则需要配置生成服务器。 在大多数情况下，这应该与 TFS 安装在单独的计算机上。 若要配置生成服务器，需要安装和配置 TFS 生成服务，安装 Visual Studio 2010，创建生成控制器和生成代理，安装代码需要的任何产品或组件以成功生成，然后安装Internet Information Services （IIS） Web 部署工具（Web 部署）。
- [创建支持部署的生成定义](creating-a-build-definition-that-supports-deployment.md)。 你需要为你的团队项目至少创建一个生成定义，然后才能在 TFS 中开始排队或触发生成。 生成定义定义生成的每个方面，包括应包括在生成中的内容、应触发生成的内容以及团队生成应发送生成输出的位置。 你可以配置生成定义以运行自定义 Microsoft 生成引擎（MSBuild）项目文件，这使你能够在自动生成中包括部署逻辑。
- [部署特定生成](deploying-a-specific-build.md)。 在许多情况下，你需要将特定版本而不是最新版本部署到目标环境。 在这种情况下，您可以配置从特定放置文件夹部署内容的生成定义。
- [配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)。 如果生成服务要将内容部署为自动生成过程的一部分，则需要在任何目标 web 服务器和数据库服务器上向生成服务帐户授予各种权限。

## <a name="key-technologies"></a>关键技术

本教程重点介绍如何使用这些产品和技术来支持自动生成和 web 部署：

- Visual Studio Team Foundation Server 2010
- Team Build 和 MSBuild
- Web Deploy

本教程还介绍了如何使用 Windows Server 2008 R2、IIS 7.5、SQL Server 2008 R2、ASP.NET 4.0 和 ASP.NET MVC 3。

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这构成了一系列有关企业级 web 部署的五个教程的组成部分。 这些是系列中的其他教程：

- [在企业方案中部署 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容为教程系列提供了上下文背景。 它介绍了教程方案，并说明了整个系列中描述的任务和演练如何适应更广泛的应用程序生命周期管理（ALM）过程。
- [企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程介绍了 MSBuild 项目文件、Web 发布管道（WPP）、Web 部署和其他相关技术。 它说明了如何使用这些工具来管理复杂的部署过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows server 以支持各种部署方案，包括使用 Web 部署代理服务（远程代理）或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 本指南提供了有关为自己的环境选择适当的部署方法的指导，并介绍了如何使用 Web 场框架（WFF）在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种高级部署任务，如自定义多个环境的数据库部署、从部署中排除文件和文件夹，以及在部署过程中使 web 应用程序脱机.

> [!div class="step-by-step"]
> [下一部分](creating-a-team-project-in-tfs.md)
