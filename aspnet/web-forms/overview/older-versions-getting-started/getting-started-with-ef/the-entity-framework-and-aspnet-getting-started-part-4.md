---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第4部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518282"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第4部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="working-with-related-data"></a>使用相关数据

在上一教程中，您使用了 `EntityDataSource` 控件对数据进行筛选、排序和分组。 在本教程中，您将显示和更新相关数据。

你将创建显示指导员列表的 "讲师" 页。 选择指导员后，会看到该教师讲授的课程列表。 选择课程后，你将看到课程的详细信息以及在课程中注册的学生列表。 可以编辑讲师名称、雇用日期和办公室分配。 Office 分配是通过导航属性访问的单独实体集。

可以在标记或代码中将主数据链接到详细信息数据。 在本教程的此部分中，将使用这两种方法。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>显示并更新 GridView 控件中的相关实体

创建一个名为 "*指导员*" 的新网页，其中使用 "*站点*母版页" 母版页，并将以下标记添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

此标记创建一个 `EntityDataSource` 控件，该控件选择指导员并启用更新。 `div` 元素将标记配置为在左侧呈现，以便以后可以在右侧添加列。

在 `EntityDataSource` 标记和结束 `</div>` 标记之间，添加用于创建 `GridView` 控件的以下标记和用于错误消息的 `Label` 控件：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

此 `GridView` 控件启用行选择，突出显示带有浅灰色背景色的选定行，并指定 `SelectedIndexChanged` 和 `Updating` 事件的处理程序（稍后将创建）。 它还为 `DataKeyNames` 属性指定 `PersonID`，以便可以将所选行的键值传递给稍后将添加的另一个控件。

最后一列包含讲师的办公室分配，它存储在 `Person` 实体的导航属性中，因为它来自关联的实体。 请注意，`EditItemTemplate` 元素指定了 `Eval` 而不是 `Bind`，因为 `GridView` 控件无法直接绑定到导航属性来更新这些属性。 你将在代码中更新 office 分配。 为此，需要引用 `TextBox` 控件，并在 `TextBox` 控件的 `Init` 事件中获取并保存该控件。

下面的 `GridView` 控件是一个用于错误消息的 `Label` 控件。 控件的 `Visible` 属性是 `false`的，并且关闭了视图状态，因此，只有当代码使其在响应错误时显示时，才会显示该标签。

打开*Instructors.aspx.cs*文件并添加以下 `using` 语句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

直接在分部类名称声明后面添加私有类字段，以保存对 "office 赋值" 文本框的引用。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

为稍后将添加代码的 `SelectedIndexChanged` 事件处理程序添加存根。 同时，为 office 分配 `TextBox` 控件的 `Init` 事件添加处理程序，以便可以存储对 `TextBox` 控件的引用。 你将使用此引用获取用户输入的值，以便更新与导航属性关联的实体。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

你将使用 `GridView` 控件的 `Updating` 事件来更新关联 `OfficeAssignment` 实体的 `Location` 属性。 为 `Updating` 事件添加以下处理程序：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

当用户在 `GridView` 行中单击 "**更新**" 时，将运行此代码。 代码使用 LINQ to Entities 检索与当前 `Person` 实体关联的 `OfficeAssignment` 实体，使用事件参数中所选行的 `PersonID`。

然后，该代码根据 `InstructorOfficeTextBox` 控件中的值执行以下操作之一：

- 如果文本框具有值并且没有要更新的 `OfficeAssignment` 实体，则创建一个。
- 如果文本框具有值并且有一个 `OfficeAssignment` 实体，则会更新 `Location` 属性值。
- 如果文本框为空，并且存在 `OfficeAssignment` 实体，则会删除该实体。

之后，它会将更改保存到数据库。 如果发生异常，它将显示一条错误消息。

运行页面。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

单击 "**编辑**"，所有字段都将更改为 "文本框"。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

更改其中的任何值，包括**Office 分配**。 单击 "**更新**"，你将看到反映在列表中的更改。

## <a name="displaying-related-entities-in-a-separate-control"></a>在单独的控件中显示相关实体

每位讲师都可以讲授一个或多个课程，因此你将添加一个 `EntityDataSource` 控件和一个 `GridView` 控件，以列出与在讲师 `GridView` 控件中选择的任何指导员关联的课程。 若要为课程实体创建标题和 `EntityDataSource` 控件，请在错误消息 `Label` 控件和结束 `</div>` 标记之间添加以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` 参数包含在 `InstructorsGridView` 控件中选择了其行的指导员 `PersonID` 的值。 `Where` 属性包含一个选择的命令，该命令从 `Course` 实体的 `People` 导航属性获取所有关联的 `Person` 实体，并且仅当其中一个关联 `Course` 实体包含所选 `Person` 值时，才选择 `PersonID` 实体。

若要创建 `GridView` 控件，请在 `CoursesEntityDataSource` 控件之后（在结束 `</div>` 标记之前）添加以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

由于未选择任何教师，因此不会显示任何课程，将包含 `EmptyDataTemplate` 元素。

运行页面。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

选择已分配一个或多个课程的指导员，课程或课程显示在列表中。 （注意：尽管数据库架构允许多个课程，但在数据库中提供的测试数据中，任何讲师都没有多个课程。 您可以使用 "**服务器资源管理器**" 窗口或 " *CoursesAdd* " 页（将在后面的教程中添加），自行将课程添加到数据库中。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` 控件只显示几个课程字段。 若要显示课程的所有详细信息，您将为用户选择的课程使用 `DetailsView` 控件。 在*default.aspx*中，在结束标记 `</div>` 标记后添加以下标记（确保将此标记放在关闭 div 标记**后面**，而不是在其之前）：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

此标记创建一个绑定到 `Courses` 实体集的 `EntityDataSource` 控件。 `Where` 属性使用课程 `GridView` 控件中所选行的 `CourseID` 值选择一个课程。 标记为 `Selected` 事件指定处理程序，稍后将用于显示学生成绩，这是层次结构中较低级别的另一层。

在*Instructors.aspx.cs*中，为 `CourseDetailsEntityDataSource_Selected` 方法创建以下存根。 （你将在本教程的后面部分填写此存根; 目前你需要它，以便编译和运行页面。）

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

运行页面。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

最初没有课程详细信息，因为未选择任何课程。 选择已分配课程的指导员，然后选择某一课程以查看详细信息。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>使用 EntityDataSource "Selected" 事件显示相关数据

最后，您需要为所选课程显示所有注册的学生及其成绩。 为此，您将使用绑定到课程 `DetailsView`的 `EntityDataSource` 控件的 `Selected` 事件。

在*default.aspx*中，将以下标记添加到 `DetailsView` 控件之后：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

此标记创建一个 `ListView` 控件，该控件显示学生的列表及其成绩。 未指定数据源，因为您将在代码中 databind 控件。 `EmptyDataTemplate` 元素提供了在未选择任何课程时要显示的消息—在这种情况下，没有要显示的学生。 `LayoutTemplate` 元素创建一个用于显示列表的 HTML 表，`ItemTemplate` 指定要显示的列。 学生 ID 和学生评分来自 `StudentGrade` 实体，而学生姓名来自 `Person` 实体，实体框架在 `StudentGrade` 实体的 `Person` 导航属性中提供该名称。

在*Instructors.aspx.cs*中，将用作存根 `CourseDetailsEntityDataSource_Selected` 方法替换为以下代码：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

此事件的事件参数以集合的形式提供选定的数据，如果未选择任何内容，则将提供零项; 如果选择了 `Course` 实体，则为一个项。 如果选择 `Course` 实体，则代码将使用 `First` 方法将集合转换为单个对象。 然后，它从导航属性中获取 `StudentGrade` 实体，将它们转换为集合，并将 `GradesListView` 控件绑定到集合。

这足以显示成绩，但你想要确保在第一次显示页面时和未选择课程时显示空数据模板中的消息。 为此，请创建以下方法，从两个位置调用：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

从 `Page_Load` 方法中调用这一新方法，以便在第一次显示该页时显示空数据模板。 并从 `InstructorsGridView_SelectedIndexChanged` 方法中调用该事件，因为在选择了指导员时将引发该事件，这意味着将新课程加载到课程 `GridView` 控制，但尚未选择 "无"。 下面是两个调用：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

运行页面。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

选择已分配课程的指导员，然后选择该课程。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

你现在已经了解了几种处理相关数据的方法。 在以下教程中，您将学习如何在现有实体之间添加关系、如何删除关系，以及如何添加具有与现有实体的关系的新实体。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-5.md)
