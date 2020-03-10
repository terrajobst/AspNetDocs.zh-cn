---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 针对用户交互（C#）响应进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画可以是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497900"
---
# <a name="animating-in-response-to-user-interaction-c"></a>响应用户交互的动画 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画可以自动启动，也可以由用户交互触发，例如通过单击鼠标。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画可以自动启动，也可以由用户交互触发，例如通过单击鼠标。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

在 "`<Animations>`" 节点中，有五种方法可通过用户交互启动动画（缺少的元素 `<OnLoad>` 在整个页面完全加载后执行）：

- `<OnClick>` （鼠标单击控件）
- `<OnHoverOut>` （鼠标离开控件）
- `<OnHoverOver>` （将鼠标悬停在控件上，停止 `<OnHoverOut>` 动画）
- `<OnMouseOut>` （鼠标离开控件）
- `<OnMouseOver>` （将鼠标悬停在控件上，而不是停止 `<OnMouseOut>` 动画）

在这种情况下，将使用 `<OnClick>`。 用户单击面板时，将同时调整其大小并淡出。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

[![鼠标单击开始动画](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

鼠标单击开始动画（[单击查看完全大小的图像](animating-in-response-to-user-interaction-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](picking-one-animation-out-of-a-list-cs.md)
> [下一页](disabling-actions-during-animation-cs.md)
