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
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>引入 ASP.NET 网页使用窗体输入数据库数据

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程介绍如何创建一个条目窗体，然后在使用 ASP.NET 网页（Razor）时，输入从窗体获取到数据库表中的数据。 它假定您已完成了有关[ASP.NET 网页中的 HTML 窗体的基础知识](https://go.microsoft.com/fwlink/?LinkId=251581)。
> 
> 学习内容：
> 
> - 有关如何处理条目窗体的详细信息。
> - 如何在数据库中添加（插入）数据。
> - 如何确保用户已在表单中输入所需的值（如何验证用户输入）。
> - 如何显示验证错误。
> - 如何从当前页面跳转到另一个页面。
>   
> 
> 介绍的功能/技术：
> 
> - `Database.Execute` 方法。
> - SQL `Insert Into` 语句
> - `Validation` 帮助程序。
> - `Response.Redirect` 方法。

## <a name="what-youll-build"></a>你将生成

在前面的教程中，介绍了如何创建数据库，通过直接在 WebMatrix 中编辑数据库来输入数据库数据，该数据库在**数据库**工作区中工作。 但在大多数应用中，这并不是将数据放入数据库的实用方法。 在本教程中，您将创建一个基于 web 的界面，使您或任何人都可以输入数据并将其保存到数据库中。

你将创建一个可在其中输入新电影的页面。 此页将包含一个输入窗体，其中包含可在其中输入电影标题、流派和年份的字段（文本框）。 该页将如下所示：

![浏览器中的 "添加电影" 页面](entering-data/_static/image1.png)

文本框将是 HTML `<input>` 元素，这些元素将类似于以下标记：

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>创建基本条目窗体

创建名为*AddMovie*的页。

将文件中的内容替换为以下标记。 覆盖所有内容;你将很快在顶部添加一个代码块。

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

此示例演示用于创建窗体的典型 HTML。 它使用文本框和提交按钮 `<input>` 元素。 文本框的标题是使用标准 `<label>` 元素创建的。 `<fieldset>` 和 `<legend>` 元素围绕窗体放置了一个不错的框。

请注意，在此页中，`<form>` 元素使用 `post` 作为 `method` 特性的值。 在上一教程中，您创建了一个使用 `get` 方法的窗体。 这是正确的，因为虽然表单已将值提交给服务器，但请求未进行任何更改。 它的所有操作都是以不同的方式获取数据。 但是，在此页中你*将*进行更改，即你要添加新的数据库记录。 因此，此窗体应该使用 `post` 方法。 （有关 `GET` 和 `POST` 操作之间的差异的详细信息，请参阅上一教程中的[GET、POST 和 HTTP Verb 安全](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)侧栏。）

请注意，每个文本框都有一个 `name` 元素（`title`、`genre``year`）。 正如你在上一教程中看到的那样，这些名称很重要，因为你必须具有这些名称，以便以后可以获取用户的输入。 您可以使用任何名称。 使用有意义的名称有助于记住正在处理的数据，这会很有帮助。

每个 `<input>` 元素的 `value` 属性包含一个 Razor 代码（例如 `Request.Form["title"]`）。 在上一教程中，你已学习了此技巧的一个版本，可在提交窗体后保留输入到文本框中的值（如果有）。

## <a name="getting-the-form-values"></a>获取窗体值

接下来，添加处理窗体的代码。 在大纲中，你将执行以下操作：

1. 检查页面是否正在发布（已提交）。 只需在用户单击该按钮时（而不是在页面首次运行时）运行。
2. 获取用户输入到文本框中的值。 在这种情况下，由于窗体使用的是 `POST` 谓词，因此从 `Request.Form` 集合获取窗体值。
3. 将值作为新记录插入到*电影*数据库表中。

在该文件的顶部，添加以下代码：

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

前几行创建变量（`title`、`genre`和 `year`）以保存文本框中的值。 行 `if(IsPost)` 确保*只*在用户单击 "**添加电影**" 按钮时（即，在窗体已发布后）设置变量。

正如你在前面的教程中看到的那样，可以使用表达式（如 `Request.Form["name"]`）获取文本框的值，其中*name*是 `<input>` 元素的名称。

变量（`title`、`genre`和 `year`）的名称是任意的。 与分配给 `<input>` 元素的名称类似，你可以随意调用它们。 （变量的名称不必与窗体上 `<input>` 元素的名称属性匹配。）但与 `<input>` 元素一样，可以使用反映它们所包含的数据的变量名称。 编写代码时，一致的名称使你可以更轻松地记住正在处理的数据。

## <a name="adding-data-to-the-database"></a>向数据库添加数据

在刚刚添加的代码块中，只需在 `if` 块的右大括号（`}`）*内*（而不是在代码块内），添加以下代码：

[!code-csharp[Main](entering-data/samples/sample3.cs)]

此示例类似于在上一教程中用于提取和显示数据的代码。 以 `db =` 开头的行将打开数据库（与之前一样），下一行将再次定义 SQL 语句，如之前所见。 但这次它定义了 SQL `Insert Into` 语句。 下面的示例显示了 `Insert Into` 语句的常规语法：

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

换句话说，您可以指定要插入的表，然后列出要插入的列，然后列出要插入的值。 （如前所述，SQL 不区分大小写，但有些人会将关键字改为大写，以便更轻松地读取命令。）

要插入的列已在命令中列出，`(Title, Genre, Year)`。 有趣的部分是如何将文本框中的值获取到命令的 `VALUES` 部分。 您看到的是 `@0`、`@1`和 `@2`，而不是实际值。 运行命令时（在 "`db.Execute`" 行中），将从文本框中传递所获得的值。

**重要提示！** 请记住，你只应在 SQL 语句中包括用户在线输入的数据的唯一方法是使用占位符，如此处所示（`VALUES(@0, @1, @2)`）。 如果将用户输入连接到 SQL 语句，会自行打开 SQL 注入式攻击，如 ASP.NET 网页（上一教程）[中的窗体基础](https://go.microsoft.com/fwlink/?LinkId=251581)中所述。

在 `if` 块中，在 `db.Execute` 行后面添加以下行：

[!code-css[Main](entering-data/samples/sample4.css)]

将新电影插入到数据库后，此线将跳转到 "*电影*" 页，以便您可以看到刚刚输入的影片。 `~` 运算符表示 "网站的根"。 （`~` 运算符仅适用于 ASP.NET 页面，而不能在 HTML 中使用。）

完整的代码块如下例所示：

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>测试插入命令（迄今为止）

尚未完成，但现在是一个好的测试时间。

在 WebMatrix 中文件的树状视图中，右键单击 " *AddMovie* " 页，然后单击 "**在浏览器中启动**"。

![浏览器中的 "添加电影" 页面](entering-data/_static/image2.png)

（如果你在浏览器中结束了不同的页面，请确保 URL `http://localhost:nnnnn/AddMovie`），其中*nnnnn*是你正在使用的端口号。）

您是否收到错误页？ 如果是这样，请仔细阅读并确保代码看起来与前面列出的内容完全相同。

以格式输入电影 &mdash; 例如，使用 "公民 Kane"、"Drama" 和 "1941"。 （或任何其他内容）然后单击 "**添加电影**"。

如果一切顺利，您会被重定向到*电影*页面。 请确保您的新电影已列出。

![显示新添加的电影的电影页面](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>验证用户输入

返回到*AddMovie*页，或再次运行它。 输入其他电影，但这次仅输入标题 &mdash; 例如，输入 "Singin' in Rain"。 然后单击 "**添加电影**"。

你将再次重定向到*电影*页面。 您可以找到新电影，但它不完整。

![显示缺少某些值的新电影的电影页面](entering-data/_static/image4.png)

当您创建了*电影*表时，您显式地说没有任何字段可以为 null。 这里有一个新电影的输入窗体，并将字段留空。 这是个错误。

在这种情况下，数据库不会实际引发（或*引发*）错误。 你未提供流派或年份，因此*AddMovie*页中的代码将这些值视为所谓的*空字符串*。 当 SQL `Insert Into` 命令运行时，"流派" 和 "年份" 字段在其中没有有用的数据，但是它们不是 null。

很显然，您不想让用户在数据库中输入半空电影信息。 解决方案是验证用户的输入。 最初，验证只需确保用户输入了所有字段的值（即，它们都不包含空字符串）。

> [!TIP]
> 
> **Null 和空字符串**
> 
> 在编程中，"无值" 的不同概念之间存在差异。 通常，如果从未以任何方式对其进行设置或初始化，则该值为*null* 。 相反，需要字符数据（字符串）的变量可以设置为*空字符串*。 在这种情况下，值不为 null;它只是显式设置为长度为零的字符字符串。 这两个语句显示了差异：
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> 这有点复杂，但要点是 `null` 表示一种不确定的状态。
> 
> 现在，必须准确了解某个值为 null 时，以及何时只是一个空字符串。 在*AddMovie*页的代码中，可以使用 `Request.Form["title"]` 等来获取文本框的值。 首次运行页面时（在单击按钮之前），`Request.Form["title"]` 的值为 null。 但在提交窗体时，`Request.Form["title"]` 获取 `title` 文本框的值。 这并不明显，但空文本框不是 null;它中只包含一个空字符串。 因此，当运行代码以响应按钮单击时，`Request.Form["title"]` 在其中包含空字符串。
> 
> 为什么此项区分非常重要？ 当您创建了*电影*表时，您显式地说没有任何字段可以为 null。 但这里有一个新电影的输入窗体，而您会将字段留空。 当您尝试保存没有流派或年份值的新电影时，您可能希望数据库产生抱怨。 但这也是 &mdash; 即使将这些文本框留空也是如此，这些值不是 null;它们是空字符串。 因此，您可以将新电影保存到数据库中，其中，这些列为空 &mdash; 但不是 null！ &mdash; 值。 因此，你必须确保用户不会提交空字符串，你可以通过验证用户的输入来完成此操作。

### <a name="the-validation-helper"></a>验证帮助器

ASP.NET 网页包含了帮助程序 &mdash; `Validation` 的帮助器 &mdash;，可用于确保用户输入满足你的要求的数据。 `Validation` 帮助器是内置于 ASP.NET 网页的帮助器之一，因此您无需使用 NuGet 将其作为包安装，这是在前面的教程中安装 Gravatar helper 的方式。

若要验证用户的输入，你需要执行以下操作：

- 使用代码指定希望在页的文本框中需要值。
- 将测试放入代码，以便仅当所有内容都得到正确验证时才将电影信息添加到数据库中。
- 向标记添加代码以显示错误消息。

在*AddMovie*页的代码块中，在变量声明之前的顶部，添加以下代码：

[!code-csharp[Main](entering-data/samples/sample7.cs)]

对于要在其中需要输入的每个字段（`<input>` 元素），只需调用一次 `Validation.RequireField`。 你还可以为每个调用添加自定义错误消息，如下所示。 （我们只是为了显示您可以放入您的内容。）

如果出现问题，则需要防止将新的电影信息插入到数据库中。 在 `if(IsPost)` 块中，使用 `&&` （逻辑 AND）添加另一个测试 `Validation.IsValid()`的条件。 完成后，整个 `if(IsPost)` 块如下所示：

[!code-csharp[Main](entering-data/samples/sample8.cs)]

如果使用 `Validation` 帮助程序注册的任何字段存在验证错误，则 `Validation.IsValid` 方法返回 false。 在这种情况下，该块中的任何代码都不会运行，因此不会在数据库中插入无效的电影条目。 当然，您不会重定向到*电影*页面。

完整的代码块，包括验证代码，现在如下例所示：

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>显示验证错误

最后一步是显示任何错误消息。 可以为每个验证错误显示单独的消息，也可以显示摘要或同时显示两者。 在本教程中，您将执行这两项操作，以便您可以看到它的工作原理。

在要验证的每个 `<input>` 元素旁边，调用 `Html.ValidationMessage` 方法并向其传递要验证的 `<input>` 元素的名称。 将 `Html.ValidationMessage` 方法放在要显示错误消息的位置。 当页面运行时，`Html.ValidationMessage` 方法将呈现验证错误将呈现的 `<span>` 元素。 （如果没有错误，则会呈现 `<span>` 元素，但其中没有任何文本。）

更改页面中的标记，使其包含页面上三个 `<input>` 元素的 `Html.ValidationMessage` 方法，如以下示例所示：

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

若要查看摘要的工作原理，还应在页面上的 `<h1>Add a Movie</h1>` 元素之后添加以下标记和代码：

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

默认情况下，`Html.ValidationSummary` 方法将在列表中显示所有验证消息（在 `<div>` 元素内的 `<ul>` 元素）。 与 `Html.ValidationMessage` 方法一样，验证摘要的标记始终呈现;如果没有错误，则不会呈现列表项。

摘要可以是显示验证消息的另一种方法，而不是使用 `Html.ValidationMessage` 方法来显示每个特定于字段的错误。 或者，您可以使用摘要和详细信息。 或者，您可以使用 `Html.ValidationSummary` 方法来显示一般错误，然后使用各个 `Html.ValidationMessage` 调用来显示详细信息。

完整的页现在如下例所示：

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

介绍完毕。 现在可以通过添加电影来测试页面，但要保留一个或多个字段。 当你执行此操作时，将看到以下错误显示：

![添加显示验证错误消息的电影页面](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>设置验证错误消息的样式

您可以看到存在错误消息，但它们并不是很好。 不过，有一种简单的方法可以对错误消息进行样式。

若要为 `Html.ValidationMessage`显示的各个错误消息建立样式，请创建一个名为 `field-validation-error`的 CSS 样式类。 若要定义验证摘要的外观，请创建一个名为 `validation-summary-errors`的 CSS 样式类。

若要查看此方法的工作方式，请在页面的 `<head>` 部分中添加一个 `<style>` 元素。 然后，定义名为 `field-validation-error` 的样式类和包含以下规则的 `validation-summary-errors`：

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

通常，您可能会将样式信息放在单独的 *.css*文件中，但为了简单起见，您现在可以将其放在页面中。 （在本教程的后面部分中，您将 CSS 规则移到单独的 *.css*文件中。）

如果存在验证错误，`Html.ValidationMessage` 方法将呈现包含 `class="field-validation-error"`的 `<span>` 元素。 通过添加该类的样式定义，可以配置消息的外观。 如果有错误，`ValidationSummary` 方法同样会动态呈现特性 `class="validation-summary-errors"`。

再次运行该页，并特意忽略几个字段。 现在，这些错误比较明显。 （实际上，它们是 overdone 的，但这只是为了显示您可以执行的操作。）

![添加显示已设置样式的验证错误的电影页面](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>添加电影页面的链接

最后一步是让从原始电影列表访问*AddMovie*页面变得非常方便。

再次打开*电影*页面。 在 `WebGrid` 助手后面的结束 `</div>` 标记后，添加以下标记：

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

如前文所述，ASP.NET 会将 `~` 运算符解释为网站的根。 无需使用 `~` 运算符;您可以使用标记 `<a href="./AddMovie">Add a movie</a>` 或其他方式来定义 HTML 理解的路径。 但是，当你为 Razor 页面创建链接时，`~` 运算符是一种很好的通用方法，因为它使站点更灵活-如果将当前页移动到子文件夹，则该链接仍将转到*AddMovie*页。 （请记住，`~` 运算符仅适用于*cshtml*页。 ASP.NET 理解它，但它不是标准 HTML。）

完成后，运行 "*电影*" 页。 它将如下所示：

![链接到 "添加电影" 页面的电影页面](entering-data/_static/image7.png)

单击 "**添加电影**" 链接，确保它转到*AddMovie*页。

## <a name="coming-up-next"></a>下一步

在下一教程中，您将学习如何允许用户编辑数据库中已有的数据。

## <a name="complete-listing-for-addmovie-page"></a>AddMovie 页的完整列表

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools 站点上的[SQL INSERT INTO 语句](http://www.w3schools.com/sql/sql_insert.asp)
- [验证 ASP.NET 网页站点中的用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)。 有关使用 `Validation` 帮助程序的详细信息。

> [!div class="step-by-step"]
> [上一页](form-basics.md)
> [下一页](updating-data.md)
