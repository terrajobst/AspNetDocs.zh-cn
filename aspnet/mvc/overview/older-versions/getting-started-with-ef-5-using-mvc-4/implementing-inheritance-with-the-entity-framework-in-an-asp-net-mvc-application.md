---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 应用程序中的实体框架实现继承（第8个，共10个） |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595324"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>使用 ASP.NET MVC 应用程序中的实体框架实现继承（第8项，共10个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载完成的项目](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 你可以从头开始学习本系列教程，也可以从此处[下载入门项目](building-the-ef5-mvc4-chapter-downloads.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请[下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，您已处理并发异常。 本教程将演示如何在数据模型中实现继承。

在面向对象的编程中，可以使用继承来消除冗余代码。 在本教程中，将更改 `Instructor` 和 `Student` 类，以便从 `Person` 基类中派生，该基类包含教师和学生所共有的属性（如 `LastName`）。 不会添加或更改任何网页，但会更改部分代码，并将在数据库中自动反映这些更改。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每个层次结构一个表和每种类型一个表继承

在面向对象的编程中，可以使用继承来更轻松地处理相关类。 例如，`School` 数据模型中的 `Instructor` 和 `Student` 类共享若干属性，这将导致冗余代码：

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

假设想要消除由 `Instructor` 和`Student` 实体共享的属性的冗余代码。 你可以创建只包含这些共享属性的 `Person` 基类，然后将 `Instructor` 和 `Student` 实体从该基类继承，如下图所示：

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

有多种方法可以在数据库中表示此继承结构。 您可能有一个 `Person` 表，其中包括有关学生和一个表中的讲师的信息。 某些列可能仅适用于讲师（`HireDate`），某些列仅适用于学生（`EnrollmentDate`），其中一些列（`LastName`，`FirstName`）。 通常，您可以使用*鉴别*器列来指示每一行代表哪种类型。 例如，鉴别器列可能包含“Instructor”来指示教师，包含“Student”来指示学生。

![每 hierarchy_example 一个表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

从单个数据库表生成实体继承结构这一模式称为*每个层次结构一个表*（TPH）继承。

另一种方法是使数据库看起来更像继承结构。 例如，在 `Person` 表中只能有名称字段，并且具有具有日期字段的单独 `Instructor` 和 `Student` 表。

![每 type_inheritance 一个表](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

为每个实体类创建数据库表的此模式称为*每个类型一个表*（TPT）继承。

TPH 继承模式通常比 TPT 继承模式提供更好实体框架的性能，因为 TPT 模式可能会导致复杂的联接查询。 本教程将演示如何实现 TPH 继承。 可以通过执行以下步骤来执行此操作：

- 创建 `Person` 类，并将 `Instructor` 和 `Student` 类更改为从 `Person`派生。
- 向数据库上下文类添加模型到数据库的映射代码。
- 在整个项目中更改 `InstructorID` 和 `StudentID` 引用，`PersonID`。

## <a name="creating-the-person-class"></a>创建 Person 类

 注意：在你更新使用这些类的控制器之前，你将无法编译该项目。 

在 "*模型*" 文件夹中，创建*Person.cs* ，并将模板代码替换为以下代码：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

在*Instructor.cs*中，从 `Person` 类派生 `Instructor` 类并删除 "键" 和 "名称" 字段。 代码将如下所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

对*Student.cs*进行类似的更改。 `Student` 类将类似于以下示例：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>将 Person 实体类型添加到模型

在*SchoolContext.cs*中，添加 `Person` 实体类型的 `DbSet` 属性：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

以上是 Entity Framework 配置每个层次结构一张表继承所需的全部操作。 正如您将看到的，重新创建数据库时，它将具有一个 `Person` 表来代替 `Student` 和 `Instructor` 表。

## <a name="changing-instructorid-and-studentid-to-personid"></a>将 InstructorID 和 StudentID 更改为 PersonID

在*SchoolContext.cs*的讲师课程映射语句中，将 `MapRightKey("InstructorID")` 更改为 `MapRightKey("PersonID")`：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

这不是必需的更改;它只更改多对多联接表中 InstructorID 列的名称。 如果将名称保留为 InstructorID，应用程序仍将正常工作。 下面是已完成的*SchoolContext.cs*：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

接下来，需要将 `InstructorID` 更改为 `PersonID`，并 `StudentID` `PersonID` 整个项目中，但 "*迁移*" 文件夹中的 "标记时间" 迁移文件***除外***。 为此，你将找到并仅打开需要更改的文件，然后对打开的文件执行全局更改。 应更改的*迁移*文件夹中的唯一文件是*Migrations\Configuration.cs.*

1. > [!IMPORTANT]
   > 首先，在 Visual Studio 中关闭所有打开的文件。
2. 单击 "**查找并替换"--** 在 "**编辑**" 菜单中查找所有文件，然后搜索包含 `InstructorID`的项目中的所有文件。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 在 "查找结果 ***" 窗口中打开 "*** **查找结果**" 窗口中的每个文件，&lt;时间戳 *\_* &gt;在 "*迁移*" 文件夹中，双击每个文件对应一行。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. 打开 "**在文件中替换**" 对话框，并将 "**查看**" 更改为**所有打开的文档**。
5. 使用 "**在文件中替换**" 对话框可将所有 `InstructorID` 更改为 `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 查找项目中包含 `StudentID`的所有文件。
7. 在 "查找结果 ***" 窗口中打开 "*** **查找结果**" 窗口中的每个文件，&lt;时间戳&gt;在 "*迁移*" 文件夹中，通过双击每个文件对应一行来 *\_\** 个迁移文件。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. 打开 "**在文件中替换**" 对话框，并将 "**查看**" 更改为**所有打开的文档**。
9. 使用 "**在文件中替换**" 对话框可将所有 `StudentID` 更改为 `PersonID`。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 生成此项目。

（请注意，这说明了用于命名主键的 `classnameID` 模式的*缺点*。 如果已命名 primary keys ID 但未指定类名前缀，则现在*不*需要重命名。）

## <a name="create-and-update-a-migrations-file"></a>创建和更新迁移文件

在 "程序包管理器控制台" （PMC）中，输入以下命令：

`Add-Migration Inheritance`

在 PMC 中运行 `Update-Database` 命令。 此时，该命令将失败，因为我们有迁移不知道如何处理的现有数据。 如果你收到以下错误：

*ALTER TABLE 语句与外键约束 "FK\_dbo 冲突。\_为 dbo。Person\_PersonID "。在表 "dbo" 的数据库 "ContosoUniversity" 中发生冲突。Person "，列" PersonID "。*

打开*迁移\&lt; timestamp&gt;\_Inheritance.cs* ，并将 `Up` 方法替换为以下代码：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

再次运行 `update-database` 命令。

> [!NOTE]
> 迁移数据和进行架构更改时，可能会收到其他错误。 如果收到无法解决的迁移错误，可以继续学习本教程，方法是更改*web.config*文件中的连接字符串或删除数据库。 最简单的方法*是在 web.config 文件中*重命名数据库。 例如，将数据库名称更改为 CU\_测试，如以下示例中所示：
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 对于新数据库，没有要迁移的数据，并且 `update-database` 命令更有可能在没有错误的情况下完成。 有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。 如果你使用此方法继续学习本教程，请跳过本教程末尾的部署步骤，因为部署的站点会在自动运行迁移时收到相同的错误。 如果要解决迁移错误，最佳资源是实体框架论坛或 StackOverflow.com 之一。

## <a name="testing"></a>正在测试

运行站点并尝试各种页面。 一切都和以前一样。

在**服务器资源管理器中，** 展开 " **SchoolContext** " 和 "**表**"，你会看到 "学生 **" 表已**替换 "**学生** **" 表。** 展开 "**人员**" 表，你会看到它包含所有在 "**学生**" 和 "**讲师**" 表中使用的列。

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

右键单击 Person 表，然后单击“显示表数据”以查看鉴别器列。

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

下图说明了新的 School 数据库的结构：

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>总结

"每个层次结构一个表" 继承现在已经针对 `Person`、`Student`和 `Instructor` 类实现。 有关此和其他继承结构的详细信息，请参阅 Morteza Manavi 的博客上的[继承映射策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)。 在下一教程中，你将看到实现存储库和工作单元模式的一些方式。

可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
