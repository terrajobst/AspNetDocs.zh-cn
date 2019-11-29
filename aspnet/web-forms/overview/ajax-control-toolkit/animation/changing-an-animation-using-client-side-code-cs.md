---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: 使用客户端代码更改动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画还可以 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606977"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="4d6d9-104">使用客户端代码更改动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="4d6d9-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="4d6d9-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4d6d9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4d6d9-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4d6d9-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="4d6d9-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="4d6d9-108">还可以使用自定义客户端 JavaScript 代码更改动画。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="4d6d9-109">概述</span><span class="sxs-lookup"><span data-stu-id="4d6d9-109">Overview</span></span>

<span data-ttu-id="4d6d9-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="4d6d9-111">还可以使用自定义客户端 JavaScript 代码更改动画。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="4d6d9-112">步骤</span><span class="sxs-lookup"><span data-stu-id="4d6d9-112">Steps</span></span>

<span data-ttu-id="4d6d9-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="4d6d9-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="4d6d9-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="4d6d9-116">实际动画由 HTML 按钮启动：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="4d6d9-117">然后，将 `AnimationExtender` 添加到页面，提供 `ID``TargetControlID` 属性和必备 `runat="server"`：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="4d6d9-118">请注意，`AnimationExtender` 控件中没有 `<Animations>` 的节点。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="4d6d9-119">自定义 JavaScript 代码用于提供与控件一起使用的动画。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="4d6d9-120">与 `AnimationExtender`的服务器 API 一样，尚无简单的方法可以将动画分配到扩展器。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="4d6d9-121">但是，扩展器确实会公开多种方法来读取和写入注册到各种事件的动画（`OnClick`、`OnLoad`等）。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="4d6d9-122">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="4d6d9-123">`get_*()` 函数的返回值的格式和 `set_*()` 函数的参数格式是一个 JSON 字符串，它提供 XML 标记的对象表示形式。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="4d6d9-124">当前无法在中传递对象，但可以从给定动画（`get_OnXXXBehavior()` 方法）中读取对象。</span><span class="sxs-lookup"><span data-stu-id="4d6d9-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="4d6d9-125">下面是一个 JSON 字符串（没有分隔引号并且格式漂亮）表示由按钮触发的动画，但通过调整面板的大小并同时淡化面板来对其进行动画处理：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="4d6d9-126">以下 JavaScript 代码将此 JSON descripting 分配给当前扩展器的 `OnClick` 动画，并运行它：</span><span class="sxs-lookup"><span data-stu-id="4d6d9-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="4d6d9-127">[![动画会立即运行，而无需鼠标单击（且标记极少）](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4d6d9-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="4d6d9-128">动画会立即运行，而无需鼠标单击（并显示很少的标记）（[单击即可查看完全大小的图像](changing-an-animation-using-client-side-code-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4d6d9-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4d6d9-129">[上一页](executing-animations-using-client-side-code-cs.md)
> [下一页](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="4d6d9-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
