---
title: 将视图添加到 MVC 应用
author: Rick-Anderson
description: 将视图添加到 MVC 应用
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 4b369028aca1e8a6cace60466b8049ccc02a2ec2
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519058"
---
# <a name="adding-a-view"></a><span data-ttu-id="0b963-103">添加视图</span><span class="sxs-lookup"><span data-stu-id="0b963-103">Adding a View</span></span>

<span data-ttu-id="0b963-104">作者： [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="0b963-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="0b963-105">在本节中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。</span><span class="sxs-lookup"><span data-stu-id="0b963-105">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span> 

<span data-ttu-id="0b963-106">使用[Razor 视图引擎](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)可以创建视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="0b963-106">You'll create a view template file using the [Razor view engine](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span></span> <span data-ttu-id="0b963-107">基于 Razor 的视图模板的文件扩展名为*cshtml* ，并提供使用C#创建 HTML 输出的简洁方法。</span><span class="sxs-lookup"><span data-stu-id="0b963-107">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="0b963-108">Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。</span><span class="sxs-lookup"><span data-stu-id="0b963-108">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="0b963-109">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="0b963-109">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="0b963-110">更改 `Index` 方法以调用控制器[视图](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View)方法，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="0b963-110">Change the `Index` method to call the controllers [View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) method, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

<span data-ttu-id="0b963-111">上面的 `Index` 方法使用视图模板生成浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="0b963-111">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="0b963-112">控制器方法（也称为[操作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)）（如上述 `Index` 方法）通常返回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) （或派生自[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)的类），而不是基元类型（如 string）。</span><span class="sxs-lookup"><span data-stu-id="0b963-112">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="0b963-113">右键单击*Views\HelloWorld*文件夹，单击 "**添加**"，然后单击 "**带有布局的 MVC 5 视图页（Razor）** "。</span><span class="sxs-lookup"><span data-stu-id="0b963-113">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image1.png)   
  
<span data-ttu-id="0b963-114">在 "**指定项目的名称**" 对话框中，输入*Index*，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="0b963-114">In the **Specify Name for Item** dialog box, enter *Index*, and then click **OK**.</span></span>  
  
![](adding-a-view/_static/image2.png)  
  
<span data-ttu-id="0b963-115">在 "**选择布局页**" 对话框中，接受默认 **\_Layout** ，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="0b963-115">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image3.png)  
  
<span data-ttu-id="0b963-116">在上面的对话框中，在左窗格中选择了 " *Views\Shared* " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="0b963-116">In the dialog above, the *Views\Shared* folder is selected in the left pane.</span></span> <span data-ttu-id="0b963-117">如果在其他文件夹中有自定义的布局文件，则可以选择它。</span><span class="sxs-lookup"><span data-stu-id="0b963-117">If you had a custom layout file in another folder, you could select it.</span></span> <span data-ttu-id="0b963-118">我们稍后将在本教程中讨论布局文件</span><span class="sxs-lookup"><span data-stu-id="0b963-118">We'll talk about the layout file later in the tutorial</span></span>

<span data-ttu-id="0b963-119">将创建*MvcMovie\Views\HelloWorld\Index.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="0b963-119">The *MvcMovie\Views\HelloWorld\Index.cshtml* file is created.</span></span>

![](adding-a-view/_static/image4.png)

<span data-ttu-id="0b963-120">添加以下突出显示的标记。</span><span class="sxs-lookup"><span data-stu-id="0b963-120">Add the following highlighted markup.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

<span data-ttu-id="0b963-121">右键单击该*索引的 cshtml*文件，然后选择 **"在浏览器中查看"** 。</span><span class="sxs-lookup"><span data-stu-id="0b963-121">Right click the *Index.cshtml* file and select **View in Browser**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="0b963-123">您还可以右键单击该*索引的 cshtml*文件，然后**在 Page Inspector 中选择 "查看"。**</span><span class="sxs-lookup"><span data-stu-id="0b963-123">You can also right click the *Index.cshtml* file and select **View in Page Inspector.**</span></span> <span data-ttu-id="0b963-124">有关详细信息，请参阅[Page Inspector 教程](../../views/using-page-inspector-in-aspnet-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="0b963-124">See the [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) for more information.</span></span>

<span data-ttu-id="0b963-125">或者，运行应用程序并浏览到 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="0b963-125">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="0b963-126">控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，该语句指定方法应使用视图模板文件来呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="0b963-126">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="0b963-127">由于未显式指定要使用的视图模板文件的名称，ASP.NET MVC 的默认设置为使用 *Index.cshtml* 视图中的文件 *\Views\HelloWorld* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="0b963-127">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="0b963-128">下图显示了我们的视图模板 &quot;的字符串！视图中&quot; 硬编码。</span><span class="sxs-lookup"><span data-stu-id="0b963-128">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="0b963-129">看起来不错。</span><span class="sxs-lookup"><span data-stu-id="0b963-129">Looks pretty good.</span></span> <span data-ttu-id="0b963-130">但请注意，浏览器的标题栏显示 "Index-My ASP.NET 应用程序"，页面顶部的大链接显示 "应用程序名称"。</span><span class="sxs-lookup"><span data-stu-id="0b963-130">However, notice that the browser's title bar shows "Index - My ASP.NET Application," and the big link at the top of the page says "Application name."</span></span> <span data-ttu-id="0b963-131">根据浏览器窗口的大小，可能需要单击右上角的三个栏才能看到 "**主页**"、"**关于**"、"**联系人**"、"**注册**" 和 **"登录**" 链接。</span><span class="sxs-lookup"><span data-stu-id="0b963-131">Depending on how small you make your browser window, you might need to click the three bars in the upper right to see the to the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="0b963-132">更改视图和布局页</span><span class="sxs-lookup"><span data-stu-id="0b963-132">Changing Views and Layout Pages</span></span>

<span data-ttu-id="0b963-133">首先，您需要更改页面顶部&quot; 链接的 &quot;应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="0b963-133">First, you want to change the &quot;Application name&quot; link at the top of the page.</span></span> <span data-ttu-id="0b963-134">该文本对于每个页面都是通用的。</span><span class="sxs-lookup"><span data-stu-id="0b963-134">That text is common to every page.</span></span> <span data-ttu-id="0b963-135">它实际上只在项目中的一个位置实现，即使它显示在应用程序的每一页上也是如此。</span><span class="sxs-lookup"><span data-stu-id="0b963-135">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="0b963-136">中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 *\_的布局 cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="0b963-136">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="0b963-137">此文件称为*布局页面*，位于所有其他页面都使用的共享文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0b963-137">This file is called a *layout page* and it's in the shared folder that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="0b963-139">布局模板允许在一个位置指定网站的 HTML 容器布局，然后将其应用到站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="0b963-139">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="0b963-140">查找 `@RenderBody()` 行。</span><span class="sxs-lookup"><span data-stu-id="0b963-140">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="0b963-141">`RenderBody` 是显示创建的所有特定于视图的页面的占位符，已包装在布局页面中&quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="0b963-141">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="0b963-142">例如，如果选择 "**关于**" 链接，则会在 `RenderBody` 方法中呈现*Views\Home\About.cshtml*视图。</span><span class="sxs-lookup"><span data-stu-id="0b963-142">For example, if you select the **About** link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="0b963-143">更改标题元素的内容。</span><span class="sxs-lookup"><span data-stu-id="0b963-143">Change the contents of the title element.</span></span> <span data-ttu-id="0b963-144">将布局模板中的[html.actionlink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx)从 &quot;应用程序名称&quot; 更改为 &quot;MVC 电影&quot;，并将控制器从 `Home` `Movies`到。</span><span class="sxs-lookup"><span data-stu-id="0b963-144">Change the [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) in the layout template from &quot;Application name&quot; to &quot;MVC Movie&quot; and the controller from `Home` to `Movies`.</span></span> <span data-ttu-id="0b963-145">完整的布局文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="0b963-145">The complete layout file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

<span data-ttu-id="0b963-146">运行该应用程序，请注意，它现在显示 &quot;MVC 电影 &quot;。</span><span class="sxs-lookup"><span data-stu-id="0b963-146">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="0b963-147">单击 "**关于**" 链接，你将看到该页面还 &quot;MVC 电影&quot;中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="0b963-147">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="0b963-148">我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="0b963-148">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="0b963-149">首次创建*Views\HelloWorld\Index.cshtml*文件时，它包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="0b963-149">When we first created the *Views\HelloWorld\Index.cshtml* file, it contained the following code:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="0b963-150">上述 Razor 代码显式设置布局页。</span><span class="sxs-lookup"><span data-stu-id="0b963-150">The Razor code above is explicitly setting the layout page.</span></span> <span data-ttu-id="0b963-151">检查 *\\_ViewStart 的视图*，其中包含的 Razor 标记完全相同。</span><span class="sxs-lookup"><span data-stu-id="0b963-151">Examine the *Views\\_ViewStart.cshtml* file, it contains the exact same Razor markup.</span></span> <span data-ttu-id="0b963-152">*[视图\\_ViewStart 的视图](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* 定义所有视图都将使用的通用布局，因此，您可以从*Views\HelloWorld\Index.cshtml*文件中注释掉或删除该代码。</span><span class="sxs-lookup"><span data-stu-id="0b963-152">The *[Views\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* file defines the common layout that all views will use, therefore you can comment out or remove that code from the *Views\HelloWorld\Index.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

<span data-ttu-id="0b963-153">可以使用 `Layout` 属性设置不同的布局视图，或将它设置为 `null`，这样将不会使用任何布局文件。</span><span class="sxs-lookup"><span data-stu-id="0b963-153">You can use the `Layout` property to set a different layout view, or set it to `null` so no layout file will be used.</span></span>

<span data-ttu-id="0b963-154">现在，让我们更改索引视图的标题。</span><span class="sxs-lookup"><span data-stu-id="0b963-154">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="0b963-155">打开*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="0b963-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="0b963-156">有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。</span><span class="sxs-lookup"><span data-stu-id="0b963-156">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="0b963-157">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="0b963-157">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

<span data-ttu-id="0b963-158">若要指示要显示的 HTML 标题，上面的代码将设置 `ViewBag` 对象（在*索引. cshtml*视图模板中）的 `Title` 属性。</span><span class="sxs-lookup"><span data-stu-id="0b963-158">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="0b963-159">请注意，布局模板（ *Views\Shared\\_Layout* ）在 `<title>` 元素中使用此值作为之前修改的 HTML 的 `<head>` 部分。</span><span class="sxs-lookup"><span data-stu-id="0b963-159">Notice that the layout template ( *Views\Shared\\_Layout.cshtml* ) uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

<span data-ttu-id="0b963-160">使用此 `ViewBag` 方法，可以轻松地在视图模板和布局文件之间传递其他参数。</span><span class="sxs-lookup"><span data-stu-id="0b963-160">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="0b963-161">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="0b963-161">Run the application.</span></span> <span data-ttu-id="0b963-162">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="0b963-162">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="0b963-163">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="0b963-163">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="0b963-164">在浏览器中按 Ctrl + F5 来强制加载来自服务器的响应。）浏览器标题是通过在*Index. cshtml*视图模板中设置的 `ViewBag.Title` 创建的，而其他 &quot;电影应用&quot; 添加到布局文件中。</span><span class="sxs-lookup"><span data-stu-id="0b963-164">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="0b963-165">另请注意， *Index.* view 模板中的内容是如何与 *\_Layout*视图模板合并的，并向浏览器发送单个 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="0b963-165">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="0b963-166">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="0b963-166">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="0b963-167">不过，我们的 &quot;数据&quot; （在这种情况下，我们的视图模板！&quot; 消息中的 &quot;Hello）是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="0b963-167">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="0b963-168">MVC 应用程序有一个 &quot;V&quot; （视图），并且你有 &quot;C&quot; （控制器），但没有 &quot;M&quot; （模型）。</span><span class="sxs-lookup"><span data-stu-id="0b963-168">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="0b963-169">稍后，我们将演练如何创建数据库并从中检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="0b963-169">Shortly, we'll walk through how to create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="0b963-170">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="0b963-170">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="0b963-171">不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="0b963-171">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="0b963-172">为了响应传入 URL 请求，将调用控制器类。</span><span class="sxs-lookup"><span data-stu-id="0b963-172">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="0b963-173">通过控制器类，您可以编写处理传入浏览器请求的代码，从数据库中检索数据，并最终决定要发送回浏览器的响应类型。</span><span class="sxs-lookup"><span data-stu-id="0b963-173">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="0b963-174">然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="0b963-174">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="0b963-175">控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="0b963-175">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="0b963-176">最佳做法：**视图模板不应执行业务逻辑或直接与数据库交互**。</span><span class="sxs-lookup"><span data-stu-id="0b963-176">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="0b963-177">相反，视图模板应仅适用于控制器为其提供的数据。</span><span class="sxs-lookup"><span data-stu-id="0b963-177">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="0b963-178">保持此 &quot;分离关注点&quot; 有助于使你的代码更干净、可测试、更易于维护。</span><span class="sxs-lookup"><span data-stu-id="0b963-178">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="0b963-179">当前，`HelloWorldController` 类中的 `Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="0b963-179">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="0b963-180">不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="0b963-180">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="0b963-181">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="0b963-181">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="0b963-182">为此，可以让控制器将视图模板所需的动态数据（参数）放置在视图模板可以访问 `ViewBag` 对象中。</span><span class="sxs-lookup"><span data-stu-id="0b963-182">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="0b963-183">返回到*HelloWorldController.cs*文件，更改 `Welcome` 方法，将 `Message` 和 `NumTimes` 值添加到 `ViewBag` 对象。</span><span class="sxs-lookup"><span data-stu-id="0b963-183">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="0b963-184">`ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中：在将对象放入其中之前，`ViewBag` 对象没有定义的属性。</span><span class="sxs-lookup"><span data-stu-id="0b963-184">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="0b963-185">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数（`name` 和 `numTimes`）从地址栏中的查询字符串映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="0b963-185">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="0b963-186">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="0b963-186">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

<span data-ttu-id="0b963-187">现在 `ViewBag` 对象包含将自动传递到该视图的数据。</span><span class="sxs-lookup"><span data-stu-id="0b963-187">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span> <span data-ttu-id="0b963-188">接下来，需要一个欢迎视图模板！</span><span class="sxs-lookup"><span data-stu-id="0b963-188">Next, you need a Welcome view template!</span></span> <span data-ttu-id="0b963-189">在 "**生成**" 菜单中，选择 "**生成解决方案**" （或按 Ctrl + Shift + B），以确保项目已编译。</span><span class="sxs-lookup"><span data-stu-id="0b963-189">In the **Build** menu, select **Build Solution** (or Ctrl+Shift+B) to make sure the project is compiled.</span></span> <span data-ttu-id="0b963-190">右键单击*Views\HelloWorld*文件夹，单击 "**添加**"，然后单击 "**带有布局的 MVC 5 视图页（Razor）** "。</span><span class="sxs-lookup"><span data-stu-id="0b963-190">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image10.png)   
  
<span data-ttu-id="0b963-191">在 "**指定项目的名称**" 对话框中，输入 "*欢迎*"，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="0b963-191">In the **Specify Name for Item** dialog box, enter *Welcome*, and then click **OK**.</span></span>   
  
<span data-ttu-id="0b963-192">在 "**选择布局页**" 对话框中，接受默认 **\_Layout** ，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="0b963-192">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image11.png)   

<span data-ttu-id="0b963-193">将创建*MvcMovie\Views\HelloWorld\Welcome.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="0b963-193">The *MvcMovie\Views\HelloWorld\Welcome.cshtml* file is created.</span></span>

<span data-ttu-id="0b963-194">替换*欢迎的 cshtml*文件中的标记。</span><span class="sxs-lookup"><span data-stu-id="0b963-194">Replace the markup in the *Welcome.cshtml* file.</span></span> <span data-ttu-id="0b963-195">你将创建一个循环，该循环显示 &quot;Hello&quot; 用户应尽可能多地显示。</span><span class="sxs-lookup"><span data-stu-id="0b963-195">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="0b963-196">下面显示了完整的*欢迎. cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="0b963-196">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

<span data-ttu-id="0b963-197">运行应用程序并浏览到以下 URL：</span><span class="sxs-lookup"><span data-stu-id="0b963-197">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="0b963-198">现在，数据是从 URL 获取的，并使用[模型绑定](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)器传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="0b963-198">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="0b963-199">控制器将数据打包到 `ViewBag` 对象中，并将该对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="0b963-199">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="0b963-200">然后，视图将以 HTML 格式向用户显示数据。</span><span class="sxs-lookup"><span data-stu-id="0b963-200">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="0b963-201">在上面的示例中，我们使用 `ViewBag` 对象将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="0b963-201">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="0b963-202">稍后在本教程中，我们将使用视图模型将数据从控制器传递给视图。</span><span class="sxs-lookup"><span data-stu-id="0b963-202">Later in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="0b963-203">用于传递数据的视图模型方法通常比查看包方法更可取。</span><span class="sxs-lookup"><span data-stu-id="0b963-203">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="0b963-204">有关详细信息，请参阅博客文章[动态 V 强类型视图](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b963-204">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span> 

<span data-ttu-id="0b963-205">嗯，这是模型的 &quot;M&quot;，而不是数据库类型。</span><span class="sxs-lookup"><span data-stu-id="0b963-205">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="0b963-206">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="0b963-206">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0b963-207">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="0b963-207">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
