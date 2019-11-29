---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 创建分级控件（C#） |Microsoft Docs
author: wenz
description: 许多网站（从电子商务到社区站点）都提供了对文章或项目进行评级的用户。 这通常需要进行一些编码工作，但我们有 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611584"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="c5900-104">创建分级控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="c5900-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="c5900-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c5900-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c5900-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c5900-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="c5900-107">许多网站（从电子商务到社区站点）都提供了对文章或项目进行评级的用户。</span><span class="sxs-lookup"><span data-stu-id="c5900-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="c5900-108">这通常需要进行一些编码工作，但我们会提供控制工具包来处理。</span><span class="sxs-lookup"><span data-stu-id="c5900-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="c5900-109">概述</span><span class="sxs-lookup"><span data-stu-id="c5900-109">Overview</span></span>

<span data-ttu-id="c5900-110">许多网站（从电子商务到社区站点）都提供了对文章或项目进行评级的用户。</span><span class="sxs-lookup"><span data-stu-id="c5900-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="c5900-111">这通常需要进行一些编码工作，但我们会提供控制工具包来处理。</span><span class="sxs-lookup"><span data-stu-id="c5900-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="c5900-112">步骤</span><span class="sxs-lookup"><span data-stu-id="c5900-112">Steps</span></span>

<span data-ttu-id="c5900-113">首先，你至少需要两种类型的映像：一个用于填写分级项，一个用于空分级项。</span><span class="sxs-lookup"><span data-stu-id="c5900-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="c5900-114">分级项通常为星形或笑脸。</span><span class="sxs-lookup"><span data-stu-id="c5900-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="c5900-115">对于这种情况，可在本教程的源代码下载内容中找到三个文件： "笑脸" 和 ".png" 和 "smiley-done"。</span><span class="sxs-lookup"><span data-stu-id="c5900-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="c5900-116">然后，创建一个新的 ASP.NET 文件，并从向其添加 `ScriptManager` 控件开始：</span><span class="sxs-lookup"><span data-stu-id="c5900-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="c5900-117">然后，从 ASP.NET AJAX 控件工具包添加 `Rating` 控件。</span><span class="sxs-lookup"><span data-stu-id="c5900-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="c5900-118">需要为此示例设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="c5900-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="c5900-119">`CurrentRating` 要使用的初始分级</span><span class="sxs-lookup"><span data-stu-id="c5900-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="c5900-120">`MaxRating` 最大分级</span><span class="sxs-lookup"><span data-stu-id="c5900-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="c5900-121">`EmptyStarCssClass` 要在分级项（星号）为空时使用的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="c5900-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="c5900-122">`FilledStarCssClass` 填写分级项（星号）时要使用的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="c5900-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="c5900-123">`StarCssClass` 要用于可见状态的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="c5900-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="c5900-124">`WaitingStarCssClass` 在向服务器发送星型分级时要使用的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="c5900-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="c5900-125">下面是用于创建分级控件的标记，其中五个项（smileys）最初未填写：</span><span class="sxs-lookup"><span data-stu-id="c5900-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="c5900-126">这三个引用的 CSS 类现在需要显示适当的图像文件，这是使用 CSS 轻松完成的：</span><span class="sxs-lookup"><span data-stu-id="c5900-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="c5900-127">请确保提供三个图像的宽度和高度，否则显示可能会混乱了 ...。</span><span class="sxs-lookup"><span data-stu-id="c5900-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="c5900-128">最后，应向用户显示分级的结果（或者至少保存在数据库中）。</span><span class="sxs-lookup"><span data-stu-id="c5900-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="c5900-129">因此，请为文本消息的输出添加标签，并添加一个 "提交" 按钮，以将评分形式回发到服务器：</span><span class="sxs-lookup"><span data-stu-id="c5900-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="c5900-130">在服务器端代码中，通过其 `ID` 访问分级控制，然后访问其 `CurrentRating` 属性，该属性是所选分级项的编号，在本例中为0到5之间的值。</span><span class="sxs-lookup"><span data-stu-id="c5900-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="c5900-131">保存页面并将其加载到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="c5900-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="c5900-132">当你将鼠标悬停在（初始为空）分级项上时，将发生 JavaScript 影响：评级发生变化。</span><span class="sxs-lookup"><span data-stu-id="c5900-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="c5900-133">单击星形组后，将保留当前评级。</span><span class="sxs-lookup"><span data-stu-id="c5900-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="c5900-134">最后，当你提交窗体时，服务器端代码会输出所选评级。</span><span class="sxs-lookup"><span data-stu-id="c5900-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="c5900-135">[![使用最小代码创建分级系统](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c5900-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="c5900-136">使用最小代码创建分级系统（[单击以查看完全大小的图像](creating-a-rating-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c5900-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c5900-137">下一页</span><span class="sxs-lookup"><span data-stu-id="c5900-137">Next</span></span>](creating-a-rating-control-vb.md)
