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
# <a name="razor-components-hosting-models"></a>承载模型的 razor 组件

通过[Daniel Roth](https://github.com/danroth27)

Razor 组件是一个 web 框架，用于运行客户端上基于 WebAssembly 的.NET 运行时在浏览器中 (*Blazor*) 或 ASP.NET Core 中的服务器端 (*ASP.NET Core Razor 组件*)。 无论托管模型、 应用和组件模型*保持不变*。 本文介绍了可用的托管模型。

## <a name="client-side-hosting-model"></a>客户端托管模型

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Blazor 的主体托管模型是在浏览器中的正在运行客户端。 在此模型中，Blazor 应用、 其依赖项和.NET 运行时被下载到浏览器中。 应用将在浏览器线程中直接执行。 所有 UI 更新和事件处理都发生在同一进程内。 可以使用任何 web 服务器首选的静态文件作为部署的应用程序资产 (请参阅[主机并将其部署](xref:host-and-deploy/razor-components/index))。

![Blazor 客户端：在浏览器在 UI 线程上运行 Blazor 应用。](hosting-models/_static/client-side.png)

若要创建一个 Blazor 应用使用客户端的托管模型，请使用**Blazor**或 **（ASP.NET Core 托管） 的 Blazor**项目模板 (`blazor`或`blazorhosted`模板时使用[dotnet 新](/dotnet/core/tools/dotnet-new)命令在命令提示符下)。 附带*blazor.webassembly.js*脚本句柄：

* 下载.NET 运行时、 应用和其依赖项。
* 若要运行该应用程序的运行时初始化。

客户端的托管模型提供了以下几个好处。 客户端 Blazor:

* 不具有任何.NET 服务器端依赖项。
* 具有丰富的交互式 UI。
* 充分利用客户端资源和功能。
* 卸载可从服务器到客户端。
* 支持脱机方案。

有客户端托管的弊端。 客户端 Blazor:

* 将应用程序限制为浏览器的功能。
* 需要支持客户端硬件和软件 （例如，WebAssembly 支持）。
* 具有更大的下载大小和加载时间较长的应用。
* 具有小于成熟的.NET 运行时和工具支持 （例如，.NET 标准支持和调试的限制）。

Visual Studio 提供了**Blazor (托管 ASP.NET Core)** 用于创建运行上 WebAssembly 和 ASP.NET Core 服务器上承载的 Blazor 应用项目模板。 ASP.NET Core 应用 Blazor 应用提供给客户端，但在其他方面的单独进程。 客户端 Blazor 应用程序可以在网络上使用 Web API 调用或 SignalR 连接与服务器交互。

> [!IMPORTANT]
> 如果客户端 Blazor 应用程序托管为 IIS 子应用的 ASP.NET Core 应用程序提供服务，禁用继承的 ASP.NET Core 模块处理程序。 Blazor 应用中设置应用基路径*index.html*到 IIS 别名在 IIS 中配置子应用程序时使用的文件。
>
> 有关详细信息，请参阅[应用程序基路径](xref:host-and-deploy/razor-components/index#app-base-path)。

## <a name="server-side-hosting-model"></a>服务器端托管模型

在 ASP.NET Core Razor 组件服务器端宿主模型中，在服务器上从 ASP.NET Core 应用中执行应用程序。 通过 SignalR 连接处理 UI 更新、事件处理和 JavaScript 调用。

![ASP.NET Core Razor 组件服务器端：在浏览器与交互 （托管在 ASP.NET Core 应用内） 的应用的服务器上通过 SignalR 连接。](hosting-models/_static/server-side.png)

若要创建使用服务器端的托管模型的 Razor 组件应用程序，请使用**Blazor （服务器端 ASP.NET Core 中）** 模板 (`blazorserver`使用时[dotnet 新](/dotnet/core/tools/dotnet-new)在命令提示符下)。 ASP.NET Core 应用托管 Razor 组件服务器端应用程序，并设置 SignalR 终结点，客户端连接。 ASP.NET Core 应用引用应用程序的`Startup`要添加类：

* 服务器端 Razor 组件服务。
* 在应用请求处理管道中。

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

*Blazor.server.js*脚本&dagger;建立客户端连接。 它是应用程序负责保持和还原应用程序状态，根据需要 （例如，发生时丢失的网络连接）。

服务器端的托管模型提供了以下几个好处：

* 可以编写使用.NET 对整个应用程序和C#使用组件模型。
* 提供丰富的交互式风格，并避免不必要的页面刷新。
* 具有显著变小的应用程序大小比客户端 Blazor 应用程序并加载速度快得多。
* 组件逻辑可以充分利用的服务器功能，其中包括使用任何.NET Core 兼容的 Api。
* .NET Core 上运行的服务器上，因此现有的.NET 工具，如调试，按预期方式工作。
* 适用于瘦客户端 （例如，浏览器不支持 WebAssembly 和资源约束设备）。

有服务器端托管的弊端：

* 具有较高的延迟：每个用户交互涉及到的网络跃点。
* 提供没有脱机支持：如果客户端连接失败，应用将停止工作。
* 可伸缩性减少了：服务器必须管理多个客户端连接，并处理客户端状态。
* 要求提供应用的 ASP.NET Core 服务器。 不使用 （例如，从 CDN) 的服务器的部署不能。

&dagger;*Blazor.server.js*脚本发布到以下路径： *bin / {调试 |版本} / {目标框架} /publish/ {应用程序名称}。应用/dist/框架 （_f)*。
