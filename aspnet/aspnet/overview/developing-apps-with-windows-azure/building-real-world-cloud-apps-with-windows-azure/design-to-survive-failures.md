---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: 在出现故障时进行设计（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: 9bf9acb8b4f8521d03c053c124c5fc4a07d6cb9a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585657"
---
# <a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>设计为可经受故障（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

在构建任意类型的应用程序时必须考虑的一个问题是，特别是在云中运行的应用程序，它是如何设计应用程序，以便能够正确地处理故障并继续提供价值，可以. 只要有足够的时间，在任何环境或任何软件系统中都会出错。 你的应用如何处理这些情况确定你的客户将获得的不确定程度，以及你需要花费多少时间来分析和解决问题。

## <a name="types-of-failures"></a>失败类型

你需要以不同方式处理两种基本类别的故障：

- 暂时性的自我修复故障，例如间歇性网络连接问题。
- 需要干预的持久故障。

对于暂时性故障，你可以实施重试策略，以确保应用程序在大多数情况下快速自动恢复。 你的客户可能会注意到响应时间稍长，否则不会受到影响。 我们将在[暂时性故障处理一章](transient-fault-handling.md)中介绍一些处理这些错误的方法。

对于持久故障，你可以实施监视和日志记录功能，以便在出现问题时及时通知你，从而促进根本原因分析。 我们将介绍一些方法，帮助你在 "[监视和遥测" 一章](monitoring-and-telemetry.md)中了解这些类型的错误。

## <a name="failure-scope"></a>故障范围

还必须考虑故障范围–是否影响单个计算机、整个服务（如 SQL 数据库或存储）或整个区域。

![故障范围](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>计算机故障

在 Azure 中，发生故障的服务器自动替换为新的服务器，并且设计良好的云应用会自动、快速地从这种类型的故障中恢复。 更早地，我们增加了无状态 web 层的可伸缩性优势，并且从故障的服务器中轻松恢复是情形的另一个优点。 轻松恢复也是平台即服务（PaaS）功能（如 SQL 数据库和 Azure App Service Web 应用）的优点之一。 硬件故障很少见，但当它们发生时，这些服务会自动处理它们;在使用其中一种服务时，甚至无需编写代码来处理计算机故障。

### <a name="service-failures"></a>服务故障

通常，云应用程序使用多个服务。 例如，Fix It 应用程序使用 SQL 数据库服务，存储服务和 web 应用程序部署到 Azure App Service。 如果你所依赖的服务之一发生故障，你的应用程序会执行什么操作？ 对于某些服务失败，"很抱歉，请稍后再试" 消息可能是最佳做法。 但在许多情况下，您可以更好地执行操作。 例如，当后端数据存储关闭时，可以接受用户输入，显示 "你的请求已收到"，并暂时将输入存储在其他位置;然后，当需要的服务再次运行时，可以检索并处理输入。

以[队列为中心的工作模式](queue-centric-work-pattern.md)一章介绍了处理此方案的一种方法。 Fix It 应用将任务存储在 SQL 数据库中，但在 SQL 数据库关闭时，无需退出工作。 在本章中，我们将了解如何将任务的用户输入存储在队列中，以及如何使用工作进程读取队列和更新任务。 如果 SQL 已关闭，创建 Fix It 任务的功能不受影响;当 SQL 数据库可用时，工作进程可以等待并处理新的任务。

### <a name="region-failures"></a>区域故障

整个区域可能会失败。 自然灾害可能会损坏数据中心，它可能会被 meteor 平展，farmer burying 可以使用 backhoe 等来剪切数据中心的干线行。如果你的应用程序托管在 stricken 数据中心，你该做什么？ 可以将 Azure 中的应用设置为同时在多个区域中运行，以便在某个区域发生灾难时，你可以继续在另一个区域中运行。 此类故障非常罕见，大多数应用程序都不会经历必要的阻碍，以确保通过此类故障的服务不中断。 请参阅本章末尾的资源部分，了解有关如何通过区域故障使应用保持可用的信息。

Azure 的目标是更轻松地处理所有这些类型的故障，你将在以下章节中看到有关如何执行此操作的一些示例。

## <a name="slas"></a>协议

人们通常会在云环境中获悉服务级别协议（Sla）。 实质上，它们承诺公司对服务的可靠性。 99.9% 的 SLA 表示预计服务将在99.9% 的时间运行。 这是 SLA 的一个相当典型的值，并且听起来非常多，但你可能不会认识到多少个停机时间的实际数量为0.1%。 下面是一个表，其中显示了不同的 SLA 百分比在一年、一个月和一周内的停机时间。

![SLA 表](design-to-survive-failures/_static/image2.png)

因此，99.9% 的 SLA 表示你的服务可能会在一年或每月43.2 分钟后关闭8.76 小时。 这比大多数人都认识到的时间更多。 因此，作为开发人员，您需要注意一定的停机时间，并以合理的方式对其进行处理。 有人将使用您的应用程序，而服务即将关闭，并且您想要将该客户的负面影响降至最低。

你应了解的有关 SLA 的一项内容是它所引用的时间框架：每周、每月还是每年都会重置时钟？ 在 Azure 中，我们每月重置一次时钟，这比每年的 SLA 更好，因为每年 SLA 可以通过将它们偏移一系列好月份来隐藏错误月份。

当然，我们总是比 SLA 努力做到更好;通常，您的工作时间比此小得多。 承诺是，如果我们的运行时间超过了你可以要求花钱回来的最长时间。 您取回的资金量可能并不能完全补偿您对超出时间的业务影响，但 SLA 的这一环节将充当强制策略，并让您知道我们确实要认真对待。

### <a name="composite-slas"></a>复合 Sla

查看 Sla 时，需要考虑的一个重要事项是在应用中使用多个服务的影响，每个服务都有一个单独的 SLA。 例如，Fix It 应用使用 Azure App Service Web 应用、Azure 存储和 SQL 数据库。 下面是此电子书在2013年12月撰写的日期：

![SLA 网站、存储、SQL 数据库](design-to-survive-failures/_static/image3.png)

基于这些服务 Sla，应用的最大停机时间是多少？ 您可能认为停机时间等于最差的 SLA 百分比，在这种情况下，可能为99.9%。 如果所有三个服务始终都出现故障，但这并不是实际发生的情况，则会为 true。 每个服务可能会在不同时间独立失败，因此，你必须通过将各个 SLA 编号相乘来计算复合 SLA。

![复合 SLA](design-to-survive-failures/_static/image4.png)

因此，你的应用程序可能不会在每月43.2 分钟，而是每月3倍，每月108分钟–并且仍处于 Azure SLA 限制范围内。

此问题在 Azure 中不是唯一的。 我们实际上提供了任何可用云服务的最佳云 Sla，如果你使用任何供应商的云服务，你将遇到类似的问题。 重点介绍如何设计你的应用程序以合理地处理不可避免的服务故障，这一点非常重要，因为它们可能会经常发生，以影响你的客户或用户。

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>与企业停机体验相比的云 Sla

人们有时会说： "在我的企业应用程序中，我从未遇到过这些问题。" 如果你询问一个月的停机时间，他们通常会说： "当然，这是偶尔发生的。" 如果你询问的频率如何，他们将承认 "有时我们需要备份或安装新的服务器或更新软件"。 当然，这会计为关闭时间。 大多数企业应用程序（除非它们特别是任务关键型应用程序）实际上已超过服务 Sla 允许的时间量。 但是，当它是您的服务器和您的基础结构，并对其进行控制时，您的 angst 的时间可能不太大。 在云环境中，你依赖于其他人，并且你不知道发生了什么情况，因此你可能会担心更多的担心。

当企业实现比从云 SLA 获取更多的时间百分比时，他们可以通过在硬件上花费更多资金来实现此目的。 云服务可以这样做，但必须对其服务进行更多的收费。 相反，你可以利用经济高效的服务并设计你的软件，使你的客户无法实现最小中断。 作为云应用设计器，你的工作并不太多，无法避免发生灾难，并通过关注软件（而不是硬件）来实现此目的。 尽管企业应用会尽力最大限度地减少故障之间的平均时间，但云应用会尽力缩短平均恢复时间。

### <a name="not-all-cloud-services-have-slas"></a>并非所有云服务都具有 Sla

还要注意，并非每个云服务都具有 SLA。 如果你的应用程序依赖于一个没有时间保证的服务，你可能会比你想像的时间更长。 例如，如果使用 Facebook 或 Twitter 等社交提供程序启用登录到你的网站，请与服务提供商联系，以了解是否存在 SLA，你可能会发现没有 SLA。 但是，如果身份验证服务出现故障，或者不能支持您在其上抛出的请求量，则您的客户将被锁定在您的应用程序之外。 你可能会关闭几天或更长时间。 一个新应用程序的创建者预计数以百计的下载并依赖于 Facebook 身份验证，但在进行实时操作之前，不会与 Facebook 交互，因为这种服务没有 SLA。

### <a name="not-all-downtime-counts-toward-slas"></a>并非所有停机时间都会计入 Sla

如果你的应用程序过度使用，某些云服务可能会有意拒绝服务。 这称为*限制*。 如果服务具有 SLA，则它应声明你可能会受到限制的条件，并且你的应用程序设计应避免出现这些情况，并在发生此限制时正确地做出响应。 例如，如果在超过特定数量的每秒时，对服务的请求将开始失败，则需要确保自动重试不会快速进行，因为它们会导致限制继续。 在[暂时性故障处理一章](transient-fault-handling.md)中，我们将详细介绍限制。

## <a name="summary"></a>总结

本章已尝试帮助你认识到现实世界的云应用程序不能正常工作的原因。 从[下一章](monitoring-and-telemetry.md)开始，本系列中的其余模式将更详细地介绍一些可用于执行此操作的策略：

- 具有良好的[监视和遥测](monitoring-and-telemetry.md)，使你能够快速找到需要干预的故障，并提供足够的信息来解决这些问题。
- 通过实现智能重试逻辑来[处理暂时性故障](transient-fault-handling.md)，以便您的应用程序在不能时自动恢复，并回退到[断路](transient-fault-handling.md#circuitbreakers)器逻辑。
- 使用[分布式缓存](distributed-caching.md)来最大程度地减少数据库访问的吞吐量、延迟和连接问题。
- 通过以[队列为中心的工作模式](queue-centric-work-pattern.md)实现松散耦合，以便在后端停止时应用前端可以继续工作。

## <a name="resources"></a>资源

有关详细信息，请参阅此电子书中的后续章节和以下资源。

文档：

- [防故障：弹性云体系结构的指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮书 by Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 防故障视频系列的网页版本。
- [在 Azure 云服务上设计大规模服务的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 通过标记 Simm 和 Michael Thomassy 的白皮书。
- [Azure 业务连续性技术指南](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx)。 白皮书： Wickline 和 Jason Roth。
- [Azure 应用程序的灾难恢复和高可用性](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx)。 白皮书： Michael McKeown、Hanu Kommalapati 和 Jason Roth。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅多个数据中心部署指南，断路器模式。
- [Azure 支持-服务级别协议](https://azure.microsoft.com/support/legal/sla/)。
- [AZURE SQL Database 中的业务连续性](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx)。 有关 SQL 数据库高可用性和灾难恢复功能的文档。
- [Azure 虚拟机中 SQL Server 的高可用性和灾难恢复](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)。

视频：

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景是通过 Microsoft 客户咨询团队（CAT）的实际客户体验。 集1和8深入探讨了设计云应用程序以保持故障的原因。 另请参阅有关从49:57 开始的剧集2中的限制的后续讨论，请参阅第2点中的故障点和故障模式（从56:05 开始）讨论，并讨论从40:55 开始的剧集3中的断路熔断器。
- [构建大：从 Azure 客户获得的课程-第二部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 标记 Simm 讨论了如何针对故障进行设计并检测所有内容。 与故障保护系列类似，但更详细地介绍了更多操作方法。

> [!div class="step-by-step"]
> [上一页](unstructured-blob-storage.md)
> [下一页](monitoring-and-telemetry.md)
