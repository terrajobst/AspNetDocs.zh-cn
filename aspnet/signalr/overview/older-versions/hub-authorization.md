---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR 中心的身份验证和授权（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本主题介绍如何限制哪些用户或角色可以访问中心方法。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450038"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="9487d-103">SignalR 中心身份验证和授权 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="9487d-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="9487d-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9487d-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="9487d-105">本主题介绍如何限制哪些用户或角色可以访问中心方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="9487d-106">概述</span><span class="sxs-lookup"><span data-stu-id="9487d-106">Overview</span></span>

<span data-ttu-id="9487d-107">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="9487d-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="9487d-108">授权属性</span><span class="sxs-lookup"><span data-stu-id="9487d-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="9487d-109">要求对所有中心进行身份验证</span><span class="sxs-lookup"><span data-stu-id="9487d-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="9487d-110">自定义授权</span><span class="sxs-lookup"><span data-stu-id="9487d-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="9487d-111">向客户端传递身份验证信息</span><span class="sxs-lookup"><span data-stu-id="9487d-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="9487d-112">.NET 客户端的身份验证选项</span><span class="sxs-lookup"><span data-stu-id="9487d-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="9487d-113">带有 Forms 身份验证的 Cookie</span><span class="sxs-lookup"><span data-stu-id="9487d-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="9487d-114">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="9487d-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="9487d-115">连接头</span><span class="sxs-lookup"><span data-stu-id="9487d-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="9487d-116">证书</span><span class="sxs-lookup"><span data-stu-id="9487d-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="9487d-117">授权属性</span><span class="sxs-lookup"><span data-stu-id="9487d-117">Authorize attribute</span></span>

<span data-ttu-id="9487d-118">SignalR 提供[授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性以指定哪些用户或角色有权访问集线器或方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="9487d-119">此属性位于 `Microsoft.AspNet.SignalR` 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="9487d-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="9487d-120">将 `Authorize` 特性应用于中心中的集线器或特定方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="9487d-121">将 `Authorize` 特性应用于 hub 类时，指定的授权要求将应用于中心中的所有方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="9487d-122">下面显示了你可以应用的不同类型的授权要求。</span><span class="sxs-lookup"><span data-stu-id="9487d-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="9487d-123">如果没有 `Authorize` 属性，则中心上的所有公共方法都可用于连接到集线器的客户端。</span><span class="sxs-lookup"><span data-stu-id="9487d-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="9487d-124">如果你在 web 应用程序中定义了名为 "Admin" 的角色，则可以指定只有该角色中的用户可以使用以下代码访问中心。</span><span class="sxs-lookup"><span data-stu-id="9487d-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="9487d-125">或者，你可以指定一个中心包含一个可供所有用户使用的方法，以及一个仅适用于经过身份验证的用户的第二种方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9487d-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="9487d-126">以下示例解决了不同的授权方案：</span><span class="sxs-lookup"><span data-stu-id="9487d-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="9487d-127">`[Authorize]` –仅限经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9487d-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="9487d-128">`[Authorize(Roles = "Admin,Manager")]` –仅指定角色中经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9487d-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="9487d-129">`[Authorize(Users = "user1,user2")]` –只有具有指定用户名的经过身份验证的用户</span><span class="sxs-lookup"><span data-stu-id="9487d-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="9487d-130">`[Authorize(RequireOutgoing=false)]` –只有经过身份验证的用户可以调用中心，但从服务器到客户端的调用不受授权限制，例如，当只有特定用户可以发送消息，但所有其他用户都可以接收消息时。</span><span class="sxs-lookup"><span data-stu-id="9487d-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="9487d-131">RequireOutgoing 属性只能应用于整个中心，而不能应用于中心内的个人方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="9487d-132">当 RequireOutgoing 未设置为 false 时，仅从服务器中调用满足授权要求的用户。</span><span class="sxs-lookup"><span data-stu-id="9487d-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="9487d-133">要求对所有中心进行身份验证</span><span class="sxs-lookup"><span data-stu-id="9487d-133">Require authentication for all hubs</span></span>

<span data-ttu-id="9487d-134">在应用程序启动时，可以通过调用[RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx)方法，要求对应用程序中的所有中心和集线器方法进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9487d-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="9487d-135">如果有多个中心并想要为所有中心强制实施身份验证要求，则可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="9487d-136">利用此方法，无法指定角色、用户或传出授权。</span><span class="sxs-lookup"><span data-stu-id="9487d-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="9487d-137">只能指定仅限经过身份验证的用户访问集线器方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="9487d-138">不过，你仍然可以将授权属性应用于中心或方法，以指定其他要求。</span><span class="sxs-lookup"><span data-stu-id="9487d-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="9487d-139">除了身份验证的基本要求外，还会应用在特性中指定的任何要求。</span><span class="sxs-lookup"><span data-stu-id="9487d-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="9487d-140">下面的示例显示了一个 Global.asa 文件，该文件将所有集线器方法限制为已通过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="9487d-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="9487d-141">如果在处理 SignalR 请求后调用 `RequireAuthentication()` 方法，SignalR 将引发 `InvalidOperationException` 异常。</span><span class="sxs-lookup"><span data-stu-id="9487d-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="9487d-142">引发此异常的原因是，在调用管道后，不能将模块添加到 HubPipeline 中。</span><span class="sxs-lookup"><span data-stu-id="9487d-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="9487d-143">前面的示例演示如何在 `Application_Start` 方法中调用 `RequireAuthentication` 方法，该方法在处理第一个请求之前执行一次。</span><span class="sxs-lookup"><span data-stu-id="9487d-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="9487d-144">自定义授权</span><span class="sxs-lookup"><span data-stu-id="9487d-144">Customized authorization</span></span>

<span data-ttu-id="9487d-145">如果需要自定义如何确定授权，可以创建一个派生自 `AuthorizeAttribute` 的类，并重写[UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="9487d-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="9487d-146">为每个请求调用此方法，以确定用户是否有权完成该请求。</span><span class="sxs-lookup"><span data-stu-id="9487d-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="9487d-147">在重写的方法中，为授权方案提供必要的逻辑。</span><span class="sxs-lookup"><span data-stu-id="9487d-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="9487d-148">下面的示例演示如何通过基于声明的标识来强制执行授权。</span><span class="sxs-lookup"><span data-stu-id="9487d-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="9487d-149">向客户端传递身份验证信息</span><span class="sxs-lookup"><span data-stu-id="9487d-149">Pass authentication information to clients</span></span>

<span data-ttu-id="9487d-150">可能需要在客户端上运行的代码中使用身份验证信息。</span><span class="sxs-lookup"><span data-stu-id="9487d-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="9487d-151">在客户端上调用方法时传递所需的信息。</span><span class="sxs-lookup"><span data-stu-id="9487d-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="9487d-152">例如，聊天应用程序方法可以作为参数传递用户的用户名称，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9487d-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="9487d-153">或者，你可以创建一个对象来表示身份验证信息，并将该对象作为参数传递，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9487d-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="9487d-154">永远不要将一个客户端的连接 id 传递到其他客户端，因为恶意用户可以使用它来模拟该客户端的请求。</span><span class="sxs-lookup"><span data-stu-id="9487d-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="9487d-155">.NET 客户端的身份验证选项</span><span class="sxs-lookup"><span data-stu-id="9487d-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="9487d-156">如果你有一个 .NET 客户端（如控制台应用程序），该应用程序与限制为已通过身份验证的用户的集线器进行交互，则可以通过 cookie、连接头或证书传递身份验证凭据。</span><span class="sxs-lookup"><span data-stu-id="9487d-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="9487d-157">本节中的示例演示如何使用不同的方法对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9487d-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="9487d-158">它们不是功能齐全的 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9487d-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="9487d-159">有关包含 SignalR 的 .NET 客户端的详细信息，请参阅[中心 API 指南-.Net 客户端](../guide-to-the-api/hubs-api-guide-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="9487d-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="9487d-160">Cookie</span><span class="sxs-lookup"><span data-stu-id="9487d-160">Cookie</span></span>

<span data-ttu-id="9487d-161">当你的 .NET 客户端与使用 ASP.NET Forms 身份验证的集线器进行交互时，你将需要在连接上手动设置身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="9487d-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="9487d-162">将该 cookie 添加到[HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx)对象上的 `CookieContainer` 属性。</span><span class="sxs-lookup"><span data-stu-id="9487d-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="9487d-163">下面的示例演示了一个控制台应用程序，该应用程序从网页中检索身份验证 cookie 并将该 cookie 添加到连接。</span><span class="sxs-lookup"><span data-stu-id="9487d-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="9487d-164">示例中的 URL `https://www.contoso.com/RemoteLogin` 指向需要创建的网页。</span><span class="sxs-lookup"><span data-stu-id="9487d-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="9487d-165">该页将检索已发布的用户名和密码，并尝试用凭据登录用户。</span><span class="sxs-lookup"><span data-stu-id="9487d-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="9487d-166">控制台应用会将凭据发布到 www.contoso.com/RemoteLogin，这可能表示包含以下代码隐藏文件的空页面。</span><span class="sxs-lookup"><span data-stu-id="9487d-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="9487d-167">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="9487d-167">Windows authentication</span></span>

<span data-ttu-id="9487d-168">使用 Windows 身份验证时，可以通过使用[DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx)属性传递当前用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="9487d-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="9487d-169">将连接的凭据设置为 DefaultCredentials 的值。</span><span class="sxs-lookup"><span data-stu-id="9487d-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="9487d-170">连接头</span><span class="sxs-lookup"><span data-stu-id="9487d-170">Connection header</span></span>

<span data-ttu-id="9487d-171">如果你的应用程序未使用 cookie，你可以将用户信息传递到连接标头。</span><span class="sxs-lookup"><span data-stu-id="9487d-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="9487d-172">例如，可以在 connection 标头中传递令牌。</span><span class="sxs-lookup"><span data-stu-id="9487d-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="9487d-173">然后，在中心中验证用户的令牌。</span><span class="sxs-lookup"><span data-stu-id="9487d-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="9487d-174">证书</span><span class="sxs-lookup"><span data-stu-id="9487d-174">Certificate</span></span>

<span data-ttu-id="9487d-175">可以传递客户端证书来验证用户。</span><span class="sxs-lookup"><span data-stu-id="9487d-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="9487d-176">在创建连接时添加证书。</span><span class="sxs-lookup"><span data-stu-id="9487d-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="9487d-177">下面的示例演示如何将客户端证书添加到连接;它不会显示完整的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="9487d-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="9487d-178">它使用[X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx)类，该类提供多种不同的方法来创建证书。</span><span class="sxs-lookup"><span data-stu-id="9487d-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
