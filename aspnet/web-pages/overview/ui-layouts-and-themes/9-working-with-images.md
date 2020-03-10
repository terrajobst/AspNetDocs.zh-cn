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
# <a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET 网页（Razor）站点中的图像

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中添加、显示和处理图像（调整大小、翻转和添加水印）。
> 
> 学习内容：
> 
> - 如何将图像动态添加到页面。
> - 如何让用户上传图像。
> - 如何调整图像大小。
> - 如何翻转或旋转图像。
> - 如何向图像添加水印。
> - 如何使用图像作为水印。
> 
> 下面是本文中引入的 ASP.NET 编程功能：
> 
> - `WebImage` 帮助程序。
> - `Path` 对象，它提供允许操作路径和文件名的方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。

<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>动态将图像添加到网页

在开发网站的同时，您可以将图像添加到您的网站和各个页面。 你还可以让用户上传图像，这对于允许他们添加个人资料照片的任务可能很有用。

如果你的站点上已有一个映像，而你只想在页面上显示该图像，则可使用如下所示的 HTML `<img>` 元素：

[!code-html[Main](9-working-with-images/samples/sample1.html)]

但有时，您需要能够动态&#8212;显示图像，即在页面运行之前不知道要显示的图像。

本部分中的过程演示如何在用户在图像名称列表中指定图像文件名的动态位置显示图像。 它们从下拉列表中选择映像的名称，并在提交页面时显示所选图像。

![影像](9-working-with-images/_static/image1.jpg "ch9images-1")

1. 在 WebMatrix 中，创建一个新网站。
2. 添加一个名为*DynamicImage*的新页面。
3. 在网站的根文件夹中，添加一个新文件夹并将其命名为*images*。
4. 将四个图像添加到刚创建的*images*文件夹中。 （您可以方便地使用任何图像，但这些图像应该适合页面。）重命名*Photo1*、 *Photo2*、 *Photo3*和*Photo4*这一映像。 （在此过程中不使用*Photo4* ，但稍后将在本文中使用它。）
5. 验证四个图像是否未标记为只读。
6. 将页面中的现有内容替换为以下内容：

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    页面的正文包含一个名为 `photoChoice`的下拉列表（`<select>` 元素）。 此列表具有三个选项，每个列表选项的 `value` 属性都具有您在*images*文件夹中放置的某个图像的名称。 实质上，此列表使用户可以选择友好名称（如 &quot;照片 1&quot;），然后在提交页面时传递 *.jpg*文件名。

    在代码中，可以从列表中获取用户的选择（即图像文件名），方法是读取 `Request["photoChoice"]`。 首先查看是否有选择。 如果有，则为映像创建一个路径，该路径包含图像的文件夹名称和用户的图像文件名。 （如果您尝试构造一个路径，但 `Request["photoChoice"]`中没有任何内容，则会出现错误。）这将产生如下所示的相对路径：

    *images/Photo1*

    路径存储在名为 `imagePath` 的变量中，稍后会在页面中用到。

    在正文中，还有一个 `<img>` 元素，用于显示用户选择的图像。 `src` 特性未设置为文件名或 URL，就像要显示静态元素一样。 相反，它设置为 `@imagePath`，这意味着它将从您在代码中设置的路径获取其值。

    但在页面首次运行时，没有要显示的图像，因为用户未选择任何内容。 这通常意味着 `src` 特性将为空，并且图像将显示为红色的 &quot;x&quot; （或者浏览器在找不到图像时所呈现的任何内容）。 若要防止出现这种情况，请将 `<img>` 元素放在测试的 `if` 块中，以确定 `imagePath` 变量中是否有任何内容。 如果用户进行了选择，`imagePath` 包含该路径。 如果用户未选择图像，或这是第一次显示页面，则不会呈现 `<img>` 元素。
7. 保存文件并在浏览器中运行页面。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）
8. 从下拉列表中选择一个映像，然后单击 "**示例图像**"。 请确保看到不同的图像用于不同的选择。

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>上传图像

前面的示例演示了如何动态显示图像，但它仅适用于已在网站上的图像。 此过程说明如何让用户上传图像，然后在页面上显示图像。 在 ASP.NET 中，可以使用 `WebImage` 帮助程序动态地处理图像，其中包含可用于创建、操作和保存图像的方法。 `WebImage` 帮助程序支持所有常见的 web 图像文件类型，包括 *.jpg*、 *.png*和 *.bmp*。 在本文中，你将使用 *.jpg*映像，但你可以使用任何图像类型。

![影像](9-working-with-images/_static/image2.jpg "ch9images-2")

1. 添加新页面，并将其命名为*UploadImage*。
2. 将页面中的现有内容替换为以下内容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    文本正文具有 `<input type="file">` 元素，此元素允许用户选择要上载的文件。 当他们单击 "**提交**" 时，将连同窗体一起提交他们选取的文件。

    若要获取上传的图像，请使用 `WebImage` 帮助器，其中包含用于处理图像的各种有用方法。 具体而言，使用 `WebImage.GetImageFromRequest` 获取上传的图像（如果有），并将其存储在名为 `photo`的变量中。

    本示例中的很多工作都涉及获取和设置文件和路径名称。 问题在于，你需要获取用户上传的映像的名称（和名称），然后创建新的路径用于存储该图像。 由于用户可能会上传具有相同名称的多个映像，因此您需要使用一些额外的代码来创建唯一名称，并确保用户不会覆盖现有图片。

    如果实际已上传图像（测试 `if (photo != null)`），则将从图像的 `FileName` 属性中获取映像名称。 用户上传图像时，`FileName` 包含用户的原始名称，其中包括用户计算机的路径。 它可能如下所示：

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    如果只是想要文件名（*SamplePhoto1*） &#8212; ，则不需要所有该路径信息。 可以通过使用 `Path.GetFileName` 方法仅去除路径中的文件，如下所示：

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    然后，通过将 GUID 添加到原始名称来创建新的唯一文件名。 （有关 Guid 的详细信息，请参阅本文后面的[关于 guid](#SB_AboutGUIDs) 。）然后，构造可用于保存映像的完整路径。 保存路径由新文件名、文件夹（映像）和当前网站位置组成。

    > [!NOTE]
    > 为了使代码能够将文件保存到*images*文件夹中，应用程序需要对该文件夹具有读写权限。 在您的开发计算机上，这通常不是问题。 但是，当你将网站发布到宿主提供程序的 web 服务器时，可能需要显式设置这些权限。 如果在宿主提供程序的服务器上运行此代码并收到错误，请与宿主提供程序联系，以了解如何设置这些权限。

    最后，将保存路径传递到 `WebImage` 帮助程序的 `Save` 方法。 这会在其新名称下存储已上传的图像。 Save 方法如下所示： `photo.Save(@"~\" + imagePath)`。 完整路径将追加到 `@"~\"`，这是当前网站位置。 （有关 `~` 运算符的信息，请参阅[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths)。）

    如前面的示例所示，页面的正文包含用于显示图像的 `<img>` 元素。 如果已设置 `imagePath`，则呈现 `<img>` 元素，并将其 `src` 特性设置为 `imagePath` 值。
3. 在浏览器中运行页。
4. 上载图像并确保它显示在页面中。
5. 在站点中，打开 "*图像*" 文件夹。 你会看到已添加的文件的文件名如下所示： 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto*

    这是你上传的映像，其 GUID 带有名称前缀。 （你自己的文件将具有不同的 GUID，并且可能命名为与*MyPhoto*不同的内容。）

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>关于 Guid
> 
> GUID （全局唯一 ID）是通常用如下格式呈现的标识符： `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`。 每个 GUID 的数字和字母（从-F）都不同，但它们都遵循8-4-4-4-12 个字符组的模式。 （从技术上讲，GUID 是16字节/128 位数字。）需要 GUID 时，可以调用为你生成 GUID 的专用代码。 Guid 后面的理念是：数字的巨大大小（3.4 x 10<sup>38</sup>）和生成它的算法之间的理念，最终保证的数值是一种类型。 因此，Guid 是在必须确保不会两次使用同一名称时生成项名称的好方法。 当然，缺点是 Guid 并不是用户友好的，因此，当名称仅用于代码中时，通常会使用 Guid。

<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>调整图像的大小

如果你的网站接受来自用户的图像，你可能希望在显示或保存之前调整图像大小。 对于此，你可以再次使用 `WebImage` 帮助程序。

此过程演示如何调整已上传图像的大小以创建缩略图，然后在网站中保存缩略图和原始图像。 在页面上显示缩略图，并使用超链接将用户重定向到完整大小的图像。

![影像](9-working-with-images/_static/image3.jpg "ch9images-3")

1. 添加一个名为*缩略图*的新页。
2. 在*images*文件夹中，创建一个名为 "*大拇指*" 的子文件夹。
3. 将页面中的现有内容替换为以下内容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    此代码类似于上一示例中的代码。 区别在于，此代码将两次保存图像两次，一次是在创建映像的缩略图副本后进行。 首先获取上传的图像，并将其保存到*images*文件夹中。 然后为缩略图构造一个新路径。 若要实际创建缩略图，请调用 `WebImage` 帮助器的 `Resize` 方法来创建 60 x 60 像素的图像。 该示例演示了如何保持纵横比，以及如何防止放大图像（以防新大小实际使图像变大）。 调整后的图像将保存在*拇指*子文件夹中。

    在标记的末尾，使用与在前面的示例中看到的动态 `src` 特性相同的 `<img>` 元素，以有条件地显示图像。 在这种情况下，会显示缩略图。 你还可以使用 `<a>` 元素创建指向图像的大版本的超链接。 与 `<img>` 元素的 `src` 特性一样，可将 `<a>` 元素的 `href` 特性动态地设置为 `imagePath`中的任何内容。 若要确保路径可以作为 URL，请将 `imagePath` 传递到 `Html.AttributeEncode` 方法，该方法将路径中的保留字符转换为 URL 中的 ok 字符。
4. 在浏览器中运行页。
5. 上传照片并验证是否显示缩略图。
6. 单击缩略图以查看完全大小的图像。
7. 请注意，在*图像*和*图像/拇指*中添加了新的文件。

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>旋转和翻转图像

`WebImage` 帮助程序还允许您翻转和旋转图像。 此过程演示如何从服务器中获取图像，将图像上下翻转（垂直），保存图像，然后在页面上显示翻转后的图像。 在此示例中，你只是在服务器上使用已有的文件（*Photo2*）。 在实际应用程序中，您可能会反向使用您动态获取的图像，就像在前面的示例中一样。

![影像](9-working-with-images/_static/image4.jpg "ch9images-4")

1. 添加一个名为*FlipImage*的新页面。
2. 将页面中的现有内容替换为以下内容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    代码使用 `WebImage` 帮助程序从服务器获取图像。 使用在前面的示例中使用的相同技术创建映像的路径，并在使用 `WebImage`创建映像时传递该路径：

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    如果找到图像，则构造新的路径和文件名，就像在前面的示例中所做的那样。 若要翻转图像，请调用 `FlipVertical` 方法，然后重新保存该图像。

    通过使用 `src` 属性设置为 "`imagePath`" 的 `<img>` 元素，再次在页面上显示图像。
3. 在浏览器中运行页。 *Photo2*的图像倒置显示。
4. 刷新页面或再次请求页面，以查看图像是否再次翻转。

若要旋转图像，请使用相同的代码，不同之处在于，您可以调用 `RotateLeft` 或 `RotateRight`，而不是调用 `FlipVertical` 或 `FlipHorizontal`。

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>向图像添加水印

将图像添加到网站时，可能需要在保存图像之前向其添加水印，或将其显示在页面上。 用户经常使用水印将版权信息添加到图像或公布其业务名称。

![影像](9-working-with-images/_static/image5.jpg "ch9images-5")

1. 添加一个名为 "*水印*" 的新页面。
2. 将页面中的现有内容替换为以下内容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    此代码类似于前面的*FlipImage*页中的代码（尽管这次使用*Photo3*文件）。 若要添加水印，请在保存图像之前调用 `WebImage` 帮助器的 `AddTextWatermark` 方法。 在对 `AddTextWatermark`的调用中，传递文本 &quot;水印&quot;，将字体颜色设置为黄色，并将字体系列设置为 Arial。 （尽管此处未显示，但 `WebImage` 帮助器还允许您指定不透明度、字体系列和字号以及水印文本的位置。）保存该映像时，它不能是只读的。

    正如你之前所见，该图像将通过使用 `<img>` 元素显示在页面上，该元素的 src 属性设置为 `@imagePath`。
3. 在浏览器中运行页。 请注意图像右下角的文本 "My 水印"。

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>使用图像作为水印

您可以使用另一个图像，而不是使用水印文本。 用户有时使用公司徽标之类的图像作为水印，或使用水印图像而不是文本来提供版权信息。

![影像](9-working-with-images/_static/image6.jpg "ch9images-6")

1. 添加一个名为*ImageWatermark*的新页面。
2. 将图像添加到可用作徽标的*images*文件夹中，并将图像重命名为*MyCompanyLogo*。 此图像应该是一个图像，在将其设置为80像素宽和20像素高时，可以清楚地看到该图像。
3. 将页面中的现有内容替换为以下内容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    这是前面示例中代码的另一种变化形式。 在这种情况下，在保存图像之前，调用 `AddImageWatermark` 向目标图像（*Photo3*）添加水印图像。 调用 `AddImageWatermark`时，可以将其宽度设置为80像素，将高度设置为20像素。 *MyCompanyLogo*图像在水平方向上居中对齐，并在目标图像的底部垂直对齐。 不透明度设置为100%，边距设置为10像素。 如果水印图像大于目标图像，则不会执行任何操作。 如果水印图像大于目标图像，并将图像水印的填充设置为零，则忽略水印。

    与前面一样，使用 `<img>` 元素和动态 `src` 特性显示图像。
4. 在浏览器中运行页。 请注意，水印图像显示在主图像底部。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[使用 ASP.NET 网页站点中的文件](https://go.microsoft.com/fwlink/?LinkId=202896)

[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkID=251587)
