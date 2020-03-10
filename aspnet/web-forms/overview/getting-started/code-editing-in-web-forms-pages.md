---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: 在 Visual Studio 2013 中编辑 ASP.NET Web 窗体的代码 |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513638"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="76d2c-102">在 Visual Studio 2013 中编辑 ASP.NET Web 窗体的代码</span><span class="sxs-lookup"><span data-stu-id="76d2c-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>

<span data-ttu-id="76d2c-103">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="76d2c-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="76d2c-104">在许多 ASP.NET Web 窗体页面中，你可以 Visual Basic、 C#或其他语言编写代码。</span><span class="sxs-lookup"><span data-stu-id="76d2c-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="76d2c-105">Visual Studio 中的代码编辑器可以帮助你快速编写代码，同时可帮助避免错误。</span><span class="sxs-lookup"><span data-stu-id="76d2c-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="76d2c-106">此外，该编辑器还提供了创建可重用代码的方法，以帮助减少需要执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="76d2c-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="76d2c-107">此演练演示了 Visual Studio 代码编辑器的各种功能。</span><span class="sxs-lookup"><span data-stu-id="76d2c-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="76d2c-108">在本演练中，你将学会如何执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="76d2c-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="76d2c-109">更正内联编码错误。</span><span class="sxs-lookup"><span data-stu-id="76d2c-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="76d2c-110">重构和重命名代码。</span><span class="sxs-lookup"><span data-stu-id="76d2c-110">Refactor and rename code.</span></span>
- <span data-ttu-id="76d2c-111">重命名变量和对象。</span><span class="sxs-lookup"><span data-stu-id="76d2c-111">Rename variables and objects.</span></span>
- <span data-ttu-id="76d2c-112">插入代码片段。</span><span class="sxs-lookup"><span data-stu-id="76d2c-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76d2c-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="76d2c-113">Prerequisites</span></span>

<span data-ttu-id="76d2c-114">若要完成本演练，你将需要：</span><span class="sxs-lookup"><span data-stu-id="76d2c-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="76d2c-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="76d2c-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="76d2c-116">将自动安装 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="76d2c-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="76d2c-117">在本系列教程中，Web 的 Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 通常称为 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="76d2c-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="76d2c-118">如果你使用的是 Visual Studio，则本演练假定你在首次启动 Visual Studio 时选择了 " **Web 开发**" 设置集合。</span><span class="sxs-lookup"><span data-stu-id="76d2c-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="76d2c-119">有关详细信息，请参阅[如何：选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76d2c-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="76d2c-120">创建 Web 应用程序项目和页面</span><span class="sxs-lookup"><span data-stu-id="76d2c-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="76d2c-121">在本演练的此部分中，你将创建一个 Web 应用程序项目并向其添加新页。</span><span class="sxs-lookup"><span data-stu-id="76d2c-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="76d2c-122">创建 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="76d2c-122">To create a Web application project</span></span>

1. <span data-ttu-id="76d2c-123">打开 Microsoft Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="76d2c-123">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="76d2c-124">在“文件”菜单上，选择“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="76d2c-124">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="76d2c-125">![文件 "菜单](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="76d2c-125">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="76d2c-126">此时将出现“新建项目”对话框。</span><span class="sxs-lookup"><span data-stu-id="76d2c-126">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="76d2c-127">选择左侧的 "**模板**" -&gt; **Visual C#**  -&gt; **Web**模板 "组。</span><span class="sxs-lookup"><span data-stu-id="76d2c-127">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="76d2c-128">在中心列中选择 " **ASP.NET Web 应用程序**" 模板。</span><span class="sxs-lookup"><span data-stu-id="76d2c-128">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="76d2c-129">将项目命名为 " ***BasicWebApp*** "，然后单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="76d2c-129">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="76d2c-130">![“新建项目”对话框](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="76d2c-130">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="76d2c-131">接下来，选择 " **Web 窗体**" 模板，然后单击 "**确定"** 按钮创建项目。</span><span class="sxs-lookup"><span data-stu-id="76d2c-131">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="76d2c-132">![新的 ASP.NET 项目 "对话框](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="76d2c-132">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="76d2c-133">Visual Studio 会创建一个新项目，其中包含基于 Web 窗体模板的预生成功能。</span><span class="sxs-lookup"><span data-stu-id="76d2c-133">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>

## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="76d2c-134">创建新的 ASP.NET Web 窗体页</span><span class="sxs-lookup"><span data-stu-id="76d2c-134">Creating a new ASP.NET Web Forms Page</span></span>

<span data-ttu-id="76d2c-135">使用 " **ASP.NET Web 应用程序**" 项目模板创建新的 Web 窗体应用程序时，Visual Studio 会添加一个名为 " *default.aspx*" 的 ASP.NET 页面（Web 窗体页）以及多个其他文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="76d2c-135">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="76d2c-136">你可以使用*default.aspx*页作为你的 Web 应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="76d2c-136">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="76d2c-137">但是，对于本演练，您将创建并使用一个新页。</span><span class="sxs-lookup"><span data-stu-id="76d2c-137">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="76d2c-138">向 Web 应用程序添加页</span><span class="sxs-lookup"><span data-stu-id="76d2c-138">To add a page to the Web application</span></span>

1. <span data-ttu-id="76d2c-139">在**解决方案资源管理器**中，右键单击 Web 应用程序名称（在本教程中，应用程序名称为 " **BasicWebSite**"），然后单击 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="76d2c-139">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="76d2c-140">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="76d2c-140">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="76d2c-141">选择左侧的 " **Visual C#**  -&gt; **Web**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="76d2c-141">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="76d2c-142">然后，从中间列表中选择 " **Web 窗体**" 并将其命名为 " *FirstWebPage*"。</span><span class="sxs-lookup"><span data-stu-id="76d2c-142">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="76d2c-143">![“添加新项”对话框](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="76d2c-143">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="76d2c-144">单击 "**添加**"，将 Web 窗体页添加到您的项目中。</span><span class="sxs-lookup"><span data-stu-id="76d2c-144">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="76d2c-145">Visual Studio 将创建新页并将其打开。</span><span class="sxs-lookup"><span data-stu-id="76d2c-145">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="76d2c-146">接下来，将此新页设置为默认启动页。</span><span class="sxs-lookup"><span data-stu-id="76d2c-146">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="76d2c-147">在**解决方案资源管理器**中，右键单击名为*FirstWebPage*的新页面，然后选择 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="76d2c-147">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="76d2c-148">下次运行此应用程序来测试进度时，会自动在浏览器中看到此新页。</span><span class="sxs-lookup"><span data-stu-id="76d2c-148">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>

## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="76d2c-149">更正内联编码错误</span><span class="sxs-lookup"><span data-stu-id="76d2c-149">Correcting Inline Coding Errors</span></span>

<span data-ttu-id="76d2c-150">Visual Studio 中的代码编辑器可帮助你在编写代码时避免错误，如果你发生了错误，代码编辑器将有助于更正此错误。</span><span class="sxs-lookup"><span data-stu-id="76d2c-150">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="76d2c-151">在本演练的此部分，您将编写一行代码，用于说明编辑器中的错误更正功能。</span><span class="sxs-lookup"><span data-stu-id="76d2c-151">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="76d2c-152">更正 Visual Studio 中的简单编码错误</span><span class="sxs-lookup"><span data-stu-id="76d2c-152">To correct simple coding errors in Visual Studio</span></span>

1. <span data-ttu-id="76d2c-153">在 "**设计**" 视图中，双击空白页为该页的**Load**事件创建处理程序。</span><span class="sxs-lookup"><span data-stu-id="76d2c-153">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="76d2c-154">只能将事件处理程序用作编写某些代码的位置。</span><span class="sxs-lookup"><span data-stu-id="76d2c-154">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="76d2c-155">在处理程序中，键入以下包含错误的行，然后按**enter**：</span><span class="sxs-lookup"><span data-stu-id="76d2c-155">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="76d2c-156">按下**enter**后，代码编辑器会将绿色和红色下划线（&quot;通常&quot; 行）置于出现问题的代码区域下。</span><span class="sxs-lookup"><span data-stu-id="76d2c-156">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="76d2c-157">绿色下划线表示警告。</span><span class="sxs-lookup"><span data-stu-id="76d2c-157">A green underline indicates a warning.</span></span> <span data-ttu-id="76d2c-158">红色下划线指示必须修复的错误。</span><span class="sxs-lookup"><span data-stu-id="76d2c-158">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="76d2c-159">将鼠标指针停留在 `myStr` 上可查看工具提示，告诉你有关警告。</span><span class="sxs-lookup"><span data-stu-id="76d2c-159">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="76d2c-160">同时，将鼠标指针停留在红色下划线上以查看错误消息。</span><span class="sxs-lookup"><span data-stu-id="76d2c-160">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="76d2c-161">下图显示带下划线的代码。</span><span class="sxs-lookup"><span data-stu-id="76d2c-161">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="76d2c-162">![设计视图中的欢迎文本](code-editing-in-web-forms-pages/_static/image5.png "设计视图中的欢迎文本")</span><span class="sxs-lookup"><span data-stu-id="76d2c-162">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="76d2c-163">必须通过在行的末尾添加一个分号 `;` 来修复该错误。</span><span class="sxs-lookup"><span data-stu-id="76d2c-163">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="76d2c-164">警告只会通知你尚未使用 `myStr` 变量。</span><span class="sxs-lookup"><span data-stu-id="76d2c-164">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="76d2c-165">在 Visual Studio 中查看当前代码格式设置，方法是选择 "**工具**" -&gt;**选项**" -&gt;**字体和颜色**"。</span><span class="sxs-lookup"><span data-stu-id="76d2c-165">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>

## <a name="refactoring-and-renaming"></a><span data-ttu-id="76d2c-166">重构和重命名</span><span class="sxs-lookup"><span data-stu-id="76d2c-166">Refactoring and Renaming</span></span>

<span data-ttu-id="76d2c-167">重构是一种软件方法，涉及重构你的代码，使其更易于理解和维护，同时保留其功能。</span><span class="sxs-lookup"><span data-stu-id="76d2c-167">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="76d2c-168">一个简单的示例是在事件处理程序中编写代码以从数据库中获取数据。</span><span class="sxs-lookup"><span data-stu-id="76d2c-168">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="76d2c-169">开发页面时，会发现需要从多个不同的处理程序访问数据。</span><span class="sxs-lookup"><span data-stu-id="76d2c-169">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="76d2c-170">因此，通过在页中创建数据访问方法并在处理程序中插入对方法的调用，可以重构该页的代码。</span><span class="sxs-lookup"><span data-stu-id="76d2c-170">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="76d2c-171">代码编辑器包含可帮助您执行各种重构任务的工具。</span><span class="sxs-lookup"><span data-stu-id="76d2c-171">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="76d2c-172">在本演练中，您将使用两种重构技术：重命名变量和提取方法。</span><span class="sxs-lookup"><span data-stu-id="76d2c-172">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="76d2c-173">其他重构选项包括封装字段、将局部变量升级到方法参数和管理方法参数。</span><span class="sxs-lookup"><span data-stu-id="76d2c-173">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="76d2c-174">这些重构选项的可用性取决于代码中的位置。</span><span class="sxs-lookup"><span data-stu-id="76d2c-174">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="76d2c-175">重构代码</span><span class="sxs-lookup"><span data-stu-id="76d2c-175">Refactoring Code</span></span>

<span data-ttu-id="76d2c-176">常见的重构方案是从位于另一个成员内的代码（如方法）中创建（提取）一个方法。</span><span class="sxs-lookup"><span data-stu-id="76d2c-176">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="76d2c-177">这会减少原始成员的大小，并使提取的代码可重复使用。</span><span class="sxs-lookup"><span data-stu-id="76d2c-177">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="76d2c-178">在本演练的此部分中，你将编写一些简单的代码，然后从中提取方法。</span><span class="sxs-lookup"><span data-stu-id="76d2c-178">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="76d2c-179">支持重构C#，因此你将创建一个使用C#作为其编程语言的页面。</span><span class="sxs-lookup"><span data-stu-id="76d2c-179">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="76d2c-180">在C#页中提取方法</span><span class="sxs-lookup"><span data-stu-id="76d2c-180">To extract a method in a C# page</span></span>

1. <span data-ttu-id="76d2c-181">切换到 "**设计**" 视图。</span><span class="sxs-lookup"><span data-stu-id="76d2c-181">Switch to **Design** view.</span></span>
2. <span data-ttu-id="76d2c-182">在 "**工具箱**" 的 "**标准**" 选项卡上，将 "[按钮](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)" 控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="76d2c-182">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="76d2c-183">双击**按钮**控件为其[单击](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件创建处理程序，然后添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="76d2c-183">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="76d2c-184">此代码创建一个**ArrayList**对象，使用一个循环将其加载到值，然后使用另一个循环来显示**ArrayList**对象的内容。</span><span class="sxs-lookup"><span data-stu-id="76d2c-184">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="76d2c-185">按 " **CTRL + F5** " 运行该页面，然后单击 ""**按钮**以确保看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="76d2c-185">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="76d2c-186">返回到代码编辑器，然后在事件处理程序中选择以下行。</span><span class="sxs-lookup"><span data-stu-id="76d2c-186">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="76d2c-187">右键单击所选内容，单击 "**重构**"，然后选择 "**提取方法**"。</span><span class="sxs-lookup"><span data-stu-id="76d2c-187">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="76d2c-188">此时将显示 "**提取方法**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="76d2c-188">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="76d2c-189">在 "**新方法名称**" 框中，键入**DisplayArray**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="76d2c-189">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="76d2c-190">代码编辑器会创建一个名为 `DisplayArray`的新方法，并在该循环最初所在的**Click**处理程序中调用新方法。</span><span class="sxs-lookup"><span data-stu-id="76d2c-190">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="76d2c-191">按**CTRL + F5**再次运行该页，并单击**按钮**。</span><span class="sxs-lookup"><span data-stu-id="76d2c-191">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="76d2c-192">页面的功能与以前相同。</span><span class="sxs-lookup"><span data-stu-id="76d2c-192">The page functions the same as it did before.</span></span> <span data-ttu-id="76d2c-193">现在，`DisplayArray` 方法可以从 page 类中的任意位置调用。</span><span class="sxs-lookup"><span data-stu-id="76d2c-193">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="76d2c-194">重命名变量</span><span class="sxs-lookup"><span data-stu-id="76d2c-194">Renaming Variables</span></span>

<span data-ttu-id="76d2c-195">使用变量和对象时，你可能希望在代码中引用它们后重命名它们。</span><span class="sxs-lookup"><span data-stu-id="76d2c-195">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="76d2c-196">但是，如果未重命名其中一个引用，重命名变量和对象会导致代码中断。</span><span class="sxs-lookup"><span data-stu-id="76d2c-196">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="76d2c-197">因此，您可以使用重构来执行重命名。</span><span class="sxs-lookup"><span data-stu-id="76d2c-197">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="76d2c-198">使用重构重命名变量</span><span class="sxs-lookup"><span data-stu-id="76d2c-198">To use refactoring to rename a variable</span></span>

1. <span data-ttu-id="76d2c-199">在**Click**事件处理程序中，找到以下行：</span><span class="sxs-lookup"><span data-stu-id="76d2c-199">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="76d2c-200">右键单击变量名称 `alist`，选择 "**重构**"，然后选择 "**重命名**"。</span><span class="sxs-lookup"><span data-stu-id="76d2c-200">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="76d2c-201">此时将显示 "**重命名**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="76d2c-201">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="76d2c-202">在 "**新名称**" 框中，键入**ArrayList1** ，并确保已选中 "**预览引用更改**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="76d2c-202">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="76d2c-203">然后单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="76d2c-203">Then click **OK**.</span></span>

    <span data-ttu-id="76d2c-204">此时将显示 "**预览更改**" 对话框，并显示一个树，其中包含对您要重命名的变量的所有引用。</span><span class="sxs-lookup"><span data-stu-id="76d2c-204">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="76d2c-205">单击 "**应用**" 以关闭 "**预览更改**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="76d2c-205">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="76d2c-206">专门引用所选实例的变量将被重命名。</span><span class="sxs-lookup"><span data-stu-id="76d2c-206">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="76d2c-207">但请注意，以下行中 `alist` 的变量不会重命名。</span><span class="sxs-lookup"><span data-stu-id="76d2c-207">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="76d2c-208">此行中的变量 `alist` 不会重命名，因为它与重命名的变量 `alist` 不表示相同的值。</span><span class="sxs-lookup"><span data-stu-id="76d2c-208">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="76d2c-209">`DisplayArray` 声明中的变量 `alist` 是该方法的局部变量。</span><span class="sxs-lookup"><span data-stu-id="76d2c-209">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="76d2c-210">这说明，使用重构对变量进行重命名不同于只在编辑器中执行查找和替换操作;重构会对变量进行重命名，并了解它正在使用的变量的语义。</span><span class="sxs-lookup"><span data-stu-id="76d2c-210">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>

## <a name="inserting-snippets"></a><span data-ttu-id="76d2c-211">插入代码段</span><span class="sxs-lookup"><span data-stu-id="76d2c-211">Inserting Snippets</span></span>

<span data-ttu-id="76d2c-212">由于 Web 窗体开发人员经常需要执行很多编码任务，因此代码编辑器提供了一个代码段库或预编写代码的块。</span><span class="sxs-lookup"><span data-stu-id="76d2c-212">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="76d2c-213">可以将这些代码段插入到页面中。</span><span class="sxs-lookup"><span data-stu-id="76d2c-213">You can insert these snippets into your page.</span></span>

<span data-ttu-id="76d2c-214">在 Visual Studio 中使用的每种语言都与插入代码片段的方式略有不同。</span><span class="sxs-lookup"><span data-stu-id="76d2c-214">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="76d2c-215">有关插入代码片段的信息，请参阅[Visual Basic IntelliSense 代码片段](https://msdn.microsoft.com/library/18yz4be4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76d2c-215">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="76d2c-216">有关在视觉对象C#中插入代码片段的信息，请参阅[visual C# Code 片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76d2c-216">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d2c-217">后续步骤</span><span class="sxs-lookup"><span data-stu-id="76d2c-217">Next Steps</span></span>

<span data-ttu-id="76d2c-218">本演练演示了 Visual Studio 2010 代码编辑器的基本功能，用于更正代码中的错误、重构代码、重命名变量以及将代码段插入到代码中。</span><span class="sxs-lookup"><span data-stu-id="76d2c-218">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="76d2c-219">编辑器中的其他功能可以快速轻松地进行应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="76d2c-219">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="76d2c-220">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="76d2c-220">For example, you might want to:</span></span>

- <span data-ttu-id="76d2c-221">了解有关 IntelliSense 功能的详细信息，例如修改 IntelliSense 选项、管理代码片段和联机搜索代码片段。</span><span class="sxs-lookup"><span data-stu-id="76d2c-221">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="76d2c-222">有关详细信息，请参阅[使用 IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76d2c-222">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="76d2c-223">了解如何创建您自己的代码片段。</span><span class="sxs-lookup"><span data-stu-id="76d2c-223">Learn how to create your own code snippets.</span></span> <span data-ttu-id="76d2c-224">有关详细信息，请参阅[创建和使用 IntelliSense 代码片段](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="76d2c-224">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="76d2c-225">了解有关 IntelliSense 代码片段的特定于 Visual Basic 的功能的详细信息，例如自定义代码段和故障排除。</span><span class="sxs-lookup"><span data-stu-id="76d2c-225">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="76d2c-226">有关详细信息，请参阅[Visual Basic IntelliSense 代码片段](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="76d2c-226">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="76d2c-227">详细C#了解 IntelliSense 的特定功能，例如重构和代码片段。</span><span class="sxs-lookup"><span data-stu-id="76d2c-227">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="76d2c-228">有关详细信息，请[参阅C# Visual IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76d2c-228">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
