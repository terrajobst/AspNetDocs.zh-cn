---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: ASP.NET 网页更新数据库数据简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程说明如何在使用 ASP.NET 网页（Razor）时更新（更改）现有数据库条目。 它假定您已完成系列 。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463490"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="cb6aa-104">ASP.NET 网页更新数据库数据简介</span><span class="sxs-lookup"><span data-stu-id="cb6aa-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>

<span data-ttu-id="cb6aa-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cb6aa-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="cb6aa-106">本教程说明如何在使用 ASP.NET 网页（Razor）时更新（更改）现有数据库条目。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="cb6aa-107">假设已通过[使用 ASP.NET 网页的窗体通过输入数据](entering-data.md)完成了系列。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="cb6aa-108">学习内容：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="cb6aa-109">如何在 `WebGrid` 帮助程序中选择单个记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="cb6aa-110">如何从数据库中读取单个记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="cb6aa-111">如何使用数据库记录中的值预加载窗体。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="cb6aa-112">如何更新数据库中的现有记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="cb6aa-113">如何在页中存储信息而不显示它。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="cb6aa-114">如何使用隐藏字段存储信息。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="cb6aa-115">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="cb6aa-116">`WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="cb6aa-117">SQL `Update` 命令。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="cb6aa-118">`Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="cb6aa-119">隐藏字段（`<input type="hidden">`）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-119">Hidden fields (`<input type="hidden">`).</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="cb6aa-120">你将生成</span><span class="sxs-lookup"><span data-stu-id="cb6aa-120">What You'll Build</span></span>

<span data-ttu-id="cb6aa-121">在上一教程中，您学习了如何将记录添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="cb6aa-122">在这里，你将学习如何显示要编辑的记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="cb6aa-123">在*电影*页面中，你将更新 `WebGrid` 帮助程序，使其在每个电影旁显示一个**编辑**链接：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![WebGrid 显示每个电影的 "编辑" 链接](updating-data/_static/image1.png)

<span data-ttu-id="cb6aa-125">单击 "**编辑**" 链接时，将转到不同的页面，其中的影片信息已在表单中：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![显示要编辑的电影的 "编辑电影" 页面](updating-data/_static/image2.png)

<span data-ttu-id="cb6aa-127">您可以更改任何值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-127">You can change any of the values.</span></span> <span data-ttu-id="cb6aa-128">提交更改后，页面中的代码将更新数据库并返回到电影列表。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="cb6aa-129">此过程部分与你在上一教程中创建的*AddMovie*页面几乎完全相同，因此我们将熟悉本教程中的大部分内容。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="cb6aa-130">可以通过多种方式来实现编辑单个影片的方法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="cb6aa-131">选择的方法很容易实现并易于理解。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="cb6aa-132">向电影列表添加编辑链接</span><span class="sxs-lookup"><span data-stu-id="cb6aa-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="cb6aa-133">首先，将更新 "*电影*" 页面，使每个电影列表也包含一个**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="cb6aa-134">打开*电影. cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="cb6aa-135">在页面的正文中，通过添加列更改 `WebGrid` 标记。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="cb6aa-136">下面是修改后的标记：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="cb6aa-137">新列如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="cb6aa-138">此列的点用于显示其文本显示为 "编辑" 的链接（`<a>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="cb6aa-139">接下来，我们要创建一个在页面运行时如下所示的链接，每个电影的 `id` 值不同：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="cb6aa-140">此链接将调用名为*EditMovie*的页，并将查询字符串 `?id=7` 传递到该页。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="cb6aa-141">新列的语法可能看起来有点复杂，但这只是因为它将多个元素放在一起。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="cb6aa-142">每个元素都非常简单。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-142">Each individual element is straightforward.</span></span> <span data-ttu-id="cb6aa-143">如果只关注 `<a>` 元素，则会看到以下标记：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="cb6aa-144">有关网格工作方式的一些背景信息：网格显示行，每个数据库记录一个，并显示数据库记录中每个字段的列。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="cb6aa-145">构造每个网格行时，`item` 对象包含该行的数据库记录（item）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="cb6aa-146">这种安排使你可以在代码中获取该行的数据。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="cb6aa-147">这就是你在此处看到的内容：表达式 `item.ID` 正在获取当前数据库项的 ID 值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="cb6aa-148">您可以使用 `item.Title`、`item.Genre`或 `item.Year`以相同的方式获取任何数据库值（标题、流派或年份）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="cb6aa-149">表达式 `"~/EditMovie?id=@item.ID` 将目标 URL 的硬编码部分（`~/EditMovie?id=`）与此动态派生的 ID 组合在一起。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="cb6aa-150">（你在上一教程中看到了 `~` 运算符; 它是表示当前网站根的 ASP.NET 运算符。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="cb6aa-151">结果是，列中的这部分标记只在运行时生成类似于以下标记的内容：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="cb6aa-152">当然，每行 `id` 的实际值将有所不同。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="cb6aa-153">为网格列创建自定义显示</span><span class="sxs-lookup"><span data-stu-id="cb6aa-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="cb6aa-154">现在返回到网格列。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-154">Now back to the grid column.</span></span> <span data-ttu-id="cb6aa-155">网格中最初包含的三个列仅显示数据值（标题、流派和年份）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="cb6aa-156">可以通过传递数据库列的名称来指定此显示 &mdash; 例如 `grid.Column("Title")`。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="cb6aa-157">这一新的**编辑**链接列是不同的。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="cb6aa-158">不指定列名，而是传递 `format` 参数。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="cb6aa-159">此参数可用于定义标记，`WebGrid` 帮助器将呈现这些标记以及 `item` 值，以将列数据显示为粗体或绿色，或采用所需的任何格式。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="cb6aa-160">例如，如果希望标题显示为粗体，则可以创建如下所示的列：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="cb6aa-161">（`format` 属性中所示的各种 `@` 字符标记标记和代码值之间的转换。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="cb6aa-162">了解 `format` 属性后，可以更轻松地了解如何将新的**编辑**链接列组合在一起：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="cb6aa-163">列*只*包含呈现链接的标记，以及从行的数据库记录中提取的某些信息（ID）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="cb6aa-164">**方法的命名参数和位置参数**</span><span class="sxs-lookup"><span data-stu-id="cb6aa-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="cb6aa-165">多次调用方法并向其传递参数时，您只需列出用逗号分隔的参数值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="cb6aa-166">以下为若干示例：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="cb6aa-167">当你首次看到此代码时，我们并没有提到此问题，但在每种情况下，你都按特定顺序向方法传递参数 &mdash; 即，在该方法中定义参数的顺序。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="cb6aa-168">对于 `db.Execute` 和 `Validation.RequireFields`，如果你将传递的值的顺序混合，则在页面运行时将收到一条错误消息，或者至少出现一些奇怪的结果。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="cb6aa-169">显然，您必须知道要在其中传递参数的顺序。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="cb6aa-170">（在 WebMatrix 中，IntelliSense 可帮助你了解参数的名称、类型和顺序。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="cb6aa-171">作为按顺序传递值的替代方法，可以使用*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="cb6aa-172">（按顺序传递参数称为使用*位置参数*。）对于命名参数，在传递参数值时显式包含参数的名称。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="cb6aa-173">在这些教程中已经多次使用了命名参数。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="cb6aa-174">例如:</span><span class="sxs-lookup"><span data-stu-id="cb6aa-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="cb6aa-175">和</span><span class="sxs-lookup"><span data-stu-id="cb6aa-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="cb6aa-176">命名参数对于几种情况非常方便，尤其是在方法需要很多参数时。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="cb6aa-177">一种情况是您希望只传递一个或两个参数，但要传递的值不在参数列表中的第一个位置。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="cb6aa-178">另一种情况是，你希望通过按最适合你的顺序传递参数，使代码更具可读性。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="cb6aa-179">显然，若要使用命名参数，必须知道参数的名称。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="cb6aa-180">WebMatrix IntelliSense 可以*显示*这些名称，但目前无法为您填充这些名称。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>

## <a name="creating-the-edit-page"></a><span data-ttu-id="cb6aa-181">创建编辑页</span><span class="sxs-lookup"><span data-stu-id="cb6aa-181">Creating the Edit Page</span></span>

<span data-ttu-id="cb6aa-182">现在，可以创建*EditMovie*页。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="cb6aa-183">当用户单击 "**编辑**" 链接时，它们将最终出现在此页上。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="cb6aa-184">创建一个名为*EditMovie*的页，并将文件中的内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="cb6aa-185">此标记和代码与你在 " *AddMovie* " 页中的内容类似。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="cb6aa-186">"提交" 按钮的文本有一个小差异。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="cb6aa-187">与*AddMovie*页一样，有一个 `Html.ValidationSummary` 调用会显示验证错误（如果有）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="cb6aa-188">这次我们将 `Validation.Message`调用，因为错误将显示在验证摘要中。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="cb6aa-189">如前面的教程中所述，可以在各种组合中使用验证摘要和各个错误消息。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="cb6aa-190">请再次注意，`<form>` 元素的 `method` 属性设置为 "`post`"。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="cb6aa-191">与*AddMovie*页一样，此页会对数据库进行更改。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="cb6aa-192">因此，此窗体应执行 `POST` 操作。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="cb6aa-193">（有关 `GET` 和 `POST` 操作之间的差异的详细信息，请参阅 HTML 窗体教程中的[GET、POST 和 HTTP Verb 安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)侧栏。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="cb6aa-194">正如您在前面的教程中看到的那样，文本框的 `value` 属性是使用 Razor 代码设置的，以便预先加载它们。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="cb6aa-195">不过，这一次使用的是该任务 `title` 和 `genre` 等变量，而不是 `Request.Form["title"]`：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="cb6aa-196">与之前一样，此标记会将文本框值预加载到电影值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="cb6aa-197">你将会看到，这一次使用变量（而不是使用 `Request` 对象）非常方便。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="cb6aa-198">此页上还有一个 `<input type="hidden">` 元素。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="cb6aa-199">此元素存储影片 ID，而不使其在页面上可见。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="cb6aa-200">该 ID 最初通过使用查询字符串值（`?id=7` 或 URL 中的类似）传递到页面。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="cb6aa-201">如果将 ID 值放在隐藏字段中，则可以确保在提交窗体时它可用，即使您不能再访问调用该页的原始 URL。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="cb6aa-202">与*AddMovie*页不同， *EditMovie*页的代码具有两个不同的函数。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="cb6aa-203">第一种函数是，在第一次显示页面时（*仅限*之后），代码从查询字符串获取影片 ID。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="cb6aa-204">然后，代码使用该 ID 从数据库中读取相应的电影，并在文本框中显示（预加载）该影片。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="cb6aa-205">第二个函数是在用户单击 "**提交更改**" 按钮时，代码必须读取文本框的值并对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="cb6aa-206">此代码还必须用新值更新数据库项。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="cb6aa-207">此方法类似于添加记录，如在*AddMovie*中所见。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="cb6aa-208">添加代码以读取单个电影</span><span class="sxs-lookup"><span data-stu-id="cb6aa-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="cb6aa-209">若要执行第一个函数，请将以下代码添加到页面顶部：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="cb6aa-210">此代码的大部分都位于 `if(!IsPost)`开始的块内。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="cb6aa-211">`!` 运算符表示 "not"，因此，*如果此请求不是 post 提交*（这是一种间接的方式），则表示该请求是*第一次运行此页*时的情况。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="cb6aa-212">如前文所述，此代码*只*应在页面首次运行时运行。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="cb6aa-213">如果未将代码包含在 `if(!IsPost)`中，则每次调用该页时都会运行，无论是第一次还是响应按钮单击。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="cb6aa-214">请注意，此代码包含一个 `else` 块。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="cb6aa-215">正如我们在引入 `if` 块时所说的那样，有时你希望在测试的条件不为 true 时运行备选代码。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="cb6aa-216">这就是这种情况。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-216">That's the case here.</span></span> <span data-ttu-id="cb6aa-217">如果条件通过（即，如果传递到页面的 ID 是 "正常"），则从数据库中读取一行。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="cb6aa-218">但是，如果条件未通过，则运行 `else` 块，代码会设置错误消息。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="cb6aa-219">验证传递到页的值</span><span class="sxs-lookup"><span data-stu-id="cb6aa-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="cb6aa-220">代码使用 `Request.QueryString["id"]` 获取传递到页面的 ID。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="cb6aa-221">此代码可确保已为 ID 实际传递值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="cb6aa-222">如果未传递任何值，则代码将设置一个验证错误。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="cb6aa-223">此代码显示了验证信息的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="cb6aa-224">在上一教程中，您将处理 `Validation` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="cb6aa-225">已注册要验证的字段，并且 ASP.NET 使用 `Html.ValidationMessage` 和 `Html.ValidationSummary`自动执行验证和显示错误。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="cb6aa-226">但在这种情况下，您并未真正验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="cb6aa-227">相反，您要验证从其他位置传递到页面的值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="cb6aa-228">`Validation` 帮助程序不会为你执行此操作。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="cb6aa-229">因此，你可以通过使用 `if(!Request.QueryString["ID"].IsEmpty()`）测试该值来自行检查值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="cb6aa-230">如果出现问题，可以使用 `Html.ValidationSummary`显示错误，就像使用 `Validation` 助手时所做的一样。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="cb6aa-231">为此，请调用 `Validation.AddFormError` 并向其传递要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="cb6aa-232">`Validation.AddFormError` 是一种内置方法，可让你定义自定义消息，将其与已熟悉的验证系统结合使用。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="cb6aa-233">（稍后在本教程中，我们将讨论如何使此验证过程更可靠。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="cb6aa-234">确保为电影提供 ID 后，代码会读取数据库，仅查找单个数据库项。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="cb6aa-235">（您可能已注意到数据库操作的常规模式：打开数据库，定义 SQL 语句，然后运行语句。）此时，SQL `Select` 语句包括 `WHERE ID = @0`。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="cb6aa-236">因为该 ID 是唯一的，所以只能返回一条记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="cb6aa-237">查询是通过使用 `db.QuerySingle` （而不是 `db.Query`用于电影列表）执行的，代码将结果放入 `row` 变量中。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="cb6aa-238">名称 `row` 任意;你可以将变量命名为你喜欢的任何名称。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="cb6aa-239">然后，将用影片详细信息填充顶部初始化的变量，以便这些值可以显示在文本框中。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="cb6aa-240">测试 "编辑" 页（迄今为止）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="cb6aa-241">如果要测试页面，请立即运行*电影*页面，并单击任何电影旁边的 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="cb6aa-242">你将看到 " *EditMovie* " 页，其中显示了所选电影的详细信息：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![显示要编辑的电影的 "编辑电影" 页面](updating-data/_static/image3.png)

<span data-ttu-id="cb6aa-244">请注意，页面的 URL 包含诸如 `?id=10` （或其他数字）之类的内容。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="cb6aa-245">到目前为止，您已经测试了*电影*页面工作中的**编辑**链接，您的页面从查询字符串读取了 ID，并且用于获取单个电影记录的数据库查询正在运行。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="cb6aa-246">您可以更改电影信息，但单击 "**提交更改**" 不会出现任何问题。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="cb6aa-247">添加代码以用用户的更改更新电影</span><span class="sxs-lookup"><span data-stu-id="cb6aa-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="cb6aa-248">在*EditMovie*文件中，若要实现第二个函数（保存更改），请将以下代码添加到 `@` 块的右大括号内。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="cb6aa-249">（如果你不确定在何处放置代码，你可以查看本教程结尾处显示[的 "编辑电影" 页的完整代码列表](#Complete_Page_Listing_for_EditMovie)。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="cb6aa-250">同样，此标记和代码类似于*AddMovie*中的代码。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="cb6aa-251">代码位于 `if(IsPost)` 块中，这是因为仅当用户单击 "**提交更改**" 按钮时才会运行此代码 &mdash; 即，当窗体已发布（且仅当）发布时。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="cb6aa-252">在这种情况下，你未使用类似 `if(IsPost && Validation.IsValid())`的测试，即，你不是使用和来合并这两个测试。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="cb6aa-253">在此页中，您首先确定是否有窗体提交（`if(IsPost)`），并且只注册要验证的字段。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="cb6aa-254">然后，你可以测试验证结果（`if(Validation.IsValid()`）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="cb6aa-255">该流程与*AddMovie*页面略有不同，但效果是相同的。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="cb6aa-256">您可以使用其他 `<input>` 元素 `Request.Form["title"]` 和类似的代码获取文本框的值。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="cb6aa-257">请注意，这一次，代码将获取隐藏字段（`<input type="hidden">`）中的影片 ID。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="cb6aa-258">当页面首次运行时，代码将获取查询字符串的 ID。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="cb6aa-259">从隐藏字段获取值，以确保获得最初显示的电影的 ID （如果自那时起，查询字符串发生了某种形式的更改）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="cb6aa-260">*AddMovie*代码和此代码之间的重要区别在于，在此代码中，你将使用 SQL `Update` 语句，而不是 `Insert Into` 语句。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="cb6aa-261">下面的示例显示 SQL `Update` 语句的语法：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="cb6aa-262">您可以按任意顺序指定任何列，并且在 `Update` 操作期间不必更新每个列。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="cb6aa-263">（您不能更新 ID 本身，因为这样做会有效地将记录保存为新记录，而 `Update` 操作不允许这样做。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cb6aa-264">**重要提示**ID 为的 `Where` 子句非常重要，因为这是数据库了解要更新的数据库记录的方式。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="cb6aa-265">如果离开 `Where` 子句，则数据库将更新数据库中的*每*条记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="cb6aa-266">在大多数情况下，这会是一项灾难。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-266">In most cases, that would be a disaster.</span></span>

<span data-ttu-id="cb6aa-267">在代码中，要更新的值将通过使用占位符传递到 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="cb6aa-268">若要重复之前提到的内容：出于安全原因，*只*使用占位符将值传递给 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="cb6aa-269">代码使用 `db.Execute` 运行 `Update` 语句后，它会重定向回列表页，您可以在其中查看更改。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="cb6aa-270">**不同的 SQL 语句，不同的方法**</span><span class="sxs-lookup"><span data-stu-id="cb6aa-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="cb6aa-271">您可能已注意到，使用略微不同的方法来运行不同的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="cb6aa-272">若要运行可能返回多个记录的 `Select` 查询，请使用 `Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="cb6aa-273">若要运行知道只返回一个数据库项的 `Select` 查询，请使用 `QuerySingle` 方法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="cb6aa-274">若要运行进行更改但不返回数据库项的命令，请使用 `Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="cb6aa-275">你必须具有不同的方法，因为每个方法都会返回不同的结果，因为你已在 `Query` 和 `QuerySingle`之间的差异中看到。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="cb6aa-276">（`Execute` 方法实际上返回一个值，&mdash;，这是受命令影响的数据库行数 &mdash; 但你现在已忽略了。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="cb6aa-277">当然，`Query` 方法可能只返回一个数据库行。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="cb6aa-278">但是，ASP.NET 始终将 `Query` 方法的结果视为集合。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="cb6aa-279">即使此方法只返回一行，也必须从集合中提取该行。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="cb6aa-280">因此，在您*知道*您只收到一行后，使用 `QuerySingle`会更方便一些。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="cb6aa-281">还有其他几种方法可执行特定类型的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="cb6aa-282">可以在 " [ASP.NET 网页 API 快速参考](../../api-reference/asp-net-web-pages-api-reference.md#Data)" 中找到数据库方法的列表。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>

## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="cb6aa-283">使 ID 验证更可靠</span><span class="sxs-lookup"><span data-stu-id="cb6aa-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="cb6aa-284">页面首次运行时，会从查询字符串获取影片 ID，以便可以从数据库中获取该电影。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="cb6aa-285">通过使用以下代码，确保确实存在要查找的值：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="cb6aa-286">你使用此代码来确保，如果用户未在*电影*页面中选择电影就会收到*EditMovies*页面，则页面将显示用户友好的错误消息。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="cb6aa-287">（否则，用户将看到一个错误，可能只是将它们搞糊涂。）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="cb6aa-288">但是，这种验证并不是非常可靠。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="cb6aa-289">还可以通过以下错误调用该页：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="cb6aa-290">ID 不是数字。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-290">The ID isn't a number.</span></span> <span data-ttu-id="cb6aa-291">例如，可以使用 `http://localhost:nnnnn/EditMovie?id=abc`之类的 URL 来调用页。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="cb6aa-292">ID 是一个数字，但它引用了不存在的电影（例如 `http://localhost:nnnnn/EditMovie?id=100934`）。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="cb6aa-293">如果你想要查看这些 Url 导致的错误，请运行*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="cb6aa-294">选择要编辑的电影，然后将 " *EditMovie* " 页的 url 更改为包含字母 ID 的 url 或者不存在的电影的 ID。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="cb6aa-295">那么，您该怎么办呢？</span><span class="sxs-lookup"><span data-stu-id="cb6aa-295">So what should you do?</span></span> <span data-ttu-id="cb6aa-296">第一种解决方法是确保不仅传递到页面的 ID，而且 ID 是整数。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="cb6aa-297">更改 `!IsPost` 测试的代码，使其类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="cb6aa-298">已将第二个条件添加到 `IsEmpty` 测试，并链接到 `&&` （逻辑 AND）：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="cb6aa-299">你可能会注意[到 ASP.NET 网页编程](../introducing-razor-syntax-c.md)教程中所示的方法 `AsBool` `AsInt` 将字符字符串转换为其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="cb6aa-300">`IsInt` 方法（以及其他方法，如 `IsBool` 和 `IsDateTime`）类似。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="cb6aa-301">但是，它们仅测试是否*可以*转换字符串，而不会实际执行转换。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="cb6aa-302">在这里，你实质上是指出*查询字符串值是否可以转换为整数 ...* 。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="cb6aa-303">另一个潜在问题是查找不存在的电影。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="cb6aa-304">用于获取电影的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="cb6aa-305">如果将 `movieId` 值传递到与实际电影不对应的 `QuerySingle` 方法，则不会返回任何内容，后面的语句（例如 `title=row.Title`）将导致错误。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="cb6aa-306">同样，这也是一个简单的修补程序。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-306">Again there's an easy fix.</span></span> <span data-ttu-id="cb6aa-307">如果 `db.QuerySingle` 方法未返回任何结果，则 `row` 变量将为 null。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="cb6aa-308">因此，你可以在尝试从 `row` 变量获取值之前检查该变量是否为 null。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="cb6aa-309">下面的代码在获取 `row` 对象外的值的语句周围添加 `if` 块：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="cb6aa-310">通过这两个额外的验证测试，页面就变得更具项目符号。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="cb6aa-311">`!IsPost` 分支的完整代码现在如下例所示：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="cb6aa-312">请注意，此任务更适合用于 `else` 块。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="cb6aa-313">如果测试未通过，则 `else` 会阻止设置错误消息。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="cb6aa-314">添加链接以返回到电影页面</span><span class="sxs-lookup"><span data-stu-id="cb6aa-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="cb6aa-315">最后和有用的详细信息是将链接添加回*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="cb6aa-316">在普通事件流中，用户将从 "*电影*" 页开始，并单击 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="cb6aa-317">这会将它们带入*EditMovie*页面，用户可以在其中编辑电影并单击按钮。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="cb6aa-318">代码处理更改后，会重定向回*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="cb6aa-319">但是：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-319">However:</span></span>

- <span data-ttu-id="cb6aa-320">用户可能决定不更改任何内容。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="cb6aa-321">用户可能已获得此页面，而没有首先单击*电影*页面中的**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="cb6aa-322">无论采用哪种方式，都要使它们更易于返回到主列表。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="cb6aa-323">这是一个简单的修复 &mdash; 在标记中的结束 `</form>` 标记后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="cb6aa-324">此标记对你在其他地方看到的 `<a>` 元素使用相同的语法。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="cb6aa-325">URL 包括 "网站的根" 这 `~`。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="cb6aa-326">测试电影更新过程</span><span class="sxs-lookup"><span data-stu-id="cb6aa-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="cb6aa-327">现在可以测试了。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-327">Now you can test.</span></span> <span data-ttu-id="cb6aa-328">运行 "*电影*" 页，然后单击电影旁边的 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="cb6aa-329">当 " *EditMovie* " 页出现时，对电影进行更改，然后单击 "**提交更改**"。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="cb6aa-330">显示电影列表时，请确保显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="cb6aa-331">若要确保验证正常工作，请单击 "**编辑**其他电影"。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="cb6aa-332">转到 " *EditMovie* " 页后，请清除 "**流派**" 字段（或 "**年份**" 字段或两者），并尝试提交更改。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="cb6aa-333">您将看到一个错误，如您所料：</span><span class="sxs-lookup"><span data-stu-id="cb6aa-333">You'll see an error, as you'd expect:</span></span>

![显示验证错误的编辑电影页面](updating-data/_static/image4.png)

<span data-ttu-id="cb6aa-335">单击 "**返回到电影列表**" 链接放弃您的更改并返回到*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="cb6aa-336">下一步</span><span class="sxs-lookup"><span data-stu-id="cb6aa-336">Coming Up Next</span></span>

<span data-ttu-id="cb6aa-337">在下一教程中，你将了解如何删除电影记录。</span><span class="sxs-lookup"><span data-stu-id="cb6aa-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="cb6aa-338">完整的电影页面列表（已更新为编辑链接）</span><span class="sxs-lookup"><span data-stu-id="cb6aa-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="cb6aa-339">编辑电影页面的完成页面列表</span><span class="sxs-lookup"><span data-stu-id="cb6aa-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="cb6aa-340">其他资源</span><span class="sxs-lookup"><span data-stu-id="cb6aa-340">Additional Resources</span></span>

- [<span data-ttu-id="cb6aa-341">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="cb6aa-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="cb6aa-342">W3Schools 站点上的[SQL UPDATE 语句](http://www.w3schools.com/sql/sql_update.asp)</span><span class="sxs-lookup"><span data-stu-id="cb6aa-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cb6aa-343">[上一页](entering-data.md)
> [下一页](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="cb6aa-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
