---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: 带有 CascadingDropDown （C#）的 Cascadingdropdown 预设置列表项 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb4a51092534e6fddbd40f868c53c58d12eef2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574690"
---
# <a name="presetting-list-entries-with-cascadingdropdown-c"></a><span data-ttu-id="29ba8-103">使用 CascadingDropDown 预设置列表条目 (C#)</span><span class="sxs-lookup"><span data-stu-id="29ba8-103">Presetting List Entries with CascadingDropDown (C#)</span></span>

<span data-ttu-id="29ba8-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="29ba8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="29ba8-105">[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="29ba8-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span></span>

> <span data-ttu-id="29ba8-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="29ba8-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="29ba8-107">使用少量代码，就可以在动态加载数据后预先选择列表元素。</span><span class="sxs-lookup"><span data-stu-id="29ba8-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="29ba8-108">概述</span><span class="sxs-lookup"><span data-stu-id="29ba8-108">Overview</span></span>

<span data-ttu-id="29ba8-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="29ba8-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="29ba8-110">（例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）使用少量代码，就可以在动态加载数据后预先选择列表元素。</span><span class="sxs-lookup"><span data-stu-id="29ba8-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="29ba8-111">步骤</span><span class="sxs-lookup"><span data-stu-id="29ba8-111">Steps</span></span>

<span data-ttu-id="29ba8-112">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="29ba8-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="29ba8-113">然后，需要 DropDownList 控件：</span><span class="sxs-lookup"><span data-stu-id="29ba8-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="29ba8-114">在此列表中，添加了一个 CascadingDropDown 扩展程序，提供了 web 服务 URL 和方法信息：</span><span class="sxs-lookup"><span data-stu-id="29ba8-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="29ba8-115">然后，CascadingDropDown 扩展器使用以下方法签名异步调用 web 服务：</span><span class="sxs-lookup"><span data-stu-id="29ba8-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="29ba8-116">方法返回类型为 CascadingDropDown 的数组。</span><span class="sxs-lookup"><span data-stu-id="29ba8-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="29ba8-117">类型的构造函数首先需要列表项的标题，然后需要值（HTML `value` 特性）。</span><span class="sxs-lookup"><span data-stu-id="29ba8-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="29ba8-118">如果第三个参数设置为 true，则会在浏览器中自动选择列表元素。</span><span class="sxs-lookup"><span data-stu-id="29ba8-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="29ba8-119">在浏览器中加载页面将在下拉列表中填充三个供应商，第二个供应商正在预选择。</span><span class="sxs-lookup"><span data-stu-id="29ba8-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="29ba8-120">[![自动填充列表并自动预选](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="29ba8-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="29ba8-121">此列表是自动填充的（[单击以查看完全大小的图像](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="29ba8-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="29ba8-122">[上一页](using-cascadingdropdown-with-a-database-cs.md)
> [下一页](using-auto-postback-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="29ba8-122">[Previous](using-cascadingdropdown-with-a-database-cs.md)
[Next](using-auto-postback-with-cascadingdropdown-cs.md)</span></span>
