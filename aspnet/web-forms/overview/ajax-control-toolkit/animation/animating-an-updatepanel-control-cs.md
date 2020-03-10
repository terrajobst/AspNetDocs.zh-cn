---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 对 UpdatePanel 控件（C#）进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 有关 ... 的内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431048"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="1779d-104">对 UpdatePanel 控件执行动画处理 (C#)</span><span class="sxs-lookup"><span data-stu-id="1779d-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="1779d-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1779d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1779d-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1779d-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="1779d-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="1779d-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1779d-108">对于 UpdatePanel 的内容，存在大量依赖于动画框架的特殊扩展器： UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="1779d-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="1779d-109">本教程演示如何为 UpdatePanel 设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="1779d-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="1779d-110">概述</span><span class="sxs-lookup"><span data-stu-id="1779d-110">Overview</span></span>

<span data-ttu-id="1779d-111">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="1779d-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1779d-112">对于 `UpdatePanel`的内容，存在大量依赖于动画框架的特殊扩展器： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="1779d-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="1779d-113">本教程演示如何为 `UpdatePanel`设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="1779d-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="1779d-114">步骤</span><span class="sxs-lookup"><span data-stu-id="1779d-114">Steps</span></span>

<span data-ttu-id="1779d-115">第一步通常是将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：</span><span class="sxs-lookup"><span data-stu-id="1779d-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="1779d-116">此方案中的动画将应用到驻留在 `UpdatePanel`中的 ASP.NET `Wizard` web 控件。</span><span class="sxs-lookup"><span data-stu-id="1779d-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="1779d-117">三个（任意）步骤提供了足够的选项来触发回发：</span><span class="sxs-lookup"><span data-stu-id="1779d-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="1779d-118">`UpdatePanelAnimationExtender` 控件所需的标记与用于 `AnimationExtender`的标记非常类似。</span><span class="sxs-lookup"><span data-stu-id="1779d-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="1779d-119">在 `TargetControlID` 特性中，我们提供了要进行动画处理的 `UpdatePanel` `ID`;在 `UpdatePanelAnimationExtender` 控件内，`<Animations>` 元素保存动画的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="1779d-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="1779d-120">但有一个差异：与 `AnimationExtender`相比，事件和事件处理程序的数量受到限制。</span><span class="sxs-lookup"><span data-stu-id="1779d-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="1779d-121">对于 `UpdatePanels`，只存在其中的两个：</span><span class="sxs-lookup"><span data-stu-id="1779d-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="1779d-122">更新 UpdatePanel 后 `<OnUpdated>`</span><span class="sxs-lookup"><span data-stu-id="1779d-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="1779d-123">当 UpdatePanel 开始更新时 `<OnUpdating>`</span><span class="sxs-lookup"><span data-stu-id="1779d-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="1779d-124">在此方案中，`UpdatePanel` 的新内容（在回发之后）应淡入。</span><span class="sxs-lookup"><span data-stu-id="1779d-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="1779d-125">这是所需的标记：</span><span class="sxs-lookup"><span data-stu-id="1779d-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="1779d-126">现在，每当在 UpdatePanel 内发生回发时，面板的新内容就会平稳地淡化。</span><span class="sxs-lookup"><span data-stu-id="1779d-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="1779d-127">[![下一个向导步骤淡入](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1779d-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="1779d-128">下一个向导步骤淡入（[单击查看完全大小的图像](animating-an-updatepanel-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="1779d-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1779d-129">[上一页](changing-an-animation-using-client-side-code-cs.md)
> [下一页](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1779d-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
