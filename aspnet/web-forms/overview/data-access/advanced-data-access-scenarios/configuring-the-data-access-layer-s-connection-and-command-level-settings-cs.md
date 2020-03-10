---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-cs
title: 配置数据访问层的连接和命令级别设置（C#） |Microsoft Docs
author: rick-anderson
description: 类型化数据集中的 Tableadapter 自动处理与数据库的连接、发出命令，并使用结果填充 DataTable 。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: cd330dd9-6254-4305-9351-dd727384c83b
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-cs
msc.type: authoredcontent
ms.openlocfilehash: 8fe7a5a2e410b47c8c2be62851f2b7b775d60209
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78444386"
---
# <a name="configuring-the-data-access-layers-connection--and-command-level-settings-c"></a>配置数据访问层的连接和命令级别的设置 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_CS.zip)或[下载 PDF](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/datatutorial72cs1.pdf)

> 类型化数据集中的 Tableadapter 自动处理与数据库的连接、发出命令，并使用结果填充 DataTable。 但在某些情况下，我们希望自己处理这些详细信息，在本教程中，我们将了解如何访问 TableAdapter 中的数据库连接和命令级别设置。

## <a name="introduction"></a>简介

在本系列教程中，我们使用了类型化的数据集来实现分层体系结构的数据访问层和业务对象。 如[第一个教程](../introduction/creating-a-data-access-layer-cs.md)中所述，类型化数据集的数据表用作数据存储库，而 tableadapter 充当包装器，用于与数据库进行通信以检索和修改基础数据。 Tableadapter 封装了处理数据库所涉及的复杂性，使我们不必编写代码来连接到数据库、发出命令，或将结果填充到 DataTable。

但有时，当我们需要 burrow 到 TableAdapter 的深度并编写直接与 ADO.NET 对象结合使用的代码时。 例如，在[事务中包装数据库的修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md)教程中，我们将方法添加到了用于开始、提交和回滚 ADO.NET 事务的 TableAdapter。 这些方法使用了内部手动创建的 `SqlTransaction` 对象，该对象已分配给 TableAdapter s `SqlCommand` 对象。

在本教程中，我们将检查如何访问 TableAdapter 中的数据库连接和命令级别设置。 具体而言，我们将向 `ProductsTableAdapter` 添加功能，以便能够访问基础连接字符串和命令超时设置。

## <a name="working-with-data-using-adonet"></a>使用 ADO.NET 处理数据

Microsoft .NET 框架包含专门用于处理数据的类的很多。 在[`System.Data` 命名空间](https://msdn.microsoft.com/library/system.data.aspx)中找到的这些类称为*ADO.NET*类。 ADO.NET 伞下的某些类与特定*数据访问接口*相关联。 你可以将数据访问接口看作是一种信道，它允许信息在 ADO.NET 类和基础数据存储之间流动。 有一些通用化提供程序，如 OleDb 和 ODBC，以及专门为特定数据库系统设计的提供程序。 例如，虽然可以使用 OleDb 访问接口连接到 Microsoft SQL Server 数据库，但 SqlClient 提供程序的工作效率要高得多，因为它专门针对 SQL Server 设计和优化。

以编程方式访问数据时，通常使用以下模式：

- 建立与数据库的连接。
- 发出命令。
- 对于 `SELECT` 查询，请使用生成的记录。

每个步骤都有单独的 ADO.NET 类。 例如，若要使用 SqlClient 提供程序连接到数据库，请使用[`SqlConnection` 类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)。 若要向数据库发出 `INSERT`、`UPDATE`、`DELETE`或 `SELECT` 命令，请使用[`SqlCommand` 类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)。

除了在[事务教程内包装数据库修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md)之外，我们还无需编写任何低级别的 ADO.NET 代码，因为 tableadapter 自动生成的代码包括连接到数据库所需的功能、发出命令、检索数据和将数据填充到数据表。 不过，有时我们需要自定义这些低级别设置。 在接下来的几个步骤中，我们将探讨如何使用 Tableadapter 内部使用的 ADO.NET 对象。

## <a name="step-1-examining-with-the-connection-property"></a>步骤1：通过连接属性进行检查

每个 TableAdapter 类都有一个指定数据库连接信息的 `Connection` 属性。 此属性的数据类型和 `ConnectionString` 值由在 "TableAdapter 配置向导" 中所做的选择决定。 请记住，当我们首次将 TableAdapter 添加到类型化数据集时，此向导会向我们询问数据库源（请参阅图1）。 此第一步中的下拉列表包含在配置文件中指定的这些数据库以及服务器资源管理器的数据连接中的任何其他数据库。 如果下拉列表中不存在要使用的数据库，则可以通过单击 "新建连接" 按钮并提供所需的连接信息，来指定新的数据库连接。

[![TableAdapter 配置向导的第一步](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image1.png)

**图 1**： TableAdapter 配置向导的第一步（[单击查看完全大小的映像](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image3.png)）

让我们花点时间来检查 TableAdapter s `Connection` 属性的代码。 如[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)教程中所述，我们可以通过转到 "类视图" 窗口查看自动生成的 TableAdapter 代码，向下钻取到相应的类，然后双击成员名称。

转到 "视图" 菜单，然后选择 "类视图" （或通过键入 Ctrl + Shift + C），导航到 "类视图" 窗口。 在类视图窗口的上半部分，向下钻取到 `NorthwindTableAdapters` 命名空间，然后选择 `ProductsTableAdapter` 类。 这会在类视图的下半部分显示 `ProductsTableAdapter` 成员，如图2所示。 双击 `Connection` 属性以查看其代码。

![双击 "类视图中的连接属性以查看其自动生成的代码](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image4.png)

**图 2**：双击 "类视图中的连接属性以查看其自动生成的代码

TableAdapter s `Connection` 属性和其他与连接相关的代码如下所示：

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample1.cs)]

当 TableAdapter 类实例化时，成员变量 `_connection` 等于 `null`。 访问 `Connection` 属性时，它首先检查 `_connection` 成员变量是否已实例化。 如果没有，则调用 `InitConnection` 方法，该方法将 `_connection` 实例化，并将其 `ConnectionString` 属性设置为从 TableAdapter 配置向导第一步中指定的连接字符串值。

还可以将 `Connection` 属性分配给 `SqlConnection` 对象。 这样做会将新的 `SqlConnection` 对象与每个 TableAdapter `SqlCommand` 对象相关联。

## <a name="step-2-exposing-connection-level-settings"></a>步骤2：公开连接级设置

连接信息应保留在 TableAdapter 中，并且应用程序体系结构中的其他层不可访问。 但是，在某些情况下，可能需要为查询、用户或 ASP.NET 页访问或自定义 TableAdapter 连接级信息。

让我们扩展 `Northwind` 数据集中的 `ProductsTableAdapter`，以包含一个 `ConnectionString` 属性，业务逻辑层可以使用该属性读取或更改 TableAdapter 使用的连接字符串。

> [!NOTE]
> *连接字符串*是一个字符串，用于指定数据库连接信息，如要使用的访问接口、数据库的位置、身份验证凭据和其他与数据库相关的设置。 有关各种数据存储和提供程序所使用的连接字符串模式的列表，请参阅[ConnectionStrings.com](http://www.connectionstrings.com/)。

如[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)教程中所述，可通过使用分部类扩展类型化数据集的自动生成的类。 首先，在 "`~/App_Code/DAL`" 文件夹下名为 `ConnectionAndCommandSettings` 的项目中创建一个新的子文件夹。

![添加一个名为 ConnectionAndCommandSettings 的子文件夹](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image5.png)

**图 3**：添加一个名为 `ConnectionAndCommandSettings` 的子文件夹

添加一个名为 `ProductsTableAdapter.ConnectionAndCommandSettings.cs` 的新类文件，并输入以下代码：

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample2.cs)]

此分部类向 `ProductsTableAdapter` 类添加一个名为 `ConnectionString` 的 `public` 属性，该属性允许任何层读取或更新 TableAdapter 基础连接的连接字符串。

创建（并保存）此分部类后，打开 `ProductsBLL` 类。 转到其中一个现有方法，在 `Adapter` 中键入，然后按 period 键以显示 IntelliSense。 你应会看到 IntelliSense 中提供的新 `ConnectionString` 属性，这意味着你可以通过编程方式从 BLL 读取或调整此值。

## <a name="exposing-the-entire-connection-object"></a>公开整个连接对象

此分部类只公开基础连接对象的一个属性： `ConnectionString`。 如果要使整个连接对象在 TableAdapter 范围外可用，则可以选择更改 `Connection` 属性 "保护级别。 我们在步骤1中检查的自动生成的代码表明，TableAdapter s `Connection` 属性被标记为 `internal`，这意味着它只能由同一程序集中的类访问。 不过，可以通过 TableAdapter s `ConnectionModifier` 属性更改此属性。

打开 `Northwind` 数据集，在设计器中单击 `ProductsTableAdapter`，然后导航到 "属性窗口"。 在这里，你将看到 `ConnectionModifier` 设置为其默认值，`Assembly`。 若要使 `Connection` 属性在类型化数据集的程序集外部可用，请将 `ConnectionModifier` 属性更改为 "`Public`"。

[![可以通过 ConnectionModifier 属性配置连接属性的可访问性级别](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image6.png)

**图 4**：可以通过 `ConnectionModifier` 属性配置 `Connection` 属性的可访问性级别（[单击以查看完全大小的映像](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image8.png)）

保存数据集，然后返回到 `ProductsBLL` 类。 与之前一样，请转到现有方法之一，键入 `Adapter`，然后按 period 键打开 IntelliSense。 此列表应包括一个 `Connection` 属性，这意味着现在可以通过编程方式从 BLL 中读取或分配任何连接级别设置。

## <a name="step-3-examining-the-command-related-properties"></a>步骤3：检查与命令相关的属性

TableAdapter 包含一个主查询，默认情况下，它具有自动生成的 `INSERT`、`UPDATE`和 `DELETE` 语句。 此主查询 `INSERT`、`UPDATE`和 `DELETE` 语句通过 `Adapter` 属性作为 ADO.NET 数据适配器对象在 TableAdapter 代码中实现。 与 `Connection` 属性一样，`Adapter` 属性的数据类型由所使用的数据访问接口确定。 由于这些教程使用 SqlClient 提供程序，因此 `Adapter` 属性的类型[`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)。

TableAdapter s `Adapter` 属性具有 `SqlCommand` 类型的三个属性，该属性用于发出 `INSERT`、`UPDATE`和 `DELETE` 语句：

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

`SqlCommand` 对象负责向数据库发送特定查询，并具有如下所示的属性： [`CommandText`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx)，其中包含要执行的即席 SQL 语句或存储过程;和[`Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)，它是 `SqlParameter` 对象的集合。 正如我们在[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)教程中看到的那样，可以通过属性窗口自定义这些命令对象。

除了其主查询外，TableAdapter 还可以包含可变数量的方法，这些方法在调用时将指定的命令调度到数据库。 所有其他方法的主查询 command 对象和 command 对象均存储在 TableAdapter s `CommandCollection` 属性中。

让我们花点时间查看 `ProductsTableAdapter` 在 `Northwind` DataSet 中为这两个属性及其支持的成员变量和帮助程序方法生成的代码：

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample3.cs)]

`Adapter` 和 `CommandCollection` 属性的代码会充分模拟 `Connection` 属性的代码。 有一些成员变量保存属性使用的对象。 `get` 访问器的属性首先检查相应的成员变量是否 `null`。 如果是这样，将调用初始化方法，该方法创建成员变量的实例并分配与核心命令相关的属性。

## <a name="step-4-exposing-command-level-settings"></a>步骤4：公开命令级设置

理想情况下，命令级信息应在数据访问层中保持封装。 如果在体系结构的其他层中需要此信息，则可以通过分部类公开此信息，就像连接级设置一样。

由于 TableAdapter 只有单个 `Connection` 属性，因此用于公开连接级设置的代码非常简单。 由于 TableAdapter 可以具有多个命令对象（`InsertCommand`、`UpdateCommand`和 `DeleteCommand`）以及 `CommandCollection` 属性中的可变数目的命令对象，因此在修改命令级别设置时，会稍微复杂一些。 更新命令级别设置时，这些设置将需要传播到所有命令对象。

例如，假设 TableAdapter 中存在一些需要很长时间执行的查询。 使用 TableAdapter 执行其中一个查询时，可能需要增加 command 对象的[`CommandTimeout` 属性](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)。 此属性指定等待命令执行的秒数，默认值为30。

若要允许由 BLL 调整 `CommandTimeout` 属性，请使用在步骤2（`ProductsTableAdapter.ConnectionAndCommandSettings.cs`）中创建的分部类文件，将以下 `public` 方法添加到 `ProductsDataTable`：

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample4.cs)]

可以从 BLL 或表示层调用此方法，以便为该 TableAdapter 实例发出的所有命令设置命令超时。

> [!NOTE]
> `Adapter` 和 `CommandCollection` 属性标记为 `private`，这意味着只能从 TableAdapter 内的代码访问这些属性。 与 `Connection` 属性不同，这些访问修饰符是不可配置的。 因此，如果需要向体系结构中的其他层公开命令级属性，则必须使用上述分部类方法来提供读取或写入 `private` 命令对象的 `public` 方法或属性。

## <a name="summary"></a>摘要

类型化数据集中的 Tableadapter 用于封装数据访问详细信息和复杂性。 使用 Tableadapter，不必担心编写 ADO.NET 代码来连接数据库、发出命令，或将结果填充到 DataTable。 它将自动为我们自动处理。

不过，有时我们需要自定义低级 ADO.NET 细节，例如更改连接字符串或默认连接或命令超时值。 TableAdapter 具有自动生成的 `Connection`、`Adapter`和 `CommandCollection` 属性，但默认情况下这些属性为 `internal` 或 `private`。 通过使用分部类扩展 TableAdapter 以包括 `public` 方法或属性，可以公开此内部信息。 或者，可以通过 TableAdapter s `ConnectionModifier` 属性配置 TableAdapter s `Connection` 属性访问修饰符。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Burnadette Leigh、S ren Jacob Lauritsen、Teresa Murphy 和 Hilton Geisenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](working-with-computed-columns-cs.md)
> [下一页](protecting-connection-strings-and-other-configuration-information-cs.md)
