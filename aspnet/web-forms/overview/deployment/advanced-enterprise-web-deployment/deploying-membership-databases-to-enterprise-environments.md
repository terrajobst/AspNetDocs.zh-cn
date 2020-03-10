---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: 将成员资格数据库部署到企业环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍在设置 ASP.NET 应用程序服务数据库时需要解决的关键注意事项和挑战（更常见 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 50f49af502b75aa5ad52756a76a5e7340aca53f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422156"
---
# <a name="deploying-membership-databases-to-enterprise-environments"></a>将成员身份数据库部署到企业环境

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍在测试、过渡或生产环境中设置 ASP.NET 应用程序服务数据库（更常见的称为成员资格数据库）时需要解决的关键注意事项和挑战。 还介绍了可用于解决这些难题的方法。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>部署成员资格数据库时的问题是什么？

在大多数情况下，设计数据库的部署策略时，需要考虑的第一件事是要部署的数据。 在开发或测试环境中，你可能想要部署用户帐户数据以便快速轻松地进行测试。 在过渡环境或生产环境中，您不太可能需要部署用户帐户数据。

遗憾的是，ASP.NET 的成员资格数据库引入了一些具体的难题，这使得这一决定变得更为复杂：

- 仅限架构的部署会使成员资格数据库处于不可操作状态。 这是因为成员资格数据库包含数据库在运行时所需的一些配置数据（在**aspnet\_SchemaVersions**表中）。 因此，如果您对成员资格数据库执行仅限架构的部署以排除用户帐户数据，则需要运行部署后脚本来添加必要的配置数据。
- 根据成员资格数据库的配置方式，成员资格提供程序可以使用计算机密钥来加密密码，并将其存储在数据库中。 在这种情况下，使用数据库部署的任何用户帐户数据在目标服务器上将变为不可用。 出于此原因，不支持部署用户帐户数据。

## <a name="choosing-a-membership-database-strategy"></a>选择成员资格数据库策略

当你选择如何在企业服务器环境中设置成员资格数据库时，请使用以下准则：

- 如果可能，请不要部署成员资格数据库。 而应在目标数据库服务器上手动创建成员资格数据库。 如果尚未自定义成员资格数据库架构，只需使用[ASP.NET SQL Server 注册工具（aspnet\_regsql）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)在目标的原位中创建一个新的架构。
- 例如，如果您没有选项，而是部署成员&#x2014;资格数据库（例如，如果您对数据库架构&#x2014;进行了大量修改，则应执行成员资格数据库的仅限架构的部署，排除用户帐户数据，然后运行部署后脚本以添加任何所需的配置数据。 您可以在[如何：部署 ASP.NET 成员资格数据库，而无需包含用户帐户](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)中找到有关这些方法的广泛指导。

请务必记住，*成员资格数据库的架构可能是相当静态*的。 即使您已自定义成员资格数据库，也不太可能需要定期更新架构，&#x2014;其频率与 web 应用程序或数据库项目中的代码的频率相同。 因此，您不需要在任何自动或单步部署过程中都包含成员资格数据库。

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>使用 VSDBCMD 更新成员资格数据库架构

如果在第一次部署后修改成员资格数据库的结构，则可能不希望使用 Internet Information Services （IIS） Web 部署工具（Web 部署）来重新部署数据库。 Web 部署中的数据库部署功能不包括将差异更新到目标数据库&#x2014;的功能，Web 部署必须删除并重新创建数据库。 这意味着会丢失任何现有的用户帐户数据，这通常不需要过渡或生产环境。

替代方法是使用 VSDBCMD 实用工具更新目标数据库的架构。 VSDBCMD 包括两项重要功能。 首先，它可以将现有数据库的架构导入到 .dbschema 文件中。 其次，它可以将 .dbschema 文件作为差异更新部署到现有数据库，这意味着它只会使目标数据库保持最新状态，而不会丢失任何数据。

您可以使用这些高级步骤更新成员资格数据库架构：

1. 使用 VSDBCMD**导入**操作为源成员资格数据库生成 .dbschema 文件。 [如何：从命令提示符导入架构](https://msdn.microsoft.com/library/dd172135.aspx)中介绍了此过程。
2. 使用 VSDBCMD**部署**操作将 .dbschema 文件部署到目标成员身份数据库。 [VSDBCMD 的命令行参考中介绍了此过程。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)。

## <a name="conclusion"></a>结束语

本主题介绍了需要在各种目标环境中设置 ASP.NET 成员资格数据库时可能会遇到的一些挑战。 具体而言，它解释了仅限架构的部署为何会使成员身份数据库处于非操作状态，并且不支持部署用户帐户数据。 本主题还提供了有关如何在不同方案中预配、部署和更新成员资格数据库的指南。

## <a name="further-reading"></a>其他阅读材料

有关如何使用 VSDBCMD 的更多指导和示例，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)和[如何：从命令提示符导入架构](https://msdn.microsoft.com/library/dd172135.aspx)。 有关使用 aspnet\_regsql 创建成员资格数据库的详细信息，请参阅[ASP.NET SQL Server 注册工具（aspnet\_regsql）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。 有关部署成员资格数据库的更多一般指南，请参阅[如何：部署 ASP.NET 成员资格数据库，而不包括用户帐户](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)。

> [!div class="step-by-step"]
> [上一页](deploying-database-role-memberships-to-test-environments.md)
> [下一页](excluding-files-and-folders-from-deployment.md)
