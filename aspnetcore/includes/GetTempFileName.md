---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165850"
---
<span data-ttu-id="1f7ee-101">**警告**:下面的代码使用`GetTempFileName`，该类会引发`IOException`如果超过 65535 个文件创建而不会删除以前的临时文件。</span><span class="sxs-lookup"><span data-stu-id="1f7ee-101">**Warning**: The following code uses `GetTempFileName`, which throws an `IOException` if more than 65535 files are created without deleting previous temporary files.</span></span> <span data-ttu-id="1f7ee-102">实际应用须删除临时文件或使用 `GetTempPath` 和 `GetRandomFileName` 创建临时文件名称。</span><span class="sxs-lookup"><span data-stu-id="1f7ee-102">A real app should either delete temporary files or use `GetTempPath` and `GetRandomFileName` to create temporary file names.</span></span> <span data-ttu-id="1f7ee-103">每个服务器限制为 65535 个文件，因此服务器上的其他应用可能已占用全部 65535 个文件。</span><span class="sxs-lookup"><span data-stu-id="1f7ee-103">The 65535 files limit is per server, so another app on the server can use up all 65535 files.</span></span> 
