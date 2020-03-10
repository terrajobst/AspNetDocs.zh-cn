---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: 用 LINQ to SQL 创建模型类（VB） |Microsoft Docs
author: microsoft
description: 本教程的目的是介绍为 ASP.NET MVC 应用程序创建模型类的一种方法。 在本教程中，您将了解如何生成模型 c 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 88a5f1037d93ef3bdc95bf60b6005ebb254ab440
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469526"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>使用 LINQ to SQL 创建模型类 (VB)

由[Microsoft](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> 本教程的目的是介绍为 ASP.NET MVC 应用程序创建模型类的一种方法。 在本教程中，您将了解如何通过利用 Microsoft LINQ to SQL 来生成模型类并执行数据库访问。

本教程的目的是介绍为 ASP.NET MVC 应用程序创建模型类的一种方法。 在本教程中，您将了解如何通过利用 Microsoft LINQ to SQL 来生成模型类并执行数据库访问。

在本教程中，我们将构建一个基本的电影数据库应用程序。 首先，我们以尽可能快、最简单的方式创建电影数据库应用程序。 我们直接从控制器操作执行所有数据访问。

接下来，了解如何使用存储库模式。 使用存储库模式需要一些更多的工作。 但是，采用此模式的优点是，它使你能够构建可适应变化并可轻松测试的应用程序。

## <a name="what-is-a-model-class"></a>什么是模型类？

MVC 模型包含未包含在 MVC 视图或 MVC 控制器中的所有应用程序逻辑。 特别是，MVC 模型包含所有应用程序业务和数据访问逻辑。

您可以使用各种不同的技术来实现您的数据访问逻辑。 例如，可以使用 Microsoft 实体框架、NHibernate、Subsonic 或 ADO.NET 类生成数据访问类。

在本教程中，我使用 LINQ to SQL 来查询和更新数据库。 LINQ to SQL 提供了一种非常简单的方法与 Microsoft SQL Server 数据库交互。 但是，请务必了解，ASP.NET MVC 框架不会以任何方式关联到 LINQ to SQL。 ASP.NET MVC 与任何数据访问技术兼容。

## <a name="create-a-movie-database"></a>创建电影数据库

在本教程中，为了说明如何生成模型类，我们构建了一个简单的电影数据库应用程序。 第一步是创建一个新数据库。 右键单击 "解决方案资源管理器" 窗口中的 "应用\_Data" 文件夹，然后选择 "**添加"、"新建项**" 菜单。 选择 SQL Server 的数据库模板，为其指定名称 MoviesDB，然后单击 "**添加**" 按钮（请参阅图1）。

[![添加新的 SQL Server 数据库](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**图 01**：添加新的 SQL Server 数据库（[单击以查看完全大小的映像](creating-model-classes-with-linq-to-sql-vb/_static/image3.png)）

创建新数据库后，可以通过双击应用\_Data 文件夹中的 MoviesDB 文件打开数据库。 双击 MoviesDB 文件将打开 "服务器资源管理器" 窗口（参见图2）。

|   | 使用 Visual Web Developer 时，"服务器资源管理器" 窗口称为 "数据库资源管理器" 窗口。 |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[使用服务器资源管理器窗口 ![](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**图 02**：使用服务器资源管理器窗口（[单击以查看完全大小的图像](creating-model-classes-with-linq-to-sql-vb/_static/image6.png)）

我们需要将一个表添加到表示电影的数据库。 右键单击 "表" 文件夹，然后选择 "**添加新表**" 菜单选项。 选择此菜单选项将打开表设计器（请参阅图3）。

[使用服务器资源管理器窗口 ![](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**图 03**：表设计器（[单击查看完全尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image9.png)）

我们需要在数据库表中添加以下列：

| **列名称** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar （200） | False |
| 导演 | nvarchar （50） | False |

需要为 Id 列执行两个特殊操作。 首先，您需要通过在表设计器中选择列并单击键的图标，将 Id 列标记为主键列。 LINQ to SQL 要求在对数据库执行插入或更新时指定主键列。

接下来，需要通过将 "是" 值指定为 "**是" 标识**属性，将 Id 列标记为标识列（请参阅图3）。 标识列是在向表中添加新的数据行时，将自动分配新数字的列。

进行这些更改后，请保存名称为 tblMovie 的表。 可以通过单击 "保存" 按钮保存表。

## <a name="create-linq-to-sql-classes"></a>创建 LINQ to SQL 类

MVC 模型将包含表示 tblMovie 数据库表的 LINQ to SQL 类。 创建这些 LINQ to SQL 类的最简单方法是：右键单击 "模型" 文件夹，选择 "**添加"、"新建项**"，选择 "LINQ to SQL 类" 模板，为类命名为 "Movie"，然后单击 "**添加**" 按钮（见图4）。

[![创建 LINQ to SQL 类](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**图 04**：创建 LINQ to SQL 类（[单击以查看完全大小的图像](creating-model-classes-with-linq-to-sql-vb/_static/image12.png)）

LINQ to SQL 类创建影片后，会立即显示对象关系设计器。 您可以将数据库表从 "服务器资源管理器" 窗口拖到 "对象关系设计器上，以创建表示特定数据库表 LINQ to SQL 类。 需要将 tblMovie 数据库表添加到对象关系设计器（请参阅图4）。

[使用对象关系设计器 ![](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**图 05**：使用对象关系设计器（[单击查看完全尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image15.png)）

默认情况下，对象关系设计器会创建一个与拖到设计器上的数据库表同名的类。 但是，我们不想要 tblMovie 类。 因此，在设计器中单击类的名称，并将类的名称更改为 "电影"。

最后，请记住单击 "**保存**" 按钮（软盘的图片）以保存 LINQ to SQL 类。 否则，对象关系设计器不会生成 LINQ to SQL 类。

## <a name="using-linq-to-sql-in-a-controller-action"></a>在控制器操作中使用 LINQ to SQL

现在我们有了 LINQ to SQL 类，可以使用这些类从数据库中检索数据。 本部分介绍如何直接在控制器操作中使用 LINQ to SQL 类。 我们将在 MVC 视图中的 tblMovies 数据库表中显示电影列表。

首先，我们需要修改 HomeController 类。 此类可在应用程序的 "控制器" 文件夹中找到。 修改类，使其类似于列表1中的类。

**列表1– `Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

列表1中的 Index （）操作使用 LINQ to SQL DataContext 类（MovieDataContext）来表示 MoviesDB 数据库。 MoveDataContext 类由 Visual Studio 对象关系设计器生成。

针对 DataContext 执行 LINQ 查询，以检索 tblMovies 数据库表中的所有电影。 电影列表被分配给名为 "电影" 的局部变量。 最后，将电影列表通过视图数据传递给视图。

为了显示电影，接下来需要修改索引视图。 可以在 Views\Home\ 文件夹中找到索引视图。 更新 "索引" 视图，使其看起来像列表2中的视图。

**列表2– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

请注意，修改后的索引视图包含视图顶部的 &lt;% @ import 命名空间%&gt; 指令。 此指令导入 MvcApplication1 命名空间。 需要使用此命名空间才能处理模型类（特别是在视图中的 Movie 类）。

清单2中的视图包含一个 For Each 循环，该循环遍历 ViewData 属性所表示的所有项。 为每个电影显示 "标题" 属性的值。

请注意，ViewData 属性的值强制转换为 IEnumerable。 为了遍历 ViewData 的内容，这是必需的。 此处的另一个选项是创建强类型视图。 创建强类型视图时，将 ViewData 属性强制转换为视图的代码隐藏类中的特定类型。

如果在修改 HomeController 类和索引视图后运行该应用程序，则会看到一个空白页。 你将看到一个空白页，因为 tblMovies 数据库表中没有电影记录。

若要向 tblMovies 数据库表添加记录，请在 "服务器资源管理器" 窗口中右键单击 "tblMovies" 数据库表（Visual Web Developer 中的 "数据库资源管理器" 窗口），然后选择菜单选项 "**显示表数据**"。 您可以使用显示的网格插入电影记录（见图5）。

[![插入电影](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**图 06**：插入影片（[单击以查看完全尺寸的图像](creating-model-classes-with-linq-to-sql-vb/_static/image18.png)）

将一些数据库记录添加到 tblMovies 表中，并运行该应用程序后，将看到图7中的页面。 所有电影数据库记录都显示在项目符号列表中。

[用索引视图 ![显示电影](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**图 07**：通过 "索引" 视图显示电影（[单击以查看完全大小的图像](creating-model-classes-with-linq-to-sql-vb/_static/image21.png)）

## <a name="using-the-repository-pattern"></a>使用存储库模式

在上一部分中，我们直接在控制器操作中使用 LINQ to SQL 类。 我们直接从 Index （）控制器操作中使用 MovieDataContext 类。 对于简单的应用程序，在执行此操作时没有任何错误。 但是，当你需要生成更复杂的应用程序时，直接在 controller 类中处理 LINQ to SQL 会产生问题。

使用控制器类中的 LINQ to SQL 使得将来难以切换数据访问技术。 例如，你可能决定从使用 Microsoft LINQ to SQL 切换为使用 Microsoft 实体框架作为你的数据访问技术。 在这种情况下，需要重新编写访问应用程序中的数据库的每个控制器。

使用控制器类中的 LINQ to SQL 也会很难为应用程序生成单元测试。 通常，在执行单元测试时不希望与数据库进行交互。 您希望使用您的单元测试来测试您的应用程序逻辑，而不是您的数据库服务器。

为了构建一个可更好地适应将来的更改并且可以更轻松地测试的 MVC 应用程序，应考虑使用存储库模式。 使用存储库模式时，将创建一个单独的存储库类，其中包含所有数据库访问逻辑。

创建存储库类时，将创建一个接口，该接口表示存储库类使用的所有方法。 在控制器中，可以针对接口而不是存储库来编写代码。 这样，以后就可以使用不同的数据访问技术来实现存储库。

清单3中的接口名为 IMovieRepository，它表示名为 .Listall （）的单个方法。

**列表 3-`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

列表4中的存储库类实现 IMovieRepository 接口。 请注意，它包含一个名为 .Listall （）的方法，该方法对应于 IMovieRepository 接口所需的方法。

**列表 4-`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

最后，列表5中的 MoviesController 类使用存储库模式。 它不再直接使用 LINQ to SQL 类。

**列表5– `Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

请注意，列表5中的 MoviesController 类具有两个构造函数。 第一个构造函数（即无参数构造函数）在应用程序运行时调用。 此构造函数创建 MovieRepository 类的一个实例，并将其传递给第二个构造函数。

第二个构造函数具有单个参数： IMovieRepository 参数。 此构造函数只是将参数的值分配给名为 \_repository 的类级字段。

MoviesController 类利用称为依赖关系注入模式的软件设计模式。 具体而言，它使用称为构造函数依赖关系注入的内容。 若要阅读有关此模式的详细信息，请参阅以下文章： Fowler：

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

请注意，MoviesController 类中的所有代码（第一个构造函数除外）都与 IMovieRepository 接口交互，而不是与实际 MovieRepository 类交互。 此代码与抽象接口交互，而不是接口的具体实现。

如果要修改应用程序使用的数据访问技术，只需使用使用备用数据库访问技术的类来实现 IMovieRepository 接口。 例如，可以创建 EntityFrameworkMovieRepository 类或 SubSonicMovieRepository 类。 由于控制器类基于接口进行编程，因此你可以将 IMovieRepository 的新实现传递到控制器类，并且类将继续工作。

此外，如果想要测试 MoviesController 类，可以将假电影存储库类传递到 MoviesController。 您可以使用类来实现 IMovieRepository 类，该类不会实际访问数据库，而是包含 IMovieRepository 接口的所有所需方法。 通过这种方式，可以对 MoviesController 类进行单元测试，而无需实际访问实际数据库。

## <a name="summary"></a>摘要

本教程的目的是演示如何通过利用 Microsoft LINQ to SQL 来创建 MVC 模型类。 我们检查了两种在 ASP.NET MVC 应用程序中显示数据库数据的策略。 首先，我们创建 LINQ to SQL 类并直接在控制器操作中使用类。 使用控制器中的 LINQ to SQL 类，可以快速轻松地在 MVC 应用程序中显示数据库数据。

接下来，我们探讨了稍微复杂一些的良性，显示数据库数据的路径。 我们充分利用了存储库模式，并在单独的存储库类中放置了所有数据库访问逻辑。 在我们的控制器中，我们针对接口而不是具体的类编写了所有代码。 存储库模式的优点在于，它使我们能够在以后轻松更改数据库访问技术，使我们可以轻松地测试控制器类。

> [!div class="step-by-step"]
> [上一页](creating-model-classes-with-the-entity-framework-vb.md)
> [下一页](displaying-a-table-of-database-data-vb.md)
