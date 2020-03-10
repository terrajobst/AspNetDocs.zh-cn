---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 使用实体框架4.0 和 ObjectDataSource 控件，第3部分：排序和筛选 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512714"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="14207-104">使用实体框架4.0 和 ObjectDataSource 控件，第3部分：排序和筛选</span><span class="sxs-lookup"><span data-stu-id="14207-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="14207-105">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="14207-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="14207-106">本教程系列在[使用实体框架 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。</span><span class="sxs-lookup"><span data-stu-id="14207-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="14207-107">如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。</span><span class="sxs-lookup"><span data-stu-id="14207-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="14207-108">你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。</span><span class="sxs-lookup"><span data-stu-id="14207-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="14207-109">如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="14207-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="14207-110">在上一教程中，你已在使用实体框架和 `ObjectDataSource` 控件的 n 层 web 应用程序中实现了存储库模式。</span><span class="sxs-lookup"><span data-stu-id="14207-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="14207-111">本教程介绍如何进行排序和筛选，以及如何处理主/从方案。</span><span class="sxs-lookup"><span data-stu-id="14207-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="14207-112">你将在 "*部门*" 页中添加以下增强功能：</span><span class="sxs-lookup"><span data-stu-id="14207-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="14207-113">允许用户按名称选择部门的文本框。</span><span class="sxs-lookup"><span data-stu-id="14207-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="14207-114">网格中显示的每个部门的课程列表。</span><span class="sxs-lookup"><span data-stu-id="14207-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="14207-115">通过单击列标题进行排序的功能。</span><span class="sxs-lookup"><span data-stu-id="14207-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="14207-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="14207-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="14207-117">添加对 GridView 列排序的功能</span><span class="sxs-lookup"><span data-stu-id="14207-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="14207-118">打开 " *default.aspx* " 页，并将 `SortParameterName="sortExpression"` 特性添加到名为 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控件。</span><span class="sxs-lookup"><span data-stu-id="14207-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="14207-119">（稍后，你将创建一个 `GetDepartments` 方法，该方法采用名为 `sortExpression`的参数。）控件开始标记的标记现在类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="14207-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="14207-120">将 `AllowSorting="true"` 特性添加到 `GridView` 控件的开始标记中。</span><span class="sxs-lookup"><span data-stu-id="14207-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="14207-121">控件开始标记的标记现在类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="14207-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="14207-122">在*Departments.aspx.cs*中，通过从 `Page_Load` 方法调用 `GridView` 控件的 `Sort` 方法来设置默认排序顺序：</span><span class="sxs-lookup"><span data-stu-id="14207-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="14207-123">可以在业务逻辑类或存储库类中添加排序或筛选的代码。</span><span class="sxs-lookup"><span data-stu-id="14207-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="14207-124">如果在业务逻辑类中执行此操作，则会在从数据库中检索数据后执行排序或筛选工作，因为业务逻辑类使用存储库返回的 `IEnumerable` 对象。</span><span class="sxs-lookup"><span data-stu-id="14207-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="14207-125">如果在存储库类中添加排序和筛选代码，并在将 LINQ 表达式或对象查询转换为 `IEnumerable` 对象之前执行此操作，则会将命令传递到数据库进行处理，这通常更有效。</span><span class="sxs-lookup"><span data-stu-id="14207-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="14207-126">在本教程中，您将以一种使处理由数据库（即存储在存储库中）完成的方式进行排序和筛选。</span><span class="sxs-lookup"><span data-stu-id="14207-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="14207-127">若要添加排序功能，必须将新方法添加到存储库接口和存储库类以及业务逻辑类中。</span><span class="sxs-lookup"><span data-stu-id="14207-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="14207-128">在*ISchoolRepository.cs*文件中，添加一个新的 `GetDepartments` 方法，该方法采用将用于对返回的部门列表进行排序的 `sortExpression` 参数：</span><span class="sxs-lookup"><span data-stu-id="14207-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="14207-129">`sortExpression` 参数将指定要排序的列以及排序方向。</span><span class="sxs-lookup"><span data-stu-id="14207-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="14207-130">将新方法的代码添加到*SchoolRepository.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="14207-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="14207-131">更改现有的无参数 `GetDepartments` 方法以调用新方法：</span><span class="sxs-lookup"><span data-stu-id="14207-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="14207-132">在测试项目中，将以下新方法添加到*MockSchoolRepository.cs*：</span><span class="sxs-lookup"><span data-stu-id="14207-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="14207-133">如果要创建依赖于此方法的任何单元测试返回已排序的列表，则需要在返回列表之前对其进行排序。</span><span class="sxs-lookup"><span data-stu-id="14207-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="14207-134">在本教程中，您将不会创建像这样的测试，因此该方法只返回未排序的部门列表。</span><span class="sxs-lookup"><span data-stu-id="14207-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="14207-135">在*SchoolBL.cs*文件中，将以下新方法添加到业务逻辑类：</span><span class="sxs-lookup"><span data-stu-id="14207-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="14207-136">此代码将排序参数传递给存储库方法。</span><span class="sxs-lookup"><span data-stu-id="14207-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="14207-137">运行 " *node.js" 页。*</span><span class="sxs-lookup"><span data-stu-id="14207-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="14207-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="14207-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="14207-139">你现在可以单击任何列标题以按该列进行排序。</span><span class="sxs-lookup"><span data-stu-id="14207-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="14207-140">如果已对列进行排序，则单击标题会反转排序方向。</span><span class="sxs-lookup"><span data-stu-id="14207-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="14207-141">添加搜索框</span><span class="sxs-lookup"><span data-stu-id="14207-141">Adding a Search Box</span></span>

<span data-ttu-id="14207-142">在本节中，您将添加一个 "搜索" 文本框，使用控制参数将其链接到 `ObjectDataSource` 控件，并将方法添加到业务逻辑类以支持筛选。</span><span class="sxs-lookup"><span data-stu-id="14207-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="14207-143">打开 " *default.aspx* " 页，并在标题和第一个 `ObjectDataSource` 控件之间添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="14207-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="14207-144">在名为 `DepartmentsObjectDataSource`的 `ObjectDataSource` 控件中，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="14207-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="14207-145">添加一个名为 `nameSearchString` 的参数的 `SelectParameters` 元素，该参数获取 `SearchTextBox` 控件中输入的值。</span><span class="sxs-lookup"><span data-stu-id="14207-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="14207-146">将 `SelectMethod` 特性值更改为 `GetDepartmentsByName`。</span><span class="sxs-lookup"><span data-stu-id="14207-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="14207-147">（稍后将创建此方法。）</span><span class="sxs-lookup"><span data-stu-id="14207-147">(You'll create this method later.)</span></span>

<span data-ttu-id="14207-148">`ObjectDataSource` 控件的标记现在类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="14207-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="14207-149">在*ISchoolRepository.cs*中，添加一个 `GetDepartmentsByName` 方法，该方法采用 `sortExpression` 和 `nameSearchString` 参数：</span><span class="sxs-lookup"><span data-stu-id="14207-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="14207-150">在*SchoolRepository.cs*中，添加以下新方法：</span><span class="sxs-lookup"><span data-stu-id="14207-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="14207-151">此代码使用 `Where` 方法来选择包含搜索字符串的项。</span><span class="sxs-lookup"><span data-stu-id="14207-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="14207-152">如果搜索字符串为空，则将选择所有记录。</span><span class="sxs-lookup"><span data-stu-id="14207-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="14207-153">请注意，当你将方法调用一起指定到此类语句（`Include`，然后 `OrderBy`，然后 `Where`）中时，`Where` 方法必须始终是最后一个。</span><span class="sxs-lookup"><span data-stu-id="14207-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="14207-154">更改采用 `sortExpression` 参数的现有 `GetDepartments` 方法，以调用新方法：</span><span class="sxs-lookup"><span data-stu-id="14207-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="14207-155">在测试项目的*MockSchoolRepository.cs*中，添加以下新方法：</span><span class="sxs-lookup"><span data-stu-id="14207-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="14207-156">在*SchoolBL.cs*中，添加以下新方法：</span><span class="sxs-lookup"><span data-stu-id="14207-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="14207-157">运行 " *node.js* " 页并输入搜索字符串以确保选择逻辑正常工作。</span><span class="sxs-lookup"><span data-stu-id="14207-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="14207-158">将文本框留空，然后尝试搜索，确保返回所有记录。</span><span class="sxs-lookup"><span data-stu-id="14207-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="14207-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="14207-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="14207-160">为每个网格行添加详细信息列</span><span class="sxs-lookup"><span data-stu-id="14207-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="14207-161">接下来，您需要查看在网格右侧单元格中显示的每个部门的所有课程。</span><span class="sxs-lookup"><span data-stu-id="14207-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="14207-162">为此，你将使用嵌套 `GridView` 控件，并将其数据绑定到 `Department` 实体的 `Courses` 导航属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="14207-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="14207-163">在 `GridView` 控件的标记*中打开 node.js* ，并为 `RowDataBound` 事件指定处理程序。</span><span class="sxs-lookup"><span data-stu-id="14207-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="14207-164">控件开始标记的标记现在类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="14207-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="14207-165">在 `Administrator` 模板字段后添加新的 `TemplateField` 元素：</span><span class="sxs-lookup"><span data-stu-id="14207-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="14207-166">此标记创建一个嵌套的 `GridView` 控件，该控件显示课程列表的编号和标题。</span><span class="sxs-lookup"><span data-stu-id="14207-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="14207-167">它不指定数据源，因为您将在 `RowDataBound` 处理程序中的代码中进行数据绑定。</span><span class="sxs-lookup"><span data-stu-id="14207-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="14207-168">打开*Departments.aspx.cs*并为 `RowDataBound` 事件添加以下处理程序：</span><span class="sxs-lookup"><span data-stu-id="14207-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="14207-169">此代码从事件参数中获取 `Department` 实体，将 `Courses` 导航属性转换为 `List` 集合，并将嵌套的 `GridView` databinds 到集合中。</span><span class="sxs-lookup"><span data-stu-id="14207-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="14207-170">通过在 `GetDepartmentsByName` 方法中创建的对象查询中调用 `Include` 方法，打开*SchoolRepository.cs*文件并指定预先加载 `Courses` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="14207-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="14207-171">`GetDepartmentsByName` 方法中的 `return` 语句现在类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="14207-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="14207-172">运行页面。</span><span class="sxs-lookup"><span data-stu-id="14207-172">Run the page.</span></span> <span data-ttu-id="14207-173">除了前面添加的排序和筛选功能，GridView 控件现在还显示每个部门的嵌套课程详细信息。</span><span class="sxs-lookup"><span data-stu-id="14207-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="14207-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="14207-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="14207-175">这将完成对排序、筛选和主/详细方案的介绍。</span><span class="sxs-lookup"><span data-stu-id="14207-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="14207-176">在下一教程中，你将了解如何处理并发。</span><span class="sxs-lookup"><span data-stu-id="14207-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="14207-177">[上一页](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="14207-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
