---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
title: 使用 DropDownList 进行主/详细信息筛选（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何在 DropDownList 控件中显示主记录，并了解 GridView 中选定列表项的详细信息。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ea44717e-ab2e-46cd-a692-e4a9c0de194c
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 62cd296a3f36e1779666a6b5db15b0ce2488d0e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639905"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>使用一个 DropDownList 实现母版/详细信息筛选 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)

> 在本教程中，我们将了解如何在 DropDownList 控件中显示主记录，并了解 GridView 中选定列表项的详细信息。

## <a name="introduction"></a>简介

常见的报表类型为 "*主/详细信息报表*"，其中报表从显示一组 "主" 记录开始。 然后，用户可以向下钻取到其中一个主记录，从而查看该主记录的 "详细信息"。 主/详细信息报表是直观显示一对多关系的理想选择，例如显示所有类别的报表，然后允许用户选择特定类别并显示其关联的产品。 此外，主/详细信息报表适用于显示特别 "宽" 表（包含大量列）的详细信息。 例如，主/详细信息报表的 "主" 级别可能只显示数据库中产品的产品名和单价，并向下钻取到特定产品会显示其他产品字段（类别、供应商、每个单位的数量，等等）。

可以通过多种方式来实现主/详细信息报表。 在本教程中，我们将介绍几个大纲/详细信息报表。 在本教程中，我们将了解如何在[DropDownList 控件](https://msdn.microsoft.com/library/dtx91y0z.aspx)中显示主记录，并了解 GridView 中选定列表项的详细信息。 具体而言，本教程的大纲/详细信息报表将列出类别和产品信息。

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>步骤1：在 DropDownList 中显示类别

我们的主/详细信息报表将列出 DropDownList 中的类别，其中选定列表项的产品在 GridView 的页面中向下显示。 接下来，第一个任务是在 DropDownList 中显示类别。 打开 `Filtering` 文件夹中的 "`FilterByDropDownList.aspx`" 页，将 "DropDownList" 从 "工具箱" 拖到页面的设计器上，并将其 `ID` 属性设置为 "`Categories`"。 接下来，单击 DropDownList 的智能标记中的 "选择数据源" 链接。 这将显示 "数据源配置向导"。

[![指定 DropDownList 的数据源](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)

**图 1**：指定 DropDownList 的数据源（[单击查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png)）

选择添加一个名为 `CategoriesDataSource` 的新 ObjectDataSource，用于调用 `CategoriesBLL` 类的 `GetCategories()` 方法。

[![添加名为 CategoriesDataSource 的新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)

**图 2**：添加名为 `CategoriesDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png)）

[![选择使用 CategoriesBLL 类](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)

**图 3**：选择使用 `CategoriesBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png)）

[![将 ObjectDataSource 配置为使用 GetCategories （）方法](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)

**图 4**：将 ObjectDataSource 配置为使用 `GetCategories()` 方法（[单击查看完全大小的映像](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png)）

配置 ObjectDataSource 后，我们仍然需要指定应在 DropDownList 中显示的数据源字段，以及哪一字段应与列表项的值相关联。 将 `CategoryName` 字段作为显示，并将 `CategoryID` 为每个列表项的值。

[![DropDownList 显示 "类别名称" 字段，并使用 "类别 Id" 作为值](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)

**图 5**：使 DropDownList 显示 "`CategoryName`" 字段并使用 "`CategoryID`" 作为值（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png)）

此时，我们有一个 DropDownList 控件，其中填充了 `Categories` 表中的记录（已在大约六秒钟内完成）。 图6显示了在浏览器中查看时的进度。

[![下拉列表中列出了当前类别](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)

**图 6**：下拉列表列出了当前类别（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png)）

## <a name="step-2-adding-the-products-gridview"></a>步骤2：添加产品 GridView

主/详细信息报表中的最后一步是列出与所选类别关联的产品。 若要实现此目的，请向页面添加一个 GridView，并创建名为 `productsDataSource`的新 ObjectDataSource。 让 `productsDataSource` 控件从 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法中剔除其数据。

[![选择 GetProductsByCategoryID （类别 Id）方法](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)

**图 7**：选择 `GetProductsByCategoryID(categoryID)` 方法（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png)）

选择此方法之后，ObjectDataSource 向导会提示我们输入方法的 *`categoryID`* 参数的值。 若要使用所选 `categories` DropDownList 项的值，请将参数源设置为 Control，并将 ControlID 设置为 `Categories`。

[![将 "类别 Id" 参数设置为 "类别 DropDownList" 的值。](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)

**图 8**：将 *`categoryID`* 参数设置为 `Categories` DropDownList 的值（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png)）

请花点时间查看浏览器中的进度。 首次访问页面时，将显示属于所选类别（饮料）的产品（如图9所示），但更改 DropDownList 不会更新数据。 这是因为必须发生回发以便 GridView 更新。 若要实现此目的，我们有两个选项（这两者都不需要编写任何代码）：

- **将 DropDownList 的**[AutoPostBack 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)设置**为 True。** （可以通过选中 DropDownList 的智能标记中的 Enable AutoPostBack 选项来实现此目的。）这会在用户更改 DropDownList 的选定项时触发回发。 因此，当用户从 DropDownList 中选择一个新类别时，回发将不幸，并将使用新选定类别的产品更新 GridView。 （这是我在本教程中使用的方法。）
- **将按钮 Web 控件添加到 DropDownList 旁边。** 将其 `Text` 属性设置为 Refresh 或类似的内容。 使用此方法时，用户需要选择一个新类别，然后单击 "" 按钮。 单击该按钮将导致回发并更新 GridView 以列出所选类别的产品。

图9和10说明了操作中的主/详细信息报表。

[首次访问页面时 ![，将显示饮料产品](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)

**图 9**：首次访问页面时，会显示饮料产品（[单击查看全尺寸图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png)）

[![选择新产品（生成）会自动导致回发，并更新 GridView](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)

**图 10**：选择新产品（"生成"）会自动导致回发，并更新 GridView （[单击查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png)）

## <a name="adding-a----choose-a-category----list-item"></a>添加 "--选择类别--" 列表项

第一次访问 "`FilterByDropDownList.aspx`" 页面时，默认情况下会选择类别 DropDownList 的第一个列表项（饮料），其中显示 GridView 中的饮料产品。 我们可能不想显示第一个类别的产品，而是选择一个 DropDownList 项，其中显示了类似于 "--选择一个类别--" 的内容。

若要向 DropDownList 添加新的列表项，请切换到属性窗口并单击 `Items` 属性中的省略号。 添加一个新列表项，其中包含 `Text` "--选择类别--" 和 `Value` `-1`。

[![添加--选择类别--列表项](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)

**图 11**：添加--选择类别--列表项（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png)）

或者，你可以通过将以下标记添加到 DropDownList 来添加列表项：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample1.aspx)]

此外，我们需要将 DropDownList 控件的 `AppendDataBoundItems` 设置为 True，因为当类别从 ObjectDataSource 绑定到 DropDownList 时，如果 `AppendDataBoundItems` 不为 True，则会覆盖所有手动添加的列表项。

![将 AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-vb/_static/image34.png)

**图 12**：将 `AppendDataBoundItems` 属性设置为 True

完成这些更改后，在首次访问该页面时，将选择 "--选择类别--" 选项，并且不会显示任何产品。

[初始页面加载上的 ![未显示任何产品](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)

**图 13**：初始页面加载时未显示任何产品（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png)）

由于选择了 "--选择类别--" 列表项，因此不会显示任何产品，因为其值是 `-1` 的，并且数据库中没有 `-1``CategoryID` 的产品。 如果这是你想要的行为，此时已经完成了！ 但是，如果您想要在 "--选择类别--" 列表项处于选中状态时显示*所有*类别，则返回到 `ProductsBLL` 类并自定义 `GetProductsByCategoryID(categoryID)` 方法，以便在 *`categoryID`* 参数中传递的值小于零时调用 `GetProducts()` 方法：

[!code-vb[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample2.vb)]

此处使用的方法类似于我们用于在[声明性参数](../basic-reporting/declarative-parameters-cs.md)教程中显示所有供应商的方法，但在本示例中，我们使用值 `-1` 来指示应检索所有记录，而不是 `Nothing`。 这是因为 `GetProductsByCategoryID(categoryID)` 方法的 *`categoryID`* 参数需要使用传入的整数值，而在声明性参数教程中，我们传入了字符串输入参数。

图14显示了选择 "--选择类别--" 选项时的 `FilterByDropDownList.aspx` 屏幕截图。 此时，默认情况下会显示所有产品，用户可以通过选择特定类别来缩小显示范围。

[默认情况下，![所有产品都已列出](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)

**图 14**：默认情况下，所有产品均已列出（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png)）

## <a name="summary"></a>总结

显示分层相关的数据时，通常可以使用主/详细信息报表来显示数据，用户可以从层次结构顶部开始浏览数据，并向下钻取详细信息。 在本教程中，我们将介绍如何生成一个简单的大纲/详细信息报告，其中显示了所选类别的产品。 为此，可以使用 DropDownList 作为类别列表，并将 GridView 用于属于所选类别的产品。

在[下一教程](master-detail-filtering-with-two-dropdownlists-vb.md)中，我们将使用两个 DropDownLists 进一步 DropDownList 接口。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
> [下一页](master-detail-filtering-with-two-dropdownlists-vb.md)
