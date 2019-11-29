---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 为 ASP.NET MVC 应用程序创建更复杂的数据模型（第4个，共10个） |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9c19ec47ad98a319ddee17db014c4b15e3734778
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595361"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>为 ASP.NET MVC 应用程序创建更复杂的数据模型（第4个，共10个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载完成的项目](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 你可以从头开始学习本系列教程，也可以从此处[下载入门项目](building-the-ef5-mvc4-chapter-downloads.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请[下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在前面的教程中，你使用了由三个实体组成的简单数据模型。 在本教程中，您将添加更多实体和关系，并通过指定格式设置、验证和数据库映射规则来自定义数据模型。 你将看到两种自定义数据模型的方式：通过将特性添加到实体类，并将代码添加到数据库上下文类中。

完成本教程后，实体类将构成下图所示的完整数据模型：

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>使用特性自定义数据模型

本节介绍如何使用指定格式化、验证和数据库映射规则的特性来自定义数据模型。 然后，在以下几个部分中，您将通过向已创建的类添加特性并为模型中的其余实体类型创建新类，来创建完整的 `School` 数据模型。

### <a name="the-datatype-attribute"></a>DataType 特性

对于学生注册日期，目前所有网页都显示有时间和日期，尽管对此字段而言重要的只是日期。 使用数据注释特性，可更改一次代码，修复每个视图中数据的显示格式。 若要查看如何执行此操作，请向 `Student` 类的 `EnrollmentDate` 属性添加一个特性。

在*Models\Student.cs*中，添加 `System.ComponentModel.DataAnnotations` 命名空间的 `using` 语句，并将 `DataType` 和 `DisplayFormat` 特性添加到 `EnrollmentDate` 属性，如以下示例中所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性用于指定比数据库内部类型更具体的数据类型。 在此示例中，我们只想跟踪日期，而不是日期和时间。 [DataType 枚举](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供多种数据类型，例如*日期、时间、PhoneNumber、货币、EmailAddress*等。 应用程序还可通过 `DataType` 特性自动提供类型特定的功能。 例如，可以为[EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)创建 `mailto:` 链接，并且可以在支持[HTML5](http://html5.org/)的浏览器中为[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供日期选择器。 数据[类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性发出 html 5[数据](http://ejohn.org/blog/html-5-data-attributes/)（发音为*数据破折号*）属性，html 5 浏览器可以理解这些属性。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性不提供任何验证。

`DataType.Date` 不指定显示日期的格式。 默认情况下，数据字段根据服务器的[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)按默认格式显示。

`DisplayFormat` 特性用于显式指定日期格式：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

`ApplyFormatInEditMode` 设置指定在文本框中显示值进行编辑时，还应应用指定的格式设置。 （您可能不希望为某些字段（例如，对于货币值），您可能不希望文本框中的货币符号进行编辑。）

您可以单独使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性，但通常最好使用[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性。 `DataType` 属性传达数据的*语义*，而不是将其呈现在屏幕上，并且提供了 `DisplayFormat`不会获得的以下好处：

- 浏览器可以启用 HTML5 功能（例如，显示日历控件、区域设置适用的货币符号、电子邮件链接等）。
- 默认情况下，浏览器将根据[区域设置](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)使用正确的格式呈现数据。
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性使 MVC 能够选择正确的字段模板来呈现数据（如果使用的是字符串模板，则为[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) ）。 有关详细信息，请参阅 Brad Wilson 的[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。 （尽管是针对 MVC 2 编写的，但本文仍适用于当前版本的 ASP.NET MVC。）

如果将 `DataType` 特性与日期字段结合使用，则还必须指定 `DisplayFormat` 属性，以确保字段在 Chrome 浏览器中正确呈现。 有关详细信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。

再次运行 "学生索引" 页，注意注册日期不再显示时间。 对于使用 `Student` 模型的任何视图，这一点都是相同的。

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

你还可以使用特性指定数据验证规则和消息。 假设要确保用户输入的名称不超过 50 个字符。 若要添加此限制，请将[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性添加到 `LastName` 并 `FirstMidName` 属性，如以下示例中所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性不会阻止用户为某个名称输入空格。 可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性将限制应用到输入。 例如，下面的代码要求第一个字符为大写，其余的字符为字母顺序：

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)特性为[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)特性提供了类似的功能，但不提供客户端验证。

运行应用程序，然后单击 "**学生**" 选项卡。收到以下错误：

*创建数据库后，支持 "SchoolContext" 上下文的模型已发生更改。请考虑使用 Code First 迁移更新数据库（[https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)）。*

数据库模型已更改，这种情况下需要更改数据库架构，并且实体框架检测到的情况。 你将使用迁移来更新架构，而不会丢失你使用 UI 添加到数据库的任何数据。 如果更改了由 `Seed` 方法创建的数据，则将更改回其原始状态，因为在 `Seed` 方法中使用了[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)方法。 （[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)相当于数据库术语中的 "upsert" 操作。）

在包管理器控制台 (PMC) 中输入以下命令：

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

`add-migration MaxLengthOnNames` 命令将创建一个名为 *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*的文件。 此文件包含将更新数据库以匹配当前数据模型的代码。 实体框架使用迁移文件名前面预置的时间戳来对迁移进行排序。 创建多个迁移后，如果删除数据库，或通过使用迁移来部署项目，则将按照创建的顺序应用所有迁移。

运行 "**创建**" 页，并输入长度超过50个字符的名称。 超过50个字符后，客户端验证会立即显示错误消息。

![客户端 val 错误](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>列属性

还可使用特性来控制类和属性映射到数据库的方式。 假设在名字字段使用了 `FirstMidName`，这是因为该字段也可能包含中间名。 但却希望将数据库列命名为 `FirstName`，因为要针对数据库编写即席查询的用户习惯使用该姓名。 若要进行此映射，可使用 `Column` 特性。

`Column` 特性指定，创建数据库时，映射到 `FirstMidName` 属性的 `Student` 表的列将被命名为 `FirstName`。 换言之，在代码引用 `Student.FirstMidName` 时，数据来源将是 `Student` 表的 `FirstName` 列或在其中进行更新。 如果未指定列名，则将其指定为与属性名称相同的名称。

将[system.componentmodel. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx)和 column name 属性的 using 语句添加到 `FirstMidName` 属性，如以下突出显示的代码所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

添加[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)会更改 SchoolContext 的模型，因此它不会与数据库匹配。 在 PMC 中输入以下命令以创建另一个迁移：

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

在**服务器资源管理器**（**数据库资源管理器**如果使用的是 Express for Web），请双击*Student*表。

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

下图显示了在应用前两个迁移之前的原始列名称。 除了从 `FirstMidName` 更改为 `FirstName`的列名以外，两个名称列已从 `MAX` 长度更改为50个字符。

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

你还可以使用[熟知的 API](https://msdn.microsoft.com/data/jj591617)进行数据库映射更改，如本教程的后面部分所示。

> [!NOTE]
> 如果尝试在完成所有这些实体类的创建之前进行编译，可能会出现编译器错误。

## <a name="create-the-instructor-entity"></a>创建 Instructor 实体

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

创建*Models\Instructor.cs*，将模板代码替换为以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

请注意，`Student` 和 `Instructor` 实体中具有几个相同属性。 在本系列后面的[实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中，你将使用继承重构以消除这种冗余。

### <a name="the-required-and-display-attributes"></a>必需的和显示的特性

`LastName` 属性上的属性指定它是必填字段，文本框的标题应为 "Last Name" （而不是属性名称，这是 "LastName"，不含空格），并且该值长度不能超过50个字符。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[StringLength 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)设置数据库中的最大长度，并为 ASP.NET MVC 提供客户端和服务器端验证。 还可在此属性中指定最小字符串长度，但最小值对数据库架构没有影响。 值类型（例如 DateTime、int、double 和 float）不需要[必需的特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)。 值类型不能赋予 null 值，因此它们原本是必需的。 您可以删除[所需的属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)，并将其替换为 `StringLength` 特性的最小长度参数：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

可以将多个属性放在一行上，因此还可以编写讲师类，如下所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName 计算属性

`FullName` 是计算属性，可返回通过串联两个其他属性创建的值。 因此，它只有一个 `get` 访问器，且在数据库中不会生成任何 `FullName` 列。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>课程和 OfficeAssignment 导航属性

`Courses` 和 `OfficeAssignment` 是导航属性。 如前所述，它们通常定义为[虚拟](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx)，以便能够利用称为[延迟加载](https://msdn.microsoft.com/magazine/hh205756.aspx)的实体框架功能。 此外，如果导航属性可以包含多个实体，则其类型必须实现[ICollection&lt;t&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx)接口。 （例如， [IList&lt;t&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx)限定，而不是[IEnumerable&lt;t&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) ，因为 `IEnumerable<T>` 不实现[Add](https://msdn.microsoft.com/library/63ywd54z.aspx)。

讲师可以讲授任意数量的课程，因此 `Courses` 定义为 `Course` 实体的集合。 我们的业务规则陈述，一个指导员最多只能有一个办公室，因此 `OfficeAssignment` 定义为单个 `OfficeAssignment` 实体（如果没有分配任何 office，可能 `null` 此实体）。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>创建 OfficeAssignment 实体

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

用以下代码创建*Models\OfficeAssignment.cs* ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

生成项目，该项目保存更改并验证编译器能否捕获任何复制和粘贴错误。

### <a name="the-key-attribute"></a>键属性

`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一关系。 Office 分配只与分配给它的指导员相关，因此，其主键也是 `Instructor` 实体的外键。 但实体框架无法自动将 `InstructorID` 视为此实体的主键，因为其名称不遵循 `ID` 或*classname* `ID` 命名约定。 因此，`Key` 特性用于将其识别为主键：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

如果实体具有其自己的主键，但你想要将属性命名为不同于 `classnameID` 或 `ID`的名称，也可以使用 `Key` 特性。 默认情况下，EF 将该键视为非数据库生成，因为列是用于标识关系的。

### <a name="the-foreignkey-attribute"></a>ForeignKey 特性

如果两个实体之间存在一对零或一关系或一对一关系（如 `OfficeAssignment` 与 `Instructor`之间），则 EF 无法确定关系的哪一端是主体，哪一端依赖于。 一对一关系在每个类中都有一个指向另一个类的引用导航属性。 [ForeignKey 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可应用于依赖类以建立关系。 如果省略了[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，则在尝试创建迁移时，会收到以下错误：

无法确定类型为 "ContosoUniversity" 和 "ContosoUniversity" 之间的关联的主体端。 必须使用关系 Fluent API 或数据批注显式配置此关联的主体端。

稍后在本教程中，我们将演示如何配置此关系与 Fluent API。

### <a name="the-instructor-navigation-property"></a>讲师导航属性

`Instructor` 实体有一个可以为 null 的 `OfficeAssignment` 导航属性（因为讲师可能没有办公室分配），并且 `OfficeAssignment` 实体具有不可为 null 的 `Instructor` 导航属性（因为在没有讲师的情况下，不能存在办公室分配，`InstructorID` 不可以为 null）。 当 `Instructor` 实体具有相关的 `OfficeAssignment` 实体时，每个实体在其导航属性中都具有对其他实体的引用。

您可以在讲师导航属性中放置一个 `[Required]` 特性，以指定必须有相关的指导员，但您不必这样做，因为 InstructorID 外键（也是此表的键）不可为 null。

## <a name="modify-the-course-entity"></a>修改 Course 实体

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

在*Models\Course.cs*中，将之前添加的代码替换为以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

课程实体具有外键属性，`DepartmentID` 指向相关的 `Department` 实体并且具有 `Department` 导航属性。 如果拥有相关实体的导航属性，则 Entity Framework 不会要求为数据模型添加外键属性。 EF 在需要时在数据库中自动创建外键。 但如果数据模型包含外键，则更新会变得更简单、更高效。 例如，当您提取课程实体进行编辑时，如果不加载它，则 `Department` 实体为 null，因此，在更新课程实体时，必须先提取 `Department` 实体。 如果数据模型中包含外键属性 `DepartmentID`，则在更新前无需提取 `Department` 实体。

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 特性

`CourseID` 属性上带有[None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)参数的[DatabaseGenerated 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)指定，主键值由用户提供，而不是由数据库生成。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

默认情况下，实体框架假定数据库生成主键值。 大多数情况下，这是理想情况。 但是，对于 `Course` 实体，你将使用用户指定的课程编号，如一个部门的1000系列、另一个部门的2000系列等等。

### <a name="foreign-key-and-navigation-properties"></a>外键和导航属性

`Course` 实体中的外键属性和导航属性反映以下关系：

- 向一个系分配课程后，出于上述原因，会出现 `DepartmentID` 外键和 `Department` 导航属性。 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- 参与一门课程的学生数量不定，因此 `Enrollments` 导航属性是一个集合： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- 一门课程可能由多位讲师讲授，因此 `Instructors` 导航属性是一个集合： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>创建部门实体

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

用以下代码创建*Models\Department.cs* ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>列属性

之前，你已使用[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)更改列名映射。 在 `Department` 实体的代码中，`Column` 特性用于更改 SQL 数据类型映射，以便使用数据库中的 SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx)类型定义列：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

通常不需要列映射，因为实体框架通常基于您为属性定义的 CLR 类型选择适当的 SQL Server 数据类型。 CLR `decimal` 类型会映射到 SQL Server `decimal` 类型。 但在这种情况下，您知道列将包含货币金额，而[money](https://msdn.microsoft.com/library/ms179882.aspx)数据类型则更适合这样做。

### <a name="foreign-key-and-navigation-properties"></a>外键和导航属性

外键和导航属性可反映以下关系：

- 一个系可能有也可能没有管理员，而管理员始终是讲师。 因此，`InstructorID` 属性包含为 `Instructor` 实体的外键，在 `int` 类型标识之后添加一个问号，以将该属性标记为可为 null。导航属性名为 `Administrator`，但包含 `Instructor` 实体： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- 一个部门可能有许多课程，因此存在一个 `Courses` 的导航属性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > 按照约定，Entity Framework 能针对不可为 null 的外键和多对多关系启用级联删除。 这可能会导致循环级联删除规则，这会导致在初始值设定项代码运行时出现异常。 例如，如果未将 `Department.InstructorID` 属性定义为可为 null，则在初始值设定项运行时，会收到以下异常消息： "引用关系将导致循环引用，这是不允许的。" 如果业务规则要求 `InstructorID` 属性为不可为 null，则必须使用以下 Fluent API 禁用关系的级联删除： 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>修改 Student 实体

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

在*Models\Student.cs*中，将之前添加的代码替换为以下代码。 突出显示所作更改。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>注册实体

 在*Models\Enrollment.cs*中，将之前添加的代码替换为以下代码

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>外键和导航属性

外键属性和导航属性可反映以下关系：

- 注册记录面向一门课程，因此存在 `CourseID` 外键属性和 `Course` 导航属性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- 注册记录面向一名学生，因此存在 `StudentID` 外键属性和 `Student` 导航属性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>多对多关系

`Student` 和 `Course` 实体之间存在多对多关系，`Enrollment` 实体将作为具有数据库中的*有效负载*的多对多联接表。 这意味着，除了联接的表的外键（在本例中为主键和 `Grade` 属性）之外，`Enrollment` 表还包含其他数据。

下图显示这些关系在实体关系图中的外观。 （此关系图是使用[实体框架 Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)生成的; 创建关系图不是本教程的一部分，它只是在此处用作说明。）

![学生-Course_many-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

每个关系线一端有1个，另一个用星号（\*）表示一对多关系。

如果 `Enrollment` 表未包括评分信息，只需包含两个外键 `CourseID` 和 `StudentID`。 在这种情况下，它与数据库中*没有负载*（或*纯联接表*）的多对多联接表相对应，无需为其创建模型类。 `Instructor` 和 `Course` 实体具有这种类型的多对多关系，如您所见，它们之间没有实体类：

![讲师 Course_many many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

但是，数据库中需要联接表，如以下数据库关系图中所示：

![讲师 Course_many many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

实体框架会自动创建 `CourseInstructor` 表，并通过读取和更新 `Instructor.Courses` 并 `Course.Instructors` 导航属性，以间接方式读取和更新此表。

## <a name="entity-diagram-showing-relationships"></a>显示关系的实体关系图

下图显示 Entity Framework Power Tools 针对已完成的学校模型创建的关系图。

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

除了多对多的关系线（\* \*）和一对多关系线（1到 \*），可在此处查看 `Instructor` 和 `OfficeAssignment` 实体之间的一对零或一关系线（1到 0 ... 1）与指导员和部门实体之间的零或一对多关系线（0 .0 到 \*）之间。

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>通过将代码添加到数据库上下文来自定义数据模型

接下来，将新实体添加到 `SchoolContext` 类，并使用[Fluent API](https://msdn.microsoft.com/data/jj591617)调用自定义某些映射。 （该 API 是 "熟知的"，因为它通常通过将一系列方法调用排列为单个语句来使用。）

在本教程中，你将仅对不能使用属性执行的数据库映射使用 Fluent API。 但 Fluent API 还可用于指定大多数格式化、验证和映射规则，这可通过特性完成。 `MinimumLength` 等特性不能通过 Fluent API 应用。 如前文所述，`MinimumLength` 不会更改架构，它只应用客户端和服务器端验证规则。

某些开发者倾向于仅使用 Fluent API 以保持实体类的“纯净”。 如有需要，可混合使用特性和 Fluent API，且有些自定义只能通过 Fluent API 实现，但通常建议选择一种方法并尽可能坚持使用这一种。

若要将新实体添加到数据模型，并使用属性执行你不执行的数据库映射，请将*DAL\SchoolContext.cs*中的代码替换为以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的新语句配置多对多联接表：

- 对于 `Instructor` 和 `Course` 实体之间的多对多关系，代码指定联接表的表名和列名。 Code First 可以为你配置多对多关系，而无需此代码，但如果不调用此代码，则将获取 `InstructorID` 列的默认名称，如 `InstructorInstructorID`。

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

下面的代码提供了一个示例，说明如何使用 Fluent API 而不是属性来指定 `Instructor` 和 `OfficeAssignment` 实体之间的关系：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

有关 "Fluent API" 语句在幕后执行的操作的信息，请参阅 "[流畅 API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) " 博客文章。

## <a name="seed-the-database-with-test-data"></a>使用测试数据设定数据库种子

将*Migrations\Configuration.cs*文件中的代码替换为以下代码，以便为你创建的新实体提供种子数据。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

正如你在第一个教程中看到的那样，此代码中的大多数只是更新或创建新的实体对象，并根据测试需要将示例数据加载到属性中。 不过，请注意如何处理与 `Instructor` 实体具有多对多关系的 `Course` 实体：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

创建 `Course` 对象时，可以使用代码 `Instructors = new List<Instructor>()`将 `Instructors` 导航属性初始化为空集合。 这样，便可以使用 `Instructors.Add` 方法添加与此 `Course` 相关的 `Instructor` 实体。 如果未创建空列表，则无法添加这些关系，因为 `Instructors` 属性为 null，并且没有 `Add` 方法。 你还可以将列表初始化添加到构造函数。

## <a name="add-a-migration-and-update-the-database"></a>添加迁移并更新数据库

在 PMC 中，输入 `add-migration` 命令：

`PM> add-Migration Chap4`

如果此时尝试更新数据库，将收到以下错误：

*ALTER TABLE 语句与外键约束 "FK\_dbo 冲突。当然\_dbo。部门\_DepartmentID "。在表 "dbo" 的数据库 "ContosoUniversity" 中发生冲突。部门 "，列" DepartmentID "。*

编辑 *\_Chap4.cs 文件&gt;&lt;时间戳*，并进行以下代码更改（您将添加一个 SQL 语句并修改 `AddColumn` 语句）：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

（请确保在添加新的 `AddColumn` 行时注释掉或删除现有的行，否则在输入 `update-database` 命令时将收到错误。）

有时，当您执行与现有数据的迁移时，您需要将存根（stub）数据插入到数据库中以满足外键约束，这就是您现在要做的。 生成的代码将不可以为 null 的 `DepartmentID` 外键添加到 `Course` 表。 如果在代码运行时 `Course` 表中已有行，则 `AddColumn` 操作将失败，因为 SQL Server 不知道要放入列中的值不能为 null。 因此，您已经更改了代码，为新列指定了默认值，并且已创建了一个名为 "Temp" 的存根部作为默认部门。 因此，如果此代码运行时存在现有 `Course` 行，它们将与 "Temp" 部门相关。

当 `Seed` 方法运行时，它将在 `Department` 表中插入行，并将现有 `Course` 行与新的 `Department` 行相关联。 如果你尚未在 UI 中添加任何课程，则不再需要 "Temp" 部门或 `Course.DepartmentID` 列上的默认值。 若要允许有人使用应用程序添加了课程，你还需要更新 `Seed` 方法代码，以确保所有 `Course` 行（而不仅仅是先前运行的 `Seed` 方法所插入的行）在从列中删除默认值并删除 "Temp" 部门之前都具有有效的 `DepartmentID` 值。

编辑完 &lt;*时间戳&gt;\_Chap4.cs*文件后，请在 PMC 中输入 `update-database` 命令以执行迁移。

> [!NOTE]
> 迁移数据和进行架构更改时，可能会收到其他错误。 如果您收到无法解决的迁移错误，则可以更改*web.config*文件中的连接字符串或删除该数据库。 最简单的方法是在*web.config 文件中*重命名数据库。 例如，将数据库名称更改为 CU\_测试，如下所示：
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> 对于新数据库，没有要迁移的数据，并且 `update-database` 命令更有可能在没有错误的情况下完成。 有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。

像之前一样，在**服务器资源管理器**中打开数据库，然后展开 "**表**" 节点以查看是否已创建所有表。 （如果您仍在之前打开**服务器资源管理器**，请单击 "**刷新**" 按钮。）

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

你没有为 `CourseInstructor` 表创建模型类。 如前所述，这是 `Instructor` 与 `Course` 实体之间的多对多关系的联接表。

右键单击 "`CourseInstructor`" 表，并选择 "**显示表数据**"，以验证它是否具有添加到 `Course.Instructors` 导航属性的 `Instructor` 实体的结果中的数据。

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>总结

现在你就得到了更复杂的数据模型和相应的数据库。 在以下教程中，你将了解有关访问相关数据的不同方法的详细信息。

可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
