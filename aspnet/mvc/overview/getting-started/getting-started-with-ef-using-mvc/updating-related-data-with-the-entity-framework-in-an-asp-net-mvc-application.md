---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中使用 EF 更新相关数据
description: 在本教程中，你将更新相关数据。 对于大多数关系，可以通过更新外键字段或导航属性来完成此操作。
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499298"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="3b319-104">教程：在 ASP.NET MVC 应用中使用 EF 更新相关数据</span><span class="sxs-lookup"><span data-stu-id="3b319-104">Tutorial: Update related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="3b319-105">在上一教程中，您显示了相关数据。</span><span class="sxs-lookup"><span data-stu-id="3b319-105">In the previous tutorial you displayed related data.</span></span> <span data-ttu-id="3b319-106">在本教程中，你将更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="3b319-106">In this tutorial you'll update related data.</span></span> <span data-ttu-id="3b319-107">对于大多数关系，可以通过更新外键字段或导航属性来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="3b319-107">For most relationships, this can be done by updating either foreign key fields or navigation properties.</span></span> <span data-ttu-id="3b319-108">对于多对多关系，实体框架不会直接公开联接表，因此你可以在相应的导航属性中添加和删除实体。</span><span class="sxs-lookup"><span data-stu-id="3b319-108">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="3b319-109">下图是一些将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="3b319-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![讲师编辑课程](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="3b319-113">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="3b319-113">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b319-114">自定义课程页面</span><span class="sxs-lookup"><span data-stu-id="3b319-114">Customize courses pages</span></span>
> * <span data-ttu-id="3b319-115">将 office 添加到讲师页</span><span class="sxs-lookup"><span data-stu-id="3b319-115">Add office to instructors page</span></span>
> * <span data-ttu-id="3b319-116">向指导员页面添加课程</span><span class="sxs-lookup"><span data-stu-id="3b319-116">Add courses to instructors page</span></span>
> * <span data-ttu-id="3b319-117">更新 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="3b319-117">Update DeleteConfirmed</span></span>
> * <span data-ttu-id="3b319-118">向创建页添加办公室位置和课程</span><span class="sxs-lookup"><span data-stu-id="3b319-118">Add office location and courses to the Create page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b319-119">系统必备</span><span class="sxs-lookup"><span data-stu-id="3b319-119">Prerequisites</span></span>

* [<span data-ttu-id="3b319-120">读取相关数据</span><span class="sxs-lookup"><span data-stu-id="3b319-120">Reading Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a><span data-ttu-id="3b319-121">自定义课程页面</span><span class="sxs-lookup"><span data-stu-id="3b319-121">Customize courses pages</span></span>

<span data-ttu-id="3b319-122">创建新的课程实体时，新实体必须与现有院系有关系。</span><span class="sxs-lookup"><span data-stu-id="3b319-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="3b319-123">为此，基架代码需包括控制器方法、创建视图和编辑视图，且视图中应包括用于选择院系的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="3b319-123">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="3b319-124">下拉列表设置 `Course.DepartmentID` 外键属性，这就是用适当的 `Department` 实体加载 `Department` 导航属性所需的全部实体框架。</span><span class="sxs-lookup"><span data-stu-id="3b319-124">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="3b319-125">将用到基架代码，但需对其稍作更改，以便添加错误处理和对下拉列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="3b319-125">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="3b319-126">在*CourseController.cs*中，删除四个 `Create` 和 `Edit` 方法，并将其替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3b319-126">In *CourseController.cs*, delete the four `Create` and `Edit` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

<span data-ttu-id="3b319-127">将以下 `using` 语句添加到文件的开头：</span><span class="sxs-lookup"><span data-stu-id="3b319-127">Add the following `using` statement at the beginning of the file:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="3b319-128">`PopulateDepartmentsDropDownList` 方法获取按名称排序的所有部门的列表，为下拉列表创建一个 `SelectList` 集合，并将该集合传递到 `ViewBag` 属性中的视图。</span><span class="sxs-lookup"><span data-stu-id="3b319-128">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="3b319-129">该方法可以使用可选的 `selectedDepartment` 参数，而调用的代码可以通过该参数来指定呈现下拉列表时被选择的项。</span><span class="sxs-lookup"><span data-stu-id="3b319-129">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="3b319-130">视图会将名称 `DepartmentID` 传递给[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper，然后，帮助者知道在 `ViewBag` 对象中查找名为 `DepartmentID`的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="3b319-130">The view will pass the name `DepartmentID` to the [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="3b319-131">`HttpGet` `Create` 方法调用 `PopulateDepartmentsDropDownList` 方法，而不设置所选的项，因为对于新课程，该部门尚未建立：</span><span class="sxs-lookup"><span data-stu-id="3b319-131">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="3b319-132">`HttpGet` `Edit` 方法根据已分配给要编辑的课程的部门 ID 设置所选项目：</span><span class="sxs-lookup"><span data-stu-id="3b319-132">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

<span data-ttu-id="3b319-133">`Create` 和 `Edit` 的 `HttpPost` 方法还包括在发生错误后重新显示该页时设置选定项的代码：</span><span class="sxs-lookup"><span data-stu-id="3b319-133">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

<span data-ttu-id="3b319-134">此代码可确保在重新显示页面以显示错误消息时，选择的任何部门始终处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="3b319-134">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="3b319-135">课程视图已基架 "部门" 字段的下拉列表，但不需要此字段的 DepartmentID 标题，因此，对*Views\Course\Create.cshtml*文件进行以下突出显示的更改以更改标题。</span><span class="sxs-lookup"><span data-stu-id="3b319-135">The Course views are already scaffolded with drop-down lists for the department field, but you don't want the DepartmentID caption for this field, so make the following highlighted change to the *Views\Course\Create.cshtml* file to change the caption.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

<span data-ttu-id="3b319-136">在*Views\Course\Edit.cshtml*中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="3b319-136">Make the same change in *Views\Course\Edit.cshtml*.</span></span>

<span data-ttu-id="3b319-137">通常，scaffolder 不会基架主键，因为键值是由数据库生成的，不能更改，并且不是向用户显示的有意义的值。</span><span class="sxs-lookup"><span data-stu-id="3b319-137">Normally the scaffolder doesn't scaffold a primary key because the key value is generated by the database and can't be changed and isn't a meaningful value to be displayed to users.</span></span> <span data-ttu-id="3b319-138">对于课程实体，scaffolder 确实包括 `CourseID` 字段的文本框，因为它知道 `DatabaseGeneratedOption.None` 属性意味着用户应该能够输入主键值。</span><span class="sxs-lookup"><span data-stu-id="3b319-138">For Course entities the scaffolder does include an text box for the `CourseID` field because it understands that the `DatabaseGeneratedOption.None` attribute means the user should be able enter the primary key value.</span></span> <span data-ttu-id="3b319-139">但它并不了解这一点，因为数字对于您想要在其他视图中看到的是有意义的，因此您需要手动添加它。</span><span class="sxs-lookup"><span data-stu-id="3b319-139">But it doesn't understand that because the number is meaningful you want to see it in the other views, so you need to add it manually.</span></span>

<span data-ttu-id="3b319-140">在*Views\Course\Edit.cshtml*中，在 "**标题**" 字段之前添加课程编号字段。</span><span class="sxs-lookup"><span data-stu-id="3b319-140">In *Views\Course\Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="3b319-141">由于它是主键，因此将显示，但不能更改它。</span><span class="sxs-lookup"><span data-stu-id="3b319-141">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

<span data-ttu-id="3b319-142">在 "编辑" 视图中，课程编号已经有一个隐藏字段（`Html.HiddenFor` 帮助程序）。</span><span class="sxs-lookup"><span data-stu-id="3b319-142">There's already a hidden field (`Html.HiddenFor` helper) for the course number in the Edit view.</span></span> <span data-ttu-id="3b319-143">添加*html.labelfor*帮助程序不会消除隐藏字段的需要，因为当用户单击 "编辑" 页上的 "**保存**" 时，不会在已发布数据中包含课程编号。</span><span class="sxs-lookup"><span data-stu-id="3b319-143">Adding an *Html.LabelFor* helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the Edit page.</span></span>

<span data-ttu-id="3b319-144">在*Views\Course\Delete.cshtml*和*Views\Course\Details.cshtml*中，将部门名称标题从 "名称" 更改为 "部门"，然后在 "**标题**" 字段之前添加课程编号字段。</span><span class="sxs-lookup"><span data-stu-id="3b319-144">In *Views\Course\Delete.cshtml* and *Views\Course\Details.cshtml*, change the department name caption from "Name" to "Department" and add a course number field before the **Title** field.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

<span data-ttu-id="3b319-145">运行 "**创建**" 页（显示 "课程索引" 页，单击 "**新建**"），然后为新课程输入数据：</span><span class="sxs-lookup"><span data-stu-id="3b319-145">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

| <span data-ttu-id="3b319-146">“值”</span><span class="sxs-lookup"><span data-stu-id="3b319-146">Value</span></span> | <span data-ttu-id="3b319-147">设置</span><span class="sxs-lookup"><span data-stu-id="3b319-147">Setting</span></span> |
| ----- | ------- |
| <span data-ttu-id="3b319-148">数字</span><span class="sxs-lookup"><span data-stu-id="3b319-148">Number</span></span> | <span data-ttu-id="3b319-149">输入*1000*。</span><span class="sxs-lookup"><span data-stu-id="3b319-149">Enter *1000*.</span></span> |
| <span data-ttu-id="3b319-150">标题</span><span class="sxs-lookup"><span data-stu-id="3b319-150">Title</span></span> | <span data-ttu-id="3b319-151">输入*代数*。</span><span class="sxs-lookup"><span data-stu-id="3b319-151">Enter *Algebra*.</span></span> |
| <span data-ttu-id="3b319-152">学分</span><span class="sxs-lookup"><span data-stu-id="3b319-152">Credits</span></span> | <span data-ttu-id="3b319-153">输入*4*。</span><span class="sxs-lookup"><span data-stu-id="3b319-153">Enter *4*.</span></span> |
|<span data-ttu-id="3b319-154">Department</span><span class="sxs-lookup"><span data-stu-id="3b319-154">Department</span></span> | <span data-ttu-id="3b319-155">选择 "**数学**"。</span><span class="sxs-lookup"><span data-stu-id="3b319-155">Select **Mathematics**.</span></span> |

<span data-ttu-id="3b319-156">单击 **“创建”** 。</span><span class="sxs-lookup"><span data-stu-id="3b319-156">Click **Create**.</span></span> <span data-ttu-id="3b319-157">将显示 "课程索引" 页，新课程将添加到列表中。</span><span class="sxs-lookup"><span data-stu-id="3b319-157">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="3b319-158">索引页列表中的院系名称来自导航属性，表明已正确建立关系。</span><span class="sxs-lookup"><span data-stu-id="3b319-158">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="3b319-159">运行 "**编辑**" 页（显示 "课程索引" 页，然后单击 "**编辑**"）。</span><span class="sxs-lookup"><span data-stu-id="3b319-159">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

<span data-ttu-id="3b319-160">更改页面上的数据，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="3b319-160">Change data on the page and click **Save**.</span></span> <span data-ttu-id="3b319-161">将显示 "课程索引" 页和更新的课程数据。</span><span class="sxs-lookup"><span data-stu-id="3b319-161">The Course Index page is displayed with the updated course data.</span></span>

## <a name="add-office-to-instructors-page"></a><span data-ttu-id="3b319-162">将 office 添加到讲师页</span><span class="sxs-lookup"><span data-stu-id="3b319-162">Add office to instructors page</span></span>

<span data-ttu-id="3b319-163">编辑讲师记录时，有时希望能更新讲师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="3b319-163">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="3b319-164">`Instructor` 实体与 `OfficeAssignment` 实体之间存在一对零或一对多的关系，这意味着您必须处理以下情况：</span><span class="sxs-lookup"><span data-stu-id="3b319-164">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="3b319-165">如果用户清除办公室分配并且它最初具有值，则必须删除并删除 `OfficeAssignment` 实体。</span><span class="sxs-lookup"><span data-stu-id="3b319-165">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="3b319-166">如果用户输入 office 分配值并且它最初为空，则必须创建新的 `OfficeAssignment` 实体。</span><span class="sxs-lookup"><span data-stu-id="3b319-166">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="3b319-167">如果用户更改了 office 分配的值，则必须更改现有 `OfficeAssignment` 实体中的值。</span><span class="sxs-lookup"><span data-stu-id="3b319-167">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="3b319-168">打开*InstructorController.cs*并查看 `HttpGet` `Edit` 方法：</span><span class="sxs-lookup"><span data-stu-id="3b319-168">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="3b319-169">此处的基架代码不是你所需的代码。</span><span class="sxs-lookup"><span data-stu-id="3b319-169">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="3b319-170">它为下拉列表设置数据，但您需要的是文本框。</span><span class="sxs-lookup"><span data-stu-id="3b319-170">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="3b319-171">将此方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3b319-171">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

<span data-ttu-id="3b319-172">此代码删除 `ViewBag` 语句，并为关联的 `OfficeAssignment` 实体添加预先加载。</span><span class="sxs-lookup"><span data-stu-id="3b319-172">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="3b319-173">不能使用 `Find` 方法执行预先加载，因此使用 `Where` 和 `Single` 方法来选择讲师。</span><span class="sxs-lookup"><span data-stu-id="3b319-173">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="3b319-174">将 `HttpPost` `Edit` 方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3b319-174">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="3b319-175">处理 office 分配更新的：</span><span class="sxs-lookup"><span data-stu-id="3b319-175">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="3b319-176">对 `RetryLimitExceededException` 的引用需要 `using` 语句;若要添加它，请将鼠标悬停在 `RetryLimitExceededException`上。</span><span class="sxs-lookup"><span data-stu-id="3b319-176">The reference to `RetryLimitExceededException` requires a `using` statement; to add it - hover your mouse over `RetryLimitExceededException`.</span></span> <span data-ttu-id="3b319-177">将显示以下消息： "![ 重试异常消息](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3b319-177">The following message appears: ![ Retry exception message](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span></span>

<span data-ttu-id="3b319-178">选择 "**显示潜在修补程序**，然后**使用**"</span><span class="sxs-lookup"><span data-stu-id="3b319-178">Select **Show potential fixes**, then **using System.Data.Entity.Infrastructure**</span></span>

![解决重试异常](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="3b319-180">该代码执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3b319-180">The code does the following:</span></span>

- <span data-ttu-id="3b319-181">将方法名称更改为 `EditPost`，因为签名现在与 `HttpGet` 方法相同（`ActionName` 特性指定仍使用/Edit/URL）。</span><span class="sxs-lookup"><span data-stu-id="3b319-181">Changes the method name to `EditPost` because the signature is now the same as the `HttpGet` method (the `ActionName` attribute specifies that the /Edit/ URL is still used).</span></span>
- <span data-ttu-id="3b319-182">使用 `Instructor` 导航属性的预先加载从数据库获取当前的 `OfficeAssignment` 实体。</span><span class="sxs-lookup"><span data-stu-id="3b319-182">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="3b319-183">这与您在 `HttpGet` `Edit` 方法中所执行的操作相同。</span><span class="sxs-lookup"><span data-stu-id="3b319-183">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="3b319-184">用模型绑定器中的值更新检索到的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="3b319-184">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="3b319-185">使用的[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)重载使你能够将你要包括的属性*列入*允许列表。</span><span class="sxs-lookup"><span data-stu-id="3b319-185">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="3b319-186">这可以防止过度发布，如[第二个教程中所](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)述。</span><span class="sxs-lookup"><span data-stu-id="3b319-186">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- <span data-ttu-id="3b319-187">如果办公室位置为空，则将 `Instructor.OfficeAssignment` 属性设置为 null，以便删除 `OfficeAssignment` 表中的相关行。</span><span class="sxs-lookup"><span data-stu-id="3b319-187">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- <span data-ttu-id="3b319-188">将更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="3b319-188">Saves the changes to the database.</span></span>

<span data-ttu-id="3b319-189">在*Views\Instructor\Edit.cshtml*中，在 "**雇佣日期**" 字段的 `div` 元素之后，添加一个用于编辑办公室位置的新字段：</span><span class="sxs-lookup"><span data-stu-id="3b319-189">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

<span data-ttu-id="3b319-190">运行页面（选择 "**讲师**" 选项卡，然后单击 "在讲师上**编辑**"）。</span><span class="sxs-lookup"><span data-stu-id="3b319-190">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="3b319-191">更改“办公室位置”，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="3b319-191">Change the **Office Location** and click **Save**.</span></span>

## <a name="add-courses-to-instructors-page"></a><span data-ttu-id="3b319-192">向指导员页面添加课程</span><span class="sxs-lookup"><span data-stu-id="3b319-192">Add courses to instructors page</span></span>

<span data-ttu-id="3b319-193">讲师可能教授任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="3b319-193">Instructors may teach any number of courses.</span></span> <span data-ttu-id="3b319-194">现在，你将通过添加使用一组复选框来更改课程分配的功能，来增强讲师编辑页面。</span><span class="sxs-lookup"><span data-stu-id="3b319-194">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes.</span></span>

<span data-ttu-id="3b319-195">`Course` 和 `Instructor` 实体之间的关系是多对多，这意味着您不能直接访问联接表中的外键属性。</span><span class="sxs-lookup"><span data-stu-id="3b319-195">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the foreign key properties which are in the join table.</span></span> <span data-ttu-id="3b319-196">相反，您可以在 `Instructor.Courses` 导航属性中添加和移除实体。</span><span class="sxs-lookup"><span data-stu-id="3b319-196">Instead, you add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="3b319-197">用于更改讲师所对应的课程的 UI 是一组复选框。</span><span class="sxs-lookup"><span data-stu-id="3b319-197">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="3b319-198">该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。</span><span class="sxs-lookup"><span data-stu-id="3b319-198">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="3b319-199">用户可以通过选择或清除复选框来更改课程分配。</span><span class="sxs-lookup"><span data-stu-id="3b319-199">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="3b319-200">如果课程数量很大，您可能想要使用不同的方法来显示视图中的数据，但您可以使用相同的方法来处理导航属性，以便创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="3b319-200">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="3b319-201">若要为复选框列表的视图提供数据，将使用视图模型类。</span><span class="sxs-lookup"><span data-stu-id="3b319-201">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="3b319-202">在*viewmodel*文件夹中创建*AssignedCourseData.cs* ，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3b319-202">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="3b319-203">在*InstructorController.cs*中，将 `HttpGet` `Edit` 方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3b319-203">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="3b319-204">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="3b319-204">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

<span data-ttu-id="3b319-205">该代码为 `Courses` 导航属性添加了预先加载，并调用新的 `PopulateAssignedCourseData` 方法使用 `AssignedCourseData` 视图模型类为复选框数组提供信息。</span><span class="sxs-lookup"><span data-stu-id="3b319-205">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="3b319-206">`PopulateAssignedCourseData` 方法中的代码读取所有 `Course` 实体，以便使用视图模型类加载课程列表。</span><span class="sxs-lookup"><span data-stu-id="3b319-206">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="3b319-207">对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。</span><span class="sxs-lookup"><span data-stu-id="3b319-207">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="3b319-208">若要在检查是否将课程分配给讲师时创建高效的查找，则分配给讲师的课程将被放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合。</span><span class="sxs-lookup"><span data-stu-id="3b319-208">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="3b319-209">对于指定讲师的课程，`Assigned` 属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="3b319-209">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="3b319-210">视图将使用此属性来确定应将哪些复选框显示为选中状态。</span><span class="sxs-lookup"><span data-stu-id="3b319-210">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="3b319-211">最后，将列表传递到 `ViewBag` 属性中的视图。</span><span class="sxs-lookup"><span data-stu-id="3b319-211">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="3b319-212">接下来，添加用户单击“保存”时执行的代码。</span><span class="sxs-lookup"><span data-stu-id="3b319-212">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="3b319-213">将 `EditPost` 方法替换为以下代码，该代码调用更新 `Instructor` 实体的 `Courses` 导航属性的新方法。</span><span class="sxs-lookup"><span data-stu-id="3b319-213">Replace the `EditPost` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="3b319-214">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="3b319-214">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

<span data-ttu-id="3b319-215">方法签名与 `HttpGet` `Edit` 方法不同，因此方法名称从 `EditPost` 返回到 `Edit`。</span><span class="sxs-lookup"><span data-stu-id="3b319-215">The method signature is now different from the `HttpGet` `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="3b319-216">因为视图没有 `Course` 实体的集合，模型绑定器无法自动更新 `Courses` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="3b319-216">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="3b319-217">你将在新的 `UpdateInstructorCourses` 方法中执行该操作，而不是使用模型联编程序来更新 `Courses` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="3b319-217">Instead of using the model binder to update the `Courses` navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="3b319-218">为此，需要从模型绑定中排除 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="3b319-218">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="3b319-219">这不需要对调用[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)的代码进行任何更改，因为你使用的是*允许列表*重载，而 `Courses` 不在包含列表中。</span><span class="sxs-lookup"><span data-stu-id="3b319-219">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="3b319-220">如果未选择任何复选框，`UpdateInstructorCourses` 中的代码将使用空集合初始化 `Courses` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="3b319-220">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="3b319-221">之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。</span><span class="sxs-lookup"><span data-stu-id="3b319-221">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="3b319-222">为便于高效查找，后两个集合存储在 `HashSet` 对象中。</span><span class="sxs-lookup"><span data-stu-id="3b319-222">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="3b319-223">如果某课程的复选框处于选中状态，但该课程不在 `Instructor.Courses` 导航属性中，则会将该课程添加到导航属性中的集合中。</span><span class="sxs-lookup"><span data-stu-id="3b319-223">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="3b319-224">如果某课程的复选框未处于选中状态，但该课程存在 `Instructor.Courses` 导航属性中，则会从导航属性中删除该课程。</span><span class="sxs-lookup"><span data-stu-id="3b319-224">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="3b319-225">在*Views\Instructor\Edit.cshtml*中，通过将以下代码添加到 "`OfficeAssignment`" 字段的 `div` 元素之后，在 "**保存**" 按钮的 `div` 元素之前添加以下代码，添加一个包含复选框数组的 "**课程**" 字段：</span><span class="sxs-lookup"><span data-stu-id="3b319-225">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the `OfficeAssignment` field and before the `div` element for the **Save** button:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

<span data-ttu-id="3b319-226">在粘贴代码后，如果分行符和缩进在此处看起来不像，请手动修复所有内容，使其看起来就像你在此处看到的内容。</span><span class="sxs-lookup"><span data-stu-id="3b319-226">After you paste the code, if line breaks and indentation don't look like they do here, manually fix everything so that it looks like what you see here.</span></span> <span data-ttu-id="3b319-227">缩进不一定要完美，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@</tr>` 行必须各成一行（如下所示），否则会出现运行时错误。</span><span class="sxs-lookup"><span data-stu-id="3b319-227">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span>

<span data-ttu-id="3b319-228">此代码将创建一个具有三列的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="3b319-228">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="3b319-229">每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。</span><span class="sxs-lookup"><span data-stu-id="3b319-229">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="3b319-230">所有复选框都具有相同的名称（"selectedCourses"），这会通知模型绑定器将这些复选框视为组。</span><span class="sxs-lookup"><span data-stu-id="3b319-230">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="3b319-231">每个复选框的 `value` 属性都设置为页面发布时 `CourseID.` 的值，模型联编程序将一个数组传递到控制器，该控制器仅包含所选复选框的 `CourseID` 值。</span><span class="sxs-lookup"><span data-stu-id="3b319-231">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="3b319-232">最初呈现复选框时，分配给讲师的课程的这些复选框具有 `checked` 属性，这些属性将选择这些复选框（将其显示为选中状态）。</span><span class="sxs-lookup"><span data-stu-id="3b319-232">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="3b319-233">更改课程分配后，你需要能够在站点返回 `Index` 页面时验证所做的更改。</span><span class="sxs-lookup"><span data-stu-id="3b319-233">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="3b319-234">因此，您需要在该页面的表中添加一列。</span><span class="sxs-lookup"><span data-stu-id="3b319-234">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="3b319-235">在这种情况下，您无需使用 `ViewBag` 对象，因为您要显示的信息已位于作为模型传递到页面的 `Instructor` 实体的 `Courses` 导航属性中。</span><span class="sxs-lookup"><span data-stu-id="3b319-235">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="3b319-236">在*Views\Instructor\Index.cshtml*中，在 " **Office** " 标题后面添加一个**课程**标题，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="3b319-236">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

<span data-ttu-id="3b319-237">然后，在 "办公室位置详细信息" 单元之后立即添加一个新的详细信息单元：</span><span class="sxs-lookup"><span data-stu-id="3b319-237">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

<span data-ttu-id="3b319-238">运行 "**讲师索引**" 页，查看分配给每个指导员的课程。</span><span class="sxs-lookup"><span data-stu-id="3b319-238">Run the **Instructor Index** page to see the courses assigned to each instructor.</span></span>

<span data-ttu-id="3b319-239">单击指导员上的 "**编辑**" 以查看 "编辑" 页。</span><span class="sxs-lookup"><span data-stu-id="3b319-239">Click **Edit** on an instructor to see the Edit page.</span></span>

<span data-ttu-id="3b319-240">更改某些课程分配，并单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="3b319-240">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="3b319-241">所作更改将反映在索引页上。</span><span class="sxs-lookup"><span data-stu-id="3b319-241">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="3b319-242">注意：如果有有限数量的课程，此处用于编辑讲师课程数据的方法很有用。</span><span class="sxs-lookup"><span data-stu-id="3b319-242">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="3b319-243">若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="3b319-243">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-deleteconfirmed"></a><span data-ttu-id="3b319-244">更新 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="3b319-244">Update DeleteConfirmed</span></span>

<span data-ttu-id="3b319-245">在*InstructorController.cs*中，删除 `DeleteConfirmed` 方法并在其位置插入以下代码。</span><span class="sxs-lookup"><span data-stu-id="3b319-245">In *InstructorController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

<span data-ttu-id="3b319-246">此代码进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="3b319-246">This code makes the following change:</span></span>

- <span data-ttu-id="3b319-247">如果将指导员指定为任何部门的管理员，则将从该部门中删除讲师分配。</span><span class="sxs-lookup"><span data-stu-id="3b319-247">If the instructor is assigned as administrator of any department, removes the instructor assignment from that department.</span></span> <span data-ttu-id="3b319-248">如果不使用此代码，如果您尝试删除已分配为部门管理员的指导员，会出现引用完整性错误。</span><span class="sxs-lookup"><span data-stu-id="3b319-248">Without this code, you would get a referential integrity error if you tried to delete an instructor who was assigned as administrator for a department.</span></span>

<span data-ttu-id="3b319-249">此代码不会处理一个以管理员身份分配给多个部门的指导员方案。</span><span class="sxs-lookup"><span data-stu-id="3b319-249">This code doesn't handle the scenario of one instructor assigned as administrator for multiple departments.</span></span> <span data-ttu-id="3b319-250">在上一教程中，您将添加代码以防止发生该方案。</span><span class="sxs-lookup"><span data-stu-id="3b319-250">In the last tutorial you'll add code that prevents that scenario from happening.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="3b319-251">向创建页添加办公室位置和课程</span><span class="sxs-lookup"><span data-stu-id="3b319-251">Add office location and courses to the Create page</span></span>

<span data-ttu-id="3b319-252">在*InstructorController.cs*中，删除 `HttpGet` 并 `HttpPost` `Create` 方法，然后在其位置添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="3b319-252">In *InstructorController.cs*, delete the `HttpGet` and `HttpPost` `Create` methods, and then add the following code in their place:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="3b319-253">此代码类似于您在编辑方法中看到的内容，但最初并未选择任何课程。</span><span class="sxs-lookup"><span data-stu-id="3b319-253">This code is similar to what you saw for the Edit methods except that initially no courses are selected.</span></span> <span data-ttu-id="3b319-254">`HttpGet` `Create` 方法调用 `PopulateAssignedCourseData` 方法，这并不是因为可能选择了课程，但为了为视图中的 `foreach` 循环提供空集合（否则，视图代码将引发空引用异常）。</span><span class="sxs-lookup"><span data-stu-id="3b319-254">The `HttpGet` `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="3b319-255">在用于检查验证错误并将新的指导员添加到数据库的模板代码之前，HttpPost Create 方法会将每个选定的课程添加到课程导航属性。</span><span class="sxs-lookup"><span data-stu-id="3b319-255">The HttpPost Create method adds each selected course to the Courses navigation property before the template code that checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="3b319-256">即使存在模型错误，也会添加课程，以便在出现模型错误时（例如，用户输入无效日期），以便在使用错误消息重新显示页面时，所做的任何课程选择都将自动还原。</span><span class="sxs-lookup"><span data-stu-id="3b319-256">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date) so that when the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="3b319-257">请注意，为了能够向 `Courses` 导航属性添加课程，必须将该属性初始化为空集合：</span><span class="sxs-lookup"><span data-stu-id="3b319-257">Notice that in order to be able to add courses to the `Courses` navigation property you have to initialize the property as an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="3b319-258">除了在控制器代码中进行此操作之外，还可以在“导师”模型中进行此操作，方法是将该属性更改为不存在集合时自动创建集合，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="3b319-258">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="3b319-259">如果通过这种方式修改 `Courses` 属性，则可以删除控制器中的显式属性初始化代码。</span><span class="sxs-lookup"><span data-stu-id="3b319-259">If you modify the `Courses` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="3b319-260">在*Views\Instructor\Create.cshtml*中，在 "雇佣日期" 字段之后、"**提交**" 按钮之前添加 "办公室位置" 文本框和课程复选框。</span><span class="sxs-lookup"><span data-stu-id="3b319-260">In *Views\Instructor\Create.cshtml*, add an office location text box and course check boxes after the hire date field and before the **Submit** button.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

<span data-ttu-id="3b319-261">在粘贴代码后，请按照之前对 "编辑" 页的操作修复分行符和缩进。</span><span class="sxs-lookup"><span data-stu-id="3b319-261">After you paste the code, fix line breaks and indentation as you did earlier for the Edit page.</span></span>

<span data-ttu-id="3b319-262">运行 "创建" 页并添加一个指导员。</span><span class="sxs-lookup"><span data-stu-id="3b319-262">Run the Create page and add an instructor.</span></span>

<a id="transactions"></a>

## <a name="handling-transactions"></a><span data-ttu-id="3b319-263">处理翻译</span><span class="sxs-lookup"><span data-stu-id="3b319-263">Handling transactions</span></span>

<span data-ttu-id="3b319-264">如[基本 CRUD 功能教程](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)中所述，默认情况下实体框架隐式实现事务。</span><span class="sxs-lookup"><span data-stu-id="3b319-264">As explained in the [Basic CRUD Functionality tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), by default the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="3b319-265">对于需要更多控制的情况下（例如，如果想要包括在事务中的实体框架之外完成的操作），请参阅 MSDN 上的[使用事务](https://msdn.microsoft.com/data/dn456843)。</span><span class="sxs-lookup"><span data-stu-id="3b319-265">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Working with Transactions](https://msdn.microsoft.com/data/dn456843) on MSDN.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="3b319-266">获取代码</span><span class="sxs-lookup"><span data-stu-id="3b319-266">Get the code</span></span>

[<span data-ttu-id="3b319-267">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="3b319-267">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="3b319-268">其他资源</span><span class="sxs-lookup"><span data-stu-id="3b319-268">Additional resources</span></span>

<span data-ttu-id="3b319-269">可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="3b319-269">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="3b319-270">下一步</span><span class="sxs-lookup"><span data-stu-id="3b319-270">Next step</span></span>

<span data-ttu-id="3b319-271">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="3b319-271">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b319-272">自定义课程页面</span><span class="sxs-lookup"><span data-stu-id="3b319-272">Customized courses pages</span></span>
> * <span data-ttu-id="3b319-273">已将 office 添加到讲师页</span><span class="sxs-lookup"><span data-stu-id="3b319-273">Added office to instructors page</span></span>
> * <span data-ttu-id="3b319-274">向讲师页添加了课程</span><span class="sxs-lookup"><span data-stu-id="3b319-274">Added courses to instructors page</span></span>
> * <span data-ttu-id="3b319-275">已更新 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="3b319-275">Updated DeleteConfirmed</span></span>
> * <span data-ttu-id="3b319-276">在 "创建" 页中添加了办公位置和课程</span><span class="sxs-lookup"><span data-stu-id="3b319-276">Added office location and courses to the Create page</span></span>

<span data-ttu-id="3b319-277">转到下一篇文章，了解如何实现异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="3b319-277">Advance to the next article to learn how to implement an asynchronous programming model.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3b319-278">异步编程模型</span><span class="sxs-lookup"><span data-stu-id="3b319-278">Asynchronous programming model</span></span>](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
