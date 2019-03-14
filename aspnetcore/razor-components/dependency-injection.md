---
title: Razor 组件依赖关系注入
author: guardrex
description: 请参阅如何 Blazor 和 Razor 组件应用程序可以使用内置的服务，方法是让注入到组件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 6ce8fa74f20145f48797d267c20ef2593368b941
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042424"
---
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="18772-103">Razor 组件依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="18772-103">Razor Components dependency injection</span></span>

<span data-ttu-id="18772-104">通过[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="18772-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="18772-105">[依赖关系注入 (DI)](/aspnet/core/fundamentals/dependency-injection)已内置。</span><span class="sxs-lookup"><span data-stu-id="18772-105">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection) is built-in.</span></span> <span data-ttu-id="18772-106">应用可以使用内置的服务，方法是让注入到组件。</span><span class="sxs-lookup"><span data-stu-id="18772-106">Apps can use built-in services by having them injected into components.</span></span> <span data-ttu-id="18772-107">应用还可以定义自定义服务，并使其可通过 DI。</span><span class="sxs-lookup"><span data-stu-id="18772-107">Apps can also define custom services and make them available via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="18772-108">依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="18772-108">Dependency injection</span></span>

<span data-ttu-id="18772-109">DI 是一种技术用于访问在一个中心位置中配置的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="18772-110">这可以是适用于：</span><span class="sxs-lookup"><span data-stu-id="18772-110">This can be useful to:</span></span>

* <span data-ttu-id="18772-111">在多个组件之间共享单个服务类的实例 (称为*单独*服务)。</span><span class="sxs-lookup"><span data-stu-id="18772-111">Share a single instance of a service class across many components (known as a *singleton* service).</span></span>
* <span data-ttu-id="18772-112">分离特定的具体服务类中的组件，并仅引用抽象。</span><span class="sxs-lookup"><span data-stu-id="18772-112">Decouple components from particular concrete service classes and only reference abstractions.</span></span> <span data-ttu-id="18772-113">例如，一个接口`IDataAccess`由具体类实现`DataAccess`。</span><span class="sxs-lookup"><span data-stu-id="18772-113">For example, an interface `IDataAccess` is implemented by a concrete class `DataAccess`.</span></span> <span data-ttu-id="18772-114">当一个组件使用 DI 接收`IDataAccess`实现，该组件不耦合到具体类型。</span><span class="sxs-lookup"><span data-stu-id="18772-114">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="18772-115">可以交换实现，可能是到单元测试中的模拟实现。</span><span class="sxs-lookup"><span data-stu-id="18772-115">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="18772-116">DI 系统是负责向服务添加到组件的实例。</span><span class="sxs-lookup"><span data-stu-id="18772-116">The DI system is responsible for supplying instances of services to components.</span></span> <span data-ttu-id="18772-117">DI 还解析依赖项以递归方式，以便服务本身可以依赖于更多服务。</span><span class="sxs-lookup"><span data-stu-id="18772-117">DI also resolves dependencies recursively so that services themselves can depend on further services.</span></span> <span data-ttu-id="18772-118">在应用启动过程中配置 DI。</span><span class="sxs-lookup"><span data-stu-id="18772-118">DI is configured during startup of the app.</span></span> <span data-ttu-id="18772-119">本主题中后面是一个示例。</span><span class="sxs-lookup"><span data-stu-id="18772-119">An example is shown later in this topic.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="18772-120">将服务添加到 DI</span><span class="sxs-lookup"><span data-stu-id="18772-120">Add services to DI</span></span>

<span data-ttu-id="18772-121">创建新的应用程序之后, 检查`Startup.ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="18772-121">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="18772-122">`ConfigureServices`方法传递[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)，这是一系列服务描述符对象 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor))。</span><span class="sxs-lookup"><span data-stu-id="18772-122">The `ConfigureServices` method is passed an [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), which is a list of service descriptor objects ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span></span> <span data-ttu-id="18772-123">通过提供到服务集合的服务描述符添加服务。</span><span class="sxs-lookup"><span data-stu-id="18772-123">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="18772-124">下面的代码示例演示了这一概念：</span><span class="sxs-lookup"><span data-stu-id="18772-124">The following code sample demonstrates the concept:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="18772-125">可以使用以下生存期配置服务：</span><span class="sxs-lookup"><span data-stu-id="18772-125">Services can be configured with the following lifetimes:</span></span>

| <span data-ttu-id="18772-126">方法</span><span class="sxs-lookup"><span data-stu-id="18772-126">Method</span></span>      | <span data-ttu-id="18772-127">描述</span><span class="sxs-lookup"><span data-stu-id="18772-127">Description</span></span> |
| ----------- | ----------- |
| [<span data-ttu-id="18772-128">单例</span><span class="sxs-lookup"><span data-stu-id="18772-128">Singleton</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | <span data-ttu-id="18772-129">创建 DI*单个实例*的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-129">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="18772-130">需要此服务的所有组件都收到对此实例的引用。</span><span class="sxs-lookup"><span data-stu-id="18772-130">All components requiring this service receive a reference to this instance.</span></span> |
| [<span data-ttu-id="18772-131">暂时</span><span class="sxs-lookup"><span data-stu-id="18772-131">Transient</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | <span data-ttu-id="18772-132">一个组件需要此服务，每当它收到*新实例*的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-132">Whenever a component requires this service, it receives a *new instance* of the service.</span></span> |
| [<span data-ttu-id="18772-133">作用域（Scoped）</span><span class="sxs-lookup"><span data-stu-id="18772-133">Scoped</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | <span data-ttu-id="18772-134">客户端 Blazor 当前没有 DI 作用域的概念。</span><span class="sxs-lookup"><span data-stu-id="18772-134">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="18772-135">`Scoped` 行为类似于`Singleton`。</span><span class="sxs-lookup"><span data-stu-id="18772-135">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="18772-136">但是，ASP.NET Core Razor 组件支持`Scoped`生存期。</span><span class="sxs-lookup"><span data-stu-id="18772-136">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="18772-137">在 Razor 组件中，作用域内的服务注册的应用范围限定为该连接。</span><span class="sxs-lookup"><span data-stu-id="18772-137">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="18772-138">出于此原因，使用作用域的服务是首选的服务，应将范围设置为当前用户 (即使当前的目的是客户端运行在浏览器中)。</span><span class="sxs-lookup"><span data-stu-id="18772-138">For this reason, using scoped services is preferred for services that should be scoped to the current user (even if the current intent is to run client-side in the browser).</span></span> |

<span data-ttu-id="18772-139">DI 系统基于 ASP.NET Core 中的 DI 系统。</span><span class="sxs-lookup"><span data-stu-id="18772-139">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="18772-140">有关详细信息，请参阅[依赖关系注入在 ASP.NET Core 中的](/aspnet/core/fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="18772-140">For more information, see [Dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span></span>

## <a name="default-services"></a><span data-ttu-id="18772-141">默认服务</span><span class="sxs-lookup"><span data-stu-id="18772-141">Default services</span></span>

<span data-ttu-id="18772-142">默认服务自动添加到应用程序的服务集合中。</span><span class="sxs-lookup"><span data-stu-id="18772-142">Default services are automatically added to the service collection of an app.</span></span> <span data-ttu-id="18772-143">下表显示了一些有用的默认值提供的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-143">The following table shows some of the useful default services provided.</span></span>

| <span data-ttu-id="18772-144">方法</span><span class="sxs-lookup"><span data-stu-id="18772-144">Method</span></span>       | <span data-ttu-id="18772-145">描述</span><span class="sxs-lookup"><span data-stu-id="18772-145">Description</span></span> |
| ------------ | ----------- |
| [<span data-ttu-id="18772-146">HttpClient</span><span class="sxs-lookup"><span data-stu-id="18772-146">HttpClient</span></span>](/dotnet/api/system.net.http.httpclient) | <span data-ttu-id="18772-147">提供用于发送 HTTP 请求和从由 URI （单一实例） 所标识资源接收 HTTP 响应的方法。</span><span class="sxs-lookup"><span data-stu-id="18772-147">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="18772-148">请注意，此实例的`HttpClient`使用浏览器来处理在后台的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="18772-148">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="18772-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress)自动设置为应用程序的基本 URI 前缀。</span><span class="sxs-lookup"><span data-stu-id="18772-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="18772-150">`HttpClient` 仅提供给客户端 Blazor 应用。</span><span class="sxs-lookup"><span data-stu-id="18772-150">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="18772-151">表示调用可能会派遣到其中一个 JavaScript 运行时的一个实例。</span><span class="sxs-lookup"><span data-stu-id="18772-151">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="18772-152">有关详细信息，请参阅 <xref:razor-components/javascript-interop>。</span><span class="sxs-lookup"><span data-stu-id="18772-152">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="18772-153">适用于使用 Uri 和导航状态 （单一实例） 的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="18772-153">Helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="18772-154">`IUriHelper` 提供给这两个客户端 Blazor 和 ASP.NET Core Razor 组件应用。</span><span class="sxs-lookup"><span data-stu-id="18772-154">`IUriHelper` is provided to both client-side Blazor and ASP.NET Core Razor Components apps.</span></span> |

<span data-ttu-id="18772-155">请注意，可以使用自定义服务提供程序而不是默认服务提供程序添加的默认模板。</span><span class="sxs-lookup"><span data-stu-id="18772-155">Note that it is possible to use a custom services provider instead of the default service provider that's added by the default template.</span></span> <span data-ttu-id="18772-156">自定义服务提供程序不会自动提供表中列出的默认服务。</span><span class="sxs-lookup"><span data-stu-id="18772-156">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="18772-157">这些服务必须显式添加到新的服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="18772-157">Those services must be added to the new service provider explicitly.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="18772-158">请求中组件的服务</span><span class="sxs-lookup"><span data-stu-id="18772-158">Request a service in a component</span></span>

<span data-ttu-id="18772-159">一旦服务添加到服务集合，它们可以注入到组件的 Razor 模板中使用`@inject`Razor 指令。</span><span class="sxs-lookup"><span data-stu-id="18772-159">Once services are added to the service collection, they can be injected into the components' Razor templates using the `@inject` Razor directive.</span></span> <span data-ttu-id="18772-160">`@inject` 有两个参数：</span><span class="sxs-lookup"><span data-stu-id="18772-160">`@inject` has two parameters:</span></span>

* <span data-ttu-id="18772-161">类型名称：要插入的服务的类型。</span><span class="sxs-lookup"><span data-stu-id="18772-161">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="18772-162">属性名称：接收注入的应用服务的属性的名称。</span><span class="sxs-lookup"><span data-stu-id="18772-162">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="18772-163">请注意，该属性不需要手动创建。</span><span class="sxs-lookup"><span data-stu-id="18772-163">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="18772-164">编译器会创建该属性。</span><span class="sxs-lookup"><span data-stu-id="18772-164">The compiler creates the property.</span></span>

<span data-ttu-id="18772-165">多个`@inject`语句可用于插入不同的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-165">Multiple `@inject` statements can be used to inject different services.</span></span>

<span data-ttu-id="18772-166">下面的示例说明如何使用 `@inject`。</span><span class="sxs-lookup"><span data-stu-id="18772-166">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="18772-167">服务实现`Services.IDataAccess`注入到组件的属性`DataRepository`。</span><span class="sxs-lookup"><span data-stu-id="18772-167">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="18772-168">请注意，代码仅使用`IDataAccess`抽象：</span><span class="sxs-lookup"><span data-stu-id="18772-168">Note how the code is only using the `IDataAccess` abstraction:</span></span>

```csharp
@page "/customer-list"
@using Services
@inject IDataAccess DataRepository

<ul>
    @if (Customers != null)
    {
        @foreach (var customer in Customers)
        {
            <li>@customer.FirstName @customer.LastName</li>
        }
    }
</ul>

@functions {
    private IReadOnlyList<Customer> Customers;

    protected override async Task OnInitAsync()
    {
        // The property DataRepository received an implementation
        // of IDataAccess through dependency injection. Use 
        // DataRepository to obtain data from the server.
        Customers = await DataRepository.GetAllCustomersAsync();
    }
}
```

<span data-ttu-id="18772-169">在内部，则生成的属性 (`DataRepository`) 用修饰`InjectAttribute`属性。</span><span class="sxs-lookup"><span data-stu-id="18772-169">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="18772-170">通常情况下，此属性不是直接使用。</span><span class="sxs-lookup"><span data-stu-id="18772-170">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="18772-171">如果基类是所必需的组件和注入的属性也是必需的基类，`InjectAttribute`可以手动添加：</span><span class="sxs-lookup"><span data-stu-id="18772-171">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

```csharp
public class ComponentBase : BlazorComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

<span data-ttu-id="18772-172">在组件派生自的基类，`@inject`指令不是必需的。</span><span class="sxs-lookup"><span data-stu-id="18772-172">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="18772-173">`InjectAttribute`基类的足以：</span><span class="sxs-lookup"><span data-stu-id="18772-173">The `InjectAttribute` of the base class is sufficient:</span></span>

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="18772-174">在服务中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="18772-174">Dependency injection in services</span></span>

<span data-ttu-id="18772-175">复杂的服务可能需要其他服务。</span><span class="sxs-lookup"><span data-stu-id="18772-175">Complex services might require additional services.</span></span> <span data-ttu-id="18772-176">在前面的示例中，`DataAccess`可能需要`HttpClient`默认服务。</span><span class="sxs-lookup"><span data-stu-id="18772-176">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="18772-177">`@inject` 或`InjectAttribute`不能在服务中使用。</span><span class="sxs-lookup"><span data-stu-id="18772-177">`@inject` or the `InjectAttribute` can't be used in services.</span></span> <span data-ttu-id="18772-178">*构造函数注入*必须改为使用。</span><span class="sxs-lookup"><span data-stu-id="18772-178">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="18772-179">通过将参数添加到服务的构造函数会添加所需的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-179">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="18772-180">当依赖关系注入创建服务时，它认识到它需要在构造函数中，并相应地提供它们的服务。</span><span class="sxs-lookup"><span data-stu-id="18772-180">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

<span data-ttu-id="18772-181">下面的代码示例演示了这一概念：</span><span class="sxs-lookup"><span data-stu-id="18772-181">The following code sample demonstrates the concept:</span></span>

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
    ...
}
```

<span data-ttu-id="18772-182">请注意构造函数注入的以下先决条件：</span><span class="sxs-lookup"><span data-stu-id="18772-182">Note the following prerequisites for constructor injection:</span></span>

* <span data-ttu-id="18772-183">必须有该形参的实参可以所有满足通过依赖关系注入的一个构造函数。</span><span class="sxs-lookup"><span data-stu-id="18772-183">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="18772-184">请注意，如果为其指定默认值，则允许未涵盖的 DI 的其他参数。</span><span class="sxs-lookup"><span data-stu-id="18772-184">Note that additional parameters not covered by DI are allowed if default values are specified for them.</span></span>
* <span data-ttu-id="18772-185">适用的构造函数必须是*公共*。</span><span class="sxs-lookup"><span data-stu-id="18772-185">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="18772-186">必须仅有一个适用的构造函数。</span><span class="sxs-lookup"><span data-stu-id="18772-186">There must only be one applicable constructor.</span></span> <span data-ttu-id="18772-187">对于产生歧义，DI 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="18772-187">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18772-188">其他资源</span><span class="sxs-lookup"><span data-stu-id="18772-188">Additional resources</span></span>

* [<span data-ttu-id="18772-189">在 ASP.NET Core 中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="18772-189">Dependency injection in ASP.NET Core</span></span>](/aspnet/core/fundamentals/dependency-injection)
