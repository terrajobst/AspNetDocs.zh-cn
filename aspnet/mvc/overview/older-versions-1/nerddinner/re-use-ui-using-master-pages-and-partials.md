---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用母版页和分区重复使用 UI |Microsoft Docs
author: microsoft
description: 步骤7介绍了如何在视图模板中应用 "晾干原则" 以消除代码重复，使用分部视图模板和母版页。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468722"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>使用母版页和部分重用 UI

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第7步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤7介绍了如何在视图模板中应用 "晾干原则" 以消除代码重复，使用分部视图模板和母版页。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner 步骤7：分区和母版页

MVC 所涉及的设计原则之一是 "不重复自己" 原则（通常称为 "干燥"）。 晾干设计有助于消除代码和逻辑的重复，最终使应用程序更快地进行构建和维护。

我们已经了解了在我们的多个 NerdDinner 方案中应用的晾干原则。 几个示例：我们的验证逻辑是在模型层中实现的，这使其能够在控制器的编辑和创建方案中强制执行;我们正在跨编辑、详细信息和删除操作方法重复使用 "NotFound" 视图模板;我们正在将约定命名模式与我们的视图模板结合使用，这样就无需在调用 View （） helper 方法时显式指定名称;同时，我们还将为 "编辑" 和 "创建" 操作方案重复使用 DinnerFormViewModel 类。

现在，我们来看看如何在视图模板中应用 "晾干原则" 来消除代码重复。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>重新访问编辑和创建视图模板

目前，我们使用两个不同的视图模板： "Edit .aspx" 和 "创建 .aspx"-显示晚餐窗体 UI。 快速直观地比较它们重点介绍它们的相似之处。 "创建窗体" 如下所示：

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

下面是 "编辑" 窗体的外观：

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

这不是什么不同？ 除了标题文本和标题文本，窗体布局和输入控件都是相同的。

如果我们打开 "Edit .aspx" 和 "创建 .aspx" 视图模板，则会发现它们包含完全相同的窗体布局和输入控制代码。 这种重复意味着，我们最终需要在引入或更改新晚餐财产时进行两次更改-这不是好的。

### <a name="using-partial-view-templates"></a>使用分部视图模板

ASP.NET MVC 支持定义 "分部视图" 模板的功能，这些模板可用于封装页面子部分的视图呈现逻辑。 "分区" 提供一种将视图呈现逻辑定义一次的有效方法，然后在应用程序的多个位置重复使用它。

为了帮助 "晾干" 我们的 "编辑 .aspx" 和 "创建 .aspx" 视图模板重复，我们可以创建一个名为 "DinnerForm" 的分部视图模板，该模板封装了这两个窗体布局和公用的输入元素。 为此，请右键单击/Views/Dinners 目录，然后选择 "添加&gt;视图" 菜单命令：

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

这会显示 "添加视图" 对话框。 我们将为要创建的新视图命名为 "DinnerForm"，在对话框中选择 "创建分部视图" 复选框，并指示我们将向其传递一个 DinnerFormViewModel 类：

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建一个新的 "DinnerForm" 视图模板。

然后，可以将重复的窗体布局/输入控件代码从我们的 "Edit .aspx/Create .aspx" 视图模板复制/粘贴到新的 "DinnerForm" 分部视图模板：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

然后，我们可以更新编辑和创建视图模板来调用 DinnerForm 部分模板，并消除窗体复制。 可以通过在视图模板中调用 RenderPartial （"DinnerForm"）来实现此目的：

##### <a name="createaspx"></a>创建 .aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

调用 RenderPartial 时，可以显式限定所需的部分模板的路径（例如： ~ Views/就/DinnerForm）。 然而，在上面的代码中，我们在 ASP.NET MVC 中利用了基于约定的命名模式，并且只是将 "DinnerForm" 指定为要呈现的部分的名称。 如果执行此操作，ASP.NET MVC 将首先在基于约定的视图目录中查找（对于 DinnersController，这将是/Views/Dinners）。 如果未找到部分模板，它将在/Views/Shared 目录中查找它。

如果调用 RenderPartial （）时只使用分部视图的名称，则 ASP.NET MVC 将向分部视图传递调用视图模板所使用的同一个模型和 ViewData 字典对象。 另外，还存在 RenderPartial （）的重载版本，使你能够传递替代模型对象和/或 ViewData 字典，使分部视图可以使用。 这对于只需传递完整模型/ViewModel 的子集的情况非常有用。

| **边主题：为什么 &lt;%%&gt; 而不是 &lt;% =%&gt;？** |
| --- |
| 你可能已注意到上面的代码之一是，在调用 RenderPartial （）时，我们使用的是 &lt;%%&gt; 块，而不是 &lt;% =%&gt; 块。 ASP.NET 中 &lt;% =%&gt; 块指示开发人员要呈现指定的值（例如： &lt;% = "Hello"%&gt; 会呈现 "Hello"）。 &lt;%%&gt; 块，而是指示开发人员想要执行代码，并且必须显式执行其中呈现的任何输出（例如： &lt;% Response （"Hello"）%&gt;。 由于 RenderPartial （）方法不返回字符串，而是将内容直接输出到调用视图模板的输出流，因此我们使用了 &lt;%%&gt; 块的原因。 它出于性能效率原因而执行此操作，这样做可以避免创建（可能非常大）的临时字符串对象。 这会减少内存使用量并提高总体应用程序吞吐量。 使用 RenderPartial （）时，一个常见的错误是在调用结束时，忘记在调用末尾添加一个分号，因为它位于 &lt;%%&gt; 块内。 例如，以下代码将导致编译器错误： &lt;% RenderPartial （"DinnerForm"）%&gt; 而不需要编写： &lt;% RenderPartial （"DinnerForm"）;%&gt; 这是因为 &lt;%%&gt; 块是自包含的代码语句，而使用C#的代码语句需要以分号结束。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>使用分部视图模板来阐明代码

我们创建了 "DinnerForm" 分部视图模板，以避免在多个位置复制视图呈现逻辑。 这是创建分部视图模板最常见的原因。

有时，即使只是在单个位置调用分部视图，也仍有必要创建分部视图。 在将视图呈现逻辑提取并分区到一个或多个命名的分部模板中时，非常复杂的视图模板通常会更易于阅读。

例如，从我们的项目中的站点 master 文件考虑以下代码片段（我们将在稍后介绍）。 代码相对简单明了，因为显示屏幕右上角的 "登录/注销" 链接的逻辑封装在 "Logonusercontrol.ascx" 部分中：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

当你发现在视图模板内尝试理解 html/代码标记时感到困惑时，请考虑在将其中一些部分提取并重构为命名完好的分部视图时，它是否更清晰。

### <a name="master-pages"></a>母版页

除了支持分部视图以外，ASP.NET MVC 还支持创建 "母版页" 模板的功能，这些模板可用于定义站点的通用布局和顶级 html。 然后，可以将内容占位符控件添加到母版页，以标识可由视图覆盖或 "填充" 的可替换区域。 这提供了一种非常有效的方法，可在应用程序中应用通用布局。

默认情况下，新的 ASP.NET MVC 项目会自动添加一个母版页模板。 此母版页的名称为 "\Views\Shared\"，位于 "" 文件夹中：

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

默认网站 .master 文件如下所示。 它定义了站点的外部 html，以及顶部导航菜单。 它包含两个可替换内容占位符控件–一个用于标题，另一个用于替换页面的主要内容：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

我们为 NerdDinner 应用程序创建的所有视图模板（"列表"、"详细信息"、"编辑"、"创建"、"NotFound" 等）都基于此站点。主模板。 这是通过在使用 "添加视图" 对话框创建视图时默认添加到 &lt;% @ Page%&gt; 指令的 "MasterPageFile" 属性指示的：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

这意味着我们可以更改站点的主内容，并在呈现任何视图模板时自动应用和使用这些更改。

接下来，我们将更新我们的站点。 master 的标头部分，使我们的应用程序的标头为 "NerdDinner" 而不是 "我的 MVC 应用程序"。 接下来，我们将更新导航菜单，以便第一个选项卡为 "查找晚餐" （由 HomeController 的 Index （）操作方法处理），并让我们添加一个名为 "承载晚餐" 的新选项卡（由 DinnersController 的 Create （）操作方法处理）：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

当我们保存站点 .master 文件并刷新浏览器时，我们将看到标题更改显示在应用程序内的所有视图中。 例如:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

并带有 */Dinners/Edit/[id]* URL：

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>下一步

分区和母版页提供了非常灵活的选项，使您可以对视图进行清晰的组织。 你会发现它们有助于避免重复查看内容/代码，并使你的视图模板更易于阅读和维护。

现在，让我们重新访问我们前面构建的列表方案，并启用可伸缩分页支持。

> [!div class="step-by-step"]
> [上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)
