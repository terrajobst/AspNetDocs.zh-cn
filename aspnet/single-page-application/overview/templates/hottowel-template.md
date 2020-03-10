---
uid: single-page-application/overview/templates/hottowel-template
title: 热的纸巾模板 |Microsoft Docs
author: madskristensen
description: HotTowel 模板
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467138"
---
# <a name="hot-towel-template"></a><span data-ttu-id="90ee7-103">Hot Towel 模板</span><span class="sxs-lookup"><span data-stu-id="90ee7-103">Hot Towel template</span></span>

<span data-ttu-id="90ee7-104">作者： [Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="90ee7-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="90ee7-105">Papa 作者编写的</span><span class="sxs-lookup"><span data-stu-id="90ee7-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="90ee7-106">选择要下载的版本：</span><span class="sxs-lookup"><span data-stu-id="90ee7-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="90ee7-107">适用于 Visual Studio 2012 的热式纸巾 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="90ee7-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="90ee7-108">Visual Studio 2013 的热的纸巾 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="90ee7-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="90ee7-109">热的，因为你不希望再转向 SPA！</span><span class="sxs-lookup"><span data-stu-id="90ee7-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="90ee7-110">想要生成 SPA，但不能决定从何处开始？</span><span class="sxs-lookup"><span data-stu-id="90ee7-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="90ee7-111">使用热的纸巾，以秒为单位，你将拥有一个 SPA 和构建所需的所有工具。</span><span class="sxs-lookup"><span data-stu-id="90ee7-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="90ee7-112">"ASP.NET" 创建了一个很好的起点。</span><span class="sxs-lookup"><span data-stu-id="90ee7-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="90ee7-113">这种情况下，它为代码提供了模块化结构，可查看导航、数据绑定、丰富的数据管理以及简单而精致的样式。</span><span class="sxs-lookup"><span data-stu-id="90ee7-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="90ee7-114">热向下提供了构建 SPA 所需的一切，使你可以专注于应用，而不是管道。</span><span class="sxs-lookup"><span data-stu-id="90ee7-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="90ee7-115">详细了解如何从[John Papa 的视频、教程和 Pluralsight 课程](http://johnpapa.net/spa?vsix)构建 SPA。</span><span class="sxs-lookup"><span data-stu-id="90ee7-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="90ee7-116">应用程序结构</span><span class="sxs-lookup"><span data-stu-id="90ee7-116">Application Structure</span></span>

<span data-ttu-id="90ee7-117">"热的纸巾 SPA" 提供了一个应用文件夹，其中包含定义应用程序的 JavaScript 和 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="90ee7-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="90ee7-118">在 App 文件夹内：</span><span class="sxs-lookup"><span data-stu-id="90ee7-118">Inside the App folder:</span></span>

- <span data-ttu-id="90ee7-119">durandal</span><span class="sxs-lookup"><span data-stu-id="90ee7-119">durandal</span></span>
- <span data-ttu-id="90ee7-120">服务</span><span class="sxs-lookup"><span data-stu-id="90ee7-120">services</span></span>
- <span data-ttu-id="90ee7-121">viewmodel</span><span class="sxs-lookup"><span data-stu-id="90ee7-121">viewmodels</span></span>
- <span data-ttu-id="90ee7-122">视图</span><span class="sxs-lookup"><span data-stu-id="90ee7-122">views</span></span>

<span data-ttu-id="90ee7-123">应用文件夹包含模块的集合。</span><span class="sxs-lookup"><span data-stu-id="90ee7-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="90ee7-124">这些模块封装了功能并声明了其他模块上的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="90ee7-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="90ee7-125">Views 文件夹包含应用程序的 HTML，viewmodel 文件夹包含视图的表示逻辑（一种公共 MVVM 模式）。</span><span class="sxs-lookup"><span data-stu-id="90ee7-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="90ee7-126">"服务" 文件夹非常适合用于容纳应用程序可能需要的任何常用服务，例如 HTTP 数据检索或本地存储交互。</span><span class="sxs-lookup"><span data-stu-id="90ee7-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="90ee7-127">多个 viewmodel 经常从服务模块重用代码。</span><span class="sxs-lookup"><span data-stu-id="90ee7-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="90ee7-128">ASP.NET MVC 服务器端应用程序结构</span><span class="sxs-lookup"><span data-stu-id="90ee7-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="90ee7-129">《热版，在熟悉且功能强大的 ASP.NET MVC 结构上构建。</span><span class="sxs-lookup"><span data-stu-id="90ee7-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="90ee7-130">应用\_启动</span><span class="sxs-lookup"><span data-stu-id="90ee7-130">App\_Start</span></span>
- <span data-ttu-id="90ee7-131">内容</span><span class="sxs-lookup"><span data-stu-id="90ee7-131">Content</span></span>
- <span data-ttu-id="90ee7-132">Controllers</span><span class="sxs-lookup"><span data-stu-id="90ee7-132">Controllers</span></span>
- <span data-ttu-id="90ee7-133">模型</span><span class="sxs-lookup"><span data-stu-id="90ee7-133">Models</span></span>
- <span data-ttu-id="90ee7-134">脚本</span><span class="sxs-lookup"><span data-stu-id="90ee7-134">Scripts</span></span>
- <span data-ttu-id="90ee7-135">视图</span><span class="sxs-lookup"><span data-stu-id="90ee7-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="90ee7-136">特色库</span><span class="sxs-lookup"><span data-stu-id="90ee7-136">Featured Libraries</span></span>

- <span data-ttu-id="90ee7-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="90ee7-137">ASP.NET MVC</span></span>
- <span data-ttu-id="90ee7-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="90ee7-138">ASP.NET Web API</span></span>
- <span data-ttu-id="90ee7-139">ASP.NET Web 优化-捆绑和缩减</span><span class="sxs-lookup"><span data-stu-id="90ee7-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="90ee7-140">简单的[.js](http://Breezejs.com) -丰富的数据管理</span><span class="sxs-lookup"><span data-stu-id="90ee7-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="90ee7-141">[Durandal](http://Durandaljs.com) -导航和查看组合</span><span class="sxs-lookup"><span data-stu-id="90ee7-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="90ee7-142">[挖空](http://Knockoutjs.com)的数据绑定</span><span class="sxs-lookup"><span data-stu-id="90ee7-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="90ee7-143">[要求 .js](http://requirejs.org) -具有 AMD 和优化的模块化</span><span class="sxs-lookup"><span data-stu-id="90ee7-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="90ee7-144">[Toastr](http://jpapa.me/c7toastr) -弹出消息</span><span class="sxs-lookup"><span data-stu-id="90ee7-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="90ee7-145">[Twitter 引导](https://twitter.github.com/bootstrap/)-强健的 CSS 样式</span><span class="sxs-lookup"><span data-stu-id="90ee7-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="90ee7-146">通过 Visual Studio 2012 热视频 SPA 模板进行安装</span><span class="sxs-lookup"><span data-stu-id="90ee7-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="90ee7-147">可以将热式安装为 Visual Studio 2012 模板。</span><span class="sxs-lookup"><span data-stu-id="90ee7-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="90ee7-148">只需单击 "`File` | " `New Project` 并选择 "`ASP.NET MVC 4 Web Application`"。</span><span class="sxs-lookup"><span data-stu-id="90ee7-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="90ee7-149">然后选择 "热的单页面应用程序" 模板并运行！</span><span class="sxs-lookup"><span data-stu-id="90ee7-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="90ee7-150">通过 NuGet 包安装</span><span class="sxs-lookup"><span data-stu-id="90ee7-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="90ee7-151">ASP.NET 也是一个 NuGet 包，用于补充现有的空的 MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="90ee7-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="90ee7-152">只需使用 Nuget 安装，然后运行！</span><span class="sxs-lookup"><span data-stu-id="90ee7-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="90ee7-153">如何在 ws-i 上构建？</span><span class="sxs-lookup"><span data-stu-id="90ee7-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="90ee7-154">只需开始添加代码！</span><span class="sxs-lookup"><span data-stu-id="90ee7-154">Simply start adding code!</span></span>

1. <span data-ttu-id="90ee7-155">添加自己的服务器端代码，最好是实体框架和 WebAPI （这与）</span><span class="sxs-lookup"><span data-stu-id="90ee7-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="90ee7-156">将视图添加到 `App/views` 文件夹</span><span class="sxs-lookup"><span data-stu-id="90ee7-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="90ee7-157">将 viewmodel 添加到 `App/viewmodels` 文件夹</span><span class="sxs-lookup"><span data-stu-id="90ee7-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="90ee7-158">将 HTML 和挖空数据绑定添加到新视图</span><span class="sxs-lookup"><span data-stu-id="90ee7-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="90ee7-159">更新中的导航路由 `shell.js`</span><span class="sxs-lookup"><span data-stu-id="90ee7-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="90ee7-160">HTML/JavaScript 演练</span><span class="sxs-lookup"><span data-stu-id="90ee7-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="90ee7-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="90ee7-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="90ee7-162">索引为 MVC 应用程序的起始路由和视图。</span><span class="sxs-lookup"><span data-stu-id="90ee7-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="90ee7-163">它包含所需的所有标准 meta 标记、css 链接和 JavaScript 引用。</span><span class="sxs-lookup"><span data-stu-id="90ee7-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="90ee7-164">正文包含单个 `<div>`，其中的所有内容（你的视图）都将在请求时放置。</span><span class="sxs-lookup"><span data-stu-id="90ee7-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="90ee7-165">`@Scripts.Render` 使用需要 node.js 来运行应用程序代码的入口点，它包含在 `main.js` 文件中。</span><span class="sxs-lookup"><span data-stu-id="90ee7-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="90ee7-166">提供了一个初始屏幕，用于演示如何在应用程序加载时创建初始屏幕。</span><span class="sxs-lookup"><span data-stu-id="90ee7-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="90ee7-167">App/main.js</span><span class="sxs-lookup"><span data-stu-id="90ee7-167">App/main.js</span></span>

<span data-ttu-id="90ee7-168">`main.js` 文件包含将在你的应用程序加载后立即运行的代码。</span><span class="sxs-lookup"><span data-stu-id="90ee7-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="90ee7-169">这是要在其中定义导航路由、设置启动视图和执行任何安装程序/引导（如填充应用程序的数据）的位置。</span><span class="sxs-lookup"><span data-stu-id="90ee7-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="90ee7-170">`main.js` 文件定义了 durandal 的多个模块，以帮助应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="90ee7-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="90ee7-171">Define 语句可帮助解析模块依赖项，以便它们可用于函数。</span><span class="sxs-lookup"><span data-stu-id="90ee7-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="90ee7-172">首先启用了调试消息，这会将有关应用程序正在执行的事件的消息发送到控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="90ee7-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="90ee7-173">Durandal 框架用于启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="90ee7-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="90ee7-174">设置约定，以便 durandal 知道所有视图和 viewmodel 分别包含在相同的命名文件夹中。</span><span class="sxs-lookup"><span data-stu-id="90ee7-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="90ee7-175">最后，`app.setRoot` 启动使用预定义 `entrance` 动画加载 `shell`。</span><span class="sxs-lookup"><span data-stu-id="90ee7-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="90ee7-176">视图</span><span class="sxs-lookup"><span data-stu-id="90ee7-176">Views</span></span>

<span data-ttu-id="90ee7-177">视图位于 `App/views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="90ee7-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="90ee7-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="90ee7-178">shell.html</span></span>

<span data-ttu-id="90ee7-179">`shell.html` 包含 HTML 的母版布局。</span><span class="sxs-lookup"><span data-stu-id="90ee7-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="90ee7-180">你的所有其他视图将在你的 `shell` 视图的某个地方组合在一起。</span><span class="sxs-lookup"><span data-stu-id="90ee7-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="90ee7-181">"热 `shell`" 提供了包含三个这类区域的：页眉、内容区域和页脚。</span><span class="sxs-lookup"><span data-stu-id="90ee7-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="90ee7-182">在请求时，其中的每个区域都将与其他视图的内容一起加载。</span><span class="sxs-lookup"><span data-stu-id="90ee7-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="90ee7-183">标头和表尾的 `compose` 绑定将分别指向 `nav` 和 `footer` 视图。</span><span class="sxs-lookup"><span data-stu-id="90ee7-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="90ee7-184">`#content` 节的撰写绑定绑定到 `router` 模块的活动项。</span><span class="sxs-lookup"><span data-stu-id="90ee7-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="90ee7-185">换句话说，单击导航链接时，将在此区域中加载其对应的视图。</span><span class="sxs-lookup"><span data-stu-id="90ee7-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="90ee7-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="90ee7-186">nav.html</span></span>

<span data-ttu-id="90ee7-187">`nav.html` 包含 SPA 的导航链接。</span><span class="sxs-lookup"><span data-stu-id="90ee7-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="90ee7-188">例如，可以在此处放置菜单结构。</span><span class="sxs-lookup"><span data-stu-id="90ee7-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="90ee7-189">这通常是数据绑定（使用挖空）到 `router` 模块，以显示在 `shell.js`中定义的导航。</span><span class="sxs-lookup"><span data-stu-id="90ee7-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="90ee7-190">挖空会查找数据绑定属性，并将其绑定到 `shell` viewmodel 以显示导航路由，并将其绑定到 `router` 模块处于从一个视图导航到另一个视图（请参阅 `router.isNavigating`）的情况。</span><span class="sxs-lookup"><span data-stu-id="90ee7-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="90ee7-191">home. html 和详细信息</span><span class="sxs-lookup"><span data-stu-id="90ee7-191">home.html and details.html</span></span>

<span data-ttu-id="90ee7-192">这些视图包含用于自定义视图的 HTML。</span><span class="sxs-lookup"><span data-stu-id="90ee7-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="90ee7-193">单击 "`nav` 视图" 菜单中的 "`home`" 链接时，将在 "`shell`" 视图的 "内容" 区域中放置 `home` 视图。</span><span class="sxs-lookup"><span data-stu-id="90ee7-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="90ee7-194">可以扩充这些视图或将其替换为你自己的自定义视图。</span><span class="sxs-lookup"><span data-stu-id="90ee7-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="90ee7-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="90ee7-195">footer.html</span></span>

<span data-ttu-id="90ee7-196">`footer.html` 包含在 `shell` 视图底部的脚注中显示的 HTML。</span><span class="sxs-lookup"><span data-stu-id="90ee7-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="90ee7-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="90ee7-197">ViewModels</span></span>

<span data-ttu-id="90ee7-198">在 `App/viewmodels` 文件夹中找到 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="90ee7-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="90ee7-199">shell.js</span><span class="sxs-lookup"><span data-stu-id="90ee7-199">shell.js</span></span>

<span data-ttu-id="90ee7-200">`shell` viewmodel 包含绑定到 `shell` 视图的属性和函数。</span><span class="sxs-lookup"><span data-stu-id="90ee7-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="90ee7-201">这通常是在其中找到菜单导航绑定的位置（请参阅 `router.mapNav` 逻辑）。</span><span class="sxs-lookup"><span data-stu-id="90ee7-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="90ee7-202">node.js 和详细信息</span><span class="sxs-lookup"><span data-stu-id="90ee7-202">home.js and details.js</span></span>

<span data-ttu-id="90ee7-203">这些 viewmodel 包含绑定到 `home` 视图的属性和函数。</span><span class="sxs-lookup"><span data-stu-id="90ee7-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="90ee7-204">它还包含视图的呈现逻辑，是数据和视图之间的粘附。</span><span class="sxs-lookup"><span data-stu-id="90ee7-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="90ee7-205">服务</span><span class="sxs-lookup"><span data-stu-id="90ee7-205">Services</span></span>

<span data-ttu-id="90ee7-206">服务位于 "应用/服务" 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="90ee7-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="90ee7-207">理想情况下，您可以将将来的服务（如 dataservice 模块）用于获取和发布远程数据。</span><span class="sxs-lookup"><span data-stu-id="90ee7-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="90ee7-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="90ee7-208">logger.js</span></span>

<span data-ttu-id="90ee7-209">"暖色" 在 "服务" 文件夹中提供 `logger` 模块。</span><span class="sxs-lookup"><span data-stu-id="90ee7-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="90ee7-210">`logger` 模块非常适合用于将消息记录到控制台和弹出 toast 中的用户。</span><span class="sxs-lookup"><span data-stu-id="90ee7-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
