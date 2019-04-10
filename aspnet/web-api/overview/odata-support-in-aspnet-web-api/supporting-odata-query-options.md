---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: 支持 OData 查询选项中 ASP.NET Web API 2 的 ASP.NET 4.x
author: MikeWasson
description: 概述与代码示例显示了支持 OData 查询选项中 ASP.NET Web API 2 ASP.NET 4.x。
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 428e4942e42436585049c1e84cd7b07a4a79c0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59411561"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="36324-103">ASP.NET Web API 2 中支持 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="36324-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="36324-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="36324-105">本概述的代码示例演示 ASP.NET Web API 2 中支持的 OData 查询选项的 ASP.NET 4.x。</span><span class="sxs-lookup"><span data-stu-id="36324-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="36324-106">OData 定义可用于修改的 OData 查询参数。</span><span class="sxs-lookup"><span data-stu-id="36324-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="36324-107">客户端的请求 URI 查询字符串中发送这些参数。</span><span class="sxs-lookup"><span data-stu-id="36324-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="36324-108">例如，若要对结果进行排序，客户端使用 $orderby 参数：</span><span class="sxs-lookup"><span data-stu-id="36324-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="36324-109">这些参数调用 OData 规范*查询选项*。</span><span class="sxs-lookup"><span data-stu-id="36324-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="36324-110">可以在项目中启用的任何 Web API 控制器的 OData 查询选项&#8212;控制器不需要是一个 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="36324-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="36324-111">这可以方便地添加功能，如筛选和排序到任何 Web API 应用程序。</span><span class="sxs-lookup"><span data-stu-id="36324-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="36324-112">启用查询选项，请阅读主题之前[OData 安全指南](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="36324-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="36324-113">启用 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="36324-114">示例查询</span><span class="sxs-lookup"><span data-stu-id="36324-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="36324-115">服务器驱动的分页</span><span class="sxs-lookup"><span data-stu-id="36324-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="36324-116">限制查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="36324-117">直接调用查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="36324-118">查询验证</span><span class="sxs-lookup"><span data-stu-id="36324-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="36324-119">启用 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-119">Enabling OData Query Options</span></span>

<span data-ttu-id="36324-120">Web API 支持以下 OData 查询选项：</span><span class="sxs-lookup"><span data-stu-id="36324-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="36324-121">选项</span><span class="sxs-lookup"><span data-stu-id="36324-121">Option</span></span> | <span data-ttu-id="36324-122">描述</span><span class="sxs-lookup"><span data-stu-id="36324-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36324-123">$expand</span><span class="sxs-lookup"><span data-stu-id="36324-123">$expand</span></span> | <span data-ttu-id="36324-124">展开相关的实体内联。</span><span class="sxs-lookup"><span data-stu-id="36324-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="36324-125">$filter</span><span class="sxs-lookup"><span data-stu-id="36324-125">$filter</span></span> | <span data-ttu-id="36324-126">筛选基于布尔条件的结果。</span><span class="sxs-lookup"><span data-stu-id="36324-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="36324-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="36324-127">$inlinecount</span></span> | <span data-ttu-id="36324-128">指示服务器在响应中包含匹配的实体的总数。</span><span class="sxs-lookup"><span data-stu-id="36324-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="36324-129">（适用于服务器端分页。）</span><span class="sxs-lookup"><span data-stu-id="36324-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="36324-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="36324-130">$orderby</span></span> | <span data-ttu-id="36324-131">对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="36324-131">Sorts the results.</span></span> |
| <span data-ttu-id="36324-132">$select</span><span class="sxs-lookup"><span data-stu-id="36324-132">$select</span></span> | <span data-ttu-id="36324-133">选择要在响应中包含的属性。</span><span class="sxs-lookup"><span data-stu-id="36324-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="36324-134">$skip</span><span class="sxs-lookup"><span data-stu-id="36324-134">$skip</span></span> | <span data-ttu-id="36324-135">将跳过前 n 个结果。</span><span class="sxs-lookup"><span data-stu-id="36324-135">Skips the first n results.</span></span> |
| <span data-ttu-id="36324-136">$top</span><span class="sxs-lookup"><span data-stu-id="36324-136">$top</span></span> | <span data-ttu-id="36324-137">返回仅前 n 个结果。</span><span class="sxs-lookup"><span data-stu-id="36324-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="36324-138">若要使用的 OData 查询选项，必须显式启用它们。</span><span class="sxs-lookup"><span data-stu-id="36324-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="36324-139">可以全局启用整个应用程序，或为特定控制器或特定操作启用它们。</span><span class="sxs-lookup"><span data-stu-id="36324-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="36324-140">若要全局启用 OData 查询选项，调用**EnableQuerySupport**上**HttpConfiguration**在启动时的类：</span><span class="sxs-lookup"><span data-stu-id="36324-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="36324-141">**EnableQuerySupport**方法，针对返回任何控制器操作的全局查询选项**IQueryable**类型。</span><span class="sxs-lookup"><span data-stu-id="36324-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="36324-142">如果不想为整个应用程序启用的查询选项，则可以启用它们的特定控制器操作通过添加 **[Queryable]** 属性为操作方法。</span><span class="sxs-lookup"><span data-stu-id="36324-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="36324-143">示例查询</span><span class="sxs-lookup"><span data-stu-id="36324-143">Example Queries</span></span>

<span data-ttu-id="36324-144">本部分介绍了可能使用 OData 查询选项的查询的类型。</span><span class="sxs-lookup"><span data-stu-id="36324-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="36324-145">查询选项的特定详细信息，请参阅上的 OData 文档[www.odata.org](http://www.odata.org/)。</span><span class="sxs-lookup"><span data-stu-id="36324-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="36324-146">有关 $展开和 $select，请参阅[使用 $select，$expand、 和 ASP.NET Web API OData 中的 $value](using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="36324-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

**<span data-ttu-id="36324-147">客户端驱动的分页</span><span class="sxs-lookup"><span data-stu-id="36324-147">Client-Driven Paging</span></span>**

<span data-ttu-id="36324-148">大型实体集的客户端可能会想要限制结果数。</span><span class="sxs-lookup"><span data-stu-id="36324-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="36324-149">例如，客户端可能会一次，其中包含用于获取下一页结果的"下一步"链接显示 10 个条目。</span><span class="sxs-lookup"><span data-stu-id="36324-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="36324-150">若要执行此操作，客户端使用的 $top 和 $skip 选项。</span><span class="sxs-lookup"><span data-stu-id="36324-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="36324-151">$Top 选项可提供的最大可返回的项目数和 $skip 选项可提供要跳过的项数。</span><span class="sxs-lookup"><span data-stu-id="36324-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="36324-152">前面的示例提取条目 21 到 30。</span><span class="sxs-lookup"><span data-stu-id="36324-152">The previous example fetches entries 21 through 30.</span></span>

**<span data-ttu-id="36324-153">筛选</span><span class="sxs-lookup"><span data-stu-id="36324-153">Filtering</span></span>**

<span data-ttu-id="36324-154">$Filter 选项允许客户端将通过应用布尔表达式筛选结果。</span><span class="sxs-lookup"><span data-stu-id="36324-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="36324-155">筛选器表达式是功能非常强大;它们包括逻辑运算符和算术运算符、 字符串函数和日期函数。</span><span class="sxs-lookup"><span data-stu-id="36324-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="36324-156">返回所有产品类别等于"Toys"。</span><span class="sxs-lookup"><span data-stu-id="36324-156">Return all products with category equal to "Toys".</span></span> | `http://localhost/Products?$filter=Category` <span data-ttu-id="36324-157">eq 'Toys</span><span class="sxs-lookup"><span data-stu-id="36324-157">eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="36324-158">返回价格小于 10 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="36324-158">Return all products with price less than 10.</span></span> | `http://localhost/Products?$filter=Price` <span data-ttu-id="36324-159">lt 10</span><span class="sxs-lookup"><span data-stu-id="36324-159">lt 10</span></span> |
| <span data-ttu-id="36324-160">逻辑运算符：返回的所有产品的价格 > = 5 且价格 < = 15。</span><span class="sxs-lookup"><span data-stu-id="36324-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | `http://localhost/Products?$filter=Price` <span data-ttu-id="36324-161">ge 5 和价格 le 15</span><span class="sxs-lookup"><span data-stu-id="36324-161">ge 5 and Price le 15</span></span> |
| <span data-ttu-id="36324-162">字符串函数：返回在名称中使用"zz"所有产品。</span><span class="sxs-lookup"><span data-stu-id="36324-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="36324-163">日期函数：2005 年之后返回与 ReleaseDate 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="36324-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | `http://localhost/Products?$filter=year(ReleaseDate)` <span data-ttu-id="36324-164">gt 2005</span><span class="sxs-lookup"><span data-stu-id="36324-164">gt 2005</span></span> |

**<span data-ttu-id="36324-165">排序</span><span class="sxs-lookup"><span data-stu-id="36324-165">Sorting</span></span>**

<span data-ttu-id="36324-166">若要对结果进行排序，请使用 $orderby 筛选器。</span><span class="sxs-lookup"><span data-stu-id="36324-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="36324-167">排序依据价格。</span><span class="sxs-lookup"><span data-stu-id="36324-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="36324-168">按降序排序 （最高到低） 的价格排序。</span><span class="sxs-lookup"><span data-stu-id="36324-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="36324-169">按类别进行排序，然后按降序排序类别中的价格进行排序。</span><span class="sxs-lookup"><span data-stu-id="36324-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="36324-170">服务器驱动的分页</span><span class="sxs-lookup"><span data-stu-id="36324-170">Server-Driven Paging</span></span>

<span data-ttu-id="36324-171">如果数据库包含数百万条记录，你不想将其发送一个有效负载中所有。</span><span class="sxs-lookup"><span data-stu-id="36324-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="36324-172">若要防止此情况，服务器可以限制单个响应中发送的条目数。</span><span class="sxs-lookup"><span data-stu-id="36324-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="36324-173">若要启用服务器分页，请设置**PageSize**属性中的**Queryable**属性。</span><span class="sxs-lookup"><span data-stu-id="36324-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="36324-174">值为要返回的最大项数。</span><span class="sxs-lookup"><span data-stu-id="36324-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="36324-175">如果你的控制器返回 OData 格式，响应正文将包含指向下一页数据的链接：</span><span class="sxs-lookup"><span data-stu-id="36324-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="36324-176">客户端可以使用此链接以提取下一个页面。</span><span class="sxs-lookup"><span data-stu-id="36324-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="36324-177">若要了解的结果集中的条目总数，客户端可以设置 $inlinecount 查询选项值与"allpages 进行请求"。</span><span class="sxs-lookup"><span data-stu-id="36324-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="36324-178">值"allpages 进行请求"指示服务器在响应中包含的总计数：</span><span class="sxs-lookup"><span data-stu-id="36324-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="36324-179">下一页的链接和内联计数都需要 OData 格式。</span><span class="sxs-lookup"><span data-stu-id="36324-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="36324-180">原因是 OData 定义特殊的字段来保存的链接和计数在响应正文中。</span><span class="sxs-lookup"><span data-stu-id="36324-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="36324-181">对于非 OData 格式，则仍可以支持通过包装中的查询结果的下一页链接和内联计数， **PageResult&lt;T&gt;** 对象。</span><span class="sxs-lookup"><span data-stu-id="36324-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="36324-182">但是，它需要更多代码。</span><span class="sxs-lookup"><span data-stu-id="36324-182">However, it requires a bit more code.</span></span> <span data-ttu-id="36324-183">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="36324-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="36324-184">下面是示例 JSON 响应：</span><span class="sxs-lookup"><span data-stu-id="36324-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="36324-185">限制查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-185">Limiting the Query Options</span></span>

<span data-ttu-id="36324-186">查询选项为客户端提供大量控制在服务器运行的查询。</span><span class="sxs-lookup"><span data-stu-id="36324-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="36324-187">在某些情况下，你可能想要限制可用于安全或性能方面的原因的选项。</span><span class="sxs-lookup"><span data-stu-id="36324-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="36324-188">**[Queryable]** 属性具有一些属性中为此生成的。</span><span class="sxs-lookup"><span data-stu-id="36324-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="36324-189">以下是一些示例。</span><span class="sxs-lookup"><span data-stu-id="36324-189">Here are some examples.</span></span>

<span data-ttu-id="36324-190">仅允许 $skip 和 $top，以支持分页和其他任何内容：</span><span class="sxs-lookup"><span data-stu-id="36324-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="36324-191">允许进行排序仅由一些特定属性，以防止对数据库中未编制索引的属性进行排序：</span><span class="sxs-lookup"><span data-stu-id="36324-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="36324-192">允许"eq"逻辑函数，但没有其他逻辑函数：</span><span class="sxs-lookup"><span data-stu-id="36324-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="36324-193">不允许任何算术运算符：</span><span class="sxs-lookup"><span data-stu-id="36324-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="36324-194">你可以通过构造全局限制选项**QueryableAttribute**实例，并将其传递给**EnableQuerySupport**函数：</span><span class="sxs-lookup"><span data-stu-id="36324-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="36324-195">直接调用查询选项</span><span class="sxs-lookup"><span data-stu-id="36324-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="36324-196">而不是使用 **[Queryable]** 属性，可以直接在您的控制器中调用的查询选项。</span><span class="sxs-lookup"><span data-stu-id="36324-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="36324-197">若要执行此操作，添加**ODataQueryOptions**控制器方法的参数。</span><span class="sxs-lookup"><span data-stu-id="36324-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="36324-198">在这种情况下，不需要 **[Queryable]** 属性。</span><span class="sxs-lookup"><span data-stu-id="36324-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="36324-199">Web API 填充**ODataQueryOptions**从 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="36324-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="36324-200">若要将查询的应用，请传递**IQueryable**到**ApplyTo**方法。</span><span class="sxs-lookup"><span data-stu-id="36324-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="36324-201">该方法将返回另一个**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="36324-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="36324-202">对于高级方案，如果还没有**IQueryable**查询提供程序，你可以检查**ODataQueryOptions**并转换到另一种形式的查询选项。</span><span class="sxs-lookup"><span data-stu-id="36324-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="36324-203">(有关示例，请参阅 RaghuRam Nadiminti 博客文章[翻译 OData 查询到 HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中还包括[示例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。)</span><span class="sxs-lookup"><span data-stu-id="36324-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="36324-204">查询验证</span><span class="sxs-lookup"><span data-stu-id="36324-204">Query Validation</span></span>

<span data-ttu-id="36324-205">**[Queryable]** 属性执行前验证查询。</span><span class="sxs-lookup"><span data-stu-id="36324-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="36324-206">在中执行此验证步骤**QueryableAttribute.ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="36324-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="36324-207">此外可以自定义验证过程。</span><span class="sxs-lookup"><span data-stu-id="36324-207">You can also customize the validation process.</span></span>

<span data-ttu-id="36324-208">另请参阅[OData 安全指南](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="36324-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="36324-209">首先，在中定义一个验证程序，它是类的替代**Web.Http.OData.Query.Validators**命名空间。</span><span class="sxs-lookup"><span data-stu-id="36324-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="36324-210">例如，下面的验证程序类禁用 $orderby 选项的 desc 选项。</span><span class="sxs-lookup"><span data-stu-id="36324-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="36324-211">子类 **[Queryable]** 属性来覆盖**ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="36324-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="36324-212">然后设置自定义属性或者全局或每个控制器：</span><span class="sxs-lookup"><span data-stu-id="36324-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="36324-213">如果使用的**ODataQueryOptions**直接，将验证程序设置的选项：</span><span class="sxs-lookup"><span data-stu-id="36324-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
