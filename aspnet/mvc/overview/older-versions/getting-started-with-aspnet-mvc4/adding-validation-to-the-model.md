---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 向模型添加验证 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455953"
---
# <a name="adding-validation-to-the-model"></a>向模型添加验证

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

在本部分中，你将向 `Movie` 模型中添加验证逻辑，并确保每当用户尝试使用应用程序创建或编辑电影时，都会强制执行验证规则。

## <a name="keeping-things-dry"></a>使东西干燥

ASP.NET MVC 的核心设计原则之一是晾干（&quot;不要自我重复&quot;）。 ASP.NET MVC 鼓励您仅指定一次功能或行为，然后让它在应用程序中的任何位置进行反映。 这会减少需要编写的代码量，并使编写的代码更少出错并且更易于维护。

ASP.NET MVC 和实体框架 Code First 提供的验证支持是有效的操作原理示例。 您可以在一个位置（在 model 类中）以声明方式指定验证规则，并在应用程序的任何位置强制执行规则。

让我们看看如何在电影应用程序中利用此验证支持。

## <a name="adding-validation-rules-to-the-movie-model"></a>向影片模型添加验证规则

首先，将一些验证逻辑添加到 `Movie` 类。

打开 Movie.cs 文件。 在该文件的顶部添加引用[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间的 `using` 语句：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

请注意，命名空间不包含 `System.Web`。 DataAnnotations 提供了一组内置验证特性，可通过声明方式应用于任何类或属性。

现在更新 `Movie` 类，以利用内置[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性。 使用以下代码作为应用属性的示例。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

运行应用程序，你将再次收到以下运行时错误：

***创建数据库后，支持 "MovieDBContext" 上下文的模型已发生更改。请考虑使用 Code First 迁移更新数据库（[https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)）。***

我们将使用迁移来更新架构。 生成解决方案，然后打开 "**包管理器控制台**" 窗口并输入以下命令：

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

此命令完成后，Visual Studio 将打开用指定名称（*AddDataAnnotationsMig*）定义新的 `DbMigration` 派生类的类文件，并在 `Up` 方法中查看用于更新架构约束的代码。 `Title` 和 `Genre` 字段不能为 null （也就是说，必须输入值），并且 `Rating` 字段的最大长度为5。

验证特性指定要对应用这些特性的模型属性强制执行的行为。 `Required` 特性指示属性必须具有值;在此示例中，电影必须具有 `Title`、`ReleaseDate`、`Genre`和 `Price` 属性的值才能有效。 `Range` 特性将值限制在指定范围内。 `StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。 内部类型（如 `decimal, int, float, DateTime`）在默认情况下是必需的，不需要 `Required` 属性。

Code First 确保在应用程序将更改保存到数据库中之前，强制执行在模型类上指定的验证规则。 例如，以下代码将在调用 `SaveChanges` 方法时引发异常，因为缺少几个必需的 `Movie` 属性值，并且价格为零（超出有效范围）。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

验证规则由 .NET Framework 自动强制实施有助于提高应用程序的可靠性。 同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。

下面是已更新的*Movie.cs*文件的完整代码列表：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 中的验证错误 UI

重新运行应用程序并导航到 */Movies* URL。

单击 "**新建**" 链接以添加新电影。 用一些无效值填写表单，然后单击 "**创建**" 按钮。

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 若要支持使用逗号（&quot;，&quot;）作为小数点的非英语区域设置的 jQuery 验证，你必须将*全球*化和特定*区域性/全球化. .js*文件（从[https://github.com/jquery/globalize](https://github.com/jquery/globalize) ）和 JavaScript 用于 `Globalize.parseFloat`。 下面的代码演示对 Views\Movies\Edit.cshtml 文件所做的修改，以便与 &quot;fr-fr&quot; 区域性一起使用：

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

请注意窗体自动使用红色边框颜色突出显示包含无效数据的文本框，并在每个文本框旁边发出适当的验证错误消息。 客户端（使用 JavaScript 和 jQuery）和服务器端（若用户禁用 JavaScript）都必定会遇到这些错误。

真正的好处是，您无需在 `MoviesController` 类中或在*Create. cshtml*视图中更改一行代码即可启用此验证 UI。 在本教程前面创建的控制器和视图会自动选取验证规则，这些规则是通过在 `Movie` 模型类的属性上使用验证特性所指定的。

您可能已注意到 `Title` 和 `Genre`属性，则在您提交窗体（单击 "**创建**" 按钮）之前，不会强制执行所需的属性，或在输入字段中输入文本并将其删除。 对于最初为空的字段（例如 "创建" 视图中的字段），并且仅具有所需的属性和其他验证属性，可以执行以下操作来触发验证：

1. 选项卡到字段。
2. 输入一些文本。
3. 退出选项卡。
4. 返回到字段。
5. 删除文本。
6. 退出选项卡。

上述序列会触发所需的验证，而不需要按 "提交" 按钮。 只需点击 "提交" 按钮而不输入任何字段，就会触发客户端验证。 存在客户端验证错误时，不会将表单数据发送到服务器。 可以通过在 HTTP Post 方法中放置一个断点，或使用[fiddler 工具](http://fiddler2.com/fiddler2/)或 IE 9 [F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)来对此进行测试。

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在 "创建视图" 和 "创建操作" 方法中进行验证

你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。 下一条列表显示了 `MovieController` 类中 `Create` 方法的外观。 在本教程的前面部分中创建它们的方式没有改变。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

第一个 (HTTP GET) `Create` 操作方法显示初始的“创建”表单。 第二个 (`[HttpPost]`) 版本处理表单发布。 第二个 `Create` 方法（`HttpPost` 版本）调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。 调用此方法将评估已应用于对象的任何验证特性。 如果对象有验证错误，则 `Create` 方法会重新显示此表单。 如果没有错误，此方法则将新电影保存在数据库中。 在我们使用的电影示例中，**当在客户端检测到验证错误时，表单不会发布到服务器; 第二个**`Create`**方法永远不会被调用**。 如果在浏览器中禁用 JavaScript，则会禁用客户端验证，并且 HTTP POST `Create` 方法会调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。

可以在 `HttpPost Create` 方法中设置断点，并验证方法从未被调用，客户端验证在检测到存在验证错误时不会提交表单数据。 如果在浏览器中禁用 JavaScript，然后提交错误的表单，将触发断点。 在没有 JavaScript 的情况下仍然可以进行完整的验证。 下图显示了如何在 Internet Explorer 中禁用 JavaScript。

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

以下图片显示如何在 FireFox 浏览器中禁用 JavaScript。

![](adding-validation-to-the-model/_static/image5.png)

下图显示了如何在 Chrome 浏览器中禁用 JavaScript。

![](adding-validation-to-the-model/_static/image6.png)

下面是在本教程的前面部分中基架的*Create.* view 模板。 以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

请注意，代码如何使用 `Html.EditorFor` 帮助器来输出每个 `Movie` 属性的 `<input>` 元素。 此帮助器旁边的调用 `Html.ValidationMessageFor` 帮助器方法。 这两个帮助器方法使用由控制器传递到视图的模型对象（在本例中为 `Movie` 对象）。 它们会自动查找在模型上指定的验证属性，并根据需要显示错误消息。

这种方法的真正优点在于，控制器和 Create view 模板都不知道要强制执行的实际验证规则或显示的特定错误消息。 仅可在 `Movie` 类中指定验证规则和错误字符串。 这些相同的验证规则会自动应用到 "编辑" 视图，以及你可能创建的用于编辑模型的任何其他视图模板。

如果要在以后更改验证逻辑，可以通过向模型中添加验证特性（在本示例中，是 `movie` 类），只在一个位置执行此操作。 无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。 这使代码非常简洁，并且更易于维护和改进。 这意味着对 DRY 原则的完全遵守。

## <a name="adding-formatting-to-the-movie-model"></a>向影片模型添加格式设置

打开 Movie.cs 文件并检查  *类*`Movie`。 除了内置的验证特性集外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间还提供格式特性。 已将[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)枚举值应用于发布日期和价格字段。 下面的代码演示具有相应[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性的 `ReleaseDate` 和 `Price` 属性。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性不是验证特性，它们用于告知视图引擎如何呈现 HTML。 在上面的示例中，`DataType.Date` 属性将电影日期显示为日期，而不是时间。 例如，以下[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性不验证数据的格式：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

上面列出的属性仅提供视图引擎对数据进行格式设置的提示（&lt;为 URL 提供&gt;，并为电子邮件 &lt;href =&quot;mailto:EmailAddress&quot;。&gt; 您可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性来验证数据的格式。

使用 `DataType` 特性的另一种方法是，可以显式设置[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下面的代码显示了 "发布日期" 属性，其中包含日期格式字符串（即 &quot;d&quot;）。 使用此来指定你不希望时间作为发布日期的一部分。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

完整的 `Movie` 类如下所示。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

运行应用程序并浏览到 `Movies` 控制器。 发布日期和价格格式良好。 下图显示了使用 &quot;fr-fr&quot; 作为区域性的发布日期和价格。

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

下图显示了以默认区域性（美国英语）显示的相同数据。

![](adding-validation-to-the-model/_static/image8.png)

在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。

> [!div class="step-by-step"]
> [上一页](adding-a-new-field-to-the-movie-model-and-table.md)
> [下一页](examining-the-details-and-delete-methods.md)
