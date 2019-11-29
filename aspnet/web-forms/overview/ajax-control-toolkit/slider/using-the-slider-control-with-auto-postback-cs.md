---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 使用带有自动回发（C#）的滑块控件 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。 可以使滑块 autopost 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598415"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="59573-104">使用带有自动回发的滑块控件（C#）</span><span class="sxs-lookup"><span data-stu-id="59573-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="59573-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="59573-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="59573-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="59573-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="59573-107">AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。</span><span class="sxs-lookup"><span data-stu-id="59573-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="59573-108">它的值更改后，可以使滑块 autopostback。</span><span class="sxs-lookup"><span data-stu-id="59573-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="59573-109">概述</span><span class="sxs-lookup"><span data-stu-id="59573-109">Overview</span></span>

<span data-ttu-id="59573-110">AJAX 控件工具包中的滑块控件提供可使用鼠标控制的图形滑块。</span><span class="sxs-lookup"><span data-stu-id="59573-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="59573-111">它的值更改后，可以使滑块 autopostback。</span><span class="sxs-lookup"><span data-stu-id="59573-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="59573-112">步骤</span><span class="sxs-lookup"><span data-stu-id="59573-112">Steps</span></span>

<span data-ttu-id="59573-113">为了使滑块在发生更改时自动回发，两个文本框都需要属性 `AutoPostBack="true"`：将成为滑块本身的文本框，以及容纳滑块位置的文本框。</span><span class="sxs-lookup"><span data-stu-id="59573-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="59573-114">下面是所需的标记：</span><span class="sxs-lookup"><span data-stu-id="59573-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="59573-115">ASP.NET AJAX 控件工具包中的 `SliderExtender` 控件将滑块功能分配给这两个文本框：</span><span class="sxs-lookup"><span data-stu-id="59573-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="59573-116">稍后将使用其他 label 元素向用户通知回发：</span><span class="sxs-lookup"><span data-stu-id="59573-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="59573-117">最后，ASP.NET AJAX `ScriptManager` 控件加载所需的 JavaScript，使控件工具包工作正常：</span><span class="sxs-lookup"><span data-stu-id="59573-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="59573-118">现在滑块将回发，在服务器端，可能会捕获并处理此事件：</span><span class="sxs-lookup"><span data-stu-id="59573-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="59573-119">[![移动滑块会触发回发](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="59573-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="59573-120">移动滑块会触发回发（[单击查看完全大小的映像](using-the-slider-control-with-auto-postback-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="59573-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="59573-121">[![之后，此更改的日期将写入标签](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="59573-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="59573-122">之后，此更改的日期将写入标签（[单击查看完全大小的图像](using-the-slider-control-with-auto-postback-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="59573-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="59573-123">下一页</span><span class="sxs-lookup"><span data-stu-id="59573-123">Next</span></span>](databinding-the-slider-control-cs.md)
