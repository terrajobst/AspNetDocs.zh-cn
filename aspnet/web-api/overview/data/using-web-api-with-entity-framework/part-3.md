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
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="ab41a-102">使用 Code First 迁移对数据库进行种子设定</span><span class="sxs-lookup"><span data-stu-id="ab41a-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="ab41a-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ab41a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ab41a-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="ab41a-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ab41a-105">在本部分中，你将使用 EF 中的[Code First 迁移](https://msdn.microsoft.com/data/jj591621)来使用测试数据为数据库提供种子。</span><span class="sxs-lookup"><span data-stu-id="ab41a-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="ab41a-106">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="ab41a-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ab41a-107">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ab41a-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="ab41a-108">此命令将名为迁移的文件夹添加到你的项目中，并在迁移文件夹中添加名为 Configuration.cs 的代码文件。</span><span class="sxs-lookup"><span data-stu-id="ab41a-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="ab41a-109">打开 Configuration.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="ab41a-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="ab41a-110">添加以下**using**语句。</span><span class="sxs-lookup"><span data-stu-id="ab41a-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="ab41a-111">然后，将以下代码添加到**配置. Seed**方法：</span><span class="sxs-lookup"><span data-stu-id="ab41a-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="ab41a-112">在 "程序包管理器控制台" 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ab41a-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="ab41a-113">第一个命令生成用于创建数据库的代码，第二个命令执行该代码。</span><span class="sxs-lookup"><span data-stu-id="ab41a-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="ab41a-114">使用[LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)在本地创建数据库。</span><span class="sxs-lookup"><span data-stu-id="ab41a-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="ab41a-115">探索 API （可选）</span><span class="sxs-lookup"><span data-stu-id="ab41a-115">Explore the API (Optional)</span></span>

<span data-ttu-id="ab41a-116">按 F5 以调试模式运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="ab41a-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="ab41a-117">Visual Studio 将启动 IIS Express 并运行你的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="ab41a-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="ab41a-118">然后，Visual Studio 会启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="ab41a-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="ab41a-119">当 Visual Studio 运行 web 项目时，它会分配一个端口号。</span><span class="sxs-lookup"><span data-stu-id="ab41a-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="ab41a-120">在下图中，端口号为50524。</span><span class="sxs-lookup"><span data-stu-id="ab41a-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="ab41a-121">运行应用程序时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="ab41a-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="ab41a-122">主页是使用 ASP.NET MVC 实现的。</span><span class="sxs-lookup"><span data-stu-id="ab41a-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="ab41a-123">页面顶部有一个链接，其中显示了 "API"。</span><span class="sxs-lookup"><span data-stu-id="ab41a-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="ab41a-124">此链接可为您提供 web API 自动生成的帮助页。</span><span class="sxs-lookup"><span data-stu-id="ab41a-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="ab41a-125">（若要了解如何生成此帮助页，以及如何向页面添加您自己的文档，请参阅[为 ASP.NET Web API 创建帮助页](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。）你可以单击 "帮助" 页链接来查看有关 API 的详细信息，包括请求和响应格式。</span><span class="sxs-lookup"><span data-stu-id="ab41a-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="ab41a-126">API 对数据库启用 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="ab41a-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="ab41a-127">下面概述了 API。</span><span class="sxs-lookup"><span data-stu-id="ab41a-127">The following summarizes the API.</span></span>

| <span data-ttu-id="ab41a-128">Authors</span><span class="sxs-lookup"><span data-stu-id="ab41a-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="ab41a-129">GET api/authors</span><span class="sxs-lookup"><span data-stu-id="ab41a-129">GET api/authors</span></span> | <span data-ttu-id="ab41a-130">获取所有作者。</span><span class="sxs-lookup"><span data-stu-id="ab41a-130">Get all authors.</span></span> |
| <span data-ttu-id="ab41a-131">GET api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="ab41a-131">GET api/authors/{id}</span></span> | <span data-ttu-id="ab41a-132">按 ID 获取作者。</span><span class="sxs-lookup"><span data-stu-id="ab41a-132">Get an author by ID.</span></span> |
| <span data-ttu-id="ab41a-133">POST /api/authors</span><span class="sxs-lookup"><span data-stu-id="ab41a-133">POST /api/authors</span></span> | <span data-ttu-id="ab41a-134">创建新的作者。</span><span class="sxs-lookup"><span data-stu-id="ab41a-134">Create a new author.</span></span> |
| <span data-ttu-id="ab41a-135">PUT /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="ab41a-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="ab41a-136">更新现有的作者。</span><span class="sxs-lookup"><span data-stu-id="ab41a-136">Update an existing author.</span></span> |
| <span data-ttu-id="ab41a-137">DELETE /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="ab41a-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="ab41a-138">删除作者。</span><span class="sxs-lookup"><span data-stu-id="ab41a-138">Delete an author.</span></span> |

| <span data-ttu-id="ab41a-139">图书</span><span class="sxs-lookup"><span data-stu-id="ab41a-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="ab41a-140">GET /api/books</span><span class="sxs-lookup"><span data-stu-id="ab41a-140">GET /api/books</span></span> | <span data-ttu-id="ab41a-141">获取所有书籍。</span><span class="sxs-lookup"><span data-stu-id="ab41a-141">Get all books.</span></span> |
| <span data-ttu-id="ab41a-142">GET /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="ab41a-142">GET /api/books/{id}</span></span> | <span data-ttu-id="ab41a-143">按 ID 获取书籍。</span><span class="sxs-lookup"><span data-stu-id="ab41a-143">Get a book by ID.</span></span> |
| <span data-ttu-id="ab41a-144">POST /api/books</span><span class="sxs-lookup"><span data-stu-id="ab41a-144">POST /api/books</span></span> | <span data-ttu-id="ab41a-145">创建新书籍。</span><span class="sxs-lookup"><span data-stu-id="ab41a-145">Create a new book.</span></span> |
| <span data-ttu-id="ab41a-146">PUT /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="ab41a-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="ab41a-147">更新现有书籍。</span><span class="sxs-lookup"><span data-stu-id="ab41a-147">Update an existing book.</span></span> |
| <span data-ttu-id="ab41a-148">DELETE /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="ab41a-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="ab41a-149">删除书籍。</span><span class="sxs-lookup"><span data-stu-id="ab41a-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="ab41a-150">查看数据库（可选）</span><span class="sxs-lookup"><span data-stu-id="ab41a-150">View the Database (Optional)</span></span>

<span data-ttu-id="ab41a-151">运行 "更新-数据库" 命令时，EF 会创建数据库，并将其称为 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="ab41a-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="ab41a-152">在本地运行应用程序时，EF 使用[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ab41a-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="ab41a-153">您可以在 Visual Studio 中查看数据库。</span><span class="sxs-lookup"><span data-stu-id="ab41a-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="ab41a-154">从“视图”菜单上，选择“SQL Server 对象资源管理器”。</span><span class="sxs-lookup"><span data-stu-id="ab41a-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="ab41a-155">在 "**连接到服务器**" 对话框的 "**服务器名称**" 编辑框中，键入 "（localdb） \v11.0"。</span><span class="sxs-lookup"><span data-stu-id="ab41a-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="ab41a-156">将 "**身份**验证" 选项保留为 "Windows 身份验证"。</span><span class="sxs-lookup"><span data-stu-id="ab41a-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="ab41a-157">单击“连接”。</span><span class="sxs-lookup"><span data-stu-id="ab41a-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="ab41a-158">Visual Studio 连接到 LocalDB，并在 "SQL Server 对象资源管理器" 窗口中显示现有的数据库。</span><span class="sxs-lookup"><span data-stu-id="ab41a-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="ab41a-159">您可以展开节点以查看 EF 创建的表。</span><span class="sxs-lookup"><span data-stu-id="ab41a-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="ab41a-160">若要查看数据，请右键单击表并选择 "**查看数据**"。</span><span class="sxs-lookup"><span data-stu-id="ab41a-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="ab41a-161">以下屏幕截图显示了 Books.xml 表的结果。</span><span class="sxs-lookup"><span data-stu-id="ab41a-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="ab41a-162">请注意，EF 用种子数据填充了数据库，表中包含 Authors 表的外键。</span><span class="sxs-lookup"><span data-stu-id="ab41a-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="ab41a-163">[上一页](part-2.md)
> [下一页](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="ab41a-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
