---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第5部分：编辑窗体和模板化 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第5部分涵盖编辑窗体和模板化。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450908"
---
# <a name="part-5-edit-forms-and-templating"></a>第5部分：编辑窗体和模板化

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。
> 
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第5部分涵盖编辑窗体和模板化。

在过去的章节中，我们从数据库加载数据并显示数据。 在本章中，我们还将启用数据编辑。

## <a name="creating-the-storemanagercontroller"></a>创建 StoreManagerController

首先，我们将创建一个名为**StoreManagerController**的新控制器。 对于这一控制器，我们将利用 ASP.NET MVC 3 工具更新中提供的基架功能。 设置 "添加控制器" 对话框的选项，如下所示。

![](mvc-music-store-part-5/_static/image1.png)

当你单击 "添加" 按钮时，你将看到 ASP.NET MVC 3 基架机制为你执行了很好的工作：

- 它使用本地实体框架变量创建新的 StoreManagerController
- 它将 StoreManager 文件夹添加到项目的 Views 文件夹中
- 它向唱片集类添加了 Create. cshtml、Delete. cshtml、Details、node.js、和 Index。

![](mvc-music-store-part-5/_static/image2.png)

新的 StoreManager 控制器类包括 CRUD （创建、读取、更新、删除）控制器操作，这些操作知道如何使用唱片集模型类，并使用我们的实体框架上下文进行数据库访问。

## <a name="modifying-a-scaffolded-view"></a>修改基架视图

请务必记住，尽管此代码是为我们生成的，但它是标准的 ASP.NET MVC 代码，就像我们在本教程中编写的一样。 它旨在节省编写样板控制器代码和手动创建强类型视图所需的时间，但这并不是你在可怕警告的注释中所看到的生成代码的类型。编写. 这是你的代码，你应更改它。

接下来，让我们从快速编辑 StoreManager 索引视图（/Views/StoreManager/Index.cshtml）开始。 此视图将显示一个表，其中列出了使用 "编辑/详细信息/删除" 链接的商店中的专辑，并包括唱片集的公共属性。 我们将删除 AlbumArtUrl 字段，因为它在此显示中不太有用。 在视图代码 &lt;表&gt; 部分中，删除围绕 AlbumArtUrl 引用 &lt;的&gt; 和 &lt;td&gt; 元素，如下所示：

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

修改后的视图代码将如下所示：

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>第一次查看存储管理器

现在，运行应用程序并浏览到/StoreManager/。 这会显示刚刚修改的存储管理器索引，并显示存储中具有要编辑、详细信息和删除链接的唱片集列表。

![](mvc-music-store-part-5/_static/image3.png)

单击 "编辑" 链接将显示包含唱片集字段的编辑窗体，包括用于流派和艺术家的下拉列表。

![](mvc-music-store-part-5/_static/image4.png)

单击底部的 "返回列表" 链接，然后单击唱片集的详细信息链接。 这将显示单个唱片集的详细信息。

![](mvc-music-store-part-5/_static/image5.png)

再次单击 "返回列表" 链接，然后单击 "删除" 链接。 此时将显示一个确认对话框，其中显示了唱片集详细信息，并询问是否确实要删除它。

![](mvc-music-store-part-5/_static/image6.png)

单击底部的 "删除" 按钮将删除该唱片集，并返回到 "索引" 页，其中显示了已删除的唱片集。

我们并不是使用存储管理器完成的，但我们有工作控制器和查看代码，使 CRUD 操作开始。

## <a name="looking-at-the-store-manager-controller-code"></a>查看存储管理器控制器代码

存储管理器控制器包含大量的代码。 接下来，从上到下。 控制器包括 MVC 控制器的一些标准命名空间，以及对模型命名空间的引用。 控制器具有 MusicStoreEntities 的专用实例，每个控制器操作都使用该实例来进行数据访问。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>存储管理器索引和详细信息操作

索引视图检索唱片集列表，包括每个唱片集的引用流派和艺术家信息，正如我们先前在处理 Store Browse 方法时看到的一样。 索引视图位于对链接对象的引用之后，因此它可以显示每个唱片集的流派名称和艺术家名称，因此控制器有效并在原始请求中查询此信息。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager 控制器的详细信息控制器操作的工作原理与我们以前使用 Find （）方法按 ID 向唱片集提供的存储控制器详细信息操作完全相同，然后将其返回给视图。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>创建操作方法

创建操作方法与我们目前为止所看到的方法稍有不同，因为它们处理窗体输入。 用户首次访问/StoreManager/Create/时，将显示一个空窗体。 此 HTML 页面将包含一个 &lt;窗体&gt; 元素，其中包含可在其中输入唱片集详细信息的 dropdown 和 textbox 输入元素。

用户填写唱片集格式值后，可以按 "保存" 按钮将这些更改提交回应用程序，以便保存到数据库中。 当用户按下 "保存" 按钮时，&lt;窗体&gt; 会执行 HTTP 回发到/StoreManager/Create/URL，并将 &lt;窗体&gt; 值作为 HTTP POST 的一部分提交。

通过使我们能够在 StoreManagerController 类中实现两个单独的 "创建" 操作方法（一个用于处理最初的 HTTP-GET 浏览到/StoreManager/Create/URL，另一个用于处理提交的更改的 HTTP POST），ASP.NET MVC 使我们可以轻松地将这两个 URL 调用方案的逻辑拆分开来。

### <a name="passing-information-to-a-view-using-viewbag"></a>使用 ViewBag 将信息传递给视图

我们已在本教程的前面部分使用了 ViewBag，但尚未谈论它。 ViewBag 允许我们将信息传递给视图，而无需使用强类型化的模型对象。 在这种情况下，"编辑 HTTP-获取控制器" 操作需要将流派和音乐家列表同时传递给窗体来填充下拉列表，最简单的方法是将其返回为 ViewBag 项。

ViewBag 是动态对象，这意味着你可以在不编写代码的情况下键入 ViewBag 或 ViewBag 来定义这些属性。 在这种情况下，控制器代码使用 ViewBag GenreId 和 ViewBag，这样，使用窗体提交的下拉值将为 GenreId 和 ArtistId，这些值是他们将设置的唱片集属性。

将使用 SelectList 对象将这些下拉值返回到窗体，此对象只是为此目的而构建的。 这是使用如下所示的代码完成的：

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

从操作方法代码中可以看到，三个参数用于创建此对象：

- 下拉列表将显示的项的列表。 请注意，这不只是一个字符串，而是传递一个流派列表。
- 传递给 SelectList 的下一个参数是选定的值。 SelectList 如何知道如何在列表中预先选择一项。 当我们查看 "编辑" 窗体时，这会很容易理解，这非常类似。
- 最终参数是要显示的属性。 在这种情况下，这指示 Genre.Name 属性将显示给用户。

考虑到这一点，HTTP GET Create 操作非常简单-两个 SelectLists 已添加到 ViewBag，并且没有模型对象传递到窗体（因为尚未创建）。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>用于在创建视图中显示下拉的 HTML 帮助器

由于我们已经讨论了下拉值如何传递给视图，接下来让我们快速查看一下视图，查看这些值的显示方式。 在视图代码（/Views/StoreManager/Create.cshtml）中，你将看到执行以下调用以显示流派下拉。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

这称为 HTML 帮助器-一种执行常见视图任务的实用工具方法。 HTML 帮助程序非常适用于保持视图代码的简洁和可读性。 ASP.NET MVC 提供 DropDownList 帮助程序，但正如我们稍后将看到的，我们可以创建自己的用于查看代码的帮助程序，我们将在应用程序中重复使用这些代码。

只需对 DropDownList 调用进行以下两项通知：在何处获取要显示的列表，以及应预先选择的值（如果有）。 第一个参数 GenreId 指示 DropDownList 在模型或 ViewBag 中查找名为 GenreId 的值。 第二个参数用于指示要在下拉列表中以初始方式显示的值。 由于此窗体是 Create 窗体，因此没有要预先选择的值和 String。将传递空值。

### <a name="handling-the-posted-form-values"></a>处理已发布的表单值

如前文所述，有两个与每个窗体相关联的操作方法。 首先处理 HTTP GET 请求，并显示窗体。 第二个处理 HTTP POST 请求，其中包含已提交的窗体值。 请注意，"控制器操作" 有一个 "[HttpPost]" 属性，该属性指示 ASP.NET MVC 只应响应 HTTP POST 请求。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

此操作具有四个责任：

- 1. 读取窗体值
- 2. 检查窗体值是否通过任何验证规则
- 3. 如果表单提交有效，请保存数据并显示更新后的列表
- 4. 如果窗体提交无效，将重新显示具有验证错误的窗体

#### <a name="reading-form-values-with-model-binding"></a>用模型绑定读取窗体值

控制器操作正在处理窗体提交，其中包含 GenreId 和 ArtistId 的值（从下拉列表中）和文本框的标题、价格和 AlbumArtUrl 的值。 尽管可以直接访问窗体值，但更好的方法是使用内置于 ASP.NET MVC 中的模型绑定功能。 当控制器操作采用模型类型作为参数时，ASP.NET MVC 将尝试使用窗体输入（以及路由和查询字符串值）来填充该类型的对象。 它通过查找名称与模型对象的属性匹配的值来实现此目标，例如，设置新的唱片集对象的 GenreId 值时，它会查找名称为 GenreId 的输入。 当使用 ASP.NET MVC 中的标准方法创建视图时，窗体将始终使用属性名称作为输入字段名称进行呈现，因此，字段名称将与之匹配。

#### <a name="validating-the-model"></a>验证模型

使用对 ModelState 的简单调用来验证模型。 我们尚未将任何验证规则添加到我们的唱集类中-我们将立即执行此操作，因此，现在这项检查并不太多了。 重要的是，此 ModelStat 检查将适合我们在我们的模型中进行的验证规则，因此，以后对验证规则的更改不需要对控制器操作代码进行任何更新。

#### <a name="saving-the-submitted-values"></a>保存提交的值

如果表单提交通过验证，则可以将这些值保存到数据库。 对于实体框架，只需将模型添加到 "唱片集" 集合并调用 SaveChanges 即可。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

实体框架生成合适的 SQL 命令来持久保存值。 保存数据后，我们将重定向回唱集列表，以便我们可以看到更新。 这是通过将 RedirectToAction 返回到我们要显示的控制器操作的名称来完成的。 在这种情况下，这是 Index 方法。

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>显示具有验证错误的无效窗体提交

对于无效的窗体输入，会将 dropdown 值添加到 ViewBag （如在 HTTP GET case 中），并将绑定的模型值传递回要显示的视图。 使用 @Html.ValidationMessageFor HTML 帮助器自动显示验证错误。

#### <a name="testing-the-create-form"></a>测试 "创建" 窗体

若要对此进行测试，请运行应用程序并浏览到/StoreManager/Create/-这将显示 StoreController Create HTTP-GET 方法返回的空白窗体。

填写某些值并单击 "创建" 按钮以提交窗体。

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>处理编辑

编辑操作对（HTTP GET 和 HTTP POST）非常类似于我们刚才查看的创建操作方法。 由于编辑方案涉及使用现有唱片集，因此编辑 HTTP-GET 方法会根据通过路由传入的 "id" 参数加载唱片集。 此用于通过 AlbumId 检索唱片集的代码与我们以前在详细信息控制器操作中查看的代码相同。 与创建/HTTP-GET 方法一样，下拉值通过 ViewBag 返回。 这样一来，我们就可以将唱片集作为模型对象返回到视图（强类型化为唱片集类），同时通过 ViewBag 传递附加数据（例如，流派列表）。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

编辑 HTTP POST 操作与创建 HTTP POST 操作非常相似。 唯一的区别是，不是将新的唱片集添加到 db。唱集，我们正在使用 db 查找唱集的当前实例。条目（唱片集），并将其状态设置为 "已修改"。 这会告知实体框架我们正在修改现有的唱片集，而不是创建一个新的。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

通过运行应用程序并浏览到/StoreManger/，然后单击唱片集的编辑链接，我们可以对此进行测试。

![](mvc-music-store-part-5/_static/image9.png)

这会显示由编辑 HTTP-GET 方法显示的编辑窗体。 填写某些值并单击 "保存" 按钮。

![](mvc-music-store-part-5/_static/image10.png)

这会发送窗体，保存值并将我们返回到唱片集列表，其中显示值已更新。

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>处理删除

删除遵循与编辑和创建相同的模式，使用一个控制器操作显示确认窗体，并使用另一个控制器操作来处理窗体提交。

HTTP-获取删除控制器操作与先前的 "存储管理器详细信息" 控制器操作完全相同。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

我们将使用 "删除视图内容" 模板来显示已强类型化为唱片集类型的窗体。

![](mvc-music-store-part-5/_static/image12.png)

"删除" 模板显示了该模型的所有字段，但我们可简化这一点。 将/Views/StoreManager/Delete.cshtml 中的视图代码更改为以下代码。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

这会显示简化的删除确认。

![](mvc-music-store-part-5/_static/image13.png)

单击 "删除" 按钮会使窗体回发到服务器，这将执行 DeleteConfirmed 操作。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

我们的 HTTP POST 删除控制器操作执行以下操作：

- 1. 按 ID 加载唱片集
- 2. 删除相册并保存更改
- 3. 重定向到索引，显示已从列表中删除唱片集

若要对此进行测试，请运行应用程序并浏览到/StoreManager。 从列表中选择一个唱片集，然后单击 "删除" 链接。

![](mvc-music-store-part-5/_static/image14.png)

此时将显示 "删除" 确认屏幕。

![](mvc-music-store-part-5/_static/image15.png)

单击 "删除" 按钮将删除该唱片集并返回到 "商店经理索引" 页，其中显示已删除该唱片集。

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>使用自定义 HTML 帮助程序截断文本

我们的商店经理索引页有一个潜在的问题。 "唱片集标题" 和 "艺术家名称" 属性的长度可能会超出我们的表格格式。 我们将创建自定义 HTML 帮助程序，以便在视图中轻松截断这些属性和其他属性。

![](mvc-music-store-part-5/_static/image17.png)

Razor 的 @helper 语法使创建自己的 helper 函数以便在视图中使用非常简单。 打开/Views/StoreManager/Index.cshtml 视图并直接在 @model 行后添加以下代码。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

此帮助器方法使用一个字符串和最大长度以允许。 如果提供的文本小于指定的长度，则助手会按原样输出该文本。 如果更长，则会截断文本，并呈现 "..."余数。

现在，我们可以使用截断帮助器来确保唱片集标题和艺术家名称属性少于25个字符。 使用新的截断帮助器的完整视图代码如下所示。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

现在，浏览/StoreManager/URL 时，唱片集和标题会保持在最大长度以下。

![](mvc-music-store-part-5/_static/image18.png)

注意：这会显示在一个视图中创建和使用帮助器的简单案例。 若要详细了解如何创建可在整个站点中使用的帮助程序，请参阅我的博客文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-4.md)
> [下一页](mvc-music-store-part-6.md)
