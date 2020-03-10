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
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a>ASP.NET 网页-删除数据库数据简介

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程介绍如何删除单个数据库条目。 它假定您已完成了[在 ASP.NET 网页中更新数据库数据](updating-data.md)的系列。
> 
> 学习内容：
> 
> - 如何从记录列表中选择单个记录。
> - 如何从数据库中删除单个记录。
> - 如何检查是否已在窗体中单击了特定按钮。
>   
> 
> 介绍的功能/技术：
> 
> - `WebGrid` 帮助程序。
> - SQL `Delete` 命令。
> - 用于运行 SQL `Delete` 命令的 `Database.Execute` 方法。

## <a name="what-youll-build"></a>你将生成

在上一教程中，您学习了如何更新现有的数据库记录。 此教程与此类似，不同之处在于，它不会更新记录。 这些过程是相同的，只是删除操作更简单，因此本教程将简短。

在 "*电影*" 页面中，你将更新 `WebGrid` 帮助程序，以便它在每个电影旁显示一个 "**删除**" 链接，以附带你之前添加的 "**编辑**" 链接。

![显示每个电影的删除链接的电影页面](deleting-data/_static/image1.png)

对于编辑，单击 "**删除**" 链接时，将转到不同的页面，其中的影片信息已在表单中：

![使用显示的电影删除电影页面](deleting-data/_static/image2.png)

然后，您可以单击该按钮以永久删除该记录。

## <a name="adding-a-delete-link-to-the-movie-listing"></a>向电影列表添加 "删除" 链接

首先，将 "**删除**" 链接添加到 `WebGrid` 帮助程序。 此链接类似于在上一教程中添加的 "**编辑**" 链接。

打开*电影. cshtml*文件。

通过添加列来更改页面正文中的 `WebGrid` 标记。 下面是修改后的标记：

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

新列如下所示：

[!code-html[Main](deleting-data/samples/sample2.html)]

网格的配置方式，网格中的 "**编辑**" 列最左侧，"**删除**" 列最右侧。 （现在在 `Year` 列后有一个逗号，以防您没有注意到。）这些链接列的位置没有什么特别之处，您可以轻松地将它们放在一起。 在这种情况下，它们是独立的，使其难以混淆。

![已标记为 "编辑" 和 "详细信息" 链接的电影页面，显示它们不是相邻的](deleting-data/_static/image3.png)

新列显示其文本显示为 "删除" 的链接（`<a>` 元素）。 链接的目标（其 `href` 特性）是最终解析为类似于此 URL 的内容的代码，每个电影的 `id` 值不同：

[!code-css[Main](deleting-data/samples/sample3.css)]

此链接将调用名为*DeleteMovie*的页面，并向其传递所选电影的 ID。

本教程不会详细介绍如何构造此链接，因为它与上一教程中的 "**编辑**" 链接（[更新 ASP.NET 网页中的数据库数据](updating-data.md)）几乎完全相同。

## <a name="creating-the-delete-page"></a>创建 "删除" 页

现在，你可以创建将作为网格中 "**删除**" 链接的目标的页面。

> [!NOTE] 
> 
> **重要提示**第一种方法是先选择要删除的记录，然后使用单独的页面和按钮来确认该过程对于安全性极其重要。 如您在前面的教程中所述，对您的网站进行*任何*更改都应*始终*使用窗体 &mdash; 就是使用 HTTP POST 操作。 如果你只是通过单击链接（即使用 GET 操作）来更改站点，则用户可能会对你的站点发出简单的请求并删除数据。 即使是对你的站点进行索引的搜索引擎爬网程序，也可能会无意中通过以下链接删除数据。
> 
> 当你的应用程序允许用户更改记录时，你必须向用户提供记录以进行编辑。 但你可能想跳过此步骤来删除记录。 不过，请不要跳过该步骤。 （这也有助于用户查看记录并确认他们正在删除所需的记录。）
> 
> 在后续教程中，你将了解如何添加登录功能，以便用户必须在删除记录前登录。

创建一个名为*DeleteMovie*的页，并将文件中的内容替换为以下标记：

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

此标记类似于*EditMovie*页，不同之处`<input type="text">`在于标记包含 `<span>` 元素。 这里没有任何要编辑的内容。 您所要做的只是显示电影详细信息，以便用户可以确保正在删除正确的电影。

标记已经包含一个链接，该链接使用户能够返回到电影列表页。

在*EditMovie*页中，所选电影的 ID 存储在隐藏字段中。 （它在第一个位置作为查询字符串值传递到页中。）有一个 `Html.ValidationSummary` 调用会显示验证错误。 在这种情况下，此错误可能是没有电影 ID 传递到页面，或者电影 ID 无效。 如果在未首先在*电影*页面中选择电影的情况下运行此页，则可能会发生这种情况。

按钮标题为**删除电影**，其 name 属性设置为 `buttonDelete`。 将在代码中使用 `name` 特性来标识提交窗体的按钮。

需要将代码写入1）在页面第一次显示时读取电影详细信息，2）在用户单击按钮时实际删除影片。

## <a name="adding-code-to-read-a-single-movie"></a>添加代码以读取单个电影

在*DeleteMovie*页的顶部，添加以下代码块：

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

此标记与*EditMovie*页面中对应的代码相同。 它从查询字符串获取影片 ID 并使用该 ID 从数据库中读取记录。 此代码包括验证测试（`IsInt()` 和 `row != null`），以确保传递给页面的电影 ID 有效。

请记住，此代码只应在页面首次运行时运行。 当用户单击 "**删除电影**" 按钮时，不希望从数据库重新读取电影记录。 因此，*如果请求不是 post 操作（窗体提交）* ，则读取电影的代码会在测试中显示 `if(!IsPost)` &mdash;。

## <a name="adding-code-to-delete-the-selected-movie"></a>添加代码以删除所选电影

若要在用户单击按钮时删除电影，请将以下代码添加到 `@` 块的右大括号内：

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

此代码类似于用于更新现有记录但更简单的代码。 此代码基本运行 SQL `Delete` 语句。

 在*EditMovie*页中，代码位于 `if(IsPost)` 块中。 这一次，`if()` 条件稍微复杂一些： 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

这里有两种情况。 第一种是提交页面，正如您在 &mdash; `if(IsPost)`之前所看到的那样。

第二个条件是 `!Request["buttonDelete"].IsEmpty()`，这意味着请求具有一个名为 `buttonDelete`的对象。 无可否认，它是测试提交窗体的按钮的间接方法。 如果窗体包含多个提交按钮，则只会在请求中显示所单击按钮的名称。 因此，如果特定按钮的名称显示在请求中 &mdash; 或如代码中所述，如果该按钮不为空 &mdash; 则为提交窗体的按钮。

`&&` 运算符表示 "and" （逻辑 AND）。 因此，整个 `if` 条件为 。

*此请求为 post （不是第一次请求）*  
  
 AND  
  
*"`buttonDelete`"* *按钮是提交窗体的按钮。*

此窗体（事实上，此页）只包含一个按钮，因此，从技术上讲，不需要对 `buttonDelete` 进行其他测试。 但仍需执行将永久删除数据的操作。 因此，您需要确保仅在用户显式请求操作时执行操作。 例如，假设你稍后展开此页面，并向其添加了其他按钮。 即使这样，仅当单击 "`buttonDelete`" 按钮时，删除电影的代码才会运行。

在*EditMovie*页中，从隐藏的字段获取 ID，然后运行 SQL 命令。 `Delete` 语句的语法为：

`DELETE FROM table WHERE ID = value`

包括 `WHERE` 子句和 ID 是至关重要的。 如果省略 WHERE 子句，*将删除表中的所有记录*。 如您所见，您可以使用占位符将 ID 值传递到 SQL 命令。

## <a name="testing-the-movie-delete-process"></a>测试电影删除过程

现在可以测试了。 运行 "*电影*" 页，然后单击电影旁边的 "**删除**"。 出现 " *DeleteMovie* " 页后，单击 "**删除电影**"。

![突出显示 "删除电影" 按钮的 "删除电影" 页面](deleting-data/_static/image4.png)

单击该按钮时，该代码将删除影片并返回到电影列表。 可以在其中搜索已删除的电影，并确认已将其删除。

## <a name="coming-up-next"></a>下一步

下一教程介绍如何为网站上的所有页面生成常见的外观和布局。

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>完整的电影页面列表（已更新为删除链接）

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie 页的完整列表

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](../introducing-razor-syntax-c.md)
- W3Schools 站点上的[SQL DELETE 语句](http://www.w3schools.com/sql/sql_delete.asp)

> [!div class="step-by-step"]
> [上一页](updating-data.md)
> [下一页](layouts.md)
