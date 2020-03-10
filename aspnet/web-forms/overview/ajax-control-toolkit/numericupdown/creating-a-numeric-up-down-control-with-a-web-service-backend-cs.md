---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: 使用 Web 服务后端创建数字向上/向下控件（C#） |Microsoft Docs
author: wenz
description: 不允许用户在复选框中键入值，而是将数字向上/向下控件（在 Windows 和其他操作系统上存在）视为更多的 c 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509012"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="ecfbb-103">使用 Web 服务后端创建数字增大/减小控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="ecfbb-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>

<span data-ttu-id="ecfbb-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ecfbb-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ecfbb-105">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ecfbb-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="ecfbb-106">不允许用户在复选框中键入值，而是在 Windows 和其他操作系统上的数字向上/向下控制（存在于 Windows 和其他操作系统上）可以更舒适地证明。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="ecfbb-107">默认情况下，NumericUpDown 控件始终将值增大或减小1，但 web 服务的灵活性更高。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="ecfbb-108">概述</span><span class="sxs-lookup"><span data-stu-id="ecfbb-108">Overview</span></span>

<span data-ttu-id="ecfbb-109">不允许用户在复选框中键入值，而是在 Windows 和其他操作系统上的数字向上/向下控制（存在于 Windows 和其他操作系统上）可以更舒适地证明。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="ecfbb-110">默认情况下，`NumericUpDown` 控件始终将值增加或减少1，但 web 服务将获得更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="ecfbb-111">步骤</span><span class="sxs-lookup"><span data-stu-id="ecfbb-111">Steps</span></span>

<span data-ttu-id="ecfbb-112">ASP.NET AJAX 控件工具包包含自动将两个按钮添加到文本框的 `NumericUpDown` 扩展器：一个用于增加其值，一个用于减小值。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="ecfbb-113">但是，该控件还支持 web 服务调用（或 page 方法调用）。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="ecfbb-114">当单击 "上移" 或 "下移" 按钮时，JavaScript 代码会连接到 web 服务器并在其中执行方法。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="ecfbb-115">方法签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="ecfbb-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="ecfbb-116">`current` 参数是文本框中的当前值;`tag` 属性是其他上下文数据，可将其设置为 `NumericUpDown` 扩展器的属性（但不是必需的）。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="ecfbb-117">对于本示例，数值向上/向下控件应仅允许作为2：1、2、4、8、16、32、64等的幂的值。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="ecfbb-118">因此，当用户想要增加值时，所执行的方法必须翻倍旧值;另一种方法必须将值除以2。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="ecfbb-119">下面是完整的 web 服务：</span><span class="sxs-lookup"><span data-stu-id="ecfbb-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="ecfbb-120">最后，创建新的 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="ecfbb-121">通常，您需要 `ScriptManager` 控件、`TextBox` 控件和 `NumericUpDownExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="ecfbb-122">对于后者，你必须提供 web 服务信息：</span><span class="sxs-lookup"><span data-stu-id="ecfbb-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="ecfbb-123">web 方法或页方法的 `ServiceDownMethod` 名称</span><span class="sxs-lookup"><span data-stu-id="ecfbb-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="ecfbb-124">通过服务方法 `ServiceDownPath` web 服务的路径;如果使用 page 方法，则省略</span><span class="sxs-lookup"><span data-stu-id="ecfbb-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="ecfbb-125">向上 web 方法或页方法 `ServiceUpMethod` 名称</span><span class="sxs-lookup"><span data-stu-id="ecfbb-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="ecfbb-126">具有 up 服务方法的 web 服务 `ServiceUpPath` 路径;如果使用 page 方法，则省略</span><span class="sxs-lookup"><span data-stu-id="ecfbb-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="ecfbb-127">下面是页面的完整标记：</span><span class="sxs-lookup"><span data-stu-id="ecfbb-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="ecfbb-128">如果运行该页面，请注意在单击上方按钮时文本框中的值始终是双精度值，单击下方的按钮时，该按钮的值将减半。</span><span class="sxs-lookup"><span data-stu-id="ecfbb-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="ecfbb-129">[仅 ![显示2的幂的数字](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ecfbb-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="ecfbb-130">仅显示2的幂的数字（[单击以查看完全大小的图像](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ecfbb-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ecfbb-131">下一部分</span><span class="sxs-lookup"><span data-stu-id="ecfbb-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
