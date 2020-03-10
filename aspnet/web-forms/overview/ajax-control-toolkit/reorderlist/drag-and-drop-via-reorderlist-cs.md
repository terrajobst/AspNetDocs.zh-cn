---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: 通过 ReorderList （C#） | 拖放 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 列表的当前顺序应为 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446006"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>通过 ReorderList 进行拖放 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 列表的当前顺序应保留在服务器上。

## <a name="overview"></a>概述

AJAX 控件工具包中的 `ReorderList` 控件提供了一个列表，用户可以通过拖放将该列表重新排序。 列表的当前顺序应保留在服务器上。

## <a name="steps"></a>步骤

`ReorderList` 控件支持将数据库中的数据绑定到列表。 最重要的是，它还支持将 list 元素的顺序更改回数据存储区。

此示例使用 Microsoft SQL Server 2005 Express Edition 作为数据存储。 数据库是 Visual Studio 安装（包括 express edition）的可选（免费）部分。 它还可作为单独的下载[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下。 对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。 如果你的设置不同，则必须修改数据库的连接信息。

设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ）。 连接到服务器，双击 "`Databases`" 并创建一个新数据库（右键单击，然后选择 "`New Database`）" `Tutorials`"。

在此数据库中，使用以下四列创建名为 `AJAX` 的新表：

- `id` （primary key，integer，identity，not NULL）
- `char` （char （1），NULL）
- `description` （varchar （50），NULL）
- `position` （int，NULL）

[![AJAX 表的布局](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX 表的布局（[单击以查看完全大小的图像](drag-and-drop-via-reorderlist-cs/_static/image3.png)）

接下来，使用几个值来填充表。 请注意，`position` 列保存元素的排序顺序。

[![AJAX 表中的初始数据](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX 表中的初始数据（[单击以查看完全大小的图像](drag-and-drop-via-reorderlist-cs/_static/image6.png)）

下一步需要生成 `SqlDataSource` 控件来与新数据库及其表进行通信。 数据源必须支持 `SELECT` 和 `UPDATE` SQL 命令。 以后更改列表元素的顺序时，`ReorderList` 控件会自动将两个值提交到数据源的 `Update` 命令：新位置和元素的 ID。 因此，对于这两个值，数据源需要 `<UpdateParameters>` 部分：

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` 控件需要设置以下属性：

- `AllowReorder`：是否可以重新排列列表项
- `DataSourceID`：数据源的 ID
- `DataKeyField`：数据源中主键列的名称
- `SortOrderField`：为列表项提供排序顺序的数据源列

在 "`<DragHandleTemplate>`" 和 "`<ItemTemplate>`" 部分中，可对列表的布局进行微调。 此外，还可以使用 `Eval()` 方法进行数据绑定，如下所示：

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

以下 CSS 样式信息（在 `ReorderList` 控件的 "`<DragHandleTemplate>`" 部分中引用）可确保鼠标指针悬停在拖动控点上时进行适当的更改：

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

最后，`ScriptManager` 控件初始化页面的 ASP.NET AJAX：

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

在浏览器中运行此示例，并对列表项进行一点重新排列。 然后，重新加载页面，并/或查看数据库。 更改的位置已被保留，并且还会通过数据库中 `position` 列中的值来反映，并且没有任何代码，只需使用标记。

[![数据库中的数据会根据新的列表项顺序进行更改](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

数据库中的数据会根据新的列表项顺序进行更改（[单击查看完全大小的图像](drag-and-drop-via-reorderlist-cs/_static/image9.png)）

> [!div class="step-by-step"]
> [上一页](using-postbacks-with-reorderlist-cs.md)
> [下一页](using-postbacks-with-reorderlist-vb.md)
