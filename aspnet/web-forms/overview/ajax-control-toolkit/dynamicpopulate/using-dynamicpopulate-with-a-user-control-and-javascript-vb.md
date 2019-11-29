---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 将通过 dynamicpopulate 与用户控件和 JavaScript 一起使用（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599117"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="be6bc-103">通过用户控件和 JavaScript 使用 DynamicPopulate (VB)</span><span class="sxs-lookup"><span data-stu-id="be6bc-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="be6bc-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="be6bc-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="be6bc-105">[下载代码](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="be6bc-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="be6bc-106">ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。</span><span class="sxs-lookup"><span data-stu-id="be6bc-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="be6bc-107">还可以使用自定义客户端 JavaScript 代码触发填充。</span><span class="sxs-lookup"><span data-stu-id="be6bc-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="be6bc-108">但当扩展器驻留在用户控件中时，必须特别小心。</span><span class="sxs-lookup"><span data-stu-id="be6bc-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="be6bc-109">概述</span><span class="sxs-lookup"><span data-stu-id="be6bc-109">Overview</span></span>

<span data-ttu-id="be6bc-110">ASP.NET AJAX 控件工具包中的 `DynamicPopulate` 控件将调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。</span><span class="sxs-lookup"><span data-stu-id="be6bc-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="be6bc-111">还可以使用自定义客户端 JavaScript 代码触发填充。</span><span class="sxs-lookup"><span data-stu-id="be6bc-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="be6bc-112">但当扩展器驻留在用户控件中时，必须特别小心。</span><span class="sxs-lookup"><span data-stu-id="be6bc-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="be6bc-113">步骤</span><span class="sxs-lookup"><span data-stu-id="be6bc-113">Steps</span></span>

<span data-ttu-id="be6bc-114">首先，需要一个 ASP.NET Web 服务，该服务实现 `DynamicPopulateExtender` 控件调用的方法。</span><span class="sxs-lookup"><span data-stu-id="be6bc-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="be6bc-115">Web 服务实现 `getDate()` 方法，该方法需要一个名为 `contextKey`的字符串类型参数，因为 `DynamicPopulate` 控件向每个 web 服务调用发送一段上下文信息。</span><span class="sxs-lookup"><span data-stu-id="be6bc-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="be6bc-116">下面是以下列三种格式之一检索当前日期的代码（文件 `DynamicPopulate.vb.asmx`）：</span><span class="sxs-lookup"><span data-stu-id="be6bc-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="be6bc-117">在下一步中，创建一个新的用户控件（`.ascx` 文件），该控件的第一行由以下声明表示：</span><span class="sxs-lookup"><span data-stu-id="be6bc-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="be6bc-118">&lt;`label`&gt; 元素将用于显示来自服务器的数据。</span><span class="sxs-lookup"><span data-stu-id="be6bc-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="be6bc-119">另外，在用户控件文件中，我们将使用三个单选按钮，每个按钮表示 web 服务支持的三种可能日期格式之一。</span><span class="sxs-lookup"><span data-stu-id="be6bc-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="be6bc-120">当用户单击某个单选按钮时，浏览器将执行如下所示的 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="be6bc-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="be6bc-121">此代码访问 `DynamicPopulateExtender` （不要担心奇怪的 ID，稍后将在此进行介绍）并触发数据的动态填充。</span><span class="sxs-lookup"><span data-stu-id="be6bc-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="be6bc-122">在当前单选按钮的上下文中，`this.value` 引用 `format1`的值，`format2` 或 `format3` web 方法所需的内容。</span><span class="sxs-lookup"><span data-stu-id="be6bc-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="be6bc-123">用户控件中唯一缺少的内容是将单选按钮链接到 web 服务的 `DynamicPopulateExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="be6bc-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="be6bc-124">同样，您可以记下控件中使用的奇怪 ID： `mcd1$myDate` 而不是 `myDate`。</span><span class="sxs-lookup"><span data-stu-id="be6bc-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="be6bc-125">以前，`mcd1_dpe1` 使用的 JavaScript 代码访问 `DynamicPopulateExtender` 而不是 `dpe1`。此命名策略是在用户控件中使用 `DynamicPopulateExtender` 时的特殊要求。</span><span class="sxs-lookup"><span data-stu-id="be6bc-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="be6bc-126">而且，您必须以特定方式嵌入用户控件，才能使其全部工作。</span><span class="sxs-lookup"><span data-stu-id="be6bc-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="be6bc-127">创建新的 ASP.NET 页面，并为刚刚实现的用户控件注册标记前缀：</span><span class="sxs-lookup"><span data-stu-id="be6bc-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="be6bc-128">然后，在新页上包含 ASP.NET AJAX `ScriptManager` 控件：</span><span class="sxs-lookup"><span data-stu-id="be6bc-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="be6bc-129">最后，将用户控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="be6bc-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="be6bc-130">你只需设置其 `ID` 属性（当然还 `runat="server"`），但你还必须将其设置为特定名称： `mcd1`，因为这是在用户控件内使用 JavaScript 访问它所使用的前缀。</span><span class="sxs-lookup"><span data-stu-id="be6bc-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="be6bc-131">就是这么简单！</span><span class="sxs-lookup"><span data-stu-id="be6bc-131">And that's it!</span></span> <span data-ttu-id="be6bc-132">页面按预期方式工作：用户单击某个单选按钮，工具箱中的控件将调用 web 服务并以所需格式显示当前日期。</span><span class="sxs-lookup"><span data-stu-id="be6bc-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="be6bc-133">[![单选按钮驻留在用户控件中](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="be6bc-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="be6bc-134">单选按钮位于用户控件中（[单击以查看完全大小的图像](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="be6bc-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="be6bc-135">上一部分</span><span class="sxs-lookup"><span data-stu-id="be6bc-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
