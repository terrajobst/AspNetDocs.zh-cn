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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508748"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>通过验证控件使用 TextBoxWatermark (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，它会被清空。 如果用户离开该框而不输入文本，则会重新出现预填充文本。 这可能会与同一页面上的 ASP.NET 验证控件发生冲突，但可能会解决这些问题。

## <a name="overview"></a>概述

AJAX 控件工具包中的 `TextBoxWatermark` 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，它会被清空。 如果用户离开该框而不输入文本，则会重新出现预填充文本。 这可能会与同一页面上的 ASP.NET 验证控件发生冲突，但可能会解决这些问题。

## <a name="steps"></a>步骤

示例的基本设置如下所示：使用 `TextBoxWatermarkExtender` 控件打水印 `TextBox` 控件。 按钮触发回发，稍后用于触发页面上的验证控件。 此外，还需要 `ScriptManager` 控件才能初始化 ASP.NET AJAX：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

现在，添加一个 `RequiredFieldValidator` 控件，该控件在提交窗体时检查字段中是否有文本。 验证程序的 `InitialValue` 属性必须设置为 `TextBoxWatermarkExtender` 控件中使用的相同值：提交窗体时，未更改文本框的值是其中的水印值：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

但这种方法存在一个问题：如果客户端禁用 JavaScript，则不会使用水印文本预填充文本字段，因此 `RequiredFieldValidator` 不会触发错误消息。 因此，第二个 `RequiredFieldValidator` 控件需要检查是否有空的文本框（省略 `InitialValue` 特性）。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

由于这两个验证程序使用 `Display`=`"Dynamic"`，因此最终用户无法区分这两个验证程序中触发的可视化外观;相反，它看起来只是其中的一个。

最后，如果没有验证程序发出错误消息，则添加一些服务器端代码以输出字段中的文本：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

[![验证器投诉原因在字段中没有文本](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

验证器投诉原因该字段中没有任何文本（[单击查看完全大小的图像](using-textboxwatermark-with-validation-controls-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](using-textboxwatermark-in-a-formview-vb.md)
