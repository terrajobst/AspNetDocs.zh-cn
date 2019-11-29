---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 数据绑定滑块控件（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以绑定当前的 positio 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598298"
---
# <a name="databinding-the-slider-control-vb"></a><span data-ttu-id="16bcc-104">数据绑定滑块控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="16bcc-104">Databinding the Slider Control (VB)</span></span>

<span data-ttu-id="16bcc-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="16bcc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="16bcc-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="16bcc-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="16bcc-107">AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。</span><span class="sxs-lookup"><span data-stu-id="16bcc-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="16bcc-108">可以将滑块的当前位置绑定到另一个 ASP.NET 控件。</span><span class="sxs-lookup"><span data-stu-id="16bcc-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="16bcc-109">概述</span><span class="sxs-lookup"><span data-stu-id="16bcc-109">Overview</span></span>

<span data-ttu-id="16bcc-110">AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。</span><span class="sxs-lookup"><span data-stu-id="16bcc-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="16bcc-111">可以将滑块的当前位置绑定到另一个 ASP.NET 控件。</span><span class="sxs-lookup"><span data-stu-id="16bcc-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="16bcc-112">步骤</span><span class="sxs-lookup"><span data-stu-id="16bcc-112">Steps</span></span>

<span data-ttu-id="16bcc-113">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="16bcc-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="16bcc-114">接下来，向页面添加两个 `TextBox` 控件。</span><span class="sxs-lookup"><span data-stu-id="16bcc-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="16bcc-115">一个将转换为图形滑块，另一个将保存滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="16bcc-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="16bcc-116">下一步已经是最后一步。</span><span class="sxs-lookup"><span data-stu-id="16bcc-116">The next step is already the final step.</span></span> <span data-ttu-id="16bcc-117">ASP.NET AJAX 控件工具包中的 `SliderExtender` 控件将从第一个文本框中创建一个滑块，并在滑块位置改变时自动更新第二个文本框。</span><span class="sxs-lookup"><span data-stu-id="16bcc-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="16bcc-118">为了使其正常工作，必须将 `SliderExtender`的 `TargetControlID` 属性设置为第一个文本框的 ID;`BoundControlID` 特性必须设置为第二个文本框的 ID。</span><span class="sxs-lookup"><span data-stu-id="16bcc-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="16bcc-119">正如您在浏览器中所看到的那样，数据绑定在这两个方向上都是这样的：在文本框中输入新值可更新滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="16bcc-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="16bcc-120">如果将第二个文本框设置为只读，则可以向文本字段添加弱保护，使用户更难手动更新其中的值。</span><span class="sxs-lookup"><span data-stu-id="16bcc-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="16bcc-121">[![滑块和文本框处于同步](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="16bcc-121">[![Slider and text box are in sync](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="16bcc-122">滑块和文本框处于同步（[单击以查看完全大小的图像](databinding-the-slider-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="16bcc-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="16bcc-123">上一部分</span><span class="sxs-lookup"><span data-stu-id="16bcc-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
