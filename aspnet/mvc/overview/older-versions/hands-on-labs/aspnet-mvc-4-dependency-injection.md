---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 依赖关系注入 |Microsoft Docs
author: rick-anderson
description: 注意：此动手实验假设你具有 ASP.NET MVC 和 ASP.NET MVC 4 筛选器的基本知识。 如果以前未使用过 ASP.NET MVC 4 筛选器，我们将 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451820"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="8dad5-104">ASP.NET MVC 4 依赖项注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="8dad5-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="8dad5-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="8dad5-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="8dad5-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="8dad5-107">此动手实验假设你具有**ASP.NET mvc**和**ASP.NET mvc 4 筛选器**的基本知识。</span><span class="sxs-lookup"><span data-stu-id="8dad5-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="8dad5-108">如果你之前未使用过**ASP.NET mvc 4 筛选器**，我们建议你使用**ASP.NET Mvc 自定义操作筛选器**动手实验。</span><span class="sxs-lookup"><span data-stu-id="8dad5-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="8dad5-109">所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)获取。</span><span class="sxs-lookup"><span data-stu-id="8dad5-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="8dad5-110">[ASP.NET MVC 4 依赖关系注入](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)中提供了此实验室特定的项目。</span><span class="sxs-lookup"><span data-stu-id="8dad5-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="8dad5-111">在**面向对象的编程**范例中，对象在存在参与者和使用者的协作模型中协同工作。</span><span class="sxs-lookup"><span data-stu-id="8dad5-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="8dad5-112">当然，这种通信模型会生成对象与组件之间的依赖关系，在复杂性增加时变得难以管理。</span><span class="sxs-lookup"><span data-stu-id="8dad5-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="8dad5-113">![类依赖项和模型复杂性](aspnet-mvc-4-dependency-injection/_static/image1.png "类依赖项和模型复杂性")</span><span class="sxs-lookup"><span data-stu-id="8dad5-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="8dad5-114">*类依赖项和模型复杂性*</span><span class="sxs-lookup"><span data-stu-id="8dad5-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="8dad5-115">你可能听说过**工厂模式**以及接口和实现之间的分离使用服务，其中客户端对象通常负责服务定位。</span><span class="sxs-lookup"><span data-stu-id="8dad5-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="8dad5-116">依赖关系注入模式是一种特定的控制反转实现。</span><span class="sxs-lookup"><span data-stu-id="8dad5-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="8dad5-117">**控制反转（IoC）** 表示对象不会创建其他对象，这些对象依赖于它们来完成工作。</span><span class="sxs-lookup"><span data-stu-id="8dad5-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="8dad5-118">相反，它们从外部源（例如 xml 配置文件）获取所需的对象。</span><span class="sxs-lookup"><span data-stu-id="8dad5-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="8dad5-119">**依赖关系注入（DI）** 表示在没有对象干预的情况下执行此操作，通常由传递构造函数参数和设置属性的框架组件完成。</span><span class="sxs-lookup"><span data-stu-id="8dad5-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="8dad5-120">依赖关系注入（DI）设计模式</span><span class="sxs-lookup"><span data-stu-id="8dad5-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="8dad5-121">从较高层次来看，依赖关系注入的目标是客户端类（例如*高尔夫选手*）需要满足接口的某些内容（例如*IClub*）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="8dad5-122">它并不关心具体类型是什么（例如 *，WoodClub、IronClub、WedgeClub*或*PutterClub*），而是希望别人处理该类型（例如，一个好的*caddy*）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="8dad5-123">ASP.NET MVC 中的依赖关系解析程序可以让你在其他位置（例如，容器或*梅花包*）注册依赖逻辑。</span><span class="sxs-lookup"><span data-stu-id="8dad5-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="8dad5-124">![依赖关系注入关系图](aspnet-mvc-4-dependency-injection/_static/image2.png "依赖关系注入图")</span><span class="sxs-lookup"><span data-stu-id="8dad5-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="8dad5-125">*依赖关系注入-高尔夫类比*</span><span class="sxs-lookup"><span data-stu-id="8dad5-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="8dad5-126">使用依赖关系注入模式和控制反转的优点如下：</span><span class="sxs-lookup"><span data-stu-id="8dad5-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="8dad5-127">减少类耦合</span><span class="sxs-lookup"><span data-stu-id="8dad5-127">Reduces class coupling</span></span>
- <span data-ttu-id="8dad5-128">增加代码重用</span><span class="sxs-lookup"><span data-stu-id="8dad5-128">Increases code reusing</span></span>
- <span data-ttu-id="8dad5-129">提高代码可维护性</span><span class="sxs-lookup"><span data-stu-id="8dad5-129">Improves code maintainability</span></span>
- <span data-ttu-id="8dad5-130">改进应用程序测试</span><span class="sxs-lookup"><span data-stu-id="8dad5-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="8dad5-131">依赖关系注入有时与抽象工厂设计模式比较，但这两种方法之间略有不同。</span><span class="sxs-lookup"><span data-stu-id="8dad5-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="8dad5-132">DI 具有一个框架，可用于通过调用工厂和注册的服务来解决依赖项。</span><span class="sxs-lookup"><span data-stu-id="8dad5-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="8dad5-133">现在，你已了解依赖关系注入模式，你将在本实验室中学习如何在 ASP.NET MVC 4 中应用此模式。</span><span class="sxs-lookup"><span data-stu-id="8dad5-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="8dad5-134">你将开始在**控制器**中使用依赖关系注入，以包含数据库访问服务。</span><span class="sxs-lookup"><span data-stu-id="8dad5-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="8dad5-135">接下来，您将向**视图**应用依赖关系注入，以使用服务并显示信息。</span><span class="sxs-lookup"><span data-stu-id="8dad5-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="8dad5-136">最后，将 DI 扩展到 ASP.NET MVC 4 筛选器，在解决方案中注入自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="8dad5-137">在此动手实验中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="8dad5-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="8dad5-138">将 ASP.NET MVC 4 与 Unity 集成，以便使用 NuGet 包进行依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="8dad5-139">在 ASP.NET MVC 控制器中使用依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="8dad5-140">在 ASP.NET MVC 视图中使用依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="8dad5-141">在 ASP.NET MVC 操作筛选器中使用依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="8dad5-142">此实验室使用 Mvc3 NuGet 包进行依赖关系解析，但可以调整任何依赖关系注入框架，使其与 ASP.NET MVC 4 结合使用。</span><span class="sxs-lookup"><span data-stu-id="8dad5-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="8dad5-143">系统必备</span><span class="sxs-lookup"><span data-stu-id="8dad5-143">Prerequisites</span></span>

<span data-ttu-id="8dad5-144">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="8dad5-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="8dad5-145">适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="8dad5-146">安装</span><span class="sxs-lookup"><span data-stu-id="8dad5-146">Setup</span></span>

<span data-ttu-id="8dad5-147">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="8dad5-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="8dad5-148">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="8dad5-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="8dad5-149">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="8dad5-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="8dad5-150">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本 &quot;文档中的附录[：附录 B：使用代码片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad5-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="8dad5-151">练习</span><span class="sxs-lookup"><span data-stu-id="8dad5-151">Exercises</span></span>

<span data-ttu-id="8dad5-152">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="8dad5-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="8dad5-153">练习1：注入控制器</span><span class="sxs-lookup"><span data-stu-id="8dad5-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="8dad5-154">练习2：注入视图</span><span class="sxs-lookup"><span data-stu-id="8dad5-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="8dad5-155">练习3：注入筛选器</span><span class="sxs-lookup"><span data-stu-id="8dad5-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="8dad5-156">每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="8dad5-157">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="8dad5-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="8dad5-158">完成本实验的估计时间： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="8dad5-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="8dad5-159">练习1：注入控制器</span><span class="sxs-lookup"><span data-stu-id="8dad5-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="8dad5-160">在此练习中，您将学习如何通过使用 NuGet 包集成 Unity，在 ASP.NET MVC 控制器中使用依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="8dad5-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="8dad5-161">出于此原因，你将在 MvcMusicStore 控制器中包含服务，以将逻辑与数据访问分隔开来。</span><span class="sxs-lookup"><span data-stu-id="8dad5-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="8dad5-162">这些服务将在控制器构造函数中创建新的依赖关系，该依赖关系注入将通过**Unity**的帮助来解决。</span><span class="sxs-lookup"><span data-stu-id="8dad5-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="8dad5-163">此方法将向你展示如何生成更少耦合的应用程序，这些应用程序更灵活、更易于维护和测试。</span><span class="sxs-lookup"><span data-stu-id="8dad5-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="8dad5-164">你还将了解如何将 ASP.NET MVC 与 Unity 集成。</span><span class="sxs-lookup"><span data-stu-id="8dad5-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="8dad5-165">关于 StoreManager 服务</span><span class="sxs-lookup"><span data-stu-id="8dad5-165">About StoreManager Service</span></span>

<span data-ttu-id="8dad5-166">开始解决方案中提供的 MVC 音乐商店现在包含管理名为**StoreService**的存储控制器数据的服务。</span><span class="sxs-lookup"><span data-stu-id="8dad5-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="8dad5-167">下面你会发现存储服务实现。</span><span class="sxs-lookup"><span data-stu-id="8dad5-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="8dad5-168">请注意，所有方法都返回模型实体。</span><span class="sxs-lookup"><span data-stu-id="8dad5-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="8dad5-169">开始解决方案的**StoreController**现在使用**StoreService**。</span><span class="sxs-lookup"><span data-stu-id="8dad5-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="8dad5-170">所有数据引用均已从**StoreController**中删除，现在可以修改当前的数据访问接口，而无需更改任何使用**StoreService**的方法。</span><span class="sxs-lookup"><span data-stu-id="8dad5-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="8dad5-171">下面你会发现， **StoreController**实现在类构造函数内与**StoreService**具有依赖关系。</span><span class="sxs-lookup"><span data-stu-id="8dad5-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="8dad5-172">本练习中引入的依赖关系与**控制反转**（IoC）有关。</span><span class="sxs-lookup"><span data-stu-id="8dad5-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="8dad5-173">**StoreController**类构造函数收到**IStoreService**类型参数，这对于从类内部执行服务调用至关重要。</span><span class="sxs-lookup"><span data-stu-id="8dad5-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="8dad5-174">不过， **StoreController**不实现任何控制器必须与 ASP.NET MVC 一起使用的默认构造函数（不带参数）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="8dad5-175">若要解决依赖关系，控制器必须由抽象工厂创建（一个返回指定类型的任何对象的类）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="8dad5-176">当类尝试创建 StoreController 时，如果没有声明无参数的构造函数，则会收到错误。</span><span class="sxs-lookup"><span data-stu-id="8dad5-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="8dad5-177">任务 1-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8dad5-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="8dad5-178">在此任务中，将运行 "开始" 应用程序，该应用程序将服务包含在将数据访问与应用程序逻辑分开的存储控制器中。</span><span class="sxs-lookup"><span data-stu-id="8dad5-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="8dad5-179">运行应用程序时，你将收到一个异常，因为默认情况下控制器服务不作为参数传递：</span><span class="sxs-lookup"><span data-stu-id="8dad5-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="8dad5-180">打开位于**Source\Ex01-Injecting Controller\Begin**的 "**开始**" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="8dad5-181">在继续之前，需要下载一些缺少的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8dad5-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8dad5-182">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8dad5-183">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="8dad5-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8dad5-184">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8dad5-185">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="8dad5-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8dad5-186">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="8dad5-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8dad5-187">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="8dad5-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="8dad5-188">按**Ctrl + F5**以运行应用程序而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="8dad5-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="8dad5-189">将收到错误消息，&quot;**没有为此对象定义无参数的构造函数**&quot;：</span><span class="sxs-lookup"><span data-stu-id="8dad5-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="8dad5-190">![运行 ASP.NET MVC Begin 应用程序时出错](aspnet-mvc-4-dependency-injection/_static/image3.png "运行 ASP.NET MVC Begin 应用程序时出错")</span><span class="sxs-lookup"><span data-stu-id="8dad5-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="8dad5-191">*运行 ASP.NET MVC Begin 应用程序时出错*</span><span class="sxs-lookup"><span data-stu-id="8dad5-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="8dad5-192">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-192">Close the browser.</span></span>

<span data-ttu-id="8dad5-193">在以下步骤中，你将使用音乐应用商店解决方案来注入此控制器所需的依赖项。</span><span class="sxs-lookup"><span data-stu-id="8dad5-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="8dad5-194">任务 2-包括 Unity 到 MvcMusicStore 解决方案</span><span class="sxs-lookup"><span data-stu-id="8dad5-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="8dad5-195">在此任务中，你将在解决方案中包括**Mvc3** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8dad5-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="8dad5-196">Mvc3 包专为 ASP.NET MVC 3 设计，但它与 ASP.NET MVC 4 完全兼容。</span><span class="sxs-lookup"><span data-stu-id="8dad5-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="8dad5-197">Unity 是一个轻型的可扩展依赖关系注入容器，它支持实例和类型截取。</span><span class="sxs-lookup"><span data-stu-id="8dad5-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="8dad5-198">它是用于任何类型的 .NET 应用程序的常规用途容器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="8dad5-199">它提供了依赖关系注入机制中的所有常见功能，包括：对象创建、通过在运行时通过指定依赖项来抽象要求，以及通过将组件配置推迟到容器来实现灵活性。</span><span class="sxs-lookup"><span data-stu-id="8dad5-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="8dad5-200">在**MvcMusicStore**项目中安装**Mvc3** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8dad5-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="8dad5-201">为此，请从 | **其他窗口**的**视图**中打开**包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="8dad5-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="8dad5-202">运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="8dad5-202">Run the following command.</span></span>

    <span data-ttu-id="8dad5-203">PMC</span><span class="sxs-lookup"><span data-stu-id="8dad5-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="8dad5-204">![正在安装 Unity. Mvc3 NuGet 包](aspnet-mvc-4-dependency-injection/_static/image4.png "正在安装 Unity. Mvc3 NuGet 包")</span><span class="sxs-lookup"><span data-stu-id="8dad5-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="8dad5-205">*正在安装 Unity. Mvc3 NuGet 包*</span><span class="sxs-lookup"><span data-stu-id="8dad5-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="8dad5-206">安装**Mvc3**包后，浏览它自动添加的文件和文件夹，以便简化 Unity 配置。</span><span class="sxs-lookup"><span data-stu-id="8dad5-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="8dad5-207">![已安装 Mvc3 包](aspnet-mvc-4-dependency-injection/_static/image5.png "已安装 Mvc3 包")</span><span class="sxs-lookup"><span data-stu-id="8dad5-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="8dad5-208">*已安装 Mvc3 包*</span><span class="sxs-lookup"><span data-stu-id="8dad5-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="8dad5-209">任务 3-在 Global.asax.cs 应用程序中注册 Unity\_开始</span><span class="sxs-lookup"><span data-stu-id="8dad5-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="8dad5-210">在此任务中，你将更新**Global.asax.cs**中的**应用程序\_Start**方法，以调用 Unity 引导程序初始值设定项，然后更新引导程序文件，以注册将用于依赖关系注入的服务和控制器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="8dad5-211">现在，你将挂接引导程序，这是用于初始化 Unity 容器和依赖关系解析程序的文件。</span><span class="sxs-lookup"><span data-stu-id="8dad5-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="8dad5-212">为此，请打开**Global.asax.cs** ，并在**应用程序\_Start**方法中添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="8dad5-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="8dad5-213">（代码段- *ASP.NET 依赖关系注入实验室-Ex01-初始化 Unity*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="8dad5-214">打开**Bootstrapper.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8dad5-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="8dad5-215">包含以下命名空间： **MvcMusicStore**和**MusicStore**。</span><span class="sxs-lookup"><span data-stu-id="8dad5-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="8dad5-216">（代码段- *ASP.NET 依赖关系注入实验室-Ex01-引导程序添加命名空间*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="8dad5-217">将**BuildUnityContainer**方法的内容替换为以下代码，用于注册商店控制器和存储服务。</span><span class="sxs-lookup"><span data-stu-id="8dad5-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="8dad5-218">（代码段- *ASP.NET 依赖关系注入实验室-Ex01-注册存储控制器和服务*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="8dad5-219">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8dad5-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="8dad5-220">在此任务中，你将运行应用程序，以验证它现在可以在包含 Unity 之后加载。</span><span class="sxs-lookup"><span data-stu-id="8dad5-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="8dad5-221">按**F5**运行应用程序，应用程序现在应加载，而不显示任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="8dad5-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="8dad5-222">![正在运行具有依赖关系注入的应用程序](aspnet-mvc-4-dependency-injection/_static/image6.png "正在运行具有依赖关系注入的应用程序")</span><span class="sxs-lookup"><span data-stu-id="8dad5-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="8dad5-223">*正在运行具有依赖关系注入的应用程序*</span><span class="sxs-lookup"><span data-stu-id="8dad5-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="8dad5-224">浏览到 **/Store**。</span><span class="sxs-lookup"><span data-stu-id="8dad5-224">Browse to **/Store**.</span></span> <span data-ttu-id="8dad5-225">这将调用现在使用**Unity**创建的**StoreController**。</span><span class="sxs-lookup"><span data-stu-id="8dad5-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="8dad5-226">![MVC 音乐商店](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC 音乐商店")</span><span class="sxs-lookup"><span data-stu-id="8dad5-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="8dad5-227">*MVC 音乐商店*</span><span class="sxs-lookup"><span data-stu-id="8dad5-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="8dad5-228">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-228">Close the browser.</span></span>

<span data-ttu-id="8dad5-229">在以下练习中，您将学习如何扩展依赖项注入范围以便在 ASP.NET MVC 视图和操作筛选器中使用它。</span><span class="sxs-lookup"><span data-stu-id="8dad5-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="8dad5-230">练习2：注入视图</span><span class="sxs-lookup"><span data-stu-id="8dad5-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="8dad5-231">在此练习中，您将学习如何在视图中使用依赖关系注入，其中的新功能为 ASP.NET MVC 4 for Unity 集成。</span><span class="sxs-lookup"><span data-stu-id="8dad5-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="8dad5-232">为此，你将在 "应用商店" 浏览视图中调用一个自定义服务，此操作将显示以下消息和图像。</span><span class="sxs-lookup"><span data-stu-id="8dad5-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="8dad5-233">然后，将项目与 Unity 集成，并创建自定义依赖项解析程序来注入依赖项。</span><span class="sxs-lookup"><span data-stu-id="8dad5-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="8dad5-234">任务 1-创建使用服务的视图</span><span class="sxs-lookup"><span data-stu-id="8dad5-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="8dad5-235">在此任务中，您将创建一个视图，该视图执行服务调用以生成新的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="8dad5-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="8dad5-236">此服务包含在此解决方案中包含的简单消息传递服务中。</span><span class="sxs-lookup"><span data-stu-id="8dad5-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="8dad5-237">打开位于**Source\Ex02-Injecting View\Begin**文件夹中的 "**开始**" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="8dad5-238">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="8dad5-239">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="8dad5-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8dad5-240">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8dad5-241">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="8dad5-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8dad5-242">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8dad5-243">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="8dad5-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8dad5-244">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="8dad5-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8dad5-245">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="8dad5-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="8dad5-246">有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="8dad5-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="8dad5-247">将**MessageService.cs**和**IMessageService.cs**类包括在 **/Services**的**源 \Assets**文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8dad5-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="8dad5-248">为此，请右键单击 "**服务**" 文件夹，然后选择 "**添加现有项**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="8dad5-249">浏览到文件的位置并包含这些文件。</span><span class="sxs-lookup"><span data-stu-id="8dad5-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="8dad5-250">![添加消息服务和服务接口](aspnet-mvc-4-dependency-injection/_static/image8.png "添加消息服务和服务接口")</span><span class="sxs-lookup"><span data-stu-id="8dad5-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="8dad5-251">*添加消息服务和服务接口*</span><span class="sxs-lookup"><span data-stu-id="8dad5-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8dad5-252">**IMessageService**接口定义由**MessageService**类实现的两个属性。</span><span class="sxs-lookup"><span data-stu-id="8dad5-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="8dad5-253">这些属性-**message**和**ImageUrl**-存储消息以及要显示的图像的 URL。</span><span class="sxs-lookup"><span data-stu-id="8dad5-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="8dad5-254">在项目的根文件夹中创建 **/Pages**文件夹，然后从**Source\Assets**添加现有类**MyBasePage.cs** 。</span><span class="sxs-lookup"><span data-stu-id="8dad5-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="8dad5-255">您将从继承的基本页具有以下结构。</span><span class="sxs-lookup"><span data-stu-id="8dad5-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="8dad5-256">![Pages 文件夹](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages 文件夹")</span><span class="sxs-lookup"><span data-stu-id="8dad5-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="8dad5-257">打开 **/Views/Store**文件夹中的 "**浏览**" 视图，并使其从**MyBasePage.cs**继承。</span><span class="sxs-lookup"><span data-stu-id="8dad5-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="8dad5-258">在 "**浏览**" 视图中，添加对**MessageService**的调用，以显示该服务检索的图像和消息。</span><span class="sxs-lookup"><span data-stu-id="8dad5-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="8dad5-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="8dad5-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="8dad5-260">任务 2-包括自定义依赖关系解析程序和自定义视图页激活器</span><span class="sxs-lookup"><span data-stu-id="8dad5-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="8dad5-261">在上一个任务中，您在视图内注入了新的依赖项，以便在其中执行服务调用。</span><span class="sxs-lookup"><span data-stu-id="8dad5-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="8dad5-262">现在，你将通过实现 ASP.NET MVC 依赖关系注入接口**IViewPageActivator**和**IDependencyResolver**来解析该依赖项。</span><span class="sxs-lookup"><span data-stu-id="8dad5-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="8dad5-263">你将在解决方案中包括**IDependencyResolver**的实现，该实现将使用 Unity 处理服务检索。</span><span class="sxs-lookup"><span data-stu-id="8dad5-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="8dad5-264">然后，您将包括**IViewPageActivator**接口的另一个自定义实现，该实现将解决视图的创建过程。</span><span class="sxs-lookup"><span data-stu-id="8dad5-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="8dad5-265">由于 ASP.NET MVC 3，依赖关系注入的实现已简化了用于注册服务的接口。</span><span class="sxs-lookup"><span data-stu-id="8dad5-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="8dad5-266">**IDependencyResolver**和**IVIEWPAGEACTIVATOR**是 ASP.NET MVC 3 功能的一部分，用于进行依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="8dad5-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="8dad5-267">**-IDependencyResolver**接口替换之前的 IMvcServiceLocator。</span><span class="sxs-lookup"><span data-stu-id="8dad5-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="8dad5-268">IDependencyResolver 的实施者必须返回服务或服务集合的实例。</span><span class="sxs-lookup"><span data-stu-id="8dad5-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="8dad5-269">**-IViewPageActivator**接口可更精细地控制通过依赖关系注入来实例化视图页面的方式。</span><span class="sxs-lookup"><span data-stu-id="8dad5-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="8dad5-270">实现**IViewPageActivator**接口的类可以使用上下文信息创建视图实例。</span><span class="sxs-lookup"><span data-stu-id="8dad5-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="8dad5-271">在项目的根文件夹中创建/**工厂**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8dad5-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="8dad5-272">将**CustomViewPageActivator.cs**从 **/Sources/Assets/** 添加到**工厂**文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8dad5-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="8dad5-273">为此，请右键单击 **/Factories**文件夹，选择 "**添加" |"现有项目**"，然后选择 " **CustomViewPageActivator.cs**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="8dad5-274">此类实现**IViewPageActivator**接口以容纳 Unity 容器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="8dad5-275">**CustomViewPageActivator**负责使用 Unity 容器来管理创建视图。</span><span class="sxs-lookup"><span data-stu-id="8dad5-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="8dad5-276">将**UnityDependencyResolver.cs**文件从 **/Sources/Assets**添加到 **/Factories**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8dad5-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="8dad5-277">为此，请右键单击 **/Factories**文件夹，选择 "**添加" |"现有项目**"，然后选择 " **UnityDependencyResolver.cs**文件"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="8dad5-278">**UnityDependencyResolver**类是 Unity 的自定义 DependencyResolver。</span><span class="sxs-lookup"><span data-stu-id="8dad5-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="8dad5-279">如果在 Unity 容器中找不到服务，则基本解析程序为 invocated。</span><span class="sxs-lookup"><span data-stu-id="8dad5-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="8dad5-280">在以下任务中，将注册这两种实现，以使模型知道服务和视图的位置。</span><span class="sxs-lookup"><span data-stu-id="8dad5-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="8dad5-281">任务 3-注册 Unity 容器中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="8dad5-282">在此任务中，您将所有前面的操作组合在一起，以进行依赖关系注入工作。</span><span class="sxs-lookup"><span data-stu-id="8dad5-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="8dad5-283">现在，你的解决方案包含以下元素：</span><span class="sxs-lookup"><span data-stu-id="8dad5-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="8dad5-284">从**MyBaseClass**继承并使用**MessageService**的**浏览**视图。</span><span class="sxs-lookup"><span data-stu-id="8dad5-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="8dad5-285">中间类-**MyBaseClass**-已为服务接口声明了依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="8dad5-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="8dad5-286">**IMessageService**的**MessageService**及其接口。</span><span class="sxs-lookup"><span data-stu-id="8dad5-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="8dad5-287">针对 Unity **UnityDependencyResolver**的自定义依赖关系解析程序，用于处理服务检索。</span><span class="sxs-lookup"><span data-stu-id="8dad5-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="8dad5-288">视图页激活器- **CustomViewPageActivator** -用于创建页面。</span><span class="sxs-lookup"><span data-stu-id="8dad5-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="8dad5-289">若要注入**浏览**视图，你现在将在 Unity 容器中注册自定义依赖关系解析程序。</span><span class="sxs-lookup"><span data-stu-id="8dad5-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="8dad5-290">打开**Bootstrapper.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="8dad5-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="8dad5-291">将**MessageService**的实例注册到 Unity 容器，以初始化服务：</span><span class="sxs-lookup"><span data-stu-id="8dad5-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="8dad5-292">（代码段- *ASP.NET 依赖关系注入实验室-Ex02-注册消息服务*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="8dad5-293">添加对**MvcMusicStore**命名空间的引用。</span><span class="sxs-lookup"><span data-stu-id="8dad5-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="8dad5-294">（代码段- *ASP.NET 依赖关系注入实验室-Ex02 命名空间*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="8dad5-295">将**CustomViewPageActivator**作为视图页激活器注册到 Unity 容器：</span><span class="sxs-lookup"><span data-stu-id="8dad5-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="8dad5-296">（代码段- *ASP.NET 依赖关系注入实验室-Ex02-Register CustomViewPageActivator*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="8dad5-297">将 ASP.NET MVC 4 默认依赖关系解析程序替换为**UnityDependencyResolver**的实例。</span><span class="sxs-lookup"><span data-stu-id="8dad5-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="8dad5-298">为此，请将**Initialize**方法内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8dad5-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="8dad5-299">（代码段- *ASP.NET 依赖关系注入实验室-Ex02-更新依赖关系解析程序*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="8dad5-300">ASP.NET MVC 提供默认的依赖关系解析程序类。</span><span class="sxs-lookup"><span data-stu-id="8dad5-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="8dad5-301">若要使用自定义依赖关系解析程序作为我们为 unity 创建的冲突解决程序，必须替换此解析程序。</span><span class="sxs-lookup"><span data-stu-id="8dad5-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="8dad5-302">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8dad5-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="8dad5-303">在此任务中，你将运行应用程序以验证应用商店浏览器是否使用该服务，并显示所检索的图像和消息：</span><span class="sxs-lookup"><span data-stu-id="8dad5-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="8dad5-304">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="8dad5-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="8dad5-305">单击 "流派" 菜单中的 "**岩石**"，并查看**MessageService**如何注入到视图并加载欢迎消息和图像。</span><span class="sxs-lookup"><span data-stu-id="8dad5-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="8dad5-306">在此示例中，我们将进入 &quot;**摇滚**&quot;：</span><span class="sxs-lookup"><span data-stu-id="8dad5-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="8dad5-307">![MVC 音乐商店-查看注入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC 音乐商店-查看注入")</span><span class="sxs-lookup"><span data-stu-id="8dad5-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="8dad5-308">*MVC 音乐商店-查看注入*</span><span class="sxs-lookup"><span data-stu-id="8dad5-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="8dad5-309">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="8dad5-310">练习3：注入操作筛选器</span><span class="sxs-lookup"><span data-stu-id="8dad5-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="8dad5-311">在以前的动手实验室**自定义操作筛选**器中，你使用了筛选器自定义和注入。</span><span class="sxs-lookup"><span data-stu-id="8dad5-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="8dad5-312">在此练习中，您将学习如何使用 Unity 容器注入具有依赖关系注入的筛选器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="8dad5-313">为此，需要向音乐商店解决方案添加一个自定义操作筛选器，该操作筛选器将跟踪站点的活动。</span><span class="sxs-lookup"><span data-stu-id="8dad5-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="8dad5-314">任务 1-在解决方案中包括跟踪筛选器</span><span class="sxs-lookup"><span data-stu-id="8dad5-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="8dad5-315">在此任务中，你将在音乐存储中包括一个用于跟踪事件的自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="8dad5-316">自定义操作筛选器概念已在以前的实验室中处理 &quot;自定义操作筛选器&quot;，你只需将 filter 类包括在此实验室的 "资产" 文件夹中，然后为 Unity 创建筛选器提供程序：</span><span class="sxs-lookup"><span data-stu-id="8dad5-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="8dad5-317">打开位于 " **Source\Ex03-注入操作 Filter\Begin** " 文件夹中的 "**开始**" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="8dad5-318">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="8dad5-319">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="8dad5-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8dad5-320">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8dad5-321">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="8dad5-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8dad5-322">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="8dad5-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8dad5-323">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="8dad5-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8dad5-324">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="8dad5-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8dad5-325">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="8dad5-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="8dad5-326">有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="8dad5-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="8dad5-327">将**TraceActionFilter.cs**文件从 **/Sources/Assets**添加到 **/Filters**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8dad5-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="8dad5-328">此自定义操作筛选器执行 ASP.NET 跟踪。</span><span class="sxs-lookup"><span data-stu-id="8dad5-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="8dad5-329">可以查看&quot; 实验室 &quot;ASP.NET MVC 4 本地和动态操作筛选器以获取更多参考。</span><span class="sxs-lookup"><span data-stu-id="8dad5-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="8dad5-330">将空类**FilterProvider.cs**添加到 **/Filters.** 文件夹中的项目。</span><span class="sxs-lookup"><span data-stu-id="8dad5-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="8dad5-331">在**FilterProvider.cs**中添加**system.web**和 node.js 命名**空间。**</span><span class="sxs-lookup"><span data-stu-id="8dad5-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="8dad5-332">（代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序添加命名空间*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="8dad5-333">使类继承自**IFilterProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="8dad5-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="8dad5-334">在**FilterProvider**类中添加**IUnityContainer**属性，然后创建类构造函数来分配容器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="8dad5-335">（代码段- *ASP.NET 依赖关系注入实验室-Ex03 提供程序构造函数*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="8dad5-336">筛选器提供程序类构造函数未在中创建**新**的对象。</span><span class="sxs-lookup"><span data-stu-id="8dad5-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="8dad5-337">容器作为参数传递，并且依赖关系由 Unity 解决。</span><span class="sxs-lookup"><span data-stu-id="8dad5-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="8dad5-338">在**FilterProvider**类中，从**IFilterProvider**接口实现方法**GetFilters** 。</span><span class="sxs-lookup"><span data-stu-id="8dad5-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="8dad5-339">（代码段- *ASP.NET 依赖关系注入实验室-Ex03 Provider GetFilters*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="8dad5-340">任务 2-注册并启用筛选器</span><span class="sxs-lookup"><span data-stu-id="8dad5-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="8dad5-341">在此任务中，您将启用站点跟踪。</span><span class="sxs-lookup"><span data-stu-id="8dad5-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="8dad5-342">为此，你将在**Bootstrapper.cs BuildUnityContainer**方法中注册筛选器以启动跟踪：</span><span class="sxs-lookup"><span data-stu-id="8dad5-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="8dad5-343">打开位于项目根目录中**的 web.config，** 并在 system.web 组中启用跟踪跟踪。</span><span class="sxs-lookup"><span data-stu-id="8dad5-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="8dad5-344">在项目根目录中打开**Bootstrapper.cs** 。</span><span class="sxs-lookup"><span data-stu-id="8dad5-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="8dad5-345">添加对**MvcMusicStore**命名空间的引用。</span><span class="sxs-lookup"><span data-stu-id="8dad5-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="8dad5-346">（代码段- *ASP.NET 依赖关系注入实验室-Ex03-引导程序添加命名空间*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="8dad5-347">选择**BuildUnityContainer**方法，并在 Unity 容器中注册筛选器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="8dad5-348">必须注册筛选器提供程序和操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="8dad5-349">（代码段- *ASP.NET 依赖关系注入实验室-Ex03-Register FilterProvider 和 ActionFilter*）</span><span class="sxs-lookup"><span data-stu-id="8dad5-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="8dad5-350">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8dad5-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="8dad5-351">在此任务中，您将运行应用程序并测试自定义操作筛选器是否正在跟踪活动：</span><span class="sxs-lookup"><span data-stu-id="8dad5-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="8dad5-352">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="8dad5-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="8dad5-353">单击 "流派" 菜单中的 "**岩石**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="8dad5-354">如果需要，可以浏览更多流派。</span><span class="sxs-lookup"><span data-stu-id="8dad5-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="8dad5-355">![Music 商店](aspnet-mvc-4-dependency-injection/_static/image11.png "Music 商店")</span><span class="sxs-lookup"><span data-stu-id="8dad5-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="8dad5-356">*Music 商店*</span><span class="sxs-lookup"><span data-stu-id="8dad5-356">*Music Store*</span></span>
3. <span data-ttu-id="8dad5-357">浏览到 **/Trace.axd**以查看 "应用程序跟踪" 页，然后单击 "**查看详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="8dad5-358">![应用程序跟踪日志](aspnet-mvc-4-dependency-injection/_static/image12.png "应用程序跟踪日志")</span><span class="sxs-lookup"><span data-stu-id="8dad5-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="8dad5-359">*应用程序跟踪日志*</span><span class="sxs-lookup"><span data-stu-id="8dad5-359">*Application Trace Log*</span></span>

    <span data-ttu-id="8dad5-360">![应用程序跟踪-请求详细信息](aspnet-mvc-4-dependency-injection/_static/image13.png "应用程序跟踪-请求详细信息")</span><span class="sxs-lookup"><span data-stu-id="8dad5-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="8dad5-361">*应用程序跟踪-请求详细信息*</span><span class="sxs-lookup"><span data-stu-id="8dad5-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="8dad5-362">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="8dad5-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="8dad5-363">摘要</span><span class="sxs-lookup"><span data-stu-id="8dad5-363">Summary</span></span>

<span data-ttu-id="8dad5-364">完成此动手实验后，你已了解如何通过使用 NuGet 包集成 Unity，在 ASP.NET MVC 4 中使用依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="8dad5-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="8dad5-365">为实现此目的，你已在控制器、视图和操作筛选器中使用了依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="8dad5-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="8dad5-366">介绍了以下概念：</span><span class="sxs-lookup"><span data-stu-id="8dad5-366">The following concepts were covered:</span></span>

- <span data-ttu-id="8dad5-367">ASP.NET MVC 4 依赖项注入功能</span><span class="sxs-lookup"><span data-stu-id="8dad5-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="8dad5-368">使用 Unity 进行 unity 集成 Mvc3 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8dad5-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="8dad5-369">控制器中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="8dad5-370">视图中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="8dad5-371">操作筛选器的依赖项注入</span><span class="sxs-lookup"><span data-stu-id="8dad5-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="8dad5-372">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="8dad5-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="8dad5-373">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="8dad5-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="8dad5-374">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="8dad5-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="8dad5-375">转到 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="8dad5-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="8dad5-376">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad5-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="8dad5-377">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-377">Click on **Install Now**.</span></span> <span data-ttu-id="8dad5-378">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="8dad5-379">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="8dad5-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="8dad5-380">![安装 Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="8dad5-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="8dad5-381">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="8dad5-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="8dad5-382">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="8dad5-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="8dad5-384">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="8dad5-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="8dad5-385">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="8dad5-385">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="8dad5-387">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="8dad5-387">*Installation progress*</span></span>
6. <span data-ttu-id="8dad5-388">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="8dad5-388">When the installation completes, click **Finish**.</span></span>

    ![安装完成](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="8dad5-390">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="8dad5-390">*Installation completed*</span></span>
7. <span data-ttu-id="8dad5-391">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="8dad5-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="8dad5-392">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="8dad5-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="8dad5-394">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="8dad5-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="8dad5-395">附录 B：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="8dad5-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="8dad5-396">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="8dad5-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="8dad5-397">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="8dad5-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="8dad5-398">![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-dependency-injection/_static/image19.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="8dad5-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="8dad5-399">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="8dad5-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="8dad5-400">***使用键盘添加代码片段（C#仅限）***</span><span class="sxs-lookup"><span data-stu-id="8dad5-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="8dad5-401">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="8dad5-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="8dad5-402">开始键入代码片段名称（不含空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="8dad5-403">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="8dad5-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="8dad5-404">选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="8dad5-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="8dad5-405">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="8dad5-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="8dad5-406">![开始键入代码片段名称](aspnet-mvc-4-dependency-injection/_static/image20.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="8dad5-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="8dad5-407">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="8dad5-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="8dad5-408">![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-dependency-injection/_static/image21.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="8dad5-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="8dad5-409">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="8dad5-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="8dad5-410">![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-dependency-injection/_static/image22.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="8dad5-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="8dad5-411">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="8dad5-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="8dad5-412">***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2.</span><span class="sxs-lookup"><span data-stu-id="8dad5-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="8dad5-413">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="8dad5-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="8dad5-414">选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。</span><span class="sxs-lookup"><span data-stu-id="8dad5-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="8dad5-415">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="8dad5-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="8dad5-416">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-dependency-injection/_static/image23.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="8dad5-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="8dad5-417">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="8dad5-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="8dad5-418">![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-dependency-injection/_static/image24.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="8dad5-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="8dad5-419">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="8dad5-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
