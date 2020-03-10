---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData 的安全指南-ASP.NET 4。x
author: MikeWasson
description: 描述在 ASP.NET 4.x 上通过 OData 公开 ASP.NET Web API 2 的数据集时要考虑的安全问题。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448292"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="94e0d-103">ASP.NET Web API 2 OData 的安全指南</span><span class="sxs-lookup"><span data-stu-id="94e0d-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="94e0d-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="94e0d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="94e0d-105">本主题介绍在 ASP.NET 4.x 上通过 OData 公开 ASP.NET Web API 2 的数据集时应考虑的一些安全问题。</span><span class="sxs-lookup"><span data-stu-id="94e0d-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="94e0d-106">EDM 安全性</span><span class="sxs-lookup"><span data-stu-id="94e0d-106">EDM Security</span></span>

<span data-ttu-id="94e0d-107">查询语义基于实体数据模型（EDM），而不是基础模型类型。</span><span class="sxs-lookup"><span data-stu-id="94e0d-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="94e0d-108">可以从 EDM 中排除属性，而不会对查询显示此属性。</span><span class="sxs-lookup"><span data-stu-id="94e0d-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="94e0d-109">例如，假设您的模型包含一个具有 Salary 属性的雇员类型。</span><span class="sxs-lookup"><span data-stu-id="94e0d-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="94e0d-110">你可能想要从 EDM 中排除此属性，以将其从客户端中隐藏。</span><span class="sxs-lookup"><span data-stu-id="94e0d-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="94e0d-111">可以通过两种方法从 EDM 中排除属性。</span><span class="sxs-lookup"><span data-stu-id="94e0d-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="94e0d-112">您可以在 model 类的属性中设置 **[IgnoreDataMember]** 属性：</span><span class="sxs-lookup"><span data-stu-id="94e0d-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="94e0d-113">还可以通过编程方式从 EDM 中删除属性：</span><span class="sxs-lookup"><span data-stu-id="94e0d-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="94e0d-114">查询安全性</span><span class="sxs-lookup"><span data-stu-id="94e0d-114">Query Security</span></span>

<span data-ttu-id="94e0d-115">恶意或简单的客户端可能会构建花费很长时间执行的查询。</span><span class="sxs-lookup"><span data-stu-id="94e0d-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="94e0d-116">在最坏的情况下，这可能会中断对服务的访问。</span><span class="sxs-lookup"><span data-stu-id="94e0d-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="94e0d-117">" **[可查询]** " 属性是一个操作筛选器，用于分析、验证和应用查询。</span><span class="sxs-lookup"><span data-stu-id="94e0d-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="94e0d-118">筛选器会将查询选项转换为 LINQ 表达式。</span><span class="sxs-lookup"><span data-stu-id="94e0d-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="94e0d-119">当 OData 控制器返回**IQueryable**类型时， **iqueryable** linq 提供程序会将 linq 表达式转换为查询。</span><span class="sxs-lookup"><span data-stu-id="94e0d-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="94e0d-120">因此，性能取决于所使用的 LINQ 提供程序，还取决于您的数据集或数据库架构的特定特性。</span><span class="sxs-lookup"><span data-stu-id="94e0d-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="94e0d-121">有关在 ASP.NET Web API 中使用 OData 查询选项的详细信息，请参阅[支持 Odata 查询选项](supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="94e0d-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="94e0d-122">如果你知道所有客户端均受信任（例如，在企业环境中），或者如果你的数据集很小，则查询性能可能不是问题。</span><span class="sxs-lookup"><span data-stu-id="94e0d-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="94e0d-123">否则，应考虑下列建议。</span><span class="sxs-lookup"><span data-stu-id="94e0d-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="94e0d-124">通过各种查询测试服务并分析数据库。</span><span class="sxs-lookup"><span data-stu-id="94e0d-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="94e0d-125">启用服务器驱动的分页，以避免在一个查询中返回大数据集。</span><span class="sxs-lookup"><span data-stu-id="94e0d-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="94e0d-126">有关详细信息，请参阅[服务器驱动的分页](supporting-odata-query-options.md#server-paging)。</span><span class="sxs-lookup"><span data-stu-id="94e0d-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="94e0d-127">是否需要 $filter 和 $orderby？</span><span class="sxs-lookup"><span data-stu-id="94e0d-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="94e0d-128">某些应用程序可能允许使用 $top 和 $skip 的客户端分页，但禁用其他查询选项。</span><span class="sxs-lookup"><span data-stu-id="94e0d-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="94e0d-129">请考虑将 $orderby 限制为聚集索引中的属性。</span><span class="sxs-lookup"><span data-stu-id="94e0d-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="94e0d-130">对不包含聚集索引的大型数据进行排序非常慢。</span><span class="sxs-lookup"><span data-stu-id="94e0d-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="94e0d-131">最大节点计数： **[可查询]** 上的**MaxNodeCount**属性设置 $filter 语法树中允许的最大节点数。</span><span class="sxs-lookup"><span data-stu-id="94e0d-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="94e0d-132">默认值为100，但你可能想要设置较低的值，因为大量的节点可能会很慢，无法编译。</span><span class="sxs-lookup"><span data-stu-id="94e0d-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="94e0d-133">如果使用 LINQ to Objects （即，在内存中的集合上使用 LINQ 查询，而不使用中间 LINQ 提供程序），则更是如此。</span><span class="sxs-lookup"><span data-stu-id="94e0d-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="94e0d-134">请考虑禁用 any （）和 all （）函数，因为这可能会很慢。</span><span class="sxs-lookup"><span data-stu-id="94e0d-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="94e0d-135">例如，如果任何字符串属性包含&#8212;大型字符串（例如，产品描述或博客条目&#8212;），请考虑禁用字符串函数。</span><span class="sxs-lookup"><span data-stu-id="94e0d-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="94e0d-136">请考虑禁止对导航属性进行筛选。</span><span class="sxs-lookup"><span data-stu-id="94e0d-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="94e0d-137">筛选导航属性可能会导致联接，这可能会很慢，具体取决于数据库架构。</span><span class="sxs-lookup"><span data-stu-id="94e0d-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="94e0d-138">下面的代码演示了阻止筛选导航属性的查询验证程序。</span><span class="sxs-lookup"><span data-stu-id="94e0d-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="94e0d-139">有关查询验证程序的详细信息，请参阅[查询验证](supporting-odata-query-options.md#query-validation)。</span><span class="sxs-lookup"><span data-stu-id="94e0d-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="94e0d-140">请考虑通过编写为数据库自定义的验证程序来限制 $filter 查询。</span><span class="sxs-lookup"><span data-stu-id="94e0d-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="94e0d-141">例如，考虑以下两个查询：</span><span class="sxs-lookup"><span data-stu-id="94e0d-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="94e0d-142">具有姓氏以 "A" 开头的参与者的所有电影。</span><span class="sxs-lookup"><span data-stu-id="94e0d-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="94e0d-143">1994中发布的所有电影。</span><span class="sxs-lookup"><span data-stu-id="94e0d-143">All movies released in 1994.</span></span>

    <span data-ttu-id="94e0d-144">如果使用者对电影进行索引，则第一次查询可能需要数据库引擎才能扫描整个电影列表。</span><span class="sxs-lookup"><span data-stu-id="94e0d-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="94e0d-145">但第二个查询可能是可接受的，假设电影按发行年份进行索引。</span><span class="sxs-lookup"><span data-stu-id="94e0d-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="94e0d-146">下面的代码演示一个验证程序，该验证程序允许筛选 "ReleaseYear" 和 "Title" 属性，但不允许使用其他属性。</span><span class="sxs-lookup"><span data-stu-id="94e0d-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="94e0d-147">一般情况下，请考虑所需的 $filter 函数。</span><span class="sxs-lookup"><span data-stu-id="94e0d-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="94e0d-148">如果客户端无需完全表现力的 $filter，则可以限制允许的函数。</span><span class="sxs-lookup"><span data-stu-id="94e0d-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
