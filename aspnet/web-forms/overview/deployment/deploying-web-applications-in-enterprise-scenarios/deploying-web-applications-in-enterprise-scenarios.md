---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: 使用 Visual Studio 2010 在企业方案中部署 Web 应用程序 |Microsoft Docs
author: jrjlee
description: 本教程集介绍了可用于在各种企业方案中部署 web 应用程序的工具和技术。 它介绍了如何充分利用 。
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: eb7b82d16079d4d086af1919d092fb28db60d8b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463430"
---
# <a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>使用 Visual Studio 2010 在企业方案中部署 Web 应用程序

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程集介绍了可用于在各种企业方案中部署 web 应用程序的工具和技术。 它介绍了如何充分利用 Visual Studio 2010、Microsoft 生成引擎（MSBuild）、Internet Information Services （IIS）7.5、IIS Web 部署工具（Web 部署）、Web 场框架（WFF）和实用工具（如 VSDBCMD）等技术简化和管理部署过程。 其中包括概念概述和面向任务的指南，这些指南可帮助你：
> 
> - 查看并建立企业规模的 web 应用程序的部署要求。
> - 配置测试、过渡和生产 web 服务器环境，以支持 web 部署。
> - 配置 Team Foundation Server （TFS）持续集成（CI）过程以支持自动 web 部署。
> - 将企业规模的 web 应用程序部署到不同的服务器环境，并具有不同的要求和限制。
> - 将更改部署到在不同服务器环境中运行的 web 应用程序。
> 
> > [!NOTE]
> > 尽管这些教程介绍了如何使用 TFS 作为 CI 服务器，但该指南可以轻松地适应任何 CI 服务器。 你不需要了解有关 TFS 的详细知识即可了解和利用这些教程。
> 
> 
> 有关这些教程的意大利语翻译，请访问[http://www.lucamorelli.it](http://www.lucamorelli.it)。

## <a name="about-the-authors"></a>关于作者

Jason 先生成了一项技术专家，其中包含一些[内容主控形状](http://www.contentmaster.com/)，在这种情况下，他一直在使用 Microsoft 产品和技术，尤其是 SharePoint 和 ASP.NET。 Jason 在计算中持有 PhD，目前已 MCPD 和 MCTS 认证。 可在[www.jrjlee.com](http://www.jrjlee.com/)阅读 Jason 的技术博客。

Benjamin 咖喱是一位主要技术专家，其中包含[内容主控](http://www.contentmaster.com/)人，她在职业生涯中编写了白皮书、SDK 文档、PowerPoint 演示文稿以及讲师指导和在线培训课程。 ASP.NET 文档团队的原始成员，他在十年内使用过 Microsoft 的 web 技术。

## <a name="target-audience"></a>目标读者

这组教程适用于使用 Visual Studio 2010 创建企业级 web 应用程序的 ASP.NET web 应用程序开发人员和解决方案架构师。 若要充分利用内容，你应该使用 Visual Studio 2010 并大致熟悉 TFS，同时了解 Microsoft web 平台技术（如 ASP.NET MVC 3、Windows Communication Foundation （WCF）、IIS、SQL）服务器和 Visual Studio 数据库项目。 但是，你不需要熟悉部署工具和技术，或者需要了解如何设置 CI 系统。

## <a name="requirements"></a>要求

若要执行这些演练并执行这些教程中所述的任务，您需要在开发计算机上安装此软件：

- Visual Studio 2010 Premium 或旗舰版 Service Pack 1
- .NET Framework 4.0
- .NET Framework 3.5 Service Pack 1
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

若要执行这些演练中描述的部署步骤，你需要有权访问示例 Web 应用程序部署环境。 为了获得最佳效果，这些环境应反映组织的企业部署模式。 然后，你可以修改本文档中提供的演练，以反映你自己组织的部署环境和要求。

## <a name="series-contents"></a>序列内容

本介绍部分包括另外两个主题。 这些设计旨在为以下教程提供一些更广泛的上下文：

- [企业 Web 部署：方案概述](enterprise-web-deployment-scenario-overview.md)。 本主题介绍支持本系列中的每个教程的方案。 此方案重点介绍名为 Fabrikam，Inc. 的虚构公司的应用程序生命周期管理（ALM）要求，因为它开发了企业规模的 web 应用程序。
- [应用程序生命周期管理：从开发到生产](application-lifecycle-management-from-development-to-production.md)。 本主题提供部署过程的高级、端到端概述。 它说明了 Fabrikam，Inc. 如何通过测试、过渡和生产环境移动企业规模的 ASP.NET web 应用程序，作为持续开发过程的一部分。

本系列包含四个教程集。 每个侧重点都侧重于 web 部署的不同方面：

- [企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程介绍了 MSBuild 项目文件、Web 发布管道、Web 部署和其他相关技术。 它说明了如何使用这些工具来管理复杂的部署过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows server 以支持各种部署方案，包括使用 Web 部署代理服务（"远程代理"）或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 它提供有关为您自己的环境选择适当的部署方法的指导，并说明如何使用 WFF 在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [为 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 TFS 以支持各种部署方案，包括作为 CI 过程的一部分自动部署和手动触发特定生成的部署。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种高级部署任务，如自定义多个环境的数据库部署、从部署中排除文件和文件夹，以及在部署过程中使 web 应用程序脱机.

## <a name="where-to-start"></a>开始位置

这一组教程使用一个示例解决方案，其中包含实际的复杂性级别，同时提供一种虚构的企业部署方案，以提供参考实现并为任务和演练提供一个常见上下文。 下一主题 "[企业 Web 部署：方案概述](enterprise-web-deployment-scenario-overview.md)" 介绍了方案和示例解决方案。 在这里，你可以完成最符合你需求的教程和主题。

> [!div class="step-by-step"]
> [下一部分](enterprise-web-deployment-scenario-overview.md)
