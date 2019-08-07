---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：使用 ASP.NET MVC 应用程序中的实体框架添加排序、筛选和分页 |Microsoft Docs
author: tdykstra
description: 在本教程中, 您将向**学生**索引页添加排序、筛选和分页功能。 还会创建一个简单的分组页面。
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810752"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="ad6b4-104">教程：使用 ASP.NET MVC 应用程序中的实体框架添加排序、筛选和分页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-104">Tutorial: Add sorting, filtering, and paging with the Entity Framework in an ASP.NET MVC application</span></span>

<span data-ttu-id="ad6b4-105">在[上一教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)中, 你为`Student`实体的基本 CRUD 操作实现了一组网页。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-105">In the [previous tutorial](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="ad6b4-106">在本教程中, 您将向**学生**索引页添加排序、筛选和分页功能。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-106">In this tutorial you add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="ad6b4-107">还会创建一个简单的分组页面。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-107">You also create a simple grouping page.</span></span>

<span data-ttu-id="ad6b4-108">下图显示了完成后页面的外观。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-108">The following image shows what the page will look like when you're done.</span></span> <span data-ttu-id="ad6b4-109">列标题是用户可以单击以按该列排序的链接。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="ad6b4-110">重复单击列标题可在升降排序顺序之间切换。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="ad6b4-112">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad6b4-113">添加列排序链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-113">Add column sort links</span></span>
> * <span data-ttu-id="ad6b4-114">添加“搜索”框</span><span class="sxs-lookup"><span data-stu-id="ad6b4-114">Add a Search box</span></span>
> * <span data-ttu-id="ad6b4-115">添加分页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-115">Add paging</span></span>
> * <span data-ttu-id="ad6b4-116">创建“关于”页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-116">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad6b4-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="ad6b4-117">Prerequisites</span></span>

* [<span data-ttu-id="ad6b4-118">实现基本的 CRUD 功能</span><span class="sxs-lookup"><span data-stu-id="ad6b4-118">Implementing Basic CRUD Functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="ad6b4-119">添加列排序链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-119">Add column sort links</span></span>

<span data-ttu-id="ad6b4-120">若要将排序添加到 "学生索引" 页, 您`Index`将更改`Student`控制器的方法, 并将代码`Student`添加到 "索引" 视图中。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="ad6b4-121">向 Index 方法添加排序功能</span><span class="sxs-lookup"><span data-stu-id="ad6b4-121">Add sorting functionality to the Index method</span></span>

- <span data-ttu-id="ad6b4-122">在*Controllers\StudentController.cs*中, 将`Index`方法替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="ad6b4-123">此代码接收来自 URL 中的查询字符串的 `sortOrder` 参数。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="ad6b4-124">查询字符串值由 ASP.NET MVC 作为操作方法的参数提供。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="ad6b4-125">参数是一个字符串, 该字符串可以是 "Name" 或 "Date", 还可以后跟下划线和字符串 "desc" 来指定降序。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-125">The parameter is a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="ad6b4-126">默认排序顺序为升序。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-126">The default sort order is ascending.</span></span>

<span data-ttu-id="ad6b4-127">首次请求索引页时，没有任何查询字符串。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="ad6b4-128">学生将按升序`LastName`显示, 这是`switch`语句中的贯穿事例建立的默认设置。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="ad6b4-129">当用户单击列标题超链接时，查询字符串中会提供相应的 `sortOrder` 值。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="ad6b4-130">使用这`ViewBag`两个变量, 以便视图可以使用适当的查询字符串值配置列标题超链接:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="ad6b4-131">这些是三元语句。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-131">These are ternary statements.</span></span> <span data-ttu-id="ad6b4-132">第一个`sortOrder`参数指定如果参数为 null 或为空, `ViewBag.NameSortParm`则应将设置为 "名称\_desc"; 否则, 它应设置为空字符串。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="ad6b4-133">通过这两个语句，视图可如下设置列标题超链接：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="ad6b4-134">当前排序顺序</span><span class="sxs-lookup"><span data-stu-id="ad6b4-134">Current sort order</span></span> | <span data-ttu-id="ad6b4-135">姓氏超链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-135">Last Name Hyperlink</span></span> | <span data-ttu-id="ad6b4-136">日期超链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad6b4-137">姓氏升序</span><span class="sxs-lookup"><span data-stu-id="ad6b4-137">Last Name ascending</span></span> | <span data-ttu-id="ad6b4-138">descending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-138">descending</span></span> | <span data-ttu-id="ad6b4-139">ascending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-139">ascending</span></span> |
| <span data-ttu-id="ad6b4-140">姓氏降序</span><span class="sxs-lookup"><span data-stu-id="ad6b4-140">Last Name descending</span></span> | <span data-ttu-id="ad6b4-141">ascending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-141">ascending</span></span> | <span data-ttu-id="ad6b4-142">ascending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-142">ascending</span></span> |
| <span data-ttu-id="ad6b4-143">日期升序</span><span class="sxs-lookup"><span data-stu-id="ad6b4-143">Date ascending</span></span> | <span data-ttu-id="ad6b4-144">ascending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-144">ascending</span></span> | <span data-ttu-id="ad6b4-145">descending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-145">descending</span></span> |
| <span data-ttu-id="ad6b4-146">日期降序</span><span class="sxs-lookup"><span data-stu-id="ad6b4-146">Date descending</span></span> | <span data-ttu-id="ad6b4-147">ascending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-147">ascending</span></span> | <span data-ttu-id="ad6b4-148">ascending</span><span class="sxs-lookup"><span data-stu-id="ad6b4-148">ascending</span></span> |

<span data-ttu-id="ad6b4-149">方法使用[LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)指定排序所依据的列。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-149">The method uses [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) to specify the column to sort by.</span></span> <span data-ttu-id="ad6b4-150">此代码在`switch`语句<xref:System.Linq.IQueryable%601>前创建一个变量`switch` , 在`switch`语句中进行修改, 并在语句`ToList`后调用方法。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-150">The code creates an <xref:System.Linq.IQueryable%601> variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="ad6b4-151">当创建和修改 `IQueryable` 变量时，不会向数据库发送任何查询。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="ad6b4-152">在您通过调用方法 (如) `IQueryable` `ToList`将对象转换为集合之前, 不会执行查询。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="ad6b4-153">因此, 此代码将产生单个查询, 该查询在`return View`语句之前不会执行。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="ad6b4-154">除了为每个排序顺序编写不同 LINQ 语句外, 还可以动态创建 LINQ 语句。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-154">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="ad6b4-155">有关动态 LINQ 的信息, 请参阅[DYNAMIC linq](https://go.microsoft.com/fwlink/?LinkID=323957)。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-155">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="ad6b4-156">向 "学生索引" 视图添加列标题超链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-156">Add column heading hyperlinks to the Student index view</span></span>

1. <span data-ttu-id="ad6b4-157">在*Views\Student\Index.cshtml*中, 将`<tr>`标题`<th>`行的和元素替换为突出显示的代码:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-157">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   <span data-ttu-id="ad6b4-158">此代码使用`ViewBag`属性中的信息设置具有适当查询字符串值的超链接。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-158">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

2. <span data-ttu-id="ad6b4-159">运行页面, 然后单击 "**姓氏**" 和 "**注册日期**" 列标题, 验证排序是否正常。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-159">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

   <span data-ttu-id="ad6b4-160">单击**姓氏**标题后, 学生会按姓氏的降序顺序显示。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-160">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

## <a name="add-a-search-box"></a><span data-ttu-id="ad6b4-161">添加“搜索”框</span><span class="sxs-lookup"><span data-stu-id="ad6b4-161">Add a Search box</span></span>

<span data-ttu-id="ad6b4-162">若要将筛选添加到 "学生索引" 页, 您将向视图添加一个文本框和一个提交按钮, 并在`Index`方法中进行相应的更改。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-162">To add filtering to the Students index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="ad6b4-163">文本框允许您在 "名字" 和 "姓氏" 字段中输入要搜索的字符串。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-163">The text box lets you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="ad6b4-164">向 Index 方法添加筛选功能</span><span class="sxs-lookup"><span data-stu-id="ad6b4-164">Add filtering functionality to the Index method</span></span>

- <span data-ttu-id="ad6b4-165">在*Controllers\StudentController.cs*中, 将`Index`方法替换为以下代码 (更改已突出显示):</span><span class="sxs-lookup"><span data-stu-id="ad6b4-165">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="ad6b4-166">代码将`searchString`参数添加`Index`到方法。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-166">The code adds a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="ad6b4-167">从要添加到索引视图的文本框中接收搜索字符串值。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="ad6b4-168">它还向 LINQ `where`语句添加一个子句, 该子句仅选择其名字或姓氏包含搜索字符串的学生。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-168">It also adds a `where` clause to the LINQ statement that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="ad6b4-169">仅当存在要搜索<xref:System.Linq.Queryable.Where%2A>的值时, 才会执行添加子句的语句。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-169">The statement that adds the <xref:System.Linq.Queryable.Where%2A> clause executes only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="ad6b4-170">在许多情况下, 你可以对实体框架实体集或作为内存中集合上的扩展方法调用同一方法。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-170">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="ad6b4-171">结果通常是相同的, 但在某些情况下可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-171">The results are normally the same but in some cases may be different.</span></span>
>
> <span data-ttu-id="ad6b4-172">例如, 将空字符串传递给它`Contains`时, 方法的 .NET Framework 实现将返回所有行, 但 SQL Server Compact 4.0 的实体框架提供程序将为空字符串返回零行。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-172">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="ad6b4-173">因此, 示例中的代码 (将`Where`语句放入`if`语句中) 可确保您获得的所有版本 SQL Server 的结果相同。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-173">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="ad6b4-174">此外, 默认情况下, `Contains`方法的 .NET Framework 实现会执行区分大小写的比较, 但实体框架 SQL Server 提供程序默认情况下执行不区分大小写的比较。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-174">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="ad6b4-175">因此, 调用`ToUpper`方法以使测试明确区分大小写确保在稍后更改代码以使用存储库时结果不会更改, 这将`IEnumerable`返回集合而不是`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-175">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="ad6b4-176">（在 `IEnumerable` 集合上调用 `Contains` 方法时，将获得 .NET Framework 实现；当在 `IQueryable` 对象上调用它时，将获得数据库提供程序实现。）</span><span class="sxs-lookup"><span data-stu-id="ad6b4-176">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
>
> <span data-ttu-id="ad6b4-177">对于不同的数据库提供程序, 或者当你使用`IQueryable` `IEnumerable`集合时, 如果你使用与对象比较, 则 Null 处理也可能不同。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-177">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="ad6b4-178">例如, 在某些情况下, `Where`诸如之类`table.Column != 0`的条件可能不会返回具有`null`作为值的列。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-178">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="ad6b4-179">默认情况下, EF 会生成附加的 SQL 运算符, 使 null 值在数据库中的运行方式与在内存中工作时的工作方式相等, 但你可以在 EF6 中设置[UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics)标志, 或在 EF Core 中调用[UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls)方法, 以配置此行为。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-179">By default, EF generates additional SQL operators to make equality between null values work in the database like it works in memory, but you can set the [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) flag in EF6 or call the [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) method in EF Core to configure this behavior.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="ad6b4-180">向 "学生索引" 视图添加搜索框</span><span class="sxs-lookup"><span data-stu-id="ad6b4-180">Add a search box to the Student index view</span></span>

1. <span data-ttu-id="ad6b4-181">在*Views\Student\Index.cshtml*中, 将突出显示的代码添加到`table`开始标记之前, 以便创建标题、文本框和**搜索**按钮。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-181">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. <span data-ttu-id="ad6b4-182">运行页面, 输入搜索字符串, 并单击 "**搜索**" 以验证筛选是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-182">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

   <span data-ttu-id="ad6b4-183">请注意, 该 URL 不包含 "a" 搜索字符串, 这意味着, 如果您将此页面做成书签, 则在使用书签时, 不会收到筛选后的列表。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-183">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="ad6b4-184">这也适用于列排序链接, 因为它们将对整个列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-184">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="ad6b4-185">在本教程后面的部分中, 您将更改 "**搜索**" 按钮以使用筛选器条件的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-185">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging"></a><span data-ttu-id="ad6b4-186">添加分页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-186">Add paging</span></span>

<span data-ttu-id="ad6b4-187">若要将分页添加到 "学生索引" 页, 你将首先安装**PagedList** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-187">To add paging to the Students index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="ad6b4-188">然后在`Index`方法中进行其他更改, 并向`Index`视图添加分页链接。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-188">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="ad6b4-189">**PagedList**是 ASP.NET Mvc 的许多良好分页和排序包之一, 这里的用途只是一个示例, 而不是针对其他选项的建议。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-189">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span>

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="ad6b4-190">安装 PagedList NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ad6b4-190">Install the PagedList.MVC NuGet package</span></span>

<span data-ttu-id="ad6b4-191">NuGet **PagedList**包会自动将**PagedList**包作为依赖项安装。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="ad6b4-192">**PagedList**包为`PagedList` `IQueryable`和集合安装集合类型和扩展方法。`IEnumerable`</span><span class="sxs-lookup"><span data-stu-id="ad6b4-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="ad6b4-193">扩展`PagedList`方法在`IQueryable`或`IEnumerable`的集合中创建单个数据页, 而`PagedList`集合提供了几个便于分页的属性和方法。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="ad6b4-194">**PagedList**包安装显示分页按钮的分页帮助程序。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

1. <span data-ttu-id="ad6b4-195">从 "**工具**" 菜单中, 依次选择 " **NuGet 包管理器**" 和 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-195">From the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>

2. <span data-ttu-id="ad6b4-196">在 "**程序包管理器控制台**" 窗口中, 确保 "**包源**" 为 " **Nuget.org** ", 并且 "**默认项目**" 是 " **ContosoUniversity**", 然后输入以下命令:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

   ```text
   Install-Package PagedList.Mvc
   ```

3. <span data-ttu-id="ad6b4-197">生成项目。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-197">Build the project.</span></span>

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="ad6b4-198">向 Index 方法添加分页功能</span><span class="sxs-lookup"><span data-stu-id="ad6b4-198">Add paging functionality to the Index method</span></span>

1. <span data-ttu-id="ad6b4-199">在*Controllers\StudentController.cs*中, 为`using` `PagedList`命名空间添加语句:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-199">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. <span data-ttu-id="ad6b4-200">将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-200">Replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   <span data-ttu-id="ad6b4-201">此代码将一个`page`参数、一个当前排序顺序参数和一个当前的筛选器参数添加到方法签名:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-201">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="ad6b4-202">第一次显示页面时, 或如果用户未单击分页或排序链接, 则所有参数都为 null。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-202">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters are null.</span></span> <span data-ttu-id="ad6b4-203">如果单击了某个页面链接, 则`page`该变量将包含要显示的页码。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-203">If a paging link is clicked, the `page` variable contains the page number to display.</span></span>

   <span data-ttu-id="ad6b4-204">`ViewBag`属性提供当前排序顺序的视图, 因为它必须包含在分页链接中, 以便在分页时保持排序顺序相同:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-204">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   <span data-ttu-id="ad6b4-205">其他属性`ViewBag.CurrentFilter`提供当前筛选器字符串的视图。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-205">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="ad6b4-206">此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-206">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="ad6b4-207">如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-207">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="ad6b4-208">在文本框中输入值并按 "提交" 按钮时, 将更改搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-208">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="ad6b4-209">在这种情况下`searchString` , 参数不为 null。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-209">In that case, the `searchString` parameter is not null.</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   <span data-ttu-id="ad6b4-210">在方法结束时, 学生`ToPagedList` `IQueryable`对象上的扩展方法会将学生查询转换为支持分页的集合类型中的一页学生。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-210">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="ad6b4-211">然后, 将一页学生传递到视图:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-211">That single page of students is then passed to the view:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   <span data-ttu-id="ad6b4-212">`ToPagedList` 方法需要一个页码。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-212">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="ad6b4-213">这两个问号表示[null 合并运算符](/dotnet/csharp/language-reference/operators/null-coalescing-operator)。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-213">The two question marks represent the [null-coalescing operator](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span></span> <span data-ttu-id="ad6b4-214">NULL 合并运算符为可为 NULL 的类型定义默认值；表达式 `(page ?? 1)` 表示如果 `page` 有值，则返回该值，如果 `page` 为 NULL，则返回 1。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-214">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="ad6b4-215">向 "学生索引" 视图添加寻呼链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-215">Add paging links to the Student index view</span></span>

1. <span data-ttu-id="ad6b4-216">在*Views\Student\Index.cshtml*中, 将现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-216">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="ad6b4-217">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-217">The changes are highlighted.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   <span data-ttu-id="ad6b4-218">页面顶部的 `@model` 语句指定视图现在获取的是 `PagedList` 对象，而不是 `List` 对象。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-218">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

   <span data-ttu-id="ad6b4-219">`using` 的`PagedList.Mvc`语句提供对分页按钮的 MVC 帮助器的访问。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-219">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

   <span data-ttu-id="ad6b4-220">代码使用[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))的重载, 以允许它指定[FormMethod](/previous-versions/aspnet/dd460179(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-220">The code uses an overload of [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) that allows it to specify [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   <span data-ttu-id="ad6b4-221">默认[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))使用 POST 提交窗体数据, 这意味着参数将在 HTTP 消息正文中传递, 而不是作为查询字符串在 URL 中传递。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-221">The default [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="ad6b4-222">当指定 HTTP GET 时，表单数据作为查询字符串在 URL 中传递，从而使用户能够将 URL 加入书签。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-222">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="ad6b4-223">[W3C for the 使用 HTTP GET 的准则](http://www.w3.org/2001/tag/doc/whenToUseGet.html), 建议你在该操作不会导致更新时使用 get。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-223">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

   <span data-ttu-id="ad6b4-224">文本框使用当前的搜索字符串进行初始化, 因此, 当您单击新页时, 您可以看到当前搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-224">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   <span data-ttu-id="ad6b4-225">列标题链接使用查询字符串向控制器传递当前搜索字符串，以便用户可以在筛选结果中进行排序：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-225">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   <span data-ttu-id="ad6b4-226">显示当前页面和总页数。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-226">The current page and total number of pages are displayed.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   <span data-ttu-id="ad6b4-227">如果没有要显示的页, 则显示 "页 0/0"。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-227">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="ad6b4-228">(在这种情况下, 页码大于页计数, 因为`Model.PageNumber`为 1, 并且`Model.PageCount`为0。)</span><span class="sxs-lookup"><span data-stu-id="ad6b4-228">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

   <span data-ttu-id="ad6b4-229">页面按钮由`PagedListPager`帮助器显示:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-229">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   <span data-ttu-id="ad6b4-230">`PagedListPager`帮助程序提供了许多可自定义的选项, 包括 url 和样式。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-230">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="ad6b4-231">有关详细信息, 请参阅 GitHub 站点上的[TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-231">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

2. <span data-ttu-id="ad6b4-232">运行页面。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-232">Run the page.</span></span>

   <span data-ttu-id="ad6b4-233">单击不同排序顺序的分页链接，以确保分页正常工作。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-233">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="ad6b4-234">然后输入一个搜索字符串并再次尝试分页，以验证分页也可以正确地进行排序和筛选。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-234">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="ad6b4-235">创建“关于”页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-235">Create an About page</span></span>

<span data-ttu-id="ad6b4-236">对于 Contoso 大学网站的 "关于" 页, 您将显示已注册每个注册日期的学生数。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-236">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="ad6b4-237">这需要对组进行分组和简单计算。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-237">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="ad6b4-238">若要完成此操作，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-238">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="ad6b4-239">为需要传递给视图的数据创建一个视图模型类。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-239">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="ad6b4-240">修改`About` 控制器`Home`中的方法。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-240">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="ad6b4-241">`About`修改视图。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-241">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="ad6b4-242">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="ad6b4-242">Create the View Model</span></span>

<span data-ttu-id="ad6b4-243">在项目文件夹中创建*viewmodel*文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-243">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="ad6b4-244">在该文件夹中, 添加一个类文件*EnrollmentDateGroup.cs* , 并将模板代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-244">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="ad6b4-245">修改主控制器</span><span class="sxs-lookup"><span data-stu-id="ad6b4-245">Modify the Home Controller</span></span>

1. <span data-ttu-id="ad6b4-246">在*HomeController.cs*中, 在文件`using`顶部添加以下语句:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-246">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. <span data-ttu-id="ad6b4-247">直接在类的左大括号之后为数据库上下文添加类变量:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-247">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. <span data-ttu-id="ad6b4-248">将 `About` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-248">Replace the `About` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   <span data-ttu-id="ad6b4-249">LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在 `EnrollmentDateGroup` 视图模型对象的集合中。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-249">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

4. <span data-ttu-id="ad6b4-250">`Dispose`添加方法:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-250">Add a `Dispose` method:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="ad6b4-251">修改“关于”视图</span><span class="sxs-lookup"><span data-stu-id="ad6b4-251">Modify the About View</span></span>

1. <span data-ttu-id="ad6b4-252">将*Views\Home\About.cshtml*文件中的代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="ad6b4-252">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. <span data-ttu-id="ad6b4-253">运行应用, 并单击 "**关于**" 链接。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-253">Run the app and click the **About** link.</span></span>

   <span data-ttu-id="ad6b4-254">每个注册日期的学生计数显示在一个表中。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-254">The count of students for each enrollment date displays in a table.</span></span>

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a><span data-ttu-id="ad6b4-256">获取代码</span><span class="sxs-lookup"><span data-stu-id="ad6b4-256">Get the code</span></span>

[<span data-ttu-id="ad6b4-257">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="ad6b4-257">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="ad6b4-258">其他资源</span><span class="sxs-lookup"><span data-stu-id="ad6b4-258">Additional resources</span></span>

<span data-ttu-id="ad6b4-259">可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-259">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad6b4-260">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ad6b4-260">Next steps</span></span>

<span data-ttu-id="ad6b4-261">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="ad6b4-261">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad6b4-262">添加列排序链接</span><span class="sxs-lookup"><span data-stu-id="ad6b4-262">Add column sort links</span></span>
> * <span data-ttu-id="ad6b4-263">添加“搜索”框</span><span class="sxs-lookup"><span data-stu-id="ad6b4-263">Add a Search box</span></span>
> * <span data-ttu-id="ad6b4-264">添加分页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-264">Add paging</span></span>
> * <span data-ttu-id="ad6b4-265">创建“关于”页</span><span class="sxs-lookup"><span data-stu-id="ad6b4-265">Create an About page</span></span>

<span data-ttu-id="ad6b4-266">转到下一篇文章, 了解如何使用连接复原和命令截取。</span><span class="sxs-lookup"><span data-stu-id="ad6b4-266">Advance to the next article to learn how to use connection resiliency and command interception.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ad6b4-267">连接复原和命令截获</span><span class="sxs-lookup"><span data-stu-id="ad6b4-267">Connection resiliency and command interception</span></span>](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
