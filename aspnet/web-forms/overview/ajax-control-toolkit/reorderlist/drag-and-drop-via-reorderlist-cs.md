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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611480"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="f6da1-104">通过 ReorderList 进行拖放 (C#)</span><span class="sxs-lookup"><span data-stu-id="f6da1-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="f6da1-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f6da1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f6da1-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f6da1-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="f6da1-107">AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。</span><span class="sxs-lookup"><span data-stu-id="f6da1-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="f6da1-108">列表的当前顺序应保留在服务器上。</span><span class="sxs-lookup"><span data-stu-id="f6da1-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="f6da1-109">概述</span><span class="sxs-lookup"><span data-stu-id="f6da1-109">Overview</span></span>

<span data-ttu-id="f6da1-110">AJAX 控件工具包中的 `ReorderList` 控件提供了一个列表，用户可以通过拖放将该列表重新排序。</span><span class="sxs-lookup"><span data-stu-id="f6da1-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="f6da1-111">列表的当前顺序应保留在服务器上。</span><span class="sxs-lookup"><span data-stu-id="f6da1-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="f6da1-112">步骤</span><span class="sxs-lookup"><span data-stu-id="f6da1-112">Steps</span></span>

<span data-ttu-id="f6da1-113">`ReorderList` 控件支持将数据库中的数据绑定到列表。</span><span class="sxs-lookup"><span data-stu-id="f6da1-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="f6da1-114">最重要的是，它还支持将 list 元素的顺序更改回数据存储区。</span><span class="sxs-lookup"><span data-stu-id="f6da1-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="f6da1-115">此示例使用 Microsoft SQL Server 2005 Express Edition 作为数据存储。</span><span class="sxs-lookup"><span data-stu-id="f6da1-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="f6da1-116">数据库是 Visual Studio 安装（包括 express edition）的可选（免费）部分。</span><span class="sxs-lookup"><span data-stu-id="f6da1-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="f6da1-117">它还可作为单独的下载[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下。</span><span class="sxs-lookup"><span data-stu-id="f6da1-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="f6da1-118">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="f6da1-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="f6da1-119">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="f6da1-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="f6da1-120">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ）。</span><span class="sxs-lookup"><span data-stu-id="f6da1-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="f6da1-121">连接到服务器，双击 "`Databases`" 并创建一个新数据库（右键单击，然后选择 "`New Database`）" `Tutorials`"。</span><span class="sxs-lookup"><span data-stu-id="f6da1-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="f6da1-122">在此数据库中，使用以下四列创建名为 `AJAX` 的新表：</span><span class="sxs-lookup"><span data-stu-id="f6da1-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="f6da1-123">`id` （primary key，integer，identity，not NULL）</span><span class="sxs-lookup"><span data-stu-id="f6da1-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="f6da1-124">`char` （char （1），NULL）</span><span class="sxs-lookup"><span data-stu-id="f6da1-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="f6da1-125">`description` （varchar （50），NULL）</span><span class="sxs-lookup"><span data-stu-id="f6da1-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="f6da1-126">`position` （int，NULL）</span><span class="sxs-lookup"><span data-stu-id="f6da1-126">`position` (int, NULL)</span></span>

<span data-ttu-id="f6da1-127">[![AJAX 表的布局](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f6da1-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="f6da1-128">AJAX 表的布局（[单击以查看完全大小的图像](drag-and-drop-via-reorderlist-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="f6da1-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="f6da1-129">接下来，使用几个值来填充表。</span><span class="sxs-lookup"><span data-stu-id="f6da1-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="f6da1-130">请注意，`position` 列保存元素的排序顺序。</span><span class="sxs-lookup"><span data-stu-id="f6da1-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="f6da1-131">[![AJAX 表中的初始数据](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f6da1-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="f6da1-132">AJAX 表中的初始数据（[单击以查看完全大小的图像](drag-and-drop-via-reorderlist-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="f6da1-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="f6da1-133">下一步需要生成 `SqlDataSource` 控件来与新数据库及其表进行通信。</span><span class="sxs-lookup"><span data-stu-id="f6da1-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="f6da1-134">数据源必须支持 `SELECT` 和 `UPDATE` SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="f6da1-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="f6da1-135">以后更改列表元素的顺序时，`ReorderList` 控件会自动将两个值提交到数据源的 `Update` 命令：新位置和元素的 ID。</span><span class="sxs-lookup"><span data-stu-id="f6da1-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="f6da1-136">因此，对于这两个值，数据源需要 `<UpdateParameters>` 部分：</span><span class="sxs-lookup"><span data-stu-id="f6da1-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="f6da1-137">`ReorderList` 控件需要设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="f6da1-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="f6da1-138">`AllowReorder`：是否可以重新排列列表项</span><span class="sxs-lookup"><span data-stu-id="f6da1-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="f6da1-139">`DataSourceID`：数据源的 ID</span><span class="sxs-lookup"><span data-stu-id="f6da1-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="f6da1-140">`DataKeyField`：数据源中主键列的名称</span><span class="sxs-lookup"><span data-stu-id="f6da1-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="f6da1-141">`SortOrderField`：为列表项提供排序顺序的数据源列</span><span class="sxs-lookup"><span data-stu-id="f6da1-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="f6da1-142">在 "`<DragHandleTemplate>`" 和 "`<ItemTemplate>`" 部分中，可对列表的布局进行微调。</span><span class="sxs-lookup"><span data-stu-id="f6da1-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="f6da1-143">此外，还可以使用 `Eval()` 方法进行数据绑定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f6da1-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="f6da1-144">以下 CSS 样式信息（在 `ReorderList` 控件的 "`<DragHandleTemplate>`" 部分中引用）可确保鼠标指针悬停在拖动控点上时进行适当的更改：</span><span class="sxs-lookup"><span data-stu-id="f6da1-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="f6da1-145">最后，`ScriptManager` 控件初始化页面的 ASP.NET AJAX：</span><span class="sxs-lookup"><span data-stu-id="f6da1-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="f6da1-146">在浏览器中运行此示例，并对列表项进行一点重新排列。</span><span class="sxs-lookup"><span data-stu-id="f6da1-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="f6da1-147">然后，重新加载页面，并/或查看数据库。</span><span class="sxs-lookup"><span data-stu-id="f6da1-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="f6da1-148">更改的位置已被保留，并且还会通过数据库中 `position` 列中的值来反映，并且没有任何代码，只需使用标记。</span><span class="sxs-lookup"><span data-stu-id="f6da1-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="f6da1-149">[![数据库中的数据会根据新的列表项顺序进行更改](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f6da1-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="f6da1-150">数据库中的数据会根据新的列表项顺序进行更改（[单击查看完全大小的图像](drag-and-drop-via-reorderlist-cs/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="f6da1-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f6da1-151">[上一页](using-postbacks-with-reorderlist-cs.md)
> [下一页](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f6da1-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
