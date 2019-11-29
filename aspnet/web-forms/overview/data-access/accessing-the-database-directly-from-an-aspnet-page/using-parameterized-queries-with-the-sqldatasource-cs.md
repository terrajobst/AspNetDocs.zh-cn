---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
title: 使用带有 SqlDataSource （C#）的参数化查询 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将继续探讨 SqlDataSource 控件并了解如何定义参数化查询。 参数可同时指定声明 。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9128aaac-afe2-449f-84b2-bb1d035083c4
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 241dc8c089d4faa9eb95a63684e8a56756bb302c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611296"
---
# <a name="using-parameterized-queries-with-the-sqldatasource-c"></a>通过 SqlDataSource 使用参数化查询 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_CS.exe)或[下载 PDF](using-parameterized-queries-with-the-sqldatasource-cs/_static/datatutorial48cs1.pdf)

> 在本教程中，我们将继续探讨 SqlDataSource 控件并了解如何定义参数化查询。 可以通过声明方式和编程方式指定参数，并且可以从多个位置（例如查询字符串、会话状态、其他控件等）中提取参数。

## <a name="introduction"></a>简介

在上一教程中，我们介绍了如何使用 SqlDataSource 控件直接从数据库中检索数据。 使用 "配置数据源向导"，我们可以选择数据库，然后选择：从表或视图中选择要返回的列;输入自定义 SQL 语句;或使用存储过程。 无论是从表中选择列，还是要输入自定义 SQL 语句，都将向 SqlDataSource 控件 `SelectCommand` 属性分配生成的即席 SQL `SELECT` 语句，这是在调用 SqlDataSource s `Select()` 方法（以编程方式或从数据 Web 控件自动进行）时执行的此 `SELECT` 语句。

前面的教程演示中使用的 SQL `SELECT` 语句缺少 `WHERE` 子句。 在 `SELECT` 语句中，`WHERE` 子句可用于限制返回的结果。 例如，若要显示成本超过 $50.00 的产品的名称，可以使用以下查询：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample1.sql)]

通常，在 `WHERE` 子句中使用的值由某些外部源（例如查询字符串值、会话变量或页面上 Web 控件的用户输入）确定。 理想情况下，通过使用*参数*指定此类输入。 使用 Microsoft SQL Server，使用 `@parameterName`表示参数，如下所示：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample2.sql)]

SqlDataSource 支持 `SELECT` 语句和 `INSERT`、`UPDATE`和 `DELETE` 语句的参数化查询。 而且，参数值可以从多个源自动提取，这些源是查询字符串、会话状态、页面上的控件等，也可以通过编程方式进行分配。 在本教程中，我们将了解如何定义参数化查询，以及如何以声明方式和编程方式指定参数值。

> [!NOTE]
> 在上一教程中，我们比较了在第一个46教程中通过 SqlDataSource 进行选择的 ObjectDataSource，指出了它们的概念性相似性。 这些相似性还扩展到参数。 已映射到业务逻辑层中方法的输入参数的 ObjectDataSource 参数。 对于 SqlDataSource，参数直接在 SQL 查询中定义。 这两个控件都具有用于其 `Select()`、`Insert()`、`Update()`和 `Delete()` 方法的参数集合，并且两者都可以使用从预定义源（查询字符串值、会话变量等）填充的参数值，也可以通过编程方式进行分配。

## <a name="creating-a-parameterized-query"></a>创建参数化查询

SqlDataSource 控件的 "配置数据源" 向导提供三个用于定义要执行以检索数据库记录的命令的途径：

- 通过从现有的表或视图中选取列，
- 通过输入自定义 SQL 语句或
- 通过选择存储过程

从现有表或视图中选取列时，必须通过 "添加 `WHERE` 子句" 对话框指定 `WHERE` 子句的参数。 但是，在创建自定义 SQL 语句时，可以将参数直接输入 `WHERE` 子句中（使用 `@parameterName` 来表示每个参数）。 [存储过程](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)包含一个或多个 SQL 语句，这些语句可以参数化。 但是，在 SQL 语句中使用的参数必须作为输入参数传递到存储过程。

由于创建参数化查询取决于 SqlDataSource s `SelectCommand` 的指定方式，因此让我们看一下所有这三种方法。 若要开始，请打开 `SqlDataSource` 文件夹中的 "`ParameterizedQueries.aspx`" 页，将 SqlDataSource 控件从工具箱拖到设计器上，并将其 `ID` 设置为 "`Products25BucksAndUnderDataSource`"。 接下来，单击控件 s 智能标记中的 "配置数据源" 链接。 选择要使用的数据库（`NORTHWINDConnectionString`），然后单击 "下一步"。

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>步骤1：从表或视图中选取列时添加`WHERE`子句

使用 SqlDataSource 控件从数据库中选择要返回的数据时，可以使用 "配置数据源" 向导，只需选取要从现有表或视图返回的列（参见图1）。 这样做会自动生成 SQL `SELECT` 语句，这是在调用 SqlDataSource s `Select()` 方法时发送到数据库的内容。 如前面的教程中所述，从下拉列表中选择 Products 表，并选中 `ProductID`、`ProductName`和 `UnitPrice` 列。

[![选择要从表或视图中返回的列](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.png)

**图 1**：选择要从表或视图返回的列（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.png)）

若要在 `SELECT` 语句中包含 `WHERE` 子句，请单击 "`WHERE`" 按钮，此时将显示 "添加 `WHERE` 子句" 对话框（参见图2）。 若要添加参数以限制 `SELECT` 查询返回的结果，请首先选择要按其筛选数据的列。 接下来，选择要用于筛选的运算符（=、&lt;、&lt;=、&gt;，等等）。 最后，选择参数 s 值的源，例如从查询字符串或会话状态。 配置参数后，单击 "添加" 按钮，将其包含在 `SELECT` 查询中。

在此示例中，只返回 `UnitPrice` 值小于或等于 $25.00 的结果。 因此，从 "列" 下拉列表中选择 "`UnitPrice`"，然后从 "运算符" 下拉列表中选择 "&lt;="。 使用硬编码的参数值（例如 $25.00）时，或者如果要以编程方式指定参数值，请在 "源" 下拉列表中选择 "无"。 接下来，在 "值" 25.00 文本框中输入硬编码的参数值，然后单击 "添加" 按钮完成该过程。

[![限制从 "添加 WHERE 子句" 对话框返回的结果](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.png)

**图 2**：限制 "添加 `WHERE` 子句" 对话框返回的结果（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.png)）

添加参数后，单击 "确定" 以返回到 "配置数据源" 向导。 向导底部的 `SELECT` 语句现在应包含一个名为 "`@UnitPrice`" 的参数 `WHERE` 子句：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample3.sql)]

> [!NOTE]
> 如果在 "添加 `WHERE` 子句" 对话框的 `WHERE` 子句中指定多个条件，则向导会将其与 `AND` 运算符联接在一起。 如果需要在 `WHERE` 子句中包含 `OR` （例如 `WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`），则必须通过自定义 SQL 语句屏幕生成 `SELECT` 语句。

完成配置 SqlDataSource （单击 "下一步"，然后单击 "完成"），然后检查 SqlDataSource 的声明性标记。 标记现在包含一个 `<SelectParameters>` 集合，该集合在 `SelectCommand`中拼写出参数的源。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample4.aspx)]

调用 SqlDataSource s `Select()` 方法时，`UnitPrice` 参数值（25.00）将应用于 `SelectCommand` 中的 `@UnitPrice` 参数，然后再将其发送到数据库。 最终结果是，仅从 `Products` 表返回小于或等于 $25.00 的产品。 若要确认这一点，请向页面添加 GridView，将其绑定到此数据源，然后通过浏览器查看页面。 只应看到列出的小于或等于 $25.00 的产品，如图3确认。

[仅显示小于或等于 $25.00 的产品 ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.png)

**图 3**：仅显示小于或等于 $25.00 的产品（[单击以查看完全尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.png)）

## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>步骤2：向自定义 SQL 语句添加参数

添加自定义 SQL 语句时，您可以显式输入 `WHERE` 子句，也可以在查询生成器的筛选单元中指定一个值。 为了说明这一点，让我们在一个 GridView 中只显示那些价格小于特定阈值的产品。 首先将文本框添加到 `ParameterizedQueries.aspx` "页，以便从用户那里收集此阈值。 将 TextBox `ID` 属性设置为 `MaxPrice`。 添加一个按钮 Web 控件，并将其 `Text` 属性设置为显示匹配的产品。

接下来，将一个 GridView 拖到页面上，并从其智能标记中选择创建一个名为 `ProductsFilteredByPriceDataSource`的新 SqlDataSource。 从 "配置数据源" 向导中，转到 "指定自定义 SQL 语句或存储过程" 屏幕（参见图4），然后输入以下查询：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample5.sql)]

输入查询（手动或通过查询生成器）后，单击 "下一步"。

[![仅返回小于或等于参数值的产品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.png)

**图 4**：仅返回小于或等于参数值的产品（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.png)）

由于查询包含参数，向导中的下一个屏幕会提示我们输入参数值的源。 从 "参数源" 下拉列表中选择 "控制"，然后从 "ControlID" 下拉列表中 `MaxPrice` （TextBox 控件 s `ID` 值）。 如果用户未在 "`MaxPrice`" 文本框中输入任何文本，则还可以输入可选的默认值。 对于这种情况，请不要输入默认值。

[![MaxPrice TextBox s Text 属性用作参数源](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.png)

**图 5**： `MaxPrice` TextBox s `Text` 属性用作参数源（[单击查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.png)）

单击 "下一步"，然后单击 "完成"，完成 "配置数据源" 向导。 GridView、TextBox、Button 和 SqlDataSource 的声明性标记如下所示：

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample6.aspx)]

请注意，SqlDataSource s `<SelectParameters>` 部分中的参数是一个 `ControlParameter`，其中包括 `ControlID` 和 `PropertyName`等其他属性。 调用 SqlDataSource s `Select()` 方法时，`ControlParameter` 从指定的 Web 控件属性获取值，并将其分配给 `SelectCommand`中的相应参数。 在此示例中，`MaxPrice` s Text 属性用作 `@MaxPrice` 参数值。

花点时间查看浏览器中的此页。 首次访问该页面时，或每次 `MaxPrice` TextBox 缺少值时，GridView 中将不会显示任何记录。

[![MaxPrice 文本框为空时不显示任何记录](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.png)

**图 6**： `MaxPrice` TextBox 为空时未显示任何记录（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.png)）

因为默认情况下，不显示任何产品的原因是，参数值的空字符串转换为数据库 `NULL` 值。 由于 `[UnitPrice] <= NULL` 的比较始终计算为 False，因此不返回任何结果。

在文本框中输入一个值（例如5.00），然后单击 "显示匹配的产品" 按钮。 在回发时，SqlDataSource 会通知 GridView 其中一个参数源已发生更改。 因此，GridView 会重新绑定到 SqlDataSource，并显示小于或等于 $5.00 的那些产品。

[显示小于或等于 $5.00 的 ![产品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.png)

**图 7**：显示小于或等于 $5.00 的产品（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.png)）

## <a name="initially-displaying-all-products"></a>最初显示所有产品

我们可能想要显示*所有*产品，而不是在第一次加载页面时不显示任何产品。 每当 "`MaxPrice`" 文本框为空时，列出所有产品的一种方法是将参数的默认值设置为一些前所未有高值（例如1000000），因为 Northwind 商贸不太可能会有其单位价格超过 $1000000 的库存。 但是，这种方法是狭隘的，在其他情况下可能不起作用。

在以前的教程中，使用 DropDownList 的[声明性参数](../basic-reporting/declarative-parameters-cs.md)和[主/详细信息筛选](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)会遇到类似的问题。 我们的解决方案是将此逻辑放在业务逻辑层中。 具体而言，BLL 检查了传入值，如果 `NULL` 或某个保留值，则将调用路由到返回所有记录的 DAL 方法。 如果传入值是普通筛选值，则调用 DAL 方法，该方法执行了使用具有所提供值的参数化 `WHERE` 子句的 SQL 语句。

遗憾的是，在使用 SqlDataSource 时，我们绕过了此体系结构。 相反，我们需要自定义 SQL 语句，以便在 `@MaximumPrice` 参数 `NULL` 或某个保留值时智能地获取所有记录。 在此练习中，让我们将其设置为：如果 `@MaximumPrice` 参数等于 `-1.0`，则将返回*所有*记录（`-1.0` 将作为保留值工作，因为没有任何产品都有负值 `UnitPrice` 值）。 为实现此目的，我们可以使用以下 SQL 语句：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample7.sql)]

如果 `@MaximumPrice` 参数等于 `-1.0`，则此 `WHERE` 子句将返回*所有*记录。 如果未 `-1.0`参数值，则仅返回其 `UnitPrice` 小于或等于 `@MaximumPrice` 参数值的那些产品。 通过将 `@MaximumPrice` 参数的默认值设置为 `-1.0`，在第一页加载时（或每次 `MaxPrice` TextBox 为空时），`@MaximumPrice` 的值为 `-1.0` 并且将显示所有产品。

[现在 ![在 MaxPrice 文本框为空时显示所有产品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.png)

**图 8**：当 "`MaxPrice`" 文本框为空时显示所有产品（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image16.png)）

对于此方法，需要注意几个注意事项。 首先，请注意，参数的数据类型是由它在 SQL 查询中的使用情况推断出来的。 如果将 `WHERE` 子句从 `@MaximumPrice = -1.0` 改为 `@MaximumPrice = -1`，则运行时将参数视为整数。 如果你随后尝试将 `MaxPrice` TextBox 赋给小数值（如5.00），则会发生错误，因为它无法将5.00 转换为整数。 若要解决此情况，请确保在 `WHERE` 子句中使用 `@MaximumPrice = -1.0` 或者，更好的做法是将 `ControlParameter` 对象的 `Type` 属性设置为 Decimal。

其次，通过将 `OR @MaximumPrice = -1.0` 添加到 `WHERE` 子句，查询引擎无法对 `UnitPrice` （假设存在）使用索引，从而导致表扫描。 如果 `Products` 表中有足够数量的记录，这可能会影响性能。 更好的方法是将此逻辑移到一个存储过程中，当需要返回所有记录时，`IF` 语句将从 `Products` `WHERE` 表执行 `SELECT` 查询，或者将所有记录都包含 `WHERE` 条件，这样就可以使用索引。

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>步骤3：创建和使用参数化存储过程

存储过程可以包含一组输入参数，这些参数可以在存储过程中定义的 SQL 语句中使用。 将 SqlDataSource 配置为使用接受输入参数的存储过程时，可以使用与即席 SQL 语句相同的技术来指定这些参数值。

为了说明如何在 SqlDataSource 中使用存储过程，让我们在 Northwind 数据库中创建一个名为 `GetProductsByCategory`的新存储过程，该存储过程接受名为 `@CategoryID` 的参数，并返回其 `CategoryID` 列与 `@CategoryID`匹配的所有产品的列。 若要创建存储过程，请访问服务器资源管理器并向下钻取到 `NORTHWND.MDF` 数据库。 （如果看不到服务器资源管理器，请转到 "视图" 菜单并选择 "服务器资源管理器" 选项将其打开。）

在 `NORTHWND.MDF` 数据库中，右键单击 "存储过程" 文件夹，选择 "添加新存储过程"，然后输入以下语法：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample8.sql)]

单击 "保存" 图标（或按 Ctrl + S）保存存储过程。 您可以通过右键单击 "存储过程" 文件夹中的存储过程，然后选择 "执行" 来对其进行测试。 这会提示你输入存储过程的参数（在此实例中为`@CategoryID`），之后结果将显示在 "输出" 窗口中。

[使用 @CategoryID 1 执行时，![GetProductsByCategory 存储过程](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image17.png)

**图 9**：使用 1 `@CategoryID` 执行时的 `GetProductsByCategory` 存储过程（[单击查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image18.png)）

让我们使用此存储过程显示 GridView 中饮料类别的所有产品。 向页面添加一个新的 GridView，并将其绑定到名为 `BeverageProductsDataSource`的新 SqlDataSource。 继续执行 "指定自定义 SQL 语句或存储过程" 屏幕，选择 "存储过程" 单选按钮，然后从下拉列表中选择 `GetProductsByCategory` 存储过程。

[![从下拉列表中选择 GetProductsByCategory 存储过程](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image19.png)

**图 10**：从下拉列表中选择 `GetProductsByCategory` 存储过程（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image20.png)）

由于存储过程接受输入参数（`@CategoryID`），因此单击 "下一步" 会提示我们指定此参数 s 值的源。 饮料 `CategoryID` 为1，因此将 "参数源" 下拉列表保留为 "无"，并在 "DefaultValue" 文本框中输入1。

[![使用硬编码值1返回 "饮料" 类别中的产品](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image21.png)

**图 11**：使用硬编码值1返回 "饮料" 类别中的产品（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image22.png)）

正如以下声明性标记所示，在使用存储过程时，SqlDataSource s `SelectCommand` 属性设置为存储过程的名称，并且[`SelectCommandType` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx)设置为 `StoredProcedure`，这表示 `SelectCommand` 是存储过程的名称，而不是即席的 SQL 语句。

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample9.aspx)]

在浏览器中测试页面。 只有属于 "饮料" 类别的产品才会显示，但*所有*产品字段都是因为 `GetProductsByCategory` 存储过程返回 `Products` 表中的所有列。 当然，我们可以限制或自定义 gridview "编辑列" 对话框中显示的字段。

[显示所有饮料 ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image23.png)

**图 12**：显示所有饮料（[单击以查看完全尺寸的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image24.png)）

## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>步骤4：以编程方式调用 SqlDataSource s`Select()`语句

在上一个教程和本教程中，我们已了解到的示例将 SqlDataSource 控件直接绑定到 GridView。 但是，可以在代码中以编程方式访问和枚举 SqlDataSource 控件的数据。 当您需要查询数据以对其进行检查，但不需要显示时，这可能特别有用。 无需编写所有样板 ADO.NET 代码即可连接到数据库、指定命令和检索结果，你可以让 SqlDataSource 处理此单调代码。

若要演示如何以编程方式使用 SqlDataSource 的数据，请假设老板已经请求创建一个网页，该网页显示随机选择的类别的名称及其关联的产品。 也就是说，当用户访问此页面时，需要从 `Categories` 表中随机选择一个类别，显示类别名称，然后列出属于该类别的产品。

为实现此目的，我们需要两个 SqlDataSource 控件，一个用于从 `Categories` 表中获取随机类别，另一个用于获取类别的产品。 在此步骤中，我们将构建检索随机类别记录的 SqlDataSource;步骤5介绍了如何在 SqlDataSource 中提取类别的产品。

首先将 SqlDataSource 添加到 `ParameterizedQueries.aspx`，并将其 `ID` 设置为 "`RandomCategoryDataSource`"。 将其配置为使用以下 SQL 查询：

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample10.sql)]

`ORDER BY NEWID()` 返回按随机顺序排序的记录（请参阅[使用 `NEWID()` 对记录进行随机排序](http://www.sqlteam.com/item.asp?ItemID=8747)）。 `SELECT TOP 1` 返回结果集中的第一条记录。 放在一起，此查询将返回单个随机选定类别中的 `CategoryID` 和 `CategoryName` 列值。

若要显示类别 `CategoryName` 值，请将 "标签" Web 控件添加到页面，将其 `ID` 属性设置为 "`CategoryNameLabel`"，然后清除其 `Text` 属性。 若要以编程方式检索 SqlDataSource 控件中的数据，需要调用其 `Select()` 方法。 [`Select()` 方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx)需要[`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)类型的单个输入参数，该参数指定如何消息数据，然后再返回数据。 这可以包含对数据进行排序和筛选的说明，并由数据 Web 控件在 SqlDataSource 控件中对数据进行排序或分页时使用。 但对于我们的示例，我们不需要在返回数据之前对其进行修改，因而会传入 `DataSourceSelectArguments.Empty` 对象。

`Select()` 方法返回实现 `IEnumerable`的对象。 返回的确切类型取决于 SqlDataSource 控件[`DataSourceMode` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)的值。 如前面的教程中所述，可以将此属性的值设置为 `DataSet` 或 `DataReader`。 如果设置为 `DataSet`，则 `Select()` 方法返回[DataView](https://msdn.microsoft.com/library/01s96x0z.aspx)对象;如果设置为 `DataReader`，它将返回实现[`IDataReader`](https://msdn.microsoft.com/library/system.data.idatareader.aspx)的对象。 由于 `RandomCategoryDataSource` SqlDataSource 的 `DataSourceMode` 属性设置为 `DataSet` （默认值），因此我们将使用 DataView 对象。

下面的代码演示了如何从 `RandomCategoryDataSource` SqlDataSource 中检索记录作为 DataView，以及如何从第一个 DataView 行读取 `CategoryName` 列值：

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample11.cs)]

`randomCategoryView[0]` 返回 DataView 中的第一个 `DataRowView`。 `randomCategoryView[0]["CategoryName"]` 返回此第一行中 `CategoryName` 列的值。 请注意，DataView 的类型为宽松类型。 若要引用特定列值，需要以字符串形式（在本例中为 "类别名称"）作为字符串传递。 图13显示了查看页面时 `CategoryNameLabel` 中显示的消息。 当然，在每次访问页面（包括回发）的情况下，`RandomCategoryDataSource` SqlDataSource 会随机选择显示的实际类别名称。

[![显示随机选择的类别名称](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image25.png)

**图 13**：将显示随机选择的类别名称（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image26.png)）

> [!NOTE]
> 如果 SqlDataSource 控件 `DataSourceMode` 属性设置为 `DataReader`，则 `Select()` 方法的返回值将需要强制转换为 `IDataReader`。 若要从第一行读取 `CategoryName` 的列值，请使用如下所示的代码：

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample12.cs)]

当 SqlDataSource 随机选择一个类别时，我们就可以添加列出了类别产品的 GridView 了。

> [!NOTE]
> 我们可以将 FormView 或 DetailsView 添加到页面，并将其绑定到 SqlDataSource，而不是使用标签 Web 控件来显示类别的名称。 然而，使用标签，我们可以探索如何以编程方式调用 SqlDataSource 的 `Select()` 语句，并使用其在代码中生成的数据。

## <a name="step-5-assigning-parameter-values-programmatically"></a>步骤5：以编程方式分配参数值

在本教程中，我们在本教程中看到的所有示例都使用了硬编码的参数值，或者从一个预定义参数源（查询字符串值、页上的 Web 控件等）获取了一个参数值。 但是，也可以通过编程方式设置 SqlDataSource 控制的参数。 若要完成我们的当前示例，需要一个 SqlDataSource，返回属于指定类别的所有产品。 此 SqlDataSource 将具有一个 `CategoryID` 参数，其值需要根据 `Page_Load` 事件处理程序中 `RandomCategoryDataSource` SqlDataSource 返回的 `CategoryID` 列值进行设置。

首先向页面添加 GridView，然后将其绑定到名为 `ProductsByCategoryDataSource`的新 SqlDataSource。 与在第3步中所做的一样，将 SqlDataSource 配置为调用 `GetProductsByCategory` 存储过程。 将 "参数源" 下拉列表设置为 "无"，但不要输入默认值，因为我们将以编程方式设置此默认值。

[![不指定参数源或默认值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image27.png)

**图 14**：不指定参数源或默认值（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image28.png)）

完成 SqlDataSource 向导后，生成的声明性标记应如下所示：

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample13.aspx)]

可以在 `Page_Load` 事件处理程序中以编程方式分配 `CategoryID` 参数的 `DefaultValue`：

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample14.cs)]

通过此添加，页面包含一个 GridView，其中显示与随机选择的类别关联的产品。

[![不指定参数源或默认值](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image29.png)

**图 15**：不指定参数源或默认值（[单击以查看完全大小的图像](using-parameterized-queries-with-the-sqldatasource-cs/_static/image30.png)）

## <a name="summary"></a>总结

SqlDataSource 使页面开发人员能够定义参数值可以进行硬编码、从预定义参数源提取或以编程方式分配的参数化查询。 在本教程中，我们介绍了如何为即席 SQL 查询和存储过程从 "配置数据源" 向导中创建参数化查询。 还介绍了如何使用硬编码的参数源，将 Web 控件作为参数源，并以编程方式指定参数值。

与 ObjectDataSource 一样，SqlDataSource 还提供了修改其基础数据的功能。 在下一教程中，我们将介绍如何通过 SqlDataSource 定义 `INSERT`、`UPDATE`和 `DELETE` 语句。 添加这些语句后，便可以利用内置的插入、编辑和删除 GridView、DetailsView 和 FormView 控件固有的功能了。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者为 Scott Clyde、Randell Schmidt 和 Ken Pespisa。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](querying-data-with-the-sqldatasource-control-cs.md)
> [下一页](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
