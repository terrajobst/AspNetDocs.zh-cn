---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 非结构化 Blob 存储（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: f48b2be755b84dff9b2672bd348c73107602c6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500408"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>非结构化 Blob 存储（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

在前面的章节中，我们介绍了分区方案，并说明了 Fix It 应用程序如何在 Azure 存储 Blob 服务中存储映像，以及如何在 Azure SQL 数据库中存储其他任务数据。 在本章中，我们将深入探讨 Blob 服务，并演示如何在 Fix It 项目代码中实现它。

## <a name="what-is-blob-storage"></a>什么是 Blob 存储？

Azure 存储 Blob 服务提供了一种在云中存储文件的方法。 与在本地网络文件系统中存储文件相比，Blob 服务具有很多优点：

- 它具有高度可伸缩性。 单个存储帐户可以存储[几百 tb](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)，并且可以有多个存储帐户。 一些最大的 Azure 客户存储了数百 pb。 Microsoft SkyDrive 使用 blob 存储。
- 这是持久的。 将自动备份存储在 Blob 服务中的每个文件。
- 它提供高可用性。 [存储的 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)承诺99.9% 或99.99% 的时间，具体取决于你选择的地理冗余选项。
- 它是 Azure 的平台即服务（PaaS）功能，这意味着只需存储和检索文件，只需为所使用的实际存储量付费，Azure 就会自动负责设置和管理所需的所有 Vm 和磁盘驱动器。服务.
- 可以通过使用 REST API 或使用编程语言 API 来访问 Blob 服务。 Sdk 适用于 .NET、Java、Ruby 和其他。
- 当你将文件存储在 Blob 服务中时，你可以轻松地通过 Internet 对其进行公开使用。
- 你可以保护 Blob 服务中的文件，以便只能由授权用户访问它们，也可以提供临时访问令牌，使其仅在有限的时间段内可供他人使用。

每次为 Azure 构建应用时，如果你想要在本地环境中存储大量数据，则会在文件中（例如图像、视频、Pdf、电子表格等）执行这些文件。

## <a name="creating-a-storage-account"></a>创建存储帐户

若要开始使用 Blob 服务，请在 Azure 中创建存储帐户。 在门户中，单击 "**新建**" " -- **Data Services** " -- **存储**" -- **快速创建**"，然后输入 URL 和数据中心位置。 数据中心位置应与 web 应用相同。

![创建存储帐户](unstructured-blob-storage/_static/image1.png)

选择要在其中存储内容的主要区域，并且如果选择[异地复制](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)选项，Azure 将在该国家/地区的另一个区域中的另一个数据中心创建所有数据的副本。 例如，如果选择 "美国西部" 数据中心，则在存储该文件时，它会转到 "美国西部" 数据中心，但在后台，Azure 还会将其复制到其他美国数据中心之一。 如果在该国家/地区的某个地区发生灾难，你的数据仍安全。

Azure 不会跨异地政治边界复制数据：如果你的主要位置在美国，你的文件将仅复制到美国内的另一个区域;如果你的主要位置为 "澳大利亚"，则仅将你的文件复制到澳大利亚的另一个数据中心。

当然，您还可以通过执行脚本中的命令来创建存储帐户，如前文所述。 下面是用于创建存储帐户的 Windows PowerShell 命令：

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

拥有存储帐户后，可以立即开始将文件存储在 Blob 服务中。

## <a name="using-blob-storage-in-the-fix-it-app"></a>在 Fix It 应用中使用 Blob 存储

利用 Fix It 应用，你可以上载照片。

![创建 Fix It 任务](unstructured-blob-storage/_static/image2.png)

单击 "**创建 fix it"** 时，应用程序将上传指定的映像文件，并将其存储在 Blob 服务中。

### <a name="set-up-the-blob-container"></a>设置 Blob 容器

若要将文件存储在 Blob 服务中，需要一个*容器*来存储它。 Blob 服务容器对应于文件系统文件夹。 在 "[自动执行所有操作" 一章](automate-everything.md)中查看的环境创建脚本将创建存储帐户，但不会创建容器。 因此 `PhotoService` 类的 `CreateAndConfigure` 方法的用途是，如果容器尚不存在，则创建一个。 此方法是从*global.asax*中的 `Application_Start` 方法调用的。

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

存储帐户名称和访问密钥存储在*web.config 文件的*`appSettings` 集合中，而 `StorageUtils.StorageAccount` 方法中的代码使用这些值生成连接字符串并建立连接：

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

然后，`CreateAndConfigureAsync` 方法创建一个表示 Blob 服务的对象，并创建一个对象，该对象表示 Blob 服务中名为 "images" 的容器（文件夹）：

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

如果名为 "images" 的容器尚不存在，则在第一次针对新存储帐户运行该应用程序时，该代码将创建容器并设置权限以使其成为公共的。 （默认情况下，新的 blob 容器是专用容器，只能由有权访问存储帐户的用户访问。）

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>在 Blob 存储中存储已上传的照片

若要上载并保存图像文件，应用将在 `PhotoService` 类中使用 `IPhotoService` 接口和接口的实现。 *PhotoService.cs*文件包含 Fix It 应用程序中与 Blob 服务通信的所有代码。

当用户单击 "**创建 fix it"** 时，将调用以下 MVC 控制器方法。 在此代码中，`photoService` 引用 `PhotoService` 类的实例，`fixittask` 引用存储新任务的数据的 `FixItTask` 实体类的实例。

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

`PhotoService` 类中的 `UploadPhotoAsync` 方法将上载的文件存储在 Blob 服务中，并返回指向新 Blob 的 URL。

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

与 `CreateAndConfigure` 方法一样，代码会连接到存储帐户，并创建一个表示 "images" blob 容器的对象，但此处所述的容器已存在。

然后，它通过将新的 GUID 值与文件扩展名连接来创建要上传的映像的唯一标识符：

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

然后，该代码使用 blob 容器对象和新的唯一标识符来创建 blob 对象，在该对象上设置一个属性来指示它是哪种类型的文件，然后使用 blob 对象将文件存储在 blob 存储中。

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

最后，它获取引用该 blob 的 URL。 此 URL 将存储在数据库中，并且可用于修复它的网页以显示已上传的图像。

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

此 URL 在数据库中存储为 FixItTask 表的一列。

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

如果只包含数据库中的 URL 和 Blob 存储中的映像，则 Fix It 应用会使数据库保持较小、可缩放且更便宜，同时存储映像，存储空间较低且能够处理 tb 或 pb。 一个存储帐户可以存储数百 tb 的修复 It 照片，你只需为你使用的部分付费。 这样，就可以开始为第一个千兆字节支付9美分，并为每个额外的 gb 为销售额添加更多映像。

### <a name="display-the-uploaded-file"></a>显示上传的文件

Fix It 应用程序在显示任务的详细信息时显示上传的图像文件。

![利用照片修复 It 任务详细信息](unstructured-blob-storage/_static/image3.png)

若要显示图像，所有 MVC 视图都必须包含发送到浏览器的 HTML 中的 `PhotoUrl` 值。 Web 服务器和数据库未使用循环来显示图像，只为图像 URL 提供几个字节。 在以下 Razor 代码中，`Model` 引用 `FixItTask` 实体类的实例。

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

如果查看显示的页面的 HTML，则会看到指向 blob 存储中的图像的 URL，如下所示：

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>摘要

已了解 Fix It 应用如何在 Blob 服务中存储映像，以及如何在 SQL 数据库中存储映像 Url。 使用 Blob 服务可以使 SQL 数据库比其他方式小得多，因此，可以扩展到几乎不受限制的任务，而无需编写大量代码即可完成。

在一个存储帐户中，你可以有几百 tb 的存储空间，与 SQL 数据库存储相比，存储成本要低得多，从大约每 gb 每千兆个字节到每个字节的3美分，再加上少量的事务费用。 请记住，你不需要支付最大容量，而只需支付你实际存储的容量，因此你的应用程序已准备好进行缩放，但你不需要支付所有额外的容量。

在[下一章](design-to-survive-failures.md)中，我们将讨论使云应用程序能够正常处理故障的重要性。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源：

- [AZURE BLOB 存储简介](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。 由 Mike 木材撰写的博客。
- [如何在 .net 中使用 Azure Blob 存储服务](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 MicrosoftAzure.com 站点上的官方文档。 Blob 存储简介，后面是代码示例，演示如何连接到 blob 存储、创建容器、上传和下载 blob 等。
- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分视频系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景是通过 Microsoft 客户咨询团队（CAT）的实际客户体验。 有关 Azure 存储服务和 blob 的讨论，请参阅从35:13 开始的剧集5。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅附属 Key pattern。

> [!div class="step-by-step"]
> [上一页](data-partitioning-strategies.md)
> [下一页](design-to-survive-failures.md)
