---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: 通过使用带 UpdatePanel (C#) 的弹出控件处理回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 特别注意必须为其拍摄...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: dff813f0f3e4da26a32fd6305e476d24484e0e7c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415084"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a><span data-ttu-id="5ca71-104">使用带 UpdatePanel 的弹出控件处理回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="5ca71-104">Handling Postbacks from A Popup Control With an UpdatePanel (C#)</span></span>

<span data-ttu-id="5ca71-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5ca71-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5ca71-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5ca71-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span></span>

> <span data-ttu-id="5ca71-107">AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="5ca71-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="5ca71-108">特别留意具有此类弹出窗口中产生的回发时要执行。</span><span class="sxs-lookup"><span data-stu-id="5ca71-108">Special care has to be taken when a postback occurs within such a popup.</span></span>


## <a name="overview"></a><span data-ttu-id="5ca71-109">概述</span><span class="sxs-lookup"><span data-stu-id="5ca71-109">Overview</span></span>

<span data-ttu-id="5ca71-110">AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="5ca71-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="5ca71-111">特别留意具有此类弹出窗口中产生的回发时要执行。</span><span class="sxs-lookup"><span data-stu-id="5ca71-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="5ca71-112">步骤</span><span class="sxs-lookup"><span data-stu-id="5ca71-112">Steps</span></span>

<span data-ttu-id="5ca71-113">使用时`PopupControl`带回发，`UpdatePanel`可以防止引起回发页面刷新。</span><span class="sxs-lookup"><span data-stu-id="5ca71-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="5ca71-114">以下标记定义了几个重要的元素：</span><span class="sxs-lookup"><span data-stu-id="5ca71-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="5ca71-115">一个`ScriptManager`控件，以使 ASP.NET AJAX Control Toolkit 工作原理</span><span class="sxs-lookup"><span data-stu-id="5ca71-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="5ca71-116">两个`TextBox`控件，这将触发一个弹出窗口</span><span class="sxs-lookup"><span data-stu-id="5ca71-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="5ca71-117">一个`Panel`将充当弹出窗口的控件</span><span class="sxs-lookup"><span data-stu-id="5ca71-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="5ca71-118">在面板内`Calendar`内嵌入控件`UpdatePanel`控件</span><span class="sxs-lookup"><span data-stu-id="5ca71-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="5ca71-119">两个`PopupControlExtender`将该面板分配到文本框中的控件</span><span class="sxs-lookup"><span data-stu-id="5ca71-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="5ca71-120">请注意，`OnSelectionChanged`属性的`Calendar`控件设置。</span><span class="sxs-lookup"><span data-stu-id="5ca71-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="5ca71-121">因此当用户选择在日历中的日期，产生的回发和服务器端方法`c1_SelectionChanged()`执行。</span><span class="sxs-lookup"><span data-stu-id="5ca71-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="5ca71-122">在该方法中，必须检索和写回文本框中的当前日期。</span><span class="sxs-lookup"><span data-stu-id="5ca71-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="5ca71-123">为此，语法如下所示：首先，代理对象`PopupControlExtender`页面上必须生成。</span><span class="sxs-lookup"><span data-stu-id="5ca71-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="5ca71-124">ASP.NET AJAX 控件工具包提供了`GetProxyForCurrentPopup()`方法。</span><span class="sxs-lookup"><span data-stu-id="5ca71-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="5ca71-125">此方法返回的对象支持`Commit()`方法可将值发送回控件触发的弹出窗口 （不触发方法调用的控件 ！）。</span><span class="sxs-lookup"><span data-stu-id="5ca71-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="5ca71-126">下面的代码提供的参数作为所选的日期`Commit()`方法，从而导致代码以便将所选的日期写回到文本框中：</span><span class="sxs-lookup"><span data-stu-id="5ca71-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="5ca71-127">现在每当您单击日历日期后，所选的日期将显示在关联的文本框中，创建日期选取器控件的当前可在许多网站上。</span><span class="sxs-lookup"><span data-stu-id="5ca71-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>


[![T<span data-ttu-id="5ca71-128">当用户单击文本框时显示他日历]</span><span class="sxs-lookup"><span data-stu-id="5ca71-128">he Calendar appears when the user clicks into the textbox]</span></span>(handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

<span data-ttu-id="5ca71-129">当用户单击文本框中，将显示日历 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5ca71-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span></span>


[![C<span data-ttu-id="5ca71-130">单击某个日期上会将其放在文本框中]</span><span class="sxs-lookup"><span data-stu-id="5ca71-130">licking on a date puts it in the textbox]</span></span>(handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

<span data-ttu-id="5ca71-131">单击某个日期将其放在文本框中 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5ca71-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5ca71-132">[上一页](using-multiple-popup-controls-cs.md)
> [下一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5ca71-132">[Previous](using-multiple-popup-controls-cs.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span></span>
