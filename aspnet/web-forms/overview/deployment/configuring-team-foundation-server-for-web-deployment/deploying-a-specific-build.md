---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 部署特定版本 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何将 web 包和数据库脚本从特定的先前版本部署到新的目标，例如过渡或生产流程图 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519572"
---
# <a name="deploying-a-specific-build"></a>部署特定生成

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何将 web 包和数据库脚本从特定的先前版本部署到新的目标，例如过渡环境或生产环境。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中描述的拆分项目文件方法，其中，生成和部署过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含环境特定的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

到目前为止，本教程集中的主题重点介绍如何在单步或自动过程中生成、打包和部署 web 应用程序和数据库。 但是，在某些常见情况下，你需要从放置文件夹中的生成列表中选择要部署的资源。 换句话说，最新的生成可能不是要部署的生成。

请考虑上一主题中所述的持续集成（CI）方案，[创建支持部署的生成定义](creating-a-build-definition-that-supports-deployment.md)。 已在 Team Foundation Server （TFS）2010中创建了生成定义。 开发人员每次将代码签入 TFS 时，团队生成将生成您的代码，创建 web 包和数据库脚本作为生成过程的一部分，运行任何单元测试，并将资源部署到测试环境。 根据你在创建生成定义时配置的保留策略，TFS 将保留特定数量的以前版本。

![](deploying-a-specific-build/_static/image1.png)

现在，假设已对测试环境中的其中一种版本执行验证和验证测试，并且已准备好将应用程序部署到过渡环境。 同时，开发人员可能已签入新代码。 不需要重新生成解决方案并将其部署到过渡环境，而不希望将最新版本部署到过渡环境。 相反，你希望部署在测试服务器上已验证并验证的特定生成。

若要实现此目的，需要告知 Microsoft 生成引擎（MSBuild），其中查找生成特定生成的 web 包和数据库脚本。

## <a name="overriding-the-outputroot-property"></a>重写 OutputRoot 属性

在[示例解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)中， *Publish*文件声明名为**OutputRoot**的属性。 顾名思义，这是包含生成过程生成的所有内容的根文件夹。 在*Publish*文件中，可以看到**OutputRoot**属性指的是所有部署资源的根位置。

> [!NOTE]
> **OutputRoot**是常用的属性名称。 视觉C#对象和 Visual Basic 项目文件也会将此属性声明为存储所有生成输出的根位置。

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

如果希望项目文件从不同的位置&#x2014;（如以前的 TFS 生成&#x2014;的输出）部署 web 包和数据库脚本，只需重写**OutputRoot**属性。 应将属性值设置为 Team Build server 上的相关生成文件夹。 如果从命令行运行 MSBuild，则可将**OutputRoot**的值指定为命令行参数：

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

但是，在实践中，如果不打算使用生成输出 ，则&#x2014;还需要跳过生成目标，而无需构建解决方案。 可以通过从命令行指定要执行的目标来执行此操作：

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

但在大多数情况下，你需要在 TFS 生成定义中生成部署逻辑。 这使具有 "**队列生成**" 权限的用户可以通过连接到 TFS 服务器来触发来自任何 Visual Studio 安装的部署。

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>创建生成定义以部署特定生成

下一过程介绍如何创建一个生成定义，使用户能够使用单个命令触发到过渡环境的部署。

在这种情况下，你不希望生成定义实际构建你&#x2014;只想在自定义项目文件中执行部署逻辑的任何内容。 如果文件在 Team Build 中运行，则*Publish*文件包含用于跳过**生成**目标的条件逻辑。 它通过计算内置的**BuildingInTeamBuild**属性来实现此功能，如果您在 Team Build 中运行项目文件，此属性将自动设置为**true** 。 因此，您可以跳过生成过程，只需运行项目文件来部署现有版本。

**创建生成定义以手动触发部署**

1. 在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，展开 "团队项目" 节点，右键单击 "**生成**"，然后单击 "**新建生成定义**"。

    ![](deploying-a-specific-build/_static/image2.png)
2. 在 "**常规**" 选项卡上，为生成定义指定一个名称（例如， **DeployToStaging**）和一个可选说明。
3. 在 "**触发器**" 选项卡上，选择 "**手动–签入" 不会触发新的生成**。
4. 在 "**生成默认值**" 选项卡上的 "**将生成输出复制到以下放置文件夹**" 框中，键入放置文件夹的通用命名约定（UNC）路径（例如 **\\TFSBUILD\Drops**）。

    ![](deploying-a-specific-build/_static/image3.png)
5. 在 "**进程**" 选项卡上的 "**生成过程文件**" 下拉列表中，选择 " **defaulttemplate.11.1.xaml** "。 这是添加到所有新团队项目的默认生成过程模板之一。
6. 在 "**生成过程参数**" 表中，单击 "**要生成的项**" 行，然后单击**省略号**按钮。

    ![](deploying-a-specific-build/_static/image4.png)
7. 在 "**要生成的项**" 对话框中，单击 "**添加**"。
8. 在 "**项类型**" 下拉列表中，选择 " **MSBuild 项目文件**"。
9. 浏览到用于控制部署过程的自定义项目文件的位置，选择该文件，然后单击 **"确定"** 。

    ![](deploying-a-specific-build/_static/image5.png)
10. 在 "**要生成的项**" 对话框中，单击 **"确定"** 。
11. 在 "**生成过程参数**" 表中，展开 "**高级**" 部分。
12. 在 " **MSBuild 参数**" 行中，指定特定于环境的项目文件的位置，并为生成文件夹的位置添加占位符：

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > 每次对生成进行排队时，需要重写**OutputRoot**值。 下一过程中会介绍这一点。
13. 单击“保存”。

触发生成时，需要更新**OutputRoot**属性，使其指向要部署的生成。

**从生成定义部署特定生成**

1. 在 "**团队资源管理器**" 窗口中，右键单击生成定义，然后单击 "使**新生成入队**"。

    ![](deploying-a-specific-build/_static/image7.png)
2. 在 "**队列生成**" 对话框中的 "**参数**" 选项卡上，展开 "**高级**" 部分。
3. 在 " **MSBuild 参数**" 行中，将**OutputRoot**属性的值替换为生成文件夹的位置。 例如:

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > 请确保在生成文件夹路径的末尾包含尾随斜杠。
4. 单击 "**队列**"。

当你对生成进行排队时，项目文件将从你在**OutputRoot**属性中指定的生成放置文件夹部署数据库脚本和 web 包。

## <a name="conclusion"></a>结束语

本主题介绍了如何使用 split 项目文件部署模型从特定的先前版本发布部署资源，如 web 包和数据库脚本。 其中介绍了如何重写**OutputRoot**属性，以及如何将部署逻辑并入 TFS 生成定义中。

## <a name="further-reading"></a>其他阅读材料

有关创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)和[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。 有关如何对生成进行排队的详细指南，请参阅对[生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。

> [!div class="step-by-step"]
> [上一页](creating-a-build-definition-that-supports-deployment.md)
> [下一页](configuring-permissions-for-team-build-deployment.md)
