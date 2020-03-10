---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
title: 包装事务内的数据库修改（C#） |Microsoft Docs
author: rick-anderson
description: 本教程是第四个教程，其中介绍了如何更新、删除和插入批数据。 在本教程中，我们将了解数据库事务如何允许 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: b45fede3-c53a-4ea1-824b-20200808dbae
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
msc.type: authoredcontent
ms.openlocfilehash: da69e466a5b506b869dc8fc0624f3e6a479199a8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489296"
---
# <a name="wrapping-database-modifications-within-a-transaction-c"></a>包装事务内的数据库修改 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_CS.zip)或[下载 PDF](wrapping-database-modifications-within-a-transaction-cs/_static/datatutorial63cs1.pdf)

> 本教程是第四个教程，其中介绍了如何更新、删除和插入批数据。 在本教程中，我们将了解数据库事务如何允许以原子操作的形式执行批处理修改，这可确保所有步骤均成功或所有步骤均失败。

## <a name="introduction"></a>简介

正如我们从有关[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程的概述开始，GridView 为行级编辑和删除提供内置支持。 只需单击几下鼠标，就能创建一个丰富的数据修改接口，而无需编写代码行，只要您是每行都有编辑和删除的内容。 但是，在某些情况下，这种情况并不充分，我们需要为用户提供编辑或删除一批记录的能力。

例如，大多数基于 web 的电子邮件客户端使用网格来列出每个消息，其中每行都包含一个复选框以及电子邮件信息（主题、发件人等）。 此接口允许用户通过选中并单击 "删除选择的消息" 按钮来删除多个消息。 批处理编辑接口非常适合于用户经常编辑多个不同记录的情况。 除了强制用户单击 "编辑"、进行更改，然后单击每个需要修改的记录的 "更新" 时，批处理编辑界面都会使用其编辑界面呈现每一行。 用户可以快速修改需要更改的行集，然后通过单击 "全部更新" 按钮保存这些更改。 本教程将介绍如何创建用于插入、编辑和删除批数据的接口。

执行批处理操作时，很重要的一点是，确定批处理中的某些操作在其他操作失败时是否可以成功。 假设有一个批处理删除接口-如果成功删除第一个选定记录，则会发生什么情况，但第二个记录由于外键约束冲突而失败。 第一条记录是否应该回滚，或者第一条记录是否可接受？

如果希望批处理操作被视为[原子操作](http://en.wikipedia.org/wiki/Atomic_operation)，其中无论是成功完成的所有步骤还是所有步骤均失败，则需要对数据访问层进行扩充以支持[数据库事务](http://en.wikipedia.org/wiki/Database_transaction)。 数据库事务可保证在事务的涵盖下执行的一组 `INSERT`、`UPDATE`和 `DELETE` 语句的原子性，这是大多数新式数据库系统都支持的一项功能。

在本教程中，我们将介绍如何扩展 DAL 以使用数据库事务。 后续教程将检查如何实现用于批量插入、更新和删除接口的网页。 让我们开始吧！

> [!NOTE]
> 在批处理事务中修改数据时，并不总是需要原子性。 在某些情况下，可能可以接受某些数据修改，但在同一批次中，其他人会失败，例如从基于 web 的电子邮件客户端中删除一组电子邮件。 如果在删除过程中出现数据库错误，则很可能会在不错误的情况下处理这些记录。 在这种情况下，不需要修改 DAL 以支持数据库事务。 但还有其他批处理操作方案，其中的原子性至关重要。 当客户将其资金从一个银行帐户移到另一个银行帐户时，必须执行两项操作：必须从第一个帐户中扣除资金，然后再将其添加到第二个帐户。 虽然银行可能不介意第一步成功完成，但第二步却失败，但其客户理解。 我建议您完成本教程并实现对 DAL 的增强，以支持数据库事务，即使您不打算在批处理中将它们用于插入、更新和删除接口，我们将在以下三个教程中构建。

## <a name="an-overview-of-transactions"></a>事务概述

大多数数据库都支持*事务*，使多个数据库命令可以分组为一个逻辑工作单元。 构成事务的数据库命令保证是原子的，这意味着所有命令都将失败或全部成功。

通常，使用以下模式通过 SQL 语句实现事务：

1. 指示事务的开始。
2. 执行构成事务的 SQL 语句。
3. 如果步骤2中的某个语句出错，则回滚事务。
4. 如果步骤2中的所有语句都完成且没有错误，请提交该事务。

在编写 SQL 脚本或创建存储过程时，或者通过编程方式使用[`System.Transactions` 命名空间](https://msdn.microsoft.com/library/system.transactions.aspx)中的类时，可以手动输入用于创建、提交和回滚事务的 SQL 语句。 在本教程中，我们将仅使用 ADO.NET 检查管理事务。 在将来的教程中，我们将介绍如何在数据访问层中使用存储过程，此时我们将浏览用于创建、回滚和提交事务的 SQL 语句。 同时，有关详细信息，请参阅在[SQL Server 存储过程中管理事务](http://www.4guysfromrolla.com/webtech/080305-1.shtml)。

> [!NOTE]
> 使用 `System.Transactions` 命名空间中的[`TransactionScope` 类](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx)，开发人员可以以编程方式包装事务范围内的一系列语句，并包括对涉及多个源的复杂事务的支持，例如两个不同的数据库，甚至异类类型的数据存储，如 Microsoft SQL Server 数据库、Oracle 数据库和 Web 服务。 我决定在此教程中使用 ADO.NET 事务，而不是 `TransactionScope` 类，因为 ADO.NET 更特定于数据库事务，在许多情况下，消耗的资源要少得多。 此外，在某些情况下，`TransactionScope` 类使用 Microsoft 分布式事务处理协调器（MSDTC）。 MSDTC 的配置、实现和性能问题使其成为一个专门的高级主题，并超出了这些教程的范围。

在 ADO.NET 中使用 SqlClient 提供程序时，将通过调用[`SqlConnection` 类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)s [`BeginTransaction` 方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)来启动事务，该方法返回[`SqlTransaction` 对象](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)。 构成事务的数据修改语句置于 `try...catch` 块内。 如果 `try` 块中的语句发生错误，则执行会传输到 `catch` 块，在这种情况下，可通过 `SqlTransaction` 对象[`Rollback` 方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)回滚事务。 如果所有语句都成功完成，则在 `try` 块末尾调用 `SqlTransaction` 对象 s [`Commit` 方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx)将提交该事务。 下面的代码段演示了此模式。 有关将事务与 ADO.NET 结合使用的其他语法和示例，请参阅使用[事务维护数据库一致性](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample1.cs)]

默认情况下，类型化数据集中的 Tableadapter 不使用事务。 若要为事务提供支持，我们需要增加 TableAdapter 类，使其包含使用以上模式在事务范围内执行一系列数据修改语句的其他方法。 在步骤2中，我们将了解如何使用分部类添加这些方法。

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>步骤1：创建使用批处理数据网页

在开始探索如何扩充 DAL 以支持数据库事务之前，首先请花一些时间来创建本教程所需的 ASP.NET 网页以及下面的三个网页。 首先添加一个名为 `BatchData` 的新文件夹，然后添加以下 ASP.NET 页面，将每个页面与 `Site.master` 母版页相关联。

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![为 SqlDataSource 相关教程添加 ASP.NET 页](wrapping-database-modifications-within-a-transaction-cs/_static/image1.gif)

**图 1**：添加 SqlDataSource 相关教程的 ASP.NET 页

对于其他文件夹，`Default.aspx` 将使用 `SectionLevelTutorialListing.ascx` 用户控件列出其部分中的教程。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](wrapping-database-modifications-within-a-transaction-cs/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image1.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](wrapping-database-modifications-within-a-transaction-cs/_static/image2.png)）

最后，将这四个页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在自定义站点地图之后添加以下标记 `<siteMapNode>`：

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample2.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧的菜单包含用于使用批量数据教程的项。

![站点映射现在包含用于使用批量数据教程的条目](wrapping-database-modifications-within-a-transaction-cs/_static/image3.gif)

**图 3**：站点地图现在包含用于使用批量数据教程的条目

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>步骤2：更新数据访问层以支持数据库事务

正如我们在第一个教程中所述，[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)，DAL 中的类型化数据集由数据表和 tableadapter 组成。 数据表保存数据时，Tableadapter 提供了将数据从数据库读入到数据表中的功能，用于通过对数据表的更改来更新数据库等。 回忆一下，Tableadapter 提供了两种用于更新数据的模式，我称之为批更新和数据库直通。 使用批处理更新模式时，TableAdapter 会传递到 Datarow 的数据集、DataTable 或集合。 枚举此数据，并对每个已插入、已修改或已删除的行执行 `InsertCommand`、`UpdateCommand`或 `DeleteCommand`。 使用 DB 直通模式时，TableAdapter 会传递插入、更新或删除单个记录所需的列值。 然后，DB 直接模式方法使用传入的值执行适当的 `InsertCommand`、`UpdateCommand`或 `DeleteCommand` 语句。

无论使用何种更新模式，Tableadapter 自动生成的方法不使用事务。 默认情况下，由 TableAdapter 执行的每个插入、更新或删除操作都被视为一个单独的操作。 例如，假设 BLL 中的某些代码使用 DB 直通模式将十条记录插入到数据库中。 此代码将调用 TableAdapter s `Insert` 方法十次。 如果前5个插入成功，但第六个插入导致了异常，则前5个插入的记录将保留在数据库中。 同样，如果使用批处理更新模式来对 DataTable 中已插入的、已修改的和已删除的行执行插入、更新和删除操作，则如果前几个修改已成功，但出现错误，则这些之前的修改将"已完成" 将保留在数据库中。

在某些情况下，我们希望确保一系列修改的原子性。 若要实现此目的，我们必须通过添加新方法来手动扩展 TableAdapter，该方法在事务的伞下执行 `InsertCommand`、`UpdateCommand`和 `DeleteCommand`。 在[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)中，我们介绍了如何使用[分部类](http://en.wikipedia.org/wiki/Partial_type)来扩展类型化数据集中的数据表功能。 此方法还可与 Tableadapter 一起使用。

类型化数据集 `Northwind.xsd` 位于 `App_Code` 文件夹 s `DAL` 子文件夹中。 在名为 `TransactionSupport` `DAL` 文件夹中创建一个子文件夹，并添加一个名为 `ProductsTableAdapter.TransactionSupport.cs` 的新类文件（参见图4）。 此文件将保存 `ProductsTableAdapter` 的部分实现，其中包括使用事务执行数据修改的方法。

![添加一个名为 TransactionSupport 的文件夹和一个名为 ProductsTableAdapter.TransactionSupport.cs 的类文件](wrapping-database-modifications-within-a-transaction-cs/_static/image4.gif)

**图 4**：添加名为 `TransactionSupport` 的文件夹和名为 `ProductsTableAdapter.TransactionSupport.cs` 的类文件

在 `ProductsTableAdapter.TransactionSupport.cs` 文件中输入以下代码：

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample3.cs)]

此处的类声明中的 `partial` 关键字向编译器指示中添加的成员将添加到 `NorthwindTableAdapters` 命名空间中的 `ProductsTableAdapter` 类中。 请注意文件顶部的 `using System.Data.SqlClient` 语句。 由于 TableAdapter 配置为使用 SqlClient 提供程序，因此，在内部它使用[`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx)对象向数据库发出其命令。 因此，需要使用 `SqlTransaction` 类来启动事务，然后将其提交或回滚。 如果使用 Microsoft SQL Server 以外的数据存储，则需要使用相应的提供程序。

这些方法提供启动、回滚和提交事务所需的构建基块。 它们标记为 `public`，使其可以从 `ProductsTableAdapter`中、从 DAL 中的另一个类或结构中的其他层（如 BLL）使用。 `BeginTransaction` 打开 TableAdapter 的内部 `SqlConnection` （如果需要），则启动该事务并将其分配给 `Transaction` 属性，并将该事务附加到 `SqlCommand` 对象的内部 `SqlDataAdapter`。 `CommitTransaction` 和 `RollbackTransaction` 在关闭内部 `Rollback` 对象之前，分别调用 `Transaction` 对象 `Commit` 和 `Connection` 方法。

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>步骤3：添加方法以更新和删除事务涵盖下的数据

完成这些方法后，我们就可以将方法添加到 `ProductsDataTable` 或 BLL，它们会在事务的一系列下执行一系列命令。 下面的方法使用批处理更新模式来更新使用事务的 `ProductsDataTable` 实例。 它通过调用 `BeginTransaction` 方法来启动事务，然后使用 `try...catch` 块发出数据修改语句。 如果对 `Adapter` 对象 s `Update` 方法的调用导致了异常，则执行将传输到将回滚事务并再次引发异常的 `catch` 块。 请记住，`Update` 方法通过枚举提供的 `ProductsDataTable` 的行并执行必要的 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 来实现批处理更新模式。 如果这些命令中的任何一个导致错误，则会回滚事务，并撤消事务生存期内先前所做的修改。 如果 `Update` 语句完全没有错误，则会完全提交事务。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample4.cs)]

通过 `ProductsTableAdapter.TransactionSupport.cs`中的分部类将 `UpdateWithTransaction` 方法添加到 `ProductsTableAdapter` 类。 另外，还可以将此方法添加到业务逻辑层的 `ProductsBLL` 类中，并进行几次语法更改。 也就是说，`this.BeginTransaction()`、`this.CommitTransaction()`和 `this.RollbackTransaction()` 中的关键字需要替换为 `Adapter` （回想一下，`Adapter` 是类型 `ProductsBLL` `ProductsTableAdapter`）中属性的名称。

`UpdateWithTransaction` 方法使用批处理更新模式，但也可以在事务范围内使用一系列 DB 直通调用，如下面的方法所示。 `DeleteProductsWithTransaction` 方法接受作为输入 `int`类型的 `List<T>`，这是要删除的 `ProductID`。 方法通过调用 `BeginTransaction` 来启动事务，然后，在 `try` 块中，会循环访问提供的列表，为每个 `ProductID` 值调用 DB 直通模式 `Delete` 方法。 如果对 `Delete` 的任何调用失败，则会将控制转移到事务回滚的 `catch` 块，并重新引发异常。 如果 `Delete` 对的所有调用都成功，则提交事务。 将此方法添加到 `ProductsBLL` 类。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample5.cs)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>跨多个 Tableadapter 应用事务

本教程中所述的与事务相关的代码允许将 `ProductsTableAdapter` 的多个语句视为一个原子操作。 但如果需要以原子方式对不同数据库表进行多个修改，会怎样呢？ 例如，在删除类别时，我们可能需要首先将其当前产品重新分配给其他类别。 这两个步骤重新分配产品并删除类别应作为原子操作执行。 但 `ProductsTableAdapter` 仅包括用于修改 `Products` 表的方法，而 `CategoriesTableAdapter` 只包含修改 `Categories` 表的方法。 那么，事务如何能同时包含这两个 Tableadapter 呢？

一种选择是将方法添加到名为 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 的 `CategoriesTableAdapter`，并让该方法调用一个存储过程，该存储过程将重新分配产品并删除存储过程中定义的事务范围内的类别。 在将来的教程中，我们将介绍如何在存储过程中开始、提交和回滚事务。

另一种方法是在包含 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 方法的 DAL 中创建帮助器类。 此方法将创建 `CategoriesTableAdapter` 和 `ProductsTableAdapter` 的实例，然后将这两个 Tableadapter `Connection` 属性设置为相同的 `SqlConnection` 实例。 此时，两个 Tableadapter 中的一个将通过调用 `BeginTransaction`来启动该事务。 用于重新分配产品和删除类别的 Tableadapter 方法将在提交或回滚事务的 `try...catch` 块中调用。

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>步骤4：将`UpdateWithTransaction`方法添加到业务逻辑层

在步骤3中，我们将 `UpdateWithTransaction` 方法添加到 DAL 中的 `ProductsTableAdapter`。 应向 BLL 添加相应的方法。 尽管表示层可以直接调用 DAL 来调用 `UpdateWithTransaction` 方法，但这些教程 strived 定义了一个将 DAL 与表示层隔离的分层体系结构。 因此，它 behooves 我们继续此方法。

打开 `ProductsBLL` 类文件，并添加一个名为 `UpdateWithTransaction` 的方法，该方法只需向下调用相应的 DAL 方法。 现在，`ProductsBLL`中应该有两个新方法： `UpdateWithTransaction`（刚刚添加的）和 `DeleteProductsWithTransaction`，这是在步骤3中添加的。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample6.cs)]

> [!NOTE]
> 这些方法不包括分配给 `ProductsBLL` 类中大多数其他方法的 `DataObjectMethodAttribute` 属性，因为我们将直接从 ASP.NET 页代码隐藏类调用这些方法。 请记住，`DataObjectMethodAttribute` 用于标记应在 ObjectDataSource 的 "配置数据源" 向导中以及哪些选项卡（SELECT、UPDATE、INSERT 或 DELETE）上出现哪些方法。 由于 GridView 缺少对批处理编辑或删除的任何内置支持，因此必须以编程方式而不是使用无代码的声明性方法来调用这些方法。

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>步骤5：以原子方式更新表示层中的数据库数据

为了说明该事务在更新一批记录时所具有的影响，让我们创建一个用户界面，该界面列出了 GridView 中的所有产品并包含一个按钮 Web 控件，单击该控件时，将 `CategoryID` 值重新分配产品。 特别是，类别重新分配将进行，以便为前几个产品分配一个有效的 `CategoryID` 值，而另一些产品则有意分配了不存在的 `CategoryID` 值。 如果我们尝试使用其 `CategoryID` 与现有类别 `CategoryID`不匹配的产品更新数据库，则会发生外键约束冲突，并将引发异常。 在此示例中，我们将看到，在使用事务时，外键约束冲突引发的异常将导致回滚之前的有效 `CategoryID` 更改。 但是，如果不使用事务，将保留对初始类别所做的修改。

首先打开 `BatchData` 文件夹中的 "`Transactions.aspx`" 页，然后从 "工具箱" 拖动到设计器上。 将其 `ID` 设置为 `Products`，并从其智能标记将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为从 `ProductsBLL` 类 `GetProducts` 方法拉取其数据。 这将是一个只读的 GridView，因此，将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"，然后单击 "完成"。

[![图5：将 ObjectDataSource 配置为使用 ProductsBLL 类 s GetProducts 方法](wrapping-database-modifications-within-a-transaction-cs/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image3.png)

**图 5**：图5：将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProducts` 方法（[单击查看完全大小的映像](wrapping-database-modifications-within-a-transaction-cs/_static/image4.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](wrapping-database-modifications-within-a-transaction-cs/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image5.png)

**图 6**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](wrapping-database-modifications-within-a-transaction-cs/_static/image6.png)）

完成 "配置数据源" 向导后，Visual Studio 将为 "产品数据" 字段创建 BoundFields 和一个 CheckBoxField。 删除除 `ProductID`、`ProductName`、`CategoryID`和 `CategoryName` 以外的所有字段，并将 `ProductName` `CategoryName` 属性分别重命名为 "产品" 和 "类别"。`HeaderText` 从智能标记中，选中 "启用分页" 选项。 进行这些修改后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample7.aspx)]

接下来，在 GridView 上方添加三个按钮 Web 控件。 将第一个按钮的 Text 属性设置为 "刷新网格"，将第二个按钮设置为 "修改类别（带有事务）"，然后将第三个按钮设置为 "修改类别（不包含事务）"。

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample8.aspx)]

此时，Visual Studio 中的设计视图应类似于图7中所示的屏幕截图。

[![页面包含一个 GridView 和三个按钮 Web 控件](wrapping-database-modifications-within-a-transaction-cs/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image7.png)

**图 7**：页面包含一个 GridView 和三个按钮 Web 控件（[单击以查看完全大小的图像](wrapping-database-modifications-within-a-transaction-cs/_static/image8.png)）

为三个按钮的每个 `Click` 事件创建事件处理程序，并使用以下代码：

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample9.cs)]

`Click` 事件处理程序的 "刷新" 按钮，只需调用 `Products` GridView s `DataBind` 方法即可将数据重新绑定到 GridView。

第二个事件处理程序将 `CategoryID` 中的产品进行重新分配，并使用 BLL 中的新事务方法，在事务的涵盖下执行数据库更新。 请注意，每个产品 `CategoryID` 任意设置为与 `ProductID`相同的值。 这将适用于前几个产品，因为这些产品的 `ProductID` 值会映射到有效 `CategoryID`。 但一旦 `ProductID` 开始变得过大，这巧合将重叠 `ProductID` s，`CategoryID` 将不再适用。

第三个 `Click` 事件处理程序以相同的方式更新产品 `CategoryID`，但使用 `ProductsTableAdapter` 默认 `Update` 方法将更新发送到数据库。 此 `Update` 方法不会包装事务内的一系列命令，因此，在遇到第一个遇到的外键约束冲突错误之前，这些更改将保持不变。

若要演示此行为，请通过浏览器访问此页。 最初应会看到第一页数据，如图8所示。 接下来，单击 "修改类别（带有事务）" 按钮。 这将导致回发并尝试将所有产品 `CategoryID` 值更新，但会导致外键约束冲突（参见图9）。

[![产品显示在可分页 GridView 中](wrapping-database-modifications-within-a-transaction-cs/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image9.png)

**图 8**：产品显示在一个可分页的 GridView 中（[单击以查看完全大小的图像](wrapping-database-modifications-within-a-transaction-cs/_static/image10.png)）

[重新分配类别 ![导致违反外键约束](wrapping-database-modifications-within-a-transaction-cs/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image11.png)

**图 9**：重新分配类别导致外键约束冲突（[单击以查看完全大小的图像](wrapping-database-modifications-within-a-transaction-cs/_static/image12.png)）

现在，单击浏览器的 "后退" 按钮，然后单击 "刷新网格" 按钮。 刷新数据时，应看到完全相同的输出，如图8所示。 也就是说，即使某些产品 `CategoryID` 更改为合法值并在数据库中更新，但在违反外键约束时，它们也会回滚。

现在，尝试单击 "修改类别（不包含事务）" 按钮。 这会导致相同的外键约束冲突错误（参见图9），但这一次，那些 `CategoryID` 值更改为合法值的产品将不会回滚。 单击浏览器的 "后退" 按钮，然后单击 "刷新网格" 按钮。 如图10所示，已重新分配前8种产品的 `CategoryID`。 例如，在图8中，改动的 `CategoryID` 为1，但在图10中，它已重新分配给2。

[![一些产品类别 Id 值已更新，但其他产品不存在](wrapping-database-modifications-within-a-transaction-cs/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image13.png)

**图 10**：某些产品 `CategoryID` 值已更新，但其他产品未更新（[单击查看全尺寸映像](wrapping-database-modifications-within-a-transaction-cs/_static/image14.png)）

## <a name="summary"></a>摘要

默认情况下，TableAdapter s 方法不会将已执行的数据库语句包装在事务范围内，但是，我们可以添加创建、提交和回滚事务的方法。 在本教程中，我们在 `ProductsTableAdapter` 类中创建了三种方法： `BeginTransaction`、`CommitTransaction`和 `RollbackTransaction`。 我们了解了如何将这些方法与 `try...catch` 块结合使用，使一系列数据修改语句成为原子的。 具体而言，我们在 `ProductsTableAdapter`中创建了 `UpdateWithTransaction` 方法，该方法使用批处理更新模式来对提供的 `ProductsDataTable`的行执行必要的修改。 我们还将 `DeleteProductsWithTransaction` 方法添加到 BLL 中的 `ProductsBLL` 类，该方法接受 `ProductID` 值的 `List` 作为其输入，并为每个 `Delete` 调用 DB 直通模式方法 `ProductID`。 这两种方法首先创建一个事务，然后在 `try...catch` 块内执行数据修改语句。 如果发生异常，事务将回滚，否则将被提交。

步骤5阐释了事务批更新与忽略使用事务的批处理更新的影响。 在接下来的三个教程中，我们将在本教程的基础上构建，并创建用于执行批量更新、删除和插入操作的用户界面。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [维护事务的数据库一致性](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [在 SQL Server 存储过程中管理事务](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [简化了事务： `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope 和 Dataadapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [在 .NET 中使用 Oracle Database 事务](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Dave Gardner、Hilton Giesenow 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一部分](batch-updating-cs.md)
