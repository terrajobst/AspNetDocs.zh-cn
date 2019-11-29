---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 以响应用户交互的动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画可以是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607034"
---
# <a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="7467a-104">响应用户交互的动画 (VB)</span><span class="sxs-lookup"><span data-stu-id="7467a-104">Animating in Response To User Interaction (VB)</span></span>

<span data-ttu-id="7467a-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7467a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7467a-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7467a-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="7467a-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="7467a-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7467a-108">动画可以自动启动，也可以由用户交互触发，例如通过单击鼠标。</span><span class="sxs-lookup"><span data-stu-id="7467a-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="7467a-109">概述</span><span class="sxs-lookup"><span data-stu-id="7467a-109">Overview</span></span>

<span data-ttu-id="7467a-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="7467a-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7467a-111">动画可以自动启动，也可以由用户交互触发，例如通过单击鼠标。</span><span class="sxs-lookup"><span data-stu-id="7467a-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="7467a-112">步骤</span><span class="sxs-lookup"><span data-stu-id="7467a-112">Steps</span></span>

<span data-ttu-id="7467a-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="7467a-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="7467a-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7467a-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="7467a-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="7467a-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="7467a-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="7467a-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="7467a-117">在 "`<Animations>`" 节点中，有五种方法可通过用户交互启动动画（缺少的元素 `<OnLoad>` 在整个页面完全加载后执行）：</span><span class="sxs-lookup"><span data-stu-id="7467a-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="7467a-118">`<OnClick>` （鼠标单击控件）</span><span class="sxs-lookup"><span data-stu-id="7467a-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="7467a-119">`<OnHoverOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="7467a-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="7467a-120">`<OnHoverOver>` （将鼠标悬停在控件上，停止 `<OnHoverOut>` 动画）</span><span class="sxs-lookup"><span data-stu-id="7467a-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="7467a-121">`<OnMouseOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="7467a-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="7467a-122">`<OnMouseOver>` （将鼠标悬停在控件上，而不是停止 `<OnMouseOut>` 动画）</span><span class="sxs-lookup"><span data-stu-id="7467a-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="7467a-123">在这种情况下，将使用 `<OnClick>`。</span><span class="sxs-lookup"><span data-stu-id="7467a-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="7467a-124">用户单击面板时，将同时调整其大小并淡出。</span><span class="sxs-lookup"><span data-stu-id="7467a-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

<span data-ttu-id="7467a-125">[![鼠标单击开始动画](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7467a-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="7467a-126">鼠标单击开始动画（[单击查看完全大小的图像](animating-in-response-to-user-interaction-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="7467a-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7467a-127">[上一页](picking-one-animation-out-of-a-list-vb.md)
> [下一页](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7467a-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
