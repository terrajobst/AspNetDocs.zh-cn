---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介绍 ASP.NET 网页-HTML 窗体基础知识 |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍如何创建输入窗体以及如何在使用 ASP.NET 网页（Razor）时处理用户输入。 现在，你 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463538"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>介绍 ASP.NET 网页-HTML 窗体基础知识

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程介绍如何创建输入窗体以及如何在使用 ASP.NET 网页（Razor）时处理用户输入。 现在您已经有了一个数据库，您将使用您的表单技能让用户在数据库中找到特定的电影。 它假定您已完成了[使用 ASP.NET 网页显示数据的简介](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。
> 
> 学习内容：
> 
> - 如何使用标准 HTML 元素创建窗体。
> - 如何读取窗体中的用户输入。
> - 如何创建可通过使用用户提供的搜索词来有选择地获取数据的 SQL 查询。
> - 如何在页中包含用户输入的内容。
>   
> 
> 介绍的功能/技术：
> 
> - `Request` 对象。
> - SQL `Where` 子句。

## <a name="what-youll-build"></a>你将生成

在上一教程中，您创建了一个数据库，向其中添加了数据，然后使用 `WebGrid` 帮助器来显示数据。 在本教程中，您将添加一个搜索框，您可以在其中查找特定流派的电影或标题包含您输入的任何单词的电影。 （例如，你将能够查找流派为 "Action" 或标题包含 "Harry" 或 "艾德" 的所有电影。）

完成本教程后，会看到如下所示的页面：

![具有流派和标题搜索的电影页面](form-basics/_static/image1.png)

页面的列表部分与上一个 &mdash; 网格的教程中的部分相同。 不同之处在于网格只显示您搜索的影片。

## <a name="about-html-forms"></a>关于 HTML 窗体

（如果你已经熟悉了如何创建 HTML 窗体并且 `GET` 和 `POST`之间存在差异，则可以跳过此部分。）

窗体具有用户输入元素 &mdash; 文本框、按钮、单选按钮、复选框、下拉列表等。 用户填写这些控件或进行选择，然后通过单击按钮提交窗体。

下面的示例演示了窗体的基本 HTML 语法：

[!code-html[Main](form-basics/samples/sample1.html)]

当此标记在页中运行时，它将创建一个简单的窗体，如下图所示：

![在浏览器中呈现的基本 HTML 窗体](form-basics/_static/image2.png)

`<form>` 元素包含要提交的 HTML 元素。 （简单错误是将元素添加到页面，然后忘记将其放在 `<form>` 元素中。 在这种情况下，不会提交任何内容。）`method` 特性告诉浏览器如何提交用户输入。 如果要在服务器上执行更新，则将此设置为 `post` 如果你只是从服务器中提取数据，则将其设置为 `get`。

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET、POST 和 HTTP Verb 安全**
> 
> HTTP （浏览器和服务器用于交换信息的协议）在基本操作中非常简单。 浏览器仅使用几个谓词来向服务器发出请求。 编写 web 代码时，了解这些谓词以及浏览器和服务器如何使用它们都很有帮助。 到目前为止，最常用的动词如下：
> 
> - `GET`。 浏览器使用此谓词从服务器提取内容。 例如，当你在浏览器中键入 URL 时，浏览器将执行 `GET` 操作来请求所需的页面。 如果页面包含图形，则浏览器将执行其他 `GET` 操作来获取映像。 如果 `GET` 操作必须将信息传递给服务器，则会将信息作为 URL 的一部分传递到查询字符串中。
> - `POST`。 浏览器发送 `POST` 请求，以便提交要在服务器上添加或更改的数据。 例如，`POST` 谓词用于在数据库中创建记录或更改现有记录。 大多数情况下，当你填写表单并单击 "提交" 按钮时，浏览器将执行 `POST` 操作。 在 `POST` 操作中，传递给服务器的数据位于页面的正文中。
> 
> 这些谓词之间的一个重要区别在于，`GET` 操作不应更改服务器上的任何内容（或以略微抽象的方式进行操作），则 `GET` 操作不会导致服务器上的状态发生更改。 你可以根据需要对相同的资源执行 `GET` 操作，并且这些资源不会更改。 （`GET` 操作通常称为 "安全"，或使用技术术语 "*幂*等"。）当然，在每次执行操作时，`POST` 请求都将在服务器上更改某些内容。
> 
> 下面两个示例将帮助说明这种区别。 使用必应或 Google 等引擎执行搜索时，需要填写包含一个文本框的窗体，然后单击 "搜索" 按钮。 浏览器执行 `GET` 操作，并将输入的值输入到作为 URL 的一部分传递的框中。 对此类型的窗体使用 `GET` 操作是正确的，因为搜索操作不会更改服务器上的任何资源，而只会提取信息。
> 
> 现在，请考虑订购联机内容的过程。 填写订单详细信息，然后单击 "提交" 按钮。 此操作将是 `POST` 请求，因为此操作将导致服务器上发生更改，如新订单记录、帐户信息更改以及可能有许多其他更改。 与 `GET` 操作不同，你不能重复 `POST` 请求（如果已这样做），则每次重新提交请求时，你都将在服务器上生成新的订单。 （在这种情况下，网站通常会警告您不要多次单击 "提交" 按钮，否则将禁用 "提交" 按钮，以便不会意外地重新提交窗体。）
> 
> 在本教程的过程中，将同时使用 `GET` 操作和 `POST` 操作来处理 HTML 窗体。 在每种情况下，我们都将介绍你使用的动词是合适的。
> 
> （若要了解有关 HTTP 谓词的详细信息，请参阅 W3C 网站上的[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)一文。）

大多数用户输入元素都是 HTML `<input>` 元素。 它们看起来像 `<input type="type" name="name">,`，其中*类型*指示所需的用户输入控件的类型。 这些元素是通用元素：

- 文本框： `<input type="text">`
- 复选框： `<input type="check">`
- 单选按钮： `<input type="radio">`
- 按钮： `<input type="button">`
- "提交" 按钮： `<input type="submit">`

你还可以使用 `<textarea>` 元素创建多行文本框和 `<select>` 元素，以创建下拉列表或可滚动列表。 （有关 HTML 窗体元素的详细信息，请参阅 W3Schools 站点上的[Html 窗体和输入](http://www.w3schools.com/html/html_forms.asp)。）

`name` 特性非常重要，因为该名称是稍后会获得元素值的方式，正如您很快将看到的那样。

有趣的部分是页面开发人员处理用户输入的内容。 没有与这些元素关联的内置行为。 相反，您必须获取用户输入或选择的值，并对其执行一些操作。 这就是你在本教程中学习的内容。

> [!TIP] 
> 
> **HTML5 和输入窗体**
> 
> 您可能知道，HTML 正在转换，最新版本（HTML5）为用户输入信息提供了更直观的支持。 例如，在 HTML5 中，你（页面开发人员）可以告诉页面你希望用户输入日期。 然后，浏览器可以自动显示日历，而不需要用户手动输入日期。 不过，HTML5 是新的，但并非所有浏览器都支持此项。
> 
> ASP.NET 网页支持 HTML5 输入用户浏览器的范围。 若要了解 HTML5 中 `<input>` 元素的新属性，请参阅 W3Schools 站点上的[HTML &lt;输入&gt; 类型属性](http://www.w3schools.com/html/html_form_input_types.asp)。

## <a name="creating-the-form"></a>创建窗体

在 WebMatrix 的 "**文件**" 工作区中，打开 "*电影. cshtml* " 页。

在结束 `</h1>` 标记之后以及在 `grid.GetHtml` 调用的开始 `<div>` 标记之前，添加以下标记：

[!code-html[Main](form-basics/samples/sample2.html)]

此标记创建一个窗体，该窗体具有名为 `searchGenre` 的文本框和一个提交按钮。 文本框和提交按钮包含在其 `method` 属性设置为 `get`的 `<form>` 元素中。 （请记住，如果未将 "文本框" 和 "提交" 按钮放入 `<form>` 元素中，则在单击该按钮时，不会提交任何内容。）由于要创建的窗体在服务器上没有进行任何更改，因此可以使用此处的 `GET` 谓词—这只会导致搜索。 （在上一教程中，你使用的是 `post` 方法，该方法是将更改提交到服务器的方式。 你将在下一教程中看到该。）

运行页面。 虽然您没有为窗体定义任何行为，但您可以看到它的外观：

![用于流派的搜索框的电影页面](form-basics/_static/image3.png)

在文本框中输入一个值，如 "喜剧"。 然后单击 "**搜索流派**"。

记下页面的 URL。 由于您将 `<form>` 元素的 `method` 属性设置为 `get`，因此您输入的值现在是 URL 中的查询字符串的一部分，如下所示：

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>读取窗体值

该页已经包含一些可获取数据库数据的代码，并在网格中显示结果。 现在，你必须添加一些代码来读取文本框的值，以便可以运行包含搜索词的 SQL 查询。

由于将窗体的方法设置为 `get`，因此可以通过使用如下所示的代码来读取在文本框中输入的值：

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString` 对象（`Request` 对象的 `QueryString` 属性）包含作为 `GET` 操作的一部分提交的元素的值。 `Request.QueryString` 属性包含在表单中提交的值的*集合*（列表）。 若要获取任何单个值，请指定所需的元素的名称。 这就是在创建文本框的 `<input>` 元素（`searchTerm`）上必须有 `name` 属性的原因。 （有关 `Request` 对象的详细信息，请参阅后面的[边栏](#BKMK_TheRequestObject)。）

很简单，足以读取文本框的值。 但是，如果用户没有在文本框中输入任何内容，但仍单击 "**搜索**"，则可以忽略这一单击，因为没有要搜索的内容。

下面的代码示例演示如何实现这些条件。 （你还不必添加此代码，稍后你将执行此操作。）

[!code-csharp[Main](form-basics/samples/sample3.cs)]

测试将以这种方式断开：

- 获取 `Request.QueryString["searchGenre"]`的值，即输入到名为 `searchGenre`的 `<input>` 元素中的值。
- 使用 `IsEmpty` 方法查明它是否为空。 此方法是确定某些内容（例如，窗体元素）是否包含值的标准方法。 但实际上，您只关心它*是否不*为空，因此 。
- 将 `!` 运算符添加到 `IsEmpty` 测试之前。 （`!` 运算符表示逻辑非）。

在纯英文版中，整个 `if` 条件转换为以下内容：*如果窗体的 searchGenre 元素不为空，则 ...*

此块设置用于创建使用搜索词的查询的阶段。 将在下一部分执行该操作。

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Request 对象**
> 
> `Request` 对象包含浏览器在请求或提交页面时发送给应用程序的所有信息。 此对象包括用户提供的所有信息，如要上传的文本框值或文件。 它还包括所有种类的附加信息，如 cookie、URL 查询字符串中的值（如果有）、正在运行的页面的文件路径、用户使用的浏览器的类型，以及在浏览器中设置的语言列表等等。
> 
> `Request` 对象是值的*集合*（列表）。 通过指定集合的名称，可以获取集合中的单个值：
> 
> `var someValue = Request["name"];`
> 
> `Request` 对象实际上会公开多个子集。 例如:
> 
> - 如果请求是一个 `POST` 请求，`Request.Form` 将从已提交的 `<form>` 元素内的元素中提供值。
> - `Request.QueryString` 仅提供 URL 的查询字符串中的值。 （在 URL （如 `http://mysite/myapp/page?searchGenre=action&page=2`）中，URL 的 `?searchGenre=action&page=2` 部分是查询字符串。）
> - `Request.Cookies` 收集可让你访问浏览器发送的 cookie。
> 
> 若要获取你知道的值在提交的窗体中，你可以使用 `Request["name"]`。 或者，你可以使用更具体的版本 `Request.Form["name"]` （适用于 `POST` 请求）或 `Request.QueryString["name"]` （对于 `GET` 请求）。 当然， *name*是要获取的项的名称。
> 
> 要获取的项的名称必须在所使用的集合中是唯一的。 这就是 `Request` 对象提供 `Request.Form` 和 `Request.QueryString`的子集的原因。 假设页面包含一个名为 `userName` 的窗体元素，*还*包含一个名为 `userName`的 cookie。 如果您获取 `Request["userName"]`，是否需要窗体值或 cookie。 但是，如果您获取 `Request.Form["userName"]` 或 `Request.Cookie["userName"]`，就会明确知道要获取哪个值。
> 
> 这是一种很好的做法，只需使用你感兴趣的 `Request` 子集，如 `Request.Form` 或 `Request.QueryString`。 对于您在本教程中创建的简单页面，它可能不会真正产生任何差别。 但是，当你创建更复杂的页面时，使用显式版本 `Request.Form` 或 `Request.QueryString` 可帮助你避免在页面包含窗体（或多个窗体）、cookie 和查询字符串值等时可能出现的问题。

## <a name="creating-a-query-by-using-a-search-term"></a>使用搜索词创建查询

现在，您已经知道了如何获取用户输入的搜索词，接下来可以创建一个使用它的查询。 请记住，若要从数据库中获取所有电影项，请使用类似于以下语句的 SQL 查询：

`SELECT * FROM Movies`

若要仅获取特定电影，必须使用包含 `Where` 子句的查询。 此子句可用于设置查询返回的行的条件。 以下是一个示例：

`SELECT * FROM Movies WHERE Genre = 'Action'`

基本格式为 `WHERE column = value`。 除了 `=`之外，你还可以使用不同的运算符，如 `>` （大于）、`<` （小于）、`<>` （不等于）、`<=` （小于或等于）等。

如果你知道，SQL 语句不区分大小写 &mdash; `SELECT` 与 `Select` 相同（甚至 `select`）。 但是，用户通常在 SQL 语句中将关键字大写，如 `SELECT` 和 `WHERE`，以使其更易于阅读。

### <a name="passing-the-search-term-as-a-parameter"></a>作为参数传递搜索词

搜索特定的流派非常简单（`WHERE Genre = 'Action'`），但您希望能够搜索用户输入的任何流派。 为此，你将创建为包含要搜索的值的占位符的 SQL 查询。 它将类似于以下命令：

`SELECT * FROM Movies WHERE Genre = @0`

占位符是后跟零的 `@` 字符。 您可能猜到，一个查询可以包含多个占位符，它们被命名为 `@0`、`@1`、`@2`等。

若要设置查询并为其实际传递值，请使用如下所示的代码：

[!code-sql[Main](form-basics/samples/sample4.sql)]

此代码类似于在网格中显示数据所执行的操作。 唯一的区别是：

- 查询包含占位符（`WHERE Genre = @0"`）。
- 查询放入变量（`selectCommand`）;在之前，你将查询直接传递到 `db.Query` 方法。
- 调用 `db.Query` 方法时，将同时传递要用于占位符的查询和值。 （如果查询有多个占位符，则可以将它们全部作为不同的值传递给方法。）

如果将所有这些元素放在一起，则会获得以下代码：

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **重要提示！** 使用占位符（如 `@0`）将值传递给 SQL 命令对于安全性*极其重要*。 在此处看到的是变量数据的占位符，是构造 SQL 命令的唯一方法。
> 
> 永远不要通过组合（串联）文本和从用户获取的值来构造 SQL 语句。 将用户输入连接到 SQL 语句将打开站点到*sql 注入攻击*，恶意用户会将值提交到攻击数据库的页面。 （有关详细信息，请参阅 MSDN 网站的[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)一文。）

## <a name="updating-the-movies-page-with-search-code"></a>更新包含搜索代码的电影页面

现在，您可以更新 "*电影*" 文件中的代码。 首先，将页面顶部代码块中的代码替换为以下代码：

[!code-csharp[Main](form-basics/samples/sample6.cs)]

此处的差别在于，你已将查询放入 `selectCommand` 变量，稍后会将该变量传递给 `db.Query`。 如果将 SQL 语句放入变量中，则可以更改语句，这是执行搜索的操作。

你还删除了这两行，稍后会将其放回：

[!code-csharp[Main](form-basics/samples/sample7.cs)]

您还不想运行查询（即，调用 `db.Query`），并且您也不想初始化 `WebGrid` 帮助程序。 确定要运行的 SQL 语句后，您将执行这些操作。

在此重写块后，可以添加用于处理搜索的新逻辑。 已完成的代码将如下所示。 更新页面中的代码，使其与以下示例匹配：

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

该页的工作方式如下所示。 每次运行该页面时，代码都会打开数据库，`selectCommand` 变量设置为从 `Movies` 表中获取所有记录的 SQL 语句。 此代码还初始化 `searchTerm` 变量。

但是，如果当前请求包含 `searchGenre` 元素的值，则代码会将 `selectCommand` 设置为一个不同的查询（即），将其设置为包含 `Where` 子句以搜索流派的查询。 它还会将 `searchTerm` 设置为搜索框中传递的任何内容（可能没有任何内容）。

无论 `selectCommand`哪一条 SQL 语句，代码都会调用 `db.Query` 来运行查询，并在 `searchTerm`中传递任何内容。 如果 `searchTerm`中没有任何内容，则不重要，因为在这种情况下，不会将值传递给 `selectCommand`。

最后，代码使用查询结果初始化 `WebGrid` 帮助程序，就像以前一样。

你可以看到，通过将 SQL 语句和搜索词放入变量中，你已增加了代码的灵活性。 你将在本教程的后面部分中看到，你可以使用此基本框架，并为不同类型的搜索继续添加逻辑。

## <a name="testing-the-search-by-genre-feature"></a>测试流派搜索功能

在 WebMatrix 中，运行 "*电影*" 页。 你会看到带有流派文本框的页面。

输入你为某个测试记录输入的流派，然后单击 "**搜索**"。 此时会看到一个列表，其中列出了与该流派匹配的影片：

![搜索 "Comedies" 流派后的电影页面列表](form-basics/_static/image4.png)

请输入不同的流派并重新搜索。 尝试使用全部小写字母或所有大写字母输入流派，以便可以看到搜索不区分大小写。

## <a name="remembering-what-the-user-entered"></a>"记住" 用户输入的内容

您可能已注意到，在输入流派并单击**搜索流派**后，会看到该流派的列表。 不过，"搜索" 文本框为空 &mdash; 也就是说，它不记得您输入的内容。

务必了解为何会出现此行为。 提交页面后，浏览器会向 web 服务器发送请求。 当 ASP.NET 获取请求时，它会创建页面的全新实例，运行其中的代码，然后再次将页面呈现到浏览器。 但实际上，页面并不知道自己使用的是其自身的以前版本。 它的所有人都知道，请求中包含某些表单数据。

每次请求页面时都 &mdash; 首次，还是提交 &mdash; 你要获取新的页面。 Web 服务器没有最近的请求的内存。 既不 ASP.NET，也不执行浏览器。 页面的这些单独实例之间唯一的连接是在它们之间传输的任何数据。 例如，如果您提交一个页面，则新页面实例可以获取之前实例发送的表单数据。 （在页面间传递数据的另一种方法是使用 cookie。）

描述这种情况的一种正式方法是说，网页是*无状态*的。 Web 服务器以及页面本身和页面中的元素不会维护有关页面以前状态的任何信息。 Web 是以这种方式设计的，因为维护单个请求的状态会迅速耗尽 web 服务器的资源，这通常会处理数千个，甚至可能每秒处理成千上万个请求。

这就是文本框为空的原因。 提交页面后，ASP.NET 创建了页面的新实例，并通过代码和标记进行了运行。 此代码中没有告诉 ASP.NET 将值放入文本框的内容。 因此，ASP.NET 不会执行任何操作，并且文本框中的值不包含任何值。

实际上有一种简单的方法可解决此问题。 您在文本框中输入的*流派可以在代码中使用，* &mdash; 它在 `Request.QueryString["searchGenre"]`中。

更新文本框的标记，以便 `value` 属性从 `searchTerm`获取其值，如下例所示：

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

在此页上，您还可以将 `value` 特性设置为 `searchTerm` 变量，因为该变量还包含您输入的流派。 但使用 `Request` 对象设置 `value` 属性，如下所示，这是完成此任务的标准方法。 （假设您甚至要在某些情况下 &mdash; 执行此操作，则您可能希望在字段中呈现*没有*值的页面。 这一切都取决于应用程序的进展情况。）

> [!NOTE]
> 不能 "记住" 用于密码的文本框的值。 这会成为允许用户使用代码填写密码字段的安全漏洞。

再次运行该页面，输入流派，然后单击 "**搜索流派**"。 这一次不仅能看到搜索结果，而且文本框记住了上次输入的内容：

![显示前一项已 "记住" 文本框的页面](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>搜索标题中的任何词

你现在可以搜索任何流派，但你可能还希望搜索标题。 搜索时很难准确地获取标题，因此，您可以搜索出现在标题内任意位置的单词。 为此，请使用 `LIKE` 运算符和语法，如下所示：

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

此命令将获取其标题包含 "艾德" 的所有电影。 使用 `LIKE` 运算符时，将通配符作为搜索词的一部分包含 `%`。 搜索 `LIKE 'adventure%'` 表示 "以 ' 艾德 ' 开头"。 （从技术上讲，这表示 "字符串 ' 艾德"，后面跟有任何内容）。同样，搜索词 `LIKE '%adventure'` 表示 "任何内容后跟字符串 ' 艾德 '"，这是另一种说 "以 ' 艾德 ' 结尾" 的方式。

因此，搜索词 `LIKE '%adventure%'` 意味着标题中的任何位置都具有 "艾德"。 （从技术上说： "标题中的任何内容，后面跟有" 艾德公司 "，然后再执行任何操作。"）

在 `<form>` 元素中，在 "流派搜索" 的 "结束 `</div>`" 标记下添加以下标记（紧靠在结束 `</form>` 元素之前）：

[!code-html[Main](form-basics/samples/sample10.html)]

处理此搜索的代码与用于流派搜索的代码相似，不同之处在于您必须组合 `LIKE` 搜索。 在页面顶部的代码块中，在流派搜索的 `if` 块后面添加此 `if` 块：

[!code-csharp[Main](form-basics/samples/sample11.cs)]

此代码使用前面看到的相同逻辑，不同之处在于，搜索使用 `LIKE` 运算符，而代码将 "`%`" 置于搜索词之前和之后。

请注意如何轻松地向页面中添加另一个搜索。 你需要做的只是：

- 创建一个测试 `if` 块，以查看相关搜索框是否具有值。
- 将 `selectCommand` 变量设置为新的 SQL 语句。
- 将 `searchTerm` 变量设置为要传递给查询的值。

下面是完整的代码块，其中包含用于标题搜索的新逻辑：

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

下面总结了此代码的作用：

- 在顶部初始化变量 `searchTerm` 和 `selectCommand`。 你将根据用户在页面中执行的操作，将这些变量设置为相应的搜索词（如果有）和相应的 SQL 命令。 默认搜索是从数据库中获取所有电影的简单情况。
- 在 `searchGenre` 和 `searchTitle`的测试中，代码将 `searchTerm` 设置为要搜索的值。 这些代码块还将 `selectCommand` 设置为该搜索的相应 SQL 命令。
- 仅调用一次 `db.Query` 方法，其中使用的是任何 SQL 命令 `selectedCommand` 以及 `searchTerm`中的任何值。 如果没有搜索词（无流派，没有标题字），则 `searchTerm` 的值为空字符串。 但这并不重要，因为在这种情况下，查询不需要参数。

## <a name="testing-the-title-search-feature"></a>测试标题搜索功能

现在可以测试已完成的搜索页面。 运行

输入一个流派，然后单击 "**搜索流派**"。 网格显示该流派的电影，就像之前一样。

输入标题字，并单击 "**搜索标题**"。 网格显示在标题中包含该单词的影片。

![搜索标题中的 "the" 后的电影页面列表](form-basics/_static/image6.png)

将这两个文本框留空，然后单击其中一个按钮。 网格显示所有电影。

## <a name="combining-the-queries"></a>合并查询

你可能会注意到，你可以执行的搜索是独占的。 不能同时搜索标题和流派，即使两个搜索框中都有值。 例如，不能搜索标题包含 "艾德" 的所有操作电影。 （正如当前对该页进行编码，如果为 "流派" 和 "标题" 输入值，则标题搜索优先。）若要创建组合条件的搜索，则必须创建包含如下语法的 SQL 查询：

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

而且，您必须使用如下所示的语句运行查询：

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

正如您所看到的，创建逻辑以允许搜索条件的多个排列可能会很多。 因此，我们将在此处停止。

## <a name="coming-up-next"></a>下一步

在下一教程中，您将创建一个使用窗体的页面，使用户能够将电影添加到数据库中。

## <a name="complete-listing-for-movie-page-updated-with-search"></a>完整的电影页面列表（已更新为搜索）

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools 站点上的[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)
- W3C 网站上的[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)一文

> [!div class="step-by-step"]
> [上一页](displaying-data.md)
> [下一页](entering-data.md)
