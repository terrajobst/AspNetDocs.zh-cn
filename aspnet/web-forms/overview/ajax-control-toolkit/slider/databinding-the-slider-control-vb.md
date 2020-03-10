---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 数据绑定滑块控件（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以绑定当前的 positio 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508898"
---
# <a name="databinding-the-slider-control-vb"></a>数据绑定滑块控件 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以将滑块的当前位置绑定到另一个 ASP.NET 控件。

## <a name="overview"></a>概述

AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以将滑块的当前位置绑定到另一个 ASP.NET 控件。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

接下来，向页面添加两个 `TextBox` 控件。 一个将转换为图形滑块，另一个将保存滑块的位置。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

下一步已经是最后一步。 ASP.NET AJAX 控件工具包中的 `SliderExtender` 控件将从第一个文本框中创建一个滑块，并在滑块位置改变时自动更新第二个文本框。 为了使其正常工作，必须将 `SliderExtender`的 `TargetControlID` 属性设置为第一个文本框的 ID;`BoundControlID` 特性必须设置为第二个文本框的 ID。

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

正如您在浏览器中所看到的那样，数据绑定在这两个方向上都是这样的：在文本框中输入新值可更新滑块的位置。 如果将第二个文本框设置为只读，则可以向文本字段添加弱保护，使用户更难手动更新其中的值。

[![滑块和文本框处于同步](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

滑块和文本框处于同步（[单击以查看完全大小的图像](databinding-the-slider-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](using-the-slider-control-with-auto-postback-vb.md)
