---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
title: 对 DataList 或 Repeater 控件中的报表数据进行分页（VB） |Microsoft Docs
author: rick-anderson
description: 尽管 DataList 和中继器都不提供自动分页或排序支持，但本教程介绍了如何向 DataList 或中继器添加分页支持,。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: bbd6b7f7-b98a-48b4-93f3-341d6a4f53c0
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c65ca1f263e41748d99323dbdf1c28fdd077246
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78503090"
---
# <a name="paging-report-data-in-a-datalist-or-repeater-control-vb"></a>分页 DataList 或 Repeater 控件中的报表数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_VB.exe)或[下载 PDF](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial44vb1.pdf)

> 尽管 DataList 和中继器都不提供自动分页或排序支持，但本教程还介绍了如何将分页支持添加到 DataList 或中继器，这允许实现更灵活的分页和数据显示界面。

## <a name="introduction"></a>简介

在联机应用程序中显示数据时，分页和排序是两种非常常见的功能。 例如，在在线书店搜索 ASP.NET 书籍时，可能会有数百个这类书籍，但是列出搜索结果的报告只列出每页的十个匹配项。 而且，结果可以按标题、价格、页计数、作者姓名等进行排序。 正如我们在[分页和排序报表数据](../paging-and-sorting/paging-and-sorting-report-data-vb.md)教程中讨论的那样，GridView、DetailsView 和 FormView 控件都提供了可在复选框的勾选标记下启用的内置分页支持。 GridView 还包括排序支持。

遗憾的是，DataList 和中继器都不提供自动分页或排序支持。 在本教程中，我们将讨论如何向 DataList 或中继器添加分页支持。 我们必须手动创建分页接口，显示适当的记录页，并记住跨回发访问的页面。 尽管这需要花费更多的时间和代码，而不是使用 GridView、DetailsView 或 FormView，但 DataList 和 Repeater 允许使用更灵活的分页和数据显示界面。

> [!NOTE]
> 本教程专门讲述分页。 在下一教程中，我们将重点介绍如何添加排序功能。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>步骤1：添加分页和排序教程网页

开始本教程之前，先花点时间添加本教程和下一教程所需的 ASP.NET 页面。 首先，在项目中创建一个名为 `PagingSortingDataListRepeater`的新文件夹。 接下来，将以下五个 ASP.NET 页面添加到此文件夹，所有这些页面都配置为使用母版页 `Site.master`：

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`

![创建 PagingSortingDataListRepeater 文件夹并添加教程 ASP.NET 页面](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**图 1**：创建 `PagingSortingDataListRepeater` 文件夹并添加教程 ASP.NET 页面

接下来，打开 `Default.aspx` 页面，并将 `SectionLevelTutorialListing.ascx` 用户控件从 `UserControls` 文件夹拖到设计图面上。 此用户控件（我们在[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中创建）枚举站点地图，并在项目符号列表中的当前部分显示这些教程。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image4.png)）

为了使项目符号列表显示我们要创建的分页和排序教程，我们需要将它们添加到站点地图。 打开 `Web.sitemap` 文件，并在编辑后添加以下标记并删除 DataList 站点地图节点标记：

[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample1.xml)]

![更新站点映射以包括新的 ASP.NET 页面](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)

**图 3**：更新站点映射以包括新的 ASP.NET 页面

## <a name="a-review-of-paging"></a>查看分页

在前面的教程中，我们看到了如何逐页浏览 GridView、DetailsView 和 FormView 控件中的数据。 这三个控件提供一种称为*默认分页*的简单分页，只需选中 "控制" 智能标记中的 "启用分页" 选项即可实现。 使用默认分页时，每次在第一页上请求数据页时，或者当用户导航到不同的数据页时，GridView、DetailsView 或 FormView 控件会重新请求 ObjectDataSource 中的*所有*数据。 然后，它将显示给定请求的页索引和每页显示的记录数的特定记录集。 我们在[分页和排序报表数据](../paging-and-sorting/paging-and-sorting-report-data-vb.md)教程中详细讨论了默认分页。

由于默认寻呼会重新请求每个页面的所有记录，因此在通过足够大量的数据进行分页时，这种情况并不可行。 例如，假设页面大小为10的50000记录。 用户每次移动到新页时，都必须从数据库检索所有50000记录，即使只显示了其中的十个记录。

*自定义分页*通过仅获取在请求的页上显示的记录的精确子集，来解决默认分页的性能问题。 实现自定义分页时，必须编写只返回正确记录集的 SQL 查询。 我们已了解如何使用 SQL Server 2005 s new [`ROW_NUMBER()` 关键字](http://www.4guysfromrolla.com/webtech/010406-1.shtml)，[通过大量数据有效分页](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)来创建此类查询。

若要在 DataList 或 Repeater 控件中实现默认分页，可以使用[`PagedDataSource` 类](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx)作为正在分页的 `ProductsDataTable` 周围的包装器。 `PagedDataSource` 类具有一个 `DataSource` 属性，该属性可分配给任何可枚举对象，并[`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx)和[`CurrentPageIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx)属性，这些属性指示每页显示的记录数和当前页索引。 设置这些属性后，可以将 `PagedDataSource` 用作任何数据 Web 控件的数据源。 枚举的 `PagedDataSource`将仅根据 `PageSize` 和 `CurrentPageIndex` 属性返回其内部 `DataSource` 的适当记录子集。 图4演示了 `PagedDataSource` 类的功能。

![PagedDataSource 使用可分页接口包装可枚举对象](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image6.png)

**图 4**： `PagedDataSource` 使用可分页接口包装可枚举对象

`PagedDataSource` 对象可以直接从业务逻辑层创建和配置，并通过 ObjectDataSource 绑定到 DataList 或中继器，也可以直接在 ASP.NET page s 代码隐藏类中创建和配置。 如果使用后一种方法，则必须使用 ObjectDataSource 放弃，并以编程方式将分页数据绑定到 DataList 或 Repeater。

`PagedDataSource` 对象还具有支持自定义分页的属性。 但是，我们可以绕过使用 `PagedDataSource` 进行自定义分页，因为在 `ProductsBLL` 类中已经有为自定义分页设计的 BLL 方法，该方法返回要显示的精确记录。

在本教程中，我们将介绍如何通过将新方法添加到 `ProductsBLL` 类（该方法返回适当配置的 `PagedDataSource` 对象）来实现 DataList 中的默认分页。 在下一教程中，我们将了解如何使用自定义分页。

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>步骤2：在业务逻辑层中添加默认分页方法

`ProductsBLL` 类当前有一种方法，用于返回所有产品信息 `GetProducts()`，一个方法用于返回 `GetProductsPaged(startRowIndex, maximumRows)`起始索引处的特定产品子集。 使用默认分页时，GridView、DetailsView 和 FormView 控件都使用 `GetProducts()` 方法检索所有产品，但随后使用 `PagedDataSource` 来只显示正确的记录子集。 若要使用 DataList 和 Repeater 控件复制此功能，可以在具有模拟此行为的 BLL 中创建新方法。

将一个方法添加到名为 `GetProductsAsPagedDataSource` 的 `ProductsBLL` 类，该方法采用两个整数输入参数：

- `pageIndex` 要显示的页的索引，索引为零和
- `pageSize` 每页显示的记录数。

`GetProductsAsPagedDataSource` 首先从 `GetProducts()`检索*所有*记录。 然后，它将创建一个 `PagedDataSource` 对象，并将其 `CurrentPageIndex` 和 `PageSize` 属性设置为传入的 `pageIndex` 和 `pageSize` 参数的值。 方法通过返回此配置的 `PagedDataSource`来结束：

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>步骤3：使用默认分页在 DataList 中显示产品信息

将 `GetProductsAsPagedDataSource` 方法添加到 `ProductsBLL` 类中后，现在可以创建提供默认分页的 DataList 或 Repeater。 首先打开 `PagingSortingDataListRepeater` 文件夹中的 "`Paging.aspx`" 页，然后从 "工具箱" 中将 DataList 拖到设计器上，将 DataList s `ID` 属性设置为 "`ProductsDefaultPaging`"。 从 DataList s 智能标记中创建一个名为 `ProductsDefaultPagingDataSource` 的新 ObjectDataSource，并对其进行配置，使其使用 `GetProductsAsPagedDataSource` 方法检索数据。

[![创建 ObjectDataSource 并将其配置为使用 GetProductsAsPagedDataSource （）方法](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**图 5**：创建 ObjectDataSource 并将其配置为使用 `GetProductsAsPagedDataSource` `()` 方法（[单击查看完全大小的映像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image9.png)）

将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**图 6**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image12.png)）

由于 `GetProductsAsPagedDataSource` 方法需要两个输入参数，因此向导会提示我们输入这些参数值的源。

必须跨回发记住页索引和页大小值。 它们可以存储在视图状态中，保存到 querystring，存储在 session 变量中，或使用其他方法记住。 对于本教程，我们将使用 querystring，该查询的优点是允许将特定的数据页作为书签。

具体而言，请分别对 `pageIndex` 和 `pageSize` 参数使用 querystring 字段 pageIndex 和 pageSize （参见图7）。 请花片刻时间为这些参数设置默认值，因为当用户第一次访问此页时，查询字符串值不会出现。 对于 "`pageIndex`"，将默认值设置为0（显示数据的第一页） `pageSize`，将默认值设置为4。

[![使用 QueryString 作为 pageIndex 和 pageSize 参数的源](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**图 7**：使用 QueryString 作为 `pageIndex` 和 `pageSize` 参数的源（[单击查看完全大小的映像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image15.png)）

配置 ObjectDataSource 后，Visual Studio 会自动为 DataList 创建 `ItemTemplate`。 自定义 `ItemTemplate` 以便只显示产品的名称、类别和供应商。 同时，将 DataList s `RepeatColumns` 属性设置为2，将其 `Width` 为100%，并将其 `ItemStyle` `Width` 为50%。 这些宽度设置将为这两列提供相等的间距。

进行这些更改后，DataList 和 ObjectDataSource 的标记应如下所示：

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

> [!NOTE]
> 由于我们未在本教程中执行任何更新或删除功能，因此你可以禁用 DataList 的视图状态以减少呈现的页面大小。

最初通过浏览器访问此页时，既不提供 `pageIndex` 也不提供 `pageSize` 查询字符串参数。 因此，将使用默认值0和4。 如图8所示，这会生成一个 DataList，其中显示前四个产品。

[![列出了前四项产品](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)

**图 8**：列出了前四个产品（[单击以查看完全大小的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)）

如果没有分页界面，则目前没有用户导航到第二页数据的方法。 我们将在步骤4中创建分页接口。 但现在，只能通过直接在 querystring 中指定分页条件来实现分页。 例如，若要查看第二页，请将浏览器的地址栏中的 URL 更改 `Paging.aspx` 到 `Paging.aspx?pageIndex=2`，然后按 Enter。 这将导致显示第二页数据（参见图9）。

[显示第二页数据 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image19.png)

**图 9**：显示第二页数据（[单击以查看完全大小的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)）

## <a name="step-4-creating-the-paging-interface"></a>步骤4：创建分页接口

可以实现各种不同的分页接口。 GridView、DetailsView 和 FormView 控件提供四个不同的接口来进行选择：

- **接下来，以前**的用户可以一次将一个页面移动到下一个或上一个页面。
- **接下来，"上一页"、"last"、"Last** " 除 "下一步" 和 "上一步" 按钮外，此接口包含用于移动到第一页或最后一页的第一个和
- **数值**列出页面接口中的页码，使用户能够快速跳转至特定页面。
- **数值、第一个、最后一个**除数字页码外，还包含用于移动到第一页或最后一页的按钮。

对于 DataList 和中继器，我们负责确定分页接口并实现它。 这涉及到在页中创建所需的 Web 控件，并在单击特定的分页接口按钮时显示请求的页面。 此外，可能需要禁用某些分页接口控件。 例如，使用 "下一步"、"上一步"、"最后一个" 接口查看第一页数据时，将禁用 "第一个" 和 "上一个" 按钮。

对于本教程，请使用 "下一步"、"上一步"、"最后一个" 接口。 将四个按钮 Web 控件添加到页面，并将其 `ID` 设置为 `FirstPage`、`PrevPage`、`NextPage`和 `LastPage`。 将 `Text` 属性设置为首先 &lt;&lt;，&lt; "上一步"、"下一 &gt;" 和 "最后 &gt;&gt;"。

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample4.aspx)]

接下来，为每个按钮创建一个 `Click` 事件处理程序。 稍后，我们将添加显示请求的页面所需的代码。

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>记住要分页到的记录总数

无论选择哪种分页接口，都需要计算并记住正在分页的记录总数。 总行数（与页面大小一起）决定正在分页的总页数（确定要添加或启用了哪些分页接口控件）。 在接下来的 "上一个"、"第一个" 和 "最后一个" 界面中，将通过两种方式使用页面计数：

- 确定是否正在查看最后一个页面，在这种情况下，"下一步" 和 "最后一个" 按钮会被禁用。
- 如果用户单击最后一个按钮，则需要将其 whisk 到最后一页，其索引小于页计数。

页计数计算为总计行数的上限除以页面大小。 例如，如果我们要分页到79条记录（每页四条记录），则页计数为20（79/4 的上限）。 如果使用的是数字分页接口，则此信息会告诉我们要显示多少个数值页按钮;如果分页接口包含 "下一步" 或 "最后一个" 按钮，则使用页面计数来确定何时禁用下一个或最后一个按钮。

如果分页接口包含 "最后一个" 按钮，则必须在每次回发时记住要分页的记录总数，以便单击最后一个按钮时，可以确定最后一页的索引。 为了便于实现此目的，请在 ASP.NET 页 s 代码隐藏类中创建一个 `TotalRowCount` 属性，该属性将其值保持为查看状态：

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

除了 `TotalRowCount`，请花一分钟时间创建只读页面级属性，以便轻松访问页面索引、页面大小和页面计数：

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample6.vb)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>确定分页的记录总数

从 ObjectDataSource s `Select()` 方法返回的 `PagedDataSource` 对象在*所有*产品记录中都包含在其中，即使 DataList 中只显示了其中的一个子集。 `PagedDataSource` s [`Count` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx)仅返回将在 DataList 中显示的项数;[`DataSourceCount` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx)返回 `PagedDataSource`中项的总数。 因此，需要将 ASP.NET 页 s `TotalRowCount` 属性分配给 `PagedDataSource` s `DataSourceCount` 属性的值。

为此，请为 ObjectDataSource `Selected` 事件创建事件处理程序。 在 `Selected` 事件处理程序中，我们有权访问 ObjectDataSource s `Select()` 方法（在本例中为 `PagedDataSource`）的返回值。

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

## <a name="displaying-the-requested-page-of-data"></a>显示请求的数据页

当用户单击寻呼界面中的某个按钮时，需要显示请求的数据页。 由于分页参数是通过 querystring 指定的，因此要显示请求的数据页，`Response.Redirect(url)` 使用户浏览器使用适当的分页参数重新请求 `Paging.aspx` 页面。 例如，若要显示第二页数据，我们会将用户重定向到 `Paging.aspx?pageIndex=1`。

为此，请创建一个将用户重定向到 `Paging.aspx?pageIndex=sendUserToPageIndex`的 `RedirectUser(sendUserToPageIndex)` 方法。 然后，从四个按钮 `Click` 事件处理程序调用此方法。 在 `FirstPage` `Click` 事件处理程序中，调用 `RedirectUser(0)`，以将其发送到第一页;在 `PrevPage` `Click` 事件处理程序中，使用 `PageIndex - 1` 作为页索引;依此类推。

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample8.vb)]

完成 `Click` 事件处理程序后，可通过单击按钮将 DataList s 记录分页。 请稍等片刻！

## <a name="disabling-paging-interface-controls"></a>禁用分页接口控件

目前，无论正在查看哪个页面，都将启用所有四个按钮。 但是，当显示第一页数据时，我们希望禁用第一个和上一个按钮，并且在显示最后一页时，将显示 "下一步" 和 "最后一个" 按钮。 由 ObjectDataSource s `Select()` 方法返回 `PagedDataSource` 对象具有[`IsFirstPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx)和[`IsLastPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx)的属性，我们可以进行检查以确定是否正在查看第一个或最后一个数据页。

将以下内容添加到 ObjectDataSource s `Selected` 事件处理程序：

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

添加此项后，在查看第一页时，将禁用第一个和最后一个按钮，而 "下一步" 和 "上一个" 按钮将在查看最后一页时禁用。

让我们通过向用户通知他们当前正在查看的页和存在的总页数，来完成分页接口。 将标签 Web 控件添加到页面，并将其 `ID` 属性设置为 `CurrentPageNumber`。 在 ObjectDataSource s 所选事件处理程序中设置其 `Text` 属性，使其包括正在查看的当前页面（`PageIndex + 1`）和总页数（`PageCount`）。

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample10.vb)]

图10显示了首次访问 `Paging.aspx`。 由于 querystring 为空，因此 DataList 默认为显示前四个产品;"第一个" 和 "上一个" 按钮已禁用。 单击 "下一步" 将显示接下来的四条记录（见图11）;现在启用了 "前" 和 "上一个" 按钮。

[显示第一页数据 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image22.png)

**图 10**：显示了数据的第一页（[单击以查看完全大小的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)）

[显示第二页数据 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)

**图 11**：显示第二页数据（[单击以查看完全大小的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)）

> [!NOTE]
> 通过允许用户指定要在每页上查看多少页，可以进一步增强分页接口。 例如，可以添加 DropDownList，其中列出了页面大小选项，如5、10、25、50和 All。 选择页面大小后，用户需要重定向回 `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`。 我将此增强功能实现为读者的练习。

## <a name="using-custom-paging"></a>使用自定义分页

使用低效的默认分页方法通过其数据对 DataList 页面进行分页。 当对大量数据进行分页时，必须使用自定义分页。 虽然实现细节略有不同，但在 DataList 中实现自定义分页的概念与使用默认分页的概念相同。 使用自定义分页时，请使用 `ProductBLL` 类 `GetProductsPaged` 方法（而不是 `GetProductsAsPagedDataSource`）。 如[通过大量数据有效分页](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)教程中所述，必须向 `GetProductsPaged` 传递起始行索引和要返回的最大行数。 可以通过 querystring 来维护这些参数，就像在默认分页中使用的 `pageIndex` 和 `pageSize` 参数。

由于没有使用自定义分页的 `PagedDataSource`，因此必须使用替代技术来确定要分页的记录总数，以及是否显示第一个或最后一个数据页。 `ProductsBLL` 类中的 `TotalNumberOfProducts()` 方法返回正在分页的产品总数。 若要确定是否正在查看第一页数据，请检查起始行索引是否为零，然后查看第一页。 如果起始行索引加上要返回的最大行数大于或等于要分页的记录总数，则查看最后一页。

在下一教程中，我们将更详细地探讨如何实现自定义分页。

## <a name="summary"></a>摘要

尽管 DataList 和 Repeater 都不提供在 GridView、DetailsView 和 FormView 控件中提供的 "开箱即用" 支持，但这种功能可以极少地添加。 实现默认分页的最简单方法是将整个产品集包装在 `PagedDataSource` 中，然后将 `PagedDataSource` 绑定到 DataList 或 Repeater。 在本教程中，我们将 `GetProductsAsPagedDataSource` 方法添加到 `ProductsBLL` 类以返回 `PagedDataSource`。 `ProductsBLL` 类已经包含了自定义分页 `GetProductsPaged` 和 `TotalNumberOfProducts`所需的方法。

除了检索要为自定义分页或默认分页的 `PagedDataSource` 中的所有记录显示的一组确切记录，还需要手动添加分页接口。 在本教程中，我们创建了下一个、上一个、第一个、最后一个具有四个按钮 Web 控件的接口。 此外，还添加了一个显示当前页码和总页数的标签控件。

在下一教程中，我们将了解如何向 DataList 和中继器添加排序支持。 此外，我们还将了解如何创建可以分页和排序的 DataList （使用默认和自定义分页的示例）。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Liz Shulok、Ken Pespisa 和 Bernadette Leigh。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](sorting-data-in-a-datalist-or-repeater-control-cs.md)
> [下一页](sorting-data-in-a-datalist-or-repeater-control-vb.md)
