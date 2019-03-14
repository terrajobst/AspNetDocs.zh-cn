---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062594"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="826ec-101">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="826ec-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="826ec-102">从命令行（在包含 Program.cs、Startup.cs 和 .csproj 文件的项目目录中）中运行如下命令：</span><span class="sxs-lookup"><span data-stu-id="826ec-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

<span data-ttu-id="826ec-103">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="826ec-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="826ec-104">当处于错误的目录时，会发生上述错误。</span><span class="sxs-lookup"><span data-stu-id="826ec-104">The preceeding error happens when you are in the wrong directory.</span></span> <span data-ttu-id="826ec-105">打开命令行界面，进入项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录），然后运行上述命令。</span><span class="sxs-lookup"><span data-stu-id="826ec-105">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files), and then run the preceeding command.</span></span>

<span data-ttu-id="826ec-106">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="826ec-106">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="826ec-107">退出 Visual Studio，然后重新运行命令。</span><span class="sxs-lookup"><span data-stu-id="826ec-107">Exit Visual Studio and run the command again.</span></span>
