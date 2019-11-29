---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 使用 Visual Studio SQL Server Compact 部署 ASP.NET Web 应用程序：简介-1/12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: ea88da1e6d510f706fc7ca370cfa32974c1243f8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587746"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>使用 Visual Studio SQL Server Compact 部署 ASP.NET Web 应用程序：第1项，共12项

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。
> 
> 这些教程将引导你完成在本地开发计算机上首先部署到 IIS 以进行测试，然后再部署到第三方托管提供商。 要部署的应用程序将使用应用程序数据库和 ASP.NET 成员资格数据库。 开始使用 SQL Server Compact，并将其部署到 SQL Server Compact，稍后的教程介绍了如何部署数据库更改以及如何迁移到 SQL Server。
> 
> 本教程假设你知道如何在 Visual Studio 中使用 ASP.NET。 如果你不想这样做，就是一个很好的开端，就是一个[基本的 ASP.NET Web 窗体教程](../tailspin-spyworks/tailspin-spyworks-part-1.md)或[基本的 ASP.NET MVC 教程](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)。
> 
> 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET 部署论坛](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)。

## <a name="overview"></a>概述

这些教程将引导你完成在本地开发计算机上首先部署到 IIS 以进行测试，然后再部署到第三方托管提供商。 要部署的应用程序将使用应用程序数据库和 ASP.NET 成员资格数据库。 开始使用 SQL Server Compact，并将其部署到 SQL Server Compact，稍后的教程介绍了如何部署数据库更改以及如何迁移到 SQL Server。

所有教程中的教程数–11还包括故障排除页，这可能会使部署过程显得非常困难。 事实上，部署站点的基本过程是创建教程集的一个相对较小的部分。 但是，在实际情况下，通常需要有关部署的一些小但重要的额外方面的信息，例如，在目标服务器上设置文件夹权限。 我们在这些教程中包含了许多其他技巧，希望教程不会留下可能会阻止你成功部署真实应用程序的信息。

这些教程旨在按顺序运行，每个部分都是在上一节中生成的。 但是，您可以跳过与您的情况无关的部分。 （跳过部件可能会要求你在后面的教程中调整过程。）

## <a name="intended-audience"></a>目标受众

本教程面向在小型组织或其他环境中工作的 ASP.NET 开发人员：

- 不使用持续集成过程（自动生成和部署）。
- 生产环境是第三方托管提供商。
- 一个用户通常会填充多个角色（相同人员开发、测试和部署）。

在企业环境中，更常见的做法是实现持续集成过程，并且生产环境通常由公司自己的服务器托管。 不同人员通常还会执行不同的角色。 有关企业部署的信息，请参阅[在企业方案中部署 Web 应用程序](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。

所有规模的组织还可以将 web 应用程序部署到 Azure，这些教程中所示的大部分过程也适用于 Azure 应用 Services Web Apps。 有关 Azure 的简介，请参阅[https://azure.microsoft.com](https://azure.microsoft.com)。

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>教程中所示的宿主提供程序

本教程将引导你完成设置具有托管公司的帐户，并将该应用程序部署到该宿主提供程序的过程。 选择了特定的托管公司，以便教程能够说明部署到实时网站的完整体验。 每个托管公司都提供不同的功能，部署到其服务器的体验会略有不同;但是，在整个过程中，本教程中所述的过程是典型过程。

本教程中使用的托管提供程序 Cytanium.com 是其中的一个可用的提供程序，在本教程中，其使用并不构成认可或建议。

## <a name="deploying-web-site-projects"></a>部署网站项目

Contoso 大学是 Visual Studio web 应用程序项目。 本教程中演示的大部分部署方法和工具不适用于[网站项目](https://msdn.microsoft.com/library/dd547590.aspx)。 有关如何部署网站项目的信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)。

## <a name="deploying-aspnet-mvc-projects"></a>部署 ASP.NET MVC 项目

在本教程中，你将部署一个 ASP.NET Web 窗体项目，但你学习如何操作的所有内容也适用于 ASP.NET MVC。 Visual Studio MVC 项目只是 web 应用程序项目的另一种形式。 唯一的区别是，如果你要部署到不支持 ASP.NET MVC 或目标版本的托管提供商，则必须确保已在项目中安装了相应的（[MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)或[mvc 4](http://nuget.org/packages/aspnetmvc)） NuGet 包。

## <a name="programming-language"></a>编程语言

示例应用程序使用C#的是C#，但教程不需要了解，并且教程所示的部署技术不特定于语言。

## <a name="troubleshooting-during-this-tutorial"></a>本教程中的故障排除

在部署期间发生错误时，或者如果部署的站点未正确运行，则错误消息不会始终提供解决方案。 若要帮助解决一些常见问题，请[参阅故障排除参考页面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。 如果您收到一条错误消息或在您完成本教程时无法正常工作，请务必查看故障排除页。

## <a name="comments-welcome"></a>欢迎评论

欢迎使用教程中的注释，并在每次更新本教程时，将对教程注释中提供的改进进行更正或建议。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已在计算机上安装了 Windows 7 或更高版本以及以下产品之一：

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [用于 Web 的 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC](https://go.microsoft.com/fwlink/?LinkId=240162)

如果安装了 Visual Studio 2010 SP1 或 Visual Web Developer Express 2010 SP1，还需要安装以下产品：

- [适用于 .net 的 AZURE SDK （VS 2010 SP1）](https://go.microsoft.com/fwlink/?LinkID=208120) （包括 Web 发布更新）
- [Microsoft Visual Studio 2010 SP1 Tools for SQL Server Compact 4。0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

若要完成本教程，还需要使用其他一些软件，但不需要加载该软件。 本教程将引导你完成在需要时进行安装的步骤。

## <a name="downloading-the-sample-application"></a>下载示例应用程序

要部署的应用程序名为 Contoso 大学，并已为您创建。 它是大学网站的简化版本，它在[ASP.NET 站点上实体框架教程](https://asp.net/entity-framework/tutorials)中所述的 Contoso 大学应用程序上松松。

安装必备组件后，请下载[Contoso 大学 web 应用程序](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)。 该 *.zip*文件包含项目的多个版本和包含所有12个教程的 PDF 文件。 若要完成本教程的步骤，请从 ContosoUniversity 开始。 若要查看该项目在教程结束时的外观，请打开 ContosoUniversity。 若要查看在教程10中迁移到完整 SQL Server 之前项目的外观，请打开 ContosoUniversity-AfterTutorial09。

若要准备完成教程步骤，请将 ContosoUniversity 保存到用于使用 Visual Studio 项目的任何文件夹。 默认情况下，这是以下文件夹：

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

（对于本教程中的屏幕截图，项目文件夹位于 `C`：驱动器的根目录中。）

启动 Visual Studio，打开该项目，然后按 CTRL + F5 运行该项目。

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

可从菜单栏访问网站页面，并允许你执行以下功能：

- 显示学生统计信息（"关于" 页）。
- 显示、编辑、删除和添加学生。
- 显示和编辑课程。
- 显示和编辑指导员。
- 显示和编辑部门。

下面是几个代表页的屏幕截图。

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>查看影响部署的应用程序功能

应用程序的以下功能会影响部署此应用程序的方式或部署方法。 本系列中的以下教程更详细地介绍了其中的每一项。

- Contoso 大学使用 SQL Server Compact 数据库来存储应用程序数据，例如学生和指导员名称。 数据库包含测试数据和生产数据的组合，在您部署到生产环境时，您需要排除测试数据。 稍后在本系列教程中，你将从 SQL Server Compact 迁移到 SQL Server。
- 应用程序使用 ASP.NET 成员资格系统，该系统将用户帐户信息存储在 SQL Server Compact 数据库中。 该应用程序定义了有权访问某些受限信息的管理员用户。 你需要在没有测试帐户的情况下部署成员资格数据库，但需要一个管理员帐户。
- 由于应用程序数据库和成员资格数据库使用 SQL Server Compact 作为数据库引擎，因此您必须将数据库引擎部署到宿主提供程序和数据库本身。
- 应用程序使用 ASP.NET 通用成员资格提供程序，以便成员资格系统可以将其数据存储在 SQL Server Compact 数据库中。 包含通用成员资格提供程序的程序集必须与应用程序一起部署。
- 应用程序使用实体框架5.0 来访问应用程序数据库中的数据。 必须随应用程序一起部署包含实体框架5.0 的程序集。
- 应用程序使用第三方错误日志记录和报告实用工具。 此实用程序在必须与应用程序一起部署的程序集中提供。
- 错误日志记录实用工具将 XML 文件中的错误信息写入文件夹。 你必须确保 ASP.NET 在部署的站点下运行的帐户对此文件夹具有写入权限，并且你必须从部署中排除此文件夹。 （否则，可能会将测试环境中的错误日志数据部署到生产环境，/或者可能会删除生产错误日志文件。）
- 应用程序包括某些必须在已部署的*web.config*文件中更改的设置，具体取决于目标环境（测试或生产）以及必须更改的其他设置，具体取决于生成配置（调试或发布）。
- Visual Studio 解决方案包括一个类库项目。 只应部署此项目生成的程序集，而不部署项目本身。

在本系列教程的第一个教程中，已下载示例 Visual Studio 项目和查看的站点功能，这些功能会影响你部署应用程序的方式。 在以下教程中，您将通过设置其中的某些项来准备自动处理的部署。 您手动处理的其他人。

> [!div class="step-by-step"]
> [下一页](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
