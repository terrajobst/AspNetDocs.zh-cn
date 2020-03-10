---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 使用 Visual Studio 2013 创建基本 ASP.NET 4.5 Web 窗体页
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511076"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a><span data-ttu-id="05c24-102">使用 Visual Studio 2013 创建基本 ASP.NET 4.5 Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="05c24-102">Using Visual Studio 2013 to create a Basic ASP.NET 4.5 Web Forms Page</span></span>

<span data-ttu-id="05c24-103">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="05c24-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

[!INCLUDE[](~/includes/rp.md)]

<span data-ttu-id="05c24-104">本演练介绍了[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)和[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)中的 web 开发环境。</span><span class="sxs-lookup"><span data-stu-id="05c24-104">This walkthrough provides you with an introduction to the Web development environment in [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) and in [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="05c24-105">本演练将指导您创建一个简单的 ASP.NET Web 窗体页，并说明创建新页、添加控件和编写代码的基本方法。</span><span class="sxs-lookup"><span data-stu-id="05c24-105">This walkthrough guides you through creating a simple ASP.NET Web Forms page and illustrates the basic techniques of creating a new page, adding controls, and writing code.</span></span>

<span data-ttu-id="05c24-106">本演练涉及以下任务：</span><span class="sxs-lookup"><span data-stu-id="05c24-106">Tasks illustrated in this walkthrough include:</span></span>

- <span data-ttu-id="05c24-107">创建文件系统 Web 窗体应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="05c24-107">Creating a file system Web Forms application project.</span></span>
- <span data-ttu-id="05c24-108">通过 Visual Studio 熟悉自己的体验。</span><span class="sxs-lookup"><span data-stu-id="05c24-108">Familiarizing yourself with Visual Studio.</span></span>
- <span data-ttu-id="05c24-109">创建 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="05c24-109">Creating an ASP.NET page.</span></span>
- <span data-ttu-id="05c24-110">添加控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-110">Adding controls.</span></span>
- <span data-ttu-id="05c24-111">添加事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="05c24-111">Adding event handlers.</span></span>
- <span data-ttu-id="05c24-112">运行和测试 Visual Studio 中的页面。</span><span class="sxs-lookup"><span data-stu-id="05c24-112">Running and testing a page from Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05c24-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="05c24-113">Prerequisites</span></span>

<span data-ttu-id="05c24-114">若要完成本演练，你将需要：</span><span class="sxs-lookup"><span data-stu-id="05c24-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="05c24-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="05c24-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="05c24-116">将自动安装 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="05c24-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="05c24-117">在本系列教程中，Web 的 Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 通常称为 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="05c24-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="05c24-118">如果你使用的是 Visual Studio，则本演练假定你在首次启动 Visual Studio 时选择了 " **Web 开发**" 设置集合。</span><span class="sxs-lookup"><span data-stu-id="05c24-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="05c24-119">有关详细信息，请参阅[如何：选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05c24-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="05c24-120">创建 Web 应用程序项目和页面</span><span class="sxs-lookup"><span data-stu-id="05c24-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="05c24-121">在本演练的此部分中，你将创建一个 Web 应用程序项目并向其添加新页。</span><span class="sxs-lookup"><span data-stu-id="05c24-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span> <span data-ttu-id="05c24-122">你还将在浏览器中添加 HTML 文本并运行该页面。</span><span class="sxs-lookup"><span data-stu-id="05c24-122">You will also add HTML text and run the page in your browser.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="05c24-123">创建 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="05c24-123">To create a Web application project</span></span>

1. <span data-ttu-id="05c24-124">打开 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="05c24-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="05c24-125">在“文件”菜单上，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="05c24-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="05c24-126">![文件 "菜单](creating-a-basic-web-forms-page/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="05c24-126">![File Menu](creating-a-basic-web-forms-page/_static/image1.png)</span></span>

    <span data-ttu-id="05c24-127">此时将出现“新建项目”对话框。</span><span class="sxs-lookup"><span data-stu-id="05c24-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="05c24-128">选择左侧的 "**模板**" -&gt; **Visual C#**  -&gt; **Web**模板 "组。</span><span class="sxs-lookup"><span data-stu-id="05c24-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="05c24-129">在中心列中选择 " **ASP.NET Web 应用程序**" 模板。</span><span class="sxs-lookup"><span data-stu-id="05c24-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="05c24-130">将项目命名为 " ***BasicWebApp*** "，然后单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="05c24-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="05c24-131">![“新建项目”对话框](creating-a-basic-web-forms-page/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="05c24-131">![New Project dialog box](creating-a-basic-web-forms-page/_static/image2.png)</span></span>
6. <span data-ttu-id="05c24-132">接下来，选择 " **Web 窗体**" 模板，然后单击 "**确定"** 按钮创建项目。</span><span class="sxs-lookup"><span data-stu-id="05c24-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="05c24-133">![新的 ASP.NET 项目 "对话框](creating-a-basic-web-forms-page/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="05c24-133">![New ASP.NET Project dialog box](creating-a-basic-web-forms-page/_static/image3.png)</span></span>  

    <span data-ttu-id="05c24-134">Visual Studio 会创建一个新项目，其中包含基于 Web 窗体模板的预生成功能。</span><span class="sxs-lookup"><span data-stu-id="05c24-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span> <span data-ttu-id="05c24-135">它不但提供了一个*主页 .aspx*页面（一个*关于 .aspx*页面），还*提供了成员*资格功能，可注册用户并保存其凭据，使用户能够登录到你的网站。</span><span class="sxs-lookup"><span data-stu-id="05c24-135">It not only provides you with a *Home.aspx* page, an *About.aspx* page, a *Contact.aspx* page, but also includes membership functionality that registers users and saves their credentials so that they can log in to your website.</span></span> <span data-ttu-id="05c24-136">创建新页面时，默认情况下，Visual Studio 会在 "**源**" 视图中显示该页面，您可以在其中查看该页面的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-136">When a new page is created, by default Visual Studio displays the page in **Source** view, where you can see the page's HTML elements.</span></span> <span data-ttu-id="05c24-137">下图显示了在创建名为*BasicWebApp*的新网页的情况下，你将在 "**源**" 视图中看到的内容。</span><span class="sxs-lookup"><span data-stu-id="05c24-137">The following illustration shows what you would see in **Source** view if you created a new Web page named *BasicWebApp.aspx*.</span></span>  
    <span data-ttu-id="05c24-138">![源视图](creating-a-basic-web-forms-page/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="05c24-138">![Source View](creating-a-basic-web-forms-page/_static/image4.png)</span></span>

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a><span data-ttu-id="05c24-139">Visual Studio Web 开发环境教程</span><span class="sxs-lookup"><span data-stu-id="05c24-139">A Tour of the Visual Studio Web Development Environment</span></span>

<span data-ttu-id="05c24-140">在继续修改页面之前，请先熟悉 Visual Studio 开发环境，这一点非常有用。</span><span class="sxs-lookup"><span data-stu-id="05c24-140">Before you proceed by modifying the page, it is useful to familiarize yourself with the Visual Studio development environment.</span></span> <span data-ttu-id="05c24-141">下图显示了 Visual Studio 中可用的 windows 和工具以及 Web Visual Studio Express。</span><span class="sxs-lookup"><span data-stu-id="05c24-141">The following illustration shows you the windows and tools that are available in Visual Studio and Visual Studio Express for Web.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="05c24-142">此关系图显示默认窗口和窗口位置。</span><span class="sxs-lookup"><span data-stu-id="05c24-142">This diagram shows default windows and window locations.</span></span> <span data-ttu-id="05c24-143">"**视图**" 菜单允许您显示其他窗口，并重新排列窗口并调整其大小以适合您的喜好。</span><span class="sxs-lookup"><span data-stu-id="05c24-143">The **View** menu allows you to display additional windows, and to rearrange and resize windows to suit your preferences.</span></span> <span data-ttu-id="05c24-144">如果已对窗口排列进行了更改，则所显示的内容将与图中的内容不匹配。</span><span class="sxs-lookup"><span data-stu-id="05c24-144">If changes have already been made to the window arrangement, what you see will not match the illustration.</span></span>

 <span data-ttu-id="05c24-145">Visual Studio 环境</span><span class="sxs-lookup"><span data-stu-id="05c24-145">The Visual Studio environment</span></span>

![Visual Studio 环境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a><span data-ttu-id="05c24-147">熟悉 Web 设计器</span><span class="sxs-lookup"><span data-stu-id="05c24-147">Familiarize yourself with the Web designer</span></span>

<span data-ttu-id="05c24-148">检查上图并将文本与以下列表匹配，其中介绍了最常用的窗口和工具。</span><span class="sxs-lookup"><span data-stu-id="05c24-148">Examine the above illustration and match the text to the following list, which describes the most commonly used windows and tools.</span></span> <span data-ttu-id="05c24-149">（并非所有你所看到的窗口和工具都列在此处，只列出了上图中标记的那些窗口和工具。）</span><span class="sxs-lookup"><span data-stu-id="05c24-149">(Not all windows and tools that you see are listed here, only those marked in the preceding illustration.)</span></span>

- <span data-ttu-id="05c24-150">'.</span><span class="sxs-lookup"><span data-stu-id="05c24-150">Toolbars.</span></span> <span data-ttu-id="05c24-151">提供用于设置文本格式、查找文本等的命令。</span><span class="sxs-lookup"><span data-stu-id="05c24-151">Provide commands for formatting text, finding text, and so on.</span></span> <span data-ttu-id="05c24-152">某些工具栏仅在 "**设计**" 视图中工作时可用。</span><span class="sxs-lookup"><span data-stu-id="05c24-152">Some toolbars are available only when you are working in **Design** view.</span></span>
- <span data-ttu-id="05c24-153">**解决方案资源管理器**"窗口。</span><span class="sxs-lookup"><span data-stu-id="05c24-153">**Solution Explorer** window.</span></span> <span data-ttu-id="05c24-154">显示您的 Web 应用程序中的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="05c24-154">Displays the files and folders in your Web application.</span></span>
- <span data-ttu-id="05c24-155">文档窗口。</span><span class="sxs-lookup"><span data-stu-id="05c24-155">Document window.</span></span> <span data-ttu-id="05c24-156">在选项卡式窗口中显示正在处理的文档。</span><span class="sxs-lookup"><span data-stu-id="05c24-156">Displays the documents you are working on in tabbed windows.</span></span> <span data-ttu-id="05c24-157">可以通过单击 "选项卡" 在文档之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="05c24-157">You can switch between documents by clicking tabs.</span></span>
- <span data-ttu-id="05c24-158">**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="05c24-158">**Properties** window.</span></span> <span data-ttu-id="05c24-159">允许您更改页面、HTML 元素、控件和其他对象的设置。</span><span class="sxs-lookup"><span data-stu-id="05c24-159">Allows you to change settings for the page, HTML elements, controls, and other objects.</span></span>
- <span data-ttu-id="05c24-160">视图选项卡。</span><span class="sxs-lookup"><span data-stu-id="05c24-160">View tabs.</span></span> <span data-ttu-id="05c24-161">提供同一文档的不同视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-161">Present you with different views of the same document.</span></span> <span data-ttu-id="05c24-162">**设计**视图是接近 WYSIWYG 的编辑图面。</span><span class="sxs-lookup"><span data-stu-id="05c24-162">**Design** view is a near-WYSIWYG editing surface.</span></span> <span data-ttu-id="05c24-163">**源**视图是页面的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="05c24-163">**Source** view is the HTML editor for the page.</span></span> <span data-ttu-id="05c24-164">**拆分**视图显示文档的**设计**视图和**源**视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-164">**Split** view displays both the **Design** view and the **Source** view for the document.</span></span> <span data-ttu-id="05c24-165">稍后将在本演练中使用 "**设计**" 和 "**源**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-165">You will work with the **Design** and **Source** views later in this walkthrough.</span></span> <span data-ttu-id="05c24-166">如果希望在 "**设计**" 视图中打开网页，请在 "**工具**" 菜单上单击 "**选项**"，选择 " **HTML 设计器**" 节点，然后更改中的 "**起始页**" 选项。</span><span class="sxs-lookup"><span data-stu-id="05c24-166">If you prefer to open Web pages in **Design** view, on the **Tools** menu, click **Options**, select the **HTML Designer** node, and change the **Start Pages In** option.</span></span>
- <span data-ttu-id="05c24-167">**工具箱**。</span><span class="sxs-lookup"><span data-stu-id="05c24-167">**ToolBox**.</span></span> <span data-ttu-id="05c24-168">提供可拖到页面上的控件和 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-168">Provides controls and HTML elements that you can drag onto your page.</span></span> <span data-ttu-id="05c24-169">**工具箱**元素按 common 函数分组。</span><span class="sxs-lookup"><span data-stu-id="05c24-169">**Toolbox** elements are grouped by common function.</span></span>
- <span data-ttu-id="05c24-170">S **E) 资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="05c24-170">S **erver Explorer**.</span></span> <span data-ttu-id="05c24-171">显示数据库连接。</span><span class="sxs-lookup"><span data-stu-id="05c24-171">Displays database connections.</span></span> <span data-ttu-id="05c24-172">如果服务器资源管理器不可见，请在 "视图" 菜单上单击 "服务器资源管理器"。</span><span class="sxs-lookup"><span data-stu-id="05c24-172">If Server Explorer is not visible, on the View menu, click Server Explorer.</span></span>

### <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="05c24-173">创建新的 ASP.NET Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="05c24-173">Creating a new ASP.NET Web Forms Page</span></span>

<span data-ttu-id="05c24-174">使用 " **ASP.NET Web 应用程序**" 项目模板创建新的 Web 窗体应用程序时，Visual Studio 会添加一个名为 " *default.aspx*" 的 ASP.NET 页面（Web 窗体页）以及多个其他文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="05c24-174">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="05c24-175">你可以使用*default.aspx*页作为你的 Web 应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="05c24-175">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="05c24-176">但是，对于本演练，您将创建并使用一个新页。</span><span class="sxs-lookup"><span data-stu-id="05c24-176">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="05c24-177">向 Web 应用程序添加页</span><span class="sxs-lookup"><span data-stu-id="05c24-177">To add a page to the Web application</span></span>

1. <span data-ttu-id="05c24-178">关闭 " *default.aspx* " 页。</span><span class="sxs-lookup"><span data-stu-id="05c24-178">Close the *Default.aspx* page.</span></span> <span data-ttu-id="05c24-179">为此，请单击显示文件名的选项卡，然后单击 "关闭" 选项。</span><span class="sxs-lookup"><span data-stu-id="05c24-179">To do this, click the tab that displays the file name and then click the close option.</span></span>
2. <span data-ttu-id="05c24-180">在**解决方案资源管理器**中，右键单击 Web 应用程序名称（在本教程中，应用程序名称为 " **BasicWebSite**"），然后单击 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="05c24-180">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="05c24-181">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="05c24-181">The **Add New Item** dialog box is displayed.</span></span>
3. <span data-ttu-id="05c24-182">选择左侧的 " **Visual C#**  -&gt; **Web**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="05c24-182">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="05c24-183">然后，从中间列表中选择 " **Web 窗体**" 并将其命名为 " *FirstWebPage*"。</span><span class="sxs-lookup"><span data-stu-id="05c24-183">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="05c24-184">![“添加新项”对话框](creating-a-basic-web-forms-page/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="05c24-184">![Add New Item dialog box](creating-a-basic-web-forms-page/_static/image6.png)</span></span>
4. <span data-ttu-id="05c24-185">单击 "**添加**" 以将网页添加到项目。</span><span class="sxs-lookup"><span data-stu-id="05c24-185">Click **Add** to add the web page to your project.</span></span>  
<span data-ttu-id="05c24-186">Visual Studio 将创建新页并将其打开。</span><span class="sxs-lookup"><span data-stu-id="05c24-186">Visual Studio creates the new page and opens it.</span></span>

### <a name="adding-html-to-the-page"></a><span data-ttu-id="05c24-187">将 HTML 添加到页面</span><span class="sxs-lookup"><span data-stu-id="05c24-187">Adding HTML to the Page</span></span>

<span data-ttu-id="05c24-188">在本演练的此部分中，将向页面添加一些静态文本。</span><span class="sxs-lookup"><span data-stu-id="05c24-188">In this part of the walkthrough, you will add some static text to the page.</span></span>

### <a name="to-add-text-to-the-page"></a><span data-ttu-id="05c24-189">向页面中添加文本</span><span class="sxs-lookup"><span data-stu-id="05c24-189">To add text to the page</span></span>

1. <span data-ttu-id="05c24-190">在文档窗口的底部，单击 "**设计**" 选项卡以切换到 "**设计**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-190">At the bottom of the document window, click the **Design** tab to switch to **Design** view.</span></span>

    <span data-ttu-id="05c24-191">设计视图以类似于所见即所得的方式显示当前页面。</span><span class="sxs-lookup"><span data-stu-id="05c24-191">Design view displays the current page in a WYSIWYG-like way.</span></span> <span data-ttu-id="05c24-192">此时，您不能在页面上包含任何文本或控件，因此，除了用一条轮廓矩形的虚线外，该页面仍为空白。</span><span class="sxs-lookup"><span data-stu-id="05c24-192">At this point, you do not have any text or controls on the page, so the page is blank except for a dashed line that outlines a rectangle.</span></span> <span data-ttu-id="05c24-193">此矩形表示页面上的**div**元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-193">This rectangle represents a **div** element on the page.</span></span>
2. <span data-ttu-id="05c24-194">在用虚线勾勒出的矩形内部单击。</span><span class="sxs-lookup"><span data-stu-id="05c24-194">Click inside the rectangle that is outlined by a dashed line.</span></span>
3. <span data-ttu-id="05c24-195">键入 "**欢迎使用 Visual Web Developer** "，然后按**enter**两次。</span><span class="sxs-lookup"><span data-stu-id="05c24-195">Type **Welcome to Visual Web Developer** and press **ENTER** twice.</span></span>

    <span data-ttu-id="05c24-196">下图显示了在 "**设计**" 视图中键入的文本。</span><span class="sxs-lookup"><span data-stu-id="05c24-196">The following illustration shows the text you typed in **Design** view.</span></span>

    <span data-ttu-id="05c24-197">![设计视图中的欢迎文本](creating-a-basic-web-forms-page/_static/image7.png "设计视图中的欢迎文本")</span><span class="sxs-lookup"><span data-stu-id="05c24-197">![Welcome text in Design view](creating-a-basic-web-forms-page/_static/image7.png "Welcome text in Design view")</span></span>
4. <span data-ttu-id="05c24-198">切换到 "**源**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-198">Switch to **Source** view.</span></span>

    <span data-ttu-id="05c24-199">您可以在 "**设计**" 视图中键入时在 "**源**" 视图中查看 HTML。</span><span class="sxs-lookup"><span data-stu-id="05c24-199">You can see the HTML in **Source** view that you created when you typed in **Design** view.</span></span>  
    <span data-ttu-id="05c24-200">![包含静态文本](creating-a-basic-web-forms-page/_static/image8.png) 的网页</span><span class="sxs-lookup"><span data-stu-id="05c24-200">![Web Page with Static Text](creating-a-basic-web-forms-page/_static/image8.png)</span></span>

### <a name="running-the-page"></a><span data-ttu-id="05c24-201">运行页面</span><span class="sxs-lookup"><span data-stu-id="05c24-201">Running the Page</span></span>

<span data-ttu-id="05c24-202">在继续操作之前，可以先将控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="05c24-202">Before you proceed by adding controls to the page, you can first run it.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="05c24-203">运行页面</span><span class="sxs-lookup"><span data-stu-id="05c24-203">To run the page</span></span>

1. <span data-ttu-id="05c24-204">在**解决方案资源管理器**中，右键单击*FirstWebPage* ，然后选择 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="05c24-204">In **Solution Explorer**, right-click *FirstWebPage.aspx* and select **Set as Start Page**.</span></span>
2. <span data-ttu-id="05c24-205">按**CTRL + F5**运行页面。</span><span class="sxs-lookup"><span data-stu-id="05c24-205">Press **CTRL+F5** to run the page.</span></span>

    <span data-ttu-id="05c24-206">页面将显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="05c24-206">The page is displayed in the browser.</span></span> <span data-ttu-id="05c24-207">尽管您创建的页的文件扩展名为 *.aspx*，但它当前与任何 HTML 页面一样运行。</span><span class="sxs-lookup"><span data-stu-id="05c24-207">Although the page you created has a file-name extension of *.aspx*, it currently runs like any HTML page.</span></span>

    <span data-ttu-id="05c24-208">若要在浏览器中显示页面，还可以在**解决方案资源管理器**中右键单击页面，然后选择 "**在浏览器中查看**"。</span><span class="sxs-lookup"><span data-stu-id="05c24-208">To display a page in the browser you can also right-click the page in **Solution Explorer** and select **View in Browser**.</span></span>
3. <span data-ttu-id="05c24-209">关闭浏览器以停止 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="05c24-209">Close the browser to stop the Web application.</span></span>

## <a name="adding-and-programming-controls"></a><span data-ttu-id="05c24-210">添加和编程控件</span><span class="sxs-lookup"><span data-stu-id="05c24-210">Adding and Programming Controls</span></span>

<a id="sectionToggle1"></a>

<span data-ttu-id="05c24-211">现在，你将向页面中添加服务器控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-211">You will now add server controls to the page.</span></span> <span data-ttu-id="05c24-212">服务器控件（例如按钮、标签、文本框和其他熟悉控件）为 Web 窗体页提供典型的窗体处理功能。</span><span class="sxs-lookup"><span data-stu-id="05c24-212">Server controls, such as buttons, labels, text boxes, and other familiar controls, provide typical form-processing capabilities for your Web Forms pages.</span></span> <span data-ttu-id="05c24-213">但是，您可以用服务器上运行的代码而不是客户端对控件进行编程。</span><span class="sxs-lookup"><span data-stu-id="05c24-213">However, you can program the controls with code that runs on the server, rather than the client.</span></span>

<span data-ttu-id="05c24-214">您将向页面添加一个[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件、一个[文本框](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件和一个 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件，并编写代码来处理[Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。</span><span class="sxs-lookup"><span data-stu-id="05c24-214">You will add a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control to the page and write code to handle the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

### <a name="to-add-controls-to-the-page"></a><span data-ttu-id="05c24-215">向页面添加控件</span><span class="sxs-lookup"><span data-stu-id="05c24-215">To add controls to the page</span></span>

1. <span data-ttu-id="05c24-216">单击 "**设计**" 选项卡以切换到 "**设计**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-216">Click the **Design** tab to switch to **Design** view.</span></span>
2. <span data-ttu-id="05c24-217">将插入点放在**欢迎使用 Visual Web Developer**文本的末尾，然后按**enter** 5 次或多次，以在**div**元素框中腾出一些空间。</span><span class="sxs-lookup"><span data-stu-id="05c24-217">Put the insertion point at the end of the **Welcome to Visual Web Developer** text and press **ENTER** five or more times to make some room in the **div** element box.</span></span>
3. <span data-ttu-id="05c24-218">在 "**工具箱**" 中，展开**标准**组（如果尚未展开）。</span><span class="sxs-lookup"><span data-stu-id="05c24-218">In the **Toolbox**, expand the **Standard** group if it is not already expanded.</span></span>  
<span data-ttu-id="05c24-219">请注意，您可能需要展开左侧的 **"工具箱**" 窗口以查看它。</span><span class="sxs-lookup"><span data-stu-id="05c24-219">Note that you may need to expand the **Toolbox** window on the left to view it.</span></span>
4. <span data-ttu-id="05c24-220">将[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件拖到页面上，并将其放置在**欢迎使用**第一行中的 " **div**元素" 框的中部。</span><span class="sxs-lookup"><span data-stu-id="05c24-220">Drag a [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control onto the page and drop it in the middle of the **div** element box that has **Welcome to Visual Web Developer** in the first line.</span></span>
5. <span data-ttu-id="05c24-221">将一个 "[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)" 控件拖到页面上，然后将其放置在[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件的右侧。</span><span class="sxs-lookup"><span data-stu-id="05c24-221">Drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page and drop it to the right of the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span>
6. <span data-ttu-id="05c24-222">将 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件拖动到页面上，将其放在[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件下的单独行中。</span><span class="sxs-lookup"><span data-stu-id="05c24-222">Drag a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control onto the page and drop it on a separate line below the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>
7. <span data-ttu-id="05c24-223">将插入点置于[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件的上方，然后键入 "**输入您的姓名：** "。</span><span class="sxs-lookup"><span data-stu-id="05c24-223">Put the insertion point above the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control, and then type **Enter your name:** .</span></span>

    <span data-ttu-id="05c24-224">此静态 HTML 文本是[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控件的标题。</span><span class="sxs-lookup"><span data-stu-id="05c24-224">This static HTML text is the caption for the [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) control.</span></span> <span data-ttu-id="05c24-225">您可以在同一页上混合使用静态 HTML 和服务器控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-225">You can mix static HTML and server controls on the same page.</span></span> <span data-ttu-id="05c24-226">下图显示了在 "**设计**" 视图中显示三个控件的方式。</span><span class="sxs-lookup"><span data-stu-id="05c24-226">The following illustration shows how the three controls appear in **Design** view.</span></span>

    <span data-ttu-id="05c24-227">![设计视图中的三个控件](creating-a-basic-web-forms-page/_static/image9.png "设计视图中的三个控件")</span><span class="sxs-lookup"><span data-stu-id="05c24-227">![Three controls in Design view](creating-a-basic-web-forms-page/_static/image9.png "Three controls in Design view")</span></span>

### <a name="setting-control-properties"></a><span data-ttu-id="05c24-228">设置控件属性</span><span class="sxs-lookup"><span data-stu-id="05c24-228">Setting Control Properties</span></span>

<span data-ttu-id="05c24-229">Visual Studio 提供了各种方法来设置页面上控件的属性。</span><span class="sxs-lookup"><span data-stu-id="05c24-229">Visual Studio offers you various ways to set the properties of controls on the page.</span></span> <span data-ttu-id="05c24-230">在本演练的此部分，您将在 "**设计**" 视图和 "**源**" 视图中设置属性。</span><span class="sxs-lookup"><span data-stu-id="05c24-230">In this part of the walkthrough, you will set properties in both **Design** view and **Source** view.</span></span>

### <a name="to-set-control-properties"></a><span data-ttu-id="05c24-231">设置控件属性</span><span class="sxs-lookup"><span data-stu-id="05c24-231">To set control properties</span></span>

1. <span data-ttu-id="05c24-232">首先，通过在 "**视图**" 菜单中选择 "&gt;**其他 windows** -&gt;"**属性 "窗口**来显示"**属性**"窗口。</span><span class="sxs-lookup"><span data-stu-id="05c24-232">First, display the **Properties** windows by selecting from the **View** menu -&gt; **Other Windows** -&gt; **Properties Window**.</span></span> <span data-ttu-id="05c24-233">还可以选择**F4**以显示 "**属性**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="05c24-233">You could alternatively select **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="05c24-234">选择 " [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) " 控件，然后在 "**属性**" 窗口中，将 "**文本**" 的值设置为 "**显示名称**"。</span><span class="sxs-lookup"><span data-stu-id="05c24-234">Select the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, and then in the **Properties** window, set the value of **Text** to **Display Name**.</span></span> <span data-ttu-id="05c24-235">您输入的文本将出现在设计器中的按钮上，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="05c24-235">The text you entered appears on the button in the designer, as shown in the following illustration.</span></span>

    <span data-ttu-id="05c24-236">![设置按钮文本](creating-a-basic-web-forms-page/_static/image10.png "设置按钮文本")</span><span class="sxs-lookup"><span data-stu-id="05c24-236">![Set Button text](creating-a-basic-web-forms-page/_static/image10.png "Set Button text")</span></span>
3. <span data-ttu-id="05c24-237">切换到 "**源**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-237">Switch to **Source** view.</span></span>

    <span data-ttu-id="05c24-238">"**源**" 视图显示页面的 HTML，其中包括 Visual Studio 为服务器控件创建的元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-238">**Source** view displays the HTML for the page, including the elements that Visual Studio has created for the server controls.</span></span> <span data-ttu-id="05c24-239">控件使用类似于 HTML 的语法进行声明，只不过标记使用前缀**asp：** 并包括属性**runat =&quot;server&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="05c24-239">Controls are declared using HTML-like syntax, except that the tags use the prefix **asp:** and include the attribute **runat=&quot;server&quot;**.</span></span>

    <span data-ttu-id="05c24-240">控件属性被声明为属性。</span><span class="sxs-lookup"><span data-stu-id="05c24-240">Control properties are declared as attributes.</span></span> <span data-ttu-id="05c24-241">例如，在步骤1中设置[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的 " [text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) " 属性时，实际上是在控件的标记中设置**文本**特性。</span><span class="sxs-lookup"><span data-stu-id="05c24-241">For example, when you set the [Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) property for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control, in step 1, you were actually setting the **Text** attribute in the control's markup.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="05c24-242">所有控件都在**form**元素内，该元素还具有特性**runat =&quot;server&quot;** 。</span><span class="sxs-lookup"><span data-stu-id="05c24-242">All the controls are inside a **form** element, which also has the attribute **runat=&quot;server&quot;**.</span></span> <span data-ttu-id="05c24-243">**Runat =&quot;server&quot;** 属性和**asp：** control 标记的前缀标记这些控件，以便在页面运行时由服务器上的 ASP.NET 进行处理。</span><span class="sxs-lookup"><span data-stu-id="05c24-243">The **runat=&quot;server&quot;** attribute and the **asp:** prefix for control tags mark the controls so that they are processed by ASP.NET on the server when the page runs.</span></span> <span data-ttu-id="05c24-244">位于 **&lt;窗体 runat =&quot;server&quot;&gt;** 和 **&lt;script runat =&quot;server&quot;** &gt;元素的代码不会以任何形式发送到浏览器，这就是 ASP.NET 代码必须位于其开始标记包含**runat =&quot;server&quot;** 特性的元素内的原因。</span><span class="sxs-lookup"><span data-stu-id="05c24-244">Code outside of **&lt;form runat=&quot;server&quot;&gt;** and **&lt;script runat=&quot;server&quot;&gt;** elements is sent unchanged to the browser, which is why the ASP.NET code must be inside an element whose opening tag contains the **runat=&quot;server&quot;** attribute.</span></span>
4. <span data-ttu-id="05c24-245">接下来，您将向 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件添加其他属性。</span><span class="sxs-lookup"><span data-stu-id="05c24-245">Next, you will add an additional property to the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)  control.</span></span> <span data-ttu-id="05c24-246">将插入点直接置于 **&lt;asp： label&gt;** **标记中，** 然后按**空格键**。</span><span class="sxs-lookup"><span data-stu-id="05c24-246">Put the insertion point directly after **asp:Label** in the **&lt;asp:Label&gt;** tag, and then press **SPACEBAR**.</span></span>

    <span data-ttu-id="05c24-247">此时将显示一个下拉列表，其中显示可以为 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件设置的可用属性列表。</span><span class="sxs-lookup"><span data-stu-id="05c24-247">A drop-down list appears that displays the list of available properties you can set for a [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="05c24-248">此功能称为**IntelliSense**，可帮助你在**源**视图中包含服务器控件、HTML 元素和页面上其他项的语法。</span><span class="sxs-lookup"><span data-stu-id="05c24-248">This feature, referred to as **IntelliSense**, helps you in **Source** view with the syntax of server controls, HTML elements, and other items on the page.</span></span> <span data-ttu-id="05c24-249">下图显示了 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件的**IntelliSense**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="05c24-249">The following illustration shows the **IntelliSense** drop-down list for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

    <span data-ttu-id="05c24-250">![IntelliSense 特性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 特性")</span><span class="sxs-lookup"><span data-stu-id="05c24-250">![IntelliSense attributes](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense attributes")</span></span>
5. <span data-ttu-id="05c24-251">选择 "**前景色**"，然后键入一个等号。</span><span class="sxs-lookup"><span data-stu-id="05c24-251">Select **ForeColor** and then type an equal sign.</span></span>

    <span data-ttu-id="05c24-252">IntelliSense 显示颜色列表。</span><span class="sxs-lookup"><span data-stu-id="05c24-252">IntelliSense displays a list of colors.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="05c24-253">查看代码时，可随时按**CTRL + J**显示**IntelliSense**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="05c24-253">You can display an **IntelliSense** drop-down list at any time by pressing **CTRL+J** when viewing code.</span></span>
6. <span data-ttu-id="05c24-254">为 " **[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** " 控件的文本选择颜色。</span><span class="sxs-lookup"><span data-stu-id="05c24-254">Select a color for the **[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** control's text.</span></span> <span data-ttu-id="05c24-255">请确保选择一个足够深色的颜色，使其能够阅读白色背景。</span><span class="sxs-lookup"><span data-stu-id="05c24-255">Make sure you select a color that is dark enough to read against a white background.</span></span>

    <span data-ttu-id="05c24-256">用您选择的颜色（包括右引号）完成**前景色**属性。</span><span class="sxs-lookup"><span data-stu-id="05c24-256">The **ForeColor** attribute is completed with the color that you have selected, including the closing quotation mark.</span></span>

### <a name="programming-the-button-control"></a><span data-ttu-id="05c24-257">对按钮控件进行编程</span><span class="sxs-lookup"><span data-stu-id="05c24-257">Programming the Button Control</span></span>

<span data-ttu-id="05c24-258">对于本演练，您将编写代码来读取用户在文本框中输入的名称，然后在 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件中显示该名称。</span><span class="sxs-lookup"><span data-stu-id="05c24-258">For this walkthrough, you will write code that reads the name that the user enters into the text box and then displays the name in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>

### <a name="add-a-default-button-event-handler"></a><span data-ttu-id="05c24-259">添加默认按钮事件处理程序</span><span class="sxs-lookup"><span data-stu-id="05c24-259">Add a default button event handler</span></span>

1. <span data-ttu-id="05c24-260">切换到 "**设计**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-260">Switch to **Design** view.</span></span>
2. <span data-ttu-id="05c24-261">双击[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-261">Double-click the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control.</span></span>

    <span data-ttu-id="05c24-262">默认情况下，Visual Studio 会切换到代码隐藏文件，并为[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的默认事件（即[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件）创建主干事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="05c24-262">By default, Visual Studio switches to a code-behind file and creates a skeleton event handler for the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's default event, the [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event.</span></span> <span data-ttu-id="05c24-263">代码隐藏文件将 UI 标记（如 HTML）从服务器代码（如C#）中分离出来。</span><span class="sxs-lookup"><span data-stu-id="05c24-263">The code-behind file separates your UI markup (such as HTML) from your server code (such as C#).</span></span>   
   <span data-ttu-id="05c24-264">光标定位到为此事件处理程序添加的代码。</span><span class="sxs-lookup"><span data-stu-id="05c24-264">The cursor is positioned to added code for this event handler.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="05c24-265">在 "**设计**" 视图中双击控件只是创建事件处理程序的几种方法之一。</span><span class="sxs-lookup"><span data-stu-id="05c24-265">Double-clicking a control in **Design** view is just one of several ways you can create event handlers.</span></span>
3. <span data-ttu-id="05c24-266">在**Button1 内\_单击**"事件处理程序"，键入**Label1** ，后跟一个句点（ **.** ）。</span><span class="sxs-lookup"><span data-stu-id="05c24-266">Inside the **Button1\_Click** event handler, type **Label1** followed by a period (**.**).</span></span>

    <span data-ttu-id="05c24-267">在标签（**Label1**）的**ID**后面键入句点时，Visual Studio 将显示 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件的可用成员列表，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="05c24-267">When you type the period after the **ID** of the label (**Label1**), Visual Studio displays a list of available members for the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control, as shown in the following illustration.</span></span> <span data-ttu-id="05c24-268">成员通常是属性、方法或事件。</span><span class="sxs-lookup"><span data-stu-id="05c24-268">A member commonly a property, method, or event.</span></span>

    <span data-ttu-id="05c24-269">![代码视图中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "代码视图中的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="05c24-269">![IntelliSense in Code view](creating-a-basic-web-forms-page/_static/image12.png "IntelliSense in Code view")</span></span>
4. <span data-ttu-id="05c24-270">完成按钮的**单击**事件处理程序，使其读取，如下面的代码示例中所示。</span><span class="sxs-lookup"><span data-stu-id="05c24-270">Finish the **Click** event handler for the button so that it reads as shown in the following code example.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. <span data-ttu-id="05c24-271">在**解决方案资源管理器**中右键单击 " *FirstWebPage* "，然后选择 "**查看标记**"，切换回查看 HTML 标记的**源**视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-271">Switch back to viewing the **Source** view of your HTML markup by right-clicking *FirstWebPage.aspx* in the **Solution Explorer** and selecting **View Markup**.</span></span>
6. <span data-ttu-id="05c24-272">滚动到 **&lt;asp：按钮&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-272">Scroll to the **&lt;asp:Button&gt;** element.</span></span> <span data-ttu-id="05c24-273">请注意， **&lt;asp： Button&gt;** 元素现在具有属性**Onclick =&quot;Button1\_单击 "&quot;** "。</span><span class="sxs-lookup"><span data-stu-id="05c24-273">Note that the **&lt;asp:Button&gt;** element now has the attribute **onclick=&quot;Button1\_Click&quot;**.</span></span>

    <span data-ttu-id="05c24-274">此属性将按钮的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件绑定到你在上一步中编码的处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="05c24-274">This attribute binds the button's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event to the handler method you coded in the previous step.</span></span>

    <span data-ttu-id="05c24-275">事件处理程序方法可以具有任何名称;你看到的名称是 Visual Studio 创建的默认名称。</span><span class="sxs-lookup"><span data-stu-id="05c24-275">Event handler methods can have any name; the name you see is the default name created by Visual Studio.</span></span> <span data-ttu-id="05c24-276">重要的是，用于 HTML 中的**OnClick**特性的名称必须与代码隐藏中定义的方法的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="05c24-276">The important point is that the name used for the **OnClick** attribute in the HTML must match the name of a method defined in the code-behind.</span></span>

### <a name="running-the-page"></a><span data-ttu-id="05c24-277">运行页面</span><span class="sxs-lookup"><span data-stu-id="05c24-277">Running the Page</span></span>

<span data-ttu-id="05c24-278">现在可以测试页上的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-278">You can now test the server controls on the page.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="05c24-279">运行页面</span><span class="sxs-lookup"><span data-stu-id="05c24-279">To run the page</span></span>

1. <span data-ttu-id="05c24-280">按**CTRL + F5**在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="05c24-280">Press **CTRL+F5** to run the page in the browser.</span></span> <span data-ttu-id="05c24-281">如果发生错误，请重新检查以上步骤。</span><span class="sxs-lookup"><span data-stu-id="05c24-281">If an error occurs, recheck the steps above.</span></span>
2. <span data-ttu-id="05c24-282">在文本框中输入一个名称，然后单击 "**显示名称**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="05c24-282">Enter a name into the text box and click the **Display Name** button.</span></span>

    <span data-ttu-id="05c24-283">您输入的名称将显示在 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件中。</span><span class="sxs-lookup"><span data-stu-id="05c24-283">The name you entered is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span> <span data-ttu-id="05c24-284">请注意，单击该按钮时，该页将发送到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="05c24-284">Note that when you click the button, the page is posted to the Web server.</span></span> <span data-ttu-id="05c24-285">然后，ASP.NET 重新创建页面，运行你的代码（在这种情况下，[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控件的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件处理程序会运行），然后将新页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="05c24-285">ASP.NET then recreates the page, runs your code (in this case, the [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control's [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event handler runs), and then sends the new page to the browser.</span></span> <span data-ttu-id="05c24-286">如果在浏览器中监视状态栏，则每次单击按钮时，都可以看到该页正在往返 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="05c24-286">If you watch the status bar in the browser, you can see that the page is making a round trip to the Web server each time you click the button.</span></span>
3. <span data-ttu-id="05c24-287">在浏览器中，右键单击该页并选择 "**查看源**"，查看正在运行的页面的源。</span><span class="sxs-lookup"><span data-stu-id="05c24-287">In the browser, view the source of the page you are running by right-clicking on the page and selecting **View source**.</span></span>

    <span data-ttu-id="05c24-288">在页源代码中，你将看到没有任何服务器代码的 HTML。</span><span class="sxs-lookup"><span data-stu-id="05c24-288">In the page source code, you see HTML without any server code.</span></span> <span data-ttu-id="05c24-289">具体而言，你看不到 **&lt;asp：** 在**源**视图中使用的&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-289">Specifically, you do not see the **&lt;asp:&gt;** elements that you were working with in **Source** view.</span></span> <span data-ttu-id="05c24-290">当页面运行时，ASP.NET 将处理服务器控件，并将 HTML 元素呈现给执行表示控件的函数的页面。</span><span class="sxs-lookup"><span data-stu-id="05c24-290">When the page runs, ASP.NET processes the server controls and renders HTML elements to the page that perform the functions that represent the control.</span></span> <span data-ttu-id="05c24-291">例如， **&lt;asp： Button&gt;** 控件呈现为 HTML **&lt;输入类型 =&quot;提交&quot;&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-291">For example, the **&lt;asp:Button&gt;** control is rendered as the HTML **&lt;input type=&quot;submit&quot;&gt;** element.</span></span>
4. <span data-ttu-id="05c24-292">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="05c24-292">Close the browser.</span></span>

## <a name="working-with-additional-controls"></a><span data-ttu-id="05c24-293">使用其他控件</span><span class="sxs-lookup"><span data-stu-id="05c24-293">Working with Additional Controls</span></span>

<a id="sectionToggle2"></a>

<span data-ttu-id="05c24-294">在本演练的此部分，您将使用[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件，该控件每次显示一个月的日期。</span><span class="sxs-lookup"><span data-stu-id="05c24-294">In this part of the walkthrough, you will work with the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control, which displays dates a month at a time.</span></span> <span data-ttu-id="05c24-295">[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件比你使用的 "按钮"、"文本框" 和 "标签" 更复杂，并说明了服务器控件的一些其他功能。</span><span class="sxs-lookup"><span data-stu-id="05c24-295">The [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control is a more complex control than the button, text box, and label you have been working with and illustrates some further capabilities of server controls.</span></span>

<span data-ttu-id="05c24-296">在本部分中，你将向页面中添加[WebControls](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="05c24-296">In this section, you will add a [System.Web.UI.WebControls.Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to the page and format it.</span></span>

### <a name="to-add-a-calendar-control"></a><span data-ttu-id="05c24-297">添加日历控件</span><span class="sxs-lookup"><span data-stu-id="05c24-297">To add a Calendar control</span></span>

1. <span data-ttu-id="05c24-298">在 Visual Studio 中，切换到 "**设计**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-298">In Visual Studio, switch to **Design** view.</span></span>
2. <span data-ttu-id="05c24-299">从 "**工具箱**" 的 "**标准**" 部分，将 "[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)" 控件拖动到页面上，并将其放置在包含其他控件的**div**元素下。</span><span class="sxs-lookup"><span data-stu-id="05c24-299">From the **Standard** section of the **Toolbox**, drag a [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control onto the page and drop it below the **div** element that contains the other controls.</span></span>

    <span data-ttu-id="05c24-300">将显示日历的智能标记面板。</span><span class="sxs-lookup"><span data-stu-id="05c24-300">The calendar's smart tag panel is displayed.</span></span> <span data-ttu-id="05c24-301">该面板会显示命令，使您可以轻松地为所选控件执行最常见的任务。</span><span class="sxs-lookup"><span data-stu-id="05c24-301">The panel displays commands that make it easy for you to perform the most common tasks for the selected control.</span></span> <span data-ttu-id="05c24-302">下图显示了在 "**设计**" 视图中呈现的[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-302">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control as rendered in **Design** view.</span></span>

    <span data-ttu-id="05c24-303">![设计视图中的日历控件](creating-a-basic-web-forms-page/_static/image13.png "设计视图中的 Calendar 控件")</span><span class="sxs-lookup"><span data-stu-id="05c24-303">![Calendar control in Design view](creating-a-basic-web-forms-page/_static/image13.png "Calendar control in Design view")</span></span>
3. <span data-ttu-id="05c24-304">在智能标记面板中，选择 "**自动套用格式**"。</span><span class="sxs-lookup"><span data-stu-id="05c24-304">In the smart tag panel, choose **Auto Format**.</span></span>

    <span data-ttu-id="05c24-305">此时将显示 "**自动套用格式**" 对话框，使用该对话框可以选择日历的格式设置方案。</span><span class="sxs-lookup"><span data-stu-id="05c24-305">The **Auto Format** dialog box is displayed, which allows you to select a formatting scheme for the calendar.</span></span> <span data-ttu-id="05c24-306">下图显示了[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件的 "**自动套用格式**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="05c24-306">The following illustration shows the **Auto Format** dialog box for the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="05c24-307">!["自动套用格式" 对话框（日历控件）](creating-a-basic-web-forms-page/_static/image14.png "“自动套用格式”对话框（Calendar 控件）")</span><span class="sxs-lookup"><span data-stu-id="05c24-307">![Auto Format dialog box (Calendar control)](creating-a-basic-web-forms-page/_static/image14.png "Auto Format dialog box (Calendar control)")</span></span>
4. <span data-ttu-id="05c24-308">从 "**选择方案**" 列表中，选择 "**简单**"，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="05c24-308">From the **Select a scheme** list, select **Simple** and then click **OK**.</span></span>
5. <span data-ttu-id="05c24-309">切换到 "**源**" 视图。</span><span class="sxs-lookup"><span data-stu-id="05c24-309">Switch to **Source** view.</span></span>

    <span data-ttu-id="05c24-310">你可以查看 **&lt;asp： Calendar&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-310">You can see the **&lt;asp:Calendar&gt;** element.</span></span> <span data-ttu-id="05c24-311">此元素比之前创建的简单控件的元素长很多。</span><span class="sxs-lookup"><span data-stu-id="05c24-311">This element is much longer than the elements for the simple controls you created earlier.</span></span> <span data-ttu-id="05c24-312">它还包括子元素，如 **&lt;WeekEndDayStyle&gt;** ，它表示各种格式设置。</span><span class="sxs-lookup"><span data-stu-id="05c24-312">It also includes subelements, such as **&lt;WeekEndDayStyle&gt;**, which represent various formatting settings.</span></span> <span data-ttu-id="05c24-313">下图显示了 "**源**" 视图中的[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-313">The following illustration shows the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control in **Source** view.</span></span> <span data-ttu-id="05c24-314">（您在 "**源**" 视图中看到的确切标记可能与插图略有不同。）</span><span class="sxs-lookup"><span data-stu-id="05c24-314">(The exact markup that you see in **Source** view might differ slightly from the illustration.)</span></span>

    <span data-ttu-id="05c24-315">![源视图中的日历控件](creating-a-basic-web-forms-page/_static/image15.png "源视图中的 Calendar 控件")</span><span class="sxs-lookup"><span data-stu-id="05c24-315">![Calendar control in Source view](creating-a-basic-web-forms-page/_static/image15.png "Calendar control in Source view")</span></span>

### <a name="programming-the-calendar-control"></a><span data-ttu-id="05c24-316">设计 Calendar 控件</span><span class="sxs-lookup"><span data-stu-id="05c24-316">Programming the Calendar Control</span></span>

<span data-ttu-id="05c24-317">在本部分中，您将计划 "[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)" 控件以显示当前选定的日期。</span><span class="sxs-lookup"><span data-stu-id="05c24-317">In this section, you will program the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control to display the currently selected date.</span></span>

### <a name="to-program-the-calendar-control"></a><span data-ttu-id="05c24-318">对日历控件进行编程</span><span class="sxs-lookup"><span data-stu-id="05c24-318">To program the Calendar control</span></span>

1. <span data-ttu-id="05c24-319">在 "**设计**" 视图中，双击 "[日历](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)" 控件。</span><span class="sxs-lookup"><span data-stu-id="05c24-319">In **Design** view, double-click the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control.</span></span>

    <span data-ttu-id="05c24-320">将创建新的事件处理程序，并将其显示在名为*FirstWebPage.aspx.cs*的代码隐藏文件中。</span><span class="sxs-lookup"><span data-stu-id="05c24-320">A new event handler is created and displayed in the code-behind file named *FirstWebPage.aspx.cs*.</span></span>
2. <span data-ttu-id="05c24-321">用下面的代码完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="05c24-321">Finish the [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) event handler with the following code.</span></span>

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    <span data-ttu-id="05c24-322">上面的代码将 "标签" 控件的文本设置为 calendar 控件的所选日期。</span><span class="sxs-lookup"><span data-stu-id="05c24-322">The above code sets the text of the label control to the selected date of the calendar control.</span></span>

### <a name="running-the-page"></a><span data-ttu-id="05c24-323">运行页面</span><span class="sxs-lookup"><span data-stu-id="05c24-323">Running the Page</span></span>

<span data-ttu-id="05c24-324">现在可以测试日历。</span><span class="sxs-lookup"><span data-stu-id="05c24-324">You can now test the calendar.</span></span>

### <a name="to-run-the-page"></a><span data-ttu-id="05c24-325">运行页面</span><span class="sxs-lookup"><span data-stu-id="05c24-325">To run the page</span></span>

1. <span data-ttu-id="05c24-326">按**CTRL + F5**在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="05c24-326">Press **CTRL+F5** to run the page in the browser.</span></span>
2. <span data-ttu-id="05c24-327">单击日历中的日期。</span><span class="sxs-lookup"><span data-stu-id="05c24-327">Click a date in the calendar.</span></span>

    <span data-ttu-id="05c24-328">您单击的日期将显示在 "[标签](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)" 控件中。</span><span class="sxs-lookup"><span data-stu-id="05c24-328">The date you clicked is displayed in the [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) control.</span></span>
3. <span data-ttu-id="05c24-329">在浏览器中，查看页面的源代码。</span><span class="sxs-lookup"><span data-stu-id="05c24-329">In the browser, view the source code for the page.</span></span>

    <span data-ttu-id="05c24-330">请注意， [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控件已以**表**的形式呈现到页面，每一天都作为**td**元素。</span><span class="sxs-lookup"><span data-stu-id="05c24-330">Note that the [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) control has been rendered to the page as a **table**, with each day as a **td** element.</span></span>
4. <span data-ttu-id="05c24-331">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="05c24-331">Close the browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05c24-332">后续步骤</span><span class="sxs-lookup"><span data-stu-id="05c24-332">Next Steps</span></span>

<a id="nextStepsToggle"></a>

<span data-ttu-id="05c24-333">本演练演示了 Visual Studio 页面设计器的基本功能。</span><span class="sxs-lookup"><span data-stu-id="05c24-333">This walkthrough has illustrated the basic features of the Visual Studio page designer.</span></span> <span data-ttu-id="05c24-334">现在，你已了解如何在 Visual Studio 中创建和编辑 Web 窗体页面，你可能需要浏览其他功能。</span><span class="sxs-lookup"><span data-stu-id="05c24-334">Now that you understand how to create and edit a Web Forms page in Visual Studio, you might want to explore other features.</span></span> <span data-ttu-id="05c24-335">例如，你可能需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="05c24-335">For example, you might want to do the following:</span></span>

- <span data-ttu-id="05c24-336">按照[使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)分步教程系列来了解有关 ASP.NET Web 窗体的详细信息。</span><span class="sxs-lookup"><span data-stu-id="05c24-336">Learn more about ASP.NET Web Forms by following the step-by-step tutorial series [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md).</span></span>
- <span data-ttu-id="05c24-337">详细了解级联样式表（CSS）。</span><span class="sxs-lookup"><span data-stu-id="05c24-337">Learn more about Cascading style sheets (CSS).</span></span> <span data-ttu-id="05c24-338">有关详细信息，请参阅[使用 CSS 概述](https://msdn.microsoft.com/library/bb398931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05c24-338">For details, see [Working with CSS Overview](https://msdn.microsoft.com/library/bb398931.aspx).</span></span>
