---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用程序中添加排序、筛选和分页实体框架 |Microsoft Docs
author: tdykstra
description: 在本教程中，您将向**学生**索引页添加排序、筛选和分页功能。 还会创建一个简单的分组页面。
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499328"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>教程：在 ASP.NET MVC 应用程序中添加排序、筛选和分页实体框架

在[上一教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)中，你为 `Student` 实体实现了一组用于基本 CRUD 操作的网页。 在本教程中，您将向**学生**索引页添加排序、筛选和分页功能。 还会创建一个简单的分组页面。

下图显示了完成后页面的外观。 列标题是用户可以单击以按该列排序的链接。 重复单击列标题可在升降排序顺序之间切换。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加列排序链接
> * 添加“搜索”框
> * 添加分页
> * 创建“关于”页

## <a name="prerequisites"></a>系统必备

* [实现基本的 CRUD 功能](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>添加列排序链接

若要将排序添加到 "学生索引" 页，您将更改 `Student` 控制器的 `Index` 方法，并将代码添加到 `Student` 索引视图。

### <a name="add-sorting-functionality-to-the-index-method"></a>向 Index 方法添加排序功能

- 在*Controllers\StudentController.cs*中，将 `Index` 方法替换为以下代码：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

此代码接收来自 URL 中的查询字符串的 `sortOrder` 参数。 查询字符串值由 ASP.NET MVC 作为操作方法的参数提供。 参数是一个字符串，该字符串可以是 "Name" 或 "Date"，还可以后跟下划线和字符串 "desc" 来指定降序。 默认排序顺序为升序。

首次请求索引页时，没有任何查询字符串。 学生按 `LastName`按升序显示，这是 `switch` 语句中由秋季事例建立的默认设置。 当用户单击列标题超链接时，查询字符串中会提供相应的 `sortOrder` 值。

使用两个 `ViewBag` 变量，以便视图可以使用适当的查询字符串值配置列标题超链接：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

这些是三元语句。 第一个参数指定如果 `sortOrder` 参数为 null 或为空，则 `ViewBag.NameSortParm` 应设置为 "name\_desc";否则，应将其设置为空字符串。 通过这两个语句，视图可如下设置列标题超链接：

| 当前的排序顺序 | 姓氏超链接 | 日期超链接 |
| --- | --- | --- |
| 姓氏升序 | descending | ascending |
| 姓氏降序 | ascending | ascending |
| 日期升序 | ascending | descending |
| 日期降序 | ascending | ascending |

方法使用[LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)指定排序所依据的列。 此代码在 `switch` 语句之前创建 <xref:System.Linq.IQueryable%601> 变量，在 `switch` 语句中修改它，并在 `switch` 语句后调用 `ToList` 方法。 当创建和修改 `IQueryable` 变量时，不会向数据库发送任何查询。 在通过调用方法（如 `ToList`）将 `IQueryable` 对象转换为集合之前，不会执行查询。 因此，此代码将产生单个查询，该查询在 `return View` 语句之前不会执行。

除了为每个排序顺序编写不同 LINQ 语句外，还可以动态创建 LINQ 语句。 有关动态 LINQ 的信息，请参阅[DYNAMIC linq](https://go.microsoft.com/fwlink/?LinkID=323957)。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>向 "学生索引" 视图添加列标题超链接

1. 在*Views\Student\Index.cshtml*中，将标题行的 `<tr>` 和 `<th>` 元素替换为突出显示的代码：

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   此代码使用 `ViewBag` 属性中的信息设置具有适当查询字符串值的超链接。

2. 运行页面，然后单击 "**姓氏**" 和 "**注册日期**" 列标题，验证排序是否正常。

   单击**姓氏**标题后，学生会按姓氏的降序顺序显示。

## <a name="add-a-search-box"></a>添加“搜索”框

若要将筛选添加到 "学生索引" 页，您将向视图添加一个文本框和一个提交按钮，并在 `Index` 方法中进行相应的更改。 文本框允许您在 "名字" 和 "姓氏" 字段中输入要搜索的字符串。

### <a name="add-filtering-functionality-to-the-index-method"></a>向索引方法添加筛选功能

- 在*Controllers\StudentController.cs*中，将 `Index` 方法替换为以下代码（更改已突出显示）：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

该代码将 `searchString` 参数添加到 `Index` 方法。 从要添加到索引视图的文本框中接收搜索字符串值。 它还将 `where` 子句添加到 LINQ 语句，该语句仅选择其名字或姓氏中包含搜索字符串的学生。 仅当存在要搜索的值时，才会执行添加 <xref:System.Linq.Queryable.Where%2A> 子句的语句。

> [!NOTE]
> 在许多情况下，你可以对实体框架实体集或作为内存中集合上的扩展方法调用同一方法。 结果通常是相同的，但在某些情况下可能会有所不同。
>
> 例如，将空字符串传递给它时，`Contains` 方法的 .NET Framework 实现将返回所有行，但 SQL Server Compact 4.0 的实体框架提供程序将为空字符串返回零行。 因此，该示例中的代码（将 `Where` 语句置于 `if` 语句中）可确保您获得的所有版本 SQL Server 的结果相同。 此外，默认情况下，`Contains` 方法的 .NET Framework 实现会执行区分大小写的比较，但默认情况下实体框架 SQL Server 提供程序执行不区分大小写的比较。 因此，调用 `ToUpper` 方法来使测试明确区分大小写确保在稍后更改代码以使用存储库时结果不会发生变化，这将返回一个 `IEnumerable` 集合，而不是 `IQueryable` 对象。 （在 `Contains` 集合上调用 `IEnumerable` 方法时，将获得 .NET Framework 实现；当在 `IQueryable` 对象上调用它时，将获得数据库提供程序实现。）
>
> 对于不同的数据库提供程序，或者当你使用 `IEnumerable` 集合时，与使用 `IQueryable` 对象相比，Null 处理也可能不同。 例如，在某些情况下，`Where` 条件（如 `table.Column != 0`）可能不会返回 `null` 作为值的列。 默认情况下，EF 会生成附加的 SQL 运算符，使 null 值在数据库中的运行方式与在内存中工作时的工作方式相等，但你可以在 EF6 中设置[UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics)标志，或在 EF Core 中调用[UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls)方法来配置此行为。

### <a name="add-a-search-box-to-the-student-index-view"></a>向 "学生索引" 视图添加搜索框

1. 在*Views\Student\Index.cshtml*中，将突出显示的代码添加到开始 `table` 标记之前，以便创建标题、文本框和**搜索**按钮。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. 运行页面，输入搜索字符串，并单击 "**搜索**" 以验证筛选是否正常工作。

   请注意，该 URL 不包含 "a" 搜索字符串，这意味着，如果您将此页面做成书签，则在使用书签时，不会收到筛选后的列表。 这也适用于列排序链接，因为它们将对整个列表进行排序。 在本教程后面的部分中，您将更改 "**搜索**" 按钮以使用筛选器条件的查询字符串。

## <a name="add-paging"></a>添加分页

若要将分页添加到 "学生索引" 页，你将首先安装**PagedList** NuGet 包。 然后，在 `Index` 方法中进行其他更改，并向 `Index` 视图添加分页链接。 **PagedList**是 ASP.NET Mvc 的许多良好分页和排序包之一，这里的用途只是一个示例，而不是针对其他选项的建议。

### <a name="install-the-pagedlistmvc-nuget-package"></a>安装 PagedList NuGet 包

NuGet **PagedList**包会自动将**PagedList**包作为依赖项安装。 **PagedList**包将为 `IQueryable` 和 `IEnumerable` 集合安装 `PagedList` 的集合类型和扩展方法。 扩展方法在 `IQueryable` 或 `IEnumerable`之外的 `PagedList` 集合中创建单个数据页，而 `PagedList` 集合提供了几个便于分页的属性和方法。 **PagedList**包安装显示分页按钮的分页帮助程序。

1. 从 "**工具**" 菜单中，依次选择 " **NuGet 包管理器**" 和 "**程序包管理器控制台**"。

2. 在 "**程序包管理器控制台**" 窗口中，确保 "**包源**" 为 " **Nuget.org** "，并且 "**默认项目**" 是 " **ContosoUniversity**"，然后输入以下命令：

   ```text
   Install-Package PagedList.Mvc
   ```

3. 生成项目。

### <a name="add-paging-functionality-to-the-index-method"></a>向 Index 方法添加分页功能

1. 在*Controllers\StudentController.cs*中，添加 `PagedList` 命名空间的 `using` 语句：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. 将 `Index` 方法替换为以下代码：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   此代码将 `page` 参数、当前排序顺序参数和当前筛选器参数添加到方法签名：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   第一次显示页面时，或如果用户未单击分页或排序链接，则所有参数都为 null。 如果单击了页面链接，则 `page` 变量包含要显示的页码。

   `ViewBag` 属性提供当前排序顺序的视图，因为它必须包含在分页链接中，以便在分页时保持排序顺序相同：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   `ViewBag.CurrentFilter`的另一个属性提供当前筛选器字符串的视图。 此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。 如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。 在文本框中输入值并按 "提交" 按钮时，将更改搜索字符串。 在这种情况下，`searchString` 参数不为 null。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   在方法结束时，学生 `IQueryable` 对象的 `ToPagedList` 扩展方法会将学生查询转换为支持分页的集合类型中的一页学生。 然后，将一页学生传递到视图：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   `ToPagedList` 方法需要一个页码。 这两个问号表示[null 合并运算符](/dotnet/csharp/language-reference/operators/null-coalescing-operator)。 NULL 合并运算符为可为 NULL 的类型定义默认值；表达式 `(page ?? 1)` 表示如果 `page` 有值，则返回该值，如果 `page` 为 NULL，则返回 1。

### <a name="add-paging-links-to-the-student-index-view"></a>向 "学生索引" 视图添加寻呼链接

1. 在*Views\Student\Index.cshtml*中，将现有代码替换为以下代码。 突出显示所作更改。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   页面顶部的 `@model` 语句指定视图现在获取的是 `PagedList` 对象，而不是 `List` 对象。

   `PagedList.Mvc` 的 `using` 语句提供对用于分页按钮的 MVC 帮助器的访问权限。

   代码使用[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))的重载，以允许它指定[FormMethod](/previous-versions/aspnet/dd460179(v=vs.100))。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   默认[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))使用 POST 提交窗体数据，这意味着参数将在 HTTP 消息正文中传递，而不是作为查询字符串在 URL 中传递。 当指定 HTTP GET 时，表单数据作为查询字符串在 URL 中传递，从而使用户能够将 URL 加入书签。 [W3C for the 使用 HTTP GET 的准则](http://www.w3.org/2001/tag/doc/whenToUseGet.html)，建议你在该操作不会导致更新时使用 get。

   文本框使用当前的搜索字符串进行初始化，因此，当您单击新页时，您可以看到当前搜索字符串。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   列标题链接使用查询字符串向控制器传递当前搜索字符串，以便用户可以在筛选结果中进行排序：

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   显示当前页面和总页数。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   如果没有要显示的页，则显示 "页 0/0"。 （在这种情况下，页码大于页面计数，因为 `Model.PageNumber` 为1，`Model.PageCount` 为0。）

   页面按钮由 `PagedListPager` 帮助器显示：

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   `PagedListPager` 帮助程序提供了许多可自定义的选项，包括 Url 和样式。 有关详细信息，请参阅 GitHub 站点上的[TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。

2. 运行页面。

   单击不同排序顺序的分页链接，以确保分页正常工作。 然后输入一个搜索字符串并再次尝试分页，以验证分页也可以正确地进行排序和筛选。

## <a name="create-an-about-page"></a>创建“关于”页

对于 Contoso 大学网站的 "关于" 页，您将显示已注册每个注册日期的学生数。 这需要对组进行分组和简单计算。 若要完成此操作，需要执行以下操作：

- 为需要传递给视图的数据创建一个视图模型类。
- 修改 `Home` 控制器中的 `About` 方法。
- 修改 `About` 视图。

### <a name="create-the-view-model"></a>创建视图模型

在项目文件夹中创建*viewmodel*文件夹。 在该文件夹中，添加一个类文件*EnrollmentDateGroup.cs* ，并将模板代码替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>修改 Home 控制器

1. 在*HomeController.cs*中，将以下 `using` 语句添加到文件顶部：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. 直接在类的左大括号之后为数据库上下文添加类变量：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. 将 `About` 方法替换为以下代码：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在 `EnrollmentDateGroup` 视图模型对象的集合中。

4. 添加 `Dispose` 方法：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>修改“关于”视图

1. 将*Views\Home\About.cshtml*文件中的代码替换为以下代码：

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. 运行应用，并单击 "**关于**" 链接。

   每个注册日期的学生计数显示在一个表中。

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加列排序链接
> * 添加“搜索”框
> * 添加分页
> * 创建“关于”页

转到下一篇文章，了解如何使用连接复原和命令截取。
> [!div class="nextstepaction"]
> [连接复原和命令截获](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
