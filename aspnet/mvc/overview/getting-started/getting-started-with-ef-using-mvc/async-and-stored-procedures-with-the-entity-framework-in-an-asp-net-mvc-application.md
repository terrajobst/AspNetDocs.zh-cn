---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中将 async 和存储过程与 EF 配合使用
description: 在本教程中，您将了解如何实现异步编程模型并了解如何使用存储过程。
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471386"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="ffb39-103">教程：在 ASP.NET MVC 应用中将 async 和存储过程与 EF 配合使用</span><span class="sxs-lookup"><span data-stu-id="ffb39-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="ffb39-104">在前面的教程中，您学习了如何使用同步编程模型读取和更新数据。</span><span class="sxs-lookup"><span data-stu-id="ffb39-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="ffb39-105">在本教程中，您将了解如何实现异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="ffb39-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="ffb39-106">异步代码有助于提高应用程序的性能，因为它可以更好地利用服务器资源。</span><span class="sxs-lookup"><span data-stu-id="ffb39-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="ffb39-107">在本教程中，你还将了解如何在实体上使用存储过程执行插入、更新和删除操作。</span><span class="sxs-lookup"><span data-stu-id="ffb39-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="ffb39-108">最后，将应用程序重新部署到 Azure，以及自首次部署后实现的所有数据库更改。</span><span class="sxs-lookup"><span data-stu-id="ffb39-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="ffb39-109">下图是一些将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="ffb39-109">The following illustrations show some of the pages that you'll work with.</span></span>

![部门页面](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![创建部门](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="ffb39-112">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="ffb39-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ffb39-113">了解异步代码</span><span class="sxs-lookup"><span data-stu-id="ffb39-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="ffb39-114">创建部门控制器</span><span class="sxs-lookup"><span data-stu-id="ffb39-114">Create a Department controller</span></span>
> * <span data-ttu-id="ffb39-115">使用存储过程</span><span class="sxs-lookup"><span data-stu-id="ffb39-115">Use stored procedures</span></span>
> * <span data-ttu-id="ffb39-116">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="ffb39-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffb39-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="ffb39-117">Prerequisites</span></span>

* [<span data-ttu-id="ffb39-118">更新相关数据</span><span class="sxs-lookup"><span data-stu-id="ffb39-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="ffb39-119">为什么使用异步代码</span><span class="sxs-lookup"><span data-stu-id="ffb39-119">Why use asynchronous code</span></span>

<span data-ttu-id="ffb39-120">Web 服务器的可用线程是有限的，而在高负载情况下的可能所有线程都被占用。</span><span class="sxs-lookup"><span data-stu-id="ffb39-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="ffb39-121">当发生这种情况的时候，服务器就无法处理新请求，直到线程被释放。</span><span class="sxs-lookup"><span data-stu-id="ffb39-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="ffb39-122">使用同步代码时，可能会出现多个线程被占用但不能执行任何操作的情况，因为它们正在等待 I/O 完成。</span><span class="sxs-lookup"><span data-stu-id="ffb39-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="ffb39-123">使用异步代码时，当进程正在等待 I/O 完成，服务器可以将其线程释放用于处理其他请求。</span><span class="sxs-lookup"><span data-stu-id="ffb39-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="ffb39-124">因此，异步代码使服务器资源的使用效率更高，并使服务器能够处理更多的流量，而无需延迟。</span><span class="sxs-lookup"><span data-stu-id="ffb39-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="ffb39-125">在较早版本的 .NET 中，编写和测试异步代码非常复杂、容易出错且难以调试。</span><span class="sxs-lookup"><span data-stu-id="ffb39-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="ffb39-126">在 .NET 4.5 中，编写、测试和调试异步代码非常简单，通常应该编写异步代码，除非您有理由不这样做。</span><span class="sxs-lookup"><span data-stu-id="ffb39-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="ffb39-127">异步代码会引入少量的开销，但对于低流量情况，性能下降可能会忽略不计，而在高流量情况下，可能会显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="ffb39-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="ffb39-128">有关异步编程的详细信息，请参阅[使用 .net 4.5 的异步支持以避免阻止调用](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)。</span><span class="sxs-lookup"><span data-stu-id="ffb39-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="ffb39-129">创建部门控制器</span><span class="sxs-lookup"><span data-stu-id="ffb39-129">Create Department controller</span></span>

<span data-ttu-id="ffb39-130">使用与之前相同的控制器相同的方式创建部门控制器，但这次请选择 "**使用异步控制器操作**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="ffb39-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="ffb39-131">以下突出显示了向同步代码添加的 `Index` 方法的同步代码，以使其实现异步操作：</span><span class="sxs-lookup"><span data-stu-id="ffb39-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="ffb39-132">应用了四项更改，使实体框架的数据库查询异步执行：</span><span class="sxs-lookup"><span data-stu-id="ffb39-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="ffb39-133">方法标记有 `async` 关键字，该关键字告诉编译器为方法体的各部分生成回调并自动创建返回的 `Task<ActionResult>` 对象。</span><span class="sxs-lookup"><span data-stu-id="ffb39-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="ffb39-134">返回类型已从 `ActionResult` 更改为 `Task<ActionResult>`。</span><span class="sxs-lookup"><span data-stu-id="ffb39-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="ffb39-135">`Task<T>` 类型表示正在进行的工作与类型 `T`的结果。</span><span class="sxs-lookup"><span data-stu-id="ffb39-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="ffb39-136">`await` 关键字已应用于 web 服务调用。</span><span class="sxs-lookup"><span data-stu-id="ffb39-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="ffb39-137">当编译器在幕后看到此关键字时，它会将方法拆分为两个部分。</span><span class="sxs-lookup"><span data-stu-id="ffb39-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="ffb39-138">第一个部分以异步方式启动的操作结束。</span><span class="sxs-lookup"><span data-stu-id="ffb39-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="ffb39-139">第二部分放入回调方法，该方法将在操作完成时调用。</span><span class="sxs-lookup"><span data-stu-id="ffb39-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="ffb39-140">调用 `ToList` 扩展方法的异步版本。</span><span class="sxs-lookup"><span data-stu-id="ffb39-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="ffb39-141">为什么 `departments.ToList` 语句已修改但不是 `departments = db.Departments` 语句？</span><span class="sxs-lookup"><span data-stu-id="ffb39-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="ffb39-142">原因在于，只有导致查询或命令发送到数据库的语句以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="ffb39-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="ffb39-143">`departments = db.Departments` 语句设置查询，但在调用 `ToList` 方法之前不会执行查询。</span><span class="sxs-lookup"><span data-stu-id="ffb39-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="ffb39-144">因此，仅异步执行 `ToList` 方法。</span><span class="sxs-lookup"><span data-stu-id="ffb39-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="ffb39-145">在 `Details` 方法和 `HttpGet` `Edit` 和 `Delete` 方法中，`Find` 方法是导致查询发送到数据库的方法，因此这是异步执行的方法：</span><span class="sxs-lookup"><span data-stu-id="ffb39-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="ffb39-146">在 `Create`、`HttpPost Edit`和 `DeleteConfirmed` 方法中，这是导致执行命令的 `SaveChanges` 方法调用，而不是仅导致内存中的实体被修改的语句（例如 `db.Departments.Add(department)`）。</span><span class="sxs-lookup"><span data-stu-id="ffb39-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="ffb39-147">打开*Views\Department\Index.cshtml*，将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="ffb39-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="ffb39-148">此代码会将标题从 "索引" 更改为 "部门"，将管理员名称移动到右侧，并提供管理员的全名。</span><span class="sxs-lookup"><span data-stu-id="ffb39-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="ffb39-149">在 "创建"、"删除"、"详细信息" 和 "编辑" 视图中，将 "`InstructorID`" 字段的标题更改为 "Administrator"，这与在课程视图中将 "部门名称" 字段更改为 "部门" 的方式相同。</span><span class="sxs-lookup"><span data-stu-id="ffb39-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="ffb39-150">在 "创建" 和 "编辑" 视图中，使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="ffb39-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="ffb39-151">在 "删除" 和 "详细信息" 视图中，使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="ffb39-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="ffb39-152">运行应用程序，然后单击 "**部门**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffb39-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="ffb39-153">一切与其他控制器中的工作方式相同，但在此控制器中，所有 SQL 查询都以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="ffb39-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="ffb39-154">使用实体框架的异步编程时需要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="ffb39-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="ffb39-155">异步代码不是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="ffb39-155">The async code is not thread safe.</span></span> <span data-ttu-id="ffb39-156">换言之，换言之，不要尝试使用同一个上下文实例并行执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="ffb39-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="ffb39-157">如果你想要利用异步代码的性能优势，请确保你所使用的任何库和包在它们调用导致 Entity Framework 数据库查询方法时也使用异步。</span><span class="sxs-lookup"><span data-stu-id="ffb39-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="ffb39-158">使用存储过程</span><span class="sxs-lookup"><span data-stu-id="ffb39-158">Use stored procedures</span></span>

<span data-ttu-id="ffb39-159">某些开发人员和 Dba 更喜欢使用存储过程来访问数据库。</span><span class="sxs-lookup"><span data-stu-id="ffb39-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="ffb39-160">在的早期版本中实体框架可以通过[执行原始 SQL 查询](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)来检索数据，但不能指示 EF 使用存储过程进行更新操作。</span><span class="sxs-lookup"><span data-stu-id="ffb39-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="ffb39-161">在 EF 6 中，可以轻松地将 Code First 配置为使用存储过程。</span><span class="sxs-lookup"><span data-stu-id="ffb39-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="ffb39-162">在*DAL\SchoolContext.cs*中，将突出显示的代码添加到 `OnModelCreating` 方法。</span><span class="sxs-lookup"><span data-stu-id="ffb39-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="ffb39-163">此代码指示实体框架在 `Department` 实体上使用存储过程执行插入、更新和删除操作。</span><span class="sxs-lookup"><span data-stu-id="ffb39-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="ffb39-164">在 "包管理控制台" 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ffb39-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="ffb39-165">打开*迁移\\&lt;时间戳&gt;\_DepartmentSP.cs*查看创建 Insert、Update 和 Delete 存储过程的 `Up` 方法中的代码：</span><span class="sxs-lookup"><span data-stu-id="ffb39-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="ffb39-166">在 "包管理控制台" 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ffb39-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="ffb39-167">在调试模式下运行应用程序，单击 "**部门**" 选项卡，然后单击 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="ffb39-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="ffb39-168">为新部门输入数据，然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="ffb39-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="ffb39-169">在 Visual Studio 中，查看 "**输出**" 窗口中的日志，以查看是否已使用存储过程插入新的 "部门" 行。</span><span class="sxs-lookup"><span data-stu-id="ffb39-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![部门插入 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="ffb39-171">Code First 创建默认存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="ffb39-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="ffb39-172">如果使用的是现有数据库，则可能需要自定义存储过程的名称，以使用数据库中已定义的存储过程。</span><span class="sxs-lookup"><span data-stu-id="ffb39-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="ffb39-173">有关如何执行此操作的信息，请参阅[实体框架 Code First 插入/更新/删除存储过程](https://msdn.microsoft.com/data/dn468673)。</span><span class="sxs-lookup"><span data-stu-id="ffb39-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="ffb39-174">如果要自定义生成的存储过程的功能，则可以编辑基架代码，以便 `Up` 方法创建存储过程。</span><span class="sxs-lookup"><span data-stu-id="ffb39-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="ffb39-175">这样一来，每当运行迁移时，所做的更改都会反映出来，并将在部署后在生产环境中自动运行时应用于生产数据库。</span><span class="sxs-lookup"><span data-stu-id="ffb39-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="ffb39-176">如果要更改在以前的迁移过程中创建的现有存储过程，则可以使用 "添加-迁移" 命令生成空白迁移，然后手动编写调用[AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx)方法的代码。</span><span class="sxs-lookup"><span data-stu-id="ffb39-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="ffb39-177">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="ffb39-177">Deploy to Azure</span></span>

<span data-ttu-id="ffb39-178">本部分要求你已完成本系列的[迁移和部署](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中的可选将**应用部署到 Azure**部分。</span><span class="sxs-lookup"><span data-stu-id="ffb39-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="ffb39-179">如果已通过删除本地项目中的数据库解决了迁移错误，请跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="ffb39-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="ffb39-180">在 Visual Studio 中，在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="ffb39-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="ffb39-181">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="ffb39-181">Click **Publish**.</span></span>

    <span data-ttu-id="ffb39-182">Visual Studio 将应用程序部署到 Azure，并在默认浏览器中打开应用程序，该应用程序在 Azure 中运行。</span><span class="sxs-lookup"><span data-stu-id="ffb39-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="ffb39-183">测试应用程序以验证其是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="ffb39-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="ffb39-184">首次运行访问数据库的页时，实体框架将运行所需的所有迁移 `Up` 方法，使数据库与当前数据模型保持最新。</span><span class="sxs-lookup"><span data-stu-id="ffb39-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="ffb39-185">你现在可以使用自上次部署以来添加的所有网页，包括你在本教程中添加的部门页面。</span><span class="sxs-lookup"><span data-stu-id="ffb39-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="ffb39-186">获取代码</span><span class="sxs-lookup"><span data-stu-id="ffb39-186">Get the code</span></span>

[<span data-ttu-id="ffb39-187">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="ffb39-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="ffb39-188">其他资源</span><span class="sxs-lookup"><span data-stu-id="ffb39-188">Additional resources</span></span>

<span data-ttu-id="ffb39-189">可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="ffb39-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffb39-190">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ffb39-190">Next steps</span></span>

<span data-ttu-id="ffb39-191">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="ffb39-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ffb39-192">了解异步代码</span><span class="sxs-lookup"><span data-stu-id="ffb39-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="ffb39-193">创建了部门控制器</span><span class="sxs-lookup"><span data-stu-id="ffb39-193">Created a Department controller</span></span>
> * <span data-ttu-id="ffb39-194">使用的存储过程</span><span class="sxs-lookup"><span data-stu-id="ffb39-194">Used stored procedures</span></span>
> * <span data-ttu-id="ffb39-195">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="ffb39-195">Deployed to Azure</span></span>

<span data-ttu-id="ffb39-196">转到下一篇文章，了解当多个用户同时更新同一实体时如何处理冲突。</span><span class="sxs-lookup"><span data-stu-id="ffb39-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ffb39-197">处理并发</span><span class="sxs-lookup"><span data-stu-id="ffb39-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
