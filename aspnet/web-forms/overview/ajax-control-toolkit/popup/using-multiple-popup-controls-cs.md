---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 使用多个 Popup 控件C#（） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 还可以使用 m 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496424"
---
# <a name="using-multiple-popup-controls-c"></a>使用多个弹出控件 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)

> AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 还可以在一个页面上使用多个 popup 控件。

## <a name="overview"></a>概述

AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 还可以在一个页面上使用多个 popup 控件。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

接下来，添加一个用作弹出窗口的面板。 在当前情况下，面板包含一个 `Calendar` 控件。 为了避免由日历回发导致的页面刷新，将面板置于 `UpdatePanel` 控件中：

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

该页还包含两个文本框。 对于每个文本框，一旦激活文本框，就会显示 "日历" 弹出窗口。

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

现在，使用 `PopupControlExtender`扩展两个文本框中的每一个。 `TargetControlID` 属性提供绑定到扩展器的控件的 ID。 `PopupControlID` 属性包含弹出面板的 ID。 在这种情况下，两个扩展器都显示同一个面板，但也可能有不同的面板。

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

现在只要单击文本字段，就会在字段下方显示一个日历，使您可以选择日期。 （其他教程将介绍如何将所选日期返回到文本框中。）

[当用户单击文本框时，将显示日历 ![](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

当用户在文本框中单击时，将显示该日历（[单击以查看完全大小的图像](using-multiple-popup-controls-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一部分](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
