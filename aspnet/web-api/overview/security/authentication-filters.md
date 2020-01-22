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
ms.openlocfilehash: b6815baf05303d5f47a14ee5fe0fdfc2836c1868
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519370"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="519ee-104">ASP.NET Web API 2 中的身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="519ee-104">Authentication Filters in ASP.NET Web API 2</span></span>

<span data-ttu-id="519ee-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="519ee-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="519ee-106">身份验证筛选器是用于对 HTTP 请求进行身份验证的组件。</span><span class="sxs-lookup"><span data-stu-id="519ee-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="519ee-107">Web API 2 和 MVC 5 都支持身份验证筛选器，但它们略有不同，这通常是在筛选器接口的命名约定中。</span><span class="sxs-lookup"><span data-stu-id="519ee-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="519ee-108">本主题介绍了 Web API 身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="519ee-108">This topic describes Web API authentication filters.</span></span>

<span data-ttu-id="519ee-109">身份验证筛选器使你可以为单个控制器或操作设置一个身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="519ee-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="519ee-110">这样一来，你的应用可以支持不同 HTTP 资源的不同身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="519ee-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="519ee-111">在本文中，我将在[https://github.com/aspnet/samples](https://github.com/aspnet/samples)上显示[基本身份验证](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)示例中的代码。</span><span class="sxs-lookup"><span data-stu-id="519ee-111">In this article, I'll show code from the [Basic Authentication](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample on [https://github.com/aspnet/samples](https://github.com/aspnet/samples).</span></span> <span data-ttu-id="519ee-112">此示例显示了实现 HTTP 基本访问身份验证方案（RFC 2617）的身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="519ee-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="519ee-113">该筛选器在名为 `IdentityBasicAuthenticationAttribute`的类中实现。</span><span class="sxs-lookup"><span data-stu-id="519ee-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="519ee-114">我不会显示示例中的所有代码，只是说明如何编写身份验证筛选器的部分。</span><span class="sxs-lookup"><span data-stu-id="519ee-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="519ee-115">设置身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="519ee-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="519ee-116">与其他筛选器一样，身份验证筛选器可应用于每个控制器、每个操作或全局应用到所有 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="519ee-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="519ee-117">若要将身份验证筛选器应用到控制器，请使用筛选器属性修饰控制器类。</span><span class="sxs-lookup"><span data-stu-id="519ee-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="519ee-118">下面的代码设置控制器类的 `[IdentityBasicAuthentication]` 筛选器，这将为控制器的所有操作启用基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="519ee-119">若要将筛选器应用于一个操作，请使用筛选器修饰该操作。</span><span class="sxs-lookup"><span data-stu-id="519ee-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="519ee-120">下面的代码在控制器的 `Post` 方法上设置 `[IdentityBasicAuthentication]` 筛选器。</span><span class="sxs-lookup"><span data-stu-id="519ee-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="519ee-121">若要将筛选器应用于所有 Web API 控制器，请将其添加到**GlobalConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="519ee-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="519ee-122">实现 Web API 身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="519ee-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="519ee-123">在 Web API 中，身份验证筛选器实现了[IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)接口。</span><span class="sxs-lookup"><span data-stu-id="519ee-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="519ee-124">它们还应继承自**system.object**，以便作为特性应用。</span><span class="sxs-lookup"><span data-stu-id="519ee-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="519ee-125">**IAuthenticationFilter**接口有两种方法：</span><span class="sxs-lookup"><span data-stu-id="519ee-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="519ee-126">**AuthenticateAsync**通过验证请求（如果存在）中的凭据来对请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="519ee-127">如果需要， **ChallengeAsync**会将身份验证质询添加到 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="519ee-128">这些方法与[rfc 2612](http://tools.ietf.org/html/rfc2616)和[rfc 2617](http://tools.ietf.org/html/rfc2617)中定义的身份验证流相对应：</span><span class="sxs-lookup"><span data-stu-id="519ee-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="519ee-129">客户端在授权标头中发送凭据。</span><span class="sxs-lookup"><span data-stu-id="519ee-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="519ee-130">这通常在客户端从服务器接收到401（未授权）响应之后发生。</span><span class="sxs-lookup"><span data-stu-id="519ee-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="519ee-131">但是，客户端可以使用任何请求发送凭据，而不是在收到401后发送。</span><span class="sxs-lookup"><span data-stu-id="519ee-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="519ee-132">如果服务器不接受凭据，则返回 "401 （未授权）" 响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="519ee-133">响应包括 Www 身份验证标头，该标头包含一项或多项挑战。</span><span class="sxs-lookup"><span data-stu-id="519ee-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="519ee-134">每个质询都指定服务器识别的身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="519ee-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="519ee-135">服务器还可以从匿名请求返回401。</span><span class="sxs-lookup"><span data-stu-id="519ee-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="519ee-136">事实上，这通常是启动身份验证过程的方式：</span><span class="sxs-lookup"><span data-stu-id="519ee-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="519ee-137">客户端发送匿名请求。</span><span class="sxs-lookup"><span data-stu-id="519ee-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="519ee-138">服务器返回401。</span><span class="sxs-lookup"><span data-stu-id="519ee-138">The server returns 401.</span></span>
3. <span data-ttu-id="519ee-139">客户端通过凭据重新发送请求。</span><span class="sxs-lookup"><span data-stu-id="519ee-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="519ee-140">此流包括*身份验证*和*授权*步骤。</span><span class="sxs-lookup"><span data-stu-id="519ee-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="519ee-141">身份验证证明了客户端的标识。</span><span class="sxs-lookup"><span data-stu-id="519ee-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="519ee-142">授权确定客户端是否可以访问特定资源。</span><span class="sxs-lookup"><span data-stu-id="519ee-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="519ee-143">在 Web API 中，身份验证筛选器处理身份验证，但不处理授权。</span><span class="sxs-lookup"><span data-stu-id="519ee-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="519ee-144">授权应由授权筛选器或在控制器操作内完成。</span><span class="sxs-lookup"><span data-stu-id="519ee-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="519ee-145">下面是 Web API 2 管道中的流：</span><span class="sxs-lookup"><span data-stu-id="519ee-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="519ee-146">在调用操作之前，Web API 将创建该操作的身份验证筛选器列表。</span><span class="sxs-lookup"><span data-stu-id="519ee-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="519ee-147">这包括具有操作范围、控制器范围和全局范围的筛选器。</span><span class="sxs-lookup"><span data-stu-id="519ee-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="519ee-148">Web API 对列表中的每个筛选器调用**AuthenticateAsync** 。</span><span class="sxs-lookup"><span data-stu-id="519ee-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="519ee-149">每个筛选器都可以验证请求中的凭据。</span><span class="sxs-lookup"><span data-stu-id="519ee-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="519ee-150">如果任何筛选器成功验证凭据，则筛选器将创建**IPrincipal** ，并将其附加到请求。</span><span class="sxs-lookup"><span data-stu-id="519ee-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="519ee-151">此时，筛选器也会触发错误。</span><span class="sxs-lookup"><span data-stu-id="519ee-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="519ee-152">如果是这样，则管道的其余部分不会运行。</span><span class="sxs-lookup"><span data-stu-id="519ee-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="519ee-153">假设没有错误，请求会流过管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="519ee-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="519ee-154">最后，Web API 调用每个身份验证筛选器的**ChallengeAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="519ee-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="519ee-155">如果需要，筛选器使用此方法将质询添加到响应中。</span><span class="sxs-lookup"><span data-stu-id="519ee-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="519ee-156">通常（但不总是）将因401错误而发生。</span><span class="sxs-lookup"><span data-stu-id="519ee-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="519ee-157">以下关系图显示了两种可能的情况。</span><span class="sxs-lookup"><span data-stu-id="519ee-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="519ee-158">在第一种情况下，身份验证筛选器成功对请求进行身份验证，授权筛选器授权请求，控制器操作返回200（OK）。</span><span class="sxs-lookup"><span data-stu-id="519ee-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="519ee-159">在第二个示例中，身份验证筛选器对请求进行身份验证，但授权筛选器返回401（未授权）。</span><span class="sxs-lookup"><span data-stu-id="519ee-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="519ee-160">在这种情况下，不会调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="519ee-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="519ee-161">身份验证筛选器将 Www 身份验证标头添加到响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="519ee-162">可能的其他组合&mdash;例如，如果控制器操作允许匿名请求，则可能具有身份验证筛选器，但没有授权。</span><span class="sxs-lookup"><span data-stu-id="519ee-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="519ee-163">实现 AuthenticateAsync 方法</span><span class="sxs-lookup"><span data-stu-id="519ee-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="519ee-164">**AuthenticateAsync**方法尝试对请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="519ee-165">下面是方法签名：</span><span class="sxs-lookup"><span data-stu-id="519ee-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="519ee-166">**AuthenticateAsync**方法必须执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="519ee-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="519ee-167">无（无操作）。</span><span class="sxs-lookup"><span data-stu-id="519ee-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="519ee-168">创建**IPrincipal**并在请求中设置它。</span><span class="sxs-lookup"><span data-stu-id="519ee-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="519ee-169">设置错误结果。</span><span class="sxs-lookup"><span data-stu-id="519ee-169">Set an error result.</span></span>

<span data-ttu-id="519ee-170">选项（1）表示请求没有筛选器理解的任何凭据。</span><span class="sxs-lookup"><span data-stu-id="519ee-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="519ee-171">选项（2）表示筛选器已成功通过身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="519ee-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="519ee-172">选项（3）表示请求具有无效的凭据（如错误密码），这会触发错误响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="519ee-173">下面是实现**AuthenticateAsync**的一般概述。</span><span class="sxs-lookup"><span data-stu-id="519ee-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="519ee-174">在请求中查找凭据。</span><span class="sxs-lookup"><span data-stu-id="519ee-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="519ee-175">如果没有凭据，则不执行任何操作并返回（无操作）。</span><span class="sxs-lookup"><span data-stu-id="519ee-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="519ee-176">如果有凭据，但筛选器不能识别身份验证方案，则不执行任何操作并返回（无操作）。</span><span class="sxs-lookup"><span data-stu-id="519ee-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="519ee-177">管道中的另一个筛选器可能会了解该方案。</span><span class="sxs-lookup"><span data-stu-id="519ee-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="519ee-178">如果存在筛选器理解的凭据，请尝试对它们进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="519ee-179">如果凭据错误，请通过设置 `context.ErrorResult`来返回401。</span><span class="sxs-lookup"><span data-stu-id="519ee-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="519ee-180">如果凭据有效，请创建**IPrincipal**并设置 `context.Principal`。</span><span class="sxs-lookup"><span data-stu-id="519ee-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="519ee-181">以下代码显示[基本身份验证](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)示例中的**AuthenticateAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="519ee-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample.</span></span> <span data-ttu-id="519ee-182">注释指明了每个步骤。</span><span class="sxs-lookup"><span data-stu-id="519ee-182">The comments indicate each step.</span></span> <span data-ttu-id="519ee-183">此代码显示了几种类型的错误：不含凭据的授权标头、不正确的凭据以及错误的用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="519ee-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="519ee-184">设置错误结果</span><span class="sxs-lookup"><span data-stu-id="519ee-184">Setting an Error Result</span></span>

<span data-ttu-id="519ee-185">如果凭据无效，则筛选器必须将 `context.ErrorResult` 设置为创建错误响应的**IHttpActionResult** 。</span><span class="sxs-lookup"><span data-stu-id="519ee-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="519ee-186">有关**IHttpActionResult**的详细信息，请参阅[Web API 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="519ee-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="519ee-187">基本身份验证示例包含一个适用于此目的的 `AuthenticationFailureResult` 类。</span><span class="sxs-lookup"><span data-stu-id="519ee-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="519ee-188">实现 ChallengeAsync</span><span class="sxs-lookup"><span data-stu-id="519ee-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="519ee-189">**ChallengeAsync**方法的用途是在需要时将身份验证质询添加到响应中。</span><span class="sxs-lookup"><span data-stu-id="519ee-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="519ee-190">下面是方法签名：</span><span class="sxs-lookup"><span data-stu-id="519ee-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="519ee-191">对请求管道中的每个身份验证筛选器调用方法。</span><span class="sxs-lookup"><span data-stu-id="519ee-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="519ee-192">必须了解的是，在创建 HTTP 响应*之前*调用**ChallengeAsync** ，甚至在控制器操作运行之前也是如此。</span><span class="sxs-lookup"><span data-stu-id="519ee-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="519ee-193">调用**ChallengeAsync**时，`context.Result` 包含 IHttpActionResult，稍后将使用该创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="519ee-194">因此，在调用**ChallengeAsync**时，你还不知道有关 HTTP 响应的任何内容。</span><span class="sxs-lookup"><span data-stu-id="519ee-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="519ee-195">**ChallengeAsync**方法应使用新的**IHttpActionResult**替换 `context.Result` 的原始值。</span><span class="sxs-lookup"><span data-stu-id="519ee-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="519ee-196">此**IHttpActionResult**必须包装原始 `context.Result`。</span><span class="sxs-lookup"><span data-stu-id="519ee-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="519ee-197">我将调用原始**IHttpActionResult** *内部结果*，并将新的**IHttpActionResult**为*外部结果*。</span><span class="sxs-lookup"><span data-stu-id="519ee-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="519ee-198">外部结果必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="519ee-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="519ee-199">调用内部结果以创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="519ee-200">检查响应。</span><span class="sxs-lookup"><span data-stu-id="519ee-200">Examine the response.</span></span>
3. <span data-ttu-id="519ee-201">如果需要，请向响应中添加身份验证质询。</span><span class="sxs-lookup"><span data-stu-id="519ee-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="519ee-202">下面的示例摘自基本身份验证示例。</span><span class="sxs-lookup"><span data-stu-id="519ee-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="519ee-203">它为外部结果定义**IHttpActionResult** 。</span><span class="sxs-lookup"><span data-stu-id="519ee-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="519ee-204">`InnerResult` 属性保留了内部**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="519ee-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="519ee-205">`Challenge` 属性表示 Www 身份验证标头。</span><span class="sxs-lookup"><span data-stu-id="519ee-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="519ee-206">请注意， **ExecuteAsync**首先调用 `InnerResult.ExecuteAsync` 来创建 HTTP 响应，然后在需要时添加质询。</span><span class="sxs-lookup"><span data-stu-id="519ee-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="519ee-207">在添加质询之前检查响应代码。</span><span class="sxs-lookup"><span data-stu-id="519ee-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="519ee-208">如果响应为401，则大多数身份验证方案仅添加质询，如下所示。</span><span class="sxs-lookup"><span data-stu-id="519ee-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="519ee-209">但是，某些身份验证方案确实会向成功响应添加质询。</span><span class="sxs-lookup"><span data-stu-id="519ee-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="519ee-210">例如，请参阅[Negotiate](http://tools.ietf.org/html/rfc4559#section-5) （RFC 4559）。</span><span class="sxs-lookup"><span data-stu-id="519ee-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="519ee-211">给定 `AddChallengeOnUnauthorizedResult` 类， **ChallengeAsync**中的实际代码非常简单。</span><span class="sxs-lookup"><span data-stu-id="519ee-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="519ee-212">只需创建结果并将其附加到 `context.Result`。</span><span class="sxs-lookup"><span data-stu-id="519ee-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="519ee-213">注意：基本身份验证示例通过将此逻辑放在扩展方法中来对其进行抽象。</span><span class="sxs-lookup"><span data-stu-id="519ee-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="519ee-214">结合身份验证筛选器与主机级身份验证</span><span class="sxs-lookup"><span data-stu-id="519ee-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="519ee-215">"主机级身份验证" 是指主机（如 IIS）执行的身份验证，然后请求到达 Web API 框架。</span><span class="sxs-lookup"><span data-stu-id="519ee-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="519ee-216">通常情况下，你可能想要为应用程序的其余部分启用主机级身份验证，但为 Web API 控制器禁用主机级身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="519ee-217">例如，典型的方案是在主机级别启用窗体身份验证，但对 Web API 使用基于令牌的身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="519ee-218">若要禁用 Web API 管道内的主机级身份验证，请在配置中调用 `config.SuppressHostPrincipal()`。</span><span class="sxs-lookup"><span data-stu-id="519ee-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="519ee-219">这会导致 Web API 从进入 Web API 管道的任何请求中删除**IPrincipal** 。</span><span class="sxs-lookup"><span data-stu-id="519ee-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="519ee-220">实际上，它 &quot;&quot; 请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="519ee-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="519ee-221">其他资源</span><span class="sxs-lookup"><span data-stu-id="519ee-221">Additional Resources</span></span>

<span data-ttu-id="519ee-222">[ASP.NET Web API 安全筛选器](https://msdn.microsoft.com/magazine/dn781361.aspx)（MSDN 杂志）</span><span class="sxs-lookup"><span data-stu-id="519ee-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
