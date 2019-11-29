---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: 从服务器代码启动模式弹出窗口 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但某些情况下，需要
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606595"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a>通过服务器代码启动模式弹出窗口 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)

> AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但是，某些情况要求在服务器端触发模式弹出窗口的打开。

## <a name="overview"></a>概述

AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但是，某些情况要求在服务器端触发模式弹出窗口的打开。

## <a name="steps"></a>步骤

首先，需要 ASP.NET 按钮 web 控件来演示 ModalPopup 控件的工作方式。 将 &lt;窗体中的此类按钮添加到新页上&gt; 元素：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

然后，需要要创建的弹出窗口的标记。 将其定义为 `<asp:Panel>` 控件并确保它包含一个按钮控件。 ModalPopup 控件提供了使此类按钮关闭弹出窗口的功能;否则，不能轻松地使其消失。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

接下来，将 ModalPopup 控件从 ASP.NET AJAX 工具包添加到页面。 设置用于加载控件的按钮、使其消失的按钮以及实际弹出窗口的 ID 的属性。

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

与所有基于 ASP.NET AJAX 的网页一样;脚本管理器是为不同的目标浏览器加载必要的 JavaScript 库所必需的：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

在浏览器中运行该示例。 单击该按钮时，将显示模式弹出窗口。 为了使用服务器端代码实现相同的效果，需要一个新的按钮：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

如您所见，单击该按钮会生成回发，并在服务器上执行 `ServerButton_Click()` 方法。 在此方法中，称为 `launchModal()` 的 JavaScript 函数的执行方式是精确的，加载页面后将执行 JavaScript 函数：

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

`launchModal()` 的作业是显示 ModalPopup。 完成 HTML 页面加载后，将执行 `launchModal()` 函数。 但当时，ASP.NET AJAX framework 尚未完全加载。 因此，`launchModal()` 函数只是设置 ModalPopup 控件以后必须显示的变量：

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

`pageLoad()` JavaScript 函数是一种特殊函数，可在完全加载 ASP.NET AJAX 后执行。 因此，我们将代码添加到此函数以显示 ModalPopup 控件，但前提是在之前调用了 `launchModal()`：

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

`$find()` 函数正在查找页上的命名元素，并需要服务器端 ID 作为参数。 因此，`$find("mpe")` 返回 ModalPopup 控件的客户端表示形式;它的 `show()` 方法允许弹出窗口出现。

[单击任一按钮时，会显示模式弹出窗口 ![](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)

单击任一按钮时，将显示模式弹出窗口（[单击以查看完全大小的图像](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](positioning-a-modalpopup-cs.md)
> [下一页](using-modalpopup-with-a-repeater-control-vb.md)
