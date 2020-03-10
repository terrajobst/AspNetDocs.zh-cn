---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: 使 Web 应用程序与 Web 部署脱机 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Internet Information Services （IIS） Web 部署在自动部署期间使 web 应用程序脱机：
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: ba60664a0c3daa0650cd7e7cfc4ab9da08df3440
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422210"
---
# <a name="taking-web-applications-offline-with-web-deploy"></a>使用 Web 部署使 Web 应用程序脱机

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web 部署）在自动部署期间使 web 应用程序脱机。 在部署完成之前，浏览到 web 应用程序的用户会重定向到*应用\_脱机 .htm*文件。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

在许多情况下，你需要在对相关组件（如数据库或 web 服务）进行更改时，使 web 应用程序脱机。 通常，在 IIS 和 ASP.NET 中，可通过将名为 App 的文件放在 IIS 网站或 web 应用程序的根文件夹中 *\_"脱机*" 来实现此目的。 *应用\_脱机*文件是一个标准 HTML 文件，通常会包含一条简单消息，通知用户由于维护，该站点暂时不可用。 尽管*应用程序\_脱机*文件位于网站的根文件夹中，但 IIS 会自动将所有请求重定向到该文件。 完成更新后，将 *\_脱机*文件删除应用，然后该网站会照常恢复请求。

当你使用 Web 部署对目标环境执行自动或单步部署时，你可能希望将*应用\_脱机 .htm*文件添加并删除到你的部署过程中。 为此，需要完成以下高级任务：

- 在用于控制部署过程的 Microsoft 生成引擎（MSBuild）项目文件中，创建一个 MSBuild 目标，以便在启动任何部署任务之前将*应用\_脱机 .htm*文件复制到目标服务器。
- 添加另一个 MSBuild 目标，用于在所有部署任务完成时，从目标服务器中删除*应用\_脱机 .htm*文件。
- 在 web 应用程序项目中，创建一个*wpp*文件，以确保在调用 Web 部署时将*应用\_脱机*文件添加到部署包。

本主题将演示如何执行这些过程。 本主题中的任务和演练假设已创建一个解决方案，该解决方案至少包含一个 web 应用程序项目，并使用自定义项目文件来控制部署过程，如[企业中的 Web 部署中](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)所述。 或者，您可以使用 "[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)" 示例解决方案来执行主题中的示例。

## <a name="adding-an-app_offline-file-to-a-web-application-project"></a>向 Web 应用程序项目添加应用程序\_脱机文件

需要完成的第一个任务是将*应用\_脱机*文件添加到 web 应用程序项目：

- 若要防止文件干扰开发过程（不希望应用程序永久脱机），应将其称为*应用程序\_"脱机*"。 例如，可以将文件*应用命名\_offline-template*。
- 若要防止文件按原样部署，应将生成操作设置为 "**无**"。

**向 web 应用程序项目添加应用\_脱机文件**

1. 在 Visual Studio 2010 中打开解决方案。
2. 在 "**解决方案资源管理器**" 窗口中，右键单击 web 应用程序项目，指向 "**添加**"，然后单击 "**新建项**"。
3. 在 "**添加新项**" 对话框中，选择 " **HTML 页**"。
4. 在 "**名称**" 框中，键入**App\_offline-template**，然后单击 "**添加**"。

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. 添加一些简单的 HTML，通知用户该应用程序不可用，然后保存该文件。 不要包含任何服务器端标记（例如，以 "asp：" 为前缀的任何标记）。 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. 在 "**解决方案资源管理器**" 窗口中，右键单击新文件，然后单击 "**属性**"。
7. 在 "**属性**" 窗口的 "**生成操作**" 行中，选择 "**无**"。

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-app_offline-file"></a>部署和删除应用\_脱机文件

下一步是修改部署逻辑，以便在部署过程开始时将文件复制到目标服务器，并将其删除。

> [!NOTE]
> 下一个过程假定您使用自定义 MSBuild 项目文件来控制您的部署过程，如[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述。 如果要直接从 Visual Studio 进行部署，则需要使用其他方法。 Sayed Ibrahim Hashimi 介绍了在[发布过程中如何使 Web 应用脱机](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)的一种方法。

若要将*应用\_脱机*文件部署到目标 IIS 网站，需要使用[Web 部署**ContentPath**提供程序](https://technet.microsoft.com/library/dd569034(WS.10).aspx)调用 msdeploy.exe。 **ContentPath**提供程序支持物理目录路径和 iis 网站或应用程序路径，这使其成为在 Visual Studio 项目文件夹和 iis web 应用程序之间同步文件的理想选择。 若要部署文件，Msdeploy.exe 命令应如下所示：

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]

若要在部署过程结束时从目标站点中删除该文件，则 Msdeploy.exe 命令应如下所示：

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]

若要在生成和部署过程中自动执行这些命令，需要将它们集成到自定义 MSBuild 项目文件中。 下一过程介绍了如何执行此操作。

**部署和删除应用\_脱机文件**

1. 在 Visual Studio 2010 中，打开用于控制部署过程的 MSBuild 项目文件。 在 "[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)" 示例解决方案中，这是 "*发布*" 文件。
2. 在根**项目**元素中，创建一个新的**PropertyGroup**元素，用于存储*应用\_脱机*部署的变量：

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. **SourceRoot**属性在*发布*文件中的其他位置定义。 它表示源内容相对于当前路径的根文件夹相对于当前路径&#x2014;的位置（相对于*发布*文件的位置）。
4. **ContentPath**提供程序将不接受相对文件路径，因此，需要先获取源文件的绝对路径，然后才能进行部署。 您可以使用[ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx)任务来执行此操作。
5. 添加一个名为**GetAppOfflineAbsolutePath**的新**Target**元素。 在此目标中，使用**ConvertToAbsolutePath**任务获取项目文件夹中 *\_脱机模板*文件的应用的绝对路径。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. 此目标获取项目文件夹中*应用\_脱机模板*文件的相对路径，并将其另存为一个绝对文件路径形式的新属性。 **BeforeTargets**特性指定你希望此目标在**DeployAppOffline**目标之前执行，你将在下一步中创建该目标。
7. 添加一个名为**DeployAppOffline**的新目标。 在此目标中，调用 Msdeploy.exe 命令，该命令将*应用\_脱机*文件部署到目标 web 服务器。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. 在此示例中， **ContactManagerIisPath**属性在项目文件中的其他位置定义。 这只是一个 IIS 应用程序路径，格式为 *[IIS 网站名称]/[应用程序名称]* 。 如果在目标中包含条件，则用户可以通过更改属性值或提供命令行参数来切换 *\_脱机部署的应用程序*。
9. 添加一个名为**DeleteAppOffline**的新目标。 在此目标中，调用 Msdeploy.exe 命令，该命令将从目标 web 服务器 *\_脱机*文件删除应用。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. 最终任务是在项目文件执行过程中的适当时刻调用这些新目标。 可以通过多种方式执行此操作。 例如，在发布的*proj*文件中， **FullPublishDependsOn**属性指定调用**FullPublish**默认目标时必须按顺序执行的目标的列表。
11. 修改 MSBuild 项目文件，以便在发布过程中的相应点调用**DeployAppOffline**和**DeleteAppOffline**目标。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

运行自定义 MSBuild 项目文件时，会在成功生成后立即将*应用\_脱机*文件部署到服务器。 所有部署任务完成后，它将从服务器中删除。

## <a name="adding-an-app_offline-file-to-deployment-packages"></a>将应用\_脱机文件添加到部署包

根据你配置部署的方式，在将 web 包部署到目标时，可能&#x2014;会自动删除目标 IIS web 应用程序&#x2014;（如*应用\_脱机*文件）中的任何现有内容。 若要确保*应用程序\_脱机 .htm*文件在部署持续时间内保持不变，除了在部署过程开始时，还需要在 web 部署包本身中包含该文件。

- 如果已按照本主题中的前一项任务操作，则会将*应用\_脱机*文件添加到 web 应用程序项目中的其他文件名下（我们使用了*应用\_offline-template*），并将生成操作设置为**None**。 这些更改是防止文件干扰开发和调试所必需的。 因此，您需要自定义打包过程，以确保 web 部署包中包含*应用程序\_的脱机 .htm*文件。

Web 发布管道（WPP）使用名为**FilesForPackagingFromProject**的项列表来生成应包含在 Web 部署包中的文件的列表。 可以通过将自己的项添加到此列表来自定义 web 包的内容。 要执行此操作，需要完成以下高级步骤：

1. 在与项目文件相同的文件夹中创建一个名为 *[项目名称]* 的自定义项目文件。

    > [!NOTE]
    > .Csproj&#x2014;文件需要与你的 web 应用程序*项目文件*&#x2014;位于同一文件夹中，例如， *ContactManager*，而不是与你用来控制生成和部署过程的任何自定义项目文件位于同一文件夹中。
2. 在 *.targets*文件中，创建一个在**CopyAllFilesToSingleFolderForPackage**目标*之前*执行的新 MSBuild 目标。 这是一个 WPP 目标，它生成要包含在包中的项的列表。
3. 在新目标中，创建一个**ItemGroup**元素。
4. 在**ItemGroup**元素中，添加**FilesForPackagingFromProject**项，并指定*应用\_脱机 .htm*文件。

*.Targets*文件应如下所示：

[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]

下面是此示例中的要点：

- **BeforeTargets**特性通过指定它应紧接在**CopyAllFilesToSingleFolderForPackage**目标之前执行，将此目标插入 WPP。
- **FilesForPackagingFromProject**项使用**DestinationRelativePath**元数据值，在将文件添加到列表中时，将该文件从*应用\_offline-template*添加到*应用\_* 。

下面的过程演示如何将此 *.targets*文件添加到 web 应用程序项目。

**将. .targets 文件添加到 web 部署包**

1. 在 Visual Studio 2010 中打开解决方案。
2. 在 "**解决方案资源管理器**" 窗口中，右键单击 web 应用程序项目节点（例如**ContactManager**），指向 "**添加**"，然后单击 "**新建项**"。
3. 在 "**添加新项**" 对话框中，选择 " **XML 文件**" 模板。
4. 在 "**名称**" 框中，键入 *[项目名称] * *. wpp** （例如， **ContactManager**），然后单击 "**添加**"。

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > 如果将新项添加到项目的根节点，则会在与项目文件相同的文件夹中创建该文件。 可以通过在 Windows 资源管理器中打开该文件夹来验证这一点。
5. 在文件中，添加前面所述的 MSBuild 标记。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. 保存并关闭 *[项目名称] .targets*文件。

下一次生成和打包 web 应用程序项目时，WPP 会自动检测 *.targets*文件。 *应用\_offline-template*文件将作为*应用\_的 offline*包含在生成的 web 部署包中。

> [!NOTE]
> 如果部署失败，*应用\_的脱机 .htm*文件将保留原样，你的应用程序将保持脱机状态。 这通常是所需的行为。 若要使你的应用程序重新联机，你可以从你的 web 服务器中删除该*应用\_脱机 .htm*文件。 或者，如果更正任何错误并运行成功的部署，则会删除*应用\_脱机 .htm*文件。

## <a name="conclusion"></a>结束语

本主题介绍了如何在部署过程中使 web 应用程序脱机，方法是在部署过程开始时，将*应用程序\_脱机*文件发布到目标服务器，并将其删除。 本主题还介绍了如何在 web 部署包中将*应用\_脱机 .htm*文件。

## <a name="further-reading"></a>其他阅读材料

有关打包和部署过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)、[配置 web 包部署的参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)和[部署 web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

如果直接从 Visual Studio 发布 web 应用程序，而不是使用这些教程中所述的自定义 MSBuild 项目文件方法，则需要使用略微不同的方法在发布过程中使应用程序脱机正在.

> [!div class="step-by-step"]
> [上一页](excluding-files-and-folders-from-deployment.md)
> [下一页](running-windows-powershell-scripts-from-msbuild-project-files.md)
