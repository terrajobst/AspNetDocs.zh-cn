---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的实体关系 |Microsoft Docs
author: MikeWasson
description: 大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。 使用 OData，客户端可以导航到 。
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484460"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="dee18-104">使用 ASP.NET Web API 2.2 的 OData v4 中的实体关系</span><span class="sxs-lookup"><span data-stu-id="dee18-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="dee18-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dee18-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="dee18-106">大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。</span><span class="sxs-lookup"><span data-stu-id="dee18-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="dee18-107">使用 OData，客户端可在实体关系上导航。</span><span class="sxs-lookup"><span data-stu-id="dee18-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="dee18-108">在给定产品的情况下，您可以找到该供应商。</span><span class="sxs-lookup"><span data-stu-id="dee18-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="dee18-109">您还可以创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="dee18-109">You can also create or remove relationships.</span></span> <span data-ttu-id="dee18-110">例如，可以设置产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="dee18-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="dee18-111">本教程演示如何使用 ASP.NET Web API 在 OData v4 中支持这些操作。</span><span class="sxs-lookup"><span data-stu-id="dee18-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="dee18-112">本教程基于[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)教程。</span><span class="sxs-lookup"><span data-stu-id="dee18-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dee18-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="dee18-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="dee18-114">Web API 2。1</span><span class="sxs-lookup"><span data-stu-id="dee18-114">Web API 2.1</span></span>
> - <span data-ttu-id="dee18-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="dee18-115">OData v4</span></span>
> - <span data-ttu-id="dee18-116">Visual Studio 2013 （[在此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下载 Visual Studio 2017）</span><span class="sxs-lookup"><span data-stu-id="dee18-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="dee18-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="dee18-117">Entity Framework 6</span></span>
> - <span data-ttu-id="dee18-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="dee18-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="dee18-119">教程版本</span><span class="sxs-lookup"><span data-stu-id="dee18-119">Tutorial versions</span></span>
>
> <span data-ttu-id="dee18-120">对于 OData 版本3，请参阅[支持 odata v3 中的实体关系](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)。</span><span class="sxs-lookup"><span data-stu-id="dee18-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="dee18-121">添加供应商实体</span><span class="sxs-lookup"><span data-stu-id="dee18-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="dee18-122">本教程基于[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)教程。</span><span class="sxs-lookup"><span data-stu-id="dee18-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="dee18-123">首先，我们需要一个相关实体。</span><span class="sxs-lookup"><span data-stu-id="dee18-123">First, we need a related entity.</span></span> <span data-ttu-id="dee18-124">将名为 `Supplier` 的类添加到模型文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dee18-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="dee18-125">将导航属性添加到 `Product` 类：</span><span class="sxs-lookup"><span data-stu-id="dee18-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="dee18-126">将新的**DbSet**添加到 `ProductsContext` 类中，以便实体框架在数据库中包含供应商表。</span><span class="sxs-lookup"><span data-stu-id="dee18-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="dee18-127">在 WebApiConfig.cs 中，将 &quot;供应商&quot; 实体集添加到实体数据模型：</span><span class="sxs-lookup"><span data-stu-id="dee18-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="dee18-128">添加供应商控制器</span><span class="sxs-lookup"><span data-stu-id="dee18-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="dee18-129">将 `SuppliersController` 类添加到 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="dee18-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="dee18-130">我不会说明如何为此控制器添加 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="dee18-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="dee18-131">步骤与产品控制器相同（请参阅[创建 OData V4 终结点](create-an-odata-v4-endpoint.md)）。</span><span class="sxs-lookup"><span data-stu-id="dee18-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="dee18-132">获取相关实体</span><span class="sxs-lookup"><span data-stu-id="dee18-132">Getting Related Entities</span></span>

<span data-ttu-id="dee18-133">若要获取产品的供应商，客户端将发送 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="dee18-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="dee18-134">若要支持此请求，请将以下方法添加到 `ProductsController` 类：</span><span class="sxs-lookup"><span data-stu-id="dee18-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="dee18-135">此方法使用默认命名约定</span><span class="sxs-lookup"><span data-stu-id="dee18-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="dee18-136">方法名称： GetX，其中 X 是导航属性。</span><span class="sxs-lookup"><span data-stu-id="dee18-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="dee18-137">参数名称：*键*</span><span class="sxs-lookup"><span data-stu-id="dee18-137">Parameter name: *key*</span></span>

<span data-ttu-id="dee18-138">如果遵循此命名约定，Web API 会自动将 HTTP 请求映射到控制器方法。</span><span class="sxs-lookup"><span data-stu-id="dee18-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="dee18-139">示例 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="dee18-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="dee18-140">示例 HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="dee18-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="dee18-141">获取相关集合</span><span class="sxs-lookup"><span data-stu-id="dee18-141">Getting a related collection</span></span>

<span data-ttu-id="dee18-142">在上面的示例中，一个产品有一个供应商。</span><span class="sxs-lookup"><span data-stu-id="dee18-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="dee18-143">导航属性还可以返回集合。</span><span class="sxs-lookup"><span data-stu-id="dee18-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="dee18-144">以下代码获取供应商的产品：</span><span class="sxs-lookup"><span data-stu-id="dee18-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="dee18-145">在这种情况下，该方法返回**IQueryable** ，而不是**SingleResult&lt;t&gt;**</span><span class="sxs-lookup"><span data-stu-id="dee18-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="dee18-146">示例 HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="dee18-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="dee18-147">示例 HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="dee18-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="dee18-148">创建实体之间的关系</span><span class="sxs-lookup"><span data-stu-id="dee18-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="dee18-149">OData 支持在两个现有实体之间创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="dee18-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="dee18-150">在 OData v4 术语中，关系是 &quot;引用&quot;。</span><span class="sxs-lookup"><span data-stu-id="dee18-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="dee18-151">（在 OData v3 中，关系称为*链接*。</span><span class="sxs-lookup"><span data-stu-id="dee18-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="dee18-152">此教程中的协议差别并不重要。）</span><span class="sxs-lookup"><span data-stu-id="dee18-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="dee18-153">引用具有自己的 URI，格式 `/Entity/NavigationProperty/$ref`。</span><span class="sxs-lookup"><span data-stu-id="dee18-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="dee18-154">例如，下面是用于对产品及其供应商之间的引用进行寻址的 URI：</span><span class="sxs-lookup"><span data-stu-id="dee18-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="dee18-155">若要添加关系，客户端将向此地址发送 POST 或 PUT 请求。</span><span class="sxs-lookup"><span data-stu-id="dee18-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="dee18-156">如果导航属性是单个实体（如 `Product.Supplier`），则放置。</span><span class="sxs-lookup"><span data-stu-id="dee18-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="dee18-157">如果导航属性是一个集合，如 `Supplier.Products`，则为 POST。</span><span class="sxs-lookup"><span data-stu-id="dee18-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="dee18-158">请求正文包含关系中其他实体的 URI。</span><span class="sxs-lookup"><span data-stu-id="dee18-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="dee18-159">下面是一个示例请求：</span><span class="sxs-lookup"><span data-stu-id="dee18-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="dee18-160">在此示例中，客户端向 `/Products(6)/Supplier/$ref`发送 PUT 请求，该请求是 ID = 6 的产品 `Supplier` 的 $ref URI。</span><span class="sxs-lookup"><span data-stu-id="dee18-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="dee18-161">如果请求成功，则服务器将发送204（无内容）响应：</span><span class="sxs-lookup"><span data-stu-id="dee18-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="dee18-162">下面是用于将关系添加到 `Product`的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="dee18-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="dee18-163">*NavigationProperty*参数指定要设置的关系。</span><span class="sxs-lookup"><span data-stu-id="dee18-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="dee18-164">（如果实体上存在多个导航属性，则可以添加更多 `case` 语句。）</span><span class="sxs-lookup"><span data-stu-id="dee18-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="dee18-165">*Link*参数包含供应商的 URI。</span><span class="sxs-lookup"><span data-stu-id="dee18-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="dee18-166">Web API 会自动分析请求正文以获取此参数的值。</span><span class="sxs-lookup"><span data-stu-id="dee18-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="dee18-167">若要查找供应商，需要 ID （或密钥），这是*link*参数的一部分。</span><span class="sxs-lookup"><span data-stu-id="dee18-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="dee18-168">为此，请使用以下 helper 方法：</span><span class="sxs-lookup"><span data-stu-id="dee18-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="dee18-169">基本上，此方法使用 OData 库将 URI 路径拆分为段，查找包含该键的段，并将该键转换为正确的类型。</span><span class="sxs-lookup"><span data-stu-id="dee18-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="dee18-170">删除实体之间的关系</span><span class="sxs-lookup"><span data-stu-id="dee18-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="dee18-171">若要删除某个关系，客户端需要将 HTTP DELETE 请求发送到 $ref URI：</span><span class="sxs-lookup"><span data-stu-id="dee18-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="dee18-172">下面是用于删除产品与供应商之间的关系的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="dee18-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="dee18-173">在这种情况下，`Product.Supplier` 是1对多关系的 &quot;1&quot; 结尾，因此，只需将 `Product.Supplier` 设置为 `null`即可删除该关系。</span><span class="sxs-lookup"><span data-stu-id="dee18-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="dee18-174">在 &quot;关系的很多&quot; 结束时，客户端必须指定要删除的相关实体。</span><span class="sxs-lookup"><span data-stu-id="dee18-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="dee18-175">为此，客户端将在请求的查询字符串中发送相关实体的 URI。</span><span class="sxs-lookup"><span data-stu-id="dee18-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="dee18-176">例如，若要从 "供应商 1" 中删除 "Product 1"：</span><span class="sxs-lookup"><span data-stu-id="dee18-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="dee18-177">若要在 Web API 中支持此方法，我们需要在 `DeleteRef` 方法中包含一个额外的参数。</span><span class="sxs-lookup"><span data-stu-id="dee18-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="dee18-178">下面是用于从 `Supplier.Products` 关系中删除产品的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="dee18-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="dee18-179">*Key*参数是供应商的密钥， *relatedKey*参数是要从 `Products` 关系中移除的产品的键。</span><span class="sxs-lookup"><span data-stu-id="dee18-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="dee18-180">请注意，Web API 会自动从查询字符串获取密钥。</span><span class="sxs-lookup"><span data-stu-id="dee18-180">Note that Web API automatically gets the key from the query string.</span></span>
