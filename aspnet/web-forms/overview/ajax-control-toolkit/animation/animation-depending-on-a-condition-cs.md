---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 基于条件的动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画是否为 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484166"
---
# <a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="6b8a8-104">取决于条件的动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="6b8a8-104">Animation Depending On a Condition (C#)</span></span>

<span data-ttu-id="6b8a8-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6b8a8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6b8a8-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6b8a8-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="6b8a8-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6b8a8-108">是否运行动画也可能依赖于某些 JavaScript 代码形式的条件。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="6b8a8-109">概述</span><span class="sxs-lookup"><span data-stu-id="6b8a8-109">Overview</span></span>

<span data-ttu-id="6b8a8-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6b8a8-111">是否运行动画也可能依赖于某些 JavaScript 代码形式的条件。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="6b8a8-112">步骤</span><span class="sxs-lookup"><span data-stu-id="6b8a8-112">Steps</span></span>

<span data-ttu-id="6b8a8-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="6b8a8-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="6b8a8-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b8a8-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="6b8a8-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="6b8a8-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="6b8a8-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="6b8a8-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="6b8a8-117">在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="6b8a8-118">`<Condition>` 元素会进入播放，而不是常规动画之一。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="6b8a8-119">作为 `ConditionScript` 特性的值提供的 JavaScript 代码在运行时执行。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="6b8a8-120">如果计算结果为 true，则执行动画，否则不执行。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="6b8a8-121">下面的标记提供了两个动画，其中每个动画都是随机在50% 的情况下执行的。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="6b8a8-122">由于 `<OnLoad>`中可能只有一个动画，因此使用 `<Sequence>` 元素将两个 `<Condition>` 动画联接在一起：</span><span class="sxs-lookup"><span data-stu-id="6b8a8-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="6b8a8-123">请注意，必须对 `ConditionScript` 属性中的小于号（`<`）进行转义（）。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="6b8a8-124">运行此脚本时，不会运行任何动画，也不会运行其中一项操作，也可以同时执行这两项操作。</span><span class="sxs-lookup"><span data-stu-id="6b8a8-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="6b8a8-125">[![面板在不调整大小的情况下淡出，因此第二个动画将运行，第一个动画不会](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b8a8-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="6b8a8-126">面板在不调整大小的情况下淡出，因此第二个动画将运行，第一个动画不会（[单击查看全尺寸图像](animation-depending-on-a-condition-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="6b8a8-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6b8a8-127">[上一页](executing-several-animations-after-each-other-cs.md)
> [下一页](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6b8a8-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
