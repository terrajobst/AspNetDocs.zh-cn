---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: 使用 ASP.NET 4 Web 应用程序中的实体框架4.0 最大化性能 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5630200a1ad1d30f6d89b38e15179f15b699fa9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439262"
---
# <a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>在 ASP.NET 4 Web 应用程序中最大化实体框架4.0 的性能

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本教程系列在[使用实体框架 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。

在上一教程中，你已了解如何处理并发冲突。 本教程介绍了用于提高使用实体框架的 ASP.NET web 应用程序的性能的选项。 你将学习多种方法来最大程度地提高性能或诊断性能问题。

以下部分中提供的信息在各种情况下可能非常有用：

- 有效地加载相关数据。
- 管理视图状态。

如果你的单个查询显示了性能问题，以下部分中提供的信息可能会很有用：

- 使用 `NoTracking` merge "选项。
- 预编译 LINQ 查询。
- 检查发送到数据库的查询命令。

以下部分中提供的信息对于具有极大数据模型的应用程序可能很有用：

- 预生成视图。

> [!NOTE]
> Web 应用程序性能受多种因素的影响，其中包括请求和响应数据的大小、数据库查询的速度、服务器可以排队的请求数，甚至还会提高任何你可能使用的客户端脚本库。 如果性能在您的应用程序中很重要，或者测试或经验表明应用程序性能不满意，则您应该遵循正常的协议来优化性能。 度量来确定性能瓶颈的发生位置，并解决将对总体应用程序性能产生最大影响的区域。
> 
> 本主题主要介绍一些方法，你可以利用这些方法提高 ASP.NET 中特定实体框架的性能。 如果确定数据访问是应用程序中的性能瓶颈之一，则此处的建议非常有用。 除了前面所述的方法，不应将此处所述的方法视为 &quot;最佳&quot; 实践，其中的许多方法仅适用于异常情况或解决特定类型的性能瓶颈。

若要开始学习本教程，请启动 Visual Studio，并打开在上一教程中使用的 Contoso 大学 web 应用程序。

## <a name="efficiently-loading-related-data"></a>有效加载相关数据

实体框架可以通过多种方式将相关数据加载到实体的导航属性中：

- *延迟加载*。 首次读取实体时，不检索相关数据。 然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。 这会导致向数据库发送多个查询，一个用于实体本身，每次必须检索到该实体的相关数据。 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*预先加载*。 读取该实体时，会同时检索相关数据。 此时通常会出现单一联接查询，检索所有必需数据。 您可以使用 `Include` 方法指定预先加载，如您在这些教程中已已看到。

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *显式加载*。 这类似于延迟加载，只不过是在代码中显式检索相关数据;在访问导航属性时，不会自动发生此情况。 您可以使用集合的导航属性的 `Load` 方法手动加载相关数据，也可以使用包含单个对象的属性的 reference 属性的 `Load` 方法。 （例如，调用 `PersonReference.Load` 方法来加载 `Department` 实体的 `Person` 导航属性。）

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

因为它们不会立即检索属性值，所以延迟加载和显式加载也称为*延迟加载*。

延迟加载是由设计器生成的对象上下文的默认行为。 如果打开定义对象上下文类的*SchoolModel.Designer.cs*文件，会发现三个构造函数方法，其中每个方法都包含以下语句：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

通常，如果您知道每个检索到的实体都需要相关数据，预先加载可提供最佳性能，因为发送到数据库的单个查询通常比检索的每个实体的单独查询更有效。 另一方面，如果你只需要访问实体的导航属性，而不经常或只是一小部分实体，则延迟加载或显式加载可能会更有效，因为预先加载将检索比你需要的更多的数据。

在 web 应用程序中，延迟加载可能会相对较小的值，因为影响相关数据的需要的用户操作在浏览器中进行，该操作不会连接到呈现该页的对象上下文。 另一方面，在对控件进行数据绑定时，通常会知道所需的数据，因此，通常最好是根据每个方案中的适当内容选择预先加载或延迟加载。

此外，在释放对象上下文之后，数据绑定控件可能会使用实体对象。 在这种情况下，延迟加载导航属性的尝试会失败。 您收到的错误消息是清晰的： &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

默认情况下，`EntityDataSource` 控件禁用延迟加载。 对于当前教程使用的 `ObjectDataSource` 控件（或从页代码访问对象上下文），可以通过多种方式在默认情况下禁用延迟加载。 您可以在实例化对象上下文时禁用它。 例如，你可以将以下行添加到 `SchoolRepository` 类的构造函数方法：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

对于 Contoso 大学应用程序，你将使对象上下文自动禁用延迟加载，以便每次实例化上下文时不必设置此属性。

打开*SchoolModel*数据模型，单击设计图面，然后在 "属性" 窗格中将 "**已启用延迟加载**" 属性设置为 `False`。 保存并关闭数据模型。

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>管理视图状态

为了提供更新功能，ASP.NET 网页在呈现页时必须存储实体的原始属性值。 在回发过程中，控件在应用更改和调用 `SaveChanges` 方法之前，可以重新创建实体的原始状态并调用实体的 `Attach` 方法。 默认情况下，ASP.NET Web 窗体数据控件使用视图状态存储原始值。 但是，视图状态可能会影响性能，因为它存储在隐藏字段中，这可能会显著增加发送到浏览器或从浏览器中发送的页的大小。

用于管理视图状态的技术或会话状态等替代方法对实体框架不唯一，因此本教程不会详细介绍本主题。 有关详细信息，请参阅本教程末尾的链接。

但是，ASP.NET 的版本4提供了一种使用视图状态的新方法，即 Web 窗体应用程序的每个 ASP.NET 开发人员都应注意： `ViewStateMode` 属性。 此新属性可在页面或控件级别设置，并且它使你能够默认禁用页面的视图状态，并仅为需要它的控件启用视图状态。

对于性能至关重要的应用程序，最佳做法是始终禁用页面级别的视图状态，并只为需要它的控件启用视图状态。 Contoso 大学页面的视图状态大小不会通过此方法大幅降低，但若要查看其工作原理，请在 "*指导员*" 页中执行此操作。 该页包含许多控件，包括禁用了视图状态的 `Label` 控件。 此页上的控件都不需要启用视图状态。 （`GridView` 控件的 `DataKeyNames` 属性指定必须在两次回发之间维护的状态，但这些值保留在控件状态中，这不受 `ViewStateMode` 属性的影响。）

`Page` 指令和 `Label` 控件标记当前与以下示例类似：

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

进行以下更改：

- 向 `Page` 指令添加 `ViewStateMode="Disabled"`。
- 从 `Label` 控件中删除 `ViewStateMode="Disabled"`。

标记现在类似于以下示例：

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

所有控件的视图状态现在均处于禁用状态。 如果以后添加的控件需要使用视图状态，则只需包含该控件的 `ViewStateMode="Enabled"` 属性即可。

## <a name="using-the-notracking-merge-option"></a>使用 NoTracking 合并选项

当对象上下文检索数据库行并创建表示它们的实体对象时，默认情况下，它还会使用其对象状态管理器跟踪这些实体对象。 此跟踪数据作为缓存，并在更新实体时使用。 由于 web 应用程序通常具有生存期较短的对象上下文实例，因此查询经常返回无需跟踪的数据，因为读取这些数据的对象上下文将在它所读取的任何实体再次使用或更新之前被释放。

在实体框架中，可以通过设置*merge 选项*来指定对象上下文是否跟踪实体对象。 您可以为单个查询或实体集设置合并选项。 如果为实体集设置了此选项，则意味着要为为该实体集创建的所有查询设置默认合并选项。

对于 Contoso 大学应用程序，从存储库访问的任何实体集都不需要进行跟踪，因此，在存储库类中的对象上下文时，可以将 merge 选项设置为对这些实体集 `NoTracking`。 （请注意，在本教程中，设置 "合并" 选项不会对应用程序的性能产生显著影响。 `NoTracking` 选项可能仅在某些高数据量方案下才能获得明显的性能改进。）

在 DAL 文件夹中，打开*SchoolRepository.cs*文件并添加构造函数方法，该方法用于设置存储库访问的实体集的合并选项：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>预编译 LINQ 查询

第一次实体框架在给定 `ObjectContext` 实例的生存期内执行实体 SQL 查询时，编译该查询需要一些时间。 编译的结果是缓存的，这意味着查询的后续执行速度要快得多。 LINQ 查询遵循类似的模式，但在每次执行查询时都要执行一些编译查询所需的工作。 换言之，对于 LINQ 查询，默认情况下不会缓存所有编译结果。

如果你的 LINQ 查询希望在对象上下文的生存期内重复运行，则可以编写代码，以在首次运行 LINQ 查询时缓存所有编译结果。

作为说明，你将对 `SchoolRepository` 类中的两个 `Get` 方法执行此操作，其中一种方法不使用任何参数（`GetInstructorNames` 方法），而是需要参数（`GetDepartmentsByAdministrator` 方法）的两种方法。 这些方法在实际情况中是不需要编译的，因为它们不是 LINQ 查询：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

但是，您可以尝试编译查询，就像编写为以下 LINQ 查询一样：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

你可以将这些方法中的代码更改为上面显示的内容，并运行应用程序以验证其是否正常工作，然后再继续。 但下面的说明直接介绍了如何创建预编译的版本。

在*DAL*文件夹中创建一个类文件，将其命名为*SchoolEntities.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

此代码创建一个用于扩展自动生成的对象上下文类的分部类。 分部类包含使用 `CompiledQuery` 类的 `Compile` 方法的两个已编译的 LINQ 查询。 它还会创建可用于调用查询的方法。 保存并关闭此文件。

接下来，在*SchoolRepository.cs*中，更改存储库类中的现有 `GetInstructorNames` 和 `GetDepartmentsByAdministrator` 方法，使其调用已编译的查询：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

运行 " *node.js" 页，验证*其工作方式是否与以前相同。 为了填充 "管理员" 下拉列表，将调用 `GetInstructorNames` 方法，当您单击 "**更新**" 时，将调用 `GetDepartmentsByAdministrator` 方法来验证没有任何教师是多个部门的管理员。

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

你已经在 Contoso 大学应用程序中预先编译了查询来了解如何执行此操作，而不是因为它会显著提高性能。 预编译 LINQ 查询确实会增加代码的复杂性，因此请确保仅对实际表示应用程序中性能瓶颈的查询执行此操作。

## <a name="examining-queries-sent-to-the-database"></a>检查发送到数据库的查询

在调查性能问题时，有时知道实体框架要发送到数据库的确切 SQL 命令会很有帮助。 如果使用的是 `IQueryable` 对象，则执行此操作的一种方法是使用 `ToTraceString` 方法。

在*SchoolRepository.cs*中，更改 `GetDepartmentsByName` 方法中的代码，使其与以下示例匹配：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

必须仅将 `departments` 变量强制转换为 `ObjectQuery` 类型，因为上述行末尾的 `Where` 方法会创建 `IQueryable` 对象;如果没有 `Where` 方法，则不需要强制转换。

在 `return` 行上设置断点，然后在调试器中运行 *"node.js" 页。* 命中断点时，查看 "**局部变量**" 窗口中的 `commandText` 变量，并使用文本可视化工具（"**值**" 列中的放大镜）在 "**文本可视化工具**" 窗口中显示其值。 你可以看到此代码生成的整个 SQL 命令：

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

作为替代方法，Visual Studio Ultimate 中的 IntelliTrace 功能提供了一种方法，用于查看不需要更改代码甚至设置断点的实体框架生成的 SQL 命令。

> [!NOTE]
> 只有在 Visual Studio Ultimate 的情况下，才能执行以下过程。

还原 `GetDepartmentsByName` 方法中的原始代码，然后在调试器中运行 "node.js *" 页。*

在 Visual Studio 中，选择 "**调试**" 菜单，然后依次选择 " **intellitrace**" 和 " **intellitrace 事件**"。

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

在**IntelliTrace**窗口中，单击 "**全部中断**"。

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

**IntelliTrace**窗口显示最近事件的列表：

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

单击**ADO.NET**行。 它将展开以显示命令文本：

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

可以从 "**局部变量**" 窗口将整个命令文本字符串复制到剪贴板。

假设您使用的数据库的表、关系和列比简单的 `School` 数据库多。 您可能会发现，收集包含多个 `Join` 子句的单个 `Select` 语句中所需的所有信息的查询变得过于复杂，无法高效工作。 在这种情况下，可以从预先加载切换到显式加载，以简化查询。

例如，尝试在*SchoolRepository.cs*中更改 `GetDepartmentsByName` 方法中的代码。 当前在该方法中，有一个对象查询，该查询具有 `Person` 和 `Courses` 导航属性的 `Include` 方法。 将 `return` 语句替换为执行显式加载的代码，如以下示例中所示：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

在调试器中运行 "node.js *" 页，* 并再次检查 " **IntelliTrace** " 窗口。 现在，在之前有单个查询，您会看到一条很长的序列。

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

单击第一个 " **ADO.NET** " 行，查看之前查看的复杂查询发生了什么情况。

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

来自部门的查询已成为一种不带 `Join` 子句的简单 `Select` 查询，但后面跟有用于检索相关课程和管理员的单独查询，该查询对原始查询返回的每个部门使用一组两个查询。

> [!NOTE]
> 如果保持启用延迟加载，则可能会由于延迟加载而导致在此处看到的模式重复多次。 通常要避免的一种模式是延迟加载主表中每一行的相关数据。 除非已验证单个联接查询太复杂，无法高效工作，否则，您通常可以通过将主查询更改为使用预先加载来提高此类情况下的性能。

## <a name="pre-generating-views"></a>预生成视图

第一次在新的应用程序域中创建 `ObjectContext` 对象时，实体框架将生成一组用于访问数据库的类。 这些类称为*视图*，如果你有一个非常大的数据模型，则生成这些视图会在新的应用程序域初始化之后延迟网站对第一个页面请求的响应。 可以通过在编译时（而不是在运行时）创建视图来减少此第一次请求延迟。

> [!NOTE]
> 如果您的应用程序没有非常大的数据模型，或者它具有大型数据模型，但您不关心在回收 IIS 之后只影响第一个页面请求的性能问题，则可以跳过此部分。 每次实例化 `ObjectContext` 对象时都不会发生视图创建，因为视图缓存在应用程序域中。 因此，除非经常在 IIS 中回收应用程序，否则非常少的页面请求将从预先生成的视图中获益。

您可以使用*edmgen.exe*命令行工具或通过使用*文本模板转换工具包*（T4）模板来预生成视图。 在本教程中，您将使用 T4 模板。

在*DAL*文件夹中，使用**文本模板**模板（位于 "**已安装的模板**" 列表中的 "**常规**" 节点下）添加文件，并将其命名为*SchoolModel.Views.tt*。 将文件中的现有代码替换为以下代码：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

此代码将生成 *.edmx*文件的视图，该文件位于与模板相同的文件夹中，并且具有与模板文件相同的名称。 例如，如果模板文件命名为*SchoolModel.Views.tt*，则它将查找名为*SchoolModel*的数据模型文件。

保存该文件，然后在**解决方案资源管理器**中右键单击该文件，然后选择 "**运行自定义工具**"。

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio 将生成一个代码文件，该文件基于模板创建名为*SchoolModel.Views.cs*的视图。 （您可能已注意到，在您选择 "**运行自定义工具**" 之前，只要保存模板文件，就会生成代码文件。）

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

你现在可以运行应用程序，并验证它的工作方式是否与以前相同。

有关预生成视图的详细信息，请参阅以下资源：

- 如何：在 MSDN 网站上[预生成视图以提高查询性能](https://msdn.microsoft.com/library/bb896240.aspx)。 介绍如何使用 `EdmGen.exe` 命令行工具来预生成视图。
- Windows Server AppFabric Customer 咨询团队博客上[的实体框架4中的预编译/预生成视图隔离性能](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx)。

这就完成了在使用实体框架的 ASP.NET web 应用程序中改进性能的简介。 有关更多信息，请参见以下资源：

- MSDN 网站上的[性能注意事项（实体框架）](https://msdn.microsoft.com/library/cc853327.aspx) 。
- [实体框架团队博客上的与性能相关的文章](https://blogs.msdn.com/b/adonet/archive/tags/performance/)。
- [EF 合并选项和已编译的查询](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx)。 此博客文章介绍了编译查询和合并选项（如 `NoTracking`）的意外行为。 如果计划在应用程序中使用已编译的查询或处理合并选项设置，请先阅读此项。
- [数据和建模客户顾问团队博客中与实体框架相关的文章](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/)。 包括有关已编译的查询以及使用 Visual Studio 2010 探查器发现性能问题的文章。
- [实体框架论坛线索，其中包含有关提高高度复杂查询性能的建议](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6)。
- [ASP.NET 状态管理建议](https://msdn.microsoft.com/library/z1hkazw7.aspx)。
- [使用实体框架和 ObjectDataSource：自定义分页](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx)。 在这些教程中创建的 ContosoUniversity 应用程序上构建的博客文章，用于说明如何在 " *default.aspx* " 页中实现分页。

下一教程回顾了版本4中的新实体框架的一些重要增强功能。

> [!div class="step-by-step"]
> [上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [下一页](what-s-new-in-the-entity-framework-4.md)
