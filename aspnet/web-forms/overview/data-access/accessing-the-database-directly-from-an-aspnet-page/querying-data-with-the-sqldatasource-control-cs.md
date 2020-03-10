---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
title: 用 SqlDataSource 控件查询数据（C#） |Microsoft Docs
author: rick-anderson
description: 在前面的教程中，我们使用了 ObjectDataSource 控件将表示层与数据访问层完全分离。 从此教程开始 。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 60512d6a-b572-4b7a-beb3-3e44b4d2020c
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 5bda42965f7d1db71b207c0b76e251b8fff64e31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508220"
---
# <a name="querying-data-with-the-sqldatasource-control-c"></a>使用 SqlDataSource 控件查询数据 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_CS.exe)或[下载 PDF](querying-data-with-the-sqldatasource-control-cs/_static/datatutorial47cs1.pdf)

> 在前面的教程中，我们使用了 ObjectDataSource 控件将表示层与数据访问层完全分离。 从本教程开始，我们将了解如何将 SqlDataSource 控件用于简单的应用程序，这些应用程序不需要这种严格地分离显示和数据访问。

## <a name="introduction"></a>简介

到目前为止，我们所检查的所有教程都使用了一种分层体系结构，其中包含表示层、业务逻辑层和数据访问层。 数据访问层（DAL）是在第一个教程（[创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)）中创建的，另一个是在第二个教程（[创建业务逻辑层](../introduction/creating-a-business-logic-layer-cs.md)）中创建的。 从使用[ObjectDataSource 教程显示数据](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)开始，我们看到了如何使用 ASP.NET 2.0 s new ObjectDataSource 控件以声明方式与表示层中的体系结构进行交互。

虽然到目前为止，所有教程都使用了体系结构来处理数据，但也可以直接从 ASP.NET 页访问、插入、更新和删除数据库数据，绕过此体系结构。 这样做会将特定数据库查询和业务逻辑直接置于网页中。 对于足够大或复杂的应用程序，设计、实现和使用分层体系结构对于应用程序的成功、可更新性和可维护性至关重要。 但是，在创建极其简单的一次性应用程序时，可能不需要开发可靠的体系结构。

ASP.NET 2.0 提供五种内置数据源控件[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)、 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)、 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)、 [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)和[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)。 SqlDataSource 可用于直接从关系数据库访问和修改数据，包括 Microsoft SQL Server、Microsoft Access、Oracle、MySQL 等。 在本教程和接下来的三个教程中，我们将探讨如何使用 SqlDataSource 控件，探索如何查询和筛选数据库数据，以及如何使用 SqlDataSource 来插入、更新和删除数据。

![ASP.NET 2.0 包括五个内置数据源控件](querying-data-with-the-sqldatasource-control-cs/_static/image1.gif)

**图 1**： ASP.NET 2.0 包括五个内置数据源控件

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>比较 ObjectDataSource 和 SqlDataSource

从概念上讲，ObjectDataSource 和 SqlDataSource 控件只是对数据进行代理。 正如在[通过 ObjectDataSource 显示数据](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程中所讨论的那样，ObjectDataSource 具有一些属性，这些属性指示提供数据的对象类型，以及用于从基础对象类型中选择、插入、更新和删除数据的方法。 配置 ObjectDataSource 的属性后，可以使用 ObjectDataSource `Select()`、`Insert()`、`Delete()`和 `Update()` 方法与基础结构进行交互，将数据 Web 控件（如 GridView、DetailsView 或 DataList）绑定到该控件。

SqlDataSource 提供了相同的功能，但针对关系数据库而不是对象库进行操作。 对于 SqlDataSource，必须指定要执行的数据库连接字符串、即席 SQL 查询或存储过程，以插入、更新、删除和检索数据。 SqlDataSource s `Select()`、`Insert()`、`Update()`和 `Delete()` 方法在调用时连接到指定的数据库并发出适当的 SQL 查询。 如下图所示，这些方法执行连接到数据库、发出查询并返回结果的 grunt 工作。

![SqlDataSource 充当数据库的代理](querying-data-with-the-sqldatasource-control-cs/_static/image2.gif)

**图 2**： SqlDataSource 充当数据库的代理

> [!NOTE]
> 在本教程中，我们将重点介绍如何从数据库中检索数据。 在[插入、更新和删除数据的 SqlDataSource 控件](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)教程中，我们将了解如何将 SqlDataSource 配置为支持插入、更新和删除操作。

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource 和 AccessDataSource 控件

除了 SqlDataSource 控件以外，ASP.NET 2.0 还包括一个 AccessDataSource 控件。 这两个不同的控件领导着许多开发人员都在 ASP.NET 2.0 的新手，怀疑 AccessDataSource 控件旨在使用 SqlDataSource 控件专门使用 Microsoft Access 来处理 Microsoft SQL Server。 尽管 AccessDataSource 旨在专门用于 Microsoft Access，但 SqlDataSource 控件适用于*任何*可通过 .net 访问的关系数据库。 这包括任何 OleDb 或与 ODBC 兼容的数据存储，如 Microsoft SQL Server、Microsoft Access、Oracle、Informix、MySQL 和 PostgreSQL，等等。

AccessDataSource 和 SqlDataSource 控件的唯一区别在于如何指定数据库连接信息。 AccessDataSource 控件只需要访问数据库文件的文件路径。 另一方面，SqlDataSource 需要一个完整的连接字符串。

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>步骤1：创建 SqlDataSource 网页

在开始探索如何使用 SqlDataSource 控件直接处理数据库数据之前，先花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程和接下来的三个页面中创建这些页面。 首先添加一个名为 `SqlDataSource`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![为 SqlDataSource 相关教程添加 ASP.NET 页](querying-data-with-the-sqldatasource-control-cs/_static/image3.gif)

**图 3**：为 SqlDataSource 相关教程添加 ASP.NET 页

与在其他文件夹中一样，`SqlDataSource` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](querying-data-with-the-sqldatasource-control-cs/_static/image5.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image4.gif)

**图 4**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](querying-data-with-the-sqldatasource-control-cs/_static/image6.gif)）

最后，将这四个页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，在将自定义按钮添加到 DataList 和 Repeater `<siteMapNode>`后面添加以下标记：

[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample1.sql)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧菜单现在包含用于编辑、插入和删除教程的项。

![站点映射现在包含 SqlDataSource 教程的条目](querying-data-with-the-sqldatasource-control-cs/_static/image7.gif)

**图 5**：站点地图现在包含 SqlDataSource 教程的条目

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>步骤2：添加和配置 SqlDataSource 控件

首先打开 `SqlDataSource` 文件夹中的 "`Querying.aspx`" 页，然后切换到 "设计视图"。 将 SqlDataSource 控件从工具箱拖到设计器上，并将其 `ID` 设置为 `ProductsDataSource`。 对于 ObjectDataSource，SqlDataSource 不会生成任何呈现的输出，因此显示为设计图面上的一个灰色框。 若要配置 SqlDataSource，请单击 SqlDataSource s 智能标记中的 "配置数据源" 链接。

![在 SqlDataSource s 智能标记中单击 "配置数据源" 链接](querying-data-with-the-sqldatasource-control-cs/_static/image8.gif)

**图 6**：单击 SqlDataSource s 智能标记中的 "配置数据源" 链接

这将打开 SqlDataSource 控件的 "配置数据源" 向导。 尽管向导的步骤不同于 ObjectDataSource 控件，但最终目标是相同的，目的是提供有关如何通过数据源检索、插入、更新和删除数据的详细信息。 对于 SqlDataSource，这需要指定要使用的基础数据库，并提供即席 SQL 语句或存储过程。

第一个向导步骤提示我们输入数据库。 下拉列表中包含在 web 应用程序 `App_Data` 文件夹中找到的那些数据库，以及已添加到服务器资源管理器中的 "数据连接" 节点的数据库。 由于我们已将 `App_Data` 文件夹中 `NORTHWIND.MDF` 数据库的连接字符串添加到了项目 `Web.config` 文件中，因此下拉列表包含对该连接字符串的引用 `NORTHWINDConnectionString`。 从下拉列表中选择此项，然后单击 "下一步"。

![从下拉列表中选择 "NORTHWINDConnectionString"](querying-data-with-the-sqldatasource-control-cs/_static/image9.gif)

**图 7**：从下拉列表中选择 `NORTHWINDConnectionString`

选择数据库后，向导将要求查询返回数据。 可以指定表或视图的列来返回，也可以输入自定义 SQL 语句或指定存储过程。 您可以通过指定自定义 SQL 语句或存储过程在此选项之间进行切换，并指定表或视图单选按钮中的列。

> [!NOTE]
> 对于第一个示例，请使用 "指定表或视图中的列" 选项。 我们将在本教程的后面部分返回到向导，并浏览 "指定自定义 SQL 语句或存储过程" 选项。

图8显示了 "指定表或视图中的列" 单选按钮时的 "配置 Select 语句" 屏幕。 下拉列表包含 Northwind 数据库中的表和视图的集合，其中显示了所选的表或视图列。 在此示例中，让 s 从 `Products` 表中返回 `ProductID`、`ProductName`和 `UnitPrice` 列。 如图8所示，在做出这些选择后，向导将显示生成的 SQL 语句 `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`。

![返回 Products 表中的数据](querying-data-with-the-sqldatasource-control-cs/_static/image10.gif)

**图 8**：返回 `Products` 表中的数据

将向导配置为从 `Products` 表中返回 `ProductID`、`ProductName`和 `UnitPrice` 列后，单击 "下一步" 按钮。 这最后一个屏幕提供了一个机会，可检查上一步中配置的查询的结果。 单击 "测试查询" 按钮会执行配置的 `SELECT` 语句，并在网格中显示结果。

![单击 "测试查询" 按钮以查看您的选择查询](querying-data-with-the-sqldatasource-control-cs/_static/image11.gif)

**图 9**：单击 "测试查询" 按钮查看 `SELECT` 查询

若要完成向导，请单击“完成”。

与 ObjectDataSource 一样，SqlDataSource s 向导仅将值分配给控件的属性，即 " [`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) " 和 " [`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) " 属性。 完成向导后，SqlDataSource 控件的声明性标记应如下所示：

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample2.aspx)]

`ConnectionString` 属性提供有关如何连接到数据库的信息。 可以为此属性分配一个完整的硬编码连接字符串值，也可以指向 `Web.config`中的连接字符串。 若要引用 Web.config 中的连接字符串值，请使用语法 `<%$ expressionPrefix:expressionValue %>`。 通常， *expressionPrefix*是 ConnectionStrings， *expressionValue*是 `Web.config` [`<connectionStrings>` 部分](https://msdn.microsoft.com/library/bf7sd233.aspx)中连接字符串的名称。 但是，可以使用语法从资源文件中引用 `<appSettings>` 元素或内容。 有关此语法的详细信息，请参阅[ASP.NET 表达式概述](https://msdn.microsoft.com/library/d5bd1tad.aspx)。

`SelectCommand` 属性指定要执行以返回数据的即席 SQL 语句或存储过程。

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>步骤3：添加数据 Web 控件并将其绑定到 SqlDataSource

配置 SqlDataSource 后，可以将其绑定到数据 Web 控件，如 GridView 或 DetailsView。 对于本教程，让我们在 GridView 中显示数据。 从 "工具箱" 中，将一个 GridView 拖到页面上，并通过从 GridView s 智能标记的下拉列表中选择数据源将其绑定到 `ProductsDataSource` SqlDataSource。

[![添加 GridView 并将其绑定到 SqlDataSource 控件](querying-data-with-the-sqldatasource-control-cs/_static/image13.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image12.gif)

**图 10**：添加 GridView 并将其绑定到 SqlDataSource 控件（[单击以查看完全大小的图像](querying-data-with-the-sqldatasource-control-cs/_static/image14.gif)）

从 GridView 的智能标记的下拉列表中选择 SqlDataSource 控件后，Visual Studio 将为数据源控件返回的每个列自动向 GridView 添加一个 BoundField 或 CheckBoxField。 由于 SqlDataSource 返回了三个数据库列 `ProductID`、`ProductName`和 `UnitPrice` GridView 中有三个字段。

请花点时间配置三个 BoundFields。 将 `ProductName` 字段 `HeaderText` "属性更改为" 产品名称 "，将" `UnitPrice` "字段更改为" 价格 "。 还要将 `UnitPrice` 字段的格式设置为货币。 进行这些修改后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample3.aspx)]

通过浏览器访问此页。 如图11所示，GridView 列出了每个产品的 `ProductID`、`ProductName`和 `UnitPrice` 值。

[![GridView 显示每个产品的 ProductID、ProductName 和单价值](querying-data-with-the-sqldatasource-control-cs/_static/image16.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image15.gif)

**图 11**： GridView 显示了每个产品的 `ProductID`、`ProductName`和 `UnitPrice` 值（[单击查看完全大小的图像](querying-data-with-the-sqldatasource-control-cs/_static/image17.gif)）

访问该页时，GridView `Select()` 方法调用其数据源控件。 使用 ObjectDataSource 控件时，这称为 `ProductsBLL` 类 `GetProducts()` 方法。 但对于 SqlDataSource，`Select()` 方法与指定的数据库建立连接，并发出 `SelectCommand` （在本示例中为`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`）。 SqlDataSource 返回其结果，GridView 随后将枚举，在 GridView 中为返回的每个数据库记录创建一行。

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>内置的数据 Web 控件功能和 SqlDataSource 控件

通常，数据 Web 控件的固有功能（分页、排序、编辑、删除、插入等）是特定于数据 Web 控件的，不依赖于所使用的数据源控件。 即，无论是绑定到 ObjectDataSource 还是 SqlDataSource，GridView 都可以利用其内置分页、排序、编辑和删除。 但是，某些数据 Web 控件功能对所使用的数据源控件或数据源控件的配置是敏感的。

例如，在对[大量数据进行有效分页](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)教程中，我们讨论了默认情况下，数据 Web 控件 naively 的分页逻辑返回基础数据源中的*所有*记录，然后在给定了当前页索引和每页显示的记录数的情况下，仅显示相应的记录子集。 当通过足够大的结果集进行分页时，此模型非常低效。 幸运的是，ObjectDataSource 可以配置为支持自定义分页，后者仅返回要显示的准确部分记录。 不过，SqlDataSource 控件缺少用于实现自定义分页的属性。

SqlDataSource 会出现另一个很微妙，其中包含分页和排序。 默认情况下，可以通过 GridView 对从 SqlDataSource 返回的数据进行分页或排序。 为了说明这一点，请在 `Querying.aspx` 中选中 "启用分页" 和 "启用排序" 选项，并验证它是否按预期方式工作。

排序和分页的工作方式是因为 SqlDataSource 将数据库数据检索到松散类型化的数据集。 查询返回的记录的总数从数据集中已确定可以进行分页。 此外，数据集的结果可以通过 DataView 排序。 当 GridView 请求分页数据或已排序数据时，SqlDataSource 将自动使用这些功能。

可以通过将 SqlDataSource 的[`DataSourceMode` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)从 `DataSet` （默认值）更改为 `DataReader`，将配置为返回 DataReader 而不是数据集。 在将 SqlDataSource 的结果传递到需要 DataReader 的现有代码时，可能首选使用 DataReader。 此外，由于 Datareader 比数据集简单得多，因此它们提供更好的性能。 但是，如果进行了此更改，数据 Web 控件既不能排序也不能分页，因为 SqlDataSource 无法确定查询返回的记录数，而且 DataReader 还会提供对返回的数据进行排序的任何技术。

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>步骤4：使用自定义 SQL 语句或存储过程

配置 SqlDataSource 控件时，可通过两种方法之一将用于返回数据的查询指定为自定义 SQL 语句或存储过程，或者作为现有表或视图中的列。 在步骤2中，我们检查了从 `Products` 表中选择列。 让我们看一下如何使用自定义 SQL 语句。

将另一个 GridView 控件添加到 `Querying.aspx` 页，然后从智能标记的下拉列表中选择创建新的数据源。 接下来，指示将从数据库中提取数据。这将创建一个新的 SqlDataSource 控件。 将控件命名为 `ProductsWithCategoryInfoDataSource`。

![创建名为 ProductsWithCategoryInfoDataSource 的新 SqlDataSource 控件](querying-data-with-the-sqldatasource-control-cs/_static/image18.gif)

**图 12**：创建名为 `ProductsWithCategoryInfoDataSource` 的新 SqlDataSource 控件

下一个屏幕会要求我们指定数据库。 如图7所示，从下拉列表中选择 "`NORTHWINDConnectionString`"，然后单击 "下一步"。 在 "配置 Select 语句" 屏幕中，选择 "指定自定义 SQL 语句或存储过程" 单选按钮，然后单击 "下一步"。 这将显示 "定义自定义语句" 或 "存储过程" 屏幕，该屏幕提供标记为 SELECT、UPDATE、INSERT 和 DELETE 的选项卡。 在每个选项卡中，您可以在文本框中输入自定义 SQL 语句，或从下拉列表中选择存储过程。 在本教程中，我们将介绍如何输入自定义 SQL 语句;下一教程包含一个使用存储过程的示例。

![输入自定义 SQL 语句或选取存储过程](querying-data-with-the-sqldatasource-control-cs/_static/image19.gif)

**图 13**：输入自定义 SQL 语句或选取存储过程

自定义 SQL 语句可以手动输入到文本框中，也可以通过单击 "查询生成器" 按钮以图形方式构造。 从 "查询生成器" 或 "文本框" 中，使用以下查询从 `Products` 表中返回 `ProductID` 和 `ProductName` 字段，方法是使用 `JOIN` 从 `CategoryName` 表中检索产品 `Categories`：

[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample4.sql)]

![您可以使用查询生成器以图形方式构造查询。](querying-data-with-the-sqldatasource-control-cs/_static/image20.gif)

**图 14**：可以使用查询生成器以图形方式构造查询。

指定查询后，单击 "下一步" 以转到 "测试查询" 屏幕。 单击 "完成" 以完成 SqlDataSource 向导。

完成该向导后，GridView 将为其添加三个 BoundFields，显示从查询返回的 `ProductID`、`ProductName`和 `CategoryName` 列，并生成以下声明性标记：

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample5.aspx)]

[![GridView 显示每个产品的 ID、名称和关联的类别名称](querying-data-with-the-sqldatasource-control-cs/_static/image22.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image21.gif)

**图 15**： GridView 显示了每个产品的 ID、名称和关联的类别名称（[单击以查看完全大小的图像](querying-data-with-the-sqldatasource-control-cs/_static/image23.gif)）

## <a name="summary"></a>摘要

在本教程中，我们介绍了如何使用 SqlDataSource 控件查询和显示数据。 与 ObjectDataSource 一样，SqlDataSource 充当代理，提供用于访问数据的声明性方法。 它的属性指定要连接到的数据库，以及要执行的 SQL `SELECT` 查询;可以通过属性窗口或使用 "配置数据源" 向导来指定。

本教程中所述的 `SELECT` 查询示例将返回指定查询中的所有记录。 不过，SqlDataSource 控件可以包含一个 `WHERE` 子句，其中的参数的值以编程方式分配或自动从指定的源中提取。 在下一教程中，我们将介绍如何创建和使用参数化查询！

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问关系数据库数据](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource 控件概述](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET 快速入门教程： SqlDataSource 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config `<connectionStrings>` 元素](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [数据库连接字符串引用](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Susan Connery、Bernadette Leigh 和 David Suru。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一部分](using-parameterized-queries-with-the-sqldatasource-cs.md)
