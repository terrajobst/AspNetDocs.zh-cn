---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165850"
---
**警告**:下面的代码使用`GetTempFileName`，该类会引发`IOException`如果超过 65535 个文件创建而不会删除以前的临时文件。 实际应用须删除临时文件或使用 `GetTempPath` 和 `GetRandomFileName` 创建临时文件名称。 每个服务器限制为 65535 个文件，因此服务器上的其他应用可能已占用全部 65535 个文件。 
