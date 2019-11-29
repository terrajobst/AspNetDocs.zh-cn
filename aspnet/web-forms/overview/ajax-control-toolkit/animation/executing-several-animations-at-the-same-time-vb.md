---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 同时执行多个动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许运行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: fc11debd06c897c29db56d42167d483f5608cdf8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575327"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a>同时执行多个动画（VB）

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许以并行方式运行多个动画。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许以并行方式运行多个动画。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。 通常，`<OnLoad>` 仅接受一个动画。 动画框架允许使用 `<Parallel>` 元素将几个动画联接到其中。 `<Parallel>` 中的所有动画都将同时执行。

下面是 `AnimationExtender` 控件的可能标记，同时淡化和调整面板的大小：

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

确实：运行此脚本时，将显示面板，然后调整其大小（超过 tripling 宽度并一半其高度），并同时淡出。

[由于浏览器的呈现引擎，面板会淡化并调整大小（包括其内容） ![](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

由于浏览器的呈现引擎，该面板会淡化并调整大小（包括其内容）（[单击查看完全大小的图像](executing-several-animations-at-the-same-time-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](adding-animation-to-a-control-vb.md)
> [下一页](executing-several-animations-after-each-other-vb.md)
