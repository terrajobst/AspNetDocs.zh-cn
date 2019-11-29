---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: 使用客户端代码执行动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画执行 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: b6ba1553b9c8c51d5d6ae1679e53f9cc1d17b769
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599666"
---
# <a name="executing-animations-using-client-side-code-c"></a>使用客户端代码执行动画 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 还可以使用自定义客户端 JavaScript 代码触发动画的执行。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 还可以使用自定义客户端 JavaScript 代码触发动画的执行。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

在 "`<Animations>`" 节点中，在用户单击面板后使用 `<OnClick>` 运行动画。 添加两个要并行执行的动画：

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

为了演示这种情况，在页面运行后，将使用 JavaScript 代码执行此动画（以及使用控制工具包创建的任何其他动画）。 首先，我们需要访问 `AnimationExtender` 控件。 ASP.NET AJAX 库为此任务提供 `$find()` 函数：

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

`AnimationExtender` 控件公开一个丰富的 API，其中包含名称与 XML 标记中使用的事件处理程序相同的方法： `OnClick()`、`OnLoad()`等。 例如，调用 `OnClick()` 方法会在 `AnimationExtender` 控件的 `<OnClick>` 元素内执行动画：

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

下面是完整的客户端 JavaScript 代码，该代码在页面完全加载后，将模拟单击面板上的单击，请注意，一旦页面和所有包含的 JavaScript 库加载完毕，ASP.NET AJAX 就会调用 `pageLoad()` 函数名称。

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

[![动画立即运行，而无需鼠标单击](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

动画会立即运行，无需鼠标单击（[单击即可查看完全大小的图像](executing-animations-using-client-side-code-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](modifying-animations-from-the-server-side-cs.md)
> [下一页](changing-an-animation-using-client-side-code-cs.md)
