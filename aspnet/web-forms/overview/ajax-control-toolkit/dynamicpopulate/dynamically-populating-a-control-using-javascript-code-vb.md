---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: 使用 JavaScript 代码动态填充控件（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497378"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a><span data-ttu-id="ab99f-103">使用 JavaScript 代码动态填充控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="ab99f-103">Dynamically Populating a Control Using JavaScript Code (VB)</span></span>

<span data-ttu-id="ab99f-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ab99f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ab99f-105">[下载代码](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ab99f-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)</span></span>

> <span data-ttu-id="ab99f-106">ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。</span><span class="sxs-lookup"><span data-stu-id="ab99f-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="ab99f-107">还可以使用自定义客户端 JavaScript 代码触发填充。</span><span class="sxs-lookup"><span data-stu-id="ab99f-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="ab99f-108">概述</span><span class="sxs-lookup"><span data-stu-id="ab99f-108">Overview</span></span>

<span data-ttu-id="ab99f-109">ASP.NET AJAX 控件工具包中的 `DynamicPopulate` 控件将调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。</span><span class="sxs-lookup"><span data-stu-id="ab99f-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="ab99f-110">还可以使用自定义客户端 JavaScript 代码触发填充。</span><span class="sxs-lookup"><span data-stu-id="ab99f-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ab99f-111">步骤</span><span class="sxs-lookup"><span data-stu-id="ab99f-111">Steps</span></span>

<span data-ttu-id="ab99f-112">首先，需要一个 ASP.NET Web 服务，该服务实现 `DynamicPopulateExtender` 控件调用的方法。</span><span class="sxs-lookup"><span data-stu-id="ab99f-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="ab99f-113">Web 服务实现 `getDate()` 方法，该方法需要一个名为 `contextKey`的字符串类型参数，因为 `DynamicPopulate` 控件向每个 web 服务调用发送一段上下文信息。</span><span class="sxs-lookup"><span data-stu-id="ab99f-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="ab99f-114">下面是以下列三种格式之一检索当前日期的代码（文件 `DynamicPopulate.vb.asmx`）：</span><span class="sxs-lookup"><span data-stu-id="ab99f-114">Here is the code (file `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

<span data-ttu-id="ab99f-115">在下一步中，创建一个新的 ASP.NET 网站，并从 ASP.NET AJAX ScriptManager 控件开始：</span><span class="sxs-lookup"><span data-stu-id="ab99f-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

<span data-ttu-id="ab99f-116">然后，添加 "标签" 控件（例如，使用同一名称的 HTML 控件或 `<asp:Label />` web 控件），稍后会显示 web 服务调用的结果。</span><span class="sxs-lookup"><span data-stu-id="ab99f-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

<span data-ttu-id="ab99f-117">接下来，请提供 `DynamicPopulateExtender` 控件并提供 web 服务信息、目标控件，但不能使用自定义 JavaScript 来触发填充的控件的名称。</span><span class="sxs-lookup"><span data-stu-id="ab99f-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

<span data-ttu-id="ab99f-118">立即到 JavaScript 部分。</span><span class="sxs-lookup"><span data-stu-id="ab99f-118">Now to the JavaScript part.</span></span> <span data-ttu-id="ab99f-119">ASP.NET AJAX 库定义的 `$find()` 函数返回对 ASP.NET AJAX 控件工具包（如 `DynamicPopulateExtender`）的服务器端对象的引用。</span><span class="sxs-lookup"><span data-stu-id="ab99f-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="ab99f-120">在当前文件中，`$find("dpe")` 返回对页中一个 `DynamicPopulateExtender` 控件的引用。</span><span class="sxs-lookup"><span data-stu-id="ab99f-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="ab99f-121">它公开一个称为 `populate()` 的方法，该方法将触发动态填充过程。</span><span class="sxs-lookup"><span data-stu-id="ab99f-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="ab99f-122">`populate()` 方法需要一个参数：作为 `getDate()` web 方法的参数的上下文键。</span><span class="sxs-lookup"><span data-stu-id="ab99f-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="ab99f-123">例如，`$find("dpe").populate("format1")` 会用月格式的当前日期填充标签。</span><span class="sxs-lookup"><span data-stu-id="ab99f-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="ab99f-124">为了使示例更灵活，用户现在可以在几种日期格式之间进行选择。</span><span class="sxs-lookup"><span data-stu-id="ab99f-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="ab99f-125">对于其中的每个，将显示单选按钮。</span><span class="sxs-lookup"><span data-stu-id="ab99f-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="ab99f-126">用户单击某个单选按钮后，JavaScript 代码将使用所选日期格式动态填充该标签。</span><span class="sxs-lookup"><span data-stu-id="ab99f-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="ab99f-127">这些单选按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="ab99f-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

<span data-ttu-id="ab99f-128">请注意，在单选按钮的上下文中，JavaScript 表达式 `this.value` 引用当前按钮的值，这恰好与 `getDate()` 方法可以使用的信息完全相同。</span><span class="sxs-lookup"><span data-stu-id="ab99f-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="ab99f-129">[![单击该按钮将以指定的格式从服务器中检索日期](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ab99f-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="ab99f-130">单击该按钮将以指定的格式从服务器中检索日期（[单击查看完全大小的图像](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ab99f-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ab99f-131">[上一页](dynamically-populating-a-control-vb.md)
> [下一页](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ab99f-131">[Previous](dynamically-populating-a-control-vb.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)</span></span>
