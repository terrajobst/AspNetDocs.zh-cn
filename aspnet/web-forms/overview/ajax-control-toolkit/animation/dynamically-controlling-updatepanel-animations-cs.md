---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: 动态控制 UpdatePanel 动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 有关 ... 的内容
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606799"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="67109-104">动态控制 UpdatePanel 动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="67109-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="67109-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="67109-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="67109-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="67109-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="67109-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="67109-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="67109-108">对于 UpdatePanel 的内容，存在大量依赖于动画框架的特殊扩展器： UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="67109-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="67109-109">它还可以与 UpdatePanel 触发器一起使用。</span><span class="sxs-lookup"><span data-stu-id="67109-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="67109-110">概述</span><span class="sxs-lookup"><span data-stu-id="67109-110">Overview</span></span>

<span data-ttu-id="67109-111">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="67109-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="67109-112">对于 `UpdatePanel`的内容，存在大量依赖于动画框架的特殊扩展器： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="67109-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="67109-113">它还可以与 `UpdatePanel` 触发器一起使用。</span><span class="sxs-lookup"><span data-stu-id="67109-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="67109-114">步骤</span><span class="sxs-lookup"><span data-stu-id="67109-114">Steps</span></span>

<span data-ttu-id="67109-115">第一步通常是将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：</span><span class="sxs-lookup"><span data-stu-id="67109-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="67109-116">此方案中的动画将应用于当前时间的显示。</span><span class="sxs-lookup"><span data-stu-id="67109-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="67109-117">可以使用 `Page_Load()` 方法将此信息写入标签，或者（为了简单起见），使用以下内联代码：</span><span class="sxs-lookup"><span data-stu-id="67109-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="67109-118">此外，还会创建用于触发更新时间的按钮：</span><span class="sxs-lookup"><span data-stu-id="67109-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="67109-119">然后，将此代码放入 `UpdatePanel` 元素的 `<ContentTemplate>` 部分。</span><span class="sxs-lookup"><span data-stu-id="67109-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="67109-120">面板的 `UpdateMode` 特性必须设置为 `"Conditional"`，因为只有触发器可以更新面板的内容。</span><span class="sxs-lookup"><span data-stu-id="67109-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="67109-121">在 `UpdatePanel`的 `<Triggers>` 部分，将创建一个异步回发触发器，并将其绑定到按钮的 `Click` 事件。</span><span class="sxs-lookup"><span data-stu-id="67109-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="67109-122">因此，如果用户单击该按钮，则将刷新 `UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="67109-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="67109-123">下面是 `UpdatePanel` 控件的标记：</span><span class="sxs-lookup"><span data-stu-id="67109-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="67109-124">最后，必须配置 `UpdatePanelAnimationExtender`：将 `TargetControlID` 属性设置为面板的 ID，并在扩展器中定义一个动画。</span><span class="sxs-lookup"><span data-stu-id="67109-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="67109-125">淡入非常有意义，这会对更新的时间产生良好的视觉效果。</span><span class="sxs-lookup"><span data-stu-id="67109-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="67109-126">扩展器标记可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="67109-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="67109-127">在浏览器中运行该文件。</span><span class="sxs-lookup"><span data-stu-id="67109-127">Run the file in the browser.</span></span> <span data-ttu-id="67109-128">只要单击该按钮，当前时间就会显示在面板中，在一秒的持续时间内总是淡入。</span><span class="sxs-lookup"><span data-stu-id="67109-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="67109-129">[![当前时间淡入](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="67109-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="67109-130">当前时间已淡入（[单击查看完全大小的图像](dynamically-controlling-updatepanel-animations-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="67109-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="67109-131">[上一页](animating-an-updatepanel-control-cs.md)
> [下一页](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="67109-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
