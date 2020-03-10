---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 多次执行多个动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许运行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483980"
---
# <a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="dc3cc-104">逐一执行多个动画 (VB)</span><span class="sxs-lookup"><span data-stu-id="dc3cc-104">Executing Several Animations after Each Other (VB)</span></span>

<span data-ttu-id="dc3cc-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="dc3cc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="dc3cc-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="dc3cc-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="dc3cc-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dc3cc-108">它允许逐个运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-108">It allows to run several animations one after the other.</span></span>

## <a name="overview"></a><span data-ttu-id="dc3cc-109">概述</span><span class="sxs-lookup"><span data-stu-id="dc3cc-109">Overview</span></span>

<span data-ttu-id="dc3cc-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dc3cc-111">它允许逐个运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="dc3cc-112">步骤</span><span class="sxs-lookup"><span data-stu-id="dc3cc-112">Steps</span></span>

<span data-ttu-id="dc3cc-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="dc3cc-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="dc3cc-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc3cc-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="dc3cc-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="dc3cc-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="dc3cc-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="dc3cc-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="dc3cc-117">在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="dc3cc-118">通常，`<OnLoad>` 仅接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="dc3cc-119">动画框架允许使用 `<Sequence>` 元素将几个动画联接到其中。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="dc3cc-120">`<Sequence>` 中的所有动画都将再执行一次。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="dc3cc-121">下面是 `AnimationExtender` 控件的可能标记，首先使面板更宽，然后降低其高度：</span><span class="sxs-lookup"><span data-stu-id="dc3cc-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="dc3cc-122">运行此脚本时，面板首先变宽，然后变小。</span><span class="sxs-lookup"><span data-stu-id="dc3cc-122">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="dc3cc-123">[![首先增加宽度](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dc3cc-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="dc3cc-124">首先增加宽度（[单击查看完全尺寸的图像](executing-several-animations-after-each-other-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="dc3cc-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>

<span data-ttu-id="dc3cc-125">[![，则会降低高度](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="dc3cc-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="dc3cc-126">那么，高度会下降（[单击查看完全大小的图像](executing-several-animations-after-each-other-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="dc3cc-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dc3cc-127">[上一页](executing-several-animations-at-the-same-time-vb.md)
> [下一页](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="dc3cc-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
