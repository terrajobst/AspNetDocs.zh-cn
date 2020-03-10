---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: 使用 Code First 迁移对数据库进行种子设定 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449114"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>使用 Code First 迁移对数据库进行种子设定

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，你将使用 EF 中的[Code First 迁移](https://msdn.microsoft.com/data/jj591621)来使用测试数据为数据库提供种子。

从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-console[Main](part-3/samples/sample1.cmd)]

此命令将名为迁移的文件夹添加到你的项目中，并在迁移文件夹中添加名为 Configuration.cs 的代码文件。

![](part-3/_static/image1.png)

打开 Configuration.cs 文件。 添加以下**using**语句。

[!code-csharp[Main](part-3/samples/sample2.cs)]

然后，将以下代码添加到**配置. Seed**方法：

[!code-csharp[Main](part-3/samples/sample3.cs)]

在 "程序包管理器控制台" 窗口中，键入以下命令：

[!code-console[Main](part-3/samples/sample4.cmd)]

第一个命令生成用于创建数据库的代码，第二个命令执行该代码。 使用[LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)在本地创建数据库。

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>探索 API （可选）

按 F5 以调试模式运行应用程序。 Visual Studio 将启动 IIS Express 并运行你的 web 应用。 然后，Visual Studio 会启动浏览器并打开应用程序的主页。

当 Visual Studio 运行 web 项目时，它会分配一个端口号。 在下图中，端口号为50524。 运行应用程序时，将看到不同的端口号。

![](part-3/_static/image3.png)

主页是使用 ASP.NET MVC 实现的。 页面顶部有一个链接，其中显示了 "API"。 此链接可为您提供 web API 自动生成的帮助页。 （若要了解如何生成此帮助页，以及如何向页面添加您自己的文档，请参阅[为 ASP.NET Web API 创建帮助页](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。）你可以单击 "帮助" 页链接来查看有关 API 的详细信息，包括请求和响应格式。

![](part-3/_static/image4.png)

API 对数据库启用 CRUD 操作。 下面概述了 API。

| Authors |  |
| --- | -- |
| GET api/authors | 获取所有作者。 |
| GET api/authors/{id} | 按 ID 获取作者。 |
| POST /api/authors | 创建新的作者。 |
| PUT /api/authors/{id} | 更新现有的作者。 |
| DELETE /api/authors/{id} | 删除作者。 |

| 图书 |  |
| --- | -- |
| GET /api/books | 获取所有书籍。 |
| GET /api/books/{id} | 按 ID 获取书籍。 |
| POST /api/books | 创建新书籍。 |
| PUT /api/books/{id} | 更新现有书籍。 |
| DELETE /api/books/{id} | 删除书籍。 |

## <a name="view-the-database-optional"></a>查看数据库（可选）

运行 "更新-数据库" 命令时，EF 会创建数据库，并将其称为 `Seed` 方法。 在本地运行应用程序时，EF 使用[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。 您可以在 Visual Studio 中查看数据库。 从“视图”菜单上，选择“SQL Server 对象资源管理器”。

![](part-3/_static/image5.png)

在 "**连接到服务器**" 对话框的 "**服务器名称**" 编辑框中，键入 "（localdb） \v11.0"。 将 "**身份**验证" 选项保留为 "Windows 身份验证"。 单击“连接”。

![](part-3/_static/image6.png)

Visual Studio 连接到 LocalDB，并在 "SQL Server 对象资源管理器" 窗口中显示现有的数据库。 您可以展开节点以查看 EF 创建的表。

![](part-3/_static/image7.png)

若要查看数据，请右键单击表并选择 "**查看数据**"。

![](part-3/_static/image8.png)

以下屏幕截图显示了 Books.xml 表的结果。 请注意，EF 用种子数据填充了数据库，表中包含 Authors 表的外键。

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [上一页](part-2.md)
> [下一页](part-4.md)
