---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效的数据分页 |Microsoft Docs
author: microsoft
description: 步骤8显示了如何将分页支持添加到我们的/Dinners URL，以便不会立即显示1000次就，而只会在 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486482"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="d065c-103">实现高效数据分页</span><span class="sxs-lookup"><span data-stu-id="d065c-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="d065c-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d065c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d065c-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="d065c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d065c-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第8步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d065c-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d065c-107">步骤8显示了如何将分页支持添加到/Dinners URL，以便一次只显示10个即将开始的就，并允许最终用户在 SEO 友好的方式下翻到整个列表。</span><span class="sxs-lookup"><span data-stu-id="d065c-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="d065c-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="d065c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="d065c-109">NerdDinner 步骤8：分页支持</span><span class="sxs-lookup"><span data-stu-id="d065c-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="d065c-110">如果我们的站点成功，会有数千个即将发布的就。</span><span class="sxs-lookup"><span data-stu-id="d065c-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="d065c-111">我们需要确保 UI 能缩放以处理所有这些就，并允许用户浏览它们。</span><span class="sxs-lookup"><span data-stu-id="d065c-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="d065c-112">为实现此目的，我们将向 */Dinners* URL 添加分页支持，以便一次只显示10个即将开始的就，并允许最终用户在 SEO 友好的方式下翻到整个列表。</span><span class="sxs-lookup"><span data-stu-id="d065c-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="d065c-113">Index （）操作方法概述</span><span class="sxs-lookup"><span data-stu-id="d065c-113">Index() Action Method Recap</span></span>

<span data-ttu-id="d065c-114">DinnersController 类中的 Index （）操作方法当前如下所示：</span><span class="sxs-lookup"><span data-stu-id="d065c-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="d065c-115">向 */Dinners* URL 发出请求时，它将检索所有即将发布的就的列表，并呈现所有即将发布的列表：</span><span class="sxs-lookup"><span data-stu-id="d065c-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="d065c-116">了解 IQueryable&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="d065c-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="d065c-117">*IQueryable&lt;t&gt;* 是在 .net 3.5 中作为 LINQ 引入的一个接口。</span><span class="sxs-lookup"><span data-stu-id="d065c-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="d065c-118">它实现了强大的 "延迟执行" 方案，我们可以利用它们来实现分页支持。</span><span class="sxs-lookup"><span data-stu-id="d065c-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="d065c-119">在我们的 DinnerRepository 中，我们将从 FindUpcomingDinners （）方法中返回一个 IQueryable&lt;晚宴&gt; 序列：</span><span class="sxs-lookup"><span data-stu-id="d065c-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="d065c-120">FindUpcomingDinners （）方法返回的 IQueryable&lt;晚宴&gt; 对象封装了一个查询，该查询使用 LINQ to SQL 从数据库中检索晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="d065c-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="d065c-121">重要的是，在尝试访问或循环访问查询中的数据之前，或在调用 System.linq.enumerable.tolist （）方法之前，不会对数据库执行查询。</span><span class="sxs-lookup"><span data-stu-id="d065c-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="d065c-122">调用我们的 FindUpcomingDinners （）方法的代码可以选择在执行查询之前将其他 "链接" 操作/筛选器添加到 IQueryable&lt;晚宴&gt; 对象。</span><span class="sxs-lookup"><span data-stu-id="d065c-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="d065c-123">然后 LINQ to SQL 就足以在请求数据时对数据库执行合并查询。</span><span class="sxs-lookup"><span data-stu-id="d065c-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="d065c-124">若要实现分页逻辑，我们可以更新 DinnersController 的 Index （）操作方法，以便在调用 System.linq.enumerable.tolist （）之前将其他 "Skip" 和 "Take" 运算符应用于返回的 IQueryable&lt;晚宴&gt; 序列：</span><span class="sxs-lookup"><span data-stu-id="d065c-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="d065c-125">上面的代码将跳过数据库中前10个即将发布的就，然后返回20就。</span><span class="sxs-lookup"><span data-stu-id="d065c-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="d065c-126">LINQ to SQL 非常智能，足以构造在 SQL 数据库（而不是 web-服务器）中执行此跳过逻辑的优化 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="d065c-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="d065c-127">这意味着，即使在数据库中有数百万个即将发布的就，此请求的一部分也只会检索到10个所需的10（使其高效且可缩放）。</span><span class="sxs-lookup"><span data-stu-id="d065c-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="d065c-128">向 URL 添加 "页面" 值</span><span class="sxs-lookup"><span data-stu-id="d065c-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="d065c-129">我们希望 Url 包含一个 "页面" 参数，该参数指示用户正在请求的晚餐范围，而不是对特定页面范围进行硬编码。</span><span class="sxs-lookup"><span data-stu-id="d065c-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="d065c-130">使用 Querystring 值</span><span class="sxs-lookup"><span data-stu-id="d065c-130">Using a Querystring value</span></span>

<span data-ttu-id="d065c-131">下面的代码演示了如何更新 Index （）操作方法以支持 querystring 参数并启用 Url，如 */Dinners？ page = 2*：</span><span class="sxs-lookup"><span data-stu-id="d065c-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="d065c-132">上面的 Index （）操作方法有一个名为 "page" 的参数。</span><span class="sxs-lookup"><span data-stu-id="d065c-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="d065c-133">参数声明为可以为 null 的整数（这是 int？指示的值）。</span><span class="sxs-lookup"><span data-stu-id="d065c-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="d065c-134">这意味着 */Dinners？ page = 2* URL 将导致值 "2" 作为参数值传递。</span><span class="sxs-lookup"><span data-stu-id="d065c-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="d065c-135">*/Dinners* URL （无 querystring 值）将导致传递 null 值。</span><span class="sxs-lookup"><span data-stu-id="d065c-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="d065c-136">我们将页面值乘以页面大小（在本例中为10行），以确定要跳过多少就。</span><span class="sxs-lookup"><span data-stu-id="d065c-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="d065c-137">在处理可以为 null 的类型时，我们使用的[ C#是 null "合并" 运算符（？？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="d065c-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="d065c-138">如果 page 参数为 null，上面的代码会将值赋给0。</span><span class="sxs-lookup"><span data-stu-id="d065c-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="d065c-139">使用嵌入的 URL 值</span><span class="sxs-lookup"><span data-stu-id="d065c-139">Using Embedded URL values</span></span>

<span data-ttu-id="d065c-140">使用查询字符串值的一种替代方法是在实际 URL 本身中嵌入页参数。</span><span class="sxs-lookup"><span data-stu-id="d065c-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="d065c-141">例如： */Dinners/Page/2*或 */Dinners/2*。</span><span class="sxs-lookup"><span data-stu-id="d065c-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="d065c-142">ASP.NET MVC 包含一个功能强大的 URL 路由引擎，可轻松支持此类方案。</span><span class="sxs-lookup"><span data-stu-id="d065c-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="d065c-143">我们可以注册将任何传入 URL 或 URL 格式映射到所需的任何控制器类或操作方法的自定义路由规则。</span><span class="sxs-lookup"><span data-stu-id="d065c-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="d065c-144">我们需要做的就是在项目中打开 global.asax 文件：</span><span class="sxs-lookup"><span data-stu-id="d065c-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="d065c-145">然后，使用 Maproute.html （） helper 方法（如对路由的第一次调用）注册新的映射规则。下面的 Maproute.html （）：</span><span class="sxs-lookup"><span data-stu-id="d065c-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="d065c-146">在此之前，我们将注册一个名为 "UpcomingDinners" 的新路由规则。</span><span class="sxs-lookup"><span data-stu-id="d065c-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="d065c-147">我们指示其 URL 格式为 "就/Page/{Page}" –其中 {Page} 是嵌入在 URL 中的参数值。</span><span class="sxs-lookup"><span data-stu-id="d065c-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="d065c-148">Maproute.html （）方法的第三个参数指示应将与此格式匹配的 Url 映射到 DinnersController 类的 Index （）操作方法。</span><span class="sxs-lookup"><span data-stu-id="d065c-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="d065c-149">我们可以使用我们之前与查询字符串方案相同的索引（）代码，但现在我们的 "page" 参数将来自 URL，而不是来自 querystring：</span><span class="sxs-lookup"><span data-stu-id="d065c-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="d065c-150">现在，当我们运行该应用程序并键入 */Dinners*时，我们将看到前10个即将发布的就：</span><span class="sxs-lookup"><span data-stu-id="d065c-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="d065c-151">当我们在 */Dinners/Page/1*中键入内容时，将看到下一页就：</span><span class="sxs-lookup"><span data-stu-id="d065c-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="d065c-152">添加页面导航 UI</span><span class="sxs-lookup"><span data-stu-id="d065c-152">Adding page navigation UI</span></span>

<span data-ttu-id="d065c-153">完成分页方案的最后一步是在视图模板中实现 "下一步" 和 "上一步" 导航用户界面，使用户能够轻松跳过晚餐数据。</span><span class="sxs-lookup"><span data-stu-id="d065c-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="d065c-154">若要正确实现此操作，我们需要知道数据库中就的总数，以及这要转换到的数据页的数目。</span><span class="sxs-lookup"><span data-stu-id="d065c-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="d065c-155">接下来，我们需要计算当前请求的 "page" 值是位于数据的开头还是结尾，并相应地显示或隐藏 "上一页" 和 "下一页" UI。</span><span class="sxs-lookup"><span data-stu-id="d065c-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="d065c-156">我们可以在索引（）操作方法中实现此逻辑。</span><span class="sxs-lookup"><span data-stu-id="d065c-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="d065c-157">此外，我们还可以向项目中添加一个帮助器类，以便以一种可重复使用的方式封装此逻辑。</span><span class="sxs-lookup"><span data-stu-id="d065c-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="d065c-158">下面是一个简单的 "PaginatedList" 帮助器类，它派生自内置 .NET Framework&gt; 集合类的列表&lt;。</span><span class="sxs-lookup"><span data-stu-id="d065c-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="d065c-159">它实现可重复使用的集合类，该类可用于对 IQueryable 数据的任意序列进行分页。</span><span class="sxs-lookup"><span data-stu-id="d065c-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="d065c-160">在我们的 NerdDinner 应用程序中，我们将使用 IQueryable&lt;晚宴&gt; 结果，但可以轻松地针对 IQueryable&lt;Product&gt; 或 IQueryable&lt;客户&gt; 会在其他应用程序方案中产生结果：</span><span class="sxs-lookup"><span data-stu-id="d065c-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="d065c-161">请注意上面它如何计算并显示 "PageIndex"、"PageSize"、"TotalCount" 和 "TotalPages" 等属性。</span><span class="sxs-lookup"><span data-stu-id="d065c-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="d065c-162">它还将公开两个帮助器属性 "HasPreviousPage" 和 "HasNextPage"，以指示集合中的数据页是位于原始序列的开头还是结尾。</span><span class="sxs-lookup"><span data-stu-id="d065c-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="d065c-163">上面的代码将导致运行两个 SQL 查询-第一个查询用于检索晚餐对象总数的计数（这不返回对象，而是执行返回整数的 "SELECT COUNT" 语句），第二个用于仅检索行我们的数据库中所需的数据用于当前数据页。</span><span class="sxs-lookup"><span data-stu-id="d065c-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="d065c-164">接下来，我们可以更新 DinnersController （）帮助程序方法，从我们的 DinnerRepository （）结果创建 PaginatedList&lt;晚宴&gt;，并将其传递给我们的视图模板：</span><span class="sxs-lookup"><span data-stu-id="d065c-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="d065c-165">然后，我们可以更新 \Views\Dinners\Index.aspx 视图模板，使其继承自 ViewPage&lt;NerdDinner。 PaginatedList&lt;晚餐&gt;&gt; 而不是 ViewPage&lt;IEnumerable&lt;晚餐&gt;&gt;，然后将以下代码添加到视图模板的底部：</span><span class="sxs-lookup"><span data-stu-id="d065c-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="d065c-166">请注意，我们如何使用 RouteLink （） helper 方法来生成超链接。</span><span class="sxs-lookup"><span data-stu-id="d065c-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="d065c-167">此方法类似于我们以前使用过的 Html.actionlink （） helper 方法。</span><span class="sxs-lookup"><span data-stu-id="d065c-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="d065c-168">不同之处在于，我们将使用我们在 global.asax 文件中设置的 "UpcomingDinners" 路由规则生成 URL。</span><span class="sxs-lookup"><span data-stu-id="d065c-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="d065c-169">这可以确保为索引（）操作方法生成 Url，格式为： */Dinners/Page/{page}* –其中，{Page} 值是我们基于当前 PageIndex 提供的变量。</span><span class="sxs-lookup"><span data-stu-id="d065c-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="d065c-170">现在，当我们再次运行应用程序时，我们将在浏览器中一次看到10个就：</span><span class="sxs-lookup"><span data-stu-id="d065c-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="d065c-171">此外，我们还提供了 &lt;&lt;&lt; 和 &gt;&gt;&gt; 导航 UI，可让我们使用搜索引擎可访问的 Url 在我们的数据上跳过和反向：</span><span class="sxs-lookup"><span data-stu-id="d065c-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="d065c-172">**侧主题：了解 IQueryable&lt;T&gt; 的含义**</span><span class="sxs-lookup"><span data-stu-id="d065c-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="d065c-173">IQueryable&lt;T&gt; 是一项功能强大的功能，可实现各种有趣的延迟执行方案（如分页和基于组合的查询）。</span><span class="sxs-lookup"><span data-stu-id="d065c-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="d065c-174">与所有强大的功能一样，你需要小心地使用它，并确保它不会被滥用。</span><span class="sxs-lookup"><span data-stu-id="d065c-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="d065c-175">务必认识到，从存储库返回 IQueryable&lt;T&gt; 结果，可以使调用代码向其追加链式运算符方法，并参与最终的查询执行。</span><span class="sxs-lookup"><span data-stu-id="d065c-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="d065c-176">如果你不希望为此功能提供调用代码，则应返回反向&lt;T&gt; 或 IEnumerable&lt;T&gt; 结果-其中包含已执行的查询的结果。</span><span class="sxs-lookup"><span data-stu-id="d065c-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="d065c-177">对于分页方案，这需要将实际的数据分页逻辑推送到被调用的存储库方法。</span><span class="sxs-lookup"><span data-stu-id="d065c-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="d065c-178">在此方案中，我们可能会将 FindUpcomingDinners （） finder 方法更新为具有返回 PaginatedList 的签名： PaginatedList&lt; 晚宴&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或返回 IList&lt;晚餐&gt;，并使用 "totalCount" out 参数返回就： IList&lt;晚餐&gt; FindUpcomingDinners （int pageIndex，int pageSize，out int totalCount） {}</span><span class="sxs-lookup"><span data-stu-id="d065c-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="d065c-179">下一步</span><span class="sxs-lookup"><span data-stu-id="d065c-179">Next Step</span></span>

<span data-ttu-id="d065c-180">现在我们来看看如何向应用程序添加身份验证和授权支持。</span><span class="sxs-lookup"><span data-stu-id="d065c-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d065c-181">[上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="d065c-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
