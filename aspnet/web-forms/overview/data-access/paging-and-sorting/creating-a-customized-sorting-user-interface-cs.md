---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
title: 创建自定义的排序用户界面C#（） |Microsoft Docs
author: rick-anderson
description: 显示已排序数据的长列表时，通过引入分隔符行对相关数据进行分组非常有用。 在本教程中，我们将了解如何凭据
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 6f81b633-9d01-4e52-ae4a-2ea6bc109475
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 93ec07a13de80e4c874ff46b5dfa626b60b632c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78502706"
---
# <a name="creating-a-customized-sorting-user-interface-c"></a>创建自定义的排序用户界面 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_CS.exe)或[下载 PDF](creating-a-customized-sorting-user-interface-cs/_static/datatutorial27cs1.pdf)

> 显示已排序数据的长列表时，通过引入分隔符行对相关数据进行分组非常有用。 在本教程中，我们将了解如何创建此类排序用户界面。

## <a name="introduction"></a>简介

当在已排序的列中显示仅有少量不同值的已排序数据的长列表时，最终用户可能会发现很难识别差异边界的确切位置。 例如，数据库中有81个产品，但仅有九个不同的类别选项（8个唯一类别加上 `NULL` 选项）。 假设有兴趣检查 "海鲜" 类别下的产品的用户。 从列出单个 GridView 中*所有*产品的页面中，用户可能会决定，最佳做法是按类别对结果进行排序，这会将所有海鲜产品组合在一起。 按类别排序后，用户需要通读列表，寻找海鲜分组的产品开始和结束的位置。 由于结果按类别名称的字母顺序排序，查找海鲜产品并不困难，但仍需要密切扫描网格中的项目列表。

为了帮助突出显示已排序组之间的边界，许多网站使用在此类组之间添加分隔符的用户界面。 类似于图1所示的分隔符使用户能够更快地查找特定组并标识其边界，还可以确定数据中存在哪些不同的组。

[明确标识每个类别组 ![](creating-a-customized-sorting-user-interface-cs/_static/image2.png)](creating-a-customized-sorting-user-interface-cs/_static/image1.png)

**图 1**：清楚地确定每个类别组（[单击以查看完全大小的图像](creating-a-customized-sorting-user-interface-cs/_static/image3.png)）

在本教程中，我们将了解如何创建此类排序用户界面。

## <a name="step-1-creating-a-standard-sortable-gridview"></a>步骤1：创建标准的可排序 GridView

在了解如何增强 GridView 来提供增强的排序界面之前，首先请创建一个列出产品的标准、可排序的 GridView。 首先打开 `PagingAndSorting` 文件夹中的 "`CustomSortingUI.aspx`" 页。 将 GridView 添加到页面，将其 `ID` 属性设置为 `ProductList`，并将其绑定到新的 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProducts()` 方法来选择记录。

接下来，配置 GridView，使其仅包含 `ProductName`、`CategoryName`、`SupplierName`和 `UnitPrice` BoundFields 以及中止的 CheckBoxField。 最后，通过选中 GridView s 智能标记（或通过将其 `AllowSorting` 属性设置为 `true`）中的 "启用排序" 复选框来配置 GridView，以支持排序。 将这些添加到 `CustomSortingUI.aspx` 页后，声明性标记应如下所示：

[!code-aspx[Main](creating-a-customized-sorting-user-interface-cs/samples/sample1.aspx)]

花点时间在浏览器中查看进度。 图2显示了按类别（按字母顺序）对其数据进行排序时可排序的 GridView。

[![可排序的 GridView s 数据按类别排序](creating-a-customized-sorting-user-interface-cs/_static/image5.png)](creating-a-customized-sorting-user-interface-cs/_static/image4.png)

**图 2**：可排序的 GridView 数据按类别排序（[单击以查看完全大小的图像](creating-a-customized-sorting-user-interface-cs/_static/image6.png)）

## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>步骤2：探索用于添加分隔符行的技术

一般的可排序 GridView 完成后，剩下的就是能够在 GridView 中的每个唯一排序组之前添加分隔行。 但如何将此类行注入到 GridView 中呢？ 实质上，我们需要遍历 GridView 的行，确定排序列中的值之间的差异，然后添加相应的分隔符行。 在考虑此问题时，解决方案似乎很自然 `RowDataBound` 事件处理程序中的某个位置。 如我们在[基于数据的自定义格式设置](../custom-formatting/custom-formatting-based-upon-data-cs.md)教程中所述，此事件处理程序通常在基于行的数据应用行级格式设置时使用。 但 `RowDataBound` 事件处理程序并不是解决方案，因为不能通过此事件处理程序以编程方式向 GridView 添加行。 实际上，GridView `Rows` 集合为只读。

若要将其他行添加到 GridView，我们有三个选择：

- 将这些元数据分隔符行添加到绑定到 GridView 的实际数据
- 将 GridView 绑定到数据后，将其他 `TableRow` 实例添加到 GridView s 控件集合
- 创建一个自定义服务器控件，该控件扩展 GridView 控件并替代负责构造 GridView s 结构的方法

如果需要在多个网页上或在多个网站上使用此功能，则创建自定义服务器控件将是最佳方法。 不过，它会执行相当多的代码，并全面探索 GridView 内部工作原理的深度。 因此，在本教程中，我们不会考虑该选项。

其他两个选项可将分隔符行添加到要绑定到 GridView 的实际数据，并在其绑定后操作 GridView s 控制集合。

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>向 GridView 绑定的数据中添加行

当 GridView 绑定到数据源时，它将为数据源返回的每个记录创建一个 `GridViewRow`。 因此，可以在将分隔符记录到 GridView 之前，通过在数据源中添加分隔符记录来注入所需的分隔行。 图3说明了这一概念。

![一种方法是向数据源添加分隔行](creating-a-customized-sorting-user-interface-cs/_static/image7.png)

**图 3**：其中一项技术涉及到将分隔符行添加到数据源

我在引号中使用术语分隔符记录，因为没有特殊的分隔符记录;相反，我们必须将数据源中的特定记录作为分隔符而不是普通数据行来标记。 对于我们的示例，我们将 `ProductsDataTable` 实例绑定到由 `ProductRows`组成的 GridView。 我们可能会将记录标记为分隔符行，方法是将其 `CategoryID` 属性设置为 `-1` （因为这样的值无法正常存在）。

若要利用此方法，我们需要执行以下步骤：

1. 以编程方式检索要绑定到 GridView 的数据（`ProductsDataTable` 实例）
2. 基于 GridView `SortExpression` 和 `SortDirection` 属性对数据进行排序
3. 遍历 `ProductsDataTable`中的 `ProductsRows`，查找排序列中的差异的位置
4. 在每个组边界，将分隔符记录 `ProductsRow` 实例插入到 DataTable 中，其中一个 `CategoryID` 设置为 `-1` （或决定将记录标记为分隔符记录的任何指定）
5. 注入分隔符行后，以编程方式将数据绑定到 GridView

除了这五个步骤，我们还需要为 GridView `RowDataBound` 事件提供事件处理程序。 在这里，我们将检查每个 `DataRow`，并确定它是否是一个 `CategoryID` 设置 `-1`的分隔行。 如果是这样，则 d 可能需要调整其格式或单元格中显示的文本。

使用此方法注入排序组边界需要的工作比上面所述的更多，因为还需要为 GridView `Sorting` 事件提供事件处理程序，并跟踪 `SortExpression` 和 `SortDirection` 值。

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>在数据绑定后操作 GridView s 控件集合

在将数据绑定到 GridView 之前，我们可以添加*分隔符行，* 而不是将数据绑定到 gridview。 数据绑定过程构建 GridView s 控件层次结构，实际上只是一个由行集合组成的 `Table` 实例，其中每个行都由一个单元集合组成。 具体而言，GridView s 控件集合在其根上包含一个 `Table` 对象，对绑定到 GridView 的 `DataSource` 中的每个记录都包含一个 `GridViewRow` （派生自 `TableRow` 类），在 `TableCell` 中的每个数据字段的每个 `GridViewRow` 实例中包含一个 `DataSource`对象。

若要在每个排序组之间添加分隔行，可以在创建此控件层次结构后直接对其进行操作。 我们可以确信在呈现页面的时间上最后一次创建了 GridView s 控件层次结构。 因此，此方法会重写 `Page` 类的 `Render` 方法，此时将对 GridView s final 控件层次结构进行更新，以包括所需的分隔符行。 图4说明了此过程。

[![一种替代方法，操作 GridView 的控件层次结构](creating-a-customized-sorting-user-interface-cs/_static/image9.png)](creating-a-customized-sorting-user-interface-cs/_static/image8.png)

**图 4**：一种替代方法，操作 GridView s 控件层次结构（[单击以查看完全大小的图像](creating-a-customized-sorting-user-interface-cs/_static/image10.png)）

对于本教程，我们将使用后一种方法自定义排序用户体验。

> [!NOTE]
> 本教程中所示的代码是基于[Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s 博客文章中提供的示例，[使用 GridView 排序分组](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)。

## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>步骤3：将分隔符行添加到 GridView s 控件层次结构

由于我们只想在创建了控件层次结构并为其创建了控件层次结构后，才需要将分隔符行添加到 GridView s 控件层次结构中，因此我们希望在页面生命周期结束时执行此添加，但在实际 GridView c 之前执行此添加控制层次结构已呈现为 HTML。 可以完成此操作的最新可能点是 `Page` 类 `Render` 事件，可以使用以下方法签名在代码隐藏类中重写：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample2.cs)]

当调用 `Page` 类的原始 `Render` 方法时 `base.Render(writer)` 将呈现该页中的每个控件，并根据控件层次结构生成标记。 因此，我们必须调用 `base.Render(writer)`，以便呈现页面，并在调用 `base.Render(writer)`之前操作 GridView s 控件层次结构，以便在呈现后将分隔符行添加到 GridView s 控制层次结构中。

若要注入排序组标题，首先需要确保用户已请求对数据进行排序。 默认情况下，GridView 的内容不会进行排序，因此，我们不需要输入任何组排序标头。

> [!NOTE]
> 如果希望在第一次加载页面时按特定列对 GridView 进行排序，请在第一页上调用 GridView s `Sort` 方法（而不是在后续回发上）。 若要实现此目的，请将此调用添加到 `if (!Page.IsPostBack)` 条件下的 `Page_Load` 事件处理程序中。 有关 `Sort` 方法的详细信息，请参阅查看[分页和排序报表数据](paging-and-sorting-report-data-cs.md)教程信息。

假设数据已排序，下一项任务是确定数据排序所依据的列，然后扫描行以查找该列的值之间的差异。 下面的代码可确保数据已排序，并找到数据排序所依据的列：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample3.cs)]

如果 GridView 尚未进行排序，则将不会设置 GridView 的 `SortExpression` 属性。 因此，仅当此属性有一些值时，才需要添加分隔行。 如果是这样，接下来需要确定数据排序所依据的列的索引。 这是通过以下方式实现的：遍历 GridView `Columns` 集合，搜索其 `SortExpression` 属性等于 GridView `SortExpression` 属性的列。 除了列 s 索引外，我们还获取 `HeaderText` 属性，该属性在显示分隔符行时使用。

通过对数据进行排序所依据的列的索引，最后一步是枚举 GridView 的行。 对于每一行，我们需要确定已排序的列的值是否与上一行的排序列值不同。 如果是这样，则需要将新的 `GridViewRow` 实例注入到控件层次结构中。 这是通过以下代码完成的：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample4.cs)]

此代码首先以编程方式引用在 GridView s 控件层次结构的根中找到的 `Table` 对象，并创建一个名为 `lastValue`的字符串变量。 `lastValue` 用于将当前行的已排序列值与上一行的值进行比较。 接下来，将对 GridView `Rows` 集合进行枚举，并为每行存储已排序的列的值，并将其存储在 `currentValue` 变量中。

> [!NOTE]
> 若要确定特定行的排序列值，请使用 cell `Text` 属性。 这适用于 BoundFields，但不会按所需的 Templatefield、CheckBoxFields 等方式工作。 接下来，我们将介绍如何考虑备用 GridView 字段。

然后，比较 `currentValue` 和 `lastValue` 变量。 如果它们不同，我们需要向控件层次结构中添加一个新的分隔行。 这是通过以下方式实现的：确定 `Table` 对象 s `Rows` 集合中 `GridViewRow` 的索引，创建新的 `GridViewRow` 和 `TableCell` 实例，然后将 `TableCell` 和 `GridViewRow` 添加到控件层次结构。

请注意，分隔符行 `TableCell` 的格式设置为跨越整个 GridView 的宽度，并使用 `SortHeaderRowStyle` CSS 类进行格式化，并具有其 `Text` 属性，使其显示排序组名称（如类别）和组 s 值（如饮料）。 最后，`lastValue` 更新为 `currentValue`的值。

用于设置排序组标题行格式的 CSS 类 `SortHeaderRowStyle` 需要在 `Styles.css` 文件中指定。 可随意使用任何喜欢的样式设置;我使用了以下内容：

[!code-css[Main](creating-a-customized-sorting-user-interface-cs/samples/sample5.css)]

使用当前代码时，排序接口会在按任何 BoundField 进行排序时添加排序组标头（请参阅图5，其中显示按供应商进行排序时的屏幕截图）。 但是，如果按任何其他字段类型（如 CheckBoxField 或 TemplateField）进行排序，则不会找到排序组标头（见图6）。

[![排序接口在按 BoundFields 排序时包括排序组标头](creating-a-customized-sorting-user-interface-cs/_static/image12.png)](creating-a-customized-sorting-user-interface-cs/_static/image11.png)

**图 5**：按 BoundFields 排序时，排序接口包括排序组标头（[单击以查看完全大小的图像](creating-a-customized-sorting-user-interface-cs/_static/image13.png)）

[排序 CheckBoxField 时，缺少排序组标头 ![](creating-a-customized-sorting-user-interface-cs/_static/image15.png)](creating-a-customized-sorting-user-interface-cs/_static/image14.png)

**图 6**：对 CheckBoxField 进行排序时排序组标头缺失（[单击以查看完全大小的图像](creating-a-customized-sorting-user-interface-cs/_static/image16.png)）

当 CheckBoxField 进行排序时，排序组标头缺失是因为代码当前只使用 `TableCell` s `Text` 属性来确定每行的已排序列的值。 对于 CheckBoxFields，`TableCell` s `Text` 属性为空字符串;值可通过位于 `TableCell` `Controls` 集合中的复选框 Web 控件来使用。

若要处理 BoundFields 以外的字段类型，我们需要增加指定 `currentValue` 变量的代码，以检查 `TableCell` s `Controls` 集合中是否存在复选框。 将此代码替换为以下代码，而不是使用 `currentValue = gvr.Cells[sortColumnIndex].Text`：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample6.cs)]

此代码检查当前行的已排序列 `TableCell`，以确定 `Controls` 集合中是否有任何控件。 如果有，并且第一个控件为复选框，则 `currentValue` 变量将设置为 "是" 或 "否"，具体取决于 `Checked` 属性的复选框。 否则，将从 `TableCell` s `Text` 属性获取值。 可以复制此逻辑来处理 GridView 中可能存在的任何 Templatefield 的排序。

如果使用上面的代码添加，排序组标头将在按中止的 CheckBoxField 排序时立即存在（请参见图7）。

[![排序 CheckBoxField 时，排序组标头现在存在](creating-a-customized-sorting-user-interface-cs/_static/image18.png)](creating-a-customized-sorting-user-interface-cs/_static/image17.png)

**图 7**：对 CheckBoxField 进行排序时，排序组标题现在存在（[单击以查看完全大小的图像](creating-a-customized-sorting-user-interface-cs/_static/image19.png)）

> [!NOTE]
> 如果产品具有 `CategoryID`、`SupplierID`或 `UnitPrice` 字段的 `NULL` 数据库值，则默认情况下，这些值将在 GridView 中显示为空字符串，这意味着，具有 `NULL` 值的产品的分隔符行 s 将按如下所示读取：（也就是说，Category 后没有名称，如 category：饮料）。 如果需要此处显示的值，可以将 BoundFields [`NullDisplayText` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx)设置为要显示的文本，或者可以在将 `currentValue` 分配给分隔符行 s `Text` 属性时，在 Render 方法中添加条件语句。

## <a name="summary"></a>摘要

GridView 不包含用于自定义排序界面的许多内置选项。 但是，在很多低级别的代码中，可以调整 GridView s 控制层次结构，以创建更多的自定义界面。 在本教程中，我们介绍了如何为可排序的 GridView 添加排序组分隔符行，以便更轻松地识别不同组和这些组边界。 有关自定义排序接口的其他示例，请查看[Scott Guthrie](https://weblogs.asp.net/scottgu/) s [ASP.NET 2.0 GridView 排序提示和技巧](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx)博客条目。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](sorting-custom-paged-data-cs.md)
> [下一页](paging-and-sorting-report-data-vb.md)
