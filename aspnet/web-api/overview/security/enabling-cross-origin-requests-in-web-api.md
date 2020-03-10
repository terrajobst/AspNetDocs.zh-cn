---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: 在 ASP.NET Web API 2 中启用跨域请求 |Microsoft Docs
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中支持跨域资源共享（CORS）。
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447614"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="e736b-103">在 ASP.NET Web API 2 中启用跨域请求</span><span class="sxs-lookup"><span data-stu-id="e736b-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="e736b-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e736b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="e736b-105">浏览器安全策略阻止 Web 页向另一个域发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="e736b-106">此限制称为*相同源策略*，可防止恶意站点读取另一个站点中的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="e736b-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="e736b-107">但是，有时你可能希望让其他站点调用你的 web API。</span><span class="sxs-lookup"><span data-stu-id="e736b-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="e736b-108">[跨源资源共享](http://www.w3.org/TR/cors/)（CORS）是一种 W3C 标准，允许服务器放松相同的源策略。</span><span class="sxs-lookup"><span data-stu-id="e736b-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="e736b-109">使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="e736b-110">CORS 比早期技术（如[JSONP](http://en.wikipedia.org/wiki/JSONP)）更安全且更灵活。</span><span class="sxs-lookup"><span data-stu-id="e736b-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="e736b-111">本教程演示如何在 Web API 应用程序中启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="e736b-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="e736b-112">本教程中使用的软件</span><span class="sxs-lookup"><span data-stu-id="e736b-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="e736b-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e736b-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="e736b-114">Web API 2。2</span><span class="sxs-lookup"><span data-stu-id="e736b-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="e736b-115">简介</span><span class="sxs-lookup"><span data-stu-id="e736b-115">Introduction</span></span>

<span data-ttu-id="e736b-116">本教程演示 ASP.NET Web API 中的 CORS 支持。</span><span class="sxs-lookup"><span data-stu-id="e736b-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="e736b-117">首先，我们将创建两个 ASP.NET 项目-一个名为 "WebService"，它托管一个 Web API 控制器，另一个称为 "WebClient"，后者调用 WebService。</span><span class="sxs-lookup"><span data-stu-id="e736b-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="e736b-118">由于这两个应用程序托管在不同的域中，因此从 WebClient 到 WebService 的 AJAX 请求是一个跨源请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="e736b-119">什么是 "相同来源"？</span><span class="sxs-lookup"><span data-stu-id="e736b-119">What is "same origin"?</span></span>

<span data-ttu-id="e736b-120">如果两个 Url 具有相同的方案、主机和端口，则它们具有相同的源。</span><span class="sxs-lookup"><span data-stu-id="e736b-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="e736b-121">（[RFC 6454](http://tools.ietf.org/html/rfc6454)）</span><span class="sxs-lookup"><span data-stu-id="e736b-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="e736b-122">这两个 Url 具有相同的源：</span><span class="sxs-lookup"><span data-stu-id="e736b-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="e736b-123">这些 Url 的来源不同于前两个 Url：</span><span class="sxs-lookup"><span data-stu-id="e736b-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="e736b-124">`http://example.net`-不同域</span><span class="sxs-lookup"><span data-stu-id="e736b-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="e736b-125">`http://example.com:9000/foo.html`-不同端口</span><span class="sxs-lookup"><span data-stu-id="e736b-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="e736b-126">`https://example.com/foo.html`-不同方案</span><span class="sxs-lookup"><span data-stu-id="e736b-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="e736b-127">`http://www.example.com/foo.html`-不同子域</span><span class="sxs-lookup"><span data-stu-id="e736b-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="e736b-128">比较来源时，Internet Explorer 不会考虑该端口。</span><span class="sxs-lookup"><span data-stu-id="e736b-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="e736b-129">创建 WebService 项目</span><span class="sxs-lookup"><span data-stu-id="e736b-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="e736b-130">本部分假设你已了解如何创建 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="e736b-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="e736b-131">否则，请参阅[ASP.NET Web API 入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e736b-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="e736b-132">启动 Visual Studio 并创建一个新的**ASP.NET Web 应用程序（.NET Framework）** 项目。</span><span class="sxs-lookup"><span data-stu-id="e736b-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="e736b-133">在 "**新建 ASP.NET Web 应用程序**" 对话框中，选择 "**空**项目" 模板。</span><span class="sxs-lookup"><span data-stu-id="e736b-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="e736b-134">在 "**添加文件夹和核心引用**" 下，选择 " **Web API** " 复选框。</span><span class="sxs-lookup"><span data-stu-id="e736b-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio 中的新 ASP.NET 项目对话框](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="e736b-136">使用以下代码添加名为 `TestController` 的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="e736b-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="e736b-137">可以在本地运行应用程序或将其部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="e736b-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="e736b-138">（对于本教程中的屏幕截图，应用程序部署到 Azure App Service Web Apps。）若要验证 web API 是否正常工作，请导航到 `http://hostname/api/test/`，其中*hostname*是部署应用程序的域。</span><span class="sxs-lookup"><span data-stu-id="e736b-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="e736b-139">应会看到响应文本，&quot;获取：测试消息&quot;。</span><span class="sxs-lookup"><span data-stu-id="e736b-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![显示测试消息的 Web 浏览器](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="e736b-141">创建 WebClient 项目</span><span class="sxs-lookup"><span data-stu-id="e736b-141">Create the WebClient project</span></span>

1. <span data-ttu-id="e736b-142">创建另一个 " **ASP.NET Web 应用程序（.NET Framework）** " 项目，然后选择 " **MVC**项目" 模板。</span><span class="sxs-lookup"><span data-stu-id="e736b-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="e736b-143">（可选）选择 "**更改身份验证** > **无身份验证**"。</span><span class="sxs-lookup"><span data-stu-id="e736b-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="e736b-144">对于本教程，不需要进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e736b-144">You don't need authentication for this tutorial.</span></span>

   ![Visual Studio 中 "新建 ASP.NET 项目" 对话框中的 MVC 模板](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="e736b-146">在**解决方案资源管理器**中，打开文件*视图/Home/索引。*</span><span class="sxs-lookup"><span data-stu-id="e736b-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="e736b-147">将此文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e736b-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="e736b-148">对于*serviceUrl*变量，请使用 web 应用程序的 URI。</span><span class="sxs-lookup"><span data-stu-id="e736b-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="e736b-149">在本地运行 WebClient 应用程序或将其发布到其他网站。</span><span class="sxs-lookup"><span data-stu-id="e736b-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="e736b-150">单击 "试用" 按钮时，将使用下拉框中列出的 HTTP 方法（GET、POST 或 PUT）将 AJAX 请求提交到 WebService 应用。</span><span class="sxs-lookup"><span data-stu-id="e736b-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="e736b-151">这使你可以检查不同的跨域请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="e736b-152">目前，WebService 应用不支持 CORS，因此，如果单击该按钮，则会出现错误。</span><span class="sxs-lookup"><span data-stu-id="e736b-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![浏览器中的 "尝试" 错误](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="e736b-154">如果在类似于[Fiddler](https://www.telerik.com/fiddler)的工具中观看 HTTP 流量，你会发现浏览器确实发送了 GET 请求，而请求成功，但是 AJAX 调用返回错误。</span><span class="sxs-lookup"><span data-stu-id="e736b-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="e736b-155">请务必了解，同源策略不会阻止浏览器*发送*请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="e736b-156">相反，它会阻止应用程序查看*响应*。</span><span class="sxs-lookup"><span data-stu-id="e736b-156">Instead, it prevents the application from seeing the *response*.</span></span>

![显示 web 请求的 Fiddler web 调试器](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="e736b-158">启用 CORS</span><span class="sxs-lookup"><span data-stu-id="e736b-158">Enable CORS</span></span>

<span data-ttu-id="e736b-159">现在，让我们在 WebService 应用中启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="e736b-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="e736b-160">首先，添加 CORS NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e736b-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="e736b-161">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="e736b-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="e736b-162">在 "程序包管理器控制台" 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e736b-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="e736b-163">此命令安装最新包并更新所有依赖项，包括核心 Web API 库。</span><span class="sxs-lookup"><span data-stu-id="e736b-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="e736b-164">使用 `-Version` 标志来面向特定版本。</span><span class="sxs-lookup"><span data-stu-id="e736b-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="e736b-165">CORS 包需要 Web API 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="e736b-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="e736b-166">打开文件*应用\_Start/webapiconfig.cs*。</span><span class="sxs-lookup"><span data-stu-id="e736b-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="e736b-167">将以下代码添加到**webapiconfig.cs**方法：</span><span class="sxs-lookup"><span data-stu-id="e736b-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="e736b-168">接下来，将 **[EnableCors]** 特性添加到 `TestController` 类：</span><span class="sxs-lookup"><span data-stu-id="e736b-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="e736b-169">对于 "源 *" 参数，* 请使用你在其中部署了 WebClient 应用程序的 URI。</span><span class="sxs-lookup"><span data-stu-id="e736b-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="e736b-170">这允许来自 WebClient 的跨源请求，同时仍不允许所有其他跨域请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="e736b-171">稍后，我将更详细地介绍 **[EnableCors]** 的参数。</span><span class="sxs-lookup"><span data-stu-id="e736b-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="e736b-172">请勿在*源 URL 末尾*包含正斜杠。</span><span class="sxs-lookup"><span data-stu-id="e736b-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="e736b-173">重新部署更新的 WebService 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e736b-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="e736b-174">无需更新 WebClient。</span><span class="sxs-lookup"><span data-stu-id="e736b-174">You don't need to update WebClient.</span></span> <span data-ttu-id="e736b-175">现在，来自 WebClient 的 AJAX 请求应成功。</span><span class="sxs-lookup"><span data-stu-id="e736b-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="e736b-176">GET、PUT 和 POST 方法都是允许的。</span><span class="sxs-lookup"><span data-stu-id="e736b-176">The GET, PUT, and POST methods are all allowed.</span></span>

![显示成功测试消息的 Web 浏览器](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="e736b-178">CORS 如何工作</span><span class="sxs-lookup"><span data-stu-id="e736b-178">How CORS Works</span></span>

<span data-ttu-id="e736b-179">本部分说明 CORS 请求中 HTTP 消息级别发生的情况。</span><span class="sxs-lookup"><span data-stu-id="e736b-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="e736b-180">了解 CORS 的工作原理很重要，这样您就可以正确配置 **[EnableCors]** 属性，并在出现问题时进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="e736b-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="e736b-181">CORS 规范引入了几个新的 HTTP 标头，它们启用了跨域请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="e736b-182">如果浏览器支持 CORS，则会自动为跨域请求设置这些标头;不需要在 JavaScript 代码中执行任何特殊操作。</span><span class="sxs-lookup"><span data-stu-id="e736b-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="e736b-183">下面是一个跨源请求的示例。</span><span class="sxs-lookup"><span data-stu-id="e736b-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="e736b-184">"源" 标头将为发出请求的站点提供域。</span><span class="sxs-lookup"><span data-stu-id="e736b-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="e736b-185">如果服务器允许该请求，则会设置访问控制允许源标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="e736b-186">此标头的值可以与源标头匹配，也可以是通配符值 "\*"，表示允许任何源。</span><span class="sxs-lookup"><span data-stu-id="e736b-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="e736b-187">如果响应不包括访问控制允许源标头，则 AJAX 请求会失败。</span><span class="sxs-lookup"><span data-stu-id="e736b-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="e736b-188">具体而言，浏览器不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="e736b-189">即使服务器返回成功的响应，浏览器也不会将响应提供给客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="e736b-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="e736b-190">**预检请求**</span><span class="sxs-lookup"><span data-stu-id="e736b-190">**Preflight Requests**</span></span>

<span data-ttu-id="e736b-191">对于某些 CORS 请求，浏览器会在发送资源的实际请求之前发送一个称为 "预检请求" 的附加请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="e736b-192">如果满足以下条件，浏览器可以跳过预检请求：</span><span class="sxs-lookup"><span data-stu-id="e736b-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="e736b-193">请求方法为*GET、HEAD 或 POST，*</span><span class="sxs-lookup"><span data-stu-id="e736b-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="e736b-194">应用程序不会设置接受、接受语言、内容语言、内容类型或最后事件 ID*之外的任何*请求标头，</span><span class="sxs-lookup"><span data-stu-id="e736b-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="e736b-195">Content-type 标头（如果已设置）是下列其中一项：</span><span class="sxs-lookup"><span data-stu-id="e736b-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="e736b-196">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="e736b-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="e736b-197">多部分/窗体数据</span><span class="sxs-lookup"><span data-stu-id="e736b-197">multipart/form-data</span></span>
    - <span data-ttu-id="e736b-198">text/plain</span><span class="sxs-lookup"><span data-stu-id="e736b-198">text/plain</span></span>

<span data-ttu-id="e736b-199">有关请求标头的规则适用于应用程序通过对**XMLHttpRequest**对象调用**setRequestHeader**而设置的标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="e736b-200">（CORS 规范调用这些 "作者请求标头"。）此规则不适用于*浏览器*可以设置的标头，例如用户代理、主机或内容长度。</span><span class="sxs-lookup"><span data-stu-id="e736b-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="e736b-201">下面是预检请求的示例：</span><span class="sxs-lookup"><span data-stu-id="e736b-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="e736b-202">预航班请求使用 HTTP OPTIONS 方法。</span><span class="sxs-lookup"><span data-stu-id="e736b-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="e736b-203">它包括两个特殊标头：</span><span class="sxs-lookup"><span data-stu-id="e736b-203">It includes two special headers:</span></span>

- <span data-ttu-id="e736b-204">访问控制-请求-方法：将用于实际请求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="e736b-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="e736b-205">访问控制-请求标头：*应用程序*在实际请求上设置的请求标头的列表。</span><span class="sxs-lookup"><span data-stu-id="e736b-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="e736b-206">（同样，这不包含浏览器设置的标头。）</span><span class="sxs-lookup"><span data-stu-id="e736b-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="e736b-207">下面是一个示例响应，假设服务器允许该请求：</span><span class="sxs-lookup"><span data-stu-id="e736b-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="e736b-208">响应包括一个访问控制允许方法标头，该标头列出了允许的方法，并且可以选择一个用于列出允许的标头的访问控制允许标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="e736b-209">如果预检请求成功，则浏览器将发送实际请求，如前文所述。</span><span class="sxs-lookup"><span data-stu-id="e736b-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="e736b-210">默认情况下，用于测试具有预检选项请求的终结点的工具（例如， [Fiddler](https://www.telerik.com/fiddler)和[Postman](https://www.getpostman.com/)）默认情况下不发送所需的选项标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="e736b-211">确认 `Access-Control-Request-Method` 和 `Access-Control-Request-Headers` 标头与请求一起发送，并且选项标头通过 IIS 到达应用。</span><span class="sxs-lookup"><span data-stu-id="e736b-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="e736b-212">若要将 IIS 配置为允许 ASP.NET 应用接收和处理选项请求，请将以下配置添加到 `<system.webServer><handlers>` 部分*中的应用的 web.config 文件中*：</span><span class="sxs-lookup"><span data-stu-id="e736b-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="e736b-213">删除 `OPTIONSVerbHandler` 会阻止 IIS 处理选项请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="e736b-214">替换 `ExtensionlessUrlHandler-Integrated-4.0` 允许选项请求访问应用，因为默认模块注册只允许 GET、HEAD、POST 和调试请求与无扩展名 Url。</span><span class="sxs-lookup"><span data-stu-id="e736b-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="e736b-215">[EnableCors] 的作用域规则</span><span class="sxs-lookup"><span data-stu-id="e736b-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="e736b-216">你可以为应用程序中的所有 Web API 控制器启用每个操作、每个控制器或全局的 CORS。</span><span class="sxs-lookup"><span data-stu-id="e736b-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="e736b-217">**按操作**</span><span class="sxs-lookup"><span data-stu-id="e736b-217">**Per Action**</span></span>

<span data-ttu-id="e736b-218">若要为单个操作启用 CORS，请在操作方法上设置 **[EnableCors]** 属性。</span><span class="sxs-lookup"><span data-stu-id="e736b-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="e736b-219">下面的示例仅为 `GetItem` 方法启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="e736b-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="e736b-220">**每个控制器**</span><span class="sxs-lookup"><span data-stu-id="e736b-220">**Per Controller**</span></span>

<span data-ttu-id="e736b-221">如果在控制器类上设置 **[EnableCors]** ，则将其应用于控制器上的所有操作。</span><span class="sxs-lookup"><span data-stu-id="e736b-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="e736b-222">若要为某个操作禁用 CORS，请将 **[DisableCors]** 特性添加到该操作。</span><span class="sxs-lookup"><span data-stu-id="e736b-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="e736b-223">下面的示例为除 `PutItem`以外的每种方法启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="e736b-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="e736b-224">**全面**</span><span class="sxs-lookup"><span data-stu-id="e736b-224">**Globally**</span></span>

<span data-ttu-id="e736b-225">若要为应用程序中的所有 Web API 控制器启用 CORS，请将**EnableCorsAttribute**实例传递到**EnableCors**方法：</span><span class="sxs-lookup"><span data-stu-id="e736b-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="e736b-226">如果在多个作用域上设置属性，则优先顺序为：</span><span class="sxs-lookup"><span data-stu-id="e736b-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="e736b-227">操作</span><span class="sxs-lookup"><span data-stu-id="e736b-227">Action</span></span>
2. <span data-ttu-id="e736b-228">控制器</span><span class="sxs-lookup"><span data-stu-id="e736b-228">Controller</span></span>
3. <span data-ttu-id="e736b-229">Global</span><span class="sxs-lookup"><span data-stu-id="e736b-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="e736b-230">设置允许的来源</span><span class="sxs-lookup"><span data-stu-id="e736b-230">Set the allowed origins</span></span>

<span data-ttu-id="e736b-231">**[EnableCors]** *属性的源参数指定*允许哪些来源访问该资源。</span><span class="sxs-lookup"><span data-stu-id="e736b-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="e736b-232">该值是允许的来源的以逗号分隔的列表。</span><span class="sxs-lookup"><span data-stu-id="e736b-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="e736b-233">你还可以使用通配符值 "\*" 允许来自任何来源的请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="e736b-234">在允许来自任何来源的请求之前，请仔细考虑。</span><span class="sxs-lookup"><span data-stu-id="e736b-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="e736b-235">这意味着，任何网站都可以对 web API 进行 AJAX 调用。</span><span class="sxs-lookup"><span data-stu-id="e736b-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="e736b-236">设置允许的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="e736b-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="e736b-237">**[EnableCors]** 特性的*方法*参数指定了允许哪些 HTTP 方法访问该资源。</span><span class="sxs-lookup"><span data-stu-id="e736b-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="e736b-238">若要允许所有方法，请使用通配符值 "\*"。</span><span class="sxs-lookup"><span data-stu-id="e736b-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="e736b-239">下面的示例只允许 GET 和 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="e736b-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="e736b-240">设置允许的请求标头</span><span class="sxs-lookup"><span data-stu-id="e736b-240">Set the allowed request headers</span></span>

<span data-ttu-id="e736b-241">本文前面介绍了预检请求可能包含一个访问控制请求标头，其中列出了应用程序设置的 HTTP 标头（所谓的 "作者请求标头"）。</span><span class="sxs-lookup"><span data-stu-id="e736b-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="e736b-242">**[EnableCors]** 特性的*标头*参数指定允许的作者请求标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="e736b-243">若要允许任何标头，请将*标头*设置为 "\*"。</span><span class="sxs-lookup"><span data-stu-id="e736b-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="e736b-244">若要将特定标头列入允许列表，请将*标头*设置为允许的标头的逗号分隔列表：</span><span class="sxs-lookup"><span data-stu-id="e736b-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="e736b-245">但是，浏览器在设置访问控制-请求标头的方式上并不完全一致。</span><span class="sxs-lookup"><span data-stu-id="e736b-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="e736b-246">例如，Chrome 当前包含 "源"。</span><span class="sxs-lookup"><span data-stu-id="e736b-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="e736b-247">FireFox 不包含标准标头（如 "Accept"），即使应用程序在脚本中设置这些标头也是如此。</span><span class="sxs-lookup"><span data-stu-id="e736b-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="e736b-248">如果将*标头*设置为 "\*" 以外的任何内容，则至少应包含 "accept"、"content-type" 和 "源"，以及要支持的任何自定义标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="e736b-249">设置允许的响应标头</span><span class="sxs-lookup"><span data-stu-id="e736b-249">Set the allowed response headers</span></span>

<span data-ttu-id="e736b-250">默认情况下，浏览器不会向应用程序公开所有的响应标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="e736b-251">默认情况下可用的响应标头包括：</span><span class="sxs-lookup"><span data-stu-id="e736b-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="e736b-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="e736b-252">Cache-Control</span></span>
- <span data-ttu-id="e736b-253">Content-Language</span><span class="sxs-lookup"><span data-stu-id="e736b-253">Content-Language</span></span>
- <span data-ttu-id="e736b-254">Content-Type</span><span class="sxs-lookup"><span data-stu-id="e736b-254">Content-Type</span></span>
- <span data-ttu-id="e736b-255">Expires</span><span class="sxs-lookup"><span data-stu-id="e736b-255">Expires</span></span>
- <span data-ttu-id="e736b-256">上次修改时间</span><span class="sxs-lookup"><span data-stu-id="e736b-256">Last-Modified</span></span>
- <span data-ttu-id="e736b-257">杂</span><span class="sxs-lookup"><span data-stu-id="e736b-257">Pragma</span></span>

<span data-ttu-id="e736b-258">CORS 规范调用这些[简单的响应标头](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)。</span><span class="sxs-lookup"><span data-stu-id="e736b-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="e736b-259">若要使其他标头可用于应用程序，请设置 **[EnableCors]** 的*exposedHeaders*参数。</span><span class="sxs-lookup"><span data-stu-id="e736b-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="e736b-260">在下面的示例中，控制器的 `Get` 方法设置名为 "X-自定义标头" 的自定义标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="e736b-261">默认情况下，浏览器不会在跨域请求中公开此标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="e736b-262">若要使标头可用，请在*exposedHeaders*中包含 "X-自定义标头"。</span><span class="sxs-lookup"><span data-stu-id="e736b-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="e736b-263">传递跨源请求中的凭据</span><span class="sxs-lookup"><span data-stu-id="e736b-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="e736b-264">凭据需要在 CORS 请求中进行特殊处理。</span><span class="sxs-lookup"><span data-stu-id="e736b-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="e736b-265">默认情况下，浏览器不会发送包含跨域请求的任何凭据。</span><span class="sxs-lookup"><span data-stu-id="e736b-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="e736b-266">凭据包括 cookie 和 HTTP 身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="e736b-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="e736b-267">若要使用跨域请求发送凭据，客户端必须将**XMLHttpRequest**设置为 true。</span><span class="sxs-lookup"><span data-stu-id="e736b-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="e736b-268">直接使用**XMLHttpRequest** ：</span><span class="sxs-lookup"><span data-stu-id="e736b-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="e736b-269">在 jQuery 中：</span><span class="sxs-lookup"><span data-stu-id="e736b-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="e736b-270">此外，服务器必须允许凭据。</span><span class="sxs-lookup"><span data-stu-id="e736b-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="e736b-271">若要在 Web API 中允许跨域凭据，请在 **[EnableCors]** 特性上将**SupportsCredentials**属性设置为 true：</span><span class="sxs-lookup"><span data-stu-id="e736b-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="e736b-272">如果此属性为 true，则 HTTP 响应将包含一个访问控制允许凭据标头。</span><span class="sxs-lookup"><span data-stu-id="e736b-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="e736b-273">此标头通知浏览器服务器允许跨源请求的凭据。</span><span class="sxs-lookup"><span data-stu-id="e736b-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="e736b-274">如果浏览器发送凭据，但响应不包含有效的 "访问控制-允许-凭据" 标头，则浏览器将不会向应用程序公开响应，而且 AJAX 请求会失败。</span><span class="sxs-lookup"><span data-stu-id="e736b-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="e736b-275">将**SupportsCredentials**设置为 true 时要小心，因为这意味着另一个域中的网站可以代表用户将登录用户的凭据发送到 Web API，而不知道用户。</span><span class="sxs-lookup"><span data-stu-id="e736b-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="e736b-276">CORS 规范还指出，如果**SupportsCredentials**为 true，则将 &quot;\*&quot;*的设置为*无效。</span><span class="sxs-lookup"><span data-stu-id="e736b-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="e736b-277">自定义 CORS 策略提供程序</span><span class="sxs-lookup"><span data-stu-id="e736b-277">Custom CORS policy providers</span></span>

<span data-ttu-id="e736b-278">**[EnableCors]** 特性实现**ICorsPolicyProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="e736b-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="e736b-279">您可以通过创建从**Attribute**派生的类并实现**ICorsPolicyProvider**来提供自己的实现。</span><span class="sxs-lookup"><span data-stu-id="e736b-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="e736b-280">现在，你可以将该属性应用于要放置 **[EnableCors]** 的任何位置。</span><span class="sxs-lookup"><span data-stu-id="e736b-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="e736b-281">例如，自定义 CORS 策略提供程序可以从配置文件中读取设置。</span><span class="sxs-lookup"><span data-stu-id="e736b-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="e736b-282">作为使用特性的替代方法，可以注册创建**ICorsPolicyProvider**对象的**ICorsPolicyProviderFactory**对象。</span><span class="sxs-lookup"><span data-stu-id="e736b-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="e736b-283">若要设置**ICorsPolicyProviderFactory**，请在启动时调用**SetCorsPolicyProviderFactory**扩展方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e736b-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="e736b-284">浏览器支持</span><span class="sxs-lookup"><span data-stu-id="e736b-284">Browser support</span></span>

<span data-ttu-id="e736b-285">Web API CORS 包是一种服务器端技术。</span><span class="sxs-lookup"><span data-stu-id="e736b-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="e736b-286">用户的浏览器还需要支持 CORS。</span><span class="sxs-lookup"><span data-stu-id="e736b-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="e736b-287">幸运的是，所有主流浏览器的当前版本都[支持 CORS](http://caniuse.com/cors)。</span><span class="sxs-lookup"><span data-stu-id="e736b-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
