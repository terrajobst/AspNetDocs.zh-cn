---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 添加视图（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458182"
---
# <a name="adding-a-view-c"></a><span data-ttu-id="98d87-103">添加视图 (C#)</span><span class="sxs-lookup"><span data-stu-id="98d87-103">Adding a View (C#)</span></span>

<span data-ttu-id="98d87-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="98d87-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="98d87-105">[此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="98d87-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="98d87-106">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="98d87-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="98d87-107">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="98d87-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="98d87-108">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="98d87-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="98d87-109">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="98d87-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="98d87-110">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="98d87-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="98d87-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="98d87-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="98d87-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="98d87-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="98d87-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="98d87-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="98d87-114">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="98d87-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="98d87-115">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="98d87-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="98d87-116">[下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="98d87-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="98d87-117">如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="98d87-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="98d87-118">在本节中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。</span><span class="sxs-lookup"><span data-stu-id="98d87-118">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="98d87-119">你将使用 ASP.NET MVC 3 中引入的新的[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)创建视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="98d87-119">You'll create a view template file using the new [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="98d87-120">基于 Razor 的视图模板的文件扩展名为*cshtml* ，并提供使用C#创建 HTML 输出的简洁方法。</span><span class="sxs-lookup"><span data-stu-id="98d87-120">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="98d87-121">Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。</span><span class="sxs-lookup"><span data-stu-id="98d87-121">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="98d87-122">首先将视图模板与 `HelloWorldController` 类中的 `Index` 方法一起使用。</span><span class="sxs-lookup"><span data-stu-id="98d87-122">Start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="98d87-123">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="98d87-123">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="98d87-124">更改 `Index` 方法以返回 `View` 对象，如下所示：</span><span class="sxs-lookup"><span data-stu-id="98d87-124">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="98d87-125">此代码使用视图模板生成浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="98d87-125">This code uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="98d87-126">在项目中，添加可与 `Index` 方法一起使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="98d87-126">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="98d87-127">为此，请在 `Index` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="98d87-127">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="98d87-128">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="98d87-128">The **Add View** dialog box appears.</span></span> <span data-ttu-id="98d87-129">保留默认值，并单击 "**添加**" 按钮：</span><span class="sxs-lookup"><span data-stu-id="98d87-129">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="98d87-130">将创建*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="98d87-130">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="98d87-131">可以在**解决方案资源管理器**中查看它们：</span><span class="sxs-lookup"><span data-stu-id="98d87-131">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="98d87-132">下面显示了已创建的*索引 cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="98d87-132">The following shows the *Index.cshtml* file that was created:</span></span>

<span data-ttu-id="98d87-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="98d87-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span></span>

<span data-ttu-id="98d87-134">在 `<h2>` 标记下添加一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="98d87-134">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="98d87-135">修改后的*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="98d87-135">The modified *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

<span data-ttu-id="98d87-136">运行应用程序并浏览到 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="98d87-136">Run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="98d87-137">控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，该语句指定方法应使用视图模板文件来呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="98d87-137">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="98d87-138">由于未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 *\Views\HelloWorld*文件夹中的*视图文件。*</span><span class="sxs-lookup"><span data-stu-id="98d87-138">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="98d87-139">下图显示了视图中硬编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="98d87-139">The image below shows the string hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="98d87-140">看起来不错。</span><span class="sxs-lookup"><span data-stu-id="98d87-140">Looks pretty good.</span></span> <span data-ttu-id="98d87-141">但请注意，浏览器的标题栏显示 "索引"，而页面上的大标题显示为 "我的 MVC 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="98d87-141">However, notice that the browser's title bar says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="98d87-142">让我们更改这些。</span><span class="sxs-lookup"><span data-stu-id="98d87-142">Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="98d87-143">更改视图和布局页</span><span class="sxs-lookup"><span data-stu-id="98d87-143">Changing Views and Layout Pages</span></span>

<span data-ttu-id="98d87-144">首先，您需要更改页面顶部的 "我的 MVC 应用程序" 标题。</span><span class="sxs-lookup"><span data-stu-id="98d87-144">First, you want to change the "My MVC Application" title at the top of the page.</span></span> <span data-ttu-id="98d87-145">该文本对于每个页面都是通用的。</span><span class="sxs-lookup"><span data-stu-id="98d87-145">That text is common to every page.</span></span> <span data-ttu-id="98d87-146">它实际上只在项目中的一个位置实现，即使它显示在应用程序中的每一页上也是如此。</span><span class="sxs-lookup"><span data-stu-id="98d87-146">It actually is implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="98d87-147">中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 *\_的布局 cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="98d87-147">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="98d87-148">此文件称为*布局页面*，它是所有其他页面都使用的共享 "shell"。</span><span class="sxs-lookup"><span data-stu-id="98d87-148">This file is called a *layout page* and it's the shared "shell" that all other pages use.</span></span>

<span data-ttu-id="98d87-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="98d87-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="98d87-150">布局模板允许在一个位置指定网站的 HTML 容器布局，然后将其应用到站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="98d87-150">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="98d87-151">请注意文件底部附近的 `@RenderBody()` 行。</span><span class="sxs-lookup"><span data-stu-id="98d87-151">Note the `@RenderBody()` line near the bottom of the file.</span></span> <span data-ttu-id="98d87-152">`RenderBody` 是一个占位符，其中所创建的所有视图特定页面都显示在 "布局" 页中的 "已包装"。</span><span class="sxs-lookup"><span data-stu-id="98d87-152">`RenderBody` is a placeholder where all the view-specific pages you create show up, "wrapped" in the layout page.</span></span> <span data-ttu-id="98d87-153">将布局模板中的标题标题从 "我的 MVC 应用程序" 更改为 "MVC 电影应用"。</span><span class="sxs-lookup"><span data-stu-id="98d87-153">Change the title heading in the layout template from "My MVC Application" to "MVC Movie App".</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

<span data-ttu-id="98d87-154">运行该应用程序，请注意，它现在显示 "MVC 电影应用"。</span><span class="sxs-lookup"><span data-stu-id="98d87-154">Run the application and notice that it now says "MVC Movie App".</span></span> <span data-ttu-id="98d87-155">单击 "**关于**" 链接，你将看到该页面还显示 "MVC 电影应用"。</span><span class="sxs-lookup"><span data-stu-id="98d87-155">Click the **About** link, and you see how that page shows "MVC Movie App", too.</span></span> <span data-ttu-id="98d87-156">我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="98d87-156">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="98d87-157">完整的 *\_布局 cshtml*文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="98d87-157">The complete *\_Layout.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="98d87-158">现在，让我们更改索引页（视图）的标题。</span><span class="sxs-lookup"><span data-stu-id="98d87-158">Now, let's change the title of the Index page (view).</span></span>

<span data-ttu-id="98d87-159">打开*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="98d87-159">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="98d87-160">有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。</span><span class="sxs-lookup"><span data-stu-id="98d87-160">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="98d87-161">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="98d87-161">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="98d87-162">若要指示要显示的 HTML 标题，上面的代码将设置 `ViewBag` 对象（在*索引. cshtml*视图模板中）的 `Title` 属性。</span><span class="sxs-lookup"><span data-stu-id="98d87-162">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="98d87-163">如果你查看布局模板的源代码，你会注意到，模板在 HTML 的 `<head>` 部分中使用 `<title>` 元素中的此值。</span><span class="sxs-lookup"><span data-stu-id="98d87-163">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML.</span></span> <span data-ttu-id="98d87-164">使用此方法，您可以轻松地在视图模板和布局文件之间传递其他参数。</span><span class="sxs-lookup"><span data-stu-id="98d87-164">Using this approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="98d87-165">运行应用程序并浏览到 `http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="98d87-165">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="98d87-166">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="98d87-166">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="98d87-167">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="98d87-167">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="98d87-168">在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）</span><span class="sxs-lookup"><span data-stu-id="98d87-168">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="98d87-169">另请注意， *Index.* view 模板中的内容是如何与 *\_Layout*视图模板合并的，并向浏览器发送单个 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="98d87-169">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="98d87-170">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="98d87-170">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="98d87-171">但我们这一点点“数据”（在此示例中为“Hello from our View Template!”</span><span class="sxs-lookup"><span data-stu-id="98d87-171">Our little bit of "data" (in this case the "Hello from our View Template!"</span></span> <span data-ttu-id="98d87-172">消息）是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="98d87-172">message) is hard-coded, though.</span></span> <span data-ttu-id="98d87-173">MVC 应用程序有一个“V”（视图），而你已有一个“C”（控制器），但还没有“M”（模型）。</span><span class="sxs-lookup"><span data-stu-id="98d87-173">The MVC application has a "V" (view) and you've got a "C" (controller), but no "M" (model) yet.</span></span> <span data-ttu-id="98d87-174">稍后，我们将逐步介绍如何创建数据库并从该数据库中检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="98d87-174">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="98d87-175">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="98d87-175">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="98d87-176">不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="98d87-176">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="98d87-177">为了响应传入 URL 请求，将调用控制器类。</span><span class="sxs-lookup"><span data-stu-id="98d87-177">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="98d87-178">控制器类用于编写处理传入参数的代码、从数据库检索数据，并最终决定要发送回浏览器的响应类型。</span><span class="sxs-lookup"><span data-stu-id="98d87-178">A controller class is where you write the code that handles the incoming parameters, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="98d87-179">然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="98d87-179">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="98d87-180">控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="98d87-180">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="98d87-181">视图模板不应执行业务逻辑或直接与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="98d87-181">A view template should never perform business logic or interact with a database directly.</span></span> <span data-ttu-id="98d87-182">相反，它应仅适用于控制器为其提供的数据。</span><span class="sxs-lookup"><span data-stu-id="98d87-182">Instead, it should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="98d87-183">维护这种 "问题分离" 有助于使代码更干净且更易维护。</span><span class="sxs-lookup"><span data-stu-id="98d87-183">Maintaining this "separation of concerns" helps keep your code clean and more maintainable.</span></span>

<span data-ttu-id="98d87-184">当前，`HelloWorldController` 类中的 `Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="98d87-184">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="98d87-185">不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="98d87-185">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="98d87-186">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="98d87-186">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="98d87-187">为此，可以让控制器将视图模板所需的动态数据放置在视图模板可以访问 `ViewBag` 对象中。</span><span class="sxs-lookup"><span data-stu-id="98d87-187">You can do this by having the controller put the dynamic data that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="98d87-188">返回到*HelloWorldController.cs*文件，更改 `Welcome` 方法，将 `Message` 和 `NumTimes` 值添加到 `ViewBag` 对象。</span><span class="sxs-lookup"><span data-stu-id="98d87-188">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="98d87-189">`ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中：在将对象放入其中之前，`ViewBag` 对象没有定义的属性。</span><span class="sxs-lookup"><span data-stu-id="98d87-189">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="98d87-190">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="98d87-190">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

<span data-ttu-id="98d87-191">现在 `ViewBag` 对象包含将自动传递到该视图的数据。</span><span class="sxs-lookup"><span data-stu-id="98d87-191">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="98d87-192">接下来，需要一个欢迎视图模板！</span><span class="sxs-lookup"><span data-stu-id="98d87-192">Next, you need a Welcome view template!</span></span> <span data-ttu-id="98d87-193">在 "**调试**" 菜单中，选择 "**生成 MvcMovie** " 以确保项目已编译。</span><span class="sxs-lookup"><span data-stu-id="98d87-193">In the **Debug** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="98d87-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="98d87-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="98d87-195">然后在 `Welcome` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="98d87-195">Then right-click inside the `Welcome` method and click **Add View**.</span></span> <span data-ttu-id="98d87-196">"**添加视图**" 对话框如下所示：</span><span class="sxs-lookup"><span data-stu-id="98d87-196">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image13.png)

<span data-ttu-id="98d87-197">单击 "**添加**"，然后在新的 "*欢迎*#" 文件中的 `<h2>` 元素下添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="98d87-197">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="98d87-198">你将创建一个循环，该循环显示 "Hello" 的次数与用户所示的次数相同。</span><span class="sxs-lookup"><span data-stu-id="98d87-198">You'll create a loop that says "Hello" as many times as the user says it should.</span></span> <span data-ttu-id="98d87-199">下面显示了完整的*欢迎. cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="98d87-199">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

<span data-ttu-id="98d87-200">运行应用程序并浏览到以下 URL：</span><span class="sxs-lookup"><span data-stu-id="98d87-200">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="98d87-201">现在，数据是从 URL 获取的，并会自动传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="98d87-201">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="98d87-202">控制器将数据打包到 `ViewBag` 对象中，并将该对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="98d87-202">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="98d87-203">然后，视图将以 HTML 格式向用户显示数据。</span><span class="sxs-lookup"><span data-stu-id="98d87-203">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image14.png)

<span data-ttu-id="98d87-204">当然，这是模型的一种“M”类型，而不是数据库类。</span><span class="sxs-lookup"><span data-stu-id="98d87-204">Well, that was a kind of an "M" for model, but not the database kind.</span></span> <span data-ttu-id="98d87-205">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="98d87-205">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="98d87-206">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="98d87-206">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
