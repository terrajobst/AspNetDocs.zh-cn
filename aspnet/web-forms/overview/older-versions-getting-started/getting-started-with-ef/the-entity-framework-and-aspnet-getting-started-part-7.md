---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第7部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78488522"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a><span data-ttu-id="0a2fd-104">入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第7部分</span><span class="sxs-lookup"><span data-stu-id="0a2fd-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 7</span></span>

<span data-ttu-id="0a2fd-105">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="0a2fd-106">Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="0a2fd-107">有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-stored-procedures"></a><span data-ttu-id="0a2fd-108">使用存储过程</span><span class="sxs-lookup"><span data-stu-id="0a2fd-108">Using Stored Procedures</span></span>

<span data-ttu-id="0a2fd-109">在上一教程中，您实现了每个层次结构一个表继承模式。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-109">In the previous tutorial you implemented a table-per-hierarchy inheritance pattern.</span></span> <span data-ttu-id="0a2fd-110">本教程将演示如何使用存储过程来获得对数据库访问的更多控制。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-110">This tutorial will show you how to use stored procedures to gain more control over database access.</span></span>

<span data-ttu-id="0a2fd-111">使用实体框架可以指定它应使用存储过程来访问数据库。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-111">The Entity Framework lets you specify that it should use stored procedures for database access.</span></span> <span data-ttu-id="0a2fd-112">对于任何实体类型，您可以指定用于创建、更新或删除该类型的实体的存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-112">For any entity type, you can specify a stored procedure to use for creating, updating, or deleting entities of that type.</span></span> <span data-ttu-id="0a2fd-113">然后，你可以在数据模型中添加对存储过程的引用，你可以使用这些引用来执行任务，例如检索实体集。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-113">Then in the data model you can add references to stored procedures that you can use to perform tasks such as retrieving sets of entities.</span></span>

<span data-ttu-id="0a2fd-114">使用存储过程是数据库访问的常见要求。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-114">Using stored procedures is a common requirement for database access.</span></span> <span data-ttu-id="0a2fd-115">在某些情况下，由于安全原因，数据库管理员可能要求所有数据库访问都要经过存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-115">In some cases a database administrator may require that all database access go through stored procedures for security reasons.</span></span> <span data-ttu-id="0a2fd-116">在其他情况下，你可能希望将业务逻辑构建到实体框架在更新数据库时使用的某些进程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-116">In other cases you may want to build business logic into some of the processes that the Entity Framework uses when it updates the database.</span></span> <span data-ttu-id="0a2fd-117">例如，在删除实体时，可能需要将其复制到存档数据库。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-117">For example, whenever an entity is deleted you might want to copy it to an archive database.</span></span> <span data-ttu-id="0a2fd-118">或每次更新行时，您可能想要在记录进行更改的记录表中写入一行。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-118">Or whenever a row is updated you might want to write a row to a logging table that records who made the change.</span></span> <span data-ttu-id="0a2fd-119">可以在存储过程中执行这些类型的任务，只要实体框架删除实体或更新实体，就会调用此存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-119">You can perform these kinds of tasks in a stored procedure that's called whenever the Entity Framework deletes an entity or updates an entity.</span></span>

<span data-ttu-id="0a2fd-120">如前面的教程中所述，你将不会创建任何新页。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-120">As in the previous tutorial, you'll not create any new pages.</span></span> <span data-ttu-id="0a2fd-121">相反，你将更改实体框架访问数据库以获取已创建的某些页面的方式。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-121">Instead, you'll change the way the Entity Framework accesses the database for some of the pages you already created.</span></span>

<span data-ttu-id="0a2fd-122">在本教程中，将在数据库中创建存储过程，用于插入 `Student` 和 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-122">In this tutorial you'll create stored procedures in the database for inserting `Student` and `Instructor` entities.</span></span> <span data-ttu-id="0a2fd-123">将它们添加到数据模型，并指定实体框架应使用这些数据模型将 `Student` 和 `Instructor` 实体添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-123">You'll add them to the data model, and you'll specify that the Entity Framework should use them for adding `Student` and `Instructor` entities to the database.</span></span> <span data-ttu-id="0a2fd-124">您还将创建一个可用于检索 `Course` 实体的存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-124">You'll also create a stored procedure that you can use to retrieve `Course` entities.</span></span>

## <a name="creating-stored-procedures-in-the-database"></a><span data-ttu-id="0a2fd-125">在数据库中创建存储过程</span><span class="sxs-lookup"><span data-stu-id="0a2fd-125">Creating Stored Procedures in the Database</span></span>

<span data-ttu-id="0a2fd-126">（如果要在本教程中使用可供下载的项目的*School .mdf*文件，则可以跳过此部分，因为存储过程已经存在。）</span><span class="sxs-lookup"><span data-stu-id="0a2fd-126">(If you're using the *School.mdf* file from the project available for download with this tutorial, you can skip this section because the stored procedures already exist.)</span></span>

<span data-ttu-id="0a2fd-127">在**服务器资源管理器**中，展开 " *School*"，右键单击 "**存储过程**"，然后选择 "**添加新存储过程**"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-127">In **Server Explorer**, expand *School.mdf*, right-click **Stored Procedures**, and select **Add New Stored Procedure**.</span></span>

<span data-ttu-id="0a2fd-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span></span>

<span data-ttu-id="0a2fd-129">复制以下 SQL 语句，并将其粘贴到 "存储过程" 窗口中，并替换主干存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-129">Copy the following SQL statements and paste them into the stored procedure window, replacing the skeleton stored procedure.</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

<span data-ttu-id="0a2fd-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span></span>

<span data-ttu-id="0a2fd-131">`Student` 实体具有四个属性： "`PersonID`"、"`LastName`"、"`FirstName`" 和 "`EnrollmentDate`"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-131">`Student` entities have four properties: `PersonID`, `LastName`, `FirstName`, and `EnrollmentDate`.</span></span> <span data-ttu-id="0a2fd-132">数据库自动生成 ID 值，存储过程接受另外三个参数。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-132">The database generates the ID value automatically, and the stored procedure accepts parameters for the other three.</span></span> <span data-ttu-id="0a2fd-133">该存储过程返回新行的记录键的值，以便实体框架可以跟踪它在内存中保留的实体版本。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-133">The stored procedure returns the value of the new row's record key so that the Entity Framework can keep track of that in the version of the entity it keeps in memory.</span></span>

<span data-ttu-id="0a2fd-134">保存并关闭 "存储过程" 窗口。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-134">Save and close the stored procedure window.</span></span>

<span data-ttu-id="0a2fd-135">使用以下 SQL 语句以相同方式创建 `InsertInstructor` 存储过程：</span><span class="sxs-lookup"><span data-stu-id="0a2fd-135">Create an `InsertInstructor` stored procedure in the same manner, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

<span data-ttu-id="0a2fd-136">同时为 `Student` 和 `Instructor` 实体创建 `Update` 存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-136">Create `Update` stored procedures for `Student` and `Instructor` entities also.</span></span> <span data-ttu-id="0a2fd-137">（数据库已具有一个 `DeletePerson` 存储过程，该过程适用于 `Instructor` 和 `Student` 实体。）</span><span class="sxs-lookup"><span data-stu-id="0a2fd-137">(The database already has a `DeletePerson` stored procedure which will work for both `Instructor` and `Student` entities.)</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

<span data-ttu-id="0a2fd-138">在本教程中，您将为每个实体类型映射所有三个函数（插入、更新和删除）。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-138">In this tutorial you'll map all three functions -- insert, update, and delete -- for each entity type.</span></span> <span data-ttu-id="0a2fd-139">使用实体框架版本4，只需将其中一个或两个函数映射到存储过程，而无需映射其他函数，但有一个例外：如果映射更新函数但不映射 delete 函数实体框架，则在您尝试删除实体。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-139">The Entity Framework version 4 allows you to map just one or two of these functions to stored procedures without mapping the others, with one exception: if you map the update function but not the delete function, the Entity Framework will throw an exception when you attempt to delete an entity.</span></span> <span data-ttu-id="0a2fd-140">在实体框架版本3.5 中，你在映射存储过程时没有这么大的灵活性：如果映射了一个函数，则需要映射所有这三个函数。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-140">In the Entity Framework version 3.5, you did not have this much flexibility in mapping stored procedures: if you mapped one function you were required to map all three.</span></span>

<span data-ttu-id="0a2fd-141">若要创建读取而不是更新数据的存储过程，请使用以下 SQL 语句创建一个选择所有 `Course` 实体的存储过程：</span><span class="sxs-lookup"><span data-stu-id="0a2fd-141">To create a stored procedure that reads rather than updates data, create one that selects all `Course` entities, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a><span data-ttu-id="0a2fd-142">向数据模型添加存储过程</span><span class="sxs-lookup"><span data-stu-id="0a2fd-142">Adding the Stored Procedures to the Data Model</span></span>

<span data-ttu-id="0a2fd-143">现在，数据库中定义了这些存储过程，但必须将这些存储过程添加到数据模型，以使它们可用于实体框架。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-143">The stored procedures are now defined in the database, but they must be added to the data model to make them available to the Entity Framework.</span></span> <span data-ttu-id="0a2fd-144">打开*SchoolModel*，右键单击设计图面，然后选择 "**从数据库更新模型**"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-144">Open *SchoolModel.edmx*, right-click the design surface, and select **Update Model from Database**.</span></span> <span data-ttu-id="0a2fd-145">在 "**选择数据库对象**" 对话框的 "**添加**" 选项卡中，展开 "**存储过程**"，选择新创建的存储过程和 `DeletePerson` 存储过程，然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-145">In the **Add** tab of the **Choose Your Database Objects** dialog box, expand **Stored Procedures**, select the newly created stored procedures and the `DeletePerson` stored procedure, and then click **Finish**.</span></span>

<span data-ttu-id="0a2fd-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span></span>

## <a name="mapping-the-stored-procedures"></a><span data-ttu-id="0a2fd-147">映射存储过程</span><span class="sxs-lookup"><span data-stu-id="0a2fd-147">Mapping the Stored Procedures</span></span>

<span data-ttu-id="0a2fd-148">在数据模型设计器中，右键单击 `Student` 实体，然后选择 "**存储过程映射**"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-148">In the data model designer, right-click the `Student` entity and select **Stored Procedure Mapping**.</span></span>

<span data-ttu-id="0a2fd-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span></span>

<span data-ttu-id="0a2fd-150">此时将显示 "**映射详细信息**" 窗口，您可以在其中指定实体框架用于插入、更新和删除此类型的实体的存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-150">The **Mapping Details** window appears, in which you can specify stored procedures that the Entity Framework should use for inserting, updating, and deleting entities of this type.</span></span>

<span data-ttu-id="0a2fd-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span></span>

<span data-ttu-id="0a2fd-152">将**Insert**函数设置为**InsertStudent**。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-152">Set the **Insert** function to **InsertStudent**.</span></span> <span data-ttu-id="0a2fd-153">此窗口将显示存储过程参数的列表，其中每个参数都必须映射到实体属性。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-153">The window shows a list of stored procedure parameters, each of which must be mapped to an entity property.</span></span> <span data-ttu-id="0a2fd-154">其中两个将自动映射，因为名称相同。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-154">Two of these are mapped automatically because the names are the same.</span></span> <span data-ttu-id="0a2fd-155">没有名为 `FirstName`的实体属性，因此您必须从显示可用实体属性的下拉列表中手动选择 `FirstMidName`。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-155">There's no entity property named `FirstName`, so you must manually select `FirstMidName` from a drop-down list that shows available entity properties.</span></span> <span data-ttu-id="0a2fd-156">（这是因为您在第一个教程中已将 `FirstName` 属性的名称更改为 `FirstMidName`。）</span><span class="sxs-lookup"><span data-stu-id="0a2fd-156">(This is because you changed the name of the `FirstName` property to `FirstMidName` in the first tutorial.)</span></span>

<span data-ttu-id="0a2fd-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span></span>

<span data-ttu-id="0a2fd-158">在相同的 "**映射详细信息**" 窗口中，将 `Update` 函数映射到 `UpdateStudent` 存储过程（请确保将 `FirstMidName` 指定为 `FirstName`的参数值，与 `Insert` 存储过程的参数值相同），并将 `Delete` 函数指定给 `DeletePerson` 存储过程。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-158">In the same **Mapping Details** window, map the `Update` function to the `UpdateStudent` stored procedure (make sure you specify `FirstMidName` as the parameter value for `FirstName`, as you did for the `Insert` stored procedure) and the `Delete` function to the `DeletePerson` stored procedure.</span></span>

<span data-ttu-id="0a2fd-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span></span>

<span data-ttu-id="0a2fd-160">按照相同的过程将讲师的 insert、update 和 delete 存储过程映射到 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-160">Follow the same procedure to map the insert, update, and delete stored procedures for instructors to the `Instructor` entity.</span></span>

<span data-ttu-id="0a2fd-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span></span>

<span data-ttu-id="0a2fd-162">对于读取而不是更新数据的存储过程，您可以使用 "**模型浏览器**" 窗口将存储过程映射到它返回的实体类型。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-162">For stored procedures that read rather than update data, you use the **Model Browser** window to map the stored procedure to the entity type it returns.</span></span> <span data-ttu-id="0a2fd-163">在数据模型设计器中，右键单击设计图面，然后选择 "**模型浏览器**"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-163">In the data model designer, right-click the design surface and select **Model Browser**.</span></span> <span data-ttu-id="0a2fd-164">打开 " **SchoolModel** " 节点，然后打开 "**存储过程**" 节点。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-164">Open the **SchoolModel.Store** node and then open the **Stored Procedures** node.</span></span> <span data-ttu-id="0a2fd-165">然后右键单击 `GetCourses` 存储过程，然后选择 "**添加函数导入**"。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-165">Then right-click the `GetCourses` stored procedure and select **Add Function Import**.</span></span>

<span data-ttu-id="0a2fd-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span></span>

<span data-ttu-id="0a2fd-167">在 "**添加函数导入**" 对话框中，在 "返回选择**实体** **的集合**" 下，选择 "`Course` 作为返回的实体类型。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-167">In the **Add Function Import** dialog box, under **Returns a Collection Of** select **Entities**, and then select `Course` as the entity type returned.</span></span> <span data-ttu-id="0a2fd-168">完成后，单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-168">When you're done, click **OK**.</span></span> <span data-ttu-id="0a2fd-169">保存并关闭 *.edmx*文件。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-169">Save and close the *.edmx* file.</span></span>

<span data-ttu-id="0a2fd-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span></span>

## <a name="using-insert-update-and-delete-stored-procedures"></a><span data-ttu-id="0a2fd-171">使用 Insert、Update 和 Delete 存储过程</span><span class="sxs-lookup"><span data-stu-id="0a2fd-171">Using Insert, Update, and Delete Stored Procedures</span></span>

<span data-ttu-id="0a2fd-172">用于插入、更新和删除数据的存储过程在您将数据添加到数据模型并将其映射到相应的实体后，会自动由实体框架使用。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-172">Stored procedures to insert, update, and delete data are used by the Entity Framework automatically after you've added them to the data model and mapped them to the appropriate entities.</span></span> <span data-ttu-id="0a2fd-173">现在，你可以运行*StudentsAdd*页，每次创建新的学生时，实体框架将使用 `InsertStudent` 存储过程向 `Student` 表中添加新行。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-173">You can now run the *StudentsAdd.aspx* page, and every time you create a new student, the Entity Framework will use the `InsertStudent` stored procedure to add the new row to the `Student` table.</span></span>

<span data-ttu-id="0a2fd-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span></span>

<span data-ttu-id="0a2fd-175">运行 student*页，* 新学生显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-175">Run the *Students.aspx* page and the new student appears in the list.</span></span>

<span data-ttu-id="0a2fd-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span></span>

<span data-ttu-id="0a2fd-177">更改该名称以验证更新函数是否正常工作，然后删除该学生以验证删除函数是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-177">Change the name to verify that the update function works, and then delete the student to verify that the delete function works.</span></span>

<span data-ttu-id="0a2fd-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span></span>

## <a name="using-select-stored-procedures"></a><span data-ttu-id="0a2fd-179">使用 Select 存储过程</span><span class="sxs-lookup"><span data-stu-id="0a2fd-179">Using Select Stored Procedures</span></span>

<span data-ttu-id="0a2fd-180">实体框架不会自动运行存储过程（如 `GetCourses`），也不能将其与 `EntityDataSource` 控件一起使用。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-180">The Entity Framework does not automatically run stored procedures such as `GetCourses`, and you cannot use them with the `EntityDataSource` control.</span></span> <span data-ttu-id="0a2fd-181">若要使用它们，请从代码中调用它们。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-181">To use them, you call them from code.</span></span>

<span data-ttu-id="0a2fd-182">打开*InstructorsCourses.aspx.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-182">Open the *InstructorsCourses.aspx.cs* file.</span></span> <span data-ttu-id="0a2fd-183">`PopulateDropDownLists` 方法使用 LINQ to entities 查询来检索所有课程实体，以便它可以循环遍历列表并确定哪些指导员分配给了指导员，哪些未分配：</span><span class="sxs-lookup"><span data-stu-id="0a2fd-183">The `PopulateDropDownLists` method uses a LINQ-to-Entities query to retrieve all course entities so that it can loop through the list and determine which ones an instructor is assigned to and which ones are unassigned:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

<span data-ttu-id="0a2fd-184">将此代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="0a2fd-184">Replace this with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

<span data-ttu-id="0a2fd-185">该页现在使用 `GetCourses` 存储过程来检索所有课程的列表。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-185">The page now uses the `GetCourses` stored procedure to retrieve the list of all courses.</span></span> <span data-ttu-id="0a2fd-186">运行页面，验证其工作方式是否与以前相同。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-186">Run the page to verify that it works as it did before.</span></span>

<span data-ttu-id="0a2fd-187">（存储过程检索到的实体的导航属性可能不会自动填充与这些实体相关的数据，具体取决于 `ObjectContext` 默认设置。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-187">(Navigation properties of entities retrieved by a stored procedure might not be automatically populated with the data related to those entities, depending on `ObjectContext` default settings.</span></span> <span data-ttu-id="0a2fd-188">有关详细信息，请参阅 MSDN Library 中的[加载相关对象](https://msdn.microsoft.com/library/bb896272.aspx)。）</span><span class="sxs-lookup"><span data-stu-id="0a2fd-188">For more information, see [Loading Related Objects](https://msdn.microsoft.com/library/bb896272.aspx) in the MSDN Library.)</span></span>

<span data-ttu-id="0a2fd-189">在下一教程中，你将了解如何使用动态数据功能，以便更轻松地对数据格式设置和验证规则进行编程和测试。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-189">In the next tutorial, you'll learn how to use Dynamic Data functionality to make it easier to program and test data formatting and validation rules.</span></span> <span data-ttu-id="0a2fd-190">您可以在数据模型元数据中指定此类规则，而不是在每个网页规则（例如数据格式字符串和是否需要某个字段）上指定此类规则，而是在每个页面上自动应用这些规则。</span><span class="sxs-lookup"><span data-stu-id="0a2fd-190">Instead of specifying on each web page rules such as data format strings and whether or not a field is required, you can specify such rules in data model metadata and they're automatically applied on every page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a2fd-191">[上一页](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="0a2fd-191">[Previous](the-entity-framework-and-aspnet-getting-started-part-6.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-8.md)</span></span>
