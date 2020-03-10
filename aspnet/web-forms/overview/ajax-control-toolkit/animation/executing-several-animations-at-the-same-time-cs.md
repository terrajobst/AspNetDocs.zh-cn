---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: 同时执行多个动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许运行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483968"
---
# <a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="58ff0-104">同时执行多个动画（C#）</span><span class="sxs-lookup"><span data-stu-id="58ff0-104">Executing Several Animations at The Same Time (C#)</span></span>

<span data-ttu-id="58ff0-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="58ff0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="58ff0-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="58ff0-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="58ff0-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="58ff0-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="58ff0-108">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="58ff0-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="58ff0-109">概述</span><span class="sxs-lookup"><span data-stu-id="58ff0-109">Overview</span></span>

<span data-ttu-id="58ff0-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="58ff0-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="58ff0-111">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="58ff0-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="58ff0-112">步骤</span><span class="sxs-lookup"><span data-stu-id="58ff0-112">Steps</span></span>

<span data-ttu-id="58ff0-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="58ff0-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="58ff0-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="58ff0-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="58ff0-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="58ff0-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="58ff0-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="58ff0-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="58ff0-117">在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="58ff0-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="58ff0-118">通常，`<OnLoad>` 仅接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="58ff0-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="58ff0-119">动画框架允许使用 `<Parallel>` 元素将几个动画联接到其中。</span><span class="sxs-lookup"><span data-stu-id="58ff0-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="58ff0-120">`<Parallel>` 中的所有动画都将同时执行。</span><span class="sxs-lookup"><span data-stu-id="58ff0-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="58ff0-121">下面是 `AnimationExtender` 控件的可能标记，同时淡化和调整面板的大小：</span><span class="sxs-lookup"><span data-stu-id="58ff0-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="58ff0-122">确实：运行此脚本时，将显示面板，然后调整其大小（超过 tripling 宽度并一半其高度），并同时淡出。</span><span class="sxs-lookup"><span data-stu-id="58ff0-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="58ff0-123">[由于浏览器的呈现引擎，面板会淡化并调整大小（包括其内容） ![](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="58ff0-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="58ff0-124">由于浏览器的呈现引擎，该面板会淡化并调整大小（包括其内容）（[单击查看完全大小的图像](executing-several-animations-at-the-same-time-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="58ff0-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58ff0-125">[上一页](adding-animation-to-a-control-cs.md)
> [下一页](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="58ff0-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
