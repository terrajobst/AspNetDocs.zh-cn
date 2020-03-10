---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: 了解 ASP.NET AJAX 身份验证和配置文件应用程序服务 |Microsoft Docs
author: scottcate
description: 身份验证服务允许用户提供凭据以便接收身份验证 cookie，而网关服务则允许自定义用户 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520310"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="3f5d2-103">了解 ASP.NET AJAX 身份验证和配置文件应用程序服务</span><span class="sxs-lookup"><span data-stu-id="3f5d2-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>

<span data-ttu-id="3f5d2-104">作者： [Scott Cate](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="3f5d2-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="3f5d2-105">Download PDF</span></span>](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="3f5d2-106">身份验证服务允许用户提供凭据以便接收身份验证 cookie，而网关服务则允许由 ASP.NET 提供的自定义用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="3f5d2-107">ASP.NET AJAX authentication 服务的使用与标准 ASP.NET Forms 身份验证兼容，因此，当前使用窗体身份验证的应用程序（如使用登录控件）不会通过升级到 AJAX 身份验证服务而被破坏。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

## <a name="introduction"></a><span data-ttu-id="3f5d2-108">简介</span><span class="sxs-lookup"><span data-stu-id="3f5d2-108">Introduction</span></span>

<span data-ttu-id="3f5d2-109">作为 .NET Framework 3.5 的一部分，Microsoft 提供了一个可调整大小的环境升级;不仅可以使用新的开发环境，而且还会推出新的语言集成查询（LINQ）功能和其他语言增强功能。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="3f5d2-110">此外，其他工具集的一些熟悉的功能（特别是 ASP.NET AJAX 扩展）将作为 .NET Framework 基类库的第一类成员包括在内。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="3f5d2-111">这些扩展可实现许多新的丰富客户端功能，包括页面的部分呈现，无需整页刷新、通过客户端脚本访问 Web 服务的能力（包括 ASP.NET 分析 API）和广泛的客户端 API用于镜像在 ASP.NET 服务器端控制集内发现的许多控制方案。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="3f5d2-112">本白皮书介绍了如何实现和使用 ASP.NET 分析和 Forms 身份验证服务，因为它们由 Microsoft ASP.NET AJAX ExtensionsThe AJAX 扩展公开，从而使窗体身份验证非常易于支持（以及分析服务）通过 Web 服务代理脚本公开。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="3f5d2-113">AJAX 扩展还支持通过 AuthenticationServiceManager 类进行自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="3f5d2-114">本白皮书基于 Visual Studio 2008 和 .NET Framework 3.5 的 Beta 2 版本。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="3f5d2-115">本白皮书还假设你将使用 Visual Studio 2008 Beta 2，而不是 Visual Web Developer Express，并将根据 Visual Studio 的用户界面提供演练。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="3f5d2-116">一些代码示例可能使用 Visual Web Developer 速成版中不可用的项目模板。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="3f5d2-117">*配置文件和身份验证*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="3f5d2-118">Microsoft ASP.NET 配置文件和身份验证服务由 ASP.NET Forms 身份验证系统提供，并且是 ASP.NET 的标准组件。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="3f5d2-119">ASP.NET AJAX 扩展通过脚本代理提供对这些服务的脚本访问，这些服务通过客户端 AJAX 库的 Sys.databases 命名空间下非常简单的模型。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="3f5d2-120">身份验证服务允许用户提供凭据以便接收身份验证 cookie，而网关服务则允许由 ASP.NET 提供的自定义用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="3f5d2-121">ASP.NET AJAX authentication 服务的使用与标准 ASP.NET Forms 身份验证兼容，因此，当前使用窗体身份验证的应用程序（如使用登录控件）不会通过升级到 AJAX 身份验证服务而被破坏。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="3f5d2-122">配置文件服务允许根据身份验证服务提供的成员资格自动集成和存储用户数据。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="3f5d2-123">存储的数据由 web.config 文件指定，各种分析服务提供程序处理数据管理。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="3f5d2-124">对于身份验证服务，AJAX 配置文件服务与标准 ASP.NET 配置文件服务兼容，因此，当前合并 ASP.NET 配置文件服务的功能的页面不应通过包含 AJAX 支持来断开。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="3f5d2-125">将 ASP.NET Authentication 和分析服务本身并入应用程序不在此白皮书的讨论范围内。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="3f5d2-126">有关该主题的详细信息，请参阅 MSDN 库参考文章使用[https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)的成员身份管理用户。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx).</span></span> <span data-ttu-id="3f5d2-127">ASP.NET 还包括一个实用工具，用于自动设置 SQL Server 的成员身份，这是 ASP.NET 成员身份的默认身份验证服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="3f5d2-128">有关详细信息，请参阅文章 ASP.NET SQL Server 注册工具（Aspnet\_regsql），网址为[https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="3f5d2-129">*使用 ASP.NET AJAX 身份验证服务*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="3f5d2-130">必须在 web.config 文件中启用 ASP.NET AJAX 身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="3f5d2-131">身份验证服务需要启用 ASP.NET Forms 身份验证，并要求在客户端浏览器上启用 cookie （脚本无法启用无 cookie 会话，因为无 cookie 会话需要 URL 参数）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="3f5d2-132">启用并配置 AJAX 身份验证服务后，客户端脚本可以立即利用 AuthenticationService 对象。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="3f5d2-133">首先，客户端脚本将需要利用 `login` 方法和 `isLoggedIn` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="3f5d2-134">存在多个属性以为登录方法提供默认值，该方法可以接受大量的参数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="3f5d2-135">*AuthenticationService 成员*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="3f5d2-136">*登录方法：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-136">*login method:*</span></span>

<span data-ttu-id="3f5d2-137">Login （）方法开始对用户凭据进行身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="3f5d2-138">此方法是异步的，不会阻止执行。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="3f5d2-139">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-139">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-140">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-140">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-141">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-142">userName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-142">userName</span></span> | <span data-ttu-id="3f5d2-143">必须的。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-143">Required.</span></span> <span data-ttu-id="3f5d2-144">要进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-144">The username to authenticate.</span></span> |
| <span data-ttu-id="3f5d2-145">密码</span><span class="sxs-lookup"><span data-stu-id="3f5d2-145">password</span></span> | <span data-ttu-id="3f5d2-146">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-146">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-147">用户的密码。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-147">The user's password.</span></span> |
| <span data-ttu-id="3f5d2-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="3f5d2-148">isPersistent</span></span> | <span data-ttu-id="3f5d2-149">可选（默认值为 false）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-149">Optional (defaults to false).</span></span> <span data-ttu-id="3f5d2-150">用户的身份验证 cookie 是否应跨会话保留。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="3f5d2-151">如果为 false，则用户将在浏览器关闭或会话过期时注销。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="3f5d2-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="3f5d2-152">redirectUrl</span></span> | <span data-ttu-id="3f5d2-153">可选（默认为 null）。身份验证成功后要将浏览器重定向到的 URL。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="3f5d2-154">如果此参数为 null 或空字符串，则不会发生重定向。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="3f5d2-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="3f5d2-155">customInfo</span></span> | <span data-ttu-id="3f5d2-156">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-156">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-157">此参数当前未使用，保留供将来使用。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="3f5d2-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-158">loginCompletedCallback</span></span> | <span data-ttu-id="3f5d2-159">可选（默认为 null）。登录成功完成时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="3f5d2-160">如果指定此参数，则此参数将覆盖 defaultLoginCompleted 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="3f5d2-161">failedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-161">failedCallback</span></span> | <span data-ttu-id="3f5d2-162">可选（默认为 null）。登录失败时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="3f5d2-163">如果指定此参数，则此参数将覆盖 defaultFailedCallback 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="3f5d2-164">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-164">userContext</span></span> | <span data-ttu-id="3f5d2-165">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-165">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-166">应传递给回调函数的自定义用户上下文数据。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="3f5d2-167">*返回值：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-167">*Return Value:*</span></span>

<span data-ttu-id="3f5d2-168">此函数不包括返回值。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-168">This function does not include a return value.</span></span> <span data-ttu-id="3f5d2-169">但是，在调用此函数时，将包括多个行为：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="3f5d2-170">如果 `redirectUrl` 参数既不为 null 也不是空字符串，则将刷新或更改当前页。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="3f5d2-171">但是，如果参数为 null 或空字符串，则调用 `loginCompletedCallback` 参数或 `defaultLoginCompletedCallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="3f5d2-172">如果对 web 服务的调用失败，则调用 `defaultFailedCallback` 属性的 `failedCallback` 参数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="3f5d2-173">*注销方法：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-173">*logout method:*</span></span>

<span data-ttu-id="3f5d2-174">注销（）方法将删除凭据 cookie，并从 web 应用程序注销当前用户。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="3f5d2-175">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-175">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-176">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-176">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-177">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="3f5d2-178">redirectUrl</span></span> | <span data-ttu-id="3f5d2-179">可选（默认为 null）。身份验证成功后要将浏览器重定向到的 URL。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="3f5d2-180">如果此参数为 null 或空字符串，则不会发生重定向。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="3f5d2-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-181">logoutCompletedCallback</span></span> | <span data-ttu-id="3f5d2-182">可选（默认为 null）。已成功完成注销时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="3f5d2-183">如果指定此参数，则此参数将覆盖 defaultLogoutCompleted 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="3f5d2-184">failedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-184">failedCallback</span></span> | <span data-ttu-id="3f5d2-185">可选（默认为 null）。登录失败时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="3f5d2-186">如果指定此参数，则此参数将覆盖 defaultFailedCallback 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="3f5d2-187">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-187">userContext</span></span> | <span data-ttu-id="3f5d2-188">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-188">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-189">应传递给回调函数的自定义用户上下文数据。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="3f5d2-190">*返回值：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-190">*Return Value:*</span></span>

<span data-ttu-id="3f5d2-191">此函数不包括返回值。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-191">This function does not include a return value.</span></span> <span data-ttu-id="3f5d2-192">但是，在调用此函数时，将包括多个行为：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="3f5d2-193">如果 `redirectUrl` 参数既不为 null 也不是空字符串，则将刷新或更改当前页。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="3f5d2-194">但是，如果参数为 null 或空字符串，则调用 `logoutCompletedCallback` 参数或 `defaultLogoutCompletedCallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="3f5d2-195">如果对 web 服务的调用失败，则调用 `defaultFailedCallback` 属性的 `failedCallback` 参数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="3f5d2-196">*defaultFailedCallback 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="3f5d2-197">此属性指定在无法与 web 服务进行通信的情况下应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="3f5d2-198">它应收到委托（或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="3f5d2-199">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="3f5d2-200">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-200">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-201">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-201">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-202">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-203">error</span><span class="sxs-lookup"><span data-stu-id="3f5d2-203">error</span></span> | <span data-ttu-id="3f5d2-204">指定错误信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-204">Specifies the error information.</span></span> |
| <span data-ttu-id="3f5d2-205">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-205">userContext</span></span> | <span data-ttu-id="3f5d2-206">指定在调用登录或注销函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="3f5d2-207">methodName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-207">methodName</span></span> | <span data-ttu-id="3f5d2-208">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-208">The name of the calling method.</span></span> |

<span data-ttu-id="3f5d2-209">*defaultLoginCompletedCallback 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="3f5d2-210">此属性指定一个函数，该函数应在登录 web 服务调用完成时调用。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="3f5d2-211">它应收到委托（或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="3f5d2-212">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="3f5d2-213">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-213">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-214">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-214">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-215">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-216">validCredentials</span><span class="sxs-lookup"><span data-stu-id="3f5d2-216">validCredentials</span></span> | <span data-ttu-id="3f5d2-217">指定用户提供的凭据是否有效。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="3f5d2-218">`true` 如果用户成功登录，则为; 否则为。否则 `false`。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="3f5d2-219">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-219">userContext</span></span> | <span data-ttu-id="3f5d2-220">指定在调用登录函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="3f5d2-221">methodName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-221">methodName</span></span> | <span data-ttu-id="3f5d2-222">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-222">The name of the calling method.</span></span> |

<span data-ttu-id="3f5d2-223">*defaultLogoutCompletedCallback 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="3f5d2-224">此属性指定一个函数，该函数应在注销 web 服务调用完成时调用。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="3f5d2-225">它应收到委托（或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="3f5d2-226">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="3f5d2-227">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-227">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-228">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-228">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-229">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-230">result</span><span class="sxs-lookup"><span data-stu-id="3f5d2-230">result</span></span> | <span data-ttu-id="3f5d2-231">此参数将始终 `null`;它保留供将来使用。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="3f5d2-232">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-232">userContext</span></span> | <span data-ttu-id="3f5d2-233">指定在调用登录函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="3f5d2-234">methodName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-234">methodName</span></span> | <span data-ttu-id="3f5d2-235">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-235">The name of the calling method.</span></span> |

<span data-ttu-id="3f5d2-236">*isLoggedIn 属性（get）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="3f5d2-237">此属性获取用户的当前身份验证状态;它在页面请求期间由 ScriptManager 对象设置。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="3f5d2-238">如果用户当前已登录，此属性将返回 `true`;否则，它将返回 `false`。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="3f5d2-239">*path 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-239">*path property (get, set):*</span></span>

<span data-ttu-id="3f5d2-240">此属性以编程方式确定身份验证 web 服务的位置。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="3f5d2-241">它可用于重写默认的身份验证提供程序，以及在 ScriptManager 控件的 AuthenticationService 子节点的 Path 属性中以声明方式设置的一个身份验证提供程序（有关详细信息，请参阅使用自定义身份验证服务提供程序主题）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="3f5d2-242">请注意，默认身份验证服务的位置不会更改。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="3f5d2-243">但是，ASP.NET AJAX 允许你指定 web 服务的位置，该服务提供与 ASP.NET AJAX authentication service proxy 相同的类接口。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="3f5d2-244">另请注意，不应将此属性设置为将脚本请求定向到当前站点之外的值。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="3f5d2-245">因为当前应用程序不会接收到身份验证凭据，所以它毫无用处;此外，基础 AJAX 不应发布跨站点请求，并且可能会在客户端浏览器中产生安全异常。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="3f5d2-246">此属性是一个 `String` 对象，表示身份验证 web 服务的路径。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="3f5d2-247">*timeout 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="3f5d2-248">此属性确定登录请求失败之前等待身份验证服务的时间长度。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="3f5d2-249">如果在等待调用完成时超时时间已到，则会调用请求失败回调，并且调用将无法完成。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="3f5d2-250">此属性是一个表示从身份验证服务等待结果的毫秒数的 `Number` 对象。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="3f5d2-251">*代码示例：登录到身份验证服务*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="3f5d2-252">以下标记是一个示例 ASP.NET 页面，其中包含对 AuthenticationService 类的登录和注销方法的简单脚本调用。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="3f5d2-253">通过 AJAX 访问 ASP.NET 分析数据</span><span class="sxs-lookup"><span data-stu-id="3f5d2-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="3f5d2-254">ASP.NET 分析服务也通过 ASP.NET AJAX 扩展公开。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="3f5d2-255">由于 ASP.NET 分析服务提供了一个用于存储和检索用户数据的丰富、精细的 API，因此这可能是一个出色的工作效率工具。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="3f5d2-256">必须在 web.config 中启用配置文件服务;默认情况下，它不是。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="3f5d2-257">为此，请确保在 web.config 中指定了 `profileService` 的子元素 = true，并且已指定可以读取或写入的属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="3f5d2-258">还必须配置配置文件服务。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-258">The profile service must also be configured.</span></span> <span data-ttu-id="3f5d2-259">尽管分析服务的配置不在本白皮书的范围内，但值得注意的是，配置文件配置设置中定义的组将可作为组名称的子属性进行访问。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="3f5d2-260">例如，如果指定了以下配置文件节：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="3f5d2-261">客户端脚本将能够访问名称、地址. Line1、第二行、Address、address、address 和 BackgroundColor 作为 ProfileService 类的属性字段的属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="3f5d2-262">配置 AJAX 分析服务后，将立即在页面中提供;但是，在使用之前，必须加载一次。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="3f5d2-263">*ProfileService 成员*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="3f5d2-264">*属性字段：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-264">*properties field:*</span></span>

<span data-ttu-id="3f5d2-265">"属性" 字段将所有配置的配置文件数据公开为可通过点操作员名称约定引用的子属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="3f5d2-266">作为属性组的子级的属性称为 "组名称"。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="3f5d2-267">在上面介绍的示例配置文件配置中，若要获取用户的状态，可以使用以下标识符：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="3f5d2-268">*load 方法：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-268">*load method:*</span></span>

<span data-ttu-id="3f5d2-269">从服务器加载选定列表或所有属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="3f5d2-270">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-270">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-271">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-271">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-272">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-273">propertyNames</span><span class="sxs-lookup"><span data-stu-id="3f5d2-273">propertyNames</span></span> | <span data-ttu-id="3f5d2-274">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-274">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-275">要从服务器加载的属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="3f5d2-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-276">loadCompletedCallback</span></span> | <span data-ttu-id="3f5d2-277">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-277">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-278">加载完成时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="3f5d2-279">failedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-279">failedCallback</span></span> | <span data-ttu-id="3f5d2-280">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-280">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-281">发生错误时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="3f5d2-282">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-282">userContext</span></span> | <span data-ttu-id="3f5d2-283">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-283">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-284">要传递给回调函数的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="3f5d2-285">Load 函数没有返回值。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-285">The load function does not have a return value.</span></span> <span data-ttu-id="3f5d2-286">如果调用成功完成，它将调用 `loadCompletedCallback` 参数或 `defaultLoadCompletedCallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="3f5d2-287">如果调用失败或超时过期，则将调用 `failedCallback` 参数或 `defaultFailedCallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="3f5d2-288">如果未提供 `propertyNames` 参数，则将从服务器中检索所有读取配置的属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="3f5d2-289">*保存方法：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-289">*save method:*</span></span>

<span data-ttu-id="3f5d2-290">Save （）方法会将指定的属性列表（或所有属性）保存到用户的 ASP.NET 配置文件。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="3f5d2-291">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-291">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-292">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-292">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-293">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-294">propertyNames</span><span class="sxs-lookup"><span data-stu-id="3f5d2-294">propertyNames</span></span> | <span data-ttu-id="3f5d2-295">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-295">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-296">要保存到服务器的属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="3f5d2-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-297">saveCompletedCallback</span></span> | <span data-ttu-id="3f5d2-298">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-298">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-299">保存完成后要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="3f5d2-300">failedCallback</span><span class="sxs-lookup"><span data-stu-id="3f5d2-300">failedCallback</span></span> | <span data-ttu-id="3f5d2-301">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-301">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-302">发生错误时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="3f5d2-303">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-303">userContext</span></span> | <span data-ttu-id="3f5d2-304">可选（默认为 null）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-304">Optional (defaults to null).</span></span> <span data-ttu-id="3f5d2-305">要传递给回调函数的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="3f5d2-306">Save 函数没有返回值。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-306">The save function does not have a return value.</span></span> <span data-ttu-id="3f5d2-307">如果调用成功完成，它将调用 `saveCompletedCallback` 参数或 `defaultSaveCompletedCallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="3f5d2-308">如果调用失败或超时过期，则将调用 `failedCallback` 或 `defaultFailedCallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="3f5d2-309">如果 `propertyNames` 参数为 null，则所有配置文件属性将发送到服务器，并且服务器将决定可以保存哪些属性以及哪些属性无法保存。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="3f5d2-310">*defaultFailedCallback 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="3f5d2-311">此属性指定在无法与 web 服务进行通信的情况下应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="3f5d2-312">它应收到委托（或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="3f5d2-313">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="3f5d2-314">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-314">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-315">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-315">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-316">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-317">Error</span><span class="sxs-lookup"><span data-stu-id="3f5d2-317">Error</span></span> | <span data-ttu-id="3f5d2-318">指定错误信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-318">Specifies the error information.</span></span> |
| <span data-ttu-id="3f5d2-319">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-319">userContext</span></span> | <span data-ttu-id="3f5d2-320">指定在调用 load 或 save 函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="3f5d2-321">methodName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-321">methodName</span></span> | <span data-ttu-id="3f5d2-322">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-322">The name of the calling method.</span></span> |

<span data-ttu-id="3f5d2-323">*defaultSaveCompleted 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="3f5d2-324">此属性指定在完成保存用户的配置文件数据时应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="3f5d2-325">它应收到委托（或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="3f5d2-326">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="3f5d2-327">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-327">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-328">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-328">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-329">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="3f5d2-330">numPropsSaved</span></span> | <span data-ttu-id="3f5d2-331">指定已保存的属性数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="3f5d2-332">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-332">userContext</span></span> | <span data-ttu-id="3f5d2-333">指定在调用 load 或 save 函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="3f5d2-334">methodName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-334">methodName</span></span> | <span data-ttu-id="3f5d2-335">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-335">The name of the calling method.</span></span> |

<span data-ttu-id="3f5d2-336">*defaultLoadCompleted 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="3f5d2-337">此属性指定应在完成加载用户的配置文件数据时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="3f5d2-338">它应收到委托（或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="3f5d2-339">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="3f5d2-340">*参数：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-340">*Parameters:*</span></span>

| <span data-ttu-id="3f5d2-341">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-341">**Parameter Name**</span></span> | <span data-ttu-id="3f5d2-342">**含义**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3f5d2-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="3f5d2-343">numPropsLoaded</span></span> | <span data-ttu-id="3f5d2-344">指定加载的属性数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="3f5d2-345">userContext</span><span class="sxs-lookup"><span data-stu-id="3f5d2-345">userContext</span></span> | <span data-ttu-id="3f5d2-346">指定在调用 load 或 save 函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="3f5d2-347">methodName</span><span class="sxs-lookup"><span data-stu-id="3f5d2-347">methodName</span></span> | <span data-ttu-id="3f5d2-348">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-348">The name of the calling method.</span></span> |

<span data-ttu-id="3f5d2-349">*path 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-349">*path property (get, set):*</span></span>

<span data-ttu-id="3f5d2-350">此属性以编程方式确定配置文件 web 服务的位置。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="3f5d2-351">它可用于重写默认配置文件服务提供程序，以及在 ScriptManager 控件的 ProfileService 子节点的路径属性中以声明方式设置的一个集。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="3f5d2-352">请注意，默认配置文件服务的位置不会更改。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="3f5d2-353">但是，ASP.NET AJAX 允许你指定 web 服务的位置，该服务提供与 ASP.NET AJAX authentication service proxy 相同的类接口。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="3f5d2-354">另请注意，不应将此属性设置为将脚本请求定向到当前站点之外的值。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="3f5d2-355">基础 AJAX 不应发布跨站点请求，并可能会在客户端浏览器中产生安全异常。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="3f5d2-356">此属性是一个 `String` 对象，表示配置文件 web 服务的路径。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="3f5d2-357">*timeout 属性（get、set）：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="3f5d2-358">此属性确定等待 load 或 save 请求失败之前等待配置文件服务的时间长度。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="3f5d2-359">如果在等待调用完成时超时时间已到，则会调用请求失败回调，并且调用将无法完成。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="3f5d2-360">此属性是一个 `Number` 对象，该对象表示要等待来自配置文件服务的结果的毫秒数。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="3f5d2-361">*代码示例：加载页面加载时的配置文件数据*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="3f5d2-362">以下代码将检查是否对用户进行了身份验证，如果是，则将用户的首选背景色作为页面加载。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="3f5d2-363">*使用自定义身份验证服务提供程序*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="3f5d2-364">ASP.NET AJAX Extension 允许您通过自定义 web 服务公开您的功能，来创建自定义脚本身份验证服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="3f5d2-365">若要使用，web 服务必须公开两种方法，`Login` 和 `Logout`;并且必须指定与默认 ASP.NET AJAX Authentication web 服务的方法签名相同的方法签名。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="3f5d2-366">创建自定义 web 服务后，你将需要在页面上以编程方式以编程方式在代码中或通过客户端脚本来指定该服务的路径。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="3f5d2-367">*若要以声明方式设置路径：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="3f5d2-368">若要以声明方式设置路径，请在 ASP.NET 页面上包含 ScriptManager 对象的 AuthenticationService 子级：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="3f5d2-369">*若要在代码中设置路径：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-369">*To set the path in code:*</span></span>

<span data-ttu-id="3f5d2-370">若要以编程方式设置路径，请通过脚本管理器的实例指定路径：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="3f5d2-371">*若要在脚本中设置路径：*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-371">*To set the path in script:*</span></span>

<span data-ttu-id="3f5d2-372">若要在脚本中以编程方式设置路径，请使用 AuthenticationService 类的 `path` 属性：</span><span class="sxs-lookup"><span data-stu-id="3f5d2-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="3f5d2-373">*用于自定义身份验证的示例 Web 服务*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="3f5d2-374">摘要</span><span class="sxs-lookup"><span data-stu-id="3f5d2-374">Summary</span></span>

<span data-ttu-id="3f5d2-375">ASP.NET 服务-特别是分析、成员身份和身份验证服务-可在客户端浏览器上轻松地向 JavaScript 公开。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="3f5d2-376">这使开发人员能够无缝地将其客户端代码与身份验证机制集成，而无需依赖 UpdatePanels 等控件来执行繁重的工作。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="3f5d2-377">还可以通过使用 web 配置设置来保护来自客户端的配置文件数据;默认情况下不提供数据，开发人员必须选择配置文件属性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="3f5d2-378">此外，通过使用等效的方法签名创建简化的 web 服务实现，开发人员可以为这些内部的 ASP.NET 服务创建自定义脚本提供程序。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="3f5d2-379">对这些技术的支持简化了丰富客户端应用程序的开发，同时为开发人员提供了可满足特定需求的各种灵活性。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="3f5d2-380">*Bio*</span><span class="sxs-lookup"><span data-stu-id="3f5d2-380">*Bio*</span></span>

<span data-ttu-id="3f5d2-381">Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f5d2-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="3f5d2-382">可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客</span><span class="sxs-lookup"><span data-stu-id="3f5d2-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3f5d2-383">[上一页](understanding-asp-net-ajax-updatepanel-triggers.md)
> [下一页](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
