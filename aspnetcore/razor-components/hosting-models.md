---
title: 承载模型的 razor 组件
author: guardrex
description: 了解客户端 Blazor 和服务器端 ASP.NET Core Razor 组件承载模型。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042434"
---
# <a name="razor-components-hosting-models"></a><span data-ttu-id="4b283-103">承载模型的 razor 组件</span><span class="sxs-lookup"><span data-stu-id="4b283-103">Razor Components hosting models</span></span>

<span data-ttu-id="4b283-104">通过[Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="4b283-104">By [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="4b283-105">Razor 组件是一个 web 框架，用于运行客户端上基于 WebAssembly 的.NET 运行时在浏览器中 (*Blazor*) 或 ASP.NET Core 中的服务器端 (*ASP.NET Core Razor 组件*)。</span><span class="sxs-lookup"><span data-stu-id="4b283-105">Razor Components is a web framework designed to run client-side in the browser on a WebAssembly-based .NET runtime (*Blazor*) or server-side in ASP.NET Core (*ASP.NET Core Razor Components*).</span></span> <span data-ttu-id="4b283-106">无论托管模型、 应用和组件模型*保持不变*。</span><span class="sxs-lookup"><span data-stu-id="4b283-106">Regardless of the hosting model, the app and component models *remain the same*.</span></span> <span data-ttu-id="4b283-107">本文介绍了可用的托管模型。</span><span class="sxs-lookup"><span data-stu-id="4b283-107">This article discusses the available hosting models.</span></span>

## <a name="client-side-hosting-model"></a><span data-ttu-id="4b283-108">客户端托管模型</span><span class="sxs-lookup"><span data-stu-id="4b283-108">Client-side hosting model</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="4b283-109">Blazor 的主体托管模型是在浏览器中的正在运行客户端。</span><span class="sxs-lookup"><span data-stu-id="4b283-109">The principal hosting model for Blazor is running client-side in the browser.</span></span> <span data-ttu-id="4b283-110">在此模型中，Blazor 应用、 其依赖项和.NET 运行时被下载到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="4b283-110">In this model, the Blazor app, its dependencies, and the .NET runtime are downloaded to the browser.</span></span> <span data-ttu-id="4b283-111">应用将在浏览器线程中直接执行。</span><span class="sxs-lookup"><span data-stu-id="4b283-111">The app is executed directly on the browser UI thread.</span></span> <span data-ttu-id="4b283-112">所有 UI 更新和事件处理都发生在同一进程内。</span><span class="sxs-lookup"><span data-stu-id="4b283-112">All UI updates and event handling happens within the same process.</span></span> <span data-ttu-id="4b283-113">可以使用任何 web 服务器首选的静态文件作为部署的应用程序资产 (请参阅[主机并将其部署](xref:host-and-deploy/razor-components/index))。</span><span class="sxs-lookup"><span data-stu-id="4b283-113">The app assets can be deployed as static files using whatever web server is preferred (see [Host and deploy](xref:host-and-deploy/razor-components/index)).</span></span>

![Blazor 客户端：在浏览器在 UI 线程上运行 Blazor 应用。](hosting-models/_static/client-side.png)

<span data-ttu-id="4b283-115">若要创建一个 Blazor 应用使用客户端的托管模型，请使用**Blazor**或 **（ASP.NET Core 托管） 的 Blazor**项目模板 (`blazor`或`blazorhosted`模板时使用[dotnet 新](/dotnet/core/tools/dotnet-new)命令在命令提示符下)。</span><span class="sxs-lookup"><span data-stu-id="4b283-115">To create a Blazor app using the client-side hosting model, use the **Blazor** or **Blazor (ASP.NET Core Hosted)** project templates (`blazor` or `blazorhosted` template when using the [dotnet new](/dotnet/core/tools/dotnet-new) command at a command prompt).</span></span> <span data-ttu-id="4b283-116">附带*blazor.webassembly.js*脚本句柄：</span><span class="sxs-lookup"><span data-stu-id="4b283-116">The included *blazor.webassembly.js* script handles:</span></span>

* <span data-ttu-id="4b283-117">下载.NET 运行时、 应用和其依赖项。</span><span class="sxs-lookup"><span data-stu-id="4b283-117">Downloading the .NET runtime, the app, and its dependencies.</span></span>
* <span data-ttu-id="4b283-118">若要运行该应用程序的运行时初始化。</span><span class="sxs-lookup"><span data-stu-id="4b283-118">Initialization of the runtime to run the app.</span></span>

<span data-ttu-id="4b283-119">客户端的托管模型提供了以下几个好处。</span><span class="sxs-lookup"><span data-stu-id="4b283-119">The client-side hosting model offers several benefits.</span></span> <span data-ttu-id="4b283-120">客户端 Blazor:</span><span class="sxs-lookup"><span data-stu-id="4b283-120">Client-side Blazor:</span></span>

* <span data-ttu-id="4b283-121">不具有任何.NET 服务器端依赖项。</span><span class="sxs-lookup"><span data-stu-id="4b283-121">Has no .NET server-side dependency.</span></span>
* <span data-ttu-id="4b283-122">具有丰富的交互式 UI。</span><span class="sxs-lookup"><span data-stu-id="4b283-122">Has a rich interactive UI.</span></span>
* <span data-ttu-id="4b283-123">充分利用客户端资源和功能。</span><span class="sxs-lookup"><span data-stu-id="4b283-123">Fully leverages client resources and capabilities.</span></span>
* <span data-ttu-id="4b283-124">卸载可从服务器到客户端。</span><span class="sxs-lookup"><span data-stu-id="4b283-124">Offloads work from the server to the client.</span></span>
* <span data-ttu-id="4b283-125">支持脱机方案。</span><span class="sxs-lookup"><span data-stu-id="4b283-125">Supports offline scenarios.</span></span>

<span data-ttu-id="4b283-126">有客户端托管的弊端。</span><span class="sxs-lookup"><span data-stu-id="4b283-126">There are downsides to client-side hosting.</span></span> <span data-ttu-id="4b283-127">客户端 Blazor:</span><span class="sxs-lookup"><span data-stu-id="4b283-127">Client-side Blazor:</span></span>

* <span data-ttu-id="4b283-128">将应用程序限制为浏览器的功能。</span><span class="sxs-lookup"><span data-stu-id="4b283-128">Restricts the app to the capabilities of the browser.</span></span>
* <span data-ttu-id="4b283-129">需要支持客户端硬件和软件 （例如，WebAssembly 支持）。</span><span class="sxs-lookup"><span data-stu-id="4b283-129">Requires capable client hardware and software (for example, WebAssembly support).</span></span>
* <span data-ttu-id="4b283-130">具有更大的下载大小和加载时间较长的应用。</span><span class="sxs-lookup"><span data-stu-id="4b283-130">Has a larger download size and longer app load time.</span></span>
* <span data-ttu-id="4b283-131">具有小于成熟的.NET 运行时和工具支持 （例如，.NET 标准支持和调试的限制）。</span><span class="sxs-lookup"><span data-stu-id="4b283-131">Has less mature .NET runtime and tooling support (for example, limitations in .NET Standard support and debugging).</span></span>

<span data-ttu-id="4b283-132">Visual Studio 提供了**Blazor (托管 ASP.NET Core)** 用于创建运行上 WebAssembly 和 ASP.NET Core 服务器上承载的 Blazor 应用项目模板。</span><span class="sxs-lookup"><span data-stu-id="4b283-132">Visual Studio includes the **Blazor (ASP.NET Core hosted)** project template for creating a Blazor app that runs on WebAssembly and is hosted on an ASP.NET Core server.</span></span> <span data-ttu-id="4b283-133">ASP.NET Core 应用 Blazor 应用提供给客户端，但在其他方面的单独进程。</span><span class="sxs-lookup"><span data-stu-id="4b283-133">The ASP.NET Core app serves the Blazor app to clients but is otherwise a separate process.</span></span> <span data-ttu-id="4b283-134">客户端 Blazor 应用程序可以在网络上使用 Web API 调用或 SignalR 连接与服务器交互。</span><span class="sxs-lookup"><span data-stu-id="4b283-134">The client-side Blazor app can interact with the server over the network using Web API calls or SignalR connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b283-135">如果客户端 Blazor 应用程序托管为 IIS 子应用的 ASP.NET Core 应用程序提供服务，禁用继承的 ASP.NET Core 模块处理程序。</span><span class="sxs-lookup"><span data-stu-id="4b283-135">If a client-side Blazor app is served by an ASP.NET Core app hosted as an IIS sub-app, disable the inherited ASP.NET Core Module handler.</span></span> <span data-ttu-id="4b283-136">Blazor 应用中设置应用基路径*index.html*到 IIS 别名在 IIS 中配置子应用程序时使用的文件。</span><span class="sxs-lookup"><span data-stu-id="4b283-136">Set the app base path in the Blazor app's *index.html* file to the IIS alias used when configuring the sub-app in IIS.</span></span>
>
> <span data-ttu-id="4b283-137">有关详细信息，请参阅[应用程序基路径](xref:host-and-deploy/razor-components/index#app-base-path)。</span><span class="sxs-lookup"><span data-stu-id="4b283-137">For more information, see [App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="server-side-hosting-model"></a><span data-ttu-id="4b283-138">服务器端托管模型</span><span class="sxs-lookup"><span data-stu-id="4b283-138">Server-side hosting model</span></span>

<span data-ttu-id="4b283-139">在 ASP.NET Core Razor 组件服务器端宿主模型中，在服务器上从 ASP.NET Core 应用中执行应用程序。</span><span class="sxs-lookup"><span data-stu-id="4b283-139">In the ASP.NET Core Razor Components server-side hosting model, the app is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="4b283-140">通过 SignalR 连接处理 UI 更新、事件处理和 JavaScript 调用。</span><span class="sxs-lookup"><span data-stu-id="4b283-140">UI updates, event handling, and JavaScript calls are handled over a SignalR connection.</span></span>

![ASP.NET Core Razor 组件服务器端：在浏览器与交互 （托管在 ASP.NET Core 应用内） 的应用的服务器上通过 SignalR 连接。](hosting-models/_static/server-side.png)

<span data-ttu-id="4b283-142">若要创建使用服务器端的托管模型的 Razor 组件应用程序，请使用**Blazor （服务器端 ASP.NET Core 中）** 模板 (`blazorserver`使用时[dotnet 新](/dotnet/core/tools/dotnet-new)在命令提示符下)。</span><span class="sxs-lookup"><span data-stu-id="4b283-142">To create a Razor Components app using the server-side hosting model, use the **Blazor (Server-side in ASP.NET Core)** template (`blazorserver` when using [dotnet new](/dotnet/core/tools/dotnet-new) at a command prompt).</span></span> <span data-ttu-id="4b283-143">ASP.NET Core 应用托管 Razor 组件服务器端应用程序，并设置 SignalR 终结点，客户端连接。</span><span class="sxs-lookup"><span data-stu-id="4b283-143">An ASP.NET Core app hosts the Razor Components server-side app and sets up the SignalR endpoint where clients connect.</span></span> <span data-ttu-id="4b283-144">ASP.NET Core 应用引用应用程序的`Startup`要添加类：</span><span class="sxs-lookup"><span data-stu-id="4b283-144">The ASP.NET Core app references the app's `Startup` class to add:</span></span>

* <span data-ttu-id="4b283-145">服务器端 Razor 组件服务。</span><span class="sxs-lookup"><span data-stu-id="4b283-145">Server-side Razor Components services.</span></span>
* <span data-ttu-id="4b283-146">在应用请求处理管道中。</span><span class="sxs-lookup"><span data-stu-id="4b283-146">The app to the request handling pipeline.</span></span>

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

<span data-ttu-id="4b283-147">*Blazor.server.js*脚本&dagger;建立客户端连接。</span><span class="sxs-lookup"><span data-stu-id="4b283-147">The *blazor.server.js* script&dagger; establishes the client connection.</span></span> <span data-ttu-id="4b283-148">它是应用程序负责保持和还原应用程序状态，根据需要 （例如，发生时丢失的网络连接）。</span><span class="sxs-lookup"><span data-stu-id="4b283-148">It's the app's responsibility to persist and restore app state as required (for example, in the event of a lost network connection).</span></span>

<span data-ttu-id="4b283-149">服务器端的托管模型提供了以下几个好处：</span><span class="sxs-lookup"><span data-stu-id="4b283-149">The server-side hosting model offers several benefits:</span></span>

* <span data-ttu-id="4b283-150">可以编写使用.NET 对整个应用程序和C#使用组件模型。</span><span class="sxs-lookup"><span data-stu-id="4b283-150">Allows you to write your entire app with .NET and C# using the component model.</span></span>
* <span data-ttu-id="4b283-151">提供丰富的交互式风格，并避免不必要的页面刷新。</span><span class="sxs-lookup"><span data-stu-id="4b283-151">Provides a rich interactive feel and avoids unnecessary page refreshes.</span></span>
* <span data-ttu-id="4b283-152">具有显著变小的应用程序大小比客户端 Blazor 应用程序并加载速度快得多。</span><span class="sxs-lookup"><span data-stu-id="4b283-152">Has a significantly smaller app size than a client-side Blazor app and loads much faster.</span></span>
* <span data-ttu-id="4b283-153">组件逻辑可以充分利用的服务器功能，其中包括使用任何.NET Core 兼容的 Api。</span><span class="sxs-lookup"><span data-stu-id="4b283-153">Component logic can take full advantage of server capabilities, including using any .NET Core compatible APIs.</span></span>
* <span data-ttu-id="4b283-154">.NET Core 上运行的服务器上，因此现有的.NET 工具，如调试，按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="4b283-154">Runs on .NET Core on the server, so existing .NET tooling, such as debugging, works as expected.</span></span>
* <span data-ttu-id="4b283-155">适用于瘦客户端 （例如，浏览器不支持 WebAssembly 和资源约束设备）。</span><span class="sxs-lookup"><span data-stu-id="4b283-155">Works with thin clients (for example, browsers that don't support WebAssembly and resource constrained devices).</span></span>

<span data-ttu-id="4b283-156">有服务器端托管的弊端：</span><span class="sxs-lookup"><span data-stu-id="4b283-156">There are downsides to server-side hosting:</span></span>

* <span data-ttu-id="4b283-157">具有较高的延迟：每个用户交互涉及到的网络跃点。</span><span class="sxs-lookup"><span data-stu-id="4b283-157">Has higher latency: Every user interaction involves a network hop.</span></span>
* <span data-ttu-id="4b283-158">提供没有脱机支持：如果客户端连接失败，应用将停止工作。</span><span class="sxs-lookup"><span data-stu-id="4b283-158">Offers no offline support: If the client connection fails, the app stops working.</span></span>
* <span data-ttu-id="4b283-159">可伸缩性减少了：服务器必须管理多个客户端连接，并处理客户端状态。</span><span class="sxs-lookup"><span data-stu-id="4b283-159">Has reduced scalability: The server must manage multiple client connections and handle client state.</span></span>
* <span data-ttu-id="4b283-160">要求提供应用的 ASP.NET Core 服务器。</span><span class="sxs-lookup"><span data-stu-id="4b283-160">Requires an ASP.NET Core server to serve the app.</span></span> <span data-ttu-id="4b283-161">不使用 （例如，从 CDN) 的服务器的部署不能。</span><span class="sxs-lookup"><span data-stu-id="4b283-161">Deployment without a server (for example, from a CDN) isn't possible.</span></span>

<span data-ttu-id="4b283-162">&dagger;*Blazor.server.js*脚本发布到以下路径： *bin / {调试 |版本} / {目标框架} /publish/ {应用程序名称}。应用/dist/框架 （_f)*。</span><span class="sxs-lookup"><span data-stu-id="4b283-162">&dagger;The *blazor.server.js* script is published to the following path: *bin/{Debug|Release}/{TARGET FRAMEWORK}/publish/{APPLICATION NAME}.App/dist/_framework*.</span></span>
