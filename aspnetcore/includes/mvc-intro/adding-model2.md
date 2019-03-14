---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044074"
---
## <a name="add-initial-migration-and-update-the-database"></a><span data-ttu-id="5d872-101">添加初始迁移并更新数据库</span><span class="sxs-lookup"><span data-stu-id="5d872-101">Add initial migration and update the database</span></span>

* <span data-ttu-id="5d872-102">打开命令提示符并导航到项目目录。</span><span class="sxs-lookup"><span data-stu-id="5d872-102">Open a command prompt and navigate to the project directory.</span></span> <span data-ttu-id="5d872-103">(目录包含*Startup.cs*文件)。</span><span class="sxs-lookup"><span data-stu-id="5d872-103">(The directory containing the *Startup.cs* file).</span></span>

* <span data-ttu-id="5d872-104">在命令提示符中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="5d872-104">Run the following commands in the command prompt:</span></span>

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  <span data-ttu-id="5d872-105">[.NET Core](/dotnet/core/tools/index)是.NET 的跨平台实现。</span><span class="sxs-lookup"><span data-stu-id="5d872-105">[.NET Core](/dotnet/core/tools/index) is a cross-platform implementation of .NET.</span></span> <span data-ttu-id="5d872-106">下面是这些命令执行的操作：</span><span class="sxs-lookup"><span data-stu-id="5d872-106">Here is what these commands do:</span></span>

  * <span data-ttu-id="5d872-107">[dotnet 还原](/dotnet/core/tools/dotnet-restore):下载中指定的 NuGet 包 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="5d872-107">[dotnet restore](/dotnet/core/tools/dotnet-restore): Downloads the NuGet packages specified in the *.csproj* file.</span></span>
  * <span data-ttu-id="5d872-108">`dotnet ef migrations add Initial`运行实体框架.NET Core CLI 迁移命令并创建初始迁移。</span><span class="sxs-lookup"><span data-stu-id="5d872-108">`dotnet ef migrations add Initial` Runs the Entity Framework .NET Core CLI migrations command and creates the initial migration.</span></span> <span data-ttu-id="5d872-109">在"添加"参数是分配到迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="5d872-109">The parameter after "add" is a name that you assign to the migration.</span></span> <span data-ttu-id="5d872-110">此处您正在命名迁移"初始"因为这是初始数据库迁移。</span><span class="sxs-lookup"><span data-stu-id="5d872-110">Here you're naming the migration "Initial" because it's the initial database migration.</span></span> <span data-ttu-id="5d872-111">此操作将创建*数据/Migrations/\<日期时间 > _Initial.cs*文件包含要添加的迁移命令*电影*到数据库表。</span><span class="sxs-lookup"><span data-stu-id="5d872-111">This operation creates the *Data/Migrations/\<date-time>_Initial.cs* file containing the migration commands to add the *Movie* table to the database.</span></span>
  * <span data-ttu-id="5d872-112">`dotnet ef database update`  我们刚刚创建的迁移更新数据库。</span><span class="sxs-lookup"><span data-stu-id="5d872-112">`dotnet ef database update`  Updates the database with the migration we just created.</span></span>

<span data-ttu-id="5d872-113">您将在下一教程中了解方面的数据库和连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5d872-113">You'll learn about the database and connection string in the next tutorial.</span></span> <span data-ttu-id="5d872-114">你将了解如何在数据模型更改[将字段添加](xref:tutorials/first-mvc-app/new-field)教程。</span><span class="sxs-lookup"><span data-stu-id="5d872-114">You'll learn about data model changes in the [Add a field](xref:tutorials/first-mvc-app/new-field) tutorial.</span></span>
