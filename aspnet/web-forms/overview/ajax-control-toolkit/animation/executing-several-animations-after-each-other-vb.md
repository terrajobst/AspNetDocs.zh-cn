---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 多次执行多个动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许运行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606877"
---
# <a name="executing-several-animations-after-each-other-vb"></a>逐一执行多个动画 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许逐个运行多个动画。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许逐个运行多个动画。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。 通常，`<OnLoad>` 仅接受一个动画。 动画框架允许使用 `<Sequence>` 元素将几个动画联接到其中。 `<Sequence>` 中的所有动画都将再执行一次。 下面是 `AnimationExtender` 控件的可能标记，首先使面板更宽，然后降低其高度：

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

运行此脚本时，面板首先变宽，然后变小。

[![首先增加宽度](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

首先增加宽度（[单击查看完全尺寸的图像](executing-several-animations-after-each-other-vb/_static/image3.png)）

[![，则会降低高度](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

那么，高度会下降（[单击查看完全大小的图像](executing-several-animations-after-each-other-vb/_static/image6.png)）

> [!div class="step-by-step"]
> [上一页](executing-several-animations-at-the-same-time-vb.md)
> [下一页](animation-depending-on-a-condition-vb.md)
