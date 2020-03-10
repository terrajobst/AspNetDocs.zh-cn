---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 使用客户端代码执行动画（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画执行 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484004"
---
# <a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="1d174-104">使用客户端代码执行动画 (VB)</span><span class="sxs-lookup"><span data-stu-id="1d174-104">Executing Animations Using Client-Side Code (VB)</span></span>

<span data-ttu-id="1d174-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1d174-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1d174-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1d174-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="1d174-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="1d174-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1d174-108">还可以使用自定义客户端 JavaScript 代码触发动画的执行。</span><span class="sxs-lookup"><span data-stu-id="1d174-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="1d174-109">概述</span><span class="sxs-lookup"><span data-stu-id="1d174-109">Overview</span></span>

<span data-ttu-id="1d174-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="1d174-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1d174-111">还可以使用自定义客户端 JavaScript 代码触发动画的执行。</span><span class="sxs-lookup"><span data-stu-id="1d174-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="1d174-112">步骤</span><span class="sxs-lookup"><span data-stu-id="1d174-112">Steps</span></span>

<span data-ttu-id="1d174-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="1d174-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="1d174-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d174-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="1d174-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="1d174-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="1d174-116">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="1d174-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="1d174-117">在 "`<Animations>`" 节点中，在用户单击面板后使用 `<OnClick>` 运行动画。</span><span class="sxs-lookup"><span data-stu-id="1d174-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="1d174-118">添加两个要并行执行的动画：</span><span class="sxs-lookup"><span data-stu-id="1d174-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="1d174-119">为了演示这种情况，在页面运行后，将使用 JavaScript 代码执行此动画（以及使用控制工具包创建的任何其他动画）。</span><span class="sxs-lookup"><span data-stu-id="1d174-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="1d174-120">首先，我们需要访问 `AnimationExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="1d174-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="1d174-121">ASP.NET AJAX 库为此任务提供 `$find()` 函数：</span><span class="sxs-lookup"><span data-stu-id="1d174-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="1d174-122">`AnimationExtender` 控件公开一个丰富的 API，其中包含名称与 XML 标记中使用的事件处理程序相同的方法： `OnClick()`、`OnLoad()`等。</span><span class="sxs-lookup"><span data-stu-id="1d174-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="1d174-123">例如，调用 `OnClick()` 方法会在 `AnimationExtender` 控件的 `<OnClick>` 元素内执行动画：</span><span class="sxs-lookup"><span data-stu-id="1d174-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="1d174-124">下面是完整的客户端 JavaScript 代码，该代码在页面完全加载后，将模拟单击面板上的单击，请注意，一旦页面和所有包含的 JavaScript 库加载完毕，ASP.NET AJAX 就会调用 `pageLoad()` 函数名称。</span><span class="sxs-lookup"><span data-stu-id="1d174-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

<span data-ttu-id="1d174-125">[![动画立即运行，而无需鼠标单击](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1d174-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="1d174-126">动画会立即运行，无需鼠标单击（[单击即可查看完全大小的图像](executing-animations-using-client-side-code-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="1d174-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1d174-127">[上一页](modifying-animations-from-the-server-side-vb.md)
> [下一页](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1d174-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
