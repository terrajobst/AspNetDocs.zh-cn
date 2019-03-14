---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048214"
---

> [!NOTE]
> 许多架构更改操作不受 EF Core SQLite 提供程序支持。 例如，支持添加列，但不支持删除列。 创建迁移以删除列，如果`ef migrations add`命令成功，但`ef database update`命令会失败。 其中某些限制可以通过手动编写迁移代码，以便执行表重新生成克服。 表重新生成涉及：

>* 重命名现有表。
>* 创建新表。
>* 将数据从旧表复制到新表。
>* 删除旧表。

有关更多信息，请参见以下资源：
> * [SQLite EF Core 数据库提供程序限制](/ef/core/providers/sqlite/limitations)
> * [自定义迁移代码](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [数据种子设定](/ef/core/modeling/data-seeding)