---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 使用查询字符串值通过模型绑定和 web 窗体筛选数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519080"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="6d51b-104">使用查询字符串值通过模型绑定和 web 窗体筛选数据</span><span class="sxs-lookup"><span data-stu-id="6d51b-104">Using query string values to filter data with model binding and web forms</span></span>

<span data-ttu-id="6d51b-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6d51b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6d51b-106">本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="6d51b-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="6d51b-107">与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。</span><span class="sxs-lookup"><span data-stu-id="6d51b-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="6d51b-108">此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="6d51b-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="6d51b-109">本教程介绍如何在查询字符串中传递值，并使用该值通过模型绑定来检索数据。</span><span class="sxs-lookup"><span data-stu-id="6d51b-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="6d51b-110">本教程基于在序列的[前面](retrieving-data.md)部分中创建的项目构建。</span><span class="sxs-lookup"><span data-stu-id="6d51b-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="6d51b-111">可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。</span><span class="sxs-lookup"><span data-stu-id="6d51b-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="6d51b-112">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="6d51b-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="6d51b-113">它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。</span><span class="sxs-lookup"><span data-stu-id="6d51b-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="6d51b-114">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="6d51b-114">What you'll build</span></span>

<span data-ttu-id="6d51b-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="6d51b-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="6d51b-116">添加新页面以显示学生的已注册课程</span><span class="sxs-lookup"><span data-stu-id="6d51b-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="6d51b-117">根据查询字符串中的值检索所选学生的已注册课程</span><span class="sxs-lookup"><span data-stu-id="6d51b-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="6d51b-118">使用从网格视图到新页面的查询字符串值添加超链接</span><span class="sxs-lookup"><span data-stu-id="6d51b-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="6d51b-119">本教程中的步骤与您在前面的[教程](sorting-paging-and-filtering-data.md)中执行的步骤非常相似，可以根据下拉列表中的用户选择筛选显示的学生。</span><span class="sxs-lookup"><span data-stu-id="6d51b-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="6d51b-120">在本教程中，您在 select 方法中使用了**control**特性来指定参数值来自控件。</span><span class="sxs-lookup"><span data-stu-id="6d51b-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="6d51b-121">在本教程中，您将使用 select 方法中的**QueryString**特性来指定参数值来自查询字符串。</span><span class="sxs-lookup"><span data-stu-id="6d51b-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="6d51b-122">添加新页面以显示学生的课程</span><span class="sxs-lookup"><span data-stu-id="6d51b-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="6d51b-123">添加新的 web 窗体，该窗体使用网站母版页，并为页面**课程**命名。</span><span class="sxs-lookup"><span data-stu-id="6d51b-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="6d51b-124">在 " **default.aspx** " 文件中，添加 "网格" 视图以显示所选学生的课程。</span><span class="sxs-lookup"><span data-stu-id="6d51b-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="6d51b-125">定义 select 方法</span><span class="sxs-lookup"><span data-stu-id="6d51b-125">Define the select method</span></span>

<span data-ttu-id="6d51b-126">在**Courses.aspx.cs**中，您将用在网格视图的**SelectMethod**属性中指定的名称添加 select 方法。</span><span class="sxs-lookup"><span data-stu-id="6d51b-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="6d51b-127">在该方法中，你将定义用于检索学生课程的查询，并指定参数来自与参数名称相同的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="6d51b-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="6d51b-128">首先，必须添加以下**using**语句。</span><span class="sxs-lookup"><span data-stu-id="6d51b-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="6d51b-129">然后，将以下代码添加到 Courses.aspx.cs：</span><span class="sxs-lookup"><span data-stu-id="6d51b-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="6d51b-130">QueryString 属性表示将名为 StudentID 的查询字符串值自动分配给此方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="6d51b-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="6d51b-131">添加带查询字符串值的超链接</span><span class="sxs-lookup"><span data-stu-id="6d51b-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="6d51b-132">在 "student" 的 "网格" 视图中，您将添加链接到您的新课程页面的超链接字段。</span><span class="sxs-lookup"><span data-stu-id="6d51b-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="6d51b-133">超链接将包含一个包含学生 id 的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="6d51b-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="6d51b-134">在 "student" 中，将以下字段添加到 "网格" 视图中紧靠总信用额度字段下方的列。</span><span class="sxs-lookup"><span data-stu-id="6d51b-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="6d51b-135">运行应用程序，并注意 "网格" 视图现在包含 "课程" 链接。</span><span class="sxs-lookup"><span data-stu-id="6d51b-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![添加超链接](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="6d51b-137">单击其中一个链接时，将看到该学生注册的课程。</span><span class="sxs-lookup"><span data-stu-id="6d51b-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![显示课程](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="6d51b-139">结论</span><span class="sxs-lookup"><span data-stu-id="6d51b-139">Conclusion</span></span>

<span data-ttu-id="6d51b-140">在本教程中，你添加了一个带有查询字符串值的链接。</span><span class="sxs-lookup"><span data-stu-id="6d51b-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="6d51b-141">你将查询字符串值用于 select 方法中的参数值。</span><span class="sxs-lookup"><span data-stu-id="6d51b-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="6d51b-142">在下一[教程](adding-business-logic-layer.md)中，你将代码从代码隐藏文件移动到业务逻辑层和数据访问层。</span><span class="sxs-lookup"><span data-stu-id="6d51b-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6d51b-143">[上一页](integrating-jquery-ui.md)
> [下一页](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="6d51b-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
