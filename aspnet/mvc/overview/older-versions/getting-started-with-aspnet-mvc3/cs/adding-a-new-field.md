---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 向电影模型和表添加新字段（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434840"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="28e15-103">向电影模型和表添加新字段 (C#)</span><span class="sxs-lookup"><span data-stu-id="28e15-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="28e15-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="28e15-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="28e15-105">[此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="28e15-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="28e15-106">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="28e15-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="28e15-107">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="28e15-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="28e15-108">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="28e15-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="28e15-109">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="28e15-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="28e15-110">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="28e15-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="28e15-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="28e15-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="28e15-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="28e15-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="28e15-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="28e15-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="28e15-114">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="28e15-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="28e15-115">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="28e15-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="28e15-116">[下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="28e15-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="28e15-117">如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="28e15-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="28e15-118">在本节中，您将对模型类进行一些更改，并了解如何更新数据库架构以匹配模型更改。</span><span class="sxs-lookup"><span data-stu-id="28e15-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="28e15-119">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="28e15-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="28e15-120">首先向现有 `Movie` 类添加新的 `Rating` 属性。</span><span class="sxs-lookup"><span data-stu-id="28e15-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="28e15-121">打开*Movie.cs*文件并添加 `Rating` 属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="28e15-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="28e15-122">完整的 `Movie` 类现在如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="28e15-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="28e15-123">使用 "**调试**&gt;**生成电影**" 菜单命令重新编译应用程序。</span><span class="sxs-lookup"><span data-stu-id="28e15-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="28e15-124">更新 `Model` 类后，还需要更新 *\Views\Movies\Index.cshtml*和 *\Views\Movies\Create.cshtml*视图模板，以支持新的 `Rating` 属性。</span><span class="sxs-lookup"><span data-stu-id="28e15-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="28e15-125">打开 " *\Views\Movies\Index.cshtml* " 文件，然后在 " **Price** " 列之后添加 `<th>Rating</th>` 列标题。</span><span class="sxs-lookup"><span data-stu-id="28e15-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="28e15-126">然后，将 `<td>` 列添加到模板末尾附近，以呈现 `@item.Rating` 值。</span><span class="sxs-lookup"><span data-stu-id="28e15-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="28e15-127">更新后的*索引 cshtml*视图模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="28e15-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="28e15-128">接下来，打开 *\Views\Movies\Create.cshtml*文件，并在窗体结尾附近添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="28e15-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="28e15-129">这将呈现一个文本框，以便您可以在创建新电影时指定级别。</span><span class="sxs-lookup"><span data-stu-id="28e15-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="28e15-130">管理模型和数据库架构差异</span><span class="sxs-lookup"><span data-stu-id="28e15-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="28e15-131">现在，你已更新了应用程序代码，以支持新的 `Rating` 属性。</span><span class="sxs-lookup"><span data-stu-id="28e15-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="28e15-132">现在，运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="28e15-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="28e15-133">不过，当你执行此操作时，你将看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="28e15-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="28e15-134">出现此错误的原因是，应用程序中更新的 `Movie` 模型类现在与现有数据库的 `Movie` 表的架构不同。</span><span class="sxs-lookup"><span data-stu-id="28e15-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="28e15-135">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="28e15-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="28e15-136">默认情况下，当你使用实体框架 Code First 来自动创建数据库时（如在本教程前面的步骤中所做的那样），Code First 将向数据库中添加一个表，以帮助跟踪数据库的架构是否与生成它的模型类的架构同步。</span><span class="sxs-lookup"><span data-stu-id="28e15-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="28e15-137">如果不同步，实体框架将引发错误。</span><span class="sxs-lookup"><span data-stu-id="28e15-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="28e15-138">这样就可以在开发时更轻松地跟踪问题，否则在运行时可能仅会发现（隐藏错误）。</span><span class="sxs-lookup"><span data-stu-id="28e15-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="28e15-139">同步检查功能导致显示您刚才看到的错误消息。</span><span class="sxs-lookup"><span data-stu-id="28e15-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="28e15-140">可以通过两种方法来解决该错误：</span><span class="sxs-lookup"><span data-stu-id="28e15-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="28e15-141">让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="28e15-142">在测试数据库上进行活动开发时，这种方法非常方便，因为它允许您将模型和数据库架构快速地一起发展。</span><span class="sxs-lookup"><span data-stu-id="28e15-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="28e15-143">不过，缺点在于丢失了数据库中的现有数据，因此*不*希望在生产数据库上使用此方法！</span><span class="sxs-lookup"><span data-stu-id="28e15-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="28e15-144">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="28e15-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="28e15-145">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="28e15-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="28e15-146">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="28e15-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="28e15-147">对于本教程，我们将使用第一种方法，即在模型发生更改时，实体框架 Code First 自动重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="28e15-148">在模型更改时自动重新创建数据库</span><span class="sxs-lookup"><span data-stu-id="28e15-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="28e15-149">让我们更新应用程序，以便在更改应用程序的模型时，Code First 自动删除并重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="28e15-150">**警告**仅当使用的是开发或测试数据库，而*从不*在包含实际数据的生产数据库中时，才应启用此方法来自动删除并重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="28e15-151">在生产服务器上使用它可能会导致数据丢失。</span><span class="sxs-lookup"><span data-stu-id="28e15-151">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="28e15-152">在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="28e15-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="28e15-153">将类命名为 "MovieInitializer"。</span><span class="sxs-lookup"><span data-stu-id="28e15-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="28e15-154">更新 `MovieInitializer` 类，使其包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="28e15-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="28e15-155">`MovieInitializer` 类指定如果模型类发生更改，则应删除模型所使用的数据库，并自动重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="28e15-156">此代码包括一个 `Seed` 方法，用于指定在创建（或重新创建）时，可自动添加到数据库中的某些默认数据。</span><span class="sxs-lookup"><span data-stu-id="28e15-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="28e15-157">这提供了用一些示例数据填充数据库的有效方法，无需在每次进行模型更改时手动填充。</span><span class="sxs-lookup"><span data-stu-id="28e15-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="28e15-158">现在，您已定义了 `MovieInitializer` 类，您需要将其连接起来，以便每次应用程序运行时，它会检查模型类是否与数据库中的架构不同。</span><span class="sxs-lookup"><span data-stu-id="28e15-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="28e15-159">如果是这样，则可以运行初始值设定项来重新创建数据库以与模型匹配，然后用示例数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="28e15-160">打开位于 `MvcMovies` 项目的根目录的*global.asax*文件：</span><span class="sxs-lookup"><span data-stu-id="28e15-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="28e15-161">*Global.asax*文件包含定义项目的整个应用程序的类，并且包含在应用程序首次启动时运行的 `Application_Start` 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="28e15-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="28e15-162">让我们将两个 using 语句添加到文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="28e15-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="28e15-163">第一个引用实体框架命名空间，第二个引用命名空间，其中 `MovieInitializer` 类所在：</span><span class="sxs-lookup"><span data-stu-id="28e15-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="28e15-164">然后查找 `Application_Start` 方法，并在方法的开头添加对 `Database.SetInitializer` 的调用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="28e15-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="28e15-165">刚添加的 `Database.SetInitializer` 语句指示当架构和数据库不匹配时，应自动删除 `MovieDBContext` 实例使用的数据库，然后重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="28e15-166">正如您所看到的，它还将用 `MovieInitializer` 类中指定的示例数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="28e15-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="28e15-167">关闭*global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="28e15-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="28e15-168">重新运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="28e15-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="28e15-169">当应用程序启动时，它会检测到模型结构不再与数据库架构匹配。</span><span class="sxs-lookup"><span data-stu-id="28e15-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="28e15-170">它会自动重新创建数据库以与新模型结构匹配，并用示例影片填充数据库：</span><span class="sxs-lookup"><span data-stu-id="28e15-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="28e15-172">单击 "**新建**" 链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="28e15-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="28e15-173">请注意，可以添加级别。</span><span class="sxs-lookup"><span data-stu-id="28e15-173">Note that you can add a rating.</span></span>

<span data-ttu-id="28e15-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="28e15-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="28e15-175">单击 **“创建”** 。</span><span class="sxs-lookup"><span data-stu-id="28e15-175">Click **Create**.</span></span> <span data-ttu-id="28e15-176">现在电影列表中显示了新电影，其中包括评分：</span><span class="sxs-lookup"><span data-stu-id="28e15-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="28e15-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="28e15-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="28e15-178">在本部分中，您将了解如何修改模型对象并使数据库与更改保持同步。</span><span class="sxs-lookup"><span data-stu-id="28e15-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="28e15-179">还了解了使用示例数据填充新创建的数据库的方法，以便可以试用方案。</span><span class="sxs-lookup"><span data-stu-id="28e15-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="28e15-180">接下来，让我们看看如何将更丰富的验证逻辑添加到模型类，并实现一些业务规则。</span><span class="sxs-lookup"><span data-stu-id="28e15-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="28e15-181">[上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="28e15-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
