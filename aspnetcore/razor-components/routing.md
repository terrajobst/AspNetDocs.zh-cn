---
title: 路由的 razor 组件
author: guardrex
description: 了解如何将请求路由在应用和有关 NavLink 组件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/01/2019
uid: razor-components/routing
ms.openlocfilehash: 5c648ba1bb3846f5baa515e808a98a3b33f81438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031604"
---
# <a name="razor-components-routing"></a><span data-ttu-id="1dfb3-103">路由的 razor 组件</span><span class="sxs-lookup"><span data-stu-id="1dfb3-103">Razor Components routing</span></span>

<span data-ttu-id="1dfb3-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="1dfb3-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="1dfb3-105">了解如何将请求路由在应用和有关 NavLink 组件。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-105">Learn how to route requests in apps and about the NavLink component.</span></span>

<span data-ttu-id="1dfb3-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)（[如何下载](xref:index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="1dfb3-107">有关先决条件，请参阅[入门](xref:razor-components/get-started)主题。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-107">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

## <a name="route-templates"></a><span data-ttu-id="1dfb3-108">路由模板</span><span class="sxs-lookup"><span data-stu-id="1dfb3-108">Route templates</span></span>

<span data-ttu-id="1dfb3-109">`<Router>`组件允许路由和路由模板提供给每个可访问的组件。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-109">The `<Router>` component enables routing, and a route template is provided to each accessible component.</span></span> <span data-ttu-id="1dfb3-110">`<Router>`部分显示在*App.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="1dfb3-110">The `<Router>` component appears in the *App.cshtml* file:</span></span>

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

<span data-ttu-id="1dfb3-111">当 *\*.cshtml*文件`@page`编译指令，则生成的类提供[RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute)指定路由模板。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-111">When a *\*.cshtml* file with an `@page` directive is compiled, the generated class is given a [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) specifying the route template.</span></span> <span data-ttu-id="1dfb3-112">在运行时，路由器将查看与组件类`RouteAttribute`并呈现任何组件有匹配的请求的 URL 的路由模板。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-112">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="1dfb3-113">多个路由模板可以应用于一个组件。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-113">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="1dfb3-114">在中[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)，以下组件响应的请求`/BlazorRoute`和`/DifferentBlazorRoute`。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-114">In the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), the following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`.</span></span>

<span data-ttu-id="1dfb3-115">*Pages/BlazorRoute.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1dfb3-115">*Pages/BlazorRoute.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

<span data-ttu-id="1dfb3-116">`<Router>` 支持设置呈现时请求的路由的回退组件进行解析。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-116">`<Router>` supports setting a fallback component for rendering when a requested route isn't resolved.</span></span> <span data-ttu-id="1dfb3-117">通过设置启用此选择加入方案`FallbackComponent`回退组件类的类型参数。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-117">Enable this opt-in scenario by setting the `FallbackComponent` parameter to the type of the fallback component class.</span></span>

<span data-ttu-id="1dfb3-118">下面的示例设置中定义的组件*Pages/MyFallbackRazorComponent.cshtml*是回退组件`<Router>`:</span><span class="sxs-lookup"><span data-stu-id="1dfb3-118">The following example sets a component defined in *Pages/MyFallbackRazorComponent.cshtml* as the fallback component for a `<Router>`:</span></span>

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> <span data-ttu-id="1dfb3-119">若要正确生成的路由，该应用程序必须包括`<base>`标记中的其*wwwroot/index.html*文件中指定的应用程序基路径`href`属性 (`<base href="/" />`)。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-119">To generate routes properly, the app must include a `<base>` tag in its *wwwroot/index.html* file with the app base path specified in the `href` attribute (`<base href="/" />`).</span></span> <span data-ttu-id="1dfb3-120">有关详细信息，请参阅[主机并将其部署：应用程序基路径](xref:host-and-deploy/razor-components/index#app-base-path)。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-120">For more information, see [Host and deploy: App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="route-parameters"></a><span data-ttu-id="1dfb3-121">路由参数</span><span class="sxs-lookup"><span data-stu-id="1dfb3-121">Route parameters</span></span>

<span data-ttu-id="1dfb3-122">路由器使用路由参数来填充相应的组件参数具有相同名称 （不区分大小写）。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-122">The router uses route parameters to populate the corresponding component parameters with the same name (case insensitive).</span></span>

<span data-ttu-id="1dfb3-123">*Pages/RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1dfb3-123">*Pages/RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

<span data-ttu-id="1dfb3-124">可选参数不受支持，因此两个`@page`指令收取在上面的示例。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-124">Optional parameters aren't supported yet, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="1dfb3-125">第一个可以导航到不带参数的组件。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-125">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="1dfb3-126">第二个`@page`指令采用`{text}`路由参数和值赋给`Text`属性。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-126">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="route-constraints"></a><span data-ttu-id="1dfb3-127">路由约束</span><span class="sxs-lookup"><span data-stu-id="1dfb3-127">Route constraints</span></span>

<span data-ttu-id="1dfb3-128">路由约束强制实施类型到一个组件路由段进行匹配。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-128">A route constraint enforces type matching on a route segment to a component.</span></span>

<span data-ttu-id="1dfb3-129">在以下示例中，如果只与匹配的路由到用户组件：</span><span class="sxs-lookup"><span data-stu-id="1dfb3-129">In the following example, the route to the Users component only matches if:</span></span>

* <span data-ttu-id="1dfb3-130">`Id`路由段是存在于请求 URL 上。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-130">An `Id` route segment is present on the request URL.</span></span>
* <span data-ttu-id="1dfb3-131">`Id`段是一个整数 (`int`)。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-131">The `Id` segment is an integer (`int`).</span></span>

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

<span data-ttu-id="1dfb3-132">下表中所示的路由约束是可供使用。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-132">The route constraints shown in the following table are available for use.</span></span> <span data-ttu-id="1dfb3-133">使用固定区域性匹配的路由约束，请参阅下表了解详细信息的警告。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-133">For the route constraints that match with the invariant culture, see the warning below the table for more information.</span></span>

| <span data-ttu-id="1dfb3-134">约束</span><span class="sxs-lookup"><span data-stu-id="1dfb3-134">Constraint</span></span> | <span data-ttu-id="1dfb3-135">示例</span><span class="sxs-lookup"><span data-stu-id="1dfb3-135">Example</span></span>           | <span data-ttu-id="1dfb3-136">匹配项示例</span><span class="sxs-lookup"><span data-stu-id="1dfb3-136">Example Matches</span></span>                                                                  | <span data-ttu-id="1dfb3-137">固定条件</span><span class="sxs-lookup"><span data-stu-id="1dfb3-137">Invariant</span></span><br><span data-ttu-id="1dfb3-138">区域性</span><span class="sxs-lookup"><span data-stu-id="1dfb3-138">culture</span></span><br><span data-ttu-id="1dfb3-139">匹配</span><span class="sxs-lookup"><span data-stu-id="1dfb3-139">matching</span></span> |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | <span data-ttu-id="1dfb3-140">`true`， `FALSE`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-140">`true`, `FALSE`</span></span>                                                                  | <span data-ttu-id="1dfb3-141">否</span><span class="sxs-lookup"><span data-stu-id="1dfb3-141">No</span></span>                               |
| `datetime` | `{dob:datetime}`  | <span data-ttu-id="1dfb3-142">`2016-12-31`， `2016-12-31 7:32pm`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-142">`2016-12-31`, `2016-12-31 7:32pm`</span></span>                                                | <span data-ttu-id="1dfb3-143">是</span><span class="sxs-lookup"><span data-stu-id="1dfb3-143">Yes</span></span>                              |
| `decimal`  | `{price:decimal}` | <span data-ttu-id="1dfb3-144">`49.99`， `-1,000.01`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-144">`49.99`, `-1,000.01`</span></span>                                                             | <span data-ttu-id="1dfb3-145">是</span><span class="sxs-lookup"><span data-stu-id="1dfb3-145">Yes</span></span>                              |
| `double`   | `{weight:double}` | <span data-ttu-id="1dfb3-146">`1.234`， `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-146">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="1dfb3-147">是</span><span class="sxs-lookup"><span data-stu-id="1dfb3-147">Yes</span></span>                              |
| `float`    | `{weight:float}`  | <span data-ttu-id="1dfb3-148">`1.234`， `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-148">`1.234`, `-1,001.01e8`</span></span>                                                           | <span data-ttu-id="1dfb3-149">是</span><span class="sxs-lookup"><span data-stu-id="1dfb3-149">Yes</span></span>                              |
| `guid`     | `{id:guid}`       | <span data-ttu-id="1dfb3-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`， `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-150">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span></span> | <span data-ttu-id="1dfb3-151">否</span><span class="sxs-lookup"><span data-stu-id="1dfb3-151">No</span></span>                               |
| `int`      | `{id:int}`        | <span data-ttu-id="1dfb3-152">`123456789`， `-123456789`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-152">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="1dfb3-153">是</span><span class="sxs-lookup"><span data-stu-id="1dfb3-153">Yes</span></span>                              |
| `long`     | `{ticks:long}`    | <span data-ttu-id="1dfb3-154">`123456789`， `-123456789`</span><span class="sxs-lookup"><span data-stu-id="1dfb3-154">`123456789`, `-123456789`</span></span>                                                        | <span data-ttu-id="1dfb3-155">是</span><span class="sxs-lookup"><span data-stu-id="1dfb3-155">Yes</span></span>                              |

> [!WARNING]
> <span data-ttu-id="1dfb3-156">验证 URL 的路由约束并将转换为始终使用固定区域性的 CLR 类型（例如 `int` 或 `DateTime`）。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-156">Route constraints that verify the URL and are converted to a CLR type (such as `int` or `DateTime`) always use the invariant culture.</span></span> <span data-ttu-id="1dfb3-157">这些约束假定 URL 不可本地化。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-157">These constraints assume that the URL is non-localizable.</span></span>

## <a name="navlink-component"></a><span data-ttu-id="1dfb3-158">NavLink 组件</span><span class="sxs-lookup"><span data-stu-id="1dfb3-158">NavLink component</span></span>

<span data-ttu-id="1dfb3-159">使用取代 HTML NavLink 组件 **\<>** 元素创建导航链接时。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-159">Use a NavLink component in place of HTML **\<a>** elements when creating navigation links.</span></span> <span data-ttu-id="1dfb3-160">NavLink 组件的行为类似于 **\<>** 元素，但它切换`active`CSS 类是否基于其`href`当前 URL 匹配。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-160">A NavLink component behaves like an **\<a>** element, except it toggles an `active` CSS class based on whether its `href` matches the current URL.</span></span> <span data-ttu-id="1dfb3-161">`active`类可帮助用户了解哪页不显示导航链接中的活动页面。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-161">The `active` class helps a user understand which page is the active page among the navigation links displayed.</span></span>

<span data-ttu-id="1dfb3-162">中的 NavMenu 组件[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)创建[Bootstrap](https://getbootstrap.com/docs/)演示了如何使用 NavLink 组件的导航栏。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-162">The NavMenu component in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) creates a [Bootstrap](https://getbootstrap.com/docs/) nav bar that demonstrates how to use NavLink components.</span></span> <span data-ttu-id="1dfb3-163">以下标记显示在前两个 NavLinks *Shared/NavMenu.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-163">The following markup shows the first two NavLinks in the *Shared/NavMenu.cshtml* file.</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

<span data-ttu-id="1dfb3-164">有两个`NavLinkMatch`选项：</span><span class="sxs-lookup"><span data-stu-id="1dfb3-164">There are two `NavLinkMatch` options:</span></span>

* <span data-ttu-id="1dfb3-165">`NavLinkMatch.All` &ndash; 指定，它与匹配整个当前 URL 时，NavLink 应处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-165">`NavLinkMatch.All` &ndash; Specifies that the NavLink should be active when it matches the entire current URL.</span></span>
* <span data-ttu-id="1dfb3-166">`NavLinkMatch.Prefix` &ndash; 指定，它与匹配的任何前缀的当前 URL 时，NavLink 应处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-166">`NavLinkMatch.Prefix` &ndash; Specifies that the NavLink should be active when it matches any prefix of the current URL.</span></span>

<span data-ttu-id="1dfb3-167">在前面的示例中，主页 NavLink (`href=""`) 匹配的所有 Url 并始终接收`active`CSS 类。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-167">In the preceding example, the Home NavLink (`href=""`) matches all URLs and always receives the `active` CSS class.</span></span> <span data-ttu-id="1dfb3-168">仅接收第二个 NavLink`active`类在用户访问 BlazorRoute 组件 (`href="BlazorRoute"`)。</span><span class="sxs-lookup"><span data-stu-id="1dfb3-168">The second NavLink only receives the `active` class when the user visits the BlazorRoute component (`href="BlazorRoute"`).</span></span>
