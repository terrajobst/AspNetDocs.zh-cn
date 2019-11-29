---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署 SQL Server 数据库更新-11 of 12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621091"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="8e31b-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署 SQL Server 数据库更新-11 （共12个）</span><span class="sxs-lookup"><span data-stu-id="8e31b-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="8e31b-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8e31b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8e31b-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="8e31b-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="8e31b-106">本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="8e31b-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="8e31b-107">如果安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="8e31b-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="8e31b-108">有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="8e31b-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="8e31b-109">有关显示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Microsoft Azure 网站，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8e31b-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="8e31b-110">概述</span><span class="sxs-lookup"><span data-stu-id="8e31b-110">Overview</span></span>

<span data-ttu-id="8e31b-111">本教程介绍如何将数据库更新部署到完整的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="8e31b-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="8e31b-112">由于 Code First 迁移执行更新数据库的所有工作，因此该过程与[部署数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程中的 SQL Server Compact 过程几乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="8e31b-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="8e31b-113">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="8e31b-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="8e31b-114">向表中添加新列</span><span class="sxs-lookup"><span data-stu-id="8e31b-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="8e31b-115">在本教程的此部分中，你将进行数据库更改和相应的代码更改，然后在 Visual Studio 中对其进行测试，以便准备将其部署到测试环境和生产环境中。</span><span class="sxs-lookup"><span data-stu-id="8e31b-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="8e31b-116">此更改涉及到将 `OfficeHours` 列添加到 `Instructor` 实体，并在**讲师**网页中显示新信息。</span><span class="sxs-lookup"><span data-stu-id="8e31b-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="8e31b-117">在 ContosoUniversity 项目中，打开*Instructor.cs*并在 `HireDate` 和 `Courses` 属性之间添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="8e31b-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="8e31b-118">更新初始值设定项类，以便它将新列与测试数据进行种子设定。</span><span class="sxs-lookup"><span data-stu-id="8e31b-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="8e31b-119">打开*Migrations\Configuration.cs*并将开始 `var instructors = new List<Instructor>` 的代码块替换为以下代码块，其中包含新列：</span><span class="sxs-lookup"><span data-stu-id="8e31b-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="8e31b-120">在 ContosoUniversity 项目中 *，打开 ""，然后*在第一个 `GridView` 控件中的 "结束 `</Columns>` 标记之前，添加一个新的" 模板 "字段：</span><span class="sxs-lookup"><span data-stu-id="8e31b-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="8e31b-121">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="8e31b-121">Build the solution.</span></span>

<span data-ttu-id="8e31b-122">打开 "**程序包管理器控制台**" 窗口，并选择 "ContosoUniversity" 作为**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="8e31b-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="8e31b-123">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="8e31b-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="8e31b-124">运行应用程序并选择 "**讲师**" 页。</span><span class="sxs-lookup"><span data-stu-id="8e31b-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="8e31b-125">加载页面所需的时间比平时长，这是因为实体框架会重新创建数据库，并使用测试数据对其进行种子设定。</span><span class="sxs-lookup"><span data-stu-id="8e31b-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="8e31b-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8e31b-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="8e31b-127">将数据库更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="8e31b-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="8e31b-128">使用 Code First 迁移时，将数据库更改部署到 SQL Server 的方法与 SQL Server Compact 相同。</span><span class="sxs-lookup"><span data-stu-id="8e31b-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="8e31b-129">但是，您必须更改测试发布配置文件，因为它仍设置为从 SQL Server Compact 迁移到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="8e31b-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="8e31b-130">第一步是删除在上一教程中创建的连接字符串转换。</span><span class="sxs-lookup"><span data-stu-id="8e31b-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="8e31b-131">不再需要这些信息，因为你将在发布配置文件中指定连接字符串转换，就像你在配置 "**包/发布 SQL** " 选项卡以便迁移到 SQL Server 之前所做的那样。</span><span class="sxs-lookup"><span data-stu-id="8e31b-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="8e31b-132">打开*web.config*文件并删除 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="8e31b-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="8e31b-133">*Web.config*文件中唯一剩余的转换用于 `appSettings` 元素中的 `Environment` 值。</span><span class="sxs-lookup"><span data-stu-id="8e31b-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="8e31b-134">现在，你可以更新发布配置文件并发布到测试环境。</span><span class="sxs-lookup"><span data-stu-id="8e31b-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="8e31b-135">打开 "**发布 Web** " 向导，然后切换到 "**配置文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8e31b-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="8e31b-136">选择 "**测试**发布配置文件"。</span><span class="sxs-lookup"><span data-stu-id="8e31b-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="8e31b-137">选择“设置”选项卡。</span><span class="sxs-lookup"><span data-stu-id="8e31b-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="8e31b-138">单击 **"启用新的数据库发布改进"** 。</span><span class="sxs-lookup"><span data-stu-id="8e31b-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="8e31b-139">在**SchoolContext**的 "连接字符串" 框中，输入在上一教程中用于*web.config*转换文件的相同值：</span><span class="sxs-lookup"><span data-stu-id="8e31b-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="8e31b-140">选择 **"执行 Code First 迁移（在应用程序启动时运行）** 。</span><span class="sxs-lookup"><span data-stu-id="8e31b-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="8e31b-141">（在你的 Visual Studio 版本中，此复选框可能标记为**Apply Code First 迁移**。）</span><span class="sxs-lookup"><span data-stu-id="8e31b-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="8e31b-142">在**DefaultConnection**的 "连接字符串" 框中，输入在上一教程中用于*web.config*转换文件的相同值：</span><span class="sxs-lookup"><span data-stu-id="8e31b-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="8e31b-143">清除 "**更新数据库**"。</span><span class="sxs-lookup"><span data-stu-id="8e31b-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="8e31b-144">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="8e31b-144">Click **Publish**.</span></span>

<span data-ttu-id="8e31b-145">Visual Studio 将代码更改部署到测试环境，并将浏览器打开到 Contoso 大学主页。</span><span class="sxs-lookup"><span data-stu-id="8e31b-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="8e31b-146">选择 "讲师" 页。</span><span class="sxs-lookup"><span data-stu-id="8e31b-146">Select the Instructors page.</span></span>

<span data-ttu-id="8e31b-147">当应用程序运行此页时，它会尝试访问数据库。</span><span class="sxs-lookup"><span data-stu-id="8e31b-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="8e31b-148">Code First 迁移检查数据库是否是最新的，并且发现尚未应用最新的迁移。</span><span class="sxs-lookup"><span data-stu-id="8e31b-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="8e31b-149">Code First 迁移将应用最新的迁移，运行 `Seed` 方法，然后此页面就会正常运行。</span><span class="sxs-lookup"><span data-stu-id="8e31b-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="8e31b-150">将看到 "新的办公时间" 列，其中包含种子数据。</span><span class="sxs-lookup"><span data-stu-id="8e31b-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="8e31b-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8e31b-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="8e31b-152">将数据库更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="8e31b-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="8e31b-153">还必须更改生产环境的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="8e31b-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="8e31b-154">在这种情况下，你将删除现有的配置文件，并通过导入已更新的 .publishsettings 文件来创建一个新的配置文件。</span><span class="sxs-lookup"><span data-stu-id="8e31b-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="8e31b-155">更新后的文件将包括位于 Cytanium 的 SQL Server 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="8e31b-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="8e31b-156">正如你在将部署到测试环境时所看到的那样，在*web.config*转换文件中不再需要连接字符串转换。</span><span class="sxs-lookup"><span data-stu-id="8e31b-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="8e31b-157">打开该文件并删除 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="8e31b-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="8e31b-158">其余转换适用于 `appSettings` 元素中的 `Environment` 值和限制访问 Elmah 错误报告的 `location` 元素。</span><span class="sxs-lookup"><span data-stu-id="8e31b-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="8e31b-159">在为生产创建新的发布配置文件之前，请使用与在[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)中的步骤相同的方法下载已更新的 .publishsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="8e31b-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="8e31b-160">（在 Cytanium 控制面板中，单击 "**网站**"，然后单击 " **contosouniversity.com** " 网站。</span><span class="sxs-lookup"><span data-stu-id="8e31b-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="8e31b-161">选择 " **Web 发布**" 选项卡，然后单击 "**下载此网站的发布配置文件**"。）执行此操作的原因是在 .publishsettings 文件中选取数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="8e31b-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="8e31b-162">首次下载该文件时，无法使用该连接字符串，因为你仍在使用 SQL Server Compact 并且尚未在 Cytanium 上创建 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="8e31b-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="8e31b-163">现在，你可以更新发布配置文件并发布到生产环境。</span><span class="sxs-lookup"><span data-stu-id="8e31b-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="8e31b-164">打开 "**发布 Web** " 向导，然后切换到 "**配置文件**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8e31b-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="8e31b-165">单击 "**管理配置文件**"，然后删除生产配置文件。</span><span class="sxs-lookup"><span data-stu-id="8e31b-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="8e31b-166">关闭 "**发布 Web** " 向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="8e31b-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="8e31b-167">再次打开 "**发布 Web** " 向导，然后单击 "**导入**"。</span><span class="sxs-lookup"><span data-stu-id="8e31b-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="8e31b-168">如果使用的是临时 URL，请在 "**连接**" 选项卡上将 "**目标 URL** " 更改为适当的值。</span><span class="sxs-lookup"><span data-stu-id="8e31b-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="8e31b-169">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="8e31b-169">Click **Next**.</span></span>

<span data-ttu-id="8e31b-170">在 "**设置**" 选项卡上，单击 **"启用新的数据库发布改进"** 。</span><span class="sxs-lookup"><span data-stu-id="8e31b-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="8e31b-171">在**SchoolContext**的 "连接字符串" 下拉列表中，选择 "Cytanium 连接字符串"。</span><span class="sxs-lookup"><span data-stu-id="8e31b-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="8e31b-173">选择 **"执行 Code First 迁移（在应用程序启动时运行）"** 。</span><span class="sxs-lookup"><span data-stu-id="8e31b-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="8e31b-174">在**DefaultConnection**的 "连接字符串" 下拉列表中，选择 "Cytanium 连接字符串"。</span><span class="sxs-lookup"><span data-stu-id="8e31b-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="8e31b-175">选择 "**配置文件**" 选项卡，单击 "**管理配置文件**"，然后将配置文件从 "contosouniversity.com-Web 部署" 重命名为 "生产"。</span><span class="sxs-lookup"><span data-stu-id="8e31b-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="8e31b-176">关闭 "发布配置文件" 以保存更改，然后重新打开它。</span><span class="sxs-lookup"><span data-stu-id="8e31b-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="8e31b-177">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="8e31b-177">Click **Publish**.</span></span> <span data-ttu-id="8e31b-178">（对于实际的生产网站，你会将*应用\_脱机*复制到生产，并将其放在项目文件夹中，然后再发布，然后在部署完成后将其删除。）</span><span class="sxs-lookup"><span data-stu-id="8e31b-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="8e31b-179">Visual Studio 将代码更改部署到测试环境，并将浏览器打开到 Contoso 大学主页。</span><span class="sxs-lookup"><span data-stu-id="8e31b-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="8e31b-180">选择 "讲师" 页。</span><span class="sxs-lookup"><span data-stu-id="8e31b-180">Select the Instructors page.</span></span>

<span data-ttu-id="8e31b-181">Code First 迁移更新数据库的方式与在测试环境中的更新方式相同。</span><span class="sxs-lookup"><span data-stu-id="8e31b-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="8e31b-182">将看到 "新的办公时间" 列，其中包含种子数据。</span><span class="sxs-lookup"><span data-stu-id="8e31b-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="8e31b-184">现在，使用 SQL Server 数据库，已成功部署了包含数据库更改的应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="8e31b-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="8e31b-185">详细信息</span><span class="sxs-lookup"><span data-stu-id="8e31b-185">More Information</span></span>

<span data-ttu-id="8e31b-186">这将完成这一系列教程，介绍如何将 ASP.NET web 应用程序部署到第三方托管提供程序。</span><span class="sxs-lookup"><span data-stu-id="8e31b-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="8e31b-187">有关这些教程中所涉及的任何主题的详细信息，请参阅 MSDN 网站上的[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e31b-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="8e31b-188">致谢</span><span class="sxs-lookup"><span data-stu-id="8e31b-188">Acknowledgements</span></span>

<span data-ttu-id="8e31b-189">我想感谢以下人员对本系列教程的内容进行了重大贡献：</span><span class="sxs-lookup"><span data-stu-id="8e31b-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="8e31b-190">Alberto Poblacion，MVP &amp; MCT，西班牙</span><span class="sxs-lookup"><span data-stu-id="8e31b-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="8e31b-191">Jarod Ferguson，数据平台开发 MVP，美国</span><span class="sxs-lookup"><span data-stu-id="8e31b-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="8e31b-192">恶劣 Mittal，Microsoft</span><span class="sxs-lookup"><span data-stu-id="8e31b-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="8e31b-193">Kristina Olson，Microsoft</span><span class="sxs-lookup"><span data-stu-id="8e31b-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="8e31b-194">Mike Pope，Microsoft</span><span class="sxs-lookup"><span data-stu-id="8e31b-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="8e31b-195">Mohit Srivastava，Microsoft</span><span class="sxs-lookup"><span data-stu-id="8e31b-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="8e31b-196">Raffaele Rialdi，意大利</span><span class="sxs-lookup"><span data-stu-id="8e31b-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="8e31b-197">Microsoft Rick Anderson</span><span class="sxs-lookup"><span data-stu-id="8e31b-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="8e31b-198">[Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）</span><span class="sxs-lookup"><span data-stu-id="8e31b-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="8e31b-199">[Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）</span><span class="sxs-lookup"><span data-stu-id="8e31b-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="8e31b-200">[Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）</span><span class="sxs-lookup"><span data-stu-id="8e31b-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="8e31b-201">Srđan Božović，塞尔维亚</span><span class="sxs-lookup"><span data-stu-id="8e31b-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="8e31b-202">[Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）</span><span class="sxs-lookup"><span data-stu-id="8e31b-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e31b-203">[上一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="8e31b-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
