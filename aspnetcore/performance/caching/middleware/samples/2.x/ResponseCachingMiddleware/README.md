---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062714"
---
# <a name="aspnet-core-response-caching-sample"></a>ASP.NET Core 响应缓存示例

本示例演示使用 ASP.NET Core [响应缓存中间件](https://docs.microsoft.com/aspnet/core/performance/caching/middleware)。

应用的响应与它的索引页，其中包括`Cache-Control`标头，若要配置的缓存行为。 应用程序还会设置`Vary`标头来配置缓存，以提供响应才`Accept-Encoding`后续请求标头中的匹配的原始请求。

运行示例时，是从缓存存储和缓存最多 10 秒时提供的索引页。
