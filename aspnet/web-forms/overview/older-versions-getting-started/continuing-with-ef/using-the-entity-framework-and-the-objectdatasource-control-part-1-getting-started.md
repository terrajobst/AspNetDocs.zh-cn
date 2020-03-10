---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 使用实体框架4.0 和 ObjectDataSource 控件，第1部分：入门 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果 yo 。
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440402"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>使用实体框架4.0 和 ObjectDataSource 控件，第1部分：入门

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本教程系列在[使用实体框架 4.0](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。
> 
> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 该示例应用程序是一个虚构的 Contoso 大学的网站。 它包括诸如学生入学、 课程创建和导师分配等功能。
> 
> 本教程演示中C#的示例。 [可下载的示例](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)包含C#和 Visual Basic 中的代码。
> 
> ## <a name="database-first"></a>Database First
> 
> 可以通过三种方式使用实体框架中的数据： *Database First*、 *Model First*和*Code First*。 本教程适用于 Database First。 有关这些工作流之间的差异以及如何为你的方案选择最佳方案的指南的信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="web-forms"></a>Web Forms — Web 窗体
> 
> 与入门系列一样，本教程系列使用 ASP.NET Web 窗体模型，并假设你知道如何在 Visual Studio 中使用 ASP.NET Web 窗体。 否则，请参阅[ASP.NET 4.5 Web Forms 入门](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 如果希望使用 ASP.NET MVC 框架，请参阅[使用 ASP.NET mvc 入门与实体框架](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> ## <a name="software-versions"></a>软件版本
> 
> | **教程中所示** | **还适用于** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web。 本教程尚未通过更高版本的 Visual Studio 进行测试。 菜单选择、对话框和模板有很多不同之处。 |
> | .NET 4 | .NET 4.5 向后兼容 .NET 4，但本教程尚未通过 .NET 4.5 进行测试。 |
> | 实体框架4 | 本教程尚未测试实体框架的更高版本。 从实体框架5开始，EF 默认使用 EF 4.1 引入的 `DbContext API`。 EntityDataSource 控件设计为使用 `ObjectContext` API。 有关如何将 EntityDataSource 控件与 `DbContext` API 一起使用的信息，请参阅[此博客文章](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)。 |
> 
> ## <a name="questions"></a>问题
> 
> 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)、[实体框架和 LINQ to Entities 论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。

`EntityDataSource` 控件使您能够快速创建应用程序，但它通常要求您在 *.aspx*页面中保留大量的业务逻辑和数据访问逻辑。 如果你希望应用程序的复杂性增加并需要持续维护，则可以提前投入更多的开发时间，以便创建具有更好维护性的*n 层*或*分层*应用程序结构。 若要实现此体系结构，请将表示层与业务逻辑层（BLL）和数据访问层（DAL）分开。 实现此结构的一种方法是使用 `ObjectDataSource` 控件而不是 `EntityDataSource` 控件。 当使用 `ObjectDataSource` 控件时，可以实现自己的数据访问代码，然后使用与其他数据源控件具有许多相同功能的控件在 .aspx 页中调用该代码 *。* 这使您可以将 n 层方法的优点与使用 Web 窗体控件进行数据访问的好处结合起来。

`ObjectDataSource` 控件也可为您提供更多的灵活性。 由于你编写自己的数据访问代码，因此更容易执行除读取、插入、更新或删除特定实体类型之外的其他操作，这是 `EntityDataSource` 控件旨在执行的任务。 例如，您可以在每次更新实体时执行日志记录、每次删除实体时存档数据，或在插入具有外键值的行时自动检查和更新相关数据。

## <a name="business-logic-and-repository-classes"></a>业务逻辑和存储库类

`ObjectDataSource` 控件的工作原理是调用你创建的类。 类包括用于检索和更新数据的方法，并向标记中的 `ObjectDataSource` 控件提供这些方法的名称。 在呈现或回发处理期间，`ObjectDataSource` 会调用您指定的方法。

除了基本的 CRUD 操作，创建的用于 `ObjectDataSource` 控件的类在 `ObjectDataSource` 读取或更新数据时可能需要执行业务逻辑。 例如，在更新部门时，可能需要验证没有其他部门拥有相同的管理员，因为一个人员不能是多个部门的管理员。

在某些 `ObjectDataSource` 文档（如[ObjectDataSource 类概述](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx)）中，控件调用一个称为*业务对象*的类，该对象同时包含业务逻辑和数据访问逻辑。 在本教程中，您将为业务逻辑和数据访问逻辑创建单独的类。 封装数据访问逻辑的类称为 "*存储库*"。 业务逻辑类既包含业务逻辑方法又包含数据访问方法，但数据访问方法调用存储库来执行数据访问任务。

你还将在 BLL 和 DAL 之间创建一个抽象层，用于简化 BLL 的自动单元测试。 此抽象层是通过以下方式实现的：创建一个接口，然后在业务逻辑类中实例化该存储库时使用接口。 这使你可以向业务逻辑类提供对实现存储库接口的任何对象的引用。 对于正常操作，提供与实体框架一起使用的存储库对象。 对于测试，你提供了一个存储库对象，该对象可处理以你可以轻松操作的方式（如定义为集合的类变量）存储的数据。

下图显示了业务逻辑类（其中包含没有存储库的数据访问逻辑）与使用存储库的数据访问逻辑之间的差异。

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

首先创建一个网页，将 `ObjectDataSource` 控件直接绑定到存储库，因为它只执行基本的数据访问任务。 在下一教程中，你将使用验证逻辑创建业务逻辑类，并将 `ObjectDataSource` 控件绑定到该类而不是存储库类。 你还将为验证逻辑创建单元测试。 在本系列教程的第三个教程中，你将向应用程序添加排序和筛选功能。

您在本教程中创建的页面将使用您在[入门教程系列](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)中创建的数据模型的 `Departments` 实体集。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>更新数据库和数据模型

在本教程中，将对数据库进行两次更改，这两个更改都需要[使用实体框架和 Web 窗体](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教程对入门中创建的数据模型进行相应的更改。 在其中一个教程中，您在设计器中进行了手动更改，以便在数据库更改后将数据模型与数据库同步。 在本教程中，您将使用设计器的 "**从数据库更新模型**" 工具来自动更新数据模型。

### <a name="adding-a-relationship-to-the-database"></a>向数据库添加关系

在 Visual Studio 中，打开在 "[实体框架" 和 "Web 窗体](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)" 教程系列的入门中创建的 Contoso 大学 web 应用程序，然后打开 `SchoolDiagram` 数据库关系图。

如果在数据库关系图中查看 `Department` 表，将看到它有一个 `Administrator` 列。 此列是 `Person` 表的外键，但在数据库中未定义外键关系。 您需要创建关系并更新数据模型，以便实体框架可以自动处理此关系。

在数据库关系图中，右键单击 `Department` 表，然后选择 "**关系**"。

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

在 "**外键关系**" 对话框中，单击 "**添加**"，然后单击 "**表和列规范**" 的省略号。

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

在 "**表和列**" 对话框中，将主键表和字段设置为 `Person` 和 `PersonID`，然后将外键表和字段设置为 `Department` 和 `Administrator`。 （如果执行此操作，关系名称将从 `FK_Department_Department` 更改为 `FK_Department_Person`。）

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

在 "**表和列**" 框中单击 **"确定"** ，在 "**外键关系**" 框中单击 "**关闭**"，并保存所做的更改。 如果系统询问您是否要保存 `Person` 和 `Department` 表，请单击 **"是"** 。

> [!NOTE]
> 如果已删除 `Person` 与 `Administrator` 列中的数据相对应的行，则将无法保存此更改。 在这种情况下，请使用**服务器资源管理器**中的表编辑器来确保每个 `Department` 行中的 `Administrator` 值包含在 `Person` 表中实际存在的记录的 ID。
> 
> 保存更改后，如果用户是部门管理员，将无法从 `Person` 表中删除行。 在生产应用程序中，您可以在数据库约束阻止删除时提供特定的错误消息，也可以指定级联删除。 有关如何指定级联删除的示例，请参阅[实体框架和 ASP.NET –入门第2部分](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)。

### <a name="adding-a-view-to-the-database"></a>向数据库添加视图

在将创建*的新的*"node.js" 页面中，你想要提供讲师的下拉列表，名称采用 "last，first" 格式，以便用户可以选择部门管理员。 为了更轻松地执行此操作，您将在数据库中创建一个视图。 视图将只包含下拉列表所需的数据：完整名称（格式正确）和记录键。

在**服务器资源管理器**中，展开 " *School*"，右键单击 "**视图**" 文件夹，然后选择 "**添加新视图**"。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

在显示 "**添加表**" 对话框时单击 "**关闭**"，然后将以下 SQL 语句粘贴到 SQL 窗格中：

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

将视图另存为 `vInstructorName`。

### <a name="updating-the-data-model"></a>更新数据模型

在*DAL*文件夹中，打开*SchoolModel*文件，右键单击设计图面，然后选择 "**从数据库更新模型**"。

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

在 "**选择数据库对象**" 对话框中，选择 "**添加**" 选项卡并选择刚创建的视图。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

单击“完成”。

在设计器中，可以看到该工具创建了一个 `vInstructorName` 实体和 `Department` 与 `Person` 实体之间的新关联。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> 在 "**输出**" 和 "**错误列表**" 窗口中，你可能会看到一条警告消息，告知你该工具为新的 `vInstructorName` 视图自动创建了主键。 这是预期行为。

如果在代码中引用新的 `vInstructorName` 实体，则不希望使用将小写字母 "v" 作为前缀的数据库约定。 因此，您将重命名模型中的实体和实体集。

打开**模型浏览器**。 您将看到 `vInstructorName` 作为实体类型和视图列出。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

在**SchoolModel** （而不是**SchoolModel**）下，右键单击**VInstructorName** ，然后选择 "**属性**"。 在 "**属性**" 窗口中，将 "**名称**" 属性更改为 "InstructorName"，并将 "**实体集名称**" 属性更改为 "InstructorNames"。

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

保存并关闭数据模型，然后重新生成项目。

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>使用存储库类和 ObjectDataSource 控件

在*DAL*文件夹中创建一个新的类文件，将其命名为*SchoolRepository.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

此代码提供了一个 `GetDepartments` 方法，该方法返回 `Departments` 实体集中的所有实体。 因为你知道将访问返回的每个行的 `Person` 导航属性，所以可以通过使用 `Include` 方法为该属性指定预先加载。 类还实现 `IDisposable` 接口，以确保在释放对象时释放数据库连接。

> [!NOTE]
> 常见的做法是为每个实体类型创建一个存储库类。 在本教程中，使用了多个实体类型的一个存储库类。 有关存储库模式的详细信息，请参阅[实体框架团队博客](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)和[Julie Lerman 的博客](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)文章。

`GetDepartments` 方法返回一个 `IEnumerable` 对象而不是 `IQueryable` 对象，以确保即使在存储存储库对象本身后，返回的集合也可用。 `IQueryable` 对象在访问时可能会导致数据库访问，但存储库对象可能会在数据绑定控件尝试呈现数据时被释放。 可以返回其他集合类型，例如 `IList` 对象，而不是 `IEnumerable` 对象。 然而，返回 `IEnumerable` 对象可确保执行典型的只读列表处理任务（如 `foreach` 循环和 LINQ 查询），但不能添加或删除集合中的项，这可能意味着此类更改会保留到数据库中。

创建一个*使用* *网站*母版页的 "node.js" 页，并在名为 `Content2`的 `Content` 控件中添加以下标记：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

此标记创建一个 `ObjectDataSource` 控件，该控件使用刚创建的存储库类，并使用 `GridView` 控件来显示数据。 `GridView` 控件指定了**Edit**和**Delete**命令，但你尚未添加代码来支持这些命令。

几列使用 `DynamicField` 控件，以便您可以利用自动数据格式和验证功能。 要使其正常工作，必须在 `Page_Init` 事件处理程序中调用 `EnableDynamicData` 方法。 （`Administrator` 字段中不使用`DynamicControl` 控件，因为这些控件不适用于导航属性。）

稍后，在将具有嵌套 `GridView` 控件的列添加到网格中时，`Vertical-Align="Top"` 属性将变得很重要。

打开*Departments.aspx.cs*文件并添加以下 `using` 语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

然后为该页的 `Init` 事件添加以下处理程序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

在*DAL*文件夹中，创建一个名为*Department.cs*的新类文件，并将现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

此代码会将元数据添加到数据模型。 它指定 `Department` 实体的 `Budget` 属性实际上表示货币，但其数据类型 `Decimal`，并指定该值必须介于0到 $1000000.00 之间。 它还指定应采用格式 mm/dd/yyyy 格式将 `StartDate` 属性格式化为日期格式。

运行 " *node.js" 页。*

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

请注意，虽然未在 "**预算**" 或 "**开始日期**" 列的 " *.aspx* " 页标记中指定格式字符串，但 `DynamicField` 控件已使用在*Department.cs*文件中提供的元数据将默认货币和日期格式应用于它们。

## <a name="adding-insert-and-delete-functionality"></a>添加插入和删除功能

打开*SchoolRepository.cs*，添加以下代码以创建 `Insert` 方法和 `Delete` 方法。 此代码还包括一个名为 `GenerateDepartmentID` 的方法，该方法用于计算 `Insert` 方法使用的下一个可用记录键值。 这是必需的，因为未将数据库配置为自动为 `Department` 表计算此数据。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach 方法

`DeleteDepartment` 方法将调用 `Attach` 方法，以便重新建立在对象上下文的对象状态管理器中维护的链接，该链接在内存中的实体和它所表示的数据库行之间。 此方法必须在方法调用 `SaveChanges` 方法之前发生。

术语 "*对象上下文*" 是指派生自 `ObjectContext` 类的实体框架类，该类用于访问实体集和实体。 在此项目的代码中，类命名为 `SchoolEntities`，它的实例始终命名为 `context`。 对象上下文的*对象状态管理器*是一个派生自 `ObjectStateManager` 类的类。 对象联系人使用对象状态管理器来存储实体对象，并跟踪每个实体对象是否与数据库中的相应表行同步。

读取实体时，对象上下文会将其存储在对象状态管理器中，并跟踪对象的表示形式是否与数据库同步。 例如，如果您更改属性值，则将设置一个标志以指示您更改的属性将不再与数据库同步。 然后，当调用 `SaveChanges` 方法时，对象上下文知道要在数据库中执行的操作，因为对象状态管理器确切知道实体的当前状态与数据库状态之间的差异。

但是，此过程通常在 web 应用程序中不起作用，因为在页面呈现后，读取实体的对象上下文实例以及其对象状态管理器中的所有内容都将被释放。 必须应用更改的对象上下文实例是为回发处理实例化的新实例。 如果是 `DeleteDepartment` 方法，`ObjectDataSource` 控件将从视图状态的值为你重新创建实体的原始版本，但此重新创建的 `Department` 实体在对象状态管理器中不存在。 如果在此重新创建的实体上调用了 `DeleteObject` 方法，则调用将失败，因为对象上下文不知道实体是否与数据库同步。 但是，调用 `Attach` 方法会重新建立重新创建的实体与数据库中的相同跟踪，该实体是在对象上下文的早期实例中读取实体时自动完成的。

有时，您不希望对象上下文跟踪对象状态管理器中的实体，并且可以设置标志来防止其执行此操作。 本系列后面的教程中显示了这种情况的示例。

### <a name="the-savechanges-method"></a>SaveChanges 方法

此简单存储库类阐释了如何执行 CRUD 操作的基本原则。 在此示例中，将在每次更新后立即调用 `SaveChanges` 方法。 在生产应用程序中，你可能需要从单独的方法中调用 `SaveChanges` 方法，以便更好地控制更新数据库的时间。 （在下一教程结束时，你会看到一个指向白皮书的链接，其中介绍了一种协调相关更新的工作单元。）另请注意，在此示例中，`DeleteDepartment` 方法不包括用于处理并发冲突的代码;本系列后面的教程中将添加要执行的代码。

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>检索要在插入时选择的指导员名称

创建新的部门时，用户必须能够从下拉列表中的一组教师列表中选择管理员。 因此，请将以下代码添加到*SchoolRepository.cs* ，以创建一个方法来使用您之前创建的视图检索讲师列表：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>创建用于插入部门的页面

创建一个使用 DepartmentsAdd*页的 "* " 页，并在名为 `Content2`的 `Content` 控件中添加以下标记：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

此标记创建两个 `ObjectDataSource` 控件，一个用于插入新的 `Department` 实体，另一个用于检索用于选择部门管理员的 `DropDownList` 控件的指导员名称。 标记创建用于输入新部门的 `DetailsView` 控件，并为控件的 `ItemInserting` 事件指定处理程序，以便可以设置 `Administrator` 外键值。 最后，`ValidationSummary` 控件可以显示错误消息。

打开*DepartmentsAdd.aspx.cs*并添加以下 `using` 语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

添加以下类变量和方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` 方法启用动态数据功能。 `DropDownList` 控件的 `Init` 事件的处理程序保存对控件的引用，而 `DetailsView` 控件的 `Inserting` 事件的处理程序使用该引用获取选定讲师的 `PersonID` 值并更新 `Administrator` 实体的 `Department` 外键属性。

运行页面，为新部门添加信息，然后单击 "**插入**" 链接。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

为另一个新部门输入值。 在 "**预算**" 字段和 "选项卡" 中，输入一个大于1000000.00 的数字作为下一个字段。 星号出现在字段中，如果将鼠标指针悬停在该字段上，则可以看到在该字段的元数据中输入的错误消息。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

单击 "**插入**"，可以看到由页面底部的 `ValidationSummary` 控件显示的错误消息。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

接下来，关闭浏览器并打开 "*部门*" 页。 通过向 `ObjectDataSource` 控件添加 `DeleteMethod` 特性，并将 `DataKeyNames` 特性添加到 `GridView` 控件中，将删除功能添加到了*node.js 页中。* 这些控件的开始标记现在将类似于以下示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

运行页面。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

删除运行*DepartmentsAdd*页面时添加的部门。

## <a name="adding-update-functionality"></a>添加更新功能

打开*SchoolRepository.cs*并添加以下 `Update` 方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

当在 " *default.aspx* " 页中单击 "**更新**" 时，`ObjectDataSource` 控件将创建两个要传递给 `UpdateDepartment` 方法的 `Department` 实体。 一个包含已存储在视图状态中的原始值，另一个包含在 `GridView` 控件中输入的新值。 `UpdateDepartment` 方法中的代码将具有原始值的 `Department` 实体传递到 `Attach` 方法，以便在实体和数据库中的内容之间建立跟踪。 然后，该代码将具有新值的 `Department` 实体传递到 `ApplyCurrentValues` 方法。 对象上下文比较旧值和新值。 如果新值不同于旧值，则对象上下文将更改属性值。 然后 `SaveChanges` 方法仅更新数据库中已更改的列。 （但是，如果此实体的更新函数映射到存储过程，则无论更改了哪些列，整个行将被更新。）

打开 "*部门 .aspx* " 文件，并将以下属性添加到 `DepartmentsObjectDataSource` 控件：

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 这会导致旧值存储在视图状态中，以便可以将它们与 `Update` 方法中的新值进行比较。
- `OldValuesParameterFormatString="orig{0}"`   
 这会通知控件 `origDepartment` 原始值参数的名称。

`ObjectDataSource` 控件开始标记的标记现在类似于以下示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

向 `GridView` 控件添加 `OnRowUpdating="DepartmentsGridView_RowUpdating"` 特性。 您将使用此设置基于用户在下拉列表中选择的行来设置 `Administrator` 属性值。 `GridView` 开始标记现在类似于以下示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

将 `Administrator` 列的 `EditItemTemplate` 控件添加到 `GridView` 控件，紧跟在该列的 `ItemTemplate` 控件之后：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

此 `EditItemTemplate` 控件类似于*DepartmentsAdd*页中的 `InsertItemTemplate` 控件。 不同之处在于，使用 `SelectedValue` 特性设置控件的初始值。

在 `GridView` 控件之前，添加一个 `ValidationSummary` 控件，就像在*DepartmentsAdd*页中所做的一样。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

打开*Departments.aspx.cs* ，并紧接在分部类声明的后面添加以下代码，以创建用于引用 `DropDownList` 控件的私有字段：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

然后为 `DropDownList` 控件的 `Init` 事件和 `GridView` 控件的 `RowUpdating` 事件添加处理程序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

`Init` 事件的处理程序保存对类字段中的 `DropDownList` 控件的引用。 `RowUpdating` 事件的处理程序使用引用获取用户输入的值并将其应用于 `Department` 实体的 `Administrator` 属性。

使用*DepartmentsAdd*页添加新的部门，然后运行 "node.js *" 页，* 并在添加的行上单击 "**编辑**"。

> [!NOTE]
> 由于数据库中的数据无效，您将无法编辑您未添加的行（即，已经存在于数据库中）。与数据库一起创建的行的管理员是学生。 如果尝试编辑其中一个文件，则会出现一个错误页面，报告错误，如 `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

如果输入的**预算**金额无效，然后单击 "**更新**"，则会看到与在 "云和 *.aspx* " 页中看到的相同星号和错误消息。

更改字段值或选择其他管理员，然后单击 "**更新**"。 将显示更改。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

这完成了将 `ObjectDataSource` 控件用于使用实体框架的基本 CRUD （创建、读取、更新、删除）操作的简介。 你已经构建了一个简单的 n 层应用程序，但业务逻辑层仍与数据访问层紧密耦合，这会使自动单元测试变得更加复杂。 在以下教程中，你将了解如何实现存储库模式，以便于进行单元测试。

> [!div class="step-by-step"]
> [下一部分](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
