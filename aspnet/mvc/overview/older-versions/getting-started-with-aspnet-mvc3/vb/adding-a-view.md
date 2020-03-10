---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 添加视图（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434516"
---
# <a name="adding-a-view-vb"></a><span data-ttu-id="0dc6a-103">添加视图 (VB)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-103">Adding a View (VB)</span></span>

<span data-ttu-id="0dc6a-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="0dc6a-105">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="0dc6a-106">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="0dc6a-107">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="0dc6a-108">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="0dc6a-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="0dc6a-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="0dc6a-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="0dc6a-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="0dc6a-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="0dc6a-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="0dc6a-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="0dc6a-112">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="0dc6a-113">本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="0dc6a-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="0dc6a-115">如果愿意C#，请切换到本教程的[ C#版本](../cs/adding-a-view.md)。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-115">If you prefer C#, switch to the [C# version](../cs/adding-a-view.md) of this tutorial.</span></span>

<span data-ttu-id="0dc6a-116">在本部分中，我们将修改 `HelloWorldController` 类以使用视图模板文件将生成 HTML 响应的过程清晰地封装到客户端。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-116">In this section we're going to modify the `HelloWorldController` class to use a view template file to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="0dc6a-117">首先，将视图模板用于 `HelloWorldController` 类中的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-117">Let's start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="0dc6a-118">目前 `Index` 方法返回一个字符串，其中包含在控制器类中硬编码的消息。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-118">Currently the `Index` method returns a string with a message that is hard-coded within the controller class.</span></span> <span data-ttu-id="0dc6a-119">更改 `Index` 方法以返回 `View` 对象，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0dc6a-119">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

<span data-ttu-id="0dc6a-120">现在，让我们将视图模板添加到我们的项目，我们可以使用 `Index` 方法调用这些模板。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-120">Let's now add a view template to our project that we can invoke with the `Index` method.</span></span> <span data-ttu-id="0dc6a-121">为此，请在 `Index` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-121">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

<span data-ttu-id="0dc6a-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span></span>

<span data-ttu-id="0dc6a-123">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-123">The **Add View** dialog box appears.</span></span> <span data-ttu-id="0dc6a-124">保留默认条目，然后单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-124">Leave the default entries and click the **Add** button.</span></span>

<span data-ttu-id="0dc6a-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span></span>

<span data-ttu-id="0dc6a-126">将创建*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.vbhtml*文件。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-126">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.vbhtml* file are created.</span></span> <span data-ttu-id="0dc6a-127">可以在**解决方案资源管理器**中查看它们：</span><span class="sxs-lookup"><span data-stu-id="0dc6a-127">You can see them in **Solution Explorer**:</span></span>

<span data-ttu-id="0dc6a-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span></span>

<span data-ttu-id="0dc6a-129">在 `<h2>` 标记下添加一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-129">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="0dc6a-130">修改后的*MvcMovie\Views\HelloWorld\Index.vbhtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-130">The modified *MvcMovie\Views\HelloWorld\Index.vbhtml* file is shown below.</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

<span data-ttu-id="0dc6a-131">运行应用程序并浏览到 &quot;hello world&quot; 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-131">Run the application and browse to the &quot;hello world&quot; controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="0dc6a-132">控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，指出我们想要使用视图模板文件来呈现客户端的响应。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-132">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which indicated that we wanted to use a view template file to render a response to the client.</span></span> <span data-ttu-id="0dc6a-133">由于我们未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 *\Views\HelloWorld*文件夹中的*视图文件。*</span><span class="sxs-lookup"><span data-stu-id="0dc6a-133">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.vbhtml* view file within the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="0dc6a-134">下图显示了视图中硬编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-134">The image below shows the string hard-coded in the view.</span></span>

<span data-ttu-id="0dc6a-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="0dc6a-136">看起来不错。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-136">Looks pretty good.</span></span> <span data-ttu-id="0dc6a-137">但请注意，浏览器的标题栏显示 &quot;索引&quot;，而页面上的大标题显示 &quot;我的 MVC 应用程序。&quot; 让我们更改这些。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-137">However, notice that the browser's title bar says &quot;Index&quot; and the big title on the page says &quot;My MVC Application.&quot; Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="0dc6a-138">更改视图和布局页面</span><span class="sxs-lookup"><span data-stu-id="0dc6a-138">Changing views and layout pages</span></span>

<span data-ttu-id="0dc6a-139">首先，让我们更改 MVC 应用程序 &quot;的文本。&quot; 共享文本，并在每一页上显示。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-139">First, let's change the text &quot;My MVC Application.&quot; That text is shared and appears on every page.</span></span> <span data-ttu-id="0dc6a-140">它实际上只出现在项目中的一个位置，即使它在应用程序的每一页上也是如此。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-140">It actually appears in only one place in our project, even though it's on every page in our application.</span></span> <span data-ttu-id="0dc6a-141">中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，并打开 *\_Layout*文件。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-141">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.vbhtml* file.</span></span> <span data-ttu-id="0dc6a-142">此文件称为布局页，它是所有其他页面都使用的共享 &quot;shell&quot;。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-142">This file is called a layout page and it's the shared &quot;shell&quot; that all other pages use.</span></span>

<span data-ttu-id="0dc6a-143">请注意文件底部附近的 `@RenderBody()` 代码行。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-143">Note the `@RenderBody()` line of code near the bottom of the file.</span></span> <span data-ttu-id="0dc6a-144">`RenderBody` 是一个占位符，其中所创建的所有页面都显示在 "布局" 页中 &quot;包装&quot;。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-144">`RenderBody` is a placeholder where all the pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="0dc6a-145">将 `<h1>` 标题从 **&quot;** 我的 Mvc 应用程序&quot; 更改为 &quot;Mvc 电影应用程序&quot;。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-145">Change the `<h1>` heading from **&quot;** My MVC Application&quot; to &quot;MVC Movie App&quot;.</span></span>

[!code-html[Main](adding-a-view/samples/sample3.html)]

<span data-ttu-id="0dc6a-146">运行应用程序，并注意它现在会显示 &quot;MVC 电影应用&quot;。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-146">Run the application and note it now says &quot;MVC Movie App&quot;.</span></span> <span data-ttu-id="0dc6a-147">单击 "**关于**" 链接，该页还会显示 &quot;MVC 电影应用&quot;。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-147">Click the **About** link, and that page shows &quot;MVC Movie App&quot;, too.</span></span>

<span data-ttu-id="0dc6a-148">下面显示了完整的 *\_布局*：</span><span class="sxs-lookup"><span data-stu-id="0dc6a-148">The complete *\_Layout.vbhtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="0dc6a-149">现在，让我们更改索引页（视图）的标题。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-149">Now, let's change the title of the Index page (view).</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

<span data-ttu-id="0dc6a-150">打开*MvcMovie\Views\HelloWorld\Index.vbhtml*。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-150">Open *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span></span> <span data-ttu-id="0dc6a-151">有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-151">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="0dc6a-152">我们将使它们略有不同，以便您可以看到哪些代码更改了应用程序的哪一部分。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-152">We'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

<span data-ttu-id="0dc6a-153">运行应用程序并浏览到`http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-153">Run the application and browse to`http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="0dc6a-154">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-154">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="0dc6a-155">在应用程序中对视图进行较小的更改时，可以轻松地对应用程序进行重大更改。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-155">It's easy to make big changes in your application with small changes to a view.</span></span> <span data-ttu-id="0dc6a-156">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-156">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="0dc6a-157">在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）</span><span class="sxs-lookup"><span data-stu-id="0dc6a-157">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="0dc6a-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span></span>

<span data-ttu-id="0dc6a-159">但这有点 &quot;数据&quot; （在这种情况下，&quot;Hello World！&quot; 消息）是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-159">Our little bit of &quot;data&quot; (in this case the &quot;Hello World!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="0dc6a-160">MVC 应用程序有 V （views），但我们有 C （控制器），但没有 M （模型）。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-160">Our MVC application has V (views) and we've got C (controllers), but no M (model) yet.</span></span> <span data-ttu-id="0dc6a-161">稍后，我们将逐步介绍如何创建数据库并从该数据库中检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-161">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="0dc6a-162">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="0dc6a-162">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="0dc6a-163">不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-163">Before we go to a database and talk about models, though, let's first talk about passing information from the Controller to a View.</span></span> <span data-ttu-id="0dc6a-164">我们想要传递视图模板所需的内容，以便向客户端呈现 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-164">We want to pass what a view template requires in order to render an HTML response to a client.</span></span> <span data-ttu-id="0dc6a-165">这些对象通常由控制器类创建并传递给视图模板，并且它们应该只包含视图模板所需的数据，而不是更多。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-165">These objects are typically created and passed by a controller class to a view template, and they should contain only the data that the view template requires — and no more.</span></span>

<span data-ttu-id="0dc6a-166">以前使用 `HelloWorldController` 类时，`Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将参数值输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-166">Previously with the `HelloWorldController` class, the `Welcome` action method took a `name` and a `numTimes` parameter and then output the parameter values to the browser.</span></span> <span data-ttu-id="0dc6a-167">不要让控制器继续直接呈现此响应，而是让我们将该数据放入包中进行查看。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-167">Rather than have the controller continue to render this response directly, let's instead we'll put that data in a bag for the View.</span></span> <span data-ttu-id="0dc6a-168">控制器和视图可以使用 `ViewBag` 对象来保存这些数据。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-168">Controllers and Views can use a `ViewBag` object to hold that data.</span></span> <span data-ttu-id="0dc6a-169">这会自动传递到视图模板，并用于使用包的内容作为数据呈现 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-169">That will be passed over to a view template automatically, and used to render the HTML response using the contents of the bag as data.</span></span> <span data-ttu-id="0dc6a-170">这样一来，控制器就会考虑到其中的一项和视图模板，使我们能够在应用程序中保持&quot; &quot;分离问题。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-170">That way the controller is concerned with one thing and the view template with another — enabling us to maintain clean &quot;separation of concerns&quot; within the application.</span></span>

<span data-ttu-id="0dc6a-171">另外，我们还可以定义一个自定义类，然后创建该对象的一个实例，用数据填充该对象并将其传递给视图。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-171">Alternatively, we could define a custom class, then create an instance of that object on our own, fill it with data and pass it to the View.</span></span> <span data-ttu-id="0dc6a-172">这通常称为 ViewModel，因为它是视图的自定义模型。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-172">That is often called a ViewModel, because it's a custom Model for the View.</span></span> <span data-ttu-id="0dc6a-173">但对于少量的数据，ViewBag 非常有用。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-173">For small amounts of data, however, the ViewBag works great.</span></span>

<span data-ttu-id="0dc6a-174">返回到*HelloWorldController*文件更改控制器内的 `Welcome` 方法，将消息和 NumTimes 置于 ViewBag 中。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-174">Return to the *HelloWorldController.vb* file change the `Welcome` method inside the controller to put the Message and NumTimes into the ViewBag.</span></span> <span data-ttu-id="0dc6a-175">ViewBag 是动态对象。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-175">The ViewBag is a dynamic object.</span></span> <span data-ttu-id="0dc6a-176">这意味着你可以将所需的任何内容放入其中。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-176">That means you can put whatever you want in to it.</span></span> <span data-ttu-id="0dc6a-177">在将某些内容放入其中之前，ViewBag 没有定义的属性。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-177">The ViewBag has no defined properties until you put something inside it.</span></span>

<span data-ttu-id="0dc6a-178">同一个文件中的新类的完整 `HelloWorldController.vb`。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-178">The complete `HelloWorldController.vb` with the new class in the same file.</span></span>

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

<span data-ttu-id="0dc6a-179">现在，我们的 ViewBag 包含将自动传递到该视图的数据。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-179">Now our ViewBag contains data that will be passed over to the View automatically.</span></span> <span data-ttu-id="0dc6a-180">同样，我们也可以在自己的对象中传递，如我们所喜欢的：</span><span class="sxs-lookup"><span data-stu-id="0dc6a-180">Again, alternatively we could have passed in our own object like this if we liked:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="0dc6a-181">现在，我们需要 `WelcomeView` 模板！</span><span class="sxs-lookup"><span data-stu-id="0dc6a-181">Now we need a `WelcomeView` template!</span></span> <span data-ttu-id="0dc6a-182">运行应用程序，以便编译新代码。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-182">Run the application so the new code is compiled.</span></span> <span data-ttu-id="0dc6a-183">关闭浏览器，在 `Welcome` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-183">Close the browser, right-click inside the `Welcome` method, and then click **Add View**.</span></span>

<span data-ttu-id="0dc6a-184">"**添加视图**" 对话框如下所示。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-184">Here's what your **Add View** dialog box looks like.</span></span>

<span data-ttu-id="0dc6a-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="0dc6a-186">将以下代码添加到新欢迎中的 `<h2>` 元素下<em>。</em>vbhtml 文件。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-186">Add the following code under the `<h2>` element in the new <em>Welcome.</em>vbhtml file.</span></span> <span data-ttu-id="0dc6a-187">我们会作出循环，说 &quot;Hello&quot;，因为用户应该说！</span><span class="sxs-lookup"><span data-stu-id="0dc6a-187">We'll make a loop and say &quot;Hello&quot; as many times as the user says we should!</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

<span data-ttu-id="0dc6a-188">运行应用程序并浏览到 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span><span class="sxs-lookup"><span data-stu-id="0dc6a-188">Run the application and browse to `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span></span>

<span data-ttu-id="0dc6a-189">现在，数据是从 URL 获取的，并会自动传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-189">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="0dc6a-190">控制器将数据打包到 `Model` 对象中，并将该对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-190">The controller packages up the data into a `Model` object and passes that object to the view.</span></span> <span data-ttu-id="0dc6a-191">视图比向用户显示 HTML 数据。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-191">The view than displays the data as HTML to the user.</span></span>

<span data-ttu-id="0dc6a-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span></span>

<span data-ttu-id="0dc6a-193">嗯，这是模型的 &quot;M&quot;，而不是数据库类型。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-193">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="0dc6a-194">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="0dc6a-194">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0dc6a-195">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="0dc6a-195">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
