---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在 OData v4 中用 ASP.NET Web API 打开类型 |Microsoft Docs
author: microsoft
description: 在 OData v4 中，开放类型是一种结构化类型，其中包含动态属性以及在类型定义中声明的任何属性。 打开...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504578"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="a5425-104">在 OData v4 中用 ASP.NET Web API 打开类型</span><span class="sxs-lookup"><span data-stu-id="a5425-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="a5425-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a5425-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a5425-106">在 OData v4 中，*开放类型*是一种结构化类型，其中包含动态属性以及在类型定义中声明的任何属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="a5425-107">开放式类型使你可以为数据模型添加灵活性。</span><span class="sxs-lookup"><span data-stu-id="a5425-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="a5425-108">本教程演示如何使用 ASP.NET Web API OData 中的开放类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="a5425-109">本教程假定你已了解如何在 ASP.NET Web API 中创建 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="a5425-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="a5425-110">如果未启用，请首先阅读[创建 OData V4 终结点](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="a5425-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a5425-111">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a5425-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a5425-112">Web API OData 5。3</span><span class="sxs-lookup"><span data-stu-id="a5425-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="a5425-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="a5425-113">OData v4</span></span>

<span data-ttu-id="a5425-114">首先，一些 OData 术语：</span><span class="sxs-lookup"><span data-stu-id="a5425-114">First, some OData terminology:</span></span>

- <span data-ttu-id="a5425-115">实体类型：具有键的结构化类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="a5425-116">复杂类型：没有键的结构化类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="a5425-117">开放式类型：包含动态属性的类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="a5425-118">实体类型和复杂类型都可以打开。</span><span class="sxs-lookup"><span data-stu-id="a5425-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="a5425-119">动态属性的值可以是基元类型、复杂类型或枚举类型;或任何这些类型的集合。</span><span class="sxs-lookup"><span data-stu-id="a5425-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="a5425-120">有关开放类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。</span><span class="sxs-lookup"><span data-stu-id="a5425-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="a5425-121">安装 Web OData 库</span><span class="sxs-lookup"><span data-stu-id="a5425-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="a5425-122">使用 NuGet 包管理器安装最新的 Web API OData 库。</span><span class="sxs-lookup"><span data-stu-id="a5425-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="a5425-123">从 "包管理器控制台" 窗口：</span><span class="sxs-lookup"><span data-stu-id="a5425-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="a5425-124">定义 CLR 类型</span><span class="sxs-lookup"><span data-stu-id="a5425-124">Define the CLR Types</span></span>

<span data-ttu-id="a5425-125">首先，将 EDM 模型定义为 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="a5425-126">创建实体数据模型（EDM）时，</span><span class="sxs-lookup"><span data-stu-id="a5425-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="a5425-127">`Category` 为枚举类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="a5425-128">`Address` 是一种复杂类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-128">`Address` is a complex type.</span></span> <span data-ttu-id="a5425-129">（它没有密钥，因此它不是实体类型。）</span><span class="sxs-lookup"><span data-stu-id="a5425-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="a5425-130">`Customer` 是实体类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-130">`Customer` is an entity type.</span></span> <span data-ttu-id="a5425-131">（有一个键。）</span><span class="sxs-lookup"><span data-stu-id="a5425-131">(It has a key.)</span></span>
- <span data-ttu-id="a5425-132">`Press` 为开放式复杂类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="a5425-133">`Book` 是一种开放的实体类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="a5425-134">若要创建开放类型，CLR 类型必须有一个类型为 `IDictionary<string, object>`的属性，该属性包含动态属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="a5425-135">生成 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="a5425-135">Build the EDM Model</span></span>

<span data-ttu-id="a5425-136">如果使用**ODataConventionModelBuilder**创建 EDM，则基于是否存在 `IDictionary<string, object>` 属性，`Press` 和 `Book` 会自动添加为开放类型。</span><span class="sxs-lookup"><span data-stu-id="a5425-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="a5425-137">还可以使用**ODataModelBuilder**显式生成 EDM。</span><span class="sxs-lookup"><span data-stu-id="a5425-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="a5425-138">添加 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="a5425-138">Add an OData Controller</span></span>

<span data-ttu-id="a5425-139">接下来，添加 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="a5425-139">Next, add an OData controller.</span></span> <span data-ttu-id="a5425-140">对于本教程，我们将使用简单的控制器，该控制器仅支持 GET 和 POST 请求，并使用内存中列表存储实体。</span><span class="sxs-lookup"><span data-stu-id="a5425-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="a5425-141">请注意，第一个 `Book` 实例没有动态属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="a5425-142">第二个 `Book` 实例具有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="a5425-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="a5425-143">"已发布"：基元类型</span><span class="sxs-lookup"><span data-stu-id="a5425-143">"Published": Primitive type</span></span>
- <span data-ttu-id="a5425-144">"作者"：基元类型的集合</span><span class="sxs-lookup"><span data-stu-id="a5425-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="a5425-145">"OtherCategories"：枚举类型的集合。</span><span class="sxs-lookup"><span data-stu-id="a5425-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="a5425-146">此外，`Book` 实例的 `Press` 属性具有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="a5425-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="a5425-147">"博客"：基元类型</span><span class="sxs-lookup"><span data-stu-id="a5425-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="a5425-148">"Address"：复杂类型</span><span class="sxs-lookup"><span data-stu-id="a5425-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="a5425-149">查询元数据</span><span class="sxs-lookup"><span data-stu-id="a5425-149">Query the Metadata</span></span>

<span data-ttu-id="a5425-150">若要获取 OData 元数据文档，请将 GET 请求发送到 `~/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="a5425-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="a5425-151">响应正文应类似于：</span><span class="sxs-lookup"><span data-stu-id="a5425-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="a5425-152">在元数据文档中，可以看到：</span><span class="sxs-lookup"><span data-stu-id="a5425-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="a5425-153">对于 `Book` 和 `Press` 类型，`OpenType` 属性的值为 true。</span><span class="sxs-lookup"><span data-stu-id="a5425-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="a5425-154">`Customer` 和 `Address` 类型不具有此属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="a5425-155">`Book` 实体类型具有三个已声明的属性： ISBN、Title 和按压。</span><span class="sxs-lookup"><span data-stu-id="a5425-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="a5425-156">OData 元数据不包括 CLR 类中的 `Book.Properties` 属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="a5425-157">同样，`Press` 复杂类型仅包含两个已声明的属性：名称和类别。</span><span class="sxs-lookup"><span data-stu-id="a5425-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="a5425-158">元数据不包括 CLR 类中的 `Press.DynamicProperties` 属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="a5425-159">查询实体</span><span class="sxs-lookup"><span data-stu-id="a5425-159">Query an Entity</span></span>

<span data-ttu-id="a5425-160">若要获取 ISBN 等于 "978-0-7356-7942-9" 的书籍，请将 GET 请求发送到 `~/Books('978-0-7356-7942-9')`。</span><span class="sxs-lookup"><span data-stu-id="a5425-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="a5425-161">响应正文应类似于以下内容。</span><span class="sxs-lookup"><span data-stu-id="a5425-161">The response body should look similar to the following.</span></span> <span data-ttu-id="a5425-162">（缩进以使其更具可读性。）</span><span class="sxs-lookup"><span data-stu-id="a5425-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="a5425-163">请注意，动态属性与已声明的属性一起包含在一起。</span><span class="sxs-lookup"><span data-stu-id="a5425-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="a5425-164">发布实体</span><span class="sxs-lookup"><span data-stu-id="a5425-164">POST an Entity</span></span>

<span data-ttu-id="a5425-165">若要添加 Book 实体，请将 POST 请求发送到 `~/Books`。</span><span class="sxs-lookup"><span data-stu-id="a5425-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="a5425-166">客户端可以设置请求负载中的动态属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="a5425-167">下面是一个示例请求。</span><span class="sxs-lookup"><span data-stu-id="a5425-167">Here is an example request.</span></span> <span data-ttu-id="a5425-168">请注意 "价格" 和 "已发布" 属性。</span><span class="sxs-lookup"><span data-stu-id="a5425-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="a5425-169">如果在控制器方法中设置断点，可以看到 Web API 已将这些属性添加到 `Properties` 字典中。</span><span class="sxs-lookup"><span data-stu-id="a5425-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="a5425-170">其他资源</span><span class="sxs-lookup"><span data-stu-id="a5425-170">Additional Resources</span></span>

[<span data-ttu-id="a5425-171">OData 开放式类型示例</span><span class="sxs-lookup"><span data-stu-id="a5425-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
