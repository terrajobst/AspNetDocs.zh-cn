---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
title: 母版/详细信息使用可选择的主控 GridView 和详细信息 DetailView （VB） |Microsoft Docs
author: rick-anderson
description: 本教程将有一个 GridView，其中的行包含每个产品的名称和价格以及 "选择" 按钮。 单击 "particu ..." 的 "选择" 按钮
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1d1a7c93-971d-4690-9c5e-dac0e5014a09
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
msc.type: authoredcontent
ms.openlocfilehash: a953c00acc4c37fd563321477b6b21689d6e686c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576445"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-vb"></a>使用带有详细信息 DetailView 的可选母版 GridView 来实现母版/详细信息查看 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_10_VB.exe)或[下载 PDF](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/datatutorial10vb1.pdf)

> 本教程将有一个 GridView，其中的行包含每个产品的名称和价格以及 "选择" 按钮。 单击特定产品的 "选择" 按钮将导致其完整详细信息显示在同一页上的 "DetailsView" 控件中。

## <a name="introduction"></a>简介

在[上一教程](master-detail-filtering-across-two-pages-vb.md)中，我们介绍了如何使用两个网页创建主/从报表： "主" 网页，其中显示了供应商列表;列出了所选供应商提供的产品的 "详细信息" 网页。 可以将这两个页面报表格式压缩为一个页面。 本教程将有一个 GridView，其中的行包含每个产品的名称和价格以及 "选择" 按钮。 单击特定产品的 "选择" 按钮将导致其完整详细信息显示在同一页上的 "DetailsView" 控件中。

[![单击 "选择" 按钮将显示产品的详细信息](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image1.png)

**图 1**：单击 "选择" 按钮将显示产品的详细信息（[单击以查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image3.png)）

## <a name="step-1-creating-a-selectable-gridview"></a>步骤1：创建可选择的 GridView

请注意，在 "双页主/详细信息" 报表中，每个主记录都包含一个超链接，单击该超链接时，会将用户发送到详细信息页，同时传递所单击的行的 `SupplierID` 值。 此类超链接已使用 HyperLinkField 添加到每个 GridView 行。 对于单页主/详细信息报表，每个 GridView 行都需要一个按钮，单击此按钮将显示详细信息。 GridView 控件可配置为为导致回发的每一行包含一个选择按钮，并将该行标记为 GridView 的[SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)。

首先，将 GridView 控件添加到 `Filtering` 文件夹中的 "`DetailsBySelecting.aspx`" 页，并将其 `ID` 属性设置为 "`ProductsGrid`"。 接下来，添加一个名为 `AllProductsDataSource` 的新 ObjectDataSource，用于调用 `ProductsBLL` 类的 `GetProducts()` 方法。

[![创建一个名为 AllProductsDataSource 的 ObjectDataSource](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image4.png)

**图 2**：创建名为 `AllProductsDataSource` 的 ObjectDataSource （[单击以查看完全大小的映像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image6.png)）

[![使用 ProductsBLL 类](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image7.png)

**图 3**：使用 `ProductsBLL` 类（[单击以查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image9.png)）

[![配置 ObjectDataSource 以调用 GetProducts （）方法](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image10.png)

**图 4**：配置 ObjectDataSource 以调用 `GetProducts()` 方法（[单击以查看完全大小的映像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image12.png)）

编辑 GridView 的字段，删除除 `ProductName` 和 `UnitPrice` BoundFields 以外的所有字段。 此外，还可以根据需要随意自定义这些 BoundFields，例如将 `UnitPrice` BoundField 的格式设置为货币，并更改 BoundFields 的 `HeaderText` 属性。 可以通过以下方式以图形方式完成这些步骤：从 GridView 的智能标记中单击 "编辑列" 链接，或手动配置声明性语法。

[![删除 "ProductName" 和 "单价" BoundFields](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image13.png)

**图 5**：删除除 `ProductName` 和 `UnitPrice` BoundFields 以外的所有内容（[单击查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image15.png)）

GridView 的最终标记为：

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample1.aspx)]

接下来，我们需要将 GridView 标记为可选，这会向每一行添加一个 "选择" 按钮。 若要实现此目的，只需选中 GridView 智能标记中的 "启用选择" 复选框。

[![使 GridView 的行可选择](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image16.png)

**图 6**：使 GridView 的行可选择（[单击查看完全尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image18.png)）

选中 "启用选择" 选项会将 CommandField 添加到 `ProductsGrid` GridView，并将其 `ShowSelectButton` 属性设置为 True。 如图6所示，这会为 GridView 的每个行生成一个选择按钮。 默认情况下，Select 按钮呈现为 LinkButtons，但你可以通过 CommandField 的 `ButtonType` 属性来改用按钮或 ImageButtons。

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample2.aspx)]

当单击 GridView 行的 "选择" 按钮时，将更新可以属性，并更新 GridView 的 `SelectedRow` 属性。 除了 `SelectedRow` 属性，GridView 还提供了[SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx)、 [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)和[SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx)属性。 `SelectedIndex` 属性返回选定行的索引，而 `SelectedValue` 和 `SelectedDataKey` 属性返回基于 GridView 的[DataKeyNames 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)的值。

`DataKeyNames` 属性用来将一个或多个数据字段值与每一行相关联，并且通常用于对每个 GridView 行的基础数据中的信息进行唯一标识。 `SelectedValue` 属性返回选定行的第一个 `DataKeyNames` 数据字段的值，`SelectedDataKey` 属性返回选定行的 `DataKey` 对象，该对象包含该行的指定数据键字段的所有值。

通过设计器将数据源绑定到 GridView、DetailsView 或 FormView 时，`DataKeyNames` 属性会自动设置为唯一标识数据字段。 虽然在前面的教程中已自动设置了此属性，但没有指定 `DataKeyNames` 属性，示例仍可正常工作。 但是，对于本教程中的可选择 GridView 以及将来要检查插入、更新和删除的教程，必须正确设置 `DataKeyNames` 属性。 请花点时间来确保 GridView 的 `DataKeyNames` 属性设置为 `ProductID`。

让我们通过浏览器查看进度。 请注意，GridView 会列出所有产品的名称和价格以及 Select LinkButton。 单击 "选择" 按钮会导致回发。 在步骤2中，我们将了解如何通过显示所选产品的详细信息，对该回发做出一次 DetailsView 响应。

[![每个产品行都包含 Select LinkButton](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image19.png)

**图 7**：每个产品行都包含一个 Select LinkButton （[单击查看全尺寸图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image21.png)）

## <a name="highlighting-the-selected-row"></a>突出显示所选行

`ProductsGrid` GridView 具有一个 `SelectedRowStyle` 属性，该属性可用于为所选行口述视觉样式。 如果使用得当，这可以更清晰地显示 GridView 当前选定的行，从而改善用户的体验。 对于本教程，让我们用黄色背景突出显示所选行。

与我们以前的教程一样，让我们努力将美观相关设置定义为 CSS 类。 因此，请在 `Styles.css` 中创建一个名为 `SelectedRowStyle`的新 CSS 类。

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample3.css)]

若要将此 CSS 类应用于本教程系列中*所有*GridViews 的 `SelectedRowStyle` 属性，请编辑 `DataWebControls` 主题中的 `GridView.skin` 外观，使其包括 `SelectedRowStyle` 设置，如下所示：

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample4.aspx)]

通过此添加，所选 GridView 行将现在以黄色背景色突出显示。

[![使用 GridView 的 SelectedRowStyle 属性自定义选定行的外观](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image22.png)

**图 8**：使用 GridView 的 `SelectedRowStyle` 属性自定义选定行的外观（[单击以查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image24.png)）

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>步骤2：在 DetailsView 中显示所选产品的详细信息

`ProductsGrid` GridView 完成后，剩下的就是添加一个 DetailsView，其中显示有关所选特定产品的信息。 将 DetailsView 控件添加到 GridView 之上，并创建名为 `ProductDetailsDataSource`的新 ObjectDataSource。 由于我们希望此 DetailsView 显示有关选定产品的特定信息，因此请将 `ProductDetailsDataSource` 配置为使用 `ProductsBLL` 类的 `GetProductByProductID(productID)` 方法。

[![调用 ProductsBLL 类的 GetProductByProductID （productID）方法](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image25.png)

**图 9**：调用 `ProductsBLL` 类的 `GetProductByProductID(productID)` 方法（[单击以查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image27.png)）

使 *`productID`* 参数的值从 GridView 控件的 `SelectedValue` 属性中获取。 如前文所述，GridView 的 `SelectedValue` 属性返回选定行的第一个数据键值。 因此，GridView 的 `DataKeyNames` 属性设置为 `ProductID`是必需的，以便 `SelectedValue`返回所选行的 `ProductID` 值。

[![将 productID 参数设置为 GridView 的 SelectedValue 属性](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image28.png)

**图 10**：将 *`productID`* 参数设置为 GridView 的 `SelectedValue` 属性（[单击查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image30.png)）

正确配置 `productDetailsDataSource` ObjectDataSource 并将其绑定到 DetailsView 后，本教程已完成！ 第一次访问该页面时，未选择任何行，因此 GridView 的 `SelectedValue` 属性返回 `Nothing`。 由于没有 `NULL` `ProductID` 值的产品，`GetProductByProductID(productID)` 方法不会返回任何记录，这意味着不会显示 DetailsView （参见图11）。 单击 GridView 行的 "选择" 按钮时，将刷新回发可以和 DetailsView。 这一次，GridView 的 `SelectedValue` 属性返回所选行的 `ProductID`，`GetProductByProductID(productID)` 方法返回一个包含有关特定产品的信息的 `ProductsDataTable`，并且 DetailsView 显示这些详细信息（见图12）。

[首次访问时 ![，只显示 GridView](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image31.png)

**图 11**：首次访问时，只显示 GridView （[单击查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image33.png)）

[选择行时 ![，将显示产品的详细信息](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image34.png)

**图 12**：选择行后，将显示产品的详细信息（[单击以查看完全大小的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image36.png)）

## <a name="summary"></a>总结

在本教程和前面三个教程中，我们已介绍了几种显示大纲/详细信息报表的方法。 在本教程中，我们介绍了如何使用可选的 GridView 来容纳主记录，并使用 DetailsView 在同一页上显示所选主记录的详细信息。 在前面的教程中，我们介绍了如何使用 DropDownLists 显示主/详细信息报表，并在一个网页上显示主记录，并在另一个网页上显示详细记录。

本教程将结束我们对主/详细信息报表的检查。 从下一教程开始，我们将开始探索如何通过 GridView、DetailsView 和 FormView 探索自定义格式。 我们将了解如何基于绑定到这些控件的数据自定义这些控件的外观，如何汇总 GridView 脚注中的数据，以及如何使用模板获得更好的布局控制度。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一部分](master-detail-filtering-across-two-pages-vb.md)
