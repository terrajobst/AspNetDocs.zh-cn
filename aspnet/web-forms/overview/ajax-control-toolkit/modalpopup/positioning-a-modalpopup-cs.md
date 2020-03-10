---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: 定位 ModalPopup （C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但是，控件不提供 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 8034f5aeb5a1a80f1ea8cbc9d638f3dfb1a38706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496916"
---
# <a name="positioning-a-modalpopup-c"></a><span data-ttu-id="aa373-104">定位 ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="aa373-104">Positioning a ModalPopup (C#)</span></span>

<span data-ttu-id="aa373-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="aa373-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="aa373-106">[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="aa373-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="aa373-107">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="aa373-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="aa373-108">但是，控件不提供用于定位 popup 的内置功能。</span><span class="sxs-lookup"><span data-stu-id="aa373-108">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="aa373-109">概述</span><span class="sxs-lookup"><span data-stu-id="aa373-109">Overview</span></span>

<span data-ttu-id="aa373-110">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="aa373-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="aa373-111">但是，控件不提供用于定位 popup 的内置功能。</span><span class="sxs-lookup"><span data-stu-id="aa373-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="aa373-112">步骤</span><span class="sxs-lookup"><span data-stu-id="aa373-112">Steps</span></span>

<span data-ttu-id="aa373-113">为了激活 ASP.NET AJAX 和控件工具包的功能，`ScriptManager`。</span><span class="sxs-lookup"><span data-stu-id="aa373-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="aa373-114">控件必须置于页面上的任何位置（但位于 `<form>` 元素内）：</span><span class="sxs-lookup"><span data-stu-id="aa373-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="aa373-115">接下来，添加一个用于模式弹出窗口的面板。</span><span class="sxs-lookup"><span data-stu-id="aa373-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="aa373-116">按钮用于关闭弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="aa373-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="aa373-117">每当显示弹出窗口时，它都应定位在页面中的某个位置。</span><span class="sxs-lookup"><span data-stu-id="aa373-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="aa373-118">对于此任务，将创建客户端 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="aa373-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="aa373-119">它首先尝试访问面板。</span><span class="sxs-lookup"><span data-stu-id="aa373-119">It first tries to access the panel.</span></span> <span data-ttu-id="aa373-120">如果成功，则使用 CSS 和 JavaScript 设置面板的位置（将 popup 的位置更改为）。</span><span class="sxs-lookup"><span data-stu-id="aa373-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="aa373-121">但 `ModalPopupExtender` 控件也会尝试定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="aa373-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="aa373-122">因此，JavaScript 代码会重复定位 popup，每10秒一次。</span><span class="sxs-lookup"><span data-stu-id="aa373-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="aa373-123">正如您所看到的，`setTimeout()` JavaScript 方法的返回值保存在全局变量中。</span><span class="sxs-lookup"><span data-stu-id="aa373-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="aa373-124">这允许使用 `clearTimeout()` 方法，按需停止快捷方式的重复定位：</span><span class="sxs-lookup"><span data-stu-id="aa373-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="aa373-125">现在，剩下的就是让浏览器在适当的时候调用这些函数。</span><span class="sxs-lookup"><span data-stu-id="aa373-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="aa373-126">当单击触发面板的按钮时，必须调用 `movePanel()` JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="aa373-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="aa373-127">当弹出窗口关闭时，`stopMoving()` 函数便会开始播放，此操作可在 `ModalPopupExtender` 控件中触发：</span><span class="sxs-lookup"><span data-stu-id="aa373-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]

<span data-ttu-id="aa373-128">[![在指定位置显示模式弹出窗口](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="aa373-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="aa373-129">模式弹出窗口出现在指定位置（[单击以查看完全大小的图像](positioning-a-modalpopup-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="aa373-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aa373-130">[上一页](handling-postbacks-from-a-modalpopup-cs.md)
> [下一页](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="aa373-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>
