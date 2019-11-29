---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署数据库更新-9 （共12个） |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74581985"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="7d7d0-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署数据库更新-9 （共12个）</span><span class="sxs-lookup"><span data-stu-id="7d7d0-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>

<span data-ttu-id="7d7d0-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7d7d0-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7d7d0-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="7d7d0-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="7d7d0-106">本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="7d7d0-107">如果安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="7d7d0-108">有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="7d7d0-109">有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7d7d0-110">概述</span><span class="sxs-lookup"><span data-stu-id="7d7d0-110">Overview</span></span>

<span data-ttu-id="7d7d0-111">在本教程中，你将进行数据库更改和相关代码更改，在 Visual Studio 中测试更改，然后将更新部署到测试和生产环境中。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="7d7d0-112">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="7d7d0-113">向表中添加新列</span><span class="sxs-lookup"><span data-stu-id="7d7d0-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="7d7d0-114">在本部分中，会将一个出生日期列添加到 `Student` 的 `Person` 基类和 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="7d7d0-115">然后更新显示讲师数据的页面，使其显示新列。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="7d7d0-116">在*ContosoUniversity*项目中，打开*Person.cs* ，并将以下属性添加到 `Person` 类的末尾（后面应该有两个右大括号）：</span><span class="sxs-lookup"><span data-stu-id="7d7d0-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="7d7d0-117">接下来，更新种子方法，使其为新列提供一个值。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="7d7d0-118">打开*Migrations\Configuration.cs*并将开始 `var instructors = new List<Instructor>` 的代码块替换为以下代码块，其中包含出生日期信息：</span><span class="sxs-lookup"><span data-stu-id="7d7d0-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="7d7d0-119">在 ContosoUniversity 项目中，打开 "*指导员*" 并添加新的 "模板" 字段以显示出生日期。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="7d7d0-120">在雇用日期和办公室分配之间添加：</span><span class="sxs-lookup"><span data-stu-id="7d7d0-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="7d7d0-121">（如果代码缩进不同步，可以按下 CTRL-K，然后按 CTRL + D 自动重新格式化文件。）</span><span class="sxs-lookup"><span data-stu-id="7d7d0-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="7d7d0-122">生成解决方案，然后打开 "**包管理器控制台**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="7d7d0-123">确保 "ContosoUniversity" 仍被选作**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="7d7d0-124">在 "**程序包管理器控制台**" 窗口中，选择 " **ContosoUniversity** " 作为**默认项目**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7d7d0-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="7d7d0-125">此命令完成后，Visual Studio 将打开定义新 `DbMigration` 类的类文件，并在 `Up` 方法中，你可以看到创建新列的代码。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="7d7d0-127">生成解决方案，然后在 "**包管理器控制台**" 窗口中输入以下命令（请确保 ContosoUniversity 项目仍处于选中状态）：</span><span class="sxs-lookup"><span data-stu-id="7d7d0-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="7d7d0-128">命令完成后，运行应用程序并选择 "讲师" 页。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="7d7d0-129">加载页面时，你会看到它具有新的 "出生日期" 字段。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="7d7d0-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="7d7d0-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="7d7d0-131">将数据库更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="7d7d0-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="7d7d0-132">在**解决方案资源管理器**选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="7d7d0-133">在**Web 一键式发布**工具栏中，选择 "**测试**发布" 配置文件，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="7d7d0-134">（如果禁用工具栏，请在**解决方案资源管理器**中选择 ContosoUniversity 项目。）</span><span class="sxs-lookup"><span data-stu-id="7d7d0-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="7d7d0-135">Visual Studio 将部署更新后的应用程序，浏览器将打开主页。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="7d7d0-136">运行 "讲师" 页，验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="7d7d0-137">当应用程序尝试访问此页的数据库时，Code First 更新数据库架构并运行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="7d7d0-138">显示页面后，会看到 "预期的**出生日期**" 列中包含日期。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="7d7d0-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7d7d0-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="7d7d0-140">将数据库更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="7d7d0-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="7d7d0-141">你现在可以部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-141">You can now deploy to production.</span></span> <span data-ttu-id="7d7d0-142">唯一的区别在于，您将使用*应用程序\_"脱机*" 来防止用户访问该站点，从而在部署更改时更新数据库。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="7d7d0-143">对于生产部署，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="7d7d0-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="7d7d0-144">将*应用\_脱机*文件上传到生产站点。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="7d7d0-145">在 Visual Studio 中，在 Web 中选择 "生产" 配置文件，**单击 "发布**" 工具栏，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="7d7d0-146">从生产站点中删除*应用\_脱机 .htm*文件。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="7d7d0-147">当应用程序在生产环境中使用时，应实现备份计划。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="7d7d0-148">也就是说，应定期将*School-Prod*和*aspnet-Prod*文件从生产站点复制到安全的存储位置，并且应保留多代此类备份。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="7d7d0-149">更新数据库时，应立即从更改之前创建备份副本。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="7d7d0-150">然后，如果您在将其部署到生产环境之前，不会发现该错误，则您仍然能够将数据库恢复到其损坏之前的状态。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>

<span data-ttu-id="7d7d0-151">当 Visual Studio 在浏览器中打开主页 URL 时，将显示 "*应用\_offline* " 页。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="7d7d0-152">*\_脱机*文件删除应用后，你可以再次浏览到你的主页，以验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="7d7d0-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="7d7d0-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="7d7d0-154">现在，你已部署了一个应用程序更新，其中包括对测试和生产的数据库更改。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="7d7d0-155">下一教程介绍如何将数据库从 SQL Server Compact 迁移到 SQL Server Express 和 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="7d7d0-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7d7d0-156">[上一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="7d7d0-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
