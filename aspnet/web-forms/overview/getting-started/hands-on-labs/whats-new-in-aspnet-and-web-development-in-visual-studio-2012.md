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
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="51e63-103">Visual Studio 2012 中 ASP.NET 和 Web 开发的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>

<span data-ttu-id="51e63-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="51e63-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="51e63-105">Visual Studio 的新版本引入了大量增强功能，重点是在使用 Web 技术时改进体验和性能。</span><span class="sxs-lookup"><span data-stu-id="51e63-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="51e63-106">Visual Studio for CSS、JavaScript 和 HTML 已经完全改进，其中包含了许多最按需代码辅助功能，例如 IntelliSense 和自动缩进。</span><span class="sxs-lookup"><span data-stu-id="51e63-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="51e63-107">与性能、绑定和缩减现已集成为内置功能，可轻松减少页面加载时间。</span><span class="sxs-lookup"><span data-stu-id="51e63-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="51e63-108">利用 Visual Studio，你可以使用最新的网站技术。</span><span class="sxs-lookup"><span data-stu-id="51e63-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="51e63-109">你可以使用跨浏览器 CSS3 代码段来确保你的站点正常工作，而不考虑客户端平台，同时利用新的 HTML5 元素和功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="51e63-110">通过此 Visual Studio 版本，编写和分析 JavaScript 代码应该更为容易。</span><span class="sxs-lookup"><span data-stu-id="51e63-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="51e63-111">IntelliSense 列表、集成的 XML 文档和导航功能现在可用于 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="51e63-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="51e63-112">现在，你可以轻松获得 JavaScript 目录。</span><span class="sxs-lookup"><span data-stu-id="51e63-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="51e63-113">此外，还可以检查 ECMAScript5 与脚本的符合性，并在早期阶段检测语法错误。</span><span class="sxs-lookup"><span data-stu-id="51e63-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="51e63-114">最后，但不是最起码，此 Visual Studio 版本实现内置的绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="51e63-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="51e63-115">将打包并压缩脚本文件和样式表，以使站点的执行速度更快。</span><span class="sxs-lookup"><span data-stu-id="51e63-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="51e63-116">此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="51e63-117">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)提供。</span><span class="sxs-lookup"><span data-stu-id="51e63-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="51e63-118">目标</span><span class="sxs-lookup"><span data-stu-id="51e63-118">Objectives</span></span>

<span data-ttu-id="51e63-119">在此动手实验中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="51e63-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="51e63-120">使用 CSS 编辑器中的新功能和改进</span><span class="sxs-lookup"><span data-stu-id="51e63-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="51e63-121">使用 HTML 编辑器中的新功能和改进</span><span class="sxs-lookup"><span data-stu-id="51e63-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="51e63-122">使用 JavaScript 编辑器中的新功能和改进</span><span class="sxs-lookup"><span data-stu-id="51e63-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="51e63-123">配置和使用绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="51e63-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="51e63-124">系统必备</span><span class="sxs-lookup"><span data-stu-id="51e63-124">Prerequisites</span></span>

- <span data-ttu-id="51e63-125">适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。</span><span class="sxs-lookup"><span data-stu-id="51e63-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="51e63-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) （适用于安装程序脚本-已在 windows 8 和 windows Server 2008 R2 上安装）</span><span class="sxs-lookup"><span data-stu-id="51e63-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="51e63-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home)或与 HTML5 兼容的浏览器</span><span class="sxs-lookup"><span data-stu-id="51e63-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="51e63-128">练习</span><span class="sxs-lookup"><span data-stu-id="51e63-128">Exercises</span></span>

<span data-ttu-id="51e63-129">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="51e63-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="51e63-130">练习1： CSS 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="51e63-131">练习2： HTML 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="51e63-132">练习3： JavaScript 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="51e63-133">练习4：捆绑和缩减</span><span class="sxs-lookup"><span data-stu-id="51e63-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="51e63-134">完成本实验的估计时间： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="51e63-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="51e63-135">练习1： CSS 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="51e63-136">Web 开发人员应熟悉与 CSS 编辑相关的很多困难。</span><span class="sxs-lookup"><span data-stu-id="51e63-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="51e63-137">CSS 样式的最大问题之一是跨浏览器兼容性。</span><span class="sxs-lookup"><span data-stu-id="51e63-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="51e63-138">这种情况通常发生在将样式应用到您的网站后，您会发现，如果在另一个浏览器或设备中打开它，它看起来会有所不同。</span><span class="sxs-lookup"><span data-stu-id="51e63-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="51e63-139">因此，您可能会花费相当长的时间来解决这些视觉问题，以了解到，当您最终在一个浏览器中工作时，它会在另一个浏览器中中断。</span><span class="sxs-lookup"><span data-stu-id="51e63-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="51e63-140">Visual Studio 现在包含一些功能，可帮助开发人员有效地访问、处理和组织 CSS 样式表。</span><span class="sxs-lookup"><span data-stu-id="51e63-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="51e63-141">在此练习中，您将满足有效组织版本的新功能，以及用于跨浏览器兼容性的 CSS3 代码片段。</span><span class="sxs-lookup"><span data-stu-id="51e63-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="51e63-142">任务 1-新编辑器功能</span><span class="sxs-lookup"><span data-stu-id="51e63-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="51e63-143">在此任务中，你将发现 "CSS 编辑器" 的新功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="51e63-144">此新编辑器通过利用新的智能缩进、改进的代码注释和增强的 IntelliSense 列表，帮助提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="51e63-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="51e63-145">启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="51e63-146">在解决方案资源管理器中，打开位于 "**样式**" 文件夹下的 "**站点**" 文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="51e63-147">请确保**文本编辑器**工具在工具栏上可见。</span><span class="sxs-lookup"><span data-stu-id="51e63-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="51e63-148">为此，请选择 "**查看** | **工具栏**" 菜单选项，并选中 "**文本编辑器**" 选项。</span><span class="sxs-lookup"><span data-stu-id="51e63-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="51e63-149">你将注意到，由于这一新版本，还为 CSS 编辑器启用了**注释**按钮（![注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)）和**取消注释**按钮（![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)）。</span><span class="sxs-lookup"><span data-stu-id="51e63-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="51e63-150">![启用编辑器和 CSS 工具](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "启用编辑器和 CSS 工具")</span><span class="sxs-lookup"><span data-stu-id="51e63-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="51e63-151">*启用编辑器和 CSS 工具*</span><span class="sxs-lookup"><span data-stu-id="51e63-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="51e63-152">滚动代码并选择任何 CSS 类定义。</span><span class="sxs-lookup"><span data-stu-id="51e63-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="51e63-153">单击 "**注释**" （![注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)） "按钮以注释所选的行。</span><span class="sxs-lookup"><span data-stu-id="51e63-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="51e63-154">然后单击 "**取消注释**（![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)）" 按钮以撤消所做的更改。</span><span class="sxs-lookup"><span data-stu-id="51e63-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="51e63-155">单击 "**折叠**（![折叠](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)）"，然后**展开**（![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) 展开位于文本左边距上的按钮）。</span><span class="sxs-lookup"><span data-stu-id="51e63-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="51e63-156">请注意，现在可以隐藏不使用的样式以使其具有更清晰的视图。</span><span class="sxs-lookup"><span data-stu-id="51e63-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="51e63-157">![折叠 CSS 类](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "折叠 CSS 类")</span><span class="sxs-lookup"><span data-stu-id="51e63-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="51e63-158">*折叠 CSS 类*</span><span class="sxs-lookup"><span data-stu-id="51e63-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="51e63-159">请确保智能缩进功能已启用。</span><span class="sxs-lookup"><span data-stu-id="51e63-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="51e63-160">选择 "**工具**" | "**选项**" 菜单选项，然后在屏幕的左窗格中选择 "**文本编辑器**" | **CSS** | **格式**"页。</span><span class="sxs-lookup"><span data-stu-id="51e63-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="51e63-161">检查**分层缩进**选项。</span><span class="sxs-lookup"><span data-stu-id="51e63-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="51e63-162">![启用分层缩进](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "启用分层缩进")</span><span class="sxs-lookup"><span data-stu-id="51e63-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="51e63-163">*启用分层缩进*</span><span class="sxs-lookup"><span data-stu-id="51e63-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="51e63-164">找到主类定义（main）并向 div 元素追加样式。</span><span class="sxs-lookup"><span data-stu-id="51e63-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="51e63-165">你会注意到，代码自动对齐，帮助用户一目了然地查找父类。</span><span class="sxs-lookup"><span data-stu-id="51e63-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="51e63-166">CSS</span><span class="sxs-lookup"><span data-stu-id="51e63-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="51e63-167">![CSS 中的层次结构对齐](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 中的层次结构对齐")</span><span class="sxs-lookup"><span data-stu-id="51e63-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="51e63-168">*CSS 中的层次结构对齐*</span><span class="sxs-lookup"><span data-stu-id="51e63-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="51e63-169">在**主 div**类的末尾，找到位于边界末尾的光标 **： 0px;** ，然后按**enter**显示 IntelliSense 列表。</span><span class="sxs-lookup"><span data-stu-id="51e63-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="51e63-170">开始键入**top** ，并注意在键入时如何筛选列表。</span><span class="sxs-lookup"><span data-stu-id="51e63-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="51e63-171">此列表将在单词的任何部分显示包含**top**的元素（在 Visual Studio 的先前版本中，该列表由*以术语开头*的项进行筛选）。</span><span class="sxs-lookup"><span data-stu-id="51e63-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="51e63-172">![CSS 中的 IntelliSense 增强功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 中的 IntelliSense 增强功能")</span><span class="sxs-lookup"><span data-stu-id="51e63-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="51e63-173">*CSS 中的 IntelliSense 增强功能*</span><span class="sxs-lookup"><span data-stu-id="51e63-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="51e63-174">任务 2-颜色选取器</span><span class="sxs-lookup"><span data-stu-id="51e63-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="51e63-175">在此任务中，你将发现集成到 Visual Studio IntelliSense 的新 CSS 颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="51e63-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="51e63-176">在 "站点导航" 中 **，** 找到标头类定义（. "标头"），并将光标放在**背景色**属性旁，在 &quot;：&quot; 和 &quot;#该代码行上 &quot; 个字符 **。**</span><span class="sxs-lookup"><span data-stu-id="51e63-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="51e63-177">![定位游标](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "定位游标")</span><span class="sxs-lookup"><span data-stu-id="51e63-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="51e63-178">*定位游标*</span><span class="sxs-lookup"><span data-stu-id="51e63-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="51e63-179">删除**冒号**（:)并再次编写它以显示颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="51e63-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="51e63-180">请注意，你将看到的第一种颜色是网站的最常见颜色。</span><span class="sxs-lookup"><span data-stu-id="51e63-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="51e63-181">如果单击白色颜色，则其 HTML 颜色代码（#fff）将替换样式表中的当前颜色代码。</span><span class="sxs-lookup"><span data-stu-id="51e63-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="51e63-182">![颜色选取器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "颜色选取器")</span><span class="sxs-lookup"><span data-stu-id="51e63-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="51e63-183">*颜色选取器*</span><span class="sxs-lookup"><span data-stu-id="51e63-183">*Color picker*</span></span>
3. <span data-ttu-id="51e63-184">在颜色选取器上按 "**展开**" （![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)） "按钮以显示颜色渐变，然后拖动渐变光标以选择不同的颜色。</span><span class="sxs-lookup"><span data-stu-id="51e63-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="51e63-185">之后，单击 "**取色**器" 按钮，然后从屏幕中选择任意颜色。</span><span class="sxs-lookup"><span data-stu-id="51e63-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="51e63-186">请注意，在移动光标时，背景色值会动态更改。</span><span class="sxs-lookup"><span data-stu-id="51e63-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="51e63-187">![颜色选取器渐变](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "颜色选取器渐变")</span><span class="sxs-lookup"><span data-stu-id="51e63-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="51e63-188">*颜色选取器渐变*</span><span class="sxs-lookup"><span data-stu-id="51e63-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="51e63-189">在**不透明度**滑块中，将选择器移动到条形图的中心，以减小不透明度。</span><span class="sxs-lookup"><span data-stu-id="51e63-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="51e63-190">请注意，背景色值现在会更改为 RGBA 大小。</span><span class="sxs-lookup"><span data-stu-id="51e63-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="51e63-191">![颜色选取器不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "颜色选取器不透明度")</span><span class="sxs-lookup"><span data-stu-id="51e63-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="51e63-192">*颜色选取器不透明度*</span><span class="sxs-lookup"><span data-stu-id="51e63-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-193">CSS3 中的 RGBA （红色、绿色、蓝色和 Alpha）颜色定义允许您定义单个项的颜色不透明度值。</span><span class="sxs-lookup"><span data-stu-id="51e63-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="51e63-194">不同于**不透明度-** 类似的 CSS 特性 **-** RGBA 颜色也与最新浏览器兼容。</span><span class="sxs-lookup"><span data-stu-id="51e63-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="51e63-195">任务 3-CSS 兼容代码段</span><span class="sxs-lookup"><span data-stu-id="51e63-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="51e63-196">在此任务中，您将学习如何使用跨浏览器兼容 CSS3 代码段来实现您网站中的某些功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="51e63-197">在 " **web.config** " 文件中，找到 "**标头**" "css 类定义" （. "标头"），并将光标置于 **/\*border radius\*/** 占位符添加新代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="51e63-198">按**enter**显示 IntelliSense 列表，并键入**radius**以筛选列表。</span><span class="sxs-lookup"><span data-stu-id="51e63-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="51e63-199">从列表中选择一个双击**边框**，并按**tab**键以插入代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="51e63-200">然后，键入半径大小（以像素为单位），然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="51e63-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="51e63-201">例如，键入 " **15px**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="51e63-202">代码段添加的 CSS3 特性将在大多数 HTML5 相容性浏览器（包括 Mozilla 和基于 WebKit 的浏览器）中呈现圆角边框。</span><span class="sxs-lookup"><span data-stu-id="51e63-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="51e63-203">![使用边框-半径代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "使用边框-半径代码段")</span><span class="sxs-lookup"><span data-stu-id="51e63-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="51e63-204">*使用边框-半径代码段*</span><span class="sxs-lookup"><span data-stu-id="51e63-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="51e63-205">在页面样式（. page）中应用相同的**边框**代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="51e63-206">CSS</span><span class="sxs-lookup"><span data-stu-id="51e63-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="51e63-207">按 **“F5”** 运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="51e63-208">请注意，每个页面现在都具有圆角边框。</span><span class="sxs-lookup"><span data-stu-id="51e63-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="51e63-209">![圆角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "圆角")</span><span class="sxs-lookup"><span data-stu-id="51e63-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="51e63-210">*圆角*</span><span class="sxs-lookup"><span data-stu-id="51e63-210">*Rounded corners*</span></span>
4. <span data-ttu-id="51e63-211">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="51e63-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="51e63-212">打开位于 "**样式**" 文件夹下的**自定义 .css**文件，并将光标放在**div 中。**</span><span class="sxs-lookup"><span data-stu-id="51e63-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="51e63-213">按 enter 显示 IntelliSense 列表，键入**框-阴影**，并按**tab**键两次，以便在类定义中插入默认的影子代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="51e63-214">将阴影值设置为**10px 10px 5px #888**。</span><span class="sxs-lookup"><span data-stu-id="51e63-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="51e63-215">然后，键入**border 半径**并插入代码片段。</span><span class="sxs-lookup"><span data-stu-id="51e63-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="51e63-216">键入**15px**以设置 radius 大小并按**enter**。</span><span class="sxs-lookup"><span data-stu-id="51e63-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="51e63-217">![带阴影的圆角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "带阴影的圆角")</span><span class="sxs-lookup"><span data-stu-id="51e63-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="51e63-218">*带阴影的圆角*</span><span class="sxs-lookup"><span data-stu-id="51e63-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-219">此时，将插入带有相应前缀（moz，webkit，o）的影子属性，以支持 Mozilla 和 Webkit （Chrome，Konkeror）浏览器。</span><span class="sxs-lookup"><span data-stu-id="51e63-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="51e63-220">创建新的类**div。 images ul li：将鼠标悬停**在**div**上，将其放在</span><span class="sxs-lookup"><span data-stu-id="51e63-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="51e63-221">CSS</span><span class="sxs-lookup"><span data-stu-id="51e63-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="51e63-222">键入 "**转换**"，并按**tab**键两次以插入转换代码片段。</span><span class="sxs-lookup"><span data-stu-id="51e63-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="51e63-223">然后，输入**旋转（-15deg）** ，以在图像悬停时更改旋转角度值。</span><span class="sxs-lookup"><span data-stu-id="51e63-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="51e63-224">CSS</span><span class="sxs-lookup"><span data-stu-id="51e63-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="51e63-225">按**F5**运行解决方案并浏览到 CSS3 页面。</span><span class="sxs-lookup"><span data-stu-id="51e63-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="51e63-226">请注意，图像具有圆角和框阴影。</span><span class="sxs-lookup"><span data-stu-id="51e63-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="51e63-227">将鼠标指针悬停在图像上，并观察它们是否旋转。</span><span class="sxs-lookup"><span data-stu-id="51e63-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="51e63-228">![转换用于旋转图像的代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "转换用于旋转图像的代码段")</span><span class="sxs-lookup"><span data-stu-id="51e63-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="51e63-229">*转换用于旋转图像的代码段*</span><span class="sxs-lookup"><span data-stu-id="51e63-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-230">如果使用的是 Internet Explorer 10，并且看不到阴影，请确保将文档模式设置为 IE10 标准。</span><span class="sxs-lookup"><span data-stu-id="51e63-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="51e63-231">按**F12**打开 Internet Explorer 开发人员工具，然后单击 "**文档模式**" 更改为 "IE10 标准"。</span><span class="sxs-lookup"><span data-stu-id="51e63-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![关于我们](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="51e63-233">练习2： HTML 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="51e63-234">Visual Studio 具有改进的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="51e63-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="51e63-235">此版本中包含的一些增强功能是 HTML 文档、HTML5 代码段、HTML 开始和结束标记匹配以及 HTML 验证中的智能缩进。</span><span class="sxs-lookup"><span data-stu-id="51e63-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="51e63-236">在此练习中，你将看到这些更改在网站标记中工作时如何提高你的熟练。</span><span class="sxs-lookup"><span data-stu-id="51e63-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="51e63-237">与 CSS 编辑器一样，HTML 编辑器也得到了改进。</span><span class="sxs-lookup"><span data-stu-id="51e63-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="51e63-238">其中的大多数改进都是使 Web 开发人员的工作变得更简单的小型。</span><span class="sxs-lookup"><span data-stu-id="51e63-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="51e63-239">例如，对于 HTML5 的更多代码片段，智能缩进，在编辑和验证目标为 HTML 文档 DOCTYPE 时匹配开始和结束标记是其中的一些改进。</span><span class="sxs-lookup"><span data-stu-id="51e63-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="51e63-240">任务 1-改进了 DOCTYPE 验证</span><span class="sxs-lookup"><span data-stu-id="51e63-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="51e63-241">HTML 编辑器现在可以检查页面的 DOCTYPE，即使该定义可能在母版页中。</span><span class="sxs-lookup"><span data-stu-id="51e63-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="51e63-242">根据页面的 DOCTYPE，HTML 编辑器将验证是否有正确的规则集，并将根据 DOCTYPE 元素筛选 IntelliSense 列表。</span><span class="sxs-lookup"><span data-stu-id="51e63-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="51e63-243">在此任务中，您将更改页面的 DOCTYPE，以查看 HTML 编辑器行为如何相应地更改。</span><span class="sxs-lookup"><span data-stu-id="51e63-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="51e63-244">如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="51e63-245">打开**网站母版页**。</span><span class="sxs-lookup"><span data-stu-id="51e63-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="51e63-246">请注意验证工具栏的目标架构。</span><span class="sxs-lookup"><span data-stu-id="51e63-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="51e63-247">HTML 编辑器的行为方式（验证、IntelliSense 等）将正确更改为符合所选 Doctype。</span><span class="sxs-lookup"><span data-stu-id="51e63-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="51e63-248">![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "在 HTML 源编辑工具栏中使用 Doctype")</span><span class="sxs-lookup"><span data-stu-id="51e63-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="51e63-249">*在 HTML 源编辑工具栏中使用 Doctype*</span><span class="sxs-lookup"><span data-stu-id="51e63-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="51e63-250">将目标架构更改为 HTML 4.01。</span><span class="sxs-lookup"><span data-stu-id="51e63-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="51e63-251">![在 HTML 源编辑工具栏中更改 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "在 HTML 源编辑工具栏中更改 Doctype")</span><span class="sxs-lookup"><span data-stu-id="51e63-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="51e63-252">*在 HTML 源编辑工具栏中更改 Doctype*</span><span class="sxs-lookup"><span data-stu-id="51e63-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="51e63-253">将光标置于**body**元素下，开始键入 HTML5 元素的名称（例如，**视频**）。</span><span class="sxs-lookup"><span data-stu-id="51e63-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="51e63-254">请注意，该元素在 IntelliSense 列表中不可用。</span><span class="sxs-lookup"><span data-stu-id="51e63-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="51e63-255">![未列出 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "未列出 HTML5 元素")</span><span class="sxs-lookup"><span data-stu-id="51e63-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="51e63-256">*未列出 HTML5 元素*</span><span class="sxs-lookup"><span data-stu-id="51e63-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="51e63-257">撤消对验证工具栏的目标架构所做的更改，从下拉列表中选择 "DOCTYPE： XHTML5"。</span><span class="sxs-lookup"><span data-stu-id="51e63-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="51e63-258">![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "在 HTML 源编辑工具栏中使用 Doctype")</span><span class="sxs-lookup"><span data-stu-id="51e63-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="51e63-259">*在 HTML 源编辑工具栏中重置 Doctype*</span><span class="sxs-lookup"><span data-stu-id="51e63-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="51e63-260">将光标置于**body**元素下，并再次开始键入 HTML5 元素（例如，如**视频**）。</span><span class="sxs-lookup"><span data-stu-id="51e63-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="51e63-261">请注意，HTML5 元素现已在 IntelliSense 列表中提供。</span><span class="sxs-lookup"><span data-stu-id="51e63-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="51e63-262">![列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "列出的 HTML5 元素")</span><span class="sxs-lookup"><span data-stu-id="51e63-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="51e63-263">*列出的 HTML5 元素*</span><span class="sxs-lookup"><span data-stu-id="51e63-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="51e63-264">任务 2-开始/结束标记自动更新</span><span class="sxs-lookup"><span data-stu-id="51e63-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="51e63-265">Visual Studio 现在会更新要编辑的元素的 HTML 开始标记或结束标记，使其相互匹配。</span><span class="sxs-lookup"><span data-stu-id="51e63-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="51e63-266">这项新功能将在编辑 HTML 标记时提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="51e63-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="51e63-267">在 " **default.aspx** " 页上，添加一个带标题的**H3**元素（例如，Visual Studio 2012 Rocks！）。</span><span class="sxs-lookup"><span data-stu-id="51e63-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="51e63-268">更改**H3**标记并键入**H2**或**H1。**</span><span class="sxs-lookup"><span data-stu-id="51e63-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="51e63-269">请注意，结束标记会自动更新。</span><span class="sxs-lookup"><span data-stu-id="51e63-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="51e63-270">你还可以修改结束标记，以查看开始标记是否相应更新。</span><span class="sxs-lookup"><span data-stu-id="51e63-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="51e63-271">![自动更新结束标记](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "自动更新结束标记")</span><span class="sxs-lookup"><span data-stu-id="51e63-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="51e63-272">*自动更新结束标记*</span><span class="sxs-lookup"><span data-stu-id="51e63-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="51e63-273">任务 3-新的 HTML5 代码片段</span><span class="sxs-lookup"><span data-stu-id="51e63-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="51e63-274">Visual Studio 现在包含多个 HTML5 代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="51e63-275">在此任务中，您将使用其中一些代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="51e63-276">将名为 "**音频**" 的新文件夹添加到 "网站" 文件夹的根目录。</span><span class="sxs-lookup"><span data-stu-id="51e63-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="51e63-277">打开 Windows 资源管理器并将任何音频文件复制到**WhatsNewASPNET**解决方案的**音频**文件夹中。</span><span class="sxs-lookup"><span data-stu-id="51e63-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="51e63-278">在 " **default.aspx** " 页中，找到 Web11 Rocks！！下的光标。</span><span class="sxs-lookup"><span data-stu-id="51e63-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="51e63-279">标头。</span><span class="sxs-lookup"><span data-stu-id="51e63-279">Header.</span></span> <span data-ttu-id="51e63-280">键入 "**音频**" 并按 tab 键。</span><span class="sxs-lookup"><span data-stu-id="51e63-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="51e63-281">新的 HTML 编辑器包括 HTML5 内容的代码片段。</span><span class="sxs-lookup"><span data-stu-id="51e63-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="51e63-282">请记得使用正确的 DOCTYPE 定义来启用 HTML5 代码段。</span><span class="sxs-lookup"><span data-stu-id="51e63-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="51e63-283">![插入 HTML5 代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "插入 HTML5 代码段")</span><span class="sxs-lookup"><span data-stu-id="51e63-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="51e63-284">*插入 HTML5 代码段*</span><span class="sxs-lookup"><span data-stu-id="51e63-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="51e63-285">更新音频源以指向现有的音频文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="51e63-286">需要将音频文件添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="51e63-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="51e63-287">按**F5**运行该站点并播放音频。</span><span class="sxs-lookup"><span data-stu-id="51e63-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="51e63-288">![运行音频控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "运行音频控件")</span><span class="sxs-lookup"><span data-stu-id="51e63-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="51e63-289">*运行音频控件*</span><span class="sxs-lookup"><span data-stu-id="51e63-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-290">还可以尝试在 Visual Studio 中包含的更多代码段，如视频、图等。</span><span class="sxs-lookup"><span data-stu-id="51e63-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="51e63-291">现在，请尝试在页面的某个部分插入控件。</span><span class="sxs-lookup"><span data-stu-id="51e63-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="51e63-292">例如，尝试插入一个**GridView**控件，而不是键入 **&lt;网格，** 开始键入 **&lt;GV**。</span><span class="sxs-lookup"><span data-stu-id="51e63-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="51e63-293">请注意，IntelliSense 列表显示了**asp： GridView**控件。</span><span class="sxs-lookup"><span data-stu-id="51e63-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="51e63-294">HTML 编辑器中的 IntelliSense 现在提供了标题大小写搜索以及部分匹配（检索包含该字词的所有元素）。</span><span class="sxs-lookup"><span data-stu-id="51e63-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="51e63-295">![使用 IntelliSense 列表插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "使用 IntelliSense 列表插入 GridView")</span><span class="sxs-lookup"><span data-stu-id="51e63-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="51e63-296">*使用 IntelliSense 列表插入 GridView*</span><span class="sxs-lookup"><span data-stu-id="51e63-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="51e63-297">如果键入 **&lt;网格**，将获取与该字词匹配的所有项，但 Visual Studio 将建议**gridview**控件：</span><span class="sxs-lookup"><span data-stu-id="51e63-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="51e63-298">![使用 IntelliSense 列表和部分匹配插入 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "使用 IntelliSense 列表和部分匹配插入 GridView")</span><span class="sxs-lookup"><span data-stu-id="51e63-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="51e63-299">*使用 IntelliSense 列表和部分匹配插入 GridView*</span><span class="sxs-lookup"><span data-stu-id="51e63-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="51e63-300">任务 4-HTML 编辑器智能标记</span><span class="sxs-lookup"><span data-stu-id="51e63-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="51e63-301">HTML 编辑器的另一项改进是智能标记功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="51e63-302">使用智能标记可轻松地按控件执行常见或重复性的开发任务。</span><span class="sxs-lookup"><span data-stu-id="51e63-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="51e63-303">此功能在 HTML 设计器中已可用，但在 HTML 编辑器中不可用。</span><span class="sxs-lookup"><span data-stu-id="51e63-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="51e63-304">打开 "**网站**"，然后找到 " **asp： Menu** " 元素。</span><span class="sxs-lookup"><span data-stu-id="51e63-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="51e63-305">将光标置于开始标记上，注意在元素底部显示的小标志符号，单击它打开 "智能任务" 菜单。</span><span class="sxs-lookup"><span data-stu-id="51e63-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="51e63-306">请注意，您可以快速访问与 Menu 控件相关的一些任务。</span><span class="sxs-lookup"><span data-stu-id="51e63-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="51e63-307">![Menu 控件的智能任务](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Menu 控件的智能任务")</span><span class="sxs-lookup"><span data-stu-id="51e63-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="51e63-308">*Menu 控件的智能任务*</span><span class="sxs-lookup"><span data-stu-id="51e63-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="51e63-309">任务 5-智能缩进</span><span class="sxs-lookup"><span data-stu-id="51e63-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="51e63-310">HTML 中的最佳做法之一是缩进嵌套元素，以使代码更具可读性。</span><span class="sxs-lookup"><span data-stu-id="51e63-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="51e63-311">在 Visual Studio 2012 中，你会注意到，在编写代码时，编辑器会自动缩进元素。</span><span class="sxs-lookup"><span data-stu-id="51e63-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="51e63-312">在 Visual Studio 的早期版本中，智能缩进在 XML 编辑器中可用，但在 HTML 编辑器中可用。</span><span class="sxs-lookup"><span data-stu-id="51e63-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>

1. <span data-ttu-id="51e63-313">请确保 HTML 编辑器上的 "缩进配置" 设置为 "智能缩进"。</span><span class="sxs-lookup"><span data-stu-id="51e63-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="51e63-314">为此，请选择 "**工具" |"选项**" 菜单选项，然后选择 "**文本编辑器" |HTML |** 屏幕的左窗格中的 "选项卡" 页。</span><span class="sxs-lookup"><span data-stu-id="51e63-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="51e63-315">选择 "智能缩进" 选项。</span><span class="sxs-lookup"><span data-stu-id="51e63-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="51e63-316">![HTML 编辑器设置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 编辑器设置")</span><span class="sxs-lookup"><span data-stu-id="51e63-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="51e63-317">*HTML 编辑器设置*</span><span class="sxs-lookup"><span data-stu-id="51e63-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="51e63-318">在 " **default.aspx** " 页上，删除 "音频" 元素下的所有内容。</span><span class="sxs-lookup"><span data-stu-id="51e63-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="51e63-319">将光标置于开始**音频**元素的末尾，然后按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="51e63-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="51e63-320">请注意，游标的新位置具有额外的缩进级别。</span><span class="sxs-lookup"><span data-stu-id="51e63-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="51e63-321">![HTML 编辑器中的智能缩进](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML 编辑器中的智能缩进")</span><span class="sxs-lookup"><span data-stu-id="51e63-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="51e63-322">*HTML 编辑器中的智能缩进*</span><span class="sxs-lookup"><span data-stu-id="51e63-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="51e63-323">使用已删除的内容还原音频标记，或在不保存更改的情况下关闭**default.aspx。**</span><span class="sxs-lookup"><span data-stu-id="51e63-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="51e63-324">任务 6-提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="51e63-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="51e63-325">Visual Studio 中包含的重构工具（如将部分代码提取到函数）是一项强大的功能，可帮助改进和重构现有代码。</span><span class="sxs-lookup"><span data-stu-id="51e63-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="51e63-326">ASP.NET 页的对应项是将 HTML 代码提取到用户控件。</span><span class="sxs-lookup"><span data-stu-id="51e63-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="51e63-327">手动执行此操作需要执行多个步骤，例如创建新的用户控件、将代码部分移到用户控件、为用户控件注册标记前缀，最后在页面上实例化用户控件。</span><span class="sxs-lookup"><span data-stu-id="51e63-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="51e63-328">现在，新的 "*提取到用户控件*" 工具会自动执行所有这些步骤。</span><span class="sxs-lookup"><span data-stu-id="51e63-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="51e63-329">在此任务中，您将使用新的 "提取到用户控件" 上下文操作从所选代码生成新的用户控件。</span><span class="sxs-lookup"><span data-stu-id="51e63-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="51e63-330">在 " **default.aspx** " 页上，选择**H2**和**音频**元素。</span><span class="sxs-lookup"><span data-stu-id="51e63-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="51e63-331">右键单击并选择 "**提取到用户控件**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="51e63-332">!["提取到用户控件" 菜单选项](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png ""提取到用户控件" 菜单选项")</span><span class="sxs-lookup"><span data-stu-id="51e63-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="51e63-333">*"提取到用户控件" 菜单选项*</span><span class="sxs-lookup"><span data-stu-id="51e63-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="51e63-334">键入新用户控件的名称。</span><span class="sxs-lookup"><span data-stu-id="51e63-334">Type a name for the new user control.</span></span> <span data-ttu-id="51e63-335">例如， **Jukebox**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="51e63-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="51e63-336">![保存提取的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "保存提取的用户控件")</span><span class="sxs-lookup"><span data-stu-id="51e63-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="51e63-337">*保存提取的用户控件*</span><span class="sxs-lookup"><span data-stu-id="51e63-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="51e63-338">请注意，已将所选代码提取到用户控件，并将所选代码的原始位置替换为新用户控件的实例。</span><span class="sxs-lookup"><span data-stu-id="51e63-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="51e63-339">![页面自动更新为使用新的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "页面自动更新为使用新的用户控件")</span><span class="sxs-lookup"><span data-stu-id="51e63-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="51e63-340">*页面自动更新为使用新的用户控件*</span><span class="sxs-lookup"><span data-stu-id="51e63-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="51e63-341">按**F5**运行该页并验证控件是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="51e63-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="51e63-342">练习3： JavaScript 编辑器中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="51e63-343">编写或编辑 JavaScript 代码不是一项简单的任务，尤其是当你的应用程序开始增长时，你发现自己处理的是长文件和数百个函数。</span><span class="sxs-lookup"><span data-stu-id="51e63-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="51e63-344">脚本开发人员通常需要执行一些额外的工作来维护代码的可读性并在文件间导航。</span><span class="sxs-lookup"><span data-stu-id="51e63-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="51e63-345">由于包含 jQuery 这类 JavaScript 库，因此脚本导航已经成为一项挑战，因为代码长度。</span><span class="sxs-lookup"><span data-stu-id="51e63-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="51e63-346">Visual Studio 已续订 JavaScript 编辑器，使代码模式可访问和组织。</span><span class="sxs-lookup"><span data-stu-id="51e63-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="51e63-347">中C#已经存在的许多 Visual Studio 功能现在已在 JavaScript 编辑器中实现：在编写时，请参阅 "定义"、"自动缩进"、"文档" 和 "验证"。</span><span class="sxs-lookup"><span data-stu-id="51e63-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="51e63-348">利用续订的 IntelliSense 列表，你可以轻松获得 JavaScript 函数目录。</span><span class="sxs-lookup"><span data-stu-id="51e63-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="51e63-349">在此练习中，您将学习 JavaScript 编辑器的一些新功能和改进。</span><span class="sxs-lookup"><span data-stu-id="51e63-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="51e63-350">你将浏览示例文件，并发现将使 JavaScript 编程在 Visual Studio 2012 中更有效的每个新特性。</span><span class="sxs-lookup"><span data-stu-id="51e63-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="51e63-351">任务 1-JavaScript 编辑器新增功能</span><span class="sxs-lookup"><span data-stu-id="51e63-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="51e63-352">此任务将向您介绍一些新的 JavaScript 编辑器功能，这些功能侧重于组织您的代码并提供更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="51e63-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="51e63-353">如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="51e63-354">按**F5**运行应用程序，并单击导航栏中的 "JavaScript" 链接。</span><span class="sxs-lookup"><span data-stu-id="51e63-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="51e63-355">多次刷新页面，并检查计数器的增量。</span><span class="sxs-lookup"><span data-stu-id="51e63-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="51e63-356">![页计数器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "页计数器")</span><span class="sxs-lookup"><span data-stu-id="51e63-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="51e63-357">*页计数器*</span><span class="sxs-lookup"><span data-stu-id="51e63-357">*Page counter*</span></span>
3. <span data-ttu-id="51e63-358">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="51e63-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="51e63-359">打开**JavaScript**页并找到 **&lt;脚本&gt;** 块（如下所示）。</span><span class="sxs-lookup"><span data-stu-id="51e63-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="51e63-360">以下代码使用 HTML5 本地存储来存储*pageLoadCount*变量，该变量存储当前用户访问页面的次数。</span><span class="sxs-lookup"><span data-stu-id="51e63-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="51e63-361">本地存储是使用 HTML5 标准引入的客户端键-值数据库。</span><span class="sxs-lookup"><span data-stu-id="51e63-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="51e63-362">数据保存在用户浏览器中的本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="51e63-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="51e63-363">在继续执行后续步骤之前，请确保将 DOCTYPE 设置为 XHTML5。</span><span class="sxs-lookup"><span data-stu-id="51e63-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="51e63-364">编辑代码，请注意，适用于 JavaScript 的 IntelliSense 包括 HTML5 功能，如本地存储和内部方法。</span><span class="sxs-lookup"><span data-stu-id="51e63-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="51e63-365">![JavaScript 中的 HTML5 JavaScript 功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 中的 HTML5 JavaScript 功能")</span><span class="sxs-lookup"><span data-stu-id="51e63-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="51e63-366">*JavaScript 中的 HTML5 JavaScript 功能*</span><span class="sxs-lookup"><span data-stu-id="51e63-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="51e63-367">单击脚本代码中的任何左大括号（ **{** ），注意括号已突出显示。</span><span class="sxs-lookup"><span data-stu-id="51e63-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="51e63-368">![突出显示方括号](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "突出显示方括号")</span><span class="sxs-lookup"><span data-stu-id="51e63-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="51e63-369">*突出显示方括号*</span><span class="sxs-lookup"><span data-stu-id="51e63-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="51e63-370">取消注释函数**testAutoAlign （）** （选择三行，可以使用**CTRL** + **K**;**CTRL** + **U**），并在函数代码中找到光标。</span><span class="sxs-lookup"><span data-stu-id="51e63-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="51e63-371">按 enter 以追加第二行。</span><span class="sxs-lookup"><span data-stu-id="51e63-371">Press enter to append a second line.</span></span> <span data-ttu-id="51e63-372">请注意，代码现在已**对齐**并**自动缩进**。</span><span class="sxs-lookup"><span data-stu-id="51e63-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="51e63-373">![JavaScript 代码自动对齐](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 代码自动对齐")</span><span class="sxs-lookup"><span data-stu-id="51e63-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="51e63-374">*JavaScript 代码自动对齐*</span><span class="sxs-lookup"><span data-stu-id="51e63-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="51e63-375">任务 2-验证 JavaScript</span><span class="sxs-lookup"><span data-stu-id="51e63-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="51e63-376">在此任务中，您将发现 ECMAScript5 standard 的新 JavaScript 验证。</span><span class="sxs-lookup"><span data-stu-id="51e63-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="51e63-377">此功能将帮助你编写符合的 JavaScript 代码，同时防止在部署站点之前出现脚本问题。</span><span class="sxs-lookup"><span data-stu-id="51e63-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="51e63-378">Visual Studio 2010 实现了 ECMAStript3 符合性，而 Visual Studio 2012 提供 ECMAScript5 合规性。</span><span class="sxs-lookup"><span data-stu-id="51e63-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>

1. <span data-ttu-id="51e63-379">打开位于**Scripts\custom**项目文件夹下的**ECMA5script5。**</span><span class="sxs-lookup"><span data-stu-id="51e63-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="51e63-380">现在，你将为 ECMAScript5 standard 测试验证。</span><span class="sxs-lookup"><span data-stu-id="51e63-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="51e63-381">可以在文件的第一行中查看 &quot;**使用 strict** &quot; 方向，这将启用 ECMAScript5**严格模式**。</span><span class="sxs-lookup"><span data-stu-id="51e63-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="51e63-382">此模式包含的语言子集阐明了过去版本的歧义，并添加了一些新功能，如 getter 和 setter、对 JSON 的库支持以及对对象属性的完整反射。</span><span class="sxs-lookup"><span data-stu-id="51e63-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="51e63-383">如果尚未打开，请打开**错误列表**（"**视图**" 菜单 |**错误列表**）。</span><span class="sxs-lookup"><span data-stu-id="51e63-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="51e63-384">请注意，**函数**声明有下划线。</span><span class="sxs-lookup"><span data-stu-id="51e63-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="51e63-385">这是因为在 ECMA5 标准函数中不能嵌套在语言结构内。</span><span class="sxs-lookup"><span data-stu-id="51e63-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="51e63-386">在下面的错误列表中，你将看到警告的详细信息。</span><span class="sxs-lookup"><span data-stu-id="51e63-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="51e63-387">![JavaScript 验证错误消息](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 验证错误消息")</span><span class="sxs-lookup"><span data-stu-id="51e63-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="51e63-388">*JavaScript 验证错误消息*</span><span class="sxs-lookup"><span data-stu-id="51e63-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="51e63-389">注释掉 **&quot;使用严格&quot;** 方向，注意错误将消失，但仍会出现警告。</span><span class="sxs-lookup"><span data-stu-id="51e63-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="51e63-390">在该文件的最后一行中，写入任意字符串（如 **&quot;测试&quot;** （包括引号以指示该字符串是字符串）。</span><span class="sxs-lookup"><span data-stu-id="51e63-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="51e63-391">写入字符串旁边的句点以显示 IntelliSense 列表，然后选择 "**剪裁**" 选项。</span><span class="sxs-lookup"><span data-stu-id="51e63-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="51e63-392">在 ECMAScript5 标准中，字符串值和变量也定义了字符串方法，如 trim、大写、搜索和替换。</span><span class="sxs-lookup"><span data-stu-id="51e63-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="51e63-393">![JavaScript 中的 IntelliSense 列表](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript 中的 IntelliSense 列表")</span><span class="sxs-lookup"><span data-stu-id="51e63-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="51e63-394">*JavaScript 中的 IntelliSense 列表*</span><span class="sxs-lookup"><span data-stu-id="51e63-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="51e63-395">任务 3-JavaScript 的 XML 文档</span><span class="sxs-lookup"><span data-stu-id="51e63-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="51e63-396">在此任务中，你将在 JavaScript 中探索 Visual Studio for XML 的功能文档。</span><span class="sxs-lookup"><span data-stu-id="51e63-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="51e63-397">你将看到 JavaScript IntelliSense 列表现在显示每个函数的 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="51e63-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="51e63-398">此外，你将在 JavaScript 中发现导航功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="51e63-399">打开位于**脚本/自定义**项目文件夹中的**XMLDoc**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="51e63-400">此文件包含有关每个 JavaScript 函数的 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="51e63-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="51e63-401">![集成到 IntelliSense 的 JavaScript XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "集成到 IntelliSense 的 JavaScript XML 文档")</span><span class="sxs-lookup"><span data-stu-id="51e63-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="51e63-402">*集成到 IntelliSense 的 JavaScript XML 文档*</span><span class="sxs-lookup"><span data-stu-id="51e63-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="51e63-403">在**XMLDoc**文件中**添加**函数后，创建一个名为**test**的新函数。</span><span class="sxs-lookup"><span data-stu-id="51e63-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="51e63-404">在**测试**函数中，调用接收两个参数的**乘法**函数。</span><span class="sxs-lookup"><span data-stu-id="51e63-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="51e63-405">请注意，"工具提示" 框显示的是**乘法**函数文档。</span><span class="sxs-lookup"><span data-stu-id="51e63-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="51e63-406">![JavaScript 函数的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 函数的 XML 文档")</span><span class="sxs-lookup"><span data-stu-id="51e63-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="51e63-407">*JavaScript 函数的 XML 文档*</span><span class="sxs-lookup"><span data-stu-id="51e63-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="51e63-408">完成函数 call 语句并键入一个*点*，以打开返回值上的 IntelliSense 列表。</span><span class="sxs-lookup"><span data-stu-id="51e63-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="51e63-409">请注意，Visual Studio 在文档中检测**返回**值，将值视为数字。</span><span class="sxs-lookup"><span data-stu-id="51e63-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="51e63-410">![返回类型的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "返回类型的 XML 文档")</span><span class="sxs-lookup"><span data-stu-id="51e63-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="51e63-411">*返回类型的 XML 文档*</span><span class="sxs-lookup"><span data-stu-id="51e63-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="51e63-412">现在，插入对 add 函数的调用。</span><span class="sxs-lookup"><span data-stu-id="51e63-412">Now, insert a call to add function.</span></span> <span data-ttu-id="51e63-413">请注意，JavaScript 编辑器现在支持函数重载。</span><span class="sxs-lookup"><span data-stu-id="51e63-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="51e63-414">当你编写函数名称时，你将能够选择文档中指定的任何可用重载。</span><span class="sxs-lookup"><span data-stu-id="51e63-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="51e63-415">![用于重载的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "用于重载的 XML 文档")</span><span class="sxs-lookup"><span data-stu-id="51e63-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="51e63-416">*用于重载的 XML 文档*</span><span class="sxs-lookup"><span data-stu-id="51e63-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="51e63-417">打开**GotoDefinition**文件并找到 **$ （） .html （）** 函数调用。</span><span class="sxs-lookup"><span data-stu-id="51e63-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="51e63-418">在**html**上查找光标。</span><span class="sxs-lookup"><span data-stu-id="51e63-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="51e63-419">按**F12**并导航到定义。</span><span class="sxs-lookup"><span data-stu-id="51e63-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="51e63-420">请注意，现在可以访问和浏览 JavaScript 代码，而无需使用 "**查找**" 工具。</span><span class="sxs-lookup"><span data-stu-id="51e63-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="51e63-421">在代码文件底部的签名块之前，找到 jQuery 指令上的光标。</span><span class="sxs-lookup"><span data-stu-id="51e63-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="51e63-422">按**F12**。</span><span class="sxs-lookup"><span data-stu-id="51e63-422">Press **F12**.</span></span> <span data-ttu-id="51e63-423">你将导航到 jQuery 库文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="51e63-424">请注意，还可以使用**F12**在 jQuery 文件中导航。</span><span class="sxs-lookup"><span data-stu-id="51e63-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="51e63-425">![导航到 jQuery 定义](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "导航到 jQuery 定义")</span><span class="sxs-lookup"><span data-stu-id="51e63-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="51e63-426">*导航到 jQuery 定义*</span><span class="sxs-lookup"><span data-stu-id="51e63-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="51e63-427">在保存文件之前，请确保 GotoDefinition 没有语法错误。</span><span class="sxs-lookup"><span data-stu-id="51e63-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="51e63-428">练习4：捆绑和缩减</span><span class="sxs-lookup"><span data-stu-id="51e63-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="51e63-429">网站包含多个 JavaScript 或 CSS 文件有多少次？</span><span class="sxs-lookup"><span data-stu-id="51e63-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="51e63-430">这是一种很常见的情况，在这种情况下，绑定和缩减可以帮助减少文件大小并使站点的执行速度更快。</span><span class="sxs-lookup"><span data-stu-id="51e63-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="51e63-431">ASP.NET 4.5 中的新绑定功能将一组 JS 或 CSS 文件打包成单个元素，并通过缩小内容减小其大小（即，删除不需要空格、删除注释、减少标识符）。</span><span class="sxs-lookup"><span data-stu-id="51e63-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="51e63-432">ASP.NET 4.5 中的绑定和缩减在运行时执行，因此该进程可以标识用户代理（例如 IE、Mozilla 等），进而通过以用户浏览器为目标来改善压缩（例如，删除特定于 Mozilla 的特定内容）当请求来自 IE 时）。</span><span class="sxs-lookup"><span data-stu-id="51e63-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="51e63-433">在此练习中，你将了解如何在 ASP.NET 4.5 中启用和使用不同类型的绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="51e63-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="51e63-434">任务 1-从 NuGet 安装捆绑包和缩减包</span><span class="sxs-lookup"><span data-stu-id="51e63-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="51e63-435">如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="51e63-436">打开 NuGet 包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="51e63-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="51e63-437">为此，请使用菜单**视图** | **其他 Windows** | **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="51e63-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="51e63-438">![打开包管理器 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "打开程序包管理器控制台")</span><span class="sxs-lookup"><span data-stu-id="51e63-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="51e63-439">*打开程序包管理器控制台*</span><span class="sxs-lookup"><span data-stu-id="51e63-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="51e63-440">在 "**程序包管理器控制台**" 中，键入**Install-Package** ，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="51e63-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="51e63-441">任务 2-默认捆绑</span><span class="sxs-lookup"><span data-stu-id="51e63-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="51e63-442">使用绑定和缩减的最简单方法是启用默认捆绑。</span><span class="sxs-lookup"><span data-stu-id="51e63-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="51e63-443">此方法使用约定来使你可以引用文件夹中 JS 和 CSS 文件的捆绑和缩小版本。</span><span class="sxs-lookup"><span data-stu-id="51e63-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="51e63-444">在此任务中，你将了解如何启用和引用捆绑的和缩小 JS 和 CSS 文件，并查看生成的输出。</span><span class="sxs-lookup"><span data-stu-id="51e63-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="51e63-445">如果尚未打开，请启动**Visual Studio**并打开位于此实验室的**Source\WhatsNewASPNET**文件夹中的**WhatsNewASPNET**解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="51e63-446">在**解决方案资源管理器**中，展开 "**样式**"、" **Scripts\custom** " 和 " **Scripts\bundle** " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="51e63-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="51e63-447">请注意，应用程序使用多个 CSS 和 JS 文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="51e63-448">![应用程序中的多个样式表和 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "应用程序中的多个样式表和 JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="51e63-449">*应用程序中的多个样式表和 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="51e63-450">打开**Global.asax.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="51e63-451">请注意，新的**Microsoft web.config**命名空间在文件开头被注释掉。</span><span class="sxs-lookup"><span data-stu-id="51e63-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="51e63-452">取消注释 using 指令以包括绑定和缩减功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="51e63-453">找到**应用程序\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="51e63-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="51e63-454">在此方法中，取消注释 EnableDefaultBundles 调用，如下面的代码段中所示。</span><span class="sxs-lookup"><span data-stu-id="51e63-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="51e63-455">这样，我们便可以通过使用指向该文件夹的路径以及 &quot;CSS&quot; 或 &quot;JS&quot; 后缀，来引用该文件夹中的 CSS 文件的捆绑集合。</span><span class="sxs-lookup"><span data-stu-id="51e63-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="51e63-456">打开 " **HeadContent** **" 文件**，然后找到 "内容" 控件。</span><span class="sxs-lookup"><span data-stu-id="51e63-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="51e63-457">请注意，CSS 文件和 JS 文件具有单个引用标记。</span><span class="sxs-lookup"><span data-stu-id="51e63-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="51e63-458">此代码用于演示目的。</span><span class="sxs-lookup"><span data-stu-id="51e63-458">This code is for demo purposes.</span></span> <span data-ttu-id="51e63-459">理想情况下，将在站点 .Master 文件中引用绑定。</span><span class="sxs-lookup"><span data-stu-id="51e63-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="51e63-460">在此示例代码中，你会发现，某些捆绑的文件也被站点 .Master 文件引用，从而使此最后一个引用多余。</span><span class="sxs-lookup"><span data-stu-id="51e63-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="51e63-461">请注意，这些链接在**href**属性中使用绑定约定，分别从 Styles 和 Scripts\custom 文件夹获取所有 CSS 或 JS 文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="51e63-462">可以使用如下所示的路径**脚本/自定义/JS**来捆绑和缩小**脚本/自定义**文件夹中的所有 JS 文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="51e63-463">这是默认绑定的默认行为。</span><span class="sxs-lookup"><span data-stu-id="51e63-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="51e63-464">打开**Styles\Site.css**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="51e63-465">请注意，原始 CSS 文件包含缩进的代码、空格和用于放大文件的注释。</span><span class="sxs-lookup"><span data-stu-id="51e63-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="51e63-466">（此外，JavaScript 文件包含空格和注释）。</span><span class="sxs-lookup"><span data-stu-id="51e63-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="51e63-467">![Scripts 文件夹中的原始 CSS 文件之一](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts 文件夹中的原始 CSS 文件之一")</span><span class="sxs-lookup"><span data-stu-id="51e63-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="51e63-468">*Scripts 文件夹中的原始 CSS 文件之一*</span><span class="sxs-lookup"><span data-stu-id="51e63-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="51e63-469">按**F5**运行应用程序并导航到 "**优化**" 页。</span><span class="sxs-lookup"><span data-stu-id="51e63-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="51e63-470">单击 " **CSS 捆绑包**" 链接以下载并打开文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="51e63-471">查看缩小绑定文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-471">Check out the minified bundled file.</span></span> <span data-ttu-id="51e63-472">你会注意到，已删除所有空格、注释和缩进字符，从而生成较小的文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="51e63-473">![捆绑的 CSS 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "捆绑的 CSS 文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="51e63-474">*捆绑的 CSS 文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="51e63-475">现在，单击 " **JS 包**" 链接以打开 JavaScript 捆绑文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="51e63-476">您可以放心地忽略资源管理器警告。</span><span class="sxs-lookup"><span data-stu-id="51e63-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="51e63-477">请注意，**自定义**文件夹下的 JavaScript 文件也会捆绑在一起，并缩小。</span><span class="sxs-lookup"><span data-stu-id="51e63-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="51e63-478">![捆绑的 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "捆绑的 JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="51e63-479">*捆绑的 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="51e63-480">在以前的 ASP.NET 版本中，为 CSS 或 JS 文件启用压缩要复杂得多。</span><span class="sxs-lookup"><span data-stu-id="51e63-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="51e63-481">现在，如您所见，只需在*global.asax*文件中添加一行即可启用绑定，然后引用站点中的捆绑文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="51e63-482">任务 3-静态包</span><span class="sxs-lookup"><span data-stu-id="51e63-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="51e63-483">利用静态绑定方法，你可以自定义要捆绑的文件集、引用和将使用的缩减方法。</span><span class="sxs-lookup"><span data-stu-id="51e63-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="51e63-484">在此任务中，你将配置一个静态捆绑以定义要捆绑的一组特定文件并缩小。</span><span class="sxs-lookup"><span data-stu-id="51e63-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="51e63-485">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="51e63-485">Close the browser.</span></span>
2. <span data-ttu-id="51e63-486">打开**Global.asax.cs**文件并找到**应用程序\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="51e63-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="51e63-487">取消注释静态捆绑代码，如下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="51e63-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="51e63-488">正在定义一个静态绑定，该绑定将与 &quot; **~/StaticBundle**&quot; 虚拟路径一起引用，并将**JsMinify**用于所有指定文件的缩减**AddFile**方法。</span><span class="sxs-lookup"><span data-stu-id="51e63-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="51e63-489">最后，将静态捆绑添加到**bundletable.enableoptimization**并启用它。</span><span class="sxs-lookup"><span data-stu-id="51e63-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="51e63-490">请注意，文件不位于同一位置;这是默认绑定的另一个优点。</span><span class="sxs-lookup"><span data-stu-id="51e63-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="51e63-491">打开**优化 .aspx**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="51e63-492">请注意，指向**静态 JS 包**的链接正在使用在 Global.asax.cs 文件中配置静态捆绑时声明的路径： **/StaticBundle**。</span><span class="sxs-lookup"><span data-stu-id="51e63-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="51e63-493">按**F5**运行应用程序，然后导航到 "**优化**" 页。</span><span class="sxs-lookup"><span data-stu-id="51e63-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="51e63-494">单击 "**静态 JS 包**" 链接打开该文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="51e63-495">请注意，缩小捆绑式 JavaScript 文件是在 &quot;/StaticBundle&quot;路径下的静态捆绑文件中配置的所有 JavaScript 文件的输出。</span><span class="sxs-lookup"><span data-stu-id="51e63-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="51e63-496">![静态 JavaScript 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "静态 JavaScript 文件捆绑")</span><span class="sxs-lookup"><span data-stu-id="51e63-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="51e63-497">*静态 JavaScript 文件捆绑*</span><span class="sxs-lookup"><span data-stu-id="51e63-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="51e63-498">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="51e63-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="51e63-499">任务 4-动态文件夹捆绑</span><span class="sxs-lookup"><span data-stu-id="51e63-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="51e63-500">在此任务中，你将了解如何配置动态文件夹捆绑。</span><span class="sxs-lookup"><span data-stu-id="51e63-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="51e63-501">动态绑定的强大之处在于，你可以包含静态 JavaScript 以及编译为 JavaScript 的语言中的其他文件，因此，在执行捆绑之前需要进行一些处理。</span><span class="sxs-lookup"><span data-stu-id="51e63-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="51e63-502">在此示例中，你将学习如何使用**DynamicFolderBundle**类为用 CofeeScript 编写的文件创建动态绑定。</span><span class="sxs-lookup"><span data-stu-id="51e63-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="51e63-503">CofeeScript 是一种编程语言，它编译为 JavaScript 并提供更简单的语法来编写 JavaScript 代码，从而增强了 JavaScript 的简洁性和可读性。</span><span class="sxs-lookup"><span data-stu-id="51e63-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="51e63-504">打开**Global.asax.cs**文件并找到**应用程序\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="51e63-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="51e63-505">取消注释动态捆绑代码，如下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="51e63-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="51e63-506">你正在定义一个动态文件夹包，该程序包将使用**CoffeeMinify**自定义缩减处理器，该处理器仅适用于具有 &quot;**咖啡**&quot; 扩展（CoffeeScript 文件）的文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="51e63-507">请注意，可以使用搜索模式来选择文件夹内要捆绑的文件，如 "\*咖啡"。</span><span class="sxs-lookup"><span data-stu-id="51e63-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="51e63-508">打开 NuGet 包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="51e63-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="51e63-509">为此，请使用菜单**视图** | **其他 Windows** | **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="51e63-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="51e63-510">在 "**程序包管理器控制台**" 中，键入**Install-Package CoffeeSharp**并按**enter**。</span><span class="sxs-lookup"><span data-stu-id="51e63-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="51e63-511">单击 "**解决方案资源管理器**" 窗口中的 "**显示所有文件**" 按钮</span><span class="sxs-lookup"><span data-stu-id="51e63-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="51e63-512">![显示所有文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "显示所有文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="51e63-513">*显示所有文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-513">*Showing all files*</span></span>
6. <span data-ttu-id="51e63-514">右键单击**解决方案资源管理器**中的**CoffeeMinify.cs**文件，然后选择 "**包括在项目中**"</span><span class="sxs-lookup"><span data-stu-id="51e63-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="51e63-515">![将 CoffeeMinify.cs 文件包含在项目中](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "将 CoffeeMinify.cs 文件包含在项目中")</span><span class="sxs-lookup"><span data-stu-id="51e63-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="51e63-516">*将 CoffeeMinify.cs 文件包含在项目中*</span><span class="sxs-lookup"><span data-stu-id="51e63-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="51e63-517">打开**CoffeeMinify.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="51e63-518">此类继承自 JsMinify，缩小 CoffeeScript 代码编译生成的 JavaScript 输出。</span><span class="sxs-lookup"><span data-stu-id="51e63-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="51e63-519">它调用 CoffeeScript 编译器首先生成 JavaScript 代码，然后将其发送到 JsMinify 方法，以缩小生成的代码。</span><span class="sxs-lookup"><span data-stu-id="51e63-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="51e63-520">从**Scripts/束**文件夹打开**Script1**和**Script2**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="51e63-521">这些文件将包括在执行与 CoffeeMinify 类的绑定时要编译的 CoffeScript 代码。</span><span class="sxs-lookup"><span data-stu-id="51e63-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="51e63-522">为简单起见，提供的 CoffeeScript 文件仅包括 CoffeeScript 示例代码。</span><span class="sxs-lookup"><span data-stu-id="51e63-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="51e63-523">注释被 JsMinify 进程排除。</span><span class="sxs-lookup"><span data-stu-id="51e63-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="51e63-524">![CoffeeScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="51e63-525">*CoffeeScript 文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-526">[CofeeScript](https://github.com/jashkenas/coffeescript/)提供了一种更简单的语法来编写 javascript 代码，增强了 javascript 的简洁性和可读性，并添加了其他功能，如数组理解和模式匹配。</span><span class="sxs-lookup"><span data-stu-id="51e63-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="51e63-527">打开 ""，然后**找到 "绑定**" 链接。</span><span class="sxs-lookup"><span data-stu-id="51e63-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="51e63-528">请注意，通过使用为动态文件夹捆绑配置的 **/Coffee**后缀，**动态 JS 捆绑包**的链接正在引用**脚本/捆绑**文件夹。</span><span class="sxs-lookup"><span data-stu-id="51e63-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="51e63-529">按**F5**运行应用程序，然后导航到 "**优化**" 页。</span><span class="sxs-lookup"><span data-stu-id="51e63-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="51e63-530">单击 "**动态 JS 包**" 链接以打开生成的文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="51e63-531">请注意，此捆绑中包含的内容只包含**咖啡**文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="51e63-532">你还可以看到已将 CoffeeScript 代码编译为 JavaScript，并且已删除已注释掉的行。</span><span class="sxs-lookup"><span data-stu-id="51e63-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="51e63-533">![动态 JS 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "动态 JS 文件捆绑")</span><span class="sxs-lookup"><span data-stu-id="51e63-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="51e63-534">*动态 JS 文件捆绑*</span><span class="sxs-lookup"><span data-stu-id="51e63-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="51e63-535">此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。</span><span class="sxs-lookup"><span data-stu-id="51e63-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="51e63-536">摘要</span><span class="sxs-lookup"><span data-stu-id="51e63-536">Summary</span></span>

<span data-ttu-id="51e63-537">此实验室可帮助你了解 Visual Studio 2012 的 ASP.NET 和 Web 开发中的新增功能，以及如何利用 Visual Studio 2012 中的各种增强功能。</span><span class="sxs-lookup"><span data-stu-id="51e63-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="51e63-538">完成此动手实验后，就可以在 Visual Studio 2012 编辑器中为 CSS、JavaScript 和 HTML 使用新功能和改进了解到。</span><span class="sxs-lookup"><span data-stu-id="51e63-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="51e63-539">此外，还可以了解到 Visual Studio 2012 如何实现内置绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="51e63-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="51e63-540">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="51e63-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="51e63-541">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="51e63-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="51e63-542">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="51e63-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="51e63-543">请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="51e63-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="51e63-544">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="51e63-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="51e63-545">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-545">Click on **Install Now**.</span></span> <span data-ttu-id="51e63-546">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="51e63-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="51e63-547">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="51e63-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="51e63-548">![安装 Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="51e63-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="51e63-549">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="51e63-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="51e63-550">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="51e63-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="51e63-552">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="51e63-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="51e63-553">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="51e63-553">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="51e63-555">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="51e63-555">*Installation progress*</span></span>
6. <span data-ttu-id="51e63-556">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-556">When the installation completes, click **Finish**.</span></span>

    ![安装完成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="51e63-558">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="51e63-558">*Installation completed*</span></span>
7. <span data-ttu-id="51e63-559">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="51e63-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="51e63-560">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="51e63-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="51e63-562">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="51e63-562">*VS Express for Web tile*</span></span>

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="51e63-563">附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="51e63-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="51e63-564">本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。</span><span class="sxs-lookup"><span data-stu-id="51e63-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="51e63-565">任务 1-从 Microsoft Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="51e63-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="51e63-566">请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="51e63-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-567">借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。</span><span class="sxs-lookup"><span data-stu-id="51e63-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="51e63-568">你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。</span><span class="sxs-lookup"><span data-stu-id="51e63-568">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="51e63-569">![登录到 Windows Azure 门户](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "登录到 Microsoft Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="51e63-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="51e63-570">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="51e63-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="51e63-571">单击命令栏上的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="51e63-572">![创建新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="51e63-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="51e63-573">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="51e63-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="51e63-574">单击 "**计算** | **网站**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="51e63-575">然后选择 "**快速创建**" 选项。</span><span class="sxs-lookup"><span data-stu-id="51e63-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="51e63-576">为新网站提供可用 URL，并单击 "**创建**网站"。</span><span class="sxs-lookup"><span data-stu-id="51e63-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-577">Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。</span><span class="sxs-lookup"><span data-stu-id="51e63-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="51e63-578">使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="51e63-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="51e63-579">它不包括设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="51e63-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="51e63-580">![使用 "快速创建" 创建新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "使用“快速创建”创建新网站")</span><span class="sxs-lookup"><span data-stu-id="51e63-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="51e63-581">*使用 "快速创建" 创建新网站*</span><span class="sxs-lookup"><span data-stu-id="51e63-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="51e63-582">请**等到新网站创建完毕。**</span><span class="sxs-lookup"><span data-stu-id="51e63-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="51e63-583">创建网站后，单击 " **URL** " 列下的链接。</span><span class="sxs-lookup"><span data-stu-id="51e63-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="51e63-584">检查新网站是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="51e63-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="51e63-585">![浏览到新网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "浏览到新网站")</span><span class="sxs-lookup"><span data-stu-id="51e63-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="51e63-586">*浏览到新网站*</span><span class="sxs-lookup"><span data-stu-id="51e63-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="51e63-587">![网站正在运行](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "网站正在运行")</span><span class="sxs-lookup"><span data-stu-id="51e63-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="51e63-588">*网站正在运行*</span><span class="sxs-lookup"><span data-stu-id="51e63-588">*Web site running*</span></span>
6. <span data-ttu-id="51e63-589">返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="51e63-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="51e63-590">![打开网站管理页](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="51e63-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="51e63-591">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="51e63-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="51e63-592">在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。</span><span class="sxs-lookup"><span data-stu-id="51e63-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-593">*发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="51e63-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="51e63-594">发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="51e63-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="51e63-595">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="51e63-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="51e63-596">![下载网站发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="51e63-597">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="51e63-598">将发布配置文件下载到已知位置。</span><span class="sxs-lookup"><span data-stu-id="51e63-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="51e63-599">在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="51e63-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="51e63-600">![正在保存发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "正在保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="51e63-601">*正在保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="51e63-602">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="51e63-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="51e63-603">如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="51e63-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="51e63-604">如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="51e63-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="51e63-605">你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="51e63-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="51e63-606">可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="51e63-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="51e63-607">如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。</span><span class="sxs-lookup"><span data-stu-id="51e63-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="51e63-608">记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="51e63-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="51e63-609">请不要创建数据库，因为它将在后面的阶段创建。</span><span class="sxs-lookup"><span data-stu-id="51e63-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="51e63-610">![SQL 数据库服务器仪表板](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL 数据库服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="51e63-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="51e63-611">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="51e63-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="51e63-612">在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="51e63-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="51e63-613">为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 选择 ip 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="51e63-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="51e63-614">输入规则的名称，并单击 !["添加-客户端-ip 地址-](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png)" 按钮。</span><span class="sxs-lookup"><span data-stu-id="51e63-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="51e63-616">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="51e63-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="51e63-617">将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。</span><span class="sxs-lookup"><span data-stu-id="51e63-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="51e63-619">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="51e63-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="51e63-620">任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="51e63-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="51e63-621">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="51e63-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="51e63-622">在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="51e63-623">![发布应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="51e63-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="51e63-624">*发布网站*</span><span class="sxs-lookup"><span data-stu-id="51e63-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="51e63-625">导入您在第一个任务中保存的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="51e63-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="51e63-626">![导入发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="51e63-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="51e63-627">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="51e63-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="51e63-628">单击 "**验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-628">Click **Validate Connection**.</span></span> <span data-ttu-id="51e63-629">验证完成后，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="51e63-630">验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="51e63-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="51e63-631">![正在验证连接](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "正在验证连接")</span><span class="sxs-lookup"><span data-stu-id="51e63-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="51e63-632">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="51e63-632">*Validating connection*</span></span>
4. <span data-ttu-id="51e63-633">在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="51e63-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="51e63-634">![Web 部署配置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="51e63-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="51e63-635">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="51e63-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="51e63-636">按如下所示配置数据库连接：</span><span class="sxs-lookup"><span data-stu-id="51e63-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="51e63-637">在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。</span><span class="sxs-lookup"><span data-stu-id="51e63-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="51e63-638">在 "**用户名**" 中键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="51e63-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="51e63-639">在 "**密码**" 中键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="51e63-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="51e63-640">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="51e63-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="51e63-641">![正在配置目标连接字符串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "正在配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="51e63-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="51e63-642">*正在配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="51e63-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="51e63-643">然后单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="51e63-643">Then click **OK**.</span></span> <span data-ttu-id="51e63-644">系统提示创建数据库时，单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="51e63-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="51e63-645">![创建数据库](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="51e63-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="51e63-646">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="51e63-646">*Creating the database*</span></span>
7. <span data-ttu-id="51e63-647">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="51e63-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="51e63-648">再单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="51e63-648">Then click **Next**.</span></span>

    <span data-ttu-id="51e63-649">![指向 SQL 数据库的连接字符串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="51e63-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="51e63-650">*指向 SQL 数据库的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="51e63-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="51e63-651">在 "**预览**" 页上，单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="51e63-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="51e63-652">![发布 web 应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="51e63-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="51e63-653">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="51e63-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="51e63-654">发布过程完成后，您的默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="51e63-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="51e63-655">![发布到 Windows Azure 的应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "发布到 Windows Azure 的应用程序")</span><span class="sxs-lookup"><span data-stu-id="51e63-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="51e63-656">*发布到 Windows Azure 的应用程序*</span><span class="sxs-lookup"><span data-stu-id="51e63-656">*Application published to Windows Azure*</span></span>
