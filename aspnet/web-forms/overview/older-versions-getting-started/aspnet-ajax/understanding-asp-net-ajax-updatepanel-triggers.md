---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: 了解 ASP.NET AJAX UpdatePanel 触发器 |Microsoft Docs
author: scottcate
description: 在 Visual Studio 中的标记编辑器中工作时，你可能会注意到（从 IntelliSense）有一个 UpdatePanel 控件的子元素。 符合之一 。
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: b1cc869f373d4f8283b4d92af74707c3f11fef61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440540"
---
# <a name="understanding-aspnet-ajax-updatepanel-triggers"></a>了解 ASP.NET AJAX UpdatePanel 触发器

作者： [Scott Cate](https://github.com/scottcate)

[下载 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> 在 Visual Studio 中的标记编辑器中工作时，你可能会注意到（从 IntelliSense）有一个 UpdatePanel 控件的子元素。 其中一个是触发器元素，它指定页面上的控件（如果使用的是用户控件，则为用户控件），该元素将触发元素所在的 UpdatePanel 控件的部分呈现。

## <a name="introduction"></a>简介

Microsoft 的 ASP.NET 技术引入了面向对象的和事件驱动的编程模型，并将其与编译的代码的优势结合起来。 但是，它的服务器端处理模型在技术中有一些固有的缺点，其中许多功能都可以通过 Microsoft ASP.NET 3.5 AJAX 扩展中包含的新功能来解决。 这些扩展可实现许多新的丰富客户端功能，包括页面的部分呈现，无需整页刷新、通过客户端脚本访问 Web 服务的能力（包括 ASP.NET 分析 API）和广泛的客户端 API用于镜像在 ASP.NET 服务器端控制集内发现的许多控制方案。

本白皮书检查 ASP.NET AJAX `UpdatePanel` 组件的 XML 触发器功能。 XML 触发器可以对组件进行精细的控制，这些组件可能会导致特定 UpdatePanel 控件的部分呈现。

本白皮书基于 .NET Framework 3.5 和 Visual Studio 2008 的 Beta 2 版本。 ASP.NET AJAX 扩展（以前面向 ASP.NET 2.0 的附加程序集）现在已集成到 .NET Framework 基类库中。 本白皮书还假设你将使用 Visual Studio 2008，而不是 Visual Web Developer Express，并将根据 Visual Studio 的用户界面提供演练（尽管代码列表将完全兼容，而不考虑开发环境）。

## <a name="triggers"></a>*触发器*

给定 UpdatePanel 的触发器默认情况下，会自动包含任何调用回发的子控件，包括将其 `AutoPostBack` 属性设置为**true**的 TextBox 控件。 但是，也可以使用标记以声明方式包含触发器;这是在 UpdatePanel 控件声明的 `<triggers>` 部分中完成的。 尽管可以通过 `Triggers` 集合属性访问触发器，但建议你在运行时（例如，如果控件在设计时不可用）通过使用页面的 ScriptManager 对象的 `RegisterAsyncPostBackControl(Control)` 方法在 `Page_Load` 事件内注册任何分部呈现触发器。 请记住，页面是无状态的，因此你应在每次创建这些控件时重新注册这些控件。

还可以禁用自动子触发器包含（因此，通过将 `ChildrenAsTriggers` 属性设置为**false**，创建回发的子控件不会自动触发部分呈现）。 这使您可以最大限度地分配哪些特定控件可以调用页面呈现，并建议您这样做，以便开发人员选择对事件做出响应，而不是处理可能出现的任何事件。

请注意，当 "UpdateMode" 设置为 "**条件**" 时，如果触发了子 updatepanel 但父对象不是，则只有子 updatepanel 会刷新。 但是，如果刷新了父 UpdatePanel，则还会刷新子 UpdatePanel。

## <a name="the-lttriggersgt-element"></a>*&lt;触发&gt; 元素*

在 Visual Studio 中的标记编辑器中工作时，你可能会注意到（从 IntelliSense）存在 `UpdatePanel` 控件的两个子元素。 最常见到的元素是 `<ContentTemplate>` 元素，该元素实质上封装了将由更新面板（我们正在启用部分呈现的内容）保存的内容。 另一个元素是 `<Triggers>` 元素，该元素指定页面上的控件（如果使用的是用户控件），该元素将触发&gt; 元素的 &lt;触发器的 UpdatePanel 控件的部分呈现。

`<Triggers>` 元素可以包含两个子节点中的任意数量： `<asp:AsyncPostBackTrigger>` 和 `<asp:PostBackTrigger>`。 它们都接受两个属性，`ControlID` 和 `EventName`，并且可以在当前封装单元中指定任何控件（例如，如果您的 UpdatePanel 控件位于 Web 用户控件内，则不应尝试引用用户控件将驻留的页上的控件）。

`<asp:AsyncPostBackTrigger>` 元素特别有用，因为它可以从作为封装的单元中的*任何*updatepanel 控件的子控件（而不仅仅是此触发器所用的 updatepanel）作为子控件的任何事件定向。 因此，可以通过任何控件来触发部分页面更新。

同样，`<asp:PostBackTrigger>` 元素可用于触发部分页面呈现，但需要完全往返服务器的情况。 当控件通常会触发部分页面呈现时（例如，在 UpdatePanel 控件的 `<ContentTemplate>` 元素中存在 `Button` 控件）时，也可以使用此触发器元素强制执行完整页面呈现。 同样，PostBackTrigger 元素可以指定任何控件，该控件是当前封装单元中任何 UpdatePanel 控件的子控件。

## <a name="lttriggersgt-element-reference"></a>*&lt;触发器&gt; 元素引用*

*标记后代：*

| **标记** | **描述** |
| --- | --- |
| &lt;asp： AsyncPostBackTrigger&gt; | 指定一个控件和事件，该控件和事件将导致包含此触发器引用的 UpdatePanel 的部分页面更新。 |
| &lt;asp： PostBackTrigger&gt; | 指定将导致完整页面更新的控件和事件（完整页面刷新）。 此标记可用于在控件将以其他方式触发部分呈现时强制执行完全刷新。 |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*演练：跨 UpdatePanel 触发器*

1. 创建一个新的 ASP.NET 页面，其中包含 ScriptManager 对象集，用于启用部分呈现。 将两个 UpdatePanels 添加到此页-在第一页中，包括标签控件（Label1）和两个按钮控件（Button1 和 Button2）。 Button1 应显示 "单击以更新" 和 "Button2" 应显示 "单击以更新此项" 或沿这些行。 在第二个 UpdatePanel 中，只包括 "标签" 控件（Label2），但将其 "前景色" 属性设置为默认值以外的其他值。
2. 将两个 UpdatePanel 标记的 UpdateMode 属性设置为 "**条件**"。

**列表1： default.aspx 的标记：** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. 在 "Button1" 的 Click 事件处理程序中，将 "Label1" 和 "Label2" 设置为依赖于时间的内容（如 "ToLongTimeString （）"）。 对于 Button2 的 Click 事件处理程序，只将 Label1 设置为与时间相关的值。

**列表2： default.aspx.cs 中的代码隐藏（已剪裁）：** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. 按 F5 生成并运行项目。 请注意，单击 "更新两个面板" 时，两个标签都将更改文本;但是，当你单击 "更新此面板" 时，仅 Label1 更新。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

（[单击以查看完全大小的映像](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png)）

## <a name="under-the-hood"></a>*揭秘*

利用我们刚刚构造的示例，我们可以看看 ASP.NET AJAX 正在做什么，以及如何使用我们的 UpdatePanel 跨面板触发器。 为此，我们将使用生成的页面源 HTML 以及名为 FireBug 的 Mozilla Firefox 扩展，我们可以轻松地检查 AJAX 回发。 我们还将使用 .NET 反射器工具 Lutz Roeder。 这两种工具都可以免费使用，并且可以通过 internet 搜索来找到。

对页面源代码的检查几乎几乎不会显示任何内容;UpdatePanel 控件呈现为 `<div>` 容器，我们可以看到脚本资源包含由 `<asp:ScriptManager>`提供。 此外，还有一些针对 AJAX 客户端脚本库内部的 PageRequestManager 的特定于 AJAX 的特定调用。 最后，我们会看到两个 UpdatePanel 容器，其中一容器 `<input>` 带有呈现为 `<span>` 容器的两个 `<asp:Label>` 控件。 （如果你在 FireBug 中检查 DOM 树，你会注意到标签显示为灰色，指示它们不会产生可见内容）。

单击 "更新此面板" 按钮，可以看到顶部的 UpdatePanel 将更新为当前服务器时间。 在 FireBug 中，选择 "控制台" 选项卡，以便可以检查请求。 首先检查 POST 请求参数：

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

（[单击以查看完全大小的映像](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png)）

请注意，UpdatePanel 通过 ScriptManager1 参数（`UpdatePanel1` 控件 `Button1`）准确指出了服务器端 AJAX 代码所触发的控制树。 现在，单击 "更新两个面板" 按钮。 然后，检查响应，我们将看到一个在字符串中设置的管道分隔的一系列变量;具体而言，我们看到的是最热门的 UpdatePanel `UpdatePanel1`，它将整个 HTML 发送到浏览器。 AJAX 客户端脚本库通过 `.innerHTML` 属性将 UpdatePanel 的原始 HTML 内容替换为新内容，因此服务器以 HTML 格式从服务器发送更改的内容。

现在，单击 "更新两个面板" 按钮，然后检查服务器的结果。 结果非常相似-两个 UpdatePanels 从服务器接收新的 HTML。 与上一次回调一样，将发送额外的页面状态。

正如我们所看到的，因为没有使用特殊代码执行 AJAX 回发，所以 AJAX 客户端脚本库能够截获窗体回发，而无需任何其他代码。 服务器控件自动利用 JavaScript，使其不会自动提交窗体-ASP.NET 自动注入用于窗体验证和状态的代码，主要通过自动脚本资源包含、PostBackOptions 类和 ClientScriptManager 类。

例如，请考虑一个 CheckBox 控件;在 .NET 反射器中检查类反汇编。 为此，请确保已打开 System.web 程序集，然后导航到 `System.Web.UI.WebControls.CheckBox` 类，打开 `RenderInputTag` 方法。 查找检查 `AutoPostBack` 属性的条件：

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

（[单击以查看完全大小的映像](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png)）

如果对 `CheckBox` 控件启用了自动回发（通过 AutoPostBack 属性设置为 true），则生成的 `<input>` 标记将使用其 `onclick` 属性中的 ASP.NET 事件处理脚本来呈现。 然后，截获窗体的提交，将 ASP.NET AJAX 注入到页面 nonintrusively，这有助于避免利用可能不精确的字符串替换可能发生的任何潜在重大更改。 此外，这使得*任何*自定义 ASP.NET 控件都可以利用 ASP.NET AJAX 的强大功能，而无需任何其他代码即可支持其在 UpdatePanel 容器中的使用。

`<triggers>` 功能对应于对 \_updateControls 的 PageRequestManager 调用中初始化的值（请注意，ASP.NET AJAX 客户端脚本库利用了以下划线开头的方法、事件和字段名称被标记为内部，并且不是在库本身的外部使用的约定）。 在此示例中，我们可以观察哪些控件旨在导致 AJAX 回发。

例如，让我们将两个附加控件添加到页面，使一个控件完全在 UpdatePanels 之外，并在 UpdatePanel 中留下一个控件。 我们将在上方的 UpdatePanel 中添加 CheckBox 控件，并删除 DropDownList，其中包含在列表中定义的一些颜色。 下面是新标记：

**列表3：新标记**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

下面是新的代码隐藏：

**列表4：代码隐藏**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

此页面背后的理念是：下拉列表中选择三种颜色之一来显示第二个标签，复选框确定是否为粗体以及标签是否显示日期和时间。 该复选框不会导致 AJAX 更新，但下拉列表应为，即使它不在 UpdatePanel 中。

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

（[单击以查看完全大小的映像](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png)）

正如上面的屏幕截图中所示，要单击的最新按钮是更新此面板的右侧按钮，该按钮更新了与底部时间无关的顶层时间。 此日期在单击之间也处于关闭状态，因为日期在底部标签中可见。 要点是底部标签的颜色：它比标签文本更新了更近，这说明控件状态很重要，用户希望通过 AJAX 回发来保留控件状态。 *但*未更新时间。 在服务器上重新呈现控件时，通过 ASP.NET 运行时所解释的页的 \_\_VIEWSTATE 字段的持久性，自动重新填充该时间。 ASP.NET AJAX 服务器代码无法识别控件所更改的状态的方法;它只是从视图状态中重新填充，然后运行相应的事件。

但应指出的是，我已在页面\_Load 事件中初始化时间，该时间已正确递增。 因此，开发人员应小心地确保适当的代码在相应的事件处理程序中运行，并在适当的时候避免使用页面\_负载。

## <a name="summary"></a>摘要

ASP.NET AJAX Extensions UpdatePanel 控件是通用的，可以利用多种方法来识别应导致其更新的控件事件。 它支持由其子控件自动更新，但也可以响应页面上其他位置的控件事件。

为了降低服务器处理负载的可能，建议将 UpdatePanel 的 `ChildrenAsTriggers` 属性设置为 `false`，并选择该事件，而不是在默认情况下包括在内。 这也会阻止任何不需要的事件引起可能不需要的影响，包括验证和输入字段更改。 这些类型的错误可能很难隔离，因为页面会以透明方式对用户进行更新，因此可能不会立即出现这种情况。

通过检查 ASP.NET AJAX 窗体发布截获模型的内部工作原理，我们能够确定它是否利用了 ASP.NET 已提供的框架。 在此过程中，它会保持与使用相同框架设计的控件的最大兼容性，并且干扰在为该页编写的任何附加 JavaScript 上最低。

## <a name="bio"></a>Bio

抢 Paveza 是 Terralever （[www.terralever.com](http://www.terralever.com)）的高级 .net 应用程序开发人员，TEMPE，AZ 中领先的交互式营销公司。 他可以[robpaveza@gmail.com](mailto:robpaveza@gmail.com)联系，他的博客位于[http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/)。

Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。 可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客

> [!div class="step-by-step"]
> [上一页](understanding-partial-page-updates-with-asp-net-ajax.md)
> [下一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
