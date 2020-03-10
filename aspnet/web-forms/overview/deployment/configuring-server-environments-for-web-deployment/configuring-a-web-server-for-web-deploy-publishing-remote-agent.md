---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 为 Web 部署发布配置 Web 服务器（远程代理） |Microsoft Docs
author: jrjlee
description: 本主题介绍如何将 Internet Information Services （IIS） web 服务器配置为支持使用 IIS Web 部署的 web 发布和部署 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: ce0d246afdfb65c2ea15a287064511e7d1d58622
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457700"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>配置用于 Web 部署发布的 Web 服务器（远程代理）

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用 IIS Web 部署工具（Web 部署）远程代理服务配置 Internet Information Services （IIS） web 服务器，以支持 web 发布和部署。
> 
> 使用 Web 部署2.0 或更高版本时，有三种主要方法可用于将应用程序或站点获取到 Web 服务器。 你可以：
> 
> - 使用*Web 部署远程代理服务*。 此方法需要较少的 web 服务器配置，但你需要提供本地服务器管理员的凭据才能将任何内容部署到服务器。
> - 使用*Web 部署处理程序*。 这种方法更复杂，需要进行更多初始工作才能设置 web 服务器。 但是，在使用此方法时，可以将 IIS 配置为允许非管理员用户执行部署。 Web 部署处理程序仅在 IIS 版本7或更高版本中可用。
> - 使用*脱机部署*。 此方法需要最少的 web 服务器配置，但服务器管理员必须手动将 web 包复制到服务器上，并通过 IIS 管理器将其导入。
> 
> 有关这些方法的主要功能、优点和缺点的详细信息，请参阅[选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>Web 部署远程代理是否适合你？

是的，如果要部署内容的用户可以在目标服务器上提供管理员凭据。 此方法在以下类型的方案中通常是必需的：

- 开发或测试环境，开发人员可以完全控制目标 web 服务器和数据库服务器。
- 小型组织，其中单个用户或一小组用户可以控制整个应用程序生命周期。

在许多大型组织中，特别是在过渡环境或生产环境中，向用户授予对 web 服务器的管理员权限通常是不现实的。 对于托管的 web 服务器，这种情况尤其不可能出现。 此外，如果计划从生成服务器自动进行部署，则可能不希望使用管理员凭据来完成部署过程。 在这些情况下，将 web 服务器配置为支持使用[Web 部署处理程序](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)的部署可能会提供更好的选择。

## <a name="task-overview"></a>任务概述

本主题说明如何使用 Web 部署远程代理方法将 Internet Information Services （IIS） 7.5 web 服务器配置为接受和部署远程计算机上的 web 包。 你需要：

- 安装 IIS 7.5 和 IIS 7 建议的配置。
- 安装 Web 部署2.1 或更高版本。
- 创建一个 IIS 网站来托管已部署的内容。
- 确保 Web 部署代理服务正在运行。

若要专门托管示例解决方案，还需要：

- 安装 .NET Framework 4.0。
- 安装 ASP.NET MVC 3。

本主题将演示如何执行上述每个过程。 本主题中的任务和演练假设你开始使用运行 Windows Server 2008 R2 的干净服务器版本。 继续之前，请确保：

- Windows Server 2008 R2 Service Pack 1 和所有可用更新均已安装。
- 服务器已加入域。
- 服务器具有静态 IP 地址。

> [!NOTE]
> 有关将计算机加入域的详细信息，请参阅将[计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 有关配置静态 IP 地址的详细信息，请参阅[配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。 远程代理服务支持 IIS 6，无需加入到域。 不过，本教程中的步骤是在 IIS 7.5 上进行开发和测试的，其他版本的过程可能会有所不同。

## <a name="install-products-and-components"></a>安装产品和组件

本部分将指导你完成在 web 服务器上安装所需的产品和组件。 在开始之前，好的做法是运行 Windows 更新以确保服务器完全处于最新状态。

在这种情况下，需要安装以下内容：

- **IIS 7 建议的配置**。 这将在你的 web 服务器上启用**Web 服务器（IIS）** 角色，并安装用于托管 ASP.NET 应用程序的 IIS 模块和组件集。
- **.NET Framework 4.0**。 这是运行在此版本的 .NET Framework 上构建的应用程序所必需的。
- **Web 部署工具2.1 或更高版本**。 这会在服务器上安装 Web 部署（及其基础可执行文件）。 在此过程中，它将安装并启动 Web 部署代理服务。 此服务允许你从远程计算机部署 web 包。
- **ASP.NET MVC 3**。 这将安装运行 MVC 3 应用程序所需的程序集。

> [!NOTE]
> 本演练介绍了如何使用 Web 平台安装程序来安装和配置所需的组件。 尽管无需使用 Web 平台安装程序，但它可以通过自动检测依赖项并确保始终获取最新的产品版本来简化安装过程。 有关详细信息，请参阅[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。

**安装所需的产品和组件**

1. 下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。
2. 安装完成后，Web 平台安装程序将自动启动。

    > [!NOTE]
    > 你现在可以从 "**开始**" 菜单启动 Web 平台安装程序。 为此，请在 "**开始**" 菜单上，单击 "**所有程序**"，然后单击 " **Microsoft Web 平台安装程序**"。
3. 在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。
4. 在窗口左侧的导航窗格中，单击 "**框架**"。
5. 在**Microsoft .NET Framework 4** "行中，如果尚未安装 .NET Framework，请单击"**添加**"。

    > [!NOTE]
    > 可能已通过 Windows 更新安装 .NET Framework 4.0。 如果产品或组件已安装，Web 平台安装程序将通过将 "**添加**" 按钮替换为**安装**的文本来指示这一点。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. 在**ASP.NET MVC 3 （Visual Studio 2010）** 行中，单击 "**添加**"。
7. 在导航窗格中，单击 "**服务器**"。
8. 在 " **IIS 7 推荐的配置**" 行中，单击 "**添加**"。
9. 在**Web 部署工具 2.1**行中，单击 "**添加**"。
10. 单击“安装”。 Web 平台安装程序将显示产品&#x2014;列表以及要安装的任何关联依赖关系&#x2014;，并将提示你接受许可条款。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. 查看许可条款，如果同意条款，请单击 "**我接受**"。
12. 安装完成后，单击 "**完成**"，然后关闭 " **Web 平台安装程序 3.0** " 窗口。

如果在安装 IIS 之前安装了 .NET Framework 4.0，则需要运行[ASP.NET Iis 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)（aspnet\_regiis），以将最新版本的 ASP.NET 注册到 iis。 如果不这样做，你会发现 IIS 将提供静态内容（如 HTML 文件），而不会有任何问题，但当你尝试浏览到 ASP.NET 内容时，它将返回**HTTP 错误404.0 –找不**到。 您可以使用此过程来确保 ASP.NET 4.0 已注册。

**向 IIS 注册 ASP.NET 4。0**

1. 单击 "**开始**"，然后键入**命令提示符**。
2. 在搜索结果中，右键单击 "**命令提示符**"，然后单击 "**以管理员身份运行**"。
3. 在命令提示符窗口中，导航到 " **%windir%\microsoft.net\framework\v4.0.30319 (对于**" 目录。
4. 键入以下命令，然后按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. 如果你打算随时托管64位 web 应用程序，则还应将 ASP.NET 的64位版本注册到 IIS。 为此，请在命令提示符窗口中导航到 **%windir%\microsoft.net\framework64\v4.0.30319 (对于**目录。
6. 键入以下命令，然后按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

作为一种很好的做法，请再次使用 Windows 更新，下载并安装适用于已安装的新产品和组件的任何可用更新。

## <a name="configure-the-iis-website"></a>配置 IIS 网站

你需要创建并配置一个 IIS 网站来托管内容，然后才能将 web 内容部署到你的服务器。 Web 部署只能将 web 包部署到现有 IIS 网站;它无法为你创建网站。 在高级别上，需要完成以下任务：

- 在文件系统上创建一个文件夹以托管你的内容。
- 创建一个 IIS 网站来提供内容，并将其与本地文件夹关联。
- 向本地文件夹上的应用程序池标识授予读取权限。

尽管不会阻止你将内容部署到 IIS 中的默认网站，但对于除测试或演示方案之外的任何内容，不建议使用此方法。 若要模拟生产环境，应该创建一个新的 IIS 网站，其中包含特定于应用程序要求的设置。

**创建和配置 IIS 网站**

1. 在本地文件系统上，创建用于存储内容的文件夹（例如， **C:\DemoSite**）。
2. 在 "**开始**" 菜单上，指向 "**管理工具**"，然后单击 " **Internet Information Services （IIS）管理器**"。
3. 在 IIS 管理器的 "**连接**" 窗格中，展开服务器节点（例如， **TESTWEB1**）。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. 右键单击 "**站点**" 节点，然后单击 "**添加网站**"。
5. 在 "**站点名称**" 框中，键入 IIS 网站的名称（例如， **DemoSite**）。
6. 在 "**物理路径**" 框中，键入（或浏览到）本地文件夹的路径（例如， **C:\DemoSite**）。
7. 在 "**端口**" 框中，键入要在其上托管网站的端口号（例如， **85**）。

    > [!NOTE]
    > 对于 HTTP，标准端口号为80，对于 HTTPS 则为443。 但是，如果你在端口80上托管此网站，你将需要停止默认网站，然后才能访问你的站点。
8. 将 "**主机名**" 框保留为空，除非你想要为网站配置域名系统（DNS）记录，然后单击 **"确定"** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > 在生产环境中，你可能想要在端口80上托管你的网站，并配置主机标头和匹配的 DNS 记录。 有关在 IIS 7 中配置主机标头的详细信息，请参阅[配置网站的主机标头（IIS 7）](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 有关 Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅[Dns 服务器概述](https://technet.microsoft.com/library/cc770392.aspx)和[dns 服务器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在 "**操作**" 窗格中的 "**编辑站点**" 下，单击 "**绑定**"。
10. 在“网站绑定”对话框中，单击“添加”。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. 在 "**添加站点绑定**" 对话框中，将 " **IP 地址**" 和 "**端口**" 设置为与现有站点配置匹配。
12. 在 "**主机名**" 框中，键入 web 服务器的名称（例如， **TESTWEB1**），然后单击 **"确定"** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > 第一个站点绑定允许使用 IP 地址和端口或 `http://localhost:85`本地访问站点。 第二个站点绑定允许使用计算机名称（例如 http://testweb1:85)，从域中的其他计算机访问站点。
13. 在 **“网站绑定”** 对话框中，单击 **“关闭”** 。
14. 在 "**连接**" 窗格中，单击 "**应用程序池**"。
15. 在 "**应用程序池**" 窗格中，右键单击应用程序池的名称，然后单击 "**基本设置**"。 默认情况下，应用程序池的名称将与网站的名称匹配（例如， **DemoSite**）。
16. 在 **.NET Framework 版本**"列表中，选择" **.NET Framework v 4.0.30319**"，然后单击 **" 确定 "** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > 示例解决方案需要 .NET Framework 4.0。 这并不是对 Web 部署一般的要求。

为了使你的网站提供内容，应用程序池标识必须对存储内容的本地文件夹具有读取权限。 在 IIS 7.5 中，应用程序池默认使用唯一的应用程序池标识运行（与以前版本的 IIS 不同，应用程序池通常使用 Network Service 帐户运行）。 应用程序池标识不是真实的用户帐户，并且不会显示在任何用户或组&#x2014;的列表中，而是在启动应用程序池时动态创建。 每个应用程序池标识都作为隐藏项添加到本地**IIS\_iis-iusrs**安全组。

若要授予对文件或文件夹上的应用程序池标识的权限，可以使用两个选项：

- 使用 IIS AppPool\</strong ><em>[应用程序池名称]</em>（例如<strong>IIS AppPool\DemoSite</strong>）的 <strong>格式，直接将权限分配给应用程序池标识。
- 将权限分配给**IIS\_iis-iusrs**组。

最常见的方法是将权限分配给本地**IIS\_iis-iusrs**组，因为此方法允许你在不重新配置文件系统权限的情况下更改应用程序池。 下一过程使用此基于组的方法。

> [!NOTE]
> 有关 IIS 7.5 中的应用程序池标识的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。

**配置 IIS 网站的文件夹权限**

1. 在 Windows 资源管理器中，浏览到本地文件夹的位置。
2. 右键单击该文件夹，然后单击 "**属性**"。
3. 在“**Security**”选项卡上，依次单击“**Edit**”、“**Add**”。
4. 单击“位置”。 在 "**位置**" 对话框中，选择本地服务器，然后单击 **"确定"** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. 在 "**选择用户或组**" 对话框中，键入**IIS\_Iis-iusrs**，单击 "**检查名称**"，然后单击 **"确定"** 。
6. 在 "<em>[文件夹名称]</em>的权限" 对话框中，请注意，默认情况下已为新组分配 "<strong>读取 &amp; 执行</strong>"、"<strong>列出文件夹内容</strong>" 和 "<strong>读取</strong>" 权限。 保持不变，并单击<strong>"确定"</strong>。
7. 单击<strong>"确定"</strong>以关闭 " <em>[文件夹名称]</em><strong>属性</strong>" 对话框。

作为最终任务，在尝试将任何 web 包部署到服务器之前，应确保 Web 部署代理服务正在运行。 从远程计算机部署包时，Web 部署代理服务负责提取和安装包的内容。 默认情况下，当你安装 Web 部署工具并在网络服务标识下运行时，将启动该服务。

你可以使用各种命令行实用工具或 Windows PowerShell cmdlet 来检查服务是否以多种不同的方式运行。 此过程描述了一个简单的基于 UI 的方法。

**检查 Web 部署代理服务是否正在运行**

1. 在“开始” 菜单上，指向“管理工具”，然后单击“服务”。
2. 找到 " **Web 部署代理服务**" 行，然后验证 "**状态**" 是否设置为 "**已启动**"。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. 如果该服务尚未启动，则单击 "**启动**"。

## <a name="configure-firewall-exceptions"></a>配置防火墙例外

默认情况下，远程代理服务在 TCP 端口80上侦听，网址为：

<http://servername.com/MSDEPLOYAGENTSERVICE>

在大多数情况下，你无需为远程代理服务配置任何其他防火墙规则，因为 web 服务器通常在端口80上侦听 HTTP 请求。 如果自定义安装以侦听非标准端口，则需要根据需要配置防火墙例外。

## <a name="conclusion"></a>结束语

此时，web 服务器已准备好接受并安装远程计算机上的 web 包。 尝试将 web 应用程序部署到服务器之前，可能需要检查以下要点：

- 是否已向 IIS 注册 ASP.NET 4.0？
- 应用程序池标识是否具有对你的网站的源文件夹的 "读取" 访问权限？
- Web 部署代理服务是否正在运行？

## <a name="further-reading"></a>其他阅读材料

有关如何配置自定义 Microsoft 生成引擎（MSBuild）项目文件以将 web 包部署到远程代理服务的指南，请参阅[配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。

> [!div class="step-by-step"]
> [上一页](scenario-configuring-a-production-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
