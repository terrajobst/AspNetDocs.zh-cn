---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: 安全指南为 ASP.NET Web API 2 OData 的 ASP.NET 4.x
author: MikeWasson
description: 介绍在 ASP.NET 上的 ASP.NET Web API 2 公开通过 OData 数据集时要考虑的安全问题 4.x。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393504"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="e47b2-103">安全指南为 ASP.NET Web API 2 OData</span><span class="sxs-lookup"><span data-stu-id="e47b2-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="e47b2-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e47b2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="e47b2-105">本主题介绍了一些在 ASP.NET 上的 ASP.NET Web API 2 公开通过 OData 数据集时应考虑的安全问题 4.x。</span><span class="sxs-lookup"><span data-stu-id="e47b2-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="e47b2-106">EDM 安全</span><span class="sxs-lookup"><span data-stu-id="e47b2-106">EDM Security</span></span>

<span data-ttu-id="e47b2-107">查询语义均基于实体数据模型 (EDM) 中，不是基础的模型类型。</span><span class="sxs-lookup"><span data-stu-id="e47b2-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="e47b2-108">可以从 EDM 排除某属性，它将看不到查询。</span><span class="sxs-lookup"><span data-stu-id="e47b2-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="e47b2-109">例如，假设您的模型包含具有薪金属性的员工类型。</span><span class="sxs-lookup"><span data-stu-id="e47b2-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="e47b2-110">你可能想要从 EDM 来隐藏客户端从排除此属性。</span><span class="sxs-lookup"><span data-stu-id="e47b2-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="e47b2-111">有两种方法来从 EDM 排除某属性。</span><span class="sxs-lookup"><span data-stu-id="e47b2-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="e47b2-112">可以设置 **[IgnoreDataMember]** 模型类中的属性上的属性：</span><span class="sxs-lookup"><span data-stu-id="e47b2-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="e47b2-113">还可以删除该属性从 EDM 以编程方式：</span><span class="sxs-lookup"><span data-stu-id="e47b2-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="e47b2-114">查询安全性</span><span class="sxs-lookup"><span data-stu-id="e47b2-114">Query Security</span></span>

<span data-ttu-id="e47b2-115">恶意或简单客户端可以采用很长时间执行的查询。</span><span class="sxs-lookup"><span data-stu-id="e47b2-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="e47b2-116">在最坏情况下这可能会中断服务的访问权限。</span><span class="sxs-lookup"><span data-stu-id="e47b2-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="e47b2-117">**[Queryable]** 属性是操作筛选器，用于分析、 验证，并将查询应用。</span><span class="sxs-lookup"><span data-stu-id="e47b2-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="e47b2-118">筛选器将 LINQ 表达式转换为查询选项。</span><span class="sxs-lookup"><span data-stu-id="e47b2-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="e47b2-119">当返回 OData 控制器**IQueryable**类型， **IQueryable** LINQ 提供程序将查询转换为 LINQ 表达式。</span><span class="sxs-lookup"><span data-stu-id="e47b2-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="e47b2-120">因此，性能取决于使用时，LINQ 提供程序和数据集或数据库架构的特定的特征。</span><span class="sxs-lookup"><span data-stu-id="e47b2-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="e47b2-121">有关在 ASP.NET Web API 中使用 OData 查询选项的详细信息，请参阅[支持 OData 查询选项](supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="e47b2-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="e47b2-122">如果您知道所有客户端信任 （例如，在企业环境中），或者如果你的数据集很小，查询性能可能不会出现问题。</span><span class="sxs-lookup"><span data-stu-id="e47b2-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="e47b2-123">否则，应考虑以下建议。</span><span class="sxs-lookup"><span data-stu-id="e47b2-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="e47b2-124">测试你的服务的各种查询和分析数据库。</span><span class="sxs-lookup"><span data-stu-id="e47b2-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="e47b2-125">启用服务器驱动的分页，以避免在一个查询中返回大型数据集。</span><span class="sxs-lookup"><span data-stu-id="e47b2-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="e47b2-126">有关详细信息，请参阅[Server-Driven 分页](supporting-odata-query-options.md#server-paging)。</span><span class="sxs-lookup"><span data-stu-id="e47b2-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="e47b2-127">您是否需要 $filter 和 $orderby？</span><span class="sxs-lookup"><span data-stu-id="e47b2-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="e47b2-128">某些应用程序可能会允许客户端分页、 使用 $top 和 $skip，但禁用其他查询选项。</span><span class="sxs-lookup"><span data-stu-id="e47b2-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="e47b2-129">考虑将 $orderby 限制为聚集索引中的属性。</span><span class="sxs-lookup"><span data-stu-id="e47b2-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="e47b2-130">没有聚集索引的大型数据排序速度较慢。</span><span class="sxs-lookup"><span data-stu-id="e47b2-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="e47b2-131">最大节点计数：**MaxNodeCount**上的属性 **[Queryable]** 设置 $filter 语法树中允许的最大数字节点。</span><span class="sxs-lookup"><span data-stu-id="e47b2-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="e47b2-132">默认值为 100，但你可能想要设置较低的值，因为大量的节点可能会很慢进行编译。</span><span class="sxs-lookup"><span data-stu-id="e47b2-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="e47b2-133">这是如果您使用的 LINQ to Objects （即，在内存中，而不使用中间 LINQ 提供程序的集合上的 LINQ 查询） 尤其如此。</span><span class="sxs-lookup"><span data-stu-id="e47b2-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="e47b2-134">请考虑禁用 any （） 和 all （） 函数中，因为这些可能会很慢。</span><span class="sxs-lookup"><span data-stu-id="e47b2-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="e47b2-135">如果任何字符串属性包含的大型字符串&#8212;例如，产品说明或博客文章&#8212;，请考虑禁用的字符串函数。</span><span class="sxs-lookup"><span data-stu-id="e47b2-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="e47b2-136">请考虑不允许对导航属性筛选。</span><span class="sxs-lookup"><span data-stu-id="e47b2-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="e47b2-137">导航属性进行筛选，则可能导致在联接，它可能会很慢，具体取决于您的数据库架构。</span><span class="sxs-lookup"><span data-stu-id="e47b2-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="e47b2-138">下面的代码演示可防止对导航属性筛选的查询验证程序。</span><span class="sxs-lookup"><span data-stu-id="e47b2-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="e47b2-139">有关查询验证程序的详细信息，请参阅[查询验证](supporting-odata-query-options.md#query-validation)。</span><span class="sxs-lookup"><span data-stu-id="e47b2-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="e47b2-140">考虑将 $filter 查询限制通过编写针对您的数据库自定义验证程序。</span><span class="sxs-lookup"><span data-stu-id="e47b2-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="e47b2-141">例如，考虑这两个查询：</span><span class="sxs-lookup"><span data-stu-id="e47b2-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="e47b2-142">与执行组件的最后一个名称以 A 开头的所有电影。</span><span class="sxs-lookup"><span data-stu-id="e47b2-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="e47b2-143">1994 年发布的所有电影。</span><span class="sxs-lookup"><span data-stu-id="e47b2-143">All movies released in 1994.</span></span>

    <span data-ttu-id="e47b2-144">除非电影已编入索引的执行组件，第一个查询可能需要扫描整个列表的电影数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="e47b2-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="e47b2-145">第二个查询可能是可接受的而假定电影进行索引按版本年份。</span><span class="sxs-lookup"><span data-stu-id="e47b2-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="e47b2-146">下面的代码演示允许上的"ReleaseYear"和"Title"属性但没有其他属性进行筛选的验证程序。</span><span class="sxs-lookup"><span data-stu-id="e47b2-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="e47b2-147">一般情况下，请考虑需要哪些 $filter 函数。</span><span class="sxs-lookup"><span data-stu-id="e47b2-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="e47b2-148">如果你的客户端不需要的完整表现力 $filter，可以限制允许的函数。</span><span class="sxs-lookup"><span data-stu-id="e47b2-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
