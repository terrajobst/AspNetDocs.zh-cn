---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 在 ASP.NET 网页（Razor）站点中显示视频 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何使用 Razor 语法页面在 ASP.NET 网页中显示视频。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510380"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET 网页（Razor）站点中显示视频

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中使用视频（媒体）播放器，使用户能够查看存储在网站上的视频。 利用 Razor 语法 ASP.NET 网页，可以播放 Flash （*swf*）、Media Player （ *.Wmv*）和 Silverlight （ *.xap*）视频。
> 
> 学习内容：
> 
> - 如何选择视频播放器。
> - 如何将视频添加到网页。
> - 如何设置视频播放器属性。
> 
> 下面是本文中介绍的 ASP.NET Razor 页面功能：
> 
> - `Video` 帮助程序。
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

## <a name="introduction"></a>简介

你可能想要在你的站点上显示视频。 实现此目的的一种方法是链接到已包含视频的站点，例如 YouTube。 如果要在自己的页面中直接嵌入来自这些网站的视频，通常可以从网站获取 HTML 标记，然后将其复制到页面中。 例如，以下示例演示了如何嵌入 YouTube 视频：

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

如果你想要播放位于你自己的网站上的视频（而不是在公共视频共享网站上），则不能使用此类嵌入的标记直接链接到它。 不过，你可以使用 `Video` 帮助程序播放来自你的网站的视频，这会直接在页面中呈现媒体播放器。

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>选择视频播放器

视频文件有很多格式，每种格式通常都需要使用不同的播放机和不同的方式来配置播放机。 在 ASP.NET Razor 页面中，可以使用 `Video` 帮助程序在网页上播放视频。 `Video` helper 简化了在网页中嵌入视频的过程，因为它会自动生成 `object`，并 `embed` 通常用于向页面添加视频的 HTML 元素。

`Video` 帮助程序支持以下媒体播放器：

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Flash Player

使用 `Video` 帮助器的 `Flash` 播放器，可以在网页中播放 Flash 视频（*swf*文件）。 至少必须提供视频文件的路径。 如果不指定路径，播放机将使用当前闪存版本设置的默认值。 典型的默认设置为：

- 该视频使用其默认宽度和高度显示，而不使用背景色显示。
- 加载页面时，视频会自动播放。
- 视频会一直循环，直到它被显式停止。
- 视频缩放以显示所有视频，而不是裁剪视频以适应特定大小。
- 视频在窗口中播放。

### <a name="the-mediaplayer-player"></a>MediaPlayer 播放器

使用 `Video` 帮助器的 `MediaPlayer` 播放器，可以在网页中播放 Windows Media 视频（ *.wmv*文件）、windows media 音频（*wma*文件）和 mp3 （*mp3*文件）。 必须包含要播放的媒体文件的路径;所有其他参数都是可选的。 如果仅指定路径，播放机将使用当前版本的 MediaPlayer 设置的默认设置，例如：

- 该视频使用其默认宽度和高度显示。
- 加载页面时，视频会自动播放。
- 视频播放一次（不循环）。
- 播放机在用户界面中显示完整的控件集。
- 视频在窗口中播放。

### <a name="the-silverlight-player"></a>Silverlight 播放器

`Video` 帮助器的 `Silverlight` 播放机使你可以播放 Windows Media 视频（ *.wmv*文件）、Windows Media 音频（ *.wma*文件）和 mp3 （*mp3*文件）。 必须将 path 参数设置为指向基于 Silverlight 的应用程序包（ *.xap*文件）。 还必须设置 width 和 height 参数。 其他所有参数都是可选参数。 当你使用 Silverlight 播放视频时，如果仅设置所需的参数，则 Silverlight 播放机将显示不带背景色的视频。

> [!NOTE]
> 如果你尚未知道 Silverlight： *.xap*文件是一个压缩文件，其中包含 *.xaml*文件中的布局说明、程序集中的托管代码和可选资源。 你可以在 Visual Studio 中创建一个 *.xap*文件作为 Silverlight 应用程序项目。

`Silverlight` 视频播放器使用您为播放机提供的设置和 *.xap*文件中提供的设置。

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME 类型
> 
> 当浏览器下载文件时，浏览器会确保文件类型与为正在呈现的文档指定的 MIME 类型匹配。 MIME 类型是文件的内容类型或媒体类型。 `Video` 帮助器使用以下 MIME 类型：
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>播放 Flash （swf）视频

此过程说明如何播放名为*sample*的 Flash 视频。 此过程假设你已在站点上获取一个名为 "*媒体*" 的文件夹，并且该*swf*文件位于该文件夹中。

1. 如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。
2. 在网站中，添加一个页面，并将其命名为*FlashVideo*。
3. 将以下标记添加到页面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. 在浏览器中运行页。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）页面随即显示，视频会自动播放。 

    ![影像](10-working-with-video/_static/image1.jpg "ch08_video-1")

可以将闪存视频的 `quality` 参数设置为 `low`、`autolow`、`autohigh`、`medium`、`high`和 `best`：

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

您可以使用 `scale` 参数更改 Flash 视频以特定大小播放，可以将该参数设置为以下内容：

- `showall`。 这会使整个视频可见，同时保持原始纵横比。 不过，您可能会在每一端上都有边框。
- `noorder`。 这会在保持原始纵横比的同时缩放视频，但可能会被裁剪。
- `exactfit`。 这样可以在不保留原始纵横比的情况下显示整个视频，但可能会发生失真。

如果没有指定 `scale` 参数，则整个视频将可见，并且在不进行任何裁剪的情况下将保持原始纵横比。 下面的示例演示如何使用 `scale` 参数：

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash player 支持名为 `windowMode`的视频模式设置。 可以将此设置为 `window`、`opaque`和 `transparent`。 默认情况下，`windowMode` 设置为 `window`，这会在网页的单独窗口中显示视频。 `opaque` 设置将隐藏网页上的所有内容。 "`transparent`" 设置允许网页的背景透过视频显示，假设视频的任何部分都是透明的。

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>播放 MediaPlayer （ *.wmv*）视频

以下过程说明如何播放名为*sample*的窗口媒体视频，该视频位于*media*文件夹中。

1. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
2. 创建名为*MediaPlayerVideo*的新页面。
3. 将以下标记添加到页面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. 在浏览器中运行页。 视频会自动加载和播放。 

    ![影像](10-working-with-video/_static/image2.jpg "ch08_video-2")

可以将 `playCount` 设置为一个整数，该整数指示自动播放视频的次数：

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode` 参数可用于指定在用户界面中显示的控件。 可以将 `uiMode` 设置为 `invisible`、`none`、`mini`或 `full`。 如果没有指定 `uiMode` 参数，则除了视频窗口外，视频还将显示 "状态" 窗口、"搜索栏"、"控制按钮" 和 "音量" 控件。 如果使用播放机播放音频文件，也会显示这些控件。 下面是有关如何使用 `uiMode` 参数的示例：

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

默认情况下，播放视频时音频处于打开状态。 可以通过将 `mute` 参数设置为 true 来使音频静音：

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

可以通过将 `volume` 参数设置为介于0到100之间的值来控制 MediaPlayer 视频的音频级别。 默认值为 50。 以下是一个示例：

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>播放 Silverlight 视频

此过程说明如何播放包含在名为*Media*的文件夹中的 Silverlight *.xap*页面中的视频。

1. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
2. 创建名为*SilverlightVideo*的新页面。
3. 将以下标记添加到页面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. 在浏览器中运行页。 

    ![影像](10-working-with-video/_static/image3.jpg "ch08_video-3")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[Silverlight 概述](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Flash 对象和嵌入标记属性](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 SDK 参数标记](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
