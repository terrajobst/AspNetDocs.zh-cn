---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 方案：配置用于 Web 部署的过渡环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍了过渡环境的典型 web 部署方案，并说明了设置类似环境所需完成的任务 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518006"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>方案：配置用于 Web 部署的过渡环境

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍了过渡环境的典型 web 部署方案，并说明了设置类似环境需要完成的任务。

许多组织使用过渡环境预览 web 应用程序或网站的更新。 这样，组织中的人员就有机会在站点 "上线" 之前浏览和查看新功能或内容，或者将其部署到生产环境。 过渡环境旨在尽可能密切地复制生产环境，以便提供逼真的预览。 这种类型的过渡环境通常具有以下特征：

- 环境包含多个负载均衡的 web 服务器和一个或多个数据库服务器，通常具有故障转移群集和数据库镜像。
- 应用程序可以由开发团队手动部署，也可以由团队生成服务器自动部署。
- 部署应用程序的用户或进程帐户不太可能在临时服务器上具有管理员权限。
- 对应用程序的更改是频繁部署的，因此环境需要支持单步或自动部署。

> [!NOTE]
> 在多个服务器上横向扩展数据库部署超出了本教程的范围。 有关此方面的详细信息，请参阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。

例如，在我们的 "[教程" 方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，TEAM FOUNDATION SERVER （TFS）管理 "联系人管理器" 解决方案。 TFS 管理员 "Walters" 已创建生成定义，使开发人员可以根据需要触发到过渡环境的部署。

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

请注意，在大多数情况下，不需要将最新版本部署到过渡环境。 相反，您很可能希望部署在测试环境中已经完成验证和验证的特定生成。

## <a name="solution-overview"></a>解决方案概述

在这种情况下，你可以通过分析部署要求来推导这些事实：

- 执行部署的用户或进程帐户在过渡服务器上不具有管理员权限，因此过渡 web 服务器必须支持非管理员部署。 因此，你需要将过渡 web 服务器配置为使用 Web 部署处理程序而不是远程代理。
- 过渡环境包含多个 web 服务器，但它需要支持一键式或自动部署，因此你需要使用 Web 场框架（WFF）来创建服务器场。 使用此方法，你可以将应用程序部署到一台 web 服务器（主服务器），WFF 将在过渡环境中的所有其他 web 服务器上复制部署。
- 执行部署的用户或进程帐户必须具有创建数据库的权限。 因此，除了配置数据库服务器以支持远程访问和部署之外，还需要将帐户添加到数据库服务器上的**dbcreator**服务器角色。

以下主题提供完成这些任务所需的所有信息：

- [使用 Web 场框架创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)。 本主题介绍如何使用 WFF 创建和配置服务器场，以便跨多个负载均衡的 web 服务器复制 web 平台产品和组件、配置设置以及网站和应用程序。
- [为 Web 部署发布（Web 部署处理程序）配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 本主题介绍如何使用远程代理方法构建支持 Web 部署发布的 web 服务器，从干净的 Windows Server 2008 R2 版本开始。
- [为 Web 部署发布配置数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何配置数据库服务器以支持远程访问和部署，从默认安装 SQL Server 2008 R2 开始。

## <a name="further-reading"></a>其他阅读材料

有关配置典型开发人员测试环境的指导，请参阅[方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。 有关配置典型生产环境的指南，请参阅[方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一页](scenario-configuring-a-production-environment-for-web-deployment.md)
