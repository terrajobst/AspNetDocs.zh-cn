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
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="58a67-103">ASP.NET Web API 2 中的跟踪</span><span class="sxs-lookup"><span data-stu-id="58a67-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="58a67-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="58a67-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="58a67-105">尝试调试基于 web 的应用程序时，不能替代一组良好的跟踪日志。</span><span class="sxs-lookup"><span data-stu-id="58a67-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="58a67-106">本教程演示如何在 ASP.NET Web API 中启用跟踪。</span><span class="sxs-lookup"><span data-stu-id="58a67-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="58a67-107">您可以使用此功能跟踪 Web API 框架在调用控制器之前和之后执行的操作。</span><span class="sxs-lookup"><span data-stu-id="58a67-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="58a67-108">你还可以使用它来跟踪你自己的代码。</span><span class="sxs-lookup"><span data-stu-id="58a67-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="58a67-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="58a67-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="58a67-110">[Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) （也适用于 visual studio 2015）</span><span class="sxs-lookup"><span data-stu-id="58a67-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="58a67-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="58a67-111">Web API 2</span></span>
> - [<span data-ttu-id="58a67-112">WebApi。</span><span class="sxs-lookup"><span data-stu-id="58a67-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="58a67-113">在 Web API 中启用诊断跟踪</span><span class="sxs-lookup"><span data-stu-id="58a67-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="58a67-114">首先，我们将创建一个新的 ASP.NET Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="58a67-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="58a67-115">在 Visual Studio 的 "**文件**" 菜单中，选择 "**新建**" > **项目**"。</span><span class="sxs-lookup"><span data-stu-id="58a67-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="58a67-116">在"模板 **" 下，选择 "** **ASP.NET Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="58a67-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="58a67-117">选择 "Web API 项目" 模板。</span><span class="sxs-lookup"><span data-stu-id="58a67-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="58a67-118">从 "**工具**" 菜单中，依次选择 " **NuGet 包管理器**"、"**包管理控制台**"。</span><span class="sxs-lookup"><span data-stu-id="58a67-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="58a67-119">在 "包管理器控制台" 窗口中，键入以下命令。</span><span class="sxs-lookup"><span data-stu-id="58a67-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="58a67-120">第一个命令安装最新的 Web API 跟踪包。</span><span class="sxs-lookup"><span data-stu-id="58a67-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="58a67-121">它还会更新核心 Web API 包。</span><span class="sxs-lookup"><span data-stu-id="58a67-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="58a67-122">第二个命令将 WebApi 包更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="58a67-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="58a67-123">如果要面向特定版本的 Web API，请在安装跟踪包时使用-Version 标志。</span><span class="sxs-lookup"><span data-stu-id="58a67-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="58a67-124">在应用\_启动文件夹中打开文件 WebApiConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="58a67-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="58a67-125">将以下代码添加到**Register**方法。</span><span class="sxs-lookup"><span data-stu-id="58a67-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="58a67-126">此代码将[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)类添加到 Web API 管道。</span><span class="sxs-lookup"><span data-stu-id="58a67-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="58a67-127">**SystemDiagnosticsTraceWriter** [类将跟踪写入到](https://msdn.microsoft.com/library/system.diagnostics.trace)</span><span class="sxs-lookup"><span data-stu-id="58a67-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="58a67-128">若要查看跟踪，请在调试器中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="58a67-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="58a67-129">在浏览器中，导航到 `/api/values`。</span><span class="sxs-lookup"><span data-stu-id="58a67-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="58a67-130">跟踪语句将写入 Visual Studio 中的 "输出" 窗口。</span><span class="sxs-lookup"><span data-stu-id="58a67-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="58a67-131">（从 "**视图**" 菜单中选择 "**输出**"）。</span><span class="sxs-lookup"><span data-stu-id="58a67-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="58a67-132">由于**SystemDiagnosticsTraceWriter** **将跟踪写入到 system.exception**，因此你可以注册其他跟踪侦听器;例如，将跟踪写入日志文件。</span><span class="sxs-lookup"><span data-stu-id="58a67-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="58a67-133">有关跟踪编写器的详细信息，请参阅 MSDN 上的[跟踪侦听器](https://msdn.microsoft.com/library/4y5y10s7.aspx)主题。</span><span class="sxs-lookup"><span data-stu-id="58a67-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="58a67-134">配置 SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="58a67-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="58a67-135">下面的代码演示如何配置跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="58a67-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="58a67-136">可以控制两个设置：</span><span class="sxs-lookup"><span data-stu-id="58a67-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="58a67-137">IsVerbose：如果为 false，则每个跟踪都包含最少的信息。</span><span class="sxs-lookup"><span data-stu-id="58a67-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="58a67-138">如果为 true，则跟踪包含详细信息。</span><span class="sxs-lookup"><span data-stu-id="58a67-138">If true, traces include more information.</span></span>
- <span data-ttu-id="58a67-139">MinimumLevel：设置最小跟踪级别。</span><span class="sxs-lookup"><span data-stu-id="58a67-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="58a67-140">跟踪级别依次为调试、信息、警告、错误和严重。</span><span class="sxs-lookup"><span data-stu-id="58a67-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="58a67-141">向 Web API 应用程序添加跟踪</span><span class="sxs-lookup"><span data-stu-id="58a67-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="58a67-142">添加跟踪编写器后，你可以立即访问由 Web API 管道创建的跟踪。</span><span class="sxs-lookup"><span data-stu-id="58a67-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="58a67-143">你还可以使用跟踪编写器来跟踪你自己的代码：</span><span class="sxs-lookup"><span data-stu-id="58a67-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="58a67-144">若要获取跟踪编写器，请调用**HttpConfiguration. GetTraceWriter**。</span><span class="sxs-lookup"><span data-stu-id="58a67-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="58a67-145">通过控制器，可以通过**ApiController**属性访问此方法。</span><span class="sxs-lookup"><span data-stu-id="58a67-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="58a67-146">若要编写跟踪，可以直接调用**ITraceWriter**方法，但[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)类定义一些更友好的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="58a67-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="58a67-147">例如，上面所示的**Info**方法会创建包含跟踪级别**信息**的跟踪。</span><span class="sxs-lookup"><span data-stu-id="58a67-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="58a67-148">Web API 跟踪基础结构</span><span class="sxs-lookup"><span data-stu-id="58a67-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="58a67-149">本部分介绍如何为 Web API 编写自定义跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="58a67-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="58a67-150">WebApi 包构建在 Web API 中更通用的跟踪基础结构之上。</span><span class="sxs-lookup"><span data-stu-id="58a67-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="58a67-151">你还可以不使用 WebApi，而是插入一些其他跟踪/日志记录库，例如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。</span><span class="sxs-lookup"><span data-stu-id="58a67-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="58a67-152">若要收集跟踪，请实现**ITraceWriter**接口。</span><span class="sxs-lookup"><span data-stu-id="58a67-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="58a67-153">下面是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="58a67-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="58a67-154">**ITraceWriter**方法创建跟踪。</span><span class="sxs-lookup"><span data-stu-id="58a67-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="58a67-155">调用方指定类别和跟踪级别。</span><span class="sxs-lookup"><span data-stu-id="58a67-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="58a67-156">类别可以是任何用户定义的字符串。</span><span class="sxs-lookup"><span data-stu-id="58a67-156">The category can be any user-defined string.</span></span> <span data-ttu-id="58a67-157">**跟踪**的实现应执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="58a67-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="58a67-158">创建新的**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="58a67-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="58a67-159">用请求、类别和跟踪级别对其进行初始化，如下所示。</span><span class="sxs-lookup"><span data-stu-id="58a67-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="58a67-160">这些值由调用方提供。</span><span class="sxs-lookup"><span data-stu-id="58a67-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="58a67-161">调用*traceAction*委托。</span><span class="sxs-lookup"><span data-stu-id="58a67-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="58a67-162">在此委托内部，调用方应填写**TraceRecord**的其余部分。</span><span class="sxs-lookup"><span data-stu-id="58a67-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="58a67-163">使用你喜欢的任何日志记录技术编写**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="58a67-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="58a67-164">此处所示的示例只调用了</span><span class="sxs-lookup"><span data-stu-id="58a67-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="58a67-165">设置跟踪编写器</span><span class="sxs-lookup"><span data-stu-id="58a67-165">Setting the Trace Writer</span></span>

<span data-ttu-id="58a67-166">若要启用跟踪，必须将 Web API 配置为使用**ITraceWriter**实现。</span><span class="sxs-lookup"><span data-stu-id="58a67-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="58a67-167">可以通过**HttpConfiguration**对象执行此操作，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="58a67-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="58a67-168">只有一个跟踪编写器可以处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="58a67-168">Only one trace writer can be active.</span></span> <span data-ttu-id="58a67-169">默认情况下，Web API 将不执行任何操作的 &quot;无操作&quot; 追踪器设置。</span><span class="sxs-lookup"><span data-stu-id="58a67-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="58a67-170">（&quot;的无操作&quot; 跟踪器存在，因此在编写跟踪之前，跟踪代码不必检查跟踪编写器是否为**null** 。）</span><span class="sxs-lookup"><span data-stu-id="58a67-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="58a67-171">Web API 跟踪的工作原理</span><span class="sxs-lookup"><span data-stu-id="58a67-171">How Web API Tracing Works</span></span>

<span data-ttu-id="58a67-172">Web API 中的跟踪使用*外观*模式：启用跟踪后，web api 使用执行跟踪调用的类包装请求管道的各个部分。</span><span class="sxs-lookup"><span data-stu-id="58a67-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="58a67-173">例如，选择控制器时，管道使用**IHttpControllerSelector**接口。</span><span class="sxs-lookup"><span data-stu-id="58a67-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="58a67-174">启用跟踪后，管道会插入实现**IHttpControllerSelector**的类，但会调用实际实现：</span><span class="sxs-lookup"><span data-stu-id="58a67-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API 跟踪使用外观模式。](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="58a67-176">此设计的优点包括：</span><span class="sxs-lookup"><span data-stu-id="58a67-176">The benefits of this design include:</span></span>

- <span data-ttu-id="58a67-177">如果未添加跟踪编写器，则不会实例化跟踪组件，并且不会影响性能。</span><span class="sxs-lookup"><span data-stu-id="58a67-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="58a67-178">如果将默认服务（如**IHttpControllerSelector** ）替换为自己的自定义实现，则跟踪不会受到影响，因为跟踪是由包装对象完成的。</span><span class="sxs-lookup"><span data-stu-id="58a67-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="58a67-179">您还可以通过替换默认的**ITraceManager**服务将整个 Web API 跟踪框架替换为您自己的自定义框架：</span><span class="sxs-lookup"><span data-stu-id="58a67-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="58a67-180">实现**ITraceManager**以初始化跟踪系统。</span><span class="sxs-lookup"><span data-stu-id="58a67-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="58a67-181">请注意，这会替换*整个*跟踪框架，包括 Web API 中内置的所有跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="58a67-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
