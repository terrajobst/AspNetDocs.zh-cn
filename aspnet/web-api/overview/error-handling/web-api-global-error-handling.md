---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2 中的全局错误处理-ASP.NET 4。x
author: davidmatson
description: ASP.NET 4.x 的 ASP.NET Web API 2 中全局错误处理的概述。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 94f2d6d31d0b37f9bb0077e6258c70a2dfb1918d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448964"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的全局错误处理

按[David Matson](https://github.com/davidmatson)， [Rick Anderson](https://twitter.com/RickAndMSFT)

本主题概述了 ASP.NET 4.x ASP.NET Web API 2 中的全局错误处理。 现在，Web API 无法通过全局方式记录或处理错误。 某些未经处理的异常可以通过[异常筛选器](exception-handling.md)进行处理，但异常筛选器无法处理多种情况。 例如:

1. 从控制器构造函数引发的异常。
2. 从消息处理程序引发的异常。
3. 在路由过程中引发的异常。
4. 在响应内容序列化过程中引发的异常。

我们想要提供一种简单、一致的方法来记录和处理这些异常。 

处理异常的主要情况有两种，在这种情况下，我们能够发送错误响应，而我们只需要记录异常。 后一种情况的一个示例是在流响应内容的中间引发异常;在这种情况下，发送新响应消息的时间太晚，因为状态代码、标头和部分内容已在网络中消失，因此我们只需中止连接。 即使无法处理异常以生成新的响应消息，仍仍支持记录异常。 在检测到错误的情况下，我们可以返回相应的错误响应，如下所示：

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>现有选项

除了[异常筛选器](exception-handling.md)外，现在还可以使用[消息处理程序](../advanced/http-message-handlers.md)来观察所有500级别的响应，但对这些响应的作用非常困难，因为它们缺乏有关原始错误的上下文。 消息处理程序还具有与异常筛选器有关的一些限制，这些限制与它们可以处理的情况有关。尽管 Web API 有捕获错误情况的跟踪基础结构，但跟踪基础结构用于诊断目的，但并不是在生产环境中运行或不适合在生产环境中运行。 全局异常处理和日志记录应该是可在生产过程中运行并插入现有监视解决方案（例如， [ELMAH](https://code.google.com/p/elmah/) ）的服务。

### <a name="solution-overview"></a>解决方案概述

 我们提供了两个新的用户可替换服务（ [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md)和 IExceptionHandler）来记录和处理未经处理的异常。 服务非常相似，但有两个主要区别：

1. 我们支持注册多个异常记录器，而只是一个异常处理程序。
2. 即使要中止连接，也始终会调用异常记录器。 仅当我们仍可以选择要发送的响应消息时，才会调用异常处理程序。

这两种服务都提供对包含异常检测点的相关信息的异常上下文的访问，特别是[HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)、 [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)、引发的异常和异常源（下面的详细信息）。

### <a name="design-principles"></a>设计原理

1. **无重大更改**由于此功能是在次要版本中添加的，因此，影响解决方案的一个重要约束是不会对类型协定或行为进行重大更改。 此约束排除了某些清理，我们想要在现有的 catch 块中实现将异常转换为500响应。 对于后续的主要发布，我们可能会考虑这种额外的清理操作。 如果这对你很重要，请在[ASP.NET Web API 用户语音](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)上投票。
2. **维护 WEB API 构造的一致性**Web API 的筛选器管道是一种很好的方法，可以通过在特定于控制器或全局范围内应用逻辑的灵活性来处理交叉切削问题。 筛选器（包括异常筛选器）始终具有操作和控制器上下文，即使是在全局范围内注册也是如此。 该协定对于筛选器是有意义的，但这意味着异常筛选器（甚至是全局范围的筛选器）不适合用于某些异常处理情况，如消息处理程序中不存在任何操作或控制器上下文的异常。 如果我们想要使用筛选器提供的可变范围来处理异常，则仍需要异常筛选器。 但是，如果我们需要处理控制器上下文之外的异常，我们还需要一个单独的构造来实现全局错误处理（没有控制器上下文和操作上下文约束的内容）。

### <a name="when-to-use"></a>何时使用

- 异常记录器是查看 Web API 捕获的所有未处理异常的解决方案。
- 异常处理程序是一种解决方案，用于自定义对 Web API 捕获的未处理异常的所有可能的响应。
- 异常筛选器是处理与特定操作或控制器相关的部分未处理异常的最简单解决方案。

### <a name="service-details"></a>服务详情

 异常记录器和处理程序服务接口是简单的异步方法，采用各自的上下文： 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 我们还提供了这两个接口的基类。 重写核心（同步或异步）方法是指在建议时间记录或处理的全部。 对于日志记录，`ExceptionLogger` 基类将确保只为每个异常调用一次核心日志记录方法（即使稍后在调用堆栈上进一步传播并再次捕获）。 `ExceptionHandler` 基类将仅对调用堆栈顶部的异常调用核心处理方法，同时忽略旧的嵌套 catch 块。 （下面的附录中介绍了这些基类的简化版本。）`IExceptionLogger` 和 `IExceptionHandler` 通过 `ExceptionContext`接收有关异常的信息。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

当框架调用异常记录器或异常处理程序时，它将始终提供 `Exception` 和 `Request`。 除了单元测试以外，它还将始终提供 `RequestContext`。 它很少提供 `ControllerContext` 和 `ActionContext` （仅在从异常筛选器的 catch 块中调用时）。 它很少提供 `Response`（仅在尝试写入响应的某些 IIS 情况下）。 请注意，由于某些属性可能 `null` 在访问 exception 类的成员之前，使用者检查 `null`。`CatchBlock` 一个字符串，指示哪个 catch 块看到了该异常。 Catch 块字符串如下所示：

- HttpServer （SendAsync 方法）
- System.web.http.exceptionhandling.exceptioncatchblocks.httpcontrollerdispatcher.sendasync （SendAsync 方法）
- System.web.http.exceptionhandling.exceptioncatchblocks.httpbatchhandler.sendasync （SendAsync 方法）
- IExceptionFilter （ApiController 在 ExecuteAsync 中处理异常筛选器管道）
- OWIN 主机：

    - HttpMessageHandlerAdapter. BufferResponseContentAsync （用于缓冲输出）
    - HttpMessageHandlerAdapter. CopyResponseContentAsync （用于流输出）
- Web 主机：

    - HttpControllerHandler. System.web.http.webhost.httpcontrollerhandler.writebufferedresponsecontentasync （用于缓冲输出）
    - HttpControllerHandler. System.web.http.webhost.httpcontrollerhandler.writestreamedresponsecontentasync （用于流输出）
    - HttpControllerHandler. System.web.http.webhost.httpcontrollerhandler.writeerrorresponsecontentasync （在缓冲输出模式下恢复错误时）

Catch 块字符串列表还可通过静态 readonly 属性获得。 （核心 catch 块字符串位于静态 System.web.http.exceptionhandling.exceptioncatchblocks.httpserver.sendasync 上; 余数显示在一个静态类上，每个静态类用于 OWIN 和 web 主机）。`IsTopLevelCatchBlock` 对于在调用堆栈顶部遵循建议的处理异常模式非常有用。 异常处理程序不会在嵌套的 catch 块发生的任何位置将异常转换为500响应，而是允许异常传播到它们即将被宿主查看。

除了 `ExceptionContext`，记录器还通过完整 `ExceptionLoggerContext`获取一段信息：

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

第二个属性 `CanBeHandled`允许记录器识别无法处理的异常。 当即将中止连接并且不能发送新的响应消息时，将调用记录器，但***不***会调用该处理程序，并且记录器可以通过此属性来标识此方案。

在 `ExceptionContext`中，处理程序将获取一个可在整个 `ExceptionHandlerContext` 上设置的属性来处理异常：

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

异常处理程序通过将 `Result` 属性设置为操作结果（例如， [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx)、 [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)、 [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)或自定义结果）来指示它已处理了异常。 如果 `Result` 属性为 null，则不会处理异常，将重新引发原始异常。

对于调用堆栈顶部的异常，我们采取了额外的步骤来确保响应适用于 API 调用方。 如果异常向上传播到主机，则调用方将显示死亡的黄色屏幕或一些其他主机提供的响应，通常是 HTML，通常不是相应的 API 错误响应。 在这些情况下，结果将从非空值开始，并且仅当自定义异常处理程序将其显式设置回 `null` （未处理）时，才会将异常传播到主机。 在这种情况下，将 `Result` 设置为 `null` 对于两种情况可能很有用：

1. OWIN 托管的 Web API，其中包含自定义异常处理在 Web API 之前/外部注册的中间件。
2. 通过浏览器进行本地调试，其中黄色的死亡对于未经处理的异常实际上是一个有帮助的响应。

对于异常记录器和异常处理程序，如果记录器或处理程序本身引发异常，则不会执行任何操作。 （除了允许异常传播外，如果你有更好的方法，请在本页底部留下反馈。）异常记录器和处理程序的协定是它们不应允许异常传播到其调用方;否则，异常将直接传播到主机上，从而导致出现 HTML 错误（如 ASP）。NET 的黄色屏幕）发送回客户端（这通常不是需要 JSON 或 XML 的 API 调用方的首选选项）。

## <a name="examples"></a>示例

### <a name="tracing-exception-logger"></a>跟踪异常记录器

下面的异常记录器将异常数据发送到配置的跟踪源（包括 Visual Studio 中的 "调试输出" 窗口）。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>自定义错误消息异常处理程序

以下为客户端生成自定义错误响应，包括与支持联系的电子邮件地址。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>注册异常筛选器

如果使用 "ASP.NET MVC 4 Web 应用程序" 项目模板来创建项目，请将 Web API 配置代码放在*应用/_Start*文件夹中的 `WebApiConfig` 类中：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>附录：基类详细信息

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
