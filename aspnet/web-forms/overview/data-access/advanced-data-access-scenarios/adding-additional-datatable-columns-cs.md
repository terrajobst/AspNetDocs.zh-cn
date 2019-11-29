---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
title: 添加其他 DataTable 列（C#） |Microsoft Docs
author: rick-anderson
description: 使用 TableAdapter 向导创建类型化数据集时，相应的 DataTable 包含主数据库查询返回的列。 但存在 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 615f3361-f21f-4338-8bc1-fce8ae071de9
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: a96f254aa54e7077456ac1a9bd6c5e2a17619d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74610857"
---
# <a name="adding-additional-datatable-columns-c"></a>添加其他 DataTable 列 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_CS.zip)或[下载 PDF](adding-additional-datatable-columns-cs/_static/datatutorial70cs1.pdf)

> 使用 TableAdapter 向导创建类型化数据集时，相应的 DataTable 包含主数据库查询返回的列。 但在某些情况下，DataTable 需要包含其他列。 在本教程中，我们将了解在需要其他 DataTable 列时为何建议使用存储过程。

## <a name="introduction"></a>简介

将 TableAdapter 添加到类型化数据集时，相应的 DataTable 架构由 TableAdapter s 主查询确定。 例如，如果主查询返回数据字段*a*、 *b*和*c*，则 DataTable 将具有三个名为*A*、 *b*和*c*的对应列。除了其主查询外，TableAdapter 还可以包含其他查询，这些查询可能会根据某些参数返回数据的一个子集。 例如，除了返回有关所有产品的信息的 `ProductsTableAdapter` s 主查询，它还包含 `GetProductsByCategoryID(categoryID)` 和 `GetProductByProductID(productID)`等方法，这些方法基于提供的参数返回特定产品信息。

如果所有 TableAdapter s 方法返回的数据字段与主查询中指定的数据字段相同或少，则使 DataTable s 架构反映 TableAdapter s 查询的模型可以很好地运行。 如果 TableAdapter 方法需要返回其他数据字段，则应相应地展开 DataTable 架构。 [使用带有详细信息 DataList 教程的主记录的项目符号列表的母版/详细信息](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)，我们向 `CategoriesTableAdapter` 中添加了一个方法，该方法返回在主 `NumberOfProducts`查询中定义的 `CategoryID`、`CategoryName`和 `Description` 数据字段，以及一个报告与每个类别关联的产品数量的附加数据字段。 我们将新列手动添加到 `CategoriesDataTable`，以便从此新方法捕获 `NumberOfProducts` 数据字段值。

如[上传文件](../working-with-binary-files/uploading-files-cs.md)教程中所述，对于使用即席 SQL 语句并具有其数据字段与主查询并不完全匹配的方法的 tableadapter，必须格外小心。 如果重新运行 TableAdapter 配置向导，它将更新所有 TableAdapter 的方法，使其数据字段列表与主查询匹配。 因此，具有自定义列列表的任何方法都将恢复到主查询的列列表中，而不会返回所需的数据。 使用存储过程时不会出现此问题。

在本教程中，我们将介绍如何扩展 DataTable 架构以包括其他列。 由于使用即席 SQL 语句时，TableAdapter 的易受攻击，因此，在本教程中，我们将使用存储过程。 有关将 TableAdapter 配置为使用存储过程的详细信息，请参阅[创建类型化数据集的 tableadapter 的新存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)和[使用类型化数据集 s Tableadapter 教程的现有存储过程](https://data-access/tutorials/using-existing-stored-procedures-for-the-typed-dataset-amp-rsquo-s-tableadapters-cs)。

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>步骤1：将`PriceQuartile`列添加到`ProductsDataTable`

在*为类型化数据集 tableadapter 教程创建新存储过程*中，我们创建了一个名为 `NorthwindWithSprocs`的类型化数据集。 此数据集当前包含两个数据表： `ProductsDataTable` 和 `EmployeesDataTable`。 `ProductsTableAdapter` 具有以下三种方法：

- `GetProducts`-主查询，返回 `Products` 表中的所有记录
- `GetProductsByCategoryID(categoryID)`-返回具有指定*类别 id*的所有产品。
- `GetProductByProductID(productID)`-返回具有指定*productID*的特定产品。

主查询和其他两个方法都返回相同的数据字段集，即 `Products` 表中的所有列。 没有相关子查询或 `JOIN` 从 `Categories` 或 `Suppliers` 表中提取相关数据。 因此，`ProductsDataTable` 的 `Products` 表中的每个字段都有对应的列。

对于本教程，让我们将方法添加到返回所有产品的名为 `GetProductsWithPriceQuartile` 的 `ProductsTableAdapter`。 除了标准产品数据字段，`GetProductsWithPriceQuartile` 还将包括一个 `PriceQuartile` 数据字段，该字段指示产品的价格为四分位。 例如，价格最昂贵25% 的产品将 `PriceQuartile` 值1，而其价格低于底部25% 的产品将具有值4。 但是，在考虑创建返回此信息的存储过程之前，我们首先需要更新 `ProductsDataTable`，以在使用 `GetProductsWithPriceQuartile` 方法时包含一列来保存 `PriceQuartile` 结果。

打开 `NorthwindWithSprocs` 数据集，然后右键单击 `ProductsDataTable`。 选择上下文菜单中的 "添加"，然后选择 "列"。

[![将新列添加到 ProductsDataTable](adding-additional-datatable-columns-cs/_static/image2.png)](adding-additional-datatable-columns-cs/_static/image1.png)

**图 1**：将新列添加到 `ProductsDataTable` （[单击以查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image3.png)）

这会将一个新列添加到 `System.String`类型的名为 Column1 的 DataTable。 需要将此列的名称更新为 PriceQuartile，并将其类型更新为 "`System.Int32`"，因为它将用于保存1到4之间的数字。 在 `ProductsDataTable` 中选择新添加的列，并从属性窗口将 `Name` 属性设置为 PriceQuartile，并将 `DataType` 属性设置为 `System.Int32`。

[![设置新列的 "名称" 和 "数据类型" 属性](adding-additional-datatable-columns-cs/_static/image5.png)](adding-additional-datatable-columns-cs/_static/image4.png)

**图 2**：设置新列 `Name` 和 `DataType` 属性（[单击以查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image6.png)）

如图2所示，还可以设置其他属性，例如，如果列中的值必须是唯一的，则如果该列是自动递增列，是否允许数据库 `NULL` 值等。 将这些值设置为其默认值。

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>步骤2：创建`GetProductsWithPriceQuartile`方法

现在，已将 `ProductsDataTable` 更新为包含 `PriceQuartile` 列，接下来可以创建 `GetProductsWithPriceQuartile` 方法。 首先右键单击 "TableAdapter"，然后从上下文菜单中选择 "添加查询"。 这将打开 "TableAdapter 查询配置向导"，该向导首先提示我们是要使用即席 SQL 语句还是新的或现有的存储过程。 由于我们还没有返回价格分位数据的存储过程，因此允许 TableAdapter 为我们创建此存储过程。 选择 "创建新存储过程" 选项，然后单击 "下一步"。

[![指示 TableAdapter 向导为我们创建存储过程](adding-additional-datatable-columns-cs/_static/image8.png)](adding-additional-datatable-columns-cs/_static/image7.png)

**图 3**：指示 TableAdapter 向导为我们创建存储过程（[单击查看完全大小的映像](adding-additional-datatable-columns-cs/_static/image9.png)）

在接下来的屏幕中，如图4所示，向导会询问要添加哪种类型的查询。 由于 `GetProductsWithPriceQuartile` 方法将返回 `Products` 表中的所有列和记录，请选择 "选择返回行" 选项，然后单击 "下一步"。

[![查询将是返回多个行的 SELECT 语句](adding-additional-datatable-columns-cs/_static/image11.png)](adding-additional-datatable-columns-cs/_static/image10.png)

**图 4**：查询将是返回多个行的 `SELECT` 语句（[单击以查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image12.png)）

接下来，系统会提示输入 `SELECT` 查询。 在向导中输入以下查询：

[!code-sql[Main](adding-additional-datatable-columns-cs/samples/sample1.sql)]

上面的查询使用 SQL Server 2005 s new [`NTILE` 函数](https://msdn.microsoft.com/library/ms175126.aspx)将结果划分为四个组，其中的组由 `UnitPrice` 值以降序排序。

遗憾的是，查询生成器不知道如何分析 `OVER` 关键字，并将在分析上述查询时显示错误。 因此，请在向导的文本框中直接输入以上查询，而不使用查询生成器。

> [!NOTE]
> 有关 NTILE 和 SQL Server 2005 s 其他排名函数的详细信息，请参阅[SQL Server 2005 联机丛书](https://msdn.microsoft.com/library/ms189798.aspx)中的 Microsoft SQL Server 2005 和[排名函数部分](https://msdn.microsoft.com/library/ms189798.aspx)[返回排名结果](http://www.4guysfromrolla.com/webtech/010406-1.shtml)。

输入 `SELECT` 查询并单击 "下一步" 后，向导将要求我们提供要创建的存储过程的名称。 将新的存储过程命名为 `Products_SelectWithPriceQuartile`，然后单击 "下一步"。

[![命名存储过程 Products_SelectWithPriceQuartile](adding-additional-datatable-columns-cs/_static/image14.png)](adding-additional-datatable-columns-cs/_static/image13.png)

**图 5**：将存储过程命名 `Products_SelectWithPriceQuartile` （[单击以查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image15.png)）

最后，系统将提示您命名 TableAdapter 方法。 将 Fill 填充为 DataTable 并返回选中的 DataTable 复选框，并将方法命名 `FillWithPriceQuartile` 和 `GetProductsWithPriceQuartile`。

[![命名 TableAdapter s 方法，然后单击 "完成"](adding-additional-datatable-columns-cs/_static/image17.png)](adding-additional-datatable-columns-cs/_static/image16.png)

**图 6**：命名 TableAdapter s 方法并单击 "完成" （[单击查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image18.png)）

通过指定 `SELECT` 查询以及名为的存储过程和 TableAdapter 方法，单击 "完成" 以完成向导。 此时，你可能会收到一条警告或两条消息，指出不支持 `OVER` 的 SQL 构造或语句。 可以忽略这些警告。

完成向导后，TableAdapter 应包括 `FillWithPriceQuartile` 和 `GetProductsWithPriceQuartile` 方法，数据库应包含名为 `Products_SelectWithPriceQuartile`的存储过程。 请花点时间验证 TableAdapter 确实包含这一新方法，并且该存储过程已正确添加到数据库中。 检查数据库时，如果看不到存储过程，请尝试右键单击 "存储过程" 文件夹，然后选择 "刷新"。

![验证是否已将新方法添加到 TableAdapter](adding-additional-datatable-columns-cs/_static/image19.png)

**图 7**：验证是否已将新方法添加到 TableAdapter

[![确保数据库包含 Products_SelectWithPriceQuartile 存储过程](adding-additional-datatable-columns-cs/_static/image21.png)](adding-additional-datatable-columns-cs/_static/image20.png)

**图 8**：确保数据库包含 `Products_SelectWithPriceQuartile` 存储过程（[单击查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image22.png)）

> [!NOTE]
> 使用存储过程而不是即席 SQL 语句的一个优点是，重新运行 TableAdapter 配置向导不会修改存储过程列列表。 若要验证此情况，请右键单击 TableAdapter，从上下文菜单中选择 "配置" 选项以启动向导，然后单击 "完成" 完成该向导。 接下来，请切换到数据库并查看 `Products_SelectWithPriceQuartile` 存储过程。 请注意，尚未修改其列列表。 如果使用的是即席 SQL 语句，则重新运行 TableAdapter 配置向导会将此查询的列列表恢复为与主查询列列表相匹配，从而从 `GetProductsWithPriceQuartile` 方法所使用的查询中删除 NTILE 语句。

调用数据访问层的 `GetProductsWithPriceQuartile` 方法时，TableAdapter 执行 `Products_SelectWithPriceQuartile` 存储过程，并向每个返回的记录的 `ProductsDataTable` 添加一行。 存储过程返回的数据字段映射到 `ProductsDataTable` 的列。 由于存储过程中返回了 `PriceQuartile` 数据字段，因此它的值将分配给 `ProductsDataTable` s `PriceQuartile` 列。

对于那些查询未返回 `PriceQuartile` 数据字段的 TableAdapter 方法，`PriceQuartile` 列 s 值是由其 `DefaultValue` 属性指定的值。 如图2所示，此值设置为默认值 `DBNull`。 如果希望使用不同的默认值，只需相应地设置 `DefaultValue` 属性即可。 只需确保 `DefaultValue` 值在给定列 s `DataType` （即 `PriceQuartile` 列的 `System.Int32`）时有效。

此时，我们已执行将其他列添加到 DataTable 的必要步骤。 若要验证此附加列是否按预期运行，请创建一个 ASP.NET 页，其中显示每个产品的名称、价格和价格分位。 但在执行此操作之前，我们首先需要更新业务逻辑层，使其包含一个方法，该方法向下调用 DAL s `GetProductsWithPriceQuartile` 方法。 我们将在步骤3中更新 BLL，然后在步骤4中创建 ASP.NET 页。

## <a name="step-3-augmenting-the-business-logic-layer"></a>步骤3：扩充业务逻辑层

在使用表示层中的新 `GetProductsWithPriceQuartile` 方法之前，我们应该首先向 BLL 添加相应的方法。 打开 `ProductsBLLWithSprocs` 类文件，并添加以下代码：

[!code-csharp[Main](adding-additional-datatable-columns-cs/samples/sample2.cs)]

与 `ProductsBLLWithSprocs`中的其他数据检索方法一样，`GetProductsWithPriceQuartile` 方法只调用 DAL s 对应的 `GetProductsWithPriceQuartile` 方法并返回其结果。

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>步骤4：在 ASP.NET 网页中显示价格分位信息

随着 BLL 添加完成，我们已准备好创建 ASP.NET 页，其中显示了每个产品的价格分位数。 打开 `AdvancedDAL` 文件夹中的 "`AddingColumns.aspx`" 页，然后将 GridView 从工具箱拖动到设计器上，并将其 `ID` 属性设置为 "`Products`"。 从 GridView s 智能标记中，将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsBLLWithSprocs` 类 `GetProductsWithPriceQuartile` 方法。 由于这将是只读网格，因此请将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![将 ObjectDataSource 配置为使用 ProductsBLLWithSprocs 类](adding-additional-datatable-columns-cs/_static/image24.png)](adding-additional-datatable-columns-cs/_static/image23.png)

**图 9**：将 ObjectDataSource 配置为使用 `ProductsBLLWithSprocs` 类（[单击以查看完全大小的映像](adding-additional-datatable-columns-cs/_static/image25.png)）

[![从 GetProductsWithPriceQuartile 方法检索产品信息](adding-additional-datatable-columns-cs/_static/image27.png)](adding-additional-datatable-columns-cs/_static/image26.png)

**图 10**：从 `GetProductsWithPriceQuartile` 方法检索产品信息（[单击以查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image28.png)）

完成 "配置数据源" 向导后，Visual Studio 将为方法返回的每个数据字段自动向 GridView 添加 BoundField 或 CheckBoxField。 其中一个数据字段是 `PriceQuartile`，这是我们添加到步骤1中的 `ProductsDataTable` 的列。

编辑 GridView s 字段，删除除 `ProductName`、`UnitPrice`和 `PriceQuartile` BoundFields 以外的所有字段。 将 `UnitPrice` BoundField 配置为将其值设置为货币格式，并分别使用 `UnitPrice` 和 `PriceQuartile` BoundFields 右对齐。 最后，将其余的 BoundFields `HeaderText` 属性分别更新为 "产品"、"价格" 和 "价格"。 另外，请检查 GridView s 智能标记的 "启用排序" 复选框。

进行这些修改后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](adding-additional-datatable-columns-cs/samples/sample3.aspx)]

图11在通过浏览器访问时显示此页。 请注意，最初产品按其价格降序排序，每个产品分配有合适的 `PriceQuartile` 值。 当然，此数据可以按其他条件进行排序，而价格按四位数的列值仍反映了产品对价格的排名（参见图12）。

[![产品按其价格排序](adding-additional-datatable-columns-cs/_static/image30.png)](adding-additional-datatable-columns-cs/_static/image29.png)

**图 11**：产品按其价格排序（[单击查看全尺寸图像](adding-additional-datatable-columns-cs/_static/image31.png)）

[按产品名称对产品进行排序 ![](adding-additional-datatable-columns-cs/_static/image33.png)](adding-additional-datatable-columns-cs/_static/image32.png)

**图 12**：产品按其名称排序（[单击以查看完全大小的图像](adding-additional-datatable-columns-cs/_static/image34.png)）

> [!NOTE]
> 只需编写几行代码，就能增加 GridView，使其基于 `PriceQuartile` 值为产品行着色。 我们可能会将第一个四分中的产品着色为浅绿色，第二个四阶绿色表示黄色，依此类推。 我建议您花点时间来添加此功能。 如果需要有关设置 GridView 格式的刷新器，请参阅[基于数据的自定义格式设置](../custom-formatting/custom-formatting-based-upon-data-cs.md)教程。

## <a name="an-alternative-approach---creating-another-tableadapter"></a>另一种方法-创建其他 TableAdapter

正如我们在本教程中看到的，在将方法添加到返回除主查询所述的数据字段以外的其他数据字段时，可以将相应的列添加到 DataTable。 但是，这种方法只有在 TableAdapter 中有少量方法返回不同的数据字段，并且这些备用数据字段不会在主查询中发生太大变化时，此方法才有效。

您可以改为将其他 TableAdapter 添加到包含返回不同数据字段的第一个 TableAdapter 中的方法的数据集，而不是将列添加到 DataTable。 对于本教程，请不要将 `PriceQuartile` 列添加到 `ProductsDataTable` （其中它仅由 `GetProductsWithPriceQuartile` 方法使用），我们可以将其他 TableAdapter 添加到使用 `Products_SelectWithPriceQuartile` 存储过程作为其主要查询的数据集 `ProductsWithPriceQuartileTableAdapter`。 以 ASP.NET 的价格来获取产品信息所需的页面将使用 `ProductsWithPriceQuartileTableAdapter`，而不能继续使用 `ProductsTableAdapter`。

通过添加新的 TableAdapter，数据表保持 untarnished，并且其列精确镜像由 TableAdapter s 方法返回的数据字段。 但是，其他 Tableadapter 可能会引入重复的任务和功能。 例如，如果那些显示 `PriceQuartile` 列的 ASP.NET 页面还需要提供插入、更新和删除支持，则 `ProductsWithPriceQuartileTableAdapter` 需要正确配置其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性。 尽管这些属性会镜像 `ProductsTableAdapter`，但此配置会引入额外的步骤。 此外，现在有两种方法可用于更新、删除或向数据库添加产品-通过 `ProductsTableAdapter` 和 `ProductsWithPriceQuartileTableAdapter` 类。

本教程的下载内容包括 `NorthwindWithSprocs` 数据集中的 `ProductsWithPriceQuartileTableAdapter` 类，其中阐释了此替代方法。

## <a name="summary"></a>总结

在大多数情况下，TableAdapter 中的所有方法都将返回相同的一组数据字段，但在某些时候，特定的方法或两个可能需要返回一个附加字段。 例如，在[主/详细信息中，使用带有详细信息 DataList 教程的主记录的项目符号列表](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)，我们向 `CategoriesTableAdapter` 添加了一种方法，除了主查询的数据字段外，还返回了报告与每个类别关联的产品数量的 `NumberOfProducts` 字段。 在本教程中，我们将介绍如何在 `ProductsTableAdapter` 中添加一个方法，该方法将返回 "`PriceQuartile`" 字段以及主查询数据字段。 若要捕获由 TableAdapter s 方法返回的其他数据字段，需要将相应的列添加到 DataTable。

如果你计划手动将列添加到 DataTable，则建议 TableAdapter 使用存储过程。 如果 TableAdapter 使用即席 SQL 语句，则每当 TableAdapter 配置向导运行时，数据字段列表中的所有方法都将恢复为主查询返回的数据字段。 此问题不会扩展到存储过程，这就是我们建议并在本教程中使用的原因。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Randy Schmidt、Jacky Goor、Bernadette Leigh 和 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](updating-the-tableadapter-to-use-joins-cs.md)
> [下一页](working-with-computed-columns-cs.md)
