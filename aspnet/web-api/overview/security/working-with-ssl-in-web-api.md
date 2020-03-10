---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: 在 Web API 中使用 SSL |Microsoft Docs
author: MikeWasson
description: 演示如何将 SSL 与 ASP.NET Web API （包括使用 SSL 客户端证书）结合使用。
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484412"
---
# <a name="working-with-ssl-in-web-api"></a><span data-ttu-id="393e3-103">Working with SSL in Web API（在 Web API 中使用 SSL）</span><span class="sxs-lookup"><span data-stu-id="393e3-103">Working with SSL in Web API</span></span>

<span data-ttu-id="393e3-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="393e3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="393e3-105">几种常见的身份验证方案不能通过纯 HTTP 进行保护。</span><span class="sxs-lookup"><span data-stu-id="393e3-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="393e3-106">尤其是，基本身份验证和窗体身份验证会发送未加密的凭据。</span><span class="sxs-lookup"><span data-stu-id="393e3-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="393e3-107">为安全，这些身份验证方案*必须*使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="393e3-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="393e3-108">此外，SSL 客户端证书可用于对客户端进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="393e3-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="393e3-109">在服务器上启用 SSL</span><span class="sxs-lookup"><span data-stu-id="393e3-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="393e3-110">若要在 IIS 7 或更高版本中设置 SSL：</span><span class="sxs-lookup"><span data-stu-id="393e3-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="393e3-111">创建或获取证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-111">Create or get a certificate.</span></span> <span data-ttu-id="393e3-112">为了进行测试，你可以创建一个自签名证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="393e3-113">添加 HTTPS 绑定。</span><span class="sxs-lookup"><span data-stu-id="393e3-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="393e3-114">有关详细信息，请参阅[如何在 IIS 7 上设置 SSL](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="393e3-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="393e3-115">对于本地测试，可以从 Visual Studio IIS Express 中启用 SSL。</span><span class="sxs-lookup"><span data-stu-id="393e3-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="393e3-116">在属性窗口中，将**SSL 启用**为**True**。</span><span class="sxs-lookup"><span data-stu-id="393e3-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="393e3-117">请注意 " **SSL URL**" 的值;使用此 URL 来测试 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="393e3-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="393e3-118">在 Web API 控制器中强制实施 SSL</span><span class="sxs-lookup"><span data-stu-id="393e3-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="393e3-119">如果有 HTTPS 和 HTTP 绑定，则客户端仍可以使用 HTTP 访问站点。</span><span class="sxs-lookup"><span data-stu-id="393e3-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="393e3-120">可以允许通过 HTTP 使用某些资源，而其他资源则需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="393e3-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="393e3-121">在这种情况下，请使用操作筛选器对受保护的资源要求 SSL。</span><span class="sxs-lookup"><span data-stu-id="393e3-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="393e3-122">以下代码演示了一个检查 SSL 的 Web API 身份验证筛选器：</span><span class="sxs-lookup"><span data-stu-id="393e3-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="393e3-123">将此筛选器添加到要求使用 SSL 的任何 Web API 操作：</span><span class="sxs-lookup"><span data-stu-id="393e3-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="393e3-124">SSL 客户端证书</span><span class="sxs-lookup"><span data-stu-id="393e3-124">SSL Client Certificates</span></span>

<span data-ttu-id="393e3-125">SSL 通过使用公钥基础结构证书提供身份验证。</span><span class="sxs-lookup"><span data-stu-id="393e3-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="393e3-126">服务器必须提供向客户端验证服务器的证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="393e3-127">客户端向服务器提供证书不太常见，但这是对客户端进行身份验证的一种选择。</span><span class="sxs-lookup"><span data-stu-id="393e3-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="393e3-128">若要将客户端证书与 SSL 一起使用，你需要一种将签名证书分发给用户的方法。</span><span class="sxs-lookup"><span data-stu-id="393e3-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="393e3-129">对于许多应用程序类型来说，这并不是一个很好的用户体验，但在某些环境（例如，企业）中可能是可行的。</span><span class="sxs-lookup"><span data-stu-id="393e3-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="393e3-130">优点</span><span class="sxs-lookup"><span data-stu-id="393e3-130">Advantages</span></span> | <span data-ttu-id="393e3-131">缺点</span><span class="sxs-lookup"><span data-stu-id="393e3-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="393e3-132">-证书凭据比用户名/密码更强。</span><span class="sxs-lookup"><span data-stu-id="393e3-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="393e3-133">-SSL 提供了一个完整的安全通道，其中包含身份验证、消息完整性和消息加密。</span><span class="sxs-lookup"><span data-stu-id="393e3-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="393e3-134">-必须获取和管理 PKI 证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="393e3-135">-客户端平台必须支持 SSL 客户端证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="393e3-136">若要将 IIS 配置为接受客户端证书，请打开 IIS 管理器并执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="393e3-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="393e3-137">单击树视图中的 "站点" 节点。</span><span class="sxs-lookup"><span data-stu-id="393e3-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="393e3-138">双击中间窗格中的 " **SSL 设置**" 功能。</span><span class="sxs-lookup"><span data-stu-id="393e3-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="393e3-139">在 "**客户端证书**" 下，选择以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="393e3-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="393e3-140">**接受**： IIS 将接受来自客户端的证书，但不需要证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="393e3-141">**要求**：需要客户端证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="393e3-142">（若要启用此选项，还必须选择 "需要 SSL"）</span><span class="sxs-lookup"><span data-stu-id="393e3-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="393e3-143">你还可以在 Applicationhost.config 文件中设置以下选项：</span><span class="sxs-lookup"><span data-stu-id="393e3-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="393e3-144">**SslNegotiateCert**标志表示 IIS 将接受来自客户端的证书，但不需要该证书（与 IIS 管理器中的 "接受" 选项等效）。</span><span class="sxs-lookup"><span data-stu-id="393e3-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="393e3-145">若要需要证书，请设置**SslRequireCert**标志。</span><span class="sxs-lookup"><span data-stu-id="393e3-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="393e3-146">若要进行测试，还可以在本地 applicationhost.config 中的 IIS Express 中设置这些选项。位于 "Documents\IISExpress\config" 中的配置文件。</span><span class="sxs-lookup"><span data-stu-id="393e3-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="393e3-147">创建用于测试的客户端证书</span><span class="sxs-lookup"><span data-stu-id="393e3-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="393e3-148">出于测试目的，可以使用[MakeCert](/windows/desktop/SecCrypto/makecert)创建客户端证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-148">For testing purposes, you can use [MakeCert.exe](/windows/desktop/SecCrypto/makecert) to create a client certificate.</span></span> <span data-ttu-id="393e3-149">首先，创建一个测试根颁发机构：</span><span class="sxs-lookup"><span data-stu-id="393e3-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="393e3-150">Makecert 将提示你输入私钥的密码。</span><span class="sxs-lookup"><span data-stu-id="393e3-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="393e3-151">接下来，将证书添加到测试服务器的 "受信任的根证书颁发机构" 存储，如下所示：</span><span class="sxs-lookup"><span data-stu-id="393e3-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="393e3-152">打开“MMC”。</span><span class="sxs-lookup"><span data-stu-id="393e3-152">Open MMC.</span></span>
2. <span data-ttu-id="393e3-153">在 "**文件**" 下，选择 "**添加/删除管理单元**"。</span><span class="sxs-lookup"><span data-stu-id="393e3-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="393e3-154">选择 "**计算机帐户**"。</span><span class="sxs-lookup"><span data-stu-id="393e3-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="393e3-155">选择 "**本地计算机**" 并完成向导。</span><span class="sxs-lookup"><span data-stu-id="393e3-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="393e3-156">在导航窗格下，展开 "受信任的根证书颁发机构" 节点。</span><span class="sxs-lookup"><span data-stu-id="393e3-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="393e3-157">在 "**操作**" 菜单上，指向 "**所有任务**"，然后单击 "**导入**" 以启动 "证书导入向导"。</span><span class="sxs-lookup"><span data-stu-id="393e3-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="393e3-158">浏览到证书文件 TempCA。</span><span class="sxs-lookup"><span data-stu-id="393e3-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="393e3-159">单击 "**打开**"，然后单击 "**下一步**" 并完成向导。</span><span class="sxs-lookup"><span data-stu-id="393e3-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="393e3-160">（系统将提示你重新输入密码。）</span><span class="sxs-lookup"><span data-stu-id="393e3-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="393e3-161">现在创建由第一个证书签名的客户端证书：</span><span class="sxs-lookup"><span data-stu-id="393e3-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="393e3-162">在 Web API 中使用客户端证书</span><span class="sxs-lookup"><span data-stu-id="393e3-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="393e3-163">在服务器端，可以通过对请求消息调用[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)来获取客户端证书。</span><span class="sxs-lookup"><span data-stu-id="393e3-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="393e3-164">如果没有客户端证书，则此方法返回 null。</span><span class="sxs-lookup"><span data-stu-id="393e3-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="393e3-165">否则，它将返回**X509Certificate2**实例。</span><span class="sxs-lookup"><span data-stu-id="393e3-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="393e3-166">使用此对象可以从证书中获取信息，如颁发者和使用者。</span><span class="sxs-lookup"><span data-stu-id="393e3-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="393e3-167">然后，可以使用此信息进行身份验证和/或授权。</span><span class="sxs-lookup"><span data-stu-id="393e3-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
