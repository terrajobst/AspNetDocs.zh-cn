---
uid: signalr/overview/security/hub-authorization
title: SignalR 中心的身份验证和授权 |Microsoft Docs
author: bradygaster
description: 本主题介绍如何限制哪些用户或角色可以访问中心方法。 本主题中使用的软件版本 Visual Studio 2013 .NET 4.5 SignalR ve 。
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467510"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="82462-104">SignalR 中心身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="82462-104">Authentication and Authorization for SignalR Hubs</span></span>

<span data-ttu-id="82462-105">作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="82462-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="82462-106">本主题介绍如何限制哪些用户或角色可以访问中心方法。</span><span class="sxs-lookup"><span data-stu-id="82462-106">This topic describes how to restrict which users or roles can access hub methods.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="82462-107">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="82462-107">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="82462-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="82462-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="82462-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="82462-109">.NET 4.5</span></span>
> - <span data-ttu-id="82462-110">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="82462-110">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="82462-111">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="82462-111">Previous versions of this topic</span></span>
>
> <span data-ttu-id="82462-112">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="82462-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="82462-113">问题和注释</span><span class="sxs-lookup"><span data-stu-id="82462-113">Questions and comments</span></span>
>
> <span data-ttu-id="82462-114">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="82462-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="82462-115">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="82462-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="82462-116">概述</span><span class="sxs-lookup"><span data-stu-id="82462-116">Overview</span></span>

<span data-ttu-id="82462-117">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="82462-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="82462-118">授权属性</span><span class="sxs-lookup"><span data-stu-id="82462-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="82462-119">要求对所有中心进行身份验证</span><span class="sxs-lookup"><span data-stu-id="82462-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="82462-120">自定义授权</span><span class="sxs-lookup"><span data-stu-id="82462-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="82462-121">向客户端传递身份验证信息</span><span class="sxs-lookup"><span data-stu-id="82462-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="82462-122">.NET 客户端的身份验证选项</span><span class="sxs-lookup"><span data-stu-id="82462-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="82462-123">带有 Forms 身份验证的 Cookie</span><span class="sxs-lookup"><span data-stu-id="82462-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="82462-124">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="82462-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="82462-125">连接头</span><span class="sxs-lookup"><span data-stu-id="82462-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="82462-126">证书</span><span class="sxs-lookup"><span data-stu-id="82462-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="82462-127">授权属性</span><span class="sxs-lookup"><span data-stu-id="82462-127">Authorize attribute</span></span>

<span data-ttu-id="82462-128">SignalR 提供[授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性以指定哪些用户或角色有权访问集线器或方法。</span><span class="sxs-lookup"><span data-stu-id="82462-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="82462-129">此属性位于 `Microsoft.AspNet.SignalR` 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="82462-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="82462-130">将 `Authorize` 特性应用于中心中的集线器或特定方法。</span><span class="sxs-lookup"><span data-stu-id="82462-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="82462-131">将 `Authorize` 特性应用于 hub 类时，指定的授权要求将应用于中心中的所有方法。</span><span class="sxs-lookup"><span data-stu-id="82462-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="82462-132">本主题提供了你可以应用的不同类型的授权要求的示例。</span><span class="sxs-lookup"><span data-stu-id="82462-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="82462-133">如果没有 `Authorize` 属性，连接的客户端可以访问中心上的任何公共方法。</span><span class="sxs-lookup"><span data-stu-id="82462-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="82462-134">如果你在 web 应用程序中定义了名为 "Admin" 的角色，则可以指定只有该角色中的用户可以使用以下代码访问中心。</span><span class="sxs-lookup"><span data-stu-id="82462-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="82462-135">或者，你可以指定一个中心包含一个可供所有用户使用的方法，以及一个仅适用于经过身份验证的用户的第二种方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="82462-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="82462-136">以下示例解决了不同的授权方案：</span><span class="sxs-lookup"><span data-stu-id="82462-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="82462-137">`[Authorize]` –仅限经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="82462-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="82462-138">`[Authorize(Roles = "Admin,Manager")]` –仅指定角色中经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="82462-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="82462-139">`[Authorize(Users = "user1,user2")]` –只有具有指定用户名的经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="82462-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="82462-140">`[Authorize(RequireOutgoing=false)]` –只有经过身份验证的用户可以调用中心，但从服务器到客户端的调用不受授权限制，例如，当只有特定用户可以发送消息，但所有其他用户都可以接收消息时。</span><span class="sxs-lookup"><span data-stu-id="82462-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="82462-141">RequireOutgoing 属性只能应用于整个中心，而不能应用于中心内的个人方法。</span><span class="sxs-lookup"><span data-stu-id="82462-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="82462-142">当 RequireOutgoing 未设置为 false 时，仅从服务器中调用满足授权要求的用户。</span><span class="sxs-lookup"><span data-stu-id="82462-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="82462-143">要求对所有中心进行身份验证</span><span class="sxs-lookup"><span data-stu-id="82462-143">Require authentication for all hubs</span></span>

<span data-ttu-id="82462-144">在应用程序启动时，可以通过调用[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)方法，要求对应用程序中的所有中心和集线器方法进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="82462-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="82462-145">如果有多个中心并想要为所有中心强制实施身份验证要求，则可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="82462-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="82462-146">利用此方法，无法指定角色、用户或传出授权的要求。</span><span class="sxs-lookup"><span data-stu-id="82462-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="82462-147">只能指定仅限经过身份验证的用户访问集线器方法。</span><span class="sxs-lookup"><span data-stu-id="82462-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="82462-148">不过，你仍然可以将授权属性应用于中心或方法，以指定其他要求。</span><span class="sxs-lookup"><span data-stu-id="82462-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="82462-149">在特性中指定的任何要求将添加到身份验证的基本要求。</span><span class="sxs-lookup"><span data-stu-id="82462-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="82462-150">以下示例显示了一个启动文件，该文件将所有集线器方法限制为已通过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="82462-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="82462-151">如果在处理 SignalR 请求后调用 `RequireAuthentication()` 方法，SignalR 将引发 `InvalidOperationException` 异常。</span><span class="sxs-lookup"><span data-stu-id="82462-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="82462-152">SignalR 会引发此异常，因为在调用管道后，不能将模块添加到 HubPipeline 中。</span><span class="sxs-lookup"><span data-stu-id="82462-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="82462-153">前面的示例演示如何在 `Configuration` 方法中调用 `RequireAuthentication` 方法，该方法在处理第一个请求之前执行一次。</span><span class="sxs-lookup"><span data-stu-id="82462-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="82462-154">自定义授权</span><span class="sxs-lookup"><span data-stu-id="82462-154">Customized authorization</span></span>

<span data-ttu-id="82462-155">如果需要自定义如何确定授权，可以创建一个派生自 `AuthorizeAttribute` 的类，并重写[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="82462-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="82462-156">对于每个请求，SignalR 将调用此方法来确定用户是否有权完成该请求。</span><span class="sxs-lookup"><span data-stu-id="82462-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="82462-157">在重写的方法中，为授权方案提供必要的逻辑。</span><span class="sxs-lookup"><span data-stu-id="82462-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="82462-158">下面的示例演示如何通过基于声明的标识来强制执行授权。</span><span class="sxs-lookup"><span data-stu-id="82462-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="82462-159">向客户端传递身份验证信息</span><span class="sxs-lookup"><span data-stu-id="82462-159">Pass authentication information to clients</span></span>

<span data-ttu-id="82462-160">可能需要在客户端上运行的代码中使用身份验证信息。</span><span class="sxs-lookup"><span data-stu-id="82462-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="82462-161">在客户端上调用方法时传递所需的信息。</span><span class="sxs-lookup"><span data-stu-id="82462-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="82462-162">例如，聊天应用程序方法可以作为参数传递用户的用户名称，如下所示。</span><span class="sxs-lookup"><span data-stu-id="82462-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="82462-163">或者，你可以创建一个对象来表示身份验证信息，并将该对象作为参数传递，如下所示。</span><span class="sxs-lookup"><span data-stu-id="82462-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="82462-164">永远不要将一个客户端的连接 id 传递到其他客户端，因为恶意用户可以使用它来模拟该客户端的请求。</span><span class="sxs-lookup"><span data-stu-id="82462-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="82462-165">.NET 客户端的身份验证选项</span><span class="sxs-lookup"><span data-stu-id="82462-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="82462-166">如果你有一个 .NET 客户端（如控制台应用程序），该应用程序与限制为已通过身份验证的用户的集线器进行交互，则可以通过 cookie、连接头或证书传递身份验证凭据。</span><span class="sxs-lookup"><span data-stu-id="82462-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="82462-167">本节中的示例演示如何使用不同的方法对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="82462-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="82462-168">它们不是功能齐全的 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="82462-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="82462-169">有关包含 SignalR 的 .NET 客户端的详细信息，请参阅[中心 API 指南-.Net 客户端](../guide-to-the-api/hubs-api-guide-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="82462-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="82462-170">Cookie</span><span class="sxs-lookup"><span data-stu-id="82462-170">Cookie</span></span>

<span data-ttu-id="82462-171">当你的 .NET 客户端与使用 ASP.NET Forms 身份验证的集线器进行交互时，你将需要在连接上手动设置身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="82462-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="82462-172">将该 cookie 添加到[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)对象上的 `CookieContainer` 属性。</span><span class="sxs-lookup"><span data-stu-id="82462-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="82462-173">下面的示例演示了一个控制台应用程序，该应用程序从网页中检索身份验证 cookie 并将该 cookie 添加到连接。</span><span class="sxs-lookup"><span data-stu-id="82462-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="82462-174">控制台应用会将凭据发布到<strong>www.contoso.com/RemoteLogin</strong> ，这可能表示包含以下代码隐藏文件的空页面。</span><span class="sxs-lookup"><span data-stu-id="82462-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="82462-175">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="82462-175">Windows authentication</span></span>

<span data-ttu-id="82462-176">使用 Windows 身份验证时，可以通过使用[DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)属性传递当前用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="82462-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="82462-177">将连接的凭据设置为 DefaultCredentials 的值。</span><span class="sxs-lookup"><span data-stu-id="82462-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="82462-178">连接头</span><span class="sxs-lookup"><span data-stu-id="82462-178">Connection header</span></span>

<span data-ttu-id="82462-179">如果你的应用程序未使用 cookie，你可以将用户信息传递到连接标头。</span><span class="sxs-lookup"><span data-stu-id="82462-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="82462-180">例如，可以在 connection 标头中传递令牌。</span><span class="sxs-lookup"><span data-stu-id="82462-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="82462-181">然后，在中心中验证用户的令牌。</span><span class="sxs-lookup"><span data-stu-id="82462-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="82462-182">证书</span><span class="sxs-lookup"><span data-stu-id="82462-182">Certificate</span></span>

<span data-ttu-id="82462-183">可以传递客户端证书来验证用户。</span><span class="sxs-lookup"><span data-stu-id="82462-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="82462-184">在创建连接时添加证书。</span><span class="sxs-lookup"><span data-stu-id="82462-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="82462-185">下面的示例演示如何将客户端证书添加到连接;它不会显示完整的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="82462-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="82462-186">它使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)类，该类提供多种不同的方法来创建证书。</span><span class="sxs-lookup"><span data-stu-id="82462-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
