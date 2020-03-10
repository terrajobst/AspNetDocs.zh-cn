---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: 了解生成过程 |Microsoft Docs
author: jrjlee
description: 本主题提供企业级生成和部署过程的演练。 本主题中所述的方法使用自定义 Microsoft Build Engin 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 802d93f7ca987d018967275bae68b8c56d883a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520832"
---
# <a name="understanding-the-build-process"></a>了解生成过程

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题提供企业级生成和部署过程的演练。 本主题中所述的方法使用自定义 Microsoft 生成引擎（MSBuild）项目文件来提供对过程的每个方面的精细控制。 在项目文件中，自定义 MSBuild 目标用于运行部署实用工具，如 Internet Information Services （IIS） Web 部署工具（Msdeploy.exe）和数据库部署实用工具 VSDBCMD。
> 
> > [!NOTE]
> > 前面的主题[了解项目文件](understanding-the-project-file.md)，其中介绍了 MSBuild 项目文件的关键组件，并引入了拆分项目文件的概念来支持部署到多个目标环境。 如果你尚不熟悉这些概念，则应在完成本主题之前查看[了解项目文件](understanding-the-project-file.md)。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="build-and-deployment-overview"></a>生成和部署概述

在[Contact Manager 解决方案](the-contact-manager-solution.md)中，三个文件控制生成和部署过程：

- *通用项目文件*（*发布*）。 这包含不在目标环境之间更改的生成和部署说明。
- *环境特定的项目文件*（*Env*）。 其中包含特定于特定目标环境的生成和部署设置。 例如，你可以使用*Env Dev*文件来提供开发人员或测试环境的设置，并创建一个名为 " *Env-Stage* " 的替代文件来提供过渡环境的设置。
- *命令文件*（*Publish-Dev*）。 这包含一个 Msbuild.exe 命令，该命令指定要执行的项目文件。 可以为每个目标环境创建一个命令文件，其中每个文件都包含一个用于指定其他特定于环境的项目文件的 Msbuild.exe 命令。 这使得开发人员只需运行相应的命令文件即可部署到不同的环境。

在示例解决方案中，可以在 "发布解决方案" 文件夹中找到这三个文件。

![](understanding-the-build-process/_static/image1.png)

在更详细地查看这些文件之前，让我们先了解一下在使用此方法时总体生成过程是如何工作的。 在较高级别，生成和部署过程如下所示：

![](understanding-the-build-process/_static/image2.png)

首先要做的事情是，这两个项目&#x2014;文件中一个包含通用生成和部署说明，另一个包含环境特定&#x2014;的设置合并到一个项目文件中。 然后，MSBuild 将通过项目文件中的说明。 它使用每个项目的项目文件来生成解决方案中的每个项目。 然后，它调用其他工具（如 Web 部署（Msdeploy.exe））和 VSDBCMD 实用程序，以将您的 Web 内容和数据库部署到目标环境。

从一开始到完成，生成和部署过程将执行以下任务：

1. 它会删除输出目录的内容，以准备全新的生成。
2. 它在解决方案中生成每个项目：

    1. 对于本示例&#x2014;中的 web 项目，生成过程会为每个项目创建一个&#x2014;web 部署包，这是一个 ASP.NET MVC WEB 应用程序和 WCF web 服务。
    2. 对于数据库项目，生成过程会为每个项目创建一个部署清单（deploymanifest 文件）。
3. 它使用 VSDBCMD 实用程序来部署解决方案中的每个数据库项目，&#x2014;&#x2014;同时使用项目文件中的各种属性和 deploymanifest 文件。
4. 它使用 Msdeploy.exe 实用工具来部署解决方案中的每个 web 项目，并使用项目文件中的各种属性来控制部署过程。

您可以使用示例解决方案更详细地跟踪此过程。

> [!NOTE]
> 有关如何为自己的服务器环境自定义特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

## <a name="invoking-the-build-and-deployment-process"></a>调用生成和部署进程

若要将 Contact Manager 解决方案部署到开发人员测试环境，开发人员需要运行*Publish-Dev*命令文件。 这将调用 Msbuild.exe，并将*Publish*指定为要执行的项目文件，并将*Env-Dev*指定为参数值。

[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]

> [!NOTE]
> **/Fl**开关（short for **/fileLogger**）将生成输出记录到当前目录中名为*msbuild.exe*的文件中。 有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。

此时，MSBuild 开始运行，加载*Publish*文件，并开始处理其中的指令。 第一个指令指示 MSBuild 导入**TargetEnvPropsFile**参数指定的项目文件。

[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]

**TargetEnvPropsFile**参数指定了*env dev*文件，因此 MSBuild 将*env 开发*文件的内容合并到*Publish*文件中。

在合并的项目文件中，MSBuild 遇到的下一个元素是属性组。 属性按其在文件中出现的顺序进行处理。 MSBuild 将为每个属性创建一个键值对，同时满足指定的条件。 稍后在文件中定义的属性将覆盖在文件中之前定义的具有相同名称的任何属性。 例如，请考虑**OutputRoot**属性。

[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]

当 MSBuild 处理第一个**OutputRoot**元素时，如果尚未提供具有相似名称的参数，则会将**OutputRoot**属性的值设置为 **。\Publish\Out**。当它遇到第二个**OutputRoot**元素时，如果条件的计算结果为**true**，则它将用**OutDir**参数的值覆盖**OutputRoot**属性的值。

MSBuild 遇到的下一个元素是单个项组，其中包含名为**buildsettings.projectstobuild**的项。

[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]

MSBuild 通过生成名为**buildsettings.projectstobuild**的项列表来处理此指令。 在这种情况下，项列表包含单个值&#x2014;，即解决方案文件的路径和文件名。

此时，剩余元素为目标。 从本质上讲，目标的处理&#x2014;方式不同于属性和项，除非用户显式指定了目标或由项目文件中的另一个构造调用，否则不会处理目标。 请记住，开始**项目**标记包含**DefaultTargets**属性。

[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]

如果调用了 Msbuild.exe，则这将指示 MSBuild 调用**FullPublish**目标。 **FullPublish**目标不包含任何任务;而只需指定依赖项列表。

[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]

此依赖项通知 MSBuild 为了执行**FullPublish**目标，它需要按提供的顺序调用此目标列表：

1. 它必须调用**Clean**目标。
2. 它必须调用**BuildProjects**目标。
3. 它必须调用**GatherPackagesForPublishing**目标。
4. 它必须调用**PublishDbPackages**目标。
5. 它必须调用**PublishWebPackages**目标。

### <a name="the-clean-target"></a>清理目标

**清理**目标基本上会删除输出目录及其所有内容，这是为全新生成做准备。

[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]

请注意，目标包含**ItemGroup**元素。 在**目标**元素中定义属性或项时，将创建*动态*属性和项。 换句话说，在执行目标之前，不会对属性或项进行处理。 输出目录可能不存在，或者在生成过程开始之前不包含任何文件，因此无法将 **\_FilesToDelete**列表生成为静态项;您必须等到执行执行完毕。 因此，可以将该列表构建为目标中的动态项。

> [!NOTE]
> 在这种情况下，因为**清理**目标是第一次执行，因此不需要使用动态项组。 但是，在这种情况下，最好使用动态属性和项，因为你可能想要在某个时间点以不同的顺序执行目标。  
> 还应瞄准，以避免声明永远不会使用的项。 如果你的项仅将由特定目标使用，请考虑将它们放在目标内，以消除生成过程中的任何不必要的开销。

动态项放在一起，**干净**的目标相当简单，并使用内置的**Message**、 **Delete**和**RemoveDir**任务来执行以下操作：

1. 向记录器发送消息。
2. 生成要删除的文件的列表。
3. 删除文件。
4. 删除输出目录。

### <a name="the-buildprojects-target"></a>BuildProjects 目标

**BuildProjects**目标基本上会生成示例解决方案中的所有项目。

[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]

前面的主题[了解项目文件](understanding-the-project-file.md)中对此目标进行了详细介绍，以说明任务和目标如何引用属性和项。 此时，您主要对**MSBuild**任务感兴趣。 您可以使用此任务来生成多个项目。 该任务不创建 Msbuild.exe 的新实例;它使用当前正在运行的实例来构建每个项目。 在此示例中，重要的要点是部署属性：

- 当完成每个项目的生成时， **DeployOnBuild**属性指示 MSBuild 在项目设置中运行任何部署说明。
- **DeployTarget**属性标识生成项目后要调用的目标。 在这种情况下，**包**目标会将项目输出生成到可部署的 web 包中。

> [!NOTE]
> **包**目标调用 Web 发布管道（WPP），该管道提供 MSBuild 与 Web 部署之间的集成。 如果希望查看 WPP 提供的内置目标，请查看% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的 " *Microsoft web.config* " 文件。

### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing 目标

如果你研究**GatherPackagesForPublishing**目标，你会注意到它不包含任何任务。 相反，它包含定义三个动态项的单个项组。

[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]

这些项引用在执行**BuildProjects**目标时创建的部署包。 无法在项目文件中静态定义这些项，因为在执行**BuildProjects**目标之前，项所引用的文件不存在。 相反，必须在未调用的目标中动态定义项，直到执行**BuildProjects**目标。

此目标中不使用这些项，&#x2014;此目标只是生成与每个项值相关联的项和元数据。 在处理这些元素后， **PublishPackages**项将包含两个值： *ContactManager*文件的路径和*ContactManager*文件的路径（& e）。 Web 部署会将这些文件创建为每个项目的 web 包的一部分，并且这些文件必须在目标服务器上调用才能部署包。 如果打开这些文件中的一个，你将看到带有各种特定于版本的参数值的 Msdeploy.exe 命令。

**DbPublishPackages**项将包含单个值，即*ContactManager*文件的路径。

> [!NOTE]
> 生成数据库项目时将生成一个 deploymanifest 文件，并且该文件使用与 MSBuild 项目文件相同的架构。 它包含部署数据库时所需的所有信息，包括数据库架构（.dbschema）的位置以及任何预先部署脚本和后期部署脚本的详细信息。 有关详细信息，请参阅[数据库生成和部署的概述](https://msdn.microsoft.com/library/aa833165.aspx)。

你将了解有关如何创建和[打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)和[部署数据库项目](deploying-database-projects.md)的部署包和数据库部署清单的详细信息。

### <a name="the-publishdbpackages-target"></a>PublishDbPackages 目标

简而言之， **PublishDbPackages**目标调用 VSDBCMD 实用工具，将**ContactManager**数据库部署到目标环境。 配置数据库部署涉及到许多决策和细微差别，你将在[部署数据库项目](deploying-database-projects.md)并[为多个环境自定义数据库部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)中了解更多相关信息。 在本主题中，我们将重点介绍此目标的实际工作方式。

首先，请注意，开始标记包含**输出**属性。

[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]

这是*目标批处理*的示例。 在 MSBuild 项目文件中，批处理是用于循环访问集合的一项技术。 **输出**属性的值 **"% （DbPublishPackages）"** 是指**DbPublishPackages**项列表的 "**标识**元数据" 属性。 此表示法 **输出 =% * * * （ItemList. ItemMetadataName）* 转换为：

- 将**DbPublishPackages**中的项拆分为包含相同**标识**元数据值的项的批。
- 每批执行一次目标。

> [!NOTE]
> **标识**是在创建时分配给每个项的[内置元数据值](https://msdn.microsoft.com/library/ms164313.aspx)之一。 它引用**项**元素&#x2014;中的**Include**特性的值，换言之，该项的路径和文件名。

在这种情况下，因为应该不会有多个具有相同路径和文件名的项，因此，实际上是使用一项的批大小。 针对每个数据库包执行一次目标。

可以在 **\_Cmd**属性中看到类似的表示法，该属性使用适当的开关生成 VSDBCMD 命令。

[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]

在这种情况下， **% （DbPublishPackages. DatabaseConnectionString）** 、 **% （DbPublishPackages TargetDatabase）** 和 **% （DbPublishPackages）** 都引用**FullPath**项集合的元数据值。 **\_Cmd**属性由**Exec**任务使用，该任务调用命令。

[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]

作为此表示法的结果， **Exec**任务将基于**DatabaseConnectionString**、 **TargetDatabase**和**FullPath**元数据值的唯一组合创建批处理，并为每个批次执行任务一次。 这是*任务批处理*的一个示例。 但是，由于目标级别批处理已经将项集合划分为单项批处理，因此**Exec**任务将运行一次，并且仅针对目标的每个迭代运行一次。 换句话说，此任务会为解决方案中的每个数据库包调用一次 VSDBCMD 实用程序。

> [!NOTE]
> 有关目标和任务批处理的详细信息，请参阅 MSBuild[批处理](https://msdn.microsoft.com/library/ms171473.aspx)、[目标批处理中的项元数据](https://msdn.microsoft.com/library/ms228229.aspx)，以及[任务批处理中的项元数据](https://msdn.microsoft.com/library/ms171474.aspx)。

### <a name="the-publishwebpackages-target"></a>PublishWebPackages 目标

此时，您已调用**BuildProjects**目标，该目标为示例解决方案中的每个项目生成一个 web 部署包。 随附每个包都是一个 *.deploy .cmd*文件，其中包含将包部署到目标环境所需的 msdeploy.exe 命令，以及一个*SetParameters*文件，该文件指定目标环境的必要细节。 你还调用了**GatherPackagesForPublishing**目标，它会生成一个项集合，其中包含你感兴趣的*部署 .cmd*文件。 实质上， **PublishWebPackages**目标执行以下功能：

- 它使用**XmlPoke**任务，为每个包操作*SetParameters*文件，以便为目标环境包含正确的详细信息。
- 它使用适当的开关为每个包调用 *.deploy .cmd*文件。

与**PublishDbPackages**目标一样， **PublishWebPackages**目标使用目标批处理来确保针对每个 web 包执行一次目标。

[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]

在目标中， **Exec**任务用于为每个 web 包运行 *.deploy .cmd*文件。

[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]

有关配置 web 包部署的详细信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。

## <a name="conclusion"></a>结束语

本主题提供了有关如何使用拆分项目文件来控制从联系人管理器示例解决方案开始到完成的生成和部署过程的演练。 使用此方法，只需运行特定于环境的命令文件，即可在单个可重复的步骤中运行复杂的企业级部署。

## <a name="further-reading"></a>其他阅读材料

有关项目文件和 WPP 的更深入介绍，请参阅[Microsoft 生成引擎内部：使用 MSBuild 和 Team Foundation build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一页](understanding-the-project-file.md)
> [下一页](building-and-packaging-web-application-projects.md)
