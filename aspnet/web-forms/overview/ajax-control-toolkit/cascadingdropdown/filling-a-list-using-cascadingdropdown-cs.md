---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: 使用 CascadingDropDown （C#）填充列表 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497762"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a><span data-ttu-id="46f51-103">使用 CascadingDropDown 填充列表 (C#)</span><span class="sxs-lookup"><span data-stu-id="46f51-103">Filling a List Using CascadingDropDown (C#)</span></span>

<span data-ttu-id="46f51-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="46f51-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="46f51-105">[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="46f51-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)</span></span>

> <span data-ttu-id="46f51-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="46f51-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="46f51-107">（例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）首先要解决的问题是，使用此控件实际填写下拉列表。</span><span class="sxs-lookup"><span data-stu-id="46f51-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="46f51-108">概述</span><span class="sxs-lookup"><span data-stu-id="46f51-108">Overview</span></span>

<span data-ttu-id="46f51-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="46f51-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="46f51-110">（例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）首先要解决的问题是，使用此控件实际填写下拉列表。</span><span class="sxs-lookup"><span data-stu-id="46f51-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="46f51-111">步骤</span><span class="sxs-lookup"><span data-stu-id="46f51-111">Steps</span></span>

<span data-ttu-id="46f51-112">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="46f51-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="46f51-113">然后，需要 DropDownList 控件：</span><span class="sxs-lookup"><span data-stu-id="46f51-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="46f51-114">在此列表中，将添加 CascadingDropDown 扩展器。</span><span class="sxs-lookup"><span data-stu-id="46f51-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="46f51-115">它将向 web 服务发送一个异步请求，该请求随后将返回要在列表中显示的项的列表。</span><span class="sxs-lookup"><span data-stu-id="46f51-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="46f51-116">为此，需要设置以下 CascadingDropDown 属性：</span><span class="sxs-lookup"><span data-stu-id="46f51-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="46f51-117">`ServicePath`：提供列表项的 web 服务的 URL</span><span class="sxs-lookup"><span data-stu-id="46f51-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="46f51-118">`ServiceMethod`：传递列表项的 Web 方法</span><span class="sxs-lookup"><span data-stu-id="46f51-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="46f51-119">`TargetControlID`：下拉列表的 ID</span><span class="sxs-lookup"><span data-stu-id="46f51-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="46f51-120">`Category`：调用时提交到 web 方法的类别信息</span><span class="sxs-lookup"><span data-stu-id="46f51-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="46f51-121">`PromptText`：从服务器异步加载列表数据时显示的文本</span><span class="sxs-lookup"><span data-stu-id="46f51-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="46f51-122">下面是 `CascadingDropDown` 元素的标记。</span><span class="sxs-lookup"><span data-stu-id="46f51-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="46f51-123">C#和 VB 的唯一区别是关联的 web 服务的名称：</span><span class="sxs-lookup"><span data-stu-id="46f51-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="46f51-124">来自 `CascadingDropDown` 扩展器的 JavaScript 代码调用具有以下签名的 web 服务方法：</span><span class="sxs-lookup"><span data-stu-id="46f51-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="46f51-125">因此，该方法需要返回 `CascadingDropDownNameValue` 类型的数组（由 ASP.NET AJAX 控件工具包定义）。</span><span class="sxs-lookup"><span data-stu-id="46f51-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="46f51-126">在 `CascadingDropDownNameValue` 构造函数中，首先必须提供列表项的文本，然后提供其值，就像 `<option value="VALUE">NAME</option>` 在 HTML 中那样。</span><span class="sxs-lookup"><span data-stu-id="46f51-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="46f51-127">下面是一些示例数据：</span><span class="sxs-lookup"><span data-stu-id="46f51-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="46f51-128">在浏览器中加载页面将触发列表，并将其填充到三个供应商。</span><span class="sxs-lookup"><span data-stu-id="46f51-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="46f51-129">[![自动填充列表](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="46f51-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="46f51-130">将自动填充列表（[单击以查看完全大小的图像](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="46f51-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="46f51-131">下一部分</span><span class="sxs-lookup"><span data-stu-id="46f51-131">Next</span></span>](using-cascadingdropdown-with-a-database-cs.md)
