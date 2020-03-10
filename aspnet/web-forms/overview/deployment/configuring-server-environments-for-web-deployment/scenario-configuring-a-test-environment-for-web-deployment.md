---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 方案：配置用于 Web 部署的测试环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍了开发人员或测试环境的典型 web 部署方案，并说明了在设置 si 之前需要完成的任务。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517982"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a>方案：配置用于 Web 部署的测试环境

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍了开发人员或测试环境的典型 web 部署方案，并说明了设置类似环境需要完成的任务。

当开发人员在 web 应用程序上工作时，他们通常会获得对服务器环境的访问权限，这些服务器环境可用于测试应用程序对应用程序所做的更改。 此类开发或测试环境通常具有以下特征：

- 环境由单个 web 服务器和一个数据库服务器组成。
- 开发人员通常在服务器上具有管理员权限，让他们将环境配置为应用程序的要求。
- 对应用程序的更改是频繁部署的，因此环境需要支持单步或自动部署。

例如，在我们的 "[教程" 方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，Matt Hink 是 Fabrikam，inc. 的开发人员正在处理 Contact Manager 解决方案，并且定期需要将更改部署到测试环境。 Matt 是测试 web 服务器和测试数据库服务器上的管理员。 最初，Matt 需要能够直接将解决方案部署到测试环境。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

随着工作进度和更多开发人员加入团队，联系人管理器解决方案将配置为 Team Foundation Server （TFS）中的持续集成（CI）。 每当开发人员签入内容时，团队生成应生成解决方案，运行任何单元测试，并自动将解决方案部署到测试环境。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>解决方案概述

测试环境需要支持远程计算机的单步或自动部署，因此你可以选择两种主要方法。 你可以：

- 使用 Web 部署代理服务配置测试 web 服务器以支持部署（"远程代理"）。
- 使用 Web 部署处理程序配置测试 web 服务器以支持部署。

> [!NOTE]
> 你还可以按[需使用 Web 部署](https://technet.microsoft.com/library/ee517345(WS.10).aspx)（"temp agent"）。 这类似于要求和约束方面的远程代理方法。

在这种情况下，开发人员在目标服务器上具有管理员权限，而测试环境不受严格的安全约束的约束，因此，逻辑选择是将测试 web 服务器配置为支持使用远程代理进行的部署。 这不太复杂，要求的初始配置比 Web 部署处理程序方法更少。 还需要配置数据库服务器以支持远程访问和部署。

以下主题提供完成这些任务所需的所有信息：

- [为 Web 部署发布（远程代理）配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。 本主题介绍如何使用远程代理方法构建支持 Web 部署发布的 web 服务器，从干净的 Windows Server 2008 R2 版本开始。
- [为 Web 部署发布配置数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何配置数据库服务器以支持远程访问和部署，从默认安装 SQL Server 2008 R2 开始。

## <a name="further-reading"></a>其他阅读材料

有关配置典型过渡环境的指导，请参阅[方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。 有关配置典型生产环境的指南，请参阅[方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](choosing-the-right-approach-to-web-deployment.md)
> [下一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
