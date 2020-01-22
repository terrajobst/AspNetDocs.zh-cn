---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: 数据分区策略（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: b8c901ec30b6d37237f80100a2978350ac389b7a
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519162"
---
# <a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>数据分区策略（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关序列的信息，请参阅[第一章](introduction.md)。

以前，我们了解到，通过添加和删除 web 服务器来扩展云应用程序的 web 层是多么简单。 但如果它们都碰到相同的数据存储，应用程序的瓶颈会从前端移到后端，并且数据层是最难缩放的。 在本章中，我们将介绍如何通过将数据分区到多个关系数据库中，或者通过将关系数据库存储与其他数据存储选项相结合来使数据层具有可伸缩性。

出于前面所述的相同原因，最大程度地设置分区方案：在应用投入生产后更改数据存储策略非常困难。 如果你认为之前有不同的方法，则可以在应用程序崩溃或长时间关闭，同时重新组织应用的数据和数据访问代码时避免出现 "Twitter"。

## <a name="the-three-vs-of-data-storage"></a>这三种数据存储

若要确定是否需要分区策略和应执行的操作，请考虑有关数据的三个问题：

- 卷–最终将存储多少数据？ 有几个千兆字节？ 有几百 gb？ 数万? Pb?
- 速度-数据增长的速率是多少？ 它是否是不生成大量数据的内部应用？ 客户要将图像和视频上传到的外部应用？
- 种类–您将存储哪种类型的数据？ 关系、图像、键值对、社交图？

如果您认为您要使用大量的卷、速度或种类，那么您必须仔细考虑哪种分区方案能让您的应用程序能够在增长时高效、高效地扩展，并确保不会遇到瓶颈。

有三种分区方法：

- 垂直分区
- 水平分区
- 混合分区

## <a name="vertical-partitioning"></a>垂直分区

垂直 portioning 类似于按列拆分表：一组列进入一个数据存储，另一组列进入不同的数据存储区。

例如，假设我的应用程序存储了有关用户的数据，包括图像：

![数据表](data-partitioning-strategies/_static/image1.png)

如果将此数据表示为表，并查看不同种类的数据，则可以看到左侧的三列具有可通过关系数据库高效存储的字符串数据，而右侧的两个列实质上是 c从图像文件中 ome。 可以将图像文件数据存储在关系数据库中，许多人会这样做，因为他们不想将数据保存到文件系统。 它们可能没有能够存储所需的数据量的文件系统，或者可能不想管理单独的备份和还原系统。 此方法非常适合用于本地数据库和云数据库中的少量数据。 在本地环境中，只需让 DBA 处理所有内容可能会更容易。

但在云数据库中，存储的成本相对较大，大量映像可能会使数据库的大小超出其有效运行的限制。 您可以通过对数据进行垂直分区来解决这些问题，这意味着您为数据表中的每一列都选择了最合适的数据存储区。 在此示例中，最好的做法是将字符串数据放入关系数据库和 Blob 存储中的图像。

![垂直分区的数据表](data-partitioning-strategies/_static/image2.png)

在云中存储图像而不是数据库在云中比在本地环境中更实用，因为无需担心设置文件服务器或管理在关系数据库外部存储的数据的备份和还原： allBlob 存储服务自动为你处理的。

这是我们在 Fix It 应用程序中实现的分区方法，我们将在[Blob 存储章节](unstructured-blob-storage.md)中查看该方法的代码。 如果没有此分区方案，并且假设平均图像大小为 3 mb，则在达到最大数据库大小 150 gb 之前，Fix It 应用程序将只能存储大约40000个任务。 删除映像后，数据库可存储10次以上的任务;在必须考虑如何实现水平分区方案之前，您可以更长时间。 随着应用程序的缩放，你的支出的增长速度会变慢，因为大量存储需求会成为非常廉价的 Blob 存储。

## <a name="horizontal-partitioning-sharding"></a>水平分区（分片）

水平 portioning 类似于按行拆分表：一个行集进入一个数据存储，另一组行进入不同的数据存储区。

给定相同的数据集，另一个选项是将不同范围的客户名称存储在不同的数据库中。

![水平分区的数据表](data-partitioning-strategies/_static/image3.png)

你需要非常小心地了解分片方案，以确保将数据均匀分布，以避免热点。 此简单示例使用姓氏的首字母不符合该要求，因为很多人都具有以某些常见字母开头的姓氏。 你需要达到比预期更早的表大小限制，因为在大多数情况下，一些数据库会变得非常大。

水平分区的下层是在对所有数据进行查询时可能很难。 在此示例中，查询必须从最多26个不同的数据库中进行绘制，才能获取应用存储的所有数据。

## <a name="hybrid-partitioning"></a>混合分区

可以合并垂直分区和水平分区。 例如，在示例数据中，可以在 Blob 存储中存储图像，并对字符串数据进行水平分区。

![已分区的数据表混合](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>对生产应用程序进行分区

从概念上讲，可以很容易地看出分区方案的工作原理，但任何分区方案都会增加代码的复杂性，并引入一些您必须处理的新的复杂问题。 如果要将图像移到 blob 存储，请在存储服务关闭时执行哪些操作？ 如何处理 blob 安全？ 如果数据库和 blob 存储不同步，会出现什么情况？ 如果你是分片，如何处理跨所有数据库的查询？

只要您在规划到生产环境之前对其进行规划，就可以管理这些问题。 许多人都不想这么做。 平均而言，我们的客户咨询团队（CAT）团队每月从其应用程序 panicked 的客户的每月一次拨打电话。 它们说： "帮助！ 我将所有内容放在一个数据存储区中，在45天内，我将用完了！ 而且，如果你有大量业务逻辑内置于你访问数据存储区的方式，并且你的客户使用的是你的应用程序，那么在迁移时，可能会有一天时间停机。 我们最终会经历 herculean 的工作，帮助客户动态地对数据进行分区，无停机时间。 如果可以避免遇到这种情况，这种方法非常令人兴奋，而且并不是您想要参与的事情！ 考虑到这一点，并将其集成到应用程序中，如果应用程序在以后增长，就会使生活变得更加轻松。

## <a name="summary"></a>摘要

使用有效的分区方案，你的云应用可以在没有瓶颈的情况下扩展到云中的 pb 数据。 如果你是在本地数据中心运行应用程序，则无需为大规模计算机或大量基础结构付费。 在云中，你可以根据需要增量添加容量，你只需在使用它时付费。

在[下一章](unstructured-blob-storage.md)中，我们将了解如何通过在 Blob 存储中存储图像来实现垂直分区。

## <a name="resources"></a>资源

有关分区策略的详细信息，请参阅以下资源。

文档：

- [在 Windows Azure 云服务上设计大规模服务的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 通过标记 Simm 和 Michael Thomassy 的白皮书。
- [Microsoft 模式和实践-云设计模式](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅数据分区指南，分片模式。

视频：

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景是通过 Microsoft 客户咨询团队（CAT）的实际客户体验。 请参阅剧集7中的分区讨论。
- [构建大：从 Microsoft Azure 客户了解的课程-第 I 部分](https://channel9.msdn.com/Events/Build/2012/3-029)。标记 Simm 讨论分区方案、分片策略、如何实现分片和 SQL 数据库联合，从19:49 开始。 与故障保护系列类似，但更详细地介绍了更多操作方法。

示例代码：

- [Windows Azure 中的云服务基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 包含分片数据库的示例应用程序。 有关实现的分片方案的说明，请参阅 Windows Azure 博客上的[分片](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx)。

> [!div class="step-by-step"]
> [上一页](data-storage-options.md)
> [下一页](unstructured-blob-storage.md)
