---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD （创建、读取、更新、删除）数据窗体项支持 |Microsoft Docs
author: microsoft
description: 步骤5演示了如何通过支持编辑、创建和删除就，进一步获取我们的 DinnersController 类。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468914"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>提供 CRUD（创建、读取、更新和删除）数据窗体输入支持

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第5步，其中演练了如何使用 ASP.NET MVC 1 构建一个小型的、完整的 web 应用程序。
> 
> 步骤5演示了如何通过支持编辑、创建和删除就，进一步获取我们的 DinnersController 类。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner 步骤5：创建、更新、删除窗体方案

我们引入了控制器和视图，并介绍了如何使用它们来实现站点上就的列表/详细信息体验。 下一步是进一步学习我们的 DinnersController 类，并支持编辑、创建和删除就。

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController 处理的 Url

我们之前向 DinnersController 添加了实现了对两个 Url 的支持的操作方法： */Dinners*和 */Dinners/Details/[id]* 。

| **URL** | **谓词** | **目的** |
| --- | --- | --- |
| *就* | GET | 显示即将发布的就的 HTML 列表。 |
| */Dinners/Details/[id]* | GET | 显示有关特定晚餐的详细信息。 |

现在，我们将添加操作方法来实现另外三个 Url： */Dinners/Edit/[id]* 、 */Dinners/Create*和 */Dinners/Delete/[id]* 。 这些 Url 支持编辑现有的就、创建新的就以及删除就。

我们将支持 HTTP GET 和 HTTP POST 谓词与这些新的 Url 的交互。 对这些 Url 的 HTTP GET 请求将显示数据的初始 HTML 视图（在 "编辑" 的情况下，用晚餐数据填充的窗体，在 "创建" 的情况下为空白窗体，在 "删除" 情况下为删除确认屏幕）。 对这些 Url 发出的 HTTP POST 请求将保存/更新/删除 DinnerRepository （和数据库）中的晚餐数据。

| **URL** | **谓词** | **目的** |
| --- | --- | --- |
| */Dinners/Edit/[id]* | GET | 显示可编辑的 HTML 窗体，其中填充了晚餐数据。 |
| POST | 将特定晚餐的窗体更改保存到数据库。 |
| */Dinners/Create* | GET | 显示允许用户定义新就的空 HTML 窗体。 |
| POST | 创建新晚餐，并将其保存在数据库中。 |
| */Dinners/Delete/[id]* | GET | 显示删除确认屏幕。 |
| POST | 从数据库中删除指定的晚餐。 |

### <a name="edit-support"></a>编辑支持

首先，我们要实现 "编辑" 方案。

#### <a name="the-http-get-edit-action-method"></a>HTTP-获取编辑操作方法

首先，我们将实现编辑操作方法的 HTTP "GET" 行为。 当请求 */Dinners/Edit/[id]* URL 时，将调用此方法。 我们的实现如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上面的代码使用 DinnerRepository 检索晚餐对象。 然后，它使用晚餐对象呈现视图模板。 由于我们未将模板名称显式传递给*view （）* helper 方法，因此它将使用基于约定的默认路径来解析视图模板：/Views/Dinners/Edit.aspx。

现在，创建此视图模板。 为此，我们将在编辑方法中右键单击，然后选择 "添加视图" 上下文菜单命令：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

在 "添加视图" 对话框中，我们将指出我们要将晚餐对象作为其模型传递到我们的视图模板，并选择自动基架 "编辑" 模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们添加新的 "Edit .aspx" 视图模板文件。 它还将在代码编辑器中打开新的 "Edit .aspx" 视图模板–用如下所示的初始 "编辑" 基架实现进行填充：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

让我们对生成的默认 "编辑" 基架进行一些更改，并更新 "编辑视图" 模板，使其包含以下内容（这会删除一些我们不想公开的属性）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

运行应用程序并请求 *"/Dinners/Edit/1"* URL 时，会看到以下页面：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

视图生成的 HTML 标记如下所示。 标准 HTML –带有 &lt;窗体&gt; 元素，该元素在推送 "Save" &lt;输入类型 = "submit"/&gt; 按钮时执行到 */Dinners/Edit/1* URL 的 HTTP POST。 为每个可编辑属性输出了 HTML &lt;输入类型 = "text"/&gt; 元素：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.beginform （）和 .Html （） Html Helper 方法

我们的 "Edit .aspx" 视图模板使用几个 "Html Helper" 方法： ValidationSummary （）、Html.beginform （）、.Html （）和 ValidationMessage （）。 除了为我们生成 HTML 标记之外，这些帮助器方法还提供内置的错误处理和验证支持。

##### <a name="htmlbeginform-helper-method"></a>Html.beginform （） helper 方法

Html.beginform （） helper 方法是在标记中输出 HTML &lt;窗体&gt; 元素的内容。 在我们的 Edit .aspx 视图模板中，你会注意到，在C#使用此方法时，我们正在应用 "using" 语句。 左大括号指示 &lt;窗体&gt; 内容的开头，右大括号表示 &lt;/form&gt; 元素的末尾：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

或者，如果你为这样的方案找到了 "using" 语句方法非自然，则可以使用 Html.beginform （）和 EndForm （）组合（执行相同的操作）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

如果调用不带任何参数的 Html.beginform （），则将导致它输出一个对当前请求的 URL 执行 HTTP POST 的窗体元素。 这就是为什么我们的编辑视图生成 *&lt;窗体 action = "/Dinners/Edit/1" method = "post"&gt;* 元素的原因。 如果要发布到不同的 URL，可以将显式参数传递给 Html.beginform （）。

##### <a name="htmltextbox-helper-method"></a>.Html （） helper 方法

Edit .aspx 视图使用 .Html （） helper 方法输出 &lt;输入类型 = "text"/&gt; 元素：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上面的 Html. TextBox （）方法采用单个参数，该参数用于指定要输出的 &lt;输入类型 = "text"/&gt; 元素的 id/名称特性，以及要从中填充 TextBox 值的模型属性。 例如，我们传递到 "编辑" 视图的晚餐对象的 "Title" 属性值为 ".NET 先期"，因此我们的 Html. TextBox （"Title"）方法调用输出： *&lt;输入 id = "title" name = "title" type = "text" value = "Net.tcp 先期备货"/&gt;* 。

此外，我们还可以使用第一个 Html. TextBox （）参数指定元素的 id/名称，然后将值显式传递为用作第二个参数：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

通常，我们需要对输出的值执行自定义格式设置。 内置于 .NET 中的字符串. Format （）静态方法对于这些方案非常有用。 我们的 "Edit .aspx" 视图模板使用此来设置 EventDate 值（类型为 DateTime 的值）的格式，以便它不会显示时间的秒数：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

可以选择使用 Html. TextBox （）的第三个参数来输出其他 HTML 特性。 下面的代码段演示如何在 &lt;输入类型 = "text"/&gt; 元素上呈现附加大小为 "30" 的属性和类 = "mycssclass" 属性。 请注意，在中C#，如何使用 "@" character because "类" 作为保留关键字来转义类属性的名称：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>实现 HTTP POST 编辑操作方法

现在，我们已实现了编辑操作方法的 HTTP 获取版本。 当用户请求 */Dinners/Edit/1* URL 时，他们将收到如下所示的 HTML 页面：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

按 "保存" 按钮将导致窗体发布到 */Dinners/Edit/1* URL，并使用 HTTP post 谓词提交 HTML &lt;输入&gt; 窗体值。 现在，让我们实现编辑操作方法的 HTTP POST 行为-这将处理保存晚餐。

首先，我们将向 DinnersController 添加一个重载的 "Edit" 操作方法，该方法具有一个 "AcceptVerbs" 属性，指示它处理 HTTP POST 方案：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

将 [AcceptVerbs] 特性应用于重载操作方法时，ASP.NET MVC 会自动根据传入的 HTTP 谓词来处理向相应操作方法发出的请求。 对 */Dinners/Edit/[id]* url 发出的 http POST 请求将跳到上述 Edit 方法，而对 */Dinners/Edit/[id]* url 发出的所有其他 HTTP 谓词请求将发送到我们实现的第一个编辑方法（没有 `[AcceptVerbs]` 属性）。

| **侧面主题：为何通过 HTTP 谓词进行区分？** |
| --- |
| 您可能会问，为什么使用单个 URL 并通过 HTTP 谓词来区分其行为呢？ 为什么不只使用两个单独的 Url 来处理加载和保存编辑更改？ 例如：/Dinners/Edit/[id] 显示初始窗体，并将/Dinners/Save/[id] 用于处理窗体发布以保存该窗体？ 发布两个单独的 Url 的缺点是，在以下情况下，我们将发布到/Dinners/Save/2，然后由于输入错误而需要重新显示 HTML 窗体，最终用户将在其浏览器的地址栏中显示/Dinners/Save/2 URL （因为这是窗体发布到的 URL）。 如果最终用户将此重新显示页面的书签设置为浏览器收藏夹列表，或复制/粘贴该 URL 并将其电子邮件发送给朋友，则他们将最终保存一个以后不起作用的 URL （因为该 URL 依赖于 post 值）。 通过公开单一 URL （如：/Dinners/Edit/[id]）并区分 HTTP 谓词对其进行处理，最终用户可以将编辑页面加入书签，并/或将 URL 发送给其他人。 |

#### <a name="retrieving-form-post-values"></a>检索窗体发布值

可以通过多种方式访问 HTTP POST "编辑" 方法中的已发布表单参数。 一种简单的方法是只使用控制器基类上的 Request 属性访问窗体集合并直接检索已发布的值：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

不过，上述方法稍微详细一些，特别是添加错误处理逻辑。

对于此方案，更好的方法是在控制器基类上利用内置的*UpdateModel （）* helper 方法。 它支持使用传入的窗体参数来更新对象的属性。 它使用反射来确定对象上的属性名称，然后根据客户端提交的输入值自动转换和分配值。

我们可以使用 UpdateModel （）方法来简化使用此代码的 HTTP POST 编辑操作：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

现在，我们可以访问 */Dinners/Edit/1* URL，更改晚餐的标题：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

单击 "保存" 按钮时，将对编辑操作执行窗体发布，并且更新的值将保留在数据库中。 然后，我们将重定向到晚餐的详细信息 URL （将显示新保存的值）：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>处理编辑错误

当前的 HTTP POST 实现工作正常–出现错误时除外。

如果用户编辑窗体时出错，则需要确保窗体重新显示，并显示信息性错误消息，指导他们修复该窗体。 这包括最终用户发布不正确输入（例如：格式错误的日期字符串）的情况，以及输入格式有效但存在业务规则冲突的情况。 出现错误时，窗体应保留用户最初输入的输入数据，以便他们无需手动重填其更改。 此过程应根据需要重复多次，直至窗体成功完成。

ASP.NET MVC 包括一些极好的内置功能，这些功能可简化错误处理并使其变得简单。 若要在操作中查看这些功能，请将编辑操作方法更新为以下代码：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上面的代码与我们以前的实现类似，只是我们正在包装工作的 try/catch 错误处理块。 如果在调用 UpdateModel （）时出现异常，或当我们尝试并保存 DinnerRepository 时（如果我们尝试保存的晚餐对象由于模型中的规则冲突而无效，将引发异常），我们的 catch 错误处理块将运行. 在此示例中，我们将遍历晚餐对象中存在的任何规则冲突，并将其添加到 ModelState 对象（我们稍后将对此进行讨论）。 然后重新显示视图。

若要查看此工作，请重新运行该应用程序，编辑晚餐，并将其更改为具有空标题，EventDate 为 "假"，并使用英国电话号码，并使用美国国家/地区值。 当我们按下 "保存" 按钮时，我们的 HTTP POST 编辑方法将不能保存晚餐（因为存在错误）并将重新显示表单：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

应用程序的错误体验非常不错。 具有无效输入的文本元素以红色突出显示，并向最终用户显示验证错误消息。 窗体还会保留用户最初输入的输入数据，从而无需重新填充任何内容。

您可能会问，这是不是吗？ "标题"、"EventDate" 和 "ContactPhone" 文本框的显示效果如何，并知道是否输出最初输入的用户值？ 如何在顶部列表中显示错误消息？ 好消息是，这种情况并不是因为，因为我们使用了一些内置的 ASP.NET MVC 功能，使输入验证和错误处理方案变得很简单。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>了解 ModelState 和验证 HTML 帮助器方法

控制器类具有一个 "ModelState" 属性集合，它提供了一种方法，用于指示将模型对象传递到视图时存在错误。 ModelState 集合中的错误条目标识包含问题的模型属性的名称（例如： "Title"、"EventDate" 或 "ContactPhone"），并允许指定用户友好的错误消息（例如： "需要标题"）。

当尝试将窗体值分配给模型对象的属性时， *UpdateModel （）* helper 方法会自动填充 ModelState 集合。 例如，晚餐对象的 EventDate 属性的类型为 DateTime。 在上述方案中，如果 UpdateModel （）方法无法将字符串值 "假" 赋给它，则 UpdateModel （）方法会将一个条目添加到 ModelState 集合，指示该属性发生了分配错误。

开发人员还可以编写代码，以显式将错误条目添加到 ModelState 集合中，如我们在我们的 "catch" 错误处理块中执行的操作。晚餐对象：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Html Helper 与 ModelState 的集成

HTML 帮助器方法（如 Html. TextBox （））-在呈现输出时检查 ModelState 集合。 如果该项存在错误，它们将呈现用户输入的值和 CSS 错误类。

例如，在我们的 "编辑" 视图中，我们使用 Html. TextBox （） helper 方法呈现晚餐对象的 EventDate：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

当在错误情况下呈现视图时，Html. TextBox （）方法检查了 ModelState 集合，以查看是否存在与晚餐对象的 "EventDate" 属性相关联的任何错误。 当它确定出现错误时，它将提交的用户输入（"假"）作为值，并将 css 错误类添加到它生成的 &lt;输入类型 = "textbox"/&gt; 标记：

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

您可以自定义 css 错误类的外观，以查找所需的外观。 默认的 CSS 错误类– "输入验证-错误" –在 *\content\site.css*样式表中定义，如下所示：

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

此 CSS 规则导致无效输入元素突出显示，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>ValidationMessage （） Helper 方法

ValidationMessage （） helper 方法可用于输出与特定模型属性关联的 ModelState 错误消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上面的代码输出： *&lt;范围 = "字段验证-错误"&gt; 值 "虚假" 无效，&lt;/span&gt;*

ValidationMessage （） helper 方法还支持第二个参数，使开发人员能够重写显示的错误文本消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上述代码输出：在 EventDate 属性存在错误时， *&lt;跨类 = "字段验证-错误"&gt;\*&lt;/span&gt;* 而不是默认错误文本。

##### <a name="htmlvalidationsummary-helper-method"></a>ValidationSummary （） Helper 方法

ValidationSummary （） helper 方法可用于呈现摘要错误消息，该消息附带一个 &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; ModelState 集合中所有详细错误消息的列表：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

ValidationSummary （） helper 方法使用可选的字符串参数，该参数定义要显示在详细错误列表上方的摘要错误消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

您可以选择使用 CSS 来替代 "错误列表" 的外观。

#### <a name="using-a-addruleviolations-helper-method"></a>使用 AddRuleViolations Helper 方法

初始的 HTTP POST 编辑实现使用其 catch 块内的 foreach 语句来循环接管晚餐对象的规则冲突，并将其添加到控制器的 ModelState 集合：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

我们可以通过将 "ControllerHelpers" 类添加到 NerdDinner 项目中来使此代码变得更清晰，并在其中实现 "AddRuleViolations" 扩展方法，将 helper 方法添加到 ASP.NET MVC ModelStateDictionary 类。 此扩展方法可以封装用 RuleViolation 错误列表填充 ModelStateDictionary 所需的逻辑：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

接下来，我们可以更新 HTTP POST 编辑操作方法，使用此扩展方法，通过晚餐规则违规填充 ModelState 集合。

#### <a name="complete-edit-action-method-implementations"></a>完成编辑操作方法实现

下面的代码实现了编辑方案所需的所有控制器逻辑：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

我们的编辑实现的一个好办法是，我们的控制器类和我们的视图模板都不能了解有关我们的晚餐模型强制执行的特定验证或业务规则的任何信息。 将来，我们可以在我们的模型中添加更多规则，而无需对控制器或视图进行任何代码更改，就可以对其进行更改。 这为我们提供了灵活的灵活性，可以在将来轻松地轻松地改进应用程序要求，只需进行少量的代码更改。

### <a name="create-support"></a>创建支持

我们已经完成了 DinnersController 类的 "编辑" 行为。 现在，让我们继续实现对它的 "创建" 支持-这将使用户能够添加新就。

#### <a name="the-http-get-create-action-method"></a>HTTP 获取创建操作方法

首先，我们将实现创建操作方法的 HTTP "GET" 行为。 当有人访问 */Dinners/Create* URL 时，将调用此方法。 我们的实现如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上面的代码创建一个新的晚餐对象，并将其 EventDate 属性分配为将来一周。 然后，它呈现基于新晚餐对象的视图。 由于我们未将名称显式传递给*view （）* helper 方法，因此它将使用基于约定的默认路径来解析视图模板：/Views/Dinners/Create.aspx。

现在，创建此视图模板。 为此，可以在 "创建操作" 方法中右键单击，然后选择 "添加视图" 上下文菜单命令。 在 "添加视图" 对话框中，我们将指出我们要将晚餐对象传递到视图模板，并选择自动基架 "创建" 模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

单击 "添加" 按钮时，Visual Studio 会将基于基架的新 "Create .aspx" 视图保存到 "\Views\Dinners" 目录中，并在 IDE 中打开它：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

让我们对为我们生成的默认 "创建" 基架文件进行一些更改，并将其修改为如下所示：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

现在，当我们运行应用程序并访问浏览器内的 *"/Dinners/Create"* URL 时，它会在创建操作实现中呈现如下所示的 UI：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>实现 HTTP POST 创建操作方法

我们已经实现了创建操作方法的 HTTP GET 版本。 当用户单击 "保存" 按钮时，它将执行窗体发布到 */Dinners/Create* URL，并使用 HTTP post 谓词提交 HTML &lt;输入&gt; 窗体值。

现在，让我们实现 "创建操作" 方法的 HTTP POST 行为。 首先，我们将向 DinnersController 添加一个重载的 "Create" 操作方法，该方法的 "AcceptVerbs" 属性指示它处理 HTTP POST 方案：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

可以通过多种方式访问已启用 HTTP POST 的 "创建" 方法中的已发布表单参数。

一种方法是创建一个新的晚餐对象，然后使用*UpdateModel （）* helper 方法（与 "编辑" 操作一样），用已发布的表单值来填充它。 接下来，我们可以将其添加到 DinnerRepository，将其保存到数据库中，然后将用户重定向到详细信息操作，以使用下面的代码显示新创建的晚餐：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

此外，我们还可以使用一种方法，在此方法中，我们的 Create （）操作方法将晚餐对象作为方法参数。 然后，ASP.NET MVC 将自动实例化新的晚餐对象，使用表单输入填充其属性，并将其传递给操作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

上述操作方法通过检查 ModelState 属性来验证是否已使用窗体 post 值成功填充晚餐对象。 如果存在输入转换问题（例如： "EventDate" 属性的字符串 "虚假"），则此方法将返回 false; 如果有任何问题，则操作方法将重新出现该窗体。

如果输入值有效，则操作方法会尝试将新晚餐添加并保存到 DinnerRepository。 它在 try/catch 块中包装此工作，如果存在任何业务规则冲突（这会导致 dinnerRepository （）方法引发异常），则会重新出现该窗体。

若要查看此操作中的错误处理行为，可以请求 */Dinners/Create* URL 并填写有关新晚餐的详细信息。 输入或值不正确将导致重新显示 "创建窗体"，其中突出显示的错误如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

请注意，我们的 "创建窗体" 将采用与编辑窗体完全相同的验证和业务规则。 这是因为我们的验证和业务规则是在模型中定义的，而不是嵌入在应用程序的 UI 或控制器中。 这意味着我们稍后可以在一个位置更改/发展验证或业务规则，并在整个应用程序中应用这些规则。 我们不需要在 "编辑" 或 "创建" 操作方法中更改任何代码，即可自动服从任何新规则或对现有规则的修改。

当我们修复输入值并再次单击 "保存" 按钮时，DinnerRepository 的添加将会成功，并且新的晚餐将添加到数据库中。 接下来，我们将重定向到 */Dinners/Details/[id]* URL，其中会显示有关新创建的晚餐的详细信息：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>删除支持

现在，我们将 "删除" 支持添加到我们的 DinnersController。

#### <a name="the-http-get-delete-action-method"></a>HTTP 获取删除操作方法

首先，我们将实现删除操作方法的 HTTP GET 行为。 当有人访问 */Dinners/Delete/[id]* URL 时，将调用此方法。 下面是实现：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

操作方法尝试检索要删除的晚餐。 如果晚餐存在，它将基于晚餐对象呈现视图。 如果该对象不存在（或已删除），则它将返回一个视图，该视图呈现我们之前为我们的 "详细信息" 操作方法创建的 "NotFound" 视图模板。

可以通过在 "删除" 操作方法中右键单击并选择 "添加视图" 上下文菜单命令来创建 "删除" 视图模板。 在 "添加视图" 对话框中，我们将指出我们要将晚餐对象作为其模型传递到我们的视图模板，并选择创建一个空模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们添加新的 "删除 .aspx" 视图模板文件。 我们会将一些 HTML 和代码添加到模板，以实现如下所示的删除确认屏幕：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上面的代码将显示要删除的晚餐的标题，如果最终用户单击其中的 "删除" 按钮，则输出 &lt;窗体&gt; 元素，该元素执行向/Dinners/Delete/[id] URL 的 POST。

当我们运行应用程序并访问有效晚餐对象的 *"/Dinners/Delete/[id]"* URL 时，它将呈现如下所示的 UI：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **侧面主题：为什么要进行 POST？** |
| --- |
| 您可能会问：我们为什么要在我们的 "删除" 确认屏幕中创建 &lt;表单&gt;？ 为什么不只使用标准超链接链接到执行实际删除操作的操作方法？ 原因在于，我们想要小心防范 web 爬网程序和搜索引擎查找 Url，并在出现以下链接时意外导致数据被删除。 基于 HTTP GET 的 Url 被视为 "安全"，以便它们能够访问/爬网，它们应该不遵循 HTTP POST。 一个好的规则是确保始终将破坏性或数据修改操作置于 HTTP POST 请求后面。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>实现 HTTP POST 删除操作方法

现在，我们已实现了 "删除" 操作方法的 HTTP 获取版本，其中显示了 "删除" 确认屏幕。 当最终用户单击 "删除" 按钮时，它将对 */Dinners/Dinner/[id]* URL 执行窗体发布。

现在，让我们使用下面的代码来实现 delete 操作方法的 HTTP "POST" 行为：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

删除操作方法的 HTTP POST 版本尝试检索要删除的晚餐对象。 如果找不到它（因为已删除），则它将呈现我们的 "NotFound" 模板。 如果找到晚餐，则会将其从 DinnerRepository 中删除。 然后呈现 "已删除" 模板。

若要实现 "已删除" 模板，我们将在操作方法中右键单击，然后选择 "添加视图" 上下文菜单。 我们会将视图命名为 "已删除"，并将其命名为空模板（而不采用强类型模型对象）。 然后，将一些 HTML 内容添加到其中：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

现在，当我们运行应用程序并访问有效晚餐对象的 *"/Dinners/Delete/[id]"* URL 时，它将呈现我们的晚餐删除确认屏幕，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

当我们单击 "删除" 按钮时，它将对 */Dinners/Delete/[id]* URL 执行 HTTP POST，该 URL 将从数据库中删除晚餐，并显示 "已删除" 视图模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>模型绑定安全性

我们讨论了两种不同的方法来使用 ASP.NET MVC 的内置模型绑定功能。 第一种方法是使用 UpdateModel （）方法来更新现有模型对象上的属性，第二种方法是使用 ASP.NET MVC 支持将模型对象作为操作方法参数传入。 这两种方法都非常强大且非常有用。

此功能还具有 it 责任。 在接受任何用户输入时始终偏执安全，这一点很重要，在将对象绑定到表单输入时也是如此。 应注意始终对任何用户输入的值进行 HTML 编码，以避免 HTML 和 JavaScript 注入攻击，并小心 SQL 注入式攻击（注意：我们使用的是应用程序的 LINQ to SQL，这会自动对参数进行编码，以防止出现这种情况攻击类型）。 切勿单独依赖于客户端验证，始终使用服务器端验证来防止黑客尝试发送虚假值。

另外一个安全项目，请确保你在使用 ASP.NET MVC 的绑定功能时要考虑的是要绑定的对象的范围。 具体而言，你需要确保了解你允许绑定的属性的安全影响，并确保仅允许更新最终用户可以更新的那些属性，这一点非常明显。

默认情况下，UpdateModel （）方法将尝试更新与传入窗体参数值匹配的模型对象的所有属性。 同样，作为操作方法参数传递的对象也会在默认情况下通过窗体参数设置其所有属性。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>按使用情况锁定绑定

可以通过提供可更新的属性的显式 "包含列表"，按使用情况锁定绑定策略。 为此，可将额外的字符串数组参数传递给 UpdateModel （）方法，如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

作为操作方法参数传递的对象还支持 "[Bind]" 属性，该属性可指定如下所示的 "允许" 属性的 "包含列表"：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>基于类型锁定绑定

你还可以基于每个类型锁定绑定规则。 这允许您指定一次绑定规则，然后将它们应用于所有控制器和操作方法的所有方案（包括 UpdateModel 和操作方法参数方案）。

您可以自定义每种类型的绑定规则，方法是将 [Bind] 特性添加到类型上，或在应用程序的 global.asax 文件中注册它（对于不属于该类型的方案非常有用）。 然后，可以使用 Bind 特性的 Include 和 Exclude 属性控制哪些属性可绑定到特定类或接口。

我们将为 NerdDinner 应用程序中的晚餐类使用此技术，并向其添加一个 "[Bind]" 属性，将可绑定属性列表限制如下：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

请注意，我们不允许通过绑定操作 RSVPs 集合，也不允许通过绑定设置 DinnerID 或 HostedBy 属性。 出于安全原因，我们将改为仅使用操作方法中的显式代码来操作这些特定属性。

### <a name="crud-wrap-up"></a>CRUD 向上环绕

ASP.NET MVC 包含许多可帮助实现窗体发布方案的内置功能。 我们使用了各种功能，在我们的 DinnerRepository 上提供 CRUD UI 支持。

我们使用以模型为中心的方法来实现我们的应用程序。 这意味着，所有验证和业务规则逻辑都是在模型层中定义的，而不是在我们的控制器或视图中定义的。 我们的控制器类和我们的视图模板都不知道我们的晚餐模型类强制执行的特定业务规则。

这会使应用程序体系结构保持整洁，并使测试更容易。 将来，我们可以将其他业务规则添加到我们的模型层中，而无需对控制器或视图*进行任何代码更改*，即可获得支持。 这将为我们提供大量的灵活性，以便在将来发展和更改应用程序。

我们的 DinnersController 现在启用晚餐列表/详细信息，以及创建、编辑和删除支持。 可以在下面找到类的完整代码：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>下一步

现在，我们在 DinnersController 类中拥有基本的 CRUD （创建、读取、更新和删除）支持。

现在我们来看看如何使用 ViewData 和 ViewModel 类在窗体上实现甚至更丰富的 UI。

> [!div class="step-by-step"]
> [上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)
