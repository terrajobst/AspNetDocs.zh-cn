---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第2部分：控制器 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第2部分涵盖控制器。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451190"
---
# <a name="part-2-controllers"></a><span data-ttu-id="4930a-104">第2部分：控制器</span><span class="sxs-lookup"><span data-stu-id="4930a-104">Part 2: Controllers</span></span>

<span data-ttu-id="4930a-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="4930a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="4930a-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="4930a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="4930a-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="4930a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="4930a-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="4930a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="4930a-109">第2部分涵盖控制器。</span><span class="sxs-lookup"><span data-stu-id="4930a-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="4930a-110">对于传统的 web 框架，传入 Url 通常映射到磁盘上的文件。</span><span class="sxs-lookup"><span data-stu-id="4930a-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="4930a-111">例如： "/Products.aspx" 或 "/Products.php" 等 URL 请求可能由 "Products" 或 "Products" 文件处理。</span><span class="sxs-lookup"><span data-stu-id="4930a-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="4930a-112">基于 Web 的 MVC 框架以略有不同的方式将 Url 映射到服务器代码。</span><span class="sxs-lookup"><span data-stu-id="4930a-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="4930a-113">它们不会将传入 Url 映射到文件，而是将 Url 映射到类的方法。</span><span class="sxs-lookup"><span data-stu-id="4930a-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="4930a-114">这些类称为 "控制器"，它们负责处理传入的 HTTP 请求，处理用户输入，检索和保存数据，确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他URL，等等）。</span><span class="sxs-lookup"><span data-stu-id="4930a-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="4930a-115">添加 HomeController</span><span class="sxs-lookup"><span data-stu-id="4930a-115">Adding a HomeController</span></span>

<span data-ttu-id="4930a-116">我们将通过添加一个控制器类来开始我们的 MVC 音乐应用商店应用程序，该控制器类将处理 Url 到我们站点的主页。</span><span class="sxs-lookup"><span data-stu-id="4930a-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="4930a-117">我们将遵循 ASP.NET MVC 的默认命名约定，并将其称为 HomeController。</span><span class="sxs-lookup"><span data-stu-id="4930a-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="4930a-118">右键单击解决方案资源管理器中的 "控制器" 文件夹，选择 "添加"，然后选择 "控制器 ..."command</span><span class="sxs-lookup"><span data-stu-id="4930a-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="4930a-119">此时将显示 "添加控制器" 对话框。</span><span class="sxs-lookup"><span data-stu-id="4930a-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="4930a-120">将控制器命名为 "HomeController"，然后按 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="4930a-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="4930a-121">这将创建一个具有以下代码的新文件 HomeController.cs：</span><span class="sxs-lookup"><span data-stu-id="4930a-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="4930a-122">若要尽可能简单地启动，请将 Index 方法替换为简单方法，只返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="4930a-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="4930a-123">我们将进行两个更改：</span><span class="sxs-lookup"><span data-stu-id="4930a-123">We'll make two changes:</span></span>

- <span data-ttu-id="4930a-124">更改方法以返回字符串而不是 ActionResult</span><span class="sxs-lookup"><span data-stu-id="4930a-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="4930a-125">更改 return 语句以返回 "Hello from Home"</span><span class="sxs-lookup"><span data-stu-id="4930a-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="4930a-126">方法现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="4930a-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="4930a-127">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="4930a-127">Running the Application</span></span>

<span data-ttu-id="4930a-128">现在，让我们运行站点。</span><span class="sxs-lookup"><span data-stu-id="4930a-128">Now let's run the site.</span></span> <span data-ttu-id="4930a-129">我们可以启动我们的 web 服务器，并使用以下任意一种来尝试使用该站点：</span><span class="sxs-lookup"><span data-stu-id="4930a-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="4930a-130">选择 Debug ⇨开始调试菜单项</span><span class="sxs-lookup"><span data-stu-id="4930a-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="4930a-131">单击工具栏中的绿色箭头按钮 ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="4930a-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="4930a-132">使用键盘快捷方式 F5。</span><span class="sxs-lookup"><span data-stu-id="4930a-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="4930a-133">使用上述任一步骤，将编译项目，然后导致开始使用 Visual Web Developer 的 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="4930a-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="4930a-134">屏幕的底部会出现一个通知，指示 ASP.NET 开发服务器已启动，并将显示在其下运行的端口号。</span><span class="sxs-lookup"><span data-stu-id="4930a-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="4930a-135">然后，Visual Web Developer 会自动打开其 URL 指向我们的 Web 服务器的浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="4930a-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="4930a-136">这样，我们就可以快速试用我们的 web 应用程序：</span><span class="sxs-lookup"><span data-stu-id="4930a-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="4930a-137">好了，这很简单–我们创建了一个新的网站，添加了一个三行函数，并且我们在浏览器中获得了文本。</span><span class="sxs-lookup"><span data-stu-id="4930a-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="4930a-138">不是火箭的，但它是一种开始。</span><span class="sxs-lookup"><span data-stu-id="4930a-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="4930a-139">*请注意，Visual Web Developer 包含 ASP.NET 开发服务器，它将以随机免费的 "端口" 号运行你的网站。在上面的屏幕截图中，站点正在 `http://localhost:26641/`上运行，因此使用的是端口26641。端口号会有所不同。当我们在本教程中讨论 URL （如/Store/Browse）时，将在端口号后发送。假设端口号为26641，浏览到/Store/Browse 将意味着浏览到 `http://localhost:26641/Store/Browse`。*</span><span class="sxs-lookup"><span data-stu-id="4930a-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="4930a-140">添加 StoreController</span><span class="sxs-lookup"><span data-stu-id="4930a-140">Adding a StoreController</span></span>

<span data-ttu-id="4930a-141">我们添加了一个简单的 HomeController，用于实现网站的主页。</span><span class="sxs-lookup"><span data-stu-id="4930a-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="4930a-142">现在，让我们添加另一个要用于实现音乐商店浏览功能的控制器。</span><span class="sxs-lookup"><span data-stu-id="4930a-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="4930a-143">我们的应用商店控制器将支持三个方案：</span><span class="sxs-lookup"><span data-stu-id="4930a-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="4930a-144">音乐应用商店中音乐流派的列表页</span><span class="sxs-lookup"><span data-stu-id="4930a-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="4930a-145">列出特定流派中所有音乐唱片集的浏览页</span><span class="sxs-lookup"><span data-stu-id="4930a-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="4930a-146">显示特定音乐唱片集相关信息的详细信息页</span><span class="sxs-lookup"><span data-stu-id="4930a-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="4930a-147">首先，我们将添加一个新的 StoreController 类。</span><span class="sxs-lookup"><span data-stu-id="4930a-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="4930a-148">如果尚未这样做，请通过关闭浏览器或选择 Debug ⇨停止调试菜单项来停止运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="4930a-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="4930a-149">现在，添加一个新 StoreController。</span><span class="sxs-lookup"><span data-stu-id="4930a-149">Now add a new StoreController.</span></span> <span data-ttu-id="4930a-150">与使用 HomeController 时一样，通过右键单击解决方案资源管理器中的 "控制器" 文件夹，然后选择 "&gt;控制器" 菜单项来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="4930a-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="4930a-151">新 StoreController 已有 "Index" 方法。</span><span class="sxs-lookup"><span data-stu-id="4930a-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="4930a-152">我们将使用此 "索引" 方法来实现列出音乐商店中所有流派的列表页。</span><span class="sxs-lookup"><span data-stu-id="4930a-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="4930a-153">我们还将添加另外两个方法来实现我们希望 StoreController 处理的其他两个方案：浏览和详细信息。</span><span class="sxs-lookup"><span data-stu-id="4930a-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="4930a-154">我们的控制器中的这些方法（索引、浏览和详细信息）称为 "控制器操作"，正如您已看到的 HomeController （）操作方法，其工作是响应 URL 请求，（一般而言，）确定哪些内容应发送回调用该 URL 的浏览器或用户。</span><span class="sxs-lookup"><span data-stu-id="4930a-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="4930a-155">我们将通过将 theIndex （）方法更改为返回字符串 "Hello from StoreController （）" 来开始我们的实现，我们将为浏览（）和详细信息（）添加类似的方法：</span><span class="sxs-lookup"><span data-stu-id="4930a-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="4930a-156">再次运行该项目，并浏览以下 Url：</span><span class="sxs-lookup"><span data-stu-id="4930a-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="4930a-157">/Store</span><span class="sxs-lookup"><span data-stu-id="4930a-157">/Store</span></span>
- <span data-ttu-id="4930a-158">/Store/Browse</span><span class="sxs-lookup"><span data-stu-id="4930a-158">/Store/Browse</span></span>
- <span data-ttu-id="4930a-159">/Store/Details</span><span class="sxs-lookup"><span data-stu-id="4930a-159">/Store/Details</span></span>

<span data-ttu-id="4930a-160">访问这些 Url 将调用控制器中的操作方法，并返回字符串响应：</span><span class="sxs-lookup"><span data-stu-id="4930a-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="4930a-161">这很好，但这只是常量字符串。</span><span class="sxs-lookup"><span data-stu-id="4930a-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="4930a-162">让我们将它们设置为动态，使其从 URL 获取信息并在页面输出中显示信息。</span><span class="sxs-lookup"><span data-stu-id="4930a-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="4930a-163">首先，我们将更改浏览操作方法，以从 URL 中检索查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="4930a-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="4930a-164">为此，我们可以将 "流派" 参数添加到操作方法。</span><span class="sxs-lookup"><span data-stu-id="4930a-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="4930a-165">当我们执行此操作时，MVC 会自动将名为 "流派" 的查询参数或窗体 post 参数传递给调用方法。</span><span class="sxs-lookup"><span data-stu-id="4930a-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="4930a-166">*注意：我们使用的是 Httputility.javascriptstringencode Server.htmlencode 实用工具方法来净化用户输入。这会阻止用户使用类似/Store/Browse 的链接向视图中注入 Javascript？流派 =&lt;脚本&gt;window。 location = "http://hackersite.com"&lt;/script&gt;。*</span><span class="sxs-lookup"><span data-stu-id="4930a-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="4930a-167">现在让我们浏览到/Store/Browse？流派 = Disco</span><span class="sxs-lookup"><span data-stu-id="4930a-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="4930a-168">接下来，请更改详细信息操作以读取和显示名为 ID 的输入参数。</span><span class="sxs-lookup"><span data-stu-id="4930a-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="4930a-169">与我们以前的方法不同，我们不会将 ID 值作为 querystring 参数嵌入。</span><span class="sxs-lookup"><span data-stu-id="4930a-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="4930a-170">相反，我们会直接将它嵌入到 URL 内。</span><span class="sxs-lookup"><span data-stu-id="4930a-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="4930a-171">例如：/Store/Details/5。</span><span class="sxs-lookup"><span data-stu-id="4930a-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="4930a-172">ASP.NET MVC 使我们无需配置任何内容即可轻松实现此目的。</span><span class="sxs-lookup"><span data-stu-id="4930a-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="4930a-173">ASP.NET MVC 的默认路由约定是将操作方法名称后面的 URL 段视为名为 "ID" 的参数。</span><span class="sxs-lookup"><span data-stu-id="4930a-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="4930a-174">如果操作方法有一个名为 ID 的参数，ASP.NET MVC 会自动将 URL 段作为参数传递给你。</span><span class="sxs-lookup"><span data-stu-id="4930a-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="4930a-175">运行应用程序并浏览到/Store/Details/5：</span><span class="sxs-lookup"><span data-stu-id="4930a-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="4930a-176">我们来回顾一下我们目前所做的事情：</span><span class="sxs-lookup"><span data-stu-id="4930a-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="4930a-177">我们已在 Visual Web Developer 中创建了新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="4930a-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="4930a-178">我们讨论了 ASP.NET MVC 应用程序的基本文件夹结构</span><span class="sxs-lookup"><span data-stu-id="4930a-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="4930a-179">我们已了解如何使用 ASP.NET 开发服务器</span><span class="sxs-lookup"><span data-stu-id="4930a-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="4930a-180">我们创建了两个控制器类： HomeController 和 StoreController</span><span class="sxs-lookup"><span data-stu-id="4930a-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="4930a-181">我们已向控制器添加了操作方法，这些方法可响应 URL 请求并向浏览器返回文本</span><span class="sxs-lookup"><span data-stu-id="4930a-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4930a-182">[上一页](mvc-music-store-part-1.md)
> [下一页](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="4930a-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
