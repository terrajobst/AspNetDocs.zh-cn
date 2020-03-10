---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 在 Visual Studio 2012 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: 在此动手实验中，你将发现一个新工具，用于在 Visual Studio 中查找和修复网页问题-Page Inspector。 Page Inspector 是一种新工具，
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473798"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a>在 Visual Studio 2012 中使用 Page Inspector

由[Web 训练营团队](https://twitter.com/webcamps)使用

> 在此动手实验中，你将发现一个新工具，用于在 Visual Studio 中查找和修复网页问题-Page Inspector。
> 
> Page Inspector 是一种新工具，它将浏览器诊断工具引入 Visual Studio，并提供浏览器、ASP.NET 和源代码之间的集成体验。 它直接在 Visual Studio IDE 内呈现网页（HTML、Web 窗体、ASP.NET MVC 或网页），并使你可以查看源代码和生成的输出。 Page Inspector 使你能够轻松地分解网站、快速构建页面并快速诊断问题。
> 
> 如今我们有很多 Web 框架，可及时创建灵活、可缩放的网站，例如 ASP.NET MVC 和 WebForms。 另一方面，因为 IDE 不支持基于模板的页面和动态内容中的设计器视图，所以更难找到页面上的问题。 因此，必须在浏览器中打开这些网站才能查看他们对用户的显示方式。
> 
> Web 开发人员使用外部工具来查找定期在浏览器中运行的问题。 然后，它们返回 IDE 并开始修复。 IDE 中的这一前后活动，浏览器和分析工具可能效率低下，有时需要在每次重现问题时进行全新部署和缓存清洗。
> 
> Page Inspector 通过结合使用一组功能，将客户端（浏览器工具）与服务器（ASP.NET 和源代码）之间的 Web 开发的空白带入一起来。
> 
> 使用 Page Inspector，可以查看源文件（包括服务器端代码）中的哪些元素生成了要在浏览器中呈现的 HTML 标记。 还可以通过 Page Inspector 修改 CSS 属性和 DOM 元素特性，以查看立即反映在浏览器中的更改。
> 
> 此动手实验将指导您完成 Page Inspector 功能，并向您演示如何使用这些功能来解决 Web 应用程序中的问题。 **此实验室包含两个使用类似流的练习，但面向不同的技术。如果你是 ASP.NET MVC 开发人员，请执行以下操作之一：如果你是 WebForms 开发人员，请执行两个练习**。
> 
> 此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)提供。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 使用 Page Inspector 分解网站
- 检查和预览 CSS 样式更改与 Page Inspector
- 使用 Page Inspector 检测和修复网页中的问题

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

你必须具有以下项才能完成此实验室：

- 适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。
- Internet Explorer 9 或更高版本

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [练习1：在 ASP.NET MVC 项目中使用 Page Inspector](#Exercise1)
2. [练习2：在 WebForms 项目中使用 Page Inspector](#Exercise2)

> [!NOTE]
> 每个练习都附带了一个起始解决方案，该解决方案位于练习的 "开始" 文件夹中，使您可以单独执行每个练习。 在练习的源代码中，您还会找到一个 End 文件夹，其中包含的 Visual Studio 解决方案的代码是完成相应练习中的步骤所产生的。 如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。

完成本实验的估计时间： **30 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>练习1：在 ASP.NET MVC 项目中使用 Page Inspector

在此练习中，您将学习如何使用**Page Inspector**预览和调试**ASP.NET MVC 4**解决方案。 首先，您将围绕该工具执行一小段重叠，以了解有助于 Web 调试过程的功能。 然后，您将在包含样式问题的网页中工作。 你将了解如何使用 Page Inspector 来查找生成问题并修复此问题的源代码。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>任务 1-探索 Page Inspector

在此任务中，你将了解如何在 ASP.NET MVC 4 项目的上下文中使用 Page Inspector 显示照片库。

1. 打开位于**Source/Ex1-MVC4/begin/** Folder 的**begin**解决方案。

   1. 在继续之前，需要下载一些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 在解决方案资源管理器的 " **/Views/Home** " 项目文件夹下，找到 "**索引**" 视图，右键单击该文件夹，然后选择 **"在 Page Inspector 中查看**"。

    ![选择要预览的文件 Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "选择要预览的文件 Page Inspector")

    *选择要预览的文件 Page Inspector*
3. "Page Inspector" 窗口将显示映射到所选源视图的 */Home/Index* URL。

    ![第一次联系 PageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *第一次与 Page Inspector*

    Page Inspector 工具已集成到 Visual Studio 环境中。 该检查器包含一个嵌入式浏览器以及一个功能强大的 HTML 探查器。 请注意，无需运行解决方案即可查看页面的外观。

    > [!NOTE]
    > 当 Page Inspector 浏览器的宽度小于打开的页面的宽度时，将不会正确显示页面。 如果发生这种情况，请调整 Page Inspector 的宽度。
4. 单击 Page Inspector 中的 "**文件**" 选项卡。

    你将看到构成索引页的所有源文件。 此功能有助于一目了然地识别所有元素，尤其是在使用分部视图和模板时。 请注意，如果单击这些链接，也可以打开每个文件。

    ![The-Files-tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *"文件" 选项卡*
5. 单击位于选项卡左侧的 "**切换检查模式**" 按钮。

    此工具可让你选择页面的任何元素，并查看其 HTML 和 Razor 代码。

    ![Toggle-Inspection-Mode-button](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *切换检查模式按钮*
6. 在 Page Inspector 浏览器中，将鼠标指针移动到页面元素上。 在将鼠标指针移动到呈现的页的任何部分时，将显示元素类型，并在 Visual Studio 编辑器中突出显示相应的源标记或代码。

    ![操作中的检查模式](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *操作中的检查模式*

    > [!NOTE]
    > 不要最大化 Page Inspector 窗口，否则将无法看到显示源代码的预览选项卡。 如果在最大化时单击 Page Inspector 中的元素，则将显示选定内容的源代码，但它将隐藏 "Page Inspector" 窗口。

    如果你注意到**索引 cshtml**文件，你会注意到，将突出显示生成所选元素的源代码部分。 此功能有助于对长源文件进行编辑，同时提供直接快捷的方法来访问代码。

    ![检查元素](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *检查元素*
7. 单击 "**切换检查模式**" 按钮（![选择 "html" 选项卡以显示 Page Inspector 浏览器中呈现的 html 代码。](using-page-inspector-in-visual-studio-2012/_static/image7.png "选择 "HTML" 选项卡以显示 Page Inspector 浏览器中呈现的 HTML 代码。") ）来禁用游标。
8. 选择 " **html** " 选项卡以显示 Page Inspector 浏览器中呈现的 html 代码。
9. 在 HTML 标记中，找到带有 Koala 链接的列表项并将其选中。

    请注意，在选择代码时，相应的输出会自动在浏览器中突出显示。 此功能可用于查看 HTML 块在页面上的呈现方式。

    ![在页面中选择 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image8.png "在页面中选择 HTML 元素")

    *在页面中选择 HTML 元素*
10. 单击 "**切换检查模式**" 按钮以启用*检查模式*并单击导航栏。 在 HTML 代码的右侧，在 "样式" 窗格中，将显示一个列表，其中包含应用于所选元素的 CSS 样式。

    > [!NOTE]
    > 由于标头是网站布局的一部分，因此 Page Inspector 还将打开 \_Layout 文件，并突出显示受影响的代码段。

    ![发现样式](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *查找所选元素的样式和源文件*
11. 启用切换检测指针后，将鼠标指针移动到蓝色的特色栏下方，并单击半圆圈。

    ![选择元素](using-page-inspector-in-visual-studio-2012/_static/image10.png "选择元素")

    *选择元素*
12. 在 "样式" 窗格中，找到 "**主-内容**" 组下的 "**背景图像**" 项。 **取消选中** **背景图像**，看看会发生什么情况。 你会注意到，浏览器会立即反映更改并隐藏圆圈。

    > [!NOTE]
    > 应用于 "Page Inspector 样式" 选项卡上的更改不会影响原始样式表。 您可以根据需要取消选中样式或更改它们的值，但它们将在刷新页面后还原。

    ![启用和禁用 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image11.png "启用和禁用 CSS 样式")

    *启用和禁用 CSS 样式*
13. 现在，使用检查模式在页眉上单击 "**你的徽标**"。
14. 在 "**样式**" 选项卡中，找到 "**网站标题**" 组下的 "**字体大小**" CSS 属性。 双击属性值并将 2.3 em 值替换为**3 em**，然后按**enter**。 请注意，标题看起来更大。

    ![更改 Page Inspector 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image12.png "更改 Page Inspector 中的 CSS 值")

    *更改 Page Inspector 中的 CSS 值*
15. 单击 "**跟踪样式**" 选项卡，该选项卡位于 Page Inspector 右窗格中。 这是查看应用于选择的所有样式的另一种方法，按属性名称排序。

    ![CSS 样式跟踪](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *对所选元素的 CSS 样式跟踪*
16. Page Inspector 的另一项功能是布局窗格。 使用检查模式，选择导航栏，然后单击右窗格中的 "**布局**" 选项卡。 您将看到所选元素的准确大小，以及其偏移、边距、填充和边框大小。 请注意，您还可以通过此视图修改这些值。

    ![Page Inspector 中的元素布局](using-page-inspector-in-visual-studio-2012/_static/image14.png "Page Inspector 中的元素布局")

    *Page Inspector 中的元素布局*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>任务 2-查找和修复照片库中的样式问题

如何诊断 Visual Studio 早期版本的网页问题？ 您可能很熟悉在 Visual Studio IDE 之外（例如 Internet Explorer 开发人员工具或 Firebug）运行的 web 调试工具。 浏览器仅了解 HTML、脚本和样式，而基础框架生成将呈现的 HTML。 出于此原因，通常需要部署整个站点以查看网页的外观。

当你想要检测并修复网站中的问题时，你可能需要执行以下步骤：

1. 从 Visual Studio 运行解决方案，或在 web 服务器上部署页面。
2. 在浏览器中，打开你使用的开发人员工具，或者只是打开源代码和样式并尝试匹配问题。 若要查找所涉及的文件，您可以使用 &quot;搜索&quot; 或 &quot;使用样式类的名称在文件&quot; 功能中搜索。
3. 检测到错误后，停止 Web 浏览器和服务器。
4. 清除浏览器缓存。
5. 返回到 Visual Studio 以应用修补程序。 重复所有要测试的步骤。

由于 ASP.NET MVC 4 中没有实际 WYSIWYG，因此在运行或部署 web 应用程序后，会在稍后的阶段检测到大多数样式问题。 现在，通过 Page Inspector，可以在不运行解决方案的情况下预览任何页面。

在此任务中，您将使用 Page inspector 并修复照片库应用程序的一些问题。

1. 使用 Page Inspector，找到该标头左侧的 "**注册**" 和 "**登录**" 链接。

    请注意，链接不会显示在右侧的预期位置，它们显示为项目符号列表。 现在，将链接向右对齐，并相应地对其进行更改。

    ![查找注册和登录链接](using-page-inspector-in-visual-studio-2012/_static/image15.png "查找注册和登录链接")

    *查找注册和登录链接*
2. 选中 "切换检查模式" 时，单击 "关闭到"，但不要打开 "注册" 链接以打开其代码。

    请注意，链接的源代码位于 **\_loginpartial.cshtml**文件中，而不是位于 \_的位置，也可能是您第一次查找的位置。 您已直接放置在正确的源文件中。
3. 在 "**样式**" 选项卡中，找到并单击 " **\<" 部分 > "#login**项"，这是这些链接的 HTML 容器。

    请注意，单击后，" **#login** " 样式会自动置于 "**站点导航**" 中。 而且，代码现已突出显示。

    ![选择 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image16.png "选择 CSS 样式")

    *选择 CSS 样式*
4. 通过删除开始和结束字符并保存**web.config**文件，取消突出显示的代码中的**文本对齐**属性。

    Page Inspector 知道构成当前页的所有不同文件，并且它可以检测到这些文件中的任何一个发生更改的时间。 只要浏览器中的当前页与源文件不同步，它就会发出警报。
5. 在 Page Inspector 浏览器中，单击地址栏下面的栏以重新加载页面。

    ![重新加载页面](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *重新加载页面*

    现在，链接位于右侧，但其外观仍类似于项目符号列表。 现在，你将删除项目符号并水平对齐链接。

    ![已更新页面](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *已更新页面*
6. 使用检查模式，选择包含 &quot;注册&quot; 的任何 **&lt;li&gt;** 项，并 &quot;&quot; 的链接。 然后，单击 " **&lt;" 部分&gt; "#login** " 项 "以访问**样式。 css**代码。

    ![查找样式](using-page-inspector-in-visual-studio-2012/_static/image19.png "查找样式")

    *查找样式*
7. 在**Style css**中，取消注释 **#login li**项的代码。 要添加的样式将隐藏项目符号并水平显示项。

    ![Restyling 登录链接](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling 登录链接")

    *Restyling 登录链接*
8. 保存**样式 .css**文件，然后单击地址下面的栏以重新加载页面。 请注意，链接正确显示。

    ![与右侧对齐的链接](using-page-inspector-in-visual-studio-2012/_static/image21.png "与右侧对齐的链接")

    *与右侧对齐的链接*
9. 最后，您将更改标题标题。 使用检查模式在此处单击**你的徽标**，并访问生成它的源代码。
10. 现在，你正处于 **\_Layout**，请将 "**你的徽标徽标**" 替换为 "**照片库**"。 保存并更新 Page Inspector 浏览器。

    ![分配新标题](using-page-inspector-in-visual-studio-2012/_static/image22.png "分配新标题")

    *分配新标题*

    ![照片库页面](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *照片库页面已更新*
11. 最后，选择**PhotoGallery**项目，并按**F5**运行该应用程序。 签出所有更改都按预期方式工作。

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>练习2：在 WebForms 项目中使用 Page Inspector

在此练习中，您将学习如何使用 Page Inspector 预览和调试 WebForms 解决方案。 你将首先对该工具执行简短的重叠，以了解有助于 Web 调试过程的 Page Inspector 功能。 然后，您将在包含样式问题的网页中工作。 你将了解如何使用 Page Inspector 来查找生成问题并修复此问题的源代码。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>任务 1-探索 Page Inspector

在此任务中，你将了解如何在 WebForms 项目的上下文中使用 Page Inspector 功能，该项目显示照片库。

1. 打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-WebForms/begin/** Folder 的**begin**解决方案。

   1. 在继续之前，需要下载一些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 在解决方案资源管理器中，找到 " **default.aspx** " 页，右键单击它，然后选择 **"在 Page Inspector 中查看"** 。

    ![用 Page Inspector 打开 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image24.png "用 Page Inspector 打开 default.aspx")

    *用 Page Inspector 打开 default.aspx*
3. "Page Inspector" 窗口将显示 "default.aspx"。

    ![在 Page Inspector 中查看 default.aspx](using-page-inspector-in-visual-studio-2012/_static/image25.png "在 Page Inspector 中查看 default.aspx")

    *在 Page Inspector 中查看 default.aspx*

    Page Inspector 工具已集成到 Visual Studio 环境中。 该检查器包含一个嵌入浏览器以及一个将显示选定代码的功能强大的 HTML 探查器。 请注意，无需运行解决方案即可查看页面的外观。

    > [!NOTE]
    > 当 Page Inspector 浏览器的宽度小于打开的页面的宽度时，将不会正确显示页面。 如果发生这种情况，请调整 Page Inspector 的宽度。
4. 单击 Page Inspector 中的 "**文件**" 选项卡。

    你将看到构成呈现的默认页面的所有源文件。 这是一种非常有用的功能，可帮助您一目了然地识别所有元素，尤其是在使用用户控件和母版页时。 请注意，你也可以导航到每个文件。

    !["文件" 选项卡](using-page-inspector-in-visual-studio-2012/_static/image26.png ""文件" 选项卡")

    *"文件" 选项卡*
5. 单击位于选项卡左侧的 "**切换检查模式**" 按钮。

    此工具可让你选择页面的任何元素，并查看其 HTML 代码和 .aspx 源。

    ![切换检查模式按钮](using-page-inspector-in-visual-studio-2012/_static/image27.png "切换检查模式按钮")

    *切换检查模式按钮*
6. 在 Page Inspector 浏览器中，将鼠标移到页面元素上。 在将鼠标指针移动到呈现的页的任何部分时，将显示元素类型，并在 Visual Studio 编辑器中突出显示相应的源标记或代码。

    ![操作中的检查模式](using-page-inspector-in-visual-studio-2012/_static/image28.png "操作中的检查模式")

    *操作中的检查模式*

    > [!NOTE]
    > 不要最大化 Page Inspector 窗口，否则将无法看到显示源代码的预览选项卡。 如果在最大化时单击 Page Inspector 中的元素，则将显示选定内容的源代码，但它将隐藏 "Page Inspector" 窗口。

    如果你注意到**默认的 .aspx**文件，你会注意到，将突出显示生成所选元素的源代码部分。 此功能简化了长源文件的版本，并提供了一种直接快捷的方法来访问代码。

    ![检查元素](using-page-inspector-in-visual-studio-2012/_static/image29.png "检查元素")

    *检查元素*
7. 单击 "**切换检查模式**" 按钮![（"html"](using-page-inspector-in-visual-studio-2012/_static/image30.png "选择-html-制表符-------------------------------------") --------------------------------------- ）（位于 Page Inspector 选项卡中）来禁用游标。
8. 选择 " **html** " 选项卡以显示 Page Inspector 浏览器中呈现的 html 代码。
9. 在 HTML 代码中，找到带有 Koala 链接的列表项并将其选中。

    请注意，在选择代码时，相应的输出会自动突出显示 "浏览器"。 此功能可用于查看 HTML 块在页面上的呈现方式。

    ![在页面中选择一个 HTML 元素](using-page-inspector-in-visual-studio-2012/_static/image31.png "在页面中选择一个 HTML 元素")

    *在页面中选择一个 HTML 元素*
10. 单击 "**切换检查模式**" 按钮以启用*检查模式*并单击导航栏。 在 HTML 代码的右侧，在 "样式" 窗格中，将显示一个列表，其中包含应用于所选元素的 CSS 样式。

    > [!NOTE]
    > 由于标头是网站布局的一部分，因此 Page Inspector 还将打开网站文件，并突出显示受影响的代码段。

    ![发现样式 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "查找所选元素的样式和源文件")

    *查找所选元素的样式和源文件*
11. 启用切换检测指针后，将鼠标指针移动到菜单栏的下方，并单击空白半圆圈。

    ![选择元素](using-page-inspector-in-visual-studio-2012/_static/image33.png "选择元素")

    *选择元素*
12. 在 "样式" 窗格中，找到 "**主-内容**" 组下的 "**背景图像**" 项。 **取消选中** **背景图像**，看看会发生什么情况。 你会注意到，浏览器会立即反映更改并隐藏圆圈。

    > [!NOTE]
    > 应用于 "Page Inspector 样式" 选项卡上的更改不会影响原始样式表。 您可以根据需要取消选中样式或更改它们的值，但它们将在刷新页面后还原。

    ![启用和禁用 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "启用和禁用 CSS 样式")

    *启用和禁用 CSS 样式*
13. 现在，使用检查模式在页眉上单击 "**你**的**徽标**"。
14. 在 "**样式**" 选项卡中，找到 "**网站标题**" 组下的 "**字体大小**" CSS 属性。 双击属性一次以编辑其值。 将 2.3 em 值替换为**3em**，然后按 enter。 请注意，标题看起来更大。

    ![更改页面 Inspector2 中的 CSS 值](using-page-inspector-in-visual-studio-2012/_static/image35.png "更改 Page Inspector 中的 CSS 值")

    *更改 Page Inspector 中的 CSS 值*
15. 单击 "**跟踪样式**" 选项卡，该选项卡位于 Page Inspector 右窗格中。 这是查看应用于选择的所有样式的另一种方法，按属性名称排序。

    ![对所选元素的 CSS 样式跟踪](using-page-inspector-in-visual-studio-2012/_static/image36.png "对所选元素的 CSS 样式跟踪")

    *对所选元素的 CSS 样式跟踪*
16. Page Inspector 的另一项功能是布局窗格。 使用检查模式，选择导航栏，然后单击右窗格中的 "**布局**" 选项卡。 您将看到所选元素的准确大小，以及其偏移、边距、填充和边框大小。 请注意，您还可以通过此视图修改这些值。

    ![Page Inspector 中的元素布局](using-page-inspector-in-visual-studio-2012/_static/image37.png "Page Inspector 中的元素布局")

    *Page Inspector 中的元素布局*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>任务 2-查找和修复照片库中的样式问题

如何诊断 Visual Studio 早期版本的网页问题？ 您可能很熟悉在 Visual Studio IDE 之外（例如 Internet Explorer 开发人员工具或 Firebug）运行的 web 调试工具。 浏览器仅了解 HTML、脚本和样式，而基础框架生成将呈现的 HTML。 出于此原因，通常需要部署整个站点以查看网页的外观。

当你想要检测并修复网站中的问题时，你可能需要执行以下步骤：

1. 从 Visual Studio 运行解决方案，或在 web 服务器上部署页面。
2. 在浏览器中，打开你使用的开发人员工具，或者只是打开源代码和样式并尝试匹配问题。 若要查找所涉及的文件，您已使用 &quot;搜索&quot; 或 &quot;使用样式类的名称在文件&quot; 功能中搜索。
3. 检测到错误后，停止 Web 浏览器和服务器。
4. 清除浏览器缓存。
5. 返回到 Visual Studio 以应用修补程序。 重复所有要测试的步骤。

由于 ASP.NET WebForms 中没有实际 WYSIWYG，因此在运行或部署后，会在稍后的阶段检测到一些样式问题。 现在，通过 Page Inspector，可以在不运行解决方案的情况下预览任何页面。

在此任务中，您将使用 Page inspector 来修复照片库应用程序的某些问题。 在以下步骤中，你将检测并快速修复标头中的一些简单样式问题。

1. 使用页面检查，找到位于页眉左侧的 "**注册**" 和 "**登录**" 链接。

    请注意，该链接不会显示在右侧的预期位置。 现在，将链接向右对齐并相应地对其进行调整。

    ![位于左侧的 "登录" 链接](using-page-inspector-in-visual-studio-2012/_static/image38.png "位于左侧的 "登录" 链接")

    *位于左侧的 "登录" 链接*
2. 选中 "切换检查模式" 后，选择 "登录" 链接以打开其代码。

    请注意，链接源代码位于**站点 .master**文件中，而不是在 default.aspx 页面中，这是你可能首先查看的位置;您已直接放置在正确的源文件中。
3. 在 "**样式**" 选项卡中，找到并单击 " **&lt;" 部分&gt; "#login**项"，这是这些链接的 HTML 容器。

    请注意，单击后，" **#login** " 样式会自动置于 "**站点导航**" 中。 而且，代码现已突出显示。

    ![选择 CSS 样式](using-page-inspector-in-visual-studio-2012/_static/image39.png "选择 CSS 样式")

    *选择 CSS 样式*
4. 通过删除开始和结束字符并保存**web.config**文件，取消突出显示的代码中的**文本对齐**属性。

    Page Inspector 知道构成当前页的所有不同文件，并且它可以检测到这些文件中的任何一个发生更改的时间。 只要浏览器中的当前页与源文件不同步，它就会发出警报。
5. 在 Page Inspector 浏览器中，单击地址栏下面的栏以保存更改并重新加载页面。

    ![重新加载页面](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *重新加载页面*

    现在，链接位于右侧，但其外观仍类似于项目符号列表。 现在，你将删除项目符号并水平对齐链接。

    ![已更新页面](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *已更新页面*
6. 使用检查模式，选择包含 &quot;注册&quot; 的任何 **&lt;li&gt;** 项，并 &quot;&quot; 的链接。 然后，单击 " **&lt;" 部分&gt; "#login** " 项 "以访问**样式。 css**代码。

    ![查找样式](using-page-inspector-in-visual-studio-2012/_static/image42.png "查找样式")

    *查找样式*
7. 在**Style css**中，取消注释 **#login li**项的代码。 要添加的样式将隐藏项目符号并水平显示项。

    ![Restyling 登录链接](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling 登录链接")

    *Restyling 登录链接*
8. 保存**样式 .css**文件，然后单击地址下面的栏以重新加载页面。 请注意，链接正确显示。

    ![与右侧对齐的链接](using-page-inspector-in-visual-studio-2012/_static/image44.png "与右侧对齐的链接")

    *与右侧对齐的链接*
9. 最后，您将更改标题标题。 请使用检查模式来单击文本，然后转到生成代码的源代码，而不是在所有文件中搜索 "**您的徽标"** 。

    ![查找站点标题](using-page-inspector-in-visual-studio-2012/_static/image45.png "查找站点标题")

    *查找站点标题*
10. 现在你位于 "**网站**" 中，用 "**照片库**" 替换 "**你的徽标**" 文本。 保存并更新 Page Inspector 浏览器。

    ![照片库页面已更新](using-page-inspector-in-visual-studio-2012/_static/image46.png "照片库页面已更新")

    *照片库页面已更新*
11. 最后，按**F5**运行应用程序。签出所有更改都按预期方式工作。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>摘要

完成此动手实验后，就可以了解到如何使用 Page Inspector 预览 Web 应用程序，而无需在浏览器中重新生成并运行该网站。 此外，还了解到了如何通过直接从呈现的输出访问源代码来快速查找和修复 bug。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *VS Express for Web 磁贴*
