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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611761"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a>仅允许在文本框中使用特定字符 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)

> ASP.NET 验证控件可以确保用户输入中仅允许某些字符。 但这仍不会阻止用户键入无效字符并尝试提交窗体。

## <a name="overview"></a>概述

ASP.NET 验证控件可以确保用户输入中仅允许某些字符。 但这仍不会阻止用户键入无效字符并尝试提交窗体。

## <a name="steps"></a>步骤

ASP.NET AJAX 控件工具包包含用于扩展文本框的 `FilteredTextBox` 控件。 激活后，只能在该字段中输入一组特定的字符。

为此，我们首先需要使用 ASP.NET AJAX `ScriptManager`，后者会加载 ASP.NET AJAX 控件工具包也使用的 JavaScript 库：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

接下来，我们需要一个文本框：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

最后，`FilteredTextBoxExtender` 控件负责限制允许用户键入的字符。 首先，将 `TargetControlID` 特性设置为 `TextBox` 控件的 `ID`。 然后，选择一个可用的 `FilterType` 值：

- `Custom` 默认值;必须提供有效字符的列表
- 仅 `LowercaseLetters` 小写字母
- 仅 `Numbers` 数字
- 仅 `UppercaseLetters` 大写字母

如果使用 `Custom FilterType`，则必须设置 `ValidChars` 属性，并提供可键入的字符列表。 顺便说一下，如果您尝试将文本粘贴到文本框中，则所有无效字符将被删除。

下面是仅允许数字的 `FilteredTextBoxExtender` 控件的标记（也可能是 `FilterType="Numbers"`的）：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

运行页，如果启用了 JavaScript，则尝试输入一个字母，否则它将不起作用;但会在页面上显示数字。 但请注意，保护 `FilteredTextBox` 提供的不是项目符号：如果启用了 JavaScript，则可以在文本框中输入任何数据，因此，必须使用其他验证方法，即 .ASP。NET 的验证控件。

[只能输入 ![位数](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)

只能输入数字（[单击以查看完全大小的图像](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一页](allowing-only-certain-characters-in-a-text-box-vb.md)
