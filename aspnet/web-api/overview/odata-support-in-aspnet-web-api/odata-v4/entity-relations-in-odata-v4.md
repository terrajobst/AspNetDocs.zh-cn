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
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>使用 ASP.NET Web API 2.2 的 OData v4 中的实体关系

作者： [Mike Wasson](https://github.com/MikeWasson)

> 大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。 使用 OData，客户端可在实体关系上导航。 在给定产品的情况下，您可以找到该供应商。 您还可以创建或删除关系。 例如，可以设置产品的供应商。
>
> 本教程演示如何使用 ASP.NET Web API 在 OData v4 中支持这些操作。 本教程基于[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)教程。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - Web API 2。1
> - OData v4
> - Visual Studio 2013 （[在此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下载 Visual Studio 2017）
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>教程版本
>
> 对于 OData 版本3，请参阅[支持 odata v3 中的实体关系](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)。

## <a name="add-a-supplier-entity"></a>添加供应商实体

> [!NOTE]
> 本教程基于[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)教程。

首先，我们需要一个相关实体。 将名为 `Supplier` 的类添加到模型文件夹中。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

将导航属性添加到 `Product` 类：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

将新的**DbSet**添加到 `ProductsContext` 类中，以便实体框架在数据库中包含供应商表。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

在 WebApiConfig.cs 中，将 &quot;供应商&quot; 实体集添加到实体数据模型：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>添加供应商控制器

将 `SuppliersController` 类添加到 "控制器" 文件夹。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

我不会说明如何为此控制器添加 CRUD 操作。 步骤与产品控制器相同（请参阅[创建 OData V4 终结点](create-an-odata-v4-endpoint.md)）。

## <a name="getting-related-entities"></a>获取相关实体

若要获取产品的供应商，客户端将发送 GET 请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

若要支持此请求，请将以下方法添加到 `ProductsController` 类：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

此方法使用默认命名约定

- 方法名称： GetX，其中 X 是导航属性。
- 参数名称：*键*

如果遵循此命名约定，Web API 会自动将 HTTP 请求映射到控制器方法。

示例 HTTP 请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

示例 HTTP 响应：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>获取相关集合

在上面的示例中，一个产品有一个供应商。 导航属性还可以返回集合。 以下代码获取供应商的产品：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

在这种情况下，该方法返回**IQueryable** ，而不是**SingleResult&lt;t&gt;**

示例 HTTP 请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

示例 HTTP 响应：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>创建实体之间的关系

OData 支持在两个现有实体之间创建或删除关系。 在 OData v4 术语中，关系是 &quot;引用&quot;。 （在 OData v3 中，关系称为*链接*。 此教程中的协议差别并不重要。）

引用具有自己的 URI，格式 `/Entity/NavigationProperty/$ref`。 例如，下面是用于对产品及其供应商之间的引用进行寻址的 URI：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

若要添加关系，客户端将向此地址发送 POST 或 PUT 请求。

- 如果导航属性是单个实体（如 `Product.Supplier`），则放置。
- 如果导航属性是一个集合，如 `Supplier.Products`，则为 POST。

请求正文包含关系中其他实体的 URI。 下面是一个示例请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

在此示例中，客户端向 `/Products(6)/Supplier/$ref`发送 PUT 请求，该请求是 ID = 6 的产品 `Supplier` 的 $ref URI。 如果请求成功，则服务器将发送204（无内容）响应：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

下面是用于将关系添加到 `Product`的控制器方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

*NavigationProperty*参数指定要设置的关系。 （如果实体上存在多个导航属性，则可以添加更多 `case` 语句。）

*Link*参数包含供应商的 URI。 Web API 会自动分析请求正文以获取此参数的值。

若要查找供应商，需要 ID （或密钥），这是*link*参数的一部分。 为此，请使用以下 helper 方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

基本上，此方法使用 OData 库将 URI 路径拆分为段，查找包含该键的段，并将该键转换为正确的类型。

## <a name="deleting-a-relationship-between-entities"></a>删除实体之间的关系

若要删除某个关系，客户端需要将 HTTP DELETE 请求发送到 $ref URI：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

下面是用于删除产品与供应商之间的关系的控制器方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

在这种情况下，`Product.Supplier` 是1对多关系的 &quot;1&quot; 结尾，因此，只需将 `Product.Supplier` 设置为 `null`即可删除该关系。

在 &quot;关系的很多&quot; 结束时，客户端必须指定要删除的相关实体。 为此，客户端将在请求的查询字符串中发送相关实体的 URI。 例如，若要从 "供应商 1" 中删除 "Product 1"：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

若要在 Web API 中支持此方法，我们需要在 `DeleteRef` 方法中包含一个额外的参数。 下面是用于从 `Supplier.Products` 关系中删除产品的控制器方法。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*Key*参数是供应商的密钥， *relatedKey*参数是要从 `Products` 关系中移除的产品的键。 请注意，Web API 会自动从查询字符串获取密钥。
