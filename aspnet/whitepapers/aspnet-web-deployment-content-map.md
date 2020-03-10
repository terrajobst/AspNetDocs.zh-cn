---
uid: whitepapers/aspnet-web-deployment-content-map
title: ASP.NET Web 部署-建议的资源 |Microsoft Docs
author: rick-anderson
description: 本主题提供有关如何使用 Visual Studio 2010 （Visual Web De ...）将 ASP.NET web 应用程序部署（发布）到 IIS 的文档资源的链接
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517274"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>ASP.NET Web 部署 - 推荐的资源

> 本主题提供有关如何使用 Visual Studio 2010、Visual Web Developer 2010 和更高版本将 ASP.NET web 应用程序部署（发布）到 IIS 的文档资源的链接。
> 
> 如果你知道一篇非常有用的博客文章、 [stackoverflow](http://stackoverflow.com)或任何其他链接，请[向我们发送一封电子邮件](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map)，其中包含该链接。
> 
> > [!NOTE] 
> > 
> > 其中的许多资源只介绍了安装最新版本的[Visual Studio Web 发布更新](https://go.microsoft.com/fwlink/?LinkID=208120)时可用的部署功能。 某些功能仅在 Visual Studio 2012 或 Visual Studio 2013 中可用。

本主题包含以下各节：

- [了解 web 项目的部署选项](#understanding)
- [查找 ASP.NET 应用程序的宿主提供程序](#findinghosting)
- [从 Visual Studio 部署 web 应用程序](#fromvs)
- [通过创建和安装 web 部署包来部署 web 应用程序](#package)
- [使用持续集成（CI）过程部署 web 应用程序](#ci)
- [在部署过程中使用 web.config 转换更改目标 Web.config 文件或 app.config 文件中的设置](#transforms)
- [在部署过程中使用 Web 部署参数更改目标 Web 应用程序中的设置](#webdeployparms)
- [在部署过程中确保应用程序处于脱机状态](#appoffline)
- [将数据库或数据库更改作为 web 应用程序部署的一部分进行部署](#databasewithweb)
- [独立于 web 应用程序部署部署数据库](#databaseseparate)
- [部署使用 ASP.NET 应用程序服务（例如，成员身份和事件探查）的 web 应用程序](#aspnetmembership)
- [针对部署进行预编译](#precompiling)
- [部署 intranet web 应用程序](#intranet)
- [自动执行不自动化的常见部署任务](#automating)
- [配置 web 服务器，使开发人员可以使用 Web 部署](#configuringservers)
- [为宿主提供程序配置服务器](#hostingprovider)
- [部署问题疑难解答](#troubleshooting)
- [获取特定部署问题的帮助](#gettinghelp)
- [其他资源](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>了解 web 项目的部署选项

- [Visual Studio 和 ASP.NET （MSDN）的 Web 部署概述](https://msdn.microsoft.com/library/dd394698.aspx)。
- [如何部署 Microsoft Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)网站。 介绍用于将 web 项目部署到 Microsoft Azure 网站的资源的选项和链接，包括[持续交付](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)（从[源代码管理](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)自动化）以及使用 Visual Studio。
- [Visual Studio 2012 Web 发布改进](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md)（视频作者： Scott Hanselman）。
- [VS 2010 中的 Web 部署概述文章](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html)（Vishal Joshi 的博客）。 更早的博客文章（但它链接到的某些 Visual Studio 2010 资源）的信息仍与 Visual Studio 2012 相关。

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>查找 ASP.NET 应用程序的宿主提供程序

- [ASP.NET 托管](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>从 Visual Studio 部署 web 应用程序

- [如何部署 Microsoft Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)网站。 说明选项并提供指向用于将 web 项目部署到 Microsoft Azure 网站的资源的链接。 包含有关从 Visual Studio 进行部署的部分。
- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部分教程系列介绍了如何部署包含 SQL Server 数据库的 web 应用程序。 对于数据库部署，使用 dbDacFx 提供程序和 Entity Framework Code First 迁移。 还包括有关[web.config 文件转换](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)、[部署单个文件](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles)、[命令行部署](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md)的信息，以及[如何通过编辑 .pubxml 文件自定义 Visual Studio web 发布管道](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)。 适用于所有 ASP.NET web 项目，包括 Web 窗体、MVC 和 Web API。）
- [如何：在 Visual studio 中使用一键式发布来部署 Web 项目](https://msdn.microsoft.com/library/dd465337.aspx)（Visual Studio Web 发布向导的参考信息）
- [使用 Visual Studio SQL Server Compact 部署 ASP.NET Web 应用程序](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。 这是使用本部分顶部列出的 Visual Studio 的较早版本的**ASP.NET Web 部署**。 目前主要用于了解如何部署 SQL Server Compact 数据库以及如何从 SQL Server Compact 迁移到 SQL Server 的完整版本的信息。
- [使用存储表、队列和 blob 的 .Net 多层应用程序](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)（Microsoft Azure 站点）。 5部分系列教程演示如何创建 MVC 项目并将其部署到 Microsoft Azure 云服务。

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>通过创建和安装 web 部署包来部署 web 应用程序

- [如何：在 Visual Studio 中创建 Web 部署包](https://msdn.microsoft.com/library/dd465323.aspx)（MSDN）。
- [如何：使用 Visual Studio （MSDN）创建的 deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。
- [使用 Web 部署包部署到开发环境中的 IIS 和第三方主机](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx)（Sayed Hashimi 的博客）。 如何使用 IIS 管理器在本地计算机上的 IIS 中以及支持 IIS 管理器进行远程管理的托管公司上安装部署包。
- [从 Visual Studio 2010 生成 Web 部署包](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010)（IIS.NET 网站）。 包含有关创建和安装命令行包的说明。
- [发布到任何位置](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx)（Sayed Hashimi 的博客）。 引入了一个 NuGet 包，它可以自动完成为多个目标环境转换 web.config 文件的过程，以便可以将一个包部署到多个服务器。 另请参阅[PackageWeb 视频](https://www.youtube.com/watch?v=-LvUJFI8CzM)By Sayed Hashimi。

另请参阅下一节。

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>使用持续集成（CI）过程部署 web 应用程序

- [持续集成和持续交付（通过 Microsoft Azure 构建实际的云应用）。](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 引入持续集成和持续交付的电子书。
- [如何部署 Microsoft Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy)网站。 介绍用于将 web 项目部署到 Microsoft Azure 网站的资源选项和链接。 包含有关从源代码管理自动部署的部分。
- [在企业方案中部署 Web 应用程序](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 40部分教程系列介绍了如何使用 Visual Studio 2010 和 Team Foundation Server 2010 在 CI 过程中自动执行部署。
- 在[Microsoft 生成引擎中：通过 Sayed Hashimi 和 William Bartholomew 使用 MSBuild 和 Team Foundation build](http://msbuildbook.com)。 这是一本书，而不是 web 资源，但它是学习如何为持续集成方案配置 MSBuild 的重要指南。
- [MSBuild 扩展包](https://github.com/mikefourie/MSBuildExtensionPack)。 包括部署任务。
- [Team Foundation Build 自定义指南](https://aka.ms/vsarsolutions)。 通过 ALM Rangers 设置 Team Foundation Server 介绍 web 部署，包括教程和视频。
- [SlowCheetah 来自 CI 服务器的 XML 转换](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx)（Sayed Hashimi 的博客）。 介绍如何使用 SlowCheetah，它是用于转换 app.config 和其他 XML 文件的 Visual Studio 外接程序。

另请参阅本页后面的在[部署期间确保应用程序脱机](aspnet-web-deployment-content-map.md#appoffline)。

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>在部署过程中使用 web.config 转换更改目标 Web.config 文件或 app.config 文件中的设置

- Web.config[文件转换](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)。
- [使用 Visual Studio （MSDN）部署 Web 项目的 Web.config 转换语法](https://msdn.microsoft.com/library/dd465326.aspx)。
- [Web 工具 2012.2-web.config 转换](https://www.youtube.com/watch?v=HdPK8mxpKEI)（使用 Sayed Hashimi 的 YouTube 视频）。 演示如何设置和预览 Web.config 转换。
- [如何实现禁用 web.config 转换？](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) （MSDN）。
- [何时应使用 Web 部署参数而不是 web.config 转换？](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) （MSDN）。
- [Codeplex.com 上发布的 XDT （XML 文档转换）](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) （.Net Web 开发和工具博客）。 公布 web.config 文件转换引擎源代码的可用性，并列出一些使用它的工具。
- [Microsoft Azure 网站：应用程序字符串和连接字符串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)（Microsoft Azure 博客）。 如果目标环境是 Microsoft Azure 网站并且你想要转换 `appSettings` 或 `connectionStrings`，则 web.config 的替代方法。

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>在部署过程中使用 Web 部署参数更改目标 Web 应用程序中的设置

- [如何：在 Web 部署包（MSDN）中使用 Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。
- [Msdeploy.exe：如何基于发布配置文件（Sayed Hashimi 的博客）在发布时更新应用设置](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx)。 演示如何将 Web deploy 参数集成到 Visual Studio 发布配置文件中。
- [Web 部署参数](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization)化（IIS.NET 网站）。
- [Web 部署参数化操作](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html)（Vishal Joshi 的博客）。
- [Web 部署参数化与 Web.config 转换](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html)（Vishal Joshi 的博客）。
- [Microsoft Azure 网站：应用程序字符串和连接字符串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)（Microsoft Azure 博客）。 如果目标环境是 Microsoft Azure 网站并且你想要将 `appSettings` 或 `connectionStrings`参数化，则可以选择使用 Web 部署参数。

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>在部署过程中确保应用程序处于脱机状态

- [使用 Visual Studio 的 ASP.NET Web 部署：部署代码更新](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 请参阅在**部署期间使应用程序脱机**的部分。
- [在发布之前使应用程序脱机](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing)（IIS.net 网站）。 介绍 Web 部署3.0 中内置的一项功能，该功能自动处理\_脱机 .htm 文件的应用程序。 此功能不适用于自定义应用\_脱机 .htm 文件。
- [如何在发布过程中使 web 应用处于脱机状态](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)（Sayed Hashimi 的博客）。 如何自动执行将自定义应用程序\_脱机文件的过程。
- [适用于应用程序脱机和 usechecksum](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx) （Microsoft Web 开发博客）的 Web 发布更新。 自动使用应用\_脱机 .htm 文件的另一个选项。
- [Web 部署 3.5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) （IIS.net 站点）。 Web 部署3.5 中的新功能，适用于自定义应用\_脱机 .htm 文件。

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>将数据库或数据库更改作为 web 应用程序部署的一部分进行部署

- [在 Visual Studio 中配置数据库部署](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)（MSDN）。 使用 web 项目部署数据库的选项概述。
- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部分教程系列使用 dbDacFx 提供程序和 Entity Framework Code First 迁移显示数据库部署。
- [如何：在 Visual Studio 中使用一键式发布来部署 Web 项目](https://msdn.microsoft.com/library/dd465337.aspx)（MSDN）。
- [将包含成员资格、OAuth 和 SQL 数据库的 Secure ASP.NET MVC 5 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)网站。 一种用于生成和部署应用程序的长教程，该应用程序使用单个 SQL Server 数据库来实现成员身份和应用程序数据。
- [使用 Visual Studio SQL Server Compact 部署 ASP.NET Web 应用程序](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。 12部分教程系列介绍了如何部署 SQL Server Compact 数据库以及如何从 SQL Server Compact 迁移到 SQL Server 的完整版本。

另请参阅本页面前面的使用持续集成（CI）过程创建和安装 web 部署包和部署 web 应用程序，以部署 web 应用程序。

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>独立于 web 应用程序部署部署数据库

- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) （MSDN）。
- [将数据包含在 SQL Server 数据库项目中](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)（SQL Server Data Tools 团队博客）。 如何在部署数据库时部署架构和数据。
- [如何将数据库部署到 Windows Azure](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) （Microsoft Azure 站点）
- [将数据库迁移到 Windows AZURE SQL Database （以前称为 SQL Azure）](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) （MSDN）。
- [使用 SSDT 将数据库迁移到 SQL Azure](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx) （SQL Server Data Tools 团队博客）。
- [将以数据为中心的应用程序迁移到 Microsoft Azure](https://msdn.microsoft.com/library/jj156154.aspx) （MSDN）。
- [将 SQL Server 数据库迁移到 Windows AZURE SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) （MSDN）。

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>部署使用 ASP.NET 应用程序服务（例如，成员身份和事件探查）的 web 应用程序

- [将包含成员资格、OAuth 和 SQL 数据库的 Secure ASP.NET MVC 5 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)网站。 一种用于生成和部署应用程序的长教程，该应用程序使用单个 SQL Server 数据库来实现成员身份和应用程序数据。
- [ASP.NET Identity](https://asp.net/identity/)。 ASP.NET Identity 的资源。
- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 12部分系列教程演示如何部署 ASP.NET 成员资格数据库。
- [配置使用应用程序服务的网站](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md)。 对于网站项目，但也适用于 web 应用程序项目。
- [生产网站上的用户和角色](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md)。 对于网站项目，但也适用于 web 应用程序项目。

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>针对部署进行预编译

- [ASP.NET Web 应用程序项目预编译概述](https://msdn.microsoft.com/library/aa983464.aspx)（MSDN）。
- [打包/发布 Web 选项卡，项目属性](https://msdn.microsoft.com/library/dd410108.aspx)（MSDN）。
- ["高级预编译设置" 对话框](https://msdn.microsoft.com/library/hh475319.aspx)（MSDN）。

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>部署 intranet web 应用程序

- [将本地组织身份验证选项（ADFS）与 Visual Studio 2013 中的 ASP.NET](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) （Vittorio Bertocci 的博客）结合使用。
- [如何使用 ASP.NET MVC 创建 Intranet 站点](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)（MSDN）。 旧版演练写入 for Visual Studio 2010 不反映 Visual Studio 2013 中引入的 intranet 项目模板的重大更改。

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>自动执行不自动化的常见部署任务

- [使用 Visual Studio 的 ASP.NET Web 部署：部署额外文件](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)。
- [设置 Web 发布的文件夹权限](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)（Sayed Hashimi 的博客）。
- [如何扩展目标文件以包含 web 项目包的注册表设置](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx)（Web 开发工具博客）。
- [扩展 XML （web.config）转换](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx)（Sayed Hashimi 的博客）。 演示如何创建自定义 XDT 转换。
- [Web 部署工具（msdeploy.exe）自定义提供程序采用 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) （Sayed Hashimi 的博客）。 演示如何创建 Web 部署的自定义提供程序。
- [如何打包和部署 COM 组件](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx)（Web 开发工具博客）。
- [如何打包 .net 程序集](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx)（Web 开发工具博客）。 如何将程序集部署到 GAC。
- [编写所有内容的脚本-将 Windows AZURE VM 用于 IIS、Web 部署和其他内容](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff)（Tugberk Ugurlu 的博客）。

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>配置 web 服务器，使开发人员可以使用 Web 部署

- [为管理员和非管理员部署（IIS.net 站点）安装和配置 Web 部署](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)。

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>为宿主提供程序配置服务器

- [Microsoft ASP.NET 4 托管部署指南](https://go.microsoft.com/fwlink/?LinkId=191365)（Microsoft 下载中心）。
- [生成配置文件 XML 文件](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file)（IIS.net 网站）。

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>部署问题疑难解答

- [在 Visual Studio 中对 Microsoft Azure 网站进行故障排除](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)（Microsoft Azure 站点）。
- [使用 Visual Studio 的 ASP.NET Web 部署：故障排除](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md)。
- [排查 Web 部署的常见问题](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy)。
- [Web 部署错误代码](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes)（IIS.net 网站）。
- [Visual Studio 和 ASP.NET （MSDN）的 Web 部署常见问题解答](https://msdn.microsoft.com/library/ee942158.aspx)。
- [IIS 与 ASP.NET 开发服务器之间的核心差异](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。
- [开发和生产之间的常见配置差异](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md)。
- [在中等信任环境中托管 ASP.NET 的应用程序](http://www.4guysfromrolla.com/articles/100307-1.aspx)（Rolla 站点的4个专家）。

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>获取特定部署问题的帮助

- [ASP.NET 配置和部署论坛](https://forums.asp.net/26.aspx/1?Configuration and Deployment)。
- [StackOverflow.com](http://www.StackOverflow.com)。

<a id="additional"></a>

## <a name="additional-resources"></a>其他资源

本部分提供了指向其他资源的链接，这些资源有助于详细了解如何使用 Visual Studio 和 IIS 部署工具。

以下博客经常包含有关 Visual Studio web 部署的信息：

- [Microsoft 博客上的 Web 开发工具](https://blogs.msdn.com/b/webdevtools/)。
- [Sayed Hashimi 的博客](http://www.sedodream.com/)。

以下资源提供了有关 Web 部署（Visual Studio 用于执行 Web 应用程序项目部署任务的 IIS 框架）的文档。 你可以在 IIS.net 网站上的[Web 部署工具论坛](https://go.microsoft.com/fwlink/?LinkId=149411)中提问有关 Web 部署的问题。

- [Web 部署简介](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy)。
- [安装和配置 Web 部署](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)。
- [用于自动 Web 部署安装程序的 PowerShell 脚本](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup)。
- [Web 部署工具](https://go.microsoft.com/fwlink/?LinkId=151481)。 TechNet 站点上 Web 部署文档的顶级目录节点。 包含有用的参考信息，但大部分 TechNet 页面尚未更新多年。
- [Web.config 命名空间](https://go.microsoft.com/fwlink/?LinkId=148630)。 API 文档，自版本1.0 起尚未更新。
- [Microsoft Web 部署团队博客](https://blogs.iis.net/msdeploy/default.aspx)。
- [IIS.net 网站中的 "发布" 选项卡](https://www.iis.net/learn/publish)。
