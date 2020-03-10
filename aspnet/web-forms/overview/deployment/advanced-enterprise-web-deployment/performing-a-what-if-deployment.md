---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 执行 What If 部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web 部署）和 V ...，来执行 "假设" （或模拟）部署。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510332"
---
# <a name="performing-a-what-if-deployment"></a>执行“What If”部署

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web 部署）和 VSDBCMD 来执行 "假设" （或模拟）部署。 这样，你就可以在实际部署应用程序之前，确定你的部署逻辑对特定目标环境的影响。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中描述的拆分项目文件方法，其中，生成和部署过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含环境特定的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="performing-a-what-if-deployment-for-web-packages"></a>为 Web 包执行 "What If" 部署

Web 部署包含了一些功能，可用于在 "假设" （或 "试用"）模式下执行部署。 当你在 "假设" 模式下部署项目时，Web 部署会生成一个日志文件，就像你已执行部署一样，但它实际上不会更改目标服务器上的任何内容。 查看日志文件可帮助你了解部署在目标服务器上的影响，具体取决于：

- 添加的内容。
- 将更新的内容。
- 删除的内容。

由于 "假设" 部署实际上不会更改目标服务器上的任何内容，因此它无法始终预测部署是否会成功。

如[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)中所述，可以通过两种方式使用 Web 部署以两&#x2014;种方式部署 web 包：直接使用 msdeploy.exe 命令行实用程序或运行生成过程生成的 *.deploy .cmd*文件。

如果要直接使用 Msdeploy.exe，可以通过将 **– whatif**标志添加到命令来运行 "假设" 部署。 例如，若要评估在将 ContactManager 包部署到过渡环境时将发生的情况，Msdeploy.exe 命令应如下所示：

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

如果对 "假设" 部署的结果感到满意，则可以删除 **– whatif**标志来运行实时部署。

> [!NOTE]
> 有关 Msdeploy.exe 的命令行选项的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。

如果你使用的是 *.deploy .cmd*文件，则可以在命令中包含 **/t**标志（试用模式）标志，而不是在命令中包含 **/y**标志（"是" 或 "更新" 模式）来运行 "假设"。 例如，若要评估通过运行 *.deploy .cmd*文件部署 ContactManager 包时将发生的情况，命令应如下所示：

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

当你对 "试用模式" 部署的结果感到满意后，可以将 **/t**标志替换为 **/y**标志，以运行实时部署：

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> 有关 *.deploy .cmd*文件的命令行选项的详细信息，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。 如果在未指定任何标志的情况下运行 *.deploy .cmd*文件，则命令提示符将显示可用标志的列表。

## <a name="performing-a-what-if-deployment-for-databases"></a>为数据库执行 "What If" 部署

本部分假设你要使用 VSDBCMD 实用工具执行基于架构的增量数据库部署。 [部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)中更详细地介绍了这种方法。 在应用此处所述的概念之前，我们建议你熟悉本主题。

在**部署**模式下使用 VSDBCMD 时，可以使用 **/Dd** （或 **/DEPLOYTODATABASE**）标志来控制 VSDBCMD 是实际部署数据库还是只生成部署脚本。 如果要部署 .dbschema 文件，这是行为：

- 如果指定 **/dd +** 或 **/Dd**，则 VSDBCMD 将生成部署脚本并部署数据库。
- 如果指定 **/dd-** 或省略开关，则 VSDBCMD 将仅生成部署脚本。

> [!NOTE]
> 如果部署的是 deploymanifest 文件而不是 .dbschema 文件，则 **/dd**开关的行为要复杂得多。 实质上，如果 deploymanifest 文件包含值为**True**的**DeployToDatabase**元素，则 VSDBCMD 将忽略 **/dd**开关的值。 [部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)完全说明了此行为。

例如，若要为**ContactManager**数据库生成部署脚本而不实际部署数据库，则 VSDBCMD 命令应如下所示：

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

VSDBCMD 是一个差异数据库部署工具，因此部署脚本会动态生成，以包含更新当前数据库（如果存在）到指定架构所需的所有 SQL 命令。 查看部署脚本是一种有用的方法，用于确定您的部署对当前数据库及其包含的数据产生的影响。 例如，你可能想要确定：

- 是否将删除任何现有的表，以及是否将导致数据丢失。
- 操作的顺序是否会产生数据丢失的风险，例如，是拆分或合并表。

如果你对部署脚本感到满意，则可以使用 **/dd +** 标志重复 VSDBCMD 以进行更改。 或者，您可以编辑部署脚本以满足您的要求，然后在数据库服务器上手动执行它。

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>将 "What If" 功能集成到自定义项目文件

在更复杂的部署方案中，你将需要使用自定义 Microsoft 生成引擎（MSBuild）项目文件来封装生成和部署逻辑，如[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述。 例如，在[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案中，*发布*文件：

- 生成解决方案。
- 使用 Web 部署打包和部署 ContactManager 应用程序。
- 使用 Web 部署打包和部署 ContactManager 应用程序。
- 部署**ContactManager**数据库。

以这种方式将多个 web 包和/或数据库的部署集成到单个步骤过程中时，您可能还希望在 "假设" 模式下执行整个部署。

*发布 proj*文件演示了如何执行此操作。 首先，需要创建属性以存储 "假设值" 值：

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

在这种情况下，你已经创建了一个名为**WhatIf**的属性，其默认值为**false**。 用户可以通过将命令行参数中的属性设置为**true** ，来重写此值，如稍后所示。

下一阶段是参数化任何 Web 部署和 VSDBCMD 命令，使标志反映**WhatIf**属性值。 例如，下一个目标（从*Publish*文件开始，并简化）会运行 *.deploy .cmd*文件来部署 web 包。 默认情况下，该命令包含 **/y**开关（"是" 或 "更新" 模式）。 如果 " **WhatIf** " 设置为 " **true**"，则会将其替换为 **/t**开关（试用或 "假设" 模式）。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

同样，下一个目标使用 VSDBCMD 实用程序来部署数据库。 默认情况下，不包括 **/dd**开关。 这意味着 VSDBCMD 将生成一个部署脚本，但不会部署该数据库&#x2014;，即 "假设" 方案。 如果**WhatIf**属性未设置为**true**，则将添加 **/dd**开关，并且 VSDBCMD 将部署该数据库。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

您可以使用相同的方法参数化项目文件中的所有相关命令。 如果要运行 "假设" 部署，只需从命令行提供**WhatIf**属性值即可：

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

通过这种方式，您可以在单个步骤中为所有项目组件运行 "假设" 部署。

## <a name="conclusion"></a>结束语

本主题介绍了如何使用 Web 部署、VSDBCMD 和 MSBuild 来运行 "假设" 部署。 "假设" 部署可让你在实际对目标环境进行任何更改之前评估建议的部署的影响。

## <a name="further-reading"></a>其他阅读材料

有关 Web 部署命令行语法的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。 有关使用 *.deploy*文件时的命令行选项的指导，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。 有关 VSDBCMD 命令行语法的指导，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)。

> [!div class="step-by-step"]
> [上一页](advanced-enterprise-web-deployment.md)
> [下一页](customizing-database-deployments-for-multiple-environments.md)
