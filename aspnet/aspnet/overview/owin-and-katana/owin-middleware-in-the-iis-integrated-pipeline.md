---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: IIS 集成管道中的 OWIN 中间件 |Microsoft Docs
author: Praburaj
description: 本文介绍如何在 IIS 集成管道中运行 OWIN 中间件组件（OMCs），以及如何设置 OMC 运行的管道事件。 你应 。
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500258"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS 集成管道中的 OWIN 中间件

作者： [Praburaj Thiagarajan](https://github.com/Praburaj)， [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本文介绍如何在 IIS 集成管道中运行 OWIN 中间件组件（OMCs），以及如何设置 OMC 运行的管道事件。 阅读本教程之前，应查看项目 Katana 和[OWIN Startup 类检测](owin-startup-class-detection.md)[的概述](an-overview-of-project-katana.md)。 本教程由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）、丽丽 Ross、Praburaj Thiagarajan 和 Howard Dierking （ [@howard\_Dierking](https://twitter.com/howard_dierking) ）撰写。

尽管[OWIN](an-overview-of-project-katana.md)中间件组件（OMCs）主要设计为在服务器不可知的管道中运行，但也可以在 IIS 集成管道中运行 OMC （ ***不*支持经典模式**）。 通过从包管理器控制台安装以下包（PMC），可以在 IIS 集成管道中使用 OMC：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

这意味着所有应用程序框架（甚至还不能在 IIS 和 system.web 之外运行的框架）都可以从现有的 OWIN 中间件组件受益。 

> [!NOTE]
> Visual Studio 2013 中的新标识系统附带的所有 `Microsoft.Owin.Security.*` 包（例如： Cookie、Microsoft 帐户、Google、Facebook、Twitter、[持有者令牌](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html)、OAuth、授权服务器、JWT、Azure Active Directory 和 Active directory 联合身份验证服务）都是 OMCs，可用于自承载和 IIS 托管方案。

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>OWIN 中间件在 IIS 集成管道中的执行方式

对于 OWIN 控制台应用程序，使用[启动配置](owin-startup-class-detection.md)构建的应用程序管道由使用 `IAppBuilder.Use` 方法添加组件的顺序设置。 也就是说， [Katana](an-overview-of-project-katana.md)运行时中的 OWIN 管道将按照 `IAppBuilder.Use`的注册顺序处理 OMCs。 在 IIS 集成管道中，请求管道由已订阅预定义管道事件集的[HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) （如[BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)、 [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)、 [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)等）组成。

如果比较 OMC 与 ASP.NET 世界[HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx)的比较，则必须将 OMC 注册到正确的预定义管道事件。 例如，当请求进入管道中的[AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)阶段时，将会调用 HttpModule `MyModule`：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

为了使 OMC 参与此相同的基于事件的执行排序， [Katana](an-overview-of-project-katana.md)运行时代码将扫描[启动配置](owin-startup-class-detection.md)，并将每个中间件组件订阅到集成管道事件。 例如，以下 OMC 和注册代码使你可以查看中间件组件的默认事件注册。 （有关创建 OWIN startup 类的更多详细说明，请参阅[OWIN Startup Class 检测](owin-startup-class-detection.md)。）

1. 创建一个空的 web 应用程序项目，并将其命名为**owin2**。
2. 从包管理器控制台（PMC）运行以下命令： 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. 添加 `OWIN Startup Class`，并将其命名为 `Startup`。 将生成的代码替换为以下代码（更改已突出显示）：  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. 按 F5 运行应用。

启动配置设置具有三个中间件组件的管道，前两个组件显示诊断信息，最后一个事件响应事件（同时显示诊断信息）。 `PrintCurrentIntegratedPipelineStage` 方法显示在其上调用该中间件的集成管道事件和消息。 "输出" 窗口显示以下内容：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

默认情况下，Katana 运行时将每个 OWIN 中间件组件映射到[PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) ，这对应于 IIS 管道事件[PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)。

## <a name="stage-markers"></a>阶段标记

使用 `IAppBuilder UseStageMarker()` 扩展方法，可以将 OMCs 标记为在管道的特定阶段执行。 若要在特定阶段运行一组中间件组件，请在注册过程中将最后一个组件设置为之后立即插入一个阶段标记。 可以在管道的哪个阶段执行中间件，以及必须运行的顺序组件（在本教程的后面部分将介绍这些规则）。 将 `UseStageMarker` 方法添加到 `Configuration` 代码，如下所示：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` 调用将配置之前注册的所有中间件组件（在本例中为两个诊断组件），以便在管道的身份验证阶段运行。 最后一个中间件组件（显示诊断和响应请求）将在 `ResolveCache` 阶段（ [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx)事件）上运行。

按 F5 运行应用。"输出" 窗口显示以下内容：

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>阶段标记规则

Owin 中间件组件（OMC）可以配置为在以下 OWIN 管道阶段事件下运行：

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. 默认情况下，OMCs 在最后一个事件（`PreHandlerExecute`）上运行。 这就是我们的第一个示例代码显示为 "PreExecuteRequestHandler" 的原因。
2. 您可以使用 `app.UseStageMarker` 方法来注册一个 OMC，以便在 `PipelineStage` 枚举中列出的 OWIN 管道的任意阶段运行。
3. OWIN 管道和 IIS 管道已排序，因此对 `app.UseStageMarker` 的调用必须按顺序排列。 不能将事件处理程序设置为在向注册的最后一个事件之前 `app.UseStageMarker`的事件。 例如，*在调用后*：

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   不会传递对 `app.UseStageMarker` 传递 `Authenticate` 或 `PostAuthenticate` 的调用，且不会引发异常。 OMCs 在最新阶段运行，默认情况下 `PreHandlerExecute`。 阶段标记用于使它们在前面运行。 如果按顺序指定阶段标记，我们将舍入到前面的标记。 换言之，添加一个阶段标记显示 "不晚于舞台 X 运行"。 OMC 在 OWIN 管道中添加之后的最早阶段标记处运行。
4. 调用 `app.UseStageMarker` 入选的最早阶段。 例如，如果从前面的示例中切换 `app.UseStageMarker` 调用的顺序：

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   "输出" 窗口将显示： 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   OMCs 在 `AuthenticateRequest` 阶段中运行，因为最后一个 OMC 注册了 `Authenticate` 事件，`Authenticate` 事件在所有其他事件之前。
