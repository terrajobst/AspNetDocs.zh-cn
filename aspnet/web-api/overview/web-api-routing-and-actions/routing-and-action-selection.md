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
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="f611b-102">ASP.NET Web API 中的路由和操作选择</span><span class="sxs-lookup"><span data-stu-id="f611b-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="f611b-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f611b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f611b-104">本文介绍 ASP.NET Web API 如何将 HTTP 请求路由到控制器上的特定操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="f611b-105">有关路由的高级概述，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f611b-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="f611b-106">本文介绍路由过程的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f611b-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="f611b-107">如果你创建一个 Web API 项目，并发现某些请求没有按你预期的方式路由，那么这篇文章将会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="f611b-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="f611b-108">路由有三个主要阶段：</span><span class="sxs-lookup"><span data-stu-id="f611b-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="f611b-109">匹配路由模板的 URI。</span><span class="sxs-lookup"><span data-stu-id="f611b-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="f611b-110">选择控制器。</span><span class="sxs-lookup"><span data-stu-id="f611b-110">Selecting a controller.</span></span>
3. <span data-ttu-id="f611b-111">选择操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-111">Selecting an action.</span></span>

<span data-ttu-id="f611b-112">您可以用自己的自定义行为来替换过程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="f611b-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="f611b-113">本文介绍了默认行为。</span><span class="sxs-lookup"><span data-stu-id="f611b-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="f611b-114">最后，我注意到了可以自定义该行为的位置。</span><span class="sxs-lookup"><span data-stu-id="f611b-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="f611b-115">路由模板</span><span class="sxs-lookup"><span data-stu-id="f611b-115">Route Templates</span></span>

<span data-ttu-id="f611b-116">路由模板看起来类似于 URI 路径，但它可以包含占位符值，用大括号指示：</span><span class="sxs-lookup"><span data-stu-id="f611b-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="f611b-117">创建路由时，可以为部分或全部占位符提供默认值：</span><span class="sxs-lookup"><span data-stu-id="f611b-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="f611b-118">你还可以提供约束，限制 URI 段如何匹配占位符：</span><span class="sxs-lookup"><span data-stu-id="f611b-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="f611b-119">框架尝试将 URI 路径中的段与模板进行匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="f611b-120">模板中的文本必须完全匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="f611b-121">占位符匹配任何值，除非指定约束。</span><span class="sxs-lookup"><span data-stu-id="f611b-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="f611b-122">框架与 URI 的其他部分（如主机名或查询参数）不匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="f611b-123">该框架选择与 URI 匹配的路由表中的第一个路由。</span><span class="sxs-lookup"><span data-stu-id="f611b-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="f611b-124">有两个特殊占位符： "{controller}" 和 "{action}"。</span><span class="sxs-lookup"><span data-stu-id="f611b-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="f611b-125">"{controller}" 提供控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="f611b-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="f611b-126">"{action}" 提供操作的名称。</span><span class="sxs-lookup"><span data-stu-id="f611b-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="f611b-127">在 Web API 中，通常会省略 "{action}"。</span><span class="sxs-lookup"><span data-stu-id="f611b-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="f611b-128">默认值</span><span class="sxs-lookup"><span data-stu-id="f611b-128">Defaults</span></span>

<span data-ttu-id="f611b-129">如果提供默认值，则路由将匹配缺少这些段的 URI。</span><span class="sxs-lookup"><span data-stu-id="f611b-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="f611b-130">例如:</span><span class="sxs-lookup"><span data-stu-id="f611b-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="f611b-131">Uri `http://localhost/api/products/all` 和 `http://localhost/api/products` 与前面的路由匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="f611b-132">在后一个 URI 中，将为缺少的 `{category}` 段指定默认值 `all`。</span><span class="sxs-lookup"><span data-stu-id="f611b-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="f611b-133">路由字典</span><span class="sxs-lookup"><span data-stu-id="f611b-133">Route Dictionary</span></span>

<span data-ttu-id="f611b-134">如果框架找到一个 URI 匹配项，则会创建一个包含每个占位符的值的字典。</span><span class="sxs-lookup"><span data-stu-id="f611b-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="f611b-135">键是占位符名称，不包括大括号。</span><span class="sxs-lookup"><span data-stu-id="f611b-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="f611b-136">值取自 URI 路径或默认值。</span><span class="sxs-lookup"><span data-stu-id="f611b-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="f611b-137">字典存储在**IHttpRouteData**对象中。</span><span class="sxs-lookup"><span data-stu-id="f611b-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="f611b-138">在此路由匹配阶段，将像处理其他占位符一样处理特殊的 "{controller}" 和 "{action}" 占位符。</span><span class="sxs-lookup"><span data-stu-id="f611b-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="f611b-139">它们只是与其他值一起存储在字典中。</span><span class="sxs-lookup"><span data-stu-id="f611b-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="f611b-140">默认值可以有特殊值**RouteParameter**。</span><span class="sxs-lookup"><span data-stu-id="f611b-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="f611b-141">如果为占位符分配了此值，则不会将该值添加到路由字典中。</span><span class="sxs-lookup"><span data-stu-id="f611b-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="f611b-142">例如:</span><span class="sxs-lookup"><span data-stu-id="f611b-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="f611b-143">对于 URI 路径 "api/products"，路由字典将包含：</span><span class="sxs-lookup"><span data-stu-id="f611b-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="f611b-144">控制器： "products"</span><span class="sxs-lookup"><span data-stu-id="f611b-144">controller: "products"</span></span>
- <span data-ttu-id="f611b-145">类别： "all"</span><span class="sxs-lookup"><span data-stu-id="f611b-145">category: "all"</span></span>

<span data-ttu-id="f611b-146">但对于 "api/products/玩具/123"，路由字典将包含：</span><span class="sxs-lookup"><span data-stu-id="f611b-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="f611b-147">控制器： "products"</span><span class="sxs-lookup"><span data-stu-id="f611b-147">controller: "products"</span></span>
- <span data-ttu-id="f611b-148">类别： "玩具"</span><span class="sxs-lookup"><span data-stu-id="f611b-148">category: "toys"</span></span>
- <span data-ttu-id="f611b-149">id： "123"</span><span class="sxs-lookup"><span data-stu-id="f611b-149">id: "123"</span></span>

<span data-ttu-id="f611b-150">默认值还可以包括未在路由模板中的任何位置显示的值。</span><span class="sxs-lookup"><span data-stu-id="f611b-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="f611b-151">如果路由匹配，则该值存储在字典中。</span><span class="sxs-lookup"><span data-stu-id="f611b-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="f611b-152">例如:</span><span class="sxs-lookup"><span data-stu-id="f611b-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="f611b-153">如果 URI 路径为 "api/root/8"，则字典将包含两个值：</span><span class="sxs-lookup"><span data-stu-id="f611b-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="f611b-154">控制器： "customers"</span><span class="sxs-lookup"><span data-stu-id="f611b-154">controller: "customers"</span></span>
- <span data-ttu-id="f611b-155">id： "8"</span><span class="sxs-lookup"><span data-stu-id="f611b-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="f611b-156">选择控制器</span><span class="sxs-lookup"><span data-stu-id="f611b-156">Selecting a Controller</span></span>

<span data-ttu-id="f611b-157">控制器选择由**IHttpControllerSelector. SelectController**方法处理。</span><span class="sxs-lookup"><span data-stu-id="f611b-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="f611b-158">此方法使用**HttpRequestMessage**实例并返回**HttpControllerDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="f611b-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="f611b-159">默认实现由**DefaultHttpControllerSelector**类提供。</span><span class="sxs-lookup"><span data-stu-id="f611b-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="f611b-160">此类使用简单的算法：</span><span class="sxs-lookup"><span data-stu-id="f611b-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="f611b-161">在路由字典中查找键 "controller"。</span><span class="sxs-lookup"><span data-stu-id="f611b-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="f611b-162">获取此键的值并附加字符串 "Controller" 以获取控制器类型名称。</span><span class="sxs-lookup"><span data-stu-id="f611b-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="f611b-163">查找具有此类型名称的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="f611b-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="f611b-164">例如，如果路由字典包含键值对 "controller" = "products"，则控制器类型为 "ProductsController"。</span><span class="sxs-lookup"><span data-stu-id="f611b-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="f611b-165">如果没有匹配的类型或多个匹配项，则该框架会向客户端返回一个错误。</span><span class="sxs-lookup"><span data-stu-id="f611b-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="f611b-166">对于步骤3， **DefaultHttpControllerSelector**使用**IHttpControllerTypeResolver**接口获取 Web API 控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="f611b-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="f611b-167">**IHttpControllerTypeResolver**的默认实现返回实现**IHttpController**的所有公共类（a），（b）不是抽象类，（c）的名称以 "Controller" 结尾。</span><span class="sxs-lookup"><span data-stu-id="f611b-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="f611b-168">操作选择</span><span class="sxs-lookup"><span data-stu-id="f611b-168">Action Selection</span></span>

<span data-ttu-id="f611b-169">选择控制器后，框架会通过调用**IHttpActionSelector. SelectAction**方法选择操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="f611b-170">此方法采用**system.web.http.controllers.httpcontrollercontext**并返回**HttpActionDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="f611b-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="f611b-171">默认实现由**ApiControllerActionSelector**类提供。</span><span class="sxs-lookup"><span data-stu-id="f611b-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="f611b-172">若要选择操作，请查看以下内容：</span><span class="sxs-lookup"><span data-stu-id="f611b-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="f611b-173">请求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f611b-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="f611b-174">路由模板中的 "{action}" 占位符（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="f611b-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="f611b-175">控制器上的操作的参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="f611b-176">在查看选择算法之前，我们需要了解有关控制器操作的一些内容。</span><span class="sxs-lookup"><span data-stu-id="f611b-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="f611b-177">**控制器上的哪些方法被视为 "操作"？**</span><span class="sxs-lookup"><span data-stu-id="f611b-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="f611b-178">选择操作时，框架仅查看控制器上的公共实例方法。</span><span class="sxs-lookup"><span data-stu-id="f611b-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="f611b-179">此外，它还不包括["特殊名称"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)方法（构造函数、事件、运算符重载等）以及从**ApiController**类继承的方法。</span><span class="sxs-lookup"><span data-stu-id="f611b-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="f611b-180">**HTTP 方法。**</span><span class="sxs-lookup"><span data-stu-id="f611b-180">**HTTP Methods.**</span></span> <span data-ttu-id="f611b-181">框架只选择与请求的 HTTP 方法匹配的操作，确定如下：</span><span class="sxs-lookup"><span data-stu-id="f611b-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="f611b-182">可以使用特性指定 HTTP 方法： **AcceptVerbs**、 **HttpDelete**、 **HttpGet**、 **HttpHead**、 **HttpOptions**、 **HttpPatch**、 **HttpPost**或**HttpPut**。</span><span class="sxs-lookup"><span data-stu-id="f611b-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="f611b-183">否则，如果控制器方法的名称以 "Get"、"Post"、"Put"、"Delete"、"Head"、"Options" 或 "Patch" 开头，则按照约定，操作支持该 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f611b-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="f611b-184">如果以上均不是，则该方法支持 POST。</span><span class="sxs-lookup"><span data-stu-id="f611b-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="f611b-185">**参数绑定。**</span><span class="sxs-lookup"><span data-stu-id="f611b-185">**Parameter Bindings.**</span></span> <span data-ttu-id="f611b-186">参数绑定是 Web API 为参数创建值的方式。</span><span class="sxs-lookup"><span data-stu-id="f611b-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="f611b-187">以下是参数绑定的默认规则：</span><span class="sxs-lookup"><span data-stu-id="f611b-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="f611b-188">简单类型是从 URI 获取的。</span><span class="sxs-lookup"><span data-stu-id="f611b-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="f611b-189">复杂类型取自请求正文。</span><span class="sxs-lookup"><span data-stu-id="f611b-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="f611b-190">简单类型包括所有[.NET Framework 基元类型](https://msdn.microsoft.com/library/system.type.isprimitive)，以及**DateTime**、 **Decimal**、 **Guid**、 **String**和**TimeSpan**。</span><span class="sxs-lookup"><span data-stu-id="f611b-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="f611b-191">对于每个操作，最多只能有一个参数读取请求正文。</span><span class="sxs-lookup"><span data-stu-id="f611b-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="f611b-192">可以重写默认的绑定规则。</span><span class="sxs-lookup"><span data-stu-id="f611b-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="f611b-193">请参阅[WebAPI 参数绑定](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f611b-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="f611b-194">此背景为操作选择算法。</span><span class="sxs-lookup"><span data-stu-id="f611b-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="f611b-195">在控制器上创建一个与 HTTP 请求方法匹配的所有操作的列表。</span><span class="sxs-lookup"><span data-stu-id="f611b-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="f611b-196">如果路由字典具有 "action" 条目，则删除名称与此值不匹配的操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="f611b-197">尝试将操作参数与 URI 匹配，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f611b-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="f611b-198">对于每个操作，获取作为简单类型的参数的列表，其中的绑定从 URI 获取参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="f611b-199">排除可选参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="f611b-200">从此列表中，尝试在路由字典或 URI 查询字符串中查找每个参数名称的匹配项。</span><span class="sxs-lookup"><span data-stu-id="f611b-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="f611b-201">匹配不区分大小写，也不依赖于参数顺序。</span><span class="sxs-lookup"><span data-stu-id="f611b-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="f611b-202">选择一个操作，其中列表中的每个参数在 URI 中都有匹配项。</span><span class="sxs-lookup"><span data-stu-id="f611b-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="f611b-203">如果有多个操作满足这些条件，则选择具有最多参数匹配项的操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="f611b-204">忽略带有 **[NonAction]** 属性的操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="f611b-205">步骤 #3 可能是最容易混淆的。</span><span class="sxs-lookup"><span data-stu-id="f611b-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="f611b-206">基本思路是，参数可以从 URI、请求正文或自定义绑定获取其值。</span><span class="sxs-lookup"><span data-stu-id="f611b-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="f611b-207">对于来自 URI 的参数，我们想要确保 URI 在路径（通过路由字典）或查询字符串中实际包含该参数的值。</span><span class="sxs-lookup"><span data-stu-id="f611b-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="f611b-208">例如，请考虑以下操作：</span><span class="sxs-lookup"><span data-stu-id="f611b-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="f611b-209">*Id*参数将绑定到 URI。</span><span class="sxs-lookup"><span data-stu-id="f611b-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="f611b-210">因此，此操作只能与包含 "id" 值的 URI 匹配，无论是在路由字典中还是在查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="f611b-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="f611b-211">可选参数是一个异常，因为这些参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="f611b-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="f611b-212">对于可选参数，如果绑定无法从 URI 获取值，则它是正常的。</span><span class="sxs-lookup"><span data-stu-id="f611b-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="f611b-213">复杂类型是一个不同原因的异常。</span><span class="sxs-lookup"><span data-stu-id="f611b-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="f611b-214">复杂类型只能通过自定义绑定绑定到 URI。</span><span class="sxs-lookup"><span data-stu-id="f611b-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="f611b-215">但在这种情况下，框架不会提前知道参数是否会绑定到特定的 URI。</span><span class="sxs-lookup"><span data-stu-id="f611b-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="f611b-216">若要确定，需要调用绑定。</span><span class="sxs-lookup"><span data-stu-id="f611b-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="f611b-217">选择算法的目标是在调用任何绑定之前从静态说明中选择操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="f611b-218">因此，复杂类型会从匹配算法中排除。</span><span class="sxs-lookup"><span data-stu-id="f611b-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="f611b-219">选择操作后，将调用所有参数绑定。</span><span class="sxs-lookup"><span data-stu-id="f611b-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="f611b-220">摘要:</span><span class="sxs-lookup"><span data-stu-id="f611b-220">Summary:</span></span>

- <span data-ttu-id="f611b-221">操作必须匹配请求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f611b-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="f611b-222">操作名称必须与路由字典中的 "action" 条目匹配（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="f611b-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="f611b-223">对于操作的每个参数，如果参数是从 URI 获取的，则必须在路由字典或 URI 查询字符串中找到参数名称。</span><span class="sxs-lookup"><span data-stu-id="f611b-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="f611b-224">（排除包含复杂类型的可选参数和参数。）</span><span class="sxs-lookup"><span data-stu-id="f611b-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="f611b-225">尝试匹配最多的参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="f611b-226">最佳匹配可能是不带参数的方法。</span><span class="sxs-lookup"><span data-stu-id="f611b-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="f611b-227">扩展示例</span><span class="sxs-lookup"><span data-stu-id="f611b-227">Extended Example</span></span>

<span data-ttu-id="f611b-228">到达</span><span class="sxs-lookup"><span data-stu-id="f611b-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="f611b-229">控制器:</span><span class="sxs-lookup"><span data-stu-id="f611b-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="f611b-230">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="f611b-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="f611b-231">路由匹配</span><span class="sxs-lookup"><span data-stu-id="f611b-231">Route Matching</span></span>

<span data-ttu-id="f611b-232">URI 与名为 "DefaultApi" 的路由匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="f611b-233">路由字典包含以下项：</span><span class="sxs-lookup"><span data-stu-id="f611b-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="f611b-234">控制器： "products"</span><span class="sxs-lookup"><span data-stu-id="f611b-234">controller: "products"</span></span>
- <span data-ttu-id="f611b-235">id： "1"</span><span class="sxs-lookup"><span data-stu-id="f611b-235">id: "1"</span></span>

<span data-ttu-id="f611b-236">路由字典不包含查询字符串参数 "版本" 和 "详细信息"，但在操作选择过程中仍会考虑这些参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="f611b-237">控制器选择</span><span class="sxs-lookup"><span data-stu-id="f611b-237">Controller Selection</span></span>

<span data-ttu-id="f611b-238">对于路由字典中的 "控制器" 条目，控制器类型为 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="f611b-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="f611b-239">操作选择</span><span class="sxs-lookup"><span data-stu-id="f611b-239">Action Selection</span></span>

<span data-ttu-id="f611b-240">HTTP 请求是一个 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="f611b-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="f611b-241">支持 GET 的控制器操作 `GetAll`、`GetById`和 `FindProductsByName`。</span><span class="sxs-lookup"><span data-stu-id="f611b-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="f611b-242">路由字典不包含 "action" 的条目，因此我们不需要与操作名称匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="f611b-243">接下来，我们尝试匹配操作的参数名称，仅查找 "获取" 操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="f611b-244">操作</span><span class="sxs-lookup"><span data-stu-id="f611b-244">Action</span></span> | <span data-ttu-id="f611b-245">要匹配的参数</span><span class="sxs-lookup"><span data-stu-id="f611b-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="f611b-246">无</span><span class="sxs-lookup"><span data-stu-id="f611b-246">none</span></span> |
| `GetById` | <span data-ttu-id="f611b-247">"id"</span><span class="sxs-lookup"><span data-stu-id="f611b-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="f611b-248">路径名</span><span class="sxs-lookup"><span data-stu-id="f611b-248">"name"</span></span> |

<span data-ttu-id="f611b-249">请注意，不会考虑 `GetById` 的*version*参数，因为它是一个可选参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="f611b-250">`GetAll` 方法与完全匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="f611b-251">`GetById` 方法也匹配，因为路由字典包含 "id"。</span><span class="sxs-lookup"><span data-stu-id="f611b-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="f611b-252">`FindProductsByName` 方法不匹配。</span><span class="sxs-lookup"><span data-stu-id="f611b-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="f611b-253">`GetById` 方法入选，因为它匹配一个参数，而不是 `GetAll`的参数。</span><span class="sxs-lookup"><span data-stu-id="f611b-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="f611b-254">方法是通过以下参数值调用的：</span><span class="sxs-lookup"><span data-stu-id="f611b-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="f611b-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="f611b-255">*id* = 1</span></span>
- <span data-ttu-id="f611b-256">*版本*= 1。5</span><span class="sxs-lookup"><span data-stu-id="f611b-256">*version* = 1.5</span></span>

<span data-ttu-id="f611b-257">请注意，尽管选择算法中未使用*版本*，但参数的值来自 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="f611b-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="f611b-258">扩展点</span><span class="sxs-lookup"><span data-stu-id="f611b-258">Extension Points</span></span>

<span data-ttu-id="f611b-259">Web API 为路由过程的某些部分提供扩展点。</span><span class="sxs-lookup"><span data-stu-id="f611b-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="f611b-260">接口</span><span class="sxs-lookup"><span data-stu-id="f611b-260">Interface</span></span> | <span data-ttu-id="f611b-261">说明</span><span class="sxs-lookup"><span data-stu-id="f611b-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f611b-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="f611b-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="f611b-263">选择控制器。</span><span class="sxs-lookup"><span data-stu-id="f611b-263">Selects the controller.</span></span> |
| <span data-ttu-id="f611b-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="f611b-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="f611b-265">获取控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="f611b-265">Gets the list of controller types.</span></span> <span data-ttu-id="f611b-266">**DefaultHttpControllerSelector**从此列表中选择控制器类型。</span><span class="sxs-lookup"><span data-stu-id="f611b-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="f611b-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="f611b-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="f611b-268">获取项目程序集的列表。</span><span class="sxs-lookup"><span data-stu-id="f611b-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="f611b-269">**IHttpControllerTypeResolver**接口使用此列表来查找控制器类型。</span><span class="sxs-lookup"><span data-stu-id="f611b-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="f611b-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="f611b-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="f611b-271">创建新的控制器实例。</span><span class="sxs-lookup"><span data-stu-id="f611b-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="f611b-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="f611b-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="f611b-273">选择操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-273">Selects the action.</span></span> |
| <span data-ttu-id="f611b-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="f611b-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="f611b-275">调用操作。</span><span class="sxs-lookup"><span data-stu-id="f611b-275">Invokes the action.</span></span> |

<span data-ttu-id="f611b-276">若要为这些接口提供自己的实现，请使用**HttpConfiguration**对象上的**服务**集合：</span><span class="sxs-lookup"><span data-stu-id="f611b-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
