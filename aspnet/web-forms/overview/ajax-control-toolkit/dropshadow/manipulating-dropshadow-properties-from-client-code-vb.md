---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 从客户端代码操作 DropShadow 属性（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 此外，还可以使用客户端 Javascript 更改此扩展器的属性。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497408"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a>通过客户端代码操作 DropShadow 属性 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 此外，还可以使用客户端 JavaScript 代码更改此扩展器的属性。

## <a name="overview"></a>概述

AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 此外，还可以使用客户端 JavaScript 代码更改此扩展器的属性。

## <a name="steps"></a>步骤

代码以包含某些文本行的面板开头：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

关联的 CSS 类为面板提供漂亮的背景色：

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

添加了 `DropShadowExtender` 以将面板扩展到投影效果，不透明度设置为50%：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

然后，ASP.NET AJAX `ScriptManager` 控件使控件工具包可以正常工作：

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

另一个面板包含两个用于设置投影不透明度的 JavaScript 链接：减号链接将减小阴影的不透明度，并将其增大。

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

然后，JavaScript 函数 `changeOpacity()` 必须首先在页面上查找 `DropShadowExtender` 控件。 ASP.NET AJAX 只为该任务定义 `$find()` 方法。 然后，`get_Opacity()` 方法检索当前不透明度，`set_Opacity()` 方法将设置它。 然后，JavaScript 代码将当前的 opacity 值放在 `<label>` 元素中：

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

在客户端上更改不透明度（[单击以查看完全大小的映像](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](adjusting-the-z-index-of-a-dropshadow-vb.md)
