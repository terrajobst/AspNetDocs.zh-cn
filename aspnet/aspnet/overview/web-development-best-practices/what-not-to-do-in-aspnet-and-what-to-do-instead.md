---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: 不在 ASP.NET 中执行的操作，而应执行的操作 |Microsoft Docs
author: Rick-Anderson
description: 本主题介绍用户在 ASP.NET web 项目中所做的几个常见错误。 它为避免这些 commo 而应采取的措施提供建议 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500132"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="0aa76-104">不得在 ASP.NET 中执行的操作和转而应执行的操作</span><span class="sxs-lookup"><span data-stu-id="0aa76-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="0aa76-105">本主题介绍用户在 ASP.NET web 项目中所做的几个常见错误。</span><span class="sxs-lookup"><span data-stu-id="0aa76-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="0aa76-106">它为避免这些常见错误应执行的操作提供了建议。</span><span class="sxs-lookup"><span data-stu-id="0aa76-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="0aa76-107">它基于在挪威开发人员大会上**Damian Edwards**的[演示](http://vimeo.com/68390507)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="0aa76-108">免责声明</span><span class="sxs-lookup"><span data-stu-id="0aa76-108">Disclaimer</span></span>

<span data-ttu-id="0aa76-109">本主题不旨在作为确保你的应用程序安全和高效的完整指南。</span><span class="sxs-lookup"><span data-stu-id="0aa76-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="0aa76-110">仍需遵循本主题未介绍的安全性和性能的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="0aa76-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="0aa76-111">它仅建议如何避免与 .NET 类和进程相关的常见错误。</span><span class="sxs-lookup"><span data-stu-id="0aa76-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="0aa76-112">概述</span><span class="sxs-lookup"><span data-stu-id="0aa76-112">Overview</span></span>

<span data-ttu-id="0aa76-113">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="0aa76-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="0aa76-114">标准符合性</span><span class="sxs-lookup"><span data-stu-id="0aa76-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="0aa76-115">控件适配器</span><span class="sxs-lookup"><span data-stu-id="0aa76-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="0aa76-116">控件的样式属性</span><span class="sxs-lookup"><span data-stu-id="0aa76-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="0aa76-117">页和控件回调</span><span class="sxs-lookup"><span data-stu-id="0aa76-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="0aa76-118">浏览器功能检测</span><span class="sxs-lookup"><span data-stu-id="0aa76-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="0aa76-119">安全性</span><span class="sxs-lookup"><span data-stu-id="0aa76-119">Security</span></span>](#security)

    - [<span data-ttu-id="0aa76-120">请求验证</span><span class="sxs-lookup"><span data-stu-id="0aa76-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="0aa76-121">无 cookie Forms 身份验证和会话</span><span class="sxs-lookup"><span data-stu-id="0aa76-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="0aa76-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="0aa76-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="0aa76-123">中等信任</span><span class="sxs-lookup"><span data-stu-id="0aa76-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="0aa76-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="0aa76-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="0aa76-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="0aa76-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="0aa76-126">可靠性和性能</span><span class="sxs-lookup"><span data-stu-id="0aa76-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="0aa76-127">PreSendRequestHeaders 和 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="0aa76-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="0aa76-128">带有 Web 窗体的异步页面事件</span><span class="sxs-lookup"><span data-stu-id="0aa76-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="0aa76-129">火灾和遗忘工作</span><span class="sxs-lookup"><span data-stu-id="0aa76-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="0aa76-130">请求实体正文</span><span class="sxs-lookup"><span data-stu-id="0aa76-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="0aa76-131">响应。重定向和响应。结束</span><span class="sxs-lookup"><span data-stu-id="0aa76-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="0aa76-132">EnableViewState 和 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="0aa76-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="0aa76-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="0aa76-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="0aa76-134">长时间运行的请求（> 110 秒）</span><span class="sxs-lookup"><span data-stu-id="0aa76-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="0aa76-135">标准符合性</span><span class="sxs-lookup"><span data-stu-id="0aa76-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="0aa76-136">控件适配器</span><span class="sxs-lookup"><span data-stu-id="0aa76-136">Control adapters</span></span>

<span data-ttu-id="0aa76-137">建议：停止使用控件适配器进行自适应呈现，而改用 CSS 媒体查询和符合标准的 HTML。</span><span class="sxs-lookup"><span data-stu-id="0aa76-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="0aa76-138">.NET 2.0 中引入了控件适配器，用于呈现针对不同设备和环境自定义的表示代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="0aa76-139">现在，可以通过 CSS 和 HTML 实现此自适应呈现。</span><span class="sxs-lookup"><span data-stu-id="0aa76-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="0aa76-140">应该停止使用控件适配器并将任何现有的适配器转换为 CSS 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="0aa76-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="0aa76-141">有关详细信息，请参阅[媒体查询](http://www.w3.org/TR/css3-mediaqueries/)和[如何：将移动页添加到 ASP.NET Web 窗体/MVC 应用程序](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="0aa76-142">控件的样式属性</span><span class="sxs-lookup"><span data-stu-id="0aa76-142">Style properties on controls</span></span>

<span data-ttu-id="0aa76-143">建议：停止在控件标记中设置样式值，并改为在 CSS 样式表中设置格式设置值。</span><span class="sxs-lookup"><span data-stu-id="0aa76-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="0aa76-144">Web 服务器控件包含数十个属性，这些属性可用于设置内嵌样式属性。</span><span class="sxs-lookup"><span data-stu-id="0aa76-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="0aa76-145">例如，"前景色" 属性设置控件文本的颜色。</span><span class="sxs-lookup"><span data-stu-id="0aa76-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="0aa76-146">您可以通过 CSS 样式表更高效地完成此相同的效果。</span><span class="sxs-lookup"><span data-stu-id="0aa76-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="0aa76-147">使用样式表可以集中样式值，并避免在整个应用程序中设置这些值。</span><span class="sxs-lookup"><span data-stu-id="0aa76-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="0aa76-148">下面的示例演示了一个 CSS 类，它将文本设置为红色。</span><span class="sxs-lookup"><span data-stu-id="0aa76-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="0aa76-149">下一个示例演示如何动态应用 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="0aa76-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="0aa76-150">页和控件回调</span><span class="sxs-lookup"><span data-stu-id="0aa76-150">Page and control callbacks</span></span>

<span data-ttu-id="0aa76-151">建议：停止使用页面和控件回调，而使用以下任何方法： AJAX、UpdatePanel、MVC 操作方法、Web API 或 SignalR。</span><span class="sxs-lookup"><span data-stu-id="0aa76-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="0aa76-152">在早期版本的 ASP.NET 中，使用页和控件回调方法，您可以更新部分网页，而不会刷新整个页面。</span><span class="sxs-lookup"><span data-stu-id="0aa76-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="0aa76-153">现在可以通过[AJAX](../../../ajax/index.md)、 [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)、 [MVC](../../../mvc/index.md)、 [Web API](../../../web-api/index.md)或[SignalR](../../../signalr/index.md)完成部分页面更新。</span><span class="sxs-lookup"><span data-stu-id="0aa76-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="0aa76-154">你应停止使用回叫方法，因为它们可能会导致友好 Url 和路由出现问题。</span><span class="sxs-lookup"><span data-stu-id="0aa76-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="0aa76-155">默认情况下，控件不会启用回调方法，但如果在控件中启用了此功能，则应禁用此功能。</span><span class="sxs-lookup"><span data-stu-id="0aa76-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="0aa76-156">浏览器功能检测</span><span class="sxs-lookup"><span data-stu-id="0aa76-156">Browser capability detection</span></span>

<span data-ttu-id="0aa76-157">建议：停止使用静态浏览器功能检测，并改为使用动态功能检测。</span><span class="sxs-lookup"><span data-stu-id="0aa76-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="0aa76-158">在早期版本的 ASP.NET 中，每个浏览器支持的功能存储在一个 XML 文件中。</span><span class="sxs-lookup"><span data-stu-id="0aa76-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="0aa76-159">通过静态查找检测功能支持不是最佳方法。</span><span class="sxs-lookup"><span data-stu-id="0aa76-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="0aa76-160">现在，可以使用功能检测框架（如[Modernizr](http://modernizr.com/)）动态检测浏览器的支持功能。</span><span class="sxs-lookup"><span data-stu-id="0aa76-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="0aa76-161">功能检测通过尝试使用方法或属性，然后检查浏览器是否生成了所需的结果，来确定支持。</span><span class="sxs-lookup"><span data-stu-id="0aa76-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="0aa76-162">默认情况下，Modernizr 包含在 Web 应用程序模板中。</span><span class="sxs-lookup"><span data-stu-id="0aa76-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="0aa76-163">安全</span><span class="sxs-lookup"><span data-stu-id="0aa76-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="0aa76-164">请求验证</span><span class="sxs-lookup"><span data-stu-id="0aa76-164">Request validation</span></span>

<span data-ttu-id="0aa76-165">建议：验证用户输入，并编码用户的输出。</span><span class="sxs-lookup"><span data-stu-id="0aa76-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="0aa76-166">请求验证是 ASP.NET 的一项功能，它检查每个请求并在发现发现的威胁时停止请求。</span><span class="sxs-lookup"><span data-stu-id="0aa76-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="0aa76-167">不要依赖请求验证来保护应用程序免受跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="0aa76-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="0aa76-168">改为验证所有用户输入并对输出进行编码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="0aa76-169">在某些有限情况下，你可以使用正则表达式来验证输入，但在更复杂的情况下，你应该使用 .NET 类来验证用户输入是否与允许的值匹配。</span><span class="sxs-lookup"><span data-stu-id="0aa76-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="0aa76-170">下面的示例演示如何使用 Uri 类中的静态方法来确定用户提供的 Uri 是否有效。</span><span class="sxs-lookup"><span data-stu-id="0aa76-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="0aa76-171">但是，若要充分验证 Uri，还应检查以确保它指定 `http` 或 `https`。</span><span class="sxs-lookup"><span data-stu-id="0aa76-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="0aa76-172">下面的示例使用实例方法来验证 Uri 是否有效。</span><span class="sxs-lookup"><span data-stu-id="0aa76-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="0aa76-173">在以 HTML 格式呈现用户输入或在 SQL 查询中包含用户输入之前，对值进行编码以确保不包括恶意代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="0aa76-174">您可以在标记中对值进行 HTML 编码，&lt;%：%&gt; 语法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0aa76-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="0aa76-175">或者，在 Razor 语法中，可以用 @ 进行 HTML 编码，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0aa76-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="0aa76-176">下一个示例演示如何在代码隐藏中对值进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="0aa76-177">若要为 SQL 命令安全地编码值，请使用命令参数，如[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="0aa76-178">无 cookie forms 身份验证和会话</span><span class="sxs-lookup"><span data-stu-id="0aa76-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="0aa76-179">建议：需要 cookie。</span><span class="sxs-lookup"><span data-stu-id="0aa76-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="0aa76-180">在查询字符串中传递身份验证信息并不安全。</span><span class="sxs-lookup"><span data-stu-id="0aa76-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="0aa76-181">因此，当应用程序包括身份验证时，需要 cookie。</span><span class="sxs-lookup"><span data-stu-id="0aa76-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="0aa76-182">如果 cookie 存储了敏感信息，请考虑要求 SSL 提供 cookie。</span><span class="sxs-lookup"><span data-stu-id="0aa76-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="0aa76-183">下面的示例演示如何在 web.config 文件中指定 Forms 身份验证要求通过 SSL 传输的 cookie。</span><span class="sxs-lookup"><span data-stu-id="0aa76-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="0aa76-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="0aa76-184">EnableViewStateMac</span></span>

<span data-ttu-id="0aa76-185">建议：绝不设置为 false。</span><span class="sxs-lookup"><span data-stu-id="0aa76-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="0aa76-186">默认情况下，EnableViewStateMac 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="0aa76-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="0aa76-187">即使您的应用程序未使用视图状态，也不要将 EnableViewStateMac 设置为 false。</span><span class="sxs-lookup"><span data-stu-id="0aa76-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="0aa76-188">将此值设置为 false 将使您的应用程序容易受到跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="0aa76-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="0aa76-189">从 ASP.NET 4.5.2 开始，运行时强制执行**EnableViewStateMac = true**。</span><span class="sxs-lookup"><span data-stu-id="0aa76-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="0aa76-190">即使将其设置为 false，运行时也会忽略此值，并继续将值设置为 true。</span><span class="sxs-lookup"><span data-stu-id="0aa76-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="0aa76-191">有关详细信息，请参阅[ASP.NET 4.5.2 And EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="0aa76-192">下面的示例演示如何将 EnableViewStateMac 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="0aa76-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="0aa76-193">不需要实际将此值设置为 true，因为它在默认情况下为 true。</span><span class="sxs-lookup"><span data-stu-id="0aa76-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="0aa76-194">但是，如果您在应用程序的任何页上将其设置为 false，则必须立即更正此值。</span><span class="sxs-lookup"><span data-stu-id="0aa76-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="0aa76-195">中等信任</span><span class="sxs-lookup"><span data-stu-id="0aa76-195">Medium trust</span></span>

<span data-ttu-id="0aa76-196">建议：不要依赖于中等信任（或任何其他信任级别）作为安全边界。</span><span class="sxs-lookup"><span data-stu-id="0aa76-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="0aa76-197">部分信任不能充分保护你的应用程序，因此不应使用。</span><span class="sxs-lookup"><span data-stu-id="0aa76-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="0aa76-198">而应使用完全信任，并将不受信任的应用程序隔离在单独的应用程序池中。</span><span class="sxs-lookup"><span data-stu-id="0aa76-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="0aa76-199">另外，在唯一标识下运行每个应用程序池。</span><span class="sxs-lookup"><span data-stu-id="0aa76-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="0aa76-200">有关详细信息，请参阅[ASP.NET 部分信任不保证应用程序隔离](https://support.microsoft.com/kb/2698981)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="0aa76-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="0aa76-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="0aa76-202">建议：不要禁用 &lt;appSettings&gt; 元素中的安全设置。</span><span class="sxs-lookup"><span data-stu-id="0aa76-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="0aa76-203">AppSettings 元素包含多个安全更新所需的值。</span><span class="sxs-lookup"><span data-stu-id="0aa76-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="0aa76-204">不应更改或禁用这些值。</span><span class="sxs-lookup"><span data-stu-id="0aa76-204">You should not change or disable these values.</span></span> <span data-ttu-id="0aa76-205">如果必须在部署更新时禁用这些值，请在完成部署后立即重新启用。</span><span class="sxs-lookup"><span data-stu-id="0aa76-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="0aa76-206">有关详细信息，请参阅[ASP.NET AppSettings 元素](https://msdn.microsoft.com/library/hh975440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="0aa76-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="0aa76-207">UrlPathEncode</span></span>

<span data-ttu-id="0aa76-208">建议：改为使用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="0aa76-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="0aa76-209">UrlPathEncode 方法已添加到 .NET Framework 以解决非常特定的浏览器兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="0aa76-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="0aa76-210">它不能充分地对 URL 进行编码，也不能保护应用程序免受跨站点脚本的的作用。</span><span class="sxs-lookup"><span data-stu-id="0aa76-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="0aa76-211">不应在应用程序中使用它。</span><span class="sxs-lookup"><span data-stu-id="0aa76-211">You should never use it in your application.</span></span> <span data-ttu-id="0aa76-212">相反，请使用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="0aa76-213">下面的示例演示如何将编码的 URL 作为超链接控件的查询字符串参数进行传递。</span><span class="sxs-lookup"><span data-stu-id="0aa76-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="0aa76-214">可靠性和性能</span><span class="sxs-lookup"><span data-stu-id="0aa76-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="0aa76-215">PreSendRequestHeaders 和 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="0aa76-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="0aa76-216">建议：不要将这些事件用于托管模块。</span><span class="sxs-lookup"><span data-stu-id="0aa76-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="0aa76-217">相反，编写一个本机 IIS 模块来执行所需的任务。</span><span class="sxs-lookup"><span data-stu-id="0aa76-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="0aa76-218">请参阅[创建本机代码 HTTP 模块](https://msdn.microsoft.com/library/ms693629.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="0aa76-219">可以将[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)和[PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)事件用于本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="0aa76-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="0aa76-220">不要将 `PreSendRequestHeaders` 和 `PreSendRequestContent` 与实现 `IHttpModule`的托管模块一起使用。</span><span class="sxs-lookup"><span data-stu-id="0aa76-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="0aa76-221">设置这些属性可能会导致异步请求出现问题。</span><span class="sxs-lookup"><span data-stu-id="0aa76-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="0aa76-222">应用程序请求路由（ARR）和 websocket 的组合可能会导致访问冲突异常，这可能会导致 w3wp.exe 崩溃。</span><span class="sxs-lookup"><span data-stu-id="0aa76-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="0aa76-223">例如，iiscore！W3_CONTEXT_BASE：： iiscore 中的 GetIsLastNotification + 68 导致了访问冲突异常（0xC0000005）。</span><span class="sxs-lookup"><span data-stu-id="0aa76-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="0aa76-224">带有 web 窗体的异步页面事件</span><span class="sxs-lookup"><span data-stu-id="0aa76-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="0aa76-225">建议：在 Web 窗体中，避免写入页面生命周期事件的异步 void 方法，而是将[onendselect](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)用于异步代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="0aa76-226">当使用**async**和**void**标记页面事件时，无法确定异步代码的完成时间。</span><span class="sxs-lookup"><span data-stu-id="0aa76-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="0aa76-227">相反，请使用 Onendselect，以使您能够跟踪其完成的方式运行异步代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="0aa76-228">下面的示例演示一个包含异步代码的按钮单击处理程序。</span><span class="sxs-lookup"><span data-stu-id="0aa76-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="0aa76-229">此示例包括异步读取字符串值，该字符串值仅作为异步任务的简化示例提供，而不是作为建议的做法。</span><span class="sxs-lookup"><span data-stu-id="0aa76-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="0aa76-230">如果使用的是异步任务，请在 web.config 文件中将 Http 运行时目标框架设置为4.5 （或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="0aa76-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="0aa76-231">如果将目标框架设置为4.5，则将打开在 .NET 4.5 中添加的新的同步上下文。</span><span class="sxs-lookup"><span data-stu-id="0aa76-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="0aa76-232">默认情况下，此值是在 Visual Studio 的新项目中设置的，但如果使用的是现有项目，则不设置此值。</span><span class="sxs-lookup"><span data-stu-id="0aa76-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="0aa76-233">火灾和遗忘工作</span><span class="sxs-lookup"><span data-stu-id="0aa76-233">Fire-and-forget work</span></span>

<span data-ttu-id="0aa76-234">建议：在 ASP.NET 中处理请求时，请避免启动暂时的工作（例如，调用 QueueUserWorkItem 方法或创建重复调用委托的计时器）。</span><span class="sxs-lookup"><span data-stu-id="0aa76-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="0aa76-235">如果你的应用程序在 ASP.NET 中运行，则你的应用程序可能会失去同步。随时可以销毁应用域，这意味着正在进行的进程可能不再与应用程序的当前状态匹配。</span><span class="sxs-lookup"><span data-stu-id="0aa76-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="0aa76-236">应将此类工作移出 ASP.NET 外部。</span><span class="sxs-lookup"><span data-stu-id="0aa76-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="0aa76-237">你可以使用 Web 作业、Windows 服务或 Azure 中的辅助角色来执行正在进行的工作，并从其他进程运行该代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="0aa76-238">如果必须在 ASP.NET 中执行此操作，则可以添加名为[WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)的 Nuget 包来运行代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="0aa76-239">请求实体正文</span><span class="sxs-lookup"><span data-stu-id="0aa76-239">Request entity body</span></span>

<span data-ttu-id="0aa76-240">建议：在处理程序的执行事件之前，避免读取 InputStream 或请求。</span><span class="sxs-lookup"><span data-stu-id="0aa76-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="0aa76-241">应从请求中读取的最早形式。 InputStream 在处理程序的执行事件期间。</span><span class="sxs-lookup"><span data-stu-id="0aa76-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="0aa76-242">在 MVC 中，控制器是处理程序，在操作方法运行时执行事件。</span><span class="sxs-lookup"><span data-stu-id="0aa76-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="0aa76-243">在 Web 窗体中，页是处理程序，执行事件是在初始化页 Init 事件时。</span><span class="sxs-lookup"><span data-stu-id="0aa76-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="0aa76-244">如果读取的请求实体正文早于 execute 事件，则会干扰请求的处理。</span><span class="sxs-lookup"><span data-stu-id="0aa76-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="0aa76-245">如果需要在执行事件之前读取请求实体正文，请使用[GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)或[GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="0aa76-246">当你使用 GetBufferlessInputStream 时，将从请求获取原始流，并承担处理整个请求的责任。</span><span class="sxs-lookup"><span data-stu-id="0aa76-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="0aa76-247">在调用 GetBufferlessInputStream、InputStream 和 ASP.NET 后，不能使用，因为它们未由填充。</span><span class="sxs-lookup"><span data-stu-id="0aa76-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="0aa76-248">当你使用 GetBufferedInputStream 时，将从请求获取流的副本。</span><span class="sxs-lookup"><span data-stu-id="0aa76-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="0aa76-249">InputStream 在以后的请求中仍可用，因为 ASP.NET 将填充其他副本。</span><span class="sxs-lookup"><span data-stu-id="0aa76-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="0aa76-250">响应。重定向和响应。结束</span><span class="sxs-lookup"><span data-stu-id="0aa76-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="0aa76-251">建议：注意调用响应后如何处理线程[。重定向（String）](https://msdn.microsoft.com/library/t9dwyts4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="0aa76-252">[Response （String）](https://msdn.microsoft.com/library/t9dwyts4.aspx)方法调用 response 方法。</span><span class="sxs-lookup"><span data-stu-id="0aa76-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="0aa76-253">在同步过程中，调用请求。重定向会导致当前线程立即中止。</span><span class="sxs-lookup"><span data-stu-id="0aa76-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="0aa76-254">但是，在异步过程中，调用响应。重定向不会中止当前线程，因此请求会继续执行代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="0aa76-255">在异步过程中，您必须从方法返回任务以停止执行代码。</span><span class="sxs-lookup"><span data-stu-id="0aa76-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="0aa76-256">在 MVC 项目中，不应调用 Response。重定向。</span><span class="sxs-lookup"><span data-stu-id="0aa76-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="0aa76-257">而是返回 RedirectResult。</span><span class="sxs-lookup"><span data-stu-id="0aa76-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="0aa76-258">EnableViewState 和 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="0aa76-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="0aa76-259">建议：使用 ViewStateMode 而不是 EnableViewState 来提供对使用视图状态的控件的精细控制。</span><span class="sxs-lookup"><span data-stu-id="0aa76-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="0aa76-260">在 Page 指令中将 EnableViewState 设置为 false 时，将为该页中的所有控件禁用视图状态，并且无法启用。</span><span class="sxs-lookup"><span data-stu-id="0aa76-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="0aa76-261">如果要仅对页面中的某些控件启用视图状态，请将页面的 "ViewStateMode" 设置为 "已禁用"。</span><span class="sxs-lookup"><span data-stu-id="0aa76-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="0aa76-262">然后，将 ViewStateMode 设置为仅在实际需要视图状态的控件上启用。</span><span class="sxs-lookup"><span data-stu-id="0aa76-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="0aa76-263">通过只为需要它的控件启用视图状态，可以缩小网页的视图状态大小。</span><span class="sxs-lookup"><span data-stu-id="0aa76-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="0aa76-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="0aa76-264">SqlMembershipProvider</span></span>

<span data-ttu-id="0aa76-265">建议：使用通用提供程序。</span><span class="sxs-lookup"><span data-stu-id="0aa76-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="0aa76-266">在当前项目模板中，SqlMembershipProvider 已由[ASP.NET 通用提供程序](http://www.nuget.org/packages/Microsoft.AspNet.Providers)替换，可作为 NuGet 包提供。</span><span class="sxs-lookup"><span data-stu-id="0aa76-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="0aa76-267">如果在使用早期版本的模板生成的项目中使用 SqlMembershipProvider，则应切换到通用提供程序。</span><span class="sxs-lookup"><span data-stu-id="0aa76-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="0aa76-268">通用提供程序适用于实体框架支持的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="0aa76-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="0aa76-269">有关详细信息，请参阅[简介 ASP.NET 通用提供程序](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0aa76-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="0aa76-270">长时间运行的请求（> 110 秒）</span><span class="sxs-lookup"><span data-stu-id="0aa76-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="0aa76-271">建议：为已连接的客户端使用[websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)或[SignalR](../../../signalr/index.md) ，并使用异步 i/o 操作。</span><span class="sxs-lookup"><span data-stu-id="0aa76-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="0aa76-272">长时间运行的请求可能会导致不可预知的结果，并降低 web 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="0aa76-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="0aa76-273">请求的默认超时设置为110秒。</span><span class="sxs-lookup"><span data-stu-id="0aa76-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="0aa76-274">如果要将会话状态与长时间运行的请求一起使用，则 ASP.NET 将在110秒后释放会话对象的锁。</span><span class="sxs-lookup"><span data-stu-id="0aa76-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="0aa76-275">但是，当锁被释放时，您的应用程序可能正在对 Session 对象执行操作，并且该操作可能无法成功完成。</span><span class="sxs-lookup"><span data-stu-id="0aa76-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="0aa76-276">如果第一个请求在运行时阻止了来自用户的第二个请求，则第二个请求可能会以不一致的状态访问会话对象。</span><span class="sxs-lookup"><span data-stu-id="0aa76-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="0aa76-277">如果你的应用程序包括阻止（或同步） i/o 操作，则应用程序将无响应。</span><span class="sxs-lookup"><span data-stu-id="0aa76-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="0aa76-278">若要提高性能，请在 .NET Framework 中使用异步 i/o 操作。</span><span class="sxs-lookup"><span data-stu-id="0aa76-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="0aa76-279">此外，请使用 Websocket 或 SignalR 将客户端连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="0aa76-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="0aa76-280">这些功能旨在有效地处理长时间运行的请求。</span><span class="sxs-lookup"><span data-stu-id="0aa76-280">These features are designed to efficiently handle long-running requests.</span></span>
