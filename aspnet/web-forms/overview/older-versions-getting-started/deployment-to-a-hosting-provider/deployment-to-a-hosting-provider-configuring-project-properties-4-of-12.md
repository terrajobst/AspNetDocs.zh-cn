---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：配置项目属性-4/12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: 6e63e75dca3d776fb9a1bd7e420ef48891daac69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507734"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：配置项目属性-4 个（共12个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

某些部署选项在存储在项目文件（ *.csproj*或 *.vbproj*文件）的项目属性中进行配置。 在大多数情况下，这些设置的默认值是你想要的，但是如果你需要更改这些设置，则可以使用 Visual Studio 中内置的**项目属性**UI 来处理这些设置。 在本教程中，您将查看**项目属性**中的部署设置。 还会创建一个占位符文件，用于部署空文件夹。

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>在项目属性窗口中配置部署设置

影响部署过程中所发生情况的大多数设置都包含在发布配置文件中，如以下教程中所示。 你应注意的几个设置位于 "**项目属性**" 窗口的 "**打包/发布**" 选项卡中。 这些设置是为每个生成配置指定的-也就是说，对于发布版本，你可以具有与调试版本不同的设置。

在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目，选择 "**属性**"，然后选择 "**打包/发布 Web** " 选项卡。

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

当显示窗口时，它默认显示针对解决方案当前处于活动状态的任何生成配置的设置。 如果**配置**框未指示 "**活动（发布）** "，请选择 "**发布**" 以显示 "发布" 生成配置的设置。 你将在测试环境和生产环境中部署版本版本。

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

选择 "**活动" （发布）** 或 "**发布**" 时，可以看到在使用 "发布" 生成配置进行部署时有效的值：

- 在 "**要部署的项**" 框中，只选择了**运行应用程序所需的文件**。 其他选项包括**此项目中的所有文件**或**此项目文件夹中的所有文件**。 通过保持默认选择不变，你可以避免部署源代码文件，例如。 此设置是必须包含在项目中的包含 SQL Server Compact 二进制文件的文件夹的原因。 有关此设置的详细信息，请参阅[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx)中的**为什么不会部署项目文件夹中的所有文件？** 。
- 选择 "**排除生成的调试符号**"。 使用此生成配置时，不会进行调试。
- 不选择**从应用中排除文件\_Data 文件夹**。 成员资格数据库的 SQL Server Compact 文件位于该文件夹中，你必须对其进行部署。 部署不包含数据库更改的更新时，将选中此复选框。
- 未选择**发布之前预编译此应用程序**。 在大多数情况下，无需预编译 web 应用程序项目。 有关此选项的详细信息，请参阅["打包/发布 Web" 选项卡、"项目属性" 和 "](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx) [高级预编译设置" 对话框](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)。
- 已选择 "**包含在包/发布 sql 中配置的所有数据库" 选项卡**，但此选项现在不起作用，因为你没有配置 "**包/发布 sql** " 选项卡。该选项卡用于旧的数据库部署方法，该方法仅用于部署 SQL Server 数据库的唯一选项。 你将使用 "[迁移到 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)教程中的"**包/发布 SQL** "选项卡。
- " **Web 部署包设置**" 部分不适用，因为在这些教程中使用一键式发布。

将 "**配置**" 下拉框更改为 "调试"，以查看 "调试版本" 的默认设置。 值是相同的，但会清除 "**排除生成的调试符号**"，以便可以在部署调试版本时进行调试。

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>确保已部署了 Elmah 文件夹

正如你在上一教程中看到的那样， [Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)提供了用于错误日志记录和报告的功能。 在 Contoso 大学，application Elmah 已配置为将错误详细信息存储在名为*Elmah*的文件夹中：

![Elmah 文件夹](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

从部署中排除特定文件或文件夹是一个常见的要求;另一个示例是用户可以将文件上传到的文件夹。 您不希望将在开发环境中创建的日志文件或上载文件部署到生产环境中。 如果要将更新部署到生产环境，则不希望部署过程删除生产环境中存在的文件。 （根据设置部署选项的方式，如果在部署时目标站点中存在文件，而不是源站点中的文件，Web 部署会从目标中删除该文件。）

如本教程前面所述，"**打包/发布 Web** " 选项卡中的 "**要部署的项目**" 选项设置为**仅运行此应用程序所需的文件**。 因此，将不会部署在开发中由 Elmah 创建的日志文件，这是你想要执行的操作。 （若要进行部署，必须将其包含在项目中，并且必须将其 "**生成操作**" 属性设置为 "**内容**"。 有关详细信息，请参阅[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx)中的**为什么不会部署项目文件夹中的所有文件？** 。 但 Web 部署将不会在目标站点中创建文件夹，除非至少有一个要复制到其中的文件。 因此，您将向文件夹中添加一个 *.txt*文件作为占位符，以便复制文件夹。

在**解决方案资源管理器**中，右键单击 " *Elmah* " 文件夹，选择 "**添加新项**"，然后创建一个名为 " *Placeholder*" 的文件。 将以下文本放入其中： "这是一个用于确保文件夹已部署的占位符文件。" 并保存该文件。 这就是您必须执行的所有操作，以确保 Visual Studio 部署此文件及其所在的文件夹，因为 *.txt*文件的 "**生成操作**" 属性默认设置为 "**内容**"。

你现在已经完成了所有部署设置任务。 在下一教程中，你将把 Contoso 大学网站部署到测试环境，并在其中进行测试。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
