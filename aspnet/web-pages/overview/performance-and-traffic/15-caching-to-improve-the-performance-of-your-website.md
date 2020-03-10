---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 缓存 ASP.NET 网页（Razor）站点中的数据以获得更好的性能 |Microsoft Docs
author: Rick-Anderson
description: 你可以通过让网站存储（即缓存）来加速你的网站，通常需要相当长的时间来检索或处理 。
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521156"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a><span data-ttu-id="4d9b8-103">缓存 ASP.NET 网页（Razor）站点中的数据以获得更好的性能</span><span class="sxs-lookup"><span data-stu-id="4d9b8-103">Caching Data in an ASP.NET Web Pages (Razor) Site for Better Performance</span></span>

<span data-ttu-id="4d9b8-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4d9b8-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4d9b8-105">本文介绍如何使用 helper 来缓存信息，以便在 ASP.NET 网页（Razor）网站中提高性能。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-105">This article explains how to use a helper to cache information for faster performance in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="4d9b8-106">你可以通过使你的网站存储&#8212;起来来加速你的网站&#8212; ，并缓存通常会花费相当长的时间来检索或处理的数据结果，并且不经常更改。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-106">You can speed up your website by having it store &#8212; that is, cache &#8212; the results of data that ordinarily would take considerable time to retrieve or process and that does not change often.</span></span>
> 
> <span data-ttu-id="4d9b8-107">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="4d9b8-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="4d9b8-108">如何使用缓存来提高网站的响应能力。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-108">How to use caching to improve the responsiveness of your website.</span></span>
> 
> <span data-ttu-id="4d9b8-109">下面是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="4d9b8-109">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="4d9b8-110">`WebCache` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-110">The `WebCache` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4d9b8-111">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="4d9b8-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4d9b8-112">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="4d9b8-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="4d9b8-113">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="4d9b8-114">每次从网站请求页面时，web 服务器都必须执行一些工作才能完成请求。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-114">Every time someone requests a page from your site, the web server has to do some work in order to fulfill the request.</span></span> <span data-ttu-id="4d9b8-115">对于某些页面，服务器可能需要执行耗时较长的任务，例如从数据库中检索数据。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-115">For some of your pages, the server might have to perform tasks that take a (comparatively) long time, such as retrieving data from a database.</span></span> <span data-ttu-id="4d9b8-116">即使这些任务不需要花费很长时间，如果您的站点遇到大量的流量，导致 web 服务器执行复杂或慢任务的一系列单独请求也可能会增加许多工作。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-116">Even if these tasks don't take long in absolute terms, if your site experiences a lot of traffic, a whole series of individual requests that cause the web server to perform the complicated or slow task can add up to a lot of work.</span></span> <span data-ttu-id="4d9b8-117">这最终会影响站点的性能。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-117">This can ultimately affect the performance of the site.</span></span>

<span data-ttu-id="4d9b8-118">在这种情况下改善网站性能的一种方法是缓存数据。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-118">One way to improve the performance of your website in circumstances like this is to cache data.</span></span> <span data-ttu-id="4d9b8-119">如果你的站点获取相同信息的重复请求，并且无需为每个人员修改信息，并且不需要对其进行重新计算，则可以提取一次数据，然后存储结果。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-119">If your site gets repeated requests for the same information, and the information does not need to be modified for each person, and it's not time sensitive, instead of re-fetching or recalculating it, you can fetch the data once and then store the results.</span></span> <span data-ttu-id="4d9b8-120">下次收到请求时，只需将其从缓存中取出。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-120">The next time a request comes in for that information, you just get it out of the cache.</span></span>

<span data-ttu-id="4d9b8-121">通常情况下，您将缓存不经常更改的信息。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-121">In general, you cache information that doesn't change frequently.</span></span> <span data-ttu-id="4d9b8-122">将信息放入缓存中时，它存储在 web 服务器的内存中。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-122">When you put information in the cache, it's stored in memory on the web server.</span></span> <span data-ttu-id="4d9b8-123">可以指定应缓存的时间长度（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-123">You can specify how long it should be cached, from seconds to days.</span></span> <span data-ttu-id="4d9b8-124">缓存期到期时，会自动从缓存中删除信息。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-124">When the caching period expires, the information is automatically removed from the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="4d9b8-125">缓存中的条目可能会因为其过期而被删除。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-125">Entries in the cache might be removed for reasons other than that they've expired.</span></span> <span data-ttu-id="4d9b8-126">例如，web 服务器的内存可能会很低，并且它可以回收内存的一种方法是从缓存中引发条目。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-126">For example, the web server might temporarily run low on memory, and one way it can reclaim memory is by throwing entries out of the cache.</span></span> <span data-ttu-id="4d9b8-127">您将看到，即使您已将信息放入缓存，也必须检查以确保它在需要时仍然存在。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-127">As you'll see, even if you've put information into the cache, you have to check to be sure it's still there when you need it.</span></span>

<span data-ttu-id="4d9b8-128">假设您的网站具有显示当前温度和天气预报的页面。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-128">Imagine your website has a page that displays the current temperature and weather forecast.</span></span> <span data-ttu-id="4d9b8-129">若要获取此类信息，你可以向外部服务发送请求。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-129">To get this type of information, you might send a request to an external service.</span></span> <span data-ttu-id="4d9b8-130">由于此信息不会有很多变化（例如，在两个小时的时间段内），并且由于外部调用需要时间和带宽，因此它非常适合用于缓存。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-130">Since this information doesn't change much (within a two-hour time period, for example) and since external calls require time and bandwidth, it's a good candidate for caching.</span></span>

## <a name="adding-caching-to-a-page"></a><span data-ttu-id="4d9b8-131">向页面添加缓存</span><span class="sxs-lookup"><span data-stu-id="4d9b8-131">Adding Caching to a Page</span></span>

<span data-ttu-id="4d9b8-132">ASP.NET 包含一个 `WebCache` 帮助程序，使你可以轻松地向网站添加缓存并将数据添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-132">ASP.NET includes a `WebCache` helper that makes it easy to add caching to your site and add data to the cache.</span></span> <span data-ttu-id="4d9b8-133">在此过程中，您将创建一个缓存当前时间的页面。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-133">In this procedure, you'll create a page that caches the current time.</span></span> <span data-ttu-id="4d9b8-134">这并不是实际的示例，因为当前时间是经常更改的内容，而这种情况并不是很复杂的计算。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-134">This isn't a real-world example, since the current time is something that does change often, and that moreover isn't complex to calculate.</span></span> <span data-ttu-id="4d9b8-135">不过，这是一个很好的方法来说明缓存的操作方式。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-135">However, it's a good way to illustrate caching in action.</span></span>

1. <span data-ttu-id="4d9b8-136">将名为*WebCache*的新页面添加到网站。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-136">Add a new page named *WebCache.cshtml* to the website.</span></span>
2. <span data-ttu-id="4d9b8-137">将以下代码和标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="4d9b8-137">Add the following code and markup to the page:</span></span>

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    <span data-ttu-id="4d9b8-138">缓存数据时，可以使用一个名称将其放入缓存，此名称在整个网站中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-138">When you cache data, you put it into the cache using a name this is unique across the website.</span></span> <span data-ttu-id="4d9b8-139">在这种情况下，将使用名为 `CachedTime`的缓存条目。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-139">In this case, you'll use a cache entry named `CachedTime`.</span></span> <span data-ttu-id="4d9b8-140">这是代码示例中所示的 `cacheItemKey`。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-140">This is the `cacheItemKey` shown in the code example.</span></span>

    <span data-ttu-id="4d9b8-141">代码首先读取 `CachedTime` 缓存条目。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-141">The code first reads the `CachedTime` cache entry.</span></span> <span data-ttu-id="4d9b8-142">如果返回值（即，如果缓存项不为 null），则代码仅将时间变量的值设置为缓存数据。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-142">If a value is returned (that is, if the cache entry isn't null), the code just sets the value of the time variable to the cache data.</span></span>

    <span data-ttu-id="4d9b8-143">但是，如果缓存项不存在（也就是说，它为 null），则代码将设置时间值，将其添加到缓存中，并将过期值设置为1分钟。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-143">However, if the cache entry doesn't exist (that is, it's null), the code sets the time value, adds it to the cache, and sets an expiration value to one minute.</span></span> <span data-ttu-id="4d9b8-144">一分钟后，将放弃缓存条目。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-144">After one minute, the cache entry is discarded.</span></span> <span data-ttu-id="4d9b8-145">（缓存中某个项目的默认过期值为20分钟。）命令 `WebCache.Set(cacheItemKey, time, 1, false)` 显示了如何将当前时间值添加到缓存，并将其有效期设置为1分钟。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-145">(The default expiration value for an item in the cache is 20 minutes.) The command `WebCache.Set(cacheItemKey, time, 1, false)` shows how to add the current time value to the cache and set its expiration to 1 minute.</span></span> <span data-ttu-id="4d9b8-146">将*slidingExpiration*参数设置为 `false` 意味着在每次请求过期时间时，不会对其进行续订。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-146">Setting the *slidingExpiration* parameter to `false` means the expiration time is not renewed each time it is requested.</span></span> <span data-ttu-id="4d9b8-147">它将在其最初添加到缓存后的一分钟后过期。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-147">It will expire exactly 1 minute after it was originally added to the cache.</span></span> <span data-ttu-id="4d9b8-148">如果将此值设置为 `true` 则每次从缓存请求该值时，将重置 "1 分钟过期时间"。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-148">If you set this value to `true` the 1 minute expiration time is reset each time the value is requested from the cache.</span></span>

    <span data-ttu-id="4d9b8-149">此代码演示缓存数据时应始终使用的模式。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-149">This code illustrates the pattern you should always use when you cache data.</span></span> <span data-ttu-id="4d9b8-150">在从缓存中获取内容之前，始终首先检查 `WebCache.Get` 方法是否返回了 null。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-150">Before you get something out of the cache, always check first whether the `WebCache.Get` method has returned null.</span></span> <span data-ttu-id="4d9b8-151">请记住，缓存条目可能已过期，或者出于其他某种原因可能已被删除，因此任何给定的条目永远都不能保证位于缓存中。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-151">Remember that the cache entry might have expired or might have been removed for some other reason, so any given entry is never guaranteed to be in the cache.</span></span>
3. <span data-ttu-id="4d9b8-152">在浏览器中运行*WebCache* 。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-152">Run *WebCache.cshtml* in a browser.</span></span> <span data-ttu-id="4d9b8-153">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）第一次请求页面时，时间数据不在缓存中，代码必须将时间值添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-153">(Make sure the page is selected in the **Files** workspace before you run it.) The first time you request the page, the time data isn't in the cache, and the code has to add the time value to the cache.</span></span>

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. <span data-ttu-id="4d9b8-155">在浏览器中刷新*WebCache* 。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-155">Refresh *WebCache.cshtml* in the browser.</span></span> <span data-ttu-id="4d9b8-156">这次，时间数据位于缓存中。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-156">This time, the time data is in the cache.</span></span> <span data-ttu-id="4d9b8-157">请注意，自上次查看页面后的时间未更改。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-157">Notice that the time hasn't changed since the last time you viewed the page.</span></span>

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. <span data-ttu-id="4d9b8-159">等待一分钟以便清空缓存，然后刷新页面。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-159">Wait one minute for the cache to be emptied, and then refresh the page.</span></span> <span data-ttu-id="4d9b8-160">该页再次指示在缓存中找不到时间数据，并将更新的时间添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="4d9b8-160">The page again indicates that the time data wasn't found in the cache, and the updated time is added to the cache.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="4d9b8-161">其他资源</span><span class="sxs-lookup"><span data-stu-id="4d9b8-161">Additional Resources</span></span>

- [<span data-ttu-id="4d9b8-162">在图表中显示数据</span><span class="sxs-lookup"><span data-stu-id="4d9b8-162">Displaying Data in a Chart</span></span>](https://go.microsoft.com/fwlink/?LinkId=202895)
- <span data-ttu-id="4d9b8-163">[WEBCACHE API 参考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="4d9b8-163">[WebCache API reference](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)</span></span>
