---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 5 应用中处理并发和 EF
description: 本教程演示如何使用乐观并发，多个用户在同一时间更新同一实体时处理冲突。
author: tdykstra
ms.author: riande
ms.topic: tutorial
ms.date: 01/15/2019
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b513d7d86d382068bc1a8f1bcc61289ee946d38b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064524"
---
<a name="handling-concurrency-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-10-of-12"></a><span data-ttu-id="0601c-103">处理并发使用 Entity Framework 6 中的 ASP.NET MVC 5 应用程序 (10 / 12)</span><span class="sxs-lookup"><span data-stu-id="0601c-103">Handling Concurrency with the Entity Framework 6 in an ASP.NET MVC 5 Application (10 of 12)</span></span>
====================

# <a name="tutorial-handle-concurrency-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="0601c-104">教程：在 ASP.NET MVC 5 应用中处理并发和 EF</span><span class="sxs-lookup"><span data-stu-id="0601c-104">Tutorial: Handle Concurrency with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="0601c-105">之前的教程介绍了如何更新数据。</span><span class="sxs-lookup"><span data-stu-id="0601c-105">In earlier tutorials you learned how to update data.</span></span> <span data-ttu-id="0601c-106">本教程演示如何使用乐观并发，多个用户在同一时间更新同一实体时处理冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-106">This tutorial shows how to use optimistic concurrency to handle conflicts when multiple users update the same entity at the same time.</span></span> <span data-ttu-id="0601c-107">更改使用的网页`Department`实体以使它们处理并发错误。</span><span class="sxs-lookup"><span data-stu-id="0601c-107">You change the web pages that work with the `Department` entity so that they handle concurrency errors.</span></span> <span data-ttu-id="0601c-108">下图显示了“编辑”和“删除”页面，包括发生并发冲突时显示的一些消息。</span><span class="sxs-lookup"><span data-stu-id="0601c-108">The following illustrations show the Edit and Delete pages, including some messages that are displayed if a concurrency conflict occurs.</span></span>

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

<span data-ttu-id="0601c-111">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="0601c-111">In this tutorial, you:</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="0601c-112">了解并发冲突</span><span class="sxs-lookup"><span data-stu-id="0601c-112">Learn about concurrency conflicts</span></span>
> * <span data-ttu-id="0601c-113">添加乐观并发</span><span class="sxs-lookup"><span data-stu-id="0601c-113">Add optimistic concurrency</span></span>
> * <span data-ttu-id="0601c-114">修改部门控制器</span><span class="sxs-lookup"><span data-stu-id="0601c-114">Modify Department controller</span></span>
> * <span data-ttu-id="0601c-115">测试并发处理</span><span class="sxs-lookup"><span data-stu-id="0601c-115">Test concurrency handling</span></span>
> * <span data-ttu-id="0601c-116">更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="0601c-116">Update the Delete page</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0601c-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="0601c-117">Prerequisites</span></span>

* [<span data-ttu-id="0601c-118">异步和存储过程</span><span class="sxs-lookup"><span data-stu-id="0601c-118">Async and Stored Procedures</span></span>](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="concurrency-conflicts"></a><span data-ttu-id="0601c-119">并发冲突</span><span class="sxs-lookup"><span data-stu-id="0601c-119">Concurrency conflicts</span></span>

<span data-ttu-id="0601c-120">当某用户显示实体数据以对其进行编辑，而另一用户在上一用户的更改写入数据库之前更新同一实体的数据时，会发生并发冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-120">A concurrency conflict occurs when one user displays an entity's data in order to edit it, and then another user updates the same entity's data before the first user's change is written to the database.</span></span> <span data-ttu-id="0601c-121">如果不启用此类冲突的检测，则最后更新数据库的人员将覆盖其他用户的更改。</span><span class="sxs-lookup"><span data-stu-id="0601c-121">If you don't enable the detection of such conflicts, whoever updates the database last overwrites the other user's changes.</span></span> <span data-ttu-id="0601c-122">在许多应用程序中，此风险是可接受的：如果用户很少或更新很少，或者一些更改被覆盖并不重要，则并发编程可能弊大于利。</span><span class="sxs-lookup"><span data-stu-id="0601c-122">In many applications, this risk is acceptable: if there are few users, or few updates, or if isn't really critical if some changes are overwritten, the cost of programming for concurrency might outweigh the benefit.</span></span> <span data-ttu-id="0601c-123">在此情况下，不必配置应用程序来处理并发冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-123">In that case, you don't have to configure the application to handle concurrency conflicts.</span></span>

### <a name="pessimistic-concurrency-locking"></a><span data-ttu-id="0601c-124">悲观并发 （锁定）</span><span class="sxs-lookup"><span data-stu-id="0601c-124">Pessimistic Concurrency (Locking)</span></span>

<span data-ttu-id="0601c-125">如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。</span><span class="sxs-lookup"><span data-stu-id="0601c-125">If your application does need to prevent accidental data loss in concurrency scenarios, one way to do that is to use database locks.</span></span> <span data-ttu-id="0601c-126">这称为*保守式并发*。</span><span class="sxs-lookup"><span data-stu-id="0601c-126">This is called *pessimistic concurrency*.</span></span> <span data-ttu-id="0601c-127">例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。</span><span class="sxs-lookup"><span data-stu-id="0601c-127">For example, before you read a row from a database, you request a lock for read-only or for update access.</span></span> <span data-ttu-id="0601c-128">如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为他们得到的是正在更改的数据的副本。</span><span class="sxs-lookup"><span data-stu-id="0601c-128">If you lock a row for update access, no other users are allowed to lock the row either for read-only or update access, because they would get a copy of data that's in the process of being changed.</span></span> <span data-ttu-id="0601c-129">如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。</span><span class="sxs-lookup"><span data-stu-id="0601c-129">If you lock a row for read-only access, others can also lock it for read-only access but not for update.</span></span>

<span data-ttu-id="0601c-130">管理锁定有缺点。</span><span class="sxs-lookup"><span data-stu-id="0601c-130">Managing locks has disadvantages.</span></span> <span data-ttu-id="0601c-131">编程可能很复杂。</span><span class="sxs-lookup"><span data-stu-id="0601c-131">It can be complex to program.</span></span> <span data-ttu-id="0601c-132">它需要大量的数据库管理资源，且随着应用程序用户数量的增加，可能会导致性能问题。</span><span class="sxs-lookup"><span data-stu-id="0601c-132">It requires significant database management resources, and it can cause performance problems as the number of users of an application increases.</span></span> <span data-ttu-id="0601c-133">由于这些原因，并不是所有的数据库管理系统都支持悲观并发。</span><span class="sxs-lookup"><span data-stu-id="0601c-133">For these reasons, not all database management systems support pessimistic concurrency.</span></span> <span data-ttu-id="0601c-134">实体框架不提供内置支持，以及本教程不展示如何实现它。</span><span class="sxs-lookup"><span data-stu-id="0601c-134">The Entity Framework provides no built-in support for it, and this tutorial doesn't show you how to implement it.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="0601c-135">开放式并发</span><span class="sxs-lookup"><span data-stu-id="0601c-135">Optimistic Concurrency</span></span>

<span data-ttu-id="0601c-136">悲观并发的替代方法是*乐观并发*。</span><span class="sxs-lookup"><span data-stu-id="0601c-136">The alternative to pessimistic concurrency is *optimistic concurrency*.</span></span> <span data-ttu-id="0601c-137">悲观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。</span><span class="sxs-lookup"><span data-stu-id="0601c-137">Optimistic concurrency means allowing concurrency conflicts to happen, and then reacting appropriately if they do.</span></span> <span data-ttu-id="0601c-138">例如，John 运行部门编辑页上，更改**预算**金额为 0.00 美元将英语系从 350,000.00 美元。</span><span class="sxs-lookup"><span data-stu-id="0601c-138">For example, John runs the Departments Edit page, changes the **Budget** amount for the English department from $350,000.00 to $0.00.</span></span>

<span data-ttu-id="0601c-139">John 单击之前**保存**，Jane 运行相同的页和更改**开始日期**字段从 9/1/2007年到 2013 年 8 月 8 日。</span><span class="sxs-lookup"><span data-stu-id="0601c-139">Before John clicks **Save**, Jane runs the same page and changes the **Start Date** field from 9/1/2007 to 8/8/2013.</span></span>

<span data-ttu-id="0601c-140">John 单击**保存**第一个和他的更改时在浏览器返回索引页上，然后 Jane 单击将看到**保存**。</span><span class="sxs-lookup"><span data-stu-id="0601c-140">John clicks **Save** first and sees his change when the browser returns to the Index page, then Jane clicks **Save**.</span></span> <span data-ttu-id="0601c-141">接下来的情况取决于并发冲突的处理方式。</span><span class="sxs-lookup"><span data-stu-id="0601c-141">What happens next is determined by how you handle concurrency conflicts.</span></span> <span data-ttu-id="0601c-142">其中一些选项包括：</span><span class="sxs-lookup"><span data-stu-id="0601c-142">Some of the options include the following:</span></span>

- <span data-ttu-id="0601c-143">可以跟踪用户已修改的属性，并仅更新数据库中相应的列。</span><span class="sxs-lookup"><span data-stu-id="0601c-143">You can keep track of which property a user has modified and update only the corresponding columns in the database.</span></span> <span data-ttu-id="0601c-144">在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。</span><span class="sxs-lookup"><span data-stu-id="0601c-144">In the example scenario, no data would be lost, because different properties were updated by the two users.</span></span> <span data-ttu-id="0601c-145">下次有人浏览英语系时，他们将看到 Jane 和 John 的更改 — 一个开始日期为 2013 年 8 月 8 日的和预算为零美元。</span><span class="sxs-lookup"><span data-stu-id="0601c-145">The next time someone browses the English department, they'll see both John's and Jane's changes — a start date of 8/8/2013 and a budget of Zero dollars.</span></span>

    <span data-ttu-id="0601c-146">这种更新方法可减少可能导致数据丢失的冲突次数，但是如果对实体的同一属性进行竞争性更改，则数据难免会丢失。</span><span class="sxs-lookup"><span data-stu-id="0601c-146">This method of updating can reduce the number of conflicts that could result in data loss, but it can't avoid data loss if competing changes are made to the same property of an entity.</span></span> <span data-ttu-id="0601c-147">Entity Framework 是否以这种方式工作取决于更新代码的实现方式。</span><span class="sxs-lookup"><span data-stu-id="0601c-147">Whether the Entity Framework works this way depends on how you implement your update code.</span></span> <span data-ttu-id="0601c-148">通常不适合在 Web 应用程序中使用，因为它要求保持大量的状态，以便跟踪实体的所有原始属性值以及新值。</span><span class="sxs-lookup"><span data-stu-id="0601c-148">It's often not practical in a web application, because it can require that you maintain large amounts of state in order to keep track of all original property values for an entity as well as new values.</span></span> <span data-ttu-id="0601c-149">维护大量的状态可能会影响应用程序的性能，因为它需要服务器资源或必须包含在网页本身（例如隐藏字段）或 Cookie 中。</span><span class="sxs-lookup"><span data-stu-id="0601c-149">Maintaining large amounts of state can affect application performance because it either requires server resources or must be included in the web page itself (for example, in hidden fields) or in a cookie.</span></span>
- <span data-ttu-id="0601c-150">可以让 John 的更改覆盖 Jane 的更改。</span><span class="sxs-lookup"><span data-stu-id="0601c-150">You can let Jane's change overwrite John's change.</span></span> <span data-ttu-id="0601c-151">下次有人浏览英语系时，他们将看到 2013 年 8 月 8 日和还原的值 350,000.00 美元。</span><span class="sxs-lookup"><span data-stu-id="0601c-151">The next time someone browses the English department, they'll see 8/8/2013 and the restored $350,000.00 value.</span></span> <span data-ttu-id="0601c-152">这称为“客户端优先”或“最后一个优先”。</span><span class="sxs-lookup"><span data-stu-id="0601c-152">This is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="0601c-153">（客户端的所有值优先于数据存储的值。）正如本部分的介绍所述，如果不为并发处理编写任何代码，则自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="0601c-153">(All values from the client take precedence over what's in the data store.) As noted in the introduction to this section, if you don't do any coding for concurrency handling, this will happen automatically.</span></span>
- <span data-ttu-id="0601c-154">您可以防止 Jane 的更改更新数据库中。</span><span class="sxs-lookup"><span data-stu-id="0601c-154">You can prevent Jane's change from being updated in the database.</span></span> <span data-ttu-id="0601c-155">通常情况下，将显示一条错误消息，给她提供数据的当前状态，让其以如果仍想要使其重新应用其更改。</span><span class="sxs-lookup"><span data-stu-id="0601c-155">Typically, you would display an error message, show her the current state of the data, and allow her to reapply her changes if she still wants to make them.</span></span> <span data-ttu-id="0601c-156">这称为“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="0601c-156">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="0601c-157">（数据存储值优先于客户端提交的值。）本教程将执行“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="0601c-157">(The data-store values take precedence over the values submitted by the client.) You'll implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="0601c-158">此方法可确保用户在未收到具体发生内容的警报时，不会覆盖任何更改。</span><span class="sxs-lookup"><span data-stu-id="0601c-158">This method ensures that no changes are overwritten without a user being alerted to what's happening.</span></span>

### <a name="detecting-concurrency-conflicts"></a><span data-ttu-id="0601c-159">检测并发冲突</span><span class="sxs-lookup"><span data-stu-id="0601c-159">Detecting Concurrency Conflicts</span></span>

<span data-ttu-id="0601c-160">您可以通过处理解决冲突[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) Entity Framework 引发的异常。</span><span class="sxs-lookup"><span data-stu-id="0601c-160">You can resolve conflicts by handling [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) exceptions that the Entity Framework throws.</span></span> <span data-ttu-id="0601c-161">为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-161">In order to know when to throw these exceptions, the Entity Framework must be able to detect conflicts.</span></span> <span data-ttu-id="0601c-162">因此，你必须正确配置数据库和数据模型。</span><span class="sxs-lookup"><span data-stu-id="0601c-162">Therefore, you must configure the database and the data model appropriately.</span></span> <span data-ttu-id="0601c-163">启用冲突检测的某些选项包括：</span><span class="sxs-lookup"><span data-stu-id="0601c-163">Some options for enabling conflict detection include the following:</span></span>

- <span data-ttu-id="0601c-164">数据库表中包含一个可用于确定某行更改时间的跟踪列。</span><span class="sxs-lookup"><span data-stu-id="0601c-164">In the database table, include a tracking column that can be used to determine when a row has been changed.</span></span> <span data-ttu-id="0601c-165">然后，可以配置实体框架，将该列中的包含`Where`的 SQL 子句`Update`或`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="0601c-165">You can then configure the Entity Framework to include that column in the `Where` clause of SQL `Update` or `Delete` commands.</span></span>

    <span data-ttu-id="0601c-166">跟踪列的数据类型通常是[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="0601c-166">The data type of the tracking column is typically [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx).</span></span> <span data-ttu-id="0601c-167">[Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新行时递增的序列号。</span><span class="sxs-lookup"><span data-stu-id="0601c-167">The [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) value is a sequential number that's incremented each time the row is updated.</span></span> <span data-ttu-id="0601c-168">在中`Update`或`Delete`命令，`Where`子句包含跟踪列 （原始行版本） 的原始值。</span><span class="sxs-lookup"><span data-stu-id="0601c-168">In an `Update` or `Delete` command, the `Where` clause includes the original value of the tracking column (the original row version).</span></span> <span data-ttu-id="0601c-169">如果正在更新的行已由另一个用户中的值更改`rowversion`列是不同于原始值，因此`Update`或`Delete`语句找不到要由于更新的行`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="0601c-169">If the row being updated has been changed by another user, the value in the `rowversion` column is different than the original value, so the `Update` or `Delete` statement can't find the row to update because of the `Where` clause.</span></span> <span data-ttu-id="0601c-170">当实体框架将查找已由更新任何行`Update`或`Delete`命令 （即，在受影响的行数为零），将其解释为并发冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-170">When the Entity Framework finds that no rows have been updated by the `Update` or `Delete` command (that is, when the number of affected rows is zero), it interprets that as a concurrency conflict.</span></span>
- <span data-ttu-id="0601c-171">配置实体框架，以便在表中包含的每个列的原始值`Where`子句`Update`和`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="0601c-171">Configure the Entity Framework to include the original values of every column in the table in the `Where` clause of `Update` and `Delete` commands.</span></span>

    <span data-ttu-id="0601c-172">如下所示的第一个选项，如果自第一次读取一行，该行中的任何内容已更改`Where`子句不会返回的行，若要更新，该实体框架将解释为并发冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-172">As in the first option, if anything in the row has changed since the row was first read, the `Where` clause won't return a row to update, which the Entity Framework interprets as a concurrency conflict.</span></span> <span data-ttu-id="0601c-173">对于包含许多列的数据库表，这种方法可能会导致非常大`Where`子句，并可能需要维护大量的状态。</span><span class="sxs-lookup"><span data-stu-id="0601c-173">For database tables that have many columns, this approach can result in very large `Where` clauses, and can require that you maintain large amounts of state.</span></span> <span data-ttu-id="0601c-174">如前所述，维持大量的状态会影响应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="0601c-174">As noted earlier, maintaining large amounts of state can affect application performance.</span></span> <span data-ttu-id="0601c-175">因此通常不建议使用此方法，并且它也不是本教程中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="0601c-175">Therefore this approach is generally not recommended, and it isn't the method used in this tutorial.</span></span>

    <span data-ttu-id="0601c-176">如果你确实想要实现此并发方法，则必须将您想要跟踪并发机制，通过添加在实体中的所有非主键属性标记[ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)属性到它们。</span><span class="sxs-lookup"><span data-stu-id="0601c-176">If you do want to implement this approach to concurrency, you have to mark all non-primary-key properties in the entity you want to track concurrency for by adding the [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) attribute to them.</span></span> <span data-ttu-id="0601c-177">更改使实体框架要包含在 SQL 中的所有列`WHERE`子句`UPDATE`语句。</span><span class="sxs-lookup"><span data-stu-id="0601c-177">That change enables the Entity Framework to include all columns in the SQL `WHERE` clause of `UPDATE` statements.</span></span>

<span data-ttu-id="0601c-178">在本教程的其余部分将添加[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)跟踪属性设置为`Department`实体，创建一个控制器和视图，并进行测试以验证是否一切运行正常。</span><span class="sxs-lookup"><span data-stu-id="0601c-178">In the remainder of this tutorial you'll add a [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tracking property to the `Department` entity, create a controller and views, and test to verify that everything works correctly.</span></span>

## <a name="add-optimistic-concurrency"></a><span data-ttu-id="0601c-179">添加乐观并发</span><span class="sxs-lookup"><span data-stu-id="0601c-179">Add optimistic concurrency</span></span>

<span data-ttu-id="0601c-180">在中*Models\Department.cs*，添加一个名为跟踪属性`RowVersion`:</span><span class="sxs-lookup"><span data-stu-id="0601c-180">In *Models\Department.cs*, add a tracking property named `RowVersion`:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

<span data-ttu-id="0601c-181">[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)属性指定此列将包含在`Where`子句`Update`和`Delete`命令发送到数据库。</span><span class="sxs-lookup"><span data-stu-id="0601c-181">The [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) attribute specifies that this column will be included in the `Where` clause of `Update` and `Delete` commands sent to the database.</span></span> <span data-ttu-id="0601c-182">该属性称为[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)因为以前版本的 SQL Server 使用 SQL[时间戳](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)之前使用 SQL 数据类型[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)替换它。</span><span class="sxs-lookup"><span data-stu-id="0601c-182">The attribute is called [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) because previous versions of SQL Server used a SQL [timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) data type before the SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) replaced it.</span></span> <span data-ttu-id="0601c-183">.Net 类型[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)是一个字节数组。</span><span class="sxs-lookup"><span data-stu-id="0601c-183">The .Net type for [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) is a byte array.</span></span>

<span data-ttu-id="0601c-184">如果你愿意使用 fluent API，则可以使用[IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)方法，以指定跟踪属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0601c-184">If you prefer to use the fluent API, you can use the [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) method to specify the tracking property, as shown in the following example:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="0601c-185">通过添加属性，更改了数据库模型，因此需要再执行一次迁移。</span><span class="sxs-lookup"><span data-stu-id="0601c-185">By adding a property you changed the database model, so you need to do another migration.</span></span> <span data-ttu-id="0601c-186">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="0601c-186">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-department-controller"></a><span data-ttu-id="0601c-187">修改部门控制器</span><span class="sxs-lookup"><span data-stu-id="0601c-187">Modify Department controller</span></span>

<span data-ttu-id="0601c-188">在中*Controllers\DepartmentController.cs*，添加`using`语句：</span><span class="sxs-lookup"><span data-stu-id="0601c-188">In *Controllers\DepartmentController.cs*, add a `using` statement:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="0601c-189">在中*DepartmentController.cs*文件中，将所有四个出现的"LastName"更改为"FullName"，以便院系管理员下拉列表将包含讲师的全名，而不是只是最后一个名称。</span><span class="sxs-lookup"><span data-stu-id="0601c-189">In the *DepartmentController.cs* file, change all four occurrences of "LastName" to "FullName" so that the department administrator drop-down lists will contain the full name of the instructor rather than just the last name.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

<span data-ttu-id="0601c-190">为现有代码替换为`HttpPost``Edit`方法使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="0601c-190">Replace the existing code for the `HttpPost` `Edit` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="0601c-191">如果 `FindAsync` 方法返回 NULL，则该院系已被另一用户删除。</span><span class="sxs-lookup"><span data-stu-id="0601c-191">If the `FindAsync` method returns null, the department was deleted by another user.</span></span> <span data-ttu-id="0601c-192">所示的代码使用已发布的表单值创建 department 实体，以便编辑页可以重新显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="0601c-192">The code shown uses the posted form values to create a department entity so that the Edit page can be redisplayed with an error message.</span></span> <span data-ttu-id="0601c-193">或者，如果仅显示错误消息而未重新显示院系字段，则不必重新创建 Department 实体。</span><span class="sxs-lookup"><span data-stu-id="0601c-193">As an alternative, you wouldn't have to re-create the department entity if you display only an error message without redisplaying the department fields.</span></span>

<span data-ttu-id="0601c-194">该视图将存储原始`RowVersion`隐藏的字段和方法中的值接收在`rowVersion`参数。</span><span class="sxs-lookup"><span data-stu-id="0601c-194">The view stores the original `RowVersion` value in a hidden field, and the method receives it in the `rowVersion` parameter.</span></span> <span data-ttu-id="0601c-195">在调用 `SaveChanges` 之前，必须将该原始 `RowVersion` 属性值置于实体的 `OriginalValues` 集合中。</span><span class="sxs-lookup"><span data-stu-id="0601c-195">Before you call `SaveChanges`, you have to put that original `RowVersion` property value in the `OriginalValues` collection for the entity.</span></span> <span data-ttu-id="0601c-196">然后当 Entity Framework 创建 SQL`UPDATE`命令时，命令将包括`WHERE`子句，用于查找的行具有原始`RowVersion`值。</span><span class="sxs-lookup"><span data-stu-id="0601c-196">Then when the Entity Framework creates a SQL `UPDATE` command, that command will include a `WHERE` clause that looks for a row that has the original `RowVersion` value.</span></span>

<span data-ttu-id="0601c-197">如果没有行受到`UPDATE`命令 (没有行具有原始`RowVersion`值)，实体框架将引发`DbUpdateConcurrencyException`异常和中的代码`catch`块获取受影响`Department`的异常中的实体对象。</span><span class="sxs-lookup"><span data-stu-id="0601c-197">If no rows are affected by the `UPDATE` command (no rows have the original `RowVersion` value), the Entity Framework throws a `DbUpdateConcurrencyException` exception, and the code in the `catch` block gets the affected `Department` entity from the exception object.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="0601c-198">此对象具有新值在用户输入其`Entity`属性，并且可以获取通过调用从数据库读取的值`GetDatabaseValues`方法。</span><span class="sxs-lookup"><span data-stu-id="0601c-198">This object has the new values entered by the user in its `Entity` property, and you can get the values read from the database by calling the `GetDatabaseValues` method.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="0601c-199">`GetDatabaseValues`方法将返回 null，如果有人已从数据库中删除行; 否则，您需要对返回的对象转换`Department`若要访问的类`Department`属性。</span><span class="sxs-lookup"><span data-stu-id="0601c-199">The `GetDatabaseValues` method returns null if someone has deleted the row from the database; otherwise, you have to cast the returned object to the `Department` class in order to access the `Department` properties.</span></span> <span data-ttu-id="0601c-200">(已检查的删除，因为`databaseEntry`将为 null 院系已被删除后，才`FindAsync`执行之前`SaveChanges`执行。)</span><span class="sxs-lookup"><span data-stu-id="0601c-200">(Because you already checked for deletion, `databaseEntry` would be null only if the department was deleted after `FindAsync` executes and before `SaveChanges` executes.)</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="0601c-201">接下来，代码将添加具有不同于在编辑页上输入的用户的数据库值的每个列的自定义错误消息：</span><span class="sxs-lookup"><span data-stu-id="0601c-201">Next, the code adds a custom error message for each column that has database values different from what the user entered on the Edit page:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="0601c-202">发生了什么情况以及如何进行处理，解释了较长的错误消息：</span><span class="sxs-lookup"><span data-stu-id="0601c-202">A longer error message explains what happened and what to do about it:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="0601c-203">最后，代码将设置`RowVersion`的值`Department`从数据库中检索到的新值的对象。</span><span class="sxs-lookup"><span data-stu-id="0601c-203">Finally, the code sets the `RowVersion` value of the `Department` object to the new value retrieved from the database.</span></span> <span data-ttu-id="0601c-204">重新显示“编辑”页时，这个新的 `RowVersion` 值将存储在隐藏字段中，当用户下次单击“保存”时，将只捕获自“编辑”页重新显示起发生的并发错误。</span><span class="sxs-lookup"><span data-stu-id="0601c-204">This new `RowVersion` value will be stored in the hidden field when the Edit page is redisplayed, and the next time the user clicks **Save**, only concurrency errors that happen since the redisplay of the Edit page will be caught.</span></span>

<span data-ttu-id="0601c-205">在中*Views\Department\Edit.cshtml*，添加隐藏的字段以保存`RowVersion`属性值，紧跟的隐藏的字段`DepartmentID`属性：</span><span class="sxs-lookup"><span data-stu-id="0601c-205">In *Views\Department\Edit.cshtml*, add a hidden field to save the `RowVersion` property value, immediately following the hidden field for the `DepartmentID` property:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="test-concurrency-handling"></a><span data-ttu-id="0601c-206">测试并发处理</span><span class="sxs-lookup"><span data-stu-id="0601c-206">Test concurrency handling</span></span>

<span data-ttu-id="0601c-207">运行站点，并单击**部门**。</span><span class="sxs-lookup"><span data-stu-id="0601c-207">Run the site and click **Departments**.</span></span>

<span data-ttu-id="0601c-208">右键单击**编辑**英语系和选择的超链接**新选项卡中打开**然后单击**编辑**英语系的超链接。</span><span class="sxs-lookup"><span data-stu-id="0601c-208">Right click the **Edit** hyperlink for the English department and select **Open in new tab,** then click the **Edit** hyperlink for the English department.</span></span> <span data-ttu-id="0601c-209">两个选项卡显示相同的信息。</span><span class="sxs-lookup"><span data-stu-id="0601c-209">The two tabs display the same information.</span></span>

<span data-ttu-id="0601c-210">在第一个浏览器选项卡中更改一个字段，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="0601c-210">Change a field in the first browser tab and click **Save**.</span></span>

<span data-ttu-id="0601c-211">浏览器显示具有更改值的索引页。</span><span class="sxs-lookup"><span data-stu-id="0601c-211">The browser shows the Index page with the changed value.</span></span>

<span data-ttu-id="0601c-212">更改第二个浏览器选项卡中的字段，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="0601c-212">Change a field in the second browser tab and click **Save**.</span></span> <span data-ttu-id="0601c-213">看见一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="0601c-213">You see an error message:</span></span>

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="0601c-215">再次单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="0601c-215">Click **Save** again.</span></span> <span data-ttu-id="0601c-216">在第二个浏览器选项卡中输入的值是随原始值的第一个浏览器中更改的数据一起保存。</span><span class="sxs-lookup"><span data-stu-id="0601c-216">The value you entered in the second browser tab is saved along with the original value of the data you changed in the first browser.</span></span> <span data-ttu-id="0601c-217">在索引页中出现时，可以看到已保存的值。</span><span class="sxs-lookup"><span data-stu-id="0601c-217">You see the saved values when the Index page appears.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="0601c-218">更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="0601c-218">Update the Delete page</span></span>

<span data-ttu-id="0601c-219">对于“删除”页，Entity Framework 以类似方式检测其他人编辑院系所引起的并发冲突。</span><span class="sxs-lookup"><span data-stu-id="0601c-219">For the Delete page, the Entity Framework detects concurrency conflicts caused by someone else editing the department in a similar manner.</span></span> <span data-ttu-id="0601c-220">当`HttpGet``Delete`方法会显示确认视图，该视图包含原始`RowVersion`隐藏字段中的值。</span><span class="sxs-lookup"><span data-stu-id="0601c-220">When the `HttpGet` `Delete` method displays the confirmation view, the view includes the original `RowVersion` value in a hidden field.</span></span> <span data-ttu-id="0601c-221">值为则供`HttpPost``Delete`在用户确认删除时调用的方法。</span><span class="sxs-lookup"><span data-stu-id="0601c-221">That value is then available to the `HttpPost` `Delete` method that's called when the user confirms the deletion.</span></span> <span data-ttu-id="0601c-222">当 Entity Framework 创建 SQL`DELETE`命令时，它包括`WHERE`子句与原始`RowVersion`值。</span><span class="sxs-lookup"><span data-stu-id="0601c-222">When the Entity Framework creates the SQL `DELETE` command, it includes a `WHERE` clause with the original `RowVersion` value.</span></span> <span data-ttu-id="0601c-223">如果命令导致零行受影响 （即数据行进行了更改后显示删除确认页），则引发并发异常，并`HttpGet Delete`错误标志设置为调用方法`true`以重新显示具有一条错误消息的确认页面。</span><span class="sxs-lookup"><span data-stu-id="0601c-223">If the command results in zero rows affected (meaning the row was changed after the Delete confirmation page was displayed), a concurrency exception is thrown, and the `HttpGet Delete` method is called with an error flag set to `true` in order to redisplay the confirmation page with an error message.</span></span> <span data-ttu-id="0601c-224">还有可能零行受影响，因为该行已由另一个用户删除，因此在这种情况下显示不同的错误消息。</span><span class="sxs-lookup"><span data-stu-id="0601c-224">It's also possible that zero rows were affected because the row was deleted by another user, so in that case a different error message is displayed.</span></span>

<span data-ttu-id="0601c-225">在中*DepartmentController.cs*，替换`HttpGet``Delete`方法使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="0601c-225">In *DepartmentController.cs*, replace the `HttpGet` `Delete` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="0601c-226">该方法接受可选参数，该参数指示是否在并发错误之后重新显示页面。</span><span class="sxs-lookup"><span data-stu-id="0601c-226">The method accepts an optional parameter that indicates whether the page is being redisplayed after a concurrency error.</span></span> <span data-ttu-id="0601c-227">如果此标志`true`，一条错误消息发送到视图使用`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="0601c-227">If this flag is `true`, an error message is sent to the view using a `ViewBag` property.</span></span>

<span data-ttu-id="0601c-228">中的代码替换`HttpPost``Delete`方法 (名为`DeleteConfirmed`) 使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="0601c-228">Replace the code in the `HttpPost` `Delete` method (named `DeleteConfirmed`) with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="0601c-229">在刚替换的基架代码中，此方法仅接受记录 ID：</span><span class="sxs-lookup"><span data-stu-id="0601c-229">In the scaffolded code that you just replaced, this method accepted only a record ID:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="0601c-230">你已更改此参数为`Department`模型绑定器创建的实体实例。</span><span class="sxs-lookup"><span data-stu-id="0601c-230">You've changed this parameter to a `Department` entity instance created by the model binder.</span></span> <span data-ttu-id="0601c-231">这使您可以访问`RowVersion`除记录键之外的属性值。</span><span class="sxs-lookup"><span data-stu-id="0601c-231">This gives you access to the `RowVersion` property value in addition to the record key.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="0601c-232">你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。</span><span class="sxs-lookup"><span data-stu-id="0601c-232">You have also changed the action method name from `DeleteConfirmed` to `Delete`.</span></span> <span data-ttu-id="0601c-233">基架的代码名为`HttpPost``Delete`方法`DeleteConfirmed`以便`HttpPost`方法唯一的签名。</span><span class="sxs-lookup"><span data-stu-id="0601c-233">The scaffolded code named the `HttpPost` `Delete` method `DeleteConfirmed` to give the `HttpPost` method a unique signature.</span></span> <span data-ttu-id="0601c-234">（CLR 要求重载的方法具有不同的方法参数。）签名是唯一的现在可以继续使用 MVC 约定，使用相同的名称`HttpPost`和`HttpGet`删除方法。</span><span class="sxs-lookup"><span data-stu-id="0601c-234">( The CLR requires overloaded methods to have different method parameters.) Now that the signatures are unique, you can stick with the MVC convention and use the same name for the `HttpPost` and `HttpGet` delete methods.</span></span>

<span data-ttu-id="0601c-235">如果捕获到并发错误，代码将重新显示“删除”确认页，并提供一个指示它应显示并发错误消息的标志。</span><span class="sxs-lookup"><span data-stu-id="0601c-235">If a concurrency error is caught, the code redisplays the Delete confirmation page and provides a flag that indicates it should display a concurrency error message.</span></span>

<span data-ttu-id="0601c-236">在中*Views\Department\Delete.cshtml*，基架的代码替换为以下代码添加错误消息字段和隐藏的字段的 DepartmentID 和 RowVersion 属性。</span><span class="sxs-lookup"><span data-stu-id="0601c-236">In *Views\Department\Delete.cshtml*, replace the scaffolded code with the following code that adds an error message field and hidden fields for the DepartmentID and RowVersion properties.</span></span> <span data-ttu-id="0601c-237">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="0601c-237">The changes are highlighted.</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

<span data-ttu-id="0601c-238">此代码将添加一条错误消息之间`h2`和`h3`标题：</span><span class="sxs-lookup"><span data-stu-id="0601c-238">This code adds an error message between the `h2` and `h3` headings:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="0601c-239">它将替换`LastName`与`FullName`中`Administrator`字段：</span><span class="sxs-lookup"><span data-stu-id="0601c-239">It replaces `LastName` with `FullName` in the `Administrator` field:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="0601c-240">最后，它将添加隐藏的字段`DepartmentID`并`RowVersion`后的，属性`Html.BeginForm`语句：</span><span class="sxs-lookup"><span data-stu-id="0601c-240">Finally, it adds hidden fields for the `DepartmentID` and `RowVersion` properties after the `Html.BeginForm` statement:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

<span data-ttu-id="0601c-241">运行院系索引页。</span><span class="sxs-lookup"><span data-stu-id="0601c-241">Run the Departments Index page.</span></span> <span data-ttu-id="0601c-242">右键单击**删除**英语系和选择的超链接**新选项卡中打开**然后在第一个选项卡中单击**编辑**英语系的超链接。</span><span class="sxs-lookup"><span data-stu-id="0601c-242">Right click the **Delete** hyperlink for the English department and select **Open in new tab,** then in the first tab click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="0601c-243">在第一个窗口，更改其中一个值，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="0601c-243">In the first window, change one of the values, and click **Save**.</span></span>

<span data-ttu-id="0601c-244">索引页会反映此更改。</span><span class="sxs-lookup"><span data-stu-id="0601c-244">The Index page confirms the change.</span></span>

<span data-ttu-id="0601c-245">在第二个选项卡中，单击“删除”。</span><span class="sxs-lookup"><span data-stu-id="0601c-245">In the second tab, click **Delete**.</span></span>

<span data-ttu-id="0601c-246">你将看到并发错误消息，且已使用数据库中的当前内容刷新了“院系”值。</span><span class="sxs-lookup"><span data-stu-id="0601c-246">You see the concurrency error message, and the Department values are refreshed with what's currently in the database.</span></span>

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

<span data-ttu-id="0601c-248">如果再次单击“删除”，会重定向到已删除显示院系的索引页。</span><span class="sxs-lookup"><span data-stu-id="0601c-248">If you click **Delete** again, you're redirected to the Index page, which shows that the department has been deleted.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="0601c-249">获取代码</span><span class="sxs-lookup"><span data-stu-id="0601c-249">Get the code</span></span>

[<span data-ttu-id="0601c-250">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="0601c-250">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="0601c-251">其他资源</span><span class="sxs-lookup"><span data-stu-id="0601c-251">Additional resources</span></span>

<span data-ttu-id="0601c-252">其他实体框架资源的链接可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="0601c-252">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="0601c-253">有关其他方法来处理各种方案，并发的信息，请参阅[乐观并发模式](https://msdn.microsoft.com/data/jj592904)并[属性值使用方面](https://msdn.microsoft.com/data/jj592677)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="0601c-253">For information about other ways to handle various concurrency scenarios, see [Optimistic Concurrency Patterns](https://msdn.microsoft.com/data/jj592904) and [Working with Property Values](https://msdn.microsoft.com/data/jj592677) on MSDN.</span></span> <span data-ttu-id="0601c-254">下一步的教程演示如何实现的每个层次结构一个表继承`Instructor`和`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="0601c-254">The next tutorial shows how to implement table-per-hierarchy inheritance for the `Instructor` and `Student` entities.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0601c-255">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0601c-255">Next steps</span></span>

<span data-ttu-id="0601c-256">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="0601c-256">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0601c-257">已了解并发冲突</span><span class="sxs-lookup"><span data-stu-id="0601c-257">Learned about concurrency conflicts</span></span>
> * <span data-ttu-id="0601c-258">添加了乐观并发</span><span class="sxs-lookup"><span data-stu-id="0601c-258">Added optimistic concurrency</span></span>
> * <span data-ttu-id="0601c-259">修改后的部门控制器</span><span class="sxs-lookup"><span data-stu-id="0601c-259">Modified Department controller</span></span>
> * <span data-ttu-id="0601c-260">测试的并发处理</span><span class="sxs-lookup"><span data-stu-id="0601c-260">Tested concurrency handling</span></span>
> * <span data-ttu-id="0601c-261">已更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="0601c-261">Updated the Delete page</span></span>

<span data-ttu-id="0601c-262">转到下一步的文章，了解如何在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="0601c-262">Advance to the next article to learn how to implement inheritance in the data model.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0601c-263">数据模型中实现继承</span><span class="sxs-lookup"><span data-stu-id="0601c-263">Implement inheritance in the data model</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
