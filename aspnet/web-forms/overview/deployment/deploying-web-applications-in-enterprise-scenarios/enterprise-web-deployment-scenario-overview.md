---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: 企业 Web 部署：方案概述 |Microsoft Docs
author: jrjlee
description: 这一组教程使用一个示例解决方案，该解决方案具有真实的复杂性级别，同时提供一种虚构的企业部署方案，以提供参考 。
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: 9786879844da13c21e6a953b1ab24b29ca8121e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463406"
---
# <a name="enterprise-web-deployment-scenario-overview"></a>企业 Web 部署：方案概述

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 这一组教程使用一个示例解决方案，其中包含实际的复杂性级别，同时提供一种虚构的企业部署方案，以提供参考实现并为任务和演练提供一个常见上下文。 本主题介绍了教程方案，并介绍了示例解决方案。

## <a name="scenario-description"></a>方案描述

Fabrikam，Inc.，一家虚构公司正在创建一个解决方案，该解决方案允许远程销售团队存储和检索 web 界面中的联系人信息。

Fabrikam，Inc. 的应用程序生命周期管理（ALM）流程要求在软件开发过程的各个阶段将解决方案部署到三个服务器环境：

- 开发人员测试或 "沙盒" 环境。
- 基于 intranet 的过渡环境。
- 面向 Internet 的生产环境。

其中每个环境都有不同的配置和安全要求，每个都有独特的部署挑战。

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam，Inc. 服务器基础结构

这是 Fabrikam，Inc. 的高级开发和部署基础结构。

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

开发人员工作站、源代码管理基础结构、开发人员测试环境和过渡环境都驻留在 Fabrikam.net 域内的 intranet 网络中。 生产环境驻留在外围网络（也称为 DMZ、外围安全区域和外围子网）中，防火墙与 intranet 网络隔离。 这是一种常见的部署方案：通常通过使用防火墙或网关服务器，将面向 Internet 的 web 服务器与内部服务器基础结构隔离开来。

在此示例中：

- 使用单独的生成服务器 Team Foundation Server （TFS）2010服务器提供源控件和持续集成（CI）功能。
- 开发人员测试环境包括 Internet Information Services （IIS） 7.5 web 服务器和 SQL Server 2008 R2 数据库服务器。
- 生产环境包含由 Web 场框架（WFF）控制器服务器同步的多个 IIS 7.5 web 服务器，以及 SQL Server 2008 R2 数据库服务器。 在实践中，数据库服务器可以使用群集或镜像来提高可伸缩性和可用性。
- 过渡环境旨在尽可能地复制生产环境的配置。
- 防火墙和网络隔离策略不允许将 intranet 直接部署到外围网络。

在第二个教程[配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)中，更详细地介绍了每个环境的配置。

### <a name="team-roles-for-alm"></a>ALM 团队角色

这些用户涉及到创建、管理、生成和发布 Contact Manager 解决方案：

- Matt Hink 是 Fabrikam，Inc. 的 web 应用程序开发人员。他是使用 Visual Studio 2010 开发联系人经理解决方案的团队的成员。 Matt 对开发人员测试环境中的服务器具有完全管理员权限，使其能够配置环境以满足其需求。 他还具有对 Visual Studio 2010 TFS 实例的用户访问权限，在该实例中存储 Contact Manager 解决方案的源代码。
- 对于 Fabrikam，Inc. 开发团队而言，Walters 是服务器管理员。 必须在 TFS 服务器上具有管理访问权限，以便可以配置 TFS 和 Team Build 的所有方面。 "抢" 还具有对测试和过渡 web 服务器的管理访问权限，并充当测试和过渡环境中数据库服务器的数据库管理员（DBA）。 对于 TFS 服务器上的 "已配置团队生成"，要执行这些任务，请执行以下操作：

    - 当用户将文件签入到 TFS 时，在应用程序上生成并运行单元测试。 这称为 CI。
    - 应用程序通过单元测试后，自动将联系人管理器应用程序部署到测试环境。 这包括在初始部署时将数据库发布到测试服务器，以及在初始部署后对数据库进行任何更新。
    - 在单步执行过程中，将联系人管理器应用程序部署到过渡环境。
    - 创建 web 包，Web 服务器管理员和 DBA 可以使用它将应用程序发布到生产环境。
- Lisa Andrews 是一个服务器管理员，负责将应用程序部署到 Fabrikam，Inc. 生产服务器。 她拥有对共享的读取访问权限，而 TFS Team Build 在生成联系人管理器应用程序后将在其中存储 web 部署包。 她还具有对生产 web 服务器的管理访问权限，以便可以将应用程序部署到生产环境中。 另外，她充当在生产环境中将数据库和数据库更新部署到数据库服务器的 DBA。

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Contact Manager 解决方案

联系人管理器解决方案旨在允许注册的已登录用户通过 web 界面添加和编辑联系人信息。 Contact Manager 解决方案由四个单独的项目组成：

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager**。 这是一个 ASP.NET MVC3 web 应用程序项目，它表示解决方案的入口点。 它提供了一些基本 web 应用程序功能，例如，为用户提供创建和查看联系人详细信息的能力。 应用程序依赖于 Windows Communication Foundation （WCF）服务来管理联系人，并使用 ASP.NET 应用程序服务数据库来管理身份验证和授权。
- **ContactManager**。 这是 Visual Studio 2010 数据库项目。 项目定义用于存储联系人详细信息的数据库的架构。
- **ContactManager**。 这是一个 WCF web services 项目。 WCF 公开一个终结点，该终结点允许调用方对联系人管理器数据库执行创建、检索、更新和删除（CRUD）操作。 该服务依赖于 Contact Manager 数据库和 ContactManager 程序集。
- **ContactManager**。 这是一个类库项目。 WCF 服务依赖于此程序集中定义的类型。

本系列的第一个教程（[企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)）中提供了解决方案及其部署要求的完整回顾。

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>部署任务

在大型组织中将应用程序部署到不同环境涉及到几个不同的任务。 这些是教程涵盖的主要任务：

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

下面是本文档前面所述的用户对部署过程中每个步骤的列表：

1. 团队的所有成员在 Visual Studio 2010 中查看 Contact Manager 解决方案，以确定重要的部署要求和问题。
2. Matt Hink 可将 Contact Manager 解决方案直接从开发人员工作站部署到开发人员测试环境，以执行部署逻辑的初始测试。
3. Matt Hink 将应用程序添加到 TFS 中的源代码管理。
4. "信息 Walters" 为 Team Build 中的联系人管理器解决方案创建了不同的生成定义。 当用户签入新代码时，一个生成定义使用 CI 将解决方案部署到开发人员测试环境。 其他生成定义允许用户根据需要触发到过渡环境的部署。
5. 用户每次签入新代码时，如果生成成功并且单元测试通过，则 Team Build 自动生成解决方案组件、运行单元测试并将解决方案部署到开发人员测试环境。
6. 当用户触发部署到过渡环境时，解决方案将打包并部署在一个单步过程中。 此过程还会生成用于手动部署到生产环境的包。
7. Lisa Andrews 通过手动导入在步骤6中创建的 web 包，将应用程序部署到生产环境。

### <a name="key-deployment-issues"></a>主要部署问题

联系人经理解决方案和 Fabrikam，Inc. 的方案重点介绍了在部署复杂的企业级解决方案时可能遇到的各种常见问题和挑战。 例如:

- 你需要能够将项目部署到多个环境，如开发人员或测试环境、过渡平台和生产服务器。 需要为每个环境部署解决方案的不同配置设置。
- 需要在单步或自动生成和部署过程中同时部署多个依赖项目。
- 你需要能够从自动过程中驱动部署。 例如，要在签入新代码时使用 CI 进程将 web 应用程序部署到过渡环境。
- 你需要能够控制部署过程，并从 Visual Studio 外部设置部署变量，因为开发人员不太可能具有适用于每个目标环境的正确配置设置或必要凭据。
- 你需要部署基于架构的数据库项目，并在后续部署中保留现有数据。
- 你需要临时部署成员资格数据库，而无需部署用户帐户数据。 你可能还需要更新已部署成员资格数据库的架构，而不会丢失现有的用户帐户数据。
- 在将内容部署到各种目标环境时，需要排除某些文件或文件夹。

此外，在频繁更新和增量管理时管理部署会引发一些额外的挑战。 例如:

- 每当开发人员签入新代码时，都将运行单元测试。 如果代码通过了单元测试，则只需部署解决方案。
- 将 web 应用程序部署到过渡环境或生产环境时，需要在部署过程中将用户重定向到*应用\_脱机 .htm*文件。
- 要记录部署活动。 部署过程应将成功或失败的部署的电子邮件通知发送给指定的收件人。
- 如果自动部署失败，部署过程应重试当前部署，或改为部署以前的 web 包。

> [!div class="step-by-step"]
> [上一页](deploying-web-applications-in-enterprise-scenarios.md)
> [下一页](application-lifecycle-management-from-development-to-production.md)
