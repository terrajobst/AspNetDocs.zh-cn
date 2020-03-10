---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: 动态添加折叠窗格（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常是用 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484142"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a><span data-ttu-id="49b9c-104">动态添加折叠窗格（VB）</span><span class="sxs-lookup"><span data-stu-id="49b9c-104">Dynamically Adding An Accordion Pane (VB)</span></span>

<span data-ttu-id="49b9c-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="49b9c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="49b9c-106">[下载代码](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="49b9c-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span></span>

> <span data-ttu-id="49b9c-107">AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。</span><span class="sxs-lookup"><span data-stu-id="49b9c-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="49b9c-108">面板通常在页面本身内进行声明，但可以使用服务器端代码来实现相同的结果。</span><span class="sxs-lookup"><span data-stu-id="49b9c-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="49b9c-109">概述</span><span class="sxs-lookup"><span data-stu-id="49b9c-109">Overview</span></span>

<span data-ttu-id="49b9c-110">AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。</span><span class="sxs-lookup"><span data-stu-id="49b9c-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="49b9c-111">面板通常在页面本身内进行声明，但可以使用服务器端代码来实现相同的结果。</span><span class="sxs-lookup"><span data-stu-id="49b9c-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="49b9c-112">步骤</span><span class="sxs-lookup"><span data-stu-id="49b9c-112">Steps</span></span>

<span data-ttu-id="49b9c-113">此折叠控件向服务器端代码公开所有重要属性。</span><span class="sxs-lookup"><span data-stu-id="49b9c-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="49b9c-114">在其他情况下，`Panes` 属性授予对组成可折叠面板的窗格的集合的访问权限。</span><span class="sxs-lookup"><span data-stu-id="49b9c-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="49b9c-115">每个窗格都有类型 `AccordionPane`。</span><span class="sxs-lookup"><span data-stu-id="49b9c-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="49b9c-116">因此，创建此类窗格非常简单：</span><span class="sxs-lookup"><span data-stu-id="49b9c-116">It is therefore trivial to create such a pane:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

<span data-ttu-id="49b9c-117">`AccordionPane` 的 `HeaderContainer` 属性提供对窗格的标头部分内 ASP.NET 控件的访问;`AccordionPane` 的 `ContentContainer` 属性对窗格的内容部分执行相同的工作。</span><span class="sxs-lookup"><span data-stu-id="49b9c-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="49b9c-118">这允许 ASP.NET 代码向窗格中添加内容：</span><span class="sxs-lookup"><span data-stu-id="49b9c-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

<span data-ttu-id="49b9c-119">最后，必须将窗格添加到折叠的 `Panes` 集合中：</span><span class="sxs-lookup"><span data-stu-id="49b9c-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

<span data-ttu-id="49b9c-120">下面是一个完整的服务器端代码，它将两个窗格添加到折叠控件：</span><span class="sxs-lookup"><span data-stu-id="49b9c-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

<span data-ttu-id="49b9c-121">唯一缺少的元素是可折叠元素本身，它取决于是否存在 ASP.NET `ScriptManager` 控件：</span><span class="sxs-lookup"><span data-stu-id="49b9c-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

<span data-ttu-id="49b9c-122">若要完成此示例，可折叠面板控件中引用的两个 CSS 类提供了浏览器的样式信息：</span><span class="sxs-lookup"><span data-stu-id="49b9c-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

<span data-ttu-id="49b9c-123">[![了服务器端代码动态添加了折叠面板中的数据](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="49b9c-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span></span>

<span data-ttu-id="49b9c-124">折叠后的数据是由服务器端代码动态添加的（[单击查看完全大小的映像](dynamically-adding-an-accordion-pane-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="49b9c-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="49b9c-125">上一页</span><span class="sxs-lookup"><span data-stu-id="49b9c-125">Previous</span></span>](databinding-to-an-accordion-vb.md)
