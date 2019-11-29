---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: 将通过 hovermenu 用于 Repeater 控件（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的通过 hovermenu 控件提供了一个简单的弹出效果：当鼠标指针悬停在某个元素上时，将在特定上出现一个弹出窗口 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9386aa2fe3a6174bbed52218337107733cb1fa99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606669"
---
# <a name="using-hovermenu-with-a-repeater-control-vb"></a><span data-ttu-id="b4854-103">通过 Repeater 控件使用 HoverMenu (VB)</span><span class="sxs-lookup"><span data-stu-id="b4854-103">Using HoverMenu with a Repeater Control (VB)</span></span>

<span data-ttu-id="b4854-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b4854-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b4854-105">[下载代码](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b4854-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span></span>

> <span data-ttu-id="b4854-106">AJAX 控件工具包中的通过 hovermenu 控件提供了一个简单的弹出效果：当鼠标指针悬停在某个元素上时，将在指定位置显示一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="b4854-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="b4854-107">还可以在 repeater 中使用此控件。</span><span class="sxs-lookup"><span data-stu-id="b4854-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="b4854-108">概述</span><span class="sxs-lookup"><span data-stu-id="b4854-108">Overview</span></span>

<span data-ttu-id="b4854-109">AJAX 控件工具包中的 `HoverMenu` 控件提供了一个简单的弹出效果：当鼠标指针悬停在某个元素上时，将在指定位置显示一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="b4854-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="b4854-110">还可以在 repeater 中使用此控件。</span><span class="sxs-lookup"><span data-stu-id="b4854-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="b4854-111">步骤</span><span class="sxs-lookup"><span data-stu-id="b4854-111">Steps</span></span>

<span data-ttu-id="b4854-112">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="b4854-112">First of all, a data source is required.</span></span> <span data-ttu-id="b4854-113">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="b4854-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="b4854-114">数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。</span><span class="sxs-lookup"><span data-stu-id="b4854-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="b4854-115">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。</span><span class="sxs-lookup"><span data-stu-id="b4854-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="b4854-116">最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="b4854-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="b4854-117">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="b4854-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="b4854-118">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="b4854-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="b4854-119">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="b4854-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="b4854-120">然后，将数据源添加到页面。</span><span class="sxs-lookup"><span data-stu-id="b4854-120">Then, add a data source to the page.</span></span> <span data-ttu-id="b4854-121">为了使用有限数量的数据，我们仅选择 AdventureWorks 数据库的供应商表中的前五个条目。</span><span class="sxs-lookup"><span data-stu-id="b4854-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="b4854-122">如果使用 Visual Studio 助手创建数据源，请记住，当前版本中的 bug 不会将表名称（`Vendor`）作为前缀，而 `Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="b4854-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="b4854-123">下面的标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="b4854-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="b4854-124">接下来，添加一个面板作为模式弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="b4854-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="b4854-125">现在，`HoverMenuExtender` 进入播放。</span><span class="sxs-lookup"><span data-stu-id="b4854-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="b4854-126">为了使数据源中的每个元素均获取其弹出式窗口，必须将扩展器置于 repeater `<ItemTemplate>` 部分中。</span><span class="sxs-lookup"><span data-stu-id="b4854-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="b4854-127">此处为标记：</span><span class="sxs-lookup"><span data-stu-id="b4854-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="b4854-128">现在，数据源中的每个项都显示一个弹出窗口（`PopupPosition` 属性），延迟为50毫秒（`PopDelay` 属性）。</span><span class="sxs-lookup"><span data-stu-id="b4854-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="b4854-129">[![在 repeater 中的每一项旁边显示悬停菜单](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b4854-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="b4854-130">悬停菜单显示在 repeater 中每个项的旁边（[单击以查看完全大小的图像](using-hovermenu-with-a-repeater-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="b4854-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b4854-131">上一部分</span><span class="sxs-lookup"><span data-stu-id="b4854-131">Previous</span></span>](using-hovermenu-with-a-repeater-control-cs.md)
