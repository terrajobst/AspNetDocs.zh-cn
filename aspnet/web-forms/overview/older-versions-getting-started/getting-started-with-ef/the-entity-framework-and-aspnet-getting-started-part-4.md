---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第4部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518282"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="89b47-104">入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第4部分</span><span class="sxs-lookup"><span data-stu-id="89b47-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>

<span data-ttu-id="89b47-105">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="89b47-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="89b47-106">Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="89b47-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="89b47-107">有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="89b47-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data"></a><span data-ttu-id="89b47-108">使用相关数据</span><span class="sxs-lookup"><span data-stu-id="89b47-108">Working with Related Data</span></span>

<span data-ttu-id="89b47-109">在上一教程中，您使用了 `EntityDataSource` 控件对数据进行筛选、排序和分组。</span><span class="sxs-lookup"><span data-stu-id="89b47-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="89b47-110">在本教程中，您将显示和更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="89b47-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="89b47-111">你将创建显示指导员列表的 "讲师" 页。</span><span class="sxs-lookup"><span data-stu-id="89b47-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="89b47-112">选择指导员后，会看到该教师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="89b47-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="89b47-113">选择课程后，你将看到课程的详细信息以及在课程中注册的学生列表。</span><span class="sxs-lookup"><span data-stu-id="89b47-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="89b47-114">可以编辑讲师名称、雇用日期和办公室分配。</span><span class="sxs-lookup"><span data-stu-id="89b47-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="89b47-115">Office 分配是通过导航属性访问的单独实体集。</span><span class="sxs-lookup"><span data-stu-id="89b47-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="89b47-116">可以在标记或代码中将主数据链接到详细信息数据。</span><span class="sxs-lookup"><span data-stu-id="89b47-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="89b47-117">在本教程的此部分中，将使用这两种方法。</span><span class="sxs-lookup"><span data-stu-id="89b47-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="89b47-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="89b47-119">显示并更新 GridView 控件中的相关实体</span><span class="sxs-lookup"><span data-stu-id="89b47-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="89b47-120">创建一个名为 "*指导员*" 的新网页，其中使用 "*站点*母版页" 母版页，并将以下标记添加到名为 `Content2`的 `Content` 控件：</span><span class="sxs-lookup"><span data-stu-id="89b47-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="89b47-121">此标记创建一个 `EntityDataSource` 控件，该控件选择指导员并启用更新。</span><span class="sxs-lookup"><span data-stu-id="89b47-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="89b47-122">`div` 元素将标记配置为在左侧呈现，以便以后可以在右侧添加列。</span><span class="sxs-lookup"><span data-stu-id="89b47-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="89b47-123">在 `EntityDataSource` 标记和结束 `</div>` 标记之间，添加用于创建 `GridView` 控件的以下标记和用于错误消息的 `Label` 控件：</span><span class="sxs-lookup"><span data-stu-id="89b47-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="89b47-124">此 `GridView` 控件启用行选择，突出显示带有浅灰色背景色的选定行，并指定 `SelectedIndexChanged` 和 `Updating` 事件的处理程序（稍后将创建）。</span><span class="sxs-lookup"><span data-stu-id="89b47-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="89b47-125">它还为 `DataKeyNames` 属性指定 `PersonID`，以便可以将所选行的键值传递给稍后将添加的另一个控件。</span><span class="sxs-lookup"><span data-stu-id="89b47-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="89b47-126">最后一列包含讲师的办公室分配，它存储在 `Person` 实体的导航属性中，因为它来自关联的实体。</span><span class="sxs-lookup"><span data-stu-id="89b47-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="89b47-127">请注意，`EditItemTemplate` 元素指定了 `Eval` 而不是 `Bind`，因为 `GridView` 控件无法直接绑定到导航属性来更新这些属性。</span><span class="sxs-lookup"><span data-stu-id="89b47-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="89b47-128">你将在代码中更新 office 分配。</span><span class="sxs-lookup"><span data-stu-id="89b47-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="89b47-129">为此，需要引用 `TextBox` 控件，并在 `TextBox` 控件的 `Init` 事件中获取并保存该控件。</span><span class="sxs-lookup"><span data-stu-id="89b47-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="89b47-130">下面的 `GridView` 控件是一个用于错误消息的 `Label` 控件。</span><span class="sxs-lookup"><span data-stu-id="89b47-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="89b47-131">控件的 `Visible` 属性是 `false`的，并且关闭了视图状态，因此，只有当代码使其在响应错误时显示时，才会显示该标签。</span><span class="sxs-lookup"><span data-stu-id="89b47-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="89b47-132">打开*Instructors.aspx.cs*文件并添加以下 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="89b47-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="89b47-133">直接在分部类名称声明后面添加私有类字段，以保存对 "office 赋值" 文本框的引用。</span><span class="sxs-lookup"><span data-stu-id="89b47-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="89b47-134">为稍后将添加代码的 `SelectedIndexChanged` 事件处理程序添加存根。</span><span class="sxs-lookup"><span data-stu-id="89b47-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="89b47-135">同时，为 office 分配 `TextBox` 控件的 `Init` 事件添加处理程序，以便可以存储对 `TextBox` 控件的引用。</span><span class="sxs-lookup"><span data-stu-id="89b47-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="89b47-136">你将使用此引用获取用户输入的值，以便更新与导航属性关联的实体。</span><span class="sxs-lookup"><span data-stu-id="89b47-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="89b47-137">你将使用 `GridView` 控件的 `Updating` 事件来更新关联 `OfficeAssignment` 实体的 `Location` 属性。</span><span class="sxs-lookup"><span data-stu-id="89b47-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="89b47-138">为 `Updating` 事件添加以下处理程序：</span><span class="sxs-lookup"><span data-stu-id="89b47-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="89b47-139">当用户在 `GridView` 行中单击 "**更新**" 时，将运行此代码。</span><span class="sxs-lookup"><span data-stu-id="89b47-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="89b47-140">代码使用 LINQ to Entities 检索与当前 `Person` 实体关联的 `OfficeAssignment` 实体，使用事件参数中所选行的 `PersonID`。</span><span class="sxs-lookup"><span data-stu-id="89b47-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="89b47-141">然后，该代码根据 `InstructorOfficeTextBox` 控件中的值执行以下操作之一：</span><span class="sxs-lookup"><span data-stu-id="89b47-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="89b47-142">如果文本框具有值并且没有要更新的 `OfficeAssignment` 实体，则创建一个。</span><span class="sxs-lookup"><span data-stu-id="89b47-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="89b47-143">如果文本框具有值并且有一个 `OfficeAssignment` 实体，则会更新 `Location` 属性值。</span><span class="sxs-lookup"><span data-stu-id="89b47-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="89b47-144">如果文本框为空，并且存在 `OfficeAssignment` 实体，则会删除该实体。</span><span class="sxs-lookup"><span data-stu-id="89b47-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="89b47-145">之后，它会将更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="89b47-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="89b47-146">如果发生异常，它将显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="89b47-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="89b47-147">运行页面。</span><span class="sxs-lookup"><span data-stu-id="89b47-147">Run the page.</span></span>

<span data-ttu-id="89b47-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="89b47-149">单击 "**编辑**"，所有字段都将更改为 "文本框"。</span><span class="sxs-lookup"><span data-stu-id="89b47-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="89b47-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="89b47-151">更改其中的任何值，包括**Office 分配**。</span><span class="sxs-lookup"><span data-stu-id="89b47-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="89b47-152">单击 "**更新**"，你将看到反映在列表中的更改。</span><span class="sxs-lookup"><span data-stu-id="89b47-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="89b47-153">在单独的控件中显示相关实体</span><span class="sxs-lookup"><span data-stu-id="89b47-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="89b47-154">每位讲师都可以讲授一个或多个课程，因此你将添加一个 `EntityDataSource` 控件和一个 `GridView` 控件，以列出与在讲师 `GridView` 控件中选择的任何指导员关联的课程。</span><span class="sxs-lookup"><span data-stu-id="89b47-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="89b47-155">若要为课程实体创建标题和 `EntityDataSource` 控件，请在错误消息 `Label` 控件和结束 `</div>` 标记之间添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="89b47-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="89b47-156">`Where` 参数包含在 `InstructorsGridView` 控件中选择了其行的指导员 `PersonID` 的值。</span><span class="sxs-lookup"><span data-stu-id="89b47-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="89b47-157">`Where` 属性包含一个选择的命令，该命令从 `Course` 实体的 `People` 导航属性获取所有关联的 `Person` 实体，并且仅当其中一个关联 `Course` 实体包含所选 `Person` 值时，才选择 `PersonID` 实体。</span><span class="sxs-lookup"><span data-stu-id="89b47-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="89b47-158">若要创建 `GridView` 控件，请在 `CoursesEntityDataSource` 控件之后（在结束 `</div>` 标记之前）添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="89b47-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="89b47-159">由于未选择任何教师，因此不会显示任何课程，将包含 `EmptyDataTemplate` 元素。</span><span class="sxs-lookup"><span data-stu-id="89b47-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="89b47-160">运行页面。</span><span class="sxs-lookup"><span data-stu-id="89b47-160">Run the page.</span></span>

<span data-ttu-id="89b47-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="89b47-162">选择已分配一个或多个课程的指导员，课程或课程显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="89b47-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="89b47-163">（注意：尽管数据库架构允许多个课程，但在数据库中提供的测试数据中，任何讲师都没有多个课程。</span><span class="sxs-lookup"><span data-stu-id="89b47-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="89b47-164">您可以使用 "**服务器资源管理器**" 窗口或 " *CoursesAdd* " 页（将在后面的教程中添加），自行将课程添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="89b47-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="89b47-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="89b47-166">`CoursesGridView` 控件只显示几个课程字段。</span><span class="sxs-lookup"><span data-stu-id="89b47-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="89b47-167">若要显示课程的所有详细信息，您将为用户选择的课程使用 `DetailsView` 控件。</span><span class="sxs-lookup"><span data-stu-id="89b47-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="89b47-168">在*default.aspx*中，在结束标记 `</div>` 标记后添加以下标记（确保将此标记放在关闭 div 标记**后面**，而不是在其之前）：</span><span class="sxs-lookup"><span data-stu-id="89b47-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="89b47-169">此标记创建一个绑定到 `Courses` 实体集的 `EntityDataSource` 控件。</span><span class="sxs-lookup"><span data-stu-id="89b47-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="89b47-170">`Where` 属性使用课程 `GridView` 控件中所选行的 `CourseID` 值选择一个课程。</span><span class="sxs-lookup"><span data-stu-id="89b47-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="89b47-171">标记为 `Selected` 事件指定处理程序，稍后将用于显示学生成绩，这是层次结构中较低级别的另一层。</span><span class="sxs-lookup"><span data-stu-id="89b47-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="89b47-172">在*Instructors.aspx.cs*中，为 `CourseDetailsEntityDataSource_Selected` 方法创建以下存根。</span><span class="sxs-lookup"><span data-stu-id="89b47-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="89b47-173">（你将在本教程的后面部分填写此存根; 目前你需要它，以便编译和运行页面。）</span><span class="sxs-lookup"><span data-stu-id="89b47-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="89b47-174">运行页面。</span><span class="sxs-lookup"><span data-stu-id="89b47-174">Run the page.</span></span>

<span data-ttu-id="89b47-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="89b47-176">最初没有课程详细信息，因为未选择任何课程。</span><span class="sxs-lookup"><span data-stu-id="89b47-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="89b47-177">选择已分配课程的指导员，然后选择某一课程以查看详细信息。</span><span class="sxs-lookup"><span data-stu-id="89b47-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="89b47-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="89b47-179">使用 EntityDataSource "Selected" 事件显示相关数据</span><span class="sxs-lookup"><span data-stu-id="89b47-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="89b47-180">最后，您需要为所选课程显示所有注册的学生及其成绩。</span><span class="sxs-lookup"><span data-stu-id="89b47-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="89b47-181">为此，您将使用绑定到课程 `DetailsView`的 `EntityDataSource` 控件的 `Selected` 事件。</span><span class="sxs-lookup"><span data-stu-id="89b47-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="89b47-182">在*default.aspx*中，将以下标记添加到 `DetailsView` 控件之后：</span><span class="sxs-lookup"><span data-stu-id="89b47-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="89b47-183">此标记创建一个 `ListView` 控件，该控件显示学生的列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="89b47-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="89b47-184">未指定数据源，因为您将在代码中 databind 控件。</span><span class="sxs-lookup"><span data-stu-id="89b47-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="89b47-185">`EmptyDataTemplate` 元素提供了在未选择任何课程时要显示的消息—在这种情况下，没有要显示的学生。</span><span class="sxs-lookup"><span data-stu-id="89b47-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="89b47-186">`LayoutTemplate` 元素创建一个用于显示列表的 HTML 表，`ItemTemplate` 指定要显示的列。</span><span class="sxs-lookup"><span data-stu-id="89b47-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="89b47-187">学生 ID 和学生评分来自 `StudentGrade` 实体，而学生姓名来自 `Person` 实体，实体框架在 `StudentGrade` 实体的 `Person` 导航属性中提供该名称。</span><span class="sxs-lookup"><span data-stu-id="89b47-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="89b47-188">在*Instructors.aspx.cs*中，将用作存根 `CourseDetailsEntityDataSource_Selected` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="89b47-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="89b47-189">此事件的事件参数以集合的形式提供选定的数据，如果未选择任何内容，则将提供零项; 如果选择了 `Course` 实体，则为一个项。</span><span class="sxs-lookup"><span data-stu-id="89b47-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="89b47-190">如果选择 `Course` 实体，则代码将使用 `First` 方法将集合转换为单个对象。</span><span class="sxs-lookup"><span data-stu-id="89b47-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="89b47-191">然后，它从导航属性中获取 `StudentGrade` 实体，将它们转换为集合，并将 `GradesListView` 控件绑定到集合。</span><span class="sxs-lookup"><span data-stu-id="89b47-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="89b47-192">这足以显示成绩，但你想要确保在第一次显示页面时和未选择课程时显示空数据模板中的消息。</span><span class="sxs-lookup"><span data-stu-id="89b47-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="89b47-193">为此，请创建以下方法，从两个位置调用：</span><span class="sxs-lookup"><span data-stu-id="89b47-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="89b47-194">从 `Page_Load` 方法中调用这一新方法，以便在第一次显示该页时显示空数据模板。</span><span class="sxs-lookup"><span data-stu-id="89b47-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="89b47-195">并从 `InstructorsGridView_SelectedIndexChanged` 方法中调用该事件，因为在选择了指导员时将引发该事件，这意味着将新课程加载到课程 `GridView` 控制，但尚未选择 "无"。</span><span class="sxs-lookup"><span data-stu-id="89b47-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="89b47-196">下面是两个调用：</span><span class="sxs-lookup"><span data-stu-id="89b47-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="89b47-197">运行页面。</span><span class="sxs-lookup"><span data-stu-id="89b47-197">Run the page.</span></span>

<span data-ttu-id="89b47-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="89b47-199">选择已分配课程的指导员，然后选择该课程。</span><span class="sxs-lookup"><span data-stu-id="89b47-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="89b47-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="89b47-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="89b47-201">你现在已经了解了几种处理相关数据的方法。</span><span class="sxs-lookup"><span data-stu-id="89b47-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="89b47-202">在以下教程中，您将学习如何在现有实体之间添加关系、如何删除关系，以及如何添加具有与现有实体的关系的新实体。</span><span class="sxs-lookup"><span data-stu-id="89b47-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="89b47-203">[上一页](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="89b47-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>
