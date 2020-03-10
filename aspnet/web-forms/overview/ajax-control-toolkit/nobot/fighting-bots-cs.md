---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 反击 Bot （C#） |Microsoft Docs
author: wenz
description: 自动机器人 plaster 网络日志和其他具有垃圾邮件的网站，无需任何用户交互即可提交注释表单。 ASP.NET 中的 NoBot 控件 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509066"
---
# <a name="fighting-bots-c"></a><span data-ttu-id="ad686-104">外部测试机器人 (C#)</span><span class="sxs-lookup"><span data-stu-id="ad686-104">Fighting Bots (C#)</span></span>

<span data-ttu-id="ad686-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ad686-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ad686-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ad686-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span></span>

> <span data-ttu-id="ad686-107">自动机器人 plaster 网络日志和其他具有垃圾邮件的网站，无需任何用户交互即可提交注释表单。</span><span class="sxs-lookup"><span data-stu-id="ad686-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="ad686-108">ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。</span><span class="sxs-lookup"><span data-stu-id="ad686-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="overview"></a><span data-ttu-id="ad686-109">概述</span><span class="sxs-lookup"><span data-stu-id="ad686-109">Overview</span></span>

<span data-ttu-id="ad686-110">自动机器人 plaster 网络日志和其他具有垃圾邮件的网站，无需任何用户交互即可提交注释表单。</span><span class="sxs-lookup"><span data-stu-id="ad686-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="ad686-111">ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。</span><span class="sxs-lookup"><span data-stu-id="ad686-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="ad686-112">步骤</span><span class="sxs-lookup"><span data-stu-id="ad686-112">Steps</span></span>

<span data-ttu-id="ad686-113">抵御 bot 的一种常见方法是使用 CAPTCHAs 完全自动化的公共把测试来区分计算机和人。</span><span class="sxs-lookup"><span data-stu-id="ad686-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="ad686-114">把测试最初是一种测试，在此测试中，有人需要确定通信合作伙伴是否是人或计算机。</span><span class="sxs-lookup"><span data-stu-id="ad686-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="ad686-115">在 web 中，CAPTCHA 通常包含一个图像，其中包含一些扭曲的字母。</span><span class="sxs-lookup"><span data-stu-id="ad686-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="ad686-116">其思想是，只有人可以读取图像上的字母，而 OCR 算法将会失败。</span><span class="sxs-lookup"><span data-stu-id="ad686-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="ad686-117">此方法有几个优点和缺点，但本教程的讨论范围之外对此进行了讨论。</span><span class="sxs-lookup"><span data-stu-id="ad686-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="ad686-118">但 ASP.NET AJAX 控件工具包中有一个控件，它提供类似的方法： `NoBot`。</span><span class="sxs-lookup"><span data-stu-id="ad686-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="ad686-119">与 CAPTCHA 相比，此方法更易于克服，但在博客上非常易于使用和费用，如果大多数垃圾邮件尝试失效（`NoBot` 控制可执行此操作），则会将其视为成功。</span><span class="sxs-lookup"><span data-stu-id="ad686-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="ad686-120">如果至少满足以下条件之一，`NoBot` 会截获当前 ASP.NET web 窗体的回发：</span><span class="sxs-lookup"><span data-stu-id="ad686-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="ad686-121">浏览器未能解决 JavaScript 谜题（例如，在停用 JavaScript 时）</span><span class="sxs-lookup"><span data-stu-id="ad686-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="ad686-122">用户已将窗体提交到快速</span><span class="sxs-lookup"><span data-stu-id="ad686-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="ad686-123">在特定时间段内，客户端 IP 地址的提交时间太长。</span><span class="sxs-lookup"><span data-stu-id="ad686-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="ad686-124">若要检查这些情况，`NoBot` 控件需要这些属性（它们都是可选的）：</span><span class="sxs-lookup"><span data-stu-id="ad686-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="ad686-125">回发之间 `ResponseMinimumDelaySeconds` 最小秒数</span><span class="sxs-lookup"><span data-stu-id="ad686-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="ad686-126">`CutoffWindowSeconds` 时间间隔，其中一个 IP 的回发是度量值</span><span class="sxs-lookup"><span data-stu-id="ad686-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="ad686-127">每个时间间隔 `CutoffMaximumInstances` 最大秒数</span><span class="sxs-lookup"><span data-stu-id="ad686-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="ad686-128">以下标记要求在两次回发之间至少经过两秒钟的时间，并且在30秒的时间间隔内只有5次回发或更少：</span><span class="sxs-lookup"><span data-stu-id="ad686-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

<span data-ttu-id="ad686-129">然后，请务必将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：</span><span class="sxs-lookup"><span data-stu-id="ad686-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

<span data-ttu-id="ad686-130">由于大部分检查 `NoBot` 都是在服务器端进行的，因此您需要检查这些验证的结果。</span><span class="sxs-lookup"><span data-stu-id="ad686-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="ad686-131">可以通过调用 `NoBot`的 `IsValid()` 方法来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="ad686-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="ad686-132">它有一个参数（作为 `out` 参数/`ByRef` 参数），该参数的类型为 `NoBotState`。</span><span class="sxs-lookup"><span data-stu-id="ad686-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="ad686-133">它的字符串表示形式包含检查失败的原因，否则 `Valid`。</span><span class="sxs-lookup"><span data-stu-id="ad686-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="ad686-134">下面的代码根据 `NoBot`的结果输出一条消息：</span><span class="sxs-lookup"><span data-stu-id="ad686-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

<span data-ttu-id="ad686-135">最后，需要提交一个窗体，并使用 label 元素输出该消息，并且已完成！</span><span class="sxs-lookup"><span data-stu-id="ad686-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

<span data-ttu-id="ad686-136">如果在前两秒内运行此脚本并停用 JavaScript 或提交窗体，或在三十秒内提交窗体7次，将收到一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="ad686-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="ad686-137">不过，请明智地使用此控制，因为只有大约90-95% 的用户激活了 JavaScript，因此5-10% 的用户将 `NoBot`的测试失败。</span><span class="sxs-lookup"><span data-stu-id="ad686-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>

<span data-ttu-id="ad686-138">[![此错误消息可能是由机器人引起的](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ad686-138">[![This error message could have been caused by a bot](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span></span>

<span data-ttu-id="ad686-139">此错误消息可能是由机器人引起的（[单击查看完全大小的映像](fighting-bots-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="ad686-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ad686-140">下一部分</span><span class="sxs-lookup"><span data-stu-id="ad686-140">Next</span></span>](fighting-bots-vb.md)
