---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: 使用 UpdatePanel 的弹出控件处理回发（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 需要特别小心 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496634"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a>使用带 UpdatePanel 的弹出控件处理回发 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)

> AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 在此类弹出窗口中发生回发时，必须特别小心。

## <a name="overview"></a>概述

AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 在此类弹出窗口中发生回发时，必须特别小心。

## <a name="steps"></a>步骤

将 `PopupControl` 与回发一起使用时，`UpdatePanel` 可以防止由回发导致的页刷新。 以下标记定义了几个重要元素：

- `ScriptManager` 控件以便 ASP.NET AJAX 控件工具包工作
- 两个 `TextBox` 的控件，它们都将触发弹出窗口
- 将用作弹出窗口的 `Panel` 控件
- 在面板中，`Calendar` 控件嵌入 `UpdatePanel` 控件中
- 两个将面板分配给文本框的 `PopupControlExtender` 控件

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

请注意，将设置 `Calendar` 控件的 `OnSelectionChanged` 属性。 因此，当用户选择日历中的日期时，将发生回发并执行服务器端方法 `c1_SelectionChanged()`。 在该方法中，必须检索当前日期并将其写回文本框。

的语法如下所示：首先，必须为页上的 `PopupControlExtender` 生成代理对象。 ASP.NET AJAX 控件工具包提供 `GetProxyForCurrentPopup()` 方法。 此方法返回的对象支持 `Commit()` 方法，该方法将值发送回触发弹出窗口的控件（而不是触发方法调用的控件！）。 下面的代码将所选日期提供为 `Commit()` 方法的参数，从而使代码将所选日期写回文本框：

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

现在，只要单击日历日期，所选日期就会显示在关联的文本框中，创建当前可以在许多网站上找到的日期选取器控件。

[当用户单击文本框时，将显示日历 ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)

当用户在文本框中单击时，将显示该日历（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png)）

[![单击日期会将其放在文本框中。](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)

单击某个日期会将其放在文本框中（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png)）

> [!div class="step-by-step"]
> [上一页](using-multiple-popup-controls-vb.md)
> [下一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)
