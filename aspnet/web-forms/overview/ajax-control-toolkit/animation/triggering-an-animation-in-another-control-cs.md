---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: 在另一个控件中触发动画C#（） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 通常，启动 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e0a1f8986047da04db6fde8e54b6fd0ac6ee2603
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430790"
---
# <a name="triggering-an-animation-in-another-control-c"></a>触发另一控件的动画 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 通常，启动动画时，用户与相同的控件交互。 不过，它还可以与一个控件交互，然后动画另一个控件。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 通常，启动动画时，用户与相同的控件交互。 不过，它还可以与一个控件交互，然后动画另一个控件。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

若要开始对面板进行动画处理，请使用 HTML 按钮。 请注意，`<input type="button" />` 在 `<asp:Button />` 上 favoured，因为当用户单击该按钮时，不需要回发。

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server"`。 务必将 `TargetControlID` 设置为按钮的 ID （触发动画的元素），而不是设置为面板的 ID （要进行动画处理的元素）

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

在 `<Animations>` "节点中，按常规方式放置动画。 若要使它们更改面板而不是按钮，请在 `AnimationExtender`中设置每个动画元素的 `AnimationTarget` 属性。 当然，`AnimationTarget` 的值是面板的 ID。 这样一来，便可在面板中进行动画处理，而不会发生触发器按钮。 下面是此方案的 `AnimationExtender` 标记：

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

请注意各个动画的显示顺序。 首先，动画运行后按钮将被停用。 由于 `<EnableAction>` 元素中没有 `AnimationTarget` 特性，因此此动画将应用于原始控件：按钮。 接下来的两个动画步骤应并行执行（`<Parallel>` 元素）。 这两个属性的 `AnimationTarget` 属性都设置为 `"Panel1"`，因此会对面板而不是按钮进行动画处理。

[![鼠标单击按钮时，将启动面板动画](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)

当鼠标单击按钮时，将启动面板动画（[单击以查看完全大小的图像](triggering-an-animation-in-another-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](disabling-actions-during-animation-cs.md)
> [下一页](modifying-animations-from-the-server-side-cs.md)
