---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 从服务器端修改动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画还可能 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 0594efea9598a6c2461a72f789b5bd5f8ece23da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483890"
---
# <a name="modifying-animations-from-the-server-side-c"></a>从服务器端修改动画（C#）

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画还可以在服务器端进行更改

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画还可以在服务器端进行更改

## <a name="steps"></a>步骤

首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

动画将应用于文本面板，如下所示：

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

其余代码在服务器端运行，不使用标记;相反，它使用代码创建 `AnimationExtender` 控件：

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

不过，控件工具包当前不提供用于创建各个动画的 API 访问权限。 不过，可以将 `AnimationExtender`的动画属性设置为包含以声明方式分配动画时使用的 XML 标记的字符串。 若要创建不能包含 `<Animations>` 元素的 XML，可以使用 .NET Framework 的 XML 支持，如以下代码所示，只需提供字符串：

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

最后，将 `AnimationExtender` 控件添加到 `<form runat="server">` 元素中的当前页，确保包含并运行动画：

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]

[![使用服务器端C#/VB 代码创建动画](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)

动画是使用服务器端C#/VB 代码创建的（[单击查看完全大小的映像](modifying-animations-from-the-server-side-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](triggering-an-animation-in-another-control-cs.md)
> [下一页](executing-animations-using-client-side-code-cs.md)
