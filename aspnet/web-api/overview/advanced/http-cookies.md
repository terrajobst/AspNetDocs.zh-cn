---
uid: web-api/overview/advanced/http-cookies
title: HTTP Cookie 在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 介绍如何发送和接收 HTTP cookie Web API 中的 ASP.NET 4.x。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126242"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="8901e-103">ASP.NET Web API 中的 HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="8901e-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="8901e-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8901e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8901e-105">本主题介绍如何发送和接收 Web API 中的 HTTP cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="8901e-106">HTTP Cookie 的背景信息</span><span class="sxs-lookup"><span data-stu-id="8901e-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="8901e-107">本部分提供 cookie 在 HTTP 级别的实现方式的简要的概述。</span><span class="sxs-lookup"><span data-stu-id="8901e-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="8901e-108">有关详细信息，请查阅[RFC 6265](http://tools.ietf.org/html/rfc6265)。</span><span class="sxs-lookup"><span data-stu-id="8901e-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="8901e-109">Cookie 是一种服务器发送的 HTTP 响应中的数据。</span><span class="sxs-lookup"><span data-stu-id="8901e-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="8901e-110">客户端 （可选） 将存储在 cookie 并将其返回在后续请求。</span><span class="sxs-lookup"><span data-stu-id="8901e-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="8901e-111">这允许客户端和服务器共享状态。</span><span class="sxs-lookup"><span data-stu-id="8901e-111">This allows the client and server to share state.</span></span> <span data-ttu-id="8901e-112">若要设置一个 cookie，服务器在响应中包含的 Set-cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="8901e-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="8901e-113">Cookie 的格式是一个名称-值对，具有可选特性。</span><span class="sxs-lookup"><span data-stu-id="8901e-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="8901e-114">例如：</span><span class="sxs-lookup"><span data-stu-id="8901e-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="8901e-115">下面是包含属性的一个示例：</span><span class="sxs-lookup"><span data-stu-id="8901e-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="8901e-116">若要返回到服务器的 cookie，客户端在更高版本的请求中包括 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="8901e-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="8901e-117">HTTP 响应可以包括多个 Set-cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="8901e-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="8901e-118">客户端返回使用单一的 Cookie 标头的多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="8901e-119">作用域和 cookie 的持续时间受 Set-cookie 标头中的以下属性：</span><span class="sxs-lookup"><span data-stu-id="8901e-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="8901e-120">**域**:告知客户端的域应接收 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="8901e-121">例如，如果域为"example.com"，客户端将 cookie 返回给每个子域 example.com。</span><span class="sxs-lookup"><span data-stu-id="8901e-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="8901e-122">如果未指定，域是源服务器。</span><span class="sxs-lookup"><span data-stu-id="8901e-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="8901e-123">**路径**:将 cookie 限制为在域中指定的路径。</span><span class="sxs-lookup"><span data-stu-id="8901e-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="8901e-124">如果未指定，则使用请求 URI 的路径。</span><span class="sxs-lookup"><span data-stu-id="8901e-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="8901e-125">**过期**:设置 cookie 的到期日期。</span><span class="sxs-lookup"><span data-stu-id="8901e-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="8901e-126">当它过期时，客户端删除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="8901e-127">**最大期限**:设置 cookie 的最大生存期。</span><span class="sxs-lookup"><span data-stu-id="8901e-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="8901e-128">当它达到最大期限时，客户端删除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="8901e-129">如果这两个`Expires`并`Max-Age`设置，`Max-Age`优先。</span><span class="sxs-lookup"><span data-stu-id="8901e-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="8901e-130">如果未设置，客户端将在当前会话结束时删除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="8901e-131">（"会话"的确切含义由确定用户代理。）</span><span class="sxs-lookup"><span data-stu-id="8901e-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="8901e-132">但是，请注意，客户端可能会忽略 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="8901e-133">例如，用户可能会禁用 cookie 出于隐私原因。</span><span class="sxs-lookup"><span data-stu-id="8901e-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="8901e-134">客户端可能会删除 cookie 之前到期，或限制 cookie 存储数。</span><span class="sxs-lookup"><span data-stu-id="8901e-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="8901e-135">出于隐私原因，客户端通常会拒绝"第三方"cookie，其中域与源服务器不匹配。</span><span class="sxs-lookup"><span data-stu-id="8901e-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="8901e-136">简单地说，服务器不应依赖于取回其设置的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="8901e-137">Web API 中的 cookie</span><span class="sxs-lookup"><span data-stu-id="8901e-137">Cookies in Web API</span></span>

<span data-ttu-id="8901e-138">若要添加到 HTTP 响应 cookie，创建**CookieHeaderValue**实例，它表示 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="8901e-139">然后调用**AddCookies**扩展方法，它定义在**System.Net.Http。HttpResponseHeadersExtensions**类中，以添加该 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="8901e-140">例如，下面的代码将添加的 cookie 中的控制器操作：</span><span class="sxs-lookup"><span data-stu-id="8901e-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="8901e-141">请注意， **AddCookies**采用的数组**CookieHeaderValue**实例。</span><span class="sxs-lookup"><span data-stu-id="8901e-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="8901e-142">若要从客户端请求中提取 cookie，调用**GetCookies**方法：</span><span class="sxs-lookup"><span data-stu-id="8901e-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="8901e-143">一个**CookieHeaderValue**包含一系列**CookieState**实例。</span><span class="sxs-lookup"><span data-stu-id="8901e-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="8901e-144">每个**CookieState**表示一个 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="8901e-145">使用索引器方法来获取**CookieState**按名称，如所示。</span><span class="sxs-lookup"><span data-stu-id="8901e-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="8901e-146">结构化的 Cookie 数据</span><span class="sxs-lookup"><span data-stu-id="8901e-146">Structured Cookie Data</span></span>

<span data-ttu-id="8901e-147">很多浏览器限制它们将存储多少 cookie&#8212;总数，以及每个域数。</span><span class="sxs-lookup"><span data-stu-id="8901e-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="8901e-148">因此，它可用于结构化的数据置于单个 cookie，而不是设置多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="8901e-149">RFC 6265 未定义 cookie 数据的结构。</span><span class="sxs-lookup"><span data-stu-id="8901e-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="8901e-150">使用**CookieHeaderValue**类，您可以将传递 cookie 数据的名称-值对的列表。</span><span class="sxs-lookup"><span data-stu-id="8901e-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="8901e-151">这些名称 / 值对编码为 URL 编码格式的 Set-cookie 标头中的数据：</span><span class="sxs-lookup"><span data-stu-id="8901e-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="8901e-152">前面的代码生成以下的 Set-cookie 标头：</span><span class="sxs-lookup"><span data-stu-id="8901e-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="8901e-153">**CookieState**类提供了索引器的方法： 从请求消息中的 cookie 中读取子值：</span><span class="sxs-lookup"><span data-stu-id="8901e-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="8901e-154">示例:设置和检索消息处理程序中的 Cookie</span><span class="sxs-lookup"><span data-stu-id="8901e-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="8901e-155">前面的示例显示如何使用从 Web API 控制器中的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="8901e-156">另一种方法是使用[消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="8901e-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="8901e-157">前面在控制器与管道中调用的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="8901e-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="8901e-158">消息处理程序可以请求到达控制器之前, 从请求中读取 cookie 或控制器生成响应后向响应添加 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="8901e-159">下面的代码演示创建的会话 Id 的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="8901e-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="8901e-160">会话 ID 存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="8901e-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="8901e-161">处理程序进行检查的会话 cookie 的请求。</span><span class="sxs-lookup"><span data-stu-id="8901e-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="8901e-162">如果请求不包含 cookie，该处理程序将生成一个新的会话 id。</span><span class="sxs-lookup"><span data-stu-id="8901e-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="8901e-163">在任一情况下，处理程序存储中的会话 ID **HttpRequestMessage.Properties**属性包。</span><span class="sxs-lookup"><span data-stu-id="8901e-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="8901e-164">它还添加到 HTTP 响应的会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="8901e-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="8901e-165">此实现不会验证从客户端的会话 ID 实际上由服务器颁发。</span><span class="sxs-lookup"><span data-stu-id="8901e-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="8901e-166">不将其用作形式的身份验证 ！</span><span class="sxs-lookup"><span data-stu-id="8901e-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="8901e-167">此示例的重点是显示 HTTP cookie 管理。</span><span class="sxs-lookup"><span data-stu-id="8901e-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="8901e-168">控制器可以获取会话 ID **HttpRequestMessage.Properties**属性包。</span><span class="sxs-lookup"><span data-stu-id="8901e-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
