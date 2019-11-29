---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: 从不带 UpdatePanel 的弹出控件处理回发（C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 当在 su 中发生回发时 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598730"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="6ab17-104">使用没有 UpdatePanel 的弹出控件处理回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="6ab17-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>

<span data-ttu-id="6ab17-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6ab17-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6ab17-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6ab17-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="6ab17-107">AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6ab17-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="6ab17-108">如果在这种面板中发生回发，并且页面上有多个面板，则很难确定单击了哪个面板。</span><span class="sxs-lookup"><span data-stu-id="6ab17-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="6ab17-109">概述</span><span class="sxs-lookup"><span data-stu-id="6ab17-109">Overview</span></span>

<span data-ttu-id="6ab17-110">AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6ab17-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="6ab17-111">如果在这种面板中发生回发，并且页面上有多个面板，则很难确定单击了哪个面板。</span><span class="sxs-lookup"><span data-stu-id="6ab17-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="6ab17-112">步骤</span><span class="sxs-lookup"><span data-stu-id="6ab17-112">Steps</span></span>

<span data-ttu-id="6ab17-113">将 `PopupControl` 与回发一起使用时，如果没有在页面上 `UpdatePanel`，则控制工具包不会提供一种方法来确定哪些客户端元素触发了弹出窗口，进而导致回发。</span><span class="sxs-lookup"><span data-stu-id="6ab17-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="6ab17-114">不过，小型技巧为此方案提供了解决方法。</span><span class="sxs-lookup"><span data-stu-id="6ab17-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="6ab17-115">首先，这是基本设置：两个文本框，两个文本框都触发同一 popup，即一个日历。</span><span class="sxs-lookup"><span data-stu-id="6ab17-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="6ab17-116">两 `PopupControlExtenders` 将文本框和弹出窗口一起显示。</span><span class="sxs-lookup"><span data-stu-id="6ab17-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="6ab17-117">基本思路是在 &lt;`form`&gt; 元素中添加一个隐藏的窗体字段，该元素包含启动弹出窗口的文本框：</span><span class="sxs-lookup"><span data-stu-id="6ab17-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="6ab17-118">加载页面时，JavaScript 代码会将事件处理程序添加到这两个文本框：每当用户单击文本框时，其名称将写入隐藏的窗体字段：</span><span class="sxs-lookup"><span data-stu-id="6ab17-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="6ab17-119">在服务器端代码中，必须读取隐藏字段的值。</span><span class="sxs-lookup"><span data-stu-id="6ab17-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="6ab17-120">由于隐藏的窗体字段是很简单的操作，因此需要使用白名单方法来验证隐藏的值。</span><span class="sxs-lookup"><span data-stu-id="6ab17-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="6ab17-121">标识正确的文本框后，会将日历中的日期写入该文本框。</span><span class="sxs-lookup"><span data-stu-id="6ab17-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

<span data-ttu-id="6ab17-122">[当用户单击文本框时，将显示日历 ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6ab17-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="6ab17-123">当用户在文本框中单击时，将显示该日历（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="6ab17-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>

<span data-ttu-id="6ab17-124">[![单击日期会将其放在文本框中。](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6ab17-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="6ab17-125">单击某个日期会将其放在文本框中（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="6ab17-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6ab17-126">[上一页](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [下一页](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6ab17-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
