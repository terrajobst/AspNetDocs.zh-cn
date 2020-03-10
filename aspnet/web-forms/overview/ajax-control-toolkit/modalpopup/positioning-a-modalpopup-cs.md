---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: 定位 ModalPopup （C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但是，控件不提供 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496916"
---
# <a name="positioning-a-modalpopup-c"></a>定位 ModalPopup (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但是，控件不提供用于定位 popup 的内置功能。

## <a name="overview"></a>概述

AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但是，控件不提供用于定位 popup 的内置功能。

## <a name="steps"></a>步骤

为了激活 ASP.NET AJAX 和控件工具包的功能，`ScriptManager`。 控件必须置于页面上的任何位置（但位于 `<form>` 元素内）：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

接下来，添加一个用于模式弹出窗口的面板。 按钮用于关闭弹出窗口：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

每当显示弹出窗口时，它都应定位在页面中的某个位置。 对于此任务，将创建客户端 JavaScript 函数。 它首先尝试访问面板。 如果成功，则使用 CSS 和 JavaScript 设置面板的位置（将 popup 的位置更改为）。 但 `ModalPopupExtender` 控件也会尝试定位弹出窗口。 因此，JavaScript 代码会重复定位 popup，每10秒一次。

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

正如您所看到的，`setTimeout()` JavaScript 方法的返回值保存在全局变量中。 这允许使用 `clearTimeout()` 方法，按需停止快捷方式的重复定位：

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

现在，剩下的就是让浏览器在适当的时候调用这些函数。 当单击触发面板的按钮时，必须调用 `movePanel()` JavaScript 函数：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

当弹出窗口关闭时，`stopMoving()` 函数便会开始播放，此操作可在 `ModalPopupExtender` 控件中触发：

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

[![在指定位置显示模式弹出窗口](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

模式弹出窗口出现在指定位置（[单击以查看完全大小的图像](positioning-a-modalpopup-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](handling-postbacks-from-a-modalpopup-cs.md)
> [下一页](launching-a-modal-popup-window-from-server-code-vb.md)
