---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
title: 内容页中的控件 ID 命名（VB） |Microsoft Docs
author: rick-anderson
description: 阐释 ContentPlaceHolder 控件如何充当命名容器，从而以编程方式处理控件（通过 FindControl） 。
ms.author: riande
ms.date: 06/10/2008
ms.assetid: dbb024a6-f043-4fc5-ad66-56556711875b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 3cb8dec47040bc65f1a024325c91590729ffbdb7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519236"
---
# <a name="control-id-naming-in-content-pages-vb"></a>内容页中的控件 ID 命名 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_VB.zip)或[下载 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_VB.pdf)

> 阐释 ContentPlaceHolder 控件如何充当命名容器，从而以编程方式处理控件（通过 FindControl）。 查看此问题和解决方法。 还介绍了如何以编程方式访问生成的 ClientID 值。

## <a name="introduction"></a>简介

所有 ASP.NET 服务器控件都包含一个 `ID` 属性，该属性用于唯一标识控件，并且是在代码隐藏类中以编程方式访问控件的方法。 同样，HTML 文档中的元素可能包含唯一标识该元素的 `id` 属性;这些 `id` 值通常在客户端脚本中使用，以编程方式引用特定的 HTML 元素。 为此，可以假设当 ASP.NET 服务器控件呈现为 HTML 时，其 `ID` 值将用作呈现的 HTML 元素的 `id` 值。 这并不一定是因为在某些情况下，只有单个 `ID` 值的单个控件在呈现的标记中可能出现多次。 假设有一个 GridView 控件，该控件包含具有 `ID` 值为 `ProductName`的标签 Web 控件的 TemplateField。 当 GridView 在运行时绑定到其数据源时，将为每个 GridView 行重复一次此标签。 每个呈现的标签都需要唯一的 `id` 值。

为了应对这种情况，ASP.NET 允许将某些控件表示为命名容器。 命名容器用作新的 `ID` 命名空间。 命名容器中显示的任何服务器控件都具有以命名容器控件 `ID` 为前缀 `id` 值。 例如，`GridView` 和 `GridViewRow` 类都是命名容器。 因此，在 GridView TemplateField 中定义的标签控件具有 `ID` `ProductName` 会获得一个呈现 `id` 值 `GridViewID_GridViewRowID_ProductName`。 因为*GridViewRowID*对于每个 GridView 行都是唯一的，所以生成的 `id` 值是唯一的。

> [!NOTE]
> [`INamingContainer` 接口](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx)用于指示特定的 ASP.NET 服务器控件应作为命名容器。 `INamingContainer` 接口不会拼写服务器控件必须实现的任何方法;相反，它用作标记。 在生成呈现的标记时，如果控件实现了此接口，则 ASP.NET 引擎会自动为其 `ID` 值加上其后代 "呈现 `id` 属性值。 步骤2中更详细地讨论了此过程。

命名容器不仅会更改呈现的 `id` 属性值，还会影响从 ASP.NET 页的代码隐藏类以编程方式引用控件的方式。 `FindControl("controlID")` 方法通常用于以编程方式引用 Web 控件。 但 `FindControl` 不会穿透命名容器。 因此，不能直接使用 `Page.FindControl` 方法来引用 GridView 或其他命名容器中的控件。

您可能有猜出，母版页和 Contentplaceholder 都是作为命名容器实现的。 在本教程中，我们将探讨母版页如何影响 HTML 元素 `id` 值和使用 `FindControl`以编程方式在内容页中引用 Web 控件的方式。

## <a name="step-1-adding-a-new-aspnet-page"></a>步骤1：添加新的 ASP.NET 页面

为了演示本教程中讨论的概念，我们将新的 ASP.NET 页面添加到我们的网站中。 在根文件夹中创建名为 `IDIssues.aspx` 的新内容页，将其绑定到 `Site.master` 的母版页。

![将内容页 IDIssues 添加到根文件夹](control-id-naming-in-content-pages-vb/_static/image1.png)

**图 01**：将 "内容" 页 `IDIssues.aspx` 添加到根文件夹

Visual Studio 会自动为母版页的四个 Contentplaceholder 创建一个内容控件。 如[*多 contentplaceholder 和默认内容*](multiple-contentplaceholders-and-default-content-vb.md)教程中所述，如果内容控件不存在，则改为发出母版页的默认 ContentPlaceHolder 内容。 由于 `QuickLoginUI` 和 `LeftColumnContent` Contentplaceholder 包含此页的适当默认标记，请继续从 `IDIssues.aspx`中删除其相应的内容控件。 此时，内容页的声明性标记应如下所示：

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample1.aspx)]

在母版页教程的 "[*指定标题、Meta 标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)" 中，我们创建了一个自定义的基本页类（`BasePage`），如果未显式设置该页面的标题，则会自动对其进行配置。 为了使 `IDIssues.aspx` 页使用此功能，页的代码隐藏类必须从 `BasePage` 类（而不是 `System.Web.UI.Page`）派生。 修改代码隐藏类的定义，使其类似于以下内容：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample2.vb)]

最后，更新 `Web.sitemap` 文件以包含此新课程的条目。 添加一个 `<siteMapNode>` 元素，并将其 `title` 和 `url` 属性分别设置为 "控制 ID 命名问题" 和 `~/IDIssues.aspx`。 完成此添加后，`Web.sitemap` 文件的标记应如下所示：

[!code-xml[Main](control-id-naming-in-content-pages-vb/samples/sample3.xml)]

如图2所示，`Web.sitemap` 中的新网站地图条目会立即反映在左列的 "课程" 部分中。

![课程部分现在包含指向 &quot;控件 ID 命名问题的链接&quot;](control-id-naming-in-content-pages-vb/_static/image2.png)

**图 02**：本课部分现在包含指向 "控件 ID 命名问题" 的链接

## <a name="step-2-examining-the-renderedidchanges"></a>步骤2：检查呈现的`ID`更改

为了更好地了解 ASP.NET 引擎对呈现的 `id` 服务器控件的值所做的修改，请将一些 Web 控件添加到 `IDIssues.aspx` 页，然后查看发送到浏览器的呈现的标记。 具体而言，键入文本 "请输入年龄："，后跟 TextBox Web 控件。 在页面上进一步向下添加按钮 Web 控件和标签 Web 控件。 将文本框的 `ID` 和 `Columns` 属性分别设置为 `Age` 和3。 设置该按钮的 `Text`，并 `ID` 属性设置为 "Submit" 并 `SubmitButton`。 清除标签的 `Text` 属性，并将其 `ID` 设置为 "`Results`"。

此时，内容控件的声明性标记应如下所示：

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample4.aspx)]

图3显示了通过 Visual Studio 的设计器查看的页面。

[![页面包含三个 Web 控件：文本框、按钮和标签](control-id-naming-in-content-pages-vb/_static/image4.png)](control-id-naming-in-content-pages-vb/_static/image3.png)

**图 03**：页面包含三个 Web 控件：文本框、按钮和标签（[单击以查看完全大小的图像](control-id-naming-in-content-pages-vb/_static/image5.png)）

通过浏览器访问页面，然后查看 HTML 源。 正如以下标记所示，文本框、按钮和标签 Web 控件的 HTML 元素 `id` 值是 Web 控件的 `ID` 值与页面中命名容器的 `ID` 值的组合。

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample5.html)]

如本教程前面所述，母版页及其 Contentplaceholder 作为命名容器。 因此，这两个控件都提供其嵌套控件的呈现 `ID` 值。 采用 TextBox 的 `id` 属性，例如： `ctl00_MainContent_Age`。 回忆一下 TextBox 控件的 `ID` 值是 `Age`的。 此值以其 ContentPlaceHolder 控件的 `ID` 值为前缀，`MainContent`。 此外，此值以母版页的 `ID` 值为前缀，`ctl00`。 净效果是由母版页、ContentPlaceHolder 控件和文本框本身的 `ID` 值组成 `id` 属性值。

图4说明了此行为。 若要确定 `Age` 文本框的呈现的 `id`，请从 TextBox 控件的 `ID` 值开始，`Age`。 接下来，按照控件层次结构向上操作。 在每个命名容器（具有粉颜色的节点）上，使用命名容器的 `id`作为当前呈现的 `id` 的前缀。

![呈现的 id 属性基于命名容器的 ID 值](control-id-naming-in-content-pages-vb/_static/image6.png)

**图 04**：呈现的 `id` 属性基于命名容器的 `ID` 值

> [!NOTE]
> 如前文所述，呈现 `id` 属性的 `ctl00` 部分构成了母版页的 `ID` 值，但你可能想知道此 `ID` 值是如何产生的。 我们未在主页面或内容页中的任何位置指定它。 在 ASP.NET 页中，大多数服务器控件都是通过页的声明性标记显式添加的。 已在 `Site.master`的标记中显式指定 `MainContent` ContentPlaceHolder 控件;`Age` TextBox `IDIssues.aspx`的标记定义。 可以通过属性窗口或声明性语法指定这些类型的控件的 `ID` 值。 其他控件（如母版页本身）未在声明性标记中定义。 因此，必须为我们自动生成其 `ID` 值。 ASP.NET 引擎在运行时为尚未显式设置 Id 的控件设置 `ID` 值。 它使用命名模式 `ctlXX`，其中*XX*是按顺序递增的整数值。

由于母版页本身用作命名容器，因此在母版页中定义的 Web 控件也会改变 `id` 属性值。 例如，在 "[*使用母版页创建站点范围布局*](creating-a-site-wide-layout-using-master-pages-vb.md)" 教程中添加到母版页的 `DisplayDate` 标签包含以下呈现的标记：

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample6.html)]

请注意，`id` 属性包括母版页的 `ID` 值（`ctl00`）和标签 Web 控件的 `ID` 值（`DateDisplay`）。

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>步骤3：通过`FindControl` 以编程方式引用 Web 控件

每个 ASP.NET 服务器控件都包含一个 `FindControl("controlID")` 方法，该方法在控件的后代中搜索名为*controlID*的控件。 如果找到此类控件，则返回它;如果未找到匹配的控件，`FindControl` 将返回 `Nothing`。

`FindControl` 在需要访问控件但没有对其进行直接引用的情况下很有用。 例如，在使用诸如 GridView 这样的数据 Web 控件时，GridView 字段内的控件在声明性语法中定义一次，但在运行时，将为每个 GridView 行创建一个控件的实例。 因此，在运行时生成的控件存在，但不能通过代码隐藏类提供直接引用。 因此，需要使用 `FindControl` 以编程方式处理 GridView 字段中的特定控件。 （有关使用 `FindControl` 访问数据 Web 控件的模板中的控件的详细信息，请参阅[基于数据的自定义格式设置](../../data-access/custom-formatting/custom-formatting-based-upon-data-vb.md)。）将 Web 控件动态添加到 Web 窗体时，会出现这种情况，这是在[创建动态数据条目用户界面](https://msdn.microsoft.com/library/aa479330.aspx)中讨论的主题。

为了说明如何使用 `FindControl` 方法在内容页中搜索控件，请为 `SubmitButton`的 `Click` 事件创建事件处理程序。 在事件处理程序中，添加以下代码，该代码以编程方式引用 `Age` TextBox 并使用 `FindControl` 方法 `Results` 标签，然后基于用户输入在 `Results` 中显示消息。

> [!NOTE]
> 当然，在此示例中，我们不需要使用 `FindControl` 引用 "标签" 和 "TextBox" 控件。 我们可以通过其 `ID` 属性值直接引用它们。 我使用这里 `FindControl` 来说明从内容页中 `FindControl` 时所发生的情况。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample7.vb)]

尽管用于调用 `FindControl` 方法的语法在 `SubmitButton_Click`的前两行中略有不同，但它们在语义上是等效的。 回忆一下，所有 ASP.NET 服务器控件都包含一个 `FindControl` 方法。 这包括 `Page` 类，所有 ASP.NET 代码隐藏类都必须从该类派生。 因此，调用 `FindControl("controlID")` 等效于调用 `Page.FindControl("controlID")`，假设你未在代码隐藏类或自定义基类中重写 `FindControl` 方法。

输入此代码后，请通过浏览器访问 `IDIssues.aspx` 页面，输入你的年龄，并单击 "提交" 按钮。 单击 "提交" 按钮时，会引发 `NullReferenceException` （请参阅图5）。

[![引发 NullReferenceException](control-id-naming-in-content-pages-vb/_static/image8.png)](control-id-naming-in-content-pages-vb/_static/image7.png)

**图 05**：引发 `NullReferenceException` （[单击查看完全大小的图像](control-id-naming-in-content-pages-vb/_static/image9.png)）

如果在 `SubmitButton_Click` 事件处理程序中设置断点，则会看到两个调用都 `FindControl` 返回 `Nothing`。 尝试访问 `Age` 文本框的 `Text` 属性时，将引发 `NullReferenceException`。

问题在于 `Control.FindControl` 仅搜索*控件*在相同命名容器中的后代。 由于母版页构成新的命名容器，因此对 `Page.FindControl("controlID")` 的调用永远不会将母版页对象 `ctl00`permeates。 （请返回到图4以查看控件层次结构，该层次结构显示 `Page` 对象作为母版页对象的父级 `ctl00`。）因此，找不到 "`Results` 标签" 和 "`Age`" 文本框，`ResultsLabel` 和 `AgeTextBox` 分配的值为 `Nothing`。

此挑战有两种解决方法：我们可以向下钻取一个命名容器，一次向适当的控制;也可以创建 permeates 命名容器的自己的 `FindControl` 方法。 我们来看一下其中的每个选项。

### <a name="drilling-into-the-appropriate-naming-container"></a>深入了解适当的命名容器

若要使用 `FindControl` 引用 "`Results` 标签" 或 "`Age`" 文本框，需要从同一命名容器中的祖先控件调用 `FindControl`。 如图4所示，`MainContent` ContentPlaceHolder 控件是同一命名容器中 `Results` 或 `Age` 的唯一上级。 换言之，从 `MainContent` 控件调用 `FindControl` 方法（如下面的代码段所示）正确返回对 `Results` 或 `Age` 控件的引用。

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample8.vb)]

但是，我们无法使用上述语法通过内容页的代码隐藏类处理 `MainContent` ContentPlaceHolder，因为 ContentPlaceHolder 是在母版页中定义的。 相反，我们必须使用 `FindControl` 获取对 `MainContent`的引用。 将 `SubmitButton_Click` 事件处理程序中的代码替换为以下修改：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample9.vb)]

如果通过浏览器访问此页，请输入你的年龄，然后单击 "提交" 按钮，将会引发 `NullReferenceException`。 如果在 `SubmitButton_Click` 事件处理程序中设置了断点，则在尝试调用 `MainContent` 对象的 `FindControl` 方法时，会出现此异常。 `MainContent` 对象等于 `Nothing`，因为 `FindControl` 方法无法找到名为 "MainContent" 的对象。 基本原因与 "`Results` 标签" 和 "`Age`" 文本框控件相同： `FindControl` 从控件层次结构的顶部开始搜索，但不渗透命名容器，但 `MainContent` ContentPlaceHolder 在母版页中，这是一个命名容器。

在可以使用 `FindControl` 获取对 `MainContent`的引用之前，首先需要引用母版页控件。 引用母版页后，我们可以通过 `FindControl` 并从那里获取对该 `MainContent` ContentPlaceHolder 的引用，`Results` 标签和 `Age` 文本框的引用（同样，通过使用 `FindControl`）。 但如何获取对母版页的引用？ 通过检查呈现的标记中的 `id` 属性，可明显地 `ctl00`母版页的 `ID` 值。 因此，我们可以使用 `Page.FindControl("ctl00")` 获取对母版页的引用，然后使用该对象获取对 `MainContent`等的引用。 以下代码片段演示了此逻辑：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample10.vb)]

尽管此代码当然会起作用，但它假定母版页的自动生成 `ID` 将始终 `ctl00`。 最好是对自动生成的值作出假设。

幸运的是，可以通过 `Page` 类的 `Master` 属性访问母版页的引用。 因此，可以改为使用 `Page.Master.FindControl("MainContent")`，而不必使用 `FindControl("ctl00")` 获取母版页的引用以访问 `MainContent` ContentPlaceHolder。 用以下代码更新 `SubmitButton_Click` 事件处理程序：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample11.vb)]

这次，通过浏览器访问页面，输入年龄，然后单击 "提交" 按钮时，会按预期方式在 `Results` 标签中显示邮件。

[在标签中显示用户的年龄 ![](control-id-naming-in-content-pages-vb/_static/image11.png)](control-id-naming-in-content-pages-vb/_static/image10.png)

**图 06**：用户的年龄显示在标签中（[单击查看完全大小的图像](control-id-naming-in-content-pages-vb/_static/image12.png)）

### <a name="recursively-searching-through-naming-containers"></a>通过命名容器递归搜索

前面的代码示例从母版页引用 `MainContent` ContentPlaceHolder 控件，然后从 `MainContent`中 `Results` 标签和 `Age` TextBox 控件，这是因为 `Control.FindControl` 方法只搜索*控件*的命名容器中的控件。 在大多数情况下，使 `FindControl` 停留在命名容器内非常有用，因为两个不同命名容器中的两个控件可能具有相同的 `ID` 值。 请考虑在其一个 Templatefield 中定义名为 `ProductName` 的标签 Web 控件的 GridView 的情况。 当数据在运行时绑定到 GridView 时，将为每个 GridView 行创建一个 `ProductName` 标签。 如果 `FindControl` 搜索所有命名容器，并且我们调用了 `Page.FindControl("ProductName")`，则 `FindControl` 会返回哪些标签实例？ 第一个 GridView 行中的 `ProductName` 标签？ 最后一行中的值是多少？

因此，在大多数情况下，只需 `Control.FindControl` 搜索*控件*的命名容器。 但还有其他一些案例，例如一个面向我们的情况，在这种情况下，我们在所有命名容器中都有唯一的 `ID`，并希望避免精心引用控件层次结构中的每个命名容器以访问控件。 具有递归搜索所有命名容器的 `FindControl` 变体也是有意义的。 遗憾的是，.NET Framework 不包含这种方法。

好消息是，我们可以创建自己的 `FindControl` 方法，以递归方式搜索所有命名容器。 事实上，使用*扩展方法*时，我们可以将 `FindControlRecursive` 方法追加到 `Control` 类，以伴随其现有 `FindControl` 方法。

> [!NOTE]
> 扩展方法是C# 3.0 和 Visual Basic 9 的新增功能，这是 .NET Framework 版本3.5 和 Visual Studio 2008 附带的语言。 简而言之，扩展方法允许开发人员通过特殊语法为现有类类型创建新方法。 有关这项有用功能的详细信息，请参阅我[的文章通过扩展方法扩展基类型功能](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)。

若要创建扩展方法，请将新文件添加到名为 `PageExtensionMethods.vb`的 `App_Code` 文件夹。 添加一个名为 `FindControlRecursive` 的扩展方法，该方法采用名为 `controlID`的 `String` 参数作为输入。 要使扩展方法正常工作，必须将类标记为 `Module`，并以 `<Extension()>` 特性为前缀。 此外，所有扩展方法都必须接受扩展方法应用于的类型的对象作为其第一个参数。

将以下代码添加到 `PageExtensionMethods.vb` 文件中，以定义此 `Module` 和 `FindControlRecursive` 扩展方法：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample12.vb)]

将此代码放置后，返回到 `IDIssues.aspx` 页的代码隐藏类，并注释掉当前的 `FindControl` 方法调用。 将它们替换为对 `Page.FindControlRecursive("controlID")`的调用。 扩展方法的含义是直接显示在 IntelliSense 下拉列表中。 如图7所示，在键入 `Page` 然后点击时间段时，`FindControlRecursive` 方法将与其他 `Control` 类方法一起包含在 IntelliSense 下拉下。

[IntelliSense 下拉方式包含 ![扩展方法](control-id-naming-in-content-pages-vb/_static/image14.png)](control-id-naming-in-content-pages-vb/_static/image13.png)

**图 07**：扩展方法包含在 IntelliSense 下拉项中（[单击以查看完全大小的图像](control-id-naming-in-content-pages-vb/_static/image15.png)）

在 `SubmitButton_Click` 事件处理程序中输入以下代码，然后通过访问该页面，输入你的年龄，并单击 "提交" 按钮来对其进行测试。 如图6所示，生成的输出将为消息 "您的年龄段已过时！"

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample13.vb)]

> [!NOTE]
> 因为扩展方法是C# 3.0 和 Visual Basic 9 的新手，所以如果使用的是 Visual Studio 2005，则不能使用扩展方法。 相反，您需要在 helper 类中实现 `FindControlRecursive` 方法。 在他的博客文章中， [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx)有此类示例， [ASP.NET 微波激射页和 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)。

## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>步骤4：在客户端脚本中使用正确的`id`属性值

如本教程中所述，通常在客户端脚本中使用 Web 控件的呈现 `id` 属性以编程方式引用特定的 HTML 元素。 例如，以下 JavaScript 通过其 `id` 引用 HTML 元素，然后在模式消息框中显示其值：

[!code-csharp[Main](control-id-naming-in-content-pages-vb/samples/sample14.cs)]

请记住，在不包含命名容器的 ASP.NET 页面中，呈现的 HTML 元素的 `id` 属性与 Web 控件的 `ID` 属性值相同。 因此，很容易将属性值中的硬编码 `id` 为 JavaScript 代码。 也就是说，如果知道要通过客户端脚本访问 `Age` TextBox Web 控件，请通过调用 `document.getElementById("Age")`来执行此操作。

此方法的问题是，在使用母版页（或其他命名容器控件）时，呈现的 HTML `id` 与 Web 控件的 `ID` 属性不是同义词。 您的第一步可能是通过浏览器访问该页，并查看源以确定实际的 `id` 属性。 知道呈现的 `id` 值后，可以将其粘贴到对 `getElementById` 的调用中，以便访问通过客户端脚本所需的 HTML 元素。 此方法小于理想方法，因为对页的控件层次结构的某些更改或对命名控件的 `ID` 属性的更改将更改生成的 `id` 属性，从而破坏 JavaScript 代码。

好消息是，呈现的 `id` 属性值可通过 Web 控件的[`ClientID` 属性](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)在服务器端代码中访问。 应使用此属性来确定客户端脚本中使用的 `id` 属性值。 例如，若要向页面添加 JavaScript 函数（在调用时），则会在模式消息框中显示 "`Age`" 文本框的值，并将以下代码添加到 `Page_Load` 事件处理程序：

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample15.vb)]

上面的代码将 `Age` TextBox 的 `ClientID` 属性的值注入到 JavaScript 调用 `getElementById`。 如果通过浏览器访问此页并查看 HTML 源，会看到以下 JavaScript 代码：

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample16.html)]

请注意，正确的 `id` 属性值 `ctl00_MainContent_Age`会出现在对 `getElementById`的调用内。 由于此值是在运行时计算的，因此它的工作方式与对页面控件层次结构的后续更改无关。

> [!NOTE]
> 此 JavaScript 示例只介绍如何添加正确引用服务器控件呈现的 HTML 元素的 JavaScript 函数。 若要使用此函数，需要创作额外的 JavaScript，以便在加载文档时或在特定的用户操作发生时调用该函数。 有关这些主题和相关主题的详细信息，请阅读使用[客户端脚本](https://msdn.microsoft.com/library/aa479302.aspx)。

## <a name="summary"></a>摘要

某些 ASP.NET 服务器控件充当命名容器，它们会影响其子代控件的呈现 `id` 属性值，以及 `FindControl` 方法 canvassed 的控件的作用域。 对于母版页，母版页本身及其 ContentPlaceHolder 控件都是命名容器。 因此，在使用 `FindControl`以编程方式引用内容页中的控件时，我们需要更多的工作。 在本教程中，我们介绍了两种方法：钻取到 ContentPlaceHolder 控件并调用其 `FindControl` 方法;并滚动我们自己的 `FindControl` 实现以递归方式搜索所有命名容器。

除了引用 Web 控件的服务器端问题之外，还存在一些客户端问题。 在缺少命名容器的情况下，Web 控件的 `ID` 属性值和呈现 `id` 属性值都是相同的。 但在添加命名容器的情况下，呈现的 `id` 属性包括 Web 控件的 `ID` 值和控件层次结构的体系中的命名容器。 如果你使用 Web 控件的 `ClientID` 属性来确定客户端脚本中呈现的 `id` 属性值，则这些命名问题都是一个非问题。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 母版页和 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [创建动态数据条目用户界面](https://msdn.microsoft.com/library/aa479330.aspx)
- [用扩展方法扩展基类型功能](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [如何：引用 ASP.NET 母版页内容](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [地主页面：提示、技巧和陷阱](http://www.odetocode.com/articles/450.aspx)
- [使用客户端脚本](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Zack 的 Suchi Barnerjee。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](urls-in-master-pages-vb.md)
> [下一页](interacting-with-the-master-page-from-the-content-page-vb.md)
