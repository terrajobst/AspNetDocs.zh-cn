---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: 带有 CascadingDropDown 的 cascadingdropdown 预设置列表项（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483806"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a>使用 CascadingDropDown 预设置列表条目 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 使用少量代码，就可以在动态加载数据后预先选择列表元素。

## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 （例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）使用少量代码，就可以在动态加载数据后预先选择列表元素。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

然后，需要 DropDownList 控件：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

在此列表中，添加了一个 CascadingDropDown 扩展程序，提供了 web 服务 URL 和方法信息：

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

然后，CascadingDropDown 扩展器使用以下方法签名异步调用 web 服务：

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

方法返回类型为 CascadingDropDown 的数组。 类型的构造函数首先需要列表项的标题，然后需要值（HTML `value` 特性）。 如果第三个参数设置为 true，则会在浏览器中自动选择列表元素。

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

在浏览器中加载页面将在下拉列表中填充三个供应商，第二个供应商正在预选择。

[![自动填充列表并自动预选](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

此列表是自动填充的（[单击以查看完全大小的图像](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](using-cascadingdropdown-with-a-database-vb.md)
> [下一页](using-auto-postback-with-cascadingdropdown-vb.md)
