---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 第6部分：创建产品和订单控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600030"
---
# <a name="part-6-creating-product-and-order-controllers"></a>第6部分：创建产品和订单控制器

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>添加产品控制器

管理控制器适用于拥有管理员权限的用户。 另一方面，客户可以查看产品，但不能创建、更新或删除它们。

我们可以轻松地限制对 Post、Put 和 Delete 方法的访问，同时使 Get 方法保持打开状态。 但请查看产品的返回数据：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

`ActualCost` 属性对客户不可见！ 解决方法是定义*数据传输对象*（DTO），其中包含应对客户可见的属性的子集。 我们将使用 LINQ `Product` 实例来 `ProductDTO` 实例。

将名为 `ProductDTO` 的类添加到 "模型" 文件夹。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

现在添加控制器。 在解决方案资源管理器中，右键单击 "控制器" 文件夹。 选择 "**添加**"，然后选择 "**控制器**"。 在 "**添加控制器**" 对话框中，将控制器命名为 &quot;ProductsController&quot;。 在 "**模板**" 下，选择 "**空 API 控制器**"。

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

将源文件中的所有内容替换为以下代码：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

控制器仍使用 `OrdersContext` 来查询数据库。 但是，我们调用 `MapProducts` 将它们投影到 `ProductDTO` 实例上，而不是直接返回 `Product` 实例：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

`MapProducts` 方法返回**IQueryable**，因此可以使用其他查询参数编写结果。 可以在 `GetProduct` 方法中查看此内容，该方法将**where**子句添加到查询中：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>添加订单控制器

接下来，添加一个允许用户创建和查看订单的控制器。

我们将从另一个 DTO 开始。 在解决方案资源管理器中，右键单击 "模型" 文件夹并添加一个名为 `OrderDTO` 的类，并使用以下实现：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

现在添加控制器。 在解决方案资源管理器中，右键单击 "控制器" 文件夹。 选择 "**添加**"，然后选择 "**控制器**"。 在 "**添加控制器**" 对话框中，设置以下选项：

- 在 "**控制器名称**" 下，输入 "OrdersController"。
- 在 "**模板**" 下，选择 "包含读/写操作的 API 控制器，使用实体框架"。
- 在 "**模型类**" 下，选择 "&quot;顺序（ProductStore）"&quot;。
- 在 "**数据上下文类**" 下，选择 "&quot;OrdersContext （ProductStore）"&quot;。

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

单击 **添加**。 这会添加一个名为 OrdersController.cs 的文件。 接下来，需要修改控制器的默认实现。

首先，删除 `PutOrder` 和 `DeleteOrder` 方法。 对于本示例，客户不能修改或删除现有订单。 在实际应用程序中，需要大量的后端逻辑来处理这些情况。 （例如，订单是否已发货？）

更改 `GetOrders` 方法，以仅返回属于用户的订单：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

更改 `GetOrder` 方法，如下所示：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

下面是对方法所做的更改：

- 返回值为 `OrderDTO` 实例，而不是 `Order`。
- 当我们在数据库中查询订单时，将使用[DbQuery](https://msdn.microsoft.com/library/gg696395)方法提取相关 `OrderDetail` 和 `Product` 实体。
- 我们使用投影来平展结果。

HTTP 响应将包含一个产品数组，其中包含数量：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

此格式比包含嵌套实体（订单、详细信息和产品）的原始对象图更易于使用。

要 `PostOrder`的最后一个方法。 现在，此方法使用 `Order` 实例。 但如果客户端发送如下所示的请求正文，则会发生什么情况：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

这是一种结构良好的顺序，实体框架会令人高兴地将其插入到数据库中。 但它包含以前不存在的产品实体。 客户端刚在我们的数据库中创建了新产品！ 当订单执行部门出现 koala 的订单时，这会对订单履行部门感到吃惊。 其道德是，对你在 POST 或 PUT 请求中接受的数据非常小心。

若要避免此问题，请将 `PostOrder` 方法更改为采用 `OrderDTO` 实例。 使用 `OrderDTO` 创建 `Order`。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

请注意，我们使用 "`ProductID`" 和 "`Quantity`" 属性，并且忽略客户端为产品名称或价格发送的任何值。 如果产品 ID 无效，则它将与数据库中的外键约束冲突，插入将失败，因为它应该会失败。

下面是完整的 `PostOrder` 方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

最后，将**授权**属性添加到控制器：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

现在只有注册的用户可以创建或查看订单。

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-5.md)
> [下一页](using-web-api-with-entity-framework-part-7.md)
