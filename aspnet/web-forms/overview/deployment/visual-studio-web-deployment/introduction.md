---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 使用 Visual Studio 的 ASP.NET Web 部署：简介 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何使用 V ... 将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 96dd31d949633e001fc595621bedbf74e98000fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640239"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>使用 Visual Studio 的 ASP.NET Web 部署：简介

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 和 Azure SDK for .NET，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 大多数过程与 Visual Studio 2013 类似。
> 
> 你要开发一个 web 应用程序，以便通过 Internet 访问该应用程序。 但 web 编程教程通常会在您向您展示如何在开发计算机上工作之前立即停止。 这一系列教程将在其他位置离开：你构建了一个 web 应用，对其进行了测试，并已准备就绪。 后续步骤 这些教程介绍了如何在本地开发计算机上首先向 IIS 部署，以便进行测试，然后再部署到 Azure 或第三方托管提供商进行过渡和生产。 要部署的示例应用程序是使用实体框架、SQL Server 和 ASP.NET 成员资格系统的 web 应用程序项目。 该示例应用程序使用 ASP.NET Web 窗体，但显示的过程也适用于 ASP.NET MVC 和 Web API。
> 
> 这些教程假设你知道如何在 Visual Studio 中使用 ASP.NET。 如果你不想这样做，就是一个很好的开端，就是一个[基本的 ASP.NET Web 窗体教程](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md)或[基本的 ASP.NET MVC 教程](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。
> 
> 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET 部署论坛](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)或[StackOverflow](http://stackoverflow.com)。
> 
> [TechNet 电子书库](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)中也提供了此内容作为免费电子书。

## <a name="overview"></a>概述

这些教程将指导你部署包含 SQL Server 数据库的 ASP.NET web 应用程序。 你将首先部署到本地开发计算机上的 IIS 进行测试，然后再部署到 Azure App Service 的 Web 应用和 Azure SQL 数据库进行过渡和生产。 你将了解如何使用 Visual Studio 一键式发布进行部署，你将了解如何使用命令行进行部署。

教程数量可能会使部署过程显得非常困难。 事实上，基本过程很简单。 但在实际情况下，通常需要执行额外的部署任务，例如，在目标服务器上设置文件夹权限。 我们已经介绍了一些其他任务，希望教程不会遗漏可能会妨碍你成功部署真实应用程序的信息。

这些教程旨在按顺序运行，每个部分都是在上一节中生成的。 你可以跳过与你的情况无关的部分，但你可能需要在以后的教程中调整过程。

## <a name="intended-audience"></a>目标受众

本教程面向在以下环境中工作的 ASP.NET 开发人员：

- 生产环境 Azure App Service Web 应用或第三方托管提供商。
- 部署不仅限于持续集成过程，而且可以直接从 Visual Studio 进行。

除了演示如何从命令行部署的一个教程外，本教程中不涉及使用[持续交付](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)过程从[源代码管理](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)进行的部署。 有关持续交付的信息，请参阅以下资源：

- [持续集成和持续交付（通过 Microsoft Azure 构建实际的云应用）](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [在 Azure App Service 中部署 web 应用](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [在企业方案中部署 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)（为 Visual Studio 2010 编写的一组较旧的教程，这些教程仍包含适用于企业环境的有用信息。）

## <a name="using-a-third-party-hosting-provider"></a>使用第三方托管提供程序

本教程将引导你完成设置 Azure 帐户并将应用程序部署到 Azure App Service 进行过渡和生产的 Web 应用的过程。 但是，可以使用相同的基本过程来部署到所选的第三方托管提供程序。 其中的教程介绍了 Azure 独有的流程，它们说明了，并说明了可在第三方托管提供商处获得哪些区别。

## <a name="deploying-web-app-projects"></a>部署 web 应用项目

下载并部署这些教程的示例应用程序是 Visual Studio web 应用程序项目。 但是，如果您安装了适用于 Visual Studio 的最新 Web 发布更新，则可以对 Web 应用项目使用相同的部署方法和工具。

## <a name="deploying-aspnet-mvc-projects"></a>部署 ASP.NET MVC 项目

该示例应用程序是一个 ASP.NET Web 窗体项目，但你了解到的所有内容也适用于 ASP.NET MVC。 Visual Studio MVC 项目只是 web 应用程序项目的另一种形式。 唯一的区别是，如果你要部署到不支持 ASP.NET MVC 或目标版本的托管提供商，则必须确保已在你的项目中安装了相应的（[MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)、 [Mvc 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)或[mvc 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)） NuGet 包。

## <a name="programming-language"></a>编程语言

示例应用程序使用C#的是C#，但教程不需要了解，并且教程所示的部署技术不特定于语言。

## <a name="database-deployment-methods"></a>数据库部署方法

可以通过三种方式在 Visual Studio 中部署 SQL Server 数据库和 web 部署：

- Entity Framework Code First 迁移
- DbDacFx Web 部署提供程序
- DbFullSql Web 部署提供程序

在本教程中，您将使用这些方法中的前两种方法。 DbFullSql Web 部署提供程序是一种旧方法，除了某些特定方案（例如从 SQL Server Compact 迁移到 SQL Server），不再建议使用此方法。

本教程中所示的方法适用于 SQL Server 数据库，而不是 SQL Server Compact。 有关如何部署 SQL Server Compact 数据库的信息，请参阅[使用 SQL Server Compact 的 Visual Studio Web 部署](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。

本教程中所示的方法要求使用 Web 部署发布方法。 如果希望使用不同的发布方法，如 FTP、文件系统或 FPSE，请参阅 Visual Studio 和 ASP.NET 的 Web 部署内容映射中的 "在 web[应用程序部署中单独部署数据库](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate)"。

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First 迁移

在实体框架版本4.3 中，Microsoft 引入了 Code First 迁移。 Code First 迁移自动执行对数据模型进行增量更改并将这些更改传播到数据库的过程。 在早期版本的 Code First 中，你通常会让实体框架在每次更改数据模型时删除并重新创建数据库。 这并不是开发中的问题，因为可以轻松地重新创建测试数据，但在生产环境中，通常需要在不删除数据库的情况下更新数据库架构。 迁移功能使 Code First 可以更新数据库，而无需删除并重新创建数据库。 您可以让 Code First 自动决定如何进行所需的架构更改，或者可以编写自定义更改的代码。 有关 Code First 迁移的简介，请参阅[Code First 迁移](https://msdn.microsoft.com/library/hh770484.aspx)。

在部署 web 项目时，Visual Studio 可以自动完成通过 Code First 迁移管理的数据库的部署过程。 当你创建发布配置文件时，你可以选择一个标记为 "执行 Code First 迁移（在应用程序启动时运行）" 的复选框。 此设置会导致部署过程在目标服务器上自动配置应用程序 Web.config 文件，以便 Code First 使用 `MigrateDatabaseToLatestVersion` 初始值设定项类。

在部署过程中，Visual Studio 不会对数据库执行任何操作。 部署后，当部署的应用程序首次访问数据库时，Code First 会自动创建数据库，或将数据库架构更新到最新版本。 如果应用程序实现了迁移种子方法，则该方法将在创建数据库或更新架构之后运行。

在本教程中，你将使用 Code First 迁移来部署应用程序数据库。

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web 部署提供程序

对于不由实体框架 Code First 管理的 SQL Server 数据库，可以在配置发布配置文件时，选中标记为 "更新数据库" 的复选框。 在初始部署期间，dbDacFx 提供程序将在目标数据库中创建表和其他数据库对象，以匹配源数据库。 在后续部署中，提供程序确定源数据库和目标数据库之间的差异，并更新目标数据库的架构以匹配源数据库。 默认情况下，访问接口不会进行任何导致数据丢失的更改，例如，在删除表或列时。

此方法不会自动部署数据库表中的数据，但你可以创建脚本来执行此操作，并将 Visual Studio 配置为在部署过程中运行它们。 在部署过程中运行脚本的另一个原因是要进行无法自动执行的架构更改，因为它们会导致数据丢失。

在本教程中，你将使用 dbDacFx 提供程序部署 ASP.NET 成员资格数据库。

## <a name="troubleshooting-during-this-tutorial"></a>本教程中的故障排除

在部署过程中发生错误时，或者如果部署的站点未正确运行，则错误消息不会始终提供明显的解决方案。 若要帮助解决一些常见问题，请[参阅故障排除参考页面](troubleshooting.md)。 如果您收到一条错误消息或在您完成本教程时无法正常工作，请务必查看故障排除页。

## <a name="comments-welcome"></a>欢迎评论

欢迎使用教程中的注释，并在每次更新本教程时，将对教程注释中提供的改进进行更正或建议。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>先决条件

本教程已针对以下产品编写：

- Windows 8 或 Windows 7。
- 带有[最新更新](https://go.microsoft.com/fwlink/?LinkId=272486)的 visual studio 2012 或 visual Studio 2012 Express for Web。
- [用于 Visual Studio 2012 的 Azure SDK](https://go.microsoft.com/fwlink/?LinkId=254364)

你可以通过使用 Visual Studio 2010 SP1 或 Visual Studio 2013 来遵循教程，但某些屏幕截图将有所不同，某些功能将有所不同。

如果使用 Visual Studio 2013，请安装[用于 Visual Studio 2013 的 AZURE SDK](https://go.microsoft.com/fwlink/?LinkID=324322)。

如果使用的是 Visual Studio 2010 SP1，请安装以下软件：

- [用于 Visual Studio 2010 的 Azure SDK](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx)。

根据计算机上已有的 SDK 依赖项的数量，安装 Azure SDK 可能需要很长时间，从几分钟到半小时或更长时间。 即使您计划发布到第三方托管提供程序（而不是 Azure），也需要 Azure SDK，因为该 SDK 包括 Visual Studio web 发布功能的最新更新。

> [!NOTE]
> 本教程是通过 Azure SDK 的版本1.8.1 编写的。 自那时起，已发布具有其他功能的较新版本。 教程已更新为提到这些功能，并链接到有关其详细信息的资源。

说明和屏幕截图基于 Windows 8，但教程说明了 Windows 7 的不同之处。

若要完成本教程，还需要使用其他一些软件，但不需要安装该软件。 本教程将引导你完成在需要时进行安装的步骤。

## <a name="download-the-sample-application"></a>下载示例应用程序

要部署的应用程序名为 Contoso 大学，并已为您创建。 它是大学网站的简化版本，它在[ASP.NET 站点上实体框架教程](https://asp.net/entity-framework/tutorials)中所述的 Contoso 大学应用程序上松松。

安装必备组件后，请下载[Contoso 大学 web 应用程序](https://go.microsoft.com/fwlink/p/?LinkId=282627)。 该 *.zip*文件包含项目的多个版本。 若要完成本教程中的步骤，请从位于C#文件夹中的项目开始。 若要查看该项目在教程结束时的外观，请在 ContosoUniversity 文件夹中打开该项目。

若要准备用于完成教程步骤的项目，请执行以下步骤：

1. 将 ContosoUniversity 解决方案文件从C#名为 ContosoUniversity 的文件夹中的文件夹保存到用于使用 Visual Studio 项目的任何文件夹中。

    默认情况下，这是 Visual Studio 2012 的下列文件夹：

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    （对于本教程中的屏幕截图，项目文件夹位于 `C`：驱动器的根目录中。）
2. 启动 Visual Studio 并打开项目。
3. 在**解决方案资源管理器**中，右键单击该解决方案，然后单击 " **EnableNuGet 包还原**"。
4. 生成解决方案。
5. 如果遇到编译错误，请手动还原 NuGet 包：

    1. 在**解决方案资源管理器**中，右键单击该解决方案，然后单击 "**管理解决方案的 NuGet 包**"。
    2. 在 "**管理 NuGet 包**" 对话框的顶部，你将看到**此解决方案缺少一些 NuGet 包。单击 "还原"。** 单击 "**还原**" 按钮。
    3. 重新生成解决方案。
6. 按 Ctrl+F5 运行应用程序。

    该应用程序将打开 Contoso 大学主页。

    ![主页开发](introduction/_static/image1.png)

    （可能会有等待时间，因为 Visual Studio 会启动 SQL Server Express 的 LocalDB 实例，如果该进程耗时过长，则可能会出现超时错误。 在这种情况下，只需重新启动该项目。）

可从菜单栏访问网站页面，并允许你执行以下功能：

- 显示学生统计信息（"关于" 页）。
- 显示、编辑、删除和添加学生。
- 显示和编辑课程。
- 显示和编辑指导员。
- 显示和编辑部门。

下面是几个代表页的屏幕截图。

![学生页开发](introduction/_static/image2.png)

![添加学生页开发](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>查看影响部署的应用程序功能

应用程序的以下功能会影响部署此应用程序的方式或部署方法。 本系列中的以下教程更详细地介绍了其中的每一项。

- Contoso 大学使用 SQL Server 数据库来存储应用程序数据，例如学生和指导员名称。 数据库包含测试数据和生产数据的组合，在您部署到生产环境时，您需要排除测试数据。
- 应用程序使用 ASP.NET 成员资格系统，该系统将用户帐户信息存储在 SQL Server 数据库中。 该应用程序定义了有权访问某些受限信息的管理员用户。 需要使用管理员帐户来部署成员资格数据库，而无需测试帐户。
- 应用程序使用第三方错误日志记录和报告实用工具。 此实用程序在必须与应用程序一起部署的程序集中提供。
- 错误日志记录实用工具将 XML 文件中的错误信息写入文件夹。 你必须确保 ASP.NET 在部署的站点下运行的帐户对此文件夹具有写入权限，并且你必须从部署中排除此文件夹。 （否则，可能会将测试环境中的错误日志数据部署到生产环境，/或者可能会删除生产错误日志文件。）
- 应用程序包括某些必须在已部署的*web.config*文件中更改的设置，具体取决于目标环境（测试、过渡或生产），以及其他必须根据生成配置（调试或发布）更改的设置。
- Visual Studio 解决方案包括一个类库项目。 只应部署此项目生成的程序集，而不部署项目本身。

## <a name="summary"></a>总结

在本系列教程的第一个教程中，已下载示例 Visual Studio 项目和查看的站点功能，这些功能会影响你部署应用程序的方式。 在以下教程中，您将通过设置其中的某些项来准备自动处理的部署。 您手动处理的其他人。

> [!div class="step-by-step"]
> [下一页](preparing-databases.md)
