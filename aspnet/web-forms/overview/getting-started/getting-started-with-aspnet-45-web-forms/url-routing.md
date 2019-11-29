---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 路由 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590714"
---
# <a name="url-routing"></a><span data-ttu-id="051b8-103">URL 路由</span><span class="sxs-lookup"><span data-stu-id="051b8-103">URL Routing</span></span>

<span data-ttu-id="051b8-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="051b8-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="051b8-105">[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="051b8-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="051b8-106">本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="051b8-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="051b8-107">此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。</span><span class="sxs-lookup"><span data-stu-id="051b8-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="051b8-108">在本教程中，您将修改 Wingtip 玩具示例应用程序以支持 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="051b8-109">使用路由，你的 web 应用程序可以使用友好、更易于记住且更好的搜索引擎支持的 Url。</span><span class="sxs-lookup"><span data-stu-id="051b8-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="051b8-110">本教程基于前面的 "成员资格和管理" 教程，是 Wingtip 玩具教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="051b8-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="051b8-111">你将学习的内容：</span><span class="sxs-lookup"><span data-stu-id="051b8-111">What you'll learn:</span></span>

- <span data-ttu-id="051b8-112">如何注册 ASP.NET Web 窗体应用程序的路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="051b8-113">如何将路由添加到网页。</span><span class="sxs-lookup"><span data-stu-id="051b8-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="051b8-114">如何从数据库中选择数据以支持路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="051b8-115">ASP.NET 路由概述</span><span class="sxs-lookup"><span data-stu-id="051b8-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="051b8-116">使用 URL 路由，你可以将应用程序配置为接受不映射到物理文件的请求 Url。</span><span class="sxs-lookup"><span data-stu-id="051b8-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="051b8-117">请求 URL 只是用户在浏览器中输入的 URL，用于在您的网站上查找页面。</span><span class="sxs-lookup"><span data-stu-id="051b8-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="051b8-118">使用路由定义对用户具有语义意义的 Url，并可帮助搜索引擎优化（SEO）。</span><span class="sxs-lookup"><span data-stu-id="051b8-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="051b8-119">默认情况下，Web 窗体模板包括[ASP.NET 友好 url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)。</span><span class="sxs-lookup"><span data-stu-id="051b8-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="051b8-120">许多基本的路由工作都将使用*友好的 url*来实现。</span><span class="sxs-lookup"><span data-stu-id="051b8-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="051b8-121">但是，在本教程中，您将添加自定义的路由功能。</span><span class="sxs-lookup"><span data-stu-id="051b8-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="051b8-122">自定义 URL 路由之前，Wingtip 玩具示例应用程序可以使用以下 URL 链接到产品：</span><span class="sxs-lookup"><span data-stu-id="051b8-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="051b8-123">通过自定义 URL 路由，Wingtip 玩具示例应用程序将使用易于阅读的 URL 链接到同一产品：</span><span class="sxs-lookup"><span data-stu-id="051b8-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="051b8-124">路由</span><span class="sxs-lookup"><span data-stu-id="051b8-124">Routes</span></span>

<span data-ttu-id="051b8-125">路由是映射到处理程序的 URL 模式。</span><span class="sxs-lookup"><span data-stu-id="051b8-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="051b8-126">处理程序可以是物理文件，例如 Web 窗体应用程序中的 .aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="051b8-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="051b8-127">处理程序也可以是处理请求的类。</span><span class="sxs-lookup"><span data-stu-id="051b8-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="051b8-128">若要定义路由，可以通过指定 URL 模式、处理程序和（可选）路由名称来创建路由类的实例。</span><span class="sxs-lookup"><span data-stu-id="051b8-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="051b8-129">可以通过将 `Route` 对象添加到 `RouteTable` 类的静态 `Routes` 属性来向应用程序添加路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="051b8-130">路由属性是存储应用程序的所有路由的 `RouteCollection` 对象。</span><span class="sxs-lookup"><span data-stu-id="051b8-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="051b8-131">URL 模式</span><span class="sxs-lookup"><span data-stu-id="051b8-131">URL Patterns</span></span>

<span data-ttu-id="051b8-132">URL 模式可以包含文本值和变量占位符（称为 URL 参数）。</span><span class="sxs-lookup"><span data-stu-id="051b8-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="051b8-133">文本和占位符位于 URL 的段中，这些段用斜杠（`/`）字符分隔。</span><span class="sxs-lookup"><span data-stu-id="051b8-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="051b8-134">对 web 应用程序发出请求时，会将 URL 分析为段和占位符，并将变量值提供给请求处理程序。</span><span class="sxs-lookup"><span data-stu-id="051b8-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="051b8-135">此过程类似于分析查询字符串中的数据并将其传递给请求处理程序的方式。</span><span class="sxs-lookup"><span data-stu-id="051b8-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="051b8-136">在这两种情况下，变量信息都包含在 URL 中，并以键值对的形式传递给处理程序。</span><span class="sxs-lookup"><span data-stu-id="051b8-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="051b8-137">对于查询字符串，键和值都在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="051b8-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="051b8-138">对于路由，密钥是 URL 模式中定义的占位符名称，并且只有这些值位于 URL 中。</span><span class="sxs-lookup"><span data-stu-id="051b8-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="051b8-139">在 URL 模式中，可以通过将占位符括在大括号中来定义占位符（`{` 和 `}`）。</span><span class="sxs-lookup"><span data-stu-id="051b8-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="051b8-140">您可以在一个段中定义多个占位符，但占位符必须由文本值分隔。</span><span class="sxs-lookup"><span data-stu-id="051b8-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="051b8-141">例如，`{language}-{country}/{action}` 是有效的路由模式。</span><span class="sxs-lookup"><span data-stu-id="051b8-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="051b8-142">但 `{language}{country}/{action}` 不是有效的模式，因为占位符之间没有文本值或分隔符。</span><span class="sxs-lookup"><span data-stu-id="051b8-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="051b8-143">因此，路由不能确定从国家/地区占位符的值中将语言占位符的值隔开的位置。</span><span class="sxs-lookup"><span data-stu-id="051b8-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="051b8-144">映射和注册路由</span><span class="sxs-lookup"><span data-stu-id="051b8-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="051b8-145">在将路由添加到 Wingtip 玩具示例应用程序的页面之前，必须在应用程序启动时注册路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="051b8-146">若要注册路由，需要修改 `Application_Start` 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="051b8-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="051b8-147">在 Visual Studio**解决方案资源管理器**中，找到并打开*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="051b8-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="051b8-148">将黄色突出显示的代码添加到*Global.asax.cs*文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="051b8-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="051b8-149">当 Wingtip 玩具示例应用程序启动时，它将调用 `Application_Start` 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="051b8-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="051b8-150">在此事件处理程序结束时，将调用 `RegisterCustomRoutes` 方法。</span><span class="sxs-lookup"><span data-stu-id="051b8-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="051b8-151">`RegisterCustomRoutes` 方法通过调用 `RouteCollection` 对象的 `MapPageRoute` 方法添加每个路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="051b8-152">路由使用路由名称、路由 URL 和物理 URL 来定义。</span><span class="sxs-lookup"><span data-stu-id="051b8-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="051b8-153">第一个参数（"`ProductsByCategoryRoute`"）是路由名称。</span><span class="sxs-lookup"><span data-stu-id="051b8-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="051b8-154">它用于在需要时调用路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="051b8-155">第二个参数（"`Category/{categoryName}`"）定义友好的替换 URL，该 URL 可基于代码动态。</span><span class="sxs-lookup"><span data-stu-id="051b8-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="051b8-156">使用基于数据生成的链接填充数据控件时，可以使用此路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="051b8-157">路由如下所示：</span><span class="sxs-lookup"><span data-stu-id="051b8-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="051b8-158">路由的第二个参数包括由大括号（`{ }`）指定的动态值。</span><span class="sxs-lookup"><span data-stu-id="051b8-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="051b8-159">在这种情况下，`categoryName` 是将用于确定正确路由路径的变量。</span><span class="sxs-lookup"><span data-stu-id="051b8-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="051b8-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="051b8-160">**Optional**</span></span>
> 
> <span data-ttu-id="051b8-161">通过将 `RegisterCustomRoutes` 方法移动到单独的类中，你可能会发现管理代码更容易。</span><span class="sxs-lookup"><span data-stu-id="051b8-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="051b8-162">在*逻辑*文件夹中，创建一个单独的 `RouteActions` 类。</span><span class="sxs-lookup"><span data-stu-id="051b8-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="051b8-163">将上面的 `RegisterCustomRoutes` 方法从*Global.asax.cs*文件移到新的 `RoutesActions` 类中。</span><span class="sxs-lookup"><span data-stu-id="051b8-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="051b8-164">使用 `RoleActions` 类和 `createAdmin` 方法作为如何从*Global.asax.cs*文件调用 `RegisterCustomRoutes` 方法的示例。</span><span class="sxs-lookup"><span data-stu-id="051b8-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>

<span data-ttu-id="051b8-165">你还可能已注意到，在 `Application_Start` 事件处理程序的开头使用 `RouteConfig` 对象的 `RegisterRoutes` 方法调用。</span><span class="sxs-lookup"><span data-stu-id="051b8-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="051b8-166">此调用用于实现默认路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-166">This call is made to implement default routing.</span></span> <span data-ttu-id="051b8-167">当使用 Visual Studio 的 Web 窗体模板创建应用程序时，该应用程序作为默认代码包括。</span><span class="sxs-lookup"><span data-stu-id="051b8-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="051b8-168">检索和使用路由数据</span><span class="sxs-lookup"><span data-stu-id="051b8-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="051b8-169">如上所述，可以定义路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="051b8-170">添加到*Global.asax.cs*文件中 `Application_Start` 事件处理程序的代码将加载可定义的路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="051b8-171">设置路由</span><span class="sxs-lookup"><span data-stu-id="051b8-171">Setting Routes</span></span>

<span data-ttu-id="051b8-172">路由要求你添加更多代码。</span><span class="sxs-lookup"><span data-stu-id="051b8-172">Routes require you to add additional code.</span></span> <span data-ttu-id="051b8-173">在本教程中，您将使用模型绑定来检索使用数据控件中的数据生成路由时使用的 `RouteValueDictionary` 对象。</span><span class="sxs-lookup"><span data-stu-id="051b8-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="051b8-174">`RouteValueDictionary` 对象将包含属于特定产品类别的产品名称列表。</span><span class="sxs-lookup"><span data-stu-id="051b8-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="051b8-175">将基于数据和路由为每个产品创建一个链接。</span><span class="sxs-lookup"><span data-stu-id="051b8-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="051b8-176">启用类别和产品的路由</span><span class="sxs-lookup"><span data-stu-id="051b8-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="051b8-177">接下来，你将更新应用程序以使用 `ProductsByCategoryRoute` 来确定要为每个产品类别链接包含的正确路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="051b8-178">你还将更新*ProductList*页，以包含每个产品的路由链接。</span><span class="sxs-lookup"><span data-stu-id="051b8-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="051b8-179">链接将显示在更改之前，但链接现在将使用 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="051b8-180">在**解决方案资源管理器**中，打开 "*站点" 母版页*（如果尚未打开）。</span><span class="sxs-lookup"><span data-stu-id="051b8-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="051b8-181">用黄色突出显示的更改更新名为 "`categoryList`" 的**ListView**控件，使标记显示如下：</span><span class="sxs-lookup"><span data-stu-id="051b8-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="051b8-182">在**解决方案资源管理器**中，打开*ProductList*页。</span><span class="sxs-lookup"><span data-stu-id="051b8-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="051b8-183">更新*ProductList*页的 `ItemTemplate` 元素，其中的更新以黄色突出显示，使标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="051b8-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="051b8-184">打开*ProductList.aspx.cs*的代码隐藏，并添加以下具有黄色突出显示的命名空间：</span><span class="sxs-lookup"><span data-stu-id="051b8-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="051b8-185">将代码隐藏（*ProductList.aspx.cs*）的 `GetProducts` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="051b8-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="051b8-186">添加产品详细信息的代码</span><span class="sxs-lookup"><span data-stu-id="051b8-186">Add Code for Product Details</span></span>

<span data-ttu-id="051b8-187">现在，请更新*ProductDetails*页的代码隐藏（*ProductDetails.aspx.cs*）以使用路由数据。</span><span class="sxs-lookup"><span data-stu-id="051b8-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="051b8-188">请注意，新的 `GetProduct` 方法还接受查询字符串值，这种情况下，用户具有使用较旧的非路由 URL 作为书签的链接。</span><span class="sxs-lookup"><span data-stu-id="051b8-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="051b8-189">将代码隐藏（*ProductDetails.aspx.cs*）的 `GetProduct` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="051b8-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="051b8-190">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="051b8-190">Running the Application</span></span>

<span data-ttu-id="051b8-191">现在可以运行应用程序来查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="051b8-192">按**F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="051b8-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="051b8-193">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="051b8-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="051b8-194">单击页面顶部的 "**产品**" 链接。</span><span class="sxs-lookup"><span data-stu-id="051b8-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="051b8-195">所有产品都显示在*ProductList*页上。</span><span class="sxs-lookup"><span data-stu-id="051b8-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="051b8-196">将为浏览器显示以下 URL （使用端口号）：</span><span class="sxs-lookup"><span data-stu-id="051b8-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="051b8-197">接下来，单击页面顶部附近的 "**汽车**类别" 链接。</span><span class="sxs-lookup"><span data-stu-id="051b8-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="051b8-198">仅汽车显示在*ProductList*页上。</span><span class="sxs-lookup"><span data-stu-id="051b8-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="051b8-199">将为浏览器显示以下 URL （使用端口号）：</span><span class="sxs-lookup"><span data-stu-id="051b8-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="051b8-200">单击包含该页上列出的第一辆轿车名称的链接（"**转换汽车**"）以显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="051b8-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="051b8-201">将为浏览器显示以下 URL （使用端口号）：</span><span class="sxs-lookup"><span data-stu-id="051b8-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="051b8-202">接下来，在浏览器中输入以下非路由 URL （使用端口号）：</span><span class="sxs-lookup"><span data-stu-id="051b8-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="051b8-203">如果用户具有标记为书签的链接，则代码仍会识别包含查询字符串的 URL。</span><span class="sxs-lookup"><span data-stu-id="051b8-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="051b8-204">总结</span><span class="sxs-lookup"><span data-stu-id="051b8-204">Summary</span></span>

<span data-ttu-id="051b8-205">在本教程中，您已添加了类别和产品的路由。</span><span class="sxs-lookup"><span data-stu-id="051b8-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="051b8-206">您已经了解了如何将路由与使用模型绑定的数据控件集成。</span><span class="sxs-lookup"><span data-stu-id="051b8-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="051b8-207">在下一教程中，你将实现全局错误处理。</span><span class="sxs-lookup"><span data-stu-id="051b8-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="051b8-208">其他资源</span><span class="sxs-lookup"><span data-stu-id="051b8-208">Additional Resources</span></span>

[<span data-ttu-id="051b8-209">ASP.NET 友好 Url</span><span class="sxs-lookup"><span data-stu-id="051b8-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="051b8-210">使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="051b8-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="051b8-211">Microsoft Azure 免费试用版</span><span class="sxs-lookup"><span data-stu-id="051b8-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="051b8-212">[上一页](membership-and-administration.md)
> [下一页](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="051b8-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
