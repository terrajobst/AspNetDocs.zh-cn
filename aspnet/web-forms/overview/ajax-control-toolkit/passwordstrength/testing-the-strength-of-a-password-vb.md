---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: 测试密码强度（VB） |Microsoft Docs
author: wenz
description: 几乎任何地方都需要密码，因此惰性用户往往会选择容易破解的简单密码。 ASP 中的 PasswordStrength 控件。N 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508970"
---
# <a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="fb4ff-104">测试密码强度 (VB)</span><span class="sxs-lookup"><span data-stu-id="fb4ff-104">Testing the Strength of a Password (VB)</span></span>

<span data-ttu-id="fb4ff-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fb4ff-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fb4ff-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fb4ff-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="fb4ff-107">几乎任何地方都需要密码，因此惰性用户往往会选择容易破解的简单密码。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="fb4ff-108">ASP.NET AJAX 控件工具包中的 PasswordStrength 控件可以检查密码的良好程度。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="fb4ff-109">概述</span><span class="sxs-lookup"><span data-stu-id="fb4ff-109">Overview</span></span>

<span data-ttu-id="fb4ff-110">几乎任何地方都需要密码，因此惰性用户往往会选择容易破解的简单密码。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="fb4ff-111">ASP.NET AJAX 控件工具包中的 `PasswordStrength` 控件可以检查密码的良好程度。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="fb4ff-112">步骤</span><span class="sxs-lookup"><span data-stu-id="fb4ff-112">Steps</span></span>

<span data-ttu-id="fb4ff-113">`PasswordStrength` 控件将扩展文本框，并检查其中的密码是否足够好。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="fb4ff-114">它通过属性提供丰富的选项;下面只是其中的一部分：</span><span class="sxs-lookup"><span data-stu-id="fb4ff-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="fb4ff-115">密码中所需的 `MinimumNumericCharacters` 最小数字字符数</span><span class="sxs-lookup"><span data-stu-id="fb4ff-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="fb4ff-116">密码中所需的最小符号字符数（不 `MinimumSymbolCharacters` 字母和数字）</span><span class="sxs-lookup"><span data-stu-id="fb4ff-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="fb4ff-117">密码 `PreferredPasswordLength` 最小长度</span><span class="sxs-lookup"><span data-stu-id="fb4ff-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="fb4ff-118">`RequiresUpperAndLowerCaseCharacters` 密码是否需要使用大写和小写字符</span><span class="sxs-lookup"><span data-stu-id="fb4ff-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="fb4ff-119">`StrengthIndicatorType` 提供了有关如何以文本（值 `"Text"`）或一种进度栏（值 `"BarIndicator"`）表示密码强度的信息。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="fb4ff-120">在 `DisplayPosition` 特性中，你将配置信息的显示位置。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="fb4ff-121">下面是一个完整的示例，包括 ASP.NET AJAX `ScriptManager` 控件、`PasswordStrength` 控件，当然还有一个文本框，用户可以在其中输入密码。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="fb4ff-122">出于演示的目的，后者窗体字段是一个常规文本字段，而不是密码字段，以便您可以在开发过程中查看所键入的内容。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="fb4ff-123">运行页并键入：只有在输入小写字母、大写字母、数字和符号后，密码才被视为 unbreakable。</span><span class="sxs-lookup"><span data-stu-id="fb4ff-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="fb4ff-124">[![密码现在为（相当）](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fb4ff-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="fb4ff-125">密码现在很好（[单击以查看完全大小的映像](testing-the-strength-of-a-password-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="fb4ff-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fb4ff-126">上一页</span><span class="sxs-lookup"><span data-stu-id="fb4ff-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)
