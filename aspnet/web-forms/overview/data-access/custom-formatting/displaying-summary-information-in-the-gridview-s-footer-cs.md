---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: 在 GridView 的页脚中显示摘要信息（C#） |Microsoft Docs
author: rick-anderson
description: 摘要信息通常显示在报表底部的摘要行中。 GridView 控件可以将一个页脚行包含到可在其中使用的单元格 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: b258a2bdeaea8da4e9c5c5d8043b167d94e1e817
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617001"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-c"></a>在 GridView 的页脚中显示摘要信息 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe)或[下载 PDF](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> 摘要信息通常显示在报表底部的摘要行中。 GridView 控件可以在其单元格中包含一个页脚行，以便以编程方式注入聚合数据。 在本教程中，我们将了解如何在此页脚行中显示聚合数据。

## <a name="introduction"></a>简介

除了查看每种产品的价格、存货量、按订单和重新排序级别，用户还可能会对聚合信息（如平均价格、库存单位总数等）感兴趣。 此类摘要信息通常显示在报表底部的摘要行中。 GridView 控件可以在其单元格中包含一个页脚行，以便以编程方式注入聚合数据。

此任务为我们带来了三个挑战：

1. 将 GridView 配置为显示其页脚行
2. 确定摘要数据;也就是说，如何计算库存单位的平均价格或总数？
3. 将摘要数据注入页脚行的相应单元格

在本教程中，我们将了解如何解决这些难题。 具体而言，我们将创建一个页面，其中列出了显示在 GridView 中的选定类别产品的下拉列表中的类别。 GridView 将包含一个页脚行，其中显示了该类别中产品的平均价格和总单位数。

[![摘要信息显示在 GridView 的脚注行中](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**图 1**：摘要信息显示在 GridView 的脚注行中（[单击以查看完全大小的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png)）

本教程中的 "产品" 母版/详细信息接口的类别基于前面的[主/详细信息筛选](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)中介绍的概念，以及 DropDownList 教程。 如果尚未学习前面的教程，请先执行此操作，再继续使用此教程。

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>步骤1：添加类别 DropDownList 和产品 GridView

在将摘要信息添加到 GridView 的脚注之前，首先只需生成主/详细信息报表。 完成此第一步后，我们将介绍如何包含摘要数据。

首先打开 `CustomFormatting` 文件夹中的 "`SummaryDataInFooter.aspx`" 页。 添加 DropDownList 控件并将其 `ID` 设置为 `Categories`。 接下来，单击 DropDownList 的智能标记中的 "选择数据源" 链接，并选择添加一个名为 `CategoriesDataSource` 的新 ObjectDataSource 来调用 `CategoriesBLL` 类的 `GetCategories()` 方法。

[![添加名为 CategoriesDataSource 的新 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**图 2**：添加名为 `CategoriesDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png)）

[![让 ObjectDataSource 调用 CategoriesBLL 类的 GetCategories （）方法](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**图 3**：使 ObjectDataSource 调用 `CategoriesBLL` 类的 `GetCategories()` 方法（[单击查看完全大小的映像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png)）

配置 ObjectDataSource 后，向导会将我们返回到 DropDownList 的数据源配置向导，需要在此向导中指定应显示的数据字段值，哪一个应对应于 DropDownList 的 `ListItem` 的值。 显示 "`CategoryName`" 字段，并使用 "`CategoryID`" 作为值。

[![使用 "类别名称" 和 "类别名称" 字段分别作为 ListItems 的文本和值](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**图 4**：分别使用 "`CategoryName`" 和 "`CategoryID`" 字段作为 `ListItem` 的 `Text` 和 `Value` （[单击以查看完全大小的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png)）

此时，我们有一个 DropDownList （`Categories`），其中列出了系统中的类别。 现在，我们需要添加一个 GridView 来列出属于所选类别的产品。 不过，在此之前，请花点时间选中 DropDownList 的智能标记中的 "启用 AutoPostBack" 复选框。 如*使用 DropDownList 教程的主/详细信息筛选*中所述，通过将 DropDownList 的 `AutoPostBack` 属性设置为 `true` 每次更改 DropDownList 值时将回发页面。 这会导致 GridView 刷新，并显示新选定类别的产品。 如果 `AutoPostBack` 属性设置为 `false` （默认值），则更改类别不会导致回发，因此不会更新列出的产品。

[![选中 DropDownList 的智能标记中的 "启用 AutoPostBack" 复选框](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

**图 5**：选中 DropDownList 的智能标记中的 "启用 AutoPostBack" 复选框（[单击查看完全尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png)）

将 GridView 控件添加到页面，以便显示所选类别的产品。 将 GridView 的 `ID` 设置为 `ProductsInCategory` 并将其绑定到名为 `ProductsInCategoryDataSource`的新 ObjectDataSource。

[![添加名为 ProductsInCategoryDataSource 的新 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**图 6**：添加名为 `ProductsInCategoryDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png)）

配置 ObjectDataSource，使其调用 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法。

[![让 ObjectDataSource 调用 GetProductsByCategoryID （类别 Id）方法](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**图 7**：使 ObjectDataSource 调用 `GetProductsByCategoryID(categoryID)` 方法（[单击查看完全大小的映像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png)）

由于 `GetProductsByCategoryID(categoryID)` 方法采用输入参数，因此在向导的最后一步中，我们可以指定参数值的源。 若要显示所选类别中的产品，请从 `Categories` DropDownList 中获取参数。

[![获取选定类别中的类别 Id 参数值 DropDownList](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**图 8**：从所选类别 DropDownList 获取 *`categoryID`* 参数值（[单击以查看完全大小的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png)）

完成向导后，GridView 对于每个产品属性都有一个 BoundField。 让我们清理这些 BoundFields，以便仅显示 `ProductName`、`UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` BoundFields。 可随意向其余 BoundFields 添加任何字段级设置（例如，将 `UnitPrice` 的格式设置为货币）。 进行这些更改后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

此时，我们有一个完全正常运行的主/详细信息报表，其中显示属于所选类别的产品的名称、单位价格、库存单位和订单数。

[![获取选定类别中的类别 Id 参数值 DropDownList](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**图 9**：从所选类别 DropDownList 获取 *`categoryID`* 参数值（[单击以查看完全大小的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png)）

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>步骤2：在 GridView 中显示页脚

GridView 控件可以同时显示页眉行和表尾行。 这些行将分别显示 `ShowHeader` 和 `ShowFooter` 属性的值，`ShowHeader` 默认为 `true` 并 `ShowFooter` 到 `false`。 若要在 GridView 中包含页脚，只需将其 `ShowFooter` 属性设置为 `true`。

[![将 GridView 的 ShowFooter 属性设置为 true](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**图 10**：将 GridView 的 `ShowFooter` 属性设置为 "`true`[" （单击查看完全大小的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png)）

页脚行对于 GridView 中定义的每个字段都有一个单元格;但默认情况下，这些单元格为空。 花点时间在浏览器中查看进度。 现在 `ShowFooter` 属性设置为 `true`，GridView 包含一个空的页脚行。

[![GridView 现在包含一个页脚行](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**图 11**： GridView 现在包含一个页脚行（[单击查看完全尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png)）

图11中的页脚行不会出现问题，因为它具有白色背景。 让我们在 `Styles.css` 中创建指定深红色背景的 `FooterStyle` CSS 类，然后在 `DataWebControls` 主题中配置 `GridView.skin` 皮肤文件，以将此 CSS 类分配给 GridView 的 `FooterStyle``CssClass` 属性。 如果需要在外观和主题上进行画笔处理，请参阅[通过 ObjectDataSource 教程显示数据](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)。

首先，将以下 CSS 类添加到 `Styles.css`：

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

虽然 `HeaderStyle`的背景色个很微妙较深并且其文本以粗体显示，但 `FooterStyle` CSS 类的样式与 `HeaderStyle` 类相似。 此外，页脚中的文本为右对齐，而标题的文本居中。

接下来，若要将此 CSS 类与每个 GridView 的页脚关联，请打开 `DataWebControls` 主题中的 `GridView.skin` 文件，并设置 `FooterStyle`的 `CssClass` 属性。 完成此添加后，该文件的标记应如下所示：

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

如下面的屏幕截图所示，这一更改使页脚更清晰。

[![GridView 的页脚行现在具有 Reddish 背景色](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**图 12**： GridView 的页脚行现在具有 Reddish 背景色（[单击以查看完全尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png)）

## <a name="step-3-computing-the-summary-data"></a>步骤3：计算汇总数据

显示 GridView 的脚注后，下一次面临的挑战是如何计算汇总数据。 可以通过两种方法来计算此聚合信息：

1. 通过 SQL 查询，我们可以向数据库发出附加查询，以便计算特定类别的汇总数据。 SQL 包含若干聚合函数以及 `GROUP BY` 子句，用于指定应汇总数据的数据。 下面的 SQL 查询将返回所需的信息：  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    当然，您不想直接从 `SummaryDataInFooter.aspx` 页发出此查询，而是在 `ProductsTableAdapter` 和 `ProductsBLL`中创建一个方法。
2. 计算此信息，因为它正如 "[基于数据的自定义格式设置](custom-formatting-based-upon-data-cs.md)" 教程中所讨论的那样，将此信息添加到 gridview 后，对于要添加到 gridview 的每个行，`RowDataBound` 将对其进行数据绑定后触发一次。 通过为此事件创建事件处理程序，我们可以保持要聚合的值的运行总计。 最后一个数据行绑定到 GridView 后，我们将计算平均值和计算平均值所需的信息。

我通常使用第二种方法，因为它可以保存对数据库的访问以及在数据访问层和业务逻辑层中实现汇总功能所需的工作，但这两种方法都能满足需要。 对于本教程，我们将使用第二个选项，并使用 `RowDataBound` 事件处理程序跟踪运行总计。

通过在设计器中选择 GridView，单击属性窗口中的闪电形图标，然后双击 `RowDataBound` 事件，为 GridView 创建 `RowDataBound` 事件处理程序。 这会在 `SummaryDataInFooter.aspx` 页的代码隐藏类中创建一个名为 `ProductsInCategory_RowDataBound` 的新事件处理程序。

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

为了保持运行总计，我们需要在事件处理程序的范围以外定义变量。 创建以下四个页面级变量：

- `_totalUnitPrice`，类型 `decimal`
- `_totalNonNullUnitPriceCount`，类型 `int`
- `_totalUnitsInStock`，类型 `int`
- `_totalUnitsOnOrder`，类型 `int`

接下来，编写代码，为 `RowDataBound` 事件处理程序中遇到的每个数据行增加这三个变量。

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

`RowDataBound` 事件处理程序首先确保我们处理的是 DataRow。 建立这一项后，仅绑定到 `e.Row` 中 `GridViewRow` 对象的 `Northwind.ProductsRow` 实例存储在变量 `product`中。 接下来，将按当前产品的相应值（假设它们不包含数据库 `NULL` 值）来递增变量的运行总计。 由于平均价格是这两个数字的商，我们将跟踪同时运行的 `UnitPrice` 总数和非`NULL` `UnitPrice` 记录数。

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>步骤4：在页脚中显示摘要数据

汇总汇总数据后，最后一步是在 GridView 的页脚行中显示它。 还可以通过 `RowDataBound` 事件处理程序以编程方式完成此任务。 请记住，`RowDataBound` 事件处理程序对绑定到 GridView 的*每*一行（包括脚注行）触发。 因此，我们可以使用以下代码扩充事件处理程序，以便在页脚行中显示数据：

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

由于在添加了所有数据行之后将页脚行添加到 GridView，因此，我们可以确信，我们已准备好在页脚中显示汇总数据，此时正在运行的总计算将完成。 最后一个步骤是在页脚的单元格中设置这些值。

若要在特定的页脚单元格中显示文本，请使用 `e.Row.Cells[index].Text = value`，其中 `Cells` 索引从0开始。 下面的代码计算平均价格（总价除以产品数），并将其与 stock 中相应的页脚单元格的库存和单位总数一起显示，并按顺序显示。

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

图13显示了此代码添加后的报告。 请注意，`ToString("c")` 如何使平均价格汇总信息的格式设置为货币格式。

[![GridView 的页脚行现在具有 Reddish 背景色](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**图 13**： GridView 的页脚行现在具有 Reddish 背景色（[单击以查看完全尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png)）

## <a name="summary"></a>总结

显示摘要数据是一种常见的报表要求，而使用 GridView 控件可以轻松地将此类信息包含在其页脚行中。 当 GridView 的 `ShowFooter` 属性设置为 `true` 时，将显示页脚行，并且可以通过 `RowDataBound` 事件处理程序以编程方式设置其单元格中的文本。 可以通过重新查询数据库或使用 ASP.NET 页的代码隐藏类中的代码以编程方式计算汇总数据，来计算汇总数据。

本教程介绍了如何通过 GridView、DetailsView 和 FormView 控件检查自定义格式。 下一教程介绍了如何使用这些相同的控件来浏览插入、更新和删除数据。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](using-the-formview-s-templates-cs.md)
> [下一页](custom-formatting-based-upon-data-vb.md)
