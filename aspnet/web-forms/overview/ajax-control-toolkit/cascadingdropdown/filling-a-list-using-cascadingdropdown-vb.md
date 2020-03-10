---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: 使用 CascadingDropDown 填充列表（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430730"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a>使用 CascadingDropDown 填充列表 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 （例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）首先要解决的问题是，使用此控件实际填写下拉列表。

## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 （例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）首先要解决的问题是，使用此控件实际填写下拉列表。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

然后，需要 DropDownList 控件：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

在此列表中，将添加 CascadingDropDown 扩展器。 它将向 web 服务发送一个异步请求，该请求随后将返回要在列表中显示的项的列表。 为此，需要设置以下 CascadingDropDown 属性：

- `ServicePath`：提供列表项的 web 服务的 URL
- `ServiceMethod`：传递列表项的 Web 方法
- `TargetControlID`：下拉列表的 ID
- `Category`：调用时提交到 web 方法的类别信息
- `PromptText`：从服务器异步加载列表数据时显示的文本

下面是 `CascadingDropDown` 元素的标记。 C#和 VB 的唯一区别是关联的 web 服务的名称：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

来自 `CascadingDropDown` 扩展器的 JavaScript 代码调用具有以下签名的 web 服务方法：

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

因此，该方法需要返回 `CascadingDropDownNameValue` 类型的数组（由 ASP.NET AJAX 控件工具包定义）。 在 `CascadingDropDownNameValue` 构造函数中，首先必须提供列表项的文本，然后提供其值，就像 `<option value="VALUE">NAME</option>` 在 HTML 中那样。 下面是一些示例数据：

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

在浏览器中加载页面将触发列表，并将其填充到三个供应商。

[![自动填充列表](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

将自动填充列表（[单击以查看完全大小的图像](filling-a-list-using-cascadingdropdown-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](using-auto-postback-with-cascadingdropdown-cs.md)
> [下一页](using-cascadingdropdown-with-a-database-vb.md)
