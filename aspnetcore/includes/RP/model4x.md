---
ms.openlocfilehash: d875717d480fe234ac5a328493fcec6a268e37a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039514"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>搭建“电影”模型的基架

* 从命令行（在包含 Program.cs、Startup.cs 和 .csproj 文件的项目目录中）中运行如下命令：

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

如果收到错误：
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

打开一个到项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）的命令 shell。
