---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 在另一个控件中触发动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 通常，启动 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430784"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="90a26-104">触发另一控件的动画 (VB)</span><span class="sxs-lookup"><span data-stu-id="90a26-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="90a26-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="90a26-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="90a26-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="90a26-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="90a26-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="90a26-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="90a26-108">通常，启动动画时，用户与相同的控件交互。</span><span class="sxs-lookup"><span data-stu-id="90a26-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="90a26-109">不过，它还可以与一个控件交互，然后动画另一个控件。</span><span class="sxs-lookup"><span data-stu-id="90a26-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="90a26-110">概述</span><span class="sxs-lookup"><span data-stu-id="90a26-110">Overview</span></span>

<span data-ttu-id="90a26-111">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="90a26-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="90a26-112">通常，启动动画时，用户与相同的控件交互。</span><span class="sxs-lookup"><span data-stu-id="90a26-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="90a26-113">不过，它还可以与一个控件交互，然后动画另一个控件。</span><span class="sxs-lookup"><span data-stu-id="90a26-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="90a26-114">步骤</span><span class="sxs-lookup"><span data-stu-id="90a26-114">Steps</span></span>

<span data-ttu-id="90a26-115">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="90a26-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="90a26-116">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="90a26-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="90a26-117">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="90a26-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="90a26-118">若要开始对面板进行动画处理，请使用 HTML 按钮。</span><span class="sxs-lookup"><span data-stu-id="90a26-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="90a26-119">请注意，`<input type="button" />` 在 `<asp:Button />` 上 favoured，因为当用户单击该按钮时，不需要回发。</span><span class="sxs-lookup"><span data-stu-id="90a26-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="90a26-120">然后，将 `AnimationExtender` 添加到页面，提供 `ID`、`TargetControlID` 属性和必备 `runat="server"`。</span><span class="sxs-lookup"><span data-stu-id="90a26-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="90a26-121">务必将 `TargetControlID` 设置为按钮的 ID （触发动画的元素），而不是设置为面板的 ID （要进行动画处理的元素）</span><span class="sxs-lookup"><span data-stu-id="90a26-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="90a26-122">在 `<Animations>` "节点中，按常规方式放置动画。</span><span class="sxs-lookup"><span data-stu-id="90a26-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="90a26-123">若要使它们更改面板而不是按钮，请在 `AnimationExtender`中设置每个动画元素的 `AnimationTarget` 属性。</span><span class="sxs-lookup"><span data-stu-id="90a26-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="90a26-124">当然，`AnimationTarget` 的值是面板的 ID。</span><span class="sxs-lookup"><span data-stu-id="90a26-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="90a26-125">这样一来，便可在面板中进行动画处理，而不会发生触发器按钮。</span><span class="sxs-lookup"><span data-stu-id="90a26-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="90a26-126">下面是此方案的 `AnimationExtender` 标记：</span><span class="sxs-lookup"><span data-stu-id="90a26-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="90a26-127">请注意各个动画的显示顺序。</span><span class="sxs-lookup"><span data-stu-id="90a26-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="90a26-128">首先，动画运行后按钮将被停用。</span><span class="sxs-lookup"><span data-stu-id="90a26-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="90a26-129">由于 `<EnableAction>` 元素中没有 `AnimationTarget` 特性，因此此动画将应用于原始控件：按钮。</span><span class="sxs-lookup"><span data-stu-id="90a26-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="90a26-130">接下来的两个动画步骤应并行执行（`<Parallel>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="90a26-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="90a26-131">这两个属性的 `AnimationTarget` 属性都设置为 `"Panel1"`，因此会对面板而不是按钮进行动画处理。</span><span class="sxs-lookup"><span data-stu-id="90a26-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="90a26-132">[![鼠标单击按钮时，将启动面板动画](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="90a26-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="90a26-133">当鼠标单击按钮时，将启动面板动画（[单击以查看完全大小的图像](triggering-an-animation-in-another-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="90a26-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="90a26-134">[上一页](disabling-actions-during-animation-vb.md)
> [下一页](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="90a26-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
