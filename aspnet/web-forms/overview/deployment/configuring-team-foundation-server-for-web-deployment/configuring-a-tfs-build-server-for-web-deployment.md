---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: 配置用于 Web 部署的 TFS 生成服务器 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何准备 Team Foundation Server （TFS）生成服务器，以使用 Team Build 和 Internet Informat 生成和部署解决方案。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b3aaf7234706d149a3c784347528923f662c3511
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512222"
---
# <a name="configuring-a-tfs-build-server-for-web-deployment"></a>配置用于 Web 部署的 TFS 生成服务器

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何准备 Team Foundation Server （TFS）生成服务器，以使用 Team Build 和 Internet Information Services （IIS） Web 部署工具（Web 部署）来构建和部署解决方案。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

若要准备生成服务器以构建和部署你的解决方案，你将需要：

- 安装和配置 TFS 生成服务。
- 安装 Visual Studio 2010。
- 安装生成解决方案所需的任何产品或组件，如 .NET Framework 或 ASP.NET MVC 的版本。
- 安装 Web 部署2.0 或更高版本。

本主题将演示如何执行这些过程，或指向存在的其他资源。 本主题中的任务和演练假定：

- 从运行 Windows Server 2008 R2 Service Pack 1 的干净服务器版本开始。
- 服务器已加入域，并具有静态 IP 地址。
- 你已在单独的服务器上安装了 TFS 应用程序层，如[企业 Web 部署：方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中所述。

### <a name="who-performs-these-procedures"></a>谁执行这些过程？

在大多数情况下，TFS 管理员将负责配置生成服务器。 在某些情况下，开发人员团队可能会取得特定生成服务器的所有权。

## <a name="install-and-configure-the-tfs-build-service"></a>安装和配置 TFS 生成服务

在配置生成服务器时，您的第一个任务是安装和配置 TFS 生成服务。 作为此过程的一部分，你将需要：

- 安装 TFS 生成服务并配置服务帐户。 任何生成任务（包括部署）都将使用生成服务帐户的标识运行。
- 创建一个*生成控制器*和一个或多个*生成代理*。 每个生成控制器都管理一组生成代理。 当你对生成进行排队时，生成控制器会将生成任务分配给可用的生成代理。 TFS 中的每个团队项目集合映射到一个生成控制器。
- 为生成输出配置放置文件夹。 这是一个网络共享。 任何生成输出（如 web 部署包）都将发送到放置文件夹。

MSDN 上的 "[管理 Team Foundation build](https://msdn.microsoft.com/library/ms252495.aspx) " 一章包含执行这些任务所需的所有资源：

- 有关 Team Foundation Build 的概念概述，包括生成服务、生成控制器和生成代理，请参阅[了解 Team Foundation 生成系统](https://msdn.microsoft.com/library/dd793166.aspx)。
- 有关安装和配置生成服务的信息，请参阅[配置生成计算机](https://msdn.microsoft.com/library/ms181712.aspx)。
- 有关创建生成控制器的信息，请参阅[创建和使用生成控制器](https://msdn.microsoft.com/library/ee330987.aspx)。
- 有关创建生成代理的信息，请参阅[创建和使用生成代理](https://msdn.microsoft.com/library/bb399135.aspx)。
- 有关创建和配置放置文件夹的信息，请参阅[设置放置文件夹](https://msdn.microsoft.com/library/bb778394.aspx)。

## <a name="install-required-products-and-components"></a>安装所需的产品和组件

若要使生成服务器能够生成解决方案，必须安装解决方案所需的任何产品、组件或程序集。 安装任何 web 平台组件之前，应在生成服务器上安装 Visual Studio 2010 （任何版本）。 这可确保核心 Microsoft 生成引擎（MSBuild）目标文件和 Web 发布管道（WPP）目标文件可用于生成服务。 如果计划在生成过程中部署 Web 包，Visual Studio 安装程序还应安装 Web 部署。

安装常见 web 平台组件的最佳方式是使用[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。 这可确保你安装的是每个产品的最新版本，并且它还会自动检测并安装每个产品的所有必备组件。 如果是[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案，则应使用 Web 平台安装程序来安装这些产品和组件：

- **.NET Framework 4.0**。 这是运行在此版本的 .NET Framework 上构建的应用程序所必需的。
- **Web 部署工具2.1 或更高版本**。 这会在服务器上安装 Web 部署（及其基础可执行文件）。 在此过程中，它将安装并启动 Web 部署代理服务。 此服务允许你从远程计算机部署 web 包。
- **ASP.NET MVC 3**。 这将安装运行 ASP.NET MVC 3 应用程序所需的程序集。

**安装所需的产品和组件**

1. 安装 Visual Studio 2010。 当系统提示您选择要安装的功能时，您应包括：

    1. 需要编译的任何编程语言。
    2. Visual Web Developer。 这可确保将 WPP 目标添加到生成服务器。

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010 安装完成后，请下载并安装[Visual studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) （如果安装媒体中尚未包含）。

    > [!NOTE]
    > Visual Studio 2010 Service Pack 1 解析的 bug 可阻止 MSBuild 查找 Msdeploy.exe 可执行文件。
3. 下载并启动[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。
4. 在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。
5. 在窗口左侧的导航窗格中，单击 "**框架**"。
6. 在**Microsoft .NET Framework 4** "行中，如果尚未安装 .NET Framework，请单击"**添加**"。

    > [!NOTE]
    > 可能已通过 Windows 更新安装 .NET Framework 4.0。 如果产品或组件已安装，Web 平台安装程序将通过将 "**添加**" 按钮替换为**安装**的文本来指示这一点。

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. 在**ASP.NET MVC 3 （Visual Studio 2010）** 行中，单击 "**添加**"。
8. 在导航窗格中，单击 "**服务器**"。
9. 在**Web 部署工具 2.1**行中，单击 "**添加**"。
10. 单击“安装”。 Web 平台安装程序将显示产品&#x2014;列表以及要安装的任何关联依赖关系&#x2014;，并将提示你接受许可条款。
11. 查看许可条款，如果同意条款，请单击 "**我接受**"。
12. 安装完成后，单击 "**完成**"，然后关闭 " **Web 平台安装程序 3.0** " 窗口。

> [!NOTE]
> 如果你的部署过程包括使用 VSDBCMD 或 SQLCMD 之类的工具，则需要确保在生成服务器上安装这些工具。 VSDBCMD 是一个 Visual Studio 工具，当你安装 Team Foundation Build 时，通常会将该工具添加到服务器。 SQLCMD 是 SQL Server 工具。 可以从 " [Microsoft SQL Server 2008 R2 功能包](https://go.microsoft.com/?linkid=9805134)" 页下载 "SQLCMD" 的独立版本。

## <a name="conclusion"></a>结束语

此时，生成服务器已准备好开始生成和部署 web 应用程序项目。 下一主题[创建支持部署的生成定义](creating-a-build-definition-that-supports-deployment.md)，描述如何创建和配置生成定义以控制项目的生成和部署时间和方式。

## <a name="further-reading"></a>其他阅读材料

有关使用 Team Build 的更多常规指南，请参阅[管理 Team Foundation build](https://msdn.microsoft.com/library/ms252495.aspx)。

> [!div class="step-by-step"]
> [上一页](adding-content-to-source-control.md)
> [下一页](creating-a-build-definition-that-supports-deployment.md)
