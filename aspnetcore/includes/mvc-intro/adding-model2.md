---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044074"
---
## <a name="add-initial-migration-and-update-the-database"></a>添加初始迁移并更新数据库

* 打开命令提示符并导航到项目目录。 (目录包含*Startup.cs*文件)。

* 在命令提示符中运行以下命令：

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  [.NET Core](/dotnet/core/tools/index)是.NET 的跨平台实现。 下面是这些命令执行的操作：

  * [dotnet 还原](/dotnet/core/tools/dotnet-restore):下载中指定的 NuGet 包 *.csproj*文件。
  * `dotnet ef migrations add Initial`运行实体框架.NET Core CLI 迁移命令并创建初始迁移。 在"添加"参数是分配到迁移的名称。 此处您正在命名迁移"初始"因为这是初始数据库迁移。 此操作将创建*数据/Migrations/\<日期时间 > _Initial.cs*文件包含要添加的迁移命令*电影*到数据库表。
  * `dotnet ef database update`  我们刚刚创建的迁移更新数据库。

您将在下一教程中了解方面的数据库和连接字符串。 你将了解如何在数据模型更改[将字段添加](xref:tutorials/first-mvc-app/new-field)教程。
