---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 使用带有 ReorderList （C#）的回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 每次重新排序列表时，po 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611405"
---
# <a name="using-postbacks-with-reorderlist-c"></a>通过 ReorderList 使用回发 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)

> AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 每次重新排序列表时，回发都应通知服务器发生了更改。

## <a name="overview"></a>概述

AJAX 控件工具包中的 `ReorderList` 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 每次重新排序列表时，回发都应通知服务器发生了更改。

## <a name="steps"></a>步骤

`ReorderList` 控件有多个可能的数据源。 一种是使用 `XmlDataSource` 控件：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

若要将此 XML 绑定到 `ReorderList` 控件并启用回发，必须设置以下属性：

- `DataSourceID`：数据源的 ID
- `SortOrderField`：作为排序依据的属性
- `AllowReorder`：是否允许用户对列表元素重新排序
- `PostBackOnReorder`：在重新排列列表时是否创建回发

下面是控件的相应标记：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

在 `ReorderList` 控件中，可以使用 `Eval()` 方法绑定数据源中的特定数据：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

在页面上的任意位置，标签将在上次重新排序发生时保存信息：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

此标签填充了服务器端代码中的文本，用于处理回发：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

最后，为了激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放在页面上：

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

[![每次重新排序都会触发回发](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

每次重新排序都会触发回发（[单击查看完全大小的映像](using-postbacks-with-reorderlist-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一页](drag-and-drop-via-reorderlist-cs.md)
