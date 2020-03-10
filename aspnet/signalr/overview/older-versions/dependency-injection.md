---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR 1.x 中的依赖关系注入 |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431540"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="b86a3-102">SignalR 1.x 中的依赖项注入</span><span class="sxs-lookup"><span data-stu-id="b86a3-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="b86a3-103">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b86a3-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b86a3-104">依赖关系注入是一种删除对象之间硬编码的依赖关系的方法，这样可以更轻松地替换对象的依赖项（使用模拟对象）或更改运行时行为。</span><span class="sxs-lookup"><span data-stu-id="b86a3-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="b86a3-105">本教程介绍如何在 SignalR 集线器上执行依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="b86a3-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="b86a3-106">它还演示了如何通过 SignalR 使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="b86a3-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="b86a3-107">IoC 容器是用于依赖关系注入的通用框架。</span><span class="sxs-lookup"><span data-stu-id="b86a3-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="b86a3-108">什么是依赖项注入？</span><span class="sxs-lookup"><span data-stu-id="b86a3-108">What is Dependency Injection?</span></span>

<span data-ttu-id="b86a3-109">如果已熟悉依赖项注入，请跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="b86a3-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="b86a3-110">*依赖关系注入*（DI）是一种模式，其中对象不负责创建其自身的依赖项。</span><span class="sxs-lookup"><span data-stu-id="b86a3-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="b86a3-111">下面是一个用于鼓励 DI 的简单示例。</span><span class="sxs-lookup"><span data-stu-id="b86a3-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="b86a3-112">假设你有一个需要记录消息的对象。</span><span class="sxs-lookup"><span data-stu-id="b86a3-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="b86a3-113">您可以定义日志记录接口：</span><span class="sxs-lookup"><span data-stu-id="b86a3-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="b86a3-114">在对象中，可以创建日志消息 `ILogger`：</span><span class="sxs-lookup"><span data-stu-id="b86a3-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="b86a3-115">这可行，但并不是最佳设计。</span><span class="sxs-lookup"><span data-stu-id="b86a3-115">This works, but it's not the best design.</span></span> <span data-ttu-id="b86a3-116">如果要将 `FileLogger` 替换为其他 `ILogger` 实现，则必须修改 `SomeComponent`。</span><span class="sxs-lookup"><span data-stu-id="b86a3-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="b86a3-117">Supposing 有很多其他对象使用 `FileLogger`，你将需要更改所有这些对象。</span><span class="sxs-lookup"><span data-stu-id="b86a3-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="b86a3-118">或者，如果您决定将 `FileLogger` 为单一实例，则还需要在整个应用程序中进行更改。</span><span class="sxs-lookup"><span data-stu-id="b86a3-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="b86a3-119">更好的方法是将 `ILogger` "注入" 对象（例如，通过使用构造函数参数）：</span><span class="sxs-lookup"><span data-stu-id="b86a3-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="b86a3-120">现在，对象不负责选择要使用的 `ILogger`。</span><span class="sxs-lookup"><span data-stu-id="b86a3-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="b86a3-121">可以切换 `ILogger` 实现，而无需更改依赖于它的对象。</span><span class="sxs-lookup"><span data-stu-id="b86a3-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="b86a3-122">此模式称为 "[构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)"。</span><span class="sxs-lookup"><span data-stu-id="b86a3-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="b86a3-123">另一种模式是 setter 注入，可通过 setter 方法或属性设置依赖关系。</span><span class="sxs-lookup"><span data-stu-id="b86a3-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="b86a3-124">SignalR 中的简单依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="b86a3-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="b86a3-125">请考虑通过[SignalR 教程入门](../getting-started/tutorial-getting-started-with-signalr.md)的聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="b86a3-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="b86a3-126">下面是该应用程序的中心类：</span><span class="sxs-lookup"><span data-stu-id="b86a3-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="b86a3-127">假设你想要在发送聊天消息前将其存储在服务器上。</span><span class="sxs-lookup"><span data-stu-id="b86a3-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="b86a3-128">您可以定义一个用于提取此功能的接口，并使用 DI 将接口注入到 `ChatHub` 类中。</span><span class="sxs-lookup"><span data-stu-id="b86a3-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="b86a3-129">唯一的问题是 SignalR 应用程序不会直接创建集线器;SignalR 会为你创建它们。</span><span class="sxs-lookup"><span data-stu-id="b86a3-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="b86a3-130">默认情况下，SignalR 需要一个 hub 类具有无参数的构造函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="b86a3-131">不过，您可以轻松地注册一个函数来创建集线器实例，并使用此函数来执行 DI。</span><span class="sxs-lookup"><span data-stu-id="b86a3-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="b86a3-132">通过调用**GlobalHost**注册该函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="b86a3-133">现在，SignalR 将在需要创建 `ChatHub` 实例时调用此匿名函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="b86a3-134">IoC 容器</span><span class="sxs-lookup"><span data-stu-id="b86a3-134">IoC Containers</span></span>

<span data-ttu-id="b86a3-135">对于简单的情况，上面的代码是正确的。</span><span class="sxs-lookup"><span data-stu-id="b86a3-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="b86a3-136">但你仍必须编写以下内容：</span><span class="sxs-lookup"><span data-stu-id="b86a3-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="b86a3-137">在具有许多依赖项的复杂应用程序中，你可能需要编写大量此 "布线" 代码。</span><span class="sxs-lookup"><span data-stu-id="b86a3-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="b86a3-138">此代码很难维护，尤其是在嵌套依赖项的情况下。</span><span class="sxs-lookup"><span data-stu-id="b86a3-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="b86a3-139">它也很难进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="b86a3-139">It is also hard to unit test.</span></span>

<span data-ttu-id="b86a3-140">一种解决方法是使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="b86a3-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="b86a3-141">IoC 容器是负责管理依赖项的软件组件。使用容器注册类型，然后使用容器来创建对象。</span><span class="sxs-lookup"><span data-stu-id="b86a3-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="b86a3-142">容器自动找出依赖关系。</span><span class="sxs-lookup"><span data-stu-id="b86a3-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="b86a3-143">许多 IoC 容器还允许您控制对象生存期和范围等任务。</span><span class="sxs-lookup"><span data-stu-id="b86a3-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="b86a3-144">"IoC" 代表 "控制反转"，这是一个框架对应用程序代码进行调用的常规模式。</span><span class="sxs-lookup"><span data-stu-id="b86a3-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="b86a3-145">IoC 容器为你构造对象，这会 "反转" 正常的控制流。</span><span class="sxs-lookup"><span data-stu-id="b86a3-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="b86a3-146">在 SignalR 中使用 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="b86a3-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="b86a3-147">聊天应用程序可能太简单，无法从 IoC 容器中获益。</span><span class="sxs-lookup"><span data-stu-id="b86a3-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="b86a3-148">我们来看看[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)示例。</span><span class="sxs-lookup"><span data-stu-id="b86a3-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="b86a3-149">StockTicker 示例定义了两个主要类：</span><span class="sxs-lookup"><span data-stu-id="b86a3-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="b86a3-150">`StockTickerHub`：用于管理客户端连接的中心类。</span><span class="sxs-lookup"><span data-stu-id="b86a3-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="b86a3-151">`StockTicker`：保存股票价格并定期更新它们的单独。</span><span class="sxs-lookup"><span data-stu-id="b86a3-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="b86a3-152">`StockTickerHub` 保存对 `StockTicker` 单一实例的引用，而 `StockTicker` 保留对 `StockTickerHub`的**IHubConnectionContext**的引用。</span><span class="sxs-lookup"><span data-stu-id="b86a3-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="b86a3-153">它使用此接口与 `StockTickerHub` 实例通信。</span><span class="sxs-lookup"><span data-stu-id="b86a3-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="b86a3-154">（有关详细信息，请参阅[Server 广播网 with ASP.NET SignalR](index.md)。）</span><span class="sxs-lookup"><span data-stu-id="b86a3-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="b86a3-155">我们可以使用 IoC 容器解开这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="b86a3-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="b86a3-156">首先，让我们来简化 `StockTickerHub` 和 `StockTicker` 类。</span><span class="sxs-lookup"><span data-stu-id="b86a3-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="b86a3-157">在下面的代码中，我注释掉了不需要的部分。</span><span class="sxs-lookup"><span data-stu-id="b86a3-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="b86a3-158">从 `StockTicker`中移除无参数的构造函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="b86a3-159">相反，我们将始终使用 DI 来创建中心。</span><span class="sxs-lookup"><span data-stu-id="b86a3-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="b86a3-160">对于 StockTicker，删除单一实例。</span><span class="sxs-lookup"><span data-stu-id="b86a3-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="b86a3-161">稍后，我们将使用 IoC 容器来控制 StockTicker 生存期。</span><span class="sxs-lookup"><span data-stu-id="b86a3-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="b86a3-162">此外，请使构造函数成为公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="b86a3-163">接下来，我们可以通过创建 `StockTicker`的接口来重构代码。</span><span class="sxs-lookup"><span data-stu-id="b86a3-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="b86a3-164">我们将使用此接口从 `StockTicker` 类中分离 `StockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="b86a3-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="b86a3-165">Visual Studio 可轻松实现这种重构。</span><span class="sxs-lookup"><span data-stu-id="b86a3-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="b86a3-166">打开文件 "StockTicker.cs"，右键单击 `StockTicker` 类声明，然后选择 "**重构**..."**提取接口**。</span><span class="sxs-lookup"><span data-stu-id="b86a3-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="b86a3-167">在 "**提取接口**" 对话框中，单击 "**全选**"。</span><span class="sxs-lookup"><span data-stu-id="b86a3-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="b86a3-168">保留其他默认值。</span><span class="sxs-lookup"><span data-stu-id="b86a3-168">Leave the other defaults.</span></span> <span data-ttu-id="b86a3-169">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="b86a3-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="b86a3-170">Visual Studio 将创建一个名为 `IStockTicker`的新接口，还会将 `StockTicker` 更改为从 `IStockTicker`派生。</span><span class="sxs-lookup"><span data-stu-id="b86a3-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="b86a3-171">打开文件 "IStockTicker.cs"，并将接口更改为 "**公共**"。</span><span class="sxs-lookup"><span data-stu-id="b86a3-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="b86a3-172">在 `StockTickerHub` 类中，将 `StockTicker` 的两个实例更改为 `IStockTicker`：</span><span class="sxs-lookup"><span data-stu-id="b86a3-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="b86a3-173">不一定要创建 `IStockTicker` 接口，但我希望显示 DI 如何帮助减少应用程序中组件之间的耦合。</span><span class="sxs-lookup"><span data-stu-id="b86a3-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="b86a3-174">添加 Ninject 库</span><span class="sxs-lookup"><span data-stu-id="b86a3-174">Add the Ninject Library</span></span>

<span data-ttu-id="b86a3-175">.NET 有许多开源 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="b86a3-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="b86a3-176">在本教程中，我将使用[Ninject](http://www.ninject.org/)。</span><span class="sxs-lookup"><span data-stu-id="b86a3-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="b86a3-177">（其他常用库包括[城堡 Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)和[StructureMap](http://docs.structuremap.net)。）</span><span class="sxs-lookup"><span data-stu-id="b86a3-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="b86a3-178">使用 NuGet 包管理器安装[Ninject 库](https://nuget.org/packages/Ninject/3.0.1.10)。</span><span class="sxs-lookup"><span data-stu-id="b86a3-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="b86a3-179">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器** > **程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="b86a3-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b86a3-180">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b86a3-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="b86a3-181">替换 SignalR 依赖关系解析程序</span><span class="sxs-lookup"><span data-stu-id="b86a3-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="b86a3-182">若要在 SignalR 中使用 Ninject，请创建从**DefaultDependencyResolver**派生的类。</span><span class="sxs-lookup"><span data-stu-id="b86a3-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="b86a3-183">此类将重写**DefaultDependencyResolver**的**GetService**和**GetServices**方法。</span><span class="sxs-lookup"><span data-stu-id="b86a3-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="b86a3-184">SignalR 调用这些方法在运行时创建各种对象，包括中心实例，以及由 SignalR 在内部使用的各种服务。</span><span class="sxs-lookup"><span data-stu-id="b86a3-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="b86a3-185">**GetService**方法创建类型的单个实例。</span><span class="sxs-lookup"><span data-stu-id="b86a3-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="b86a3-186">重写此方法，以调用 Ninject 内核的**TryGet**方法。</span><span class="sxs-lookup"><span data-stu-id="b86a3-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="b86a3-187">如果该方法返回 null，则回退到默认的冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="b86a3-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="b86a3-188">**GetServices**方法创建指定类型的对象的集合。</span><span class="sxs-lookup"><span data-stu-id="b86a3-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="b86a3-189">重写此方法以将 Ninject 的结果与默认解析程序的结果连接。</span><span class="sxs-lookup"><span data-stu-id="b86a3-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="b86a3-190">配置 Ninject 绑定</span><span class="sxs-lookup"><span data-stu-id="b86a3-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="b86a3-191">现在，我们将使用 Ninject 声明类型绑定。</span><span class="sxs-lookup"><span data-stu-id="b86a3-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="b86a3-192">打开文件 RegisterHubs.cs。</span><span class="sxs-lookup"><span data-stu-id="b86a3-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="b86a3-193">在 `RegisterHubs.Start` 方法中，创建 Ninject 调用*内核*的 Ninject 容器。</span><span class="sxs-lookup"><span data-stu-id="b86a3-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="b86a3-194">创建自定义依赖关系解析程序的实例：</span><span class="sxs-lookup"><span data-stu-id="b86a3-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="b86a3-195">为 `IStockTicker` 创建绑定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b86a3-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="b86a3-196">此代码说明两个问题。</span><span class="sxs-lookup"><span data-stu-id="b86a3-196">This code is saying two things.</span></span> <span data-ttu-id="b86a3-197">首先，每当应用程序需要 `IStockTicker`时，内核都应创建 `StockTicker`的实例。</span><span class="sxs-lookup"><span data-stu-id="b86a3-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="b86a3-198">其次，`StockTicker` 类应是创建为单一实例对象的。</span><span class="sxs-lookup"><span data-stu-id="b86a3-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="b86a3-199">Ninject 将创建一个对象实例，并为每个请求返回同一个实例。</span><span class="sxs-lookup"><span data-stu-id="b86a3-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="b86a3-200">创建**IHubConnectionContext**的绑定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b86a3-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="b86a3-201">此代码创建一个返回**IHubConnection**的匿名函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="b86a3-202">**WhenInjectedInto**方法告诉 Ninject 仅在创建 `IStockTicker` 实例时才使用此函数。</span><span class="sxs-lookup"><span data-stu-id="b86a3-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="b86a3-203">原因是 SignalR 在内部创建**IHubConnectionContext**实例，而我们不希望重写 SignalR 创建它们的方式。</span><span class="sxs-lookup"><span data-stu-id="b86a3-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="b86a3-204">此函数仅适用于我们的 `StockTicker` 类。</span><span class="sxs-lookup"><span data-stu-id="b86a3-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="b86a3-205">将依赖关系解析程序传递到**routeconfig**方法中：</span><span class="sxs-lookup"><span data-stu-id="b86a3-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="b86a3-206">现在，SignalR 将使用**routeconfig**中指定的冲突解决程序，而不是默认的冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="b86a3-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="b86a3-207">下面是 `RegisterHubs.Start`的完整代码列表。</span><span class="sxs-lookup"><span data-stu-id="b86a3-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="b86a3-208">若要在 Visual Studio 中运行 StockTicker 应用程序，请按 F5。</span><span class="sxs-lookup"><span data-stu-id="b86a3-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="b86a3-209">在浏览器窗口中，导航到 `http://localhost:*port*/SignalR.Sample/StockTicker.html`。</span><span class="sxs-lookup"><span data-stu-id="b86a3-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="b86a3-210">应用程序的功能与以前完全相同。</span><span class="sxs-lookup"><span data-stu-id="b86a3-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="b86a3-211">（有关说明，请参阅[使用 ASP.NET SignalR 进行服务器广播](index.md)。）我们尚未更改该行为;只是使代码更易于测试、维护和发展。</span><span class="sxs-lookup"><span data-stu-id="b86a3-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
