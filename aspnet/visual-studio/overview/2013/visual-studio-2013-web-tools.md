---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 动手实验： Visual Studio 2013 Web Tools |Microsoft Docs
author: rick-anderson
description: Visual Studio 是的优秀开发环境。基于网络的 Windows 和 web 项目。 它包含一个功能强大的文本编辑器，可轻松用于 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505004"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a>动手实验： Visual Studio 2013 Web 工具

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

> Visual Studio 是的优秀开发环境。基于网络的 Windows 和 web 项目。 它包括一个功能强大的文本编辑器，可轻松地在没有项目的情况下编辑独立的文件。
> 
> 编辑每个文件时，Visual Studio 将保留功能完备的分析树。 这使 Visual Studio 能够提供无与伦比的自动完成功能和基于文档的操作，同时使开发体验变得更快、更愉快。 这些功能在 HTML 和 CSS 文档中尤其有用。
> 
> 此功能的所有功能也可用于扩展，这使得使用强大的新功能扩展编辑器以满足你的需求。 Web Essentials 是（主要是） Visual Studio 的 web 相关增强功能的集合。 它包括许多新的 IntelliSense 完成（特别是对于 CSS）、新的浏览器链接功能、适用于 JavaScript 文件的自动 JSHint、HTML 和 CSS 的新警告以及对新式 web 开发所必需的许多其他功能。
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。

<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 使用 Web Essentials 中包含的新 HTML 编辑器功能，如丰富的 HTML5 代码段和 Zen 编码
- 使用 Web Essentials 中包含的新 CSS 编辑器功能，如颜色选取器和浏览器矩阵工具提示
- 使用 Web Essentials 中包含的新 JavaScript 编辑器功能，如 "提取到文件" 和 "适用于所有 HTML 元素的 IntelliSense"
- 使用浏览器链接在浏览器和 Visual Studio 之间交换数据

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下各项：

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)或更高版本
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行此动手实验中的练习，您需要先设置您的环境。

1. 打开 Windows 资源管理器窗口并浏览到实验室的**源**文件夹。
2. 右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。
3. 如果显示了 "用户帐户控制" 对话框，请确认操作以继续。

> [!NOTE]
> 确保在运行安装过程之前，您已检查本实验的所有依赖项。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。

> [!NOTE]
> 每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。 请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。 在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。 如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。

---

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [使用浏览器链接和 Web Essentials](#Exercise1)
2. [利用代码片段和 IntelliSense](#Exercise2)

> [!NOTE]
> 首次启动 Visual Studio 时，必须选择一个预定义的设置集合。 每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。 此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。 如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>练习1：使用浏览器链接和 Web Essentials

**Web Essentials**是一个 Visual Studio 扩展，它为新式 web 开发添加了各种有用的功能，主要侧重于使 web 开发体验变得更快、更愉快。 你可以从 Visual Studio 中的扩展库安装 Web Essentials。

**Browser Link**是 Visual Studio 2013 中包含的一项新功能，它在 VISUAL studio IDE 和任何打开的浏览器之间提供通道，以在 web 应用程序和 Visual Studio 之间交换数据。 Web Essentials 通过工具扩展浏览器链接，直接从浏览器中操作您的网页的 DOM 对象模型和 CSS 样式。

在此练习中，您将探讨**Web Essentials**和**浏览器链接**支持的一些功能，以增强简单的测验页面。

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>任务 1-在多个浏览器中运行项目

在此任务中，你要将 web 应用程序配置为一次在多个浏览器中运行，这对于跨浏览器测试非常有用。

1. 打开**Microsoft Visual Studio**。
2. 在 "**文件**" 菜单中选择 "**打开 |项目/解决方案 ...** 并浏览到实验室的**源**文件夹中的**Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** （C:\WebCampsTK\HOL\VSWebTooling\Source）。 选择 "**开始**"，然后单击 "**打开**"。
3. 在 Visual Studio 工具栏中，展开浏览器菜单，然后选择 "**浏览方式**..."。

    !["浏览方式" 菜单选项](visual-studio-2013-web-tools/_static/image1.png "浏览方式 。浏览器菜单")

    *"浏览方式" 菜单选项*
4. 在 "**浏览方式**" 对话框中，通过按住**CTRL**键并单击 "**设为默认值**"，选择**Google Chrome**和**Internet Explorer** 。

    !["浏览方式" 对话框](visual-studio-2013-web-tools/_static/image2.png ""浏览方式" 对话框")

    *选择多个默认浏览器*
5. Google Chrome 和 Internet Explorer 现在应显示为默认浏览器。 单击“取消”以关闭对话框。

    ![作为默认浏览器的 Google Chrome 和 Internet Explorer](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 和 Internet Explorer 默认浏览器")

    *作为默认浏览器的 Google Chrome 和 Internet Explorer*

    > [!NOTE]
    > 配置默认浏览器后，会在浏览器菜单中选择 "**多个浏览器**" 选项。
    > 
    > ![多个浏览器](visual-studio-2013-web-tools/_static/image4.png "多个浏览器")
6. 按**CTRL** + **F5**运行应用程序而不进行调试。
7. 当浏览器窗口打开时，将其中一个窗口放置在另一台上，以便同时查看两个浏览器上的更新。 浏览器应显示带有浅蓝色矩形的网页。

    ![将一个浏览器放置在另一个浏览器之上](visual-studio-2013-web-tools/_static/image5.png "将一个浏览器放置在另一个浏览器之上")

    *将一个浏览器放置在另一个浏览器之上*
8. 不要关闭浏览器。 你将在下一任务中使用它们。

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>任务 2-使用 Zen 编码创建 HTML 元素

**Zen 编码**是用于高速 HTML、XML、XSL （或任何其他结构化代码格式）编码和编辑的编辑器插件。 此插件的核心是一个功能强大的缩写引擎，可用于将类似于 CSS 选择器的表达式展开为 HTML 代码。 Zen 编码是一种使用 CSS 样式选择器语法编写 HTML 的快捷方法。

在此练习中，您将使用 Web Essentials 提供的 Zen 编码功能生成表示问题的选项的 HTML 按钮。

1. 切换回 Visual Studio。
2. 打开位于 | **Home**文件夹中的**视图**的**索引.**
3. **将&lt;!--TODO：在此处添加选项--&gt;** 注释替换为以下代码，然后按**tab**。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. 应将代码扩展到 HTML。

    ![扩展 HTML](visual-studio-2013-web-tools/_static/image6.png "扩展 HTML")

    *扩展 HTML*

    > [!NOTE]
    > 若要了解有关 Zen 编码语法的详细信息，请参阅以下[文章](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)。
5. 单击 "**刷新链接浏览器**" 按钮可更新这两个浏览器。

    ![刷新链接的浏览器](visual-studio-2013-web-tools/_static/image7.png "刷新链接的浏览器")

    *刷新链接的浏览器*

    ![Internet Explorer-通过四个按钮更新页面](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-通过四个按钮更新页面")

    *Internet Explorer-通过四个按钮更新页面*

    ![Google Chrome-已通过四个按钮更新页面](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-已通过四个按钮更新页面")

    *Google Chrome-已通过四个按钮更新页面*
6. 切换回 Visual Studio。
7. 您已将这些按钮添加到页面中，但仍需要添加一个模板问题。 为此，你将使用 Web Essentials 中名为**Lorem Ipsum 生成器**的新功能。 找到具有**类**属性 "**前部**" 的**div**元素。
8. 添加以下代码作为**div**的第一个子元素，然后按**tab**。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. 应将代码扩展到 HTML。

    ![Lorem Ipsum 自动生成](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 自动生成")

    *Lorem Ipsum 自动生成*

    > [!NOTE]
    > 作为 Zen 编码的一部分，现在可以直接在 HTML 编辑器中生成 Lorem Ipsum 代码。 只需键入 "lorem **" 和 "命中" 选项卡**，将插入一个30个 word lorem Ipsum 文本。 例如， *lorem10*插入10个 Lorem Ipsum 词。
10. 你将在问题的顶部添加徽标，方法是使用名为**Lorem 像素生成器**的 Web Essentials 中的另一个新功能。 将以下代码添加为**div**元素的第一个子元素，并将**容器**作为**类**值，并按**tab**。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. 代码应扩展到 HTML。

    ![自动生成 Lorem 像素](visual-studio-2013-web-tools/_static/image11.png "自动生成 Lorem 像素")

    *自动生成 Lorem 像素*

    > [!NOTE]
    > 作为 Zen 编码的一部分，还可以在 HTML 编辑器中直接生成 Lorem 像素代码。 只需键入 " **200X200 大小"-** "动物 **" 和 "点击" 选项卡**，即可插入带有动物200x200 大小图像的**img**标记。 有关详细信息，请参阅[Lorem 像素](http://www.lorempixel.com)。
12. 单击 "**刷新链接浏览器**" 按钮可更新这两个浏览器。

    ![Internet Explorer-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-自动生成的图像和文本")

    *Internet Explorer-自动生成的图像和文本*

    ![Google Chrome-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-自动生成的图像和文本")

    *Google Chrome-自动生成的图像和文本*

    > [!NOTE]
    > 由于添加代码段时，会随机选择图像，因此浏览器中显示的图像可能会有所不同。
13. 不要关闭浏览器。 你将在下一任务中使用它们。

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>任务 3-更新样式属性

在此任务中，您将使用浏览器链接的**检查模式**功能来检测生成特定 DOM 元素的确切位置，然后使用 Web Essentials 提供的颜色选取器更新该元素的颜色属性。

1. 在 Internet Explorer 浏览器中，按**CTRL** + **ALT** + **I**启用检查模式。
2. 将指针移到浅蓝色边框上，然后单击。

    ![将指针移到浅蓝色边框上](visual-studio-2013-web-tools/_static/image14.png "将指针移到浅蓝色边框上")

    *将指针移到浅蓝色边框上*
3. 切换回 Visual Studio。 请注意，在浏览器中选择的 HTML 元素也会在 Visual Studio HTML 编辑器中进行选择。

    ![Visual Studio HTML 编辑器中选定的 HTML 元素](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 编辑器中选定的 HTML 元素")

    *Visual Studio HTML 编辑器中选定的 HTML 元素*
4. 现在，您将更新**前**一个 CSS 类，以便更改所选元素的样式。 为此，请按**CTRL** + **打开**"**导航到**搜索" 框。 键入 **"** "，然后按**enter**以打开文件。

    ![正在打开文件站点 css](visual-studio-2013-web-tools/_static/image16.png "正在打开文件站点 css")

    *正在打开文件站点 css*
5. 按**CTRL** + **F** ，然后**键入，** 查找 CSS 选择器。
6. 在类的 border 属性中单击浅蓝色正方形，以打开颜色选取器。

    ![打开颜色选取器](visual-studio-2013-web-tools/_static/image17.png "打开颜色选取器")

    *打开颜色选取器*
7. 通过单击 v 形按钮展开颜色选取器，然后选择一种新颜色。

    ![展开颜色选取器](visual-studio-2013-web-tools/_static/image18.png "展开颜色选取器")

    *展开颜色选取器*
8. 按**CTRL** + **ALT** + **enter**以刷新链接的浏览器。
9. 切换到 Internet Explorer，并注意边框的颜色如何变化。

    ![Internet Explorer-已更新边框颜色](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-已更新边框颜色")

    *Internet Explorer-已更新边框颜色*
10. 切换到 Google Chrome 并注意边框的颜色如何变化。

    ![Google Chrome-已更新边框颜色](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-已更新边框颜色")

    *Google Chrome-已更新边框颜色*
11. 切换回 Visual Studio。
12. 请在**web.config**文件的末尾，按**CTRL** + **F**查找**btn**选择器。
13. 请注意， **-webkit**属性以绿色下划线表示。

    ![-btn 选择器的 webkit-radius 属性](visual-studio-2013-web-tools/_static/image21.png "-btn 选择器的 webkit-radius 属性")

    *-btn 选择器的 webkit-radius 属性*
14. 将插入符号放置在 **-webkit**属性中。 该属性的第一个单词的第一个字母下应显示一条蓝线。 这是**智能标记**。
15. 按**CTRL** +  **。** 打开 "建议" 菜单，并单击 "**添加缺少的标准属性（边框-半径）** "。

    ![添加缺少的标准属性建议](visual-studio-2013-web-tools/_static/image22.png "添加缺少的标准属性建议")

    *添加缺少的标准属性建议*
16. **边框-radius**属性会自动添加到 CSS 规则。

    ![缺少添加的标准属性](visual-studio-2013-web-tools/_static/image23.png "缺少添加的标准属性")

    *缺少添加的标准属性*
17. 将指针移到**边框-半径**属性上以显示**浏览器矩阵工具提示**。 **Browser matrix 工具提示**在每个浏览器中显示属性的可用性。

    ![浏览器矩阵工具提示](visual-studio-2013-web-tools/_static/image24.png "浏览器矩阵工具提示")

    *浏览器矩阵工具提示*
18. 请注意，**边框-radius**属性的值仍带有下划线。 将指针移到值上可查看警告消息。

    ![边框-radius 属性值警告](visual-studio-2013-web-tools/_static/image25.png "边框-radius 属性值警告")

    *边框-radius 属性值警告*
19. 如工具提示所建议，删除**边框-radius**属性值的单位。
20. 作为**边框-半径**是用于定义圆角边框的的标准属性，您可以从 CSS 规则中删除 **-webkit-radius**属性和值。
21. 将插入符号放置在**自动换行**属性中，可以看到智能标记也显示在下方。
22. 打开菜单，然后单击 "**添加缺少的供应商详细信息**"。

    ![添加缺少的供应商详细信息建议](visual-studio-2013-web-tools/_static/image26.png "添加缺少的供应商详细信息建议")

    *添加缺少的供应商详细信息建议*
23. **-Ms 自动换行**属性会自动添加到 CSS 规则。

    ![添加的供应商特定属性](visual-studio-2013-web-tools/_static/image27.png "添加的供应商特定属性")

    *添加的供应商特定属性*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>任务 4-从浏览器更新 HTML 代码

在此任务中，您将使用浏览器链接的**设计模式**功能在浏览器中编辑 DOM 对象，并将更改传输到 Visual Studio 中的 HTML 源文件。

1. 在 Google Chrome 中，按**CTRL** + **ALT** + **D**启用设计模式。
2. 将指针移到**Lorem Ipsum dolor sit amet**标签上，然后单击。

    ![编辑问题](visual-studio-2013-web-tools/_static/image28.png "编辑问题")

    *编辑问题*
3. 应显示一个游标。 将原始文本替换为*写入更长问题时的外观*，然后按**ESC**退出设计模式。

    ![已编辑问题](visual-studio-2013-web-tools/_static/image29.png "已编辑问题")

    *已编辑问题*
4. 如果尚未打开，请切换回 Visual Studio 并打开 "**索引"。** 请注意，已更新 **&lt;p&gt;** 元素的内部文本。

    ![HTML 页中已更新的问题](visual-studio-2013-web-tools/_static/image30.png "HTML 页中已更新的问题")

    *HTML 页中已更新的问题*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>任务 5-查看 SEO 相关警告

**搜索引擎优化**（SEO）是在搜索引擎的结果列表中使网站排名更高的过程。 站点排名越高，列出的一致性越多，该站点从该搜索引擎获得的访问者就越多。 Web Essentials 包含一个分析工具，该工具可检查 HTML、报告发现的问题并为修复这些问题提供帮助。

1. 中转到 "**视图**" 菜单，然后单击 "**错误列表**" 打开 "**错误列表**" 窗口。

    !["视图" 菜单中的错误列表](visual-studio-2013-web-tools/_static/image31.png ""视图" 菜单中的错误列表")

    *"视图" 菜单中的错误列表*
2. 请注意，会出现一个 SEO 警告，通知缺少页面说明 **&lt;元&gt;** 标记。 双击 "SEO 警告" 项以修复它。

    ![“错误列表”窗口](visual-studio-2013-web-tools/_static/image32.png "“错误列表”窗口")

    *“错误列表”窗口*
3. 在 " **Web Essentials** " 对话框中，单击 **"是"** 以 &lt;meta&gt; 标记插入描述。

    !["Web Essentials" 对话框](visual-studio-2013-web-tools/_static/image33.png ""Web Essentials" 对话框")

    *"Web Essentials" 对话框*
4. 将打开 **\_布局**的编辑器，并将 **&lt;meta&gt;** 标记自动添加到 HTML 文件的**head**部分。

    ![_Layout 页中自动添加的 Meta 标记](visual-studio-2013-web-tools/_static/image34.png "_Layout 页中自动添加的 Meta 标记")

    *已自动添加到 \_布局页的元标记*
5. 将**content**特性的值更改为*GeekQuiz* ，并保存该文件。

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>练习2：利用代码片段和 IntelliSense

在 Web Essentials 中，HTML 编辑器已通过额外功能进行了扩展。 在此练习中，你将看到一些新功能，这些功能在开发 web 应用程序时非常有用。

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>任务 1-在 HTML 文档中使用 IntelliSense

你将在此任务中看到的第一个新功能称为**动态 IntelliSense**。 动态 IntelliSense 读取其他标记和特性，以推断你将使用的可能 id。

在此任务中，您将创建一个新的 HTML form 元素，该元素包含一个标签和一个输入字段。 然后，您将向该标签添加一个**for**属性以将其绑定到输入，并且您将看到基于范围中输入的 Id 的 IntelliSense 建议。

1. 打开**Visual Studio Express 2013 For Web** ，并打开位于**TakingAdvantageofCodeSnippetsandIntelliSense/begin**文件夹**中的 buildingappswithcachingservice-ex2-getproducts latency-cs 解决方案。** 或者，你可以继续学习你在上一练习中获得的解决方案。
2. 在**解决方案资源管理器**中，打开位于 "**主**文件夹" | "**视图**" 中的 "**索引 ...** " 文件。
3. 将以下窗体添加&gt;元素的 **&lt;节**中。

    （代码段- *VisualStudio2013WebTooling* - *Buildingappswithcachingservice-ex2-getproducts latency-cs* - *窗体*）

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 输入标记前面应带有字段说明的标签。 在输入标记前面添加以下标签。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **&lt;标签&gt;** 的属性指定标签绑定**到的窗**体元素。 特性的值应等于相关元素的 id。 将**for**特性添加到 **&lt;标签&gt;** 元素。 如下图中所示，&quot;名称&quot; 值基于同一范围内的元素的 id （括 **&lt;窗体&gt;** ）在 "IntelliSense" 框中弹出。

    ![在 IntelliSense 中显示 id](visual-studio-2013-web-tools/_static/image35.png "在 IntelliSense 中显示 id")

    *在 IntelliSense 中显示 id*
6. 删除最近添加的 **&lt;表单&gt;** 元素及其内容。

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>任务 2-使用 HTML 代码片段

HTML5 引入了25个以上的新语义标记。 Visual Studio 已经具有这些标记的 IntelliSense 支持，但通过添加新的代码段，Visual Studio 2013 可以更快、更轻松地编写标记。 尽管这些标记并不复杂，但它们附带了几个小微妙之处，例如为*音频*标记添加正确的编解码器回退。 在此任务中，您将看到音频标记的 HTML 代码段。

1. 在 "**索引 ...** " 文件中，在 "&lt;"**部分&gt;** 元素内键入 **&lt;aud** ，如下图所示。

    ![插入音频元素](visual-studio-2013-web-tools/_static/image36.png "插入音频元素")

    *插入音频元素*
2. 按**tab**两次，并注意如何在页上添加以下代码，并将光标放在第一个源的**src**属性上。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > 按**tab**键两次，将插入代码段。 "音频" 代码片段显示*音频*标记的标准用法，其中包含两个源文件以改进支持。
3. 删除第二行并更新第一行的源，并将以下链接更新到 WebCampsTV Katana show： [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)。 生成的代码如下所示。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > 使用源文件*KatanaProject*作为示例。 如果愿意，可以使用其他源。
4. 按**CTRL** + **S**以保存文件。
5. 按**CTRL** + **F5**启动应用程序。
6. 请注意，音频播放器已添加到应用程序。

    ![Internet Explorer 中的音频播放器](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer 中的音频播放器")

    *Internet Explorer 中的音频播放器*

    ![Google Chrome 中的音频播放器](visual-studio-2013-web-tools/_static/image38.png "Google Chrome 中的音频播放器")

    *Google Chrome 中的音频播放器*
7. 不要关闭浏览器。 你将在下一任务中使用它们。

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>任务 3-使用 JavaScript 文档中的 IntelliSense

使用 Web Essentials 2013，样式表和 HTML 页面生成 Id 和类名称的列表。 在此任务中，你将了解这些列表如何改进 Web Essentials 2013 中的 JavaScript IntelliSense 支持。

1. 在**索引 cshtml**文件中，添加以下代码以定义 JavaScript 代码的**脚本**标记。

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. 在**script**标记中添加以下代码，以定义就绪回调函数。

    （代码段- *VisualStudio2013WebTooling* - *buildingappswithcachingservice-ex2-getproducts latency-cs* - *ReadyFunction*）

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. 将插入符号置于**script**标记中，然后按**CTRL** +  **。** 打开 "建议" 菜单。
4. 单击 "**提取到文件**"。

    ![JavaScript 提取到文件建议](visual-studio-2013-web-tools/_static/image39.png "JavaScript 提取到文件建议")

    *JavaScript 提取到文件建议*
5. 在 "**另存为**" 窗口中，选择 "**脚本**" 文件夹，将文件命名为**Init** ，然后单击 "**保存**"。

    ![另存为窗口](visual-studio-2013-web-tools/_static/image40.png "另存为窗口")

    *另存为窗口*

    > [!NOTE]
    > 将创建**init**文件，并将脚本的内容移动到该文件。
    > 
    > ![用包含的内容创建的 Init node.js 文件](visual-studio-2013-web-tools/_static/image41.png "用包含的内容创建的 Init node.js 文件")
    > 
    > *用包含的内容创建的 Init node.js 文件*
6. 打开**索引. cshtml**文件，并检查是否已将脚本标记替换为对**init .js**文件的引用。

    ![Init .js html 参考](visual-studio-2013-web-tools/_static/image42.png "Init .js html 参考")

    *Init .js html 参考*
7. 请参阅**解决方案资源管理器**，并注意**init node.js**文件已自动包含在解决方案中。

    ![解决方案中包含的 Init .js 文件](visual-studio-2013-web-tools/_static/image43.png "解决方案中包含的 Init .js 文件")

    *解决方案中包含的 Init .js 文件*
8. 切换回**init .js**文件以更新**ready**函数回调。
9. 在传递到*ready*的函数回调定义中，添加以下代码以按特定类特性获取所有元素。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. 按**CTRL** + **getElementsByClassName**函数调用内引号之间的**空格**。

    ![显示 getElementsByClassName 函数的 IntelliSense](visual-studio-2013-web-tools/_static/image44.png "显示 getElementsByClassName 函数的 IntelliSense")

    *显示 getElementsByClassName 函数的 IntelliSense*

    > [!NOTE]
    > 请注意，IntelliSense 显示了项目样式表中定义的类。
11. 将创建的行替换为下面的代码。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. 将光标放在**getElementsByTagName**函数中的**引号内，** 并按**CTRL** + **Space**"。

    ![显示 getElementByTagName 方法的 IntelliSense](visual-studio-2013-web-tools/_static/image45.png "显示 getElementByTagName 方法的 IntelliSense")

    *显示 getElementsByTagName 方法的 IntelliSense*
13. 从列表中选择 **&quot;音频&quot;** ，然后按**enter**。 结果如下图所示。

    ![检索音频元素](visual-studio-2013-web-tools/_static/image46.png "检索音频元素")

    *检索音频元素*
14. 在**解决方案资源管理器**中，右键单击**Scripts**文件夹中的缩小文件，然后从**Web Essentials**菜单中**选择 "** **JavaScript 文件**"。

    ![缩小 JavaScript 文件](visual-studio-2013-web-tools/_static/image47.png "缩小 JavaScript 文件")

    *缩小 JavaScript 文件*
15. 当系统提示在源文件更改时启用自动缩减时，请单击 **"是"** 。

    ![启用自动缩减警告](visual-studio-2013-web-tools/_static/image48.png "启用自动缩减警告")

    *启用自动缩减警告*

    > [!NOTE]
    > 将创建**init. node.js** ，并将其添加为**init .js**文件的依赖项。
    > 
    > ![已创建最小的 .js 文件](visual-studio-2013-web-tools/_static/image49.png "已创建最小的 .js 文件")
    > 
    > *已创建最小的 .js 文件*
16. 打开**init. .js**文件，并注意该文件为缩小。

    ![Init. .js 文件内容](visual-studio-2013-web-tools/_static/image50.png "Init. .js 文件内容")

    *Init. .js 文件内容*
17. 在**init .js**文件中，将以下代码添加到**getElementsByTagName**函数调用下以播放所有音频元素。

    （代码段- *VisualStudio2013WebTooling* - *buildingappswithcachingservice-ex2-getproducts latency-cs* - *PlayAudioElements*）

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. 单击 " **CTRL** + **S**以保存文件。 由于已打开缩小文件，因此你将看到一个对话框，指出该文件已在源编辑器之外进行了修改。 单击 **“是”** 。

    ![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
19. 切换回**init .** 文件，以验证该文件是否已用新代码进行更新。

    ![已更新初始. js 文件](visual-studio-2013-web-tools/_static/image52.png "已更新初始. js 文件")

    *已更新初始. js 文件*
20. 单击**浏览器链接刷新**按钮。
21. 两个浏览器刷新后，你在上一任务中看到的音频播放机将自动开始播放。

    ![音频播放器包含在视图中](visual-studio-2013-web-tools/_static/image53.png "音频播放器包含在视图中")

    *音频播放器包含在视图中*

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

通过完成本动手实验，你学习了如何：

- 使用 Web Essentials 中包含的新 HTML 编辑器功能，如丰富的 HTML5 代码段和 Zen 编码
- 使用 Web Essentials 中包含的新 CSS 编辑器功能，如颜色选取器和浏览器矩阵工具提示
- 使用 Web Essentials 中包含的新 JavaScript 编辑器功能，如 "提取到文件" 和 "适用于所有 HTML 元素的 IntelliSense"
- 使用浏览器链接在浏览器和 Visual Studio 之间交换数据
