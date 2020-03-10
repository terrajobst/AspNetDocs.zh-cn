---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 同时执行多个动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许运行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: fc11debd06c897c29db56d42167d483f5608cdf8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497798"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="93f85-104">同时执行多个动画（VB）</span><span class="sxs-lookup"><span data-stu-id="93f85-104">Executing Several Animations at The Same Time (VB)</span></span>

<span data-ttu-id="93f85-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="93f85-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="93f85-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="93f85-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="93f85-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="93f85-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="93f85-108">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="93f85-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="93f85-109">概述</span><span class="sxs-lookup"><span data-stu-id="93f85-109">Overview</span></span>

<span data-ttu-id="93f85-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="93f85-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="93f85-111">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="93f85-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="93f85-112">步骤</span><span class="sxs-lookup"><span data-stu-id="93f85-112">Steps</span></span>

<span data-ttu-id="93f85-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="93f85-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="93f85-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="93f85-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="93f85-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="93f85-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="93f85-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="93f85-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="93f85-117">在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="93f85-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="93f85-118">通常，`<OnLoad>` 仅接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="93f85-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="93f85-119">动画框架允许使用 `<Parallel>` 元素将几个动画联接到其中。</span><span class="sxs-lookup"><span data-stu-id="93f85-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="93f85-120">`<Parallel>` 中的所有动画都将同时执行。</span><span class="sxs-lookup"><span data-stu-id="93f85-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="93f85-121">下面是 `AnimationExtender` 控件的可能标记，同时淡化和调整面板的大小：</span><span class="sxs-lookup"><span data-stu-id="93f85-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="93f85-122">确实：运行此脚本时，将显示面板，然后调整其大小（超过 tripling 宽度并一半其高度），并同时淡出。</span><span class="sxs-lookup"><span data-stu-id="93f85-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="93f85-123">[由于浏览器的呈现引擎，面板会淡化并调整大小（包括其内容） ![](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="93f85-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="93f85-124">由于浏览器的呈现引擎，该面板会淡化并调整大小（包括其内容）（[单击查看完全大小的图像](executing-several-animations-at-the-same-time-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="93f85-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="93f85-125">[上一页](adding-animation-to-a-control-vb.md)
> [下一页](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="93f85-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
