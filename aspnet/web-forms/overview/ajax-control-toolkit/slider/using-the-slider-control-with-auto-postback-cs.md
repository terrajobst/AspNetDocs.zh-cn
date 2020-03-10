---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 使用带有自动回发（C#）的滑块控件 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以使滑块 autopost 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445826"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a>使用带有自动回发的滑块控件（C#）

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)

> AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 它的值更改后，可以使滑块 autopostback。

## <a name="overview"></a>概述

AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 它的值更改后，可以使滑块 autopostback。

## <a name="steps"></a>步骤

为了使滑块在发生更改时自动回发，两个文本框都需要属性 `AutoPostBack="true"`：将成为滑块本身的文本框，以及容纳滑块位置的文本框。 下面是所需的标记：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

ASP.NET AJAX 控件工具包中的 `SliderExtender` 控件将滑块功能分配给这两个文本框：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

稍后将使用其他 label 元素向用户通知回发：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

最后，ASP.NET AJAX `ScriptManager` 控件加载所需的 JavaScript，使控件工具包工作正常：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

现在滑块将回发，在服务器端，可能会捕获并处理此事件：

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

[![移动滑块会触发回发](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

移动滑块会触发回发（[单击查看完全大小的映像](using-the-slider-control-with-auto-postback-cs/_static/image3.png)）

[![之后，此更改的日期将写入标签](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

之后，此更改的日期将写入标签（[单击查看完全大小的图像](using-the-slider-control-with-auto-postback-cs/_static/image6.png)）

> [!div class="step-by-step"]
> [下一部分](databinding-the-slider-control-cs.md)
