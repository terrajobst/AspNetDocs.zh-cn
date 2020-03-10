---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用基本身份验证。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447632"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="a39b8-103">ASP.NET Web API 中的基本身份验证</span><span class="sxs-lookup"><span data-stu-id="a39b8-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="a39b8-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a39b8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a39b8-105">基本身份验证在[RFC 2617 中定义，HTTP 身份验证：基本和摘要式访问身份验证](http://www.ietf.org/rfc/rfc2617.txt)。</span><span class="sxs-lookup"><span data-stu-id="a39b8-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="a39b8-106">缺点</span><span class="sxs-lookup"><span data-stu-id="a39b8-106">Disadvantages</span></span>

- <span data-ttu-id="a39b8-107">用户凭据是在请求中发送的。</span><span class="sxs-lookup"><span data-stu-id="a39b8-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="a39b8-108">凭据以纯文本形式发送。</span><span class="sxs-lookup"><span data-stu-id="a39b8-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="a39b8-109">凭据随每个请求一起发送。</span><span class="sxs-lookup"><span data-stu-id="a39b8-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="a39b8-110">除了在浏览器会话结束以外，没有办法注销。</span><span class="sxs-lookup"><span data-stu-id="a39b8-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="a39b8-111">易受跨站点请求伪造（CSRF）的攻击;需要反 CSRF 度量值。</span><span class="sxs-lookup"><span data-stu-id="a39b8-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="a39b8-112">优点</span><span class="sxs-lookup"><span data-stu-id="a39b8-112">Advantages</span></span>

- <span data-ttu-id="a39b8-113">Internet 标准版。</span><span class="sxs-lookup"><span data-stu-id="a39b8-113">Internet standard.</span></span>
- <span data-ttu-id="a39b8-114">受所有主要浏览器的支持。</span><span class="sxs-lookup"><span data-stu-id="a39b8-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="a39b8-115">相对简单的协议。</span><span class="sxs-lookup"><span data-stu-id="a39b8-115">Relatively simple protocol.</span></span>

<span data-ttu-id="a39b8-116">基本身份验证的工作原理如下所示：</span><span class="sxs-lookup"><span data-stu-id="a39b8-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="a39b8-117">如果请求要求身份验证，则服务器将返回401（未授权）。</span><span class="sxs-lookup"><span data-stu-id="a39b8-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="a39b8-118">响应包括 WWW 身份验证标头，指示服务器支持基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="a39b8-119">客户端向授权标头中的客户端凭据发送另一个请求。</span><span class="sxs-lookup"><span data-stu-id="a39b8-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="a39b8-120">凭据的格式为字符串 "名称： password"，采用 base64 编码。</span><span class="sxs-lookup"><span data-stu-id="a39b8-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="a39b8-121">凭据未加密。</span><span class="sxs-lookup"><span data-stu-id="a39b8-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="a39b8-122">基本身份验证在 "领域" 的上下文中执行。</span><span class="sxs-lookup"><span data-stu-id="a39b8-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="a39b8-123">服务器在 WWW 身份验证标头中包含领域的名称。</span><span class="sxs-lookup"><span data-stu-id="a39b8-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="a39b8-124">用户的凭据在该领域内有效。</span><span class="sxs-lookup"><span data-stu-id="a39b8-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="a39b8-125">领域的确切范围由服务器定义。</span><span class="sxs-lookup"><span data-stu-id="a39b8-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="a39b8-126">例如，你可以定义多个领域来对资源进行分区。</span><span class="sxs-lookup"><span data-stu-id="a39b8-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="a39b8-127">由于凭据未加密发送，因此基本身份验证仅通过 HTTPS 进行保护。</span><span class="sxs-lookup"><span data-stu-id="a39b8-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="a39b8-128">请参阅[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a39b8-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="a39b8-129">基本身份验证也容易受到 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="a39b8-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="a39b8-130">用户输入凭据后，浏览器会在会话期间自动将其发送到相同域的后续请求。</span><span class="sxs-lookup"><span data-stu-id="a39b8-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="a39b8-131">这包括 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="a39b8-131">This includes AJAX requests.</span></span> <span data-ttu-id="a39b8-132">请参阅[防止跨站点请求伪造（CSRF）攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="a39b8-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="a39b8-133">带有 IIS 的基本身份验证</span><span class="sxs-lookup"><span data-stu-id="a39b8-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="a39b8-134">IIS 支持基本身份验证，但有一些需要注意的事项：根据用户的 Windows 凭据对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="a39b8-135">这意味着用户必须拥有服务器域中的帐户。</span><span class="sxs-lookup"><span data-stu-id="a39b8-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="a39b8-136">对于面向公众的网站，通常需要针对 ASP.NET 成员资格提供程序进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="a39b8-137">若要使用 IIS 启用基本身份验证，请在 ASP.NET 项目的 web.config 中将身份验证模式设置为 "Windows"：</span><span class="sxs-lookup"><span data-stu-id="a39b8-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="a39b8-138">在此模式下，IIS 使用 Windows 凭据进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="a39b8-139">此外，还必须在 IIS 中启用基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="a39b8-140">在 IIS 管理器中转到 "功能" 视图，选择 "身份验证"，并启用基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="a39b8-141">在 Web API 项目中，为需要身份验证的任何控制器操作添加 `[Authorize]` 特性。</span><span class="sxs-lookup"><span data-stu-id="a39b8-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="a39b8-142">客户端通过设置请求中的 Authorization 标头对自身进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="a39b8-143">浏览器客户端会自动执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="a39b8-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="a39b8-144">Nonbrowser 客户端将需要设置标头。</span><span class="sxs-lookup"><span data-stu-id="a39b8-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="a39b8-145">具有自定义成员身份的基本身份验证</span><span class="sxs-lookup"><span data-stu-id="a39b8-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="a39b8-146">如前所述，IIS 中内置的基本身份验证使用 Windows 凭据。</span><span class="sxs-lookup"><span data-stu-id="a39b8-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="a39b8-147">这意味着你需要为你的宿主服务器上的用户创建帐户。</span><span class="sxs-lookup"><span data-stu-id="a39b8-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="a39b8-148">但对于 internet 应用程序，用户帐户通常存储在外部数据库中。</span><span class="sxs-lookup"><span data-stu-id="a39b8-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="a39b8-149">下面的代码演示如何执行基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="a39b8-150">您可以通过替换 `CheckPassword` 方法来轻松插入 ASP.NET 成员资格提供程序，这是本示例中的一个虚方法。</span><span class="sxs-lookup"><span data-stu-id="a39b8-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="a39b8-151">在 Web API 2 中，应考虑编写[身份验证筛选器](authentication-filters.md)或[OWIN 中间件](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="a39b8-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="a39b8-152">若要启用 HTTP 模块，请将以下内容添加到**system.webserver 节中的 web.config**文件中：</span><span class="sxs-lookup"><span data-stu-id="a39b8-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="a39b8-153">将 "; Yourassemblyname&gt" 替换为程序集的名称（不包括 "dll" 扩展名）。</span><span class="sxs-lookup"><span data-stu-id="a39b8-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="a39b8-154">你应禁用其他身份验证方案，如窗体或 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="a39b8-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
