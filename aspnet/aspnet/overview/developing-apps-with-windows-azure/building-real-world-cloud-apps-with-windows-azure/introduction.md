---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 用 Azure 构建实际的云应用 |Microsoft Docs
author: MikeWasson
description: 此电子书指导你完成构建真实云解决方案的基于模式的方法。 这些模式适用于开发流程以及 。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: 8a4ef3aa37a9296e92fbeb513968e3abeee072d0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585520"
---
# <a name="building-real-world-cloud-apps-with-azure"></a>用 Azure 构建实际的云应用

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 此电子书指导你完成构建真实云解决方案的基于模式的方法。 模式适用于开发流程以及体系结构和编码实践。
> 
> 内容基于 Scott Guthrie 开发的演示文稿，他在2013年6月（[第 1](http://vimeo.com/68215538)部分、[第 2](http://vimeo.com/68215602)部分）和年 9 2013[月（第一部分，第](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324) [2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)部分）的 Microsoft Tech ED 澳大利亚的挪威开发人员大会（NDC）举行。 [许多人](more-patterns-and-guidance.md#acknowledgments)在将内容从视频转换为书面形式时更新并增加了内容。

## <a name="intended-audience"></a>目标受众

如果开发人员想要了解如何针对云进行开发（考虑迁移到云），或者是云开发新手，则可以从这里简要概述他们需要知道的最重要概念和实践。 概念以具体的示例为例，每个章节链接到其他资源以获取更深入的信息。 示例和指向其他资源的链接适用于 Microsoft 框架和服务，但阐释的原则也适用于其他 web 开发框架和云环境。

已为云开发的开发人员可能会在此处找到一些建议，使其更成功。 可以单独读取系列中的每一章，以便选择感兴趣的主题。

观看 Scott Guthrie 的任何人都可以*通过 Azure 演示来构建真实的云应用*，并希望获得更多详细信息和更新的信息。

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>云开发模式

本电子书介绍了适用于云开发的十三种建议模式。 此处使用 "模式" 是一种很大的意义，这意味着建议使用此方法完成操作：开发、设计和编码云应用的最佳方式。 这是一种关键模式，可帮助你 "成功进入成功"，前提是你跟随它们。

- [自动执行所有](automate-everything.md)操作。

    - 使用脚本可最大程度地提高效率，并最大程度地减少重复过程中的
    - 演示： Azure 管理脚本。
- [源代码管理](source-control.md)。 

    - 在源代码管理中设置分支结构，以便于 DevOps 工作流。
    - 演示：向源代码管理添加脚本。
    - 演示：使敏感数据不受源代码管理。
    - 演示：在 Visual Studio 中使用 Git。
- [持续集成和交付](continuous-integration-and-continuous-delivery.md)。 

    - 通过每个源代码管理签入自动完成生成和部署。
- [Web 开发最佳实践](web-development-best-practices.md)。 

    - 使 web 层保持无状态。
    - 演示：在 Azure App Service 中的 Web 应用中缩放和自动缩放。
    - 避免会话状态。
    - 在 CDN 不可用时，将 CDN 与回退配合使用。
    - 使用异步编程模型。
    - 演示： ASP.NET MVC 和实体框架中的异步。
- [单一登录](single-sign-on.md)。 

    - Azure Active Directory 简介。
    - 演示：创建使用 Azure Active Directory 的 ASP.NET 应用。
- [数据存储选项](data-storage-options.md)。 

    - 数据存储区的类型。
    - 如何选择正确的数据存储。
    - 演示： Azure SQL 数据库。
- [数据分区策略](data-partitioning-strategies.md)。 

    - 将数据垂直和/或水平分区，以便于缩放关系数据库。
- [非结构化 blob 存储](unstructured-blob-storage.md)。 

    - 使用 blob 服务在云中存储文件。
    - 演示：在 Fix It 应用中使用 blob 存储。
- [设计为可经受故障](design-to-survive-failures.md)。 

    - 故障类型。
    - 故障范围。
    - 了解 Sla。
- [监视和遥测](monitoring-and-telemetry.md)。 

    - 为什么您应该购买一个遥测应用程序并编写自己的代码来检测您的应用程序。
    - 演示： Azure 的新 Relic
    - 演示：在 Fix It 应用中记录代码。
    - 演示： Fix It 应用中的依赖关系注入。
    - 演示：在 Azure 中提供内置日志记录支持。
- [暂时性故障处理](transient-fault-handling.md)。 

    - 使用智能重试/回退逻辑来缓解暂时性故障的影响。
    - 演示：在实体框架6中重试/后退。
- [分布式缓存](distributed-caching.md)。 

    - 使用分布式缓存提高可伸缩性并降低数据库事务成本。
- 以[队列为中心的工作模式](queue-centric-work-pattern.md)。 

    - 实现高可用性，并通过松散耦合 web 和辅助角色层提高可伸缩性。
    - 演示： Fix It 应用中的 Azure 存储队列。
- [更多云应用模式和指南](more-patterns-and-guidance.md)。
- [附录：“Fix It”示例应用程序](the-fix-it-sample-application.md)

    - 已知问题
    - 最佳做法
    - 如何下载、构建、运行和部署。

这些模式适用于所有云环境，但我们将使用基于 Microsoft 技术和服务（如 Visual Studio、Team Foundation Service、ASP.NET 和 Azure）的示例来演示这些模式。

本章的其余部分介绍了 fix it 示例应用程序和 Web 应用在 Azure App Service 的云环境中运行。

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>Fix it 示例应用程序

本电子书中所示的大部分屏幕截图和代码示例都基于[Scott Guthrie](https://weblogs.asp.net/scottgu/)最初开发的 Fix It 应用，旨在演示推荐的云应用开发模式和实践。

![Fix It 应用主页](introduction/_static/image1.png)

该示例应用程序是一个简单的工作项票证系统。 当你需要固定的内容时，你可以创建一个票证并将其分配给某人，其他人可以登录并查看分配给他们的票证，并在完成工作后将票证标记为已完成。

这是标准的 Visual Studio web 项目。 它基于 ASP.NET MVC 构建并使用 SQL Server 数据库。 它可以在 IIS Express 本地运行，并且可以部署到 Azure 网站以在云中运行。 您可以使用窗体身份验证和本地数据库或使用社交提供程序（如 Google）登录。 （稍后我们还将演示如何使用 Active Directory 组织帐户进行登录。）

![登录页](introduction/_static/image2.png)

登录后，可以创建票证，将其分配给某人，并上传要修复的内容的图片。

![创建 Fix It 任务](introduction/_static/image3.png)

![已创建修复 It 任务](introduction/_static/image4.png)

你可以跟踪创建的工作项的进度，查看分配给你的票证，查看票证详细信息，并将项标记为已完成。

这是一个非常简单的应用程序，从功能角度看，您将了解如何生成该应用程序，以便它可以扩展到数百万的用户，并且可以灵活应对数据库故障和连接终止等因素。 你还将了解如何创建自动化的敏捷开发工作流，该工作流可让你轻松、快速地循环访问开发周期，使应用更好、更好地实现。

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Azure App Service 中的 Web 应用

用于 Fix It 应用程序的云环境是 Azure 的一种服务，我们称之为 "网站"。 此服务是一种可在 Azure 中托管自己的 web 应用的方法，无需创建 Vm，并使其保持更新、安装和配置 IIS 等。我们将网站托管在 Vm 上，并自动为你提供备份和恢复及其他服务。 网站服务适用于 ASP.NET、node.js、PHP 和 Python。 利用它，你可以使用 Visual Studio、Web 部署、FTP、Git 或 TFS 快速进行部署。 通常只需几秒钟即可开始部署，以及通过 Internet 进行更新的时间。 这一切都是免费的，可以在流量增长时进行扩展。

在幕后，Azure App Service 中的 Web 应用程序提供了大量体系结构组件和功能，如果您打算在自己的 Vm 上使用 IIS 来承载网站，则必须自行构建。 一个组件是自动配置 IIS 的部署终结点，并将你的应用程序安装到你想要在其上运行站点的任意多个 Vm 上。

![部署服务](introduction/_static/image5.png)

当用户访问该网站时，他们不会直接命中 IIS Vm，而是通过[应用程序请求路由（ARR）](https://www.iis.net/downloads/microsoft/application-request-routing)负载平衡器。 您可以将这些服务器与自己的服务器一起使用，但此处的优点是它们会自动设置。 它们使用智能试探法，其中包括会话相关性、IIS 中的队列深度和每台计算机上的 CPU 使用率等因素，以将流量定向到托管您的网站的虚拟机。

![ARR 负载均衡器](introduction/_static/image6.png)

如果某个计算机出现故障，Azure 会自动从轮换中提取该虚拟机，并启动新的 VM 实例，并开始将流量定向到新的实例-所有应用程序都不会停机。

![从计算机故障中自动恢复](introduction/_static/image7.png)

这一切都是自动进行的。 只需创建一个网站并使用 Windows PowerShell、Visual Studio 或 Azure 管理门户将应用程序部署到该网站。

有关演示如何在 Visual Studio 中创建 web 应用程序并将其部署到 Azure 网站的快捷快捷教程，请参阅[Azure 和 ASP.NET 入门](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。

<a id="summary"></a>
## <a name="summary"></a>总结

本简介提供了本书将介绍的主题的列表、示例应用程序的屏幕截图，以及 Azure App Service 云环境中的 Web 应用程序的简要概述。 在和中开发应用程序的一个很好的优点是，可以轻松地自动执行重复的开发任务，如创建测试环境并向其部署代码。 如何执行此操作是[下一章](automate-everything.md)的主题。

## <a name="resources"></a>资源

有关本章所涵盖主题的详细信息，请参阅以下资源。

文档：

- [Azure App Service 中的 Web 应用](https://azure.microsoft.com/services/app-service/web/)。 有关 Web 应用的 Azure 文档的门户页。
- [Web 应用、云服务和 Vm：何时使用哪些功能？](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) 如 WAWS 所示，只是在 Azure 中运行 web 应用的三种方法之一。 本文介绍三种方法之间的差异，并提供有关如何选择适合你的方案的指南。 与网站一样，云服务是 Azure 的一项 PaaS 功能。 Vm 是 IaaS 功能。 有关 PaaS 和 IaaS 的说明，请参阅 "[数据选项](data-storage-options.md#paasiaas)" 一章。

视频：

- [Scott Guthrie 从步骤0开始-什么是 Azure 云 OS？](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- 网站[体系结构-具有 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。
- [Azure 网站与 Nir Mashkowski 的内部机制](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。

> [!div class="step-by-step"]
> [下一页](automate-everything.md)
