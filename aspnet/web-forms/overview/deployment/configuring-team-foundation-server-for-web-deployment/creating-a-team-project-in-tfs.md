---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: 在 TFS 中创建团队项目 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在 Team Foundation Server （TFS）2010中创建新的团队项目。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519560"
---
# <a name="creating-a-team-project-in-tfs"></a>在 TFS 中创建团队项目

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何在 Team Foundation Server （TFS）2010中创建新的团队项目。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

## <a name="task-overview"></a>任务概述

若要预配和使用 TFS 中的新团队项目，需要完成以下高级步骤：

- 向将创建新团队项目的用户授予权限。
- 创建团队项目。
- 向将处理项目的团队成员授予权限。
- 签入某些内容。

本主题将演示如何执行这些过程，并将确定可能负责每个过程的用户和作业角色。 请注意，根据你的组织的结构，每个任务都可能是不同人员的责任。

本主题中的任务和演练假定您已安装并配置 TFS，并且您已在配置过程中创建了一个团队项目集合。 有关这些假设的详细信息，以及有关该方案的更多常规背景信息，请参阅为[Web 部署配置 TFS 生成服务器](configuring-a-tfs-build-server-for-web-deployment.md)。

## <a name="grant-permissions-to-the-team-project-creator"></a>向团队项目创建者授予权限

若要创建新的团队项目，你需要具备以下权限：

- 您必须具有 TFS 应用程序层上的 "**创建新项目**" 权限。 通常通过将用户添加到 "**项目集合管理员**" TFS 组来授予此权限。 **Team Foundation Administrators**全局组还包括此权限。
- 您必须有权在与 TFS 团队项目集合相对应的 SharePoint 网站集内创建新的团队网站。 通常通过将用户添加到对 SharePoint 网站集具有**完全控制**权限的 sharepoint 组来授予此权限。
- 如果使用 SQL Server Reporting Services 功能，则必须是 Reporting Services 中的 " **Team Foundation 内容管理员**" 角色的成员。

### <a name="who-performs-these-procedures"></a>谁执行这些过程？

通常，管理 TFS 部署的人员或组也会执行这些过程。

由于这是一个具有高特权的权限集，因此新团队项目通常由一小部分用户创建，负责管理 TFS 部署。 通常不会向开发人员授予创建新团队项目所需的权限。

### <a name="grant-permissions-in-tfs"></a>在 TFS 中授予权限

如果要使用户能够创建新的团队项目，则第一个高级任务是将用户添加到团队项目集合的 "**项目集合管理员**" 组。

**将用户添加到 "项目集合管理员" 组**

1. 在 TFS 服务器上的 "**开始**" 菜单中，指向 "**所有程序**"，单击**Microsoft Team Foundation Server 2010**"，然后单击" **Team Foundation 管理控制台**"。
2. 在导航树视图中，展开 "**应用层**"，然后单击 "**团队项目集合**"。

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. 在 "**团队项目集合**" 窗格中，选择要管理的团队项目集合。

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. 在 "**常规**" 选项卡上，单击 "**组成员身份**"。

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. 在 "**全局组**" 对话框中，选择 "**项目集合管理员**" 组，然后单击 "**属性**"。
6. 在 " **Team Foundation Server 组属性**" 对话框中，选择 " **Windows 用户或组**"，然后单击 "**添加**"。

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. 在 "**选择用户、计算机或组**" 对话框中，键入你希望能够创建新团队项目的用户的用户名，单击 "**检查名称**"，然后单击 **"确定"** 。

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. 在**Team Foundation Server 组属性**"对话框中，单击 **" 确定 "** 。
9. 在 "**全局组**" 对话框中，单击 "**关闭**"。

### <a name="grant-permissions-in-sharepoint-services"></a>在 SharePoint Services 中授予权限

接下来，您需要授予用户在与 TFS 团队项目集合对应的 SharePoint 网站集中创建新团队网站的权限。

**授予对 SharePoint 网站集的 "完全控制" 权限**

1. 在 Team Foundation Server 管理控制台的 "**团队项目集合**" 页上，选择要管理的团队项目集合。
2. 在 " **SharePoint 站点**" 选项卡上，记下 "**当前默认站点位置**URL" 的值。

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. 打开 Internet Explorer，然后前往步骤2中记下的 URL。

    > [!NOTE]
    > 如果你未以创建团队项目集合的用户身份登录到 Windows，则需要以此用户身份登录到 SharePoint 以便继续。
4. 在 **“网站操作”** 菜单上，单击 **“网站设置”** 。

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. 在 "**站点设置**" 页上的 "**用户和权限**" 下，单击 "**人员和组**"。
6. 在左侧导航面板中，单击 "**组**"。

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. 在 "**用户和组：所有组**" 页上，单击 "**为此站点设置组**"。

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > 由于双 HTTP 编码错误，你可能会收到 "<strong>找不到 http 404</strong> " 错误。 如果出现这种情况，请将 URL 替换为：   
   > `[site_collection_URL]/_layouts/permsetup.aspx` 例如：  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. 在 "**为此站点设置组**" 页上，将创建团队项目的用户添加到 "**所有者**" 组，然后单击 **"确定"** 。

    ![](creating-a-team-project-in-tfs/_static/image10.png)

有关使用户能够在团队项目集合中创建新团队项目的详细信息，请参阅[为团队项目集合设置管理员权限](https://msdn.microsoft.com/library/dd547204.aspx)。

## <a name="create-a-new-team-project-and-add-users"></a>创建新的团队项目并添加用户

获得必要的权限后，可以使用 Visual Studio 2010 中的 "**团队资源管理器**" 窗口创建新的团队项目。 此方法提供了一个向导，该向导收集所有必需的信息，并在 TFS、SharePoint 和 SQL Server Reporting Services 中执行必要的任务。 还需要向开发人员团队成员授予对新团队项目的权限，以使他们能够添加和修改内容。

### <a name="who-performs-these-procedures"></a>谁执行这些过程？

通常，TFS 管理员或开发人员团队负责人会执行这些过程。

### <a name="create-a-new-team-project"></a>创建新的团队项目

下一过程介绍如何在 TFS 2010 中创建新的团队项目。

**创建新的团队项目**

1. 在 "**开始**" 菜单上，指向 "**所有程序**"，单击**Microsoft Visual Studio 2010**，右键单击**Microsoft Visual Studio 2010**"，然后单击" 以**管理员身份运行**"。

    > [!NOTE]
    > 如果不以管理员身份运行 Visual Studio 2010，则 "新建团队项目向导" 将在上一步中失败。
2. 如果此时出现 **“用户帐户控制”** 对话框，请单击 **“是”** 。
3. 在 Visual Studio 的 "**团队**" 菜单上，单击 "**连接到 Team Foundation Server**"。

    > [!NOTE]
    > 如果已配置到 TFS 服务器的连接，则可以省略步骤4-7。
4. 在 "**连接到团队项目**" 对话框中，单击 "**服务器**"。
5. 在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**添加**"。
6. 在 "**添加 Team Foundation Server** " 对话框中，提供 TFS 实例的详细信息，然后单击 **"确定"** 。

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. 在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**关闭**"。
8. 在 "**连接到团队项目**" 对话框中，选择要连接到的 TFS 实例，选择要添加到的团队项目集合，然后单击 "**连接**"。

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. 在 "**团队资源管理器**" 窗口中，右键单击团队项目集合，然后单击 "**新建团队项目**"。

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. 在 "**新建团队项目**" 对话框中，为团队项目提供名称和说明，然后单击 "**下一步**"。

    > [!NOTE]
    > 如果你的团队项目包含空格，则当你使用 Internet Information Services （IIS） Web 部署工具（Web 部署）从输出路径部署包时可能会遇到一些问题。 路径中的空格会使运行 Web 部署命令变得更加困难。

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. 在 "**选择过程模板**" 页上，选择要用于管理开发过程的过程模板，然后单击 "**下一步**"。

    > [!NOTE]
    > 有关 TFS 过程模板的详细信息，请参阅[过程模板和工具](https://msdn.microsoft.com/vstudio/aa718795)。
12. 在 "**团队网站设置**" 页上，保持默认设置不变，然后单击 "**下一步**"。
13. 此设置创建或标识与 TFS 团队项目关联的 SharePoint 团队网站。 你的开发团队可以使用此网站来管理文档、参与讨论线索、创建 wiki 页，以及执行与代码无关的其他任务。 有关详细信息，请参阅[SharePoint 产品与 Team Foundation Server 之间的交互](https://msdn.microsoft.com/library/ms253177.aspx)。
14. 在 "**指定源代码管理设置**" 页上，保持默认设置不变，然后单击 "**下一步**"。
15. 此设置在 TFS 文件夹层次结构中标识或创建将充当内容根文件夹的位置。
16. 在 "**确认团队项目设置**" 页上，单击 "**完成**"。
17. 成功创建新团队项目后，在 "**团队项目创建**" 页上，单击 "**关闭**"。

### <a name="add-users-to-a-team-project"></a>将用户添加到团队项目

现在，你已创建新的团队项目，你可以向用户授予权限，使其能够开始添加和合作内容。

**将用户添加到团队项目**

1. 在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，右键单击团队项目，指向 "**团队项目设置**"，然后单击 "**组成员资格**"。

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. 若要使用户能够添加、修改和删除源代码管理下的代码，你需要将其添加到 "**参与者**" 组。
3. 在 "**项目组**" 对话框中，选择 "**参与者**" 组，然后单击 "**属性**"。

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. 在 " **Team Foundation Server 组属性**" 对话框中，选择 " **Windows 用户或组**"，然后单击 "**添加**"。

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. 在 "**选择用户、计算机或组**" 对话框中，键入要添加到团队项目的用户的用户名，单击 "**检查名称**"，然后单击 **"确定"** 。

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. 在**Team Foundation Server 组属性**"对话框中，单击 **" 确定 "** 。
7. 在 "**项目组**" 对话框中，单击 "**关闭**"。

## <a name="conclusion"></a>结束语

此时，你的新团队项目可以使用，并且你的开发人员团队可以开始添加内容并在开发过程中进行协作。

下一主题[将内容添加到源代码管理](adding-content-to-source-control.md)中介绍了如何将内容添加到源代码管理。

## <a name="further-reading"></a>其他阅读材料

若要更广泛地了解如何在 TFS 中创建团队项目，请参阅[创建团队项目](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)。 有关使用户能够在团队项目集合中创建新团队项目的详细信息，请参阅[为团队项目集合设置管理员权限](https://msdn.microsoft.com/library/dd547204.aspx)。 有关将用户添加到团队项目的详细信息，请参阅[将用户添加到团队项目](https://msdn.microsoft.com/library/bb558971.aspx)。

> [!div class="step-by-step"]
> [上一页](configuring-team-foundation-server-for-web-deployment.md)
> [下一页](adding-content-to-source-control.md)
