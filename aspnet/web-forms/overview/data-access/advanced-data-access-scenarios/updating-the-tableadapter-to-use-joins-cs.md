---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
title: 更新 TableAdapter 以使用 Join （C#） |Microsoft Docs
author: rick-anderson
description: 使用数据库时，通常会请求分散在多个表中的数据。 若要从两个不同的表中检索数据，可以使用 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 675531a7-cb54-4dd6-89ac-2636e4c285a5
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
msc.type: authoredcontent
ms.openlocfilehash: 24ff3645783dabfcdef5ac313a2d4833e4998efc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78427772"
---
# <a name="updating-the-tableadapter-to-use-joins-c"></a>更新 TableAdapter 以使用 JOIN (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_CS.zip)或[下载 PDF](updating-the-tableadapter-to-use-joins-cs/_static/datatutorial69cs1.pdf)

> 使用数据库时，通常会请求分散在多个表中的数据。 若要从两个不同的表中检索数据，可以使用相关子查询或联接运算。 在本教程中，我们将比较相关子查询和联接语法，然后查看如何创建在其主查询中包含联接的 TableAdapter。

## <a name="introduction"></a>简介

使用关系数据库时，我们感兴趣的数据通常分布在多个表中。 例如，在显示产品信息时，我们可能希望列出每个产品对应的类别和供应商的名称。 `Products` 表具有 `CategoryID` 和 `SupplierID` 值，但实际类别和供应商名称分别位于 `Categories` 表和 `Suppliers` 表中。

若要从另一个相关表中检索信息，可以使用*相关子查询*或 *`JOIN`。* 相关子查询是一个嵌套的 `SELECT` 查询，用于引用外部查询中的列。 例如，在[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)教程中，我们在 `ProductsTableAdapter` s 主查询中使用两个相关子查询来返回每个产品的类别和供应商名称。 `JOIN` 是将两个不同表中的相关行合并在一起的 SQL 构造。 我们在使用[SqlDataSource 控件查询数据](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs.md)中使用了 `JOIN`，以显示每个产品的类别信息。

由于 TableAdapter s 向导中有一些用于自动生成相应 `INSERT`、`UPDATE`和 `DELETE` 语句的限制，我们 abstained 了与 Tableadapter 结合 `JOIN` 使用的原因。 更具体地说，如果 TableAdapter 的主查询包含任何 `JOIN`，则 TableAdapter 无法自动为其 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性创建即席 SQL 语句或存储过程。

在本教程中，我们将先比较并对比相关的子查询和 `JOIN`，然后再研究如何创建在其主查询中包含 `JOIN` 的 TableAdapter。

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>比较和对比相关子查询和`JOIN`

请记住，在 `Northwind` 数据集的第一个教程中创建的 `ProductsTableAdapter` 使用相关子查询来返回每个产品的对应类别和供应商名称。 `ProductsTableAdapter` 的主查询如下所示。

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample1.sql)]

这两个相关子查询-`(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` 和 `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)` `SELECT` 查询将每个产品返回单个值作为外部 `SELECT` 语句的列列表中的额外列。

或者，可以使用 `JOIN` 返回每个产品的供应商和类别名称。 下面的查询返回与上述输出相同的输出，但使用 `JOIN` s 来代替子查询：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample2.sql)]

`JOIN` 根据某些条件将一个表中的记录与另一个表中的记录合并在一起。 例如，在上面的查询中，`LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` 指示 SQL Server 将每个产品记录与类别记录合并，其 `CategoryID` 值与产品 `CategoryID` 值匹配。 合并的结果允许我们处理每个产品（如 `CategoryName`）对应的类别字段。

> [!NOTE]
> 在从关系数据库查询数据时，通常使用 `JOIN`。 如果你不熟悉 `JOIN` 语法，或者需要在其使用时进行一次工作，我将在[W3 学校](http://www.w3schools.com/)上建议使用[SQL Join 教程](http://www.w3schools.com/sql/sql_join.asp)。 另请参阅[SQL 联机丛书](https://msdn.microsoft.com/library/ms130214.aspx)的[`JOIN` 基础知识](https://msdn.microsoft.com/library/ms191517.aspx)和[子查询基础](https://msdn.microsoft.com/library/ms189575.aspx)部分。

由于 `JOIN` s 和相关子查询都可用于检索其他表中的相关数据，因此许多开发人员会将其外在优势，知道使用哪种方法。 我以前提到过的所有 SQL 专家都大致相同，因为 SQL Server 将产生大致完全相同的执行计划。 他们的建议是使用您和您的团队最熟悉的方法。 值得一提的是，在 imparting 这一建议之后，这些专家会立即通过相关子查询表达 `JOIN` s 的首选项。

使用类型化数据集生成数据访问层时，这些工具在使用子查询时效果更佳。 特别是，当主查询包含任何 `JOIN` 时，TableAdapter s 向导不会自动生成相应的 `INSERT`、`UPDATE`和 `DELETE` 语句，但在使用相关子查询时将自动生成这些语句。

若要探索这种缺点，请在 `~/App_Code/DAL` 文件夹中创建临时类型化数据集。 在 "TableAdapter 配置向导" 中，选择使用即席 SQL 语句，并输入以下 `SELECT` 查询（请参阅图1）：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample3.sql)]

[![输入包含联接的主查询](updating-the-tableadapter-to-use-joins-cs/_static/image2.png)](updating-the-tableadapter-to-use-joins-cs/_static/image1.png)

**图 1**：输入包含 `JOIN` s 的主查询（[单击以查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image3.png)）

默认情况下，TableAdapter 会根据主查询自动创建 `INSERT`、`UPDATE`和 `DELETE` 语句。 如果单击 "高级" 按钮，可以看到已启用此功能。 尽管有此设置，但 TableAdapter 将无法创建 `INSERT`、`UPDATE`和 `DELETE` 语句，因为主查询包含 `JOIN`。

![输入包含联接的主查询](updating-the-tableadapter-to-use-joins-cs/_static/image4.png)

**图 2**：输入包含 `JOIN` s 的主查询

单击“完成”按钮以完成向导。 此时，您的数据集设计器将包含单个 TableAdapter，其中每个字段对应于在 `SELECT` 查询的列列表中返回的每个字段。 这包括 `CategoryName` 和 `SupplierName`，如图3所示。

![DataTable 包含列列表中返回的每个字段的列](updating-the-tableadapter-to-use-joins-cs/_static/image5.png)

**图 3**： DataTable 包含列列表中返回的每个字段的列

虽然 DataTable 具有相应的列，但 TableAdapter 缺少 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性的值。 若要确认这一点，请在设计器中单击 TableAdapter，然后前往属性窗口。 在这里，你将看到 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性设置为 "（无）"。

[![将 InsertCommand、UpdateCommand 和 DeleteCommand 属性设置为 "（无）"](updating-the-tableadapter-to-use-joins-cs/_static/image7.png)](updating-the-tableadapter-to-use-joins-cs/_static/image6.png)

**图 4**： "`InsertCommand`"、"`UpdateCommand`" 和 "`DeleteCommand`" 属性均设置为 "（无）" （[单击查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image8.png)）

若要解决这种缺点，可以通过属性窗口为 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性手动提供 SQL 语句和参数。 或者，我们可以首先将 TableAdapter s 主查询配置为*不*包括任何 `JOIN`。 这将允许为我们自动生成 `INSERT`、`UPDATE`和 `DELETE` 语句。 完成向导后，可以手动从属性窗口中更新 TableAdapter `SelectCommand`，使其包含 `JOIN` 语法。

虽然这种方法有效，但在使用即席 SQL 查询时非常脆弱，因为无论何时通过向导重新配置 TableAdapter s 主查询，都将重新创建自动生成的 `INSERT`、`UPDATE`和 `DELETE` 语句。 这意味着，如果右键单击 TableAdapter，从上下文菜单中选择 "配置"，则会丢失以后进行的所有自定义，并再次完成向导。

TableAdapter 自动生成的 `INSERT`、`UPDATE`和 `DELETE` 语句的易受攻击，只限于即席 SQL 语句。 如果 TableAdapter 使用存储过程，则可以自定义 `SelectCommand`、`InsertCommand`、`UpdateCommand`或 `DeleteCommand` 存储过程，并重新运行 TableAdapter 配置向导，而不必担心将会修改存储过程。

在接下来的几个步骤中，我们将创建一个 TableAdapter，该 TableAdapter 最初使用省略任何 `JOIN` 的主查询，以便自动生成相应的 insert、update 和 delete 存储过程。 然后，将更新 `SelectCommand`，以便使用从相关表返回其他列的 `JOIN`。 最后，我们将创建一个相应的业务逻辑层类，并演示如何在 ASP.NET 网页中使用 TableAdapter。

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>步骤1：使用简化的主查询创建 TableAdapter

对于本教程，我们将为 `NorthwindWithSprocs` 数据集中的 `Employees` 表添加 TableAdapter 和强类型的 DataTable。 `Employees` 表包含一个 `ReportsTo` 字段，该字段指定了员工经理 `EmployeeID`。 例如，employee Anne 刘天妮的 `ReportTo` 值为5，这是 Steven 的 `EmployeeID`。 因此，Anne 向 Steven （经理）报告。 除了报告每个员工 `ReportsTo` 值，我们可能还想要检索其经理的姓名。 这可以使用 `JOIN`来实现。 但在最初创建 TableAdapter 时使用 `JOIN` 会阻止向导自动生成相应的插入、更新和删除功能。 因此，我们首先创建一个不包含任何 `JOIN` 的 TableAdapter。 然后，在步骤2中，我们将更新主查询存储过程，以通过 `JOIN`检索管理器的名称。

首先打开 `~/App_Code/DAL` 文件夹中的 `NorthwindWithSprocs` 数据集。 右键单击设计器，从上下文菜单中选择 "添加" 选项，然后选择 "TableAdapter" 菜单项。 这将启动 TableAdapter 配置向导。 如图5所示，让向导创建新的存储过程，然后单击 "下一步"。 有关使用 TableAdapter s 向导创建新存储过程的复习，请参阅为[类型化数据集 tableadapter 教程创建新的存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)。

[![选择 "创建新存储过程" 选项](updating-the-tableadapter-to-use-joins-cs/_static/image10.png)](updating-the-tableadapter-to-use-joins-cs/_static/image9.png)

**图 5**：选择 "创建新存储过程" 选项（[单击以查看完全大小的映像](updating-the-tableadapter-to-use-joins-cs/_static/image11.png)）

对于 TableAdapter s 主查询使用以下 `SELECT` 语句：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample4.sql)]

由于此查询不包含任何 `JOIN`，因此，TableAdapter 向导会自动创建具有相应 `INSERT`、`UPDATE`和 `DELETE` 语句的存储过程，以及用于执行主查询的存储过程。

以下步骤使我们能够命名 TableAdapter 的存储过程。 使用名称 `Employees_Select`、`Employees_Insert`、`Employees_Update`和 `Employees_Delete`，如图6所示。

[![命名 TableAdapter 的存储过程](updating-the-tableadapter-to-use-joins-cs/_static/image13.png)](updating-the-tableadapter-to-use-joins-cs/_static/image12.png)

**图 6**：命名 TableAdapter 的存储过程（[单击以查看完全大小的映像](updating-the-tableadapter-to-use-joins-cs/_static/image14.png)）

最后一个步骤提示我们命名 TableAdapter 的方法。 使用 `Fill` 和 `GetEmployees` 作为方法名称。 另外，请确保选中 "创建方法以将更新直接发送到数据库（GenerateDBDirectMethods）" 复选框。

[![命名 TableAdapter s 方法 Fill 和 GetEmployees](updating-the-tableadapter-to-use-joins-cs/_static/image16.png)](updating-the-tableadapter-to-use-joins-cs/_static/image15.png)

**图 7**：将 TableAdapter s 方法命名 `Fill` 和 `GetEmployees` （[单击以查看完全大小的映像](updating-the-tableadapter-to-use-joins-cs/_static/image17.png)）

完成向导后，请花点时间检查数据库中的存储过程。 应该会看到四个新的文件： `Employees_Select`、`Employees_Insert`、`Employees_Update`和 `Employees_Delete`。 接下来，检查刚刚创建的 `EmployeesDataTable` 和 `EmployeesTableAdapter`。 对于主查询返回的每个字段，DataTable 都包含一个列。 单击 TableAdapter，然后中转到属性窗口。 在这里，你将看到 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性正确配置为调用相应的存储过程。

[![TableAdapter 包含插入、更新和删除功能](updating-the-tableadapter-to-use-joins-cs/_static/image19.png)](updating-the-tableadapter-to-use-joins-cs/_static/image18.png)

**图 8**： TableAdapter 包含插入、更新和删除功能（[单击以查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image20.png)）

自动创建 insert、update 和 delete 存储过程并正确配置 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性后，我们就可以自定义 `SelectCommand` 的存储过程，以返回有关每个员工经理的其他信息。 具体而言，我们需要更新 `Employees_Select` 存储过程以使用 `JOIN` 并返回 manager `FirstName` 和 `LastName` 值。 在更新了存储过程后，我们将需要更新 DataTable，使其包含这些其他列。 我们将在步骤2和步骤3中处理这两个任务。

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>步骤2：自定义存储过程以包含`JOIN`

首先转到服务器资源管理器，向下钻取 Northwind 数据库的 "存储过程" 文件夹，并打开 `Employees_Select` 存储过程。 如果看不到此存储过程，请右键单击 "存储过程" 文件夹，然后选择 "刷新"。 更新存储过程，使其使用 `LEFT JOIN` 返回经理的名字和姓氏：

[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample5.sql)]

更新 `SELECT` 语句后，请转到 "文件" 菜单，然后选择 "保存 `Employees_Select`来保存更改。 此外，也可以单击工具栏中的 "保存" 图标或按 Ctrl + S。 保存更改后，右键单击服务器资源管理器中的 `Employees_Select` 存储过程，然后选择 "执行"。 这将运行存储过程，并在输出窗口中显示其结果（参见图9）。

[![存储过程结果将显示在输出窗口](updating-the-tableadapter-to-use-joins-cs/_static/image22.png)](updating-the-tableadapter-to-use-joins-cs/_static/image21.png)

**图 9**：存储过程结果显示在输出窗口中（[单击以查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image23.png)）

## <a name="step-3-updating-the-datatable-s-columns"></a>步骤3：更新 DataTable 列

此时，`Employees_Select` 存储过程返回 `ManagerFirstName` 和 `ManagerLastName` 值，但 `EmployeesDataTable` 缺少这些列。 可以通过以下两种方式之一将这些缺失列添加到 DataTable：

- **手动**-在数据集设计器中右键单击 DataTable，然后从 "添加" 菜单中选择 "列"。 然后，可以对该列命名并相应地设置其属性。
- **自动**-TableAdapter 配置向导将更新 DataTable 列以反映 `SelectCommand` 存储过程返回的字段。 使用即席 SQL 语句时，向导还会删除 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 属性，因为 `SelectCommand` 现在包含 `JOIN`。 但在使用存储过程时，这些命令属性会保持不变。

我们已经探讨了如何在前面的教程中手动添加 DataTable 列，包括使用带有详细信息 DataList 和[上传文件](../working-with-binary-files/uploading-files-cs.md)[的主记录的项目符号列表的母版/详细](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)信息，我们将在下一教程中更详细地介绍此过程。 但对于本教程，让我们通过 TableAdapter 配置向导使用自动方法。

首先右键单击 "`EmployeesTableAdapter`"，然后从上下文菜单中选择 "配置"。 这将打开 "TableAdapter 配置向导"，其中列出了用于选择、插入、更新和删除的存储过程，以及它们的返回值和参数（如果有）。 图10显示了此向导。 这里，我们可以看到 `Employees_Select` 存储过程现在返回 `ManagerFirstName` 和 `ManagerLastName` 字段。

[![向导显示 Employees_Select 存储过程的已更新列列表](updating-the-tableadapter-to-use-joins-cs/_static/image25.png)](updating-the-tableadapter-to-use-joins-cs/_static/image24.png)

**图 10**：向导显示 `Employees_Select` 存储过程的已更新列列表（[单击以查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image26.png)）

单击 "完成" 完成向导。 返回到数据集设计器后，`EmployeesDataTable` 包括另外两列： `ManagerFirstName` 和 `ManagerLastName`。

[![EmployeesDataTable 包含两个新列](updating-the-tableadapter-to-use-joins-cs/_static/image28.png)](updating-the-tableadapter-to-use-joins-cs/_static/image27.png)

**图 11**： `EmployeesDataTable` 包含两个新列（[单击以查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image29.png)）

为了说明更新后的 `Employees_Select` 存储过程是否有效，并且 TableAdapter 的插入、更新和删除功能仍可正常工作，让我们创建一个允许用户查看和删除员工的网页。 但在创建此类页面之前，我们需要先在业务逻辑层中创建一个新类，以便与 `NorthwindWithSprocs` 数据集中的员工合作。 在步骤4中，我们将创建一个 `EmployeesBLLWithSprocs` 类。 在步骤5中，我们将从 ASP.NET 页面使用此类。

## <a name="step-4-implementing-the-business-logic-layer"></a>步骤4：实现业务逻辑层

在名为 `EmployeesBLLWithSprocs.cs`的 `~/App_Code/BLL` 文件夹中创建一个新的类文件。 此类模仿现有 `EmployeesBLL` 类的语义，只有这一新的类提供的方法更少，并使用 `NorthwindWithSprocs` 数据集（而不是 `Northwind` 数据集）。 向 `EmployeesBLLWithSprocs` 类添加下面的代码。

[!code-csharp[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample6.cs)]

`EmployeesBLLWithSprocs` 类 `Adapter` 属性返回 `NorthwindWithSprocs` 数据集 `EmployeesTableAdapter`的实例。 该类 `GetEmployees` 和 `DeleteEmployee` 方法使用此方法。 `GetEmployees` 方法调用对应于 `EmployeesTableAdapter` s 的 `GetEmployees` 方法，该方法调用 `Employees_Select` 存储过程，并在 `EmployeeDataTable`中填充其结果。 `DeleteEmployee` 方法类似地调用 `EmployeesTableAdapter` s `Delete` 方法，该方法调用 `Employees_Delete` 存储过程。

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>步骤5：使用表示层中的数据

`EmployeesBLLWithSprocs` 类完成后，我们就可以通过 ASP.NET 页面来处理员工数据。 打开 `AdvancedDAL` 文件夹中的 "`JOINs.aspx`" 页，然后将 GridView 从工具箱拖动到设计器上，并将其 `ID` 属性设置为 "`Employees`"。 接下来，从 GridView s 智能标记将网格绑定到名为 `EmployeesDataSource`的新 ObjectDataSource 控件。

将 ObjectDataSource 配置为使用 `EmployeesBLLWithSprocs` 类，并从 "选择" 和 "删除" 选项卡中，确保从下拉列表中选择 `GetEmployees` 和 `DeleteEmployee` 方法。 单击 "完成" 以完成 ObjectDataSource 配置。

[![将 ObjectDataSource 配置为使用 EmployeesBLLWithSprocs 类](updating-the-tableadapter-to-use-joins-cs/_static/image31.png)](updating-the-tableadapter-to-use-joins-cs/_static/image30.png)

**图 12**：将 ObjectDataSource 配置为使用 `EmployeesBLLWithSprocs` 类（[单击以查看完全大小的映像](updating-the-tableadapter-to-use-joins-cs/_static/image32.png)）

[![让 ObjectDataSource 使用 GetEmployees 和 DeleteEmployee 方法](updating-the-tableadapter-to-use-joins-cs/_static/image34.png)](updating-the-tableadapter-to-use-joins-cs/_static/image33.png)

**图 13**：使 ObjectDataSource 使用 `GetEmployees` 和 `DeleteEmployee` 方法（[单击查看完全大小的映像](updating-the-tableadapter-to-use-joins-cs/_static/image35.png)）

对于每个 `EmployeesDataTable` s 列，Visual Studio 会将 BoundField 添加到 GridView。 删除所有这些 BoundFields （`Title`、`LastName`、`FirstName`、`ManagerFirstName`和 `ManagerLastName` 除外），并分别重命名最后四个 BoundFields 到 "姓"、"名字"、"经理"、"名字" 和 "经理姓氏" 的 `HeaderText` 属性。

若要允许用户从此页中删除员工，需要执行两项操作。 首先，通过选中 "启用从其智能标记中删除" 选项来指示 GridView 提供删除功能。 其次，将 ObjectDataSource `OldValuesParameterFormatString` 属性从 ObjectDataSource 向导（`original_{0}`）设置的值更改为其默认值（`{0}`）。 进行这些更改后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample7.aspx)]

通过浏览器访问页面，对其进行测试。 如图14所示，此页将列出每个员工及其经理的姓名（假设他们有一个）。

[![Employees_Select 存储过程中的联接返回管理器的名称](updating-the-tableadapter-to-use-joins-cs/_static/image37.png)](updating-the-tableadapter-to-use-joins-cs/_static/image36.png)

**图 14**： `Employees_Select` 存储过程中的 `JOIN` 返回经理的名称（[单击查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image38.png)）

单击 "删除" 按钮将启动删除工作流，该工作流落执行 `Employees_Delete` 存储过程。 但是，由于外键约束冲突，存储过程中尝试的 `DELETE` 语句将失败（请参见图15）。 具体而言，每个员工都有 `Orders` 表中的一条或多条记录，导致删除失败。

[删除具有相应订单的员工将导致外键约束冲突 ![](updating-the-tableadapter-to-use-joins-cs/_static/image40.png)](updating-the-tableadapter-to-use-joins-cs/_static/image39.png)

**图 15**：删除具有相应订单的员工将导致外键约束冲突（[单击以查看完全大小的图像](updating-the-tableadapter-to-use-joins-cs/_static/image41.png)）

若要允许删除员工，可以执行以下操作：

- 将 foreign key 约束更新为级联删除，
- 对于要删除的员工，请从 `Orders` 表中手动删除记录，或
- 更新 `Employees_Delete` 存储过程，以先删除 `Orders` 表中的相关记录，然后再删除 `Employees` 记录。 我们在[使用类型化数据集 s tableadapter 教程的现有存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)中讨论了这一方法。

我将此留给读者的练习。

## <a name="summary"></a>摘要

使用关系数据库时，查询通常会从多个相关表中提取数据。 相关子查询和 `JOIN` 提供了两种不同的方法，可用于从查询中的相关表访问数据。 在前面的教程中，我们最常使用相关子查询，因为 TableAdapter 无法自动生成涉及 `JOIN` 的查询 `INSERT`、`UPDATE`和 `DELETE` 语句。 尽管可以手动提供这些值，但使用即席 SQL 语句时，在完成 TableAdapter 配置向导时，将覆盖任何自定义项。

幸运的是，使用存储过程创建的 Tableadapter 不会受到使用即席 SQL 语句创建的易受攻击。 因此，在使用存储过程时，可以创建一个其主查询使用 `JOIN` 的 TableAdapter。 在本教程中，我们介绍了如何创建此类 TableAdapter。 我们开始使用用于 TableAdapter s 查询的无 `JOIN``SELECT` 查询，以便自动创建相应的 insert、update 和 delete 存储过程。 完成 TableAdapter 的初始配置后，我们增加了 `SelectCommand` 存储过程以使用 `JOIN`，并重新运行了 TableAdapter 配置向导来更新 `EmployeesDataTable` 的列。

重新运行 TableAdapter 配置向导会自动更新 `EmployeesDataTable` 列，以反映 `Employees_Select` 存储过程返回的数据字段。 另外，我们还可以将这些列手动添加到 DataTable。 在下一教程中，我们将探讨如何手动将列添加到 DataTable。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Hilton Geisenow、David Suru 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [下一页](adding-additional-datatable-columns-cs.md)
