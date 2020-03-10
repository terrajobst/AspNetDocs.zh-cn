---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 解决方案 |Microsoft Docs
author: jrjlee
description: 这一系列教程使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;联系人管理器解决方案来表示企业规模的应用程序，该应用程序具有真实的上面 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473810"
---
# <a name="the-contact-manager-solution"></a>Contact Manager 解决方案

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 这一[系列教程](web-deployment-in-the-enterprise.md)使用一个示例解决方案&#x2014;，其中使用了&#x2014;联系人管理器解决方案来表示企业规模的应用程序，该应用程序具有真实的复杂性级别。 本主题介绍联系人管理器解决方案，介绍解决方案的关键组件，并确定在企业环境中将此类应用程序部署到各种目标平台时面临的挑战。
> 
> 当你完成这些教程中的各个主题时，你可以使用 Contact Manager 解决方案作为参考实现，演示如何在企业部署方案中满足特定挑战。 下一主题 "[设置联系人管理器" 解决方案](setting-up-the-contact-manager-solution.md)介绍了如何在开发人员工作站上下载和运行解决方案。

## <a name="solution-overview"></a>解决方案概述

Contact Manager 解决方案由四个单独的项目组成：

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager**。 这是一个 ASP.NET MVC 3 web 应用程序项目，它表示解决方案的入口点。 它提供了一些基本 web 应用程序功能，例如，为用户提供创建和查看联系人详细信息的能力。 应用程序依赖于 Windows Communication Foundation （WCF）服务来管理联系人，并使用 ASP.NET 应用程序服务数据库来管理身份验证和授权。
- **ContactManager**。 这是一个 Visual Studio 数据库项目。 项目定义用于存储联系人详细信息的数据库的架构。
- **ContactManager**。 这是一个 WCF web services 项目。 WCF 服务公开一个终结点，该终结点允许调用方对**ContactManager**数据库执行创建、检索、更新和删除（CRUD）操作。 该服务依赖于**ContactManager**数据库和**ContactManager**程序集。
- **ContactManager**。 这是一个类库项目。 WCF 服务依赖于此程序集中定义的类型。

此解决方案还包括一个名为 Publish 的解决方案文件夹。 其中包含各种自定义项目文件和命令文件，它们演示了如何控制和操作生成和部署过程。 本教程稍后将对这些内容进行更详细的介绍。

在概念级别上，解决方案的组件组合在一起，如下所示：

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> 尽管 ASP.NET MVC 3 web 应用程序使用 ASP.NET 成员资格提供程序，但 web 应用程序中的所有页面都允许匿名访问。 这显然不是真实的配置。 不过，解决方案是以这种方式设置的，使你可以更轻松地部署和测试解决方案，而无需配置用户帐户和角色。

## <a name="deployment-challenges"></a>部署难题

"联系人管理器" 解决方案阐明了许多企业部署方案中常见的一些部署难题：

- 解决方案包含多个依赖项目。 你需要同时部署这些项目。
- 需要为每个环境更新连接字符串和服务终结点，在很多情况下，这些信息将不能供开发人员使用。
- 将**ContactManager**数据库部署到过渡环境和生产环境时，需要在后续部署中保留现有数据。
- 部署 ASP.NET 应用程序服务数据库时，需要部署某些配置数据，但要省略任何用户帐户数据。
- 这些项目包括一些不应部署的文件和文件夹。 需要从部署过程中排除这些文件和文件夹。
- 解决方案需要支持从 Team Foundation Server （TFS）生成服务器自动部署。

## <a name="conclusion"></a>结束语

本主题提供了联系人管理器解决方案的高级概述，并确定了许多企业部署方案中常见的一些固有的部署挑战。 本教程中的其余主题介绍了可用于解决这些难题的一些方法。

下一主题 "[设置联系人管理器" 解决方案](setting-up-the-contact-manager-solution.md)介绍了如何在开发人员工作站上下载和运行解决方案。

> [!div class="step-by-step"]
> [上一页](web-deployment-in-the-enterprise.md)
> [下一页](setting-up-the-contact-manager-solution.md)
