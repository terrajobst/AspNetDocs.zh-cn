---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: 从服务器代码启动模式弹出窗口（C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 但某些情况下，需要
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: fec0ce2cdd24333f65201301718440e1a09d930e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496976"
---
# <a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="7bb99-104">通过服务器代码启动模式弹出窗口 (C#)</span><span class="sxs-lookup"><span data-stu-id="7bb99-104">Launching a Modal Popup Window from Server Code (C#)</span></span>

<span data-ttu-id="7bb99-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7bb99-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7bb99-106">[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7bb99-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="7bb99-107">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="7bb99-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7bb99-108">但是，某些情况要求在服务器端触发模式弹出窗口的打开。</span><span class="sxs-lookup"><span data-stu-id="7bb99-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="7bb99-109">概述</span><span class="sxs-lookup"><span data-stu-id="7bb99-109">Overview</span></span>

<span data-ttu-id="7bb99-110">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="7bb99-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7bb99-111">但是，某些情况要求在服务器端触发模式弹出窗口的打开。</span><span class="sxs-lookup"><span data-stu-id="7bb99-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="7bb99-112">步骤</span><span class="sxs-lookup"><span data-stu-id="7bb99-112">Steps</span></span>

<span data-ttu-id="7bb99-113">首先，需要 ASP.NET 按钮 web 控件来演示 ModalPopup 控件的工作方式。</span><span class="sxs-lookup"><span data-stu-id="7bb99-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="7bb99-114">将 &lt;窗体中的此类按钮添加到新页上&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="7bb99-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="7bb99-115">然后，需要要创建的弹出窗口的标记。</span><span class="sxs-lookup"><span data-stu-id="7bb99-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="7bb99-116">将其定义为 `<asp:Panel>` 控件并确保它包含一个按钮控件。</span><span class="sxs-lookup"><span data-stu-id="7bb99-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="7bb99-117">ModalPopup 控件提供了使此类按钮关闭弹出窗口的功能;否则，不能轻松地使其消失。</span><span class="sxs-lookup"><span data-stu-id="7bb99-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="7bb99-118">接下来，将 ModalPopup 控件从 ASP.NET AJAX 工具包添加到页面。</span><span class="sxs-lookup"><span data-stu-id="7bb99-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="7bb99-119">设置用于加载控件的按钮、使其消失的按钮以及实际弹出窗口的 ID 的属性。</span><span class="sxs-lookup"><span data-stu-id="7bb99-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="7bb99-120">与所有基于 ASP.NET AJAX 的网页一样;脚本管理器是为不同的目标浏览器加载必要的 JavaScript 库所必需的：</span><span class="sxs-lookup"><span data-stu-id="7bb99-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="7bb99-121">在浏览器中运行该示例。</span><span class="sxs-lookup"><span data-stu-id="7bb99-121">Run the example in the browser.</span></span> <span data-ttu-id="7bb99-122">单击该按钮时，将显示模式弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="7bb99-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="7bb99-123">为了使用服务器端代码实现相同的效果，需要一个新的按钮：</span><span class="sxs-lookup"><span data-stu-id="7bb99-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="7bb99-124">如您所见，单击该按钮会生成回发，并在服务器上执行 `ServerButton_Click()` 方法。</span><span class="sxs-lookup"><span data-stu-id="7bb99-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="7bb99-125">在此方法中，称为 `launchModal()` 的 JavaScript 函数的执行方式是精确的，加载页面后将执行 JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="7bb99-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="7bb99-126">`launchModal()` 的作业是显示 ModalPopup。</span><span class="sxs-lookup"><span data-stu-id="7bb99-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="7bb99-127">完成 HTML 页面加载后，将执行 `launchModal()` 函数。</span><span class="sxs-lookup"><span data-stu-id="7bb99-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="7bb99-128">但当时，ASP.NET AJAX framework 尚未完全加载。</span><span class="sxs-lookup"><span data-stu-id="7bb99-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="7bb99-129">因此，`launchModal()` 函数只是设置 ModalPopup 控件以后必须显示的变量：</span><span class="sxs-lookup"><span data-stu-id="7bb99-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="7bb99-130">`pageLoad()` JavaScript 函数是一种特殊函数，可在完全加载 ASP.NET AJAX 后执行。</span><span class="sxs-lookup"><span data-stu-id="7bb99-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="7bb99-131">因此，我们将代码添加到此函数以显示 ModalPopup 控件，但前提是在之前调用了 `launchModal()`：</span><span class="sxs-lookup"><span data-stu-id="7bb99-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="7bb99-132">`$find()` 函数正在查找页上的命名元素，并需要服务器端 ID 作为参数。</span><span class="sxs-lookup"><span data-stu-id="7bb99-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="7bb99-133">因此，`$find("mpe")` 返回 ModalPopup 控件的客户端表示形式;它的 `show()` 方法允许弹出窗口出现。</span><span class="sxs-lookup"><span data-stu-id="7bb99-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="7bb99-134">[单击任一按钮时，会显示模式弹出窗口 ![](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7bb99-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="7bb99-135">单击任一按钮时，将显示模式弹出窗口（[单击以查看完全大小的图像](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="7bb99-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7bb99-136">下一部分</span><span class="sxs-lookup"><span data-stu-id="7bb99-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
