---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: 调整 DropShadow 的 Z 索引（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 但是，这种阴影有时会与其他控件冲突，(...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 10495a9590ce1f25e9e3fa218ac5144268f50711
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497510"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a><span data-ttu-id="4768d-104">调整 DropShadow 的 Z-索引 (VB)</span><span class="sxs-lookup"><span data-stu-id="4768d-104">Adjusting the Z-Index of a DropShadow (VB)</span></span>

<span data-ttu-id="4768d-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4768d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4768d-106">[下载代码](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4768d-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span></span>

> <span data-ttu-id="4768d-107">AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="4768d-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="4768d-108">但是，这种阴影有时会与其他控件（例如 ASP.NET Menu 控件）冲突。</span><span class="sxs-lookup"><span data-stu-id="4768d-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="4768d-109">弹出菜单项时，它显示在投影的后面。</span><span class="sxs-lookup"><span data-stu-id="4768d-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="4768d-110">概述</span><span class="sxs-lookup"><span data-stu-id="4768d-110">Overview</span></span>

<span data-ttu-id="4768d-111">AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="4768d-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="4768d-112">但是，这种阴影有时会与其他控件（例如 ASP.NET Menu 控件）冲突。</span><span class="sxs-lookup"><span data-stu-id="4768d-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="4768d-113">弹出菜单项时，它显示在投影的后面。</span><span class="sxs-lookup"><span data-stu-id="4768d-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="4768d-114">步骤</span><span class="sxs-lookup"><span data-stu-id="4768d-114">Steps</span></span>

<span data-ttu-id="4768d-115">该代码带有面板本身，其中包含足够的文本，以便面板包含足够文本以使效果可见：</span><span class="sxs-lookup"><span data-stu-id="4768d-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

<span data-ttu-id="4768d-116">另一面板直接放置在 `panelShadow` 面板之前。</span><span class="sxs-lookup"><span data-stu-id="4768d-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="4768d-117">它包含水平方向的菜单，以便菜单项显示在 "`dropShadow`" 面板上（或相反：）：</span><span class="sxs-lookup"><span data-stu-id="4768d-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

<span data-ttu-id="4768d-118">然后，添加 `DropShadowExtender`，以使用投影效果扩展 `panelShadow` 面板：</span><span class="sxs-lookup"><span data-stu-id="4768d-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

<span data-ttu-id="4768d-119">最后，ASP.NET AJAX `ScriptManager` 控件使控件工具包能够正常工作：</span><span class="sxs-lookup"><span data-stu-id="4768d-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

<span data-ttu-id="4768d-120">运行此脚本时，菜单项显示在面板的下方。</span><span class="sxs-lookup"><span data-stu-id="4768d-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="4768d-121">但是，菜单使用 CSS 类 `panel` 其中你只需定义两项内容即可使元素出现在另一个面板前面：</span><span class="sxs-lookup"><span data-stu-id="4768d-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="4768d-122">相对定位</span><span class="sxs-lookup"><span data-stu-id="4768d-122">Relative positioning</span></span>
- <span data-ttu-id="4768d-123">正 z 索引</span><span class="sxs-lookup"><span data-stu-id="4768d-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

<span data-ttu-id="4768d-124">然后，`DropShadowExtender` 控件不会再与 Menu 控件冲突。</span><span class="sxs-lookup"><span data-stu-id="4768d-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="4768d-125">[![之前：菜单项不可见](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4768d-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span></span>

<span data-ttu-id="4768d-126">之前：菜单项不可见（[单击查看完全大小的图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4768d-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span></span>

<span data-ttu-id="4768d-127">[![后：菜单项出现](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4768d-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span></span>

<span data-ttu-id="4768d-128">后：菜单项出现（[单击以查看完全大小的图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="4768d-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4768d-129">[上一页](manipulating-dropshadow-properties-from-client-code-cs.md)
> [下一页](manipulating-dropshadow-properties-from-client-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4768d-129">[Previous](manipulating-dropshadow-properties-from-client-code-cs.md)
[Next](manipulating-dropshadow-properties-from-client-code-vb.md)</span></span>
