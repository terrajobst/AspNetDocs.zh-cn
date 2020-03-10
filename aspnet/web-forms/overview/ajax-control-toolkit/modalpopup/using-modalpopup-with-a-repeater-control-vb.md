---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
title: 将 ModalPopup 用于 Repeater 控件（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。 还可以使用此 contr 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0c8e74f1-b3ba-4ca9-a1c5-f5c4831a359a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 0966770f0218ca91ba7d25e7bf703bf7b005738e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496838"
---
# <a name="using-modalpopup-with-a-repeater-control-vb"></a><span data-ttu-id="349b8-104">通过 Repeater 控件使用 ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="349b8-104">Using ModalPopup with a Repeater Control (VB)</span></span>

<span data-ttu-id="349b8-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="349b8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="349b8-106">[下载代码](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="349b8-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)</span></span>

> <span data-ttu-id="349b8-107">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="349b8-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="349b8-108">还可以在 repeater 中使用此控件。</span><span class="sxs-lookup"><span data-stu-id="349b8-108">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="349b8-109">概述</span><span class="sxs-lookup"><span data-stu-id="349b8-109">Overview</span></span>

<span data-ttu-id="349b8-110">AJAX 控件工具包中的 ModalPopup 控件提供了使用客户端方法创建模式弹出窗口的简单方法。</span><span class="sxs-lookup"><span data-stu-id="349b8-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="349b8-111">还可以在 repeater 中使用此控件。</span><span class="sxs-lookup"><span data-stu-id="349b8-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="349b8-112">步骤</span><span class="sxs-lookup"><span data-stu-id="349b8-112">Steps</span></span>

<span data-ttu-id="349b8-113">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="349b8-113">First of all, a data source is required.</span></span> <span data-ttu-id="349b8-114">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="349b8-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="349b8-115">数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。</span><span class="sxs-lookup"><span data-stu-id="349b8-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="349b8-116">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。</span><span class="sxs-lookup"><span data-stu-id="349b8-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="349b8-117">最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="349b8-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="349b8-118">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="349b8-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="349b8-119">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="349b8-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="349b8-120">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="349b8-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="349b8-121">然后，将数据源添加到页面。</span><span class="sxs-lookup"><span data-stu-id="349b8-121">Then, add a data source to the page.</span></span> <span data-ttu-id="349b8-122">为了使用有限数量的数据，我们仅选择 AdventureWorks 数据库的供应商表中的前五个条目。</span><span class="sxs-lookup"><span data-stu-id="349b8-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="349b8-123">如果使用 Visual Studio 助手创建数据源，请记住，当前版本中的 bug 不会将表名称（`Vendor`）作为前缀，而 `Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="349b8-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="349b8-124">下面的标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="349b8-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="349b8-125">接下来，添加一个用于模式弹出窗口的面板。</span><span class="sxs-lookup"><span data-stu-id="349b8-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="349b8-126">它包含一个 `Button` 控件来再次关闭弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="349b8-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="349b8-127">为了使 popup 在中继器内正常工作，必须将 `ModalPopupExtender` 控件置于 repeater 的 `<ItemTemplate>` 部分。</span><span class="sxs-lookup"><span data-stu-id="349b8-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="349b8-128">因此，该面板位于中继器之外，但扩展器在内部。</span><span class="sxs-lookup"><span data-stu-id="349b8-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="349b8-129">下面是中继器的标记：</span><span class="sxs-lookup"><span data-stu-id="349b8-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="349b8-130">然后，将显示数据源中的每个项，并在其旁边显示一个按钮，用于触发模式弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="349b8-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>

<span data-ttu-id="349b8-131">[![可以为每个数据源输入触发模式弹出窗口](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="349b8-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="349b8-132">可以为每个数据源输入触发模式弹出窗口（[单击以查看完全大小的映像](using-modalpopup-with-a-repeater-control-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="349b8-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="349b8-133">[上一页](launching-a-modal-popup-window-from-server-code-vb.md)
> [下一页](handling-postbacks-from-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="349b8-133">[Previous](launching-a-modal-popup-window-from-server-code-vb.md)
[Next](handling-postbacks-from-a-modalpopup-vb.md)</span></span>
