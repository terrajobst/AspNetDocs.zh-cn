---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: 通过 ReorderList （VB）进行拖放 |Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f7c5749053d8bf587467fb1939fca05ce2872a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598657"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="8b728-103">通过 ReorderList 进行拖放 (VB)</span><span class="sxs-lookup"><span data-stu-id="8b728-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="8b728-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8b728-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8b728-105">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8b728-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="8b728-106">AJAX 控件工具包中的 ReorderList 控件提供了一个列表，用户可以通过拖放将该列表重新排序。</span><span class="sxs-lookup"><span data-stu-id="8b728-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8b728-107">列表的当前顺序应保留在服务器上。</span><span class="sxs-lookup"><span data-stu-id="8b728-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="8b728-108">概述</span><span class="sxs-lookup"><span data-stu-id="8b728-108">Overview</span></span>

<span data-ttu-id="8b728-109">AJAX 控件工具包中的 `ReorderList` 控件提供了一个列表，用户可以通过拖放将该列表重新排序。</span><span class="sxs-lookup"><span data-stu-id="8b728-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8b728-110">列表的当前顺序应保留在服务器上。</span><span class="sxs-lookup"><span data-stu-id="8b728-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="8b728-111">步骤</span><span class="sxs-lookup"><span data-stu-id="8b728-111">Steps</span></span>

<span data-ttu-id="8b728-112">`ReorderList` 控件支持将数据库中的数据绑定到列表。</span><span class="sxs-lookup"><span data-stu-id="8b728-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="8b728-113">最重要的是，它还支持将 list 元素的顺序更改回数据存储区。</span><span class="sxs-lookup"><span data-stu-id="8b728-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="8b728-114">此示例使用 Microsoft SQL Server 2005 Express Edition 作为数据存储。</span><span class="sxs-lookup"><span data-stu-id="8b728-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="8b728-115">数据库是 Visual Studio 安装（包括 express edition）的可选（免费）部分。</span><span class="sxs-lookup"><span data-stu-id="8b728-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="8b728-116">它还可作为单独的下载[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下。</span><span class="sxs-lookup"><span data-stu-id="8b728-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="8b728-117">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="8b728-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="8b728-118">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="8b728-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="8b728-119">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ）。</span><span class="sxs-lookup"><span data-stu-id="8b728-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="8b728-120">连接到服务器，双击 "`Databases`" 并创建一个新数据库（右键单击，然后选择 "`New Database`）" `Tutorials`"。</span><span class="sxs-lookup"><span data-stu-id="8b728-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="8b728-121">在此数据库中，使用以下四列创建名为 `AJAX` 的新表：</span><span class="sxs-lookup"><span data-stu-id="8b728-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="8b728-122">`id` （primary key，integer，identity，not NULL）</span><span class="sxs-lookup"><span data-stu-id="8b728-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="8b728-123">`char` （char （1），NULL）</span><span class="sxs-lookup"><span data-stu-id="8b728-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="8b728-124">`description` （varchar （50），NULL）</span><span class="sxs-lookup"><span data-stu-id="8b728-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="8b728-125">`position` （int，NULL）</span><span class="sxs-lookup"><span data-stu-id="8b728-125">`position` (int, NULL)</span></span>

<span data-ttu-id="8b728-126">[![AJAX 表的布局](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8b728-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="8b728-127">AJAX 表的布局（[单击以查看完全大小的图像](drag-and-drop-via-reorderlist-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="8b728-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="8b728-128">接下来，使用几个值来填充表。</span><span class="sxs-lookup"><span data-stu-id="8b728-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="8b728-129">请注意，`position` 列保存元素的排序顺序。</span><span class="sxs-lookup"><span data-stu-id="8b728-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="8b728-130">[![AJAX 表中的初始数据](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8b728-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="8b728-131">AJAX 表中的初始数据（[单击以查看完全大小的图像](drag-and-drop-via-reorderlist-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="8b728-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="8b728-132">下一步需要生成 `SqlDataSource` 控件来与新数据库及其表进行通信。</span><span class="sxs-lookup"><span data-stu-id="8b728-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="8b728-133">数据源必须支持 `SELECT` 和 `UPDATE` SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="8b728-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="8b728-134">以后更改列表元素的顺序时，`ReorderList` 控件会自动将两个值提交到数据源的 `Update` 命令：新位置和元素的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b728-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="8b728-135">因此，对于这两个值，数据源需要 `<UpdateParameters>` 部分：</span><span class="sxs-lookup"><span data-stu-id="8b728-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="8b728-136">`ReorderList` 控件需要设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="8b728-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="8b728-137">`AllowReorder`：是否可以重新排列列表项</span><span class="sxs-lookup"><span data-stu-id="8b728-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="8b728-138">`DataSourceID`：数据源的 ID</span><span class="sxs-lookup"><span data-stu-id="8b728-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="8b728-139">`DataKeyField`：数据源中主键列的名称</span><span class="sxs-lookup"><span data-stu-id="8b728-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="8b728-140">`SortOrderField`：为列表项提供排序顺序的数据源列</span><span class="sxs-lookup"><span data-stu-id="8b728-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="8b728-141">在 "`<DragHandleTemplate>`" 和 "`<ItemTemplate>`" 部分中，可对列表的布局进行微调。</span><span class="sxs-lookup"><span data-stu-id="8b728-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="8b728-142">此外，还可以使用 `Eval()` 方法进行数据绑定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8b728-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="8b728-143">以下 CSS 样式信息（在 `ReorderList` 控件的 "`<DragHandleTemplate>`" 部分中引用）可确保鼠标指针悬停在拖动控点上时进行适当的更改：</span><span class="sxs-lookup"><span data-stu-id="8b728-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="8b728-144">最后，`ScriptManager` 控件初始化页面的 ASP.NET AJAX：</span><span class="sxs-lookup"><span data-stu-id="8b728-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="8b728-145">在浏览器中运行此示例，并对列表项进行一点重新排列。</span><span class="sxs-lookup"><span data-stu-id="8b728-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="8b728-146">然后，重新加载页面，并/或查看数据库。</span><span class="sxs-lookup"><span data-stu-id="8b728-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="8b728-147">更改的位置已被保留，并且还会通过数据库中 `position` 列中的值来反映，并且没有任何代码，只需使用标记。</span><span class="sxs-lookup"><span data-stu-id="8b728-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="8b728-148">[![数据库中的数据会根据新的列表项顺序进行更改](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8b728-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="8b728-149">数据库中的数据会根据新的列表项顺序进行更改（[单击查看完全大小的图像](drag-and-drop-via-reorderlist-vb/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="8b728-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8b728-150">上一部分</span><span class="sxs-lookup"><span data-stu-id="8b728-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
