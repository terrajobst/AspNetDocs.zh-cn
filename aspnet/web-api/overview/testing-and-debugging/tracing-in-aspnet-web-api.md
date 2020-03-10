---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2 中的跟踪 |Microsoft Docs
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中启用跟踪。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484340"
---
# <a name="tracing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的跟踪

作者： [Mike Wasson](https://github.com/MikeWasson)

> 尝试调试基于 web 的应用程序时，不能替代一组良好的跟踪日志。 本教程演示如何在 ASP.NET Web API 中启用跟踪。 您可以使用此功能跟踪 Web API 框架在调用控制器之前和之后执行的操作。 你还可以使用它来跟踪你自己的代码。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - [Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) （也适用于 visual studio 2015）
> - Web API 2
> - [WebApi。](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>在 Web API 中启用诊断跟踪

首先，我们将创建一个新的 ASP.NET Web 应用程序项目。 在 Visual Studio 的 "**文件**" 菜单中，选择 "**新建**" > **项目**"。 在"模板 **" 下，选择 "** **ASP.NET Web 应用程序**"。

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

选择 "Web API 项目" 模板。

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

从 "**工具**" 菜单中，依次选择 " **NuGet 包管理器**"、"**包管理控制台**"。

在 "包管理器控制台" 窗口中，键入以下命令。

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

第一个命令安装最新的 Web API 跟踪包。 它还会更新核心 Web API 包。 第二个命令将 WebApi 包更新到最新版本。

> [!NOTE]
> 如果要面向特定版本的 Web API，请在安装跟踪包时使用-Version 标志。

在应用\_启动文件夹中打开文件 WebApiConfig.cs。 将以下代码添加到**Register**方法。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

此代码将[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)类添加到 Web API 管道。 **SystemDiagnosticsTraceWriter** [类将跟踪写入到](https://msdn.microsoft.com/library/system.diagnostics.trace)

若要查看跟踪，请在调试器中运行应用程序。 在浏览器中，导航到 `/api/values`。

![](tracing-in-aspnet-web-api/_static/image5.png)

跟踪语句将写入 Visual Studio 中的 "输出" 窗口。 （从 "**视图**" 菜单中选择 "**输出**"）。

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

由于**SystemDiagnosticsTraceWriter** **将跟踪写入到 system.exception**，因此你可以注册其他跟踪侦听器;例如，将跟踪写入日志文件。 有关跟踪编写器的详细信息，请参阅 MSDN 上的[跟踪侦听器](https://msdn.microsoft.com/library/4y5y10s7.aspx)主题。

### <a name="configuring-systemdiagnosticstracewriter"></a>配置 SystemDiagnosticsTraceWriter

下面的代码演示如何配置跟踪编写器。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

可以控制两个设置：

- IsVerbose：如果为 false，则每个跟踪都包含最少的信息。 如果为 true，则跟踪包含详细信息。
- MinimumLevel：设置最小跟踪级别。 跟踪级别依次为调试、信息、警告、错误和严重。

## <a name="adding-traces-to-your-web-api-application"></a>向 Web API 应用程序添加跟踪

添加跟踪编写器后，你可以立即访问由 Web API 管道创建的跟踪。 你还可以使用跟踪编写器来跟踪你自己的代码：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

若要获取跟踪编写器，请调用**HttpConfiguration. GetTraceWriter**。 通过控制器，可以通过**ApiController**属性访问此方法。

若要编写跟踪，可以直接调用**ITraceWriter**方法，但[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)类定义一些更友好的扩展方法。 例如，上面所示的**Info**方法会创建包含跟踪级别**信息**的跟踪。

## <a name="web-api-tracing-infrastructure"></a>Web API 跟踪基础结构

本部分介绍如何为 Web API 编写自定义跟踪编写器。

WebApi 包构建在 Web API 中更通用的跟踪基础结构之上。 你还可以不使用 WebApi，而是插入一些其他跟踪/日志记录库，例如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。

若要收集跟踪，请实现**ITraceWriter**接口。 下面是一个简单的示例：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**ITraceWriter**方法创建跟踪。 调用方指定类别和跟踪级别。 类别可以是任何用户定义的字符串。 **跟踪**的实现应执行以下操作：

1. 创建新的**TraceRecord**。 用请求、类别和跟踪级别对其进行初始化，如下所示。 这些值由调用方提供。
2. 调用*traceAction*委托。 在此委托内部，调用方应填写**TraceRecord**的其余部分。
3. 使用你喜欢的任何日志记录技术编写**TraceRecord**。 此处所示的示例只调用了

## <a name="setting-the-trace-writer"></a>设置跟踪编写器

若要启用跟踪，必须将 Web API 配置为使用**ITraceWriter**实现。 可以通过**HttpConfiguration**对象执行此操作，如以下代码所示：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

只有一个跟踪编写器可以处于活动状态。 默认情况下，Web API 将不执行任何操作的 &quot;无操作&quot; 追踪器设置。 （&quot;的无操作&quot; 跟踪器存在，因此在编写跟踪之前，跟踪代码不必检查跟踪编写器是否为**null** 。）

## <a name="how-web-api-tracing-works"></a>Web API 跟踪的工作原理

Web API 中的跟踪使用*外观*模式：启用跟踪后，web api 使用执行跟踪调用的类包装请求管道的各个部分。

例如，选择控制器时，管道使用**IHttpControllerSelector**接口。 启用跟踪后，管道会插入实现**IHttpControllerSelector**的类，但会调用实际实现：

![Web API 跟踪使用外观模式。](tracing-in-aspnet-web-api/_static/image8.png)

此设计的优点包括：

- 如果未添加跟踪编写器，则不会实例化跟踪组件，并且不会影响性能。
- 如果将默认服务（如**IHttpControllerSelector** ）替换为自己的自定义实现，则跟踪不会受到影响，因为跟踪是由包装对象完成的。

您还可以通过替换默认的**ITraceManager**服务将整个 Web API 跟踪框架替换为您自己的自定义框架：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

实现**ITraceManager**以初始化跟踪系统。 请注意，这会替换*整个*跟踪框架，包括 Web API 中内置的所有跟踪代码。
