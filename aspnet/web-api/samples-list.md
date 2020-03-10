---
uid: web-api/samples-list
title: Web API 示例列表-ASP.NET 4。x
author: rick-anderson
description: ASP.NET 4.x ASP.NET Web API 示例列表
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484262"
---
# <a name="web-api-samples-list"></a>Web API 示例列表

## <a name="httpclient-samples"></a>HttpClient 示例

**必应翻译示例** | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

演示如何使用**HttpClient**类调用[Microsoft Translator 服务](https://msdn.microsoft.com/library/ff512419.aspx)。 Microsoft Translator 服务 API 需要一个 OAuth 令牌，应用程序通过将请求发送到 Azure 令牌服务器来获取对转换器服务的每个请求的请求。 令牌服务器的结果将送入发送到转换服务的请求。 运行此示例之前，必须[从 Azure Marketplace 获取应用程序密钥](https://msdn.microsoft.com/library/hh454950.aspx)，并填写 AccessTokenMessageHandler 示例类中的信息。

**Google Maps 示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

使用**HttpClient**从[Google Maps API](https://developers.google.com/maps/)下载 Redmond、WA 的地图，将其另存为本地文件，然后打开默认图像查看器。

**Twitter 客户端示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

演示如何使用**HttpClient**编写简单的 Twitter 客户端。 该示例使用**HttpMessageHandler**将 OAuth 身份验证信息插入到传出的**HttpRequestMessage**中。 使用 JSON.NET 读取 Twitter 的结果。 运行此示例之前，必须[从 Twitter 获取应用程序密钥](https://dev.twitter.com/)，并填写 OAuthMessageHandler 示例类中的信息。

**全球银行样品** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [vs 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [vs 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

演示如何使用 JSON.NET 分析结果，从而检索全球银行数据站点中的数据。

## <a name="web-api-samples"></a>Web API 示例

**与 ASP.NET Web API** | [VS 2012 源](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)的入门

演示如何创建支持 HTTP GET 请求的基本 web API。 包含[第一个 ASP.NET Web API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程的源代码。

**ASP.NET Web API JavaScript 方案–**  | [VS 2012 源](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)的注释

演示如何使用 ASP.NET Web API 生成支持浏览器客户端的 Web Api，并可使用 jQuery 轻松地调用。

**联系人经理** | [VS 2010 源](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

此示例使用 ASP.NET Web API 生成一个简单的联系人管理器应用程序。 应用程序由 ASP.NET MVC 应用程序使用的联系人管理器 web API 和 Windows Phone 的应用程序组成，用于显示和管理联系人列表。

**批处理示例** | [详细说明](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

演示如何在 ASP.NET 中实现 HTTP 批处理。 批处理包含将多个 HTTP 请求放入单个 MIME 多部分实体正文，然后以 HTTP POST 的形式发送到服务器。 分别处理请求，并将响应放入另一个 MIME 多部分实体正文，并返回到客户端。

**内容控制器示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [vs 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [vs 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

演示如何使用流异步读取和写入请求和响应实体。 示例控制器有两个操作：一个 PUT 操作，它以异步方式读取请求实体正文并将其存储在本地文件中，并将返回操作返回到本地文件。

**自定义程序集冲突解决程序示例** | [VS 2012 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

演示如何修改 ASP.NET Web API 以支持动态加载的库程序集中的控制器的发现。 该示例实现一个自定义**IAssembliesResolver** ，它调用默认实现，然后将库程序集添加到默认结果中。

**自定义媒体类型格式化程序示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

演示如何使用**BufferedMediaTypeFormatter**基类创建自定义媒体类型格式化程序。 此基类适用于主要使用同步读写操作的格式化程序。 除了显示媒体类型格式化程序，该示例还演示了如何将它作为应用程序的**HttpConfiguration**的一部分进行注册。 请注意，对于主要使用异步读取和写入操作的格式化程序，也可以直接使用**MediaTypeFormatter**基类。

**自定义参数绑定示例** | [详细说明](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 源](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

说明如何自定义参数绑定过程，该过程确定如何将请求中的信息绑定到操作参数。 在此示例中，主控制器具有四项操作：

1. BindPrincipal 演示如何从自定义泛型主体绑定 IPrincipal 参数，而不是从 HTTP GET 消息绑定;
2. BindCustomComplexTypeFromUriOrBody 演示如何绑定复杂类型参数，该参数可能来自消息正文或来自 HTTP POST 消息的请求 URI;
3. BindCustomComplexTypeFromUriWithRenamedProperty 演示如何将复杂类型参数与来自 HTTP POST 消息的请求 URI 的已重命名属性绑定;
4. PostMultipleParametersFromBody 演示如何绑定 POST 消息的正文中的多个参数;

**文件上传示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

演示如何使用 MIME 多部分文件上传将文件上传到**ApiController** ，以及如何使用**ProgressNotificationHandler**通过**HttpClient**设置进度通知。 控制器将异步读取 HTML 文件的内容，并将一个或多个正文部分写入到本地文件。 响应包含有关上传的文件（或文件）的信息。

**文件上传到 Azure Blob 存储示例** | [详细说明](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

此示例类似于文件上传示例，但它不是将上传的文件保存在本地磁盘上，而是使用[Windows AZURE SDK for .net](https://www.windowsazure.com/develop/net/)将文件异步上传到[Azure Blob 存储](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 它还提供了一种机制，用于列出[Azure Blob 存储容器](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)中当前存在的 blob。 可以试用 Azure SDK 随附的**Azure 存储模拟器**运行的示例。 如果你有[Azure 存储帐户](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)，也可以针对真实存储服务运行。

**Http 消息处理程序管道示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

演示如何在客户端（**HttpClient**）和服务器（ASP.NET Web API）上连接**HttpMessageHandler**实例。 在此示例中，在客户端和服务器上使用相同的处理程序。 尽管完全相同的处理程序在这两个位置中都是相同的，但在客户端和服务器端，对象模型是相同的。

**JSON 上传示例** | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

演示如何在**ApiController**上传和下载 JSON。 该示例使用最小的**ApiController**并使用**HttpClient**访问它。

**混合示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

演示如何从**ApiController**操作中异步访问多个远程站点。 每次命中此操作时，请求都是异步执行的，因此不会阻止任何线程。

**内存跟踪示例** | [详细说明](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

此示例项目创建一个 Nuget 包，该程序包将自定义内存中跟踪编写器安装到 ASP.NET Web API 应用程序中。

**MongoDB 示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

演示如何使用 MongoDB 作为**ApiController**的持久存储，并使用存储库模式。

**响应正文处理器示例** | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

演示如何在将响应实体传输到客户端之前将其复制到本地文件，并以异步方式对该文件执行其他处理。 该示例实现了一个**HttpMessageHandler** ，该方法包装响应实体，该实体将自身以普通和本地文件的形式写入输出。

 | [VS 2012 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)**上传 XDocument 示例** | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx)

演示如何使用**PushStreamContent**和**HttpClient**将 XDocument 上载到**ApiController** 。

**验证示例** | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

说明如何在 ASP.NET WebAPI 中的模型上使用验证属性来验证 HTTP 请求的内容。 演示如何根据需要标记属性，如何使用框架定义的验证属性和自定义验证特性来批注模型，以及如何为无效的模型状态返回错误响应。

 | [详细说明](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 源](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)的**Web 窗体示例**

显示添加到 Web 窗体项目的 ApiController。

**[RestBugs 示例](https://github.com/howarddierking/RestBugs)**

RestBugs 是一个简单的 bug 跟踪应用程序，演示如何使用 ASP.NET Web API 和新的 HTTP 客户端库来创建超媒体驱动系统。 该示例包含使用 ASP.NET Web API 的客户端和服务器实现。 服务器使用自定义 Razor 格式化程序生成资源表示形式。 该示例还提供了一个 node.js 服务器，用于说明使用超媒体设计来分离客户端和服务器的好处。
