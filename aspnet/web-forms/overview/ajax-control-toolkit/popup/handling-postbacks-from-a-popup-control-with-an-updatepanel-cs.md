---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: 使用 UpdatePanel （C#）从 Popup 控件处理回发Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 需要特别小心 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496664"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a><span data-ttu-id="609fc-104">使用带 UpdatePanel 的弹出控件处理回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="609fc-104">Handling Postbacks from A Popup Control With an UpdatePanel (C#)</span></span>

<span data-ttu-id="609fc-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="609fc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="609fc-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="609fc-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span></span>

> <span data-ttu-id="609fc-107">AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="609fc-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="609fc-108">在此类弹出窗口中发生回发时，必须特别小心。</span><span class="sxs-lookup"><span data-stu-id="609fc-108">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="overview"></a><span data-ttu-id="609fc-109">概述</span><span class="sxs-lookup"><span data-stu-id="609fc-109">Overview</span></span>

<span data-ttu-id="609fc-110">AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="609fc-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="609fc-111">在此类弹出窗口中发生回发时，必须特别小心。</span><span class="sxs-lookup"><span data-stu-id="609fc-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="609fc-112">步骤</span><span class="sxs-lookup"><span data-stu-id="609fc-112">Steps</span></span>

<span data-ttu-id="609fc-113">将 `PopupControl` 与回发一起使用时，`UpdatePanel` 可以防止由回发导致的页刷新。</span><span class="sxs-lookup"><span data-stu-id="609fc-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="609fc-114">以下标记定义了几个重要元素：</span><span class="sxs-lookup"><span data-stu-id="609fc-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="609fc-115">`ScriptManager` 控件以便 ASP.NET AJAX 控件工具包工作</span><span class="sxs-lookup"><span data-stu-id="609fc-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="609fc-116">两个 `TextBox` 的控件，它们都将触发弹出窗口</span><span class="sxs-lookup"><span data-stu-id="609fc-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="609fc-117">将用作弹出窗口的 `Panel` 控件</span><span class="sxs-lookup"><span data-stu-id="609fc-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="609fc-118">在面板中，`Calendar` 控件嵌入 `UpdatePanel` 控件中</span><span class="sxs-lookup"><span data-stu-id="609fc-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="609fc-119">两个将面板分配给文本框的 `PopupControlExtender` 控件</span><span class="sxs-lookup"><span data-stu-id="609fc-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="609fc-120">请注意，将设置 `Calendar` 控件的 `OnSelectionChanged` 属性。</span><span class="sxs-lookup"><span data-stu-id="609fc-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="609fc-121">因此，当用户选择日历中的日期时，将发生回发并执行服务器端方法 `c1_SelectionChanged()`。</span><span class="sxs-lookup"><span data-stu-id="609fc-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="609fc-122">在该方法中，必须检索当前日期并将其写回文本框。</span><span class="sxs-lookup"><span data-stu-id="609fc-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="609fc-123">的语法如下所示：首先，必须为页上的 `PopupControlExtender` 生成代理对象。</span><span class="sxs-lookup"><span data-stu-id="609fc-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="609fc-124">ASP.NET AJAX 控件工具包提供 `GetProxyForCurrentPopup()` 方法。</span><span class="sxs-lookup"><span data-stu-id="609fc-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="609fc-125">此方法返回的对象支持 `Commit()` 方法，该方法将值发送回触发弹出窗口的控件（而不是触发方法调用的控件！）。</span><span class="sxs-lookup"><span data-stu-id="609fc-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="609fc-126">下面的代码将所选日期提供为 `Commit()` 方法的参数，从而使代码将所选日期写回文本框：</span><span class="sxs-lookup"><span data-stu-id="609fc-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="609fc-127">现在，只要单击日历日期，所选日期就会显示在关联的文本框中，创建当前可以在许多网站上找到的日期选取器控件。</span><span class="sxs-lookup"><span data-stu-id="609fc-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>

<span data-ttu-id="609fc-128">[当用户单击文本框时，将显示日历 ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="609fc-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="609fc-129">当用户在文本框中单击时，将显示该日历（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="609fc-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="609fc-130">[![单击日期会将其放在文本框中。](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="609fc-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="609fc-131">单击某个日期会将其放在文本框中（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="609fc-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="609fc-132">[上一页](using-multiple-popup-controls-cs.md)
> [下一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span><span class="sxs-lookup"><span data-stu-id="609fc-132">[Previous](using-multiple-popup-controls-cs.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span></span>
