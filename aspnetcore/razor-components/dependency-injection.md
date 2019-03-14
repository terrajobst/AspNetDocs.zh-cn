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
# <a name="razor-components-dependency-injection"></a>Razor 组件依赖关系注入

通过[Rainer Stropek](https://www.timecockpit.com)

[依赖关系注入 (DI)](/aspnet/core/fundamentals/dependency-injection)已内置。 应用可以使用内置的服务，方法是让注入到组件。 应用还可以定义自定义服务，并使其可通过 DI。

## <a name="dependency-injection"></a>依赖关系注入

DI 是一种技术用于访问在一个中心位置中配置的服务。 这可以是适用于：

* 在多个组件之间共享单个服务类的实例 (称为*单独*服务)。
* 分离特定的具体服务类中的组件，并仅引用抽象。 例如，一个接口`IDataAccess`由具体类实现`DataAccess`。 当一个组件使用 DI 接收`IDataAccess`实现，该组件不耦合到具体类型。 可以交换实现，可能是到单元测试中的模拟实现。

DI 系统是负责向服务添加到组件的实例。 DI 还解析依赖项以递归方式，以便服务本身可以依赖于更多服务。 在应用启动过程中配置 DI。 本主题中后面是一个示例。

## <a name="add-services-to-di"></a>将服务添加到 DI

创建新的应用程序之后, 检查`Startup.ConfigureServices`方法：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

`ConfigureServices`方法传递[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)，这是一系列服务描述符对象 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor))。 通过提供到服务集合的服务描述符添加服务。 下面的代码示例演示了这一概念：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

可以使用以下生存期配置服务：

| 方法      | 描述 |
| ----------- | ----------- |
| [单例](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | 创建 DI*单个实例*的服务。 需要此服务的所有组件都收到对此实例的引用。 |
| [暂时](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | 一个组件需要此服务，每当它收到*新实例*的服务。 |
| [作用域（Scoped）](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | 客户端 Blazor 当前没有 DI 作用域的概念。 `Scoped` 行为类似于`Singleton`。 但是，ASP.NET Core Razor 组件支持`Scoped`生存期。 在 Razor 组件中，作用域内的服务注册的应用范围限定为该连接。 出于此原因，使用作用域的服务是首选的服务，应将范围设置为当前用户 (即使当前的目的是客户端运行在浏览器中)。 |

DI 系统基于 ASP.NET Core 中的 DI 系统。 有关详细信息，请参阅[依赖关系注入在 ASP.NET Core 中的](/aspnet/core/fundamentals/dependency-injection)。

## <a name="default-services"></a>默认服务

默认服务自动添加到应用程序的服务集合中。 下表显示了一些有用的默认值提供的服务。

| 方法       | 描述 |
| ------------ | ----------- |
| [HttpClient](/dotnet/api/system.net.http.httpclient) | 提供用于发送 HTTP 请求和从由 URI （单一实例） 所标识资源接收 HTTP 响应的方法。 请注意，此实例的`HttpClient`使用浏览器来处理在后台的 HTTP 流量。 [HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress)自动设置为应用程序的基本 URI 前缀。 `HttpClient` 仅提供给客户端 Blazor 应用。 |
| `IJSRuntime` | 表示调用可能会派遣到其中一个 JavaScript 运行时的一个实例。 有关详细信息，请参阅 <xref:razor-components/javascript-interop>。 |
| `IUriHelper` | 适用于使用 Uri 和导航状态 （单一实例） 的帮助程序。 `IUriHelper` 提供给这两个客户端 Blazor 和 ASP.NET Core Razor 组件应用。 |

请注意，可以使用自定义服务提供程序而不是默认服务提供程序添加的默认模板。 自定义服务提供程序不会自动提供表中列出的默认服务。 这些服务必须显式添加到新的服务提供程序。

## <a name="request-a-service-in-a-component"></a>请求中组件的服务

一旦服务添加到服务集合，它们可以注入到组件的 Razor 模板中使用`@inject`Razor 指令。 `@inject` 有两个参数：

* 类型名称：要插入的服务的类型。
* 属性名称：接收注入的应用服务的属性的名称。 请注意，该属性不需要手动创建。 编译器会创建该属性。

多个`@inject`语句可用于插入不同的服务。

下面的示例说明如何使用 `@inject`。 服务实现`Services.IDataAccess`注入到组件的属性`DataRepository`。 请注意，代码仅使用`IDataAccess`抽象：

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

在内部，则生成的属性 (`DataRepository`) 用修饰`InjectAttribute`属性。 通常情况下，此属性不是直接使用。 如果基类是所必需的组件和注入的属性也是必需的基类，`InjectAttribute`可以手动添加：

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

在组件派生自的基类，`@inject`指令不是必需的。 `InjectAttribute`基类的足以：

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a>在服务中的依赖关系注入

复杂的服务可能需要其他服务。 在前面的示例中，`DataAccess`可能需要`HttpClient`默认服务。 `@inject` 或`InjectAttribute`不能在服务中使用。 *构造函数注入*必须改为使用。 通过将参数添加到服务的构造函数会添加所需的服务。 当依赖关系注入创建服务时，它认识到它需要在构造函数中，并相应地提供它们的服务。

下面的代码示例演示了这一概念：

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

请注意构造函数注入的以下先决条件：

* 必须有该形参的实参可以所有满足通过依赖关系注入的一个构造函数。 请注意，如果为其指定默认值，则允许未涵盖的 DI 的其他参数。
* 适用的构造函数必须是*公共*。
* 必须仅有一个适用的构造函数。 对于产生歧义，DI 将引发异常。

## <a name="additional-resources"></a>其他资源

* [在 ASP.NET Core 中的依赖关系注入](/aspnet/core/fundamentals/dependency-injection)
