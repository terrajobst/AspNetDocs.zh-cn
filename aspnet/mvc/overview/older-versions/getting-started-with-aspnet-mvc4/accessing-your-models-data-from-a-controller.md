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
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="cd629-104">从控制器访问模型的数据</span><span class="sxs-lookup"><span data-stu-id="cd629-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="cd629-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cd629-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="cd629-106">[此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="cd629-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="cd629-107">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="cd629-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="cd629-108">在本部分中，您将创建一个新的 `MoviesController` 类，然后编写代码来检索影片数据并使用视图模板在浏览器中显示该数据。</span><span class="sxs-lookup"><span data-stu-id="cd629-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="cd629-109">在继续执行下一步之前，请**生成应用程序**。</span><span class="sxs-lookup"><span data-stu-id="cd629-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="cd629-110">右键单击 "*控制器*" 文件夹，然后创建新的 `MoviesController` 控制器。</span><span class="sxs-lookup"><span data-stu-id="cd629-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="cd629-111">在生成应用程序之前，不会显示以下选项。</span><span class="sxs-lookup"><span data-stu-id="cd629-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="cd629-112">选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="cd629-112">Select the following options:</span></span>

- <span data-ttu-id="cd629-113">控制器名称： **MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="cd629-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="cd629-114">（这是默认值。</span><span class="sxs-lookup"><span data-stu-id="cd629-114">(This is the default.</span></span> <span data-ttu-id="cd629-115">)</span><span class="sxs-lookup"><span data-stu-id="cd629-115">)</span></span>
- <span data-ttu-id="cd629-116">模板：**包含读/写操作和视图的 MVC 控制器，使用实体框架**。</span><span class="sxs-lookup"><span data-stu-id="cd629-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="cd629-117">Model 类：**电影（MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="cd629-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="cd629-118">数据上下文类： **MovieDBContext （MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="cd629-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="cd629-119">视图： **Razor （CSHTML）** 。</span><span class="sxs-lookup"><span data-stu-id="cd629-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="cd629-120">（默认值。）</span><span class="sxs-lookup"><span data-stu-id="cd629-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="cd629-122">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="cd629-122">Click **Add**.</span></span> <span data-ttu-id="cd629-123">Visual Studio Express 创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="cd629-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="cd629-124">项目的 "*控制器*" 文件夹中*的 MoviesController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="cd629-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="cd629-125">项目的 "*视图*" 文件夹中的 "*电影*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="cd629-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="cd629-126">在新的*Views\Movies* *文件夹中* *创建. cshtml、Delete （* cshtml）、Details、</span><span class="sxs-lookup"><span data-stu-id="cd629-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="cd629-127">ASP.NET MVC 4 自动创建 CRUD （创建、读取、更新和删除）操作方法和视图（创建、读取、更新和删除）操作方法和视图（自动创建 CRUD 操作方法和视图）。</span><span class="sxs-lookup"><span data-stu-id="cd629-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="cd629-128">现在，你有了一个功能完备的 web 应用程序，它允许你创建、列出、编辑和删除电影条目。</span><span class="sxs-lookup"><span data-stu-id="cd629-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="cd629-129">运行应用程序，并通过将 */Movies*追加到浏览器地址栏中的 URL 来浏览到 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="cd629-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="cd629-130">由于应用程序依赖于默认路由（在*global.asax*文件中定义），因此浏览器请求 `http://localhost:xxxxx/Movies` 会路由到 `Movies` 控制器的默认 `Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="cd629-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="cd629-131">换句话说，浏览器请求 `http://localhost:xxxxx/Movies` 与浏览器请求 `http://localhost:xxxxx/Movies/Index`有效。</span><span class="sxs-lookup"><span data-stu-id="cd629-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="cd629-132">结果为空电影列表，因为尚未添加任何影片。</span><span class="sxs-lookup"><span data-stu-id="cd629-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="cd629-133">创建电影</span><span class="sxs-lookup"><span data-stu-id="cd629-133">Creating a Movie</span></span>

<span data-ttu-id="cd629-134">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="cd629-134">Select the **Create New** link.</span></span> <span data-ttu-id="cd629-135">输入有关电影的一些详细信息，然后单击 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="cd629-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="cd629-136">单击 "**创建**" 按钮会将窗体发布到服务器，在该窗体中，电影信息保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="cd629-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="cd629-137">然后，你会被重定向到 */Movies* URL，在该 URL 中，你可以在列表中看到新创建的电影。</span><span class="sxs-lookup"><span data-stu-id="cd629-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="cd629-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="cd629-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="cd629-139">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="cd629-139">Create a couple more movie entries.</span></span> <span data-ttu-id="cd629-140">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="cd629-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="cd629-141">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="cd629-141">Examining the Generated Code</span></span>

<span data-ttu-id="cd629-142">打开*Controllers\MoviesController.cs*文件并检查生成的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="cd629-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="cd629-143">下面显示了包含 `Index` 方法的电影控制器的一部分。</span><span class="sxs-lookup"><span data-stu-id="cd629-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="cd629-144">如前文所述，`MoviesController` 类中的以下行将实例化电影数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="cd629-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="cd629-145">可以使用影片数据库上下文来查询、编辑和删除影片。</span><span class="sxs-lookup"><span data-stu-id="cd629-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="cd629-146">对 `Movies` 控制器的请求将返回电影数据库的 `Movies` 表中的所有条目，然后将结果传递到 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="cd629-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="cd629-147">强类型模型和 @model 关键字</span><span class="sxs-lookup"><span data-stu-id="cd629-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="cd629-148">在本教程的前面部分，你已了解控制器如何使用 `ViewBag` 对象将数据或对象传递到视图模板。</span><span class="sxs-lookup"><span data-stu-id="cd629-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="cd629-149">`ViewBag` 是一个动态对象，它提供了一种用于向视图传递信息的后期绑定方法。</span><span class="sxs-lookup"><span data-stu-id="cd629-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="cd629-150">ASP.NET MVC 还提供将强类型化数据或对象传递到视图模板的功能。</span><span class="sxs-lookup"><span data-stu-id="cd629-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="cd629-151">此强类型方法可在 Visual Studio 编辑器中更好地编译代码和更丰富的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="cd629-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="cd629-152">Visual Studio 中的基架机制将此方法与 `MoviesController` 类结合使用，并在创建方法和视图时查看模板。</span><span class="sxs-lookup"><span data-stu-id="cd629-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="cd629-153">在*Controllers\MoviesController.cs*文件中，检查生成的 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="cd629-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="cd629-154">下面显示了包含 `Details` 方法的电影控制器的一部分。</span><span class="sxs-lookup"><span data-stu-id="cd629-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="cd629-155">如果找到 `Movie`，则 `Movie` 模型的实例将传递到详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="cd629-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="cd629-156">检查*Views\Movies\Details.cshtml*文件的内容。</span><span class="sxs-lookup"><span data-stu-id="cd629-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="cd629-157">通过将 `@model` 语句包含在视图模板文件的顶部，可以指定视图所需的对象类型。</span><span class="sxs-lookup"><span data-stu-id="cd629-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="cd629-158">创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：</span><span class="sxs-lookup"><span data-stu-id="cd629-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="cd629-159">此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。</span><span class="sxs-lookup"><span data-stu-id="cd629-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="cd629-160">例如，在*详细信息*模板中，代码将每个电影字段传递到 `DisplayNameFor`，并将[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助器与强类型 `Model` 对象一起传递。</span><span class="sxs-lookup"><span data-stu-id="cd629-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="cd629-161">"创建" 和 "编辑" 方法和 "视图" 模板也会传递影片模型对象。</span><span class="sxs-lookup"><span data-stu-id="cd629-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="cd629-162">检查*MoviesController.cs*文件中的*索引 cshtml*视图模板和 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="cd629-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="cd629-163">请注意，当调用 `Index` 操作方法中的 `View` helper 方法时，代码如何创建[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象。</span><span class="sxs-lookup"><span data-stu-id="cd629-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="cd629-164">然后，该代码将此 `Movies` 列表从控制器传递到视图：</span><span class="sxs-lookup"><span data-stu-id="cd629-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="cd629-165">创建影片控制器时，Visual Studio Express 会自动将以下 `@model` 语句包含在*索引 cshtml*文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="cd629-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="cd629-166">此 `@model` 指令允许使用强类型的 `Model` 对象访问控制器传递给视图的电影列表。</span><span class="sxs-lookup"><span data-stu-id="cd629-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="cd629-167">例如，在*索引 cshtml*模板中，代码通过对强类型化 `Model` 对象执行 `foreach` 语句来循环播放电影：</span><span class="sxs-lookup"><span data-stu-id="cd629-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="cd629-168">因为 `Model` 对象是强类型的（作为 `IEnumerable<Movie>` 对象），所以循环中的每个 `item` 对象均键入为 `Movie`。</span><span class="sxs-lookup"><span data-stu-id="cd629-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="cd629-169">除此之外，这意味着您可以在代码编辑器中对代码进行编译时检查，并获得完整的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="cd629-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="cd629-171">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="cd629-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="cd629-172">实体框架 Code First 检测到提供的数据库连接字符串指向的 `Movies` 数据库尚不存在，因此 Code First 会自动创建数据库。</span><span class="sxs-lookup"><span data-stu-id="cd629-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="cd629-173">你可以通过查看*应用\_Data*文件夹来验证它是否已创建。</span><span class="sxs-lookup"><span data-stu-id="cd629-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="cd629-174">如果看不到 "*电影 .mdf* " 文件，请单击 "**解决方案资源管理器**" 工具栏中的 "**显示所有文件**" 按钮，单击 "**刷新**" 按钮，然后展开 "*应用\_数据*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="cd629-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="cd629-175">双击 *""，以打开*"**数据库资源管理器**"，然后展开 "**表**" 文件夹以查看 "电影" 表。</span><span class="sxs-lookup"><span data-stu-id="cd629-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="cd629-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="cd629-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="cd629-177">如果 "数据库资源管理器" 未显示，请从 "**工具**" 菜单中选择 "**连接到数据库**"，然后取消 "**选择数据源**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="cd629-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="cd629-178">这将强制打开数据库资源管理器。</span><span class="sxs-lookup"><span data-stu-id="cd629-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="cd629-179">如果使用的是 VWD 或 Visual Studio 2010，并收到类似于以下内容的错误：</span><span class="sxs-lookup"><span data-stu-id="cd629-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="cd629-180">数据库 "C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES。无法打开 .MDF "，因为它是版本706。</span><span class="sxs-lookup"><span data-stu-id="cd629-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="cd629-181">此服务器支持版本655和更早版本。</span><span class="sxs-lookup"><span data-stu-id="cd629-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="cd629-182">不支持降级路径。</span><span class="sxs-lookup"><span data-stu-id="cd629-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="cd629-183">用户代码未处理 &quot;InvalidOperation 异常&quot; 提供的 SqlConnection 未指定初始目录。</span><span class="sxs-lookup"><span data-stu-id="cd629-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="cd629-184">需要安装[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)和[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)。</span><span class="sxs-lookup"><span data-stu-id="cd629-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="cd629-185">验证在上一页中指定的 `MovieDBContext` 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="cd629-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="cd629-186">右键单击 `Movies` 表，然后选择 "**显示表数据**" 以查看创建的数据。</span><span class="sxs-lookup"><span data-stu-id="cd629-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="cd629-187">右键单击 `Movies` 表，然后选择 "**打开表定义**"，查看实体框架 Code First 创建的表结构。</span><span class="sxs-lookup"><span data-stu-id="cd629-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="cd629-188">请注意，`Movies` 表的架构是如何映射到前面创建的 `Movie` 类的。</span><span class="sxs-lookup"><span data-stu-id="cd629-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="cd629-189">实体框架 Code First 会根据 `Movie` 类自动为你创建此架构。</span><span class="sxs-lookup"><span data-stu-id="cd629-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="cd629-190">完成后，请通过右键单击*MovieDBContext*并选择 "**关闭连接**" 来关闭连接。</span><span class="sxs-lookup"><span data-stu-id="cd629-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="cd629-191">（如果不关闭连接，则在下次运行项目时可能会收到错误）。</span><span class="sxs-lookup"><span data-stu-id="cd629-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="cd629-192">现在，你已创建了数据库和一个简单的列表页，用于显示内容。</span><span class="sxs-lookup"><span data-stu-id="cd629-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="cd629-193">在下一教程中，我们将检查基架代码的其余部分，并添加 `SearchIndex` 方法和 `SearchIndex` 视图，使您能够在此数据库中搜索电影。</span><span class="sxs-lookup"><span data-stu-id="cd629-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cd629-194">[上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="cd629-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
