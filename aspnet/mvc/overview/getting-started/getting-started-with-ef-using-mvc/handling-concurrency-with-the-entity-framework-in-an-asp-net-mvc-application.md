---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 5 应用中使用 EF 处理并发
description: 本教程介绍当多个用户同时更新同一个实体时，如何使用乐观并发处理冲突。
author: tdykstra
ms.author: riande
ms.topic: tutorial
ms.date: 01/15/2019
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 43c5fdff5601c9bff32300d3460de0079a498d28
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499388"
---
# <a name="tutorial-handle-concurrency-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="b74a4-103">教程：在 ASP.NET MVC 5 应用中使用 EF 处理并发</span><span class="sxs-lookup"><span data-stu-id="b74a4-103">Tutorial: Handle Concurrency with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="b74a4-104">在前面的教程中，您学习了如何更新数据。</span><span class="sxs-lookup"><span data-stu-id="b74a4-104">In earlier tutorials you learned how to update data.</span></span> <span data-ttu-id="b74a4-105">本教程介绍当多个用户同时更新同一个实体时，如何使用乐观并发处理冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-105">This tutorial shows how to use optimistic concurrency to handle conflicts when multiple users update the same entity at the same time.</span></span> <span data-ttu-id="b74a4-106">您可以更改与 `Department` 实体一起使用的网页，以便处理并发错误。</span><span class="sxs-lookup"><span data-stu-id="b74a4-106">You change the web pages that work with the `Department` entity so that they handle concurrency errors.</span></span> <span data-ttu-id="b74a4-107">下图显示了“编辑”和“删除”页面，包括发生并发冲突时显示的一些消息。</span><span class="sxs-lookup"><span data-stu-id="b74a4-107">The following illustrations show the Edit and Delete pages, including some messages that are displayed if a concurrency conflict occurs.</span></span>

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

<span data-ttu-id="b74a4-110">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="b74a4-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b74a4-111">了解并发冲突</span><span class="sxs-lookup"><span data-stu-id="b74a4-111">Learn about concurrency conflicts</span></span>
> * <span data-ttu-id="b74a4-112">添加乐观并发</span><span class="sxs-lookup"><span data-stu-id="b74a4-112">Add optimistic concurrency</span></span>
> * <span data-ttu-id="b74a4-113">修改部门控制器</span><span class="sxs-lookup"><span data-stu-id="b74a4-113">Modify Department controller</span></span>
> * <span data-ttu-id="b74a4-114">测试并发处理</span><span class="sxs-lookup"><span data-stu-id="b74a4-114">Test concurrency handling</span></span>
> * <span data-ttu-id="b74a4-115">更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="b74a4-115">Update the Delete page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b74a4-116">系统必备</span><span class="sxs-lookup"><span data-stu-id="b74a4-116">Prerequisites</span></span>

* [<span data-ttu-id="b74a4-117">异步和存储过程</span><span class="sxs-lookup"><span data-stu-id="b74a4-117">Async and Stored Procedures</span></span>](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="concurrency-conflicts"></a><span data-ttu-id="b74a4-118">并发冲突</span><span class="sxs-lookup"><span data-stu-id="b74a4-118">Concurrency conflicts</span></span>

<span data-ttu-id="b74a4-119">当某用户显示实体数据以对其进行编辑，而另一用户在上一用户的更改写入数据库之前更新同一实体的数据时，会发生并发冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-119">A concurrency conflict occurs when one user displays an entity's data in order to edit it, and then another user updates the same entity's data before the first user's change is written to the database.</span></span> <span data-ttu-id="b74a4-120">如果不启用此类冲突的检测，则最后更新数据库的人员将覆盖其他用户的更改。</span><span class="sxs-lookup"><span data-stu-id="b74a4-120">If you don't enable the detection of such conflicts, whoever updates the database last overwrites the other user's changes.</span></span> <span data-ttu-id="b74a4-121">在许多应用程序中，此风险是可接受的：如果用户很少或更新很少，或者一些更改被覆盖并不重要，则并发编程可能弊大于利。</span><span class="sxs-lookup"><span data-stu-id="b74a4-121">In many applications, this risk is acceptable: if there are few users, or few updates, or if isn't really critical if some changes are overwritten, the cost of programming for concurrency might outweigh the benefit.</span></span> <span data-ttu-id="b74a4-122">在此情况下，不必配置应用程序来处理并发冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-122">In that case, you don't have to configure the application to handle concurrency conflicts.</span></span>

### <a name="pessimistic-concurrency-locking"></a><span data-ttu-id="b74a4-123">悲观并发（锁定）</span><span class="sxs-lookup"><span data-stu-id="b74a4-123">Pessimistic Concurrency (Locking)</span></span>

<span data-ttu-id="b74a4-124">如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。</span><span class="sxs-lookup"><span data-stu-id="b74a4-124">If your application does need to prevent accidental data loss in concurrency scenarios, one way to do that is to use database locks.</span></span> <span data-ttu-id="b74a4-125">这称为 "*悲观并发*"。</span><span class="sxs-lookup"><span data-stu-id="b74a4-125">This is called *pessimistic concurrency*.</span></span> <span data-ttu-id="b74a4-126">例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。</span><span class="sxs-lookup"><span data-stu-id="b74a4-126">For example, before you read a row from a database, you request a lock for read-only or for update access.</span></span> <span data-ttu-id="b74a4-127">如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为他们得到的是正在更改的数据的副本。</span><span class="sxs-lookup"><span data-stu-id="b74a4-127">If you lock a row for update access, no other users are allowed to lock the row either for read-only or update access, because they would get a copy of data that's in the process of being changed.</span></span> <span data-ttu-id="b74a4-128">如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。</span><span class="sxs-lookup"><span data-stu-id="b74a4-128">If you lock a row for read-only access, others can also lock it for read-only access but not for update.</span></span>

<span data-ttu-id="b74a4-129">管理锁定有缺点。</span><span class="sxs-lookup"><span data-stu-id="b74a4-129">Managing locks has disadvantages.</span></span> <span data-ttu-id="b74a4-130">编程可能很复杂。</span><span class="sxs-lookup"><span data-stu-id="b74a4-130">It can be complex to program.</span></span> <span data-ttu-id="b74a4-131">它需要大量的数据库管理资源，且随着应用程序用户数量的增加，可能会导致性能问题。</span><span class="sxs-lookup"><span data-stu-id="b74a4-131">It requires significant database management resources, and it can cause performance problems as the number of users of an application increases.</span></span> <span data-ttu-id="b74a4-132">由于这些原因，并不是所有的数据库管理系统都支持悲观并发。</span><span class="sxs-lookup"><span data-stu-id="b74a4-132">For these reasons, not all database management systems support pessimistic concurrency.</span></span> <span data-ttu-id="b74a4-133">实体框架不提供对它的内置支持，本教程不会演示如何实现它。</span><span class="sxs-lookup"><span data-stu-id="b74a4-133">The Entity Framework provides no built-in support for it, and this tutorial doesn't show you how to implement it.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="b74a4-134">开放式并发</span><span class="sxs-lookup"><span data-stu-id="b74a4-134">Optimistic Concurrency</span></span>

<span data-ttu-id="b74a4-135">保守式并发的替代方法是*乐观并发*。</span><span class="sxs-lookup"><span data-stu-id="b74a4-135">The alternative to pessimistic concurrency is *optimistic concurrency*.</span></span> <span data-ttu-id="b74a4-136">悲观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。</span><span class="sxs-lookup"><span data-stu-id="b74a4-136">Optimistic concurrency means allowing concurrency conflicts to happen, and then reacting appropriately if they do.</span></span> <span data-ttu-id="b74a4-137">例如，John 运行 "部门编辑" 页，将英语系的**预算**金额从 $350000.00 更改为 $0.00。</span><span class="sxs-lookup"><span data-stu-id="b74a4-137">For example, John runs the Departments Edit page, changes the **Budget** amount for the English department from $350,000.00 to $0.00.</span></span>

<span data-ttu-id="b74a4-138">John 单击 "**保存**" 之前，Jane 运行相同的页面，并将 "**开始日期**" 字段从9/1/2007 更改为8/8/2013。</span><span class="sxs-lookup"><span data-stu-id="b74a4-138">Before John clicks **Save**, Jane runs the same page and changes the **Start Date** field from 9/1/2007 to 8/8/2013.</span></span>

<span data-ttu-id="b74a4-139">John 单击 "**保存**"，然后在浏览器返回到索引页时看到其更改，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="b74a4-139">John clicks **Save** first and sees his change when the browser returns to the Index page, then Jane clicks **Save**.</span></span> <span data-ttu-id="b74a4-140">接下来的情况取决于并发冲突的处理方式。</span><span class="sxs-lookup"><span data-stu-id="b74a4-140">What happens next is determined by how you handle concurrency conflicts.</span></span> <span data-ttu-id="b74a4-141">其中一些选项包括：</span><span class="sxs-lookup"><span data-stu-id="b74a4-141">Some of the options include the following:</span></span>

- <span data-ttu-id="b74a4-142">可以跟踪用户已修改的属性，并仅更新数据库中相应的列。</span><span class="sxs-lookup"><span data-stu-id="b74a4-142">You can keep track of which property a user has modified and update only the corresponding columns in the database.</span></span> <span data-ttu-id="b74a4-143">在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。</span><span class="sxs-lookup"><span data-stu-id="b74a4-143">In the example scenario, no data would be lost, because different properties were updated by the two users.</span></span> <span data-ttu-id="b74a4-144">下次有人浏览英语系时，他们将看到 John 和 Jane 的更改，即开始日期为8/8/2013，预算为零美元。</span><span class="sxs-lookup"><span data-stu-id="b74a4-144">The next time someone browses the English department, they'll see both John's and Jane's changes — a start date of 8/8/2013 and a budget of Zero dollars.</span></span>

    <span data-ttu-id="b74a4-145">这种更新方法可减少可能导致数据丢失的冲突次数，但是如果对实体的同一属性进行竞争性更改，则数据难免会丢失。</span><span class="sxs-lookup"><span data-stu-id="b74a4-145">This method of updating can reduce the number of conflicts that could result in data loss, but it can't avoid data loss if competing changes are made to the same property of an entity.</span></span> <span data-ttu-id="b74a4-146">Entity Framework 是否以这种方式工作取决于更新代码的实现方式。</span><span class="sxs-lookup"><span data-stu-id="b74a4-146">Whether the Entity Framework works this way depends on how you implement your update code.</span></span> <span data-ttu-id="b74a4-147">通常不适合在 Web 应用程序中使用，因为它要求保持大量的状态，以便跟踪实体的所有原始属性值以及新值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-147">It's often not practical in a web application, because it can require that you maintain large amounts of state in order to keep track of all original property values for an entity as well as new values.</span></span> <span data-ttu-id="b74a4-148">维护大量的状态可能会影响应用程序的性能，因为它需要服务器资源或必须包含在网页本身（例如隐藏字段）或 Cookie 中。</span><span class="sxs-lookup"><span data-stu-id="b74a4-148">Maintaining large amounts of state can affect application performance because it either requires server resources or must be included in the web page itself (for example, in hidden fields) or in a cookie.</span></span>
- <span data-ttu-id="b74a4-149">可以让 Jane 的更改覆盖 John 的更改。</span><span class="sxs-lookup"><span data-stu-id="b74a4-149">You can let Jane's change overwrite John's change.</span></span> <span data-ttu-id="b74a4-150">下次有人浏览英语系时，他们将看到8/8/2013 和已还原的 $350000.00 值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-150">The next time someone browses the English department, they'll see 8/8/2013 and the restored $350,000.00 value.</span></span> <span data-ttu-id="b74a4-151">这称为“客户端优先”或“最后一个优先”。</span><span class="sxs-lookup"><span data-stu-id="b74a4-151">This is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="b74a4-152">（客户端的所有值优先于数据存储中的内容。）如本部分简介中所述，如果不执行任何并发处理编码，则会自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="b74a4-152">(All values from the client take precedence over what's in the data store.) As noted in the introduction to this section, if you don't do any coding for concurrency handling, this will happen automatically.</span></span>
- <span data-ttu-id="b74a4-153">您可以阻止在数据库中更新 Jane 的更改。</span><span class="sxs-lookup"><span data-stu-id="b74a4-153">You can prevent Jane's change from being updated in the database.</span></span> <span data-ttu-id="b74a4-154">通常情况下，会显示一条错误消息，向她显示数据的当前状态，并允许她重新应用更改（如果她仍想要进行更改）。</span><span class="sxs-lookup"><span data-stu-id="b74a4-154">Typically, you would display an error message, show her the current state of the data, and allow her to reapply her changes if she still wants to make them.</span></span> <span data-ttu-id="b74a4-155">这称为“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="b74a4-155">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="b74a4-156">（数据存储值优先于客户端提交的值。）在本教程中，您将实施存储入选方案。</span><span class="sxs-lookup"><span data-stu-id="b74a4-156">(The data-store values take precedence over the values submitted by the client.) You'll implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="b74a4-157">此方法可确保用户在未收到具体发生内容的警报时，不会覆盖任何更改。</span><span class="sxs-lookup"><span data-stu-id="b74a4-157">This method ensures that no changes are overwritten without a user being alerted to what's happening.</span></span>

### <a name="detecting-concurrency-conflicts"></a><span data-ttu-id="b74a4-158">检测并发冲突</span><span class="sxs-lookup"><span data-stu-id="b74a4-158">Detecting Concurrency Conflicts</span></span>

<span data-ttu-id="b74a4-159">可以通过处理实体框架引发的[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx)异常来解决冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-159">You can resolve conflicts by handling [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) exceptions that the Entity Framework throws.</span></span> <span data-ttu-id="b74a4-160">为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-160">In order to know when to throw these exceptions, the Entity Framework must be able to detect conflicts.</span></span> <span data-ttu-id="b74a4-161">因此，你必须正确配置数据库和数据模型。</span><span class="sxs-lookup"><span data-stu-id="b74a4-161">Therefore, you must configure the database and the data model appropriately.</span></span> <span data-ttu-id="b74a4-162">启用冲突检测的某些选项包括：</span><span class="sxs-lookup"><span data-stu-id="b74a4-162">Some options for enabling conflict detection include the following:</span></span>

- <span data-ttu-id="b74a4-163">数据库表中包含一个可用于确定某行更改时间的跟踪列。</span><span class="sxs-lookup"><span data-stu-id="b74a4-163">In the database table, include a tracking column that can be used to determine when a row has been changed.</span></span> <span data-ttu-id="b74a4-164">然后，可以将实体框架配置为将该列包含在 SQL `Update` 的 `Where` 子句中或 `Delete` 命令。</span><span class="sxs-lookup"><span data-stu-id="b74a4-164">You can then configure the Entity Framework to include that column in the `Where` clause of SQL `Update` or `Delete` commands.</span></span>

    <span data-ttu-id="b74a4-165">跟踪列的数据类型通常为[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b74a4-165">The data type of the tracking column is typically [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx).</span></span> <span data-ttu-id="b74a4-166">[Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新行时递增的序列号。</span><span class="sxs-lookup"><span data-stu-id="b74a4-166">The [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) value is a sequential number that's incremented each time the row is updated.</span></span> <span data-ttu-id="b74a4-167">在 `Update` 或 `Delete` 命令中，`Where` 子句包含跟踪列（原始行版本）的原始值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-167">In an `Update` or `Delete` command, the `Where` clause includes the original value of the tracking column (the original row version).</span></span> <span data-ttu-id="b74a4-168">如果正在更新的行已由其他用户更改，则 `rowversion` 列中的值与原始值不同，因此 `Update` 或 `Delete` 语句由于 `Where` 子句而无法找到要更新的行。</span><span class="sxs-lookup"><span data-stu-id="b74a4-168">If the row being updated has been changed by another user, the value in the `rowversion` column is different than the original value, so the `Update` or `Delete` statement can't find the row to update because of the `Where` clause.</span></span> <span data-ttu-id="b74a4-169">当实体框架发现 `Update` 或 `Delete` 命令没有更新任何行（即，受影响的行数为零时），它会将其解释为并发冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-169">When the Entity Framework finds that no rows have been updated by the `Update` or `Delete` command (that is, when the number of affected rows is zero), it interprets that as a concurrency conflict.</span></span>
- <span data-ttu-id="b74a4-170">将实体框架配置为在 `Update` 和 `Delete` 命令的 `Where` 子句中包含表中每一列的原始值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-170">Configure the Entity Framework to include the original values of every column in the table in the `Where` clause of `Update` and `Delete` commands.</span></span>

    <span data-ttu-id="b74a4-171">在第一个选项中，如果行中的任何内容在第一次读取后发生了更改，则 `Where` 子句将不返回要更新的行，实体框架会将其解释为并发冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-171">As in the first option, if anything in the row has changed since the row was first read, the `Where` clause won't return a row to update, which the Entity Framework interprets as a concurrency conflict.</span></span> <span data-ttu-id="b74a4-172">对于包含多个列的数据库表，此方法可能会产生非常大的 `Where` 子句，并可能要求你维护大量状态。</span><span class="sxs-lookup"><span data-stu-id="b74a4-172">For database tables that have many columns, this approach can result in very large `Where` clauses, and can require that you maintain large amounts of state.</span></span> <span data-ttu-id="b74a4-173">如前所述，维持大量的状态会影响应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="b74a4-173">As noted earlier, maintaining large amounts of state can affect application performance.</span></span> <span data-ttu-id="b74a4-174">因此通常不建议使用此方法，并且它也不是本教程中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="b74a4-174">Therefore this approach is generally not recommended, and it isn't the method used in this tutorial.</span></span>

    <span data-ttu-id="b74a4-175">如果确实要实现这种并发方法，则必须将[ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)属性添加到要跟踪其并发的实体中的所有非主键属性。</span><span class="sxs-lookup"><span data-stu-id="b74a4-175">If you do want to implement this approach to concurrency, you have to mark all non-primary-key properties in the entity you want to track concurrency for by adding the [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) attribute to them.</span></span> <span data-ttu-id="b74a4-176">通过此更改，实体框架可以在 `UPDATE` 语句的 SQL `WHERE` 子句中包含所有列。</span><span class="sxs-lookup"><span data-stu-id="b74a4-176">That change enables the Entity Framework to include all columns in the SQL `WHERE` clause of `UPDATE` statements.</span></span>

<span data-ttu-id="b74a4-177">在本教程的剩余部分中，你将[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)跟踪属性添加到 `Department` 实体、创建控制器和视图，并进行测试以验证一切是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="b74a4-177">In the remainder of this tutorial you'll add a [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tracking property to the `Department` entity, create a controller and views, and test to verify that everything works correctly.</span></span>

## <a name="add-optimistic-concurrency"></a><span data-ttu-id="b74a4-178">添加乐观并发</span><span class="sxs-lookup"><span data-stu-id="b74a4-178">Add optimistic concurrency</span></span>

<span data-ttu-id="b74a4-179">在*Models\Department.cs*中，添加一个名为 `RowVersion`的跟踪属性：</span><span class="sxs-lookup"><span data-stu-id="b74a4-179">In *Models\Department.cs*, add a tracking property named `RowVersion`:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

<span data-ttu-id="b74a4-180">[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)特性指定此列将包含在发送到数据库的 `Update` 和 `Delete` 命令的 `Where` 子句中。</span><span class="sxs-lookup"><span data-stu-id="b74a4-180">The [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) attribute specifies that this column will be included in the `Where` clause of `Update` and `Delete` commands sent to the database.</span></span> <span data-ttu-id="b74a4-181">此属性被称为[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)，这是因为以前版本的 SQL SERVER 在 sql [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)将其替换之前使用 sql [Timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)数据类型。</span><span class="sxs-lookup"><span data-stu-id="b74a4-181">The attribute is called [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) because previous versions of SQL Server used a SQL [timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) data type before the SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) replaced it.</span></span> <span data-ttu-id="b74a4-182">[Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)的 .net 类型是字节数组。</span><span class="sxs-lookup"><span data-stu-id="b74a4-182">The .Net type for [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) is a byte array.</span></span>

<span data-ttu-id="b74a4-183">如果希望使用 Fluent API，可以使用[IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)方法来指定跟踪属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="b74a4-183">If you prefer to use the fluent API, you can use the [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) method to specify the tracking property, as shown in the following example:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="b74a4-184">通过添加属性，更改了数据库模型，因此需要再执行一次迁移。</span><span class="sxs-lookup"><span data-stu-id="b74a4-184">By adding a property you changed the database model, so you need to do another migration.</span></span> <span data-ttu-id="b74a4-185">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b74a4-185">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-department-controller"></a><span data-ttu-id="b74a4-186">修改部门控制器</span><span class="sxs-lookup"><span data-stu-id="b74a4-186">Modify Department controller</span></span>

<span data-ttu-id="b74a4-187">在*Controllers\DepartmentController.cs*中，添加一个 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="b74a4-187">In *Controllers\DepartmentController.cs*, add a `using` statement:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="b74a4-188">在*DepartmentController.cs*文件中，将 "LastName" 的所有四个匹配项更改为 "FullName"，以便 "部门管理员" 下拉列表将包含讲师的全名，而不只是姓氏。</span><span class="sxs-lookup"><span data-stu-id="b74a4-188">In the *DepartmentController.cs* file, change all four occurrences of "LastName" to "FullName" so that the department administrator drop-down lists will contain the full name of the instructor rather than just the last name.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

<span data-ttu-id="b74a4-189">将 `HttpPost` `Edit` 方法的现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b74a4-189">Replace the existing code for the `HttpPost` `Edit` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="b74a4-190">如果 `FindAsync` 方法返回 NULL，则该院系已被另一用户删除。</span><span class="sxs-lookup"><span data-stu-id="b74a4-190">If the `FindAsync` method returns null, the department was deleted by another user.</span></span> <span data-ttu-id="b74a4-191">显示的代码使用已发布的窗体值创建部门实体，以便可以使用错误消息重新显示 "编辑" 页。</span><span class="sxs-lookup"><span data-stu-id="b74a4-191">The code shown uses the posted form values to create a department entity so that the Edit page can be redisplayed with an error message.</span></span> <span data-ttu-id="b74a4-192">或者，如果仅显示错误消息而未重新显示院系字段，则不必重新创建 Department 实体。</span><span class="sxs-lookup"><span data-stu-id="b74a4-192">As an alternative, you wouldn't have to re-create the department entity if you display only an error message without redisplaying the department fields.</span></span>

<span data-ttu-id="b74a4-193">视图将原始 `RowVersion` 值存储在隐藏字段中，方法在 `rowVersion` 参数中接收它。</span><span class="sxs-lookup"><span data-stu-id="b74a4-193">The view stores the original `RowVersion` value in a hidden field, and the method receives it in the `rowVersion` parameter.</span></span> <span data-ttu-id="b74a4-194">在调用 `SaveChanges` 之前，必须将该原始 `RowVersion` 属性值置于实体的 `OriginalValues` 集合中。</span><span class="sxs-lookup"><span data-stu-id="b74a4-194">Before you call `SaveChanges`, you have to put that original `RowVersion` property value in the `OriginalValues` collection for the entity.</span></span> <span data-ttu-id="b74a4-195">当实体框架创建 SQL `UPDATE` 命令时，该命令将包含一个 `WHERE` 子句，该子句将查找具有原始 `RowVersion` 值的行。</span><span class="sxs-lookup"><span data-stu-id="b74a4-195">Then when the Entity Framework creates a SQL `UPDATE` command, that command will include a `WHERE` clause that looks for a row that has the original `RowVersion` value.</span></span>

<span data-ttu-id="b74a4-196">如果 `UPDATE` 命令（没有行具有原始 `RowVersion` 值）不影响任何行，实体框架将引发 `DbUpdateConcurrencyException` 异常，而 `catch` 块中的代码将从异常对象获取受影响的 `Department` 实体。</span><span class="sxs-lookup"><span data-stu-id="b74a4-196">If no rows are affected by the `UPDATE` command (no rows have the original `RowVersion` value), the Entity Framework throws a `DbUpdateConcurrencyException` exception, and the code in the `catch` block gets the affected `Department` entity from the exception object.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="b74a4-197">此对象具有用户在其 `Entity` 属性中输入的新值，你可以通过调用 `GetDatabaseValues` 方法获取从数据库中读取的值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-197">This object has the new values entered by the user in its `Entity` property, and you can get the values read from the database by calling the `GetDatabaseValues` method.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="b74a4-198">如果有人删除了数据库中的行，则 `GetDatabaseValues` 方法返回 null;否则，你必须将返回的对象强制转换为 `Department` 类，才能访问 `Department` 属性。</span><span class="sxs-lookup"><span data-stu-id="b74a4-198">The `GetDatabaseValues` method returns null if someone has deleted the row from the database; otherwise, you have to cast the returned object to the `Department` class in order to access the `Department` properties.</span></span> <span data-ttu-id="b74a4-199">（由于你已检查删除，`databaseEntry` 仅当在 `FindAsync` 执行之后以及 `SaveChanges` 执行之前删除了该部门时才为 null。）</span><span class="sxs-lookup"><span data-stu-id="b74a4-199">(Because you already checked for deletion, `databaseEntry` would be null only if the department was deleted after `FindAsync` executes and before `SaveChanges` executes.)</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="b74a4-200">接下来，代码为其数据库值不同于在 "编辑" 页上输入的数据库值的每个列添加一条自定义错误消息：</span><span class="sxs-lookup"><span data-stu-id="b74a4-200">Next, the code adds a custom error message for each column that has database values different from what the user entered on the Edit page:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="b74a4-201">更长的错误消息说明发生了什么情况以及如何处理它：</span><span class="sxs-lookup"><span data-stu-id="b74a4-201">A longer error message explains what happened and what to do about it:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="b74a4-202">最后，该代码将 `Department` 对象的 `RowVersion` 值设置为从数据库中检索到的新值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-202">Finally, the code sets the `RowVersion` value of the `Department` object to the new value retrieved from the database.</span></span> <span data-ttu-id="b74a4-203">重新显示“编辑”页时，这个新的 `RowVersion` 值将存储在隐藏字段中，当用户下次单击“保存”时，将只捕获自“编辑”页重新显示起发生的并发错误。</span><span class="sxs-lookup"><span data-stu-id="b74a4-203">This new `RowVersion` value will be stored in the hidden field when the Edit page is redisplayed, and the next time the user clicks **Save**, only concurrency errors that happen since the redisplay of the Edit page will be caught.</span></span>

<span data-ttu-id="b74a4-204">在*Views\Department\Edit.cshtml*中，添加隐藏字段以保存 `RowVersion` 属性值，紧跟在 `DepartmentID` 属性的隐藏字段之后：</span><span class="sxs-lookup"><span data-stu-id="b74a4-204">In *Views\Department\Edit.cshtml*, add a hidden field to save the `RowVersion` property value, immediately following the hidden field for the `DepartmentID` property:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="test-concurrency-handling"></a><span data-ttu-id="b74a4-205">测试并发处理</span><span class="sxs-lookup"><span data-stu-id="b74a4-205">Test concurrency handling</span></span>

<span data-ttu-id="b74a4-206">运行站点并单击 "**部门**"。</span><span class="sxs-lookup"><span data-stu-id="b74a4-206">Run the site and click **Departments**.</span></span>

<span data-ttu-id="b74a4-207">右键单击英语系的 "**编辑**" 超链接，然后选择 "**在新选项卡中打开"，** 然后单击英语系的 "**编辑**" 超链接。</span><span class="sxs-lookup"><span data-stu-id="b74a4-207">Right click the **Edit** hyperlink for the English department and select **Open in new tab,** then click the **Edit** hyperlink for the English department.</span></span> <span data-ttu-id="b74a4-208">这两个选项卡显示相同的信息。</span><span class="sxs-lookup"><span data-stu-id="b74a4-208">The two tabs display the same information.</span></span>

<span data-ttu-id="b74a4-209">在第一个浏览器选项卡中更改一个字段，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="b74a4-209">Change a field in the first browser tab and click **Save**.</span></span>

<span data-ttu-id="b74a4-210">浏览器显示具有更改值的索引页。</span><span class="sxs-lookup"><span data-stu-id="b74a4-210">The browser shows the Index page with the changed value.</span></span>

<span data-ttu-id="b74a4-211">在第二个浏览器选项卡中更改字段，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="b74a4-211">Change a field in the second browser tab and click **Save**.</span></span> <span data-ttu-id="b74a4-212">看见一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="b74a4-212">You see an error message:</span></span>

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="b74a4-214">再次单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="b74a4-214">Click **Save** again.</span></span> <span data-ttu-id="b74a4-215">在第二个浏览器选项卡中输入的值与在第一个浏览器中更改的数据的原始值一起保存。</span><span class="sxs-lookup"><span data-stu-id="b74a4-215">The value you entered in the second browser tab is saved along with the original value of the data you changed in the first browser.</span></span> <span data-ttu-id="b74a4-216">在索引页中出现时，可以看到已保存的值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-216">You see the saved values when the Index page appears.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="b74a4-217">更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="b74a4-217">Update the Delete page</span></span>

<span data-ttu-id="b74a4-218">对于“删除”页，Entity Framework 以类似方式检测其他人编辑院系所引起的并发冲突。</span><span class="sxs-lookup"><span data-stu-id="b74a4-218">For the Delete page, the Entity Framework detects concurrency conflicts caused by someone else editing the department in a similar manner.</span></span> <span data-ttu-id="b74a4-219">当 "`HttpGet` `Delete`" 方法显示 "确认" 视图时，该视图将在隐藏字段中包含原始 `RowVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-219">When the `HttpGet` `Delete` method displays the confirmation view, the view includes the original `RowVersion` value in a hidden field.</span></span> <span data-ttu-id="b74a4-220">然后，该值可供用户确认删除时调用的 `HttpPost` `Delete` 方法使用。</span><span class="sxs-lookup"><span data-stu-id="b74a4-220">That value is then available to the `HttpPost` `Delete` method that's called when the user confirms the deletion.</span></span> <span data-ttu-id="b74a4-221">当实体框架创建 SQL `DELETE` 命令时，它将包含一个具有原始 `RowVersion` 值的 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="b74a4-221">When the Entity Framework creates the SQL `DELETE` command, it includes a `WHERE` clause with the original `RowVersion` value.</span></span> <span data-ttu-id="b74a4-222">如果命令导致0行受影响（也就是说，在显示 "删除确认" 页面后更改了该行），则会引发并发异常，并会调用 `HttpGet Delete` 方法，并将错误标志设置为 "`true`" 以重新显示包含错误消息的确认页面。</span><span class="sxs-lookup"><span data-stu-id="b74a4-222">If the command results in zero rows affected (meaning the row was changed after the Delete confirmation page was displayed), a concurrency exception is thrown, and the `HttpGet Delete` method is called with an error flag set to `true` in order to redisplay the confirmation page with an error message.</span></span> <span data-ttu-id="b74a4-223">因为行已被其他用户删除，所以也可能会影响零行，因此在这种情况下，将显示不同的错误消息。</span><span class="sxs-lookup"><span data-stu-id="b74a4-223">It's also possible that zero rows were affected because the row was deleted by another user, so in that case a different error message is displayed.</span></span>

<span data-ttu-id="b74a4-224">在*DepartmentController.cs*中，将 `HttpGet` `Delete` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b74a4-224">In *DepartmentController.cs*, replace the `HttpGet` `Delete` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="b74a4-225">该方法接受可选参数，该参数指示是否在并发错误之后重新显示页面。</span><span class="sxs-lookup"><span data-stu-id="b74a4-225">The method accepts an optional parameter that indicates whether the page is being redisplayed after a concurrency error.</span></span> <span data-ttu-id="b74a4-226">如果 `true`此标志，则会使用 `ViewBag` 属性将错误消息发送到视图。</span><span class="sxs-lookup"><span data-stu-id="b74a4-226">If this flag is `true`, an error message is sent to the view using a `ViewBag` property.</span></span>

<span data-ttu-id="b74a4-227">将 `HttpPost` `Delete` 方法中的代码替换 `DeleteConfirmed`为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b74a4-227">Replace the code in the `HttpPost` `Delete` method (named `DeleteConfirmed`) with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="b74a4-228">在刚替换的基架代码中，此方法仅接受记录 ID：</span><span class="sxs-lookup"><span data-stu-id="b74a4-228">In the scaffolded code that you just replaced, this method accepted only a record ID:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="b74a4-229">已将此参数更改为模型绑定器创建的 `Department` 实体实例。</span><span class="sxs-lookup"><span data-stu-id="b74a4-229">You've changed this parameter to a `Department` entity instance created by the model binder.</span></span> <span data-ttu-id="b74a4-230">这使你除了记录键外，还可以访问 `RowVersion` 属性值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-230">This gives you access to the `RowVersion` property value in addition to the record key.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="b74a4-231">你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。</span><span class="sxs-lookup"><span data-stu-id="b74a4-231">You have also changed the action method name from `DeleteConfirmed` to `Delete`.</span></span> <span data-ttu-id="b74a4-232">`HttpPost` 的名为的基架代码 `Delete` 方法 `DeleteConfirmed` 为 `HttpPost` 方法指定唯一签名。</span><span class="sxs-lookup"><span data-stu-id="b74a4-232">The scaffolded code named the `HttpPost` `Delete` method `DeleteConfirmed` to give the `HttpPost` method a unique signature.</span></span> <span data-ttu-id="b74a4-233">（CLR 要求重载方法具有不同的方法参数。）签名是唯一的，可以坚持使用 MVC 约定，并为 `HttpPost` 和 `HttpGet` delete 方法使用相同的名称。</span><span class="sxs-lookup"><span data-stu-id="b74a4-233">( The CLR requires overloaded methods to have different method parameters.) Now that the signatures are unique, you can stick with the MVC convention and use the same name for the `HttpPost` and `HttpGet` delete methods.</span></span>

<span data-ttu-id="b74a4-234">如果捕获到并发错误，代码将重新显示“删除”确认页，并提供一个指示它应显示并发错误消息的标志。</span><span class="sxs-lookup"><span data-stu-id="b74a4-234">If a concurrency error is caught, the code redisplays the Delete confirmation page and provides a flag that indicates it should display a concurrency error message.</span></span>

<span data-ttu-id="b74a4-235">在*Views\Department\Delete.cshtml*中，将基架代码替换为以下代码，以便为 DepartmentID 和 RowVersion 属性添加错误消息字段和隐藏字段。</span><span class="sxs-lookup"><span data-stu-id="b74a4-235">In *Views\Department\Delete.cshtml*, replace the scaffolded code with the following code that adds an error message field and hidden fields for the DepartmentID and RowVersion properties.</span></span> <span data-ttu-id="b74a4-236">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="b74a4-236">The changes are highlighted.</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

<span data-ttu-id="b74a4-237">此代码在 `h2` 和 `h3` 标题之间添加错误消息：</span><span class="sxs-lookup"><span data-stu-id="b74a4-237">This code adds an error message between the `h2` and `h3` headings:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="b74a4-238">它将 `LastName` 替换为 `Administrator` 字段中 `FullName`：</span><span class="sxs-lookup"><span data-stu-id="b74a4-238">It replaces `LastName` with `FullName` in the `Administrator` field:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="b74a4-239">最后，它将添加 `DepartmentID` 的隐藏字段，并在 `Html.BeginForm` 语句后 `RowVersion` 属性：</span><span class="sxs-lookup"><span data-stu-id="b74a4-239">Finally, it adds hidden fields for the `DepartmentID` and `RowVersion` properties after the `Html.BeginForm` statement:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

<span data-ttu-id="b74a4-240">运行 "部门索引" 页。</span><span class="sxs-lookup"><span data-stu-id="b74a4-240">Run the Departments Index page.</span></span> <span data-ttu-id="b74a4-241">右键单击英语系的 "**删除**" 超链接，然后选择 "**在新选项卡中打开"，** 然后在第一个选项卡中，单击英语系的 "**编辑**" 超链接。</span><span class="sxs-lookup"><span data-stu-id="b74a4-241">Right click the **Delete** hyperlink for the English department and select **Open in new tab,** then in the first tab click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="b74a4-242">在第一个窗口中，更改其中一个值，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="b74a4-242">In the first window, change one of the values, and click **Save**.</span></span>

<span data-ttu-id="b74a4-243">索引页确认更改。</span><span class="sxs-lookup"><span data-stu-id="b74a4-243">The Index page confirms the change.</span></span>

<span data-ttu-id="b74a4-244">在第二个选项卡中，单击“删除”。</span><span class="sxs-lookup"><span data-stu-id="b74a4-244">In the second tab, click **Delete**.</span></span>

<span data-ttu-id="b74a4-245">你将看到并发错误消息，且已使用数据库中的当前内容刷新了“院系”值。</span><span class="sxs-lookup"><span data-stu-id="b74a4-245">You see the concurrency error message, and the Department values are refreshed with what's currently in the database.</span></span>

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

<span data-ttu-id="b74a4-247">如果再次单击“删除”，会重定向到已删除显示院系的索引页。</span><span class="sxs-lookup"><span data-stu-id="b74a4-247">If you click **Delete** again, you're redirected to the Index page, which shows that the department has been deleted.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="b74a4-248">获取代码</span><span class="sxs-lookup"><span data-stu-id="b74a4-248">Get the code</span></span>

[<span data-ttu-id="b74a4-249">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="b74a4-249">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="b74a4-250">其他资源</span><span class="sxs-lookup"><span data-stu-id="b74a4-250">Additional resources</span></span>

<span data-ttu-id="b74a4-251">可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="b74a4-251">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="b74a4-252">有关处理各种并发方案的其他方法的信息，请参阅 MSDN 上的[乐观并发模式](https://msdn.microsoft.com/data/jj592904)和使用[属性值](https://msdn.microsoft.com/data/jj592677)。</span><span class="sxs-lookup"><span data-stu-id="b74a4-252">For information about other ways to handle various concurrency scenarios, see [Optimistic Concurrency Patterns](https://msdn.microsoft.com/data/jj592904) and [Working with Property Values](https://msdn.microsoft.com/data/jj592677) on MSDN.</span></span> <span data-ttu-id="b74a4-253">下一教程介绍如何实现 `Instructor` 和 `Student` 实体的每个层次结构一个表继承。</span><span class="sxs-lookup"><span data-stu-id="b74a4-253">The next tutorial shows how to implement table-per-hierarchy inheritance for the `Instructor` and `Student` entities.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b74a4-254">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b74a4-254">Next steps</span></span>

<span data-ttu-id="b74a4-255">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="b74a4-255">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b74a4-256">已了解并发冲突</span><span class="sxs-lookup"><span data-stu-id="b74a4-256">Learned about concurrency conflicts</span></span>
> * <span data-ttu-id="b74a4-257">添加了开放式并发</span><span class="sxs-lookup"><span data-stu-id="b74a4-257">Added optimistic concurrency</span></span>
> * <span data-ttu-id="b74a4-258">修改的部门控制器</span><span class="sxs-lookup"><span data-stu-id="b74a4-258">Modified Department controller</span></span>
> * <span data-ttu-id="b74a4-259">已测试并发处理</span><span class="sxs-lookup"><span data-stu-id="b74a4-259">Tested concurrency handling</span></span>
> * <span data-ttu-id="b74a4-260">已更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="b74a4-260">Updated the Delete page</span></span>

<span data-ttu-id="b74a4-261">转到下一篇文章，了解如何在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="b74a4-261">Advance to the next article to learn how to implement inheritance in the data model.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b74a4-262">在数据模型中实现继承</span><span class="sxs-lookup"><span data-stu-id="b74a4-262">Implement inheritance in the data model</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
