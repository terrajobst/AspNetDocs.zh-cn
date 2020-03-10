---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第6部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454916"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第6部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="implementing-table-per-hierarchy-inheritance"></a>实现“每个层次结构一个表”继承

在上一教程中，您将通过添加和删除关系并添加与现有实体有关系的新实体来处理相关数据。 本教程将演示如何在数据模型中实现继承。

在面向对象的编程中，可以使用继承来更轻松地处理相关类。 例如，可以创建从 `Person` 基类派生的 `Instructor` 和 `Student` 类。 可以在实体框架中的实体之间创建相同种类的继承结构。

在本教程的此部分，不会创建任何新网页。 相反，您将向数据模型中添加派生实体，并修改现有页面以使用新实体。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每个层次结构一个表和每种类型一个表继承

数据库可以将有关相关对象的信息存储在一个表或多个表中。 例如，在 `School` 数据库中，`Person` 表在一个表中包含学生和教师的相关信息。 某些列仅适用于讲师（`HireDate`），一些列仅适用于学生（`EnrollmentDate`），一些列用于（`LastName`，`FirstName`）。

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

您可以配置实体框架以创建 `Instructor` 并 `Student` 从 `Person` 实体继承的实体。 从单个数据库表生成实体继承结构这一模式称为*每个层次结构一个表*（TPH）继承。

对于课程，`School` 数据库使用不同的模式。 在线课程和现场课程存储在单独的表中，每个表都有一个指向 `Course` 表的外键。 这两个课程类型所共有的信息仅存储在 `Course` 表中。

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

您可以配置实体框架数据模型，使 `OnlineCourse` 和 `OnsiteCourse` 实体从 `Course` 实体继承。 此模式从单独的表为每个类型生成实体继承结构，每个单独的表引用一个存储所有类型的数据的表，称为*每个类型一个表*（TPT）继承。

TPH 继承模式通常比 TPT 继承模式提供更好实体框架的性能，因为 TPT 模式可能会导致复杂的联接查询。 本演练演示如何实现 TPH 继承。 可以通过执行以下步骤来执行此操作：

- 创建从 `Person`派生的 `Instructor` 和 `Student` 实体类型。
- 将与派生的实体相关的属性从 `Person` 实体移动到派生的实体。
- 对派生类型中的属性设置约束。
- 使 `Person` 成为抽象实体。
- 将每个派生实体映射到 `Person` 表，其中包含一个指定如何确定 `Person` 行是否表示该派生类型的条件。

## <a name="adding-instructor-and-student-entities"></a>添加教师和学生实体

打开<em>SchoolModel</em>文件，右键单击设计器中的未占用区域，选择 "<strong>添加</strong>"，然后选择 "<strong>实体</strong>"<em>。</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

在 "**添加实体**" 对话框中，将实体命名为 `Instructor`，并将其 "**基本类型**" 选项设置为 "`Person`"。

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

单击“确定”。 设计器将创建一个派生自 `Person` 实体的 `Instructor` 实体。 新实体尚没有任何属性。

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

重复此过程以创建也派生自 `Person`的 `Student` 实体。

只有指导员具有雇用日期，因此，你需要将该属性从 `Person` 实体移动到 `Instructor` 实体。 在 "`Person`" 实体中，右键单击 "`HireDate`" 属性，然后单击 "**剪切**"。 然后右键单击 "`Instructor`" 实体中的 "**属性**"，然后单击 "**粘贴**"。

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

`Instructor` 实体的雇用日期不能为 null。 右键单击 "`HireDate`" 属性，单击 "**属性**"，然后在 "**属性**" 窗口中，将 "`Nullable`" 更改为 "`False`"。

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

重复此过程，将 `EnrollmentDate` 属性从 `Person` 实体移到 `Student` 实体。 请确保将 `Nullable` 设置为 `False` 用于 `EnrollmentDate` 属性。

现在，`Person` 实体仅包含 `Instructor` 和 `Student` 实体共有的属性（除了导航属性以外，不会移动这些属性），但实体只能用作继承结构中的基础实体。 因此，您需要确保永远不会被视为独立的实体。 右键单击 `Person` 实体，选择 "**属性**"，然后在 "**属性**" 窗口中，将 "**抽象**" 属性的值更改为 " **True**"。

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>将指导员和学生实体映射到 Person 表

现在，您需要告诉实体框架如何区分数据库中的 `Instructor` 和 `Student` 实体。

右键单击 "`Instructor`" 实体，然后选择 "**表映射**"。 在 "**映射详细信息**" 窗口中，单击 "**添加表" 或 "视图**"，然后选择 "**人员**"。

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

单击 "**添加条件**"，然后选择 "**雇佣**日期"。

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

将**Operator**改为**Is** ，将**值/属性**更改为**Not Null**。

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

对 `Students` 实体重复此过程，指定此实体在 `EnrollmentDate` 列不为 null 时映射到 `Person` 表。 然后保存并关闭数据模型。

生成项目，以便创建新实体作为类并使其在设计器中可用。

## <a name="using-the-instructor-and-student-entities"></a>使用讲师和学生实体

当您创建了与学生和教师数据一起使用的网页时，可以将它们绑定到 `Person` 实体集，并按 `HireDate` 或 `EnrollmentDate` 属性进行筛选，以将返回的数据限制为学生或讲师。 但是，现在当你将每个数据源控件绑定到 `Person` 实体集时，你可以指定仅选择 `Student` 或 `Instructor` 实体类型。 因为实体框架知道如何区分 `Person` 实体集中的学生和教师，所以可以删除手动输入的 `Where` 属性设置。

在 Visual Studio 设计器中，可以在 "`Configure Data Source` 向导" 的 " **EntityTypeFilter** " 下拉框中指定 `EntityDataSource` 控件应选择的实体类型，如下面的示例中所示。

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

在 "**属性**" 窗口中，您可以删除不再需要的 `Where` 子句值，如下面的示例中所示。

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

不过，由于您已将 `EntityDataSource` 控件的标记更改为使用 `ContextTypeName` 属性，因此您无法在已创建的 `EntityDataSource` 控件上运行 "**配置数据源**" 向导。 因此，您将改为更改标记以进行所需的更改。

打开 " *student" 页。* 在 `StudentsEntityDataSource` 控件中，删除 `Where` 属性并添加 `EntityTypeFilter="Student"` 属性。 标记现在将类似于以下示例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

设置 `EntityTypeFilter` 属性可确保 `EntityDataSource` 控件将仅选择指定的实体类型。 如果要检索 `Student` 和 `Instructor` 实体类型，则不会设置此属性。 （只有在将控件用于只读数据访问时，才可以使用一个 `EntityDataSource` 的控件检索多个实体类型。 如果使用 `EntityDataSource` 控件插入、更新或删除实体，并且它绑定到的实体集可以包含多个类型，则只能使用一个实体类型，并且必须设置此属性。）

对 `SearchEntityDataSource` 控件重复此过程，但仅删除 `Where` 属性的部分，该部分选择 `Student` 实体，而不是完全删除属性。 控件的开始标记现在将类似于以下示例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

运行页面，验证它是否仍然像以前一样工作。

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

更新你在前面的教程中创建的以下页面，使其使用新的 `Student` 和 `Instructor` 实体，而不是 `Person` 实体，然后运行它们以验证它们的工作方式与之前一样：

- 在*StudentsAdd*中，将 `EntityTypeFilter="Student"` 添加到 `StudentsEntityDataSource` 控件。 标记现在将类似于以下示例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- 在 *.aspx*中，将 `EntityTypeFilter="Student"` 添加到 `StudentStatisticsEntityDataSource` 控件并删除 `Where="it.EnrollmentDate is not null"`。 标记现在将类似于以下示例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- 在*InstructorsCourses 和*中，将 `EntityTypeFilter="Instructor"` 添加到 `InstructorsEntityDataSource`*控件并删除*`Where="it.HireDate is not null"`。 *指导员*中的标记现在类似于以下示例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    *InstructorsCourses*中的标记现在将类似于以下示例：

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

由于这些更改，已通过多种方式改进了 Contoso 大学应用程序的可维护性。 您已将选择和验证逻辑移出 UI 层（ *.aspx*标记），并使其成为数据访问层的组成部分。 这有助于将你的应用程序代码与你将来可能在数据库架构或数据模型中所做的更改隔离开来。 例如，你可以决定将学生雇用老师的辅助工具，从而获得雇用日期。 然后，可以添加新的属性，将学生与教师区分开来并更新数据模型。 Web 应用程序中的任何代码都不需要更改，除非你想要为学生显示雇用日期。 添加 `Instructor` 和 `Student` 实体的另一个好处是，你的代码比引用实际为学生或讲师的对象 `Person` 更容易理解。

你现在已在实体框架中看到了实现继承模式的一种方法。 在以下教程中，您将了解如何使用存储过程来更好地控制实体框架访问数据库的方式。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-7.md)
