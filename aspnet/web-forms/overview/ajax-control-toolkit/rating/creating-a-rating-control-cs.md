---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 创建分级控件（C#） |Microsoft Docs
author: wenz
description: 许多网站（从电子商务到社区站点）都提供了对文章或项目进行评级的用户。 这通常需要进行一些编码工作，但我们有 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611584"
---
# <a name="creating-a-rating-control-c"></a>创建分级控件 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)

> 许多网站（从电子商务到社区站点）都提供了对文章或项目进行评级的用户。 这通常需要进行一些编码工作，但我们会提供控制工具包来处理。

## <a name="overview"></a>概述

许多网站（从电子商务到社区站点）都提供了对文章或项目进行评级的用户。 这通常需要进行一些编码工作，但我们会提供控制工具包来处理。

## <a name="steps"></a>步骤

首先，你至少需要两种类型的映像：一个用于填写分级项，一个用于空分级项。 分级项通常为星形或笑脸。 对于这种情况，可在本教程的源代码下载内容中找到三个文件： "笑脸" 和 ".png" 和 "smiley-done"。

然后，创建一个新的 ASP.NET 文件，并从向其添加 `ScriptManager` 控件开始：

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

然后，从 ASP.NET AJAX 控件工具包添加 `Rating` 控件。 需要为此示例设置以下属性：

- `CurrentRating` 要使用的初始分级
- `MaxRating` 最大分级
- `EmptyStarCssClass` 要在分级项（星号）为空时使用的 CSS 类
- `FilledStarCssClass` 填写分级项（星号）时要使用的 CSS 类
- `StarCssClass` 要用于可见状态的 CSS 类
- `WaitingStarCssClass` 在向服务器发送星型分级时要使用的 CSS 类

下面是用于创建分级控件的标记，其中五个项（smileys）最初未填写：

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

这三个引用的 CSS 类现在需要显示适当的图像文件，这是使用 CSS 轻松完成的：

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

请确保提供三个图像的宽度和高度，否则显示可能会混乱了 ...。

最后，应向用户显示分级的结果（或者至少保存在数据库中）。 因此，请为文本消息的输出添加标签，并添加一个 "提交" 按钮，以将评分形式回发到服务器：

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

在服务器端代码中，通过其 `ID` 访问分级控制，然后访问其 `CurrentRating` 属性，该属性是所选分级项的编号，在本例中为0到5之间的值。

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

保存页面并将其加载到浏览器中。 当你将鼠标悬停在（初始为空）分级项上时，将发生 JavaScript 影响：评级发生变化。 单击星形组后，将保留当前评级。 最后，当你提交窗体时，服务器端代码会输出所选评级。

[![使用最小代码创建分级系统](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)

使用最小代码创建分级系统（[单击以查看完全大小的图像](creating-a-rating-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一页](creating-a-rating-control-vb.md)
