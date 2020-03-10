---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 配置团队生成部署的权限 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置权限以使生成服务器能够将内容部署到 web 服务器和数据库服务器，作为自动 b 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518504"
---
# <a name="configuring-permissions-for-team-build-deployment"></a>配置团队生成部署权限

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置权限以使生成服务器能够将内容部署到 web 服务器和数据库服务器，作为自动生成过程的一部分。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

安装 Team Foundation Server （TFS）2010生成服务时，请指定要用于运行服务的标识。 默认情况下，这是 "网络服务" 帐户。 或者，您可以将生成服务配置为使用域帐户运行。

需要 Windows 身份验证的任何部署任务以及计划使用 Team Build 自动执行的部署任务将使用生成服务标识运行。 因此，你需要向生成服务标识授予对 web 服务器和数据库服务器所需的任何权限。

> [!NOTE]
> 网络服务帐户使用计算机帐户向其他计算机进行身份验证。 计算机帐户采用 * [域名] 格式\[计算机名称] * **$** &#x2014;例如**FABRIKAM\TFSBUILD $** 。 同样，如果你的生成服务使用网络服务标识运行，则应将任何所需的权限授予你的生成服务器的计算机帐户标识。

## <a name="configuring-web-server-permissions"></a>配置 Web 服务器权限

如[选择正确的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)中所述，如果要将 web 包部署到远程 web 服务器，可以使用以下两种主要方法：

- 通过在目标服务器上以*Web 部署代理服务*（也称为远程代理）为目标来部署应用程序。
- 通过将目标服务器上的*Internet Information Services* （*IIS） Web 部署处理程序*作为目标来从远程位置部署应用程序。

在这种情况下，远程代理有两个主要限制：

- 远程代理仅支持 NTLM 身份验证。 换句话说，部署必须使用生成服务标识&#x2014;，而不能模拟其他帐户。
- 若要使用远程代理，执行部署的帐户必须是目标服务器上的管理员。

同时，这两种限制使得远程代理方法不适合自动团队生成部署。 若要使用此方法，您需要使生成服务帐户成为任何目标 web 服务器上的管理员。

与此相反，Web 部署处理程序方法具有以下优点：

- Web 部署处理程序支持通过 HTTPS 进行的基本身份验证，这允许你将备用帐户的凭据传递到 IIS Web 部署工具（Web 部署）。
- 你可以配置目标 web 服务器以允许非管理员用户使用 Web 部署处理程序将内容部署到特定的 IIS 网站。

因此，当你从 Team Build 自动部署 Web 包时，最好将 Web 部署处理程序设定为目标。 建议采用以下过程：

1. 创建低特权域帐户以用于部署。
2. 配置 Web 部署处理程序，并向帐户授予向特定 IIS 网站部署内容所需的权限，如[配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述。
3. 调用 Web 部署，Web 部署并使用基本身份验证并提供所创建的域帐户的凭据，以执行部署。

在 "[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)" 示例解决方案中，您可以在特定于环境的项目文件中指定身份验证类型（基本或 NTLM）、Web 部署凭据和终结点地址（远程代理或 Web 部署处理程序）。 当执行项目文件时，这些值用于构建并运行 Web 部署命令。 有关详细信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

有关配置 Web 部署处理程序的详细信息（包括如何配置权限），请参阅[配置 Web 服务器以进行 Web 部署发布（Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 有关配置远程代理的详细信息，请参阅[为 Web 部署发布（远程代理）配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。

## <a name="configuring-database-server-permissions"></a>配置数据库服务器权限

若要将数据库部署到 SQL Server，你必须：

- 在 SQL Server 实例上创建部署帐户的登录名。
- 向登录名授予对 SQL Server 实例的**DBCreator**权限。
- 初始部署后，将登录名添加到目标数据库的**db\_所有者**角色。 这是必需的，因为在后续部署中，你要修改现有数据库，而不是创建新数据库。

使用 NTLM 身份验证或 SQL Server 身份验证，可以对 SQL Server 实例进行身份验证：

- 如果你使用 NTLM 身份验证，则需要向生成服务帐户授予上面所述的权限。
- 如果使用 SQL Server 身份验证，则需要将上述权限授予 SQL Server 帐户。 还需要在用于部署数据库的连接字符串中包含 SQL Server 用户名和密码。

有关如何配置数据库部署权限的分步详细信息，请参阅为[Web 部署发布配置数据库服务器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。

## <a name="conclusion"></a>结束语

此时，你应该了解当你从 Team Build 自动执行 web 应用程序和数据库部署时，所需的权限以及为你打开的身份验证选项。 还应能够在 IIS web 服务器和 SQL Server 数据库服务器上实现所需的权限。

## <a name="further-reading"></a>其他阅读材料

有关配置 Windows server 环境以支持远程部署的详细信息，请参阅[为 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](deploying-a-specific-build.md)
