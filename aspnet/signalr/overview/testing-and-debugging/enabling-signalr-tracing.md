---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: 启用 SignalR 跟踪 |Microsoft Docs
author: bradygaster
description: 本文档介绍如何为 SignalR 服务器和客户端启用和配置跟踪。 利用跟踪功能，您可以查看有关事件的诊断信息 。
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467438"
---
# <a name="enabling-signalr-tracing"></a>启用 SignalR 跟踪

通过[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍如何为 SignalR 服务器和客户端启用和配置跟踪。 跟踪使你可以查看有关 SignalR 应用程序中事件的诊断信息。
>
> 本主题最初由 Fletcher 的写作。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR 版本2
>
>
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

启用跟踪后，SignalR 应用程序会创建事件的日志项。 你可以从客户端和服务器记录事件。 跟踪服务器日志连接、扩展提供程序和消息总线事件。 对客户端的跟踪记录连接事件。 在 SignalR 2.1 和更高版本中，在客户端上进行的跟踪会记录中心调用消息的全部内容。

## <a name="contents"></a>内容

- [在服务器上启用跟踪](#server)

    - [将服务器事件记录到文本文件](#server_text)
    - [将服务器事件记录到事件日志中](#server_eventlog)
- [在 .NET 客户端中启用跟踪（Windows 桌面应用程序）](#net_client)

    - [向控制台记录桌面客户端事件](#desktop_console)
    - [将桌面客户端事件记录到文本文件中](#desktop_text)
- [在 Windows Phone 8 个客户端中启用跟踪](#phone)

    - [将客户端事件 Windows Phone 日志记录到 UI](#phone_ui)
    - [将客户端事件 Windows Phone 日志记录到调试控制台](#phone_debug)
- [在 JavaScript 客户端中启用跟踪](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>在服务器上启用跟踪

在应用程序的配置文件（App.config 或 web.config 中，具体取决于项目的类型）上启用对服务器的跟踪。指定要记录的事件的类别。 在配置文件中，还可以指定是使用[TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)的实现将事件记录到文本文件、Windows 事件日志还是自定义日志。

服务器事件类别包含以下消息种类：

| Source | 消息 |
| --- | --- |
| SignalR.SqlMessageBus | SQL 消息总线扩展提供程序设置、数据库操作、错误和超时事件 |
| SignalR.ServiceBusMessageBus | Service bus 扩展提供程序主题创建和订阅、错误和消息传递事件 |
| SignalR.RedisMessageBus | Redis 扩展提供程序连接、断开连接和错误事件 |
| SignalR.ScaleoutMessageBus | 扩展消息传递事件 |
| SignalR.Transports.WebSocketTransport | WebSocket 传输连接、断开连接、消息传递和错误事件 |
| SignalR.Transports.ServerSentEventsTransport | ServerSentEvents 传输连接、断开连接、消息传递和错误事件 |
| SignalR.Transports.ForeverFrameTransport | ForeverFrame 传输连接、断开连接、消息传递和错误事件 |
| SignalR.Transports.LongPollingTransport | LongPolling 传输连接、断开连接、消息传递和错误事件 |
| SignalR.Transports.TransportHeartBeat | 传输连接、断开连接和 keepalive 事件 |
| SignalR.ReflectedHubDescriptorProvider | 中心发现事件 |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>将服务器事件记录到文本文件

下面的代码演示如何为每个事件类别启用跟踪。 此示例将应用程序配置为将事件记录到文本文件中。

**用于启用跟踪的 XML 服务器代码**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

在上面的代码中，`SignalRSwitch` 项指定用于发送到指定日志的事件的[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 。 在这种情况下，它设置为 `Verbose` 这意味着记录所有调试和跟踪消息。

以下输出显示了使用上述配置文件的应用程序 `transports.log.txt` 文件中的条目。 它显示新连接、已删除的连接和传输检测信号事件。

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>将服务器事件记录到事件日志中

若要将事件记录到事件日志而不是文本文件，请更改 "`sharedListeners`" 节点中的项的值。 下面的代码演示如何将服务器事件记录到事件日志中：

**用于将事件记录到事件日志的 XML 服务器代码**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

事件记录在应用程序日志中，并通过事件查看器提供，如下所示：

![显示 SignalR 日志的事件查看器](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> 使用事件日志时，请将 " **TraceLevel** " 设置为 " **Error** "，以保持消息的可管理性。

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>在 .NET 客户端中启用跟踪（Windows 桌面应用程序）

.NET 客户端可以[使用对等](https://msdn.microsoft.com/library/system.io.textwriter.aspx)的实现将事件记录到控制台、文本文件或自定义日志。

若要在 .NET 客户端中启用日志记录，请将连接的 `TraceLevel` 属性设置为 TraceLevels 值，将 `TraceWriter` 属性设置[为有效的](https://msdn.microsoft.com/library/system.io.textwriter.aspx) [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 。

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>向控制台记录桌面客户端事件

下面C#的代码演示如何将 .net 客户端中的事件记录到控制台：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>将桌面客户端事件记录到文本文件中

下面C#的代码演示如何将 .net 客户端中的事件记录到文本文件中：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

以下输出显示了使用上述配置文件的应用程序 `ClientLog.txt` 文件中的条目。 它显示连接到服务器的客户端，以及调用 `addMessage`的客户端方法的中心：

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>在 Windows Phone 8 个客户端中启用跟踪

用于 Windows Phone 应用程序的 SignalR 应用程序与桌面应用程序使用相同的 .NET 客户端[，但不](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)能使用[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)将其写入到文件。 相反，您需要为跟踪创建[一个用于跟踪的自](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)定义实现。

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>将客户端事件 Windows Phone 日志记录到 UI

[SignalR 基本代码](https://github.com/SignalR/SignalR/archive/master.zip)包含一个 Windows Phone 示例，该示例使用名为 `TextBlockWriter`[的自定义](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)类型为实现将跟踪输出写入[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 。 可在**samples/SignalR**项目中找到此类。 WP8。 在创建 `TextBlockWriter`的实例时，传入当前[SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)，并在[system.windows.controls.stackpanel>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中创建用于跟踪输出的[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

然后，跟踪输出将写入在传入的[system.windows.controls.stackpanel>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中创建的新[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>将客户端事件 Windows Phone 日志记录到调试控制台

若要将输出发送到调试控制台而不是 UI，请创建一个写入 "调试" 窗口并将其分配给连接的[TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) [属性的 "分配"。](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

然后，跟踪信息将写入 Visual Studio 中的 "调试" 窗口：

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>在 JavaScript 客户端中启用跟踪

若要对连接启用客户端日志记录，请在调用 `start` 方法来建立连接之前，设置连接对象上的 `logging` 属性。

**用于对浏览器控制台启用跟踪的客户端 JavaScript 代码（包含生成的代理）**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**用于对浏览器控制台启用跟踪的客户端 JavaScript 代码（不包含生成的代理）**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

启用跟踪后，JavaScript 客户端会将事件记录到浏览器控制台。 若要访问浏览器控制台，请参阅[监视传输](../getting-started/introduction-to-signalr.md#MonitoringTransports)。

以下屏幕截图显示了已启用跟踪的 SignalR JavaScript 客户端。 它在浏览器控制台中显示连接和中心调用事件：

![在浏览器控制台中 SignalR 跟踪事件](enabling-signalr-tracing/_static/image4.png)
