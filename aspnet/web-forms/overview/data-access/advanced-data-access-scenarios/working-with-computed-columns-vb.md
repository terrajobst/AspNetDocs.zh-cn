---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
title: 使用计算列（VB） |Microsoft Docs
author: rick-anderson
description: 创建数据库表时，Microsoft SQL Server 允许您定义计算列，该列的值是从通常 referen 的表达式计算得出的。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 5811b8ff-ed56-40fc-9397-6b69ae09a8f6
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: e425d7363c2cdea6efb0ba51f3fc2b6a5330bf2a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74602827"
---
# <a name="working-with-computed-columns-vb"></a>处理计算列 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_VB.zip)或[下载 PDF](working-with-computed-columns-vb/_static/datatutorial71vb1.pdf)

> 创建数据库表时，Microsoft SQL Server 允许您定义计算列，该列的值是由通常引用同一数据库记录中其他值的表达式计算得出的。 此类值在数据库中是只读的，在使用 Tableadapter 时需要特别注意。 在本教程中，我们将了解如何满足计算列所带来的挑战。

## <a name="introduction"></a>简介

Microsoft SQL Server 允许使用 *[计算列](https://msdn.microsoft.com/library/ms191250.aspx)* ，这些列的值是从通常引用同一表中其他列的值的表达式计算得出的。 例如，时间跟踪数据模型可能有一个名为 `ServiceLog` 的表，其中的列包括 `ServicePerformed`、`EmployeeID`、`Rate`和 `Duration`等。 尽管可以通过网页或其他编程界面来计算每个服务项目的应付金额（速率乘以持续时间），但在报告此信息的名为 `AmountDue` `ServiceLog` 表中加入列可能会很方便。 此列可以作为普通列创建，但需要在 `Rate` 或 `Duration` 列值更改时进行更新。 更好的方法是使用表达式 `Rate * Duration`使 `AmountDue` 列成为计算列。 这样做会导致 SQL Server 在查询中引用时自动计算 `AmountDue` 列值。

由于计算列的值是由表达式确定的，因此，此类列是只读的，因此不能在 `INSERT` 或 `UPDATE` 语句中为它们分配值。 但是，当计算列是使用即席 SQL 语句的 TableAdapter 的主要查询的一部分时，它们将自动包含在自动生成的 `INSERT` 和 `UPDATE` 语句中。 因此，必须更新 TableAdapter s `INSERT` 和 `UPDATE` 查询以及 `InsertCommand` 和 `UpdateCommand` 属性才能删除对所有计算列的引用。

将计算列与使用即席 SQL 语句的 TableAdapter 结合使用的一个挑战是，在完成 TableAdapter 配置向导时，将自动重新生成 TableAdapter s `INSERT` 和 `UPDATE` 查询。 因此，如果重新运行该向导，则从 `UPDATE` `INSERT` 中手动删除的计算列将重新出现。 尽管使用存储过程的 Tableadapter 不受此易受攻击的影响，但它们确实有其自己的不相关，我们将在步骤3中进行解决。

在本教程中，我们会将计算列添加到 Northwind 数据库中的 `Suppliers` 表，然后创建相应的 TableAdapter 以便使用此表及其计算列。 我们会让 TableAdapter 使用存储过程而不是即席 SQL 语句，以便在使用 TableAdapter 配置向导时，自定义设置不会丢失。

让我们开始吧！

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>步骤1：将计算列添加到`Suppliers`表

Northwind 数据库没有任何计算列，因此我们需要添加一个。 在本教程中，我们将计算列添加到名为 `FullContactName` 的 `Suppliers` 表中，该表返回按以下格式使用的联系人姓名、职务和公司： `ContactName` （`ContactTitle`，`CompanyName`）。 显示与供应商有关的信息时，可以在报表中使用此计算列。

首先，在服务器资源管理器中右键单击 `Suppliers` 表，然后从上下文菜单中选择 "打开表定义"，以打开 `Suppliers` 表定义。 这将显示表的列及其属性（如数据类型），无论它们是否允许 `NULL` 等。 若要添加计算列，请首先在列名称中键入表定义。 接下来，在属性窗口列的 "计算列规范" 部分下的 "（公式）" 文本框中输入其表达式（请参阅图1）。 将计算列 `FullContactName` 命名，并使用以下表达式：

[!code-sql[Main](working-with-computed-columns-vb/samples/sample1.sql)]

请注意，可以使用 `+` 运算符将字符串连接到 SQL 中。 `CASE` 语句的使用方式类似于传统编程语言中的条件。 在上面的表达式中，`CASE` 语句可以读取为：如果 `ContactTitle` 不 `NULL`，则输出用逗号连接的 `ContactTitle` 值，否则不发出任何内容。 有关 `CASE` 语句有用性的详细信息，请参阅[SQL `CASE` 语句的强大功能](http://www.4guysfromrolla.com/webtech/102704-1.shtml)。

> [!NOTE]
> 可以使用其他 `ISNULL(ContactTitle, '')`，而不是使用 `CASE` 语句。 如果 CheckExpression 为非 NULL，则返回 ，否则返回*replacementValue*。 [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx) 尽管 `ISNULL` 或 `CASE` 在此实例中都有效，但仍有更复杂的方案，`ISNULL`不能匹配 `CASE` 语句的灵活性。

添加此计算列后，你的屏幕应类似于图1中的屏幕截图。

[![将名为 FullContactName 的计算列添加到供应商表](working-with-computed-columns-vb/_static/image2.png)](working-with-computed-columns-vb/_static/image1.png)

**图 1**：将名为 `FullContactName` 的计算列添加到 `Suppliers` 表（[单击查看完全大小的图像](working-with-computed-columns-vb/_static/image3.png)）

命名计算列并输入其表达式后，通过单击工具栏中的 "保存" 图标，通过按 Ctrl + S 或通过转到 "文件" 菜单并选择 "保存 `Suppliers`来保存对表所做的更改。

保存表应刷新服务器资源管理器，包括 `Suppliers` 表 s 列列表中只添加的列。 而且，输入到 "（公式）" 文本框中的表达式将自动调整为一个等效的表达式，该表达式包含不必要的空格，将列名称括在方括号（`[]`）中，并包含括号来更明确地显示运算顺序：

[!code-sql[Main](working-with-computed-columns-vb/samples/sample2.sql)]

有关 Microsoft SQL Server 中计算列的详细信息，请参阅[技术文档](https://msdn.microsoft.com/library/ms191250.aspx)。 另外，请参阅[如何：指定计算列](https://msdn.microsoft.com/library/ms188300.aspx)以获取创建计算列的分步演练。

> [!NOTE]
> 默认情况下，计算列不会以物理方式存储在表中，而是在每次在查询中引用它们时重新计算列。 不过，通过选中 "持久保存" 复选框，您可以指示 SQL Server 将计算列实际存储在表中。 这样做允许在计算列上创建索引，这可以提高在其 `WHERE` 子句中使用计算列值的查询的性能。 有关详细信息，请参阅为[计算列创建索引](https://msdn.microsoft.com/library/ms189292.aspx)。

## <a name="step-2-viewing-the-computed-column-s-values"></a>步骤2：查看计算列的值

开始在数据访问层上工作之前，让我们花点时间查看 `FullContactName` 值。 在服务器资源管理器中，右键单击 `Suppliers` 表名称，然后从上下文菜单中选择 "新建查询"。 这会打开一个查询窗口，提示我们选择要在查询中包含的表。 添加 `Suppliers` 表，然后单击 "关闭"。 接下来，检查供应商表中的 `CompanyName`、`ContactName`、`ContactTitle`和 `FullContactName` 列。 最后，单击工具栏中的红色感叹号图标来执行查询并查看结果。

如图2所示，结果包括 `FullContactName`，其中使用格式 `ContactName` （`ContactTitle`、`CompanyName`）列出 `CompanyName`、`ContactName`和 `ContactTitle` 列。

[![FullContactName 使用格式名称（ContactTitle，公司名称）](working-with-computed-columns-vb/_static/image5.png)](working-with-computed-columns-vb/_static/image4.png)

**图 2**： `FullContactName` 使用格式 `ContactName` （`ContactTitle`，`CompanyName`）（[单击查看完全大小的图像](working-with-computed-columns-vb/_static/image6.png)）

## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>步骤3：将`SuppliersTableAdapter`添加到数据访问层

为了在应用程序中使用供应商信息，我们需要首先在 DAL 中创建一个 TableAdapter 和 DataTable。 理想情况下，可以使用前面教程中所述的相同步骤来完成此操作。 但是，使用计算列会引入几个 wrinkles，用于提供讨论。

如果使用的是使用即席 SQL 语句的 TableAdapter，只需通过 TableAdapter 配置向导将计算列包含在 TableAdapter 主查询中。 但是，这将自动生成 `INSERT` 和包含计算列的 `UPDATE` 语句。 如果尝试执行其中一种方法，则会出现 `SqlException` 一条消息，其中包含列 ColumnName，因此无法修改列*ColumnName* ，因为它是计算列，或者是将引发 UNION 运算符的结果。 尽管可以通过 TableAdapter s `InsertCommand` 和 `UpdateCommand` 属性手动调整 `INSERT` 和 `UPDATE` 语句，但每当重新运行 TableAdapter 配置向导时，这些自定义项都将丢失。

由于使用即席 SQL 语句的 Tableadapter 的易受攻击，因此建议在使用计算列时使用存储过程。 如果使用的是现有存储过程，只需按[使用类型化数据集的 tableadapter 教程的现有存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)中所述配置 TableAdapter。 但是，如果您具有使用 TableAdapter 向导来创建存储过程，则必须最初从主查询中省略所有计算列。 如果在主查询中包含计算列，则 TableAdapter 配置向导将在完成时通知你无法创建相应的存储过程。 简而言之，我们需要使用计算的无列主查询来初始配置 TableAdapter，然后手动更新相应的存储过程，并 `SelectCommand`，以包括计算列。 此方法类似于 "[更新 TableAdapter 以使用](updating-the-tableadapter-to-use-joins-vb.md) *`JOIN`教程*" 中使用的方法。

对于本教程，让我们添加一个新的 TableAdapter，并让它自动创建存储过程。 因此，我们首先需要从主查询中省略 `FullContactName` 计算列。

首先打开 `~/App_Code/DAL` 文件夹中的 `NorthwindWithSprocs` 数据集。 在设计器中单击右键，然后从上下文菜单中选择添加新的 TableAdapter。 这将启动 TableAdapter 配置向导。 指定要查询数据的数据库（从 `Web.config``NORTHWNDConnectionString`），然后单击 "下一步"。 由于尚未创建用于查询或修改 `Suppliers` 表的任何存储过程，因此请选择 "创建新存储过程" 选项，以便向导将为我们创建并单击 "下一步"。

[![选择 "创建新存储过程" 选项](working-with-computed-columns-vb/_static/image8.png)](working-with-computed-columns-vb/_static/image7.png)

**图 3**：选择 "创建新存储过程" 选项（[单击以查看完全大小的映像](working-with-computed-columns-vb/_static/image9.png)）

后续步骤会提示我们进行主查询。 输入以下查询，该查询将返回每个供应商的 `SupplierID`、`CompanyName`、`ContactName`和 `ContactTitle` 列。 请注意，此查询有意省略了计算列（`FullContactName`）;我们将更新相应的存储过程，以在步骤4中包括此列。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample3.sql)]

在输入主查询并单击 "下一步" 后，向导将允许您命名将生成的四个存储过程。 将这些存储过程命名 `Suppliers_Select`、`Suppliers_Insert`、`Suppliers_Update`和 `Suppliers_Delete`，如图4所示。

[![自定义自动生成的存储过程的名称](working-with-computed-columns-vb/_static/image11.png)](working-with-computed-columns-vb/_static/image10.png)

**图 4**：自定义自动生成的存储过程的名称（[单击以查看完全大小的映像](working-with-computed-columns-vb/_static/image12.png)）

下一个向导步骤允许我们命名 TableAdapter 方法，并指定访问和更新数据所用的模式。 选中所有三个复选框，但将 `GetData` 方法重命名为 `GetSuppliers`。 单击“完成”按钮以完成向导。

[![将 GetSuppliers 的方法重命名为 ""](working-with-computed-columns-vb/_static/image14.png)](working-with-computed-columns-vb/_static/image13.png)

**图 5**：将 `GetData` 方法重命名为 `GetSuppliers` （[单击查看完全大小的图像](working-with-computed-columns-vb/_static/image15.png)）

单击 "完成" 后，向导将创建四个存储过程，并将 TableAdapter 和相应的 DataTable 添加到类型化数据集。

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>步骤4：在 TableAdapter s 主查询中包括计算列

现在，我们需要更新在步骤3中创建的 TableAdapter 和 DataTable，以包含 `FullContactName` 计算列。 此操作包括两个步骤：

1. 更新 `Suppliers_Select` 存储过程以返回 `FullContactName` 计算列，并
2. 更新 DataTable 以包含相应的 `FullContactName` 列。

首先导航到服务器资源管理器并向下钻取到 "存储过程" 文件夹。 打开 `Suppliers_Select` 存储过程并更新 `SELECT` 查询，使之包含 `FullContactName` 计算列：

[!code-sql[Main](working-with-computed-columns-vb/samples/sample4.sql)]

通过单击工具栏中的 "保存" 图标，通过按 Ctrl + S 或从 "文件" 菜单中选择 "保存 `Suppliers_Select`" 选项，保存对存储过程所做的更改。

接下来，返回到 "数据集设计器"，右键单击 "`SuppliersTableAdapter`"，然后从上下文菜单中选择 "配置"。 请注意，`Suppliers_Select` 列现在包含其数据列集合中的 `FullContactName` 列。

[![运行 TableAdapter s 配置向导以更新 DataTable 列](working-with-computed-columns-vb/_static/image17.png)](working-with-computed-columns-vb/_static/image16.png)

**图 6**：运行 TableAdapter s 配置向导以更新 DataTable 的列（[单击以查看完全大小的映像](working-with-computed-columns-vb/_static/image18.png)）

单击“完成”按钮以完成向导。 这会将相应的列自动添加到 `SuppliersDataTable`。 TableAdapter 向导的智能足以检测 `FullContactName` 列是否为计算列，因此为只读。 因此，它将 `ReadOnly` 的列属性设置为 `true`。 若要验证这一点，请从 `SuppliersDataTable` 中选择列，然后访问属性窗口（请参阅图7）。 请注意，也会相应地设置 `FullContactName` 列 s `DataType` 和 `MaxLength` 属性。

[![FullContactName 列被标记为只读](working-with-computed-columns-vb/_static/image20.png)](working-with-computed-columns-vb/_static/image19.png)

**图 7**： `FullContactName` 列被标记为只读（[单击以查看完全大小的图像](working-with-computed-columns-vb/_static/image21.png)）

## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>步骤5：将`GetSupplierBySupplierID`方法添加到 TableAdapter

对于本教程，我们将创建一个在可更新的网格中显示供应商的 ASP.NET 页面。 在过去的教程中，我们通过将 DAL 中的特定记录作为强类型 DataTable 检索来更新业务逻辑层中的单个记录，更新其属性，然后将更新后的 DataTable 发送回 DAL，以将更改传播到数据库。 若要完成此第一步-从 DAL 检索要更新的记录，我们需要首先将 `GetSupplierBySupplierID(supplierID)` 方法添加到 DAL。

右键单击数据集设计中的 `SuppliersTableAdapter`，然后从上下文菜单中选择 "添加查询" 选项。 如步骤3中所述，通过选择 "创建新存储过程" 选项，让向导为我们生成新的存储过程（有关此向导步骤的屏幕截图，请参阅图3）。 由于此方法将返回包含多个列的记录，因此，指示要使用的 SQL 查询是返回行的 SELECT，然后单击 "下一步"。

[![选择 "选择返回行" 选项](working-with-computed-columns-vb/_static/image23.png)](working-with-computed-columns-vb/_static/image22.png)

**图 8**：选择 "选择返回行" 选项（[单击以查看完全大小的图像](working-with-computed-columns-vb/_static/image24.png)）

后续步骤会提示我们输入用于此方法的查询。 输入以下，这将返回与主查询相同的数据字段，但对于特定的供应商。

[!code-sql[Main](working-with-computed-columns-vb/samples/sample5.sql)]

下一个屏幕会要求我们命名将自动生成的存储过程。 为此存储过程命名 `Suppliers_SelectBySupplierID` 然后单击 "下一步"。

[![命名存储过程 Suppliers_SelectBySupplierID](working-with-computed-columns-vb/_static/image26.png)](working-with-computed-columns-vb/_static/image25.png)

**图 9**：将存储过程命名 `Suppliers_SelectBySupplierID` （[单击以查看完全大小的图像](working-with-computed-columns-vb/_static/image27.png)）

最后，向导提示我们输入用于 TableAdapter 的数据访问模式和方法名称。 选中这两个复选框，但将 `FillBy` 和 `GetDataBy` 方法分别重命名为 `FillBySupplierID` 和 `GetSupplierBySupplierID`。

[![命名 TableAdapter 方法 FillBySupplierID 和 GetSupplierBySupplierID](working-with-computed-columns-vb/_static/image29.png)](working-with-computed-columns-vb/_static/image28.png)

**图 10**：将 TableAdapter 方法命名 `FillBySupplierID` 和 `GetSupplierBySupplierID` （[单击以查看完全大小的映像](working-with-computed-columns-vb/_static/image30.png)）

单击“完成”按钮以完成向导。

## <a name="step-6-creating-the-business-logic-layer"></a>步骤6：创建业务逻辑层

在创建使用在步骤1中创建的计算列的 ASP.NET 页面之前，首先需要在 BLL 中添加相应的方法。 我们将在步骤7中创建的 ASP.NET 页允许用户查看和编辑供应商。 因此，我们需要 BLL 至少提供一个方法来获取所有供应商，并使用另一个方法来更新特定的供应商。

在 `~/App_Code/BLL` 文件夹中创建一个名为 `SuppliersBLLWithSprocs` 的新类文件，并添加以下代码：

[!code-vb[Main](working-with-computed-columns-vb/samples/sample6.vb)]

与其他 BLL 类一样，`SuppliersBLLWithSprocs` 具有一个 `Protected` `Adapter` 属性，该属性返回 `SuppliersTableAdapter` 类的实例以及两个 `Public` 方法： `GetSuppliers` 和 `UpdateSupplier`。 `GetSuppliers` 方法调用并返回由数据访问层中的相应 `GetSupplier` 方法返回的 `SuppliersDataTable`。 `UpdateSupplier` 方法检索有关通过调用 DAL s `GetSupplierBySupplierID(supplierID)` 方法更新的特定供应商的信息。 然后，它会更新 `CategoryName`、`ContactName`和 `ContactTitle` 属性，并通过调用数据访问层的 `Update` 方法并传入经过修改的 `SuppliersRow` 对象，将这些更改提交到数据库。

> [!NOTE]
> 除了 `SupplierID` 和 `CompanyName`之外，"供应商" 表中的所有列都允许 `NULL` 值。 因此，如果传入的 `contactName` 或 `contactTitle` 参数是 `Nothing`，我们需要分别使用 `ContactTitle` 和 `NULL` 方法将相应的 `ContactName` 和 `SetContactNameNull` 属性分别设置为 `SetContactTitleNull` 数据库值。

## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>步骤7：使用表示层中的计算列

将计算列添加到 `Suppliers` 表并且 DAL 和 BLL 进行了相应更新后，便可以生成可与 `FullContactName` 计算列一起使用的 ASP.NET 页。 首先打开 `AdvancedDAL` 文件夹中的 "`ComputedColumns.aspx`" 页，然后从 "工具箱" 拖动到设计器上。 将 GridView `ID` 属性设置为 `Suppliers`，并从其智能标记将其绑定到名为 `SuppliersDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用我们在步骤6中添加的 `SuppliersBLLWithSprocs` 类，然后单击 "下一步"。

[![将 ObjectDataSource 配置为使用 SuppliersBLLWithSprocs 类](working-with-computed-columns-vb/_static/image32.png)](working-with-computed-columns-vb/_static/image31.png)

**图 11**：将 ObjectDataSource 配置为使用 `SuppliersBLLWithSprocs` 类（[单击以查看完全大小的映像](working-with-computed-columns-vb/_static/image33.png)）

`SuppliersBLLWithSprocs` 类中仅定义了两个方法： `GetSuppliers` 和 `UpdateSupplier`。 确保在 "选择" 和 "更新" 选项卡中分别指定这两种方法，然后单击 "完成" 完成 ObjectDataSource 的配置。

完成 "数据源配置向导" 后，Visual Studio 将为返回的每个数据字段添加 BoundField。 删除 `SupplierID` BoundField，并分别将 `CompanyName`、`ContactName`、`ContactTitle`和 `FullContactName` BoundFields 的 `HeaderText` 属性分别更改为 "公司"、"联系人姓名"、"职务" 和 "完整联系人姓名"。 从智能标记中，选中 "启用编辑" 复选框以启用 GridView 的内置编辑功能。

除了将 BoundFields 添加到 GridView 外，完成数据源向导还会导致 Visual Studio 将 ObjectDataSource `OldValuesParameterFormatString` 属性设置为原始\_{0}。 将此设置恢复为其默认值 {0}。

对 GridView 和 ObjectDataSource 进行这些编辑后，其声明性标记应如下所示：

[!code-aspx[Main](working-with-computed-columns-vb/samples/sample7.aspx)]

接下来，通过浏览器访问此页。 如图12所示，每个供应商都在包含 `FullContactName` 列的网格中列出，其值只是与 `ContactName` （`ContactTitle`，`CompanyName`）格式设置的其他三个列的连接。

[网格中列出了每个供应商 ![](working-with-computed-columns-vb/_static/image35.png)](working-with-computed-columns-vb/_static/image34.png)

**图 12**：每个供应商在网格中列出（[单击以查看完全大小的图像](working-with-computed-columns-vb/_static/image36.png)）

单击特定供应商的 "编辑" 按钮会导致回发，并使该行呈现在其编辑界面中（参见图13）。 前三列呈现在其默认编辑界面中（`Text` 属性设置为数据字段的值）的 TextBox 控件。 但 `FullContactName` 列仍保留为文本。 如果在数据源配置向导完成时将 BoundFields 添加到 GridView，则 `FullContactName` BoundField s `ReadOnly` 属性设置为 `True`，因为 `SuppliersDataTable` 中的相应 `FullContactName` 列的 `ReadOnly` 属性设置为 `True`。 如步骤4所述，`FullContactName` s `ReadOnly` 属性设置为 `True`，因为 TableAdapter 检测到该列为计算列。

[![FullContactName 列不可编辑](working-with-computed-columns-vb/_static/image38.png)](working-with-computed-columns-vb/_static/image37.png)

**图 13**：无法编辑 `FullContactName` 列（[单击以查看完全大小的图像](working-with-computed-columns-vb/_static/image39.png)）

继续并更新一个或多个可编辑列的值，然后单击 "更新"。 请注意如何自动更新 `FullContactName` 的值以反映所做的更改。

> [!NOTE]
> GridView 当前对可编辑字段使用 BoundFields，从而导致默认编辑界面。 由于 `CompanyName` 字段是必需的，因此应将其转换为包含 RequiredFieldValidator 的 TemplateField。 对于感兴趣的读者来说，我将其作为练习。 有关将 BoundField 转换为 TemplateField 并添加验证控件的分步说明，请参阅向[编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)教程。

## <a name="summary"></a>总结

在定义表的架构时，Microsoft SQL Server 允许包含计算列。 这些列的值是从通常引用同一记录中其他列中的值的表达式计算得出的。 由于计算列的值基于表达式，因此它们是只读的，不能在 `INSERT` 或 `UPDATE` 语句中为其赋值。 这会在使用尝试自动生成相应的 `INSERT`、`UPDATE`和 `DELETE` 语句的 TableAdapter 的主查询中使用计算列时带来挑战。

在本教程中，我们讨论了规避计算列所带来的挑战的方法。 具体而言，我们在 TableAdapter 中使用存储过程来克服使用即席 SQL 语句的 Tableadapter 中的易受攻击。 当使用 TableAdapter 向导创建新的存储过程时，主要查询最初省略所有计算列，这一点很重要，因为它们存在会阻止数据修改存储过程的生成。 最初配置 TableAdapter 后，可以重组其 `SelectCommand` 存储过程以包含所有计算列。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Hilton Geisenow 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](adding-additional-datatable-columns-vb.md)
> [下一页](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
