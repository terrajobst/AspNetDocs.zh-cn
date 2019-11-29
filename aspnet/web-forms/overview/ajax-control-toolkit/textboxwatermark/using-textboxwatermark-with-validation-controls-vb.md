---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 结合使用 TextBoxWatermark 和验证控件（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597243"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a><span data-ttu-id="98c5d-104">通过验证控件使用 TextBoxWatermark (VB)</span><span class="sxs-lookup"><span data-stu-id="98c5d-104">Using TextBoxWatermark With Validation Controls (VB)</span></span>

<span data-ttu-id="98c5d-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="98c5d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="98c5d-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="98c5d-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span></span>

> <span data-ttu-id="98c5d-107">AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="98c5d-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="98c5d-108">当用户在框中单击时，它会被清空。</span><span class="sxs-lookup"><span data-stu-id="98c5d-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="98c5d-109">如果用户离开该框而不输入文本，则会重新出现预填充文本。</span><span class="sxs-lookup"><span data-stu-id="98c5d-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="98c5d-110">这可能会与同一页面上的 ASP.NET 验证控件发生冲突，但可能会解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="98c5d-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="98c5d-111">概述</span><span class="sxs-lookup"><span data-stu-id="98c5d-111">Overview</span></span>

<span data-ttu-id="98c5d-112">AJAX 控件工具包中的 `TextBoxWatermark` 控件扩展了文本框，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="98c5d-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="98c5d-113">当用户在框中单击时，它会被清空。</span><span class="sxs-lookup"><span data-stu-id="98c5d-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="98c5d-114">如果用户离开该框而不输入文本，则会重新出现预填充文本。</span><span class="sxs-lookup"><span data-stu-id="98c5d-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="98c5d-115">这可能会与同一页面上的 ASP.NET 验证控件发生冲突，但可能会解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="98c5d-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="98c5d-116">步骤</span><span class="sxs-lookup"><span data-stu-id="98c5d-116">Steps</span></span>

<span data-ttu-id="98c5d-117">示例的基本设置如下所示：使用 `TextBoxWatermarkExtender` 控件打水印 `TextBox` 控件。</span><span class="sxs-lookup"><span data-stu-id="98c5d-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="98c5d-118">按钮触发回发，稍后用于触发页面上的验证控件。</span><span class="sxs-lookup"><span data-stu-id="98c5d-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="98c5d-119">此外，还需要 `ScriptManager` 控件才能初始化 ASP.NET AJAX：</span><span class="sxs-lookup"><span data-stu-id="98c5d-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="98c5d-120">现在，添加一个 `RequiredFieldValidator` 控件，该控件在提交窗体时检查字段中是否有文本。</span><span class="sxs-lookup"><span data-stu-id="98c5d-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="98c5d-121">验证程序的 `InitialValue` 属性必须设置为 `TextBoxWatermarkExtender` 控件中使用的相同值：提交窗体时，未更改文本框的值是其中的水印值：</span><span class="sxs-lookup"><span data-stu-id="98c5d-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="98c5d-122">但这种方法存在一个问题：如果客户端禁用 JavaScript，则不会使用水印文本预填充文本字段，因此 `RequiredFieldValidator` 不会触发错误消息。</span><span class="sxs-lookup"><span data-stu-id="98c5d-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="98c5d-123">因此，第二个 `RequiredFieldValidator` 控件需要检查是否有空的文本框（省略 `InitialValue` 特性）。</span><span class="sxs-lookup"><span data-stu-id="98c5d-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="98c5d-124">由于这两个验证程序使用 `Display`=`"Dynamic"`，因此最终用户无法区分这两个验证程序中触发的可视化外观;相反，它看起来只是其中的一个。</span><span class="sxs-lookup"><span data-stu-id="98c5d-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="98c5d-125">最后，如果没有验证程序发出错误消息，则添加一些服务器端代码以输出字段中的文本：</span><span class="sxs-lookup"><span data-stu-id="98c5d-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="98c5d-126">[![验证器投诉原因在字段中没有文本](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="98c5d-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="98c5d-127">验证器投诉原因该字段中没有任何文本（[单击查看完全大小的图像](using-textboxwatermark-with-validation-controls-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="98c5d-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="98c5d-128">上一部分</span><span class="sxs-lookup"><span data-stu-id="98c5d-128">Previous</span></span>](using-textboxwatermark-in-a-formview-vb.md)
