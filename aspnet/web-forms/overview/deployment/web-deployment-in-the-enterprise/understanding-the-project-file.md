---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 了解项目文件 |Microsoft Docs
author: jrjlee
description: Microsoft 生成引擎（MSBuild）项目文件位于生成和部署过程的核心。 本主题从有关 MSBuild 的概念性概述开始 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 419fe51aaf65bddcc2c50380f099f842a8d9439c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508052"
---
# <a name="understanding-the-project-file"></a>了解项目文件

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Microsoft 生成引擎（MSBuild）项目文件位于生成和部署过程的核心。 本主题以 MSBuild 和项目文件的概念性概述开头。 它介绍了在处理项目文件时将遇到的关键组件，并通过一个示例来演示如何使用项目文件来部署真实的应用程序。
> 
> 学习内容：
> 
> - MSBuild 如何使用 MSBuild 项目文件来生成项目。
> - MSBuild 如何与部署技术（如 Internet Information Services （IIS） Web 部署工具（Web 部署））集成。
> - 如何了解项目文件的关键组件。
> - 如何使用项目文件来构建和部署复杂的应用程序。

## <a name="msbuild-and-the-project-file"></a>MSBuild 和项目文件

在 Visual Studio 中创建和生成解决方案时，Visual Studio 使用 MSBuild 在解决方案中生成每个项目。 每个 Visual Studio 项目都包含一个 MSBuild 项目文件，其中包含一个文件扩展名，用于反映&#x2014;项目类型（例如C# ，项目（.Csproj））、Visual Basic.NET 项目（.vbproj）或数据库项目（.dbproj）。 为了生成项目，MSBuild 必须处理与项目关联的项目文件。 项目文件是一个 XML 文档，其中包含 MSBuild 生成项目所需的所有信息和说明，如要包含的内容、平台要求、版本信息、web 服务器或数据库服务器设置，以及必须执行的任务。

MSBuild 项目文件基于[MSBUILD XML 架构](/visualstudio/msbuild/msbuild-project-file-schema-reference)，因此，生成过程是完全开放且透明的。 此外，无需安装 Visual Studio 即可使用 MSBuild 引擎&#x2014;，而 msbuild 可执行文件是 .NET Framework 的一部分，你可以在命令提示符下运行它。 作为开发人员，您可以使用 MSBuild XML 架构来创建自己的 MSBuild 项目文件，以对项目的生成和部署方式进行完善且精细的控制。 这些自定义项目文件的工作方式与 Visual Studio 自动生成的项目文件的工作方式完全相同。

> [!NOTE]
> 你还可以将 MSBuild 项目文件与 Team Foundation Server （TFS）中的团队生成服务一起使用。 例如，你可以在持续集成（CI）方案中使用项目文件，以便在签入新代码时自动部署到测试环境。 有关详细信息，请参阅为[自动 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。

### <a name="project-file-naming-conventions"></a>项目文件命名约定

创建自己的项目文件时，可以使用任何所需的文件扩展名。 但是，若要使你的解决方案更易于理解，你应该使用以下常见约定：

- 创建生成项目的项目文件时，请使用 proj 扩展。
- 创建可重用的项目文件时，请使用 .targets 扩展名以导入其他项目文件。 带有 .targets 扩展名的文件通常不会生成任何内容，只是包含可以导入到 proj 文件中的说明。

### <a name="integration-with-deployment-technologies"></a>与部署技术的集成

如果你使用的是 Visual Studio 2010 中的 web 应用程序项目，例如 ASP.NET web 应用程序和 ASP.NET MVC web 应用程序，则你将知道这些项目包括用于将 web 应用程序打包和部署到目标环境的内置支持。 这些项目的**属性**页包括 "**打包/发布 Web** " 和 "**包/发布 SQL** " 选项卡，你可以使用这些选项卡配置应用程序组件的打包和部署方式。 这会显示 "**打包/发布 Web** " 选项卡：

![](understanding-the-project-file/_static/image1.png)

这些功能背后的基础技术称为 Web 发布管道（WPP）。 此 WPP 实质上将 MSBuild 和[Web 部署](https://go.microsoft.com/?linkid=9805122)结合起来，为 Web 应用程序提供完整的生成、打包和部署过程。

好消息是，你可以在为 web 项目创建自定义项目文件时利用 WPP 提供的集成点。 你可以在项目文件中包含部署说明，此操作可让你生成项目、创建 web 部署包，并通过单个项目文件和对 MSBuild 的单次调用在远程服务器上安装这些包。 你还可以调用任何其他可执行文件作为生成过程的一部分。 例如，你可以运行 VSDBCMD 命令行工具，以从架构文件部署数据库。 在本主题的过程中，你将了解如何利用这些功能满足企业部署方案的要求。

> [!NOTE]
> 有关 web 应用程序部署过程工作原理的详细信息，请参阅[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698.aspx)。

## <a name="the-anatomy-of-a-project-file"></a>项目文件的解析

更详细地查看生成过程之前，有必要花一些时间来熟悉 MSBuild 项目文件的基本结构。 本部分概述了在查看、编辑或创建项目文件时将遇到的更常见的元素。 具体来说，您将了解：

- 如何使用*属性*来管理生成过程的变量。
- 如何使用*项*来标识与生成进程（如代码文件）的输入。
- 如何使用*目标*和*任务*来向 MSBuild 提供执行指令，并使用在项目文件中的其他位置定义的*属性*和*项*。

这会显示 MSBuild 项目文件中的关键元素之间的关系：

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>项目元素

[项目](https://msdn.microsoft.com/library/bcxfsh87.aspx)元素是每个项目文件的根元素。 除了标识项目文件的 XML 架构以外，**项目**元素还可以包含属性以指定生成过程的入口点。 例如，在 "[联系人管理器" 示例解决方案](the-contact-manager-solution.md)中， *Publish*文件指定生成应通过调用名为**FullPublish**的目标来启动。

[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]

### <a name="properties-and-conditions"></a>属性和条件

若要成功生成和部署项目，项目文件通常需要提供许多不同的信息片段。 这些信息可能包括服务器名称、连接字符串、凭据、生成配置、源和目标文件路径，以及要支持自定义的任何其他信息。 在项目文件中，必须在[PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx)元素内定义属性。 MSBuild 属性包含键值对。 在**PropertyGroup**元素中，元素名称定义属性键，元素的内容定义属性值。 例如，可以定义名为**ServerName**和**ConnectionString**的属性，以存储静态服务器名称和连接字符串。

[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]

若要检索属性值，请使用格式 *$ （PropertyName）* 。 例如，若要检索**ServerName**属性的值，请键入：

[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]

> [!NOTE]
> 你将在本主题的后面部分介绍如何以及何时使用属性值。

在项目文件中将信息嵌入为静态属性并非总是用于管理生成过程的理想方法。 在许多情况下，你将需要从其他源中获取信息，或使用户能够从命令提示符中提供信息。 MSBuild 允许您将任何属性值指定为命令行参数。 例如，当用户从命令行运行 Msbuild.exe 时，用户可以提供**ServerName**的值。

[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]

> [!NOTE]
> 有关可用于 Msbuild.exe 的参数和开关的详细信息，请参阅[Msbuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。

您可以使用相同的属性语法来获取环境变量和内置项目属性的值。 许多常用的属性是为你定义的，你可以通过包含相关参数名称在项目文件中使用它们。 例如，&#x2014;若要检索当前项目平台（例如**x86**或**AnyCpu**&#x2014;），可以在项目文件中包含 **$ （platform）** 属性引用。 有关详细信息，请参阅[用于生成命令和属性的宏](https://msdn.microsoft.com/library/c02as0cs.aspx)、[常用的 MSBuild 项目属性](https://msdn.microsoft.com/library/bb629394.aspx)以及[保留属性](https://msdn.microsoft.com/library/ms164309.aspx)。

属性通常与*条件*结合使用。 大多数 MSBuild 元素都支持**Condition**特性，这使你可以指定 MSBuild 计算元素时所依据的条件。 例如，请考虑以下属性定义：

[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]

当 MSBuild 处理此属性定义时，它会首先检查 **$ （OutputRoot）** 属性值是否可用。 如果属性值为空&#x2014;，则该用户未提供此属性&#x2014;的值，条件的计算结果为**true** ，并且属性值设置为 **。\Publish\Out**。如果用户已为此属性提供值，则条件的计算结果为**false** ，并且不使用静态属性值。

有关可用于指定条件的不同方法的详细信息，请参阅[MSBuild 条件](https://msdn.microsoft.com/library/7szfhaft.aspx)。

### <a name="items-and-item-groups"></a>项和项组

项目文件的一个重要角色是定义生成过程的输入。 通常，这些输入是文件&#x2014;代码文件、配置文件、命令文件以及您需要在生成过程中进行处理或复制的任何其他文件。 在 MSBuild 项目架构中，这些输入由[项](https://msdn.microsoft.com/library/ms164283.aspx)元素表示。 在项目文件中，必须在[ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx)元素中定义项。 就像**属性**元素一样，你可以按喜欢的方式命名**项**元素。 但是，必须指定**Include**特性来标识该项表示的文件或通配符。

[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]

通过指定多个具有相同名称的**项**元素，您可以有效地创建一个命名的资源列表。 在操作中查看此操作的一个好方法是查看 Visual Studio 创建的项目文件之一。 例如，示例解决方案中的*ContactManager*文件包含许多项组，每个项组具有多个同名的**项**元素。

[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]

通过这种方式，项目文件将指示 MSBuild 构造文件的列表，这些文件需要以**相同的方式**&#x2014;进行处理。若要成功生成，**编译**列表中包括必须编译的代码文件，并且**内容**列表包括必须以未经修改的方式复制的资源。 我们将在本主题的后面部分介绍生成过程是如何引用和使用这些项的。

Item 元素还可以包含[ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx)子元素。 这些是用户定义的键值对，本质上表示特定于该项目的属性。 例如，项目文件中的许多**编译**项元素都包含**DependentUpon**子元素。

[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]

> [!NOTE]
> 除了用户创建的项元数据外，在创建时将为所有项分配各种通用元数据。 有关详细信息，请参阅[常见项元数据](https://msdn.microsoft.com/library/ms164313.aspx)。

可以在根级别**项目**元素内或特定**目标**元素中创建**ItemGroup**元素。 **ItemGroup**元素还支持**条件**属性，这使你可以根据项目配置或平台等条件来定制生成过程的输入。

### <a name="targets-and-tasks"></a>目标和任务

在 MSBuild 架构中， [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx)元素表示单个生成指令（或任务）。 MSBuild 包含许多预定义任务。 例如:

- **复制**任务将文件复制到新位置。
- **Csc**任务调用 Visual C#编译器。
- **Vbc**任务调用 Visual Basic 编译器。
- **Exec**任务运行指定的程序。
- **消息**任务将消息写入记录器。

> [!NOTE]
> 有关现成可用的任务的完整详细信息，请参阅[MSBuild 任务参考](https://msdn.microsoft.com/library/7z253716.aspx)。 有关任务的详细信息，包括如何创建您自己的自定义任务，请参阅[MSBuild 任务](https://msdn.microsoft.com/library/ms171466.aspx)。

任务必须始终包含在[目标](https://msdn.microsoft.com/library/t50z2hka.aspx)元素中。 **目标**元素是按顺序执行的一组或多项任务，项目文件可以包含多个目标。 当你想要运行一个任务或一组任务时，可以调用包含它们的目标。 例如，假设有一个记录消息的简单项目文件。

[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]

可以通过使用 **/t**开关指定目标，从命令行调用目标。

[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]

或者，可以将**DefaultTargets**属性添加到**项目**元素，以指定要调用的目标。

[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]

在这种情况下，无需从命令行指定目标。 只需指定项目文件，MSBuild 就会调用**FullPublish**目标。

[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]

目标和任务都可以包括**条件**特性。 因此，如果满足某些条件，则可以选择忽略整个目标或单个任务。

一般而言，在您创建有用的任务和目标时，您需要参考在项目文件中的其他位置定义的属性和项：

- 若要使用属性值，请键入 **$ （***propertyname***）** ，其中*PropertyName*是**属性**元素的名称或参数的名称。
- 若要使用某一项，请键入 **@ （** 项目名称） *，其中，* 项目名称是**item**元素的名称。

> [!NOTE]
> 请记住，如果你创建了多个具有相同名称的项，则会生成一个列表。 与此相反，如果您创建了多个具有相同名称的属性，则您提供的最后一个属性值将覆盖任何具有&#x2014;相同名称的以前的属性，属性只能包含单个值。

例如，在示例解决方案的*Publish*文件中，查看**BuildProjects**目标。

[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]

在此示例中，可以观察到以下要点：

- 如果指定了**BuildingInTeamBuild**参数并且其值为**true**，则将不会执行此目标中的任何任务。
- 目标包含[MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx)任务的单个实例。 此任务允许您生成其他 MSBuild 项目。
- **Buildsettings.projectstobuild**项将传递给任务。 此项可以表示项目或解决方案文件的列表，这些文件均由项组中的**buildsettings.projectstobuild**项元素定义。 在这种情况下， **buildsettings.projectstobuild**项引用单个解决方案文件。

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- 传递给**MSBuild**任务的属性值包括名为**OutputRoot**和**Configuration**的参数。 如果提供了参数值，则将这些参数设置为参数值，如果不是，则设置静态属性值。

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

你还可以看到**MSBuild**任务调用了一个名为 "**生成**" 的目标。 这是在 Visual Studio 项目文件中广泛使用的几个内置目标之一，可在自定义项目文件中使用，如**生成**、**清理**、**重新生成**和**发布**。 你将在本主题的后面部分了解如何使用目标和任务来控制生成过程，以及有关**MSBuild**任务的详细信息。

> [!NOTE]
> 有关目标的详细信息，请参阅[MSBuild 目标](https://msdn.microsoft.com/library/ms171462.aspx)。

## <a name="splitting-project-files-to-support-multiple-environments"></a>拆分项目文件以支持多个环境

假设您希望能够将解决方案部署到多个环境，如测试服务器、过渡平台和生产环境。 此配置在这些环境&#x2014;之间的差异可能会明显不同于服务器名称、连接字符串等，但在凭据、安全设置和许多其他方面也可能有所不同。 如果需要定期执行此操作，则每次切换目标环境时都无法在项目文件中编辑多个属性。 它也是一个理想的解决方案，需要向生成过程提供属性值的无限列表。

幸运的是，有一种替代方法。 MSBuild 使你可以在多个项目文件之间拆分你的生成配置。 若要查看其工作原理，请注意，在示例解决方案中，有两个自定义项目文件：

- *发布 proj*，其中包含所有环境通用的属性、项和目标。
- *Env-Dev*，其中包含特定于开发人员环境的属性。

现在请注意， *Publish*文件包含一个[Import](https://msdn.microsoft.com/library/92x05xfs.aspx)元素，紧靠在 "打开**项目**" 标记下。

[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]

**Import**元素用于将另一个 msbuild 项目文件的内容导入到当前的 msbuild 项目文件中。 在这种情况下， **TargetEnvPropsFile**参数提供您要导入的项目文件的文件名。 在运行 MSBuild 时，可以为此参数提供一个值。

[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]

这会有效地将两个文件的内容合并为一个项目文件。 使用此方法，你可以创建一个项目文件，其中包含通用生成配置和多个包含特定于环境的属性的附加项目文件。 因此，只需运行包含不同参数值的命令，就能将解决方案部署到不同的环境。

![](understanding-the-project-file/_static/image3.png)

以这种方式拆分项目文件是一种很好的做法。 它允许开发人员通过运行单个命令部署到多个环境，同时避免跨多个项目文件复制通用生成属性。

> [!NOTE]
> 有关如何为自己的服务器环境自定义特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

## <a name="conclusion"></a>结束语

本主题提供了对 MSBuild 项目文件的常规介绍，并介绍了如何创建自己的自定义项目文件来控制生成过程。 它还引入了将项目文件拆分为通用生成指令和特定于环境的生成属性的概念，使你可以轻松地生成项目并将其部署到多个目标。

下一主题 "[了解生成过程](understanding-the-build-process.md)" 将提供更多有关如何使用项目文件来控制生成和部署的详细信息，指导你逐步完成解决方案的部署。

## <a name="further-reading"></a>其他阅读材料

有关项目文件和 WPP 的更深入介绍，请参阅[Microsoft 生成引擎内部：使用 MSBuild 和 Team Foundation build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一页](setting-up-the-contact-manager-solution.md)
> [下一页](understanding-the-build-process.md)
