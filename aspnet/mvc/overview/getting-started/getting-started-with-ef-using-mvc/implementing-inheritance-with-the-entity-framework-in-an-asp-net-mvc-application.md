---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 5 应用中使用 EF 实现继承
description: 本教程将演示如何在数据模型中实现继承。
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519383"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>教程：在 ASP.NET MVC 5 应用中使用 EF 实现继承

在上一教程中，您已处理并发异常。 本教程将演示如何在数据模型中实现继承。

在面向对象的编程中，可以使用[继承](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))来简化[代码重用](http://en.wikipedia.org/wiki/Code_reuse)。 在本教程中，将更改 `Instructor` 和 `Student` 类，以便从 `Person` 基类中派生，该基类包含教师和学生所共有的属性（如 `LastName`）。 不会添加或更改任何网页，但会更改部分代码，并将在数据库中自动反映这些更改。

在本教程中，你将了解：

> [!div class="checklist"]
> * 了解如何将继承映射到数据库
> * 创建 Person 类
> * 更新 Instructor 和 Student
> * 向模型添加人员
> * 创建和更新迁移
> * 测试实现
> * 部署到 Azure

## <a name="prerequisites"></a>先决条件

* [处理并发](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>会将继承映射到数据库

`School` 数据模型中的 `Instructor` 和 `Student` 类具有几个相同的属性：

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

假设想要消除由 `Instructor` 和`Student` 实体共享的属性的冗余代码。 或者想要写入可以格式化姓名的服务，而无需关注该姓名来自教师还是学生。 你可以创建只包含这些共享属性的 `Person` 基类，然后将 `Instructor` 和 `Student` 实体从该基类继承，如下图所示：

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

有多种方法可以在数据库中表示此继承结构。 您可能有一个 `Person` 表，其中包括有关学生和一个表中的讲师的信息。 某些列可能仅适用于讲师（`HireDate`），某些列仅适用于学生（`EnrollmentDate`），其中一些列（`LastName`，`FirstName`）。 通常，您可以使用*鉴别*器列来指示每一行代表哪种类型。 例如，鉴别器列可能包含“Instructor”来指示教师，包含“Student”来指示学生。

![每 hierarchy_example 一个表](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

从单个数据库表生成实体继承结构这一模式称为*每个层次结构一个表*（TPH）继承。

另一种方法是使数据库看起来更像继承结构。 例如，在 `Person` 表中只能有名称字段，并且具有具有日期字段的单独 `Instructor` 和 `Student` 表。

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

为每个实体类创建数据库表的此模式称为*每个类型一个表*（TPT）继承。

另一种方法是将所有非抽象类型映射到单独的表。 类的所有属性（包括继承的属性）映射到相应表的列。 此模式称为每个具体类一张表 (TPC) 继承。 如果为 `Person`、`Student`和 `Instructor` 类实现了 TPC 继承（如上所示），则在实现继承后，`Student` 和 `Instructor` 表的外观将与以前相同。

在实体框架中，TPC 和 TPH 继承模式通常比 TPT 继承模式提供更好的性能，因为 TPT 模式可能会导致复杂的联接查询。

本教程将演示如何实现 TPH 继承。 TPH 是实体框架中的默认继承模式，因此您只需创建一个 `Person` 类，将 `Instructor` 和 `Student` 类更改为从 `Person`派生，将新类添加到 `DbContext`中，并创建迁移。 （有关如何实现其他继承模式的信息，请参阅 MSDN 实体框架文档中的[映射每种类型一个表（TPT）继承](https://msdn.microsoft.com/data/jj591617#2.5)和[映射每个具体的表类（TPC）继承](https://msdn.microsoft.com/data/jj591617#2.6)。）

## <a name="create-the-person-class"></a>创建 Person 类

在 "*模型*" 文件夹中，创建*Person.cs* ，并将模板代码替换为以下代码：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>更新 Instructor 和 Student

现在，更新*Instructor.cs*和*Student.cs* ，以从*Person.sc*继承值。

在*Instructor.cs*中，从 `Person` 类派生 `Instructor` 类并删除 "键" 和 "名称" 字段。 代码将如下所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

对*Student.cs*进行类似的更改。 `Student` 类将类似于以下示例：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>向模型添加人员

在*SchoolContext.cs*中，添加 `Person` 实体类型的 `DbSet` 属性：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

以上是 Entity Framework 配置每个层次结构一张表继承所需的全部操作。 正如您将看到的，在数据库更新时，它将具有一个 `Person` 表来代替 `Student` 和 `Instructor` 表。

## <a name="create-and-update-migrations"></a>创建和更新迁移

在 "程序包管理器控制台" （PMC）中，输入以下命令：

`Add-Migration Inheritance`

在 PMC 中运行 `Update-Database` 命令。 此时，该命令将失败，因为我们有迁移不知道如何处理的现有数据。 你会收到如下错误消息：

> *无法删除对象 "dbo"。讲师 "，因为它被 FOREIGN KEY 约束引用。*

打开*迁移\&lt; timestamp&gt;\_Inheritance.cs* ，并将 `Up` 方法替换为以下代码：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

此代码负责以下数据库更新任务：

- 删除指向 Student 表的外键约束和索引。
- 将 Instructor 表重命名为 Person，根据需要做出更改以存储学生数据：

    - 为学生添加可为 NULL 的 EnrollmentDate。
    - 添加鉴别器列来指示行代表学生还是教师。
    - HireDate 可为 NULL，因为学生行不会包含聘用日期。
    - 添加临时字段，用于更新指向学生的外键。 将学生复制到 Person 表后，他们将获得新的主键值。
- 将数据从 Student 表复制到 Person 表。 这将使学生获取分配的新主键值。
- 修复指向学生的外键值。
- 重新创建外键约束和索引，现在将它们指向 Person 表。

（如果已使用 GUID 而不是整数作为主键类型，那么将不需要更改学生主键值，并且可能已省略其中多个步骤。）

再次运行命令 `update-database`。

（在生产系统中，您可以对 Down 方法进行相应的更改，以防您不得不使用该方法返回到以前的数据库版本。 对于本教程，你将不会使用 Down 方法。）

> [!NOTE]
> 迁移数据和进行架构更改时，可能会收到其他错误。 如果收到无法解决的迁移错误，可以继续学习本教程，方法是更改*web.config*文件中的连接字符串，或者删除数据库。 最简单的方法*是在 web.config 文件中*重命名数据库。 例如，将数据库名称更改为 ContosoUniversity2，如以下示例中所示：
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> 对于新数据库，没有要迁移的数据，并且 `update-database` 命令更有可能在没有错误的情况下完成。 有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。 如果你使用此方法来继续学习本教程，请跳过本教程末尾的部署步骤或部署到新的站点和数据库。 如果你将更新部署到已部署到的同一站点，则在它自动运行迁移时，EF 会收到相同的错误。 如果要解决迁移错误，最佳资源是实体框架论坛或 StackOverflow.com 之一。

## <a name="test-the-implementation"></a>测试实现

运行站点并尝试各种页面。 一切都和以前一样。

在**服务器资源管理器中，** 依次展开 "**数据 Connections\SchoolContext** " 和 "**表**"，你会看到 "学生 **" 表已**替换 "**学生** **" 表。** 展开 "**人员**" 表，你会看到它包含所有在 "**学生**" 和 "**讲师**" 表中使用的列。

右键单击 Person 表，然后单击“显示表数据”以查看鉴别器列。

下图说明了新的 School 数据库的结构：

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>部署到 Azure

本部分要求你已完成本系列教程的第[3 部分（排序、筛选和分页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)）中的 "将**应用程序部署到 Azure** " 部分。 如果已通过删除本地项目中的数据库解决了迁移错误，请跳过此步骤;或创建新的站点和数据库，并将其部署到新的环境。

1. 在 Visual Studio 中，在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”。

2. 单击“发布”。

    Web 应用将在默认浏览器中打开。

3. 测试应用程序以验证其是否正常工作。

    首次运行访问数据库的页时，实体框架将运行所需的所有迁移 `Up` 方法，使数据库与当前数据模型保持最新。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

有关此和其他继承结构的详细信息，请参阅 MSDN 上的[TPT 继承模式](https://msdn.microsoft.com/data/jj618293)和[TPH 继承模式](https://msdn.microsoft.com/data/jj618292)。 下一个教程将介绍如何处理各种相对高级的 Entity Framework 方案。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 已了解如何将继承映射到数据库
> * 已创建 Person 类
> * 已更新 Instructor 和 Student
> * 已将人员添加到模型
> * 创建和更新迁移
> * 已测试实现
> * 部署到 Azure

转到下一篇文章，了解有关开发使用实体框架 Code First 的 ASP.NET web 应用程序的基础知识的主题。
> [!div class="nextstepaction"]
> [高级 Entity Framework 方案](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
