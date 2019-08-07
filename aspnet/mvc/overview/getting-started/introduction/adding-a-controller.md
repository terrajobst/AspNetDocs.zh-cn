---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810775"
---
# <a name="adding-a-controller"></a><span data-ttu-id="785f9-102">添加控制器</span><span class="sxs-lookup"><span data-stu-id="785f9-102">Adding a Controller</span></span>

<span data-ttu-id="785f9-103">作者: [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="785f9-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="785f9-104">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="785f9-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="785f9-105">MVC 是用于开发应用程序的一种模式, 该模式设计良好、可测试且易于维护。</span><span class="sxs-lookup"><span data-stu-id="785f9-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="785f9-106">基于 MVC 的应用程序包含:</span><span class="sxs-lookup"><span data-stu-id="785f9-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="785f9-107">**M**模式:类, 这些类表示应用程序的数据, 并使用验证逻辑来强制执行该数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="785f9-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="785f9-108">**V**视图:应用程序用于动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="785f9-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="785f9-109">**C**控制器:处理传入浏览器请求、检索模型数据, 然后指定将响应返回到浏览器的视图模板的类。</span><span class="sxs-lookup"><span data-stu-id="785f9-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="785f9-110">我们将在本系列教程中介绍所有这些概念, 并向您演示如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="785f9-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="785f9-111">首先, 让我们创建一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="785f9-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="785f9-112">在**解决方案资源管理器**中, 右键单击 "*控制器*" 文件夹, 然后依次单击 "**添加**"、"**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="785f9-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="785f9-113">在 "**添加基架**" 对话框中, 单击 " **MVC 5 控制器-空**", 然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="785f9-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="785f9-114">将新控制器命名为 "HelloWorldController", 并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="785f9-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![添加控制器](adding-a-controller/_static/image3.png)

<span data-ttu-id="785f9-116">请注意,**解决方案资源管理器**创建了一个名为*HelloWorldController.cs*的新文件和一个新的文件夹*Views\HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="785f9-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="785f9-117">控制器在 IDE 中处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="785f9-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="785f9-118">将该文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="785f9-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="785f9-119">控制器方法将以 HTML 形式返回一个字符串作为示例。</span><span class="sxs-lookup"><span data-stu-id="785f9-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="785f9-120">控制器名`HelloWorldController`为, 第一种方法名为`Index`。</span><span class="sxs-lookup"><span data-stu-id="785f9-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="785f9-121">让我们从浏览器中调用它。</span><span class="sxs-lookup"><span data-stu-id="785f9-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="785f9-122">运行应用程序 (按 F5 或 Ctrl + F5)。</span><span class="sxs-lookup"><span data-stu-id="785f9-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="785f9-123">在浏览器中, &quot;将&quot; HelloWorld 追加到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="785f9-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="785f9-124">(例如, 在下图中, 它是`http://localhost:1234/HelloWorld.`) 浏览器中的页面将类似于以下屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="785f9-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="785f9-125">在上面的方法中, 代码直接返回了一个字符串。</span><span class="sxs-lookup"><span data-stu-id="785f9-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="785f9-126">你已告诉系统只返回了一些 HTML, 但确实返回了!</span><span class="sxs-lookup"><span data-stu-id="785f9-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="785f9-127">ASP.NET MVC 根据传入 URL 调用不同的控制器类 (以及其中的不同操作方法)。</span><span class="sxs-lookup"><span data-stu-id="785f9-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="785f9-128">ASP.NET MVC 使用的默认 URL 路由逻辑使用如下格式来确定要调用的代码:</span><span class="sxs-lookup"><span data-stu-id="785f9-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="785f9-129">在*应用\_启动/RouteConfig*文件中设置路由格式。</span><span class="sxs-lookup"><span data-stu-id="785f9-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="785f9-130">当你运行应用程序但不提供任何 URL 段时, 它将默认为 "Home" 控制器和上述代码的 "默认值" 部分中指定的 "索引" 操作方法。</span><span class="sxs-lookup"><span data-stu-id="785f9-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="785f9-131">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="785f9-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="785f9-132">因此, */HelloWorld*映射到`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="785f9-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="785f9-133">URL 的第二部分确定要执行的类的操作方法。</span><span class="sxs-lookup"><span data-stu-id="785f9-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="785f9-134">因此, */HelloWorld/Index*将导致`Index`执行`HelloWorldController`类的方法。</span><span class="sxs-lookup"><span data-stu-id="785f9-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="785f9-135">请注意, 我们只需要浏览到 */HelloWorld* , 并`Index`在默认情况下使用该方法。</span><span class="sxs-lookup"><span data-stu-id="785f9-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="785f9-136">这是因为, 名`Index`为的方法是将在控制器上调用的默认方法, 如果未显式指定一个方法。</span><span class="sxs-lookup"><span data-stu-id="785f9-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="785f9-137">URL 段的第三部分 (`Parameters`) 针对的是路由数据。</span><span class="sxs-lookup"><span data-stu-id="785f9-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="785f9-138">稍后, 我们将在本教程中看到路由数据。</span><span class="sxs-lookup"><span data-stu-id="785f9-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="785f9-139">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="785f9-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="785f9-140">此方法将运行并返回该&quot;字符串, 这是欢迎操作方法 ... `Welcome`&quot;.</span><span class="sxs-lookup"><span data-stu-id="785f9-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="785f9-141">默认 MVC 映射为`/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="785f9-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="785f9-142">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="785f9-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="785f9-143">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="785f9-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="785f9-144">让我们略微修改该示例, 以便可以将一些参数信息从 URL 传递到控制器 (例如, */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="785f9-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="785f9-145">`Welcome`将方法更改为包含两个参数, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="785f9-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="785f9-146">请注意, 该代码使用C#可选的参数功能, 指示如果没有`numTimes`为该参数传递值, 则该参数应默认为1。</span><span class="sxs-lookup"><span data-stu-id="785f9-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="785f9-147">安全说明:上面的代码使用[httputility.javascriptstringencode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)保护应用程序免受恶意输入 (即 JavaScript) 的攻击。</span><span class="sxs-lookup"><span data-stu-id="785f9-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="785f9-148">有关详细信息，请参阅[操作说明：通过将 HTML 编码应用于字符串](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)来防范 Web 应用程序中的脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="785f9-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="785f9-149">运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`)。</span><span class="sxs-lookup"><span data-stu-id="785f9-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="785f9-150">可在 URL 中对 `name` 和 `numtimes` 使用其他值。</span><span class="sxs-lookup"><span data-stu-id="785f9-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="785f9-151">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数从地址栏中的查询字符串映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="785f9-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="785f9-152">在上面的示例中, 未使用 URL `Parameters`段 () `name` , 且和`numTimes`参数作为[查询字符串](http://en.wikipedia.org/wiki/Query_string)进行传递。</span><span class="sxs-lookup"><span data-stu-id="785f9-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="785f9-153">?</span><span class="sxs-lookup"><span data-stu-id="785f9-153">The ?</span></span> <span data-ttu-id="785f9-154">上述 URL 中的 (问号) 是一个分隔符, 查询字符串如下所示。</span><span class="sxs-lookup"><span data-stu-id="785f9-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="785f9-155">&amp; 字符用于分隔查询字符串。</span><span class="sxs-lookup"><span data-stu-id="785f9-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="785f9-156">将欢迎方法替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="785f9-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="785f9-157">运行应用程序并输入以下 URL:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="785f9-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="785f9-158">这次第三个 URL 段与 route 参数`ID.`匹配`Welcome`时, 操作方法包含与`ID` `RegisterRoutes`方法中的 URL 规范匹配的参数 ()。</span><span class="sxs-lookup"><span data-stu-id="785f9-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="785f9-159">在 ASP.NET MVC 应用程序中, 更常见的做法是将参数作为路由数据 (就像上面的 ID 那样) 传递到查询字符串。</span><span class="sxs-lookup"><span data-stu-id="785f9-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="785f9-160">你还可以添加路由, 以将`name`和`numtimes`传入参数作为 URL 中的路由数据。</span><span class="sxs-lookup"><span data-stu-id="785f9-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="785f9-161">在*App\_Start\RouteConfig.cs*文件中, 添加 "Hello" 路由:</span><span class="sxs-lookup"><span data-stu-id="785f9-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="785f9-162">运行应用程序并浏览到`/localhost:XXX/HelloWorld/Welcome/Scott/3`。</span><span class="sxs-lookup"><span data-stu-id="785f9-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="785f9-163">对于许多 MVC 应用程序而言, 默认路由是正常的。</span><span class="sxs-lookup"><span data-stu-id="785f9-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="785f9-164">你将在本教程的后面部分了解如何使用模型绑定器传递数据, 并且你无需修改该的默认路由。</span><span class="sxs-lookup"><span data-stu-id="785f9-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="785f9-165">在这些示例中, 控制器已执行&quot;MVC 的 VC&quot;部分, 即视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="785f9-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="785f9-166">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="785f9-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="785f9-167">通常情况下, 你不希望控制器直接返回 HTML, 因为这会对代码非常麻烦。</span><span class="sxs-lookup"><span data-stu-id="785f9-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="785f9-168">我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="785f9-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="785f9-169">接下来, 我们来看看如何实现此目的。</span><span class="sxs-lookup"><span data-stu-id="785f9-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="785f9-170">[上一页](getting-started.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="785f9-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
