---
ms.openlocfilehash: 5ed24cd8a7e880a496d0c0295f7c1fb07f0e1032
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035984"
---
下表详细说明了 ASP.NET Core 代码生成器参数：

| 参数               | 描述|
| ----------------- | ------------ |
| -m  | 模型的名称。 |
| -dc  | 要使用的 `DbContext` 类。 |
| -udl | 使用默认布局。 |
| -outDir | 用于创建视图的相对输出文件夹路径。 |
| --referenceScriptLibraries | 向“编辑”和“创建”页面添加 `_ValidationScriptsPartial` |

使用 `h` 开关获取 `aspnet-codegenerator razorpage` 命令方面的帮助：

```console
dotnet aspnet-codegenerator razorpage -h
```
