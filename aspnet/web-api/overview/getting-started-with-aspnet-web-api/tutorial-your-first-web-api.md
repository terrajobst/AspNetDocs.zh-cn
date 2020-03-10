---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: 开始处理 ASP.NET Web API 2 （C#）-ASP.NET 4。x
author: MikeWasson
description: 代码教程。 使用 ASP.NET Web API 创建返回产品列表的 Web API。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448550"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="961b0-104">ASP.NET Web API 2 （C#）入门</span><span class="sxs-lookup"><span data-stu-id="961b0-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="961b0-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="961b0-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="961b0-106">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="961b0-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="961b0-107">在本教程中，你将使用 ASP.NET Web API 创建返回产品列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="961b0-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="961b0-108">HTTP 并非仅用于为网页提供服务。</span><span class="sxs-lookup"><span data-stu-id="961b0-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="961b0-109">HTTP 也是一个功能强大的平台，用于构建公开服务和数据的 Api。</span><span class="sxs-lookup"><span data-stu-id="961b0-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="961b0-110">HTTP 简单、灵活且无处不在。</span><span class="sxs-lookup"><span data-stu-id="961b0-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="961b0-111">几乎任何可以考虑的平台都有一个 HTTP 库，因此 HTTP 服务可以访问范围广泛的客户端，包括浏览器、移动设备和传统的桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="961b0-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="961b0-112">ASP.NET Web API 是一个用于在 .NET Framework 之上构建 Web API 的框架。</span><span class="sxs-lookup"><span data-stu-id="961b0-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="961b0-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="961b0-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="961b0-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="961b0-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="961b0-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="961b0-115">Web API 2</span></span>

<span data-ttu-id="961b0-116">有关本教程的更高版本，请参阅[使用 ASP.NET Core 和 Visual Studio For Windows 创建 WEB API](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 。</span><span class="sxs-lookup"><span data-stu-id="961b0-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="961b0-117">创建 Web API 项目</span><span class="sxs-lookup"><span data-stu-id="961b0-117">Create a Web API Project</span></span>

<span data-ttu-id="961b0-118">在本教程中，你将使用 ASP.NET Web API 创建返回产品列表的 Web API。</span><span class="sxs-lookup"><span data-stu-id="961b0-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="961b0-119">前端网页使用 jQuery 显示结果。</span><span class="sxs-lookup"><span data-stu-id="961b0-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="961b0-120">启动 Visual Studio，然后从**起始**页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="961b0-121">或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="961b0-122">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="961b0-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="961b0-123">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="961b0-124">在项目模板列表中，选择 " **ASP.NET Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="961b0-125">将项目命名为 "ProductsApp"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="961b0-126">在 "**新建 ASP.NET 项目**" 对话框中，选择 "**空**" 模板。</span><span class="sxs-lookup"><span data-stu-id="961b0-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="961b0-127">在 &quot;为&quot;添加文件夹和核心引用 "下，检查**WEB API**。</span><span class="sxs-lookup"><span data-stu-id="961b0-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="961b0-128">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="961b0-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="961b0-129">你还可以使用 &quot;Web API&quot; 模板创建 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="961b0-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="961b0-130">Web API 模板使用 ASP.NET MVC 提供 API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="961b0-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="961b0-131">我使用的是本教程的空模板，因为我想要显示没有 MVC 的 Web API。</span><span class="sxs-lookup"><span data-stu-id="961b0-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="961b0-132">一般情况下，不需要知道 ASP.NET MVC 即可使用 Web API。</span><span class="sxs-lookup"><span data-stu-id="961b0-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="961b0-133">添加模型</span><span class="sxs-lookup"><span data-stu-id="961b0-133">Adding a Model</span></span>

<span data-ttu-id="961b0-134">模型是表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="961b0-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="961b0-135">ASP.NET Web API 可以将模型自动序列化为 JSON、XML 或其他格式，然后将序列化的数据写入 HTTP 响应消息的正文中。</span><span class="sxs-lookup"><span data-stu-id="961b0-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="961b0-136">只要客户端可以读取序列化格式，它就可以反序列化该对象。</span><span class="sxs-lookup"><span data-stu-id="961b0-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="961b0-137">大多数客户端可以解析 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="961b0-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="961b0-138">而且，客户端可以通过在 HTTP 请求消息中设置 Accept 标头来指示它需要哪种格式。</span><span class="sxs-lookup"><span data-stu-id="961b0-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="961b0-139">首先，让我们创建一个表示产品的简单模型。</span><span class="sxs-lookup"><span data-stu-id="961b0-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="961b0-140">如果解决方案资源管理器尚未出现，请单击“视图”菜单，并选择“解决方案资源管理器”。</span><span class="sxs-lookup"><span data-stu-id="961b0-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="961b0-141">在解决方案资源管理器中，右键单击“模型”文件夹。</span><span class="sxs-lookup"><span data-stu-id="961b0-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="961b0-142">在上下文菜单中，依次选择“添加”、“类”。</span><span class="sxs-lookup"><span data-stu-id="961b0-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="961b0-143">将类命名为 &quot;产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="961b0-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="961b0-144">将以下属性添加到 `Product` 类。</span><span class="sxs-lookup"><span data-stu-id="961b0-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="961b0-145">添加控制器</span><span class="sxs-lookup"><span data-stu-id="961b0-145">Adding a Controller</span></span>

<span data-ttu-id="961b0-146">在 Web API 中，控制器是处理 HTTP 请求的对象。</span><span class="sxs-lookup"><span data-stu-id="961b0-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="961b0-147">我们将添加一个控制器，该控制器可返回产品列表或由 ID 指定的单个产品。</span><span class="sxs-lookup"><span data-stu-id="961b0-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="961b0-148">如果已使用 ASP.NET MVC，则已熟悉控制器。</span><span class="sxs-lookup"><span data-stu-id="961b0-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="961b0-149">Web API 控制器类似于 MVC 控制器，但继承了**ApiController**类而不是**Controller**类。</span><span class="sxs-lookup"><span data-stu-id="961b0-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="961b0-150">在“解决方案资源管理器”中，右键单击“控制器”文件夹。</span><span class="sxs-lookup"><span data-stu-id="961b0-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="961b0-151">依次选择“添加”、“控制器”。</span><span class="sxs-lookup"><span data-stu-id="961b0-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="961b0-152">在“添加基架”对话框中，选择“Web API 控制器 - 空”。</span><span class="sxs-lookup"><span data-stu-id="961b0-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="961b0-153">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="961b0-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="961b0-154">在 "**添加控制器**" 对话框中，将控制器命名为 &quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="961b0-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="961b0-155">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="961b0-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="961b0-156">基架会在 "控制器" 文件夹中创建一个名为 "ProductsController.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="961b0-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="961b0-157">不需要将控制器放入名为控制器的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="961b0-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="961b0-158">文件夹名称只是一种用于组织源文件的简便方法。</span><span class="sxs-lookup"><span data-stu-id="961b0-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="961b0-159">如果此文件尚未打开，请双击文件将其打开。</span><span class="sxs-lookup"><span data-stu-id="961b0-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="961b0-160">将此文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="961b0-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="961b0-161">为了使示例简单，产品存储在控制器类内的固定阵列中。</span><span class="sxs-lookup"><span data-stu-id="961b0-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="961b0-162">当然，在实际的应用程序中，您将查询数据库或使用其他外部数据源。</span><span class="sxs-lookup"><span data-stu-id="961b0-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="961b0-163">控制器定义了返回产品的两个方法：</span><span class="sxs-lookup"><span data-stu-id="961b0-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="961b0-164">`GetAllProducts` 方法将整个产品列表作为**IEnumerable&lt;产品&gt;** 类型返回。</span><span class="sxs-lookup"><span data-stu-id="961b0-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="961b0-165">`GetProduct` 方法按 ID 查找单个产品。</span><span class="sxs-lookup"><span data-stu-id="961b0-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="961b0-166">就这么简单！</span><span class="sxs-lookup"><span data-stu-id="961b0-166">That's it!</span></span> <span data-ttu-id="961b0-167">你有一个有效的 web API。</span><span class="sxs-lookup"><span data-stu-id="961b0-167">You have a working web API.</span></span> <span data-ttu-id="961b0-168">控制器上的每个方法都对应于一个或多个 Uri：</span><span class="sxs-lookup"><span data-stu-id="961b0-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="961b0-169">控制器方法</span><span class="sxs-lookup"><span data-stu-id="961b0-169">Controller Method</span></span> | <span data-ttu-id="961b0-170">URI</span><span class="sxs-lookup"><span data-stu-id="961b0-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="961b0-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="961b0-171">GetAllProducts</span></span> | <span data-ttu-id="961b0-172">/api/products</span><span class="sxs-lookup"><span data-stu-id="961b0-172">/api/products</span></span> |
| <span data-ttu-id="961b0-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="961b0-173">GetProduct</span></span> | <span data-ttu-id="961b0-174">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="961b0-174">/api/products/*id*</span></span> |

<span data-ttu-id="961b0-175">对于 `GetProduct` 方法，URI 中的*id*是占位符。</span><span class="sxs-lookup"><span data-stu-id="961b0-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="961b0-176">例如，若要获取 ID 为5的产品，请 `api/products/5`URI。</span><span class="sxs-lookup"><span data-stu-id="961b0-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="961b0-177">有关 Web API 如何将 HTTP 请求路由到控制器方法的详细信息，请参阅[中的路由 ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="961b0-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="961b0-178">通过 Javascript 和 jQuery 调用 Web API</span><span class="sxs-lookup"><span data-stu-id="961b0-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="961b0-179">在本部分中，我们将添加一个使用 AJAX 调用 web API 的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="961b0-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="961b0-180">我们将使用 jQuery 进行 AJAX 调用，并使用结果来更新页面。</span><span class="sxs-lookup"><span data-stu-id="961b0-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="961b0-181">在解决方案资源管理器中，右键单击项目并选择 "**添加**"，然后选择 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="961b0-182">在 "**添加新项**" 对话框中，选择 "**视觉对象C#** " 下的 " **Web** " 节点，然后选择 " **HTML" 页**项。</span><span class="sxs-lookup"><span data-stu-id="961b0-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="961b0-183">将该页命名为 &quot;&quot;的索引。</span><span class="sxs-lookup"><span data-stu-id="961b0-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="961b0-184">将此文件中的所有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="961b0-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="961b0-185">有多种方式可以获取 jQuery。</span><span class="sxs-lookup"><span data-stu-id="961b0-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="961b0-186">在此示例中，我使用了[Microsoft AJAX CDN](../../../ajax/cdn/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="961b0-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="961b0-187">你还可以从[http://jquery.com/](http://jquery.com/)下载它，ASP.NET 的 "Web API" 项目模板也包含 jQuery。</span><span class="sxs-lookup"><span data-stu-id="961b0-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="961b0-188">获取产品列表</span><span class="sxs-lookup"><span data-stu-id="961b0-188">Getting a List of Products</span></span>

<span data-ttu-id="961b0-189">若要获取产品列表，请将 HTTP GET 请求发送到 &quot;/api/products&quot;。</span><span class="sxs-lookup"><span data-stu-id="961b0-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="961b0-190">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/)函数发送 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="961b0-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="961b0-191">For response 包含 JSON 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="961b0-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="961b0-192">`done` 函数指定在请求成功时调用的回调。</span><span class="sxs-lookup"><span data-stu-id="961b0-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="961b0-193">在回调中，我们用产品信息更新 DOM。</span><span class="sxs-lookup"><span data-stu-id="961b0-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="961b0-194">按 ID 获取产品</span><span class="sxs-lookup"><span data-stu-id="961b0-194">Getting a Product By ID</span></span>

<span data-ttu-id="961b0-195">若要按 ID 获取产品，请将 HTTP GET 请求发送到 &quot;/api/products/*id*&quot;，其中*ID*为产品 id。</span><span class="sxs-lookup"><span data-stu-id="961b0-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="961b0-196">我们仍调用 `getJSON` 来发送 AJAX 请求，但这次我们将 ID 放在请求 URI 中。</span><span class="sxs-lookup"><span data-stu-id="961b0-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="961b0-197">此请求的响应是单个产品的 JSON 表示形式。</span><span class="sxs-lookup"><span data-stu-id="961b0-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="961b0-198">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="961b0-198">Running the Application</span></span>

<span data-ttu-id="961b0-199">按 F5 开始调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="961b0-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="961b0-200">网页应如下所示：</span><span class="sxs-lookup"><span data-stu-id="961b0-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="961b0-201">若要按 ID 获取产品，请输入 ID，然后单击 "搜索"：</span><span class="sxs-lookup"><span data-stu-id="961b0-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="961b0-202">如果输入的 ID 无效，服务器将返回 HTTP 错误：</span><span class="sxs-lookup"><span data-stu-id="961b0-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="961b0-203">使用 F12 查看 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="961b0-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="961b0-204">使用 HTTP 服务时，查看 HTTP 请求和请求消息可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="961b0-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="961b0-205">可以通过使用 Internet Explorer 9 中的 F12 开发人员工具来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="961b0-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="961b0-206">在 Internet Explorer 9 中，按**F12**打开工具。</span><span class="sxs-lookup"><span data-stu-id="961b0-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="961b0-207">单击 "**网络**" 选项卡，然后按 "**开始捕获**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="961b0-208">现在返回网页并按**F5**重新加载网页。</span><span class="sxs-lookup"><span data-stu-id="961b0-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="961b0-209">Internet Explorer 将捕获浏览器与 web 服务器之间的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="961b0-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="961b0-210">"摘要" 视图显示页面的所有网络流量：</span><span class="sxs-lookup"><span data-stu-id="961b0-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="961b0-211">找到相对 URI "api/products/" 的条目。</span><span class="sxs-lookup"><span data-stu-id="961b0-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="961b0-212">选择此条目，并单击 "**前往详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="961b0-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="961b0-213">在详细信息视图中，有选项卡可用于查看请求和响应标头和正文。</span><span class="sxs-lookup"><span data-stu-id="961b0-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="961b0-214">例如，如果单击 "**请求标头**" 选项卡，你可以看到客户端在 Accept 标头中请求 &quot;application/json&quot;。</span><span class="sxs-lookup"><span data-stu-id="961b0-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="961b0-215">如果单击 "响应正文" 选项卡，则可以看到如何将产品列表序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="961b0-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="961b0-216">其他浏览器具有类似的功能。</span><span class="sxs-lookup"><span data-stu-id="961b0-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="961b0-217">另一种有用的工具是[Fiddler](http://www.fiddler2.com/fiddler2/)，这是一个 web 调试代理。</span><span class="sxs-lookup"><span data-stu-id="961b0-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="961b0-218">你可以使用 Fiddler 来查看 HTTP 流量，还可以编写 HTTP 请求，这使你可以完全控制请求中的 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="961b0-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="961b0-219">查看此应用在 Azure 上运行</span><span class="sxs-lookup"><span data-stu-id="961b0-219">See this App Running on Azure</span></span>

<span data-ttu-id="961b0-220">要查看作为实时 web 应用运行的已完成站点吗？</span><span class="sxs-lookup"><span data-stu-id="961b0-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="961b0-221">只需单击以下按钮，即可将应用程序的完整版本部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="961b0-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="961b0-222">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="961b0-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="961b0-223">如果还没有帐户，可以使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="961b0-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="961b0-224">[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。</span><span class="sxs-lookup"><span data-stu-id="961b0-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="961b0-225">[激活 msdn 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-msdn 订阅每月提供可用于付费 Azure 服务的信用额度。</span><span class="sxs-lookup"><span data-stu-id="961b0-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="961b0-226">后续步骤</span><span class="sxs-lookup"><span data-stu-id="961b0-226">Next Steps</span></span>

- <span data-ttu-id="961b0-227">有关支持 POST、PUT 和 DELETE 操作以及写入数据库的 HTTP 服务的更完整示例，请参阅将[WEB API 2 与实体框架6一起使用](../data/using-web-api-with-entity-framework/part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="961b0-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="961b0-228">若要深入了解如何在 HTTP 服务的基础上创建流畅的响应式 web 应用程序，请参阅[ASP.NET 单页应用程序](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="961b0-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="961b0-229">有关如何将 Visual Studio web 项目部署到 Azure App Service 的信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="961b0-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
