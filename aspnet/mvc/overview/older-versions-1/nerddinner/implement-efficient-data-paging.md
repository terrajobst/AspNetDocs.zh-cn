---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效的数据分页 |Microsoft Docs
author: microsoft
description: 步骤8显示了如何将分页支持添加到我们的/Dinners URL，以便不会立即显示1000次就，而只会在 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486482"
---
# <a name="implement-efficient-data-paging"></a>实现高效数据分页

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第8步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤8显示了如何将分页支持添加到/Dinners URL，以便一次只显示10个即将开始的就，并允许最终用户在 SEO 友好的方式下翻到整个列表。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner 步骤8：分页支持

如果我们的站点成功，会有数千个即将发布的就。 我们需要确保 UI 能缩放以处理所有这些就，并允许用户浏览它们。 为实现此目的，我们将向 */Dinners* URL 添加分页支持，以便一次只显示10个即将开始的就，并允许最终用户在 SEO 友好的方式下翻到整个列表。

### <a name="index-action-method-recap"></a>Index （）操作方法概述

DinnersController 类中的 Index （）操作方法当前如下所示：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

向 */Dinners* URL 发出请求时，它将检索所有即将发布的就的列表，并呈现所有即将发布的列表：

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>了解 IQueryable&lt;T&gt;

*IQueryable&lt;t&gt;* 是在 .net 3.5 中作为 LINQ 引入的一个接口。 它实现了强大的 "延迟执行" 方案，我们可以利用它们来实现分页支持。

在我们的 DinnerRepository 中，我们将从 FindUpcomingDinners （）方法中返回一个 IQueryable&lt;晚宴&gt; 序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

FindUpcomingDinners （）方法返回的 IQueryable&lt;晚宴&gt; 对象封装了一个查询，该查询使用 LINQ to SQL 从数据库中检索晚餐对象。 重要的是，在尝试访问或循环访问查询中的数据之前，或在调用 System.linq.enumerable.tolist （）方法之前，不会对数据库执行查询。 调用我们的 FindUpcomingDinners （）方法的代码可以选择在执行查询之前将其他 "链接" 操作/筛选器添加到 IQueryable&lt;晚宴&gt; 对象。 然后 LINQ to SQL 就足以在请求数据时对数据库执行合并查询。

若要实现分页逻辑，我们可以更新 DinnersController 的 Index （）操作方法，以便在调用 System.linq.enumerable.tolist （）之前将其他 "Skip" 和 "Take" 运算符应用于返回的 IQueryable&lt;晚宴&gt; 序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上面的代码将跳过数据库中前10个即将发布的就，然后返回20就。 LINQ to SQL 非常智能，足以构造在 SQL 数据库（而不是 web-服务器）中执行此跳过逻辑的优化 SQL 查询。 这意味着，即使在数据库中有数百万个即将发布的就，此请求的一部分也只会检索到10个所需的10（使其高效且可缩放）。

### <a name="adding-a-page-value-to-the-url"></a>向 URL 添加 "页面" 值

我们希望 Url 包含一个 "页面" 参数，该参数指示用户正在请求的晚餐范围，而不是对特定页面范围进行硬编码。

#### <a name="using-a-querystring-value"></a>使用 Querystring 值

下面的代码演示了如何更新 Index （）操作方法以支持 querystring 参数并启用 Url，如 */Dinners？ page = 2*：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上面的 Index （）操作方法有一个名为 "page" 的参数。 参数声明为可以为 null 的整数（这是 int？指示的值）。 这意味着 */Dinners？ page = 2* URL 将导致值 "2" 作为参数值传递。 */Dinners* URL （无 querystring 值）将导致传递 null 值。

我们将页面值乘以页面大小（在本例中为10行），以确定要跳过多少就。 在处理可以为 null 的类型时，我们使用的[ C#是 null "合并" 运算符（？？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) 。 如果 page 参数为 null，上面的代码会将值赋给0。

#### <a name="using-embedded-url-values"></a>使用嵌入的 URL 值

使用查询字符串值的一种替代方法是在实际 URL 本身中嵌入页参数。 例如： */Dinners/Page/2*或 */Dinners/2*。 ASP.NET MVC 包含一个功能强大的 URL 路由引擎，可轻松支持此类方案。

我们可以注册将任何传入 URL 或 URL 格式映射到所需的任何控制器类或操作方法的自定义路由规则。 我们需要做的就是在项目中打开 global.asax 文件：

![](implement-efficient-data-paging/_static/image2.png)

然后，使用 Maproute.html （） helper 方法（如对路由的第一次调用）注册新的映射规则。下面的 Maproute.html （）：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

在此之前，我们将注册一个名为 "UpcomingDinners" 的新路由规则。 我们指示其 URL 格式为 "就/Page/{Page}" –其中 {Page} 是嵌入在 URL 中的参数值。 Maproute.html （）方法的第三个参数指示应将与此格式匹配的 Url 映射到 DinnersController 类的 Index （）操作方法。

我们可以使用我们之前与查询字符串方案相同的索引（）代码，但现在我们的 "page" 参数将来自 URL，而不是来自 querystring：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

现在，当我们运行该应用程序并键入 */Dinners*时，我们将看到前10个即将发布的就：

![](implement-efficient-data-paging/_static/image3.png)

当我们在 */Dinners/Page/1*中键入内容时，将看到下一页就：

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>添加页面导航 UI

完成分页方案的最后一步是在视图模板中实现 "下一步" 和 "上一步" 导航用户界面，使用户能够轻松跳过晚餐数据。

若要正确实现此操作，我们需要知道数据库中就的总数，以及这要转换到的数据页的数目。 接下来，我们需要计算当前请求的 "page" 值是位于数据的开头还是结尾，并相应地显示或隐藏 "上一页" 和 "下一页" UI。 我们可以在索引（）操作方法中实现此逻辑。 此外，我们还可以向项目中添加一个帮助器类，以便以一种可重复使用的方式封装此逻辑。

下面是一个简单的 "PaginatedList" 帮助器类，它派生自内置 .NET Framework&gt; 集合类的列表&lt;。 它实现可重复使用的集合类，该类可用于对 IQueryable 数据的任意序列进行分页。 在我们的 NerdDinner 应用程序中，我们将使用 IQueryable&lt;晚宴&gt; 结果，但可以轻松地针对 IQueryable&lt;Product&gt; 或 IQueryable&lt;客户&gt; 会在其他应用程序方案中产生结果：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

请注意上面它如何计算并显示 "PageIndex"、"PageSize"、"TotalCount" 和 "TotalPages" 等属性。 它还将公开两个帮助器属性 "HasPreviousPage" 和 "HasNextPage"，以指示集合中的数据页是位于原始序列的开头还是结尾。 上面的代码将导致运行两个 SQL 查询-第一个查询用于检索晚餐对象总数的计数（这不返回对象，而是执行返回整数的 "SELECT COUNT" 语句），第二个用于仅检索行我们的数据库中所需的数据用于当前数据页。

接下来，我们可以更新 DinnersController （）帮助程序方法，从我们的 DinnerRepository （）结果创建 PaginatedList&lt;晚宴&gt;，并将其传递给我们的视图模板：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

然后，我们可以更新 \Views\Dinners\Index.aspx 视图模板，使其继承自 ViewPage&lt;NerdDinner。 PaginatedList&lt;晚餐&gt;&gt; 而不是 ViewPage&lt;IEnumerable&lt;晚餐&gt;&gt;，然后将以下代码添加到视图模板的底部：

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

请注意，我们如何使用 RouteLink （） helper 方法来生成超链接。 此方法类似于我们以前使用过的 Html.actionlink （） helper 方法。 不同之处在于，我们将使用我们在 global.asax 文件中设置的 "UpcomingDinners" 路由规则生成 URL。 这可以确保为索引（）操作方法生成 Url，格式为： */Dinners/Page/{page}* –其中，{Page} 值是我们基于当前 PageIndex 提供的变量。

现在，当我们再次运行应用程序时，我们将在浏览器中一次看到10个就：

![](implement-efficient-data-paging/_static/image5.png)

此外，我们还提供了 &lt;&lt;&lt; 和 &gt;&gt;&gt; 导航 UI，可让我们使用搜索引擎可访问的 Url 在我们的数据上跳过和反向：

![](implement-efficient-data-paging/_static/image6.png)

| **侧主题：了解 IQueryable&lt;T&gt; 的含义** |
| --- |
| IQueryable&lt;T&gt; 是一项功能强大的功能，可实现各种有趣的延迟执行方案（如分页和基于组合的查询）。 与所有强大的功能一样，你需要小心地使用它，并确保它不会被滥用。 务必认识到，从存储库返回 IQueryable&lt;T&gt; 结果，可以使调用代码向其追加链式运算符方法，并参与最终的查询执行。 如果你不希望为此功能提供调用代码，则应返回反向&lt;T&gt; 或 IEnumerable&lt;T&gt; 结果-其中包含已执行的查询的结果。 对于分页方案，这需要将实际的数据分页逻辑推送到被调用的存储库方法。 在此方案中，我们可能会将 FindUpcomingDinners （） finder 方法更新为具有返回 PaginatedList 的签名： PaginatedList&lt; 晚宴&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或返回 IList&lt;晚餐&gt;，并使用 "totalCount" out 参数返回就： IList&lt;晚餐&gt; FindUpcomingDinners （int pageIndex，int pageSize，out int totalCount） {} |

### <a name="next-step"></a>下一步

现在我们来看看如何向应用程序添加身份验证和授权支持。

> [!div class="step-by-step"]
> [上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)
