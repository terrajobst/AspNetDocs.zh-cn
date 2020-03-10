---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: 在 ASP.NET 网页（Razor）站点中使用图像 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何在网站中添加、显示和操作图像（调整大小、翻转和添加水印）。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 53514b3c314fc182a43c82974ffcfa8158a636a1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512876"
---
# <a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="dd88d-103">使用 ASP.NET 网页（Razor）站点中的图像</span><span class="sxs-lookup"><span data-stu-id="dd88d-103">Working with Images in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="dd88d-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="dd88d-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="dd88d-105">本文介绍如何在 ASP.NET 网页（Razor）网站中添加、显示和处理图像（调整大小、翻转和添加水印）。</span><span class="sxs-lookup"><span data-stu-id="dd88d-105">This article shows you how to add, display, and manipulate images (resize, flip, and add watermarks) in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="dd88d-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="dd88d-107">如何将图像动态添加到页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-107">How to add an image to a page dynamically.</span></span>
> - <span data-ttu-id="dd88d-108">如何让用户上传图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-108">How to let users upload an image.</span></span>
> - <span data-ttu-id="dd88d-109">如何调整图像大小。</span><span class="sxs-lookup"><span data-stu-id="dd88d-109">How to resize an image.</span></span>
> - <span data-ttu-id="dd88d-110">如何翻转或旋转图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-110">How to flip or rotate an image.</span></span>
> - <span data-ttu-id="dd88d-111">如何向图像添加水印。</span><span class="sxs-lookup"><span data-stu-id="dd88d-111">How to add a watermark to an image.</span></span>
> - <span data-ttu-id="dd88d-112">如何使用图像作为水印。</span><span class="sxs-lookup"><span data-stu-id="dd88d-112">How to use an image as a watermark.</span></span>
> 
> <span data-ttu-id="dd88d-113">下面是本文中引入的 ASP.NET 编程功能：</span><span class="sxs-lookup"><span data-stu-id="dd88d-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="dd88d-114">`WebImage` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="dd88d-114">The `WebImage` helper.</span></span>
> - <span data-ttu-id="dd88d-115">`Path` 对象，它提供允许操作路径和文件名的方法。</span><span class="sxs-lookup"><span data-stu-id="dd88d-115">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dd88d-116">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="dd88d-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="dd88d-117">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="dd88d-117">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="dd88d-118">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="dd88d-118">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="dd88d-119">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="dd88d-119">This tutorial also works with WebMatrix 3.</span></span>

<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a><span data-ttu-id="dd88d-120">动态将图像添加到网页</span><span class="sxs-lookup"><span data-stu-id="dd88d-120">Adding an Image to a Web Page Dynamically</span></span>

<span data-ttu-id="dd88d-121">在开发网站的同时，您可以将图像添加到您的网站和各个页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-121">You can add images to your website and to individual pages while you're developing the website.</span></span> <span data-ttu-id="dd88d-122">你还可以让用户上传图像，这对于允许他们添加个人资料照片的任务可能很有用。</span><span class="sxs-lookup"><span data-stu-id="dd88d-122">You can also let users upload images, which might be useful for tasks like letting them add a profile photo.</span></span>

<span data-ttu-id="dd88d-123">如果你的站点上已有一个映像，而你只想在页面上显示该图像，则可使用如下所示的 HTML `<img>` 元素：</span><span class="sxs-lookup"><span data-stu-id="dd88d-123">If an image is already available on your site and you just want to display it on a page, you use an HTML `<img>` element like this:</span></span>

[!code-html[Main](9-working-with-images/samples/sample1.html)]

<span data-ttu-id="dd88d-124">但有时，您需要能够动态&#8212;显示图像，即在页面运行之前不知道要显示的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-124">Sometimes, though, you need to be able to display images dynamically &#8212; that is, you don't know what image to display until the page is running.</span></span>

<span data-ttu-id="dd88d-125">本部分中的过程演示如何在用户在图像名称列表中指定图像文件名的动态位置显示图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-125">The procedure in this section shows how to display an image on the fly where users specify the image file name from a list of image names.</span></span> <span data-ttu-id="dd88d-126">它们从下拉列表中选择映像的名称，并在提交页面时显示所选图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-126">They select the name of the image from a drop-down list, and when they submit the page, the image they selected is displayed.</span></span>

<span data-ttu-id="dd88d-127">![影像](9-working-with-images/_static/image1.jpg "ch9images-1")</span><span class="sxs-lookup"><span data-stu-id="dd88d-127">![[image]](9-working-with-images/_static/image1.jpg "ch9images-1.jpg")</span></span>

1. <span data-ttu-id="dd88d-128">在 WebMatrix 中，创建一个新网站。</span><span class="sxs-lookup"><span data-stu-id="dd88d-128">In WebMatrix, create a new website.</span></span>
2. <span data-ttu-id="dd88d-129">添加一个名为*DynamicImage*的新页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-129">Add a new page named *DynamicImage.cshtml*.</span></span>
3. <span data-ttu-id="dd88d-130">在网站的根文件夹中，添加一个新文件夹并将其命名为*images*。</span><span class="sxs-lookup"><span data-stu-id="dd88d-130">In the root folder of the website, add a new folder and name it *images*.</span></span>
4. <span data-ttu-id="dd88d-131">将四个图像添加到刚创建的*images*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dd88d-131">Add four images to the *images* folder you just created.</span></span> <span data-ttu-id="dd88d-132">（您可以方便地使用任何图像，但这些图像应该适合页面。）重命名*Photo1*、 *Photo2*、 *Photo3*和*Photo4*这一映像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-132">(Any images you have handy will do, but they should fit onto a page.) Rename the images *Photo1.jpg*, *Photo2.jpg*, *Photo3.jpg*, and *Photo4.jpg*.</span></span> <span data-ttu-id="dd88d-133">（在此过程中不使用*Photo4* ，但稍后将在本文中使用它。）</span><span class="sxs-lookup"><span data-stu-id="dd88d-133">(You won't use *Photo4.jpg* in this procedure, but you'll use it later in the article.)</span></span>
5. <span data-ttu-id="dd88d-134">验证四个图像是否未标记为只读。</span><span class="sxs-lookup"><span data-stu-id="dd88d-134">Verify that the four images are not marked as read-only.</span></span>
6. <span data-ttu-id="dd88d-135">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-135">Replace the existing content in the page with the following:</span></span>

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    <span data-ttu-id="dd88d-136">页面的正文包含一个名为 `photoChoice`的下拉列表（`<select>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="dd88d-136">The body of the page has a drop-down list (a `<select>` element) that's named `photoChoice`.</span></span> <span data-ttu-id="dd88d-137">此列表具有三个选项，每个列表选项的 `value` 属性都具有您在*images*文件夹中放置的某个图像的名称。</span><span class="sxs-lookup"><span data-stu-id="dd88d-137">The list has three options, and the `value` attribute of each list option has the name of one of the images that you put in the *images* folder.</span></span> <span data-ttu-id="dd88d-138">实质上，此列表使用户可以选择友好名称（如 &quot;照片 1&quot;），然后在提交页面时传递 *.jpg*文件名。</span><span class="sxs-lookup"><span data-stu-id="dd88d-138">Essentially, the list lets the user select a friendly name like &quot;Photo 1&quot;, and it then passes the *.jpg* file name when the page is submitted.</span></span>

    <span data-ttu-id="dd88d-139">在代码中，可以从列表中获取用户的选择（即图像文件名），方法是读取 `Request["photoChoice"]`。</span><span class="sxs-lookup"><span data-stu-id="dd88d-139">In the code, you can get the user's selection (in other words, the image file name) from the list by reading `Request["photoChoice"]`.</span></span> <span data-ttu-id="dd88d-140">首先查看是否有选择。</span><span class="sxs-lookup"><span data-stu-id="dd88d-140">You first see if there's a selection at all.</span></span> <span data-ttu-id="dd88d-141">如果有，则为映像创建一个路径，该路径包含图像的文件夹名称和用户的图像文件名。</span><span class="sxs-lookup"><span data-stu-id="dd88d-141">If there is, you construct a path for the image that consists of the name of the folder for the images and the user's image file name.</span></span> <span data-ttu-id="dd88d-142">（如果您尝试构造一个路径，但 `Request["photoChoice"]`中没有任何内容，则会出现错误。）这将产生如下所示的相对路径：</span><span class="sxs-lookup"><span data-stu-id="dd88d-142">(If you tried to construct a path but there was nothing in `Request["photoChoice"]`, you'd get an error.) This results in a relative path like this:</span></span>

    <span data-ttu-id="dd88d-143">*images/Photo1*</span><span class="sxs-lookup"><span data-stu-id="dd88d-143">*images/Photo1.jpg*</span></span>

    <span data-ttu-id="dd88d-144">路径存储在名为 `imagePath` 的变量中，稍后会在页面中用到。</span><span class="sxs-lookup"><span data-stu-id="dd88d-144">The path is stored in variable named `imagePath` that you'll need later in the page.</span></span>

    <span data-ttu-id="dd88d-145">在正文中，还有一个 `<img>` 元素，用于显示用户选择的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-145">In the body, there's also an `<img>` element that's used to display the image that the user picked.</span></span> <span data-ttu-id="dd88d-146">`src` 特性未设置为文件名或 URL，就像要显示静态元素一样。</span><span class="sxs-lookup"><span data-stu-id="dd88d-146">The `src` attribute isn't set to a file name or URL, like you'd do to display a static element.</span></span> <span data-ttu-id="dd88d-147">相反，它设置为 `@imagePath`，这意味着它将从您在代码中设置的路径获取其值。</span><span class="sxs-lookup"><span data-stu-id="dd88d-147">Instead, it's set to `@imagePath`, meaning that it gets its value from the path you set in code.</span></span>

    <span data-ttu-id="dd88d-148">但在页面首次运行时，没有要显示的图像，因为用户未选择任何内容。</span><span class="sxs-lookup"><span data-stu-id="dd88d-148">The first time that the page runs, though, there's no image to display, because the user hasn't selected anything.</span></span> <span data-ttu-id="dd88d-149">这通常意味着 `src` 特性将为空，并且图像将显示为红色的 &quot;x&quot; （或者浏览器在找不到图像时所呈现的任何内容）。</span><span class="sxs-lookup"><span data-stu-id="dd88d-149">This would normally mean that the `src` attribute would be empty and the image would show up as a red &quot;x&quot; (or whatever the browser renders when it can't find an image).</span></span> <span data-ttu-id="dd88d-150">若要防止出现这种情况，请将 `<img>` 元素放在测试的 `if` 块中，以确定 `imagePath` 变量中是否有任何内容。</span><span class="sxs-lookup"><span data-stu-id="dd88d-150">To prevent this, you put the `<img>` element in an `if` block that tests to see whether the `imagePath` variable has anything in it.</span></span> <span data-ttu-id="dd88d-151">如果用户进行了选择，`imagePath` 包含该路径。</span><span class="sxs-lookup"><span data-stu-id="dd88d-151">If the user made a selection, `imagePath` contains the path.</span></span> <span data-ttu-id="dd88d-152">如果用户未选择图像，或这是第一次显示页面，则不会呈现 `<img>` 元素。</span><span class="sxs-lookup"><span data-stu-id="dd88d-152">If the user didn't pick an image or if this is the first time the page is displayed, the `<img>` element isn't even rendered.</span></span>
7. <span data-ttu-id="dd88d-153">保存文件并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-153">Save the file and run the page in a browser.</span></span> <span data-ttu-id="dd88d-154">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）</span><span class="sxs-lookup"><span data-stu-id="dd88d-154">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
8. <span data-ttu-id="dd88d-155">从下拉列表中选择一个映像，然后单击 "**示例图像**"。</span><span class="sxs-lookup"><span data-stu-id="dd88d-155">Select an image from the drop-down list and then click **Sample Image**.</span></span> <span data-ttu-id="dd88d-156">请确保看到不同的图像用于不同的选择。</span><span class="sxs-lookup"><span data-stu-id="dd88d-156">Make sure that you see different images for different choices.</span></span>

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a><span data-ttu-id="dd88d-157">上传图像</span><span class="sxs-lookup"><span data-stu-id="dd88d-157">Uploading an Image</span></span>

<span data-ttu-id="dd88d-158">前面的示例演示了如何动态显示图像，但它仅适用于已在网站上的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-158">The previous example showed you how to display an image dynamically, but it worked only with images that were already on your website.</span></span> <span data-ttu-id="dd88d-159">此过程说明如何让用户上传图像，然后在页面上显示图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-159">This procedure shows how to let users upload an image, which is then displayed on the page.</span></span> <span data-ttu-id="dd88d-160">在 ASP.NET 中，可以使用 `WebImage` 帮助程序动态地处理图像，其中包含可用于创建、操作和保存图像的方法。</span><span class="sxs-lookup"><span data-stu-id="dd88d-160">In ASP.NET, you can manipulate images on the fly using the `WebImage` helper, which has methods that let you create, manipulate, and save images.</span></span> <span data-ttu-id="dd88d-161">`WebImage` 帮助程序支持所有常见的 web 图像文件类型，包括 *.jpg*、 *.png*和 *.bmp*。</span><span class="sxs-lookup"><span data-stu-id="dd88d-161">The `WebImage` helper supports all the common web image file types, including *.jpg*, *.png*, and *.bmp*.</span></span> <span data-ttu-id="dd88d-162">在本文中，你将使用 *.jpg*映像，但你可以使用任何图像类型。</span><span class="sxs-lookup"><span data-stu-id="dd88d-162">Throughout this article, you'll use *.jpg* images, but you can use any of the image types.</span></span>

<span data-ttu-id="dd88d-163">![影像](9-working-with-images/_static/image2.jpg "ch9images-2")</span><span class="sxs-lookup"><span data-stu-id="dd88d-163">![[image]](9-working-with-images/_static/image2.jpg "ch9images-2.jpg")</span></span>

1. <span data-ttu-id="dd88d-164">添加新页面，并将其命名为*UploadImage*。</span><span class="sxs-lookup"><span data-stu-id="dd88d-164">Add a new page and name it *UploadImage.cshtml*.</span></span>
2. <span data-ttu-id="dd88d-165">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-165">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    <span data-ttu-id="dd88d-166">文本正文具有 `<input type="file">` 元素，此元素允许用户选择要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="dd88d-166">The body of the text has an `<input type="file">` element, which lets users select a file to upload.</span></span> <span data-ttu-id="dd88d-167">当他们单击 "**提交**" 时，将连同窗体一起提交他们选取的文件。</span><span class="sxs-lookup"><span data-stu-id="dd88d-167">When they click **Submit**, the file they picked is submitted along with the form.</span></span>

    <span data-ttu-id="dd88d-168">若要获取上传的图像，请使用 `WebImage` 帮助器，其中包含用于处理图像的各种有用方法。</span><span class="sxs-lookup"><span data-stu-id="dd88d-168">To get the uploaded image, you use the `WebImage` helper, which has all sorts of useful methods for working with images.</span></span> <span data-ttu-id="dd88d-169">具体而言，使用 `WebImage.GetImageFromRequest` 获取上传的图像（如果有），并将其存储在名为 `photo`的变量中。</span><span class="sxs-lookup"><span data-stu-id="dd88d-169">Specifically, you use `WebImage.GetImageFromRequest` to get the uploaded image (if any) and store it in a variable named `photo`.</span></span>

    <span data-ttu-id="dd88d-170">本示例中的很多工作都涉及获取和设置文件和路径名称。</span><span class="sxs-lookup"><span data-stu-id="dd88d-170">A lot of the work in this example involves getting and setting file and path names.</span></span> <span data-ttu-id="dd88d-171">问题在于，你需要获取用户上传的映像的名称（和名称），然后创建新的路径用于存储该图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-171">The issue is that you want to get the name (and just the name) of the image that the user uploaded, and then create a new path for where you're going to store the image.</span></span> <span data-ttu-id="dd88d-172">由于用户可能会上传具有相同名称的多个映像，因此您需要使用一些额外的代码来创建唯一名称，并确保用户不会覆盖现有图片。</span><span class="sxs-lookup"><span data-stu-id="dd88d-172">Because users could potentially upload multiple images that have the same name, you use a bit of extra code to create unique names and make sure that users don't overwrite existing pictures.</span></span>

    <span data-ttu-id="dd88d-173">如果实际已上传图像（测试 `if (photo != null)`），则将从图像的 `FileName` 属性中获取映像名称。</span><span class="sxs-lookup"><span data-stu-id="dd88d-173">If an image actually has been uploaded (the test `if (photo != null)`), you get the image name from the image's `FileName` property.</span></span> <span data-ttu-id="dd88d-174">用户上传图像时，`FileName` 包含用户的原始名称，其中包括用户计算机的路径。</span><span class="sxs-lookup"><span data-stu-id="dd88d-174">When the user uploads the image, `FileName` contains the user's original name, which includes the path from the user's computer.</span></span> <span data-ttu-id="dd88d-175">它可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd88d-175">It might look like this:</span></span>

    <span data-ttu-id="dd88d-176">*C:\Users\Joe\Pictures\SamplePhoto1.jpg*</span><span class="sxs-lookup"><span data-stu-id="dd88d-176">*C:\Users\Joe\Pictures\SamplePhoto1.jpg*</span></span>

    <span data-ttu-id="dd88d-177">如果只是想要文件名（*SamplePhoto1*） &#8212; ，则不需要所有该路径信息。</span><span class="sxs-lookup"><span data-stu-id="dd88d-177">You don't want all that path information, though &#8212; you just want the actual file name (*SamplePhoto1.jpg*).</span></span> <span data-ttu-id="dd88d-178">可以通过使用 `Path.GetFileName` 方法仅去除路径中的文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd88d-178">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    <span data-ttu-id="dd88d-179">然后，通过将 GUID 添加到原始名称来创建新的唯一文件名。</span><span class="sxs-lookup"><span data-stu-id="dd88d-179">You then create a new unique file name by adding a GUID to the original name.</span></span> <span data-ttu-id="dd88d-180">（有关 Guid 的详细信息，请参阅本文后面的[关于 guid](#SB_AboutGUIDs) 。）然后，构造可用于保存映像的完整路径。</span><span class="sxs-lookup"><span data-stu-id="dd88d-180">(For more about GUIDs, see [About GUIDs](#SB_AboutGUIDs) later in this article.) Then you construct a complete path that you can use to save the image.</span></span> <span data-ttu-id="dd88d-181">保存路径由新文件名、文件夹（映像）和当前网站位置组成。</span><span class="sxs-lookup"><span data-stu-id="dd88d-181">The save path is made up of the new file name, the folder (images), and the current website location.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd88d-182">为了使代码能够将文件保存到*images*文件夹中，应用程序需要对该文件夹具有读写权限。</span><span class="sxs-lookup"><span data-stu-id="dd88d-182">In order for your code to save files in the *images* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="dd88d-183">在您的开发计算机上，这通常不是问题。</span><span class="sxs-lookup"><span data-stu-id="dd88d-183">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="dd88d-184">但是，当你将网站发布到宿主提供程序的 web 服务器时，可能需要显式设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="dd88d-184">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="dd88d-185">如果在宿主提供程序的服务器上运行此代码并收到错误，请与宿主提供程序联系，以了解如何设置这些权限。</span><span class="sxs-lookup"><span data-stu-id="dd88d-185">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

    <span data-ttu-id="dd88d-186">最后，将保存路径传递到 `WebImage` 帮助程序的 `Save` 方法。</span><span class="sxs-lookup"><span data-stu-id="dd88d-186">Finally, you pass the save path to the `Save` method of the `WebImage` helper.</span></span> <span data-ttu-id="dd88d-187">这会在其新名称下存储已上传的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-187">This stores the uploaded image under its new name.</span></span> <span data-ttu-id="dd88d-188">Save 方法如下所示： `photo.Save(@"~\" + imagePath)`。</span><span class="sxs-lookup"><span data-stu-id="dd88d-188">The save method looks like this: `photo.Save(@"~\" + imagePath)`.</span></span> <span data-ttu-id="dd88d-189">完整路径将追加到 `@"~\"`，这是当前网站位置。</span><span class="sxs-lookup"><span data-stu-id="dd88d-189">The complete path is appended to `@"~\"`, which is the current website location.</span></span> <span data-ttu-id="dd88d-190">（有关 `~` 运算符的信息，请参阅[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths)。）</span><span class="sxs-lookup"><span data-stu-id="dd88d-190">(For information about the `~` operator, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="dd88d-191">如前面的示例所示，页面的正文包含用于显示图像的 `<img>` 元素。</span><span class="sxs-lookup"><span data-stu-id="dd88d-191">As in the previous example, the body of the page contains an `<img>` element to display the image.</span></span> <span data-ttu-id="dd88d-192">如果已设置 `imagePath`，则呈现 `<img>` 元素，并将其 `src` 特性设置为 `imagePath` 值。</span><span class="sxs-lookup"><span data-stu-id="dd88d-192">If `imagePath` has been set, the `<img>` element is rendered and its `src` attribute is set to the `imagePath` value.</span></span>
3. <span data-ttu-id="dd88d-193">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="dd88d-193">Run the page in a browser.</span></span>
4. <span data-ttu-id="dd88d-194">上载图像并确保它显示在页面中。</span><span class="sxs-lookup"><span data-stu-id="dd88d-194">Upload an image and make sure it's displayed in the page.</span></span>
5. <span data-ttu-id="dd88d-195">在站点中，打开 "*图像*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd88d-195">In your site, open the *images* folder.</span></span> <span data-ttu-id="dd88d-196">你会看到已添加的文件的文件名如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd88d-196">You see that a new file has been added whose file name looks something like this::</span></span> 

    <span data-ttu-id="dd88d-197">*45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto*</span><span class="sxs-lookup"><span data-stu-id="dd88d-197">*45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*</span></span>

    <span data-ttu-id="dd88d-198">这是你上传的映像，其 GUID 带有名称前缀。</span><span class="sxs-lookup"><span data-stu-id="dd88d-198">This is the image that you uploaded with a GUID prefixed to the name.</span></span> <span data-ttu-id="dd88d-199">（你自己的文件将具有不同的 GUID，并且可能命名为与*MyPhoto*不同的内容。）</span><span class="sxs-lookup"><span data-stu-id="dd88d-199">(Your own file will have a different GUID and probably is named something different than *MyPhoto.png*.)</span></span>

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a><span data-ttu-id="dd88d-200">关于 Guid</span><span class="sxs-lookup"><span data-stu-id="dd88d-200">About GUIDs</span></span>
> 
> <span data-ttu-id="dd88d-201">GUID （全局唯一 ID）是通常用如下格式呈现的标识符： `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`。</span><span class="sxs-lookup"><span data-stu-id="dd88d-201">A GUID (globally-unique ID) is an identifier that's usually rendered in a format like this: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`.</span></span> <span data-ttu-id="dd88d-202">每个 GUID 的数字和字母（从-F）都不同，但它们都遵循8-4-4-4-12 个字符组的模式。</span><span class="sxs-lookup"><span data-stu-id="dd88d-202">The numbers and letters (from A-F) differ for each GUID, but they all follow the pattern of using groups of 8-4-4-4-12 characters.</span></span> <span data-ttu-id="dd88d-203">（从技术上讲，GUID 是16字节/128 位数字。）需要 GUID 时，可以调用为你生成 GUID 的专用代码。</span><span class="sxs-lookup"><span data-stu-id="dd88d-203">(Technically, a GUID is a 16-byte/128-bit number.) When you need a GUID, you can call specialized code that generates a GUID for you.</span></span> <span data-ttu-id="dd88d-204">Guid 后面的理念是：数字的巨大大小（3.4 x 10<sup>38</sup>）和生成它的算法之间的理念，最终保证的数值是一种类型。</span><span class="sxs-lookup"><span data-stu-id="dd88d-204">The idea behind GUIDs is that between the enormous size of the number (3.4 x 10<sup>38</sup>) and the algorithm for generating it, the resulting number is virtually guaranteed to be one of a kind.</span></span> <span data-ttu-id="dd88d-205">因此，Guid 是在必须确保不会两次使用同一名称时生成项名称的好方法。</span><span class="sxs-lookup"><span data-stu-id="dd88d-205">GUIDs therefore are a good way to generate names for things when you must guarantee that you won't use the same name twice.</span></span> <span data-ttu-id="dd88d-206">当然，缺点是 Guid 并不是用户友好的，因此，当名称仅用于代码中时，通常会使用 Guid。</span><span class="sxs-lookup"><span data-stu-id="dd88d-206">The downside, of course, is that GUIDs aren't particularly user friendly, so they tend to be used when the name is used only in code.</span></span>

<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a><span data-ttu-id="dd88d-207">调整图像的大小</span><span class="sxs-lookup"><span data-stu-id="dd88d-207">Resizing an Image</span></span>

<span data-ttu-id="dd88d-208">如果你的网站接受来自用户的图像，你可能希望在显示或保存之前调整图像大小。</span><span class="sxs-lookup"><span data-stu-id="dd88d-208">If your website accepts images from a user, you might want to resize the images before you display or save them.</span></span> <span data-ttu-id="dd88d-209">对于此，你可以再次使用 `WebImage` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="dd88d-209">You can again use the `WebImage` helper for this.</span></span>

<span data-ttu-id="dd88d-210">此过程演示如何调整已上传图像的大小以创建缩略图，然后在网站中保存缩略图和原始图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-210">This procedure shows how to resize an uploaded image to create a thumbnail and then save the thumbnail and original image in the website.</span></span> <span data-ttu-id="dd88d-211">在页面上显示缩略图，并使用超链接将用户重定向到完整大小的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-211">You display the thumbnail on the page and use a hyperlink to redirect users to the full-sized image.</span></span>

<span data-ttu-id="dd88d-212">![影像](9-working-with-images/_static/image3.jpg "ch9images-3")</span><span class="sxs-lookup"><span data-stu-id="dd88d-212">![[image]](9-working-with-images/_static/image3.jpg "ch9images-3.jpg")</span></span>

1. <span data-ttu-id="dd88d-213">添加一个名为*缩略图*的新页。</span><span class="sxs-lookup"><span data-stu-id="dd88d-213">Add a new page named *Thumbnail.cshtml*.</span></span>
2. <span data-ttu-id="dd88d-214">在*images*文件夹中，创建一个名为 "*大拇指*" 的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd88d-214">In the *images* folder, create a subfolder named *thumbs*.</span></span>
3. <span data-ttu-id="dd88d-215">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-215">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    <span data-ttu-id="dd88d-216">此代码类似于上一示例中的代码。</span><span class="sxs-lookup"><span data-stu-id="dd88d-216">This code is similar to the code from the previous example.</span></span> <span data-ttu-id="dd88d-217">区别在于，此代码将两次保存图像两次，一次是在创建映像的缩略图副本后进行。</span><span class="sxs-lookup"><span data-stu-id="dd88d-217">The difference is that this code saves the image twice, once normally and once after you create a thumbnail copy of the image.</span></span> <span data-ttu-id="dd88d-218">首先获取上传的图像，并将其保存到*images*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dd88d-218">First you get the uploaded image and save it in the *images* folder.</span></span> <span data-ttu-id="dd88d-219">然后为缩略图构造一个新路径。</span><span class="sxs-lookup"><span data-stu-id="dd88d-219">You then construct a new path for the thumbnail image.</span></span> <span data-ttu-id="dd88d-220">若要实际创建缩略图，请调用 `WebImage` 帮助器的 `Resize` 方法来创建 60 x 60 像素的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-220">To actually create the thumbnail, you call the `WebImage` helper's `Resize` method to create a 60-pixel by 60-pixel image.</span></span> <span data-ttu-id="dd88d-221">该示例演示了如何保持纵横比，以及如何防止放大图像（以防新大小实际使图像变大）。</span><span class="sxs-lookup"><span data-stu-id="dd88d-221">The example shows how you preserve the aspect ratio and how you can prevent the image from being enlarged (in case the new size would actually make the image larger).</span></span> <span data-ttu-id="dd88d-222">调整后的图像将保存在*拇指*子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dd88d-222">The resized image is then saved in the *thumbs* subfolder.</span></span>

    <span data-ttu-id="dd88d-223">在标记的末尾，使用与在前面的示例中看到的动态 `src` 特性相同的 `<img>` 元素，以有条件地显示图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-223">At the end of the markup, you use the same `<img>` element with the dynamic `src` attribute that you've seen in the previous examples to conditionally show the image.</span></span> <span data-ttu-id="dd88d-224">在这种情况下，会显示缩略图。</span><span class="sxs-lookup"><span data-stu-id="dd88d-224">In this case, you display the thumbnail.</span></span> <span data-ttu-id="dd88d-225">你还可以使用 `<a>` 元素创建指向图像的大版本的超链接。</span><span class="sxs-lookup"><span data-stu-id="dd88d-225">You also use an `<a>` element to create a hyperlink to the big version of the image.</span></span> <span data-ttu-id="dd88d-226">与 `<img>` 元素的 `src` 特性一样，可将 `<a>` 元素的 `href` 特性动态地设置为 `imagePath`中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="dd88d-226">As with the `src` attribute of the `<img>` element, you set the `href` attribute of the `<a>` element dynamically to whatever is in `imagePath`.</span></span> <span data-ttu-id="dd88d-227">若要确保路径可以作为 URL，请将 `imagePath` 传递到 `Html.AttributeEncode` 方法，该方法将路径中的保留字符转换为 URL 中的 ok 字符。</span><span class="sxs-lookup"><span data-stu-id="dd88d-227">To make sure that the path can work as a URL, you pass `imagePath` to the `Html.AttributeEncode` method, which converts reserved characters in the path to characters that are ok in a URL.</span></span>
4. <span data-ttu-id="dd88d-228">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="dd88d-228">Run the page in a browser.</span></span>
5. <span data-ttu-id="dd88d-229">上传照片并验证是否显示缩略图。</span><span class="sxs-lookup"><span data-stu-id="dd88d-229">Upload a photo and verify that the thumbnail is shown.</span></span>
6. <span data-ttu-id="dd88d-230">单击缩略图以查看完全大小的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-230">Click the thumbnail to see the full-size image.</span></span>
7. <span data-ttu-id="dd88d-231">请注意，在*图像*和*图像/拇指*中添加了新的文件。</span><span class="sxs-lookup"><span data-stu-id="dd88d-231">In the *images* and *images/thumbs*, note that new files have been added.</span></span>

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a><span data-ttu-id="dd88d-232">旋转和翻转图像</span><span class="sxs-lookup"><span data-stu-id="dd88d-232">Rotating and Flipping an Image</span></span>

<span data-ttu-id="dd88d-233">`WebImage` 帮助程序还允许您翻转和旋转图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-233">The `WebImage` helper also lets you flip and rotate images.</span></span> <span data-ttu-id="dd88d-234">此过程演示如何从服务器中获取图像，将图像上下翻转（垂直），保存图像，然后在页面上显示翻转后的图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-234">This procedure shows how to get an image from the server, flip the image upside down (vertically), save it, and then display the flipped image on the page.</span></span> <span data-ttu-id="dd88d-235">在此示例中，你只是在服务器上使用已有的文件（*Photo2*）。</span><span class="sxs-lookup"><span data-stu-id="dd88d-235">In this example, you're just using a file you already have on the server (*Photo2.jpg*).</span></span> <span data-ttu-id="dd88d-236">在实际应用程序中，您可能会反向使用您动态获取的图像，就像在前面的示例中一样。</span><span class="sxs-lookup"><span data-stu-id="dd88d-236">In a real application, you'd probably flip an image whose name you get dynamically, like you did in previous examples.</span></span>

<span data-ttu-id="dd88d-237">![影像](9-working-with-images/_static/image4.jpg "ch9images-4")</span><span class="sxs-lookup"><span data-stu-id="dd88d-237">![[image]](9-working-with-images/_static/image4.jpg "ch9images-4.jpg")</span></span>

1. <span data-ttu-id="dd88d-238">添加一个名为*FlipImage*的新页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-238">Add a new page named *FlipImage.cshtml*.</span></span>
2. <span data-ttu-id="dd88d-239">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-239">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    <span data-ttu-id="dd88d-240">代码使用 `WebImage` 帮助程序从服务器获取图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-240">The code uses the `WebImage` helper to get an image from the server.</span></span> <span data-ttu-id="dd88d-241">使用在前面的示例中使用的相同技术创建映像的路径，并在使用 `WebImage`创建映像时传递该路径：</span><span class="sxs-lookup"><span data-stu-id="dd88d-241">You create the path to the image using the same technique you used in earlier examples for saving images, and you pass that path when you create an image using `WebImage`:</span></span>

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    <span data-ttu-id="dd88d-242">如果找到图像，则构造新的路径和文件名，就像在前面的示例中所做的那样。</span><span class="sxs-lookup"><span data-stu-id="dd88d-242">If an image is found, you construct a new path and file name, like you did in earlier examples.</span></span> <span data-ttu-id="dd88d-243">若要翻转图像，请调用 `FlipVertical` 方法，然后重新保存该图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-243">To flip the image, you call the `FlipVertical` method, and then you save the image again.</span></span>

    <span data-ttu-id="dd88d-244">通过使用 `src` 属性设置为 "`imagePath`" 的 `<img>` 元素，再次在页面上显示图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-244">The image is again displayed on the page by using the `<img>` element with the `src` attribute set to `imagePath`.</span></span>
3. <span data-ttu-id="dd88d-245">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="dd88d-245">Run the page in a browser.</span></span> <span data-ttu-id="dd88d-246">*Photo2*的图像倒置显示。</span><span class="sxs-lookup"><span data-stu-id="dd88d-246">The image for *Photo2.jpg* is shown upside down.</span></span>
4. <span data-ttu-id="dd88d-247">刷新页面或再次请求页面，以查看图像是否再次翻转。</span><span class="sxs-lookup"><span data-stu-id="dd88d-247">Refresh the page or request the page again to see the image is flipped right side up again.</span></span>

<span data-ttu-id="dd88d-248">若要旋转图像，请使用相同的代码，不同之处在于，您可以调用 `RotateLeft` 或 `RotateRight`，而不是调用 `FlipVertical` 或 `FlipHorizontal`。</span><span class="sxs-lookup"><span data-stu-id="dd88d-248">To rotate an image, you use the same code, except that instead of calling the `FlipVertical` or `FlipHorizontal`, you call `RotateLeft` or `RotateRight`.</span></span>

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a><span data-ttu-id="dd88d-249">向图像添加水印</span><span class="sxs-lookup"><span data-stu-id="dd88d-249">Adding a Watermark to an Image</span></span>

<span data-ttu-id="dd88d-250">将图像添加到网站时，可能需要在保存图像之前向其添加水印，或将其显示在页面上。</span><span class="sxs-lookup"><span data-stu-id="dd88d-250">When you add images to your website, you might want to add a watermark to the image before you save it or display it on a page.</span></span> <span data-ttu-id="dd88d-251">用户经常使用水印将版权信息添加到图像或公布其业务名称。</span><span class="sxs-lookup"><span data-stu-id="dd88d-251">People often use watermarks to add copyright information to an image or to advertise their business name.</span></span>

<span data-ttu-id="dd88d-252">![影像](9-working-with-images/_static/image5.jpg "ch9images-5")</span><span class="sxs-lookup"><span data-stu-id="dd88d-252">![[image]](9-working-with-images/_static/image5.jpg "ch9images-5.jpg")</span></span>

1. <span data-ttu-id="dd88d-253">添加一个名为 "*水印*" 的新页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-253">Add a new page named *Watermark.cshtml*.</span></span>
2. <span data-ttu-id="dd88d-254">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-254">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    <span data-ttu-id="dd88d-255">此代码类似于前面的*FlipImage*页中的代码（尽管这次使用*Photo3*文件）。</span><span class="sxs-lookup"><span data-stu-id="dd88d-255">This code is like the code in the *FlipImage.cshtml* page from earlier (although this time it uses the *Photo3.jpg* file).</span></span> <span data-ttu-id="dd88d-256">若要添加水印，请在保存图像之前调用 `WebImage` 帮助器的 `AddTextWatermark` 方法。</span><span class="sxs-lookup"><span data-stu-id="dd88d-256">To add the watermark, you call the `WebImage` helper's `AddTextWatermark` method before you save the image.</span></span> <span data-ttu-id="dd88d-257">在对 `AddTextWatermark`的调用中，传递文本 &quot;水印&quot;，将字体颜色设置为黄色，并将字体系列设置为 Arial。</span><span class="sxs-lookup"><span data-stu-id="dd88d-257">In the call to `AddTextWatermark`, you pass the text &quot;My Watermark&quot;, set the font color to yellow, and set the font family to Arial.</span></span> <span data-ttu-id="dd88d-258">（尽管此处未显示，但 `WebImage` 帮助器还允许您指定不透明度、字体系列和字号以及水印文本的位置。）保存该映像时，它不能是只读的。</span><span class="sxs-lookup"><span data-stu-id="dd88d-258">(Although it's not shown here, the `WebImage` helper also lets you specify opacity, font family and font size, and the position of the watermark text.) When you save the image it must not be read-only.</span></span>

    <span data-ttu-id="dd88d-259">正如你之前所见，该图像将通过使用 `<img>` 元素显示在页面上，该元素的 src 属性设置为 `@imagePath`。</span><span class="sxs-lookup"><span data-stu-id="dd88d-259">As you've seen before, the image is displayed on the page by using the `<img>` element with the src attribute set to `@imagePath`.</span></span>
3. <span data-ttu-id="dd88d-260">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="dd88d-260">Run the page in a browser.</span></span> <span data-ttu-id="dd88d-261">请注意图像右下角的文本 "My 水印"。</span><span class="sxs-lookup"><span data-stu-id="dd88d-261">Notice the text "My Watermark" at the bottom-right corner of the image.</span></span>

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a><span data-ttu-id="dd88d-262">使用图像作为水印</span><span class="sxs-lookup"><span data-stu-id="dd88d-262">Using an Image As a Watermark</span></span>

<span data-ttu-id="dd88d-263">您可以使用另一个图像，而不是使用水印文本。</span><span class="sxs-lookup"><span data-stu-id="dd88d-263">Instead of using text for a watermark, you can use another image.</span></span> <span data-ttu-id="dd88d-264">用户有时使用公司徽标之类的图像作为水印，或使用水印图像而不是文本来提供版权信息。</span><span class="sxs-lookup"><span data-stu-id="dd88d-264">People sometimes use images like a company logo as a watermark, or they use a watermark image instead of text for copyright information.</span></span>

<span data-ttu-id="dd88d-265">![影像](9-working-with-images/_static/image6.jpg "ch9images-6")</span><span class="sxs-lookup"><span data-stu-id="dd88d-265">![[image]](9-working-with-images/_static/image6.jpg "ch9images-6.jpg")</span></span>

1. <span data-ttu-id="dd88d-266">添加一个名为*ImageWatermark*的新页面。</span><span class="sxs-lookup"><span data-stu-id="dd88d-266">Add a new page named *ImageWatermark.cshtml*.</span></span>
2. <span data-ttu-id="dd88d-267">将图像添加到可用作徽标的*images*文件夹中，并将图像重命名为*MyCompanyLogo*。</span><span class="sxs-lookup"><span data-stu-id="dd88d-267">Add an image to the *images* folder that you can use as a logo, and rename the image *MyCompanyLogo.jpg*.</span></span> <span data-ttu-id="dd88d-268">此图像应该是一个图像，在将其设置为80像素宽和20像素高时，可以清楚地看到该图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-268">This image should be an image that you can see clearly when it's set to 80 pixels wide and 20 pixels high.</span></span>
3. <span data-ttu-id="dd88d-269">将页面中的现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="dd88d-269">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    <span data-ttu-id="dd88d-270">这是前面示例中代码的另一种变化形式。</span><span class="sxs-lookup"><span data-stu-id="dd88d-270">This is another variation on the code from earlier examples.</span></span> <span data-ttu-id="dd88d-271">在这种情况下，在保存图像之前，调用 `AddImageWatermark` 向目标图像（*Photo3*）添加水印图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-271">In this case, you call `AddImageWatermark` to add the watermark image to the target image (*Photo3.jpg*) before you save the image.</span></span> <span data-ttu-id="dd88d-272">调用 `AddImageWatermark`时，可以将其宽度设置为80像素，将高度设置为20像素。</span><span class="sxs-lookup"><span data-stu-id="dd88d-272">When you call `AddImageWatermark`, you set its width to 80 pixels and the height to 20 pixels.</span></span> <span data-ttu-id="dd88d-273">*MyCompanyLogo*图像在水平方向上居中对齐，并在目标图像的底部垂直对齐。</span><span class="sxs-lookup"><span data-stu-id="dd88d-273">The *MyCompanyLogo.jpg* image is horizontally aligned in the center and vertically aligned at the bottom of the target image.</span></span> <span data-ttu-id="dd88d-274">不透明度设置为100%，边距设置为10像素。</span><span class="sxs-lookup"><span data-stu-id="dd88d-274">The opacity is set to 100% and the padding is set to 10 pixels.</span></span> <span data-ttu-id="dd88d-275">如果水印图像大于目标图像，则不会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="dd88d-275">If the watermark image is bigger than the target image, nothing will happen.</span></span> <span data-ttu-id="dd88d-276">如果水印图像大于目标图像，并将图像水印的填充设置为零，则忽略水印。</span><span class="sxs-lookup"><span data-stu-id="dd88d-276">If the watermark image is bigger than the target image and you set the padding for the image watermark to zero, the watermark is ignored.</span></span>

    <span data-ttu-id="dd88d-277">与前面一样，使用 `<img>` 元素和动态 `src` 特性显示图像。</span><span class="sxs-lookup"><span data-stu-id="dd88d-277">As before, you display the image using the `<img>` element and a dynamic `src` attribute.</span></span>
4. <span data-ttu-id="dd88d-278">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="dd88d-278">Run the page in a browser.</span></span> <span data-ttu-id="dd88d-279">请注意，水印图像显示在主图像底部。</span><span class="sxs-lookup"><span data-stu-id="dd88d-279">Notice that the watermark image appears at the bottom of the main image.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="dd88d-280">其他资源</span><span class="sxs-lookup"><span data-stu-id="dd88d-280">Additional Resources</span></span>

[<span data-ttu-id="dd88d-281">使用 ASP.NET 网页站点中的文件</span><span class="sxs-lookup"><span data-stu-id="dd88d-281">Working with Files in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202896)

[<span data-ttu-id="dd88d-282">使用 Razor 语法 ASP.NET 网页编程简介</span><span class="sxs-lookup"><span data-stu-id="dd88d-282">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
