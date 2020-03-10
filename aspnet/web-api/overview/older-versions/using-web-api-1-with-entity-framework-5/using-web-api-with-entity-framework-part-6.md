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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421286"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="75c98-102">第6部分：创建产品和订单控制器</span><span class="sxs-lookup"><span data-stu-id="75c98-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="75c98-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="75c98-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="75c98-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="75c98-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="75c98-105">添加产品控制器</span><span class="sxs-lookup"><span data-stu-id="75c98-105">Add a Products Controller</span></span>

<span data-ttu-id="75c98-106">管理控制器适用于拥有管理员权限的用户。</span><span class="sxs-lookup"><span data-stu-id="75c98-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="75c98-107">另一方面，客户可以查看产品，但不能创建、更新或删除它们。</span><span class="sxs-lookup"><span data-stu-id="75c98-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="75c98-108">我们可以轻松地限制对 Post、Put 和 Delete 方法的访问，同时使 Get 方法保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="75c98-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="75c98-109">但请查看产品的返回数据：</span><span class="sxs-lookup"><span data-stu-id="75c98-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="75c98-110">`ActualCost` 属性对客户不可见！</span><span class="sxs-lookup"><span data-stu-id="75c98-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="75c98-111">解决方法是定义*数据传输对象*（DTO），其中包含应对客户可见的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="75c98-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="75c98-112">我们将使用 LINQ `Product` 实例来 `ProductDTO` 实例。</span><span class="sxs-lookup"><span data-stu-id="75c98-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="75c98-113">将名为 `ProductDTO` 的类添加到 "模型" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="75c98-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="75c98-114">现在添加控制器。</span><span class="sxs-lookup"><span data-stu-id="75c98-114">Now add the controller.</span></span> <span data-ttu-id="75c98-115">在解决方案资源管理器中，右键单击 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="75c98-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="75c98-116">选择 "**添加**"，然后选择 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="75c98-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="75c98-117">在 "**添加控制器**" 对话框中，将控制器命名为 &quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="75c98-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="75c98-118">在 "**模板**" 下，选择 "**空 API 控制器**"。</span><span class="sxs-lookup"><span data-stu-id="75c98-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="75c98-119">将源文件中的所有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="75c98-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="75c98-120">控制器仍使用 `OrdersContext` 来查询数据库。</span><span class="sxs-lookup"><span data-stu-id="75c98-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="75c98-121">但是，我们调用 `MapProducts` 将它们投影到 `ProductDTO` 实例上，而不是直接返回 `Product` 实例：</span><span class="sxs-lookup"><span data-stu-id="75c98-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="75c98-122">`MapProducts` 方法返回**IQueryable**，因此可以使用其他查询参数编写结果。</span><span class="sxs-lookup"><span data-stu-id="75c98-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="75c98-123">可以在 `GetProduct` 方法中查看此内容，该方法将**where**子句添加到查询中：</span><span class="sxs-lookup"><span data-stu-id="75c98-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="75c98-124">添加订单控制器</span><span class="sxs-lookup"><span data-stu-id="75c98-124">Add an Orders Controller</span></span>

<span data-ttu-id="75c98-125">接下来，添加一个允许用户创建和查看订单的控制器。</span><span class="sxs-lookup"><span data-stu-id="75c98-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="75c98-126">我们将从另一个 DTO 开始。</span><span class="sxs-lookup"><span data-stu-id="75c98-126">We'll start with another DTO.</span></span> <span data-ttu-id="75c98-127">在解决方案资源管理器中，右键单击 "模型" 文件夹并添加一个名为 `OrderDTO` 的类，并使用以下实现：</span><span class="sxs-lookup"><span data-stu-id="75c98-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="75c98-128">现在添加控制器。</span><span class="sxs-lookup"><span data-stu-id="75c98-128">Now add the controller.</span></span> <span data-ttu-id="75c98-129">在解决方案资源管理器中，右键单击 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="75c98-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="75c98-130">选择 "**添加**"，然后选择 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="75c98-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="75c98-131">在 "**添加控制器**" 对话框中，设置以下选项：</span><span class="sxs-lookup"><span data-stu-id="75c98-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="75c98-132">在 "**控制器名称**" 下，输入 "OrdersController"。</span><span class="sxs-lookup"><span data-stu-id="75c98-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="75c98-133">在 "**模板**" 下，选择 "包含读/写操作的 API 控制器，使用实体框架"。</span><span class="sxs-lookup"><span data-stu-id="75c98-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="75c98-134">在 "**模型类**" 下，选择 "&quot;顺序（ProductStore）"&quot;。</span><span class="sxs-lookup"><span data-stu-id="75c98-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="75c98-135">在 "**数据上下文类**" 下，选择 "&quot;OrdersContext （ProductStore）"&quot;。</span><span class="sxs-lookup"><span data-stu-id="75c98-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="75c98-136">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="75c98-136">Click **Add**.</span></span> <span data-ttu-id="75c98-137">这会添加一个名为 OrdersController.cs 的文件。</span><span class="sxs-lookup"><span data-stu-id="75c98-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="75c98-138">接下来，需要修改控制器的默认实现。</span><span class="sxs-lookup"><span data-stu-id="75c98-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="75c98-139">首先，删除 `PutOrder` 和 `DeleteOrder` 方法。</span><span class="sxs-lookup"><span data-stu-id="75c98-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="75c98-140">对于本示例，客户不能修改或删除现有订单。</span><span class="sxs-lookup"><span data-stu-id="75c98-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="75c98-141">在实际应用程序中，需要大量的后端逻辑来处理这些情况。</span><span class="sxs-lookup"><span data-stu-id="75c98-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="75c98-142">（例如，订单是否已发货？）</span><span class="sxs-lookup"><span data-stu-id="75c98-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="75c98-143">更改 `GetOrders` 方法，以仅返回属于用户的订单：</span><span class="sxs-lookup"><span data-stu-id="75c98-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="75c98-144">更改 `GetOrder` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75c98-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="75c98-145">下面是对方法所做的更改：</span><span class="sxs-lookup"><span data-stu-id="75c98-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="75c98-146">返回值为 `OrderDTO` 实例，而不是 `Order`。</span><span class="sxs-lookup"><span data-stu-id="75c98-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="75c98-147">当我们在数据库中查询订单时，将使用[DbQuery](https://msdn.microsoft.com/library/gg696395)方法提取相关 `OrderDetail` 和 `Product` 实体。</span><span class="sxs-lookup"><span data-stu-id="75c98-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="75c98-148">我们使用投影来平展结果。</span><span class="sxs-lookup"><span data-stu-id="75c98-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="75c98-149">HTTP 响应将包含一个产品数组，其中包含数量：</span><span class="sxs-lookup"><span data-stu-id="75c98-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="75c98-150">此格式比包含嵌套实体（订单、详细信息和产品）的原始对象图更易于使用。</span><span class="sxs-lookup"><span data-stu-id="75c98-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="75c98-151">要 `PostOrder`的最后一个方法。</span><span class="sxs-lookup"><span data-stu-id="75c98-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="75c98-152">现在，此方法使用 `Order` 实例。</span><span class="sxs-lookup"><span data-stu-id="75c98-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="75c98-153">但如果客户端发送如下所示的请求正文，则会发生什么情况：</span><span class="sxs-lookup"><span data-stu-id="75c98-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="75c98-154">这是一种结构良好的顺序，实体框架会令人高兴地将其插入到数据库中。</span><span class="sxs-lookup"><span data-stu-id="75c98-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="75c98-155">但它包含以前不存在的产品实体。</span><span class="sxs-lookup"><span data-stu-id="75c98-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="75c98-156">客户端刚在我们的数据库中创建了新产品！</span><span class="sxs-lookup"><span data-stu-id="75c98-156">The client just created a new product in our database!</span></span> <span data-ttu-id="75c98-157">当订单执行部门出现 koala 的订单时，这会对订单履行部门感到吃惊。</span><span class="sxs-lookup"><span data-stu-id="75c98-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="75c98-158">其道德是，对你在 POST 或 PUT 请求中接受的数据非常小心。</span><span class="sxs-lookup"><span data-stu-id="75c98-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="75c98-159">若要避免此问题，请将 `PostOrder` 方法更改为采用 `OrderDTO` 实例。</span><span class="sxs-lookup"><span data-stu-id="75c98-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="75c98-160">使用 `OrderDTO` 创建 `Order`。</span><span class="sxs-lookup"><span data-stu-id="75c98-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="75c98-161">请注意，我们使用 "`ProductID`" 和 "`Quantity`" 属性，并且忽略客户端为产品名称或价格发送的任何值。</span><span class="sxs-lookup"><span data-stu-id="75c98-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="75c98-162">如果产品 ID 无效，则它将与数据库中的外键约束冲突，插入将失败，因为它应该会失败。</span><span class="sxs-lookup"><span data-stu-id="75c98-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="75c98-163">下面是完整的 `PostOrder` 方法：</span><span class="sxs-lookup"><span data-stu-id="75c98-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="75c98-164">最后，将**授权**属性添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="75c98-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="75c98-165">现在只有注册的用户可以创建或查看订单。</span><span class="sxs-lookup"><span data-stu-id="75c98-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="75c98-166">[上一页](using-web-api-with-entity-framework-part-5.md)
> [下一页](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="75c98-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
