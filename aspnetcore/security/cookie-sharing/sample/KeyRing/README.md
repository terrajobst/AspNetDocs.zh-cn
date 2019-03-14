---
ms.openlocfilehash: 17ae8088e2e570628883ea5f8d71e093e6ed7cc8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043024"
---
# <a name="data-protection-key-folder"></a><span data-ttu-id="50863-101">数据保护密钥文件夹</span><span class="sxs-lookup"><span data-stu-id="50863-101">Data protection key folder</span></span>

<span data-ttu-id="50863-102">此文件是一个占位符，以创建一个共享的文件夹用于数据保护密钥。</span><span class="sxs-lookup"><span data-stu-id="50863-102">This file is a placeholder to create a shared folder for data protection keys.</span></span>

<span data-ttu-id="50863-103">在生产部署中，将开发根和永远不会在签入此目录中的文件之外的项置于源代码管理。</span><span class="sxs-lookup"><span data-stu-id="50863-103">In a production deployment, place the keys outside of the development root and never check-in files in this directory into source control.</span></span> <span data-ttu-id="50863-104">保护使用 DPAPI 或 x509 证书文件中的数据保护密钥。</span><span class="sxs-lookup"><span data-stu-id="50863-104">Protect data protection keys in the files with DPAPI or an X509Certificate.</span></span>

<span data-ttu-id="50863-105">请参阅[ASP.NET Core 中的数据保护：使用者 Api、 配置、 扩展性 Api 和实现](https://docs.microsoft.com/aspnet/core/security/data-protection/)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="50863-105">See [Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation](https://docs.microsoft.com/aspnet/core/security/data-protection/) for more information.</span></span>
