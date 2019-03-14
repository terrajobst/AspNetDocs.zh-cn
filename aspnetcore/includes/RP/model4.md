---
ms.openlocfilehash: 5ed24cd8a7e880a496d0c0295f7c1fb07f0e1032
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035984"
---
<span data-ttu-id="02a75-101">下表详细说明了 ASP.NET Core 代码生成器参数：</span><span class="sxs-lookup"><span data-stu-id="02a75-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="02a75-102">参数</span><span class="sxs-lookup"><span data-stu-id="02a75-102">Parameter</span></span>               | <span data-ttu-id="02a75-103">描述</span><span class="sxs-lookup"><span data-stu-id="02a75-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="02a75-104">-m</span><span class="sxs-lookup"><span data-stu-id="02a75-104">-m</span></span>  | <span data-ttu-id="02a75-105">模型的名称。</span><span class="sxs-lookup"><span data-stu-id="02a75-105">The name of the model.</span></span> |
| <span data-ttu-id="02a75-106">-dc</span><span class="sxs-lookup"><span data-stu-id="02a75-106">-dc</span></span>  | <span data-ttu-id="02a75-107">要使用的 `DbContext` 类。</span><span class="sxs-lookup"><span data-stu-id="02a75-107">The `DbContext` class to use.</span></span> |
| <span data-ttu-id="02a75-108">-udl</span><span class="sxs-lookup"><span data-stu-id="02a75-108">-udl</span></span> | <span data-ttu-id="02a75-109">使用默认布局。</span><span class="sxs-lookup"><span data-stu-id="02a75-109">Use the default layout.</span></span> |
| <span data-ttu-id="02a75-110">-outDir</span><span class="sxs-lookup"><span data-stu-id="02a75-110">-outDir</span></span> | <span data-ttu-id="02a75-111">用于创建视图的相对输出文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="02a75-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="02a75-112">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="02a75-112">--referenceScriptLibraries</span></span> | <span data-ttu-id="02a75-113">向“编辑”和“创建”页面添加 `_ValidationScriptsPartial`</span><span class="sxs-lookup"><span data-stu-id="02a75-113">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="02a75-114">使用 `h` 开关获取 `aspnet-codegenerator razorpage` 命令方面的帮助：</span><span class="sxs-lookup"><span data-stu-id="02a75-114">Use the `h` switch to get help on the `aspnet-codegenerator razorpage` command:</span></span>

```console
dotnet aspnet-codegenerator razorpage -h
```
