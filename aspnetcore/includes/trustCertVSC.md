---
ms.openlocfilehash: 476580d4bc2435f73ef37c5344ab7fea4b67b9b8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032494"
---
<span data-ttu-id="d1d8f-101">通过运行以下命令来信任 HTTPS 开发证书：</span><span class="sxs-lookup"><span data-stu-id="d1d8f-101">Trust the HTTPS development certificate by running the following command:</span></span>

```console
dotnet dev-certs https --trust
```

<span data-ttu-id="d1d8f-102">以上命令会显示以下对话：</span><span class="sxs-lookup"><span data-stu-id="d1d8f-102">The preceding command displays the following dialog:</span></span>

![安全警告对话](~/getting-started/_static/cert.png)

<span data-ttu-id="d1d8f-104">如果你同意信任开发证书，请选择“是”。</span><span class="sxs-lookup"><span data-stu-id="d1d8f-104">Select **Yes** if you agree to trust the development certificate.</span></span>

<span data-ttu-id="d1d8f-105">有关详细信息，请参阅[信任 ASP.NET Core HTTPS 开发证书](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos)。</span><span class="sxs-lookup"><span data-stu-id="d1d8f-105">See [Trust the ASP.NET Core HTTPS development certificate](xref:security/enforcing-ssl#trust-the-aspnet-core-https-development-certificate-on-windows-and-macos) for more information.</span></span>