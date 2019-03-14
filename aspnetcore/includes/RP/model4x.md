---
ms.openlocfilehash: d875717d480fe234ac5a328493fcec6a268e37a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039514"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="3b59e-101">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="3b59e-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="3b59e-102">从命令行（在包含 Program.cs、Startup.cs 和 .csproj 文件的项目目录中）中运行如下命令：</span><span class="sxs-lookup"><span data-stu-id="3b59e-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="3b59e-103">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="3b59e-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="3b59e-104">打开一个到项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）的命令 shell。</span><span class="sxs-lookup"><span data-stu-id="3b59e-104">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
