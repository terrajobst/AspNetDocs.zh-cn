---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
title: 通过 SqlDataSource 实现开放式并发（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将回顾一下乐观并发控制的基本知识，并探讨如何使用 SqlDataSource 控件实现它。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: a8fa72ee-8328-4854-a419-c1b271772303
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 431734b5245c20ac840147cf0827fa7f8d1e4d17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445310"
---
# <a name="implementing-optimistic-concurrency-with-the-sqldatasource-vb"></a>使用 SqlDataSource 实现乐观并发 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_VB.exe)或[下载 PDF](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/datatutorial50vb1.pdf)

> 在本教程中，我们将回顾一下乐观并发控制的基本知识，并探讨如何使用 SqlDataSource 控件实现它。

## <a name="introduction"></a>介绍

在前面的教程中，我们探讨了如何将插入、更新和删除功能添加到 SqlDataSource 控件中。 简而言之，若要提供这些功能，需要在控件 `InsertCommand`、`UpdateCommand`或 `DeleteCommand` 属性中指定相应的 `INSERT`、`UPDATE`或 `DELETE` SQL 语句，同时指定 `InsertParameters`、`UpdateParameters`和 `DeleteParameters` 集合中的相应参数。 尽管可以手动指定这些属性和集合，但 "配置数据源向导" 的 "高级" 按钮提供了 "生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框，该复选框将基于 `SELECT` 语句自动创建这些语句。

除了 "生成 `INSERT`、`UPDATE`和 `DELETE` 语句" 复选框，"高级 SQL 生成选项" 对话框包括 "使用开放式并发" 选项（请参阅图1）。 选中时，自动生成的 `UPDATE` 和 `DELETE` 语句中的 `WHERE` 子句将被修改为仅在用户上一次将数据加载到网格后未修改基础数据库数据时才执行 update 或 delete。

![你可以从 "高级 SQL 生成选项" 对话框添加乐观并发支持](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.gif)

**图 1**：你可以从 "高级 SQL 生成选项" 对话框添加乐观并发支持

回到[实现开放式并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程中，我们探讨了开放式并发控制的基础知识，以及如何将其添加到 ObjectDataSource。 在本教程中，我们将对乐观并发控制的基础进行润色，并探讨如何使用 SqlDataSource 实现它。

## <a name="a-recap-of-optimistic-concurrency"></a>开放式并发概述

对于允许多个同时存在的用户编辑或删除相同数据的 web 应用程序，有可能一个用户可能会意外覆盖其他更改。 在[实现开放式并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程中，我提供了以下示例：

假设两个用户 Jisun 和 Sam 都在访问应用程序中的一个页面，允许访问者通过 GridView 控件更新和删除产品。 同时单击 Chai 的 "编辑" 按钮。 Jisun 将产品名称更改为 Chai 茶，并单击 "更新" 按钮。 Net 结果是发送到数据库的 `UPDATE` 语句，该语句将设置*所有*产品的可更新字段（即使 Jisun 仅更新了一个字段，`ProductName`）。 此时，数据库的值为 Chai 茶、类别饮料、供应商现 Liquids 等，并在此特定产品上如此。 但是，Sam on Sam 的屏幕仍会以 Chai 的形式显示可编辑 GridView 行中的产品名称。 提交 Jisun s 更改后的几秒钟后，Sam 会将类别更新为调味品并单击 "更新"。 这会导致向数据库发送 `UPDATE` 语句，该语句将产品名称设置为 Chai，将 `CategoryID` 设置为相应的调味品类别 ID，依此类推。 已覆盖 Jisun 对产品名称所做的更改。

图2说明了这种交互。

[![两个用户同时更新 a 记录时，可能会有一个用户更改为覆盖其他](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.png)

**图 2**：当两个用户同时更新 a 记录时，可能会有一个用户更改为覆盖其他（[单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.png)）

若要防止此情况开拓，必须实现一种[并发控制](http://en.wikipedia.org/wiki/Concurrency_control)形式。 [开放式并发](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)本教程的重点是假设：尽管每次可能会发生并发冲突，但大多数情况下不会出现此类冲突。 因此，如果发生冲突，则乐观并发控制只会通知用户这些更改无法保存，因为另一个用户已修改了相同的数据。

> [!NOTE]
> 对于假设出现多个并发冲突的应用程序，或者如果无法容忍此类冲突，则可以改为使用悲观并发控制。 有关悲观并发控制的更详尽的讨论，请返回到[实现乐观并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程。

乐观并发控制的工作原理是确保正在更新或删除的记录的值与更新或删除进程启动时的值相同。 例如，当在可编辑 GridView 中单击 "编辑" 按钮时，将从数据库中读取记录的值并将其显示在文本框和其他 Web 控件中。 这些原始值由 GridView 保存。 稍后，在用户进行更改并单击 "更新" 按钮后，使用的 `UPDATE` 语句必须考虑原始值加上新值，并且仅当用户开始编辑的原始值与数据库中的值相同时，才更新基础数据库记录。 图3描绘了这一系列事件。

[![更新或删除成功，则原始值必须等于当前数据库值](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.png)

**图 3**：要使更新或删除成功，原始值必须等于当前数据库值（[单击即可查看完全大小的映像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.png)）

有多种方法可实现开放式并发（请参阅[Peter Bromberg](http://peterbromberg.net/)的[开放式并发更新逻辑](http://www.eggheadcafe.com/articles/20050719.asp)，简要了解一些选项）。 SqlDataSource 使用的方法（以及我们的数据访问层中使用的 ADO.NET 类型化数据集）将 `WHERE` 子句补充，以包括所有原始值的比较。 例如，下面的 `UPDATE` 语句仅在以下情况下才会更新产品的名称和价格：当前数据库值等于在 GridView 中更新记录时最初检索到的值。 `@ProductName` 和 `@UnitPrice` 参数包含用户输入的新值，而 `@original_ProductName` 和 `@original_UnitPrice` 包含在单击 "编辑" 按钮时最初加载到 GridView 的值：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample1.sql)]

正如我们在本教程中看到的那样，使用 SqlDataSource 启用乐观并发控制就像选中一个复选框一样简单。

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>步骤 1：创建支持开放式并发的 SqlDataSource

首先打开 `SqlDataSource` 文件夹中的 "`OptimisticConcurrency.aspx`" 页。 将 SqlDataSource 控件从工具箱拖到设计器上，将其 `ID` 属性设置为 `ProductsDataSourceWithOptimisticConcurrency`。 接下来，单击控件 s 智能标记中的 "配置数据源" 链接。 在向导的第一个屏幕中，选择使用 `NORTHWINDConnectionString` 并单击 "下一步"。

[![选择使用 NORTHWINDConnectionString](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.png)

**图 4**：选择使用 `NORTHWINDConnectionString` （[单击查看完全大小的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.png)）

在此示例中，我们将添加一个 GridView，使用户能够编辑 `Products` 表。 因此，在 "配置 Select 语句" 屏幕中，从下拉列表中选择 "`Products`" 表，然后选择 "`ProductID`"、"`ProductName`"、"`UnitPrice`" 和 "`Discontinued`" 列，如图5所示。

[从 Products 表中 ![，返回 ProductID、ProductName、单价和废止列](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.png)

**图 5**：从 "`Products`" 表返回 "`ProductID`"、"`ProductName`"、"`UnitPrice`" 和 "`Discontinued`" 列（[单击以查看完全大小的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.png)）

选取列后，单击 "高级" 按钮以打开 "高级 SQL 生成选项" 对话框。 选中 "生成 `INSERT`、`UPDATE`和 `DELETE`" 语句并使用 "开放式并发" 复选框，并单击 "确定" （有关屏幕截图，请参阅图1）。 单击 "下一步"，然后单击 "完成" 完成向导。

完成 "配置数据源" 向导后，请花点时间检查生成的 `DeleteCommand` 和 `UpdateCommand` 属性以及 `DeleteParameters` 和 `UpdateParameters` 集合。 要执行此操作，最简单的方法是单击左下角的 "源" 选项卡以查看页面声明性语法。 可在其中找到 `UpdateCommand` 值：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample2.sql)]

`UpdateParameters` 集合中具有七个参数：

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample3.aspx)]

同样，`DeleteCommand` 属性和 `DeleteParameters` 集合应该如下所示：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample4.sql)]

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample5.aspx)]

除了增加 `UpdateCommand` 和 `DeleteCommand` 属性的 `WHERE` 子句（并将附加参数添加到各自的参数集合）外，还可以选择 "使用开放式并发" 选项来调整两个其他属性：

- 将[`ConflictDetection` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx)从 `OverwriteChanges` （默认值）更改为 `CompareAllValues`
- 将[`OldValuesParameterFormatString` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx)从 {0} （默认值）更改为原\_{0}。

当数据 Web 控件调用 SqlDataSource `Update()` 或 `Delete()` 方法时，它会传入原始值。 如果 SqlDataSource `ConflictDetection` 属性设置为 `CompareAllValues`，则这些原始值将添加到命令中。 `OldValuesParameterFormatString` 属性提供了用于这些原始值参数的命名模式。 "配置数据源" 向导使用原始\_{0} 并在 `UpdateCommand` 中为每个原始参数命名，并相应地 `DeleteCommand` 属性和 `UpdateParameters` 和 `DeleteParameters` 集合。

> [!NOTE]
> 由于我们未使用 SqlDataSource 控件的插入功能，因此可随意删除 `InsertCommand` 属性及其 `InsertParameters` 集合。

## <a name="correctly-handlingnullvalues"></a>正确处理`NULL`值

遗憾的是，使用乐观并发时，"配置数据源" 向导自动生成的扩充的 `UPDATE` 和 `DELETE` 语句*不*能用于包含 `NULL` 值的记录。 若要查看原因，请考虑我们的 SqlDataSource `UpdateCommand`：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample6.sql)]

`Products` 表中的 `UnitPrice` 列可以具有 `NULL` 值。 如果某个特定记录具有 `UnitPrice`的 `NULL` 值，则 `WHERE` 子句部分 `[UnitPrice] = @original_UnitPrice` 将*始终*计算为 false，因为 `NULL = NULL` 始终返回 false。 因此，不能编辑或删除包含 `NULL` 值的记录，因为 `WHERE` 子句的 `UPDATE` 和 `DELETE` 语句不会返回任何要更新或删除的行。

> [!NOTE]
> 此 bug 首次在2004年6月的[SqlDataSource 生成错误的 SQL 语句](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937)，据称计划在下一版本的 ASP.NET 中修复。

若要解决此问题，必须手动更新可以具有 `NULL` 值的**所有**列的 `UpdateCommand` 和 `DeleteCommand` 属性中的 `WHERE` 子句。 通常，将 `[ColumnName] = @original_ColumnName` 更改为：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample7.sql)]

这一修改可通过从属性窗口中的 UpdateQuery 或 DeleteQuery 选项直接通过声明性标记进行，或通过配置数据中 "指定自定义 SQL 语句或存储过程" 选项的 "更新和删除" 选项卡进行源向导。 同样，必须对 `UpdateCommand` 的*每个*列和可包含 `NULL` 值的 `DeleteCommand` s `WHERE` 子句进行此修改。

将此示例应用于我们的示例会导致以下修改后的 `UpdateCommand` 和 `DeleteCommand` 值：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>步骤 2：添加具有编辑和删除选项的 GridView

如果将 SqlDataSource 配置为支持开放式并发，则剩下的就是将数据 Web 控件添加到利用此并发控制的页面。 对于本教程，让我们添加一个同时提供编辑和删除功能的 GridView。 若要实现此目的，请将 GridView 从工具箱拖到设计器上，并将其 `ID` 设置为 `Products`。 从 GridView s 智能标记中，将其绑定到步骤1中添加的 `ProductsDataSourceWithOptimisticConcurrency` SqlDataSource 控件。 最后，选中 "启用编辑并启用从智能标记中删除选项"。

[![将 GridView 绑定到 SqlDataSource 并启用编辑和删除](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.png)

**图 6**：将 GridView 绑定到 SqlDataSource 并启用编辑和删除（[单击查看完全大小的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image10.png)）

添加 GridView 后，通过删除 `ProductID` BoundField，将 `ProductName` BoundField s `HeaderText` 属性更改为 "产品"，并更新 `UnitPrice` BoundField 来配置其外观，使其 `HeaderText` 属性只是价格。 理想情况下，我们将增强编辑界面，使其包含用于 `ProductName` 值的 RequiredFieldValidator 和 `UnitPrice` 值的 CompareValidator （以确保它是格式正确的数值）。 请参阅[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程，深入了解如何自定义 GridView 编辑界面。

> [!NOTE]
> 由于从 GridView 传递到 SqlDataSource 的原始值存储在视图状态中，因此必须启用 GridView 的视图状态。

对 GridView 进行这些修改后，GridView 和 SqlDataSource 声明性标记应如下所示：

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample9.aspx)]

若要查看操作中的乐观并发控制，请打开两个浏览器窗口，并同时在这两个窗口中加载 `OptimisticConcurrency.aspx` 页面。 单击两个浏览器中第一个产品的 "编辑" 按钮。 在一个浏览器中，更改产品名称，并单击 "更新"。 浏览器将回发并返回到其预编辑模式，显示刚刚编辑的记录的新产品名称。

在第二个浏览器窗口中，更改价格（但保留产品名称作为其原始值），然后单击 "更新"。 在回发时，网格将恢复为其预编辑模式，但不会记录对价格的更改。 第二个浏览器显示的值与具有旧价格的新产品名称相同。 在第二个浏览器窗口中所做的更改丢失。 而且，所做的更改也会丢失，因为没有异常或消息表明发生了并发冲突。

[![第二个浏览器窗口中的更改是否以静默方式丢失](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image11.png)

**图 7**：第二个浏览器窗口中的更改被悄悄丢失（[单击查看完全大小的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image12.png)）

由于 `UPDATE` 语句 s `WHERE` 子句筛选掉了所有记录，因此不会影响任何行，因此无法提交第二个浏览器更改的原因。 让我们再次查看 `UPDATE` 语句：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample10.sql)]

当第二个浏览器窗口更新记录时，`WHERE` 子句中指定的原始产品名称将不与现有产品名称匹配（因为它已由第一个浏览器更改）。 因此，语句 `[ProductName] = @original_ProductName` 返回 False，并且 `UPDATE` 不影响任何记录。

> [!NOTE]
> 删除操作的方式与此相同。 在两个浏览器窗口打开的情况下，首先使用一个指定的产品进行编辑，然后保存其更改。 在将更改保存到一个浏览器后，单击另一个中的同一产品的 "删除" 按钮。 由于原始值在 `DELETE` 语句 s `WHERE` 子句中不匹配，因此，delete 将以静默方式失败。

在第二个浏览器窗口中从最终用户的角度来看，单击 "更新" 按钮后，网格将返回到预编辑模式，但其更改已丢失。 不过，没有视觉反馈，因为其更改未出现。 理想情况下，如果用户的更改丢失了并发冲突，我们将通知他们，可能会将网格保持在编辑模式下。 让我们看看如何实现此目的。

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>步骤 3：确定发生并发冲突的时间

由于并发冲突拒绝了所做的更改，因此当发生并发冲突时，将很好地向用户发出警报。 若要向用户发出警报，请将 "标签" Web 控件添加到名为 `ConcurrencyViolationMessage` 页面的顶部，其 `Text` 属性显示以下消息：您尝试更新或删除其他用户同时更新的记录。 请检查其他用户的更改，然后重做更新或删除。 `CssClass` 属性设置为 "警告"，这是在 `Styles.css` 中定义的一个 CSS 类，它以红色、斜体、粗体和大字体显示文本。 最后，将标签 `Visible` 和 `EnableViewState` 属性设置为 "`False`"。 这将隐藏该标签，仅限我们显式将其 `Visible` 属性设置为 `True`的回发。

[![向页面添加 "标签" 控件以显示警告](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image13.png)

**图 8**：向页面添加 "标签" 控件以显示警告（[单击以查看完全大小的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image14.png)）

执行 update 或 delete 时，GridView `RowUpdated` 和 `RowDeleted` 事件处理程序在其数据源控件执行请求的 update 或 delete 后激发。 我们可以从这些事件处理程序中确定操作影响的行数。 如果零行受到影响，我们想要显示 `ConcurrencyViolationMessage` 标签。

为 `RowUpdated` 事件和 `RowDeleted` 事件创建事件处理程序并添加以下代码：

[!code-vb[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample11.vb)]

在这两个事件处理程序中，我们将检查 `e.AffectedRows` 属性，如果该属性等于0，则将 `ConcurrencyViolationMessage` 标签 s `Visible` 属性设置为 "`True`"。 在 `RowUpdated` 事件处理程序中，我们还通过将 `KeepInEditMode` 属性设置为 true，指示 GridView 停留在编辑模式。 在此过程中，需要将数据重新绑定到网格，以便将其他用户的数据加载到编辑界面。 这是通过调用 GridView 的 `DataBind()` 方法来完成的。

如图9所示，在这两个事件处理程序中，每当发生并发冲突时，都会显示一条非常明显的消息。

[在出现并发冲突的情况中，会显示一条消息 ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image15.png)

**图 9**：出现并发冲突时，会显示一条消息（[单击以查看完全大小的映像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image16.png)）

## <a name="summary"></a>Summary

在创建多个并发用户可能编辑相同数据的 web 应用程序时，请务必考虑并发控制选项。 默认情况下，ASP.NET 数据 Web 控件和数据源控件不使用任何并发控制。 如本教程中所述，通过 SqlDataSource 实现乐观并发控制相对简单快捷。 SqlDataSource 处理了将扩充的 `WHERE` 子句添加到自动生成的 `UPDATE` 和 `DELETE` 语句的大部分琐碎工作，但处理 `NULL` 值列时有几个微妙之处，如正确处理 `NULL` 值部分所述。

本教程将结束我们对 SqlDataSource 的检查。 我们剩下的教程将返回使用 ObjectDataSource 和分层体系结构处理数据。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一篇](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
