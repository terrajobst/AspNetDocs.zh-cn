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
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="21102-104">在 ASP.NET Web 窗体中使用适用于 Visual Studio 2012 的 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="21102-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="21102-105">通过 Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="21102-105">by Tim Ammann</span></span>

> <span data-ttu-id="21102-106">Visual Studio 2012 Page Inspector 是使用集成浏览器的 web 开发工具。</span><span class="sxs-lookup"><span data-stu-id="21102-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="21102-107">在集成浏览器中选择任意元素，Page Inspector 会立即突出显示该元素的源和 CSS。</span><span class="sxs-lookup"><span data-stu-id="21102-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="21102-108">可以在应用程序中浏览任意页面，快速找到所呈现标记的源，并直接在 Visual Studio 环境中使用浏览器工具。</span><span class="sxs-lookup"><span data-stu-id="21102-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="21102-109">本教程演示如何启用检查模式，然后在你的 web 项目中快速查找和编辑 CSS 规则和文本。</span><span class="sxs-lookup"><span data-stu-id="21102-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="21102-110">本教程使用 Web 窗体应用程序项目，但也可以将 Page Inspector 用于网站项目和[MVC](https://go.microsoft.com/?linkid=9802002)应用程序。</span><span class="sxs-lookup"><span data-stu-id="21102-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="21102-111">本教程包含以下部分：</span><span class="sxs-lookup"><span data-stu-id="21102-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="21102-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="21102-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="21102-113">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="21102-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="21102-114">使用 Page Inspector 查看应用程序</span><span class="sxs-lookup"><span data-stu-id="21102-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="21102-115">启用检查模式</span><span class="sxs-lookup"><span data-stu-id="21102-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="21102-116">使用 Page Inspector 对标记进行更改</span><span class="sxs-lookup"><span data-stu-id="21102-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="21102-117">检查模式和 HTML 窗口</span><span class="sxs-lookup"><span data-stu-id="21102-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="21102-118">在 "样式" 窗口中预览 CSS 更改</span><span class="sxs-lookup"><span data-stu-id="21102-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="21102-119">CSS 自动同步</span><span class="sxs-lookup"><span data-stu-id="21102-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="21102-120">使用 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="21102-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="21102-121">系统必备</span><span class="sxs-lookup"><span data-stu-id="21102-121">Prerequisites</span></span>

- <span data-ttu-id="21102-122">[用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="21102-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="21102-123">若要获取最新版本的 Page Inspector，请使用[Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)安装用于 .net 2.0 的 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="21102-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="21102-124">Page Inspector 与 Microsoft Web 开发人员工具捆绑在一起。</span><span class="sxs-lookup"><span data-stu-id="21102-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="21102-125">最新版本为1.3。</span><span class="sxs-lookup"><span data-stu-id="21102-125">The latest version is 1.3.</span></span> <span data-ttu-id="21102-126">若要检查你的版本，请运行 Visual Studio，然后从 "**帮助**" 菜单中选择 "**关于 Microsoft Visual Studio** 。</span><span class="sxs-lookup"><span data-stu-id="21102-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="21102-127">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="21102-127">Create a Web Application</span></span>

<span data-ttu-id="21102-128">首先，将创建一个 web 应用程序，该应用程序将与 Page Inspector 使用。</span><span class="sxs-lookup"><span data-stu-id="21102-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="21102-129">在 Visual Studio 中，选择 "**文件**" &gt; "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="21102-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="21102-130">在左侧，展开 "**视觉C#对象**"，选择 " **web**"，然后选择 " **ASP.NET web 窗体应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="21102-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![新的 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="21102-132">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="21102-132">Click **OK**.</span></span>

<span data-ttu-id="21102-133">应用程序将在 "**源**" 视图中打开。</span><span class="sxs-lookup"><span data-stu-id="21102-133">The application opens in **Source** view.</span></span>

![源视图中的新 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="21102-135">现在，你已经有了要使用的应用程序，可以使用 Page Inspector 来检查和修改它。</span><span class="sxs-lookup"><span data-stu-id="21102-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="21102-136">使用 Page Inspector 查看应用程序</span><span class="sxs-lookup"><span data-stu-id="21102-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="21102-137">接下来，你将查看 Page Inspector 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="21102-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="21102-138">在**解决方案资源管理器**中，右键单击项目，然后选择 "**在 Page Inspector 中查看**"。</span><span class="sxs-lookup"><span data-stu-id="21102-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![在页面检查器中查看](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="21102-140">默认情况下，当 Page Inspector 首次启动时，它将作为 Visual Studio 环境左侧的窄窗口停靠。</span><span class="sxs-lookup"><span data-stu-id="21102-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="21102-141">将其停靠在左侧，并将其设置为适合你的宽度，或将其停靠在顶部、底部或右侧的一个工具区域中：</span><span class="sxs-lookup"><span data-stu-id="21102-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![Page Inspector 停靠位置](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="21102-143">如果取消停靠 "Page Inspector" 窗口，则可以将其放置在 Visual Studio 之外，甚至是在另一个监视器上（如果有）。</span><span class="sxs-lookup"><span data-stu-id="21102-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="21102-144">但是，若要在取消停靠 Page Inspector 窗口时，在 Page Inspector 和 Visual Studio 之间的 ALT + TAB，请参阅 "**工具**" &gt;**选项**"&gt;**环境**&gt;**选项卡和窗口**"，然后在 **"选项卡**" 下，清除 "**浮动工具窗口始终停留在主窗口顶部**：</span><span class="sxs-lookup"><span data-stu-id="21102-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![清除 "浮动工具窗口" 复选框，并在 Visual Studio 和取消停靠的 Page Inspector 窗口之间的 ALT + TAB](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="21102-146">"Page Inspector" 窗口的顶部窗格显示浏览器窗口中的当前页。</span><span class="sxs-lookup"><span data-stu-id="21102-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="21102-147">底部窗格显示左侧 HTML 标记中的页面，并在右侧显示可用于检查页面的不同方面的选项卡。</span><span class="sxs-lookup"><span data-stu-id="21102-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="21102-148">底部窗格类似于 Internet Explorer 中的[F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)。</span><span class="sxs-lookup"><span data-stu-id="21102-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="21102-149">（但是，与开发人员工具不同，你可以在 Visual Studio 中使用 Page Inspector。）</span><span class="sxs-lookup"><span data-stu-id="21102-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="21102-151">在本教程中，你将使用 "Page Inspector 浏览器" 窗格和 " **HTML** " 和 "**样式**" 选项卡，以帮助你快速导航并更改应用程序。</span><span class="sxs-lookup"><span data-stu-id="21102-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="21102-152">启用检查模式</span><span class="sxs-lookup"><span data-stu-id="21102-152">Enable Inspection Mode</span></span>

<span data-ttu-id="21102-153">接下来，您将了解 Page Inspector 的检查模式的工作方式。</span><span class="sxs-lookup"><span data-stu-id="21102-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="21102-154">在 "Page Inspector" 窗口中，单击 "**检查**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="21102-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="21102-156">若要查看操作中的检查模式，请将鼠标移动到 Page Inspector 浏览器窗口内页面的不同部分。</span><span class="sxs-lookup"><span data-stu-id="21102-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="21102-157">正如你所做的那样，鼠标指针将更改为大加号，并突出显示下面的元素：</span><span class="sxs-lookup"><span data-stu-id="21102-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![悬停在 div 上。内容包装](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="21102-159">移动鼠标指针时，请注意</span><span class="sxs-lookup"><span data-stu-id="21102-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="21102-160">**源**视图中的内容将发生变化，以显示与页面上所选元素对应的标记。</span><span class="sxs-lookup"><span data-stu-id="21102-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="21102-161">将突出显示相关标记。</span><span class="sxs-lookup"><span data-stu-id="21102-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="21102-162">如果源位于另一个文件中，则会在 "源" 视图中打开该文件，并突出显示相关标记。</span><span class="sxs-lookup"><span data-stu-id="21102-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="21102-163">Page Inspector 中的 " **HTML** " 选项卡中显示的标记也将更改为与页面上所选的元素相对应。</span><span class="sxs-lookup"><span data-stu-id="21102-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="21102-164">在 " **HTML** " 选项卡中，概述了相关标记。</span><span class="sxs-lookup"><span data-stu-id="21102-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="21102-165">"**样式**" 选项卡显示与当前所选内容相关的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="21102-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="21102-166">使用 Page Inspector 对标记进行更改</span><span class="sxs-lookup"><span data-stu-id="21102-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="21102-167">现在，你将了解如何使用 Page Inspector 来查找和更改位置可能不会立即显而易见的标记或文本。</span><span class="sxs-lookup"><span data-stu-id="21102-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="21102-168">将 Page Inspector 放检查模式，然后滚动到主页的底部。</span><span class="sxs-lookup"><span data-stu-id="21102-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="21102-169">一旦输入页脚区，Page Inspector 将在 "源" 视图中的 "其他" 选项卡的右侧临时选项卡上打开 "**源**" 视图中的 "*站点*" 布局文件，并突出显示所选母版页的部分。</span><span class="sxs-lookup"><span data-stu-id="21102-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="21102-170">这会显示 Page Inspector 如何查找并显示页面上的内容，这些内容可能来自于最初打开的文件之外的其他文件。</span><span class="sxs-lookup"><span data-stu-id="21102-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![页脚突出显示检查模式](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="21102-172">在 "Page Inspector 浏览器" 窗口中，将鼠标指针移动到带有版权声明<a id="a"></a>的行上。</span><span class="sxs-lookup"><span data-stu-id="21102-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="21102-173">在*站点母版页*中，将突出显示相应的行。</span><span class="sxs-lookup"><span data-stu-id="21102-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![突出显示了页脚版权行](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="21102-175">将一些文本添加到*站点 .master*文件中行的末尾。</span><span class="sxs-lookup"><span data-stu-id="21102-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="21102-176">&amp;copy &lt;p&gt;&lt;%： DateTime . Year%&gt;-My ASP.NET Application Rocks！&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="21102-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="21102-177">现在，按 Ctrl + Alt + Enter，或单击 "更新" 栏以在 "Page Inspector 浏览器" 窗口中查看结果。</span><span class="sxs-lookup"><span data-stu-id="21102-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![我的 ASP.NET 应用程序 Rocks！](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="21102-179">您可能认为页脚位于*default.aspx*页面上，但它已在主布局页面中，并 Page Inspector 找到它。</span><span class="sxs-lookup"><span data-stu-id="21102-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="21102-180">检查模式和 HTML 窗口</span><span class="sxs-lookup"><span data-stu-id="21102-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="21102-181">接下来，您将快速了解 HTML 窗口以及它如何为您映射元素。</span><span class="sxs-lookup"><span data-stu-id="21102-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="21102-182">将 Page Inspector 放置在检查模式中。</span><span class="sxs-lookup"><span data-stu-id="21102-182">Put Page Inspector in Inspection Mode.</span></span>

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="21102-184">单击 "此处显示徽标" 页面的顶部部分。</span><span class="sxs-lookup"><span data-stu-id="21102-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="21102-185">您将更详细地检查特定元素，因此，在浏览器窗口中显示的内容将不再随着鼠标指针的移动而改变。</span><span class="sxs-lookup"><span data-stu-id="21102-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="21102-186">现在，将鼠标指针移动到**HTML**窗口。</span><span class="sxs-lookup"><span data-stu-id="21102-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="21102-187">移动鼠标指针时，Page Inspector 在**HTML**窗口中勾勒元素，并在浏览器窗口中突出显示相应的元素。</span><span class="sxs-lookup"><span data-stu-id="21102-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 窗口](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="21102-189">与之前一样，Page Inspector 会在临时选项卡中打开*网站 .master*文件。单击 "主节点" 选项卡，并在 &lt;标头&gt; "部分突出显示相应的标记：</span><span class="sxs-lookup"><span data-stu-id="21102-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![突出显示标记](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="21102-191">在 "样式" 窗口中预览 CSS 更改</span><span class="sxs-lookup"><span data-stu-id="21102-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="21102-192">接下来，您将了解如何使用 Page Inspector**样式**"窗口来预览 CSS 的更改。</span><span class="sxs-lookup"><span data-stu-id="21102-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="21102-193">单击 "**检查**" 按钮以将 Page Inspector 放置在检查模式中。</span><span class="sxs-lookup"><span data-stu-id="21102-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="21102-194">在 "Page Inspector 浏览器" 窗口中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装**器" 标签。</span><span class="sxs-lookup"><span data-stu-id="21102-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![悬停在元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="21102-196">在 div. 内容包装部分中单击一次，然后将鼠标指针移动到 "**样式**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="21102-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="21102-197">在 "属性-包装类选择器" 下，清除并选中 "背景色" 属性的复选框。</span><span class="sxs-lookup"><span data-stu-id="21102-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![清除背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="21102-199">请注意如何在 Page Inspector 浏览器窗口中立即更改预览。</span><span class="sxs-lookup"><span data-stu-id="21102-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="21102-200">再次选中此复选框，然后双击属性值并将其更改为 `red`。</span><span class="sxs-lookup"><span data-stu-id="21102-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="21102-201">更改将立即显示：</span><span class="sxs-lookup"><span data-stu-id="21102-201">The change shows immediately:</span></span>

![红色背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="21102-203">在将更改提交到样式表本身之前，"**样式**" 窗口可让你轻松地测试和预览 CSS 更改。</span><span class="sxs-lookup"><span data-stu-id="21102-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="21102-204">CSS 自动同步</span><span class="sxs-lookup"><span data-stu-id="21102-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="21102-205">此功能需要 Page Inspector 1.3 版。</span><span class="sxs-lookup"><span data-stu-id="21102-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="21102-206">使用 CSS 自动同步功能，可以直接编辑 CSS 文件，并立即在 Page Inspector 浏览器中查看更改。</span><span class="sxs-lookup"><span data-stu-id="21102-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="21102-207">单击 "**检查**" 以将 Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="21102-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="21102-208">在 "Page Inspector 浏览器" 中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装**器" 标签。</span><span class="sxs-lookup"><span data-stu-id="21102-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="21102-209">单击 "一次" 以选择此元素。</span><span class="sxs-lookup"><span data-stu-id="21102-209">Click once to select this element.</span></span>

<span data-ttu-id="21102-210">"**样式**" 窗口显示此元素的所有 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="21102-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="21102-211">向下滚动以查找 ""。</span><span class="sxs-lookup"><span data-stu-id="21102-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="21102-212">单击 "."。</span><span class="sxs-lookup"><span data-stu-id="21102-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="21102-213">Page Inspector 打开定义此样式（web.config）的 CSS 文件，并突出显示相应的 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="21102-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS 文件](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="21102-215">现在，将 `background-color` 的值更改为 "red"。</span><span class="sxs-lookup"><span data-stu-id="21102-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="21102-216">更改会立即显示在 Page Inspector 浏览器中。</span><span class="sxs-lookup"><span data-stu-id="21102-216">The change appears immediately in the Page Inspector browser.</span></span>

![Page Inspector 浏览器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="21102-218">使用 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="21102-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="21102-219">接下来，您将学习如何使用 Page Inspector 在默认应用程序中快速查找和更改已突出显示文本的 CSS。</span><span class="sxs-lookup"><span data-stu-id="21102-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="21102-220">在此示例中，你决定不喜欢蓝色突出显示，并且想要将其更改为另一种颜色。</span><span class="sxs-lookup"><span data-stu-id="21102-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="21102-221">单击 "**检查**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="21102-221">Click the **Inspect** button.</span></span>

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="21102-223">在 "Page Inspector 浏览器" 窗口中，将鼠标指针移到突出显示的 "视频、教程和示例" 文本上，以便显示 CSS "标记" 标签。</span><span class="sxs-lookup"><span data-stu-id="21102-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![悬停在 mark 元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="21102-225">单击该文本将其选中。</span><span class="sxs-lookup"><span data-stu-id="21102-225">Click the text to select it.</span></span> <span data-ttu-id="21102-226">对应的 CSS 标记选择器显示在 "**样式**" 窗口的底部。</span><span class="sxs-lookup"><span data-stu-id="21102-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![在 "样式" 窗口中标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="21102-228">单击标记选择器。</span><span class="sxs-lookup"><span data-stu-id="21102-228">Click the mark selector.</span></span> <span data-ttu-id="21102-229">这将打开 web 应用程序的*web.config 文件。*</span><span class="sxs-lookup"><span data-stu-id="21102-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="21102-230">单击 "站点" "css" 选项卡，将突出显示选择器对应的 CSS：</span><span class="sxs-lookup"><span data-stu-id="21102-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![在样式表中标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="21102-232">选择并删除具有背景色属性的行。</span><span class="sxs-lookup"><span data-stu-id="21102-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="21102-233">现在，你将使用新的 Visual Studio 2012 CSS 颜色选取器为 "**标记**背景-颜色" 属性选择新颜色。</span><span class="sxs-lookup"><span data-stu-id="21102-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="21102-234">使用 Visual Studio 2012 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="21102-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="21102-235">Visual Studio 2012 中的 CSS 编辑器提供了一个颜色选取器，使您可以轻松地选择和插入颜色。</span><span class="sxs-lookup"><span data-stu-id="21102-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="21102-236">它有一个简单的颜色栏和一个提供更精细控制的 "弹出项" 选取器。</span><span class="sxs-lookup"><span data-stu-id="21102-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="21102-237">颜色选取器包含一种标准颜色调色板，支持标准颜色名称、哈希代码、RGB、RGBA、HSL 和 HSLA 颜色，并维护最近在文档中使用的颜色的列表。</span><span class="sxs-lookup"><span data-stu-id="21102-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="21102-238">在背景色属性所在的行上，键入 "bc"，然后按向下键一次。</span><span class="sxs-lookup"><span data-stu-id="21102-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="21102-239">当你在连字符分隔属性（如 "背景色"）中键入每个单词的第一个字符时，IntelliSense 将筛选该列表以仅显示匹配的属性：</span><span class="sxs-lookup"><span data-stu-id="21102-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Intellisense 筛选值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="21102-241">现在，键入一个冒号。</span><span class="sxs-lookup"><span data-stu-id="21102-241">Now type a colon.</span></span> <span data-ttu-id="21102-242">执行此操作时，将插入完整的背景色属性名称。</span><span class="sxs-lookup"><span data-stu-id="21102-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="21102-243">键入 **#** 或**rgb （** ，并显示颜色选取器栏：</span><span class="sxs-lookup"><span data-stu-id="21102-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS 颜色选取器栏](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="21102-245">若要查看颜色选取器栏的工作方式，请使用鼠标指针单击其颜色，或按向下箭头键，然后使用向左箭头和向右箭头键来遍历颜色。</span><span class="sxs-lookup"><span data-stu-id="21102-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="21102-246">访问颜色时，会预览背景色属性的相应值：</span><span class="sxs-lookup"><span data-stu-id="21102-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![已预览背景色属性值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="21102-248">此时，可以按 Enter 选择值，然后选择分号（;)完成 CSS 条目。</span><span class="sxs-lookup"><span data-stu-id="21102-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="21102-249">现在，请继续查看下一部分，以便可以看到颜色选取器弹出窗口的工作方式。</span><span class="sxs-lookup"><span data-stu-id="21102-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="21102-250">使用 "颜色选取器" 弹出窗口</span><span class="sxs-lookup"><span data-stu-id="21102-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="21102-251">如果颜色条没有您所需的确切颜色，可以使用 "颜色选取器" 弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="21102-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="21102-252">若要打开它，请单击颜色栏右端的双 v 形 v 形，或在键盘上按向下键一次或两次。</span><span class="sxs-lookup"><span data-stu-id="21102-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 颜色选取器弹出窗口](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="21102-254">单击右侧垂直条中的颜色。</span><span class="sxs-lookup"><span data-stu-id="21102-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="21102-255">这会在主窗口中显示该颜色的渐变。</span><span class="sxs-lookup"><span data-stu-id="21102-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="21102-256">按 Enter 键直接从竖线中选择一种颜色，或单击主窗口中的任何点以选择更高的精度。</span><span class="sxs-lookup"><span data-stu-id="21102-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="21102-257">如果您要使用的计算机屏幕上有一种颜色（它不必在 Visual Studio 用户界面内），则可以使用右下方的吸管工具捕获其值。</span><span class="sxs-lookup"><span data-stu-id="21102-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="21102-258">还可以通过移动颜色选取器底部的滑块来更改颜色的不透明度。</span><span class="sxs-lookup"><span data-stu-id="21102-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="21102-259">这样做会将颜色值更改为 RGBA 值，因为 RGBA 格式可以表示不透明度。</span><span class="sxs-lookup"><span data-stu-id="21102-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="21102-260">选择一种颜色后，按 Enter，然后键入一个分号来完成*站点导航*文件中的背景色项。</span><span class="sxs-lookup"><span data-stu-id="21102-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="21102-261">Page Inspector 更新栏</span><span class="sxs-lookup"><span data-stu-id="21102-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="21102-262">Page Inspector 立即检测对*站点 .css*文件（或应用程序中的任何文件）所做的更改，并在更新栏中显示警报。</span><span class="sxs-lookup"><span data-stu-id="21102-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![更新栏](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="21102-264">若要保存所有文件并刷新 Page Inspector 浏览器，请按 Ctrl + Alt + Enter，或单击更新栏。</span><span class="sxs-lookup"><span data-stu-id="21102-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="21102-265">突出显示颜色的更改将显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="21102-265">The change in the highlight color appears in the browser:</span></span>

![突出显示颜色已更改](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="21102-267">请注意，你可以直接从 Visual Studio 环境中刷新 Page Inspector 浏览器。</span><span class="sxs-lookup"><span data-stu-id="21102-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="21102-268">使用 Page Inspector 而不是外部浏览器，可以在开发 web 应用程序时保持在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="21102-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="21102-269">另请参阅</span><span class="sxs-lookup"><span data-stu-id="21102-269">See Also</span></span>

<span data-ttu-id="21102-270">[简介 Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) （第9频道视频）</span><span class="sxs-lookup"><span data-stu-id="21102-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="21102-271">[Page Inspector 错误消息](https://go.microsoft.com/?linkid=9813062)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="21102-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
