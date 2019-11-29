---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: 从列表中选取一个动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 该框架还允许
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606744"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="77d45-104">选取列表中的一个动画 (VB)</span><span class="sxs-lookup"><span data-stu-id="77d45-104">Picking One Animation Out Of a List (VB)</span></span>

<span data-ttu-id="77d45-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="77d45-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="77d45-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="77d45-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="77d45-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="77d45-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="77d45-108">使用该框架，程序员还可以根据某些 JavaScript 代码的评估，从动画列表中选取一种动画。</span><span class="sxs-lookup"><span data-stu-id="77d45-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="77d45-109">概述</span><span class="sxs-lookup"><span data-stu-id="77d45-109">Overview</span></span>

<span data-ttu-id="77d45-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="77d45-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="77d45-111">使用该框架，程序员还可以根据某些 JavaScript 代码的评估，从动画列表中选取一种动画。</span><span class="sxs-lookup"><span data-stu-id="77d45-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="77d45-112">步骤</span><span class="sxs-lookup"><span data-stu-id="77d45-112">Steps</span></span>

<span data-ttu-id="77d45-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="77d45-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="77d45-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="77d45-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="77d45-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="77d45-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="77d45-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="77d45-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="77d45-117">在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="77d45-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="77d45-118">`<Case>` 元素会进入播放，而不是常规动画之一。</span><span class="sxs-lookup"><span data-stu-id="77d45-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="77d45-119">计算其 SelectScript 属性的值;返回值必须是数字。</span><span class="sxs-lookup"><span data-stu-id="77d45-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="77d45-120">根据此数字，将执行 &lt;事例&gt; 中的一个 subanimations。</span><span class="sxs-lookup"><span data-stu-id="77d45-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="77d45-121">例如，如果 SelectScript 的计算结果为2，则控件工具包会在 &lt;大小写&gt; （从0开始计数）内运行第三个动画。</span><span class="sxs-lookup"><span data-stu-id="77d45-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="77d45-122">以下标记定义了三个 subanimations：调整宽度大小、调整高度大小并淡出。然后，JavaScript 代码（`Math.floor(3 * Math.random())`）将选取0到2之间的一个数字，以便运行三个动画之一：</span><span class="sxs-lookup"><span data-stu-id="77d45-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

<span data-ttu-id="77d45-123">[![可能的三个动画之一：面板变宽](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77d45-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="77d45-124">可能的三个动画之一：面板变宽（[单击以查看完全大小的图像](picking-one-animation-out-of-a-list-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="77d45-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77d45-125">[上一页](animation-depending-on-a-condition-vb.md)
> [下一页](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="77d45-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
