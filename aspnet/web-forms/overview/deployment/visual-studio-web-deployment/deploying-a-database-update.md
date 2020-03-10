---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署数据库更新 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440786"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="95544-103">使用 Visual Studio 的 ASP.NET Web 部署：部署数据库更新</span><span class="sxs-lookup"><span data-stu-id="95544-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="95544-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="95544-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="95544-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="95544-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="95544-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="95544-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="95544-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="95544-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="95544-108">概述</span><span class="sxs-lookup"><span data-stu-id="95544-108">Overview</span></span>

<span data-ttu-id="95544-109">在本教程中，你将进行数据库更改和相关的代码更改，在 Visual Studio 中测试更改，然后将更新部署到测试、过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="95544-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="95544-110">本教程首先演示如何更新 Code First 迁移管理的数据库，然后，它将演示如何使用 dbDacFx 提供程序更新数据库。</span><span class="sxs-lookup"><span data-stu-id="95544-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="95544-111">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="95544-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="95544-112">使用 Code First 迁移部署数据库更新</span><span class="sxs-lookup"><span data-stu-id="95544-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="95544-113">在本部分中，会将一个出生日期列添加到 `Student` 的 `Person` 基类和 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="95544-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="95544-114">然后更新显示讲师数据的页面，使其显示新列。</span><span class="sxs-lookup"><span data-stu-id="95544-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="95544-115">最后，将所做的更改部署到测试、过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="95544-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="95544-116">向应用程序数据库中的表添加列</span><span class="sxs-lookup"><span data-stu-id="95544-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="95544-117">在*ContosoUniversity*项目中，打开*Person.cs* ，并将以下属性添加到 `Person` 类的末尾（后面应该有两个右大括号）：</span><span class="sxs-lookup"><span data-stu-id="95544-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="95544-118">接下来，更新 `Seed` 方法，使其为新列提供一个值。</span><span class="sxs-lookup"><span data-stu-id="95544-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="95544-119">打开*Migrations\Configuration.cs*并将开始 `var instructors = new List<Instructor>` 的代码块替换为以下代码块，其中包含出生日期信息：</span><span class="sxs-lookup"><span data-stu-id="95544-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="95544-120">生成解决方案，然后打开 "**包管理器控制台**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="95544-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="95544-121">确保 "ContosoUniversity" 仍被选作**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="95544-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="95544-122">在 "**程序包管理器控制台**" 窗口中，选择 " **ContosoUniversity** " 作为**默认项目**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="95544-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="95544-123">此命令完成后，Visual Studio 将打开定义新 `DbMigration` 类的类文件，并在 `Up` 方法中，你可以看到创建新列的代码。</span><span class="sxs-lookup"><span data-stu-id="95544-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="95544-124">`Up` 方法将在您实现更改时创建列，并且 `Down` 方法在您回滚更改时删除列。</span><span class="sxs-lookup"><span data-stu-id="95544-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="95544-126">生成解决方案，然后在 "**包管理器控制台**" 窗口中输入以下命令（请确保 ContosoUniversity 项目仍处于选中状态）：</span><span class="sxs-lookup"><span data-stu-id="95544-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="95544-127">实体框架运行 `Up` 方法，然后运行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="95544-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="95544-128">在 "讲师" 页中显示新列</span><span class="sxs-lookup"><span data-stu-id="95544-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="95544-129">在 ContosoUniversity 项目中，打开 "*指导员*" 并添加新的 "模板" 字段以显示出生日期。</span><span class="sxs-lookup"><span data-stu-id="95544-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="95544-130">在雇用日期和办公室分配之间添加：</span><span class="sxs-lookup"><span data-stu-id="95544-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="95544-131">（如果代码缩进不同步，可以按下 CTRL-K，然后按 CTRL + D 自动重新格式化文件。）</span><span class="sxs-lookup"><span data-stu-id="95544-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="95544-132">运行应用程序，并单击 "**讲师**" 链接。</span><span class="sxs-lookup"><span data-stu-id="95544-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="95544-133">加载页面时，你会看到它具有新的 "出生日期" 字段。</span><span class="sxs-lookup"><span data-stu-id="95544-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![包含出生日期的指导员页面](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="95544-135">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="95544-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="95544-136">部署数据库更新</span><span class="sxs-lookup"><span data-stu-id="95544-136">Deploy the database update</span></span>

1. <span data-ttu-id="95544-137">在**解决方案资源管理器**选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="95544-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="95544-138">在**Web 一键式发布**工具栏中，单击 "**测试**发布配置文件"，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="95544-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="95544-139">（如果禁用工具栏，请在**解决方案资源管理器**中选择 ContosoUniversity 项目。）</span><span class="sxs-lookup"><span data-stu-id="95544-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="95544-140">Visual Studio 将部署更新后的应用程序，浏览器将打开主页。</span><span class="sxs-lookup"><span data-stu-id="95544-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="95544-141">运行 "**讲师**" 页，验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="95544-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="95544-142">当应用程序尝试访问此页的数据库时，Code First 更新数据库架构并运行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="95544-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="95544-143">显示页面后，会看到 "预期的**出生日期**" 列中包含日期。</span><span class="sxs-lookup"><span data-stu-id="95544-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="95544-144">在**Web 一键式发布**工具栏中，单击 "**过渡**发布配置文件"，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="95544-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="95544-145">在过渡环境中运行**讲师**页，验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="95544-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="95544-146">在**Web 一键式发布**工具栏中，单击 "**生产**" 发布配置文件，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="95544-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="95544-147">在生产环境中运行**讲师**页，验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="95544-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="95544-148">对于包含数据库更改的实际生产应用程序更新，通常还会在部署过程中使应用程序脱机，如前一教程中所述，使用*应用\_"脱机*"。</span><span class="sxs-lookup"><span data-stu-id="95544-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="95544-149">使用 dbDacFx 提供程序部署数据库更新</span><span class="sxs-lookup"><span data-stu-id="95544-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="95544-150">在本部分中，将向成员资格数据库中的*用户*表添加*备注*列，并创建一个页面，用于显示和编辑每个用户的注释。</span><span class="sxs-lookup"><span data-stu-id="95544-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="95544-151">然后，将所做的更改部署到测试、过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="95544-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="95544-152">向成员资格数据库中的表添加列</span><span class="sxs-lookup"><span data-stu-id="95544-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="95544-153">在 Visual Studio 中，打开**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="95544-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="95544-154">展开 **（localdb） \v11.0**，展开 "**数据库**"，展开 " **ContosoUniversity** " （非**aspnet-ContosoUniversity**），然后展开 "**表**"。</span><span class="sxs-lookup"><span data-stu-id="95544-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="95544-155">如果在**SQL Server** "节点下看不到" **（localdb） \v11.0** "，请右键单击" **SQL Server** "节点，然后单击"**添加 SQL Server**"。</span><span class="sxs-lookup"><span data-stu-id="95544-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="95544-156">在 "**连接到服务器**" 对话框中，输入 *（localdb） \v11.0*作为**服务器名称**，然后单击 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="95544-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="95544-157">如果看不到**ContosoUniversity**，请运行项目并使用*管理员*凭据登录（password 为*devpwd*），然后刷新**SQL Server 对象资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="95544-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="95544-158">右键单击 "**用户**" 表，然后单击 "**视图设计器**"。</span><span class="sxs-lookup"><span data-stu-id="95544-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX 视图设计器](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="95544-160">在设计器中，添加 "*注释*" 列并将其设置为*nvarchar （128）* ，然后单击 "**更新**"。</span><span class="sxs-lookup"><span data-stu-id="95544-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![添加注释列](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="95544-162">在 "**预览数据库更新**" 框中，单击 "**更新数据库**"。</span><span class="sxs-lookup"><span data-stu-id="95544-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![预览数据库更新](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="95544-164">创建页面以显示和编辑新列</span><span class="sxs-lookup"><span data-stu-id="95544-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="95544-165">在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目中的**帐户**文件夹，单击 "**添加**"，然后单击 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="95544-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="95544-166">使用母版页创建新的**Web 窗体**，并将其命名为 "*用户"。*</span><span class="sxs-lookup"><span data-stu-id="95544-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="95544-167">接受默认的*Site master*文件作为母版页。</span><span class="sxs-lookup"><span data-stu-id="95544-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="95544-168">将以下标记复制到 `MainContent` `Content` 元素（3个 `Content` 元素的最后一个元素）：</span><span class="sxs-lookup"><span data-stu-id="95544-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="95544-169">右键单击 "*用户*" 页，然后单击 "**在浏览器中查看**"。</span><span class="sxs-lookup"><span data-stu-id="95544-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="95544-170">使用*管理员*用户凭据（密码为*devpwd*）登录，并向用户添加一些注释以验证该页是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="95544-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![用户页](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="95544-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="95544-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="95544-173">部署数据库更新</span><span class="sxs-lookup"><span data-stu-id="95544-173">Deploy the database update</span></span>

<span data-ttu-id="95544-174">若要使用 dbDacFx 提供程序进行部署，只需在发布配置文件中选择 "**更新数据库**" 选项。</span><span class="sxs-lookup"><span data-stu-id="95544-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="95544-175">但是，在使用此选项时，对于初始部署，还配置了一些其他要运行的 SQL 脚本：这些脚本仍在配置文件中，必须阻止它们再次运行。</span><span class="sxs-lookup"><span data-stu-id="95544-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="95544-176">右键单击 "ContosoUniversity" 项目并单击 "**发布**"，打开 "**发布 Web** " 向导。</span><span class="sxs-lookup"><span data-stu-id="95544-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="95544-177">选择**测试**配置文件。</span><span class="sxs-lookup"><span data-stu-id="95544-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="95544-178">单击 **“设置”** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="95544-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="95544-179">在**DefaultConnection**下，选择 "**更新数据库**"。</span><span class="sxs-lookup"><span data-stu-id="95544-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="95544-180">禁用您配置为初始部署运行的其他脚本：</span><span class="sxs-lookup"><span data-stu-id="95544-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="95544-181">单击 "**配置数据库更新**"。</span><span class="sxs-lookup"><span data-stu-id="95544-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="95544-182">在 "**配置数据库更新**" 对话框中，清除 " *Grant* " 和 " *aspnet-data-dev*" 旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="95544-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="95544-183">单击“关闭”。</span><span class="sxs-lookup"><span data-stu-id="95544-183">Click **Close**.</span></span>
6. <span data-ttu-id="95544-184">单击 **预览** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="95544-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="95544-185">在**DefaultConnection**下的 "**数据库**" 下，单击 "**预览数据库**" 链接。</span><span class="sxs-lookup"><span data-stu-id="95544-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![数据库预览](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="95544-187">预览窗口显示将在目标数据库中运行的脚本，以使该数据库架构与源数据库的架构匹配。</span><span class="sxs-lookup"><span data-stu-id="95544-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="95544-188">该脚本包含一个用于添加新列的 ALTER TABLE 命令。</span><span class="sxs-lookup"><span data-stu-id="95544-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="95544-189">关闭 "**数据库预览**" 对话框，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="95544-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="95544-190">Visual Studio 将部署更新后的应用程序，浏览器将打开主页。</span><span class="sxs-lookup"><span data-stu-id="95544-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="95544-191">运行 "用户信息" 页（向主页 URL 添加*帐户/用户*类型），验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="95544-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="95544-192">必须输入*admin*和*devpwd*登录。</span><span class="sxs-lookup"><span data-stu-id="95544-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="95544-193">默认情况下，表中的数据不会进行部署，并且你没有配置要运行的数据部署脚本，因此你不会发现在开发中添加的注释。</span><span class="sxs-lookup"><span data-stu-id="95544-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="95544-194">你现在可以在 "过渡" 中添加新的注释，以验证是否已将更改部署到数据库，并且页面是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="95544-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="95544-195">按照相同的过程部署到过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="95544-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="95544-196">别忘了禁用多余的脚本。</span><span class="sxs-lookup"><span data-stu-id="95544-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="95544-197">与测试配置文件相比，唯一的区别在于，你只会在暂存和生产配置文件中禁用一个脚本，因为它们配置为仅运行*aspnet-prod-data*。</span><span class="sxs-lookup"><span data-stu-id="95544-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="95544-198">用于过渡和生产的凭据为 admin 和 prodpwd。</span><span class="sxs-lookup"><span data-stu-id="95544-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="95544-199">对于包含数据库更改的实际生产应用程序更新，通常还需要在部署过程中将应用程序脱机，方法是在发布和删除应用程序后将其上载 *\_* ，如[前一教程](deploying-a-code-update.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="95544-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="95544-200">摘要</span><span class="sxs-lookup"><span data-stu-id="95544-200">Summary</span></span>

<span data-ttu-id="95544-201">现在，你已部署了一个应用程序更新，其中包含使用 Code First 迁移和 dbDacFx 提供程序的数据库更改。</span><span class="sxs-lookup"><span data-stu-id="95544-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![包含出生日期的指导员页面](deploying-a-database-update/_static/image8.png)

![用户页](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="95544-204">下一教程将演示如何使用命令行执行部署。</span><span class="sxs-lookup"><span data-stu-id="95544-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95544-205">[上一页](deploying-a-code-update.md)
> [下一页](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="95544-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
