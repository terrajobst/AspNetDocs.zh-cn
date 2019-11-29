---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: 基于条件的动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画是否为 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 583ebdbf109beb74b9a425020477183067bbb79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607007"
---
# <a name="animation-depending-on-a-condition-vb"></a>取决于条件的动画 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 是否运行动画也可能依赖于某些 JavaScript 代码形式的条件。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 是否运行动画也可能依赖于某些 JavaScript 代码形式的条件。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。 `<Condition>` 元素会进入播放，而不是常规动画之一。 作为 `ConditionScript` 特性的值提供的 JavaScript 代码在运行时执行。 如果计算结果为 true，则执行动画，否则不执行。 下面的标记提供了两个动画，其中每个动画都是随机在50% 的情况下执行的。 由于 `<OnLoad>`中可能只有一个动画，因此使用 `<Sequence>` 元素将两个 `<Condition>` 动画联接在一起：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

请注意，必须对 `ConditionScript` 属性中的小于号（`<`）进行转义（）。 运行此脚本时，不会运行任何动画，也不会运行其中一项操作，也可以同时执行这两项操作。

[![面板在不调整大小的情况下淡出，因此第二个动画将运行，第一个动画不会](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

面板在不调整大小的情况下淡出，因此第二个动画将运行，第一个动画不会（[单击查看全尺寸图像](animation-depending-on-a-condition-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](executing-several-animations-after-each-other-vb.md)
> [下一页](picking-one-animation-out-of-a-list-vb.md)
