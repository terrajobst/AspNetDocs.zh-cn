---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: 在 ASP.NET Web API 2 中启用跨域请求 |Microsoft Docs
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中支持跨域资源共享（CORS）。
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447614"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>在 ASP.NET Web API 2 中启用跨域请求

作者： [Mike Wasson](https://github.com/MikeWasson)

> 浏览器安全策略阻止 Web 页向另一个域发出 AJAX 请求。 此限制称为*相同源策略*，可防止恶意站点读取另一个站点中的敏感数据。 但是，有时你可能希望让其他站点调用你的 web API。
>
> [跨源资源共享](http://www.w3.org/TR/cors/)（CORS）是一种 W3C 标准，允许服务器放松相同的源策略。 使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。 CORS 比早期技术（如[JSONP](http://en.wikipedia.org/wiki/JSONP)）更安全且更灵活。 本教程演示如何在 Web API 应用程序中启用 CORS。
>
> ## <a name="software-used-in-the-tutorial"></a>本教程中使用的软件
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2。2

## <a name="introduction"></a>简介

本教程演示 ASP.NET Web API 中的 CORS 支持。 首先，我们将创建两个 ASP.NET 项目-一个名为 "WebService"，它托管一个 Web API 控制器，另一个称为 "WebClient"，后者调用 WebService。 由于这两个应用程序托管在不同的域中，因此从 WebClient 到 WebService 的 AJAX 请求是一个跨源请求。

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>什么是 "相同来源"？

如果两个 Url 具有相同的方案、主机和端口，则它们具有相同的源。 （[RFC 6454](http://tools.ietf.org/html/rfc6454)）

这两个 Url 具有相同的源：

- `http://example.com/foo.html`
- `http://example.com/bar.html`

这些 Url 的来源不同于前两个 Url：

- `http://example.net`-不同域
- `http://example.com:9000/foo.html`-不同端口
- `https://example.com/foo.html`-不同方案
- `http://www.example.com/foo.html`-不同子域

> [!NOTE]
> 比较来源时，Internet Explorer 不会考虑该端口。

## <a name="create-the-webservice-project"></a>创建 WebService 项目

> [!NOTE]
> 本部分假设你已了解如何创建 Web API 项目。 否则，请参阅[ASP.NET Web API 入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。

1. 启动 Visual Studio 并创建一个新的**ASP.NET Web 应用程序（.NET Framework）** 项目。
2. 在 "**新建 ASP.NET Web 应用程序**" 对话框中，选择 "**空**项目" 模板。 在 "**添加文件夹和核心引用**" 下，选择 " **Web API** " 复选框。

   ![Visual Studio 中的新 ASP.NET 项目对话框](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. 使用以下代码添加名为 `TestController` 的 Web API 控制器：

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. 可以在本地运行应用程序或将其部署到 Azure。 （对于本教程中的屏幕截图，应用程序部署到 Azure App Service Web Apps。）若要验证 web API 是否正常工作，请导航到 `http://hostname/api/test/`，其中*hostname*是部署应用程序的域。 应会看到响应文本，&quot;获取：测试消息&quot;。

   ![显示测试消息的 Web 浏览器](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>创建 WebClient 项目

1. 创建另一个 " **ASP.NET Web 应用程序（.NET Framework）** " 项目，然后选择 " **MVC**项目" 模板。 （可选）选择 "**更改身份验证** > **无身份验证**"。 对于本教程，不需要进行身份验证。

   ![Visual Studio 中 "新建 ASP.NET 项目" 对话框中的 MVC 模板](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. 在**解决方案资源管理器**中，打开文件*视图/Home/索引。* 将此文件中的代码替换为以下代码：

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   对于*serviceUrl*变量，请使用 web 应用程序的 URI。

3. 在本地运行 WebClient 应用程序或将其发布到其他网站。

单击 "试用" 按钮时，将使用下拉框中列出的 HTTP 方法（GET、POST 或 PUT）将 AJAX 请求提交到 WebService 应用。 这使你可以检查不同的跨域请求。 目前，WebService 应用不支持 CORS，因此，如果单击该按钮，则会出现错误。

![浏览器中的 "尝试" 错误](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> 如果在类似于[Fiddler](https://www.telerik.com/fiddler)的工具中观看 HTTP 流量，你会发现浏览器确实发送了 GET 请求，而请求成功，但是 AJAX 调用返回错误。 请务必了解，同源策略不会阻止浏览器*发送*请求。 相反，它会阻止应用程序查看*响应*。

![显示 web 请求的 Fiddler web 调试器](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>启用 CORS

现在，让我们在 WebService 应用中启用 CORS。 首先，添加 CORS NuGet 包。 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在 "程序包管理器控制台" 窗口中，键入以下命令：

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

此命令安装最新包并更新所有依赖项，包括核心 Web API 库。 使用 `-Version` 标志来面向特定版本。 CORS 包需要 Web API 2.0 或更高版本。

打开文件*应用\_Start/webapiconfig.cs*。 将以下代码添加到**webapiconfig.cs**方法：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

接下来，将 **[EnableCors]** 特性添加到 `TestController` 类：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

对于 "源 *" 参数，* 请使用你在其中部署了 WebClient 应用程序的 URI。 这允许来自 WebClient 的跨源请求，同时仍不允许所有其他跨域请求。 稍后，我将更详细地介绍 **[EnableCors]** 的参数。

请勿在*源 URL 末尾*包含正斜杠。

重新部署更新的 WebService 应用程序。 无需更新 WebClient。 现在，来自 WebClient 的 AJAX 请求应成功。 GET、PUT 和 POST 方法都是允许的。

![显示成功测试消息的 Web 浏览器](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>CORS 如何工作

本部分说明 CORS 请求中 HTTP 消息级别发生的情况。 了解 CORS 的工作原理很重要，这样您就可以正确配置 **[EnableCors]** 属性，并在出现问题时进行故障排除。

CORS 规范引入了几个新的 HTTP 标头，它们启用了跨域请求。 如果浏览器支持 CORS，则会自动为跨域请求设置这些标头;不需要在 JavaScript 代码中执行任何特殊操作。

下面是一个跨源请求的示例。 "源" 标头将为发出请求的站点提供域。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

如果服务器允许该请求，则会设置访问控制允许源标头。 此标头的值可以与源标头匹配，也可以是通配符值 "\*"，表示允许任何源。

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

如果响应不包括访问控制允许源标头，则 AJAX 请求会失败。 具体而言，浏览器不允许该请求。 即使服务器返回成功的响应，浏览器也不会将响应提供给客户端应用程序。

**预检请求**

对于某些 CORS 请求，浏览器会在发送资源的实际请求之前发送一个称为 "预检请求" 的附加请求。

如果满足以下条件，浏览器可以跳过预检请求：

- 请求方法为*GET、HEAD 或 POST，*
- 应用程序不会设置接受、接受语言、内容语言、内容类型或最后事件 ID*之外的任何*请求标头，
- Content-type 标头（如果已设置）是下列其中一项：

    - application/x-www-form-urlencoded
    - 多部分/窗体数据
    - text/plain

有关请求标头的规则适用于应用程序通过对**XMLHttpRequest**对象调用**setRequestHeader**而设置的标头。 （CORS 规范调用这些 "作者请求标头"。）此规则不适用于*浏览器*可以设置的标头，例如用户代理、主机或内容长度。

下面是预检请求的示例：

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

预航班请求使用 HTTP OPTIONS 方法。 它包括两个特殊标头：

- 访问控制-请求-方法：将用于实际请求的 HTTP 方法。
- 访问控制-请求标头：*应用程序*在实际请求上设置的请求标头的列表。 （同样，这不包含浏览器设置的标头。）

下面是一个示例响应，假设服务器允许该请求：

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

响应包括一个访问控制允许方法标头，该标头列出了允许的方法，并且可以选择一个用于列出允许的标头的访问控制允许标头。 如果预检请求成功，则浏览器将发送实际请求，如前文所述。

默认情况下，用于测试具有预检选项请求的终结点的工具（例如， [Fiddler](https://www.telerik.com/fiddler)和[Postman](https://www.getpostman.com/)）默认情况下不发送所需的选项标头。 确认 `Access-Control-Request-Method` 和 `Access-Control-Request-Headers` 标头与请求一起发送，并且选项标头通过 IIS 到达应用。

若要将 IIS 配置为允许 ASP.NET 应用接收和处理选项请求，请将以下配置添加到 `<system.webServer><handlers>` 部分*中的应用的 web.config 文件中*：

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

删除 `OPTIONSVerbHandler` 会阻止 IIS 处理选项请求。 替换 `ExtensionlessUrlHandler-Integrated-4.0` 允许选项请求访问应用，因为默认模块注册只允许 GET、HEAD、POST 和调试请求与无扩展名 Url。

## <a name="scope-rules-for-enablecors"></a>[EnableCors] 的作用域规则

你可以为应用程序中的所有 Web API 控制器启用每个操作、每个控制器或全局的 CORS。

**按操作**

若要为单个操作启用 CORS，请在操作方法上设置 **[EnableCors]** 属性。 下面的示例仅为 `GetItem` 方法启用 CORS。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**每个控制器**

如果在控制器类上设置 **[EnableCors]** ，则将其应用于控制器上的所有操作。 若要为某个操作禁用 CORS，请将 **[DisableCors]** 特性添加到该操作。 下面的示例为除 `PutItem`以外的每种方法启用 CORS。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**全面**

若要为应用程序中的所有 Web API 控制器启用 CORS，请将**EnableCorsAttribute**实例传递到**EnableCors**方法：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

如果在多个作用域上设置属性，则优先顺序为：

1. 操作
2. 控制器
3. Global

## <a name="set-the-allowed-origins"></a>设置允许的来源

**[EnableCors]** *属性的源参数指定*允许哪些来源访问该资源。 该值是允许的来源的以逗号分隔的列表。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

你还可以使用通配符值 "\*" 允许来自任何来源的请求。

在允许来自任何来源的请求之前，请仔细考虑。 这意味着，任何网站都可以对 web API 进行 AJAX 调用。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>设置允许的 HTTP 方法

**[EnableCors]** 特性的*方法*参数指定了允许哪些 HTTP 方法访问该资源。 若要允许所有方法，请使用通配符值 "\*"。 下面的示例只允许 GET 和 POST 请求。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>设置允许的请求标头

本文前面介绍了预检请求可能包含一个访问控制请求标头，其中列出了应用程序设置的 HTTP 标头（所谓的 "作者请求标头"）。 **[EnableCors]** 特性的*标头*参数指定允许的作者请求标头。 若要允许任何标头，请将*标头*设置为 "\*"。 若要将特定标头列入允许列表，请将*标头*设置为允许的标头的逗号分隔列表：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

但是，浏览器在设置访问控制-请求标头的方式上并不完全一致。 例如，Chrome 当前包含 "源"。 FireFox 不包含标准标头（如 "Accept"），即使应用程序在脚本中设置这些标头也是如此。

如果将*标头*设置为 "\*" 以外的任何内容，则至少应包含 "accept"、"content-type" 和 "源"，以及要支持的任何自定义标头。

## <a name="set-the-allowed-response-headers"></a>设置允许的响应标头

默认情况下，浏览器不会向应用程序公开所有的响应标头。 默认情况下可用的响应标头包括：

- Cache-Control
- Content-Language
- Content-Type
- Expires
- 上次修改时间
- 杂

CORS 规范调用这些[简单的响应标头](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)。 若要使其他标头可用于应用程序，请设置 **[EnableCors]** 的*exposedHeaders*参数。

在下面的示例中，控制器的 `Get` 方法设置名为 "X-自定义标头" 的自定义标头。 默认情况下，浏览器不会在跨域请求中公开此标头。 若要使标头可用，请在*exposedHeaders*中包含 "X-自定义标头"。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>传递跨源请求中的凭据

凭据需要在 CORS 请求中进行特殊处理。 默认情况下，浏览器不会发送包含跨域请求的任何凭据。 凭据包括 cookie 和 HTTP 身份验证方案。 若要使用跨域请求发送凭据，客户端必须将**XMLHttpRequest**设置为 true。

直接使用**XMLHttpRequest** ：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

在 jQuery 中：

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

此外，服务器必须允许凭据。 若要在 Web API 中允许跨域凭据，请在 **[EnableCors]** 特性上将**SupportsCredentials**属性设置为 true：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

如果此属性为 true，则 HTTP 响应将包含一个访问控制允许凭据标头。 此标头通知浏览器服务器允许跨源请求的凭据。

如果浏览器发送凭据，但响应不包含有效的 "访问控制-允许-凭据" 标头，则浏览器将不会向应用程序公开响应，而且 AJAX 请求会失败。

将**SupportsCredentials**设置为 true 时要小心，因为这意味着另一个域中的网站可以代表用户将登录用户的凭据发送到 Web API，而不知道用户。 CORS 规范还指出，如果**SupportsCredentials**为 true，则将 &quot;\*&quot;*的设置为*无效。

## <a name="custom-cors-policy-providers"></a>自定义 CORS 策略提供程序

**[EnableCors]** 特性实现**ICorsPolicyProvider**接口。 您可以通过创建从**Attribute**派生的类并实现**ICorsPolicyProvider**来提供自己的实现。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

现在，你可以将该属性应用于要放置 **[EnableCors]** 的任何位置。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

例如，自定义 CORS 策略提供程序可以从配置文件中读取设置。

作为使用特性的替代方法，可以注册创建**ICorsPolicyProvider**对象的**ICorsPolicyProviderFactory**对象。

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

若要设置**ICorsPolicyProviderFactory**，请在启动时调用**SetCorsPolicyProviderFactory**扩展方法，如下所示：

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>浏览器支持

Web API CORS 包是一种服务器端技术。 用户的浏览器还需要支持 CORS。 幸运的是，所有主流浏览器的当前版本都[支持 CORS](http://caniuse.com/cors)。
