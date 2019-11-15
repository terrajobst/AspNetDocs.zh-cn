---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: 在 ASP.NET MVC 4 中使用异步方法 |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你使用 Visual Studio Express 2012 for Web 构建异步 ASP.NET MVC Web 应用程序的基础知识，这是一款免费版 。
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 5df6a9c136b1934b3afd731eb0ceac1e0faa483e
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115078"
---
# <a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>在 ASP.NET MVC 4 中使用异步方法

作者： [Rick Anderson]((https://twitter.com/RickAndMSFT))

> 本教程将介绍使用[Visual Studio Express 2012 For Web](https://www.microsoft.com/visualstudio/11)构建异步 ASP.NET MVC Web 应用程序的基础知识，这是 Microsoft Visual Studio 的免费版本。 你还可以使用[Visual Studio 2012](https://www.microsoft.com/visualstudio/11)。
> 
> 本教程在 github 上提供了完整的示例[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)

结合使用[.net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx)的 ASP.NET MVC 4[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx)类，您可以编写返回 Task 类型为[Task&lt;ActionResult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx)的对象的异步操作方法。 .NET Framework 4 引入了一个称为[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)的异步编程概念，ASP.NET MVC 4 支持[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)。 任务由[tasks 命名空间中的](https://msdn.microsoft.com/library/system.threading.tasks.aspx)**任务**类型和相关类型来表示。 .NET Framework 4.5 使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字构建这一异步支持，这些关键字使得处理[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)对象比以前的异步方法更复杂。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字是语法简写，指示代码段应以异步方式等待某个代码的其他部分。 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字表示一个提示，可用于将方法标记为基于任务的异步方法。 **Await**、 **async**和**Task**对象的组合使你可以更轻松地在 .net 4.5 中编写异步代码。 异步方法的新模型称为*基于任务的异步模式*（**点击**）。 本教程假定你熟悉使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字以及[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)命名空间的异步编程。

有关使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字以及[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)命名空间的详细信息，请参阅以下参考。

- [白皮书： .NET 中的异步](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await 常见问题](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 异步编程](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>线程池如何处理请求

在 web 服务器上，.NET Framework 维护用于处理 ASP.NET 请求的线程池。 请求到达时，会调度池中的线程来处理该请求。 如果以同步方式处理请求，则处理请求的线程将在处理请求时处于繁忙状态，并且该线程无法处理其他请求。   
  
这可能不是问题，因为线程池的大小足以容纳多个繁忙线程。 但是，线程池中的线程数受到限制（.NET 4.5 的默认最大值是5000）。 在具有长时间运行的请求的高并发性的大型应用程序中，所有可用线程可能都处于繁忙状态。 这种情况称为线程不足。 达到此条件时，web 服务器会将请求排队。 如果请求队列已满，则 web 服务器将拒绝 HTTP 503 状态（服务器太忙）的请求。 CLR 线程池在新线程注入上具有限制。 如果并发为突发（也就是说，您的网站可以突然获得大量请求），并且所有可用的请求线程都忙于处理，因为具有高延迟的后端调用，所以，受限制的线程注入率会使应用程序的响应速度非常差。 此外，添加到线程池的每个新线程都具有开销（如 1 MB 的堆栈内存）。 使用同步方法对高延迟调用进行服务的 web 应用程序，其中线程池增长到 .NET 4.5 默认值最多5，000个线程使用的内存大约为 5 GB异步方法和仅50线程。 执行异步工作时，不一定要使用线程。 例如，当你发出异步 web 服务请求时，ASP.NET 将不会在**异步**方法调用与**await**之间使用任何线程。 使用线程池来处理具有较高延迟的请求可能会导致内存占用量较大，并且服务器硬件利用率不佳。

## <a name="processing-asynchronous-requests"></a>处理异步请求

在启动时看到大量并发请求的 web 应用中，或具有突发负载（其中并发增长突然增加）时，使 web 服务调用异步会提高应用程序的响应能力。 异步请求的处理时间与同步请求所需的时间相同。 如果请求发出需要两秒钟时间才能完成的 web 服务调用，则该请求将需要两秒钟，无论是同步执行还是异步执行。 但是，在异步调用期间，线程在等待第一个请求完成时不会被阻止响应其他请求。 因此，当有多个并发请求调用长时间运行的操作时，异步请求会阻止请求队列和线程池的增长。

## <a id="ChoosingSyncVasync"></a>选择同步操作方法或异步操作方法

本部分列出了使用同步或异步操作方法的相关准则。 这些只是指导原则;分别检查每个应用程序，以确定异步方法是否有助于提高性能。

通常，在下列情况下使用同步方法：

- 操作简单或短时间运行。
- 简易性比效率更重要。
- 操作主要是 CPU 操作，而不是涉及大量磁盘或网络开销的操作。 对 CPU 绑定的操作使用异步操作方法不会带来任何好处，并会导致更大的开销。

通常，在下列情况下使用异步方法：

- 正在调用可通过异步方法使用的服务，并且使用的是 .NET 4.5 或更高版本。
- 操作是网络绑定的，而不是由 CPU 绑定的。
- 并行性比代码简单性更重要。
- 需要提供一种机制，使用户能够取消长时间运行的请求。
- 切换线程的优点超出了上下文切换的成本。 通常，如果同步方法在 ASP.NET 请求线程上等待，而不执行任何操作，则应使方法异步。 通过将调用设为异步，ASP.NET 请求线程在等待 web 服务请求完成时，不会停止工作。
- 测试表明阻塞操作是站点性能瓶颈，而 IIS 可以通过对这些阻止调用使用异步方法来提供更多请求。

可下载的示例演示如何有效地使用异步操作方法。 提供的示例旨在通过 .NET 4.5 在 ASP.NET MVC 4 中提供异步编程的简单演示。 该示例不应作为 ASP.NET MVC 中异步编程的参考体系结构。 该示例程序调用[ASP.NET Web API](../../../web-api/index.md)方法，这些方法进而调用[任务。延迟](https://msdn.microsoft.com/library/hh139096(VS.110).aspx)以模拟长时间运行的 Web 服务调用。 大多数生产应用程序将不会显示使用异步操作方法的明显优势。   
  
一些应用程序要求所有操作方法都是异步的。 通常，将一些同步操作方法转换为异步方法可为所需的工作量提高效率。

## <a id="SampleApp"></a>示例应用程序

你可以从[GitHub](https://github.com/)站点上的[https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET)下载示例应用程序。 存储库由三个项目组成：

- *Mvc4Async*： ASP.NET MVC 4 项目，其中包含本教程中使用的代码。 它使 Web API 调用**WebAPIpgw**服务。
- *WebAPIpgw*：实现 `Products, Gizmos and Widgets` 控制器的 ASP.NET MVC 4 Web API 项目。 它为*WebAppAsync*项目和*Mvc4Async*项目提供数据。
- *WebAppAsync*：在其他教程中使用的 ASP.NET Web 窗体项目。

## <a id="GizmosSynch"></a>Gizmos 同步操作方法

 下面的代码演示了用于显示 gizmos 列表的 `Gizmos` 同步操作方法。 （对于本文，别出心裁是虚构的机械设备。） 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

下面的代码演示别出心裁服务的 `GetGizmos` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos` 方法将 URI 传递到 ASP.NET Web API HTTP 服务，该服务返回 gizmos 数据列表。 *WebAPIpgw*项目包含 `gizmos, widget` 和 `product` 控制器的 Web API 实现。  
下图显示了示例项目中的 gizmos 视图。

![Gizmos](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>创建异步 Gizmos 操作方法

该示例使用新的[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)和[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字（在 .Net 4.5 和 Visual Studio 2012 中提供），让编译器负责维护异步编程所需的复杂转换。 编译器使你可以使用C#的同步控制流构造编写代码，并且编译器会自动应用使用回调所需的转换，以避免阻塞线程。

下面的代码演示 `Gizmos` 同步方法和 `GizmosAsync` 异步方法。 如果你的浏览器支持[HTML 5 `<mark>` 元素](http://www.w3.org/wiki/HTML/Elements/mark)，你会在 `GizmosAsync` 中看到黄色突出显示的更改。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 应用了以下更改，以允许 `GizmosAsync` 是异步的。

- 方法标记有[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字，该关键字告诉编译器为部分主体生成回调并自动创建返回的 `Task<ActionResult>`。
- &quot;Async&quot; 追加到方法名称。 不需要追加 "Async"，但这是编写异步方法时的约定。
- 返回类型已从 `ActionResult` 更改为 `Task<ActionResult>`。 `Task<ActionResult>` 的返回类型表示正在进行的工作，并为方法的调用方提供一个句柄，用于等待异步操作完成。 在这种情况下，调用方为 web 服务。 `Task<ActionResult>` 表示 `ActionResult.` 的结果中的正在进行的工作
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字已应用于 web 服务调用。
- 调用了异步 web 服务 API （`GetGizmosAsync`）。

在 `GetGizmosAsync` 方法体内部，调用了另一个异步方法 `GetGizmosAsync`。 `GetGizmosAsync` 立即返回一个将在数据可用时最终完成的 `Task<List<Gizmo>>`。 因为在有别出心裁数据之前不需要执行任何其他操作，因此代码会等待任务（使用**await**关键字）。 只能在使用**async**关键字批注的方法中使用**await**关键字。

**等待**关键字不会阻止线程，直到任务完成。 它将方法的其余部分注册为任务的回调，并立即返回。 当等待的任务最终完成时，它将调用该回调，并因此在其中断时继续执行方法。 有关使用[await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)和[Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字以及[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)命名空间的详细信息，请参阅[async 引用](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)。

下面的代码演示 `GetGizmos` 和 `GetGizmosAsync` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 异步更改与上述**GizmosAsync**的更改类似。 

- 方法签名通过[async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字进行批注，返回类型已更改为 `Task<List<Gizmo>>`，而*async*追加到方法名称。
- 使用异步[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)类而不是[WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx)类。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字已应用于[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)异步方法。

下图显示了异步别出心裁视图。

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

Gizmos 数据的浏览器表示形式与同步调用创建的视图相同。 唯一的区别是，在负载较重的情况下，异步版本的性能可能更高。

## <a id="Parallel"></a>并行执行多个操作

当操作必须执行多个独立的操作时，异步操作方法与同步方法相比具有明显的优势。 在提供的示例中，同步方法 `PWG`（适用于产品、小组件和 Gizmos）显示三个 web 服务调用的结果，以获取产品、小组件和 Gizmos 的列表。 提供这些服务的[ASP.NET Web API](../../../web-api/index.md)项目使用[任务延迟](https://msdn.microsoft.com/library/hh139096(VS.110).aspx)来模拟延迟或慢速网络调用。 当延迟设置为500毫秒时，异步 `PWGasync` 方法将需要一小段500以上的时间才能完成，同时同步 `PWG` 版本需要超过1500毫秒。 下面的代码演示了同步 `PWG` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

下面的代码演示了异步 `PWGasync` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

下图显示了从**PWGasync**方法返回的视图。

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>使用取消标记

返回 `Task<ActionResult>`的异步操作方法可取消，即当使用[AsyncTimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx)特性提供一个参数时，它们将采用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)参数。 下面的代码演示 `GizmosCancelAsync` 方法，超时为150毫秒。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

下面的代码演示 GetGizmosAsync 重载，它采用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)参数。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

在提供的示例应用程序中，选择 "*取消标记" 演示*链接将调用 `GizmosCancelAsync` 方法，并演示异步调用的取消。

## <a id="ServerConfig"></a>高并发/高延迟 Web 服务调用的服务器配置

若要实现异步 web 应用程序的优势，可能需要对默认服务器配置进行一些更改。 配置和压力测试异步 web 应用程序时，请记住以下几点。

- Windows 7、Windows Vista 和所有 Windows 客户端操作系统最多可以有10个并发请求。 你将需要 Windows Server 操作系统，以查看高负载下的异步方法的优点。
- 在提升的命令提示符下向 IIS 注册 .NET 4.5：  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regiis-i  
  请参阅[ASP.NET IIS 注册工具（Aspnet\_regiis）](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- 可能需要将[HTTP .sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) queue 限制从默认值1000提高到5000。 如果设置过低，可能会看到[http： .sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture)拒绝请求，并显示 http 503 状态。 更改 http.sys 队列限制：

    - 打开 IIS 管理器并导航到 "应用程序池" 窗格。
    - 右键单击目标应用程序池，然后选择 "**高级设置**"。  
        ![高级](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - 在 "**高级设置**" 对话框中，将*队列长度*从1000更改为5000。  
        ![队列长度](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  请注意，在上面的图像中，.NET framework 作为 "v 4.0" 列出，即使应用程序池使用的是 .NET 4.5 也是如此。 要了解这种差异，请参阅以下内容：

    - [.NET 版本控制和多目标 .NET 4.5 是 .NET 4.0 的就地升级](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [如何将 IIS 应用程序或 AppPool 设置为使用 ASP.NET 3.5，而不是2。0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework 版本和依赖关系](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- 如果你的应用程序使用 web 服务或 System.NET 通过 HTTP 与后端通信，则你可能需要增加[connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx)元素。 对于 ASP.NET 应用程序，这被自动配置功能限制为 Cpu 数量的12倍。 这意味着，在四处理器上，最多可以有12个 \* 4 = 48 并发连接到 IP 终结点。 由于此方法已绑定到自动[配置](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)，因此在 ASP.NET 应用程序中增加 `maxconnection` 的最简单方法是在*global.asax*文件的 from `Application_Start` 方法中以编程方式设置[ServicePointManager servicepointmanager.defaultconnectionlimit。](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) 有关示例，请参阅示例下载。
- 在 .NET 4.5 中， [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)的默认值为5000。
