---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API 中的路由和操作选择 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446912"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a>ASP.NET Web API 中的路由和操作选择

作者： [Mike Wasson](https://github.com/MikeWasson)

本文介绍 ASP.NET Web API 如何将 HTTP 请求路由到控制器上的特定操作。

> [!NOTE]
> 有关路由的高级概述，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

本文介绍路由过程的详细信息。 如果你创建一个 Web API 项目，并发现某些请求没有按你预期的方式路由，那么这篇文章将会有所帮助。

路由有三个主要阶段：

1. 匹配路由模板的 URI。
2. 选择控制器。
3. 选择操作。

您可以用自己的自定义行为来替换过程的某些部分。 本文介绍了默认行为。 最后，我注意到了可以自定义该行为的位置。

## <a name="route-templates"></a>路由模板

路由模板看起来类似于 URI 路径，但它可以包含占位符值，用大括号指示：

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

创建路由时，可以为部分或全部占位符提供默认值：

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

你还可以提供约束，限制 URI 段如何匹配占位符：

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

框架尝试将 URI 路径中的段与模板进行匹配。 模板中的文本必须完全匹配。 占位符匹配任何值，除非指定约束。 框架与 URI 的其他部分（如主机名或查询参数）不匹配。 该框架选择与 URI 匹配的路由表中的第一个路由。

有两个特殊占位符： "{controller}" 和 "{action}"。

- "{controller}" 提供控制器的名称。
- "{action}" 提供操作的名称。 在 Web API 中，通常会省略 "{action}"。

### <a name="defaults"></a>默认值

如果提供默认值，则路由将匹配缺少这些段的 URI。 例如:

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

Uri `http://localhost/api/products/all` 和 `http://localhost/api/products` 与前面的路由匹配。 在后一个 URI 中，将为缺少的 `{category}` 段指定默认值 `all`。

### <a name="route-dictionary"></a>路由字典

如果框架找到一个 URI 匹配项，则会创建一个包含每个占位符的值的字典。 键是占位符名称，不包括大括号。 值取自 URI 路径或默认值。 字典存储在**IHttpRouteData**对象中。

在此路由匹配阶段，将像处理其他占位符一样处理特殊的 "{controller}" 和 "{action}" 占位符。 它们只是与其他值一起存储在字典中。

默认值可以有特殊值**RouteParameter**。 如果为占位符分配了此值，则不会将该值添加到路由字典中。 例如:

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

对于 URI 路径 "api/products"，路由字典将包含：

- 控制器： "products"
- 类别： "all"

但对于 "api/products/玩具/123"，路由字典将包含：

- 控制器： "products"
- 类别： "玩具"
- id： "123"

默认值还可以包括未在路由模板中的任何位置显示的值。 如果路由匹配，则该值存储在字典中。 例如:

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

如果 URI 路径为 "api/root/8"，则字典将包含两个值：

- 控制器： "customers"
- id： "8"

## <a name="selecting-a-controller"></a>选择控制器

控制器选择由**IHttpControllerSelector. SelectController**方法处理。 此方法使用**HttpRequestMessage**实例并返回**HttpControllerDescriptor**。 默认实现由**DefaultHttpControllerSelector**类提供。 此类使用简单的算法：

1. 在路由字典中查找键 "controller"。
2. 获取此键的值并附加字符串 "Controller" 以获取控制器类型名称。
3. 查找具有此类型名称的 Web API 控制器。

例如，如果路由字典包含键值对 "controller" = "products"，则控制器类型为 "ProductsController"。 如果没有匹配的类型或多个匹配项，则该框架会向客户端返回一个错误。

对于步骤3， **DefaultHttpControllerSelector**使用**IHttpControllerTypeResolver**接口获取 Web API 控制器类型的列表。 **IHttpControllerTypeResolver**的默认实现返回实现**IHttpController**的所有公共类（a），（b）不是抽象类，（c）的名称以 "Controller" 结尾。

## <a name="action-selection"></a>操作选择

选择控制器后，框架会通过调用**IHttpActionSelector. SelectAction**方法选择操作。 此方法采用**system.web.http.controllers.httpcontrollercontext**并返回**HttpActionDescriptor**。

默认实现由**ApiControllerActionSelector**类提供。 若要选择操作，请查看以下内容：

- 请求的 HTTP 方法。
- 路由模板中的 "{action}" 占位符（如果存在）。
- 控制器上的操作的参数。

在查看选择算法之前，我们需要了解有关控制器操作的一些内容。

**控制器上的哪些方法被视为 "操作"？** 选择操作时，框架仅查看控制器上的公共实例方法。 此外，它还不包括["特殊名称"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)方法（构造函数、事件、运算符重载等）以及从**ApiController**类继承的方法。

**HTTP 方法。** 框架只选择与请求的 HTTP 方法匹配的操作，确定如下：

1. 可以使用特性指定 HTTP 方法： **AcceptVerbs**、 **HttpDelete**、 **HttpGet**、 **HttpHead**、 **HttpOptions**、 **HttpPatch**、 **HttpPost**或**HttpPut**。
2. 否则，如果控制器方法的名称以 "Get"、"Post"、"Put"、"Delete"、"Head"、"Options" 或 "Patch" 开头，则按照约定，操作支持该 HTTP 方法。
3. 如果以上均不是，则该方法支持 POST。

**参数绑定。** 参数绑定是 Web API 为参数创建值的方式。 以下是参数绑定的默认规则：

- 简单类型是从 URI 获取的。
- 复杂类型取自请求正文。

简单类型包括所有[.NET Framework 基元类型](https://msdn.microsoft.com/library/system.type.isprimitive)，以及**DateTime**、 **Decimal**、 **Guid**、 **String**和**TimeSpan**。 对于每个操作，最多只能有一个参数读取请求正文。

> [!NOTE]
> 可以重写默认的绑定规则。 请参阅[WebAPI 参数绑定](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)。

此背景为操作选择算法。

1. 在控制器上创建一个与 HTTP 请求方法匹配的所有操作的列表。
2. 如果路由字典具有 "action" 条目，则删除名称与此值不匹配的操作。
3. 尝试将操作参数与 URI 匹配，如下所示： 

    1. 对于每个操作，获取作为简单类型的参数的列表，其中的绑定从 URI 获取参数。 排除可选参数。
    2. 从此列表中，尝试在路由字典或 URI 查询字符串中查找每个参数名称的匹配项。 匹配不区分大小写，也不依赖于参数顺序。
    3. 选择一个操作，其中列表中的每个参数在 URI 中都有匹配项。
    4. 如果有多个操作满足这些条件，则选择具有最多参数匹配项的操作。
4. 忽略带有 **[NonAction]** 属性的操作。

步骤 #3 可能是最容易混淆的。 基本思路是，参数可以从 URI、请求正文或自定义绑定获取其值。 对于来自 URI 的参数，我们想要确保 URI 在路径（通过路由字典）或查询字符串中实际包含该参数的值。

例如，请考虑以下操作：

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

*Id*参数将绑定到 URI。 因此，此操作只能与包含 "id" 值的 URI 匹配，无论是在路由字典中还是在查询字符串中。

可选参数是一个异常，因为这些参数是可选的。 对于可选参数，如果绑定无法从 URI 获取值，则它是正常的。

复杂类型是一个不同原因的异常。 复杂类型只能通过自定义绑定绑定到 URI。 但在这种情况下，框架不会提前知道参数是否会绑定到特定的 URI。 若要确定，需要调用绑定。 选择算法的目标是在调用任何绑定之前从静态说明中选择操作。 因此，复杂类型会从匹配算法中排除。

选择操作后，将调用所有参数绑定。

摘要:

- 操作必须匹配请求的 HTTP 方法。
- 操作名称必须与路由字典中的 "action" 条目匹配（如果存在）。
- 对于操作的每个参数，如果参数是从 URI 获取的，则必须在路由字典或 URI 查询字符串中找到参数名称。 （排除包含复杂类型的可选参数和参数。）
- 尝试匹配最多的参数。 最佳匹配可能是不带参数的方法。

## <a name="extended-example"></a>扩展示例

到达

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

控制器:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP 请求：

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>路由匹配

URI 与名为 "DefaultApi" 的路由匹配。 路由字典包含以下项：

- 控制器： "products"
- id： "1"

路由字典不包含查询字符串参数 "版本" 和 "详细信息"，但在操作选择过程中仍会考虑这些参数。

### <a name="controller-selection"></a>控制器选择

对于路由字典中的 "控制器" 条目，控制器类型为 `ProductsController`。

### <a name="action-selection"></a>操作选择

HTTP 请求是一个 GET 请求。 支持 GET 的控制器操作 `GetAll`、`GetById`和 `FindProductsByName`。 路由字典不包含 "action" 的条目，因此我们不需要与操作名称匹配。

接下来，我们尝试匹配操作的参数名称，仅查找 "获取" 操作。

| 操作 | 要匹配的参数 |
| --- | --- |
| `GetAll` | 无 |
| `GetById` | "id" |
| `FindProductsByName` | 路径名 |

请注意，不会考虑 `GetById` 的*version*参数，因为它是一个可选参数。

`GetAll` 方法与完全匹配。 `GetById` 方法也匹配，因为路由字典包含 "id"。 `FindProductsByName` 方法不匹配。

`GetById` 方法入选，因为它匹配一个参数，而不是 `GetAll`的参数。 方法是通过以下参数值调用的：

- *id* = 1
- *版本*= 1。5

请注意，尽管选择算法中未使用*版本*，但参数的值来自 URI 查询字符串。

## <a name="extension-points"></a>扩展点

Web API 为路由过程的某些部分提供扩展点。

| 接口 | 说明 |
| --- | --- |
| **IHttpControllerSelector** | 选择控制器。 |
| **IHttpControllerTypeResolver** | 获取控制器类型的列表。 **DefaultHttpControllerSelector**从此列表中选择控制器类型。 |
| **IAssembliesResolver** | 获取项目程序集的列表。 **IHttpControllerTypeResolver**接口使用此列表来查找控制器类型。 |
| **IHttpControllerActivator** | 创建新的控制器实例。 |
| **IHttpActionSelector** | 选择操作。 |
| **IHttpActionInvoker** | 调用操作。 |

若要为这些接口提供自己的实现，请使用**HttpConfiguration**对象上的**服务**集合：

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
