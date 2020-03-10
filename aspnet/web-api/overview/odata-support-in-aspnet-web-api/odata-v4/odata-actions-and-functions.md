---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的操作和函数 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，操作和函数是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。 本教程演示如何 。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448058"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="2da52-104">使用 ASP.NET Web API 2.2 的 OData v4 中的操作和函数</span><span class="sxs-lookup"><span data-stu-id="2da52-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="2da52-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2da52-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="2da52-106">在 OData 中，操作和函数是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="2da52-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="2da52-107">本教程演示如何使用 Web API 2.2 将操作和函数添加到 OData v4 终结点。</span><span class="sxs-lookup"><span data-stu-id="2da52-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="2da52-108">本教程基于[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)教程</span><span class="sxs-lookup"><span data-stu-id="2da52-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2da52-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="2da52-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="2da52-110">Web API 2。2</span><span class="sxs-lookup"><span data-stu-id="2da52-110">Web API 2.2</span></span>
> - <span data-ttu-id="2da52-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="2da52-111">OData v4</span></span>
> - <span data-ttu-id="2da52-112">Visual Studio 2013 （[在此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下载 Visual Studio 2017）</span><span class="sxs-lookup"><span data-stu-id="2da52-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="2da52-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2da52-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="2da52-114">教程版本</span><span class="sxs-lookup"><span data-stu-id="2da52-114">Tutorial versions</span></span>
>
> <span data-ttu-id="2da52-115">对于 OData 版本3，请参阅[ASP.NET Web API 2 中的 Odata 操作](../odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="2da52-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="2da52-116">*操作*和*函数*之间的区别在于操作可能有副作用，而函数不会有副作用。</span><span class="sxs-lookup"><span data-stu-id="2da52-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="2da52-117">操作和函数都可以返回数据。</span><span class="sxs-lookup"><span data-stu-id="2da52-117">Both actions and functions can return data.</span></span> <span data-ttu-id="2da52-118">操作的一些用途包括：</span><span class="sxs-lookup"><span data-stu-id="2da52-118">Some uses for actions include:</span></span>

- <span data-ttu-id="2da52-119">复杂事务。</span><span class="sxs-lookup"><span data-stu-id="2da52-119">Complex transactions.</span></span>
- <span data-ttu-id="2da52-120">一次操作多个实体。</span><span class="sxs-lookup"><span data-stu-id="2da52-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="2da52-121">仅允许更新实体的某些属性。</span><span class="sxs-lookup"><span data-stu-id="2da52-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="2da52-122">发送的数据不是实体。</span><span class="sxs-lookup"><span data-stu-id="2da52-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="2da52-123">函数可用于返回与实体或集合不直接对应的信息。</span><span class="sxs-lookup"><span data-stu-id="2da52-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="2da52-124">操作（或函数）可以面向单个实体或集合。</span><span class="sxs-lookup"><span data-stu-id="2da52-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="2da52-125">在 OData 术语中，这是*绑定*。</span><span class="sxs-lookup"><span data-stu-id="2da52-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="2da52-126">你还可以 &quot;未绑定的&quot; 操作/函数，这些操作在服务上被称为静态操作。</span><span class="sxs-lookup"><span data-stu-id="2da52-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="2da52-127">示例：添加操作</span><span class="sxs-lookup"><span data-stu-id="2da52-127">Example: Adding an Action</span></span>

<span data-ttu-id="2da52-128">让我们定义一个操作来对产品进行评级。</span><span class="sxs-lookup"><span data-stu-id="2da52-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="2da52-129">本教程基于教程[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="2da52-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="2da52-130">首先，添加一个 `ProductRating` 模型来表示评级。</span><span class="sxs-lookup"><span data-stu-id="2da52-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="2da52-131">同时，将**DbSet**添加到 `ProductsContext` 类，以便 EF 将在数据库中创建一个分级表。</span><span class="sxs-lookup"><span data-stu-id="2da52-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="2da52-132">向 EDM 添加操作</span><span class="sxs-lookup"><span data-stu-id="2da52-132">Add the Action to the EDM</span></span>

<span data-ttu-id="2da52-133">在 WebApiConfig.cs 中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="2da52-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="2da52-134">**EntityTypeConfiguration**方法将操作添加到实体数据模型（EDM）。</span><span class="sxs-lookup"><span data-stu-id="2da52-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="2da52-135">**参数**方法为操作指定类型化参数。</span><span class="sxs-lookup"><span data-stu-id="2da52-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="2da52-136">此代码还设置 EDM 的命名空间。</span><span class="sxs-lookup"><span data-stu-id="2da52-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="2da52-137">命名空间之所以重要，是因为操作的 URI 包含完全限定的操作名称：</span><span class="sxs-lookup"><span data-stu-id="2da52-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="2da52-138">在典型的 IIS 配置中，此 URL 中的点将导致 IIS 返回错误404。</span><span class="sxs-lookup"><span data-stu-id="2da52-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="2da52-139">可以通过将以下部分添加到 web.config 文件来解决此问题：</span><span class="sxs-lookup"><span data-stu-id="2da52-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="2da52-140">为操作添加控制器方法</span><span class="sxs-lookup"><span data-stu-id="2da52-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="2da52-141">若要启用 &quot;速率&quot; 操作，请将以下方法添加到 `ProductsController`：</span><span class="sxs-lookup"><span data-stu-id="2da52-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="2da52-142">请注意，方法名称与操作名称匹配。</span><span class="sxs-lookup"><span data-stu-id="2da52-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="2da52-143">**[HttpPost]** 特性指定方法是 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="2da52-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="2da52-144">若要调用该操作，客户端将发送 HTTP POST 请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2da52-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="2da52-145">&quot;速率&quot; 操作绑定到产品实例，因此操作的 URI 是附加到实体 URI 的完全限定的操作名称。</span><span class="sxs-lookup"><span data-stu-id="2da52-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="2da52-146">（请记住，我们将 EDM 命名空间设置为 &quot;ProductService&quot;，因此完全限定的操作名称 &quot;ProductService&quot;。）</span><span class="sxs-lookup"><span data-stu-id="2da52-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="2da52-147">请求正文包含操作参数作为 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="2da52-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="2da52-148">Web API 会自动将 JSON 负载转换为**ODataActionParameters**对象，该对象只是参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="2da52-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="2da52-149">使用此字典可以访问控制器方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="2da52-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="2da52-150">如果客户端发送的操作参数格式不正确，则**ModelState**的值为 false。</span><span class="sxs-lookup"><span data-stu-id="2da52-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="2da52-151">检查控制器方法中的此标志，并在**IsValid**为 false 时返回错误。</span><span class="sxs-lookup"><span data-stu-id="2da52-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="2da52-152">示例：添加函数</span><span class="sxs-lookup"><span data-stu-id="2da52-152">Example: Adding a Function</span></span>

<span data-ttu-id="2da52-153">现在，让我们添加一个返回最昂贵的产品的 OData 函数。</span><span class="sxs-lookup"><span data-stu-id="2da52-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="2da52-154">与前面一样，第一步是将函数添加到 EDM。</span><span class="sxs-lookup"><span data-stu-id="2da52-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="2da52-155">在 WebApiConfig.cs 中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="2da52-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="2da52-156">在这种情况下，该函数将绑定到 Products 集合，而不是单独的产品实例。</span><span class="sxs-lookup"><span data-stu-id="2da52-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="2da52-157">客户端通过发送 GET 请求来调用函数：</span><span class="sxs-lookup"><span data-stu-id="2da52-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="2da52-158">下面是此函数的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="2da52-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="2da52-159">请注意，方法名称与函数名称匹配。</span><span class="sxs-lookup"><span data-stu-id="2da52-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="2da52-160">**[HttpGet]** 特性指定方法是 HTTP GET 方法。</span><span class="sxs-lookup"><span data-stu-id="2da52-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="2da52-161">下面是 HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="2da52-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="2da52-162">示例：添加未绑定函数</span><span class="sxs-lookup"><span data-stu-id="2da52-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="2da52-163">上一个示例是绑定到集合的函数。</span><span class="sxs-lookup"><span data-stu-id="2da52-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="2da52-164">在下面的示例中，我们将创建一个*未绑定*的函数。</span><span class="sxs-lookup"><span data-stu-id="2da52-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="2da52-165">未绑定函数将作为服务的静态操作调用。</span><span class="sxs-lookup"><span data-stu-id="2da52-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="2da52-166">在此示例中，函数将返回给定邮政编码的增值税。</span><span class="sxs-lookup"><span data-stu-id="2da52-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="2da52-167">在 Webapiconfig.cs 文件中，将函数添加到 EDM：</span><span class="sxs-lookup"><span data-stu-id="2da52-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="2da52-168">请注意，我们将直接在**ODataModelBuilder**（而不是实体类型或集合）上调用**函数**。</span><span class="sxs-lookup"><span data-stu-id="2da52-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="2da52-169">这会告知模型生成器该函数未绑定。</span><span class="sxs-lookup"><span data-stu-id="2da52-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="2da52-170">下面是实现函数的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="2da52-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="2da52-171">将此方法放在哪个 Web API 控制器上并不重要。</span><span class="sxs-lookup"><span data-stu-id="2da52-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="2da52-172">可以将其放在 `ProductsController`中，也可以定义一个单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="2da52-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="2da52-173">**[ODataRoute]** 特性定义函数的 URI 模板。</span><span class="sxs-lookup"><span data-stu-id="2da52-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="2da52-174">下面是客户端请求的示例：</span><span class="sxs-lookup"><span data-stu-id="2da52-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="2da52-175">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="2da52-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
