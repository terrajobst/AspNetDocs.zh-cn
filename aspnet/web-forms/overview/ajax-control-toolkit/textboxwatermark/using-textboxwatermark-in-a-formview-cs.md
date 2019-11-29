---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
title: 在 FormView （C#）中使用 TextBoxWatermark |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6ee90bf-32a5-4987-a384-15cc7dd30c8a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
msc.type: authoredcontent
ms.openlocfilehash: 13ac0da5ca53756aa7c660cdc47c96f0c865b006
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611318"
---
# <a name="using-textboxwatermark-in-a-formview-c"></a><span data-ttu-id="b7ecf-104">在 FormView 中使用 TextBoxWatermark (C#)</span><span class="sxs-lookup"><span data-stu-id="b7ecf-104">Using TextBoxWatermark in a FormView (C#)</span></span>

<span data-ttu-id="b7ecf-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b7ecf-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b7ecf-106">[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b7ecf-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span></span>

> <span data-ttu-id="b7ecf-107">AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="b7ecf-108">当用户在框中单击时，它会被清空。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="b7ecf-109">如果用户离开该框而不输入文本，则会重新出现预填充文本。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="b7ecf-110">在 FormView 控件中也可以这样做。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-110">This is also possible within a FormView control.</span></span>

## <a name="overview"></a><span data-ttu-id="b7ecf-111">概述</span><span class="sxs-lookup"><span data-stu-id="b7ecf-111">Overview</span></span>

<span data-ttu-id="b7ecf-112">AJAX 控件工具包中的 `TextBoxWatermark` 控件扩展了文本框，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="b7ecf-113">当用户在框中单击时，它会被清空。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="b7ecf-114">如果用户离开该框而不输入文本，则会重新出现预填充文本。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="b7ecf-115">这也可能出现在 `FormView` 控件中。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="b7ecf-116">步骤</span><span class="sxs-lookup"><span data-stu-id="b7ecf-116">Steps</span></span>

<span data-ttu-id="b7ecf-117">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-117">First of all, a data source is required.</span></span> <span data-ttu-id="b7ecf-118">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="b7ecf-119">数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="b7ecf-120">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="b7ecf-121">最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="b7ecf-122">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="b7ecf-123">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="b7ecf-124">若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：</span><span class="sxs-lookup"><span data-stu-id="b7ecf-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample1.aspx)]

<span data-ttu-id="b7ecf-125">然后，将数据源添加到支持 `DELETE`、`INSERT` 和 `UPDATE` SQL 语句的页面。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="b7ecf-126">如果使用 Visual Studio 助手创建数据源，请记住，当前版本中的 bug 不会将表名称（`Vendor`）作为前缀，而 `Purchasing`。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="b7ecf-127">下面的标记显示了正确的语法：</span><span class="sxs-lookup"><span data-stu-id="b7ecf-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample2.aspx)]

<span data-ttu-id="b7ecf-128">请记住数据源的名称（`ID`），因为它将在 `FormView` 控件的 `DataSourceID` 属性中使用。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="b7ecf-129">`FormView` 的 `<InsertItemTemplate>` 部分包含一个文本框，该文本框由 `TextBoxWatermarkExtender` 控件扩展。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="b7ecf-130">确保扩展程序位于模板内，而不是位于该模板之外。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample3.aspx)]

<span data-ttu-id="b7ecf-131">现在，当用户更改为 `FormView` 控件的插入模式时，新供应商的文本字段将预先填充，因为 `TextBoxWatermarkExtender` 控件。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="b7ecf-132">在文本框内单击，使填充文本消失。</span><span class="sxs-lookup"><span data-stu-id="b7ecf-132">A click inside the textbox lets the filler text disappear.</span></span>

<span data-ttu-id="b7ecf-133">[![字段中的水印来自扩展器](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b7ecf-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span></span>

<span data-ttu-id="b7ecf-134">该字段中的水印来自扩展器（[单击查看完全大小的图像](using-textboxwatermark-in-a-formview-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="b7ecf-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b7ecf-135">下一页</span><span class="sxs-lookup"><span data-stu-id="b7ecf-135">Next</span></span>](using-textboxwatermark-with-validation-controls-cs.md)
