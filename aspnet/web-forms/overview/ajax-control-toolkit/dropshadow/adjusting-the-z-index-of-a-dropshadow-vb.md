---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: 调整 DropShadow 的 Z 索引（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 但是，这种阴影有时会与其他控件冲突，(.。。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 10495a9590ce1f25e9e3fa218ac5144268f50711
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574143"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a>调整 DropShadow 的 Z-索引 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)

> AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 但是，这种阴影有时会与其他控件（例如 ASP.NET Menu 控件）冲突。 弹出菜单项时，它显示在投影的后面。

## <a name="overview"></a>概述

AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 但是，这种阴影有时会与其他控件（例如 ASP.NET Menu 控件）冲突。 弹出菜单项时，它显示在投影的后面。

## <a name="steps"></a>步骤

该代码带有面板本身，其中包含足够的文本，以便面板包含足够文本以使效果可见：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

另一面板直接放置在 `panelShadow` 面板之前。 它包含水平方向的菜单，以便菜单项显示在 "`dropShadow`" 面板上（或相反：）：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

然后，添加 `DropShadowExtender`，以使用投影效果扩展 `panelShadow` 面板：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

最后，ASP.NET AJAX `ScriptManager` 控件使控件工具包能够正常工作：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

运行此脚本时，菜单项显示在面板的下方。 但是，菜单使用 CSS 类 `panel` 其中你只需定义两项内容即可使元素出现在另一个面板前面：

- 相对定位
- 正 z 索引

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

然后，`DropShadowExtender` 控件不会再与 Menu 控件冲突。

[![之前：菜单项不可见](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

之前：菜单项不可见（[单击查看完全大小的图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png)）

[![后：菜单项出现](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

后：菜单项出现（[单击以查看完全大小的图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png)）

> [!div class="step-by-step"]
> [上一页](manipulating-dropshadow-properties-from-client-code-cs.md)
> [下一页](manipulating-dropshadow-properties-from-client-code-vb.md)
