---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API 中的 HTTP Cookie-ASP.NET 4。x
author: MikeWasson
description: 介绍如何在 ASP.NET 4.x 的 Web API 中发送和接收 HTTP cookie。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449312"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="d6e94-103">ASP.NET Web API 中的 HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="d6e94-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="d6e94-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d6e94-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d6e94-105">本主题介绍如何在 Web API 中发送和接收 HTTP cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="d6e94-106">HTTP Cookie 的背景</span><span class="sxs-lookup"><span data-stu-id="d6e94-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="d6e94-107">本部分简要概述了如何在 HTTP 级别实现 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="d6e94-108">有关详细信息，请参阅[RFC 6265](http://tools.ietf.org/html/rfc6265)。</span><span class="sxs-lookup"><span data-stu-id="d6e94-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="d6e94-109">Cookie 是服务器在 HTTP 响应中发送的一段数据。</span><span class="sxs-lookup"><span data-stu-id="d6e94-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="d6e94-110">客户端（可选）存储 cookie 并在后续请求中返回。</span><span class="sxs-lookup"><span data-stu-id="d6e94-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="d6e94-111">这允许客户端和服务器共享状态。</span><span class="sxs-lookup"><span data-stu-id="d6e94-111">This allows the client and server to share state.</span></span> <span data-ttu-id="d6e94-112">若要设置 cookie，服务器会在响应中包括一个集 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="d6e94-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="d6e94-113">Cookie 的格式为名称-值对，具有可选属性。</span><span class="sxs-lookup"><span data-stu-id="d6e94-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="d6e94-114">例如:</span><span class="sxs-lookup"><span data-stu-id="d6e94-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="d6e94-115">下面是一个具有属性的示例：</span><span class="sxs-lookup"><span data-stu-id="d6e94-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="d6e94-116">若要将 cookie 返回到服务器，客户端会在以后的请求中包含 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="d6e94-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="d6e94-117">HTTP 响应可以包括多个设置 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="d6e94-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="d6e94-118">客户端使用一个 Cookie 标头返回多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="d6e94-119">Cookie 的范围和持续时间由设置 Cookie 标头中的以下属性控制：</span><span class="sxs-lookup"><span data-stu-id="d6e94-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="d6e94-120">**域**：告知客户端哪个域应接收 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="d6e94-121">例如，如果域为 "example.com"，则客户端会将该 cookie 返回到 example.com 的每个子域。</span><span class="sxs-lookup"><span data-stu-id="d6e94-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="d6e94-122">如果未指定，则域为源服务器。</span><span class="sxs-lookup"><span data-stu-id="d6e94-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="d6e94-123">**路径**：将 cookie 限制为域中的指定路径。</span><span class="sxs-lookup"><span data-stu-id="d6e94-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="d6e94-124">如果未指定，则使用请求 URI 的路径。</span><span class="sxs-lookup"><span data-stu-id="d6e94-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="d6e94-125">**过期**：为 cookie 设置到期日期。</span><span class="sxs-lookup"><span data-stu-id="d6e94-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="d6e94-126">当 cookie 过期时，客户端会将其删除。</span><span class="sxs-lookup"><span data-stu-id="d6e94-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="d6e94-127">**最大期限**：设置 cookie 的最大生存期。</span><span class="sxs-lookup"><span data-stu-id="d6e94-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="d6e94-128">客户端在达到最长期限时删除 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="d6e94-129">如果同时设置了 `Expires` 和 `Max-Age`，则 `Max-Age` 优先。</span><span class="sxs-lookup"><span data-stu-id="d6e94-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="d6e94-130">如果未设置，则在当前会话结束时，客户端将删除 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="d6e94-131">（"会话" 的确切含义由用户代理决定。）</span><span class="sxs-lookup"><span data-stu-id="d6e94-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="d6e94-132">但请注意，客户端可能会忽略 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="d6e94-133">例如，出于隐私原因，用户可能禁用 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="d6e94-134">在客户端过期之前，客户端可能会删除 cookie，或限制存储的 cookie 数。</span><span class="sxs-lookup"><span data-stu-id="d6e94-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="d6e94-135">出于隐私原因，客户端通常会拒绝 "第三方" cookie，其中域与源服务器不匹配。</span><span class="sxs-lookup"><span data-stu-id="d6e94-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="d6e94-136">简而言之，服务器不应依赖于取回它所设置的 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="d6e94-137">Web API 中的 cookie</span><span class="sxs-lookup"><span data-stu-id="d6e94-137">Cookies in Web API</span></span>

<span data-ttu-id="d6e94-138">若要将 cookie 添加到 HTTP 响应，请创建表示该 cookie 的**CookieHeaderValue**实例。</span><span class="sxs-lookup"><span data-stu-id="d6e94-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="d6e94-139">然后调用**AddCookies**扩展方法，该方法在**系统 .net 中定义。HttpResponseHeadersExtensions**类用于添加 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="d6e94-140">例如，下面的代码在控制器操作中添加了一个 cookie：</span><span class="sxs-lookup"><span data-stu-id="d6e94-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="d6e94-141">请注意， **AddCookies**采用**CookieHeaderValue**实例的数组。</span><span class="sxs-lookup"><span data-stu-id="d6e94-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="d6e94-142">若要从客户端请求中提取 cookie，请调用**GetCookies**方法：</span><span class="sxs-lookup"><span data-stu-id="d6e94-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="d6e94-143">**CookieHeaderValue**包含**CookieState**实例的集合。</span><span class="sxs-lookup"><span data-stu-id="d6e94-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="d6e94-144">每个**CookieState**都表示一个 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="d6e94-145">按照如下所示，使用索引器方法获取**CookieState** 。</span><span class="sxs-lookup"><span data-stu-id="d6e94-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="d6e94-146">结构化 Cookie 数据</span><span class="sxs-lookup"><span data-stu-id="d6e94-146">Structured Cookie Data</span></span>

<span data-ttu-id="d6e94-147">许多浏览器会限制它们将存储&#8212;总数的 cookie 数和每个域的数量。</span><span class="sxs-lookup"><span data-stu-id="d6e94-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="d6e94-148">因此，可以将结构化数据放入单个 cookie，而不是设置多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="d6e94-149">RFC 6265 未定义 cookie 数据的结构。</span><span class="sxs-lookup"><span data-stu-id="d6e94-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="d6e94-150">使用**CookieHeaderValue**类，可以传递 cookie 数据的名称/值对列表。</span><span class="sxs-lookup"><span data-stu-id="d6e94-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="d6e94-151">这些名称-值对在 Set-Cookie 标头中编码为 URL 编码的格式数据：</span><span class="sxs-lookup"><span data-stu-id="d6e94-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="d6e94-152">前面的代码生成以下 Set-Cookie 标头：</span><span class="sxs-lookup"><span data-stu-id="d6e94-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="d6e94-153">**CookieState**类提供了一个索引器方法，用于从请求消息中的 cookie 读取子值：</span><span class="sxs-lookup"><span data-stu-id="d6e94-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="d6e94-154">示例：在消息处理程序中设置和检索 Cookie</span><span class="sxs-lookup"><span data-stu-id="d6e94-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="d6e94-155">前面的示例演示如何在 Web API 控制器中使用 cookie。</span><span class="sxs-lookup"><span data-stu-id="d6e94-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="d6e94-156">另一种方法是使用[消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="d6e94-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="d6e94-157">与控制器相比，在管道中调用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="d6e94-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="d6e94-158">在请求到达控制器之前，消息处理程序可以从请求读取 cookie，或在控制器生成响应后将 cookie 添加到响应中。</span><span class="sxs-lookup"><span data-stu-id="d6e94-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="d6e94-159">下面的代码演示了用于创建会话 Id 的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="d6e94-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="d6e94-160">会话 ID 存储在一个 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="d6e94-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="d6e94-161">处理程序将检查会话 cookie 的请求。</span><span class="sxs-lookup"><span data-stu-id="d6e94-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="d6e94-162">如果请求不包括 cookie，处理程序会生成新的会话 ID。</span><span class="sxs-lookup"><span data-stu-id="d6e94-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="d6e94-163">在这两种情况下，处理程序将会话 ID 存储在**HttpRequestMessage**属性包中。</span><span class="sxs-lookup"><span data-stu-id="d6e94-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="d6e94-164">它还将会话 cookie 添加到 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="d6e94-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="d6e94-165">此实现不会验证来自客户端的会话 ID 是否确实由服务器颁发。</span><span class="sxs-lookup"><span data-stu-id="d6e94-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="d6e94-166">不要将其用作身份验证形式！</span><span class="sxs-lookup"><span data-stu-id="d6e94-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="d6e94-167">示例的要点是显示 HTTP cookie 管理。</span><span class="sxs-lookup"><span data-stu-id="d6e94-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="d6e94-168">控制器可以从**HttpRequestMessage**属性包获取会话 ID。</span><span class="sxs-lookup"><span data-stu-id="d6e94-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
