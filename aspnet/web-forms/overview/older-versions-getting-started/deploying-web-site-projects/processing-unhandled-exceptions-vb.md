---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
title: 处理未经处理的异常（VB） |Microsoft Docs
author: rick-anderson
description: 在生产环境中的 web 应用程序上发生运行时错误时，请务必通知开发人员并记录错误，以便可以在 la 上诊断 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 051296f0-9519-4e78-835c-d868da13b0a0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 8d2e12af29bd95ce9898fa6a5e81be8b7a761f76
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473636"
---
# <a name="processing-unhandled-exceptions-vb"></a>处理未经处理的异常 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[查看或下载示例代码](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb/samples)（[如何下载](/aspnet/core/tutorials/index#how-to-download-a-sample)）

> 在生产环境中的 web 应用程序上发生运行时错误时，请务必通知开发人员并记录错误，以便在以后的某个时间点进行诊断。 本教程概述了 ASP.NET 如何处理运行时错误，并探讨了每当未处理的异常冒泡到 ASP.NET 运行时，将执行自定义代码的一种方法。

## <a name="introduction"></a>简介

当 ASP.NET 应用程序中发生未经处理的异常时，它将冒泡到 ASP.NET 运行时，这会引发 `Error` 事件并显示相应的错误页。 有三种不同类型的错误页：运行时错误黄色屏幕死亡（YSOD）;异常详细信息 YSOD;和自定义错误页。 在[前面的教程](displaying-a-custom-error-page-vb.md)中，我们将应用程序配置为使用远程用户的自定义错误页，并 YSOD 用户访问本地的用户的异常详细信息。

对于默认的运行时错误 YSOD，使用与站点的外观匹配的用户友好自定义错误页是首选的，但是显示自定义错误页只是综合性错误处理解决方案的一部分。 如果在生产环境中出现错误，开发人员会收到错误通知，以便他们能够发现异常的原因并解决该错误。 此外，还应记录错误的详细信息，以便在以后的某个时间点检查和诊断错误。

本教程演示如何访问未经处理的异常的详细信息，以便可以记录这些异常，并通知开发人员。 此教程后面的两个教程将探讨错误日志记录库，这些库在配置后将自动通知开发人员运行时错误并记录其详细信息。

> [!NOTE]
> 如果需要以某种独特的方式处理未经处理的异常，则本教程中检查的信息最有用。 如果只需要记录异常并通知开发人员，则使用错误日志记录库是一种方法。 接下来的两个教程概括介绍了两个库。

## <a name="executing-code-when-theerrorevent-is-raised"></a>引发`Error`事件时执行代码

事件为对象提供了一种机制，用于指示发生了一些有趣的事情，以及另一个对象执行代码以响应。 作为 ASP.NET 开发人员，您习惯于考虑到事件。 如果希望在访问者单击特定按钮时运行某些代码，请为该按钮的 `Click` 事件创建事件处理程序，并将代码放在此处。 假设每当发生未经处理的异常时，ASP.NET 运行时都会引发其[`Error` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)，随后会在事件处理程序中记录错误的详细信息。 但如何为 `Error` 事件创建事件处理程序呢？

`Error` 事件是[`HttpApplication` 类](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)中的多个事件之一，这些事件在请求的生存期内在 HTTP 管道中的特定阶段引发。 例如，在每个请求开始时引发 `HttpApplication` 类的[`BeginRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx);当安全模块识别请求程序时，将引发其[`AuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)。 这些 `HttpApplication` 事件使页面开发人员能够在请求生存期的各个点上执行自定义逻辑。

可以将 `HttpApplication` 事件的事件处理程序放置在一个名为 `Global.asax`的特殊文件中。 若要在网站中创建此文件，请使用名为 `Global.asax`的全局应用程序类模板将新项添加到网站的根目录。

[![](processing-unhandled-exceptions-vb/_static/image2.png)](processing-unhandled-exceptions-vb/_static/image1.png)

**图 1**：将 `Global.asax` 添加到 Web 应用程序  
 （[单击以查看完全大小的映像](processing-unhandled-exceptions-vb/_static/image3.png)）

根据你使用的是 Web 应用程序项目（WAP）还是网站项目（WSP），Visual Studio 创建的 `Global.asax` 文件的内容和结构略有不同。 对于 WAP，`Global.asax` 作为两个单独的文件实现 `Global.asax` 和 `Global.asax.vb`。 `Global.asax` 文件只包含一个引用 `.vb` 文件的 `@Application` 指令;相关事件处理程序在 `Global.asax.vb` 文件中定义。 对于 WSPs，只会创建一个文件，`Global.asax`，并在 `<script runat="server">` 块中定义事件处理程序。

在 WAP by Visual Studio 的全局应用程序类模板中创建的 `Global.asax` 文件包括名为 `Application_BeginRequest`、`Application_AuthenticateRequest`和 `Application_Error`的事件处理程序，这些事件处理程序分别是 `HttpApplication` 事件的事件处理程序 `BeginRequest`、`AuthenticateRequest`和 `Error`。 还有名为 `Application_Start`、`Session_Start`、`Application_End`和 `Session_End`的事件处理程序，这些事件处理程序是在 web 应用程序启动、新会话启动时、应用程序结束时以及会话结束时触发的事件处理程序。 在 WSP 中通过 Visual Studio 创建的 `Global.asax` 文件只包含 `Application_Error`、`Application_Start`、`Session_Start`、`Application_End`和 `Session_End` 事件处理程序。

> [!NOTE]
> 部署 ASP.NET 应用程序时，需要将 `Global.asax` 文件复制到生产环境中。 不需要将在 WAP 中创建的 `Global.asax.vb` 文件复制到生产，因为此代码编译到项目的程序集中。

Visual Studio 的全局应用程序类模板创建的事件处理程序并不详尽。 可以通过将事件处理程序命名为 `Application_EventName`，为任何 `HttpApplication` 事件添加事件处理程序。 例如，可以将以下代码添加到 `Global.asax` 文件中，以便为[`AuthorizeRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)创建事件处理程序：

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample1.vb)]

同样，您可以删除任何不需要的全局应用程序类模板创建的事件处理程序。 对于本教程，我们只需 `Error` 事件的事件处理程序;可以随意删除 `Global.asax` 文件中的其他事件处理程序。

> [!NOTE]
> *HTTP 模块*提供了另一种为 `HttpApplication` 事件定义事件处理程序的方法。 HTTP 模块是作为类文件创建的，它可以直接放置在 web 应用程序项目中或分成单独的类库。 由于可以将它们分为一个类库，因此 HTTP 模块提供了更灵活且可重复使用的模型，可用于创建 `HttpApplication` 事件处理程序。 `Global.asax` 文件特定于其所在的 web 应用程序，因此可以将 HTTP 模块编译成程序集，此时将 HTTP 模块添加到网站中就像将程序集放在 `Bin` 文件夹中，并在 `Web.config`注册模块一样简单。 本教程不介绍如何创建和使用 HTTP 模块，但以下两个教程中使用的两个错误日志记录库是作为 HTTP 模块实现的。 有关 HTTP 模块的优点的更多背景信息，请参阅[使用 Http 模块和处理程序创建可插入的 ASP.NET 组件](https://msdn.microsoft.com/library/aa479332.aspx)。

## <a name="retrieving-information-about-the-unhandled-exception"></a>检索有关未经处理的异常的信息

此时，我们有一个带有 `Application_Error` 事件处理程序的 global.asax 文件。 在此事件处理程序执行时，需要通知开发人员此错误并记录其详细信息。 若要完成这些任务，我们首先需要确定所引发异常的详细信息。 使用服务器对象的[`GetLastError` 方法](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx)可以检索导致引发 `Error` 事件的未处理异常的详细信息。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample2.vb)]

`GetLastError` 方法返回 `Exception`类型的对象，该对象是 .NET Framework 中所有异常的基类型。 但是，在上面的代码中，我将 `GetLastError` 返回的异常对象强制转换为 `HttpException` 的对象。 如果 `Error` 事件正在激发，因为在 ASP.NET 资源的处理过程中引发了异常，则会将引发的异常包装在 `HttpException`中。 若要获取被错误事件的实际异常，请使用 `InnerException` 属性。 如果由于基于 HTTP 的异常引发了 `Error` 事件（例如，对不存在的页的请求），则会引发 `HttpException`，但不会出现内部异常。

下面的代码使用 `GetLastErrormessage` 检索有关触发 `Error` 事件的异常的信息，并将 `HttpException` 存储在名为 `lastErrorWrapper`的变量中。 然后，它将原始异常的类型、消息和堆栈跟踪存储在三个字符串变量中，检查 `lastErrorWrapper` 是触发 `Error` 事件的实际异常（对于基于 HTTP 的异常），还是只是在处理请求时引发的异常的包装器。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample3.vb)]

此时，您需要编写代码，以便将异常的详细信息记录到数据库表中。 您可以为相关的每个错误详细信息（类型、消息、堆栈跟踪等）和其他有用的信息（例如请求的页面的 URL 和当前登录的用户的名称）创建包含列的数据库表。 然后，在 `Application_Error` 事件处理程序中，连接到数据库并将记录插入到表中。 同样，您可以添加代码以通过电子邮件向开发人员发出错误消息。

接下来的两个教程中所述的错误日志记录库提供了此类功能，因此无需自行生成此错误日志记录和通知。 但是，为了说明引发 `Error` 事件，并且 `Application_Error` 事件处理程序可用于记录错误详细信息并通知开发人员，我们将添加代码，以便在发生错误时通知开发人员。

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>在发生未经处理的异常时通知开发人员

当生产环境中发生未处理的异常时，请务必向开发团队发出警报，以便他们可以评估错误并确定需要采取哪些操作。 例如，如果在连接到数据库时出错，则需要仔细检查连接字符串，或许还需要与 web 托管公司建立支持票证。 如果异常是由于编程错误而发生的，则可能需要添加其他代码或验证逻辑，以防以后出现此类错误。

使用[`System.Net.Mail` 命名空间](https://msdn.microsoft.com/library/system.net.mail.aspx)中的 .NET Framework 类可以轻松地发送电子邮件。 [`MailMessage` 类](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx)表示一封电子邮件，其属性如 `To`、`From`、`Subject`、`Body`和 `Attachments`。 `SmtpClass` 用于使用指定的 SMTP 服务器发送 `MailMessage` 对象;可以通过编程方式或在 `Web.config file`的[`<system.net>` 元素](https://msdn.microsoft.com/library/6484zdc1.aspx)中以编程方式指定 SMTP 服务器设置。 有关在 ASP.NET 应用程序中发送电子邮件的详细信息，请参阅我的文章、[在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)和[系统 .NET. Mail 常见问题解答](http://systemnetmail.com/)。

> [!NOTE]
> `<system.net>` 元素包含 `SmtpClient` 类在发送电子邮件时使用的 SMTP 服务器设置。 Web 托管公司可能有可用于从应用程序发送电子邮件的 SMTP 服务器。 有关应在 web 应用程序中使用的 SMTP 服务器设置的信息，请参阅 web 宿主的支持部分。

将以下代码添加到 `Application_Error` 事件处理程序，以便在发生错误时向开发人员发送电子邮件：

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample4.vb)]

尽管上面的代码非常冗长，但大部分代码会创建在发送给开发人员的电子邮件中显示的 HTML。 代码首先引用 `GetLastError` 方法（`lastErrorWrapper`）返回的 `HttpException`。 通过 `lastErrorWrapper.InnerException` 检索请求引发的实际异常，并将其分配给变量 `lastError`。 类型、消息和堆栈跟踪信息是从 `lastError` 检索的，并存储在三个字符串变量中。

接下来，创建一个名为 `mm` 的 `MailMessage` 对象。 电子邮件正文为 HTML 格式，并显示请求的页面的 URL、当前登录用户的名称以及有关异常的信息（类型、消息和堆栈跟踪）。 `HttpException` 类的一个很酷的问题是，你可以通过调用[GetHtmlErrorMessage 方法](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)来生成用于创建异常详细信息的 HTML。 此处使用此方法检索异常详细信息 YSOD 标记，并将其作为附件添加到电子邮件中。 注意：如果触发 `Error` 事件的异常是基于 HTTP 的异常（例如，对不存在的页的请求），则 `GetHtmlErrorMessage` 方法将返回 `null`。

最后一步是发送 `MailMessage`。 这是通过创建新的 `SmtpClient` 方法并调用其 `Send` 方法来完成的。

> [!NOTE]
> 在您的 web 应用程序中使用此代码之前，您需要更改 "`ToAddress` 中的值并 `FromAddress` 常量从 support@example.com 发送到错误通知电子邮件应发送到的电子邮件地址，并从该地址发起。 还需要在 `Web.config`的 "`<system.net>`" 部分中指定 SMTP 服务器设置。 请咨询 web 主机提供商以确定要使用的 SMTP 服务器设置。

无论何时出现错误，开发人员都会向开发人员发送一封电子邮件，该电子邮件汇总了错误并包含 YSOD。 在前面的教程中，我们通过访问流派来演示了运行时错误，并通过 querystring 传入了无效的 `ID` 值，如 `Genre.aspx?ID=foo`。 如果在开发环境中访问与 `Global.asax` 文件相同的用户体验，则在开发环境中，将继续看到异常详细信息黄色屏幕死亡，而在生产环境中，你会看到自定义错误页。 除了此现有行为外，开发人员还将发送一封电子邮件。

**图 2**显示访问 `Genre.aspx?ID=foo`时收到的电子邮件。 电子邮件正文汇总了异常信息，而 `YSOD.htm` 附件显示了异常详细信息 YSOD 中显示的内容（请参阅**图 3**）。

[![](processing-unhandled-exceptions-vb/_static/image5.png)](processing-unhandled-exceptions-vb/_static/image4.png)

**图 2**：每当出现未经处理的异常时，开发人员都会收到电子邮件通知  
 （[单击以查看完全大小的映像](processing-unhandled-exceptions-vb/_static/image6.png)）

[![](processing-unhandled-exceptions-vb/_static/image8.png)](processing-unhandled-exceptions-vb/_static/image7.png)

**图 3**：电子邮件通知包括异常详细信息 YSOD 作为附件  
 （[单击以查看完全大小的映像](processing-unhandled-exceptions-vb/_static/image9.png)）

## <a name="what-about-using-the-custom-error-page"></a>使用自定义错误页的情况如何？

本教程演示了如何在发生未经处理的异常时使用 `Global.asax` 和 `Application_Error` 事件处理程序执行代码。 具体而言，我们使用此事件处理程序将错误通知开发人员;我们可以将其扩展为，同时记录数据库中的错误详细信息。 `Application_Error` 事件处理程序的存在不会影响最终用户的体验。 它们仍会看到配置的错误页，YSOD 错误详细信息、运行时错误 YSOD 或自定义错误页。

使用自定义错误页面时，很有必要知道 `Global.asax` 文件和 `Application_Error` 事件是否是必需的。 当发生错误时，用户将显示在 "自定义错误" 页上，为什么我们不能将代码通知开发人员，并将错误详细信息记录到自定义错误页的代码隐藏类中呢？ 虽然您当然可以将代码添加到自定义错误页的代码隐藏类，但使用我们在前面的教程中探讨的技术时，您无法访问触发 `Error` 事件的异常的详细信息。 从自定义错误页调用 `GetLastError` 方法将返回 `Nothing`。

此行为的原因是因为通过重定向到达了自定义错误页。 当未处理的异常到达 ASP.NET 运行时时，ASP.NET 引擎引发其 `Error` 事件（执行 `Application_Error` 事件处理程序），然后通过发出 `Response.Redirect(customErrorPageUrl)`将用户*重定向*到自定义错误页。 `Response.Redirect` 方法使用 HTTP 302 状态代码将响应发送到客户端，指导浏览器请求新的 URL，即自定义错误页。 然后，浏览器会自动请求此新页面。 您可以知道自定义错误页是从错误产生的页面中单独请求的，因为浏览器的地址栏更改为自定义错误页 URL （请参阅**图 4**）。

[![](processing-unhandled-exceptions-vb/_static/image11.png)](processing-unhandled-exceptions-vb/_static/image10.png)

**图 4**：发生错误时，浏览器将重定向到自定义错误页 URL  
 （[单击以查看完全大小的映像](processing-unhandled-exceptions-vb/_static/image12.png)）

最终效果是，在服务器响应 HTTP 302 重定向时，发生未经处理的异常的请求结束。 对自定义错误页的后续请求是全新请求;此时，ASP.NET 引擎放弃了错误信息，而且还无法将上一个请求中的未处理异常与新的自定义错误页请求相关联。 这就是从自定义错误页调用 `GetLastError` 返回 `null` 的原因。

但是，可以在导致错误的同一请求期间执行自定义错误页。 [`Server.Transfer(url)`](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx)方法将执行转移到指定的 URL，并在同一请求中对其进行处理。 可以将 `Application_Error` 事件处理程序中的代码移到自定义错误页的代码隐藏类，并在 `Global.asax` 中将其替换为以下代码：

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample5.vb)]

现在，当发生未处理的异常时，`Application_Error` 事件处理程序会根据 HTTP 状态代码将控制转移到适当的自定义错误页。 由于已传输控制权，因此自定义错误页可以通过 `Server.GetLastError` 访问未经处理的异常信息，并可以通知开发人员出现错误并记录其详细信息。 `Server.Transfer` 调用会阻止 ASP.NET 引擎将用户重定向到自定义错误页。 相反，自定义错误页的内容将作为对生成错误的页的响应返回。

## <a name="summary"></a>摘要

当 ASP.NET web 应用程序中发生未经处理的异常时，ASP.NET 运行时会引发 `Error` 事件，并显示配置的错误页。 通过为错误事件创建事件处理程序，我们可以通知开发人员错误、记录其详细信息或以其他方式进行处理。 可以通过两种方法为 `HttpApplication` 事件创建事件处理程序，如 `Error`：在 `Global.asax` 文件中，或从 HTTP 模块。 本教程演示了如何在 `Global.asax` 文件中创建一个 `Error` 事件处理程序，该处理程序通过电子邮件通知开发人员出现错误。

如果需要以某种独特或自定义的方式处理未经处理的异常，则创建 `Error` 事件处理程序会很有用。 但是，创建自己的 `Error` 事件处理程序来记录异常或通知开发人员并不是最有效的时间，因为已存在可在几分钟内设置的免费且易于使用的错误日志记录库。 接下来的两个教程检查两个这类库。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET HTTP 模块和 HTTP 处理程序概述](https://support.microsoft.com/kb/307985)
- [正确响应未处理的异常-处理未经处理的异常](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` 类和 ASP.NET 应用程序对象](http://www.eggheadcafe.com/articles/20030211.asp)
- [ASP.NET 中的 HTTP 处理程序和 HTTP 模块](http://www.15seconds.com/Issue/020417.htm)
- [在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [了解 `Global.asax` 文件](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [使用 HTTP 模块和处理程序创建可插入的 ASP.NET 组件](https://msdn.microsoft.com/library/aa479332.aspx)
- [使用 ASP.NET `Global.asax` 文件](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [使用 `HttpApplication` 实例](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [上一页](displaying-a-custom-error-page-vb.md)
> [下一页](logging-error-details-with-asp-net-health-monitoring-vb.md)
