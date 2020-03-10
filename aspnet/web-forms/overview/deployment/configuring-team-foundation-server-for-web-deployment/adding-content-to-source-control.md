---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 向源代码管理添加内容 |Microsoft Docs
author: jrjlee
description: 本主题说明如何在 Team Foundation Server （TFS）2010中将内容添加到源代码管理。 其中介绍了如何将解决方案和项目添加到团队项目 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515108"
---
# <a name="adding-content-to-source-control"></a>向源代码管理添加内容

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题说明如何在 Team Foundation Server （TFS）2010中将内容添加到源代码管理。 它介绍如何将解决方案和项目添加到 TFS 中的团队项目，并说明如何将外部依赖项（如框架或程序集）添加到源代码管理。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

## <a name="task-overview"></a>任务概述

在大多数情况下，开发人员团队的每个成员都应该能够向源代码管理添加内容。 若要将解决方案添加到 TFS 中的源代码管理，需要完成以下高级步骤：

- 连接到团队项目。
- 将服务器上的团队项目文件夹结构映射到本地计算机上的文件夹结构。
- 将解决方案及其内容添加到源代码管理。
- 向源代码管理添加任何外部依赖项。

本主题将演示如何执行这些过程。

本主题中的任务和演练假设已创建一个新的 TFS 团队项目来管理内容。 有关创建新团队项目的详细信息，请参阅[在 TFS 中创建团队项目](creating-a-team-project-in-tfs.md)。

### <a name="who-performs-these-procedures"></a>谁执行这些过程？

在大多数情况下，开发人员团队的每个成员都应该能够在特定团队项目中添加和修改内容。

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>连接到团队项目并创建文件夹映射

在将任何内容添加到源代码管理之前，需要连接到团队项目，并在服务器上的文件夹结构和本地计算机上的文件系统之间创建映射。

**连接到团队项目并映射本地路径**

1. 在开发人员工作站上，打开 Visual Studio 2010。
2. 在 Visual Studio 的 "**团队**" 菜单上，单击 "**连接到 Team Foundation Server**"。

    > [!NOTE]
    > 如果已配置到 TFS 服务器的连接，则可以省略步骤3-6。
3. 在 "**连接到团队项目**" 对话框中，单击 "**服务器**"。
4. 在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**添加**"。
5. 在 "**添加 Team Foundation Server** " 对话框中，提供 TFS 实例的详细信息，然后单击 **"确定"** 。

    ![](adding-content-to-source-control/_static/image1.png)
6. 在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**关闭**"。
7. 在 "**连接到团队项目**" 对话框中，选择要连接到的 TFS 实例，选择 "团队项目集合"，选择要添加到的团队项目，然后单击 "**连接**"。

    ![](adding-content-to-source-control/_static/image2.png)
8. 在 "**团队资源管理器**" 窗口中，展开你的团队项目，然后双击 "**源代码管理**"。

    ![](adding-content-to-source-control/_static/image3.png)
9. 在 "**源代码管理器**" 选项卡上，单击 "**未映射**"。

    ![](adding-content-to-source-control/_static/image4.png)
10. 在 "**映射**" 对话框中的 "**本地文件夹**" 框中，浏览到（或创建）一个本地文件夹，将其用作团队项目的根文件夹，然后单击 "**映射**"。

    ![](adding-content-to-source-control/_static/image5.png)
11. 如果系统提示你下载源文件，请单击 **"是"** 。

    ![](adding-content-to-source-control/_static/image6.png)

此时，已将团队项目的服务器端文件夹映射到开发人员工作站上的本地文件夹。 你还将团队项目中的任何现有内容下载到本地文件夹结构。 你现在可以开始将自己的内容添加到源代码管理。

## <a name="add-projects-and-solutions-to-source-control"></a>向源代码管理添加项目和解决方案

若要将项目和解决方案添加到源代码管理，首先需要将它们移到本地计算机上的团队项目的映射文件夹中。 然后，你可以签入内容以将添加的内容与服务器同步。

**向源代码管理添加项目**

1. 在开发人员工作站上，将项目和解决方案移动到团队项目的映射文件夹结构内的适当位置。

    > [!NOTE]
    > 很多组织都有一个首选方法，即如何在源代码管理中组织项目和解决方案。 有关如何构造文件夹的指导，请参阅[如何：在 Team Foundation Server 中构造源代码管理文件夹](https://msdn.microsoft.com/library/bb668992.aspx)。
2. 在 Visual Studio 2010 中打开解决方案。
3. 在 "**解决方案资源管理器**" 窗口中，右键单击解决方案，然后单击 "**将解决方案添加到源代码管理**"。

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > 在某些情况下，你可能需要将项目单独添加到源代码管理中，以便更精确地控制对源代码的组织方式，这在某些情况下，具体取决于你的组织对 TFS 中的内容进行结构控制的方式。
4. 验证 "**源代码管理器**" 选项卡是否显示已在团队项目的服务器文件夹结构中添加的内容。

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > "**源代码管理器**" 选项卡显示你的内容，而无需进一步提示，因为你已将解决方案添加到本地文件系统上的映射文件夹中。 如果你的解决方案在未映射的位置，则系统会提示你指定 TFS 和本地文件系统中的文件夹位置。
5. 在 "**源代码管理器**" 选项卡上的 "**文件夹**" 窗格中，右键单击团队项目（例如**ContactManager**），然后单击 "**签入挂起的更改**"。
6. 在 "**签入-源文件**" 对话框中，键入注释，然后单击 "**签入**"。

    ![](adding-content-to-source-control/_static/image9.png)

此时，已将解决方案添加到 TFS 中的源代码管理。

## <a name="add-external-dependencies-to-source-control"></a>向源代码管理添加外部依赖项

向源代码管理添加项目或解决方案时，还将添加项目或解决方案中的所有文件和文件夹。 但是，在很多情况下，项目和解决方案也依赖于外部依赖项（如本地程序集）才能正常工作。 你需要将任何此类资源添加到源代码管理中，以允许团队生成和开发人员团队的其他成员成功生成你的代码。

例如，联系人管理器示例解决方案的文件夹结构包含一个名为 "包" 的文件夹。 其中包含 ADO.NET 实体框架4.1 的程序集和各种支持资源。 "包" 文件夹不是 "联系人管理器" 解决方案的一部分，但是如果没有该文件夹，该解决方案将无法成功生成。 若要启用 Team Build 来生成解决方案，需要将 "包" 文件夹添加到源代码管理中。

> [!NOTE]
> 包含 "包" 文件夹的典型情况是，使用适用于 Visual Studio 2010 的 NuGet 扩展向解决方案添加实体框架或类似资源时，会发生什么情况。

**向源代码管理添加非项目内容**

1. 确保要添加的项（例如，包文件夹）位于本地文件系统的映射文件夹中的适当位置。
2. 在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，展开你的团队项目，然后双击 "**源代码管理**"。

    ![](adding-content-to-source-control/_static/image10.png)
3. 在 "**源代码管理器**" 选项卡上的 "**文件夹**" 窗格中，选择包含要添加的项的文件夹。
4. 单击 "**将项目添加到文件夹**" 按钮。

    ![](adding-content-to-source-control/_static/image11.png)
5. 在 "**添加到源代码管理**" 对话框中，选择要添加的文件夹，然后单击 "**下一步**"。

    ![](adding-content-to-source-control/_static/image12.png)
6. 在 "已**排除的项**" 选项卡上，选择已自动排除的所有必需项（例如，程序集），然后单击 "**包括项**"。

    ![](adding-content-to-source-control/_static/image13.png)
7. 在 "**要添加的项**" 选项卡上，验证是否列出了要包含的所有文件，然后单击 "**完成**"。

    ![](adding-content-to-source-control/_static/image14.png)
8. 在 "**源代码管理器**" 窗口中，单击 "**签入**" 按钮。

    ![](adding-content-to-source-control/_static/image15.png)
9. 在 "**签入-源文件**" 对话框中，键入注释，然后单击 "**签入**"。

此时，已将解决方案的外部依赖项添加到源代码管理中。

## <a name="conclusion"></a>结束语

本主题介绍了如何连接到团队项目、映射文件夹结构，以及如何将内容添加到源代码管理。 有关如何处理源代码管理下的项的详细信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。

下一主题：[配置用于 Web 部署的 Tfs 生成服务器](configuring-a-tfs-build-server-for-web-deployment.md)，介绍如何准备 Tfs Team build 服务器来构建和部署解决方案。

## <a name="further-reading"></a>其他阅读材料

有关在 TFS 中使用源代码管理的更全面的信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。

> [!div class="step-by-step"]
> [上一页](creating-a-team-project-in-tfs.md)
> [下一页](configuring-a-tfs-build-server-for-web-deployment.md)
