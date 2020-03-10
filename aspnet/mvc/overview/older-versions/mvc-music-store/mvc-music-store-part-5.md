---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第5部分：编辑窗体和模板化 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第5部分涵盖编辑窗体和模板化。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450908"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="54dbb-104">第5部分：编辑窗体和模板化</span><span class="sxs-lookup"><span data-stu-id="54dbb-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="54dbb-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="54dbb-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="54dbb-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="54dbb-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="54dbb-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="54dbb-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="54dbb-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="54dbb-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="54dbb-109">第5部分涵盖编辑窗体和模板化。</span><span class="sxs-lookup"><span data-stu-id="54dbb-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="54dbb-110">在过去的章节中，我们从数据库加载数据并显示数据。</span><span class="sxs-lookup"><span data-stu-id="54dbb-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="54dbb-111">在本章中，我们还将启用数据编辑。</span><span class="sxs-lookup"><span data-stu-id="54dbb-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="54dbb-112">创建 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="54dbb-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="54dbb-113">首先，我们将创建一个名为**StoreManagerController**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="54dbb-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="54dbb-114">对于这一控制器，我们将利用 ASP.NET MVC 3 工具更新中提供的基架功能。</span><span class="sxs-lookup"><span data-stu-id="54dbb-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="54dbb-115">设置 "添加控制器" 对话框的选项，如下所示。</span><span class="sxs-lookup"><span data-stu-id="54dbb-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="54dbb-116">当你单击 "添加" 按钮时，你将看到 ASP.NET MVC 3 基架机制为你执行了很好的工作：</span><span class="sxs-lookup"><span data-stu-id="54dbb-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="54dbb-117">它使用本地实体框架变量创建新的 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="54dbb-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="54dbb-118">它将 StoreManager 文件夹添加到项目的 Views 文件夹中</span><span class="sxs-lookup"><span data-stu-id="54dbb-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="54dbb-119">它向唱片集类添加了 Create. cshtml、Delete. cshtml、Details、node.js、和 Index。</span><span class="sxs-lookup"><span data-stu-id="54dbb-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="54dbb-120">新的 StoreManager 控制器类包括 CRUD （创建、读取、更新、删除）控制器操作，这些操作知道如何使用唱片集模型类，并使用我们的实体框架上下文进行数据库访问。</span><span class="sxs-lookup"><span data-stu-id="54dbb-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="54dbb-121">修改基架视图</span><span class="sxs-lookup"><span data-stu-id="54dbb-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="54dbb-122">请务必记住，尽管此代码是为我们生成的，但它是标准的 ASP.NET MVC 代码，就像我们在本教程中编写的一样。</span><span class="sxs-lookup"><span data-stu-id="54dbb-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="54dbb-123">它旨在节省编写样板控制器代码和手动创建强类型视图所需的时间，但这并不是你在可怕警告的注释中所看到的生成代码的类型。编写.</span><span class="sxs-lookup"><span data-stu-id="54dbb-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="54dbb-124">这是你的代码，你应更改它。</span><span class="sxs-lookup"><span data-stu-id="54dbb-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="54dbb-125">接下来，让我们从快速编辑 StoreManager 索引视图（/Views/StoreManager/Index.cshtml）开始。</span><span class="sxs-lookup"><span data-stu-id="54dbb-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="54dbb-126">此视图将显示一个表，其中列出了使用 "编辑/详细信息/删除" 链接的商店中的专辑，并包括唱片集的公共属性。</span><span class="sxs-lookup"><span data-stu-id="54dbb-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="54dbb-127">我们将删除 AlbumArtUrl 字段，因为它在此显示中不太有用。</span><span class="sxs-lookup"><span data-stu-id="54dbb-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="54dbb-128">在视图代码 &lt;表&gt; 部分中，删除围绕 AlbumArtUrl 引用 &lt;的&gt; 和 &lt;td&gt; 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="54dbb-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="54dbb-129">修改后的视图代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="54dbb-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="54dbb-130">第一次查看存储管理器</span><span class="sxs-lookup"><span data-stu-id="54dbb-130">A first look at the Store Manager</span></span>

<span data-ttu-id="54dbb-131">现在，运行应用程序并浏览到/StoreManager/。</span><span class="sxs-lookup"><span data-stu-id="54dbb-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="54dbb-132">这会显示刚刚修改的存储管理器索引，并显示存储中具有要编辑、详细信息和删除链接的唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="54dbb-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="54dbb-133">单击 "编辑" 链接将显示包含唱片集字段的编辑窗体，包括用于流派和艺术家的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="54dbb-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="54dbb-134">单击底部的 "返回列表" 链接，然后单击唱片集的详细信息链接。</span><span class="sxs-lookup"><span data-stu-id="54dbb-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="54dbb-135">这将显示单个唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="54dbb-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="54dbb-136">再次单击 "返回列表" 链接，然后单击 "删除" 链接。</span><span class="sxs-lookup"><span data-stu-id="54dbb-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="54dbb-137">此时将显示一个确认对话框，其中显示了唱片集详细信息，并询问是否确实要删除它。</span><span class="sxs-lookup"><span data-stu-id="54dbb-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="54dbb-138">单击底部的 "删除" 按钮将删除该唱片集，并返回到 "索引" 页，其中显示了已删除的唱片集。</span><span class="sxs-lookup"><span data-stu-id="54dbb-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="54dbb-139">我们并不是使用存储管理器完成的，但我们有工作控制器和查看代码，使 CRUD 操作开始。</span><span class="sxs-lookup"><span data-stu-id="54dbb-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="54dbb-140">查看存储管理器控制器代码</span><span class="sxs-lookup"><span data-stu-id="54dbb-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="54dbb-141">存储管理器控制器包含大量的代码。</span><span class="sxs-lookup"><span data-stu-id="54dbb-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="54dbb-142">接下来，从上到下。</span><span class="sxs-lookup"><span data-stu-id="54dbb-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="54dbb-143">控制器包括 MVC 控制器的一些标准命名空间，以及对模型命名空间的引用。</span><span class="sxs-lookup"><span data-stu-id="54dbb-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="54dbb-144">控制器具有 MusicStoreEntities 的专用实例，每个控制器操作都使用该实例来进行数据访问。</span><span class="sxs-lookup"><span data-stu-id="54dbb-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="54dbb-145">存储管理器索引和详细信息操作</span><span class="sxs-lookup"><span data-stu-id="54dbb-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="54dbb-146">索引视图检索唱片集列表，包括每个唱片集的引用流派和艺术家信息，正如我们先前在处理 Store Browse 方法时看到的一样。</span><span class="sxs-lookup"><span data-stu-id="54dbb-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="54dbb-147">索引视图位于对链接对象的引用之后，因此它可以显示每个唱片集的流派名称和艺术家名称，因此控制器有效并在原始请求中查询此信息。</span><span class="sxs-lookup"><span data-stu-id="54dbb-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="54dbb-148">StoreManager 控制器的详细信息控制器操作的工作原理与我们以前使用 Find （）方法按 ID 向唱片集提供的存储控制器详细信息操作完全相同，然后将其返回给视图。</span><span class="sxs-lookup"><span data-stu-id="54dbb-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="54dbb-149">创建操作方法</span><span class="sxs-lookup"><span data-stu-id="54dbb-149">The Create Action Methods</span></span>

<span data-ttu-id="54dbb-150">创建操作方法与我们目前为止所看到的方法稍有不同，因为它们处理窗体输入。</span><span class="sxs-lookup"><span data-stu-id="54dbb-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="54dbb-151">用户首次访问/StoreManager/Create/时，将显示一个空窗体。</span><span class="sxs-lookup"><span data-stu-id="54dbb-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="54dbb-152">此 HTML 页面将包含一个 &lt;窗体&gt; 元素，其中包含可在其中输入唱片集详细信息的 dropdown 和 textbox 输入元素。</span><span class="sxs-lookup"><span data-stu-id="54dbb-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="54dbb-153">用户填写唱片集格式值后，可以按 "保存" 按钮将这些更改提交回应用程序，以便保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="54dbb-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="54dbb-154">当用户按下 "保存" 按钮时，&lt;窗体&gt; 会执行 HTTP 回发到/StoreManager/Create/URL，并将 &lt;窗体&gt; 值作为 HTTP POST 的一部分提交。</span><span class="sxs-lookup"><span data-stu-id="54dbb-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="54dbb-155">通过使我们能够在 StoreManagerController 类中实现两个单独的 "创建" 操作方法（一个用于处理最初的 HTTP-GET 浏览到/StoreManager/Create/URL，另一个用于处理提交的更改的 HTTP POST），ASP.NET MVC 使我们可以轻松地将这两个 URL 调用方案的逻辑拆分开来。</span><span class="sxs-lookup"><span data-stu-id="54dbb-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="54dbb-156">使用 ViewBag 将信息传递给视图</span><span class="sxs-lookup"><span data-stu-id="54dbb-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="54dbb-157">我们已在本教程的前面部分使用了 ViewBag，但尚未谈论它。</span><span class="sxs-lookup"><span data-stu-id="54dbb-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="54dbb-158">ViewBag 允许我们将信息传递给视图，而无需使用强类型化的模型对象。</span><span class="sxs-lookup"><span data-stu-id="54dbb-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="54dbb-159">在这种情况下，"编辑 HTTP-获取控制器" 操作需要将流派和音乐家列表同时传递给窗体来填充下拉列表，最简单的方法是将其返回为 ViewBag 项。</span><span class="sxs-lookup"><span data-stu-id="54dbb-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="54dbb-160">ViewBag 是动态对象，这意味着你可以在不编写代码的情况下键入 ViewBag 或 ViewBag 来定义这些属性。</span><span class="sxs-lookup"><span data-stu-id="54dbb-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="54dbb-161">在这种情况下，控制器代码使用 ViewBag GenreId 和 ViewBag，这样，使用窗体提交的下拉值将为 GenreId 和 ArtistId，这些值是他们将设置的唱片集属性。</span><span class="sxs-lookup"><span data-stu-id="54dbb-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="54dbb-162">将使用 SelectList 对象将这些下拉值返回到窗体，此对象只是为此目的而构建的。</span><span class="sxs-lookup"><span data-stu-id="54dbb-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="54dbb-163">这是使用如下所示的代码完成的：</span><span class="sxs-lookup"><span data-stu-id="54dbb-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="54dbb-164">从操作方法代码中可以看到，三个参数用于创建此对象：</span><span class="sxs-lookup"><span data-stu-id="54dbb-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="54dbb-165">下拉列表将显示的项的列表。</span><span class="sxs-lookup"><span data-stu-id="54dbb-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="54dbb-166">请注意，这不只是一个字符串，而是传递一个流派列表。</span><span class="sxs-lookup"><span data-stu-id="54dbb-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="54dbb-167">传递给 SelectList 的下一个参数是选定的值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="54dbb-168">SelectList 如何知道如何在列表中预先选择一项。</span><span class="sxs-lookup"><span data-stu-id="54dbb-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="54dbb-169">当我们查看 "编辑" 窗体时，这会很容易理解，这非常类似。</span><span class="sxs-lookup"><span data-stu-id="54dbb-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="54dbb-170">最终参数是要显示的属性。</span><span class="sxs-lookup"><span data-stu-id="54dbb-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="54dbb-171">在这种情况下，这指示 Genre.Name 属性将显示给用户。</span><span class="sxs-lookup"><span data-stu-id="54dbb-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="54dbb-172">考虑到这一点，HTTP GET Create 操作非常简单-两个 SelectLists 已添加到 ViewBag，并且没有模型对象传递到窗体（因为尚未创建）。</span><span class="sxs-lookup"><span data-stu-id="54dbb-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="54dbb-173">用于在创建视图中显示下拉的 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="54dbb-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="54dbb-174">由于我们已经讨论了下拉值如何传递给视图，接下来让我们快速查看一下视图，查看这些值的显示方式。</span><span class="sxs-lookup"><span data-stu-id="54dbb-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="54dbb-175">在视图代码（/Views/StoreManager/Create.cshtml）中，你将看到执行以下调用以显示流派下拉。</span><span class="sxs-lookup"><span data-stu-id="54dbb-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="54dbb-176">这称为 HTML 帮助器-一种执行常见视图任务的实用工具方法。</span><span class="sxs-lookup"><span data-stu-id="54dbb-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="54dbb-177">HTML 帮助程序非常适用于保持视图代码的简洁和可读性。</span><span class="sxs-lookup"><span data-stu-id="54dbb-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="54dbb-178">ASP.NET MVC 提供 DropDownList 帮助程序，但正如我们稍后将看到的，我们可以创建自己的用于查看代码的帮助程序，我们将在应用程序中重复使用这些代码。</span><span class="sxs-lookup"><span data-stu-id="54dbb-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="54dbb-179">只需对 DropDownList 调用进行以下两项通知：在何处获取要显示的列表，以及应预先选择的值（如果有）。</span><span class="sxs-lookup"><span data-stu-id="54dbb-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="54dbb-180">第一个参数 GenreId 指示 DropDownList 在模型或 ViewBag 中查找名为 GenreId 的值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="54dbb-181">第二个参数用于指示要在下拉列表中以初始方式显示的值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="54dbb-182">由于此窗体是 Create 窗体，因此没有要预先选择的值和 String。将传递空值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="54dbb-183">处理已发布的表单值</span><span class="sxs-lookup"><span data-stu-id="54dbb-183">Handling the Posted Form values</span></span>

<span data-ttu-id="54dbb-184">如前文所述，有两个与每个窗体相关联的操作方法。</span><span class="sxs-lookup"><span data-stu-id="54dbb-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="54dbb-185">首先处理 HTTP GET 请求，并显示窗体。</span><span class="sxs-lookup"><span data-stu-id="54dbb-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="54dbb-186">第二个处理 HTTP POST 请求，其中包含已提交的窗体值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="54dbb-187">请注意，"控制器操作" 有一个 "[HttpPost]" 属性，该属性指示 ASP.NET MVC 只应响应 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="54dbb-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="54dbb-188">此操作具有四个责任：</span><span class="sxs-lookup"><span data-stu-id="54dbb-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="54dbb-189">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="54dbb-189">Read the form values</span></span>
- 2. <span data-ttu-id="54dbb-190">检查窗体值是否通过任何验证规则</span><span class="sxs-lookup"><span data-stu-id="54dbb-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="54dbb-191">如果表单提交有效，请保存数据并显示更新后的列表</span><span class="sxs-lookup"><span data-stu-id="54dbb-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="54dbb-192">如果窗体提交无效，将重新显示具有验证错误的窗体</span><span class="sxs-lookup"><span data-stu-id="54dbb-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="54dbb-193">用模型绑定读取窗体值</span><span class="sxs-lookup"><span data-stu-id="54dbb-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="54dbb-194">控制器操作正在处理窗体提交，其中包含 GenreId 和 ArtistId 的值（从下拉列表中）和文本框的标题、价格和 AlbumArtUrl 的值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="54dbb-195">尽管可以直接访问窗体值，但更好的方法是使用内置于 ASP.NET MVC 中的模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="54dbb-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="54dbb-196">当控制器操作采用模型类型作为参数时，ASP.NET MVC 将尝试使用窗体输入（以及路由和查询字符串值）来填充该类型的对象。</span><span class="sxs-lookup"><span data-stu-id="54dbb-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="54dbb-197">它通过查找名称与模型对象的属性匹配的值来实现此目标，例如，设置新的唱片集对象的 GenreId 值时，它会查找名称为 GenreId 的输入。</span><span class="sxs-lookup"><span data-stu-id="54dbb-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="54dbb-198">当使用 ASP.NET MVC 中的标准方法创建视图时，窗体将始终使用属性名称作为输入字段名称进行呈现，因此，字段名称将与之匹配。</span><span class="sxs-lookup"><span data-stu-id="54dbb-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="54dbb-199">验证模型</span><span class="sxs-lookup"><span data-stu-id="54dbb-199">Validating the Model</span></span>

<span data-ttu-id="54dbb-200">使用对 ModelState 的简单调用来验证模型。</span><span class="sxs-lookup"><span data-stu-id="54dbb-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="54dbb-201">我们尚未将任何验证规则添加到我们的唱集类中-我们将立即执行此操作，因此，现在这项检查并不太多了。</span><span class="sxs-lookup"><span data-stu-id="54dbb-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="54dbb-202">重要的是，此 ModelStat 检查将适合我们在我们的模型中进行的验证规则，因此，以后对验证规则的更改不需要对控制器操作代码进行任何更新。</span><span class="sxs-lookup"><span data-stu-id="54dbb-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="54dbb-203">保存提交的值</span><span class="sxs-lookup"><span data-stu-id="54dbb-203">Saving the submitted values</span></span>

<span data-ttu-id="54dbb-204">如果表单提交通过验证，则可以将这些值保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="54dbb-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="54dbb-205">对于实体框架，只需将模型添加到 "唱片集" 集合并调用 SaveChanges 即可。</span><span class="sxs-lookup"><span data-stu-id="54dbb-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="54dbb-206">实体框架生成合适的 SQL 命令来持久保存值。</span><span class="sxs-lookup"><span data-stu-id="54dbb-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="54dbb-207">保存数据后，我们将重定向回唱集列表，以便我们可以看到更新。</span><span class="sxs-lookup"><span data-stu-id="54dbb-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="54dbb-208">这是通过将 RedirectToAction 返回到我们要显示的控制器操作的名称来完成的。</span><span class="sxs-lookup"><span data-stu-id="54dbb-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="54dbb-209">在这种情况下，这是 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="54dbb-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="54dbb-210">显示具有验证错误的无效窗体提交</span><span class="sxs-lookup"><span data-stu-id="54dbb-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="54dbb-211">对于无效的窗体输入，会将 dropdown 值添加到 ViewBag （如在 HTTP GET case 中），并将绑定的模型值传递回要显示的视图。</span><span class="sxs-lookup"><span data-stu-id="54dbb-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="54dbb-212">使用 @Html.ValidationMessageFor HTML 帮助器自动显示验证错误。</span><span class="sxs-lookup"><span data-stu-id="54dbb-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="54dbb-213">测试 "创建" 窗体</span><span class="sxs-lookup"><span data-stu-id="54dbb-213">Testing the Create Form</span></span>

<span data-ttu-id="54dbb-214">若要对此进行测试，请运行应用程序并浏览到/StoreManager/Create/-这将显示 StoreController Create HTTP-GET 方法返回的空白窗体。</span><span class="sxs-lookup"><span data-stu-id="54dbb-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="54dbb-215">填写某些值并单击 "创建" 按钮以提交窗体。</span><span class="sxs-lookup"><span data-stu-id="54dbb-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="54dbb-216">处理编辑</span><span class="sxs-lookup"><span data-stu-id="54dbb-216">Handling Edits</span></span>

<span data-ttu-id="54dbb-217">编辑操作对（HTTP GET 和 HTTP POST）非常类似于我们刚才查看的创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="54dbb-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="54dbb-218">由于编辑方案涉及使用现有唱片集，因此编辑 HTTP-GET 方法会根据通过路由传入的 "id" 参数加载唱片集。</span><span class="sxs-lookup"><span data-stu-id="54dbb-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="54dbb-219">此用于通过 AlbumId 检索唱片集的代码与我们以前在详细信息控制器操作中查看的代码相同。</span><span class="sxs-lookup"><span data-stu-id="54dbb-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="54dbb-220">与创建/HTTP-GET 方法一样，下拉值通过 ViewBag 返回。</span><span class="sxs-lookup"><span data-stu-id="54dbb-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="54dbb-221">这样一来，我们就可以将唱片集作为模型对象返回到视图（强类型化为唱片集类），同时通过 ViewBag 传递附加数据（例如，流派列表）。</span><span class="sxs-lookup"><span data-stu-id="54dbb-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="54dbb-222">编辑 HTTP POST 操作与创建 HTTP POST 操作非常相似。</span><span class="sxs-lookup"><span data-stu-id="54dbb-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="54dbb-223">唯一的区别是，不是将新的唱片集添加到 db。唱集，我们正在使用 db 查找唱集的当前实例。条目（唱片集），并将其状态设置为 "已修改"。</span><span class="sxs-lookup"><span data-stu-id="54dbb-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="54dbb-224">这会告知实体框架我们正在修改现有的唱片集，而不是创建一个新的。</span><span class="sxs-lookup"><span data-stu-id="54dbb-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="54dbb-225">通过运行应用程序并浏览到/StoreManger/，然后单击唱片集的编辑链接，我们可以对此进行测试。</span><span class="sxs-lookup"><span data-stu-id="54dbb-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="54dbb-226">这会显示由编辑 HTTP-GET 方法显示的编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="54dbb-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="54dbb-227">填写某些值并单击 "保存" 按钮。</span><span class="sxs-lookup"><span data-stu-id="54dbb-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="54dbb-228">这会发送窗体，保存值并将我们返回到唱片集列表，其中显示值已更新。</span><span class="sxs-lookup"><span data-stu-id="54dbb-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="54dbb-229">处理删除</span><span class="sxs-lookup"><span data-stu-id="54dbb-229">Handling Deletion</span></span>

<span data-ttu-id="54dbb-230">删除遵循与编辑和创建相同的模式，使用一个控制器操作显示确认窗体，并使用另一个控制器操作来处理窗体提交。</span><span class="sxs-lookup"><span data-stu-id="54dbb-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="54dbb-231">HTTP-获取删除控制器操作与先前的 "存储管理器详细信息" 控制器操作完全相同。</span><span class="sxs-lookup"><span data-stu-id="54dbb-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="54dbb-232">我们将使用 "删除视图内容" 模板来显示已强类型化为唱片集类型的窗体。</span><span class="sxs-lookup"><span data-stu-id="54dbb-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="54dbb-233">"删除" 模板显示了该模型的所有字段，但我们可简化这一点。</span><span class="sxs-lookup"><span data-stu-id="54dbb-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="54dbb-234">将/Views/StoreManager/Delete.cshtml 中的视图代码更改为以下代码。</span><span class="sxs-lookup"><span data-stu-id="54dbb-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="54dbb-235">这会显示简化的删除确认。</span><span class="sxs-lookup"><span data-stu-id="54dbb-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="54dbb-236">单击 "删除" 按钮会使窗体回发到服务器，这将执行 DeleteConfirmed 操作。</span><span class="sxs-lookup"><span data-stu-id="54dbb-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="54dbb-237">我们的 HTTP POST 删除控制器操作执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="54dbb-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="54dbb-238">按 ID 加载唱片集</span><span class="sxs-lookup"><span data-stu-id="54dbb-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="54dbb-239">删除相册并保存更改</span><span class="sxs-lookup"><span data-stu-id="54dbb-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="54dbb-240">重定向到索引，显示已从列表中删除唱片集</span><span class="sxs-lookup"><span data-stu-id="54dbb-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="54dbb-241">若要对此进行测试，请运行应用程序并浏览到/StoreManager。</span><span class="sxs-lookup"><span data-stu-id="54dbb-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="54dbb-242">从列表中选择一个唱片集，然后单击 "删除" 链接。</span><span class="sxs-lookup"><span data-stu-id="54dbb-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="54dbb-243">此时将显示 "删除" 确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="54dbb-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="54dbb-244">单击 "删除" 按钮将删除该唱片集并返回到 "商店经理索引" 页，其中显示已删除该唱片集。</span><span class="sxs-lookup"><span data-stu-id="54dbb-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="54dbb-245">使用自定义 HTML 帮助程序截断文本</span><span class="sxs-lookup"><span data-stu-id="54dbb-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="54dbb-246">我们的商店经理索引页有一个潜在的问题。</span><span class="sxs-lookup"><span data-stu-id="54dbb-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="54dbb-247">"唱片集标题" 和 "艺术家名称" 属性的长度可能会超出我们的表格格式。</span><span class="sxs-lookup"><span data-stu-id="54dbb-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="54dbb-248">我们将创建自定义 HTML 帮助程序，以便在视图中轻松截断这些属性和其他属性。</span><span class="sxs-lookup"><span data-stu-id="54dbb-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="54dbb-249">Razor 的 @helper 语法使创建自己的 helper 函数以便在视图中使用非常简单。</span><span class="sxs-lookup"><span data-stu-id="54dbb-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="54dbb-250">打开/Views/StoreManager/Index.cshtml 视图并直接在 @model 行后添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="54dbb-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="54dbb-251">此帮助器方法使用一个字符串和最大长度以允许。</span><span class="sxs-lookup"><span data-stu-id="54dbb-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="54dbb-252">如果提供的文本小于指定的长度，则助手会按原样输出该文本。</span><span class="sxs-lookup"><span data-stu-id="54dbb-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="54dbb-253">如果更长，则会截断文本，并呈现 "..."余数。</span><span class="sxs-lookup"><span data-stu-id="54dbb-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="54dbb-254">现在，我们可以使用截断帮助器来确保唱片集标题和艺术家名称属性少于25个字符。</span><span class="sxs-lookup"><span data-stu-id="54dbb-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="54dbb-255">使用新的截断帮助器的完整视图代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="54dbb-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="54dbb-256">现在，浏览/StoreManager/URL 时，唱片集和标题会保持在最大长度以下。</span><span class="sxs-lookup"><span data-stu-id="54dbb-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="54dbb-257">注意：这会显示在一个视图中创建和使用帮助器的简单案例。</span><span class="sxs-lookup"><span data-stu-id="54dbb-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="54dbb-258">若要详细了解如何创建可在整个站点中使用的帮助程序，请参阅我的博客文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="54dbb-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="54dbb-259">[上一页](mvc-music-store-part-4.md)
> [下一页](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="54dbb-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
