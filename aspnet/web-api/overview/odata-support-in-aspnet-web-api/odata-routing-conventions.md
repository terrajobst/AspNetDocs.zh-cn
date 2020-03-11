---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 Odata 中的路由约定-ASP.NET 4。x
author: MikeWasson
description: 介绍 ASP.NET 4.x 中的 Web API 2 用于 OData 终结点的路由约定。
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498194"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 Odata 中的路由约定

作者： [Mike Wasson](https://github.com/MikeWasson)

> 本文介绍 ASP.NET 4.x 中的 Web API 2 用于 OData 终结点的路由约定。

当 Web API 获取 OData 请求时，它会将请求映射到控制器名称和操作名称。 该映射基于 HTTP 方法和 URI。 例如，`GET /odata/Products(1)` 映射到 `ProductsController.GetProduct`。

本文的第1部分介绍了内置的 OData 路由约定。 这些约定专用于 OData 终结点，并替换默认的 Web API 路由系统。 （当调用**MapODataRoute**时，将发生替换。）

在第2部分中，我将介绍如何添加自定义路由约定。 目前，内置约定不涵盖整个范围的 OData Uri，但可以对其进行扩展以应对其他情况。

- [内置路由约定](#conventions)
- [自定义路由约定](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>内置路由约定

在描述 Web API 中的 OData 路由约定之前，了解 OData Uri 非常有用。 [ODATA URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)包含：

- 服务根
- 资源路径
- 查询选项

![](odata-routing-conventions/_static/image1.png)

对于路由，重要的部分是资源路径。 资源路径划分为多个段。 例如，`/Products(1)/Supplier` 有三个段：

- `Products` 引用名为 "Products" 的实体集。
- `1` 是实体键，则从集中选择单个实体。
- `Supplier` 是用于选择相关实体的导航属性。

因此，此路径将选取产品1的供应商。

> [!NOTE]
> OData 路径段并不总是对应于 URI 段。 例如，"1" 被视为路径段。

**控制器名称。** 控制器名称始终从资源路径根的实体集派生。 例如，如果 `/Products(1)/Supplier`资源路径，Web API 将查找名为 `ProductsController`的控制器。

**操作名称。** 操作名称派生自路径段和实体数据模型（EDM），如下表所示。 在某些情况下，操作名称有两种选择。 例如，"Get" 或 &quot;GetProducts&quot;。

**查询实体**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| 获取/entityset | /Products | GetEntitySet 或 Get | GetProducts |
| 获取/entityset （key） | /Products(1) | GetEntityType 或 Get | GetProduct |
| 获取/entityset （key）/cast | /Products(1)/Models.Book | GetEntityType 或 Get | GetBook |

有关详细信息，请参阅[创建只读 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。

**创建、更新和删除实体**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| POST/entityset | /Products | PostEntityType 或 Post | PostProduct |
| PUT/entityset （key） | /Products(1) | PutEntityType 或 Put | PutProduct |
| PUT/entityset （key）/cast | /Products(1)/Models.Book | PutEntityType 或 Put | PutBook |
| PATCH/entityset （key） | /Products(1) | PatchEntityType 或修补程序 | PatchProduct |
| PATCH/entityset （key）/cast | /Products(1)/Models.Book | PatchEntityType 或修补程序 | PatchBook |
| 删除/entityset （key） | /Products(1) | DeleteEntityType 或 Delete | DeleteProduct |
| 删除/entityset （key）/cast | /Products(1)/Models.Book | DeleteEntityType 或 Delete | DeleteBook |

**查询导航属性**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| 获取/entityset （key）/navigation | /Products （1）/Supplier | GetNavigationFromEntityType 或 GetNavigation | GetSupplierFromProduct |
| 获取/entityset （key）/cast/navigation | /Products(1)/Models.Book/Author | GetNavigationFromEntityType 或 GetNavigation | GetAuthorFromBook |

有关详细信息，请参阅使用[实体关系](odata-v3/working-with-entity-relations.md)。

**创建和删除链接**

| 请求 | 示例 URI | 操作名称 |
| --- | --- | --- |
| POST/entityset （key）/$links/navigation | /Products （1）/$links/Supplier | CreateLink |
| PUT/entityset （key）/$links/navigation | /Products （1）/$links/Supplier | CreateLink |
| 删除/entityset （key）/$links/navigation | /Products （1）/$links/Supplier | DeleteLink |
| 删除/entityset （key）/$links/navigation （relatedKey） | /Products/(1)/$links/Suppliers(1) | DeleteLink |

有关详细信息，请参阅使用[实体关系](odata-v3/working-with-entity-relations.md)。

**属性**

*需要 Web API 2*

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| 获取/entityset （key）/property | /Products(1)/Name | GetPropertyFromEntityType 或 GetProperty | GetNameFromProduct |
| 获取/entityset （key）/cast/property | /Products(1)/Models.Book/Author | GetPropertyFromEntityType 或 GetProperty | GetTitleFromBook |

**操作**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| POST/entityset （key）/action | /Products （1）/Rate | ActionNameOnEntityType 或 ActionName | RateOnProduct |
| POST/entityset （key）/cast/action | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType 或 ActionName | CheckOutOnBook |

有关详细信息，请参阅[OData 操作](odata-v3/odata-actions.md)。

**方法签名**

下面是方法签名的一些规则：

- 如果路径包含一个键，则该操作应该具有一个名为*key*的参数。
- 如果路径包含导航属性中的键，则该操作应该具有一个名为*relatedKey*的参数。
- 用 **[FromODataUri]** 参数装饰*key*和*relatedKey*参数。
- POST 和 PUT 请求采用实体类型的参数。
- PATCH 请求采用类型为**Delta&lt;t&gt;** 的参数，其中*t*是实体类型。

下面是一个示例，演示了每个内置 OData 路由约定的方法签名。

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>自定义路由约定

目前，内置约定不涵盖所有可能的 OData Uri。 可以通过实现**IODataRoutingConvention**接口添加新约定。 此接口有两种方法：

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController**返回控制器的名称。
- **SelectAction**返回操作的名称。

对于这两种方法，如果约定不适用于该请求，则该方法应返回 null。

**ODataPath**参数表示已分析的 OData 资源路径。 它包含一个 **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 实例列表，每个实例对应于资源路径的每个段。 **ODataPathSegment**是一个抽象类;每个段类型由从**ODataPathSegment**派生的类表示。

**ODataPath. TemplatePath**属性是一个字符串，表示串联所有路径段。 例如，如果 URI 是 `/Products(1)/Supplier`的，则路径模板 &quot;~/entityset/key/navigation&quot;。 请注意，段不会直接对应于 URI 段。 例如，实体键（1）表示为其自己的**ODataPathSegment**。

通常， **IODataRoutingConvention**的实现会执行以下操作：

1. 比较路径模板以查看此约定是否适用于当前请求。 如果不适用，则返回 null。
2. 如果约定适用，请使用**ODataPathSegment**实例的属性派生控制器和操作名称。
3. 对于操作，请将任何值添加到应绑定到操作参数的路由字典（通常为实体键）。

让我们看一个具体的示例。 内置路由约定不支持对导航集合进行索引。 换句话说，Uri 没有约定，如下所示：

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

下面是用于处理此类查询的自定义路由约定。

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

注意：

1. 我从**EntitySetRoutingConvention**派生，因为该类中的**SelectController**方法适用于这一新的路由约定。 这意味着我不需要重新实现**SelectController**。
2. 该约定仅适用于 GET 请求，且仅在路径模板 &quot;~/entityset/key/navigation/key&quot;时才适用。
3. 操作名称为 &quot;Get {EntityType}&quot;，其中 *{entitytype}* 是导航集合的类型。 例如，&quot;GetSupplier&quot;。 你可以使用任何所需的命名约定&#8212; ，只需确保控制器操作匹配。
4. 操作采用名为*key*和*relatedKey*的两个参数。 （有关一些预定义参数名称的列表，请参阅[ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)。）

下一步是将新约定添加到路由约定列表。 在配置过程中将发生这种情况，如下面的代码所示：

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

下面是一些可用于研究的其他示例路由约定：

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

当然，Web API 本身是开源的，因此可以查看内置路由约定的[源代码](http://aspnetwebstack.codeplex.com/)。 这些是在**system.web**命名空间中定义的。
