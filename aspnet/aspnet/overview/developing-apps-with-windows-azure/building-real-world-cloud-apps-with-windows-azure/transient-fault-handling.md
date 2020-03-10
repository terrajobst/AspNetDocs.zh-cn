---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: 暂时性故障处理（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: e798cb83cfb97db63fef6dc38c8f62804461d01b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500420"
---
# <a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>暂时性故障处理（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

设计真实的云应用程序时，必须考虑的一个问题是如何处理临时服务中断。 此问题在云应用中特别重要，因为你依赖于网络连接和外部服务。 通常情况下，你可能会获得极少的故障，这通常是自我修复的，如果你不打算智能地处理它们，它们将导致客户的体验不佳。

## <a name="causes-of-transient-failures"></a>暂时性故障的原因

在云环境中，会发现失败的和已删除的数据库连接定期发生。 这部分原因是，与本地环境相比，你的 web 服务器和数据库服务器之间有直接的物理连接，这是因为你要经历更多负载均衡器。 此外，当你依赖于多租户服务时，你会发现对服务的调用会变慢或超时，因为使用该服务的其他人会频繁地访问该服务。 在其他情况下，您可能是由于过于频繁地遇到服务的用户，并且服务有意限制您的身份–拒绝连接–以防您对服务的其他租户造成不利影响。

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>使用智能重试/回退逻辑来缓解暂时性故障的影响

您可以识别通常是暂时性的错误，并自动重试导致错误的操作，而不会引发异常并向客户显示 "不可用" 或 "错误" 页。 大多数情况下，该操作将在第二次尝试时成功完成，并且你将从错误中恢复，而客户却不知道存在问题。

可以通过多种方式实现智能重试逻辑。

- Microsoft 模式 &amp; 实践组具有[暂时性故障处理应用程序块](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx)，如果你使用 ADO.NET 进行 SQL 数据库访问（而不是通过实体框架），则会为你执行所有操作。 你只需设置重试策略-重试查询或命令的次数和尝试之间的等待时间，并在*使用*块中包装 SQL 代码。

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH 还支持[Azure 角色中缓存](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx)和[服务总线](https://azure.microsoft.com/services/service-bus/)。
- 使用实体框架通常不会直接使用 SQL 连接，因此不能使用此模式和实践包，但实体框架6会直接在框架中生成这种重试逻辑。 与指定重试策略的方式类似，在访问数据库时，EF 使用该策略。

    若要在 Fix It 应用中使用此功能，只需添加一个派生自*DbConfiguration*的类并打开重试逻辑。

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    对于框架识别为暂时性错误的 SQL 数据库异常，所示的代码指示 EF 重试操作最多3次，两次重试之间有指数的退接延迟，最大延迟为5秒。 指数回退是指在每次重试失败后，它将等待较长的一段时间，然后重试。 如果行中的三次尝试失败，则会引发异常。 以下关于断路熔断器的部分说明了为何要使用指数回退和数量有限的重试次数。

    使用 Azure 存储服务时，你可能会遇到类似的问题，因为 Fix It 应用对 Blob 执行此类工作，并且 .NET 存储客户端 API 已经实现了相同类型的逻辑。 你只需指定重试策略，或者，如果你对默认设置感到满意，则无需执行此操作。

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>断路熔断器

在一段时间内，如果不希望重试次数过多，则有几个原因：

- 太多用户持续重试失败的请求可能会降低其他用户的体验。 如果数百万人都发出重复的重试请求，你可能会占用 IIS 调度队列，并阻止你的应用程序处理请求，而该请求可能会成功处理。
- 如果每个用户在发生服务故障后重试，则可能会有许多请求在其开始恢复时被排队，该服务会变得溢出。
- 如果错误是由于限制导致的，并且服务将使用此时间窗口来进行限制，则继续重试可能会将该窗口移出并导致限制继续。
- 可能有用户正在等待网页呈现。 使人们的等待时间太长可能会更令人讨厌，因为这样会使用户在以后重试。

指数重试通过限制服务可从应用程序获取的重试频率来解决其中一些问题。 但还需要进行*断路*操作：这意味着，在某个特定的重试阈值，应用程序将停止重试并执行其他操作，例如以下操作之一：

- 自定义回退。 如果你无法从 Reuters 获得股票价格，你可能会从 Bloomberg 获取股票价格;或者，如果您无法从数据库获取数据，则可能可以从缓存中获取数据。
- 无提示失败。 如果你的应用程序所需的服务并不完全相同，则只在无法获取数据时返回 null。 如果要显示 Fix It 任务，但 Blob 服务没有响应，则可以在不使用映像的情况下显示任务详细信息。
- 快速失败。 错误：用户避免使用重试请求使服务扩散，这可能会导致其他用户的服务中断或扩展限制窗口。 可以显示友好的 "稍后重试" 消息。

没有任何一个大小合适的重试策略。 在异步后台工作进程中，你可以重试更多次并等待更长时间，而不是在用户等待响应的同步 web 应用中等待。 你可以等待关系数据库服务的重试次数超过缓存服务的重试次数。 下面是一些建议的重试策略示例，可让你了解数字的变化方式。 （"快速第一条" 表示第一次重试之前没有延迟。

![示例重试策略](transient-fault-handling/_static/image1.png)

有关 SQL 数据库重试策略指南，请参阅对[Sql 数据库的暂时性故障和连接错误进行故障排除](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)。

## <a name="summary"></a>摘要

在大多数情况下，重试/后退策略有助于使暂时错误对客户不可见，在使用 ADO.NET、实体框架或 Azure 存储服务时，Microsoft 提供了可用于最大程度地降低工作实现策略的框架。

[下一章](distributed-caching.md)介绍如何使用分布式缓存提高性能和可靠性。

## <a name="resources"></a>资源

有关更多信息，请参见以下资源：

文档

- [在 Azure 云服务上设计大规模服务的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 通过标记 Simm 和 Michael Thomassy 的白皮书。 与故障保护系列类似，但更详细地介绍了更多操作方法。 请参阅遥测和诊断部分。
- [防故障：弹性云体系结构的指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮书 by Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 防故障视频系列的网页版本。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅重试模式，计划程序代理监督程序模式。
- [AZURE SQL 数据库中的容错能力](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)。 Tony Petrossian 的博客文章。
- [实体框架连接复原/重试逻辑](https://msdn.microsoft.com/data/dn456835)。 如何使用和自定义实体框架6的暂时性故障处理功能。
- [ASP.NET MVC 应用程序中的实体框架的连接复原和命令截获](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四个系列系列教程中的第四部分介绍了如何设置 SQL 数据库的 EF 6 连接复原功能。

视频

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景是通过 Microsoft 客户咨询团队（CAT）的实际客户体验。 请参阅有关从40:55 开始的剧集3中的断路熔断器讨论。
- [构建大：从 Azure 客户获得的课程-第二部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 标记 Simm 讨论了如何针对故障、暂时性故障处理和检测一切进行设计。

代码示例

- [Azure 中的云服务基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 Microsoft Azure Customer 咨询团队创建的示例应用程序，演示如何使用[企业库暂时性故障处理块](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)（TFH）。 有关详细信息，请参阅[云服务基础数据访问层 - 临时故障处理](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)。 建议使用 TFH 直接使用 ADO.NET （不使用实体框架）进行数据库访问。

> [!div class="step-by-step"]
> [上一页](monitoring-and-telemetry.md)
> [下一页](distributed-caching.md)
