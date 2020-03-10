---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: 处理来自 ModalPopup （VB）的回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 如果需要特别注意，
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: df0b71b3e336a0d230869623473bdac24b3dd07b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504020"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a>通过 ModalPopup 处理回发 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 从弹出窗口中创建回发时，必须特别小心。

## <a name="overview"></a>概述

AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 从弹出窗口中创建回发时，必须特别小心。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

接下来，添加一个用于模式弹出窗口的面板。 在该处，用户可以输入名称和电子邮件地址。 按钮用于关闭弹出窗口并保存信息。 请注意，将设置 `OnClick` 特性，以便在单击此按钮时发生回发：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

该页本身包含两个标签，用于完全相同的信息：名称和电子邮件地址。 按钮用于触发模式弹出窗口：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

为了使弹出窗口出现，请添加 `ModalPopupExtender` 控件。 将 `PopupControlID` 特性设置为面板的 ID，并将 `TargetControlID` 到按钮的 ID：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

现在，每当单击模式弹出窗口中的 "`Save`" 按钮时，就会执行服务器端 `SaveData()` 方法。 在那里，可以将输入的数据保存在数据存储中。 为了简单起见，新数据只是在标签中输出：

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

此外，应用当前名称和电子邮件填充模式弹出窗口中的 textbox 控件。 但这仅在不发生回发时才是必需的。 如果有回发，ASP.NET viewstate 功能将自动使用适当的值填充文本框。

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

[![模式弹出窗口导致回发](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

模式弹出窗口导致回发（[单击查看完全大小的映像](handling-postbacks-from-a-modalpopup-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](using-modalpopup-with-a-repeater-control-vb.md)
> [下一页](positioning-a-modalpopup-vb.md)
