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
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>不得在 ASP.NET 中执行的操作和转而应执行的操作

> 本主题介绍用户在 ASP.NET web 项目中所做的几个常见错误。 它为避免这些常见错误应执行的操作提供了建议。 它基于在挪威开发人员大会上**Damian Edwards**的[演示](http://vimeo.com/68390507)。

## <a name="disclaimer"></a>免责声明

本主题不旨在作为确保你的应用程序安全和高效的完整指南。 仍需遵循本主题未介绍的安全性和性能的最佳做法。 它仅建议如何避免与 .NET 类和进程相关的常见错误。

## <a name="overview"></a>概述

本主题包含以下各节：

- [标准符合性](#standards)

    - [控件适配器](#adapters)
    - [控件的样式属性](#styleprop)
    - [页和控件回调](#callback)
    - [浏览器功能检测](#browsercap)
- [安全性](#security)

    - [请求验证](#validation)
    - [无 cookie Forms 身份验证和会话](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [中等信任](#medium)
    - [&lt;appSettings&gt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [可靠性和性能](#performance)

    - [PreSendRequestHeaders 和 PreSendRequestContent](#presend)
    - [带有 Web 窗体的异步页面事件](#asyncevents)
    - [火灾和遗忘工作](#fire)
    - [请求实体正文](#requestentity)
    - [响应。重定向和响应。结束](#redirect)
    - [EnableViewState 和 ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [长时间运行的请求（> 110 秒）](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>标准符合性

<a id="adapters"></a>

### <a name="control-adapters"></a>控件适配器

建议：停止使用控件适配器进行自适应呈现，而改用 CSS 媒体查询和符合标准的 HTML。

.NET 2.0 中引入了控件适配器，用于呈现针对不同设备和环境自定义的表示代码。 现在，可以通过 CSS 和 HTML 实现此自适应呈现。 应该停止使用控件适配器并将任何现有的适配器转换为 CSS 和 HTML。

有关详细信息，请参阅[媒体查询](http://www.w3.org/TR/css3-mediaqueries/)和[如何：将移动页添加到 ASP.NET Web 窗体/MVC 应用程序](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)。

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>控件的样式属性

建议：停止在控件标记中设置样式值，并改为在 CSS 样式表中设置格式设置值。

Web 服务器控件包含数十个属性，这些属性可用于设置内嵌样式属性。 例如，"前景色" 属性设置控件文本的颜色。 您可以通过 CSS 样式表更高效地完成此相同的效果。 使用样式表可以集中样式值，并避免在整个应用程序中设置这些值。

下面的示例演示了一个 CSS 类，它将文本设置为红色。

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

下一个示例演示如何动态应用 CSS 类。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>页和控件回调

建议：停止使用页面和控件回调，而使用以下任何方法： AJAX、UpdatePanel、MVC 操作方法、Web API 或 SignalR。

在早期版本的 ASP.NET 中，使用页和控件回调方法，您可以更新部分网页，而不会刷新整个页面。 现在可以通过[AJAX](../../../ajax/index.md)、 [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)、 [MVC](../../../mvc/index.md)、 [Web API](../../../web-api/index.md)或[SignalR](../../../signalr/index.md)完成部分页面更新。 你应停止使用回叫方法，因为它们可能会导致友好 Url 和路由出现问题。 默认情况下，控件不会启用回调方法，但如果在控件中启用了此功能，则应禁用此功能。

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>浏览器功能检测

建议：停止使用静态浏览器功能检测，并改为使用动态功能检测。

在早期版本的 ASP.NET 中，每个浏览器支持的功能存储在一个 XML 文件中。 通过静态查找检测功能支持不是最佳方法。 现在，可以使用功能检测框架（如[Modernizr](http://modernizr.com/)）动态检测浏览器的支持功能。 功能检测通过尝试使用方法或属性，然后检查浏览器是否生成了所需的结果，来确定支持。 默认情况下，Modernizr 包含在 Web 应用程序模板中。

<a id="security"></a>

## <a name="security"></a>安全

<a id="validation"></a>

### <a name="request-validation"></a>请求验证

建议：验证用户输入，并编码用户的输出。

请求验证是 ASP.NET 的一项功能，它检查每个请求并在发现发现的威胁时停止请求。 不要依赖请求验证来保护应用程序免受跨站点脚本攻击。 改为验证所有用户输入并对输出进行编码。 在某些有限情况下，你可以使用正则表达式来验证输入，但在更复杂的情况下，你应该使用 .NET 类来验证用户输入是否与允许的值匹配。

下面的示例演示如何使用 Uri 类中的静态方法来确定用户提供的 Uri 是否有效。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

但是，若要充分验证 Uri，还应检查以确保它指定 `http` 或 `https`。 下面的示例使用实例方法来验证 Uri 是否有效。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

在以 HTML 格式呈现用户输入或在 SQL 查询中包含用户输入之前，对值进行编码以确保不包括恶意代码。

您可以在标记中对值进行 HTML 编码，&lt;%：%&gt; 语法，如下所示。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

或者，在 Razor 语法中，可以用 @ 进行 HTML 编码，如下所示。

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

下一个示例演示如何在代码隐藏中对值进行 HTML 编码。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

若要为 SQL 命令安全地编码值，请使用命令参数，如[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)。 <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>无 cookie forms 身份验证和会话

建议：需要 cookie。

在查询字符串中传递身份验证信息并不安全。 因此，当应用程序包括身份验证时，需要 cookie。 如果 cookie 存储了敏感信息，请考虑要求 SSL 提供 cookie。

下面的示例演示如何在 web.config 文件中指定 Forms 身份验证要求通过 SSL 传输的 cookie。

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

建议：绝不设置为 false。

默认情况下，EnableViewStateMac 设置为 true。 即使您的应用程序未使用视图状态，也不要将 EnableViewStateMac 设置为 false。 将此值设置为 false 将使您的应用程序容易受到跨站点脚本攻击。

从 ASP.NET 4.5.2 开始，运行时强制执行**EnableViewStateMac = true**。 即使将其设置为 false，运行时也会忽略此值，并继续将值设置为 true。 有关详细信息，请参阅[ASP.NET 4.5.2 And EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)。

下面的示例演示如何将 EnableViewStateMac 设置为 true。 不需要实际将此值设置为 true，因为它在默认情况下为 true。 但是，如果您在应用程序的任何页上将其设置为 false，则必须立即更正此值。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>中等信任

建议：不要依赖于中等信任（或任何其他信任级别）作为安全边界。

部分信任不能充分保护你的应用程序，因此不应使用。 而应使用完全信任，并将不受信任的应用程序隔离在单独的应用程序池中。 另外，在唯一标识下运行每个应用程序池。 有关详细信息，请参阅[ASP.NET 部分信任不保证应用程序隔离](https://support.microsoft.com/kb/2698981)。

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

建议：不要禁用 &lt;appSettings&gt; 元素中的安全设置。

AppSettings 元素包含多个安全更新所需的值。 不应更改或禁用这些值。 如果必须在部署更新时禁用这些值，请在完成部署后立即重新启用。

有关详细信息，请参阅[ASP.NET AppSettings 元素](https://msdn.microsoft.com/library/hh975440.aspx)。

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

建议：改为使用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 。

UrlPathEncode 方法已添加到 .NET Framework 以解决非常特定的浏览器兼容性问题。 它不能充分地对 URL 进行编码，也不能保护应用程序免受跨站点脚本的的作用。 不应在应用程序中使用它。 相反，请使用[UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)。

下面的示例演示如何将编码的 URL 作为超链接控件的查询字符串参数进行传递。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>可靠性和性能

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders 和 PreSendRequestContent

建议：不要将这些事件用于托管模块。 相反，编写一个本机 IIS 模块来执行所需的任务。 请参阅[创建本机代码 HTTP 模块](https://msdn.microsoft.com/library/ms693629.aspx)。

可以将[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)和[PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)事件用于本机 IIS 模块。
> [!WARNING]
> 不要将 `PreSendRequestHeaders` 和 `PreSendRequestContent` 与实现 `IHttpModule`的托管模块一起使用。 设置这些属性可能会导致异步请求出现问题。 应用程序请求路由（ARR）和 websocket 的组合可能会导致访问冲突异常，这可能会导致 w3wp.exe 崩溃。 例如，iiscore！W3_CONTEXT_BASE：： iiscore 中的 GetIsLastNotification + 68 导致了访问冲突异常（0xC0000005）。

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>带有 web 窗体的异步页面事件

建议：在 Web 窗体中，避免写入页面生命周期事件的异步 void 方法，而是将[onendselect](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)用于异步代码。

当使用**async**和**void**标记页面事件时，无法确定异步代码的完成时间。 相反，请使用 Onendselect，以使您能够跟踪其完成的方式运行异步代码。

下面的示例演示一个包含异步代码的按钮单击处理程序。 此示例包括异步读取字符串值，该字符串值仅作为异步任务的简化示例提供，而不是作为建议的做法。

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

如果使用的是异步任务，请在 web.config 文件中将 Http 运行时目标框架设置为4.5 （或更高版本）。 如果将目标框架设置为4.5，则将打开在 .NET 4.5 中添加的新的同步上下文。 默认情况下，此值是在 Visual Studio 的新项目中设置的，但如果使用的是现有项目，则不设置此值。

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>火灾和遗忘工作

建议：在 ASP.NET 中处理请求时，请避免启动暂时的工作（例如，调用 QueueUserWorkItem 方法或创建重复调用委托的计时器）。

如果你的应用程序在 ASP.NET 中运行，则你的应用程序可能会失去同步。随时可以销毁应用域，这意味着正在进行的进程可能不再与应用程序的当前状态匹配。

应将此类工作移出 ASP.NET 外部。 你可以使用 Web 作业、Windows 服务或 Azure 中的辅助角色来执行正在进行的工作，并从其他进程运行该代码。

如果必须在 ASP.NET 中执行此操作，则可以添加名为[WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)的 Nuget 包来运行代码。

<a id="requestentity"></a>

### <a name="request-entity-body"></a>请求实体正文

建议：在处理程序的执行事件之前，避免读取 InputStream 或请求。

应从请求中读取的最早形式。 InputStream 在处理程序的执行事件期间。 在 MVC 中，控制器是处理程序，在操作方法运行时执行事件。 在 Web 窗体中，页是处理程序，执行事件是在初始化页 Init 事件时。 如果读取的请求实体正文早于 execute 事件，则会干扰请求的处理。

如果需要在执行事件之前读取请求实体正文，请使用[GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)或[GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)。 当你使用 GetBufferlessInputStream 时，将从请求获取原始流，并承担处理整个请求的责任。 在调用 GetBufferlessInputStream、InputStream 和 ASP.NET 后，不能使用，因为它们未由填充。 当你使用 GetBufferedInputStream 时，将从请求获取流的副本。 InputStream 在以后的请求中仍可用，因为 ASP.NET 将填充其他副本。

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>响应。重定向和响应。结束

建议：注意调用响应后如何处理线程[。重定向（String）](https://msdn.microsoft.com/library/t9dwyts4.aspx)。

[Response （String）](https://msdn.microsoft.com/library/t9dwyts4.aspx)方法调用 response 方法。 在同步过程中，调用请求。重定向会导致当前线程立即中止。 但是，在异步过程中，调用响应。重定向不会中止当前线程，因此请求会继续执行代码。 在异步过程中，您必须从方法返回任务以停止执行代码。

在 MVC 项目中，不应调用 Response。重定向。 而是返回 RedirectResult。

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState 和 ViewStateMode

建议：使用 ViewStateMode 而不是 EnableViewState 来提供对使用视图状态的控件的精细控制。

在 Page 指令中将 EnableViewState 设置为 false 时，将为该页中的所有控件禁用视图状态，并且无法启用。 如果要仅对页面中的某些控件启用视图状态，请将页面的 "ViewStateMode" 设置为 "已禁用"。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

然后，将 ViewStateMode 设置为仅在实际需要视图状态的控件上启用。

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

通过只为需要它的控件启用视图状态，可以缩小网页的视图状态大小。

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

建议：使用通用提供程序。

在当前项目模板中，SqlMembershipProvider 已由[ASP.NET 通用提供程序](http://www.nuget.org/packages/Microsoft.AspNet.Providers)替换，可作为 NuGet 包提供。 如果在使用早期版本的模板生成的项目中使用 SqlMembershipProvider，则应切换到通用提供程序。 通用提供程序适用于实体框架支持的所有数据库。

有关详细信息，请参阅[简介 ASP.NET 通用提供程序](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)。

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>长时间运行的请求（> 110 秒）

建议：为已连接的客户端使用[websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)或[SignalR](../../../signalr/index.md) ，并使用异步 i/o 操作。

长时间运行的请求可能会导致不可预知的结果，并降低 web 应用程序的性能。 请求的默认超时设置为110秒。 如果要将会话状态与长时间运行的请求一起使用，则 ASP.NET 将在110秒后释放会话对象的锁。 但是，当锁被释放时，您的应用程序可能正在对 Session 对象执行操作，并且该操作可能无法成功完成。 如果第一个请求在运行时阻止了来自用户的第二个请求，则第二个请求可能会以不一致的状态访问会话对象。

如果你的应用程序包括阻止（或同步） i/o 操作，则应用程序将无响应。

若要提高性能，请在 .NET Framework 中使用异步 i/o 操作。 此外，请使用 Websocket 或 SignalR 将客户端连接到服务器。 这些功能旨在有效地处理长时间运行的请求。
