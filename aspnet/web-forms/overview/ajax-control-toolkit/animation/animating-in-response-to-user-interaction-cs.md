---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 针对用户交互（C#）响应进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画可以是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497900"
---
# <a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="448dc-104">响应用户交互的动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="448dc-104">Animating in Response To User Interaction (C#)</span></span>

<span data-ttu-id="448dc-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="448dc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="448dc-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="448dc-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="448dc-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="448dc-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="448dc-108">动画可以自动启动，也可以由用户交互触发，例如通过单击鼠标。</span><span class="sxs-lookup"><span data-stu-id="448dc-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="448dc-109">概述</span><span class="sxs-lookup"><span data-stu-id="448dc-109">Overview</span></span>

<span data-ttu-id="448dc-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="448dc-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="448dc-111">动画可以自动启动，也可以由用户交互触发，例如通过单击鼠标。</span><span class="sxs-lookup"><span data-stu-id="448dc-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="448dc-112">步骤</span><span class="sxs-lookup"><span data-stu-id="448dc-112">Steps</span></span>

<span data-ttu-id="448dc-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="448dc-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="448dc-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="448dc-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="448dc-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="448dc-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="448dc-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="448dc-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="448dc-117">在 "`<Animations>`" 节点中，有五种方法可通过用户交互启动动画（缺少的元素 `<OnLoad>` 在整个页面完全加载后执行）：</span><span class="sxs-lookup"><span data-stu-id="448dc-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="448dc-118">`<OnClick>` （鼠标单击控件）</span><span class="sxs-lookup"><span data-stu-id="448dc-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="448dc-119">`<OnHoverOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="448dc-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="448dc-120">`<OnHoverOver>` （将鼠标悬停在控件上，停止 `<OnHoverOut>` 动画）</span><span class="sxs-lookup"><span data-stu-id="448dc-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="448dc-121">`<OnMouseOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="448dc-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="448dc-122">`<OnMouseOver>` （将鼠标悬停在控件上，而不是停止 `<OnMouseOut>` 动画）</span><span class="sxs-lookup"><span data-stu-id="448dc-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="448dc-123">在这种情况下，将使用 `<OnClick>`。</span><span class="sxs-lookup"><span data-stu-id="448dc-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="448dc-124">用户单击面板时，将同时调整其大小并淡出。</span><span class="sxs-lookup"><span data-stu-id="448dc-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

<span data-ttu-id="448dc-125">[![鼠标单击开始动画](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="448dc-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="448dc-126">鼠标单击开始动画（[单击查看完全大小的图像](animating-in-response-to-user-interaction-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="448dc-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="448dc-127">[上一页](picking-one-animation-out-of-a-list-cs.md)
> [下一页](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="448dc-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
