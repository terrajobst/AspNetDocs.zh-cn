---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: 从不带 UpdatePanel 的弹出控件处理回发（C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 当在 su 中发生回发时 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496502"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>使用没有 UpdatePanel 的弹出控件处理回发 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 如果在这种面板中发生回发，并且页面上有多个面板，则很难确定单击了哪个面板。

## <a name="overview"></a>概述

AJAX 控件工具包中的 PopupControl 扩展器提供了一种简单的方法，可在激活任何其他控件时触发弹出窗口。 如果在这种面板中发生回发，并且页面上有多个面板，则很难确定单击了哪个面板。

## <a name="steps"></a>步骤

将 `PopupControl` 与回发一起使用时，如果没有在页面上 `UpdatePanel`，则控制工具包不会提供一种方法来确定哪些客户端元素触发了弹出窗口，进而导致回发。 不过，小型技巧为此方案提供了解决方法。

首先，这是基本设置：两个文本框，两个文本框都触发同一 popup，即一个日历。 两 `PopupControlExtenders` 将文本框和弹出窗口一起显示。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

基本思路是在 &lt;`form`&gt; 元素中添加一个隐藏的窗体字段，该元素包含启动弹出窗口的文本框：

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

加载页面时，JavaScript 代码会将事件处理程序添加到这两个文本框：每当用户单击文本框时，其名称将写入隐藏的窗体字段：

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

在服务器端代码中，必须读取隐藏字段的值。 由于隐藏的表单字段进行了一些无关紧要操作，一种允许列表方法验证隐藏的值是必需的。 标识正确的文本框后，会将日历中的日期写入该文本框。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[当用户单击文本框时，将显示日历 ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

当用户在文本框中单击时，将显示该日历（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)）

[![单击日期会将其放在文本框中。](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

单击某个日期会将其放在文本框中（[单击以查看完全大小的图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)）

> [!div class="step-by-step"]
> [上一页](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [下一页](using-multiple-popup-controls-vb.md)
