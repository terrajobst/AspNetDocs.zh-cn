---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 创建并运行部署命令文件 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何生成一个命令文件，该命令文件将允许你使用 Microsoft 生成引擎（MSBuild）项目文件作为单步执行 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514976"
---
# <a name="creating-and-running-a-deployment-command-file"></a>创建并运行部署命令文件

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何生成一个命令文件，该文件将允许使用 Microsoft 生成引擎（MSBuild）项目文件作为单步骤、可重复的过程运行部署。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;[联系人管理器](the-contact-manager-solution.md)解决方案来表示具有真实复杂性级别的 WEB 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解生成过程](understanding-the-build-process.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="process-overview"></a>流程概述

在本主题中，你将了解如何创建并运行一个命令文件，该文件使用这些项目文件来执行目标环境的可重复部署。 实质上，命令文件只需包含以下 MSBuild 命令：

- 指示 MSBuild 执行环境无关的*Publish*文件。
- 指示*Publish*文件，其中包含特定于环境的项目设置以及在何处可以找到它。

## <a name="create-an-msbuild-command"></a>创建 MSBuild 命令

如[了解生成过程](understanding-the-build-process.md)中所述，环境特定的项目*文件（例如，环境*&#x2014;特定的项目文件&#x2014;）设计为在生成时导入到与环境无关的*Publish*文件中。 这两个文件一起提供了一组完整的说明，告诉 MSBuild 如何生成和部署解决方案。

*Publish*文件使用**import**元素导入特定于环境的项目文件。

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

因此，当你使用 Msbuild.exe 生成并部署 Contact Manager 解决方案时，你需要：

- 在*Publish*文件上运行 msbuild.exe。
- 通过提供名为**TargetEnvPropsFile**的命令行参数来指定环境特定的项目文件的位置。

为此，MSBuild 命令应如下所示：

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

从这里开始，这是一个简单的步骤，可以将其迁移到可重复的单步部署。 只需将 MSBuild 命令添加到 .cmd 文件即可。 在 "联系人管理器" 解决方案中，"发布" 文件夹包含一个名为 "Publish-Dev" 的文件，该文件执行此*命令*。

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> **/Fl**开关指示 msbuild 在调用 msbuild.exe 的工作目录中创建一个名为*msbuild.exe*的日志文件。

若要部署或重新部署 Contact Manager 解决方案，只需运行*Publish-Dev*文件。 运行该文件时，MSBuild 将：

- 生成解决方案中的所有项目。
- 为 web 应用程序项目生成可部署的 web 包。
- 为数据库项目生成 .dbschema 和 deploymanifest 文件。
- 将 web 包部署到 web 服务器。
- 将数据库部署到数据库服务器。

## <a name="run-the-deployment"></a>运行部署

为目标环境创建了命令文件后，只需运行该文件就能完成整个部署。

**将 Contact Manager 解决方案部署到测试环境**

1. 在开发人员工作站上，打开 Windows 资源管理器，然后浏览到*Publish-Dev*文件的位置。
2. 双击该文件以运行该文件。
3. 如果出现 "**打开文件–安全警告**" 对话框，请单击 "**运行**"。
4. 如果正确设置了配置设置和测试服务器，则 "命令提示符" 窗口将在 MSBuild 完成项目文件处理后显示 "**生成成功**" 消息。

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. 如果这是你第一次将解决方案部署到此环境中，则需要将测试 web 服务器计算机帐户添加到**ContactManager**数据库上**db\_datawriter**和**db\_datareader**角色。 为[Web 部署发布配置数据库服务器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)中介绍了此过程。

    > [!NOTE]
    > 仅需在创建数据库时分配这些权限。 默认情况下，生成过程将不会在每次部署&#x2014;时重新创建数据库，而是将现有数据库与最新架构进行比较，并仅进行所需的更改。 因此，在首次部署解决方案时，只需映射这些数据库角色。
6. 打开 Internet Explorer 并浏览到联系人管理器应用程序的 URL （例如 `http://testweb1:85/ContactManager/`）。
7. 验证应用程序是否按预期工作，以及是否能够添加联系人。

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>结束语

通过创建包含 MSBuild 说明的命令文件，可以快速轻松地构建多项目解决方案并将其部署到特定目标环境。 如果需要反复将解决方案部署到多个目标环境，可以创建多个命令文件。 在每个命令文件中，MSBuild 命令将生成相同的通用项目文件，但它会指定其他特定于环境的项目文件。 例如，要发布到开发人员或测试环境的命令文件可能包含以下 MSBuild 命令：

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

要发布到过渡环境的命令文件可能包含以下 MSBuild 命令：

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> 有关如何为自己的服务器环境自定义特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

还可以通过在 MSBuild 命令中重写属性或设置各种其他开关，为每个环境自定义生成过程。 有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。

> [!div class="step-by-step"]
> [上一页](deploying-database-projects.md)
> [下一页](manually-installing-web-packages.md)
