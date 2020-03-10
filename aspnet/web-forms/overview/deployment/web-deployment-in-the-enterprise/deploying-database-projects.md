---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: 部署数据库项目 |Microsoft Docs
author: jrjlee
description: 注意：在许多企业部署方案中，需要能够将增量更新发布到已部署的数据库。 替代方法是重新创建 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 221808758492aedb8e8329364e511df28fd11105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514940"
---
# <a name="deploying-database-projects"></a>部署数据库项目

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> 在许多企业部署方案中，需要能够将增量更新发布到已部署的数据库。 替代方法是在每次部署时重新创建数据库，这意味着会丢失现有数据库中的所有数据。 使用 Visual Studio 2010 时，建议使用 VSDBCMD 作为增量数据库发布的建议方法。 不过，下一版本的 Visual Studio 和 Web 发布管道（WPP）将包括支持直接增量发布的工具。

如果在 Visual Studio 2010 中打开联系人管理器示例解决方案，则会看到数据库项目包含一个包含四个文件的 Properties 文件夹。

![](deploying-database-projects/_static/image1.png)

与项目文件（在本例中为*ContactManager* ）一起，这些文件控制生成和部署过程的各个方面：

- *Sqlcmdvars*文件提供部署项目时使用的任何 SQLCMD 变量的值。 每个解决方案配置（例如，调试和发布）都可以指定一个不同的 sqlcmdvars 文件。
- *Sqldeployment*文件提供特定于部署的设置，例如，是使用项目中定义的排序规则还是目标服务器的排序规则，无论是每次重新创建目标数据库，还是只是修改现有数据库以使其保持最新状态等。 每个解决方案配置都可以指定一个不同的 sqldeployment 文件。
- *Sqlpermissions*文件是一个 XML 文档，可用于定义要添加到目标数据库的任何权限。 所有解决方案配置共享相同的 sqlpermissions 文件。
- *Sqlsettings*文件指定创建数据库时要使用的数据库级属性，如要使用的排序规则、比较运算符的行为，等等。 所有解决方案配置共享相同的 sqlsettings 文件。

值得一段时间在 Visual Studio 中打开这些文件并熟悉内容。

生成数据库项目时，生成过程将创建两个文件：

- *数据库架构*（.dbschema 文件）。 这将描述要以 XML 格式创建的数据库的架构。
- *部署清单*（deploymanifest 文件）。 这包含创建和部署数据库所需的所有信息。 它引用 .dbschema 文件以及其他资源，例如部署说明（sqldeployment 文件）和任何预先部署或后期部署 SQL 脚本。

这会显示这些资源之间的关系：

![](deploying-database-projects/_static/image2.png)

如您所见，sqlsettings 文件和 sqlpermissions 文件是生成过程的输入。 除了数据库项目文件，这些文件用于创建数据库架构文件。 Sqldeployment 文件和 sqlcmdvars 文件通过了不变的生成过程。 部署清单指示数据库架构的位置、sqldeployment 文件、sqlcmdvars 文件以及任何预先部署或后期部署 SQL 脚本。

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>为什么使用 VSDBCMD 部署数据库项目？

可以通过多种不同的方法来部署数据库项目。 但是，并不是所有它们都适用于将数据库项目部署到企业环境中的远程服务器。 考虑数据库项目部署的所需内容。 在企业部署方案中，您可能需要：

- 能够从远程位置部署数据库项目。
- 能够对现有数据库进行增量更新。
- 包括预先部署脚本或后期部署脚本的功能。
- 为多个目标环境定制部署的能力。
- 将数据库项目部署为更大的、通常已编写脚本的单步解决方案部署的一部分。

可以使用以下三种主要方法来部署数据库项目：

- 你可以在 Visual Studio 2010 中将部署功能与数据库项目类型一起使用。 在 Visual Studio 2010 中生成和部署数据库项目时，部署过程使用部署清单来生成特定于生成配置的基于 SQL 的部署文件。 如果数据库尚不存在，则将创建数据库，如果数据库已存在，则将对其进行必要的更改。 可以使用 SQLCMD 在目标服务器上运行此文件，也可以设置 Visual Studio 来创建和运行文件。 此方法的缺点是，你只对部署设置的控制受到限制。 你可能还需要修改 SQL 部署文件以提供特定于环境的变量值。 你只能在安装了 Visual Studio 2010 的计算机上使用此方法，开发人员需要了解并提供适用于所有目标环境的连接字符串和凭据。
- 您可以使用 Internet Information Services （IIS） Web 部署工具（Web 部署）将[数据库部署为 Web 应用程序项目的一部分](https://msdn.microsoft.com/library/dd465343.aspx)。 但是，如果你想要部署数据库项目而不是只是复制目标服务器上的现有本地数据库，则此方法要复杂得多。 您可以将 Web 部署配置为运行数据库项目生成的 SQL 部署脚本，但为了实现此目的，您需要为 Web 应用程序项目创建自定义 WPP 目标文件。 这会增加部署过程的复杂程度。 此外，Web 部署不直接支持对现有数据库进行增量更新。 有关此方法的详细信息，请参阅[将 Web 发布管道扩展到包数据库项目部署的 SQL 文件](https://go.microsoft.com/?linkid=9805121)。
- 您可以使用 VSDBCMD 实用程序来部署数据库，方法是使用数据库架构还是部署清单。 可以从 MSBuild 目标调用 VSDBCMD，这使你可以在更大的脚本化部署过程中发布数据库。 你可以从 VSDBCMD 命令重写 sqlcmdvars 文件中的变量和其他许多数据库属性，这使你可以针对不同的环境自定义部署，而无需创建多个生成配置。 VSDBCMD 提供了与众不同的功能，这意味着它将仅进行必要的更改，使目标数据库与你的数据库架构相一致。 VSDBCMD 还提供了各种命令行选项，使你可以精细地控制部署过程。

从此概述中，你可以看到，将 VSDBCMD 与 MSBuild 结合使用最适合于典型的企业部署方案：

|  | Visual Studio 2010 | Web 部署 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| 是否支持远程部署？ | 是 | 是 | 是 |
| 支持增量更新？ | 是 | No | 是 |
| 支持预先部署/后期部署脚本？ | 是 | 是 | 是 |
| 支持多环境部署？ | 有限 | 有限 | 是 |
| 支持脚本部署？ | 有限 | 是 | 是 |

本主题的其余部分介绍了如何将 VSDBCMD 与 MSBuild 结合使用来部署数据库项目。

## <a name="understanding-the-deployment-process"></a>了解部署过程

使用 VSDBCMD 实用工具，可以使用数据库架构（.dbschema 文件）或部署清单（deploymanifest 文件）来部署数据库。 在实践中，你几乎始终使用部署清单，因为部署清单允许你为各种部署属性提供默认值，并确定要运行的任何预先部署或后期部署 SQL 脚本。 例如，此 VSDBCMD 命令用于在测试环境中将**ContactManager**数据库部署到数据库服务器：

[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]

这种情况下：

- **/A** （或 **/Action**）开关指定要 VSDBCMD 执行的操作。 你可以将其设置为 "**导入**" 或 "**部署**"。 **导入**选项用于基于现有数据库生成 .dbschema 文件，"**部署**" 选项用于将 .dbschema 文件部署到目标数据库。
- **/Manifest** （或 **/ManifestFile**）开关标识你想要部署的 deploymanifest 文件。 如果要改为使用 .dbschema 文件，请使用 **/model** （或 **/ModelFile**）开关。
- **/Cs** （或 **/ConnectionString**）开关提供目标数据库服务器的连接字符串。 请注意，这不包括连接到服务器以&#x2014;创建数据库所需的数据库 VSDBCMD 的名称;不需要连接到单个数据库。 如果你的 deploymanifest 文件包含一个连接字符串，则可以省略此开关。 如果仍使用此开关，则开关值将覆盖. deploymanifest 值。
- <strong>/P： TargetDatabase</strong>属性提供要在创建时分配给目标数据库的名称。 这会重写 deploymanifest 文件中的<strong>TargetDatabase</strong>属性的值。 您可以使用<strong>/p：</strong> <em>[property name]</em>语法来设置各种部署属性，并覆盖在 sqlcmdvars 文件中声明的任何 SQLCMD 变量。
- **/Dd +** （或 **/DeployToDatabase +** ）开关指示你要创建部署并将其部署到目标环境。 如果指定 **/dd-** 或省略开关，VSDBCMD 将生成部署脚本，但不会将其部署到目标环境。 此开关通常会造成混淆，下一部分将对此进行更详细的介绍。
- **/Script** （或 **/DeploymentScriptFile**）开关指定要在何处生成部署脚本。 此值不影响部署过程。

有关 VSDBCMD 的详细信息，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)和[如何：使用 VSDBCMD 从命令提示符准备要部署的数据库。EXE](https://msdn.microsoft.com/library/dd193258.aspx)。

有关如何在 MSBuild 项目文件中使用 VSDBCMD 的示例，请参阅[了解生成过程](understanding-the-build-process.md)。 有关如何为多个环境配置数据库部署设置的示例，请参阅[自定义多个环境的数据库](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)部署。

## <a name="understanding-the-deploytodatabase-switch"></a>了解 DeployToDatabase 开关

**/Dd**或 **/DeployToDatabase**开关的行为取决于是否对 .dbschema 文件或 deploymanifest 文件使用 VSDBCMD。 如果使用的是 .dbschema 文件，则行为相当简单：

- 如果指定 **/dd +** 或 **/Dd**，则 VSDBCMD 将生成部署脚本并部署数据库。
- 如果指定 **/dd-** 或省略开关，则 VSDBCMD 将仅生成部署脚本。

如果使用的是 deploymanifest 文件，则行为会更复杂一些。 这是因为，deploymanifest 文件包含属性名称**DeployToDatabase** ，该属性还可确定是否部署了数据库。

[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]

根据数据库项目的属性设置此属性的值。 如果将 "**部署" 操作**设置为 "**创建部署脚本（.sql）** "，则此值将为**False**。 如果将 "**部署" 操作**设置为 "**创建部署脚本（.sql）" 并将其部署到数据库**，则值为**True**。

> [!NOTE]
> 这些设置与特定的生成配置和平台相关联。 例如，如果你配置了 "**调试**" 配置的设置，然后使用 "**发布**" 配置发布，则将不使用你的设置。

![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> 在此方案中，应始终将 "**部署" 操作**设置为**创建部署脚本（.sql）** ，因为您不希望 Visual Studio 2010 部署您的数据库。 换言之， **DeployToDatabase**属性应始终为**False**。

指定**DeployToDatabase**属性后，如果属性值为**false**，则 **/dd**开关将仅重写属性：

- 如果**DeployToDatabase**属性为**False**，并且指定了 **/dd +** 或 **/dd**，则 VSDBCMD 将覆盖**DeployToDatabase**属性并部署数据库。
- 如果**DeployToDatabase**属性为**False**，则指定 **/dd-** 或省略开关时，VSDBCMD 将不会部署数据库。
- 如果**DeployToDatabase**属性为**True**，则 VSDBCMD 将忽略此开关并部署数据库。
- 不管是否也要部署数据库，都将在每种情况下生成一个部署脚本。

## <a name="conclusion"></a>结束语

本主题概述了 Visual Studio 2010 中数据库项目的生成和部署过程。 还介绍了如何将 VSDBCMD 与 MSBuild 结合使用来支持企业规模的数据库部署。

有关如何在实践中工作的详细信息，请参阅[自定义多个环境的数据库部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。

## <a name="further-reading"></a>其他阅读材料

若要了解如何通过为每个环境创建单独的部署配置文件来自定义数据库部署，请参阅[自定义多个环境的数据库部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。 有关如何通过运行后期部署脚本来配置数据库角色成员身份的指导，请参阅将[数据库角色成员身份部署到测试环境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 有关管理成员资格数据库所施加的一些独特挑战的指导，请参阅[将成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

MSDN 上的这些主题提供了有关 Visual Studio 数据库项目和数据库部署过程的更广泛的指导和背景信息：

- [Visual Studio 2010 SQL Server 数据库项目](https://msdn.microsoft.com/library/ff678491.aspx)
- [管理数据库更改](https://msdn.microsoft.com/library/aa833404.aspx)
- [如何：使用 VSDBCMD 从命令提示符准备要部署的数据库.EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [数据库生成和部署概述](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-web-packages.md)
> [下一页](creating-and-running-a-deployment-command-file.md)
