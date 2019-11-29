---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: 在 Repeater 中使用 ConfirmButton （C#） |Microsoft Docs
author: wenz
description: 当用户单击按钮（包括 LinkButton 控件）时，AJAX 控件工具包中的 ConfirmButton 扩展器将创建 "是/否" 弹出窗口。 仅在 "是" 时 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 468a830f01c48dc39b22bc5d826f80533df65c1a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574392"
---
# <a name="using-a-confirmbutton-in-a-repeater-c"></a><span data-ttu-id="91379-104">在 Repeater 中使用 ConfirmButton (C#)</span><span class="sxs-lookup"><span data-stu-id="91379-104">Using a ConfirmButton In a Repeater (C#)</span></span>

<span data-ttu-id="91379-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="91379-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="91379-106">[下载代码](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="91379-106">[Download Code](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span></span>

> <span data-ttu-id="91379-107">当用户单击按钮（包括 LinkButton 控件）时，AJAX 控件工具包中的 ConfirmButton 扩展器将创建 "是/否" 弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="91379-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="91379-108">仅当单击 "是" 时，才会执行该按钮的操作，否则取消该操作。</span><span class="sxs-lookup"><span data-stu-id="91379-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="91379-109">这也可能出现在中继器中。</span><span class="sxs-lookup"><span data-stu-id="91379-109">This is also possible in a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="91379-110">概述</span><span class="sxs-lookup"><span data-stu-id="91379-110">Overview</span></span>

<span data-ttu-id="91379-111">当用户单击按钮（包括 LinkButton 控件）时，AJAX 控件工具包中的 ConfirmButton 扩展器将创建 "是/否" 弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="91379-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="91379-112">仅当单击 "是" 时，才会执行该按钮的操作，否则取消该操作。</span><span class="sxs-lookup"><span data-stu-id="91379-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="91379-113">这也可能出现在中继器中。</span><span class="sxs-lookup"><span data-stu-id="91379-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="91379-114">步骤</span><span class="sxs-lookup"><span data-stu-id="91379-114">Steps</span></span>

<span data-ttu-id="91379-115">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="91379-115">First of all, a data source is required.</span></span> <span data-ttu-id="91379-116">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="91379-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="91379-117">数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。</span><span class="sxs-lookup"><span data-stu-id="91379-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="91379-118">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。</span><span class="sxs-lookup"><span data-stu-id="91379-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="91379-119">最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="91379-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="91379-120">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="91379-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="91379-121">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="91379-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="91379-122">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="91379-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

<span data-ttu-id="91379-123">然后需要数据源。</span><span class="sxs-lookup"><span data-stu-id="91379-123">Then, a data source is required.</span></span> <span data-ttu-id="91379-124">为了简单起见，只检索 AdventureWorks 的 "供应商" 表中的前五个条目。</span><span class="sxs-lookup"><span data-stu-id="91379-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="91379-125">请注意，使用 Visual Studio 向导创建数据源时，表名称（`Vendors`）当前没有正确地以 `Purchasing`为前缀。</span><span class="sxs-lookup"><span data-stu-id="91379-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="91379-126">以下标记是正确的：</span><span class="sxs-lookup"><span data-stu-id="91379-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

<span data-ttu-id="91379-127">然后，可以在中继器内使用此数据源。</span><span class="sxs-lookup"><span data-stu-id="91379-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="91379-128">与往常一样，`DataBinder.Eval()` 方法从数据源中检索数据。</span><span class="sxs-lookup"><span data-stu-id="91379-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="91379-129">然后，必须将 `ConfirmButtonExtender` 控件放置在 repeater 的 `<ItemTemplate>` 部分中，以便将其显示在数据源中的每个条目中。</span><span class="sxs-lookup"><span data-stu-id="91379-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]

<span data-ttu-id="91379-130">[!["确认" 按钮显示在数据源中的每个条目旁边](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="91379-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)</span></span>

<span data-ttu-id="91379-131">"确认" 按钮显示在数据源中的每个条目旁边（[单击以查看完全大小的图像](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="91379-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="91379-132">下一页</span><span class="sxs-lookup"><span data-stu-id="91379-132">Next</span></span>](using-a-confirmbutton-in-a-repeater-vb.md)
