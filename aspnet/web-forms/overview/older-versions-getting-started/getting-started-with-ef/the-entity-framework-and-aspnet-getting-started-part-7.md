---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第7部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78488522"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第7部分

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)

## <a name="using-stored-procedures"></a>使用存储过程

在上一教程中，您实现了每个层次结构一个表继承模式。 本教程将演示如何使用存储过程来获得对数据库访问的更多控制。

使用实体框架可以指定它应使用存储过程来访问数据库。 对于任何实体类型，您可以指定用于创建、更新或删除该类型的实体的存储过程。 然后，你可以在数据模型中添加对存储过程的引用，你可以使用这些引用来执行任务，例如检索实体集。

使用存储过程是数据库访问的常见要求。 在某些情况下，由于安全原因，数据库管理员可能要求所有数据库访问都要经过存储过程。 在其他情况下，你可能希望将业务逻辑构建到实体框架在更新数据库时使用的某些进程。 例如，在删除实体时，可能需要将其复制到存档数据库。 或每次更新行时，您可能想要在记录进行更改的记录表中写入一行。 可以在存储过程中执行这些类型的任务，只要实体框架删除实体或更新实体，就会调用此存储过程。

如前面的教程中所述，你将不会创建任何新页。 相反，你将更改实体框架访问数据库以获取已创建的某些页面的方式。

在本教程中，将在数据库中创建存储过程，用于插入 `Student` 和 `Instructor` 实体。 将它们添加到数据模型，并指定实体框架应使用这些数据模型将 `Student` 和 `Instructor` 实体添加到数据库中。 您还将创建一个可用于检索 `Course` 实体的存储过程。

## <a name="creating-stored-procedures-in-the-database"></a>在数据库中创建存储过程

（如果要在本教程中使用可供下载的项目的*School .mdf*文件，则可以跳过此部分，因为存储过程已经存在。）

在**服务器资源管理器**中，展开 " *School*"，右键单击 "**存储过程**"，然后选择 "**添加新存储过程**"。

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

复制以下 SQL 语句，并将其粘贴到 "存储过程" 窗口中，并替换主干存储过程。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` 实体具有四个属性： "`PersonID`"、"`LastName`"、"`FirstName`" 和 "`EnrollmentDate`"。 数据库自动生成 ID 值，存储过程接受另外三个参数。 该存储过程返回新行的记录键的值，以便实体框架可以跟踪它在内存中保留的实体版本。

保存并关闭 "存储过程" 窗口。

使用以下 SQL 语句以相同方式创建 `InsertInstructor` 存储过程：

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

同时为 `Student` 和 `Instructor` 实体创建 `Update` 存储过程。 （数据库已具有一个 `DeletePerson` 存储过程，该过程适用于 `Instructor` 和 `Student` 实体。）

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

在本教程中，您将为每个实体类型映射所有三个函数（插入、更新和删除）。 使用实体框架版本4，只需将其中一个或两个函数映射到存储过程，而无需映射其他函数，但有一个例外：如果映射更新函数但不映射 delete 函数实体框架，则在您尝试删除实体。 在实体框架版本3.5 中，你在映射存储过程时没有这么大的灵活性：如果映射了一个函数，则需要映射所有这三个函数。

若要创建读取而不是更新数据的存储过程，请使用以下 SQL 语句创建一个选择所有 `Course` 实体的存储过程：

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>向数据模型添加存储过程

现在，数据库中定义了这些存储过程，但必须将这些存储过程添加到数据模型，以使它们可用于实体框架。 打开*SchoolModel*，右键单击设计图面，然后选择 "**从数据库更新模型**"。 在 "**选择数据库对象**" 对话框的 "**添加**" 选项卡中，展开 "**存储过程**"，选择新创建的存储过程和 `DeletePerson` 存储过程，然后单击 "**完成**"。

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>映射存储过程

在数据模型设计器中，右键单击 `Student` 实体，然后选择 "**存储过程映射**"。

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

此时将显示 "**映射详细信息**" 窗口，您可以在其中指定实体框架用于插入、更新和删除此类型的实体的存储过程。

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

将**Insert**函数设置为**InsertStudent**。 此窗口将显示存储过程参数的列表，其中每个参数都必须映射到实体属性。 其中两个将自动映射，因为名称相同。 没有名为 `FirstName`的实体属性，因此您必须从显示可用实体属性的下拉列表中手动选择 `FirstMidName`。 （这是因为您在第一个教程中已将 `FirstName` 属性的名称更改为 `FirstMidName`。）

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

在相同的 "**映射详细信息**" 窗口中，将 `Update` 函数映射到 `UpdateStudent` 存储过程（请确保将 `FirstMidName` 指定为 `FirstName`的参数值，与 `Insert` 存储过程的参数值相同），并将 `Delete` 函数指定给 `DeletePerson` 存储过程。

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

按照相同的过程将讲师的 insert、update 和 delete 存储过程映射到 `Instructor` 实体。

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

对于读取而不是更新数据的存储过程，您可以使用 "**模型浏览器**" 窗口将存储过程映射到它返回的实体类型。 在数据模型设计器中，右键单击设计图面，然后选择 "**模型浏览器**"。 打开 " **SchoolModel** " 节点，然后打开 "**存储过程**" 节点。 然后右键单击 `GetCourses` 存储过程，然后选择 "**添加函数导入**"。

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

在 "**添加函数导入**" 对话框中，在 "返回选择**实体** **的集合**" 下，选择 "`Course` 作为返回的实体类型。 完成后，单击“确定”。 保存并关闭 *.edmx*文件。

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>使用 Insert、Update 和 Delete 存储过程

用于插入、更新和删除数据的存储过程在您将数据添加到数据模型并将其映射到相应的实体后，会自动由实体框架使用。 现在，你可以运行*StudentsAdd*页，每次创建新的学生时，实体框架将使用 `InsertStudent` 存储过程向 `Student` 表中添加新行。

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

运行 student*页，* 新学生显示在列表中。

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

更改该名称以验证更新函数是否正常工作，然后删除该学生以验证删除函数是否正常工作。

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>使用 Select 存储过程

实体框架不会自动运行存储过程（如 `GetCourses`），也不能将其与 `EntityDataSource` 控件一起使用。 若要使用它们，请从代码中调用它们。

打开*InstructorsCourses.aspx.cs*文件。 `PopulateDropDownLists` 方法使用 LINQ to entities 查询来检索所有课程实体，以便它可以循环遍历列表并确定哪些指导员分配给了指导员，哪些未分配：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

将此代码替换为以下代码：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

该页现在使用 `GetCourses` 存储过程来检索所有课程的列表。 运行页面，验证其工作方式是否与以前相同。

（存储过程检索到的实体的导航属性可能不会自动填充与这些实体相关的数据，具体取决于 `ObjectContext` 默认设置。 有关详细信息，请参阅 MSDN Library 中的[加载相关对象](https://msdn.microsoft.com/library/bb896272.aspx)。）

在下一教程中，你将了解如何使用动态数据功能，以便更轻松地对数据格式设置和验证规则进行编程和测试。 您可以在数据模型元数据中指定此类规则，而不是在每个网页规则（例如数据格式字符串和是否需要某个字段）上指定此类规则，而是在每个页面上自动应用这些规则。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-8.md)
