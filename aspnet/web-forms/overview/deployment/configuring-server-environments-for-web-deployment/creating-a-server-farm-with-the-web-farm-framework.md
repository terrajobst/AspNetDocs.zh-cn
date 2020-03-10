---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 使用 Web 场框架创建服务器场 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Web 场框架（WFF）2.0 从服务器集合创建和配置 web 服务器场。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517496"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a>使用 Web Farm Framework 创建服务器场

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用 Web 场框架（WFF）2.0 从服务器集合创建和配置 web 服务器场。

WFF 使你能够跨多个负载均衡的 web 服务器同步 web 平台产品和组件、web 应用程序、网站和配置设置。 在需要多个 web 服务器（如过渡环境和生产环境）的情况下，这可以极大地简化部署和配置过程。 你可以将 web 应用程序部署到&#x2014;*主服务器*&#x2014;的一台服务器上，WFF 将在服务器场中的所有其他 web 服务器上自动复制该 web 应用程序。

## <a name="understanding-the-web-farm-framework"></a>了解 Web 场框架

可以使用 WFF 2.0 预配、管理内容并将其部署到一组 web 服务器。 WFF 部署由三个关键服务器角色组成：

- *控制器服务器*。 使用此服务器创建和配置 WFF 服务器场。 控制器服务器管理 web 平台组件、配置设置和服务器场中 web 服务器之间的应用程序的同步。 在控制器服务器上安装 WFF 2.0，控制器服务器将依次在服务器场中的每台服务器上安装 WFF 代理。 控制器服务器在概念上并不属于任何 WFF 服务器场，单个控制器服务器可以管理多个服务器场。 在此方案中，将使用单个 WFF 控制器服务器来创建和管理过渡服务器场和生产服务器场。
- *主服务器*。 每个 WFF 服务器场都包含单个主服务器。 当你安装 web 平台组件或将应用程序部署到主服务器时，WFF 会将你所做的更改同步到服务器场中的所有其他服务器。
- *辅助服务器*。 每个 WFF 服务器场都包含一个或多个辅助服务器。 对主服务器所做的任何更改都会复制到服务器场中的每个辅助服务器。

这说明了这些服务器角色如何与 Fabrikam、Inc. 过渡和生产环境相关：

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

在此方案中，过渡环境和生产环境都配置为 WFF 服务器场。 单个 WFF 控制器服务器管理这两个服务器场。 在每个服务器场中，对主服务器所做的任何更改都会复制到每个辅助服务器。

在开始配置过渡环境和生产环境之前，我们建议你阅读以下文章，以熟悉 WFF 2.0 的关键概念：

- [用于 IIS 7 的 Web 场框架2.0 概述](https://go.microsoft.com/?linkid=9805126)
- [使用用于 IIS 7 的 Web 场框架2.0 设置服务器场](https://go.microsoft.com/?linkid=9805127)
- [用于 IIS 7 的 Web 场框架2.0 的系统和平台要求](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>任务概述

若要完成本主题中的任务和演练，你将需要至少三个&#x2014;服务器：一个 WFF 控制器，一个是服务器场的主 web 服务器，并且是服务器场的一个或多个辅助 web 服务器。 你可以随时将更多辅助服务器添加到 WFF 服务器场。 在高级别中，若要为过渡环境或生产环境创建和配置 WFF 服务器场，需要：

- 通过安装 Internet Information Services （IIS）7.5 和 WFF 2.0 创建控制器服务器。
- 通过创建通用的管理员帐户并配置防火墙例外来准备主服务器和辅助服务器。
- 使用控制器服务器上的 IIS 管理器来配置服务器场。
- 使用 IIS 应用程序请求路由（ARR）或其他负载平衡技术配置负载平衡。

本主题中的任务和演练假设你要从运行 Windows Server 2008 R2 的干净服务器版本开始。 在开始之前，对于每个服务器，请确保：

- Windows Server 2008 R2 Service Pack 1 和所有可用更新均已安装。
- 服务器已加入域。
- 服务器具有静态 IP 地址。

> [!NOTE]
> 有关将计算机加入域的详细信息，请参阅将[计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 有关配置静态 IP 地址的详细信息，请参阅[配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。

## <a name="create-the-wff-controller-server"></a>创建 WFF 控制器服务器

若要创建 WFF 控制器服务器，需要安装 IIS 7 或更高版本以及 WFF 2.0 或更高版本。 在这两个方面，WFF 使用 IIS Web 部署工具（Web 部署）2.x 来同步场中的服务器。 如果使用 Web 平台安装程序安装 WFF，则安装程序将自动下载并安装 Web 部署。

**创建 WFF 控制器服务器**

1. 下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9739157)。
2. 在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。
3. 在窗口左侧的导航窗格中，单击 "**服务器**"。
4. 在 " **IIS 7 推荐的配置**" 行中，单击 "**添加**"。
5. 在<strong>Web 场框架2中。</strong><em>x</em>行，单击 "<strong>添加</strong>"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. 单击“安装”。 请注意，Web 平台安装程序已在安装列表中添加了 Web 部署工具和其他各种依赖关系。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. 查看许可条款，如果同意条款，请单击 "**我接受**"。
8. 安装完成后，单击 "**完成**"，然后关闭 " **Web 平台安装程序 3.0** " 窗口。

## <a name="configure-the-primary-and-secondary-servers"></a>配置主服务器和辅助服务器

在创建 WFF 服务器场之前，应在将构成场的 web 服务器上完成一些准备任务：

- 添加防火墙例外以允许**核心网络**、**远程管理**以及**文件和打印机共享**功能与 WFF 控制器服务器进行通信。
- 在 Active Directory 中创建一个域帐户（例如， **FABRIKAM\stagingfarm**），并将其添加到每台服务器上的本地管理员组。 创建服务器场时，将使用此帐户作为服务器场管理员帐户。

有关如何在 Windows 防火墙中配置这些防火墙例外的详细信息，请参阅[适用于 IIS 7 的 Web 场框架2.0 的系统和平台要求](https://go.microsoft.com/?linkid=9805128)。 对于其他防火墙系统，请参阅产品文档。

您可以使用下一个过程将域帐户添加到 Windows Server 2008 R2 中的本地管理员组。 你应在要添加到服务器场&#x2014;中的每个服务器上执行此过程，换言之，将同一个域帐户添加到主服务器和每个辅助服务器上的本地管理员组中。

**将域帐户添加到本地管理员组**

1. 在 "**开始**" 菜单上，指向 "**管理工具**"，然后单击 "**服务器管理器**"。
2. 在 "**服务器管理器**" 窗口的树视图窗格中，展开 "**配置**"，展开 "**本地用户和组**"，然后单击 "**组**"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. 在 "**组**" 窗格中，双击 "**管理员**"。
4. 在 "**管理员属性**" 对话框中，单击 "**添加**"。
5. 在 "**选择用户、计算机、服务帐户或组**" 对话框中，键入（或浏览）到你的域帐户（例如， **FABRIKAM\stagingfarm**），然后单击 **"确定"** 。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. 在 "**管理员属性**" 对话框中，单击 **"确定"** 。

服务器现在可以添加到服务器场中。 对于主服务器，你可以在这两种情况下，将服务器配置为满足你在创建服务器场&#x2014;之前或之后的应用程序要求，WFF 将通过将相同的产品、组件或配置部署到辅助服务器来同步服务器。 为了简单起见，本教程假定你将在完成创建服务器场后配置主服务器。

## <a name="create-the-wff-server-farm"></a>创建 WFF 服务器场

此时，所有服务器都已准备好添加到 WFF 服务器场：

- 已在控制器服务器上安装 WFF。
- 你已在主和辅助 web 服务器上配置防火墙例外。
- 已将域帐户添加到主和辅助 web 服务器上的本地管理员组。

下一步是在 WFF 中创建服务器场。 可以从 WFF 控制器服务器上的 IIS 管理器执行此操作。

**创建 WFF 服务器场**

1. 在 WFF 控制器服务器上的 "**开始**" 菜单中，指向 "**管理工具**"，然后单击 " **Internet Information Services （IIS）管理器**"。
2. 在 "**连接**" 窗格中，展开本地服务器节点，右键单击 "**服务器场**"，然后单击 "**创建服务器场**"。
3. 在 "**创建服务器场**" 对话框中，为服务器场键入有意义的名称（例如，**过渡场**），然后选择 "**设置服务器场**"。
4. 键入添加到每个服务器上的本地管理员组的域帐户的用户名和密码。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. 单击 **“下一步”** 。
6. 在 "**添加服务器**" 页上，键入主服务器的完全限定的域名（FQDN），选择 "**主服务器**"，然后单击 "**添加**"。
7. 此时，WFF 将尝试使用所提供的凭据联系主服务器。 如果连接成功，则会将主服务器添加到 "**添加服务器**" 页上的表中。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > 您可能已注意到，默认情况下，**服务器可用于负载平衡**。 WFF 使用 IIS ARR 模块来实现负载平衡，从而在服务器场中的 web 服务器之间分发请求。 在大多数情况下，如果想要使用第三方负载平衡解决方案，只需清除 "**服务器可用于负载平衡**" 选项。
8. 在 "**添加服务器**" 页上，键入第一个辅助服务器的 FQDN，然后单击 "**添加**"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. 对场中的任何其他辅助服务器重复步骤7，然后单击 "**完成**"。

你的 WFF 服务器场现在已启动并正在运行。 在主服务器上安装的任何 web 平台产品或组件以及部署到主服务器的任何 web 应用程序或内容都将自动预配到所有辅助服务器上。

WFF 是一个广泛而又复杂的主题，你可以在[用于 IIS 7 的 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129)网站上了解有关该主题的详细信息。 但在这种情况下，需要注意以下两个功能区域：

- *应用程序预配*是指在服务器场中的所有辅助服务器上复制主服务器的内容（例如 web 应用程序和配置设置）的过程。 例如，如果您将联系人管理器示例解决方案部署到主临时服务器，则 WFF 应用程序预配过程会将此解决方案部署到所有辅助暂存服务器。 默认情况下，应用程序预配过程每隔30秒运行一次。
- *平台设置*是将 web 平台产品和组件从主服务器同步到服务器场中的所有辅助服务器的过程。 例如，如果在主过渡服务器上安装 ASP.NET MVC 3，则平台预配过程将使用 Web 平台安装程序在所有辅助暂存服务器上安装 ASP.NET MVC 3。 默认情况下，平台预配过程每五分钟运行一次。

你可以从 WFF 控制器服务器上的 IIS 管理器中管理基本应用程序和平台设置设置。

**了解应用程序和平台预配设置**

1. 在 IIS 管理器的 "**连接**" 窗格中，选择服务器场。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. 在 "**服务器场**" 窗格中，双击 "**应用程序设置**"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. 如您所见，服务器场当前配置为每隔30秒同步主服务器和辅助服务器之间的 web 内容和配置设置。
4. 单击 "**上一步**"，然后双击 "**平台设置**"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. 正如您所看到的，当前已将服务器场配置为每隔五分钟同步主服务器和辅助服务器之间的 web 平台产品和组件。
6. 单击 **“上一步”** 。
7. 若要强制服务器场立即同步 web 平台产品，请在 "**操作**" 窗格中单击 "**预配平台**"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > 平台设置可能需要一段时间。 安装程序进程在服务器场中的辅助服务器上的后台运行。
8. 一旦你已允许足够的时间来完成预配过程，你可以验证你已添加到主服务器的产品和组件现在已在辅助服务器上复制。 例如，你可以登录到辅助服务器，并使用 "**服务器管理器**" 窗口验证是否已安装 web 服务器角色。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. 你还可以查看 "已安装的程序" 列表以验证是否添加了各种 web 平台组件。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>配置负载均衡

创建 web 场时，需要设置某种形式的负载均衡，以便在 web 服务器之间分发 HTTP 请求。 这可能是 Windows Server 2008 网络负载平衡、IIS ARR 或基于软件的第三方或基于硬件的负载平衡解决方案。

WFF 旨在与 IIS ARR 紧密集成。 若要利用此集成，需要在 WFF 控制器服务器上安装 ARR 模块。 然后，你可以将所有 web 流量定向到控制器服务器，通常通过配置域名系统（DNS）记录。 然后，控制器服务器将根据服务器可用性和其他各种条件在服务器场中的服务器之间分发传入的请求。

> [!NOTE]
> 不需要对 WFF 使用 ARR;可以将 WFF 配置为使用第三方负载平衡解决方案。 有关详细信息，请参阅[用于 IIS 7 的 Web 场框架2.0 概述](https://go.microsoft.com/?linkid=9805126)。

使用 ARR 进行负载平衡是一个复杂的主题，其中大多数都超出了本教程的范围。 但是，您可以使用下一个过程安装 ARR 模块，并开始进行负载平衡。

**在 WFF 控制器服务器上设置负载均衡**

1. 在 WFF 控制器服务器上，启动 Web 平台安装程序。
2. 在**Web 平台安装程序 3.0**窗口的顶部，单击 "**产品**"。
3. 在窗口左侧的导航窗格中，单击 "**服务器**"。
4. 在**应用程序请求路由 2.5**行中，单击 "**添加**"。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. 单击 "**安装**"，然后按照**Web 平台安装**窗口中的说明进行操作。
6. 安装完成后，启动 IIS 管理器，然后在 "**连接**" 窗格中，单击 "服务器场" 节点。 请注意，已在 "**服务器场**" 窗格中添加了几个新图标。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. 在 "**服务器场**" 窗格中，双击 "**负载均衡**"。
8. 在 "**负载平衡**" 窗格中，选择负载平衡算法（例如，**最小的请求**）。

    > [!NOTE]
    > 有关负载平衡算法和其他配置设置的详细信息，请参阅[应用程序请求路由模块](https://go.microsoft.com/?linkid=9805130)。

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. 在 "**操作**" 窗格中，单击 "**应用**"。

你现在已为服务器场中的服务器配置了基本负载平衡。 如果将所有 web 场流量定向到控制器服务器，则会根据可用性和所选的负载平衡算法在服务器场中的服务器之间分配请求。

若要详细了解如何通过 ARR 配置负载平衡，请参阅[应用程序请求路由模块](https://go.microsoft.com/?linkid=9805130)。

## <a name="monitor-the-server-farm"></a>监视服务器场

你可以随时通过控制器服务器上的 IIS 管理器监视服务器场的运行状况。 在 "**连接**" 窗格中，展开服务器场，然后单击 "**服务器**"。 中间窗格将显示场中每个服务器的摘要，以及最近活动的跟踪日志。

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>结束语

WFF 服务器场现在应启动并运行。 你可以将主服务器配置为支持你首选&#x2014;的任何部署方法。有关详细信息&#x2014;，你的配置将在服务器场中的每个辅助服务器上复制。

## <a name="further-reading"></a>其他阅读材料

有关配置和使用 WFF 的所有方面的更多指导，请参阅[适用于 IIS 7 的 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129)网站。

> [!div class="step-by-step"]
> [上一页](configuring-a-database-server-for-web-deploy-publishing.md)
> [下一页](configuring-deployment-properties-for-a-target-environment.md)
