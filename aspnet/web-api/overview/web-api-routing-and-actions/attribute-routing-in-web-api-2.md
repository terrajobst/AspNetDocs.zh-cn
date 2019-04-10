---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: 属性路由在 ASP.NET Web API 2 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 65e2268418501f89a77a0ba20f7960a618c2e9b7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59405451"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="c78e1-102">ASP.NET Web API 2 中的属性路由</span><span class="sxs-lookup"><span data-stu-id="c78e1-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="c78e1-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c78e1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c78e1-104">*路由*是 Web API 如何匹配到某个操作的 URI。</span><span class="sxs-lookup"><span data-stu-id="c78e1-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="c78e1-105">Web API 2 支持一种新类型的路由，称为*的属性路由*。</span><span class="sxs-lookup"><span data-stu-id="c78e1-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="c78e1-106">顾名思义，属性路由使用属性定义的路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="c78e1-107">属性路由可以更好地控制 Uri 在你的 web API。</span><span class="sxs-lookup"><span data-stu-id="c78e1-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="c78e1-108">例如，您可以轻松创建描述层次结构的资源的 Uri。</span><span class="sxs-lookup"><span data-stu-id="c78e1-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="c78e1-109">早期样式的路由，名为基于约定的路由，但仍完全支持。</span><span class="sxs-lookup"><span data-stu-id="c78e1-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="c78e1-110">事实上，您可以组合在同一项目中的这两种技术。</span><span class="sxs-lookup"><span data-stu-id="c78e1-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="c78e1-111">本主题演示如何启用属性路由并描述了各种选项的属性路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="c78e1-112">有关使用属性路由的端到端教程，请参阅[使用 Web API 2 中的属性路由创建 REST API](create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="c78e1-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c78e1-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="c78e1-113">Prerequisites</span></span>

<span data-ttu-id="c78e1-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、 Professional 或 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="c78e1-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="c78e1-115">或者，使用 NuGet 包管理器安装所需的包。</span><span class="sxs-lookup"><span data-stu-id="c78e1-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="c78e1-116">从**工具**在 Visual Studio 中，选择菜单**NuGet 包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="c78e1-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="c78e1-117">在包管理器控制台窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="c78e1-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="c78e1-118">为什么属性路由？</span><span class="sxs-lookup"><span data-stu-id="c78e1-118">Why Attribute Routing?</span></span>

<span data-ttu-id="c78e1-119">使用 Web API 的第一版*基于约定的*路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="c78e1-120">在该类型的路由，则定义一个或多个路由模板，它们基本上是参数化字符串。</span><span class="sxs-lookup"><span data-stu-id="c78e1-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="c78e1-121">当框架收到请求时，它可匹配与路由模板的 URI。</span><span class="sxs-lookup"><span data-stu-id="c78e1-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="c78e1-122">(有关基于约定的路由的详细信息，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c78e1-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="c78e1-123">基于约定的路由的一个优点是在单个位置，定义模板，并路由规则一致地应用于所有控制器。</span><span class="sxs-lookup"><span data-stu-id="c78e1-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="c78e1-124">遗憾的是，基于约定的路由会难以支持某些 URI 模式常用于 RESTful Api。</span><span class="sxs-lookup"><span data-stu-id="c78e1-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="c78e1-125">例如，资源通常包含子资源：客户下了订单、 电影具有参与者、 丛书有作者，等等。</span><span class="sxs-lookup"><span data-stu-id="c78e1-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="c78e1-126">很自然地创建反映这些关系的 Uri:</span><span class="sxs-lookup"><span data-stu-id="c78e1-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="c78e1-127">此类型的 URI 很难创建使用基于约定的路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="c78e1-128">尽管可以完成，结果不能扩展，如果有多个控制器或资源类型。</span><span class="sxs-lookup"><span data-stu-id="c78e1-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="c78e1-129">属性路由中，它就很简单，此 uri 定义路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="c78e1-130">您只需将属性添加到控制器操作：</span><span class="sxs-lookup"><span data-stu-id="c78e1-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="c78e1-131">以下是一些其他路由使简单的模式。</span><span class="sxs-lookup"><span data-stu-id="c78e1-131">Here are some other patterns that attribute routing makes easy.</span></span>

**<span data-ttu-id="c78e1-132">API 版本控制</span><span class="sxs-lookup"><span data-stu-id="c78e1-132">API versioning</span></span>**

<span data-ttu-id="c78e1-133">在此示例中，"/ api/v1/产品"将路由到控制器不同"/ api/v2/产品"。</span><span class="sxs-lookup"><span data-stu-id="c78e1-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

**<span data-ttu-id="c78e1-134">重载的 URI 段</span><span class="sxs-lookup"><span data-stu-id="c78e1-134">Overloaded URI segments</span></span>**

<span data-ttu-id="c78e1-135">在此示例中，"1"是订单号，但是"挂起"映射到集合。</span><span class="sxs-lookup"><span data-stu-id="c78e1-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

**<span data-ttu-id="c78e1-136">多个参数类型</span><span class="sxs-lookup"><span data-stu-id="c78e1-136">Multiple parameter types</span></span>**

<span data-ttu-id="c78e1-137">在此示例中，"1"是订单号，但指定一个日期，"2013年/06/16"。</span><span class="sxs-lookup"><span data-stu-id="c78e1-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="c78e1-138">启用属性路由</span><span class="sxs-lookup"><span data-stu-id="c78e1-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="c78e1-139">若要启用的属性路由，请调用**MapHttpAttributeRoutes**在配置过程。</span><span class="sxs-lookup"><span data-stu-id="c78e1-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="c78e1-140">此扩展方法中定义**System.Web.Http.HttpConfigurationExtensions**类。</span><span class="sxs-lookup"><span data-stu-id="c78e1-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="c78e1-141">属性路由可以与组合[基于约定的](routing-in-aspnet-web-api.md)路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="c78e1-142">若要定义基于约定的路由，请调用**MapHttpRoute**方法。</span><span class="sxs-lookup"><span data-stu-id="c78e1-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="c78e1-143">有关配置 Web API 的详细信息，请参阅[配置 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c78e1-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="c78e1-144">注意:从 Web API 1 迁移</span><span class="sxs-lookup"><span data-stu-id="c78e1-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="c78e1-145">在 Web API 2 之前的 Web API 项目模板生成的代码如下：</span><span class="sxs-lookup"><span data-stu-id="c78e1-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="c78e1-146">如果启用属性路由，则此代码将引发异常。</span><span class="sxs-lookup"><span data-stu-id="c78e1-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="c78e1-147">如果升级现有的 Web API 项目，以使用属性路由，请务必更新此配置代码所示：</span><span class="sxs-lookup"><span data-stu-id="c78e1-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="c78e1-148">有关详细信息，请参阅[配置与 ASP.NET 托管的 Web API](../advanced/configuring-aspnet-web-api.md#webhost)。</span><span class="sxs-lookup"><span data-stu-id="c78e1-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>


<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="c78e1-149">添加路由属性</span><span class="sxs-lookup"><span data-stu-id="c78e1-149">Adding Route Attributes</span></span>

<span data-ttu-id="c78e1-150">下面是路由的使用属性定义的示例：</span><span class="sxs-lookup"><span data-stu-id="c78e1-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="c78e1-151">将字符串&quot;客户 / {customerId} orders&quot;是用于路由的 URI 模板。</span><span class="sxs-lookup"><span data-stu-id="c78e1-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="c78e1-152">Web API 会尝试匹配请求 URI 的模板。</span><span class="sxs-lookup"><span data-stu-id="c78e1-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="c78e1-153">在此示例中，"客户"和"orders"文本段，并且在"{customerId}"是一个变量参数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="c78e1-154">下面的 Uri 与此模板相匹配：</span><span class="sxs-lookup"><span data-stu-id="c78e1-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="c78e1-155">你可以限制通过匹配[约束](#constraints)，本主题后面所述。</span><span class="sxs-lookup"><span data-stu-id="c78e1-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="c78e1-156">请注意， &quot;{customerId}&quot;路由模板中的参数的名称匹配*customerId*方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="c78e1-157">当 Web API 调用的控制器操作时，它会将路由参数绑定。</span><span class="sxs-lookup"><span data-stu-id="c78e1-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="c78e1-158">例如，如果 URI 是`http://example.com/customers/1/orders`，Web API 将尝试绑定的值"1"向*customerId*操作中的参数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="c78e1-159">URI 模板可以具有多个参数：</span><span class="sxs-lookup"><span data-stu-id="c78e1-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="c78e1-160">路由属性不具有任何控制器方法使用基于约定的路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="c78e1-161">这样一来，您可以组合这两种类型的同一个项目中的路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c78e1-162">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="c78e1-162">HTTP Methods</span></span>

<span data-ttu-id="c78e1-163">Web API 还将选择操作请求 （GET、 POST 等） 的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="c78e1-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="c78e1-164">默认情况下，Web API 将查找与控制器方法名称的开头的不区分大小写匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="c78e1-165">例如，名为的控制器方法`PutCustomers`匹配 HTTP PUT 请求。</span><span class="sxs-lookup"><span data-stu-id="c78e1-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="c78e1-166">以下属性来修饰的方法与任何替代此约定：</span><span class="sxs-lookup"><span data-stu-id="c78e1-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- **<span data-ttu-id="c78e1-167">[HttpDelete]</span><span class="sxs-lookup"><span data-stu-id="c78e1-167">[HttpDelete]</span></span>**
- **<span data-ttu-id="c78e1-168">[HttpGet]</span><span class="sxs-lookup"><span data-stu-id="c78e1-168">[HttpGet]</span></span>**
- **<span data-ttu-id="c78e1-169">[HttpHead]</span><span class="sxs-lookup"><span data-stu-id="c78e1-169">[HttpHead]</span></span>**
- **<span data-ttu-id="c78e1-170">[HttpOptions]</span><span class="sxs-lookup"><span data-stu-id="c78e1-170">[HttpOptions]</span></span>**
- **<span data-ttu-id="c78e1-171">[HttpPatch]</span><span class="sxs-lookup"><span data-stu-id="c78e1-171">[HttpPatch]</span></span>**
- **<span data-ttu-id="c78e1-172">[HttpPost]</span><span class="sxs-lookup"><span data-stu-id="c78e1-172">[HttpPost]</span></span>**
- **<span data-ttu-id="c78e1-173">[HttpPut]</span><span class="sxs-lookup"><span data-stu-id="c78e1-173">[HttpPut]</span></span>**

<span data-ttu-id="c78e1-174">下面的示例将 CreateBook 方法映射到 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="c78e1-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="c78e1-175">对于所有其他 HTTP 方法，包括非标准的方法，使用**AcceptVerbs**属性，它使用的 HTTP 方法列表。</span><span class="sxs-lookup"><span data-stu-id="c78e1-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="c78e1-176">路由前缀</span><span class="sxs-lookup"><span data-stu-id="c78e1-176">Route Prefixes</span></span>

<span data-ttu-id="c78e1-177">通常情况下，所有以相同前缀开头的控制器中路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="c78e1-178">例如：</span><span class="sxs-lookup"><span data-stu-id="c78e1-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="c78e1-179">可以通过使用针对整个控制器设置公共前缀 **[RoutePrefix]** 属性：</span><span class="sxs-lookup"><span data-stu-id="c78e1-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="c78e1-180">使用 method 属性上颚化符 （~） 重写的路由前缀：</span><span class="sxs-lookup"><span data-stu-id="c78e1-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="c78e1-181">路由前缀可以包含参数：</span><span class="sxs-lookup"><span data-stu-id="c78e1-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="c78e1-182">路由约束</span><span class="sxs-lookup"><span data-stu-id="c78e1-182">Route Constraints</span></span>

<span data-ttu-id="c78e1-183">路由约束让你限制如何匹配路由模板中的参数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="c78e1-184">常规语法&quot;{参数： 约束}&quot;。</span><span class="sxs-lookup"><span data-stu-id="c78e1-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="c78e1-185">例如：</span><span class="sxs-lookup"><span data-stu-id="c78e1-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="c78e1-186">在这里，第一个路由将仅选择如果&quot;id&quot; URI 段是一个整数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="c78e1-187">否则，将选择第二个路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="c78e1-188">下表列出了支持的约束。</span><span class="sxs-lookup"><span data-stu-id="c78e1-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="c78e1-189">约束</span><span class="sxs-lookup"><span data-stu-id="c78e1-189">Constraint</span></span> | <span data-ttu-id="c78e1-190">描述</span><span class="sxs-lookup"><span data-stu-id="c78e1-190">Description</span></span> | <span data-ttu-id="c78e1-191">示例</span><span class="sxs-lookup"><span data-stu-id="c78e1-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c78e1-192">alpha</span><span class="sxs-lookup"><span data-stu-id="c78e1-192">alpha</span></span> | <span data-ttu-id="c78e1-193">匹配大写或小写字符 (-z、 A-Z)</span><span class="sxs-lookup"><span data-stu-id="c78e1-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="c78e1-194">{x: alpha}</span><span class="sxs-lookup"><span data-stu-id="c78e1-194">{x:alpha}</span></span> |
| <span data-ttu-id="c78e1-195">bool</span><span class="sxs-lookup"><span data-stu-id="c78e1-195">bool</span></span> | <span data-ttu-id="c78e1-196">匹配一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-196">Matches a Boolean value.</span></span> | <span data-ttu-id="c78e1-197">{x: bool}</span><span class="sxs-lookup"><span data-stu-id="c78e1-197">{x:bool}</span></span> |
| <span data-ttu-id="c78e1-198">datetime</span><span class="sxs-lookup"><span data-stu-id="c78e1-198">datetime</span></span> | <span data-ttu-id="c78e1-199">匹配项**DateTime**值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="c78e1-200">{x: datetime}</span><span class="sxs-lookup"><span data-stu-id="c78e1-200">{x:datetime}</span></span> |
| <span data-ttu-id="c78e1-201">decimal</span><span class="sxs-lookup"><span data-stu-id="c78e1-201">decimal</span></span> | <span data-ttu-id="c78e1-202">匹配十进制值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-202">Matches a decimal value.</span></span> | <span data-ttu-id="c78e1-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="c78e1-203">{x:decimal}</span></span> |
| <span data-ttu-id="c78e1-204">double</span><span class="sxs-lookup"><span data-stu-id="c78e1-204">double</span></span> | <span data-ttu-id="c78e1-205">与 64 位浮点值匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="c78e1-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="c78e1-206">{x:double}</span></span> |
| <span data-ttu-id="c78e1-207">float</span><span class="sxs-lookup"><span data-stu-id="c78e1-207">float</span></span> | <span data-ttu-id="c78e1-208">与 32 位浮点值匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="c78e1-209">{x: float}</span><span class="sxs-lookup"><span data-stu-id="c78e1-209">{x:float}</span></span> |
| <span data-ttu-id="c78e1-210">guid</span><span class="sxs-lookup"><span data-stu-id="c78e1-210">guid</span></span> | <span data-ttu-id="c78e1-211">匹配的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-211">Matches a GUID value.</span></span> | <span data-ttu-id="c78e1-212">{x: guid}</span><span class="sxs-lookup"><span data-stu-id="c78e1-212">{x:guid}</span></span> |
| <span data-ttu-id="c78e1-213">int</span><span class="sxs-lookup"><span data-stu-id="c78e1-213">int</span></span> | <span data-ttu-id="c78e1-214">与 32 位整数值匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="c78e1-215">{x: int}</span><span class="sxs-lookup"><span data-stu-id="c78e1-215">{x:int}</span></span> |
| <span data-ttu-id="c78e1-216">length</span><span class="sxs-lookup"><span data-stu-id="c78e1-216">length</span></span> | <span data-ttu-id="c78e1-217">与具有指定长度或长度的指定范围内的字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="c78e1-218">{x:length(6)} {x:length(1,20)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="c78e1-219">long</span><span class="sxs-lookup"><span data-stu-id="c78e1-219">long</span></span> | <span data-ttu-id="c78e1-220">与 64 位整数值匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="c78e1-221">{x： 长时间}</span><span class="sxs-lookup"><span data-stu-id="c78e1-221">{x:long}</span></span> |
| <span data-ttu-id="c78e1-222">max</span><span class="sxs-lookup"><span data-stu-id="c78e1-222">max</span></span> | <span data-ttu-id="c78e1-223">匹配一个整数，其最大值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="c78e1-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-224">{x:max(10)}</span></span> |
| <span data-ttu-id="c78e1-225">maxlength</span><span class="sxs-lookup"><span data-stu-id="c78e1-225">maxlength</span></span> | <span data-ttu-id="c78e1-226">与最大长度的字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="c78e1-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="c78e1-228">min</span><span class="sxs-lookup"><span data-stu-id="c78e1-228">min</span></span> | <span data-ttu-id="c78e1-229">匹配一个整数，其最小值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="c78e1-230">{x: min(10)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-230">{x:min(10)}</span></span> |
| <span data-ttu-id="c78e1-231">minlength</span><span class="sxs-lookup"><span data-stu-id="c78e1-231">minlength</span></span> | <span data-ttu-id="c78e1-232">与最小长度的字符串相匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="c78e1-233">{x: minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="c78e1-234">range</span><span class="sxs-lookup"><span data-stu-id="c78e1-234">range</span></span> | <span data-ttu-id="c78e1-235">一个整数值的范围内的匹配项。</span><span class="sxs-lookup"><span data-stu-id="c78e1-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="c78e1-236">{x: range(10,50)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="c78e1-237">正则表达式</span><span class="sxs-lookup"><span data-stu-id="c78e1-237">regex</span></span> | <span data-ttu-id="c78e1-238">与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="c78e1-238">Matches a regular expression.</span></span> | <span data-ttu-id="c78e1-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="c78e1-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="c78e1-240">请注意，某些约束，如&quot;min&quot;，在括号中采用自变量。</span><span class="sxs-lookup"><span data-stu-id="c78e1-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="c78e1-241">可以将多个约束应用于参数，用冒号分隔。</span><span class="sxs-lookup"><span data-stu-id="c78e1-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="c78e1-242">自定义路由约束</span><span class="sxs-lookup"><span data-stu-id="c78e1-242">Custom Route Constraints</span></span>

<span data-ttu-id="c78e1-243">您可以通过实现来创建自定义路由约束**IHttpRouteConstraint**接口。</span><span class="sxs-lookup"><span data-stu-id="c78e1-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="c78e1-244">例如，以下限制将限制为非零的整数值的参数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="c78e1-245">下面的代码演示如何注册该约束：</span><span class="sxs-lookup"><span data-stu-id="c78e1-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="c78e1-246">现在可以将约束应用在路由中：</span><span class="sxs-lookup"><span data-stu-id="c78e1-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="c78e1-247">也可以替换整个**DefaultInlineConstraintResolver**类的实现**IInlineConstraintResolver**接口。</span><span class="sxs-lookup"><span data-stu-id="c78e1-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="c78e1-248">执行此操作将替换的所有内置的约束，除非你的实现**IInlineConstraintResolver**专门将它们添加。</span><span class="sxs-lookup"><span data-stu-id="c78e1-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="c78e1-249">可选 URI 参数和默认值</span><span class="sxs-lookup"><span data-stu-id="c78e1-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="c78e1-250">可以通过将问号添加到路由参数，使 URI 参数可选。</span><span class="sxs-lookup"><span data-stu-id="c78e1-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="c78e1-251">如果某个路由参数是可选的则必须定义方法参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="c78e1-252">在此示例中，`/api/books/locale/1033`和`/api/books/locale`返回相同的资源。</span><span class="sxs-lookup"><span data-stu-id="c78e1-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="c78e1-253">或者，可以指定在路由模板中，默认值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c78e1-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="c78e1-254">这是上一示例中，几乎相同，但没有行为的细微的差别在于时应用的默认值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="c78e1-255">在第一个示例 ("{lcid:int？}") 中，1033年的默认值是直接分配给方法参数，因此该参数会将此确切值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="c78e1-256">在第二个示例 ("{lcid:int = 1033年}")，"1033"的默认值都通过模型绑定过程。</span><span class="sxs-lookup"><span data-stu-id="c78e1-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="c78e1-257">默认模型联编程序会将数字值 1033年为"1033"。</span><span class="sxs-lookup"><span data-stu-id="c78e1-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="c78e1-258">但是，您可以插入自定义模型联编程序，这可能会执行一些不同。</span><span class="sxs-lookup"><span data-stu-id="c78e1-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="c78e1-259">（在大多数情况下，除非你有自定义模型绑定器在管道中的两种形式将等效。）</span><span class="sxs-lookup"><span data-stu-id="c78e1-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="c78e1-260">路由名称</span><span class="sxs-lookup"><span data-stu-id="c78e1-260">Route Names</span></span>

<span data-ttu-id="c78e1-261">在 Web API 中，每个路由都有一个名称。</span><span class="sxs-lookup"><span data-stu-id="c78e1-261">In Web API, every route has a name.</span></span> <span data-ttu-id="c78e1-262">路由名称可用于生成链接，以便可以在 HTTP 响应中包含一个链接。</span><span class="sxs-lookup"><span data-stu-id="c78e1-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="c78e1-263">若要指定路由名称，设置**名称**特性的属性。</span><span class="sxs-lookup"><span data-stu-id="c78e1-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="c78e1-264">下面的示例演示如何设置路由名称，以及如何生成一个链接时使用的路由名称。</span><span class="sxs-lookup"><span data-stu-id="c78e1-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="c78e1-265">路由顺序</span><span class="sxs-lookup"><span data-stu-id="c78e1-265">Route Order</span></span>

<span data-ttu-id="c78e1-266">当框架尝试匹配与路由的 URI 时，它会评估按特定顺序的路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="c78e1-267">若要指定的顺序，将设置**顺序**路由属性上的属性。</span><span class="sxs-lookup"><span data-stu-id="c78e1-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="c78e1-268">首先计算较低的值。</span><span class="sxs-lookup"><span data-stu-id="c78e1-268">Lower values are evaluated first.</span></span> <span data-ttu-id="c78e1-269">默认顺序值为零。</span><span class="sxs-lookup"><span data-stu-id="c78e1-269">The default order value is zero.</span></span>

<span data-ttu-id="c78e1-270">下面是如何确定总排序：</span><span class="sxs-lookup"><span data-stu-id="c78e1-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="c78e1-271">比较**顺序**路由属性的属性。</span><span class="sxs-lookup"><span data-stu-id="c78e1-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="c78e1-272">查看路由模板中的每个 URI 段。</span><span class="sxs-lookup"><span data-stu-id="c78e1-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="c78e1-273">为每个段进行排序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c78e1-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="c78e1-274">文本段。</span><span class="sxs-lookup"><span data-stu-id="c78e1-274">Literal segments.</span></span>
    2. <span data-ttu-id="c78e1-275">将路由参数的约束。</span><span class="sxs-lookup"><span data-stu-id="c78e1-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="c78e1-276">不受限制的路由参数。</span><span class="sxs-lookup"><span data-stu-id="c78e1-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="c78e1-277">通配符参数具有约束的段。</span><span class="sxs-lookup"><span data-stu-id="c78e1-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="c78e1-278">通配符参数不受限制的段。</span><span class="sxs-lookup"><span data-stu-id="c78e1-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="c78e1-279">对于一个路由排序不区分大小写的序号字符串比较 ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) 的路由模板。</span><span class="sxs-lookup"><span data-stu-id="c78e1-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="c78e1-280">这是一个示例。</span><span class="sxs-lookup"><span data-stu-id="c78e1-280">Here is an example.</span></span> <span data-ttu-id="c78e1-281">假设定义以下控制器：</span><span class="sxs-lookup"><span data-stu-id="c78e1-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="c78e1-282">这些路由排序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c78e1-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="c78e1-283">orders/details</span><span class="sxs-lookup"><span data-stu-id="c78e1-283">orders/details</span></span>
2. <span data-ttu-id="c78e1-284">orders/{id}</span><span class="sxs-lookup"><span data-stu-id="c78e1-284">orders/{id}</span></span>
3. <span data-ttu-id="c78e1-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="c78e1-285">orders/{customerName}</span></span>
4. <span data-ttu-id="c78e1-286">orders/{\*date}</span><span class="sxs-lookup"><span data-stu-id="c78e1-286">orders/{\*date}</span></span>
5. <span data-ttu-id="c78e1-287">orders/pending</span><span class="sxs-lookup"><span data-stu-id="c78e1-287">orders/pending</span></span>

<span data-ttu-id="c78e1-288">请注意"详细信息"是一个文本段和出现之前"{id}"，但"挂起"会显示上一次由于**顺序**属性为 1。</span><span class="sxs-lookup"><span data-stu-id="c78e1-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="c78e1-289">(本示例假定那里没有客户名为"详细信息"或"挂起"。</span><span class="sxs-lookup"><span data-stu-id="c78e1-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="c78e1-290">一般情况下，尝试避免不明确的路由。</span><span class="sxs-lookup"><span data-stu-id="c78e1-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="c78e1-291">在此示例中，更好的路由模板`GetByCustomer`是"客户 / {customerName}")</span><span class="sxs-lookup"><span data-stu-id="c78e1-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
