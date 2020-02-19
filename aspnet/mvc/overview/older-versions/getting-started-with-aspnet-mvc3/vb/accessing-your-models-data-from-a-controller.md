---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457921"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="1c87e-103">从控制器访问模型的数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="1c87e-103">Accessing your Model's Data from a Controller (VB)</span></span>

<span data-ttu-id="1c87e-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1c87e-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="1c87e-105">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="1c87e-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="1c87e-106">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="1c87e-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="1c87e-107">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="1c87e-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="1c87e-108">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="1c87e-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="1c87e-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="1c87e-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="1c87e-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="1c87e-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="1c87e-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="1c87e-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="1c87e-112">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="1c87e-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="1c87e-113">本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="1c87e-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="1c87e-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="1c87e-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="1c87e-115">如果愿意C#，请切换到本教程的[ C#版本](../cs/accessing-your-models-data-from-a-controller.md)。</span><span class="sxs-lookup"><span data-stu-id="1c87e-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>

<span data-ttu-id="1c87e-116">在本部分中，您将创建一个新的 `MoviesController` 类，然后编写代码来检索影片数据并使用视图模板在浏览器中显示该数据。</span><span class="sxs-lookup"><span data-stu-id="1c87e-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="1c87e-117">在继续操作之前，请确保生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c87e-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="1c87e-118">右键单击 "*控制器*" 文件夹，然后创建新的 `MoviesController` 控制器。</span><span class="sxs-lookup"><span data-stu-id="1c87e-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="1c87e-119">选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="1c87e-119">Select the following options:</span></span>

- <span data-ttu-id="1c87e-120">控制器名称： **MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="1c87e-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="1c87e-121">（这是默认值。）</span><span class="sxs-lookup"><span data-stu-id="1c87e-121">(This is the default.)</span></span>
- <span data-ttu-id="1c87e-122">模板：**包含读/写操作和视图的控制器，使用实体框架**。</span><span class="sxs-lookup"><span data-stu-id="1c87e-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="1c87e-123">Model 类：**电影（MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="1c87e-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="1c87e-124">数据上下文类： **MovieDBContext （MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="1c87e-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="1c87e-125">视图： **Razor （CSHTML）** 。</span><span class="sxs-lookup"><span data-stu-id="1c87e-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="1c87e-126">（默认值。）</span><span class="sxs-lookup"><span data-stu-id="1c87e-126">(The default.)</span></span>

<span data-ttu-id="1c87e-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="1c87e-128">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="1c87e-128">Click **Add**.</span></span> <span data-ttu-id="1c87e-129">Visual Web Developer 会创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="1c87e-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="1c87e-130">项目的 "*控制器*" 文件夹中*的 MoviesController*文件。</span><span class="sxs-lookup"><span data-stu-id="1c87e-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="1c87e-131">项目的 "*视图*" 文件夹中的 "*电影*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c87e-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="1c87e-132">在新的 Views\Movies 文件夹中创建 、Node.js *、详细信息。* Vbhtml、node.js 和*Index。*</span><span class="sxs-lookup"><span data-stu-id="1c87e-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="1c87e-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="1c87e-134">ASP.NET MVC 3 基架机制自动创建 CRUD （创建、读取、更新和删除）操作方法和视图。</span><span class="sxs-lookup"><span data-stu-id="1c87e-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="1c87e-135">现在，你有了一个功能完备的 web 应用程序，它允许你创建、列出、编辑和删除电影条目。</span><span class="sxs-lookup"><span data-stu-id="1c87e-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="1c87e-136">运行应用程序，并通过将 */Movies*追加到浏览器地址栏中的 URL 来浏览到 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="1c87e-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="1c87e-137">由于应用程序依赖于默认路由（在*global.asax*文件中定义），因此浏览器请求 `http://localhost:xxxxx/Movies` 会路由到 `Movies` 控制器的默认 `Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="1c87e-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="1c87e-138">换句话说，浏览器请求 `http://localhost:xxxxx/Movies` 与浏览器请求 `http://localhost:xxxxx/Movies/Index`有效。</span><span class="sxs-lookup"><span data-stu-id="1c87e-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="1c87e-139">结果为空电影列表，因为尚未添加任何影片。</span><span class="sxs-lookup"><span data-stu-id="1c87e-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="1c87e-140">创建电影</span><span class="sxs-lookup"><span data-stu-id="1c87e-140">Creating a Movie</span></span>

<span data-ttu-id="1c87e-141">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="1c87e-141">Select the **Create New** link.</span></span> <span data-ttu-id="1c87e-142">输入有关电影的一些详细信息，然后单击 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="1c87e-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="1c87e-143">单击 "**创建**" 按钮会将窗体发布到服务器，在该窗体中，电影信息保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="1c87e-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="1c87e-144">然后，你会被重定向到 */Movies* URL，在该 URL 中，你可以在列表中看到新创建的电影。</span><span class="sxs-lookup"><span data-stu-id="1c87e-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="1c87e-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="1c87e-146">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="1c87e-146">Create a couple more movie entries.</span></span> <span data-ttu-id="1c87e-147">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="1c87e-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="1c87e-148">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="1c87e-148">Examining the Generated Code</span></span>

<span data-ttu-id="1c87e-149">打开*Controllers\MoviesController.vb*文件并检查生成的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="1c87e-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="1c87e-150">下面显示了包含 `Index` 方法的电影控制器的一部分。</span><span class="sxs-lookup"><span data-stu-id="1c87e-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="1c87e-151">如前文所述，`MoviesController` 类中的以下行将实例化电影数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="1c87e-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="1c87e-152">可以使用影片数据库上下文来查询、编辑和删除影片。</span><span class="sxs-lookup"><span data-stu-id="1c87e-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="1c87e-153">对 `Movies` 控制器的请求将返回电影数据库的 `Movies` 表中的所有条目，然后将结果传递到 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="1c87e-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="1c87e-154">强类型模型和 @model 关键字</span><span class="sxs-lookup"><span data-stu-id="1c87e-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="1c87e-155">在本教程的前面部分，你已了解控制器如何使用 `ViewBag` 对象将数据或对象传递到视图模板。</span><span class="sxs-lookup"><span data-stu-id="1c87e-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="1c87e-156">`ViewBag` 是一个动态对象，它提供了一种用于向视图传递信息的后期绑定方法。</span><span class="sxs-lookup"><span data-stu-id="1c87e-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="1c87e-157">ASP.NET MVC 还提供将强类型化数据或对象传递到视图模板的功能。</span><span class="sxs-lookup"><span data-stu-id="1c87e-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="1c87e-158">利用此强类型方法，可以更好地对代码进行编译时检查，并在 Visual Web Developer 编辑器中更丰富的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="1c87e-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="1c87e-159">我们将使用此方法和 `MoviesController` 类和*索引。*</span><span class="sxs-lookup"><span data-stu-id="1c87e-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="1c87e-160">请注意，当调用 `Index` 操作方法中的 `View` helper 方法时，代码如何创建[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象。</span><span class="sxs-lookup"><span data-stu-id="1c87e-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="1c87e-161">然后，该代码将此 `Movies` 列表从控制器传递到视图：</span><span class="sxs-lookup"><span data-stu-id="1c87e-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="1c87e-162">通过将 `@ModelType` 语句包含在视图模板文件的顶部，可以指定视图所需的对象类型。</span><span class="sxs-lookup"><span data-stu-id="1c87e-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="1c87e-163">创建影片控制器时，Visual Web Developer 会自动在*索引*`@model` 语句的顶部包含以下语句：</span><span class="sxs-lookup"><span data-stu-id="1c87e-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="1c87e-164">此 `@ModelType` 指令允许使用强类型的 `Model` 对象访问控制器传递给视图的电影列表。</span><span class="sxs-lookup"><span data-stu-id="1c87e-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="1c87e-165">例如，在索引（ *vbhtml* ）模板中，代码通过对强类型化 `Model` 对象执行 `foreach` 语句来循环播放电影：</span><span class="sxs-lookup"><span data-stu-id="1c87e-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="1c87e-166">因为 `Model` 对象是强类型的（作为 `IEnumerable<Movie>` 对象），所以循环中的每个 `item` 对象均键入为 `Movie`。</span><span class="sxs-lookup"><span data-stu-id="1c87e-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="1c87e-167">除此之外，这意味着您可以在代码编辑器中对代码进行编译时检查，并获得完整的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="1c87e-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="1c87e-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="1c87e-169">使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="1c87e-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="1c87e-170">实体框架 Code First 检测到提供的数据库连接字符串指向的 `Movies` 数据库尚不存在，因此 Code First 会自动创建数据库。</span><span class="sxs-lookup"><span data-stu-id="1c87e-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="1c87e-171">你可以通过查看*应用\_Data*文件夹来验证它是否已创建。</span><span class="sxs-lookup"><span data-stu-id="1c87e-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="1c87e-172">如果看*不到 "* 所有文件"，请单击 "**解决方案资源管理器**" 工具栏中的 "**显示所有文件**" 按钮，单击 "**刷新**" 按钮，然后展开 "*应用\_数据*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c87e-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="1c87e-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="1c87e-174">双击 "**服务器资源管理器**打开 *"。*</span><span class="sxs-lookup"><span data-stu-id="1c87e-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="1c87e-175">然后展开 "**表**" 文件夹，查看已在数据库中创建的表。</span><span class="sxs-lookup"><span data-stu-id="1c87e-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="1c87e-176">如果在双击 ""，则会出现错误 *，请确保*已安装**适用于 SQL Server Compact 4.0 的 VISUAL Studio 2010 SP1 工具**。</span><span class="sxs-lookup"><span data-stu-id="1c87e-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="1c87e-177">（有关软件的链接，请参阅本系列教程第1部分中的先决条件列表。）如果你现在安装该版本，则必须关闭并重新打开 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="1c87e-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>

<span data-ttu-id="1c87e-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="1c87e-179">有两个表，一个用于 `Movie` 实体集，然后是 `EdmMetadata` 表。</span><span class="sxs-lookup"><span data-stu-id="1c87e-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="1c87e-180">实体框架使用 `EdmMetadata` 表来确定模型和数据库不同步的时间。</span><span class="sxs-lookup"><span data-stu-id="1c87e-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="1c87e-181">右键单击 `Movies` 表，然后选择 "**显示表数据**" 以查看创建的数据。</span><span class="sxs-lookup"><span data-stu-id="1c87e-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="1c87e-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="1c87e-183">右键单击 `Movies` 表，然后选择 "**编辑表架构**"。</span><span class="sxs-lookup"><span data-stu-id="1c87e-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="1c87e-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="1c87e-186">请注意，`Movies` 表的架构是如何映射到前面创建的 `Movie` 类的。</span><span class="sxs-lookup"><span data-stu-id="1c87e-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="1c87e-187">实体框架 Code First 会根据 `Movie` 类自动为你创建此架构。</span><span class="sxs-lookup"><span data-stu-id="1c87e-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="1c87e-188">完成后，关闭连接。</span><span class="sxs-lookup"><span data-stu-id="1c87e-188">When you're finished, close the connection.</span></span> <span data-ttu-id="1c87e-189">（如果不关闭连接，则在下次运行项目时可能会收到错误）。</span><span class="sxs-lookup"><span data-stu-id="1c87e-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="1c87e-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="1c87e-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="1c87e-191">现在，你已创建了数据库和一个简单的列表页，用于显示内容。</span><span class="sxs-lookup"><span data-stu-id="1c87e-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="1c87e-192">在下一教程中，我们将检查基架代码的其余部分，并添加 `SearchIndex` 方法和 `SearchIndex` 视图，使您能够在此数据库中搜索电影。</span><span class="sxs-lookup"><span data-stu-id="1c87e-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c87e-193">[上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="1c87e-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
