---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 打包过程疑难解答 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何通过使用 M ... 中的 EnablePackageProcessLoggingAndAssert 属性来收集有关打包过程的详细信息。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509750"
---
# <a name="troubleshooting-the-packaging-process"></a>打包过程故障排除

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何通过使用 Microsoft 生成引擎（MSBuild）中的**EnablePackageProcessLoggingAndAssert**属性来收集有关打包过程的详细信息。
> 
> 将**EnablePackageProcessLoggingAndAssert**属性设置为**true**时，MSBuild 将：
> 
> - 向生成日志添加有关打包过程的其他信息。
> - 在某些情况下（例如，如果在打包列表中找到了重复的文件），记录错误。
> - 在*项目名称*\_Package 文件夹中创建日志目录，并使用该目录记录有关要打包的文件的信息。
> 
> 如果打包过程失败，或者 web 部署包不包含所需的文件，则可以使用此信息对过程进行故障排除，查明出现问题的位置。
> 
> > [!NOTE]
> > 仅当使用**调试**配置生成项目时， **EnablePackageProcessLoggingAndAssert**属性才适用。 在其他配置中将忽略该属性。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>了解 EnablePackageProcessLoggingAndAssert 属性

[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)介绍了 Web 发布管道（WPP）如何提供一组可扩展 msbuild 功能的 msbuild 目标，并使其能够与 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web 部署）集成。 打包 web 应用程序项目时，会调用 WPP 目标。

许多这些 WPP 目标包括在**EnablePackageProcessLoggingAndAssert**属性设置为**true**时记录附加信息的条件逻辑。 例如，如果你查看**包**目标，可以看到它会创建一个附加的日志目录，并将文件列表写入文本文件，如果**EnablePackageProcessLoggingAndAssert**等于**true**。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> 此 WPP 目标是在 "% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web" 文件夹中的 " *web.config* " 文件中定义的。 可在 Visual Studio 2010 或任何 XML 编辑器中打开此文件并查看目标。 请注意不要修改该文件的内容。

## <a name="enabling-the-additional-logging"></a>启用其他日志记录

可以通过多种方式提供**EnablePackageProcessLoggingAndAssert**属性的值，具体取决于生成项目的方式。

如果从命令行生成项目，则可以将**EnablePackageProcessLoggingAndAssert**属性的值作为命令行参数提供：

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

如果要使用自定义项目文件来生成项目，可以在**MSBuild**任务的**Properties**特性中包括**EnablePackageProcessLoggingAndAssert**值：

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

如果使用 Team Foundation Server （TFS）生成定义生成项目，可以在 " **MSBuild 参数**" 行中为**EnablePackageProcessLoggingAndAssert**属性提供值：![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> 有关创建和配置生成定义的详细信息，请参阅[创建支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

或者，如果要在每个生成中包含包，可以修改 web 应用程序项目的项目文件，以将**EnablePackageProcessLoggingAndAssert**属性设置为**true**。 应将属性添加到 .csproj 或 .vbproj 文件中的第一个**PropertyGroup**元素。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>查看日志文件

当你生成并打包**EnablePackageProcessLoggingAndAssert**设置为**true**的 web 应用程序项目时，MSBuild 将在*项目名称*\_package 文件夹中创建一个名为 Log 的附加文件夹。 日志文件夹包含各种文件：

![](troubleshooting-the-packaging-process/_static/image2.png)

你看到的文件列表将因你的项目和生成过程中的功能而异。 但是，这些文件通常用于在过程的各个阶段记录 WPP 正在收集的文件的列表：

- *PreExcludePipelineCollectFilesPhaseFileList*文件列出了 MSBuild 在为排除指定的任何文件被删除之前收集的文件。
- 删除为排除指定的任何文件后， *AfterExcludeFilesFilesList*文件将包含已修改的文件列表。

    > [!NOTE]
    > 有关从打包过程中排除文件和文件夹的详细信息，请参阅[从部署中排除文件和文件夹](excluding-files-and-folders-from-deployment.md)。
- *AfterTransformWebConfig*文件列出了在*执行任何 web.config*转换后为打包收集的文件。 在此列表中，所有特定于配置的*web.config*转换文件（如*web.config*和 web.config）都将从要打包的文件列表中*排除。* 单个转换后的*web.config*将包含在其位置。
- *PostAutoParameterizationWebConfigConnectionStrings*文件包含已参数化*web.config 文件中*的连接字符串之后的文件列表。 在部署包时，可以通过此过程将连接字符串替换为目标环境的正确设置。
- *Prepackage*文件包含要包含在包中的已完成的预生成文件列表。

> [!NOTE]
> 其他日志文件的名称通常对应于 WPP 目标。 你可以通过查看% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的 " *Microsoft* web.config" 文件来查看这些目标。

如果你的 web 包的内容不是你所期望的内容，则查看这些文件可能是在处理过程中的哪个点发生错误的有用方法。

## <a name="conclusion"></a>结束语

本主题介绍了如何使用 MSBuild 中的**EnablePackageProcessLoggingAndAssert**属性对打包过程进行故障排除。 它介绍了向生成过程提供属性值的不同方法，并介绍了在将属性设置为**true**时所记录的其他信息。

## <a name="further-reading"></a>其他阅读材料

有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。 有关 WPP 以及它如何管理打包过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。 有关如何从 web 部署包中排除特定文件和文件夹的指导，请参阅[从部署中排除文件和文件夹](excluding-files-and-folders-from-deployment.md)。

> [!div class="step-by-step"]
> [上一页](running-windows-powershell-scripts-from-msbuild-project-files.md)
