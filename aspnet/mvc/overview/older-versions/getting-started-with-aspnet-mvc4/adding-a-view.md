---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: 添加视图 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457630"
---
# <a name="adding-a-view"></a><span data-ttu-id="c0a22-104">添加视图</span><span class="sxs-lookup"><span data-stu-id="c0a22-104">Adding a View</span></span>

<span data-ttu-id="c0a22-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c0a22-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="c0a22-106">[此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="c0a22-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="c0a22-107">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="c0a22-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="c0a22-108">在本节中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。</span><span class="sxs-lookup"><span data-stu-id="c0a22-108">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="c0a22-109">你将使用 ASP.NET MVC 3 引入的[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)创建视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="c0a22-109">You'll create a view template file using the [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="c0a22-110">基于 Razor 的视图模板的文件扩展名为*cshtml* ，并提供使用C#创建 HTML 输出的简洁方法。</span><span class="sxs-lookup"><span data-stu-id="c0a22-110">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="c0a22-111">Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。</span><span class="sxs-lookup"><span data-stu-id="c0a22-111">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="c0a22-112">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="c0a22-112">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="c0a22-113">更改 `Index` 方法以返回 `View` 对象，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="c0a22-113">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="c0a22-114">上面的 `Index` 方法使用视图模板生成浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="c0a22-114">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="c0a22-115">控制器方法（也称为[操作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)）（如上述 `Index` 方法）通常返回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) （或派生自[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)的类），而不是基元类型（如 string）。</span><span class="sxs-lookup"><span data-stu-id="c0a22-115">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="c0a22-116">在项目中，添加可与 `Index` 方法一起使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="c0a22-116">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="c0a22-117">为此，请在 `Index` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="c0a22-117">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="c0a22-118">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="c0a22-118">The **Add View** dialog box appears.</span></span> <span data-ttu-id="c0a22-119">保留默认值，并单击 "**添加**" 按钮：</span><span class="sxs-lookup"><span data-stu-id="c0a22-119">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="c0a22-120">将创建*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="c0a22-120">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="c0a22-121">可以在**解决方案资源管理器**中查看它们：</span><span class="sxs-lookup"><span data-stu-id="c0a22-121">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="c0a22-122">下面显示了已创建的*索引 cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="c0a22-122">The following shows the *Index.cshtml* file that was created:</span></span>

![HelloWorldIndex](adding-a-view/_static/image4.png)

<span data-ttu-id="c0a22-124">在 `<h2>` 标记下添加以下 HTML。</span><span class="sxs-lookup"><span data-stu-id="c0a22-124">Add the following HTML under the `<h2>` tag.</span></span>

[!code-html[Main](adding-a-view/samples/sample2.html)]

<span data-ttu-id="c0a22-125">完整的*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0a22-125">The complete *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

<span data-ttu-id="c0a22-126">如果使用的是 Visual Studio 2012，请在 "解决方案资源管理器" 中，右键单击*索引.* # 文件，然后**在 Page Inspector 中选择 "查看**"。</span><span class="sxs-lookup"><span data-stu-id="c0a22-126">If you are using Visual Studio 2012, in solution explorer, right click the *Index.cshtml* file and select **View in Page Inspector**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="c0a22-128">[Page Inspector 教程](../../views/using-page-inspector-in-aspnet-mvc.md)包含有关此新工具的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0a22-128">The [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) has more information about this new tool.</span></span>

<span data-ttu-id="c0a22-129">或者，运行应用程序并浏览到 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="c0a22-129">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="c0a22-130">控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，该语句指定方法应使用视图模板文件来呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="c0a22-130">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="c0a22-131">由于未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 *\Views\HelloWorld*文件夹中的*视图文件。*</span><span class="sxs-lookup"><span data-stu-id="c0a22-131">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="c0a22-132">下图显示了我们的视图模板 &quot;的字符串！视图中&quot; 硬编码。</span><span class="sxs-lookup"><span data-stu-id="c0a22-132">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="c0a22-133">看起来不错。</span><span class="sxs-lookup"><span data-stu-id="c0a22-133">Looks pretty good.</span></span> <span data-ttu-id="c0a22-134">但请注意，浏览器的标题栏显示 &quot;索引我的 ASP.NET A&quot;，页面顶部的大链接显示此处 &quot;徽标。下面&quot; &quot;你的徽标。&quot; "链接" 是 "注册" 和 "登录" 链接，并链接到 "主页"、"关于" 和 "联系人" 页。</span><span class="sxs-lookup"><span data-stu-id="c0a22-134">However, notice that the browser's title bar shows &quot;Index My ASP.NET A&quot; and the big link on the top of the page says &quot;your logo here.&quot; Below the &quot;your logo here.&quot; link are registration and log in links, and below that links to Home, About and Contact pages.</span></span> <span data-ttu-id="c0a22-135">我们来更改其中一些。</span><span class="sxs-lookup"><span data-stu-id="c0a22-135">Let's change some of these.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="c0a22-136">更改视图和布局页</span><span class="sxs-lookup"><span data-stu-id="c0a22-136">Changing Views and Layout Pages</span></span>

<span data-ttu-id="c0a22-137">首先，需要在此处更改徽标 &quot;。页面顶部&quot; 标题。</span><span class="sxs-lookup"><span data-stu-id="c0a22-137">First, you want to change the &quot;your logo here.&quot; title at the top of the page.</span></span> <span data-ttu-id="c0a22-138">该文本对于每个页面都是通用的。</span><span class="sxs-lookup"><span data-stu-id="c0a22-138">That text is common to every page.</span></span> <span data-ttu-id="c0a22-139">它实际上只在项目中的一个位置实现，即使它显示在应用程序的每一页上也是如此。</span><span class="sxs-lookup"><span data-stu-id="c0a22-139">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="c0a22-140">中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 *\_的布局 cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="c0a22-140">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="c0a22-141">此文件称为*布局页*，它是所有其他页面都使用的共享 &quot;shell&quot;。</span><span class="sxs-lookup"><span data-stu-id="c0a22-141">This file is called a *layout page* and it's the shared &quot;shell&quot; that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="c0a22-143">布局模板允许在一个位置指定网站的 HTML 容器布局，然后将其应用到站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="c0a22-143">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="c0a22-144">查找 `@RenderBody()` 行。</span><span class="sxs-lookup"><span data-stu-id="c0a22-144">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="c0a22-145">`RenderBody` 是显示创建的所有特定于视图的页面的占位符，已包装在布局页面中&quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="c0a22-145">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="c0a22-146">例如，如果选择 "关于" 链接，则会在 `RenderBody` 方法中呈现*Views\Home\About.cshtml*视图。</span><span class="sxs-lookup"><span data-stu-id="c0a22-146">For example, if you select the About link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="c0a22-147">在此处&quot; &quot;徽标，将布局模板中的网站标题标题更改为 &quot;MVC 电影&quot;。</span><span class="sxs-lookup"><span data-stu-id="c0a22-147">Change the site-title heading in the layout template from &quot;your logo here&quot; to &quot;MVC Movie&quot;.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="c0a22-148">将 title 元素的内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="c0a22-148">Replace the contents of the title element with the following markup:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="c0a22-149">运行该应用程序，请注意，它现在显示 &quot;MVC 电影 &quot;。</span><span class="sxs-lookup"><span data-stu-id="c0a22-149">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="c0a22-150">单击 "**关于**" 链接，你将看到该页面还 &quot;MVC 电影&quot;中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="c0a22-150">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="c0a22-151">我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="c0a22-151">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="c0a22-152">现在，让我们更改索引视图的标题。</span><span class="sxs-lookup"><span data-stu-id="c0a22-152">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="c0a22-153">打开*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="c0a22-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="c0a22-154">有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。</span><span class="sxs-lookup"><span data-stu-id="c0a22-154">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="c0a22-155">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="c0a22-155">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

<span data-ttu-id="c0a22-156">若要指示要显示的 HTML 标题，上面的代码将设置 `ViewBag` 对象（在*索引. cshtml*视图模板中）的 `Title` 属性。</span><span class="sxs-lookup"><span data-stu-id="c0a22-156">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="c0a22-157">如果你查看布局模板的源代码，你会注意到，模板在 `<title>` 元素中使用此值作为之前修改的 HTML 的 `<head>` 部分。</span><span class="sxs-lookup"><span data-stu-id="c0a22-157">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span> <span data-ttu-id="c0a22-158">使用此 `ViewBag` 方法，可以轻松地在视图模板和布局文件之间传递其他参数。</span><span class="sxs-lookup"><span data-stu-id="c0a22-158">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="c0a22-159">运行应用程序并浏览到 `http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="c0a22-159">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="c0a22-160">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="c0a22-160">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="c0a22-161">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="c0a22-161">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="c0a22-162">在浏览器中按 Ctrl + F5 来强制加载来自服务器的响应。）浏览器标题是通过在*Index. cshtml*视图模板中设置的 `ViewBag.Title` 创建的，而其他 &quot;电影应用&quot; 添加到布局文件中。</span><span class="sxs-lookup"><span data-stu-id="c0a22-162">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="c0a22-163">另请注意， *Index.* view 模板中的内容是如何与 *\_Layout*视图模板合并的，并向浏览器发送单个 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="c0a22-163">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="c0a22-164">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="c0a22-164">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="c0a22-165">不过，我们的 &quot;数据&quot; （在这种情况下，我们的视图模板！&quot; 消息中的 &quot;Hello）是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="c0a22-165">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="c0a22-166">MVC 应用程序有一个 &quot;V&quot; （视图），并且你有 &quot;C&quot; （控制器），但没有 &quot;M&quot; （模型）。</span><span class="sxs-lookup"><span data-stu-id="c0a22-166">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="c0a22-167">稍后，我们将逐步介绍如何创建数据库并从该数据库中检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="c0a22-167">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="c0a22-168">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="c0a22-168">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="c0a22-169">不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="c0a22-169">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="c0a22-170">为了响应传入 URL 请求，将调用控制器类。</span><span class="sxs-lookup"><span data-stu-id="c0a22-170">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="c0a22-171">通过控制器类，您可以编写处理传入浏览器请求的代码，从数据库中检索数据，并最终决定要发送回浏览器的响应类型。</span><span class="sxs-lookup"><span data-stu-id="c0a22-171">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="c0a22-172">然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="c0a22-172">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="c0a22-173">控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="c0a22-173">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="c0a22-174">最佳做法：**视图模板不应执行业务逻辑或直接与数据库交互**。</span><span class="sxs-lookup"><span data-stu-id="c0a22-174">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="c0a22-175">相反，视图模板应仅适用于控制器为其提供的数据。</span><span class="sxs-lookup"><span data-stu-id="c0a22-175">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="c0a22-176">保持此 &quot;分离关注点&quot; 有助于使你的代码更干净、可测试、更易于维护。</span><span class="sxs-lookup"><span data-stu-id="c0a22-176">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="c0a22-177">当前，`HelloWorldController` 类中的 `Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="c0a22-177">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="c0a22-178">不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="c0a22-178">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="c0a22-179">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="c0a22-179">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="c0a22-180">为此，可以让控制器将视图模板所需的动态数据（参数）放置在视图模板可以访问 `ViewBag` 对象中。</span><span class="sxs-lookup"><span data-stu-id="c0a22-180">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="c0a22-181">返回到*HelloWorldController.cs*文件，更改 `Welcome` 方法，将 `Message` 和 `NumTimes` 值添加到 `ViewBag` 对象。</span><span class="sxs-lookup"><span data-stu-id="c0a22-181">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="c0a22-182">`ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中：在将对象放入其中之前，`ViewBag` 对象没有定义的属性。</span><span class="sxs-lookup"><span data-stu-id="c0a22-182">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="c0a22-183">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数（`name` 和 `numTimes`）从地址栏中的查询字符串映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="c0a22-183">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="c0a22-184">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0a22-184">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="c0a22-185">现在 `ViewBag` 对象包含将自动传递到该视图的数据。</span><span class="sxs-lookup"><span data-stu-id="c0a22-185">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="c0a22-186">接下来，需要一个欢迎视图模板！</span><span class="sxs-lookup"><span data-stu-id="c0a22-186">Next, you need a Welcome view template!</span></span> <span data-ttu-id="c0a22-187">在 "**生成**" 菜单中，选择 "**生成 MvcMovie** " 以确保项目已编译。</span><span class="sxs-lookup"><span data-stu-id="c0a22-187">In the **Build** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="c0a22-188">然后在 `Welcome` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="c0a22-188">Then right-click inside the `Welcome` method and click **Add View**.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="c0a22-189">"**添加视图**" 对话框如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0a22-189">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image11.png)

<span data-ttu-id="c0a22-190">单击 "**添加**"，然后在新的 "*欢迎*#" 文件中的 `<h2>` 元素下添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="c0a22-190">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="c0a22-191">你将创建一个循环，该循环显示 &quot;Hello&quot; 用户应尽可能多地显示。</span><span class="sxs-lookup"><span data-stu-id="c0a22-191">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="c0a22-192">下面显示了完整的*欢迎. cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="c0a22-192">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

<span data-ttu-id="c0a22-193">运行应用程序并浏览到以下 URL：</span><span class="sxs-lookup"><span data-stu-id="c0a22-193">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="c0a22-194">现在，数据是从 URL 获取的，并使用[模型绑定](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)器传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="c0a22-194">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="c0a22-195">控制器将数据打包到 `ViewBag` 对象中，并将该对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="c0a22-195">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="c0a22-196">然后，视图将以 HTML 格式向用户显示数据。</span><span class="sxs-lookup"><span data-stu-id="c0a22-196">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="c0a22-197">在上面的示例中，我们使用 `ViewBag` 对象将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="c0a22-197">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="c0a22-198">在本教程中，我们将使用视图模型将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="c0a22-198">Latter in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="c0a22-199">用于传递数据的视图模型方法通常比查看包方法更可取。</span><span class="sxs-lookup"><span data-stu-id="c0a22-199">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="c0a22-200">有关详细信息，请参阅博客文章[动态 V 强类型视图](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0a22-200">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span>

<span data-ttu-id="c0a22-201">嗯，这是模型的 &quot;M&quot;，而不是数据库类型。</span><span class="sxs-lookup"><span data-stu-id="c0a22-201">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="c0a22-202">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="c0a22-202">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c0a22-203">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="c0a22-203">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
