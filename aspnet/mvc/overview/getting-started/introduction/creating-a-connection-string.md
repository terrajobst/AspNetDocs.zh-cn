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
ms.openlocfilehash: d3c6e736c5dcf4a3615e3c72cfc033effc7cc8e6
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519305"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="f4257-102">创建连接字符串并使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="f4257-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="f4257-103">作者： [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="f4257-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="f4257-104">创建连接字符串并使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="f4257-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="f4257-105">你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。</span><span class="sxs-lookup"><span data-stu-id="f4257-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="f4257-106">但您可能会问的一个问题是如何指定它将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="f4257-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="f4257-107">实际上不必指定要使用的数据库，实体框架将默认为使用[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。</span><span class="sxs-lookup"><span data-stu-id="f4257-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="f4257-108">在本部分中，我们将在应用程序的 web.config*文件中*显式添加一个连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f4257-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="f4257-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="f4257-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="f4257-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)是按需启动并在用户模式下运行的 SQL Server Express 数据库引擎的轻型版本。</span><span class="sxs-lookup"><span data-stu-id="f4257-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="f4257-111">LocalDB 在 SQL Server Express 的特殊执行模式下运行，该模式使您能够将数据库用作 *.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="f4257-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="f4257-112">通常，LocalDB 数据库文件保存在 web 项目的*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f4257-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="f4257-113">不建议在生产 web 应用程序中使用 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="f4257-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="f4257-114">LocalDB 不应与 web 应用程序一起用于生产，因为它不能与 IIS 一起使用。</span><span class="sxs-lookup"><span data-stu-id="f4257-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="f4257-115">但是，可以轻松地将 LocalDB 数据库迁移到 SQL Server 或 SQL Azure。</span><span class="sxs-lookup"><span data-stu-id="f4257-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="f4257-116">在 Visual Studio 2017 中，默认情况下使用 Visual Studio 安装 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="f4257-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="f4257-117">默认情况下，实体框架将查找与对象上下文类（此项目`MovieDBContext`）相同的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f4257-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="f4257-118">有关详细信息，请参阅[SQL Server ASP.NET Web 应用程序的连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f4257-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="f4257-119">打开如下所示的应用程序根*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f4257-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="f4257-120">（而不是*Views*文件夹中的*web.config 文件。* ）</span><span class="sxs-lookup"><span data-stu-id="f4257-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="f4257-121">查找 `<connectionStrings>` 元素：</span><span class="sxs-lookup"><span data-stu-id="f4257-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="f4257-122">将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。</span><span class="sxs-lookup"><span data-stu-id="f4257-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="f4257-123">下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="f4257-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="f4257-124">这两个连接字符串非常类似。</span><span class="sxs-lookup"><span data-stu-id="f4257-124">The two connection strings are very similar.</span></span> <span data-ttu-id="f4257-125">第一个连接字符串命名为 `DefaultConnection`，并用于成员资格数据库以控制谁可以访问应用程序。</span><span class="sxs-lookup"><span data-stu-id="f4257-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="f4257-126">已添加的连接字符串指定*应用\_Data*文件夹中名为*Movie .mdf*的 LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="f4257-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="f4257-127">在本教程中，我们不会使用成员资格数据库，有关成员身份、身份验证和安全性的详细信息，请参阅我的教程[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="f4257-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="f4257-128">连接字符串的名称必须与[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="f4257-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="f4257-129">实际上，不需要添加 `MovieDBContext` 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f4257-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="f4257-130">如果未指定连接字符串，实体框架将使用[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类的完全限定名称（在此情况下 `MvcMovie.Models.MovieDBContext`）在用户目录中创建一个 LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="f4257-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="f4257-131">只要数据库具有，就可以将其命名为任意名称 *.MDF*后缀。</span><span class="sxs-lookup"><span data-stu-id="f4257-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="f4257-132">例如，我们可以将数据库命名为*MyFilms*。</span><span class="sxs-lookup"><span data-stu-id="f4257-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="f4257-133">接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。</span><span class="sxs-lookup"><span data-stu-id="f4257-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f4257-134">[上一页](adding-a-model.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="f4257-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
