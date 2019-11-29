---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
title: 对 DataList 或 Repeater 控件中的数据进行排序（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将探讨如何在 DataList 和 Repeater 中包含排序支持，以及如何构造其数据可以 。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 97c13898-0741-45f9-b3fa-7540ab1679e6
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 81e07bec8569b9ee987dfaa84dec9eec95a2692f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74638534"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-vb"></a>排序 DataList 或 Repeater 控件中的数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_VB.exe)或[下载 PDF](sorting-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial45vb1.pdf)

> 在本教程中，我们将介绍如何在 DataList 和 Repeater 中加入排序支持，以及如何构造可对其数据进行分页和排序的 DataList 或 Repeater。

## <a name="introduction"></a>简介

在[上一教程](paging-report-data-in-a-datalist-or-repeater-control-vb.md)中，我们探讨了如何向 DataList 添加分页支持。 我们在 `ProductsBLL` 类（`GetProductsAsPagedDataSource`）中创建了一个返回 `PagedDataSource` 对象的新方法。 绑定到 DataList 或中继器时，DataList 或 Repeater 只显示请求的数据页。 此方法类似于 GridView、DetailsView 和 FormView 控件在内部使用的方法，以提供其内置的默认分页功能。

除了提供分页支持以外，GridView 还包括现成的排序支持。 DataList 和 Repeater 都不提供内置排序功能;但是，可以使用一些代码来添加排序功能。 在本教程中，我们将介绍如何在 DataList 和 Repeater 中加入排序支持，以及如何构造可对其数据进行分页和排序的 DataList 或 Repeater。

## <a name="a-review-of-sorting"></a>排序检查

正如我们在[分页和排序报表数据](../paging-and-sorting/paging-and-sorting-report-data-vb.md)教程中看到的那样，GridView 控件提供了现成的排序支持。 每个 GridView 字段都可以有关联的 `SortExpression`，指示对数据进行排序所依据的数据字段。 当 GridView `AllowSorting` 属性设置为 `true`时，具有 `SortExpression` 属性值的每个 GridView 字段的标头将呈现为 LinkButton。 当用户单击某个特定 GridView 字段 "标头" 时，将发生回发，并根据所单击的字段 "`SortExpression`对数据进行排序。

GridView 控件也有一个 `SortExpression` 属性，该属性存储数据排序所依据的 GridView 字段的 `SortExpression`。 此外，`SortDirection` 属性指示是按升序还是降序对数据进行排序（如果用户连续单击特定 GridView 字段标题链接两次，则会切换排序顺序）。

当 GridView 绑定到其数据源控件时，它会将其 `SortExpression`，并 `SortDirection` 属性传递到数据源控件。 数据源控件检索数据，然后根据提供的 `SortExpression` 和 `SortDirection` 属性对数据进行排序。 对数据进行排序后，数据源控件将其返回给 GridView。

若要在 DataList 或 Repeater 控件中复制此功能，必须执行以下操作：

- 创建排序接口
- 记住要按其排序的数据字段，以及是按升序还是按降序排序
- 指示 ObjectDataSource 按特定数据字段对数据进行排序

在步骤3和4中，我们将解决这三个任务。 接下来，我们将探讨如何在 DataList 或中继器中包含分页和排序支持。

## <a name="step-2-displaying-the-products-in-a-repeater"></a>步骤2：在中继器中显示产品

在考虑如何实现任何与排序相关的功能之前，让我们首先列出 Repeater 控件中的产品。 首先打开 `PagingSortingDataListRepeater` 文件夹中的 "`Sorting.aspx`" 页。 将 Repeater 控件添加到网页，并将其 `ID` 属性设置为 `SortableProducts`。 从 "Repeater" 智能标记中创建一个名为 `ProductsDataSource` 的新 ObjectDataSource，并将其配置为从 `ProductsBLL` 类 `GetProducts()` 方法检索数据。 从 "插入"、"更新" 和 "删除" 选项卡的下拉列表中选择 "（无）" 选项。

[![创建 ObjectDataSource 并将其配置为使用 GetProductsAsPagedDataSource （）方法](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**图 1**：创建 ObjectDataSource 并将其配置为使用 `GetProductsAsPagedDataSource()` 方法（[单击查看完全大小的映像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image3.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image4.png)

**图 2**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image6.png)）

与 DataList 不同，Visual Studio 不会在将 Repeater 控件绑定到数据源后自动为其创建 `ItemTemplate`。 而且，我们必须以声明方式添加此 `ItemTemplate`，因为 Repeater 控件的智能标记缺少 DataList s 中的编辑模板选项。 允许使用上一教程中的相同 `ItemTemplate`，其中显示了产品名称、供应商和类别。

添加 `ItemTemplate`后，Repeater 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample1.aspx)]

图3在浏览器中查看时显示此页。

[![显示每个产品的名称、供应商和类别](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**图 3**：显示了每个产品的名称、供应商和类别（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image9.png)）

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>步骤3：指示 ObjectDataSource 对数据进行排序

若要对在 Repeater 中显示的数据进行排序，需要将排序表达式的 ObjectDataSource 通知给数据排序依据。 在 ObjectDataSource 检索其数据之前，它首先会激发其[`Selecting` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)，这为我们提供了指定排序表达式的机会。 `Selecting` 事件处理程序传递[`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)类型的对象，该对象的属性名为[`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)类型。 `DataSourceSelectArguments` 类旨在将数据相关请求从数据使用者传递到数据源控件，并包括[`SortExpression` 属性](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)。

若要将 ASP.NET 页中的排序信息传递到 ObjectDataSource，请为 `Selecting` 事件创建事件处理程序，并使用以下代码：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

应为*sortExpression*值分配数据字段的名称，以便对数据进行排序（例如 ProductName）。 没有与排序方向相关的属性，因此，如果要按降序对数据进行排序，请将字符串 DESC 追加到*sortExpression*值（例如 ProductName DESC）。

继续，尝试为*sortExpression*使用一些不同的硬编码值，并在浏览器中测试结果。 如图4所示，使用 ProductName DESC 作为*sortExpression*时，产品按其名称以逆序字母顺序排序。

[![产品按其名称以逆序字母顺序排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**图 4**：产品按其名称以逆序字母顺序排序（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image12.png)）

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>步骤4：创建排序接口并记住排序表达式和方向

在 GridView 中开启排序支持将每个可排序字段的标头文本转换为 LinkButton，单击此项可对数据进行相应排序。 此类排序接口对 GridView 非常合理，其中的数据在列中整齐地布局。 但对于 DataList 和 Repeater 控件，需要不同的排序接口。 数据列表（而不是数据网格）的常见排序接口是一个下拉列表，提供可用于对数据进行排序的字段。 在本教程中，让 s 实现此类接口。

将 DropDownList Web 控件添加到 `SortableProducts` Repeater 上，并将其 `ID` 属性设置为 "`SortBy`"。 在属性窗口中，单击 "`Items`" 属性中的省略号以显示 "有选择的集合编辑器"。 添加 `ListItem` 以便按 `ProductName`、`CategoryName`和 `SupplierName` 字段对数据进行排序。 另外，还可以添加一个 `ListItem` 以便按其名称以逆序字母顺序对产品进行排序。

`ListItem` `Text` 属性可以设置为任何值（例如名称），但 `Value` 属性必须设置为数据字段的名称（例如 ProductName）。 若要按降序对结果进行排序，请将字符串 DESC 追加到数据字段名称，如 ProductName DESC。

![为每个可排序的数据字段添加一个项](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**图 5**：为每个可排序的数据字段添加 `ListItem`

最后，在 DropDownList 右侧添加一个按钮 Web 控件。 将其 `ID` 设置为 `RefreshRepeater` 及其 `Text` 属性进行刷新。

创建 `ListItem` 并添加 "刷新" 按钮后，DropDownList 和按钮的声明性语法应类似于以下形式：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

排序 DropDownList 完成后，接下来需要更新 ObjectDataSource `Selecting` 事件处理程序，使其使用所选 `SortBy``ListItem` s `Value` 属性，而不是硬编码的排序表达式。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample4.vb)]

此时，第一次访问该页面时，产品最初会按 `ProductName` 数据字段进行排序，因为它是默认选择的 `SortBy` `ListItem` （请参阅图6）。 选择其他排序选项（如 "类别" 和 "刷新"）将导致回发并按类别名称对数据进行重新排序，如图7所示。

[![产品最初按其名称进行排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)

**图 6**：产品最初按其名称进行排序（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)）

[![产品现在按类别排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)

**图 7**：产品现在按类别排序（[单击查看完全尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image19.png)）

> [!NOTE]
> 单击 "刷新" 按钮将导致自动对数据进行重新排序，因为 Repeater 的视图状态已禁用，从而导致 Repeater 在每次回发时重新绑定到其数据源。 如果已启用 "中继器" 视图状态，更改 "排序" 下拉列表将不会对排序顺序产生任何影响。 若要解决此情况，请为 "刷新" 按钮的 `Click` 事件创建事件处理程序，并将中继器重新绑定到其数据源（通过调用 Repeater s `DataBind()` 方法）。

## <a name="remembering-the-sort-expression-and-direction"></a>记住排序表达式和方向

在可能发生非排序相关回发的页上创建可排序的 DataList 或 Repeater 时，需要在回发之间记住排序表达式和方向。 例如，假设我们在本教程中更新了中继器，以包含每个产品的 "删除" 按钮。 当用户单击 "删除" 按钮时，我们将运行一些代码来删除所选产品，然后将数据重新绑定到中继器。 如果未在回发期间保留排序详细信息，则屏幕上显示的数据将恢复为原始排序顺序。

对于本教程，DropDownList 会将排序表达式和方向隐式保存到我们的视图状态。 如果我们使用的是不同的排序接口，比如，LinkButtons 提供了各种排序选项，则需要注意，请记住跨回发的排序顺序。 这可以通过在页的视图状态中存储排序参数来实现，方法是在查询字符串中包含 sort 参数，或者通过某些其他状态持久性方法。

本教程中的后续示例将探讨如何在页的视图状态中保存排序详细信息。

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>步骤5：将排序支持添加到使用默认分页的 DataList

在[前面的教程](paging-report-data-in-a-datalist-or-repeater-control-vb.md)中，我们探讨了如何使用 DataList 实现默认分页。 让我们扩展前面的示例，以包括对分页数据进行排序的功能。 首先打开 `PagingSortingDataListRepeater` 文件夹中的 `SortingWithDefaultPaging.aspx` 和 `Paging.aspx` 页面。 在 "`Paging.aspx`" 页上，单击 "源" 按钮以查看页面的声明性标记。 复制所选文本（见图8），然后将其粘贴到 `<asp:Content>` 标记之间 `SortingWithDefaultPaging.aspx` 的声明性标记中。

[![将 &lt;asp： Content&gt; 标记中的声明性标记从页面 .aspx 复制到 SortingWithDefaultPaging](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)

**图 8**：将 `<asp:Content>` 标记中的声明性标记从 `Paging.aspx` 复制到 `SortingWithDefaultPaging.aspx` （[单击查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image22.png)）

复制声明性标记后，将 `Paging.aspx` 页 s 代码隐藏类中的方法和属性复制到 `SortingWithDefaultPaging.aspx`的代码隐藏类。 接下来，请花点时间查看浏览器中的 "`SortingWithDefaultPaging.aspx`" 页。 它应表现出与 `Paging.aspx`相同的功能和外观。

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>增强 ProductsBLL 以包含默认分页和排序方法

在上一教程中，我们在 `ProductsBLL` 类中创建了一个 `GetProductsAsPagedDataSource(pageIndex, pageSize)` 方法，该方法返回 `PagedDataSource` 对象。 此 `PagedDataSource` 对象是用*所有*产品（通过 BLL 的 `GetProducts()` 方法）填充的，但是当绑定到 DataList 时，仅显示与指定*pageIndex*和*pageSize*输入参数相对应的记录。

在本教程的前面部分，我们通过指定 ObjectDataSource s `Selecting` 事件处理程序中的排序表达式来添加排序支持。 当 ObjectDataSource 返回一个可进行排序的对象（如 `GetProducts()` 方法返回的 `ProductsDataTable`）时，这非常有效。 但是，`GetProductsAsPagedDataSource` 方法返回的 `PagedDataSource` 对象不支持对其内部数据源进行排序。 相反，我们需要先对从 `GetProducts()` 方法返回的结果进行排序，*然后再*将其放入 `PagedDataSource`。

若要实现此目的，请在 `ProductsBLL` 类中创建一个新方法，`GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`。 若要对 `GetProducts()` 方法返回的 `ProductsDataTable` 进行排序，请指定其默认 `DataTableView`的 `Sort` 属性：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`GetProductsSortedAsPagedDataSource` 方法与上一教程中创建的 `GetProductsAsPagedDataSource` 方法稍有不同。 具体而言，`GetProductsSortedAsPagedDataSource` 接受附加输入参数 `sortExpression`，并将该值分配给 `ProductDataTable` `DefaultView`的 `Sort` 属性。 几行代码稍后，会为 `PagedDataSource` 对象的数据源分配 `ProductDataTable` s `DefaultView`。

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>调用 GetProductsSortedAsPagedDataSource 方法并指定 SortExpression 输入参数的值

完成 `GetProductsSortedAsPagedDataSource` 方法后，下一步是提供此参数的值。 `SortingWithDefaultPaging.aspx` 中的 ObjectDataSource 当前配置为调用 `GetProductsAsPagedDataSource` 方法，并通过其两个 `QueryStringParameters`传递两个输入参数，这些参数在 `SelectParameters` 集合中指定。 这两个 `QueryStringParameters` 表示 `GetProductsAsPagedDataSource` 方法 s *pageIndex*和*pageSize*参数的源来自 querystring 字段 `pageIndex` 和 `pageSize`。

更新 ObjectDataSource `SelectMethod` 属性，使其调用新的 `GetProductsSortedAsPagedDataSource` 方法。 然后，添加一个新的 `QueryStringParameter`，以便从 querystring 字段 `sortExpression`访问*sortExpression*输入参数。 将 `QueryStringParameter` `DefaultValue` 设置为 "ProductName"。

进行这些更改后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample6.aspx)]

此时，"`SortingWithDefaultPaging.aspx`" 页将按产品名称的字母顺序对其结果进行排序（参见图9）。 这是因为，默认情况下，ProductName 的值作为 `GetProductsSortedAsPagedDataSource` 方法 s *sortExpression*参数传入。

[![默认情况下，结果按 ProductName 排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)

**图 9**：默认情况下，结果按 `ProductName` 排序（[单击查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)）

如果手动添加 `sortExpression` querystring 字段，如 `SortingWithDefaultPaging.aspx?sortExpression=CategoryName` 结果将按指定 `sortExpression`排序。 但是，当移动到不同的数据页时，此 `sortExpression` 参数不会包含在查询字符串中。 事实上，单击 "下一步" 或 "最后一页" 按钮会使我们恢复 `Paging.aspx`！ 此外，目前还没有排序接口。 用户可以更改分页数据的排序顺序的唯一方式是直接操作 querystring。

## <a name="creating-the-sorting-interface"></a>创建排序接口

首先需要更新 `RedirectUser` 方法，以便将用户发送到 `SortingWithDefaultPaging.aspx` （而不是 `Paging.aspx`）并将 `sortExpression` 值包含在 querystring 中。 还应添加一个名为 `SortExpression` 属性的只读页面级。 此属性类似于在上一教程中创建的 `PageIndex` 和 `PageSize` 属性，如果存在，则返回 `sortExpression` querystring 字段的值，否则返回默认值（ProductName）。

目前 `RedirectUser` 方法仅接受单个输入参数要显示的页的索引。 不过，有时我们希望使用排序表达式（而不是查询字符串中指定的内容）将用户重定向到特定的数据页。 稍后我们将为此页面创建排序界面，其中包含一系列用于按指定列对数据进行排序的按钮 Web 控件。 单击其中一个按钮时，我们希望重定向用户，并传入适当的排序表达式值。 若要提供此功能，请创建 `RedirectUser` 方法的两个版本。 第一个应该只接受要显示的页索引，而第二个只接受页索引和排序表达式。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

在本教程的第一个示例中，我们使用 DropDownList 创建了排序接口。 在此示例中，让我们使用位于 DataList 一的三个按钮 Web 控件进行排序，`ProductName`，一个用于 `CategoryName`，另一个用于 `SupplierName`。 添加三个按钮 Web 控件，并相应地设置其 `ID` 和 `Text` 属性：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample8.aspx)]

接下来，为每个创建一个 `Click` 事件处理程序。 事件处理程序应调用 `RedirectUser` 方法，并使用相应的排序表达式将用户返回到第一页。

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

首次访问该页面时，数据按产品名称字母顺序排序（请参阅图9）。 单击 "下一步" 按钮转到第二页数据，然后单击 "按类别排序" 按钮。 这会将我们返回到第一页数据，按类别名称排序（请参阅图10）。 同样，单击 "按供应商排序" 按钮会按供应商从数据的第一页对数据进行排序。 数据分页到后，会记住排序选项。 图11按类别排序后显示该页，然后转到第十三个数据页。

[按类别对产品进行排序 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)

**图 10**：按类别对产品进行排序（[单击查看全尺寸图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image28.png)）

[![在分页数据时记住排序表达式](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image29.png)

**图 11**：对数据进行分页时，将记住排序表达式（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image31.png)）

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>步骤6：通过中继器中的记录进行自定义分页

通过使用低效的默认分页技术，在步骤5页面中通过其数据检查 DataList 示例。 当对大量数据进行分页时，必须使用自定义分页。 返回[到通过大量数据有效分页](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)并对[自定义分页数据进行排序](../paging-and-sorting/sorting-custom-paged-data-vb.md)教程，我们探讨了默认值和自定义分页之间的差异，以及在 BLL 中创建的方法，以便利用自定义分页数据和对自定义分页数据进行排序。 具体而言，在这两个以前的教程中，我们向 `ProductsBLL` 类中添加了以下三种方法：

- `GetProductsPaged(startRowIndex, maximumRows)` 返回一小部分记录，从*startRowIndex*开始，而不是超过*maximumRows*。
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` 返回按指定*sortExpression*输入参数排序的特定记录子集。
- `TotalNumberOfProducts()` 提供 `Products` 数据库表中的记录总数。

可以使用这些方法通过 DataList 或 Repeater 控件高效地对数据进行分页和排序。 为了说明这一点，让我们首先创建一个具有自定义分页支持的中继器控件;接下来，我们将添加排序功能。

打开 `PagingSortingDataListRepeater` 文件夹中的 "`SortingWithCustomPaging.aspx`" 页，并向页面中添加中继器，并将其 `ID` 属性设置为 "`Products`"。 从 "Repeater" 智能标记中，创建一个名为 `ProductsDataSource`的新 ObjectDataSource。 将其配置为从 `ProductsBLL` 类 `GetProductsPaged` 方法中选择其数据。

[![将 ObjectDataSource 配置为使用 ProductsBLL Class s GetProductsPaged 方法](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image32.png)

**图 12**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProductsPaged` 方法（[单击以查看完全大小的映像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image34.png)）

将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"，然后单击 "下一步" 按钮。 "配置数据源" 向导现在会提示输入 `GetProductsPaged` 方法*startRowIndex*和*maximumRows*输入参数的源。 事实上，会忽略这些输入参数。 相反， *startRowIndex*和*maximumRows*值将通过 ObjectDataSource `Selecting` 事件处理程序中的 `Arguments` 属性传入，就像我们在本教程的第一个演示中指定*sortExpression*的方式一样。 因此，请在向导中将 "参数源" 下拉列表保留为 "无"。

[![将参数源设置为 "无"](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image35.png)

**图 13**：将参数源设置为 "无" （[单击查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image37.png)）

> [!NOTE]
> 不要将 ObjectDataSource `EnablePaging`*属性设置为*`true`。 这将导致 ObjectDataSource 自动将其自己的*startRowIndex*和*maximumRows*参数添加到 `SelectMethod` 的现有参数列表中。 将自定义分页数据绑定到 GridView、DetailsView 或 FormView 控件时，`EnablePaging` 属性非常有用，因为这些控件预计在 `EnablePaging` 属性 `true`时，仅可用于 ObjectDataSource 的某些行为。 由于我们必须手动添加 DataList 和 Repeater 的分页支持，因此，请将此属性设置为 `false` （默认值），因为我们会直接在 ASP.NET 页面中制作所需功能。

最后，定义中继站 `ItemTemplate` 以便显示产品的名称、类别和供应商。 进行这些更改之后，中继器和 ObjectDataSource 声明性语法应类似于以下形式：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample10.aspx)]

请花点时间通过浏览器访问该页，并注意不返回任何记录。 这是因为我们还需要指定*startRowIndex*和*maximumRows*参数值;因此，为两者传入0值。 若要指定这些值，请为 ObjectDataSource `Selecting` 事件创建事件处理程序，并以编程方式将这些参数值设置为分别为0和5的硬编码值：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample11.vb)]

进行此更改后，在浏览器中查看页面时，会显示前5个产品。

[显示前5条记录 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image38.png)

**图 14**：显示前5条记录（[单击查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image40.png)）

> [!NOTE]
> 图14中列出的产品将按产品名称进行排序，这是因为执行有效自定义分页查询的 `GetProductsPaged` 存储过程按 `ProductName`对结果进行排序。

为了允许用户单步执行页面，我们需要跟踪起始行索引和最大行数，并在回发之间记住这些值。 在默认分页示例中，我们使用了 querystring 字段来保存这些值;对于此演示，让我们在页的视图状态中保存此信息。 创建以下两个属性：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample12.vb)]

接下来，更新选择事件处理程序中的代码，使其使用 `StartRowIndex` 和 `MaximumRows` 属性，而不是硬编码值0和5：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample13.vb)]

此时，页面仍只显示前五个记录。 但是，在设置了这些属性后，我们就可以创建分页接口了。

## <a name="adding-the-paging-interface"></a>添加分页接口

允许使用默认分页示例中使用的第一个、上一个、下一个和最后一个分页接口，包括显示正在查看的数据页的标签 Web 控件以及存在的总页数。 在中继器下面添加四个按钮 Web 控件和标签。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample14.aspx)]

接下来，为四个按钮创建 `Click` 事件处理程序。 单击其中一个按钮时，需要更新 `StartRowIndex`，然后将数据重新绑定到中继器。 "上一步"、"上一步" 和 "下一步" 按钮的代码非常简单，但对于最后一个按钮，我们如何确定最后一个数据页的起始行索引？ 若要计算此索引以及能否确定是否应启用 "下一步" 和 "上一个" 按钮，我们需要知道正在分页到的记录数。 可以通过调用 `ProductsBLL` 类 `TotalNumberOfProducts()` 方法来确定这一点。 让我们创建一个名为 `TotalRowCount` 的只读属性，该属性将返回 `TotalNumberOfProducts()` 方法的结果：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample15.vb)]

通过此属性，我们现在可以确定最后一页的起始行索引。 具体而言，它是 `TotalRowCount` 减1除以 `MaximumRows`（乘以 `MaximumRows`）的整数结果。 现在，我们可以为四个分页接口按钮编写 `Click` 事件处理程序：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample16.vb)]

最后，当查看第一页数据时，需要禁用分页界面中的第一个和最后一个按钮，并在查看最后一个页面时禁用 "下一个" 和 "最后一个" 按钮。 若要实现此目的，请将以下代码添加到 ObjectDataSource s `Selecting` 事件处理程序：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample17.vb)]

添加这些 `Click` 事件处理程序和代码以根据当前起始行索引启用或禁用分页接口元素后，请在浏览器中测试页面。 如图15所示，第一次访问页面时，第一个和前一个按钮将被禁用。 单击 "下一步" 将显示第二页数据，而单击 "最后" 将显示最后一页（请参阅图16和17）。 查看数据的最后一页时，"下一步" 和 "最后一个" 按钮将被禁用。

[查看产品的第一页时，![上一个和最后一个按钮被禁用](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image41.png)

**图 15**：查看产品的第一页时，上一个和最后一个按钮被禁用（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image43.png)）

[显示产品的第二页 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image44.png)

**图 16**：显示了产品的第二页（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image46.png)）

[![单击 "上一步" 将显示最后一页的数据](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image47.png)

**图 17**：单击 "上一步" 将显示最后一页的数据（[单击查看完全尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image49.png)）

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>步骤7：包含对自定义分页中继器的排序支持

现在已经实现了自定义分页，我们已准备好加入排序支持。 `ProductsBLL` 类 `GetProductsPagedAndSorted` 方法具有与 `GetProductsPaged`相同的*startRowIndex*和*maximumRows*输入参数，但允许附加*sortExpression*输入参数。 若要从 `SortingWithCustomPaging.aspx`使用 `GetProductsPagedAndSorted` 方法，需要执行以下步骤：

1. 将 ObjectDataSource `SelectMethod` 属性从 `GetProductsPaged` 更改为 `GetProductsPagedAndSorted`。
2. 将*sortExpression* `Parameter` 对象添加到 ObjectDataSource `SelectParameters` 集合。
3. 创建专用的页面级 `SortExpression` 属性，该属性通过页面的视图状态在回发之间保持其值。
4. 更新 ObjectDataSource `Selecting` 事件处理程序，以便为 ObjectDataSource s *sortExpression*参数分配页面级 `SortExpression` 属性的值。
5. 创建排序接口。

首先更新 ObjectDataSource `SelectMethod` 属性并添加*sortExpression* `Parameter`。 请确保*sortExpression* `Parameter` s `Type` 属性设置为 "`String`"。 完成前两个任务后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample18.aspx)]

接下来，需要一个页级 `SortExpression` 属性，其值被序列化为视图状态。 如果未设置排序表达式值，请使用 ProductName 作为默认值：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample19.vb)]

在 ObjectDataSource 调用 `GetProductsPagedAndSorted` 方法之前，我们需要将*sortExpression* `Parameter` 设置为 `SortExpression` 属性的值。 在 `Selecting` 事件处理程序中，添加以下代码行：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample20.vb)]

剩下的就是实现排序接口。 正如我们在上一示例中所做的那样，让我们使用三个按钮 Web 控件实现了排序界面，用户可以按产品名称、类别或供应商对结果进行排序。

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample21.aspx)]

为这三个按钮控件创建 `Click` 事件处理程序。 在事件处理程序中，将 `StartRowIndex` 重置为0，将 `SortExpression` 设置为适当的值，并将数据重新绑定到 Repeater：

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample22.vb)]

就是这样！ 虽然实现自定义分页和排序的步骤很多，但这些步骤与默认分页的步骤非常类似。 图18显示了按类别排序后查看数据的最后一页的产品。

[显示最后一个数据页，按类别排序，随即显示 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image50.png)

**图 18**：显示了按类别排序的最后一页数据（[单击以查看完全大小的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image52.png)）

> [!NOTE]
> 在前面的示例中，当供应商供应商进行排序时，使用的是排序表达式。 但是，对于自定义分页实现，我们需要使用 "公司名称"。 这是因为负责实现自定义分页的存储过程 `GetProductsPagedAndSorted` 将排序表达式传递到 `ROW_NUMBER()` 关键字，`ROW_NUMBER()` 关键字需要实际列名而不是别名。 因此，必须使用 `CompanyName` （`Suppliers` 表中列的名称），而不是在用于排序表达式的 `SELECT` 查询（`SupplierName`）中使用的别名。

## <a name="summary"></a>总结

DataList 和 Repeater 都无法提供内置排序支持，但有一些代码和自定义排序接口，可以添加此类功能。 实现排序而不是分页时，可以通过传递到 ObjectDataSource s `Select` 方法中的 `DataSourceSelectArguments` 对象指定排序表达式。 此 `DataSourceSelectArguments` 对象 s `SortExpression` 属性可在 ObjectDataSource `Selecting` 事件处理程序中进行分配。

若要向已提供分页支持的 DataList 或中继器添加排序功能，最简单的方法是自定义业务逻辑层以包含接受排序表达式的方法。 然后，可以通过 `SelectParameters`中的参数在中传递此信息。

本教程完成了对 DataList 和 Repeater 控件的分页和排序检查。 我们的下一个和最后一个教程将介绍如何将按钮 Web 控件添加到 DataList 和 Repeater 模板中，以便基于每个项提供一些自定义的、用户启动的功能。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导审查人员是 David Suru。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一部分](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
