---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188714"
---
> <span data-ttu-id="fbe86-101">如果应用使用 SQLite 作为其标识数据存储区，不支持一些命令。</span><span class="sxs-lookup"><span data-stu-id="fbe86-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="fbe86-102">由于数据库引擎中的限制`Alter`命令将引发以下异常：</span><span class="sxs-lookup"><span data-stu-id="fbe86-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="fbe86-103">"System.NotSupportedException:SQLite 不支持。 此迁移操作"</span><span class="sxs-lookup"><span data-stu-id="fbe86-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="fbe86-104">作为替代，若要更改的表在数据库上运行 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="fbe86-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
