---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 使用带有自动回发的滑块控件（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以使滑块 autopost 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445778"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="92496-104">使用带有自动回发的滑块控件（VB）</span><span class="sxs-lookup"><span data-stu-id="92496-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="92496-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="92496-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="92496-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="92496-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="92496-107">AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。</span><span class="sxs-lookup"><span data-stu-id="92496-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="92496-108">它的值更改后，可以使滑块 autopostback。</span><span class="sxs-lookup"><span data-stu-id="92496-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="92496-109">概述</span><span class="sxs-lookup"><span data-stu-id="92496-109">Overview</span></span>

<span data-ttu-id="92496-110">AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。</span><span class="sxs-lookup"><span data-stu-id="92496-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="92496-111">它的值更改后，可以使滑块 autopostback。</span><span class="sxs-lookup"><span data-stu-id="92496-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="92496-112">步骤</span><span class="sxs-lookup"><span data-stu-id="92496-112">Steps</span></span>

<span data-ttu-id="92496-113">为了使滑块在发生更改时自动回发，两个文本框都需要属性 `AutoPostBack="true"`：将成为滑块本身的文本框，以及容纳滑块位置的文本框。</span><span class="sxs-lookup"><span data-stu-id="92496-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="92496-114">下面是所需的标记：</span><span class="sxs-lookup"><span data-stu-id="92496-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="92496-115">ASP.NET AJAX 控件工具包中的 `SliderExtender` 控件将滑块功能分配给这两个文本框：</span><span class="sxs-lookup"><span data-stu-id="92496-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="92496-116">稍后将使用其他 label 元素向用户通知回发：</span><span class="sxs-lookup"><span data-stu-id="92496-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="92496-117">最后，ASP.NET AJAX `ScriptManager` 控件加载所需的 JavaScript，使控件工具包工作正常：</span><span class="sxs-lookup"><span data-stu-id="92496-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="92496-118">现在滑块将回发，在服务器端，可能会捕获并处理此事件：</span><span class="sxs-lookup"><span data-stu-id="92496-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="92496-119">[![移动滑块会触发回发](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="92496-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="92496-120">移动滑块会触发回发（[单击查看完全大小的映像](using-the-slider-control-with-auto-postback-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="92496-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="92496-121">[![之后，此更改的日期将写入标签](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="92496-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="92496-122">之后，此更改的日期将写入标签（[单击查看完全大小的图像](using-the-slider-control-with-auto-postback-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="92496-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="92496-123">[上一页](databinding-the-slider-control-cs.md)
> [下一页](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="92496-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
