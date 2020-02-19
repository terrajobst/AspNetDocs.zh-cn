---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 创建连接字符串并使用 SQL Server LocalDB |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456512"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>创建连接字符串并使用 SQL Server LocalDB

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>创建连接字符串并使用 SQL Server LocalDB

你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。 但您可能会问的一个问题是如何指定它将连接到的数据库。 实际上不必指定要使用的数据库，实体框架将默认为使用[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。 在本部分中，我们将在应用程序的 web.config*文件中*显式添加一个连接字符串。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)是按需启动并在用户模式下运行的 SQL Server Express 数据库引擎的轻型版本。 LocalDB 在 SQL Server Express 的特殊执行模式下运行，该模式使您能够将数据库用作 *.mdf*文件。 通常，LocalDB 数据库文件保存在 web 项目的*应用\_Data*文件夹中。

不建议在生产 web 应用程序中使用 SQL Server Express。 LocalDB 不应与 web 应用程序一起用于生产，因为它不能与 IIS 一起使用。 但是，可以轻松地将 LocalDB 数据库迁移到 SQL Server 或 SQL Azure。

在 Visual Studio 2017 中，默认情况下使用 Visual Studio 安装 LocalDB。

默认情况下，实体框架将查找与对象上下文类（此项目`MovieDBContext`）相同的连接字符串。 有关详细信息，请参阅[SQL Server ASP.NET Web 应用程序的连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。

打开如下所示的应用程序根*web.config*文件。 （而不是*Views*文件夹中的*web.config 文件。* ）

![](creating-a-connection-string/_static/image1.png)

查找 `<connectionStrings>` 元素：

![](creating-a-connection-string/_static/image2.png)

将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

这两个连接字符串非常类似。 第一个连接字符串命名为 `DefaultConnection`，并用于成员资格数据库以控制谁可以访问应用程序。 已添加的连接字符串指定*应用\_Data*文件夹中名为*Movie .mdf*的 LocalDB 数据库。 在本教程中，我们不会使用成员资格数据库，有关成员身份、身份验证和安全性的详细信息，请参阅我的教程[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。

连接字符串的名称必须与[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类的名称匹配。

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

实际上，不需要添加 `MovieDBContext` 连接字符串。 如果未指定连接字符串，实体框架将使用[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类的完全限定名称（在此情况下 `MvcMovie.Models.MovieDBContext`）在用户目录中创建一个 LocalDB 数据库。 只要数据库具有，就可以将其命名为任意名称 *.MDF*后缀。 例如，我们可以将数据库命名为*MyFilms*。

接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。

> [!div class="step-by-step"]
> [上一页](adding-a-model.md)
> [下一页](accessing-your-models-data-from-a-controller.md)
