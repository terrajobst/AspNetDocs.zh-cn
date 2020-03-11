---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: 配置 ASP.NET Web API 2 ASP.NET
author: MikeWasson
description: 为 ASP.NET 4.x 配置 ASP.NET Web API 2：配置设置、ASP.NET 1.x 托管、OWIN 自托管、全局服务和预控制器配置。
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449342"
---
# <a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="b03ba-103">配置 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="b03ba-103">Configuring ASP.NET Web API 2</span></span>

<span data-ttu-id="b03ba-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b03ba-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b03ba-105">本主题介绍如何配置 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="b03ba-105">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="b03ba-106">配置设置</span><span class="sxs-lookup"><span data-stu-id="b03ba-106">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="b03ba-107">配置包含 ASP.NET 托管的 Web API</span><span class="sxs-lookup"><span data-stu-id="b03ba-107">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="b03ba-108">配置包含 OWIN 自承载的 Web API</span><span class="sxs-lookup"><span data-stu-id="b03ba-108">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="b03ba-109">全局 Web API 服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-109">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="b03ba-110">每控制器配置</span><span class="sxs-lookup"><span data-stu-id="b03ba-110">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="b03ba-111">配置设置</span><span class="sxs-lookup"><span data-stu-id="b03ba-111">Configuration Settings</span></span>

<span data-ttu-id="b03ba-112">Web API 配置设置是在[HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)类中定义的。</span><span class="sxs-lookup"><span data-stu-id="b03ba-112">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="b03ba-113">成员</span><span class="sxs-lookup"><span data-stu-id="b03ba-113">Member</span></span> | <span data-ttu-id="b03ba-114">说明</span><span class="sxs-lookup"><span data-stu-id="b03ba-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b03ba-115">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="b03ba-115">**DependencyResolver**</span></span> | <span data-ttu-id="b03ba-116">启用控制器的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="b03ba-116">Enables dependency injection for controllers.</span></span> <span data-ttu-id="b03ba-117">请参阅[使用 WEB API 依赖关系解析程序](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-117">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="b03ba-118">**过滤器**</span><span class="sxs-lookup"><span data-stu-id="b03ba-118">**Filters**</span></span> | <span data-ttu-id="b03ba-119">操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-119">Action filters.</span></span> |
| <span data-ttu-id="b03ba-120">**程序**</span><span class="sxs-lookup"><span data-stu-id="b03ba-120">**Formatters**</span></span> | <span data-ttu-id="b03ba-121">[媒体类型格式化程序](../formats-and-model-binding/media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-121">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="b03ba-122">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="b03ba-122">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="b03ba-123">指定服务器是否应在 HTTP 响应消息中包含错误详细信息，例如异常消息和堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="b03ba-123">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="b03ba-124">请参阅[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))。</span><span class="sxs-lookup"><span data-stu-id="b03ba-124">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="b03ba-125">**初始值设定项**</span><span class="sxs-lookup"><span data-stu-id="b03ba-125">**Initializer**</span></span> | <span data-ttu-id="b03ba-126">一个函数，该函数执行**HttpConfiguration**的最终初始化。</span><span class="sxs-lookup"><span data-stu-id="b03ba-126">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="b03ba-127">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="b03ba-127">**MessageHandlers**</span></span> | <span data-ttu-id="b03ba-128">[HTTP 消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-128">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="b03ba-129">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="b03ba-129">**ParameterBindingRules**</span></span> | <span data-ttu-id="b03ba-130">用于绑定控制器操作上的参数的规则的集合。</span><span class="sxs-lookup"><span data-stu-id="b03ba-130">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="b03ba-131">**属性**</span><span class="sxs-lookup"><span data-stu-id="b03ba-131">**Properties**</span></span> | <span data-ttu-id="b03ba-132">泛型属性包。</span><span class="sxs-lookup"><span data-stu-id="b03ba-132">A generic property bag.</span></span> |
| <span data-ttu-id="b03ba-133">**路由**</span><span class="sxs-lookup"><span data-stu-id="b03ba-133">**Routes**</span></span> | <span data-ttu-id="b03ba-134">路由的集合。</span><span class="sxs-lookup"><span data-stu-id="b03ba-134">The collection of routes.</span></span> <span data-ttu-id="b03ba-135">请参阅[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-135">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="b03ba-136">**服务**</span><span class="sxs-lookup"><span data-stu-id="b03ba-136">**Services**</span></span> | <span data-ttu-id="b03ba-137">服务的集合。</span><span class="sxs-lookup"><span data-stu-id="b03ba-137">The collection of services.</span></span> <span data-ttu-id="b03ba-138">请参阅[服务](#services)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-138">See [Services](#services).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="b03ba-139">系统必备</span><span class="sxs-lookup"><span data-stu-id="b03ba-139">Prerequisites</span></span>

<span data-ttu-id="b03ba-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional 或 Enterprise 版本。</span><span class="sxs-lookup"><span data-stu-id="b03ba-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="b03ba-141">配置包含 ASP.NET 托管的 Web API</span><span class="sxs-lookup"><span data-stu-id="b03ba-141">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="b03ba-142">在 ASP.NET 应用程序中，通过在**应用程序\_Start**方法中调用[GLOBALCONFIGURATION](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx)配置 Web API。</span><span class="sxs-lookup"><span data-stu-id="b03ba-142">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="b03ba-143">**Configure**方法使用一个委托，该委托具有一个类型为**HttpConfiguration**的参数。</span><span class="sxs-lookup"><span data-stu-id="b03ba-143">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="b03ba-144">在委托内执行所有配置。</span><span class="sxs-lookup"><span data-stu-id="b03ba-144">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="b03ba-145">下面是一个使用匿名委托的示例：</span><span class="sxs-lookup"><span data-stu-id="b03ba-145">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="b03ba-146">在 Visual Studio 2017 中，如果在 "**新建 ASP.NET 项目**" 对话框中选择 "Web API"，则 "ASP.NET Web 应用程序" 项目模板会自动设置配置代码。</span><span class="sxs-lookup"><span data-stu-id="b03ba-146">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="b03ba-147">项目模板在应用\_启动文件夹内创建名为 "WebApiConfig.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="b03ba-147">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="b03ba-148">此代码文件定义委托，你应在其中放置你的 Web API 配置代码。</span><span class="sxs-lookup"><span data-stu-id="b03ba-148">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="b03ba-149">项目模板还将从应用程序中调用委托的代码添加 **\_Start**。</span><span class="sxs-lookup"><span data-stu-id="b03ba-149">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="b03ba-150">配置包含 OWIN 自承载的 Web API</span><span class="sxs-lookup"><span data-stu-id="b03ba-150">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="b03ba-151">如果你是使用 OWIN 自承载的，则创建一个新的**HttpConfiguration**实例。</span><span class="sxs-lookup"><span data-stu-id="b03ba-151">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="b03ba-152">对此实例执行任何配置，然后将该实例传递给**Owin. UseWebApi**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="b03ba-152">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="b03ba-153">教程[使用 OWIN 到自承载 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)显示完整步骤。</span><span class="sxs-lookup"><span data-stu-id="b03ba-153">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="b03ba-154">全局 Web API 服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-154">Global Web API Services</span></span>

<span data-ttu-id="b03ba-155">**HttpConfiguration**集合包含一组全局服务，Web API 使用这些服务来执行各种任务，如控制器选择和内容协商。</span><span class="sxs-lookup"><span data-stu-id="b03ba-155">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="b03ba-156">**服务**集合不是用于服务发现或依赖关系注入的通用机制。</span><span class="sxs-lookup"><span data-stu-id="b03ba-156">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="b03ba-157">它仅存储 Web API 框架已知的服务类型。</span><span class="sxs-lookup"><span data-stu-id="b03ba-157">It only stores service types that are known to the Web API framework.</span></span>

<span data-ttu-id="b03ba-158">**服务**集合使用一组默认服务进行初始化，你可以提供自己的自定义实现。</span><span class="sxs-lookup"><span data-stu-id="b03ba-158">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="b03ba-159">某些服务支持多个实例，而其他服务只能有一个实例。</span><span class="sxs-lookup"><span data-stu-id="b03ba-159">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="b03ba-160">（但是，还可以在控制器级别提供服务，请参阅[按控制器配置](#percontrollerconfig)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-160">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="b03ba-161">单实例服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-161">Single-Instance Services</span></span>

| <span data-ttu-id="b03ba-162">服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-162">Service</span></span> | <span data-ttu-id="b03ba-163">说明</span><span class="sxs-lookup"><span data-stu-id="b03ba-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b03ba-164">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="b03ba-164">**IActionValueBinder**</span></span> | <span data-ttu-id="b03ba-165">获取参数的绑定。</span><span class="sxs-lookup"><span data-stu-id="b03ba-165">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="b03ba-166">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="b03ba-166">**IApiExplorer**</span></span> | <span data-ttu-id="b03ba-167">获取应用程序公开的 Api 的说明。</span><span class="sxs-lookup"><span data-stu-id="b03ba-167">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="b03ba-168">请参阅[创建 WEB API 的帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-168">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="b03ba-169">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="b03ba-169">**IAssembliesResolver**</span></span> | <span data-ttu-id="b03ba-170">获取应用程序的程序集的列表。</span><span class="sxs-lookup"><span data-stu-id="b03ba-170">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="b03ba-171">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-171">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="b03ba-172">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="b03ba-172">**IBodyModelValidator**</span></span> | <span data-ttu-id="b03ba-173">验证媒体类型格式化程序从请求正文读取的模型。</span><span class="sxs-lookup"><span data-stu-id="b03ba-173">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="b03ba-174">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="b03ba-174">**IContentNegotiator**</span></span> | <span data-ttu-id="b03ba-175">执行内容协商。</span><span class="sxs-lookup"><span data-stu-id="b03ba-175">Performs content negotiation.</span></span> |
| <span data-ttu-id="b03ba-176">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="b03ba-176">**IDocumentationProvider**</span></span> | <span data-ttu-id="b03ba-177">提供 Api 的文档。</span><span class="sxs-lookup"><span data-stu-id="b03ba-177">Provides documentation for APIs.</span></span> <span data-ttu-id="b03ba-178">默认值为 **null**。</span><span class="sxs-lookup"><span data-stu-id="b03ba-178">The default is **null**.</span></span> <span data-ttu-id="b03ba-179">请参阅[创建 WEB API 的帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-179">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="b03ba-180">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="b03ba-180">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="b03ba-181">指示宿主是否应缓冲 HTTP 消息实体正文。</span><span class="sxs-lookup"><span data-stu-id="b03ba-181">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="b03ba-182">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="b03ba-182">**IHttpActionInvoker**</span></span> | <span data-ttu-id="b03ba-183">调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b03ba-183">Invokes a controller action.</span></span> <span data-ttu-id="b03ba-184">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-184">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="b03ba-185">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="b03ba-185">**IHttpActionSelector**</span></span> | <span data-ttu-id="b03ba-186">选择控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b03ba-186">Selects a controller action.</span></span> <span data-ttu-id="b03ba-187">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-187">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="b03ba-188">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="b03ba-188">**IHttpControllerActivator**</span></span> | <span data-ttu-id="b03ba-189">激活控制器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-189">Activates a controller.</span></span> <span data-ttu-id="b03ba-190">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-190">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="b03ba-191">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="b03ba-191">**IHttpControllerSelector**</span></span> | <span data-ttu-id="b03ba-192">选择控制器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-192">Selects a controller.</span></span> <span data-ttu-id="b03ba-193">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-193">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="b03ba-194">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="b03ba-194">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="b03ba-195">提供应用程序中的 Web API 控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="b03ba-195">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="b03ba-196">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-196">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="b03ba-197">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="b03ba-197">**ITraceManager**</span></span> | <span data-ttu-id="b03ba-198">初始化跟踪框架。</span><span class="sxs-lookup"><span data-stu-id="b03ba-198">Initializes the tracing framework.</span></span> <span data-ttu-id="b03ba-199">请参阅[ASP.NET Web API 中的跟踪](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-199">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="b03ba-200">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="b03ba-200">**ITraceWriter**</span></span> | <span data-ttu-id="b03ba-201">提供跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-201">Provides a trace writer.</span></span> <span data-ttu-id="b03ba-202">默认值为 "无操作" 跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-202">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="b03ba-203">请参阅[ASP.NET Web API 中的跟踪](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="b03ba-203">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="b03ba-204">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="b03ba-204">**IModelValidatorCache**</span></span> | <span data-ttu-id="b03ba-205">提供模型验证程序的缓存。</span><span class="sxs-lookup"><span data-stu-id="b03ba-205">Provides a cache of model validators.</span></span> |

<span data-ttu-id="b03ba-206">多实例服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-206">Multiple-Instance Services</span></span>

|                 <span data-ttu-id="b03ba-207">服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-207">Service</span></span>                 |                                                                                                              <span data-ttu-id="b03ba-208">说明</span><span class="sxs-lookup"><span data-stu-id="b03ba-208">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <span data-ttu-id="b03ba-209"><strong>IFilterProvider</strong></span><span class="sxs-lookup"><span data-stu-id="b03ba-209"><strong>IFilterProvider</strong></span></span>     |                                                                                           <span data-ttu-id="b03ba-210">返回控制器操作的筛选器列表。</span><span class="sxs-lookup"><span data-stu-id="b03ba-210">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <span data-ttu-id="b03ba-211"><strong>ModelBinderProvider</strong></span><span class="sxs-lookup"><span data-stu-id="b03ba-211"><strong>ModelBinderProvider</strong></span></span>   |                                                                                                <span data-ttu-id="b03ba-212">返回给定类型的模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="b03ba-212">Returns a model binder for a given type.</span></span>                                                                                                |
| <span data-ttu-id="b03ba-213"><strong>ModelMetadataProvider</strong></span><span class="sxs-lookup"><span data-stu-id="b03ba-213"><strong>ModelMetadataProvider</strong></span></span>  |                                                                                                     <span data-ttu-id="b03ba-214">提供模型的元数据。</span><span class="sxs-lookup"><span data-stu-id="b03ba-214">Provides metadata for a model.</span></span>                                                                                                     |
| <span data-ttu-id="b03ba-215"><strong>ModelValidatorProvider</strong></span><span class="sxs-lookup"><span data-stu-id="b03ba-215"><strong>ModelValidatorProvider</strong></span></span> |                                                                                                   <span data-ttu-id="b03ba-216">为模型提供验证程序。</span><span class="sxs-lookup"><span data-stu-id="b03ba-216">Provides a validator for a model.</span></span>                                                                                                    |
|  <span data-ttu-id="b03ba-217"><strong>ValueProviderFactory</strong></span><span class="sxs-lookup"><span data-stu-id="b03ba-217"><strong>ValueProviderFactory</strong></span></span>  | <span data-ttu-id="b03ba-218">创建值提供程序。</span><span class="sxs-lookup"><span data-stu-id="b03ba-218">Creates a value provider.</span></span> <span data-ttu-id="b03ba-219">有关详细信息，请参阅 Mike 停止项博客文章[如何在 WebAPI 中创建自定义值提供程序](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="b03ba-219">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="b03ba-220">若要将自定义实现添加到多实例服务，请调用**服务**集合上的**add**或**Insert** ：</span><span class="sxs-lookup"><span data-stu-id="b03ba-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="b03ba-221">若要将单实例服务替换为自定义实现，请调用**服务**集合上的**replace** ：</span><span class="sxs-lookup"><span data-stu-id="b03ba-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="b03ba-222">每控制器配置</span><span class="sxs-lookup"><span data-stu-id="b03ba-222">Per-Controller Configuration</span></span>

<span data-ttu-id="b03ba-223">您可以基于每个控制器重写以下设置：</span><span class="sxs-lookup"><span data-stu-id="b03ba-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="b03ba-224">媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="b03ba-224">Media-type formatters</span></span>
- <span data-ttu-id="b03ba-225">参数绑定规则</span><span class="sxs-lookup"><span data-stu-id="b03ba-225">Parameter binding rules</span></span>
- <span data-ttu-id="b03ba-226">服务</span><span class="sxs-lookup"><span data-stu-id="b03ba-226">Services</span></span>

<span data-ttu-id="b03ba-227">为此，请定义一个实现**IControllerConfiguration**接口的自定义特性。</span><span class="sxs-lookup"><span data-stu-id="b03ba-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="b03ba-228">然后将属性应用到控制器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="b03ba-229">下面的示例使用自定义格式化程序替换默认的媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="b03ba-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="b03ba-230">**IControllerConfiguration**方法采用两个参数：</span><span class="sxs-lookup"><span data-stu-id="b03ba-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="b03ba-231">**HttpControllerSettings**对象</span><span class="sxs-lookup"><span data-stu-id="b03ba-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="b03ba-232">**HttpControllerDescriptor**对象</span><span class="sxs-lookup"><span data-stu-id="b03ba-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="b03ba-233">**HttpControllerDescriptor**包含控制器的说明，你可以检查该说明以提供信息，以便区分两个控制器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="b03ba-234">使用**HttpControllerSettings**对象配置控制器。</span><span class="sxs-lookup"><span data-stu-id="b03ba-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="b03ba-235">此对象包含可以基于每个控制器重写的配置参数的子集。</span><span class="sxs-lookup"><span data-stu-id="b03ba-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="b03ba-236">默认情况下，不会更改为全局**HttpConfiguration**对象的任何设置。</span><span class="sxs-lookup"><span data-stu-id="b03ba-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
