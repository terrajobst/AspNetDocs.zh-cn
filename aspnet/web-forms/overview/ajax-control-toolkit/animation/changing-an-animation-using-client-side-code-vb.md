---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: 使用客户端代码更改动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画还可以 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: cce0a5a901f71edd40eada59ac7eeba93222e2b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430988"
---
# <a name="changing-an-animation-using-client-side-code-vb"></a>使用客户端代码更改动画 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 还可以使用自定义客户端 JavaScript 代码更改动画。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 还可以使用自定义客户端 JavaScript 代码更改动画。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

实际动画由 HTML 按钮启动：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

请注意，`AnimationExtender` 控件中没有 `<Animations>` 的节点。 自定义 JavaScript 代码用于提供与控件一起使用的动画。

与 `AnimationExtender`的服务器 API 一样，尚无简单的方法可以将动画分配到扩展器。 但是，扩展器确实会公开多种方法来读取和写入注册到各种事件的动画（`OnClick`、`OnLoad`等）。 下面是一些可能的恶意活动：

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

`get_*()` 函数的返回值的格式和 `set_*()` 函数的参数格式是一个 JSON 字符串，它提供 XML 标记的对象表示形式。 当前无法在中传递对象，但可以从给定动画（`get_OnXXXBehavior()` 方法）中读取对象。

下面是一个 JSON 字符串（没有分隔引号并且格式漂亮）表示由按钮触发的动画，但通过调整面板的大小并同时淡化面板来对其进行动画处理：

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

以下 JavaScript 代码将此 JSON descripting 分配给当前扩展器的 `OnClick` 动画，并运行它：

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]

[![动画会立即运行，而无需鼠标单击（且标记极少）](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

动画会立即运行，而无需鼠标单击（并显示很少的标记）（[单击即可查看完全大小的图像](changing-an-animation-using-client-side-code-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](executing-animations-using-client-side-code-vb.md)
> [下一页](animating-an-updatepanel-control-vb.md)
