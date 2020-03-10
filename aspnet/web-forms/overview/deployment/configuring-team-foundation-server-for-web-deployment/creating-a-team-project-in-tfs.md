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
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="30276-103">在 TFS 中创建团队项目</span><span class="sxs-lookup"><span data-stu-id="30276-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="30276-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="30276-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="30276-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="30276-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="30276-106">本主题介绍如何在 Team Foundation Server （TFS）2010中创建新的团队项目。</span><span class="sxs-lookup"><span data-stu-id="30276-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="30276-107">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="30276-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="30276-108">任务概述</span><span class="sxs-lookup"><span data-stu-id="30276-108">Task Overview</span></span>

<span data-ttu-id="30276-109">若要预配和使用 TFS 中的新团队项目，需要完成以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="30276-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="30276-110">向将创建新团队项目的用户授予权限。</span><span class="sxs-lookup"><span data-stu-id="30276-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="30276-111">创建团队项目。</span><span class="sxs-lookup"><span data-stu-id="30276-111">Create the team project.</span></span>
- <span data-ttu-id="30276-112">向将处理项目的团队成员授予权限。</span><span class="sxs-lookup"><span data-stu-id="30276-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="30276-113">签入某些内容。</span><span class="sxs-lookup"><span data-stu-id="30276-113">Check in some content.</span></span>

<span data-ttu-id="30276-114">本主题将演示如何执行这些过程，并将确定可能负责每个过程的用户和作业角色。</span><span class="sxs-lookup"><span data-stu-id="30276-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="30276-115">请注意，根据你的组织的结构，每个任务都可能是不同人员的责任。</span><span class="sxs-lookup"><span data-stu-id="30276-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="30276-116">本主题中的任务和演练假定您已安装并配置 TFS，并且您已在配置过程中创建了一个团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="30276-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="30276-117">有关这些假设的详细信息，以及有关该方案的更多常规背景信息，请参阅为[Web 部署配置 TFS 生成服务器](configuring-a-tfs-build-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="30276-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="30276-118">向团队项目创建者授予权限</span><span class="sxs-lookup"><span data-stu-id="30276-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="30276-119">若要创建新的团队项目，你需要具备以下权限：</span><span class="sxs-lookup"><span data-stu-id="30276-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="30276-120">您必须具有 TFS 应用程序层上的 "**创建新项目**" 权限。</span><span class="sxs-lookup"><span data-stu-id="30276-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="30276-121">通常通过将用户添加到 "**项目集合管理员**" TFS 组来授予此权限。</span><span class="sxs-lookup"><span data-stu-id="30276-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="30276-122">**Team Foundation Administrators**全局组还包括此权限。</span><span class="sxs-lookup"><span data-stu-id="30276-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="30276-123">您必须有权在与 TFS 团队项目集合相对应的 SharePoint 网站集内创建新的团队网站。</span><span class="sxs-lookup"><span data-stu-id="30276-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="30276-124">通常通过将用户添加到对 SharePoint 网站集具有**完全控制**权限的 sharepoint 组来授予此权限。</span><span class="sxs-lookup"><span data-stu-id="30276-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="30276-125">如果使用 SQL Server Reporting Services 功能，则必须是 Reporting Services 中的 " **Team Foundation 内容管理员**" 角色的成员。</span><span class="sxs-lookup"><span data-stu-id="30276-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="30276-126">谁执行这些过程？</span><span class="sxs-lookup"><span data-stu-id="30276-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="30276-127">通常，管理 TFS 部署的人员或组也会执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="30276-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="30276-128">由于这是一个具有高特权的权限集，因此新团队项目通常由一小部分用户创建，负责管理 TFS 部署。</span><span class="sxs-lookup"><span data-stu-id="30276-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="30276-129">通常不会向开发人员授予创建新团队项目所需的权限。</span><span class="sxs-lookup"><span data-stu-id="30276-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="30276-130">在 TFS 中授予权限</span><span class="sxs-lookup"><span data-stu-id="30276-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="30276-131">如果要使用户能够创建新的团队项目，则第一个高级任务是将用户添加到团队项目集合的 "**项目集合管理员**" 组。</span><span class="sxs-lookup"><span data-stu-id="30276-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="30276-132">**将用户添加到 "项目集合管理员" 组**</span><span class="sxs-lookup"><span data-stu-id="30276-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="30276-133">在 TFS 服务器上的 "**开始**" 菜单中，指向 "**所有程序**"，单击**Microsoft Team Foundation Server 2010**"，然后单击" **Team Foundation 管理控制台**"。</span><span class="sxs-lookup"><span data-stu-id="30276-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="30276-134">在导航树视图中，展开 "**应用层**"，然后单击 "**团队项目集合**"。</span><span class="sxs-lookup"><span data-stu-id="30276-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="30276-135">在 "**团队项目集合**" 窗格中，选择要管理的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="30276-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="30276-136">在 "**常规**" 选项卡上，单击 "**组成员身份**"。</span><span class="sxs-lookup"><span data-stu-id="30276-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="30276-137">在 "**全局组**" 对话框中，选择 "**项目集合管理员**" 组，然后单击 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="30276-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="30276-138">在 " **Team Foundation Server 组属性**" 对话框中，选择 " **Windows 用户或组**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="30276-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="30276-139">在 "**选择用户、计算机或组**" 对话框中，键入你希望能够创建新团队项目的用户的用户名，单击 "**检查名称**"，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="30276-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="30276-140">在**Team Foundation Server 组属性**"对话框中，单击 **" 确定 "** 。</span><span class="sxs-lookup"><span data-stu-id="30276-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="30276-141">在 "**全局组**" 对话框中，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="30276-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="30276-142">在 SharePoint Services 中授予权限</span><span class="sxs-lookup"><span data-stu-id="30276-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="30276-143">接下来，您需要授予用户在与 TFS 团队项目集合对应的 SharePoint 网站集中创建新团队网站的权限。</span><span class="sxs-lookup"><span data-stu-id="30276-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="30276-144">**授予对 SharePoint 网站集的 "完全控制" 权限**</span><span class="sxs-lookup"><span data-stu-id="30276-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="30276-145">在 Team Foundation Server 管理控制台的 "**团队项目集合**" 页上，选择要管理的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="30276-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="30276-146">在 " **SharePoint 站点**" 选项卡上，记下 "**当前默认站点位置**URL" 的值。</span><span class="sxs-lookup"><span data-stu-id="30276-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="30276-147">打开 Internet Explorer，然后前往步骤2中记下的 URL。</span><span class="sxs-lookup"><span data-stu-id="30276-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="30276-148">如果你未以创建团队项目集合的用户身份登录到 Windows，则需要以此用户身份登录到 SharePoint 以便继续。</span><span class="sxs-lookup"><span data-stu-id="30276-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="30276-149">在 **“网站操作”** 菜单上，单击 **“网站设置”** 。</span><span class="sxs-lookup"><span data-stu-id="30276-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="30276-150">在 "**站点设置**" 页上的 "**用户和权限**" 下，单击 "**人员和组**"。</span><span class="sxs-lookup"><span data-stu-id="30276-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="30276-151">在左侧导航面板中，单击 "**组**"。</span><span class="sxs-lookup"><span data-stu-id="30276-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="30276-152">在 "**用户和组：所有组**" 页上，单击 "**为此站点设置组**"。</span><span class="sxs-lookup"><span data-stu-id="30276-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="30276-153">由于双 HTTP 编码错误，你可能会收到 "<strong>找不到 http 404</strong> " 错误。</span><span class="sxs-lookup"><span data-stu-id="30276-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="30276-154">如果出现这种情况，请将 URL 替换为：</span><span class="sxs-lookup"><span data-stu-id="30276-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="30276-155">`[site_collection_URL]/_layouts/permsetup.aspx` 例如：</span><span class="sxs-lookup"><span data-stu-id="30276-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="30276-156">在 "**为此站点设置组**" 页上，将创建团队项目的用户添加到 "**所有者**" 组，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="30276-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="30276-157">有关使用户能够在团队项目集合中创建新团队项目的详细信息，请参阅[为团队项目集合设置管理员权限](https://msdn.microsoft.com/library/dd547204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="30276-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="30276-158">创建新的团队项目并添加用户</span><span class="sxs-lookup"><span data-stu-id="30276-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="30276-159">获得必要的权限后，可以使用 Visual Studio 2010 中的 "**团队资源管理器**" 窗口创建新的团队项目。</span><span class="sxs-lookup"><span data-stu-id="30276-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="30276-160">此方法提供了一个向导，该向导收集所有必需的信息，并在 TFS、SharePoint 和 SQL Server Reporting Services 中执行必要的任务。</span><span class="sxs-lookup"><span data-stu-id="30276-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="30276-161">还需要向开发人员团队成员授予对新团队项目的权限，以使他们能够添加和修改内容。</span><span class="sxs-lookup"><span data-stu-id="30276-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="30276-162">谁执行这些过程？</span><span class="sxs-lookup"><span data-stu-id="30276-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="30276-163">通常，TFS 管理员或开发人员团队负责人会执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="30276-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="30276-164">创建新的团队项目</span><span class="sxs-lookup"><span data-stu-id="30276-164">Create a New Team Project</span></span>

<span data-ttu-id="30276-165">下一过程介绍如何在 TFS 2010 中创建新的团队项目。</span><span class="sxs-lookup"><span data-stu-id="30276-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="30276-166">**创建新的团队项目**</span><span class="sxs-lookup"><span data-stu-id="30276-166">**To create a new team project**</span></span>

1. <span data-ttu-id="30276-167">在 "**开始**" 菜单上，指向 "**所有程序**"，单击**Microsoft Visual Studio 2010**，右键单击**Microsoft Visual Studio 2010**"，然后单击" 以**管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="30276-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="30276-168">如果不以管理员身份运行 Visual Studio 2010，则 "新建团队项目向导" 将在上一步中失败。</span><span class="sxs-lookup"><span data-stu-id="30276-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="30276-169">如果此时出现 **“用户帐户控制”** 对话框，请单击 **“是”** 。</span><span class="sxs-lookup"><span data-stu-id="30276-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="30276-170">在 Visual Studio 的 "**团队**" 菜单上，单击 "**连接到 Team Foundation Server**"。</span><span class="sxs-lookup"><span data-stu-id="30276-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="30276-171">如果已配置到 TFS 服务器的连接，则可以省略步骤4-7。</span><span class="sxs-lookup"><span data-stu-id="30276-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="30276-172">在 "**连接到团队项目**" 对话框中，单击 "**服务器**"。</span><span class="sxs-lookup"><span data-stu-id="30276-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="30276-173">在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="30276-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="30276-174">在 "**添加 Team Foundation Server** " 对话框中，提供 TFS 实例的详细信息，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="30276-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="30276-175">在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="30276-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="30276-176">在 "**连接到团队项目**" 对话框中，选择要连接到的 TFS 实例，选择要添加到的团队项目集合，然后单击 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="30276-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="30276-177">在 "**团队资源管理器**" 窗口中，右键单击团队项目集合，然后单击 "**新建团队项目**"。</span><span class="sxs-lookup"><span data-stu-id="30276-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="30276-178">在 "**新建团队项目**" 对话框中，为团队项目提供名称和说明，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="30276-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="30276-179">如果你的团队项目包含空格，则当你使用 Internet Information Services （IIS） Web 部署工具（Web 部署）从输出路径部署包时可能会遇到一些问题。</span><span class="sxs-lookup"><span data-stu-id="30276-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="30276-180">路径中的空格会使运行 Web 部署命令变得更加困难。</span><span class="sxs-lookup"><span data-stu-id="30276-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="30276-181">在 "**选择过程模板**" 页上，选择要用于管理开发过程的过程模板，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="30276-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="30276-182">有关 TFS 过程模板的详细信息，请参阅[过程模板和工具](https://msdn.microsoft.com/vstudio/aa718795)。</span><span class="sxs-lookup"><span data-stu-id="30276-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="30276-183">在 "**团队网站设置**" 页上，保持默认设置不变，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="30276-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="30276-184">此设置创建或标识与 TFS 团队项目关联的 SharePoint 团队网站。</span><span class="sxs-lookup"><span data-stu-id="30276-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="30276-185">你的开发团队可以使用此网站来管理文档、参与讨论线索、创建 wiki 页，以及执行与代码无关的其他任务。</span><span class="sxs-lookup"><span data-stu-id="30276-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="30276-186">有关详细信息，请参阅[SharePoint 产品与 Team Foundation Server 之间的交互](https://msdn.microsoft.com/library/ms253177.aspx)。</span><span class="sxs-lookup"><span data-stu-id="30276-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="30276-187">在 "**指定源代码管理设置**" 页上，保持默认设置不变，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="30276-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="30276-188">此设置在 TFS 文件夹层次结构中标识或创建将充当内容根文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="30276-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="30276-189">在 "**确认团队项目设置**" 页上，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="30276-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="30276-190">成功创建新团队项目后，在 "**团队项目创建**" 页上，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="30276-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="30276-191">将用户添加到团队项目</span><span class="sxs-lookup"><span data-stu-id="30276-191">Add Users to a Team Project</span></span>

<span data-ttu-id="30276-192">现在，你已创建新的团队项目，你可以向用户授予权限，使其能够开始添加和合作内容。</span><span class="sxs-lookup"><span data-stu-id="30276-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="30276-193">**将用户添加到团队项目**</span><span class="sxs-lookup"><span data-stu-id="30276-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="30276-194">在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，右键单击团队项目，指向 "**团队项目设置**"，然后单击 "**组成员资格**"。</span><span class="sxs-lookup"><span data-stu-id="30276-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="30276-195">若要使用户能够添加、修改和删除源代码管理下的代码，你需要将其添加到 "**参与者**" 组。</span><span class="sxs-lookup"><span data-stu-id="30276-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="30276-196">在 "**项目组**" 对话框中，选择 "**参与者**" 组，然后单击 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="30276-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="30276-197">在 " **Team Foundation Server 组属性**" 对话框中，选择 " **Windows 用户或组**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="30276-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="30276-198">在 "**选择用户、计算机或组**" 对话框中，键入要添加到团队项目的用户的用户名，单击 "**检查名称**"，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="30276-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="30276-199">在**Team Foundation Server 组属性**"对话框中，单击 **" 确定 "** 。</span><span class="sxs-lookup"><span data-stu-id="30276-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="30276-200">在 "**项目组**" 对话框中，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="30276-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="30276-201">结束语</span><span class="sxs-lookup"><span data-stu-id="30276-201">Conclusion</span></span>

<span data-ttu-id="30276-202">此时，你的新团队项目可以使用，并且你的开发人员团队可以开始添加内容并在开发过程中进行协作。</span><span class="sxs-lookup"><span data-stu-id="30276-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="30276-203">下一主题[将内容添加到源代码管理](adding-content-to-source-control.md)中介绍了如何将内容添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="30276-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="30276-204">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="30276-204">Further Reading</span></span>

<span data-ttu-id="30276-205">若要更广泛地了解如何在 TFS 中创建团队项目，请参阅[创建团队项目](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="30276-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="30276-206">有关使用户能够在团队项目集合中创建新团队项目的详细信息，请参阅[为团队项目集合设置管理员权限](https://msdn.microsoft.com/library/dd547204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="30276-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="30276-207">有关将用户添加到团队项目的详细信息，请参阅[将用户添加到团队项目](https://msdn.microsoft.com/library/bb558971.aspx)。</span><span class="sxs-lookup"><span data-stu-id="30276-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="30276-208">[上一页](configuring-team-foundation-server-for-web-deployment.md)
> [下一页](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="30276-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
