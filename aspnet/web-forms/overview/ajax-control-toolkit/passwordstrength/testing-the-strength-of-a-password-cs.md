---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: 测试强度的密码 (C#) |Microsoft Docs
author: wenz
description: 密码是必需几乎任意位置，以便延迟用户倾向于选择简单密码，这容易被破解。 在 ASP 中 PasswordStrength 控件。N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: d8ac50874d0325ed9583a16e1b4e19b3becabb99
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391508"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="6de38-104">测试密码强度 (C#)</span><span class="sxs-lookup"><span data-stu-id="6de38-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="6de38-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6de38-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6de38-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6de38-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="6de38-107">密码是必需几乎任意位置，以便延迟用户倾向于选择简单密码，这容易被破解。</span><span class="sxs-lookup"><span data-stu-id="6de38-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="6de38-108">ASP.NET AJAX 控件工具包中的 PasswordStrength 控件可以检查得再好密码。</span><span class="sxs-lookup"><span data-stu-id="6de38-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="6de38-109">概述</span><span class="sxs-lookup"><span data-stu-id="6de38-109">Overview</span></span>

<span data-ttu-id="6de38-110">密码是必需几乎任意位置，以便延迟用户倾向于选择简单密码，这容易被破解。</span><span class="sxs-lookup"><span data-stu-id="6de38-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="6de38-111">`PasswordStrength` ASP.NET AJAX 控件工具包中的控件可以检查得再好密码的信息。</span><span class="sxs-lookup"><span data-stu-id="6de38-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="6de38-112">步骤</span><span class="sxs-lookup"><span data-stu-id="6de38-112">Steps</span></span>

<span data-ttu-id="6de38-113">`PasswordStrength`控件扩展的文本框中，并检查是否已经足够好中它的密码。</span><span class="sxs-lookup"><span data-stu-id="6de38-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="6de38-114">它提供了丰富的属性，则通过选项以下是只是其中一些：</span><span class="sxs-lookup"><span data-stu-id="6de38-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- `MinimumNumericCharacters` <span data-ttu-id="6de38-115">密码中所需的数字字符的最小数量</span><span class="sxs-lookup"><span data-stu-id="6de38-115">minimum number of numeric characters required in the password</span></span>
- `MinimumSymbolCharacters` <span data-ttu-id="6de38-116">密码中所需的最小数量的符号字符 （不字母和数字）</span><span class="sxs-lookup"><span data-stu-id="6de38-116">minimum number of symbol characters (not letters and digits) required in the password</span></span>
- `PreferredPasswordLength` <span data-ttu-id="6de38-117">最小密码长度</span><span class="sxs-lookup"><span data-stu-id="6de38-117">minimum length of the password</span></span>
- `RequiresUpperAndLowerCaseCharacters` <span data-ttu-id="6de38-118">是否需使用大写和小写字符的密码</span><span class="sxs-lookup"><span data-stu-id="6de38-118">whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="6de38-119">`StrengthIndicatorType`提供的信息如何显示为文本的密码的强度 (值`"Text"`) 或作为一种类型的进度栏 (值`"BarIndicator"`)。</span><span class="sxs-lookup"><span data-stu-id="6de38-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="6de38-120">在`DisplayPosition`属性中，你将配置信息的显示位置。</span><span class="sxs-lookup"><span data-stu-id="6de38-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="6de38-121">下面是完整的示例，包括 ASP.NET AJAX`ScriptManager`控件，`PasswordStrength`控件和当然一个文本框，用户可能会在其中输入密码。</span><span class="sxs-lookup"><span data-stu-id="6de38-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="6de38-122">为了演示目的后, 一种形式字段是普通文本字段并不是密码字段，以便您可以看到在开发过程中您键入的内容。</span><span class="sxs-lookup"><span data-stu-id="6de38-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="6de38-123">运行页面，然后立即键入：仅输入小写字母、 大写字母、 数字和符号后，密码会被确认为不可换行。</span><span class="sxs-lookup"><span data-stu-id="6de38-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


[![N<span data-ttu-id="6de38-124">ow 密码适合 （非常）]</span><span class="sxs-lookup"><span data-stu-id="6de38-124">ow the password is (quite) good]</span></span>(testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

<span data-ttu-id="6de38-125">现在，密码是 （非常） 很好 ([单击此项可查看原尺寸图像](testing-the-strength-of-a-password-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6de38-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6de38-126">下一步</span><span class="sxs-lookup"><span data-stu-id="6de38-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
