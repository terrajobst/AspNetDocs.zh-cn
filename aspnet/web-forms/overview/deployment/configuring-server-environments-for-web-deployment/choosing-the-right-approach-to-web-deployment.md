---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 选择正确的 Web 部署方法 |Microsoft Docs
author: jrjlee
description: 使用 Internet Information Services （IIS） Web 部署工具（Web 部署）2.0 或更高版本时，可以使用以下三种主要方法获取 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13f784dd8e6404806104d56b026b3c41ca178892
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441422"
---
# <a name="choosing-the-right-approach-to-web-deployment"></a>选择 Web 部署的适当方法

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 使用 Internet Information Services （IIS） Web 部署工具（Web 部署）2.0 或更高版本时，可以使用以下三种主要方法将打包的 web 应用程序部署到 web 服务器上。 你可以：
> 
> - 通过目标服务器上的*Web 部署代理服务*（也称为 "远程代理"）来部署应用程序。
> - 使用点播 Web 部署（也称为 "temp agent"）从远程位置部署应用程序。
> - 通过目标服务器上的*IIS Web 部署处理程序*来部署应用程序。
> - 通过将 web 包手动复制到目标服务器并通过 IIS 管理器导入来部署应用程序。
> 
> 你配置目标 web 服务器的方式将取决于你想要使用的部署方法。 本主题将帮助你决定部署哪种方法适合你。

下表显示了每种部署方法的主要优点和缺点，以及大多数情况下最适合的方案。

| 方法 | 优点 | 缺点 | 典型方案 |
| --- | --- | --- | --- |
| 远程代理 | 它很容易设置。 它适用于 web 应用程序和内容的定期更新。 | 用户必须是目标服务器上的管理员。 用户无法提供备用凭据。 | 开发环境。 测试环境。 |
| 临时代理 | 不需要在目标计算机上安装 Web 部署。 自动使用最新版本的 Web 部署。 | 用户必须是目标服务器上的管理员。 用户无法提供备用凭据。 | 开发环境。 测试环境。 |
| Web 部署处理程序 | 非管理员用户可以部署内容。 它适用于 web 应用程序和内容的定期更新。 | 设置起来要复杂得多。 | 过渡环境。 Intranet 生产环境。 宿主环境。 |
| 脱机部署 | 很容易设置。 它适用于隔离环境。 | 服务器管理员每次都必须手动复制和导入 web 包。 | 面向 Internet 的生产环境。 隔离网络环境。 |

## <a name="using-the-remote-agent"></a>使用远程代理

在目标服务器上使用默认设置安装 Web 部署时，将自动安装和启动 Web 部署代理服务（"远程代理"）。 默认情况下，远程代理会在此地址公开 HTTP 终结点：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]

> [!NOTE]
> 你可以将 [*server*] 替换为 web 服务器的计算机名称、你的 web 服务器的 IP 地址或解析为你的 web 服务器的主机名。

服务器管理员可以通过指定此终结点地址，从远程位置（例如开发人员计算机或生成服务器）部署 web 包。 例如，假设在 Fabrikam，Inc. 的 Matt Hink 已在其开发人员计算机上生成 ContactManager web 应用程序项目。 生成过程将生成一个 web 包和一个 *.deploy .cmd*文件，其中包含安装包所需的 Web 部署命令。 如果 Matt 是 TESTWEB1 服务器上的服务器管理员，则可以通过在其开发人员计算机上运行以下命令，将 web 应用程序部署到测试 web 服务器：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]

在实际情况下，如果提供计算机名称，则 Web 部署可执行文件可以推断远程代理的终结点地址，因此 Matt 只需要键入：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]

> [!NOTE]
> 有关 Web 部署命令行语法和 *.deploy .cmd*文件的详细信息，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。

远程代理提供一种简单的方法来从远程位置部署内容，这种方法可以很好地使用一键式或自动部署。 但是，运行部署命令的用户还必须是目标服务器上的域管理员或本地管理员组的成员。 此外，远程代理不支持基本身份验证，因此不能在命令行上传递替代凭据。

远程代理提供了一种在开发或测试方案中进行部署的有用方法，在这种情况下，开发人员对测试服务器环境具有完全管理员控制并不少见，通常会重新生成和重新部署应用程序解答. 但是，对于过渡环境或生产环境而言，此方法通常不太合适。

有关使用远程代理方法的方案的端到端示例，请参阅[方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。

## <a name="using-the-temp-agent"></a>使用 Temp 代理

部署的 temp 代理方法类似于远程代理方法。 但是，与远程代理方法不同，你无需在目标 Web 服务器上安装 Web 部署。 相反，当您执行部署时，Web 部署将在目标服务器上安装 Web 部署代理服务的临时版本，并使用此版本将内容部署到 IIS。 部署完成后，将删除所有临时文件。

如果要使用 temp agent 提供程序设置，请将 **/g**标志添加到部署命令：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]

> [!NOTE]
> 如果 web 部署代理服务已安装在目标计算机上，即使该服务未运行，也不能使用 temp 代理。

此方法的优点是，不需要在目标服务器上维护 Web 部署安装。 此外，不需要确保源计算机和目标计算机运行相同版本的 Web 部署。 但是，此方法与远程代理方法的主体限制相同，也就是说，你必须是目标服务器上的本地管理员才能部署内容，并且仅支持 NTLM 身份验证。 Temp 代理方法还需要更多的目标环境初始配置。

有关使用 temp 代理的详细信息，请参阅[如何：使用 .deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)和[按需 Web 部署](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。

## <a name="using-the-web-deploy-handler"></a>使用 Web 部署处理程序

对于 IIS 7，Web 部署通过 IIS Web 部署处理程序提供了一种备选部署方法。 Web 部署处理程序与 IIS Web 管理服务（WMSvc）紧密集成，这旨在允许用户从远程位置管理 IIS 网站。

默认情况下，远程代理会在此地址公开 HTTP 终结点：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]

> [!NOTE]
> 你可以将 [*server*] 替换为 web 服务器的计算机名称、你的 web 服务器的 IP 地址或解析为你的 web 服务器的主机名。

通过远程代理和 temp 代理进行 Web 部署处理程序的大优势在于，您可以将 IIS 配置为允许非管理员用户将应用程序和内容部署到特定的 IIS 网站。 Web 部署处理程序还支持基本身份验证，因此你可以在 Web 部署命令中提供作为参数的替代凭据。 主要缺点是，Web 部署处理程序最初的设置和配置要复杂得多。

对于非管理员用户，Web 管理服务（WMSvc）只允许用户使用站点级连接连接到 IIS，而不允许使用服务器级连接连接到 IIS。 若要访问特定站点，可以在终结点地址中包含特定于站点的查询字符串：

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]

例如，假设某一生成过程配置为在每次成功生成后自动将 web 应用程序部署到过渡环境。 如果使用远程代理方法，则需要在目标服务器上将生成过程标识为管理员。 与此相反，使用 Web 部署处理程序方法，您可以向非管理员用户&#x2014;授予仅限特定&#x2014;IIS**网站的权限**，并且生成过程可以提供这些凭据来部署 Web 包。

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]

> [!NOTE]
> 有关 Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。 有关使用 *.deploy .cmd*文件的详细信息，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。

Web 部署处理程序提供了一种用于在过渡环境、托管环境和基于 intranet 的生产环境中进行部署的有用方法，在这种环境中，可以远程访问服务器，但不能使用管理员凭据。

有关使用 Web 部署处理程序方法的方案的端到端示例，请参阅[方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。

## <a name="using-offline-deployment"></a>使用脱机部署

在某些情况下，不可能或不切实际地将应用程序和内容从远程位置部署到 IIS 网站。 例如，源计算机和目标计算机可能位于独立的网络或网段中，或防火墙策略可能不允许远程访问。

在这种情况下，仍可以使用 Web 部署的打包和发布功能;你不能从远程位置使用它们。 相反，目标服务器上的管理员必须将 web 包复制到服务器上，并通过 IIS 管理器将其导入。

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

脱机部署方法通常适用于面向 Internet 的生产环境，其中外围网络中的服务器可能与内部网络中的计算机的连接受限。

有关使用脱机部署方法的方案的端到端示例，请参阅[方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。

## <a name="further-reading"></a>其他阅读材料

有关 Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。 有关使用 *.deploy .cmd*文件的详细信息，请参阅[如何：使用 .Deploy .Cmd 文件安装部署包](https://msdn.microsoft.com/library/ff356104.aspx)。

有关从远程计算机部署 web 包的不同方法的更多常规指导，请参阅[远程使用 Web 部署](https://technet.microsoft.com/library/ee461175(WS.10).aspx)。 有关使用点播 Web 部署的详细信息，请参阅[点播 Web 部署](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。

> [!div class="step-by-step"]
> [上一页](configuring-server-environments-for-web-deployment.md)
> [下一页](scenario-configuring-a-test-environment-for-web-deployment.md)
