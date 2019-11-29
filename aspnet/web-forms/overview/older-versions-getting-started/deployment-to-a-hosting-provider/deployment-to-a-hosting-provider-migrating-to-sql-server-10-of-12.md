---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：迁移到 SQL Server-10 个，共12个 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640583"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a><span data-ttu-id="f07da-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：迁移到 SQL Server-10 （共12个）</span><span class="sxs-lookup"><span data-stu-id="f07da-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Migrating to SQL Server - 10 of 12</span></span>

<span data-ttu-id="f07da-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f07da-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f07da-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="f07da-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="f07da-106">本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="f07da-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="f07da-107">如果安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="f07da-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="f07da-108">有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="f07da-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="f07da-109">有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f07da-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="f07da-110">概述</span><span class="sxs-lookup"><span data-stu-id="f07da-110">Overview</span></span>

<span data-ttu-id="f07da-111">本教程演示如何从 SQL Server Compact 迁移到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f07da-111">This tutorial shows you how to migrate from SQL Server Compact to SQL Server.</span></span> <span data-ttu-id="f07da-112">您可能想要这样做的一个原因是利用 SQL Server Compact 不支持的 SQL Server 功能，如存储过程、触发器、视图或复制。</span><span class="sxs-lookup"><span data-stu-id="f07da-112">One reason you might want to do that is to take advantage of SQL Server features that SQL Server Compact does not support, such as stored procedures, triggers, views, or replication.</span></span> <span data-ttu-id="f07da-113">有关 SQL Server Compact 和 SQL Server 之间的差异的详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="f07da-113">For more information about the differences between SQL Server Compact and SQL Server, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

### <a name="sql-server-express-versus-full-sql-server-for-development"></a><span data-ttu-id="f07da-114">用于开发的 SQL Server Express 与完全 SQL Server</span><span class="sxs-lookup"><span data-stu-id="f07da-114">SQL Server Express versus full SQL Server for Development</span></span>

<span data-ttu-id="f07da-115">一旦决定升级到 SQL Server，你可能希望在开发和测试环境中使用 SQL Server 或 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="f07da-115">Once you've decided to upgrade to SQL Server, you might want to use SQL Server or SQL Server Express in your development and test environments.</span></span> <span data-ttu-id="f07da-116">除了工具支持和数据库引擎功能中的差异外，SQL Server Compact 与 SQL Server 的其他版本之间提供程序实现之间的差异。</span><span class="sxs-lookup"><span data-stu-id="f07da-116">In addition to the differences in tool support and in database engine features, there are differences in provider implementations between SQL Server Compact and other versions of SQL Server.</span></span> <span data-ttu-id="f07da-117">这些差异可能会导致相同的代码生成不同的结果。</span><span class="sxs-lookup"><span data-stu-id="f07da-117">These differences can cause the same code to generate different results.</span></span> <span data-ttu-id="f07da-118">因此，如果您决定将 SQL Server Compact 作为开发数据库，则应在每次部署到生产环境之前，在测试环境中全面测试您的站点 SQL Server 或 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="f07da-118">Therefore, if you decide to keep SQL Server Compact as your development database, you should thoroughly test your site in SQL Server or SQL Server Express in a test environment before each deployment to production.</span></span>

<span data-ttu-id="f07da-119">与 SQL Server Compact 不同，SQL Server Express 实质上是相同的数据库引擎，并使用与完整 SQL Server 相同的 .NET 提供程序。</span><span class="sxs-lookup"><span data-stu-id="f07da-119">Unlike SQL Server Compact, SQL Server Express is essentially the same database engine and uses the same .NET provider as full SQL Server.</span></span> <span data-ttu-id="f07da-120">当你测试 SQL Server Express 时，你可以放心地获得与 SQL Server 相同的结果。</span><span class="sxs-lookup"><span data-stu-id="f07da-120">When you test with SQL Server Express, you can be confident of getting the same results as you will with SQL Server.</span></span> <span data-ttu-id="f07da-121">您可以将大多数相同的数据库工具与 SQL Server Express 一起使用，这些工具可用于 SQL Server （一个值得[SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)的值得注意的异常），并支持其他 SQL Server 功能，如存储过程、视图、触发器和复制。</span><span class="sxs-lookup"><span data-stu-id="f07da-121">You can use most of the same database tools with SQL Server Express that you can use with SQL Server (a notable exception being [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), and it supports other features of SQL Server like stored procedures, views, triggers, and replication.</span></span> <span data-ttu-id="f07da-122">（但是，您通常必须在生产网站中使用完整 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f07da-122">(You typically have to use full SQL Server in a production website, however.</span></span> <span data-ttu-id="f07da-123">SQL Server Express 可以在共享的宿主环境中运行，但并不是针对此环境设计的，并且许多宿主提供程序不支持它。）</span><span class="sxs-lookup"><span data-stu-id="f07da-123">SQL Server Express can run in a shared hosting environment, but it was not designed for that, and many hosting providers do not support it.)</span></span>

<span data-ttu-id="f07da-124">如果使用的是 Visual Studio 2012，通常会为开发环境选择 SQL Server Express LocalDB，因为这是 Visual Studio 默认安装的内容。</span><span class="sxs-lookup"><span data-stu-id="f07da-124">If you are using Visual Studio 2012, you typically choose SQL Server Express LocalDB for your development environment because that is what is installed by default with Visual Studio.</span></span> <span data-ttu-id="f07da-125">但是，LocalDB 在 IIS 中不起作用，因此对于测试环境，必须使用 SQL Server 或 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="f07da-125">However, LocalDB does not work in IIS, so for your test environment you have to use either SQL Server or SQL Server Express.</span></span>

### <a name="combining-databases-versus-keeping-them-separate"></a><span data-ttu-id="f07da-126">合并数据库，并将其保持独立</span><span class="sxs-lookup"><span data-stu-id="f07da-126">Combining Databases versus Keeping Them Separate</span></span>

<span data-ttu-id="f07da-127">Contoso 大学应用程序有两个 SQL Server Compact 数据库：成员资格数据库（*aspnet*）和应用程序数据库（*School .sdf*）。</span><span class="sxs-lookup"><span data-stu-id="f07da-127">The Contoso University application has two SQL Server Compact databases: the membership database (*aspnet.sdf*) and the application database (*School.sdf*).</span></span> <span data-ttu-id="f07da-128">迁移时，可以将这些数据库迁移到两个不同的数据库或单个数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-128">When you migrate, you can migrate these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="f07da-129">你可能想要将它们组合在一起，以便于你的应用程序数据库和成员资格数据库之间进行数据库联接。</span><span class="sxs-lookup"><span data-stu-id="f07da-129">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="f07da-130">托管计划还可能会提供组合的原因。</span><span class="sxs-lookup"><span data-stu-id="f07da-130">Your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="f07da-131">例如，宿主提供程序可能会为多个数据库收取更多的费用，甚至可能甚至不允许多个数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-131">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span> <span data-ttu-id="f07da-132">这就是本教程中使用的 Cytanium Lite 托管帐户，只允许单个 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-132">That's the case with the Cytanium Lite hosting account that's used for this tutorial, which allows only a single SQL Server database.</span></span>

<span data-ttu-id="f07da-133">在本教程中，你将以这种方式迁移两个数据库：</span><span class="sxs-lookup"><span data-stu-id="f07da-133">In this tutorial, you'll migrate your two databases this way:</span></span>

- <span data-ttu-id="f07da-134">迁移到开发环境中的两个 LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-134">Migrate to two LocalDB databases in the development environment.</span></span>
- <span data-ttu-id="f07da-135">迁移到测试环境中的两个 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-135">Migrate to two SQL Server Express databases in the test environment.</span></span>
- <span data-ttu-id="f07da-136">在生产环境中迁移到一个组合的完整 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-136">Migrate to one combined full SQL Server database in the production environment.</span></span>

<span data-ttu-id="f07da-137">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="f07da-137">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="installing-sql-server-express"></a><span data-ttu-id="f07da-138">安装 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="f07da-138">Installing SQL Server Express</span></span>

<span data-ttu-id="f07da-139">默认情况下，默认情况下，将使用 Visual Studio 2010 自动安装 SQL Server Express，但默认情况下它不与 Visual Studio 2012 一起安装。</span><span class="sxs-lookup"><span data-stu-id="f07da-139">SQL Server Express is automatically installed by default with Visual Studio 2010, but by default it is not installed with Visual Studio 2012.</span></span> <span data-ttu-id="f07da-140">若要安装 SQL Server 2012 Express，请单击以下链接</span><span class="sxs-lookup"><span data-stu-id="f07da-140">To install SQL Server 2012 Express, click the following link</span></span>

- [<span data-ttu-id="f07da-141">SQL Server Express 2012</span><span class="sxs-lookup"><span data-stu-id="f07da-141">SQL Server Express 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=29062)

<span data-ttu-id="f07da-142">选择*简体中文/x64/sqlexpr.exe\_x64\_简体中文*或*简体中文/x86/sqlexpr.exe\_x86\_简体中文*，然后在安装向导中接受默认设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-142">Choose *ENU/x64/SQLEXPR\_x64\_ENU.exe* or *ENU/x86/SQLEXPR\_x86\_ENU.exe*, and in the installation wizard accept the default settings.</span></span> <span data-ttu-id="f07da-143">有关安装选项的详细信息，请参阅[从安装向导安装 SQL Server 2012 （安装程序）](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f07da-143">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="f07da-144">为测试环境创建 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="f07da-144">Creating SQL Server Express Databases for the Test Environment</span></span>

<span data-ttu-id="f07da-145">下一步是创建 ASP.NET 成员身份和 School 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-145">The next step is to create the ASP.NET membership and School databases.</span></span>

<span data-ttu-id="f07da-146">从 "**视图**" 菜单中选择 "**服务器资源管理器**（Visual Web Developer 中的**数据库资源管理器**）"，然后右键单击 "**数据连接**"，然后选择 "**创建新的 SQL Server 数据库**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-146">From the **View** menu select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

<span data-ttu-id="f07da-148">在 "新建**SQL Server 数据库**" 对话框的 "**服务器名称**" 框中，输入 ".\SQLExpress"，在 "**新数据库名称**" 框中输入 "aspnet-测试"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-148">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-Test" in the **New database name** box, then click **OK**.</span></span>

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

<span data-ttu-id="f07da-150">按照相同的过程创建一个名为 "School Test" 的新 SQL Server Express School 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-150">Follow the same procedure to create a new SQL Server Express School database named "School-Test".</span></span>

<span data-ttu-id="f07da-151">（你要将 "Test" 追加到这些数据库名称，因为稍后你将为开发环境创建每个数据库的另一个实例，并且你需要能够区分这两个数据库集。）</span><span class="sxs-lookup"><span data-stu-id="f07da-151">(You're appending "Test" to these database names because later you'll create an additional instance of each database for the development environment, and you need to be able to differentiate the two sets of databases.)</span></span>

<span data-ttu-id="f07da-152">**服务器资源管理器**现在显示两个新数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-152">**Server Explorer** now shows the two new databases.</span></span>

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a><span data-ttu-id="f07da-154">为新数据库创建 Grant 脚本</span><span class="sxs-lookup"><span data-stu-id="f07da-154">Creating a Grant Script for the New Databases</span></span>

<span data-ttu-id="f07da-155">当应用程序在开发计算机上的 IIS 中运行时，应用程序将通过使用默认应用程序池的凭据来访问数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-155">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="f07da-156">但是，默认情况下，应用程序池标识没有打开数据库的权限。</span><span class="sxs-lookup"><span data-stu-id="f07da-156">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="f07da-157">因此，你必须运行脚本来授予该权限。</span><span class="sxs-lookup"><span data-stu-id="f07da-157">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="f07da-158">在本部分中，将创建稍后要运行的脚本，以确保应用程序在 IIS 中运行时可以打开数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-158">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="f07da-159">在 "[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)的解决方案" 教程中创建的解决方案的*SolutionFiles*文件夹中，创建一个名为*Grant*.sql 的新 SQL 文件。</span><span class="sxs-lookup"><span data-stu-id="f07da-159">In the solution's *SolutionFiles* folder that you created in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, create a new SQL file named *Grant.sql*.</span></span> <span data-ttu-id="f07da-160">将以下 SQL 命令复制到该文件中，然后保存并关闭该文件：</span><span class="sxs-lookup"><span data-stu-id="f07da-160">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> <span data-ttu-id="f07da-161">此脚本旨在与 SQL Server 2008 和 Windows 7 中的 IIS 设置一起使用，因为在本教程中指定了这些设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-161">This script is designed to work with SQL Server 2008 and with the IIS settings in Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="f07da-162">如果使用的是其他版本的 SQL Server 或 Windows，或者在计算机上以不同的方式设置 IIS，则可能需要对此脚本进行更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-162">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="f07da-163">有关 SQL Server 脚本的详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="f07da-163">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f07da-164">**安全说明**此脚本向 db\_所有者授予在运行时访问数据库的用户的权限，您将在生产环境中使用该权限。</span><span class="sxs-lookup"><span data-stu-id="f07da-164">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="f07da-165">在某些情况下，你可能想要指定具有仅用于部署的完整数据库架构更新权限的用户，并为运行时指定仅拥有读取和写入数据权限的其他用户。</span><span class="sxs-lookup"><span data-stu-id="f07da-165">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="f07da-166">有关详细信息，请参阅在[部署到 IIS 作为测试环境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)中查看**Code First 迁移的自动 web.config 更改**。</span><span class="sxs-lookup"><span data-stu-id="f07da-166">For more information, see **Reviewing the Automatic Web.config Changes for Code First Migrations** in [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).</span></span>

## <a name="configuring-database-deployment-for-the-test-environment"></a><span data-ttu-id="f07da-167">为测试环境配置数据库部署</span><span class="sxs-lookup"><span data-stu-id="f07da-167">Configuring Database Deployment for the Test Environment</span></span>

<span data-ttu-id="f07da-168">接下来，你将配置 Visual Studio，以便它将为每个数据库执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="f07da-168">Next, you'll configure Visual Studio so that it will do the following tasks for each database:</span></span>

- <span data-ttu-id="f07da-169">生成一个 SQL 脚本，该脚本在目标数据库中创建源数据库的结构（表、列、约束等）。</span><span class="sxs-lookup"><span data-stu-id="f07da-169">Generate a SQL script that creates the source database's structure (tables, columns, constraints, etc.) in the destination database.</span></span>
- <span data-ttu-id="f07da-170">生成一个 SQL 脚本，用于将源数据库的数据插入目标数据库的表中。</span><span class="sxs-lookup"><span data-stu-id="f07da-170">Generate a SQL script that inserts the source database's data into the tables in the destination database.</span></span>
- <span data-ttu-id="f07da-171">在目标数据库中运行生成的脚本以及您创建的授予脚本。</span><span class="sxs-lookup"><span data-stu-id="f07da-171">Run the generated scripts, and the Grant script that you created, in the destination database.</span></span>

<span data-ttu-id="f07da-172">打开项目的 "**属性**" 窗口，然后选择 "**包/发布 SQL** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-172">Open the **Project Properties** window and select the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f07da-173">请确保在 "**配置**" 下拉列表中选择 "**活动（发布）** " 或 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-173">Make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="f07da-174">单击 "**启用此页**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-174">Click **Enable this Page**.</span></span>

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

<span data-ttu-id="f07da-176">"**包/发布 SQL** " 选项卡通常处于禁用状态，因为它指定了旧的部署方法。</span><span class="sxs-lookup"><span data-stu-id="f07da-176">The **Package/Publish SQL** tab is normally disabled because it specifies a legacy deployment method.</span></span> <span data-ttu-id="f07da-177">在大多数情况下，应在 "**发布 Web** " 向导中配置数据库部署。</span><span class="sxs-lookup"><span data-stu-id="f07da-177">For most scenarios, you should configure database deployment in the **Publish Web** wizard.</span></span> <span data-ttu-id="f07da-178">从 SQL Server Compact 迁移到 SQL Server 或 SQL Server Express 是一个特殊情况，此方法是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="f07da-178">Migrating from SQL Server Compact to SQL Server or SQL Server Express is a special case for which this method is a good choice.</span></span>

<span data-ttu-id="f07da-179">单击 "**从 Web.config 导入**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-179">Click **Import from Web.config**.</span></span>

![Selecting_Import_from_Web .config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

<span data-ttu-id="f07da-181">Visual Studio 将在*web.config*文件中查找连接字符串，找到一个用于成员资格数据库，另一个用于 School 数据库，并添加与**数据库条目**表中的每个连接字符串相对应的行。</span><span class="sxs-lookup"><span data-stu-id="f07da-181">Visual Studio looks for connection strings in the *Web.config* file, finds one for the membership database and one for the School database, and adds a row corresponding to each connection string in the **Database Entries** table.</span></span> <span data-ttu-id="f07da-182">它找到的连接字符串适用于现有 SQL Server Compact 数据库，下一步是配置这些数据库的部署方式和位置。</span><span class="sxs-lookup"><span data-stu-id="f07da-182">The connection strings it finds are for the existing SQL Server Compact databases, and your next step will be to configure how and where to deploy these databases.</span></span>

<span data-ttu-id="f07da-183">您可以在 "数据库条目**详细信息**" 部分的 "**数据库**项" 表下输入数据库部署设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-183">You enter database deployment settings in the **Database Entry Details** section below the **Database Entries** table.</span></span> <span data-ttu-id="f07da-184">"**数据库条目详细信息**" 部分中显示的设置与 "**数据库项**" 表中的哪个行相关，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="f07da-184">The settings shown in the **Database Entry Details** section pertain to whichever row in the **Database Entries** table is selected, as shown in the following illustration.</span></span>

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="f07da-186">为成员资格数据库配置部署设置</span><span class="sxs-lookup"><span data-stu-id="f07da-186">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="f07da-187">若要配置应用于成员资格数据库的设置，请在 "**数据库条目**" 表中选择 " **DefaultConnection** " 行。</span><span class="sxs-lookup"><span data-stu-id="f07da-187">Select the **DefaultConnection-Deployment** row in the **Database Entries** table in order to configure settings that apply to the membership database.</span></span>

<span data-ttu-id="f07da-188">在 "**目标数据库的连接字符串**" 中，输入指向新 SQL Server Express 成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-188">In **Connection string for destination database**, enter a connection string that points to the new SQL Server Express membership database.</span></span> <span data-ttu-id="f07da-189">你可以从**服务器资源管理器**获取所需的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-189">You can get the connection string you need from **Server Explorer**.</span></span> <span data-ttu-id="f07da-190">在**服务器资源管理器**中，展开 "**数据连接**" 并选择 " **aspnetTest** " 数据库，然后在 "**属性**" 窗口中复制**连接字符串**值。</span><span class="sxs-lookup"><span data-stu-id="f07da-190">In **Server Explorer**, expand **Data Connections** and select the **aspnetTest** database, then from the **Properties** window copy the **Connection String** value.</span></span>

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

<span data-ttu-id="f07da-192">此处重现相同的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="f07da-192">The same connection string is reproduced here:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

<span data-ttu-id="f07da-193">将此连接字符串复制并粘贴到 "**包/发布 SQL** " 选项卡中**目标数据库的连接字符串**中。</span><span class="sxs-lookup"><span data-stu-id="f07da-193">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f07da-194">请确保已选择 "**从现有数据库提取数据和/或架构**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-194">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span> <span data-ttu-id="f07da-195">这会导致在目标数据库中自动生成并运行 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="f07da-195">This is what causes SQL scripts to be automatically generated and run in the destination database.</span></span>

<span data-ttu-id="f07da-196">**源数据库值的连接字符串**是从*web.config 文件中*提取的，指向开发 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-196">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="f07da-197">这是将用于生成稍后将在目标数据库中运行的脚本的源数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-197">This is the source database that will be used to generate the scripts that will run later in the destination database.</span></span> <span data-ttu-id="f07da-198">由于你想要部署数据库的生产版本，因此请将 "aspnet-Dev" 更改为 "aspnet-Prod"。</span><span class="sxs-lookup"><span data-stu-id="f07da-198">Since you want to deploy the production version of the database, change "aspnet-Dev.sdf" to "aspnet-Prod.sdf".</span></span>

<span data-ttu-id="f07da-199">由于要复制数据（用户帐户和角色）以及数据库结构，因此请将**数据库脚本选项**从**架构仅**更改为**架构和数据**。</span><span class="sxs-lookup"><span data-stu-id="f07da-199">Change **Database scripting options** from **Schema Only** to **Schema and data**, since you want to copy your data (user accounts and roles) as well as the database structure.</span></span>

<span data-ttu-id="f07da-200">若要配置部署以运行之前创建的 grant 脚本，必须将其添加到 "**数据库脚本**" 部分。</span><span class="sxs-lookup"><span data-stu-id="f07da-200">To configure deployment to run the grant scripts that you created earlier, you have to add them to the **Database Scripts** section.</span></span> <span data-ttu-id="f07da-201">单击 "**添加脚本**"，然后在 "**添加 SQL 脚本**" 对话框中，导航到你在其中存储了 grant 脚本的文件夹（这是包含你的解决方案文件的文件夹）。</span><span class="sxs-lookup"><span data-stu-id="f07da-201">Click **Add Script**, and in the **Add SQL Scripts** dialog box, navigate to the folder where you stored the grant script (this is the folder that contains your solution file).</span></span> <span data-ttu-id="f07da-202">选择名为*Grant .sql*的文件，并单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-202">Select the file named *Grant.sql*, and click **Open**.</span></span>

<span data-ttu-id="f07da-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="f07da-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span></span>

<span data-ttu-id="f07da-204">**数据库条目**中的**DefaultConnection**行的设置现在如下图所示：</span><span class="sxs-lookup"><span data-stu-id="f07da-204">The settings for the **DefaultConnection-Deployment** row in **Database Entries** now look like the following illustration:</span></span>

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="f07da-206">为 School 数据库配置部署设置</span><span class="sxs-lookup"><span data-stu-id="f07da-206">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="f07da-207">接下来，在 "**数据库项**" 表中选择 " **SchoolContext** " 行，以便为 School 数据库配置部署设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-207">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure deployment settings for the School database.</span></span>

<span data-ttu-id="f07da-208">您可以使用之前使用的方法来获取新的 SQL Server Express 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-208">You can use the same method you used earlier to get the connection string for the new SQL Server Express database.</span></span> <span data-ttu-id="f07da-209">将此连接字符串复制到 "**包/发布 SQL** " 选项卡中**目标数据库的连接字符串**中。</span><span class="sxs-lookup"><span data-stu-id="f07da-209">Copy this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

<span data-ttu-id="f07da-210">请确保已选择 "**从现有数据库提取数据和/或架构**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-210">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span>

<span data-ttu-id="f07da-211">**源数据库值的连接字符串**是从*web.config 文件中*提取的，指向开发 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-211">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="f07da-212">将 "School-Dev" 更改为 "School-Prod" 以部署数据库的生产版本。</span><span class="sxs-lookup"><span data-stu-id="f07da-212">Change "School-Dev.sdf" to "School-Prod.sdf" to deploy the production version of the database.</span></span> <span data-ttu-id="f07da-213">（您从未在\_Data 文件夹的应用程序中创建了一个 School-Prod 文件，因此你稍后将从测试环境将该文件复制到 ContosoUniversity 项目文件夹中的应用程序\_Data 文件夹。）</span><span class="sxs-lookup"><span data-stu-id="f07da-213">(You never created a School-Prod.sdf file in the App\_Data folder, so you'll copy that file from the test environment to the App\_Data folder in the ContosoUniversity project folder later.)</span></span>

<span data-ttu-id="f07da-214">将**数据库脚本选项**更改为**架构和数据**。</span><span class="sxs-lookup"><span data-stu-id="f07da-214">Change **Database scripting options** to **Schema and data**.</span></span>

<span data-ttu-id="f07da-215">还需要运行脚本来向应用程序池标识授予对此数据库的读取和写入权限，因此请添加*grant .sql*脚本文件，就像对成员资格数据库执行的操作一样。</span><span class="sxs-lookup"><span data-stu-id="f07da-215">You also want to run the script to grant read and write permission for this database to the application pool identity, so add the *Grant.sql* script file as you did for the membership database.</span></span>

<span data-ttu-id="f07da-216">完成后，**数据库条目**中**SchoolContext**行的设置如下图所示：</span><span class="sxs-lookup"><span data-stu-id="f07da-216">When you're done, the settings for the **SchoolContext-Deployment** row in **Database Entries** look like the following illustration:</span></span>

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

<span data-ttu-id="f07da-218">保存对 "**包/发布 SQL** " 选项卡所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-218">Save the changes to the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f07da-219">将*School-Prod*文件从*c:\inetpub\wwwroot\ContosoUniversity\App\_data*文件夹复制到 ContosoUniversity 项目中的*应用\_data*文件夹。</span><span class="sxs-lookup"><span data-stu-id="f07da-219">Copy the *School-Prod.sdf* file from the *c:\inetpub\wwwroot\ContosoUniversity\App\_Data* folder to the *App\_Data* folder in the ContosoUniversity project.</span></span>

### <a name="specifying-transacted-mode-for-the-grant-script"></a><span data-ttu-id="f07da-220">为授予脚本指定事务处理模式</span><span class="sxs-lookup"><span data-stu-id="f07da-220">Specifying Transacted Mode for the Grant Script</span></span>

<span data-ttu-id="f07da-221">部署过程将生成用于部署数据库架构和数据的脚本。</span><span class="sxs-lookup"><span data-stu-id="f07da-221">The deployment process generates scripts that deploy the database schema and data.</span></span> <span data-ttu-id="f07da-222">默认情况下，这些脚本在事务中运行。</span><span class="sxs-lookup"><span data-stu-id="f07da-222">By default, these scripts run in a transaction.</span></span> <span data-ttu-id="f07da-223">但是，默认情况下，自定义脚本（如授予脚本）不能在事务中运行。</span><span class="sxs-lookup"><span data-stu-id="f07da-223">However, custom scripts (like the grant scripts) by default do not run in a transaction.</span></span> <span data-ttu-id="f07da-224">如果部署过程混合使用事务模式，则在部署过程中运行脚本时，可能会出现超时错误。</span><span class="sxs-lookup"><span data-stu-id="f07da-224">If the deployment process mixes transaction modes, you might get a timeout error when the scripts run during deployment.</span></span> <span data-ttu-id="f07da-225">在本部分中，将编辑项目文件，以便将自定义脚本配置为在事务中运行。</span><span class="sxs-lookup"><span data-stu-id="f07da-225">In this section, you edit the project file in order to configure the custom scripts to run in a transaction.</span></span>

<span data-ttu-id="f07da-226">在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目，然后选择 "**卸载项目**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-226">In **Solution Explorer**, right-click the **ContosoUniversity** project and select **Unload Project**.</span></span>

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

<span data-ttu-id="f07da-228">然后再次右键单击该项目，然后选择 "**编辑 ContosoUniversity**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-228">Then right-click the project again and select **Edit ContosoUniversity.csproj**.</span></span>

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

<span data-ttu-id="f07da-230">Visual Studio 编辑器会显示项目文件的 XML 内容。</span><span class="sxs-lookup"><span data-stu-id="f07da-230">The Visual Studio editor shows you the XML content of the project file.</span></span> <span data-ttu-id="f07da-231">请注意，有几个 `PropertyGroup` 元素。</span><span class="sxs-lookup"><span data-stu-id="f07da-231">Notice that there are several `PropertyGroup` elements.</span></span> <span data-ttu-id="f07da-232">（在该图中，已省略 `PropertyGroup` 元素的内容。）</span><span class="sxs-lookup"><span data-stu-id="f07da-232">(In the image, the contents of the `PropertyGroup` elements have been omitted.)</span></span>

![项目文件编辑器窗口](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

<span data-ttu-id="f07da-234">第一个没有 `Condition` 属性的是适用于无论生成配置如何适用的设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-234">The first one, which has no `Condition` attribute, is for settings that apply regardless of build configuration.</span></span> <span data-ttu-id="f07da-235">一个 `PropertyGroup` 元素仅适用于调试生成配置（注意 `Condition` 属性），一个仅适用于发布生成配置，另一个仅适用于测试生成配置。</span><span class="sxs-lookup"><span data-stu-id="f07da-235">One `PropertyGroup` element applies only to the Debug build configuration (note the `Condition` attribute), one applies only to the Release build configuration, and one applies only to the Test build configuration.</span></span> <span data-ttu-id="f07da-236">在发布生成配置的 `PropertyGroup` 元素中，你将看到一个 `PublishDatabaseSettings` 元素，其中包含你在 "**包/发布 SQL** " 选项卡上输入的设置。存在与指定的每个 grant 脚本对应的 `Object` 元素（请注意 "Grant" 的两个实例）。</span><span class="sxs-lookup"><span data-stu-id="f07da-236">Within the `PropertyGroup` element for the Release build configuration, you'll see a `PublishDatabaseSettings` element that contains the settings you entered on the **Package/Publish SQL** tab. There is an `Object` element that corresponds to each of the grant scripts you specified (notice the two instances of "Grant.sql").</span></span> <span data-ttu-id="f07da-237">默认情况下，将 `False`每个 grant 脚本的 `Source` 元素的 `Transacted` 属性。</span><span class="sxs-lookup"><span data-stu-id="f07da-237">By default, the `Transacted` attribute of the `Source` element for each grant script is `False`.</span></span>

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

<span data-ttu-id="f07da-239">将 `Source` 元素的 `Transacted` 属性的值更改为 "`True`"。</span><span class="sxs-lookup"><span data-stu-id="f07da-239">Change the value of the `Transacted` attribute of the `Source` element to `True`.</span></span>

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

<span data-ttu-id="f07da-241">保存并关闭项目文件，然后在**解决方案资源管理器**中右键单击该项目，然后选择 "**重新加载项目**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-241">Save and close the project file, and then right-click the project in **Solution Explorer** and select **Reload Project**.</span></span>

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a><span data-ttu-id="f07da-243">设置连接字符串的 web.config 转换</span><span class="sxs-lookup"><span data-stu-id="f07da-243">Setting up Web.Config Transformations for the Connection Strings</span></span>

<span data-ttu-id="f07da-244">在 "**包/发布 SQL** " 选项卡上输入的新 SQL Express 数据库的连接字符串仅 Web 部署用于在部署期间更新目标数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-244">The connection strings for the new SQL Express databases that you entered on the **Package/Publish SQL** tab are used by Web Deploy only for updating the destination database during deployment.</span></span> <span data-ttu-id="f07da-245">你仍必须设置*web.config*转换，以便部署的*web.config*文件中的连接字符串指向新的 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-245">You still have to set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file point to the new SQL Server Express databases.</span></span> <span data-ttu-id="f07da-246">（使用 "**包/发布 SQL** " 选项卡时，无法在发布配置文件中配置连接字符串。）</span><span class="sxs-lookup"><span data-stu-id="f07da-246">(When you use the **Package/Publish SQL** tab, you can't configure connection strings in the publish profile.)</span></span>

<span data-ttu-id="f07da-247">打开*web.config*并将 `connectionStrings` 元素替换为以下示例中的 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="f07da-247">Open *Web.Test.config* and replace the `connectionStrings` element with the `connectionStrings` element in the following example.</span></span> <span data-ttu-id="f07da-248">（请确保仅复制 connectionStrings 元素，而不是此处所示的环绕代码来提供上下文。）</span><span class="sxs-lookup"><span data-stu-id="f07da-248">(Make sure you only copy the connectionStrings element, not the surrounding code that is shown here to provide context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

<span data-ttu-id="f07da-249">此代码会使每个 `add` 元素的 `connectionString` 和 `providerName` 属性替换为*已部署的 web.config 文件*。</span><span class="sxs-lookup"><span data-stu-id="f07da-249">This code causes the `connectionString` and `providerName` attributes of each `add` element to be replaced in the deployed *Web.config* file.</span></span> <span data-ttu-id="f07da-250">这些连接字符串与您在 "**包/发布 SQL** " 选项卡中输入的字符串不同。已将设置 "MultipleActiveResultSets = True" 添加到其中，因为实体框架和通用提供程序需要此设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-250">These connection strings are not identical to the ones you entered in the **Package/Publish SQL** tab. The setting "MultipleActiveResultSets=True" has been added to them because it's required for the Entity Framework and the Universal Providers.</span></span>

## <a name="installing-sql-server-compact"></a><span data-ttu-id="f07da-251">安装 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f07da-251">Installing SQL Server Compact</span></span>

<span data-ttu-id="f07da-252">SqlServerCompact NuGet 包提供 Contoso 大学应用程序的 SQL Server Compact 数据库引擎程序集。</span><span class="sxs-lookup"><span data-stu-id="f07da-252">The SqlServerCompact NuGet package provides the SQL Server Compact database engine assemblies for the Contoso University application.</span></span> <span data-ttu-id="f07da-253">但现在它并不是必须能够读取 SQL Server Compact 数据库的应用程序，Web 部署而是为了创建要在 SQL Server 数据库中运行的脚本。</span><span class="sxs-lookup"><span data-stu-id="f07da-253">But now it is not the application but Web Deploy that must be able to read the SQL Server Compact databases, in order to create scripts to run in the SQL Server databases.</span></span> <span data-ttu-id="f07da-254">若要启用 Web 部署读取 SQL Server Compact 数据库，请使用以下链接在开发计算机上安装 SQL Server Compact： [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)。</span><span class="sxs-lookup"><span data-stu-id="f07da-254">To enable Web Deploy to read SQL Server Compact databases, install SQL Server Compact on the development computer by using the following link: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).</span></span>

## <a name="deploying-to-the-test-environment"></a><span data-ttu-id="f07da-255">部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="f07da-255">Deploying to the Test Environment</span></span>

<span data-ttu-id="f07da-256">若要发布到测试环境，您必须创建一个配置为使用用于数据库发布的 "**包/发布 SQL** " 选项卡而不是 "发布配置文件数据库" 设置的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="f07da-256">In order to publish to the Test environment, you have to create a publish profile that is configured to use the **Package/Publish SQL** tab for database publishing instead of the publish profile database settings.</span></span>

<span data-ttu-id="f07da-257">首先，删除现有的测试配置文件。</span><span class="sxs-lookup"><span data-stu-id="f07da-257">First, delete the existing Test profile.</span></span>

<span data-ttu-id="f07da-258">在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-258">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f07da-259">选择 "**配置文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-259">Select the **Profile** tab.</span></span>

<span data-ttu-id="f07da-260">单击 "**管理配置文件**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-260">Click **Manage Profiles**.</span></span>

<span data-ttu-id="f07da-261">选择 "**测试**"，单击 "**删除**"，然后单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-261">Select **Test**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="f07da-262">关闭 "**发布 Web** " 向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-262">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="f07da-263">接下来，创建一个新的测试配置文件并使用它来发布项目。</span><span class="sxs-lookup"><span data-stu-id="f07da-263">Next, create a new Test profile and use it to publish the project.</span></span>

<span data-ttu-id="f07da-264">在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-264">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f07da-265">选择 "**配置文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-265">Select the **Profile** tab.</span></span>

<span data-ttu-id="f07da-266">从下拉列表中选择 " **&lt;新建 ..."&gt;** ，并输入 "Test" 作为配置文件名称。</span><span class="sxs-lookup"><span data-stu-id="f07da-266">Select **&lt;New...&gt;** from the drop-down list, and enter "Test" as the profile name.</span></span>

<span data-ttu-id="f07da-267">在 "**服务 URL** " 框中，输入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="f07da-267">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="f07da-268">在 "**站点/应用程序**" 框中，输入*Default Web Site/ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="f07da-268">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="f07da-269">在 "**目标 URL** " 框中，输入 `http://localhost/ContosoUniversity/`。</span><span class="sxs-lookup"><span data-stu-id="f07da-269">In the **Destination URL** box, enter `http://localhost/ContosoUniversity/`.</span></span>

<span data-ttu-id="f07da-270">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="f07da-270">Click **Next**.</span></span>

<span data-ttu-id="f07da-271">"**设置**" 选项卡警告你已配置 "**包/发布 SQL** " 选项卡，并且通过单击 "启用新的数据库发布改进"，你可以重写这些选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-271">The **Settings** tab warns you that the **Package/Publish SQL** tab has been configured, and it gives you an opportunity to override them by clicking enable the new database publishing improvements.</span></span> <span data-ttu-id="f07da-272">对于此部署，不想覆盖 "**打包/发布 SQL** " 选项卡设置，只需单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-272">For this deployment you don't want to override the **Package/Publish SQL** tab settings, so just click **Next**.</span></span>

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

<span data-ttu-id="f07da-274">"**预览**" 选项卡上的消息指示**未选择要发布的数据库**，但这仅意味着在发布配置文件中未配置数据库发布。</span><span class="sxs-lookup"><span data-stu-id="f07da-274">A message on the **Preview** tab indicates that **No databases are selected to publish**, but this only means that database publishing is not configured in the publish profile.</span></span>

<span data-ttu-id="f07da-275">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="f07da-275">Click **Publish**.</span></span>

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

<span data-ttu-id="f07da-277">Visual Studio 将部署应用程序，并将浏览器打开到测试环境中站点的主页。</span><span class="sxs-lookup"><span data-stu-id="f07da-277">Visual Studio deploys the application and opens the browser to the home page of the site in the test environment.</span></span> <span data-ttu-id="f07da-278">运行 "讲师" 页，看看它是否显示了你之前看到的相同数据。</span><span class="sxs-lookup"><span data-stu-id="f07da-278">Run the Instructors page to see that it displays the same data that you saw earlier.</span></span> <span data-ttu-id="f07da-279">运行 "**添加学生**" 页，添加一个新的学生，然后在 "**学生**" 页中查看新的学生。</span><span class="sxs-lookup"><span data-stu-id="f07da-279">Run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="f07da-280">这将验证是否可以更新数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-280">This verifies that the you can update the database.</span></span> <span data-ttu-id="f07da-281">选择 "**更新信用额度**" 页（需要登录）以验证是否已部署成员资格数据库并且您有权访问该数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-281">Select the **Update Credits** page (you'll need to log in) to verify that the membership database was deployed and you have access to it.</span></span>

## <a name="creating-a-sql-server-database-for-the-production-environment"></a><span data-ttu-id="f07da-282">为生产环境创建 SQL Server 数据库</span><span class="sxs-lookup"><span data-stu-id="f07da-282">Creating a SQL Server Database for the Production Environment</span></span>

<span data-ttu-id="f07da-283">现在，你已将部署到测试环境，接下来可以设置生产的部署。</span><span class="sxs-lookup"><span data-stu-id="f07da-283">Now that you've deployed to the test environment, you're ready to set up deployment to production.</span></span> <span data-ttu-id="f07da-284">您可以通过创建要部署到的数据库，开始对测试环境执行的操作。</span><span class="sxs-lookup"><span data-stu-id="f07da-284">You begin as you did for the test environment, by creating a database to deploy to.</span></span> <span data-ttu-id="f07da-285">在您想起此概述后，Cytanium Lite 托管计划仅允许单个 SQL Server 数据库，因此您只需要设置一个数据库而不是两个数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-285">As you recall from the Overview, the Cytanium Lite hosting plan only allows a single SQL Server database, so you will set up only one database, not two.</span></span> <span data-ttu-id="f07da-286">成员资格和学校 SQL Server Compact 数据库中的所有表和数据将部署到生产环境中的一个 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-286">All of the tables and data from the membership and School SQL Server Compact databases will be deployed into one SQL Server database in production.</span></span>

<span data-ttu-id="f07da-287">在[http://panel.cytanium.com](http://panel.cytanium.com)中转到 Cytanium 控制面板。</span><span class="sxs-lookup"><span data-stu-id="f07da-287">Go to the Cytanium control panel at [http://panel.cytanium.com](http://panel.cytanium.com).</span></span> <span data-ttu-id="f07da-288">将鼠标停留在**数据库**上，然后单击 " **SQL Server 2008**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-288">Hold the mouse over **Databases** and then click **SQL Server 2008**.</span></span>

<span data-ttu-id="f07da-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="f07da-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span></span>

<span data-ttu-id="f07da-290">在**SQL Server 2008** "页上，单击"**创建数据库**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-290">In the **SQL Server 2008** page, click **Create Database**.</span></span>

<span data-ttu-id="f07da-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="f07da-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span></span>

<span data-ttu-id="f07da-292">将数据库命名为 "School"，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-292">Name the database "School" and click **Save**.</span></span> <span data-ttu-id="f07da-293">（该页面自动添加前缀 "contosou"，因此有效名称将为 "contosouSchool"。）</span><span class="sxs-lookup"><span data-stu-id="f07da-293">(The page automatically adds the prefix "contosou", so the effective name will be "contosouSchool".)</span></span>

<span data-ttu-id="f07da-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="f07da-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span></span>

<span data-ttu-id="f07da-295">在同一页上，单击 "**创建用户**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-295">On the same page, click **Create User**.</span></span> <span data-ttu-id="f07da-296">在 Cytanium 服务器上，而不是使用集成的 Windows 安全性，并让应用程序池标识打开数据库，则将创建一个拥有打开数据库的权限的用户。</span><span class="sxs-lookup"><span data-stu-id="f07da-296">On Cytanium's servers, rather than using integrated Windows security and letting the application pool identity open your database, you'll create a user that has authority to open your database.</span></span> <span data-ttu-id="f07da-297">将用户的凭据添加到生产*web.config*文件中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-297">You'll add the user's credentials to the connection strings that go in the production *Web.config* file.</span></span> <span data-ttu-id="f07da-298">在此步骤中，你将创建这些凭据。</span><span class="sxs-lookup"><span data-stu-id="f07da-298">In this step you create those credentials.</span></span>

<span data-ttu-id="f07da-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="f07da-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span></span>

<span data-ttu-id="f07da-300">在**SQL 用户属性**页中填写必填字段：</span><span class="sxs-lookup"><span data-stu-id="f07da-300">Fill in the required fields in the **SQL User Properties** page:</span></span>

- <span data-ttu-id="f07da-301">输入 "ContosoUniversityUser" 作为名称。</span><span class="sxs-lookup"><span data-stu-id="f07da-301">Enter "ContosoUniversityUser" as the name.</span></span>
- <span data-ttu-id="f07da-302">输入密码。</span><span class="sxs-lookup"><span data-stu-id="f07da-302">Enter a password.</span></span>
- <span data-ttu-id="f07da-303">选择**contosouSchool**作为默认数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-303">Select **contosouSchool** as the default database.</span></span>
- <span data-ttu-id="f07da-304">选中 " **contosouSchool** " 复选框。</span><span class="sxs-lookup"><span data-stu-id="f07da-304">Select the **contosouSchool** check box.</span></span>

<span data-ttu-id="f07da-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="f07da-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span></span>

## <a name="configuring-database-deployment-for-the-production-environment"></a><span data-ttu-id="f07da-306">为生产环境配置数据库部署</span><span class="sxs-lookup"><span data-stu-id="f07da-306">Configuring Database Deployment for the Production Environment</span></span>

<span data-ttu-id="f07da-307">现在，你已准备好在 "**打包/发布 SQL** " 选项卡中设置数据库部署设置，正如之前在测试环境中所做的那样。</span><span class="sxs-lookup"><span data-stu-id="f07da-307">Now you're ready to set up database deployment settings in the **Package/Publish SQL** tab, as you did earlier for the test environment.</span></span>

<span data-ttu-id="f07da-308">打开**项目**的 "属性" 窗口，选择 "**包/发布 SQL** " 选项卡，并确保在 "**配置**" 下拉列表中选择 "**活动（发布）** " 或 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-308">Open the **Project Properties** window, select the **Package/Publish SQL** tab, and make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="f07da-309">为每个数据库配置部署设置时，为生产环境和测试环境执行的操作的主要区别在于如何配置连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-309">When you configure deployment settings for each database, the key difference between what you do for production and test environments is in how you configure connection strings.</span></span> <span data-ttu-id="f07da-310">对于测试环境，你输入了不同的目标数据库连接字符串，但对于生产环境，目标连接字符串对于这两个数据库都是相同的。</span><span class="sxs-lookup"><span data-stu-id="f07da-310">For the test environment you entered different destination database connection strings, but for the production environment the destination connection string will be the same for both databases.</span></span> <span data-ttu-id="f07da-311">这是因为你要将两个数据库部署到生产环境中的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-311">This is because you are deploying both databases to one database in production.</span></span>

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="f07da-312">为成员资格数据库配置部署设置</span><span class="sxs-lookup"><span data-stu-id="f07da-312">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="f07da-313">若要配置应用于成员资格数据库的设置，请在 "**数据库项**" 表中选择 " **DefaultConnection** " 行。</span><span class="sxs-lookup"><span data-stu-id="f07da-313">To configure settings that apply to the membership database, select the **DefaultConnection-Deployment** row in the **Database Entries** table.</span></span>

<span data-ttu-id="f07da-314">在 "**目标数据库的连接字符串**" 中，输入指向刚刚创建的新生产 SQL Server 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-314">In **Connection string for destination database**, enter a connection string that points to the new production SQL Server database that you just created.</span></span> <span data-ttu-id="f07da-315">可以从欢迎电子邮件中获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f07da-315">You can get the connection string from your welcome email.</span></span> <span data-ttu-id="f07da-316">电子邮件的相关部分包含以下示例连接字符串：</span><span class="sxs-lookup"><span data-stu-id="f07da-316">The relevant part of the email contains the following sample connection string:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

<span data-ttu-id="f07da-317">替换这三个变量后，所需的连接字符串如下例所示：</span><span class="sxs-lookup"><span data-stu-id="f07da-317">After you replace the three variables, the connection string you need looks like this example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

<span data-ttu-id="f07da-318">将此连接字符串复制并粘贴到 "**包/发布 SQL** " 选项卡中**目标数据库的连接字符串**中。</span><span class="sxs-lookup"><span data-stu-id="f07da-318">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f07da-319">确保仍选择了**现有数据库中的 "请求数据" 和/或 "架构**"，并且**数据库脚本选项**仍为 "架构" 和 "**数据**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-319">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="f07da-320">在 "**数据库脚本**" 框中，清除 Grant 脚本旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="f07da-320">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="f07da-322">为 School 数据库配置部署设置</span><span class="sxs-lookup"><span data-stu-id="f07da-322">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="f07da-323">接下来，在 "**数据库项**" 表中选择 " **SchoolContext** " 行，以便配置 School 数据库设置。</span><span class="sxs-lookup"><span data-stu-id="f07da-323">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure the School database settings.</span></span>

<span data-ttu-id="f07da-324">将相同的连接字符串复制到为成员资格数据库复制到该字段中的**目标数据库的连接字符串**中。</span><span class="sxs-lookup"><span data-stu-id="f07da-324">Copy the same connection string into **Connection string for destination database** that you copied into that field for the membership database.</span></span>

<span data-ttu-id="f07da-325">确保仍选择了**现有数据库中的 "请求数据" 和/或 "架构**"，并且**数据库脚本选项**仍为 "架构" 和 "**数据**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-325">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="f07da-326">在 "**数据库脚本**" 框中，清除 Grant 脚本旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="f07da-326">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

<span data-ttu-id="f07da-327">保存对 "**包/发布 SQL** " 选项卡所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-327">Save the changes to the **Package/Publish SQL** tab.</span></span>

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a><span data-ttu-id="f07da-328">将连接字符串的 web.config 转换设置为生产数据库</span><span class="sxs-lookup"><span data-stu-id="f07da-328">Setting Up Web.Config Transforms for the Connection Strings to Production Databases</span></span>

<span data-ttu-id="f07da-329">接下来，您将设置*web.config*转换，以便将部署的*web.config*文件中的连接字符串指向新的生产数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-329">Next, you'll set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file to point to the new production database.</span></span> <span data-ttu-id="f07da-330">在 "**包/发布 SQL** " 选项卡上为 Web 部署所输入的连接字符串与应用程序需要使用的连接字符串相同，但添加了 "`MultipleResultSets`" 选项。</span><span class="sxs-lookup"><span data-stu-id="f07da-330">The connection string that you entered on the **Package/Publish SQL** tab for Web Deploy to use is the same as the one the application needs to use, except for the addition of the `MultipleResultSets` option.</span></span>

<span data-ttu-id="f07da-331">打开*web.config*并将 `connectionStrings` 元素替换为 `connectionStrings` 元素，如下面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="f07da-331">Open *Web.Production.config* and replace the `connectionStrings` element with a `connectionStrings` element that looks like the following example.</span></span> <span data-ttu-id="f07da-332">（仅复制 `connectionStrings` 元素，而不是为显示上下文而提供的周围标记。）</span><span class="sxs-lookup"><span data-stu-id="f07da-332">(Only copy the `connectionStrings` element, not the surrounding tags that are provided to show the context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

<span data-ttu-id="f07da-333">有时会看到通知，告诉您*始终对 web.config 文件中*的连接字符串进行加密。</span><span class="sxs-lookup"><span data-stu-id="f07da-333">You sometimes see advice that tells you to always encrypt connection strings in the *Web.config* file.</span></span> <span data-ttu-id="f07da-334">如果要部署到自己公司的网络上的服务器，这可能是合适的。</span><span class="sxs-lookup"><span data-stu-id="f07da-334">This might be appropriate if you were deploying to servers on your own company's network.</span></span> <span data-ttu-id="f07da-335">但是，在部署到共享的宿主环境时，将信任托管提供程序的安全做法，并且不需要或不切实际地对连接字符串进行加密。</span><span class="sxs-lookup"><span data-stu-id="f07da-335">When you are deploying to a shared hosting environment, though, you're trusting the security practices of the hosting provider, and it's not necessary or practical to encrypt the connection strings.</span></span>

## <a name="deploying-to-the-production-environment"></a><span data-ttu-id="f07da-336">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="f07da-336">Deploying to the Production Environment</span></span>

<span data-ttu-id="f07da-337">现在，你已准备好部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="f07da-337">Now you're ready to deploy to production.</span></span> <span data-ttu-id="f07da-338">Web 部署将读取项目*应用\_Data*文件夹中的 SQL Server Compact 数据库，并在生产 SQL Server 数据库中重新创建其所有表和数据。</span><span class="sxs-lookup"><span data-stu-id="f07da-338">Web Deploy will read the SQL Server Compact databases in your project's *App\_Data* folder and re-create all of their tables and data in the production SQL Server database.</span></span> <span data-ttu-id="f07da-339">若要使用 "**打包/发布 Web** " 选项卡设置进行发布，必须为生产创建新的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="f07da-339">In order to publish by using the **Package/Publish Web** tab settings, you have to create a new publish profile for production.</span></span>

<span data-ttu-id="f07da-340">首先，删除现有的生产配置文件，就像之前测试配置文件一样。</span><span class="sxs-lookup"><span data-stu-id="f07da-340">First, delete the existing Production profile as you did the Test profile earlier.</span></span>

<span data-ttu-id="f07da-341">在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-341">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f07da-342">选择 "**配置文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-342">Select the **Profile** tab.</span></span>

<span data-ttu-id="f07da-343">单击 "**管理配置文件**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-343">Click **Manage Profiles**.</span></span>

<span data-ttu-id="f07da-344">选择 "**生产**"，单击 "**删除**"，然后单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-344">Select **Production**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="f07da-345">关闭 "**发布 Web** " 向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-345">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="f07da-346">接下来，创建新的生产配置文件并使用它来发布项目。</span><span class="sxs-lookup"><span data-stu-id="f07da-346">Next, create a new Production profile and use it to publish the project.</span></span>

<span data-ttu-id="f07da-347">在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-347">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f07da-348">选择 "**配置文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-348">Select the **Profile** tab.</span></span>

<span data-ttu-id="f07da-349">单击 "**导入**"，然后选择前面下载的 .publishsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="f07da-349">Click **Import**, and select the .publishsettings file that you downloaded earlier.</span></span>

<span data-ttu-id="f07da-350">在 "**连接**" 选项卡上，将 "**目标 URL** " 更改为正确的临时 URL，在此示例中 http://contosouniversity.com.vserver01.cytanium.com 。</span><span class="sxs-lookup"><span data-stu-id="f07da-350">On the **Connection** tab, change the **Destination URL** to the correct temporary URL, which in this example is http://contosouniversity.com.vserver01.cytanium.com.</span></span>

<span data-ttu-id="f07da-351">将该配置文件重命名为生产。</span><span class="sxs-lookup"><span data-stu-id="f07da-351">Rename the profile to Production.</span></span> <span data-ttu-id="f07da-352">（选择 "**配置文件**" 选项卡，然后单击 "**管理配置文件**"）。</span><span class="sxs-lookup"><span data-stu-id="f07da-352">(Select the **Profile** tab and click **Manage Profiles** to do that).</span></span>

<span data-ttu-id="f07da-353">关闭 "**发布 Web** " 向导以保存你所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-353">Close the **Publish Web** wizard to save your changes.</span></span>

<span data-ttu-id="f07da-354">在实际应用程序中，如果在生产环境中更新数据库，则可以在发布之前执行两个额外的步骤：</span><span class="sxs-lookup"><span data-stu-id="f07da-354">In a real application in which the database was being updated in production, you would do two additional steps now before you publish:</span></span>

1. <span data-ttu-id="f07da-355">如[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中所示，将应用上传到 *\_offline。*</span><span class="sxs-lookup"><span data-stu-id="f07da-355">Upload *app\_offline.htm*, as shown in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span>
2. <span data-ttu-id="f07da-356">使用 Cytanium "控制面板" 的 "**文件管理器**" 功能，将*aspnet-Prod*和*School-Prod*文件从生产站点复制到 ContosoUniversity 项目的 "*应用\_Data* " 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f07da-356">Use the **File Manager** feature of the Cytanium control panel to copy the *aspnet-Prod.sdf* and *School-Prod.sdf* files from the production site to the *App\_Data* folder of the ContosoUniversity project.</span></span> <span data-ttu-id="f07da-357">这可确保正在部署到新 SQL Server 数据库的数据包含生产网站所做的最新更新。</span><span class="sxs-lookup"><span data-stu-id="f07da-357">This ensures that the data you're deploying to the new SQL Server database includes the latest updates made by your production website.</span></span>

<span data-ttu-id="f07da-358">在**Web 一键式发布**工具栏中，确保选择了 "**生产**配置文件"，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-358">In the **Web One Click Publish** toolbar, make sure that the **Production** profile is selected, and then click **Publish**.</span></span>

<span data-ttu-id="f07da-359">如果在发布之前上传<em>\_offline 的应用</em>，则必须使用 Cytanium 控制面板中的 "<strong>文件管理器</strong>" 实用程序来删除<em>脱机应用\_。</em>htm。</span><span class="sxs-lookup"><span data-stu-id="f07da-359">If you uploaded <em>app\_offline.htm</em> before publishing, you have to use the <strong>File Manager</strong> utility in the Cytanium control panel to delete <em>app\_offline.</em>htm before you test.</span></span> <span data-ttu-id="f07da-360">同时，还可以从<em>应用\_Data</em>文件夹中删除<em>.sdf</em>文件。</span><span class="sxs-lookup"><span data-stu-id="f07da-360">You can also at the same time delete the <em>.sdf</em> files from the <em>App\_Data</em> folder.</span></span>

<span data-ttu-id="f07da-361">你现在可以打开浏览器，并使用你的公共网站的 URL 来测试应用程序，就像在部署到测试环境后执行的操作一样。</span><span class="sxs-lookup"><span data-stu-id="f07da-361">You can now open a browser and go to the URL of your public site to test the application the same way you did after deploying to the test environment.</span></span>

## <a name="switching-to-sql-server-express-localdb-in-development"></a><span data-ttu-id="f07da-362">切换到开发 SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="f07da-362">Switching to SQL Server Express LocalDB in Development</span></span>

<span data-ttu-id="f07da-363">如概述中所述，通常最好在用于测试和生产的开发环境中使用相同的数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="f07da-363">As was explained in the Overview, it's generally best to use the same database engine in development that you use in test and production.</span></span> <span data-ttu-id="f07da-364">（请记住，使用开发 SQL Server Express 的优势在于，数据库在开发、测试和生产环境中的工作方式相同。）在本部分中，你将在从 Visual Studio 中运行应用程序时，将 ContosoUniversity 项目设置为使用 SQL Server Express LocalDB。</span><span class="sxs-lookup"><span data-stu-id="f07da-364">(Remember that the advantage to using SQL Server Express in development is that the database will work the same in your development, test, and production environments.) In this section you'll set up the ContosoUniversity project to use SQL Server Express LocalDB when you run the application from Visual Studio.</span></span>

<span data-ttu-id="f07da-365">要执行此迁移，最简单的方法是让 Code First 和成员资格系统为您创建这两个新的开发数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-365">The simplest way to perform this migration is to let Code First and the membership system create both new development databases for you.</span></span> <span data-ttu-id="f07da-366">使用此方法迁移需要三个步骤：</span><span class="sxs-lookup"><span data-stu-id="f07da-366">Using this method to migrate requires three steps:</span></span>

1. <span data-ttu-id="f07da-367">更改连接字符串以指定新的 SQL Express LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-367">Change the connection strings to specify new SQL Express LocalDB databases.</span></span>
2. <span data-ttu-id="f07da-368">运行网站管理工具来创建管理员用户。</span><span class="sxs-lookup"><span data-stu-id="f07da-368">Run the Web Site Administration Tool to create an administrator user.</span></span> <span data-ttu-id="f07da-369">这会创建成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-369">This creates the membership database.</span></span>
3. <span data-ttu-id="f07da-370">使用 Code First 迁移更新数据库命令创建应用程序数据库并设定其种子。</span><span class="sxs-lookup"><span data-stu-id="f07da-370">Use the Code First Migrations update-database command to create and seed the application database.</span></span>

### <a name="updating-connection-strings-in-the-webconfig-file"></a><span data-ttu-id="f07da-371">更新 Web.config 文件中的连接字符串</span><span class="sxs-lookup"><span data-stu-id="f07da-371">Updating Connection Strings in the Web.config file</span></span>

<span data-ttu-id="f07da-372">打开 web.config*文件并*将 `connectionStrings` 元素替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f07da-372">Open the *Web.config* file and replace the `connectionStrings` element with the following code:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a><span data-ttu-id="f07da-373">创建成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="f07da-373">Creating the Membership Database</span></span>

<span data-ttu-id="f07da-374">在**解决方案资源管理器**中，选择 "ContosoUniversity" 项目，然后单击 "**项目**" 菜单中的 " **ASP.NET 配置**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-374">In **Solution Explorer**, select the ContosoUniversity project, and then click **ASP.NET Configuration** in the **Project** menu.</span></span>

<span data-ttu-id="f07da-375">选择“安全”选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-375">Select the Security tab.</span></span>

<span data-ttu-id="f07da-376">单击 "**创建或管理角色**"，然后创建**管理员**角色。</span><span class="sxs-lookup"><span data-stu-id="f07da-376">Click **Create or Manage Roles**, and then create an **Administrator** role.</span></span>

<span data-ttu-id="f07da-377">返回到 "安全" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f07da-377">Return to the Security tab.</span></span>

<span data-ttu-id="f07da-378">单击 "**创建用户**"，然后选中 "**管理员**" 复选框并创建名为 "管理员" 的用户。</span><span class="sxs-lookup"><span data-stu-id="f07da-378">Click **Create user**, and then select the **Administrator** check box and create a user named admin.</span></span>

<span data-ttu-id="f07da-379">关闭**网站管理工具**。</span><span class="sxs-lookup"><span data-stu-id="f07da-379">Close the **Web Site Administration Tool**.</span></span>

### <a name="creating-the-school-database"></a><span data-ttu-id="f07da-380">创建 School 数据库</span><span class="sxs-lookup"><span data-stu-id="f07da-380">Creating the School Database</span></span>

<span data-ttu-id="f07da-381">打开 "包管理器控制台" 窗口。</span><span class="sxs-lookup"><span data-stu-id="f07da-381">Open the Package Manager Console window.</span></span>

<span data-ttu-id="f07da-382">在 "**默认项目**" 下拉列表中，选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="f07da-382">In the **Default project** drop-down list, select the ContosoUniversity.DAL project.</span></span>

<span data-ttu-id="f07da-383">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f07da-383">Enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

<span data-ttu-id="f07da-384">Code First 迁移应用创建数据库的初始迁移，然后应用 AddBirthDate 迁移，然后运行 Seed 方法。</span><span class="sxs-lookup"><span data-stu-id="f07da-384">Code First Migrations applies the Initial migration that creates the database and then applies the AddBirthDate migration, then it runs the Seed method.</span></span>

<span data-ttu-id="f07da-385">按 Ctrl-F5 运行该站点。</span><span class="sxs-lookup"><span data-stu-id="f07da-385">Run the site by pressing Control-F5.</span></span> <span data-ttu-id="f07da-386">与测试环境和生产环境相同，运行 "**添加学生**" 页，添加新的学生，然后在 "**学生**" 页中查看新的学生。</span><span class="sxs-lookup"><span data-stu-id="f07da-386">As you did for the test and production environments, run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="f07da-387">这会验证 School 数据库是否已创建和初始化，以及你是否具有对该数据库的读写访问权限。</span><span class="sxs-lookup"><span data-stu-id="f07da-387">This verifies that the School database was created and initialized and that you have read and write access to it.</span></span>

<span data-ttu-id="f07da-388">选择 "**更新信用额度**" 页，然后登录以验证是否已部署成员资格数据库以及您是否有权访问该数据库。</span><span class="sxs-lookup"><span data-stu-id="f07da-388">Select the **Update Credits** page and log in to verify that the membership database was deployed and that you have access to it.</span></span> <span data-ttu-id="f07da-389">如果你没有迁移你的用户帐户，请创建一个管理员帐户，然后选择 "**更新信用额度**" 页以验证其是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="f07da-389">If you did not migrate your user accounts, create an administrator account and then select the **Update Credits** page to verify that it works.</span></span>

## <a name="cleaning-up-sql-server-compact-files"></a><span data-ttu-id="f07da-390">清理 SQL Server Compact 文件</span><span class="sxs-lookup"><span data-stu-id="f07da-390">Cleaning Up SQL Server Compact Files</span></span>

<span data-ttu-id="f07da-391">你不再需要包含的文件和 NuGet 包来支持 SQL Server Compact。</span><span class="sxs-lookup"><span data-stu-id="f07da-391">You no longer need files and NuGet packages that were included to support SQL Server Compact.</span></span> <span data-ttu-id="f07da-392">如果需要（此步骤不是必需的），可以清除不需要的文件和引用。</span><span class="sxs-lookup"><span data-stu-id="f07da-392">If you want (this step is not required), you can clean up unneeded files and references.</span></span>

<span data-ttu-id="f07da-393">在**解决方案资源管理器**中，从*应用程序\_Data*文件夹中删除 *.sdf*文件，并从*bin*文件夹中删除*amd64*和*x86*文件夹。</span><span class="sxs-lookup"><span data-stu-id="f07da-393">In **Solution Explorer**, delete the *.sdf* files from the *App\_Data* folder and the *amd64* and *x86* folders from the *bin* folder.</span></span>

<span data-ttu-id="f07da-394">在**解决方案资源管理器**中，右键单击该解决方案（不是项目之一），然后单击 "**管理解决方案的 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-394">In **Solution Explorer**, right-click the solution (not one of the projects), and then click **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="f07da-395">在 "**管理 NuGet 包**" 对话框的左窗格中，选择 "**已安装包**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-395">In the left pane of the **Manage NuGet Packages** dialog box, select **Installed packages**.</span></span>

<span data-ttu-id="f07da-396">选择**EntityFramework SqlServerCompact**包，并单击 "**管理**"。</span><span class="sxs-lookup"><span data-stu-id="f07da-396">Select the **EntityFramework.SqlServerCompact** package and click **Manage**.</span></span>

<span data-ttu-id="f07da-397">在 "**选择项目**" 对话框中，这两个项目都处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="f07da-397">In the **Select Projects** dialog box, both projects are selected.</span></span> <span data-ttu-id="f07da-398">若要在这两个项目中卸载包，请清除这两个复选框，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="f07da-398">To uninstall the package in both projects, clear both check boxes, then click **OK**.</span></span>

<span data-ttu-id="f07da-399">在询问是否要卸载依赖包的对话框中，单击 "否"。</span><span class="sxs-lookup"><span data-stu-id="f07da-399">In the dialog box that asks if you want to uninstall the dependent packages also, click No.</span></span> <span data-ttu-id="f07da-400">其中一个是您必须保留的实体框架包。</span><span class="sxs-lookup"><span data-stu-id="f07da-400">One of these is the Entity Framework package that you have to keep.</span></span>

<span data-ttu-id="f07da-401">按照相同的过程卸载**SqlServerCompact**包。</span><span class="sxs-lookup"><span data-stu-id="f07da-401">Follow the same procedure to uninstall the **SqlServerCompact** package.</span></span> <span data-ttu-id="f07da-402">（必须按此顺序卸载包，因为**EntityFramework SqlServerCompact**包依赖于**SqlServerCompact**包。）</span><span class="sxs-lookup"><span data-stu-id="f07da-402">(The packages must be uninstalled in this order because the **EntityFramework.SqlServerCompact** package depends on the **SqlServerCompact** package.)</span></span>

<span data-ttu-id="f07da-403">你现在已成功迁移到 SQL Server Express 和完整 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f07da-403">You have now successfully migrated to SQL Server Express and full SQL Server.</span></span> <span data-ttu-id="f07da-404">在下一教程中，你将进行另一次数据库更改，当你的测试数据库和生产数据库使用 SQL Server Express 和完全 SQL Server 时，你将了解如何部署数据库更改。</span><span class="sxs-lookup"><span data-stu-id="f07da-404">In the next tutorial you'll make another database change, and you'll see how to deploy database changes when your test and production databases use SQL Server Express and full SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f07da-405">[上一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="f07da-405">[Previous](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span></span>
