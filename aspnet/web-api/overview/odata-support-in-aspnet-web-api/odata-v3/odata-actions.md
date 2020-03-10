---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: 支持 ASP.NET Web API 2 中的 OData 操作 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，操作是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。 操作的一些用途包括： "实现 ..."
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448172"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中支持 OData 操作

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 在 OData 中，*操作*是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。 操作的一些用途包括：
> 
> - 实现复杂事务。
> - 一次操作多个实体。
> - 仅允许更新实体的某些属性。
> - 将信息发送到实体中未定义的服务器。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API 2
> - OData 版本3
> - Entity Framework 6

## <a name="example-rating-a-product"></a>示例：对产品进行评级

在此示例中，我们希望让用户对产品进行评级，并为每个产品公开平均评分。 在数据库中，我们将存储评级列表，并将其键控到产品。

下面是可以用来表示实体框架中的分级的模型：

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

但我们不希望客户端将 `ProductRating` 对象发布到 "分级" 集合中。 从直观上说，评级与 Products 集合相关联，并且客户端应只需要发布评级值。

因此，我们定义了客户端可以对产品调用的操作，而不是使用一般的 CRUD 操作。 在 OData 术语中，此操作将*绑定*到产品实体。

>操作在服务器上有副作用。 出于此原因，将使用 HTTP POST 请求来调用它们。 操作可以具有参数和返回类型，在服务元数据中进行了介绍。 客户端会在请求正文中发送参数，服务器将在响应正文中发送返回值。 若要调用 "Rate Product" 操作，客户端需要向 URI 发送 POST，如下所示：

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 请求中的数据只是产品分级：

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>在实体数据模型中声明操作

在 Web API 配置中，将操作添加到实体数据模型（EDM）：

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

此代码将 "RateProduct" 定义为可对产品实体执行的操作。 它还声明操作采用名为 "分级" 的**int**参数，并返回一个**整数**值。

## <a name="add-the-action-to-the-controller"></a>将操作添加到控制器

"RateProduct" 操作绑定到产品实体。 若要实现此操作，请向 Products 控制器添加一个名为 `RateProduct` 的方法：

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

请注意，方法名称与 EDM 中操作的名称相匹配。 此方法具有两个参数：

- *key*：要进行评级的产品的键。
- *parameters*：操作参数值的字典。

如果使用默认路由约定，则必须将密钥参数命名为 "key"。 还必须包含 **[FromOdataUri]** 属性，如下所示。 此属性告知 Web API 在分析来自请求 URI 的密钥时使用 OData 语法规则。

使用*parameters*字典获取操作参数：

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

如果客户端发送正确格式的操作参数，则**ModelState**的值为 true。 在这种情况下，可以使用**ODataActionParameters**字典获取参数值。 在此示例中，`RateProduct` 操作采用一个名为 "分级" 的参数。

## <a name="action-metadata"></a>操作元数据

若要查看服务元数据，请将 GET 请求发送到/odata/$metadata。 下面是声明 `RateProduct` 操作的元数据部分：

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport**元素声明操作。 大多数字段都一目了然，但有两个值得注意的事项：

- **IsBindable**是指在目标实体上至少可以调用此操作。
- **IsAlwaysBindable**表示操作始终可以在目标实体上调用。

不同之处在于一些操作对客户端始终可用，但其他操作可能取决于实体的状态。 例如，假设您定义了 "购买" 操作。 只能购买库存项。 如果项脱销，客户端将无法调用该操作。

定义 EDM 时，**操作**方法会创建一个始终可绑定的操作：

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

我将在本主题的后面部分讨论非始终可绑定的操作（也称为*暂时性*操作）。

## <a name="invoking-the-action"></a>调用操作

现在让我们看一下客户端将如何调用此操作。 假设客户端要向 ID 为4的产品提供2的评级。 下面是使用请求正文的 JSON 格式的示例请求消息：

[!code-console[Main](odata-actions/samples/sample9.cmd)]

下面是响应消息：

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>将操作绑定到实体集

在上面的示例中，操作绑定到单个实体：客户端对单个产品进行评级。 你还可以将操作绑定到实体的集合。 只需进行以下更改：

在 EDM 中，将操作添加到实体的**集合**属性。

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

在控制器方法中，省略*key*参数。

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

现在，客户端将调用 Products 实体集上的操作：

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>具有集合参数的操作

操作可以具有采用值集合的参数。 在 EDM 中，使用**CollectionParameter&lt;t&gt;** 声明参数。

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

这将声明一个名为 "分级" 的参数，该参数采用**int**值的集合。 在控制器方法中，仍从**ODataActionParameters**对象获取参数值，但现在值为**ICollection&lt;int&gt;** 值：

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>暂时性操作

在 "RateProduct" 示例中，用户始终可以对产品进行分级，因此该操作始终可用。 但某些操作依赖于实体的状态。 例如，在视频租赁服务中，"结帐" 操作并非始终可用。 （这取决于该视频的副本是否可用。）这种类型的操作称为*暂时性*操作。

在服务元数据中，暂时性操作的**IsAlwaysBindable**等于 false。 这实际上是默认值，因此元数据将如下所示：

[!code-xml[Main](odata-actions/samples/sample16.xml)]

这就是这一问题的原因：如果操作是暂时性的，则服务器需要在操作可用时通知客户端。 它通过在实体中包含指向操作的链接来完成此操作。 下面是电影实体的示例：

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" 属性包含指向签出操作的链接。 如果此操作不可用，则服务器将忽略链接。

若要在 EDM 中声明暂时性操作，请调用**TransientAction**方法：

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

此外，还必须提供一个函数，该函数返回给定实体的操作链接。 通过调用**HasActionLink**来设置此函数。 可以将函数编写为 lambda 表达式：

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

如果此操作可用，则 lambda 表达式将返回指向操作的链接。 OData 序列化程序在序列化实体时包含此链接。 当操作不可用时，函数将返回 `null`。

## <a name="additional-resources"></a>其他资源

[OData 操作示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
