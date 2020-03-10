---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第3部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522638"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第3部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="filtering-ordering-and-grouping-data"></a>筛选、排序和分组数据

在上一教程中，您使用了 `EntityDataSource` 控件来显示和编辑数据。 在本教程中，你将对数据进行筛选、排序和分组。 通过设置 `EntityDataSource` 控件的属性来执行此操作时，语法与其他数据源控件不同。 不过，您可以使用 `QueryExtender` 控件来最大程度地减少这些差异。

你将更改 "student *" 页，以便对学生进行*筛选，按名称排序，然后按名称进行搜索。 还将更改 "*课程*" 页，以显示所选部门的课程并按名称搜索课程。 最后，将学生统计信息添加到 "*关于*" 页。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>使用 EntityDataSource "Where" 属性筛选数据

打开你在上一教程中创建*的 "student" 页。* 当前配置时，页面中的 `GridView` 控件将显示 `People` 实体集中的所有名称。 但是，你只希望显示学生，你可以通过选择 `Person` 具有非 null 注册日期的实体来找到这些学生。

切换到 "**设计**" 视图并选择 "`EntityDataSource`" 控件。 在“属性” 窗口中，将 `Where` 属性设置为 `it.EnrollmentDate is not null`。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

在 `EntityDataSource` 控件的 `Where` 属性中使用的语法是实体 SQL 的。 实体 SQL 类似于 Transact-sql，但它自定义用于实体而不是数据库对象。 在表达式 `it.EnrollmentDate is not null`中，单词 `it` 表示对查询所返回的实体的引用。 因此，`it.EnrollmentDate` 引用 `EntityDataSource` 控件返回的 `Person` 实体的 `EnrollmentDate` 属性。

运行页面。 学生列表现在仅包含学生。 （没有显示任何注册日期的行。）

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>使用 EntityDataSource "OrderBy" 属性对数据进行排序

您还希望此列表在第一次显示时按名称顺序排列。 在 "**设计**" 视图中，"student *" 页仍*处于打开状态，并且仍选中 "`EntityDataSource`" 控件，在 "**属性**" 窗口中，将 " **OrderBy** " 属性设置为 `it.LastName`。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

运行页面。 学生列表现在按姓氏顺序排列。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>使用控制参数设置 "Where" 属性

与其他数据源控件一样，可以将参数值传递给 `Where` 属性。 在本教程的第2部分中创建的 "*课程 .aspx* " 页上，可以使用此方法来显示与用户从下拉列表中选择的部门关联的课程。

打开 *"* 课堂" 并切换到 "**设计**" 视图。 将第二个 `EntityDataSource` 控件添加到页面，并将其命名为 `CoursesEntityDataSource`。 将其连接到 `SchoolEntities` 模型，然后选择 "`Courses`" 作为**EntitySetName**值。

在 "**属性**" 窗口中，单击**Where**属性框中的省略号。 （请确保在使用 "**属性**" 窗口之前，`CoursesEntityDataSource` 控件仍处于选中状态。）

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

随即显示 "**表达式编辑器**" 对话框。 在此对话框中，选择 "**根据提供的参数自动生成 Where 表达式**"，然后单击 "**添加参数**"。 将参数命名 `DepartmentID`，选择 "**控件**" 作为**参数源**值，然后选择 " **DepartmentsDropDownList** " 作为 " **ControlID** " 值。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

单击 "**显示高级属性**"，然后在 "**表达式编辑器**" 对话框的 "**属性**" 窗口中，将 "`Type`" 属性更改为 "`Int32`"。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

完成后，单击“确定”。

在下拉列表下方，将 `GridView` 控件添加到页面，并将其命名为 `CoursesGridView`。 将其连接到 `CoursesEntityDataSource` 的数据源控件，单击 "**刷新架构**"，单击 "**编辑列**"，然后删除 `DepartmentID` 列。 `GridView` 控件标记类似于下面的示例。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

当用户在下拉列表中更改所选部门时，你希望关联课程的列表自动更改。 若要进行此操作，请选择下拉列表，并在 "**属性**" 窗口中将 `AutoPostBack` 属性设置为 `True`。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

完成使用设计器后，请切换到 "**源**" 视图，将 `CoursesEntityDataSource` 控件的 `ConnectionString` 和 `DefaultContainer` name 属性替换为 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 特性。 完成后，控件的标记将类似于下面的示例。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

运行页面并使用下拉列表选择不同的部门。 `GridView` 控件中仅显示所选部门提供的课程。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>使用 EntityDataSource "GroupBy" 属性对数据进行分组

假设 Contoso 大学希望将一些学生正文统计信息放在其 "关于" 页上。 具体来说，它想要按学生注册的日期来显示学生的细分。

打开*有关 .aspx*，然后在 "**源**" 视图中，将 `BodyContent` 控件的现有内容替换为 `h2` 标记之间的 "学生正文统计信息"：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

在标题后面添加一个 `EntityDataSource` 控件，并将其命名为 `StudentStatisticsEntityDataSource`。 将其连接到 `SchoolEntities`，选择 `People` 的实体集，并将向导中的 "**选择**" 框保持不变。 在 "**属性**" 窗口中设置以下属性：

- 若要仅筛选学生，请将 `Where` 属性设置为 `it.EnrollmentDate is not null`。
- 若要按注册日期对结果进行分组，请将 `GroupBy` 属性设置为 `it.EnrollmentDate`。
- 若要选择注册日期和学生数量，请将 `Select` 属性设置为 `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`。
- 若要按注册日期对结果进行排序，请将 `OrderBy` 属性设置为 `it.EnrollmentDate`。

在 "**源**" 视图中，用 `ContextTypeName` 属性替换 `ConnectionString` 和 `DefaultContainer` name 属性。 `EntityDataSource` 控件标记现在与下面的示例类似。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

`Select`、`GroupBy`和 `Where` 属性的语法类似于 Transact-sql，但指定当前实体的 `it` 关键字除外。

添加以下标记，创建 `GridView` 控件以显示数据。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

运行页面，查看按注册日期显示学生数的列表。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>使用 QueryExtender 控件进行筛选和排序

`QueryExtender` 控件提供了一种在标记中指定筛选和排序的方法。 语法独立于所使用的数据库管理系统（DBMS）。 它通常与实体框架无关，但用于导航属性的语法对于实体框架是唯一的。

在本教程的此部分中，你将使用 `QueryExtender` 控件来筛选和排序数据，其中一个排序依据字段将是导航属性。

（如果想要使用代码而不是标记来扩展由 `EntityDataSource` 控件自动生成的查询，则可以通过处理 `QueryCreated` 事件来执行此操作。 这就是 `QueryExtender` 控件如何扩展 `EntityDataSource` 控件查询的方法。）

打开 " *default.aspx* " 页，并在先前添加的标记下面插入以下标记，以创建标题、用于输入搜索字符串的文本框、"搜索" 按钮，以及绑定到 `Courses` 实体集的 `EntityDataSource` 控件。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

请注意，`EntityDataSource` 控件的 `Include` 属性设置为 "`Department`"。 在数据库中，`Course` 表不包含部门名称;它包含 `DepartmentID` 外键列。 如果直接查询数据库，若要获取部门名称以及课程数据，则必须联接 `Course` 和 `Department` 表。 通过将 `Include` 属性设置为 `Department`，你可以指定在获取 `Course` 实体时，实体框架应执行获取相关 `Department` 实体的操作。 然后 `Department` 实体存储在 `Course` 实体的 `Department` 导航属性中。 （默认情况下，数据模型设计器生成的 `SchoolEntities` 类在需要时检索相关数据，并且您已将数据源控件绑定到该类，因此不需要设置 `Include` 属性。 但是，设置它会提高页面的性能，因为否则实体框架会对数据库进行单独的调用，以检索 `Course` 实体和相关 `Department` 实体的数据。）

在刚创建的 `EntityDataSource` 控件之后，插入以下标记，以创建绑定到该 `EntityDataSource` 控件的 `QueryExtender` 控件。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` 元素指定要选择其标题与文本框中输入的值相匹配的课程。 仅会比较在文本框中输入的字符数，因为 `SearchType` 属性指定 `StartsWith`。

`OrderByExpression` 元素指定将按部门名称中的课程标题对结果集进行排序。 请注意如何指定部门名称： `Department.Name`。 由于 `Course` 实体与 `Department` 实体之间的关联是一对一的，因此 `Department` 导航属性包含 `Department` 的实体。 （如果这是一对多关系，则属性将包含一个集合。）若要获取部门名称，必须指定 `Department` 实体的 `Name` 属性。

最后，添加一个 `GridView` 控件以显示课程列表：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

第一列是显示部门名称的模板字段。 数据绑定表达式指定 `Department.Name`，就像你在 `QueryExtender` 控件中看到的一样。

运行页面。 初始显示按部门和课程标题显示所有课程的列表。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

输入 "m" 并单击 "**搜索**"，以查看其标题以 "m" 开头的所有课程（搜索不区分大小写）。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>使用 "Like" 运算符来筛选数据

通过在 `Like` 控件的 `EntityDataSource` 属性中使用 `Where` 运算符，可以实现与 `QueryExtender` 控件的 `StartsWith`、`Contains`和 `EndsWith` 搜索类型类似的效果。 在本教程的此部分中，你将了解如何使用 `Like` 运算符按名称搜索学生。

在**源**视图中打开 "student *"。* 在 `GridView` 控件后，添加以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

此标记类似于之前在之前看到的，但 `Where` 属性值除外。 `Where` 表达式的第二部分定义了一个子字符串搜索（`LIKE %FirstMidName% or LIKE %LastName%`），该搜索将搜索在文本框中输入的内容的名字和姓氏。

运行页面。 最初，你会看到所有学生，因为 `StudentName` 参数的默认值为 "%"。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

在文本框中输入字母 "g"，然后单击 "**搜索**"。 你会看到一个学生列表，其中包含在名字或姓氏中包含 "g" 的学生。

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

你现在已经显示、更新、筛选、排序和分组了各个表中的数据。 在下一教程中，您将开始使用相关数据（主-从方案）。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-4.md)
