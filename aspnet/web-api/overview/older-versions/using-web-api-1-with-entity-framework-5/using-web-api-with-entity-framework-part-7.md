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
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="abfea-102">第7部分：创建主页</span><span class="sxs-lookup"><span data-stu-id="abfea-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="abfea-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="abfea-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="abfea-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="abfea-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="abfea-105">创建主页面</span><span class="sxs-lookup"><span data-stu-id="abfea-105">Creating the Main Page</span></span>

<span data-ttu-id="abfea-106">在本部分中，你将创建主应用程序页。</span><span class="sxs-lookup"><span data-stu-id="abfea-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="abfea-107">此页将比管理页更复杂，因此，我们将通过几个步骤来进行处理。</span><span class="sxs-lookup"><span data-stu-id="abfea-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="abfea-108">在此过程中，您将看到一些更高级的挖空技术。</span><span class="sxs-lookup"><span data-stu-id="abfea-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="abfea-109">下面是页面的基本布局：</span><span class="sxs-lookup"><span data-stu-id="abfea-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="abfea-110">"产品" 包含一系列产品。</span><span class="sxs-lookup"><span data-stu-id="abfea-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="abfea-111">"购物车" 包含具有数量的产品的数组。</span><span class="sxs-lookup"><span data-stu-id="abfea-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="abfea-112">单击 "添加到购物车" 将更新购物车。</span><span class="sxs-lookup"><span data-stu-id="abfea-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="abfea-113">"Orders" 包含订单 Id 的数组。</span><span class="sxs-lookup"><span data-stu-id="abfea-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="abfea-114">"详细信息" 包含订单详细信息，这是一组项（产品，含数量）</span><span class="sxs-lookup"><span data-stu-id="abfea-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="abfea-115">首先，我们将在 HTML 中定义一些基本布局，而不包含数据绑定或脚本。</span><span class="sxs-lookup"><span data-stu-id="abfea-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="abfea-116">打开文件视图/Home/Index，并将所有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="abfea-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="abfea-117">接下来，添加脚本部分并创建空视图模型：</span><span class="sxs-lookup"><span data-stu-id="abfea-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="abfea-118">根据前面所绘的设计，视图模型需要可观察量产品、购物车、订单和详细信息。</span><span class="sxs-lookup"><span data-stu-id="abfea-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="abfea-119">将以下变量添加到 `AppViewModel` 对象：</span><span class="sxs-lookup"><span data-stu-id="abfea-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="abfea-120">用户可以将 "产品" 列表中的项添加到购物车中，并从购物车中删除商品。</span><span class="sxs-lookup"><span data-stu-id="abfea-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="abfea-121">为了封装这些函数，我们将创建另一个表示产品的视图模型类。</span><span class="sxs-lookup"><span data-stu-id="abfea-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="abfea-122">将下列代码添加到 `AppViewModel`：</span><span class="sxs-lookup"><span data-stu-id="abfea-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="abfea-123">`ProductViewModel` 类包含两个用于将产品移入和移出购物车的函数： `addItemToCart` 将产品的一个单位添加到购物车，`removeAllFromCart` 删除产品的所有数量。</span><span class="sxs-lookup"><span data-stu-id="abfea-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="abfea-124">用户可以选择现有订单并获取订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="abfea-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="abfea-125">我们会将此功能封装到另一个视图模型中：</span><span class="sxs-lookup"><span data-stu-id="abfea-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="abfea-126">使用订单初始化 `OrderDetailsViewModel`，并通过将 AJAX 请求发送到服务器来提取订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="abfea-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="abfea-127">另外，请注意 `OrderDetailsViewModel`上的 `total` 属性。</span><span class="sxs-lookup"><span data-stu-id="abfea-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="abfea-128">此属性是名为计算的可[观察对象](http://knockoutjs.com/documentation/computedObservables.html)的特殊类型的可观察对象。</span><span class="sxs-lookup"><span data-stu-id="abfea-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="abfea-129">顾名思义，计算的可观测对象允许您在这种情况下，将&#8212;数据绑定到计算所得的值，这是订单的总成本。</span><span class="sxs-lookup"><span data-stu-id="abfea-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="abfea-130">接下来，将这些函数添加到 `AppViewModel`：</span><span class="sxs-lookup"><span data-stu-id="abfea-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="abfea-131">`resetCart` 从购物车中删除所有项。</span><span class="sxs-lookup"><span data-stu-id="abfea-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="abfea-132">`getDetails` 获取订单的详细信息（通过将新 `OrderDetailsViewModel` 推送到 `details` 列表）。</span><span class="sxs-lookup"><span data-stu-id="abfea-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="abfea-133">`createOrder` 创建新订单并清空购物车。</span><span class="sxs-lookup"><span data-stu-id="abfea-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="abfea-134">最后，通过对产品和订单进行 AJAX 请求来初始化视图模型：</span><span class="sxs-lookup"><span data-stu-id="abfea-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="abfea-135">好的，这是很多代码，但我们逐步构建了这种代码，因此，但愿设计是显而易见的。</span><span class="sxs-lookup"><span data-stu-id="abfea-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="abfea-136">现在，我们可以将一些挖空绑定添加到 HTML。</span><span class="sxs-lookup"><span data-stu-id="abfea-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="abfea-137">**产品**</span><span class="sxs-lookup"><span data-stu-id="abfea-137">**Products**</span></span>

<span data-ttu-id="abfea-138">下面是产品列表的绑定：</span><span class="sxs-lookup"><span data-stu-id="abfea-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="abfea-139">这会循环访问 products 数组，并显示名称和价格。</span><span class="sxs-lookup"><span data-stu-id="abfea-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="abfea-140">仅当用户登录时，"添加到订单" 按钮才可见。</span><span class="sxs-lookup"><span data-stu-id="abfea-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="abfea-141">"添加到订单" 按钮会对产品的 `ProductViewModel` 实例调用 `addItemToCart`。</span><span class="sxs-lookup"><span data-stu-id="abfea-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="abfea-142">这说明了挖空的一项不错的功能：当视图模型包含其他视图模型时，可以将绑定应用于内部模型。</span><span class="sxs-lookup"><span data-stu-id="abfea-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="abfea-143">在此示例中，`foreach` 中的绑定应用于每个 `ProductViewModel` 实例。</span><span class="sxs-lookup"><span data-stu-id="abfea-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="abfea-144">这种方法比将所有功能放入单一视图模型要简洁得多。</span><span class="sxs-lookup"><span data-stu-id="abfea-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="abfea-145">**放**</span><span class="sxs-lookup"><span data-stu-id="abfea-145">**Cart**</span></span>

<span data-ttu-id="abfea-146">下面是购物车的绑定：</span><span class="sxs-lookup"><span data-stu-id="abfea-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="abfea-147">这会循环访问 cart 阵列，并显示名称、价格和数量。</span><span class="sxs-lookup"><span data-stu-id="abfea-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="abfea-148">请注意，"删除" 链接和 "创建顺序" 按钮已绑定到视图模型函数。</span><span class="sxs-lookup"><span data-stu-id="abfea-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="abfea-149">**订购**</span><span class="sxs-lookup"><span data-stu-id="abfea-149">**Orders**</span></span>

<span data-ttu-id="abfea-150">下面是 orders 列表的绑定：</span><span class="sxs-lookup"><span data-stu-id="abfea-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="abfea-151">这会循环访问订单并显示订单 ID。</span><span class="sxs-lookup"><span data-stu-id="abfea-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="abfea-152">链接上的 click 事件绑定到 `getDetails` 函数。</span><span class="sxs-lookup"><span data-stu-id="abfea-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="abfea-153">**订单详细信息**</span><span class="sxs-lookup"><span data-stu-id="abfea-153">**Order Details**</span></span>

<span data-ttu-id="abfea-154">下面是订单详细信息的绑定：</span><span class="sxs-lookup"><span data-stu-id="abfea-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="abfea-155">这会循环访问订单中的项目，并显示产品、价格和数量。</span><span class="sxs-lookup"><span data-stu-id="abfea-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="abfea-156">仅当详细信息数组包含一个或多个项时，才会显示周围的 div。</span><span class="sxs-lookup"><span data-stu-id="abfea-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="abfea-157">结束语</span><span class="sxs-lookup"><span data-stu-id="abfea-157">Conclusion</span></span>

<span data-ttu-id="abfea-158">在本教程中，您创建了一个应用程序，该应用程序使用实体框架与数据库进行通信，并 ASP.NET Web API 在数据层的顶层提供面向公众的接口。</span><span class="sxs-lookup"><span data-stu-id="abfea-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="abfea-159">我们使用 ASP.NET MVC 4 来呈现 HTML 页面，并使用挖空和 jQuery 来提供动态交互，无需重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="abfea-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="abfea-160">其他资源:</span><span class="sxs-lookup"><span data-stu-id="abfea-160">Additional resources:</span></span>

- [<span data-ttu-id="abfea-161">ASP.NET 数据访问内容映射</span><span class="sxs-lookup"><span data-stu-id="abfea-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="abfea-162">实体框架开发人员中心</span><span class="sxs-lookup"><span data-stu-id="abfea-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="abfea-163">上一页</span><span class="sxs-lookup"><span data-stu-id="abfea-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
