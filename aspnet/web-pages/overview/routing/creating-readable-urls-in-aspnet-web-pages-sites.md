---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 在 ASP.NET 网页（Razor）站点中创建可读 Url |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）网站中进行路由，以及如何使用它来利用更具可读性且更适用于 SEO 的 Url。 你将 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509906"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="17a6f-104">在 ASP.NET 网页（Razor）站点中创建可读 Url</span><span class="sxs-lookup"><span data-stu-id="17a6f-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="17a6f-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="17a6f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="17a6f-106">本文介绍如何在 ASP.NET 网页（Razor）网站中进行路由，以及如何使用它来利用更具可读性且更适用于 SEO 的 Url。</span><span class="sxs-lookup"><span data-stu-id="17a6f-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="17a6f-107">学习内容：</span><span class="sxs-lookup"><span data-stu-id="17a6f-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="17a6f-108">ASP.NET 如何使用路由来使你可以使用可读性更强的可搜索 Url。</span><span class="sxs-lookup"><span data-stu-id="17a6f-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="17a6f-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="17a6f-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="17a6f-110">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="17a6f-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="17a6f-111">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="17a6f-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="17a6f-112">关于路由</span><span class="sxs-lookup"><span data-stu-id="17a6f-112">About Routing</span></span>

<span data-ttu-id="17a6f-113">站点中页面的 Url 可能会影响站点的工作方式。</span><span class="sxs-lookup"><span data-stu-id="17a6f-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="17a6f-114">&quot;友好&quot; 的 URL 可以使用户更轻松地使用站点。</span><span class="sxs-lookup"><span data-stu-id="17a6f-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="17a6f-115">它还可帮助网站的搜索引擎优化（SEO）。</span><span class="sxs-lookup"><span data-stu-id="17a6f-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="17a6f-116">ASP.NET 网站包括自动使用友好 Url 的功能。</span><span class="sxs-lookup"><span data-stu-id="17a6f-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="17a6f-117">使用 ASP.NET 可以创建有意义的 Url，用于描述用户操作，而不是仅指向服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="17a6f-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="17a6f-118">请考虑以下用于虚构博客的 Url：</span><span class="sxs-lookup"><span data-stu-id="17a6f-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="17a6f-119">将这些 Url 与以下 Url 进行比较：</span><span class="sxs-lookup"><span data-stu-id="17a6f-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="17a6f-120">在第一对中，用户必须知道该博客是使用 "*博客 ...* " 页显示的，然后必须构造一个获取正确类别或日期范围的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="17a6f-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="17a6f-121">第二组示例更易于理解和创建。</span><span class="sxs-lookup"><span data-stu-id="17a6f-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="17a6f-122">第一个示例的 Url 也直接指向特定文件（即*博客*）。</span><span class="sxs-lookup"><span data-stu-id="17a6f-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="17a6f-123">如果由于某种原因，博客被移到服务器上的另一个文件夹，或者重新编写博客以使用不同的页面，则链接会出错。</span><span class="sxs-lookup"><span data-stu-id="17a6f-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="17a6f-124">第二组 Url 未指向特定页面，因此即使在博客实现或位置发生更改时，Url 仍然有效。</span><span class="sxs-lookup"><span data-stu-id="17a6f-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="17a6f-125">在 ASP.NET 网页中，可以创建更友好的 Url，如上述示例中的 Url，因为 ASP.NET 使用*路由*。</span><span class="sxs-lookup"><span data-stu-id="17a6f-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="17a6f-126">路由创建从 URL 到可满足请求的页面的逻辑映射。</span><span class="sxs-lookup"><span data-stu-id="17a6f-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="17a6f-127">因为映射是逻辑的（而不是物理映射），所以路由为你定义站点的 Url 提供了极大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="17a6f-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="17a6f-128">路由的工作原理</span><span class="sxs-lookup"><span data-stu-id="17a6f-128">How Routing Works</span></span>

<span data-ttu-id="17a6f-129">当 ASP.NET 处理请求时，它会读取 URL 以确定如何路由该请求。</span><span class="sxs-lookup"><span data-stu-id="17a6f-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="17a6f-130">ASP.NET 尝试将 URL 的各个段与磁盘上的文件进行匹配，从左至右。</span><span class="sxs-lookup"><span data-stu-id="17a6f-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="17a6f-131">如果存在匹配项，则 URL 中剩余的任何内容将作为*路径信息*传递到页面。</span><span class="sxs-lookup"><span data-stu-id="17a6f-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="17a6f-132">假设有人使用此 URL 发出请求：</span><span class="sxs-lookup"><span data-stu-id="17a6f-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="17a6f-133">搜索如下所示：</span><span class="sxs-lookup"><span data-stu-id="17a6f-133">The search goes like this:</span></span>

1. <span data-ttu-id="17a6f-134">是否存在路径和名称为 */a/b/c.cshtml*的文件？</span><span class="sxs-lookup"><span data-stu-id="17a6f-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="17a6f-135">如果是这样，请运行该页并向其传递无信息。</span><span class="sxs-lookup"><span data-stu-id="17a6f-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="17a6f-136">否则...</span><span class="sxs-lookup"><span data-stu-id="17a6f-136">Otherwise ...</span></span>
2. <span data-ttu-id="17a6f-137">是否存在路径和名称为 */a/b.cshtml*的文件？</span><span class="sxs-lookup"><span data-stu-id="17a6f-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="17a6f-138">如果是这样，请运行该页并向其传递 `c` 值。</span><span class="sxs-lookup"><span data-stu-id="17a6f-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="17a6f-139">否则 。</span><span class="sxs-lookup"><span data-stu-id="17a6f-139">Otherwise …</span></span>
3. <span data-ttu-id="17a6f-140">是否存在路径和名称为 */a.cshtml*的文件？</span><span class="sxs-lookup"><span data-stu-id="17a6f-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="17a6f-141">如果是这样，请运行该页并向其传递 `b/c` 值。</span><span class="sxs-lookup"><span data-stu-id="17a6f-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="17a6f-142">如果搜索在其指定文件夹中找不到与 *.* # 文件完全匹配的项，ASP.NET 将继续依次查找这些文件：</span><span class="sxs-lookup"><span data-stu-id="17a6f-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="17a6f-143">*/a/b/c/default.cshtml* （无路径信息）。</span><span class="sxs-lookup"><span data-stu-id="17a6f-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="17a6f-144">*/a/b/c/index.cshtml* （无路径信息）。</span><span class="sxs-lookup"><span data-stu-id="17a6f-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="17a6f-145">为清楚起见，对特定页面的请求（即包含 *.* # 文件扩展名的请求）的工作方式与预期的一样。</span><span class="sxs-lookup"><span data-stu-id="17a6f-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="17a6f-146">例如 `http://www.contoso.com/a/b.cshtml` 的请求会正常运行第*b.* 页。</span><span class="sxs-lookup"><span data-stu-id="17a6f-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="17a6f-147">在页面中，可以通过页面的 `UrlData` 属性获取路径信息，该属性是一个词典。</span><span class="sxs-lookup"><span data-stu-id="17a6f-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="17a6f-148">假设你有一个名为*ViewCustomers*的文件，并且你的站点获取此请求：</span><span class="sxs-lookup"><span data-stu-id="17a6f-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="17a6f-149">如以上规则所述，请求将发送到你的页面。</span><span class="sxs-lookup"><span data-stu-id="17a6f-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="17a6f-150">在该页中，您可以使用如下所示的代码来获取和显示路径信息（在本例中，值 &quot;1000&quot;）：</span><span class="sxs-lookup"><span data-stu-id="17a6f-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="17a6f-151">由于路由不涉及完整的文件名，因此，如果页面的名称相同但文件扩展名不同（例如， *m y*和*m y*），则可能存在歧义。</span><span class="sxs-lookup"><span data-stu-id="17a6f-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="17a6f-152">为了避免出现路由问题，最好确保站点中的页面的名称仅在扩展名上不同。</span><span class="sxs-lookup"><span data-stu-id="17a6f-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="17a6f-153">其他资源</span><span class="sxs-lookup"><span data-stu-id="17a6f-153">Additional Resources</span></span>

<span data-ttu-id="17a6f-154">[WebMatrix-适用于 SEO 的 url、urldata.base 和路由](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。</span><span class="sxs-lookup"><span data-stu-id="17a6f-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="17a6f-155">Mike Brind 的此博客文章提供了有关路由在 ASP.NET 网页中的工作原理的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="17a6f-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
