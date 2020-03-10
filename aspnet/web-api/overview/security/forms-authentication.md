---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API 中的 Forms 身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用 Forms 身份验证。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484376"
---
# <a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="7ba83-103">ASP.NET Web API 中的 Forms 身份验证</span><span class="sxs-lookup"><span data-stu-id="7ba83-103">Forms Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="7ba83-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7ba83-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7ba83-105">Forms 身份验证使用 HTML 窗体将用户的凭据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="7ba83-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="7ba83-106">它不是 Internet 标准。</span><span class="sxs-lookup"><span data-stu-id="7ba83-106">It is not an Internet standard.</span></span> <span data-ttu-id="7ba83-107">Forms 身份验证仅适用于从 web 应用程序调用的 web Api，以便用户可以与 HTML 窗体进行交互。</span><span class="sxs-lookup"><span data-stu-id="7ba83-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="7ba83-108">优点</span><span class="sxs-lookup"><span data-stu-id="7ba83-108">Advantages</span></span> | <span data-ttu-id="7ba83-109">缺点</span><span class="sxs-lookup"><span data-stu-id="7ba83-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="7ba83-110">-易于实现：内置于 ASP.NET 中。</span><span class="sxs-lookup"><span data-stu-id="7ba83-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="7ba83-111">-使用 ASP.NET 成员资格提供程序，以便于管理用户帐户。</span><span class="sxs-lookup"><span data-stu-id="7ba83-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="7ba83-112">-不是标准 HTTP 身份验证机制;使用 HTTP cookie，而不是标准授权标头。</span><span class="sxs-lookup"><span data-stu-id="7ba83-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="7ba83-113">-要求使用浏览器客户端。</span><span class="sxs-lookup"><span data-stu-id="7ba83-113">- Requires a browser client.</span></span> <span data-ttu-id="7ba83-114">-以纯文本形式发送凭据。</span><span class="sxs-lookup"><span data-stu-id="7ba83-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="7ba83-115">-易受跨站点请求伪造（CSRF）的攻击;需要反 CSRF 度量值。</span><span class="sxs-lookup"><span data-stu-id="7ba83-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="7ba83-116">-难于从 nonbrowser 客户端使用。</span><span class="sxs-lookup"><span data-stu-id="7ba83-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="7ba83-117">登录需要浏览器。</span><span class="sxs-lookup"><span data-stu-id="7ba83-117">Login requires a browser.</span></span> <span data-ttu-id="7ba83-118">-在请求中发送用户凭据。</span><span class="sxs-lookup"><span data-stu-id="7ba83-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="7ba83-119">-某些用户禁用 cookie。</span><span class="sxs-lookup"><span data-stu-id="7ba83-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="7ba83-120">简单地说，ASP.NET 中的窗体身份验证的工作方式如下：</span><span class="sxs-lookup"><span data-stu-id="7ba83-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="7ba83-121">客户端请求要求身份验证的资源。</span><span class="sxs-lookup"><span data-stu-id="7ba83-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="7ba83-122">如果用户未通过身份验证，则服务器将返回 HTTP 302 （找到）并重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="7ba83-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="7ba83-123">用户输入凭据并提交窗体。</span><span class="sxs-lookup"><span data-stu-id="7ba83-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="7ba83-124">服务器返回重定向回原始 URI 的另一个 HTTP 302。</span><span class="sxs-lookup"><span data-stu-id="7ba83-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="7ba83-125">此响应包括身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="7ba83-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="7ba83-126">客户端会再次请求资源。</span><span class="sxs-lookup"><span data-stu-id="7ba83-126">The client requests the resource again.</span></span> <span data-ttu-id="7ba83-127">请求包括身份验证 cookie，因此服务器将授予请求。</span><span class="sxs-lookup"><span data-stu-id="7ba83-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="7ba83-128">有关详细信息，请参阅[Forms 身份验证概述。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7ba83-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="7ba83-129">将 Forms 身份验证用于 Web API</span><span class="sxs-lookup"><span data-stu-id="7ba83-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="7ba83-130">若要创建使用窗体身份验证的应用程序，请在 MVC 4 项目向导中选择 "Internet 应用程序" 模板。</span><span class="sxs-lookup"><span data-stu-id="7ba83-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="7ba83-131">此模板创建用于帐户管理的 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="7ba83-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="7ba83-132">你还可以使用 ASP.NET 秋季2012更新中提供的 "单页面应用程序" 模板。</span><span class="sxs-lookup"><span data-stu-id="7ba83-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="7ba83-133">在 web API 控制器中，可以使用 `[Authorize]` 特性来限制访问权限，如[使用 [授权] 特性](authentication-and-authorization-in-aspnet-web-api.md#auth3)中所述。</span><span class="sxs-lookup"><span data-stu-id="7ba83-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="7ba83-134">Forms 身份验证使用会话 cookie 对请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="7ba83-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="7ba83-135">浏览器自动向目标网站发送所有相关 cookie。</span><span class="sxs-lookup"><span data-stu-id="7ba83-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="7ba83-136">此功能使得表单身份验证很容易遭受跨站点请求伪造（CSRF）攻击，请参阅[防止跨站点请求伪造（CSRF）攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="7ba83-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="7ba83-137">Forms 身份验证不会对用户的凭据进行加密。</span><span class="sxs-lookup"><span data-stu-id="7ba83-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="7ba83-138">因此，除非与 SSL 一起使用，否则 forms 身份验证不安全。</span><span class="sxs-lookup"><span data-stu-id="7ba83-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="7ba83-139">请参阅[在 WEB API 中使用 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7ba83-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
