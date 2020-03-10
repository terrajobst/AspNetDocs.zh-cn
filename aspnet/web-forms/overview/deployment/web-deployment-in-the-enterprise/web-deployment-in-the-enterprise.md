---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: 企业中的 Web 部署 |Microsoft Docs
author: jrjlee
description: 本教程介绍如何在管理企业级 web 应用程序到 unixodbc-devel 的部署时遇到大量挑战
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: bc7bb676a71af4ec3451aa3adf3c03ce3b5200d5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509714"
---
# <a name="web-deployment-in-the-enterprise"></a>企业中的 Web 部署

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程介绍了在管理企业级 web 应用程序到开发、测试、过渡和生产环境的部署时，如何应对你会遇到的许多挑战。 本教程包含一个参考解决方案，其中混合了概念和面向任务的内容，指导你完成各种常见任务和过程。
> 
> 有关这些教程的意大利语翻译，请访问[http://www.lucamorelli.it](http://www.lucamorelli.it)。

## <a name="enterprise-deployment-challenges"></a>企业部署难题

当组织希望管理复杂的企业级解决方案的部署时，通常会遇到这些难题：

- 你需要能够将项目部署到多个环境，如开发人员或测试环境、过渡平台和生产服务器。 需要为每个环境部署解决方案的不同配置设置。
- 需要在单步或自动生成和部署过程中同时部署多个依赖项目。
- 你需要能够从自动过程中驱动部署。 例如，你想要使用持续集成（CI）过程在签入新代码时将 web 应用程序部署到测试环境。
- 你需要能够控制部署过程，并从 Visual Studio 外部设置部署变量，因为开发人员不太可能具有适用于每个目标环境的正确配置设置或必要凭据。
- 你需要部署基于架构的数据库项目，并在后续部署中保留现有数据。
- 你需要临时部署成员资格数据库，而无需部署用户帐户数据。 你可能还需要更新已部署成员资格数据库的架构，而不会丢失现有的用户帐户数据。
- 在将内容部署到各种目标环境时，需要排除某些文件或文件夹。

## <a name="overview-of-approach"></a>方法概述

本教程与本系列中的其他教程一起使用这一高级方法来满足上述挑战。

- **使用自定义 Microsoft 生成引擎（MSBuild）项目文件来控制整个生成和部署过程。**
- 这使您可以生成和部署解决方案中的每个项目，作为一个可脚本化的操作的一部分。
- 环境特定的设置是使用简单的特定于环境的项目文件配置的。 与通过 Visual Studio 以中心方式使用解决方案配置和发布配置文件来配置不同环境的部署相比，此方法可让你从 Visual Studio 外部配置和管理部署过程。 这意味着开发人员不需要事先了解连接字符串、服务终结点、服务器凭据以及目标环境的其他部署变量。
- Team Build 可以调用自定义项目文件作为 Team Foundation Server （TFS）工作流的一部分。 这使你可以为 CI 方案配置自动部署。

**使用 Internet Information Services （IIS） Web 部署工具（Web 部署）打包和部署 Web 应用程序项目。**

- Web 部署提供了一个框架，使你可以将 web 应用程序内容打包并部署到目标 IIS web 服务器，以及依赖项、配置设置、安全设置和其他任何要求。
- 你可以从自定义 MSBuild 项目文件中控制整个打包和部署过程。 你还可以处理 web 部署包附带的配置设置，例如连接字符串、服务终结点和 IIS 目标详细信息。
- Web 部署和 Web 发布管道一起提供了许多扩展点，可用于自定义部署。 例如，可以轻松地从 web 部署包中排除不需要的文件和文件夹。

**使用 VSDBCMD 实用程序部署和更新数据库架构。**

- 使用 VSDBCMD 可以从数据库架构文件（.dbschema）部署数据库，该文件是在生成 Visual Studio 数据库项目时生成的。 与此相反，Web 部署中包含的数据库部署功能更适合用于从本地 SQL Server 实例部署现有数据库。
- 与用于部署数据库项目的 Visual Studio 功能不同，VSDBCMD 允许你将差异更新部署到现有的目标数据库。 这允许您在升级数据库架构时保留所有现有数据。
- 你可以从自定义 MSBuild 项目文件中执行 VSDBCMD 命令。

## <a name="content-map"></a>内容映射

本教程包含四个主要方面的主题。

这些主题介绍了 Contact Manager&#x2014;解决方案&#x2014;的参考解决方案，并说明了如何在本地计算机上下载该解决方案并对其进行配置：

- [Contact Manager 解决方案](the-contact-manager-solution.md)
- [设置 Contact Manager 解决方案](setting-up-the-contact-manager-solution.md)

这些主题介绍了 MSBuild 项目文件，说明了如何创建和使用自定义项目文件，并演练了联系人管理器解决方案的部署过程：

- [了解项目文件](understanding-the-project-file.md)
- [了解生成过程](understanding-the-build-process.md)

这些主题介绍了 web 应用程序部署，包括生成和打包过程的工作原理，生成过程如何与 Web 发布管道集成，如何修改部署参数，以及如何将 web 包部署到目标情形

- [生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)
- [为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)
- [部署 Web 程序包](deploying-web-packages.md)

- [部署数据库项目](deploying-database-projects.md)介绍了可用于部署 Visual Studio 数据库项目的不同技术，以及每种方法的优点和缺点。 [创建和运行部署命令文件](creating-and-running-a-deployment-command-file.md)介绍如何创建一个简单的命令文件，用于封装部署逻辑，并使你能够将复杂的解决方案部署为单步过程。
- 最后，通过向 IIS 中导入 web 包的方式，[手动安装 Web 包](manually-installing-web-packages.md)结束本教程。

## <a name="key-technologies"></a>关键技术

本教程中的主题主要使用以下技术来管理生成和部署：

- Visual Studio 2010
- MSBuild
- IIS 7.5
- Web 部署 2.0
- VSDBCMD 数据库部署实用工具

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这构成了一系列有关企业级 web 部署的五个教程的组成部分。 这些是系列中的其他教程：

- [在企业方案中部署 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容为教程系列提供了上下文背景。 它介绍了教程方案，并说明了整个系列中描述的任务和演练如何适应更广泛的应用程序生命周期管理（ALM）过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows server 以支持各种部署方案，包括使用 Web 部署代理服务（远程代理）或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 本指南提供了有关为自己的环境选择适当的部署方法的指导，并介绍了如何使用 Web 场框架（WFF）在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [为 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 TFS 以支持各种部署方案，包括作为 CI 过程的一部分自动部署和手动触发特定生成的部署。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种高级部署任务，如自定义多个环境的数据库部署、从部署中排除文件和文件夹，以及在部署过程中使 web 应用程序脱机.

> [!div class="step-by-step"]
> [下一部分](the-contact-manager-solution.md)
