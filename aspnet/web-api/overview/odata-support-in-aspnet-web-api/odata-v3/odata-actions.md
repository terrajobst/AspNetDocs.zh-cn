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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600350"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="f9de8-104">ASP.NET Web API 2 中支持 OData 操作</span><span class="sxs-lookup"><span data-stu-id="f9de8-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="f9de8-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f9de8-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f9de8-106">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="f9de8-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="f9de8-107">在 OData 中，*操作*是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="f9de8-108">操作的一些用途包括：</span><span class="sxs-lookup"><span data-stu-id="f9de8-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="f9de8-109">实现复杂事务。</span><span class="sxs-lookup"><span data-stu-id="f9de8-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="f9de8-110">一次操作多个实体。</span><span class="sxs-lookup"><span data-stu-id="f9de8-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="f9de8-111">仅允许更新实体的某些属性。</span><span class="sxs-lookup"><span data-stu-id="f9de8-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="f9de8-112">将信息发送到实体中未定义的服务器。</span><span class="sxs-lookup"><span data-stu-id="f9de8-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f9de8-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="f9de8-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f9de8-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="f9de8-114">Web API 2</span></span>
> - <span data-ttu-id="f9de8-115">OData 版本3</span><span class="sxs-lookup"><span data-stu-id="f9de8-115">OData Version 3</span></span>
> - <span data-ttu-id="f9de8-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="f9de8-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="f9de8-117">示例：对产品进行评级</span><span class="sxs-lookup"><span data-stu-id="f9de8-117">Example: Rating a Product</span></span>

<span data-ttu-id="f9de8-118">在此示例中，我们希望让用户对产品进行评级，并为每个产品公开平均评分。</span><span class="sxs-lookup"><span data-stu-id="f9de8-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="f9de8-119">在数据库中，我们将存储评级列表，并将其键控到产品。</span><span class="sxs-lookup"><span data-stu-id="f9de8-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="f9de8-120">下面是可以用来表示实体框架中的分级的模型：</span><span class="sxs-lookup"><span data-stu-id="f9de8-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="f9de8-121">但我们不希望客户端将 `ProductRating` 对象发布到 "分级" 集合中。</span><span class="sxs-lookup"><span data-stu-id="f9de8-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="f9de8-122">从直观上说，评级与 Products 集合相关联，并且客户端应只需要发布评级值。</span><span class="sxs-lookup"><span data-stu-id="f9de8-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="f9de8-123">因此，我们定义了客户端可以对产品调用的操作，而不是使用一般的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="f9de8-124">在 OData 术语中，此操作将*绑定*到产品实体。</span><span class="sxs-lookup"><span data-stu-id="f9de8-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="f9de8-125">操作在服务器上有副作用。</span><span class="sxs-lookup"><span data-stu-id="f9de8-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="f9de8-126">出于此原因，将使用 HTTP POST 请求来调用它们。</span><span class="sxs-lookup"><span data-stu-id="f9de8-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="f9de8-127">操作可以具有参数和返回类型，在服务元数据中进行了介绍。</span><span class="sxs-lookup"><span data-stu-id="f9de8-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="f9de8-128">客户端会在请求正文中发送参数，服务器将在响应正文中发送返回值。</span><span class="sxs-lookup"><span data-stu-id="f9de8-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="f9de8-129">若要调用 "Rate Product" 操作，客户端需要向 URI 发送 POST，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9de8-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="f9de8-130">POST 请求中的数据只是产品分级：</span><span class="sxs-lookup"><span data-stu-id="f9de8-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="f9de8-131">在实体数据模型中声明操作</span><span class="sxs-lookup"><span data-stu-id="f9de8-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="f9de8-132">在 Web API 配置中，将操作添加到实体数据模型（EDM）：</span><span class="sxs-lookup"><span data-stu-id="f9de8-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="f9de8-133">此代码将 "RateProduct" 定义为可对产品实体执行的操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="f9de8-134">它还声明操作采用名为 "分级" 的**int**参数，并返回一个**整数**值。</span><span class="sxs-lookup"><span data-stu-id="f9de8-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="f9de8-135">将操作添加到控制器</span><span class="sxs-lookup"><span data-stu-id="f9de8-135">Add the Action to the Controller</span></span>

<span data-ttu-id="f9de8-136">"RateProduct" 操作绑定到产品实体。</span><span class="sxs-lookup"><span data-stu-id="f9de8-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="f9de8-137">若要实现此操作，请向 Products 控制器添加一个名为 `RateProduct` 的方法：</span><span class="sxs-lookup"><span data-stu-id="f9de8-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="f9de8-138">请注意，方法名称与 EDM 中操作的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="f9de8-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="f9de8-139">此方法具有两个参数：</span><span class="sxs-lookup"><span data-stu-id="f9de8-139">The method has two parameters:</span></span>

- <span data-ttu-id="f9de8-140">*key*：要进行评级的产品的键。</span><span class="sxs-lookup"><span data-stu-id="f9de8-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="f9de8-141">*parameters*：操作参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="f9de8-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="f9de8-142">如果使用默认路由约定，则必须将密钥参数命名为 "key"。</span><span class="sxs-lookup"><span data-stu-id="f9de8-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="f9de8-143">还必须包含 **[FromOdataUri]** 属性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9de8-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="f9de8-144">此属性告知 Web API 在分析来自请求 URI 的密钥时使用 OData 语法规则。</span><span class="sxs-lookup"><span data-stu-id="f9de8-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="f9de8-145">使用*parameters*字典获取操作参数：</span><span class="sxs-lookup"><span data-stu-id="f9de8-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="f9de8-146">如果客户端发送正确格式的操作参数，则**ModelState**的值为 true。</span><span class="sxs-lookup"><span data-stu-id="f9de8-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="f9de8-147">在这种情况下，可以使用**ODataActionParameters**字典获取参数值。</span><span class="sxs-lookup"><span data-stu-id="f9de8-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="f9de8-148">在此示例中，`RateProduct` 操作采用一个名为 "分级" 的参数。</span><span class="sxs-lookup"><span data-stu-id="f9de8-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="f9de8-149">操作元数据</span><span class="sxs-lookup"><span data-stu-id="f9de8-149">Action Metadata</span></span>

<span data-ttu-id="f9de8-150">若要查看服务元数据，请将 GET 请求发送到/odata/$metadata。</span><span class="sxs-lookup"><span data-stu-id="f9de8-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="f9de8-151">下面是声明 `RateProduct` 操作的元数据部分：</span><span class="sxs-lookup"><span data-stu-id="f9de8-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="f9de8-152">**FunctionImport**元素声明操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="f9de8-153">大多数字段都一目了然，但有两个值得注意的事项：</span><span class="sxs-lookup"><span data-stu-id="f9de8-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="f9de8-154">**IsBindable**是指在目标实体上至少可以调用此操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="f9de8-155">**IsAlwaysBindable**表示操作始终可以在目标实体上调用。</span><span class="sxs-lookup"><span data-stu-id="f9de8-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="f9de8-156">不同之处在于一些操作对客户端始终可用，但其他操作可能取决于实体的状态。</span><span class="sxs-lookup"><span data-stu-id="f9de8-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="f9de8-157">例如，假设您定义了 "购买" 操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="f9de8-158">只能购买库存项。</span><span class="sxs-lookup"><span data-stu-id="f9de8-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="f9de8-159">如果项脱销，客户端将无法调用该操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="f9de8-160">定义 EDM 时，**操作**方法会创建一个始终可绑定的操作：</span><span class="sxs-lookup"><span data-stu-id="f9de8-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="f9de8-161">我将在本主题的后面部分讨论非始终可绑定的操作（也称为*暂时性*操作）。</span><span class="sxs-lookup"><span data-stu-id="f9de8-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="f9de8-162">调用操作</span><span class="sxs-lookup"><span data-stu-id="f9de8-162">Invoking the Action</span></span>

<span data-ttu-id="f9de8-163">现在让我们看一下客户端将如何调用此操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="f9de8-164">假设客户端要向 ID 为4的产品提供2的评级。</span><span class="sxs-lookup"><span data-stu-id="f9de8-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="f9de8-165">下面是使用请求正文的 JSON 格式的示例请求消息：</span><span class="sxs-lookup"><span data-stu-id="f9de8-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="f9de8-166">下面是响应消息：</span><span class="sxs-lookup"><span data-stu-id="f9de8-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="f9de8-167">将操作绑定到实体集</span><span class="sxs-lookup"><span data-stu-id="f9de8-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="f9de8-168">在上面的示例中，操作绑定到单个实体：客户端对单个产品进行评级。</span><span class="sxs-lookup"><span data-stu-id="f9de8-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="f9de8-169">你还可以将操作绑定到实体的集合。</span><span class="sxs-lookup"><span data-stu-id="f9de8-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="f9de8-170">只需进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="f9de8-170">Just make the following changes:</span></span>

<span data-ttu-id="f9de8-171">在 EDM 中，将操作添加到实体的**集合**属性。</span><span class="sxs-lookup"><span data-stu-id="f9de8-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="f9de8-172">在控制器方法中，省略*key*参数。</span><span class="sxs-lookup"><span data-stu-id="f9de8-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="f9de8-173">现在，客户端将调用 Products 实体集上的操作：</span><span class="sxs-lookup"><span data-stu-id="f9de8-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="f9de8-174">具有集合参数的操作</span><span class="sxs-lookup"><span data-stu-id="f9de8-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="f9de8-175">操作可以具有采用值集合的参数。</span><span class="sxs-lookup"><span data-stu-id="f9de8-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="f9de8-176">在 EDM 中，使用**CollectionParameter&lt;t&gt;** 声明参数。</span><span class="sxs-lookup"><span data-stu-id="f9de8-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="f9de8-177">这将声明一个名为 "分级" 的参数，该参数采用**int**值的集合。</span><span class="sxs-lookup"><span data-stu-id="f9de8-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="f9de8-178">在控制器方法中，仍从**ODataActionParameters**对象获取参数值，但现在值为**ICollection&lt;int&gt;** 值：</span><span class="sxs-lookup"><span data-stu-id="f9de8-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="f9de8-179">暂时性操作</span><span class="sxs-lookup"><span data-stu-id="f9de8-179">Transient Actions</span></span>

<span data-ttu-id="f9de8-180">在 "RateProduct" 示例中，用户始终可以对产品进行分级，因此该操作始终可用。</span><span class="sxs-lookup"><span data-stu-id="f9de8-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="f9de8-181">但某些操作依赖于实体的状态。</span><span class="sxs-lookup"><span data-stu-id="f9de8-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="f9de8-182">例如，在视频租赁服务中，"结帐" 操作并非始终可用。</span><span class="sxs-lookup"><span data-stu-id="f9de8-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="f9de8-183">（这取决于该视频的副本是否可用。）这种类型的操作称为*暂时性*操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="f9de8-184">在服务元数据中，暂时性操作的**IsAlwaysBindable**等于 false。</span><span class="sxs-lookup"><span data-stu-id="f9de8-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="f9de8-185">这实际上是默认值，因此元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9de8-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="f9de8-186">这就是这一问题的原因：如果操作是暂时性的，则服务器需要在操作可用时通知客户端。</span><span class="sxs-lookup"><span data-stu-id="f9de8-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="f9de8-187">它通过在实体中包含指向操作的链接来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="f9de8-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="f9de8-188">下面是电影实体的示例：</span><span class="sxs-lookup"><span data-stu-id="f9de8-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="f9de8-189">"#CheckOut" 属性包含指向签出操作的链接。</span><span class="sxs-lookup"><span data-stu-id="f9de8-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="f9de8-190">如果此操作不可用，则服务器将忽略链接。</span><span class="sxs-lookup"><span data-stu-id="f9de8-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="f9de8-191">若要在 EDM 中声明暂时性操作，请调用**TransientAction**方法：</span><span class="sxs-lookup"><span data-stu-id="f9de8-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="f9de8-192">此外，还必须提供一个函数，该函数返回给定实体的操作链接。</span><span class="sxs-lookup"><span data-stu-id="f9de8-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="f9de8-193">通过调用**HasActionLink**来设置此函数。</span><span class="sxs-lookup"><span data-stu-id="f9de8-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="f9de8-194">可以将函数编写为 lambda 表达式：</span><span class="sxs-lookup"><span data-stu-id="f9de8-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="f9de8-195">如果此操作可用，则 lambda 表达式将返回指向操作的链接。</span><span class="sxs-lookup"><span data-stu-id="f9de8-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="f9de8-196">OData 序列化程序在序列化实体时包含此链接。</span><span class="sxs-lookup"><span data-stu-id="f9de8-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="f9de8-197">当操作不可用时，函数将返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="f9de8-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9de8-198">其他资源</span><span class="sxs-lookup"><span data-stu-id="f9de8-198">Additional Resources</span></span>

[<span data-ttu-id="f9de8-199">OData 操作示例</span><span class="sxs-lookup"><span data-stu-id="f9de8-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
