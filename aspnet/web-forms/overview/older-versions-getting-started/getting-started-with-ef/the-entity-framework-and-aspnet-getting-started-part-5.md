---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web Forms-第5部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423866"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web Forms-第5部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="working-with-related-data-continued"></a>使用相关数据（续）

在上一教程中，您开始使用 `EntityDataSource` 控件来处理相关数据。 您在导航属性中显示了多个级别的层次结构和已编辑的数据。 在本教程中，您将通过添加和删除关系并添加与现有实体有关系的新实体来继续处理相关数据。

你将创建一个页面，用于添加分配给部门的课程。 这两个部门已经存在，当您创建一个新课程时，您将在其与现有部门之间建立关系。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

您还将创建一个使用多对多关系的页面，方法是将指导员分配给课程（在您选择的两个实体之间添加关系）或从课程中删除指导员（删除您的两个实体之间的关系select）。 在数据库中，添加讲师和课程之间的关系将导致新行添加到 `CourseInstructor` 关联表中;删除关系涉及到从 `CourseInstructor` 关联表中删除行。 不过，您可以在实体框架中通过设置导航属性来执行此操作，而无需显式引用 `CourseInstructor` 表。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>将具有关系的实体添加到现有实体

创建一个使用 CoursesAdd*母版页的*名为的新网页，并将以下标记添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

此标记创建一个 `EntityDataSource` 控件，该控件可选择用于启用插入的课程，并为 `Inserting` 事件指定处理程序。 创建新的 `Course` 实体时，将使用该处理程序更新 `Department` 导航属性。

标记还会创建一个 `DetailsView` 控件以用于添加新的 `Course` 实体。 标记使用 `Course` 实体属性的绑定字段。 需要输入 `CourseID` 值，因为这不是系统生成的 ID 字段。 相反，它是在创建课程时必须手动指定的课程编号。

由于导航属性不能用于 `BoundField` 控件，因此可以对 `Department` 导航属性使用模板字段。 模板字段提供了一个下拉列表，用于选择部门。 下拉列表将通过使用 `Eval` （而不是 `Bind`）绑定到 `Departments` 实体集，因为你不能直接绑定导航属性来更新这些属性。 为 `DropDownList` 控件的 `Init` 事件指定处理程序，以便可以存储对控件的引用以供更新 `DepartmentID` 外键的代码使用。

在*CoursesAdd.aspx.cs*的分部类声明的后面，添加一个类字段以保存对 `DepartmentsDropDownList` 控件的引用：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

为 `DepartmentsDropDownList` 控件的 `Init` 事件添加处理程序，以便可以存储对该控件的引用。 这允许你获取用户输入的值，并使用它来更新 `Course` 实体的 `DepartmentID` 值。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

为 `DetailsView` 控件的 `Inserting` 事件添加处理程序：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

当用户单击 "`Insert`" 时，将在插入新记录前引发 `Inserting` 事件。 处理程序中的代码从 `DropDownList` 控件获取 `DepartmentID`，并使用它来设置将用于 `Course` 实体的 `DepartmentID` 属性的值。

实体框架将负责将此课程添加到关联 `Department` 实体的 `Courses` 导航属性。 它还将部门添加到 `Course` 实体的 `Department` 导航属性。

运行页面。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

输入 "ID"、"标题"、"信用数" 并选择一个部门，然后单击 "**插入**"。

运行 "球场 *" 页，* 然后选择同一部门查看新课程。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>使用多对多关系

`Courses` 实体集与 `People` 实体集之间的关系是多对多关系。 `Course` 实体具有名为 `People` 的导航属性，该属性可包含零个、一个或多个相关 `Person` 实体（表示分配给讲授该课程的教师）。 `Person` 实体具有一个名为 `Courses` 的导航属性，该属性可包含零个、一个或多个相关 `Course` 实体（表示讲师分配给教授的课程）。 一个讲师可以讲授多个课程，一个课程可能由多个讲师讲授。 在本演练的此部分中，你将通过更新相关实体的导航属性来添加和删除 `Person` 与 `Course` 实体之间的关系。

创建一个使用 InstructorsCourses*母版页的*名为的新网页，并将以下标记添加到名为 `Content2`的 `Content` 控件：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

此标记创建一个 `EntityDataSource` 控件，该控件检索教师 `Person` 实体的名称和 `PersonID`。 `DropDrownList` 控件绑定到 `EntityDataSource` 控件。 `DropDownList` 控件指定 `DataBound` 事件的处理程序。 你将使用此处理程序来 databind 显示课程的两个下拉列表。

标记还会创建以下控件组，用于将课程分配给所选讲师：

- 用于选择要分配的课程的 `DropDownList` 控件。 此控件将填充当前未分配给所选讲师的课程。
- 用于启动赋值的 `Button` 控件。
- 一个 `Label` 控件，在分配失败时显示错误消息。

最后，标记还会创建一组用于从所选指导员中删除课程的控件。

在*InstructorsCourses.aspx.cs*中，添加 using 语句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

添加用于填充显示课程的两个下拉列表的方法：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

此代码将获取 `Courses` 实体集中的所有课程，并从所选讲师的 `Person` 实体的 `Courses` 导航属性获取课程。 然后，它确定分配给该讲师的课程，并相应地填充下拉列表。

为 "`Assign`" 按钮的 `Click` 事件添加处理程序：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

此代码获取选定讲师的 `Person` 实体，获取所选课程的 `Course` 实体，并将所选课程添加到讲师 `Person` 实体的 `Courses` 导航属性。 然后，它会将更改保存到数据库，并重新填充下拉列表，以便可以立即查看结果。

为 "`Remove`" 按钮的 `Click` 事件添加处理程序：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

此代码获取选定讲师的 `Person` 实体，获取所选课程的 `Course` 实体，并从 `Person` 实体的 `Courses` 导航属性中删除所选课程。 然后，它会将更改保存到数据库，并重新填充下拉列表，以便可以立即查看结果。

将代码添加到 `Page_Load` 方法，以便在报告没有错误时不显示错误消息，并为讲师下拉列表的 `DataBound` 和 `SelectedIndexChanged` 事件添加处理程序，以填充课程下拉列表：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

运行页面。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

选择指导员。 "<strong>分配课程</strong>" 下拉列表显示讲师未讲授的课程，"<strong>删除课程</strong>" 下拉列表显示教师已分配到的课程。 在 "<strong>分配课程</strong>" 部分中，选择课程，然后单击 "<strong>分配</strong>"。 课程将移至 "<strong>删除课程</strong>" 下拉列表。 选择 "<strong>删除课程</strong>" 部分中的课程，并单击 "<strong>删除</strong>"<em>。</em> 课程转到 "<strong>分配课程</strong>" 下拉列表。

你现在已经了解了一些使用相关数据的方法。 在以下教程中，你将了解如何在数据模型中使用继承来改善应用程序的可维护性。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-6.md)
