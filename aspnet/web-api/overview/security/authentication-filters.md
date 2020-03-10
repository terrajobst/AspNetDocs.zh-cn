---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 中的身份验证筛选器 |Microsoft Docs
author: MikeWasson
description: 身份验证筛选器是用于对 HTTP 请求进行身份验证的组件。 Web API 2 和 MVC 5 两者都支持身份验证筛选器，但它们略有不同。
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447770"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的身份验证筛选器

作者： [Mike Wasson](https://github.com/MikeWasson)

> 身份验证筛选器是用于对 HTTP 请求进行身份验证的组件。 Web API 2 和 MVC 5 都支持身份验证筛选器，但它们略有不同，这通常是在筛选器接口的命名约定中。 本主题介绍了 Web API 身份验证筛选器。

身份验证筛选器使你可以为单个控制器或操作设置一个身份验证方案。 这样一来，你的应用可以支持不同 HTTP 资源的不同身份验证机制。

在本文中，我将在[https://github.com/aspnet/samples](https://github.com/aspnet/samples)上显示[基本身份验证](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)示例中的代码。 此示例显示了实现 HTTP 基本访问身份验证方案（RFC 2617）的身份验证筛选器。 该筛选器在名为 `IdentityBasicAuthenticationAttribute`的类中实现。 我不会显示示例中的所有代码，只是说明如何编写身份验证筛选器的部分。

## <a name="setting-an-authentication-filter"></a>设置身份验证筛选器

与其他筛选器一样，身份验证筛选器可应用于每个控制器、每个操作或全局应用到所有 Web API 控制器。

若要将身份验证筛选器应用到控制器，请使用筛选器属性修饰控制器类。 下面的代码设置控制器类的 `[IdentityBasicAuthentication]` 筛选器，这将为控制器的所有操作启用基本身份验证。

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

若要将筛选器应用于一个操作，请使用筛选器修饰该操作。 下面的代码在控制器的 `Post` 方法上设置 `[IdentityBasicAuthentication]` 筛选器。

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

若要将筛选器应用于所有 Web API 控制器，请将其添加到**GlobalConfiguration**。

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>实现 Web API 身份验证筛选器

在 Web API 中，身份验证筛选器实现了[IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)接口。 它们还应继承自**system.object**，以便作为特性应用。

**IAuthenticationFilter**接口有两种方法：

- **AuthenticateAsync**通过验证请求（如果存在）中的凭据来对请求进行身份验证。
- 如果需要， **ChallengeAsync**会将身份验证质询添加到 HTTP 响应。

这些方法与[rfc 2612](http://tools.ietf.org/html/rfc2616)和[rfc 2617](http://tools.ietf.org/html/rfc2617)中定义的身份验证流相对应：

1. 客户端在授权标头中发送凭据。 这通常在客户端从服务器接收到401（未授权）响应之后发生。 但是，客户端可以使用任何请求发送凭据，而不是在收到401后发送。
2. 如果服务器不接受凭据，则返回 "401 （未授权）" 响应。 响应包括 Www 身份验证标头，该标头包含一项或多项挑战。 每个质询都指定服务器识别的身份验证方案。

服务器还可以从匿名请求返回401。 事实上，这通常是启动身份验证过程的方式：

1. 客户端发送匿名请求。
2. 服务器返回401。
3. 客户端通过凭据重新发送请求。

此流包括*身份验证*和*授权*步骤。

- 身份验证证明了客户端的标识。
- 授权确定客户端是否可以访问特定资源。

在 Web API 中，身份验证筛选器处理身份验证，但不处理授权。 授权应由授权筛选器或在控制器操作内完成。

下面是 Web API 2 管道中的流：

1. 在调用操作之前，Web API 将创建该操作的身份验证筛选器列表。 这包括具有操作范围、控制器范围和全局范围的筛选器。
2. Web API 对列表中的每个筛选器调用**AuthenticateAsync** 。 每个筛选器都可以验证请求中的凭据。 如果任何筛选器成功验证凭据，则筛选器将创建**IPrincipal** ，并将其附加到请求。 此时，筛选器也会触发错误。 如果是这样，则管道的其余部分不会运行。
3. 假设没有错误，请求会流过管道的其余部分。
4. 最后，Web API 调用每个身份验证筛选器的**ChallengeAsync**方法。 如果需要，筛选器使用此方法将质询添加到响应中。 通常（但不总是）将因401错误而发生。

以下关系图显示了两种可能的情况。 在第一种情况下，身份验证筛选器成功对请求进行身份验证，授权筛选器授权请求，控制器操作返回200（OK）。

![](authentication-filters/_static/image1.png)

在第二个示例中，身份验证筛选器对请求进行身份验证，但授权筛选器返回401（未授权）。 在这种情况下，不会调用控制器操作。 身份验证筛选器将 Www 身份验证标头添加到响应。

![](authentication-filters/_static/image2.png)

可能的其他组合&mdash;例如，如果控制器操作允许匿名请求，则可能具有身份验证筛选器，但没有授权。

## <a name="implementing-the-authenticateasync-method"></a>实现 AuthenticateAsync 方法

**AuthenticateAsync**方法尝试对请求进行身份验证。 下面是方法签名：

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

**AuthenticateAsync**方法必须执行下列操作之一：

1. 无（无操作）。
2. 创建**IPrincipal**并在请求中设置它。
3. 设置错误结果。

选项（1）表示请求没有筛选器理解的任何凭据。 选项（2）表示筛选器已成功通过身份验证请求。 选项（3）表示请求具有无效的凭据（如错误密码），这会触发错误响应。

下面是实现**AuthenticateAsync**的一般概述。

1. 在请求中查找凭据。
2. 如果没有凭据，则不执行任何操作并返回（无操作）。
3. 如果有凭据，但筛选器不能识别身份验证方案，则不执行任何操作并返回（无操作）。 管道中的另一个筛选器可能会了解该方案。
4. 如果存在筛选器理解的凭据，请尝试对它们进行身份验证。
5. 如果凭据错误，请通过设置 `context.ErrorResult`来返回401。
6. 如果凭据有效，请创建**IPrincipal**并设置 `context.Principal`。

以下代码显示[基本身份验证](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)示例中的**AuthenticateAsync**方法。 注释指明了每个步骤。 此代码显示了几种类型的错误：不含凭据的授权标头、不正确的凭据以及错误的用户名/密码。

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>设置错误结果

如果凭据无效，则筛选器必须将 `context.ErrorResult` 设置为创建错误响应的**IHttpActionResult** 。 有关**IHttpActionResult**的详细信息，请参阅[Web API 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。

基本身份验证示例包含一个适用于此目的的 `AuthenticationFailureResult` 类。

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>实现 ChallengeAsync

**ChallengeAsync**方法的用途是在需要时将身份验证质询添加到响应中。 下面是方法签名：

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

对请求管道中的每个身份验证筛选器调用方法。

必须了解的是，在创建 HTTP 响应*之前*调用**ChallengeAsync** ，甚至在控制器操作运行之前也是如此。 调用**ChallengeAsync**时，`context.Result` 包含 IHttpActionResult，稍后将使用该创建 HTTP 响应。 因此，在调用**ChallengeAsync**时，你还不知道有关 HTTP 响应的任何内容。 **ChallengeAsync**方法应使用新的**IHttpActionResult**替换 `context.Result` 的原始值。 此**IHttpActionResult**必须包装原始 `context.Result`。

![](authentication-filters/_static/image3.png)

我将调用原始**IHttpActionResult** *内部结果*，并将新的**IHttpActionResult**为*外部结果*。 外部结果必须执行以下操作：

1. 调用内部结果以创建 HTTP 响应。
2. 检查响应。
3. 如果需要，请向响应中添加身份验证质询。

下面的示例摘自基本身份验证示例。 它为外部结果定义**IHttpActionResult** 。

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

`InnerResult` 属性保留了内部**IHttpActionResult**。 `Challenge` 属性表示 Www 身份验证标头。 请注意， **ExecuteAsync**首先调用 `InnerResult.ExecuteAsync` 来创建 HTTP 响应，然后在需要时添加质询。

在添加质询之前检查响应代码。 如果响应为401，则大多数身份验证方案仅添加质询，如下所示。 但是，某些身份验证方案确实会向成功响应添加质询。 例如，请参阅[Negotiate](http://tools.ietf.org/html/rfc4559#section-5) （RFC 4559）。

给定 `AddChallengeOnUnauthorizedResult` 类， **ChallengeAsync**中的实际代码非常简单。 只需创建结果并将其附加到 `context.Result`。

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

注意：基本身份验证示例通过将此逻辑放在扩展方法中来对其进行抽象。

## <a name="combining-authentication-filters-with-host-level-authentication"></a>结合身份验证筛选器与主机级身份验证

"主机级身份验证" 是指主机（如 IIS）执行的身份验证，然后请求到达 Web API 框架。

通常情况下，你可能想要为应用程序的其余部分启用主机级身份验证，但为 Web API 控制器禁用主机级身份验证。 例如，典型的方案是在主机级别启用窗体身份验证，但对 Web API 使用基于令牌的身份验证。

若要禁用 Web API 管道内的主机级身份验证，请在配置中调用 `config.SuppressHostPrincipal()`。 这会导致 Web API 从进入 Web API 管道的任何请求中删除**IPrincipal** 。 实际上，它 &quot;&quot; 请求进行身份验证。

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>其他资源

[ASP.NET Web API 安全筛选器](https://msdn.microsoft.com/magazine/dn781361.aspx)（MSDN 杂志）
