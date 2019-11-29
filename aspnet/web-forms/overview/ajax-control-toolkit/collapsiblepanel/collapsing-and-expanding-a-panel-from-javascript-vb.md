---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: 从 JavaScript 折叠和展开面板（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展了面板，使其能够折叠其内容并将其展开 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599363"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>通过 JavaScript 折叠和展开面板 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展了面板，使其能够折叠其内容并再次展开。 也可以通过自定义 JavaScript 代码触发这两个操作。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展了面板，使其能够折叠其内容并再次展开。 也可以通过自定义 JavaScript 代码触发这两个操作。

## <a name="steps"></a>步骤

首先，创建一个新的 ASP.NET 页面，并在一个 `<form>` 元素中包含 `ScriptManager`。 这会加载控件工具包所需的 ASP.NET AJAX 库：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

然后，创建一个带有一些文本的面板，以便可以查看折叠/展开效果：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

如您所见，该面板引用了此处显示的 CSS 类（基本上定义了背景颜色和面板的宽度）：

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

`CollapsiblePanelExtender` 控件需要 `TargetControlID` 属性，以便该工具包知道在请求时折叠或展开哪个面板：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

遗憾的是，扩展器当前未公开用于折叠或展开面板的特定 API，但某些未记录的方法将执行此操作。 首先，将三个 HTML 按钮添加到页面，随后会触发客户端 JavaScript 以折叠或展开面板的内容：

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

在客户端 JavaScript 代码中（从 `<script type="text/javascript">`开始），需要使用 `$find()` 方法来访问 `CollapsiblePanelExtender`。 `$find("cpe")` 将返回对它的引用。 从这里开始，特定的方法可解决现有的任务。

用于打开（展开）面板的方法称为 `_doOpen()`;下面的代码实现单击第一个按钮时调用的 `doOpen()` 函数：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

若要关闭或折叠面板，需要执行 `_doClose()` 方法。 因此，当用户单击第二个按钮时，将调用以下 JavaScript 代码：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

第三个按钮切换面板的状态：从折叠展开为展开状态，反之亦然。 `CollapsiblePanelExtender` 公开 `toggle()` 方法，该方法执行的操作完全正确：反转面板的状态。 但还有另一种方法（由 `toggle()` 方法在内部使用）： `CollapsiblePanelExtender()` 的 `get_Collapsed()` 方法告诉我们面板是否折叠。 根据此函数的返回值，将面板展开（`_doOpen()` 方法）或折叠（`_doClose()`）方法：

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[第三个按钮 ![更改面板的状态：从折叠到已展开并返回](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

第三个按钮更改面板的状态：从折叠到展开和后退（[单击以查看完全大小的图像](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一部分](collapsing-and-expanding-a-panel-from-javascript-cs.md)
