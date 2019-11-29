---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: 多次执行多个动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它允许运行 severa 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: e378ac038796dbd44e89d099532b9e186dcf673f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575455"
---
# <a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="6997d-104">逐一执行多个动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="6997d-104">Executing Several Animations after Each Other (C#)</span></span>

<span data-ttu-id="6997d-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6997d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6997d-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6997d-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="6997d-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="6997d-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6997d-108">它允许逐个运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="6997d-108">It allows to run several animations one after the other.</span></span>

<span data-ttu-id="6997d-109">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="6997d-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6997d-110">它允许逐个运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="6997d-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="6997d-111">步骤</span><span class="sxs-lookup"><span data-stu-id="6997d-111">Steps</span></span>

<span data-ttu-id="6997d-112">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="6997d-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="6997d-113">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6997d-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="6997d-114">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="6997d-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="6997d-115">然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="6997d-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="6997d-116">在 "`<Animations>`" 节点中，在完全加载页面后使用 `<OnLoad>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="6997d-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="6997d-117">通常，`<OnLoad>` 仅接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="6997d-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="6997d-118">动画框架允许使用 `<Sequence>` 元素将几个动画联接到其中。</span><span class="sxs-lookup"><span data-stu-id="6997d-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="6997d-119">`<Sequence>` 中的所有动画都将再执行一次。</span><span class="sxs-lookup"><span data-stu-id="6997d-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="6997d-120">下面是 `AnimationExtender` 控件的可能标记，首先使面板更宽，然后降低其高度：</span><span class="sxs-lookup"><span data-stu-id="6997d-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="6997d-121">运行此脚本时，面板首先变宽，然后变小。</span><span class="sxs-lookup"><span data-stu-id="6997d-121">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="6997d-122">[![首先增加宽度](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6997d-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="6997d-123">首先增加宽度（[单击查看完全尺寸的图像](executing-several-animations-after-each-other-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="6997d-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>

<span data-ttu-id="6997d-124">[![，则会降低高度](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6997d-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="6997d-125">那么，高度会下降（[单击查看完全大小的图像](executing-several-animations-after-each-other-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="6997d-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6997d-126">[上一页](executing-several-animations-at-the-same-time-cs.md)
> [下一页](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6997d-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
