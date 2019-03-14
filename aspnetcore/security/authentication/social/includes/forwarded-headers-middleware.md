---
ms.openlocfilehash: d7ef9b11af8ee11e4ec84404f8cdeb0b89384a3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57130445"
---
## <a name="forward-request-information-with-a-proxy-or-load-balancer"></a>转发请求使用代理的信息或负载均衡器

如果代理服务器或负载均衡器后面部署应用，原始请求信息的一些可能会转发到请求标头中的应用程序。 此信息通常包括安全请求方案 (`https`)，主机和客户端 IP 地址。 应用程序不会自动读取这些请求标头，以发现和使用原始请求信息。

在生成链接会影响与外部提供商的身份验证流中使用方案。 丢失的安全方案 (`https`) 生成不正确的不安全重定向 Url，应用程序。

使用转发头中间件可用于处理请求的应用提供的原始请求信息。

有关详细信息，请参阅 <xref:host-and-deploy/proxy-load-balancer>。
