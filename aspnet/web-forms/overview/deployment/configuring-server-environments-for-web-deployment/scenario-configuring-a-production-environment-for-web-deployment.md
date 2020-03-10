---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 方案：配置用于 Web 部署的生产环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍了生产环境的典型 web 部署方案，并介绍了需要完成哪些任务才能设置类似 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515930"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a>方案：配置用于 Web 部署的生产环境

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍了生产环境的典型 web 部署方案，并说明了设置类似环境需要完成的任务。

生产环境是 web 应用程序或网站的最终目标。 至此，你的应用程序已通过测试，已部署到过渡环境，并已准备好 "上线"。 根据你的 web 内容的性质和用途、你的组织的规模、你的目标受众以及许多其他因素，生产环境的特征可能会有很大的差异。 在企业规模的方案中，生产环境可能具有以下特征：

- 环境包含多个负载均衡的 web 服务器和一个或多个数据库服务器，通常具有故障转移群集和数据库镜像。
- 如果环境面向 Internet，则很可能与内部网络隔离。 它可能位于外围网络中的不同子网中，它可能位于不同的域中，并且可能位于完全不同的网络基础结构上。
- 开发人员和生成服务器进程帐户在生产服务器上不太可能拥有管理员权限。
- 对应用程序所做的更改的部署频率低于测试或过渡部署。

> [!NOTE]
> 在多个服务器上横向扩展数据库部署超出了本教程的范围。 有关此方面的详细信息，请参阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。

例如，在我们的[教程方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，团队生成服务器包含生成定义，使用户能够生成 Contact Manager 解决方案并在单个步骤中将其部署到过渡环境。 当应用程序准备好部署到生产环境时，由于安全要求和网络基础结构施加的约束，生产环境管理员必须手动将 web 包复制到生产 web 服务器上并导入通过 Internet Information Services （IIS）管理器。

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>解决方案概述

在这种情况下，你可以通过分析部署要求来推导这些事实：

- 由于安全限制和网络配置，无法将生产环境配置为支持一键式或自动部署。 脱机部署是此方案中唯一可行的方法。
- 生产环境包含多个 web 服务器，因此你可以使用 Web 场框架（WFF）来创建服务器场。 使用此方法，管理员只需将该应用程序导入到一台 web 服务器（主服务器）上，WFF 将在生产环境中的所有其他 web 服务器上复制部署。

以下主题提供完成这些任务所需的所有信息：

- [使用 Web 场框架创建服务器场](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何使用 WFF 创建和配置服务器场，以便跨多个负载均衡的 web 服务器复制 web 平台产品和组件、配置设置以及网站和应用程序。
- [为 Web 部署发布（脱机部署）配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 本主题介绍如何构建 web 服务器，使管理员能够从干净的 Windows Server 2008 R2 版本开始，手动导入和部署 web 包。
- [为 Web 部署发布配置数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何配置数据库服务器以支持远程访问和部署，从默认安装 SQL Server 2008 R2 开始。

## <a name="further-reading"></a>其他阅读材料

有关配置典型开发人员测试环境的指导，请参阅[方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。 有关配置典型过渡环境的指导，请参阅[方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
