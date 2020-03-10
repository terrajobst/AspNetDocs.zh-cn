---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 第7部分：创建主页 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484448"
---
# <a name="part-7-creating-the-main-page"></a>第7部分：创建主页

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>创建主页面

在本部分中，你将创建主应用程序页。 此页将比管理页更复杂，因此，我们将通过几个步骤来进行处理。 在此过程中，您将看到一些更高级的挖空技术。 下面是页面的基本布局：

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "产品" 包含一系列产品。
- "购物车" 包含具有数量的产品的数组。 单击 "添加到购物车" 将更新购物车。
- "Orders" 包含订单 Id 的数组。
- "详细信息" 包含订单详细信息，这是一组项（产品，含数量）

首先，我们将在 HTML 中定义一些基本布局，而不包含数据绑定或脚本。 打开文件视图/Home/Index，并将所有内容替换为以下内容：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

接下来，添加脚本部分并创建空视图模型：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

根据前面所绘的设计，视图模型需要可观察量产品、购物车、订单和详细信息。 将以下变量添加到 `AppViewModel` 对象：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

用户可以将 "产品" 列表中的项添加到购物车中，并从购物车中删除商品。 为了封装这些函数，我们将创建另一个表示产品的视图模型类。 将下列代码添加到 `AppViewModel`：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel` 类包含两个用于将产品移入和移出购物车的函数： `addItemToCart` 将产品的一个单位添加到购物车，`removeAllFromCart` 删除产品的所有数量。

用户可以选择现有订单并获取订单详细信息。 我们会将此功能封装到另一个视图模型中：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

使用订单初始化 `OrderDetailsViewModel`，并通过将 AJAX 请求发送到服务器来提取订单详细信息。

另外，请注意 `OrderDetailsViewModel`上的 `total` 属性。 此属性是名为计算的可[观察对象](http://knockoutjs.com/documentation/computedObservables.html)的特殊类型的可观察对象。 顾名思义，计算的可观测对象允许您在这种情况下，将&#8212;数据绑定到计算所得的值，这是订单的总成本。

接下来，将这些函数添加到 `AppViewModel`：

- `resetCart` 从购物车中删除所有项。
- `getDetails` 获取订单的详细信息（通过将新 `OrderDetailsViewModel` 推送到 `details` 列表）。
- `createOrder` 创建新订单并清空购物车。

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

最后，通过对产品和订单进行 AJAX 请求来初始化视图模型：

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

好的，这是很多代码，但我们逐步构建了这种代码，因此，但愿设计是显而易见的。 现在，我们可以将一些挖空绑定添加到 HTML。

**产品**

下面是产品列表的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

这会循环访问 products 数组，并显示名称和价格。 仅当用户登录时，"添加到订单" 按钮才可见。

"添加到订单" 按钮会对产品的 `ProductViewModel` 实例调用 `addItemToCart`。 这说明了挖空的一项不错的功能：当视图模型包含其他视图模型时，可以将绑定应用于内部模型。 在此示例中，`foreach` 中的绑定应用于每个 `ProductViewModel` 实例。 这种方法比将所有功能放入单一视图模型要简洁得多。

**放**

下面是购物车的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

这会循环访问 cart 阵列，并显示名称、价格和数量。 请注意，"删除" 链接和 "创建顺序" 按钮已绑定到视图模型函数。

**订购**

下面是 orders 列表的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

这会循环访问订单并显示订单 ID。 链接上的 click 事件绑定到 `getDetails` 函数。

**订单详细信息**

下面是订单详细信息的绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

这会循环访问订单中的项目，并显示产品、价格和数量。 仅当详细信息数组包含一个或多个项时，才会显示周围的 div。

## <a name="conclusion"></a>结束语

在本教程中，您创建了一个应用程序，该应用程序使用实体框架与数据库进行通信，并 ASP.NET Web API 在数据层的顶层提供面向公众的接口。 我们使用 ASP.NET MVC 4 来呈现 HTML 页面，并使用挖空和 jQuery 来提供动态交互，无需重新加载页面。

其他资源:

- [ASP.NET 数据访问内容映射](https://msdn.microsoft.com/library/6759sth4.aspx)
- [实体框架开发人员中心](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-6.md)
