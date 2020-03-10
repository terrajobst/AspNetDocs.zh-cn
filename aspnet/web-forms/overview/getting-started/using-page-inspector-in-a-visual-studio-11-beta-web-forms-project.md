---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: 在 ASP.NET Web 窗体中使用 Visual Studio 2012 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 Page Inspector 是使用集成浏览器的 web 开发工具。 在集成浏览器中选择任意元素，并 Page Inspector 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464942"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>在 ASP.NET Web 窗体中使用适用于 Visual Studio 2012 的 Page Inspector

通过 Tim Ammann

> Visual Studio 2012 Page Inspector 是使用集成浏览器的 web 开发工具。 在集成浏览器中选择任意元素，Page Inspector 会立即突出显示该元素的源和 CSS。 可以在应用程序中浏览任意页面，快速找到所呈现标记的源，并直接在 Visual Studio 环境中使用浏览器工具。
> 
> 本教程演示如何启用检查模式，然后在你的 web 项目中快速查找和编辑 CSS 规则和文本。 本教程使用 Web 窗体应用程序项目，但也可以将 Page Inspector 用于网站项目和[MVC](https://go.microsoft.com/?linkid=9802002)应用程序。
> 
> 本教程包含以下部分：
> 
> [先决条件](#_1_prerequisites)
> 
> [创建 Web 应用程序](#_2_creating_a)
> 
> [使用 Page Inspector 查看应用程序](#_3_using_page)
> 
> [启用检查模式](#_4_inspection_mode)
> 
> [使用 Page Inspector 对标记进行更改](#_5_using_page)
> 
> [检查模式和 HTML 窗口](#_6_inspection_mode)
> 
> [在 "样式" 窗口中预览 CSS 更改](#_7_previewing_css)
> 
> [CSS 自动同步](#css_auto_sync)
> 
> [使用 CSS 颜色选取器](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>系统必备

- [用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。

> [!NOTE]
> 若要获取最新版本的 Page Inspector，请使用[Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)安装用于 .net 2.0 的 Azure SDK。

Page Inspector 与 Microsoft Web 开发人员工具捆绑在一起。 最新版本为1.3。 若要检查你的版本，请运行 Visual Studio，然后从 "**帮助**" 菜单中选择 "**关于 Microsoft Visual Studio** 。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>创建 Web 应用程序

首先，将创建一个 web 应用程序，该应用程序将与 Page Inspector 使用。 在 Visual Studio 中，选择 "**文件**" &gt; "**新建项目**"。 在左侧，展开 "**视觉C#对象**"，选择 " **web**"，然后选择 " **ASP.NET web 窗体应用程序**"。

![新的 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

单击“确定”。

应用程序将在 "**源**" 视图中打开。

![源视图中的新 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

现在，你已经有了要使用的应用程序，可以使用 Page Inspector 来检查和修改它。

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>使用 Page Inspector 查看应用程序

接下来，你将查看 Page Inspector 的应用程序。 在**解决方案资源管理器**中，右键单击项目，然后选择 "**在 Page Inspector 中查看**"。

![在页面检查器中查看](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

默认情况下，当 Page Inspector 首次启动时，它将作为 Visual Studio 环境左侧的窄窗口停靠。 将其停靠在左侧，并将其设置为适合你的宽度，或将其停靠在顶部、底部或右侧的一个工具区域中：

![Page Inspector 停靠位置](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

如果取消停靠 "Page Inspector" 窗口，则可以将其放置在 Visual Studio 之外，甚至是在另一个监视器上（如果有）。 但是，若要在取消停靠 Page Inspector 窗口时，在 Page Inspector 和 Visual Studio 之间的 ALT + TAB，请参阅 "**工具**" &gt;**选项**"&gt;**环境**&gt;**选项卡和窗口**"，然后在 **"选项卡**" 下，清除 "**浮动工具窗口始终停留在主窗口顶部**：

![清除 "浮动工具窗口" 复选框，并在 Visual Studio 和取消停靠的 Page Inspector 窗口之间的 ALT + TAB](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

"Page Inspector" 窗口的顶部窗格显示浏览器窗口中的当前页。 底部窗格显示左侧 HTML 标记中的页面，并在右侧显示可用于检查页面的不同方面的选项卡。 底部窗格类似于 Internet Explorer 中的[F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)。 （但是，与开发人员工具不同，你可以在 Visual Studio 中使用 Page Inspector。）

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

在本教程中，你将使用 "Page Inspector 浏览器" 窗格和 " **HTML** " 和 "**样式**" 选项卡，以帮助你快速导航并更改应用程序。

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>启用检查模式

接下来，您将了解 Page Inspector 的检查模式的工作方式。 在 "Page Inspector" 窗口中，单击 "**检查**" 按钮。

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

若要查看操作中的检查模式，请将鼠标移动到 Page Inspector 浏览器窗口内页面的不同部分。 正如你所做的那样，鼠标指针将更改为大加号，并突出显示下面的元素：

![悬停在 div 上。内容包装](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

移动鼠标指针时，请注意

- **源**视图中的内容将发生变化，以显示与页面上所选元素对应的标记。 将突出显示相关标记。 如果源位于另一个文件中，则会在 "源" 视图中打开该文件，并突出显示相关标记。

- Page Inspector 中的 " **HTML** " 选项卡中显示的标记也将更改为与页面上所选的元素相对应。 在 " **HTML** " 选项卡中，概述了相关标记。

- "**样式**" 选项卡显示与当前所选内容相关的 CSS 规则。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>使用 Page Inspector 对标记进行更改

现在，你将了解如何使用 Page Inspector 来查找和更改位置可能不会立即显而易见的标记或文本。

将 Page Inspector 放检查模式，然后滚动到主页的底部。

一旦输入页脚区，Page Inspector 将在 "源" 视图中的 "其他" 选项卡的右侧临时选项卡上打开 "**源**" 视图中的 "*站点*" 布局文件，并突出显示所选母版页的部分。 这会显示 Page Inspector 如何查找并显示页面上的内容，这些内容可能来自于最初打开的文件之外的其他文件。

![页脚突出显示检查模式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

在 "Page Inspector 浏览器" 窗口中，将鼠标指针移动到带有版权声明<a id="a"></a>的行上。

在*站点母版页*中，将突出显示相应的行。

![突出显示了页脚版权行](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

将一些文本添加到*站点 .master*文件中行的末尾。

&amp;copy &lt;p&gt;&lt;%： DateTime . Year%&gt;-My ASP.NET Application Rocks！&lt;/p&gt;

现在，按 Ctrl + Alt + Enter，或单击 "更新" 栏以在 "Page Inspector 浏览器" 窗口中查看结果。

![我的 ASP.NET 应用程序 Rocks！](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

您可能认为页脚位于*default.aspx*页面上，但它已在主布局页面中，并 Page Inspector 找到它。

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>检查模式和 HTML 窗口

接下来，您将快速了解 HTML 窗口以及它如何为您映射元素。

将 Page Inspector 放置在检查模式中。

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

单击 "此处显示徽标" 页面的顶部部分。 您将更详细地检查特定元素，因此，在浏览器窗口中显示的内容将不再随着鼠标指针的移动而改变。

现在，将鼠标指针移动到**HTML**窗口。 移动鼠标指针时，Page Inspector 在**HTML**窗口中勾勒元素，并在浏览器窗口中突出显示相应的元素。

![HTML 窗口](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

与之前一样，Page Inspector 会在临时选项卡中打开*网站 .master*文件。单击 "主节点" 选项卡，并在 &lt;标头&gt; "部分突出显示相应的标记：

![突出显示标记](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>在 "样式" 窗口中预览 CSS 更改

接下来，您将了解如何使用 Page Inspector**样式**"窗口来预览 CSS 的更改。

单击 "**检查**" 按钮以将 Page Inspector 放置在检查模式中。

在 "Page Inspector 浏览器" 窗口中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装**器" 标签。

![悬停在元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

在 div. 内容包装部分中单击一次，然后将鼠标指针移动到 "**样式**" 窗口。 在 "属性-包装类选择器" 下，清除并选中 "背景色" 属性的复选框。

![清除背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

请注意如何在 Page Inspector 浏览器窗口中立即更改预览。

再次选中此复选框，然后双击属性值并将其更改为 `red`。 更改将立即显示：

![红色背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

在将更改提交到样式表本身之前，"**样式**" 窗口可让你轻松地测试和预览 CSS 更改。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自动同步

> [!NOTE]
> 此功能需要 Page Inspector 1.3 版。

使用 CSS 自动同步功能，可以直接编辑 CSS 文件，并立即在 Page Inspector 浏览器中查看更改。

单击 "**检查**" 以将 Page Inspector 置于检查模式。

在 "Page Inspector 浏览器" 中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装**器" 标签。 单击 "一次" 以选择此元素。

"**样式**" 窗口显示此元素的所有 CSS 规则。 向下滚动以查找 ""。 单击 "."。 Page Inspector 打开定义此样式（web.config）的 CSS 文件，并突出显示相应的 CSS 样式。

![CSS 文件](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

现在，将 `background-color` 的值更改为 "red"。 更改会立即显示在 Page Inspector 浏览器中。

![Page Inspector 浏览器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>使用 CSS 颜色选取器

接下来，您将学习如何使用 Page Inspector 在默认应用程序中快速查找和更改已突出显示文本的 CSS。 在此示例中，你决定不喜欢蓝色突出显示，并且想要将其更改为另一种颜色。

单击 "**检查**" 按钮。

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

在 "Page Inspector 浏览器" 窗口中，将鼠标指针移到突出显示的 "视频、教程和示例" 文本上，以便显示 CSS "标记" 标签。

![悬停在 mark 元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

单击该文本将其选中。 对应的 CSS 标记选择器显示在 "**样式**" 窗口的底部。

![在 "样式" 窗口中标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

单击标记选择器。 这将打开 web 应用程序的*web.config 文件。* 单击 "站点" "css" 选项卡，将突出显示选择器对应的 CSS：

![在样式表中标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

选择并删除具有背景色属性的行。

现在，你将使用新的 Visual Studio 2012 CSS 颜色选取器为 "**标记**背景-颜色" 属性选择新颜色。

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>使用 Visual Studio 2012 CSS 颜色选取器

Visual Studio 2012 中的 CSS 编辑器提供了一个颜色选取器，使您可以轻松地选择和插入颜色。 它有一个简单的颜色栏和一个提供更精细控制的 "弹出项" 选取器。

颜色选取器包含一种标准颜色调色板，支持标准颜色名称、哈希代码、RGB、RGBA、HSL 和 HSLA 颜色，并维护最近在文档中使用的颜色的列表。

在背景色属性所在的行上，键入 "bc"，然后按向下键一次。

当你在连字符分隔属性（如 "背景色"）中键入每个单词的第一个字符时，IntelliSense 将筛选该列表以仅显示匹配的属性：

![Intellisense 筛选值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

现在，键入一个冒号。 执行此操作时，将插入完整的背景色属性名称。 键入 **#** 或**rgb （** ，并显示颜色选取器栏：

![CSS 颜色选取器栏](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

若要查看颜色选取器栏的工作方式，请使用鼠标指针单击其颜色，或按向下箭头键，然后使用向左箭头和向右箭头键来遍历颜色。 访问颜色时，会预览背景色属性的相应值：

![已预览背景色属性值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

此时，可以按 Enter 选择值，然后选择分号（;)完成 CSS 条目。 现在，请继续查看下一部分，以便可以看到颜色选取器弹出窗口的工作方式。

#### <a name="using-the-color-picker-pop-down"></a>使用 "颜色选取器" 弹出窗口

如果颜色条没有您所需的确切颜色，可以使用 "颜色选取器" 弹出窗口。

若要打开它，请单击颜色栏右端的双 v 形 v 形，或在键盘上按向下键一次或两次。

![CSS 颜色选取器弹出窗口](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

单击右侧垂直条中的颜色。 这会在主窗口中显示该颜色的渐变。 按 Enter 键直接从竖线中选择一种颜色，或单击主窗口中的任何点以选择更高的精度。

如果您要使用的计算机屏幕上有一种颜色（它不必在 Visual Studio 用户界面内），则可以使用右下方的吸管工具捕获其值。

还可以通过移动颜色选取器底部的滑块来更改颜色的不透明度。 这样做会将颜色值更改为 RGBA 值，因为 RGBA 格式可以表示不透明度。

选择一种颜色后，按 Enter，然后键入一个分号来完成*站点导航*文件中的背景色项。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Page Inspector 更新栏

Page Inspector 立即检测对*站点 .css*文件（或应用程序中的任何文件）所做的更改，并在更新栏中显示警报。

![更新栏](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

若要保存所有文件并刷新 Page Inspector 浏览器，请按 Ctrl + Alt + Enter，或单击更新栏。 突出显示颜色的更改将显示在浏览器中：

![突出显示颜色已更改](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>请注意，你可以直接从 Visual Studio 环境中刷新 Page Inspector 浏览器。 使用 Page Inspector 而不是外部浏览器，可以在开发 web 应用程序时保持在编辑器中。

## <a name="see-also"></a>另请参阅

[简介 Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) （第9频道视频）

[Page Inspector 错误消息](https://go.microsoft.com/?linkid=9813062)（MSDN）
