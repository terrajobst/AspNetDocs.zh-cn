---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 使用带有 ReorderList （C#）的回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 每次重新排序列表时，po 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508910"
---
# <a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="4d5af-104">通过 ReorderList 使用回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="4d5af-104">Using Postbacks with ReorderList (C#)</span></span>

<span data-ttu-id="4d5af-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4d5af-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4d5af-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4d5af-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="4d5af-107">AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。</span><span class="sxs-lookup"><span data-stu-id="4d5af-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="4d5af-108">每次重新排序列表时，回发都应通知服务器发生了更改。</span><span class="sxs-lookup"><span data-stu-id="4d5af-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="4d5af-109">概述</span><span class="sxs-lookup"><span data-stu-id="4d5af-109">Overview</span></span>

<span data-ttu-id="4d5af-110">AJAX 控件工具包中的 `ReorderList` 控件提供了一个列表，用户可以通过拖放将该列表重新排序。</span><span class="sxs-lookup"><span data-stu-id="4d5af-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="4d5af-111">每次重新排序列表时，回发都应通知服务器发生了更改。</span><span class="sxs-lookup"><span data-stu-id="4d5af-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="4d5af-112">步骤</span><span class="sxs-lookup"><span data-stu-id="4d5af-112">Steps</span></span>

<span data-ttu-id="4d5af-113">`ReorderList` 控件有多个可能的数据源。</span><span class="sxs-lookup"><span data-stu-id="4d5af-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="4d5af-114">一种是使用 `XmlDataSource` 控件：</span><span class="sxs-lookup"><span data-stu-id="4d5af-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="4d5af-115">若要将此 XML 绑定到 `ReorderList` 控件并启用回发，必须设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="4d5af-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="4d5af-116">`DataSourceID`：数据源的 ID</span><span class="sxs-lookup"><span data-stu-id="4d5af-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="4d5af-117">`SortOrderField`：作为排序依据的属性</span><span class="sxs-lookup"><span data-stu-id="4d5af-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="4d5af-118">`AllowReorder`：是否允许用户对列表元素重新排序</span><span class="sxs-lookup"><span data-stu-id="4d5af-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="4d5af-119">`PostBackOnReorder`：在重新排列列表时是否创建回发</span><span class="sxs-lookup"><span data-stu-id="4d5af-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="4d5af-120">下面是控件的相应标记：</span><span class="sxs-lookup"><span data-stu-id="4d5af-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="4d5af-121">在 `ReorderList` 控件中，可以使用 `Eval()` 方法绑定数据源中的特定数据：</span><span class="sxs-lookup"><span data-stu-id="4d5af-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="4d5af-122">在页面上的任意位置，标签将在上次重新排序发生时保存信息：</span><span class="sxs-lookup"><span data-stu-id="4d5af-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="4d5af-123">此标签填充了服务器端代码中的文本，用于处理回发：</span><span class="sxs-lookup"><span data-stu-id="4d5af-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="4d5af-124">最后，为了激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放在页面上：</span><span class="sxs-lookup"><span data-stu-id="4d5af-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

<span data-ttu-id="4d5af-125">[![每次重新排序都会触发回发](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4d5af-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="4d5af-126">每次重新排序都会触发回发（[单击查看完全大小的映像](using-postbacks-with-reorderlist-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4d5af-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4d5af-127">下一部分</span><span class="sxs-lookup"><span data-stu-id="4d5af-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
