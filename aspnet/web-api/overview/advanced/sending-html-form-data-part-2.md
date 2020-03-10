---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 在 ASP.NET Web API 中发送 HTML 窗体数据：文件上传和多部分 ASP.NET 4。x
author: MikeWasson
description: 本教程演示如何将文件上传到 web API。 还介绍了如何处理多部分 MIME 数据。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449210"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="a8ab1-104">在 ASP.NET Web API 中发送 HTML 窗体数据：文件上传和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="a8ab1-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="a8ab1-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a8ab1-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="a8ab1-106">第2部分：文件上传和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="a8ab1-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="a8ab1-107">本教程演示如何将文件上传到 web API。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="a8ab1-108">还介绍了如何处理多部分 MIME 数据。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="a8ab1-109">[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="a8ab1-110">下面是用于上载文件的 HTML 窗体的示例：</span><span class="sxs-lookup"><span data-stu-id="a8ab1-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="a8ab1-111">此窗体包含文本输入控件和文件输入控件。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="a8ab1-112">当窗体包含文件输入控件时， **enctype**特性应始终 &quot;多部分/窗体数据&quot;，这将指定窗体将作为多部分 MIME 消息发送。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="a8ab1-113">通过查看示例请求，可以最轻松地了解多部分 MIME 消息的格式：</span><span class="sxs-lookup"><span data-stu-id="a8ab1-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="a8ab1-114">此消息分为两*部分*，分别用于每个窗体控件。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="a8ab1-115">部分边界由以破折号开头的行指示。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="a8ab1-116">部分边界包含随机组件（&quot;41184676334&quot;），以确保边界字符串不会意外出现在消息部分中。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="a8ab1-117">每个消息部分都包含一个或多个标头，后面是部分内容。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="a8ab1-118">内容处置标头包含控件的名称。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="a8ab1-119">对于文件，它还包含文件名。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="a8ab1-120">Content-type 标头介绍了该部分中的数据。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="a8ab1-121">如果省略此标头，则默认值为 text/简洁。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="a8ab1-122">在上面的示例中，用户使用内容类型 image/jpeg 上传了一个名为 GrandCanyon 的文件;并且文本输入的值为 &quot;夏天假期&quot;。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="a8ab1-123">文件上传</span><span class="sxs-lookup"><span data-stu-id="a8ab1-123">File Upload</span></span>

<span data-ttu-id="a8ab1-124">现在，让我们看看从多部分 MIME 消息读取文件的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="a8ab1-125">控制器将异步读取文件。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="a8ab1-126">Web API 使用[基于任务的编程模型](https://msdn.microsoft.com/library/dd460693.aspx)支持异步操作。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="a8ab1-127">首先，如果你针对的是支持**async**和**await**关键字的 .NET Framework 4.5，则代码为。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="a8ab1-128">请注意，控制器操作不采用任何参数。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="a8ab1-129">这是因为，我们处理操作中的请求正文，而不调用媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="a8ab1-130">**IsMultipartContent**方法检查请求是否包含多部分 MIME 消息。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="a8ab1-131">否则，控制器将返回 HTTP 状态代码415（不支持的媒体类型）。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="a8ab1-132">**MultipartFormDataStreamProvider**类是一个帮助器对象，它为上传的文件分配文件流。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="a8ab1-133">若要读取多部分 MIME 消息，请调用**ReadAsMultipartAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="a8ab1-134">此方法提取所有消息部分，并将其写入**MultipartFormDataStreamProvider**提供的流中。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="a8ab1-135">当方法完成时，可以从**FileData**属性获取有关文件的信息，该属性是**MultipartFileData**对象的集合。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="a8ab1-136">**MultipartFileData**是服务器上保存文件的本地文件名。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="a8ab1-137">**MultipartFileData**包含部件标题（*而不*是请求标头）。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="a8ab1-138">你可以使用它来访问\_处置和 Content-type 标头的内容。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="a8ab1-139">顾名思义， **ReadAsMultipartAsync**是一种异步方法。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="a8ab1-140">若要在方法完成后执行工作，请使用[延续任务](https://msdn.microsoft.com/library/ee372288.aspx)（.net 4.0）或**await**关键字（.net 4.5）。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="a8ab1-141">下面是前面代码的 .NET Framework 4.0 版本：</span><span class="sxs-lookup"><span data-stu-id="a8ab1-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="a8ab1-142">读取窗体控件数据</span><span class="sxs-lookup"><span data-stu-id="a8ab1-142">Reading Form Control Data</span></span>

<span data-ttu-id="a8ab1-143">我前面介绍的 HTML 窗体具有文本输入控件。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="a8ab1-144">可以从**MultipartFormDataStreamProvider**的**FormData**属性中获取该控件的值。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="a8ab1-145">**FormData**是包含窗体控件的名称/值对的**NameValueCollection** 。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="a8ab1-146">集合可以包含重复键。</span><span class="sxs-lookup"><span data-stu-id="a8ab1-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="a8ab1-147">请考虑以下形式：</span><span class="sxs-lookup"><span data-stu-id="a8ab1-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="a8ab1-148">请求正文可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="a8ab1-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="a8ab1-149">在这种情况下， **FormData**集合将包含以下键/值对：</span><span class="sxs-lookup"><span data-stu-id="a8ab1-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="a8ab1-150">行程：往返行程</span><span class="sxs-lookup"><span data-stu-id="a8ab1-150">trip: round-trip</span></span>
- <span data-ttu-id="a8ab1-151">选项：不间断</span><span class="sxs-lookup"><span data-stu-id="a8ab1-151">options: nonstop</span></span>
- <span data-ttu-id="a8ab1-152">选项：日期</span><span class="sxs-lookup"><span data-stu-id="a8ab1-152">options: dates</span></span>
- <span data-ttu-id="a8ab1-153">座位：窗口</span><span class="sxs-lookup"><span data-stu-id="a8ab1-153">seat: window</span></span>
