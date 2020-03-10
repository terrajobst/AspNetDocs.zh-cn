---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 教程：使用 MVC 5 开始使用 EF Database First
description: 本教程演示如何从现有数据库开始，并快速创建允许用户与数据进行交互的 web 应用程序。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471458"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a><span data-ttu-id="24295-103">教程：使用 MVC 5 开始使用 EF Database First</span><span class="sxs-lookup"><span data-stu-id="24295-103">Tutorial: Get started with EF Database First using MVC 5</span></span>

<span data-ttu-id="24295-104">使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。</span><span class="sxs-lookup"><span data-stu-id="24295-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="24295-105">本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。</span><span class="sxs-lookup"><span data-stu-id="24295-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="24295-106">生成的代码与数据库表中的列相对应。</span><span class="sxs-lookup"><span data-stu-id="24295-106">The generated code corresponds to the columns in the database table.</span></span> <span data-ttu-id="24295-107">在本系列文章的最后一部分，你将了解如何将数据批注添加到数据模型，以指定验证要求和显示格式。</span><span class="sxs-lookup"><span data-stu-id="24295-107">In the last part of the series, you learn how add data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="24295-108">完成后，可以转到 Azure 文章，了解如何将 .NET 应用和 SQL 数据库部署到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="24295-108">When you're done, you can advance to an Azure article to learn how to deploy a .NET app and SQL database to Azure App Service.</span></span>

<span data-ttu-id="24295-109">本教程演示如何从现有数据库开始，并快速创建允许用户与数据进行交互的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="24295-109">This tutorial shows how to start with an existing database and quickly create a web application that enables users to interact with the data.</span></span> <span data-ttu-id="24295-110">它使用实体框架6和 MVC 5 来构建 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="24295-110">It uses the Entity Framework 6 and MVC 5 to build the web application.</span></span> <span data-ttu-id="24295-111">利用 ASP.NET 基架功能，你可以自动生成用于显示、更新、创建和删除数据的代码。</span><span class="sxs-lookup"><span data-stu-id="24295-111">The ASP.NET Scaffolding feature enables you to automatically generate code for displaying, updating, creating and deleting data.</span></span> <span data-ttu-id="24295-112">使用 Visual Studio 中的发布工具，可以轻松地将站点和数据库部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="24295-112">Using the publishing tools within Visual Studio, you can easily deploy the site and database to Azure.</span></span>

<span data-ttu-id="24295-113">这部分系列重点介绍如何创建数据库并使用数据对其进行填充。</span><span class="sxs-lookup"><span data-stu-id="24295-113">This part of the series focuses on creating a database and populating it with data.</span></span>

<span data-ttu-id="24295-114">本系列文章由 Tom Dykstra 和 Rick Anderson 提供。</span><span class="sxs-lookup"><span data-stu-id="24295-114">This series was written with contributions from Tom Dykstra and Rick Anderson.</span></span> <span data-ttu-id="24295-115">它已根据 "评论" 部分中用户的反馈进行了改进。</span><span class="sxs-lookup"><span data-stu-id="24295-115">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="24295-116">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="24295-116">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24295-117">设置数据库</span><span class="sxs-lookup"><span data-stu-id="24295-117">Set up the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24295-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="24295-118">Prerequisites</span></span>

[<span data-ttu-id="24295-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="24295-119">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a><span data-ttu-id="24295-120">设置数据库</span><span class="sxs-lookup"><span data-stu-id="24295-120">Set up the database</span></span>

<span data-ttu-id="24295-121">若要模拟具有现有数据库的环境，首先要创建一个具有一些预填充数据的数据库，然后创建连接到该数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="24295-121">To mimic the environment of having an existing database, you will first create a database with some pre-filled data, and then create your web application that connects to the database.</span></span>

<span data-ttu-id="24295-122">本教程是使用 LocalDB 和 Visual Studio 2017 开发的。</span><span class="sxs-lookup"><span data-stu-id="24295-122">This tutorial was developed using LocalDB with Visual Studio 2017.</span></span> <span data-ttu-id="24295-123">你可以使用现有的数据库服务器而不是 LocalDB，但根据你的 Visual Studio 版本和你的数据库类型，Visual Studio 中的所有数据工具可能都不受支持。</span><span class="sxs-lookup"><span data-stu-id="24295-123">You can use an existing database server instead of LocalDB, but depending on your version of Visual Studio and your type of database, all of the data tools in Visual Studio might not be supported.</span></span> <span data-ttu-id="24295-124">如果这些工具不适用于您的数据库，则可能需要在您的数据库的管理套件内执行特定于数据库的一些步骤。</span><span class="sxs-lookup"><span data-stu-id="24295-124">If the tools are not available for your database, you may need to perform some of the database-specific steps within the management suite for your database.</span></span>

<span data-ttu-id="24295-125">如果你的 Visual Studio 版本中的数据库工具有问题，请确保已安装最新版本的数据库工具。</span><span class="sxs-lookup"><span data-stu-id="24295-125">If you have a problem with the database tools in your version of Visual Studio, make sure you have installed the latest version of the database tools.</span></span> <span data-ttu-id="24295-126">有关更新或安装数据库工具的信息，请参阅[Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)。</span><span class="sxs-lookup"><span data-stu-id="24295-126">For information about updating or installing the database tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).</span></span>

<span data-ttu-id="24295-127">启动 Visual Studio 并创建一个**SQL Server 数据库项目**。</span><span class="sxs-lookup"><span data-stu-id="24295-127">Launch Visual Studio and create a **SQL Server Database Project**.</span></span> <span data-ttu-id="24295-128">将项目命名为**ContosoUniversityData**。</span><span class="sxs-lookup"><span data-stu-id="24295-128">Name the project **ContosoUniversityData**.</span></span>

![创建数据库项目](setting-up-database/_static/image1.png)

<span data-ttu-id="24295-130">你现在已有一个空的数据库项目。</span><span class="sxs-lookup"><span data-stu-id="24295-130">You now have an empty database project.</span></span> <span data-ttu-id="24295-131">若要确保可以将此数据库部署到 Azure，请将 Azure SQL 数据库设置为项目的目标平台。</span><span class="sxs-lookup"><span data-stu-id="24295-131">To make sure that you can deploy this database to Azure, you'll set Azure SQL Database as the target platform for the project.</span></span> <span data-ttu-id="24295-132">设置目标平台实际上不会部署数据库;这只意味着数据库项目将验证数据库设计是否与目标平台兼容。</span><span class="sxs-lookup"><span data-stu-id="24295-132">Setting the target platform does not actually deploy the database; it only means that the database project will verify that the database design is compatible with the target platform.</span></span> <span data-ttu-id="24295-133">若要设置目标平台，请打开该项目的 "**属性**"，然后选择目标平台**Microsoft Azure SQL 数据库**。</span><span class="sxs-lookup"><span data-stu-id="24295-133">To set the target platform, open the **Properties** for the project and select **Microsoft Azure SQL Database** for the target platform.</span></span>

<span data-ttu-id="24295-134">您可以通过添加定义表的 SQL 脚本来创建本教程所需的表。</span><span class="sxs-lookup"><span data-stu-id="24295-134">You can create the tables needed for this tutorial by adding SQL scripts that define the tables.</span></span> <span data-ttu-id="24295-135">右键单击您的项目并添加一个新项。</span><span class="sxs-lookup"><span data-stu-id="24295-135">Right-click your project and add a new item.</span></span> <span data-ttu-id="24295-136">选择表**和视图** > **表**，并为*其命名*。</span><span class="sxs-lookup"><span data-stu-id="24295-136">Select **Tables and Views** > **Table** and name it *Student*.</span></span>

<span data-ttu-id="24295-137">在表文件中，将 T-sql 命令替换为以下代码，以创建表。</span><span class="sxs-lookup"><span data-stu-id="24295-137">In the table file, replace the T-SQL command with the following code to create the table.</span></span>

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

<span data-ttu-id="24295-138">请注意，设计窗口会自动与代码同步。</span><span class="sxs-lookup"><span data-stu-id="24295-138">Notice that the design window automatically synchronizes with the code.</span></span> <span data-ttu-id="24295-139">您可以使用代码或设计器。</span><span class="sxs-lookup"><span data-stu-id="24295-139">You can work with either the code or designer.</span></span>

![显示代码和设计](setting-up-database/_static/image5.png)

<span data-ttu-id="24295-141">添加另一个表。</span><span class="sxs-lookup"><span data-stu-id="24295-141">Add another table.</span></span> <span data-ttu-id="24295-142">此时间为 it 课程命名，并使用以下 T-sql 命令。</span><span class="sxs-lookup"><span data-stu-id="24295-142">This time name it Course and use the following T-SQL command.</span></span>

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

<span data-ttu-id="24295-143">再重复一次，创建名为 "注册" 的表。</span><span class="sxs-lookup"><span data-stu-id="24295-143">And, repeat one more time to create a table named Enrollment.</span></span>

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

<span data-ttu-id="24295-144">您可以通过在部署数据库后运行的脚本，使用数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="24295-144">You can populate your database with data through a script that is run after the database is deployed.</span></span> <span data-ttu-id="24295-145">向项目中添加后期部署脚本。</span><span class="sxs-lookup"><span data-stu-id="24295-145">Add a Post-Deployment Script to the project.</span></span> <span data-ttu-id="24295-146">右键单击您的项目并添加一个新项。</span><span class="sxs-lookup"><span data-stu-id="24295-146">Right-click your project and add a new item.</span></span> <span data-ttu-id="24295-147">选择 "**用户脚本**" > **部署后脚本**。</span><span class="sxs-lookup"><span data-stu-id="24295-147">Select **User Scripts** > **Post-Deployment Script**.</span></span> <span data-ttu-id="24295-148">可以使用默认名称。</span><span class="sxs-lookup"><span data-stu-id="24295-148">You can use the default name.</span></span>

<span data-ttu-id="24295-149">将以下 T-sql 代码添加到后期部署脚本。</span><span class="sxs-lookup"><span data-stu-id="24295-149">Add the following T-SQL code to the post-deployment script.</span></span> <span data-ttu-id="24295-150">此脚本仅在未找到匹配记录时将数据添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="24295-150">This script simply adds data to the database when no matching record is found.</span></span> <span data-ttu-id="24295-151">它不会覆盖或删除可能已输入数据库的任何数据。</span><span class="sxs-lookup"><span data-stu-id="24295-151">It does not overwrite or delete any data you may have entered into the database.</span></span>

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

<span data-ttu-id="24295-152">请务必注意，每次部署数据库项目时都将运行后期部署脚本。</span><span class="sxs-lookup"><span data-stu-id="24295-152">It is important to note that the post-deployment script is run every time you deploy your database project.</span></span> <span data-ttu-id="24295-153">因此，在编写此脚本时，您需要仔细考虑您的要求。</span><span class="sxs-lookup"><span data-stu-id="24295-153">Therefore, you need to carefully consider your requirements when writing this script.</span></span> <span data-ttu-id="24295-154">在某些情况下，你可能希望在每次部署项目时从一组已知的数据开始。</span><span class="sxs-lookup"><span data-stu-id="24295-154">In some cases, you may wish to start over from a known set of data every time the project is deployed.</span></span> <span data-ttu-id="24295-155">在其他情况下，您可能不想以任何方式更改现有数据。</span><span class="sxs-lookup"><span data-stu-id="24295-155">In other cases, you may not want to alter the existing data in any way.</span></span> <span data-ttu-id="24295-156">根据你的要求，你可以决定是需要部署后脚本还是需要在脚本中包括的内容。</span><span class="sxs-lookup"><span data-stu-id="24295-156">Based on your requirements, you can decide whether you need a post-deployment script or what you need to include in the script.</span></span> <span data-ttu-id="24295-157">有关使用后期部署脚本填充数据库的详细信息，请参阅[在 SQL Server 数据库项目中包含数据](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。</span><span class="sxs-lookup"><span data-stu-id="24295-157">For more information about populating your database with a post-deployment script, see [Including Data in a SQL Server Database Project](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).</span></span>

<span data-ttu-id="24295-158">现在有4个 SQL 脚本文件，但没有实际表。</span><span class="sxs-lookup"><span data-stu-id="24295-158">You now have 4 SQL script files but no actual tables.</span></span> <span data-ttu-id="24295-159">你已准备好将数据库项目部署到 localdb。</span><span class="sxs-lookup"><span data-stu-id="24295-159">You are ready to deploy your database project to localdb.</span></span> <span data-ttu-id="24295-160">在 Visual Studio 中，单击 "开始" 按钮（或按 F5）以生成并部署数据库项目。</span><span class="sxs-lookup"><span data-stu-id="24295-160">In Visual Studio, click the Start button (or F5) to build and deploy your database project.</span></span> <span data-ttu-id="24295-161">检查 "**输出**" 选项卡，验证生成和部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="24295-161">Check the **Output** tab to verify that the build and deployment succeeded.</span></span>

<span data-ttu-id="24295-162">若要查看是否已创建新数据库，请打开**SQL Server 对象资源管理器**，然后在正确的本地数据库服务器（在本例中为**localdb） \ProjectsV13**中查找该项目的名称。</span><span class="sxs-lookup"><span data-stu-id="24295-162">To see that the new database has been created, open **SQL Server Object Explorer** and look for the name of the project in the correct local database server (in this case **(localdb)\ProjectsV13**).</span></span>

<span data-ttu-id="24295-163">若要查看表中是否填充了数据，请右键单击表，然后选择 "**查看数据**"。</span><span class="sxs-lookup"><span data-stu-id="24295-163">To see that the tables are populated with data, right-click a table, and select **View Data**.</span></span>

![显示表数据](setting-up-database/_static/image9.png)

<span data-ttu-id="24295-165">将显示表数据的可编辑视图。</span><span class="sxs-lookup"><span data-stu-id="24295-165">An editable view of the table data is displayed.</span></span> <span data-ttu-id="24295-166">例如，如果选择 "**表** > " > **查看数据**"，则会看到一个表，其中包含三列 **（课程**、**标题**和**信用**）和四**行。**</span><span class="sxs-lookup"><span data-stu-id="24295-166">For example, if you select **Tables** > **dbo.course** > **View Data**, you see a table with three columns (**Course**, **Title**, and **Credits**) and four rows.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24295-167">其他资源</span><span class="sxs-lookup"><span data-stu-id="24295-167">Additional resources</span></span>

<span data-ttu-id="24295-168">有关 Code First 开发的介绍性示例，请参阅[与 ASP.NET MVC 5 入门](../introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="24295-168">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> <span data-ttu-id="24295-169">有关更高级的示例，请参阅为[ASP.NET MVC 4 应用创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="24295-169">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="24295-170">有关选择使用哪种实体框架方法的指导，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。</span><span class="sxs-lookup"><span data-stu-id="24295-170">For guidance on selecting which Entity Framework approach to use, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>

## <a name="next-steps"></a><span data-ttu-id="24295-171">后续步骤</span><span class="sxs-lookup"><span data-stu-id="24295-171">Next steps</span></span>

<span data-ttu-id="24295-172">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="24295-172">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24295-173">设置数据库</span><span class="sxs-lookup"><span data-stu-id="24295-173">Set up the database</span></span>

<span data-ttu-id="24295-174">转到下一教程，了解如何创建 web 应用程序和数据模型。</span><span class="sxs-lookup"><span data-stu-id="24295-174">Advance to the next tutorial to learn how to create the web application and data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="24295-175">创建 web 应用程序和数据模型</span><span class="sxs-lookup"><span data-stu-id="24295-175">Create the web application and data models</span></span>](creating-the-web-application.md)
