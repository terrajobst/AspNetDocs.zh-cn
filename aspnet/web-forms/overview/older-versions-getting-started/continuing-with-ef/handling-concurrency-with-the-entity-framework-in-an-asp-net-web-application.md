---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: 处理 ASP.NET 4 Web 应用程序中与实体框架4.0 的并发操作 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513500"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>使用 ASP.NET 4 Web 应用程序中的实体框架4.0 处理并发

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本教程系列在[使用实体框架 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。

在上一教程中，您学习了如何使用 `ObjectDataSource` 控件和实体框架对数据进行排序和筛选。 本教程介绍用于在使用实体框架的 ASP.NET web 应用程序中处理并发的选项。 你将创建专用于更新讲师办公室分配的新网页。 你将在该页面和前面创建的部门页中处理并发问题。

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>并发冲突

当一个用户编辑记录，而另一个用户在第一个用户的更改写入数据库之前编辑同一个记录时，将发生并发冲突。 如果未设置实体框架来检测此类冲突，则数据库的任何更新将最后覆盖其他用户所做的更改。 在许多应用程序中，此风险是可接受的，无需将应用程序配置为处理可能的并发冲突。 （如果有很少的用户或较少的更新，或者如果某些更改被覆盖，就不是真的很重要，则并发编程的成本可能会超出权益。）如果无需担心并发冲突，则可以跳过本教程;本系列中的其余两个教程不依赖于您在此中生成的任何内容。

### <a name="pessimistic-concurrency-locking"></a>悲观并发（锁定）

如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。 这称为 "*悲观并发*"。 例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。 如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为他们得到的是正在更改的数据的副本。 如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。

管理锁有一些缺点。 编程可能很复杂。 它需要大量的数据库管理资源，如果应用程序的用户数增加（也就是说，它不能很好地进行缩放），则可能会导致性能问题。 由于这些原因，并不是所有的数据库管理系统都支持悲观并发。 实体框架不提供对它的内置支持，本教程不会演示如何实现它。

### <a name="optimistic-concurrency"></a>开放式并发

保守式并发的替代方法是*乐观并发*。 悲观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。 例如，John 运行 "node.js *" 页，* 单击历史记录部门的 "**编辑**" 链接，并将**预算**量从 $1000000.00 减少到 $125000.00。 （John 管理竞争部门，希望为自己的部门腾出资金。）

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John 单击 "**更新**" 之前，Jane 运行相同的页面，单击历史记录部门的 "**编辑**" 链接，然后将 "**开始日期**" 字段从1/10/2011 更改为1/1/1999。 （Jane 管理历史部门并想要为其增加资历。）

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

John 单击 "**更新**"，然后单击 "**更新**"。 Jane 的浏览器现在列出了**预算**金额为 $1000000.00，但这是不正确的，因为金额已由 John 更改为 $125000.00。

在此方案中，您可以执行以下操作：

- 可以跟踪用户已修改的属性，并仅更新数据库中相应的列。 在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。 下次有人浏览历史记录部门时，他们将看到1/1/1999 和 $125000.00。 

    这是实体框架中的默认行为，它可以显著减少可能导致数据丢失的冲突数。 但是，如果对实体的相同属性进行了竞争性更改，则此行为不会导致数据丢失。 此外，此行为并非总是可行;在将存储过程映射到实体类型时，会在数据库中对实体进行任何更改时，更新实体的所有属性。
- 可以让 Jane 的更改覆盖 John 的更改。 Jane 单击 "**更新**" 后，**预算**量会恢复为 $1000000.00。 这称为“客户端优先”或“最后一个优先”。 （客户端的值优先于数据存储中的内容。）
- 您可以阻止在数据库中更新 Jane 的更改。 通常情况下，会显示一条错误消息，向她显示数据的当前状态，并允许她在仍想要进行更改时重新输入其更改。 您可以通过保存输入来进一步实现过程的自动化，并使她有机会重新应用它，而无需重新输入。 这称为“存储优先”方案。 （数据存储值优先于客户端提交的值。）

### <a name="detecting-concurrency-conflicts"></a>检测并发冲突

在实体框架中，可以通过处理实体框架引发的 `OptimisticConcurrencyException` 异常来解决冲突。 为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。 因此，你必须正确配置数据库和数据模型。 启用冲突检测的某些选项包括：

- 在数据库中，包含一个可用于确定行更改时间的表列。 然后，可以将实体框架配置为将该列包含在 SQL `Update` 的 `Where` 子句中或 `Delete` 命令。

    这就是 `OfficeAssignment` 表中 `Timestamp` 列的目的。

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    `Timestamp` 列的数据类型也称为 `Timestamp`。 但是，此列实际上不包含日期或时间值。 相反，此值是每次更新行时递增的序列号。 在 `Update` 或 `Delete` 命令中，`Where` 子句包含原始 `Timestamp` 值。 如果正在更新的行已由其他用户更改，则 `Timestamp` 中的值与原始值不同，因此 `Where` 子句返回无要更新的行。 如果实体框架发现当前 `Update` 或 `Delete` 命令未更新任何行（即，受影响的行数为零时），则会将其解释为并发冲突。
- 将实体框架配置为在 `Update` 和 `Delete` 命令的 `Where` 子句中包含表中每一列的原始值。

    在第一个选项中，如果行中的任何内容在第一次读取后发生了更改，则 `Where` 子句将不返回要更新的行，实体框架会将其解释为并发冲突。 此方法与使用 `Timestamp` 字段一样有效，但可能效率低下。 对于包含多个列的数据库表，它可能会产生非常大的 `Where` 子句，在 web 应用程序中，它可以要求您维护大量的状态。 维护大量状态可能会影响应用程序性能，因为它需要服务器资源（例如会话状态）或必须包含在网页本身中（例如，视图状态）。

在本教程中，您将为没有跟踪属性（`Department` 实体）的实体和具有跟踪属性（`OfficeAssignment` 实体）的实体添加乐观并发冲突的错误处理。

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>处理无跟踪属性的开放式并发

若要为不具有跟踪（`Timestamp`）属性的 `Department` 实体实现开放式并发，你将完成以下任务：

- 更改数据模型，为 `Department` 实体启用并发跟踪。
- 在 `SchoolRepository` 类中，处理 `SaveChanges` 方法中的并发异常。
- 在 " *default.aspx* " 页中，通过向用户显示一条消息来处理并发异常，警告尝试的更改失败。 然后，用户可以查看当前值，并在需要时重试更改。

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>在数据模型中启用并发跟踪

在 Visual Studio 中，打开在本系列前面的教程中使用的 Contoso 大学 web 应用程序。

打开*SchoolModel*，并在数据模型设计器中右键单击 `Department` 实体中的 `Name` 属性，然后单击 "**属性**"。 在 "**属性**" 窗口中，将 "`ConcurrencyMode`" 属性更改为 "`Fixed`"。

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

对其他非主键标量属性（`Budget`、`StartDate`和 `Administrator`执行相同的操作。）（不能对导航属性执行此操作。）这指定每当实体框架生成 `Update` 或 `Delete` SQL 命令以更新数据库中的 `Department` 实体时，都必须在 `Where` 子句中包含这些列（具有原始值）。 如果在执行 `Update` 或 `Delete` 命令时找不到任何行，实体框架将引发乐观并发异常。

保存并关闭数据模型。

### <a name="handling-concurrency-exceptions-in-the-dal"></a>在 DAL 中处理并发异常

打开*SchoolRepository.cs* ，并为 `System.Data` 命名空间添加以下 `using` 语句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

添加以下新的 `SaveChanges` 方法，该方法处理开放式并发异常：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

如果在调用此方法时出现并发错误，则会将内存中实体的属性值替换为当前数据库中的值。 引发并发异常，使网页能够处理该异常。

在 `DeleteDepartment` 和 `UpdateDepartment` 方法中，将对 `context.SaveChanges()` 的现有调用替换为对 `SaveChanges()` 的调用，以便调用新方法。

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>处理表示层中的并发异常

打开 "*部门*" 并向 `DepartmentsObjectDataSource` 控件添加 `OnDeleted="DepartmentsObjectDataSource_Deleted"` 特性。 控件的开始标记现在将类似于下面的示例。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

在 `DepartmentsGridView` 控件中，指定 `DataKeyNames` 属性中的所有表列，如以下示例中所示。 请注意，这将创建非常大的视图状态字段，这是使用跟踪字段通常是跟踪并发冲突的首选方式的一个原因。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

打开*Departments.aspx.cs* ，并为 `System.Data` 命名空间添加以下 `using` 语句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

添加以下新方法，将从数据源控件的 `Updated` 调用该方法，并 `Deleted` 事件处理程序来处理并发异常：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

此代码检查异常类型，如果它是并发异常，则代码会动态创建一个 `CustomValidator` 控件，该控件随后会在 `ValidationSummary` 控件中显示一条消息。

从前面添加的 `Updated` 事件处理程序调用新方法。 此外，请创建一个调用相同方法的新 `Deleted` 事件处理程序（但不执行任何其他操作）：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>在 "部门" 页中测试开放式并发

运行 " *node.js" 页。*

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

单击行中的 "**编辑**" 并更改 "**预算**" 列中的值。 （请记住，只能编辑为本教程创建的记录，因为现有 `School` 数据库记录包含一些无效数据。 经济部门的记录是一种安全的记录。）

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

打开新的浏览器窗口并再次运行该页（将 URL 从第一个浏览器窗口的地址框复制到第二个浏览器窗口）。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

在之前编辑的同一行中单击 "**编辑**"，并将**预算**值更改为其他值。

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

在第二个浏览器窗口中，单击 "**更新**"。 **预算**金额已成功更改为此新值。

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

在第一个浏览器窗口中，单击 "**更新**"。 更新失败。 将使用你在第二个浏览器窗口中设置的值重新显示**预算**金额，并且你将看到一条错误消息。

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>使用跟踪属性处理开放式并发

若要为具有跟踪属性的实体处理开放式并发，你需要完成以下任务：

- 向数据模型添加存储过程以管理 `OfficeAssignment` 实体。 （跟踪属性和存储过程不一定要一起使用; 它们只是组合在这里，以便进行说明。）
- 将 CRUD 方法添加到 DAL，并将 BLL 添加到 `OfficeAssignment` 实体的 BLL，其中包括用于处理 DAL 中的开放式并发异常的代码。
- 创建 office 分配网页。
- 测试新网页中的开放式并发。

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>将 OfficeAssignment 存储过程添加到数据模型

在模型设计器中打开*SchoolModel*文件，右键单击设计图面，然后单击 "**从数据库更新模型**"。 在 "**选择数据库对象**" 对话框的 "**添加**" 选项卡中，展开 "**存储过程**" 并选择三个 `OfficeAssignment` 存储过程（请参阅以下屏幕截图），然后单击 "**完成**"。 （当您使用脚本下载或创建这些存储过程时，它们已在数据库中。）

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

右键单击 "`OfficeAssignment`" 实体，然后选择 "**存储过程映射**"。

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

设置**插入**、**更新**和**删除**函数以使用其相应的存储过程。 对于 `Update` 函数的 `OrigTimestamp` 参数，将**属性**设置为 `Timestamp`，然后选择 "**使用原始值**" 选项。

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

当实体框架调用 `UpdateOfficeAssignment` 存储过程时，它将传递 `OrigTimestamp` 参数中 `Timestamp` 列的原始值。 存储过程在其 `Where` 子句中使用此参数：

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

该存储过程还会在更新后选择 `Timestamp` 列的新值，以便实体框架可以将内存中的 `OfficeAssignment` 实体与相应的数据库行保持同步。

（请注意，删除 office 分配的存储过程没有 `OrigTimestamp` 的参数。 因此，在删除之前，实体框架无法验证实体是否已更改。）

保存并关闭数据模型。

### <a name="adding-officeassignment-methods-to-the-dal"></a>将 OfficeAssignment 方法添加到 DAL

打开*ISchoolRepository.cs*并为 `OfficeAssignment` 实体集添加以下 CRUD 方法：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

将以下新方法添加到*SchoolRepository.cs*。 在 `UpdateOfficeAssignment` 方法中，调用本地 `SaveChanges` 方法而不是 `context.SaveChanges`。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

在测试项目中，打开*MockSchoolRepository.cs* ，并向其添加以下 `OfficeAssignment` 集合和 CRUD 方法。 （Mock 存储库必须实现存储库接口，否则解决方案将不会编译。）

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>将 OfficeAssignment 方法添加到 BLL

在主项目中，打开*SchoolBL.cs*并为其添加以下用于 `OfficeAssignment` 实体集的 CRUD 方法：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>创建 OfficeAssignments 网页

创建一个使用*网站母版页*的新网页，并将其命名为*OfficeAssignments*。 将以下标记添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

请注意，在 `DataKeyNames` 特性中，标记指定了 `Timestamp` 属性以及记录键（`InstructorID`）。 在 `DataKeyNames` 特性中指定属性将导致控件以控件状态（类似于视图状态）保存这些属性，以便在回发处理期间原始值可用。

如果未保存 `Timestamp` 值，则实体框架不会将其用于 SQL `Update` 命令的 `Where` 子句。 因此，无需进行更新。 因此，每次更新 `OfficeAssignment` 实体时，实体框架都将引发乐观并发异常。

打开*OfficeAssignments.aspx.cs*并为数据访问层添加以下 `using` 语句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

添加以下 `Page_Init` 方法，该方法可启用动态数据功能。 此外，为 `ObjectDataSource` 控件的 `Updated` 事件添加以下处理程序，以检查并发错误：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>在 OfficeAssignments 页中测试开放式并发

运行*OfficeAssignments*页。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

单击行中的 "**编辑**" 并更改 "**位置**" 列中的值。

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

打开新的浏览器窗口，并再次运行页面（将 URL 从第一个浏览器窗口复制到第二个浏览器窗口）。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

在之前编辑的同一行中单击 "**编辑**"，并将 "**位置**" 值更改为其他值。

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

在第二个浏览器窗口中，单击 "**更新**"。

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

切换到第一个浏览器窗口，然后单击 "**更新**"。

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

你将看到一条错误消息，并且**位置**值已更新，以显示在第二个浏览器窗口中更改它的值。

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>用 EntityDataSource 控件处理并发

`EntityDataSource` 控件包括内置逻辑，该逻辑识别数据模型中的并发设置并相应地处理更新和删除操作。 但是，与所有异常一样，你必须自行处理 `OptimisticConcurrencyException` 异常，以便提供用户友好的错误消息。

接下来，您将配置 "*课程 .aspx* " 页（使用 `EntityDataSource` 控件）以允许更新和删除操作，并在发生并发冲突时显示错误消息。 `Course` 实体没有并发跟踪列，因此将使用与 `Department` 实体相同的方法：跟踪所有非键属性的值。

打开*SchoolModel*文件。 对于 `Course` 实体的非键属性（`Title`、`Credits`和 `DepartmentID`），请将 "**并发模式**" 属性设置为 "`Fixed`"。 然后保存并关闭数据模型。

打开 " *default.aspx* " 页并进行以下更改：

- 在 `CoursesEntityDataSource` 控件中，添加 `EnableUpdate="true"` 和 `EnableDelete="true"` 特性。 该控件的开始标记现在类似于以下示例：

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- 在 `CoursesGridView` 控件中，将 `DataKeyNames` 属性值更改为 "`"CourseID,Title,Credits,DepartmentID"`"。 然后，将 `CommandField` 元素添加到显示 "**编辑**" 和 "**删除**" 按钮的 `Columns` 元素（`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`）。 `GridView` 控件现在类似于以下示例：

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

运行页面，并在 "部门" 页中创建一个冲突情况。 在两个浏览器窗口中运行该页面，在每个窗口的同一行中单击 "**编辑**"，并在每个窗口中进行不同更改。 在一个窗口中单击 "**更新**"，然后在另一个窗口中单击 "**更新**"。 第二次单击 "**更新**" 时，会看到由未处理的并发异常导致的错误页。

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

处理此错误的方式非常类似于针对 `ObjectDataSource` 控件处理此错误的方式。 打开 " *default.aspx* " 页，然后在 "`CoursesEntityDataSource`" 控件中，为 `Deleted` 和 `Updated` 事件指定处理程序。 控件的开始标记现在类似于以下示例：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

在 `CoursesGridView` 控件之前，添加以下 `ValidationSummary` 控件：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

在*Courses.aspx.cs*中，添加 `System.Data` 命名空间的 `using` 语句，添加检查并发异常的方法，并为 `EntityDataSource` 控件的 `Updated` 和 `Deleted` 处理程序添加处理程序。 该代码将如下所示：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

此代码与你为 `ObjectDataSource` 控件执行的操作的唯一区别在于，在这种情况下，并发异常位于事件参数对象的 `Exception` 属性中，而不是在该异常的 `InnerException` 属性中。

运行该页并再次创建并发冲突。 此时将显示一条错误消息：

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

处理并发冲突已介绍完毕。 下一教程将提供有关如何在使用实体框架的 web 应用程序中提高性能的指南。

> [!div class="step-by-step"]
> [上一页](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [下一页](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
