---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 从部署中排除文件和文件夹 |Microsoft Docs
author: jrjlee
description: 本主题介绍在生成和打包 web 应用程序项目时，如何从 web 部署包中排除文件和文件夹。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438416"
---
# <a name="excluding-files-and-folders-from-deployment"></a>从部署中排除文件和文件夹

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍在生成和打包 web 应用程序项目时，如何从 web 部署包中排除文件和文件夹。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="overview"></a>概述

当您在 Visual Studio 2010 中生成 web 应用程序项目时，Web 发布管道（WPP）允许您通过将已编译的 web 应用程序打包到可部署的 web 包中来扩展此生成过程。 然后，可以使用 Internet Information Services （IIS） Web 部署工具（Web 部署）将此 web 包部署到远程 IIS web 服务器，或通过 IIS 管理器手动导入 web 包。 此打包过程在[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中进行了介绍。

那么，如何控制 web 包中包含的内容呢？ Visual Studio 中的项目设置，通过基础项目文件，为很多方案提供足够的控制权。 但是，在某些情况下，可能需要将 web 包的内容定制为特定的目标环境。 例如，你可能想要在将应用程序部署到测试环境时包括日志文件的文件夹，但在将应用程序部署到过渡环境或生产环境时排除文件夹。 本主题将演示如何执行此操作。

## <a name="what-gets-included-by-default"></a>默认情况下包含哪些内容？

当你在 Visual Studio 中配置你的 web 应用程序项目属性时，"**包/发布**" 网页上的 "**要部署的项目**" 列表使你可以指定要包括在 web 部署包中的内容。 默认情况下，此设置为**仅限运行此应用程序所需的文件**。

![](excluding-files-and-folders-from-deployment/_static/image1.png)

如果仅选择**运行此应用程序所需的文件**，WPP 将尝试确定哪些文件应添加到 web 包中。 这包括：

- 项目的所有生成输出。
- 任何标记有**Content**的生成操作的文件。

> [!NOTE]
> 确定要包含的文件的逻辑包含在此文件中：   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ （OnlyFilesToRunTheApp）*

## <a name="excluding-specific-files-and-folders"></a>排除特定的文件和文件夹

在某些情况下，您需要更精细地控制部署哪些文件和文件夹。 如果您知道您要提前排除哪些文件，并且排除适用于所有目标环境，则您可以简单地将每个文件的**生成操作**设置为 "**无**"。

**从部署中排除特定文件**

1. 在 "**解决方案资源管理器**" 窗口中，右键单击该文件，然后单击 "**属性**"。
2. 在 "**属性**" 窗口的 "**生成操作**" 行中，选择 "**无**"。

但是，这种方法并不是很方便。 例如，你可能想要根据目标环境以及从 Visual Studio 外部包含哪些文件和文件夹。 例如，在 "联系人管理器" 示例解决方案中，查看 ContactManager 项目的内容：

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- 内部文件夹包含一些 SQL 脚本，开发人员可以使用这些脚本来创建、删除和填充用于开发的本地数据库。 应将此文件夹中的任何内容部署到过渡环境或生产环境中。
- Scripts 文件夹包含多个 JavaScript 文件。 其中的许多文件纯粹是为了支持调试或在 Visual Studio 中提供 IntelliSense。 其中一些文件不应部署到过渡环境或生产环境中。 但是，你可能希望将它们部署到开发人员测试环境中，以便于进行故障排除。

虽然您可以操作项目文件以排除特定文件和文件夹，但有一种更简单的方法。 WPP 包含一种机制，可通过生成名为**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**的项列表来排除文件和文件夹。 您可以通过将您自己的项添加到这些列表来扩展此机制。 要执行此操作，需要完成以下高级步骤：

1. 在与项目文件相同的文件夹中创建一个名为 *[项目名称]* 的自定义项目文件。

    > [!NOTE]
    > .Csproj&#x2014;文件需要与你的 web 应用程序*项目文件*&#x2014;位于同一文件夹中，例如， *ContactManager*，而不是与你用来控制生成和部署过程的任何自定义项目文件位于同一文件夹中。
2. 在 *. .targets*文件中，添加一个**ItemGroup**元素。
3. 在**ItemGroup**元素中，添加**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**项，以根据需要排除特定的文件和文件夹。

*这是此文件的*基本结构：

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

请注意，每个项都包含名为**FromTarget**的项元数据元素。 这是一个可选值，不会影响生成过程;它仅用于指示当有人查看生成日志时省略特定文件或文件夹的原因。

## <a name="excluding-files-and-folders-from-a-web-package"></a>从 Web 包中排除文件和文件夹

下一过程演示了如何在生成项目时，将*wpp*文件添加到 web 应用程序项目，以及如何使用该文件从 web 包中排除特定的文件和文件夹。

**从 web 部署包中排除文件和文件夹**

1. 在 Visual Studio 2010 中打开解决方案。
2. 在 "**解决方案资源管理器**" 窗口中，右键单击 web 应用程序项目节点（例如**ContactManager**），指向 "**添加**"，然后单击 "**新建项**"。
3. 在 "**添加新项**" 对话框中，选择 " **XML 文件**" 模板。
4. 在 "**名称**" 框中，键入 *[项目名称] * *. wpp** （例如， **ContactManager**），然后单击 "**添加**"。

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > 如果将新项添加到项目的根节点，则会在与项目文件相同的文件夹中创建该文件。 可以通过在 Windows 资源管理器中打开该文件夹来验证这一点。
5. 在文件中，添加**项目**元素和**ItemGroup**元素：

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. 如果要从 web 包中排除文件夹，请将**ExcludeFromPackageFolders**元素添加到**ItemGroup**元素：

   1. 在**Include**特性中，提供要排除的文件夹的分号分隔列表。
   2. 在**FromTarget** metadata 元素中，提供一个有意义的值，用于指示排除文件夹的原因，例如， *.targets*文件的名称。

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. 如果要从 web 包中排除文件，请将**ExcludeFromPackageFiles**元素添加到**ItemGroup**元素：

   1. 在**Include**特性中，提供要排除的文件的列表（以分号分隔）。
   2. 在**FromTarget** metadata 元素中，提供一个有意义的值，用于指示排除文件的原因，例如， *.targets*文件的名称。

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. *[项目名称] wpp*文件现在应如下所示：

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. 保存并关闭 *[项目名称] .targets*文件。

下一次生成和打包 web 应用程序项目时，WPP 会自动检测 *.targets*文件。 您指定的任何文件和文件夹不会包含在 web 包中。

## <a name="conclusion"></a>结束语

本主题介绍了如何在生成 web 包时排除特定文件和文件夹，方法是在与 web 应用程序项目文件相同的文件夹中创建一个自定义的 *.targets*文件。

## <a name="further-reading"></a>其他阅读材料

有关使用自定义 Microsoft 生成引擎（MSBuild）项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。 有关打包和部署过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)、[配置 web 包部署的参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)和[部署 web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

> [!div class="step-by-step"]
> [上一页](deploying-membership-databases-to-enterprise-environments.md)
> [下一页](taking-web-applications-offline-with-web-deploy.md)
