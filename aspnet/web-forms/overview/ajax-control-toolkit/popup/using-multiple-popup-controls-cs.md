---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 使用多个 Popup 控件C#（） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 还可以使用 m 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496424"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="a6d46-104">使用多个弹出控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="a6d46-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="a6d46-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a6d46-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a6d46-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a6d46-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="a6d46-107">AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="a6d46-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a6d46-108">还可以在一个页面上使用多个 popup 控件。</span><span class="sxs-lookup"><span data-stu-id="a6d46-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="a6d46-109">概述</span><span class="sxs-lookup"><span data-stu-id="a6d46-109">Overview</span></span>

<span data-ttu-id="a6d46-110">AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="a6d46-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="a6d46-111">还可以在一个页面上使用多个 popup 控件。</span><span class="sxs-lookup"><span data-stu-id="a6d46-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="a6d46-112">步骤</span><span class="sxs-lookup"><span data-stu-id="a6d46-112">Steps</span></span>

<span data-ttu-id="a6d46-113">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="a6d46-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="a6d46-114">接下来，添加一个用作弹出窗口的面板。</span><span class="sxs-lookup"><span data-stu-id="a6d46-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="a6d46-115">在当前情况下，面板包含一个 `Calendar` 控件。</span><span class="sxs-lookup"><span data-stu-id="a6d46-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="a6d46-116">为了避免由日历回发导致的页面刷新，将面板置于 `UpdatePanel` 控件中：</span><span class="sxs-lookup"><span data-stu-id="a6d46-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="a6d46-117">该页还包含两个文本框。</span><span class="sxs-lookup"><span data-stu-id="a6d46-117">The page also contains two text boxes.</span></span> <span data-ttu-id="a6d46-118">对于每个文本框，一旦激活文本框，就会显示 "日历" 弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="a6d46-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="a6d46-119">现在，使用 `PopupControlExtender`扩展两个文本框中的每一个。</span><span class="sxs-lookup"><span data-stu-id="a6d46-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="a6d46-120">`TargetControlID` 属性提供绑定到扩展器的控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="a6d46-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="a6d46-121">`PopupControlID` 属性包含弹出面板的 ID。</span><span class="sxs-lookup"><span data-stu-id="a6d46-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="a6d46-122">在这种情况下，两个扩展器都显示同一个面板，但也可能有不同的面板。</span><span class="sxs-lookup"><span data-stu-id="a6d46-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="a6d46-123">现在只要单击文本字段，就会在字段下方显示一个日历，使您可以选择日期。</span><span class="sxs-lookup"><span data-stu-id="a6d46-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="a6d46-124">（其他教程将介绍如何将所选日期返回到文本框中。）</span><span class="sxs-lookup"><span data-stu-id="a6d46-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="a6d46-125">[当用户单击文本框时，将显示日历 ![](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6d46-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="a6d46-126">当用户在文本框中单击时，将显示该日历（[单击以查看完全大小的图像](using-multiple-popup-controls-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a6d46-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a6d46-127">下一部分</span><span class="sxs-lookup"><span data-stu-id="a6d46-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
