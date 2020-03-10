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
# <a name="introducing-aspnet-web-pages---updating-database-data"></a>ASP.NET 网页更新数据库数据简介

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程说明如何在使用 ASP.NET 网页（Razor）时更新（更改）现有数据库条目。 假设已通过[使用 ASP.NET 网页的窗体通过输入数据](entering-data.md)完成了系列。
> 
> 学习内容：
> 
> - 如何在 `WebGrid` 帮助程序中选择单个记录。
> - 如何从数据库中读取单个记录。
> - 如何使用数据库记录中的值预加载窗体。
> - 如何更新数据库中的现有记录。
> - 如何在页中存储信息而不显示它。
> - 如何使用隐藏字段存储信息。
>   
> 
> 介绍的功能/技术：
> 
> - `WebGrid` 帮助程序。
> - SQL `Update` 命令。
> - `Database.Execute` 方法。
> - 隐藏字段（`<input type="hidden">`）。

## <a name="what-youll-build"></a>你将生成

在上一教程中，您学习了如何将记录添加到数据库中。 在这里，你将学习如何显示要编辑的记录。 在*电影*页面中，你将更新 `WebGrid` 帮助程序，使其在每个电影旁显示一个**编辑**链接：

![WebGrid 显示每个电影的 "编辑" 链接](updating-data/_static/image1.png)

单击 "**编辑**" 链接时，将转到不同的页面，其中的影片信息已在表单中：

![显示要编辑的电影的 "编辑电影" 页面](updating-data/_static/image2.png)

您可以更改任何值。 提交更改后，页面中的代码将更新数据库并返回到电影列表。

此过程部分与你在上一教程中创建的*AddMovie*页面几乎完全相同，因此我们将熟悉本教程中的大部分内容。

可以通过多种方式来实现编辑单个影片的方法。 选择的方法很容易实现并易于理解。

## <a name="adding-an-edit-link-to-the-movie-listing"></a>向电影列表添加编辑链接

首先，将更新 "*电影*" 页面，使每个电影列表也包含一个**编辑**链接。

打开*电影. cshtml*文件。

在页面的正文中，通过添加列更改 `WebGrid` 标记。 下面是修改后的标记：

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

新列如下所示：

[!code-html[Main](updating-data/samples/sample2.html)]

此列的点用于显示其文本显示为 "编辑" 的链接（`<a>` 元素）。 接下来，我们要创建一个在页面运行时如下所示的链接，每个电影的 `id` 值不同：

[!code-css[Main](updating-data/samples/sample3.css)]

此链接将调用名为*EditMovie*的页，并将查询字符串 `?id=7` 传递到该页。

新列的语法可能看起来有点复杂，但这只是因为它将多个元素放在一起。 每个元素都非常简单。 如果只关注 `<a>` 元素，则会看到以下标记：

[!code-html[Main](updating-data/samples/sample4.html)]

有关网格工作方式的一些背景信息：网格显示行，每个数据库记录一个，并显示数据库记录中每个字段的列。 构造每个网格行时，`item` 对象包含该行的数据库记录（item）。 这种安排使你可以在代码中获取该行的数据。 这就是你在此处看到的内容：表达式 `item.ID` 正在获取当前数据库项的 ID 值。 您可以使用 `item.Title`、`item.Genre`或 `item.Year`以相同的方式获取任何数据库值（标题、流派或年份）。

表达式 `"~/EditMovie?id=@item.ID` 将目标 URL 的硬编码部分（`~/EditMovie?id=`）与此动态派生的 ID 组合在一起。 （你在上一教程中看到了 `~` 运算符; 它是表示当前网站根的 ASP.NET 运算符。）

结果是，列中的这部分标记只在运行时生成类似于以下标记的内容：

[!code-xml[Main](updating-data/samples/sample5.xml)]

当然，每行 `id` 的实际值将有所不同。

## <a name="creating-a-custom-display-for-a-grid-column"></a>为网格列创建自定义显示

现在返回到网格列。 网格中最初包含的三个列仅显示数据值（标题、流派和年份）。 可以通过传递数据库列的名称来指定此显示 &mdash; 例如 `grid.Column("Title")`。

这一新的**编辑**链接列是不同的。 不指定列名，而是传递 `format` 参数。 此参数可用于定义标记，`WebGrid` 帮助器将呈现这些标记以及 `item` 值，以将列数据显示为粗体或绿色，或采用所需的任何格式。 例如，如果希望标题显示为粗体，则可以创建如下所示的列：

[!code-html[Main](updating-data/samples/sample6.html)]

（`format` 属性中所示的各种 `@` 字符标记标记和代码值之间的转换。）

了解 `format` 属性后，可以更轻松地了解如何将新的**编辑**链接列组合在一起：

[!code-html[Main](updating-data/samples/sample7.html)]

列*只*包含呈现链接的标记，以及从行的数据库记录中提取的某些信息（ID）。

> [!TIP]
> 
> **方法的命名参数和位置参数**
> 
> 多次调用方法并向其传递参数时，您只需列出用逗号分隔的参数值。 以下为若干示例：
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> 当你首次看到此代码时，我们并没有提到此问题，但在每种情况下，你都按特定顺序向方法传递参数 &mdash; 即，在该方法中定义参数的顺序。 对于 `db.Execute` 和 `Validation.RequireFields`，如果你将传递的值的顺序混合，则在页面运行时将收到一条错误消息，或者至少出现一些奇怪的结果。 显然，您必须知道要在其中传递参数的顺序。 （在 WebMatrix 中，IntelliSense 可帮助你了解参数的名称、类型和顺序。）
> 
> 作为按顺序传递值的替代方法，可以使用*命名参数*。 （按顺序传递参数称为使用*位置参数*。）对于命名参数，在传递参数值时显式包含参数的名称。 在这些教程中已经多次使用了命名参数。 例如:
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> 和
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> 命名参数对于几种情况非常方便，尤其是在方法需要很多参数时。 一种情况是您希望只传递一个或两个参数，但要传递的值不在参数列表中的第一个位置。 另一种情况是，你希望通过按最适合你的顺序传递参数，使代码更具可读性。
> 
> 显然，若要使用命名参数，必须知道参数的名称。 WebMatrix IntelliSense 可以*显示*这些名称，但目前无法为您填充这些名称。

## <a name="creating-the-edit-page"></a>创建编辑页

现在，可以创建*EditMovie*页。 当用户单击 "**编辑**" 链接时，它们将最终出现在此页上。

创建一个名为*EditMovie*的页，并将文件中的内容替换为以下标记：

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

此标记和代码与你在 " *AddMovie* " 页中的内容类似。 "提交" 按钮的文本有一个小差异。 与*AddMovie*页一样，有一个 `Html.ValidationSummary` 调用会显示验证错误（如果有）。 这次我们将 `Validation.Message`调用，因为错误将显示在验证摘要中。 如前面的教程中所述，可以在各种组合中使用验证摘要和各个错误消息。

请再次注意，`<form>` 元素的 `method` 属性设置为 "`post`"。 与*AddMovie*页一样，此页会对数据库进行更改。 因此，此窗体应执行 `POST` 操作。 （有关 `GET` 和 `POST` 操作之间的差异的详细信息，请参阅 HTML 窗体教程中的[GET、POST 和 HTTP Verb 安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)侧栏。）

正如您在前面的教程中看到的那样，文本框的 `value` 属性是使用 Razor 代码设置的，以便预先加载它们。 不过，这一次使用的是该任务 `title` 和 `genre` 等变量，而不是 `Request.Form["title"]`：

`<input type="text" name="title" value="@title" />`

与之前一样，此标记会将文本框值预加载到电影值。 你将会看到，这一次使用变量（而不是使用 `Request` 对象）非常方便。

此页上还有一个 `<input type="hidden">` 元素。 此元素存储影片 ID，而不使其在页面上可见。 该 ID 最初通过使用查询字符串值（`?id=7` 或 URL 中的类似）传递到页面。 如果将 ID 值放在隐藏字段中，则可以确保在提交窗体时它可用，即使您不能再访问调用该页的原始 URL。

与*AddMovie*页不同， *EditMovie*页的代码具有两个不同的函数。 第一种函数是，在第一次显示页面时（*仅限*之后），代码从查询字符串获取影片 ID。 然后，代码使用该 ID 从数据库中读取相应的电影，并在文本框中显示（预加载）该影片。

第二个函数是在用户单击 "**提交更改**" 按钮时，代码必须读取文本框的值并对其进行验证。 此代码还必须用新值更新数据库项。 此方法类似于添加记录，如在*AddMovie*中所见。

## <a name="adding-code-to-read-a-single-movie"></a>添加代码以读取单个电影

若要执行第一个函数，请将以下代码添加到页面顶部：

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

此代码的大部分都位于 `if(!IsPost)`开始的块内。 `!` 运算符表示 "not"，因此，*如果此请求不是 post 提交*（这是一种间接的方式），则表示该请求是*第一次运行此页*时的情况。 如前文所述，此代码*只*应在页面首次运行时运行。 如果未将代码包含在 `if(!IsPost)`中，则每次调用该页时都会运行，无论是第一次还是响应按钮单击。

请注意，此代码包含一个 `else` 块。 正如我们在引入 `if` 块时所说的那样，有时你希望在测试的条件不为 true 时运行备选代码。 这就是这种情况。 如果条件通过（即，如果传递到页面的 ID 是 "正常"），则从数据库中读取一行。 但是，如果条件未通过，则运行 `else` 块，代码会设置错误消息。

## <a name="validating-a-value-passed-to-the-page"></a>验证传递到页的值

代码使用 `Request.QueryString["id"]` 获取传递到页面的 ID。 此代码可确保已为 ID 实际传递值。 如果未传递任何值，则代码将设置一个验证错误。

此代码显示了验证信息的另一种方法。 在上一教程中，您将处理 `Validation` 帮助程序。 已注册要验证的字段，并且 ASP.NET 使用 `Html.ValidationMessage` 和 `Html.ValidationSummary`自动执行验证和显示错误。 但在这种情况下，您并未真正验证用户输入。 相反，您要验证从其他位置传递到页面的值。 `Validation` 帮助程序不会为你执行此操作。

因此，你可以通过使用 `if(!Request.QueryString["ID"].IsEmpty()`）测试该值来自行检查值。 如果出现问题，可以使用 `Html.ValidationSummary`显示错误，就像使用 `Validation` 助手时所做的一样。 为此，请调用 `Validation.AddFormError` 并向其传递要显示的消息。 `Validation.AddFormError` 是一种内置方法，可让你定义自定义消息，将其与已熟悉的验证系统结合使用。 （稍后在本教程中，我们将讨论如何使此验证过程更可靠。）

确保为电影提供 ID 后，代码会读取数据库，仅查找单个数据库项。 （您可能已注意到数据库操作的常规模式：打开数据库，定义 SQL 语句，然后运行语句。）此时，SQL `Select` 语句包括 `WHERE ID = @0`。 因为该 ID 是唯一的，所以只能返回一条记录。

查询是通过使用 `db.QuerySingle` （而不是 `db.Query`用于电影列表）执行的，代码将结果放入 `row` 变量中。 名称 `row` 任意;你可以将变量命名为你喜欢的任何名称。 然后，将用影片详细信息填充顶部初始化的变量，以便这些值可以显示在文本框中。

## <a name="testing-the-edit-page-so-far"></a>测试 "编辑" 页（迄今为止）

如果要测试页面，请立即运行*电影*页面，并单击任何电影旁边的 "**编辑**" 链接。 你将看到 " *EditMovie* " 页，其中显示了所选电影的详细信息：

![显示要编辑的电影的 "编辑电影" 页面](updating-data/_static/image3.png)

请注意，页面的 URL 包含诸如 `?id=10` （或其他数字）之类的内容。 到目前为止，您已经测试了*电影*页面工作中的**编辑**链接，您的页面从查询字符串读取了 ID，并且用于获取单个电影记录的数据库查询正在运行。

您可以更改电影信息，但单击 "**提交更改**" 不会出现任何问题。

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>添加代码以用用户的更改更新电影

在*EditMovie*文件中，若要实现第二个函数（保存更改），请将以下代码添加到 `@` 块的右大括号内。 （如果你不确定在何处放置代码，你可以查看本教程结尾处显示[的 "编辑电影" 页的完整代码列表](#Complete_Page_Listing_for_EditMovie)。）

[!code-csharp[Main](updating-data/samples/sample12.cs)]

同样，此标记和代码类似于*AddMovie*中的代码。 代码位于 `if(IsPost)` 块中，这是因为仅当用户单击 "**提交更改**" 按钮时才会运行此代码 &mdash; 即，当窗体已发布（且仅当）发布时。 在这种情况下，你未使用类似 `if(IsPost && Validation.IsValid())`的测试，即，你不是使用和来合并这两个测试。 在此页中，您首先确定是否有窗体提交（`if(IsPost)`），并且只注册要验证的字段。 然后，你可以测试验证结果（`if(Validation.IsValid()`）。 该流程与*AddMovie*页面略有不同，但效果是相同的。

您可以使用其他 `<input>` 元素 `Request.Form["title"]` 和类似的代码获取文本框的值。 请注意，这一次，代码将获取隐藏字段（`<input type="hidden">`）中的影片 ID。 当页面首次运行时，代码将获取查询字符串的 ID。 从隐藏字段获取值，以确保获得最初显示的电影的 ID （如果自那时起，查询字符串发生了某种形式的更改）。

*AddMovie*代码和此代码之间的重要区别在于，在此代码中，你将使用 SQL `Update` 语句，而不是 `Insert Into` 语句。 下面的示例显示 SQL `Update` 语句的语法：

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

您可以按任意顺序指定任何列，并且在 `Update` 操作期间不必更新每个列。 （您不能更新 ID 本身，因为这样做会有效地将记录保存为新记录，而 `Update` 操作不允许这样做。）

> [!NOTE] 
> 
> **重要提示**ID 为的 `Where` 子句非常重要，因为这是数据库了解要更新的数据库记录的方式。 如果离开 `Where` 子句，则数据库将更新数据库中的*每*条记录。 在大多数情况下，这会是一项灾难。

在代码中，要更新的值将通过使用占位符传递到 SQL 语句。 若要重复之前提到的内容：出于安全原因，*只*使用占位符将值传递给 SQL 语句。

代码使用 `db.Execute` 运行 `Update` 语句后，它会重定向回列表页，您可以在其中查看更改。

> [!TIP] 
> 
> **不同的 SQL 语句，不同的方法**
> 
> 您可能已注意到，使用略微不同的方法来运行不同的 SQL 语句。 若要运行可能返回多个记录的 `Select` 查询，请使用 `Query` 方法。 若要运行知道只返回一个数据库项的 `Select` 查询，请使用 `QuerySingle` 方法。 若要运行进行更改但不返回数据库项的命令，请使用 `Execute` 方法。
> 
> 你必须具有不同的方法，因为每个方法都会返回不同的结果，因为你已在 `Query` 和 `QuerySingle`之间的差异中看到。 （`Execute` 方法实际上返回一个值，&mdash;，这是受命令影响的数据库行数 &mdash; 但你现在已忽略了。）
> 
> 当然，`Query` 方法可能只返回一个数据库行。 但是，ASP.NET 始终将 `Query` 方法的结果视为集合。 即使此方法只返回一行，也必须从集合中提取该行。 因此，在您*知道*您只收到一行后，使用 `QuerySingle`会更方便一些。
> 
> 还有其他几种方法可执行特定类型的数据库操作。 可以在 " [ASP.NET 网页 API 快速参考](../../api-reference/asp-net-web-pages-api-reference.md#Data)" 中找到数据库方法的列表。

## <a name="making-validation-for-the-id-more-robust"></a>使 ID 验证更可靠

页面首次运行时，会从查询字符串获取影片 ID，以便可以从数据库中获取该电影。 通过使用以下代码，确保确实存在要查找的值：

[!code-csharp[Main](updating-data/samples/sample13.cs)]

你使用此代码来确保，如果用户未在*电影*页面中选择电影就会收到*EditMovies*页面，则页面将显示用户友好的错误消息。 （否则，用户将看到一个错误，可能只是将它们搞糊涂。）

但是，这种验证并不是非常可靠。 还可以通过以下错误调用该页：

- ID 不是数字。 例如，可以使用 `http://localhost:nnnnn/EditMovie?id=abc`之类的 URL 来调用页。
- ID 是一个数字，但它引用了不存在的电影（例如 `http://localhost:nnnnn/EditMovie?id=100934`）。

如果你想要查看这些 Url 导致的错误，请运行*电影*页面。 选择要编辑的电影，然后将 " *EditMovie* " 页的 url 更改为包含字母 ID 的 url 或者不存在的电影的 ID。

那么，您该怎么办呢？ 第一种解决方法是确保不仅传递到页面的 ID，而且 ID 是整数。 更改 `!IsPost` 测试的代码，使其类似于以下示例：

[!code-csharp[Main](updating-data/samples/sample14.cs)]

已将第二个条件添加到 `IsEmpty` 测试，并链接到 `&&` （逻辑 AND）：

[!code-csharp[Main](updating-data/samples/sample15.cs)]

你可能会注意[到 ASP.NET 网页编程](../introducing-razor-syntax-c.md)教程中所示的方法 `AsBool` `AsInt` 将字符字符串转换为其他数据类型。 `IsInt` 方法（以及其他方法，如 `IsBool` 和 `IsDateTime`）类似。 但是，它们仅测试是否*可以*转换字符串，而不会实际执行转换。 在这里，你实质上是指出*查询字符串值是否可以转换为整数 ...* 。

另一个潜在问题是查找不存在的电影。 用于获取电影的代码如下所示：

[!code-csharp[Main](updating-data/samples/sample16.cs)]

如果将 `movieId` 值传递到与实际电影不对应的 `QuerySingle` 方法，则不会返回任何内容，后面的语句（例如 `title=row.Title`）将导致错误。

同样，这也是一个简单的修补程序。 如果 `db.QuerySingle` 方法未返回任何结果，则 `row` 变量将为 null。 因此，你可以在尝试从 `row` 变量获取值之前检查该变量是否为 null。 下面的代码在获取 `row` 对象外的值的语句周围添加 `if` 块：

[!code-csharp[Main](updating-data/samples/sample17.cs)]

通过这两个额外的验证测试，页面就变得更具项目符号。 `!IsPost` 分支的完整代码现在如下例所示：

[!code-csharp[Main](updating-data/samples/sample18.cs)]

请注意，此任务更适合用于 `else` 块。 如果测试未通过，则 `else` 会阻止设置错误消息。

## <a name="adding-a-link-to-return-to-the-movies-page"></a>添加链接以返回到电影页面

最后和有用的详细信息是将链接添加回*电影*页面。 在普通事件流中，用户将从 "*电影*" 页开始，并单击 "**编辑**" 链接。 这会将它们带入*EditMovie*页面，用户可以在其中编辑电影并单击按钮。 代码处理更改后，会重定向回*电影*页面。

但是：

- 用户可能决定不更改任何内容。
- 用户可能已获得此页面，而没有首先单击*电影*页面中的**编辑**链接。

无论采用哪种方式，都要使它们更易于返回到主列表。 这是一个简单的修复 &mdash; 在标记中的结束 `</form>` 标记后添加以下标记：

[!code-html[Main](updating-data/samples/sample19.html)]

此标记对你在其他地方看到的 `<a>` 元素使用相同的语法。 URL 包括 "网站的根" 这 `~`。

## <a name="testing-the-movie-update-process"></a>测试电影更新过程

现在可以测试了。 运行 "*电影*" 页，然后单击电影旁边的 "**编辑**"。 当 " *EditMovie* " 页出现时，对电影进行更改，然后单击 "**提交更改**"。 显示电影列表时，请确保显示所做的更改。

若要确保验证正常工作，请单击 "**编辑**其他电影"。 转到 " *EditMovie* " 页后，请清除 "**流派**" 字段（或 "**年份**" 字段或两者），并尝试提交更改。 您将看到一个错误，如您所料：

![显示验证错误的编辑电影页面](updating-data/_static/image4.png)

单击 "**返回到电影列表**" 链接放弃您的更改并返回到*电影*页面。

## <a name="coming-up-next"></a>下一步

在下一教程中，你将了解如何删除电影记录。

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>完整的电影页面列表（已更新为编辑链接）

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>编辑电影页面的完成页面列表

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](../../getting-started/introducing-razor-syntax-c.md)
- W3Schools 站点上的[SQL UPDATE 语句](http://www.w3schools.com/sql/sql_update.asp)

> [!div class="step-by-step"]
> [上一页](entering-data.md)
> [下一页](deleting-data.md)
