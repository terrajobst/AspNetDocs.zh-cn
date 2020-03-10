---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: 通过 CascadingDropDown 使用自动回发（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 5dea23a20aba00af5109f05f18365b89e409a131
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430658"
---
# <a name="using-auto-postback-with-cascadingdropdown-vb"></a>通过 CascadingDropDown 使用自动回发 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 但是，在使用 CascadingDropDown 控件时，ASP。NET 的 DropDownList 控件的 AutoPostBack 功能不起作用，因为以异步方式将数据加载到列表中会生成（不必要的）回发本身。 利用一些 JavaScript 代码，可以避免这种影响。

## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 （例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）但是，在使用 CascadingDropDown 控件时，ASP。NET 的 DropDownList 控件的 AutoPostBack 功能不起作用，因为以异步方式将数据加载到列表中会生成（不必要的）回发本身。 利用一些 JavaScript 代码，可以避免这种影响。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 和控件工具包的功能，`ScriptManager` 控件必须置于页面上的任何位置（但在 &lt;`form`&gt; 元素中）：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

然后，需要 DropDownList 控件：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

在此列表中，添加了一个 CascadingDropDown 扩展程序，提供了 web 服务 URL 和方法信息：

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

然后，CascadingDropDown 扩展器使用以下方法签名异步调用 web 服务：

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

方法返回类型为 CascadingDropDown 的数组。 类型的构造函数首先需要列表项的标题，然后需要值（HTML `value` 特性）。

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

在浏览器中加载页面将在下拉列表中填充三个供应商，第二个供应商正在预选择。 此外，ASP.NET 还定义了 `__doPostBack()` JavaScript 方法。 加载页面后，此 JavaScript 调用会添加到下拉列表中，但仅当其中有元素时才会出现。 如果列表中没有元素，则说明控件工具包当前正在加载它们，因此 JavaScript 代码使用超时，并在半秒后再次尝试。

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

这样，仅当列表中有实际元素并且用户选择一个条目时，才会执行回发。

[选择列表元素 ![导致回发](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

选择列表元素会导致回发（[单击查看完全大小的映像](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](presetting-list-entries-with-cascadingdropdown-vb.md)
