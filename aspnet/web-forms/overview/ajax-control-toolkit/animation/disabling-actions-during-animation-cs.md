---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: 在动画过程中禁用C#操作（） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 它还支持操作 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: e91205ad2f9e6ee1fdd869ceb7587c3a82754772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430952"
---
# <a name="disabling-actions-during-animation-c"></a><span data-ttu-id="c04c4-104">动画过程中禁用操作 (C#)</span><span class="sxs-lookup"><span data-stu-id="c04c4-104">Disabling Actions during Animation (C#)</span></span>

<span data-ttu-id="c04c4-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c04c4-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c04c4-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c04c4-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span></span>

> <span data-ttu-id="c04c4-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="c04c4-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c04c4-108">它还支持鼠标单击等操作。</span><span class="sxs-lookup"><span data-stu-id="c04c4-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="c04c4-109">但当鼠标单击开始动画时，最好在动画过程中禁用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="c04c4-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="c04c4-110">概述</span><span class="sxs-lookup"><span data-stu-id="c04c4-110">Overview</span></span>

<span data-ttu-id="c04c4-111">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="c04c4-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c04c4-112">它还支持鼠标单击等操作。</span><span class="sxs-lookup"><span data-stu-id="c04c4-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="c04c4-113">但当鼠标单击开始动画时，最好在动画过程中禁用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="c04c4-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="c04c4-114">步骤</span><span class="sxs-lookup"><span data-stu-id="c04c4-114">Steps</span></span>

<span data-ttu-id="c04c4-115">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="c04c4-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

<span data-ttu-id="c04c4-116">动画将应用于如下所示的 HTML 按钮：</span><span class="sxs-lookup"><span data-stu-id="c04c4-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

<span data-ttu-id="c04c4-117">请注意，使用 HTML 控件而不是 Web 控件，因为我们不希望按钮创建回发;它只应启动客户端动画。</span><span class="sxs-lookup"><span data-stu-id="c04c4-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="c04c4-118">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="c04c4-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

<span data-ttu-id="c04c4-119">在 `<Animations>` "节点中，`<OnClick>` 是用于处理鼠标单击的右元素。</span><span class="sxs-lookup"><span data-stu-id="c04c4-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="c04c4-120">但是，在动画过程中也可以单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="c04c4-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="c04c4-121">`<EnableAction>` 元素可以处理这种情况。</span><span class="sxs-lookup"><span data-stu-id="c04c4-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="c04c4-122">设置 `Enabled="false"` 将在动画中禁用该按钮。</span><span class="sxs-lookup"><span data-stu-id="c04c4-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="c04c4-123">由于我们使用多个单独的动画（禁用按钮和实际动画），因此需要 `<Parallel>` 元素将单个动画一起粘附到其中。</span><span class="sxs-lookup"><span data-stu-id="c04c4-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="c04c4-124">下面是 `AnimationExtender`的完整标记：</span><span class="sxs-lookup"><span data-stu-id="c04c4-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

<span data-ttu-id="c04c4-125">在动画后，还可以使用列表末尾的以下 XML 元素来重新启用按钮：</span><span class="sxs-lookup"><span data-stu-id="c04c4-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

<span data-ttu-id="c04c4-126">但在给定的方案中，这会很无用，因为按钮淡出，在动画结束时不可见。</span><span class="sxs-lookup"><span data-stu-id="c04c4-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="c04c4-127">[![动画运行后，按钮将被禁用](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c04c4-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span></span>

<span data-ttu-id="c04c4-128">动画运行后，该按钮将被禁用（[单击以查看完全大小的图像](disabling-actions-during-animation-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c04c4-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c04c4-129">[上一页](animating-in-response-to-user-interaction-cs.md)
> [下一页](triggering-an-animation-in-another-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c04c4-129">[Previous](animating-in-response-to-user-interaction-cs.md)
[Next](triggering-an-animation-in-another-control-cs.md)</span></span>
