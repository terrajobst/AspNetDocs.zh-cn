---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 在模型绑定和 web 窗体中对数据进行排序、分页和筛选 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441062"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="44513-104">通过模型绑定和 web 窗体对数据进行排序、分页和筛选</span><span class="sxs-lookup"><span data-stu-id="44513-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="44513-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="44513-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="44513-106">本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="44513-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="44513-107">与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。</span><span class="sxs-lookup"><span data-stu-id="44513-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="44513-108">此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="44513-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="44513-109">本教程介绍如何通过模型绑定来添加数据的排序、分页和筛选。</span><span class="sxs-lookup"><span data-stu-id="44513-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="44513-110">本教程基于在序列的第[一部分](retrieving-data.md)中创建的项目构建。</span><span class="sxs-lookup"><span data-stu-id="44513-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="44513-111">可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。</span><span class="sxs-lookup"><span data-stu-id="44513-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="44513-112">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="44513-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="44513-113">它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。</span><span class="sxs-lookup"><span data-stu-id="44513-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="44513-114">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="44513-114">What you'll build</span></span>

<span data-ttu-id="44513-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="44513-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="44513-116">启用数据的排序和分页</span><span class="sxs-lookup"><span data-stu-id="44513-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="44513-117">启用基于用户所选内容的数据筛选</span><span class="sxs-lookup"><span data-stu-id="44513-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="44513-118">添加排序</span><span class="sxs-lookup"><span data-stu-id="44513-118">Add sorting</span></span>

<span data-ttu-id="44513-119">在 GridView 中启用排序非常简单。</span><span class="sxs-lookup"><span data-stu-id="44513-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="44513-120">在 Student 文件中，只需在 GridView 中将**AllowSorting**设置为**true**即可。</span><span class="sxs-lookup"><span data-stu-id="44513-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="44513-121">不需要为每个列设置**SortExpression**值，因为 DataField 会自动使用。</span><span class="sxs-lookup"><span data-stu-id="44513-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="44513-122">GridView 修改查询以包括按选定值对数据进行排序。</span><span class="sxs-lookup"><span data-stu-id="44513-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="44513-123">以下突出显示的代码显示了为启用排序需要进行的添加。</span><span class="sxs-lookup"><span data-stu-id="44513-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="44513-124">运行 web 应用程序，并按不同列中的值测试学生记录排序。</span><span class="sxs-lookup"><span data-stu-id="44513-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![对学生进行排序](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="44513-126">添加分页</span><span class="sxs-lookup"><span data-stu-id="44513-126">Add paging</span></span>

<span data-ttu-id="44513-127">启用分页也非常简单。</span><span class="sxs-lookup"><span data-stu-id="44513-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="44513-128">在 GridView 中，将**AllowPaging**属性设置为**true** ，并将**PageSize**属性设置为要在每页上显示的记录数。</span><span class="sxs-lookup"><span data-stu-id="44513-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="44513-129">在本教程中，可以将其设置为4。</span><span class="sxs-lookup"><span data-stu-id="44513-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="44513-130">运行 web 应用程序，请注意，现在将记录分成多个页面，而在单个页面上只显示4条记录。</span><span class="sxs-lookup"><span data-stu-id="44513-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![添加分页](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="44513-132">延迟的查询执行会提高应用程序的效率。</span><span class="sxs-lookup"><span data-stu-id="44513-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="44513-133">GridView 会修改查询以仅检索当前页的记录，而不是检索整个数据集。</span><span class="sxs-lookup"><span data-stu-id="44513-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="44513-134">按用户选择筛选记录</span><span class="sxs-lookup"><span data-stu-id="44513-134">Filter records by user selection</span></span>

<span data-ttu-id="44513-135">模型绑定添加了多个属性，使您可以指定如何在模型绑定方法中设置参数的值。</span><span class="sxs-lookup"><span data-stu-id="44513-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="44513-136">这些属性位于**ModelBinding**命名空间中。</span><span class="sxs-lookup"><span data-stu-id="44513-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="44513-137">这些权限包括：</span><span class="sxs-lookup"><span data-stu-id="44513-137">They include:</span></span>

- <span data-ttu-id="44513-138">控件</span><span class="sxs-lookup"><span data-stu-id="44513-138">Control</span></span>
- <span data-ttu-id="44513-139">Cookie</span><span class="sxs-lookup"><span data-stu-id="44513-139">Cookie</span></span>
- <span data-ttu-id="44513-140">窗体</span><span class="sxs-lookup"><span data-stu-id="44513-140">Form</span></span>
- <span data-ttu-id="44513-141">配置文件</span><span class="sxs-lookup"><span data-stu-id="44513-141">Profile</span></span>
- <span data-ttu-id="44513-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="44513-142">QueryString</span></span>
- <span data-ttu-id="44513-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="44513-143">RouteData</span></span>
- <span data-ttu-id="44513-144">会话</span><span class="sxs-lookup"><span data-stu-id="44513-144">Session</span></span>
- <span data-ttu-id="44513-145">UserProfile</span><span class="sxs-lookup"><span data-stu-id="44513-145">UserProfile</span></span>
- <span data-ttu-id="44513-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="44513-146">ViewState</span></span>

<span data-ttu-id="44513-147">在本教程中，您将使用控件的值来筛选在 GridView 中显示的记录。</span><span class="sxs-lookup"><span data-stu-id="44513-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="44513-148">将**控件**特性添加到之前创建的查询方法。</span><span class="sxs-lookup"><span data-stu-id="44513-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="44513-149">在[后面](using-query-string-values-to-retrieve-data.md)的教程中，你要将**QueryString**特性应用于参数以指定参数值来自查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="44513-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="44513-150">首先，在 ValidationSummary 上方添加一个下拉列表，用于筛选显示的学生。</span><span class="sxs-lookup"><span data-stu-id="44513-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="44513-151">在代码隐藏文件中，修改 select 方法以接收来自控件的值，并将参数的名称设置为提供该值的控件的名称。</span><span class="sxs-lookup"><span data-stu-id="44513-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="44513-152">必须为**ModelBinding**命名空间添加**using**语句以解析控件属性。</span><span class="sxs-lookup"><span data-stu-id="44513-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="44513-153">下面的代码演示了选择方法重新工作，以根据下拉列表的值筛选返回的数据。</span><span class="sxs-lookup"><span data-stu-id="44513-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="44513-154">在参数之前添加控件特性会将此参数的值指定为具有相同名称的控件。</span><span class="sxs-lookup"><span data-stu-id="44513-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="44513-155">运行 web 应用程序并从下拉列表中选择不同的值，以筛选学生列表。</span><span class="sxs-lookup"><span data-stu-id="44513-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![筛选学生](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="44513-157">结论</span><span class="sxs-lookup"><span data-stu-id="44513-157">Conclusion</span></span>

<span data-ttu-id="44513-158">在本教程中，将对数据进行排序和分页。</span><span class="sxs-lookup"><span data-stu-id="44513-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="44513-159">还启用了按控件的值筛选数据。</span><span class="sxs-lookup"><span data-stu-id="44513-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="44513-160">在下一[教程](integrating-jquery-ui.md)中，你将通过将 JQuery UI 小组件集成到动态数据模板来增强 UI。</span><span class="sxs-lookup"><span data-stu-id="44513-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="44513-161">[上一页](updating-deleting-and-creating-data.md)
> [下一页](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="44513-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
