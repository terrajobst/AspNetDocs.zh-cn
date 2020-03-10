---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: 生成和打包 Web 应用程序项目 |Microsoft Docs
author: jrjlee
description: 若要将 web 应用程序项目部署到远程服务器环境，您的第一个任务是生成项目并生成 web 部署 packa 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 1d0ee0264ce6461d7b0159f1a44de4de31e2d079
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463226"
---
# <a name="building-and-packaging-web-application-projects"></a>生成和打包 Web 应用程序项目

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 当你要将 web 应用程序项目部署到远程服务器环境时，你的第一个任务是生成项目并生成一个 web 部署包。 本主题介绍了如何在 web 应用程序项目中使用生成过程。 具体而言，它介绍：
> 
> - Web 发布管道（WPP）如何扩展生成过程以包含部署功能。
> - Internet Information Services （IIS） Web 部署工具（Web 部署）如何将您的 Web 应用程序转换为部署包。
> - 生成和打包过程的工作原理以及创建的文件。

在 Visual Studio 2010 中，WPP 支持 web 应用程序项目的生成和部署过程。 WPP 提供一组 Microsoft 生成引擎（MSBuild）目标，这些目标扩展 MSBuild 的功能，并使其能够与 Web 部署集成。 在 Visual Studio 中，你可以在 web 应用程序项目的属性页上查看此扩展功能。 "**打包/发布**" 网页与 "**包/发布 SQL** " 页一起，使你可以配置在生成过程完成后，如何打包 Web 应用程序项目以进行部署。

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP 如何工作？

如果你查看基于的 web 应用程序项目的项目C#文件，可以看到它导入了两个 .targets 文件。

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]

第一个**Import**语句对于所有视觉对象C#都是通用的。 此文件为*Microsoft*，其中包含特定于视觉对象C#的目标和任务。 例如，在此处C#调用编译器（**Csc**）任务。 然后， *microsoft. .targets*文件会导入*microsoft Common .targets*文件。 这定义了所有项目（如**生成**、**重新生成**、**运行**、**编译**和**清理**）公用的目标。 第二个**Import**语句特定于 web 应用程序项目。 然后， *WebApplication*文件会导入 " *web.config* " 文件。 *Microsoft* web.config 文件实质上*是*WPP。 它定义了用于调用 Web 部署来完成各种部署任务的目标，如**Package**和**MSDeployPublish**。

若要了解如何使用这些附加目标，请在 "联系人管理器" 示例解决方案中打开 "*发布*" 文件，并查看**BuildProjects**目标。

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]

此目标使用**MSBuild**任务来生成各种项目。 请注意**DeployOnBuild**和**DeployTarget**属性：

- **DeployOnBuild = true**属性本质上意味着 "我想要在生成成功完成时执行其他目标"。
- 当**DeployOnBuild**属性等于**True**时， **DeployTarget**属性标识想要执行的目标的名称。 在这种情况下，你要指定在生成项目后 MSBuild 会执行**包**目标。

**包**目标是在*web.config*文件中定义的。 实质上，此目标将获取 web 应用程序项目的生成输出，并将其转换为可发布到 IIS web 服务器的 web 部署包。

> [!NOTE]
> 若要在 Visual Studio 2010 中查看项目文件（例如<em>ContactManager</em>），首先需要从解决方案中卸载该项目。 在 "<strong>解决方案资源管理器</strong>" 窗口中，右键单击项目节点，然后单击 "<strong>卸载项目</strong>"。 再次右键单击项目节点，然后单击 "<strong>编辑</strong><em>[项目文件]</em>"）。 项目文件将以其原始 XML 格式打开。 请记住在完成后重新加载项目。  
> 有关 MSBuild 目标、任务和<strong>导入</strong>语句的详细信息，请参阅[了解项目文件](understanding-the-project-file.md)。 有关项目文件和 WPP 的更深入介绍，请参阅[Microsoft 生成引擎内部：使用 MSBuild 和 Team Foundation build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

## <a name="what-is-a-web-deployment-package"></a>什么是 Web 部署包？

当你通过使用 Visual Studio 2010 或直接使用 MSBuild 生成和部署 web 应用程序项目时，最终结果通常是*web 部署包*。 Web 部署包是一个 .zip 文件。 它包含 IIS 和 Web 部署重新创建 Web 应用程序所需的所有内容，包括：

- Web 应用程序的编译输出，其中包括内容、资源文件、配置文件、JavaScript 和级联样式表（CSS）资源等。
- Web 应用程序项目的程序集，以及解决方案中的任何引用项目。
- 用于生成在 web 应用程序中部署的任何数据库的 SQL 脚本。

生成 web 部署包后，可以通过多种方式将其发布到 IIS web 服务器。 例如，你可以通过将 Web 部署远程代理服务或目标 web 服务器上的 Web 部署处理程序作为目标来远程部署，或者可以使用 IIS 管理器在目标 web 服务器上手动导入包。 有关这些部署方法的详细信息，请参阅[选择正确的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。

## <a name="how-does-the-build-process-work"></a>生成过程是如何工作的？

这会显示生成和打包 web 应用程序项目时所发生的情况：

![](building-and-packaging-web-application-projects/_static/image2.png)

在生成 web 应用程序项目时，生成过程将生成一个名为 *[项目名称] 的文件。SourceManifest*。 除了项目文件和生成输出，此 *。SourceManifest*文件告知 Web 部署它需要包含在 Web 部署包中的内容。 使用这些输入，Web 部署会生成一个名为 *[项目名称] .zip*的 Web 部署包。

除了 web 部署包，生成过程还会生成两个文件，这些文件可帮助你使用包：

- *.Deploy .cmd*文件包含一组参数化的 Web 部署（msdeploy.exe）命令，可将 Web 部署包发布到远程 IIS Web 服务器。 使用适当的参数运行 *.deploy .cmd*文件，通常可以更快、更轻松地手动构造 msdeploy.exe 命令。
- *SetParameters*文件为 msdeploy.exe 命令提供了一组参数值。 这些值包括属性，如要将包部署到的 IIS web 应用程序的名称、在*web.config*文件中定义的任何服务终结点和连接字符串的值，以及在项目属性页上定义的任何部署属性值。

*SetParameters*文件是管理部署过程的关键。 此文件是根据 web 应用程序项目的内容动态生成的。 例如，如果将连接字符串添加到*web.config 文件，* 则生成过程将自动检测连接字符串，并相应地参数化部署，并在*SetParameters*文件中创建一个条目，以允许您在部署过程中修改连接字符串。 下一主题 "[配置 Web 包部署的参数](configuring-parameters-for-web-package-deployment.md)" 将更详细地说明此文件的角色，并介绍在生成和部署过程中修改它的不同方法。

> [!NOTE]
> 在 Visual Studio 2010 中，WPP 不支持在打包前预编译 web 应用程序中的页面。 Visual Studio 的下一个版本和 WPP 将包括将 web 应用程序预编译为打包选项的功能。

## <a name="conclusion"></a>结束语

本主题概述了 Visual Studio 2010 中 web 应用程序项目的生成和打包过程。 它介绍了如何通过 WPP 从 MSBuild 调用 Web 部署命令，并说明了生成和打包过程的工作方式。

创建 web 部署包后，下一步是部署它。 有关此内容的详细信息，请参阅[为 Web 包部署](configuring-parameters-for-web-package-deployment.md)和[部署 Web 包](deploying-web-packages.md)配置参数。

## <a name="further-reading"></a>其他阅读材料

本教程中的后续主题（[为 Web 包部署](configuring-parameters-for-web-package-deployment.md)和[部署 Web](deploying-web-packages.md)包配置参数）提供了有关如何使用已创建的 web 包的指导。 本系列中的最后一个教程是[高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)，它提供有关如何自定义打包过程和对其进行故障排除的指导。

有关项目文件和 WPP 的更深入介绍，请参阅[Microsoft 生成引擎内部：使用 MSBuild 和 Team Foundation build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一页](understanding-the-build-process.md)
> [下一页](configuring-parameters-for-web-package-deployment.md)
