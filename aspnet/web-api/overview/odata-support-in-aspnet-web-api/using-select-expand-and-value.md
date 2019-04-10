---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: 使用 $select，$expand 和 $value 中 ASP.NET Web API 2 OData 的 ASP.NET 4.x
author: MikeWasson
description: 为 $ 的概述和代码示例展开，$select，和 $value 选项 OData Web API 2 中的 ASP.NET 4.x。
ms.author: riande
ms.date: 10/11/2013
ms.custom: seoapril2019
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: 8b5d3e87c679a31f1908aa648219ae5c6b701a1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400693"
---
# <a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="08ecd-103">使用 $select，$expand、 和 ASP.NET Web API 2 OData 中的 $value</span><span class="sxs-lookup"><span data-stu-id="08ecd-103">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="08ecd-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="08ecd-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="08ecd-105">为 $ 的概述和代码示例展开，$select，和 $value 选项 OData Web API 2 中的 ASP.NET 4.x。</span><span class="sxs-lookup"><span data-stu-id="08ecd-105">Overview and code samples for the $expand, $select, and $value options in OData Web API 2 for ASP.NET 4.x.</span></span> <span data-ttu-id="08ecd-106">这些选项允许客户端来控制该通道从服务器返回的表示形式。</span><span class="sxs-lookup"><span data-stu-id="08ecd-106">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="08ecd-107">**$expand**导致相关的实体是以内联形式包含在响应中的。</span><span class="sxs-lookup"><span data-stu-id="08ecd-107">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="08ecd-108">**$select**选择要在响应中包含的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="08ecd-108">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="08ecd-109">**$value**获取属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="08ecd-109">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="08ecd-110">示例架构</span><span class="sxs-lookup"><span data-stu-id="08ecd-110">Example Schema</span></span>

<span data-ttu-id="08ecd-111">对于本文中，我将使用 OData 服务，用于定义三个实体：产品、 供应商和类别。</span><span class="sxs-lookup"><span data-stu-id="08ecd-111">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="08ecd-112">每个产品都有一个类别和一个供应商。</span><span class="sxs-lookup"><span data-stu-id="08ecd-112">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="08ecd-113">下面是定义实体模型的 C# 类：</span><span class="sxs-lookup"><span data-stu-id="08ecd-113">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="08ecd-114">请注意，`Product`类定义的导航属性`Supplier`和`Category`。</span><span class="sxs-lookup"><span data-stu-id="08ecd-114">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="08ecd-115">`Category`类定义中每个类别的产品的导航属性。</span><span class="sxs-lookup"><span data-stu-id="08ecd-115">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="08ecd-116">若要创建此架构的 OData 终结点，请使用 Visual Studio 2013 的基架，如中所述[在 ASP.NET Web API 中创建 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="08ecd-116">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="08ecd-117">有关产品、 类别和供应商添加单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="08ecd-117">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="08ecd-118">启用 $展开和 $select</span><span class="sxs-lookup"><span data-stu-id="08ecd-118">Enabling $expand and $select</span></span>

<span data-ttu-id="08ecd-119">在 Visual Studio 2013 中，Web API OData 基架创建一个控制器，来自动支持 $expand 和 $select。</span><span class="sxs-lookup"><span data-stu-id="08ecd-119">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="08ecd-120">有关参考，下面是支持 $ 要求展开和 $select 控制器中的。</span><span class="sxs-lookup"><span data-stu-id="08ecd-120">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="08ecd-121">对于集合，该控制器`Get`方法必须返回**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="08ecd-121">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="08ecd-122">对于单个实体，返回**可取值为 SingleResult&lt;T&gt;**，其中 T 为**IQueryable** ，其中包含零个或一个实体。</span><span class="sxs-lookup"><span data-stu-id="08ecd-122">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="08ecd-123">此外，修饰您`Get`方法与 **[Queryable]** 属性，如前面的代码片段中所示。</span><span class="sxs-lookup"><span data-stu-id="08ecd-123">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="08ecd-124">或者，调用**EnableQuerySupport**上**HttpConfiguration**在启动时的对象。</span><span class="sxs-lookup"><span data-stu-id="08ecd-124">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="08ecd-125">(有关详细信息，请参阅[启用 OData 查询选项](supporting-odata-query-options.md#enable)。)</span><span class="sxs-lookup"><span data-stu-id="08ecd-125">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="08ecd-126">使用 $expand</span><span class="sxs-lookup"><span data-stu-id="08ecd-126">Using $expand</span></span>

<span data-ttu-id="08ecd-127">在查询的 OData 实体或集合时，默认响应不包括相关的实体。</span><span class="sxs-lookup"><span data-stu-id="08ecd-127">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="08ecd-128">例如，下面是类别实体集的默认响应：</span><span class="sxs-lookup"><span data-stu-id="08ecd-128">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="08ecd-129">正如您所看到的即使类别实体具有一个产品的导航链接响应不包括任何产品。</span><span class="sxs-lookup"><span data-stu-id="08ecd-129">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="08ecd-130">但是，客户端可以使用 $展开此项可获取每个类别的产品列表。</span><span class="sxs-lookup"><span data-stu-id="08ecd-130">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="08ecd-131">$Expand 选项中请求的查询字符串：</span><span class="sxs-lookup"><span data-stu-id="08ecd-131">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="08ecd-132">现在服务器将包括每个类别，各类别的内联的产品。</span><span class="sxs-lookup"><span data-stu-id="08ecd-132">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="08ecd-133">下面是响应负载：</span><span class="sxs-lookup"><span data-stu-id="08ecd-133">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="08ecd-134">请注意"value"数组中的每个项包含的产品列表。</span><span class="sxs-lookup"><span data-stu-id="08ecd-134">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="08ecd-135">$ Expand 选项采用以逗号分隔列表与要扩展的导航属性。</span><span class="sxs-lookup"><span data-stu-id="08ecd-135">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="08ecd-136">以下请求展开该类别和产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="08ecd-136">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="08ecd-137">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="08ecd-137">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="08ecd-138">您可以展开多个导航属性的级别。</span><span class="sxs-lookup"><span data-stu-id="08ecd-138">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="08ecd-139">下面的示例包括一个类别的所有产品以及每个产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="08ecd-139">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="08ecd-140">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="08ecd-140">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="08ecd-141">默认情况下，Web API 限制为 2 的最大展开深度。</span><span class="sxs-lookup"><span data-stu-id="08ecd-141">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="08ecd-142">防止发送等复杂请求客户端`$expand=Orders/OrderDetails/Product/Supplier/Region`，这可能很低效查询并创建大型的响应。</span><span class="sxs-lookup"><span data-stu-id="08ecd-142">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="08ecd-143">若要重写默认值，设置**MaxExpansionDepth**上的属性 **[Queryable]** 属性。</span><span class="sxs-lookup"><span data-stu-id="08ecd-143">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="08ecd-144">详细了解 $ expand 选项，请参阅[展开 ($expand) 系统查询选项](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand)官方 OData 文档中。</span><span class="sxs-lookup"><span data-stu-id="08ecd-144">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="08ecd-145">使用 $select</span><span class="sxs-lookup"><span data-stu-id="08ecd-145">Using $select</span></span>

<span data-ttu-id="08ecd-146">$Select 选项指定要在响应正文中包含的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="08ecd-146">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="08ecd-147">例如，若要获取的名称和每个产品的价格，请使用以下查询：</span><span class="sxs-lookup"><span data-stu-id="08ecd-147">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="08ecd-148">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="08ecd-148">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="08ecd-149">你可以组合 $select 和 $expand 中相同的查询。</span><span class="sxs-lookup"><span data-stu-id="08ecd-149">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="08ecd-150">请确保在 $select 选项中包含扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="08ecd-150">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="08ecd-151">例如，以下请求获取的产品名称和供应商。</span><span class="sxs-lookup"><span data-stu-id="08ecd-151">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="08ecd-152">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="08ecd-152">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="08ecd-153">此外可以选择一个扩展属性中的属性。</span><span class="sxs-lookup"><span data-stu-id="08ecd-153">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="08ecd-154">以下请求扩展产品，并选择类别名称和产品名称。</span><span class="sxs-lookup"><span data-stu-id="08ecd-154">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="08ecd-155">下面是响应正文：</span><span class="sxs-lookup"><span data-stu-id="08ecd-155">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="08ecd-156">有关 $select 选项的详细信息，请参阅[Select 系统查询选项 ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select)官方 OData 文档中。</span><span class="sxs-lookup"><span data-stu-id="08ecd-156">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="08ecd-157">获取单个实体 ($value) 的属性</span><span class="sxs-lookup"><span data-stu-id="08ecd-157">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="08ecd-158">有两种方法可从实体获取的个别属性的 OData 客户端。</span><span class="sxs-lookup"><span data-stu-id="08ecd-158">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="08ecd-159">客户端可以获取 OData 格式的值或获取属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="08ecd-159">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="08ecd-160">以下请求获取 OData 格式的属性。</span><span class="sxs-lookup"><span data-stu-id="08ecd-160">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="08ecd-161">此处是 JSON 格式的示例响应：</span><span class="sxs-lookup"><span data-stu-id="08ecd-161">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="08ecd-162">若要获取的属性的原始值，向 URI 追加 $value:</span><span class="sxs-lookup"><span data-stu-id="08ecd-162">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="08ecd-163">下面是响应。</span><span class="sxs-lookup"><span data-stu-id="08ecd-163">Here is the response.</span></span> <span data-ttu-id="08ecd-164">请注意，内容类型"text/plain"不是 JSON。</span><span class="sxs-lookup"><span data-stu-id="08ecd-164">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="08ecd-165">若要在 OData 控制器中支持这些查询，将添加一个名为方法`GetProperty`，其中`Property`是属性的名称。</span><span class="sxs-lookup"><span data-stu-id="08ecd-165">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="08ecd-166">例如，若要获取的 Name 属性的方法将被命名为`GetName`。</span><span class="sxs-lookup"><span data-stu-id="08ecd-166">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="08ecd-167">该方法应返回该属性的值：</span><span class="sxs-lookup"><span data-stu-id="08ecd-167">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
