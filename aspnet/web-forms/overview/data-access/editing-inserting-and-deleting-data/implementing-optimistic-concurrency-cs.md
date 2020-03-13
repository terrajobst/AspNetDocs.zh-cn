---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: 实现开放式并发（C#） |Microsoft Docs
author: rick-anderson
description: 对于允许多个用户编辑数据的 web 应用程序，有两个用户可以同时编辑相同数据的风险。 在此 tutori 中 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 3cddb0efd28249ffc5708ece39c80581d078a5a2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78492422"
---
# <a name="implementing-optimistic-concurrency-c"></a>实现乐观并发 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe)或[下载 PDF](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> 对于允许多个用户编辑数据的 web 应用程序，有两个用户可以同时编辑相同数据的风险。 在本教程中，我们将实现开放式并发控制来应对此风险。

## <a name="introduction"></a>介绍

对于仅允许用户查看数据的 web 应用程序，或仅包含可修改数据的单个用户的 web 应用程序，不会有两个并发用户意外覆盖另一个更改的威胁。 但对于允许多个用户更新或删除数据的 web 应用程序，有可能会有一个用户对另一个并发用户的冲突进行修改。 如果没有任何并发策略，当两个用户同时编辑一条记录时，最后提交她的更改的用户将覆盖第一个记录所做的更改。

例如，假设两个用户 Jisun 和 Sam 都在访问应用程序中的一个页面，允许访问者通过 GridView 控件更新和删除产品。 同时单击 GridView 中的 "编辑" 按钮。 Jisun 将产品名称更改为 "Chai 茶" 并单击 "更新" 按钮。 Net 结果是发送到数据库的 `UPDATE` 语句，该语句将设置产品的*所有*可更新字段（即使 Jisun 仅更新了一个字段，`ProductName`）。 此时，数据库的值为 "Chai 茶"、"供应商现 Liquids"、"供应商"。 但是，Sam 上的 GridView 仍会在可编辑 GridView 行中显示为 "Chai" 的产品名称。 提交 Jisun 更改后的几秒钟后，Sam 会将类别更新为调味品并单击 "更新"。 这会导致向数据库发送 `UPDATE` 语句，该语句将产品名称设置为 "Chai"，将 `CategoryID` 设置为相应的饮料类别 ID 等。 已覆盖 Jisun 对产品名称所做的更改。 图1以图形方式描述此系列事件。

[![两个用户同时更新 a 记录时，可能会有一个用户更改为覆盖其他](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**图 1**：当两个用户同时更新 a 记录时，可能会有一个用户更改为覆盖其他（[单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image3.png)）

同样，当两个用户访问某个页面时，当另一个用户删除记录时，可能会有一个用户正在更新该记录。 或者，在用户加载页面和单击 "删除" 按钮时，其他用户可能已修改该记录的内容。

有三种可用的[并发控制](http://en.wikipedia.org/wiki/Concurrency_control)策略：

- **不执行任何**操作-如果并发用户正在修改同一条记录，则让最后一个 commit 入选（默认行为）
- [**开放式并发**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)-假设每次可能都存在并发冲突，而绝大多数时间都不会出现这种冲突;因此，如果发生冲突，只需通知用户其更改将无法保存，因为其他用户已修改了相同的数据
- **悲观并发**-假设并发冲突很常见，并且由于其他用户的并发活动，用户不会被告知其更改未保存，因此，当一个用户开始更新记录时，将其锁定，从而阻止其他任何用户编辑或删除该记录，直到用户提交其修改为止

到目前为止，我们的所有教程都使用了默认的并发解决方案策略-即，我们让最后一次写入入选。 在本教程中，我们将讨论如何实现开放式并发控制。

> [!NOTE]
> 在本系列教程中，我们不会讨论悲观并发示例。 很少使用悲观并发，因为如果没有正确释放，此类锁会阻止其他用户更新数据。 例如，如果用户锁定了某一记录进行编辑，然后在将其解除锁定之前离开了一天，则在原始用户返回并完成其更新之前，其他用户将无法更新该记录。 因此，在使用悲观并发的情况下，通常会有一个超时，如果达到此值，则会取消锁定。 用于在用户完成订单过程时锁定特定座位位置的票证销售网站是悲观并发控制的一个示例。

## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>步骤 1：了解如何实现开放式并发

乐观并发控制的工作原理是确保正在更新或删除的记录的值与更新或删除进程启动时的值相同。 例如，当在可编辑 GridView 中单击 "编辑" 按钮时，将从数据库中读取记录的值并将其显示在文本框和其他 Web 控件中。 这些原始值由 GridView 保存。 稍后，在用户进行更改并单击 "更新" 按钮后，原始值和新值将发送到业务逻辑层，然后再发送到数据访问层。 如果用户开始编辑的原始值与数据库中仍有的值相同，则数据访问层必须发出一条 SQL 语句，该语句将仅更新记录。 图2描绘了此事件序列。

[![更新或删除成功，则原始值必须等于当前数据库值](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**图 2**：要使更新或删除成功，原始值必须等于当前数据库值（[单击即可查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image6.png)）

有多种方法可实现开放式并发（请参阅[Peter Bromberg](http://peterbromberg.net/)的[开放式并发更新逻辑](http://www.eggheadcafe.com/articles/20050719.asp)，简要了解一些选项）。 ADO.NET 类型化数据集提供一个实现，该实现只能用 checkbox 的勾选标记。 为类型化数据集中的 TableAdapter 启用乐观并发将增加 TableAdapter 的 `UPDATE` 和 `DELETE` 语句，以便在 `WHERE` 子句中包含所有原始值的比较。 例如，下面的 `UPDATE` 语句仅在以下情况下才会更新产品的名称和价格：当前数据库值等于在 GridView 中更新记录时最初检索到的值。 `@ProductName` 和 `@UnitPrice` 参数包含用户输入的新值，而 `@original_ProductName` 和 `@original_UnitPrice` 包含在单击 "编辑" 按钮时最初加载到 GridView 的值：

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> 为了便于阅读，此 `UPDATE` 语句已经过简化。 在实践中，`UnitPrice` 签入 `WHERE` 子句将更涉及，因为 `UnitPrice` 可以包含 `NULL` 并检查 `NULL = NULL` 是否始终返回 False （改为必须使用 `IS NULL`）。

除了使用其他基础 `UPDATE` 语句外，将 TableAdapter 配置为使用开放式并发还会修改其 DB 直接方法的签名。 从我们的第一个教程开始，[*创建数据访问层*](../introduction/creating-a-data-access-layer-cs.md)，数据库直接方法是接受标量值列表作为输入参数（而不是强类型化的 DataRow 或 DataTable 实例）的方法。 使用开放式并发时，DB direct `Update()` 和 `Delete()` 方法还包括原始值的输入参数。 此外，还必须更改使用批处理更新模式的 BLL 中的代码（接受 Datarow 的 `Update()` 方法重载，而不是标量值）。

不要将现有 DAL 的 Tableadapter 扩展为使用乐观并发（这将需要更改 BLL 以适应），而是创建一个名为 `NorthwindOptimisticConcurrency`的新的类型化数据集，我们将添加一个使用乐观并发的 `Products` TableAdapter。 接下来，我们将创建一个 `ProductsOptimisticConcurrencyBLL` 业务逻辑层类，该类具有相应修改以支持开放式并发 DAL。 在此基础上进行了布局后，就可以创建 ASP.NET 页面了。

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>步骤 2：创建支持开放式并发的数据访问层

若要创建新的类型化数据集，请右键单击 `App_Code` 文件夹中的 `DAL` 文件夹，然后添加一个名为 `NorthwindOptimisticConcurrency`的新数据集。 正如我们在第一个教程中看到的那样，这样做会将新的 TableAdapter 添加到类型化数据集，并自动启动 TableAdapter 配置向导。 在第一个屏幕中，系统将提示你使用 `Web.config`中的 `NORTHWNDConnectionString` 设置来指定要连接到的数据库-连接到同一 Northwind 数据库。

[![连接到同一 Northwind 数据库](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**图 3**：连接到同一 Northwind 数据库（[单击以查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image9.png)）

接下来，系统将提示您如何查询数据：通过即席 SQL 语句、新存储过程或现有存储过程。 由于我们在原始 DAL 中使用了即席 SQL 查询，因此请在此处使用此选项。

[![使用即席 SQL 语句指定要检索的数据](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**图 4**：使用即席 SQL 语句指定要检索的数据（[单击查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image12.png)）

在下面的屏幕中，输入用于检索产品信息的 SQL 查询。 让我们从原始 DAL 使用与 `Products` TableAdapter 完全相同的 SQL 查询，这将返回所有 `Product` 列以及产品的供应商和类别名称：

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]

[![使用来自原始 DAL 中的产品 TableAdapter 的相同 SQL 查询](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**图 5**：使用原始 DAL 中 `Products` TableAdapter 的相同 SQL 查询（[单击以查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image15.png)）

在转到下一屏幕之前，请单击 "高级选项" 按钮。 若要让 TableAdapter 使用乐观并发控制，只需选中 "使用开放式并发" 复选框即可。

[![通过选中 "使用开放式并发&quot; &quot;" 复选框来启用乐观并发控制](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**图 6**：通过选中 "使用开放式并发" 复选框启用乐观并发控制（[单击以查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image18.png)）

最后，指示 TableAdapter 应使用既填充 DataTable 还是返回 DataTable 的数据访问模式;还指示应创建 DB 直接方法。 将的方法名称从 "操作" 更改为 "GetProducts"，以反映我们在原始 DAL 中使用的命名约定。

[![让 TableAdapter 利用所有数据访问模式](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**图 7**：让 TableAdapter 利用所有数据访问模式（[单击查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image21.png)）

完成向导后，数据集设计器将包括强类型 `Products` DataTable 和 TableAdapter。 请花点时间将 DataTable 从 `Products` 重命名为 `ProductsOptimisticConcurrency`，可以通过右键单击 DataTable 的标题栏，然后从上下文菜单中选择 "重命名" 来执行此操作。

[![DataTable 和 TableAdapter 已添加到类型化数据集](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**图 8**：已将 DataTable 和 TableAdapter 添加到类型化数据集（[单击查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image24.png)）

若要查看在 `ProductsOptimisticConcurrency` TableAdapter （使用乐观并发）和产品 TableAdapter （不是）之间的 `UPDATE` 和 `DELETE` 查询之间的差异，请单击 TableAdapter 并中转到属性窗口。 在 "`DeleteCommand`" 和 "`UpdateCommand` 属性" `CommandText` 子属性 "子属性中，可以看到调用 DAL 的 update 或 delete 相关方法时发送到数据库的实际 SQL 语法。 对于 `ProductsOptimisticConcurrency` TableAdapter，使用的 `DELETE` 语句是：

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

而原始 DAL 中产品 TableAdapter 的 `DELETE` 语句则简单得多：

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

正如您所看到的，使用乐观并发的 TableAdapter 的 `DELETE` 语句中的 `WHERE` 子句包括：每个 `Product` 表的现有列值与上次填充 GridView （或 DetailsView 或 FormView）时的原始值之间的比较。 由于 `ProductID`、`ProductName`和 `Discontinued` 之外的所有字段都可以具有 `NULL` 值，因此，在 `NULL` 子句中正确比较 `WHERE` 值时将包含附加参数和检查。

在本教程中，我们不会向启用了开放式并发的数据集添加任何其他数据表，因为我们的 ASP.NET 页将只提供更新和删除产品信息。 但是，我们仍然需要将 `GetProductByProductID(productID)` 方法添加到 `ProductsOptimisticConcurrency` 的 TableAdapter 中。

为此，请右键单击 TableAdapter 的标题栏（`Fill` 和 `GetProducts` 方法名称上方的区域，然后从上下文菜单中选择 "添加查询"。 这将启动 "TableAdapter 查询配置向导"。 与 TableAdapter 的初始配置一样，选择使用即席 SQL 语句创建 `GetProductByProductID(productID)` 方法（请参阅图4）。 由于 `GetProductByProductID(productID)` 方法返回有关特定产品的信息，因此表示此查询是返回行的 `SELECT` 查询类型。

[![将查询类型标记为 &quot;选择返回行&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**图 9**：将查询类型标记为 "`SELECT` 返回行" （[单击查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image27.png)）

在下一个屏幕上，系统将提示你输入要使用的 SQL 查询，并预先加载 TableAdapter 的默认查询。 将现有查询扩充为包含子句 `WHERE ProductID = @ProductID`，如图10所示。

[![向预先加载的查询添加一个 WHERE 子句以返回特定产品记录](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**图 10**：将 `WHERE` 子句添加到预先加载的查询以返回特定产品记录（[单击查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image30.png)）

最后，将生成的方法名称更改为 `FillByProductID` 并 `GetProductByProductID`。

[![将方法重命名为 FillByProductID 和 GetProductByProductID](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**图 11**：将方法重命名为 "`FillByProductID`" 和 "`GetProductByProductID`" （[单击查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image33.png)）

完成此向导后，TableAdapter 现在包含用于检索数据的两个方法： `GetProducts()`，它将返回*所有*产品;和 `GetProductByProductID(productID)`，它返回指定的产品。

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>步骤 3：为启用了开放式并发的 DAL 创建业务逻辑层

我们的现有 `ProductsBLL` 类包含使用批更新和数据库直接模式的示例。 `AddProduct` 方法和 `UpdateProduct` 重载都使用批处理更新模式，并将 `ProductRow` 实例传入到 TableAdapter 的 Update 方法。 另一方面，`DeleteProduct` 方法使用 DB 直接模式，调用 TableAdapter 的 `Delete(productID)` 方法。

利用新的 `ProductsOptimisticConcurrency` TableAdapter，DB 直接方法现在还要求传递原始值。 例如，`Delete` 方法现在需要10个输入参数：原始 `ProductID`、`ProductName`、`SupplierID`、`CategoryID`、`QuantityPerUnit`、`UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、`ReorderLevel`和 `Discontinued`。 它在发送到数据库的 `DELETE` 语句 `WHERE` 子句中使用这些附加输入参数的值，如果数据库的当前值映射到原始值，则仅删除指定的记录。

虽然在批处理更新模式中使用的 TableAdapter `Update` 方法的方法签名尚未更改，但记录原始值和新值所需的代码具有。 因此，请不要使用现有的 `ProductsBLL` 类尝试使用启用了开放式并发的 DAL，而是创建一个新的业务逻辑层类来使用新的 DAL。

将名为 `ProductsOptimisticConcurrencyBLL` 的类添加到 `App_Code` 文件夹内的 `BLL` 文件夹中。

![将 ProductsOptimisticConcurrencyBLL 类添加到 BLL 文件夹](implementing-optimistic-concurrency-cs/_static/image34.png)

**图 12**：将 `ProductsOptimisticConcurrencyBLL` 类添加到 BLL 文件夹

接下来，将以下代码添加到 `ProductsOptimisticConcurrencyBLL` 类：

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

请注意类声明开头的 using `NorthwindOptimisticConcurrencyTableAdapters` 语句。 `NorthwindOptimisticConcurrencyTableAdapters` 命名空间包含 `ProductsOptimisticConcurrencyTableAdapter` 类，该类提供 DAL 的方法。 同样，在类声明之前，你会找到 `System.ComponentModel.DataObject` 特性，该特性指示 Visual Studio 将此类包含在 ObjectDataSource 向导的下拉列表中。

`ProductsOptimisticConcurrencyBLL`的 `Adapter` 属性提供对 `ProductsOptimisticConcurrencyTableAdapter` 类的实例的快速访问，并遵循我们的原始 BLL 类（`ProductsBLL`、`CategoriesBLL`等）中使用的模式。 最后，`GetProducts()` 方法只是向下调用 DAL 的 `GetProducts()` 方法，并返回一个 `ProductsOptimisticConcurrencyDataTable` 对象，该对象使用数据库中每个产品记录的 `ProductsOptimisticConcurrencyRow` 实例进行填充。

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>使用 DB 直接模式和乐观并发删除产品

对使用开放式并发的 DAL 使用 DB direct 模式时，必须将这些方法传递给新的和原始值。 对于删除，没有新值，因此只需传入原始值。 在 BLL 中，必须接受所有原始参数作为输入参数。 让我们在 `ProductsOptimisticConcurrencyBLL` 类中拥有 `DeleteProduct` 方法，使用 DB 直接方法。 这意味着此方法需要将所有十个产品数据字段作为输入参数，并将其传递给 DAL，如以下代码所示：

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

如果原始值（即，在用户单击 "删除" 按钮时，最后加载到 GridView 中的值）与数据库中的值不同，则 `WHERE` 子句不会与任何数据库记录匹配，也不会影响任何记录。 因此，TableAdapter 的 `Delete` 方法将返回 `0`，并且 BLL 的 `DeleteProduct` 方法将返回 `false`。

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>使用带有乐观并发的批处理更新模式更新产品

如前文所述，无论是否采用了开放式并发，批处理更新模式的 TableAdapter `Update` 方法都具有相同的方法签名。 也就是说，`Update` 方法需要 DataRow、Datarow 数组或类型化数据集。 没有用于指定原始值的其他输入参数。 这是可能的，因为 DataTable 跟踪其 DataRow 的原始值和修改后的值。 当 DAL 发出其 `UPDATE` 语句时，将用 DataRow 的原始值填充 `@original_ColumnName` 参数，而 `@ColumnName` 参数则用 DataRow 的已修改值填充。

在 `ProductsBLL` 类（它使用我们的原始非开放式并发 DAL）中，当使用批更新模式更新产品信息时，我们的代码将执行以下一系列事件：

1. 使用 TableAdapter 的 `GetProductByProductID(productID)` 方法将当前数据库产品信息读入 `ProductRow` 实例
2. 将新值分配到步骤1中的 `ProductRow` 实例
3. 调用 TableAdapter 的 `Update` 方法，并传入 `ProductRow` 实例

但是，这一顺序不能正确支持乐观并发，因为在步骤1中填充的 `ProductRow` 是直接从数据库填充的，这意味着，DataRow 使用的原始值是当前存在于数据库中的值，而不是在编辑过程开始时绑定到 GridView 的值。 相反，在使用启用了开放式并发的 DAL 时，需要改变 `UpdateProduct` 方法重载才能使用以下步骤：

1. 使用 TableAdapter 的 `GetProductByProductID(productID)` 方法将当前数据库产品信息读入 `ProductsOptimisticConcurrencyRow` 实例
2. 将*原始*值分配给步骤1中的 `ProductsOptimisticConcurrencyRow` 实例
3. 调用 `ProductsOptimisticConcurrencyRow` 实例的 `AcceptChanges()` 方法，该方法指示 DataRow 当前的值是 "原始" 值
4. 将*新*值分配给 `ProductsOptimisticConcurrencyRow` 实例
5. 调用 TableAdapter 的 `Update` 方法，并传入 `ProductsOptimisticConcurrencyRow` 实例

步骤1读取指定产品记录的所有当前数据库值。 此步骤在更新*所有*产品列的 `UpdateProduct` 重载中是多余的（因为在步骤2中覆盖了这些值，但在步骤2中覆盖了这些值），但这对于那些仅作为输入参数传入了列值子集的重载是必需的。 将原始值分配给 `ProductsOptimisticConcurrencyRow` 实例后，将调用 `AcceptChanges()` 方法，该方法将当前 DataRow 值标记为要在 `UPDATE` 语句的 `@original_ColumnName` 参数中使用的原始值。 接下来，将新参数值分配给 `ProductsOptimisticConcurrencyRow`，最后调用 `Update` 方法，并传入 DataRow。

下面的代码显示接受所有产品数据字段作为输入参数的 `UpdateProduct` 重载。 尽管此处未显示，但在本教程的下载中包含的 `ProductsOptimisticConcurrencyBLL` 类还包含一个 `UpdateProduct` 重载，该重载只接受产品的名称和价格作为输入参数。

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>步骤 4：将 ASP.NET 页中的原始值和新值传递到 BLL 方法

DAL 和 BLL 完成后，剩下的就是创建一个可利用内置于系统中的开放式并发逻辑的 ASP.NET 页面。 具体而言，数据 Web 控件（GridView、DetailsView 或 FormView）必须记住其原始值，并且 ObjectDataSource 必须将这两组值传递到业务逻辑层。 此外，必须将 ASP.NET 页配置为正常处理并发冲突。

首先打开 `EditInsertDelete` 文件夹中的 "`OptimisticConcurrency.aspx`" 页，然后将一个 GridView 添加到设计器中，将其 `ID` 属性设置为 "`ProductsGrid`"。 从 GridView 的智能标记中，选择创建名为 `ProductsOptimisticConcurrencyDataSource`的新 ObjectDataSource。 由于我们希望此 ObjectDataSource 使用支持开放式并发的 DAL，请将其配置为使用 `ProductsOptimisticConcurrencyBLL` 对象。

[![让 ObjectDataSource 使用 ProductsOptimisticConcurrencyBLL 对象](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**图 13**：让 ObjectDataSource 使用 `ProductsOptimisticConcurrencyBLL` 对象（[单击查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image37.png)）

从向导的下拉列表中选择 `GetProducts`、`UpdateProduct`和 `DeleteProduct` 方法。 对于 UpdateProduct 方法，请使用接受所有产品数据字段的重载。

## <a name="configuring-the-objectdatasource-controls-properties"></a>配置 ObjectDataSource 控件的属性

完成向导后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

如您所见，`DeleteParameters` 集合包含 `ProductsOptimisticConcurrencyBLL` 类的 `DeleteProduct` 方法中的10个输入参数的 `Parameter` 实例。 同样，`UpdateParameters` 集合包含 `UpdateProduct`中每个输入参数的 `Parameter` 实例。

对于之前涉及数据修改的这些教程，我们此时将删除该 ObjectDataSource 的 `OldValuesParameterFormatString` 属性，因为此属性指示 BLL 方法应传递旧的（或原始）值以及新的值。 此外，此属性值指示原始值的输入参数名称。 由于我们要将原始值传入到 BLL，因此*请勿删除此*属性。

> [!NOTE]
> `OldValuesParameterFormatString` 属性的值必须映射到 BLL 中预期原始值的输入参数名称。 由于我们将这些参数命名 `original_productName`、`original_supplierID`等，因此你可以将 `OldValuesParameterFormatString` 属性值保留为 `original_{0}`。 然而，如果 BLL 方法的输入参数的名称类似于 `old_productName`、`old_supplierID`等，则需要将 `OldValuesParameterFormatString` 属性更新为 `old_{0}`。

为了使 ObjectDataSource 正确地将原始值传递到 BLL 方法，需要进行一个最终的属性设置。 ObjectDataSource 具有可分配给[以下两个值之一](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx)的[ConflictDetection 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx)：

- `OverwriteChanges`-默认值;不向 BLL 方法的原始输入参数发送原始值
- `CompareAllValues`-会将原始值发送到 BLL 方法;使用开放式并发时选择此选项

请花点时间将 `ConflictDetection` 属性设置为 `CompareAllValues`。

## <a name="configuring-the-gridviews-properties-and-fields"></a>配置 GridView 的属性和字段

已正确配置 ObjectDataSource 的属性后，让我们来强调设置 GridView。 首先，由于我们希望 GridView 支持编辑和删除，请单击 GridView 智能标记中的 "启用编辑并启用删除" 复选框。 这会添加一个 CommandField，其 `ShowEditButton` 和 `ShowDeleteButton` 均设置为 `true`。

绑定到 `ProductsOptimisticConcurrencyDataSource` ObjectDataSource 时，GridView 包含产品的每个数据字段的字段。 尽管可以编辑此类 GridView，但用户体验是可接受的。 `CategoryID` 和 `SupplierID` BoundFields 将呈现为文本框，要求用户输入相应的类别和供应商作为 ID 号。 对于数字字段和无验证控件，都不会有任何格式，以确保已提供产品的名称，并确保单价、库存单位、按顺序排列的单位和重新排序级别值都是正确的数值，并且大于或等于为零。

如我们在向*编辑和插入界面添加验证控件*和*自定义数据修改接口*教程中所述，可以通过将 BoundFields 替换为 templatefield 来自定义用户界面。 我已通过以下方式修改了此 GridView 及其编辑界面：

- 删除 `ProductID`、`SupplierName`和 `CategoryName` BoundFields
- 将 `ProductName` BoundField 转换为 TemplateField 并添加 RequiredFieldValidation 控件。
- 将 `CategoryID` 和 `SupplierID` BoundFields 转换为 Templatefield，并将编辑界面调整为使用 DropDownLists 而不是文本框。 在这些 Templatefield 的 "`ItemTemplates`中，将显示 `CategoryName` 和 `SupplierName` 数据字段。
- 将 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` BoundFields 转换为 Templatefield 并添加 CompareValidator 控件。

由于我们已经检查了如何在前面的教程中完成这些任务，我只需在此处列出最终的声明性语法，并使实现保持为实践。

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

我们非常接近使用一个完整的示例。 不过，有几个微妙之处将会爬出并导致我们的问题。 此外，我们还需要一些接口，当发生并发冲突时，它会向用户发出警报。

> [!NOTE]
> 为了使数据 Web 控件正确地将原始值传递到 ObjectDataSource （随后将这些值传递到 BLL），将 GridView 的 `EnableViewState` 属性设置为 `true` （默认值）是非常重要的。 如果禁用视图状态，则在回发时原始值会丢失。

## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>将正确的原始值传递到 ObjectDataSource

配置 GridView 的方式有几个问题。 如果 ObjectDataSource 的 `ConflictDetection` 属性设置为 `CompareAllValues` （如下所示），则当 GridView （或 DetailsView 或 FormView）调用 ObjectDataSource 的 `Update()` 或 `Delete()` 方法时，ObjectDataSource 会尝试将 GridView 的原始值复制到其相应的 `Parameter` 实例中。 有关此过程的图形表示形式，请参阅图2。

具体而言，每次数据绑定到 GridView 时，将为 GridView 的原始值分配双向数据绑定语句中的值。 因此，必需的原始值全部通过双向数据绑定来捕获，并以可转换格式提供。

要了解这一点很重要，请花点时间访问浏览器中的页面。 按照预期，GridView 使用最左侧列中的 "编辑" 和 "删除" 按钮列出了每个产品。

[![在 GridView 中列出的产品](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**图 14**：产品在 GridView 中列出（[单击以查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image40.png)）

如果单击任何产品的 "删除" 按钮，则会引发 `FormatException`。

[![尝试删除 FormatException 中的任何产品结果](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**图 15**：尝试删除 `FormatException` 的任何产品结果（[单击查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image43.png)）

当 ObjectDataSource 尝试读取原始 `UnitPrice` 值时，将引发 `FormatException`。 由于 `ItemTemplate` 的 `UnitPrice` 格式为货币（`<%# Bind("UnitPrice", "{0:C}") %>`），因此它包含货币符号，如 $19.95。 当 ObjectDataSource 尝试将此字符串转换为 `decimal`时，会发生 `FormatException`。 若要避免此问题，我们有多种选择：

- 从 `ItemTemplate`中删除货币格式。 也就是说，不使用 `<%# Bind("UnitPrice", "{0:C}") %>`，只需使用 `<%# Bind("UnitPrice") %>`。 这种情况的缺点是价格不再经过格式化。
- 显示 `UnitPrice` 在 `ItemTemplate`中格式化为货币的格式，但使用 `Eval` 关键字实现此目的。 请记住，`Eval` 执行单向数据绑定。 我们仍需要为原始值提供 `UnitPrice` 值，因此，在 `ItemTemplate`中仍需要一个双向 databinding 语句，但这可以放置在 `Visible` 属性设置为 `false`的标签 Web 控件中。 可以在 ItemTemplate 中使用以下标记：

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- 使用 `<%# Bind("UnitPrice") %>`从 `ItemTemplate`中删除货币格式。 在 GridView 的 `RowDataBound` 事件处理程序中，以编程方式访问显示 `UnitPrice` 值的标签 Web 控件，并将其 `Text` 属性设置为格式化版本。
- 将 `UnitPrice` 设置为货币格式。 在 GridView 的 `RowDeleting` 事件处理程序中，用 `Decimal.Parse`将现有的原始 `UnitPrice` 值（$19.95）替换为实际的十进制值。 我们已了解如何在[*ASP.NET 页教程中处理 BLL 和 DAL 级别的异常*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)中，在 `RowUpdating` 事件处理程序中实现类似的操作。

在我的示例中，我选择使用第二种方法，添加一个隐藏的标签 Web 控件，该控件的 `Text` 属性是绑定到未格式化的 `UnitPrice` 值的双向数据。

解决此问题后，请尝试再次单击任何产品的 "删除" 按钮。 这次，当 ObjectDataSource 尝试调用 BLL 的 `UpdateProduct` 方法时，会收到 `InvalidOperationException`。

[![ObjectDataSource 找不到具有要发送的输入参数的方法](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**图 16**：ObjectDataSource 找不到具有要发送的输入参数的方法（[单击查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image46.png)）

查看异常消息，显然，ObjectDataSource 需要调用包含 `original_CategoryName` 和 `original_SupplierName` 输入参数的 BLL `DeleteProduct` 方法。 这是因为 `CategoryID` 和 `SupplierID` Templatefield 的 `ItemTemplate` 当前包含包含 "`CategoryName`" 和 "`SupplierName`" 数据字段的双向绑定语句。 相反，我们需要包含具有 `CategoryID` 和 `SupplierID` 数据字段的 `Bind` 语句。 若要实现此目的，请将现有 Bind 语句替换为 `Eval` 语句，然后添加隐藏的标签控件，这些控件的 `Text` 属性将绑定到 `CategoryID`，并使用双向数据绑定 `SupplierID` 数据字段，如下所示：

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

进行这些更改后，我们现在可以成功删除和编辑产品信息！ 在步骤5中，我们将介绍如何验证是否检测到了并发冲突。 但现在，请花几分钟时间来尝试更新和删除一些记录，以确保单个用户的更新和删除操作按预期运行。

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>步骤 5：测试开放式并发支持

为了验证是否检测到并发冲突（而不是导致数据被盲目覆盖），需要在此页上打开两个浏览器窗口。 在两个浏览器实例中，单击 "Chai" 的 "编辑" 按钮。 然后，只需在其中一个浏览器中，将名称更改为 "Chai 茶" 并单击 "更新"。 更新应成功并将 GridView 返回到其预编辑状态，并将 "Chai 茶" 作为新产品名称。

但在另一个浏览器窗口实例中，"产品名称" 文本框仍显示 "Chai"。 在第二个浏览器窗口中，将 `UnitPrice` 更新为 `25.00`。 如果不使用乐观并发支持，则在第二个浏览器实例中单击 "更新" 会将产品名称更改回 "Chai"，从而覆盖第一个浏览器实例所做的更改。 但在使用了开放式并发的情况下，在第二个浏览器实例中单击 "更新" 按钮会导致[system.data.dbconcurrencyexception](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)。

[![检测到并发冲突时，将引发 System.data.dbconcurrencyexception](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**图 17**：如果检测到并发冲突，则会引发 `DBConcurrencyException` （[单击查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image49.png)）

仅当使用 DAL 的批处理更新模式时，才会引发 `DBConcurrencyException`。 DB 直接模式不会引发异常，它仅指示没有行受到影响。 为了说明这一点，将浏览器实例的 GridView 返回到其预编辑状态。 接下来，在第一个浏览器实例中单击 "编辑" 按钮，然后将产品名称从 "Chai 茶" 改回 "Chai"，然后单击 "更新"。 在第二个浏览器窗口中，单击 "Chai" 的 "删除" 按钮。

单击 "删除" 后，该页面回发，GridView 会调用 ObjectDataSource 的 `Delete()` 方法，而 ObjectDataSource 会向下调用 `ProductsOptimisticConcurrencyBLL` 类的 `DeleteProduct` 方法，同时传递原始值。 第二个浏览器实例的原始 `ProductName` 值为 "Chai 茶"，此值与数据库中的当前 `ProductName` 值不匹配。 因此，对数据库发出的 `DELETE` 语句会影响零行，因为 `WHERE` 子句所满足的数据库中不存在任何记录。 `DeleteProduct` 方法返回 `false`，并且 ObjectDataSource 的数据将重新绑定到 GridView。

从最终用户的角度来看，在第二个浏览器窗口中单击 "Chai 茶" 的 "删除" 按钮会使屏幕闪烁，而在返回后，该产品仍在那里，但现在它作为 "Chai" （第一个浏览器所做的产品名称更改）列出。实例）。 如果用户再次单击 "删除" 按钮，则 Delete 将会成功，因为 GridView 的原始 `ProductName` 值（"Chai"）现在与数据库中的值相匹配。

在这两种情况下，用户体验远远不理想。 在使用批更新模式时，我们显然不希望向用户显示 `DBConcurrencyException` 异常的本质细节。 使用 DB 直接模式时的行为有些混乱，因为用户命令失败，但没有确切地指示原因。

若要解决这两个问题，可以在页面上创建 "标签 Web 控件"，以提供有关更新或删除失败原因的说明。 对于批处理更新模式，我们可以确定 GridView 的后期级别事件处理程序中是否出现 `DBConcurrencyException` 异常，并根据需要显示警告标签。 对于 DB 直接方法，我们可以检查 BLL 方法的返回值（如果一行受到影响 `false`，则 `true`），并根据需要显示信息性消息。

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>步骤 6：添加信息性消息，并在出现并发冲突时显示这些消息

发生并发冲突时，表现的行为取决于是否使用了 DAL 的批处理更新或 DB 直接模式。 本教程使用这两种模式，以及用于更新的批更新模式和用于删除的 DB 直接模式。 首先，让我们将两个标签 Web 控件添加到页面，说明在尝试删除或更新数据时出现并发冲突。 将 "标签" 控件的 `Visible` 和 `EnableViewState` 属性设置为 `false`;这将导致在每个页面上都隐藏它们，但这些特定页面访问除外，其 `Visible` 属性以编程方式设置为 `true`。

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

除了设置其 `Visible`、`EnabledViewState`和 `Text` 属性以外，我还将 `CssClass` 属性设置为 `Warning`，这会使标签的显示为大、红色、斜体、粗体。 已定义此 CSS `Warning` 类并将其添加到了样式。 css 返回了*与插入、更新和删除教程关联的事件*。

添加这些标签后，Visual Studio 中的设计器应类似于图18。

[已将两个标签控件添加到页面 ![](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**图 18**：已将两个标签控件添加到页面中（[单击以查看完全大小的图像](implementing-optimistic-concurrency-cs/_static/image52.png)）

使用这些 "标签" Web 控件即可完成检查如何确定发生了并发冲突的时间，此时可以将适当的标签 `Visible` 属性设置为 `true`，显示信息性消息。

## <a name="handling-concurrency-violations-when-updating"></a>在更新时处理并发冲突

首先，让我们看看如何在使用批更新模式时处理并发冲突。 由于与批处理更新模式发生的冲突将导致引发 `DBConcurrencyException` 异常，我们需要将代码添加到 ASP.NET 页，以确定在更新过程中是否发生了 `DBConcurrencyException` 异常。 如果是这样，则应向用户显示一条消息，说明未保存其更改，因为另一个用户在开始编辑记录和单击 "更新" 按钮之间修改了相同的数据。

正如我们在*ASP.NET 页教程中处理 BLL 和 DAL 级别的异常*中所述，可以在数据 Web 控件的后期级事件处理程序中检测并取消此类异常。 因此，我们需要为 GridView 的 `RowUpdated` 事件创建事件处理程序，该事件检查是否引发了 `DBConcurrencyException` 异常。 此事件处理程序将传递对在更新过程中引发的任何异常的引用，如下面的事件处理程序代码所示：

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

在出现 `DBConcurrencyException` 异常的情况下，此事件处理程序会显示 "`UpdateConflictMessage` 标签" 控件，并指示已处理异常。 使用此代码后，当更新记录发生并发冲突时，用户所做的更改将丢失，因为他们会在同一时间覆盖其他用户的修改。 特别是，GridView 返回到其预编辑状态并绑定到当前的数据库数据。 这会将 GridView 行与其他用户所做的更改（以前不可见）进行更新。 此外，`UpdateConflictMessage` 的标签控件将向用户解释刚发生的情况。 此事件序列在图19中详细说明。

[![用户更新在遇到并发冲突时丢失](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**图 19**：出现并发冲突时，用户的更新会丢失（[单击查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image55.png)）

> [!NOTE]
> 或者，可以通过将传入的 `GridViewUpdatedEventArgs` 对象的 `KeepInEditMode` 属性设置为 true，而不是将 GridView 返回到预编辑状态。 不过，如果采用这种方法，请确保将数据重新绑定到 GridView （通过调用其 `DataBind()` 方法），以便将其他用户的值加载到编辑界面。 使用本教程可供下载的代码在 `RowUpdated` 事件处理程序中注释掉了以下两行代码：只需取消注释这些代码行，在发生并发冲突后，GridView 仍处于编辑模式。

## <a name="responding-to-concurrency-violations-when-deleting"></a>删除时响应并发冲突

使用 DB 直接模式时，不会在出现并发冲突的情况下引发异常。 相反，database 语句不会影响任何记录，因为 WHERE 子句与任何记录都不匹配。 在 BLL 中创建的所有数据修改方法已经过设计，因此它们将返回一个布尔值，指示它们是否对一个记录进行了精确的影响。 因此，若要确定删除记录时是否发生了并发冲突，可以查看 BLL 的 `DeleteProduct` 方法的返回值。

可以通过传递到事件处理程序的 `ObjectDataSourceStatusEventArgs` 对象的 `ReturnValue` 属性，在 ObjectDataSource 的后期级别事件处理程序中检查 BLL 方法的返回值。 由于我们希望确定来自 `DeleteProduct` 方法的返回值，因此我们需要为 ObjectDataSource 的 `Deleted` 事件创建事件处理程序。 `ReturnValue` 属性的类型为 `object`，如果引发了异常，并且在该方法返回值之前中断了该方法，则可以 `null`。 因此，应该首先确保 `ReturnValue` 属性没有 `null` 并且是布尔值。 如果此检查通过，我们将显示 "`DeleteConflictMessage` 标签" 控件（如果 `ReturnValue` `false`）。 这可以通过使用以下代码来实现：

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

出现并发冲突时，将取消用户的删除请求。 将刷新 GridView，并显示该记录在用户加载页面和单击 "删除" 按钮时所发生的更改。 当这种冲突发生时，将显示 `DeleteConflictMessage` 标签，说明刚才发生的情况（请参阅图20）。

[![在遇到并发冲突时取消用户删除](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**图 20**：在出现并发冲突时取消用户删除（[单击查看完全大小的映像](implementing-optimistic-concurrency-cs/_static/image58.png)）

## <a name="summary"></a>Summary

在允许多个并发用户更新或删除数据的每个应用程序中都存在并发冲突的机会。 如果未考虑此类冲突，则当两个用户同时更新在上一次写入 "wins" 时获取的相同数据时，将覆盖其他用户的更改更改。 或者，开发人员可以实现乐观或悲观并发控制。 乐观并发控制假定并发冲突不常发生，只是不允许使用导致并发冲突的更新或删除命令。 悲观并发控制假设经常发生并发冲突，只是拒绝一个用户的 update 或 delete 命令是不可接受的。 使用悲观并发控制，更新记录涉及锁定，从而防止任何其他用户在锁定时修改或删除记录。

.NET 中的类型化数据集提供支持乐观并发控制的功能。 具体而言，发送到数据库的 `UPDATE` 和 `DELETE` 语句包含表的所有列，因此，仅当记录的当前数据与用户执行更新或删除时的原始数据匹配时，才会执行更新或删除。 将 DAL 配置为支持乐观并发后，需要更新 BLL 方法。 此外，必须对向下调用到 BLL 的 ASP.NET 页进行配置，以便 ObjectDataSource 从其数据 Web 控件检索原始值并将它们向下传递到 BLL。

正如本教程中所述，在 ASP.NET web 应用程序中实现开放式并发控制涉及更新 DAL 和 BLL，并在 ASP.NET 页中添加支持。 这一增加的工作是否是您的时间和精力的一项投入时间取决于您的应用程序。 如果你不经常有并发用户更新数据，或者更新数据的数据与其他用户不同，则并发控制不是一个关键问题。 然而，如果您的站点上的多个用户经常处理相同的数据，则并发控制可帮助防止一个用户的更新或删除无意中覆盖了另一个用户。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](customizing-the-data-modification-interface-cs.md)
> [下一页](adding-client-side-confirmation-when-deleting-cs.md)
