---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 在动画过程中禁用操作（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它还支持操作 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606807"
---
# <a name="disabling-actions-during-animation-vb"></a>动画过程中禁用操作 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它还支持鼠标单击等操作。 但当鼠标单击开始动画时，最好在动画过程中禁用鼠标单击。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它还支持鼠标单击等操作。 但当鼠标单击开始动画时，最好在动画过程中禁用鼠标单击。

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

动画将应用于如下所示的 HTML 按钮：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

请注意，使用 HTML 控件而不是 Web 控件，因为我们不希望按钮创建回发;它只应启动客户端动画。

然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

在 `<Animations>` "节点中，`<OnClick>` 是用于处理鼠标单击的右元素。 但是，在动画过程中也可以单击该按钮。 `<EnableAction>` 元素可以处理这种情况。 设置 `Enabled="false"` 将在动画中禁用该按钮。 由于我们使用多个单独的动画（禁用按钮和实际动画），因此需要 `<Parallel>` 元素将单个动画一起粘附到其中。 下面是 `AnimationExtender`的完整标记：

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

在动画后，还可以使用列表末尾的以下 XML 元素来重新启用按钮：

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

但在给定的方案中，这会很无用，因为按钮淡出，在动画结束时不可见。

[![动画运行后，按钮将被禁用](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

动画运行后，该按钮将被禁用（[单击以查看完全大小的图像](disabling-actions-during-animation-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](animating-in-response-to-user-interaction-vb.md)
> [下一页](triggering-an-animation-in-another-control-vb.md)
