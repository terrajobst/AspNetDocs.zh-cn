---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第3部分：视图和 Viewmodel |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第3部分介绍了视图和 Viewmodel。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451130"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="ce56c-104">第3部分：视图和 Viewmodel</span><span class="sxs-lookup"><span data-stu-id="ce56c-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="ce56c-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="ce56c-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="ce56c-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="ce56c-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="ce56c-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="ce56c-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="ce56c-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="ce56c-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="ce56c-109">第3部分介绍了视图和 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="ce56c-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="ce56c-110">到目前为止，我们刚刚从控制器操作返回了字符串。</span><span class="sxs-lookup"><span data-stu-id="ce56c-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="ce56c-111">这是了解控制器工作方式的好方法，但并不是您想要如何构建真实的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce56c-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="ce56c-112">我们想要一种更好的方法来向访问站点的浏览器生成 HTML，其中一种方法是，我们可以使用模板文件更轻松地自定义要发回的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="ce56c-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="ce56c-113">这正是视图的作用。</span><span class="sxs-lookup"><span data-stu-id="ce56c-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="ce56c-114">添加视图模板</span><span class="sxs-lookup"><span data-stu-id="ce56c-114">Adding a View template</span></span>

<span data-ttu-id="ce56c-115">若要使用视图模板，我们将更改 HomeController Index 方法以返回 ActionResult，并使其返回 View （），如下所示：</span><span class="sxs-lookup"><span data-stu-id="ce56c-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="ce56c-116">上述更改指出，而不是返回字符串，而是想要使用 "视图" 来生成结果。</span><span class="sxs-lookup"><span data-stu-id="ce56c-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="ce56c-117">现在，我们将向项目中添加相应的视图模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="ce56c-118">为此，我们将文本光标置于索引操作方法中，然后右键单击并选择 "添加视图"。</span><span class="sxs-lookup"><span data-stu-id="ce56c-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="ce56c-119">此时将显示 "添加视图" 对话框：</span><span class="sxs-lookup"><span data-stu-id="ce56c-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="ce56c-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ce56c-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="ce56c-121">"添加视图" 对话框使我们能够快速轻松地生成视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="ce56c-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="ce56c-122">默认情况下，"添加视图" 对话框预先填充要创建的视图模板的名称，使其与将使用它的操作方法相匹配。</span><span class="sxs-lookup"><span data-stu-id="ce56c-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="ce56c-123">因为我们在 HomeController 的 Index （）操作方法中使用了 "添加视图" 上下文菜单，所以上面的 "添加视图" 对话框具有 "索引"，因为默认情况下填充了视图名称。</span><span class="sxs-lookup"><span data-stu-id="ce56c-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="ce56c-124">我们不需要更改此对话框中的任何选项，因此请单击 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ce56c-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="ce56c-125">单击 "添加" 按钮后，Visual Web Developer 会在 \Views\Home 目录中创建新的 "索引" 视图模板（如果尚不存在，则创建该文件夹）。</span><span class="sxs-lookup"><span data-stu-id="ce56c-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="ce56c-126">"ASP.NET" 文件的名称和文件夹位置很重要，并遵循默认的 "MVC 命名约定"。</span><span class="sxs-lookup"><span data-stu-id="ce56c-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="ce56c-127">目录名称 \Views\Home 与名为 HomeController 的控制器匹配。</span><span class="sxs-lookup"><span data-stu-id="ce56c-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="ce56c-128">视图模板名称、索引与将显示视图的控制器操作方法相匹配。</span><span class="sxs-lookup"><span data-stu-id="ce56c-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="ce56c-129">当我们使用此命名约定返回视图时，ASP.NET MVC 使我们无需显式指定视图模板的名称或位置。</span><span class="sxs-lookup"><span data-stu-id="ce56c-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="ce56c-130">当我们在我们的 HomeController 中编写如下代码时，它将默认呈现 \Views\Home\Index.cshtml 视图模板：</span><span class="sxs-lookup"><span data-stu-id="ce56c-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="ce56c-131">在单击 "添加视图" 对话框中的 "添加" 按钮后，Visual Web Developer 创建并打开了 "Index. cshtml" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="ce56c-132">下面显示了 Index 的内容。</span><span class="sxs-lookup"><span data-stu-id="ce56c-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="ce56c-133">此视图使用的是 Razor 语法，这比在 ASP.NET Web 窗体和 ASP.NET MVC 的以前版本中使用的 Web 窗体视图引擎更为简洁。</span><span class="sxs-lookup"><span data-stu-id="ce56c-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="ce56c-134">Web 窗体视图引擎在 ASP.NET MVC 3 中仍可用，但许多开发人员发现，Razor 视图引擎适用于 ASP.NET MVC 开发确实很好。</span><span class="sxs-lookup"><span data-stu-id="ce56c-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="ce56c-135">前三行使用 ViewBag 设置页面标题。</span><span class="sxs-lookup"><span data-stu-id="ce56c-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="ce56c-136">稍后我们将更详细地介绍此功能的工作原理，但首先我们来更新文本标题文本并查看该页。</span><span class="sxs-lookup"><span data-stu-id="ce56c-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="ce56c-137">将 &lt;h2&gt; 标记更新为 "这是主页"，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ce56c-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="ce56c-138">运行该应用程序时，会显示新文本显示在主页上。</span><span class="sxs-lookup"><span data-stu-id="ce56c-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="ce56c-139">使用通用网站元素的布局</span><span class="sxs-lookup"><span data-stu-id="ce56c-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="ce56c-140">大多数网站包含许多页面之间共享的内容：导航、页脚、徽标图像、样式表引用等。使用 Razor 视图引擎可以轻松地使用名为 \_Layout 的页面进行管理，该页面已在/Views/Shared 文件夹中自动创建。</span><span class="sxs-lookup"><span data-stu-id="ce56c-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="ce56c-141">双击此文件夹以查看内容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ce56c-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="ce56c-142">来自各个视图的内容将由 @RenderBody（）命令显示，并且我们希望在其外部显示的任何通用内容都可添加到 \_的布局。 cshtml 标记。</span><span class="sxs-lookup"><span data-stu-id="ce56c-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="ce56c-143">我们会希望我们的 MVC 音乐商店具有一个通用标头，其中包含指向主页的链接，并在站点中的所有页面上存储区域，因此，我们会将该标头添加到 @RenderBody（）语句前面的模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="ce56c-144">更新样式表</span><span class="sxs-lookup"><span data-stu-id="ce56c-144">Updating the StyleSheet</span></span>

<span data-ttu-id="ce56c-145">空项目模板包含一个非常简单的 CSS 文件，其中只包含用于显示验证消息的样式。</span><span class="sxs-lookup"><span data-stu-id="ce56c-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="ce56c-146">设计器还提供了一些其他 CSS 和图像来定义站点的外观，因此我们将在其中立即添加。</span><span class="sxs-lookup"><span data-stu-id="ce56c-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="ce56c-147">已更新的 CSS 文件和映像包含在 MvcMusicStore-Assets 的内容目录中，该目录可在[MVC-音乐存储](https://github.com/evilDave/MVC-Music-Store)中找到。</span><span class="sxs-lookup"><span data-stu-id="ce56c-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="ce56c-148">我们会在 Windows 资源管理器中选择这两个文件，并将其放在 Visual Web Developer 的解决方案内容文件夹中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ce56c-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="ce56c-149">系统会要求你确认是否要覆盖现有的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="ce56c-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="ce56c-150">单击“是”。</span><span class="sxs-lookup"><span data-stu-id="ce56c-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="ce56c-151">应用程序的内容文件夹现在如下所示：</span><span class="sxs-lookup"><span data-stu-id="ce56c-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="ce56c-152">现在，让我们运行应用程序，并查看主页上的更改的外观。</span><span class="sxs-lookup"><span data-stu-id="ce56c-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="ce56c-153">让我们回顾一下所做的更改： HomeController 的索引操作方法会找到并显示 \Views\Home\Index.cshtmlView 模板，尽管我们的视图模板遵循了标准命名约定，但我们的视图模板却是 "返回视图（）"。</span><span class="sxs-lookup"><span data-stu-id="ce56c-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="ce56c-154">主页正在显示在 \Views\Home\Index.cshtml 视图模板内定义的简单欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="ce56c-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="ce56c-155">主页正在使用我们的 \_布局 cshtml 模板，因此欢迎消息包含在标准网站 HTML 布局中。</span><span class="sxs-lookup"><span data-stu-id="ce56c-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="ce56c-156">使用模型将信息传递给我们的视图</span><span class="sxs-lookup"><span data-stu-id="ce56c-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="ce56c-157">只显示硬编码 HTML 的视图模板不会产生非常有趣的网站。</span><span class="sxs-lookup"><span data-stu-id="ce56c-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="ce56c-158">要创建动态网站，我们将改为将控制器操作的信息传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="ce56c-159">在 "模型-视图-控制器" 模式中，术语 "模型" 是指表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="ce56c-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="ce56c-160">通常，模型对象与数据库中的表相对应，但不一定要这样做。</span><span class="sxs-lookup"><span data-stu-id="ce56c-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="ce56c-161">返回 ActionResult 的控制器操作方法可以将模型对象传递到视图。</span><span class="sxs-lookup"><span data-stu-id="ce56c-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="ce56c-162">这样一来，控制器就可以将生成响应所需的所有信息完全打包，然后将此信息传递到一个视图模板以生成相应的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="ce56c-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="ce56c-163">通过查看其工作方式，可以更轻松地了解这一点，因此让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="ce56c-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="ce56c-164">首先，我们将创建一些模型类来表示商店中的流派和唱片集。</span><span class="sxs-lookup"><span data-stu-id="ce56c-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="ce56c-165">首先，让我们创建一个流派类。</span><span class="sxs-lookup"><span data-stu-id="ce56c-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="ce56c-166">右键单击项目中的 "模型" 文件夹，选择 "添加类" 选项，并将文件命名为 "Genre.cs"。</span><span class="sxs-lookup"><span data-stu-id="ce56c-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="ce56c-167">然后，将公共字符串名称属性添加到已创建的类：</span><span class="sxs-lookup"><span data-stu-id="ce56c-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="ce56c-168">*注意：如果您想知道，{get; set;} 表示法正在使用C#自动实现的属性功能。这为我们提供了属性的优点，而无需声明支持字段。*</span><span class="sxs-lookup"><span data-stu-id="ce56c-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="ce56c-169">接下来，请按照相同的步骤创建具有标题和流派属性的唱片集类（名为 Album.cs）：</span><span class="sxs-lookup"><span data-stu-id="ce56c-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="ce56c-170">现在，我们可以修改 StoreController，以使用显示模型中的动态信息的视图。</span><span class="sxs-lookup"><span data-stu-id="ce56c-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="ce56c-171">如果现在为-出于演示目的，我们根据请求 ID 命名了唱集，我们可以像下面的视图所示显示该信息。</span><span class="sxs-lookup"><span data-stu-id="ce56c-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="ce56c-172">首先，我们将更改存储详细信息操作，以便显示单个唱片集的信息。</span><span class="sxs-lookup"><span data-stu-id="ce56c-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="ce56c-173">在**StoreControllers**类的顶部添加一个 "using" 语句以包括 MvcMusicStore 命名空间，因此，每次使用唱片集类时，不需要键入 MvcMusicStore。</span><span class="sxs-lookup"><span data-stu-id="ce56c-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="ce56c-174">该类的 "using" 部分现在应如下所示。</span><span class="sxs-lookup"><span data-stu-id="ce56c-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="ce56c-175">接下来，我们将更新详细信息控制器操作，使其返回 ActionResult 而不是字符串，就像使用 HomeController 的 Index 方法时所做的一样。</span><span class="sxs-lookup"><span data-stu-id="ce56c-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="ce56c-176">现在，我们可以修改逻辑以将唱片集对象返回到视图中。</span><span class="sxs-lookup"><span data-stu-id="ce56c-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="ce56c-177">稍后在本教程中，我们将从数据库中检索数据，但现在，我们将使用 "虚拟数据" 开始使用。</span><span class="sxs-lookup"><span data-stu-id="ce56c-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="ce56c-178">*注意：如果不熟悉C#，则可以假设使用 var 表示我们的唱集变量为后期绑定。这不是正确的– C#编译器将根据我们分配给变量的内容来使用类型推理来确定唱片集属于唱片集类型，并将本地唱片集变量编译为唱片集类型，因此我们将获得编译时检查和 Visual Studio 代码编辑器支持。*</span><span class="sxs-lookup"><span data-stu-id="ce56c-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="ce56c-179">现在，让我们创建一个使用唱片集生成 HTML 响应的视图模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="ce56c-180">在执行此操作之前，我们需要生成项目，以便 "添加视图" 对话框知道我们新创建的唱集类。</span><span class="sxs-lookup"><span data-stu-id="ce56c-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="ce56c-181">可以通过选择 "调试⇨生成 MvcMusicStore" 菜单项来生成项目（为实现额外信用，可以使用 Ctrl + Shift-B 快捷方式生成项目）。</span><span class="sxs-lookup"><span data-stu-id="ce56c-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="ce56c-182">现在我们已经设置了支持类，接下来可以构建视图模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="ce56c-183">右键单击详细信息方法，然后选择 "添加视图 ..."从上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="ce56c-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="ce56c-184">我们将创建一个新的视图模板，就像我们在使用 HomeController 之前做的一样。</span><span class="sxs-lookup"><span data-stu-id="ce56c-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="ce56c-185">由于我们是从 StoreController 创建它，因此默认情况下将在 \Views\Store\Index.cshtml 文件中生成它。</span><span class="sxs-lookup"><span data-stu-id="ce56c-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="ce56c-186">与之前不同，我们将选中 "创建强类型的视图" 复选框。</span><span class="sxs-lookup"><span data-stu-id="ce56c-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="ce56c-187">接下来，我们将在 "查看数据类" 下拉 downlist 中选择 "唱片集" 类。</span><span class="sxs-lookup"><span data-stu-id="ce56c-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="ce56c-188">这将导致 "添加视图" 对话框创建一个需要将唱片集对象传递到其使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="ce56c-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="ce56c-189">单击 "添加" 按钮时，将创建 \Views\Store\Details.cshtml 视图模板，其中包含以下代码。</span><span class="sxs-lookup"><span data-stu-id="ce56c-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="ce56c-190">请注意第一行，它指示此视图已强类型化到我们的唱片集类中。</span><span class="sxs-lookup"><span data-stu-id="ce56c-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="ce56c-191">Razor 视图引擎了解它已传递一个唱片集对象，因此我们可以轻松地访问模型属性，甚至可以在 Visual Web Developer 编辑器中获得 IntelliSense 的好处。</span><span class="sxs-lookup"><span data-stu-id="ce56c-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="ce56c-192">更新 &lt;h2&gt; 标记，使其显示唱片集的 Title 属性，方法是将该行修改为如下所示。</span><span class="sxs-lookup"><span data-stu-id="ce56c-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="ce56c-193">请注意，在输入 @Model 关键字之后的时间段时，将触发 IntelliSense，其中显示了唱片集类支持的属性和方法。</span><span class="sxs-lookup"><span data-stu-id="ce56c-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="ce56c-194">现在，让我们重新运行项目并访问/Store/Details/5 URL。</span><span class="sxs-lookup"><span data-stu-id="ce56c-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="ce56c-195">我们将看到如下唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ce56c-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="ce56c-196">现在，我们将对 "存储浏览" 操作方法进行类似更新。</span><span class="sxs-lookup"><span data-stu-id="ce56c-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="ce56c-197">更新方法，使其返回 ActionResult，并修改方法逻辑，使其创建新的流派对象并将其返回给视图。</span><span class="sxs-lookup"><span data-stu-id="ce56c-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="ce56c-198">右键单击浏览方法，然后选择 "添加视图 ..."在上下文菜单中，添加一个强类型的视图，将强类型化添加到流派类中。</span><span class="sxs-lookup"><span data-stu-id="ce56c-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="ce56c-199">更新视图代码中的 &lt;h2&gt; 元素（在/Views/Store/Browse.cshtml 中）以显示流派信息。</span><span class="sxs-lookup"><span data-stu-id="ce56c-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="ce56c-200">现在，让我们重新运行项目并浏览到/Store/Browse？流派 = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="ce56c-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="ce56c-201">我们会看到如下所示的浏览页。</span><span class="sxs-lookup"><span data-stu-id="ce56c-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="ce56c-202">最后，让我们对**商店索引**操作方法和视图进行稍微复杂的更新，以显示我们的商店中所有流派的列表。</span><span class="sxs-lookup"><span data-stu-id="ce56c-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="ce56c-203">我们将使用流派列表作为模型对象，而不只是使用单个流派来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="ce56c-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="ce56c-204">右键单击 "存储索引" 操作方法，然后选择 "添加视图"，选择 "流派" 作为模型类，并按 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ce56c-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="ce56c-205">首先，我们将更改 @model 声明，以指示该视图将需要多个流派对象，而不只是一个。</span><span class="sxs-lookup"><span data-stu-id="ce56c-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="ce56c-206">更改/Store/Index.cshtml 的第一行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ce56c-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="ce56c-207">这会告诉 Razor 视图引擎它将使用可以容纳多个流派对象的模型对象。</span><span class="sxs-lookup"><span data-stu-id="ce56c-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="ce56c-208">我们使用的是 IEnumerable&lt;流派&gt; 而不是&lt;流派&gt; 列表，因为它更通用，使我们能够将模型类型以后更改为支持 IEnumerable 接口的任何对象类型。</span><span class="sxs-lookup"><span data-stu-id="ce56c-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="ce56c-209">接下来，我们将遍历模型中的流派对象，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ce56c-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="ce56c-210">请注意，我们在输入此代码时具有完全的 IntelliSense 支持，因此，在我们输入 "@Model" 时。</span><span class="sxs-lookup"><span data-stu-id="ce56c-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="ce56c-211">我们看到类型为 "流派" 的 IEnumerable 支持的所有方法和属性。</span><span class="sxs-lookup"><span data-stu-id="ce56c-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="ce56c-212">在我们的 "foreach" 循环中，Visual Web Developer 知道每个项的类型为 "流派"，因此我们会看到每个流派类型的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ce56c-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="ce56c-213">接下来，基架功能检查了流派对象，并确定每个对象都有一个 Name 属性，以便循环访问并将其写入。它还会生成每个单独项的编辑、详细信息和删除链接。</span><span class="sxs-lookup"><span data-stu-id="ce56c-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="ce56c-214">我们稍后会在我们的商店经理中利用这一点，但现在，我们想要创建一个简单的列表。</span><span class="sxs-lookup"><span data-stu-id="ce56c-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="ce56c-215">当我们运行该应用程序并浏览到/Store 时，我们看到显示了 "计数" 和 "流派列表"。</span><span class="sxs-lookup"><span data-stu-id="ce56c-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="ce56c-216">在页面之间添加链接</span><span class="sxs-lookup"><span data-stu-id="ce56c-216">Adding Links between pages</span></span>

<span data-ttu-id="ce56c-217">当前列出流派的/Store URL 仅以纯文本形式列出流派名称。</span><span class="sxs-lookup"><span data-stu-id="ce56c-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="ce56c-218">让我们对此进行更改，而不是将纯文本改为将流派名称链接到相应的/Store/Browse URL，这样，单击类似于 "Disco" 的音乐流派就会导航到/Store/Browse？流派 = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="ce56c-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="ce56c-219">我们可以使用类似下面的代码更新 \Views\Store\Index.cshtml 视图模板来输出这些链接 **（不要在此中进行改进）** ：</span><span class="sxs-lookup"><span data-stu-id="ce56c-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="ce56c-220">这种方法很有效，但可能会在以后出现问题，因为它依赖于硬编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="ce56c-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="ce56c-221">例如，如果我们要重命名控制器，则需要在代码中搜索，查找需要更新的链接。</span><span class="sxs-lookup"><span data-stu-id="ce56c-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="ce56c-222">可使用的替代方法是利用 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="ce56c-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="ce56c-223">ASP.NET MVC 包含 HTML Helper 方法，这些方法可从我们的查看模板代码中使用，以执行与此类似的各种常见任务。</span><span class="sxs-lookup"><span data-stu-id="ce56c-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="ce56c-224">.Html （） helper 方法非常有用，可轻松生成 HTML &lt;&gt; 链接，并处理令人讨厌的详细信息，例如确保 URL 路径正确地进行 URL 编码。</span><span class="sxs-lookup"><span data-stu-id="ce56c-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="ce56c-225">Html.actionlink （）具有多个不同的重载，以允许为你的链接指定尽可能多的信息。</span><span class="sxs-lookup"><span data-stu-id="ce56c-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="ce56c-226">最简单的情况是，在客户端上单击超链接时，将只提供链接文本和操作方法。</span><span class="sxs-lookup"><span data-stu-id="ce56c-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="ce56c-227">例如，我们可以使用以下调用链接到存储详细信息页上的 "/Store/" 索引（）方法和链接文本 "中转到存储索引"：</span><span class="sxs-lookup"><span data-stu-id="ce56c-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="ce56c-228">*注意：在这种情况下，我们不需要指定控制器名称，因为我们只链接到呈现当前视图的同一控制器中的其他操作。*</span><span class="sxs-lookup"><span data-stu-id="ce56c-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="ce56c-229">但指向浏览页的链接将需要传递参数，因此，我们将使用采用三个参数的 Html.actionlink 方法的另一个重载：</span><span class="sxs-lookup"><span data-stu-id="ce56c-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="ce56c-230">链接文本，将显示流派名称</span><span class="sxs-lookup"><span data-stu-id="ce56c-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="ce56c-231">控制器操作名称（浏览）</span><span class="sxs-lookup"><span data-stu-id="ce56c-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="ce56c-232">路由参数值，同时指定名称（流派）和值（流派名称）</span><span class="sxs-lookup"><span data-stu-id="ce56c-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="ce56c-233">将这些内容放在一起，下面介绍了如何将这些链接写入商店索引视图：</span><span class="sxs-lookup"><span data-stu-id="ce56c-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="ce56c-234">现在，当我们再次运行项目并访问/Store/URL 时，我们将看到一个流派列表。</span><span class="sxs-lookup"><span data-stu-id="ce56c-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="ce56c-235">每个流派均为超链接–单击此项时，将转到我们的/Store/Browse？流派 = *[流派]* URL。</span><span class="sxs-lookup"><span data-stu-id="ce56c-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="ce56c-236">流派列表的 HTML 如下所示：</span><span class="sxs-lookup"><span data-stu-id="ce56c-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="ce56c-237">[上一页](mvc-music-store-part-2.md)
> [下一页](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="ce56c-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
