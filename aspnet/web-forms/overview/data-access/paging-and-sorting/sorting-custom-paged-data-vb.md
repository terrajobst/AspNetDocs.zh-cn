---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
title: 排序自定义分页数据（VB） |Microsoft Docs
author: rick-anderson
description: 在上一教程中，我们学习了如何在网页上呈现数据时实现自定义分页。 在本教程中，我们将了解如何扩展前面的 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 4823a186-caaf-4116-a318-c7ff4d955ddc
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 934c7558d907611732ae6f04c553bc9e295c569b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618486"
---
# <a name="sorting-custom-paged-data-vb"></a>排序自定义分页数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_VB.exe)或[下载 PDF](sorting-custom-paged-data-vb/_static/datatutorial26vb1.pdf)

> 在上一教程中，我们学习了如何在网页上呈现数据时实现自定义分页。 在本教程中，我们将介绍如何扩展前面的示例以包含对自定义分页排序的支持。

## <a name="introduction"></a>简介

与默认分页相比，自定义分页可以提高按多种数量级对数据进行分页的性能，并在通过大量数据进行分页时，使自定义分页成为事实上的分页实现选择。 然而，实现自定义分页比实现默认分页更为重要，但在将排序添加到组合时尤其如此。 在本教程中，我们将扩展前面的示例，以支持排序*和*自定义分页。

> [!NOTE]
> 由于本教程基于前面的教程，因此在开始之前，请先从上一教程的网页（`EfficientPaging.aspx`）中复制 `<asp:Content>` 元素中的声明性语法，然后将其粘贴到 `SortParameter.aspx` 页面的 `<asp:Content>` 元素之间。 有关将一个 ASP.NET 页的功能复制到另一页的更详细的讨论，请参阅返回向[编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)教程中的步骤1。

## <a name="step-1-reexamining-the-custom-paging-technique"></a>步骤1： Reexamining 自定义分页技术

若要使自定义分页正常工作，必须实现一些技术，以便在给定起始行索引和最大行参数的情况下有效地获取特定的记录子集。 可以使用几种方法来实现此目标。 在前面的教程中，我们将介绍如何使用 Microsoft SQL Server 2005 s new `ROW_NUMBER()` 排名函数实现此功能。 简而言之，`ROW_NUMBER()` 排名函数为按指定的排序顺序排序的查询返回的每一行分配一个行号。 然后，通过返回编号结果的特定部分来获取相应的记录子集。 下面的查询演示了如何使用此方法在按 `ProductName`按字母顺序对结果进行排序时，返回编号为11到20的产品：

[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample1.sql)]

此方法适用于使用特定的排序顺序（`ProductName` 按字母顺序排序，在本例中为）的分页，但需要修改查询以显示按不同排序表达式排序的结果。 理想情况下，可以重写上面的查询以在 `OVER` 子句中使用参数，如下所示：

[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample2.sql)]

遗憾的是，不允许使用参数化 `ORDER BY` 子句。 相反，我们必须创建接受 `@sortExpression` 输入参数的存储过程，但使用以下解决方法之一：

- 为每个可使用的排序表达式编写硬编码查询;然后，使用 `IF/ELSE` T-sql 语句确定要执行的查询。
- 使用 `CASE` 语句，根据 `@sortExpressio` n 输入参数提供动态 `ORDER BY` 表达式;有关详细信息，请参阅[SQL `CASE` 语句的强大功能](http://www.4guysfromrolla.com/webtech/102704-1.shtml)中用于动态排序查询结果部分。
- 在存储过程中将适当的查询创建为字符串，然后使用[`sp_executesql` 系统存储过程](https://msdn.microsoft.com/library/ms188001.aspx)来执行动态查询。

其中每个解决方法都有一些缺点。 第一个选项与其他两个选项不同，因为它要求你为每个可能的排序表达式创建一个查询。 因此，如果以后决定向 GridView 添加新的可排序字段，则还需要返回并更新存储过程。 第二种方法有一些微妙之处，它会在按非字符串数据库列排序时引入性能问题，并且与第一种方法存在相同的可维护性问题。 如果攻击者能够在所选的输入参数值中执行存储过程，则使用动态 SQL 的第三个选择会引入 SQL 注入式攻击的风险。

尽管这些方法均不完美，但我认为第三个选项是这三个选项中的最佳选择。 通过使用动态 SQL，它提供了其他两个不同的灵活性。 此外，如果攻击者能够在其选择的输入参数中执行存储过程，则只能利用 SQL 注入式攻击。 由于 DAL 使用参数化查询，ADO.NET 将保护通过体系结构发送到数据库的参数，这意味着，仅当攻击者可以直接执行存储过程时，SQL 注入攻击漏洞才存在。

若要实现此功能，请在 Northwind 数据库中创建名为 `GetProductsPagedAndSorted`的新存储过程。 此存储过程应接受三个输入参数： `@sortExpression`（类型为 `nvarchar(100`的输入参数），该参数指定如何对结果进行排序并直接注入 `OVER` 子句中 `ORDER BY` 文本的后面;并且 `@startRowIndex` 和 `@maximumRows`，则在上一教程中检查 `GetProductsPaged` 存储过程中的两个整数输入参数。 使用以下脚本创建 `GetProductsPagedAndSorted` 存储过程：

[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample3.sql)]

存储过程首先确保指定了 `@sortExpression` 参数的值。 如果缺少，结果将按 `ProductID`进行排名。 接下来，将构造动态 SQL 查询。 请注意，此处的动态 SQL 查询与之前用于检索 Products 表中所有行的查询略有不同。 在前面的示例中，我们使用子查询获取了与每个产品关联的类别和供应商的名称。 这一决定是在[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中完成的，而不是使用 `JOIN` s，因为 TableAdapter 无法自动创建此类查询的关联插入、更新和删除方法。 不过，`GetProductsPagedAndSorted` 存储过程必须使用 `JOIN` 来按类别或供应商名称对结果进行排序。

此动态查询是通过串联静态查询部分和 `@sortExpression`、`@startRowIndex`和 `@maximumRows` 参数生成的。 由于 `@startRowIndex` 和 `@maximumRows` 是整数参数，因此必须将它们转换为 nvarchar，以便正确连接。 构造此动态 SQL 查询后，将通过 `sp_executesql`执行该查询。

花点时间为 `@sortExpression`、`@startRowIndex`和 `@maximumRows` 参数的不同值测试此存储过程。 在服务器资源管理器中，右键单击存储过程名称，然后选择 "执行"。 这将打开 "运行存储过程" 对话框，您可以在其中输入输入参数（参见图1）。 若要按类别名称对结果进行排序，请对 `@sortExpression` 参数值使用 "类名称"。若要按供应商的公司名称进行排序，请使用 "公司名称"。 提供参数值之后，单击 "确定"。 结果将显示在 "输出" 窗口中。 图2显示了按 `UnitPrice` 按降序排序时返回11到20的产品时的结果。

![对于存储过程，请尝试为三个输入参数提供不同的值](sorting-custom-paged-data-vb/_static/image1.png)

**图 1**：为存储过程尝试三个输入参数的不同值

[![存储过程的结果将显示在输出窗口](sorting-custom-paged-data-vb/_static/image3.png)](sorting-custom-paged-data-vb/_static/image2.png)

**图 2**：输出窗口中显示存储过程的结果（[单击查看完全大小的图像](sorting-custom-paged-data-vb/_static/image4.png)）

> [!NOTE]
> 按 `OVER` 子句中指定 `ORDER BY` 列对结果进行排序时，SQL Server 必须对结果进行排序。 如果对列有聚集索引或有覆盖索引，则这是一个快速操作，如果有覆盖索引，则这是一个快速操作，否则可能更昂贵。 若要改善足够大的查询的性能，请考虑为排序所依据的列添加非聚集索引。 有关更多详细信息，请参阅[SQL Server 2005 中的排名函数和性能](http://www.sql-server-performance.com/ak_ranking_functions.asp)。

## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>步骤2：扩充数据访问和业务逻辑层

创建 `GetProductsPagedAndSorted` 存储过程后，下一步就是提供通过我们的应用程序体系结构执行该存储过程的方法。 这就需要为 DAL 和 BLL 添加适当的方法。 首先，将方法添加到 DAL。 打开 `Northwind.xsd` 类型化数据集，右键单击 `ProductsTableAdapter`，然后从上下文菜单中选择 "添加查询" 选项。 如前面的教程中所述，我们希望将这一新的 DAL 方法配置为使用现有的存储过程 `GetProductsPagedAndSorted`（在本例中为）。 首先指示你希望新的 TableAdapter 方法使用现有的存储过程。

![选择使用现有存储过程](sorting-custom-paged-data-vb/_static/image5.png)

**图 3**：选择使用现有存储过程

若要指定要使用的存储过程，请从下一个屏幕的下拉列表中选择 `GetProductsPagedAndSorted` 存储过程。

![使用 GetProductsPagedAndSorted 存储过程](sorting-custom-paged-data-vb/_static/image6.png)

**图 4**：使用 GetProductsPagedAndSorted 存储过程

此存储过程将返回一组记录作为其结果，因此，在下一屏幕中，指示返回表格数据。

![指示存储过程返回表格数据](sorting-custom-paged-data-vb/_static/image7.png)

**图 5**：指示存储过程返回表格数据

最后，创建同时使用 Fill 数据表和返回 DataTable 模式的 DAL 方法，分别 `FillPagedAndSorted` 和 `GetProductsPagedAndSorted`命名方法。

![选择方法名称](sorting-custom-paged-data-vb/_static/image8.png)

**图 6**：选择方法名称

至此，我们已扩展 DAL，接下来可以转到 BLL。 打开 `ProductsBLL` 类文件，并添加新方法 `GetProductsPagedAndSorted`。 此方法需要接受三个输入参数 `sortExpression`、`startRowIndex`和 `maximumRows`，只需向下调用 DAL s `GetProductsPagedAndSorted` 方法即可，如下所示：

[!code-vb[Main](sorting-custom-paged-data-vb/samples/sample4.vb)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>步骤3：将 ObjectDataSource 配置为传入 SortExpression 参数

扩充 DAL 和 BLL 以包含利用 `GetProductsPagedAndSorted` 存储过程的方法，剩下的就是在 "`SortParameter.aspx`" 页中配置 ObjectDataSource 来使用新的 BLL 方法，并基于用户请求对结果进行排序的列传入 `SortExpression` 参数。

首先，将 ObjectDataSource `SelectMethod` 从 `GetProductsPaged` 更改为 `GetProductsPagedAndSorted`。 这可以通过配置数据源向导、属性窗口或直接通过声明性语法完成。 接下来，需要为 ObjectDataSource s [`SortParameterName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)提供一个值。 如果设置此属性，则 ObjectDataSource 尝试将 GridView s `SortExpression` 属性传入 `SelectMethod`。 具体而言，ObjectDataSource 查找其名称等于 `SortParameterName` 属性值的输入参数。 由于 BLL `GetProductsPagedAndSorted` 方法具有名为 `sortExpression`的排序表达式输入参数，因此请将 ObjectDataSource s `SortExpression` 属性设置为 sortExpression。

完成这两个更改后，ObjectDataSource 的声明性语法应类似于以下形式：

[!code-aspx[Main](sorting-custom-paged-data-vb/samples/sample5.aspx)]

> [!NOTE]
> 与前面的教程一样，请确保 ObjectDataSource 不在其 SelectParameters 集合*中包含 sortExpression* 、StartRowIndex 或 maximumRows 输入参数。

若要在 GridView 中启用排序，只需选中 "GridView s 智能" 标记中的 "启用排序" 复选框，这将 `AllowSorting` 属性设置为 `true`，并使每个列的标题文本呈现为 LinkButton。 当最终用户单击其中一个标头 LinkButtons 时，会发生回发可以和以下步骤：

1. GridView 会将其[`SortExpression` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)更新为已单击其标题链接的字段的 `SortExpression` 值
2. ObjectDataSource 调用 `GetProductsPagedAndSorted` 方法，并传入 GridView s `SortExpression` 属性作为方法 s `sortExpression` 输入参数的值（以及相应的 `startRowIndex` 和 `maximumRows` 输入参数值）
3. BLL 调用 DAL s `GetProductsPagedAndSorted` 方法
4. DAL 执行 `GetProductsPagedAndSorted` 存储过程，并传入 `@sortExpression` 参数（连同 `@startRowIndex` 和 `@maximumRows` 输入参数值）
5. 存储过程将相应的数据子集返回到 BLL，并将其返回到 ObjectDataSource;然后，将此数据绑定到 GridView，呈现为 HTML，并向下发送给最终用户

图7显示了按 `UnitPrice` 按升序进行排序时的第一页结果。

[![结果按单价排序](sorting-custom-paged-data-vb/_static/image10.png)](sorting-custom-paged-data-vb/_static/image9.png)

**图 7**：按单价对结果进行排序（[单击查看全尺寸图像](sorting-custom-paged-data-vb/_static/image11.png)）

尽管当前实现可以按产品名称、类别名称、每个单位的数量和单价正确地对结果进行排序，但尝试按供应商名称对结果进行排序会导致运行时异常（参见图8）。

![尝试按供应商对结果进行排序会导致以下运行时异常](sorting-custom-paged-data-vb/_static/image12.png)

**图 8**：尝试按供应商对结果进行排序会导致以下运行时异常

发生此异常的原因是，`SupplierName` BoundField 的 GridView `SortExpression` 设置为 `SupplierName`。 但是，实际上会调用 `Suppliers` 表中的供应商名称，`CompanyName` 我们已将此列名称作为 `SupplierName`的别名。 但是，`ROW_NUMBER()` 函数使用的 `OVER` 子句不能使用别名，并且必须使用实际列名。 因此，将 `SupplierName` BoundField s `SortExpression` 从供应商更改为公司名称（参见图9）。 如图10所示，在此更改后，可以按供应商对结果进行排序。

![将 BoundField 的供应商更改为公司名称](sorting-custom-paged-data-vb/_static/image13.png)

**图 9**：将 BoundField 的供应商的 SortExpression 更改为公司名称

[![结果现在可以按供应商排序](sorting-custom-paged-data-vb/_static/image15.png)](sorting-custom-paged-data-vb/_static/image14.png)

**图 10**：现在可以按供应商对结果进行排序（[单击查看全尺寸图像](sorting-custom-paged-data-vb/_static/image16.png)）

## <a name="summary"></a>总结

我们在前面的教程中检查的自定义分页实现需要在设计时指定结果的排序顺序。 简而言之，这意味着我们实现的自定义分页实现无法同时提供排序功能。 在本教程中，我们将通过扩展存储过程来克服了这一限制，使其包含可对结果进行排序的 `@sortExpression` 输入参数。

在 DAL 和 BLL 中创建了此存储过程并创建了新方法后，我们可以通过将 ObjectDataSource 配置为传入 GridView current `SortExpression` 属性到 BLL `SelectMethod`来实现提供排序和自定义分页的 GridView。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Carlos Santos。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](efficiently-paging-through-large-amounts-of-data-vb.md)
> [下一页](creating-a-customized-sorting-user-interface-vb.md)
