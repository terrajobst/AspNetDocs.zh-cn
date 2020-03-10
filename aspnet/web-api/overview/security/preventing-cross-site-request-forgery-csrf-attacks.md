---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 在 ASP.NET MVC 中阻止跨站点请求伪造（CSRF）攻击
author: MikeWasson
description: 介绍跨站点请求伪造（CSRF）攻击，以及如何在 ASP.NET Web MVC 中实现反 CSRF 度量值。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447110"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a><span data-ttu-id="297e0-103">阻止 ASP.NET MVC 应用程序中的跨站点请求伪造（CSRF）攻击</span><span class="sxs-lookup"><span data-stu-id="297e0-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET MVC Application</span></span>

<span data-ttu-id="297e0-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="297e0-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="297e0-105">跨站点请求伪造（CSRF）是一种攻击，其中恶意站点将请求发送到用户当前登录的有漏洞站点</span><span class="sxs-lookup"><span data-stu-id="297e0-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="297e0-106">下面是 CSRF 攻击的示例：</span><span class="sxs-lookup"><span data-stu-id="297e0-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="297e0-107">用户使用窗体身份验证登录 `www.example.com`。</span><span class="sxs-lookup"><span data-stu-id="297e0-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="297e0-108">服务器对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="297e0-108">The server authenticates the user.</span></span> <span data-ttu-id="297e0-109">来自服务器的响应包含一个身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="297e0-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="297e0-110">如果不注销，用户将访问恶意网站。</span><span class="sxs-lookup"><span data-stu-id="297e0-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="297e0-111">此恶意网站包含以下 HTML 格式：</span><span class="sxs-lookup"><span data-stu-id="297e0-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="297e0-112">请注意，窗体操作会发布到易受攻击的站点，而不是恶意站点。</span><span class="sxs-lookup"><span data-stu-id="297e0-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="297e0-113">这是 CSRF 的 "跨站点" 部分。</span><span class="sxs-lookup"><span data-stu-id="297e0-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="297e0-114">用户单击 "提交" 按钮。</span><span class="sxs-lookup"><span data-stu-id="297e0-114">The user clicks the submit button.</span></span> <span data-ttu-id="297e0-115">浏览器包含请求中的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="297e0-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="297e0-116">请求在服务器上使用用户的身份验证上下文运行，并可执行允许经过身份验证的用户执行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="297e0-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="297e0-117">尽管此示例要求用户单击 "窗体" 按钮，但恶意页面可以轻松地运行自动提交窗体的脚本。</span><span class="sxs-lookup"><span data-stu-id="297e0-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="297e0-118">而且，使用 SSL 不会阻止 CSRF 攻击，因为恶意站点可以发送 "https://" 请求。</span><span class="sxs-lookup"><span data-stu-id="297e0-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="297e0-119">通常，可以对使用 cookie 进行身份验证的网站执行 CSRF 攻击，因为浏览器会将所有相关 cookie 发送到目标网站。</span><span class="sxs-lookup"><span data-stu-id="297e0-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="297e0-120">但是，CSRF 攻击并不局限于利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="297e0-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="297e0-121">例如，基本身份验证和摘要式身份验证也容易受到攻击。</span><span class="sxs-lookup"><span data-stu-id="297e0-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="297e0-122">用户使用基本或摘要式身份验证登录后。</span><span class="sxs-lookup"><span data-stu-id="297e0-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="297e0-123">浏览器会自动发送凭据，直到会话结束。</span><span class="sxs-lookup"><span data-stu-id="297e0-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="297e0-124">防伪标记</span><span class="sxs-lookup"><span data-stu-id="297e0-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="297e0-125">为了帮助防止 CSRF 攻击，ASP.NET MVC 使用了防伪令牌，也称为*请求验证令牌*。</span><span class="sxs-lookup"><span data-stu-id="297e0-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="297e0-126">客户端请求包含窗体的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="297e0-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="297e0-127">服务器在响应中包括两个标记。</span><span class="sxs-lookup"><span data-stu-id="297e0-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="297e0-128">一个令牌作为 cookie 发送。</span><span class="sxs-lookup"><span data-stu-id="297e0-128">One token is sent as a cookie.</span></span> <span data-ttu-id="297e0-129">另一个被置于隐藏的窗体字段中。</span><span class="sxs-lookup"><span data-stu-id="297e0-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="297e0-130">令牌是随机生成的，因此，攻击者无法猜测值。</span><span class="sxs-lookup"><span data-stu-id="297e0-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="297e0-131">当客户端提交窗体时，它必须将两个令牌都发送回服务器。</span><span class="sxs-lookup"><span data-stu-id="297e0-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="297e0-132">客户端将 cookie 令牌作为 cookie 发送，并在表单数据内发送窗体令牌。</span><span class="sxs-lookup"><span data-stu-id="297e0-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="297e0-133">（当用户提交窗体时，浏览器客户端会自动执行此功能。）</span><span class="sxs-lookup"><span data-stu-id="297e0-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="297e0-134">如果请求不包含这两个令牌，服务器将不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="297e0-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="297e0-135">下面是带有隐藏的窗体标记的 HTML 窗体的示例：</span><span class="sxs-lookup"><span data-stu-id="297e0-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="297e0-136">由于存在相同的源策略，恶意页面无法读取用户的令牌，因此，防伪令牌工作正常。</span><span class="sxs-lookup"><span data-stu-id="297e0-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="297e0-137">（[相同源策略](http://www.w3.org/Security/wiki/Same_Origin_Policy)阻止在两个不同站点上托管的文档访问彼此的内容。</span><span class="sxs-lookup"><span data-stu-id="297e0-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="297e0-138">因此，在前面的示例中，恶意页面可以将请求发送到 example.com，但无法读取响应。）</span><span class="sxs-lookup"><span data-stu-id="297e0-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="297e0-139">若要防止 CSRF 攻击，请将防伪令牌与任何身份验证协议一起使用，浏览器会在用户登录后自动发送凭据。</span><span class="sxs-lookup"><span data-stu-id="297e0-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="297e0-140">这包括基于 cookie 的身份验证协议（如 forms 身份验证）以及基本和摘要式身份验证等协议。</span><span class="sxs-lookup"><span data-stu-id="297e0-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="297e0-141">对于任何 nonsafe 方法（POST、PUT、DELETE），都应需要防伪令牌。</span><span class="sxs-lookup"><span data-stu-id="297e0-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="297e0-142">此外，请确保安全方法（GET、HEAD）没有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="297e0-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="297e0-143">而且，如果你启用了跨域支持（如 CORS 或 JSONP），则甚至安全方法（如 GET）都可能容易遭受 CSRF 攻击，使得攻击者能够读取可能敏感的数据。</span><span class="sxs-lookup"><span data-stu-id="297e0-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="297e0-144">ASP.NET MVC 中的防伪令牌</span><span class="sxs-lookup"><span data-stu-id="297e0-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="297e0-145">若要将防伪令牌添加到 Razor 页面，请使用**HtmlHelper. AntiForgeryToken** helper 方法：</span><span class="sxs-lookup"><span data-stu-id="297e0-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="297e0-146">此方法可添加隐藏的窗体字段，还可以设置 cookie 令牌。</span><span class="sxs-lookup"><span data-stu-id="297e0-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="297e0-147">反 CSRF 和 AJAX</span><span class="sxs-lookup"><span data-stu-id="297e0-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="297e0-148">对于 AJAX 请求，窗体标记可能是一个问题，因为 AJAX 请求可能发送 JSON 数据，而不是 HTML 表单数据。</span><span class="sxs-lookup"><span data-stu-id="297e0-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="297e0-149">一种解决方法是在自定义 HTTP 标头中发送令牌。</span><span class="sxs-lookup"><span data-stu-id="297e0-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="297e0-150">以下代码使用 Razor 语法生成令牌，然后将令牌添加到 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="297e0-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="297e0-151">令牌是通过调用**防伪**在服务器上生成的。</span><span class="sxs-lookup"><span data-stu-id="297e0-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="297e0-152">处理请求时，请从请求标头中提取令牌。</span><span class="sxs-lookup"><span data-stu-id="297e0-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="297e0-153">然后调用**防伪**方法来验证令牌。</span><span class="sxs-lookup"><span data-stu-id="297e0-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="297e0-154">如果标记无效，则**Validate**方法将引发异常。</span><span class="sxs-lookup"><span data-stu-id="297e0-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
