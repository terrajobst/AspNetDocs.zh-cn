---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: 在数据库中使用 CascadingDropDown （C#） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 的更改会在 anoth 中加载关联值。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: bcf453170d17807b4e3b2d2a8b545cba43139f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483746"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="423af-103">通过数据库使用 CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="423af-103">Using CascadingDropDown with a Database (C#)</span></span>

<span data-ttu-id="423af-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="423af-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="423af-105">[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="423af-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="423af-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="423af-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="423af-107">为了使其正常工作，必须创建一个特殊的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="423af-107">In order for this to work, a special web service must be created.</span></span>

## <a name="overview"></a><span data-ttu-id="423af-108">概述</span><span class="sxs-lookup"><span data-stu-id="423af-108">Overview</span></span>

<span data-ttu-id="423af-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。</span><span class="sxs-lookup"><span data-stu-id="423af-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="423af-110">（例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）为了使其正常工作，必须创建一个特殊的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="423af-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="423af-111">步骤</span><span class="sxs-lookup"><span data-stu-id="423af-111">Steps</span></span>

<span data-ttu-id="423af-112">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="423af-112">First of all, a data source is required.</span></span> <span data-ttu-id="423af-113">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="423af-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="423af-114">数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。</span><span class="sxs-lookup"><span data-stu-id="423af-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="423af-115">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。</span><span class="sxs-lookup"><span data-stu-id="423af-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="423af-116">最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="423af-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="423af-117">对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="423af-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="423af-118">如果你的设置不同，则必须修改数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="423af-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="423af-119">若要激活 ASP.NET AJAX 和控件工具包的功能，`ScriptManager` 控件必须置于页面上的任何位置（但在 &lt;`form`&gt; 元素中）：</span><span class="sxs-lookup"><span data-stu-id="423af-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="423af-120">在下一步中，需要两个 DropDownList 控件。</span><span class="sxs-lookup"><span data-stu-id="423af-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="423af-121">在此示例中，我们使用 AdventureWorks 提供商和联系人信息，因此我们为可用供应商创建一个列表，并为可用联系人创建一个列表：</span><span class="sxs-lookup"><span data-stu-id="423af-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="423af-122">然后，必须将两个 CascadingDropDown 扩展程序添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="423af-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="423af-123">一个表将填充第一个（供应商）列表，另一个将填充第二个（联系人）列表。</span><span class="sxs-lookup"><span data-stu-id="423af-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="423af-124">必须设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="423af-124">The following attributes must be set:</span></span>

- <span data-ttu-id="423af-125">`ServicePath`：提供列表项的 web 服务的 URL</span><span class="sxs-lookup"><span data-stu-id="423af-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="423af-126">`ServiceMethod`：传递列表项的 Web 方法</span><span class="sxs-lookup"><span data-stu-id="423af-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="423af-127">`TargetControlID`：下拉列表的 ID</span><span class="sxs-lookup"><span data-stu-id="423af-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="423af-128">`Category`：调用时提交到 web 方法的类别信息</span><span class="sxs-lookup"><span data-stu-id="423af-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="423af-129">`PromptText`：从服务器异步加载列表数据时显示的文本</span><span class="sxs-lookup"><span data-stu-id="423af-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="423af-130">`ParentControlID`：（可选）用于触发当前列表加载的父下拉列表</span><span class="sxs-lookup"><span data-stu-id="423af-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="423af-131">根据所使用的编程语言，有问题的 web 服务的名称会发生更改，但所有其他属性值都是相同的。</span><span class="sxs-lookup"><span data-stu-id="423af-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="423af-132">下面是第一个下拉列表的 CascadingDropDown 元素：</span><span class="sxs-lookup"><span data-stu-id="423af-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="423af-133">第二个列表的控件扩展器需要设置 `ParentControlID` 特性，以便在 "供应商" 列表中选择一个条目，以便在 "联系人" 列表中加载关联的元素。</span><span class="sxs-lookup"><span data-stu-id="423af-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="423af-134">然后，将在 web 服务中完成实际工作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="423af-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="423af-135">请注意，将使用 `[ScriptService]` 属性，否则，ASP.NET AJAX 无法创建 JavaScript 代理以从客户端脚本代码访问 web 方法。</span><span class="sxs-lookup"><span data-stu-id="423af-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="423af-136">CascadingDropDown 调用的 web 方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="423af-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="423af-137">因此，返回值必须是由控件工具包定义 `CascadingDropDownNameValue` 类型的数组。</span><span class="sxs-lookup"><span data-stu-id="423af-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="423af-138">`GetVendors()` 方法非常易于实现：代码连接到 AdventureWorks 数据库，并查询前25个供应商。</span><span class="sxs-lookup"><span data-stu-id="423af-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="423af-139">`CascadingDropDownNameValue` 构造函数中的第一个参数是列表项的标题，第二个参数的值（HTML 的 &lt;中的值属性 `option`&gt; 元素）。</span><span class="sxs-lookup"><span data-stu-id="423af-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="423af-140">代码如下：</span><span class="sxs-lookup"><span data-stu-id="423af-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="423af-141">获取供应商关联的联系人（方法名称： `GetContactsForVendor()`）有点棘手。</span><span class="sxs-lookup"><span data-stu-id="423af-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="423af-142">首先，必须确定第一个下拉列表中选择的供应商。</span><span class="sxs-lookup"><span data-stu-id="423af-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="423af-143">控件工具包为该任务定义 helper 方法： `ParseKnownCategoryValuesString()` 方法返回包含下拉列表数据的 `StringDictionary` 元素：</span><span class="sxs-lookup"><span data-stu-id="423af-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="423af-144">出于安全原因，必须先验证此数据。</span><span class="sxs-lookup"><span data-stu-id="423af-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="423af-145">因此，如果有一个供应商条目（因为第一个 CascadingDropDown 元素的 `Category` 属性设置为 `"Vendor"`），则可以检索所选供应商的 ID：</span><span class="sxs-lookup"><span data-stu-id="423af-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="423af-146">此方法的其余部分是相当直接的，然后是。</span><span class="sxs-lookup"><span data-stu-id="423af-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="423af-147">使用供应商的 ID 作为 SQL 查询的参数，该查询检索该供应商的所有关联联系人。</span><span class="sxs-lookup"><span data-stu-id="423af-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="423af-148">同样，该方法返回 `CascadingDropDownNameValue`类型的数组。</span><span class="sxs-lookup"><span data-stu-id="423af-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="423af-149">加载 ASP.NET 页面，一小段时间后，在供应商列表中填充25个条目。</span><span class="sxs-lookup"><span data-stu-id="423af-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="423af-150">选取一项，并注意第二个下拉列表是如何填充数据的。</span><span class="sxs-lookup"><span data-stu-id="423af-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>

<span data-ttu-id="423af-151">[![自动填充第一个列表](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="423af-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="423af-152">将自动填充第一个列表（[单击以查看完全大小的图像](using-cascadingdropdown-with-a-database-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="423af-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>

<span data-ttu-id="423af-153">[![第一个列表根据第一个列表中的选择进行填充](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="423af-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="423af-154">第二个列表根据第一个列表中的选择进行填充（[单击以查看完全大小的图像](using-cascadingdropdown-with-a-database-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="423af-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="423af-155">[上一页](filling-a-list-using-cascadingdropdown-cs.md)
> [下一页](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="423af-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
