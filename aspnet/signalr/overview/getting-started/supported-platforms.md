---
uid: signalr/overview/getting-started/supported-platforms
title: 支持的平台 |Microsoft Docs
author: bradygaster
description: 本文介绍了 SignalR 支持的客户端和服务器。
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450122"
---
# <a name="supported-platforms"></a>支持的平台

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍了 SignalR 支持的客户端和服务器。 
> 
> ## <a name="questions-and-comments"></a>问题和注释
> 
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

在各种服务器和客户端配置下支持 SignalR。 此外，每个传输选项都具有自己的一组要求;如果传输的系统要求不可用，则 SignalR 将正常故障转移到其他传输。 有关 SignalR 支持的传输的详细信息，请参阅[传输和回退](introduction-to-signalr.md#transports)。

## <a name="server-system-requirements"></a>服务器系统要求

可以在各种服务器配置上托管 SignalR 服务器组件。 本部分介绍了支持的操作系统版本、.NET framework、Internet Information Server 和其他组件。

### <a name="supported-server-operating-systems"></a>支持的服务器操作系统

可在以下服务器或客户端操作系统中承载 SignalR 服务器组件。 请注意，对于 SignalR，若要使用 Websocket，需要 Windows Server 2012、Windows Server 2016 或 Windows 8 （可在 Microsoft Azure 网站上使用 WebSocket，前提是该站点的 .NET framework 版本设置为4.5，且在站点的配置页）。

- Windows 2016 Server
- Windows Server 2012
- Windows Server 2008 r2
- Windows 10
- Windows 8
- Windows 7
- Microsoft Azure

### <a name="supported-server-net-framework-version"></a>支持的服务器 .NET Framework 版本

仅 .NET Framework 4.5 支持 SignalR 2。 有关提高可靠性、兼容性、稳定性和性能的更新，请参阅[建议的更新](#updates)部分。

### <a name="supported-server-iis-versions"></a>支持的服务器 IIS 版本

当 SignalR 承载于 IIS 中时，支持以下版本。 请注意，如果使用客户端操作系统（例如 for 开发（Windows 8 或 Windows 7）），则不应使用完整版本的 IIS 或 Cassini，因为将同时施加10个同时进行的连接，这会由于连接是暂时性的，经常重新建立，并且不会在不再使用时立即释放。 IIS Express 应在客户端操作系统上使用。

另请注意，对于 SignalR 要使用 WebSocket，必须使用 IIS 8 或 IIS 8 Express，服务器必须使用 Windows 8、Windows Server 2012 或更高版本，并且必须在 IIS 中启用 WebSocket。 有关如何在 IIS 中启用 WebSocket 的信息，请参阅[iis 8.0 Websocket 协议支持](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)。

- IIS 8 或 IIS 8 Express。
- IIS 7 和7.5。 需要对[无扩展名 url](https://support.microsoft.com/kb/980368)的支持。
- IIS 必须在集成模式下运行;不支持经典模式。 如果使用服务器发送的事件传输在经典模式下运行 IIS，则可能会遇到长达30秒的消息延迟。
- 宿主应用程序必须在完全信任模式下运行。

## <a name="client-system-requirements"></a>客户端系统要求

SignalR 可用于各种客户端平台。 本部分介绍了在 web 浏览器、Windows 桌面应用程序、Silverlight 应用程序和移动设备中使用 SignalR 的系统要求。

### <a name="web-browsers"></a>Web 浏览器

SignalR 可用于各种 web 浏览器，但通常仅支持最新的两个版本。

在浏览器中使用 SignalR 的应用程序必须使用 jQuery 版本1.6.4 或更高版本（如1.7.2、1.8.2 或1.9.1）。

可以在以下浏览器中使用 SignalR：

- Microsoft Internet Explorer 8、9、10和11版。 支持新式版、桌面版和移动版。
- Mozilla Firefox：当前版本-1，Windows 和 Mac 版本。
- Google Chrome：当前版本-1，Windows 和 Mac 版本。
- Safari：当前版本-1，Mac 和 iOS 版本。
- Opera：当前版本-1，仅 Windows。
- Android 浏览器

除了需要某些浏览器外，SignalR 使用的各种传输都具有自己的要求。 以下配置支持以下传输：

<a id="browser"></a>

**Web 浏览器传输要求**

| 传输 | Internet Explorer | Chrome （Windows 或 iOS） | Firefox | Safari （OSX 或 iOS） | Android |
| --- | --- | --- | --- | --- | --- |
| WebSockets | 10+ | 当前-1 | 当前-1 | 当前-1 | 不适用 |
| 服务器发送的事件 | 不适用 | 当前-1 | 当前-1 | 当前-1 | 不适用 |
| ForeverFrame | 8+ | 不适用 | 不适用 | 不适用 | 4.1 |
| 长轮询 | 8+ | 当前-1 | 当前-1 | 当前-1 | 4.1 |

\*：需要 6 + 才能实现完整功能。

#### <a name="unsupported-browsers"></a>不受支持的浏览器

尽管 SignalR*可能会*在较旧的浏览器版本中运行而不会出现重大问题，但我们并不积极地测试 SignalR，通常不修复其中可能出现的 bug。

### <a name="windows-desktop-and-silverlight-applications"></a>Windows 桌面和 Silverlight 应用程序

除了在 web 浏览器中运行外，SignalR 还可以托管在独立的 Windows 客户端或 Silverlight 应用程序中。 Windows 桌面和 Silverlight SignalR 应用程序具有以下系统要求。

- Windows XP SP3 或更高版本支持使用 .NET 4 的应用程序。
- Windows Vista 或更高版本支持使用 .NET Framework 4.5 的应用程序。

除了操作系统和 .NET framework 要求外，SignalR 提供的传输还具有自己的要求。 以下配置支持以下传输：

**Windows 桌面和 Silverlight 传输要求**

| 传输 | .NET 应用程序 | Silverlight |
| --- | --- | --- |
| Web 套接字 | Windows 8 + 和 .NET 4.5 + | 不适用 |
| 永久帧 | 不适用 | 不适用 |
| 服务器发送的事件 | .NET 4+ | 5+ |
| 长轮询 | .NET 4+ | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Windows 应用商店和 Windows Phone 应用程序

SignalR 可以在 Windows 应用商店应用程序和 Windows Phone 8 应用程序中使用。 以下配置支持以下传输：

**Windows 应用商店和 Windows Phone 传输要求**

| 传输 | Windows 应用商店/.NET | Windows 应用商店/JavaScript | Windows Phone/ IE | Windows Phone/.NET |
| --- | --- | --- | --- | --- |
| WebSockets | 不适用 | Win8 + | 8+ | 不适用 |
| 永久帧 | 不适用 | Win8 + | 7.5+ | 不适用 |
| 服务器发送的事件 | Win8 + | 不适用 | 不适用 | 8+ |
| 长轮询 | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>建议的更新

建议对 SignalR 服务器进行以下更新：

- [此处](https://support.microsoft.com/kb/2750149)提供 .NET Framework 4.5 的更新。
- Microsoft 会定期发布 ASP.NET 的 Qfe。 应将它们应用为可用。
