---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: 项目 Katana 概述 |Microsoft Docs
author: howarddierking
description: ASP.NET 框架已超过10年，平台已经实现了无数个网站和服务的开发。 作为 Web 应用程序 。
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 1f28db822930cdfd2ebf4cf9bb27d173f4aa4201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500342"
---
# <a name="an-overview-of-project-katana"></a>项目 Katana 概述

作者： [Howard Dierking](https://github.com/howarddierking)

> ASP.NET 框架已超过10年，平台已经实现了无数个网站和服务的开发。 随着 Web 应用程序开发策略的发展，框架能够在 ASP.NET MVC 和 ASP.NET Web API 等技术中逐步发展。 由于 Web 应用程序开发将其下一个发展步骤带入云计算领域，project [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)提供了 ASP.NET 应用程序的基础组件集，使应用程序能够灵活、可移植、轻便并提供更好的性能–另外一种方法是，project [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) cloud 优化 ASP.NET 应用程序。

## <a name="why-katana--why-now"></a>为什么 Katana –为什么要这样做呢？

 无论是讨论开发人员框架还是最终用户产品，都必须了解用于创建产品的基础动机，这一点很重要，其中包括了解产品的创建者。 ASP.NET 最初是在两个客户中创建的。   
  
**第一组客户是经典 ASP 开发人员。** 目前，ASP 是通过 interweaving 标记和服务器端脚本创建动态、数据驱动的网站和应用程序的一项主要技术。 ASP 运行时为服务器端脚本提供了一组对象，这些对象抽象了基础 HTTP 协议和 Web 服务器的核心方面，并提供了对其他服务（如会话和应用程序状态管理、缓存等）的访问权限。虽然功能强大、经典的 ASP 应用程序在不断增长的同时也是一项挑战。 这在很大程度上是因为在脚本环境中找不到与代码和标记交错产生的代码重复的结构。 为了充分利用经典 ASP 的优势，同时应对其中一些挑战，ASP.NET 充分利用了由 .NET Framework 面向对象的语言提供的代码组织，同时还保留了服务器端编程模型经典 ASP 开发人员熟悉的。

**ASP.NET 的第二组目标客户是 Windows 业务应用程序开发人员。** 与经典 ASP 开发人员一样，熟悉编写 HTML 标记和代码以生成更多 HTML 标记，WinForms 开发人员（如他们之前的 VB6 开发人员）熟悉了包含画布和丰富用户集的设计时体验。接口控件。 第一个版本的 ASP.NET （也称为 "Web 窗体"）提供了类似的设计时体验，同时提供了用户界面组件的服务器端事件模型和一组基础结构功能（如 ViewState）来创建无缝的开发人员体验在客户端和服务器端编程之间。 Web 窗体在 WinForms 开发人员熟悉的有状态事件模型下有效地隐藏了 Web 的无状态特性。

### <a name="challenges-raised-by-the-historical-model"></a>历史模型引发的质询

**最终结果是一个功能丰富、功能丰富的运行时和开发人员编程模型。** 但是，使用该功能，有几个值得注意的问题。 首先，该框架是**单一**的，它具有逻辑上不同的功能单元，它们在同一个 system.web 程序集（例如，包含 Web 窗体框架的核心 HTTP 对象）中紧密耦合。 其次，ASP.NET 是较大 .NET Framework 的一部分，这意味着各**版本之间的时间将按年的顺序进行。** 这样，ASP.NET 就难以跟上不断发展的 Web 开发所发生的所有更改。 最后，使用几种不同方式为特定的 Web 宿主选项耦合了 System.web： Internet Information Services （IIS）。

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>进化步骤： ASP.NET MVC 和 ASP.NET Web API

Web 开发中发生了很多更改！ Web 应用程序越来越多地开发成一系列小型、集中的组件，而不是大型框架。 组件数量以及它们的发布频率在不断提高的速度。 保持 Web 的步调非常明显，需要框架才能获得更小、更分离、更集中而不是更富丰富的功能，因此， **ASP.NET 团队采取了几个发展的步骤，将 ASP.NET 作为可插入 Web 组件系列，而不是单一框架**。

最早的变化之一是众所周知的模型视图-控制器（MVC）设计模式的普及，这归功于 Web 开发框架，如 Ruby on Rails。 构建 Web 应用程序的这种样式使开发人员可以更好地控制其应用程序的标记，同时仍然保留标记和业务逻辑的分离，这是 ASP.NET 的初始卖点之一。 为了满足此样式的 Web 应用程序开发的需求，Microsoft 通过**开发 ASP.NET MVC** （而不是将其包含在 .NET Framework 中）来更好地定位自身。 ASP.NET MVC 作为独立下载发布。 这使工程团队能够比以前可能更频繁地交付更新。

Web 应用程序开发的另一个主要转变是从动态的服务器生成的网页过渡到静态初始标记，并在客户端脚本中生成的页面的动态部分**通过 AJAX 请求与后端 Web api**进行通信。 这种体系结构转换有助于 propel Web Api 的发展和开发 ASP.NET Web API 框架。 就 ASP.NET MVC 而言，ASP.NET Web API 的版本提供了另一种机会进一步发展 ASP.NET，作为一个更具模块化的框架。 工程团队利用机会和**生成的 ASP.NET Web API，使其不依赖于 system.web 中的任何一种核心框架类型**。 这两个方面已经实现了：首先，它意味着 ASP.NET Web API 可以完全独立地进行发展（并且它可以继续快速循环，因为它是通过 NuGet 提供的）。 其次，由于不存在对 System.web 的外部依赖关系，因此没有 IIS 的依赖项，ASP.NET Web API 包括在自定义主机（例如，控制台应用程序、Windows 服务等）中运行的功能。

### <a name="the-future-a-nimble-framework"></a>未来：灵活框架

通过将框架组件彼此分离，然后在 NuGet 上发布它们，框架现在可以**更快速地循环访问**。 此外，对于需要**小型轻型主机**作为其服务的开发人员，Web API 的自承载功能的强大功能和灵活性也非常吸引人。 事实上，这是一个很好的方法，实际上，其他框架也需要此功能，而这种新的挑战是，每个框架都在其自己的主机进程中运行，并且需要独立管理（启动、停止等）。 新式 Web 应用程序通常支持静态文件服务、动态页面生成、Web API 以及最近的实时/推送通知。 应该单独运行和管理其中每个服务的情况并不是真实的。

需要的是单一托管抽象，使开发人员能够从各种不同的组件和框架中编写应用程序，然后在支持的主机上运行该应用程序。

## <a name="the-open-web-interface-for-net-owin"></a>.NET 的开放 Web 接口（OWIN）

 通过 Ruby 社区中的[货架](http://rack.github.io/)实现的优点，.net 社区的若干成员设置为在 Web 服务器和框架组件之间创建抽象。 OWIN 抽象的两个设计目标是非常简单，并且可能会在其他框架类型上占用最少的依赖项。 这两个目标有助于确保：

- 可以更轻松地开发和使用新组件。
- 应用程序可以更轻松地在主机和可能的整个平台/操作系统之间移植。

生成的抽象包括两个核心元素。 第一个是环境字典。 此数据结构负责存储处理 HTTP 请求和响应所需的所有状态以及任何相关的服务器状态。 环境字典定义如下：

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

与 OWIN 兼容的 Web 服务器负责使用数据（如 HTTP 请求和响应的正文流和标头集合）填充环境字典。 然后，应用程序或框架组件负责用其他值填充或更新字典，并写入响应正文流。

除了指定环境字典的类型外，OWIN 规范还定义了一系列核心字典键值对。 例如，下表显示了 HTTP 请求所需的字典密钥：

| 键名 | 值说明 |
| --- | --- |
| `"owin.RequestBody"` | 包含请求正文的流（如果有）。 如果没有请求正文，则 Null 可用作占位符。 请参阅[请求正文](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)。 |
| `"owin.RequestHeaders"` | 请求标头的 `IDictionary<string, string[]>`。 请参阅[标头](http://owin.org/html/owin.html#3-3-headers)。 |
| `"owin.RequestMethod"` | 包含请求的 HTTP 请求方法的 `string` （例如，`"GET"`、`"POST"`）。 |
| `"owin.RequestPath"` | 包含请求路径的 `string`。 路径必须相对于应用程序委托的 "根";请参阅[路径](http://owin.org/html/owin.html#5-3-paths)。 |
| `"owin.RequestPathBase"` | 一个 `string`，其中包含与应用程序委托的 "根" 对应的请求路径部分;请参阅[路径](http://owin.org/html/owin.html#5-3-paths)。 |
| `"owin.RequestProtocol"` | 包含协议名称和版本的 `string` （例如 `"HTTP/1.0"` 或 `"HTTP/1.1"`）。 |
| `"owin.RequestQueryString"` | 包含 HTTP 请求 URI 的查询字符串组件的 `string`，没有前导 "？"（例如 `"foo=bar&baz=quux"`）。 该值可以是空字符串。 |
| `"owin.RequestScheme"` | 包含用于请求的 URI 方案的 `string` （例如，`"http"`、`"https"`）;请参阅[URI 方案](http://owin.org/html/owin.html#5-1-uri-scheme)。 |

OWIN 的第二个关键元素是应用程序委托。 这是一个函数签名，用作 OWIN 应用程序中所有组件之间的主接口。 应用程序委托的定义如下所示：

`Func<IDictionary<string, object>, Task>;`

然后，应用程序委托只是 Func 委托类型的实现，其中函数接受环境字典作为输入并返回一个任务。 对于开发人员而言，此设计具有多个含义：

- 编写 OWIN 组件需要的类型依赖项非常少。 这极大地提高了开发人员 OWIN 的可访问性。
- 异步设计使抽象能够通过其处理计算资源来高效，尤其是在更多的 i/o 密集型操作中。
- 由于应用程序委托是执行的原子单元，并且环境字典作为委托的参数来执行，因此，OWIN 组件可以轻松地链接在一起以创建复杂的 HTTP 处理管道。

从实现的角度来看，OWIN 是规范（[http://owin.org/html/owin.html](http://owin.org/html/owin.html)）。 它的目标不是下一 Web 框架，而是有关 Web 框架和 Web 服务器如何交互的规范。

如果已调查[OWIN](http://owin.org/)或[Katana](https://github.com/aspnet/AspNetKatana/wiki)，还可能注意到[OWIN NuGet 包](http://nuget.org/packages/Owin)和 OWIN。 此库包含单个 interface [IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)，它可将整理的启动序列作为 OWIN 规范第[4 节](http://owin.org/html/owin.html#4-application-startup)中所述的启动顺序。 尽管不需要生成 OWIN 服务器，但[IAppBuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)接口提供了一个具体的参考点，并且由 Katana 项目组件使用。

## <a name="project-katana"></a>项目 Katana

尽管[OWIN](http://owin.org/html/owin.html)规范和*OWIN*都是社区拥有的，并且社区运行开源工作，但[Katana](https://github.com/aspnet/AspNetKatana/wiki)项目表示由 Microsoft 构建和发布的一组 OWIN 组件。 这些组件包括基础结构组件（例如主机和服务器）以及功能组件（例如身份验证组件）以及到框架（如[SignalR](../../../signalr/index.md)和[ASP.NET Web API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)）的绑定。 项目具有以下三个高级别目标： 

- **可移植**–当新组件可用时，组件应该能够轻松地替代它们。 这包括从框架到服务器和主机的所有类型的组件。 此目标的含义是，第三方框架可以在 Microsoft 服务器上无缝运行，而 Microsoft framework 可能在第三方服务器和主机上运行。
- **模块化/灵活**–不同于许多框架，其中包括默认情况下打开的多种功能，Katana 项目组件应很小且具有针对性，并使应用程序开发人员能够控制应用程序中要使用的组件。
- **轻型/高性能/可缩放**性-通过将框架的传统概念分解为一组由应用程序开发人员显式添加的小型、集中的组件，生成的 Katana 应用程序可以消耗更少的计算资源，因此可以处理更多的负载，而不是使用其他类型的服务器和框架。 由于应用程序的要求需要底层基础结构中的更多功能，因此可以将这些功能添加到 OWIN 管道，但这应该是应用程序开发人员的一个明确决定。 此外，可代替性的较低级别的组件意味着，当它们可用时，可以无缝引入新的高性能服务器来提高 OWIN 应用程序的性能，而无需中断这些应用程序。

## <a name="getting-started-with-katana-components"></a>入门 Katana 组件

首次引入时， [node.js](http://nodejs.org/)框架的一个方面是立即吸引人们的注意力，这就是一种简单的方法，即可以创作和运行 Web 服务器。 如果 Katana 目标[以 node.js 为形式显示，则](http://nodejs.org/)可以通过指出 Katana 带来了 node.js （及其类似框架[）的许多](http://nodejs.org/)好处，而不会强制开发人员提供有关开发 ASP.NET Web 应用程序的所有内容。 若要使此语句保持为 true，Katana 项目的入门在本质上[与 node.js 一样简单。](http://nodejs.org/)

## <a name="creating-hello-world"></a>正在创建 "Hello World！"

JavaScript 和 .NET 开发的一个明显的区别在于编译器的存在（或不存在）。 因此，简单的 Katana 服务器的起点是 Visual Studio 项目。 但是，我们可以从最小的项目类型开始：空的 ASP.NET Web 应用程序。

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

接下来，我们将在项目中安装[Owin](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) NuGet 包。 此包提供在 ASP.NET 请求管道中运行的 OWIN 服务器。 它可以在[NuGet 库](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)中找到，并且可以使用 Visual Studio 包管理器对话框或程序包管理器控制台通过以下命令进行安装：

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

安装 `Microsoft.Owin.Host.SystemWeb` 包将安装其他一些包作为依赖项。 其中一个依赖项是 `Microsoft.Owin`，这是一个库，提供若干帮助器类型和用于开发 OWIN 应用程序的方法。 我们可以使用这些类型快速编写下面的 "hello world" 服务器。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

此非常简单的 Web 服务器现在可以使用 Visual Studio 的**F5**命令运行，并提供对调试的完全支持。

## <a name="switching-hosts"></a>切换主机

默认情况下，前面的 "hello world" 示例在 ASP.NET 请求管道中运行，后者在 IIS 上下文中使用 System.web。 这种方法本身可能会带来巨大的价值，因为它使我们能够利用 OWIN 管道的灵活性和可组合性以及 IIS 的总体成熟度。 但是，在某些情况下，IIS 提供的权益不是必需的，而需要的则是更小、更轻型的主机。 如果要在 IIS 和 system.web 之外运行简单的 Web 服务器，需要执行哪些操作？

为了说明可移植性目标，从 Web 服务器主机移到命令行主机时，只需将新的服务器和主机依赖项添加到项目的输出文件夹，然后启动主机即可。 在此示例中，我们将在名为 `OwinHost.exe` 的 Katana 主机中托管 Web 服务器，并将使用基于 Katana HttpListener 的服务器。 与其他 Katana 组件类似，这些组件将使用以下命令从 NuGet 获取：

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

然后，可以从命令行导航到项目根文件夹，只需运行 `OwinHost.exe` （安装在其各自 NuGet 包的 tools 文件夹中）。 默认情况下，`OwinHost.exe` 配置为查找基于 HttpListener 的服务器，因此不需要其他配置。 在 Web 浏览器中导航到 `http://localhost:5000/` 显示现在通过控制台运行的应用程序。

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana 体系结构

 Katana 组件体系结构将应用程序划分为四个逻辑层，如下所示：*主机、服务器、中间件*和*应用程序*。 组件体系结构的分解方式是，在许多情况下，可以轻松地替换这些层的实现，而无需重新编译应用程序。   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>Host

 主机负责以下操作：

- 管理基础进程。
- 协调导致选择服务器的工作流，并对将处理请求的 OWIN 管道的构造进行处理。

  目前，对于基于 Katana 的应用程序，有3种主要托管选项：  
  
**Iis/ASP. .net**：使用标准 HttpModule 和 HttpHandler 类型，OWIN 管道可在 IIS 上作为 ASP.NET 请求流的一部分运行。 ASP.NET 托管支持通过将 SystemWeb NuGet 包安装到 Web 应用程序项目中来启用。 此外，由于 IIS 既充当主机又充当服务器，因此在此 NuGet 包中 OWIN 服务器/主机的区别是与父的，这意味着，如果使用 SystemWeb 主机，开发人员不能替换备用服务器实现。  
  
**自定义主机**： Katana 组件套件允许开发人员在自己的自定义进程中托管应用程序，无论该应用程序是控制台应用程序、Windows 服务，等等。此功能类似于 Web API 提供的自承载功能。 下面的示例演示了 Web API 代码的自定义宿主：  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana 应用程序的自主机设置类似于：

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API 和 Katana 自承载示例之间的一个明显区别是，Katana 自托管示例中缺少 Web API 配置代码。 为了同时启用可移植性和可组合性，Katana 将启动服务器的代码与配置请求处理管道的代码分开。 配置 Web API 的代码，则包含在类启动中，这在 WebApplication 中另外指定为类型参数。

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

本文稍后将更详细地讨论 startup 类。 但是，启动 Katana 自宿主进程所需的代码看起来与您今天在 ASP.NET Web API 自宿主应用程序中使用的代码类似。

**Owinhost.exe**：尽管有些需要编写自定义进程来运行 Katana Web 应用程序，但很多情况下，只需启动一个预生成的可执行文件，就可以启动服务器并运行其应用程序。 对于此方案，Katana 组件套件包括 `OwinHost.exe`。 从项目的根目录中运行时，此可执行文件将启动服务器（默认情况下使用 HttpListener 服务器），并使用约定来查找和运行用户的启动类。 若要进行更精细的控制，可执行文件提供了许多其他命令行参数。

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>服务器

 尽管主机负责启动和维护应用程序在其中运行的进程，但服务器的责任是打开网络套接字，倾听请求，然后通过用户指定的 OWIN 组件的管道发送它们（可能已注意到，此管道是在应用程序开发人员的 Startup 类中指定的。 目前，Katana 项目包含两个服务器实现： 

- **Owin**：正如前文所述，IIS 与 ASP.NET 管道共同充当了主机和服务器。 因此，在选择此宿主选项时，IIS 都管理宿主级别的问题，例如进程激活和侦听 HTTP 请求。 对于 ASP.NET Web 应用程序，它会将请求发送到 ASP.NET 管道。 Katana SystemWeb 主机将注册 ASP.NET HttpModule 和 HttpHandler，以便在请求流过 HTTP 管道时截获请求，并通过用户指定的 OWIN 管道发送请求。
- **Owin HttpListener**：作为其名称，此 Katana 服务器使用 .NET Framework 的 HttpListener 类打开套接字，并将请求发送到开发人员指定的 Owin 管道。 这当前是 Katana 自承载 API 和 Owinhost.exe 的默认服务器选择。

## <a name="middlewareframework"></a>中间件/框架

 如前所述，当服务器接受来自客户端的请求时，它负责通过 OWIN 组件（由开发人员的启动代码指定）的管道传递它。 这些管道组件称为中间件。  
 在非常基本的层面上，OWIN 中间件组件只需实现 OWIN 应用程序委托即可调用该委托。

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

但是，为了简化中间件组件的开发和组合，Katana 支持用于中间件组件的少量约定和帮助器类型。 最常见的是 `OwinMiddleware` 类。 使用此类生成的自定义中间件组件如下所示： 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 此类派生自 `OwinMiddleware`，实现一个将管道中的下一个中间件的实例作为其参数之一的构造函数，然后将其传递给基构造函数。 用于配置中间件的其他参数也会在下一个中间件参数之后声明为构造函数参数。   
  
在运行时，中间件通过重写的 `Invoke` 方法执行。 此方法使用 `OwinContext`类型的单个自变量。 此上下文对象由前面所述的 `Microsoft.Owin` NuGet 包提供，并提供对请求、响应和环境字典的强类型访问，以及一些其他的帮助器类型。   
  
可以在应用程序启动代码中轻松地将中间件类添加到 OWIN 管道，如下所示：   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

由于 Katana 基础结构只是构建 OWIN 中间件组件的管道，并且组件只需支持应用程序委托即可参与管道，因此中间件组件的复杂性可能会很大，从简单记录器到整个框架（如 ASP.NET、Web API 或[SignalR](../../../signalr/index.md)）。 例如，将 ASP.NET Web API 添加到以前的 OWIN 管道需要添加以下启动代码：

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana 基础结构将基于在配置方法中将中间件组件添加到 IAppBuilder 对象的顺序生成该组件的管道。 在我们的示例中，LoggerMiddleware 可以处理流过管道的所有请求，而不考虑这些请求的最终处理方式。 这使得中间件组件（例如身份验证组件）能够处理包含多个组件和框架（例如 ASP.NET Web API、SignalR 和静态文件服务器）的管道的请求。
 
## <a name="applications"></a>应用程序

如前面的示例所示，OWIN 和 Katana 项目不应视为新的应用程序编程模型，而是作为一种抽象方式，用于从服务器和托管基础结构分离应用程序编程模型和框架。 例如，在生成 Web API 应用程序时，无论应用程序是否使用 Katana 项目中的组件在 OWIN 管道中运行，开发人员框架都将继续使用 ASP.NET Web API 框架。 对于应用程序开发人员来说，与 OWIN 相关的代码的一个位置就是应用程序的启动代码，开发人员可以在其中撰写 OWIN 管道。 在启动代码中，开发人员将注册一系列 UseXx 语句，通常是每个要处理传入请求的中间件组件。 此体验与在当前系统中注册 HTTP 模块的效果相同。 通常，较大的框架中间件（如 ASP.NET Web API 或[SignalR](../../../signalr/index.md) ）将在管道末尾进行注册。 交叉切削中间件组件（如用于身份验证或缓存的组件）通常注册到管道的开头，以便它们处理在管道中稍后注册的所有框架和组件的请求。 这种不同的中间件组件和基础结构组件之间的分离使组件能够在不同的速度中发展，同时确保整体系统保持稳定。

## <a name="components--nuget-packages"></a>组件-NuGet 包

与许多当前库和框架一样，Katana 项目组件以一组 NuGet 包的形式提供。 在即将推出的版本2.0 中，Katana 包依赖关系图如下所示。 （单击图像查看大图。）

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

几乎 Katana 项目中的每个包都在 Owin 包上直接或间接依赖于。 你可能会记住，这是包含 IAppBuilder 接口的包，它提供了 OWIN 规范的第4节中所述的应用程序启动序列的具体实现。 此外，许多包都依赖于 Owin，后者提供了一组帮助器类型用于处理 HTTP 请求和响应。 包的其余部分可分类为托管基础结构包（服务器或主机）或中间件。 Katana 项目外部的包和依赖项显示为橙色。

Katana 2.0 的托管基础结构包括基于 SystemWeb 和 HttpListener 的服务器、使用 OWIN 运行 OWINHOST.EXE 应用程序的 Owinhost.exe 包以及用于自承载 OWIN 应用程序的 OWIN 包自定义主机（例如，控制台应用程序、Windows 服务等）

对于 Katana 2.0，中间件组件主要侧重于提供不同的身份验证方法。 还提供了一个用于诊断的附加中间件组件，它支持启动和错误页。 随着 OWIN 的不断发展，中间件组件的生态系统和第三方开发的生态系统组件的生态系统也会增长。

## <a name="conclusion"></a>结束语

 从一开始，Katana 项目的目标尚未创建，因此迫使开发人员了解另一个 Web 框架。 相反，目标是创建一个抽象来向 .NET Web 应用程序开发人员提供比以前更多的选择。 通过将典型 Web 应用程序堆栈的逻辑层分解为一组可替换的组件，Katana 项目可在整个堆栈中启用组件，以对这些组件有意义的速度进行改进。 通过构建简单的 OWIN 抽象的所有组件，Katana 使框架和构建在这些框架之上的应用程序可在各种不同的服务器和主机之间移植。 通过使开发人员能够控制堆栈，Katana 可确保开发人员对其 Web 堆栈的轻型或功能的丰富程度做出最佳选择。  

## <a name="for-more-information-about-katana"></a>有关 Katana 的详细信息

- GitHub 上的 Katana 项目： [https://github.com/aspnet/AspNetKatana/](https://github.com/aspnet/AspNetKatana/)。
- 视频： [Katana 项目-OWIN for ASP.NET](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET)，By Howard Dierking。

## <a name="acknowledgements"></a>致谢

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/)：（twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ） rick 是 Microsoft 专注于 Azure 和 MVC 的高级编程编写器。
- [Scott Hanselman](http://www.hanselman.com/blog/)：（twitter [@shanselman](https://twitter.com/shanselman) ）
- [吴建 Galloway](https://weblogs.asp.net/jgalloway/default.aspx)：（twitter [@jongalloway](https://twitter.com/jongalloway) ）
