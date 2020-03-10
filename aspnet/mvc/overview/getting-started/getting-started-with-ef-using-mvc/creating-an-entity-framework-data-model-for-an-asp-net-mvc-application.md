---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 教程：使用 MVC 5 开始使用实体框架 6 Code First |Microsoft Docs
description: 在本系列教程中，您将了解如何生成使用实体框架6进行数据访问的 ASP.NET MVC 5 应用程序。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499406"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>教程：使用 MVC 5 开始使用实体框架 6 Code First

> [!NOTE]
> 对于新开发，我们建议[ASP.NET Core Razor Pages](/aspnet/core/razor-pages) ASP.NET MVC 控制器和视图。 有关使用 Razor Pages 的与此类似的系列教程，请参阅[教程： ASP.NET Core 中的 Razor Pages 入门](/aspnet/core/tutorials/razor-pages/razor-pages-start)。 新教程：
> * 易于关注。
> * 提供更多 EF Core 最佳做法。
> * 使用更高效的查询。
> * 通过最新 API 更新到更高版本。
> * 涵盖更多功能。
> * 是开发新应用程序的首选方法。

在本系列教程中，您将了解如何生成使用实体框架6进行数据访问的 ASP.NET MVC 5 应用程序。 本教程使用 Code First 工作流。 有关如何在 Code First、Database First 和 Model First 之间进行选择的详细信息，请参阅[创建模型](/ef/ef6/modeling/)。

本系列教程介绍了如何构建 Contoso 大学的示例应用程序。 该示例应用程序是一个简单的大学网站。 利用它，你可以查看和更新学生、课程和教师信息。 下面是创建的两个屏幕：

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![编辑学生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建 MVC web 应用
> * 设置网站样式
> * 安装实体框架6
> * 创建数据模型
> * 创建数据库上下文
> * 使用测试数据初始化数据库
> * 设置 EF 6 以使用 LocalDB
> * 创建控制器和视图
> * 查看数据库

## <a name="prerequisites"></a>系统必备

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>创建 MVC web 应用

1. 打开 Visual Studio，并使用C# " **ASP.NET web 应用程序（.NET Framework）** " 模板创建一个 web 项目。 将项目命名为*ContosoUniversity* ，然后选择 **"确定"** 。

   ![Visual Studio 中的 "新建项目" 对话框](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. 在**New ASP.NET Web 应用程序-ContosoUniversity**中，选择 " **MVC**"。

   ![Visual Studio 中的 "新建 web 应用" 对话框](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > 默认情况下， **authentication**选项设置为 "**无身份验证**"。 对于本教程，web 应用不需要用户登录。 此外，它不会基于登录用户限制访问权限。

1. 选择“确定”创建项目。

## <a name="set-up-the-site-style"></a>设置网站样式

通过几个简单的更改设置站点菜单、 布局和主页。

1. *_Layout\\打开 Views\Shared*，并进行以下更改：

   - 将每次出现的 "我的 ASP.NET Application" 和 "Application name" 更改为 "Contoso 大学"。
   - 为学生、课程、教师和部门添加菜单项，并删除联系人条目。

   下面的代码片段突出显示了这些更改：

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. 在*Views\Home\Index.cshtml*中，将该文件的内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关此应用程序的文本：

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. 按 Ctrl + F5 运行该网站。 你将看到带有主菜单的主页。

## <a name="install-entity-framework-6"></a>安装实体框架6

1. 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。

2. 在“程序包管理器控制台”窗口中，输入以下命令：

   ```text
   Install-Package EntityFramework
   ```

此步骤是本教程手动执行的几个步骤中的一步，但这可能已由 ASP.NET MVC 基架功能自动完成。 您要手动执行这些操作，以便您可以查看使用实体框架（EF）所需的步骤。 稍后将使用基架创建 MVC 控制器和视图。 替代方法是让基架自动安装 EF NuGet 包、创建数据库上下文类并创建连接字符串。 当您准备好这样做时，您需要做的就是在创建实体类后，跳过这些步骤并基架 MVC 控制器。

## <a name="create-the-data-model"></a>创建数据模型

接下来你将创建 Contoso 大学应用程序的实体类。 你将从以下三个实体开始：

**课程** <-> **注册** <-> **学生**

| 实体 | 关系 |
| -------- | ------------ |
| 课程注册课程 | 一对多 |
| 学生注册 | 一对多 |

`Student` 和 `Enrollment`实体之间是一对多的关系，`Course` 和`Enrollment` 实体之间也是一个对多的关系。 换而言之，一名学生可以修读任意数量的课程, 并且某一课程可以被任意数量的学生修读。

在下面几节中，你将为其中的每个实体创建一个类。

> [!NOTE]
> 如果尝试在完成所有这些实体类的创建之前编译项目，将会出现编译器错误。

### <a name="the-student-entity"></a>Student 实体

- 在 "*模型*" 文件夹中，右键单击**解决方案资源管理器**的文件夹，然后选择 "**添加** > **类**"，创建名为*Student.cs*的类文件。 将模板代码替换为以下代码：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 属性将成为对应于此类的数据库表中的主键。 默认情况下，实体框架会将名为 `ID` 或*classname* `ID` 的属性解释为主键。

`Enrollments` 属性是*导航属性*。 导航属性中包含与此实体相关的其他实体。 在这种情况下，`Student` 实体的 `Enrollments` 属性将包含与该 `Student` 实体相关的所有 `Enrollment` 实体。 换言之，如果数据库中给定的 `Student` 行具有两个相关 `Enrollment` 行（其 `StudentID` 外键列中包含该学生的主键值的行），则该 `Student` 实体的 `Enrollments` 导航属性将包含这两个 `Enrollment` 的实体。

导航属性通常定义为 `virtual`，以便它们可以利用某些实体框架功能，如*延迟加载*。 （稍后将在本系列的 "[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)" 教程中介绍延迟加载。）

如果导航属性可以具有多个实体 （如多对多或一对多关系），那么导航属性的类型必须是可以添加、 删除和更新条目的容器，如 `ICollection`。

### <a name="the-enrollment-entity"></a>Enrollment 实体

- 在 *Models* 文件夹中，创建 *Enrollment.cs* 并且用以下代码替换现有代码：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` 属性将为主键;此实体使用*classname* `ID` 模式，而不是在 `Student` 实体中看到的那样 `ID`。 通常情况下，你选择一个主键模式，并在你的数据模型自始至终使用这种模式。 在这里，使用了两种不同的模式只是为了说明你可以使用任一模式来指定主键。 在后面的教程中，你将了解如何使用不带 `classname` 的 `ID`，从而更轻松地在数据模型中实现继承。

`Grade` 属性是一个[枚举](/ef/ef6/modeling/code-first/data-types/enums)。 `Grade` 声明类型后的`?`表示 `Grade` 属性可以为 [null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。 Null 的级别不同于零级别，null 表示分数未知或尚未赋值。

`StudentID` 属性是一个外键，`Student` 是与其且对应的导航属性。 `Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含单个 `Student` 实体 (与前面所看到的 `Student.Enrollments` 导航属性不同后，`Student`中可以容纳多个 `Enrollment` 实体)。

`CourseID` 属性是一个外键，`Course` 是与其且对应的导航属性。 `Enrollment` 实体与一个 `Course` 实体相关联。

实体框架将属性指定为外键属性，如果该属性命名为 *&lt;导航属性名称&gt;&lt;主键属性名称&gt;* （例如，`StudentID` 导航属性 `Student`，因为 `Student` 实体的主键是 `ID`）。 也可以将外键属性命名为相同 *&lt;主键属性名称&gt;* （例如 `CourseID`，因为 `Course` 实体的主键是 `CourseID`）。

### <a name="the-course-entity"></a>Course 实体

- 在 "*模型*" 文件夹中，创建*Course.cs*，并将模板代码替换为以下代码：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 属性是导航属性。 一个 `Course` 体可以与任意数量的 `Enrollment` 实体相关。

在本系列的后续教程中，我们将详细介绍 <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 特性。 简单来说，此特性让你能自行指定主键，而不是让数据库自动指定主键。

## <a name="create-the-database-context"></a>创建数据库上下文

为给定数据模型协调实体框架功能的主类是*数据库上下文*类。 可以通过从[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx)类派生来创建此类。 在代码中，可以指定要包含在数据模型中的实体。 你还可以定义某些 Entity Framework 行为。 在此项目中将数据库上下文类命名为 `SchoolContext`。

- 若要在 ContosoUniversity 项目中创建文件夹，请在**解决方案资源管理器**中右键单击该项目，然后单击 "**添加**"，然后单击 "**新建文件夹**"。 将新文件夹命名为*DAL* （适用于数据访问层）。 在该文件夹中，创建一个名为*SchoolContext.cs*的新类文件，并将模板代码替换为以下代码：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>指定实体集

此代码为每个实体集创建一个[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx)属性。 在实体框架术语中，*实体集*通常对应于数据库表，*实体*对应于表中的行。

> [!NOTE]
>
> 您可以省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 语句，它的工作原理相同。 实体框架将隐式包含它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。

### <a name="specify-the-connection-string"></a>指定连接字符串

连接字符串的名称（稍后要添加到 web.config 文件中）将传递到构造函数。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

你还可以传递连接字符串本身，而不是存储在 web.config 文件中的连接字符串的名称。 有关用于指定要使用的数据库的选项的详细信息，请参阅[连接字符串和模型](/ef/ef6/fundamentals/configuring/connection-strings)。

如果未显式指定连接字符串或名称，则实体框架假设连接字符串名称与类名称相同。 然后，本示例中的默认连接字符串名称将为 `SchoolContext`，就像您显式指定的一样。

### <a name="specify-singular-table-names"></a>指定单一表名称

[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的 `modelBuilder.Conventions.Remove` 语句阻止复数表名称。 如果未执行此操作，则数据库中生成的表将被命名为 `Students`、`Courses`和 `Enrollments`。 相反，表名称将为 `Student`、`Course`和 `Enrollment`。 开发者对表名称是否应为复数意见不一。 本教程使用单数形式，但重要的是，您可以选择您喜欢的任何形式，包括或省略此行代码。

## <a name="initialize-db-with-test-data"></a>使用测试数据初始化数据库

当应用程序运行时，实体框架可以自动创建（或删除并重新创建）数据库。 您可以指定在每次应用程序运行时执行此操作，或仅在模型与现有数据库不同步时执行此操作。 您还可以编写一个 `Seed` 方法，该方法实体框架在创建数据库后自动调用，以便使用测试数据填充它。

默认行为是只在数据库不存在时才创建数据库（如果模型发生了更改并且数据库已存在，则会引发异常）。 在本部分中，你将指定在模型发生更改时应删除并重新创建数据库。 删除数据库将导致丢失所有数据。 这通常在开发过程中是正常的，因为在重新创建数据库时将运行 `Seed` 方法，并将重新创建测试数据。 但在生产环境中，您通常不希望每次需要更改数据库架构时都丢失所有数据。 稍后，您将了解如何使用 Code First 迁移更改数据库架构（而不是删除和重新创建数据库）来处理模型更改。

1. 在 DAL 文件夹中，创建一个名为*SchoolInitializer.cs*的新类文件，并将模板代码替换为以下代码，这会导致在需要时创建数据库，并将测试数据加载到新数据库中。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` 方法采用数据库上下文对象作为输入参数，方法中的代码使用该对象将新实体添加到数据库中。 对于每个实体类型，代码将创建新实体的集合，将其添加到相应的 `DbSet` 属性，然后将更改保存到数据库。 不需要在每个实体组之后调用 `SaveChanges` 方法，如此处所示，但这样做可帮助您找到问题的根源（如果代码写入数据库时出现异常）。

2. 若要告诉实体框架使用初始值设定项类，请将一个元素添加到应用程序*web.config*文件（位于根项目文件夹中）的 `entityFramework` 元素中，如以下示例中所示：

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type` 指定完全限定的上下文类名称和它所在的程序集，并且 `databaseinitializer type` 指定初始值设定项类及其所在程序集的完全限定名称。 （如果不希望 EF 使用初始值设定项，则可在 `context` 元素上设置属性： `disableDatabaseInitialization="true"`。）有关详细信息，请参阅[配置文件设置](/ef/ef6/fundamentals/configuring/config-file)。

   在*web.config 文件中*设置初始值设定项的替代方法是在*Global.asax.cs*文件中将 `Database.SetInitializer` 语句添加到 `Application_Start` 方法，以便在代码中执行此操作。 有关详细信息，请参阅[了解实体框架 Code First 中的数据库初始值设定项](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。

现在已设置应用程序，以便在应用程序的给定运行中首次访问数据库时，实体框架将数据库与模型（`SchoolContext` 和实体类）进行比较。 如果存在差异，应用程序会删除并重新创建数据库。

> [!NOTE]
> 将应用程序部署到生产 web 服务器时，必须删除或禁用删除并重新创建该数据库的代码。 你将在本系列的后续教程中执行此操作。

## <a name="set-up-ef-6-to-use-localdb"></a>设置 EF 6 以使用 LocalDB

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)是 SQL Server Express 数据库引擎的轻型版本。 它易于安装和配置，可以按需启动并在用户模式下运行。 LocalDB 在 SQL Server Express 的特殊执行模式下运行，该模式使您能够将数据库用作 *.mdf*文件。 如果希望能够使用项目复制数据库，则可以将 LocalDB 数据库文件放在 web 项目的*应用\_Data*文件夹中。 使用 SQL Server Express 中的用户实例功能，还可以使用 *.mdf*文件，但不推荐使用用户实例功能;因此，建议使用 LocalDB 来处理 *.mdf*文件。 默认情况下，使用 Visual Studio 安装 LocalDB。

通常，SQL Server Express 不用于生产 web 应用程序。 不建议将 LocalDB 特别用于 web 应用程序，因为它不能与 IIS 一起使用。

- 在本教程中，你将使用 LocalDB。 打开应用程序*web.config*文件，并在 `appSettings` 元素前面添加一个 `connectionStrings` 元素，如下面的示例中所示。 （请确保更新根项目文件夹中的*web.config 文件。* "*视图*" 子文件夹中还有一个不需要更新*的 web.config 文件*。

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

添加的连接字符串指定实体框架将使用名为*ContosoUniversity1*的 LocalDB 数据库。 （数据库尚不存在，但 EF 会创建它。）如果要在应用中创建数据库 *\_Data*文件夹，可以将 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 添加到连接字符串。 有关连接字符串的详细信息，请参阅[SQL Server ASP.NET Web 应用程序的连接字符串](/previous-versions/aspnet/jj653752(v=vs.110))。

在*web.config 文件中，实际上*不需要连接字符串。 如果没有提供连接字符串，实体框架会根据上下文类使用默认连接字符串。 有关详细信息，请参阅[Code First 到新的数据库](/ef/ef6/modeling/code-first/workflows/new-database)。

## <a name="create-controller-and-views"></a>创建控制器和视图

现在，您将创建一个网页来显示数据。 请求数据的过程会自动触发数据库的创建。 首先创建一个新的控制器。 但在执行此操作之前，请生成项目，使模型和上下文类可用于 MVC 控制器基架。

1. 右键单击**解决方案资源管理器**中的 "**控制器**" 文件夹，选择 "**添加**"，然后单击 "**新建基架项**"。
2. 在 "**添加基架**" 对话框中，选择 "**包含视图的 MVC 5 控制器，使用实体框架**"，然后选择 "**添加**"。

     ![在 Visual Studio 中添加基架对话框](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. 在 "**添加控制器**" 对话框中，进行以下选择，然后选择 "**添加**"：

   - Model 类： **Student （ContosoUniversity）** 。 （如果未在下拉列表中看到此选项，请生成项目，然后重试。）
   - 数据上下文类： **SchoolContext （ContosoUniversity）** 。
   - 控制器名称： **StudentController** （而不是 StudentsController）。
   - 为其他字段保留默认值。

     单击 "**添加**" 时，scaffolder 会创建一个*StudentController.cs*文件和一组与控制器一起使用的视图（*cshtml*文件）。 在将来创建使用实体框架的项目时，还可以利用 scaffolder 的一些附加功能：创建第一个模型类，不要创建连接字符串，然后在 "**添加控制器**" 框中，通过选择 "**数据上下文类**" 旁边的 **+** 按钮来指定**新的数据上下文**。 Scaffolder 将创建 `DbContext` 类和连接字符串以及控制器和视图。
4. Visual Studio 将打开*Controllers\StudentController.cs*文件。 你会看到已创建实例化数据库上下文对象的类变量：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` 操作方法通过读取数据库上下文实例的 `Students` 属性，从*学生*实体集中获取学生列表：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\Index.cshtml*视图将此列表显示在表中：

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. 按 Ctrl+F5 运行项目。 （如果收到 "无法创建卷影副本" 错误，请关闭浏览器并重试。）

     单击 "**学生**" 选项卡以查看 `Seed` 方法插入的测试数据。 根据浏览器窗口的大小，你会在顶部的地址栏中看到 "学生" 选项卡链接，或单击右上角以查看链接。

     ![菜单按钮](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>查看数据库

当你运行 "学生" 页且应用程序尝试访问数据库时，EF 发现没有数据库并创建了数据库。 然后，EF 运行 seed 方法来用数据填充数据库。

您可以使用**服务器资源管理器**或**SQL Server 对象资源管理器**（SSOX）在 Visual Studio 中查看数据库。 对于本教程，你将使用**服务器资源管理器**。

1. 关闭浏览器。
2. 在**服务器资源管理器**中，展开 "**数据连接**" （可能需要首先选择 "刷新" 按钮），展开 "**学校上下文（ContosoUniversity）** "，然后展开 "**表**" 以查看新数据库中的表。

3. 右键单击**Student**表，然后单击 "**显示表数据**"，查看已创建的列和插入到该表中的行。

4. 关闭**服务器资源管理器**连接。

*ContosoUniversity1*和 *.ldf*数据库文件位于 *% USERPROFILE%* 文件夹中。

由于你使用的是 `DropCreateDatabaseIfModelChanges` 初始值设定项，因此你现在可以对 `Student` 类进行更改，然后再次运行应用程序，并将自动重新创建数据库以匹配你的更改。 例如，如果向 `Student` 类添加 `EmailAddress` 属性，请再次运行 "学生" 页，然后再次查看表，您将看到一个新的 `EmailAddress` 列。

## <a name="conventions"></a>约定

您必须编写的代码量，以便实体框架能够为您创建完整数据库，这是因为*约定*或实体框架所做的假设。 其中一些内容已经过说明，或已被使用，无需注意它们：

- 实体类名称的复数形式用作表名称。
- 使用实体属性名作为列名。
- 命名为 `ID` 或*classname* `ID` 的实体属性被识别为主键属性。
- 如果属性命名为 *&lt;导航属性名称&gt;&lt;primary key 属性名称&gt;* （例如 `StudentID` 导航属性 `Student`，因为 `Student` 实体的主键是 `ID`），则该属性将被解释为外键属性。 也可以将外键属性命名为相同 &lt;主键属性名称&gt; （例如 `EnrollmentID`，因为 `Enrollment` 实体的主键是 `EnrollmentID`）。

你已了解到可以重写约定。 例如，你指定了表名不应为复数，稍后你将看到如何将属性显式标记为外键属性。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

有关 EF 6 的详细信息，请参阅以下文章：

* [ASP.NET 数据访问 - 推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)

* [Code First 约定](/ef/ef6/modeling/code-first/conventions/built-in)

* [创建更复杂的数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建 MVC web 应用
> * 设置网站样式
> * 安装实体框架6
> * 已创建数据模型
> * 已创建数据库上下文
> * 已使用测试数据初始化数据库
> * 设置 EF 6 以使用 LocalDB
> * 已创建控制器和视图
> * 已查看数据库

转到下一篇文章，了解如何在控制器和视图中查看和自定义创建、读取、更新、删除（CRUD）代码。
> [!div class="nextstepaction"]
> [实现基本的 CRUD 功能](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)