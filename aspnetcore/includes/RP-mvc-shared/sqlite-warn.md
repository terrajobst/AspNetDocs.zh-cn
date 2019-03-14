---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048214"
---

> [!NOTE]
> <span data-ttu-id="4bca7-101">许多架构更改操作不受 EF Core SQLite 提供程序支持。</span><span class="sxs-lookup"><span data-stu-id="4bca7-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="4bca7-102">例如，支持添加列，但不支持删除列。</span><span class="sxs-lookup"><span data-stu-id="4bca7-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="4bca7-103">创建迁移以删除列，如果`ef migrations add`命令成功，但`ef database update`命令会失败。</span><span class="sxs-lookup"><span data-stu-id="4bca7-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="4bca7-104">其中某些限制可以通过手动编写迁移代码，以便执行表重新生成克服。</span><span class="sxs-lookup"><span data-stu-id="4bca7-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="4bca7-105">表重新生成涉及：</span><span class="sxs-lookup"><span data-stu-id="4bca7-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="4bca7-106">重命名现有表。</span><span class="sxs-lookup"><span data-stu-id="4bca7-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="4bca7-107">创建新表。</span><span class="sxs-lookup"><span data-stu-id="4bca7-107">Creating a new table.</span></span>
>* <span data-ttu-id="4bca7-108">将数据从旧表复制到新表。</span><span class="sxs-lookup"><span data-stu-id="4bca7-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="4bca7-109">删除旧表。</span><span class="sxs-lookup"><span data-stu-id="4bca7-109">Dropping the old table.</span></span>

<span data-ttu-id="4bca7-110">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="4bca7-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="4bca7-111">SQLite EF Core 数据库提供程序限制</span><span class="sxs-lookup"><span data-stu-id="4bca7-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="4bca7-112">自定义迁移代码</span><span class="sxs-lookup"><span data-stu-id="4bca7-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="4bca7-113">数据种子设定</span><span class="sxs-lookup"><span data-stu-id="4bca7-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)