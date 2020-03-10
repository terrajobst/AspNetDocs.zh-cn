---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: 从 JavaScript 折叠和展开面板（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展了面板，使其能够折叠其内容并将其展开 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: aa9779c65fb587193dbabde55cc6900283ce239d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430592"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a><span data-ttu-id="fd591-103">通过 JavaScript 折叠和展开面板 (VB)</span><span class="sxs-lookup"><span data-stu-id="fd591-103">Collapsing and Expanding a Panel from JavaScript (VB)</span></span>

<span data-ttu-id="fd591-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fd591-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fd591-105">[下载代码](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fd591-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span></span>

> <span data-ttu-id="fd591-106">ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展了面板，使其能够折叠其内容并再次展开。</span><span class="sxs-lookup"><span data-stu-id="fd591-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="fd591-107">也可以通过自定义 JavaScript 代码触发这两个操作。</span><span class="sxs-lookup"><span data-stu-id="fd591-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="fd591-108">概述</span><span class="sxs-lookup"><span data-stu-id="fd591-108">Overview</span></span>

<span data-ttu-id="fd591-109">ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展了面板，使其能够折叠其内容并再次展开。</span><span class="sxs-lookup"><span data-stu-id="fd591-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="fd591-110">也可以通过自定义 JavaScript 代码触发这两个操作。</span><span class="sxs-lookup"><span data-stu-id="fd591-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="fd591-111">步骤</span><span class="sxs-lookup"><span data-stu-id="fd591-111">Steps</span></span>

<span data-ttu-id="fd591-112">首先，创建一个新的 ASP.NET 页面，并在一个 `<form>` 元素中包含 `ScriptManager`。</span><span class="sxs-lookup"><span data-stu-id="fd591-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="fd591-113">这会加载控件工具包所需的 ASP.NET AJAX 库：</span><span class="sxs-lookup"><span data-stu-id="fd591-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="fd591-114">然后，创建一个带有一些文本的面板，以便可以查看折叠/展开效果：</span><span class="sxs-lookup"><span data-stu-id="fd591-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="fd591-115">如您所见，该面板引用了此处显示的 CSS 类（基本上定义了背景颜色和面板的宽度）：</span><span class="sxs-lookup"><span data-stu-id="fd591-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

<span data-ttu-id="fd591-116">`CollapsiblePanelExtender` 控件需要 `TargetControlID` 属性，以便该工具包知道在请求时折叠或展开哪个面板：</span><span class="sxs-lookup"><span data-stu-id="fd591-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

<span data-ttu-id="fd591-117">遗憾的是，扩展器当前未公开用于折叠或展开面板的特定 API，但某些未记录的方法将执行此操作。</span><span class="sxs-lookup"><span data-stu-id="fd591-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="fd591-118">首先，将三个 HTML 按钮添加到页面，随后会触发客户端 JavaScript 以折叠或展开面板的内容：</span><span class="sxs-lookup"><span data-stu-id="fd591-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="fd591-119">在客户端 JavaScript 代码中（从 `<script type="text/javascript">`开始），需要使用 `$find()` 方法来访问 `CollapsiblePanelExtender`。</span><span class="sxs-lookup"><span data-stu-id="fd591-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="fd591-120">`$find("cpe")` 将返回对它的引用。</span><span class="sxs-lookup"><span data-stu-id="fd591-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="fd591-121">从这里开始，特定的方法可解决现有的任务。</span><span class="sxs-lookup"><span data-stu-id="fd591-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="fd591-122">用于打开（展开）面板的方法称为 `_doOpen()`;下面的代码实现单击第一个按钮时调用的 `doOpen()` 函数：</span><span class="sxs-lookup"><span data-stu-id="fd591-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

<span data-ttu-id="fd591-123">若要关闭或折叠面板，需要执行 `_doClose()` 方法。</span><span class="sxs-lookup"><span data-stu-id="fd591-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="fd591-124">因此，当用户单击第二个按钮时，将调用以下 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="fd591-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

<span data-ttu-id="fd591-125">第三个按钮切换面板的状态：从折叠展开为展开状态，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="fd591-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="fd591-126">`CollapsiblePanelExtender` 公开 `toggle()` 方法，该方法执行的操作完全正确：反转面板的状态。</span><span class="sxs-lookup"><span data-stu-id="fd591-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="fd591-127">但还有另一种方法（由 `toggle()` 方法在内部使用）： `CollapsiblePanelExtender()` 的 `get_Collapsed()` 方法告诉我们面板是否折叠。</span><span class="sxs-lookup"><span data-stu-id="fd591-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="fd591-128">根据此函数的返回值，将面板展开（`_doOpen()` 方法）或折叠（`_doClose()`）方法：</span><span class="sxs-lookup"><span data-stu-id="fd591-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

<span data-ttu-id="fd591-129">[第三个按钮 ![更改面板的状态：从折叠到已展开并返回](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fd591-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="fd591-130">第三个按钮更改面板的状态：从折叠到展开和后退（[单击以查看完全大小的图像](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="fd591-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fd591-131">上一页</span><span class="sxs-lookup"><span data-stu-id="fd591-131">Previous</span></span>](collapsing-and-expanding-a-panel-from-javascript-cs.md)
