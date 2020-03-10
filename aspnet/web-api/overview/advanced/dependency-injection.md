---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2 中的依赖项注入-ASP.NET 4。x
author: MikeWasson
description: 本教程演示如何在 ASP.NET 4.x 的 ASP.NET Web API 控制器中注入依赖项。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504944"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="a78f8-103">ASP.NET Web API 2 中的依赖项注入</span><span class="sxs-lookup"><span data-stu-id="a78f8-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="a78f8-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a78f8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a78f8-105">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="a78f8-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="a78f8-106">本教程演示如何在 ASP.NET Web API 控制器中注入依赖项。</span><span class="sxs-lookup"><span data-stu-id="a78f8-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a78f8-107">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a78f8-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a78f8-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a78f8-108">Web API 2</span></span>
> - [<span data-ttu-id="a78f8-109">Unity 应用程序块</span><span class="sxs-lookup"><span data-stu-id="a78f8-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="a78f8-110">实体框架6（版本5也适用）</span><span class="sxs-lookup"><span data-stu-id="a78f8-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="a78f8-111">什么是依赖项注入？</span><span class="sxs-lookup"><span data-stu-id="a78f8-111">What is Dependency Injection?</span></span>

<span data-ttu-id="a78f8-112">依赖项是另一个对象所需的任何对象。</span><span class="sxs-lookup"><span data-stu-id="a78f8-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="a78f8-113">例如，通常定义处理数据访问的[存储库](http://martinfowler.com/eaaCatalog/repository.html)。</span><span class="sxs-lookup"><span data-stu-id="a78f8-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="a78f8-114">我们来看一个示例。</span><span class="sxs-lookup"><span data-stu-id="a78f8-114">Let's illustrate with an example.</span></span> <span data-ttu-id="a78f8-115">首先，我们将定义域模型：</span><span class="sxs-lookup"><span data-stu-id="a78f8-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="a78f8-116">下面是一个简单存储库类，它使用实体框架在数据库中存储项。</span><span class="sxs-lookup"><span data-stu-id="a78f8-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="a78f8-117">现在，让我们定义一个 Web API 控制器，用于支持 `Product` 实体的 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="a78f8-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="a78f8-118">（为方便起见，我要退出 POST 和其他方法。）下面是第一次尝试：</span><span class="sxs-lookup"><span data-stu-id="a78f8-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="a78f8-119">请注意，控制器类依赖于 `ProductRepository`，并让控制器创建 `ProductRepository` 实例。</span><span class="sxs-lookup"><span data-stu-id="a78f8-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="a78f8-120">但出于多种原因，对依赖项进行硬编码是一种不好的做法。</span><span class="sxs-lookup"><span data-stu-id="a78f8-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="a78f8-121">如果要使用不同的实现替换 `ProductRepository`，还需要修改控制器类。</span><span class="sxs-lookup"><span data-stu-id="a78f8-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="a78f8-122">如果 `ProductRepository` 具有依赖关系，则必须在控制器中对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="a78f8-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="a78f8-123">对于包含多个控制器的大型项目，你的配置代码将分散到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="a78f8-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="a78f8-124">这种情况很难进行单元测试，因为控制器是硬编码的，以便查询数据库。</span><span class="sxs-lookup"><span data-stu-id="a78f8-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="a78f8-125">对于单元测试，应使用模拟或存根存储库，这是当前设计所不可能的。</span><span class="sxs-lookup"><span data-stu-id="a78f8-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="a78f8-126">可以通过将存储库*注入*控制器来解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="a78f8-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="a78f8-127">首先，将 `ProductRepository` 类重构为一个接口：</span><span class="sxs-lookup"><span data-stu-id="a78f8-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="a78f8-128">然后以构造函数参数的形式提供 `IProductRepository`：</span><span class="sxs-lookup"><span data-stu-id="a78f8-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="a78f8-129">此示例使用[构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="a78f8-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="a78f8-130">你还可以使用*setter 注入*，你可以在其中通过 setter 方法或属性设置依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a78f8-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="a78f8-131">但现在会出现问题，因为应用程序不会直接创建控制器。</span><span class="sxs-lookup"><span data-stu-id="a78f8-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="a78f8-132">Web API 在路由请求时创建控制器，而 Web API 不知道 `IProductRepository`的任何内容。</span><span class="sxs-lookup"><span data-stu-id="a78f8-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="a78f8-133">这就是 Web API 依赖关系解析程序所处的位置。</span><span class="sxs-lookup"><span data-stu-id="a78f8-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="a78f8-134">Web API 依赖关系解析程序</span><span class="sxs-lookup"><span data-stu-id="a78f8-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="a78f8-135">Web API 定义用于解析依赖项的**IDependencyResolver**接口。</span><span class="sxs-lookup"><span data-stu-id="a78f8-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="a78f8-136">下面是接口的定义：</span><span class="sxs-lookup"><span data-stu-id="a78f8-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="a78f8-137">**IDependencyScope**接口有两种方法：</span><span class="sxs-lookup"><span data-stu-id="a78f8-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="a78f8-138">**GetService**创建一个类型的实例。</span><span class="sxs-lookup"><span data-stu-id="a78f8-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="a78f8-139">**GetServices**创建指定类型的对象的集合。</span><span class="sxs-lookup"><span data-stu-id="a78f8-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="a78f8-140">**IDependencyResolver**方法继承**IDependencyScope**并添加**BeginScope**方法。</span><span class="sxs-lookup"><span data-stu-id="a78f8-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="a78f8-141">我将在本教程的后面部分讨论范围。</span><span class="sxs-lookup"><span data-stu-id="a78f8-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="a78f8-142">当 Web API 创建控制器实例时，它将首先调用**IDependencyResolver GetService**，并传入控制器类型。</span><span class="sxs-lookup"><span data-stu-id="a78f8-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="a78f8-143">可以使用此扩展性挂钩创建控制器，解析任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="a78f8-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="a78f8-144">如果**GetService**返回 Null，Web API 将在控制器类上查找无参数的构造函数。</span><span class="sxs-lookup"><span data-stu-id="a78f8-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="a78f8-145">与 Unity 容器的依赖项解析</span><span class="sxs-lookup"><span data-stu-id="a78f8-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="a78f8-146">尽管你可以从头开始编写完整的**IDependencyResolver**实现，但该接口实际上设计为在 Web API 与现有 IoC 容器之间充当桥梁。</span><span class="sxs-lookup"><span data-stu-id="a78f8-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="a78f8-147">IoC 容器是负责管理依赖项的软件组件。</span><span class="sxs-lookup"><span data-stu-id="a78f8-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="a78f8-148">使用容器注册类型，然后使用容器来创建对象。</span><span class="sxs-lookup"><span data-stu-id="a78f8-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="a78f8-149">容器自动找出依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a78f8-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="a78f8-150">许多 IoC 容器还允许您控制对象生存期和范围等任务。</span><span class="sxs-lookup"><span data-stu-id="a78f8-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="a78f8-151">"IoC" 代表 "控制反转"，这是一个框架对应用程序代码进行调用的常规模式。</span><span class="sxs-lookup"><span data-stu-id="a78f8-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="a78f8-152">IoC 容器为你构造对象，这会 "反转" 正常的控制流。</span><span class="sxs-lookup"><span data-stu-id="a78f8-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="a78f8-153">对于本教程，我们[将使用 Microsoft](https://msdn.microsoft.com/library/ff647202.aspx)模式 &amp; 实践。</span><span class="sxs-lookup"><span data-stu-id="a78f8-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="a78f8-154">（其他常用库包括[城堡 Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)和[StructureMap](http://structuremap.github.io/documentation/)。）你可以使用 NuGet 包管理器安装 Unity。</span><span class="sxs-lookup"><span data-stu-id="a78f8-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="a78f8-155">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="a78f8-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="a78f8-156">在 "程序包管理器控制台" 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a78f8-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="a78f8-157">下面是包装 Unity 容器的**IDependencyResolver**实现。</span><span class="sxs-lookup"><span data-stu-id="a78f8-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="a78f8-158">如果**GetService**方法无法解析类型，则应返回**null**。</span><span class="sxs-lookup"><span data-stu-id="a78f8-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="a78f8-159">如果**GetServices**方法无法解析类型，则应返回一个空集合对象。</span><span class="sxs-lookup"><span data-stu-id="a78f8-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="a78f8-160">请勿引发未知类型的异常。</span><span class="sxs-lookup"><span data-stu-id="a78f8-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="a78f8-161">配置依赖关系解析程序</span><span class="sxs-lookup"><span data-stu-id="a78f8-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="a78f8-162">在全局**HttpConfiguration**对象的**DependencyResolver**属性上设置依赖关系解析程序。</span><span class="sxs-lookup"><span data-stu-id="a78f8-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="a78f8-163">下面的代码将 `IProductRepository` 接口注册到 Unity，然后创建 `UnityResolver`。</span><span class="sxs-lookup"><span data-stu-id="a78f8-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="a78f8-164">依赖关系范围和控制器生存期</span><span class="sxs-lookup"><span data-stu-id="a78f8-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="a78f8-165">控制器是根据请求创建的。</span><span class="sxs-lookup"><span data-stu-id="a78f8-165">Controllers are created per request.</span></span> <span data-ttu-id="a78f8-166">为了管理对象生存期， **IDependencyResolver**使用了*作用域*的概念。</span><span class="sxs-lookup"><span data-stu-id="a78f8-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="a78f8-167">附加到**HttpConfiguration**对象的依赖关系解析程序具有全局范围。</span><span class="sxs-lookup"><span data-stu-id="a78f8-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="a78f8-168">当 Web API 创建控制器时，它会调用**BeginScope**。</span><span class="sxs-lookup"><span data-stu-id="a78f8-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="a78f8-169">此方法返回表示子作用域的**IDependencyScope** 。</span><span class="sxs-lookup"><span data-stu-id="a78f8-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="a78f8-170">然后，Web API 在子作用域上调用**GetService** ，以创建控制器。</span><span class="sxs-lookup"><span data-stu-id="a78f8-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="a78f8-171">请求完成后，Web API 会调用子范围中的**Dispose** 。</span><span class="sxs-lookup"><span data-stu-id="a78f8-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="a78f8-172">使用**dispose**方法释放控制器的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a78f8-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="a78f8-173">如何实现**BeginScope**取决于 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="a78f8-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="a78f8-174">对于 Unity，范围对应于子容器：</span><span class="sxs-lookup"><span data-stu-id="a78f8-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="a78f8-175">大多数 IoC 容器具有相似的等效项。</span><span class="sxs-lookup"><span data-stu-id="a78f8-175">Most IoC containers have similar equivalents.</span></span>
