---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: 引入 ASP.NET 网页使用窗体输入数据库数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍如何创建一个条目窗体，然后在使用 ASP.NET 网页（...）时，输入从窗体获取到数据库表中的数据。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506600"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="3ec92-103">引入 ASP.NET 网页使用窗体输入数据库数据</span><span class="sxs-lookup"><span data-stu-id="3ec92-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>

<span data-ttu-id="3ec92-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3ec92-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3ec92-105">本教程介绍如何创建一个条目窗体，然后在使用 ASP.NET 网页（Razor）时，输入从窗体获取到数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="3ec92-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="3ec92-106">它假定您已完成了有关[ASP.NET 网页中的 HTML 窗体的基础知识](https://go.microsoft.com/fwlink/?LinkId=251581)。</span><span class="sxs-lookup"><span data-stu-id="3ec92-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="3ec92-107">学习内容：</span><span class="sxs-lookup"><span data-stu-id="3ec92-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3ec92-108">有关如何处理条目窗体的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="3ec92-109">如何在数据库中添加（插入）数据。</span><span class="sxs-lookup"><span data-stu-id="3ec92-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="3ec92-110">如何确保用户已在表单中输入所需的值（如何验证用户输入）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="3ec92-111">如何显示验证错误。</span><span class="sxs-lookup"><span data-stu-id="3ec92-111">How to display validation errors.</span></span>
> - <span data-ttu-id="3ec92-112">如何从当前页面跳转到另一个页面。</span><span class="sxs-lookup"><span data-stu-id="3ec92-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="3ec92-113">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="3ec92-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="3ec92-114">`Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="3ec92-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="3ec92-115">SQL `Insert Into` 语句</span><span class="sxs-lookup"><span data-stu-id="3ec92-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="3ec92-116">`Validation` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3ec92-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="3ec92-117">`Response.Redirect` 方法。</span><span class="sxs-lookup"><span data-stu-id="3ec92-117">The `Response.Redirect` method.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="3ec92-118">你将生成</span><span class="sxs-lookup"><span data-stu-id="3ec92-118">What You'll Build</span></span>

<span data-ttu-id="3ec92-119">在前面的教程中，介绍了如何创建数据库，通过直接在 WebMatrix 中编辑数据库来输入数据库数据，该数据库在**数据库**工作区中工作。</span><span class="sxs-lookup"><span data-stu-id="3ec92-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="3ec92-120">但在大多数应用中，这并不是将数据放入数据库的实用方法。</span><span class="sxs-lookup"><span data-stu-id="3ec92-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="3ec92-121">在本教程中，您将创建一个基于 web 的界面，使您或任何人都可以输入数据并将其保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="3ec92-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="3ec92-122">你将创建一个可在其中输入新电影的页面。</span><span class="sxs-lookup"><span data-stu-id="3ec92-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="3ec92-123">此页将包含一个输入窗体，其中包含可在其中输入电影标题、流派和年份的字段（文本框）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="3ec92-124">该页将如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-124">The page will look like this page:</span></span>

![浏览器中的 "添加电影" 页面](entering-data/_static/image1.png)

<span data-ttu-id="3ec92-126">文本框将是 HTML `<input>` 元素，这些元素将类似于以下标记：</span><span class="sxs-lookup"><span data-stu-id="3ec92-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="3ec92-127">创建基本条目窗体</span><span class="sxs-lookup"><span data-stu-id="3ec92-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="3ec92-128">创建名为*AddMovie*的页。</span><span class="sxs-lookup"><span data-stu-id="3ec92-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="3ec92-129">将文件中的内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="3ec92-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="3ec92-130">覆盖所有内容;你将很快在顶部添加一个代码块。</span><span class="sxs-lookup"><span data-stu-id="3ec92-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="3ec92-131">此示例演示用于创建窗体的典型 HTML。</span><span class="sxs-lookup"><span data-stu-id="3ec92-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="3ec92-132">它使用文本框和提交按钮 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3ec92-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="3ec92-133">文本框的标题是使用标准 `<label>` 元素创建的。</span><span class="sxs-lookup"><span data-stu-id="3ec92-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="3ec92-134">`<fieldset>` 和 `<legend>` 元素围绕窗体放置了一个不错的框。</span><span class="sxs-lookup"><span data-stu-id="3ec92-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="3ec92-135">请注意，在此页中，`<form>` 元素使用 `post` 作为 `method` 特性的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="3ec92-136">在上一教程中，您创建了一个使用 `get` 方法的窗体。</span><span class="sxs-lookup"><span data-stu-id="3ec92-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="3ec92-137">这是正确的，因为虽然表单已将值提交给服务器，但请求未进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="3ec92-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="3ec92-138">它的所有操作都是以不同的方式获取数据。</span><span class="sxs-lookup"><span data-stu-id="3ec92-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="3ec92-139">但是，在此页中你*将*进行更改，即你要添加新的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="3ec92-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="3ec92-140">因此，此窗体应该使用 `post` 方法。</span><span class="sxs-lookup"><span data-stu-id="3ec92-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="3ec92-141">（有关 `GET` 和 `POST` 操作之间的差异的详细信息，请参阅上一教程中的[GET、POST 和 HTTP Verb 安全](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)侧栏。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="3ec92-142">请注意，每个文本框都有一个 `name` 元素（`title`、`genre``year`）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="3ec92-143">正如你在上一教程中看到的那样，这些名称很重要，因为你必须具有这些名称，以便以后可以获取用户的输入。</span><span class="sxs-lookup"><span data-stu-id="3ec92-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="3ec92-144">您可以使用任何名称。</span><span class="sxs-lookup"><span data-stu-id="3ec92-144">You can use any names.</span></span> <span data-ttu-id="3ec92-145">使用有意义的名称有助于记住正在处理的数据，这会很有帮助。</span><span class="sxs-lookup"><span data-stu-id="3ec92-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="3ec92-146">每个 `<input>` 元素的 `value` 属性包含一个 Razor 代码（例如 `Request.Form["title"]`）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="3ec92-147">在上一教程中，你已学习了此技巧的一个版本，可在提交窗体后保留输入到文本框中的值（如果有）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="3ec92-148">获取窗体值</span><span class="sxs-lookup"><span data-stu-id="3ec92-148">Getting the Form Values</span></span>

<span data-ttu-id="3ec92-149">接下来，添加处理窗体的代码。</span><span class="sxs-lookup"><span data-stu-id="3ec92-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="3ec92-150">在大纲中，你将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3ec92-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="3ec92-151">检查页面是否正在发布（已提交）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="3ec92-152">只需在用户单击该按钮时（而不是在页面首次运行时）运行。</span><span class="sxs-lookup"><span data-stu-id="3ec92-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="3ec92-153">获取用户输入到文本框中的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="3ec92-154">在这种情况下，由于窗体使用的是 `POST` 谓词，因此从 `Request.Form` 集合获取窗体值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="3ec92-155">将值作为新记录插入到*电影*数据库表中。</span><span class="sxs-lookup"><span data-stu-id="3ec92-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="3ec92-156">在该文件的顶部，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="3ec92-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="3ec92-157">前几行创建变量（`title`、`genre`和 `year`）以保存文本框中的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="3ec92-158">行 `if(IsPost)` 确保*只*在用户单击 "**添加电影**" 按钮时（即，在窗体已发布后）设置变量。</span><span class="sxs-lookup"><span data-stu-id="3ec92-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="3ec92-159">正如你在前面的教程中看到的那样，可以使用表达式（如 `Request.Form["name"]`）获取文本框的值，其中*name*是 `<input>` 元素的名称。</span><span class="sxs-lookup"><span data-stu-id="3ec92-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="3ec92-160">变量（`title`、`genre`和 `year`）的名称是任意的。</span><span class="sxs-lookup"><span data-stu-id="3ec92-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="3ec92-161">与分配给 `<input>` 元素的名称类似，你可以随意调用它们。</span><span class="sxs-lookup"><span data-stu-id="3ec92-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="3ec92-162">（变量的名称不必与窗体上 `<input>` 元素的名称属性匹配。）但与 `<input>` 元素一样，可以使用反映它们所包含的数据的变量名称。</span><span class="sxs-lookup"><span data-stu-id="3ec92-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="3ec92-163">编写代码时，一致的名称使你可以更轻松地记住正在处理的数据。</span><span class="sxs-lookup"><span data-stu-id="3ec92-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="3ec92-164">向数据库添加数据</span><span class="sxs-lookup"><span data-stu-id="3ec92-164">Adding Data to the Database</span></span>

<span data-ttu-id="3ec92-165">在刚刚添加的代码块中，只需在 `if` 块的右大括号（`}`）*内*（而不是在代码块内），添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="3ec92-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="3ec92-166">此示例类似于在上一教程中用于提取和显示数据的代码。</span><span class="sxs-lookup"><span data-stu-id="3ec92-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="3ec92-167">以 `db =` 开头的行将打开数据库（与之前一样），下一行将再次定义 SQL 语句，如之前所见。</span><span class="sxs-lookup"><span data-stu-id="3ec92-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="3ec92-168">但这次它定义了 SQL `Insert Into` 语句。</span><span class="sxs-lookup"><span data-stu-id="3ec92-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="3ec92-169">下面的示例显示了 `Insert Into` 语句的常规语法：</span><span class="sxs-lookup"><span data-stu-id="3ec92-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="3ec92-170">换句话说，您可以指定要插入的表，然后列出要插入的列，然后列出要插入的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="3ec92-171">（如前所述，SQL 不区分大小写，但有些人会将关键字改为大写，以便更轻松地读取命令。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="3ec92-172">要插入的列已在命令中列出，`(Title, Genre, Year)`。</span><span class="sxs-lookup"><span data-stu-id="3ec92-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="3ec92-173">有趣的部分是如何将文本框中的值获取到命令的 `VALUES` 部分。</span><span class="sxs-lookup"><span data-stu-id="3ec92-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="3ec92-174">您看到的是 `@0`、`@1`和 `@2`，而不是实际值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="3ec92-175">运行命令时（在 "`db.Execute`" 行中），将从文本框中传递所获得的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="3ec92-176">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="3ec92-176">**Important!**</span></span> <span data-ttu-id="3ec92-177">请记住，你只应在 SQL 语句中包括用户在线输入的数据的唯一方法是使用占位符，如此处所示（`VALUES(@0, @1, @2)`）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="3ec92-178">如果将用户输入连接到 SQL 语句，会自行打开 SQL 注入式攻击，如 ASP.NET 网页（上一教程）[中的窗体基础](https://go.microsoft.com/fwlink/?LinkId=251581)中所述。</span><span class="sxs-lookup"><span data-stu-id="3ec92-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="3ec92-179">在 `if` 块中，在 `db.Execute` 行后面添加以下行：</span><span class="sxs-lookup"><span data-stu-id="3ec92-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="3ec92-180">将新电影插入到数据库后，此线将跳转到 "*电影*" 页，以便您可以看到刚刚输入的影片。</span><span class="sxs-lookup"><span data-stu-id="3ec92-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="3ec92-181">`~` 运算符表示 "网站的根"。</span><span class="sxs-lookup"><span data-stu-id="3ec92-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="3ec92-182">（`~` 运算符仅适用于 ASP.NET 页面，而不能在 HTML 中使用。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="3ec92-183">完整的代码块如下例所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="3ec92-184">测试插入命令（迄今为止）</span><span class="sxs-lookup"><span data-stu-id="3ec92-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="3ec92-185">尚未完成，但现在是一个好的测试时间。</span><span class="sxs-lookup"><span data-stu-id="3ec92-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="3ec92-186">在 WebMatrix 中文件的树状视图中，右键单击 " *AddMovie* " 页，然后单击 "**在浏览器中启动**"。</span><span class="sxs-lookup"><span data-stu-id="3ec92-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![浏览器中的 "添加电影" 页面](entering-data/_static/image2.png)

<span data-ttu-id="3ec92-188">（如果你在浏览器中结束了不同的页面，请确保 URL `http://localhost:nnnnn/AddMovie`），其中*nnnnn*是你正在使用的端口号。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="3ec92-189">您是否收到错误页？</span><span class="sxs-lookup"><span data-stu-id="3ec92-189">Did you get an error page?</span></span> <span data-ttu-id="3ec92-190">如果是这样，请仔细阅读并确保代码看起来与前面列出的内容完全相同。</span><span class="sxs-lookup"><span data-stu-id="3ec92-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="3ec92-191">以格式输入电影 &mdash; 例如，使用 "公民 Kane"、"Drama" 和 "1941"。</span><span class="sxs-lookup"><span data-stu-id="3ec92-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="3ec92-192">（或任何其他内容）然后单击 "**添加电影**"。</span><span class="sxs-lookup"><span data-stu-id="3ec92-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="3ec92-193">如果一切顺利，您会被重定向到*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="3ec92-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="3ec92-194">请确保您的新电影已列出。</span><span class="sxs-lookup"><span data-stu-id="3ec92-194">Make sure that your new movie is listed.</span></span>

![显示新添加的电影的电影页面](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="3ec92-196">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="3ec92-196">Validating User Input</span></span>

<span data-ttu-id="3ec92-197">返回到*AddMovie*页，或再次运行它。</span><span class="sxs-lookup"><span data-stu-id="3ec92-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="3ec92-198">输入其他电影，但这次仅输入标题 &mdash; 例如，输入 "Singin' in Rain"。</span><span class="sxs-lookup"><span data-stu-id="3ec92-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="3ec92-199">然后单击 "**添加电影**"。</span><span class="sxs-lookup"><span data-stu-id="3ec92-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="3ec92-200">你将再次重定向到*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="3ec92-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="3ec92-201">您可以找到新电影，但它不完整。</span><span class="sxs-lookup"><span data-stu-id="3ec92-201">You can find the new movie, but it's incomplete.</span></span>

![显示缺少某些值的新电影的电影页面](entering-data/_static/image4.png)

<span data-ttu-id="3ec92-203">当您创建了*电影*表时，您显式地说没有任何字段可以为 null。</span><span class="sxs-lookup"><span data-stu-id="3ec92-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="3ec92-204">这里有一个新电影的输入窗体，并将字段留空。</span><span class="sxs-lookup"><span data-stu-id="3ec92-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="3ec92-205">这是个错误。</span><span class="sxs-lookup"><span data-stu-id="3ec92-205">That's an error.</span></span>

<span data-ttu-id="3ec92-206">在这种情况下，数据库不会实际引发（或*引发*）错误。</span><span class="sxs-lookup"><span data-stu-id="3ec92-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="3ec92-207">你未提供流派或年份，因此*AddMovie*页中的代码将这些值视为所谓的*空字符串*。</span><span class="sxs-lookup"><span data-stu-id="3ec92-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="3ec92-208">当 SQL `Insert Into` 命令运行时，"流派" 和 "年份" 字段在其中没有有用的数据，但是它们不是 null。</span><span class="sxs-lookup"><span data-stu-id="3ec92-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="3ec92-209">很显然，您不想让用户在数据库中输入半空电影信息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="3ec92-210">解决方案是验证用户的输入。</span><span class="sxs-lookup"><span data-stu-id="3ec92-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="3ec92-211">最初，验证只需确保用户输入了所有字段的值（即，它们都不包含空字符串）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP]
> 
> <span data-ttu-id="3ec92-212">**Null 和空字符串**</span><span class="sxs-lookup"><span data-stu-id="3ec92-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="3ec92-213">在编程中，"无值" 的不同概念之间存在差异。</span><span class="sxs-lookup"><span data-stu-id="3ec92-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="3ec92-214">通常，如果从未以任何方式对其进行设置或初始化，则该值为*null* 。</span><span class="sxs-lookup"><span data-stu-id="3ec92-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="3ec92-215">相反，需要字符数据（字符串）的变量可以设置为*空字符串*。</span><span class="sxs-lookup"><span data-stu-id="3ec92-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="3ec92-216">在这种情况下，值不为 null;它只是显式设置为长度为零的字符字符串。</span><span class="sxs-lookup"><span data-stu-id="3ec92-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="3ec92-217">这两个语句显示了差异：</span><span class="sxs-lookup"><span data-stu-id="3ec92-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="3ec92-218">这有点复杂，但要点是 `null` 表示一种不确定的状态。</span><span class="sxs-lookup"><span data-stu-id="3ec92-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="3ec92-219">现在，必须准确了解某个值为 null 时，以及何时只是一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="3ec92-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="3ec92-220">在*AddMovie*页的代码中，可以使用 `Request.Form["title"]` 等来获取文本框的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="3ec92-221">首次运行页面时（在单击按钮之前），`Request.Form["title"]` 的值为 null。</span><span class="sxs-lookup"><span data-stu-id="3ec92-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="3ec92-222">但在提交窗体时，`Request.Form["title"]` 获取 `title` 文本框的值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="3ec92-223">这并不明显，但空文本框不是 null;它中只包含一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="3ec92-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="3ec92-224">因此，当运行代码以响应按钮单击时，`Request.Form["title"]` 在其中包含空字符串。</span><span class="sxs-lookup"><span data-stu-id="3ec92-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="3ec92-225">为什么此项区分非常重要？</span><span class="sxs-lookup"><span data-stu-id="3ec92-225">Why is this distinction important?</span></span> <span data-ttu-id="3ec92-226">当您创建了*电影*表时，您显式地说没有任何字段可以为 null。</span><span class="sxs-lookup"><span data-stu-id="3ec92-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="3ec92-227">但这里有一个新电影的输入窗体，而您会将字段留空。</span><span class="sxs-lookup"><span data-stu-id="3ec92-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="3ec92-228">当您尝试保存没有流派或年份值的新电影时，您可能希望数据库产生抱怨。</span><span class="sxs-lookup"><span data-stu-id="3ec92-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="3ec92-229">但这也是 &mdash; 即使将这些文本框留空也是如此，这些值不是 null;它们是空字符串。</span><span class="sxs-lookup"><span data-stu-id="3ec92-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="3ec92-230">因此，您可以将新电影保存到数据库中，其中，这些列为空 &mdash; 但不是 null！</span><span class="sxs-lookup"><span data-stu-id="3ec92-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="3ec92-231">&mdash; 值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-231">&mdash; values.</span></span> <span data-ttu-id="3ec92-232">因此，你必须确保用户不会提交空字符串，你可以通过验证用户的输入来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="3ec92-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>

### <a name="the-validation-helper"></a><span data-ttu-id="3ec92-233">验证帮助器</span><span class="sxs-lookup"><span data-stu-id="3ec92-233">The Validation Helper</span></span>

<span data-ttu-id="3ec92-234">ASP.NET 网页包含了帮助程序 &mdash; `Validation` 的帮助器 &mdash;，可用于确保用户输入满足你的要求的数据。</span><span class="sxs-lookup"><span data-stu-id="3ec92-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="3ec92-235">`Validation` 帮助器是内置于 ASP.NET 网页的帮助器之一，因此您无需使用 NuGet 将其作为包安装，这是在前面的教程中安装 Gravatar helper 的方式。</span><span class="sxs-lookup"><span data-stu-id="3ec92-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="3ec92-236">若要验证用户的输入，你需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3ec92-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="3ec92-237">使用代码指定希望在页的文本框中需要值。</span><span class="sxs-lookup"><span data-stu-id="3ec92-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="3ec92-238">将测试放入代码，以便仅当所有内容都得到正确验证时才将电影信息添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="3ec92-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="3ec92-239">向标记添加代码以显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="3ec92-240">在*AddMovie*页的代码块中，在变量声明之前的顶部，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="3ec92-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="3ec92-241">对于要在其中需要输入的每个字段（`<input>` 元素），只需调用一次 `Validation.RequireField`。</span><span class="sxs-lookup"><span data-stu-id="3ec92-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="3ec92-242">你还可以为每个调用添加自定义错误消息，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3ec92-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="3ec92-243">（我们只是为了显示您可以放入您的内容。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="3ec92-244">如果出现问题，则需要防止将新的电影信息插入到数据库中。</span><span class="sxs-lookup"><span data-stu-id="3ec92-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="3ec92-245">在 `if(IsPost)` 块中，使用 `&&` （逻辑 AND）添加另一个测试 `Validation.IsValid()`的条件。</span><span class="sxs-lookup"><span data-stu-id="3ec92-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="3ec92-246">完成后，整个 `if(IsPost)` 块如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="3ec92-247">如果使用 `Validation` 帮助程序注册的任何字段存在验证错误，则 `Validation.IsValid` 方法返回 false。</span><span class="sxs-lookup"><span data-stu-id="3ec92-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="3ec92-248">在这种情况下，该块中的任何代码都不会运行，因此不会在数据库中插入无效的电影条目。</span><span class="sxs-lookup"><span data-stu-id="3ec92-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="3ec92-249">当然，您不会重定向到*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="3ec92-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="3ec92-250">完整的代码块，包括验证代码，现在如下例所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="3ec92-251">显示验证错误</span><span class="sxs-lookup"><span data-stu-id="3ec92-251">Displaying Validation Errors</span></span>

<span data-ttu-id="3ec92-252">最后一步是显示任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-252">The last step is to display any error messages.</span></span> <span data-ttu-id="3ec92-253">可以为每个验证错误显示单独的消息，也可以显示摘要或同时显示两者。</span><span class="sxs-lookup"><span data-stu-id="3ec92-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="3ec92-254">在本教程中，您将执行这两项操作，以便您可以看到它的工作原理。</span><span class="sxs-lookup"><span data-stu-id="3ec92-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="3ec92-255">在要验证的每个 `<input>` 元素旁边，调用 `Html.ValidationMessage` 方法并向其传递要验证的 `<input>` 元素的名称。</span><span class="sxs-lookup"><span data-stu-id="3ec92-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="3ec92-256">将 `Html.ValidationMessage` 方法放在要显示错误消息的位置。</span><span class="sxs-lookup"><span data-stu-id="3ec92-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="3ec92-257">当页面运行时，`Html.ValidationMessage` 方法将呈现验证错误将呈现的 `<span>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3ec92-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="3ec92-258">（如果没有错误，则会呈现 `<span>` 元素，但其中没有任何文本。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="3ec92-259">更改页面中的标记，使其包含页面上三个 `<input>` 元素的 `Html.ValidationMessage` 方法，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="3ec92-260">若要查看摘要的工作原理，还应在页面上的 `<h1>Add a Movie</h1>` 元素之后添加以下标记和代码：</span><span class="sxs-lookup"><span data-stu-id="3ec92-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="3ec92-261">默认情况下，`Html.ValidationSummary` 方法将在列表中显示所有验证消息（在 `<div>` 元素内的 `<ul>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="3ec92-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="3ec92-262">与 `Html.ValidationMessage` 方法一样，验证摘要的标记始终呈现;如果没有错误，则不会呈现列表项。</span><span class="sxs-lookup"><span data-stu-id="3ec92-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="3ec92-263">摘要可以是显示验证消息的另一种方法，而不是使用 `Html.ValidationMessage` 方法来显示每个特定于字段的错误。</span><span class="sxs-lookup"><span data-stu-id="3ec92-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="3ec92-264">或者，您可以使用摘要和详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="3ec92-265">或者，您可以使用 `Html.ValidationSummary` 方法来显示一般错误，然后使用各个 `Html.ValidationMessage` 调用来显示详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="3ec92-266">完整的页现在如下例所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="3ec92-267">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="3ec92-267">That's it.</span></span> <span data-ttu-id="3ec92-268">现在可以通过添加电影来测试页面，但要保留一个或多个字段。</span><span class="sxs-lookup"><span data-stu-id="3ec92-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="3ec92-269">当你执行此操作时，将看到以下错误显示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-269">When you do, you see the following error display:</span></span>

![添加显示验证错误消息的电影页面](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="3ec92-271">设置验证错误消息的样式</span><span class="sxs-lookup"><span data-stu-id="3ec92-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="3ec92-272">您可以看到存在错误消息，但它们并不是很好。</span><span class="sxs-lookup"><span data-stu-id="3ec92-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="3ec92-273">不过，有一种简单的方法可以对错误消息进行样式。</span><span class="sxs-lookup"><span data-stu-id="3ec92-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="3ec92-274">若要为 `Html.ValidationMessage`显示的各个错误消息建立样式，请创建一个名为 `field-validation-error`的 CSS 样式类。</span><span class="sxs-lookup"><span data-stu-id="3ec92-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="3ec92-275">若要定义验证摘要的外观，请创建一个名为 `validation-summary-errors`的 CSS 样式类。</span><span class="sxs-lookup"><span data-stu-id="3ec92-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="3ec92-276">若要查看此方法的工作方式，请在页面的 `<head>` 部分中添加一个 `<style>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3ec92-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="3ec92-277">然后，定义名为 `field-validation-error` 的样式类和包含以下规则的 `validation-summary-errors`：</span><span class="sxs-lookup"><span data-stu-id="3ec92-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="3ec92-278">通常，您可能会将样式信息放在单独的 *.css*文件中，但为了简单起见，您现在可以将其放在页面中。</span><span class="sxs-lookup"><span data-stu-id="3ec92-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="3ec92-279">（在本教程的后面部分中，您将 CSS 规则移到单独的 *.css*文件中。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="3ec92-280">如果存在验证错误，`Html.ValidationMessage` 方法将呈现包含 `class="field-validation-error"`的 `<span>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3ec92-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="3ec92-281">通过添加该类的样式定义，可以配置消息的外观。</span><span class="sxs-lookup"><span data-stu-id="3ec92-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="3ec92-282">如果有错误，`ValidationSummary` 方法同样会动态呈现特性 `class="validation-summary-errors"`。</span><span class="sxs-lookup"><span data-stu-id="3ec92-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="3ec92-283">再次运行该页，并特意忽略几个字段。</span><span class="sxs-lookup"><span data-stu-id="3ec92-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="3ec92-284">现在，这些错误比较明显。</span><span class="sxs-lookup"><span data-stu-id="3ec92-284">The errors are now more noticeable.</span></span> <span data-ttu-id="3ec92-285">（实际上，它们是 overdone 的，但这只是为了显示您可以执行的操作。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![添加显示已设置样式的验证错误的电影页面](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="3ec92-287">添加电影页面的链接</span><span class="sxs-lookup"><span data-stu-id="3ec92-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="3ec92-288">最后一步是让从原始电影列表访问*AddMovie*页面变得非常方便。</span><span class="sxs-lookup"><span data-stu-id="3ec92-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="3ec92-289">再次打开*电影*页面。</span><span class="sxs-lookup"><span data-stu-id="3ec92-289">Open the *Movies* page again.</span></span> <span data-ttu-id="3ec92-290">在 `WebGrid` 助手后面的结束 `</div>` 标记后，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="3ec92-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="3ec92-291">如前文所述，ASP.NET 会将 `~` 运算符解释为网站的根。</span><span class="sxs-lookup"><span data-stu-id="3ec92-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="3ec92-292">无需使用 `~` 运算符;您可以使用标记 `<a href="./AddMovie">Add a movie</a>` 或其他方式来定义 HTML 理解的路径。</span><span class="sxs-lookup"><span data-stu-id="3ec92-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="3ec92-293">但是，当你为 Razor 页面创建链接时，`~` 运算符是一种很好的通用方法，因为它使站点更灵活-如果将当前页移动到子文件夹，则该链接仍将转到*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="3ec92-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="3ec92-294">（请记住，`~` 运算符仅适用于*cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="3ec92-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="3ec92-295">ASP.NET 理解它，但它不是标准 HTML。）</span><span class="sxs-lookup"><span data-stu-id="3ec92-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="3ec92-296">完成后，运行 "*电影*" 页。</span><span class="sxs-lookup"><span data-stu-id="3ec92-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="3ec92-297">它将如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ec92-297">It will look like this page:</span></span>

![链接到 "添加电影" 页面的电影页面](entering-data/_static/image7.png)

<span data-ttu-id="3ec92-299">单击 "**添加电影**" 链接，确保它转到*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="3ec92-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="3ec92-300">下一步</span><span class="sxs-lookup"><span data-stu-id="3ec92-300">Coming Up Next</span></span>

<span data-ttu-id="3ec92-301">在下一教程中，您将学习如何允许用户编辑数据库中已有的数据。</span><span class="sxs-lookup"><span data-stu-id="3ec92-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="3ec92-302">AddMovie 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="3ec92-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="3ec92-303">其他资源</span><span class="sxs-lookup"><span data-stu-id="3ec92-303">Additional Resources</span></span>

- [<span data-ttu-id="3ec92-304">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="3ec92-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="3ec92-305">W3Schools 站点上的[SQL INSERT INTO 语句](http://www.w3schools.com/sql/sql_insert.asp)</span><span class="sxs-lookup"><span data-stu-id="3ec92-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="3ec92-306">[验证 ASP.NET 网页站点中的用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)。</span><span class="sxs-lookup"><span data-stu-id="3ec92-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="3ec92-307">有关使用 `Validation` 帮助程序的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ec92-307">More information about working with the `Validation` helper.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3ec92-308">[上一页](form-basics.md)
> [下一页](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="3ec92-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
