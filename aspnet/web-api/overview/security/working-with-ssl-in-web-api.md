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
# <a name="working-with-ssl-in-web-api"></a>Working with SSL in Web API（在 Web API 中使用 SSL）

作者： [Mike Wasson](https://github.com/MikeWasson)

几种常见的身份验证方案不能通过纯 HTTP 进行保护。 尤其是，基本身份验证和窗体身份验证会发送未加密的凭据。 为安全，这些身份验证方案*必须*使用 SSL。 此外，SSL 客户端证书可用于对客户端进行身份验证。

## <a name="enabling-ssl-on-the-server"></a>在服务器上启用 SSL

若要在 IIS 7 或更高版本中设置 SSL：

- 创建或获取证书。 为了进行测试，你可以创建一个自签名证书。
- 添加 HTTPS 绑定。

有关详细信息，请参阅[如何在 IIS 7 上设置 SSL](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。

对于本地测试，可以从 Visual Studio IIS Express 中启用 SSL。 在属性窗口中，将**SSL 启用**为**True**。 请注意 " **SSL URL**" 的值;使用此 URL 来测试 HTTPS 连接。

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>在 Web API 控制器中强制实施 SSL

如果有 HTTPS 和 HTTP 绑定，则客户端仍可以使用 HTTP 访问站点。 可以允许通过 HTTP 使用某些资源，而其他资源则需要 SSL。 在这种情况下，请使用操作筛选器对受保护的资源要求 SSL。 以下代码演示了一个检查 SSL 的 Web API 身份验证筛选器：

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

将此筛选器添加到要求使用 SSL 的任何 Web API 操作：

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL 客户端证书

SSL 通过使用公钥基础结构证书提供身份验证。 服务器必须提供向客户端验证服务器的证书。 客户端向服务器提供证书不太常见，但这是对客户端进行身份验证的一种选择。 若要将客户端证书与 SSL 一起使用，你需要一种将签名证书分发给用户的方法。 对于许多应用程序类型来说，这并不是一个很好的用户体验，但在某些环境（例如，企业）中可能是可行的。

| 优点 | 缺点 |
| --- | --- |
| -证书凭据比用户名/密码更强。 -SSL 提供了一个完整的安全通道，其中包含身份验证、消息完整性和消息加密。 | -必须获取和管理 PKI 证书。 -客户端平台必须支持 SSL 客户端证书。 |

若要将 IIS 配置为接受客户端证书，请打开 IIS 管理器并执行以下步骤：

1. 单击树视图中的 "站点" 节点。
2. 双击中间窗格中的 " **SSL 设置**" 功能。
3. 在 "**客户端证书**" 下，选择以下选项之一： 

    - **接受**： IIS 将接受来自客户端的证书，但不需要证书。
    - **要求**：需要客户端证书。 （若要启用此选项，还必须选择 "需要 SSL"）

你还可以在 Applicationhost.config 文件中设置以下选项：

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

**SslNegotiateCert**标志表示 IIS 将接受来自客户端的证书，但不需要该证书（与 IIS 管理器中的 "接受" 选项等效）。 若要需要证书，请设置**SslRequireCert**标志。 若要进行测试，还可以在本地 applicationhost.config 中的 IIS Express 中设置这些选项。位于 "Documents\IISExpress\config" 中的配置文件。

### <a name="creating-a-client-certificate-for-testing"></a>创建用于测试的客户端证书

出于测试目的，可以使用[MakeCert](/windows/desktop/SecCrypto/makecert)创建客户端证书。 首先，创建一个测试根颁发机构：

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

Makecert 将提示你输入私钥的密码。

接下来，将证书添加到测试服务器的 "受信任的根证书颁发机构" 存储，如下所示：

1. 打开“MMC”。
2. 在 "**文件**" 下，选择 "**添加/删除管理单元**"。
3. 选择 "**计算机帐户**"。
4. 选择 "**本地计算机**" 并完成向导。
5. 在导航窗格下，展开 "受信任的根证书颁发机构" 节点。
6. 在 "**操作**" 菜单上，指向 "**所有任务**"，然后单击 "**导入**" 以启动 "证书导入向导"。
7. 浏览到证书文件 TempCA。
8. 单击 "**打开**"，然后单击 "**下一步**" 并完成向导。 （系统将提示你重新输入密码。）

现在创建由第一个证书签名的客户端证书：

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>在 Web API 中使用客户端证书

在服务器端，可以通过对请求消息调用[GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx)来获取客户端证书。 如果没有客户端证书，则此方法返回 null。 否则，它将返回**X509Certificate2**实例。 使用此对象可以从证书中获取信息，如颁发者和使用者。 然后，可以使用此信息进行身份验证和/或授权。

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
