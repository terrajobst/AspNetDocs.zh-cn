---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: 部署 Web 包 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web ...）将 web 部署包发布到远程服务器。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 91b99e6e250342851aea6860164b6f6af54818d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464966"
---
# <a name="deploying-web-packages"></a>部署 Web 程序包

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用 Internet Information Services （IIS） Web 部署工具（Web 部署）2.0 将 web 部署包发布到远程服务器。
> 
> 可以通过两种主要方式将 web 包部署到远程服务器：
> 
> - 您可以直接使用 Msdeploy.exe 命令行实用程序。
> - 可以运行生成过程生成的 *[项目名称] .deploy .cmd*文件。
> 
> 不管使用哪种方法，最终结果都是相同的。 实质上，所有 *.deploy .cmd*文件都是运行包含某些预先确定值的 msdeploy.exe，因此，您无需为部署包提供尽可能多的信息。 这简化了部署过程。 另一方面，通过使用 Msdeploy.exe，你可以更加灵活地实现包的部署方式。
> 
> 你使用哪种方法取决于各种因素，包括部署过程所需的控制量，以及你是面向 Web 部署远程代理服务还是 Web 部署处理程序。 本主题说明如何使用每种方法，并识别每种方法的适用时间。
> 
> 本主题中的任务和演练假定：
> 
> - 已构建并打包 web 应用程序，如[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)中所述。
> - 已修改*SetParameters*文件，以便为目标环境提供正确的参数值，如为[Web 包部署配置参数](configuring-parameters-for-web-package-deployment.md)中所述。

运行 [*项目名称*] *. .deploy .cmd*文件是部署 web 包的最简单方法。 特别是，使用 *.deploy .cmd*文件比直接使用 msdeploy.exe 具有以下优势：

- 您无需指定 web 部署包&#x2014;的位置。 *.deploy .cmd*文件已经知道了它所在的位置。
- 您无需指定*SetParameters*文件的位置。&#x2014;该文件已知道该*文件所在*的位置。
- 不需要指定源和目标 Msdeploy.exe 提供程序&#x2014; *。 .deploy .cmd*文件已经知道要使用哪些值。
- 不需要指定 Msdeploy.exe 操作设置&#x2014; *。 .deploy .cmd*文件会自动将通常需要的值添加到 msdeploy.exe 命令。

使用 *.deploy .cmd*文件部署 web 包之前，应确保：

- *.Deploy .cmd*文件，[*项目名称*]。*SetParameters*文件和 web 包（[*项目名称*]。*zip*）位于同一个文件夹中。
- Web 部署（Msdeploy.exe）安装在运行 *.deploy*文件的计算机上。

*.Deploy .cmd*文件支持各种命令行选项。 当你从命令提示符运行该文件时，这是基本语法：

[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]

您必须指定 **/t**标志或 **/y**标志，以指示您是要分别执行试用版还是实时部署（不要在同一命令中使用这两种标志）。 下表说明了每个标志的用途。

| Flag | 说明 |
| --- | --- |
| **/T** | 使用 **– whatif**标志调用 msdeploy.exe，这指示试用版。 它不会部署包，而是创建一个报表，其中包含部署包时将发生的情况。 |
| **/Y** | 调用不带 **– whatif**标志的 msdeploy.exe。 这会将包部署到本地计算机或指定的目标服务器。 |
| **一样** | 指定目标服务器名称或服务 URL。 有关可在此处提供的值的详细信息，请参阅本主题中的**端点注意事项**部分。 如果省略 **/m**标志，包将部署到本地计算机。 |
| **/A** | 指定 Msdeploy.exe 应用于执行部署的身份验证类型。 可能的值为**NTLM**和**Basic**。 如果省略 **/a**标志，则身份验证类型默认为**NTLM** ，以便部署到 Web 部署远程代理服务，并为部署到 Web 部署处理程序的**基本**身份验证。 |
| **/U** | 指定用户名。 这仅适用于使用基本身份验证的情况。 |
| **/P** | 指定密码。 这仅适用于使用基本身份验证的情况。 |
| **/L** | 指示应将包部署到本地 IIS Express 实例。 |
| **/G** | 指定使用[tempAgent 提供程序设置](https://technet.microsoft.com/library/ee517345(WS.10).aspx)部署包。 如果省略 **/g**标志，则该值默认为**false**。 |

> [!NOTE]
> 每次生成过程创建 web 包时，它还会创建一个名为 *[项目名称]. deploy-readme*的文件，用于说明这些部署选项。

除了这些标志以外，还可以将 Web 部署操作设置指定为其他 *.deploy*参数。 你指定的任何其他设置只会传递到基础 Msdeploy.exe 命令。 有关这些设置的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。

假设要通过运行 *.deploy .cmd*文件将 ContactManager web 应用程序项目部署到测试环境。 你的测试环境配置为使用 Web 部署远程代理服务，如[配置用于 Web 部署发布的 Web 服务器（远程代理）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)中所述。 若要部署 web 应用程序，需要完成以下步骤。

**使用 .deploy .cmd 文件部署 web 应用程序**

1. 生成并打包 web 应用程序项目，如[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)中所述。
2. 按照为[Web 包部署配置参数](configuring-parameters-for-web-package-deployment.md)中所述，修改*ContactManager*文件以包含测试环境的正确参数值。
3. 打开命令提示符窗口并导航到*ContactManager*文件所在的位置。
4. 键入以下命令，然后按 Enter：

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

在此示例中：

- **/Y**标志指示你要实际部署包，而不是执行试用运行。
- **/M**标志指示你要将包部署到名为 TESTWEB1 的服务器。 在此值中，Msdeploy.exe 将尝试将包部署到 http://TESTWEB1/MSDeployAgentServiceWeb 部署远程代理服务。
- **/A**标志指示你希望使用 NTLM 身份验证。 因此，无需指定用户名和密码。

若要演示如何使用 *.deploy. .deploy*文件来简化部署过程，请查看使用上面所示的选项运行*ContactManager*时生成和执行的 msdeploy.exe 命令。

[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]

有关使用 *.deploy .cmd*文件部署 web 包的详细信息，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。

## <a name="using-msdeployexe"></a>使用 Msdeploy.exe

尽管使用 *.deploy .cmd*文件通常可简化部署过程，但在某些情况下，最好直接使用 msdeploy.exe。 例如:

- 如果要以非管理员用户的身份部署到 Web 部署处理程序，则不能使用 *.deploy .cmd*文件。 这是因为 Web 部署2.0 中的 bug，如**终结点注意事项**中所述。
- 如果要在不同位置的不同*SetParameters*文件之间手动切换，你可能更愿意直接使用 msdeploy.exe。
- 如果要重写几个 Msdeploy.exe 命令行参数，则可以直接使用 Msdeploy.exe。

使用 Msdeploy.exe 时，需要提供三个关键信息片段：

- 一个 **-source**参数，用于指示数据的来源。
- 一个 **– dest**参数，用于指示数据的目标位置。
- **– Verb**参数，用于指示要执行的[操作](https://technet.microsoft.com/library/dd568989(WS.10).aspx)。

Msdeploy.exe 依赖于[Web 部署提供程序](https://technet.microsoft.com/library/dd569040(WS.10).aspx)来处理源数据和目标数据。 Web 部署包含大量提供程序，这些提供程序可以使用&#x2014;的应用程序和数据源（例如，存在用于 SQL Server 数据库、IIS web 服务器、证书、全局程序集缓存（GAC）程序集、各种不同配置文件以及许多其他类型的数据）的提供程序。 **– Source**参数和 **– dest**参数都必须指定提供程序，格式为 **– source**： [*providerName*] = [*location*]。 将 web 包部署到 IIS 网站时，应使用以下值：

- **–源**提供程序始终[打包](https://technet.microsoft.com/library/dd569019(WS.10).aspx)。 例如:

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **– Dest**提供程序始终是[自动](https://technet.microsoft.com/library/dd569016(WS.10).aspx)的。例如：

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **–谓词**始终**同步**。

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

此外，还需要指定其他[特定于提供程序的设置](https://technet.microsoft.com/library/dd569001(WS.10).aspx)和常规[操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。 例如，假设要将 ContactManager web 应用程序部署到过渡环境。 部署将面向 Web 部署处理程序，并且必须使用基本身份验证。 若要部署 web 应用程序，需要完成以下步骤。

**使用 Msdeploy.exe 部署 web 应用程序**

1. 生成并打包 web 应用程序项目，如[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)中所述。
2. 按照为[Web 包部署配置参数](configuring-parameters-for-web-package-deployment.md)中所述，修改*ContactManager*文件以包含过渡环境的正确参数值。
3. 打开命令提示符窗口并浏览到 Msdeploy.exe 的位置。 这通常位于%PROGRAMFILES%\IIS\Microsoft Web 部署 V2\msdeploy.exe。
4. 键入此命令，然后按 Enter （忽略换行符）：

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

在此示例中：

- **– Source**参数指定**包**提供程序并指示 web 包的位置。
- **– Dest**参数指定**自动**提供程序。 **ComputerName**设置在目标服务器上提供 Web 部署处理程序的服务 URL。 **Authtype**设置指示你要使用基本身份验证，因此，你需要提供**用户名**和**密码**。 最后， **includeAcls = "False"** 设置指示您不希望将源 web 应用程序中的文件的访问控制列表（acl）复制到目标服务器。
- **– Verb： sync**参数指示你要复制目标服务器上的源内容。
- **– DisableLink**参数指示不需要在目标服务器上复制应用程序池、虚拟目录配置或安全套接字层（SSL）证书。 有关详细信息，请参阅[Web 部署链接扩展](https://technet.microsoft.com/library/dd569028(WS.10).aspx)。
- **– SetParamFile**参数提供*SetParameters*文件的位置。
- **– AllowUntrusted**开关指示 Web 部署应接受受信任的证书颁发机构颁发的 SSL 证书。 如果要部署到 Web 部署处理程序，并且已使用自签名证书来保护服务 URL，则需要包括此开关。

## <a name="automating-web-package-deployment"></a>自动部署 Web 包

在许多企业方案中，你需要将 web 包部署为更大的单步或自动部署的一部分。 无论你是选择通过运行 *.deploy*文件还是直接使用 msdeploy.exe 来部署 web 包，都可以参数化命令，并从 Microsoft 生成引擎（MSBuild）项目文件中的目标调用它们。

在 "联系人管理器" 示例解决方案中，查看*Publish*文件中的**PublishWebPackages**目标。 对于名为**PublishPackages**的项列表标识的每个 *.deploy .cmd*文件，此目标运行一次。 目标使用属性和项元数据为每个 *.deploy*文件生成一组完整的参数值，然后使用**Exec**任务来运行命令。

[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]

> [!NOTE]
> 若要更深入地了解示例解决方案中的项目文件模型以及一般的自定义项目文件的简介，请参阅[了解项目文件](understanding-the-project-file.md)和[了解生成过程](understanding-the-build-process.md)。

## <a name="endpoint-considerations"></a>终结点注意事项

无论你是通过运行 *.deploy*文件还是直接使用 msdeploy.exe 来部署 web 包，你都需要为你的部署指定计算机名称或服务终结点。

如果使用 Web 部署远程代理服务配置目标 web 服务器以进行部署，请将目标服务 URL 指定为目标。

[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]

或者，你可以将服务器名称单独指定为目标，Web 部署将推断远程代理服务 URL。

[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]

如果使用 Web 部署处理程序配置目标 web 服务器以进行部署，则需要将 IIS Web 管理服务（WMSvc）的终结点地址指定为目标。 默认情况下，这将采用以下格式：

[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]

您可以使用 *.deploy .cmd*文件或 msdeploy.exe 直接作为此类终结点的目标。 但是，如果你想要以非管理员用户的身份部署到 Web 部署处理程序，如为[Web 部署发布（Web 部署处理程序）配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述，需要将查询字符串添加到服务终结点地址。

[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]

这是因为，非管理员用户没有 IIS 的服务器级访问权限;他（她）只能访问特定的 IIS 网站。 撰写本文时，由于 Web 发布管道（WPP）中存在 bug，因此无法使用包含查询字符串的终结点地址运行 *.deploy .cmd*文件。 在此方案中，需要直接使用 Msdeploy.exe 来部署 web 包。

> [!NOTE]
> 有关 Web 部署远程代理服务和 Web 部署处理程序的详细信息，请参阅[选择 Web 部署的正确方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。 有关如何配置特定于环境的项目文件以部署到这些终结点的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

## <a name="authentication-considerations"></a>身份验证注意事项

无论是通过运行 *.deploy*文件还是直接使用 msdeploy.exe 来部署 web 包，都需要指定身份验证类型。 Web 部署接受两个可能的值： **NTLM**或**基本**。 如果指定基本身份验证，还需要提供用户名和密码。 选择身份验证类型时，需要注意以下几个因素：

- 如果要部署到 Web 部署远程代理服务，则必须使用 NTLM 身份验证。 远程代理服务不接受基本身份验证凭据。
- 如果要部署到 Web 部署处理程序，则可以使用 NTLM 或基本身份验证。 默认设置为 "基本身份验证"。 尽管基本身份验证依赖于以纯文本格式传输的用户名和密码，但你的凭据受到保护，因为 Web 部署处理程序始终使用 SSL 加密。
- 如果你的 web 包包含数据库，并且 web 服务器和数据库服务器是单独的计算机，则你将无法使用 NTLM 身份验证部署数据库，因为[ntlm "双跃点" 限制](https://go.microsoft.com/?linkid=9805120)。 需要在部署连接字符串中使用 SQL Server 凭据，或提供基本身份验证凭据以 Web 部署。 将[成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)中更详细地介绍了此问题。

## <a name="conclusion"></a>结束语

本主题介绍了如何通过运行 *.deploy .cmd*文件或直接使用 msdeploy.exe 来部署 web 包。 本文介绍了每种方法可能适用的情况，并说明了如何在较大的单步或自动生成过程中将部署命令参数化和运行。

## <a name="further-reading"></a>其他阅读材料

有关如何创建和参数化 web 部署包的指南，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)和[配置 web 包部署的参数](configuring-parameters-for-web-package-deployment.md)。 有关如何从 Team Foundation Server （TFS）实例生成和部署 web 包的指南，请参阅为[自动 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 有关如何自定义部署过程和排查其问题的信息，请参阅[从部署中排除文件和文件夹](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)。

> [!div class="step-by-step"]
> [上一页](configuring-parameters-for-web-package-deployment.md)
> [下一页](deploying-database-projects.md)
