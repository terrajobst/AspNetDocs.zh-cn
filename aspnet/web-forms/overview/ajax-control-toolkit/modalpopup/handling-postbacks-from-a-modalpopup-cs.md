---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: 处理来自 ModalPopup （）的C#回发（） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 如果需要特别注意，
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599107"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a><span data-ttu-id="8a759-104">通过 ModalPopup 处理回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="8a759-104">Handling Postbacks from a ModalPopup (C#)</span></span>

<span data-ttu-id="8a759-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8a759-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8a759-106">[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8a759-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span></span>

> <span data-ttu-id="8a759-107">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="8a759-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="8a759-108">从弹出窗口中创建回发时，必须特别小心。</span><span class="sxs-lookup"><span data-stu-id="8a759-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="8a759-109">概述</span><span class="sxs-lookup"><span data-stu-id="8a759-109">Overview</span></span>

<span data-ttu-id="8a759-110">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="8a759-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="8a759-111">从弹出窗口中创建回发时，必须特别小心。</span><span class="sxs-lookup"><span data-stu-id="8a759-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="8a759-112">步骤</span><span class="sxs-lookup"><span data-stu-id="8a759-112">Steps</span></span>

<span data-ttu-id="8a759-113">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="8a759-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="8a759-114">接下来，添加一个用于模式弹出窗口的面板。</span><span class="sxs-lookup"><span data-stu-id="8a759-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="8a759-115">在该处，用户可以输入名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="8a759-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="8a759-116">按钮用于关闭弹出窗口并保存信息。</span><span class="sxs-lookup"><span data-stu-id="8a759-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="8a759-117">请注意，将设置 `OnClick` 特性，以便在单击此按钮时发生回发：</span><span class="sxs-lookup"><span data-stu-id="8a759-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="8a759-118">该页本身包含两个标签，用于完全相同的信息：名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="8a759-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="8a759-119">按钮用于触发模式弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="8a759-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

<span data-ttu-id="8a759-120">为了使弹出窗口出现，请添加 `ModalPopupExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="8a759-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="8a759-121">将 `PopupControlID` 特性设置为面板的 ID，并将 `TargetControlID` 到按钮的 ID：</span><span class="sxs-lookup"><span data-stu-id="8a759-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

<span data-ttu-id="8a759-122">现在，每当单击模式弹出窗口中的 "`Save`" 按钮时，就会执行服务器端 `SaveData()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8a759-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="8a759-123">在那里，可以将输入的数据保存在数据存储中。</span><span class="sxs-lookup"><span data-stu-id="8a759-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="8a759-124">为了简单起见，新数据只是在标签中输出：</span><span class="sxs-lookup"><span data-stu-id="8a759-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

<span data-ttu-id="8a759-125">此外，应用当前名称和电子邮件填充模式弹出窗口中的 textbox 控件。</span><span class="sxs-lookup"><span data-stu-id="8a759-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="8a759-126">但这仅在不发生回发时才是必需的。</span><span class="sxs-lookup"><span data-stu-id="8a759-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="8a759-127">如果有回发，ASP.NET viewstate 功能将自动使用适当的值填充文本框。</span><span class="sxs-lookup"><span data-stu-id="8a759-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

<span data-ttu-id="8a759-128">[![模式弹出窗口导致回发](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8a759-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="8a759-129">模式弹出窗口导致回发（[单击查看完全大小的映像](handling-postbacks-from-a-modalpopup-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="8a759-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8a759-130">[上一页](using-modalpopup-with-a-repeater-control-cs.md)
> [下一页](positioning-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8a759-130">[Previous](using-modalpopup-with-a-repeater-control-cs.md)
[Next](positioning-a-modalpopup-cs.md)</span></span>
