---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 5 应用中使用 EF 处理并发
description: 本教程介绍当多个用户同时更新同一个实体时，如何使用乐观并发处理冲突。
author: tdykstra
ms.author: riande
ms.topic: tutorial
ms.date: 01/15/2019
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 43c5fdff5601c9bff32300d3460de0079a498d28
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499388"
---
# <a name="tutorial-handle-concurrency-with-ef-in-an-aspnet-mvc-5-app"></a>教程：在 ASP.NET MVC 5 应用中使用 EF 处理并发

在前面的教程中，您学习了如何更新数据。 本教程介绍当多个用户同时更新同一个实体时，如何使用乐观并发处理冲突。 您可以更改与 `Department` 实体一起使用的网页，以便处理并发错误。 下图显示了“编辑”和“删除”页面，包括发生并发冲突时显示的一些消息。

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 了解并发冲突
> * 添加乐观并发
> * 修改部门控制器
> * 测试并发处理
> * 更新“删除”页

## <a name="prerequisites"></a>系统必备

* [异步和存储过程](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="concurrency-conflicts"></a>并发冲突

当某用户显示实体数据以对其进行编辑，而另一用户在上一用户的更改写入数据库之前更新同一实体的数据时，会发生并发冲突。 如果不启用此类冲突的检测，则最后更新数据库的人员将覆盖其他用户的更改。 在许多应用程序中，此风险是可接受的：如果用户很少或更新很少，或者一些更改被覆盖并不重要，则并发编程可能弊大于利。 在此情况下，不必配置应用程序来处理并发冲突。

### <a name="pessimistic-concurrency-locking"></a>悲观并发（锁定）

如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。 这称为 "*悲观并发*"。 例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。 如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为他们得到的是正在更改的数据的副本。 如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。

管理锁定有缺点。 编程可能很复杂。 它需要大量的数据库管理资源，且随着应用程序用户数量的增加，可能会导致性能问题。 由于这些原因，并不是所有的数据库管理系统都支持悲观并发。 实体框架不提供对它的内置支持，本教程不会演示如何实现它。

### <a name="optimistic-concurrency"></a>开放式并发

保守式并发的替代方法是*乐观并发*。 悲观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。 例如，John 运行 "部门编辑" 页，将英语系的**预算**金额从 $350000.00 更改为 $0.00。

John 单击 "**保存**" 之前，Jane 运行相同的页面，并将 "**开始日期**" 字段从9/1/2007 更改为8/8/2013。

John 单击 "**保存**"，然后在浏览器返回到索引页时看到其更改，然后单击 "**保存**"。 接下来的情况取决于并发冲突的处理方式。 其中一些选项包括：

- 可以跟踪用户已修改的属性，并仅更新数据库中相应的列。 在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。 下次有人浏览英语系时，他们将看到 John 和 Jane 的更改，即开始日期为8/8/2013，预算为零美元。

    这种更新方法可减少可能导致数据丢失的冲突次数，但是如果对实体的同一属性进行竞争性更改，则数据难免会丢失。 Entity Framework 是否以这种方式工作取决于更新代码的实现方式。 通常不适合在 Web 应用程序中使用，因为它要求保持大量的状态，以便跟踪实体的所有原始属性值以及新值。 维护大量的状态可能会影响应用程序的性能，因为它需要服务器资源或必须包含在网页本身（例如隐藏字段）或 Cookie 中。
- 可以让 Jane 的更改覆盖 John 的更改。 下次有人浏览英语系时，他们将看到8/8/2013 和已还原的 $350000.00 值。 这称为“客户端优先”或“最后一个优先”。 （客户端的所有值优先于数据存储中的内容。）如本部分简介中所述，如果不执行任何并发处理编码，则会自动执行此操作。
- 您可以阻止在数据库中更新 Jane 的更改。 通常情况下，会显示一条错误消息，向她显示数据的当前状态，并允许她重新应用更改（如果她仍想要进行更改）。 这称为“存储优先”方案。 （数据存储值优先于客户端提交的值。）在本教程中，您将实施存储入选方案。 此方法可确保用户在未收到具体发生内容的警报时，不会覆盖任何更改。

### <a name="detecting-concurrency-conflicts"></a>检测并发冲突

可以通过处理实体框架引发的[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx)异常来解决冲突。 为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。 因此，你必须正确配置数据库和数据模型。 启用冲突检测的某些选项包括：

- 数据库表中包含一个可用于确定某行更改时间的跟踪列。 然后，可以将实体框架配置为将该列包含在 SQL `Update` 的 `Where` 子句中或 `Delete` 命令。

    跟踪列的数据类型通常为[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新行时递增的序列号。 在 `Update` 或 `Delete` 命令中，`Where` 子句包含跟踪列（原始行版本）的原始值。 如果正在更新的行已由其他用户更改，则 `rowversion` 列中的值与原始值不同，因此 `Update` 或 `Delete` 语句由于 `Where` 子句而无法找到要更新的行。 当实体框架发现 `Update` 或 `Delete` 命令没有更新任何行（即，受影响的行数为零时），它会将其解释为并发冲突。
- 将实体框架配置为在 `Update` 和 `Delete` 命令的 `Where` 子句中包含表中每一列的原始值。

    在第一个选项中，如果行中的任何内容在第一次读取后发生了更改，则 `Where` 子句将不返回要更新的行，实体框架会将其解释为并发冲突。 对于包含多个列的数据库表，此方法可能会产生非常大的 `Where` 子句，并可能要求你维护大量状态。 如前所述，维持大量的状态会影响应用程序的性能。 因此通常不建议使用此方法，并且它也不是本教程中使用的方法。

    如果确实要实现这种并发方法，则必须将[ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)属性添加到要跟踪其并发的实体中的所有非主键属性。 通过此更改，实体框架可以在 `UPDATE` 语句的 SQL `WHERE` 子句中包含所有列。

在本教程的剩余部分中，你将[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)跟踪属性添加到 `Department` 实体、创建控制器和视图，并进行测试以验证一切是否正常工作。

## <a name="add-optimistic-concurrency"></a>添加乐观并发

在*Models\Department.cs*中，添加一个名为 `RowVersion`的跟踪属性：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)特性指定此列将包含在发送到数据库的 `Update` 和 `Delete` 命令的 `Where` 子句中。 此属性被称为[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)，这是因为以前版本的 SQL SERVER 在 sql [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)将其替换之前使用 sql [Timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)数据类型。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)的 .net 类型是字节数组。

如果希望使用 Fluent API，可以使用[IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)方法来指定跟踪属性，如以下示例中所示：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

通过添加属性，更改了数据库模型，因此需要再执行一次迁移。 在包管理器控制台 (PMC) 中输入以下命令：

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-department-controller"></a>修改部门控制器

在*Controllers\DepartmentController.cs*中，添加一个 `using` 语句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

在*DepartmentController.cs*文件中，将 "LastName" 的所有四个匹配项更改为 "FullName"，以便 "部门管理员" 下拉列表将包含讲师的全名，而不只是姓氏。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

将 `HttpPost` `Edit` 方法的现有代码替换为以下代码：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

如果 `FindAsync` 方法返回 NULL，则该院系已被另一用户删除。 显示的代码使用已发布的窗体值创建部门实体，以便可以使用错误消息重新显示 "编辑" 页。 或者，如果仅显示错误消息而未重新显示院系字段，则不必重新创建 Department 实体。

视图将原始 `RowVersion` 值存储在隐藏字段中，方法在 `rowVersion` 参数中接收它。 在调用 `SaveChanges` 之前，必须将该原始 `RowVersion` 属性值置于实体的 `OriginalValues` 集合中。 当实体框架创建 SQL `UPDATE` 命令时，该命令将包含一个 `WHERE` 子句，该子句将查找具有原始 `RowVersion` 值的行。

如果 `UPDATE` 命令（没有行具有原始 `RowVersion` 值）不影响任何行，实体框架将引发 `DbUpdateConcurrencyException` 异常，而 `catch` 块中的代码将从异常对象获取受影响的 `Department` 实体。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

此对象具有用户在其 `Entity` 属性中输入的新值，你可以通过调用 `GetDatabaseValues` 方法获取从数据库中读取的值。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

如果有人删除了数据库中的行，则 `GetDatabaseValues` 方法返回 null;否则，你必须将返回的对象强制转换为 `Department` 类，才能访问 `Department` 属性。 （由于你已检查删除，`databaseEntry` 仅当在 `FindAsync` 执行之后以及 `SaveChanges` 执行之前删除了该部门时才为 null。）

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

接下来，代码为其数据库值不同于在 "编辑" 页上输入的数据库值的每个列添加一条自定义错误消息：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

更长的错误消息说明发生了什么情况以及如何处理它：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

最后，该代码将 `Department` 对象的 `RowVersion` 值设置为从数据库中检索到的新值。 重新显示“编辑”页时，这个新的 `RowVersion` 值将存储在隐藏字段中，当用户下次单击“保存”时，将只捕获自“编辑”页重新显示起发生的并发错误。

在*Views\Department\Edit.cshtml*中，添加隐藏字段以保存 `RowVersion` 属性值，紧跟在 `DepartmentID` 属性的隐藏字段之后：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="test-concurrency-handling"></a>测试并发处理

运行站点并单击 "**部门**"。

右键单击英语系的 "**编辑**" 超链接，然后选择 "**在新选项卡中打开"，** 然后单击英语系的 "**编辑**" 超链接。 这两个选项卡显示相同的信息。

在第一个浏览器选项卡中更改一个字段，然后单击“保存”。

浏览器显示具有更改值的索引页。

在第二个浏览器选项卡中更改字段，然后单击 "**保存**"。 看见一条错误消息：

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

再次单击“保存”。 在第二个浏览器选项卡中输入的值与在第一个浏览器中更改的数据的原始值一起保存。 在索引页中出现时，可以看到已保存的值。

## <a name="update-the-delete-page"></a>更新“删除”页

对于“删除”页，Entity Framework 以类似方式检测其他人编辑院系所引起的并发冲突。 当 "`HttpGet` `Delete`" 方法显示 "确认" 视图时，该视图将在隐藏字段中包含原始 `RowVersion` 值。 然后，该值可供用户确认删除时调用的 `HttpPost` `Delete` 方法使用。 当实体框架创建 SQL `DELETE` 命令时，它将包含一个具有原始 `RowVersion` 值的 `WHERE` 子句。 如果命令导致0行受影响（也就是说，在显示 "删除确认" 页面后更改了该行），则会引发并发异常，并会调用 `HttpGet Delete` 方法，并将错误标志设置为 "`true`" 以重新显示包含错误消息的确认页面。 因为行已被其他用户删除，所以也可能会影响零行，因此在这种情况下，将显示不同的错误消息。

在*DepartmentController.cs*中，将 `HttpGet` `Delete` 方法替换为以下代码：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

该方法接受可选参数，该参数指示是否在并发错误之后重新显示页面。 如果 `true`此标志，则会使用 `ViewBag` 属性将错误消息发送到视图。

将 `HttpPost` `Delete` 方法中的代码替换 `DeleteConfirmed`为以下代码：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

在刚替换的基架代码中，此方法仅接受记录 ID：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

已将此参数更改为模型绑定器创建的 `Department` 实体实例。 这使你除了记录键外，还可以访问 `RowVersion` 属性值。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。 `HttpPost` 的名为的基架代码 `Delete` 方法 `DeleteConfirmed` 为 `HttpPost` 方法指定唯一签名。 （CLR 要求重载方法具有不同的方法参数。）签名是唯一的，可以坚持使用 MVC 约定，并为 `HttpPost` 和 `HttpGet` delete 方法使用相同的名称。

如果捕获到并发错误，代码将重新显示“删除”确认页，并提供一个指示它应显示并发错误消息的标志。

在*Views\Department\Delete.cshtml*中，将基架代码替换为以下代码，以便为 DepartmentID 和 RowVersion 属性添加错误消息字段和隐藏字段。 突出显示所作更改。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

此代码在 `h2` 和 `h3` 标题之间添加错误消息：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

它将 `LastName` 替换为 `Administrator` 字段中 `FullName`：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

最后，它将添加 `DepartmentID` 的隐藏字段，并在 `Html.BeginForm` 语句后 `RowVersion` 属性：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

运行 "部门索引" 页。 右键单击英语系的 "**删除**" 超链接，然后选择 "**在新选项卡中打开"，** 然后在第一个选项卡中，单击英语系的 "**编辑**" 超链接。

在第一个窗口中，更改其中一个值，然后单击 "**保存**"。

索引页确认更改。

在第二个选项卡中，单击“删除”。

你将看到并发错误消息，且已使用数据库中的当前内容刷新了“院系”值。

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

如果再次单击“删除”，会重定向到已删除显示院系的索引页。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

有关处理各种并发方案的其他方法的信息，请参阅 MSDN 上的[乐观并发模式](https://msdn.microsoft.com/data/jj592904)和使用[属性值](https://msdn.microsoft.com/data/jj592677)。 下一教程介绍如何实现 `Instructor` 和 `Student` 实体的每个层次结构一个表继承。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 已了解并发冲突
> * 添加了开放式并发
> * 修改的部门控制器
> * 已测试并发处理
> * 已更新“删除”页

转到下一篇文章，了解如何在数据模型中实现继承。
> [!div class="nextstepaction"]
> [在数据模型中实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
