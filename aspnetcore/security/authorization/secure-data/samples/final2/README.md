---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049104"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>如何生成/运行安全的用户数据示例

* 使用机密管理器工具设置密码：

  `dotnet user-secrets set SeedUserPW <pw>`

* 更新数据库：

    `dotnet ef database update`

* 在项目中启用 HTTPS
