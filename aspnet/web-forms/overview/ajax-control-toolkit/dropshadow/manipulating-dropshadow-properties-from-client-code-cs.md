---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 从客户端代码（C#）操作 DropShadow 属性 |Microsoft Docs
author: wenz
description: 自定义 DataList 的编辑界面
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497426"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="05335-103">通过客户端代码操作 DropShadow 属性 (C#)</span><span class="sxs-lookup"><span data-stu-id="05335-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>

<span data-ttu-id="05335-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="05335-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="05335-105">[下载代码](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="05335-105">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="05335-106">AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="05335-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="05335-107">此外，还可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="05335-107">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="05335-108">概述</span><span class="sxs-lookup"><span data-stu-id="05335-108">Overview</span></span>

<span data-ttu-id="05335-109">AJAX 控件工具包中的 DropShadow 控件扩展了一个带有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="05335-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="05335-110">此外，还可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="05335-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="05335-111">步骤</span><span class="sxs-lookup"><span data-stu-id="05335-111">Steps</span></span>

<span data-ttu-id="05335-112">代码以包含某些文本行的面板开头：</span><span class="sxs-lookup"><span data-stu-id="05335-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="05335-113">关联的 CSS 类为面板提供漂亮的背景色：</span><span class="sxs-lookup"><span data-stu-id="05335-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="05335-114">添加了 `DropShadowExtender` 以将面板扩展到投影效果，不透明度设置为50%：</span><span class="sxs-lookup"><span data-stu-id="05335-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="05335-115">然后，ASP.NET AJAX `ScriptManager` 控件使控件工具包可以正常工作：</span><span class="sxs-lookup"><span data-stu-id="05335-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="05335-116">另一个面板包含两个用于设置投影不透明度的 JavaScript 链接：减号链接将减小阴影的不透明度，并将其增大。</span><span class="sxs-lookup"><span data-stu-id="05335-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="05335-117">然后，JavaScript 函数 `changeOpacity()` 必须首先在页面上查找 `DropShadowExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="05335-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="05335-118">ASP.NET AJAX 只为该任务定义 `$find()` 方法。</span><span class="sxs-lookup"><span data-stu-id="05335-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="05335-119">然后，`get_Opacity()` 方法检索当前不透明度，`set_Opacity()` 方法将设置它。</span><span class="sxs-lookup"><span data-stu-id="05335-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="05335-120">然后，JavaScript 代码将当前的 opacity 值放在 `<label>` 元素中：</span><span class="sxs-lookup"><span data-stu-id="05335-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

<span data-ttu-id="05335-121">[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="05335-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="05335-122">在客户端上更改不透明度（[单击以查看完全大小的映像](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="05335-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="05335-123">[上一页](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [下一页](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="05335-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
