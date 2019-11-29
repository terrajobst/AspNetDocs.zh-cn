---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署仅限代码的更新-8 of 12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572789"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署仅限代码的更新-8 （共12个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

初始部署完成后，你维护和开发网站的工作将继续进行，在此之前，你将需要部署更新。 本教程将指导你完成将更新部署到应用程序代码的过程。 此更新不涉及数据库更改;在下一教程中，你将看到有关部署数据库更改的不同之处。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="making-a-code-change"></a>更改代码

作为应用程序更新的简单示例，你将向**讲师**页添加选定讲师讲授的课程列表。

如果您运行的是**讲师**页，您会注意到网格中有**选择**的链接，但除了使行背景变为灰色以外，它们不会执行任何操作。

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

现在，你将添加在单击 "**选择**" 链接时运行的代码，并显示所选指导员讲授的课程列表。

在*default.aspx*中，在**ErrorMessageLabel** `Label` 控件后立即添加以下标记：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

运行页面并选择一个指导员。 你将看到该教师讲授的课程列表。

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>将代码更新部署到测试环境

部署到测试环境只需再次运行一次单击 "发布" 即可。 若要使此过程更快，你可以使用**Web 一键式发布**工具栏。

在 "**视图**" 菜单中选择 "**工具栏**"，然后选择 **"Web 一键式发布"** 。

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

在**解决方案资源管理器**中，选择 ContosoUniversity 项目。

**Web 一键式发布**工具栏上，选择 "**测试**发布配置文件"，然后单击 "**发布 Web** " （其箭头指向左侧和右侧的图标）。

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio 将部署更新后的应用程序，浏览器会自动打开到主页。 运行 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

通常情况下，还会进行回归测试（即，测试站点的其余部分以确保新的更改不会破坏现有的任何功能）。 但对于本教程，你将跳过该步骤并继续将更新部署到生产环境。

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>阻止将初始数据库状态重新部署到生产环境

在实际应用程序中，用户在初次部署后与生产站点进行交互，并使用实时数据填充数据库。 因此，您不希望在其初始状态下重新部署成员资格数据库，这会擦除所有实时数据。 由于 SQL Server Compact 数据库是*应用\_Data*文件夹中的文件，因此必须通过更改部署设置来防止此情况，以便不部署*应用\_Data*文件夹中的文件。

打开 ContosoUniversity 项目的 "**项目属性**" 窗口，然后选择 "**打包/发布 Web** " 选项卡。确保 "**配置**" 下拉框中选择了 "**活动（发布）** " 或 "**发布**"，然后选择 **"从应用程序中排除文件\_Data 文件夹**。

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

如果你决定以后部署调试版本，则最好对调试生成配置进行相同的更改：将**配置**更改为 "**调试**"，然后选择 **"从应用程序中排除文件\_Data 文件夹**。

保存并关闭 "**打包/发布 Web** " 选项卡。

> [!NOTE] 
> 
> [!IMPORTANT]
> 请确保在发布配置文件中选择的 "目标位置不**删除其他文件**"。 如果选择该选项，部署过程将删除已部署站点中的应用\_数据中的数据库，并将删除应用\_数据文件夹本身。

## <a name="preventing-user-access-to-the-production-site-during-update"></a>在更新过程中阻止用户访问生产站点

现在正在部署的更改是单个页面的简单更改。 但有时你会部署更大的更改，在这种情况下，如果用户在部署完成之前请求页面，则站点可能会奇怪。 若要防止出现这种情况，可以使用*应用\_脱机 .htm*文件。 在应用程序的根文件夹中将名为 "app" 的文件\_为 " *offline* " 时，IIS 会自动显示该文件，而不是运行应用程序。 因此，若要在部署过程中阻止访问，请在根文件夹中将*应用\_为 offline* ，运行部署过程，然后删除*应用\_"脱机*"。

在**解决方案资源管理器**中，右键单击解决方案（不是项目之一），然后选择 "**新建解决方案文件夹**"。

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

将文件夹命名为*SolutionFiles*。

在 "新建" 文件夹中，创建一个名为 app 的 HTML 页面 *\_offline*。 将现有内容替换为以下标记：

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

你可以通过使用 FTP 连接或托管提供程序控制面板中的**文件管理器**实用工具，将*应用\_脱机 .htm*文件复制到站点。 对于本教程，你将使用**文件管理器**。

打开 "控制面板"，选择 "**文件管理器**"，如您在[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)中所做的那样。 选择 " **contosouniversity.com** "，然后选择 " **wwwroot** " 获取应用程序的根文件夹，然后单击 "**上载**"。

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

在 "**上传文件**" 对话框中，选择 "*应用\_脱机 .htm*文件，然后单击"**上载**"。

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

浏览到你的站点的 URL。 此时将显示 "*应用\_offline* " 页，而不是主页。

[![App_offline。 htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

你现在已准备好部署到生产环境。

## <a name="deploying-the-code-update-to-the-production-environment"></a>将代码更新部署到生产环境

在**Web 一键式发布**工具栏中，选择 "**生产**" 发布配置文件，然后单击 "**发布 Web**"。

Visual Studio 将部署更新后的应用程序，并将浏览器打开到站点的主页。 将显示*应用程序\_脱机 .htm*文件。 必须先删除*应用\_脱机 .htm*文件，然后才能进行测试以验证部署是否成功。

返回到控制面板中的**文件管理器**应用程序。 选择**contosouniversity.com**和**wwwroot**，选择 " **app\_** "，然后单击 "**删除**"。

[![Deleting_app_offline .htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

在浏览器中，打开公共站点中的 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

现在，你已部署了一个不涉及数据库更改的应用程序更新。 下一教程介绍如何部署数据库更改。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
