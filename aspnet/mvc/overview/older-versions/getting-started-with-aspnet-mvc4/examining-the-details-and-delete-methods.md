---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: 检查详细信息和删除方法 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 37787a26f37473b9d36792a9f7715982cb274074
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485312"
---
# <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="b2821-104">检查 Details 和 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="b2821-104">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="b2821-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b2821-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="b2821-106">[此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="b2821-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="b2821-107">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="b2821-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="b2821-108">在本教程的此部分，您将检查自动生成的 `Details` 和 `Delete` 方法。</span><span class="sxs-lookup"><span data-stu-id="b2821-108">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="b2821-109">检查 Details 和 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="b2821-109">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="b2821-110">打开 `Movie` 控制器并检查 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="b2821-110">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="b2821-111">创建此操作方法的 MVC 基架引擎添加注释，该注释显示调用方法的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="b2821-111">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="b2821-112">在这种情况下，它是一个 `GET` 请求，其中包含三个 URL 段、`Movies` 控制器、`Details` 方法和 `ID` 值。</span><span class="sxs-lookup"><span data-stu-id="b2821-112">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="b2821-113">Code First 使用 `Find` 方法可以轻松地搜索数据。</span><span class="sxs-lookup"><span data-stu-id="b2821-113">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="b2821-114">内置于方法中的一个重要的安全功能是，代码验证 `Find` 方法在代码尝试使用影片之前是否找到了电影。</span><span class="sxs-lookup"><span data-stu-id="b2821-114">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="b2821-115">例如，黑客可以通过将 `http://localhost:xxxx/Movies/Details/1` 链接创建的 URL 更改为类似于 `http://localhost:xxxx/Movies/Details/12345` （或其他不表示实际电影的值），将错误引入到站点中。</span><span class="sxs-lookup"><span data-stu-id="b2821-115">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="b2821-116">如果未检查是否有空电影，空电影会导致数据库错误。</span><span class="sxs-lookup"><span data-stu-id="b2821-116">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="b2821-117">检查 `Delete` 和 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="b2821-117">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="b2821-118">请注意，`HTTP Get``Delete` 方法不会删除指定的电影，它会返回电影的视图，可在其中提交（`HttpPost`）删除操作。</span><span class="sxs-lookup"><span data-stu-id="b2821-118">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="b2821-119">执行删除操作以响应 GET 请求（或者说，执行编辑操作、创建操作或更改数据的任何其他操作）会打开安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="b2821-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="b2821-120">有关此操作的详细信息，请参阅 Stephen Walther 的博客文章[ASP.NET MVC Tip #46 —不要使用删除链接，因为它们创建了安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2821-120">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="b2821-121">删除数据的 `HttpPost` 方法命名为 `DeleteConfirmed`，以便为 HTTP POST 方法提供一个唯一的签名或名称。</span><span class="sxs-lookup"><span data-stu-id="b2821-121">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="b2821-122">下面显示了两个方法签名：</span><span class="sxs-lookup"><span data-stu-id="b2821-122">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="b2821-123">公共语言运行时 (CLR) 需要重载方法拥有唯一的参数签名（相同的方法名称但不同的参数列表）。</span><span class="sxs-lookup"><span data-stu-id="b2821-123">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="b2821-124">但在这里，你需要两个删除方法-一个用于 GET，一个用于 POST，这两个方法具有相同的参数签名。</span><span class="sxs-lookup"><span data-stu-id="b2821-124">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="b2821-125">（它们都需要接受单个整数作为参数。）</span><span class="sxs-lookup"><span data-stu-id="b2821-125">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="b2821-126">为此，可以执行几项操作。</span><span class="sxs-lookup"><span data-stu-id="b2821-126">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="b2821-127">一种方式是为方法指定不同的名称。</span><span class="sxs-lookup"><span data-stu-id="b2821-127">One is to give the methods different names.</span></span> <span data-ttu-id="b2821-128">这正是前面的示例中的基架机制进行的操作。</span><span class="sxs-lookup"><span data-stu-id="b2821-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="b2821-129">但是，这会造成一个小问题：ASP.NET 按名称将 URL 段映射到操作方法，如果重命名方法，则路由通常无法找到该方法。</span><span class="sxs-lookup"><span data-stu-id="b2821-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="b2821-130">该示例中也提供了解决方案，即向 `ActionName("Delete")` 方法添加 `DeleteConfirmed` 属性。</span><span class="sxs-lookup"><span data-stu-id="b2821-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="b2821-131">这将有效地为路由系统执行映射，以便包含 POST 请求的<em>/Delete/</em>的 URL 将查找 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="b2821-131">This effectively performs mapping for the routing system so that a URL that includes <em>/Delete/</em>for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="b2821-132">避免使用具有相同名称和签名的方法的问题的另一种常见方法是：人为更改 POST 方法的签名以包含未使用的参数。</span><span class="sxs-lookup"><span data-stu-id="b2821-132">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="b2821-133">例如，某些开发人员添加了一个传递给 POST 方法的参数类型 `FormCollection`，只是不使用参数：</span><span class="sxs-lookup"><span data-stu-id="b2821-133">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="b2821-134">摘要</span><span class="sxs-lookup"><span data-stu-id="b2821-134">Summary</span></span>

<span data-ttu-id="b2821-135">现在，你有了一个完整的 ASP.NET MVC 应用程序，它将数据存储在本地数据库中。</span><span class="sxs-lookup"><span data-stu-id="b2821-135">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="b2821-136">你可以创建、读取、更新、删除和搜索电影。</span><span class="sxs-lookup"><span data-stu-id="b2821-136">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="b2821-137">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b2821-137">Next Steps</span></span>

<span data-ttu-id="b2821-138">生成并测试 web 应用程序后，下一步就是使其可供其他人通过 Internet 使用。</span><span class="sxs-lookup"><span data-stu-id="b2821-138">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="b2821-139">为此，必须将其部署到 web 宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="b2821-139">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="b2821-140">Microsoft 在免费的 microsoft [Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中为多达10个网站提供免费的 web 托管。</span><span class="sxs-lookup"><span data-stu-id="b2821-140">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="b2821-141">我建议你接下来按照教程[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)网站。</span><span class="sxs-lookup"><span data-stu-id="b2821-141">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="b2821-142">好的教程是 Tom Dykstra 为[ASP.NET MVC 应用程序创建实体框架数据模型](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="b2821-142">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="b2821-143">[Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是提出问题的好地方。</span><span class="sxs-lookup"><span data-stu-id="b2821-143">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="b2821-144">请在 twitter 上关注[我](https://twitter.com/RickAndMSFT)，以便可以在我的最新教程中获取更新。</span><span class="sxs-lookup"><span data-stu-id="b2821-144">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="b2821-145">欢迎提供反馈。</span><span class="sxs-lookup"><span data-stu-id="b2821-145">Feedback is welcome.</span></span>

<span data-ttu-id="b2821-146">\- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b2821-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="b2821-147">\- [Scott Hanselman](http://www.hanselman.com/blog/) twitter： [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="b2821-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b2821-148">上一页</span><span class="sxs-lookup"><span data-stu-id="b2821-148">Previous</span></span>](adding-validation-to-the-model.md)
