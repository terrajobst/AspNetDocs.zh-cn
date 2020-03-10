---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web Forms-第5部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423866"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a><span data-ttu-id="0c0a6-104">入门实体框架 4.0 Database First 和 ASP.NET 4 Web Forms-第5部分</span><span class="sxs-lookup"><span data-stu-id="0c0a6-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 5</span></span>

<span data-ttu-id="0c0a6-105">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="0c0a6-106">Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="0c0a6-107">有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data-continued"></a><span data-ttu-id="0c0a6-108">使用相关数据（续）</span><span class="sxs-lookup"><span data-stu-id="0c0a6-108">Working with Related Data, Continued</span></span>

<span data-ttu-id="0c0a6-109">在上一教程中，您开始使用 `EntityDataSource` 控件来处理相关数据。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-109">In the previous tutorial you began to use the `EntityDataSource` control to work with related data.</span></span> <span data-ttu-id="0c0a6-110">您在导航属性中显示了多个级别的层次结构和已编辑的数据。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-110">You displayed multiple levels of hierarchy and edited data in navigation properties.</span></span> <span data-ttu-id="0c0a6-111">在本教程中，您将通过添加和删除关系并添加与现有实体有关系的新实体来继续处理相关数据。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-111">In this tutorial you'll continue to work with related data by adding and deleting relationships and by adding a new entity that has a relationship to an existing entity.</span></span>

<span data-ttu-id="0c0a6-112">你将创建一个页面，用于添加分配给部门的课程。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-112">You'll create a page that adds courses that are assigned to departments.</span></span> <span data-ttu-id="0c0a6-113">这两个部门已经存在，当您创建一个新课程时，您将在其与现有部门之间建立关系。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-113">The departments already exist, and when you create a new course, at the same time you'll establish a relationship between it and an existing department.</span></span>

<span data-ttu-id="0c0a6-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span></span>

<span data-ttu-id="0c0a6-115">您还将创建一个使用多对多关系的页面，方法是将指导员分配给课程（在您选择的两个实体之间添加关系）或从课程中删除指导员（删除您的两个实体之间的关系select）。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-115">You'll also create a page that works with a many-to-many relationship by assigning an instructor to a course (adding a relationship between two entities that you select) or removing an instructor from a course (removing a relationship between two entities that you select).</span></span> <span data-ttu-id="0c0a6-116">在数据库中，添加讲师和课程之间的关系将导致新行添加到 `CourseInstructor` 关联表中;删除关系涉及到从 `CourseInstructor` 关联表中删除行。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-116">In the database, adding a relationship between an instructor and a course results in a new row being added to the `CourseInstructor` association table; removing a relationship involves deleting a row from the `CourseInstructor` association table.</span></span> <span data-ttu-id="0c0a6-117">不过，您可以在实体框架中通过设置导航属性来执行此操作，而无需显式引用 `CourseInstructor` 表。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-117">However, you do this in the Entity Framework by setting navigation properties, without referring to the `CourseInstructor` table explicitly.</span></span>

<span data-ttu-id="0c0a6-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span></span>

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a><span data-ttu-id="0c0a6-119">将具有关系的实体添加到现有实体</span><span class="sxs-lookup"><span data-stu-id="0c0a6-119">Adding an Entity with a Relationship to an Existing Entity</span></span>

<span data-ttu-id="0c0a6-120">创建一个使用 CoursesAdd*母版页的*名为的新网页，并将以下标记添加到名为 `Content2`的 `Content` 控件：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-120">Create a new web page named *CoursesAdd.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

<span data-ttu-id="0c0a6-121">此标记创建一个 `EntityDataSource` 控件，该控件可选择用于启用插入的课程，并为 `Inserting` 事件指定处理程序。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-121">This markup creates an `EntityDataSource` control that selects courses, that enables inserting, and that specifies a handler for the `Inserting` event.</span></span> <span data-ttu-id="0c0a6-122">创建新的 `Course` 实体时，将使用该处理程序更新 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-122">You'll use the handler to update the `Department` navigation property when a new `Course` entity is created.</span></span>

<span data-ttu-id="0c0a6-123">标记还会创建一个 `DetailsView` 控件以用于添加新的 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-123">The markup also creates a `DetailsView` control to use for adding new `Course` entities.</span></span> <span data-ttu-id="0c0a6-124">标记使用 `Course` 实体属性的绑定字段。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-124">The markup uses bound fields for `Course` entity properties.</span></span> <span data-ttu-id="0c0a6-125">需要输入 `CourseID` 值，因为这不是系统生成的 ID 字段。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-125">You have to enter the `CourseID` value because this is not a system-generated ID field.</span></span> <span data-ttu-id="0c0a6-126">相反，它是在创建课程时必须手动指定的课程编号。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-126">Instead, it's a course number that must be specified manually when the course is created.</span></span>

<span data-ttu-id="0c0a6-127">由于导航属性不能用于 `BoundField` 控件，因此可以对 `Department` 导航属性使用模板字段。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-127">You use a template field for the `Department` navigation property because navigation properties cannot be used with `BoundField` controls.</span></span> <span data-ttu-id="0c0a6-128">模板字段提供了一个下拉列表，用于选择部门。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-128">The template field provides a drop-down list to select the department.</span></span> <span data-ttu-id="0c0a6-129">下拉列表将通过使用 `Eval` （而不是 `Bind`）绑定到 `Departments` 实体集，因为你不能直接绑定导航属性来更新这些属性。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-129">The drop-down list is bound to the `Departments` entity set by using `Eval` rather than `Bind`, again because you cannot directly bind navigation properties in order to update them.</span></span> <span data-ttu-id="0c0a6-130">为 `DropDownList` 控件的 `Init` 事件指定处理程序，以便可以存储对控件的引用以供更新 `DepartmentID` 外键的代码使用。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-130">You specify a handler for the `DropDownList` control's `Init` event so that you can store a reference to the control for use by the code that updates the `DepartmentID` foreign key.</span></span>

<span data-ttu-id="0c0a6-131">在*CoursesAdd.aspx.cs*的分部类声明的后面，添加一个类字段以保存对 `DepartmentsDropDownList` 控件的引用：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-131">In *CoursesAdd.aspx.cs* just after the partial-class declaration, add a class field to hold a reference to the `DepartmentsDropDownList` control:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

<span data-ttu-id="0c0a6-132">为 `DepartmentsDropDownList` 控件的 `Init` 事件添加处理程序，以便可以存储对该控件的引用。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-132">Add a handler for the `DepartmentsDropDownList` control's `Init` event so that you can store a reference to the control.</span></span> <span data-ttu-id="0c0a6-133">这允许你获取用户输入的值，并使用它来更新 `Course` 实体的 `DepartmentID` 值。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-133">This lets you get the value the user has entered and use it to update the `DepartmentID` value of the `Course` entity.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

<span data-ttu-id="0c0a6-134">为 `DetailsView` 控件的 `Inserting` 事件添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-134">Add a handler for the `DetailsView` control's `Inserting` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

<span data-ttu-id="0c0a6-135">当用户单击 "`Insert`" 时，将在插入新记录前引发 `Inserting` 事件。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-135">When the user clicks `Insert`, the `Inserting` event is raised before the new record is inserted.</span></span> <span data-ttu-id="0c0a6-136">处理程序中的代码从 `DropDownList` 控件获取 `DepartmentID`，并使用它来设置将用于 `Course` 实体的 `DepartmentID` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-136">The code in the handler gets the `DepartmentID` from the `DropDownList` control and uses it to set the value that will be used for the `DepartmentID` property of the `Course` entity.</span></span>

<span data-ttu-id="0c0a6-137">实体框架将负责将此课程添加到关联 `Department` 实体的 `Courses` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-137">The Entity Framework will take care of adding this course to the `Courses` navigation property of the associated `Department` entity.</span></span> <span data-ttu-id="0c0a6-138">它还将部门添加到 `Course` 实体的 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-138">It also adds the department to the `Department` navigation property of the `Course` entity.</span></span>

<span data-ttu-id="0c0a6-139">运行页面。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-139">Run the page.</span></span>

<span data-ttu-id="0c0a6-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span></span>

<span data-ttu-id="0c0a6-141">输入 "ID"、"标题"、"信用数" 并选择一个部门，然后单击 "**插入**"。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-141">Enter an ID, a title, a number of credits, and select a department, then click **Insert**.</span></span>

<span data-ttu-id="0c0a6-142">运行 "球场 *" 页，* 然后选择同一部门查看新课程。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-142">Run the *Courses.aspx* page, and select the same department to see the new course.</span></span>

<span data-ttu-id="0c0a6-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span></span>

## <a name="working-with-many-to-many-relationships"></a><span data-ttu-id="0c0a6-144">使用多对多关系</span><span class="sxs-lookup"><span data-stu-id="0c0a6-144">Working with Many-to-Many Relationships</span></span>

<span data-ttu-id="0c0a6-145">`Courses` 实体集与 `People` 实体集之间的关系是多对多关系。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-145">The relationship between the `Courses` entity set and the `People` entity set is a many-to-many relationship.</span></span> <span data-ttu-id="0c0a6-146">`Course` 实体具有名为 `People` 的导航属性，该属性可包含零个、一个或多个相关 `Person` 实体（表示分配给讲授该课程的教师）。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-146">A `Course` entity has a navigation property named `People` that can contain zero, one, or more related `Person` entities (representing instructors assigned to teach that course).</span></span> <span data-ttu-id="0c0a6-147">`Person` 实体具有一个名为 `Courses` 的导航属性，该属性可包含零个、一个或多个相关 `Course` 实体（表示讲师分配给教授的课程）。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-147">And a `Person` entity has a navigation property named `Courses` that can contain zero, one, or more related `Course` entities (representing courses that instructor is assigned to teach).</span></span> <span data-ttu-id="0c0a6-148">一个讲师可以讲授多个课程，一个课程可能由多个讲师讲授。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-148">One instructor might teach multiple courses, and one course might be taught by multiple instructors.</span></span> <span data-ttu-id="0c0a6-149">在本演练的此部分中，你将通过更新相关实体的导航属性来添加和删除 `Person` 与 `Course` 实体之间的关系。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-149">In this section of the walkthrough, you'll add and remove relationships between `Person` and `Course` entities by updating the navigation properties of the related entities.</span></span>

<span data-ttu-id="0c0a6-150">创建一个使用 InstructorsCourses*母版页的*名为的新网页，并将以下标记添加到名为 `Content2`的 `Content` 控件：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-150">Create a new web page named *InstructorsCourses.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

<span data-ttu-id="0c0a6-151">此标记创建一个 `EntityDataSource` 控件，该控件检索教师 `Person` 实体的名称和 `PersonID`。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-151">This markup creates an `EntityDataSource` control that retrieves the name and `PersonID` of `Person` entities for instructors.</span></span> <span data-ttu-id="0c0a6-152">`DropDrownList` 控件绑定到 `EntityDataSource` 控件。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-152">A `DropDrownList` control is bound to the `EntityDataSource` control.</span></span> <span data-ttu-id="0c0a6-153">`DropDownList` 控件指定 `DataBound` 事件的处理程序。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-153">The `DropDownList` control specifies a handler for the `DataBound` event.</span></span> <span data-ttu-id="0c0a6-154">你将使用此处理程序来 databind 显示课程的两个下拉列表。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-154">You'll use this handler to databind the two drop-down lists that display courses.</span></span>

<span data-ttu-id="0c0a6-155">标记还会创建以下控件组，用于将课程分配给所选讲师：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-155">The markup also creates the following group of controls to use for assigning a course to the selected instructor:</span></span>

- <span data-ttu-id="0c0a6-156">用于选择要分配的课程的 `DropDownList` 控件。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-156">A `DropDownList` control for selecting a course to assign.</span></span> <span data-ttu-id="0c0a6-157">此控件将填充当前未分配给所选讲师的课程。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-157">This control will be populated with courses that are currently not assigned to the selected instructor.</span></span>
- <span data-ttu-id="0c0a6-158">用于启动赋值的 `Button` 控件。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-158">A `Button` control to initiate the assignment.</span></span>
- <span data-ttu-id="0c0a6-159">一个 `Label` 控件，在分配失败时显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-159">A `Label` control to display an error message if the assignment fails.</span></span>

<span data-ttu-id="0c0a6-160">最后，标记还会创建一组用于从所选指导员中删除课程的控件。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-160">Finally, the markup also creates a group of controls to use for removing a course from the selected instructor.</span></span>

<span data-ttu-id="0c0a6-161">在*InstructorsCourses.aspx.cs*中，添加 using 语句：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-161">In *InstructorsCourses.aspx.cs*, add a using statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

<span data-ttu-id="0c0a6-162">添加用于填充显示课程的两个下拉列表的方法：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-162">Add a method for populating the two drop-down lists that display courses:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

<span data-ttu-id="0c0a6-163">此代码将获取 `Courses` 实体集中的所有课程，并从所选讲师的 `Person` 实体的 `Courses` 导航属性获取课程。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-163">This code gets all courses from the `Courses` entity set and gets the courses from the `Courses` navigation property of the `Person` entity for the selected instructor.</span></span> <span data-ttu-id="0c0a6-164">然后，它确定分配给该讲师的课程，并相应地填充下拉列表。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-164">It then determines which courses are assigned to that instructor and populates the drop-down lists accordingly.</span></span>

<span data-ttu-id="0c0a6-165">为 "`Assign`" 按钮的 `Click` 事件添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-165">Add a handler for the `Assign` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

<span data-ttu-id="0c0a6-166">此代码获取选定讲师的 `Person` 实体，获取所选课程的 `Course` 实体，并将所选课程添加到讲师 `Person` 实体的 `Courses` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-166">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and adds the selected course to the `Courses` navigation property of the instructor's `Person` entity.</span></span> <span data-ttu-id="0c0a6-167">然后，它会将更改保存到数据库，并重新填充下拉列表，以便可以立即查看结果。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-167">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="0c0a6-168">为 "`Remove`" 按钮的 `Click` 事件添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-168">Add a handler for the `Remove` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

<span data-ttu-id="0c0a6-169">此代码获取选定讲师的 `Person` 实体，获取所选课程的 `Course` 实体，并从 `Person` 实体的 `Courses` 导航属性中删除所选课程。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-169">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and removes the selected course from the `Person` entity's `Courses` navigation property.</span></span> <span data-ttu-id="0c0a6-170">然后，它会将更改保存到数据库，并重新填充下拉列表，以便可以立即查看结果。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-170">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="0c0a6-171">将代码添加到 `Page_Load` 方法，以便在报告没有错误时不显示错误消息，并为讲师下拉列表的 `DataBound` 和 `SelectedIndexChanged` 事件添加处理程序，以填充课程下拉列表：</span><span class="sxs-lookup"><span data-stu-id="0c0a6-171">Add code to the `Page_Load` method that makes sure the error messages are not visible when there's no error to report, and add handlers for the `DataBound` and `SelectedIndexChanged` events of the instructors drop-down list to populate the courses drop-down lists:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

<span data-ttu-id="0c0a6-172">运行页面。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-172">Run the page.</span></span>

<span data-ttu-id="0c0a6-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span></span>

<span data-ttu-id="0c0a6-174">选择指导员。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-174">Select an instructor.</span></span> <span data-ttu-id="0c0a6-175">"<strong>分配课程</strong>" 下拉列表显示讲师未讲授的课程，"<strong>删除课程</strong>" 下拉列表显示教师已分配到的课程。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-175">The <strong>Assign a Course</strong> drop-down list displays the courses that the instructor doesn't teach, and the <strong>Remove a Course</strong> drop-down list displays the courses that the instructor is already assigned to.</span></span> <span data-ttu-id="0c0a6-176">在 "<strong>分配课程</strong>" 部分中，选择课程，然后单击 "<strong>分配</strong>"。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-176">In the <strong>Assign a Course</strong> section, select a course and then click <strong>Assign</strong>.</span></span> <span data-ttu-id="0c0a6-177">课程将移至 "<strong>删除课程</strong>" 下拉列表。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-177">The course moves to the <strong>Remove a Course</strong> drop-down list.</span></span> <span data-ttu-id="0c0a6-178">选择 "<strong>删除课程</strong>" 部分中的课程，并单击 "<strong>删除</strong>"<em>。</em></span><span class="sxs-lookup"><span data-stu-id="0c0a6-178">Select a course in the <strong>Remove a Course</strong> section and click <strong>Remove</strong><em>.</em></span></span> <span data-ttu-id="0c0a6-179">课程转到 "<strong>分配课程</strong>" 下拉列表。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-179">The course moves to the <strong>Assign a Course</strong> drop-down list.</span></span>

<span data-ttu-id="0c0a6-180">你现在已经了解了一些使用相关数据的方法。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-180">You have now seen some more ways to work with related data.</span></span> <span data-ttu-id="0c0a6-181">在以下教程中，你将了解如何在数据模型中使用继承来改善应用程序的可维护性。</span><span class="sxs-lookup"><span data-stu-id="0c0a6-181">In the following tutorial, you'll learn how to use inheritance in the data model to improve the maintainability of your application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0c0a6-182">[上一页](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="0c0a6-182">[Previous](the-entity-framework-and-aspnet-getting-started-part-4.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-6.md)</span></span>
