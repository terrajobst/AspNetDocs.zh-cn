---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 对 UpdatePanel 控件（C#）进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 有关 ... 的内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599910"
---
# <a name="animating-an-updatepanel-control-c"></a>对 UpdatePanel 控件执行动画处理 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 对于 UpdatePanel 的内容，存在大量依赖于动画框架的特殊扩展器： UpdatePanelAnimation。 本教程演示如何为 UpdatePanel 设置此类动画。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 对于 `UpdatePanel`的内容，存在大量依赖于动画框架的特殊扩展器： `UpdatePanelAnimation`。 本教程演示如何为 `UpdatePanel`设置此类动画。

## <a name="steps"></a>步骤

第一步通常是将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

此方案中的动画将应用到驻留在 `UpdatePanel`中的 ASP.NET `Wizard` web 控件。 三个（任意）步骤提供了足够的选项来触发回发：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

`UpdatePanelAnimationExtender` 控件所需的标记与用于 `AnimationExtender`的标记非常类似。 在 `TargetControlID` 特性中，我们提供了要进行动画处理的 `UpdatePanel` `ID`;在 `UpdatePanelAnimationExtender` 控件内，`<Animations>` 元素保存动画的 XML 标记。 但有一个差异：与 `AnimationExtender`相比，事件和事件处理程序的数量受到限制。 对于 `UpdatePanels`，只存在其中的两个：

- 更新 UpdatePanel 后 `<OnUpdated>`
- 当 UpdatePanel 开始更新时 `<OnUpdating>`

在此方案中，`UpdatePanel` 的新内容（在回发之后）应淡入。 这是所需的标记：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

现在，每当在 UpdatePanel 内发生回发时，面板的新内容就会平稳地淡化。

[![下一个向导步骤淡入](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

下一个向导步骤淡入（[单击查看完全大小的图像](animating-an-updatepanel-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](changing-an-animation-using-client-side-code-cs.md)
> [下一页](dynamically-controlling-updatepanel-animations-cs.md)
