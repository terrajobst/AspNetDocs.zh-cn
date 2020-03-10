---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 向缓存页面添加动态内容（VB） |Microsoft Docs
author: microsoft
description: 了解如何在同一页面中混合动态和缓存内容。 通过缓存后替换，可以显示动态内容，例如横幅广告 o 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: f2f4372498e5a38bbfcb96d6e9f6338b0ef4df1f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486962"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a><span data-ttu-id="703e8-104">向缓存页添加动态内容 (VB)</span><span class="sxs-lookup"><span data-stu-id="703e8-104">Adding Dynamic Content to a Cached Page (VB)</span></span>

<span data-ttu-id="703e8-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="703e8-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="703e8-106">了解如何在同一页面中混合动态和缓存内容。</span><span class="sxs-lookup"><span data-stu-id="703e8-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="703e8-107">通过缓存后替换，可以在已缓存的页面内显示动态内容，例如横幅广告或新闻项。</span><span class="sxs-lookup"><span data-stu-id="703e8-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="703e8-108">利用输出缓存，可以显著提高 ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="703e8-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="703e8-109">并非每次请求页面时都重新生成页面，只需生成一次页面并将其缓存在多个用户的内存中即可。</span><span class="sxs-lookup"><span data-stu-id="703e8-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="703e8-110">但出现问题。</span><span class="sxs-lookup"><span data-stu-id="703e8-110">But there is a problem.</span></span> <span data-ttu-id="703e8-111">如果需要在页面中显示动态内容，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="703e8-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="703e8-112">例如，假设您想要在页面上显示横幅广告。</span><span class="sxs-lookup"><span data-stu-id="703e8-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="703e8-113">您不希望对横幅广告进行缓存，以便每个用户都能看到非常相同的广告。</span><span class="sxs-lookup"><span data-stu-id="703e8-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="703e8-114">您不会这样做！</span><span class="sxs-lookup"><span data-stu-id="703e8-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="703e8-115">幸运的是，有一个简单的解决方案。</span><span class="sxs-lookup"><span data-stu-id="703e8-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="703e8-116">可以利用名为*后缓存替换*的 ASP.NET 框架功能。</span><span class="sxs-lookup"><span data-stu-id="703e8-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="703e8-117">使用缓存后替换，可以替换缓存在内存中的页面中的动态内容。</span><span class="sxs-lookup"><span data-stu-id="703e8-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="703e8-118">通常，当你使用 &lt;OutputCache&gt; 属性输出缓存页面时，将在服务器和客户端（web 浏览器）上缓存页面。</span><span class="sxs-lookup"><span data-stu-id="703e8-118">Normally, when you output cache a page by using the &lt;OutputCache&gt; attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="703e8-119">使用缓存后替换时，页仅缓存在服务器上。</span><span class="sxs-lookup"><span data-stu-id="703e8-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="703e8-120">使用缓存后替换</span><span class="sxs-lookup"><span data-stu-id="703e8-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="703e8-121">使用缓存后替换需要两个步骤。</span><span class="sxs-lookup"><span data-stu-id="703e8-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="703e8-122">首先，需要定义一个方法，该方法返回一个字符串，该字符串表示要在缓存页面中显示的动态内容。</span><span class="sxs-lookup"><span data-stu-id="703e8-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="703e8-123">接下来，调用 Httpresponse.cache WriteSubstitution （）方法将动态内容注入到页面中。</span><span class="sxs-lookup"><span data-stu-id="703e8-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="703e8-124">例如，假设您希望在缓存的页中随机显示不同的新闻项。</span><span class="sxs-lookup"><span data-stu-id="703e8-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="703e8-125">列表1中的类公开了一个名为 RenderNews （）的方法，该方法从三个新闻项的列表中随机返回一个新闻项。</span><span class="sxs-lookup"><span data-stu-id="703e8-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="703e8-126">**列表1– Models\News.vb**</span><span class="sxs-lookup"><span data-stu-id="703e8-126">**Listing 1 – Models\News.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

<span data-ttu-id="703e8-127">若要利用缓存后替换，请调用 Httpresponse.cache WriteSubstitution （）方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="703e8-128">WriteSubstitution （）方法设置代码以将缓存页的区域替换为动态内容。</span><span class="sxs-lookup"><span data-stu-id="703e8-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="703e8-129">WriteSubstitution （）方法用于在列表2的视图中显示随机新闻项。</span><span class="sxs-lookup"><span data-stu-id="703e8-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="703e8-130">**列表 2-Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="703e8-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

<span data-ttu-id="703e8-131">RenderNews 方法传递给 WriteSubstitution （）方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="703e8-132">请注意，不会调用 RenderNews 方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-132">Notice that the RenderNews method is not called.</span></span> <span data-ttu-id="703e8-133">而是使用 AddressOf 运算符的帮助将对方法的引用传递给 WriteSubstitution （）。</span><span class="sxs-lookup"><span data-stu-id="703e8-133">Instead a reference to the method is passed to WriteSubstitution() with the help of the AddressOf operator.</span></span>

<span data-ttu-id="703e8-134">索引视图被缓存。</span><span class="sxs-lookup"><span data-stu-id="703e8-134">The Index view is cached.</span></span> <span data-ttu-id="703e8-135">视图由列表3中的控制器返回。</span><span class="sxs-lookup"><span data-stu-id="703e8-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="703e8-136">请注意，Index （）操作使用 &lt;OutputCache&gt; 特性进行修饰，这会导致索引视图缓存60秒。</span><span class="sxs-lookup"><span data-stu-id="703e8-136">Notice that the Index() action is decorated with an &lt;OutputCache&gt; attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="703e8-137">**列表 3-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="703e8-137">**Listing 3 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

<span data-ttu-id="703e8-138">即使已缓存索引视图，请求索引页时也会显示不同的随机新闻项。</span><span class="sxs-lookup"><span data-stu-id="703e8-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="703e8-139">请求 "索引" 页时，页面显示的时间不会更改60秒（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="703e8-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="703e8-140">这种情况不会发生更改，证明页面已缓存。</span><span class="sxs-lookup"><span data-stu-id="703e8-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="703e8-141">但是，由 WriteSubstitution （）方法插入的内容–随机新闻项目–随每个请求而更改。</span><span class="sxs-lookup"><span data-stu-id="703e8-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="703e8-142">**图1–在缓存页面中注入动态新闻项**</span><span class="sxs-lookup"><span data-stu-id="703e8-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="703e8-144">在 Helper 方法中使用后缓存替换</span><span class="sxs-lookup"><span data-stu-id="703e8-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="703e8-145">更简单的方法是利用缓存后的替换方法，将对 WriteSubstitution （）方法的调用封装到自定义帮助器方法中。</span><span class="sxs-lookup"><span data-stu-id="703e8-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="703e8-146">此方法由列表4中的 helper 方法说明。</span><span class="sxs-lookup"><span data-stu-id="703e8-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="703e8-147">**列表 4-Helpers\AdHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="703e8-147">**Listing 4 – Helpers\AdHelper.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

<span data-ttu-id="703e8-148">列表4包含一个 Visual Basic 模块，该模块公开两个方法： RenderBanner （）和 RenderBannerInternal （）。</span><span class="sxs-lookup"><span data-stu-id="703e8-148">Listing 4 contains a Visual Basic module that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="703e8-149">RenderBanner （）方法表示实际的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="703e8-150">此方法扩展了标准 ASP.NET MVC HtmlHelper 类，以便您可以在视图中调用 RenderBanner （），就像使用任何其他帮助器方法一样。</span><span class="sxs-lookup"><span data-stu-id="703e8-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="703e8-151">RenderBanner （）方法调用 Httpresponse.cache （）方法将 RenderBannerInternal （）方法传递给 WriteSubstitution （）方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="703e8-152">RenderBannerInternal （）方法是私有方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="703e8-153">此方法不会公开为帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="703e8-154">RenderBannerInternal （）方法从三个横幅广告图像的列表中随机返回一个横幅广告图像。</span><span class="sxs-lookup"><span data-stu-id="703e8-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="703e8-155">"列表 5" 中修改的索引视图说明了如何使用 RenderBanner （） helper 方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="703e8-156">请注意，视图顶部包含附加的 &lt;% @ Import%&gt; 指令以导入 MvcApplication1 命名空间。</span><span class="sxs-lookup"><span data-stu-id="703e8-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="703e8-157">如果忽略导入此命名空间，则 RenderBanner （）方法不会在 Html 属性上显示为方法。</span><span class="sxs-lookup"><span data-stu-id="703e8-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="703e8-158">**列表5– Views\Home\Index.aspx （with RenderBanner （）方法）**</span><span class="sxs-lookup"><span data-stu-id="703e8-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

<span data-ttu-id="703e8-159">在列表5中请求视图呈现的页面时，每个请求都会显示不同的横幅广告（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="703e8-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="703e8-160">将缓存该页，但会通过 RenderBanner （） helper 方法动态注入标题广告。</span><span class="sxs-lookup"><span data-stu-id="703e8-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="703e8-161">**图 2-显示随机横幅广告的索引视图**</span><span class="sxs-lookup"><span data-stu-id="703e8-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="703e8-163">摘要</span><span class="sxs-lookup"><span data-stu-id="703e8-163">Summary</span></span>

<span data-ttu-id="703e8-164">本教程介绍了如何在缓存页面中动态更新内容。</span><span class="sxs-lookup"><span data-stu-id="703e8-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="703e8-165">已了解如何使用 Httpresponse.cache WriteSubstitution （）方法使动态内容注入到缓存页中。</span><span class="sxs-lookup"><span data-stu-id="703e8-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="703e8-166">还了解了如何在 HTML 帮助器方法中封装对 WriteSubstitution （）方法的调用。</span><span class="sxs-lookup"><span data-stu-id="703e8-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="703e8-167">尽可能利用缓存，这可能会对 web 应用程序的性能产生显著影响。</span><span class="sxs-lookup"><span data-stu-id="703e8-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="703e8-168">如本教程中所述，即使您需要在页面中显示动态内容，也可以利用缓存。</span><span class="sxs-lookup"><span data-stu-id="703e8-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="703e8-169">[上一页](improving-performance-with-output-caching-vb.md)
> [下一页](creating-a-controller-vb.md)</span><span class="sxs-lookup"><span data-stu-id="703e8-169">[Previous](improving-performance-with-output-caching-vb.md)
[Next](creating-a-controller-vb.md)</span></span>
