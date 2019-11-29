---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 创建互斥复选框（VB） |Microsoft Docs
author: wenz
description: 如果只能选择一组选项中的一个选项，则通常会使用单选按钮。 但有一个缺点：选中组中的一个单选按钮后,。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606467"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="ab3e7-104">创建互斥复选框 (VB)</span><span class="sxs-lookup"><span data-stu-id="ab3e7-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>

<span data-ttu-id="ab3e7-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ab3e7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ab3e7-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ab3e7-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="ab3e7-107">如果只能选择一组选项中的一个选项，则通常会使用单选按钮。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="ab3e7-108">但有一个缺点：选中组中的一个单选按钮后，不能取消选中所有单选按钮。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="ab3e7-109">任何时候都可以取消选中复选框，但并不相互排斥。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="ab3e7-110">本教程提供了这两种方法的最佳方案：互相排斥的复选框。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="ab3e7-111">概述</span><span class="sxs-lookup"><span data-stu-id="ab3e7-111">Overview</span></span>

<span data-ttu-id="ab3e7-112">如果只能选择一组选项中的一个选项，则通常会使用单选按钮。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="ab3e7-113">但有一个缺点：选中组中的一个单选按钮后，不能取消选中所有单选按钮。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="ab3e7-114">任何时候都可以取消选中复选框，但并不相互排斥。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="ab3e7-115">本教程提供了这两种方法的最佳方案：互相排斥的复选框。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="ab3e7-116">步骤</span><span class="sxs-lookup"><span data-stu-id="ab3e7-116">Steps</span></span>

<span data-ttu-id="ab3e7-117">ASP.NET AJAX 控件工具包包含 MutuallyExclusiveCheckBox 扩展器。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="ab3e7-118">这使程序员能够为组名称（`Key` 属性）分配任何复选框。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="ab3e7-119">在同一组内的所有复选框中，一次只能选择一项。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="ab3e7-120">首先，将两个复选框放在新的 ASP.NET 页上。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="ab3e7-121">可能还有更多，但有两个足以说明这一原则：</span><span class="sxs-lookup"><span data-stu-id="ab3e7-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="ab3e7-122">对于这两个复选框，必须在页面上放置一个 MutuallyExclusiveCheckBoxExtender 控件。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="ab3e7-123">这两个键特性都需要具有相同的值，就像 HTML 单选按钮元素的值特性必须完全相同以指示它们所属的组。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="ab3e7-124">扩展器的 TargetControlID 属性指向复选框的 ID。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="ab3e7-125">最后，包括 ASP.NET AJAX 控件工具包的所有元素所需的 ASP.NET AJAX `ScriptManager`：</span><span class="sxs-lookup"><span data-stu-id="ab3e7-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="ab3e7-126">保存并运行页面：可以选中和取消选中这两个复选框，但不能同时选中两个复选框。</span><span class="sxs-lookup"><span data-stu-id="ab3e7-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="ab3e7-127">[一次只能检查一个 checkbox ![](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ab3e7-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="ab3e7-128">一次只能检查一个复选框（[单击查看完全大小的图像](creating-mutually-exclusive-checkboxes-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ab3e7-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ab3e7-129">上一部分</span><span class="sxs-lookup"><span data-stu-id="ab3e7-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
