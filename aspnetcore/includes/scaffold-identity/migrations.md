---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037394"
---
<span data-ttu-id="7fd6b-101">生成的标识数据库代码需要[Entity Framework Core 迁移](/ef/core/managing-schemas/migrations/)。</span><span class="sxs-lookup"><span data-stu-id="7fd6b-101">The generated Identity database code requires [Entity Framework Core Migrations](/ef/core/managing-schemas/migrations/).</span></span> <span data-ttu-id="7fd6b-102">创建迁移并更新数据库。</span><span class="sxs-lookup"><span data-stu-id="7fd6b-102">Create a migration and update the database.</span></span> <span data-ttu-id="7fd6b-103">例如，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7fd6b-103">For example, run the following commands:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7fd6b-104">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7fd6b-104">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="7fd6b-105">在 Visual Studio**程序包管理器控制台**:</span><span class="sxs-lookup"><span data-stu-id="7fd6b-105">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7fd6b-106">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="7fd6b-106">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

<span data-ttu-id="7fd6b-107">"CreateIdentitySchema"name 参数为`Add-Migration`是任意的命令。</span><span class="sxs-lookup"><span data-stu-id="7fd6b-107">The "CreateIdentitySchema" name parameter for the `Add-Migration` command is arbitrary.</span></span> <span data-ttu-id="7fd6b-108">`"CreateIdentitySchema"` 介绍迁移。</span><span class="sxs-lookup"><span data-stu-id="7fd6b-108">`"CreateIdentitySchema"` describes the migration.</span></span>
