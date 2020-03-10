---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 配置用于 Web 部署的服务器环境 |Microsoft Docs
author: jrjlee
description: 本教程将演示如何设置服务器环境，以便在各种不同的 scenario 中支持一键式或自动化的网站部署和发布 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515114"
---
# <a name="configuring-server-environments-for-web-deployment"></a>配置用于 Web 部署的服务器环境

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程将演示如何设置服务器环境，以支持在各种不同方案中进行一键式或自动化的网站部署和发布。 本教程介绍了如何完成各种任务，如将 web 服务器配置为支持特定的部署方法和设置 Web 场框架（WFF）服务器场，以及提供更高级的端到端指南。
> 
> 本教程使用[企业 Web 部署：方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中所述的 Fabrikam，inc. 部署方案作为示例和网络基础结构的参考点。
> 
> 有关这些教程的意大利语翻译，请访问[http://www.lucamorelli.it](http://www.lucamorelli.it)。

本教程包括以下主题：

- [选择 Web 部署的适当方法](choosing-the-right-approach-to-web-deployment.md)
- [方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)
- [方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)
- [配置用于 Web 部署发布的 Web 服务器（远程代理）](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [配置用于 Web 部署发布的 Web 服务器（离线部署）](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [配置用于 Web 部署发布的数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)
- [使用 Web Farm Framework 创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)
- [配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)

第一个主题是[选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)，其中介绍了可用于通过使用 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web 部署）2.0 发布 Web 应用程序的主要方法。 它还标识映射到每个方法的方案。 在此，每个方案主题都提供了完成所需任务的高级概述，并标识了帮助你完成这些任务所需的主题。

如果你使用[了解构建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)和部署解决方案的生成过程中所述的拆分项目文件方法，则最后一个主题是为[目标环境配置部署属性](configuring-deployment-properties-for-a-target-environment.md)，描述如何配置特定于环境的项目文件以部署到不同的目标环境。

## <a name="key-technologies"></a>关键技术

本教程重点介绍如何使用这些产品和技术来支持 web 部署：

- IIS 7.5
- Web 部署2。x
- WFF 2.x
- IIS Web 管理服务（WMSvc）

本教程还介绍了如何使用 Windows Server 2008 R2、SQL Server 2008 R2、ASP.NET 4.0 和 ASP.NET MVC 3。

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这构成了一系列有关企业级 web 部署的五个教程的组成部分。 这些是系列中的其他教程：

- [在企业方案中部署 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容为教程系列提供了上下文背景。 它介绍了教程方案，并说明了整个系列中描述的任务和演练如何适应更广泛的应用程序生命周期管理（ALM）过程。
- [企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程介绍 Microsoft 生成引擎（MSBuild）项目文件、Web 发布管道、Web 部署和其他相关技术。 它说明了如何使用这些工具来管理复杂的部署过程。
- [为 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 Team Foundation Server （TFS）以支持不同的部署方案，包括自动部署（作为持续集成（CI）过程的一部分）和手动触发的特定生成的部署。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种高级部署任务，如自定义多个环境的数据库部署、从部署中排除文件和文件夹，以及在部署过程中使 web 应用程序脱机.

> [!div class="step-by-step"]
> [下一部分](choosing-the-right-approach-to-web-deployment.md)
