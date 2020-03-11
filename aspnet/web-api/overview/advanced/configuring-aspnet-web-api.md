---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: 配置 ASP.NET Web API 2 ASP.NET
author: MikeWasson
description: 为 ASP.NET 4.x 配置 ASP.NET Web API 2：配置设置、ASP.NET 1.x 托管、OWIN 自托管、全局服务和预控制器配置。
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449342"
---
# <a name="configuring-aspnet-web-api-2"></a>配置 ASP.NET Web API 2

作者： [Mike Wasson](https://github.com/MikeWasson)

本主题介绍如何配置 ASP.NET Web API。

- [配置设置](#settings)
- [配置包含 ASP.NET 托管的 Web API](#webhost)
- [配置包含 OWIN 自承载的 Web API](#selfhost)
- [全局 Web API 服务](#services)
- [每控制器配置](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>配置设置

Web API 配置设置是在[HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)类中定义的。

| 成员 | 说明 |
| --- | --- |
| **DependencyResolver** | 启用控制器的依赖关系注入。 请参阅[使用 WEB API 依赖关系解析程序](dependency-injection.md)。 |
| **过滤器** | 操作筛选器。 |
| **程序** | [媒体类型格式化程序](../formats-and-model-binding/media-formatters.md)。 |
| **IncludeErrorDetailPolicy** | 指定服务器是否应在 HTTP 响应消息中包含错误详细信息，例如异常消息和堆栈跟踪。 请参阅[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))。 |
| **初始值设定项** | 一个函数，该函数执行**HttpConfiguration**的最终初始化。 |
| **MessageHandlers** | [HTTP 消息处理程序](http-message-handlers.md)。 |
| **ParameterBindingRules** | 用于绑定控制器操作上的参数的规则的集合。 |
| **属性** | 泛型属性包。 |
| **路由** | 路由的集合。 请参阅[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。 |
| **服务** | 服务的集合。 请参阅[服务](#services)。 |

## <a name="prerequisites"></a>系统必备

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional 或 Enterprise 版本。

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>配置包含 ASP.NET 托管的 Web API

在 ASP.NET 应用程序中，通过在**应用程序\_Start**方法中调用[GLOBALCONFIGURATION](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx)配置 Web API。 **Configure**方法使用一个委托，该委托具有一个类型为**HttpConfiguration**的参数。 在委托内执行所有配置。

下面是一个使用匿名委托的示例：

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

在 Visual Studio 2017 中，如果在 "**新建 ASP.NET 项目**" 对话框中选择 "Web API"，则 "ASP.NET Web 应用程序" 项目模板会自动设置配置代码。

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

项目模板在应用\_启动文件夹内创建名为 "WebApiConfig.cs" 的文件。 此代码文件定义委托，你应在其中放置你的 Web API 配置代码。

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

项目模板还将从应用程序中调用委托的代码添加 **\_Start**。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>配置包含 OWIN 自承载的 Web API

如果你是使用 OWIN 自承载的，则创建一个新的**HttpConfiguration**实例。 对此实例执行任何配置，然后将该实例传递给**Owin. UseWebApi**扩展方法。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

教程[使用 OWIN 到自承载 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)显示完整步骤。

<a id="services"></a>
## <a name="global-web-api-services"></a>全局 Web API 服务

**HttpConfiguration**集合包含一组全局服务，Web API 使用这些服务来执行各种任务，如控制器选择和内容协商。

> [!NOTE]
> **服务**集合不是用于服务发现或依赖关系注入的通用机制。 它仅存储 Web API 框架已知的服务类型。

**服务**集合使用一组默认服务进行初始化，你可以提供自己的自定义实现。 某些服务支持多个实例，而其他服务只能有一个实例。 （但是，还可以在控制器级别提供服务，请参阅[按控制器配置](#percontrollerconfig)。

单实例服务

| 服务 | 说明 |
| --- | --- |
| **IActionValueBinder** | 获取参数的绑定。 |
| **IApiExplorer** | 获取应用程序公开的 Api 的说明。 请参阅[创建 WEB API 的帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。 |
| **IAssembliesResolver** | 获取应用程序的程序集的列表。 请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IBodyModelValidator** | 验证媒体类型格式化程序从请求正文读取的模型。 |
| **IContentNegotiator** | 执行内容协商。 |
| **IDocumentationProvider** | 提供 Api 的文档。 默认值为 **null**。 请参阅[创建 WEB API 的帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。 |
| **IHostBufferPolicySelector** | 指示宿主是否应缓冲 HTTP 消息实体正文。 |
| **IHttpActionInvoker** | 调用控制器操作。 请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpActionSelector** | 选择控制器操作。 请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpControllerActivator** | 激活控制器。 请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpControllerSelector** | 选择控制器。 请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **IHttpControllerTypeResolver** | 提供应用程序中的 Web API 控制器类型的列表。 请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。 |
| **ITraceManager** | 初始化跟踪框架。 请参阅[ASP.NET Web API 中的跟踪](../testing-and-debugging/tracing-in-aspnet-web-api.md)。 |
| **ITraceWriter** | 提供跟踪编写器。 默认值为 "无操作" 跟踪编写器。 请参阅[ASP.NET Web API 中的跟踪](../testing-and-debugging/tracing-in-aspnet-web-api.md)。 |
| **IModelValidatorCache** | 提供模型验证程序的缓存。 |

多实例服务

|                 服务                 |                                                                                                              说明                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           返回控制器操作的筛选器列表。                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                返回给定类型的模型联编程序。                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     提供模型的元数据。                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   为模型提供验证程序。                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | 创建值提供程序。 有关详细信息，请参阅 Mike 停止项博客文章[如何在 WebAPI 中创建自定义值提供程序](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) |

若要将自定义实现添加到多实例服务，请调用**服务**集合上的**add**或**Insert** ：

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

若要将单实例服务替换为自定义实现，请调用**服务**集合上的**replace** ：

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>每控制器配置

您可以基于每个控制器重写以下设置：

- 媒体类型格式化程序
- 参数绑定规则
- 服务

为此，请定义一个实现**IControllerConfiguration**接口的自定义特性。 然后将属性应用到控制器。

下面的示例使用自定义格式化程序替换默认的媒体类型格式化程序。

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

**IControllerConfiguration**方法采用两个参数：

- **HttpControllerSettings**对象
- **HttpControllerDescriptor**对象

**HttpControllerDescriptor**包含控制器的说明，你可以检查该说明以提供信息，以便区分两个控制器。

使用**HttpControllerSettings**对象配置控制器。 此对象包含可以基于每个控制器重写的配置参数的子集。 默认情况下，不会更改为全局**HttpConfiguration**对象的任何设置。
