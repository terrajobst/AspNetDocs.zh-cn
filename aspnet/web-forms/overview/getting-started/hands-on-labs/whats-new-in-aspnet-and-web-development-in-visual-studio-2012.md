---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 中 ASP.NET 和 Web 开发的新增功能 |Microsoft Docs
author: rick-anderson
description: 新版本的 Visual Studio 引入了许多增强功能，重点是在使用 Web 技术时提高体验和性能 ...。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422096"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>Visual Studio 2012 中 ASP.NET 和 Web 开发的新增功能

由[Web 训练营团队](https://twitter.com/webcamps)使用

> Visual Studio 的新版本引入了大量增强功能，重点是在使用 Web 技术时改进体验和性能。 Visual Studio for CSS、JavaScript 和 HTML 已经完全改进，其中包含了许多最按需代码辅助功能，例如 IntelliSense 和自动缩进。 与性能、绑定和缩减现已集成为内置功能，可轻松减少页面加载时间。
> 
> 利用 Visual Studio，你可以使用最新的网站技术。 你可以使用跨浏览器 CSS3 代码段来确保你的站点正常工作，而不考虑客户端平台，同时利用新的 HTML5 元素和功能。
> 
> 通过此 Visual Studio 版本，编写和分析 JavaScript 代码应该更为容易。 IntelliSense 列表、集成的 XML 文档和导航功能现在可用于 JavaScript 代码。 现在，你可以轻松获得 JavaScript 目录。 此外，还可以检查 ECMAScript5 与脚本的符合性，并在早期阶段检测语法错误。
> 
> 最后，但不是最起码，此 Visual Studio 版本实现内置的绑定和缩减。 将打包并压缩脚本文件和样式表，以使站点的执行速度更快。
> 
> 此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)提供。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在此动手实验中，您将学习如何：

- 使用 CSS 编辑器中的新功能和改进
- 使用 HTML 编辑器中的新功能和改进
- 使用 JavaScript 编辑器中的新功能和改进
- 配置和使用绑定和缩减

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

- 适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) （适用于安装程序脚本-已在 windows 8 和 windows Server 2008 R2 上安装）
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home)或与 HTML5 兼容的浏览器

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包括以下练习：

1. [练习1： CSS 编辑器中的新增功能](#Exercise1)
2. [练习2： HTML 编辑器中的新增功能](#Exercise2)
3. [练习3： JavaScript 编辑器中的新增功能](#Exercise3)
4. [练习4：捆绑和缩减](#Exercise4)

完成本实验的估计时间： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>练习1： CSS 编辑器中的新增功能

Web 开发人员应熟悉与 CSS 编辑相关的很多困难。 CSS 样式的最大问题之一是跨浏览器兼容性。 这种情况通常发生在将样式应用到您的网站后，您会发现，如果在另一个浏览器或设备中打开它，它看起来会有所不同。 因此，您可能会花费相当长的时间来解决这些视觉问题，以了解到，当您最终在一个浏览器中工作时，它会在另一个浏览器中中断。

Visual Studio 现在包含一些功能，可帮助开发人员有效地访问、处理和组织 CSS 样式表。 在此练习中，您将满足有效组织版本的新功能，以及用于跨浏览器兼容性的 CSS3 代码片段。

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>任务 1-新编辑器功能

在此任务中，你将发现 "CSS 编辑器" 的新功能。 此新编辑器通过利用新的智能缩进、改进的代码注释和增强的 IntelliSense 列表，帮助提高工作效率。

1. 启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。
2. 在解决方案资源管理器中，打开位于 "**样式**" 文件夹下的 "**站点**" 文件。 请确保**文本编辑器**工具在工具栏上可见。 为此，请选择 "**查看** | **工具栏**" 菜单选项，并选中 "**文本编辑器**" 选项。 你将注意到，由于这一新版本，还为 CSS 编辑器启用了**注释**按钮（![注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)）和**取消注释**按钮（![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)）。

    ![启用编辑器和 CSS 工具](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "启用编辑器和 CSS 工具")

    *启用编辑器和 CSS 工具*
3. 滚动代码并选择任何 CSS 类定义。 单击 "**注释**" （![注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)） "按钮以注释所选的行。 然后单击 "**取消注释**（![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)）" 按钮以撤消所做的更改。
4. 单击 "**折叠**（![折叠](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)）"，然后**展开**（![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) 展开位于文本左边距上的按钮）。 请注意，现在可以隐藏不使用的样式以使其具有更清晰的视图。

    ![折叠 CSS 类](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "折叠 CSS 类")

    *折叠 CSS 类*
5. 请确保智能缩进功能已启用。 选择 "**工具**" | "**选项**" 菜单选项，然后在屏幕的左窗格中选择 "**文本编辑器**" | **CSS** | **格式**"页。 检查**分层缩进**选项。

    ![启用分层缩进](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "启用分层缩进")

    *启用分层缩进*
6. 找到主类定义（main）并向 div 元素追加样式。 你会注意到，代码自动对齐，帮助用户一目了然地查找父类。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![CSS 中的层次结构对齐](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 中的层次结构对齐")

    *CSS 中的层次结构对齐*
7. 在**主 div**类的末尾，找到位于边界末尾的光标 **： 0px;** ，然后按**enter**显示 IntelliSense 列表。 开始键入**top** ，并注意在键入时如何筛选列表。 此列表将在单词的任何部分显示包含**top**的元素（在 Visual Studio 的先前版本中，该列表由*以术语开头*的项进行筛选）。

    ![CSS 中的 IntelliSense 增强功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 中的 IntelliSense 增强功能")

    *CSS 中的 IntelliSense 增强功能*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>任务 2-颜色选取器

在此任务中，你将发现集成到 Visual Studio IntelliSense 的新 CSS 颜色选取器。

1. 在 "站点导航" 中 **，** 找到标头类定义（. "标头"），并将光标放在**背景色**属性旁，在 &quot;：&quot; 和 &quot;#该代码行上 &quot; 个字符 **。**

    ![定位游标](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "定位游标")

    *定位游标*
2. 删除**冒号**（:)并再次编写它以显示颜色选取器。 请注意，你将看到的第一种颜色是网站的最常见颜色。 如果单击白色颜色，则其 HTML 颜色代码（#fff）将替换样式表中的当前颜色代码。

    ![颜色选取器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "颜色选取器")

    *颜色选取器*
3. 在颜色选取器上按 "**展开**" （![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)） "按钮以显示颜色渐变，然后拖动渐变光标以选择不同的颜色。 之后，单击 "**取色**器" 按钮，然后从屏幕中选择任意颜色。 请注意，在移动光标时，背景色值会动态更改。

    ![颜色选取器渐变](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "颜色选取器渐变")

    *颜色选取器渐变*
4. 在**不透明度**滑块中，将选择器移动到条形图的中心，以减小不透明度。 请注意，背景色值现在会更改为 RGBA 大小。

    ![颜色选取器不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "颜色选取器不透明度")

    *颜色选取器不透明度*

    > [!NOTE]
    > CSS3 中的 RGBA （红色、绿色、蓝色和 Alpha）颜色定义允许您定义单个项的颜色不透明度值。 不同于**不透明度-** 类似的 CSS 特性 **-** RGBA 颜色也与最新浏览器兼容。

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>任务 3-CSS 兼容代码段

在此任务中，您将学习如何使用跨浏览器兼容 CSS3 代码段来实现您网站中的某些功能。

1. 在 " **web.config** " 文件中，找到 "**标头**" "css 类定义" （. "标头"），并将光标置于 **/\*border radius\*/** 占位符添加新代码段。 按**enter**显示 IntelliSense 列表，并键入**radius**以筛选列表。 从列表中选择一个双击**边框**，并按**tab**键以插入代码段。 然后，键入半径大小（以像素为单位），然后按**enter**。 例如，键入 " **15px**"。

    代码段添加的 CSS3 特性将在大多数 HTML5 相容性浏览器（包括 Mozilla 和基于 WebKit 的浏览器）中呈现圆角边框。

    ![使用边框-半径代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "使用边框-半径代码段")

    *使用边框-半径代码段*
2. 在页面样式（. page）中应用相同的**边框**代码段。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. 按 **“F5”** 运行该解决方案。 请注意，每个页面现在都具有圆角边框。

    ![圆角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "圆角")

    *圆角*
4. 关闭浏览器并返回到 Visual Studio。
5. 打开位于 "**样式**" 文件夹下的**自定义 .css**文件，并将光标放在**div 中。**
6. 按 enter 显示 IntelliSense 列表，键入**框-阴影**，并按**tab**键两次，以便在类定义中插入默认的影子代码段。 将阴影值设置为**10px 10px 5px #888**。 然后，键入**border 半径**并插入代码片段。 键入**15px**以设置 radius 大小并按**enter**。

    ![带阴影的圆角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "带阴影的圆角")

    *带阴影的圆角*

    > [!NOTE]
    > 此时，将插入带有相应前缀（moz，webkit，o）的影子属性，以支持 Mozilla 和 Webkit （Chrome，Konkeror）浏览器。
7. 创建新的类**div。 images ul li：将鼠标悬停**在**div**上，将其放在

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. 键入 "**转换**"，并按**tab**键两次以插入转换代码片段。 然后，输入**旋转（-15deg）** ，以在图像悬停时更改旋转角度值。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. 按**F5**运行解决方案并浏览到 CSS3 页面。 请注意，图像具有圆角和框阴影。 将鼠标指针悬停在图像上，并观察它们是否旋转。

    ![转换用于旋转图像的代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "转换用于旋转图像的代码段")

    *转换用于旋转图像的代码段*

    > [!NOTE]
    > 如果使用的是 Internet Explorer 10，并且看不到阴影，请确保将文档模式设置为 IE10 标准。 按**F12**打开 Internet Explorer 开发人员工具，然后单击 "**文档模式**" 更改为 "IE10 标准"。

    ![关于我们](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>练习2： HTML 编辑器中的新增功能

Visual Studio 具有改进的 HTML 编辑器。 此版本中包含的一些增强功能是 HTML 文档、HTML5 代码段、HTML 开始和结束标记匹配以及 HTML 验证中的智能缩进。 在此练习中，你将看到这些更改在网站标记中工作时如何提高你的熟练。

与 CSS 编辑器一样，HTML 编辑器也得到了改进。 其中的大多数改进都是使 Web 开发人员的工作变得更简单的小型。 例如，对于 HTML5 的更多代码片段，智能缩进，在编辑和验证目标为 HTML 文档 DOCTYPE 时匹配开始和结束标记是其中的一些改进。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>任务 1-改进了 DOCTYPE 验证

HTML 编辑器现在可以检查页面的 DOCTYPE，即使该定义可能在母版页中。 根据页面的 DOCTYPE，HTML 编辑器将验证是否有正确的规则集，并将根据 DOCTYPE 元素筛选 IntelliSense 列表。

在此任务中，您将更改页面的 DOCTYPE，以查看 HTML 编辑器行为如何相应地更改。

1. 如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。
2. 打开**网站母版页**。
3. 请注意验证工具栏的目标架构。 HTML 编辑器的行为方式（验证、IntelliSense 等）将正确更改为符合所选 Doctype。

    ![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "在 HTML 源编辑工具栏中使用 Doctype")

    *在 HTML 源编辑工具栏中使用 Doctype*
4. 将目标架构更改为 HTML 4.01。

    ![在 HTML 源编辑工具栏中更改 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "在 HTML 源编辑工具栏中更改 Doctype")

    *在 HTML 源编辑工具栏中更改 Doctype*
5. 将光标置于**body**元素下，开始键入 HTML5 元素的名称（例如，**视频**）。 请注意，该元素在 IntelliSense 列表中不可用。

    ![未列出 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "未列出 HTML5 元素")

    *未列出 HTML5 元素*
6. 撤消对验证工具栏的目标架构所做的更改，从下拉列表中选择 "DOCTYPE： XHTML5"。

    ![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "在 HTML 源编辑工具栏中使用 Doctype")

    *在 HTML 源编辑工具栏中重置 Doctype*
7. 将光标置于**body**元素下，并再次开始键入 HTML5 元素（例如，如**视频**）。 请注意，HTML5 元素现已在 IntelliSense 列表中提供。

    ![列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "列出的 HTML5 元素")

    *列出的 HTML5 元素*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>任务 2-开始/结束标记自动更新

Visual Studio 现在会更新要编辑的元素的 HTML 开始标记或结束标记，使其相互匹配。 这项新功能将在编辑 HTML 标记时提高工作效率。

1. 在 " **default.aspx** " 页上，添加一个带标题的**H3**元素（例如，Visual Studio 2012 Rocks！）。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. 更改**H3**标记并键入**H2**或**H1。**

    请注意，结束标记会自动更新。 你还可以修改结束标记，以查看开始标记是否相应更新。

    ![自动更新结束标记](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "自动更新结束标记")

    *自动更新结束标记*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>任务 3-新的 HTML5 代码片段

Visual Studio 现在包含多个 HTML5 代码段。 在此任务中，您将使用其中一些代码段。

1. 将名为 "**音频**" 的新文件夹添加到 "网站" 文件夹的根目录。 打开 Windows 资源管理器并将任何音频文件复制到**WhatsNewASPNET**解决方案的**音频**文件夹中。
2. 在 " **default.aspx** " 页中，找到 Web11 Rocks！！下的光标。 标头。 键入 "**音频**" 并按 tab 键。

    新的 HTML 编辑器包括 HTML5 内容的代码片段。 请记得使用正确的 DOCTYPE 定义来启用 HTML5 代码段。

    ![插入 HTML5 代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "插入 HTML5 代码段")

    *插入 HTML5 代码段*
3. 更新音频源以指向现有的音频文件。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > 需要将音频文件添加到解决方案中。
4. 按**F5**运行该站点并播放音频。

    ![运行音频控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "运行音频控件")

    *运行音频控件*

    > [!NOTE]
    > 还可以尝试在 Visual Studio 中包含的更多代码段，如视频、图等。
5. 现在，请尝试在页面的某个部分插入控件。 例如，尝试插入一个**GridView**控件，而不是键入 **&lt;网格，** 开始键入 **&lt;GV**。 请注意，IntelliSense 列表显示了**asp： GridView**控件。

    HTML 编辑器中的 IntelliSense 现在提供了标题大小写搜索以及部分匹配（检索包含该字词的所有元素）。

    ![使用 IntelliSense 列表插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "使用 IntelliSense 列表插入 GridView")

    *使用 IntelliSense 列表插入 GridView*

    如果键入 **&lt;网格**，将获取与该字词匹配的所有项，但 Visual Studio 将建议**gridview**控件：

    ![使用 IntelliSense 列表和部分匹配插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "使用 IntelliSense 列表和部分匹配插入 GridView")

    *使用 IntelliSense 列表和部分匹配插入 GridView*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>任务 4-HTML 编辑器智能标记

HTML 编辑器的另一项改进是智能标记功能。 使用智能标记可轻松地按控件执行常见或重复性的开发任务。 此功能在 HTML 设计器中已可用，但在 HTML 编辑器中不可用。

1. 打开 "**网站**"，然后找到 " **asp： Menu** " 元素。 将光标置于开始标记上，注意在元素底部显示的小标志符号，单击它打开 "智能任务" 菜单。 请注意，您可以快速访问与 Menu 控件相关的一些任务。

    ![Menu 控件的智能任务](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Menu 控件的智能任务")

    *Menu 控件的智能任务*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>任务 5-智能缩进

HTML 中的最佳做法之一是缩进嵌套元素，以使代码更具可读性。 在 Visual Studio 2012 中，你会注意到，在编写代码时，编辑器会自动缩进元素。

> [!NOTE]
> 在 Visual Studio 的早期版本中，智能缩进在 XML 编辑器中可用，但在 HTML 编辑器中可用。

1. 请确保 HTML 编辑器上的 "缩进配置" 设置为 "智能缩进"。 为此，请选择 "**工具" |"选项**" 菜单选项，然后选择 "**文本编辑器" |HTML |** 屏幕的左窗格中的 "选项卡" 页。 选择 "智能缩进" 选项。

    ![HTML 编辑器设置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 编辑器设置")

    *HTML 编辑器设置*
2. 在 " **default.aspx** " 页上，删除 "音频" 元素下的所有内容。
3. 将光标置于开始**音频**元素的末尾，然后按**ENTER**。

    请注意，游标的新位置具有额外的缩进级别。

    ![HTML 编辑器中的智能缩进](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML 编辑器中的智能缩进")

    *HTML 编辑器中的智能缩进*
4. 使用已删除的内容还原音频标记，或在不保存更改的情况下关闭**default.aspx。**

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>任务 6-提取到用户控件

Visual Studio 中包含的重构工具（如将部分代码提取到函数）是一项强大的功能，可帮助改进和重构现有代码。 ASP.NET 页的对应项是将 HTML 代码提取到用户控件。 手动执行此操作需要执行多个步骤，例如创建新的用户控件、将代码部分移到用户控件、为用户控件注册标记前缀，最后在页面上实例化用户控件。 现在，新的 "*提取到用户控件*" 工具会自动执行所有这些步骤。

在此任务中，您将使用新的 "提取到用户控件" 上下文操作从所选代码生成新的用户控件。

1. 在 " **default.aspx** " 页上，选择**H2**和**音频**元素。
2. 右键单击并选择 "**提取到用户控件**"。

    !["提取到用户控件" 菜单选项](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png ""提取到用户控件" 菜单选项")

    *"提取到用户控件" 菜单选项*
3. 键入新用户控件的名称。 例如， **Jukebox**，然后单击 **"确定"** 。

    ![保存提取的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "保存提取的用户控件")

    *保存提取的用户控件*
4. 请注意，已将所选代码提取到用户控件，并将所选代码的原始位置替换为新用户控件的实例。

    ![页面自动更新为使用新的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "页面自动更新为使用新的用户控件")

    *页面自动更新为使用新的用户控件*
5. 按**F5**运行该页并验证控件是否正常工作。

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>练习3： JavaScript 编辑器中的新增功能

编写或编辑 JavaScript 代码不是一项简单的任务，尤其是当你的应用程序开始增长时，你发现自己处理的是长文件和数百个函数。 脚本开发人员通常需要执行一些额外的工作来维护代码的可读性并在文件间导航。 由于包含 jQuery 这类 JavaScript 库，因此脚本导航已经成为一项挑战，因为代码长度。

Visual Studio 已续订 JavaScript 编辑器，使代码模式可访问和组织。 中C#已经存在的许多 Visual Studio 功能现在已在 JavaScript 编辑器中实现：在编写时，请参阅 "定义"、"自动缩进"、"文档" 和 "验证"。 利用续订的 IntelliSense 列表，你可以轻松获得 JavaScript 函数目录。

在此练习中，您将学习 JavaScript 编辑器的一些新功能和改进。 你将浏览示例文件，并发现将使 JavaScript 编程在 Visual Studio 2012 中更有效的每个新特性。

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>任务 1-JavaScript 编辑器新增功能

此任务将向您介绍一些新的 JavaScript 编辑器功能，这些功能侧重于组织您的代码并提供更好的用户体验。

1. 如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。
2. 按**F5**运行应用程序，并单击导航栏中的 "JavaScript" 链接。 多次刷新页面，并检查计数器的增量。

    ![页计数器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "页计数器")

    *页计数器*
3. 关闭浏览器并返回到 Visual Studio。
4. 打开**JavaScript**页并找到 **&lt;脚本&gt;** 块（如下所示）。

    以下代码使用 HTML5 本地存储来存储*pageLoadCount*变量，该变量存储当前用户访问页面的次数。 本地存储是使用 HTML5 标准引入的客户端键-值数据库。 数据保存在用户浏览器中的本地计算机上。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > 在继续执行后续步骤之前，请确保将 DOCTYPE 设置为 XHTML5。
5. 编辑代码，请注意，适用于 JavaScript 的 IntelliSense 包括 HTML5 功能，如本地存储和内部方法。

    ![JavaScript 中的 HTML5 JavaScript 功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 中的 HTML5 JavaScript 功能")

    *JavaScript 中的 HTML5 JavaScript 功能*
6. 单击脚本代码中的任何左大括号（ **{** ），注意括号已突出显示。

    ![突出显示方括号](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "突出显示方括号")

    *突出显示方括号*
7. 取消注释函数**testAutoAlign （）** （选择三行，可以使用**CTRL** + **K**;**CTRL** + **U**），并在函数代码中找到光标。 按 enter 以追加第二行。 请注意，代码现在已**对齐**并**自动缩进**。

    ![JavaScript 代码自动对齐](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 代码自动对齐")

    *JavaScript 代码自动对齐*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>任务 2-验证 JavaScript

在此任务中，您将发现 ECMAScript5 standard 的新 JavaScript 验证。 此功能将帮助你编写符合的 JavaScript 代码，同时防止在部署站点之前出现脚本问题。

> [!NOTE]
> Visual Studio 2010 实现了 ECMAStript3 符合性，而 Visual Studio 2012 提供 ECMAScript5 合规性。

1. 打开位于**Scripts\custom**项目文件夹下的**ECMA5script5。** 现在，你将为 ECMAScript5 standard 测试验证。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    可以在文件的第一行中查看 &quot;**使用 strict** &quot; 方向，这将启用 ECMAScript5**严格模式**。 此模式包含的语言子集阐明了过去版本的歧义，并添加了一些新功能，如 getter 和 setter、对 JSON 的库支持以及对对象属性的完整反射。
2. 如果尚未打开，请打开**错误列表**（"**视图**" 菜单 |**错误列表**）。 请注意，**函数**声明有下划线。 这是因为在 ECMA5 标准函数中不能嵌套在语言结构内。 在下面的错误列表中，你将看到警告的详细信息。

    ![JavaScript 验证错误消息](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 验证错误消息")

    *JavaScript 验证错误消息*
3. 注释掉 **&quot;使用严格&quot;** 方向，注意错误将消失，但仍会出现警告。
4. 在该文件的最后一行中，写入任意字符串（如 **&quot;测试&quot;** （包括引号以指示该字符串是字符串）。 写入字符串旁边的句点以显示 IntelliSense 列表，然后选择 "**剪裁**" 选项。

    在 ECMAScript5 标准中，字符串值和变量也定义了字符串方法，如 trim、大写、搜索和替换。

    ![JavaScript 中的 IntelliSense 列表](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript 中的 IntelliSense 列表")

    *JavaScript 中的 IntelliSense 列表*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>任务 3-JavaScript 的 XML 文档

在此任务中，你将在 JavaScript 中探索 Visual Studio for XML 的功能文档。 你将看到 JavaScript IntelliSense 列表现在显示每个函数的 XML 文档。 此外，你将在 JavaScript 中发现导航功能。

1. 打开位于**脚本/自定义**项目文件夹中的**XMLDoc**文件。 此文件包含有关每个 JavaScript 函数的 XML 文档。

    ![集成到 IntelliSense 的 JavaScript XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "集成到 IntelliSense 的 JavaScript XML 文档")

    *集成到 IntelliSense 的 JavaScript XML 文档*
2. 在**XMLDoc**文件中**添加**函数后，创建一个名为**test**的新函数。
3. 在**测试**函数中，调用接收两个参数的**乘法**函数。 请注意，"工具提示" 框显示的是**乘法**函数文档。

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![JavaScript 函数的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 函数的 XML 文档")

    *JavaScript 函数的 XML 文档*
4. 完成函数 call 语句并键入一个*点*，以打开返回值上的 IntelliSense 列表。 请注意，Visual Studio 在文档中检测**返回**值，将值视为数字。

    ![返回类型的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "返回类型的 XML 文档")

    *返回类型的 XML 文档*
5. 现在，插入对 add 函数的调用。 请注意，JavaScript 编辑器现在支持函数重载。 当你编写函数名称时，你将能够选择文档中指定的任何可用重载。

    ![用于重载的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "用于重载的 XML 文档")

    *用于重载的 XML 文档*
6. 打开**GotoDefinition**文件并找到 **$ （） .html （）** 函数调用。 在**html**上查找光标。
7. 按**F12**并导航到定义。 请注意，现在可以访问和浏览 JavaScript 代码，而无需使用 "**查找**" 工具。
8. 在代码文件底部的签名块之前，找到 jQuery 指令上的光标。 按**F12**。 你将导航到 jQuery 库文件。 请注意，还可以使用**F12**在 jQuery 文件中导航。

    ![导航到 jQuery 定义](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "导航到 jQuery 定义")

    *导航到 jQuery 定义*

> [!NOTE]
> 在保存文件之前，请确保 GotoDefinition 没有语法错误。

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>练习4：捆绑和缩减

网站包含多个 JavaScript 或 CSS 文件有多少次？ 这是一种很常见的情况，在这种情况下，绑定和缩减可以帮助减少文件大小并使站点的执行速度更快。 ASP.NET 4.5 中的新绑定功能将一组 JS 或 CSS 文件打包成单个元素，并通过缩小内容减小其大小（即，删除不需要空格、删除注释、减少标识符）。

ASP.NET 4.5 中的绑定和缩减在运行时执行，因此该进程可以标识用户代理（例如 IE、Mozilla 等），进而通过以用户浏览器为目标来改善压缩（例如，删除特定于 Mozilla 的特定内容）当请求来自 IE 时）。

在此练习中，你将了解如何在 ASP.NET 4.5 中启用和使用不同类型的绑定和缩减。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>任务 1-从 NuGet 安装捆绑包和缩减包

1. 如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。
2. 打开 NuGet 包管理器控制台。 为此，请使用菜单**视图** | **其他 Windows** | **程序包管理器控制台**。

    ![打开包管理器 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "打开程序包管理器控制台")

    *打开程序包管理器控制台*
3. 在 "**程序包管理器控制台**" 中，键入**Install-Package** ，然后按**enter**。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>任务 2-默认捆绑

使用绑定和缩减的最简单方法是启用默认捆绑。 此方法使用约定来使你可以引用文件夹中 JS 和 CSS 文件的捆绑和缩小版本。

在此任务中，你将了解如何启用和引用捆绑的和缩小 JS 和 CSS 文件，并查看生成的输出。

1. 如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。
2. 在**解决方案资源管理器**中，展开 "**样式**"、" **Scripts\custom** " 和 " **Scripts\bundle** " 文件夹。

    请注意，应用程序使用多个 CSS 和 JS 文件。

    ![应用程序中的多个样式表和 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "应用程序中的多个样式表和 JavaScript 文件")

    *应用程序中的多个样式表和 JavaScript 文件*
3. 打开**Global.asax.cs**文件。

    请注意，新的**Microsoft web.config**命名空间在文件开头被注释掉。 取消注释 using 指令以包括绑定和缩减功能。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. 找到**应用程序\_Start**方法。

    在此方法中，取消注释 EnableDefaultBundles 调用，如下面的代码段中所示。 这样，我们便可以通过使用指向该文件夹的路径以及 &quot;CSS&quot; 或 &quot;JS&quot; 后缀，来引用该文件夹中的 CSS 文件的捆绑集合。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. 打开 " **HeadContent** **" 文件**，然后找到 "内容" 控件。

    请注意，CSS 文件和 JS 文件具有单个引用标记。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > 此代码用于演示目的。 理想情况下，将在站点 .Master 文件中引用绑定。 在此示例代码中，你会发现，某些捆绑的文件也被站点 .Master 文件引用，从而使此最后一个引用多余。
6. 请注意，这些链接在**href**属性中使用绑定约定，分别从 Styles 和 Scripts\custom 文件夹获取所有 CSS 或 JS 文件。

    可以使用如下所示的路径**脚本/自定义/JS**来捆绑和缩小**脚本/自定义**文件夹中的所有 JS 文件。 这是默认绑定的默认行为。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. 打开**Styles\Site.css**文件。

    请注意，原始 CSS 文件包含缩进的代码、空格和用于放大文件的注释。 （此外，JavaScript 文件包含空格和注释）。

    ![Scripts 文件夹中的原始 CSS 文件之一](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts 文件夹中的原始 CSS 文件之一")

    *Scripts 文件夹中的原始 CSS 文件之一*
8. 按**F5**运行应用程序并导航到 "**优化**" 页。
9. 单击 " **CSS 捆绑包**" 链接以下载并打开文件。

    查看缩小绑定文件。 你会注意到，已删除所有空格、注释和缩进字符，从而生成较小的文件。

    ![捆绑的 CSS 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "捆绑的 CSS 文件")

    *捆绑的 CSS 文件*
10. 现在，单击 " **JS 包**" 链接以打开 JavaScript 捆绑文件。 您可以放心地忽略资源管理器警告。 请注意，**自定义**文件夹下的 JavaScript 文件也会捆绑在一起，并缩小。

    ![捆绑的 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "捆绑的 JavaScript 文件")

    *捆绑的 JavaScript 文件*

    在以前的 ASP.NET 版本中，为 CSS 或 JS 文件启用压缩要复杂得多。 现在，如您所见，只需在*global.asax*文件中添加一行即可启用绑定，然后引用站点中的捆绑文件。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>任务 3-静态包

利用静态绑定方法，你可以自定义要捆绑的文件集、引用和将使用的缩减方法。

在此任务中，你将配置一个静态捆绑以定义要捆绑的一组特定文件并缩小。

1. 关闭浏览器。
2. 打开**Global.asax.cs**文件并找到**应用程序\_Start**方法。
3. 取消注释静态捆绑代码，如下面的代码所示。

    正在定义一个静态绑定，该绑定将与 &quot; **~/StaticBundle**&quot; 虚拟路径一起引用，并将**JsMinify**用于所有指定文件的缩减**AddFile**方法。 最后，将静态捆绑添加到**bundletable.enableoptimization**并启用它。

    请注意，文件不位于同一位置;这是默认绑定的另一个优点。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. 打开**优化 .aspx**文件。

    请注意，指向**静态 JS 包**的链接正在使用在 Global.asax.cs 文件中配置静态捆绑时声明的路径： **/StaticBundle**。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. 按**F5**运行应用程序，然后导航到 "**优化**" 页。
6. 单击 "**静态 JS 包**" 链接打开该文件。

    请注意，缩小捆绑式 JavaScript 文件是在 &quot;/StaticBundle&quot;路径下的静态捆绑文件中配置的所有 JavaScript 文件的输出。

    ![静态 JavaScript 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "静态 JavaScript 文件捆绑")

    *静态 JavaScript 文件捆绑*
7. 关闭浏览器并返回到 Visual Studio。

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>任务 4-动态文件夹捆绑

在此任务中，你将了解如何配置动态文件夹捆绑。 动态绑定的强大之处在于，你可以包含静态 JavaScript 以及编译为 JavaScript 的语言中的其他文件，因此，在执行捆绑之前需要进行一些处理。

在此示例中，你将学习如何使用**DynamicFolderBundle**类为用 CofeeScript 编写的文件创建动态绑定。 CofeeScript 是一种编程语言，它编译为 JavaScript 并提供更简单的语法来编写 JavaScript 代码，从而增强了 JavaScript 的简洁性和可读性。

1. 打开**Global.asax.cs**文件并找到**应用程序\_Start**方法。
2. 取消注释动态捆绑代码，如下面的代码所示。

    你正在定义一个动态文件夹包，该程序包将使用**CoffeeMinify**自定义缩减处理器，该处理器仅适用于具有 &quot;**咖啡**&quot; 扩展（CoffeeScript 文件）的文件。 请注意，可以使用搜索模式来选择文件夹内要捆绑的文件，如 "\*咖啡"。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. 打开 NuGet 包管理器控制台。 为此，请使用菜单**视图** | **其他 Windows** | **程序包管理器控制台**。
4. 在 "**程序包管理器控制台**" 中，键入**Install-Package CoffeeSharp**并按**enter**。
5. 单击 "**解决方案资源管理器**" 窗口中的 "**显示所有文件**" 按钮

    ![显示所有文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "显示所有文件")

    *显示所有文件*
6. 右键单击**解决方案资源管理器**中的**CoffeeMinify.cs**文件，然后选择 "**包括在项目中**"

    ![将 CoffeeMinify.cs 文件包含在项目中](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "将 CoffeeMinify.cs 文件包含在项目中")

    *将 CoffeeMinify.cs 文件包含在项目中*
7. 打开**CoffeeMinify.cs**文件。

    此类继承自 JsMinify，缩小 CoffeeScript 代码编译生成的 JavaScript 输出。 它调用 CoffeeScript 编译器首先生成 JavaScript 代码，然后将其发送到 JsMinify 方法，以缩小生成的代码。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. 从**Scripts/束**文件夹打开**Script1**和**Script2**文件。

    这些文件将包括在执行与 CoffeeMinify 类的绑定时要编译的 CoffeScript 代码。

    为简单起见，提供的 CoffeeScript 文件仅包括 CoffeeScript 示例代码。 注释被 JsMinify 进程排除。

    ![CoffeeScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 文件")

    *CoffeeScript 文件*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/)提供了一种更简单的语法来编写 javascript 代码，增强了 javascript 的简洁性和可读性，并添加了其他功能，如数组理解和模式匹配。
9. 打开 ""，然后**找到 "绑定**" 链接。

    请注意，通过使用为动态文件夹捆绑配置的 **/Coffee**后缀，**动态 JS 捆绑包**的链接正在引用**脚本/捆绑**文件夹。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. 按**F5**运行应用程序，然后导航到 "**优化**" 页。
11. 单击 "**动态 JS 包**" 链接以打开生成的文件。

    请注意，此捆绑中包含的内容只包含**咖啡**文件。 你还可以看到已将 CoffeeScript 代码编译为 JavaScript，并且已删除已注释掉的行。

    ![动态 JS 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "动态 JS 文件捆绑")

    *动态 JS 文件捆绑*

> [!NOTE]
> 此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。

<a id="Summary"></a>
## <a name="summary"></a>摘要

此实验室可帮助你了解 Visual Studio 2012 的 ASP.NET 和 Web 开发中的新增功能，以及如何利用 Visual Studio 2012 中的各种增强功能。

完成此动手实验后，就可以在 Visual Studio 2012 编辑器中为 CSS、JavaScript 和 HTML 使用新功能和改进了解到。 此外，还可以了解到 Visual Studio 2012 如何实现内置绑定和缩减。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *VS Express for Web 磁贴*

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序

本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-从 Microsoft Azure 门户创建新网站

1. 请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。 你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。

    ![登录到 Windows Azure 门户](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "登录到 Microsoft Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击命令栏上的 "**新建**"。

    ![创建新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "创建新网站")

    *创建新网站*
3. 单击 "**计算** | **网站**"。 然后选择 "**快速创建**" 选项。 为新网站提供可用 URL，并单击 "**创建**网站"。

    > [!NOTE]
    > Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。 它不包括设置数据库的步骤。

    ![使用 "快速创建" 创建新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "使用“快速创建”创建新网站")

    *使用 "快速创建" 创建新网站*
4. 请**等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "打开网站管理页")

    *打开网站管理页*
7. 在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。

    > [!NOTE]
    > *发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。 发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。

    ![下载网站发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。

    ![正在保存发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。 记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。 为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 选择 ip 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框中。 输入规则的名称，并单击 !["添加-客户端-ip 地址-](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png)" 按钮。

    ![添加客户端 IP 地址](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *添加客户端 IP 地址*
3. 将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。

    ![确认更改](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *确认更改*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。

    ![发布应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 "**验证连接**"。 验证完成后，单击 "**下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "正在验证连接")

    *正在验证连接*
4. 在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。

    ![Web 部署配置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。
   - 在 "**用户名**" 中键入服务器管理员登录名。
   - 在 "**密码**" 中键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![正在配置目标连接字符串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 然后单击 **“确定”** 。 系统提示创建数据库时，单击 **"是"** 。

    ![创建数据库](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 再单击 **“下一步”** 。

    ![指向 SQL 数据库的连接字符串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 "**预览**" 页上，单击 "**发布**"。

    ![发布 web 应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

    ![发布到 Windows Azure 的应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "发布到 Windows Azure 的应用程序")

    *发布到 Windows Azure 的应用程序*
