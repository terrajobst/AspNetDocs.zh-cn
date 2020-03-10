---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 使用类型化数据集的 Tableadapter 的现有存储过程（VB） |Microsoft Docs
author: rick-anderson
description: 在上一教程中，我们学习了如何使用 TableAdapter 向导来生成新的存储过程。 在本教程中，我们将了解如何将同一 TableAdapter 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 2da25f6a-757e-4e7b-a812-1575288d8f7a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: e35c3d6a98516a07f6119e6cb9dbeb99bc28fe33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78427124"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>使用适用于类型化数据集的 TableAdapter 的现有存储过程 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_VB.zip)或[下载 PDF](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial68vb1.pdf)

> 在上一教程中，我们学习了如何使用 TableAdapter 向导来生成新的存储过程。 在本教程中，我们将了解相同的 TableAdapter 向导如何处理现有的存储过程。 我们还将了解如何将新存储过程手动添加到数据库中。

## <a name="introduction"></a>简介

在[前面的教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)中，我们看到了如何将类型化数据集 tableadapter 配置为使用存储过程来访问数据，而不是即席 SQL 语句。 具体而言，我们已经检查了如何让 TableAdapter 向导自动创建这些存储过程。 将旧应用程序迁移到 ASP.NET 2.0 时，或围绕现有数据模型构建 ASP.NET 2.0 网站时，该数据库可能已包含我们所需的存储过程。 或者，您可能更愿意手动或通过用于自动生成存储过程的 TableAdapter 向导以外的其他工具来创建存储过程。

在本教程中，我们将介绍如何将 TableAdapter 配置为使用现有的存储过程。 由于 Northwind 数据库只包含一小部分内置存储过程，因此，我们还将了解通过 Visual Studio 环境将新存储过程手动添加到数据库时所需的步骤。 让我们开始吧！

> [!NOTE]
> 在[事务中包装数据库修改](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程中，我们向 TableAdapter 添加了一些方法，以支持事务（`BeginTransaction`、`CommitTransaction`等）。 或者，可以完全在存储过程中管理事务，这无需修改数据访问层代码。 在本教程中，我们将探讨用于在事务范围内执行存储过程语句的 T-sql 命令。

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>步骤1：将存储过程添加到 Northwind 数据库

使用 Visual Studio 可以轻松地向数据库添加新的存储过程。 在 Northwind 数据库中添加一个新的存储过程，该存储过程将返回 `Products` 表中具有特定 `CategoryID` 值的所有列。 在 "服务器资源管理器" 窗口中，展开 Northwind 数据库，以便显示其文件夹-数据库关系图、表、视图等。 如前面的教程中所述，"存储过程" 文件夹包含数据库的现有存储过程。 若要添加新的存储过程，只需右键单击 "存储过程" 文件夹，然后从上下文菜单中选择 "添加新存储过程" 选项。

[![右键单击 "存储过程" 文件夹并添加一个新的存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**图 1**：右键单击 "存储过程" 文件夹并添加一个新的存储过程（[单击以查看完全大小的映像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)）

如图1所示，选择 "添加新存储过程" 选项将在 Visual Studio 中打开一个脚本窗口，其中包含创建存储过程所需的 SQL 脚本的大纲。 我们的工作是增加此脚本并执行该脚本，此时将存储过程添加到数据库中。

输入以下脚本：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

此脚本在执行时将向名为 `Products_SelectByCategoryID`的 Northwind 数据库添加一个新的存储过程。 此存储过程接受一个输入参数（`@CategoryID``int`类型），并返回这些产品中具有匹配 `CategoryID` 值的所有字段。

若要执行此 `CREATE PROCEDURE` 脚本并将该存储过程添加到数据库，请单击工具栏中的 "保存" 图标，或按 Ctrl + S。 完成此操作后，存储过程文件夹将刷新，并显示新创建的存储过程。 此外，此窗口中的脚本会将个很微妙从 `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` 更改为 `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`。 `CREATE PROCEDURE` 将新的存储过程添加到数据库，`ALTER PROCEDURE` 更新现有存储过程。 由于脚本开始已更改为 `ALTER PROCEDURE`，因此更改存储过程输入参数或 SQL 语句并单击 "保存" 图标将用这些更改更新存储过程。

图2显示了 `Products_SelectByCategoryID` 存储过程保存后的 Visual Studio。

[![存储过程 Products_SelectByCategoryID 已添加到数据库中](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)

**图 2**：存储过程 `Products_SelectByCategoryID` 已添加到数据库中（[单击查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)）

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>步骤2：配置 TableAdapter 以使用现有存储过程

`Products_SelectByCategoryID` 存储过程已添加到数据库中，我们可以将数据访问层配置为在调用它的方法之一时使用此存储过程。 具体而言，我们会将 `GetProductsByCategoryID(<_i22_>categoryID)<!--_i22_-->` 方法添加到 `NorthwindWithSprocs` 类型化数据集中的 `ProductsTableAdapter`，该数据集调用我们刚刚创建的 `Products_SelectByCategoryID` 存储过程。

首先打开 `NorthwindWithSprocs` 数据集。 右键单击 `ProductsTableAdapter`，然后选择 "添加查询" 以启动 "TableAdapter 查询配置向导"。 在[前面的教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)中，我们选择使用 TableAdapter 为我们创建一个新的存储过程。 但对于本教程，我们希望将新的 TableAdapter 方法连接到现有的 `Products_SelectByCategoryID` 存储过程。 因此，请在向导的第一步中选择 "使用现有存储过程" 选项，然后单击 "下一步"。

[![选择 "使用现有存储过程" 选项](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)

**图 3**：选择 "使用现有存储过程" 选项（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)）

以下屏幕提供了一个用数据库存储过程填充的下拉列表。 选择存储过程将在左侧列出其输入参数，并在右侧列出返回的数据字段（如果有）。 从列表中选择 `Products_SelectByCategoryID` 存储过程，并单击 "下一步"。

[![选择 Products_SelectByCategoryID 存储过程](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)

**图 4**：选择 `Products_SelectByCategoryID` 存储过程（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)）

下一个屏幕会询问我们存储过程返回的数据类型，此处的答案决定了由 TableAdapter s 方法返回的类型。 例如，如果我们指示返回表格数据，则该方法将返回使用存储过程返回的记录填充的 `ProductsDataTable` 实例。 与此相反，如果我们指出此存储过程返回单个值，则 TableAdapter 将返回一个 `Object`，该对象被分配到存储过程返回的第一个记录的第一列中的值。

由于 `Products_SelectByCategoryID` 存储过程返回属于特定类别的所有产品，因此请选择第一个应答表格数据，并单击 "下一步"。

[![指示存储过程返回表格数据](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)

**图 5**：指示存储过程返回表格数据（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)）

剩下的就是指出要使用的方法模式，后跟这些方法的名称。 保留 "填充 DataTable" 和 "返回 DataTable" 选项，但将方法重命名为 "`FillByCategoryID`" 和 "`GetProductsByCategoryID`"。 然后单击 "下一步" 以查看向导将执行的任务的摘要。 如果一切正常，请单击 "完成"。

[![命名方法 FillByCategoryID 和 GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**图 6**： `FillByCategoryID` 和 `GetProductsByCategoryID` 命名方法（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png)）

> [!NOTE]
> 刚才创建的 TableAdapter 方法 `FillByCategoryID` 和 `GetProductsByCategoryID`需要 `Integer`类型的输入参数。 此输入参数值通过其 `@CategoryID` 参数传递到存储过程。 如果修改 `Products_SelectByCategory` 存储过程的参数，则还需要更新这些 TableAdapter 方法的参数。 如[前面的教程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)中所述，可以通过以下两种方式之一完成此操作：通过手动添加或删除参数集合中的参数或通过重新运行 TableAdapter 向导来执行此操作。

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>步骤3：将`GetProductsByCategoryID(categoryID)`方法添加到 BLL

`GetProductsByCategoryID` DAL 方法完成后，下一步就是在业务逻辑层中提供对此方法的访问。 打开 `ProductsBLLWithSprocs` 类文件，并添加以下方法：

[!code-vb[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.vb)]

此 BLL 方法只返回从 `ProductsTableAdapter` s `GetProductsByCategoryID` 方法返回的 `ProductsDataTable`。 `DataObjectMethodAttribute` 属性提供由 ObjectDataSource s 配置数据源向导使用的元数据。 具体而言，此方法将出现在 "选择选项卡 s" 下拉列表中。

## <a name="step-4-displaying-products-by-category"></a>步骤4：按类别显示产品

若要测试新添加的 `Products_SelectByCategoryID` 存储过程和相应的 DAL 和 BLL 方法，请创建包含 DropDownList 和 GridView 的 ASP.NET 页面。 DropDownList 将列出数据库中的所有类别，而 GridView 将显示属于所选类别的产品。

> [!NOTE]
> 在前面的教程中，我们使用 DropDownLists 创建了 master/detail 接口。 若要深入了解如何实现此类主/详细信息报表，请参阅[使用 DropDownList 的大纲/详细信息筛选](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)。

打开 `AdvancedDAL` 文件夹中的 "`ExistingSprocs.aspx`" 页，并将 "DropDownList" 从 "工具箱" 拖到设计器上。 将 DropDownList `ID` 属性设置为 "`Categories`"，并将其 `AutoPostBack` 属性设置为 "`True`"。 接下来，从其智能标记将 DropDownList 绑定到名为 `CategoriesDataSource`的新 ObjectDataSource。 配置 ObjectDataSource，使其从 `CategoriesBLL` 类 `GetCategories` 方法检索其数据。 将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![从 CategoriesBLL 类 s GetCategories 方法检索数据](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**图 7**：从 `CategoriesBLL` 类 `GetCategories` 方法检索数据（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)

**图 8**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)）

完成 ObjectDataSource 向导后，将 DropDownList 配置为显示 `CategoryName` 数据字段，并使用 `CategoryID` 字段作为每个 `ListItem`的 `Value`。

此时，DropDownList 和 ObjectDataSource 的声明性标记应类似于以下内容：

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.aspx)]

接下来，将一个 GridView 拖到设计器上，将其放在 DropDownList 下。 将 GridView `ID` 设置为 `ProductsByCategory`，并从其智能标记将其绑定到名为 `ProductsByCategoryDataSource`的新 ObjectDataSource。 将 `ProductsByCategoryDataSource` ObjectDataSource 配置为使用 `ProductsBLLWithSprocs` 类，使其能够使用 `GetProductsByCategoryID(categoryID)` 方法检索其数据。 由于此 GridView 仅用于显示数据，因此请将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"，然后单击 "下一步"。

[![将 ObjectDataSource 配置为使用 ProductsBLLWithSprocs 类](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)

**图 9**：将 ObjectDataSource 配置为使用 `ProductsBLLWithSprocs` 类（[单击以查看完全大小的映像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)）

[![从 GetProductsByCategoryID （类别 Id）方法检索数据](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)

**图 10**：从 `GetProductsByCategoryID(categoryID)` 方法检索数据（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)）

在 "选择" 选项卡中选择的方法需要参数，因此向导的最后一步会提示我们输入源参数。 设置要控制的 "参数源" 下拉列表，然后从 "ControlID" 下拉列表中选择 "`Categories`" 控件。 单击“完成”按钮以完成向导。

[![使用类别 DropDownList 作为类别 Id 参数的源](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**图 11**：使用 `Categories` DropDownList 作为 `categoryID` 参数的源（[单击查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png)）

完成 ObjectDataSource 向导后，Visual Studio 将为每个产品数据字段添加 BoundFields 和 CheckBoxField。 您可以根据需要随意自定义这些字段。

通过浏览器访问此页。 在访问该页面时，将选择 "饮料" 类别，并在网格中列出相应的产品。 如图12所示，将下拉列表更改为备用类别将导致回发，并使用新选定类别的产品重新加载网格。

[显示 "生成" 类别中的产品 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**图 12**：显示 "生成" 类别中的产品（[单击以查看完全尺寸的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)）

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>步骤5：在事务范围内包装存储过程语句

在[事务中包装数据库修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)教程中，我们讨论了在事务范围内执行一系列数据库修改语句的方法。 回忆一下，在事务中执行的修改要么全部成功，要么全部失败，从而保证原子性。 使用事务的方法包括：

- 使用 `System.Transactions` 命名空间中的类，
- 数据访问层使用 `SqlTransaction`等 ADO.NET 类，并
- 直接在存储过程中添加 T-sql transaction 命令

*事务教程中的包装数据库修改*使用 DAL 中的 ADO.NET 类。 本教程的其余部分将介绍如何使用存储过程中的 T-sql 命令来管理事务。

用于手动启动、提交和回滚事务的三个关键 SQL 命令分别分别 `BEGIN TRANSACTION`、`COMMIT TRANSACTION`和 `ROLLBACK TRANSACTION`。 与 ADO.NET 方法一样，使用存储过程中的事务时，需要应用以下模式：

1. 指示事务的开始。
2. 执行构成事务的 SQL 语句。
3. 如果步骤2中的任何一个语句出错，则回滚事务。
4. 如果步骤2中的所有语句都完成且没有错误，请提交该事务。

可使用以下模板在 T-sql 语法中实现此模式：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

该模板首先定义一个 `TRY...CATCH` 块，即一个构造 SQL Server 2005 的新构造。 与 Visual Basic 中 `Try...Catch` 块一样，SQL `TRY...CATCH` 块执行 `TRY` 块中的语句。 如果任何语句引发错误，控制将立即传输到 `CATCH` 块。

如果在执行构成事务的 SQL 语句时没有错误，`COMMIT TRANSACTION` 语句将提交更改并完成该事务。 但是，如果其中一个语句导致错误，则 `CATCH` 块中的 `ROLLBACK TRANSACTION` 会将数据库恢复到事务开始之前的状态。 该存储过程还使用[RAISERROR 命令](https://msdn.microsoft.com/library/ms178592.aspx)引发错误，这将导致应用程序中引发 `SqlException`。

> [!NOTE]
> 由于 `TRY...CATCH` 块是 SQL Server 2005 的新手，因此，如果使用的是较旧版本的 Microsoft SQL Server，则上述模板将不起作用。 如果使用的不是 SQL Server 2005，请参阅在将与其他版本的 SQL Server 一起使用的模板的[SQL Server 存储过程中管理事务](http://www.4guysfromrolla.com/webtech/080305-1.shtml)。

让我们看一个具体的示例。 `Categories` 和 `Products` 表之间存在外键约束，这意味着 `Products` 表中的每个 `CategoryID` 字段必须映射到 `CategoryID` 表中的 `Categories` 值。 任何违反此约束的操作（例如，尝试删除具有关联产品的类别）都将导致外键约束冲突。 若要验证这一点，请在使用二进制数据部分（`~/BinaryData/UpdatingAndDeleting.aspx`）重新访问更新和删除现有的二进制数据示例。 此页将列出系统中的每个类别以及 "编辑" 和 "删除" 按钮（见图13），但如果您尝试删除某个类别，其中包含关联的产品（如饮料），则删除由于外键约束冲突而失败（请参阅图14）。

[使用 "编辑" 和 "删除" 按钮在 GridView 中显示每个类别 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)

**图 13**：按 "编辑" 和 "删除" 按钮在 GridView 中显示每个类别（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)）

[![无法删除现有产品的类别](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)

**图 14**：无法删除现有产品的类别（[单击以查看完全大小的图像](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)）

不过，假设我们想要删除类别，而不考虑它们是否有关联的产品。 如果要删除包含产品的类别，假设我们还想要删除其现有产品（不过，另一个选项是将其产品 `CategoryID` 值设置为 `NULL`）。 可以通过 foreign key 约束的级联规则实现此功能。 另外，我们还可以创建接受 `@CategoryID` 输入参数的存储过程，并在调用它时显式删除所有关联的产品和指定的类别。

此类存储过程的第一次尝试可能如下所示：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

虽然这将会明确删除关联的产品和类别，但它不会在事务的涵盖下执行此操作。 假设 `Categories` 上有一些其他 foreign key 约束禁止删除特定 `@CategoryID` 值。 问题在于，在这种情况下，将在尝试删除类别之前删除所有产品。 最终结果是，对于这种类别，此存储过程将删除其所有产品，而类别仍保留，因为它仍在其他某个表中具有相关记录。

但是，如果存储过程已包装在事务范围内，则会在 `Categories`删除失败时回滚到 `Products` 表的删除。 以下存储过程脚本使用事务来确保两个 `DELETE` 语句之间的原子性：

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.sql)]

请花点时间将 `Categories_Delete` 存储过程添加到 Northwind 数据库。 有关将存储过程添加到数据库的说明，请参阅返回到步骤1。

## <a name="step-6-updating-thecategoriestableadapter"></a>步骤6：更新`CategoriesTableAdapter`

虽然已将 `Categories_Delete` 存储过程添加到数据库中，但 DAL 当前配置为使用即席 SQL 语句执行删除操作。 我们需要更新 `CategoriesTableAdapter`，并将其指示为改用 `Categories_Delete` 存储过程。

> [!NOTE]
> 在本教程的前面部分，我们使用的是 `NorthwindWithSprocs` 数据集。 但该数据集仅有一个实体 `ProductsDataTable`，我们需要使用类别。 因此，在本教程的剩余部分中，我讨论了引用 `Northwind` 数据集的数据访问层，这是我们在[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中的第一个创建的数据集。

打开 Northwind 数据集，选择 `CategoriesTableAdapter`，并中转到属性窗口。 属性窗口列出了 TableAdapter 使用的 `InsertCommand`、`UpdateCommand`、`DeleteCommand`和 `SelectCommand`，以及其名称和连接信息。 展开 "`DeleteCommand`" 属性以查看其详细信息。 如图15所示，`DeleteCommand` s `CommandType` 属性设置为 Text，这指示它将 `CommandText` 属性中的文本作为即席 SQL 查询发送。

![在设计器中选择 CategoriesTableAdapter，以在 "属性" 窗口中查看其属性。](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)

**图 15**：在设计器中选择 `CategoriesTableAdapter`，以在 "属性" 窗口中查看其属性

若要更改这些设置，请在属性窗口中选择（DeleteCommand）文本，然后从下拉列表中选择 "（新建）"。 这将清除 `CommandText`、`CommandType`和 `Parameters` 属性的设置。 接下来，将 `CommandType` 属性设置为 `StoredProcedure`，然后键入 `CommandText` （`dbo.Categories_Delete`）的存储过程的名称。 如果确保按此顺序输入属性-首先为 `CommandType`，然后 `CommandText`-Visual Studio 将自动填充参数集合。 如果未按此顺序输入这些属性，则必须通过 "参数集合编辑器" 手动添加参数。 在这两种情况下，在 "参数" 属性中单击省略号即可显示 "参数集合编辑器"，以验证是否进行了正确的参数设置更改（请参阅图16）。 如果在对话框中看不到任何参数，请手动添加 `@CategoryID` 参数（不需要添加 `@RETURN_VALUE` 参数）。

![确保参数设置正确](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**图 16**：确保参数设置正确

在对 DAL 进行更新后，删除类别将自动删除其所有关联的产品，并在事务的涵盖下执行此操作。 若要验证这一点，请返回到 "更新和删除现有的二进制数据" 页，然后单击其中一个类别的 "删除" 按钮。 只单击一次鼠标，就会删除类别及其所有关联的产品。

> [!NOTE]
> 在测试 `Categories_Delete` 存储过程之前，将删除多个产品以及所选的类别，因此，创建数据库的备份副本可能是明智的。 如果在 `App_Data`中使用 `NORTHWND.MDF` 数据库，只需关闭 Visual Studio，并将 `App_Data` 中的 MDF 和 LDF 文件复制到其他文件夹。 测试功能后，可以通过关闭 Visual Studio 并将 `App_Data` 中的当前 MDF 和 LDF 文件替换为备份副本来还原数据库。

## <a name="summary"></a>摘要

尽管 TableAdapter 向导会自动生成存储过程，但有时我们可能已创建了此类存储过程，或者想要使用其他工具手动创建这些存储过程。 为了满足此类情况，还可以将 TableAdapter 配置为指向现有的存储过程。 在本教程中，我们将介绍如何通过 Visual Studio 环境将存储过程手动添加到数据库，以及如何将 TableAdapter s 方法连接到这些存储过程。 我们还在存储过程中检查了用于启动、提交和回滚事务的 T-sql 命令和脚本模式。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Hilton Geisenow、S ren Jacob Lauritsen 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [下一页](updating-the-tableadapter-to-use-joins-vb.md)
