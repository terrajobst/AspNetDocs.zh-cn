---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署仅限代码的更新-8 of 12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572789"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="296be-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署仅限代码的更新-8 （共12个）</span><span class="sxs-lookup"><span data-stu-id="296be-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>

<span data-ttu-id="296be-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="296be-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="296be-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="296be-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="296be-106">本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="296be-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="296be-107">如果安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="296be-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="296be-108">有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="296be-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="296be-109">有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="296be-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="296be-110">概述</span><span class="sxs-lookup"><span data-stu-id="296be-110">Overview</span></span>

<span data-ttu-id="296be-111">初始部署完成后，你维护和开发网站的工作将继续进行，在此之前，你将需要部署更新。</span><span class="sxs-lookup"><span data-stu-id="296be-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="296be-112">本教程将指导你完成将更新部署到应用程序代码的过程。</span><span class="sxs-lookup"><span data-stu-id="296be-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="296be-113">此更新不涉及数据库更改;在下一教程中，你将看到有关部署数据库更改的不同之处。</span><span class="sxs-lookup"><span data-stu-id="296be-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="296be-114">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="296be-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="296be-115">更改代码</span><span class="sxs-lookup"><span data-stu-id="296be-115">Making a Code Change</span></span>

<span data-ttu-id="296be-116">作为应用程序更新的简单示例，你将向**讲师**页添加选定讲师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="296be-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="296be-117">如果您运行的是**讲师**页，您会注意到网格中有**选择**的链接，但除了使行背景变为灰色以外，它们不会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="296be-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="296be-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="296be-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="296be-119">现在，你将添加在单击 "**选择**" 链接时运行的代码，并显示所选指导员讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="296be-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="296be-120">在*default.aspx*中，在**ErrorMessageLabel** `Label` 控件后立即添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="296be-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="296be-121">运行页面并选择一个指导员。</span><span class="sxs-lookup"><span data-stu-id="296be-121">Run the page and select an instructor.</span></span> <span data-ttu-id="296be-122">你将看到该教师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="296be-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="296be-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="296be-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="296be-124">将代码更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="296be-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="296be-125">部署到测试环境只需再次运行一次单击 "发布" 即可。</span><span class="sxs-lookup"><span data-stu-id="296be-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="296be-126">若要使此过程更快，你可以使用**Web 一键式发布**工具栏。</span><span class="sxs-lookup"><span data-stu-id="296be-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="296be-127">在 "**视图**" 菜单中选择 "**工具栏**"，然后选择 **"Web 一键式发布"** 。</span><span class="sxs-lookup"><span data-stu-id="296be-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="296be-129">在**解决方案资源管理器**中，选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="296be-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="296be-130">**Web 一键式发布**工具栏上，选择 "**测试**发布配置文件"，然后单击 "**发布 Web** " （其箭头指向左侧和右侧的图标）。</span><span class="sxs-lookup"><span data-stu-id="296be-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="296be-132">Visual Studio 将部署更新后的应用程序，浏览器会自动打开到主页。</span><span class="sxs-lookup"><span data-stu-id="296be-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="296be-133">运行 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="296be-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="296be-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="296be-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="296be-135">通常情况下，还会进行回归测试（即，测试站点的其余部分以确保新的更改不会破坏现有的任何功能）。</span><span class="sxs-lookup"><span data-stu-id="296be-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="296be-136">但对于本教程，你将跳过该步骤并继续将更新部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="296be-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="296be-137">阻止将初始数据库状态重新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="296be-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="296be-138">在实际应用程序中，用户在初次部署后与生产站点进行交互，并使用实时数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="296be-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="296be-139">因此，您不希望在其初始状态下重新部署成员资格数据库，这会擦除所有实时数据。</span><span class="sxs-lookup"><span data-stu-id="296be-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="296be-140">由于 SQL Server Compact 数据库是*应用\_Data*文件夹中的文件，因此必须通过更改部署设置来防止此情况，以便不部署*应用\_Data*文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="296be-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="296be-141">打开 ContosoUniversity 项目的 "**项目属性**" 窗口，然后选择 "**打包/发布 Web** " 选项卡。确保 "**配置**" 下拉框中选择了 "**活动（发布）** " 或 "**发布**"，然后选择 **"从应用程序中排除文件\_Data 文件夹**。</span><span class="sxs-lookup"><span data-stu-id="296be-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="296be-143">如果你决定以后部署调试版本，则最好对调试生成配置进行相同的更改：将**配置**更改为 "**调试**"，然后选择 **"从应用程序中排除文件\_Data 文件夹**。</span><span class="sxs-lookup"><span data-stu-id="296be-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="296be-144">保存并关闭 "**打包/发布 Web** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="296be-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="296be-145">请确保在发布配置文件中选择的 "目标位置不**删除其他文件**"。</span><span class="sxs-lookup"><span data-stu-id="296be-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="296be-146">如果选择该选项，部署过程将删除已部署站点中的应用\_数据中的数据库，并将删除应用\_数据文件夹本身。</span><span class="sxs-lookup"><span data-stu-id="296be-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>

## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="296be-147">在更新过程中阻止用户访问生产站点</span><span class="sxs-lookup"><span data-stu-id="296be-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="296be-148">现在正在部署的更改是单个页面的简单更改。</span><span class="sxs-lookup"><span data-stu-id="296be-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="296be-149">但有时你会部署更大的更改，在这种情况下，如果用户在部署完成之前请求页面，则站点可能会奇怪。</span><span class="sxs-lookup"><span data-stu-id="296be-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="296be-150">若要防止出现这种情况，可以使用*应用\_脱机 .htm*文件。</span><span class="sxs-lookup"><span data-stu-id="296be-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="296be-151">在应用程序的根文件夹中将名为 "app" 的文件\_为 " *offline* " 时，IIS 会自动显示该文件，而不是运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="296be-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="296be-152">因此，若要在部署过程中阻止访问，请在根文件夹中将*应用\_为 offline* ，运行部署过程，然后删除*应用\_"脱机*"。</span><span class="sxs-lookup"><span data-stu-id="296be-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="296be-153">在**解决方案资源管理器**中，右键单击解决方案（不是项目之一），然后选择 "**新建解决方案文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="296be-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="296be-155">将文件夹命名为*SolutionFiles*。</span><span class="sxs-lookup"><span data-stu-id="296be-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="296be-156">在 "新建" 文件夹中，创建一个名为 app 的 HTML 页面 *\_offline*。</span><span class="sxs-lookup"><span data-stu-id="296be-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="296be-157">将现有内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="296be-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="296be-158">你可以通过使用 FTP 连接或托管提供程序控制面板中的**文件管理器**实用工具，将*应用\_脱机 .htm*文件复制到站点。</span><span class="sxs-lookup"><span data-stu-id="296be-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="296be-159">对于本教程，你将使用**文件管理器**。</span><span class="sxs-lookup"><span data-stu-id="296be-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="296be-160">打开 "控制面板"，选择 "**文件管理器**"，如您在[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)中所做的那样。</span><span class="sxs-lookup"><span data-stu-id="296be-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="296be-161">选择 " **contosouniversity.com** "，然后选择 " **wwwroot** " 获取应用程序的根文件夹，然后单击 "**上载**"。</span><span class="sxs-lookup"><span data-stu-id="296be-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="296be-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="296be-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="296be-163">在 "**上传文件**" 对话框中，选择 "*应用\_脱机 .htm*文件，然后单击"**上载**"。</span><span class="sxs-lookup"><span data-stu-id="296be-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="296be-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="296be-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="296be-165">浏览到你的站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="296be-165">Browse to your site's URL.</span></span> <span data-ttu-id="296be-166">此时将显示 "*应用\_offline* " 页，而不是主页。</span><span class="sxs-lookup"><span data-stu-id="296be-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="296be-167">[![App_offline。 htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="296be-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="296be-168">你现在已准备好部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="296be-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="296be-169">将代码更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="296be-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="296be-170">在**Web 一键式发布**工具栏中，选择 "**生产**" 发布配置文件，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="296be-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="296be-171">Visual Studio 将部署更新后的应用程序，并将浏览器打开到站点的主页。</span><span class="sxs-lookup"><span data-stu-id="296be-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="296be-172">将显示*应用程序\_脱机 .htm*文件。</span><span class="sxs-lookup"><span data-stu-id="296be-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="296be-173">必须先删除*应用\_脱机 .htm*文件，然后才能进行测试以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="296be-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="296be-174">返回到控制面板中的**文件管理器**应用程序。</span><span class="sxs-lookup"><span data-stu-id="296be-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="296be-175">选择**contosouniversity.com**和**wwwroot**，选择 " **app\_** "，然后单击 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="296be-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="296be-176">[![Deleting_app_offline .htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="296be-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="296be-177">在浏览器中，打开公共站点中的 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="296be-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="296be-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="296be-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="296be-179">现在，你已部署了一个不涉及数据库更改的应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="296be-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="296be-180">下一教程介绍如何部署数据库更改。</span><span class="sxs-lookup"><span data-stu-id="296be-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="296be-181">[上一页](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="296be-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
