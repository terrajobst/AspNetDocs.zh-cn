---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 处理实体关系 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449120"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="c1b8e-102">处理实体关系</span><span class="sxs-lookup"><span data-stu-id="c1b8e-102">Handling Entity Relations</span></span>

<span data-ttu-id="c1b8e-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c1b8e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c1b8e-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="c1b8e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="c1b8e-105">本部分详细介绍了 EF 如何加载相关实体，以及如何处理模型类中的循环导航属性。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="c1b8e-106">（本部分提供了背景知识，并不是完成本教程所必需的。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="c1b8e-107">如果愿意，请跳到第[5 部分。](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="c1b8e-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="c1b8e-108">预先加载与延迟加载</span><span class="sxs-lookup"><span data-stu-id="c1b8e-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="c1b8e-109">将 EF 用于关系数据库时，请务必了解 EF 如何加载相关数据。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="c1b8e-110">这也有助于查看 EF 生成的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="c1b8e-111">若要跟踪 SQL，请将以下代码行添加到 `BookServiceContext` 构造函数：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="c1b8e-112">如果将 GET 请求发送到/api/books，它将返回如下所示的 JSON：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="c1b8e-113">您可以看到 Author 属性为 null，即使该书包含有效的作者。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="c1b8e-114">这是因为 EF 未加载相关的作者实体。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="c1b8e-115">SQL 查询的跟踪日志会确认这一点：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="c1b8e-116">SELECT 语句采用书籍表，而不引用作者表。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="c1b8e-117">下面是 `BooksController` 类中返回书籍列表的方法。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="c1b8e-118">我们来看看如何将作者返回为 JSON 数据的一部分。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="c1b8e-119">有三种方法可以在实体框架中加载相关数据：预先加载、延迟加载和显式加载。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="c1b8e-120">每种方法都有权衡，因此了解它们的工作原理很重要。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="c1b8e-121">预先加载</span><span class="sxs-lookup"><span data-stu-id="c1b8e-121">Eager Loading</span></span>

<span data-ttu-id="c1b8e-122">如果*预先加载*，则 EF 会将相关实体加载到初始数据库查询中。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="c1b8e-123">若要执行预先加载，请使用**system.web. Include**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="c1b8e-124">这会告知 EF 将作者数据包含在查询中。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="c1b8e-125">如果进行此更改并运行应用，则 JSON 数据现在如下所示：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="c1b8e-126">跟踪日志显示 EF 对书籍和作者表执行联接。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="c1b8e-127">延迟加载</span><span class="sxs-lookup"><span data-stu-id="c1b8e-127">Lazy Loading</span></span>

<span data-ttu-id="c1b8e-128">使用延迟加载时，当取消引用实体的导航属性时，EF 会自动加载相关实体。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="c1b8e-129">若要启用延迟加载，请将导航属性设置为虚拟。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="c1b8e-130">例如，在 Book 类中：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="c1b8e-131">现在，请考虑以下代码：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="c1b8e-132">启用延迟加载后，访问 `books[0]` 上的 `Author` 属性会导致 EF 为作者查询数据库。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="c1b8e-133">延迟加载需要多个数据库行程，因为在每次检索相关实体时 EF 都会发送一个查询。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="c1b8e-134">通常，您希望为您序列化的对象禁用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="c1b8e-135">序列化程序必须读取模型上的所有属性，这将触发加载相关实体。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="c1b8e-136">例如，当 EF 序列化启用了延迟加载的书籍列表时，以下是 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="c1b8e-137">你可以看到，EF 为三个作者进行了三次单独的查询。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="c1b8e-138">有时可能需要使用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="c1b8e-139">预先加载可能会导致 EF 生成非常复杂的联接。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="c1b8e-140">或者，可能需要一小部分数据的相关实体，延迟加载会更有效。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="c1b8e-141">避免序列化问题的一种方法是序列化数据传输对象（Dto）而不是实体对象。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="c1b8e-142">本文稍后会介绍此方法。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="c1b8e-143">显式加载</span><span class="sxs-lookup"><span data-stu-id="c1b8e-143">Explicit Loading</span></span>

<span data-ttu-id="c1b8e-144">显式加载类似于延迟加载，只不过您在代码中显式获取了相关数据，在访问导航属性时，不会自动发生此情况。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="c1b8e-145">显式加载使你可以更好地控制加载相关数据的时间，但需要额外的代码。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="c1b8e-146">有关显式加载的详细信息，请参阅[加载相关实体](https://msdn.microsoft.com/data/jj574232#explicit)。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="c1b8e-147">导航属性和循环引用</span><span class="sxs-lookup"><span data-stu-id="c1b8e-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="c1b8e-148">定义书籍和作者模型时，我在 "`Book`" 类上为 "书籍-作者" 关系定义了导航属性，但没有按其他方向定义导航属性。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="c1b8e-149">如果将相应的导航属性添加到 `Author` 类，会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="c1b8e-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="c1b8e-150">遗憾的是，这会导致在序列化模型时出现问题。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="c1b8e-151">如果加载相关数据，则会创建一个圆形对象图。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="c1b8e-152">当 JSON 或 XML 格式化程序尝试序列化关系图时，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="c1b8e-153">这两个格式化程序引发不同的异常消息。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="c1b8e-154">下面是 JSON 格式化程序的示例：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="c1b8e-155">下面是 XML 格式化程序：</span><span class="sxs-lookup"><span data-stu-id="c1b8e-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="c1b8e-156">一种解决方法是使用 Dto，我将在下一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="c1b8e-157">或者，你可以配置 JSON 和 XML 格式化程序来处理图形周期。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="c1b8e-158">有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="c1b8e-159">对于本教程，不需要 `Author.Book` 导航属性，因此可将其省略。</span><span class="sxs-lookup"><span data-stu-id="c1b8e-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c1b8e-160">[上一页](part-3.md)
> [下一页](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="c1b8e-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
