---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 动态添加折叠窗格（C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常是用 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 2834f56bd77c412923f4a8f382e670727f70eae4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607259"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a>动态添加折叠窗格（C#）

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)

> AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常在页面本身内进行声明，但可以使用服务器端代码来实现相同的结果。

## <a name="overview"></a>概述

AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常在页面本身内进行声明，但可以使用服务器端代码来实现相同的结果。

## <a name="steps"></a>步骤

此折叠控件向服务器端代码公开所有重要属性。 在其他情况下，`Panes` 属性授予对组成可折叠面板的窗格的集合的访问权限。 每个窗格都有类型 `AccordionPane`。 因此，创建此类窗格非常简单：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

`AccordionPane` 的 `HeaderContainer` 属性提供对窗格的标头部分内 ASP.NET 控件的访问;`AccordionPane` 的 `ContentContainer` 属性对窗格的内容部分执行相同的工作。 这允许 ASP.NET 代码向窗格中添加内容：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

最后，必须将窗格添加到折叠的 `Panes` 集合中：

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

下面是一个完整的服务器端代码，它将两个窗格添加到折叠控件：

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

唯一缺少的元素是可折叠元素本身，它取决于是否存在 ASP.NET `ScriptManager` 控件：

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

若要完成此示例，可折叠面板控件中引用的两个 CSS 类提供了浏览器的样式信息：

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

[![了服务器端代码动态添加了折叠面板中的数据](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)

折叠后的数据是由服务器端代码动态添加的（[单击查看完全大小的映像](dynamically-adding-an-accordion-pane-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](databinding-to-an-accordion-cs.md)
> [下一页](databinding-to-an-accordion-vb.md)
