---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: 为 Web 包部署配置参数 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何设置参数值，如 Internet Information Services （IIS） web 应用程序名称、连接字符串和服务终结点,。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: f04ace98d81a33053b10cab7e40dbd75a6c0992c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438398"
---
# <a name="configuring-parameters-for-web-package-deployment"></a>为 Web 程序包部署配置参数

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍在将 web 包部署到远程 IIS web 服务器时，如何设置参数值，如 Internet Information Services （IIS） web 应用程序名称、连接字符串和服务终结点。

构建 web 应用程序项目时，生成和打包过程会生成三个密钥文件：

- *[项目名称] .zip*文件。 这是 web 应用程序项目的 web 部署包。 此程序包包含重新创建远程 IIS web 服务器上的 web 应用程序所需的所有程序集、文件、数据库脚本和资源。
- *[项目名称] .deploy .cmd*文件。 这包含一组参数化的 Web 部署（Msdeploy.exe）命令，可将 Web 部署包发布到远程 IIS Web 服务器。
- *[项目名称]。SetParameters*文件。 这会为 Msdeploy.exe 命令提供一组参数值。 你可以更新此文件中的值，并在部署 Web 包时将其作为命令行参数传递给 Web 部署。

> [!NOTE]
> 有关生成和打包过程的详细信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。

SetParameters 文件是从你的 web 应用程序项目文件和项目中的任何配置文件中动态生成的 *。* 当你生成并打包你的项目时，Web 发布管道（WPP）将自动检测到部署环境（例如目标 IIS Web 应用程序和任何数据库连接字符串）之间可能会更改的许多变量。 这些值在 web 部署包中自动参数化并添加到*SetParameters*文件。 例如，如果将连接字符串添加到 web 应用程序项目中的*web.config 文件，* 则生成过程将检测此更改，并相应地将条目添加到*SetParameters*文件。

在许多情况下，这种自动参数化就足够了。 但是，如果用户需要更改部署环境（如应用程序设置或服务终结点 Url）之间的其他设置，则需要告诉 WPP 将部署包中的这些值参数化，并将相应的项添加到*SetParameters*文件。 下面的部分介绍了如何执行此操作。

### <a name="automatic-parameterization"></a>自动参数化

生成和打包 web 应用程序时，WPP 会自动将以下内容参数化：

- 目标 IIS web 应用程序的路径和名称。
- *Web.config 文件中*的任意连接字符串。
- 在项目属性页中添加到 "**包/发布 SQL** " 选项卡的任何数据库的连接字符串。

例如，如果要生成并打包[联系人管理器](the-contact-manager-solution.md)示例解决方案，而不以任何方式触及参数化过程，则 WPP 会生成此*ContactManager*文件：

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]

这种情况下：

- **Iis Web 应用程序名称**参数是要在其中部署 Web 应用程序的 iis 路径。 默认值是从项目属性页的 "**打包/发布**" 网页获取的。
- **Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 连接字符串**参数是从*web.config 文件中的* **connectionStrings/add**元素生成的。 它表示应用程序应用于联系成员资格数据库的连接字符串。 此处提供的值将替换为*已部署的 web.config 文件*。 默认值是从预部署*web.config*文件中获取的。

WPP 还会在生成的部署包中参数化这些属性。 安装部署包时，可以提供这些属性的值。 如果通过 IIS 管理器手动安装包（如[手动安装 Web 包](manually-installing-web-packages.md)中所述），则安装向导将提示你为任何参数提供值。 如果你使用 *.deploy .cmd*文件以远程方式安装包（如[部署 Web 包](deploying-web-packages.md)中所述），Web 部署将查找此*SetParameters*文件以提供参数值。 您可以手动编辑*SetParameters*文件中的值，也可以在自动生成和部署过程中自定义该文件。 本主题稍后将对此过程进行更详细的介绍。

### <a name="custom-parameterization"></a>自定义参数化

在更复杂的部署方案中，您通常需要在部署项目之前将其他属性参数化。 一般而言，您应该参数化目标环境之间的任何属性和设置。 其中包括：

- *Web.config 文件中*的服务终结点。
- *Web.config 文件中*的应用程序设置。
- 要提示用户指定的任何其他声明性属性。

参数化这些属性的最简单方法是将*parameters .xml*文件添加到 web 应用程序项目的根文件夹中。 例如，在 Contact Manager 解决方案中，ContactManager 项目在根文件夹中包括一个*parameters .xml*文件。

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

如果打开此文件，则会看到它包含单个**参数**项。 该项使用 XML 路径语言（XPath）查询来查找和参数化*web.config*文件中的 ContactService WINDOWS COMMUNICATION FOUNDATION （WCF）服务的终结点 URL。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]

除了对部署包中的终结点 URL 进行参数化以外，WPP 还会将相应的项添加到随部署包一起生成的*SetParameters*文件。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]

如果手动安装部署包，则 IIS 管理器会提示你提供服务终结点地址和已自动参数化的属性。 如果通过运行 *.deploy .cmd*文件来安装部署包，则可以编辑*SetParameters*文件，以提供服务终结点地址的值，以及自动参数化属性的值。

有关如何创建*parameters .xml*文件的完整详细信息，请参阅[如何：在安装包时使用参数配置部署设置](https://msdn.microsoft.com/library/ff398068.aspx)。 名**为的过程使用 web.config 文件设置的部署参数**提供了分步说明。

## <a name="modifying-the-setparametersxml-file"></a>修改 SetParameters 文件

如果你计划通过运行 *.deploy .cmd*文件或通过&#x2014;从命令行&#x2014;运行 msdeploy.exe 来手动部署 web 应用程序包，则无需停止在部署之前手动编辑*SetParameters*文件。 但是，如果你正在使用企业级解决方案，则可能需要在更大的自动生成和部署过程中部署 web 应用程序包。 在此方案中，需要 Microsoft 生成引擎（MSBuild）才能为你修改*SetParameters*文件。 可以通过使用 MSBuild **XmlPoke**任务来执行此操作。

[联系人管理器示例解决方案](the-contact-manager-solution.md)演示了此过程。 下面的代码示例已编辑为仅显示与此示例相关的详细信息。

> [!NOTE]
> 若要更深入地了解示例解决方案中的项目文件模型以及一般的自定义项目文件的简介，请参阅[了解项目文件](understanding-the-project-file.md)和[了解生成过程](understanding-the-build-process.md)。

首先，将相关参数值定义为特定于环境的项目文件中的属性（例如， *Env-Dev*）。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]

> [!NOTE]
> 有关如何为自己的服务器环境自定义特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

接下来， *Publish*文件导入这些属性。 由于每个*SetParameters*文件都与 *.deploy .cmd*文件相关联，并且我们最终希望项目文件调用每个 *.deploy .cmd*文件，因此项目文件会*为每个 .deploy .cmd 文件创建*一个 MSBuild*项*，并将相关属性定义为*项元数据*。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]

这种情况下：

- **ParametersXml**元数据值指示*SetParameters*文件的位置。
- **IisWebAppName**值是要将 web 应用程序部署到的 IIS 路径。
- **MembershipDBConnectionString**值是成员资格数据库的连接字符串， **MembershipDBConnectionName**值是*SetParameters*文件中相应参数的**name**属性。
- **ServiceEndpointValue**值是目标服务器上 WCF 服务的终结点地址， **ServiceEndpointParamName**值是*SetParameters*文件中相应参数的 name 特性。

最后，在*发布的 proj*文件中， **PublishWebPackages**目标使用**XmlPoke**任务来修改*SetParameters*文件中的这些值。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]

你会注意到，每个**XmlPoke**任务指定了四个属性值：

- **XmlInputPath**属性告知任务在何处查找要修改的文件。
- **查询**属性是用于标识要更改的 XML 节点的 XPath 查询。
- **Value**属性是要插入到所选 XML 节点中的新值。
- **Condition**属性是指应在其上运行或不运行任务的条件。 在这些情况下，条件可确保不会尝试将 null 值或空值插入到*SetParameters*文件中。

## <a name="conclusion"></a>结束语

本主题介绍了*SetParameters*文件的角色，并说明了在生成 web 应用程序项目时如何生成该文件。 它介绍了如何通过将*参数 .xml*文件添加到项目中来参数化其他设置。 还介绍了如何通过使用项目文件中的**XmlPoke**任务，将*SetParameters*文件修改为更大的自动生成过程的一部分。

下一主题 "[部署 Web 包](deploying-web-packages.md)" 介绍了如何通过运行 *.deploy .cmd*文件或直接使用 msdeploy.exe 命令来部署 web 包。 在这两种情况下，都可以将*SetParameters*文件指定为部署参数。

## <a name="further-reading"></a>其他阅读材料

有关如何创建 web 包的信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。 有关如何实际部署 web 包的指南，请参阅[部署 web](deploying-web-packages.md)包。 有关如何创建*parameters .xml*文件的分步演练，请参阅[如何：在安装包时使用参数配置部署设置](https://msdn.microsoft.com/library/ff398068.aspx)。

有关 Web 部署中参数化的更多常规信息，请参阅[Web 部署参数化操作](https://go.microsoft.com/?linkid=9805119)（博客文章）。

> [!div class="step-by-step"]
> [上一页](building-and-packaging-web-application-projects.md)
> [下一页](deploying-web-packages.md)
