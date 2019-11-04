---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中使用 EF 读取相关数据
description: 在本教程中，您将读取并显示相关数据，即实体框架加载到导航属性中的数据。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445649"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="9739e-103">教程：在 ASP.NET MVC 应用中使用 EF 读取相关数据</span><span class="sxs-lookup"><span data-stu-id="9739e-103">Tutorial: Read related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="9739e-104">在上一教程中，你已完成 School 数据模型。</span><span class="sxs-lookup"><span data-stu-id="9739e-104">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="9739e-105">在本教程中，您将读取并显示相关数据，即实体框架加载到导航属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-105">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="9739e-106">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="9739e-106">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[<span data-ttu-id="9739e-108">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="9739e-108">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> <span data-ttu-id="9739e-109">Contoso 大学示例 web 应用程序演示了如何使用实体框架 6 Code First 和 Visual Studio 创建 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9739e-109">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio.</span></span> <span data-ttu-id="9739e-110">若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9739e-110">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="9739e-111">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="9739e-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9739e-112">了解如何加载相关数据</span><span class="sxs-lookup"><span data-stu-id="9739e-112">Learn how to load related data</span></span>
> * <span data-ttu-id="9739e-113">创建“课程”页</span><span class="sxs-lookup"><span data-stu-id="9739e-113">Create a Courses page</span></span>
> * <span data-ttu-id="9739e-114">创建“讲师”页</span><span class="sxs-lookup"><span data-stu-id="9739e-114">Create an Instructors page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9739e-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9739e-115">Prerequisites</span></span>

* [<span data-ttu-id="9739e-116">创建更复杂的数据模型</span><span class="sxs-lookup"><span data-stu-id="9739e-116">Create a more complex data model</span></span>](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a><span data-ttu-id="9739e-117">了解如何加载相关数据</span><span class="sxs-lookup"><span data-stu-id="9739e-117">Learn how to load related data</span></span>

<span data-ttu-id="9739e-118">实体框架可以通过多种方式将相关数据加载到实体的导航属性中：</span><span class="sxs-lookup"><span data-stu-id="9739e-118">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="9739e-119">*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="9739e-119">*Lazy loading*.</span></span> <span data-ttu-id="9739e-120">首次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-120">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="9739e-121">然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-121">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="9739e-122">这会导致向数据库发送多个查询，一个用于实体本身，每次必须检索到该实体的相关数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-122">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> <span data-ttu-id="9739e-123">默认情况下，`DbContext` 类启用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-123">The `DbContext` class enables lazy loading by default.</span></span>

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="9739e-125">*预先加载*。</span><span class="sxs-lookup"><span data-stu-id="9739e-125">*Eager loading*.</span></span> <span data-ttu-id="9739e-126">读取该实体时，会同时检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-126">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="9739e-127">此时通常会出现单一联接查询，检索所有必需数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-127">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="9739e-128">使用 `Include` 方法指定预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-128">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="9739e-130">*显式加载*。</span><span class="sxs-lookup"><span data-stu-id="9739e-130">*Explicit loading*.</span></span> <span data-ttu-id="9739e-131">这类似于延迟加载，只不过是在代码中显式检索相关数据;在访问导航属性时，不会自动发生此情况。</span><span class="sxs-lookup"><span data-stu-id="9739e-131">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="9739e-132">通过获取实体的对象状态管理器条目并调用集合，可以手动加载相关数据[。](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)用于集合的 load 方法或用于保存单个实体的属性的[load 方法。](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="9739e-132">You load related data manually by getting the object state manager entry for an entity and calling the [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) method for collections or the [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) method for properties that hold a single entity.</span></span> <span data-ttu-id="9739e-133">（在以下示例中，如果想要加载 "管理员" 导航属性，请将 `Collection(x => x.Courses)` 替换为 `Reference(x => x.Administrator)`。）通常，仅当关闭延迟加载时才使用显式加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-133">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.) Typically you'd use explicit loading only when you've turned lazy loading off.</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="9739e-135">因为它们不会立即检索属性值，所以延迟加载和显式加载也称为*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="9739e-135">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

### <a name="performance-considerations"></a><span data-ttu-id="9739e-136">性能注意事项</span><span class="sxs-lookup"><span data-stu-id="9739e-136">Performance considerations</span></span>

<span data-ttu-id="9739e-137">如果知道自己需要每个检索的实体的相关数据，选择预先加载可获得最佳性能，因为相比每个检索的实体的单独查询，发送到数据库的单个查询更加有效。</span><span class="sxs-lookup"><span data-stu-id="9739e-137">If you know you need related data for every entity retrieved, eager loading often offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="9739e-138">例如，在上面的示例中，假设每个部门都有十个相关的课程。</span><span class="sxs-lookup"><span data-stu-id="9739e-138">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="9739e-139">预先加载的示例会生成一个（联接）查询和一个到数据库的单次往返。</span><span class="sxs-lookup"><span data-stu-id="9739e-139">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="9739e-140">延迟加载和显式加载示例会导致对数据库进行11次查询和十一次往返。</span><span class="sxs-lookup"><span data-stu-id="9739e-140">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="9739e-141">延迟较高时，额外往返数据库对性能尤为不利。</span><span class="sxs-lookup"><span data-stu-id="9739e-141">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="9739e-142">另一方面，在某些情况下，延迟加载更为有效。</span><span class="sxs-lookup"><span data-stu-id="9739e-142">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="9739e-143">预先加载可能会导致生成非常复杂的联接，这 SQL Server 无法有效地处理。</span><span class="sxs-lookup"><span data-stu-id="9739e-143">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="9739e-144">或者，如果您需要只为正在处理的一组实体的子集访问实体的导航属性，则延迟加载可能会更好，因为预先加载将检索比您所需的数据更多的数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-144">Or if you need to access an entity's navigation properties only for a subset of a set of the entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="9739e-145">如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。</span><span class="sxs-lookup"><span data-stu-id="9739e-145">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="9739e-146">延迟加载可以屏蔽导致性能问题的代码。</span><span class="sxs-lookup"><span data-stu-id="9739e-146">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="9739e-147">例如，如果代码未指定预先加载或未显式加载，但处理大量实体，并且在每次迭代中使用多个导航属性，则可能会非常低效（因为与数据库之间的往返次数很多）。</span><span class="sxs-lookup"><span data-stu-id="9739e-147">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="9739e-148">使用本地 SQL server 进行开发良好的应用程序在迁移到 Azure SQL 数据库时可能会遇到性能问题，因为这会增加延迟和延迟加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-148">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="9739e-149">使用真实的测试负载分析数据库查询将有助于确定是否适合延迟加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-149">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="9739e-150">有关详细信息，请参阅[揭密实体框架策略：加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx)和[使用实体框架将网络延迟减少到 SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9739e-150">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

### <a name="disable-lazy-loading-before-serialization"></a><span data-ttu-id="9739e-151">在序列化之前禁用延迟加载</span><span class="sxs-lookup"><span data-stu-id="9739e-151">Disable lazy loading before serialization</span></span>

<span data-ttu-id="9739e-152">如果在序列化过程中使延迟加载处于启用状态，最终可以查询比预期更多的数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-152">If you leave lazy loading enabled during serialization, you can end up querying significantly more data than you intended.</span></span> <span data-ttu-id="9739e-153">序列化通常通过访问类型实例上的每个属性来工作。</span><span class="sxs-lookup"><span data-stu-id="9739e-153">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="9739e-154">属性访问会触发延迟加载，并且会序列化这些延迟加载的实体。</span><span class="sxs-lookup"><span data-stu-id="9739e-154">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="9739e-155">然后，序列化过程访问延迟加载的实体的每个属性，这可能会导致更多的延迟加载和序列化。</span><span class="sxs-lookup"><span data-stu-id="9739e-155">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="9739e-156">若要防止此运行时链反应，请在序列化实体之前关闭延迟加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-156">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="9739e-157">序列化还可能会由于实体框架使用的代理类而变得很复杂，如[高级方案教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)中所述。</span><span class="sxs-lookup"><span data-stu-id="9739e-157">Serialization can also be complicated by the proxy classes that the Entity Framework uses, as explained in the [Advanced Scenarios tutorial](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).</span></span>

<span data-ttu-id="9739e-158">避免序列化问题的一种方法是序列化数据传输对象（Dto）而不是实体对象，如[使用带有实体框架的 WEB API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教程中所示。</span><span class="sxs-lookup"><span data-stu-id="9739e-158">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) tutorial.</span></span>

<span data-ttu-id="9739e-159">如果不使用 Dto，则可以禁用延迟加载，并通过[禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)来避免代理问题。</span><span class="sxs-lookup"><span data-stu-id="9739e-159">If you don't use DTOs, you can disable lazy loading and avoid proxy issues by [disabling proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>

<span data-ttu-id="9739e-160">以下是[禁用延迟加载](https://msdn.microsoft.com/data/jj574232)的其他一些方法：</span><span class="sxs-lookup"><span data-stu-id="9739e-160">Here are some other [ways to disable lazy loading](https://msdn.microsoft.com/data/jj574232):</span></span>

- <span data-ttu-id="9739e-161">对于特定的导航属性，请在声明属性时省略 `virtual` 关键字。</span><span class="sxs-lookup"><span data-stu-id="9739e-161">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="9739e-162">对于所有导航属性，将 `LazyLoadingEnabled` 设置为 `false`，将以下代码放在上下文类的构造函数中：</span><span class="sxs-lookup"><span data-stu-id="9739e-162">For all navigation properties, set `LazyLoadingEnabled` to `false`, put the following code in the constructor of your context class:</span></span>

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a><span data-ttu-id="9739e-163">创建“课程”页</span><span class="sxs-lookup"><span data-stu-id="9739e-163">Create a Courses page</span></span>

<span data-ttu-id="9739e-164">`Course` 实体包含一个导航属性，该属性包含将课程分配到的部门的 `Department` 实体。</span><span class="sxs-lookup"><span data-stu-id="9739e-164">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="9739e-165">若要在课程列表中显示分配的部门的名称，需要从 `Course.Department` 导航属性中的 `Department` 实体获取 `Name` 属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-165">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="9739e-166">使用之前用于 `Student` 控制器的实体框架 scaffolder，为 `Course` 实体类型创建一个名为 `CourseController` （不是 CoursesController）的控制器，同时使用**与视图相同的 MVC 5 控制器**选项：</span><span class="sxs-lookup"><span data-stu-id="9739e-166">Create a controller named `CourseController` (not CoursesController) for the `Course` entity type, using the same options for the **MVC 5 Controller with views, using Entity Framework** scaffolder that you did earlier for the `Student` controller:</span></span>

| <span data-ttu-id="9739e-167">设置</span><span class="sxs-lookup"><span data-stu-id="9739e-167">Setting</span></span> | <span data-ttu-id="9739e-168">“值”</span><span class="sxs-lookup"><span data-stu-id="9739e-168">Value</span></span> |
| ------- | ----- |
| <span data-ttu-id="9739e-169">模型类</span><span class="sxs-lookup"><span data-stu-id="9739e-169">Model class</span></span> | <span data-ttu-id="9739e-170">选择**课程（ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="9739e-170">Select **Course (ContosoUniversity.Models)**.</span></span> |
| <span data-ttu-id="9739e-171">数据上下文类</span><span class="sxs-lookup"><span data-stu-id="9739e-171">Data context class</span></span> | <span data-ttu-id="9739e-172">选择**SchoolContext （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="9739e-172">Select **SchoolContext (ContosoUniversity.DAL)**.</span></span> |
| <span data-ttu-id="9739e-173">控制器名称</span><span class="sxs-lookup"><span data-stu-id="9739e-173">Controller name</span></span> | <span data-ttu-id="9739e-174">输入*CourseController*。</span><span class="sxs-lookup"><span data-stu-id="9739e-174">Enter *CourseController*.</span></span> <span data-ttu-id="9739e-175">同样，不*CoursesController* *。*</span><span class="sxs-lookup"><span data-stu-id="9739e-175">Again, not *CoursesController* with an *s*.</span></span> <span data-ttu-id="9739e-176">选择 "**课程（ContosoUniversity）** " 时，将自动填充 "**控制器名称**" 值。</span><span class="sxs-lookup"><span data-stu-id="9739e-176">When you selected **Course (ContosoUniversity.Models)**, the **Controller name** value was automatically populated.</span></span> <span data-ttu-id="9739e-177">必须更改该值。</span><span class="sxs-lookup"><span data-stu-id="9739e-177">You have to change the value.</span></span> |

<span data-ttu-id="9739e-178">保留其他默认值并添加控制器。</span><span class="sxs-lookup"><span data-stu-id="9739e-178">Leave the other default values and add the controller.</span></span>

<span data-ttu-id="9739e-179">打开*Controllers\CourseController.cs*并查看 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="9739e-179">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="9739e-180">自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-180">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="9739e-181">打开*Views\Course\Index.cshtml* ，将模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="9739e-181">Open *Views\Course\Index.cshtml* and replace the template code with the following code.</span></span> <span data-ttu-id="9739e-182">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="9739e-182">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

<span data-ttu-id="9739e-183">已对基架代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="9739e-183">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="9739e-184">将标题从**索引**更改为**课程**。</span><span class="sxs-lookup"><span data-stu-id="9739e-184">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="9739e-185">添加了显示 `CourseID` 属性值的“数字”列。</span><span class="sxs-lookup"><span data-stu-id="9739e-185">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="9739e-186">默认情况下，主键不基架，因为它们对于最终用户没有意义。</span><span class="sxs-lookup"><span data-stu-id="9739e-186">By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="9739e-187">但在这种情况下主键是有意义的，而你需要将其呈现出来。</span><span class="sxs-lookup"><span data-stu-id="9739e-187">However, in this case the primary key is meaningful and you want to show it.</span></span>
- <span data-ttu-id="9739e-188">将 "**部门**" 列移动到右侧，并更改其标题。</span><span class="sxs-lookup"><span data-stu-id="9739e-188">Moved the **Department** column to the right side and changed its heading.</span></span> <span data-ttu-id="9739e-189">Scaffolder 正确地选择了从 `Department` 实体显示 `Name` 属性，但在课程页面中，列标题应为 "**部门**" 而不是 "**名称**"。</span><span class="sxs-lookup"><span data-stu-id="9739e-189">The scaffolder correctly chose to display the `Name` property from the `Department` entity, but here in the Course page the column heading should be **Department** rather than **Name**.</span></span>

<span data-ttu-id="9739e-190">请注意，对于 "部门" 列，基架代码显示加载到 `Department` 导航属性中的 `Department` 实体的 `Name` 属性：</span><span class="sxs-lookup"><span data-stu-id="9739e-190">Notice that for the Department column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="9739e-191">运行页面（在 Contoso 大学主页上选择 "**课程**" 选项卡），查看具有部门名称的列表。</span><span class="sxs-lookup"><span data-stu-id="9739e-191">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

## <a name="create-an-instructors-page"></a><span data-ttu-id="9739e-192">创建“讲师”页</span><span class="sxs-lookup"><span data-stu-id="9739e-192">Create an Instructors page</span></span>

<span data-ttu-id="9739e-193">在本部分中，你将为 `Instructor` 实体创建一个控制器和视图，以便显示 "讲师" 页。</span><span class="sxs-lookup"><span data-stu-id="9739e-193">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors page.</span></span> <span data-ttu-id="9739e-194">该页面通过以下方式读取和显示相关数据：</span><span class="sxs-lookup"><span data-stu-id="9739e-194">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="9739e-195">讲师列表显示 `OfficeAssignment` 实体中的相关数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-195">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="9739e-196">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="9739e-196">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="9739e-197">你将对 `OfficeAssignment` 实体使用预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-197">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="9739e-198">如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。</span><span class="sxs-lookup"><span data-stu-id="9739e-198">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="9739e-199">在这种情况下，你希望显示所有显示的讲师的办公室分配情况。</span><span class="sxs-lookup"><span data-stu-id="9739e-199">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="9739e-200">用户选择一名讲师时，显示相关 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="9739e-200">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="9739e-201">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="9739e-201">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="9739e-202">你将对 `Course` 实体及其相关 `Department` 实体使用预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-202">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="9739e-203">在这种情况下，延迟加载可能更高效，因为你只需要为所选指导员提供课程。</span><span class="sxs-lookup"><span data-stu-id="9739e-203">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="9739e-204">但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-204">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="9739e-205">当用户选择一门课程时，将显示 `Enrollments` 实体集中的相关数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-205">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="9739e-206">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="9739e-206">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="9739e-207">你将为 `Enrollment` 实体及其相关 `Student` 实体添加显式加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-207">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="9739e-208">（由于启用了延迟加载，因此不需要显式加载，但这会显示如何进行显式加载。）</span><span class="sxs-lookup"><span data-stu-id="9739e-208">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="9739e-209">为讲师索引视图创建视图模型</span><span class="sxs-lookup"><span data-stu-id="9739e-209">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="9739e-210">"讲师" 页显示三个不同的表。</span><span class="sxs-lookup"><span data-stu-id="9739e-210">The Instructors page shows three different tables.</span></span> <span data-ttu-id="9739e-211">因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-211">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="9739e-212">在*viewmodel*文件夹中，创建*InstructorIndexData.cs*并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9739e-212">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a><span data-ttu-id="9739e-213">创建讲师控制器和视图</span><span class="sxs-lookup"><span data-stu-id="9739e-213">Create the Instructor Controller and Views</span></span>

<span data-ttu-id="9739e-214">使用 EF 读取/写入操作创建 `InstructorController` （而非 InstructorsController）控制器：</span><span class="sxs-lookup"><span data-stu-id="9739e-214">Create an `InstructorController` (not InstructorsController) controller with EF read/write action:</span></span>

| <span data-ttu-id="9739e-215">设置</span><span class="sxs-lookup"><span data-stu-id="9739e-215">Setting</span></span> | <span data-ttu-id="9739e-216">“值”</span><span class="sxs-lookup"><span data-stu-id="9739e-216">Value</span></span> |
| ------- | ----- |
| <span data-ttu-id="9739e-217">模型类</span><span class="sxs-lookup"><span data-stu-id="9739e-217">Model class</span></span> | <span data-ttu-id="9739e-218">选择 "**指导员" （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="9739e-218">Select **Instructor (ContosoUniversity.Models)**.</span></span> |
| <span data-ttu-id="9739e-219">数据上下文类</span><span class="sxs-lookup"><span data-stu-id="9739e-219">Data context class</span></span> | <span data-ttu-id="9739e-220">选择**SchoolContext （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="9739e-220">Select **SchoolContext (ContosoUniversity.DAL)**.</span></span> |
| <span data-ttu-id="9739e-221">控制器名称</span><span class="sxs-lookup"><span data-stu-id="9739e-221">Controller name</span></span> | <span data-ttu-id="9739e-222">输入*InstructorController*。</span><span class="sxs-lookup"><span data-stu-id="9739e-222">Enter *InstructorController*.</span></span> <span data-ttu-id="9739e-223">同样，不*InstructorsController* *。*</span><span class="sxs-lookup"><span data-stu-id="9739e-223">Again, not *InstructorsController* with an *s*.</span></span> <span data-ttu-id="9739e-224">选择 "**课程（ContosoUniversity）** " 时，将自动填充 "**控制器名称**" 值。</span><span class="sxs-lookup"><span data-stu-id="9739e-224">When you selected **Course (ContosoUniversity.Models)**, the **Controller name** value was automatically populated.</span></span> <span data-ttu-id="9739e-225">必须更改该值。</span><span class="sxs-lookup"><span data-stu-id="9739e-225">You have to change the value.</span></span> |

<span data-ttu-id="9739e-226">保留其他默认值并添加控制器。</span><span class="sxs-lookup"><span data-stu-id="9739e-226">Leave the other default values and add the controller.</span></span>

<span data-ttu-id="9739e-227">打开*Controllers\InstructorController.cs* ，并为 `ViewModels` 命名空间添加 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="9739e-227">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="9739e-228">`Index` 方法中的基架代码仅指定 `OfficeAssignment` 导航属性的预先加载：</span><span class="sxs-lookup"><span data-stu-id="9739e-228">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="9739e-229">将 `Index` 方法替换为以下代码，以加载其他相关数据并将其放入视图模型：</span><span class="sxs-lookup"><span data-stu-id="9739e-229">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="9739e-230">方法接受可选的路由数据（`id`）和查询字符串参数（`courseID`），该参数提供选定讲师和所选课程的 ID 值，并将所有所需数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="9739e-230">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="9739e-231">参数由页面上的“选择”超链接提供。</span><span class="sxs-lookup"><span data-stu-id="9739e-231">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

<span data-ttu-id="9739e-232">代码先创建一个视图模型实例，并在其中放入讲师列表。</span><span class="sxs-lookup"><span data-stu-id="9739e-232">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="9739e-233">此代码为 `Instructor.OfficeAssignment` 和 `Instructor.Courses` 导航属性指定预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-233">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="9739e-234">第二个 `Include` 方法将加载课程，对于加载的每个课程，它会预先加载 `Course.Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-234">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="9739e-235">如前所述，无需预先加载，但会执行此操作来提高性能。</span><span class="sxs-lookup"><span data-stu-id="9739e-235">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="9739e-236">由于视图始终需要 `OfficeAssignment` 实体，因此在同一查询中提取该视图会更有效。</span><span class="sxs-lookup"><span data-stu-id="9739e-236">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="9739e-237">当在网页中选择了指导员时，`Course` 实体是必需的，因此，只有在选择了比不使用的课程更频繁地显示页面时，预先加载比延迟加载更好。</span><span class="sxs-lookup"><span data-stu-id="9739e-237">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="9739e-238">如果选择了指导员 ID，则会从视图模型中的指导员列表中检索所选的指导员。</span><span class="sxs-lookup"><span data-stu-id="9739e-238">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="9739e-239">然后，将从该教师 `Courses` 导航属性中的 `Course` 实体加载视图模型的 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-239">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="9739e-240">`Where` 方法返回一个集合，但在此示例中，传递给该方法的条件仅导致返回单个 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="9739e-240">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="9739e-241">`Single` 方法将集合转换为单个 `Instructor` 实体，这使你能够访问该实体的 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-241">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="9739e-242">当您知道集合将只有一个项时，对集合使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="9739e-242">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="9739e-243">如果传递给它的集合为空或有多个项，则 `Single` 方法会引发异常。</span><span class="sxs-lookup"><span data-stu-id="9739e-243">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="9739e-244">替代项为[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，如果集合为空，则返回默认值（在本例中为`null`）。</span><span class="sxs-lookup"><span data-stu-id="9739e-244">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="9739e-245">但是，在这种情况下，仍会引发异常（尝试在 `null` 引用上查找 `Courses` 属性），并且异常消息不会明确指出问题的原因。</span><span class="sxs-lookup"><span data-stu-id="9739e-245">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="9739e-246">调用 `Single` 方法时，还可以传入 `Where` 条件，而不是单独调用 `Where` 方法：</span><span class="sxs-lookup"><span data-stu-id="9739e-246">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="9739e-247">而不是：</span><span class="sxs-lookup"><span data-stu-id="9739e-247">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="9739e-248">接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。</span><span class="sxs-lookup"><span data-stu-id="9739e-248">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="9739e-249">然后，将通过该课程 `Enrollments` 导航属性中的 `Enrollment` 实体加载视图模型的 `Enrollments` 属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-249">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a><span data-ttu-id="9739e-250">修改讲师索引视图</span><span class="sxs-lookup"><span data-stu-id="9739e-250">Modify the Instructor Index View</span></span>

<span data-ttu-id="9739e-251">在*Views\Instructor\Index.cshtml*中，将模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="9739e-251">In *Views\Instructor\Index.cshtml*, replace the template code with the following code.</span></span> <span data-ttu-id="9739e-252">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="9739e-252">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

<span data-ttu-id="9739e-253">已对现有代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="9739e-253">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="9739e-254">将模型类更改为了 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="9739e-254">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="9739e-255">将页标题从“索引”更改为了“讲师”。</span><span class="sxs-lookup"><span data-stu-id="9739e-255">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="9739e-256">添加了仅当 `item.OfficeAssignment` 不为 null 时才显示 `item.OfficeAssignment.Location` 的**Office**列。</span><span class="sxs-lookup"><span data-stu-id="9739e-256">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="9739e-257">（由于这是一对零或一的关系，因此可能没有相关的 `OfficeAssignment` 实体。）</span><span class="sxs-lookup"><span data-stu-id="9739e-257">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span>

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- <span data-ttu-id="9739e-258">添加了将 `class="success"` 动态添加到选定讲师的 `tr` 元素中的代码。</span><span class="sxs-lookup"><span data-stu-id="9739e-258">Added code that will dynamically add `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="9739e-259">这将使用[启动](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)类设置所选行的背景色。</span><span class="sxs-lookup"><span data-stu-id="9739e-259">This sets a background color for the selected row using a [Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) class.</span></span>

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- <span data-ttu-id="9739e-260">添加了在每行中的其他链接之前标记为 "**选择**" 的新 `ActionLink`，这将导致所选的指导员 ID 发送到 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="9739e-260">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="9739e-261">运行应用程序并选择 "**讲师**" 选项卡。当没有相关的 `OfficeAssignment` 实体时，此页将显示相关 `OfficeAssignment` 实体的 `Location` 属性和一个空的表单元。</span><span class="sxs-lookup"><span data-stu-id="9739e-261">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

<span data-ttu-id="9739e-262">在*Views\Instructor\Index.cshtml*文件中，在关闭 `table` 元素（位于文件末尾）后面添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="9739e-262">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following code.</span></span> <span data-ttu-id="9739e-263">选择讲师时，此代码显示与讲师相关的课程列表。</span><span class="sxs-lookup"><span data-stu-id="9739e-263">This code displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="9739e-264">此代码读取视图模型的 `Courses` 属性以显示课程列表。</span><span class="sxs-lookup"><span data-stu-id="9739e-264">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="9739e-265">它还提供了一个 `Select` 超链接，该超链接将所选课程的 ID 发送到 `Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="9739e-265">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

<span data-ttu-id="9739e-266">运行页面并选择一个指导员。</span><span class="sxs-lookup"><span data-stu-id="9739e-266">Run the page and select an instructor.</span></span> <span data-ttu-id="9739e-267">此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。</span><span class="sxs-lookup"><span data-stu-id="9739e-267">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

<span data-ttu-id="9739e-268">在刚刚添加的代码块后，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="9739e-268">After the code block you just added, add the following code.</span></span> <span data-ttu-id="9739e-269">选择课程后，代码将显示参与课程的学生列表。</span><span class="sxs-lookup"><span data-stu-id="9739e-269">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="9739e-270">此代码读取视图模型的 `Enrollments` 属性，以显示课程中注册的学生列表。</span><span class="sxs-lookup"><span data-stu-id="9739e-270">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="9739e-271">运行页面并选择一个指导员。</span><span class="sxs-lookup"><span data-stu-id="9739e-271">Run the page and select an instructor.</span></span> <span data-ttu-id="9739e-272">然后选择一门课程，查看参与的学生列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="9739e-272">Then select a course to see the list of enrolled students and their grades.</span></span>

### <a name="adding-explicit-loading"></a><span data-ttu-id="9739e-273">添加显式加载</span><span class="sxs-lookup"><span data-stu-id="9739e-273">Adding Explicit Loading</span></span>

<span data-ttu-id="9739e-274">打开*InstructorController.cs* ，查看 `Index` 方法如何获取所选课程的注册列表：</span><span class="sxs-lookup"><span data-stu-id="9739e-274">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="9739e-275">检索到讲师列表时，你为 `Courses` 导航属性指定了预先加载，并为每个课程的 `Department` 属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-275">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="9739e-276">然后，将 `Courses` 集合放置在视图模型中，现在将从该集合中的一个实体访问 `Enrollments` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-276">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="9739e-277">由于未指定 `Course.Enrollments` 导航属性的预先加载，因此，该属性中的数据将作为延迟加载的结果出现在页面中。</span><span class="sxs-lookup"><span data-stu-id="9739e-277">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="9739e-278">如果在未以任何其他方式更改代码的情况下禁用延迟加载，则无论该课程实际具有多少注册，`Enrollments` 属性都将为 null。</span><span class="sxs-lookup"><span data-stu-id="9739e-278">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="9739e-279">在这种情况下，若要加载 `Enrollments` 属性，必须指定预先加载或显式加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-279">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="9739e-280">您已经了解了如何执行预先加载。</span><span class="sxs-lookup"><span data-stu-id="9739e-280">You've already seen how to do eager loading.</span></span> <span data-ttu-id="9739e-281">若要查看显式加载的示例，请将 `Index` 方法替换为以下代码，这会显式加载 `Enrollments` 属性。</span><span class="sxs-lookup"><span data-stu-id="9739e-281">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="9739e-282">更改的代码已突出显示。</span><span class="sxs-lookup"><span data-stu-id="9739e-282">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

<span data-ttu-id="9739e-283">获取所选 `Course` 实体后，新代码将显式加载该课程的 `Enrollments` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="9739e-283">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="9739e-284">然后，它显式加载每个 `Enrollment` 实体的相关 `Student` 实体：</span><span class="sxs-lookup"><span data-stu-id="9739e-284">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="9739e-285">请注意，使用 `Collection` 方法加载集合属性，但对于只包含一个实体的属性，则使用 `Reference` 方法。</span><span class="sxs-lookup"><span data-stu-id="9739e-285">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span>

<span data-ttu-id="9739e-286">立即运行讲师索引页，您将看到页面上显示的内容没有任何区别，不过您已经更改了数据的检索方式。</span><span class="sxs-lookup"><span data-stu-id="9739e-286">Run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="9739e-287">获取代码</span><span class="sxs-lookup"><span data-stu-id="9739e-287">Get the code</span></span>

[<span data-ttu-id="9739e-288">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="9739e-288">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="9739e-289">其他资源</span><span class="sxs-lookup"><span data-stu-id="9739e-289">Additional resources</span></span>

<span data-ttu-id="9739e-290">可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="9739e-290">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9739e-291">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9739e-291">Next steps</span></span>

<span data-ttu-id="9739e-292">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="9739e-292">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9739e-293">已了解如何加载相关数据</span><span class="sxs-lookup"><span data-stu-id="9739e-293">Learned how to load related data</span></span>
> * <span data-ttu-id="9739e-294">已创建“课程”页</span><span class="sxs-lookup"><span data-stu-id="9739e-294">Created a Courses page</span></span>
> * <span data-ttu-id="9739e-295">已创建“讲师”页</span><span class="sxs-lookup"><span data-stu-id="9739e-295">Created an Instructors page</span></span>

<span data-ttu-id="9739e-296">请继续阅读下一篇文章，了解如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="9739e-296">Advance to the next article to learn how to update related data.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9739e-297">更新相关数据</span><span class="sxs-lookup"><span data-stu-id="9739e-297">Update related data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
