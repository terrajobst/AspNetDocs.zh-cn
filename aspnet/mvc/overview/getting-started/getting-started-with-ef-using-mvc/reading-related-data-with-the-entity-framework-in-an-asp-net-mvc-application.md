---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中使用 EF 读取相关数据
description: 在本教程中，您将读取并显示相关数据，即实体框架加载到导航属性中的数据。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445649"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>教程：在 ASP.NET MVC 应用中使用 EF 读取相关数据

在上一教程中，你已完成 School 数据模型。 在本教程中，您将读取并显示相关数据，即实体框架加载到导航属性中的数据。

下图是将会用到的页面。

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 6 Code First 和 Visual Studio 创建 ASP.NET MVC 5 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

在本教程中，你将了解：

> [!div class="checklist"]
> * 了解如何加载相关数据
> * 创建“课程”页
> * 创建“讲师”页

## <a name="prerequisites"></a>Prerequisites

* [创建更复杂的数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>了解如何加载相关数据

实体框架可以通过多种方式将相关数据加载到实体的导航属性中：

- *延迟加载*。 首次读取实体时，不检索相关数据。 然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。 这会导致向数据库发送多个查询，一个用于实体本身，每次必须检索到该实体的相关数据。 默认情况下，`DbContext` 类启用延迟加载。

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *预先加载*。 读取该实体时，会同时检索相关数据。 此时通常会出现单一联接查询，检索所有必需数据。 使用 `Include` 方法指定预先加载。

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *显式加载*。 这类似于延迟加载，只不过是在代码中显式检索相关数据;在访问导航属性时，不会自动发生此情况。 通过获取实体的对象状态管理器条目并调用集合，可以手动加载相关数据[。](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)用于集合的 load 方法或用于保存单个实体的属性的[load 方法。](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) （在以下示例中，如果想要加载 "管理员" 导航属性，请将 `Collection(x => x.Courses)` 替换为 `Reference(x => x.Administrator)`。）通常，仅当关闭延迟加载时才使用显式加载。

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

因为它们不会立即检索属性值，所以延迟加载和显式加载也称为*延迟加载*。

### <a name="performance-considerations"></a>性能注意事项

如果知道自己需要每个检索的实体的相关数据，选择预先加载可获得最佳性能，因为相比每个检索的实体的单独查询，发送到数据库的单个查询更加有效。 例如，在上面的示例中，假设每个部门都有十个相关的课程。 预先加载的示例会生成一个（联接）查询和一个到数据库的单次往返。 延迟加载和显式加载示例会导致对数据库进行11次查询和十一次往返。 延迟较高时，额外往返数据库对性能尤为不利。

另一方面，在某些情况下，延迟加载更为有效。 预先加载可能会导致生成非常复杂的联接，这 SQL Server 无法有效地处理。 或者，如果您需要只为正在处理的一组实体的子集访问实体的导航属性，则延迟加载可能会更好，因为预先加载将检索比您所需的数据更多的数据。 如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。

延迟加载可以屏蔽导致性能问题的代码。 例如，如果代码未指定预先加载或未显式加载，但处理大量实体，并且在每次迭代中使用多个导航属性，则可能会非常低效（因为与数据库之间的往返次数很多）。 使用本地 SQL server 进行开发良好的应用程序在迁移到 Azure SQL 数据库时可能会遇到性能问题，因为这会增加延迟和延迟加载。 使用真实的测试负载分析数据库查询将有助于确定是否适合延迟加载。 有关详细信息，请参阅[揭密实体框架策略：加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx)和[使用实体框架将网络延迟减少到 SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx)。

### <a name="disable-lazy-loading-before-serialization"></a>在序列化之前禁用延迟加载

如果在序列化过程中使延迟加载处于启用状态，最终可以查询比预期更多的数据。 序列化通常通过访问类型实例上的每个属性来工作。 属性访问会触发延迟加载，并且会序列化这些延迟加载的实体。 然后，序列化过程访问延迟加载的实体的每个属性，这可能会导致更多的延迟加载和序列化。 若要防止此运行时链反应，请在序列化实体之前关闭延迟加载。

序列化还可能会由于实体框架使用的代理类而变得很复杂，如[高级方案教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)中所述。

避免序列化问题的一种方法是序列化数据传输对象（Dto）而不是实体对象，如[使用带有实体框架的 WEB API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教程中所示。

如果不使用 Dto，则可以禁用延迟加载，并通过[禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)来避免代理问题。

以下是[禁用延迟加载](https://msdn.microsoft.com/data/jj574232)的其他一些方法：

- 对于特定的导航属性，请在声明属性时省略 `virtual` 关键字。
- 对于所有导航属性，将 `LazyLoadingEnabled` 设置为 `false`，将以下代码放在上下文类的构造函数中：

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>创建“课程”页

`Course` 实体包含一个导航属性，该属性包含将课程分配到的部门的 `Department` 实体。 若要在课程列表中显示分配的部门的名称，需要从 `Course.Department` 导航属性中的 `Department` 实体获取 `Name` 属性。

使用之前用于 `Student` 控制器的实体框架 scaffolder，为 `Course` 实体类型创建一个名为 `CourseController` （不是 CoursesController）的控制器，同时使用**与视图相同的 MVC 5 控制器**选项：

| 设置 | “值” |
| ------- | ----- |
| 模型类 | 选择**课程（ContosoUniversity）** 。 |
| 数据上下文类 | 选择**SchoolContext （ContosoUniversity）** 。 |
| 控制器名称 | 输入*CourseController*。 同样，不*CoursesController* *。* 选择 "**课程（ContosoUniversity）** " 时，将自动填充 "**控制器名称**" 值。 必须更改该值。 |

保留其他默认值并添加控制器。

打开*Controllers\CourseController.cs*并查看 `Index` 方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。

打开*Views\Course\Index.cshtml* ，将模板代码替换为以下代码。 突出显示所作更改：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

已对基架代码进行了如下更改：

- 将标题从**索引**更改为**课程**。
- 添加了显示 `CourseID` 属性值的“数字”列。 默认情况下，主键不基架，因为它们对于最终用户没有意义。 但在这种情况下主键是有意义的，而你需要将其呈现出来。
- 将 "**部门**" 列移动到右侧，并更改其标题。 Scaffolder 正确地选择了从 `Department` 实体显示 `Name` 属性，但在课程页面中，列标题应为 "**部门**" 而不是 "**名称**"。

请注意，对于 "部门" 列，基架代码显示加载到 `Department` 导航属性中的 `Department` 实体的 `Name` 属性：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

运行页面（在 Contoso 大学主页上选择 "**课程**" 选项卡），查看具有部门名称的列表。

## <a name="create-an-instructors-page"></a>创建“讲师”页

在本部分中，你将为 `Instructor` 实体创建一个控制器和视图，以便显示 "讲师" 页。 该页面通过以下方式读取和显示相关数据：

- 讲师列表显示 `OfficeAssignment` 实体中的相关数据。 `Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。 你将对 `OfficeAssignment` 实体使用预先加载。 如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。 在这种情况下，你希望显示所有显示的讲师的办公室分配情况。
- 用户选择一名讲师时，显示相关 `Course` 实体。 `Instructor` 和 `Course` 实体之间存在多对多关系。 你将对 `Course` 实体及其相关 `Department` 实体使用预先加载。 在这种情况下，延迟加载可能更高效，因为你只需要为所选指导员提供课程。 但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。
- 当用户选择一门课程时，将显示 `Enrollments` 实体集中的相关数据。 `Course` 和 `Enrollment` 实体之间存在一对多的关系。 你将为 `Enrollment` 实体及其相关 `Student` 实体添加显式加载。 （由于启用了延迟加载，因此不需要显式加载，但这会显示如何进行显式加载。）

### <a name="create-a-view-model-for-the-instructor-index-view"></a>为讲师索引视图创建视图模型

"讲师" 页显示三个不同的表。 因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。

在*viewmodel*文件夹中，创建*InstructorIndexData.cs*并将现有代码替换为以下代码：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>创建讲师控制器和视图

使用 EF 读取/写入操作创建 `InstructorController` （而非 InstructorsController）控制器：

| 设置 | “值” |
| ------- | ----- |
| 模型类 | 选择 "**指导员" （ContosoUniversity）** 。 |
| 数据上下文类 | 选择**SchoolContext （ContosoUniversity）** 。 |
| 控制器名称 | 输入*InstructorController*。 同样，不*InstructorsController* *。* 选择 "**课程（ContosoUniversity）** " 时，将自动填充 "**控制器名称**" 值。 必须更改该值。 |

保留其他默认值并添加控制器。

打开*Controllers\InstructorController.cs* ，并为 `ViewModels` 命名空间添加 `using` 语句：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` 方法中的基架代码仅指定 `OfficeAssignment` 导航属性的预先加载：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

将 `Index` 方法替换为以下代码，以加载其他相关数据并将其放入视图模型：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

方法接受可选的路由数据（`id`）和查询字符串参数（`courseID`），该参数提供选定讲师和所选课程的 ID 值，并将所有所需数据传递给视图。 参数由页面上的“选择”超链接提供。

代码先创建一个视图模型实例，并在其中放入讲师列表。 此代码为 `Instructor.OfficeAssignment` 和 `Instructor.Courses` 导航属性指定预先加载。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

第二个 `Include` 方法将加载课程，对于加载的每个课程，它会预先加载 `Course.Department` 导航属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

如前所述，无需预先加载，但会执行此操作来提高性能。 由于视图始终需要 `OfficeAssignment` 实体，因此在同一查询中提取该视图会更有效。 当在网页中选择了指导员时，`Course` 实体是必需的，因此，只有在选择了比不使用的课程更频繁地显示页面时，预先加载比延迟加载更好。

如果选择了指导员 ID，则会从视图模型中的指导员列表中检索所选的指导员。 然后，将从该教师 `Courses` 导航属性中的 `Course` 实体加载视图模型的 `Courses` 属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Where` 方法返回一个集合，但在此示例中，传递给该方法的条件仅导致返回单个 `Instructor` 实体。 `Single` 方法将集合转换为单个 `Instructor` 实体，这使你能够访问该实体的 `Courses` 属性。

当您知道集合将只有一个项时，对集合使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)方法。 如果传递给它的集合为空或有多个项，则 `Single` 方法会引发异常。 替代项为[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，如果集合为空，则返回默认值（在本例中为`null`）。 但是，在这种情况下，仍会引发异常（尝试在 `null` 引用上查找 `Courses` 属性），并且异常消息不会明确指出问题的原因。 调用 `Single` 方法时，还可以传入 `Where` 条件，而不是单独调用 `Where` 方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

而不是：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。 然后，将通过该课程 `Enrollments` 导航属性中的 `Enrollment` 实体加载视图模型的 `Enrollments` 属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>修改讲师索引视图

在*Views\Instructor\Index.cshtml*中，将模板代码替换为以下代码。 突出显示所作更改：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

已对现有代码进行了如下更改：

- 将模型类更改为了 `InstructorIndexData`。
- 将页标题从“索引”更改为了“讲师”。
- 添加了仅当 `item.OfficeAssignment` 不为 null 时才显示 `item.OfficeAssignment.Location` 的**Office**列。 （由于这是一对零或一的关系，因此可能没有相关的 `OfficeAssignment` 实体。）

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- 添加了将 `class="success"` 动态添加到选定讲师的 `tr` 元素中的代码。 这将使用[启动](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)类设置所选行的背景色。

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- 添加了在每行中的其他链接之前标记为 "**选择**" 的新 `ActionLink`，这将导致所选的指导员 ID 发送到 `Index` 方法。

运行应用程序并选择 "**讲师**" 选项卡。当没有相关的 `OfficeAssignment` 实体时，此页将显示相关 `OfficeAssignment` 实体的 `Location` 属性和一个空的表单元。

在*Views\Instructor\Index.cshtml*文件中，在关闭 `table` 元素（位于文件末尾）后面添加以下代码。 选择讲师时，此代码显示与讲师相关的课程列表。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

此代码读取视图模型的 `Courses` 属性以显示课程列表。 它还提供了一个 `Select` 超链接，该超链接将所选课程的 ID 发送到 `Index` 操作方法。

运行页面并选择一个指导员。 此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。

在刚刚添加的代码块后，添加以下代码。 选择课程后，代码将显示参与课程的学生列表。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

此代码读取视图模型的 `Enrollments` 属性，以显示课程中注册的学生列表。

运行页面并选择一个指导员。 然后选择一门课程，查看参与的学生列表及其成绩。

### <a name="adding-explicit-loading"></a>添加显式加载

打开*InstructorController.cs* ，查看 `Index` 方法如何获取所选课程的注册列表：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

检索到讲师列表时，你为 `Courses` 导航属性指定了预先加载，并为每个课程的 `Department` 属性指定了预先加载。 然后，将 `Courses` 集合放置在视图模型中，现在将从该集合中的一个实体访问 `Enrollments` 导航属性。 由于未指定 `Course.Enrollments` 导航属性的预先加载，因此，该属性中的数据将作为延迟加载的结果出现在页面中。

如果在未以任何其他方式更改代码的情况下禁用延迟加载，则无论该课程实际具有多少注册，`Enrollments` 属性都将为 null。 在这种情况下，若要加载 `Enrollments` 属性，必须指定预先加载或显式加载。 您已经了解了如何执行预先加载。 若要查看显式加载的示例，请将 `Index` 方法替换为以下代码，这会显式加载 `Enrollments` 属性。 更改的代码已突出显示。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

获取所选 `Course` 实体后，新代码将显式加载该课程的 `Enrollments` 导航属性：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

然后，它显式加载每个 `Enrollment` 实体的相关 `Student` 实体：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

请注意，使用 `Collection` 方法加载集合属性，但对于只包含一个实体的属性，则使用 `Reference` 方法。

立即运行讲师索引页，您将看到页面上显示的内容没有任何区别，不过您已经更改了数据的检索方式。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 已了解如何加载相关数据
> * 已创建“课程”页
> * 已创建“讲师”页

请继续阅读下一篇文章，了解如何更新相关数据。

> [!div class="nextstepaction"]
> [更新相关数据](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
