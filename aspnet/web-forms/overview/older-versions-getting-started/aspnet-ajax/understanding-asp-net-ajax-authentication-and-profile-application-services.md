---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: 了解 ASP.NET AJAX 身份验证和配置文件应用程序服务 |Microsoft Docs
author: scottcate
description: 身份验证服务允许用户提供凭据以便接收身份验证 cookie，而网关服务则允许自定义用户 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520310"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>了解 ASP.NET AJAX 身份验证和配置文件应用程序服务

作者： [Scott Cate](https://github.com/scottcate)

[下载 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> 身份验证服务允许用户提供凭据以便接收身份验证 cookie，而网关服务则允许由 ASP.NET 提供的自定义用户配置文件。 ASP.NET AJAX authentication 服务的使用与标准 ASP.NET Forms 身份验证兼容，因此，当前使用窗体身份验证的应用程序（如使用登录控件）不会通过升级到 AJAX 身份验证服务而被破坏。

## <a name="introduction"></a>简介

作为 .NET Framework 3.5 的一部分，Microsoft 提供了一个可调整大小的环境升级;不仅可以使用新的开发环境，而且还会推出新的语言集成查询（LINQ）功能和其他语言增强功能。 此外，其他工具集的一些熟悉的功能（特别是 ASP.NET AJAX 扩展）将作为 .NET Framework 基类库的第一类成员包括在内。 这些扩展可实现许多新的丰富客户端功能，包括页面的部分呈现，无需整页刷新、通过客户端脚本访问 Web 服务的能力（包括 ASP.NET 分析 API）和广泛的客户端 API用于镜像在 ASP.NET 服务器端控制集内发现的许多控制方案。

本白皮书介绍了如何实现和使用 ASP.NET 分析和 Forms 身份验证服务，因为它们由 Microsoft ASP.NET AJAX ExtensionsThe AJAX 扩展公开，从而使窗体身份验证非常易于支持（以及分析服务）通过 Web 服务代理脚本公开。 AJAX 扩展还支持通过 AuthenticationServiceManager 类进行自定义身份验证。

本白皮书基于 Visual Studio 2008 和 .NET Framework 3.5 的 Beta 2 版本。 本白皮书还假设你将使用 Visual Studio 2008 Beta 2，而不是 Visual Web Developer Express，并将根据 Visual Studio 的用户界面提供演练。 一些代码示例可能使用 Visual Web Developer 速成版中不可用的项目模板。

## <a name="profiles-and-authentication"></a>*配置文件和身份验证*

Microsoft ASP.NET 配置文件和身份验证服务由 ASP.NET Forms 身份验证系统提供，并且是 ASP.NET 的标准组件。 ASP.NET AJAX 扩展通过脚本代理提供对这些服务的脚本访问，这些服务通过客户端 AJAX 库的 Sys.databases 命名空间下非常简单的模型。

身份验证服务允许用户提供凭据以便接收身份验证 cookie，而网关服务则允许由 ASP.NET 提供的自定义用户配置文件。 ASP.NET AJAX authentication 服务的使用与标准 ASP.NET Forms 身份验证兼容，因此，当前使用窗体身份验证的应用程序（如使用登录控件）不会通过升级到 AJAX 身份验证服务而被破坏。

配置文件服务允许根据身份验证服务提供的成员资格自动集成和存储用户数据。 存储的数据由 web.config 文件指定，各种分析服务提供程序处理数据管理。 对于身份验证服务，AJAX 配置文件服务与标准 ASP.NET 配置文件服务兼容，因此，当前合并 ASP.NET 配置文件服务的功能的页面不应通过包含 AJAX 支持来断开。

将 ASP.NET Authentication 和分析服务本身并入应用程序不在此白皮书的讨论范围内。 有关该主题的详细信息，请参阅 MSDN 库参考文章使用[https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)的成员身份管理用户。 ASP.NET 还包括一个实用工具，用于自动设置 SQL Server 的成员身份，这是 ASP.NET 成员身份的默认身份验证服务提供程序。 有关详细信息，请参阅文章 ASP.NET SQL Server 注册工具（Aspnet\_regsql），网址为[https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)。

## <a name="using-the-aspnet-ajax-authentication-service"></a>*使用 ASP.NET AJAX 身份验证服务*

必须在 web.config 文件中启用 ASP.NET AJAX 身份验证服务：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

身份验证服务需要启用 ASP.NET Forms 身份验证，并要求在客户端浏览器上启用 cookie （脚本无法启用无 cookie 会话，因为无 cookie 会话需要 URL 参数）。

启用并配置 AJAX 身份验证服务后，客户端脚本可以立即利用 AuthenticationService 对象。 首先，客户端脚本将需要利用 `login` 方法和 `isLoggedIn` 属性。 存在多个属性以为登录方法提供默认值，该方法可以接受大量的参数。

*AuthenticationService 成员*

*登录方法：*

Login （）方法开始对用户凭据进行身份验证的请求。 此方法是异步的，不会阻止执行。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| userName | 必须的。 要进行身份验证的用户名。 |
| 密码 | 可选（默认为 null）。 用户的密码。 |
| isPersistent | 可选（默认值为 false）。 用户的身份验证 cookie 是否应跨会话保留。 如果为 false，则用户将在浏览器关闭或会话过期时注销。 |
| redirectUrl | 可选（默认为 null）。身份验证成功后要将浏览器重定向到的 URL。 如果此参数为 null 或空字符串，则不会发生重定向。 |
| customInfo | 可选（默认为 null）。 此参数当前未使用，保留供将来使用。 |
| loginCompletedCallback | 可选（默认为 null）。登录成功完成时要调用的函数。 如果指定此参数，则此参数将覆盖 defaultLoginCompleted 属性。 |
| failedCallback | 可选（默认为 null）。登录失败时要调用的函数。 如果指定此参数，则此参数将覆盖 defaultFailedCallback 属性。 |
| userContext | 可选（默认为 null）。 应传递给回调函数的自定义用户上下文数据。 |

*返回值：*

此函数不包括返回值。 但是，在调用此函数时，将包括多个行为：

- 如果 `redirectUrl` 参数既不为 null 也不是空字符串，则将刷新或更改当前页。
- 但是，如果参数为 null 或空字符串，则调用 `loginCompletedCallback` 参数或 `defaultLoginCompletedCallback` 属性。
- 如果对 web 服务的调用失败，则调用 `defaultFailedCallback` 属性的 `failedCallback` 参数。

*注销方法：*

注销（）方法将删除凭据 cookie，并从 web 应用程序注销当前用户。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| redirectUrl | 可选（默认为 null）。身份验证成功后要将浏览器重定向到的 URL。 如果此参数为 null 或空字符串，则不会发生重定向。 |
| logoutCompletedCallback | 可选（默认为 null）。已成功完成注销时要调用的函数。 如果指定此参数，则此参数将覆盖 defaultLogoutCompleted 属性。 |
| failedCallback | 可选（默认为 null）。登录失败时要调用的函数。 如果指定此参数，则此参数将覆盖 defaultFailedCallback 属性。 |
| userContext | 可选（默认为 null）。 应传递给回调函数的自定义用户上下文数据。 |

*返回值：*

此函数不包括返回值。 但是，在调用此函数时，将包括多个行为：

- 如果 `redirectUrl` 参数既不为 null 也不是空字符串，则将刷新或更改当前页。
- 但是，如果参数为 null 或空字符串，则调用 `logoutCompletedCallback` 参数或 `defaultLogoutCompletedCallback` 属性。
- 如果对 web 服务的调用失败，则调用 `defaultFailedCallback` 属性的 `failedCallback` 参数。

*defaultFailedCallback 属性（get、set）：*

此属性指定在无法与 web 服务进行通信的情况下应调用的函数。 它应收到委托（或函数引用）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| error | 指定错误信息。 |
| userContext | 指定在调用登录或注销函数时提供的用户上下文信息。 |
| methodName | 调用方法的名称。 |

*defaultLoginCompletedCallback 属性（get、set）：*

此属性指定一个函数，该函数应在登录 web 服务调用完成时调用。 它应收到委托（或函数引用）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| validCredentials | 指定用户提供的凭据是否有效。 `true` 如果用户成功登录，则为; 否则为。否则 `false`。 |
| userContext | 指定在调用登录函数时提供的用户上下文信息。 |
| methodName | 调用方法的名称。 |

*defaultLogoutCompletedCallback 属性（get、set）：*

此属性指定一个函数，该函数应在注销 web 服务调用完成时调用。 它应收到委托（或函数引用）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| result | 此参数将始终 `null`;它保留供将来使用。 |
| userContext | 指定在调用登录函数时提供的用户上下文信息。 |
| methodName | 调用方法的名称。 |

*isLoggedIn 属性（get）：*

此属性获取用户的当前身份验证状态;它在页面请求期间由 ScriptManager 对象设置。

如果用户当前已登录，此属性将返回 `true`;否则，它将返回 `false`。

*path 属性（get、set）：*

此属性以编程方式确定身份验证 web 服务的位置。 它可用于重写默认的身份验证提供程序，以及在 ScriptManager 控件的 AuthenticationService 子节点的 Path 属性中以声明方式设置的一个身份验证提供程序（有关详细信息，请参阅使用自定义身份验证服务提供程序主题）。

请注意，默认身份验证服务的位置不会更改。 但是，ASP.NET AJAX 允许你指定 web 服务的位置，该服务提供与 ASP.NET AJAX authentication service proxy 相同的类接口。

另请注意，不应将此属性设置为将脚本请求定向到当前站点之外的值。 因为当前应用程序不会接收到身份验证凭据，所以它毫无用处;此外，基础 AJAX 不应发布跨站点请求，并且可能会在客户端浏览器中产生安全异常。

此属性是一个 `String` 对象，表示身份验证 web 服务的路径。

*timeout 属性（get、set）：*

此属性确定登录请求失败之前等待身份验证服务的时间长度。 如果在等待调用完成时超时时间已到，则会调用请求失败回调，并且调用将无法完成。

此属性是一个表示从身份验证服务等待结果的毫秒数的 `Number` 对象。

*代码示例：登录到身份验证服务*

以下标记是一个示例 ASP.NET 页面，其中包含对 AuthenticationService 类的登录和注销方法的简单脚本调用。

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>通过 AJAX 访问 ASP.NET 分析数据

ASP.NET 分析服务也通过 ASP.NET AJAX 扩展公开。 由于 ASP.NET 分析服务提供了一个用于存储和检索用户数据的丰富、精细的 API，因此这可能是一个出色的工作效率工具。

必须在 web.config 中启用配置文件服务;默认情况下，它不是。 为此，请确保在 web.config 中指定了 `profileService` 的子元素 = true，并且已指定可以读取或写入的属性，如下所示：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

还必须配置配置文件服务。 尽管分析服务的配置不在本白皮书的范围内，但值得注意的是，配置文件配置设置中定义的组将可作为组名称的子属性进行访问。 例如，如果指定了以下配置文件节：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

客户端脚本将能够访问名称、地址. Line1、第二行、Address、address、address 和 BackgroundColor 作为 ProfileService 类的属性字段的属性。

配置 AJAX 分析服务后，将立即在页面中提供;但是，在使用之前，必须加载一次。

*ProfileService 成员*

*属性字段：*

"属性" 字段将所有配置的配置文件数据公开为可通过点操作员名称约定引用的子属性。 作为属性组的子级的属性称为 "组名称"。 在上面介绍的示例配置文件配置中，若要获取用户的状态，可以使用以下标识符：

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*load 方法：*

从服务器加载选定列表或所有属性。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| propertyNames | 可选（默认为 null）。 要从服务器加载的属性。 |
| loadCompletedCallback | 可选（默认为 null）。 加载完成时要调用的函数。 |
| failedCallback | 可选（默认为 null）。 发生错误时要调用的函数。 |
| userContext | 可选（默认为 null）。 要传递给回调函数的上下文信息。 |

Load 函数没有返回值。 如果调用成功完成，它将调用 `loadCompletedCallback` 参数或 `defaultLoadCompletedCallback` 属性。 如果调用失败或超时过期，则将调用 `failedCallback` 参数或 `defaultFailedCallback` 属性。

如果未提供 `propertyNames` 参数，则将从服务器中检索所有读取配置的属性。

*保存方法：*

Save （）方法会将指定的属性列表（或所有属性）保存到用户的 ASP.NET 配置文件。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| propertyNames | 可选（默认为 null）。 要保存到服务器的属性。 |
| saveCompletedCallback | 可选（默认为 null）。 保存完成后要调用的函数。 |
| failedCallback | 可选（默认为 null）。 发生错误时要调用的函数。 |
| userContext | 可选（默认为 null）。 要传递给回调函数的上下文信息。 |

Save 函数没有返回值。 如果调用成功完成，它将调用 `saveCompletedCallback` 参数或 `defaultSaveCompletedCallback` 属性。 如果调用失败或超时过期，则将调用 `failedCallback` 或 `defaultFailedCallback` 属性。

如果 `propertyNames` 参数为 null，则所有配置文件属性将发送到服务器，并且服务器将决定可以保存哪些属性以及哪些属性无法保存。

*defaultFailedCallback 属性（get、set）：*

此属性指定在无法与 web 服务进行通信的情况下应调用的函数。 它应收到委托（或函数引用）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| Error | 指定错误信息。 |
| userContext | 指定在调用 load 或 save 函数时提供的用户上下文信息。 |
| methodName | 调用方法的名称。 |

*defaultSaveCompleted 属性（get、set）：*

此属性指定在完成保存用户的配置文件数据时应调用的函数。 它应收到委托（或函数引用）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| numPropsSaved | 指定已保存的属性数。 |
| userContext | 指定在调用 load 或 save 函数时提供的用户上下文信息。 |
| methodName | 调用方法的名称。 |

*defaultLoadCompleted 属性（get、set）：*

此属性指定应在完成加载用户的配置文件数据时调用的函数。 它应收到委托（或函数引用）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| numPropsLoaded | 指定加载的属性数。 |
| userContext | 指定在调用 load 或 save 函数时提供的用户上下文信息。 |
| methodName | 调用方法的名称。 |

*path 属性（get、set）：*

此属性以编程方式确定配置文件 web 服务的位置。 它可用于重写默认配置文件服务提供程序，以及在 ScriptManager 控件的 ProfileService 子节点的路径属性中以声明方式设置的一个集。

请注意，默认配置文件服务的位置不会更改。 但是，ASP.NET AJAX 允许你指定 web 服务的位置，该服务提供与 ASP.NET AJAX authentication service proxy 相同的类接口。

另请注意，不应将此属性设置为将脚本请求定向到当前站点之外的值。 基础 AJAX 不应发布跨站点请求，并可能会在客户端浏览器中产生安全异常。

此属性是一个 `String` 对象，表示配置文件 web 服务的路径。

*timeout 属性（get、set）：*

此属性确定等待 load 或 save 请求失败之前等待配置文件服务的时间长度。 如果在等待调用完成时超时时间已到，则会调用请求失败回调，并且调用将无法完成。

此属性是一个 `Number` 对象，该对象表示要等待来自配置文件服务的结果的毫秒数。

*代码示例：加载页面加载时的配置文件数据*

以下代码将检查是否对用户进行了身份验证，如果是，则将用户的首选背景色作为页面加载。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*使用自定义身份验证服务提供程序*

ASP.NET AJAX Extension 允许您通过自定义 web 服务公开您的功能，来创建自定义脚本身份验证服务提供程序。 若要使用，web 服务必须公开两种方法，`Login` 和 `Logout`;并且必须指定与默认 ASP.NET AJAX Authentication web 服务的方法签名相同的方法签名。

创建自定义 web 服务后，你将需要在页面上以编程方式以编程方式在代码中或通过客户端脚本来指定该服务的路径。

*若要以声明方式设置路径：*

若要以声明方式设置路径，请在 ASP.NET 页面上包含 ScriptManager 对象的 AuthenticationService 子级：

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*若要在代码中设置路径：*

若要以编程方式设置路径，请通过脚本管理器的实例指定路径：

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*若要在脚本中设置路径：*

若要在脚本中以编程方式设置路径，请使用 AuthenticationService 类的 `path` 属性：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*用于自定义身份验证的示例 Web 服务*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>摘要

ASP.NET 服务-特别是分析、成员身份和身份验证服务-可在客户端浏览器上轻松地向 JavaScript 公开。 这使开发人员能够无缝地将其客户端代码与身份验证机制集成，而无需依赖 UpdatePanels 等控件来执行繁重的工作。 还可以通过使用 web 配置设置来保护来自客户端的配置文件数据;默认情况下不提供数据，开发人员必须选择配置文件属性。

此外，通过使用等效的方法签名创建简化的 web 服务实现，开发人员可以为这些内部的 ASP.NET 服务创建自定义脚本提供程序。 对这些技术的支持简化了丰富客户端应用程序的开发，同时为开发人员提供了可满足特定需求的各种灵活性。

## <a name="bio"></a>*Bio*

Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。 可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-updatepanel-triggers.md)
> [下一页](understanding-asp-net-ajax-localization.md)
