---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: 仅允许在文本框中使用特定字符（C#） |Microsoft Docs
author: wenz
description: ASP.NET 验证控件可以确保用户输入中仅允许某些字符。 但这仍不会阻止用户键入无效 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: d1e367becd574e31d24fca8545f76b1ed3c4d85e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446354"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="eafc8-104">仅允许在文本框中使用特定字符 (C#)</span><span class="sxs-lookup"><span data-stu-id="eafc8-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>

<span data-ttu-id="eafc8-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="eafc8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="eafc8-106">[下载代码](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="eafc8-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="eafc8-107">ASP.NET 验证控件可以确保用户输入中仅允许某些字符。</span><span class="sxs-lookup"><span data-stu-id="eafc8-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="eafc8-108">但这仍不会阻止用户键入无效字符并尝试提交窗体。</span><span class="sxs-lookup"><span data-stu-id="eafc8-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="eafc8-109">概述</span><span class="sxs-lookup"><span data-stu-id="eafc8-109">Overview</span></span>

<span data-ttu-id="eafc8-110">ASP.NET 验证控件可以确保用户输入中仅允许某些字符。</span><span class="sxs-lookup"><span data-stu-id="eafc8-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="eafc8-111">但这仍不会阻止用户键入无效字符并尝试提交窗体。</span><span class="sxs-lookup"><span data-stu-id="eafc8-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="eafc8-112">步骤</span><span class="sxs-lookup"><span data-stu-id="eafc8-112">Steps</span></span>

<span data-ttu-id="eafc8-113">ASP.NET AJAX 控件工具包包含用于扩展文本框的 `FilteredTextBox` 控件。</span><span class="sxs-lookup"><span data-stu-id="eafc8-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="eafc8-114">激活后，只能在该字段中输入一组特定的字符。</span><span class="sxs-lookup"><span data-stu-id="eafc8-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="eafc8-115">为此，我们首先需要使用 ASP.NET AJAX `ScriptManager`，后者会加载 ASP.NET AJAX 控件工具包也使用的 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="eafc8-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="eafc8-116">接下来，我们需要一个文本框：</span><span class="sxs-lookup"><span data-stu-id="eafc8-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="eafc8-117">最后，`FilteredTextBoxExtender` 控件负责限制允许用户键入的字符。</span><span class="sxs-lookup"><span data-stu-id="eafc8-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="eafc8-118">首先，将 `TargetControlID` 特性设置为 `TextBox` 控件的 `ID`。</span><span class="sxs-lookup"><span data-stu-id="eafc8-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="eafc8-119">然后，选择一个可用的 `FilterType` 值：</span><span class="sxs-lookup"><span data-stu-id="eafc8-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="eafc8-120">`Custom` 默认值;必须提供有效字符的列表</span><span class="sxs-lookup"><span data-stu-id="eafc8-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="eafc8-121">仅 `LowercaseLetters` 小写字母</span><span class="sxs-lookup"><span data-stu-id="eafc8-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="eafc8-122">仅 `Numbers` 数字</span><span class="sxs-lookup"><span data-stu-id="eafc8-122">`Numbers` digits only</span></span>
- <span data-ttu-id="eafc8-123">仅 `UppercaseLetters` 大写字母</span><span class="sxs-lookup"><span data-stu-id="eafc8-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="eafc8-124">如果使用 `Custom FilterType`，则必须设置 `ValidChars` 属性，并提供可键入的字符列表。</span><span class="sxs-lookup"><span data-stu-id="eafc8-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="eafc8-125">顺便说一下，如果您尝试将文本粘贴到文本框中，则所有无效字符将被删除。</span><span class="sxs-lookup"><span data-stu-id="eafc8-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="eafc8-126">下面是仅允许数字的 `FilteredTextBoxExtender` 控件的标记（也可能是 `FilterType="Numbers"`的）：</span><span class="sxs-lookup"><span data-stu-id="eafc8-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="eafc8-127">运行页，如果启用了 JavaScript，则尝试输入一个字母，否则它将不起作用;但会在页面上显示数字。</span><span class="sxs-lookup"><span data-stu-id="eafc8-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="eafc8-128">但请注意，保护 `FilteredTextBox` 提供的不是项目符号：如果启用了 JavaScript，则可以在文本框中输入任何数据，因此，必须使用其他验证方法，即 .ASP。NET 的验证控件。</span><span class="sxs-lookup"><span data-stu-id="eafc8-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="eafc8-129">[只能输入 ![位数](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="eafc8-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span></span>

<span data-ttu-id="eafc8-130">只能输入数字（[单击以查看完全大小的图像](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="eafc8-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="eafc8-131">下一部分</span><span class="sxs-lookup"><span data-stu-id="eafc8-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)
