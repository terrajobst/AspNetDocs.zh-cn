---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 通过输出缓存提高性能（VB） |Microsoft Docs
author: microsoft
description: 在本教程中，你将了解如何通过利用输出缓存来大幅提高 ASP.NET MVC web 应用程序的性能。 你 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: b713b56e149f196794b3223ba88e3b41bf3e34c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486650"
---
# <a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="91c3a-104">通过输出缓存提升性能 (VB)</span><span class="sxs-lookup"><span data-stu-id="91c3a-104">Improving Performance with Output Caching (VB)</span></span>

<span data-ttu-id="91c3a-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="91c3a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="91c3a-106">在本教程中，你将了解如何通过利用输出缓存来大幅提高 ASP.NET MVC web 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="91c3a-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="91c3a-107">了解如何缓存控制器操作返回的结果，以便每次新用户调用该操作时都不需要创建相同的内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="91c3a-108">本教程的目的是说明如何通过使用输出缓存来大幅提高 ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="91c3a-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="91c3a-109">使用输出缓存可以缓存控制器操作返回的内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="91c3a-110">这样，每次调用同一控制器操作时，都不需要生成相同的内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="91c3a-111">例如，假设 ASP.NET MVC 应用程序在名为 Index 的视图中显示数据库记录的列表。</span><span class="sxs-lookup"><span data-stu-id="91c3a-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="91c3a-112">通常，每次用户调用返回索引视图的控制器操作时，都必须通过执行数据库查询来从数据库中检索数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="91c3a-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="91c3a-113">另一方面，如果你可以利用输出缓存，则每次用户调用同一控制器操作时，都可以避免执行数据库查询。</span><span class="sxs-lookup"><span data-stu-id="91c3a-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="91c3a-114">视图可以从缓存中检索，而不是从控制器操作重新生成。</span><span class="sxs-lookup"><span data-stu-id="91c3a-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="91c3a-115">使用缓存可以避免在服务器上执行冗余工作。</span><span class="sxs-lookup"><span data-stu-id="91c3a-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="91c3a-116">启用输出缓存</span><span class="sxs-lookup"><span data-stu-id="91c3a-116">Enabling Output Caching</span></span>

<span data-ttu-id="91c3a-117">可以通过将 &lt;OutputCache&gt; 特性添加到单个控制器操作或整个控制器类来启用输出缓存。</span><span class="sxs-lookup"><span data-stu-id="91c3a-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="91c3a-118">例如，列表1中的控制器公开一个名为 Index （）的操作。</span><span class="sxs-lookup"><span data-stu-id="91c3a-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="91c3a-119">索引（）操作的输出将缓存10秒。</span><span class="sxs-lookup"><span data-stu-id="91c3a-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="91c3a-120">**列表1– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="91c3a-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

<span data-ttu-id="91c3a-121">在 ASP.NET MVC 的 Beta 版本中，输出缓存不适用于[http://www.MySite.com/](http://www.mysite.com/)的 URL。</span><span class="sxs-lookup"><span data-stu-id="91c3a-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="91c3a-122">相反，你必须输入类似[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。</span><span class="sxs-lookup"><span data-stu-id="91c3a-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>

<span data-ttu-id="91c3a-123">在列表1中，Index （）操作的输出缓存了10秒。</span><span class="sxs-lookup"><span data-stu-id="91c3a-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="91c3a-124">如果需要，可以指定更长的缓存持续时间。</span><span class="sxs-lookup"><span data-stu-id="91c3a-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="91c3a-125">例如，如果想要将控制器操作的输出缓存一天，则可以将缓存持续时间指定为86400秒（60秒 \* 60 分钟 \* 24 小时）。</span><span class="sxs-lookup"><span data-stu-id="91c3a-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="91c3a-126">不能保证在指定的时间内缓存内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="91c3a-127">当内存资源较低时，缓存将开始自动逐出内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="91c3a-128">列表1中的主控制器返回列表2中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="91c3a-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="91c3a-129">此视图没有什么特别之处。</span><span class="sxs-lookup"><span data-stu-id="91c3a-129">There is nothing special about this view.</span></span> <span data-ttu-id="91c3a-130">"索引" 视图只显示当前时间（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="91c3a-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="91c3a-131">**列表 2-Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="91c3a-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="91c3a-132">**图1–缓存的索引视图**</span><span class="sxs-lookup"><span data-stu-id="91c3a-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="91c3a-134">如果通过在浏览器的地址栏中输入 URL/Home/Index 来多次调用 Index （）操作，并反复在浏览器中点击 "刷新/重新加载" 按钮，则索引视图显示的时间不会更改10秒。</span><span class="sxs-lookup"><span data-stu-id="91c3a-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="91c3a-135">因为视图被缓存，所以会显示相同的时间。</span><span class="sxs-lookup"><span data-stu-id="91c3a-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="91c3a-136">需要了解的是，将为访问应用程序的所有用户缓存相同的视图。</span><span class="sxs-lookup"><span data-stu-id="91c3a-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="91c3a-137">调用 Index （）操作的任何人都将获取索引视图的相同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="91c3a-138">这意味着，web 服务器为索引视图提供服务所必须执行的工作量大大减少。</span><span class="sxs-lookup"><span data-stu-id="91c3a-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="91c3a-139">清单2中的视图执行的操作确实非常简单。</span><span class="sxs-lookup"><span data-stu-id="91c3a-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="91c3a-140">视图只显示当前时间。</span><span class="sxs-lookup"><span data-stu-id="91c3a-140">The view just displays the current time.</span></span> <span data-ttu-id="91c3a-141">不过，您可以轻松地缓存一个显示一组数据库记录的视图。</span><span class="sxs-lookup"><span data-stu-id="91c3a-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="91c3a-142">在这种情况下，每次调用返回视图的控制器操作时，都不需要从数据库中检索一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="91c3a-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="91c3a-143">缓存可以减少 web 服务器和数据库服务器必须执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="91c3a-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="91c3a-144">请勿在 MVC 视图中使用 &lt;% @ OutputCache%&gt; 指令的页面。</span><span class="sxs-lookup"><span data-stu-id="91c3a-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="91c3a-145">此指令从 Web 窗体世界中出血，不应在 ASP.NET MVC 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="91c3a-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="91c3a-146">内容缓存位置</span><span class="sxs-lookup"><span data-stu-id="91c3a-146">Where Content is Cached</span></span>

<span data-ttu-id="91c3a-147">默认情况下，当你使用 &lt;OutputCache&gt; 属性时，内容将缓存在三个位置： web 服务器、任何代理服务器和 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="91c3a-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="91c3a-148">可以通过修改 &lt;OutputCache&gt; 属性的 Location 属性，来控制缓存内容的位置。</span><span class="sxs-lookup"><span data-stu-id="91c3a-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="91c3a-149">可以将 "位置" 属性设置为以下值之一：</span><span class="sxs-lookup"><span data-stu-id="91c3a-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="91c3a-150">·随时</span><span class="sxs-lookup"><span data-stu-id="91c3a-150">· Any</span></span>
> 
> <span data-ttu-id="91c3a-151">·机</span><span class="sxs-lookup"><span data-stu-id="91c3a-151">· Client</span></span>
> 
> <span data-ttu-id="91c3a-152">·数量</span><span class="sxs-lookup"><span data-stu-id="91c3a-152">· Downstream</span></span>
> 
> <span data-ttu-id="91c3a-153">·服务</span><span class="sxs-lookup"><span data-stu-id="91c3a-153">· Server</span></span>
> 
> <span data-ttu-id="91c3a-154">·内容</span><span class="sxs-lookup"><span data-stu-id="91c3a-154">· None</span></span>
> 
> <span data-ttu-id="91c3a-155">·ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="91c3a-155">· ServerAndClient</span></span>

<span data-ttu-id="91c3a-156">默认情况下，Location 属性的值为 Any。</span><span class="sxs-lookup"><span data-stu-id="91c3a-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="91c3a-157">但是，在某些情况下，你可能只想要在浏览器或服务器上缓存。</span><span class="sxs-lookup"><span data-stu-id="91c3a-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="91c3a-158">例如，如果你要缓存为每个用户个性化的信息，则不应在服务器上缓存该信息。</span><span class="sxs-lookup"><span data-stu-id="91c3a-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="91c3a-159">如果向不同用户显示不同的信息，则应该仅在客户端上缓存该信息。</span><span class="sxs-lookup"><span data-stu-id="91c3a-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="91c3a-160">例如，列表3中的控制器公开了一个名为 GetName （）的操作，该操作将返回当前用户名。</span><span class="sxs-lookup"><span data-stu-id="91c3a-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="91c3a-161">如果插孔登录到网站并调用 GetName （）操作，则该操作将返回字符串 "Hi 插孔"。</span><span class="sxs-lookup"><span data-stu-id="91c3a-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="91c3a-162">随后，如果 Jill 登录到网站并调用 GetName （）操作，她还将获得字符串 "Hi 插座"。</span><span class="sxs-lookup"><span data-stu-id="91c3a-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="91c3a-163">在插孔最初调用控制器操作后，将在 web 服务器上为所有用户缓存此字符串。</span><span class="sxs-lookup"><span data-stu-id="91c3a-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="91c3a-164">**列表 3-Controllers\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="91c3a-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="91c3a-165">大多数情况下，列表3中的控制器不能按您所需的方式工作。</span><span class="sxs-lookup"><span data-stu-id="91c3a-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="91c3a-166">您不希望将消息 "Jill"。</span><span class="sxs-lookup"><span data-stu-id="91c3a-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="91c3a-167">永远不应在服务器缓存中缓存个性化内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="91c3a-168">但是，你可能需要在浏览器缓存中缓存个性化内容以提高性能。</span><span class="sxs-lookup"><span data-stu-id="91c3a-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="91c3a-169">如果在浏览器中缓存内容，并且用户多次调用同一控制器操作，则可以从浏览器缓存而不是服务器检索内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="91c3a-170">列表4中修改后的控制器将缓存 GetName （）操作的输出。</span><span class="sxs-lookup"><span data-stu-id="91c3a-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="91c3a-171">但是，仅在浏览器上缓存内容，而不是在服务器上缓存内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="91c3a-172">这样一来，当多个用户调用 GetName （）方法时，每个人都将获得自己的用户名，而不是其他人的用户名。</span><span class="sxs-lookup"><span data-stu-id="91c3a-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="91c3a-173">**列表 4-Controllers\UserController.vb**</span><span class="sxs-lookup"><span data-stu-id="91c3a-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="91c3a-174">请注意，列表4中的 &lt;OutputCache&gt; 属性包含一个设置为值 OutputCacheLocation 的位置属性。</span><span class="sxs-lookup"><span data-stu-id="91c3a-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="91c3a-175">&lt;OutputCache&gt; 属性还包括一个 NoStore 属性。</span><span class="sxs-lookup"><span data-stu-id="91c3a-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="91c3a-176">NoStore 属性用于通知代理服务器和浏览器，它们不应存储缓存内容的永久副本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="91c3a-177">改变输出缓存</span><span class="sxs-lookup"><span data-stu-id="91c3a-177">Varying the Output Cache</span></span>

<span data-ttu-id="91c3a-178">在某些情况下，你可能希望具有相同内容的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="91c3a-179">例如，假设您要创建一个主/详细信息页。</span><span class="sxs-lookup"><span data-stu-id="91c3a-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="91c3a-180">母版页显示电影标题列表。</span><span class="sxs-lookup"><span data-stu-id="91c3a-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="91c3a-181">单击标题时，将获得所选电影的详细信息。</span><span class="sxs-lookup"><span data-stu-id="91c3a-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="91c3a-182">如果缓存详细信息页，则无论单击哪个电影，都将显示相同电影的详细信息。</span><span class="sxs-lookup"><span data-stu-id="91c3a-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="91c3a-183">第一个用户选择的第一个电影将显示给未来的所有用户。</span><span class="sxs-lookup"><span data-stu-id="91c3a-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="91c3a-184">可以通过利用 &lt;OutputCache&gt; 属性的 VaryByParam 属性来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="91c3a-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="91c3a-185">当窗体参数或查询字符串参数不同时，此属性可让你创建具有相同内容的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="91c3a-186">例如，列表5中的控制器公开了两个名为 Master （）和 Details （）的操作。</span><span class="sxs-lookup"><span data-stu-id="91c3a-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="91c3a-187">Master （）操作返回电影标题列表，详细信息（）操作返回所选电影的详细信息。</span><span class="sxs-lookup"><span data-stu-id="91c3a-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="91c3a-188">**列表5– Controllers\MoviesController.vb**</span><span class="sxs-lookup"><span data-stu-id="91c3a-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="91c3a-189">Master （）操作包含值为 "none" 的 VaryByParam 属性。</span><span class="sxs-lookup"><span data-stu-id="91c3a-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="91c3a-190">调用 Master （）操作时，将返回母版视图的相同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="91c3a-191">忽略任何窗体参数或查询字符串参数（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="91c3a-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="91c3a-192">**图 2-/Movies/Master 视图**</span><span class="sxs-lookup"><span data-stu-id="91c3a-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="91c3a-194">**图 3-/Movies/Details 视图**</span><span class="sxs-lookup"><span data-stu-id="91c3a-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="91c3a-196">详细信息（）操作包括一个值为 "Id" 的 VaryByParam 属性。</span><span class="sxs-lookup"><span data-stu-id="91c3a-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="91c3a-197">当 Id 参数的不同值传递到控制器操作时，将生成详细信息视图的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="91c3a-198">务必要了解，使用 VaryByParam 属性会导致更多的缓存，而不是更少。</span><span class="sxs-lookup"><span data-stu-id="91c3a-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="91c3a-199">为 Id 参数的每个不同版本创建详细信息视图的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="91c3a-200">可以将 VaryByParam 属性设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="91c3a-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="91c3a-201">\* = 在窗体或查询字符串参数不同时创建不同的缓存版本。</span><span class="sxs-lookup"><span data-stu-id="91c3a-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="91c3a-202">无 = 从不创建不同的缓存版本</span><span class="sxs-lookup"><span data-stu-id="91c3a-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="91c3a-203">参数的分号列表，只要列表中有任何窗体或查询字符串参数发生变化，就创建不同的缓存版本</span><span class="sxs-lookup"><span data-stu-id="91c3a-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

#### <a name="creating-a-cache-profile"></a><span data-ttu-id="91c3a-204">创建缓存配置文件</span><span class="sxs-lookup"><span data-stu-id="91c3a-204">Creating a Cache Profile</span></span>

<span data-ttu-id="91c3a-205">作为通过修改 &lt;OutputCache&gt; 属性的属性来配置输出缓存属性的替代方法，可以在 web 配置文件（web.config）中创建缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="91c3a-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="91c3a-206">在 web 配置文件中创建缓存配置文件可提供几个重要优势。</span><span class="sxs-lookup"><span data-stu-id="91c3a-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="91c3a-207">首先，通过在 web 配置文件中配置输出缓存，可以控制控制器操作在一个中央位置缓存内容的方式。</span><span class="sxs-lookup"><span data-stu-id="91c3a-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="91c3a-208">你可以创建一个缓存配置文件，并将该配置文件应用于多个控制器或控制器操作。</span><span class="sxs-lookup"><span data-stu-id="91c3a-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="91c3a-209">其次，你可以修改 web 配置文件，而无需重新编译应用程序。</span><span class="sxs-lookup"><span data-stu-id="91c3a-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="91c3a-210">如果需要对已部署到生产环境的应用程序禁用缓存，只需修改在 web 配置文件中定义的缓存配置文件即可。</span><span class="sxs-lookup"><span data-stu-id="91c3a-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="91c3a-211">将自动检测并应用对 web 配置文件所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="91c3a-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="91c3a-212">例如，清单6中的 &lt;缓存&gt; web 配置部分定义了一个名为 Cache1Hour 的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="91c3a-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="91c3a-213">&lt;缓存&gt; 部分必须出现在 web 配置文件的 &lt;system.web&gt; 部分中。</span><span class="sxs-lookup"><span data-stu-id="91c3a-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="91c3a-214">**清单6– web.config 的缓存部分**</span><span class="sxs-lookup"><span data-stu-id="91c3a-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="91c3a-215">列表7中的控制器说明了如何使用 &lt;OutputCache&gt; 属性将 Cache1Hour 配置文件应用到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="91c3a-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="91c3a-216">**列表 7-Controllers\ProfileController.vb**</span><span class="sxs-lookup"><span data-stu-id="91c3a-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="91c3a-217">如果在列表7中调用由控制器公开的索引（）操作，则将返回1小时的相同时间。</span><span class="sxs-lookup"><span data-stu-id="91c3a-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="91c3a-218">摘要</span><span class="sxs-lookup"><span data-stu-id="91c3a-218">Summary</span></span>

<span data-ttu-id="91c3a-219">输出缓存提供了一种非常简单的方法，可显著提高 ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="91c3a-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="91c3a-220">在本教程中，已学习如何使用 &lt;OutputCache&gt; 属性来缓存控制器操作的输出。</span><span class="sxs-lookup"><span data-stu-id="91c3a-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="91c3a-221">还了解了如何修改 &lt;OutputCache&gt; 属性（如 Duration 和 VaryByParam 属性）的属性，以修改如何缓存内容。</span><span class="sxs-lookup"><span data-stu-id="91c3a-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="91c3a-222">最后，你已了解如何在 web 配置文件中定义缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="91c3a-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="91c3a-223">[上一页](understanding-action-filters-vb.md)
> [下一页](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="91c3a-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
