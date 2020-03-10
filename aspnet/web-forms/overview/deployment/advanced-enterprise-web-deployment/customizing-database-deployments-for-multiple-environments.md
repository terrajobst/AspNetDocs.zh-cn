---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: 为多个环境自定义数据库部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在部署过程中将数据库的属性定制为特定的目标环境。 注意：本主题假设 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 8ae8cb1a322afb95c5d2e8d5e73c7825c7b2fe5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489032"
---
# <a name="customizing-database-deployments-for-multiple-environments"></a>自定义多个环境的数据库部署

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何在部署过程中将数据库的属性定制为特定的目标环境。
> 
> > [!NOTE]
> > 本主题假设你要使用 Msbuild.exe 和 VSDBCMD 部署 Visual Studio 2010 数据库项目。 有关选择此方法的原因的详细信息，请参阅[企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)和[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。
> 
> 
> 将数据库项目部署到多个目标时，通常需要为每个目标环境自定义数据库部署属性。 例如，在测试环境中，您通常会在每次部署时重新创建数据库，而在过渡环境或生产环境中，您更有可能进行增量更新以保留数据。
> 
> 在 Visual Studio 2010 数据库项目中，部署设置包含在部署配置（sqldeployment）文件中。 本主题将演示如何创建特定于环境的部署配置文件，并指定要用作 VSDBCMD 参数的配置文件。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

本主题假定：

- 按照[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述，使用拆分项目文件方法进行解决方案部署。
- 从项目文件调用 VSDBCMD 来部署数据库项目，如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述。

若要创建支持在目标环境之间改变数据库部署属性的部署系统，需要：

- 为每个目标环境创建部署配置（. sqldeployment）文件。
- 创建一个 VSDBCMD 命令，该命令将部署配置文件指定为命令行开关。
- 参数化 Microsoft 生成引擎（MSBuild）项目文件中的 VSDBCMD 命令，以便 VSDBCMD 选项适用于目标环境。

本主题将演示如何执行上述每个过程。

## <a name="creating-environment-specific-deployment-configuration-files"></a>创建环境特定的部署配置文件

默认情况下，数据库项目包含一个名为*sqldeployment*的部署配置文件。 如果在 Visual Studio 2010 中打开此文件，可以看到可供你使用的不同部署选项：

- **部署比较排序规则**。 这使您可以选择是使用您的项目的数据库排序规则（*源*排序规则）还是目标服务器的数据库排序规则（*目标*排序规则）。 在大多数情况下，你需要在部署到开发或测试环境时使用源排序规则。 部署到过渡环境或生产环境时，通常需要保持目标排序规则不变，以避免任何互操作性问题。
- **部署数据库属性**。 这允许您选择是否应用数据库属性（如*sqlsettings*文件中所定义）。 首次部署数据库时，应该部署数据库属性。 如果要更新现有数据库，则属性应该已准备就绪，并且你不需要再次部署它们。
- **始终重新创建数据库**。 这使你可以选择在每次部署时是否重新创建目标数据库，或进行增量更改，使目标数据库与你的架构保持同步。 如果重新创建数据库，则会丢失现有数据库中的所有数据。 因此，通常应将此值设置为**false** ，以便部署到过渡环境或生产环境。
- **如果可能发生数据丢失，则阻止增量部署**。 这使你可以选择在对数据库架构进行更改将导致数据丢失的情况下是否应停止部署。 通常将此值设置为**true** ，以便部署到生产环境，从而使你能够干预和保护任何重要数据。 如果将 "**始终重新创建数据库**" 设置为 " **false**"，则此设置将不起作用。
- **在单用户模式下执行部署**。 在开发或测试环境中，这通常不是问题。 但是，通常应将此值设置为**true** ，以便部署到过渡环境或生产环境。 这会阻止用户在部署过程中对数据库进行更改。
- **在部署之前备份数据库**。 在部署到生产环境时，通常将此值设置为**true** ，以防止数据丢失。 如果你的临时数据库包含大量数据，则在部署到过渡环境时，你可能还希望将其设置为**true** 。
- **为目标数据库中但不在数据库项目中的对象生成 DROP 语句**。 在大多数情况下，这是对数据库进行增量更改的必不可少的组成部分。 如果将 "**始终重新创建数据库**" 设置为 " **false**"，则此设置将不起作用。
- **不要使用 ALTER ASSEMBLY 语句更新 CLR 类型**。 此设置确定 SQL Server 应如何将公共语言运行时（CLR）类型更新为较新的程序集版本。 在大多数情况下，此值应设置为**false** 。

此表显示了不同目标环境的典型部署设置。 但是，根据具体的要求，设置可能会有所不同。

|  | 开发人员/测试 | 过渡/集成 | 生产 |
| --- | --- | --- | --- |
| **部署比较排序规则** | source | Target | Target |
| **部署数据库属性** | True | 仅首次 | 仅首次 |
| **始终重新创建数据库** | True | False | False |
| **如果可能发生数据丢失，则阻止增量部署** | False | 可能 | True |
| **在单用户模式下执行部署脚本** | False | True | True |
| **部署前备份数据库** | False | 可能 | True |
| **为目标数据库中但不在数据库项目中的对象生成 DROP 语句** | False | True | True |
| **不要使用 ALTER ASSEMBLY 语句更新 CLR 类型** | False | False | False |

> [!NOTE]
> 有关数据库部署属性和环境注意事项的详细信息，请参阅[数据库项目设置的概述](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)、[如何：配置部署详细信息的属性](https://msdn.microsoft.com/library/dd172125.aspx)、[生成数据库并将其部署到隔离的开发环境](https://msdn.microsoft.com/library/dd193409.aspx)，以及[生成数据库并将其部署到过渡环境或生产环境](https://msdn.microsoft.com/library/dd193413.aspx)。

若要支持将数据库项目部署到多个目标，应为每个目标环境创建一个部署配置文件。

**创建环境特定的配置文件**

1. 在 Visual Studio 2010 的 "**解决方案资源管理器**" 窗口中，右键单击数据库项目，然后单击 "**属性**"。
2. 在 "数据库项目" 属性页上，在 **"部署" 选项卡**上的 "**部署配置文件**" 行中，单击 "**新建**"。

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. 在 "**新建部署配置文件**" 对话框中，为文件指定一个有意义的名称（例如， **TestEnvironment. sqldeployment**），然后单击 "**保存**"。
4. 在 *[Filename] * * *. sqldeployment** 页上，设置部署属性以匹配目标环境的要求，然后保存该文件。

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. 请注意，新文件将添加到数据库项目的 Properties 文件夹中。

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>在 VSDBCMD 中指定部署配置文件

在 Visual Studio 2010 中使用解决方案配置（如调试和发布）时，可以将部署配置文件与每个配置相关联。 生成特定配置时，生成过程将生成特定于配置的部署清单文件，该文件指向配置特定的部署配置文件。 不过，这些教程中所述的部署方法的主要目的之一是使用户能够控制部署过程，而无需使用 Visual Studio 2010 和解决方案配置。 在此方法中，无论目标部署环境如何，解决方案配置都是相同的。 若要将数据库部署自适应特定目标环境，可以使用 VSDBCMD 命令行选项指定部署配置文件。

若要在 VSDBCMD 中指定部署配置文件，请使用**p：/DeploymentConfigurationFile**开关并提供文件的完整路径。 这会重写部署清单标识的部署配置文件。 例如，你可以使用此 VSDBCMD 命令将**ContactManager**数据库部署到测试环境：

[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]

> [!NOTE]
> 请注意，在将文件复制到输出目录时，生成过程可能会重命名你的 sqldeployment 文件。

如果在预先部署或后期部署 SQL 脚本中使用 SQL 命令变量，则可以使用类似的方法将环境特定的 sqlcmdvars 文件与部署相关联。 在这种情况下，可以使用**p：/SqlCommandVariablesFile**开关来识别 sqlcmdvars 文件。

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>从 MSBuild 项目文件运行 VSDBCMD 命令

可以通过使用 MSBuild 目标中的**Exec**任务，从 msbuild 项目文件调用 VSDBCMD 命令。 最简单的形式如下：

[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]

- 在实践中，若要使您的项目文件易于阅读和重用，您需要创建用于存储各种命令行参数的属性。 这样，用户就可以更轻松地在特定于环境的项目文件中提供属性值或从 MSBuild 命令行重写默认值。 如果你使用[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，则应相应地在两个文件之间划分生成说明和属性：
- 环境特定的设置（如部署配置文件名、数据库连接字符串和目标数据库名称）应位于特定于环境的项目文件中。
- 运行 VSDBCMD 命令的 MSBuild 目标与 VSDBCMD 可执行文件的位置（如可执行文件的位置）应在通用项目文件中。

还应确保在调用 VSDBCMD 之前生成数据库项目，以便创建 deploymanifest 文件并使其可供使用。 有关此方法的完整示例，请参阅主题[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，该过程将指导你完成[Contact Manager 示例解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)中的项目文件。

## <a name="conclusion"></a>结束语

本主题介绍了如何在使用 MSBuild 和 VSDBCMD 部署数据库项目时，将数据库属性自适应不同的目标环境。 当你需要将数据库项目部署为大型企业级解决方案的一部分时，此方法非常有用。 这些解决方案通常部署到多个目标，如沙盒开发或测试环境、过渡或集成平台以及生产或实时环境。 其中每个目标环境通常都需要一组唯一的数据库部署属性。

## <a name="further-reading"></a>其他阅读材料

有关使用 VSDBCMD 部署数据库项目的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

MSDN 上的这些文章提供了有关数据库部署的更多常规指导：

- [数据库项目设置概述](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [如何：配置部署详细信息的属性](https://msdn.microsoft.com/library/dd172125.aspx)
- [生成数据库并将其部署到隔离开发环境](https://msdn.microsoft.com/library/dd193409.aspx)
- [生成数据库并将其部署到过渡环境或生产环境](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [上一页](performing-a-what-if-deployment.md)
> [下一页](deploying-database-role-memberships-to-test-environments.md)
