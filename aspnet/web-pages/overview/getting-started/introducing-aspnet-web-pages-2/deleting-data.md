---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: 介绍 ASP.NET 网页-删除数据库数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍如何删除单个数据库条目。 本文假设已完成在 ASP.NET Web Pa 中更新数据库数据的系列 。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510458"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="9bc3c-104">ASP.NET 网页-删除数据库数据简介</span><span class="sxs-lookup"><span data-stu-id="9bc3c-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="9bc3c-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9bc3c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9bc3c-106">本教程介绍如何删除单个数据库条目。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="9bc3c-107">它假定您已完成了[在 ASP.NET 网页中更新数据库数据](updating-data.md)的系列。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="9bc3c-108">学习内容：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9bc3c-109">如何从记录列表中选择单个记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="9bc3c-110">如何从数据库中删除单个记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="9bc3c-111">如何检查是否已在窗体中单击了特定按钮。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="9bc3c-112">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="9bc3c-113">`WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="9bc3c-114">SQL `Delete` 命令。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="9bc3c-115">用于运行 SQL `Delete` 命令的 `Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="9bc3c-116">你将生成</span><span class="sxs-lookup"><span data-stu-id="9bc3c-116">What You'll Build</span></span>

<span data-ttu-id="9bc3c-117">在上一教程中，您学习了如何更新现有的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="9bc3c-118">此教程与此类似，不同之处在于，它不会更新记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="9bc3c-119">这些过程是相同的，只是删除操作更简单，因此本教程将简短。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="9bc3c-120">在 "*电影*" 页面中，你将更新 `WebGrid` 帮助程序，以便它在每个电影旁显示一个 "**删除**" 链接，以附带你之前添加的 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![显示每个电影的删除链接的电影页面](deleting-data/_static/image1.png)

<span data-ttu-id="9bc3c-122">对于编辑，单击 "**删除**" 链接时，将转到不同的页面，其中的影片信息已在表单中：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![使用显示的电影删除电影页面](deleting-data/_static/image2.png)

<span data-ttu-id="9bc3c-124">然后，您可以单击该按钮以永久删除该记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="9bc3c-125">向电影列表添加 "删除" 链接</span><span class="sxs-lookup"><span data-stu-id="9bc3c-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="9bc3c-126">首先，将 "**删除**" 链接添加到 `WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="9bc3c-127">此链接类似于在上一教程中添加的 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="9bc3c-128">打开*电影. cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="9bc3c-129">通过添加列来更改页面正文中的 `WebGrid` 标记。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="9bc3c-130">下面是修改后的标记：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="9bc3c-131">新列如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="9bc3c-132">网格的配置方式，网格中的 "**编辑**" 列最左侧，"**删除**" 列最右侧。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="9bc3c-133">（现在在 `Year` 列后有一个逗号，以防您没有注意到。）这些链接列的位置没有什么特别之处，您可以轻松地将它们放在一起。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="9bc3c-134">在这种情况下，它们是独立的，使其难以混淆。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![已标记为 "编辑" 和 "详细信息" 链接的电影页面，显示它们不是相邻的](deleting-data/_static/image3.png)

<span data-ttu-id="9bc3c-136">新列显示其文本显示为 "删除" 的链接（`<a>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="9bc3c-137">链接的目标（其 `href` 特性）是最终解析为类似于此 URL 的内容的代码，每个电影的 `id` 值不同：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="9bc3c-138">此链接将调用名为*DeleteMovie*的页面，并向其传递所选电影的 ID。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="9bc3c-139">本教程不会详细介绍如何构造此链接，因为它与上一教程中的 "**编辑**" 链接（[更新 ASP.NET 网页中的数据库数据](updating-data.md)）几乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="9bc3c-140">创建 "删除" 页</span><span class="sxs-lookup"><span data-stu-id="9bc3c-140">Creating the Delete Page</span></span>

<span data-ttu-id="9bc3c-141">现在，你可以创建将作为网格中 "**删除**" 链接的目标的页面。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9bc3c-142">**重要提示**第一种方法是先选择要删除的记录，然后使用单独的页面和按钮来确认该过程对于安全性极其重要。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="9bc3c-143">如您在前面的教程中所述，对您的网站进行*任何*更改都应*始终*使用窗体 &mdash; 就是使用 HTTP POST 操作。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="9bc3c-144">如果你只是通过单击链接（即使用 GET 操作）来更改站点，则用户可能会对你的站点发出简单的请求并删除数据。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="9bc3c-145">即使是对你的站点进行索引的搜索引擎爬网程序，也可能会无意中通过以下链接删除数据。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="9bc3c-146">当你的应用程序允许用户更改记录时，你必须向用户提供记录以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="9bc3c-147">但你可能想跳过此步骤来删除记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="9bc3c-148">不过，请不要跳过该步骤。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-148">Don't skip that step, though.</span></span> <span data-ttu-id="9bc3c-149">（这也有助于用户查看记录并确认他们正在删除所需的记录。）</span><span class="sxs-lookup"><span data-stu-id="9bc3c-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="9bc3c-150">在后续教程中，你将了解如何添加登录功能，以便用户必须在删除记录前登录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="9bc3c-151">创建一个名为*DeleteMovie*的页，并将文件中的内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="9bc3c-152">此标记类似于*EditMovie*页，不同之处`<input type="text">`在于标记包含 `<span>` 元素。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="9bc3c-153">这里没有任何要编辑的内容。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-153">There's nothing here to edit.</span></span> <span data-ttu-id="9bc3c-154">您所要做的只是显示电影详细信息，以便用户可以确保正在删除正确的电影。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="9bc3c-155">标记已经包含一个链接，该链接使用户能够返回到电影列表页。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="9bc3c-156">在*EditMovie*页中，所选电影的 ID 存储在隐藏字段中。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="9bc3c-157">（它在第一个位置作为查询字符串值传递到页中。）有一个 `Html.ValidationSummary` 调用会显示验证错误。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="9bc3c-158">在这种情况下，此错误可能是没有电影 ID 传递到页面，或者电影 ID 无效。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="9bc3c-159">如果在未首先在*电影*页面中选择电影的情况下运行此页，则可能会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="9bc3c-160">按钮标题为**删除电影**，其 name 属性设置为 `buttonDelete`。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="9bc3c-161">将在代码中使用 `name` 特性来标识提交窗体的按钮。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="9bc3c-162">需要将代码写入1）在页面第一次显示时读取电影详细信息，2）在用户单击按钮时实际删除影片。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="9bc3c-163">添加代码以读取单个电影</span><span class="sxs-lookup"><span data-stu-id="9bc3c-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="9bc3c-164">在*DeleteMovie*页的顶部，添加以下代码块：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="9bc3c-165">此标记与*EditMovie*页面中对应的代码相同。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="9bc3c-166">它从查询字符串获取影片 ID 并使用该 ID 从数据库中读取记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="9bc3c-167">此代码包括验证测试（`IsInt()` 和 `row != null`），以确保传递给页面的电影 ID 有效。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="9bc3c-168">请记住，此代码只应在页面首次运行时运行。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="9bc3c-169">当用户单击 "**删除电影**" 按钮时，不希望从数据库重新读取电影记录。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="9bc3c-170">因此，*如果请求不是 post 操作（窗体提交）* ，则读取电影的代码会在测试中显示 `if(!IsPost)` &mdash;。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="9bc3c-171">添加代码以删除所选电影</span><span class="sxs-lookup"><span data-stu-id="9bc3c-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="9bc3c-172">若要在用户单击按钮时删除电影，请将以下代码添加到 `@` 块的右大括号内：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="9bc3c-173">此代码类似于用于更新现有记录但更简单的代码。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="9bc3c-174">此代码基本运行 SQL `Delete` 语句。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="9bc3c-175">在*EditMovie*页中，代码位于 `if(IsPost)` 块中。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="9bc3c-176">这一次，`if()` 条件稍微复杂一些：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="9bc3c-177">这里有两种情况。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-177">There are two conditions here.</span></span> <span data-ttu-id="9bc3c-178">第一种是提交页面，正如您在 &mdash; `if(IsPost)`之前所看到的那样。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="9bc3c-179">第二个条件是 `!Request["buttonDelete"].IsEmpty()`，这意味着请求具有一个名为 `buttonDelete`的对象。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="9bc3c-180">无可否认，它是测试提交窗体的按钮的间接方法。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="9bc3c-181">如果窗体包含多个提交按钮，则只会在请求中显示所单击按钮的名称。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="9bc3c-182">因此，如果特定按钮的名称显示在请求中 &mdash; 或如代码中所述，如果该按钮不为空 &mdash; 则为提交窗体的按钮。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="9bc3c-183">`&&` 运算符表示 "and" （逻辑 AND）。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="9bc3c-184">因此，整个 `if` 条件为 。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="9bc3c-185">*此请求为 post （不是第一次请求）*</span><span class="sxs-lookup"><span data-stu-id="9bc3c-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="9bc3c-186">AND</span><span class="sxs-lookup"><span data-stu-id="9bc3c-186">AND</span></span>  
  
<span data-ttu-id="9bc3c-187">*"`buttonDelete`"* *按钮是提交窗体的按钮。*</span><span class="sxs-lookup"><span data-stu-id="9bc3c-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="9bc3c-188">此窗体（事实上，此页）只包含一个按钮，因此，从技术上讲，不需要对 `buttonDelete` 进行其他测试。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="9bc3c-189">但仍需执行将永久删除数据的操作。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="9bc3c-190">因此，您需要确保仅在用户显式请求操作时执行操作。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="9bc3c-191">例如，假设你稍后展开此页面，并向其添加了其他按钮。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="9bc3c-192">即使这样，仅当单击 "`buttonDelete`" 按钮时，删除电影的代码才会运行。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="9bc3c-193">在*EditMovie*页中，从隐藏的字段获取 ID，然后运行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="9bc3c-194">`Delete` 语句的语法为：</span><span class="sxs-lookup"><span data-stu-id="9bc3c-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="9bc3c-195">包括 `WHERE` 子句和 ID 是至关重要的。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="9bc3c-196">如果省略 WHERE 子句，*将删除表中的所有记录*。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="9bc3c-197">如您所见，您可以使用占位符将 ID 值传递到 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="9bc3c-198">测试电影删除过程</span><span class="sxs-lookup"><span data-stu-id="9bc3c-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="9bc3c-199">现在可以测试了。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-199">Now you can test.</span></span> <span data-ttu-id="9bc3c-200">运行 "*电影*" 页，然后单击电影旁边的 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="9bc3c-201">出现 " *DeleteMovie* " 页后，单击 "**删除电影**"。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![突出显示 "删除电影" 按钮的 "删除电影" 页面](deleting-data/_static/image4.png)

<span data-ttu-id="9bc3c-203">单击该按钮时，该代码将删除影片并返回到电影列表。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="9bc3c-204">可以在其中搜索已删除的电影，并确认已将其删除。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="9bc3c-205">下一步</span><span class="sxs-lookup"><span data-stu-id="9bc3c-205">Coming Up Next</span></span>

<span data-ttu-id="9bc3c-206">下一教程介绍如何为网站上的所有页面生成常见的外观和布局。</span><span class="sxs-lookup"><span data-stu-id="9bc3c-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="9bc3c-207">完整的电影页面列表（已更新为删除链接）</span><span class="sxs-lookup"><span data-stu-id="9bc3c-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="9bc3c-208">DeleteMovie 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="9bc3c-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="9bc3c-209">其他资源</span><span class="sxs-lookup"><span data-stu-id="9bc3c-209">Additional Resources</span></span>

- [<span data-ttu-id="9bc3c-210">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="9bc3c-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="9bc3c-211">W3Schools 站点上的[SQL DELETE 语句](http://www.w3schools.com/sql/sql_delete.asp)</span><span class="sxs-lookup"><span data-stu-id="9bc3c-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9bc3c-212">[上一页](updating-data.md)
> [下一页](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="9bc3c-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
