---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037394"
---
生成的标识数据库代码需要[Entity Framework Core 迁移](/ef/core/managing-schemas/migrations/)。 创建迁移并更新数据库。 例如，运行以下命令：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

在 Visual Studio**程序包管理器控制台**:

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

"CreateIdentitySchema"name 参数为`Add-Migration`是任意的命令。 `"CreateIdentitySchema"` 介绍迁移。
