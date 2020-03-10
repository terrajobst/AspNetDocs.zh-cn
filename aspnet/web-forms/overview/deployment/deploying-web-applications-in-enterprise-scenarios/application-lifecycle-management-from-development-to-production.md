---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 应用程序生命周期管理：从开发到生产 |Microsoft Docs
author: jrjlee
description: 本主题说明了虚构公司如何通过测试、过渡和生产环境（例如 ...）来管理 ASP.NET web 应用程序的部署。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 230cf4393db0ee19cfc42ed54359d61e7926a49d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520424"
---
# <a name="application-lifecycle-management-from-development-to-production"></a>应用程序生命周期管理：从开发到生产

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题说明了如何通过测试、过渡和生产环境将 ASP.NET web 应用程序部署为持续开发过程的一部分。 本主题中提供了有关如何执行特定任务的详细信息和演练的链接。
> 
> 本主题旨在提供企业中有关 web 部署的一[系列教程](deploying-web-applications-in-enterprise-scenarios.md)的高级概述。 如果你不熟悉此处&#x2014;所述的某些概念，请不要担心下面的教程提供了有关所有这些任务和技术的详细信息。
> 
> > [!NOTE]
> > 为了简单起见，本主题不讨论作为部署过程的一部分更新数据库。 但是，对数据库功能进行增量更新是一项要求的企业部署方案，你可以在本系列教程的后面部分找到有关如何完成此操作的指导。 有关详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。

## <a name="overview"></a>概述

此处所示的部署过程基于[企业 Web 部署：方案概述](enterprise-web-deployment-scenario-overview.md)中所述的 Fabrikam，inc. 部署方案。 在学习本主题之前，应阅读方案概述。 实质上，该方案检查组织如何通过典型企业环境中的各个阶段来管理合理复杂的 web 应用程序（即[联系人经理解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)）的部署。

从较高层次来看，Contact Manager 解决方案在开发和部署过程中将经历以下几个阶段：

1. 开发人员将一些代码签入 Team Foundation Server （TFS）2010。
2. TFS 生成代码并运行与团队项目关联的任何单元测试。
3. TFS 将解决方案部署到测试环境。
4. 开发人员团队在测试环境中验证并验证解决方案。
5. 过渡环境管理员对过渡环境执行 "假设" 部署，以确定部署是否会导致任何问题。
6. 过渡环境管理员执行到过渡环境的实时部署。
7. 此解决方案在过渡环境中进行用户验收测试。
8. Web 部署包被手动导入到生产环境中。

这些阶段构成了持续开发周期的一部分。

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

在实践中，此过程稍微复杂一些，因为我们更详细地探讨每个阶段。 Fabrikam，Inc. 对每个目标环境使用不同的部署方法。

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

本主题的其余部分将探讨此部署生命周期的以下关键阶段：

- **先决条件**：在放置部署逻辑之前，你需要如何配置你的服务器基础结构。
- **初始开发和部署**：首次部署解决方案之前需要执行的操作。
- **要测试的部署**：当开发人员签入新代码时，如何自动将内容打包并部署到测试环境。
- **部署到过渡**：如何将特定版本部署到过渡环境，以及如何执行 "假设" 部署以确保部署不会导致任何问题。
- **部署到生产**：当网络基础结构阻止远程部署时，如何将 web 包导入生产环境。

## <a name="prerequisites"></a>系统必备

任何部署方案中的第一项任务是确保你的服务器基础结构满足你的部署工具和技术的要求。 在此示例中，Fabrikam，Inc. 配置了其服务器基础结构，如下所示：

- TFS 配置为包括团队项目集合、生成控制器和生成代理。 有关详细信息，请参阅为[自动 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 。
- 测试环境配置为接受使用 Web 部署代理服务（"远程代理"）的远程部署，如[方案：配置用于 Web 部署的测试环境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md)和[配置用于 Web 部署发布的 Web 服务器（远程代理）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)中所述。
- 过渡环境配置为使用 Web 部署处理程序终结点接受远程部署，如[方案：配置用于 Web 部署的过渡环境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md)和[配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述。
- 生产环境配置为允许管理员手动将 web 部署包导入 Internet Information Services （IIS），如[方案：配置用于 Web 部署的生产环境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md)和[配置用于 Web 部署发布的 Web 服务器（脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)中所述。

## <a name="initial-development-and-deployment"></a>初始开发和部署

在 Fabrikam，Inc. 开发团队首次部署 Contact Manager 解决方案之前，需要执行以下任务：

- 在 TFS 中创建新的团队项目。
- 创建包含部署逻辑的 Microsoft 生成引擎（MSBuild）项目文件。
- 创建用于触发部署过程的 TFS 生成定义。

### <a name="create-a-new-team-project"></a>创建新的团队项目

- TFS 管理员为应用程序创建新的团队项目（如在[TFS 中创建团队项目](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)中所述）为应用程序创建新的团队项目。 接下来，首席开发人员 Matt Hink 创建一个主干解决方案。 他根据[将内容添加到源代码管理](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)中所述，将其文件签入 TFS 中的新团队项目。

### <a name="create-the-deployment-logic"></a>创建部署逻辑

Matt Hink 使用[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的 split 项目文件方法创建各种自定义 MSBuild 项目文件。 Matt 创建：

- 名为*Publish*的项目文件，用于运行部署过程。 此文件包含在解决方案中生成项目的 MSBuild 目标、创建 web 包以及将包部署到目标服务器环境。
- 环境特定的项目文件，其名称为*Env-Dev*和*env*。 这些设置分别包含特定于测试环境和过渡环境的设置，例如连接字符串、服务终结点以及将接收 web 包的远程服务的详细信息。 有关为特定目标环境选择正确设置的指导，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

若要运行部署，用户可以使用 MSBuild 或 Team Build 执行*Publish*文件，并将相关的特定于环境的项目文件（*env*或*env*）的位置指定为命令行参数。 然后， *Publish*文件导入特定于环境的项目文件，为每个目标环境创建一组完整的发布说明。

> [!NOTE]
> 这些自定义项目文件的工作方式与用于调用 MSBuild 的机制无关。 例如，可以直接使用 MSBuild 命令行，如[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述。 你可以从命令文件运行项目文件，如[创建和运行部署命令文件](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)中所述。 或者，你可以根据[创建支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)中所述，从 TFS 中的生成定义运行项目文件。  
> 在每种情况下，最终结果是&#x2014;相同的 MSBuild 执行合并的项目文件并将解决方案部署到目标环境。 这为你提供了有关如何触发发布过程的很大的灵活性。

创建自定义项目文件后，Matt 会将这些文件添加到解决方案文件夹中，并将其签入源代码管理。

### <a name="create-build-definitions"></a>创建生成定义

作为最后一项准备任务，Matt 和抢一起工作，为新的团队项目创建三个生成定义：

- **DeployToTest**。 这会生成 Contact Manager 解决方案，并将其部署到测试环境中，每次发生签入。
- **DeployToStaging**。 当开发人员对生成进行排队时，这会将从指定的早期版本部署到过渡环境中的资源。
- **DeployToStaging**。 当开发人员对生成进行排队时，这将执行 "假设" 部署到过渡环境。

以下各节提供了有关每个生成定义的更多详细信息。

## <a name="deployment-to-test"></a>要测试的部署

Fabrikam，Inc. 的开发团队维护测试环境以执行各种软件测试活动，如验证和验证、可用性测试、兼容性测试，以及即席或探索测试。

开发团队已在 TFS 中创建了一个名为**DeployToTest**的生成定义。 此生成定义使用持续集成触发器，这意味着每次 Fabrikam，Inc. 开发团队的成员执行签入时都会运行生成过程。 触发生成时，生成定义将：

- 生成 ContactManager 解决方案。 这进而会生成解决方案中的每个项目。
- 在解决方案文件夹结构中运行任何单元测试（如果解决方案成功生成）。
- 运行控制部署过程的自定义项目文件（如果解决方案成功生成并通过所有单元测试）。

最终的结果是，如果解决方案成功生成并通过了单元测试，则会将 web 包和任何其他部署资源部署到测试环境中。

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>部署过程是如何工作的？

**DeployToTest**生成定义为 MSBuild 提供以下参数：

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]

当团队生成生成解决方案中的项目时，将使用**DeployOnBuild = true**和**DeployTarget = package**属性。 当项目是 web 应用程序项目时，这些属性指示 MSBuild 为项目创建 web 部署包。 **TargetEnvPropsFile**属性指示*Publish*文件，在何处可以找到要导入的特定于环境的项目文件。

> [!NOTE]
> 有关如何创建此类生成定义的详细演练，请参阅[创建支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

*Publish*文件包含用于生成解决方案中每个项目的目标。 不过，它还包括在 Team Build 中执行文件时跳过这些生成目标的条件逻辑。 这样，你便可以利用团队生成提供的其他生成功能，如运行单元测试的能力。 如果解决方案生成或单元测试失败，则不会执行*Publish*文件，并且不会部署应用程序。

条件逻辑是通过计算**BuildingInTeamBuild**属性来实现的。 这是一个 MSBuild 属性，当你使用 Team Build 来生成项目时，此属性将自动设置为**true** 。

## <a name="deployment-to-staging"></a>部署到过渡

当生成满足测试环境中开发人员团队的所有要求时，团队可能需要将同一版本部署到过渡环境。 通常情况下，过渡环境配置为匹配生产或 "实时" 环境的特征，例如，在服务器规范、操作系统和软件以及网络配置方面。 过渡环境通常用于负载测试、用户验收测试和更广泛的内部审查。 生成直接从生成服务器部署到过渡环境。

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

用于将解决方案部署到过渡环境（ **DeployToStaging**和**DeployToStaging**）的生成定义共享以下特征：

- 它们实际上不会生成任何内容。 当 "解决方法" 将解决方案部署到过渡环境时，他希望部署在测试环境中已经过验证和验证的特定现有版本。 生成定义只需运行控制部署过程的自定义项目文件。
- 当抢触发生成时，他使用生成参数来指定哪个生成包含要从生成服务器部署的资源。
- 生成定义不会自动触发。 当用户想要将解决方案部署到过渡环境时，请手动对生成进行排队。

这是部署到过渡环境的高级过程：

1. 过渡环境管理员，Walters 是使用**DeployToStaging**生成定义对生成进行排队。 "抢" 使用生成定义参数来指定要部署的生成。
2. **DeployToStaging**生成定义在 "假设" 模式下运行自定义项目文件。 这会生成日志文件，就像是否可以使用该方法来执行实时部署，但它实际上不会对目标环境进行任何更改。
3. "" "" "" "" "" "" "" "" "" "" "。 特别是，"更新" 需要检查将添加的内容、要更新的内容以及将删除的内容。
4. 如果要使部署不会对现有资源或数据进行任何不需要的更改，则使用**DeployToStaging**生成定义对生成进行排队。
5. **DeployToStaging**生成定义运行自定义项目文件。 它们将部署资源发布到过渡环境中的主 web 服务器。
6. Web 场框架（WFF）控制器同步过渡环境中的 web 服务器。 这会使应用程序在服务器场中的所有 web 服务器上可用。

### <a name="how-does-the-deployment-process-work"></a>部署过程是如何工作的？

**DeployToStaging**生成定义为 MSBuild 提供以下参数：

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]

**TargetEnvPropsFile**属性指示*Publish*文件，在何处可以找到要导入的特定于环境的项目文件。 **OutputRoot**属性重写内置值，并指示包含要部署的资源的生成文件夹的位置。 当 "OutputRoot" 对生成进行排队时，他使用 "**参数**" 选项卡为 " " 属性提供更新的值。

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 有关如何创建此类生成定义的详细信息，请参阅[部署特定生成](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)。

**DeployToStaging**生成定义包含与**DeployToStaging**生成定义相同的部署逻辑。 不过，它还包括其他参数**WhatIf = true**：

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]

在*Publish*文件中， **WhatIf**属性指示应在 "假设" 模式下发布所有部署资源。 换句话说，生成的日志文件就像部署已过，但目标环境中实际没有发生任何更改。 这样，你就可以评估建议的部署&#x2014;的影响，特别是添加的内容、将更新的内容以及在实际进行任何更改&#x2014;之前会删除的内容。

> [!NOTE]
> 有关如何配置 "假设" 部署的详细信息，请参阅[执行 "What If" 部署](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)。

将应用程序部署到过渡环境中的主 web 服务器后，WFF 会自动在服务器场中的所有服务器之间同步应用程序。

> [!NOTE]
> 有关配置 WFF 以同步 web 服务器的详细信息，请参阅[使用 Web 场框架创建服务器场](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)。

## <a name="deployment-to-production"></a>部署到生产

在过渡环境中批准某个生成后，Fabrikam，Inc. 团队可以将该应用程序发布到生产环境。 在生产环境中，应用程序进入 "实时"，并进入最终用户的目标受众。

生产环境位于面向 Internet 的外围网络中。 这与包含生成服务器的内部网络是隔离的。 生产环境管理员郭 Andrews 必须手动从生成服务器复制 web 部署包，并将其导入到主生产 web 服务器上的 IIS 中。

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

这是部署到生产环境的高级过程：

1. 开发人员团队建议在某个版本已准备好部署到生产环境中。 团队建议在生成服务器上的放置文件夹中的 web 部署包位置。
2. Lisa 从生成服务器收集 web 包，并将其复制到生产环境中的主 web 服务器。
3. Lisa 使用 IIS 管理器来导入主 web 服务器上的 web 包并将其发布。
4. WFF 控制器将同步生产环境中的 web 服务器。 这会使应用程序在服务器场中的所有 web 服务器上可用。

### <a name="how-does-the-deployment-process-work"></a>部署过程是如何工作的？

IIS 管理器包含一个 "导入应用程序包" 向导，该向导可让你轻松地将 web 包发布到 IIS 网站。 有关如何执行此过程的演练，请参阅[手动安装 Web 包](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)。

## <a name="conclusion"></a>结束语

本主题提供了典型的企业级 web 应用程序的部署生命周期的说明。

本主题提供了一系列教程的一部分，这些教程提供了有关 web 应用程序部署的各个方面的指导。 在实践中，部署过程的每个阶段都有很多其他任务和注意事项，并且不能在单个演练中涵盖所有任务和注意事项。 有关详细信息，请参阅以下教程：

- [企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程全面介绍了使用 MSBuild 和 IIS Web 部署工具（Web 部署）的 web 部署技术。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程提供有关如何配置 Windows server 环境以支持各种部署方案的指南。
- [为自动 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程提供有关如何将部署逻辑集成到 TFS 生成过程的指导。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程提供有关如何满足组织面临的一些更复杂的部署挑战的指导。

> [!div class="step-by-step"]
> [上一页](enterprise-web-deployment-scenario-overview.md)
