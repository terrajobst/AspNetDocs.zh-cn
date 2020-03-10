---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 从客户端代码操作 DropShadow 属性（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。 此外，还可以使用客户端 Javascript 更改此扩展器的属性。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497408"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="c41ba-104">通过客户端代码操作 DropShadow 属性 (VB)</span><span class="sxs-lookup"><span data-stu-id="c41ba-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="c41ba-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c41ba-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c41ba-106">[下载代码](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c41ba-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="c41ba-107">AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="c41ba-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="c41ba-108">此外，还可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="c41ba-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="c41ba-109">概述</span><span class="sxs-lookup"><span data-stu-id="c41ba-109">Overview</span></span>

<span data-ttu-id="c41ba-110">AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="c41ba-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="c41ba-111">此外，还可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="c41ba-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="c41ba-112">步骤</span><span class="sxs-lookup"><span data-stu-id="c41ba-112">Steps</span></span>

<span data-ttu-id="c41ba-113">代码以包含某些文本行的面板开头：</span><span class="sxs-lookup"><span data-stu-id="c41ba-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="c41ba-114">关联的 CSS 类为面板提供漂亮的背景色：</span><span class="sxs-lookup"><span data-stu-id="c41ba-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="c41ba-115">添加了 `DropShadowExtender` 以将面板扩展到投影效果，不透明度设置为50%：</span><span class="sxs-lookup"><span data-stu-id="c41ba-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="c41ba-116">然后，ASP.NET AJAX `ScriptManager` 控件使控件工具包可以正常工作：</span><span class="sxs-lookup"><span data-stu-id="c41ba-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="c41ba-117">另一个面板包含两个用于设置投影不透明度的 JavaScript 链接：减号链接将减小阴影的不透明度，并将其增大。</span><span class="sxs-lookup"><span data-stu-id="c41ba-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="c41ba-118">然后，JavaScript 函数 `changeOpacity()` 必须首先在页面上查找 `DropShadowExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="c41ba-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="c41ba-119">ASP.NET AJAX 只为该任务定义 `$find()` 方法。</span><span class="sxs-lookup"><span data-stu-id="c41ba-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="c41ba-120">然后，`get_Opacity()` 方法检索当前不透明度，`set_Opacity()` 方法将设置它。</span><span class="sxs-lookup"><span data-stu-id="c41ba-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="c41ba-121">然后，JavaScript 代码将当前的 opacity 值放在 `<label>` 元素中：</span><span class="sxs-lookup"><span data-stu-id="c41ba-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="c41ba-122">[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c41ba-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="c41ba-123">在客户端上更改不透明度（[单击以查看完全大小的映像](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c41ba-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c41ba-124">上一页</span><span class="sxs-lookup"><span data-stu-id="c41ba-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
