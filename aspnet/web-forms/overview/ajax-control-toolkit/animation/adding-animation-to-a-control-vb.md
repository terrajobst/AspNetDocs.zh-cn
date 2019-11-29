---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 向控件添加动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 本教程演示如何 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607146"
---
# <a name="adding-animation-to-a-control-vb"></a>将动画添加到控件 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 本教程介绍如何设置此类动画。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 本教程介绍如何设置此类动画。

## <a name="steps"></a>步骤

第一步通常是将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

此方案中的动画将应用于文本面板，如下所示：

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

面板的关联 CSS 类定义背景色和宽度：

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

接下来，我们需要 `AnimationExtender`。 提供 `ID` 和通常的 `runat="server"`之后，`TargetControlID` 特性必须设置为在示例中为动画显示的面板：

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

使用 XML 语法以声明方式应用整个动画，但目前尚不完全支持 Visual Studio 的 IntelliSense。 根节点在此节点中 `<Animations>;`，允许多个事件确定何时执行动画（s）：

- `OnClick` （鼠标单击）
- `OnHoverOut` （当鼠标离开控件时）
- `OnHoverOver` （当鼠标悬停在控件上时，停止 `OnHoverOut` 动画）
- `OnLoad` （已加载页面时）
- `OnMouseOut` （当鼠标离开控件时）
- `OnMouseOver` （当鼠标悬停在控件上时，不会停止 `OnMouseOut` 动画）

该框架附带一组动画，每个动画由其自己的 XML 元素表示。 下面是一个选择：

- `<Color>` （更改颜色）
- `<FadeIn>` （淡入）
- `<FadeOut>` （淡化）
- `<Property>` （更改控件的属性）
- `<Pulse>` （pulsating）
- `<Resize>` （更改大小）
- `<Scale>` （按比例更改大小）

在此示例中，面板应淡出。动画将需要1.5 秒（`Duration` 属性），并显示每秒24帧（动画步骤）（`Fps` 属性）。 下面是 `AnimationExtender` 控件的完整标记：

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

运行此脚本时，将显示面板，并在1到半秒内淡出。

[面板 ![淡出](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

面板会淡化（[单击以查看完全大小的图像](adding-animation-to-a-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](dynamically-controlling-updatepanel-animations-cs.md)
> [下一页](executing-several-animations-at-the-same-time-vb.md)
