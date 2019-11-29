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
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="818d7-104">将动画添加到控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="818d7-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="818d7-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="818d7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="818d7-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="818d7-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="818d7-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="818d7-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="818d7-108">本教程介绍如何设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="818d7-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="818d7-109">概述</span><span class="sxs-lookup"><span data-stu-id="818d7-109">Overview</span></span>

<span data-ttu-id="818d7-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="818d7-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="818d7-111">本教程介绍如何设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="818d7-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="818d7-112">步骤</span><span class="sxs-lookup"><span data-stu-id="818d7-112">Steps</span></span>

<span data-ttu-id="818d7-113">第一步通常是将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：</span><span class="sxs-lookup"><span data-stu-id="818d7-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="818d7-114">此方案中的动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="818d7-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="818d7-115">面板的关联 CSS 类定义背景色和宽度：</span><span class="sxs-lookup"><span data-stu-id="818d7-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="818d7-116">接下来，我们需要 `AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="818d7-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="818d7-117">提供 `ID` 和通常的 `runat="server"`之后，`TargetControlID` 特性必须设置为在示例中为动画显示的面板：</span><span class="sxs-lookup"><span data-stu-id="818d7-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="818d7-118">使用 XML 语法以声明方式应用整个动画，但目前尚不完全支持 Visual Studio 的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="818d7-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="818d7-119">根节点在此节点中 `<Animations>;`，允许多个事件确定何时执行动画（s）：</span><span class="sxs-lookup"><span data-stu-id="818d7-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="818d7-120">`OnClick` （鼠标单击）</span><span class="sxs-lookup"><span data-stu-id="818d7-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="818d7-121">`OnHoverOut` （当鼠标离开控件时）</span><span class="sxs-lookup"><span data-stu-id="818d7-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="818d7-122">`OnHoverOver` （当鼠标悬停在控件上时，停止 `OnHoverOut` 动画）</span><span class="sxs-lookup"><span data-stu-id="818d7-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="818d7-123">`OnLoad` （已加载页面时）</span><span class="sxs-lookup"><span data-stu-id="818d7-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="818d7-124">`OnMouseOut` （当鼠标离开控件时）</span><span class="sxs-lookup"><span data-stu-id="818d7-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="818d7-125">`OnMouseOver` （当鼠标悬停在控件上时，不会停止 `OnMouseOut` 动画）</span><span class="sxs-lookup"><span data-stu-id="818d7-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="818d7-126">该框架附带一组动画，每个动画由其自己的 XML 元素表示。</span><span class="sxs-lookup"><span data-stu-id="818d7-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="818d7-127">下面是一个选择：</span><span class="sxs-lookup"><span data-stu-id="818d7-127">Here is a selection:</span></span>

- <span data-ttu-id="818d7-128">`<Color>` （更改颜色）</span><span class="sxs-lookup"><span data-stu-id="818d7-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="818d7-129">`<FadeIn>` （淡入）</span><span class="sxs-lookup"><span data-stu-id="818d7-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="818d7-130">`<FadeOut>` （淡化）</span><span class="sxs-lookup"><span data-stu-id="818d7-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="818d7-131">`<Property>` （更改控件的属性）</span><span class="sxs-lookup"><span data-stu-id="818d7-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="818d7-132">`<Pulse>` （pulsating）</span><span class="sxs-lookup"><span data-stu-id="818d7-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="818d7-133">`<Resize>` （更改大小）</span><span class="sxs-lookup"><span data-stu-id="818d7-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="818d7-134">`<Scale>` （按比例更改大小）</span><span class="sxs-lookup"><span data-stu-id="818d7-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="818d7-135">在此示例中，面板应淡出。动画将需要1.5 秒（`Duration` 属性），并显示每秒24帧（动画步骤）（`Fps` 属性）。</span><span class="sxs-lookup"><span data-stu-id="818d7-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="818d7-136">下面是 `AnimationExtender` 控件的完整标记：</span><span class="sxs-lookup"><span data-stu-id="818d7-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="818d7-137">运行此脚本时，将显示面板，并在1到半秒内淡出。</span><span class="sxs-lookup"><span data-stu-id="818d7-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="818d7-138">[面板 ![淡出](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="818d7-138">[![The panel is fading out](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="818d7-139">面板会淡化（[单击以查看完全大小的图像](adding-animation-to-a-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="818d7-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="818d7-140">[上一页](dynamically-controlling-updatepanel-animations-cs.md)
> [下一页](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="818d7-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
