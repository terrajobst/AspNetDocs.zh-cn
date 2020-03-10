---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
title: 为目标环境配置部署属性 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置特定于环境的属性，以便将示例联系人管理器解决方案部署到特定目标环境 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b5b86e03-b8ed-46e6-90fa-e1da88ef34e9
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
msc.type: authoredcontent
ms.openlocfilehash: 9742be7d718384c1b108d5f2c0c43e8e8d4fe8a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516806"
---
# <a name="configuring-deployment-properties-for-a-target-environment"></a>配置目标环境的部署属性

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置特定于环境的属性，以便将示例联系人管理器解决方案部署到特定目标环境。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案来表示具有真实复杂性级别的 WEB 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="process-overview"></a>流程概述

用于生成和部署联系人管理器解决方案的项目文件分为两个物理文件：

- 一个包含通用生成设置和说明（*发布*文件文件）。
- 一个包含特定于环境的生成设置（即 *，环境、* *环境、环境*）。

在生成时，适当的特定于环境的项目文件将合并到通用*发布*文件文件中，以形成一组完整的生成说明。 你可以通过使用描述你自己的部署方案的设置创建或自定义特定于环境的项目文件来配置特定目标环境的部署。

这些值中的许多取决于目标环境的配置&#x2014;方式（具体取决于目标 web 服务器是否配置为使用 Web 部署代理服务（远程代理）或 Web 部署处理程序。 有关这些方法的详细信息，以及有关为自己的环境选择适当方法的指导，请参阅[选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。

[联系人管理器方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)需要两个特定于环境的项目文件：

- 部署到开发人员测试环境（环境*开发*人员）。 开发人员测试环境配置为接受使用远程代理的远程部署，如[方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)中所述。 此文件需要提供远程代理终结点地址以及特定于位置的设置（如连接字符串和服务终结点）。
- 部署到过渡环境（*环境*中）。 过渡环境配置为使用 Web 部署处理程序接受远程部署，如[方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)中所述。 此文件需要提供 Web 部署处理程序终结点地址以及特定于位置的设置，例如连接字符串和服务终结点。

请务必注意，在环境特定的项目文件中配置的设置不会影响 web 包本身&#x2014;的内容，而是控制包的部署方式以及提取包时提供的参数值。 你要按照[方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)和[手动安装 web 包](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)中所述，手动将 web 包导入到生产环境中，因此在生成包时，与环境特定的项目文件中使用的设置无关。 导入包时，Internet Information Services （IIS）管理器将提示你输入任何参数化值（如连接字符串和服务终结点）。

若要将 Contact Manager 解决方案部署到你自己的目标环境，你可以自定义此文件或将其用作模板并创建你自己的文件。

**为 "联系人管理器" 解决方案配置特定于环境的部署设置**

1. 在 Visual Studio 2010 中打开 ContactManager-WCF 解决方案。
2. 在 "**解决方案资源管理器**" 窗口中，展开 "**发布**" 文件夹，展开 " **EnvConfig** " 文件夹，然后双击 " **Env-Dev**"。

    ![](configuring-deployment-properties-for-a-target-environment/_static/image1.png)
3. 将*Env-Dev*文件中的属性值替换为你自己的测试环境的正确值。

    > [!NOTE]
    > 此过程后面的表提供了有关这些属性中每个属性的详细信息。
4. 保存您的工作，然后关闭*Env 开发*文件。

## <a name="choosing-the-right-deployment-properties"></a>选择正确的部署属性

下表描述了特定于示例环境的项目文件中的每个属性的*用途，并*对应该提供的值提供了一些指导。

|                                                        属性名                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        详细信息                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <strong>MSDeployComputerName</strong>目标 web 服务器或服务终结点的名称。               |                                                                                                                                                                                                                                              如果要部署到目标 web 服务器上的远程代理服务，可以指定目标计算机的名称（例如， <strong>TESTWEB1</strong>或<strong>TESTWEB1.fabrikam.net</strong>），也可以指定远程代理终结点（例如 `http://TESTWEB1/MSDEPLOYAGENTSERVICE`）。 在每种情况下，部署的工作方式相同。 如果要部署到目标 Web 服务器上的 Web 部署处理程序，则应指定服务终结点，并包括 IIS 网站的名称作为查询字符串参数（例如，`https://STAGEWEB1:8172/MSDeploy.axd?site=DemoSite`）。                                                                                                                                                                                                                                              |
|         <strong>MSDeployAuth</strong>Web 部署应用于向远程计算机进行身份验证的方法。          |                                                                                                                                                                                                                          此设置应设置为 " <strong>NTLM</strong> " 或 "<strong>基本</strong>"。 通常，如果要部署到远程代理服务，则将使用<strong>NTLM</strong> ，如果要部署到 Web 部署处理程序，则使用<strong>Basic</strong> 。 如果使用基本身份验证，则还需指定 IIS Web 部署工具（Web 部署）应模拟的用户名和密码，以便执行部署。 在此示例中，这些值通过<strong>MSDeployUsername</strong>和<strong>MSDeployPassword</strong>属性提供。 如果你使用 NTLM 身份验证，则可以省略这些属性或将其保留为空。                                                                                                                                                                                                                          |
| <strong>MSDeployUsername</strong>如果使用基本身份验证，Web 部署将在远程计算机上使用此帐户。  |                                                                                                                                                                                                                                                                                                                                                                                                                       这应采用 "<em>域</em>\*用户名" 格式（例如<strong>FABRIKAM\matt</strong>）。 仅当指定了基本身份验证时，才使用此值。 如果你使用 NTLM 身份验证，则可以省略此属性。 如果提供了值，则将忽略该值。                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <strong>MSDeployPassword</strong>如果使用基本身份验证，Web 部署将在远程计算机上使用此密码。 |                                                                                                                                                                                                                                                                                                                                                                                                                    这是在<strong>MSDeployUsername</strong>属性中指定的用户帐户的密码。 仅当指定了基本身份验证时，才使用此值。 如果你使用 NTLM 身份验证，则可以省略此属性。 如果提供了值，则将忽略该值。                                                                                                                                                                                                                                                                                                                                                                                                                    |
|     <strong>ContactManagerIisPath</strong>要在其上部署 Contact Manager MVC 应用程序的 IIS 路径。     |                                                                                                                                                                                                                                                                                                                                                                        这应该是显示在 IIS 管理器中的路径，格式为 [<em>iis 网站名称</em>]/[<em>web</em><em>应用程序名称</em>]。 请记住，在部署应用程序之前 IIS 网站需要存在。 例如，如果你创建了一个名为 DemoSite 的 IIS 网站，则可将 MVC 应用程序的 IIS 路径指定为 DemoSite/ContactManager。                                                                                                                                                                                                                                                                                                                                                                        |
|   <strong>ContactManagerServiceIisPath</strong>要在其上部署联系人管理器 WCF 服务的 IIS 路径。    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          例如，如果你创建了一个名为 DemoSite 的 IIS 网站，则可以指定 WCF 服务的 IIS 路径为<strong>DemoSite/ContactManagerService</strong>。                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                  <strong>ContactManagerTargetUrl</strong>可用于访问 WCF 服务的 URL。                   |                                                                                                                                                     这将采用以下格式： [<em>IIS 网站根 URL</em>]/[<em>服务应用程序名称</em>]/[<em>服务终结点</em>]。 例如，如果已在端口85上创建了一个 IIS 网站，则该 URL 将采用 `http://localhost:85/ContactManagerService/ContactService.svc`格式。 请记住，MVC 应用程序和 WCF 服务部署到同一服务器。 因此，此 URL 只能从安装它的计算机进行访问。 因此，最好是在 URL 中使用 localhost 或 IP 地址，而不是计算机名或主机标头。 如果使用计算机名或主机标头，则 IIS 中的[环回检查](https://go.microsoft.com/?linkid=9805131)安全功能可能会阻止 URL 并返回<strong>HTTP 401.1-未经授权</strong>的错误。                                                                                                                                                     |
|                  <strong>CmDatabaseConnectionString</strong>数据库服务器的连接字符串。                  | 连接字符串确定 VSDBCMD 将用于联系数据库服务器和创建数据库的凭据，以及 web 服务器应用程序池将用于联系数据库服务器并与数据库进行交互的凭据。 实质上，你有两种选择。 可以指定<strong>集成安全性 = true</strong>，在这种情况下使用集成 Windows 身份验证： <strong>DATA Source = TESTDB1; 集成安全性 = true。</strong>在这种情况下，将使用运行 VSDBCMD 可执行文件的用户的凭据创建数据库，并且应用程序将使用 web 服务器计算机帐户的标识访问数据库。 或者，您可以指定 SQL Server 帐户的用户名和密码。 在这种情况下，VSDBCMD 使用 SQL Server 凭据来创建数据库，并使用应用程序池与数据库进行交互： <strong>Data Source = TESTDB1;User Id = ASqlUser;Password = Pa $ $w 0rd</strong>本主题中的演练假定你将使用集成的 Windows 身份验证。 |
|        <strong>CmTargetDatabase</strong>要在数据库服务器上创建的数据库的名称。        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     此处提供的值将作为参数添加到 VSDBCMD 命令。 它还用于生成一个完整的连接字符串，web 服务器上的应用程序池可以使用该字符串来与数据库进行交互。                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

这些示例演示了如何为特定的部署方案配置这些属性。

### <a name="example-1x2014deployment-to-the-remote-agent-service"></a>示例 1&#x2014;部署到远程代理服务

在此示例中：

- 正在部署到 TESTWEB1 上的远程代理服务。
- 你将指示 Web 部署使用 NTLM 身份验证。 Web 部署将使用用于调用 Microsoft 生成引擎（MSBuild）的凭据运行。
- 使用集成身份验证将**ContactManager**数据库部署到 TESTDB1。 将使用用于调用 MSBuild 的凭据来部署数据库。

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample1.xml)]

### <a name="example-2x2014deployment-to-the-web-deploy-handler-endpoint"></a>示例 2&#x2014;部署到 Web 部署处理程序终结点

在此示例中：

- 正在部署到 STAGEWEB1 上的 Web 部署处理程序服务终结点。
- 你将指示 Web 部署使用基本身份验证。
- 你正在指定 Web 部署应模拟远程计算机上的 FABRIKAM\stagingdeployer 帐户。
- 你正在使用 SQL Server 身份验证将**ContactManager**数据库部署到 STAGEDB1。

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample2.xml)]

## <a name="conclusion"></a>结束语

此时，项目文件已完全配置为生成 Contact Manager 解决方案并将其部署到一个或多个目标环境。

若要使用这些项目文件作为单步、可重复的部署过程的一部分，需要使用 MSBuild 执行*Publish*文件，并传入特定于环境的项目文件的位置作为参数。 可以通过多种方式实现此目的：

- 有关 MSBuild 的概述以及自定义项目文件的简介，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。
- 有关如何表述用于执行自定义项目文件的 MSBuild 命令的信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。
- 若要了解如何将 MSBuild 命令合并为单步、可重复部署的命令文件，请参阅[创建和运行部署命令文件](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)。
- 有关如何从 Team Build 执行自定义项目文件的信息，请参阅[创建支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

> [!div class="step-by-step"]
> [上一页](creating-a-server-farm-with-the-web-farm-framework.md)
