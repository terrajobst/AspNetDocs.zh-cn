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
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456786"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="de0b5-104">非结构化 Blob 存储（通过 Azure 构建实际的云应用）</span><span class="sxs-lookup"><span data-stu-id="de0b5-104">Unstructured Blob Storage (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="de0b5-105">作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="de0b5-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="de0b5-106">[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="de0b5-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="de0b5-107">**使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="de0b5-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="de0b5-108">它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。</span><span class="sxs-lookup"><span data-stu-id="de0b5-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="de0b5-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="de0b5-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="de0b5-110">在前面的章节中，我们介绍了分区方案，并说明了 Fix It 应用程序如何在 Azure 存储 Blob 服务中存储映像，以及如何在 Azure SQL 数据库中存储其他任务数据。</span><span class="sxs-lookup"><span data-stu-id="de0b5-110">In the previous chapter we looked at partitioning schemes and explained how the Fix It app stores images in the Azure Storage Blob service, and other task data in Azure SQL Database.</span></span> <span data-ttu-id="de0b5-111">在本章中，我们将深入探讨 Blob 服务，并演示如何在 Fix It 项目代码中实现它。</span><span class="sxs-lookup"><span data-stu-id="de0b5-111">In this chapter we go deeper into the Blob service and show how it's implemented in Fix It project code.</span></span>

## <a name="what-is-blob-storage"></a><span data-ttu-id="de0b5-112">什么是 Blob 存储？</span><span class="sxs-lookup"><span data-stu-id="de0b5-112">What is Blob storage?</span></span>

<span data-ttu-id="de0b5-113">Azure 存储 Blob 服务提供了一种在云中存储文件的方法。</span><span class="sxs-lookup"><span data-stu-id="de0b5-113">The Azure Storage Blob service provides a way to store files in the cloud.</span></span> <span data-ttu-id="de0b5-114">与在本地网络文件系统中存储文件相比，Blob 服务具有很多优点：</span><span class="sxs-lookup"><span data-stu-id="de0b5-114">The Blob service has a number of advantages over storing files in a local network file system:</span></span>

- <span data-ttu-id="de0b5-115">它具有高度可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="de0b5-115">It's highly scalable.</span></span> <span data-ttu-id="de0b5-116">单个存储帐户可以存储[几百 tb](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)，并且可以有多个存储帐户。</span><span class="sxs-lookup"><span data-stu-id="de0b5-116">A single Storage account can store [hundreds of terabytes](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), and you can have multiple Storage accounts.</span></span> <span data-ttu-id="de0b5-117">一些最大的 Azure 客户存储了数百 pb。</span><span class="sxs-lookup"><span data-stu-id="de0b5-117">Some of the biggest Azure customers store hundreds of petabytes.</span></span> <span data-ttu-id="de0b5-118">Microsoft SkyDrive 使用 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="de0b5-118">Microsoft SkyDrive uses blob storage.</span></span>
- <span data-ttu-id="de0b5-119">这是持久的。</span><span class="sxs-lookup"><span data-stu-id="de0b5-119">It's durable.</span></span> <span data-ttu-id="de0b5-120">将自动备份存储在 Blob 服务中的每个文件。</span><span class="sxs-lookup"><span data-stu-id="de0b5-120">Every file you store in the Blob service is automatically backed up.</span></span>
- <span data-ttu-id="de0b5-121">它提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="de0b5-121">It provides high availability.</span></span> <span data-ttu-id="de0b5-122">[存储的 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)承诺99.9% 或99.99% 的时间，具体取决于你选择的地理冗余选项。</span><span class="sxs-lookup"><span data-stu-id="de0b5-122">The [SLA for Storage](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) promises 99.9% or 99.99% uptime, depending on which geo-redundancy option you choose.</span></span>
- <span data-ttu-id="de0b5-123">它是 Azure 的平台即服务（PaaS）功能，这意味着只需存储和检索文件，只需为所使用的实际存储量付费，Azure 就会自动负责设置和管理所需的所有 Vm 和磁盘驱动器。服务.</span><span class="sxs-lookup"><span data-stu-id="de0b5-123">It's a platform-as-a-service (PaaS) feature of Azure, which means you just store and retrieve files, paying only for the actual amount of storage you use, and Azure automatically takes care of setting up and managing all of the VMs and disk drives required for the service.</span></span>
- <span data-ttu-id="de0b5-124">可以通过使用 REST API 或使用编程语言 API 来访问 Blob 服务。</span><span class="sxs-lookup"><span data-stu-id="de0b5-124">You can access the Blob service by using a REST API or by using a programming language API.</span></span> <span data-ttu-id="de0b5-125">Sdk 适用于 .NET、Java、Ruby 和其他。</span><span class="sxs-lookup"><span data-stu-id="de0b5-125">SDKs are available for .NET, Java, Ruby, and others.</span></span>
- <span data-ttu-id="de0b5-126">当你将文件存储在 Blob 服务中时，你可以轻松地通过 Internet 对其进行公开使用。</span><span class="sxs-lookup"><span data-stu-id="de0b5-126">When you store a file in the Blob service, you can easily make it publicly available over the Internet.</span></span>
- <span data-ttu-id="de0b5-127">你可以保护 Blob 服务中的文件，以便只能由授权用户访问它们，也可以提供临时访问令牌，使其仅在有限的时间段内可供他人使用。</span><span class="sxs-lookup"><span data-stu-id="de0b5-127">You can secure files in the Blob service so they can accessed only by authorized users, or you can provide temporary access tokens that makes them available to someone only for a limited period of time.</span></span>

<span data-ttu-id="de0b5-128">每次为 Azure 构建应用时，如果你想要在本地环境中存储大量数据，则会在文件中（例如图像、视频、Pdf、电子表格等）执行这些文件。</span><span class="sxs-lookup"><span data-stu-id="de0b5-128">Anytime you're building an app for Azure and you want to store a lot of data that in an on-premises environment would go in files -- such as images, videos, PDFs, spreadsheets, etc. -- consider the Blob service.</span></span>

## <a name="creating-a-storage-account"></a><span data-ttu-id="de0b5-129">创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="de0b5-129">Creating a Storage account</span></span>

<span data-ttu-id="de0b5-130">若要开始使用 Blob 服务，请在 Azure 中创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="de0b5-130">To get started with the Blob service you create a Storage account in Azure.</span></span> <span data-ttu-id="de0b5-131">在门户中，单击 "**新建**" " -- **Data Services** " -- **存储**" -- **快速创建**"，然后输入 URL 和数据中心位置。</span><span class="sxs-lookup"><span data-stu-id="de0b5-131">In the portal, click **New** -- **Data Services** -- **Storage** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="de0b5-132">数据中心位置应与 web 应用相同。</span><span class="sxs-lookup"><span data-stu-id="de0b5-132">The data center location should be the same as your web app.</span></span>

![创建存储帐户](unstructured-blob-storage/_static/image1.png)

<span data-ttu-id="de0b5-134">选择要在其中存储内容的主要区域，并且如果选择[异地复制](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)选项，Azure 将在该国家/地区的另一个区域中的另一个数据中心创建所有数据的副本。</span><span class="sxs-lookup"><span data-stu-id="de0b5-134">You pick the primary region where you want to store the content, and if you choose the [geo-replication](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) option, Azure creates replicas of all your data in a different data center in another region of the country.</span></span> <span data-ttu-id="de0b5-135">例如，如果选择 "美国西部" 数据中心，则在存储该文件时，它会转到 "美国西部" 数据中心，但在后台，Azure 还会将其复制到其他美国数据中心之一。</span><span class="sxs-lookup"><span data-stu-id="de0b5-135">For example, if you choose the Western US data center, when you store a file it goes to the Western US data center, but in the background Azure also copies it to one of the other US data centers.</span></span> <span data-ttu-id="de0b5-136">如果在该国家/地区的某个地区发生灾难，你的数据仍安全。</span><span class="sxs-lookup"><span data-stu-id="de0b5-136">If a disaster happens in one region of the country, your data is still safe.</span></span>

<span data-ttu-id="de0b5-137">Azure 不会跨异地政治边界复制数据：如果你的主要位置在美国，你的文件将仅复制到美国内的另一个区域;如果你的主要位置为 "澳大利亚"，则仅将你的文件复制到澳大利亚的另一个数据中心。</span><span class="sxs-lookup"><span data-stu-id="de0b5-137">Azure won't replicate data across geo-political boundaries: if your primary location is in the U.S., your files are only replicated to another region within the U.S.; if your primary location is Australia, your files are only replicated to another data center in Australia.</span></span>

<span data-ttu-id="de0b5-138">当然，您还可以通过执行脚本中的命令来创建存储帐户，如前文所述。</span><span class="sxs-lookup"><span data-stu-id="de0b5-138">Of course, you can also create a Storage account by executing commands from a script, as we saw earlier.</span></span> <span data-ttu-id="de0b5-139">下面是用于创建存储帐户的 Windows PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="de0b5-139">Here's a Windows PowerShell command to create a Storage account:</span></span>

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

<span data-ttu-id="de0b5-140">拥有存储帐户后，可以立即开始将文件存储在 Blob 服务中。</span><span class="sxs-lookup"><span data-stu-id="de0b5-140">Once you have a Storage account, you can immediately start storing files in the Blob service.</span></span>

## <a name="using-blob-storage-in-the-fix-it-app"></a><span data-ttu-id="de0b5-141">在 Fix It 应用中使用 Blob 存储</span><span class="sxs-lookup"><span data-stu-id="de0b5-141">Using Blob storage in the Fix It app</span></span>

<span data-ttu-id="de0b5-142">利用 Fix It 应用，你可以上载照片。</span><span class="sxs-lookup"><span data-stu-id="de0b5-142">The Fix It app enables you to upload photos.</span></span>

![创建 Fix It 任务](unstructured-blob-storage/_static/image2.png)

<span data-ttu-id="de0b5-144">单击 "**创建 fix it"** 时，应用程序将上传指定的映像文件，并将其存储在 Blob 服务中。</span><span class="sxs-lookup"><span data-stu-id="de0b5-144">When you click **Create the FixIt**, the application uploads the specified image file and stores it in the Blob service.</span></span>

### <a name="set-up-the-blob-container"></a><span data-ttu-id="de0b5-145">设置 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="de0b5-145">Set up the Blob container</span></span>

<span data-ttu-id="de0b5-146">若要将文件存储在 Blob 服务中，需要一个*容器*来存储它。</span><span class="sxs-lookup"><span data-stu-id="de0b5-146">In order to store a file in the Blob service you need a *container* to store it in.</span></span> <span data-ttu-id="de0b5-147">Blob 服务容器对应于文件系统文件夹。</span><span class="sxs-lookup"><span data-stu-id="de0b5-147">A Blob service container corresponds to a file system folder.</span></span> <span data-ttu-id="de0b5-148">在 "[自动执行所有操作" 一章](automate-everything.md)中查看的环境创建脚本将创建存储帐户，但不会创建容器。</span><span class="sxs-lookup"><span data-stu-id="de0b5-148">The environment creation scripts that we reviewed in the [Automate Everything chapter](automate-everything.md) create the Storage account, but they don't create a container.</span></span> <span data-ttu-id="de0b5-149">因此 `PhotoService` 类的 `CreateAndConfigure` 方法的用途是，如果容器尚不存在，则创建一个。</span><span class="sxs-lookup"><span data-stu-id="de0b5-149">So the purpose of the `CreateAndConfigure` method of the `PhotoService` class is to create a container if it doesn't already exist.</span></span> <span data-ttu-id="de0b5-150">此方法是从*global.asax*中的 `Application_Start` 方法调用的。</span><span class="sxs-lookup"><span data-stu-id="de0b5-150">This method is called from the `Application_Start` method in *Global.asax*.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

<span data-ttu-id="de0b5-151">存储帐户名称和访问密钥存储在*web.config 文件的*`appSettings` 集合中，而 `StorageUtils.StorageAccount` 方法中的代码使用这些值生成连接字符串并建立连接：</span><span class="sxs-lookup"><span data-stu-id="de0b5-151">The storage account name and access key are stored in the `appSettings` collection of the *Web.config* file, and code in the `StorageUtils.StorageAccount` method uses those values to build a connection string and establish a connection:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

<span data-ttu-id="de0b5-152">然后，`CreateAndConfigureAsync` 方法创建一个表示 Blob 服务的对象，并创建一个对象，该对象表示 Blob 服务中名为 "images" 的容器（文件夹）：</span><span class="sxs-lookup"><span data-stu-id="de0b5-152">The `CreateAndConfigureAsync` method then creates an object that represents the Blob service, and an object that represents a container (folder) named "images" in the Blob service:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

<span data-ttu-id="de0b5-153">如果名为 "images" 的容器尚不存在，则在第一次针对新存储帐户运行该应用程序时，该代码将创建容器并设置权限以使其成为公共的。</span><span class="sxs-lookup"><span data-stu-id="de0b5-153">If a container named "images" doesn't exist yet -- which will be true the first time you run the app against a new storage account -- the code creates the container and sets permissions to make it public.</span></span> <span data-ttu-id="de0b5-154">（默认情况下，新的 blob 容器是专用容器，只能由有权访问存储帐户的用户访问。）</span><span class="sxs-lookup"><span data-stu-id="de0b5-154">(By default, new blob containers are private and are accessible only to users who have permission to access your storage account.)</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a><span data-ttu-id="de0b5-155">在 Blob 存储中存储已上传的照片</span><span class="sxs-lookup"><span data-stu-id="de0b5-155">Store the uploaded photo in Blob storage</span></span>

<span data-ttu-id="de0b5-156">若要上载并保存图像文件，应用将在 `PhotoService` 类中使用 `IPhotoService` 接口和接口的实现。</span><span class="sxs-lookup"><span data-stu-id="de0b5-156">To upload and save the image file, the app uses an `IPhotoService` interface and an implementation of the interface in the `PhotoService` class.</span></span> <span data-ttu-id="de0b5-157">*PhotoService.cs*文件包含 Fix It 应用程序中与 Blob 服务通信的所有代码。</span><span class="sxs-lookup"><span data-stu-id="de0b5-157">The *PhotoService.cs* file contains all of the code in the Fix It app that communicates with the Blob service.</span></span>

<span data-ttu-id="de0b5-158">当用户单击 "**创建 fix it"** 时，将调用以下 MVC 控制器方法。</span><span class="sxs-lookup"><span data-stu-id="de0b5-158">The following MVC controller method is called when the user clicks **Create the FixIt**.</span></span> <span data-ttu-id="de0b5-159">在此代码中，`photoService` 引用 `PhotoService` 类的实例，`fixittask` 引用存储新任务的数据的 `FixItTask` 实体类的实例。</span><span class="sxs-lookup"><span data-stu-id="de0b5-159">In this code, `photoService` refers to an instance of the `PhotoService` class, and `fixittask` refers to an instance of the `FixItTask` entity class that stores data for a new task.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

<span data-ttu-id="de0b5-160">`PhotoService` 类中的 `UploadPhotoAsync` 方法将上载的文件存储在 Blob 服务中，并返回指向新 Blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="de0b5-160">The `UploadPhotoAsync` method in the `PhotoService` class stores the uploaded file in the Blob service and returns a URL that points to the new blob.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

<span data-ttu-id="de0b5-161">与 `CreateAndConfigure` 方法一样，代码会连接到存储帐户，并创建一个表示 "images" blob 容器的对象，但此处所述的容器已存在。</span><span class="sxs-lookup"><span data-stu-id="de0b5-161">As in the `CreateAndConfigure` method, the code connects to the storage account and creates an object that represents the "images" blob container, except here it assumes the container already exists.</span></span>

<span data-ttu-id="de0b5-162">然后，它通过将新的 GUID 值与文件扩展名连接来创建要上传的映像的唯一标识符：</span><span class="sxs-lookup"><span data-stu-id="de0b5-162">Then it creates a unique identifier for the image about to be uploaded, by concatenating a new GUID value with the file extension:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

<span data-ttu-id="de0b5-163">然后，该代码使用 blob 容器对象和新的唯一标识符来创建 blob 对象，在该对象上设置一个属性来指示它是哪种类型的文件，然后使用 blob 对象将文件存储在 blob 存储中。</span><span class="sxs-lookup"><span data-stu-id="de0b5-163">The code then uses the blob container object and the new unique identifier to create a blob object, sets an attribute on that object indicating what kind of file it is, and then uses the blob object to store the file in blob storage.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

<span data-ttu-id="de0b5-164">最后，它获取引用该 blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="de0b5-164">Finally, it gets a URL that references the blob.</span></span> <span data-ttu-id="de0b5-165">此 URL 将存储在数据库中，并且可用于修复它的网页以显示已上传的图像。</span><span class="sxs-lookup"><span data-stu-id="de0b5-165">This URL will be stored in the database and can be used in Fix It web pages to display the uploaded image.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

<span data-ttu-id="de0b5-166">此 URL 在数据库中存储为 FixItTask 表的一列。</span><span class="sxs-lookup"><span data-stu-id="de0b5-166">This URL is stored in the database as one of the columns of the FixItTask table.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

<span data-ttu-id="de0b5-167">如果只包含数据库中的 URL 和 Blob 存储中的映像，则 Fix It 应用会使数据库保持较小、可缩放且更便宜，同时存储映像，存储空间较低且能够处理 tb 或 pb。</span><span class="sxs-lookup"><span data-stu-id="de0b5-167">With only the URL in the database, and images in Blob storage, the Fix It app keeps the database small, scalable, and inexpensive, while the images are stored where storage is cheap and capable of handling terabytes or petabytes.</span></span> <span data-ttu-id="de0b5-168">一个存储帐户可以存储数百 tb 的修复 It 照片，你只需为你使用的部分付费。</span><span class="sxs-lookup"><span data-stu-id="de0b5-168">One storage account can store hundreds of terabytes of Fix It photos, and you only pay for what you use.</span></span> <span data-ttu-id="de0b5-169">这样，就可以开始为第一个千兆字节支付9美分，并为每个额外的 gb 为销售额添加更多映像。</span><span class="sxs-lookup"><span data-stu-id="de0b5-169">So you can start off small paying 9 cents for the first gigabyte, and add more images for pennies per additional gigabyte.</span></span>

### <a name="display-the-uploaded-file"></a><span data-ttu-id="de0b5-170">显示上传的文件</span><span class="sxs-lookup"><span data-stu-id="de0b5-170">Display the uploaded file</span></span>

<span data-ttu-id="de0b5-171">Fix It 应用程序在显示任务的详细信息时显示上传的图像文件。</span><span class="sxs-lookup"><span data-stu-id="de0b5-171">The Fix It application displays the uploaded image file when it displays details for a task.</span></span>

![利用照片修复 It 任务详细信息](unstructured-blob-storage/_static/image3.png)

<span data-ttu-id="de0b5-173">若要显示图像，所有 MVC 视图都必须包含发送到浏览器的 HTML 中的 `PhotoUrl` 值。</span><span class="sxs-lookup"><span data-stu-id="de0b5-173">To display the image, all the MVC view has to do is include the `PhotoUrl` value in the HTML sent to the browser.</span></span> <span data-ttu-id="de0b5-174">Web 服务器和数据库未使用循环来显示图像，只为图像 URL 提供几个字节。</span><span class="sxs-lookup"><span data-stu-id="de0b5-174">The web server and the database are not using cycles to display the image, they are only serving up a few bytes to the image URL.</span></span> <span data-ttu-id="de0b5-175">在以下 Razor 代码中，`Model` 引用 `FixItTask` 实体类的实例。</span><span class="sxs-lookup"><span data-stu-id="de0b5-175">In the following Razor code, `Model` refers to an instance of the `FixItTask` entity class.</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

<span data-ttu-id="de0b5-176">如果查看显示的页面的 HTML，则会看到指向 blob 存储中的图像的 URL，如下所示：</span><span class="sxs-lookup"><span data-stu-id="de0b5-176">If you look at the HTML of the page that displays, you see the URL pointing directly to the image in blob storage, something like this:</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a><span data-ttu-id="de0b5-177">总结</span><span class="sxs-lookup"><span data-stu-id="de0b5-177">Summary</span></span>

<span data-ttu-id="de0b5-178">已了解 Fix It 应用如何在 Blob 服务中存储映像，以及如何在 SQL 数据库中存储映像 Url。</span><span class="sxs-lookup"><span data-stu-id="de0b5-178">You've seen how the Fix It app stores images in the Blob service and only image URLs in the SQL database.</span></span> <span data-ttu-id="de0b5-179">使用 Blob 服务可以使 SQL 数据库比其他方式小得多，因此，可以扩展到几乎不受限制的任务，而无需编写大量代码即可完成。</span><span class="sxs-lookup"><span data-stu-id="de0b5-179">Using the Blob service keeps the SQL database much smaller than it otherwise would be, makes it possible to scale up to an almost unlimited number of tasks, and can be done without writing a lot of code.</span></span>

<span data-ttu-id="de0b5-180">在一个存储帐户中，你可以有几百 tb 的存储空间，与 SQL 数据库存储相比，存储成本要低得多，从大约每 gb 每千兆个字节到每个字节的3美分，再加上少量的事务费用。</span><span class="sxs-lookup"><span data-stu-id="de0b5-180">You can have hundreds of terabytes in a storage account, and the storage cost is much less expensive than SQL Database storage, starting at about 3 cents per gigabyte per month plus a small transaction charge.</span></span> <span data-ttu-id="de0b5-181">请记住，你不需要支付最大容量，而只需支付你实际存储的容量，因此你的应用程序已准备好进行缩放，但你不需要支付所有额外的容量。</span><span class="sxs-lookup"><span data-stu-id="de0b5-181">And keep in mind that you're not paying for the maximum capacity but only for the amount you actually store, so your app is ready to scale but you're not paying for all that extra capacity.</span></span>

<span data-ttu-id="de0b5-182">在[下一章](design-to-survive-failures.md)中，我们将讨论使云应用程序能够正常处理故障的重要性。</span><span class="sxs-lookup"><span data-stu-id="de0b5-182">In the [next chapter](design-to-survive-failures.md) we'll talk about the importance of making a cloud app capable of gracefully handling failures.</span></span>

## <a name="resources"></a><span data-ttu-id="de0b5-183">资源</span><span class="sxs-lookup"><span data-stu-id="de0b5-183">Resources</span></span>

<span data-ttu-id="de0b5-184">有关详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="de0b5-184">For more information see the following resources:</span></span>

- <span data-ttu-id="de0b5-185">[AZURE BLOB 存储简介](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。</span><span class="sxs-lookup"><span data-stu-id="de0b5-185">[An Introduction to Azure BLOB Storage](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/).</span></span> <span data-ttu-id="de0b5-186">由 Mike 木材撰写的博客。</span><span class="sxs-lookup"><span data-stu-id="de0b5-186">Blog by Mike Wood.</span></span>
- <span data-ttu-id="de0b5-187">[如何在 .net 中使用 Azure Blob 存储服务](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="de0b5-187">[How to use the Azure Blob Storage Service in .NET](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs).</span></span> <span data-ttu-id="de0b5-188">MicrosoftAzure.com 站点上的官方文档。</span><span class="sxs-lookup"><span data-stu-id="de0b5-188">Official documentation on the MicrosoftAzure.com site.</span></span> <span data-ttu-id="de0b5-189">Blob 存储简介，后面是代码示例，演示如何连接到 blob 存储、创建容器、上传和下载 blob 等。</span><span class="sxs-lookup"><span data-stu-id="de0b5-189">A brief introduction to blob storage followed by code examples showing how to connect to blob storage, create containers, upload and download blobs, etc.</span></span>
- <span data-ttu-id="de0b5-190">[故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。</span><span class="sxs-lookup"><span data-stu-id="de0b5-190">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="de0b5-191">九部分视频系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。</span><span class="sxs-lookup"><span data-stu-id="de0b5-191">Nine-part video series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="de0b5-192">以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景是通过 Microsoft 客户咨询团队（CAT）的实际客户体验。</span><span class="sxs-lookup"><span data-stu-id="de0b5-192">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="de0b5-193">有关 Azure 存储服务和 blob 的讨论，请参阅从35:13 开始的剧集5。</span><span class="sxs-lookup"><span data-stu-id="de0b5-193">For a discussion of Azure Storage service and blobs, see episode 5 starting at 35:13.</span></span>
- <span data-ttu-id="de0b5-194">[Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。</span><span class="sxs-lookup"><span data-stu-id="de0b5-194">[Microsoft Patterns and Practices - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx).</span></span> <span data-ttu-id="de0b5-195">请参阅附属 Key pattern。</span><span class="sxs-lookup"><span data-stu-id="de0b5-195">See Valet Key pattern.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="de0b5-196">[上一页](data-partitioning-strategies.md)
> [下一页](design-to-survive-failures.md)</span><span class="sxs-lookup"><span data-stu-id="de0b5-196">[Previous](data-partitioning-strategies.md)
[Next](design-to-survive-failures.md)</span></span>
