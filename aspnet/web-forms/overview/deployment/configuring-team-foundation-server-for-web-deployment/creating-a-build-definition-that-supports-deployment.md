---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 创建支持部署的生成定义 |Microsoft Docs
author: jrjlee
description: 如果要在 Team Foundation Server （TFS）2010中执行任何类型的生成，则需要在团队项目中创建生成定义。 本主题 des 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489008"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a>创建支持部署的生成定义

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 如果要在 Team Foundation Server （TFS）2010中执行任何类型的生成，则需要在团队项目中创建生成定义。 本主题介绍如何在 TFS 中创建新的生成定义，以及如何在 Team Build 中作为生成过程的一部分来控制 web 部署。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中描述的拆分项目文件方法，其中，生成和部署过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含环境特定的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

生成定义是控制 TFS 中团队项目的生成方式和时间的机制。 每个生成定义指定：

- 要生成的项，如 Visual Studio 解决方案文件或自定义 Microsoft 生成引擎（MSBuild）项目文件。
- 确定生成应发生的条件的条件，如手动触发器、持续集成（CI）或封闭签入。
- 团队生成应将生成输出发送到的位置，包括部署项目，例如 web 包和数据库脚本。
- 应保留每个生成的时间量。
- 生成过程的各种其他参数。

> [!NOTE]
> 有关生成定义的详细信息，请参阅[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。

本主题将演示如何创建使用 CI 的生成定义，以便在开发人员签入新内容时触发生成。 如果生成成功，则生成服务运行自定义项目文件以将解决方案部署到测试环境。

触发生成时，需要执行以下操作：

- 首先，团队构建应生成解决方案。 作为此过程的一部分，团队生成将调用 Web 发布管道（WPP）以生成解决方案中每个 web 应用程序项目的 web 部署包。 Team Build 还将运行与解决方案关联的所有单元测试。
- 如果解决方案生成失败，则团队生成不需要进一步操作。 应将单元测试失败视为生成失败。
- 如果解决方案生成成功，则团队生成应运行控制解决方案部署的自定义项目文件。 作为此过程的一部分，Team Build 将调用 Internet Information Services （IIS） Web 部署工具（Web 部署）在目标 Web 服务器上安装打包的 web 应用程序，并且它将调用 VSDBCMD 实用工具来运行数据库创建目标数据库服务器上的脚本。

这说明了该过程：

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案包含自定义的 msbuild 项目文件 *，该*文件可从 msbuild 或 Team Build 中运行。 如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述，此项目文件定义了将 web 包和数据库部署到目标环境的逻辑。 此文件包含在生成和打包过程中运行的逻辑，如果该过程在 Team Build 中运行，则只保留运行的部署任务。 这是因为，当你以这种方式自动执行部署时，通常需要确保解决方案成功生成，并在部署过程开始之前通过所有单元测试。

下一节将介绍如何通过创建新的生成定义来实现此过程。

> [!NOTE]
> 在此&#x2014;过程中，单个自动过程生成、测试和部署解决方案&#x2014;可能最适合部署到测试环境。 对于过渡环境和生产环境，您很可能希望从已在测试环境中验证和验证的以前版本部署内容。 下一主题[部署特定生成](deploying-a-specific-build.md)中介绍了此方法。

### <a name="who-performs-this-procedure"></a>谁执行此过程？

通常，TFS 管理员执行此过程。 在某些情况下，开发人员团队负责人可能负责 TFS 中的团队项目集合。 若要创建新的生成定义，你必须是包含你的解决方案的团队项目集合的 "**项目集合生成管理员**" 组的成员。

## <a name="create-a-build-definition-for-ci-and-deployment"></a>创建 CI 和部署的生成定义

下一过程介绍如何创建 CI 触发的生成定义。 如果生成成功，则使用自定义 MSBuild 项目文件中的逻辑来部署解决方案。

**为 CI 和部署创建生成定义**

1. 在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，展开 "团队项目" 节点，右键单击 "**生成**"，然后单击 "**新建生成定义**"。

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. 在 "**常规**" 选项卡上，为生成定义指定一个名称（例如， **DeployToTest**）和一个可选说明。
3. 在 "**触发器**" 选项卡上，选择要触发新生成的条件。 例如，如果想要生成解决方案并将其部署到测试环境，则每次开发人员签入新代码时，请选择 "**持续集成**"。
4. 在 "**生成默认值**" 选项卡上的 "**将生成输出复制到以下放置文件夹**" 框中，键入放置文件夹的通用命名约定（UNC）路径（例如 **\\TFSBUILD\Drops**）。

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > 此放置位置存储多个版本，具体取决于你配置的保留策略。 如果要将部署项目从特定生成发布到过渡环境或生产环境，可在此处找到这些项目。
5. 在 "**进程**" 选项卡上的 "**生成过程文件**" 下拉列表中，选择 " **defaulttemplate.11.1.xaml** "。 这是添加到所有新团队项目的默认生成过程模板之一。
6. 在 "**生成过程参数**" 表中，单击 "**要生成的项**" 行，然后单击**省略号**按钮。

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. 在 "**要生成的项**" 对话框中，单击 "**添加**"。
8. 浏览到解决方案文件的位置，然后单击 **"确定"** 。

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. 在 "**要生成的项**" 对话框中，单击 "**添加**"。
10. 在 "**项类型**" 下拉列表中，选择 " **MSBuild 项目文件**"。
11. 浏览到用于控制部署过程的自定义项目文件的位置，选择该文件，然后单击 **"确定"** 。

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. "**要生成的项**" 对话框现在应显示两个项。 单击“确定”。

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. 在 "**进程**" 选项卡上的 "**生成过程参数**" 表中，展开 "**高级**" 部分。
14. 在 " **MSBuild 参数**" 行中，添加要*生成的任何*项所需的 MSBuild 命令行参数。 在 Contact Manager 解决方案方案中，需要以下参数：

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. 在此示例中：

    1. 当你生成联系人管理器解决方案时， **DeployOnBuild = true**和**DeployTarget = package**参数是必需的。 这会指示 MSBuild 在生成每个 web 应用程序项目后创建 web 部署包，如[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中所述。
    2. 当你生成*Publish*文件时， **TargetEnvPropsFile**参数是必需的。 此属性指示特定于环境的配置文件的位置，如[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述。
16. 在 "**保留策略**" 选项卡上，根据需要配置要保留的每种类型的生成数。
17. 单击“保存”。

## <a name="queue-a-build"></a>将生成排入队列

此时，您已创建了至少一个新的生成定义。 你定义的生成过程现在将根据你在生成定义中指定的触发器运行。

如果已将生成定义配置为使用 CI，则可以通过两种方式来测试生成定义：

- 将某些内容签入到团队项目以触发自动生成。
- 手动对生成进行排队。

**手动对生成进行排队**

1. 在 "**团队资源管理器**" 窗口中，右键单击生成定义，然后单击 "使**新生成入队**"。

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. 在 "**队列生成**" 对话框中，查看 "生成属性"，然后单击 "**队列**"。

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

若要查看生成&#x2014;的进度和结果，而不考虑是否手动触发，或者在 "&#x2014;**团队资源管理器**" 窗口中自动双击生成定义。 这将打开 "**生成资源管理器**" 选项卡。

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

在这里，你可以对失败的生成进行故障排除。 如果双击单个生成，则可以查看摘要信息，并单击 "到详细日志文件"。

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

您可以使用此信息对失败的生成进行故障排除并解决所有问题，然后再尝试其他生成。

> [!NOTE]
> 在您向生成服务器授予目标环境中所需的任何权限之前，执行部署逻辑的生成可能会失败。 有关详细信息，请参阅[配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)。

## <a name="monitor-the-build-process"></a>监视生成过程

TFS 提供范围广泛的功能，可帮助您监视生成过程。 例如，TFS 可以在生成完成时向你发送电子邮件，或在任务栏通知区域中显示警报。 有关详细信息，请参阅[运行和监视生成](https://msdn.microsoft.com/library/ms181721.aspx)。

## <a name="conclusion"></a>结束语

本主题介绍了如何在 TFS 中创建生成定义。 生成定义是为 CI 配置的，因此每当开发人员将内容签入到团队项目时，生成过程都将运行。 生成定义执行自定义 MSBuild 项目文件，以将 web 包和数据库脚本部署到目标服务器环境。

为了使自动部署在生成过程中成功，您需要向目标 web 服务器和目标数据库服务器上的生成服务帐户授予适当的权限。 本教程中的最后一个主题是[配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)，介绍如何识别和配置从 Team build server 进行自动部署所需的权限。

## <a name="further-reading"></a>其他阅读材料

有关创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)和[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。 有关如何对生成进行排队的详细指南，请参阅对[生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。

> [!div class="step-by-step"]
> [上一页](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一页](deploying-a-specific-build.md)
