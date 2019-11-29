---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 从列表中选取一个动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 该框架还允许
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2bc203d694792716bbf4f7d7b8d152c589bf99b1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575125"
---
# <a name="picking-one-animation-out-of-a-list-c"></a>选取列表中的一个动画 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 使用该框架，程序员还可以根据某些 JavaScript 代码的评估，从动画列表中选取一种动画。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 使用该框架，程序员还可以根据某些 JavaScript 代码的评估，从动画列表中选取一种动画。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。 `<Case>` 元素会进入播放，而不是常规动画之一。 计算其 SelectScript 属性的值;返回值必须是数字。 根据此数字，将执行 &lt;事例&gt; 中的一个 subanimations。 例如，如果 SelectScript 的计算结果为2，则控件工具包会在 &lt;大小写&gt; （从0开始计数）内运行第三个动画。

以下标记定义了三个 subanimations：调整宽度大小、调整高度大小并淡出。然后，JavaScript 代码（`Math.floor(3 * Math.random())`）将选取0到2之间的一个数字，以便运行三个动画之一：

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

[![可能的三个动画之一：面板变宽](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

可能的三个动画之一：面板变宽（[单击以查看完全大小的图像](picking-one-animation-out-of-a-list-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](animation-depending-on-a-condition-cs.md)
> [下一页](animating-in-response-to-user-interaction-cs.md)
