---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 为类型化数据集的 Tableadapter 创建新的存储过程（VB） |Microsoft Docs
author: rick-anderson
description: 在前面的教程中，我们在代码中创建了 SQL 语句，并将语句传递到要执行的数据库。 另一种方法是使用 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: a5a4a9ba-d18d-489a-a6b0-a3c26d6b0274
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: a7cc890038e5bb4eb61c7c3b808154c196ab2423
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78428708"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>新建适用于类型化数据集的 TableAdapter 的存储过程 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_VB.zip)或[下载 PDF](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial67vb1.pdf)

> 在前面的教程中，我们在代码中创建了 SQL 语句，并将语句传递到要执行的数据库。 另一种方法是使用存储过程，在数据库中预定义 SQL 语句。 在本教程中，我们将了解如何让 TableAdapter 向导为我们生成新的存储过程。

## <a name="introduction"></a>简介

这些教程的数据访问层（DAL）使用类型化数据集。 如[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中所述，类型化数据集由强类型的数据表和 tableadapter 组成。 数据表表示系统中的逻辑实体，同时 Tableadapter 接口与基础数据库一起执行数据访问。 这包括：用数据填充数据表，执行返回标量数据的查询，以及插入、更新和删除数据库中的记录。

Tableadapter 执行的 SQL 命令可以是即席 SQL 语句，如 `SELECT columnList FROM TableName`或存储过程。 体系结构中的 Tableadapter 使用即席 SQL 语句。 然而，许多开发人员和数据库管理员都倾向于即席 SQL 语句的存储过程，以提高安全性、可维护性和可更新性。 其他 ardently 更喜欢使用即席 SQL 语句来实现灵活性。 在我自己的工作中，我对即席 SQL 语句使用存储过程，但选择使用即席 SQL 语句来简化前面的教程。

定义 TableAdapter 或添加新方法时，TableAdapter s 向导使得创建新的存储过程或使用现有的存储过程与使用即席 SQL 语句一样简单。 在本教程中，我们将检查如何使 TableAdapter s 向导自动生成存储过程。 在下一教程中，我们将介绍如何配置 TableAdapter s 方法以使用现有存储过程或手动创建的存储过程。

> [!NOTE]
> 请参阅 "Howard" 的博客文章["尚不要使用存储过程？" 和 "](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/) [Frans Bouma](https://weblogs.asp.net/fbouma/) s" 博客条目[存储过程是错误的，M Kay？对于生动，请](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx)参阅存储过程和即席 SQL 的优缺点。

## <a name="stored-procedure-basics"></a>存储过程基本知识

函数是所有编程语言通用的构造。 函数是在调用函数时执行的语句的集合。 函数可以接受输入参数，还可以选择返回值。 *[存储过程](http://en.wikipedia.org/wiki/Stored_procedure)* 是与编程语言中的函数共享许多相似之处的数据库构造。 存储过程由一组在调用存储过程时执行的 T-sql 语句组成。 存储过程可以接受零个到多个输入参数，并可以从 `SELECT` 查询返回标量值、输出参数或最常见的结果集。

> [!NOTE]
> 存储过程经常称为 sprocs 或 Sp。

存储过程是使用[`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) t-sql 语句创建的。 例如，以下 T-sql 脚本将创建一个名为 `GetProductsByCategoryID` 的存储过程，该存储过程采用一个名为 `@CategoryID` 的参数，并返回 `UnitPrice`表中这些列的 `ProductID`、`ProductName`、`Discontinued` 和 `Products` 字段，它们具有匹配的 `CategoryID` 值：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

创建此存储过程后，可以使用以下语法来调用它：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.sql)]

> [!NOTE]
> 在下一教程中，我们将通过 Visual Studio IDE 来检查创建存储过程。 但对于本教程，我们将让 TableAdapter 向导自动生成存储过程。

除了只返回数据以外，存储过程通常还用于在单个事务的范围内执行多个数据库命令。 例如，名为 `DeleteCategory`的存储过程可能采用 `@CategoryID` 参数，并执行两个 `DELETE` 语句：第一个语句，删除相关产品，另一个语句删除指定的类别。 存储过程中的多个语句*不*会自动包装在事务中。 需要发出其他 T-sql 命令，以确保将存储过程多个命令视为原子操作。 在后续教程中，我们将了解如何将存储过程的命令包装在事务范围内。

在体系结构中使用存储过程时，数据访问层的方法将调用特定的存储过程，而不是发出即席 SQL 语句。 这将集中执行的 SQL 语句的位置（在数据库上），而不是在应用程序体系结构中定义它。 这种集中的功能可以更轻松地查找、分析和优化查询，并提供与数据库的使用位置和使用方式更清晰的图像。

有关存储过程基础知识的详细信息，请参阅本教程末尾的进一步阅读部分中的资源。

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>步骤1：创建高级数据访问层方案网页

在开始介绍如何使用存储过程创建 DAL 之前，首先请花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本网站中创建这些页面，接下来的几个教程。 首先添加一个名为 `AdvancedDAL`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![为高级数据访问层方案教程添加 ASP.NET 页](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**图 1**：添加高级数据访问层方案教程的 ASP.NET 页

与在其他文件夹中一样，`AdvancedDAL` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)）

最后，将这些页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在使用批量数据 `<siteMapNode>`之后添加以下标记：

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧的菜单中包括高级 DAL 方案教程中的项。

![站点映射现在包含高级 DAL 方案教程的条目](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)

**图 3**：站点地图现在包含高级 DAL 方案教程的条目

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>步骤2：配置 TableAdapter 以创建新的存储过程

若要演示如何创建使用存储过程而不是即席 SQL 语句的数据访问层，请在名为 `NorthwindWithSprocs.xsd`的 `~/App_Code/DAL` 文件夹中创建新的类型化数据集。 由于我们已在前面的教程中详细介绍了此过程，因此我们将通过此处的步骤快速完成。 如果在创建和配置类型化数据集时遇到问题，或者需要进一步的分步说明，请参阅[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程。

右键单击 "`DAL`" 文件夹，选择 "添加新项"，然后选择数据集模板（如图4所示），将一个新数据集添加到项目。

[![将新的类型化数据集添加到名为 NorthwindWithSprocs 的项目](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)

**图 4**：将新的类型化数据集添加到名为 `NorthwindWithSprocs.xsd` 的项目（[单击查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)）

这会创建新的类型化数据集，打开其设计器，创建新的 TableAdapter，并启动 TableAdapter 配置向导。 TableAdapter 配置向导的第一个步骤要求我们选择要使用的数据库。 应在下拉列表中列出 Northwind 数据库的连接字符串。 选择此，然后单击 "下一步"。

在下一个屏幕中，我们可以选择 TableAdapter 应如何访问数据库。 在前面的教程中，我们选择了第一个选项 "使用 SQL 语句"。 对于本教程，请选择第二个选项 "创建新存储过程"，然后单击 "下一步"。

[![指示 TableAdapter 创建新的存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)

**图 5**：指示 TableAdapter 创建新的存储过程（[单击以查看完全大小的映像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)）

就像使用即席 SQL 语句一样，在下面的步骤中，我们将要求提供用于 TableAdapter s 主查询的 `SELECT` 语句。 但是，TableAdapter s 向导将创建包含此 `SELECT` 查询的存储过程，而不是使用此处输入的 `SELECT` 语句直接执行即席查询。

对此 TableAdapter 使用以下 `SELECT` 查询：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

[![输入 SELECT 查询](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)

**图 6**：输入 `SELECT` 查询（[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)）

> [!NOTE]
> 上面的查询与 `Northwind` 类型化数据集中的 `ProductsTableAdapter` 的主查询略有不同。 请记住，`Northwind` 类型化数据集中的 `ProductsTableAdapter` 包括两个相关子查询，分别用于返回每个产品类别和供应商的类别名称和公司名称。 在即将[更新 TableAdapter 以使用 join](updating-the-tableadapter-to-use-joins-vb.md)教程中，我们将了解如何将此相关数据添加到此 TableAdapter。

请花点时间单击 "高级选项" 按钮。 从这里，我们可以指定该向导是否还应为 TableAdapter 生成 insert、update 和 delete 语句，是否使用乐观并发性，以及在插入和更新后是否应刷新数据表。 默认情况下，将选中 "生成 Insert、Update 和 Delete 语句" 选项。 保持选中状态。 对于本教程，请保留未选中 "使用开放式并发选项"。

当使用 TableAdapter 向导自动创建存储过程时，将出现 "刷新数据表" 选项。 不管是否选中此复选框，生成的 insert 和 update 存储过程都将检索刚刚插入的或仅更新的记录，如步骤3中所示。

![选中 "生成 Insert、Update 和 Delete 语句" 选项](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)

**图 7**：选中 "生成 Insert、Update 和 Delete 语句" 选项

> [!NOTE]
> 如果选中了 "使用开放式并发" 选项，则向导将向 `WHERE` 子句添加其他条件，以防止在其他字段中发生更改时更新数据。 有关使用 TableAdapter 的内置开放式并发控制功能的详细信息，请参阅[执行开放式并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程。

输入 `SELECT` 查询并确认是否选中了 "生成 Insert、Update 和 Delete 语句" 选项后，单击 "下一步"。 下一个屏幕（如图8所示）将提示输入向导为选择、插入、更新和删除数据而创建的存储过程的名称。 将这些存储过程的名称更改为 `Products_Select`、`Products_Insert`、`Products_Update`和 `Products_Delete`。

[![重命名存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**图 8**：重命名存储过程（[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png)）

若要查看 TableAdapter 向导将用于创建四个存储过程的 T-sql，请单击 "预览 SQL 脚本" 按钮。 从 "预览 SQL 脚本" 对话框中，您可以将脚本保存到文件或将其复制到剪贴板。

![预览用于生成存储过程的 SQL 脚本](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**图 9**：预览用于生成存储过程的 SQL 脚本

命名存储过程后，单击 "下一步" 以命名 TableAdapter 的相应方法。 就像使用即席 SQL 语句一样，可以创建填充现有 DataTable 或返回新 DataTable 的方法。 还可以指定 TableAdapter 是否应包括用于插入、更新和删除记录的 DB 直通模式。 选中所有三个复选框，但将 "返回 DataTable" 方法重命名为 `GetProducts` （如图10所示）。

[![命名方法 Fill 和 GetProducts](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)

**图 10**：将方法命名 `Fill` 和 `GetProducts` （[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)）

单击 "下一步" 查看向导将执行的步骤摘要。 通过单击 "完成" 按钮完成向导。 向导完成后，您将返回到数据集设计器，此时应包括 `ProductsDataTable`。

[![数据集的设计器将显示新添加的 ProductsDataTable](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)

**图 11**：数据集设计器显示新添加的 `ProductsDataTable` （[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)）

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>步骤3：检查新创建的存储过程

步骤2中使用的 TableAdapter 向导会自动创建用于选择、插入、更新和删除数据的存储过程。 这些存储过程可通过 Visual Studio 进行查看或修改，方法是转到服务器资源管理器并向下钻取到数据库的 "存储过程" 文件夹。 如图12所示，Northwind 数据库包含四个新的存储过程： `Products_Delete`、`Products_Insert`、`Products_Select`和 `Products_Update`。

![在第2步中创建的四个存储过程可在数据库的 "存储过程" 文件夹中找到](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)

**图 12**：在第2步中创建的四个存储过程可在数据库的 "存储过程" 文件夹中找到

> [!NOTE]
> 如果看不到 "服务器资源管理器"，请访问 "查看" 菜单，然后选择 "服务器资源管理器" 选项。 如果看不到从步骤2中添加的与产品相关的存储过程，请尝试右键单击 "存储过程" 文件夹，然后选择 "刷新"。

若要查看或修改存储过程，请在服务器资源管理器中双击其名称，或者右键单击该存储过程，然后选择 "打开"。 图13显示了打开的 `Products_Delete` 存储过程。

[可在 Visual Studio 中打开和修改 ![存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)

**图 13**：可以在 Visual Studio 中打开和修改存储过程（[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)）

`Products_Delete` 和 `Products_Select` 存储过程的内容都非常简单。 另一方面，`Products_Insert` 和 `Products_Update` 存储过程都一定要进行更仔细的检查，因为在其 `INSERT` 和 `UPDATE` 语句后它们都执行 `SELECT` 语句。 例如，以下 SQL 组成 `Products_Insert` 存储过程：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

该存储过程接受由 TableAdapter s 向导中指定的 `SELECT` 查询所返回 `Products` 列作为输入参数，并在 `INSERT` 语句中使用这些值。 使用 `INSERT` 语句后，`SELECT` 查询将用于返回新添加的记录的 `Products` 列值（包括 `ProductID`）。 当使用批更新模式添加新记录时，此刷新功能非常有用，因为它会自动将新添加的 `ProductRow` 实例 `ProductID` 属性与数据库分配的自动递增的值进行更新。

下面的代码演示了此功能。 它包含为 `NorthwindWithSprocs` 类型化数据集创建的 `ProductsTableAdapter` 和 `ProductsDataTable`。 通过创建一个 `ProductsRow` 实例，提供其值并调用 TableAdapter s `Update` 方法，并传入 `ProductsDataTable`，将新产品添加到数据库中。 在内部，TableAdapter s `Update` 方法枚举传入的 DataTable 中的 `ProductsRow` 实例（在本示例中，只有一个，我们刚刚添加了一个），并执行适当的 insert、update 或 delete 命令。 在这种情况下，将执行 `Products_Insert` 存储过程，该过程将向 `Products` 表中添加一条新记录，并返回新添加的记录的详细信息。 然后更新 `ProductsRow` 实例的 `ProductID` 值。 `Update` 方法完成后，可以通过 `ProductsRow` `ProductID` 属性访问新添加的记录的 `ProductID` 值。

[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.vb)]

`Products_Update` 存储过程类似地在其 `UPDATE` 语句后面包含 `SELECT` 语句。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample7.sql)]

请注意，此存储过程包含两个用于 `ProductID`的输入参数： `@Original_ProductID` 和 `@ProductID`。 此功能可用于可能更改主键的情况。 例如，在雇员数据库中，每个雇员记录可能使用员工的社会安全号码作为其主键。 若要更改现有员工的社会保障号，必须提供新的社会保险号和原始安全号码。 对于 `Products` 表，不需要此类功能，因为 `ProductID` 列为 `IDENTITY` 列，并且永远不应更改。 事实上，`Products_Update` 存储过程中的 `UPDATE` 语句不会将 `ProductID` 列包含在其列列表中。 因此，虽然在 `UPDATE` 语句 s `WHERE` 子句中使用 `@Original_ProductID`，但它对于 `Products` 表来说是多余的，并且可以被 `@ProductID` 参数替换。 修改存储过程的参数时，还会更新使用该存储过程的 TableAdapter 方法，这一点很重要。

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>步骤4：修改存储过程的参数和更新 TableAdapter

由于 `@Original_ProductID` 参数是多余的，因此让我们从 `Products_Update` 存储过程中删除它。 打开 `Products_Update` 存储过程，删除 `@Original_ProductID` 参数，并在 `UPDATE` 语句的 `WHERE` 子句中将从 `@Original_ProductID` 使用的参数名称更改为 `@ProductID`。 进行这些更改后，存储过程中的 T-sql 应该如下所示：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample8.sql)]

若要将这些更改保存到数据库，请单击工具栏中的 "保存" 图标或按 Ctrl + S。 此时，`Products_Update` 存储过程不需要 `@Original_ProductID` 输入参数，但 TableAdapter 配置为通过此类参数。 您可以通过在 "数据集设计器" 中选择 TableAdapter，转到属性窗口，然后单击 `UpdateCommand` s `Parameters` 集合中的省略号，来查看 TableAdapter 将发送到 `Products_Update` 存储过程的参数。 此时将打开图14中显示的 "参数集合编辑器" 对话框。

![参数集合编辑器列出了传递到 Products_Update 存储过程的参数](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)

**图 14**：参数集合编辑器列出了传递到 `Products_Update` 存储过程的参数

只需从成员列表中选择 "`@Original_ProductID`" 参数并单击 "删除" 按钮，即可从此处删除此参数。

或者，您可以通过右键单击设计器中的 TableAdapter，然后选择 "配置"，来刷新用于所有方法的参数。 这会显示 "TableAdapter 配置向导"，其中列出了用于选择、插入、更新和删除的存储过程，以及存储过程期望接收的参数。 如果单击 "更新" 下拉列表，则可以看到 `Products_Update` 的存储过程所需的输入参数，这些参数现在不再包括 `@Original_ProductID` （参见图15）。 只需单击 "完成" 即可自动更新由 TableAdapter 使用的参数集合。

[![你也可以使用 TableAdapter s 配置向导来刷新其方法参数集合](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**图 15**：你也可以使用 TableAdapter s 配置向导来刷新其方法参数集合（[单击查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png)）

## <a name="step-5-adding-additional-tableadapter-methods"></a>步骤5：添加其他 TableAdapter 方法

如步骤2所示，创建新的 TableAdapter 时，可以轻松地自动生成相应的存储过程。 向 TableAdapter 添加其他方法时，情况也是如此。 为了说明这一点，让我们将 `GetProductByProductID(productID)` 方法添加到步骤2中创建的 `ProductsTableAdapter`。 此方法会将 `ProductID` 值作为输入，并返回有关指定产品的详细信息。

首先右键单击 "TableAdapter"，然后从上下文菜单中选择 "添加查询"。

![向 TableAdapter 添加新查询](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**图 16**：向 TableAdapter 添加新查询

这将启动 "TableAdapter 查询配置向导"，该向导将首先提示 TableAdapter 应如何访问数据库。 若要创建新的存储过程，请选择 "创建新存储过程" 选项，然后单击 "下一步"。

[![选择 "创建新存储过程" 选项](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)

**图 17**：选择 "创建新存储过程" 选项（[单击以查看完全大小的映像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)）

下一个屏幕会要求我们确定要执行的查询类型，是返回一组行还是单个标量值，或者执行 `UPDATE`、`INSERT`或 `DELETE` 语句。 由于 `GetProductByProductID(productID)` 方法将返回一行，因此请保留选中 "返回行" 选项，然后单击 "下一步"。

[![选择 "选择返回行" 选项](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)

**图 18**：选择 "选择返回行" 选项（[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)）

下一屏幕将显示 TableAdapter s main query，其中只列出了存储过程的名称（`dbo.Products_Select`）。 将存储过程名称替换为以下 `SELECT` 语句，该语句将返回指定产品的所有产品字段：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample9.sql)]

[![使用 SELECT 查询替换存储过程名称](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)

**图 19**：使用 `SELECT` 查询替换存储过程名称（[单击查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)）

接下来的屏幕将要求你命名要创建的存储过程。 输入 `Products_SelectByProductID` 的名称，然后单击 "下一步"。

[![命名新存储过程 Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**图 20**：将新存储过程命名 `Products_SelectByProductID` （[单击以查看完全大小的映像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image46.png)）

向导的最后一步允许更改生成的方法名称，并指示是使用 "填充 DataTable" 模式还是返回 DataTable 模式，或同时返回这两种模式。 对于此方法，请将这两个选项保持选中状态，但将方法重命名为 `FillByProductID` 和 `GetProductByProductID`。 单击 "下一步" 以查看向导将执行的步骤的摘要，然后单击 "完成" 以完成向导。

[![重命名 TableAdapter s 方法到 FillByProductID 和 GetProductByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image47.png)

**图 21**：重命名 TableAdapter s 方法以便 `FillByProductID` 和 `GetProductByProductID` （[单击查看完全大小的映像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image49.png)）

完成该向导后，TableAdapter 有一个新的可用方法，`GetProductByProductID(productID)` 调用该方法时，将执行刚刚创建的 `Products_SelectByProductID` 存储过程。 通过深化到 "存储过程" 文件夹并打开 `Products_SelectByProductID` （如果看不到它，右键单击 "存储过程" 文件夹并选择 "刷新"），从服务器资源管理器查看此新存储过程。

请注意，`SelectByProductID` 存储过程采用 `@ProductID` 输入参数，并执行在向导中输入的 `SELECT` 语句。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>步骤6：创建业务逻辑层类

在整个教程系列中，我们已 strived 维护一个分层体系结构，在该体系结构中，表示层已对业务逻辑层（BLL）进行所有调用。 为了遵守这一设计决策，首先需要为新的类型化数据集创建一个 BLL 类，然后才能从表示层访问产品数据。

在 `~/App_Code/BLL` 文件夹中创建一个名为 `ProductsBLLWithSprocs.vb` 的新类文件，并向其中添加以下代码：

[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample11.vb)]

此类模拟前面教程中的 `ProductsBLL` 类语义，但使用 `NorthwindWithSprocs` 数据集中的 `ProductsTableAdapter` 和 `ProductsDataTable` 对象。 例如，`ProductsBLLWithSprocs` 类使用 `Imports NorthwindWithSprocsTableAdapters`，而不是将类文件开头的 `Imports NorthwindTableAdapters` 语句作为 `ProductsBLL`。 同样，此类中使用的 `ProductsDataTable` 和 `ProductsRow` 对象都带有 `NorthwindWithSprocs` 命名空间的前缀。 `ProductsBLLWithSprocs` 类提供两种数据访问方法： `GetProducts` 和 `GetProductByProductID`，以及添加、更新和删除单个产品实例的方法。

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>步骤7：使用表示层中的`NorthwindWithSprocs`数据集

此时，我们已创建一个使用存储过程访问和修改基础数据库数据的 DAL。 我们还构建了一个基本的 BLL，其中包含用于检索所有产品或特定产品的方法，以及用于添加、更新和删除产品的方法。 若要将本教程舍入，请创建一个 ASP.NET 页，该页使用 BLL s `ProductsBLLWithSprocs` 类来显示、更新和删除记录。

打开 `AdvancedDAL` 文件夹中的 "`NewSprocs.aspx`" 页，然后将 GridView 从工具箱拖动到设计器上，并将其命名为 "`Products`"。 从 GridView s 智能标记中，选择将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsBLLWithSprocs` 类，如图22所示。

[![将 ObjectDataSource 配置为使用 ProductsBLLWithSprocs 类](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image50.png)

**图 22**：将 ObjectDataSource 配置为使用 `ProductsBLLWithSprocs` 类（[单击查看完全大小的映像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image52.png)）

"选择" 选项卡中的下拉列表具有两个选项： "`GetProducts`" 和 "`GetProductByProductID`"。 由于我们要显示 GridView 中的所有产品，因此请选择 `GetProducts` 方法。 "更新"、"插入" 和 "删除" 选项卡中的下拉列表仅有一种方法。 确保每个下拉列表都选择了相应的方法，然后单击 "完成"。

在 ObjectDataSource 向导完成后，Visual Studio 会将 BoundFields 和 CheckBoxField 添加到 "产品数据" 字段的 GridView。 通过选中智能标记中提供的 "启用编辑和启用删除" 选项，打开 GridView 的内置编辑和删除功能。

[![页面包含启用了编辑和删除支持的 GridView](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image53.png)

**图 23**：页面包含启用了编辑和删除支持的 GridView （[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image55.png)）

如前面的教程中所述，在完成 ObjectDataSource 向导时，Visual Studio 会将 `OldValuesParameterFormatString` 属性设置为原始\_{0}。 此操作需要恢复为其默认值 {0}，以使数据修改功能能够正常运行，前提是 BLL 中方法所需的参数。 因此，请务必将 `OldValuesParameterFormatString` 属性设置为 {0} 或从声明性语法中删除属性。

完成 "配置数据源" 向导后，在 GridView 中启用编辑和删除支持，并将 ObjectDataSource `OldValuesParameterFormatString` 属性返回到其默认值后，页面的声明性标记应如下所示：

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample12.aspx)]

此时，我们可以通过自定义编辑界面以包括验证，将 `CategoryID` 和 `SupplierID` 列呈现为 DropDownLists 等，来整理 GridView。 我们还可以将客户端确认添加到 "删除" 按钮，并建议你花些时间来实现这些增强功能。 由于前面的教程中介绍了这些主题，因此我们不会在此处再次介绍这些主题。

无论您是否增强 GridView，都可以在浏览器中测试页面的核心功能。 如图24所示，该页面列出了 GridView 中的产品，该产品提供按行编辑和删除功能。

[![可以从 GridView 查看、编辑和删除产品](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image56.png)

**图 24**：可以从 GridView 查看、编辑和删除产品（[单击以查看完全大小的图像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image58.png)）

## <a name="summary"></a>摘要

类型化数据集中的 Tableadapter 可以使用即席 SQL 语句或存储过程来访问数据库中的数据。 使用存储过程时，可以使用现有存储过程，也可以指示使用 TableAdapter 向导根据 `SELECT` 查询创建新的存储过程。 在本教程中，我们探讨了如何为我们自动创建存储过程。

尽管自动生成的存储过程有助于节省时间，但在某些情况下，该向导创建的存储过程不会与我们自己创建的存储过程一致。 例如，`Products_Update` 存储过程，即使 `@Original_ProductID` 参数是多余的，也应同时需要 `@Original_ProductID` 和 `@ProductID` 输入参数。

在许多情况下，可能已创建了存储过程，或者我们需要手动生成它们，以便对存储过程的命令进行更精细的控制。 在任一情况下，我们都需要指示 TableAdapter 使用现有存储过程作为其方法。 下一教程将介绍如何实现此目的。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [创建和维护存储过程](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [从存储过程中检索标量数据](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [SQL Server 存储过程基础知识](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [存储过程：概述](http://www.sqlteam.com/item.asp?ItemID=563)
- [编写存储过程](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Geisenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
> [下一页](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
