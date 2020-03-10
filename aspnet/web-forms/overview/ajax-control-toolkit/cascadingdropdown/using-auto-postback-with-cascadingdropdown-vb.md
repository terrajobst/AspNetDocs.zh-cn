---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: 通过 CascadingDropDown 使用自动回发（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430658"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a><span data-ttu-id="b13cc-103">通过 CascadingDropDown 使用自动回发 (VB)</span><span class="sxs-lookup"><span data-stu-id="b13cc-103">Using Auto-Postback with CascadingDropDown (VB)</span></span>

<span data-ttu-id="b13cc-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b13cc-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b13cc-105">[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b13cc-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span></span>

> <span data-ttu-id="b13cc-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="b13cc-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="b13cc-107">但是，在使用 CascadingDropDown 控件时，ASP。NET 的 DropDownList 控件的 AutoPostBack 功能不起作用，因为以异步方式将数据加载到列表中会生成（不必要的）回发本身。</span><span class="sxs-lookup"><span data-stu-id="b13cc-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="b13cc-108">利用一些 JavaScript 代码，可以避免这种影响。</span><span class="sxs-lookup"><span data-stu-id="b13cc-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="b13cc-109">概述</span><span class="sxs-lookup"><span data-stu-id="b13cc-109">Overview</span></span>

<span data-ttu-id="b13cc-110">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="b13cc-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="b13cc-111">（例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）但是，在使用 CascadingDropDown 控件时，ASP。NET 的 DropDownList 控件的 AutoPostBack 功能不起作用，因为以异步方式将数据加载到列表中会生成（不必要的）回发本身。</span><span class="sxs-lookup"><span data-stu-id="b13cc-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="b13cc-112">利用一些 JavaScript 代码，可以避免这种影响。</span><span class="sxs-lookup"><span data-stu-id="b13cc-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="b13cc-113">步骤</span><span class="sxs-lookup"><span data-stu-id="b13cc-113">Steps</span></span>

<span data-ttu-id="b13cc-114">若要激活 ASP.NET AJAX 和控件工具包的功能，`ScriptManager` 控件必须置于页面上的任何位置（但在 &lt;`form`&gt; 元素中）：</span><span class="sxs-lookup"><span data-stu-id="b13cc-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="b13cc-115">然后，需要 DropDownList 控件：</span><span class="sxs-lookup"><span data-stu-id="b13cc-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="b13cc-116">在此列表中，添加了一个 CascadingDropDown 扩展程序，提供了 web 服务 URL 和方法信息：</span><span class="sxs-lookup"><span data-stu-id="b13cc-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="b13cc-117">然后，CascadingDropDown 扩展器使用以下方法签名异步调用 web 服务：</span><span class="sxs-lookup"><span data-stu-id="b13cc-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="b13cc-118">方法返回类型为 CascadingDropDown 的数组。</span><span class="sxs-lookup"><span data-stu-id="b13cc-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="b13cc-119">类型的构造函数首先需要列表项的标题，然后需要值（HTML `value` 特性）。</span><span class="sxs-lookup"><span data-stu-id="b13cc-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="b13cc-120">在浏览器中加载页面将在下拉列表中填充三个供应商，第二个供应商正在预选择。</span><span class="sxs-lookup"><span data-stu-id="b13cc-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="b13cc-121">此外，ASP.NET 还定义了 `__doPostBack()` JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="b13cc-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="b13cc-122">加载页面后，此 JavaScript 调用会添加到下拉列表中，但仅当其中有元素时才会出现。</span><span class="sxs-lookup"><span data-stu-id="b13cc-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="b13cc-123">如果列表中没有元素，则说明控件工具包当前正在加载它们，因此 JavaScript 代码使用超时，并在半秒后再次尝试。</span><span class="sxs-lookup"><span data-stu-id="b13cc-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

<span data-ttu-id="b13cc-124">这样，仅当列表中有实际元素并且用户选择一个条目时，才会执行回发。</span><span class="sxs-lookup"><span data-stu-id="b13cc-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="b13cc-125">[选择列表元素 ![导致回发](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b13cc-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="b13cc-126">选择列表元素会导致回发（[单击查看完全大小的映像](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="b13cc-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b13cc-127">上一页</span><span class="sxs-lookup"><span data-stu-id="b13cc-127">Previous</span></span>](presetting-list-entries-with-cascadingdropdown-vb.md)
