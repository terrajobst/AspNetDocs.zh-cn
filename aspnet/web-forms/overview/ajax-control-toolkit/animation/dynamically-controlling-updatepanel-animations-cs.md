---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: 动态控制 UpdatePanel 动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 有关 ... 的内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606799"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a>动态控制 UpdatePanel 动画 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 对于 UpdatePanel 的内容，存在大量依赖于动画框架的特殊扩展器： UpdatePanelAnimation。 它还可以与 UpdatePanel 触发器一起使用。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 对于 `UpdatePanel`的内容，存在大量依赖于动画框架的特殊扩展器： `UpdatePanelAnimation`。 它还可以与 `UpdatePanel` 触发器一起使用。

## <a name="steps"></a>步骤

第一步通常是将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

此方案中的动画将应用于当前时间的显示。 可以使用 `Page_Load()` 方法将此信息写入标签，或者（为了简单起见），使用以下内联代码：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

此外，还会创建用于触发更新时间的按钮：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

然后，将此代码放入 `UpdatePanel` 元素的 `<ContentTemplate>` 部分。 面板的 `UpdateMode` 特性必须设置为 `"Conditional"`，因为只有触发器可以更新面板的内容。 在 `UpdatePanel`的 `<Triggers>` 部分，将创建一个异步回发触发器，并将其绑定到按钮的 `Click` 事件。 因此，如果用户单击该按钮，则将刷新 `UpdatePanel`。 下面是 `UpdatePanel` 控件的标记：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

最后，必须配置 `UpdatePanelAnimationExtender`：将 `TargetControlID` 属性设置为面板的 ID，并在扩展器中定义一个动画。 淡入非常有意义，这会对更新的时间产生良好的视觉效果。 扩展器标记可能如下所示：

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

在浏览器中运行该文件。 只要单击该按钮，当前时间就会显示在面板中，在一秒的持续时间内总是淡入。

[![当前时间淡入](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)

当前时间已淡入（[单击查看完全大小的图像](dynamically-controlling-updatepanel-animations-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](animating-an-updatepanel-control-cs.md)
> [下一页](adding-animation-to-a-control-vb.md)
