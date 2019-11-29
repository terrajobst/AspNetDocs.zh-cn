---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 向视图母版页传递数据 |Microsoft Docs
author: microsoft
description: 本教程的目的是说明如何将数据从控制器传递到视图母版页。 我们检查两个将数据传递到视图的策略 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593742"
---
# <a name="passing-data-to-view-master-pages-vb"></a><span data-ttu-id="da319-104">向视图母版页传递数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="da319-104">Passing Data to View Master Pages (VB)</span></span>

<span data-ttu-id="da319-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="da319-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="da319-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="da319-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> <span data-ttu-id="da319-107">本教程的目的是说明如何将数据从控制器传递到视图母版页。</span><span class="sxs-lookup"><span data-stu-id="da319-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="da319-108">我们检查两个将数据传递给视图母版页的策略。</span><span class="sxs-lookup"><span data-stu-id="da319-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="da319-109">首先，我们讨论一种简单的解决方案，该解决方案会导致应用程序难以维护。</span><span class="sxs-lookup"><span data-stu-id="da319-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="da319-110">接下来，我们将研究一个更好的解决方案，该解决方案需要更多初始工作，但会导致应用程序更易于维护。</span><span class="sxs-lookup"><span data-stu-id="da319-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="da319-111">将数据传递给视图母版页</span><span class="sxs-lookup"><span data-stu-id="da319-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="da319-112">本教程的目的是说明如何将数据从控制器传递到视图母版页。</span><span class="sxs-lookup"><span data-stu-id="da319-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="da319-113">我们检查两个将数据传递给视图母版页的策略。</span><span class="sxs-lookup"><span data-stu-id="da319-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="da319-114">首先，我们讨论一种简单的解决方案，该解决方案会导致应用程序难以维护。</span><span class="sxs-lookup"><span data-stu-id="da319-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="da319-115">接下来，我们将研究一个更好的解决方案，该解决方案需要更多初始工作，但会导致应用程序更易于维护。</span><span class="sxs-lookup"><span data-stu-id="da319-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="da319-116">问题</span><span class="sxs-lookup"><span data-stu-id="da319-116">The Problem</span></span>

<span data-ttu-id="da319-117">假设要生成一个电影数据库应用程序，并且想要在应用程序的每一页上显示电影类别列表（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="da319-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="da319-118">而且，假设电影类别列表存储在数据库表中。</span><span class="sxs-lookup"><span data-stu-id="da319-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="da319-119">在这种情况下，可以从数据库中检索类别，并在视图母版页中呈现影片类别列表。</span><span class="sxs-lookup"><span data-stu-id="da319-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>

<span data-ttu-id="da319-120">[![在视图母版页中显示电影类别](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="da319-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="da319-121">**图 01**：在视图母版页中显示电影类别（[单击以查看完全大小的图像](passing-data-to-view-master-pages-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="da319-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image3.png))</span></span>

<span data-ttu-id="da319-122">这就是问题所在。</span><span class="sxs-lookup"><span data-stu-id="da319-122">Here's the problem.</span></span> <span data-ttu-id="da319-123">如何在母版页中检索电影类别列表？</span><span class="sxs-lookup"><span data-stu-id="da319-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="da319-124">直接在母版页中调用模型类的方法很有吸引力。</span><span class="sxs-lookup"><span data-stu-id="da319-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="da319-125">换句话说，在母版页中包含用于从数据库检索数据的代码非常有吸引力。</span><span class="sxs-lookup"><span data-stu-id="da319-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="da319-126">但是，绕过 MVC 控制器访问数据库将会违反与构建 MVC 应用程序的主要优势之一相关的问题。</span><span class="sxs-lookup"><span data-stu-id="da319-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="da319-127">在 MVC 应用程序中，你希望 mvc 控制器和 MVC 模型之间的所有交互都由 MVC 控制器进行处理。</span><span class="sxs-lookup"><span data-stu-id="da319-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="da319-128">这种关注点的分离将导致更易于维护、更适应性且可测试的应用程序。</span><span class="sxs-lookup"><span data-stu-id="da319-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="da319-129">在 MVC 应用程序中，传递给视图的所有数据（包括视图母版页）应由控制器操作传递到视图。</span><span class="sxs-lookup"><span data-stu-id="da319-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="da319-130">而且，数据应通过利用视图数据来传递。</span><span class="sxs-lookup"><span data-stu-id="da319-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="da319-131">在本教程的剩余部分中，我将介绍两种将视图数据传递到视图母版页的方法。</span><span class="sxs-lookup"><span data-stu-id="da319-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="da319-132">简单的解决方案</span><span class="sxs-lookup"><span data-stu-id="da319-132">The Simple Solution</span></span>

<span data-ttu-id="da319-133">让我们从将视图数据从控制器传递到视图母版页的最简单解决方案开始。</span><span class="sxs-lookup"><span data-stu-id="da319-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="da319-134">最简单的解决方案是在每个控制器操作中传递母版页的视图数据。</span><span class="sxs-lookup"><span data-stu-id="da319-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="da319-135">请考虑列表1中的控制器。</span><span class="sxs-lookup"><span data-stu-id="da319-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="da319-136">它公开了两个名为 `Index()` 和 `Details()`的操作。</span><span class="sxs-lookup"><span data-stu-id="da319-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="da319-137">`Index()` 操作方法返回电影数据库表中的每个电影。</span><span class="sxs-lookup"><span data-stu-id="da319-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="da319-138">`Details()` 操作方法返回特定电影类别中的每个电影。</span><span class="sxs-lookup"><span data-stu-id="da319-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="da319-139">**列表1– `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="da319-139">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

<span data-ttu-id="da319-140">请注意，`Index()` 和 `Details()` 操作都添加了两项来查看数据。</span><span class="sxs-lookup"><span data-stu-id="da319-140">Notice that both the `Index()` and the `Details()` actions add two items to view data.</span></span> <span data-ttu-id="da319-141">`Index()` 操作将添加两个键：类别和影片。</span><span class="sxs-lookup"><span data-stu-id="da319-141">The `Index()` action adds two keys: categories and movies.</span></span> <span data-ttu-id="da319-142">类别键表示 "视图" 母版页显示的电影类别的列表。</span><span class="sxs-lookup"><span data-stu-id="da319-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="da319-143">电影键表示 "索引视图" 页显示的电影列表。</span><span class="sxs-lookup"><span data-stu-id="da319-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="da319-144">`Details()` 操作还添加了两个名为 "类别" 和 "电影" 的键。</span><span class="sxs-lookup"><span data-stu-id="da319-144">The `Details()` action also adds two keys named categories and movies.</span></span> <span data-ttu-id="da319-145">类别键再次表示视图母版页显示的电影类别的列表。</span><span class="sxs-lookup"><span data-stu-id="da319-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="da319-146">电影键表示 "详细信息视图" 页显示的特定类别中的电影列表（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="da319-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>

<span data-ttu-id="da319-147">[![详细信息视图](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="da319-147">[![The Details view](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="da319-148">**图 02**：详细信息视图（[单击查看完全尺寸的图像](passing-data-to-view-master-pages-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="da319-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image6.png))</span></span>

<span data-ttu-id="da319-149">索引视图包含在列表2中。</span><span class="sxs-lookup"><span data-stu-id="da319-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="da319-150">它只是在查看数据中循环显示电影项所表示的电影列表。</span><span class="sxs-lookup"><span data-stu-id="da319-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="da319-151">**列表2– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="da319-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="da319-152">视图母版页包含在列表3中。</span><span class="sxs-lookup"><span data-stu-id="da319-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="da319-153">视图母版页从视图数据循环访问并呈现类别项表示的所有电影类别。</span><span class="sxs-lookup"><span data-stu-id="da319-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="da319-154">**列表 3-`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="da319-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="da319-155">所有数据都通过视图数据传递到视图和 "视图" 母版页。</span><span class="sxs-lookup"><span data-stu-id="da319-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="da319-156">这是将数据传递到母版页的正确方法。</span><span class="sxs-lookup"><span data-stu-id="da319-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="da319-157">那么，此解决方案有什么不妥呢？</span><span class="sxs-lookup"><span data-stu-id="da319-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="da319-158">问题在于，此解决方案违反了晾干（不要自我重复）原则。</span><span class="sxs-lookup"><span data-stu-id="da319-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="da319-159">每个控制器操作都必须添加完全相同的电影类别列表以查看数据。</span><span class="sxs-lookup"><span data-stu-id="da319-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="da319-160">在应用程序中具有重复的代码，使应用程序更加难以维护、改编和修改。</span><span class="sxs-lookup"><span data-stu-id="da319-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="da319-161">好的解决方案</span><span class="sxs-lookup"><span data-stu-id="da319-161">The Good Solution</span></span>

<span data-ttu-id="da319-162">在本部分中，我们将讨论将数据从控制器操作传递到视图母版页的替代方法和更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="da319-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="da319-163">我们不会在每个控制器操作中为母版页添加电影类别，只会将电影类别添加到视图数据一次。</span><span class="sxs-lookup"><span data-stu-id="da319-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="da319-164">视图母版页使用的所有视图数据都添加到了应用程序控制器中。</span><span class="sxs-lookup"><span data-stu-id="da319-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="da319-165">ApplicationController 类包含在列表4中。</span><span class="sxs-lookup"><span data-stu-id="da319-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="da319-166">ApplicationController 类包含在列表4中。</span><span class="sxs-lookup"><span data-stu-id="da319-166">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="da319-167">**列表 4-`Controllers\ApplicationController.vb`**</span><span class="sxs-lookup"><span data-stu-id="da319-167">**Listing 4 – `Controllers\ApplicationController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

<span data-ttu-id="da319-168">对于列表4中的应用程序控制器，应注意以下三个方面。</span><span class="sxs-lookup"><span data-stu-id="da319-168">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="da319-169">首先，请注意，该类继承自基本 System.web 类。</span><span class="sxs-lookup"><span data-stu-id="da319-169">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="da319-170">应用程序控制器是一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="da319-170">The Application controller is a controller class.</span></span>

<span data-ttu-id="da319-171">其次，请注意，应用程序控制器类是 MustInherit 类。</span><span class="sxs-lookup"><span data-stu-id="da319-171">Second, notice that the Application controller class is a MustInherit class.</span></span> <span data-ttu-id="da319-172">MustInherit 类是必须由具体类实现的类。</span><span class="sxs-lookup"><span data-stu-id="da319-172">An MustInherit class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="da319-173">由于应用程序控制器是一个 MustInherit 类，因此不能直接调用在类中定义的任何方法。</span><span class="sxs-lookup"><span data-stu-id="da319-173">Because the Application controller is an MustInherit class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="da319-174">如果尝试直接调用应用程序类，则会出现 "找不到资源" 错误消息。</span><span class="sxs-lookup"><span data-stu-id="da319-174">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="da319-175">第三，请注意，应用程序控制器包含一个用于添加电影类别列表以查看数据的构造函数。</span><span class="sxs-lookup"><span data-stu-id="da319-175">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="da319-176">继承自应用程序控制器的每个控制器类都会自动调用应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="da319-176">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="da319-177">无论何时对继承自应用程序控制器的任何控制器调用任何操作，都将自动在视图数据中包含电影类别。</span><span class="sxs-lookup"><span data-stu-id="da319-177">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="da319-178">列表5中的电影控制器继承自应用程序控制器。</span><span class="sxs-lookup"><span data-stu-id="da319-178">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="da319-179">**列表5– `Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="da319-179">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

<span data-ttu-id="da319-180">与上一节中所述的主控制器一样，电影控制器公开了两个名为 `Index()` 和 `Details()`的操作方法。</span><span class="sxs-lookup"><span data-stu-id="da319-180">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="da319-181">请注意，视图母版页显示的电影类别列表未添加到 `Index()` 或 `Details()` 方法中的查看数据。</span><span class="sxs-lookup"><span data-stu-id="da319-181">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="da319-182">由于影片控制器继承自应用程序控制器，因此会将电影类别列表添加到自动查看数据中。</span><span class="sxs-lookup"><span data-stu-id="da319-182">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="da319-183">请注意，用于为视图母版页添加视图数据的此解决方案不违反晾干（不要自我重复）原则。</span><span class="sxs-lookup"><span data-stu-id="da319-183">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="da319-184">用于将电影类别列表添加到视图数据的代码仅包含在一个位置：应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="da319-184">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="da319-185">总结</span><span class="sxs-lookup"><span data-stu-id="da319-185">Summary</span></span>

<span data-ttu-id="da319-186">在本教程中，我们讨论了将视图数据从控制器传递到视图母版页的两种方法。</span><span class="sxs-lookup"><span data-stu-id="da319-186">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="da319-187">首先，我们只是一种简单的方法，但难以维护。</span><span class="sxs-lookup"><span data-stu-id="da319-187">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="da319-188">在第一部分中，我们讨论了如何在应用程序的每个控制器操作中为视图母版页添加视图数据。</span><span class="sxs-lookup"><span data-stu-id="da319-188">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="da319-189">我们结论，这是一种不好的方法，因为它违反了晾干（不要自我重复）原则。</span><span class="sxs-lookup"><span data-stu-id="da319-189">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="da319-190">接下来，我们将讨论一个更好的策略，以便添加视图母版页查看数据所需的数据。</span><span class="sxs-lookup"><span data-stu-id="da319-190">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="da319-191">我们只在应用程序控制器中添加了一次视图数据，而不是在每个控制器操作中添加视图数据。</span><span class="sxs-lookup"><span data-stu-id="da319-191">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="da319-192">这样，就可以避免在将数据传递到 ASP.NET MVC 应用程序中的视图母版页时出现重复代码。</span><span class="sxs-lookup"><span data-stu-id="da319-192">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="da319-193">上一部分</span><span class="sxs-lookup"><span data-stu-id="da319-193">Previous</span></span>](creating-page-layouts-with-view-master-pages-vb.md)
