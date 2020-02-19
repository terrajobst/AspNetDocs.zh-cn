---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e9c7f24d426635760b613f570b85455ce71b3dc
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458053"
---
# <a name="accessing-your-models-data-from-a-controller-c"></a>从控制器访问模型的数据 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。
> 
> 
> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题提供了包含C#源代码的 Visual Web Developer 项目。 [下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

在本部分中，您将创建一个新的 `MoviesController` 类，然后编写代码来检索影片数据并使用视图模板在浏览器中显示该数据。 在继续操作之前，请确保生成应用程序。

右键单击 "*控制器*" 文件夹，然后创建新的 `MoviesController` 控制器。 选择以下选项：

- 控制器名称： **MoviesController**。 （这是默认值。 )
- 模板：**包含读/写操作和视图的控制器，使用实体框架**。
- Model 类：**电影（MvcMovie）** 。
- 数据上下文类： **MovieDBContext （MvcMovie）** 。
- 视图： **Razor （CSHTML）** 。 （默认值。）

[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)

单击“添加”。 Visual Web Developer 会创建以下文件和文件夹：

- 项目的 "*控制器*" 文件夹中*的 MoviesController.cs*文件。
- 项目的 "*视图*" 文件夹中的 "*电影*" 文件夹。
- 在新的*Views\Movies* *文件夹中* *创建. cshtml、Delete （* cshtml）、Details、

[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 基架机制自动创建 CRUD （创建、读取、更新和删除）操作方法和视图。 现在，你有了一个功能完备的 web 应用程序，它允许你创建、列出、编辑和删除电影条目。

运行应用程序，并通过将 */Movies*追加到浏览器地址栏中的 URL 来浏览到 `Movies` 控制器。 由于应用程序依赖于默认路由（在*global.asax*文件中定义），因此浏览器请求 `http://localhost:xxxxx/Movies` 会路由到 `Movies` 控制器的默认 `Index` 操作方法。 换句话说，浏览器请求 `http://localhost:xxxxx/Movies` 与浏览器请求 `http://localhost:xxxxx/Movies/Index`有效。 结果为空电影列表，因为尚未添加任何影片。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a>创建电影

选择“新建”链接。 输入有关电影的一些详细信息，然后单击 "**创建**" 按钮。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

单击 "**创建**" 按钮会将窗体发布到服务器，在该窗体中，电影信息保存在数据库中。 然后，你会被重定向到 */Movies* URL，在该 URL 中，你可以在列表中看到新创建的电影。

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)

再创建几个其他的电影条目。 试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。

## <a name="examining-the-generated-code"></a>检查生成的代码

打开*Controllers\MoviesController.cs*文件并检查生成的 `Index` 方法。 下面显示了包含 `Index` 方法的电影控制器的一部分。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

如前文所述，`MoviesController` 类中的以下行将实例化电影数据库上下文。 可以使用影片数据库上下文来查询、编辑和删除影片。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

对 `Movies` 控制器的请求将返回电影数据库的 `Movies` 表中的所有条目，然后将结果传递到 `Index` 视图。

## <a name="strongly-typed-models-and-the-model-keyword"></a>强类型模型和 @model 关键字

在本教程的前面部分，你已了解控制器如何使用 `ViewBag` 对象将数据或对象传递到视图模板。 `ViewBag` 是一个动态对象，它提供了一种用于向视图传递信息的后期绑定方法。

ASP.NET MVC 还提供将强类型化数据或对象传递到视图模板的功能。 利用此强类型方法，可以更好地对代码进行编译时检查，并在 Visual Web Developer 编辑器中更丰富的 IntelliSense。 我们将使用此方法和 `MoviesController` 类和*索引. cshtml*视图模板。

请注意，当调用 `Index` 操作方法中的 `View` helper 方法时，代码如何创建[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象。 然后，该代码将此 `Movies` 列表从控制器传递到视图：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

通过将 `@model` 语句包含在视图模板文件的顶部，可以指定视图所需的对象类型。 创建影片控制器时，Visual Web Developer 会在*索引 cshtml*文件的顶部自动包含以下 `@model` 语句：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

此 `@model` 指令允许使用强类型的 `Model` 对象访问控制器传递给视图的电影列表。 例如，在*索引 cshtml*模板中，代码通过对强类型化 `Model` 对象执行 `foreach` 语句来循环播放电影：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

因为 `Model` 对象是强类型的（作为 `IEnumerable<Movie>` 对象），所以循环中的每个 `item` 对象均键入为 `Movie`。 除此之外，这意味着您可以在代码编辑器中对代码进行编译时检查，并获得完整的 IntelliSense 支持：

[![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntelliSense")](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>使用 SQL Server Compact

实体框架 Code First 检测到提供的数据库连接字符串指向的 `Movies` 数据库尚不存在，因此 Code First 会自动创建数据库。 你可以通过查看*应用\_Data*文件夹来验证它是否已创建。 如果看*不到 "* 所有文件"，请单击 "**解决方案资源管理器**" 工具栏中的 "**显示所有文件**" 按钮，单击 "**刷新**" 按钮，然后展开 "*应用\_数据*" 文件夹。

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)

双击 "**服务器资源管理器**打开 *"。* 然后展开 "**表**" 文件夹，查看已在数据库中创建的表。

> [!NOTE]
> 如果在双击 ""，则会出现错误 *，请确保*已安装[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）。 （有关软件的链接，请参阅本系列教程第1部分中的先决条件列表。）如果你现在安装该版本，则必须关闭并重新打开 Visual Web Developer。

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)

有两个表，一个用于 `Movie` 实体集，然后是 `EdmMetadata` 表。 实体框架使用 `EdmMetadata` 表来确定模型和数据库不同步的时间。

右键单击 `Movies` 表，然后选择 "**显示表数据**" 以查看创建的数据。

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png "MoviesTable")](accessing-your-models-data-from-a-controller/_static/image15.png)

右键单击 `Movies` 表，然后选择 "**编辑表架构**"。

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)

[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)

请注意，`Movies` 表的架构是如何映射到前面创建的 `Movie` 类的。 实体框架 Code First 会根据 `Movie` 类自动为你创建此架构。

完成后，关闭连接。 （如果不关闭连接，则在下次运行项目时可能会收到错误）。

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)

现在，你已创建了数据库和一个简单的列表页，用于显示内容。 在下一教程中，我们将检查基架代码的其余部分，并添加 `SearchIndex` 方法和 `SearchIndex` 视图，使您能够在此数据库中搜索电影。

> [!div class="step-by-step"]
> [上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)
