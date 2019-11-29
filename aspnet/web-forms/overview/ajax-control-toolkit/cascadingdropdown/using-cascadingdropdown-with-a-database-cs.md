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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599785"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a>通过数据库使用 CascadingDropDown (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)

> AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 为了使其正常工作，必须创建一个特殊的 web 服务。

## <a name="overview"></a>概述

AJAX 控件工具包中的 CascadingDropDown 控件扩展了 DropDownList 控件，以便其中一个 DropDownList 中的更改加载另一个 DropDownList 中的关联值。 （例如，一个列表提供美国省/市/自治区列表，然后使用该州的主要城市填充下一个列表。）为了使其正常工作，必须创建一个特殊的 web 服务。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。 最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。

对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。 如果你的设置不同，则必须修改数据库的连接信息。

若要激活 ASP.NET AJAX 和控件工具包的功能，`ScriptManager` 控件必须置于页面上的任何位置（但在 &lt;`form`&gt; 元素中）：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

在下一步中，需要两个 DropDownList 控件。 在此示例中，我们使用 AdventureWorks 提供商和联系人信息，因此我们为可用供应商创建一个列表，并为可用联系人创建一个列表：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

然后，必须将两个 CascadingDropDown 扩展程序添加到页面中。 一个表将填充第一个（供应商）列表，另一个将填充第二个（联系人）列表。 必须设置以下属性：

- `ServicePath`：提供列表项的 web 服务的 URL
- `ServiceMethod`：传递列表项的 Web 方法
- `TargetControlID`：下拉列表的 ID
- `Category`：调用时提交到 web 方法的类别信息
- `PromptText`：从服务器异步加载列表数据时显示的文本
- `ParentControlID`：（可选）用于触发当前列表加载的父下拉列表

根据所使用的编程语言，有问题的 web 服务的名称会发生更改，但所有其他属性值都是相同的。 下面是第一个下拉列表的 CascadingDropDown 元素：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

第二个列表的控件扩展器需要设置 `ParentControlID` 特性，以便在 "供应商" 列表中选择一个条目，以便在 "联系人" 列表中加载关联的元素。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

然后，将在 web 服务中完成实际工作，如下所示。 请注意，将使用 `[ScriptService]` 属性，否则，ASP.NET AJAX 无法创建 JavaScript 代理以从客户端脚本代码访问 web 方法。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

CascadingDropDown 调用的 web 方法的签名如下所示：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

因此，返回值必须是由控件工具包定义 `CascadingDropDownNameValue` 类型的数组。 `GetVendors()` 方法非常易于实现：代码连接到 AdventureWorks 数据库，并查询前25个供应商。 `CascadingDropDownNameValue` 构造函数中的第一个参数是列表项的标题，第二个参数的值（HTML 的 &lt;中的值属性 `option`&gt; 元素）。 代码如下：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

获取供应商关联的联系人（方法名称： `GetContactsForVendor()`）有点棘手。 首先，必须确定第一个下拉列表中选择的供应商。 控件工具包为该任务定义 helper 方法： `ParseKnownCategoryValuesString()` 方法返回包含下拉列表数据的 `StringDictionary` 元素：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

出于安全原因，必须先验证此数据。 因此，如果有一个供应商条目（因为第一个 CascadingDropDown 元素的 `Category` 属性设置为 `"Vendor"`），则可以检索所选供应商的 ID：

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

此方法的其余部分是相当直接的，然后是。 使用供应商的 ID 作为 SQL 查询的参数，该查询检索该供应商的所有关联联系人。 同样，该方法返回 `CascadingDropDownNameValue`类型的数组。

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

加载 ASP.NET 页面，一小段时间后，在供应商列表中填充25个条目。 选取一项，并注意第二个下拉列表是如何填充数据的。

[![自动填充第一个列表](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)

将自动填充第一个列表（[单击以查看完全大小的图像](using-cascadingdropdown-with-a-database-cs/_static/image3.png)）

[![第一个列表根据第一个列表中的选择进行填充](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)

第二个列表根据第一个列表中的选择进行填充（[单击以查看完全大小的图像](using-cascadingdropdown-with-a-database-cs/_static/image6.png)）

> [!div class="step-by-step"]
> [上一页](filling-a-list-using-cascadingdropdown-cs.md)
> [下一页](presetting-list-entries-with-cascadingdropdown-cs.md)
