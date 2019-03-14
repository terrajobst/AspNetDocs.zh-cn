---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188714"
---
> 如果应用使用 SQLite 作为其标识数据存储区，不支持一些命令。 由于数据库引擎中的限制`Alter`命令将引发以下异常：
>
> "System.NotSupportedException:SQLite 不支持。 此迁移操作" 
>
> 作为替代，若要更改的表在数据库上运行 Code First 迁移。
