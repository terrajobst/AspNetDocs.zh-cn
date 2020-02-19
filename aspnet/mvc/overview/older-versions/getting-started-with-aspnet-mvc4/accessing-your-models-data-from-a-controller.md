---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456161"
---
# <a name="accessing-your-models-data-from-a-controller"></a>从控制器访问模型的数据

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

在本部分中，您将创建一个新的 `MoviesController` 类，然后编写代码来检索影片数据并使用视图模板在浏览器中显示该数据。

在继续执行下一步之前，请**生成应用程序**。

右键单击 "*控制器*" 文件夹，然后创建新的 `MoviesController` 控制器。 在生成应用程序之前，不会显示以下选项。 选择以下选项：

- 控制器名称： **MoviesController**。 （这是默认值。 )
- 模板：**包含读/写操作和视图的 MVC 控制器，使用实体框架**。
- Model 类：**电影（MvcMovie）** 。
- 数据上下文类： **MovieDBContext （MvcMovie）** 。
- 视图： **Razor （CSHTML）** 。 （默认值。）

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

单击“添加”。 Visual Studio Express 创建以下文件和文件夹：

- 项目的 "*控制器*" 文件夹中*的 MoviesController.cs*文件。
- 项目的 "*视图*" 文件夹中的 "*电影*" 文件夹。
- 在新的*Views\Movies* *文件夹中* *创建. cshtml、Delete （* cshtml）、Details、

ASP.NET MVC 4 自动创建 CRUD （创建、读取、更新和删除）操作方法和视图（创建、读取、更新和删除）操作方法和视图（自动创建 CRUD 操作方法和视图）。 现在，你有了一个功能完备的 web 应用程序，它允许你创建、列出、编辑和删除电影条目。

运行应用程序，并通过将 */Movies*追加到浏览器地址栏中的 URL 来浏览到 `Movies` 控制器。 由于应用程序依赖于默认路由（在*global.asax*文件中定义），因此浏览器请求 `http://localhost:xxxxx/Movies` 会路由到 `Movies` 控制器的默认 `Index` 操作方法。 换句话说，浏览器请求 `http://localhost:xxxxx/Movies` 与浏览器请求 `http://localhost:xxxxx/Movies/Index`有效。 结果为空电影列表，因为尚未添加任何影片。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>创建电影

选择“新建”链接。 输入有关电影的一些详细信息，然后单击 "**创建**" 按钮。

![](accessing-your-models-data-from-a-controller/_static/image3.png)

单击 "**创建**" 按钮会将窗体发布到服务器，在该窗体中，电影信息保存在数据库中。 然后，你会被重定向到 */Movies* URL，在该 URL 中，你可以在列表中看到新创建的电影。

![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")

再创建几个其他的电影条目。 试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。

## <a name="examining-the-generated-code"></a>检查生成的代码

打开*Controllers\MoviesController.cs*文件并检查生成的 `Index` 方法。 下面显示了包含 `Index` 方法的电影控制器的一部分。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

如前文所述，`MoviesController` 类中的以下行将实例化电影数据库上下文。 可以使用影片数据库上下文来查询、编辑和删除影片。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

对 `Movies` 控制器的请求将返回电影数据库的 `Movies` 表中的所有条目，然后将结果传递到 `Index` 视图。

## <a name="strongly-typed-models-and-the-model-keyword"></a>强类型模型和 @model 关键字

在本教程的前面部分，你已了解控制器如何使用 `ViewBag` 对象将数据或对象传递到视图模板。 `ViewBag` 是一个动态对象，它提供了一种用于向视图传递信息的后期绑定方法。

ASP.NET MVC 还提供将强类型化数据或对象传递到视图模板的功能。 此强类型方法可在 Visual Studio 编辑器中更好地编译代码和更丰富的 IntelliSense。 Visual Studio 中的基架机制将此方法与 `MoviesController` 类结合使用，并在创建方法和视图时查看模板。

在*Controllers\MoviesController.cs*文件中，检查生成的 `Details` 方法。 下面显示了包含 `Details` 方法的电影控制器的一部分。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

如果找到 `Movie`，则 `Movie` 模型的实例将传递到详细信息视图。 检查*Views\Movies\Details.cshtml*文件的内容。

通过将 `@model` 语句包含在视图模板文件的顶部，可以指定视图所需的对象类型。 创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。 例如，在*详细信息*模板中，代码将每个电影字段传递到 `DisplayNameFor`，并将[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助器与强类型 `Model` 对象一起传递。 "创建" 和 "编辑" 方法和 "视图" 模板也会传递影片模型对象。

检查*MoviesController.cs*文件中的*索引 cshtml*视图模板和 `Index` 方法。 请注意，当调用 `Index` 操作方法中的 `View` helper 方法时，代码如何创建[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象。 然后，该代码将此 `Movies` 列表从控制器传递到视图：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

创建影片控制器时，Visual Studio Express 会自动将以下 `@model` 语句包含在*索引 cshtml*文件的顶部：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

此 `@model` 指令允许使用强类型的 `Model` 对象访问控制器传递给视图的电影列表。 例如，在*索引 cshtml*模板中，代码通过对强类型化 `Model` 对象执行 `foreach` 语句来循环播放电影：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

因为 `Model` 对象是强类型的（作为 `IEnumerable<Movie>` 对象），所以循环中的每个 `item` 对象均键入为 `Movie`。 除此之外，这意味着您可以在代码编辑器中对代码进行编译时检查，并获得完整的 IntelliSense 支持：

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

实体框架 Code First 检测到提供的数据库连接字符串指向的 `Movies` 数据库尚不存在，因此 Code First 会自动创建数据库。 你可以通过查看*应用\_Data*文件夹来验证它是否已创建。 如果看不到 "*电影 .mdf* " 文件，请单击 "**解决方案资源管理器**" 工具栏中的 "**显示所有文件**" 按钮，单击 "**刷新**" 按钮，然后展开 "*应用\_数据*" 文件夹。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

双击 *""，以打开*"**数据库资源管理器**"，然后展开 "**表**" 文件夹以查看 "电影" 表。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> 如果 "数据库资源管理器" 未显示，请从 "**工具**" 菜单中选择 "**连接到数据库**"，然后取消 "**选择数据源**" 对话框。 这将强制打开数据库资源管理器。

> [!NOTE]
> 如果使用的是 VWD 或 Visual Studio 2010，并收到类似于以下内容的错误：
> 
> - 数据库 "C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES。无法打开 .MDF "，因为它是版本706。 此服务器支持版本655和更早版本。 不支持降级路径。
> - 用户代码未处理 &quot;InvalidOperation 异常&quot; 提供的 SqlConnection 未指定初始目录。
> 
> 需要安装[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)和[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)。 验证在上一页中指定的 `MovieDBContext` 连接字符串。

右键单击 `Movies` 表，然后选择 "**显示表数据**" 以查看创建的数据。

![](accessing-your-models-data-from-a-controller/_static/image8.png)

右键单击 `Movies` 表，然后选择 "**打开表定义**"，查看实体框架 Code First 创建的表结构。

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

请注意，`Movies` 表的架构是如何映射到前面创建的 `Movie` 类的。 实体框架 Code First 会根据 `Movie` 类自动为你创建此架构。

完成后，请通过右键单击*MovieDBContext*并选择 "**关闭连接**" 来关闭连接。 （如果不关闭连接，则在下次运行项目时可能会收到错误）。

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

现在，你已创建了数据库和一个简单的列表页，用于显示内容。 在下一教程中，我们将检查基架代码的其余部分，并添加 `SearchIndex` 方法和 `SearchIndex` 视图，使您能够在此数据库中搜索电影。

> [!div class="step-by-step"]
> [上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)
