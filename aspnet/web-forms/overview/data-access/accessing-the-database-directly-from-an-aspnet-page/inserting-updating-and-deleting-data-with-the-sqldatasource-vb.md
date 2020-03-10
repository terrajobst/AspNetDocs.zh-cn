---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: 用 SqlDataSource （VB）插入、更新和删除数据 |Microsoft Docs
author: rick-anderson
description: 在前面的教程中，我们已了解如何允许 ObjectDataSource 控件插入、更新和删除数据。 SqlDataSource 控件支持 t 。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 4f7b282b09769272df8ff3a32aa4c509c8917481
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508334"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>使用 SqlDataSource 插入、更新和删除数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe)或[下载 PDF](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> 在前面的教程中，我们已了解如何允许 ObjectDataSource 控件插入、更新和删除数据。 SqlDataSource 控件支持相同的操作，但方法是不同的，本教程介绍如何将 SqlDataSource 配置为插入、更新和删除数据。

## <a name="introduction"></a>简介

如[插入、更新和删除的概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)中所述，GridView 控件提供内置的更新和删除功能，而 DetailsView 和 FormView 控件包含插入支持以及编辑和删除功能。 可以直接将这些数据修改功能插入数据源控件，无需编写代码行。 概述如何使用 ObjectDataSource 来[插入、更新和删除](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)检查，以方便使用 GridView、DetailsView 和 FormView 控件进行插入、更新和删除。 或者，可以使用 SqlDataSource 来代替 ObjectDataSource。

回忆一下，若要支持插入、更新和删除，需要为 ObjectDataSource 指定对象层方法，以执行插入、更新或删除操作。 对于 SqlDataSource，需要提供要执行 `INSERT`、`UPDATE`和 `DELETE` SQL 语句（或存储过程）。 正如我们在本教程中看到的那样，这些语句可以手动创建，也可以由 SqlDataSource s 配置数据源向导自动生成。

> [!NOTE]
> 由于我们已经讨论了 GridView、DetailsView 和 FormView 控件的插入、编辑和删除功能，因此本教程将重点介绍如何配置 SqlDataSource 控件以支持这些操作。 如果需要在 GridView、DetailsView 和 FormView 范围内实现这些功能，请从[插入、更新和删除的概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)开始，返回到编辑、插入和删除数据教程。

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>步骤1：指定`INSERT`、`UPDATE`和`DELETE`语句

正如我们过去两个教程中所示，若要从 SqlDataSource 控件中检索数据，需要设置两个属性：

1. `ConnectionString`，它指定要将查询发送到的数据库，以及
2. `SelectCommand`，它指定要执行的临时 SQL 语句或存储过程名称以返回结果。

对于带有参数 `SelectCommand` 值，参数值是通过 SqlDataSource s `SelectParameters` 集合指定的，并且可以包含硬编码值、通用参数源值（querystring 字段、会话变量、Web 控制值等），也可以通过编程方式分配。 以编程方式或从数据 Web 控件自动调用 SqlDataSource 控件 `Select()` 方法时，将建立与数据库的连接，参数值将分配给该查询，并且该命令将 shuttled 到数据库。 然后，结果将作为数据集或 DataReader 返回，具体取决于控件的 `DataSourceMode` 属性的值。

除了选择数据，SqlDataSource 控件还可用于通过以相同方式提供 `INSERT`、`UPDATE`和 `DELETE` SQL 语句来插入、更新和删除数据。 只需将 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性分配给要执行的 `INSERT`、`UPDATE`和 `DELETE` SQL 语句。 如果语句包含参数（因为它们最常如此），请将它们包含在 `InsertParameters`、`UpdateParameters`和 `DeleteParameters` 集合中。

指定 `InsertCommand`、`UpdateCommand`或 `DeleteCommand` 值后，相应的数据 Web 控件中的 "启用插入"、"启用编辑" 或 "启用删除" 选项将变为可用。 为了说明这一点，让我们从[SqlDataSource 控件教程的查询数据](querying-data-with-the-sqldatasource-control-vb.md)中创建的 `Querying.aspx` 页面获取示例，并对其进行扩展以包含删除功能。

首先打开 `SqlDataSource` 文件夹中的 "`InsertUpdateDelete.aspx`" 和 "`Querying.aspx`" 页。 从 "`Querying.aspx`" 页上的 "设计器" 中，选择第一个示例中的 SqlDataSource 和 GridView （`ProductsDataSource` 和 `GridView1` 控件）。 选择两个控件后，请在 "编辑" 菜单中选择 "复制" （或只需按 Ctrl + C）。 接下来，请前往 `InsertUpdateDelete.aspx` 的设计器并粘贴到控件中。 将这两个控件移动到 `InsertUpdateDelete.aspx`后，请在浏览器中测试页面。 应该会看到 `Products` 数据库表中所有记录的 `ProductID`、`ProductName`和 `UnitPrice` 列的值。

[列出的所有产品 ![按 ProductID 排序](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**图 1**：列出所有产品，按 `ProductID` 排序（[单击查看全尺寸图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png)）

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>添加 SqlDataSource`DeleteCommand`和`DeleteParameters`属性

此时，我们有一个 SqlDataSource，它只返回 `Products` 表中的所有记录和呈现此数据的 GridView。 我们的目标是扩展此示例，使用户能够通过 GridView 删除产品。 若要实现此目的，需要为 SqlDataSource 控件 `DeleteCommand` 和 `DeleteParameters` 属性指定值，然后将 GridView 配置为支持删除。

可以通过多种方式指定 `DeleteCommand` 和 `DeleteParameters` 属性：

- 通过声明性语法
- 从设计器中的属性窗口
- 从 "配置数据源" 向导中的 "指定自定义 SQL 语句或存储过程" 屏幕
- 通过在 "配置数据源" 向导中的 "从视图中的表中指定列" 屏幕中的 "高级" 按钮，该按钮实际上会自动生成在 `DeleteCommand` 和 `DeleteParameters` 属性中使用的 `DELETE` SQL 语句和参数集合。

我们将检查如何自动在步骤2中创建 `DELETE` 语句。 现在，让我们使用设计器中的属性窗口，但 "配置数据源向导" 或 "声明性语法" 选项也同样适用。

在 `InsertUpdateDelete.aspx`的设计器中，单击 "`ProductsDataSource`" SqlDataSource，然后打开 "属性窗口" （从 "视图" 菜单中选择 "属性窗口"，或只需按 F4）。 选择 DeleteQuery 属性，该属性将显示一组省略号。

![从 "属性" 窗口中选择 DeleteQuery 属性](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**图 2**：从 "属性" 窗口中选择 DeleteQuery 属性

> [!NOTE]
> SqlDataSource 没有 DeleteQuery 属性。 相反，DeleteQuery 是 `DeleteCommand` 和 `DeleteParameters` 属性的组合，仅在通过设计器查看窗口时在属性窗口中列出。 如果在 "源" 视图中查看属性窗口，则会找到 `DeleteCommand` 属性。

单击 DeleteQuery 属性中的省略号，打开 "命令和参数编辑器" 对话框（请参阅图3）。 从此对话框中，您可以指定 `DELETE` SQL 语句并指定参数。 如果需要，请在 "`DELETE` 命令" 文本框中输入以下查询（手动或使用查询生成器）：

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

接下来，单击 "刷新参数" 按钮，将 `@ProductID` 参数添加到下面的参数列表中。

[![在 "属性" 窗口中选择 DeleteQuery 属性](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**图 3**：在 "属性" 窗口中选择 "DeleteQuery" 属性（[单击以查看完全大小的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png)）

不要*提供此*参数的值（将其参数源保持为 "无"）。 将删除支持添加到 GridView 后，GridView 将使用其 "删除" 按钮所在的行的 `DataKeys` 集合的值自动提供此参数值。

> [!NOTE]
> `DELETE` 查询中使用的参数名称*必须*与 GridView、DetailsView 或 FormView 中 `DataKeyNames` 值的名称相同。 也就是说，`DELETE` 语句中的参数是名为 `@ProductID` （而不是 `@ID`）的有意，因为 Products 表中的主键列名称（以及 GridView 中的 DataKeyNames 值）将 `ProductID`。

如果参数名称和 `DataKeyNames` 值不匹配，则 GridView 无法自动为参数分配 `DataKeys` 集合中的值。

在 "命令和参数编辑器" 对话框中输入与删除相关的信息后，单击 "确定"，然后进入源视图以检查生成的声明性标记：

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

请注意，添加了 `DeleteCommand` 属性以及名为 `productID`的 `<DeleteParameters>` 部分和参数对象。

## <a name="configuring-the-gridview-for-deleting"></a>配置要删除的 GridView

添加 `DeleteCommand` 属性后，GridView s 智能标记现在包含 Enable 删除选项。 继续并选中此复选框。 如[插入、更新和删除的概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)中所述，这会导致 GridView 添加其 `ShowDeleteButton` 属性设置为 `True`的 CommandField。 如图4所示，通过浏览器访问页面时，将包含 "删除" 按钮。 通过删除某些产品来测试此页。

[![每个 GridView 行现在包含一个 "删除" 按钮](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**图 4**：每个 GridView 行现在包含一个 "删除" 按钮（[单击以查看完全大小的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png)）

单击 "删除" 按钮时，会发生回发，GridView 会将 "删除" 按钮所在的行的 `DataKeys` 集合值的值分配给 `ProductID` 参数，并调用 SqlDataSource s `Delete()` 方法。 然后，SqlDataSource 控件连接到数据库并执行 `DELETE` 语句。 然后，GridView 重新绑定到 SqlDataSource，返回并显示当前产品集（不再包括刚删除的记录）。

> [!NOTE]
> 由于 GridView 使用其 `DataKeys` 集合来填充 SqlDataSource 参数，因此，在 GridView `DataKeyNames` 属性设置为构成主键的列，并且 SqlDataSource `SelectCommand` 返回这些列时，这一点至关重要。 此外，SqlDataSource s `DeleteCommand` 中的参数名称必须设置为 `@ProductID`，这一点非常重要。 如果未设置 `DataKeyNames` 属性，或者未将参数命名为 `@ProductsID`，则单击 "删除" 按钮将导致回发，但实际上不会删除任何记录。

图5以图形方式描述了这种交互。 有关与插入、更新和删除数据 Web 控件相关的事件链的详细讨论，请参阅[检查与插入、更新和删除教程关联的事件](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)。

![单击 GridView 中的 "删除" 按钮将调用 SqlDataSource s Delete （）方法](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**图 5**：单击 GridView 中的 "删除" 按钮将调用 SqlDataSource `Delete()` 方法

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>步骤2：自动生成`INSERT`、`UPDATE`和`DELETE`语句

在步骤1检查后，可以通过属性窗口或控件的声明性语法指定 `INSERT`、`UPDATE`和 `DELETE` SQL 语句。 但是，这种方法要求手动写出 SQL 语句，这可能是单调的，而且容易出错。 幸运的是，"配置数据源" 向导会提供一个选项，用于在使用 "从视图中的表" 屏幕中指定列时自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句。

让我们浏览这一自动生成选项。 将 DetailsView 添加到 `InsertUpdateDelete.aspx` 中的设计器，并将其 `ID` 属性设置为 "`ManageProducts`"。 接下来，从 DetailsView s 智能标记中，选择创建新的数据源，并创建一个名为 `ManageProductsDataSource`的 SqlDataSource。

[![创建一个名为 ManageProductsDataSource 的新 SqlDataSource](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**图 6**：创建名为 `ManageProductsDataSource` 的新 SqlDataSource （[单击查看完全大小的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png)）

在 "配置数据源" 向导中，选择使用 `NORTHWINDConnectionString` 连接字符串，然后单击 "下一步"。 在 "配置 Select 语句" 屏幕上，保留 "指定表或视图中的列" 单选按钮，并从下拉列表中选择 `Products` 表。 从复选框列表中选择 `ProductID`、`ProductName`、`UnitPrice`和 `Discontinued` 列。

[![使用 Products 表，返回 ProductID、ProductName、单价和废止列](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**图 7**：使用 `Products` 表，返回 "`ProductID`"、"`ProductName`"、"`UnitPrice`" 和 "`Discontinued`" 列（[单击以查看完全大小的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png)）

若要根据所选的表和列自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句，请单击 "高级" 按钮，然后选中 "生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框。

![选中 "生成 INSERT、UPDATE 和 DELETE 语句" 复选框](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**图 8**：选中 "生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框

仅当所选表具有主键并且主键列（或列）包含在返回列的列表中时，"生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框才会可选。 在选中 "生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框后，"使用开放式并发" 复选框将变为可选择，将在生成的 `UPDATE` 和 `DELETE` 语句中增加 `WHERE` 子句以提供乐观并发控制。 现在，将此复选框保留为未选中状态;在下一教程中，我们将通过 SqlDataSource 控件检查乐观并发。

选中 "生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框后，单击 "确定" 以返回到 "配置 Select 语句" 屏幕，然后单击 "下一步"，然后单击 "完成"，完成 "配置数据源" 向导。 完成该向导后，Visual Studio 会将 `ProductID`、`ProductName`和 `UnitPrice` 列的 DetailsView 添加到 DetailsView，并为 `Discontinued` 列添加 CheckBoxField。 在 "DetailsView s" 智能标记中，选中 "启用分页" 选项，以便访问此页的用户可以单步执行产品。 另外，请清除 DetailsView `Width` 和 `Height` 属性。

请注意，智能标记具有 "启用插入"、"启用编辑" 和 "启用删除" 选项。 这是因为，SqlDataSource 包含 `InsertCommand`、`UpdateCommand`和 `DeleteCommand`的值，如下面的声明性语法所示：

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

请注意，SqlDataSource 控件具有的值自动设置为其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性。 `InsertCommand` 和 `UpdateCommand` 属性中引用的列集基于 `SELECT` 语句中的列。 也就是说，不是在 `InsertCommand` 和 `UpdateCommand`中包含*每个*"产品" 列，而是在 `SelectCommand` 中仅指定了这些列（更少 `ProductID`，因为它是一个[`IDENTITY` 列](http://www.sqlteam.com/item.asp?ItemID=102)，因为它是在编辑时不能更改，并且在插入时会自动分配该值。） 此外，对于 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性中的每个参数，`InsertParameters`、`UpdateParameters`和 `DeleteParameters` 集合中都有相应的参数。

若要启用 DetailsView s 数据修改功能，请选中 "启用插入"、"启用编辑" 和 "在其智能标记中启用删除选项"。 这会添加一个 CommandField，其 `ShowInsertButton`、`ShowEditButton`和 `ShowDeleteButton` 属性设置为 `True`。

访问浏览器中的页面，并记下 DetailsView 中包含的编辑、删除和新按钮。 单击 "编辑" 按钮会将 DetailsView 转换为编辑模式，这将显示其 `ReadOnly` 属性设置为 "`False` （默认值）" 作为文本框的每个 BoundField，"CheckBoxField" 显示为复选框。

[![DetailsView s 默认编辑界面](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**图 9**： DetailsView s 默认编辑界面（[单击以查看完全大小的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png)）

同样，您可以删除当前所选的产品或向系统添加新产品。 由于 `InsertCommand` 语句仅适用于 "`ProductName`"、"`UnitPrice`" 和 "`Discontinued`" 列，因此在插入时，其他列都具有 `NULL` 或其默认值。 与 ObjectDataSource 一样，如果 `InsertCommand` 缺少任何不允许使用 `NULL` 的数据库表列，并且没有默认值，则在尝试执行 `INSERT` 语句时会发生 SQL 错误。

> [!NOTE]
> 插入和编辑接口的 DetailsView 缺少任何自定义或验证。 若要添加验证控件或自定义接口，需要将 BoundFields 转换为 Templatefield。 有关详细信息，请参阅向[编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)和[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程。

另外，请记住，在更新和删除时，DetailsView 使用当前产品 `DataKey` 值，此值仅在配置了 `DataKeyNames` 属性时才存在。 如果 "编辑" 或 "删除" 似乎不起作用，请确保设置了 "`DataKeyNames`" 属性。

## <a name="limitations-of-automatically-generating-sql-statements"></a>自动生成 SQL 语句的限制

由于 "生成 `INSERT`"、"`UPDATE`" 和 "`DELETE` 语句" 选项仅在从表中选取列时才可用，因此对于更复杂的查询，您必须编写自己的 `INSERT`、`UPDATE`和 `DELETE` 语句，就像我们在步骤1中所做的一样。 通常，SQL `SELECT` 语句使用 `JOIN` 来返回一个或多个查找表中的数据，以便进行显示（例如，显示产品信息时返回 `Categories` 表的 `CategoryName` 字段）。 同时，我们可能希望允许用户编辑、更新或将数据插入核心表（在本例中为`Products`）。

尽管可以手动输入 `INSERT`、`UPDATE`和 `DELETE` 语句，但请考虑以下保存时间提示。 最初设置 SqlDataSource，以便它仅从 `Products` 表中提取数据。 使用 "配置数据源向导" 指定表或视图屏幕中的列，以便您可以自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句。 然后，在完成向导后，选择从属性窗口配置 SelectQuery （或者，也可以返回到 "配置数据源" 向导，但使用 "指定自定义 SQL 语句或存储过程" 选项）。 然后更新 `SELECT` 语句以包括 `JOIN` 语法。 此方法为自动生成的 SQL 语句提供节省时间的优势，并允许更多自定义的 `SELECT` 语句。

自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句的另一个限制是，`INSERT` 和 `UPDATE` 语句中的列基于 `SELECT` 语句返回的列。 但是，我们可能需要更新或插入更多或更少的字段。 例如，在步骤2的示例中，可能需要让 `UnitPrice` BoundField 为只读。 在这种情况下，它不应出现在 `UpdateCommand`中。 或者，我们可能需要设置一个表字段的值，该字段不会出现在 GridView 中。 例如，在添加新记录时，可能希望将 `QuantityPerUnit` 值设置为 TODO。

如果需要此类自定义项，则需要通过 "属性窗口"、"在向导中指定自定义 SQL 语句或存储过程" 选项或声明性语法来手动进行此类自定义。

> [!NOTE]
> 添加在数据 Web 控件中没有相应字段的参数时，请记住，这些参数值需要以某种方式分配值。 这些值可以是：在 `InsertCommand` 或 `UpdateCommand`中直接硬编码;可以来自一些预定义的源（查询字符串、会话状态、页面上的 Web 控件等）;可以通过编程方式进行分配，如前面的教程中所述。

## <a name="summary"></a>摘要

为了使数据 Web 控件能够利用内置的插入、编辑和删除功能，数据源控件绑定到的数据源控件必须提供此类功能。 对于 SqlDataSource，这意味着必须将 `INSERT`、`UPDATE`和 `DELETE` SQL 语句分配给 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性。 这些属性和相应的参数集合可以手动添加，也可以通过 "配置数据源" 向导自动生成。 在本教程中，我们将介绍这两种方法。

在[实现开放式并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程中，我们使用了与 ObjectDataSource 的开放式并发来进行检查。 SqlDataSource 控件还提供了开放式并发支持。 如步骤2中所述，自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句时，向导提供了 "使用开放式并发" 选项。 如接下来的教程中所示，使用 SqlDataSource 的开放式并发会修改 `UPDATE` 中的 `WHERE` 子句和 `DELETE` 语句，以确保自上次在页面上显示数据以来其他列的值尚未更改。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [下一页](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
