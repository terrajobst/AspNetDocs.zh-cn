---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: 测试密码强度（C#） |Microsoft Docs
author: wenz
description: 几乎任何地方都需要密码，因此惰性用户往往会选择容易破解的简单密码。 ASP 中的 PasswordStrength 控件。N 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: e55eab9feebc18f39dd40c59cfb423208296b6c5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508964"
---
# <a name="testing-the-strength-of-a-password-c"></a>测试密码强度 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> 几乎任何地方都需要密码，因此惰性用户往往会选择容易破解的简单密码。 ASP.NET AJAX 控件工具包中的 PasswordStrength 控件可以检查密码的良好程度。

## <a name="overview"></a>概述

几乎任何地方都需要密码，因此惰性用户往往会选择容易破解的简单密码。 ASP.NET AJAX 控件工具包中的 `PasswordStrength` 控件可以检查密码的良好程度。

## <a name="steps"></a>步骤

`PasswordStrength` 控件将扩展文本框，并检查其中的密码是否足够好。 它通过属性提供丰富的选项;下面只是其中的一部分：

- 密码中所需的 `MinimumNumericCharacters` 最小数字字符数
- 密码中所需的最小符号字符数（不 `MinimumSymbolCharacters` 字母和数字）
- 密码 `PreferredPasswordLength` 最小长度
- `RequiresUpperAndLowerCaseCharacters` 密码是否需要使用大写和小写字符

`StrengthIndicatorType` 提供了有关如何以文本（值 `"Text"`）或一种进度栏（值 `"BarIndicator"`）表示密码强度的信息。 在 `DisplayPosition` 特性中，你将配置信息的显示位置。 下面是一个完整的示例，包括 ASP.NET AJAX `ScriptManager` 控件、`PasswordStrength` 控件，当然还有一个文本框，用户可以在其中输入密码。 出于演示的目的，后者窗体字段是一个常规文本字段，而不是密码字段，以便您可以在开发过程中查看所键入的内容。

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

运行页并键入：只有在输入小写字母、大写字母、数字和符号后，密码才被视为 unbreakable。

[![密码现在为（相当）](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

密码现在很好（[单击以查看完全大小的映像](testing-the-strength-of-a-password-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一部分](testing-the-strength-of-a-password-vb.md)
